# Clipwire public pages

Static pages for the platform developer apps: a home page, privacy policy and terms (Google needs them to move the OAuth app to production; TikTok's audit asks for the same). `callback.html` is the https redirect for TikTok login: it only shows the address so you can paste it into `clipwire connect tiktok`. It sends nothing anywhere.

## Before publishing

The contact address on the pages is set. To change it, search and replace it in `index.html`, `privacy.html` and `terms.html`.

## Host on GitHub Pages (free)

1. On github.com, create a **public** repository, for example `clipwire-site`. No "GTA" in the name.
2. Upload `index.html`, `privacy.html`, `terms.html`, `callback.html` and `style.css` to the repository root (Add file → Upload files → Commit).
3. Go to Settings → Pages. Under Source, pick "Deploy from a branch", choose `main` and `/ (root)`, then Save. The site appears within a minute or two at `https://<your-username>.github.io/clipwire-site/`.

## Where each URL goes

| Where | Field | Value |
|---|---|---|
| Google Auth Platform → Branding | App home page | `https://<user>.github.io/clipwire-site/` |
| | Privacy policy | `https://<user>.github.io/clipwire-site/privacy.html` |
| | Terms of service | `https://<user>.github.io/clipwire-site/terms.html` |
| | Authorized domains | `<user>.github.io` |
| TikTok developer app | Terms / privacy URLs | the same two pages |
| TikTok Login Kit | Redirect URI | `https://<user>.github.io/clipwire-site/callback.html` |
| `.env` | `TIKTOK_REDIRECT_URI` | same redirect URI |

After filling in Branding, go back to Audience and click **Publish app**. The YouTube login then stops expiring every 7 days. Reconnect once afterwards (`connect youtube`) to get a token that doesn't expire.

TikTok login asks you to paste a URL, so run it in an interactive terminal (`-it`, not `-T`):

```powershell
docker compose run --rm -it api connect tiktok
```
