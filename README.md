# breadcrumbs - LLM Tags Template

[![Cookiecutter Template](https://img.shields.io/badge/template-cookiecutter-brightgreen.svg)](https://github.com/cookiecutter/cookiecutter)

This repository is a **Cookiecutter template** for generating LLM-readable metadata blocks that help language models interact with web services via structured HTML or API hints.

## Purpose

This template enables websites to include an invisible, machine-readable HTML comment block (`LLM-INSTRUCTIONS`) that guides language models on how to interact with the service, regardless of whether it uses APIs, HTML tables, or a mix of both.

## Features

- Supports multi-path access: MCP endpoint, API, or HTML UI fallback.
- Declarative JSON structure embedded in HTML comments.
- Customizable query and response mappings.
- Compatible with any domain (biology, finance, weather, etc.).

## Usage

To generate a project:

```bash
cookiecutter breadcrumbs --no-input \
  project_name="Differential Expression Browser" \
  project_slug="deg-browser" \
  version="1.0.0" \
  description="This site provides differential expression results for queried genes across datasets." \
  doi="" \
  documentation_url="https://deg-browser.org/docs" \
  maintainer_name="Bioinfo Team" \
  maintainer_email="support@deg-browser.org" \
  mcp_endpoint_url="https://deg-browser.org/mcp" \
  api_endpoint_url="https://deg-browser.org/api/search" \
  http_method="GET" \
  timeout=15 \
  query_route="/search?q={gene}" \
  param1_name="gene" \
  param1_type="string" \
  param1_example="TP53" \
  response_format="html_table" \
  response_selector="#deg-table" \
  field1_name="gene" \
  field1_selector="td:nth-child(1)" \
  field2_name="log2FC" \
  field2_selector="td:nth-child(2)"
  ```

```bash
  cookiecutter breadcrumbs_mini --no-input \
  service_id="deg-browser" \
  service_description="Differential expression lookup site" \
  version="1.0.0" \
  doi="" \
  docs_url="https://deg-browser.org/docs" \
  mcp_url="https://deg-browser.org/mcp" \
  api_url="https://deg-browser.org/api/search" \
  http_method="GET" \
  timeout_sec=15 \
  html_route="/search?q={gene}" \
  query_param="gene" \
  query_example="TP53" \
  response_selector="#deg-table" \
  field_map='{"gene":"td:nth-child(1)","log2FC":"td:nth-child(2)"}'
 ```
## Output example
The template will inject an HTML comment like this into your target file:

```html
<!-- LLM-INSTRUCTIONS
{
  "$schema": "https://example.com/llm-webservice-meta-1.1.json",
  "id": "deg-browser",
  "name": "Differential Expression Browser",
  ...
}
END LLM-INSTRUCTIONS -->
```

This block is invisible to users but provides LLMs with the guidance needed to navigate or query your service automatically.