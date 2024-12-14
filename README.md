# KMP Build Desktop App GitHub Action

## Overview

This GitHub Action is designed to build desktop applications for multiple platforms (Windows, Linux, MacOS) using Kotlin Multiplatform (KMP) and Gradle. It automates the process of setting up the development environment, building the application, and uploading platform-specific artifacts.

## Features

- Sets up Java 17 development environment using Zulu OpenJDK
- Configures Gradle build system
- Implements caching to speed up subsequent builds
- Packages desktop application for the current operating system
- Uploads platform-specific executables and installers as artifacts

## Inputs

### `desktop_package_name`
- **Description**: Name of the desktop project module
- **Required**: Yes
- **Type**: String

## Platforms Supported

- Windows
- Linux (Ubuntu)
- macOS

## Usage Example

```yaml
jobs:
  build-desktop-app:
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v4
      - uses: openMF/kmp-build-desktop-app-action@v1.0.0
        with:
          desktop_package_name: 'my-desktop-module'
```

## Build Process

The action performs the following steps:

1. Set up Java 17 development environment using Zulu OpenJDK
2. Configure Gradle build system
3. Cache Gradle dependencies and build outputs
4. Package desktop application using `./gradlew packageDistributionForCurrentOS`
5. Upload platform-specific artifacts:
    - Windows: `.exe` and `.msi` files
    - Linux: `.deb` files
    - macOS: `.dmg` files

## Prerequisites

- A Kotlin Multiplatform project configured for desktop application development
- Gradle wrapper in the project
- Gradle task `packageDistributionForCurrentOS` defined for building desktop distributions

## Recommendations

- Ensure your Gradle build script includes the necessary configuration for packaging desktop applications
- Test the action in your project's continuous integration workflow
- Verify that the `packageDistributionForCurrentOS` task works correctly locally before integrating this action
