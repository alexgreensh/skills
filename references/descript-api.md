# Descript API Reference

Shared reference for all Descript-integrated skills. Loaded when a workflow needs API interaction.

## API documentation

**Source of truth:** [docs.descriptapi.com](https://docs.descriptapi.com/)

The Descript API is early access and actively evolving. If anything in a skill conflicts with the current docs, the docs win.

## Authentication

1. Go to Descript Settings → API tokens
2. Click "Create token," name it, and associate it with a Drive
3. Copy and store it securely — tokens can't be recovered after creation
4. Token permissions are scoped to the Drive it was created under

**Pattern:** Skills describe what to do and when; your MCP connection (or API client) handles the actual calls.

**Without MCP configured:** Every API step can be done manually through the Descript app instead.

## Job polling

All Descript API operations are asynchronous. After every `prompt_project_agent` or `import_media` call, poll `GET /jobs/{job_id}` (via `get_job`) until `job_state` is `"stopped"` and check `result.status` for `"success"` or `"error"` before proceeding.

Use a `callback_url` if you want a webhook instead of polling.

## Media import

Two ways to get media into a project via the API:

**URL import:** Pass a public or pre-signed URL in the `url` field. Descript fetches it server-side.

**Direct file upload:** Pass `content_type` (MIME type) and `file_size` (bytes) instead of `url`. The response includes a signed `upload_url` (valid 3 hours). PUT the raw file bytes to that URL with `Content-Type: application/octet-stream`. The import job detects the upload and begins processing automatically.

You can mix both methods in a single `import_media` request. Items with `url` are fetched server-side; items with `content_type` and `file_size` return signed upload URLs.

**Direct upload flow:**
1. Call `import_media` with `content_type` and `file_size` for each file
2. PUT file bytes to each signed `upload_url` from the response
3. Poll `get_job` until complete (same as URL imports)

**Manual alternative:** Drag and drop files into your Descript project via the desktop app.

## Known limitations

| Limitation | Workaround |
|-----------|-----------|
| **No volume ramps / gain envelopes** | Draw manually in Descript desktop app |
| **Agent is one-shot** | Frame each instruction as a complete, self-contained request |
| **composition_id is WIP** | Target by `project_id`, describe composition by name in prompt |
| **No shared media library access** | User manually drags files from library into the project's media panel |
| **Google Drive imports** | Require auth Descript can't satisfy; use Dropbox with `dl=1` links, or upload directly |

These limitations reflect the API as of early 2026. Check [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest.
