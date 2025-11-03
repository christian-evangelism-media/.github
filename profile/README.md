# CEM Organization

A full-stack media management and ordering platform built with modern web technologies.

## Projects

### [cem-api](https://github.com/cem-org/cem-api)

Backend API built with AdonisJS 6 and PostgreSQL.

**Features:**
- User authentication and session management
- Media management (photos, videos, audio files)
- Order creation and tracking
- RESTful API with JSON responses

**Tech Stack:**
- AdonisJS 6
- PostgreSQL
- TypeScript
- Lucid ORM

### [cem-web](https://github.com/cem-org/cem-web)

Frontend web application built with React and Vite.

**Features:**
- User authentication (register, login, logout)
- Media browsing and filtering by type
- Shopping cart and order placement
- Multi-language support (English, Spanish, French)
- Dark/light theme toggle
- Responsive design

**Tech Stack:**
- React 18
- TypeScript
- Vite
- TanStack Query (React Query)
- Tailwind CSS
- i18next

## Getting Started

### Prerequisites

- Node.js 20+
- PostgreSQL 14+
- npm or yarn

### Setup

1. **Clone the repositories**
   ```bash
   git clone https://github.com/cem-org/cem-api.git
   git clone https://github.com/cem-org/cem-web.git
   ```

2. **Set up the API**
   ```bash
   cd cem-api
   npm install
   cp .env.example .env
   # Generate APP_KEY and configure database credentials
   node ace migration:run
   npm run dev
   ```

3. **Set up the Web App**
   ```bash
   cd cem-web
   npm install
   cp .env.example .env
   # Configure VITE_API_URL if needed
   npm run dev
   ```

## Architecture

The platform follows a client-server architecture:

- **Frontend**: Single-page application communicating with the backend via REST API
- **Backend**: RESTful API with session-based authentication using cookies
- **Database**: PostgreSQL with Lucid ORM for data persistence

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

See individual repositories for license information.
