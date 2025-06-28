# 📱 OTA & State Management Overview

This document outlines the approach used for over-the-air (OTA) updates and state management in the Housr Student Living app built with React Native and Expo.

---

## 🚀 Over-the-Air (OTA) Updates

**Tooling:** Expo EAS Updates (`expo-updates`)

**Workflow:**

- Used the **Managed Workflow** with EAS to support rapid deployment cycles.
- Configured `eas.json` with separate channels:
  - `development` – for local testing
  - `preview` – internal QA
  - `production` – live users

**Key Practices:**

- OTA updates triggered via `eas update --channel preview/production`
- Runtime versioning managed via `app.config.js` using `expo-updates getRuntimeVersionAsync`
- In-app logic prompts users to reload when a new update is detected.
- Changes like layout fixes, copy updates, and minor bugs were deployed without needing full app store releases.

---

## ⚙️ State Management

**Library:** Zustand with TypeScript and AsyncStorage

**Why Zustand?**

- Minimal boilerplate
- Lightweight and easy to scale
- Better suited for React Native apps compared to Redux

**Store Structure:**

- `authStore`: Handles user session and token
- `userStore`: Profile, preferences, roles
- `bookingStore`: Manages room reservations, housing data

**Persistence:**

- State slices persisted using Zustand middleware + `AsyncStorage`
- Auto-rehydration on app launch
- Manual clear on logout

**Usage Highlights:**

- Global state for login status, booking filters, user preferences
- Triggers notifications and updates UI reactively
- Type-safe with strong typings for all store methods and slices

---

## 🔧 Deployment + QA

- GitHub Actions pipeline for CI
- OTA deployment logged and tracked via EAS dashboard
- Versioned rollback support using `expo-updates`
- OTA used primarily for:
  - Bug fixes
  - Copy/layout adjustments
  - Minor UX enhancements

---

### 📬 Questions?

Feel free to contact me if you'd like a walkthrough of the setup or see code examples from this implementation.
