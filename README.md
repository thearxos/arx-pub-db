# arx-pub-db

The **public community registry for arx** — the ArxOS package manager.

This repo is the open, community half of arx. It holds `community.db`: a list of public git
repositories that anyone can install with arx. It is intentionally **public and unofficial** so
the community can contribute freely, the way the AUR works for Arch.

## Two channels, one tool

- **Official tools** — delivered instantly from Cloudflare R2 over TLS and verified by sha256
  (fail-closed) before anything runs. Their source lives in the Stingray Labs repos. You do not
  find these here; arx pulls them from its tools index automatically on `arx update`.
- **Community tools** *(this repo)* — public git repos contributed by anyone. arx builds and
  installs them straight from their source. They are **not vetted or signed by Stingray Labs**.
  Read the code first and install at your own risk. arx still runs its pre-exec guard and scans
  each build/install script before it runs, but that is a safety net, not an endorsement.

## Using it

```sh
arx pub                     # browse the community registry
arx pub search <text>       # find a community repo
arx pub install <name>      # build + install one (from its public git source)
```

## Contributing a repo

1. Fork this repo.
2. Add one line to `community.db`, keeping the fields exact:

   ```
   name | repo_url | category | description | maintainer | verify
   ```

   - **name** — unique, lowercase, `[a-z0-9-]`. Becomes the arx install target.
   - **repo_url** — an `https://` git URL. HTTPS only; ssh/file/http are refused.
   - **category** — one of `tool`, `theme`, `plugin`, `arsenal`, `kernel`, `lib`, `other`.
   - **description** — one short line, no pipe characters.
   - **maintainer** — your GitHub handle. You vouch for and maintain the entry.
   - **verify** — the exact reviewed source revision, written as `commit=<full 40-hex SHA>`.
     Mutable branch tips are rejected during install.

3. Keep the list alphabetical within its section, one repo per line.
4. Open a pull request. Keep the entry honest: describe what the repo actually does.

Entries that misrepresent a repo, point at malware, or break the format are removed.

---
Part of **ArxOS**, by Stingray Labs. The tool is **arx**.
