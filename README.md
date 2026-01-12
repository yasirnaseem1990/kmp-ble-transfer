# KMP BLE Transfer  
This project implements a Kotlin Multiplatform (KMP) application that enables peer‑to‑peer money transfers over Bluetooth Low Energy (BLE). Each device acts as both a BLE advertiser (GATT server) and scanner (GATT client) to send and receive amounts using a custom GATT service UUID.  

## Features  
- **BLE Money Transfer Service** with custom GATT Service UUID (`A0F0BEEF-0000-4000-8000-000000000001`) and Transfer Data Characteristic UUID (`A0F0BEEF-0000-4000-8000-000000000002`) supporting READ, WRITE, NOTIFY.  
- **Location & Bluetooth Permissions**: The Android implementation requests and checks the necessary runtime permissions for Bluetooth (including scanning and advertising) and coarse/fine location to enable BLE operations.  
- **Discovery Scoped by UUID**: Devices advertise and scan only for the custom Money Transfer Service UUID to avoid unwanted devices.  
- **Send/Receive Amounts**: UI allows selecting a discovered device and sending a specified amount via the transfer characteristic; amounts received trigger notifications and are added to the transactions list.  
- **Transaction History**: Maintains a list of recent transactions (sent and received) with amount, direction, peer, and timestamp.  
- **Modern UI**: Compose UI built to mirror the reference Stitch design: clean cards, minimal palette, and clear typography.  
- **Dependency Injection**: Uses Koin for injecting repositories, use cases, and BLE components.  
- **Navigation**: Uses Navigation Compose 3 for screen transitions (e.g., device list, send money, transaction history).  
- **Multiplatform Support**: Shared domain and data logic implemented in `shared` module; Android-specific BLE implementation in `androidApp`; placeholder iOS implementation added in `iosApp` with CoreBluetooth scaffolding for future development.  
- **Gradle KMP Setup**: Uses Kotlin Multiplatform Gradle plugin with targets for Android and iOS; configures source sets and dependencies; includes gradle wrapper.  
- **Instrumentation & Unit Tests**: Unit tests cover business logic and BLE integration via fakes/mocks using Koin; instrumentation tests provided for Android BLE scanning/advertising flows.  
- **Low‑Spec Device Considerations**: BLE scanning modes use low‑latency or balanced settings based on device capabilities; UI remains lightweight and responsive.  

## Project Structure  
- `shared/` &ndash; common KMP module containing domain models, repositories, use cases, and Koin modules.  
- `androidApp/` &ndash; Android‑specific code including BLE advertiser, scanner, GATT server/client, Compose UI, ViewModels, Koin module, and instrumentation tests.  
- `iosApp/` &ndash; iOS‑specific module with CoreBluetooth scaffolding for scanning/advertising and SwiftUI UI (to be implemented).  

## Getting Started  
1. **Clone the repository** and open it in Android Studio (latest stable).  
2. **Build the project**; Gradle will download dependencies and set up the KMP modules.  
3. **Run the Android app** on a device running Android 8.0 (API 26) or higher with BLE support. Grant Bluetooth and location permissions when prompted.  
4. **iOS support** is scaffolded; open `iosApp` in Xcode and implement CoreBluetooth scanning/advertising with the same UUIDs.  

## Notes  
- This repository contains only skeleton code; you will need to implement the full BLE logic, UI, and tests as described.  
- Ensure to follow SOLID principles and clean architecture practices when adding modules.  
- For UI, refer to the Stitch design link for exact visuals.  
- Instrumentation tests require physical or emulator devices with BLE capabilities.
