# Croupier: A Real-Time OCR & UI Analysis Framework for Android
**Technologies:** Kotlin, Jetpack Compose, Gemini AI, Android Services, Text-to-Speech (TTS)

Croupier.apk (One-Check Mode) https://www.youtube.com/watch?v=REShrnKKy_s

Croupier.apk (Two-Check Mode) https://www.youtube.com/watch?v=32vL1JOkKmM

### Overview

Croupier is a proof-of-concept (PoC) Android application demonstrating a high-performance framework for real-time screen analysis. It continuously captures, analyzes, and interprets UI elements using Optical Character Recognition (OCR) and a Gemini AI model.

This project is intended as a technical case study for a portfolio, focusing on:
* Optimizing on-device data processing in real-time.
* Integrating AI models (Gemini) for intelligent data extraction.
* Managing application state in Jetpack Compose with a high-frequency data source.
* Leveraging Android's accessibility features (TTS) for data output.

### Core Features

* **High-Speed Screen Analysis:** Utilizes an Android Service to run a persistent scanning loop.
* **Intelligent OCR:** Extracts raw text from specified screen regions.
* **Gemini AI Integration:** Uses Google's Gemini AI to parse the raw OCR text, structure it, and handle inconsistencies.
* **Real-Time Audio Feedback:** Integrates with Android's Text-to-Speech (TTS) engine to announce the processed data, demonstrating an accessibility use case.
* **Dynamic Configuration:** The UI (built with Jetpack Compose) allows adjusting parameters like scan intervals to balance performance and accuracy.

### Technical Challenges & Solutions

The primary challenge was achieving reliable, low-latency analysis without draining system resources.

1.  **Performance vs. Accuracy (Scan Modes):**
    * **"One-Check Mode":** Prioritizes speed. The system confirms data after the first successful reading. With a scan interval of `1000ms`, this can sometimes conflict with the TTS engine's speech duration (approx. `1250ms` for two items), leading to self-corrections. This demonstrates a fascinating trade-off.
    * **"Two-Check Mode":** Prioritizes accuracy. The system requires two identical, consecutive readings to confirm the data, typically using a `2000ms` interval. This is slower but highly resilient to momentary OCR glitches.

2.  **State Management in Compose:**
    * The background Service pushes data updates at a high frequency. The Jetpack Compose UI uses `StateFlow` and `collectAsStateWithLifecycle` to observe this data stream efficiently, ensuring the UI remains responsive and reflects the latest processed information without flickering.

3.  **Accessibility & Synchronization:**
    * A key challenge was synchronizing the scan loop with the TTS engine. The solution involves managing a queue for the TTS engine and ensuring the scan interval is properly tuned (e.g., to `1300ms` or higher) to allow speech to complete before the next update is processed.

### Disclaimer

This project is a technical demonstration of on-device OCR and AI capabilities. It is intended for educational and portfolio purposes **only** to showcase skills in Android development, systems design, and AI integration.
