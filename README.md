<p align="center">
  <img src="https://img.shields.io/badge/Type-Web%20App-4285F4?style=for-the-badge&logo=html5" alt="Type">
  <img src="https://img.shields.io/badge/Language-JavaScript-F7DF1E?style=for-the-badge&logo=javascript" alt="Language">
  <img src="https://img.shields.io/badge/Style-CSS3-1572B6?style=for-the-badge&logo=css3" alt="Style">
  <img src="https://img.shields.io/badge/Responsive-Mobile%20First-44CC11?style=for-the-badge&logo=googlechrome" alt="Responsive">
  <img src="https://img.shields.io/github/license/vijaykumarGK-Developer/rakthavahini-html?style=for-the-badge" alt="License">
</p>

<h1 align="center">🩸 Rakta-Vahini — Web App</h1>
<h3 align="center">Real-Time Blood Donation Network (HTML/CSS/JS Edition)</h3>

<p align="center">
  A fully responsive, single-page web application that connects blood donors with hospitals and individuals in urgent need.<br>
  This is the <strong>browser-based version</strong> of the <a href="https://github.com/vijaykumarGK-Developer/rakthavahini">Rakta-Vahini Android app</a>, built with vanilla HTML, CSS, and JavaScript — no frameworks, no build tools, no dependencies.
</p>

---

## ✨ Features

### 🔍 Intelligent Donor Discovery
- **Proximity-Based Search** — Find donors within a customizable radius (1–100 km) using the Haversine distance formula.
- **Live GPS Integration** — Fetch your real-time location via the Geolocation API for accurate distance matching.
- **Smart Scoring System** — Donors ranked by a composite score of distance, response speed, and donation frequency.
- **Blood Group Filter** — Dropdown selector for all 8 major blood groups (O+, O−, A+, A−, B+, B−, AB+, AB−).
- **Skeleton Loading** — Shimmer animation placeholders while search results are processing.

### 🚨 Emergency SOS System
- **One-Tap Broadcast** — Trigger an urgent SOS request specifying blood group and units needed via a modal bottom sheet.
- **Instant Alert** — Simulated push notification to nearby eligible donors and hospitals.

### 🏥 Hospital & Blood Bank Network
- **Verified Directory** — Curated list of hospitals with address, coordinates, email, and contact numbers.
- **One-Tap Call** — Click-to-dial for both mobile and landline numbers.

### 🏆 Heroism & Recognition
- **Certificate of Heroism** — Auto-generated digital certificate after every logged donation, with certificate ID and printable format.

### 🎨 Modern UI/UX
- **Mobile-First Design** — Optimized for mobile screens with a max-width of 420px, works on any device.
- **Dark Mode** — Full dark theme with persistent preference saved to `localStorage`.
- **Animated Navigation** — Smooth tab switching with active state indicators and icon scaling.
- **Haptic Feedback** — Vibrates on supported devices for critical interactions.
- **Slide-Out Overlays** — Fullscreen overlay panels for donor details, hospital info, settings, and certificates.
- **Snackbar Notifications** — Non-intrusive toast messages for user feedback.

### 👤 Dual Registration
- **Individual Donors** — Register with name, age, gender, blood group, phone, and address.
- **Hospitals** — Register as a verified institution with full contact details.

---

## 📱 Screenshots

```
┌─────────────────────┐  ┌─────────────────────┐  ┌─────────────────────┐
│                     │  │                     │  │                     │
│   Search Tab        │  │   User Profile      │  │   Settings          │
│   with Filters      │  │   Detail Overlay    │  │   Panel             │
│                     │  │                     │  │                     │
│        🔍           │  │        👤           │  │        ⚙️           │
│                     │  │                     │  │                     │
└─────────────────────┘  └─────────────────────┘  └─────────────────────┘
```

> ℹ️ *Open `index.html` in a browser to see the full app in action.*

---

## 🚀 Quick Start

No build tools or dependencies required. Just open the file in any browser:

