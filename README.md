# Smart Media Content Factory

> **One upload. Every format.**

[![HackIndia Hackathon](https://img.shields.io/badge/HackIndia-Pixels_to_Products_2026-blue.svg)](https://hackindia.org/2026/pixels-to-products-cloudinary-ai-hackathon-2026)
[![Track 1](https://img.shields.io/badge/Track_1-AI_Media_Pipelines-indigo.svg)](#hackathon-track)
[![Cloudinary SDK](https://img.shields.io/badge/Cloudinary-SDK_v2_%26_AI_Engine-blue.svg)](https://cloudinary.com)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_%26_Firestore-orange.svg)](https://firebase.google.com)
[![Express Server](https://img.shields.io/badge/Backend-Node.js_%2F_Express_5-green.svg)](https://nodejs.org)
[![React Frontend](https://img.shields.io/badge/Frontend-React_19_%2F_Vite_8-cyan.svg)](https://react.dev)

A general-purpose smart media transformation and distribution engine for creators, marketers, photographers, sellers, and digital teams.

Upload one master image or video to generate, optimize, organize, and deliver platform-ready media across Social Media, Web, Profiles, Commerce, and video workflows.

The product combines three connected capabilities:

- **Image Media Factory** — one image into destination-specific visual formats.
- **Video Pipeline** — one source video into platform-ready MP4 variants.
- **Content Generation** — turn an existing visual asset into shareable motion content.

---

## Project Links & Demo

| Resource | Link | Note |
| :--- | :--- | :--- |
| **Live Application** | [(https://cloudinary-coral.vercel.app/)] | Live link |
| **Demo Video (2–4 min)** | `[ADD 2–4 MIN DEMO VIDEO URL]` | Working Demo |
| **Official GitHub Repo** | [(https://github.com/ilesh18/cloudinary)] | Main submission branch |

---

## Hackathon Track

### Track 1 — AI Media Pipelines

Submitted to **Track 1 — AI Media Pipelines** for the **Pixels to Products — Cloudinary AI Hackathon 2026**.

**Smart Media Content Factory** uses Cloudinary not as a passive file store, but as an active, programmatic media processing engine.

Images uploaded to the platform undergo automated ingestion signal analysis, background removal, content-aware reframing, preset-driven derived transformations, responsive `f_auto,q_auto` delivery, and context-indexed search.

Videos are handled as Cloudinary video resources and can be transformed into platform-ready MP4 variants.

The platform also includes a content-generation workflow that uses an existing visual asset as the starting point for creating shareable motion content.

---

## The Problem vs. The Solution

### The Problem

Visual distribution across modern digital platforms is highly repetitive and time-consuming:

- A single photo must be manually re-cropped for Instagram Posts (1:1), Stories (9:16), YouTube (16:9), Web Banners (1920x600), and Profile Avatars.
- Naive center cropping accidentally cuts off critical focal subjects like faces, logos, or products.
- Removing backgrounds or maintaining disjointed asset folders wastes hours and storage quota.
- A single video often needs different dimensions and delivery formats for different platforms.
- Turning an existing image into a polished social video can require additional editing tools and manual work.

### The Solution

**Upload once. Deliver everywhere.**

The platform ingests one master media asset and routes it through the appropriate processing pipeline.

For image media, the platform generates destination-specific variants across four core categories:

1. **SOCIAL**: Instagram Post, Instagram Portrait, Instagram Story / TikTok, YouTube Thumbnail, Social Square, Social Landscape.
2. **WEB**: Website Desktop Hero Banner, Website Mobile Banner.
3. **PERSONAL**: Profile Avatar / Thumbnail.
4. **COMMERCE**: Marketplace Square, Store Catalog, Product Thumbnail, Transparent Cutout PNG.

For video media, the Video Pipeline generates platform-ready MP4 variants.

For content generation, an existing visual asset can be transformed into shareable motion content without requiring the user to manually build the complete video from scratch.

---

## Two-Branch Composition Architecture

Smart Media Content Factory intelligently branches its image composition strategy based on media type:

```text
                       UPLOADED MASTER IMAGE
                                  │
                    CLOUDINARY INGESTION & ANALYSIS
                                  │
                  ┌───────────────┴────────────────┐
                  │                                │
      PRODUCT / OBJECT MEDIA             GENERAL / LIFESTYLE PHOTO
                  │                                │
      Cloudinary Background Removal        Cloudinary Content-Aware Crop
                  │                                │
       Cutout Layered Composition           Preserved Focal Subjects
                  │                                │
      (c_fit + c_lpad + b_rgb/white)       (f_auto, q_auto Reframing)
                  │                                │
                  └───────────────┬────────────────┘
                                  ▼
                       PLATFORM-READY TARGET FORMAT
```

### Product / Object Branch

Extracts object cutouts with Cloudinary:

```text
effect: 'background_removal'
```

and composes them inside padded canvas boundaries using:

```text
c_fit
c_lpad
b_rgb / white
```

This helps prevent important subjects from being clipped during destination-specific transformations.

### Lifestyle / Photography Branch

Uses Cloudinary content-aware gravity:

```text
gravity: 'auto'
```

to intelligently reframe important subjects while preserving the surrounding context of the original image.

---

# Video Pipeline

The Video Pipeline handles source videos independently from the image-processing pipeline.

The original video is preserved while Cloudinary generates platform-specific video variants.

## Video Pipeline Architecture

```text
                         UPLOADED VIDEO
                              │
                              ▼
                    CLOUDINARY VIDEO RESOURCE
                              │
                              ▼
                    VIDEO TRANSFORMATIONS
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
        REELS / SHORTS      SQUARE          YOUTUBE
        1080 × 1920       1080 × 1080      1920 × 1080
             │                │                │
             └────────────────┼────────────────┘
                              ▼
                     EXPLICIT MP4 DELIVERY
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                OPEN VIDEO          DOWNLOAD
```

### Supported Video Variants

| Platform | Dimensions | Aspect Ratio | Output |
| :--- | :--- | :--- | :--- |
| **Reels / Shorts** | `1080 × 1920` | `9:16` | `mp4` |
| **Square Video** | `1080 × 1080` | `1:1` | `mp4` |
| **YouTube / Landscape** | `1920 × 1080` | `16:9` | `mp4` |

### Video Processing

The source video can remain in its original format, including:

```text
MOV
MP4
```

Cloudinary is responsible for the actual video transformation and MP4 delivery.

The platform does not simply rename the source file from `.mov` to `.mp4`.

Instead, the pipeline requests an actual MP4 representation through Cloudinary's video transformation and delivery system.

### Video Delivery

Explicit MP4 variants are generated for the platform-specific outputs.

The resulting assets can be:

- Opened directly in the browser.
- Downloaded as MP4.
- Shared through their generated delivery URLs.
- Stored and referenced through the application's media workflow.

---

# Content Generation

Content Generation is the second major media workflow of the application.

Instead of starting with a blank video editor, the workflow starts with an existing visual asset.

## Content Generation Flow

```text
                         EXISTING IMAGE
                              │
                              ▼
                       CONTENT PURPOSE
                              │
                              ▼
                    CONTENT GENERATION
                              │
                              ▼
                     MOTION / COMPOSITION
                              │
                              ▼
                       SOCIAL-READY VIDEO
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                 OPEN                DOWNLOAD
```

The goal is to reduce the work required to turn an existing visual asset into a finished piece of shareable motion content.

The workflow is designed around the principle:

> **Start with the media you already have, then turn it into content ready for distribution.**

---

# Supported Image Preset Formats

| Category | Format Preset Name | Dimensions | Composition Strategy | Output Format |
| :--- | :--- | :--- | :--- | :--- |
| **Social** | Instagram Post | `1080 × 1080` | Cutout padded 80% scale on neutral canvas | `jpg` |
| **Social** | Instagram Portrait | `1080 × 1350` | Cutout padded 4:5 scale | `jpg` |
| **Social** | Instagram Story / TikTok | `1080 × 1920` | Cutout padded vertical safe margin | `jpg` |
| **Social** | YouTube Thumbnail | `1280 × 720` | Cutout centered 16:9 on dark backdrop | `jpg` |
| **Social** | Generic Social Square | `1080 × 1080` | Cutout centered on white background | `jpg` |
| **Social** | Social Landscape Share | `1200 × 630` | Cutout centered on 1.91:1 banner canvas | `jpg` |
| **Web** | Website Desktop Hero Banner | `1920 × 600` | Cutout east-aligned hero with text margin | `webp` |
| **Web** | Website Mobile Banner | `600 × 450` | Cutout centered 4:3 mobile container | `webp` |
| **Personal** | Profile / Avatar Thumbnail | `800 × 800` | Cutout centered 1:1 circular profile ratio | `jpg` |
| **Commerce** | Marketplace Square | `1000 × 1000` | Cutout centered 80% scale on white canvas | `jpg` |
| **Commerce** | Store Catalog | `1000 × 1000` | Cutout centered on off-white canvas | `jpg` |
| **Commerce** | Product Thumbnail | `300 × 300` | Cutout centered thumbnail scale | `jpg` |
| **Commerce** | Transparent Product | Native | Raw PNG cutout with transparent alpha channel | `png` |

---

# Key Features & Implementation Matrix

| Feature | Description | Technical Implementation |
| :--- | :--- | :--- |
| **Stream Upload** | Ingests high-resolution master media with metadata | `cloudinary.uploader.upload_stream` |
| **Signal Analysis** | Generates color palettes, quality scores, & watermark detection | `colors: true`, `quality_analysis`, `accessibility_analysis` |
| **Background Removal** | Server-side subject isolation without canvas manipulation | `effect: 'background_removal'` |
| **Smart Cropping** | Focal preservation for lifestyle/nature photos | `gravity: 'auto'` |
| **Preset Packs** | Batch generates Social, Web, Personal, and Commerce packs | Centralized `socialPresets` transformation registry |
| **Optimized Delivery** | Delivers optimal image formats and quality dynamically | `f_auto`, `q_auto` delivery parameters |
| **Asset Search API** | Real-time cross-catalog search using tags and context | `cloudinary.search.expression()` API |
| **ZIP Package Download** | Packages master and derived assets into structured ZIP archives | `JSZip` stream bundling |
| **Public Showcases** | Generates shareable public token URLs for external review | Token resolution mapping to Cloudinary URLs |
| **Video Pipeline** | Converts source videos into platform-ready explicit MP4 variants | Cloudinary video transformations and MP4 delivery |
| **Content Generation** | Turns an existing visual asset into shareable motion content | Content-generation workflow integrated with the media workspace |
| **Firebase Auth & Security** | Strict ownership checks and token verification on API routes | Firebase Admin SDK (`verifyIdToken`) |

---

# System Architecture

```mermaid
flowchart TD

    subgraph Client["React 19 + Vite 8 Client"]
        UI["User Interface Component"]
        AuthContext["Firebase Auth Context"]
        APIService["API Service Layer"]
    end

    subgraph Server["Node.js + Express Server"]
        Router["Express API Router"]
        AuthMiddleware["Firebase Token Verification"]
        CloudinaryService["Cloudinary Transformation Engine"]
        FirestoreConfig["Firebase Admin SDK"]
    end

    subgraph CloudinaryCloud["Cloudinary Engine"]
        UploadAPI["Upload Stream Ingestion"]
        AnalysisAI["Colors & Quality Signals"]
        BgRemoval["Background Removal Engine"]
        SmartCrop["Content-Aware Gravity Engine"]
        VideoPipeline["Video Transformation / MP4 Delivery"]
        SearchAPI["Search API Index"]
        CDN["Optimized CDN Delivery"]
    end

    subgraph FirebaseCloud["Firebase Platform"]
        FirebaseAuth["Firebase Authentication"]
        Firestore["Cloud Firestore DB"]
    end

    UI --> AuthContext
    AuthContext --> FirebaseAuth

    UI --> APIService
    APIService -->|"Bearer ID Token"| Router

    Router --> AuthMiddleware
    AuthMiddleware --> FirestoreConfig
    Router --> CloudinaryService

    CloudinaryService --> UploadAPI
    UploadAPI --> AnalysisAI
    UploadAPI --> BgRemoval
    UploadAPI --> SmartCrop
    CloudinaryService --> VideoPipeline
    CloudinaryService --> SearchAPI
    CloudinaryService --> CDN

    FirestoreConfig --> Firestore

    Router -->|"Delivery URLs & Metadata"| APIService
```

---

# Tech Stack

### Frontend

- React 19
- Vite 8
- Tailwind CSS 4
- Lucide React
- React Router DOM v7

### Backend

- Node.js
- Express 5
- Multer
- JSZip

### Media Infrastructure

- Cloudinary SDK v2
- Cloudinary Upload API
- Cloudinary Upload Stream
- Cloudinary Search API
- Cloudinary Image Transformations
- Cloudinary Video Transformations
- Cloudinary CDN
- `f_auto`
- `q_auto`
- Explicit MP4 delivery

### Database & Authentication

- Firebase Authentication
- Cloud Firestore
- Firebase Admin SDK

---

# Repository Structure

```text
cloudinary/
├── server/                       # Express Node.js Backend API
│   ├── src/
│   │   ├── config/
│   │   │   ├── cloudinary.js     # Cloudinary SDK configuration
│   │   │   └── firebaseAdmin.js  # Firebase Admin SDK setup
│   │   ├── controllers/
│   │   │   └── productController.js
│   │   ├── routes/
│   │   │   └── productRoutes.js
│   │   ├── services/
│   │   │   └── cloudinaryService.js
│   │   └── server.js
│   └── package.json
├── src/                          # React Client Application
│   ├── components/
│   ├── context/
│   │   └── AuthContext.jsx
│   ├── pages/
│   └── services/
│       └── api.js
├── .env.example
├── server/
│   └── .env.example
├── firestore.rules
├── package.json
└── README.md
```

---

# Quickstart & Local Setup

## 1. Prerequisites

- **Node.js**: v18+
- **Cloudinary Account**: Cloud Name, API Key, API Secret
- **Firebase Project**: Email/Password Authentication and Firestore

---

## 2. Environment Variables Setup

### Server `.env`

Create:

```text
server/.env
```

Add:

```env
PORT=5000
CLIENT_ORIGIN=http://localhost:5173

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

FIREBASE_PROJECT_ID=your_project_id
FIREBASE_CLIENT_EMAIL=your_client_email
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYOUR_KEY\n-----END PRIVATE KEY-----\n"
```

### Client `.env`

Create:

```text
.env
```

Add:

```env
VITE_FIREBASE_API_KEY=your_web_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project_id.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project_id.firebasestorage.app
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id

VITE_API_URL=http://localhost:5000
```

Never commit `.env` files or real credentials.

---

## 3. Installation & Start

```bash
# Clone the repository
git clone https://github.com/HackIndiaXYZ/pixels-to-products-cloudinary-ai-hackathon-2026-origin.git
cd pixels-to-products-cloudinary-ai-hackathon-2026-origin

# Install frontend dependencies
npm install

# Install backend dependencies
cd server
npm install
cd ..

# Terminal 1: Start backend
cd server
npm run dev

# Terminal 2: Start frontend
npm run dev
```

The frontend runs on the Vite development server and the backend runs on the configured Express port.

---

# Hackathon Verification Guide

Judges can verify Cloudinary integration directly inside the Cloudinary Dashboard.

### 1. Uploaded Media

Check the Cloudinary Media Library for uploaded assets.

Verify that:

- Images are stored as image resources.
- Videos are stored as video resources.
- Original media remains preserved.

### 2. Metadata and Tags

Inspect uploaded media for associated:

- Metadata
- Tags
- Analysis results
- Context information

where available.

### 3. Image Derived Assets

Inspect generated image transformations to verify that Cloudinary is performing:

- Resizing
- Cropping
- Content-aware transformations
- Background removal
- Format optimization

### 4. Video Variants

Upload a source video and inspect the generated variants:

- Reels / Shorts — `1080 × 1920`
- Square — `1080 × 1080`
- YouTube — `1920 × 1080`

The platform variants are delivered as explicit MP4 outputs.

### 5. Search

Verify that indexed metadata and generated assets can be searched through the application's Cloudinary Search integration.

### 6. Delivery

Open generated assets and inspect their Cloudinary delivery URLs and transformation parameters.

---

# Cloudinary Integration

Cloudinary is the core media engine of the application.

## Upload

Original media is uploaded through the Cloudinary Upload API using server-side processing.

For images, the application uses Cloudinary image resources.

For videos, the application uses Cloudinary video resources.

The original source remains preserved.

---

## AI Analysis

Where enabled and available, the application uses Cloudinary's media analysis capabilities for information such as:

- AI-generated tags
- Image quality signals
- Color information
- Watermark detection
- Image/content classification
- Other supported analysis metadata

Only results actually returned by Cloudinary are persisted and displayed.

---

## Background Removal

Cloudinary performs background removal on supported media.

The original image remains unchanged, while a processed representation can be used for product/object-focused compositions.

---

## Smart Cropping

Cloudinary intelligent/content-aware cropping is used for media formats where preserving the important subject is more useful than a basic center crop.

The platform uses:

```text
gravity: 'auto'
```

where appropriate.

---

## Video Processing

Video uploads are handled as Cloudinary video resources.

The Video Pipeline preserves the original source and generates explicit MP4 variants:

```text
Reels / Shorts
1080 × 1920

Square
1080 × 1080

YouTube / Landscape
1920 × 1080
```

The explicit MP4 variants use Cloudinary video transformations and MP4 delivery rather than simply renaming the source file.

A `.mov` source can therefore be transformed into a playable `.mp4` delivery variant without requiring the user to manually convert the original video first.

---

## Transformations

Destination-specific media variants are generated with Cloudinary transformations rather than client-side pixel manipulation.

Examples include:

- Resizing
- Cropping
- Content-aware gravity
- Product cutout composition
- Padding
- Layering
- Background/underlay composition
- Video reframing
- Video format conversion

---

## Optimized Delivery

Generated media uses Cloudinary optimized delivery where appropriate:

```text
f_auto
q_auto
```

This allows Cloudinary to select an appropriate delivery format and quality for supported image/web workflows.

For explicit platform video variants, the application requests MP4 delivery instead of relying on automatic image-format selection.

---

## Search

The application uses Cloudinary Search to find generated assets using indexed media information, tags, and associated metadata.

The Search API allows the Media Library to retrieve and filter real Cloudinary assets rather than relying on mock data.

---

## Metadata

Firestore stores the application-level relationships between:

- Users
- Source media
- Generated assets
- Asset type
- Platform
- Processing state

Cloudinary remains responsible for the actual media.

---

# End-to-End Workflow

```text
User uploads image or video
        ↓
Firebase-authenticated request
        ↓
Express backend
        ↓
Cloudinary upload
        ↓
Media-type-specific processing
        │
        ├── IMAGE
        │     ↓
        │   Cloudinary analysis
        │     ↓
        │   Background removal / smart crop
        │     ↓
        │   Destination-specific image transformations
        │
        └── VIDEO
              ↓
            Cloudinary video resource
              ↓
            Video transformations
              ↓
            Explicit MP4 variants
              ↓
              └──────────────┐
                             ▼
                    Generated Cloudinary Assets
                             ↓
                    Optimized Cloudinary Delivery
                             ↓
                       Firestore Metadata
                             ↓
                        Media Library
                             ↓
                 Search / Open / Download / Share
                             ↓
                 Content Generation when requested
```

---

# How It Works

## 1. Upload Once

The user uploads one master image or video.

The original media is preserved.

---

## 2. Analyze

Cloudinary analyzes supported image media and returns available:

- Tags
- Visual signals
- Color information
- Quality information
- Other configured analysis results

---

## 3. Choose the Workflow

The user can work with:

- Image destination formats
- Video platform variants
- Content generation

---

## 4. Transform

Cloudinary generates the requested destination-specific image or video variants.

---

## 5. Optimize

Generated media is delivered through Cloudinary's optimized delivery mechanisms.

For image/web workflows:

```text
f_auto
q_auto
```

For platform video outputs:

```text
MP4
```

is explicitly requested.

---

## 6. Organize

Firestore stores the relationship between:

- Authenticated user
- Source media
- Generated assets
- Asset type
- Platform
- Processing state

---

## 7. Search and Reuse

The user can:

- Search assets
- Open generated media
- Download individual assets
- Download generated packages
- Regenerate assets
- Share generated assets

---

# Security & Data Isolation

- **Server-Side Credentials**: Cloudinary API secrets and Firebase Admin credentials remain server-side.
- **Token Verification**: Protected Express routes verify Firebase Authentication ID tokens.
- **Ownership Checks**: API operations verify that the authenticated user owns the requested media.
- **Firestore Rules**: Firestore security rules isolate private user data by authenticated UID.
- **No Secret Frontend Exposure**: Server-only credentials are never placed in `VITE_` frontend variables.
- **Original Media Preservation**: Processing creates derived outputs without replacing the original source.

---

# Testing

## Basic Workflow

1. Create an account.
2. Log in.
3. Upload one image.
4. Confirm the upload succeeds.
5. Confirm Cloudinary receives the source media.
6. Confirm available AI/media analysis results appear.
7. Generate destination formats.
8. Open generated assets.
9. Search the Media Library.
10. Download an individual asset.
11. Download all available assets.
12. Generate a share link and open it.

---

## Image Testing

Test the application with:

- Product images
- Portrait photographs
- Landscape photographs
- Event photographs
- General photographs

Verify that the composition strategy preserves the important visual subject for each type.

---

## Video Pipeline Testing

Test with:

- `.mov`
- `.mp4`

Verify that:

1. The source video uploads successfully.
2. Cloudinary recognizes it as a video resource.
3. The original video remains preserved.
4. Reels output is generated as playable MP4.
5. Square output is generated as playable MP4.
6. YouTube output is generated as playable MP4.
7. Generated MP4 URLs open directly in a browser.
8. Generated videos can be downloaded.
9. The source does not need to be manually converted before processing.
10. The generated output dimensions match the requested platform preset.

---

## Content Generation Testing

Verify that:

1. An existing visual asset can enter the content-generation workflow.
2. The selected content-generation workflow starts successfully.
3. Generated motion content is associated with the source asset.
4. Generated content can be opened when generation completes.
5. Generated content can be downloaded when available.

---

## Security Testing

Verify that:

- Unauthenticated users cannot access protected application data.
- User A cannot access User B's private media.
- User A cannot regenerate User B's assets.
- User A cannot delete User B's products or media.
- Share links expose only intentionally shared content.
- Cloudinary API secrets are never exposed to the frontend.

---

# Deployment

## Frontend

The frontend can be deployed to Vercel.

Recommended settings for a root-level Vite application:

```text
Framework Preset: Vite
Build Command: npm run build
Output Directory: dist
Install Command: npm install
```

Frontend environment variable:

```env
VITE_API_URL=https://your-render-backend.onrender.com
```

---

## Backend

The Express backend can be deployed to Render.

Recommended settings when the backend lives inside `server/`:

```text
Root Directory: server
Build Command: npm install
Start Command: npm start
```

Required backend environment variables include:

```env
PORT=
CLIENT_ORIGIN=https://your-vercel-frontend.vercel.app

CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

FIREBASE_PROJECT_ID=
FIREBASE_CLIENT_EMAIL=
FIREBASE_PRIVATE_KEY=
```

Never place backend secrets in frontend environment variables.

---

# Hackathon Requirements

The project is built for the **Pixels to Products — Cloudinary AI Hackathon 2026**.

## Cloudinary

- Cloudinary is an active part of the product.
- Image and video media are uploaded through Cloudinary.
- Media is analyzed through Cloudinary where supported.
- Image media is transformed through Cloudinary.
- Video media is transformed through Cloudinary.
- Videos are delivered as platform-ready MP4 variants.
- Generated assets are delivered through Cloudinary.
- Cloudinary Search is used for asset discovery.
- `f_auto` and `q_auto` are used for optimized image/web delivery where appropriate.
- Explicit MP4 delivery is used for platform video variants.
- Cloudinary acts as the application's media processing and delivery infrastructure.

---

## Submission Materials

| Requirement | Status |
| :--- | :--- |
| Public GitHub Repository | Complete |
| README | Complete |
| Live Demo | Add final URL |
| 2–4 Minute Demo Video | Add final URL |
| Cloudinary Feedback Survey | Complete separately |

---

# Future Improvements

Potential future extensions include:

- Richer video editing controls
- Additional platform presets
- Batch media processing
- Advanced collaborative asset management
- More sophisticated composition strategies
- Expanded delivery workflows
- Broader content-generation controls
- Additional media automation workflows

These are future improvements and are not required for the current implementation.

---

# Acknowledgements

Built for the **Pixels to Products — Cloudinary AI Hackathon 2026**.

- Special thanks to **Cloudinary** for their media APIs and AI capabilities.
- Special thanks to **HackIndia** for organizing the hackathon.

---

> **Smart Media Content Factory — One upload. Every format.**
