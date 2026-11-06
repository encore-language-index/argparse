# argparse

`argparse` is a small, dependency-light command-line parser for Encore
programs. It provides typed option specifications, deterministic diagnostics,
and a single process-argument boundary for command-line tools.

```encore
let spec = CommandSpec::new("build")
    .option(OptionSpec::value("--profile", "", "name", "optimization profile"))
    .option(OptionSpec::flag("--help", "-h", "show help"))

match parse(spec, process_args(2_usize)) {
    ParseOutcome::Ok(args) => { /* use args.value/has/positionals */ }
    ParseOutcome::Err(message) => { /* render one deterministic error */ }
}
```

Use `process_arg_count()` and `process_arg(index)` when a command needs the
raw process vector (for example, to forward arguments after `--`).

## SDK development

Encore pins this package as a Git submodule. Clone the complete SDK with
`git clone --recurse-submodules --branch trunk https://github.com/encore-ecosystem/encore.git`
and edit this package under `packages/argparse/`. Sibling `path@` dependencies
are resolved from that checkout. Encore CI tests the exact package commits
with the compiler on all supported native targets. Published package archives
rewrite path dependencies to exact index versions.
