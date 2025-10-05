# SecureVault - Password Manager

A full-stack password manager built with React, TypeScript, Tailwind CSS, and Lovable Cloud (Supabase).

## Features

### 1. Authentication
- Email + password signup and login
- Passwords hashed with bcrypt
- Secure session management with JWT
- Auto-confirm email for development

### 2. Password Generator
- Adjustable password length (8-32 characters)
- Customizable options:
  - Include uppercase letters
  - Include lowercase letters
  - Include numbers
  - Include symbols
  - Exclude look-alike characters (O/0, l/1, etc.)
- Real-time password strength meter
- One-click copy with auto-clear clipboard after 15 seconds
- Rotating security tips

### 3. Secure Vault
- Create, read, update, delete password entries
- Each entry includes:
  - Title (required)
  - Username
  - Password (required, encrypted)
  - URL
  - Notes
- **Client-side AES-256 encryption** - server only stores encrypted data
- Search and filter functionality
- Per-user access control (users can only see their own passwords)

### 4. UI/UX
- Clean, minimal dashboard
- Sidebar navigation (Home, Generator, Vault)
- Dark mode toggle
- Fully responsive design (mobile + desktop)
- Modern gradient design with purple/blue theme

## Security Features

- ✅ Client-side encryption with AES-256-GCM
- ✅ Passwords never stored in plain text
- ✅ PBKDF2 key derivation (100,000 iterations)
- ✅ Row Level Security (RLS) policies in database
- ✅ Auto-clear clipboard after 15 seconds
- ✅ Input validation with Zod
- ✅ No secrets in logs or console

## Tech Stack

- **Frontend**: React 18, TypeScript, Vite
- **Styling**: Tailwind CSS, shadcn/ui components
- **Backend**: Lovable Cloud (Supabase)
- **Database**: PostgreSQL with Row Level Security
- **Authentication**: Supabase Auth
- **Encryption**: Web Crypto API (AES-256-GCM, PBKDF2)

## Setup Instructions

### Prerequisites
- Node.js 18+ and npm
- A Lovable account (backend is pre-configured)

### Installation

1. Clone the repository:
```bash
git clone <YOUR_GIT_URL>
cd <YOUR_PROJECT_NAME>
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser to `http://localhost:8080`

### First Time Setup

1. Navigate to `/auth` and create an account
2. Email confirmation is auto-enabled for development
3. Start using the password generator and vault!

## Project Structure

```
src/
├── components/          # React components
│   ├── ui/             # shadcn/ui components
│   ├── AppSidebar.tsx  # Navigation sidebar
│   ├── MainLayout.tsx  # Main app layout
│   ├── ThemeProvider.tsx
│   ├── ProtectedRoute.tsx
│   └── Vault*.tsx      # Vault-related components
├── contexts/           # React contexts
│   └── AuthContext.tsx
├── lib/               # Utilities
│   ├── crypto-utils.ts    # AES-256 encryption
│   ├── password-utils.ts  # Password generation
│   └── utils.ts
├── pages/             # Page components
│   ├── Auth.tsx       # Login/signup
│   ├── Home.tsx       # Dashboard
│   ├── Generator.tsx  # Password generator
│   └── Vault.tsx      # Password vault
└── integrations/
    └── supabase/      # Supabase client (auto-generated)
```

## Encryption Details

All passwords are encrypted **client-side** before being sent to the server:

1. **Key Derivation**: Uses PBKDF2 with 100,000 iterations and SHA-256
2. **Encryption**: AES-256-GCM with random IV and salt
3. **Storage**: Only encrypted blobs are stored in the database
4. **Decryption**: Only happens in your browser when you view a password

**Note**: For the demo, a default master password is used. In production, implement proper master password management with user prompts.

## Database Schema

### profiles
- `id` (UUID, primary key, references auth.users)
- `email` (text)
- `created_at` (timestamp)
- `updated_at` (timestamp)

### vault_items
- `id` (UUID, primary key)
- `user_id` (UUID, references auth.users)
- `title` (text, required)
- `username` (text, optional)
- `encrypted_password` (text, required)
- `url` (text, optional)
- `notes` (text, optional)
- `created_at` (timestamp)
- `updated_at` (timestamp)

## Security Best Practices

1. Never reuse passwords across sites
2. Use unique passwords for each account
3. Enable 2FA when available
4. Use the password generator for strong passwords
5. Store all credentials in the encrypted vault
6. Regularly update passwords for sensitive accounts

## Development

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Key Files

- `src/lib/crypto-utils.ts` - Encryption/decryption functions
- `src/lib/password-utils.ts` - Password generation and strength calculation
- `src/contexts/AuthContext.tsx` - Authentication state management

## Deployment

This project is configured to deploy via Lovable:

1. Click the **Publish** button in the Lovable interface
2. Your app will be deployed with backend included
3. Custom domains can be configured in Project Settings

## Support

For issues or questions:
- Check the [Lovable Documentation](https://docs.lovable.dev/)
- Join the [Lovable Discord](https://discord.gg/lovable)

## License

MIT License - feel free to use this project for your own password management needs!