```bash
# Clone the repository
git clone https://github.com/vijaykumarGK-Developer/rakthavahini-html.git

# Open directly in your browser
cd rakthavahini-html
open index.html           # macOS
start index.html          # Windows
xdg-open index.html       # Linux
```

Or serve it locally with any HTTP server:

```bash
# Python 3
python -m http.server 8080

# Node.js (requires npx)
npx serve .

# VS Code
# Install "Live Server" extension → Right-click index.html → Open with Live Server
```

Then open `http://localhost:8080` in your browser.

---

## 📂 Project Structure

```
rakthavahini-html/
├── index.html              # Single-page application (HTML + CSS + JS)
├── README.md               # You are here
└── LICENSE                 # MIT License
```

Everything is contained in a single `index.html` file — **no external dependencies, no frameworks, no build step**.

---

## 🏗 Architecture

The app is built as a **single-page application (SPA)** with vanilla JavaScript and follows these design patterns:

```
┌─────────────────────────────────────────────────────────────┐
│                     index.html                              │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────────┐ │
│  │ CSS      │  │ HTML     │  │ JS       │  │ localStorage│ │
│  │ (Themes, │  │ (Screens,│  │ (Logic,  │  │ (Persistence│ │
│  │  Layout) │  │  Overlays│  │  State)  │  │  Theme)     │ │
│  └──────────┘  └──────────┘  └──────────┘  └────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### State Management

Application state is managed through in-memory JavaScript arrays and objects:

| State Variable | Type | Description |
|---|---|---|
| `enrolledUsers` | `Array<Object>` | All registered donor profiles |
| `enrolledHospitals` | `Array<Object>` | Verified hospital directory |
| `myHistory` | `Array<Date>` | Personal donation history |
| `myLiveLocation` | `Object or null` | Current GPS coordinates |

### Tab Navigation

| Tab | ID | Render Function | Description |
|---|---|---|---|
| Search | `search` | `renderSearch()` | Donor discovery with filters |
| Profile | `profile` | `renderProfile()` | Dual registration form |
| Hospitals | `hospitals` | `renderHospitals()` | Hospital directory |
| Users | `users` | `renderUsers()` | All registered donors |
| History | `history` | `renderHistory()` | Donation activity feed |

---

## 🧩 Features Deep Dive

### Smart Scoring Algorithm

Donors are ranked for relevance using this formula:

```
smartScore = distance + (responseSpeed × 0.1) + (activeDaysAgo × 0.5) - (freq × 0.2)
```

**Factors:**
- `distance` — Geographic proximity (km)
- `responseSpeed` — Historical response time rating
- `activeDaysAgo` — Recency of activity
- `freq` — Lifetime donation count

Lower scores indicate better matches. The top-ranked donor receives a `🌟 Best Match` badge.

### Eligibility Enforcement

A strict **90-day cooling period** is enforced:

```javascript
const daysSince = (new Date() - donor.lastDonation) / (1000 * 60 * 60 * 24);
donor.isEligible = daysSince > 90;
```

Donors who have donated within the last 90 days are excluded from search results and marked with a `🚫 Cooling Period` badge.

### Haversine Distance Calculation

Uses the standard Haversine formula for accurate geographic distance:

```javascript
function calculateDistance(lat1, lon1, lat2, lon2) {
    const R = 6371;
    const dLat = (lat2 - lat1) * Math.PI / 180;
    const dLon = (lon2 - lon1) * Math.PI / 180;
    const a = Math.sin(dLat/2)**2 + Math.cos(lat1*Math.PI/180) * Math.cos(lat2*Math.PI/180) * Math.sin(dLon/2)**2;
    return (R * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a))).toFixed(1);
}
```

### Dark Mode

Theme preference is persisted using `localStorage`:

```javascript
function toggleTheme(isDark) {
    if(isDark) {
        document.body.classList.add('dark-theme');
        localStorage.setItem('theme', 'dark');
    } else {
        document.body.classList.remove('dark-theme');
        localStorage.setItem('theme', 'light');
    }
}

