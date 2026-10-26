# Minecraft Mod Hub — backend starter

This project packages your HTML/CSS website with a Node.js + Express API. Mod data is stored in `data/mods.json` and survives restarts. This is a lightweight starter; for high traffic or multiple server instances, use a real database such as PostgreSQL.

## Requirements
- Node.js 18 or newer
- Internet connection for `npm install`

## Run on Windows
1. Extract the ZIP.
2. Open the extracted `minecraft-mod-hub-backend` folder in VS Code.
3. Open Terminal and run:
   ```bash
   npm install
   ```
4. Set an admin token in PowerShell (choose your own long random value):
   ```powershell
   $env:ADMIN_TOKEN="replace-with-a-long-random-secret"
   ```
5. Start the server:
   ```bash
   npm start
   ```
6. Visit `http://localhost:3000`.

## API routes
- `GET /api/health` — health check
- `GET /api/mods` — list all mods
- `GET /api/mods?q=fps` — search mods
- `GET /api/mods?category=survival` — filter by category (case-insensitive)
- `GET /api/mods/:id` — get one mod
- `GET /api/mods/:id/download` — increments the download-request count, then redirects to its configured URL
- `POST /api/admin/mods` — add a mod (requires `x-admin-token`)
- `PATCH /api/admin/mods/:id` — update a mod (requires `x-admin-token`)
- `DELETE /api/admin/mods/:id` — delete a mod (requires `x-admin-token`)

Example admin request:
```bash
curl -X POST http://localhost:3000/api/admin/mods ^
  -H "Content-Type: application/json" ^
  -H "x-admin-token: replace-with-a-long-random-secret" ^
  -d "{\"id\":\"my-addon\",\"name\":\"My Add-on\",\"category\":\"Survival\",\"version\":\"1.0\",\"description\":\"A sample addon\",\"downloadUrl\":\"https://mcpedl.com/\"}"
```

## Important notes
- The original HTML linked to files using `file:///C:/...`, which only works on the creator's computer. Those links have been changed to backend routes.
- Seed download URLs point to official Minecraft or MCPEDL landing pages as safe placeholders. They are not direct downloads of the specific mods. Update `data/mods.json` with direct URLs only when you have permission to distribute/link to those files.
- This starter does not upload files, handle user accounts, or provide a full admin dashboard.
- Before public deployment: use HTTPS, set a strong `ADMIN_TOKEN` in the host's environment, back up `data/mods.json`, and consider rate limiting and a production database.
