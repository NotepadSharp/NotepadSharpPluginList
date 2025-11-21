# NotepadSharp Plugin List

**NotepadSharp Plugin List** is the official repository for community plugins compatible with the cross-platform text editor [NotepadSharp](https://github.com/yourusername/notepadsharp "null").

This repository serves as the single, verified source for the built-in **Plugin Manager** within the NotepadSharp application, allowing users to safely install, update, and manage extensions across Windows, Linux, and macOS.

## 🛡️ Security and Verification (Trusted Build)

To ensure the highest level of security and integrity for our cross-platform users, NotepadSharp utilizes a **Trusted Build** model:

1. **Source Code Required:** All submissions must reference the source code in a public repository.
    
2. **Verified Artifacts:** The final plugin DLLs are **not** provided by the external developer. Instead, they are built, scanned, and digitally sealed by our continuous integration (CI) pipeline within a secure environment.
    
3. **Hash Verification:** The `pl.json` list contains the SHA-256 hash of the CI-built DLL, which NotepadSharp verifies upon download.
    

## Submitting a Plugin

We welcome all compatible plugins built using the [NotepadSharp Plugin SDK](https://github.com/yourusername/notepadsharp "null").

### Submission Requirements

To submit a plugin, please open a Pull Request (PR) to this repository and update the `plugins.json` manifest file following the required schema. Your PR must include:

1. **Repository URL:** The public URL of the plugin's source code repository.
    
2. **Commit Hash/Tag:** A specific, stable Git commit hash or tag (e.g., `v1.0.0`) that identifies the exact version of the source code we are authorized to build.
    
3. **Licensing:** Confirmation that the plugin is provided under an open-source license (e.g., MIT, Apache 2.0).
    

Please ensure your plugin builds successfully locally before submitting your PR.

## Current Plugin Manifests

The main manifest file is updated automatically by the CI/CD pipeline after a successful build and security scan.

- [Plugin List Manifest (JSON)](https://www.google.com/search?q=pl.json "null") - The core file consumed by the NotepadSharp Plugin Manager.
    

## Build Status and Releases

The Continuous Integration (CI) pipeline is responsible for building, scanning, and releasing all plugins in this list.

## Support and Questions

For questions about the Plugin Manager or how to develop plugins, please check the main application repository:

- [NotepadSharp GitHub Discussions](https://github.com/yourusername/notepadsharp/discussions "null")
    
- [Plugin Architecture Documentation](https://www.google.com/search?q=https://github.com/yourusername/notepadsharp%23plugin-system "null")
    

_Made with .NET and Avalonia UI for the cross-platform community._