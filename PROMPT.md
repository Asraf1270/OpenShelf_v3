# OpenShelf Migration Plan: Laravel + React + Inertia.js

This document contains a step-by-step guide and specific prompts for an AI agent to rebuild **OpenShelf** using a modern tech stack.

## Architecture Overview
- **Backend:** Laravel 11.x (PHP 8.2+)
- **Frontend:** React + Inertia.js (The Modern Monolith)
- **Styling:** Vanilla CSS / Tailwind (User's choice, but sticking to the premium Glassmorphic aesthetic)
- **Database:** MySQL
- **Microservices Strategy:** Starting with a Modular Monolith and extracting specific services (e.g., Notification Service, Media Service) as separate Laravel/Node.js instances.

---

## Phase 1: Initialization & Environment Setup

### Prompt 1: Initializing the Project
> "I want to rebuild my current PHP project 'OpenShelf' into a **Laravel + React + Inertia.js** application. 
> 1. Initialize a new Laravel 11 project in a sub-folder named `openshelf-v3`.
> 2. Install **Laravel Starter Kit (Breeze)** with **React + Inertia** stack.
> 3. Configure the `.env` file for local development.
> 4. Ensure the UI includes a dark mode toggle by default as per the current project's preference."

---

## Phase 2: Database Migration & Modeling

### Prompt 2: Database Schema Analysis & Migration
> "Analyze the existing `data/schema.sql` and `config/database.php` from the legacy project. 
> 1. Create Laravel migrations for all tables: `users`, `books`, `categories`, `borrow_requests`, `notifications`, `announcements`, `audit_logs`, and `donations`.
> 3. Ensure all foreign key constraints and indexes are correctly defined.
> 4. Create Eloquent Models for each table with proper relationships (e.g., User hasMany Books, Book belongsTo Category, etc.).
> 5. Implement 'Soft Deletes' for books and borrow requests."

---

## Phase 3: Authentication & User Management

### Prompt 3: Advanced Auth Logic
> "Migrate the authentication logic from the legacy project.
> 1. Implement email domain verification (only allowing specific university domains) during registration.
> 2. Update the `User` model to include fields like `phone_number`, `profile_image`, and `role` (user/admin).
> 3. Create a custom middleware to handle `admin` access.
> 4. Implement the 'Password Recovery' flow using Laravel's built-in features but customized to include the legacy OTP logic if necessary."

---

## Phase 4: Frontend Foundation & Design System

### Prompt 4: Design System & Layout
> "I want to maintain the **Premium Glassmorphic** aesthetic of the current project.
> 1. Create a `RootLayout` in React that includes a sticky header, a mobile-first navigation menu, and a theme toggle.
> 2. Define a global CSS file using HSL color variables for the glassmorphism effects (blur, borders, transparency).
> 3. Build a reusable `BookCard` component with hover animations and skeletal loading states."

---

## Phase 5: Core Feature - Book Discovery (Infinite Scroll)

### Prompt 5: Migrating Book Index & Search
> "Rebuild the main books discovery page (`books/index.php`).
> 1. Create a `BookController` with an `index` method that supports Inertia rendering.
> 2. Implement **Cursor-based Pagination** (matching the legacy v2.6.0 logic) to handle infinite scroll.
> 3. Create a React page `Books/Index` that uses `useInView` (Intersection Observer) to trigger pagination.
> 4. Implement the intelligent search and filtering system that updates the URL query parameters and fetches results without a full page reload."

---

## Phase 6: Borrowing Logic & Notifications

### Prompt 6: Borrowing Workflow
> "Implement the book borrowing system.
> 1. Create a `BorrowController` to handle requests, approvals, and returns.
> 2. When a borrow request is made, trigger a **Notification** (both in-app and via Email).
> 3. Use Laravel's Notification system to handle multi-channel alerts (Database + Mail).
> 4. Build a 'My Borrowed Books' React page with progress bars for due dates."

---

## Phase 7: Microservices Integration (Extraction)

### Prompt 7: Extracting the Notification Service
> "To move towards a microservices architecture, let's decouple the **Notification Service**.
> 1. Create a separate Laravel service (or a standalone Node.js app) specifically for handling emails and in-app alerts.
> 2. Set up a **REST API** or a **Message Queue (Redis/RabbitMQ)** to communicate between the main app and the Notification service.
> 3. Update the main OpenShelf app to dispatch notification events to this new service instead of sending them directly."

---

## Phase 8: Admin Dashboard & Reports

### Prompt 8: Admin Panel Rebuild
> "Rebuild the Admin Dashboard using **React + Inertia**.
> 1. Create a statistics overview with charts (using Chart.js or Recharts) showing book additions and borrow trends.
> 2. Build management tables for Users and Books with bulk action capabilities.
> 3. Implement the CSV export functionality for reports using a Laravel library like 'Maatwebsite/Laravel-Excel'."

---

## Final Steps: PWA & Deployment

### Prompt 9: PWA Implementation
> "The current project is a PWA. Let's carry that over.
> 1. Setup `vite-plugin-pwa` to generate the service worker and manifest.json.
> 2. Ensure offline support for the 'My Borrowed' page so users can see their due dates without internet.
> 3. Finalize the deployment script for a production environment."
