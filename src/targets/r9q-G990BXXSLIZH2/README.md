# SM-G990B G990BXXSLIZH2 source set

This directory contains the exact source used for the hardware-proven
`SM-G990B` / `G990BXXSLIZH2` payload.

Samsung's 5.4 kernel requires target-specific compiler stack geometry for the
legacy `rt_mutex_waiter` overlay. The proven route uses a pselect result-copy
COW fault and `overlay_asm.S`; newer shared-engine changes must not silently
alter those frames. For that reason the Makefile selects the frozen `port/`
source set only for this target.

Build with NDK r27b:

```sh
ANDROID_NDK_HOME=/path/to/android-ndk-r27b \
  make TARGET=r9q-G990BXXSLIZH2
```

The target automatically uses API 30 for the exploit and API 35 for the
generic Root My Galaxy helper. A clean build reproduces:

```text
bea1dbcf12de52dc902a29e79fe2f929e8e6e078a24123507ad92ff28eebfc0e  cve-2026-43499-app.so
fd193ddecbc5db5d13e72281cf54ce3ae054e1b3d8728c1dfc64ff1fc80d0bb8  cve-2026-43499-root
```

The full hardware record and KernelSU details are in
[`../../../docs/SM-G990B-G990BXXSLIZH2.md`](../../../docs/SM-G990B-G990BXXSLIZH2.md).
