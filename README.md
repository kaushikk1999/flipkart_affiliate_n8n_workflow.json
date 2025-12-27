# flipkart_affiliate_n8n_workflow.json

Flipkart (Affiliate API) → Structured Product Rows (n8n)

This repository contains an n8n workflow JSON that pulls Deals of the Day (DOTD) from the official Flipkart Affiliate Offer API, then normalizes the response into structured rows you can send to Google Sheets, databases, or any downstream system. 

What this workflow does

Calls Flipkart Affiliate DOTD Offer API endpoint:

GET https://affiliate-api.flipkart.net/affiliate/offers/v1/dotd/json 


Authenticates using required headers:

Fk-Affiliate-Id

Fk-Affiliate-Token 

Outputs a clean list of product-like rows with fields such as:

category, title, sellingPrice, mrp, discount, url, image

Prerequisites

A running n8n instance (cloud or self-hosted).

A Flipkart Affiliate Program account with Affiliate ID and Token (API access is for registered affiliates). 

Files

flipkart_affiliate_n8n_workflow.json — n8n workflow export (import this into n8n).

How to import into n8n

Open n8n Editor.

Use Import from File (or Import from URL) and select flipkart_affiliate_n8n_workflow.json. 


The workflow will appear in your canvas.

Workflow overview (nodes)

Manual Trigger — starts the workflow.

Set Credentials — stores FK_AFFILIATE_ID and FK_AFFILIATE_TOKEN (replace placeholders).

HTTP Request — calls the Flipkart Affiliate DOTD endpoint and returns JSON. 


Normalize to Rows (Code) — converts nested API response into flat rows for easy export.

Setup

Open the Set Credentials node:

Replace:

YOUR_AFFILIATE_ID

YOUR_AFFILIATE_TOKEN

Save the workflow.

Note: n8n exports do not include sensitive credential values when you use credential objects—this workflow keeps credentials in a Set node so you can quickly test, but for production you should store secrets more securely (env/credentials vault). 
n8n Docs

Run

Click Execute Workflow in n8n.

Inspect the output of Normalize to Rows to see structured items.

Output schema (example fields)

Each item is emitted as:

category (string)

title (string)

sellingPrice (number/string)

mrp (number/string)

discount (number/string)

url (string)

image (string)

Extending the workflow

Common next steps:

Add Google Sheets node to append rows into a sheet (structured data into sheets).

Add Postgres/MySQL/MongoDB node to store rows in a database.

Add a Cron trigger instead of Manual Trigger for scheduled pulls.

Troubleshooting

401/403 errors: Verify Affiliate ID/Token and headers in the HTTP Request node. The endpoint requires Fk-Affiliate-Id and Fk-Affiliate-Token. 


Unexpected JSON structure: Flipkart responses can vary; the Code node uses defensive parsing. If you see empty output, inspect the HTTP response and tweak the normalization mapping.

Timeouts: Increase timeout in the HTTP Request node if needed (n8n supports configurable HTTP requests). 


Compliance / Terms

Use this workflow in accordance with Flipkart’s Affiliate API Terms of Use and program rules. 
Flipkart Affiliate
