# ebpf
## Starting point for me
* [Linux Observability with BPF](https://www.amazon.com/gp/product/1492050202) book
## Core concepts
### Programming model
- A userspace program loads an ebpf program into the kernel via the [bpf](https://man7.org/linux/man-pages/man2/bpf.2.html) syscall.
  - Also via `bpf_prog_load` in [bpf-helpers](https://man7.org/linux/man-pages/man7/bpf-helpers.7.html)
- The above userspace program and the ebpf program communicate via message passing using eBPF maps.
- Message passing uses eBPF maps for data. There are multiple map types.
  - There are helpers in [bpf-helpers](https://man7.org/linux/man-pages/man7/bpf-helpers.7.html) to setup different ebpf map types.

### kprobes
- https://www.kernel.org/doc/html/v5.10/trace/kprobes.html
- Hook almost any kernel routine
- Gets packaged like a kernel module
- Can modify registers and stack - be careful (dbl check - what does the verifier do for kprobe safety)
- Can run pre or post call
- Unstable across kernel versions

### tracepoints
- https://www.kernel.org/doc/html/v5.10/trace/tracepoints.html
- Stable hooks pre-defined by developers
- Guaranteed to always be same across kernel versions
- Doesn't cover all routines
- Also works pre/post call.
- /sys/kernel/debug/tracing filesystem
  - How to use the above file system https://www.kernel.org/doc/html/v5.10/trace/events.html

## Useful links
- https://github.com/bpftools/linux-observability-with-bpf
- [bpf-helpers](https://man7.org/linux/man-pages/man7/bpf-helpers.7.html)
- [bpf syscall](https://man7.org/linux/man-pages/man2/bpf.2.html)
- Headers for userspace program:
  - https://github.com/torvalds/linux/blob/737d0646a83cdc65c070a9de61a1ef106cca5ff1/tools/lib/bpf/bpf_helpers.h
  - https://github.com/torvalds/linux/blob/737d0646a83cdc65c070a9de61a1ef106cca5ff1/tools/lib/bpf/bpf.h
- Headers for bpf program in kernel (I think):
  - https://github.com/torvalds/linux/blob/737d0646a83cdc65c070a9de61a1ef106cca5ff1/include/linux/bpf.h
- BPF Complier Collection (BCC): https://github.com/iovisor/bcc/tree/master
  - Tutorial: https://github.com/iovisor/bcc/blob/master/docs/tutorial_bcc_python_developer.md
