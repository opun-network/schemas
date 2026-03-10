# Livelihood Domain – User Stories and Payload Mapping

This document describes **user stories** and **payload mapping** for the OPuN Livelihood domain (Beckn 2.0, `opun:livelihood`). It is intended for reviewers to verify that sample payloads align with signed user stories and the expected request–response flow.

**Schema and examples location:**  
- Schema extension: `livelihood/v1/schema-extension/`  
- Example payloads: `livelihood/v1/examples/` (by flow: discover, search, select, init, confirm, status, update, support, cancel)

---

## 1. User Stories

Actors: **Job Seeker** (via BAP), **Employer / Provider** (BPP). All flows use `context.domain`: `opun:livelihood`.

### 1.1 Job Seeker (BAP side)

| # | User story | Flow | Example payloads |
|---|------------|------|------------------|
| 1 | As a job seeker, I want to discover employers or catalogs so that I can find job opportunities. | Discover | `livelihood/v1/examples/discover/discover.json` → `on_discover.json` |
| 2 | As a job seeker, I want to search for jobs by keywords, location, work mode, or disability-friendly filters so that I see relevant listings. | Search | `livelihood/v1/examples/search/search.json` → `on_search.json` |
| 3 | As a job seeker, I want to select a job to see full details and the application form so that I can decide to apply. | Select | `livelihood/v1/examples/select/select.json` → `on_select.json` |
| 4 | As a job seeker, I want to submit an application with my profile and filled form (XForms 2.0) so that the employer receives it. | Init | `livelihood/v1/examples/init/init.json` → `on_init.json` |
| 5 | As a job seeker, I want to confirm my application after review so that it is formally submitted. | Confirm | `livelihood/v1/examples/confirm/confirm.json` → `on_confirm.json` |
| 6 | As a job seeker, I want to check the status of my application (e.g. in review, shortlisted, offered). | Status | `livelihood/v1/examples/status/status.json` → `on_status.json` |
| 7 | As a job seeker, I want to update my contact details on an existing application. | Update | `livelihood/v1/examples/update/update.json` (BUYER_CONTACT_UPDATE) → `on_update` |
| 8 | As a job seeker, I want to accept or decline a job offer so that the employer knows my decision. | Update | `livelihood/v1/examples/update/update_job_offer_accepted.json` (BUYER_OFFER_ACCEPTANCE) → `on_update` |
| 9 | As a job seeker, I want to confirm my joining date so that onboarding can be planned. | Update | `livelihood/v1/examples/update/update_joining_confirmed.json` (JOINING_CONFIRMED) → `on_update` |
| 10 | As a job seeker, I want to get support (e.g. application or hiring process) when I have questions. | Support | `livelihood/v1/examples/support/support.json` → `on_support.json` |
| 11 | As a job seeker, I want to withdraw my application when I no longer wish to be considered. | Cancel | `livelihood/v1/examples/cancel/cancel.json` → `on_cancel.json` |

### 1.2 Employer / Provider (BPP side)

| # | User story | Flow | Example payloads |
|---|------------|------|------------------|
| 1 | As an employer, I want to publish my job catalog so that job seekers can discover and search it. | Discover (catalog) | `livelihood/v1/examples/discover/catalog_publish.json`, `on_discover.json` |
| 2 | As an employer, I want to return relevant job results for a search so that candidates can choose roles. | Search | `livelihood/v1/examples/search/on_search.json` |
| 3 | As an employer, I want to return full job details and application form (XForms 2.0) when a job is selected. | Select | `livelihood/v1/examples/select/on_select.json` |
| 4 | As an employer, I want to receive and validate an application (form + profile) and return an order/application id. | Init | `livelihood/v1/examples/init/on_init.json` |
| 5 | As an employer, I want to confirm receipt of the application and set initial status (e.g. DRAFT, SUBMITTED). | Confirm | `livelihood/v1/examples/confirm/on_confirm.json` |
| 6 | As an employer, I want to return current application/order status when the candidate checks. | Status | `livelihood/v1/examples/status/on_status.json` |
| 7 | As an employer, I want to notify the candidate when status changes (e.g. in review, shortlisted, offer sent, joining confirmed). | Update | `livelihood/v1/examples/update/on_update.json`, `on_update_shortlisted.json`, `on_update_job_offer.json`, `on_update_job_offer_accepted.json`, `on_update_joining_confirmed.json` |
| 8 | As an employer, I want to provide support contact or ticket details when support is requested. | Support | `livelihood/v1/examples/support/on_support.json` |
| 9 | As an employer, I want to acknowledge withdrawal when the candidate or I cancel the application. | Cancel | `livelihood/v1/examples/cancel/on_cancel.json` |

