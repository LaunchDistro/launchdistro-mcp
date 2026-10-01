# LaunchDistro MCP

LaunchDistro is a hosted MCP server that plans a product's startup-directory submissions and checks that the links went live. Your own AI app (Claude Code, Claude Desktop, Cursor, Codex, VS Code, ...) fills each directory's form in **your own browser**; LaunchDistro supplies the verified catalog, the order to submit in, the playbook for each form and the live-link check.

This repository holds documentation and the registry manifest only. The server runs at `https://launchdistro.com/api/mcp`.

- Site: https://launchdistro.com
- Full docs: https://launchdistro.com/docs
- Tools reference: https://launchdistro.com/docs/tools

## What it does

1. **Match**: which directories take your product (type, region, badge rules, requirements), with the reason for each one that does not.
2. **Plan**: the order to submit in and a daily pace for your domain's rating, each directory with a reason for its place.
3. **Playbook**: before each directory, what its form asks, which profile field goes where, the free plan's conditions and where to stop for you.
4. **Record**: what happened at each directory, on your dashboard.
5. **Verify**: opens the public listing, checks that it links to your product and reads the link's `rel` (dofollow or nofollow). A listing counts as live only after this check.

## Connect

Create a token for your AI app on https://launchdistro.com/dashboard/setup (one token per app, revocable on its own). Then:

**Claude Code**

```bash
claude mcp add --scope user --transport http launchdistro https://launchdistro.com/api/mcp --header "Authorization: Bearer <your-token>"
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "launchdistro": {
      "url": "https://launchdistro.com/api/mcp",
      "headers": { "Authorization": "Bearer <your-token>" }
    }
  }
}
```

**Codex** (`~/.codex/config.toml`)

```toml
[mcp_servers.launchdistro]
url = "https://launchdistro.com/api/mcp"
http_headers = { Authorization = "Bearer <your-token>" }
```

**VS Code**

```bash
code --add-mcp '{"name":"launchdistro","type":"http","url":"https://launchdistro.com/api/mcp","headers":{"Authorization":"Bearer <your-token>"}}'
```

**Claude Desktop**: Customize, Connectors, **+**, Add custom connector. Name it LaunchDistro and paste `https://launchdistro.com/api/mcp?token=<your-token>`.

**Any other app**: add a remote (Streamable HTTP) server with the URL above and the header `Authorization: Bearer <your-token>`.

Step-by-step setup and troubleshooting: https://launchdistro.com/docs/setup

## Tools

| Group | Tool | What it does |
| --- | --- | --- |
| Plan | `match_directories` | Every catalogued directory for the product: ready, locked or not a fit, with the reason |
| Plan | `plan_submissions` | Orders the ready directories and saves the plan; submits nothing |
| Product profile | `list_products` | The products on your account |
| Product profile | `get_product_profile` | The product's facts and the fields directories ask that are still empty |
| Product profile | `save_product_profile` | Saves facts you confirmed, merged onto the stored profile |
| Submit | `submission_playbook` | How to submit to one directory; call it before every submission |
| Submit | `record_submission` | Records what happened at a directory, with the confirmation page as proof |
| Check and report | `verify_link` | Opens a public listing and checks the link and its `rel` |
| Check and report | `verify_badge` | Checks that your site shows the badge or link back a directory asks for |
| Check and report | `list_submissions` | What you have sent and what is waiting on you |
| Check and report | `report_directory_fact` | Tells LaunchDistro what a directory's page says that its playbook did not |
| Check and report | `suggest_directory` | Suggests a directory LaunchDistro does not list |
| Account | `license_status` | Plan, free submissions left and connected apps |

It also registers one prompt, `submit`, which runs the whole flow for one directory. Parameters and return values: https://launchdistro.com/docs/tools

## Try it

Once connected, ask your AI app:

- "Add my product from this repo, and ask me what you can't find."
- "Where does my product qualify?"
- "Plan my next 10 directories, dofollow first."
- "Submit my product to the next directory on the plan."
- "What have I sent, and what is waiting on me?"

## Privacy and what runs where

- Forms are filled by your AI app in your own browser, with your own sessions. Nothing is submitted from LaunchDistro's servers.
- Your agent stops and asks you at every sign-in, CAPTCHA, code, payment, terms checkbox or ambiguous field.
- LaunchDistro's server opens public pages itself only for `verify_link` and `verify_badge`.
- Passwords and payment details never go to LaunchDistro.
- What is stored and for how long: https://launchdistro.com/privacy

## Plans

A free plan with 10 submissions, a one-off Launch for one product, and Pro for every product and weekly link monitoring. Current prices and limits: https://launchdistro.com/pricing

## Support

Questions and problems: https://launchdistro.com
