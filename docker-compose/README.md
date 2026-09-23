# Installing Docker

## 1. Installing WSL and Ubuntu
Refer to: \
https://learn.microsoft.com/en-us/windows/wsl/install-manual

WSL (Windows Subsystem for Linux) provides the Linux environment required to run Docker on Windows 11.

### 1.1 Install WSL

1. Open **PowerShell as Administrator**.
2. Run:

```powershell
wsl --install
```

3. Restart Windows if requested.

The `wsl --install` command enables the required Windows components, installs WSL 2, and installs Ubuntu by default. ([Microsoft Learn][1])

### 1.2 Select the Ubuntu LTS Version

If installing Ubuntu manually or selecting the distribution through the Microsoft Store:

1. Open the **Microsoft Store**.
2. Search for **Ubuntu**.
3. View the available Ubuntu versions.
4. Select the **latest supported Ubuntu LTS release**.
5. Select **Get** to download and install Ubuntu.

Do not select an obsolete Ubuntu release simply because it is listed as an available version. Use the current supported LTS release so that the environment receives security updates for the supported lifetime of the release. Microsoft provides the available Ubuntu distributions through the Microsoft Store and WSL installation mechanisms. ([Microsoft Learn][2])

### 1.3 Verify WSL

Open PowerShell and run:

```powershell
wsl --status
```

Then:

```powershell
wsl --list --verbose
```

The Ubuntu distribution should show:

```text
VERSION
2
```

WSL 2 is required for this environment.

## 2. Installing Docker Desktop in Windows 11

Now that WSL 2 and Ubuntu have been installed, install **Docker Desktop for Windows**.

Docker Desktop will use the existing WSL 2 installation as its Linux container backend.

### 2.1 Download Docker Desktop
https://docs.docker.com/desktop/setup/install/windows-install/

1. Open a web browser.
2. Go to the official Docker Desktop download page.
3. Download **Docker Desktop for Windows – x86_64** for a standard Intel/AMD Windows 11 laptop.
4. Save the installer.

### 2.2 Install Docker Desktop

1. Run the downloaded `Docker Desktop Installer.exe`.
2. When the installer asks which backend to use, select:

**Use WSL 2 instead of Hyper-V**

3. Continue through the installation.
4. Start **Docker Desktop** when the installation completes.

Docker's current Windows installer uses WSL 2 as the default backend on supported systems.

### 2.3 Enable WSL Integration

After Docker Desktop starts:

1. Open **Docker Desktop**.
2. Select **Settings**.
3. Select **General**.
4. Confirm:

**Use the WSL 2 based engine**

5. Select **Resources → WSL Integration**.
6. Enable integration for:

**Ubuntu**

7. Select **Apply & Restart**.

This makes the Docker CLI available directly from the Ubuntu WSL terminal.

### 2.4 Verify Docker

Open the Ubuntu terminal and run:

```bash
docker --version
```

Then:

```bash
docker compose version
```

Finally:

```bash
docker run hello-world
```

The `hello-world` container should download and run successfully.

### 2.5 Important

Do **not** install Docker Engine separately inside Ubuntu.

Docker Desktop provides the Docker Engine and integrates it with WSL 2. Installing another Docker Engine inside the Ubuntu distribution can create conflicts.
