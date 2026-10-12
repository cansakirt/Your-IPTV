# Your IPTV

A Stremio add-on that connects your IPTV subscription to the Stremio media interface. It supports both M3U playlist URLs and Xtream API credentials, exposing movies, series, and live TV categories as catalog entries inside Stremio.

## Features

- Browse IPTV movies, series, and live channels in Stremio
- Works with either:
  - an M3U playlist URL
  - an Xtream API base URL + username + password
- Automatically discovers categories from the provider API
- Includes a config page for generating a Stremio install URL
- Lightweight Node.js server for serving Stremio-compatible API endpoints
- Deployment-ready with Docker and Procfile-based hosting

## Supported Use Cases

This project is intended for users who already have a valid IPTV subscription and want to access it through Stremio.

Important: free or public M3U lists are not supported by design.

## Project Structure

- `index.js` — Express server that exposes the Stremio endpoints
- `addon.js` — core logic for authenticating and querying IPTV APIs
- `manifest.js` — add-on manifest metadata
- `configure.html` — configuration page used to generate the install URL
- `config.js` — runtime environment settings
- `Dockerfile` / `Procfile` — deployment helpers

## Requirements

- Node.js 18+
- An active IPTV subscription with either:
  - an M3U URL, or
  - Xtream API credentials
- Stremio installed on your device

## Installation

1. Clone the repository:

```bash
git clone https://github.com/gorlev/Your-IPTV.git
cd Your-IPTV
```

2. Install dependencies:

```bash
npm install
```

3. Start the add-on locally:

```bash
npm start
```

4. Open the configuration page:

```text
http://localhost:3649/configure
```

The app listens on port `3649` by default in local mode.

## Configuration

From the configuration page, you can choose between two methods:

### 1) M3U URL

Provide your IPTV playlist URL. The app parses the base URL and credentials to build the Stremio configuration link.

### 2) Xtream API

Provide:

- Base URL (for example `http://your-provider.example.com:80`)
- Username
- Password

The generated install link can then be opened in Stremio to add the add-on.

## Local Run Behavior

The project uses `config.js` to switch between local and hosted environments:

- local mode: `http://127.0.0.1:3649`
- hosted mode: uses environment port/host values

## Deployment

The repository includes a `Dockerfile` and a `Procfile`, so it can be deployed to container-based or process-based hosting providers.

Typical flow:

```bash
npm install
npm start
```

If deploying to a platform using `PORT`, ensure the environment variable is configured and the generated Stremio URLs match your public domain.

## Notes

- This project communicates with IPTV provider endpoints such as `player_api.php`
- It is designed to work with the Stremio add-on API
- The generated Stremio manifest can be used as an installable add-on URL

## License

This project uses the ISC license as defined in `package.json`.

## Disclaimer

This project does not provide IPTV content or subscriptions. You must provide your own valid IPTV service credentials or playlist.

## Repository URL

https://github.com/gorlev/Your-IPTV
