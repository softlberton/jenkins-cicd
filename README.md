# jenkins-mobile-cicd

## Documentation



- ## Architecture
  - [CICD Platform](docs/diagram/platform.md)
  - [Requirements](docs/diagram/requirements.md)
  - [Agents](docs/diagram/agents.md)

- ## Explanation
  - [Plataform](docs/explanation/platform.md)
  - [Native Tools](docs/explanation/tools.md)

-----------

```mermaid
flowchart LR
  Master["Jenkins Master"] --> Agent1["Android Agent (macOS + SDK/NDK + Gradle)"]
  Master --> Agent2["iOS Agent (macOS + Xcode + CocoaPods + fastlane)"]
  Agent1 --> APK["APK Artifact - Google Play / Repository"]
  Agent2 --> IPA["IPA Artifact - App Store / Repository"]
```

## Google Cloud Artifact Repository

- https://cloud.google.com/artifact-registry/docs
