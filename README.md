# :musical_note: Music app

This project is a backend API for a music application, utilizing MongoDB for data storage and Express.js with TypeScript for the server-side logic. It allows for managing artists, albums, and tracks, including user authentication and authorization.

## 🎼 About the Project

This project provides a robust backend API for a music application. It allows users to manage artists, albums, and tracks, with features for publishing and unpublishing content. The API supports user authentication via traditional username/password or Google OAuth, and implements role-based access control.

## ✨ Features

- **Artist Management:** Create, view, update, and delete artists. Admins can publish/unpublish artists.
- **Album Management:** Create, view, update, and delete albums. Admins can publish/unpublish albums. Albums can only be published if their associated artist is published.
- **Track Management:** Create, view, update, and delete tracks. Admins can publish/unpublish tracks. Tracks can only be published if their associated album is published.
- **User Authentication:** Secure user registration and login using JWT. Supports Google OAuth for faster sign-in.
- **Authorization:** Role-based access control (admin/user) for certain operations.
- **Track History:** Users can log their listening history.
- **Image Uploads:** Supports uploading images for artists and albums.
- **Data Seeding:** Includes a script to populate the database with initial data.

## 🛠️ Tech Stack

- **Backend:** TypeScript, Node.js, Express.js
- **Database:** MongoDB (with Mongoose)
- **Frontend:** React, Redux Toolkit, Material-UI (MUI), React Router, Axios, Zod (for validation), React Toastify
- **Authentication:** JWT, Google OAuth
- **Other:** Multer (for file uploads), Argon2 (for password hashing), Dotenv (for environment variables)

## 📋 Installation

To get this project up and running locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/novikovaula007-rgb/music-app.git
    cd music-app
    ```

2.  **Install backend dependencies:**
    Navigate to the `api` directory and install the necessary packages:
    ```bash
    cd api
    npm install
    ```

3.  **Install frontend dependencies:**
    Navigate to the `frontend` directory and install the necessary packages:
    ```bash
    cd ../frontend
    npm install
    ```

4.  **Set up environment variables:**
    Create a `.env` file in the `api` directory based on `.env.template` and populate it with your MongoDB connection string and other necessary credentials (like `JWT_SECRET`, `CLIENT_ID`, `CLIENT_SECRET` for Google OAuth).
    ```
    # api/.env
    DB=mongodb://localhost:27017/your_db_name
    JWT_SECRET=your_jwt_secret
    CLIENT_ID=your_google_client_id
    CLIENT_SECRET=your_google_client_secret
    ```

5.  **Seed the database (optional):**
    You can seed the database with initial data by running the `seed` script in the `api` directory:
    ```bash
    npm run seed
    ```

6.  **Run the backend server:**
    Start the API server:
    ```bash
    npm run dev
    ```
    The API will typically run on `http://localhost:8000`.

7.  **Run the frontend development server:**
    Open another terminal, navigate to the `frontend` directory, and start the React development server:
    ```bash
    cd ../frontend
    npm run dev
    ```
    The frontend application will usually be accessible at `http://localhost:5173`.

## ▶️ Usage

This project is a full-stack music application where the backend API (`api` directory) serves data to a React frontend (`frontend` directory).

### Backend Use Cases:

-   **API Endpoints:** The backend exposes RESTful API endpoints for managing artists, albums, tracks, users, and track history. These are defined in the `api/routes` directory.
-   **Authentication & Authorization:** Handles user login, registration, and Google OAuth. It uses JWT for session management and middleware (`api/middleware`) to protect routes based on user roles and authentication status.
-   **Database Operations:** Interacts with MongoDB to perform CRUD operations on the music data models.

### Frontend Use Cases:

-   **Browse Artists:** View a list of artists, with options to publish/unpublish for admins.
-   **View Artist Albums:** Navigate to an artist's page to see their albums.
-   **View Album Tracks:** Navigate to an album's page to see its tracks.
-   **Create Content:** Authenticated users (or admins) can create new artists, albums, and tracks.
-   **Track Playback & History:** Listen to tracks and view your listening history.
-   **User Accounts:** Register, log in, and log out.

## 📚 API Reference

### Authentication Routes (`/users`)

-   `POST /users`: Register a new user.
-   `POST /users/sessions`: Log in a user.
-   `DELETE /users/sessions`: Log out a user.
-   `POST /users/google`: Log in/register with Google OAuth.

### Artist Routes (`/artists`)

-   `GET /artists`: Get all artists (published or user-owned).
-   `GET /artists/:artist_id`: Get a specific artist.
-   `POST /artists`: Create a new artist (requires authentication).
-   `DELETE /artists/:artist_id`: Delete an artist (requires authentication, owner or admin).
-   `PATCH /artists/:id/togglePublished`: Toggle artist published status (admin only).

### Album Routes (`/albums`)

-   `GET /albums`: Get all albums (published or user-owned, filterable by artist).
-   `GET /albums/:album_id`: Get a specific album.
-   `POST /albums`: Create a new album (requires authentication).
-   `DELETE /albums/:album_id`: Delete an album (requires authentication, owner or admin).
-   `PATCH /albums/:id/togglePublished`: Toggle album published status (admin only).

### Track Routes (`/tracks`)

-   `GET /tracks`: Get all tracks (published or user-owned, filterable by album).
-   `GET /tracks/:artist_id`: Get tracks by artist (filtered by albums).
-   `POST /tracks`: Create a new track (requires authentication).
-   `DELETE /tracks/:track_id`: Delete a track (requires authentication, owner or admin).
-   `PATCH /tracks/:id/togglePublished`: Toggle track published status (admin only).

### Track History Routes (`/track_history`)

-   `POST /track_history`: Record a track as played (requires authentication).
-   `GET /track_history`: Get the current user's listening history.
