# Contributing to the RJ CMS Registry

Thank you for contributing to the RJ CMS ecosystem. This document explains how to submit your theme or plugin to the official registry.

---

## Table of Contents

- [Before You Submit](#before-you-submit)
- [Step 1: Prepare Your GitHub Repository](#step-1-prepare-your-github-repository)
- [Step 2: Create a GitHub Release](#step-2-create-a-github-release)
- [Step 3: Fork and Edit the Registry](#step-3-fork-and-edit-the-registry)
- [Step 4: Update updated_at](#step-4-update-updated_at)
- [Step 5: Open a Pull Request](#step-5-open-a-pull-request)
- [Review Process](#review-process)
- [After Approval](#after-approval)
- [Changing Metadata](#changing-metadata)
- [Removal](#removal)
- [Code of Conduct](#code-of-conduct)
- [Questions](#questions)

---

## Before You Submit

Make sure you have:

- [ ] A **public GitHub repository** with your theme or plugin
- [ ] A valid `theme.json` or `plugin.json` at the repository root
- [ ] At least **one published GitHub Release** with a ZIP asset
- [ ] An **open-source license** (MIT, GPL, Apache, BSD, etc.)
- [ ] A working `README.md` in your repository

If any of these are missing, your pull request will be closed.

---

## Step 1: Prepare Your GitHub Repository

### Theme repository

```text
your-theme/
├── theme.json
├── README.md
├── LICENSE
├── screenshot.png
├── views/
│   ├── layout.blade.php
│   ├── single-post.blade.php
│   ├── single-page.blade.php
│   └── archive.blade.php
└── assets/
    ├── css/
    └── js/
```

### Plugin repository

```text
your-plugin/
├── plugin.json
├── README.md
├── LICENSE
├── src/
│   └── Plugin.php
└── assets/
```

### `theme.json` example

```json
{
    "name": "Your Theme Name",
    "slug": "your-theme-slug",
    "version": "1.0.0",
    "author": "Your Name",
    "author_url": "https://example.com",
    "description": "A short description of your theme.",
    "requires": {
        "rj_cms": ">=1.0.0",
        "php": ">=8.2"
    },
    "supports": {
        "builder_header": true,
        "builder_footer": true,
        "builder_page": true
    }
}
```

### `plugin.json` example

```json
{
    "name": "Your Plugin Name",
    "slug": "your-plugin-slug",
    "version": "1.0.0",
    "author": "Your Name",
    "author_url": "https://example.com",
    "description": "A short description of your plugin.",
    "requires": {
        "rj_cms": ">=1.0.0",
        "php": ">=8.2"
    },
    "hooks": {
        "activate": "YourVendor\\YourPlugin\\Plugin::activate",
        "deactivate": "YourVendor\\YourPlugin\\Plugin::deactivate"
    }
}
```

> The `slug` field must be unique. Matching your repository name is recommended, but not required.

---

## Step 2: Create a GitHub Release

1. Go to your repository on GitHub.
2. Click **Releases**, then **Draft a new release**.
3. Create a tag such as `v1.0.0`. It must match the version in your manifest.
4. Set the title, for example `Your Theme 1.0.0`.
5. Describe what changed in this version.
6. Attach a ZIP file containing your theme or plugin.
7. Click **Publish release**.

### ZIP requirements

- Must contain your manifest (`theme.json` or `plugin.json`) at the root or one level deep.
- Must be under 50 MB.
- The filename is flexible (`theme.zip`, `your-theme-1.0.0.zip`, etc.).

### Accepted ZIP structures

Wrapped in a single folder:

```text
your-theme.zip
└── your-theme/
    ├── theme.json
    ├── views/
    └── assets/
```

Flat:

```text
your-theme.zip
├── theme.json
├── views/
└── assets/
```

### Rejected ZIP structure

Anything nested deeper than one level will be rejected:

```text
your-theme.zip
└── src/
    └── your-theme/
        └── theme.json
```

---

## Step 3: Fork and Edit the Registry

1. Fork [mr-ruhid/rj_cms_theme_and_plugin_list](https://github.com/mr-ruhid/rj_cms_theme_and_plugin_list).
2. Open `registry.json`.
3. Add your entry alphabetically to the `themes` or `plugins` array.

### Theme entry example

```json
{
    "repo": "your-username/your-theme",
    "verified": false,
    "featured": false,
    "category": "blog",
    "tags": ["minimal", "responsive"]
}
```

### Plugin entry example

```json
{
    "repo": "your-username/your-plugin",
    "verified": false,
    "featured": false,
    "category": "seo",
    "tags": ["meta", "sitemap"]
}
```

> **Important:** Always submit with `"verified": false` and `"featured": false`. Maintainers set these after review.

### Allowed categories

**Themes:** `general`, `blog`, `magazine`, `portfolio`, `shop`, `business`, `landing`, `photography`

**Plugins:** `seo`, `analytics`, `forms`, `ecommerce`, `social`, `security`, `performance`, `marketing`, `utilities`

If your package does not fit any category, use `general` for themes or `utilities` for plugins.

---

## Step 4: Update updated_at

Change the `updated_at` field to the current UTC timestamp:

```json
"updated_at": "2026-10-17T14:30:00Z"
```

Format: `YYYY-MM-DDTHH:MM:SSZ`

---

## Step 5: Open a Pull Request

1. Commit your changes with a clear message:

   ```text
   Add theme: Your Theme Name
   ```

   or

   ```text
   Add plugin: Your Plugin Name
   ```

2. Push to your fork.
3. Open a pull request against `main`.
4. Fill in the PR template:
   - Package name
   - Repository URL
   - Short description
   - Link to the latest release
   - License type

---

## Review Process

### Automatic validation

When your PR is opened, the following checks run:

- [ ] `registry.json` is valid JSON
- [ ] Schema validation passes
- [ ] Your repository is public and accessible
- [ ] Your repository has a valid manifest
- [ ] Your repository has at least one release with a ZIP

### Manual review

If validation passes, a maintainer reviews the package:

- [ ] Code quality is reasonable
- [ ] No malicious code
- [ ] README is present
- [ ] License file is present
- [ ] Screenshot is present (themes only)

Typical review time is **1 to 7 days**.

If everything checks out, your package gets `"verified": true` and appears in the RJ CMS admin panel.

---

## After Approval

Once your package is in the registry, you do not need to open new PRs for new versions. Just publish a new GitHub Release:

1. Update `version` in `theme.json` or `plugin.json`.
2. Commit the change.
3. Create a new release (tag `v1.1.0`, etc.).
4. Attach the new ZIP.

RJ CMS detects the update within 12 hours, or immediately when the user clicks **Check for updates**.

---

## Changing Metadata

Open a new PR if you need to:

- Change the category or tags
- Update the repository URL (for example, moved from a personal account to an organization)
- Request removal

---

## Removal

To remove your package, open a PR that deletes your entry from `registry.json` and mention the reason in the description.

Maintainers may also remove packages that:

- Have deleted or private repositories
- Contain malicious code
- Violate the license requirement
- Have been inactive for more than 2 years

---

## Code of Conduct

- Be respectful.
- No spam or self-promotion without a real product.
- No packages that exist only to collect user data.
- No obfuscated code.
- No paid-only packages. Freemium is fine if the base version is free.

---

## Questions

- Open an issue: [github.com/mr-ruhid/rj_cms_theme_and_plugin_list/issues](https://github.com/mr-ruhid/rj_cms_theme_and_plugin_list/issues)
- Start a discussion using GitHub Discussions

---

## Thank You

Every contribution makes RJ CMS better for everyone. We appreciate your time and effort.