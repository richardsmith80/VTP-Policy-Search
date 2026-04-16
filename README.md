<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VA VTP & Beneficiary Travel Policy Search</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Arial,Helvetica,sans-serif;background:#f0f4f8;color:#1a1a1a;min-height:100vh}
#header{background:#1a3a5c;color:#fff;padding:18px 24px}
#header h1{font-size:20px;font-weight:700;margin-bottom:4px}
#header p{font-size:11px;opacity:.8;line-height:1.5}
#searchbox{background:#fff;border-bottom:1px solid #c8d3dc;padding:14px 24px;position:sticky;top:0;z-index:10;box-shadow:0 2px 8px rgba(0,0,0,.08)}
#searchbox input{width:100%;font-size:15px;padding:10px 14px;border:2px solid #1a3a5c;border-radius:6px;outline:none;color:#1a1a1a}
#searchbox input:focus{border-color:#2980b9;box-shadow:0 0 0 3px rgba(41,128,185,.15)}
#hint{font-size:11px;color:#546e7a;margin-top:6px}
#results{padding:16px 24px;max-width:1100px;margin:0 auto}
#summary{font-size:12px;color:#546e7a;margin-bottom:12px;padding:6px 0;border-bottom:1px solid #d0d7de}
.card{background:#fff;border-radius:8px;border:.5px solid #d0d7de;margin-bottom:14px;overflow:hidden;box-shadow:0 1px 4px rgba(0,0,0,.06)}
.card-header{padding:12px 16px;display:flex;align-items:flex-start;gap:10px;cursor:pointer;user-select:none}
.card-header:hover{background:#f7f9fb}
.tag{font-size:10px;font-weight:700;padding:2px 8px;border-radius:3px;white-space:nowrap;flex-shrink:0;margin-top:2px}
.tag-def{background:#e8eef5;color:#1a3a5c;border:1px solid #b0c4d8}
.tag-elig{background:#e6f4ea;color:#1a6632;border:1px solid #a8d5b5}
.tag-proc{background:#fff8e1;color:#7a5300;border:1px solid #ffe082}
.tag-stat{background:#f3e8ff;color:#5b1a8f;border:1px solid #c8a0f4}
.tag-gap{background:#fde8e8;color:#7a0000;border:1px solid #e04040}
.tag-smt{background:#fff3cd;color:#6d4c00;border:1px solid #ffd966}
.tag-pay{background:#e8f4fd;color:#1a3a5c;border:1px solid #b0cfe8}
.tag-deny{background:#fce8e8;color:#8b1a1a;border:1px solid #f4b3b3}
.tag-memo{background:#f0e8ff;color:#4a0080;border:1px solid #c8a0f4}
.tag-visn{background:#fff0e0;color:#7a3a00;border:1px solid #f0c040}
.tag-order{background:#e0f7e9;color:#1a6632;border:1px solid #6dbe8b}
.q{font-size:13px;font-weight:700;color:#0d2137;flex:1;line-height:1.4}
.arrow{font-size:12px;color:#888;flex-shrink:0;margin-top:2px;transition:transform .2s}
.card.open .arrow{transform:rotate(180deg)}
.card-body{display:none;padding:0 16px 14px 16px;border-top:.5px solid #e8eef5}
.card.open .card-body{display:block}
.answer{font-size:12px;line-height:1.7;color:#1a1a1a;margin-top:10px}
.answer b{color:#0d2137}
.answer .auth{display:inline-block;background:#f0f4f8;border:1px solid #c8d3dc;border-radius:3px;padding:1px 6px;font-size:10px;color:#1a3a5c;font-family:monospace;margin:2px 2px 2px 0}
.answer .warn{background:#fff8e1;border:1px solid #ffe082;border-radius:4px;padding:6px 10px;margin-top:8px;font-size:11px;color:#7a5300}
.answer .crit{background:#fde8e8;border:1px solid #e04040;border-radius:4px;padding:6px 10px;margin-top:8px;font-size:11px;color:#7a0000}
.answer .ok{background:#e6f4ea;border:1px solid #a8d5b5;border-radius:4px;padding:6px 10px;margin-top:8px;font-size:11px;color:#1a6632}
.answer .info{background:#e8f4fd;border:1px solid #b0cfe8;border-radius:4px;padding:6px 10px;margin-top:8px;font-size:11px;color:#1a3a5c}
.tpl-box{background:#f0f7f0;border:1px solid #6dbe8b;border-radius:6px;padding:10px 14px;margin-top:10px}
.tpl-box h4{font-size:11px;font-weight:700;color:#1a6632;margin-bottom:8px;text-transform:uppercase;letter-spacing:.04em}
.tpl-links{display:flex;flex-wrap:wrap;gap:6px}
.tpl-link{display:inline-flex;align-items:center;gap:4px;background:#1a6632;color:#fff;font-size:11px;font-weight:700;padding:4px 10px;border-radius:4px;text-decoration:none;cursor:pointer}
.tpl-link:hover{background:#155228}
.tpl-link.leaf{background:#c0392b}
.tpl-link.leaf:hover{background:#922b21}
.tpl-modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:9999;align-items:flex-start;justify-content:center;padding:40px 20px;overflow-y:auto}
.tpl-modal.show{display:flex}
.tpl-inner{background:#fff;border-radius:10px;max-width:700px;width:100%;padding:24px;box-shadow:0 8px 40px rgba(0,0,0,.25);position:relative}
.tpl-inner h2{font-size:16px;color:#1a3a5c;margin-bottom:4px}
.tpl-inner .sub{font-size:11px;color:#546e7a;margin-bottom:16px}
.tpl-inner .step{margin-bottom:12px}
.tpl-inner .step-num{display:inline-block;background:#1a3a5c;color:#fff;font-size:10px;font-weight:700;border-radius:50%;width:20px;height:20px;text-align:center;line-height:20px;margin-right:6px;flex-shrink:0}
.tpl-inner .step-title{font-size:12px;font-weight:700;color:#0d2137}
.tpl-inner .step-body{font-size:11px;color:#37474f;margin-top:4px;margin-left:26px;line-height:1.6}
.tpl-inner .step-body b{color:#0d2137}
.tpl-inner .note{background:#fff8e1;border:1px solid #ffe082;border-radius:4px;padding:6px 10px;font-size:11px;color:#7a5300;margin-top:4px;margin-left:26px}
.tpl-inner .crit-note{background:#fde8e8;border:1px solid #e04040;border-radius:4px;padding:6px 10px;font-size:11px;color:#7a0000;margin-top:4px;margin-left:26px}
.tpl-close{position:absolute;top:16px;right:16px;background:#546e7a;color:#fff;border:none;border-radius:4px;padding:4px 10px;font-size:11px;cursor:pointer;font-weight:700}
#empty{text-align:center;padding:60px 20px;color:#546e7a}
#empty h2{font-size:18px;margin-bottom:8px;color:#1a3a5c}
#empty p{font-size:12px;line-height:1.7}
.example-chips{display:flex;flex-wrap:wrap;gap:6px;justify-content:center;margin-top:14px}
.chip{background:#fff;border:1px solid #b0c4d8;border-radius:20px;padding:4px 12px;font-size:11px;color:#1a3a5c;cursor:pointer}
.chip:hover{background:#e8eef5}
#footer{text-align:center;padding:14px;font-size:10px;color:#888;border-top:.5px solid #d0d7de;margin-top:20px}
</style>
</head>
<body>

<!-- TEMPLATE MODALS -->
<div id="modal-smt" class="tpl-modal" onclick="closeMod('smt')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('smt')">✕ Close</button>
  <h2>Special Mode Transport (SMT) — Ambulance &amp; Wheelchair Van</h2>
  <div class="sub">Cerner BT Order Guide | Requires clinician signature | Authority: 38 CFR 70.10(d); 38 CFR 70.30(a)(4)</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">Access patient chart in Cerner</span>
  <div class="step-body">Encounter must be at a facility location. Create a between-visit encounter at a facility location if needed.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Place Beneficiary Travel Order — select "Special Mode"</span>
  <div class="step-body"><b>Special Mode</b> is for: Ambulance (ALS &amp; BLS) or wheelchair van (e.g., Medstar, Medtran).<br>Non-physician positions must propose the order and send to provider for co-signature.<br>Order must be under <b>Inpatient or Ambulatory – In Office (Meds in Office)</b>.<br>Enter as <b>Proposed</b> with <b>clinical co-signature</b> held until provider signs.</div>
  <div class="note">ALS = Advanced Life Support ambulance | BLS = Basic Life Support ambulance | Wheelchair Van = stretcher/ambulette-equivalent SMT</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Fill out form — Required (Red) and Optional (Yellow) fields</span>
  <div class="step-body">• Select transport type: ALS, BLS, or Wheelchair Van<br>• Diagnosis must be listed (convert problem to diagnosis if not in current FIN)<br>• Duration: typically reflects one fiscal year; new order may be needed after expiration<br>• For recurring transport: select "To and From all authorized VA and Non-VA care" — non-clinical staff can then enter a <b>Repeat Travel Request</b> for each specific trip<br>• Suggested method for inpatient, CLC, and Veterans requiring documentation of transport requests to VTP</div>
  <div class="crit-note">SMT should NOT be used for convenience of the patient/family or because the claimant has "no other way to get in." More economical common carrier options must be considered first. Clinical justification must be consistent with how the claimant is transported in daily life.</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">Clinician requirements</span>
  <div class="step-body">Per 38 CFR 70.2: Clinician = Physician, PA, NP, Psychologist, or other independent licensed practitioner. Must have current credentialing and privileging at a VAMC. Clinical determinations may NOT be delegated to non-clinician staff. Clinicians cannot be compelled to make decisions outside their scope of practice.</div></div>
  <div class="step"><span class="step-num">5</span><span class="step-title">Sign order — Approval date must be a FUTURE date (at least 1 day)</span>
  <div class="step-body">Approval by date must be future for travel staff to complete in Multi Patient Task List. For urgent orders, notify local beneficiary travel office by phone.</div></div>
  <div class="step"><span class="step-num">6</span><span class="step-title">Message auto-generated to travel staff</span>
  <div class="step-body">If adjustments needed after review/approval: access form in documentation or form browser → forward updated form to Beneficiary Travel Pool. A new order may be needed based on individual circumstances.</div></div>
  <div class="step"><span class="step-num">7</span><span class="step-title">Travel staff: check Multi Patient Task List</span>
  <div class="step-body">Right-click in Multi Patient Task List → Order Info → History Tab to verify order was created by provider and proposed order signed by provider.</div></div>
</div>
</div>

<div id="modal-cc" class="tpl-modal" onclick="closeMod('cc')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('cc')">✕ Close</button>
  <h2>Common Carrier — Airline, Train, Bus, Taxi, Uber</h2>
  <div class="sub">Cerner BT Order Guide | Authority: 38 CFR 70.30(a)(1)</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">Access patient chart in Cerner</span>
  <div class="step-body">Encounter must be at a facility location. Create a between-visit encounter at a facility location if needed.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Place Beneficiary Travel Order — select "Common Carrier"</span>
  <div class="step-body"><b>Common Carrier</b> = VA sets up airline, train, bus, taxi, or Uber.<br>Must be placed PRIOR to flight, bus, and train travel.<br>Can also be used to justify reimbursement for taxi/Uber expenses for BT-eligible Veterans.<br>For medically necessary option or attendant: provider must sign.<br>Non-clinical needs: order can be released without provider signature.</div>
  <div class="note">Red = Required | Yellow = Optional | Green = Non-clinical (no provider signature needed)</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Fill out form</span>
  <div class="step-body">• Medical justification required if Veteran cannot ride a more economical method of public transportation<br>• Medically necessary option and attendant option must be signed by provider<br>• Note may be backdated by changing travel commence date — limited by duration selected by provider<br>• Changes in provider, Non-VA authorizations, Veteran eligibility, or residence may require a new note</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">For Uber specifically (Mann-Grandstaff / Spokane)</span>
  <div class="step-body">• <b>Spokane Uber Health</b> = one-time rides<br>• <b>Spokane Uber Health Standing Order</b> = recurring trips same day/time (dialysis, cancer treatments, etc.)<br>• After common carrier consult is placed and accepted by travel staff, LEAF request can be entered by anyone<br>• Requester notified via email at each stage of the process</div></div>
  <div class="step"><span class="step-num">5</span><span class="step-title">Attach flight itinerary in Cerner (Travel Staff)</span>
  <div class="step-body">Select Communicate → free text subject and message → Open other attachments → Browse → Network → C$ (local drive) or shared drive → locate saved itinerary → Attach → Send. Refresh chart to see added note.</div></div>
  <div class="step"><span class="step-num">6</span><span class="step-title">Sign and process</span>
  <div class="step-body">Approval by date must be future. Urgent orders: notify local BT office by phone. Travel staff check Multi Patient Task List.</div></div>
</div>
</div>

<div id="modal-nf" class="tpl-modal" onclick="closeMod('nf')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('nf')">✕ Close</button>
  <h2>Nearest Facility — Mileage Reimbursement to Non-Nearest VA or Non-VA Facility</h2>
  <div class="sub">Cerner BT Order Guide | Requires clinician signature | Authority: 38 CFR 70.30(b)(1)(2)</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">When to use Nearest Facility order</span>
  <div class="step-body"><b>Nearest Facility</b> = mileage reimbursement when a Veteran is paid to travel to a facility that is NOT the closest facility, because the nearest VA does not have the required care available within the necessary time frame.<br><br>Two acceptable justifications:<br>• <b>"This facility provides care which is unavailable within necessary time frame to the nearest VA healthcare facility"</b> — for Veterans receiving care at a VA facility<br>• <b>"Due to longstanding Veteran/provider/program relationship, it is clinically in the Veteran's best interest to continue at this facility"</b> — acceptable for BOTH VA and Non-VA care; this is the ONLY acceptable form for Non-VA care under MISSION Act (intended to treat the Veteran closest to their residence)</div>
  <div class="note">Needs to be signed by a provider within the scope of their practice.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Access patient chart in Cerner and place BT Order</span>
  <div class="step-body">Encounter must be at a facility location. Non-physician positions propose to provider for co-signature. Order under Inpatient or Ambulatory – In Office. Enter as Proposed with clinical co-signature held until provider signs.</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Fill out form</span>
  <div class="step-body">• Diagnosis must be listed (convert problem to diagnosis if not in FIN)<br>• Note may be backdated by changing travel commence date — limited by duration selected<br>• Changes in provider, Non-VA authorizations, Veteran eligibility, or residence may require a new note</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">Sign and process</span>
  <div class="step-body">Approval by date must be a future date (at least 1 day). Urgent: notify local BT office by phone. Travel staff check Multi Patient Task List → Order Info → History Tab.</div></div>
</div>
</div>

<div id="modal-att" class="tpl-modal" onclick="closeMod('att')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('att')">✕ Close</button>
  <h2>Attendant — Medical Escort for Common Carrier Travel</h2>
  <div class="sub">Cerner BT Order Guide | Requires clinician signature | Authority: 38 CFR 70.10(a)(8)</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">When to use Attendant order</span>
  <div class="step-body"><b>Attendant</b> = when a BT-eligible Veteran needs to be transported via common carrier (train, bus, or airline) by VA and needs a <b>medical escort</b> to accompany them.<br>• Must be signed and entered by a provider<br>• VA will set up the flight for an attendant of their choosing — VA cannot provide an attendant for the Veteran<br>• If a VA employee accompanies the Veteran, this must be coordinated with employee travel</div>
  <div class="note">Lodging entered in the form will NOT initiate a referral — lodging must be separately processed.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Access patient chart in Cerner and place BT Order</span>
  <div class="step-body">Encounter must be at a facility location. Non-physician positions propose to provider for co-signature. Medically necessary option and attendant option must be signed by provider.</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Fill out form</span>
  <div class="step-body">• Diagnosis must be listed<br>• Red = Required | Yellow = Optional<br>• Note may be backdated by changing travel commence date — limited by duration<br>• Changes in provider, Non-VA authorizations, eligibility, or residence may require a new note</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">Sign and process</span>
  <div class="step-body">Approval by date must be a future date (at least 1 day). Urgent: notify local BT office by phone.</div></div>
</div>
</div>

<div id="modal-rt" class="tpl-modal" onclick="closeMod('rt')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('rt')">✕ Close</button>
  <h2>Repeat Travel Request — Requesting a Ride (Not Reimbursement)</h2>
  <div class="sub">Cerner BT Order Guide | Can be entered by non-clinical staff if active SMT or Common Carrier order exists</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">When to use Repeat Travel Request</span>
  <div class="step-body"><b>Repeat Travel Request</b> = ONLY for requesting a ride (not reimbursement) when an existing SMT or Common Carrier order already covers the date of the request.<br><br>Example: A Veteran has a 1-year Special Mode order and needs VTS/BT alerted for a specific upcoming ride.<br><br><b>Often used by:</b> Social Workers, CLC staff, Nurses<br><b>Can be entered by:</b> Non-clinical staff IF an SMT or Common Carrier order signed by a clinician is active and covers this request</div>
  <div class="crit-note">Repeat Travel Request will be based off the original SMT or Common Carrier order. If the original order specifies a specific location and duration, this request must fall within those guidelines. If the Veteran is discharged, travel eligibility may change.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Access patient chart in Cerner</span>
  <div class="step-body">Encounter must be at a facility location. Verify active SMT or Common Carrier order exists and covers the requested date before entering.</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Fill out form and enter order</span>
  <div class="step-body">• Red = Required | Yellow = Optional<br>• Diagnosis must be listed<br>• Approval by date must be a future date (at least 1 day)<br>• Order can be entered by non-clinical staff for this request type</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">Message auto-generated to travel staff</span>
  <div class="step-body">If adjustments needed after review: access form in documentation or form browser → forward to Beneficiary Travel Pool. Acceptable formats shown in Multi Patient Task List History Tab.</div></div>
</div>
</div>

<div id="modal-cg" class="tpl-modal" onclick="closeMod('cg')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('cg')">✕ Close</button>
  <h2>Caregiver BT Order</h2>
  <div class="sub">Cerner BT Order Guide | Authority: 38 CFR Part 71; P.L. 111-163 §305</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">When to use Caregiver order</span>
  <div class="step-body">The <b>Caregiver</b> form authorizes travel for the primary or secondary caregiver of eligible Veterans, or individuals who have applied for the caregiver program and are traveling while participating in the <b>Program of Comprehensive Assistance for Family Caregivers (PCAFC)</b> under P.L. 111-163, Section 305.<br><br>Eligible travel includes:<br>• During approved instruction, education, and training to provide personal care services<br>• While accompanying the eligible Veteran during travel to/from a VA or VA-authorized medical facility (only if Veteran is also BT eligible)<br>• While traveling for consultation, professional counseling, marriage and family counseling, training, or MH services in connection with treatment of a Veteran receiving care for an SC disability</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Process in Cerner</span>
  <div class="step-body">Same process as other BT orders: access patient chart, place BT Order, select Caregiver form, fill out required fields, sign. Encounter must be at a facility location.</div></div>
</div>
</div>

<div id="modal-sd" class="tpl-modal" onclick="closeMod('sd')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('sd')">✕ Close</button>
  <h2>Service Dog BT Order</h2>
  <div class="sub">Cerner BT Order Guide | Authority: 38 U.S.C. §1714(a)(d); 38 CFR §17.148-154</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">When to use Service Dog order</span>
  <div class="step-body">The <b>Service Dog</b> consult is ONLY to be used in conjunction with travel benefits associated with:<br>• Obtaining, training, and re-training a service dog provided by VA<br>• Provision, maintenance, and replacement of hardware for the dog to perform tasks necessary to assist the Veteran<br><br>No income or SC eligibility requirement — BT eligibility for service dog travel is automatic under 38 U.S.C. §1714(a)(d).<br>Travel for obtaining a REPLACEMENT service dog is also covered, even if the Veteran is receiving other benefits for the dog being replaced.</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Important distinction</span>
  <div class="step-body">BT eligibility is automatic for service dog travel. However, if SMT (ambulance/wheelchair van) is needed for the trip, a VA clinician must SEPARATELY determine that SMT is medically required — the service dog travel authorization alone does not create SMT eligibility.</div></div>
</div>
</div>

<!-- LEAF MODAL -->
<div id="modal-leaf" class="tpl-modal" onclick="closeMod('leaf')">
<div class="tpl-inner" onclick="event.stopPropagation()">
  <button class="tpl-close" onclick="closeMod('leaf')">✕ Close</button>
  <h2>LEAF Pre-Payment Request — VISN 20 Common Carrier Pre-Pay</h2>
  <div class="sub">VISN 20 Only | For Veterans below pension income threshold unable to purchase their own common carrier travel</div>
  <div class="step"><span class="step-num">1</span><span class="step-title">What is the LEAF Pre-Pay request?</span>
  <div class="step-body">Under standard BT rules, common carrier travel (airfare, bus, train, taxi/Uber) is reimbursed AFTER travel. For Veterans who cannot afford to purchase their own travel upfront, VISN 20 has a hybrid approach allowing pre-pay consideration for Veterans with income below the VA pension threshold. This process must be completed <b>no less than 1 workweek before travel</b>.</div>
  <div class="crit-note">Pre-payment without completing the LEAF process may constitute an Anti-Deficiency Act violation (31 U.S.C. §1341).</div></div>
  <div class="step"><span class="step-num">2</span><span class="step-title">Step A — Income Verification</span>
  <div class="step-body">Facility care team verifies Veteran's combined earned and unearned income does not exceed the 2026 maximum annual pension rate (e.g., $17,441 for 0 dependents; $22,839 for 1 dependent; add ~$2,984 per additional dependent).</div></div>
  <div class="step"><span class="step-num">3</span><span class="step-title">Step B — LEAF Documentation</span>
  <div class="step-body">Via LEAF, document for each episode of pre-pay travel:<br>• Request naming: Lastname – Appointment date (e.g., Smith – 2-22-26)<br>• Attestation: care team member discussed proposed travel with Veteran (Yes/No)<br>• Attestation: Veteran indicated clear inability to pay and be reimbursed (Yes/No)<br>• Brief summary of need for travel (free text — no PHI/PII)<br>• Justification of financial hardship (free text — no PHI/PII)</div></div>
  <div class="step"><span class="step-num">4</span><span class="step-title">Steps C–F — Review and Approval Chain</span>
  <div class="step-body"><b>Step C:</b> Mobility Manager/VTP staff verify eligibility and income in Enrollment System → Approve or Disapprove<br><b>Step D:</b> Associate Director approves for Veterans below threshold; submits to VISN DND for Veterans over threshold<br><b>Step E:</b> VISN DND reviews and approves over-threshold requests<br><b>Step F:</b> Mobility Manager/VTP staff purchases ticket</div></div>
  <div style="margin-top:12px">
    <a href="https://leaf.va.gov/VISN20/496/visn20/report.php?a=TravelPrePay" target="_blank" class="tpl-link leaf" style="font-size:13px;padding:8px 16px;text-decoration:none">🔗 Open LEAF Pre-Pay Request Form</a>
  </div>
</div>
</div>

<div id="header">
  <h1>VA Veterans Transportation Program — Policy &amp; Regulation Search</h1>
  <p>Covers: Beneficiary Travel (BT) · Veterans Transportation Service (VTS) · Contract SMT · Cerner BT Orders · 38 U.S.C. 111 · 111A · 1703 · 1720J · 1725 · 1728 · VHA 1601B.05 · VHA 1695(1) · 38 CFR Part 70 · Policy Memos · VISN 20 Pre-Pay · Transplant Travel · SMT Clinical Determinations</p>
</div>
<div id="searchbox">
  <input type="text" id="q" placeholder="Type a question or keyword — e.g. 'how do I order a wheelchair van in Cerner' or 'deductible waiver' or '1720J'" oninput="search()">
  <div id="hint">Try: order ambulance · wheelchair van Cerner · common carrier · nearest facility · repeat travel · attendant · deductible · SMT · 1720J · 1725 · AMA · gap scenario · dialysis · transplant · drug rehab · VISN 20 pre-pay · LEAF · PADRECC · rural · foreign travel · BT eligible · not BT eligible</div>
</div>
<div id="results">
  <div id="summary" style="display:none"></div>
  <div id="cards"></div>
  <div id="empty">
    <h2>VA VTP &amp; Beneficiary Travel Policy Search</h2>
    <p>Type any question, keyword, or topic above.<br>Results include Cerner order guides, regulatory citations, policy memos, and the VTP authorization matrix.</p>
    <div class="example-chips">
      <span class="chip" onclick="setQ('how do I order ambulance in Cerner')">Order ambulance in Cerner</span>
      <span class="chip" onclick="setQ('wheelchair van SMT order Cerner')">Wheelchair van order</span>
      <span class="chip" onclick="setQ('common carrier Uber order Cerner')">Common carrier / Uber</span>
      <span class="chip" onclick="setQ('nearest facility order non-VA mileage')">Nearest facility order</span>
      <span class="chip" onclick="setQ('repeat travel request VTS ride')">Repeat travel request</span>
      <span class="chip" onclick="setQ('attendant medical escort order')">Attendant order</span>
      <span class="chip" onclick="setQ('who is eligible for beneficiary travel')">BT eligibility</span>
      <span class="chip" onclick="setQ('deductible waiver financial hardship')">Deductible waiver</span>
      <span class="chip" onclick="setQ('non-VA ER to SNF gap scenario')">Non-VA ER to SNF</span>
      <span class="chip" onclick="setQ('1720J suicidal crisis transport')">1720J suicide crisis</span>
      <span class="chip" onclick="setQ('AMA against medical advice transport')">AMA discharge</span>
      <span class="chip" onclick="setQ('VISN 20 prepay LEAF common carrier')">VISN 20 pre-pay / LEAF</span>
      <span class="chip" onclick="setQ('transplant travel donor cost responsibility')">Transplant travel</span>
      <span class="chip" onclick="setQ('BT eligible vs not BT eligible difference')">BT eligible vs not BT eligible</span>
    </div>
  </div>
</div>
<div id="footer">Reference only — verify against current VHA directives and 38 CFR Part 70. | VTP: VHAMSVTPLeadership@va.gov | 404-828-5601 | BT Questions: VHABeneficiaryTravelQuestions@va.gov | Generated 2025</div>

<script>
function openMod(id){document.getElementById('modal-'+id).classList.add('show');document.body.style.overflow='hidden';}
function closeMod(id){document.getElementById('modal-'+id).classList.remove('show');document.body.style.overflow='';}

// ── KNOWLEDGE BASE ────────────────────────────────────────────────────────────
var KB=[

// ══ CERNER ORDER GUIDES ═══════════════════════════════════════════════════════
{tags:['order'],keywords:['ambulance order cerner ALS BLS special mode smt how to place order wheel chair van medstar medtran'],
q:'How do I order an ambulance or wheelchair van (SMT) in Cerner for a Veteran?',
a:'Use the <b>Special Mode (SMT)</b> Beneficiary Travel order in Cerner for ambulance (ALS or BLS) or wheelchair van transport.<br><br><b>Two eligibility gates must BOTH be confirmed before entering the order:</b><br>1. <b>BT Eligibility</b> — Veteran must be administratively BT eligible (SC disability, 30%+ rating, pension, income at/below pension rate, C&P exam, or service dog travel)<br>2. <b>Clinician medical necessity</b> — A VA clinician must determine SMT is medically required and document it<br><br><b>Who must sign:</b> Provider (Physician, PA, NP, Psychologist, or other independent licensed practitioner). Non-physician positions must propose to provider for co-signature.<br><br><b>Key rules:</b><br>• Diagnosis must be listed to generate the consult<br>• Approval date must be a FUTURE date (at least 1 day)<br>• Duration typically reflects one fiscal year<br>• For recurring transport: select "To and From all authorized VA and Non-VA care" — non-clinical staff can then enter Repeat Travel Requests for each specific trip<br><br><span class="auth">38 CFR 70.10(d)</span> <span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">VHA 1601B.05 App. A §15</span>'
+tplBox([['smt','📋 SMT / Ambulance / Wheelchair Van Order Guide']])
+'<div class="crit">SMT should NOT be used for convenience or because the Veteran has "no other way to get in." More economical common carrier must be considered first. Justification must be consistent with how the claimant is transported in daily life.</div>'},

{tags:['order'],keywords:['common carrier order cerner airline flight bus taxi uber train how to place order'],
q:'How do I order common carrier transport (airline, bus, taxi, Uber) in Cerner?',
a:'Use the <b>Common Carrier</b> Beneficiary Travel order in Cerner.<br><br><b>What Common Carrier covers:</b><br>• VA sets up airline, train, bus, or taxi travel — must be placed BEFORE flight/bus/train<br>• Can also justify reimbursement for taxi/Uber expenses for BT-eligible Veterans<br>• Should have medical justification if Veteran cannot ride a more economical method of public transportation<br><br><b>BT Eligibility required</b> — Veteran must be BT eligible for VA to set up or reimburse common carrier travel.<br><br><b>Who must sign:</b> Medically necessary option and attendant option must be signed by provider. Non-clinical common carrier needs do not require provider signature.<br><br><b>For Uber specifically (Mann-Grandstaff / Spokane):</b><br>• After common carrier consult is accepted by travel staff, enter LEAF request<br>• Spokane Uber Health = one-time rides<br>• Spokane Uber Health Standing Order = recurring trips same day/time (dialysis, cancer treatments)<br><br><span class="auth">38 CFR 70.30(a)(1)</span> <span class="auth">VHA 1601B.05 App. A §5(a)(1)</span>'
+tplBox([['cc','📋 Common Carrier / Uber Order Guide']])},

{tags:['order'],keywords:['nearest facility order cerner mileage non-VA non-nearest reimbursement mission act longstanding'],
q:'How do I place a Nearest Facility order in Cerner for mileage to a non-nearest VA or non-VA facility?',
a:'Use the <b>Nearest Facility</b> Beneficiary Travel order when a Veteran is traveling to a facility that is NOT the closest, because the nearest VA does not have the required care available.<br><br><b>Two acceptable justifications in Cerner:</b><br>1. <b>"This facility provides care which is unavailable within necessary time frame to the nearest VA healthcare facility"</b> — for Veterans receiving care at a VA facility only<br>2. <b>"Due to longstanding Veteran/provider/program relationship, it is clinically in the Veteran\'s best interest to continue at this facility"</b> — acceptable for BOTH VA and Non-VA care. This is the ONLY acceptable form for Non-VA care (MISSION Act is intended to treat the Veteran closest to their residence)<br><br><b>BT Eligibility required.</b> Must be signed by a provider within scope of practice.<br><br><b>Key rules:</b><br>• Diagnosis must be listed<br>• Note may be backdated by changing travel commence date — limited by duration provider selects<br>• Changes in provider, Non-VA authorizations, Veteran eligibility, or Veteran\'s residence may require a new note<br><br><span class="auth">38 CFR 70.30(b)(1)(2)</span> <span class="auth">VHA 1601B.05 App. A §5(c)(3)</span>'
+tplBox([['nf','📋 Nearest Facility Order Guide']])},

{tags:['order'],keywords:['attendant order cerner medical escort common carrier flight train bus sign provider'],
q:'How do I order an attendant (medical escort) for a Veteran traveling by common carrier in Cerner?',
a:'Use the <b>Attendant</b> Beneficiary Travel order when a BT-eligible Veteran needs to be transported via common carrier (train, bus, or airline) by VA and needs a medical escort.<br><br><b>Key rules:</b><br>• Must be signed and entered by a provider<br>• VA will set up the flight for an attendant of their choosing — VA cannot provide an attendant for the Veteran<br>• If a VA employee accompanies the Veteran, coordinate with employee travel separately<br>• Lodging entered in the form will NOT initiate a referral — must be separately processed<br>• Medically necessary option and attendant option must be signed by provider<br><br><b>BT Eligibility required</b> for the Veteran. Attendant is deductible-exempt.<br><br><span class="auth">38 CFR 70.10(a)(8)</span> <span class="auth">VHA 1601B.05 App. A §4(b)</span>'
+tplBox([['att','📋 Attendant Order Guide']])},

{tags:['order'],keywords:['repeat travel request cerner ride VTS non-clinical social worker nurse CLC inpatient'],
q:'How do I enter a Repeat Travel Request in Cerner? Who can enter it?',
a:'Use the <b>Repeat Travel Request</b> when you need to request a RIDE (not reimbursement) and an existing SMT or Common Carrier order already covers the date.<br><br><b>Who can enter it:</b> Non-clinical staff (Social Workers, CLC staff, Nurses) — IF an SMT or Common Carrier order signed by a clinician is active and covers the requested date.<br><br><b>When to use:</b><br>• Veteran has a 1-year Special Mode order and needs VTS/BT alerted for a specific upcoming ride<br>• Suggested method for inpatient, CLC, and Veterans requiring documentation of transport requests to VTP<br><br><b>Important limitations:</b><br>• Must fall within the original order\'s location and duration guidelines<br>• If the Veteran is discharged, travel eligibility may change — verify before entering<br>• Cannot be used to create a new transport authorization — the original clinician-signed order must be active<br><br><span class="auth">VHA 1695(1) App. A §3</span>'
+tplBox([['rt','📋 Repeat Travel Request Guide']])},

{tags:['order'],keywords:['caregiver order cerner PCAFC family caregiver comprehensive assistance PL 111-163'],
q:'How do I enter a Caregiver BT order in Cerner?',
a:'Use the <b>Caregiver</b> form to authorize travel for the primary or secondary caregiver of eligible Veterans, or individuals who have applied for the caregiver program and are traveling while participating in the <b>Program of Comprehensive Assistance for Family Caregivers (PCAFC)</b> under P.L. 111-163, Section 305.<br><br><b>Eligible Caregiver travel includes:</b><br>• During approved instruction, education, and training to provide personal care services<br>• While accompanying the eligible Veteran during travel to/from a VA or VA-authorized medical facility — ONLY if the Veteran is also BT eligible<br>• While traveling for consultation, professional counseling, marriage and family counseling, training, or MH services in connection with treatment of a Veteran receiving care for an SC disability<br><br><span class="auth">38 CFR Part 71</span> <span class="auth">P.L. 111-163 §305</span> <span class="auth">VHA 1601B.05 App. A §4(e)</span>'
+tplBox([['cg','📋 Caregiver Order Guide']])},

{tags:['order'],keywords:['service dog order cerner 17.148 training hardware replacement obtain'],
q:'How do I enter a Service Dog BT order in Cerner?',
a:'Use the <b>Service Dog</b> consult in Cerner ONLY for travel associated with:<br>• Obtaining, training, and re-training a VA-provided service dog<br>• Provision, maintenance, and replacement of hardware for the dog to perform tasks necessary to assist the Veteran<br><br><b>BT eligibility is automatic</b> — no income or SC eligibility requirement under 38 U.S.C. §1714(a)(d). Travel for obtaining a REPLACEMENT service dog is also covered even if receiving benefits for the dog being replaced.<br><br><b>If SMT is also needed:</b> A clinician must SEPARATELY determine that SMT is medically required — the service dog authorization alone does not create SMT eligibility.<br><br><span class="auth">38 U.S.C. §1714(a)(d)</span> <span class="auth">38 CFR §17.148-154</span> <span class="auth">VHA 1601B.05 App. A §3(f)</span>'
+tplBox([['sd','📋 Service Dog Order Guide']])},

// ══ BT ELIGIBLE VS NOT BT ELIGIBLE ═══════════════════════════════════════════
{tags:['elig'],keywords:['BT eligible vs not BT eligible difference what changes VTS contract SMT 1725 1720J'],
q:'What is the difference between BT eligible and not BT eligible — and why does it matter?',
a:'This is one of the most important distinctions in the entire VTP program. <b>BT eligibility determines which transport authorities and payment methods are available.</b><br><br><b>A Veteran IS BT eligible if they meet ONE of these:</b><br>• Traveling for treatment of a service-connected (SC) disability (any % rating)<br>• SC rating of 30% or more (traveling for any condition)<br>• Traveling for a scheduled C&P examination<br>• Receiving VA pension under 38 U.S.C. §1521<br>• Annual income does not exceed the maximum pension rate under 38 U.S.C. §1521<br>• Traveling to obtain a service dog (38 CFR §17.148)<br>• Veterans with SCI/D, vision impairment, or multiple amputations traveling to VA special rehab programs (P.L. 114-223)<br><br><b>IF BT ELIGIBLE:</b><br>✅ Can receive mileage/common carrier reimbursement<br>✅ Can use contract SMT (ambulance/wheelchair van) if clinician determines medically required<br>✅ Emergency SC care at non-VA = 38 U.S.C. 1728 applies (reimburses travel AND medical)<br>✅ Emergency processed as 1703 (if reported within 72 hrs) or 1728<br>✅ VISN 20 pre-pay may apply if income below pension threshold<br><br><b>IF NOT BT ELIGIBLE:</b><br>❌ Cannot receive BT mileage or common carrier reimbursement<br>❌ Cannot use contract SMT through BT program<br>✅ CAN still use VTS direct transport (enrolled Veterans for any scheduled/urgent/unscheduled visit)<br>✅ CAN receive emergency reimbursement under 38 U.S.C. 1725 (non-SC, no other insurance)<br>✅ 1720J emergent suicide care — NO BT eligibility required<br><br><span class="auth">38 CFR 70.10(a)</span> <span class="auth">38 U.S.C. §1725</span> <span class="auth">38 U.S.C. §1720J</span> <span class="auth">VHA 1601B.05 App. A §3</span><div class="crit">For emergency 911/ER scenarios: OCC through eCAMS determines whether 1703 (BT eligible required), 1725 (NOT BT eligible), or 1728 (BT eligible, SC condition) applies.</div>'},

// ══ DEFINITIONS ═══════════════════════════════════════════════════════════════
{tags:['def'],keywords:['attendant definition aid assistance physical clinician determination'],
q:'What is the definition of an Attendant for BT purposes?',
a:'<b>Attendant</b> — An individual accompanying a beneficiary who is eligible for beneficiary travel and who is medically determined to require the aid or physical assistance of another person, as determined by a VA clinician.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(a)</span><div class="ok">Attendant cannot be a VA employee. Medical necessity must be determined by a VA clinician. Attendants are deductible-exempt. For shared POV travel, mileage is limited to one beneficiary amount.</div>'},

{tags:['def'],keywords:['clinician definition who can order smt special mode who can sign'],
q:'Who qualifies as a clinician for BT purposes — who can sign SMT and Nearest Facility orders?',
a:'<b>Clinician</b> per 38 CFR 70.2 = Physician, Physician Assistant (PA), Nurse Practitioner (NP), Certified Nurse Practitioner (CNP), Clinical Nurse Specialist (CNS), Certified Nurse-Midwife (CNM), Psychologist, or other licensed independent practitioner acting within the scope of their practice.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">Fed. Reg. 2016-29950 eff. Jan 13 2017</span><br><br><b>Key rules in Cerner:</b><br>• Non-physician positions must propose the order and send to provider for co-signature<br>• Clinicians must have current credentialing and privileging with a VAMC and be current VA staff<br>• Clinical determinations may NOT be delegated to non-clinician staff<br>• Clinicians cannot be compelled to make decisions outside their scope of practice<div class="ok">Effective January 13, 2017, CNP, CNS, and CNM APRNs were added and may approve SMT without physician supervision. Psychologists and LIPs (social workers with advanced licensure) may make SMT determinations for MH/behavioral health conditions with a Chief of Staff Delegation Letter.</div>'},

{tags:['def'],keywords:['special mode transportation definition ambulance ambulette wheelchair van air not taxi not POV'],
q:'What is a Special Mode of Transportation (SMT)?',
a:'<b>Special Mode of Transportation</b> — Ambulance, ambulette, air ambulance, wheelchair van, or other mode specifically designed to transport disabled persons.<br><br><b>NOT a special mode:</b> bus, subway, taxi, train, airplane, or a modified privately-owned vehicle (POV) with special adaptive equipment.<br><br>A modified POV is reimbursable as standard mileage only — it cannot be invoiced as SMT.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(q)</span><div class="warn">Using a modified POV at SMT rates = improper payment. In Cerner, only enter SMT orders for true ambulance or wheelchair van (stretcher van) transport.</div>'},

{tags:['def'],keywords:['irregular discharge AMA against medical advice definition transport denied'],
q:'What is an irregular discharge / AMA discharge and why does it matter?',
a:'<b>Irregular Discharge</b> — Release of a competent patient from a VA or VA-authorized facility due to: refusal/neglect/obstruction of examination or treatment; leaving without clinician approval; or disorderly conduct when discharge is the appropriate disciplinary action.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(k)</span><div class="crit">AMA/irregular discharge = HARD STOP for all transport: BT mileage, VTS, and contract SMT. Applies to VA facilities AND VA-authorized non-VA facilities (CNH, community care inpatient, non-VA rehab, etc.). OIG has cited facilities for improper SMT payments on AMA discharges. Do NOT enter a Cerner BT order or arrange contract SMT for an AMA discharge.</div>'},

// ══ ELIGIBILITY ═══════════════════════════════════════════════════════════════
{tags:['elig'],keywords:['eligible beneficiary travel who qualifies veteran SC disability pension income 30 percent'],
q:'Who is eligible for Beneficiary Travel (BT) payments?',
a:'Veterans are BT eligible if they meet ONE of these qualifiers:<br><br><b>(a)</b> Traveling for treatment of a <b>service-connected (SC) disability</b> — any % rating<br><b>(b)</b> <b>SC rating of 30% or more</b> — traveling for any condition<br><b>(c)</b> Traveling for a <b>scheduled C&amp;P examination</b><br><b>(d)</b> Receiving <b>VA pension under 38 U.S.C. §1521</b><br><b>(e)</b> Annual income does not exceed the <b>maximum annual pension rate</b> under 38 U.S.C. §1521<br><b>(f)</b> Traveling to obtain a <b>service dog</b> under 38 CFR §17.148<br><b>(g)</b> Veterans with <b>vision impairment, SCI/D, or double/multiple amputation</b> traveling to VA special disabilities rehab program (P.L. 114-223, effective Oct 1, 2016)<br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 CFR 70.10(a)</span> <span class="auth">VHA 1601B.05 App. A §3</span>'
+tplBox([['leaf','💰 LEAF Pre-Pay Form (VISN 20 — for Veterans who cannot afford upfront travel)']])},

{tags:['elig'],keywords:['VTS eligibility veterans transportation service enrolled non-enrolled broader than BT'],
q:'Who is eligible for Veterans Transportation Service (VTS)? How is it different from BT?',
a:'<b>VTS eligibility is BROADER than BT eligibility.</b> A Veteran does NOT need to be BT eligible to ride VTS.<br><br><b>VTS is authorized for all enrolled Veterans</b> for any scheduled, urgent, or unscheduled visit; medication/prosthetic pickup; or VA-determined medical events. Non-enrolled Veterans can use VTS for C&amp;P exams, walk-in visits, and enrollment.<br><br><b>Key distinction:</b><br>• <b>BT eligible Veterans</b> → can receive mileage/reimbursement AND use contract SMT → can use VTS<br>• <b>NOT BT eligible but enrolled</b> → can use VTS direct transport but NOT contract SMT through BT program; NOT eligible for mileage reimbursement<br><br><span class="auth">38 U.S.C. §111A</span> <span class="auth">38 CFR 70.71</span> <span class="auth">VHA 1695(1) §5</span>'},

// ══ DEDUCTIBLE ════════════════════════════════════════════════════════════════
{tags:['pay'],keywords:['deductible amount monthly cap six one way three round trip 18 dollars'],
q:'What is the BT deductible amount and monthly cap?',
a:'<b>Deductible:</b> $3.00 per one-way trip ($6.00 for a round-trip).<br><b>Monthly cap:</b> $18.00 or six one-way trips (three round-trips), whichever occurs first.<br><br>Once the cap is reached, remaining travel for that calendar month is <b>free of deductible charges</b>.<br><br><span class="auth">38 CFR 70.31</span> <span class="auth">VHA 1601B.05 App. A §6</span><div class="info">SMT trips are deductible-EXEMPT. C&P exam trips are deductible-EXEMPT. Attendant trips are deductible-EXEMPT. Donor trips are deductible-EXEMPT.</div>'},

{tags:['pay'],keywords:['deductible waiver financial hardship pension means test income exempt severe'],
q:'When must the deductible be waived (financial hardship)?',
a:'The deductible <b>must</b> be waived when it would cause severe financial hardship. This occurs if the Veteran:<br><br><b>(a)</b> Is in receipt of a <b>VA pension</b>; or<br><b>(b)</b> Has income for the preceding year that does not exceed the <b>VA national means test household income threshold</b>; or<br><b>(c)</b> Can demonstrate that due to <b>loss of employment or disability incurrence</b>, income in the year of travel will not exceed the threshold<br><br>Waivers are valid through the end of the calendar year or until household income changes. Veteran must notify VA of any income change during the waiver period.<br><br><span class="auth">38 CFR 70.31(c)(d)(e)</span> <span class="auth">VHA 1601B.05 App. A §6(c)(d)</span><br><br>Current income thresholds: <b>va.gov/HEALTHBENEFITS/apps/explorer/AnnualIncomeLimits/HealthBenefits</b>'
+tplBox([['leaf','💰 LEAF Pre-Pay Form (VISN 20 — for Veterans who cannot afford upfront travel)']])},

// ══ PAYMENT PRINCIPLES ════════════════════════════════════════════════════════
{tags:['pay'],keywords:['meals lodging pre-approval required overnight stay reimbursement 50 percent per diem'],
q:'What are the rules for meals and lodging reimbursement?',
a:'VA may reimburse actual cost up to <b>50% of the government employee per diem rate</b> for meals and/or lodging when VA determines an overnight stay is required.<br><br><b>⚠️ PRE-APPROVAL IS MANDATORY — the single most common denial reason:</b><br>The Veteran must apply and receive approval BEFORE obtaining meals and/or lodging. Booking a hotel before approval = claim denied. No exceptions.<br><br><b>Factors VA considers:</b><br>• Distance the Veteran must travel<br>• Time of day the appointment is scheduled<br>• Weather or congestion conditions<br>• Veteran\'s medical condition and impact on ability to travel<br><br><span class="auth">38 CFR 70.30(a)(3)</span> <span class="auth">38 CFR 70.20(d)</span> <span class="auth">VHA 1601B.05 App. A §1(d) and §5(a)(4)</span><div class="crit">Pre-approval must precede the stay. There are no exceptions. In Cerner: lodging in the attendant form does NOT initiate a referral — lodging must be separately processed.</div>'},

{tags:['pay'],keywords:['round trip one way return trip approved scheduled unscheduled walk in emergency'],
q:'When is round-trip BT payment approved vs. one-way return only?',
a:'<b>Round-trip approved when:</b><br>• Travel was in connection with care <b>scheduled with VHA prior to arrival</b>; OR<br>• Travel was for <b>emergency treatment</b><br><br><b>One-way (return trip only) when:</b><br>• Travel was NOT scheduled and NOT emergency treatment — VA approves the return trip ONLY if VHA actually provided care or services<br><br><b>Round-trip denied when:</b><br>• Travel was not scheduled, not emergency, AND VHA did NOT provide care<br><br><span class="auth">38 CFR 70.4(b)(c)</span> <span class="auth">VHA 1601B.05 App. A §8(b)(c)</span>'},

{tags:['pay'],keywords:['apply deadline 30 days file claim beneficiary travel time limit submit'],
q:'What is the deadline to apply for BT reimbursement?',
a:'<b>Standard travel (no SMT):</b> Apply within <b>30 calendar days</b> after completing travel.<br><br><b>Travel including SMT:</b> Must apply AND obtain VA clinician approval <b>prior to travel</b>. If prior approval was not obtained, application is considered timely only if submitted within 30 days AND travel was for emergency treatment.<br><br><b>Meals/lodging:</b> Must apply and receive approval <b>before</b> obtaining meals and/or lodging.<br><br><b>Exception:</b> If a person becomes eligible after travel occurs, they may apply within 30 days of becoming eligible.<br><br><span class="auth">38 CFR 70.20(b)(c)(d)(f)</span> <span class="auth">VHA 1601B.05 App. A §1(b)(c)(d)(f)</span>'},

// ══ SMT CLINICAL DETERMINATIONS ══════════════════════════════════════════════
{tags:['smt'],keywords:['SMT clinical documentation medical necessity reminder dialog template CPRS Cerner how to document'],
q:'What documentation is required for Special Mode Transportation (SMT) authorization?',
a:'Effective May 1, 2016, the <b>Medical Transport Certification Reminder Dialog Template</b> (or equivalent electronic documentation in Cerner) is required to document:<br>• Aid and Attendance/Housebound status<br>• Nearest Facility determination<br>• Special Mode Transportation/Common Carrier determination<br>• National Caregiver status<br>• Attendant and Service Dog status<br><br>The template allows clinicians to certify transportation needs for <b>up to one year forward</b>, reducing per-trip burden. Must be approved by electronic signature in Cerner.<br><br><b>In Cerner:</b> Use the BT Beneficiary Travel order → Special Mode → fill out required fields → provider must sign (or proposed and co-signed).<br><br><span class="auth">10N Policy Memo Apr 12 2016</span> <span class="auth">38 CFR Part 70</span><br><br>Questions: <b>VHABeneficiaryTravelQuestions@va.gov</b>'
+tplBox([['smt','📋 SMT / Ambulance / Wheelchair Van Order Guide']])},

{tags:['smt'],keywords:['SMT clinical criteria who needs ambulance wheelchair when appropriate cannot ride common carrier safety'],
q:'What are the clinical criteria for approving SMT?',
a:'Two criteria MUST BOTH be met:<br><b>1. BT eligibility</b> — Veteran must be administratively BT eligible<br><b>2. Medical necessity</b> — A VA clinician must determine SMT is medically required<br><br><b>Medical Criteria (Safety Focus):</b><br>The justification must confirm the claimant <b>cannot safely be transported by private vehicle, taxi, bus, train, airplane, or other common carrier</b>. SMT is appropriate when:<br>• Veteran cannot transfer into a common carrier or POV without assistance<br>• Veteran requires restraints during transport<br>• Veteran requires medical care during transport that an attendant cannot provide<br><br>The clinical justification must be <b>consistent with how the claimant is transported in daily life</b>.<br><br><span class="auth">38 CFR 70.10(d)</span> <span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">VTP SMT Clinical Determinations Guidance</span>'
+tplBox([['smt','📋 SMT / Ambulance / Wheelchair Van Order Guide']])
+'<div class="warn">In Cerner, SMT orders are entered under the "Special Mode" BT order type. Non-physician positions must propose the order and send to provider for co-signature.</div>'},

// ══ EMERGENCY AUTHORITIES ═════════════════════════════════════════════════════
{tags:['stat'],keywords:['1725 emergency reimbursement non-VA facility non-SC enrolled veteran 911'],
q:'What is 38 U.S.C. 1725 and when does it apply?',
a:'<b>38 U.S.C. 1725 — Reimbursement for Emergency Treatment (non-SC conditions)</b><br><br>The Secretary SHALL reimburse a Veteran for emergency treatment at a non-VA facility. ALL of the following must be met:<br>1. Veteran is <b>enrolled</b> in VA health care<br>2. Veteran received VA care within the <b>preceding 24 months</b><br>3. Veteran is <b>personally financially liable</b> to the provider<br>4. Veteran has <b>no entitlement</b> to care under a health-plan contract<br>5. No other contractual or legal recourse against a third party<br>6. VA/Federal facilities were <b>not feasibly available</b><br><br><b>BT eligibility NOT required for 1725</b> — this is a reimbursement authority for Veterans who are enrolled but not necessarily BT eligible.<br><br><span class="auth">38 U.S.C. §1725</span> <span class="auth">38 CFR 17.1000-17.1008</span><div class="crit">1725 is a REIMBURSEMENT authority — NOT a pre-authorization for VA-arranged transport. Do NOT enter a Cerner BT order or arrange contract SMT for an ongoing emergency that 1725 covers. Processed by POM through eCAMS.</div>'},

{tags:['stat'],keywords:['1728 SC service connected emergency reimbursement travel incidental expenses'],
q:'What is 38 U.S.C. 1728 and how does it differ from 1725?',
a:'<b>38 U.S.C. 1728 — Reimbursement of Certain Medical Expenses (SC conditions)</b><br><br>1728 reimburses emergency treatment for <b>service-connected conditions</b> including <b>travel and incidental expenses</b>.<br><br><b>Key difference from 1725:</b><br>• <b>1725</b> = non-SC conditions; no other insurance required; BT eligibility NOT required<br>• <b>1728</b> = SC conditions; covers travel and incidental expenses in addition to medical costs; <b>BT eligibility IS required</b><br><br>Processing: 1728 is processed by POM through eCAMS.<br><br><span class="auth">38 U.S.C. §1728</span> <span class="auth">38 CFR 17.120</span>'},

{tags:['stat'],keywords:['1720J suicidal crisis emergent suicide care transport payment who pays BT eligible not required'],
q:'What is 38 U.S.C. 1720J and does it require BT eligibility?',
a:'<b>38 U.S.C. 1720J — Emergent Suicide Care</b><br><br><b>BT eligibility is NOT required.</b> 1720J covers ANY individual in acute suicidal crisis who is a Veteran or qualifies under 38 U.S.C. §1720I(b). No enrollment, income, or SC requirement.<br><br>The Secretary SHALL pay costs of emergency transportation under 1720J. <b>1720J has its own separate appropriation.</b><br><br><b>Period of care:</b> Up to 30 days inpatient/residential or up to 90 days outpatient. Notification to VA within 7 days of non-VA admission required.<br><br><span class="auth">38 U.S.C. §1720J</span> <span class="auth">38 CFR 17.1200-17.1225</span><div class="crit">DO NOT use BT-funded SMT contract or enter a standard Cerner BT order for 1720J transport. 1720J uses its own appropriation administered by OCC and Suicide Prevention Coordinator. Processed by POM through eCAMS.</div>'},

{tags:['stat'],keywords:['1703 community care contracts non-VA geographic inaccessibility MISSION Act gate'],
q:'What is 38 U.S.C. 1703 and why is it the "gate" for non-VA to non-VA transport?',
a:'<b>38 U.S.C. 1703 — Contracts for Hospital Care and Medical Services in Non-Department Facilities</b><br><br>When VA facilities cannot furnish economical care due to geographical inaccessibility or inability to provide required care, the Secretary may contract with non-VA facilities.<br><br><b>For non-VA to non-VA transport scenarios:</b><br>• 1703 is the ONLY authority that can authorize both the non-VA care AND transport between two non-VA facilities<br>• A 1703 authorization for the CARE does NOT automatically authorize transport between two non-VA facilities — OCC must separately authorize the transport<br>• Two separate authorizations are always required: one for the care, one for the transport<br><br><b>BT eligibility IS required</b> when 1703 is the applicable authority (processed by local BT Mobility Manager through eCAMS if reported within 72 hours).<br><br><span class="auth">38 U.S.C. §1703</span> <span class="auth">38 CFR Part 17</span><div class="crit">Do NOT enter a standard Cerner BT/SMT order for non-VA to non-VA scenarios. Call OCC and let eCAMS determine the authority. This is the most common OIG improper payment finding.</div>'},

// ══ eCAMS PROCESSING ══════════════════════════════════════════════════════════
{tags:['proc'],keywords:['ecams processing 1703 1725 1728 OCC 72 hours who processes payment pathway POM MM'],
q:'How are emergency transport payments processed through eCAMS? Which authority applies?',
a:'For 911/ER emergencies and approved non-VA ER-to-ER transfers, <b>OCC through eCAMS</b> determines the applicable payment authority:<br><br><table style="font-size:11px;border-collapse:collapse;width:100%;margin-top:6px"><tr style="background:#e8eef5"><th style="padding:4px 6px;text-align:left;border:.5px solid #c8d3dc">Authority</th><th style="padding:4px 6px;text-align:left;border:.5px solid #c8d3dc">When</th><th style="padding:4px 6px;text-align:left;border:.5px solid #c8d3dc">BT Eligible?</th><th style="padding:4px 6px;text-align:left;border:.5px solid #c8d3dc">Processed By</th></tr><tr><td style="padding:4px 6px;border:.5px solid #c8d3dc">38 U.S.C. 1703</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">Reported within 72 hrs</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">YES required</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">Local BT MM through eCAMS</td></tr><tr style="background:#f7f9fb"><td style="padding:4px 6px;border:.5px solid #c8d3dc">38 U.S.C. 1725</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">Veteran NOT BT eligible</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">NOT required</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">POM through eCAMS</td></tr><tr><td style="padding:4px 6px;border:.5px solid #c8d3dc">38 U.S.C. 1728</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">Veteran IS BT eligible (SC condition)</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">YES required</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">POM through eCAMS</td></tr><tr style="background:#f7f9fb"><td style="padding:4px 6px;border:.5px solid #c8d3dc">38 U.S.C. 1720J</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">Acute suicidal crisis</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">NOT required</td><td style="padding:4px 6px;border:.5px solid #c8d3dc">POM through eCAMS</td></tr></table><br><span class="auth">Transportation Arrangement and Payment Responsibility 2023</span>'},

// ══ GAP SCENARIOS ═════════════════════════════════════════════════════════════
{tags:['gap'],keywords:['non-VA ER to SNF skilled nursing facility transport who pays gap OCC 1703'],
q:'Can VA pay for transport from a non-VA ER to a non-VA SNF?',
a:'<b>CRITICAL GAP SCENARIO — Do NOT use standard BT/VTS or enter a Cerner BT order.</b><br><br>Standard BT cannot authorize non-VA to non-VA transport. Transport is only authorized if ALL of the following are met:<br>1. VA OCC authorizes the SNF placement under 38 U.S.C. 1703<br>2. OCC separately authorizes transport between the non-VA ER and the non-VA SNF<br>3. BOTH facilities are VA-authorized<br><br>The fact that VA paid for the non-VA ER care under 1725 or 1728 does NOT automatically extend BT authority to the SNF transfer.<br><br><span class="auth">38 CFR 70.30(b)(1)(2)</span> <span class="auth">38 U.S.C. §1703(a)</span><div class="crit">Call OCC immediately. Do NOT enter a Cerner BT or SMT order. This is the most commonly cited OIG improper payment scenario.</div>'},

{tags:['gap'],keywords:['non-VA ER to non-VA inpatient rehab IRF LTAC transport gap OCC'],
q:'Can VA pay for transport from a non-VA ER to a non-VA inpatient, rehab (IRF), or LTAC facility?',
a:'<b>Not through standard BT/VTS.</b> All require OCC authorization through 38 U.S.C. 1703.<br><br><b>For ALL non-VA ER to non-VA step-down transfers:</b><br>1. OCC must have an active 1703 authorization for the receiving non-VA facility specifically<br>2. OCC must separately authorize transport between the two non-VA facilities<br>3. BOTH facilities must be VA-authorized<br><br><b>Additional notes by facility type:</b><br>• <b>IRF</b>: IRF clinical criteria (3 hrs/day therapy, rehab potential) must be specifically authorized — a generic inpatient authorization does NOT cover IRF<br>• <b>LTAC</b>: LTAC level of care (ventilator, complex wound care) must be specifically authorized<br>• <b>Psychiatric</b>: If transfer is for suicidal crisis, 38 U.S.C. 1720J may apply instead of 1703<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">Call OCC. Do NOT enter Cerner BT or SMT order for these scenarios. Each facility in the chain needs its own independent OCC authorization.</div>'},

{tags:['gap'],keywords:['non-VA inpatient to non-VA SNF rehab gap OCC each facility independent authorization'],
q:'Can VA pay for transport from a non-VA inpatient facility to a non-VA SNF or rehab?',
a:'<b>Not through standard BT/VTS.</b> Each step in the post-acute chain requires its own independent OCC authorization.<br><br><b>Each receiving facility requires:</b><br>1. A NEW, separate OCC 1703 authorization for the receiving facility (the inpatient authorization does NOT carry over)<br>2. OCC must separately authorize transport between the two non-VA facilities<br>3. ALL facilities must individually be VA-authorized<br><br>The inpatient 1703 authorization does NOT carry over to SNF, IRF, or LTAC.<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">Call OCC for each step in the care chain. Do NOT enter Cerner BT or SMT orders for non-VA to non-VA transfers.</div>'},

{tags:['gap'],keywords:['non-VA SNF discharge home transport BT authorized place of stay standard BT'],
q:'When a Veteran leaves a VA-authorized non-VA SNF, is transport home covered by BT?',
a:'<b>Yes — discharge from a VA-authorized non-VA SNF to the Veteran\'s residence IS standard BT</b>, provided the Veteran is BT eligible.<br><br>The VA-authorized non-VA SNF is the Veteran\'s <b>place of stay</b> — discharge to residence = standard BT trip from place of stay.<br><br>Contract SMT authorized if BT eligible and SMT medically required for the discharge (common given patient medical condition at time of SNF discharge).<br><br>In Cerner: enter standard BT SMT or common carrier order as appropriate.<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.30(b)(1)(3)</span><div class="ok">Payment cap applies from the non-VA SNF location, not from the Veteran\'s prior permanent residence. This is one of the few non-VA chain steps that resolves to standard BT — an order CAN be entered in Cerner.</div>'},

// ══ DRUG / ALCOHOL REHAB ══════════════════════════════════════════════════════
{tags:['proc'],keywords:['drug alcohol rehab transport SATP substance abuse VA non-VA sober living halfway house'],
q:'What are the BT/VTS rules for drug and alcohol rehabilitation transport?',
a:'<b>VA SATP (VA Substance Abuse Treatment Program):</b><br>• Transport from home to VA SATP = standard BT if Veteran is BT eligible → enter Cerner BT order<br>• VA SATP residential = place of stay for BT purposes during the program<br>• Discharge from VA SATP to home = standard BT → enter Cerner BT order<br>• AMA from VA SATP = hard stop, no BT, no Cerner order, no contract SMT<br><br><b>Non-VA Drug/Alcohol Rehab (VA-authorized under 1703):</b><br>• Transport from home to non-VA rehab = standard BT if BT eligible and facility is VA-authorized → enter Cerner BT order<br>• Non-VA rehab residential = place of stay for BT purposes<br>• Discharge to home = standard BT → enter Cerner BT order<br>• AMA = hard stop<br>• <b>Non-VA inpatient → non-VA rehab = GAP SCENARIO → Call OCC; do NOT enter Cerner BT order</b><br><br><b>Sober living / halfway house:</b> NOT covered. Not a VA-authorized medical facility. Hard exclusion. No Cerner BT order, no BT, no VTS.<br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 U.S.C. §1703</span> <span class="auth">38 CFR 70.30</span>'},

// ══ TRANSPLANT ════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['transplant travel donor support person referring facility responsible cost coverage'],
q:'Who is responsible for transplant travel costs and what is covered?',
a:'<b>Referring Facility Responsible For:</b><br>• Round-trip transport for Veteran + one support person — for all transplant-related travel<br>• Living donor + one support person — for pre-donation, donation, and 2 years post-donation follow-up<br>• Mode of transport, parking, tolls, pre-approved en-route lodging and meals<br><br><b>VA Transplant Center (VATC) Responsible For:</b><br>• Lodging costs for Veteran/support person for all transplant-related stays (lifetime)<br>• Lodging for donor/support person for 2 years post-donation<br>• Local parking, local mileage, and additional approved costs at the transplant center<br><br><b>Meals and Lodging:</b> Reimbursed up to 50% of GSA rate. En-route lodging authorized when travel exceeds 12 hours.<br><br><b>For community (non-VA) transplant:</b> Veteran must meet standard BT eligibility; 1703 contract required; referring VA responsible.<br><br><span class="auth">38 CFR Part 70</span> <span class="auth">VHA Directive 2012-018</span> <span class="auth">VHA Transplant Travel Procedure Guide Feb 2018</span>'},

// ══ VISN 20 PRE-PAY ════════════════════════════════════════════════════════════
{tags:['visn'],keywords:['VISN 20 prepay pre-pay common carrier LEAF airfare bus OGC opinion advance purchase'],
q:'What is the VISN 20 Common Carrier Pre-Payment policy and how do I submit a LEAF request?',
a:'<b>Background:</b> Standard BT is a reimbursement program — Veterans purchase travel and VA reimburses. An April 2023 OGC opinion confirmed VA does NOT have authority to pre-pay common carrier travel. However, some Veterans cannot afford to purchase travel upfront.<br><br><b>VISN 20 Hybrid Approach (VISN 20 facilities only):</b><br>• <b>Above pension threshold:</b> Reimbursement only<br>• <b>Below pension threshold:</b> Pre-pay CONSIDERATION available — requires LEAF process, must be completed ≥1 workweek before travel<br><br><b>LEAF Process Steps:</b><br>A: Income verification → B: LEAF documentation (no PHI/PII) → C: Mobility Manager review → D: Associate Director approval → E: VISN DND (if over threshold) → F: Ticket purchase<br><br><b>2026 Pension Thresholds:</b> 0 dependents: $17,441 | 1: $22,839 | 2: $25,823 | 3: $28,807 | 4: $31,791 | add ~$2,984/additional dependent<br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 CFR Part 70</span> <span class="auth">OGC Opinion Apr 2023</span> <span class="auth">VISN 20 White Paper Updated 2/4/26</span>'
+tplBox([['leaf','💰 Open LEAF Pre-Pay Request Form'],['cc','📋 Common Carrier Order Guide']])
+'<div class="crit">Pre-payment without completing the LEAF process may constitute an Anti-Deficiency Act violation (31 U.S.C. §1341).</div>'},

// ══ SPECIAL PROGRAMS ══════════════════════════════════════════════════════════
{tags:['proc'],keywords:['PL 114-223 SCI spinal cord vision impairment amputation special rehab eligibility statutory'],
q:'What did P.L. 114-223 change about BT eligibility for Veterans with SCI, vision impairment, or multiple amputations?',
a:'<b>Effective October 1, 2016</b> (communicated March 2, 2017), P.L. 114-223 Section 250 expanded BT eligibility to Veterans with vision impairment, SCI/D, or double/multiple amputations whose travel is in connection with care at a VA special disabilities rehabilitation program, if care is provided on an <b>inpatient basis</b> or during a period of VA-provided <b>temporary lodging</b>.<br><br>This eligibility is <b>independent of standard financial eligibility criteria</b> — no income or SC rating requirement needed.<br><br><b>In Cerner:</b> Enter a standard BT order. The BT eligibility is statutory. However, if SMT is needed, a clinician must still separately document medical necessity.<br><br><span class="auth">P.L. 114-223 Section 250</span> <span class="auth">VHA 1601B.05 App. A §3(g)</span> <span class="auth">10N Policy Memo Mar 2, 2017</span>'},

{tags:['proc'],keywords:['PADRECC Parkinson disease travel cost responsibility referring facility centers'],
q:'Who pays for travel costs for Veterans referred to PADRECCs?',
a:'<b>The referring facility is responsible for ALL travel costs</b> associated with Veterans traveling to Parkinson\'s Disease Research, Education, and Clinical Centers (PADRECCs) — including VHA-sponsored clinical trials.<br><br>The six PADRECC centers: Philadelphia, Richmond, Houston, West Los Angeles, San Francisco, and a combined Portland/Seattle center.<br><br><span class="auth">10N Policy Memo Jul 31 2002</span> <span class="auth">38 U.S.C. §111</span><br><br>Contact: VHABeneficiaryTravelQuestions@va.gov'},

{tags:['proc'],keywords:['dialysis transport daily high frequency BT eligible monthly cap deductible exempt'],
q:'Can VA transport Veterans to dialysis at a non-VA VA-contracted facility?',
a:'<b>Yes</b> — provided the non-VA dialysis center is VA-authorized under 38 U.S.C. 1703 and the Veteran is BT eligible.<br><br><b>High-frequency transport (typically 3x/week):</b><br>• Each trip is a standard BT trip from residence to VA-authorized dialysis center<br>• Monthly deductible cap ($18.00 or 6 one-way trips) applies to mileage claims — after cap, remaining trips that month are deductible-free<br>• SMT trips are deductible-EXEMPT<br>• Dialysis patients often meet SMT medical necessity (AV fistulas, access sites, mobility limitations) — verify with clinician at program enrollment rather than per-trip<br><br><b>In Cerner:</b> Enter SMT order with duration covering the treatment episode. Use Uber Health Standing Order for recurring same-day/time trips (dialysis) via Common Carrier if applicable.<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.30(b)(2)</span> <span class="auth">38 CFR 70.31</span>'
+tplBox([['smt','📋 SMT / Ambulance / Wheelchair Van Order Guide'],['cc','📋 Common Carrier / Uber Order Guide']])},

{tags:['proc'],keywords:['OTP opioid treatment program methadone clinic daily transport deductible monthly cap'],
q:'What are the rules for transporting Veterans to an Opioid Treatment Program (OTP)?',
a:'OTP transport is standard BT if the OTP is VA or VA-authorized and the Veteran is BT eligible.<br><br>• OTP is covered under the medical benefits package (38 CFR 17.38)<br>• High-frequency daily transport is payable — each trip evaluated on BT eligibility<br>• Monthly deductible cap ($18.00 / 6 one-way trips) applies to mileage; SMT trips are deductible-exempt<br>• For daily transport with SMT medical necessity: verify eligibility and medical necessity at enrollment rather than per trip<br><br><b>In Cerner:</b> Enter SMT or Common Carrier order with appropriate duration. If BT NOT eligible, Veteran can still use VTS direct transport but cannot claim mileage reimbursement.<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.31(b)(1)</span>'
+tplBox([['smt','📋 SMT Order Guide'],['rt','📋 Repeat Travel Request Guide']])},

{tags:['proc'],keywords:['HRTG highly rural grant VSO state agency county 7 persons per square mile'],
q:'What is the Highly Rural Transportation Grant (HRTG) program?',
a:'HRTG provides grants to VSOs and State Veteran Service Agencies to assist Veterans in <b>highly rural areas</b> (counties with fewer than <b>7 persons per square mile</b>) with transportation to VA facilities.<br><br>• Approximately <b>$3 million</b> available annually<br>• Maximum grant: <b>$50,000 per highly rural area</b><br>• Transport provided by the GRANTEE organization — NOT through VA\'s BT SMT contract<br>• VA BT SMT contract and Cerner BT orders do NOT apply to HRTG-funded trips<br>• VTS Mobility Managers should coordinate with HRTG grantees as a community resource<br><br><span class="auth">P.L. 111-163</span> <span class="auth">38 U.S.C. §501</span> <span class="auth">VHA 1695(1) App. F §7</span>'},

// ══ BEHAVIORAL RESTRICTIONS ═══════════════════════════════════════════════════
{tags:['proc'],keywords:['BPRF behavioral patient record flag OBR order behavioral restriction deny transport VTS'],
q:'Can a Behavioral Patient Record Flag (BPRF) alone be used to deny VTS transport?',
a:'<b>No — a BPRF alone is NOT sufficient to deny VTS transport.</b><br><br>To restrict VTS transport, an <b>Order of Behavioral Restriction (OBR)</b> must be issued by the <b>VA medical facility Chief of Staff</b> following a behavioral threat assessment by the Disruptive Behavior Committee (DBC) in collaboration with the VTP Board of Directors.<br><br>BPRFs and OBRs are reviewed at least every 2 years.<br><br><span class="auth">VHA 1695(1) §5(k)(1)</span> <span class="auth">VHA 1160.08(1)</span> <span class="auth">38 CFR 17.107</span><div class="crit">An active OBR covering transportation = HARD STOP for all transport modes including contract SMT and Cerner BT orders. Contract SMT cannot override an OBR.</div>'},

// ══ CNH ═══════════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['community nursing home CNH VA authorized transport periodic appointments discharge place of stay'],
q:'What are the BT rules for Veterans in VA-authorized Community Nursing Homes (CNH)?',
a:'VA-authorized CNH under 38 U.S.C. §1720 = the Veteran\'s <b>place of stay</b> for all BT calculations.<br><br>• <b>CNH → VA for periodic appointments:</b> Standard BT — enter Cerner BT order; CNH is origin; payment cap applies from CNH, not prior residence<br>• <b>CNH → VA-authorized community specialist:</b> Standard BT — two VA authorizations needed: CNH placement (1720) + community care for specialist (1703)<br>• <b>CNH → non-VA ER (911):</b> 38 U.S.C. 1725 reimburses emergency provider — NOT a Cerner BT order<br>• <b>Non-medical transport from CNH (family visits, social passes):</b> NOT covered — no Cerner BT order<br>• <b>Discharge from CNH to home:</b> Standard BT if BT eligible — enter Cerner BT order<br>• <b>AMA discharge from CNH:</b> Hard stop — no Cerner BT order, no contract SMT<br><br><span class="auth">38 U.S.C. §1720</span> <span class="auth">38 CFR 70.30(b)(3)(5)</span>'
+tplBox([['smt','📋 SMT Order Guide'],['rt','📋 Repeat Travel Request Guide']])},

// ══ APPEALS ════════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['appeal denied BT claim administrative clinical how to appeal modernization act'],
q:'How does a Veteran appeal a denied BT claim?',
a:'When a BT claim is denied, the claimant and accredited representative must be provided <b>written notice of the decision</b>.<br><br><b>Administrative determination</b> (eligibility, timeliness, payment amount): Appeal per <b>VHA Notice 2022-05</b> (Appeals Modernization Act in VHA).<br><br><b>Clinical determination</b> (SMT medical necessity, nearest facility): File a clinical appeal per <b>VHA Directive 1041</b> (Appeal of VHA Clinical Decisions).<br><br><span class="auth">38 U.S.C. §5104</span> <span class="auth">38 U.S.C. §5103A</span> <span class="auth">VHA Notice 2022-05</span> <span class="auth">VHA Directive 1041</span>'},

// ══ NON-EMERGENT PREAUTH ═══════════════════════════════════════════════════════
{tags:['smt'],keywords:['non-emergent transport preauthorization VetRide CPT codes A0428 A0426 A0130'],
q:'What is the non-emergent transport preauthorization policy and what CPT codes require it?',
a:'<b>All non-emergent transportation must be preauthorized and initiated by the authorizing VA facility</b> before transport occurs. Only VA employees can obligate on behalf of the government.<br><br><b>CPT codes requiring preauthorization:</b><br>• A0428 — BLS Non-Emergent<br>• A0426 — ALS Non-Emergent<br>• A0130 — Wheelchair Non-Emergent<br>• A0430 — Fixed Wing Air Transport Non-Emergent<br>• A0431 — Rotary Wing Air Transport Non-Emergent<br>• T2005 — Stretcher Non-Emergent<br><br>Requests are submitted through the <b>VetRide Admin Portal</b> (Administrative Trip Requestor profile required).<br><br><span class="auth">VTP Non-Emergent Transport Policy Summary</span> <span class="auth">38 CFR Part 70</span><div class="warn">In Cerner: enter the BT order BEFORE transport occurs. Unauthorized or ineligible payments may be subject to recapture. Pre-authorization without the Cerner order process may constitute an Anti-Deficiency Act violation.</div>'
+tplBox([['smt','📋 SMT / Ambulance / Wheelchair Van Order Guide']])},

// ══ CONTACTS ═══════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['contact VTP leadership phone email questions beneficiary travel VHAMSVTPLeadership'],
q:'What are the key VTP contacts for BT and VTS questions?',
a:'<b>Veterans Transportation Program (VTP) — General Questions:</b><br>Email: VHAMSVTPLeadership@va.gov<br>Phone: 404-828-5601<br><br><b>Beneficiary Travel Questions:</b><br>Email: VHABeneficiaryTravelQuestions@va.gov<br><br><b>Community Care Information:</b><br>va.gov/COMMUNITYCARE/index.asp<br><br><b>Annual Income Thresholds:</b><br>va.gov/HEALTHBENEFITS/apps/explorer/AnnualIncomeLimits/HealthBenefits<br><br><b>Customer Satisfaction Survey (VTS):</b><br>1-855-682-4048<br><br><b>VISN 20 Pre-Pay LEAF Form:</b><br>leaf.va.gov/VISN20/496/visn20/report.php?a=TravelPrePay'
+tplBox([['leaf','💰 LEAF Pre-Pay Form']])},

// ══ VTS PRIORITY ═══════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['VTS priority order first enrolled veteran non-enrolled insufficient resources limited'],
q:'What is the priority order for VTS when resources are insufficient?',
a:'When VTS resources are insufficient, the following priority order applies:<br><br><b>1.</b> Basis for eligibility — <b>Enrolled Veterans first</b>, then: non-enrolled Veterans → Servicemembers → Family Caregivers → counseling/MH services persons → CITI beneficiaries → Guests<br><b>2.</b> First-in-time request<br><b>3.</b> Clinical need<br><b>4.</b> Inability to transport themselves<br><b>5.</b> Eligibility for other transportation services or benefits<br><b>6.</b> Availability of other transportation services<br><b>7.</b> VA facility\'s ability to maximize available resources<br><br>Any person denied VTS must be assisted in identifying and accessing other transportation options.<br><br><span class="auth">38 CFR 70.73(c)</span> <span class="auth">VHA 1695(1) §5 and §15</span>'},

// ══ FOREIGN TRAVEL ════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['foreign travel Philippines overseas FMP CHAMPVA authorized care abroad international'],
q:'Is BT covered for Veterans traveling abroad or living in the Philippines?',
a:'<b>Generally no — BT does not apply outside the United States.</b><br><br><b>Philippines:</b> Explicitly excluded per VHA Directive 1521. No BT, no Cerner BT order, no contract SMT.<br><br><b>Other foreign countries:</b> No BT payment authorized for the foreign portion of any trip.<br><br><b>Exception — U.S. portion only:</b> For Veterans traveling to the U.S. from abroad for FMP/CHAMPVA-authorized care, BT covers ONLY the in-U.S. portion (from the U.S. port of entry onward). A Cerner BT order may be entered for that in-U.S. segment if the Veteran is BT eligible.<br><br><span class="auth">38 CFR 70.2 (United States definition)</span> <span class="auth">VHA 1601B.05 App. A §12</span> <span class="auth">VHA Directive 1521</span>'},

];

// ── TEMPLATE BOX HELPER ───────────────────────────────────────────────────────
function tplBox(links){
  var inner=links.map(function(l){
    var id=l[0],label=l[1];
    if(id==='leaf'){
      return '<button class="tpl-link leaf" onclick="openMod(\'leaf\')">'+label+'</button>';
    }
    return '<button class="tpl-link" onclick="openMod(\''+id+'\')">'+label+'</button>';
  }).join('');
  return '<div class="tpl-box"><h4>Order Guides &amp; Tools</h4><div class="tpl-links">'+inner+'</div></div>';
}

// ── SEARCH ENGINE ──────────────────────────────────────────────────────────────
function tokenize(s){
  return (s||'').toLowerCase().replace(/[^a-z0-9\s]/g,' ').split(/\s+/).filter(function(w){return w.length>2;});
}
var STOP=new Set(['the','and','for','are','not','was','that','this','with','from','they','have','been','will','when','what','does','can','who','how','all','any','but','our','you','your','its','use','get']);

function score(entry,tokens){
  var hay=(entry.q+' '+entry.keywords.join(' ')+' '+entry.a).toLowerCase();
  var s=0;
  tokens.forEach(function(t){
    if(STOP.has(t))return;
    if(entry.keywords.join(' ').toLowerCase().includes(t))s+=4;
    else if(entry.q.toLowerCase().includes(t))s+=3;
    else if(hay.includes(t))s+=1;
  });
  return s;
}

function search(){
  var raw=document.getElementById('q').value.trim();
  var cardsEl=document.getElementById('cards');
  var emptyEl=document.getElementById('empty');
  var summaryEl=document.getElementById('summary');
  if(raw.length<2){
    cardsEl.innerHTML='';
    emptyEl.style.display='block';
    summaryEl.style.display='none';
    return;
  }
  var tokens=tokenize(raw);
  var scored=KB.map(function(e){return{e:e,s:score(e,tokens)};}).filter(function(x){return x.s>0;});
  scored.sort(function(a,b){return b.s-a.s;});
  var top=scored.slice(0,12);
  emptyEl.style.display='none';
  summaryEl.style.display='block';
  summaryEl.textContent=top.length+' result'+(top.length!==1?'s':'')+' for "'+raw+'"';
  cardsEl.innerHTML='';
  if(top.length===0){
    cardsEl.innerHTML='<div style="text-align:center;padding:40px;color:#546e7a"><b>No results found.</b><br><br>Try different keywords or browse the chips above.<br>Contact VHABeneficiaryTravelQuestions@va.gov for specific policy questions.</div>';
    return;
  }
  top.forEach(function(item,idx){
    var e=item.e;
    var tagClass='tag-'+e.tags[0];
    var tagLabel=e.tags[0].toUpperCase();
    var card=document.createElement('div');
    card.className='card';
    card.innerHTML='<div class="card-header" onclick="toggle(this)">'
      +'<span class="tag '+tagClass+'">'+tagLabel+'</span>'
      +'<span class="q">'+e.q+'</span>'
      +'<span class="arrow">▼</span>'
      +'</div>'
      +'<div class="card-body"><div class="answer">'+e.a+'</div></div>';
    if(idx===0)card.classList.add('open');
    cardsEl.appendChild(card);
  });
}

function toggle(header){header.parentElement.classList.toggle('open');}

function setQ(text){
  document.getElementById('q').value=text;
  search();
  document.getElementById('q').focus();
}
</script>
</body>
</html>
