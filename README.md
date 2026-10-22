# 🚀 TechHub (The Tech Giants) — Full-Stack Platform

[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React 19](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite_6-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS v4](https://img.shields.io/badge/Tailwind_CSS_v4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)
[![Express 5](https://img.shields.io/badge/Express_5-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB_Atlas-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Google Gemini](https://img.shields.io/badge/Google_Gemini_AI-8E75B2?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)
[![Cloudinary](https://img.shields.io/badge/Cloudinary-3448C5?style=for-the-badge&logo=cloudinary&logoColor=white)](https://cloudinary.com/)
[![Supabase](https://img.shields.io/badge/Supabase_Storage-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)

> **TechHub** (by *The Tech Giants*) is a comprehensive, production-grade full-stack platform built for technology enthusiasts, software engineers, and computer science students. It integrates rich technical blogging, curated student study materials, real-time technology news, community interaction, and Google Gemini AI-driven semantic search.

---

## 📑 Table of Contents

1. [Executive Summary](#-executive-summary)
2. [System Architecture](#-system-architecture)
3. [Key Features](#-key-features)
4. [Technology Stack](#-technology-stack)
5. [Repository Structure](#-repository-structure)
6. [Database Schema & Data Models](#-database-schema--data-models)
7. [API Documentation](#-api-documentation)
8. [Frontend Pages & User Flows](#-frontend-pages--user-flows)
9. [AI & Cloud Integrations](#-ai--cloud-integrations)
10. [Security, Authentication & Moderation](#-security-authentication--moderation)
11. [Environment Variables](#-environment-variables)
12. [Installation & Local Development](#-installation--local-development)
13. [Deployment Guide](#-deployment-guide)
14. [Contributing & License](#-contributing--license)

---

## 🌟 Executive Summary

The Tech Giants platform bridges technical content creation, academic learning, and real-time industry awareness:
- **For Readers & Students**: Browse curated articles, search via AI across published blogs, bookmark articles to personal reading lists, access downloadable academic study notes (handwritten & printed PDFs), and stay updated with live news headlines.
- **For Writers & Admins**: Full-featured Markdown editor with live preview, automated Cloudinary media asset optimization, Gemini AI assistant for generating SEO-friendly titles and summaries, real-time reader engagement metrics, live user analytics, and note distribution controls.

---

## 🏗 System Architecture

The project is structured as a full-stack TypeScript monorepo with an Express REST API backend and a React (Vite) single-page application frontend.

```mermaid
flowchart TD
    subgraph Client["Frontend Client (React 19 + Vite + Tailwind CSS v4)"]
        UI["UI / Pages & Routing"]
        AuthCtx["AuthContext & Axios Interceptors"]
        MdEd["Markdown-it / ReactMarkdown"]
        Slider["News Ticker & Framer Motion"]
    end

    subgraph Server["Backend Server (Node.js + Express 5 + TypeScript)"]
        Router["Express Router & Controllers"]
        AuthMW["Auth Middleware & Argon2 / JWT / Passport"]
        RateLmt["Rate Limiters & Profanity Moderator"]
        MulterMem["Multer In-Memory Buffer"]
    end

    subgraph Services["External APIs & Cloud Infrastructure"]
        Mongo[("MongoDB Atlas Database")]
        Gemini["Google Gemini AI (3-Flash-Preview)"]
        Cloudinary["Cloudinary (Blog Cover Images)"]
        Supabase["Supabase (Notes PDF Storage)"]
        GNews["GNews API (Tech Top Headlines)"]
        GoogleOAuth["Google OAuth 2.0"]
        GoogleApps["Google Apps Script (Contact Form)"]
    end

    UI --> AuthCtx
    AuthCtx -->|REST API Requests with Bearer Token| Router
    Router --> AuthMW
    AuthMW --> RateLmt
    RateLmt --> MulterMem
    Router -->|Read / Write Documents| Mongo
    Router -->|RAG Smart Search & SEO Assist| Gemini
    MulterMem -->|Upload / Delete Images| Cloudinary
    Client -->|Direct PDF Upload & Download| Supabase
    Router -->|Fetch & Cache News (6h TTL)| GNews
    AuthMW -->|OAuth Handshake| GoogleOAuth
    UI -->|Submit Form Data| GoogleApps
```

---

## 🚀 Key Features

### 1. ✍️ Technical Blog Publishing
- **Interactive Markdown Editor**: Integrated `react-markdown-editor-lite` with `markdown-it` supporting live split-screen preview, headers, code snippets, lists, and formatted tables.
- **Reader Rendering Engine**: `react-markdown` augmented with `remark-gfm` (GitHub Flavored Markdown) and `rehype-raw` for rendering embedded HTML blocks, syntax formatting, and styling.
- **Cloudinary Image Optimization**: Direct memory-buffer uploads via Multer, generating responsive CDN URLs, and automated cleanup on post deletion or replacement.
- **Category Filtering & Search**: Instant client-side title search and dynamic category filtering (`Technology`, `Programming`, `Web Dev`, `Software`, `Hardware`, `AI`, `Gaming`, `Cyber Security`).
- **Engagement Tools**: View counts incremented per read, interactive user Likes, personal Reading List bookmarking, and native Web Share integration (Twitter/X).

### 2. 🧠 Google Gemini AI Integration
- **RAG-Style "Smart Search"**: Users can ask natural language technical questions via the global navigation bar. The backend synthesizes all published blog articles into context and prompts Google Gemini (`gemini-3-flash-preview`) to answer in under three sentences directly from the community's knowledge base.
- **Rate-Limited AI Protection**: Protected by `express-rate-limit` (15 requests per 15-minute window per IP) to prevent quota exhaustion and abuse.
- **Admin AI Writer Assistant**: Integrated button in the blog creation suite that analyzes article content and automatically drafts SEO-optimized titles or concise summaries.

### 3. 📰 Real-Time Tech News Ticker
- **Automated Headline Ingestion**: Consumes top tech headlines from the **GNews API**.
- **Smart 6-Hour Database Caching**: Stores news items in MongoDB to conserve API rate limits; refreshes only when the cached data exceeds 6 hours.
- **Infinite Looping Marquee**: Framer Motion ticker placed at the top of the Home view featuring article images, sources, and external links.

### 4. 📚 Academic Study Material Hub
- **Curated Student Notes**: Repository of university/college handwritten and typed notes categorized by subject and type (`handwritten` vs. `printed`).
- **Supabase Storage Integration**: Large PDF files are uploaded directly to a public Supabase Storage bucket (`materials`), preserving backend memory.
- **Auth-Gated Downloads**: Users must be signed in to download PDFs; guest users are prompted with a sleek login/signup modal.

### 5. 💬 Moderated Commenting System
- **Real-Time Community Discussion**: Nested discussion threads under every published article.
- **Automated Profanity & Blocklist Filter**: Custom filtering utility (`moderator.ts`) checks submissions against forbidden vulgarity and spam patterns before persisting to MongoDB.
- **Author Privileges**: Post authors and admins can delete comments directly from the article view or admin panel.

### 6. 👤 User Management & Real-Time Presence
- **Personalized User Dashboard**: Displays account details, joined date, and an active reading list tracker.
- **Heartbeat Active Presence**: The frontend issues an authenticated heartbeat ping every 2 minutes (`/api/users/heartbeat`), maintaining an accurate `lastActive` timestamp.
- **Live User Analytics**: Admins can see real-time concurrent active users (active within the last 5 minutes) alongside total registered user accounts.

### 7. 🛡️ Role-Based Access Control (RBAC) & Administration
- **Master Admin Dashboard**: Overview of total posts, cumulative views across all articles, active user counts, and quick management table.
- **Admin Analytics Screen**: Identifies top-performing articles sorted by view counts and likes leaderboard.
- **Route Protections**: Client-side `ProtectedRoute` guards and server-side `authenticate` and `isAdmin` middleware prevent unauthorized access to publishing tools.

---

## 🛠 Technology Stack

### Backend (`server/`)
| Category | Technology | Description |
| :--- | :--- | :--- |
| **Runtime** | Node.js (v18+) | Server-side JavaScript runtime |
| **Framework** | Express.js v5.2 | Web framework with routing and middleware |
| **Language** | TypeScript v5.9 | Type-safe enterprise JavaScript |
| **Database** | MongoDB Atlas / Mongoose v9.0 | Schema-based NoSQL object modeling |
| **Authentication** | JWT & Passport.js | Dual authentication: JSON Web Tokens & Google OAuth 2.0 |
| **Password Hashing** | Argon2 v0.44 | Modern, memory-hard hashing algorithm |
| **AI SDK** | `@google/generative-ai` v0.24 | Official Google Gemini API client |
| **Media Storage** | Cloudinary SDK v2.8 | Cloud asset hosting and media manipulation |
| **File Handling** | Multer v2.0 | In-memory multipart/form-data upload handling |
| **HTTP Client** | Axios v1.13 | External API requests (GNews) |
| **Email Service** | Nodemailer v7.0 | Password recovery email delivery |
| **Security & Utilities** | `express-rate-limit`, `cookie-parser`, `cors` | Rate limiting, cookie parsing, CORS controls |

### Frontend (`tech-blog-app/`)
| Category | Technology | Description |
| :--- | :--- | :--- |
| **Library** | React 19 | Declarative component UI library |
| **Build Tool** | Vite 6 | High-speed frontend build tool and dev server |
| **Language** | TypeScript 5.8 | Type-safe UI components and interfaces |
| **Styling** | Tailwind CSS v4 | Utility-first responsive CSS framework |
| **Animations** | Framer Motion v12 | Parallax scroll animations and smooth infinite news marquee |
| **Routing** | React Router DOM v7 | Client-side declarative routing and protected routes |
| **Cloud Storage** | `@supabase/supabase-js` v2.89 | Client-side file uploading to Supabase Storage |
| **Markdown** | `react-markdown`, `remark-gfm`, `rehype-raw`, `markdown-it`, `react-markdown-editor-lite` | Full-cycle Markdown authoring, parsing, and rendering |
| **Icons & UI** | `lucide-react`, `react-icons`, `react-hot-toast` | Modern icon sets and toast notifications |
| **Analytics/Charts** | `recharts` | Data visualization for performance analytics |
| **Date Formatting** | `date-fns` v4.1 | Date manipulation and relative distance calculations |

---

## 📂 Repository Structure

```text
the-tech-giants-private/
├── .vscode/
│   └── settings.json
├── server/                               # Backend Node.js / Express / TypeScript Application
│   ├── src/
│   │   ├── config/
│   │   │   ├── cloudinary.ts             # Cloudinary API credentials & v2 instance
│   │   │   └── passport.ts               # Google OAuth 2.0 Strategy configuration
│   │   ├── controllers/
│   │   │   ├── authController.ts         # Register, Login, Forgot & Reset Password
│   │   │   ├── blogController.ts         # Blog CRUD, Gemini Smart Search & AI Assist
│   │   │   ├── commentController.ts      # Comment management & profanity checks
│   │   │   ├── materialController.ts     # Study notes upload & retrieval
│   │   │   ├── newsController.ts         # GNews fetch & MongoDB cache controller
│   │   │   └── userController.ts         # Profiles, bookmarks, count, & heartbeat
│   │   ├── middleware/
│   │   │   ├── authMiddleware.ts         # JWT validation & Admin role verification
│   │   │   ├── multerConfig.ts           # MemoryStorage upload configuration
│   │   │   └── rateLimiter.ts            # Rate limiters for AI search & general APIs
│   │   ├── models/
│   │   │   ├── blog.ts                   # Blog Schema (views, likes, markdown, Cloudinary)
│   │   │   ├── comment.ts                # Comment Schema (author, blog relation)
│   │   │   ├── material.ts               # Material Schema (PDF link, category, type)
│   │   │   ├── news.ts                   # News Schema (cached headlines from GNews)
│   │   │   └── user.ts                   # User Schema (Argon2 hash, roles, bookmarks)
│   │   ├── routes/
│   │   │   ├── adminRoutes.ts            # Admin verification endpoints
│   │   │   ├── authRoutes.ts             # Authentication & OAuth callback routes
│   │   │   ├── blogRoutes.ts             # Blog operations & AI search endpoints
│   │   │   ├── commentRoutes.ts          # Article comment routes
│   │   │   ├── materialRoutes.ts         # Study material upload/list routes
│   │   │   ├── newsRoutes.ts             # News ticker routes
│   │   │   └── userRoutes.ts             # User profiles, bookmarks, and heartbeat
│   │   ├── types/
│   │   │   └── express.d.ts              # Custom TypeScript extensions for Express
│   │   ├── utils/
│   │   │   ├── moderator.ts              # Inappropriate content / profanity regex filter
│   │   │   └── tokens.ts                 # Access & Refresh JWT generation utilities
│   │   └── index.ts                      # Express app bootstrapper, CORS, and DB connection
│   ├── .env                              # Backend environment secrets
│   ├── .gitignore                        # Git exclusion rules for server
│   ├── package.json                      # Server dependencies and scripts
│   └── tsconfig.json                     # Server TypeScript compiler configuration
│
├── tech-blog-app/                        # Frontend React 19 / Vite / Tailwind Application
│   ├── public/
│   │   ├── favicon.svg                   # Application favicon
│   │   └── vite.svg                      # Vite logo
│   ├── src/
│   │   ├── api/
│   │   │   └── axios.ts                  # Axios instance with Bearer token interceptor
│   │   ├── assets/                       # Static SVGs and UI graphics
│   │   ├── components/
│   │   │   ├── Admin/
│   │   │   │   ├── AdminLayout.tsx       # Sidebar navigation layout for admin pages
│   │   │   │   ├── AdminMaterials.tsx    # Study materials management table
│   │   │   │   └── MaterialUpload.tsx    # Supabase PDF upload form
│   │   │   ├── Loader/
│   │   │   │   ├── PageLoader.tsx        # Initial application splash screen loader
│   │   │   │   └── PulseLoader.tsx       # Content placeholder skeleton loader
│   │   │   ├── User/
│   │   │   │   └── UserLayout.tsx        # Navigation sidebar layout for user pages
│   │   │   ├── BlogCard.tsx              # Grid card preview for blog posts
│   │   │   ├── CommentSection.tsx        # Comment thread and submission box
│   │   │   ├── Footer.tsx                # Global footer with social links
│   │   │   ├── Navbar.tsx                # Auto-hiding navbar with AI Smart Search input
│   │   │   ├── NewsSlider.tsx            # Infinite scrolling Framer Motion news ticker
│   │   │   ├── ProtectedRoute.tsx        # Route guard checking authentication & admin roles
│   │   │   └── SuccessModal.tsx          # Submission feedback dialog
│   │   ├── context/
│   │   │   └── AuthContext.tsx           # Global user authentication state provider
│   │   ├── pages/
│   │   │   ├── Admin/
│   │   │   │   ├── AdminAnalytics.tsx    # Blog performance, likes, and comment overview
│   │   │   │   └── AdminDashboard.tsx    # Master dashboard, metrics, and blog table
│   │   │   ├── Auth/
│   │   │   │   ├── Auth.tsx              # Login / Signup tabs & Google OAuth button
│   │   │   │   └── ResetPassword.tsx     # Password recovery form with token verification
│   │   │   ├── Blogs/
│   │   │   │   ├── BlogDetail.tsx        # Full markdown article view, likes, and bookmarks
│   │   │   │   ├── Blogs.tsx             # Library page with category selector and search
│   │   │   │   ├── CreateBlog.tsx        # Markdown editor with Gemini AI SEO assistant
│   │   │   │   └── SavedBlogs.tsx        # User's bookmarked reading list
│   │   │   ├── User/
│   │   │   │   └── UserDashboard.tsx     # User profile, account info, and reading metrics
│   │   │   ├── About.tsx                 # Platform vision and community mission
│   │   │   ├── Contact.tsx               # Contact form wired to Google Apps Script
│   │   │   ├── Home.tsx                  # Landing page with hero parallax and featured blogs
│   │   │   ├── NotFoundPage.tsx          # Custom 404 page
│   │   │   └── StudyMaterial.tsx         # Notes library with direct download handling
│   │   ├── utils/
│   │   │   └── markdown.ts               # Markdown helper functions
│   │   ├── App.css                       # Application root styling
│   │   ├── App.tsx                       # React Router configuration & heartbeat runner
│   │   ├── index.css                     # Tailwind CSS directives & global resets
│   │   ├── main.tsx                      # React root rendering with AuthProvider
│   │   ├── supabaseClient.ts             # Supabase client instantiation
│   │   └── vite-env.d.ts                 # Vite environment variable type declarations
│   ├── .env                              # Frontend environment variables
│   ├── .gitignore                        # Git exclusion rules for client
│   ├── eslint.config.js                  # ESLint configuration
│   ├── index.html                        # Application HTML entry template
│   ├── package.json                      # Client dependencies and scripts
│   ├── tsconfig.app.json                 # Client app TypeScript configuration
│   ├── tsconfig.json                     # TypeScript reference configuration
│   ├── tsconfig.node.json                # Vite node config TypeScript rules
│   ├── vercel.json                       # Vercel SPA routing rewrite rules
│   └── vite.config.ts                    # Vite build configuration with Tailwind plugin
└── README.md                             # Repository Master Documentation
```

---

## 🗄 Database Schema & Data Models

All models are defined using **Mongoose** for MongoDB Atlas:

### 1. `User` Model
```typescript
{
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true, lowercase: true },
  password: { type: String, required: function() { return !this.googleId; } },
  googleId: { type: String, unique: true, sparse: true },
  avatar: { type: String, default: '' },
  profilePic: { type: String, default: '' },
  role: { type: String, enum: ['user', 'admin'], default: 'user' },
  resetPasswordToken: { type: String, default: null },
  resetPasswordExpires: { type: Date, default: null },
  lastActive: { type: Date, default: Date.now },
  attendance: [{ date: Date, minutesSpent: Number }],
  bookmarks: [{ type: Schema.Types.ObjectId, ref: 'Blog' }],
  timestamps: true // createdAt, updatedAt
}
```
*Note: Passwords are automatically hashed via an Argon2 pre-save hook whenever modified.*

### 2. `Blog` Model
```typescript
{
  title: { type: String, required: true },
  slug: { type: String, unique: true, sparse: true, trim: true, lowercase: true, index: true },
  content: { type: String, required: true }, // Full Markdown text
  imageUrl: { type: String, required: true }, // Cloudinary secure CDN URL
  cloudinaryId: { type: String, required: false }, // Cloudinary asset ID for deletion
  author: { type: Schema.Types.ObjectId, ref: 'User' },
  views: { type: Number, default: 0 },
  category: { type: String, required: true },
  likes: [{ type: Schema.Types.ObjectId, ref: 'User', default: [] }],
  createdAt: { type: Date, default: Date.now },
  timestamps: true
}
```

### 3. `Comment` Model
```typescript
{
  content: { type: String, required: true },
  author: { type: Schema.Types.ObjectId, ref: 'User', required: true },
  blog: { type: Schema.Types.ObjectId, ref: 'Blog', required: true },
  createdAt: { type: Date, default: Date.now }
}
```

### 4. `Material` Model
```typescript
{
  title: { type: String, required: true },
  description: { type: String, required: true },
  category: { type: String, required: true },
  type: { type: String, enum: ['handwritten', 'printed'], required: true },
  fileUrl: { type: String, required: true }, // Public Supabase Storage download link
  timestamps: true
}
```

### 5. `News` Model
```typescript
{
  title: { type: String, required: true },
  description: { type: String },
  content: { type: String },
  url: { type: String, required: true, unique: true }, // Deduplication key
  image: { type: String },
  sourceName: { type: String },
  category: { type: String, default: 'technology' },
  publishedAt: { type: Date },
  timestamps: true
}
```

---

## 📡 API Documentation

### Base URL: `/api`

| Endpoint | Method | Auth Level | Description |
| :--- | :---: | :---: | :--- |
| **Authentication** | | | |
| `/auth/register` | `POST` | Public | Create new account with email & password |
| `/auth/login` | `POST` | Public | Login with credentials; returns JWT + sets refresh cookie |
| `/auth/google` | `GET` | Public | Starts Google OAuth 2.0 flow |
| `/auth/google/callback` | `GET` | Public | Google OAuth callback handler; redirects with token |
| `/auth/forgot-password` | `POST` | Public | Generates reset token & sends recovery email |
| `/auth/reset-password/:token` | `POST` | Public | Validates reset token and sets new Argon2 password |
| **Blogs** | | | |
| `/blogs/all` | `GET` | Public | Get all published blogs (newest first) |
| `/blogs/:id` | `GET` | Public | Get single blog by ID & increment view count |
| `/blogs/create` | `POST` | Admin | Create new blog with multipart image (`multer` + Cloudinary) |
| `/blogs/:id` | `PUT` | Admin/User | Update blog text and optionally replace cover image |
| `/blogs/:id` | `DELETE` | Admin | Delete blog and remove image from Cloudinary |
| `/blogs/like/:id` | `POST` | Authenticated | Toggle like state on a blog post |
| `/blogs/bookmarks/:id` | `POST` | Authenticated | Toggle bookmark state in user profile |
| `/blogs/smart-search` | `POST` | Rate-Limited | Query Google Gemini AI over all blog content |
| `/blogs/ai-assist` | `POST` | Admin | Prompt Gemini AI for SEO titles or content summaries |
| **Comments** | | | |
| `/comments/:blogId` | `GET` | Public | Get all comments for a specific blog post |
| `/comments/:blogId` | `POST` | Authenticated | Add a comment (screened through profanity moderator) |
| `/comments/:commentId` | `DELETE` | Authenticated | Delete a comment |
| `/comments/all-recent` | `GET` | Authenticated | Fetch globally recent comments for admin oversight |
| **Study Materials** | | | |
| `/materials` | `GET` | Public | List all downloadable study materials |
| `/materials/upload` | `POST` | Admin | Register metadata and Supabase PDF storage URL |
| `/materials/:id` | `DELETE` | Admin | Remove study material record from catalog |
| **News** | | | |
| `/news/latest` | `GET` | Public | Get top 10 tech news articles (cached 6 hours in DB) |
| **Users** | | | |
| `/users/me` | `GET` | Authenticated | Get current authenticated user details |
| `/users/profile` | `GET` | Authenticated | Get user profile with fully populated bookmarks |
| `/users/heartbeat` | `POST` | Authenticated | Update user's `lastActive` timestamp |
| `/users/stats` | `GET` | Admin | Get total registered users and live user count |
| `/users/count` | `GET` | Admin | Total number of registered regular users |
| **Admin** | | | |
| `/admin/stats` | `GET` | Admin | Admin-only connectivity verification |

---

## 🖥 Frontend Pages & User Flows

```text
/                      -> Landing Page (News Ticker, Animated Parallax Hero, Featured Posts)
├── /blogs             -> Full Library (Category Filtering, Instant Search, Blog Cards)
├── /blog/:id          -> Article Reader (Markdown Renderer, Likes, Bookmarks, Comments)
├── /study-material    -> Academic Notes Hub (Search, Category Filters, Direct PDF Download)
├── /about             -> About Us (Community Mission, Engineering Pillars)
├── /contact           -> Contact Form (Direct submit to Google Apps Script)
├── /privacy           -> Privacy Policy (Data collection, security, cloud services)
├── /auth              -> Authentication Portal (Login / Register Tabs, Google OAuth)
├── /reset-password/:t -> Password Reset Workflow
│
├── /dashboard         -> [User Protected] Account overview, reading progress
└── /dashboard/saved   -> [User Protected] Saved articles reading list
│
└── /admin             -> [Admin Protected] Master Dashboard (Post & View Metrics, Blog Table)
    ├── /admin/create  -> [Admin Protected] Markdown Blog Authoring + AI Assistance
    ├── /admin/edit/:id-> [Admin Protected] Edit existing post & replace imagery
    ├── /admin/analytics->[Admin Protected] Top views, likes leaderboard, recent comments
    ├── /admin/materials->[Admin Protected] Study notes catalog manager
    └── /admin/upload-notes->[Admin Protected] Direct Supabase PDF upload form
```

---

## 🤖 AI & Cloud Integrations

### 1. Google Gemini AI (`gemini-3-flash-preview`)
- **Smart Knowledge Retrieval**: When a query hits `/api/blogs/smart-search`, the backend aggregates the titles and Markdown bodies of all database articles. The model acts as a dedicated technical assistant, answering user questions strictly from the articles or acknowledging if a topic is not yet covered.
- **Admin Writing Assistance**: When authoring a post at `/admin/create`, the admin can click "Generate AI Title / Summary" to trigger `/api/blogs/ai-assist`, using Gemini to produce concise, SEO-friendly headlines.

### 2. Cloudinary CDN
- Manages all blog header images under the `tech_blogs` directory. Images are handled directly in memory by Multer and streamed to Cloudinary, ensuring the server filesystem remains stateless.

### 3. Supabase Cloud Storage
- Dedicated storage bucket: `materials`. Uploads are executed directly from the client using `@supabase/supabase-js`, returning a public CDN URL that is subsequently persisted to MongoDB.

### 4. GNews API
- Regularly fetches breaking headlines (`category=technology`, `lang=en`). The backend performs upsert operations keyed on the article URL, avoiding duplication and serving cached results within a 6-hour window to minimize external API costs.

---

## 🔒 Security, Authentication & Moderation

- **Password Security**: Argon2 memory-hard password hashing with salt, providing superior protection against GPU-based brute-force attacks.
- **Dual Token Architecture**:
  - `accessToken`: Short-lived JWT transmitted via HTTP `Authorization: Bearer <token>` header.
  - `refreshToken`: Stored in a secure, `httpOnly`, `sameSite: strict` cookie (7 days validity).
- **Google OAuth 2.0 Integration**: Managed using `passport-google-oauth20`. Links existing accounts with identical email addresses or registers new users automatically.
- **CORS Protection**: Whitelists authorized origins (`http://localhost:5173` for development and `https://the-tech-giants-private.vercel.app` for production).
- **Rate Limiting**: `aiSearchLimiter` caps requests to 15 per 15-minute window per IP to safeguard Gemini AI usage quotas.
- **Automated Content Moderation**: Comments are sanitized against whole-word profanity patterns (`moderator.ts`) before insertion into the database.
- **Production Build Hygiene**: Vite is configured with esbuild minification (`pure: ['console.log', 'console.debug']`, `drop: ['debugger']`) in production mode to completely eliminate client-side debug statements from shipping bundles.

---

## 🔑 Environment Variables

### Backend Configuration (`server/.env`)
```ini
# Server Configuration
PORT=5000
NODE_ENV=development

# Database
MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/techblog?retryWrites=true&w=majority

# JWT Secrets
JWT_SECRET=your_super_secret_jwt_key
REFRESH_SECRET=your_super_secret_refresh_key

# Cloudinary (Blog Images)
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Google Gemini AI
GEMINI_API_KEY=your_gemini_api_key

# GNews API (News Ticker)
GNEWS_API_KEY=your_gnews_api_key

# Google OAuth 2.0
GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_CALLBACK_URL=http://localhost:5000/api/auth/google/callback

# Client URLs (for redirects & CORS)
CLIENT_URL=http://localhost:5173
VITE_API_URL=http://localhost:5000/api
```

### Frontend Configuration (`tech-blog-app/.env`)
```ini
# Backend API Base URL
VITE_API_URL=http://localhost:5000/api

# Supabase Storage (Study Materials)
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your_supabase_anon_public_key
```

---

## 💻 Installation & Local Development

### Prerequisites
- [Node.js](https://nodejs.org/) (v18.0.0 or higher recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account and cluster connection string
- [Cloudinary](https://cloudinary.com/) account
- [Supabase](https://supabase.com/) project with a public `materials` storage bucket
- [Google Cloud Console](https://console.cloud.google.com/) OAuth 2.0 credentials
- [Google AI Studio](https://aistudio.google.com/) Gemini API Key

---

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-username/the-tech-giants-private.git
cd the-tech-giants-private
```

---

### Step 2: Configure & Start the Backend Server
```bash
cd server

# 1. Install dependencies
npm install

# 2. Create and fill in your .env file (see template above)
cp .env.example .env

# 3. Start the development server with live reload
npm run dev
```
*The backend API will start on `http://localhost:5000`.*

---

### Step 3: Configure & Start the Frontend Client
Open a new terminal window:
```bash
cd tech-blog-app

# 1. Install dependencies
npm install

# 2. Create and fill in your .env file
cp .env.example .env

# 3. Start the Vite development server
npm run dev
```
*The frontend application will start on `http://localhost:5173`.*

---

## 🚢 Deployment Guide

### Frontend Deployment (Vercel)
1. Push your repository to GitHub.
2. In the [Vercel Dashboard](https://vercel.com/), create a new project and select the `tech-blog-app` root directory.
3. Configure the build settings:
   - **Framework Preset**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
4. Add the Environment Variables:
   - `VITE_API_URL`: Your deployed backend API URL (e.g., `https://api.yourdomain.com/api`)
   - `VITE_SUPABASE_URL`: Your Supabase Project URL
   - `VITE_SUPABASE_ANON_KEY`: Your Supabase Anonymous Public Key
5. The included `vercel.json` ensures client-side routing works smoothly:
```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

### Backend Deployment (Render / Railway / VPS)
1. Deploy from the `server` directory.
2. Set the Environment Variables in your hosting dashboard matching `server/.env`.
3. Set the build and start commands:
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm start` (executes `node dist/index.js`)
4. In Google Cloud Console, update your **Authorized redirect URIs** to include your production callback:
   - `https://api.yourdomain.com/api/auth/google/callback`

---

## 🤝 Contributing & License

1. Fork the Project repository.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

Distributed under the **ISC License**. See `server/package.json` for details.

---

<p align="center">
  Built with ❤️ by <b>The Tech Giants</b> community.
</p>
