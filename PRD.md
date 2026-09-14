# PRD: theprawnredirects

## Overview
A Vercel redirect configuration repo that maps short vanity URLs to their canonical destinations on `www.hong-yi.me`. Used by "The Prawn" brand/collective to provide memorable short links for members and content. Zero code — entirely Vercel-native redirects.

## Goals
- Map short slugs (e.g. `/bryan`, `/bs234`) to full canonical URLs
- Map content paths (e.g. `/photos`, `/blog`) to blog sub-paths
- Map collective member paths to their dedicated pages
- Support both short and long slug variants for each destination

## Non-Goals
- Dynamic redirects (all are static)
- Analytics on redirect clicks
- Custom domain management
- Backend server

## User Stories
- As Bryan, I want to share `theprawnredirects.vercel.app/bryan` and have it redirect to my collective page.
- As a viewer, I want `/photos` to go directly to the photo collection blog post.

## Tech Stack
- **Config**: Vercel `vercel.json` redirects (no code)
- **Deployment**: Vercel

## Architecture
```
theprawnredirects/
└── vercel.json     # all redirect rules
```

## Redirect Map

| Source | Destination |
|--------|-------------|
| `/` | `https://www.hong-yi.me/` |
| `/about`, `/theprawnabout` | `https://www.hong-yi.me/theprawnabout` |
| `/collective`, `/theprawncollective` | `https://www.hong-yi.me/theprawncollective` |
| `/blog`, `/theprawnblog` | `https://www.hong-yi.me/theprawnblog` |
| `/privacy`, `/theprawnprivacy` | `https://www.hong-yi.me/theprawnprivacy` |
| `/my-two-cents` | `https://www.hong-yi.me/blog/my-two-cents` |
| `/video`, `/videos` | `https://www.hong-yi.me/blog/video-showcase` |
| `/photos` | `https://www.hong-yi.me/blog/photo-collection` |
| `/hongyime`, `/bryanseah`, `/bryan`, `/bs234`, `/bs` | `https://www.hong-yi.me/` |
| `/shotsbyseah234`, `/shotsbyseah`, `/sbs`, `/shotbyseah` | `https://www.hong-yi.me/theprawncollective/shotsbyseah234` |
| `/prawnproductions234`, `/prawnproductions`, `/prawnproduction` | `https://www.hong-yi.me/theprawncollective/prawnproductions234` |

All redirects are `permanent: true` (HTTP 308).

## Deployment / Run
Push reviewed configuration changes to `main` and verify the resulting Vercel
deployment. There is no application build or local server. Do not create a second
CLI deployment when Git has already deployed the same commit.

## Constraints & Notes
- **Permanent redirects**: `permanent: true` = HTTP 308; clients may cache these; verify updated destinations with fresh requests after a change
- **Destination domain**: `www.hong-yi.me` is the canonical home site; this repo redirects visitors there and does not proxy page content
- **Maintenance**: add new redirect rules in `vercel.json` and redeploy
- **No fallback**: unmatched routes return Vercel's default 404
