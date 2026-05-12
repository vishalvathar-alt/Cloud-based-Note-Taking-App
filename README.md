# CloudNotes Pro

A modern, responsive, cloud-based note-taking application built with Next.js 14 and Firebase.

## Features

- **Google Authentication**: Secure login using Firebase Auth.
- **Real-time Sync**: Notes sync across devices instantly using Firestore.
- **Full CRUD**: Create, read, update, and delete notes.
- **Tagging System**: Organize notes with custom tags.
- **Search & Filter**: Find notes by title, content, or specific tags.
- **Responsive UI**: Optimized for mobile and desktop screens.
- **Modern Tech Stack**: Built with TypeScript and Tailwind CSS.

## Prerequisites

- Node.js (v18.0.0 or higher)
- A Firebase Project

## Installation

1. Clone the repository
2. Install dependencies:
    `npm install`

## Configuration

1. Create a `.env.local` file in the root directory.
2. Add your Firebase configuration keys:
    `NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key`
    `NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com`
    `NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id`
    `NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project.appspot.com`
    `NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_id`
    `NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id`

## Firebase Setup

1. **Authentication**: Enable Google Login provider in the Firebase Console.
2. **Firestore Database**: 
   - Create a Cloud Firestore database.
   - Set up the following Security Rules:
    
    `service cloud.firestore {`
      `match /databases/{database}/documents {`
        `match /notes/{noteId} {`
          `allow read, write: if request.auth != null && (resource == null || request.auth.uid == resource.data.userId);`
        `}`
      `}`
    `}`

3. **Indexes**: If you see an error in the console about missing indexes for ordering, follow the link provided in the error log to generate the required index automatically.

## Running the App

Run the development server:
    `npm run dev`

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Deployment

The easiest way to deploy is using Vercel:
1. Push your code to GitHub.
2. Connect your repo to Vercel.
3. Add the Environment Variables from your `.env.local` to the Vercel project settings.
4. Deploy!

## Project Structure

- `src/app`: Next.js App Router pages and layouts.
- `src/components`: Reusable UI components (NoteCard, Modal, Sidebar, etc.).
- `src/context`: Auth state management.
- `src/lib`: Firebase SDK initialization and Firestore service logic.
- `src/types`: TypeScript interfaces for the application data models.
