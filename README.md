# 🎬 3D Projector Player — Admin Console

A secure web-based Admin Console for managing users and 3D video content for the 3D Projector Player desktop application.

**Live Demo:** [https://idyllic-lollipop-2954a9.netlify.app/](https://idyllic-lollipop-2954a9.netlify.app/)

---

##  Overview

The Admin Console is a single-page web application that allows administrators to:
- Manage and approve registered users
- Upload and encrypt 3D video content
- Monitor platform usage and storage statistics
- Send automated email notifications to users on approval or disapproval

---

##  Features

### User Management
- View all registered users with their email, role and last seen status
- Approve or disapprove users with a real-time toggle switch
- Bulk approve or disapprove multiple users at once
- Delete users from the platform
- Search and filter users by email

### Content Management
- Upload 3D video files with in-browser AES-256 encryption before upload
- Auto-generate and store AES encryption keys securely in the database
- Upload optional thumbnail images for each movie
- Set movie metadata — title, description, genre, rating, duration
- View, manage and delete existing movies
- Live upload progress tracking with speed and ETA display

### Overview Dashboard
- Total users count
- Approved users count
- Total movies count
- Pending approval count
- Storage usage per movie with visual progress bars

### Email Notifications
- Automated approval email sent to user when approved by admin
- Automated disapproval email sent when access is revoked
- Emails sent via Resend using custom domain

---

##  Tech Stack

| Technology | Purpose |
|-----------|---------|
| HTML5 | Page structure and layout |
| CSS3 | Styling, dark theme, responsive design |
| Vanilla JavaScript (ES6+) | All logic and interactivity |
| Web Crypto API | In-browser AES-256-CBC encryption |
| Fetch API | HTTP requests to Supabase |
| XMLHttpRequest | Upload progress tracking |
| Supabase Auth | Admin authentication and JWT tokens |
| Supabase Database (PostgreSQL) | User approvals, movie metadata, statistics |
| Supabase Storage | Encrypted video file storage |
| Supabase Edge Functions | Secure serverless operations |
| Resend | Automated email notifications |
| Netlify | Static site hosting and deployment |

---

##  Security Features

- **In-browser AES-256-CBC encryption** — Video files are encrypted before leaving the browser. The server never receives unencrypted content.
- **JWT authentication** — Admin session is managed via Supabase JWT tokens.
- **Row Level Security (RLS)** — All Supabase database tables have RLS policies enabled.
- **Just-In-Time key delivery** — Decryption keys are released only to authenticated and approved users via a secure Edge Function.
- **No framework dependencies** — Minimal attack surface with pure HTML/CSS/JS.

---

##  How It Works

### Video Upload Flow
```
Admin selects video file
        ↓
Browser generates AES-256 key
        ↓
Video encrypted in browser (Web Crypto API)
        ↓
Encrypted file uploaded to Supabase Storage
        ↓
AES key stored in Supabase Database
        ↓
Movie metadata saved (title, genre, duration etc.)
```

### User Approval Flow
```
User registers on desktop app
        ↓
Admin sees user in console → toggles approval ON
        ↓
Supabase Edge Function triggered
        ↓
Approval email sent to user via Resend
        ↓
User can now log in and play movies
```

### Secure Playback Flow
```
Approved user clicks Play in desktop app
        ↓
App calls Supabase Edge Function (get-video-key)
        ↓
Edge Function verifies JWT token + approval status
        ↓
AES key returned to app
        ↓
Video decrypted in memory (never written to disk)
        ↓
Video plays via LibVLCSharp
```

---

##  Deployment

This project is deployed as a static site on **Netlify** using Netlify Drop.

To deploy your own instance:
1. Create a free account at [netlify.com](https://netlify.com)
2. Go to [netlify.com/drop](https://netlify.com/drop)
3. Drag and drop the `index.html` file
4. Your console is live instantly

---

##  Configuration

The following values are configured inside `index.html`:

```javascript
const SUPABASE_URL = 'your_supabase_project_url'
const SUPABASE_ANON_KEY = 'your_supabase_anon_key'
```

Replace these with your own Supabase project credentials if you are hosting your own instance.

---

##  Project Structure

```
admin-console/
│
├── index.html          # Complete single-page admin console
└── README.md           # This file
```

---


### User Management
- View all registered users
- Toggle approval status
- Bulk operations

### Content Management
- Upload and encrypt videos
- Manage movie library
- Track storage usage

### Overview Dashboard
- Platform statistics
- Storage breakdown per movie

---

##  Related

- **3D Projector Player Desktop App** — Windows WPF application that consumes this admin console's content
- **Supabase Project** — Backend powering both the admin console and the desktop app
- **Resend** — Email service used for user notifications

---

##  Author

**Nitya Singh**
- Email: nityasingh2244@gmail.com
- Project: Built for Yuktavairagi — yuktavairagi.com

---

##  License

This project is proprietary and built for client use.
All rights reserved © 2026 Yuktavairagi.
