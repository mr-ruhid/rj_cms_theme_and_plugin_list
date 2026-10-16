# RJ CMS Theme and Plugin Registry

The official community registry for **RJ CMS** themes and plugins.

This repository is a **directory**, not a hosting service. Every package lives in its own GitHub repository, and RJ CMS reads this registry to discover what is available.

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [How to Submit](#how-to-submit)
- [Registry Format](#registry-format)
- [How Updates Work](#how-updates-work)
- [Manifest Requirements](#manifest-requirements)
- [Release Asset Requirements](#release-asset-requirements)
- [Verification Levels](#verification-levels)
- [Removal Policy](#removal-policy)
- [License](#license)
- [Links](#links)

---

## Overview

RJ CMS uses this registry to power the **Add New Theme** and **Add New Plugin** admin pages. When a user clicks **Browse Community**, RJ CMS does the following:

1. Fetches `registry.json` from this repository.
2. Reads each entry's GitHub repository.
3. Queries `releases/latest` through the GitHub API.
4. Displays the name, version, description, author and an install button.

No packages are stored here. The registry only contains a list of approved repositories.

---

## Repository Structure

```text
.
├── registry.json          Master list of themes and plugins
├── schema/                JSON validation schemas
├── CONTRIBUTING.md        How to submit your theme or plugin
└── .github/workflows/     Automatic validation on pull requests
```

---

## How to Submit

The full instructions are in [CONTRIBUTING.md](CONTRIBUTING.md). The short version:

1. Fork this repository.
2. Add your entry to `registry.json`.
3. Open a pull request.
4. Wait for a maintainer review.

Your package must:

- Live in a **public GitHub repository**.
- Include a valid `theme.json` or `plugin.json` at the repository root.
- Publish at least one **GitHub Release** with a ZIP asset.
- Use an open-source license such as MIT, GPL or Apache.

---

## Registry Format

```json
{
    "version": "1.0",
    "updated_at": "2026-10-17T00:00:00Z",
    "themes": [
        {
            "repo": "owner/repo",
            "verified": true,
            "featured": false,
            "category": "general",
            "tags": ["minimal", "blog"]
        }
    ],
    "plugins": [
        {
            "repo": "owner/repo",
            "verified": true,
            "featured": false,
            "category": "seo",
            "tags": ["seo", "analytics"]
        }
    ]
}
```

### Field Reference

| Field      | Type    | Required | Description                                          |
|------------|---------|----------|------------------------------------------------------|
| `repo`     | string  | Yes      | GitHub repository in `owner/repo` format             |
| `verified` | boolean | Yes      | Set by maintainers after review                      |
| `featured` | boolean | No       | Shown on the browse page (maintainers only)          |
| `category` | string  | No       | Primary category, see the list below                 |
| `tags`     | array   | No       | Search keywords                                      |

### Categories

**Themes:** `general`, `blog`, `magazine`, `portfolio`, `shop`, `business`, `landing`, `photography`

**Plugins:** `seo`, `analytics`, `forms`, `ecommerce`, `social`, `security`, `performance`, `marketing`, `utilities`

---

## How Updates Work

Once your package is listed, you do not need to touch this repository when you ship a new version.

1. Publish a new release on GitHub.
2. RJ CMS queries `releases/latest` automatically.
3. Users see **Update available** in their admin panel.

The registry only changes when:

- A package is added or removed.
- A package's `verified` or `featured` status changes.
- Its category or tags are updated.

---

## Manifest Requirements

### Themes (`theme.json`)

```json
{
    "name": "Theme Name",
    "slug": "theme-slug",
    "version": "1.0.0",
    "author": "Your Name",
    "description": "Short description",
    "requires": {
        "rj_cms": ">=1.0.0",
        "php": ">=8.2"
    }
}
```

### Plugins (`plugin.json`)

```json
{
    "name": "Plugin Name",
    "slug": "plugin-slug",
    "version": "1.0.0",
    "author": "Your Name",
    "description": "Short description",
    "requires": {
        "rj_cms": ">=1.0.0",
        "php": ">=8.2"
    }
}
```

---

## Release Asset Requirements

Each GitHub Release must include a ZIP file containing your theme or plugin.

- **Theme ZIP:** must contain `theme.json` at the root, or one level deep.
- **Plugin ZIP:** must contain `plugin.json` at the root, or one level deep.
- **Maximum size:** 50 MB.

RJ CMS downloads the first ZIP asset it finds in the release.

---

## Verification Levels

| Level          | Meaning                                                                                          |
|----------------|--------------------------------------------------------------------------------------------------|
| **Verified**   | Manifest is valid, repository is public, at least one release exists, and the code was reviewed. |
| **Community**  | Manifest is valid and repository is public, but the code has not been reviewed yet.              |
| **Unverified** | Listed but not reviewed. This is a temporary status.                                             |

Only maintainers can set `verified: true`.

---

## Removal Policy

A package may be removed from the registry if:

- Its repository is deleted or made private.
- It violates the license requirement.
- It contains malicious code.
- The author requests removal.

---

## License

This registry is licensed under the MIT License. Individual packages are covered by their own licenses.

---

## Links

- **RJ CMS:** [github.com/mr-ruhid/rj-cms-ai](https://github.com/mr-ruhid/rj-cms-ai)
- **Issues:** [github.com/mr-ruhid/rj_cms_theme_and_plugin_list/issues](https://github.com/mr-ruhid/rj_cms_theme_and_plugin_list/issues)