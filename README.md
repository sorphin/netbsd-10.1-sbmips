# NetBSD/sbmips 10.1 — Full Release for Broadcom SiByte SB1 (BCM1250 / BCM1280 / BCM1480)

This repository provides a fully built NetBSD 10.1 release for Broadcom SiByte SB1 systems (BCM1250 / BCM1280 / BCM1480 and other SiByte-based MIPS64 big‑endian boards).

IMPORTANT: This is an UNOFFICIAL BUILD by **sorphin**, not an official NetBSD distribution. Use at your own risk.

---

## What's included

A complete, bootable NetBSD 10.1 release for the sbmips target.

- releases/kernel/
  - netbsd-GENERIC.gz
  - MD5
  - SHA512
- releases/sets/
  - base.tgz
  - comp.tgz
  - etc.tgz
  - kern-GENERIC.tgz
  - modules.tgz
  - misc.tgz
  - tests.tgz
  - text.tgz
  - man.tgz
  - rescue.tgz
  - games.tgz
  - gpufw.tgz
  - MD5
  - SHA512

SHA512 and MD5 lists are provided for verification.

---

## Build note

Built with the official NetBSD `build.sh`:

```
./build.sh -m sbmips -a mipseb -T ../tools -O ../obj -D ../dest -U -N0 release
```

Host: Linux x86_64 (Debian-like container).

Toolchain auto-built by `build.sh`.

No nonstandard compiler flags.

---

## Patch note

NetBSD 10.1 has a minor build regression in the `crash(8)` tool for sbmips due to a missing include for `bool`.

This build contains a one-line fix that simply adds:

```c
#include <sys/stdbool.h>
```

to:

```
sys/arch/sbmips/include/systemsw.h
```

so it looks like this:
```
#include <sys/types.h>
/* Added by sorphin to fix build - 11172025 */
#include <sys/stdbool.h>
```

Everything else builds cleanly.

---

## Checksums & signature

SHA512 and MD5 checksums are included (see `netbsd-sbmips-10.1-release/releases/kernel/SHA512` and `netbsd-sbmips-10.1-release/releases/sets/SHA512`). 

Advanced users will know how to verify hashes and signatures for their preferred workflow.

---

## License

Binaries originate from the NetBSD source tree (2-clause BSD license).

Additions/patches/README here are MIT unless otherwise noted.

Do not include or redistribute non-redistributable third-party blobs.

---

## Credits & contact

Built and tested on SB1 hardware by sorphin.

For questions or issues, open an issue in this repository: https://github.com/sorphin/netbsd-10.1-sbmips
