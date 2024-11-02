# Resolving the VSCode Rust Workspace Error

VSCode may not index and provide intellisense to crates like `scipio-airtable`, `scipio-workspace`, `scipio-macros`, `scipio-sendgrid` etc. This is because VSCode is not configured properly. You can resolve this by doing the following:

<br/>

Create a file called `.vscode/settings.json` in the root of the project. Then, paste the following in (make sure to change /path/to/scipio to the path to your cloned directory).

```json
{
  "rust-analyzer.linkedProjects": ["/path/to/scipio/Cargo.toml"],
  "rust.analyzer.cargo.loadOutDirsFromCheck": true,
  "rust-analyzer.cargo.allFeatures": true
}
```

If you still have errors, you can try to make VSCode use a separate instance of `rust-analyzer` instead of the bundled version. To do this, run the following command `rustup component add rust-analyzer`. Then, in your `settings.json`, add another line:

```json
{
  "rust-analyzer.linkedProjects": ["/path/to/scipio/Cargo.toml"],
  "rust.analyzer.cargo.loadOutDirsFromCheck": true,
  "rust-analyzer.cargo.allFeatures": true
}
```

```diff
{
  "rust-analyzer.linkedProjects": ["/path/to/scipio/Cargo.toml"],
  "rust.analyzer.cargo.loadOutDirsFromCheck": true,
  "rust-analyzer.cargo.allFeatures": true,
  + "rust-analyzer.server.path": "/path/to/your/rust/analyzer"
}
```

To find the path to the rust analyzer you are using, you can run the following command: `which rust-analyzer`.
