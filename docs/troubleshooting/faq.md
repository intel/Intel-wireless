# Frequently Asked Questions (FAQ)

## Q: When I use cross-compiling backport driver, it shows error in kconf components: `./kconf/conf: 1: Syntax error: "(" unexpected`. What happened?

In several non-x86 SoC SDKs which are based on Poky/Yocto, it is necessary to run the required steps to set up the cross-compilation environment. Those steps overwrite important Makefile variables. This causes the failure of compiling kconf component in host machine. To resolve the problem, unset those environment variables:

```bash
unset CC CXX LD CFLAGS CXXFLAGS LDFLAGS
```

Then re-run the build commands.
