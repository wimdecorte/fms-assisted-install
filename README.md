# FileMaker Server Assisted Install Configuration

This repository contains assisted installation configuration files for FileMaker Server across different platforms, along with a unified configuration file that combines all available options.

For detailed information about assisted installation, refer to the official Claris documentation: [Assisted Install of FileMaker Server 17 and later](https://support.claris.com/s/article/Assisted-install-of-FileMaker-Server-17-and-later?language=en_US)

## Files Overview

- `macOS/Assisted Install.txt` - macOS-specific configuration
- `Ubuntu/Assisted Install.txt` - Ubuntu/Linux-specific configuration  
- `Windows/Assisted Install.txt` - Windows-specific configuration
- `assisted_installer_unified.txt` - Unified configuration containing all options

## File Location Requirements

The Assisted Install.txt file must be placed in the correct location for each platform:

- **Windows**: Assisted Install.txt and Setup.exe must be in the Files folder during installation
- **macOS**: Assisted Install.txt must be in the same folder as the FileMaker Server installer application during installation  
- **Linux**: Assisted Install.txt must be in the same folder as the FileMaker Server DEB installer during installation

**Note**: The Assisted Install.txt file is cross-platform compatible. The same file can be used for installing on Windows, macOS, and Linux systems.

## Configuration Options

### Common Options (All Platforms)

These options are available across macOS, Ubuntu, and Windows:

| Option | Default Value | Description | Version Introduced |
|--------|---------------|-------------|-------------------|
| `License Accepted` | 0 | Set to 1 to automatically accept the FileMaker Server license agreement during installation | FMS 18 |
| `Organization` | (empty) | Organization name that will be associated with the FileMaker Server installation | - |
| `Deployment Options` | 0 | Deployment configuration type (0=single machine, 1=multiple machines) | - |
| `FileMaker Server User` | 0 | User account configuration for FileMaker Server service (0=system default, 1=custom user) | - |
| `Admin Console User` | admin | Username for accessing the FileMaker Server Admin Console | - |
| `Admin Console Password` | (empty) | Password for accessing the FileMaker Server Admin Console | - |
| `Admin Console PIN` | (empty) | Four-digit PIN for command line interface (CLI) password reset | - |
| `License Certificate Path` | (empty) | Full path to the FileMaker Server license certificate file (.fmcert) | - |
| `Remove Sample Database` | 0 | Set to 1 to automatically remove the sample database after installation | FMS 2023 |
| `Remove Desktop Shortcut` | 0 | Set to 1 to remove desktop shortcuts created during installation | FMS 2023 |
| `Load Previous Configuration` | 0 | Set to 1 to restore previous FileMaker Server configuration settings | FMS 2023 |
| `Filter Databases` | 0 | Set to 1 to enable database filtering during the installation process | FMS 2023 |
| `Use HTTPS Tunneling` | 0 | Set to 1 to enable HTTPS tunneling for secure connections | FMS 2024 |

### Platform-Specific Options

#### Windows Only

| Option | Default Value | Description | Version Introduced |
|--------|---------------|-------------|-------------------|
| `Disable 8dot3 Name Creation` | 1 | Set to 1 to disable the creation of 8.3 format file names on Windows for improved performance | FMS 26.0.1 |

#### macOS and Windows Only

| Option | Default Value | Description | Version Introduced |
|--------|---------------|-------------|-------------------|
| `Launch Deployment Assistant` | 1 | Set to 1 to automatically launch the Deployment Assistant after installation completes | - |
| `Skip Dialogs` | 0 | Set to 1 to skip interactive installation dialogs and use configuration file values | - |

#### Ubuntu/Linux Only

| Option | Default Value | Description | Version Introduced |
|--------|---------------|-------------|-------------------|
| `Security Check` | 1 | Set to 1 to perform system security checks during installation (Linux-specific) | - |
| `Swap File Size` | (varies) | Size of the swap file to create (e.g., "1G" for 1GB, "2G" for 2GB) | FMS 2024 |
| `Swappiness` | 10 | Linux kernel swappiness parameter (0-200, controls swap file usage). See [official kernel documentation](https://askubuntu.com/a/103916) for detailed explanation of values | FMS 2024 |
| `Preserve Firewall` | 0 | Set to 1 to preserve existing firewall settings during installation | - |

## Usage

### Platform-Specific Installation

Use the appropriate configuration file for your target platform:

- **macOS**: Use `macOS/Assisted Install.txt`
- **Ubuntu/Linux**: Use `Ubuntu/Assisted Install.txt`  
- **Windows**: Use `Windows/Assisted Install.txt`

### Cross-Platform Development

For development or testing across multiple platforms, use `assisted_installer_unified.txt` which contains all available options. Note that platform-specific options will be ignored on platforms that don't support them.

## Configuration Format

All configuration files follow the same INI-style format:

```ini
[Assisted Install]

License Accepted=1
Organization=Your Company Name
Admin Console User=admin
Admin Console Password=YourSecurePassword
Admin Console PIN=1234
License Certificate Path=C:\Users\username\Downloads\LicenseCert.fmcert
```

### Example File Paths

**License Certificate Path examples:**
- Windows: `C:\Users\username\Downloads\LicenseCert.fmcert`
- macOS: `/Users/username/Downloads/LicenseCert.fmcert`
- Linux: `/home/username/Downloads/LicenseCert.fmcert`

**Swap File Size examples (Linux only):**
- 1GB swap file: `1G`
- 2GB swap file: `2G`
- 4GB swap file: `4G`

### Value Types

- **Boolean values**: `0` (false) or `1` (true)
- **String values**: Any text string (can be empty)
- **Numeric values**: Integer values (e.g., `10` for Swappiness)
- **File sizes**: Use format like `1G`, `2G`, `4G` for swap file sizes

## Notes

- Empty values indicate that the option will use system defaults or prompt for user input
- Boolean options use `0` for false and `1` for true
- Platform-specific options are automatically ignored on unsupported platforms
- The unified file serves as a comprehensive reference for all available configuration options

### Important Installation Notes

- **License Certificate**: FileMaker Server uses a license certificate (.fmcert) to set the license key. You receive this via email with a link to your software download page. Keep a copy in a safe place for reinstallation purposes.
- **Silent Installation**: For silent installations, `License Accepted=1` is required. If left at the default `0`, the installation will stop.
- **Organization Name**: When specifying an organization, type the name exactly as it appears on the software download page.
- **Multiple-Machine Deployments**: You need separate Assisted Install.txt files for the primary machine and FileMaker WebDirect secondary machines.
- **Default Swap File Sizes**: Linux installations use default swap file sizes of 1GB, 2GB, and 4GB depending on available free space.
- **Swappiness Values**: 
  - `0` = Avoid using swap file unless absolutely necessary
  - `100` = Equal cost between swap and filesystem paging (balanced)
  - `200` = Maximum swap usage preference
  - Default is `10`
  - Range is 0-200 (see [official kernel documentation](https://askubuntu.com/a/103916))
