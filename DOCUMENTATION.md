# 📖 Rakta-Vahini — Web App Documentation

> **Version:** 1.0.0 | **Last Updated:** June 2026 | **Tech:** Vanilla HTML/CSS/JS

---

## Table of Contents

1. [Project Overview](#-project-overview)
2. [Architecture & Design](#-architecture--design)
3. [Code Structure & Component Reference](#-code-structure--component-reference)
4. [State Management](#-state-management)
5. [Algorithms](#-algorithms)
6. [Theming System](#-theming-system)
7. [API Reference (Functions)](#-api-reference-functions)
8. [Browser Support & Compatibility](#-browser-support--compatibility)
9. [Performance Considerations](#-performance-considerations)
10. [Contributing Guidelines](#-contributing-guidelines)
11. [Code of Conduct](#-code-of-conduct)
12. [Security Policy](#-security-policy)
13. [Changelog](#-changelog)
14. [FAQ](#-faq)
15. [Troubleshooting Guide](#-troubleshooting-guide)

---

## 📋 Project Overview

Rakta-Vahini Web App is a **single-page application (SPA)** built entirely with vanilla HTML5, CSS3, and JavaScript. It replicates the functionality of the [Android version](https://github.com/vijaykumarGK-Developer/rakthavahini) as a zero-dependency browser-based blood donation network.

### Key Principles

| Principle | Description |
|---|---|
| **Zero Dependencies** | No frameworks, no build tools, no package managers. Open `index.html` and it works. |
| **Mobile First** | Designed for mobile screens (max-width 420px) but works on all devices. |
| **Single File** | All HTML, CSS, and JS live in one file for simplicity and portability. |
| **Offline-Capable Core** | Core functionality works without a server when opened directly from the filesystem. |

### File Structure

```
rakthavahini-html/
├── index.html          # Complete application (HTML + CSS + JS)
├── README.md           # Project overview and quick start
├── DOCUMENTATION.md    # You are here
└── LICENSE             # MIT License
```

---

## 🏗 Architecture & Design

### Application Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                        index.html                                │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │  HTML STRUCTURE                                            │ │
│  │  ┌─────────┐ ┌──────────┐ ┌──────────┐ ┌────────────────┐ │ │
│  │  │ Splash  │ │Onboarding│ │ App Shell │ │ Overlays &     │ │ │
│  │  │ Screen  │ │ Screen   │ │ (Header, │ │ Bottom Sheet   │ │ │
│  │  │         │ │          │ │  Main,   │ │                │ │ │
│  │  │         │ │          │ │  Nav,    │ │                │ │ │
│  │  │         │ │          │ │  FAB)    │ │                │ │ │
│  │  └─────────┘ └──────────┘ └──────────┘ └────────────────┘ │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │  CSS STYLES                                               │ │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────────┐ │ │
│  │  │ Theme    │ │ Layout   │ │Components│ │ Animations &   │ │ │
│  │  │ Variables│ │ (Flexbox)│ │(Card,    │ │ Transitions    │ │ │
│  │  │ :root    │ │          │ │ Button,  │ │                │ │ │
│  │  │          │ │          │ │ Badge)   │ │                │ │ │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────────────┘ │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │  JAVASCRIPT LOGIC                                         │ │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────────┐ │ │
│  │  │ App      │ │ Render   │ │Event     │ │ Utility        │ │ │
│  │  │ State &  │ │ Functions│ │Handlers &│ │ Functions      │ │ │
│  │  │ Data     │ │          │ │ Callbacks│ │(Distance,      │ │ │
│  │  │          │ │          │ │          │ │ Formatting)    │ │ │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────────────┘ │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │  BROWSER APIS                                             │ │
│  │  ┌────────────────┐ ┌────────────────┐ ┌────────────────┐  │ │
│  │  │ Geolocation API│ │ Vibration API  │ │ localStorage    │  │ │
│  │  │ (GPS)          │ │ (Haptics)      │ │ (Persistence)  │  │ │
│  │  └────────────────┘ └────────────────┘ └────────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

### Screen Flow

```
App Load
    │
    ▼
┌────────────┐
│  Splash    │ (2 seconds, animated)
│  Screen    │
└─────┬──────┘
      │
      ▼
┌────────────┐   First visit?    ┌──────────────┐
│ Onboarding │ ──────yes──────>  │ Main App     │
│ Screen     │                  │ (Tab View)   │
└────────────┘                  └──────┬───────┘
      │ no                             │
      └────────────────────────────────┘
                                       │
                              ┌────────┴────────┐
                              │  5 Navigation   │
                              │     Tabs        │
                              ├───┬───┬───┬───┬──┤
                              │ S │ P │ H │ U │ H│
                              │ e │ r │ o │ s │ i│
                              │ a │ o │ s │ e │ s│
                              │ r │ f │ p │ r │ t│
                              │ c │ i │ i │ s │ o│
                              │ h │ l │ t │   │ r│
                              │   │ e │ a │   │ y│
                              │   │   │ l │   │  │
                              │   │   │ s │   │  │
                              └───┴───┴───┴───┴──┘
                                       │
                              ┌────────┴────────┐
                              │  Overlays:      │
                              │  User Detail    │
                              │  Hospital Detail│
                              │  Settings       │
                              │  Certificate    │
                              │  Static Pages   │
                              └─────────────────┘
```

### HTML Layout Structure

```html
<div id="app-container">                    <!-- Phone-frame container -->
    <div id="splash-screen">...</div>        <!-- Splash overlay -->
    <div id="onboarding-screen">...</div>    <!-- First-run overlay -->
    <header>...</header>                     <!-- App bar with title + settings icon -->
    <main id="main-content"></main>          <!-- Dynamic tab content -->
    <div class="fab">🚨</div>                <!-- SOS floating action button -->
    <nav>...</nav>                           <!-- Bottom tab navigation (5 tabs) -->
    <div id="universal-overlay">...</div>    <!-- Slide-in overlay for detail views -->
    <div class="bottom-sheet">...</div>      <!-- Modal bottom sheet for SOS -->
    <div id="snackbar">...</div>             <!-- Toast notification -->
</div>
```

---

## 🧩 Code Structure & Component Reference

### CSS Architecture

The CSS uses **custom properties (CSS variables)** for theming. All colors, backgrounds, and borders are defined in `:root` (light) and overridden in `body.dark-theme` (dark).

#### Custom Properties

| Variable | Light Default | Dark Override | Purpose |
|---|---|---|---|
| `--primary` | `#D32F2F` | `#EF5350` | Primary action color |
| `--primary-dark` | `#9A0007` | `#D32F2F` | Darker primary shade |
| `--light-red` | `#ffebee` | `#3b1c1c` | Background for blood badges |
| `--bg-color` | `#f4f6f8` | `#121212` | Main background |
| `--card-bg` | `#ffffff` | `#1e1e1e` | Card surface color |
| `--text-main` | `#1D1B20` | `#ffffff` | Primary text color |
| `--text-muted` | `#666666` | `#aaaaaa` | Secondary text color |
| `--success` | `#2E7D32` | `#81C784` | Success/eligible state |
| `--border` | `#eeeeee` | `#333333` | Border and divider color |
| `--nav-bg` | `#ffffff` | `#1e1e1e` | Bottom navigation background |
| `--skeleton-1` | `#f0f0f0` | `#2c2c2c` | Skeleton shimmer light |
| `--skeleton-2` | `#e0e0e0` | `#3c3c3c` | Skeleton shimmer dark |

#### Key CSS Classes

| Class | Type | Purpose |
|---|---|---|
| `.card` | Component | Reusable card container with shadow and border |
| `.clickable-card` | Modifier | Adds hover/active press effect to cards |
| `.blood-badge` | Component | Blood group display badge (e.g., "O+") |
| `.btn` | Component | Primary action button (red) |
| `.btn-outline` | Component | Outlined secondary button |
| `.btn.location-btn` | Variant | Blue-themed location button |
| `.form-group` | Layout | Form field wrapper with label |
| `.form-control` | Component | Styled input/select/textarea |
| `.segment-control` | Component | Two-option toggle switch |
| `.segment-btn` | Component | Individual segment option |
| `.skeleton` | Animation | Skeleton loading placeholder |
| `.fullscreen-overlay` | Layout | Slide-in overlay panel |
| `.bottom-sheet` | Layout | Modal bottom sheet |
| `.fab` | Component | Floating action button (SOS) |
| `.smart-badge` | Component | "Best Match" ranking badge |
| `.certificate` | Component | Donation certificate frame |
| `#snackbar` | Component | Toast notification bar |

### JavaScript Component Reference

#### Core State Variables

| Variable | Type | Line | Description |
|---|---|---|---|
| `now` | `Date` | 316 | Current timestamp reference |
| `myHistory` | `Array<Date>` | 321 | Personal donation history |
| `myLiveLocation` | `Object|null` | 322 | `{lat, lng}` or null |
| `enrolledUsers` | `Array<Donor>` | 324 | All registered donor profiles |
| `enrolledHospitals` | `Array<Hospital>` | 331 | All registered hospitals |
| `currentProfileView` | `string` | 336 | `"user"` or `"hospital"` |
| `currentHistoryView` | `string` | 337 | `"user"` or `"hospital"` |

#### Data Models (JavaScript Objects)

**Donor Object:**
```javascript
{
    name: "Rahul Sharma",
    age: 28,
    gender: "Male",
    group: "O+",
    phone: "9876543210",
    altPhone: "9876543201",
    address: "Sector 4",
    distance: 5,              // Default distance (km)
    lat: 28.6139,             // Latitude
    lng: 77.2090,             // Longitude
    lastDonation: Date,        // Last donation timestamp
    responseSpeed: 5,          // Response speed rating
    freq: 8,                  // Lifetime donation count
    activeDaysAgo: 1,         // Days since last activity
    // Computed (added during filtering):
    isEligible: Boolean,
    calcDist: Number,
    smartScore: Number
}
```

**Hospital Object:**
```javascript
{
    name: "City Care Hospital",
    address: "123 Main St, Medical District",
    lat: 12.9716,
    lng: 77.5946,
    email: "emergency@citycare.com",
    phone: "9988776655",
    landline: "011-2345678"
}
```

#### Render Functions

| Function | Line | Description | Returns |
|---|---|---|---|
| `renderSearch()` | 364 | Renders the Search tab with blood group filter, radius slider, and results list | DOM update |
| `renderProfile()` | 566 | Renders dual registration form (Individual/Hospital) | DOM update |
| `renderHospitals()` | 637 | Renders hospital directory cards | DOM update |
| `renderUsers()` | 649 | Renders all registered donors with eligibility badges | DOM update |
| `renderHistory()` | 666 | Renders donation log feed with user/hospital toggle | DOM update |
| `renderSkeleton(container)` | 397 | Renders shimmer placeholder cards | DOM update |

#### Overlay Functions

| Function | Line | Description |
|---|---|---|
| `openOverlay(title, htmlContent)` | 450 | Opens fullscreen slide-over panel |
| `closeOverlay()` | 456 | Closes slide-over panel |
| `openUserDetail(index)` | 458 | Shows donor profile in overlay |
| `openHospitalDetail(index)` | 482 | Shows hospital info in overlay |
| `openSettings()` | 516 | Shows settings panel in overlay |
| `showStatic(page)` | 537 | Shows About/FAQ/Privacy/Support pages |
| `logDonation()` | 547 | Logs donation and shows Certificate of Heroism |

#### SOS Functions

| Function | Line | Description |
|---|---|---|
| `openEmergencySheet()` | 503 | Opens SOS bottom sheet |
| `closeEmergencySheet()` | 504 | Closes SOS bottom sheet |
| `triggerSOS()` | 506 | Broadcasts SOS alert |

#### Utility Functions

| Function | Line | Description |
|---|---|---|
| `haptic()` | 290 | Triggers device vibration (40ms) |
| `fetchLiveLocation(callback)` | 340 | Gets GPS coordinates via Geolocation API |
| `calculateDistance(lat1, lon1, lat2, lon2)` | 355 | Haversine formula → distance in km |
| `filterDonors()` | 404 | Filters and sorts donors by eligibility, distance, and smart score |
| `updateRadius(val)` | 395 | Updates radius slider display |
| `toggleTheme(isDark)` | 531 | Switches between light/dark themes |
| `showToast(message)` | 709 | Shows snackbar notification |
| `switchTab(tabId, element)` | 700 | Switches between navigation tabs |
| `saveUser()` | 634 | Registers a new donor |
| `saveHospital()` | 635 | Registers a new hospital |
| `formatFullDate(date)` | 319 | Formats Date to readable string |
| `finishOnboarding()` | 308 | Completes first-run onboarding |

---

## 🎮 State Management

The application uses **in-memory state** with JavaScript arrays and objects. There is no state management library — state is mutated directly and UI is re-rendered by calling the appropriate render function.

### State Flow

```
User Action (click, form input, GPS)
        │
        ▼
Event Handler / Callback
        │
        ▼
State Mutation (push to array, update variable)
        │
        ▼
Render Function Called (e.g., renderSearch())
        │
        ▼
DOM Updated (innerHTML replacement)
        │
        ▼
User Sees New UI
```

### State Persistence

| Data | Storage Method | Key |
|---|---|---|
| Theme preference | `localStorage` | `theme` |
| Onboarding completion | `localStorage` | `onboarded` |
| Donor data | In-memory array | `enrolledUsers` |
| Hospital data | In-memory array | `enrolledHospitals` |
| Donation history | In-memory array | `myHistory` |

### Data Flow for Donor Search

```
1. User selects blood group + radius
2. filterDonors() called
3. Skeleton loading shown (renderSkeleton)
4. 400ms delay (simulated network)
5. For each donor:
   a. Calculate days since last donation
   b. Set isEligible (days > 90)
   c. Calculate distance (Haversine formula)
   d. Calculate smartScore
6. Filter: group match AND within radius AND eligible
7. Sort by smartScore (ascending)
8. Render results with "🌟 Best Match" badge on #1
```

---

## 🔬 Algorithms

### Smart Scoring Formula

```javascript
smartScore = calcDist + (responseSpeed * 0.1) + (activeDaysAgo * 0.5) - (freq * 0.2)
```

| Variable | Weight | Effect | Rationale |
|---|---|---|---|
| `calcDist` | 1.0 | Closer is better | Proximity priority |
| `responseSpeed` | 0.1 | Lower is better | Fast responders ranked higher |
| `activeDaysAgo` | 0.5 | Lower is better | Recently active donors preferred |
| `freq` | -0.2 | Higher is better | Rewards frequent donors |

### Eligibility Algorithm

```javascript
const daysSince = (new Date() - donor.lastDonation) / (1000 * 60 * 60 * 24);
donor.isEligible = daysSince > 90;
```

The 90-day cooling period is based on standard blood donation medical guidelines.

### Haversine Distance Formula

```javascript
R = 6371  // Earth's radius in km
dLat = toRadians(lat2 - lat1)
dLon = toRadians(lon2 - lon1)
a = sin²(dLat/2) + cos(lat1) × cos(lat2) × sin²(dLon/2)
c = 2 × atan2(√a, √(1-a))
distance = R × c
```

Returns distance in kilometers with one decimal place.

---

## 🎨 Theming System

### Light Mode (Default)

- Background: `#f4f6f8` (light gray)
- Cards: `#ffffff` (white)
- Primary: `#D32F2F` (blood red)
- Text: `#1D1B20` (near black)

### Dark Mode

- Background: `#121212` (material dark)
- Cards: `#1e1e1e` (dark gray)
- Primary: `#EF5350` (lighter red for contrast)
- Text: `#ffffff` (white)

### Toggle Implementation

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
```

The theme is applied by adding/removing `.dark-theme` class on `<body>`. CSS variables automatically update all child elements.

---

## 📚 API Reference (Functions)

### `haptic()`
Triggers tactile feedback.
- **API:** `navigator.vibrate(40)`
- **Duration:** 40ms
- **Fallback:** Silent fail if Vibration API unsupported

### `fetchLiveLocation(callback?)`
Captures device GPS coordinates.
- **API:** `navigator.geolocation.getCurrentPosition()`
- **Success:** Sets `myLiveLocation`, randomizes donor coords for demo, calls `filterDonors()`
- **Error:** Shows toast "❌ GPS Denied"
- **Fallback:** Uses default coordinates if GPS denied

### `calculateDistance(lat1, lon1, lat2, lon2) → string`
Haversine formula distance calculator.
- **Input:** 4 latitude/longitude values
- **Output:** Distance in km (1 decimal), string type
- **Edge case:** Returns `"0"` if any coordinate is missing

### `showToast(message)`
Displays a temporary snackbar message.
- **Duration:** 3 seconds (auto-hide)
- **Animation:** Slide up (fadein 0.3s) → hold 2.4s → slide down (fadeout 0.3s)

### `switchTab(tabId, element)`
Changes the active navigation tab.
- **Side effects:** Removes `.active` from all nav items, adds to clicked element, closes any open overlay, calls the appropriate render function

---

## 🌐 Browser Support & Compatibility

| Feature | Chrome | Firefox | Safari | Edge | Opera | Samsung Internet |
|---|---|---|---|---|---|---|
| **CSS Custom Properties** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Flexbox** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **CSS Animations** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Geolocation API** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Vibration API** | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ |
| **localStorage** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **ES6 Features** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

### Minimum Requirements
- **Browser:** Chrome 49+, Firefox 44+, Safari 10+, Edge 16+
- **JavaScript:** ES6 (2015) support
- **CSS:** Custom Properties support

---

## ⚡ Performance Considerations

| Aspect | Implementation | Impact |
|---|---|---|
| **Rendering** | Full `innerHTML` replacement on tab switch | Simple but re-renders entire content area |
| **Search** | 400ms artificial delay + skeleton shimmer | Improves perceived performance |
| **State** | In-memory arrays | Fast access, no async overhead |
| **CSS** | Single stylesheet with custom properties | No flash of unstyled content (FOUC) |
| **DOM Size** | Single page, dynamic content injection | Small DOM footprint |

### Known Limitations

- No virtual DOM — full re-render on tab switch
- Mock data — no real backend persistence
- Simple array search — O(n) complexity
- No lazy loading — all data in memory

---

## 🤝 Contributing Guidelines

### How to Contribute

1. **Fork** the repository.
2. **Create a feature branch:**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Make changes** in `index.html`.
4. **Test** — Open locally, test all 5 tabs, overlay interactions, dark mode, and SOS flow.
5. **Commit:**
   ```bash
   git commit -m "feat: add amazing feature"
   ```
6. **Push:**
   ```bash
   git push origin feature/amazing-feature
   ```
7. **Open a Pull Request.**

### Coding Standards

- **HTML:** Semantic tags, consistent indentation (4 spaces).
- **CSS:** Use custom properties for colors, keep specificity low, follow existing naming.
- **JavaScript:** Use `const`/`let` (no `var`), arrow functions, template literals.
- **Single-File Rule:** All code must remain in `index.html` unless a strong reason exists to split.
- **No Dependencies:** Do not add external libraries, CDN links, or build tools.

### Pull Request Checklist

- [ ] Tested in Chrome, Firefox, and Safari
- [ ] Dark mode works for new UI elements
- [ ] Mobile responsive (420px viewport)
- [ ] No console errors
- [ ] Haptic feedback on interactive elements
- [ ] Consistent with existing code style

---

## 📜 Code of Conduct

### Our Pledge

We pledge to make participation in this project a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity, level of experience, nationality, personal appearance, race, religion, or sexual identity.

### Standards

**Positive behavior:**
- Using welcoming and inclusive language
- Respecting differing viewpoints
- Accepting constructive criticism graciously
- Focusing on community benefit
- Showing empathy

**Unacceptable behavior:**
- Sexualized language or imagery
- Trolling, insults, or personal attacks
- Public or private harassment
- Publishing others' private information
- Unprofessional conduct

### Enforcement

Report violations to [vijaykumar2572003@gmail.com](mailto:vijaykumar2572003@gmail.com). All complaints will be reviewed and investigated.

---

## 🔒 Security Policy

### Supported Versions

| Version | Supported |
|---|---|
| 1.0.x | ✅ Supported |

### Reporting Vulnerabilities

Email [vijaykumar2572003@gmail.com](mailto:vijaykumar2572003@gmail.com) with:
- Description of the vulnerability
- Steps to reproduce
- Potential impact

Response expected within 48 hours.

### Security Notes

- **No data transmission** — This version uses local mock data only. No data leaves the browser.
- **No cookies or tracking** — Only `localStorage` for theme preference.
- **Geolocation** — Used only with explicit user consent via the browser's permission prompt.
- **Phone calls** — Uses `tel:` protocol links, which only open the dialer. No call data is transmitted.

---

## 📝 Changelog

### [1.0.0] — June 2026

#### Added
- 🩸 Intelligent donor discovery with proximity-based search
- 🌐 Live GPS integration via Geolocation API
- 📐 Haversine distance calculation for accurate geo-matching
- 🧮 Smart scoring algorithm for donor ranking
- 🚨 Emergency SOS broadcast system with modal bottom sheet
- 🏥 Hospital and blood bank directory with click-to-dial
- 🏆 Donation logging with auto-generated Certificate of Heroism
- 🌓 Dark/Light theme with localStorage persistence
- 👤 Dual registration (individual donors and hospitals)
- 🔍 5-tab navigation (Search, Profile, Hospitals, Users, History)
- 💀 Skeleton loading shimmer animation
- 🔔 Snackbar toast notifications
- 📱 Mobile-first responsive design
- 📄 Print-ready certificate layout

---

## ❓ FAQ

**Q: Do I need to install anything?**
A: No. Just open `index.html` in any modern browser.

**Q: Does this app connect to a real database?**
A: No. This version uses mock data stored in memory. Real-time sync via Firebase is planned.

**Q: Does the SOS feature send real notifications?**
A: In this version, SOS triggers a simulated browser alert. Real push notifications require a backend service.

**Q: Is my location data stored?**
A: No. Location is used in-memory for distance calculation and is not persisted or transmitted.

**Q: Can I deploy this to a web server?**
A: Yes. Upload `index.html` to any static hosting (GitHub Pages, Netlify, Vercel, etc.).

**Q: How do I add real donor data?**
A: Either modify the `enrolledUsers` array in the JavaScript or build a backend API.

---

## 🔧 Troubleshooting Guide

### App not loading

| Cause | Solution |
|---|---|
| File opened in older browser | Use Chrome/Firefox/Safari (latest version). |
| Corrupted download | Re-clone the repository. |
| File encoding issue | Ensure `index.html` is saved as UTF-8. |

### GPS not working

| Cause | Solution |
|---|---|
| Permission denied | Grant location permission when prompted by the browser. |
| HTTP served (not HTTPS) | Geolocation API requires HTTPS (or localhost). |
| Desktop browser | Some desktop browsers block GPS — use a mobile device. |

### Dark mode not persisting

| Cause | Solution |
|---|---|
| Private/incognito mode | `localStorage` is cleared on session end. |
| Storage cleared | Theme preference is stored in `localStorage['theme']`. |

### UI looks broken

| Cause | Solution |
|---|---|
| Browser too narrow | The app is designed for mobile (max 420px). Use a wider view or mobile emulation. |
| CSS not loaded | Ensure no browser extensions are blocking inline styles. |

### Contact Support

Open an issue at [GitHub Issues](https://github.com/vijaykumarGK-Developer/rakthavahini-html/issues) with:
- Browser and version
- Steps to reproduce
- Screenshots (if applicable)

---

<p align="center">
  <i>Rakta-Vahini — Connecting Hearts, Saving Lives.</i>
  <br>
  <a href="https://github.com/vijaykumarGK-Developer/rakthavahini-html">GitHub</a> •
  <a href="mailto:vijaykumar2572003@gmail.com">Contact</a> •
  <a href="https://github.com/vijaykumarGK-Developer/rakthavahini-html/issues">Issues</a>
  <br><br>
  <sub>Built with ❤️ using vanilla HTML, CSS, and JavaScript</sub>
</p>
