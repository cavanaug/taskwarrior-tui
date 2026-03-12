## Running Tests

### Unit tests (no external data needed)

Most tests (keyconfig parsing, priority cycling, help rendering, etc.) run without
any external setup:

```sh
cargo test -- --skip test_taskwarrior_tui
```

### Integration tests (require test data)

The `test_taskwarrior_tui` test needs `TASKDATA` and `TASKRC` environment variables
pointing at a taskwarrior data directory. Clone the upstream test fixtures first:

```sh
git clone https://github.com/kdheepak/taskwarrior-testdata.git
```

Then run tests with the env vars set:

```sh
TASKRC=taskwarrior-testdata/.taskrc TASKDATA=taskwarrior-testdata/.task cargo test
```

Alternatively, if you use `direnv`, the `.envrc` file expects the data at `tests/data/`:

```sh
mkdir -p tests/data
cp -r taskwarrior-testdata/.task tests/data/.task
cp taskwarrior-testdata/.taskrc tests/data/.taskrc
direnv allow
cargo test
```
