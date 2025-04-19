# xv6 on Apple Silicon

This repo documents how to build and run MIT's [xv6-riscv](https://github.com/mit-pdos/xv6-riscv) teaching operating system on Apple Silicon Macs (M1, M2, M3, M4).

You’ll be using `riscv64-elf-gcc`, `riscv64-elf-binutils`, and `qemu` — no need to build the full RISC-V GNU toolchain.

---

## Requirements

- macOS 11+ (Apple Silicon)
- Homebrew
- QEMU (with RISC-V support)
- `riscv64-elf-gcc` and `riscv64-elf-binutils`

---

## Setup

### 1. Install Homebrew (if not already)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install Required Packages

```bash
brew install qemu riscv64-elf-gcc riscv64-elf-binutils
```

Confirm the tools are available:

```bash
riscv64-elf-gcc --version
which riscv64-elf-gcc
```

> If you run into PATH issues, ensure Homebrew’s bin path is in your shell profile:
>
> ```bash
> echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zprofile
> source ~/.zprofile
> ```

---

## Clone xv6 and Build

```bash
git clone https://github.com/mit-pdos/xv6-riscv.git
cd xv6-riscv
make TOOLPREFIX=riscv64-elf- qemu
```

> You must specify `TOOLPREFIX=riscv64-elf-` so that `make` knows to use your installed toolchain.

---

## Notes for Apple Silicon

- Use the Terminal or iTerm2 — some other terminal emulators might cause QEMU to behave incorrectly.
- You do **not** need the full `riscv-gnu-toolchain` to build xv6.
- If you get errors like “command not found” or linker errors, double-check that both `riscv64-elf-gcc` and `riscv64-elf-ld` are installed.

---

## Optional: Avoid Repeating TOOLPREFIX

If you don't want to pass `TOOLPREFIX` every time, add the following to the top of the `Makefile`:

```make
TOOLPREFIX = riscv64-elf-
```

---

## Tested On

- ✅ macOS Sequoia 14.4
- ✅ Apple M4 Pro
- ✅ QEMU 9.2.3 (via Homebrew)
- ✅ riscv64-elf-gcc 14.2.0

---

## Resources

- [xv6-riscv GitHub Repo](https://github.com/mit-pdos/xv6-riscv)
- [6.S081 (MIT OS Course)](https://pdos.csail.mit.edu/6.828/2023/)
- [QEMU RISC-V Docs](https://wiki.qemu.org/Documentation/Platforms/RISCV)

---

## Tags

`xv6` `risc-v` `macos` `apple-silicon` `m1` `m2` `m3` `m4` `qemu` `osdev`
