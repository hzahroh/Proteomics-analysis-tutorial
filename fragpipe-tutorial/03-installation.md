# Installing FragPipe

Unlike many desktop applications, FragPipe is a **portable Java application**. After downloading the software, you can extract the files, launch FragPipe, and configure the required tools. No traditional installation wizard is needed on Linux, while Windows users can use the official installer.


## Learning Objectives
- Install Java
- Download and launch FragPipe
- Configure FragPipe
- Verify that the software is correctly installed

## System requirements

| Component | Recommendation |
|------------|----------------|
| Java | Java 17 or later |
| RAM | ≥16 GB (32 GB for large datasets) |
| Storage | ≥20 GB free disk space |
| CPU | Multi-core processor |

Supported operating systems: Windows and Linux. macOS is **not** officially supported for the complete FragPipe workflow.
This tutorial was developed and tested using Linux. The workflow is also compatible with Windows.

> [!IMPORTANT]
> Although the GUI can be launched on **macOS**, several required tools (including Philosopher and DIA-NN) are unavailable on macOS.

# Step 1. Install Java

FragPipe requires **Java 17 or later**.

Before installing FragPipe, verify whether Java is already installed by opening a terminal (Linux) or Command Prompt (Windows) and running:

```bash
java -version
```

If Java is installed correctly, you should see output similar to:

```text
openjdk version "17.0.x"
```

If Java is not installed, follow the instructions for your operating system below.

## Linux (Ubuntu)

Install OpenJDK 17 using:

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

Verify the installation:

```bash
java -version
```

> [!TIP]
> If the command is not recognized, Java may not be installed correctly or may not be available in your system PATH.

## Windows

Bundled with installer.
No additional Java installation is required unless you choose to use the portable version instead of the installer.


## Step 2: Download FragPipe

Download the latest release of FragPipe from one of the following sources:

- **Official website:** https://fragpipe.nesvilab.org
- **GitHub Releases:** https://github.com/Nesvilab/FragPipe/releases

Proceed to the instructions below for your specific operating system.

## Step 3: Install FragPipe

### Wundows
1. Download **FragPipe-24.x-installer.exe**.
2. Double-click the installer.
3. Follow the installation wizard.
4. Launch FragPipe from the Desktop shortcut or Start Menu.

The Windows installer automatically installs Java and Python.

## Linux

1. Download **FragPipe-24.x-linux.zip**.
2. Open a terminal and navigate to the download directory.
3. Extract the archive:
```bash
unzip FragPipe-24.x-linux.zip
```
4. Enter the installation directory:
```bash
cd FragPipe/bin
```
5. Make the launcher executable:
```bash
chmod +x fragpipe
```
6. Launch FragPipe:
```bash
./fragpipe
```
The `chmod +x` command grants execute permission to the launcher and only needs to be performed once.

# Step 4. Configure FragPipe

When FragPipe is launched for the first time, the **Config** tab will be displayed. 
FragPipe relies on several tools to perform peptide identification, protein inference, and protein quantification.

| Tool | Required | Purpose |
|------|----------|---------|
| MSFragger | Yes | Peptide database search |
| IonQuant | Yes | Label-free protein quantification |
| Philosopher | Yes | Protein inference and FDR estimation |
| MSBooster | Recommended | Improves peptide identification using deep learning |
| DIA-NN | Optional | Required only for DIA workflows |
| Python | Optional | Required for spectral library generation and database splitting |

Download the required tools:
1. Open the **Config** tab.
2. Click **Download/Update** beside the **MSFragger, IonQuant, diaTracer** section.
3. A license agreement window will appear.

Fill in:

- First name
- Last name
- Academic email address
- Institution

Read and accept the required license agreements, then click **Send Verification Email**.

After receiving the verification email:

1. Open the email and fill in the verification code in FragPipe.
3. Download will start and FragPipe will detect the downloaded tools automatically.

The configuration is complete when the licence for the tools are no longer showing **N/A**. 

> [!TIP]
> > If the internet does not work (happened to us) or if for some reasons you can't send verification email, you can download MsFragger, IonQuant and diaTracer manually from Nesvilab's website below by entering your institutional email address:
> - [MsFragger](https://msfragger.arsci.com/upgrader/)
> - [IonQuant](https://msfragger.arsci.com/ionquant/)
> - [diaTracer](https://msfragger-upgrader.nesvilab.org/diatracer/)
> After download is complete, point out to the downloaded tools directory on FragPipe to allow FragPipe to detect the tools automatically.

You are now ready to begin processing proteomics data.

# Frequently Asked Questions

### Why is macOS not supported?

FragPipe itself is a Java application, but several required software components (including Philosopher and DIA-NN) are currently unavailable for macOS. As a result, the complete workflow cannot be executed natively.

For this tutorial, we recommend using **Windows** or **Linux**.

---

### Why does FragPipe say "Philosopher is not supported on macOS"?

Philosopher currently has no macOS release.

Without Philosopher, FragPipe cannot perform protein inference or false discovery rate (FDR) estimation.

---

### Why do I see "DIA-NN only works in Windows and Linux"?

DIA-NN is only required for **DIA** proteomics workflows.

Since this tutorial uses **DDA** data, this warning can generally be ignored.


> [!IMPORTANT]
> **Checkpoint**
>
> Before continuing to the next chapter, ensure that:
> - [ ] FragPipe opens successfully.
> - [ ] The Config tab shows MSFragger, Philosopher, and IonQuant correctly installed.
> - [ ] No error messages are displayed.

Once these steps are complete, proceed to part 4: Preparing Input Files.



