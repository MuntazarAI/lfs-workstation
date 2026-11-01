# LFS Workstation

A hands-on engineering project to build a practical Linux workstation from **Linux From Scratch (LFS) 13.1-systemd** and **Beyond Linux From Scratch (BLFS) 13.1-systemd**.

The purpose is to understand how a Linux system is assembled, keep the build reproducible, and eventually create a lightweight development environment for Python, AI, and the existing JARVIS OS project.

> **Project status:** In progress. This repository is a build log and documentation project—not a ready-to-install Linux distribution.

## Contents

- [Project goals](#project-goals)
- [Build environment](#build-environment)
- [Verified progress](#verified-progress)
- [Engineering principles](#engineering-principles)
- [Roadmap](#roadmap)
- [Documentation](#documentation)
- [Build and verification notes](#build-and-verification-notes)
- [Official references](#official-references)
- [Scope and limitations](#scope-and-limitations)

## Project goals

- Build and maintain a custom LFS/BLFS system.
- Document versions, dependencies, commands, checksums, tests, and troubleshooting.
- Add a lightweight graphical desktop and practical workstation applications.
- Prepare a development environment for software engineering, Python, and AI.
- Later, assess and integrate the existing JARVIS OS project without restarting or duplicating its architecture.

## Build environment

| Item | Details |
|---|---|
| Base system | LFS 13.1-systemd |
| Architecture | x86_64 |
| Build host | Fedora, using a virtual machine |
| VM resources | 4 vCPUs, 5 GiB RAM, 80 GiB virtual disk |
| Compiler | GCC / G++ 16.2.0 |
| Build tool | GNU Make 4.4.1 |
| Typical parallelism | `make -j2` |

## Verified progress

| Component | Version | Status |
|---|---:|---|
| LFS base system | 13.1-systemd | Booted and usable in the VM |
| GCC / G++ | 16.2.0 | Available |
| GNU Make | 4.4.1 | Available |
| OpenSSL | 4.0.1 | Available |
| CMake | 4.4.2 | Built, installed, and version-checked |
| cURL / libcurl | 8.21.0 | Built and installed with OpenSSL, zlib, and zstd |
| PCRE2 | 10.47 | Available for Git configuration |
| Git | 2.55.0 | Built with optional Rust support disabled; installed and verified |
| FreeType | 2.14.3 | Installed; header version verified |
| Fontconfig | 2.18.3 | Installed; `pkg-config` and `fc-cache` verified |
| Xfce desktop | — | Planned |
| Browser and everyday applications | — | Planned |
| Python / AI development environment | — | Planned |
| JARVIS OS integration | — | Planned |

Git installation was verified in the LFS system:

```text
git version 2.55.0
/usr/bin/git
/usr/libexec/git-core
```

Git's optional Rust component was disabled because Cargo was not installed in the LFS environment. This does not mean Rust or Cargo is installed, and it does not imply that every optional Git feature is enabled.

## Engineering principles

1. **Follow the matching official book.** Use LFS/BLFS 13.1-systemd instructions for package configuration and installation.
2. **Verify source archives.** Check a published checksum before extracting and compiling.
3. **Build as an unprivileged user.** Configure and compile as the normal build user; use root for system-wide installation when required.
4. **Record reproducible details.** Keep versions, configure options, test results, and fixes in the project notes.
5. **Install deliberately.** Add only the dependencies and applications needed for the intended workstation.
6. **Protect private data.** Never commit credentials, access tokens, private keys, personal backups, or private configuration.
7. **Report status honestly.** Mark a component complete only after verifying it on the actual system.

## Roadmap

- [x] Build and install CMake 4.4.2
- [x] Build and install cURL 8.21.0
- [x] Build and install Git 2.55.0
- [x] Build and verify FreeType 2.14.3 and Fontconfig 2.18.3
- [ ] Record and test basic HTTPS downloads and source verification
- [ ] Select essential command-line and networking tools
- [ ] Build the required graphical stack using BLFS instructions
- [ ] Install and configure Xfce
- [ ] Add a browser, terminal, file manager, editor, and audio support
- [ ] Set up Python and development dependencies
- [ ] Review the existing JARVIS OS requirements and integrate what the system can support
- [ ] Document setup, recovery, and maintenance procedures

## Documentation

- [Documentation index](docs/README.md)
- [Build log](docs/build-log.md)
- [Troubleshooting notes](docs/troubleshooting.md)

## Build and verification notes

The VM has 4 vCPUs and 5 GiB RAM, so two parallel jobs are the default for builds:

```bash
make -j2
```

Use each package's documented build procedure rather than applying this command blindly to every package. Run package tests when practical and record any failures or skipped tests.

### Verified source archives

| Package | Version | Recorded checksum |
|---|---:|---|
| cURL | 8.21.0 | MD5: `230131079987135cbe1eadb77a04af57` |
| Git | 2.55.0 | MD5: `758c02a1b621cc0868ee0a0d99573e6b` |
| Fontconfig | 2.18.3 | MD5: `ce819e229ca6fb7d1be47a192d6681a3` |
| CMake | 4.4.2 | Checksum verified before building; see the original package notes for the exact value |

The cURL and Git MD5 values above are recorded to preserve the checks used during this build. Prefer a stronger checksum (such as SHA-256) when published by the package source.

## Official references

- [Linux From Scratch](https://www.linuxfromscratch.org/lfs/)
- [Beyond Linux From Scratch](https://www.linuxfromscratch.org/blfs/)
- [BLFS 13.1-systemd book](https://www.linuxfromscratch.org/blfs/view/13.1-systemd/)

## Scope and limitations

This is a personal learning and engineering log. It is not currently a general-purpose distribution or a production security claim. Hardware support, package availability, optional features, and planned capabilities must be verified on the actual system as the project develops.
