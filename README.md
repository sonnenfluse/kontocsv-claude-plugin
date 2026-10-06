# KontoCSV for Claude

KontoCSV is a remote MCP connector and Claude skill for converting PDF bank, card, and payment statements or transaction CSV files into validated accounting-ready exports.

The public Claude workflow deliberately keeps source documents outside Claude attachments. The connector creates a short-lived KontoCSV browser-upload link, the user selects the document directly on KontoCSV, and Claude then uses KontoCSV tools to inspect the source, prepare an existing-credit conversion, request explicit confirmation, track validation, and return an eligible export.

Supported destinations include Standard Bank CSV, DATEV, Lexware, MT940, CAMT.053, QuickBooks/QBO, Xero, Exact Online and additional locale-specific accounting profiles.

Documentation: https://www.kontocsv.de/en/claude-connector

Privacy policy: https://www.kontocsv.de/en/privacy/claude

Support: https://www.kontocsv.de/en/support

Support email: support@kontocsv.de

Terms of service: https://www.kontocsv.de/en/terms
