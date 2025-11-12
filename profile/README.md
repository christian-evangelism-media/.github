# Christian Evangelism Media (CEM)

A full-stack platform for distributing Christian evangelism media materials in 30 languages, with role-based administration and content management.

## Repository

### [cem](https://github.com/christian-evangelism-media/cem)

A monorepo containing all CEM applications with end-to-end type safety via Tuyau.

**Structure:**
```
cem/
├── packages/
│   ├── api/          Backend API (AdonisJS 6)
│   ├── web/          Public website (React 19)
│   ├── ops/          Staff operations panel (React 19)
│   └── scanner/      Mobile app for warehouse (Ionic/React)
├── package.json      Workspace configuration
└── .adonisjs/        Generated API types (Tuyau)
```

**Key Features:**
- End-to-end type safety between backend and all frontends via Tuyau
- Role-based authentication and authorization (super_admin, admin, support, help, user)
- Multi-language media management with i18n support (30 languages)
- Order creation and tracking
- Cart management
- Email verification system
- Media visibility control (draft/published)
- Customer messaging system
- Shopping cart and order placement
- Address management
- Language preference system
- PDF viewing (digital and press-ready versions)
- Barcode scanning for warehouse operations
- Health monitoring and emergency lockdown
- Maintenance mode control

**Tech Stack:**
- **Backend:** AdonisJS 6, PostgreSQL, Lucid ORM
- **Frontends:** React 19, TypeScript, Vite
- **UI:** TailwindCSS v4, DaisyUI
- **State:** TanStack Query
- **i18n:** i18next (frontend), @adonisjs/i18n (backend)
- **Mobile:** Ionic, Capacitor
- **Type Safety:** Tuyau
- **Email:** Resend

## Role-Based Permission System

### Roles
1. **super_admin** - Full system access, created via database
2. **admin** - Full service administration, created by super_admin
3. **support** - Customer service & account management, created by admin/super_admin
4. **help** - Warehouse/fulfillment & media draft creation, created by admin/super_admin
5. **user** - Public website access only (default)

### Key Permissions
- **Media Visibility**: Help creates drafts, admin/super_admin publish
- **User Management**: Admin can manage user/support/help roles, super_admin can create admins
- **Content Control**: Help can only edit their own unpublished media
- **Messages**: Support handles customer service, help does not
- **Orders**: All staff can view and update order status

## Getting Started

### Prerequisites

- Node.js 20+
- PostgreSQL 14+
- npm or yarn

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/christian-evangelism-media/cem.git
   cd cem
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up the API**
   ```bash
   cd packages/api
   cp .env.example .env
   # Configure database credentials and generate APP_KEY
   node ace migration:run
   cd ../..
   ```

4. **Set up environment files for frontends**
   ```bash
   # Web
   cp packages/web/.env.example packages/web/.env
   # Set VITE_API_URL=http://localhost:3333

   # Ops
   cp packages/ops/.env.example packages/ops/.env
   # Set VITE_API_URL=http://localhost:3333

   # Scanner
   cp packages/scanner/.env.example packages/scanner/.env
   # Set VITE_API_URL=http://localhost:3333
   ```

5. **Generate API types (critical for type safety)**
   ```bash
   npm run generate:types
   ```

6. **Run development servers**
   ```bash
   # Run all from monorepo root:
   npm run dev:api      # API on port 3333
   npm run dev:web      # Web on port 5173
   npm run dev:ops      # Ops on port 5174
   npm run dev:scanner  # Scanner on port 5175
   ```

7. **Create the first super_admin**
   ```sql
   -- Connect to PostgreSQL
   PGPASSWORD=postgres psql -U postgres -d cem

   -- Promote a user to super_admin
   UPDATE users SET role = 'super_admin' WHERE email = 'your-email@example.com';
   ```

### Important: Type Generation Workflow

When you modify API routes, controllers, or request/response structures, you MUST regenerate types:

```bash
npm run generate:types
```

This ensures all frontends have up-to-date TypeScript types from the backend.

## Architecture

The platform follows a monorepo architecture with multiple applications:

- **Backend (packages/api)**: RESTful API with role-based access control and session-based authentication
- **Public Frontend (packages/web)**: User-facing SPA for browsing and ordering media
- **Operations Frontend (packages/ops)**: Operations panel for managing content, orders, users, and customer service
- **Mobile App (packages/scanner)**: Ionic/React app for warehouse barcode scanning and order fulfillment
- **Database**: PostgreSQL with JSONB fields for multi-language content
- **Type Safety**: Tuyau generates TypeScript types from API routes, shared across all frontends

## Supported Languages

The platform supports 30 languages in ISO 639 format:
- Arabic (ar), Bengali (bn), German (de), Greek (el), English (en), Spanish (es)
- Persian (fa), French (fr), Hausa (ha), Hebrew (he), Hindi (hi), Haitian Creole (ht)
- Indonesian (id), Ilocano (ilo), Italian (it), Japanese (ja), Korean (ko), Marathi (mr)
- Punjabi (pa), Portuguese (pt), Romanian (ro), Russian (ru), Swahili (sw), Tamil (ta)
- Telugu (te), Tagalog (tl), Turkish (tr), Urdu (ur), Vietnamese (vi), Chinese (zh)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

All repositories are dual-licensed under MIT License and The Unlicense.
