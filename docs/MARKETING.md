# JOMO Studio — Marketing, QR & Campaign Tracking

This document is the operational source of truth for JOMO Studio offline/online campaign tracking. The goal is to make every future print run, QR code, advertisement and campaign reproducible and attributable in GA4.

## 1. Current production baseline

- Website: https://jomostudio.nl
- GA4 Measurement ID: `G-4EZXY0FQH5`
- GA4 is loaded only in production from the shared `Base.astro` layout.
- Standard page views are tracked by GA4.
- Custom `contact_click` event tracks contact-link clicks.
- `contact_click` parameters: `method` and `link_url`.
- Supported contact methods currently include email, WhatsApp and Telegram; `tel:` links are also supported automatically if added later.

### Current public contact details

These values must be checked against the production website before producing a new physical print run:

- Name: Yaroslav Redka
- Role: Director, JOMO Studio
- Field: Web Development
- Email: `redyamusic@outlook.com`
- WhatsApp / phone: `+31 6 57337248`
- Website: `jomostudio.nl`
- Business-card language: English
- Geographic location: intentionally omitted from the card so the studio is not positioned as local-only.

Do not copy old contact information blindly. The production website remains the authority for contact details.

## 2. UTM naming convention

Use lowercase ASCII values, underscores between words, and stable names. Never create a QR code for a campaign before assigning its UTM values.

Required parameters:

- `utm_source` — physical/digital source or distribution origin.
- `utm_medium` — marketing medium.
- `utm_campaign` — campaign or rollout identifier.
- `utm_content` — creative, batch, placement or variant identifier.

Optional:

- `utm_term` — only when a meaningful keyword/audience dimension exists.

### Business card batch 1

Destination:

`https://jomostudio.nl/?utm_source=business_card&utm_medium=offline&utm_campaign=jomo_launch_2026&utm_content=card_v1`

Interpretation:

- source: `business_card`
- medium: `offline`
- campaign: `jomo_launch_2026`
- content: `card_v1`

This URL is the canonical tracking destination for the first business-card design/batch. Do not reuse `card_v1` for a materially different card design or distribution experiment.

## 3. Future QR / campaign rules

Each materially different channel, creative or distribution experiment should receive a distinguishable UTM combination. Examples:

- second card design: `utm_content=card_v2`
- flyer: `utm_source=flyer&utm_medium=offline`
- poster: `utm_source=poster&utm_medium=offline`
- Instagram campaign: `utm_source=instagram&utm_medium=paid_social`
- partner/referral placement: use a stable source identifier and document the partner/campaign before publishing.

If cards are deliberately split by city/event/country and attribution matters, create separate `utm_content` or campaign identifiers rather than printing one indistinguishable QR everywhere.

Do not encode personal or sensitive information in UTM parameters.

## 4. QR production standard

For print:

1. QR destination must be the final HTTPS URL with the approved UTM parameters.
2. Generate with high error correction when practical.
3. Preserve a proper quiet zone around the QR code.
4. Keep strong black/white contrast; avoid decorative modifications that reduce readability.
5. Test the final exported print file, not only the source QR image.
6. Test from at least two phones/camera apps before sending a large run to print.
7. Confirm the resulting visit appears in GA4 Realtime and that campaign dimensions are populated.

For a new batch, never overwrite the historical campaign identity if doing so would make old and new distribution impossible to distinguish.

## 5. Business card production baseline

Current format prepared for batch 1:

- Finished size: 85 × 55 mm
- Bleed: 3 mm on all sides
- Print-document page size with bleed: 91 × 61 mm
- Two-sided
- English
- No location
- Front: official JOMO branding / Web Development positioning
- Back: name, role, field, website, email, phone/WhatsApp and tracked QR
- Branding rule: only the real JOMO wordmark/logo from the repository `brand/` assets; never substitute an AI-generated/recreated logo.

Before printing, verify the chosen print shop's required size, bleed, PDF standard, color profile, minimum text size and safe-area rules. The printer specification overrides this baseline where necessary.

### Planned first physical run

- Quantity: 100 cards
- Intended print timing/location: Berlin, August 2026
- Tracking identity: `business_card / offline / jomo_launch_2026 / card_v1`

The intended location/timing is operational context, not a permanent brand location.

## 6. Measurement workflow

Before launch:

1. Define campaign purpose and distribution method.
2. Assign UTM values using this document.
3. Generate QR/link.
4. Test destination and redirect behavior.
5. Verify GA4 Realtime.
6. Archive the exact URL and creative/batch identifier here.
7. Only then print/publish.

After launch:

- Review acquisition by source / medium / campaign.
- Review landing-page engagement.
- Review `contact_click` events.
- Where possible, compare scans/sessions → contact clicks → actual enquiries → closed clients.
- Do not interpret a QR scan as a lead; the meaningful funnel is visit → contact intent → enquiry → client.

## 7. Campaign registry

Keep this table updated whenever a new tracked asset goes live.

| Status | Asset | Source | Medium | Campaign | Content | Destination | Notes |
|---|---|---|---|---|---|---|---|
| Planned / print-ready | Business card batch 1 | `business_card` | `offline` | `jomo_launch_2026` | `card_v1` | `https://jomostudio.nl/?utm_source=business_card&utm_medium=offline&utm_campaign=jomo_launch_2026&utm_content=card_v1` | First run, 100 cards; intended Berlin print |

## 8. Versioning policy

Create a new registry row when any of the following changes materially:

- channel/source;
- campaign objective;
- design/creative variant;
- CTA;
- landing page;
- target audience or distribution experiment where separate attribution is useful.

Keep old rows. Historical tracking identifiers must remain understandable later.

## 9. Preflight checklist for every new print run

- [ ] Contact details checked against production website
- [ ] Correct official brand asset used
- [ ] Correct final dimensions
- [ ] Printer-specific bleed confirmed
- [ ] Safe margins confirmed
- [ ] UTM destination recorded in campaign registry
- [ ] QR generated from exact recorded destination
- [ ] QR scanned successfully from final PDF/artwork
- [ ] Website opens over HTTPS
- [ ] GA4 Realtime receives test visit
- [ ] Contact CTA tracking tested
- [ ] Spelling/name/role reviewed
- [ ] Final PDF visually inspected at 100%+
- [ ] Printer requirements checked before order

## 10. Scaling principle

This repository should remain the source of truth for JOMO Studio's website-related marketing instrumentation. New cards, flyers, posters, paid campaigns, referral links and QR codes should be documented here before launch so campaign history and attribution do not depend on chat history or memory.
