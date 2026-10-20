# 🔐 Password Vault

A secure, client-side password maner that runs entirely in your browser. All credentials are encrypted with your master password and stored locally, so nothing is ever sent to a server.

## ✨ Features

- **Strong encryption:** AES-256-GCM, with the key derived from your master password using PBKDF2-SHA256 (600,000 iterations)
- **Local only:** the encrypted vault is stored in your browser's `localStorage`
- **Animated vault door:** unlock animation, plus a shake-and-glow warning on a wrong password
- **Account recovery:** a recovery key, shown once when you create the vault, lets you set a new master password if you forget it
- **Reset vault:** start over with an empty vault when neither the password nor the recovery key is available
- **Auto-lock:** the vault locks after 5 minutes of inactivity, with a live countdown
- **Password generator:** creates 20-character passwords with no randomness bias that always include uppercase, lowercase, numbers and symbols
- **Strength meter:** a color-coded bar that rates passwords as weak, medium or strong
- **Search:** filter saved credentials by site or username
- **One-click copy:** copy usernames and passwords to the clipboard
- **Show/hide passwords:** reveal a password with a decoding animation
- **Safe delete:** a two-click confirmation prevents accidental deletion
- **Responsive design:** works on desktop and mobile
- **Accessibility:** respects the "reduce motion" system setting

## 🚀 Getting Started

1. Download or clone this repository.
2. Open `index.html` in a modern browser (Chrome, Edge, Firefox or Safari).
3. Create a master password of at least 8 characters.
4. Save the recovery key that appears. Copy it or download it as a `.txt` file and keep it somewhere safe and offline.
5. Start adding your credentials.

No installation, build step or server is required.

> **Note:** The Web Crypto API only works in a secure context. Open the file directly (`file://`), or serve it over `https://` or `localhost`.

## 🛡️ How It Works

| Step | Details |
|------|---------|
| Data key | A random 256-bit key encrypts your credentials with AES-GCM, using a fresh 12-byte IV on every save |
| Password lock | Your master password and a random salt go through PBKDF2-SHA256 (600k iterations); the result encrypts ("wraps") the data key |
| Recovery lock | A random 32-character recovery key (160 bits) goes through PBKDF2-SHA256 (200k iterations) and wraps the same data key a second time |
| Storage | `{ version, salt, wrappedKey, recoverySalt, recoveryWrappedKey, iv, data }` is saved in `localStorage` under the key `secure_password_vault` |
| Unlocking | Either the master password or the recovery key can unwrap the data key; if decryption fails, the input is rejected |

Because the credentials are encrypted with the data key and not directly with your password, recovering or changing the master password only re-wraps the data key. Your saved credentials are never re-encrypted or exposed.

## 🔑 Forgot Your Master Password?

1. On the unlock screen, click **Forgot master password?**
2. Enter your recovery key. Dashes, spaces and letter case don't matter.
3. Choose a new master password and click **Recover vault**.

Your recovery key keeps working after recovery. To replace it, unlock the vault and click **Recovery key** in the header. This creates a new key and the old one stops working immediately.

If you've lost both the master password and the recovery key, choose **Reset vault instead** and type `DELETE` to confirm. This permanently erases the vault so you can start a new one.

> **Upgrading:** vaults created before recovery keys existed (version 1) are upgraded automatically the next time you unlock them, and a recovery key is shown to save.

The decrypted data key and your credentials exist only in memory while the vault is unlocked, and they are cleared when you lock it. Your master password and recovery key are never stored.

## ⚠️ Important

- **Save your recovery key.** It's shown only once. If you lose both it and your master password, your saved credentials are lost permanently.
- **Keep the recovery key private.** Anyone who has it and access to your browser can open your vault.
- **Clearing your browser data deletes the vault.** This includes site data and `localStorage`.
- **The vault belongs to one browser on one device.** It does not sync between browsers or devices.
- **Keep your device secure.** This tool cannot protect against malware or browser extensions that have access to the page.

## 🧰 Tech Stack

- HTML5 and CSS3 (animations, glassmorphism, responsive grid)
- Vanilla JavaScript
- Web Crypto API (`crypto.subtle`)
- Google Fonts: Space Grotesk and JetBrains Mono

## 📁 Project Structure

```
├── index.html   # Complete app (markup, styles and scripts)
└── README.md    # Documentation
```

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
