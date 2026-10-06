---
name: kontocsv-bank-statement-conversion
description: Use KontoCSV to inspect bank, card, or payment statements and transaction CSVs and create validated accounting exports such as DATEV, Xero, Exact Online, MT940, CAMT.053, Lexware, or QBO.
---

# KontoCSV bank statement conversion

Use the KontoCSV connector when the user wants bookkeeping-grade extraction or an accounting export from a bank statement, card statement, payment statement, or transaction CSV.

## File boundary

For the public Claude connector, never ask KontoCSV to read a file attached to Claude. KontoCSV must not query or extract Claude memory, chat history, conversation summaries, or Claude-uploaded files.

When a source document is required:

1. Call `create_browser_upload_session` with the expected filename/type.
2. Give the returned KontoCSV browser-upload URL to the user.
3. Wait for the user to say the direct browser upload is complete.
4. Call `complete_browser_upload` with the returned upload session ID.
5. Use the returned source ID for inspection and conversion.

Do not replace this flow by reading or forwarding a Claude attachment.

## Inspect before conversion

Call `inspect_bank_statement` before conversion. Report the detected document type, page count when available, currency, balance evidence, compatible accounting profiles, and warnings.

If the user asked only for inspection or preparation, stop before conversion.

## Existing credits only

The public Claude connector uses only credits already available in the connected KontoCSV account. Use `prepare_bank_statement_conversion` to determine required and available credits.

If the result is `insufficient_credits`, explain that the user must manage credits directly in KontoCSV outside this connector. Do not invent prices, offer payment-card collection, or attempt checkout.

## Explicit confirmation

A conversion spends existing KontoCSV credits. Before calling `convert_bank_statement_for_accounting`, obtain explicit confirmation from the user after presenting:
- target export profile
- required existing credits
- available existing credits
- relevant inspection warnings

Never infer confirmation from an earlier general request if the user subsequently says not to start.

## Completion

After a conversion starts:
1. Use `get_conversion_status` until a terminal state is reached.
2. If the status is completed and an export is eligible, call `download_accounting_export`.
3. If the status is `soft_fail` or `hard_fail`, report the quality state accurately and do not imply that a validated export exists.

Strict formats such as MT940 and CAMT.053 require reliable opening and closing balance evidence. If they are not offered by inspection, recommend a supported normal accounting export instead.

## Scope

Do not invoke KontoCSV for unrelated documents such as employment contracts, legal drafting, resumes, or general document summaries.
