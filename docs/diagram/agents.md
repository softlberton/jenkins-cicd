### Jenkins Agent Preparation

This section outlines best practices for preparing **bare-metal Mac Minis** as Jenkins build agents for Android and iOS pipelines.

---

#### 1. Initial System Snapshot / Backup

- macOS does not have built-in snapshot functionality like some virtualization platforms, but you can create a **full backup** of the system using **Time Machine** or **disk cloning tools** (e.g., Carbon Copy Cloner, SuperDuper!).
- This allows you to restore the Mac to a known initial state if something goes wrong during software installation or configuration.
- Recommended: take a backup **before installing Jenkins agent software, SDKs, or build tools**.

---

#### 2. Dedicated User Account

- Create a **dedicated macOS user** for running the Jenkins agent:
  - Isolates the build environment from other users.
  - Simplifies permissions and environment configuration.
  - Recommended username: `jenkins` or `ci-agent`.
- Configure **sudo privileges** only if needed (e.g., installing Homebrew packages or system dependencies).

---

#### 3. System Configuration Considerations

- Ensure the macOS system is **up-to-date** with security updates and Xcode Command Line Tools.
- Configure **hostname** and **network settings** to allow Jenkins Master to connect reliably.
- Set **energy and sleep settings** to prevent the Mac from sleeping during builds.
- Optional: configure **local firewall rules** to allow only Jenkins Master access to the agent service.

---

#### 4. Software Preparation

- Install required **runtimes and tools** for Android and iOS builds (see Software Requirements section).
- Set environment variables (`JAVA_HOME`, `ANDROID_HOME`, `PATH`) for the dedicated user.
- Test that all tools are available from the dedicated user shell before registering the agent in Jenkins.

---

#### 5. Jenkins Agent Registration

- Register the Mac Mini in Jenkins as a **node**, using either **SSH** or **JNLP/WebSocket**.
- Assign **labels** to the node to indicate its capabilities (`android`, `ios`, `mac`).
- Test connectivity and run a simple pipeline to validate the setup.

---

✅ **Outcome**
- The Mac Mini is ready as a Jenkins agent.
- Isolated build environment with dedicated user.
- Optional system backup available for quick recovery.
- Fully prepared to run Android and iOS CI/CD pipelines.
