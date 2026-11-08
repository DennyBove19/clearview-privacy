# Privacy policy source (ClearView for Salesforce)

Host this anywhere with a stable public URL and paste that URL into the Chrome Web
Store's **Privacy policy URL** field. A GitHub Gist, a page on your own domain, or a
Google Doc set to "anyone with the link" all work.

Two things to fill in before publishing: the **contact address** at the bottom, and the
**effective date**. Both are marked `TODO`.

Dev-only file. `dev-handoff/` never ships and `.md` is skipped by the packager.

---

# Privacy Policy for ClearView for Salesforce

**Effective date:** TODO
**Publisher:** BoveDev

## What ClearView is

ClearView is a Chrome side panel that displays Salesforce records to employees of the
organization that installed it. It is distributed unlisted and is intended for that
organization's staff, not for the general public.

## How ClearView signs you in

ClearView has no accounts, no passwords and no login of its own. It reads the Salesforce
session cookie already present in your browser for your company's Salesforce host and
uses it to call the Salesforce API as you. It follows that ClearView can only ever see the
records your own Salesforce user is permitted to see.

That session cookie is read at the moment a request is made, attached to that request,
and discarded. It is never written to disk, never copied anywhere, and never sent to any
destination other than the Salesforce host it came from.

## What ClearView reads

From Salesforce, on your behalf: leads, opportunities, orders and order line items,
service appointments, work orders, users and Chatter posts. In practice this includes
customer names, street addresses, phone numbers, contract amounts, payment dates and the
names of employees.

ClearView reads this data to display it. It does not build a profile, score anyone, or make
decisions about anyone.

## What stays on your device

ClearView caches what it reads so that moving between tabs does not refetch thousands of
records. All of this lives in Chrome's extension storage on your own computer:

- **Settings** (`chrome.storage.sync`): your selected office, timeframe, report defaults,
  column order and last open tab. Chrome may sync these across your own signed-in Chrome
  profiles, as it does for any extension setting.
- **Caches and history** (`chrome.storage.local`): cached Salesforce responses, one
  performance snapshot per report per day retained for roughly 120 days, a field-name
  cache, and a local log of cancellations.
- **Messaging setup, for managers who use it** (`chrome.storage.local`): your ClickSend
  credentials, your sending number, your message templates, and a local mirror of the
  recent sent-log so that "already texted" markers still show when the network does not
  answer.

None of this is transmitted to BoveDev or to anyone else.

## What leaves your device, and where it goes

ClearView talks to four destinations, and only these four.

**Your company's Salesforce org.** All record reads and writes. This is your own data
going back to your own system.

**Google Firestore.** One thing only: a log of which appointments and quotes have already
been texted, so that two managers do not message the same customer twice. It is one
document per day, whose entries are keyed by Salesforce record identifier and hold a
timestamp, who sent the message, and which kind of message it was. No customer name,
phone number, address or message body is stored in Firestore. Team configuration such as
office regions and the manager roster is read from Salesforce, not from Firestore.

**The OSRM routing service** (`router.project-osrm.org`). When you use route planning,
ClearView sends appointment coordinates, rounded to four decimal places, to get driving times
between stops. No names, no addresses as text, and no record identifiers are sent. Results
are cached locally for a week.

**ClickSend.** Only if a manager configures text messaging, which requires granting an
additional permission at that moment. When a message is sent, the recipient's phone number
and the message text go to ClickSend, which delivers the SMS. Managers supply their own
ClickSend credentials; those credentials are stored in Chrome's extension storage on the
manager's own device.

## What ClearView never does

- No analytics, telemetry, crash reporting or usage tracking of any kind.
- No advertising, and no third-party trackers or SDKs.
- No data is sent to BoveDev. The developer has no server and receives nothing.
- No data is sold, rented or transferred to anyone.
- No data is used to determine creditworthiness or for any lending purpose.
- No code is downloaded and run. Everything ClearView executes ships inside the extension.

## Retention and deletion

Cached Salesforce data and settings live on your device until you remove them.
Uninstalling ClearView deletes all of it. You can also clear it without uninstalling from
`chrome://extensions`, by opening ClearView's details and removing its site data.

Data in Salesforce is governed by your employer's own retention policy, not by ClearView. The
messaging log in Firestore is controlled by your organization's administrator. Message
delivery records held by ClickSend are governed by ClickSend's own policy.

## Children

ClearView is a workplace tool. It is not directed at children and is not intended for anyone
under 13.

## Changes to this policy

If this policy changes, the effective date above is updated and the revised policy is
posted at this same URL.

## Contact

Questions about this policy, or requests about data ClearView holds:

bovedev@gmail.com
