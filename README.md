Follow these steps to set up the project on your local machine.

### 1. Clone the Repository
Open your terminal and run:
```bash
git clone <your-repo-url>
cd payplatform-mobile
```

### 2. Install Dependencies
Ensure you have **Node.js** installed. Then, install the required packages:
```bash
npm install
```

### 3. Run the Development Server
Start the project locally:
```bash
npm run dev
```
Once started, the terminal will provide a local URL (usually `http://localhost:5173`).

---

## 🛠 How to View the Mobile Output
Since this is a web-based mobile app, it will look stretched on a standard desktop monitor. To view it as intended:

1.  Open the link in **Chrome** or **Edge**.
2.  Right-click and select **Inspect** (or press `F12`).
3.  Click the **Toggle Device Toolbar** icon (the phone/tablet icon) at the top left of the DevTools window.
4.  Select a device (e.g., **iPhone 14** or **Pixel 7**) from the dropdown menu.

---

## 🏗 Project Architecture
We have transitioned to a **Mobile-First Single Page Application (SPA)** structure.

### Key File Changes
* **`src/main.tsx`**: The entry point. It no longer uses a platform switcher; it renders the `App` component directly.
* **`src/App.tsx`**: The heart of the mobile application. It handles authentication logic, tab navigation (Dashboard, Payments, etc.), and global state (Dark Mode).
* **`src/App.css`**: Contains the consolidated mobile styles, including CSS variables for header heights and dark mode themes.

### Folder Structure
```text
src/
├── mobile/
│   ├── components/       # UI elements (Header, Navigation, Settings)
│   └── MobileApp.css     # (Deprecated - styles moved to App.css)
├── data/                 # Mock JSON data for payments and notifications
├── shared/               # TypeScript types and interfaces
├── Login/                # User authentication components
└── App.tsx               # Main mobile logic & Framer Motion transitions
```

---

## ✨ Key Features for Teammates

### 1. Animated Transitions
We use `framer-motion` for page transitions. 
* **Swiping**: Users can swipe left or right on the main content to switch between tabs.
* **Spring Physics**: Transitions use a "stiffness" of 300 for a snappy, native feel.

### 2. Smart Header
The `MobileHeader` is scroll-aware. It automatically collapses when the user scrolls down to maximize screen real estate and reappears on scroll-up.

### 3. Authentication Flow
The app checks `localStorage` for a `payplatform_token`.
* **Logged Out**: Displays the `LoginPage`.
* **Logged In**: Persists user session and dark mode preferences across refreshes.

### 4. Real-time Feedback
The app is designed to handle real-time data. Payments and Notifications are mapped from JSON data, making it easy to swap in a live WebSocket or API feed later.

---

## 💡 Tech Stack
* **Framework**: React (Vite)
* **Styling**: CSS3 (Variables & Flexbox)
* **Animation**: Framer Motion
* **Icons/UI**: Custom components in `./mobile/components`

> **Note:** When adding new features, ensure they are "thumb-friendly"—keep interactive elements within easy reach of the bottom of the screen!

---
