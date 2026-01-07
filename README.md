# ValACE Website Ecosystem: User Portal & CMS (FrontEnd)

![Framework](https://img.shields.io/badge/Frontend-React_18-blue)
![Build Tool](https://img.shields.io/badge/Build-Vite-purple)
![DevOps](https://img.shields.io/badge/Container-Docker_Compose-2496ED)
![Routing](https://img.shields.io/badge/Proxy-Nginx-009639)
![Status](https://img.shields.io/badge/Production-Live-success)

> **Project Context:** This is the official digital platform for the **Valenzuela City Academic Center for Excellence (ValACE)**. It consists of a public-facing **User Portal** for constituents to access services and a secure **Content Management System (CMS)** for library staff to update announcements and resources in real-time.

## 📖 System Overview

Moving beyond static websites, the ValACE platform is a dynamic Single Page Application (SPA) built to handle high traffic and frequent content updates. 

It separates the "Public View" from the "Admin View," allowing non-technical library staff to manage the website's content without needing to touch the codebase. The system uses a modern **React + Vite** architecture, containerized with **Docker**, ensuring consistency across development, staging, and production environments.

## 🎯 Key Capabilities

### 🏛️ Public User Portal
* **Dynamic Content Loading:** Fetches announcements, events, and facility statuses in real-time via the API.
* **Context-Driven State:** Utilizes React Context API (`APILayout.jsx`) for global state management, reducing prop-drilling.
* **Responsive Design:** Optimized for Valenzuela constituents accessing the site via mobile data.

### ⚙️ Content Management System (CMS)
* **No-Code Updates:** Admin dashboard allows staff to upload images and write announcements.
* **Analytics Integration:** Built-in connection to **Google Analytics (GA4)** to track visitor demographics and page engagement.

## 🏗️ Technical Architecture

This project implements a robust **Reverse Proxy Architecture** to handle API requests securely and avoid CORS issues in production.

* **Frontend:** React (Vite) for high-performance rendering.
* **Server:** Nginx acts as the web server and reverse proxy.
* **Routing Strategy:**
    * `/` (Root): Serves the React Static Files.
    * `/api/*`: Nginx forwards these requests to the backend server.
    
> **Why this matters:** This setup allows the frontend and backend to appear as the same origin to the browser, simplifying security headers and cookie management.

## 🛠️ Tech Stack & DevOps

| Layer | Technology | Description |
| :--- | :--- | :--- |
| **UI Framework** | React + Vite | Chosen for superior build speeds compared to CRA. |
| **State** | Context API | Lightweight state management for user sessions. |
| **Containerization** | Docker | Full support for `.env` injection and multi-stage builds. |
| **Orchestration** | Docker Compose | One-command deployment (`docker-compose up --build`). |
| **Linting** | ESLint | Enforces code quality standards across the dev team. |

## 🐳 Deployment Strategy

The application is fully "Dockerized" for rapid deployment. It supports environment-specific configurations via `.env` injection at runtime.

**Production Build Cycle:**
1.  **Build:** Vite compiles the source into optimized static assets in `/dist`.
2.  **Containerize:** Docker wraps the assets with an Nginx configuration.
3.  **Deploy:** The container listens on port `80` (or configured port), routing traffic internally.

```yaml
# docker-compose.yml snippet
services:
  frontend:
    build: .
    ports:
      - "${PORT}:80"
    environment:
      - VITE_API_HOST=host.docker.internal
