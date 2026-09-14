# The Prawn Redirects

Twenty-five fixed short links, served by Vercel's native redirects. The entire
application configuration is [vercel.json](vercel.json); there is no dependency
installation, build command or application server.

## Use a short link

- [go.hong-yi.me/bryan](https://go.hong-yi.me/bryan) opens the public homepage.
- [go.hong-yi.me/photos](https://go.hong-yi.me/photos) opens the photo collection.
- [go.hong-yi.me/blog](https://go.hong-yi.me/blog) opens the blog.

The same paths work on `at.hong-yi.me`, `visit.hong-yi.me`,
`theprawnredirects.hong-yi.me` and `theprawnredirects.vercel.app`.
See the complete grouped route map in [PRD.md](PRD.md).

## Change and verify a destination

1. Edit the matching rule in `vercel.json`. Keep existing short paths when a page moves.
2. Confirm the target page exists and use its final HTTPS URL to avoid redirect chains.
3. Review the diff and validate JSON with `python -m json.tool vercel.json` if Python is available.
4. Push the reviewed change to `main`; the linked Vercel project deploys automatically.
5. Check the new deployment's commit and the public redirect's status and `Location` header.

For example, `curl -I https://go.hong-yi.me/bryan` should return HTTP 308 and
`Location: https://www.hong-yi.me/`.
In Windows PowerShell, use `curl.exe` to invoke curl explicitly. Also open the
destination and confirm its content, because a valid redirect can lead to a missing page.

## Behavior and hosting

All rules use `permanent: true` (HTTP 308). Unmatched paths return 404; this is a
fixed alias map, not a general URL shortener. There are no application records,
Supabase calls, background jobs or click analytics. Destination pages are managed
separately on `www.hong-yi.me`; this repository sends visitors there.

The September 2026 maintenance pass preserves all 25 short paths, repairs five
profile aliases by directing them to the public homepage and removes the former intermediate non-www hop. It does not
establish monthly Vercel bandwidth or billing savings.

Reference: [Vercel configuration redirects](https://vercel.com/docs/routing/redirects/configuration-redirects).

## License

Apache-2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
