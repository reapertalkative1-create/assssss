> Cấu hình API mặc định trong Cài đặt cũng được mã hóa, kiểm tra và rotate bằng các lệnh bên dưới (migration 0011). Giữ database và khóa để không phải nhập lại API.

# Session encryption keys (Phase 4)

Telegram sessions are as sensitive as the account itself. They are stored **encrypted** (Fernet: AES-128-CBC + HMAC-SHA256)
and the key lives **outside the database**, so a stolen database dump or database backup alone is useless.
Every ciphertext is bound to its record (purpose + id), so rows cannot be swapped or replayed.

## Where the key lives
| Option | Setting | Notes |
|---|---|---|
| File (recommended) | `TFCC_SESSION_ENCRYPTION_KEY_FILE=/run/secrets/tfcc_session.key` | Must be `chmod 600`, owned by the API user. The API **refuses to start** if group/others can read it (POSIX). |
| Environment | `TFCC_SESSION_ENCRYPTION_KEY=<key>` | Fine for Docker secrets / systemd `EnvironmentFile` (mode 600). Never commit it. |

Generate: `python -m app.cli generate-key`. In production the API refuses to start without a key.
Without a key the rest of the dashboard works but account login/session features answer `503 encryption_not_configured`.

## Backup and restore of the KEY (do this on day one)
1. Store at least **two offline copies** of the key (password manager + printed/sealed copy in a safe place).
2. **Never** put the key in the same backup set as the database dump, and never in Git or chat.
3. Test the restore: on a staging copy restore the DB backup, supply the key, run `python -m app.cli verify-keys`
   (`sessions_failed` must be 0).
4. **If the key is lost, stored sessions cannot be recovered.** Accounts must be logged in again (phone + OTP).
   `verify-keys` tells you immediately whether the configured key matches the data.

## Rotating the key
1. `python -m app.cli generate-key` → new key.
2. Configure **both**, new first: `TFCC_SESSION_ENCRYPTION_KEY=<new>,<old>` (or both lines in the key file). Restart the API.
3. `python -m app.cli rotate-keys` re-encrypts every session/pending payload with the new key (audited as `keys.rotated`).
4. `python -m app.cli verify-keys` → `sessions_on_old_key` must be 0. Remove the old key. Back up the new one (see above).

## What is never stored or sent
- Per-account Telegram `api_id` / `api_hash` are entered through the dashboard, encrypted with purpose `telegram_app` bound to the account UUID, and released only to its authenticated assigned worker. Dashboard responses expose only a configured flag. Key verification and rotation include these encrypted pairs. Worker environment credentials remain a legacy fallback.
- The phone number is stored masked only. OTP codes and 2FA passwords travel dashboard → API → worker inside an encrypted,
  short-lived command payload that is **wiped as soon as the worker fetches it** (or when it expires); they are never audited or logged.
- Sessions are never in API responses, the frontend, logs, job payloads or on worker disks (workers keep them in memory).
- A worker can read a session only while it holds that account's lease, and every read is audited (`account.session_fetched`).

- SpamBot reports are encrypted with purpose `spam_report` bound to the account UUID. Outgoing appeal text uses encrypted command payloads, wiped on delivery; reports are included in key verification/rotation. Audit excludes the conversation text.

- Bulk appeal settings use purpose `appeal_settings` bound to the job UUID; rendered previews use `appeal_preview` bound to `job_id:account_id`. Both participate in key verification/rotation. Full phone/email values are temporarily present only in encrypted drafts/command payloads, with admin-only preview access.
