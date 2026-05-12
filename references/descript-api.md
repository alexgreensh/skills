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

The Descript API does not currently support local file upload — media must be at a publicly accessible URL. Upload files to your cloud storage service (Dropbox, Google Drive, S3) and get a public URL before calling `import_media`.

**Manual alternative:** Drag and drop files into your Descript project via the desktop app.

## Known limitations

| Limitation | Workaround |
|-----------|-----------|
| **No local file upload via API** | Upload to cloud storage, use public URL; or drag-and-drop into Descript desktop app |
| **No volume ramps / gain envelopes** | Draw manually in Descript desktop app |
| **Agent is one-shot** | Frame each instruction as a complete, self-contained request |
| **composition_id is WIP** | Target by `project_id`, describe composition by name in prompt |
| **No shared media library access** | User manually drags files from library into the project's media panel |
| **Google Drive imports** | Require auth Descript can't satisfy; use Dropbox with `dl=1` links, or upload directly |

These limitations reflect the API as of early 2026. Check [docs.descriptapi.com](https://docs.descriptapi.com/) for the latest.
