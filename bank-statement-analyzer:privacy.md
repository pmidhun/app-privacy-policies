---
title: Bank Statement Analyzer - Privacy Policy
---

# Privacy Policy for Bank Statement Analyzer

**Last updated:** October 3, 2026

This privacy policy describes how the Bank Statement Analyzer Android app ("the app") handles your information. The app is developed and operated by an independent developer, not a company with a dedicated support team — if you have questions, use the contact details at the bottom of this page.

## Summary

The app analyzes your bank and credit card statements entirely on your device by default. It does not require you to create an account, and it does not collect your name, email address, or any other personal identifier. It does not use analytics, advertising, or crash-reporting SDKs. The only data that ever leaves your device is described in detail below, and in every case it is sent for the specific purpose of making the app work, never sold, and never used for advertising.

## What data the app handles, and where it's stored

### Statement files and extracted transaction data

When you import a bank or credit card statement (PDF), the app:

- Stores the original PDF file in encrypted storage on your device, using Android's hardware-backed keystore to protect the encryption key.
- Extracts transaction data (dates, descriptions, amounts, running balances) and stores it in a local, encrypted (SQLCipher) database on your device.

This data is **not uploaded to any server** as part of normal statement processing. All PDF parsing and transaction extraction runs locally, on your device.

### Cloud OCR fallback (optional, per-document consent required)

Some statements are scanned/image-only PDFs with no extractable text layer. If the on-device parser cannot read a statement at all, the app can optionally send that specific PDF to a cloud OCR service (Amazon Textract, via the app's own backend) to extract its text.

- This only happens for a specific file, and only after the app shows you an explicit consent dialog naming that file and asking permission to send it off-device.
- If you decline, the file is not uploaded, and your decision is still recorded (locally and in a server-side log, for audit purposes) alongside no file content.
- If you accept, the PDF is transmitted over an encrypted connection to the app's backend (hosted on Amazon Web Services), processed by Amazon Textract to extract text, and the extracted text is returned to the app. The backend does not retain the PDF or the extracted statement text after the request completes.

### Transaction categorization (opt-in, description text only)

The app can automatically suggest a spending category (e.g. "Groceries", "Transport") for each transaction, using a cloud AI model (Amazon Bedrock, Anthropic Claude), via the app's backend.

- This feature requires a one-time, explicit consent before it is used for the first time. You can decline, and the app remains fully usable without it (you can categorize transactions manually instead).
- Only the bare transaction description text (e.g. a merchant name) is sent for categorization — **never** the amount, date, account number, or any other statement content. The backend independently re-validates every piece of text before it reaches the AI model, and rejects anything that looks like it might contain a date, amount, or account/reference number, as a safeguard independent of the app's own filtering.
- Categorization results are cached on your device so the same description doesn't need to be re-sent.

### Device identifier (no accounts, no login)

The app does not have user accounts or a login system. Instead, each installation of the app registers for a device-scoped identifier, used solely to authenticate the app's own requests to its backend (e.g. for the cloud OCR and categorization features above, and to check subscription status). This identifier is not linked to your name, email, or any other personal identifier, and is not shared with or sold to any third party.

### Subscription and billing information

If you choose to subscribe to the app's premium tier, billing is handled entirely by Google Play Billing. The app itself does not receive or store your payment details (card numbers, billing address, etc.) — Google processes payments under its own [Privacy Policy](https://policies.google.com/privacy). The app only receives confirmation of your subscription status to unlock premium features.

## Third-party services used

The app's backend infrastructure runs on **Amazon Web Services (AWS)**, specifically:

- **Amazon Textract** — optional cloud OCR, described above.
- **Amazon Bedrock** — optional AI-based transaction categorization, described above.

Subscriptions are processed by **Google Play Billing**.

No other third-party services, SDKs, advertising networks, or analytics platforms are integrated into the app.

## Data retention and deletion

- All statement files and transaction data are stored locally on your device and are deleted when you delete them within the app, or when you uninstall the app.
- The backend does not persist uploaded PDF content or extracted statement text beyond the time needed to process a single request.
- The backend retains only your device identifier and minimal usage counters (e.g. daily request counts, for abuse prevention) for as long as your installation remains active.
- Uninstalling the app removes all locally stored data. To request deletion of your device identifier and any associated backend records, contact the developer using the information below.

## Children's privacy

The app is not directed at children under 13, and the developer does not knowingly collect data from children under 13.

## Changes to this policy

This policy may be updated as the app's features change. Material changes will be reflected by updating the "Last updated" date above. Continued use of the app after a change constitutes acceptance of the updated policy.

## Contact

If you have questions about this privacy policy or how your data is handled, contact: **pmidhun007+bank-statements-analyzer@gmail.com**

---

*This document describes the app's actual data handling behavior as implemented in its source code.*
