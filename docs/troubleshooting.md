# Troubleshooting Notes

This file records problems encountered during the LFS Workstation build and the resolution confirmed on the system.

## Git 2.55.0 build failed because Cargo was missing

**Symptom**

The build reported:

```text
/bin/sh: line 1: cargo: command not found
make: *** [Makefile:3021: target/release/libgitcore.a] Error 127
```

**Cause**

Git 2.55.0 can optionally compile Rust-based components. Cargo was not installed in the LFS environment, and the existing build attempted to compile that component.

**Resolution**

From the Git source directory, as the unprivileged build user:

```bash
cd /home/muntazar/sources/git-2.55.0
make clean
make -j2 NO_RUST=1
```

After the build completed successfully, install as root:

```bash
cd /home/muntazar/sources/git-2.55.0
make NO_RUST=1 perllibdir=/usr/lib/perl5/5.44/site_perl install
```

**Verification**

```text
git version 2.55.0
/usr/bin/git
/usr/libexec/git-core
```

**Lesson**

Use `NO_RUST=1` as a Make variable for both the build and install commands. Verify the installed executable before recording the milestone as complete.

## SSH login shell warning when using `su - muntazar`

**Symptom**

The shell printed warnings such as:

```text
su: cannot set terminal process group (-1): Inappropriate ioctl for device
su: no job control in this shell
```

**Meaning**

This can happen when switching users from a session without a controlling terminal. The shell may still accept and run commands, but interactive job control is unavailable.

**Practical check**

Run `pwd` to confirm the working directory before running commands that depend on a specific source path. Use `cd /home/muntazar/sources/<package-directory>` explicitly when needed.
