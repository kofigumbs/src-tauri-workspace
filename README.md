**TL;DR** `cargo metadata` always gets it right.

Normally, the target directory is `../target` (relative to `tauri.conf.json`):
```
~/Documents/src-tauri-workspace (master)
$ bash -c 'cd standard/src-tauri && cargo metadata --format-version=1 | jq .target_directory'
"/Users/kofi/Documents/src-tauri-workspace/standard/src-tauri/target"
```

`cargo/config.toml` can override:
```
~/Documents/src-tauri-workspace (master)
$ cat custom-target/.cargo/config.toml
[build]
target-dir = "custom-target"

~/Documents/src-tauri-workspace (master)
$ bash -c 'cd custom-target/src-tauri && cargo metadata --format-version=1 | jq .target_directory'
"/Users/kofi/Documents/src-tauri-workspace/custom-target/custom-target"
```

For workspaces, the target directory is in the workspace root:
```
~/Documents/src-tauri-workspace (master)
$ bash -c 'cd a-workspace && cargo metadata --format-version=1 | jq .target_directory'
"/Users/kofi/Documents/src-tauri-workspace/a-workspace/target"

~/Documents/src-tauri-workspace (master)
$ bash -c 'cd a-workspace/src-tauri && cargo metadata --format-version=1 | jq .target_directory'
"/Users/kofi/Documents/src-tauri-workspace/a-workspace/target"
```
