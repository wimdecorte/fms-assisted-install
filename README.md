# FileMaker Server Assisted Install Configuration

This repository contains assisted installation configuration files for FileMaker Server across different platforms, along with a unified configuration file that combines all available options.

For detailed information about assisted installation, refer to the official Claris documentation: [Assisted Install of FileMaker Server 17 and later](https://support.claris.com/s/article/Assisted-install-of-FileMaker-Server-17-and-later?language=en_US)

## Files Overview

- `macOS/Assisted Install.txt` - macOS-specific configuration
- `Ubuntu/Assisted Install.txt` - Ubuntu/Linux-specific configuration  
- `Windows/Assisted Install.txt` - Windows-specific configuration
- `assisted_installer_unified.txt` - Unified configuration containing all options

## Configuration Options

### Common Options (All Platforms)

These options are available across macOS, Ubuntu, and Windows:

| Option | Default Value | Description |
|--------|---------------|-------------|
| `License Accepted` | 0 | Set to 1 to automatically accept the FileMaker Server license agreement during installation |
| `Organization` | (empty) | Organization name that will be associated with the FileMaker Server installation |
| `Deployment Options` | 0 | Deployment configuration type (0=single machine, 1=multiple machines) |
| `FileMaker Server User` | 0 | User account configuration for FileMaker Server service (0=system default, 1=custom user) |
| `Admin Console User` | (empty) | Username for accessing the FileMaker Server Admin Console |
| `Admin Console Password` | (empty) | Password for accessing the FileMaker Server Admin Console |
| `Admin Console PIN` | (empty) | Additional PIN for enhanced security when accessing the Admin Console |
| `License Certificate Path` | (empty) | Full path to the FileMaker Server license certificate file (.fmsl) |
| `Remove Sample Database` | 0 | Set to 1 to automatically remove the sample database after installation |
| `Remove Desktop Shortcut` | 0 | Set to 1 to remove desktop shortcuts created during installation |
| `Load Previous Configuration` | 0 | Set to 1 to restore previous FileMaker Server configuration settings |
| `Filter Databases` | 1 | Set to 1 to enable database filtering during the installation process |
| `Use HTTPS Tunneling` | 0 | Set to 1 to enable HTTPS tunneling for secure connections |

### Platform-Specific Options

#### Windows Only

| Option | Default Value | Description | Version Introduced |
|--------|---------------|-------------|-------------------|
| `Disable 8dot3 Name Creation` | 1 | Set to 1 to disable the creation of 8.3 format file names on Windows for improved performance | FMS 26.0.1 |

#### macOS and Windows Only

| Option | Default Value | Description |
|--------|---------------|-------------|
| `Launch Deployment Assistant` | 1 | Set to 1 to automatically launch the Deployment Assistant after installation completes |
| `Skip Dialogs` | 0 | Set to 1 to skip interactive installation dialogs and use configuration file values |

#### Ubuntu/Linux Only

| Option | Default Value | Description |
|--------|---------------|-------------|
| `Security Check` | 1 | Set to 1 to perform system security checks during installation (Linux-specific) |
| `Swap File Size` | (empty) | Size of the swap file to create in megabytes (e.g., "2048" for 2GB) |
| `Swappiness` | 10 | Linux kernel swappiness parameter (0-100, controls swap file usage) |
| `Preserve Firewall` | 0 | Set to 1 to preserve existing firewall settings during installation |

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

Option Name=Value

Another Option=Value
```

### Value Types

- **Boolean values**: `0` (false) or `1` (true)
- **String values**: Any text string (can be empty)
- **Numeric values**: Integer values (e.g., `10` for Swappiness)

## Notes

- Empty values indicate that the option will use system defaults or prompt for user input
- Boolean options use `0` for false and `1` for true
- Platform-specific options are automatically ignored on unsupported platforms
- The unified file serves as a comprehensive reference for all available configuration options
