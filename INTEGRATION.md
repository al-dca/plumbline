<!-- forevenza-managed-integration/1 -->
# Plumbline

Plumbline screens a person or company name against the US Treasury OFAC SDN list and its aliases in seconds, returning each match with its score, entry number and programs and the list's publication date; a match is a lead for review, not a determination. Its company checks (LEI and SEC registration, SEC-reported XBRL figures and federal contract awards) answer from the public registries where they are running, and every answer names the record it came from.

Operated by Forevenza.

- [Canonical website](https://plumbline.forevenza.com/)
- [Current OpenAPI description](https://plumbline.forevenza.com/openapi.json)
- MCP endpoint: https://plumbline.forevenza.com/mcp
- Business contact: hello@plumbline.forevenza.com

## Discover the current interface

The published OpenAPI description is the source of truth for operations, inputs and any authentication requirements. This repository contains integration documentation; it does not promise that every operation is free or that a service request has been accepted. Follow the service's current terms before sending business information or creating a request.

```sh
curl --fail --silent --show-error 'https://plumbline.forevenza.com/openapi.json'
```

Run `node examples/discover.mjs` with Node.js 20 or later to list the current documented HTTP operations. It only reads the public specification and does not submit a customer request.
