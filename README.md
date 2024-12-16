# KMP Desktop Build Action

## Overview

This GitHub Action automates the build process for cross-platform desktop applications, supporting multiple operating systems and build configurations.

## Features

- 🖥️ Cross-platform support (Windows, macOS, Linux)
- 🛠️ Flexible build type configuration (Debug/Release)
- 📦 Automatic artifact generation and upload
- 🚀 Gradle build caching for improved performance

## Usage Examples

### Basic Debug Build
```yaml
  build_desktop:
     name: Build Desktop App
     strategy:
        matrix:
           os: [ ubuntu-latest, macos-latest, windows-latest ]
     runs-on: ${{ matrix.os }}
     steps:
        - name: Checkout Repository
          uses: actions/checkout@v4
          
        - name: Build Desktop App
          uses: openMF/kmp-build-desktop-app-action@v1.0.0
          with:
            desktop_package_name: 'myapp'
```

### Release Build
```yaml
  build_desktop:
     name: Build Desktop App
     strategy:
        matrix:
           os: [ ubuntu-latest, macos-latest, windows-latest ]
     runs-on: ${{ matrix.os }}
     steps:
        - name: Checkout Repository
          uses: actions/checkout@v4

        - name: Build Desktop App
          uses: openMF/kmp-build-desktop-app-action@v1.0.0
          with:
            desktop_package_name: 'myapp'
            build_type: 'Release'
```

## Inputs

### `desktop_package_name`
- **Description**: Name of the desktop project module
- **Required**: `true`
- **Type**: `string`
- **Example**: `'mydesktopapp'`

### `build_type`
- **Description**: Type of build to perform
- **Required**: `false`
- **Default**: `'Debug'`
- **Accepted Values**:
   - `'Debug'`
   - `'Release'`

## Outputs

### Platform-Specific Artifact Names
- **Windows**: `Windows-Apps`
   - Contains: `.exe` and `.msi` files
- **Linux**: `Linux-App`
   - Contains: `.deb` files
- **macOS**: `MacOS-App`
   - Contains: `.dmg` files

## Best Practices

- Always specify the `desktop_package_name`
- Use `Release` build type for production distributions
- Check artifact names carefully when downloading
- Verify file integrity after download

## Troubleshooting

### Common Issues
- Ensure Gradle build script is correctly configured
- Check that packaging commands match your project structure
- Verify Java 17 is installed and compatible

### Debugging
- Review GitHub Actions logs for detailed build information
- Check Gradle build output for specific errors
- Ensure all required dependencies are included in the build

## Requirements

- Java 17
- Gradle
- Compatible Kotlin Multiplatform Desktop configuration