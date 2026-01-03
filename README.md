# Laravel File Uploader

A modern, responsive file uploader built with Laravel 12, Inertia.js, React 19, and Tailwind CSS v4. Features chunked uploads with pause/resume support, progress tracking, and file management.

## Features

- **Chunked File Uploads** - Large files are uploaded in chunks for reliability
- **Pause & Resume** - Control upload flow with pause/resume functionality
- **Real-time Progress** - Live upload progress with speed and time estimates
- **Drag & Drop** - Intuitive drag-and-drop interface
- **File Persistence** - Uploaded files are saved to database and disk
- **Download & Delete** - Manage uploaded files with ease
- **Responsive Design** - Works seamlessly on mobile, tablet, and desktop
- **Type-safe Routes** - Powered by Laravel Wayfinder for end-to-end type safety

## Tech Stack

- **Backend**: Laravel 12, PHP 8.4
- **Frontend**: React 19, Inertia.js v2
- **Styling**: Tailwind CSS v4
- **Build Tool**: Vite
- **Database**: SQLite (default)
- **Package Manager**: Composer (PHP), Bun (JS)

## Requirements

- PHP 8.4+
- Composer 2+
- Bun 1.0+
- Node.js 18+ (for Vite)

## Installation

1. Clone the repository:

```bash
git clone <repository-url>
cd laravel-uploader
```

2. Install PHP dependencies:

```bash
composer install
```

3. Install JavaScript dependencies:

```bash
bun install
```

4. Set up environment file:

```bash
cp .env.example .env
php artisan key:generate
```

5. Run database migrations:

```bash
php artisan migrate --force
```

6. Build assets:

```bash
bun run build
```

## Development

Start the development server with all services:

```bash
bun run dev
```

This runs:

- PHP server (localhost:8000)
- Vite dev server
- Queue worker
- Log viewer (pail)

## Production Build

```bash
bun run build
```

## Project Structure

```
app/
├── Console/
├── Exceptions/
├── Http/
│   ├── Controllers/
│   │   ├── HomeController.php
│   │   └── UploadController.php
│   ├── Middleware/
│   ├── Resources/
│   │   └── UploadResource.php
│   └── Requests/
├── Models/
│   └── Upload.php
└── Providers/
bootstrap/
database/
├── factories/
├── migrations/
│   └── 2026_01_03_105156_create_uploads_table.php
└── seeders/
resources/
├── css/
│   └── app.css
└── js/
    ├── app.tsx
    ├── components/
    │   ├── file-card.tsx
    │   ├── file-preview.tsx
    │   ├── hooks/
    │   │   ├── use-file-selection.ts
    │   │   └── use-files-drag-drop.ts
    │   ├── selected-files.tsx
    │   ├── uploader.tsx
    │   ├── upload-dropzone.tsx
    │   └── uploaded-files.tsx
    ├── lib/
    ├── pages/
    │   └── home.tsx
    └── types/
routes/
├── api.php
├── console.php
└── web.php
tests/
├── Feature/
├── Unit/
└── Pest.php
vite.config.ts
```

## API Endpoints

| Method | Endpoint                    | Description            |
| ------ | --------------------------- | ---------------------- |
| POST   | `/upload/chunk`             | Upload file chunks     |
| POST   | `/upload/abort`             | Abort ongoing upload   |
| GET    | `/upload/{upload}/download` | Download uploaded file |
| DELETE | `/upload/{upload}`          | Delete uploaded file   |

## Upload Flow

1. User selects files via click or drag & drop
2. Files are split into chunks (default: 2MB)
3. Chunks are uploaded sequentially
4. Progress is tracked with speed and time estimates
5. User can pause/resume at any time
6. On completion, file metadata is saved to database
7. Uploaded files appear in the "Recent Uploads" list

## Configuration

### Chunk Size

Modify chunk size in `resources/js/components/hooks/use-file-selection.ts`:

```typescript
const CHUNK_SIZE = 1024 * 1024 * 2; // 2MB default
```

### Storage

Default storage uses local disk. Configure in `.env`:

```env
FILESYSTEM_DISK=local
```

## Testing

Run all tests:

```bash
bun run test
```

Or with PHP Artisan:

```bash
php artisan test
```

## Code Quality

Format and lint code:

```bash
bun run format
bun run lint
bun run types
```

Or run all checks:

```bash
composer check
```

## License

MIT
