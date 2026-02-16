# MetaScrape OG Tag Validator

A GitHub Action that validates Open Graph and Twitter Card meta tags on your website using the [MetaScrape API](https://metascrape.shanecode.org).

Catch missing or broken social share previews before they go live.

## Usage

```yaml
name: Validate OG Tags
on:
  push:
    branches: [main]
  pull_request:

jobs:
  og-check:
    runs-on: ubuntu-latest
    steps:
      - uses: shanecode/metascrape-action@v1
        with:
          api-key: ${{ secrets.METASCRAPE_API_KEY }}
          urls: |
            https://yoursite.com
            https://yoursite.com/blog
            https://yoursite.com/pricing
```

## Get a Free API Key

MetaScrape offers 100 free requests/month — more than enough for CI validation.

1. Sign up at [metascrape.shanecode.org/signup](https://metascrape.shanecode.org/signup)
2. Copy your `msk_` API key
3. Add it as a repository secret (`METASCRAPE_API_KEY`)

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `urls` | Newline-separated URLs to validate | **required** |
| `api-key` | MetaScrape API key | **required** |
| `require-og-title` | Fail if `og:title` is missing | `true` |
| `require-og-description` | Fail if `og:description` is missing | `true` |
| `require-og-image` | Fail if `og:image` is missing | `true` |
| `require-twitter-card` | Fail if `twitter:card` is missing | `false` |
| `require-favicon` | Fail if favicon is missing | `false` |

## Outputs

| Output | Description |
|--------|-------------|
| `passed` | `true` if all URLs passed validation |

## Example Output

```
Checking https://yoursite.com
✅ https://yoursite.com — all checks passed
  title:       Your Site - Build Something Great
  og:title:    Your Site - Build Something Great
  og:desc:     The best way to build modern web apps.
  og:image:    https://yoursite.com/og.png
  twitter:     summary_large_image
  favicon:     https://yoursite.com/favicon.ico

Checking https://yoursite.com/blog
⚠️ https://yoursite.com/blog — missing og:image

================================
Results: 1 passed, 1 failed
================================
```

## Why validate OG tags in CI?

- Broken social previews = lost clicks when your content is shared
- Missing `og:image` makes your links look unprofessional on Twitter, Slack, Discord
- Easy to accidentally break meta tags during refactors
- Catch issues before they reach production

## Powered by MetaScrape

This action uses the [MetaScrape API](https://metascrape.shanecode.org) to extract and validate metadata. MetaScrape handles the actual page fetching, JavaScript rendering, and metadata extraction so you get accurate results.

[Get your free API key](https://metascrape.shanecode.org/signup) | [API docs](https://metascrape.shanecode.org/#docs) | [npm package](https://www.npmjs.com/package/@shanecode/metascrape)
