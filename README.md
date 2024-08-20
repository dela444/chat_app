# Real-Time Chat Application

## Overview

This is a real-time chat application built with Node.js, Express.js, React.js, Socket.IO, Redis and PostgreSQL. The application includes features like user registration and authentication, real-time messaging with both chat rooms and private messages. Users can create and join chat rooms and the application implements message status tracking (sent, delivered, read). To enhance user experience, the frontend is built using React.js and Material-UI (MUI), ensuring a responsive and user-friendly interface.

Additional features include rate limiting to prevent spamming, as well as the ability to display user online/offline status.

Since Heroku discontinued its free tier, I deployed both the frontend and backend of my application on Vercel, with the database hosted on Supabase. However, Vercel has limitations regarding request execution time, particularly with Redis and sockets, but the application works smoothly in the local environment.

**Update**: To overcome the limitations encountered with Vercel, I have found a better solution by deploying the backend of the application on Render. This deployment has resolved the issues related to request execution time. You can access the live application here: [Chat Application Demo](https://chat-app-fe-seven.vercel.app).

In addition to the project description, I have also created a demo video providing a quick overview of the application. You can watch the demo video [here](https://youtu.be/Ii9fKDRG1-c).




## Repositories

This repository serves as the main overview for the chat application, which is split into two separate repositories:

- **[Frontend Repository](https://github.com/dela444/chat_app_fe)**: Contains the React.js application with Material-UI.
- **[Backend Repository](https://github.com/dela444/chat_app_be)**: Contains the Node.js/Express.js server with Socket.IO, Redis and PostgreSQL.

Setup instructions will be provided both in this repository and in the individual README files of each repository.

## Table of Contents

1. [Features](#features)
2. [Technologies Used](#technologies-used)
3. [Installation and Setup](#installation-and-setup)
4. [Project Structure](#project-structure)
5. [API Documentation](#api-documentation)
6. [Database setup](#database-setup)


## Features

- **User Registration and Authentication:** 
  - Users can register with a username and password.
  - After successful user authentication, a JWT (JSON Web Token) is issued to grant secure access for future requests.

- **Real-Time Messaging:**
  - Users can send and receive messages in real-time using Socket.IO.
  - Supports both chat rooms and private messages.
  - Users can create and join chat rooms.

- **Message Status Tracking:**
  - Messages are tracked with statuses: sent, delivered and read.

- **Rate Limiting:**
  - Rate limiting is implemented to prevent spamming, restricting users to a limited number of messages they can send per minute. Rate limiting is also applied to login and registration routes to protect against brute-force attacks and ensure system stability.
  
- **User Online/Offline Status:**
  - Displays the online/offline status of users in real-time.

- **Persistent Chat Rooms:**
  - Chat rooms are stored in the database, allowing users to create and join existing rooms.

- **Message Storage:**
  - All messages are stored in PostgreSQL and Redis and retrieved when necessary.
  - New users joining a chat room can see the most recent messages.
    
- **Responsive Frontend:**
  - Built with React.js and Material-UI (MUI) for a user-friendly and responsive interface.
 
## Technologies Used

### Backend:
- Node.js
- Express.js
- Socket.IO
- Redis
- PostgreSQL

### Frontend:
- React.js
- Material-UI (MUI)

### Authentication:
- JWT (JSON Web Tokens)

## Installation and Setup

Follow these steps to set up and run the project locally.

### Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) 
- [npm](https://www.npmjs.com/) or [Yarn](https://classic.yarnpkg.com/) (package managers for Node.js)
- [PostgreSQL](https://www.postgresql.org/) 
- [Redis](https://redis.io/) (for real-time messaging and rate limiting)
  
### Backend Setup

1. **Clone the Backend Repository:**
  ```bash
    git clone https://github.com/dela444/chat_app_be.git

    cd chat_app_be
  ```
2. **Update `package.json`:**

Open the `package.json` file and change the `name` property from:

```json
   {
    "name": "backend",
    "version": "1.0.0",
```
To:

```json
   {
    "name": "chat_app_be",
    "version": "1.0.0",
  }
```

3. **Update `package-lock.json`:**

Open the `package-lock.json` file and change the `name` property from:

```json
  {
    "name": "backend",
    "version": "1.0.0",
    "lockfileVersion": 2,
    "requires": true,
    "packages": {
      "": {
        "name": "backend",
```
To:

```json
  {
    "name": "chat_app_be",
    "version": "1.0.0",
    "lockfileVersion": 2,
    "requires": true,
    "packages": {
      "": {
        "name": "chat_app_be",
```

4. **Install Dependencies:**

  ```bash
  npm install
  ```

5. **Set Up Environment Variables:**

   Create a `.env` file in the root of the backend directory and add the following environment variables:
   
```bash
PORT=5000
JWT_SECRET=your_jwt_secret
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USER=your_db_user
DATABASE_PASSWORD=your_db_password
DATABASE_NAME=your_db_name
DATABASE_MAX=1000
DATABASE_TIMEOUT_MILLIS=30000
    
REDIS_HOST=your_reds_host
REDIS_PORT=your_redis_port
REDIS_PASSWORD=your_redis_password
 ``` 
6. **Start the Backend Server:**
 ```bash
  npm run dev
  ```

### Frontend Setup

1. **Clone the Frontend Repository:**

  ```bash
    git clone https://github.com/dela444/chat_app_fe.git

    cd chat_app_fe
  ```

2. **Update `package.json`:**

Open the `package.json` file and change the `name` property from:

```json
   {
    "name": "frontend",
    "version": "0.1.0",
    "private": true,
  }
```
To:

```json
   {
    "name": "chat_app_fe",
    "version": "0.1.0",
    "private": true,
  }
```

3. **Update `package-lock.json`:**

Open the `package-lock.json` file and change the `name` property from:

```json
   {
    "name": "frontend",
    "version": "0.1.0",
    "lockfileVersion": 2,
    "requires": true,
    "packages": {
      "": {
        "name": "frontend",
```

To:

```json
   {
    "name": "chat_app_fe",
    "version": "0.1.0",
    "lockfileVersion": 2,
    "requires": true,
    "packages": {
      "": {
        "name": "chat_app_fe",
```

4. **Install Dependencies:**

 ```bash
  npm install
  ```
5. **Set Up Environment Variables:**

   Create a `.env` file in the root of the backend directory and add the following environment variables:
   
  ```bash
  REACT_APP_FRONTEND_URL = 'http://localhost:3000'
  REACT_APP_BACKEND_URL = 'http://localhost:5000'
  ```
 
6. **Start the Frontend Server:**

 ```bash
  npm start
  ```

The frontend application should now be running on http://localhost:3000.

## Project Structure

This section provides an overview of the project structure for both frontend and backend of the application.

### Backend Project Structure

The backend project structure is organized as follows:
```bash
chat_app_be/
├── tests/
│ ├── controllers/
│ │ ├── authController.test.js
│ │ ├── chatController.test.js
│ │ └── redisController.test.js
│ └── socketio/
│ └── index.test.js
├── controllers/
│ ├── authController.js
│ ├── chatController.js
│ └── errorController.js
├── helpers/
│ ├── rateLimiter.js
│ ├── redisHelpers.js
│ └── validationHelpers.js
├── routes/
│ ├── auth.js
│ └── chat.js
├── socketio/
│ └── index.js
├── app.js
├── config.js
├── redis.js
├── package-lock.json
├── package.json
└── README.md
```
### Explanation

- **`__tests__/`**: Contains test files for controllers and socket.io functionality.
  - **`controllers/`**: Test files for different controllers.
  - **`socketio/`**: Test file for socket.io functionalities.
- **`controllers/`**: Contains the core logic for handling requests.
  - **`authController.js`**: Handles authentication logic.
  - **`chatController.js`**: Manages chat operations.
  - **`errorController.js`**: Custom Error class for error handling.
- **`helpers/`**: Contains utility functions and helpers.
  - **`rateLimiter.js`**: Utility function for rate limiting.
  - **`redisHelpers.js`**: Utility functions for Redis.
  - **`validationHelpers.js`**: Functions for validating input.
- **`routes/`**: Defines API routes.
  - **`auth.js`**: Routes for authentication.
  - **`chat.js`**: Routes for chat functionalities.
- **`socketio/`**: Contains the setup and management of socket.io.
  - **`index.js`**: Main file for socket.io setup.
- **`app.js`**: Entry point for the application.
- **`config.js`**: Configuration settings for database.
- **`redis.js`**: Redis connection setup.
- **`README.md`**: Documentation for the project.

### Frontend Project Structure

The frontend project structure is organized as follows:

```bash
chat_app_fe/
├── public/
│ ├── images/
│ │ └── images
│ ├── index.html
│ └── manifest.json
├── src/
│ ├── components/
│ │ ├── Authentication/
│ │ │ ├── Authentication.module.css
│ │ │ └── index.js
│ │ ├── Chat/
│ │ │ ├── Chat.module.css
│ │ │ └── index.js
│ │ ├── CreateRoomModal/
│ │ │ ├── CreateRoomModal.module.css
│ │ │ └── index.js
│ │ ├── ErrorPage/
│ │ │ └── index.js
│ │ ├── ProtectedRoute/
│ │ │ └── index.js
│ │ └── Sidebar/
│ │ ├── Sidebar.module.css
│ │ └── index.js
│ ├── constants/
│ │ └── appDefaults.js
│ ├── App.css
│ ├── App.js
│ ├── index.css
│ ├── index.js
│ ├── socket.js
│ └── UserContext.js
├── .gitignore
├── package-lock.json
├── package.json
└── README.md
```

## API Documentation

- **POST `/auth/register`**: Register a new user.
  - **Description**: This endpoint allows a new user to register with a username and password.
  - **Request Body**:
    ```json
    {
      "username": "string",
      "password": "string"
    }
    ```
  - **Response**:
    ```json
    {
      "success": true,
      "token": "string",
      "username": "string"
    }
    ```
    or error message.

- **POST `/auth/check-auth`**: Verify if the user is authenticated.
  - **Description**: This endpoint checks if the provided JWT is valid and if the user is authenticated.
  - **Request Headers**: `Authorization: Bearer <token>`
  - **Response**:
    ```json
    {
      "success": true,
      "token": "string",
      "username": "string"
    }
    ```
    or error message.

- **POST `/login`**: Authenticate a user and return a JWT.
  - **Description**: This endpoint allows an existing user to log in and receive a JSON Web Token (JWT) for authenticated access.
  - **Request Body**:
    ```json
    {
      "username": "string",
      "password": "string"
    }
    ```
  - **Response**:
    ```json
    {
      "success": true,
      "token": "string",
      "username": "string"
    }
    ```
    or error message.

- **POST `/create-room`**: Create a new chat room.
  - **Description**: This endpoint allows a user to create a new chat room.
  - **Request Body**:
    ```json
    {
      "name": "string",
    }
    ```
  - **Response**:
    ```json
    {
      "success": true,
    }
    ```
    or error message.

- **POST `/message`**: Store message to database.
  - **Description**: This endpoint stores new message to database.
  - **Request Body**:
    ```json
    {
      "message": "string",
      "from": "string",
      "recipient_id": "string",
      "recipient_type": "string"
    }
    ```
  - **Response**:
    ```json
    {
      "success": true,
      "message": "string",
      "message_id": "string",
      "creation_time": "string"
    }
    ```
    or error message.

### Error Message Format

Error messages follow a format:

```json
{
  "success": false,
  "status": "error",
  "message": "error message"
}
```

* `status`:
  * `"fail"` indicates that the operation could not be completed (e.g., invalid input or failed request).
  * `"error"` indicates an internal server error or unexpected issue that needs attention.

## Database Setup

To set up the database, execute the following SQL commands:

```sql
create table if not exists chat_users
(
    id       serial
        primary key,
    username varchar not null
        unique,
    password varchar not null,
    user_id  varchar not null
        unique
);

create table if not exists chat_rooms
(
    id      serial
        primary key,
    name    varchar not null
        unique,
    room_id varchar not null
        unique
);

create table if not exists messages
(
    id             serial
        primary key,
    content        varchar not null,
    message_id     varchar not null
        unique,
    sender_id      varchar not null
        constraint messages_chat_users_user_id_fk
            references chat_users (user_id),
    recipient_id   varchar not null,
    creation_time  varchar not null,
    recipient_type varchar not null
);

-- Insert initial users

insert into chat_users (username, password, user_id) values
('hamza', '$2b$10$CZiEiDEy2WOfrrAVODA0ReQ1wXp47KQWAKKo2kD9z1XZRTdADy.ue', '257c74fd-ba60-48a3-a7fd-80e76c65ef8f');

insert into chat_users (username, password, user_id) values
('delic', '$2b$10$V3jgiQgChJmxk3AF0ewntuOs/.IF/eFwHBcFzR13SdSRFxgDaNMf2', '8da54cf3-da93-42c8-a3b1-8debe0e064ca');

-- Insert initial chat rooms

insert into chat_rooms (name, room_id) values ('ChatRoom1', 'c5b7ba1c-9f25-4024-b6b5-af234f4975b0');

insert into chat_rooms (name, room_id) values ('ChatRoom2', '3780623d-688c-424b-9fb6-d208798b6ed6');

```
### Initial Data Setup

The following two initial users and two chat rooms have been created for easier testing of the application:

#### Users:
- **User 1**:
  - Username: `hamza`
  - Password: `hamzadelic`
- **User 2**:
  - Username: `delic`
  - Password: `delichamza`

### Chat Rooms:
- **Room 1**: `ChatRoom1`
- **Room 2**: `ChatRoom2`

The passwords for the users are encrypted in the database, but the credentials provided above can be used to log in.

  
