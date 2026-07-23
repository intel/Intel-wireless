# Frequently Asked Questions (FAQ)

## Q: Why does cross-compiling the backport driver produce the following kconf error: `./kconf/conf: 1: Syntax error: "(" unexpected`. What is the cause and resolution?

In several non-x86 SoC SDKs that are based on Poky/Yocto, it is necessary to run the required steps to set up the cross-compilation environment. Those steps overwrite important Makefile variables. This causes the compilation of the kconf component to fail in the host machine. To resolve the problem, unset those environment variables:

```bash
unset CC CXX LD CFLAGS CXXFLAGS LDFLAGS
```

Then re-run the build commands.
