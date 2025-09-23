# Jenkins Bare-Metal macOS Agents (Mac Mini M4, 16 GB)

This document provides guidelines for configuring **bare-metal Mac Minis** (16–32 GB RAM) as Jenkins agents for mobile CI/CD workloads (Android and iOS).

---

## Purpose

- Extend the current Jenkins environment with macOS-based build capacity.
- Support complete **application lifecycle pipelines** for both Android and iOS.
- Ensure consistent, reproducible builds using a standardized software stack.

---

## Software Requirements

### Common

- Homebrew (package manager)
- Git
- Jenkins Agent (configured via SSH or JNLP)

### Android Agent Setup

- **Java JDK** (11 or 17, depending on project requirements)
- **Android SDK + NDK** (via `sdkmanager`)
- **Gradle** (or use project Gradle wrapper)

### iOS Agent Setup

- **Xcode** (latest stable version)
- **Xcode Command Line Tools**
- **CocoaPods**
- **Fastlane**

---

## Hardware Requirements

### Recommended Specs

- **Memory**:  
  - Minimum: **16 GB** (suitable for running a single pipeline at a time).  
  - Recommended: **32 GB** (allows parallel jobs and heavier builds such as iOS with Xcode + Android SDK simultaneously).  

- **Storage**:  
  - SSD with at least **512 GB** free space.
  - Recommended: **1 TB SSD** to accommodate:  
    - Multiple Xcode versions (each ~12–15 GB).  
    - Android SDK/NDK and emulators (~20–30 GB).  
    - Build caches, Gradle, CocoaPods, fastlane artifacts, etc.

- **Network**:  
  - Stable high-speed connection (1 Gbps preferred).  
  - Direct access to Jenkins Master and GCP Artifactory Registry.

---

## Maintenance

- Ensure Mac agents are kept up-to-date with required runtimes and tools.
- Regularly **clean up build caches** to free up SSD space.  
- Keep **Xcode and Android SDKs** updated but avoid unnecessary versions. 
- Monitor pipeline logs and test reports for troubleshooting.

---

## Jenkins Integration

- Register each Mac Mini as a Jenkins node with label(s):
  - android → for Android builds
  - ios → for iOS builds
- Assign 1 executor per node (16 GB machines are optimized for single-job execution).

---

## Expected Outcome

- Both Mac Minis are integrated into Jenkins as stable build agents.
- Pipelines can build, test, and package Android and iOS applications.
- Agents are ready for artifact upload (e.g., GCP Artifactory Registry) and deployment to app stores (Google Play, Apple App Store).
