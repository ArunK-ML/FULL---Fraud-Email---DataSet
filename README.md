# FULL---Fraud-Email---DataSet
Fraud Email

Data Souces Link : https://www.kaggle.com/datasets/advaithsrao/enron-fraud-email-dataset

**Shape**: (8369, 32) → 8,369 rows and 32 columns

**Type**: All columns are stored as object (string-like), even if some represent booleans or numbers.

**Columns**: ['Folder-User', 'Folder-Name', 'Message-ID', 'Date', 'From', 'To', 'Subject',
 'Mime-Version', 'Content-Type', 'Content-Transfer-Encoding', 'X-From', 'X-To',
 'X-cc', 'X-bcc', 'X-Folder', 'X-Origin', 'X-FileName', 'Body', 'Cc', 'Bcc',
 'Time', 'Attendees', 'Re', 'Source', 'Mail-ID', 'POI-Present',
 'Suspicious-Folders', 'Sender-Type', 'Unique-Mails-From-Sender',
 'Low-Comm', 'Contains-Reply-Forwards', 'Label']

Key Columns (Important for Fraud Detection):

From / To / Cc / Bcc → Sender & recipients

Subject / Body → Email content

POI-Present → Whether a “Person of Interest” is involved (Fraud flag indicator)

Suspicious-Folders → Flag if mail was in a suspicious folder

Sender-Type → Internal vs External sender

Unique-Mails-From-Sender → Count of unique mails from sender

Low-Comm → Whether sender had low communication

Contains-Reply-Forwards → Boolean if reply/forward present

Label → Target variable (0 = Normal, 1 = Fraud-related) ✅

| From                                                                  | To                                                              | Subject                                | POI-Present | Suspicious-Folders | Sender-Type | Label |
| --------------------------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------- | ----------- | ------------------ | ----------- | ----- |
| [lyris@listserv.augusthome.com](mailto:lyris@listserv.augusthome.com) | [daren.farmer@enron.com](mailto:daren.farmer@enron.com)         | Welcome to WoodworkingTips.com!        | FALSE       | FALSE              | External    | 0     |
| [scott.joyce@bankofamerica.com](mailto:scott.joyce@bankofamerica.com) | [v.charles.weldon@enron.com](mailto:v.charles.weldon@enron.com) | RE: Friday                             | FALSE       | FALSE              | External    | 0     |
| customer\_service\@footlocker                                         | [dfarmer@enron.com](mailto:dfarmer@enron.com)                   | Order Confirmation from Footlocker.com | FALSE       | FALSE              | External    | 1     |


📂 Metadata Columns

Folder-User

The user’s personal mailbox directory (e.g., maildir).

Helps identify which Enron employee account the email belongs to.

Folder-Name

Specific folder in the mailbox (e.g., inbox, sent, or user’s custom folders).

Useful for tracking whether fraud-related emails were stored in unusual places.

Message-ID

Unique identifier for each email (like a fingerprint).

Prevents duplicates and helps link chains of communication.

Date

Timestamp of when the email was sent.

Patterns of fraud may cluster in certain time periods (e.g., around earnings reports).

👤 Sender & Receiver Information

From

The actual sender’s email address.

Important for detecting fraudulent external vs. internal sources.

To

Primary recipient(s).

Reveals communication networks (who talks to whom).

Cc

Carbon copy recipients.

Often used to hide others in the loop.

Bcc

Blind carbon copy recipients.

Rarely used normally → suspicious if heavily present.

X-From

Cleaned version of the sender’s name/address.

Sometimes more readable than raw “From”.

X-To

Cleaned version of recipient list.

Helps avoid parsing issues in “To”.

X-cc

Cleaned version of Cc recipients.

Might indicate hidden communication networks.

X-bcc

Cleaned version of Bcc.

Often extremely rare → anomalies matter.

📧 Email Structure & Content

Subject

The subject line of the email.

Can reveal fraud clues (e.g., “contract,” “deal,” “urgent”).

Body

Full text of the email.

Richest source of fraud detection via NLP.

Mime-Version

Email format version (usually 1.0).

More technical; not directly useful but can help detect unusual emails.

Content-Type

Type of content (text/plain, text/html, etc.).

HTML emails may carry hidden content/phishing attempts.

Content-Transfer-Encoding

Encoding method (7bit, base64, etc.).

Base64 might hide attachments or encrypted text.

🗂️ System Information

X-Folder

Path of the folder (e.g., /inbox/junk/).

Suspicious folders can be flagged.

X-Origin

Source account that generated the email.

Sometimes different from “From,” which can indicate spoofing.

X-FileName

Name of the email file saved locally.

Metadata useful for reconstruction.

📅 Meeting & Reply Info

Time

Time extracted separately (sometimes without date).

Can be used for analyzing communication hours.

Attendees

People included in meetings (if email contains meeting request).

Fraud may involve small secret groups.

Re

Reply chain marker (Re:).

Helps detect threads and if fraud-related communication is hidden in replies.

🏢 Source & Tracking

Source

Data source (here: “Enron Data”).

Mostly constant.

Mail-ID

Another unique identifier (hash of email).

For cross-checking.

🚩 Fraud-Specific Features

POI-Present

Flag if a Person of Interest (POI) was involved (TRUE/FALSE).

Strong fraud indicator.

Suspicious-Folders

TRUE if the email was stored in a suspicious folder.

Helps detect deliberate hiding.

Sender-Type

Internal vs. External.

External senders may be more suspicious.

Unique-Mails-From-Sender

Count of how many unique mails this sender has sent.

Very high or very low counts could be suspicious.

Low-Comm

TRUE if sender had low communication overall.

Someone who rarely communicates but sends critical fraud emails is suspicious.

Contains-Reply-Forwards

TRUE if email contains “Re:” or “Fwd:”.

Fraudsters may avoid forwards to reduce traceability.

🎯 Target Column

Label

The ground-truth fraud label:

0 → Normal email

1 → Fraud-related email ✅

This is the column you predict using ML models.

✅ Summary:

Metadata columns (Folder-*, Message-ID, etc.) → Organizing emails.

Communication columns (From, To, Cc, etc.) → Mapping networks.

Content columns (Subject, Body) → NLP-based fraud detection.

Fraud features (POI-Present, Suspicious-Folders, Low-Comm, etc.) → Pre-engineered features designed to highlight suspicious behavior.

Label → Supervised learning target.