### 1.3 Flow summary

- **BAP** sends: `discover`, `search`, `select`, `init`, `confirm`, `status`, `update`, `support`, `cancel`.
- **BPP** responds with the corresponding `on_*` action for each.
- **Update** is used for (1) BAP-initiated changes (contact update, offer acceptance, joining confirmation) and (2) BPP-initiated status notifications (in review, shortlisted, offer letter, offer accepted, joining confirmed). The same `transaction_id` / `order.id` ties the conversation.

---

## 2. Flow and Payload Mapping

Each Beckn action is a **request (BAP → BPP)** and **response (BPP → BAP)** pair. The typical livelihood sequence is: Discover → Search → Select → Init → Confirm → (Status | Update | Support | Cancel as needed).

### 2.1 Flow-to-file mapping

| Step | Action | Request (BAP → BPP) | Response (BPP → BAP) |
|------|--------|---------------------|----------------------|
| 1 | Discover | `livelihood/v1/examples/discover/discover.json` | `livelihood/v1/examples/discover/on_discover.json` |
| 2 | Search | `livelihood/v1/examples/search/search.json` | `livelihood/v1/examples/search/on_search.json` |
| 3 | Select | `livelihood/v1/examples/select/select.json` | `livelihood/v1/examples/select/on_select.json` |
| 4 | Init | `livelihood/v1/examples/init/init.json` | `livelihood/v1/examples/init/on_init.json` |
| 5 | Confirm | `livelihood/v1/examples/confirm/confirm.json` | `livelihood/v1/examples/confirm/on_confirm.json` |
| 6 | Status | `livelihood/v1/examples/status/status.json` | `livelihood/v1/examples/status/on_status.json` |
| 7 | Update | See §2.2 | See §2.2 |
| 8 | Support | `livelihood/v1/examples/support/support.json` | `livelihood/v1/examples/support/on_support.json` |
| 9 | Cancel | `livelihood/v1/examples/cancel/cancel.json` | `livelihood/v1/examples/cancel/on_cancel.json` |

### 2.2 Update flow variants (livelihood)

Within **update** / **on_update**, the same `transaction_id` and `order.id` are used; `updateType` and `fulfillmentStatus` / `applicationStatus` distinguish the variant.

| Variant | Direction | updateType / intent | Example file(s) |
|---------|-----------|---------------------|------------------|
| Contact update | BAP → BPP | `BUYER_CONTACT_UPDATE` | `livelihood/v1/examples/update/update.json` → `on_update` |
| Status: In review | BPP → BAP | `STATUS_UPDATE` | `livelihood/v1/examples/update/on_update.json` |
| Status: Shortlisted | BPP → BAP | `STATUS_UPDATE` | `livelihood/v1/examples/update/on_update_shortlisted.json` |
| Job offer (letter) | BPP → BAP | `STATUS_UPDATE` | `livelihood/v1/examples/update/on_update_job_offer.json` |
| Offer accepted | BAP → BPP then BPP → BAP | `BUYER_OFFER_ACCEPTANCE` then `STATUS_UPDATE` | `livelihood/v1/examples/update/update_job_offer_accepted.json` → `on_update_job_offer_accepted.json` |
| Joining confirmed | BAP → BPP and/or BPP → BAP | `JOINING_CONFIRMED` | `livelihood/v1/examples/update/update_joining_confirmed.json`, `livelihood/v1/examples/update/on_update_joining_confirmed.json` |

### 2.3 Application form (XForms 2.0)

- **on_select:** Form structure is provided in `beckn:xinput.beckn:form.beckn:data` (XForms 2.0 XML with empty data fields).
- **init** and **confirm:** Filled form data is sent/echoed in `beckn:orderAttributes.opun:applicationForm.opun:formData` (same XForms 2.0 structure with user-provided values).

---

## 3. Matching Sample Payloads to User Stories

- Each row in §1 maps a **user story** to a **flow** and to **example payload file(s)** under `livelihood/v1/examples/`.
- §2 maps each **flow step** to **request** and **response** payload paths.
- Reviewers can use this document to confirm that the sample payloads in the repository align with the signed user stories and the intended Beckn request–response sequence.