// Restore on load
if(localStorage.getItem('theme') === 'dark') {
    document.body.classList.add('dark-theme');
}
```

---

## 🛠 Tech Stack

| Technology | Usage |
|---|---|
| **HTML5** | Semantic markup, single-file structure |
| **CSS3** | Custom properties (variables), Flexbox, animations, transitions, responsive design |
| **Vanilla JavaScript** | DOM manipulation, Geolocation API, localStorage, event handling, state management |
| **Geolocation API** | Real-time GPS location capture |
| **Vibration API** | Haptic feedback on supported devices |
| **Windows 95 Sound Effect** | Nostalgic `img` references (decorative) |

### Zero Dependencies

No frameworks (React, Angular, Vue), no build tools (Webpack, Vite), no package managers (npm, yarn). Just a single `index.html` that works everywhere.

---

## 📖 Usage Guide

### 🩸 As a Donor

1. **Register** — Go to the Profile tab, fill in your details as an Individual, and save.
2. **Enable Location** — Click "Fetch My Live Location" on the Search tab for accurate distance matching.
3. **Search** — Use the Search tab to find donation opportunities matching your blood group.
4. **Respond** — Click a donor card for full details and tap "Secure Call" to coordinate.
5. **Log Donations** — After donating, use "I Donated Today" to generate your Certificate of Heroism.

### 🏥 As a Hospital

1. **Register** — Switch to Hospital mode in the Profile tab and fill in your facility details.
2. **Broadcast Needs** — Tap the SOS button (🚨) to request specific blood groups and units.
3. **Track** — Monitor the Users tab for eligible donors in your area.

### 🎖 Earning Recognition

- Each logged donation generates a **Certificate of Heroism** with your name, date, and unique certificate ID.
- Certificates are printable directly from the browser.

---

## 🌐 Browser Support

| Browser | Support |
|---|---|
| Chrome | ✅ Fully supported |
| Firefox | ✅ Fully supported |
| Safari | ✅ Fully supported |
| Edge | ✅ Fully supported |
| Opera | ✅ Fully supported |
| Samsung Internet | ✅ Fully supported |

Requires a modern browser with JavaScript and Geolocation API support.

---

## 🤝 Contributing

Contributions are welcome! Since this is a single-file app, contributions are straightforward.

### Workflow

1. **Fork** the repository.
2. **Create a feature branch:**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make your changes** in `index.html`.
4. **Commit your changes:**
   ```bash
   git commit -m "feat: add amazing feature"
   ```
5. **Push to the branch:**
   ```bash
   git push origin feature/amazing-feature
   ```
6. **Open a Pull Request.**

### Guidelines

- Keep the single-file architecture — no external dependencies.
- Follow the existing code style (vanilla JS, CSS custom properties).
- Test in multiple browsers before submitting.
- Add comments for complex logic.
- Ensure dark mode works for any new UI elements.

---

## 📄 License

Distributed under the **MIT License**. See [LICENSE](LICENSE) for more information.

---

## 🗺 Roadmap

- [x] Core donor discovery with smart scoring
- [x] Emergency SOS broadcast
- [x] Hospital directory with click-to-dial
- [x] Donation logging with hero certificates
- [x] Dark/light theme
- [ ] Firebase Firestore integration for real-time sync
- [ ] Push notification support
- [ ] Multi-language support
- [ ] Responsive tablet layout
- [ ] Service Worker for offline support
- [ ] PWA manifest for installable app

---

## 📬 Contact

**Vijay Kumar G K**

- GitHub: [@vijaykumarGK-Developer](https://github.com/vijaykumarGK-Developer)
- Android Version: [rakthavahini](https://github.com/vijaykumarGK-Developer/rakthavahini)
- Web Version: [rakthavahini-html](https://github.com/vijaykumarGK-Developer/rakthavahini-html)

---

<p align="center">
  <i>Rakta-Vahini — Connecting Hearts, Saving Lives.</i>
  <br><br>
  <sub>Built with ❤️ using vanilla HTML, CSS, and JavaScript — no frameworks, no build tools, just code.</sub>
</p>
