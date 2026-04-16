<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="color-scheme" content="light only">
<title>Threat Hunt Report – Scattered Spider</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --navy:      #0d1b2a;
    --blue:      #1a4a7a;
    --accent:    #1e88e5;
    --accent2:   #e53935;
    --light:     #e8f0fe;
    --lighter:   #f4f7fc;
    --border:    #c5d5e8;
    --text:      #1a2332;
    --muted:     #5a6a7e;
    --white:     #ffffff;
    --mono:      'IBM Plex Mono', monospace;
    --sans:      'IBM Plex Sans', sans-serif;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; color-scheme: light only; }

  html { background: #ffffff !important; color-scheme: light only; }

  body {
    font-family: var(--sans);
    font-size: 11pt;
    color: var(--text);
    background: #ffffff !important;
    max-width: 780px;
    margin: 0 auto;
    padding: 48px 56px;
    line-height: 1.65;
  }

  /* ── COVER ─────────────────────────────────────────── */
  .cover {
    margin-bottom: 40px;
    padding-bottom: 28px;
    border-bottom: 3px solid var(--navy);
  }

  .cover-eyebrow {
    font-family: var(--mono);
    font-size: 8.5pt;
    font-weight: 600;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 10px;
  }

  .cover-title {
    font-family: var(--sans);
    font-size: 28pt;
    font-weight: 700;
    color: var(--navy);
    line-height: 1.1;
    margin-bottom: 6px;
  }

  .cover-subtitle {
    font-size: 12pt;
    font-weight: 300;
    color: var(--muted);
    margin-bottom: 24px;
  }

  /* ── METADATA TABLE ────────────────────────────────── */
  .meta-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0;
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    margin-bottom: 0;
  }

  .meta-row {
    display: contents;
  }

  .meta-label {
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--white);
    background: var(--blue);
    padding: 8px 12px;
    border-bottom: 1px solid #2a5a8a;
  }

  .meta-value {
    font-size: 9.5pt;
    color: var(--text);
    background: var(--lighter);
    padding: 8px 12px;
    border-bottom: 1px solid var(--border);
    border-left: 1px solid var(--border);
  }

  .meta-row:last-child .meta-label,
  .meta-row:last-child .meta-value { border-bottom: none; }

  .badge-high {
    display: inline-block;
    background: var(--accent2);
    color: white;
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 2px;
    letter-spacing: 0.06em;
  }

  .badge-actor {
    display: inline-block;
    background: var(--navy);
    color: white;
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 2px;
    letter-spacing: 0.06em;
  }

  /* ── SECTIONS ──────────────────────────────────────── */
  .section {
    margin-bottom: 36px;
  }

  h1 {
    font-family: var(--sans);
    font-size: 14pt;
    font-weight: 700;
    color: var(--navy);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding-bottom: 6px;
    border-bottom: 2px solid var(--accent);
    margin-bottom: 14px;
    margin-top: 36px;
  }

  h2 {
    font-family: var(--sans);
    font-size: 11pt;
    font-weight: 700;
    color: var(--blue);
    margin-bottom: 8px;
    margin-top: 28px;
  }

  p {
    margin-bottom: 10px;
    font-weight: 300;
  }

  /* ── BLOCKQUOTE ────────────────────────────────────── */
  blockquote {
    border-left: 3px solid var(--accent);
    background: var(--lighter);
    padding: 12px 16px;
    margin: 12px 0;
    font-style: italic;
    color: var(--text);
    font-size: 10.5pt;
  }

  /* ── FLAG CARDS ────────────────────────────────────── */
  .flag-card {
    border: 1.5px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    margin-bottom: 28px;
    page-break-inside: avoid;
  }

  .flag-header {
    display: flex;
    align-items: center;
    gap: 12px;
    background: var(--navy);
    padding: 10px 16px;
  }

  .flag-number {
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    color: var(--accent);
    letter-spacing: 0.1em;
    white-space: nowrap;
  }

  .flag-title {
    font-family: var(--sans);
    font-size: 10.5pt;
    font-weight: 600;
    color: var(--white);
  }

  .flag-body {
    padding: 14px 16px;
    background: var(--white);
  }

  .flag-objective {
    font-size: 9.5pt;
    color: var(--muted);
    font-style: italic;
    margin-bottom: 10px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
  }

  .flag-narrative {
    font-size: 10pt;
    font-weight: 300;
    margin-bottom: 14px;
  }

  .screenshot-label {
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--muted);
    margin-bottom: 6px;
  }

  .screenshot-box {
    border: 1.5px dashed var(--border);
    background: var(--lighter);
    border-radius: 3px;
    height: 130px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 12px;
  }

  .screenshot-box span {
    font-family: var(--mono);
    font-size: 8.5pt;
    color: #aab4c0;
  }

  /* ── MITRE TABLE ───────────────────────────────────── */
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 9.5pt;
    margin-top: 10px;
  }

  th {
    background: var(--navy);
    color: var(--white);
    font-family: var(--mono);
    font-size: 8pt;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    padding: 8px 12px;
    text-align: left;
  }

  td {
    padding: 8px 12px;
    border-bottom: 1px solid var(--border);
    font-weight: 300;
  }

  tr:nth-child(even) td { background: var(--lighter); }

  code {
    font-family: var(--mono);
    font-size: 9pt;
    background: var(--light);
    color: var(--blue);
    padding: 1px 5px;
    border-radius: 2px;
  }

  ul {
    padding-left: 20px;
    margin-bottom: 10px;
  }

  ul li {
    margin-bottom: 4px;
    font-weight: 300;
  }

  /* ── FOOTER ────────────────────────────────────────── */
  .report-footer {
    margin-top: 48px;
    padding-top: 12px;
    border-top: 1.5px solid var(--border);
    font-family: var(--mono);
    font-size: 8pt;
    color: var(--muted);
    display: flex;
    justify-content: space-between;
  }

  .no-query { color: var(--muted); font-style: italic; font-size: 9.5pt; }
  @media (prefers-color-scheme: dark) {
    html, body, div, p, h1, h2, h3, span, td, th, li, blockquote, table {
      background-color: revert !important;
      color: revert !important;
    }
    html { background: #ffffff !important; }
    body { background: #ffffff !important; color: #1a2332 !important; }
    .cover { background: #ffffff !important; }
    .meta-label { background: #1a4a7a !important; color: #ffffff !important; }
    .meta-value { background: #f4f7fc !important; color: #1a2332 !important; }
    .flag-header { background: #0d1b2a !important; }
    .flag-number { color: #1e88e5 !important; }
    .flag-title { color: #ffffff !important; }
    .flag-body { background: #ffffff !important; }
    .flag-objective { color: #5a6a7e !important; }
    .flag-narrative { color: #1a2332 !important; }
    .screenshot-box { background: #f4f7fc !important; }
    .screenshot-box span { color: #aab4c0 !important; }
    th { background: #0d1b2a !important; color: #ffffff !important; }
    td { background: #ffffff !important; color: #1a2332 !important; }
    tr:nth-child(even) td { background: #f4f7fc !important; }
    code { background: #e8f0fe !important; color: #1a4a7a !important; }
    blockquote { background: #f4f7fc !important; color: #1a2332 !important; }
    h1 { color: #0d1b2a !important; }
    h2 { color: #1a4a7a !important; }
    .cover-title { color: #0d1b2a !important; }
    .cover-subtitle { color: #5a6a7e !important; }
    .report-footer { color: #5a6a7e !important; }
    .badge-high { background: #e53935 !important; color: #ffffff !important; }
    .badge-actor { background: #0d1b2a !important; color: #ffffff !important; }
  }
</style>
</head>
<body>

<!-- ── COVER ─────────────────────────────────────────────────────────────── -->
<div class="cover">
  <div class="cover-eyebrow">Incident Report // IR-2026-0225-BEC</div>
  <div class="cover-title">Threat Hunt Report:<br>Scattered Spider</div>
  <div class="cover-subtitle">Business Email Compromise Investigation</div>

  <div class="meta-grid">
    <div class="meta-row">
      <div class="meta-label">Incident ID</div>
      <div class="meta-value">IR-2026-0225-BEC</div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Severity</div>
      <div class="meta-value"><span class="badge-high">HIGH</span></div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Date Reported</div>
      <div class="meta-value">26 February 2026, 09:30 UTC</div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Financial Impact</div>
      <div class="meta-value">£24,500 (funds frozen)</div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Affected Account</div>
      <div class="meta-value">Mark Smith</div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Organisation</div>
      <div class="meta-value">LogN Pacific Financial Services</div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Threat Actor</div>
      <div class="meta-value"><span class="badge-actor">Scattered Spider</span></div>
    </div>
    <div class="meta-row">
      <div class="meta-label">Status</div>
      <div class="meta-value">Active — Assigned</div>
    </div>
  </div>
</div>

<!-- ── TRIGGER ───────────────────────────────────────────────────────────── -->
<h1>Trigger</h1>
<p>LogN Pacific Financial Services received an urgent call from their bank's fraud department. A vendor payment of £24,500 was redirected to an unknown account. The receiving bank flagged the transaction as suspicious and froze the funds. The finance team insists they followed standard procedures.</p>

<!-- ── INITIAL REPORT ─────────────────────────────────────────────────────── -->
<h1>Initial Report</h1>
<p>Finance employee Mark Smith reported "weird MFA notifications" on the evening of 25 February. He was at home watching TV and kept getting prompted to approve a sign-in. He assumed it was an IT glitch and eventually approved one to make them stop. The next morning, colleagues discovered inbox rules nobody created.</p>

<!-- ── OBJECTIVE ──────────────────────────────────────────────────────────── -->
<h1>Objective</h1>
<p>Confirm the compromise. Identify the attacker's infrastructure. Scope the damage. Determine what inbox rules were created, what emails were sent, and what data was accessed. Identify the threat actor.</p>

<!-- ── IR LEAD BRIEF ──────────────────────────────────────────────────────── -->
<h1>IR Lead // Opening Brief</h1>
<blockquote>"We have a confirmed fraudulent wire transfer. £24,500 redirected to an unknown account. The bank caught it and froze the funds. Finance say they followed procedure … they got an email from a known colleague with updated banking details and processed it."</blockquote>
<blockquote>"That colleague is Mark Smith. Mark reported weird MFA notifications last night. He approved one just to make it stop. This morning his team found inbox rules nobody created. I need you in the sign-in logs now. Confirm the compromise, identify the attacker's infrastructure, and tell me how they got past MFA. Clock is running."</blockquote>

<!-- ── FLAGS ──────────────────────────────────────────────────────────────── -->
<h1>Flags</h1>

<!-- Flag 1 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 01</div>
    <div class="flag-title">Compromised Account</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Before you can investigate, confirm the compromised identity.</div>
    <div class="flag-narrative">By querying the SignInLogs within the attack time frame, the victim user was identified as Mark Smith.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 2 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 02</div>
    <div class="flag-title">Attacker Source IP</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Locate the attacker's source IP.</div>
    <div class="flag-narrative">To find Mark's legitimate IP, sign-in data prior to the attack window was queried and compared against the IP address recorded at the start of the attack.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 3 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 03</div>
    <div class="flag-title">Attack Origin Country</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Locate the attacker's origin country using the IP address.</div>
    <div class="flag-narrative">iplookup.org was used to retrieve geolocation data for the attacker's IP address, confirming the origin as the Netherlands.</div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste IP lookup screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 4 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 04</div>
    <div class="flag-title">MFA Denial Error Code</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What error code shows that MFA was required but not completed?</div>
    <div class="flag-narrative">SignInLogs were queried within the attack window and filtered for failed authentication attempts. The result returned the error code indicating MFA was required but not completed.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 5 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 05</div>
    <div class="flag-title">MFA Fatigue Intensity</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: How many MFA push requests came through before Mark accepted one?</div>
    <div class="flag-narrative">SignInLogs were filtered within the attack window and ResultSignatures sorted by time. This confirmed that Mark received 3 MFA push requests before accepting one, consistent with an MFA fatigue (push bombing) attack.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 6 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 06</div>
    <div class="flag-title">Application Accessed</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: After initial access, the attacker accessed a specific application – which one?</div>
    <div class="flag-narrative">SignInLogs were sorted from the exact time of the attacker's successful authentication. The attacker first accessed Outlook on the Web.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 7 & 8 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 07 &amp; 08</div>
    <div class="flag-title">Attacker OS and Browser</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Find the attacker's OS and browser.</div>
    <div class="flag-narrative">The DeviceDetail field within SignInLogs was examined, revealing the attacker's operating system and browser information.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 9 & 10 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 09 &amp; 10</div>
    <div class="flag-title">First Post-Auth Action and Rule Creation</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What was the first thing the attacker did after successfully accessing the account?</div>
    <div class="flag-narrative">The CloudAppEvents table provides telemetry for Office 365 and other cloud services. Querying this table revealed that the attacker first accessed Mark's mail items in Microsoft Exchange. Evidence of inbox rule creation was also identified.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 11–14 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 11 – 14</div>
    <div class="flag-title">Forward Rule Name and Details</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Find the name of the rule created by the attacker and its details.</div>
    <div class="flag-narrative">Parsing the RawEventData field in CloudAppEvents revealed how the attacker attempted to conceal their activity. The name field was left blank. The rule forwards any emails containing specific financial keywords to an external address: <code>insights@duck.com</code>. StopProcessingRules was set to <code>True</code> to prevent further rule evaluation and reduce detection.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 15 & 16 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 15 &amp; 16</div>
    <div class="flag-title">Delete Rule Name and Keywords</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Was a rule created to delete messages and conceal the attack?</div>
    <div class="flag-narrative">A second rule named <code>..</code> was identified. This rule automatically deleted inbound messages containing keywords associated with security alerts and suspicious activity notifications.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 17–20 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 17 – 20</div>
    <div class="flag-title">BEC Attack</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Search EmailEvents to find who received the fraudulent email.</div>
    <div class="flag-narrative">Querying EmailEvents using Mark Smith's display name returned the full attack chain. The recipient of the fraudulent email was <code>j.reynolds@lognpacific.org</code>. The attacker used thread hijacking to increase the email's apparent legitimacy. The subject line was: <code>RE: Invoice #INV-2026-0892 - Updated Banking Details</code>.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 21 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 21</div>
    <div class="flag-title">Cloud App Accessed</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What else did the attacker access, if anything?</div>
    <div class="flag-narrative">CloudAppEvents confirmed the attacker also accessed Mark Smith's Microsoft OneDrive during the same session.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 22 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 22</div>
    <div class="flag-title">SharePoint App Accessed</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What was the other cloud app the attacker accessed?</div>
    <div class="flag-narrative">Further querying of CloudAppEvents identified Microsoft SharePoint as an additional cloud application accessed by the attacker.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 23 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 23</div>
    <div class="flag-title">Session Correlation</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Check the CloudAppEvents inbox rule events. In RawEventData, find AppAccessContext.AADSessionId. Then confirm it matches the SessionId in SigninLogs for the attacker's successful authentication.</div>
    <div class="flag-narrative">The <code>AADSessionId</code> value extracted from RawEventData in CloudAppEvents was matched against the <code>SessionId</code> field in SignInLogs, confirming a single continuous attacker session from authentication through to post-compromise activity.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 24 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 24</div>
    <div class="flag-title">Conditional Access Status</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Conditional Access policies can block sign-ins from unmanaged devices or risky locations. Check the attacker's successful sign-in. What was the ConditionalAccessStatus?</div>
    <div class="flag-narrative">Filtering SignInLogs from the start of the attack and reviewing the <code>ConditionalAccessStatus</code> field confirmed that no Conditional Access policy was applied to the attacker's sign-in.</div>
    <div class="screenshot-label">Query Used</div>
    <div class="screenshot-box"><span>[ Paste query screenshot here ]</span></div>
    <div class="screenshot-label">Result</div>
    <div class="screenshot-box"><span>[ Paste result screenshot here ]</span></div>
  </div>
</div>

<!-- Flag 25 & 26 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 25 &amp; 26</div>
    <div class="flag-title">MITRE ATT&amp;CK Mapping</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Map the attack methods to the MITRE ATT&CK framework.</div>
    <div class="flag-narrative">MFA fatigue maps to T1621 because attackers spam MFA prompts to pressure users into approving access. Email rule creation maps to T1114.003 when used to forward and exfiltrate emails, or T1564.008 when used to hide alerts and conceal malicious activity.</div>
    <table>
      <thead>
        <tr><th>Technique ID</th><th>Name</th><th>Observed Behaviour</th></tr>
      </thead>
      <tbody>
        <tr><td><code>T1621</code></td><td>MFA Request Generation</td><td>Repeated push bombing until victim approved</td></tr>
        <tr><td><code>T1114.003</code></td><td>Email Forwarding Rule</td><td>Financial emails silently forwarded to insights@duck.com</td></tr>
        <tr><td><code>T1564.008</code></td><td>Email Hiding Rules</td><td>Deletion rule suppressed security alert notifications</td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- Flag 27 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 27</div>
    <div class="flag-title">Credential Source</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What type of malware typically provides initial credentials to groups like this?</div>
    <div class="flag-narrative">The type of malware that typically provides these stolen credentials is <strong>infostealer malware</strong>. Infostealers are designed to harvest saved passwords, browser cookies, session tokens, autofill data, and other sensitive information from infected systems. Threat actors then sell this data on underground markets for use in follow-on attacks. Common examples include families such as RedLine, Raccoon, and Lumma.</div>
  </div>
</div>

<!-- Flag 28 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 28</div>
    <div class="flag-title">Immediate Containment</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: What is the first remediation action?</div>
    <div class="flag-narrative">The first action is to disable Mark Smith's account and force a password reset.</div>
  </div>
</div>

<!-- Flag 29 -->
<div class="flag-card">
  <div class="flag-header">
    <div class="flag-number">FLAG 29</div>
    <div class="flag-title">Threat Actor Attribution</div>
  </div>
  <div class="flag-body">
    <div class="flag-objective">Objective: Throughout this investigation you observed MFA fatigue, inbox rule persistence, BEC targeting finance, and use of anonymising infrastructure. Who did this?</div>
    <div class="flag-narrative"><strong>Scattered Spider.</strong> The techniques, infrastructure, and targeting profile observed in this incident are consistent with Scattered Spider (also tracked as UNC3944), a financially motivated threat group responsible for high-profile intrusions at MGM Resorts, Caesars Entertainment, and multiple UK retail organisations.</div>
  </div>
</div>

<!-- ── FOOTER ─────────────────────────────────────────────────────────────── -->
<div class="report-footer">
  <span>Cyber Range // Hunt 02 — SCATTERED INVOICE</span>
  <span>IR-2026-0225-BEC</span>
</div>

</body>
</html>
