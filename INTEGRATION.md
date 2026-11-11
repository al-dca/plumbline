<!-- forevenza-managed-integration/1 -->
# Plumbline

Plumbline screens a person or company name against the US Treasury OFAC SDN list and its aliases in seconds, returning each match with its score, entry number and programs and the list's publication date; a match is a lead for review, not a determination. Its company checks (LEI and SEC registration, SEC-reported XBRL figures and federal contract awards) answer from the public registries where they are running, and every answer names the record it came from.

Operated by Forevenza.

- [Canonical website](https://plumbline.forevenza.com/)
- [Current OpenAPI description](https://plumbline.forevenza.com/openapi.json)
- MCP endpoint: https://plumbline.forevenza.com/mcp
- Business contact: hello@plumbline.forevenza.com

## Screen a name and retain the source context

Plumbline provides a focused OFAC SDN name screen with aliases. Its output supports investigation of candidate matches; it is not a comprehensive global sanctions check or a compliance decision.

1. Inspect tools/list, then call screen\_sanctions with the name to investigate. The optional min\_score ranges from 0.5 to 1; the default is 0.82.
2. Read matches together with publication, fetched\_at and entries\_screened. Keep the returned query and min\_score with any saved result so the context can be reproduced.
3. Review listed\_name, ofac\_uid, list, programs and the similarity score for each candidate. A name score does not establish that two parties are the same.
4. Discover the other available public-registry tools through the live schema below. Availability and input requirements may differ by operation.

- Coverage is OFAC SDN and its aliases, not every sanctions or export-control list. A no-match result is not clearance.
- At most 20 distinct designations are returned. entries\_screened counts source records including aliases, not distinct people or companies.
- The list is refreshed daily, but inspect fetched\_at and publication in the actual response; the response is not a guaranteed-current compliance record.



## Connect an MCP client

Use the remote Streamable HTTP endpoint in an MCP client that supports it. Clients that use a mcpServers configuration can start with:

```json
{
  "mcpServers": {
    "plumbline": {
      "type": "http",
      "url": "https://plumbline.forevenza.com/mcp"
    }
  }
}
```

Inspect the live tools before choosing an operation:

```sh
node examples/discover-mcp.mjs
```

This Node.js 20+ example initializes the connection and reads every page of tools/list. It prints each current tool's description, input schema and action annotations; it never invokes a tool or submits a customer request. If discovery fails, it reports an error rather than implying the operation is available. Review the operation's inputs and terms before calling it.

## Discover the current HTTP interface

The published OpenAPI description is the source of truth for HTTP operations, inputs and any authentication requirements. This repository contains integration documentation and client examples, not the server implementation. It does not promise that every operation is free or that a service request has been accepted. Follow the service's current terms before sending business information or creating a request.

```sh
curl --fail --silent --show-error 'https://plumbline.forevenza.com/openapi.json'
```

Run `node examples/discover.mjs` with Node.js 20 or later to list the current documented HTTP operations. It only reads the public specification and does not submit a customer request.
