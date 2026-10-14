 # 🔐 Password Vault

A secure, client-side password manager that runs entirely in your browser. All credentials are encrypted with your master password and stored locally, so nothing is ever sent to a server.

## ✨ Features

- **Strong encryption:** AES-256-GCM, with the key derived from your master password using PBKDF2-SHA256 (600,000 iterations)
- **Local only:** the encrypted vault is stored in your browser's `localStorage`
- **Animated vault door:** unlock animation, plus a shake-and-glow warning on a wrong password
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
4. Start adding your credentials.

No installation, build step or server is required.

> **Note:** The Web Crypto API only works in a secure context. Open the file directly (`file://`), or serve it over `https://` or `localhost`.

## 🛡️ How It Works

| Step | Details |
|------|---------|
| Key derivation | Your master password and a random 16-byte salt go through PBKDF2-SHA256 (600k iterations) to produce a 256-bit key |
| Encryption | Credentials are serialized to JSON and encrypted with AES-GCM using a fresh 12-byte IV on every save |
| Storage | `{ version, salt, iv, data }` is saved in `localStorage` under the key `secure_password_vault` |
| Unlocking | The key is re-derived from your password; if decryption fails, the password is rejected |

Your master password and decrypted data exist only in memory while the vault is unlocked, and they are cleared when you lock it.

## ⚠️ Important

- **Your master password cannot be recovered.** If you forget it, your saved credentials are lost permanently.
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
