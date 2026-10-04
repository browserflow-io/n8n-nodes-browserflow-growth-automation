# Browserflow for Growth Automation

Bring browser automation into your n8n workflows. Scrape leads, enrich company
information, monitor products and prices, collect reports, and automate repetitive
website tasks with [Browserflow](https://browserflow.io/home).

Build your own browser flow with AI, test it, and publish it in Browserflow.
Then run it from n8n with new inputs and use the results in your next steps.
Connect the work you do in your browser to your CRM, spreadsheets, databases,
and other apps through n8n.

## What you can build

- **Lead research and enrichment:** collect company and contact details, then add
  them to your lead list or update a CRM record.
- **Product and market monitoring:** gather product names, prices, availability,
  and competitor information for comparisons or alerts.
- **Sales and data entry:** use data from earlier n8n steps to fill forms, update
  records, and carry out the website actions you recorded.
- **Finance and operations:** collect invoice details, reports, and records from
  vendor portals and pass them to your business tools.
- **Content and research:** collect articles, track metrics, and gather information
  for summaries, reports, or publishing workflows.

You choose the websites, steps, inputs, and results when building your flow.
Start from your own task or clone a community flow from the
[Browserflow marketplace](https://browserflow.io/marketplace).
For signed-in tasks, save a login profile in Browserflow and attach it to your flow.
Normal runs follow your saved steps without AI deciding each action; optional
AI repair can help when a page changes.

## Before you start

You need a Browserflow account with subscription access and a successfully tested,
published flow. Create and edit flows in Browserflow; this node runs them from n8n.
Browserflow and n8n plans and usage costs are separate.

This package is available for self-hosted n8n with community nodes enabled.
n8n verification is pending, so it is not yet available as a verified node in
n8n Cloud. It has been tested with n8n 2.39.8.

## Install

In self-hosted n8n, open **Settings → Community Nodes → Install** and enter:

```text
@browserflow/n8n-nodes-browserflow-growth-automation
```

Follow the [n8n community node installation guide](https://docs.n8n.io/integrations/community-nodes/installation/gui-install/).
The node appears as **Browserflow for Growth Automation**.

## Credentials

1. Add **Browserflow for Growth Automation** to your workflow and create a
   **Browserflow OAuth2 API** credential.
2. For a new self-hosted n8n installation, send the exact **OAuth Redirect URL**
   shown in the credential to **hello@browserflow.io** so it can be registered.
3. Connect your account, sign in to Browserflow, and approve the permissions.
4. Return to n8n and select your credential.

There is no API key or client secret to copy. The connection can find your
published flows, start runs, and retrieve their results. Your n8n instance
receives the inputs and results you use in your workflow. You can revoke access
in Browserflow under **Account → Connected apps**.

## Run your first flow

1. In Browserflow, build your browser flow, define its inputs and output fields,
   test it, and publish it.
2. In n8n, choose it using **Flow → From List**, or enter its ID with **By ID**.
3. Fill in **Inputs** with fixed values or map data from an earlier n8n node.
4. Execute your workflow. Browserflow runs the published flow and the node waits
   for its results.
5. Use the returned fields in the next n8n nodes to update your apps, send an alert,
   or continue processing the data.

For example, take a company website from your CRM, pass it into your research
flow, and map the returned company details back to that CRM record. Or run a
product-monitoring flow on a schedule, compare prices, and send an alert when
something changes. These are workflows you configure using this node and the
other n8n nodes for your chosen apps.

Each incoming n8n item starts one Browserflow run and returns one output item.
Your flow determines the returned fields. If a field contains a list, use n8n's
**Split Out** node to process each row separately. For example, a flow returning
`{"items":[{"name":"Example"}],"count":1}` makes `{{$json.items}}` and
`{{$json.count}}` available to later nodes.

Import the [starter workflow](https://github.com/browserflow-io/n8n-nodes-browserflow-growth-automation/blob/main/examples/run-flow.json)
to try the connection. Select your credential and published flow, then map its
inputs. The example is inactive and contains no credentials.

## Options

- **Limit:** return up to 100 results per list in one run. Accepts 1–100; if omitted,
  the flow's saved list limit is used, capped at 100.
- **Offset:** skip results to collect a later batch. Accepts 0–250000. For batches
  of 100, use offsets 0, 100, 200, and so on. Your flow must be set up to reach
  the later results, for example through pagination or scrolling.
- **Timeout (Seconds):** how long n8n waits for the result. Defaults to 300 seconds;
  accepts 1–3600. Larger offsets may need more time, and your n8n workflow or
  instance may have its own time limit.

Limit and Offset apply to each list in the flow. Each batch runs the flow again,
including its website actions, so use batching where repeating those actions is
intended. If n8n stops waiting, the Browserflow run may still be running. Check
its run history before starting another execution.

## Troubleshooting

- **Flow missing from the list:** test and publish it in the connected Browserflow
  account, then refresh the list. Draft flows are not listed.
- **Inputs missing or outdated:** define inputs in Browserflow, test and publish
  the updated flow, then refresh its input fields in n8n. Leave optional fields
  unset to use their published defaults.
- **Connection rejected:** check that your exact OAuth Redirect URL is registered.
  If access was revoked, reconnect the credential.
- **Subscription required:** check subscription access in the Browserflow account
  you connected.
- **Website login expired:** sign in again in Browserflow and update the flow's
  saved login profile.
- **Run timed out:** inspect the run in Browserflow before trying again. A new n8n
  execution starts a new run and may repeat website actions.

## Help and resources

- [Browserflow documentation](https://browserflow.io/docs)
- [Browserflow support](https://browserflow.io/support) or **hello@browserflow.io**
- [Report an integration issue](https://github.com/browserflow-io/n8n-nodes-browserflow-growth-automation/issues)

Do not include credentials or private website data in public issues.
This package connects to the current Browserflow platform. The older
`n8n-nodes-browserflow` package and Browserflow for LinkedIn are separate;
installing this package does not migrate existing workflows.

For contributors: [development and release notes](https://github.com/browserflow-io/n8n-nodes-browserflow-growth-automation/blob/main/RELEASE.md).
Licensed under [MIT](https://github.com/browserflow-io/n8n-nodes-browserflow-growth-automation/blob/main/LICENSE.md).
