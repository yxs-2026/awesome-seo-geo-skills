# Windows local deployment — 2026-10-31

This branch records a local Windows deployment of six upstream projects. Source licenses and notices remain with each project. Public source forks are preserved separately from machine-specific credentials and runtime data.

| Project | Personal fork | Local status |
| --- | --- | --- |
| Marketing Skills | https://github.com/yxs-2026/marketingskills | Updated to 2.14.0; 53 skills installed |
| Claude SEO | https://github.com/yxs-2026/claude-seo | Updated to 2.5.0; managed runtime and PDF smoke checks passed |
| squirrelscan | https://github.com/yxs-2026/squirrelscan | Stable Windows CLI 0.0.147 installed and one-page passive offline audit and live MCP call passed (15 tools); source main may be ahead of the published binary |
| GEOInflow | https://github.com/yxs-2026/GEOInflow | Source and local startup configuration prepared; production image built and migrations passed; first official demo import is running |
| Elmo | https://github.com/yxs-2026/elmo | Running at http://127.0.0.1:3300; database and HTTP health checks passed; UI-only stub mode |
| Awesome SEO & GEO Skills | https://github.com/yxs-2026/awesome-seo-geo-skills | Source catalog and finder skill installed |

## Source versions

- Marketing Skills: `88c79f6528a9347420e57ceb1fff9a60de651768`.
- Claude SEO: `6be93f45064ffbadced572b5d5c95f55fd263af0`.
- Both forks retain `backup/pre-update-20261031` branches before their fast-forward updates.
- Other forks retain their upstream source history and default visibility.

## Local setup

1. Install Docker Desktop with WSL 2. If a per-user install reports that Virtual Machine Platform is disabled, use an all-users install with administrator approval and follow its restart instructions.
2. The prepared GEOInflow stack uses its upstream compose definition, an isolated PostgreSQL volume and loopback port 3002.
3. The prepared Elmo stack builds its upstream web, migration and worker targets, uses its own PostgreSQL volume and loopback port 3300.
4. Elmo is configured for a UI-only stub environment until a real provider is selected. Its tracking worker is opt-in. Stub outputs are not real AI visibility measurements.
5. Keep generated secrets and database contents local. No generated environment files, access tokens, model keys, customer data or logs are stored in this branch.
6. Verify container health and HTTP responses before marking either application running.

## Skills and compatibility

The updated installation contains 108 user skills in total, including previously installed tools outside these six projects. The three SEO audit entry points remain distinct: `marketing-seo-audit`, `seo-audit`, and `ryze-seo-audit`.

Windows/Codex path adaptations and local launchers are preserved. A local note corrects outdated AI SEO guidance: Google now documents a Generative AI performance report in Search Console. Source skill advice must still be checked against current primary documentation.

- https://support.google.com/webmasters/answer/16984139
- https://developers.google.com/search/docs/fundamentals/ai-optimization-guide

## Windows verification and deployment templates

Docker Desktop 4.97.0, Docker Engine 29.9.2 and WSL 3.0.3 are installed and running. Elmo's health endpoint and initial registration page return HTTP 200. Its source lint check passed on 941 files; an upstream Biome schema-version advisory remains informational.

Clone container projects with `git -c core.autocrlf=false clone URL` so Linux shell scripts and checksum-verified data retain their original bytes. Both local source trees match their Git commits after restoring LF line endings.

Portable templates are in [windows-local](windows-local/): `elmo.compose.yaml`, `elmo.env.example`, and `geoinflow.env.example`. Replace all credential placeholders with separately generated random values, and keep the resulting `.env` files private. Elmo uses `docker compose --env-file .env -f elmo.compose.yaml up --build -d`. GEOInflow uses its original `docker-compose.liekan.yml` with the private environment file. Both applications bind only to loopback. GEOInflow's official example is synthetic; Elmo's tracking worker remains disabled until real providers are configured.
