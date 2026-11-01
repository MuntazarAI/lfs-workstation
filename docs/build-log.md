# Build Log

This log records the current verified progress of the LFS Workstation build. It is not a substitute for the package instructions in the matching BLFS book.

## Environment

- Base system: LFS 13.1-systemd
- Architecture: x86_64
- Build user: `muntazar`
- Source directory: `/home/muntazar/sources`
- Build host: Fedora, with LFS running in a virtual machine
- VM resources: 4 vCPUs, 5 GiB RAM, 80 GiB virtual disk
- Typical build parallelism: `-j2`

## Verified packages

### CMake 4.4.2

- Status: built and installed.
- Verification: `cmake --version` reported CMake 4.4.2.
- Testing note: one isolated CTest failure was observed around stop-time behavior; 674 of 675 tests passed. Do not treat the suite as completely passing.

### cURL 8.21.0

- Status: built and installed.
- Configuration used OpenSSL, zlib, and zstd.
- HTTP/2 support was not enabled because nghttp2 was not available during configuration.
- IDN, LDAP, and libpsl support were also not enabled.
- Source archive MD5 recorded during the build: `230131079987135cbe1eadb77a04af57`.
- Verification: `curl --version` reported cURL 8.21.0 with OpenSSL 4.0.1, zlib 1.3.2, and zstd 1.5.7.

### Git 2.55.0

- Status: built, installed, and version-checked.
- Source archive MD5 recorded during the build: `758c02a1b621cc0868ee0a0d99573e6b`.
- Configure options:
  ```bash
  ./configure \
      --prefix=/usr \
      --with-gitconfig=/etc/gitconfig \
      --with-python=python3 \
      --with-libpcre2
  ```
- The first build attempt tried to invoke Cargo, which was not installed.
- The build was then cleaned and rebuilt with the Makefile option `NO_RUST=1` to disable Git's optional Rust component.
- Verified output:
  ```text
  git version 2.55.0
  /usr/bin/git
  /usr/libexec/git-core
  ```
- Scope note: disabling the Rust component means Rust-dependent optional Git functionality is not included in this build.

## Source verification notes

Checksums are useful only when compared with a trustworthy value published by the upstream project or its official release instructions. The MD5 values above preserve the checks recorded during this build; use a stronger upstream-published checksum when available.

## Next steps

- [ ] Verify HTTPS downloads with the installed cURL.
- [ ] Review Git's basic operation and configuration.
- [ ] Select essential command-line and networking utilities.
- [ ] Begin graphical-stack planning from the matching BLFS book.
