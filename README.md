<h1 align="center">Orca s3dev Plugins</h1>

<p align="center">
  <img src="https://img.shields.io/badge/plugins-1-08C?style=flat" alt="1 plugin in the index" />
  <img src="https://img.shields.io/badge/Orca-%E2%89%A5%201.4.0-4493F8?style=flat" alt="Requires Orca 1.4.0 or newer" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-08C?style=flat" alt="MIT License" /></a>
</p>

<p align="center">
  <sub><a href="docs/readme/README.ru.md">Русский</a></sub>
</p>

<p align="center">
  <strong>A plugin marketplace index for <a href="https://github.com/stablyai/orca">Orca</a>.</strong><br/>
  Add this repository as a marketplace source and install the plugins listed below from inside Orca.
</p>

---

## Add this marketplace to Orca

1. **Settings** → **Plugins** → enable the plugin system.
2. Open **Marketplace sources**.
3. Paste the URL into **Git URL**, keep the ref as `main`, and click **Add source**:

   ```
   https://github.com/smwbev/orca-plugins.git
   ```

4. The index appears under **Configured sources** as **Orca s3dev Plugins**, pinned at the exact commit it fetched.
5. Open the **All** tab, find the plugin you want, and click **Install**.

Orca reuses your system Git credentials, so private repositories work the same way.

> **Not the same as “Install plugin”.** This URL belongs in **Manage sources**, not in the **Install plugin** dialog — a marketplace index is not a plugin and cannot be installed as one. Pasting it there fails with *“Add an explicit #ref …”*, because that dialog expects a plugin repository pinned to a tag, for example `https://github.com/smwbev/orca-russian.git#v5.1.1`.

### Refreshing and removing

- The refresh icon next to the source re-fetches the index and re-pins it to the newest commit.
- The trash icon removes the source. Plugins installed from it stay installed until you remove them separately.

---

## What's in the index

| Plugin | ID | Category | Description |
|---|---|---|---|
| [Русский](https://github.com/smwbev/orca-russian) | `smwbev.russian` | `languages` | A complete Russian translation of the Orca interface — 11,721 strings, 98.2 % of the catalog |

Every entry pins an exact release tag rather than a moving branch, so an install always resolves to reviewed content. When a plugin ships a new version, the `ref` in [`orca-marketplace.json`](orca-marketplace.json) is bumped and Orca offers the update after the next refresh.

---

## Index format

```jsonc
{
  "name": "Orca s3dev Plugins",   // shown in Orca's source list
  "owner": "smwbev",              // must match the account that hosts the index
  "plugins": [
    {
      "id": "smwbev.russian",     // publisher.id — must equal the plugin manifest identity
      "source": {
        "kind": "git",
        "url": "https://github.com/smwbev/orca-russian.git",
        "ref": "v5.1.1"           // tag, branch, or commit
      },
      "description": "…",
      "categories": ["languages"]
    }
  ]
}
```

Two rules are worth knowing before adding an entry:

- **`id` must match the plugin's own manifest.** Orca compares the marketplace id against `publisher` + `id` in `orca-plugin.json` and refuses the install on mismatch.
- **Reserved identities.** A publisher of `stablyai`, or any id starting with `orca-`, is reserved for the official marketplace. If such an entry does not resolve to the stablyai organization, Orca rejects **the whole index**, not just that entry — every plugin from this source stops being installable.

Note that Orca currently hides listings categorised as `themes`, `icons`, `icon-themes`, `terminal-themes`, or `skills`, because installing them leads to a dead end. `languages` and other categories display normally.

---

## License

The index in this repository is released under the [MIT License](LICENSE).

Each listed plugin is a separate project with its own license — see its repository. See [NOTICE](NOTICE) for attribution details.
