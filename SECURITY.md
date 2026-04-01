# Security Notes (JonesHong fork)

## Pinned Versions
- `camoufox[geoip]==0.4.11` (pinned in pyproject.toml)
- Firefox binary: v135.0.1-beta.24

## Known-Good Binary Hash
```
SHA256: 43805f5cbf01d9a2803ac0641926c09754a47aad8caeb3b6b143aeb0bff054a1
File:   ~/Library/Caches/camoufox/Camoufox.app/Contents/MacOS/camoufox
```

## Fork Changes from upstream (Bin-Huang/camoufox-cli)
1. `server.py`: Unix socket `os.chmod(self.socket_path, 0o700)` — owner-only access
2. `pyproject.toml`: Pin camoufox==0.4.11, update URLs to JonesHong fork

## Update SOP
1. `git fetch upstream && git diff main..upstream/main -- src/`
2. Review: server.py (socket), browser.py (launch), pyproject.toml (deps)
3. `git merge upstream/main` → resolve conflicts → test Perplexity + Grok
4. `uv tool install git+https://github.com/JonesHong/camoufox-cli.git --force`
5. After `camoufox-cli install`: verify binary hash matches known-good

## Verify Binary Integrity
```bash
shasum -a 256 ~/Library/Caches/camoufox/Camoufox.app/Contents/MacOS/camoufox
# Should match known-good hash above (unless intentionally upgraded)
```
