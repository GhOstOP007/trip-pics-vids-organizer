 <div align="center">

# 👻 GhOstOP Studio
### ✈️ Trip & Vacation Photo Organizer

**Organize your travel memories intelligently with AI.**

[🌐 Try the Web Version](https://ghostop-studio-trip-picsvid-org.netlify.app)

**By GhOstOP Studio**

A smart, privacy-focused desktop application that automatically organizes your scattered travel photos and videos using on-device AI, GPS metadata, and intelligent file grouping.

![JavaScript](https://img.shields.io/badge/Vanilla-JS-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Electron](https://img.shields.io/badge/Electron-Desktop-47848F?style=for-the-badge&logo=electron&logoColor=white)
![Transformers.js](https://img.shields.io/badge/AI-Transformers.js-FF6F00?style=for-the-badge)
![Privacy](https://img.shields.io/badge/Privacy-Local_AI-4CAF50?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## 📸 About the Project

Coming back from a vacation with thousands of scattered photos and videos?

**GhOstOP Studio — Trip & Vacation Photo Organizer** helps you organize your travel memories automatically.

Whether you've explored mountains, beaches, cities, or cafés, GhOstOP Studio can group your media by destination, content, and other characteristics.

The application prioritizes local processing, meaning your personal photos don't need to be uploaded to a cloud server for AI analysis.

## ✨ Features

### 📍 Smart Destination Sorting

Automatically organize photos by the places you've visited.

- Extracts GPS coordinates from EXIF metadata.
- Groups media based on geographical location.
- Supports online reverse geocoding using OpenStreetMap.
- Converts GPS coordinates into readable location names.
- Falls back to coordinate-based grouping when offline.

### 🤖 AI-Powered Photo Categorization

Uses the **CLIP ViT-B/32** image classification model through Transformers.js.

Automatically categorizes travel photos into groups such as:

- 🏔️ Travel & Vibe
- 🍔 Food & Cafés
- 🌿 Nature & Landscapes
- 🤳 Selfies & Portraits
- 🏛️ Landmarks & Architecture

AI inference runs locally on your computer.

### ☁️ On-Demand AI Model Downloads

GhOstOP Studio keeps its installer smaller by downloading the AI model only when needed.

- No multi-gigabyte AI model bundled with the installer.
- Download the model when AI sorting is first used.
- View download progress.
- Retry interrupted downloads.
- Store the model locally for future use.
- Run AI classification offline after the initial download.
- Manage downloaded model files.

**Note:** An internet connection is required for the initial AI model download.

### 👯 Duplicate & Burst-Shot Detection

Identify potentially redundant photos using:

- File hashing.
- Image aspect-ratio comparisons.
- Similarity heuristics.

This helps identify duplicate and near-duplicate media from trips and burst photography.

### 🔒 Privacy-Focused Processing

Your photos remain on your device during local AI processing.

- Local AI inference.
- Local EXIF metadata extraction.
- Native filesystem operations.
- No photo uploads required for classification.
- Optional online location lookup.

**Privacy note:** When online reverse geocoding is enabled, GPS coordinates are sent to the location service to resolve place names. The photo files themselves are not uploaded.

### 🎨 Modern Desktop Experience

- Custom Electron desktop interface.
- Smooth animations.
- Custom GhOstOP Studio ghost icon.
- Native window controls.
- Folder selection.
- File organization and undo functionality.
- ZIP export support.

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Desktop Framework | Electron |
| AI / Machine Learning | Transformers.js |
| AI Model | CLIP ViT-B/32 |
| AI Runtime | ONNX Runtime / WebAssembly |
| Metadata Extraction | exifr |
| ZIP Export | JSZip |
| Location Services | OpenStreetMap Nominatim |
| Package Manager | npm |
| Windows Installer | electron-builder |

---

## 🚀 Getting Started

### Prerequisites

Install the following:

- [Node.js](https://nodejs.org/) (includes npm)
- Git (optional, for cloning the repository)

Python is not required for the runtime AI download version.

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

Replace the placeholders with your actual GitHub repository details.

### 2. Install Dependencies

```bash
npm install
```

### 3. Run the Desktop Application

```bash
npm start
```

This launches GhOstOP Studio using Electron.

### 4. Download the AI Model

When AI-based sorting is requested for the first time:

1. Open GhOstOP Studio.
2. Select a folder containing photos.
3. Choose AI-based sorting.
4. Start the model download when prompted.
5. Wait for the model to finish downloading.
6. Start organizing your photos.

After downloading, the AI model can be reused without an internet connection.

### 5. Build the Windows Installer

```bash
npm run build
```

The generated installer will be available inside the `dist/` directory.

The installer excludes the downloaded AI model to keep the distributable package smaller.

---

## 🌐 Web Version

You can try the browser-based version here:

**[Launch GhOstOP Studio Online](https://ghostop-studio-trip-picsvid-org.netlify.app)**

The web version is intended for testing the interface and supported browser-based features.

Some native filesystem capabilities require the Electron desktop application. Browser functionality also depends on the browser's filesystem permissions and supported APIs.

---

## 🧠 How the AI Works

GhOstOP Studio uses **CLIP (Contrastive Language–Image Pretraining)** to classify images based on their visual content.

### AI Classification Pipeline

1. **Image Selection:** The user selects a folder containing travel media.
2. **Image Preprocessing:** Images are prepared for classification.
3. **Model Loading:** The locally downloaded CLIP model is loaded.
4. **Semantic Classification:** Images are compared against travel-oriented text descriptions.
5. **Category Assignment:** The most relevant categories are selected.
6. **File Organization:** Media is grouped according to the selected sorting options.

Example classification prompts:

```text
A holiday photo at a tourist destination
A photo of mountains and natural landscapes
A photo of food at a restaurant
A selfie taken during a vacation
A photo of a historical landmark
```

The application can also use lightweight image-analysis heuristics to assist with categorization.

---

## 📍 How Location Sorting Works

GhOstOP Studio extracts GPS metadata from supported media files.

When location sorting is selected, the application can operate in two modes.

**Online Mode**

Uses OpenStreetMap's Nominatim reverse-geocoding service to convert GPS coordinates into readable geographical names.

**Offline Mode**

Uses locally available location information or coordinate-based grouping without requiring a network connection.

If online lookup fails, the application can fall back to offline grouping.

---

## 📂 Desktop API (`window.ghostop`)

The Electron desktop application uses a preload bridge to expose supported native operations to the frontend.

An example of the desktop API structure:

```javascript
window.ghostop = {
  listMedia: async (folderPath) => {},
  readFile: async (path) => {},
  selectFolder: async () => {},
  moveFile: async (
    baseDir,
    oldPath,
    newRelativePathArr,
    fileName
  ) => {},
  undoMove: async (
    baseDir,
    currentPath,
    originalRelativePath,
    originalFullPath
  ) => {},
  writeSortLog: async (baseDir, logArray) => {},
  removeSortLog: async (baseDir) => {},
  reverseGeocode: async (lat, lon) => {},
  windowAction: (action) => {}
};
```

The example above illustrates the API structure. Actual implementations are provided by the Electron preload and main-process code.

---

## 🗺️ Roadmap

Potential future improvements:

- [ ] More efficient AI models with smaller download sizes.
- [ ] Additional AI sorting categories.
- [ ] Improved duplicate detection using perceptual hashing.
- [ ] Video scene classification.
- [ ] Offline city-name database.
- [ ] Additional export formats.
- [ ] Cross-platform desktop releases.
- [ ] Automatic application updates.

---

## 🤝 Contributing

Contributions, bug reports, and feature suggestions are welcome.

To contribute:

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Test the application.
5. Submit a pull request.

---

## 📜 License

This project is licensed under the **MIT License**.

See the `LICENSE` file for details.

---

<div align="center">

### 👻 GhOstOP Studio

**Your memories deserve better organization.**

Made with ❤️ for travelers, photographers, and explorers.

[Try the Web App](https://ghostop-studio-trip-picsvid-org.netlify.app)

</div>
