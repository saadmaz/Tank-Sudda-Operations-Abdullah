# Abdullah — Daily Field & Operations Tracker

A mobile-first, zero-typing daily field tracker for Tank Sudha & Euro Motors field management.

## 🚀 Live Hosting on Cloudflare Pages (`abd.tanksudda.com`)

### Step 1: Push Repository to GitHub
Make sure the latest code is committed and pushed to your GitHub repository:
```bash
git add .
git commit -m "Add index.html and Firestore database integration"
git push -u origin main
```

### Step 2: Connect to Cloudflare Pages
1. Log in to your [Cloudflare Dashboard](https://dash.cloudflare.com/).
2. In the left sidebar, click **Workers & Pages**.
3. Click **Create Application** > **Pages** tab > **Connect to Git**.
4. Select your GitHub repository: `saadmaz/Tank-Sudda-Operations-Abdullah`.
5. In the Build Configuration:
   - **Framework preset**: `None`
   - **Build command**: *(leave empty)*
   - **Build output directory**: `/` (or leave empty/root)
6. Click **Save and Deploy**. Your site will be live instantly on a `*.pages.dev` subdomain.

### Step 3: Attach Custom Domain (`abd.tanksudda.com`)
1. In your Cloudflare Pages project page, click the **Custom domains** tab.
2. Click **Set up a custom domain**.
3. Enter `abd.tanksudda.com` and click **Continue**.
4. If your root domain `tanksudda.com` is already on Cloudflare DNS, Cloudflare will automatically add the CNAME record and provision an SSL certificate with 1 click!
5. If `tanksudda.com` is managed on external DNS (e.g., Namecheap, GoDaddy):
   - Add a `CNAME` record:
     - **Name / Host**: `abd`
     - **Target**: `<your-project-name>.pages.dev`

---

## ☁️ Google Cloud Firestore Database Setup

The tracker stores and synchronizes daily morning plans and live field check-ins in real-time with offline support.

### 1. Create a Firebase Project
1. Go to the [Firebase Console](https://console.firebase.google.com/).
2. Click **Add Project** and give it a name (e.g., `tank-sudda-operations`).

### 2. Enable Firestore Database
1. In the Firebase console sidebar, navigate to **Build** > **Firestore Database**.
2. Click **Create database**.
3. Choose a region near you (e.g., `asia-south1` or `us-central1`).
4. Choose **Start in test mode** (allows read/write during setup).
5. For production security rules, navigate to the **Rules** tab in Firestore and paste:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /daily_logs/{date} {
      allow read, write: if true;
    }
  }
}
```

### 3. Get Your Firebase Config
1. In Firebase Console, click the ⚙️ **Project settings** icon (top-left).
2. Under the **General** tab, scroll down to **Your apps** and click the **Web (</>)** icon.
3. Register the app (e.g., `Tank Sudda Web Tracker`).
4. Copy the `firebaseConfig` object.

### 4. Apply Configuration (2 Easy Ways)

#### Option A: In the Web App UI (No code editing needed)
1. Open the hosted web app or `index.html`.
2. Tap the **Cloud DB / Local** pill in the top header.
3. Paste the Firebase config JSON directly into the box.
4. Tap **Save & Connect**. The indicator will turn **🟢 Synced**.

#### Option B: In `firebase-config.js`
Open `firebase-config.js` and replace the placeholder credentials:
```javascript
window.FIREBASE_CONFIG = {
    apiKey: "AIzaSy...",
    authDomain: "your-project-id.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project-id.appspot.com",
    messagingSenderId: "...",
    appId: "..."
};
```
Commit and push to GitHub, and Cloudflare Pages will automatically redeploy!

---

## 📱 Features

- **1-Tap Morning Plan**: Site Inspection, Brand Pitching, Quality QC, Havlock/Dehiwala/Kadawala Branch compliance and stock checks.
- **Field Check-In**: One tap logs completion with automatic timestamps.
- **Off-Plan Quick Log**: Instant recording of unplanned client visits and finance invoice handovers.
- **Offline Resilient**: Changes are stored in browser storage instantly, and automatically synced with Firestore as soon as cellular data reconnects.
- **WhatsApp Ready**: One-click formatted morning and EOD audit messages ready to paste into WhatsApp management groups.
