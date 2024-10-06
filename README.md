# GitHub Automation with PowerShell

Welcome to the **GitHub Automation with PowerShell** guide! This repository provides a set of custom PowerShell functions and aliases to streamline your GitHub workflow using the GitHub CLI (`gh`). Whether you're creating repositories, listing them, or managing them, these commands are designed to enhance your productivity.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Available Commands](#available-commands)
  - [Create a New Repository](#create-a-new-repository)
  - [List Repositories (HTTPS)](#list-repositories-https)
  - [List Repositories (SSH)](#list-repositories-ssh)
  - [Remove a Repository (SSH)](#remove-a-repository-ssh)
  - [Remove a Repository (HTTPS)](#remove-a-repository-https)
  - [Reload PowerShell Profile](#reload-powershell-profile)
  - [Edit PowerShell Profile](#edit-powershell-profile)
- [Usage Examples](#usage-examples)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before using these custom PowerShell commands, ensure you have the following installed and configured:

- **PowerShell 7.5.0-preview.5** or later
- **GitHub CLI (`gh`)** version 2.58.0 or later
- **Oh-My-Posh** for PowerShell customization
- **Posh-Git** for Git enhancements in PowerShell

## Installation

1. **Clone the Repository** (if applicable):
   ```powershell
   git clone https://github.com/yourusername/github-automation-powershell.git
   cd github-automation-powershell
   ```

2. **Install GitHub CLI**:
   If not already installed, use `winget` to install:
   ```powershell
   winget install GitHub.cli
   ```

3. **Install Oh-My-Posh**:
   ```powershell
   winget install JanDeDobbeleer.OhMyPosh
   ```

4. **Install Posh-Git**:
   ```powershell
   Install-Module posh-git -Scope CurrentUser
   ```

5. **Add Custom Functions and Aliases**:
   Ensure your PowerShell profile (`$PROFILE`) includes the custom functions and aliases. You can copy the functions from this README into your profile.

## Configuration

1. **Authenticate GitHub CLI**:
   ```powershell
   gh auth login
   ```
   Follow the prompts to authenticate with your GitHub account.

2. **Set Up SSH Agent**:
   Ensure your SSH keys are added:
   ```powershell
   ssh-add -l
   ```
   If your key isn't listed, add it:
   ```powershell
   ssh-add ~/.ssh/id_ed25519
   ```

3. **Initialize Oh-My-Posh**:
   Add the following to your PowerShell profile:
   ```powershell
   oh-my-posh init pwsh --config "C:\Users\syrym\AppData\Local\oh-my-posh\paradox.omp.json" | Invoke-Expression
   ```

## Available Commands

### Create a New Repository

- **Function:** `new-repo`
- **Alias:** `nr`

**Description:** Creates a new GitHub repository with the specified name, description, and visibility.

**Parameters:**
- `-name` (string, mandatory): Name of the repository.
- `-description` (string, optional): Description of the repository.
- `-private` (switch, optional): If set, the repository will be private. Otherwise, it will be public.

**Usage:**
```powershell
nr -name "repositoryName" -description "Repository Description" -private
```

### List Repositories (HTTPS)

- **Function:** `list-repos-http`
- **Alias:** `lrhttp`

**Description:** Lists all your GitHub repositories with their HTTPS URLs.

**Usage:**
```powershell
lrhttp
```

### List Repositories (SSH)

- **Function:** `list-repos-ssh`
- **Alias:** `lrssh`

**Description:** Lists all your GitHub repositories with their SSH URLs.

**Usage:**
```powershell
lrssh
```

### Remove a Repository (SSH)

- **Function:** `remove-repo-ssh`
- **Alias:** `rrssh`

**Description:** Deletes a GitHub repository using its SSH URL.

**Parameters:**
- `-repoFullName` (string, mandatory): Full name of the repository (e.g., `username/repo`).

**Usage:**
```powershell
rrssh -repoFullName "username/repo"
```

### Remove a Repository (HTTPS)

- **Function:** `remove-repo-http`
- **Alias:** `rrhttp`

**Description:** Deletes a GitHub repository using its HTTPS URL.

**Parameters:**
- `-repoFullName` (string, mandatory): Full name of the repository (e.g., `username/repo`).

**Usage:**
```powershell
rrhttp -repoFullName "username/repo"
```

### Reload PowerShell Profile

- **Function:** `reload-profile`
- **Alias:** `rp`

**Description:** Reloads your PowerShell profile to apply any changes.

**Usage:**
```powershell
rp
```

### Edit PowerShell Profile

- **Function:** `edit-profile`
- **Alias:** `ep`

**Description:** Opens your PowerShell profile in Notepad for editing.

**Usage:**
```powershell
ep
```

## Usage Examples

### Creating a Private Repository

```powershell
nr -name "myPrivateRepo" -description "This is a private repository." -private
```

### Listing All Repositories with HTTPS URLs

```powershell
lrhttp
```

### Listing All Repositories with SSH URLs

```powershell
lrssh
```

### Removing a Repository via SSH

```powershell
rrssh -repoFullName "syrym-almaty/powershellEducation"
```

### Removing a Repository via HTTPS

```powershell
rrhttp -repoFullName "syrym-almaty/powershellEducation"
```

### Reloading the PowerShell Profile

```powershell
rp
```

### Editing the PowerShell Profile

```powershell
ep
```

## Troubleshooting

### `create-repo` Not Recognized

If you encounter an error stating that `create-repo` is not recognized:

1. **Ensure Functions are Loaded:**
   Make sure your PowerShell profile includes the function definitions and aliases. Reload the profile:
   ```powershell
   . $PROFILE
   ```

2. **Check GitHub CLI Installation:**
   Verify that `gh` is installed and accessible:
   ```powershell
   gh --version
   ```

3. **Verify Token Permissions:**
   Ensure your GitHub token has the necessary permissions (`repo` or `public_repo`).

### Alias Conflicts

If an alias like `rp` is read-only or already in use:

1. **Use a Different Alias:**
   Modify the alias in your PowerShell profile to avoid conflicts.
   ```powershell
   set-alias reloadp reload-profile  # Using 'reloadp' instead of 'rp'
   ```

2. **Remove Existing Alias:**
   If you prefer to use `rp`, remove the existing alias first:
   ```powershell
   Remove-Item alias:rp -Force
   set-alias rp reload-profile
   ```


