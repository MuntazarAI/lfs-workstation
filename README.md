# LFS Workstation

A learning project to build a practical, custom Linux workstation from **Linux From Scratch (LFS) 13.1-systemd** and **Beyond Linux From Scratch (BLFS) 13.1-systemd**.

The goal is to understand how a Linux system is assembled, document each step reproducibly, and eventually create a lightweight development environment for working on the existing JARVIS OS project.

> **Status:** In progress. This repository documents the build; it is not a ready-to-install distribution.

## Goals

- Build and maintain a custom LFS/BLFS system.
- Keep notes on build commands, dependencies, verification, and troubleshooting.
- Add a lightweight desktop environment and everyday workstation applications.
- Prepare a development environment for Python, software engineering, and AI projects.
- Later, evaluate and integrate the existing JARVIS OS project without duplicating or restarting its architecture.

## Current environment

- **Base:** Linux From Scratch 13.1-systemd
- **Architecture:** x86_64
- **Build environment:** Virtual machine on a Fedora host
- **VM resources:** 4 vCPUs, 5 GiB RAM, 80 GiB virtual disk
- **Compiler:** GCC 16.2.0
- **Build parallelism:** Usually `make -j2` to fit the VM's resources

## Build progress

| Component | Version | Status |
|---|---:|---|
| LFS base system | 13.1-systemd | Booted and usable in the VM |
| GCC / G++ | 16.2.0 | Available |
| GNU Make | 4.4.1 | Available |
| OpenSSL | 4.0.1 | Available |
| CMake | 4.4.2 | Built and installed |
| cURL / libcurl | 8.21.0 | Built and installed with OpenSSL, zlib, and zstd |
| PCRE2 | 10.47 | Available for Git configuration |
| Git | 2.55.0 | Source checksum verified; configuration completed; build and installation pending |
| Xfce desktop | — | Planned |
| Browser and everyday applications | — | Planned |
| Python / AI development environment | — | Planned |
| JARVIS OS integration | — | Planned |

This table reflects the progress recorded in the project notes and will be updated as work is verified.

## Principles

1. **Follow the official book.** Use the matching LFS/BLFS 13.1-systemd documentation and package instructions.
2. **Verify source archives.** Check published checksums before extracting and compiling source code.
3. **Build as an unprivileged user.** Run configure and compilation as the normal build user; use root only for installation steps that require system-wide writes.
4. **Keep notes reproducible.** Record versions, configure options, test outcomes, and relevant fixes.
5. **Install only what is needed.** Add dependencies in a deliberate order instead of attempting to install every BLFS package.
6. **Protect secrets and personal data.** Never commit credentials, private keys, tokens, private configuration, or unrelated backups.

## Planned roadmap

- [ ] Finish Git 2.55.0 build and installation; verify `git --version`
- [ ] Check basic HTTPS downloads and source verification
- [ ] Install selected command-line and networking tools
- [ ] Build the graphical stack using the official BLFS instructions
- [ ] Install and configure Xfce
- [ ] Add a browser, terminal, file manager, editor, and audio support
- [ ] Set up Python and development dependencies
- [ ] Review the existing JARVIS OS requirements and integrate only what the system can support
- [ ] Document final setup, recovery, and maintenance steps

## Build notes

For this VM, two parallel build jobs are the default:

```bash
make -j2
```

Do not run this blindly for every package: use each package's official BLFS instructions, required configuration, tests, and installation procedure.

### Verified source archives so far

- **CMake 4.4.2** — source archive checksum verified before building.
- **cURL 8.21.0** — MD5 `230131079987135cbe1eadb77a04af57` verified before building.
- **Git 2.55.0** — MD5 `758c02a1b621cc0868ee0a0d99573e6b` verified; configuration succeeded. Compilation and installation are not yet complete.

MD5 is recorded here to match the source checksum provided by the corresponding package instructions; prefer stronger published checksums when available.

## Documentation

- [Linux From Scratch](https://www.linuxfromscratch.org/lfs/)
- [Beyond Linux From Scratch](https://www.linuxfromscratch.org/blfs/)
- [BLFS 13.1-systemd book](https://www.linuxfromscratch.org/blfs/view/13.1-systemd/)

## Scope

This repository is a personal learning and engineering log. Package availability, build results, and planned features are not claims of a production-ready or secure general-purpose distribution. Each stage will be marked complete only after it has been tested on the actual system.
