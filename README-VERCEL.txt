LOW POLY DRIFT SERVER - VERCEL ADAPTATION

Deploy this folder as a separate Vercel project (do not replace the website project).
The project uses the Vercel Function catch-all at api/[...path].js and routes all paths
through the original HTTP server. The WebSocket server is attached to the exported
HTTP server. Region is set to Sydney (syd1).

IMPORTANT LIMITATIONS
- This is a first-pass Vercel adaptation, not a guarantee of full multiplayer parity.
- Vercel Functions can accept WebSockets, but each connection is pinned to one function
  instance only for that invocation's lifetime. Connections can close at maxDuration.
- Room state is currently held in in-memory Maps. Different function instances do not
  share those Maps. Players assigned to different instances may not see the same rooms.
  For reliable multi-instance multiplayer, the room/player state and cross-instance
  broadcasts must be moved to a shared service such as Redis.
- gifts-used.json is written to the deployment filesystem in the original code. Vercel
  deployment files are not persistent writable storage; single-use gift tracking needs
  a database/Redis before relying on it in production.
- The Vercel Hobby plan's actual maxDuration and usage quotas may be lower than this
  project setting; Vercel enforces the plan limit.

ENVIRONMENT VARIABLES TO CONFIGURE IN VERCEL
REGION=Sydney, AU
ADMIN_PASSWORD= choose a strong password
GIFT_SECRET= choose a long random secret

Do not change your existing Render deployments. Test this as a separate Vercel project.
