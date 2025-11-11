# Christian Evangelism Media (CEM)

A full-stack platform for distributing Christian evangelism media materials in 30 languages, with role-based administration and content management.

## Projects

### [cem-api](https://github.com/christian-evangelism-media/cem-api)

Backend API built with AdonisJS 6 and PostgreSQL.

**Features:**
- Role-based authentication and authorization (super_admin, admin, support, user)
- Multi-language media management with i18n support (30 languages)
- Order creation and tracking
- Cart management
- Email verification system
- Media visibility control (draft/published)
- Admin endpoints for user and content management
- RESTful API with session-based authentication

**Tech Stack:**
- AdonisJS 6
- PostgreSQL
- TypeScript
- Lucid ORM
- Vinejs validation

### [cem-web](https://github.com/christian-evangelism-media/cem-web)

Public-facing web application built with React and Vite.

**Features:**
- User authentication (register, login, logout)
- Browse and filter Christian evangelism media by language and type
- Shopping cart and order placement
- Address management
- Language preference system (affects media ordering)
- Multi-language UI support (30 languages via i18next)
- PDF viewing (digital and press-ready versions)
- Responsive design with dark mode
- Dynamic pagination based on screen height

**Tech Stack:**
- React 19
- TypeScript
- Vite
- TanStack Query (React Query)
- TailwindCSS v4
- DaisyUI
- i18next
- React Router

### [cem-ops](https://github.com/christian-evangelism-media/cem-ops)

Operations panel for managing the service.

**Features:**
- Dashboard with statistics
- User management (create, edit, role assignment)
- Media management (create, edit, delete, publish/unpublish)
- Order management (view, update status)
- Customer messaging system
- Role-based UI (features shown/hidden based on permissions)
- Media draft system (help creates drafts, admins publish)
- Inline role changes with permission checks
- Responsive design matching cem-web

**Tech Stack:**
- React 19
- TypeScript
- Vite
- TanStack Query
- TailwindCSS v4
- DaisyUI
- Luxon
- React Router

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

1. **Clone the repositories**
   ```bash
   git clone https://github.com/christian-evangelism-media/cem-api.git
   git clone https://github.com/christian-evangelism-media/cem-web.git
   git clone https://github.com/christian-evangelism-media/cem-ops.git
   ```

2. **Set up the API**
   ```bash
   cd cem-api
   npm install
   cp .env.example .env
   # Configure database credentials and generate APP_KEY
   node ace migration:run
   npm run dev
   ```

3. **Set up the Web App**
   ```bash
   cd cem-web
   npm install
   cp .env.example .env
   # Set VITE_API_URL=http://localhost:3333
   npm run dev
   ```

4. **Set up the Operations Panel**
   ```bash
   cd cem-ops
   npm install
   cp .env.example .env
   # Set VITE_API_URL=http://localhost:3333
   npm run dev
   ```

5. **Create the first super_admin**
   ```sql
   -- Connect to PostgreSQL
   PGPASSWORD=postgres psql -U postgres -d cem

   -- Promote a user to super_admin
   UPDATE users SET role = 'super_admin' WHERE email = 'your-email@example.com';
   ```

## Architecture

The platform follows a client-server architecture with separate public and operations frontends:

- **Public Frontend (cem-web)**: User-facing SPA for browsing and ordering media
- **Operations Frontend (cem-ops)**: Operations panel for managing content, orders, users, and customer service
- **Backend (cem-api)**: RESTful API with role-based access control and session-based authentication
- **Database**: PostgreSQL with JSONB fields for multi-language content

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
