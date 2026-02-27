# Deployment Rules

## Tier 1 — Static Apps (S3)
- HTML/CSS/JS only apps are deployed to AWS S3 static hosting.
- Build output goes to dist/ or build/ directory.
- No server-side code.

## Tier 2 — Server Apps (PM2 + nginx)
- Node.js or other server apps run via PM2.
- Served at /apps/<projectId>/ via nginx reverse proxy.
- App must listen on the assigned PORT environment variable.

## CRITICAL: URL Rules
- NEVER hardcode localhost or 127.0.0.1 in client-facing code.
- Browsers: use window.location.origin or relative paths for API calls.
- Servers: bind to 0.0.0.0 (not localhost) so nginx can proxy to the process.
- WebSocket: use wss:// with window.location.host, not ws://localhost.

## Port Assignment
- The PORT env var is set by the deployment system. Always use process.env.PORT.