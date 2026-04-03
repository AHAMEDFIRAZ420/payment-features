# 📦 Android Build Guide (APK Generation)

This guide explains how to transform the **PayPlatform** React web application into a standalone Android APK using **Capacitor**.

## 🛠 Prerequisites
Unlike the web development setup, building an APK requires native Android tools:

1.  **Android Studio**: [Download & Install](https://developer.android.com/studio).
2.  **Java JDK 17+**: Ensure `JAVA_HOME` is set in your environment variables.
3.  **Android SDK**: Installed via Android Studio (SDK Manager).
4.  **A Finished Web Build**: Your React app must be bug-free in the browser first.

---

## 🚀 Step 1: Install Capacitor
Run these commands in your project root to add the mobile bridge:

```bash
# Install Capacitor core and CLI
npm install @capacitor/core @capacitor/cli

# Install the Android platform support
npm install @capacitor/android
```

## 🚀 Step 2: Initialize Capacitor
Initialize the configuration. When prompted, use `PayPlatform` as the name and `com.payplatform.app` (or similar) as the ID.

```bash
npx cap init
```

> **Important:** Open the newly created `capacitor.config.ts` and ensure `webDir` is set to `'dist'` (which is the default output folder for Vite).

## 🚀 Step 3: Build the React Project
Capacitor wraps your **production build**, not your source code. You must build the web version first:

```bash
npm run build
```
*This creates the `/dist` folder.*

## 🚀 Step 4: Add & Sync Android
Now, tell Capacitor to create the Android project files based on your `/dist` folder:

```bash
# Create the 'android' folder
npx cap add android

# Sync your web code into the android folder
npx cap copy android
```

---

## 🏗️ Step 5: Generating the APK in Android Studio
Now we move from the command line to the official Android IDE.

1.  **Open Android Studio**.
2.  Select **"Open an Existing Project"** and navigate to your project's `/android` folder.
3.  Wait for **Gradle** to finish syncing (this may take a few minutes the first time).
4.  In the top menu, go to:
    **Build** > **Build Bundle(s) / APK(s)** > **Build APK(s)**.
5.  Android Studio will notify you when it's done. Click the **"Locate"** link in the popup to find your `app-debug.apk`.

---

## 📲 Step 6: Testing on a Real Device
1.  Enable **Developer Options** and **USB Debugging** on your Android phone.
2.  Plug your phone into your laptop.
3.  In Android Studio, click the **Green Play Button** (Run) at the top.
4.  The app will install and open automatically on your phone!

---

## 💡 Maintenance Commands
Whenever you make changes to your React code in the future, follow this "Update Loop":

```bash
npm run build          # Re-build web files
npx cap copy android   # Push changes to the android folder
# Then Build APK in Android Studio
```

---

### Pro-Tip for PayPlatform:
Since your project uses a **PostgreSQL** backend, remember that `localhost:5000` won't work on a real phone! You'll need to update your API base URL in `App.tsx` to your laptop’s **IP Address** (e.g., `http://192.168.1.5:5000`) so the phone can "see" your server over the same Wi-Fi.
