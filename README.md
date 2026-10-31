<div align="center">
  <!-- Replace the src below with a link to your actual logo/banner if you have one -->
  <h1>✈️ Trip & Vacation Photo Organizer</h1>
  <p><strong>By GhOstOP Studio</strong></p>
  <p>
    A smart, local-first desktop application that automatically categorizes your scattered travel memories using on-device AI and GPS metadata.
  </p>

  <p>
    <img src="https://img.shields.io/badge/Vanilla-JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="Vanilla JS">
    <img src="https://img.shields.io/badge/Electron-Desktop-47848F?style=for-the-badge&logo=electron&logoColor=white" alt="Electron">
    <img src="https://img.shields.io/badge/AI-Transformers.js-FF6F00?style=for-the-badge" alt="Transformers.js">
    <img src="https://img.shields.io/badge/Privacy-100%25_Local-4CAF50?style=for-the-badge" alt="Privacy">
  </p>
</div>

<hr>

Coming back from a vacation with thousands of scattered photos and videos? **Trip Photo Organizer** is here to help. It instantly groups your media by the cities you visited or the type of photo (food, landmarks, selfies, nature)—without ever uploading your personal files to the cloud.

## ✨ Features for Travelers

- 📍 **Smart Destination Sorting:** Extracts EXIF GPS data to automatically group your photos and videos by the places and cities you visited. It uses OpenStreetMap reverse geocoding to turn raw coordinates into readable place names.
- 🤖 **Local AI Content Categorization:** Uses an on-device AI model (CLIP ViT-B/32) to instantly recognize what is in your photos. It automatically sorts your memories into intuitive travel folders like **Travel & vibe**, **Food & cafés**, **Nature**, and **Selfies**.
- 👯 **Burst-Shot Cleanup:** Uses smart hashing and aspect-ratio checks to find duplicate and near-duplicate images, helping you easily clear out burst shots from your trip.
- 🔒 **100% Offline & Private:** Your personal vacation photos never leave your computer. All AI processing and EXIF extraction happen directly on your local machine.
- 🎨 **Delightful UI:** Features a beautifully animated, hardware-accelerated interface that makes organizing your camera roll genuinely fun.

## 🛠️ Tech Stack

| Category                  | Technology                                       |
| :------------------------ | :----------------------------------------------- |
| **Frontend**              | Vanilla HTML5, CSS3, JavaScript (ES6+)           |
| **Animation**             | HTML5 `<canvas>` API                             |
| **AI / Machine Learning** | `@huggingface/transformers` (WebAssembly/WebGPU) |
| **Metadata**              | `exifr` (GPS and capture time extraction)        |
| **File Packing**          | `jszip` (for web-fallback exporting)             |

## 🚀 Getting Started

### Prerequisites

You will need [Node.js](https://nodejs.org/) and `npm` installed on your machine.

### Installation

**1. Clone the repository:**

```bash
git clone [https://github.com/yourusername/trip-photo-organizer.git](https://github.com/yourusername/trip-photo-organizer.git)
cd trip-photo-organizer


2. Install dependencies:
This project relies on local node modules for the browser scripts and AI models.

Bash
npm install jszip exifr @huggingface/transformers

3. Run the App:

For Web: Serve the directory using any local web server (e.g., npx serve . or VS Code Live Server). Note: In web mode, the app will generate a downloaded .zip file instead of modifying your local disk.

For Desktop: This frontend is designed to be wrapped in an Electron app that exposes the window.ghostop API for native filesystem operations.

🧠 How the Travel AI Works
If "AI Sort" is enabled, the app downloads a quantized version of the Xenova/clip-vit-base-patch32 model directly to your device. It evaluates your images against custom travel-oriented prompts—such as "a holiday photo at a tourist destination" or "a photo of a coffee or drink at a cafe".

For maximum speed, it also applies a custom pixel-analysis algorithm (analyzing color saturation, brightness, and skin tones) to quickly sort obvious files before the heavy AI kicks in.

📂 Desktop API Hook (window.ghostop)
To fully utilize the app to move files directly on your hard drive, it requires an Electron wrapper. Ensure your Electron preload.js script exposes the following methods to the window.ghostop object:

JavaScript
window.ghostop = {
  listMedia: async (folderPath) => { /* ... */ },
  readFile: async (path) => { /* ... */ },
  selectFolder: async () => { /* ... */ },
  moveFile: async (baseDir, oldPath, newRelativePathArr, fileName) => { /* ... */ },
  undoMove: async (baseDir, currentPath, originalRelativePath, originalFullPath) => { /* ... */ },
  writeSortLog: async (baseDir, logArray) => { /* ... */ },
  removeSortLog: async (baseDir) => { /* ... */ },
  reverseGeocode: async (lat, lon) => { /* ... */ },
  windowAction: (action) => { /* minimize, toggleMaximize, close */ }
}
📜 License
This project is licensed under the MIT License - Feel free to use, modify, and distribute this project for your own adventures.
```
