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
#header p{font-size:11px;opacity:.8}
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
<div id="header">
  <h1>VA Veterans Transportation Program — Policy & Regulation Search</h1>
  <p>Covers: Beneficiary Travel (BT) · Veterans Transportation Service (VTS) · Contract SMT · 38 U.S.C. 111 · 111A · 1703 · 1720J · 1725 · 1728 · VHA 1601B.05 · VHA 1695(1) · 38 CFR Part 70 · Policy Memos · VISN 20 Pre-Pay · Transplant Travel · SMT Clinical Determinations</p>
</div>
<div id="searchbox">
  <input type="text" id="q" placeholder="Type a question or keyword — e.g. 'can we use contract transport for non-VA ER to SNF' or 'deductible waiver' or '1720J'" oninput="search()">
  <div id="hint">Try: eligibility · deductible · SMT · 1703 · 1720J · 1725 · AMA · contract transport · dialysis · transplant · drug rehab · gap scenario · VISN 20 pre-pay · PADRECC · attendant · caregiver · homeless · incarcerated · OTP · HRTG · rural · foreign travel</div>
</div>
<div id="results">
  <div id="summary" style="display:none"></div>
  <div id="cards"></div>
  <div id="empty">
    <h2>VA VTP &amp; Beneficiary Travel Policy Search</h2>
    <p>Type any question, keyword, or topic above.<br>Results are drawn from VHA Directives, 38 CFR Part 70, statutory authority, policy memoranda, and the VTP authorization matrix.</p>
    <div class="example-chips">
      <span class="chip" onclick="setQ('who is eligible for beneficiary travel')">Who is eligible for BT?</span>
      <span class="chip" onclick="setQ('deductible waiver financial hardship')">Deductible waiver</span>
      <span class="chip" onclick="setQ('special mode transportation requirements')">SMT requirements</span>
      <span class="chip" onclick="setQ('non-VA ER to SNF gap scenario')">Non-VA ER to SNF</span>
      <span class="chip" onclick="setQ('1720J suicidal crisis transport')">1720J suicide crisis</span>
      <span class="chip" onclick="setQ('AMA against medical advice transport')">AMA discharge</span>
      <span class="chip" onclick="setQ('contract transport SMT authorized')">Contract SMT rules</span>
      <span class="chip" onclick="setQ('dialysis transport daily')">Dialysis transport</span>
      <span class="chip" onclick="setQ('drug alcohol rehab transport')">Drug/alcohol rehab</span>
      <span class="chip" onclick="setQ('VISN 20 prepay common carrier')">VISN 20 pre-pay</span>
      <span class="chip" onclick="setQ('transplant travel donor')">Transplant travel</span>
      <span class="chip" onclick="setQ('PADRECC Parkinson travel cost')">PADRECC travel</span>
      <span class="chip" onclick="setQ('meals lodging pre-approval')">Meals &amp; lodging</span>
      <span class="chip" onclick="setQ('attendant caregiver eligibility')">Attendant/caregiver</span>
      <span class="chip" onclick="setQ('rural highly rural HRTG grant')">Rural/HRTG</span>
      <span class="chip" onclick="setQ('foreign travel Philippines')">Foreign travel</span>
    </div>
  </div>
</div>
<div id="footer">Reference only — verify against current VHA directives and 38 CFR Part 70 before making eligibility determinations. | VTP Leadership: VHAMSVTPLeadership@va.gov | 404-828-5601 | Compiled 2025</div>

<script>
// ── KNOWLEDGE BASE ────────────────────────────────────────────────────────────
// Each entry: { tags[], keywords[], q, a (HTML string) }
var KB = [

// ══ DEFINITIONS ══════════════════════════════════════════════════════════════
{tags:['def'],keywords:['attendant definition','aid assistance physical'],
q:'What is the definition of an Attendant for BT purposes?',
a:'<b>Attendant</b> — An individual accompanying a beneficiary who is eligible for beneficiary travel and who is medically determined to require the aid or physical assistance of another person, as determined by a VA clinician.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(a)</span><div class="ok">An attendant cannot be a VA employee. Medical necessity must be determined by a VA clinician. Attendants are deductible-exempt and mileage for shared POV travel is limited to one beneficiary amount.</div>'},

{tags:['def'],keywords:['clinician definition who can order smt special mode'],
q:'Who qualifies as a clinician for BT purposes (who can order SMT)?',
a:'<b>Clinician</b> — A Physician, Physician Assistant (PA), Nurse Practitioner (NP), Certified Nurse Practitioner (CNP), Clinical Nurse Specialist (CNS), Certified Nurse-Midwife (CNM), Psychologist, or other licensed independent practitioner acting within the scope of their practice.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(d)</span> <span class="auth">Fed. Reg. 2016-29950 eff. Jan 13 2017</span><div class="ok">Effective January 13, 2017, CNP, CNS, and CNM APRNs were added as clinicians with full practice authority to approve SMT without physician supervision, regardless of state law. Psychologists and LIPs (social workers, professional counselors) may also make SMT determinations for mental health/behavioral health conditions with a Chief of Staff Delegation Letter (expires 365 days or Jan 1 of following year).</div>'},

{tags:['def'],keywords:['special mode transportation definition ambulance ambulette wheelchair van air'],
q:'What is a Special Mode of Transportation (SMT)?',
a:'<b>Special Mode of Transportation</b> — An ambulance, ambulette, air ambulance, wheelchair van, or other mode of transportation specially designed to transport disabled persons.<br><br><b>NOT a special mode:</b> bus, subway, taxi, train, airplane, or a modified privately-owned vehicle (POV) with special adaptive equipment — even if the POV has a wheelchair lift.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(q)</span><div class="warn">A modified POV is reimbursable as standard mileage only — it cannot be invoiced as SMT. Using a modified POV rate would be an improper payment.</div>'},

{tags:['def'],keywords:['irregular discharge definition ama against medical advice'],
q:'What is an irregular discharge / AMA discharge?',
a:'<b>Irregular Discharge</b> — The release of a competent patient from a VA or VA-authorized hospital, nursing home, or domiciliary care due to: refusal, neglect, or obstruction of examination or treatment; leaving without approval of the treating health care clinician; or disorderly conduct when discharge is the appropriate disciplinary action.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(k)</span><div class="crit">An irregular/AMA discharge is a HARD STOP for all transport including BT, VTS, and contract SMT. This applies to VA facilities AND VA-authorized non-VA facilities (community care inpatient, CNH, non-VA drug/alcohol rehab, etc.). OIG has cited facilities for improper SMT payments on AMA discharges.</div>'},

{tags:['def'],keywords:['residence definition domicile seasonal'],
q:'How is "residence" defined for BT purposes?',
a:'<b>Residence</b> — A legal residence or personal domicile even if seasonal. A person may maintain more than one residence but may only have one residence at a time for purposes of determining BT benefits. A post office box or other non-residential point of delivery does NOT constitute a residence.<br><br><span class="auth">38 CFR 70.2</span> <span class="auth">VHA 1601B.05 §2(o)</span><div class="warn">A homeless Veteran\'s shelter or place of staying is treated as their current place of stay — not their residence — for BT payment calculation purposes. BT pays from place of stay, not from a prior residence.</div>'},

{tags:['def'],keywords:['unable to defray definition income pension'],
q:'What does "unable to defray" mean and who qualifies?',
a:'A Veteran is <b>unable to defray</b> travel costs if the Veteran:<br>1. Has income not exceeding the maximum annual rate of pension under 38 U.S.C. §1521<br>2. Can demonstrate that due to loss of employment or disability, income in the year of travel will not exceed that pension rate<br>3. Has a service-connected (SC) disability rating of at least 30%<br>4. Is traveling in connection with treatment of a SC disability<br><br><span class="auth">38 CFR 70.10(c)</span> <span class="auth">VHA 1601B.05 §2(s)</span>'},

{tags:['def'],keywords:['terminal condition definition life expectancy 6 months'],
q:'What is a terminal condition for BT purposes?',
a:'<b>Terminal Condition</b> — A condition resulting in a life expectancy of less than 6 months, as certified by a VA health care provider.<br><br><span class="auth">VHA 1601B.05 §2(r)</span><div class="ok">A Veteran with a terminal condition may receive BT for transport from a VA facility to a receiving facility closer to home. The deductible is waived for terminal condition transport.</div>'},

// ══ ELIGIBILITY ══════════════════════════════════════════════════════════════
{tags:['elig'],keywords:['eligible beneficiary travel who qualifies veteran sc disability pension income'],
q:'Who is eligible for Beneficiary Travel (BT) payments?',
a:'The following Veterans are eligible for BT after meeting ONE of these qualifiers:<br><br><b>(a)</b> Veteran traveling to/from VA or VA-authorized facility for treatment of a <b>service-connected (SC) disability</b> — any percent rating<br><b>(b)</b> Veteran with <b>SC rating of 30% or more</b> traveling for any condition<br><b>(c)</b> Veteran traveling for a <b>scheduled C&amp;P examination</b><br><b>(d)</b> Veteran receiving <b>VA pension under 38 U.S.C. §1521</b><br><b>(e)</b> Veteran whose <b>annual income does not exceed the maximum annual pension rate</b> under 38 U.S.C. §1521<br><b>(f)</b> Veteran traveling to obtain a <b>service dog</b> under 38 CFR §17.148 (no income/SC requirement)<br><b>(g)</b> Veterans with <b>vision impairment, SCI/D, or double/multiple amputation</b> traveling to a VA special disabilities rehab program (P.L. 114-223)<br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 CFR 70.10(a)</span> <span class="auth">VHA 1601B.05 App. A §3</span>'},

{tags:['elig'],keywords:['other persons eligible family member caregiver attendant donor non-veteran'],
q:'Who else besides Veterans is eligible for BT (non-Veterans)?',
a:'In addition to Veterans, the following persons are eligible for BT:<br><br><b>Attendants</b> — physically assisting a BT-eligible beneficiary, as medically determined by a VA clinician. Cannot be a VA employee.<br><b>Approved Family Caregivers (PCAFC)</b> — approved under 38 CFR Part 71, when accompanying the Veteran or traveling for training/counseling.<br><b>Family members (consultation)</b> — traveling for consultation, counseling, training, or MH services related to a Veteran receiving SC care.<br><b>Family members (bereavement)</b> — traveling for bereavement counseling related to death of Veteran in active duty, line of duty.<br><b>Allied Beneficiaries</b> — subject to reimbursement agreement by the foreign government concerned.<br><b>Beneficiaries of other Federal agencies</b> — subject to reimbursement agreement.<br><b>Organ donors (transplant)</b> — traveling to VA Transplant Center.<br><br><span class="auth">38 CFR 70.10(a)(7)(8)(9)(10)</span> <span class="auth">VHA 1601B.05 App. A §4</span>'},

{tags:['elig'],keywords:['vts eligibility veterans transportation service enrolled non-enrolled'],
q:'Who is eligible for Veterans Transportation Service (VTS)?',
a:'VTS eligibility is <b>broader</b> than BT eligibility. VTS is authorized for:<br><br><b>All BT-eligible persons</b> (cannot double-claim for same trip)<br><b>All enrolled Veterans</b> — for any scheduled, urgent, or unscheduled visit; medication/prosthetic pickup; or VA-determined medical events<br><b>Non-enrolled Veterans</b> — for C&amp;P exams, walk-in visits, enrollment, or VA-determined medical events<br><b>Servicemembers</b> — traveling to VA or VA-authorized facility<br><b>Prospective and approved Family Caregivers (PCAFC)</b><br><b>Attendants</b><br><b>CHAMPVA beneficiaries</b> — only when care is at a VA facility through CITI<br><b>Guests</b> — space-available, lowest priority, one per Veteran<br><b>VJO Veterans</b> — to mandated court appearances and VA/community care appointments<br><b>CWT Veterans</b> — to VA employment associated with CWT participation<br><br><span class="auth">38 U.S.C. §111A</span> <span class="auth">38 CFR 70.71</span> <span class="auth">VHA 1695(1) §5</span>'},

{tags:['elig'],keywords:['champva citi eligibility vts transport'],
q:'Are CHAMPVA beneficiaries eligible for BT or VTS?',
a:'<b>CHAMPVA beneficiaries are NOT eligible for BT</b> reimbursement. They are NOT listed as BT-eligible persons under 38 CFR 70.10.<br><br><b>CHAMPVA beneficiaries ARE eligible for VTS</b> — but ONLY when care is being provided at a VA facility through the CHAMPVA Inhouse Treatment Initiative (CITI).<br><br>CHAMPVA pays for care costs but does NOT cover transportation to that care at non-VA providers.<br><br><span class="auth">38 CFR 70.10</span> <span class="auth">38 CFR 70.71(h)</span> <span class="auth">38 CFR 17.270-17.278</span> <span class="auth">VHA 1695(1) §5(g)</span><div class="crit">No BT authority = no contract SMT authority for CHAMPVA beneficiaries. VTS direct transport only, and only for CITI care at a VA facility.</div>'},

{tags:['elig'],keywords:['incarcerated veteran eligibility vts transport'],
q:'Are incarcerated Veterans eligible for BT or VTS?',
a:'<b>No — incarcerated Veterans are explicitly excluded</b> from both BT and VTS transport.<br><br><span class="auth">VHA 1695(1) §5(k)(3)</span><div class="ok">Eligibility is restored upon release on bail or completion of the sentence. Veterans enrolled in the Veterans Justice Outreach (VJO) Program who are not incarcerated are eligible for VTS transport to mandated court appearances and VA/community care appointments associated with their VJO participation.</div>'},

{tags:['elig'],keywords:['active duty servicemember transport vts'],
q:'Are active duty Servicemembers eligible for VTS or BT?',
a:'<b>Servicemembers are eligible for VTS</b> direct transport to VA or VA-authorized facilities for VA care, C&amp;P exams, or enrollment.<br><br><b>BT reimbursement cost is DOD\'s responsibility</b> — not VA\'s. VA provides transport only when a reimbursement agreement with DOD exists (VHA Directive 1660.06).<br><br><span class="auth">38 U.S.C. §111A</span> <span class="auth">38 CFR 70.71(d)</span> <span class="auth">VHA 1695(1) §5(d)</span> <span class="auth">VHA Directive 1660.06</span><div class="crit">Do NOT use the BT SMT contract for active duty members — this misallocates BT appropriation funds. VTS direct transport only. DOD reimburses VA per the agreement.</div>'},

{tags:['elig'],keywords:['guest vts eligibility space available'],
q:'Can a guest ride with a Veteran on VTS?',
a:'<b>Yes — but only on VTS, space-available, and at the lowest priority.</b><br><br>A guest may travel with an eligible Veteran or Servicemember provided:<br>1. Resources (seats) remain available AFTER all eligible persons are served<br>2. Only ONE guest per Veteran<br>3. The guest is lowest priority and may be bumped<br><br><span class="auth">38 CFR 70.71(i)</span> <span class="auth">VHA 1695(1) §5(h)</span><div class="crit">Guests have NO BT eligibility. No contract SMT for guests under any circumstances.</div>'},

// ══ DEDUCTIBLE ═══════════════════════════════════════════════════════════════
{tags:['pay'],keywords:['deductible amount monthly cap one way round trip'],
q:'What is the BT deductible amount and monthly cap?',
a:'<b>Deductible:</b> $3.00 per one-way trip ($6.00 for a round-trip).<br><b>Monthly cap:</b> $18.00 or six one-way trips (three round-trips), whichever occurs first.<br><br>Once the $18.00 monthly cap or six one-way trips is reached in a calendar month, remaining travel for that month is <b>free of deductible charges</b>.<br><br><span class="auth">38 CFR 70.31</span> <span class="auth">VHA 1601B.05 App. A §6</span>'},

{tags:['pay'],keywords:['deductible exempt exceptions no deductible smt cp exam non-veteran attendant donor'],
q:'When does the deductible NOT apply (deductible exemptions)?',
a:'The deductible does NOT apply when:<br><br><b>(a)</b> Travel is by <b>special mode of transportation (SMT)</b><br><b>(b)</b> Travel is to a VA facility for a <b>scheduled C&amp;P examination</b><br><b>(c)</b> Travel is by a <b>non-Veteran</b><br><b>(d)</b> Travel is by an <b>attendant</b><br><b>(e)</b> Travel is by a <b>donor</b><br><b>(f)</b> The deductible would cause <b>severe financial hardship</b> (see deductible waiver)<br><br><span class="auth">38 CFR 70.31(b)</span> <span class="auth">VHA 1601B.05 App. A §6(b)</span>'},

{tags:['pay'],keywords:['deductible waiver financial hardship pension income means test'],
q:'When must the deductible be waived (financial hardship)?',
a:'The deductible <b>must</b> be waived when it would cause the Veteran severe financial hardship. Severe financial hardship occurs if the Veteran:<br><br><b>(a)</b> Is in receipt of a <b>VA pension</b>; or<br><b>(b)</b> Has income for the preceding year that does not exceed the <b>VA national means test household income threshold</b>; or<br><b>(c)</b> Can demonstrate that due to <b>loss of employment or incurrence of a disability</b>, income in the year of travel will not exceed the VA national means test threshold<br><br>Waivers are valid through the end of the calendar year or until household income changes. The Veteran must notify VA of any income change during the waiver period.<br><br><span class="auth">38 CFR 70.31(c)(d)(e)</span> <span class="auth">VHA 1601B.05 App. A §6(c)(d)</span><br><br>Current income thresholds: <b>va.gov/HEALTHBENEFITS/apps/explorer/AnnualIncomeLimits/HealthBenefits</b>'},

// ══ SMT CLINICAL DETERMINATIONS ══════════════════════════════════════════════
{tags:['smt'],keywords:['smt clinical determination documentation medical necessity requirement how to document'],
q:'What documentation is required for Special Mode Transportation (SMT) authorization?',
a:'Per the April 2016 10N Policy Memo and VTP/VA-CASE guidance:<br><br><b>Required:</b> Effective May 1, 2016, the Medical Transport Certification Reminder Dialog Template (or equivalent electronic documentation in CPRS) is required to document:<br>• Aid and Attendance/Housebound status<br>• Nearest Facility determination<br>• Special Mode Transportation/Common Carrier determination<br>• National Caregiver status<br>• Attendant and Service Dog status<br><br>The template allows clinicians to certify transportation needs for <b>up to one year forward</b>, reducing per-trip documentation burden. Approval must be by electronic signature in CPRS.<br><br><span class="auth">10N Policy Memo Apr 12 2016</span> <span class="auth">38 CFR Part 70</span> <span class="auth">VHA 1601B.05</span><br><br>Template download: <b>va.gov/vdl/application.asp?appid=60</b><br>Questions: <b>VHABeneficiaryTravelQuestions@va.gov</b>'},

{tags:['smt'],keywords:['smt clinical criteria who needs ambulance wheelchair van when appropriate medical criteria'],
q:'What are the clinical criteria for approving SMT (ambulance/wheelchair van)?',
a:'Two criteria MUST both be met:<br><b>1. BT eligibility</b> — Veteran must be administratively eligible for BT<br><b>2. Clinical medical necessity</b> — A VA clinician must determine SMT is medically required<br><br><b>Medical Criteria (Safety Focus):</b><br>The justification must confirm the claimant <b>cannot safely be transported by private vehicle, taxi, bus, train, airplane, or other common carrier</b>. Examples where SMT is appropriate:<br>• Cannot transfer into a common carrier or POV without assistance<br>• Requires restraints during transport<br>• Requires medical care during transport that an attendant cannot provide<br><br>The clinical justification must be <b>consistent with how the claimant is transported in daily life</b>.<br><br><span class="auth">38 CFR 70.10(d)</span> <span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">VTP SMT Clinical Determinations Guidance</span><div class="warn">SMT should NOT be used for convenience of the patient/family or simply because the claimant has "no other way to get in." More economical common carrier options must be considered first.</div>'},

{tags:['smt'],keywords:['psychologist lip social worker delegate smt order chief of staff delegation letter'],
q:'Can a psychologist or social worker (LIP) order SMT?',
a:'<b>Yes — with specific conditions.</b><br><br>Psychologists and Licensed Independent Practitioners (LIPs) — including social workers and professional counselors with advanced state licensure and appropriate VA privileges — may make SMT determinations specifically for <b>mental health/behavioral health conditions and functional ability determinations</b>.<br><br><b>Requirements:</b><br>• Chief of Staff must issue a <b>Justification and Delegation of Authority memorandum</b> to the Mobility Manager, naming specific clinicians, their credentials, and the conditions under which they may make SMT determinations<br>• Authority expires in <b>365 days or January 1 of the following year</b>, whichever comes first<br>• The BT program office must maintain a list of approved Psychologists and LIPs<br><br><span class="auth">VTP SMT Clinical Determinations Guidance</span> <span class="auth">38 CFR 70.2 (clinician definition)</span><div class="warn">Clinical determinations may NOT be delegated to VA staff who do not meet the clinician definition. The delegation letter must be renewed annually.</div>'},

{tags:['smt'],keywords:['aprn nurse practitioner cnp cns cnm order smt beneficiary travel'],
q:'Can APRNs (Nurse Practitioners, Clinical Nurse Specialists, Certified Nurse-Midwives) order SMT?',
a:'<b>Yes — effective January 13, 2017.</b><br><br>VA amended its medical regulations (Fed. Reg. 2016-29950, effective Jan 13, 2017) to permit full practice authority to CNP, CNS, and CNM APRNs when acting within the scope of their VA employment. These APRNs may approve Special Mode Transportation under current BT regulations <b>without clinical supervision or mandatory physician collaboration</b>, regardless of individual state practice regulations.<br><br><span class="auth">Fed. Reg. 2016-29950 (eff. Jan 13, 2017)</span> <span class="auth">VTP Announcement Jan 2017</span> <span class="auth">38 CFR 70.2</span><div class="ok">No additional regulatory amendments were needed. APRNs are included in the "other independent licensed practitioners" definition. No Chief of Staff delegation letter is required for these three APRN roles.</div>'},

{tags:['smt'],keywords:['contract smt two gates required eligibility medical necessity both'],
q:'What are the two required gates before arranging a contract SMT vendor?',
a:'Both of the following must be confirmed BEFORE a contract SMT vendor is arranged:<br><br><b>Gate 1 — BT Eligibility:</b> The Veteran must be administratively eligible for BT under 38 CFR 70.10 (SC disability, 30%+ rating, pension, income, C&amp;P exam, etc.)<br><br><b>Gate 2 — Clinician Medical Necessity:</b> A VA clinician (within their scope of practice) must determine that SMT is medically required for this transport<br><br><span class="auth">38 CFR 70.10(d)</span> <span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">VHA 1695(1) App. A §3</span> <span class="auth">VHA 1601B.05 App. A §15</span><div class="crit">The Business Office must verify BT eligibility AND medical authorization before approving any SMT vendor invoice. This is the primary OIG audit finding area for SMT improper payments.</div>'},

{tags:['smt'],keywords:['non-emergent transport preauthorization required cpt codes a0428 a0426'],
q:'What is the non-emergent transport preauthorization policy?',
a:'<b>All non-emergent transportation must be preauthorized and initiated by the authorizing VA facility</b> before transport occurs.<br><br>Only VA employees are authorized to obligate on behalf of the government. Non-VA entities cannot bind the government for BT transport costs.<br><br><b>CPT codes requiring preauthorization:</b><br>• A0428 — BLS Non-Emergent<br>• A0426 — ALS Non-Emergent<br>• A0130 — Wheelchair Non-Emergent<br>• A0430 — Fixed Wing Air Transport Non-Emergent<br>• A0431 — Rotary Wing Air Transport Non-Emergent<br>• T2005 — Stretcher Non-Emergent<br><br>Requests are submitted through the <b>VetRide Admin Portal</b> (Administrative Trip Requestor profile required).<br><br><span class="auth">VTP Non-Emergent Transport Policy Summary</span> <span class="auth">38 CFR Part 70</span><div class="warn">Unauthorized or ineligible payments may be subject to recapture. Pre-authorization without completing this process may constitute an Anti-Deficiency Act violation.</div>'},

// ══ PAYMENT PRINCIPLES ═══════════════════════════════════════════════════════
{tags:['pay'],keywords:['mileage rate common carrier payment what is paid reimbursable expenses'],
q:'What travel expenses does VA pay under BT?',
a:'VA pays the following for BT when travel expenses are actually incurred:<br><br><b>(a) Mileage/Common Carrier:</b> Per mile rate set by VA for POV use, or actual cost of most economical common carrier (bus, train, taxi, airplane). Mileage may not exceed common carrier cost unless medically necessary. Common carrier payment may not exceed POV amount unless POV is not reasonably accessible or common carrier is medically necessary.<br><b>(b) Tolls and Fares:</b> Actual cost of ferry fares, bridge tolls, road tolls, and tunnel tolls.<br><b>(c) Special Mode of Transportation:</b> Actual cost, subject to verifications.<br><b>(d) Meals and Lodging:</b> Actual cost not exceeding 50% of the government employee rate, when VA determines an overnight stay is required — and ONLY when pre-approved before booking.<br><br><span class="auth">38 CFR 70.30(a)</span> <span class="auth">VHA 1601B.05 App. A §5</span>'},

{tags:['pay'],keywords:['nearest facility payment limited nearest VA payment cap residence'],
q:'How is payment limited to the nearest appropriate facility?',
a:'BT payment is limited to travel from the beneficiary\'s <b>residence (or place of stay)</b> to the <b>nearest VA medical facility</b> where the care or services could be provided, and back.<br><br>Payment may be made to the nearest <b>non-VA facility</b> if a VA clinician determines it is necessary to obtain care at a non-VA facility.<br><br>If a beneficiary is staying somewhere other than their residence (e.g., nursing home, CNH, non-VA inpatient), that location is their <b>place of stay</b> and serves as the payment origin — but the cap still cannot exceed what would be paid from that location to the nearest appropriate facility.<br><br><span class="auth">38 CFR 70.30(b)(1)(2)(3)</span> <span class="auth">VHA 1601B.05 App. A §5(c)</span><div class="warn">If a Veteran from Detroit is treated in Baltimore, payment for the return trip is capped at the Detroit-area nearest VA distance — not the Baltimore-to-Detroit distance.</div>'},

{tags:['pay'],keywords:['meals lodging pre-approval required overnight stay reimbursement'],
q:'What are the rules for meals and lodging reimbursement?',
a:'VA may reimburse actual cost of meals and/or lodging up to <b>50% of the government employee per diem rate</b> when VA determines an overnight stay is required.<br><br><b>Factors considered:</b><br>• Distance the Veteran must travel<br>• Time of day the appointment is scheduled<br>• Weather or congestion conditions<br>• The Veteran\'s medical condition and its impact on ability to travel<br><br><b>⚠ PRE-APPROVAL IS MANDATORY — hardest requirement in BT:</b><br>The Veteran must apply for and receive approval BEFORE obtaining the meals and/or lodging. Booking a hotel before approval = claim denied, no exceptions.<br><br><span class="auth">38 CFR 70.30(a)(3)</span> <span class="auth">38 CFR 70.20(d)</span> <span class="auth">VHA 1601B.05 App. A §1(d) and §5(a)(4)</span><div class="crit">This is the single most common reason for lodging claim denial. Pre-approval must precede the stay. There are no exceptions.</div>'},

{tags:['pay'],keywords:['one-way return trip unscheduled walk-in round trip approval'],
q:'When is round-trip BT payment approved vs. one-way only?',
a:'<b>Round-trip approved when:</b><br>• Travel was in connection with care <b>scheduled with VHA prior to arrival</b>; OR<br>• Travel was for <b>emergency treatment</b><br><br><b>One-way (return trip only) when:</b><br>• Travel was NOT scheduled with VHA prior to arrival AND was not emergency treatment — VA will approve the <b>return trip only if VHA actually provided care or services</b><br><br><b>Round-trip denied when:</b><br>• Travel was not scheduled, not emergency, AND VHA did NOT provide care<br><br><span class="auth">38 CFR 70.4(b)(c)</span> <span class="auth">VHA 1601B.05 App. A §8(b)(c)</span>'},

{tags:['pay'],keywords:['apply 30 days deadline file claim beneficiary travel application time limit'],
q:'What is the deadline to apply for BT reimbursement?',
a:'A claimant must apply for BT within <b>30 calendar days</b> after completing beneficiary travel that does not include special mode transportation.<br><br>For travel including SMT: must apply AND obtain VA clinician approval <b>prior to travel</b>. If prior approval was not obtained, the application is considered timely only if submitted within 30 days AND travel was for emergency treatment.<br><br>For meals/lodging: must apply and receive approval <b>before</b> obtaining meals and/or lodging.<br><br><b>Exception:</b> If a person becomes eligible after travel occurs, they may apply within 30 days of becoming eligible.<br><br><span class="auth">38 CFR 70.20(b)(c)(d)(f)</span> <span class="auth">VHA 1601B.05 App. A §1(b)(c)(d)(f)</span>'},

// ══ EMERGENCY AUTHORITIES ════════════════════════════════════════════════════
{tags:['stat'],keywords:['1725 emergency reimbursement non-VA facility non-SC enrolled veteran'],
q:'What is 38 U.S.C. 1725 and when does it apply?',
a:'<b>38 U.S.C. 1725 — Reimbursement for Emergency Treatment (non-SC conditions)</b><br><br>The Secretary SHALL reimburse a Veteran for emergency treatment at a non-Department facility. Eligibility requires ALL of:<br>1. Veteran is <b>enrolled</b> in VA health care<br>2. Veteran received VA care within the <b>preceding 24 months</b><br>3. Veteran is <b>personally financially liable</b> to the provider<br>4. Veteran has <b>no entitlement</b> to care under a health-plan contract<br>5. No other contractual or legal recourse against a third party<br>6. VA/Federal facilities were <b>not feasibly available</b><br><br>Emergency treatment means: care when delay would be hazardous to life or health; until the Veteran can safely be transferred to a VA/Federal facility.<br><br><span class="auth">38 U.S.C. §1725</span> <span class="auth">38 CFR 17.1000-17.1008</span><div class="crit">1725 is a REIMBURSEMENT authority — it reimburses the Veteran or provider AFTER the fact. It does NOT pre-authorize a VA-arranged contract transport. Pre-arranged contract SMT and emergency 911 response are mutually exclusive. BT explicitly excludes non-SC emergency transport at non-VA facilities covered by 1725 (38 CFR 70.30(e)).</div>'},

{tags:['stat'],keywords:['1728 emergency reimbursement SC service connected condition travel incidental expenses'],
q:'What is 38 U.S.C. 1728 and how does it differ from 1725?',
a:'<b>38 U.S.C. 1728 — Reimbursement of Certain Medical Expenses (SC conditions)</b><br><br>1728 reimburses emergency treatment for <b>service-connected conditions</b> including <b>travel and incidental expenses</b>. Applies when the Veteran paid for emergency treatment from sources other than VA, for:<br>• An adjudicated SC disability<br>• A non-SC disability aggravating an SC disability<br>• Any disability of a Veteran with total permanent SC disability<br>• Illness/injury of a Veteran in a vocational rehabilitation program<br><br><b>Key difference from 1725:</b><br>• <b>1725</b> = non-SC conditions; requires no other health insurance; requires enrolled + 24-month VA care<br>• <b>1728</b> = SC conditions; covers travel and incidental expenses in addition to medical costs<br><br><span class="auth">38 U.S.C. §1728</span> <span class="auth">38 CFR 17.120</span><div class="warn">Like 1725, 1728 is a REIMBURSEMENT authority — not a pre-authorization for VA-arranged contract transport.</div>'},

{tags:['stat'],keywords:['1720J suicidal crisis emergent suicide care transport payment who pays'],
q:'What is 38 U.S.C. 1720J and who pays for transport under it?',
a:'<b>38 U.S.C. 1720J — Emergent Suicide Care</b><br><br>The Secretary SHALL:<br>• Furnish emergent suicide care at a VA facility<br>• Pay for emergent suicide care at a non-VA facility<br>• Reimburse the eligible individual for emergent suicide care at a non-VA facility<br>• Pay costs of emergency transportation<br><br><b>Eligibility:</b> Any individual in acute suicidal crisis who is a Veteran (38 U.S.C. §101) or qualifies under 38 U.S.C. §1720I(b). <b>No enrollment, income, or SC requirement.</b><br><br><b>Period of care:</b> Up to 30 days inpatient/residential; or up to 90 days outpatient if inpatient unavailable. May be extended.<br><br><b>Notification:</b> Individual must notify VA within 7 days of non-VA admission.<br><br><span class="auth">38 U.S.C. §1720J</span> <span class="auth">38 CFR 17.1200-17.1225</span><div class="crit">1720J has its OWN appropriation and payment stream — separate from the BT fund. Using a BT-funded SMT contract for a 1720J transport = improper use of BT appropriation. OCC and the Suicide Prevention Coordinator administer 1720J payments through eCAMS (POM processes 1728 and 1725; BT MM processes 1703).</div>'},

{tags:['stat'],keywords:['1703 community care contracts non-VA non-department facility geographic inaccessibility'],
q:'What is 38 U.S.C. 1703 and when does it authorize non-VA care?',
a:'<b>38 U.S.C. 1703 — Contracts for Hospital Care and Medical Services in Non-Department Facilities</b><br><br>When VA facilities are not capable of furnishing economical hospital care or medical services because of <b>geographical inaccessibility</b> or <b>inability to furnish the required care</b>, the Secretary may contract with non-VA facilities to furnish:<br>• Care for SC disabilities<br>• Medical services for eligible Veterans who cannot be appropriately treated at VA<br>• Emergency care posing serious threat to life or health (until safe transfer to VA)<br>• Hospital care for women Veterans<br>• Care in non-contiguous States (excluding Puerto Rico)<br><br><span class="auth">38 U.S.C. §1703</span> <span class="auth">38 CFR Part 17</span><div class="crit">1703 is the gate for all non-VA to non-VA transport scenarios. A 1703 community care authorization for the CARE does not automatically authorize transport between two non-VA facilities — OCC must separately authorize the transport. Two separate authorizations are always required: one for the care, one for the transport.</div>'},

// ══ EMERGENCY PAYMENT PROCESSING ═════════════════════════════════════════════
{tags:['proc'],keywords:['ecams processing 1703 1725 1728 occ 72 hours who processes payment pathway'],
q:'How are emergency transport payments processed through eCAMS? Which authority applies?',
a:'For 911/ER emergencies and approved non-VA ER-to-ER transfers, <b>OCC through eCAMS</b> determines the applicable payment authority:<br><br><b>38 U.S.C. 1703</b> — If reported within <b>72 hours</b>; BT eligibility IS required<br><b>38 U.S.C. 1725</b> — If Veteran is NOT BT eligible; BT eligibility NOT required<br><b>38 U.S.C. 1728</b> — If Veteran IS BT eligible (SC condition); BT eligibility IS required<br><br><b>Processing pathways:</b><br>• <b>1703</b> → processed for payment by local BT Mobility Manager (MM) through eCAMS<br>• <b>1725 and 1728</b> → processed for payment by Program Office Manager (POM) through eCAMS<br>• <b>1720J</b> → processed for payment by POM through eCAMS (separate appropriation)<br><br><span class="auth">Transportation Arrangement and Payment Responsibility 2023</span> <span class="auth">38 U.S.C. §§1703, 1725, 1728, 1720J</span>'},

// ══ GAP SCENARIOS ════════════════════════════════════════════════════════════
{tags:['gap'],keywords:['non-VA ER to SNF skilled nursing facility transport who pays gap'],
q:'Can VA pay for transport from a non-VA ER to a non-VA SNF?',
a:'<b>This is the most critical gap scenario.</b> Standard BT/VTS cannot authorize non-VA to non-VA transport.<br><br><b>Transport is ONLY authorized if ALL of the following are met:</b><br>1. VA Office of Community Care (OCC) authorizes the SNF placement under 38 U.S.C. 1703<br>2. OCC separately authorizes transport between the non-VA ER and the non-VA SNF<br>3. BOTH facilities are VA-authorized<br><br>The fact that VA paid for the non-VA ER care under 1725 or 1728 does NOT automatically extend BT authority to the SNF transfer.<br><br><span class="auth">38 CFR 70.30(b)(1)(2)</span> <span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">VHA 1601B.05 App. A §5(c)(9)(c)</span><div class="crit">Do NOT use BT SMT contract for this scenario. This is the most commonly cited OIG improper payment scenario. Call OCC immediately when this situation arises.</div>'},

{tags:['gap'],keywords:['non-VA ER to non-VA inpatient transfer transport gap authorized'],
q:'Can VA pay for transport from a non-VA ER to a non-VA inpatient facility?',
a:'<b>Not through standard BT/VTS.</b> This requires OCC authorization through 38 U.S.C. 1703.<br><br><b>Transport is ONLY authorized if ALL of the following are met:</b><br>1. OCC has an active 1703 authorization for the non-VA inpatient admission specifically<br>2. OCC separately authorizes transport between the non-VA ER and the non-VA inpatient facility<br>3. BOTH facilities are VA-authorized<br><br>Note: If the transfer is for a suicidal crisis, 38 U.S.C. 1720J may be the applicable authority instead of 1703 — consult Suicide Prevention Coordinator and OCC.<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">The 1703 authorization for the inpatient stay does NOT automatically authorize transport. OCC must separately authorize the transport between the two non-VA facilities.</div>'},

{tags:['gap'],keywords:['non-VA inpatient to non-VA SNF rehab transport gap authorized OCC'],
q:'Can VA pay for transport from a non-VA inpatient facility to a non-VA SNF or rehab facility?',
a:'<b>Not through standard BT/VTS.</b> This requires a NEW, separate OCC authorization for each receiving facility.<br><br><b>Transport is ONLY authorized if ALL of the following are met:</b><br>1. OCC has an active 1703 authorization for the non-VA inpatient stay<br>2. OCC separately obtains a NEW 1703 authorization for the non-VA SNF/rehab admission<br>3. OCC separately authorizes transport between the two non-VA facilities<br>4. ALL facilities are individually VA-authorized<br><br><b>A single community care authorization does NOT cover the step-down transfer or the new facility.</b> Each step in the post-acute chain requires its own independent OCC authorization.<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">The inpatient 1703 authorization does NOT carry over to the SNF/rehab. OCC must open a fresh authorization for each new facility AND authorize the transport separately.</div>'},

{tags:['gap'],keywords:['non-VA ER to non-VA inpatient rehab IRF transport gap'],
q:'Can VA pay for transport from a non-VA ER to a non-VA Inpatient Rehabilitation Facility (IRF)?',
a:'<b>Not through standard BT/VTS.</b> IRF admissions require additional clinical criteria beyond standard inpatient care.<br><br><b>Transport is ONLY authorized if ALL of the following are met:</b><br>1. OCC has an active 1703 authorization for the non-VA IRF admission<br>2. OCC separately authorizes transport between the non-VA ER and the non-VA IRF<br>3. BOTH facilities are VA-authorized under 1703<br>4. IRF level of care is clinically justified (typically 3 hours/day of therapy, rehabilitation potential)<br><br><b>Note:</b> A generic inpatient authorization does NOT cover IRF level of care — OCC must specifically authorize IRF.<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">IRF criteria are strict. OCC must authorize IRF level of care specifically. Call OCC — do not use BT SMT contract.</div>'},

{tags:['gap'],keywords:['non-VA ER to non-VA LTAC long term acute care transport gap'],
q:'Can VA pay for transport from a non-VA ER to a non-VA Long-Term Acute Care (LTAC) facility?',
a:'<b>Not through standard BT/VTS.</b> LTAC facilities provide higher acuity care than SNFs and require specific clinical justification.<br><br><b>Transport is ONLY authorized if ALL of the following are met:</b><br>1. OCC has an active 1703 authorization for the non-VA LTAC admission<br>2. OCC separately authorizes transport between the non-VA ER and the non-VA LTAC<br>3. BOTH facilities are VA-authorized under 1703<br>4. LTAC level of care is clinically justified (mechanical ventilation, complex wound care, etc.)<br><br>A generic inpatient authorization does NOT cover LTAC — OCC must specifically authorize LTAC level of care.<br><br><span class="auth">38 U.S.C. §1703(a)</span> <span class="auth">38 CFR 70.30(b)(1)(2)</span><div class="crit">Call OCC. Do not use BT SMT contract for this scenario.</div>'},

{tags:['gap'],keywords:['non-VA SNF discharge to home transport BT authorized place of stay'],
q:'When a Veteran is discharged from a VA-authorized non-VA SNF, is transport home covered by BT?',
a:'<b>Yes — discharge from a VA-authorized non-VA SNF to the Veteran\'s residence IS covered by standard BT</b>, provided the Veteran is BT eligible.<br><br>The VA-authorized non-VA SNF is treated as the Veteran\'s <b>place of stay</b> for BT purposes. Discharge to the Veteran\'s residence = standard BT trip from place of stay to residence.<br><br>Contract SMT is authorized if the Veteran is BT eligible and SMT is medically required for the discharge transport (common given patient medical condition).<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.30(b)(1)(3)</span> <span class="auth">VHA 1601B.05 App. A §5(c)</span><div class="ok">Payment cap applies from the non-VA SNF location, not from the Veteran\'s prior permanent residence. This is one of the few non-VA chain steps that resolves to standard BT.</div>'},

// ══ DRUG / ALCOHOL REHAB ═════════════════════════════════════════════════════
{tags:['proc'],keywords:['drug alcohol rehab transport SATP substance abuse treatment program VA non-VA'],
q:'What are the BT/VTS rules for drug and alcohol rehabilitation transport?',
a:'<b>VA SATP (VA-operated Substance Abuse Treatment Program):</b><br>• Transport from home to VA SATP (admission or outpatient) = standard BT if Veteran is BT eligible<br>• VA SATP residential = Veteran\'s place of stay for BT purposes during the program<br>• Discharge from VA SATP to home = standard BT trip<br>• AMA from VA SATP = hard stop, no BT or contract SMT<br>• VA inpatient → VA SATP = standard inter-facility transfer (VHA Directive 1094)<br><br><b>Non-VA Drug/Alcohol Rehab (VA-authorized under 1703):</b><br>• Transport from home to non-VA rehab = standard BT if Veteran is BT eligible and facility is VA-authorized<br>• Non-VA rehab residential = place of stay for BT purposes<br>• Discharge to home = standard BT<br>• AMA = hard stop<br>• Non-VA inpatient → non-VA rehab = GAP SCENARIO — requires separate OCC 1703 authorization<br><br><b>Sober living / halfway house:</b> NOT covered under any BT authority. Not a VA-authorized medical facility. Hard exclusion.<br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 U.S.C. §1703</span> <span class="auth">38 CFR 70.30</span> <span class="auth">VHA 1601B.05 App. A §5</span>'},

// ══ TRANSPLANT ════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['transplant travel procedure guide donor support person referring facility responsible'],
q:'Who is responsible for transplant travel costs and what is covered?',
a:'<b>Referral Facility Responsible For:</b><br>• All round-trip transportation costs for the Veteran AND one support person — for pre-transplant evaluations, transplant episode, and post-transplant follow-up<br>• Living donor AND one support person — for pre-donation evaluation, donation episode, and post-donation follow-up for 2 years<br>• Mode of transport, parking, tolls, pre-approved lodging and meals en route<br><br><b>VA Transplant Center (VATC) Responsible For:</b><br>• Lodging costs for Veteran and support person for all transplant-related stays (lifetime)<br>• Lodging for living donor/support person for 2 years post-donation<br>• Local parking, local mileage, and additional approved costs<br><br><b>Meals and Lodging:</b> Reimbursed at actual cost up to 50% of GSA rate. En-route lodging authorized when travel exceeds 12 hours.<br><br><b>For community (non-VA) transplant:</b> Veteran must meet standard BT eligibility; 1703 contract required; referring VA responsible.<br><br><span class="auth">38 CFR Part 70</span> <span class="auth">VHA Directive 2012-018</span> <span class="auth">VHA Transplant Travel Procedure Guide Feb 2018</span>'},

{tags:['proc'],keywords:['PADRECC Parkinson disease travel cost responsibility referring facility'],
q:'Who pays for travel costs for Veterans referred to PADRECCs (Parkinson\'s Disease centers)?',
a:'<b>The referring facility is responsible for all travel costs</b> associated with travel of Veterans to Parkinson\'s Disease Research, Education, and Clinical Centers (PADRECCs).<br><br>This responsibility extends to all services provided by the PADRECCs, including VHA-sponsored clinical trials.<br><br>The six PADRECC centers are located at: Philadelphia, Richmond, Houston, West Los Angeles, San Francisco, and a combined Portland/Seattle center.<br><br><span class="auth">10N Policy Memo Jul 31 2002</span> <span class="auth">38 U.S.C. §111</span><br><br>Contact: Dr. John Booss, National Director for Neurology | VHABeneficiaryTravelQuestions@va.gov'},

// ══ SPECIAL PROGRAMS ═════════════════════════════════════════════════════════
{tags:['proc'],keywords:['PL 114-223 special disabilities SCI spinal cord vision impairment amputation eligibility'],
q:'What did P.L. 114-223 change about BT eligibility for Veterans with SCI, vision impairment, or multiple amputations?',
a:'<b>Effective October 1, 2016</b>, Section 250 of Public Law 114-223 expanded BT eligibility to Veterans with:<br>• Vision impairment<br>• Spinal cord injury or disorder (SCI/D)<br>• Double or multiple amputations<br><br>...whose travel is in connection with care provided through a <b>VA special disabilities rehabilitation program</b> (including SCI centers, blind rehabilitation centers, and prosthetics rehabilitation centers), if care is provided:<br>• On an <b>inpatient basis</b>; OR<br>• During a period in which VA provides the Veteran with <b>temporary lodging</b> at a VA medical facility<br><br>This expanded eligibility is INDEPENDENT of standard financial eligibility criteria (no income or SC rating requirement needed).<br><br><span class="auth">P.L. 114-223 Section 250</span> <span class="auth">VHA 1601B.05 App. A §3(g)</span> <span class="auth">10N Policy Memo Mar 2, 2017</span><div class="ok">SMT medical necessity must still be clinician-documented even though BT eligibility is statutory for these Veterans.</div>'},

{tags:['proc'],keywords:['dialysis transport daily high frequency BT eligible monthly cap deductible'],
q:'Can VA transport Veterans to dialysis at a non-VA VA-contracted facility?',
a:'<b>Yes</b> — provided the non-VA dialysis center is VA-authorized under 38 U.S.C. 1703 community care and the Veteran is BT eligible.<br><br>High-frequency (typically 3x/week) BT trips to VA-contracted dialysis = standard BT from residence to VA-authorized dialysis center.<br><br><b>Monthly deductible cap applies:</b> $18.00 or 6 one-way trips per month, whichever occurs first. After that, remaining trips are deductible-free for that month.<br><br>Dialysis patients often meet SMT medical necessity due to AV fistulas, access sites, and mobility limitations — <b>verify with clinician at enrollment</b> rather than per-trip.<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.30(b)(2)</span> <span class="auth">38 CFR 70.31</span>'},

{tags:['proc'],keywords:['OTP opioid treatment program methadone clinic daily transport deductible'],
q:'What are the rules for transporting Veterans to an Opioid Treatment Program (OTP)?',
a:'OTP transport is covered under standard BT if the OTP is VA or VA-authorized and the Veteran is BT eligible.<br><br><b>Key points:</b><br>• OTP is covered under the medical benefits package (38 CFR 17.38)<br>• High-frequency daily transport is payable — each trip evaluated on BT eligibility<br>• <b>Monthly deductible cap ($18.00 / 6 one-way trips)</b> applies to mileage claims<br>• SMT trips are deductible-exempt<br>• For daily transport with SMT medical necessity, verify eligibility and medical necessity at program enrollment rather than per trip<br><br><span class="auth">38 CFR 70.30(a)(4)</span> <span class="auth">38 CFR 70.31(b)(1)</span> <span class="auth">38 CFR 17.38</span>'},

{tags:['proc'],keywords:['HRTG highly rural transportation grant VSO state agency county'],
q:'What is the Highly Rural Transportation Grant (HRTG) program?',
a:'The <b>HRTG</b> provides grants to Veteran Service Organizations (VSOs) and State Veteran Service Agencies to assist Veterans in <b>highly rural areas</b> (counties with fewer than <b>7 persons per square mile</b>) with innovative transportation services to VA facilities.<br><br>• Approximately <b>$3 million</b> available annually<br>• Maximum grant: <b>$50,000 per highly rural area</b><br>• Transport is provided by the GRANTEE organization — NOT through VA\'s BT SMT contract<br>• VA BT SMT contract authority does NOT apply to HRTG-funded trips<br>• VTS Mobility Managers should coordinate with HRTG grantees as a community resource<br><br><span class="auth">P.L. 111-163</span> <span class="auth">38 U.S.C. §501</span> <span class="auth">VHA 1695(1) App. F §7</span>'},

{tags:['proc'],keywords:['homeless veteran shelter transport BT VTS pickup place of stay'],
q:'Can VA transport homeless Veterans? What are the rules?',
a:'<b>VTS can transport homeless Veterans</b> for health care access and enrollment purposes.<br><br>VTS will transport enrolled homeless Veterans to:<br>• Health care appointments<br>• VA appointments directly related to housing or CWT participation<br><br>VTS will NOT transport Veterans to:<br>• HUD or local housing authority appointments<br>• Non-VA employment (Supportive Employment Program participants)<br><br>For BT purposes: A shelter or temporary lodging where the homeless Veteran is staying = their <b>place of stay</b> (origin for BT payment calculations).<br><br>For <b>contract SMT</b>: The Veteran must separately be verified as BT eligible. VTS is available regardless of BT status; contract SMT requires BT eligibility + SMT medical necessity.<br><br><span class="auth">38 U.S.C. §111A</span> <span class="auth">VHA 1695(1) App. C §2</span> <span class="auth">38 CFR 70.30(b)(3)</span>'},

// ══ VISN 20 PRE-PAY ═══════════════════════════════════════════════════════════
{tags:['visn'],keywords:['VISN 20 prepay pre-pay common carrier airfare bus advance purchase OGC opinion'],
q:'What is the VISN 20 Common Carrier Pre-Payment policy and why does it exist?',
a:'<b>Background:</b> Under 38 U.S.C. §111 and 38 CFR Part 70, BT is a reimbursement program — the Veteran purchases travel and VA reimburses after care is received. An April 2023 OGC informal opinion confirmed VA does NOT have authority to pre-pay or advance purchase common carrier travel (airfare, bus, train, rideshare/taxi).<br><br><b>The Problem:</b> Some Veterans cannot afford to purchase their own common carrier transportation and file for reimbursement — particularly transplant and RRTP patients.<br><br><b>VISN 20 Hybrid Approach (applied to VISN 20 facilities only):</b><br>• <b>Above pension threshold:</b> Reimbursement only (no pre-pay)<br>• <b>Below pension threshold:</b> Pre-pay CONSIDERATION available — not an entitlement, requires individual review and documented approval through the LEAF process<br><br><b>This process may be paused, amended, or concluded at any point at the request of VISN leadership.</b><br><br><span class="auth">38 U.S.C. §111</span> <span class="auth">38 CFR Part 70</span> <span class="auth">OGC Opinion Apr 2023</span> <span class="auth">VISN 20 White Paper Updated 2/4/26</span><div class="warn">Pre-payment without completing the LEAF process may constitute an Anti-Deficiency Act violation (31 U.S.C. §1341).</div>'},

{tags:['visn'],keywords:['VISN 20 LEAF process steps pension threshold income 2026 approval workflow'],
q:'What is the VISN 20 LEAF pre-pay approval process?',
a:'The LEAF process must be completed <b>no less than 1 workweek prior to travel</b> for each individual episode of pre-pay common carrier travel.<br><br><b>Step A — Care Team:</b> Verify Veteran\'s combined earned and unearned income does not exceed the 2026 maximum annual pension rate<br><b>Step B — LEAF Documentation:</b> Document: request naming (Lastname – Appt date), attestation that travel was discussed with Veteran, attestation of clear inability to pay, summary of need, justification of financial hardship (no PHI/PII)<br><b>Step C — Mobility Manager/VTP Staff:</b> Verify travel eligibility, justification, income in Enrollment System → Approval or Disapproval<br><b>Step D — Associate Director Approval:</b> Approves for Veterans below pension threshold; submits to VISN DND for Veterans over threshold<br><b>Step E — VISN DND (if over threshold):</b> Reviews and approves all over-threshold requests<br><b>Step F — Ticket Purchase:</b> Mobility Manager/VTP staff purchases ticket<br><br><span class="auth">VISN 20 White Paper Updated 2/4/26</span>'},

{tags:['visn'],keywords:['2026 pension income threshold amounts VISN 20 dependents'],
q:'What are the 2026 pension income thresholds for VISN 20 BT eligibility?',
a:'<b>2026 Maximum Annual Pension Rate Thresholds (38 CFR 70.10(c)(1)(2)):</b><br><br>0 dependents: $17,441 | 1 dependent: $22,839 | 2 dependents: $25,823 | 3 dependents: $28,807 | 4 dependents: $31,791 | 5 dependents: $34,775 | 6 dependents: $37,759 | 7 dependents: $40,743 | 8 dependents: $43,727 | 9 dependents: $46,711 | 10+ dependents: add $2,984 per additional dependent<br><br><b>Note:</b> Aid &amp; Attendance (A&amp;A) and Housebound (HB) pension recipients may qualify at higher thresholds if a VA provider has documented they meet 38 CFR 3.351/3.352 criteria.<br><br><span class="auth">VISN 20 White Paper Updated 2/4/26</span> <span class="auth">38 CFR 70.10(c)(1)(2)</span><br><br>Current thresholds: <b>va.gov/HEALTHBENEFITS/apps/explorer/AnnualIncomeLimits/HealthBenefits</b>'},

// ══ BEHAVIORAL RESTRICTIONS ═══════════════════════════════════════════════════
{tags:['proc'],keywords:['BPRF behavioral patient record flag OBR order behavioral restriction deny transport'],
q:'Can a Behavioral Patient Record Flag (BPRF) alone be used to deny VTS transport?',
a:'<b>No — a BPRF alone is NOT sufficient to deny VTS transport.</b><br><br>The BPRF is informational — it indicates behavioral risks but does not by itself restrict services.<br><br>To restrict VTS transport, an <b>Order of Behavioral Restriction (OBR)</b> must be issued by the <b>VA medical facility Chief of Staff</b> following:<br>• A behavioral threat assessment by the VA medical facility Disruptive Behavior Committee (DBC)<br>• Collaboration with the VTP Board of Directors<br><br>The OBR must specifically address transportation safety and the resulting restrictions. BPRFs and OBRs are reviewed at least every 2 years.<br><br><span class="auth">VHA 1695(1) §5(k)(1)</span> <span class="auth">VHA 1160.08(1)</span> <span class="auth">38 CFR 17.107</span><div class="crit">An active OBR covering transportation is a HARD STOP for all transport modes including contract SMT. Contract SMT cannot override an OBR.</div>'},

// ══ FOREIGN TRAVEL ════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['foreign travel Philippines overseas FMP CHAMPVA authorized care abroad'],
q:'Is BT covered for Veterans traveling abroad or living in the Philippines?',
a:'<b>Generally no — BT does not apply outside the United States.</b><br><br><b>Philippines:</b> Travel in the Philippines is NOT a VA covered health care benefit per VHA Directive 1521. Standard BT travel in the Philippines is explicitly excluded.<br><br><b>Other foreign countries:</b> No BT travel payment is authorized when a Veteran residing in a foreign country travels to the U.S. for authorized VA care.<br><br><b>Exception — U.S. portion only:</b> For Veterans who travel to the U.S. from abroad for FMP/CHAMPVA-authorized care, BT covers ONLY the in-U.S. portion (from the U.S. port of entry onward to the VA facility).<br><br>Foreign medical care is authorized through the VHA Foreign Medical Program (FMP) or CHAMPVA — both administered by VHA Office of Community Care, Denver, CO.<br><br><span class="auth">38 CFR 70.2 (United States definition)</span> <span class="auth">VHA 1601B.05 App. A §12</span> <span class="auth">VHA Directive 1521</span>'},

// ══ APPEALS ═══════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['appeal denied BT claim administrative clinical how to appeal'],
q:'How does a Veteran appeal a denied BT claim?',
a:'When a BT claim is denied, the claimant and accredited representative must be provided <b>written notice of the decision</b>.<br><br><b>Administrative determination (e.g., eligibility, timeliness, payment amount):</b><br>File an appeal in accordance with <b>VHA Notice 2022-05</b> (Appeals Modernization Act in the Veterans Health Administration).<br><br><b>Clinical determination (e.g., SMT medical necessity, nearest facility determination):</b><br>File a clinical appeal in accordance with <b>VHA Directive 1041</b> (Appeal of VHA Clinical Decisions).<br><br><span class="auth">38 U.S.C. §5104</span> <span class="auth">38 U.S.C. §5103A</span> <span class="auth">VHA Notice 2022-05</span> <span class="auth">VHA Directive 1041</span>'},

// ══ FALSE STATEMENTS / FRAUD ══════════════════════════════════════════════════
{tags:['deny'],keywords:['false statement fraud BT claim prosecution recapture overpayment'],
q:'What happens if a Veteran makes a false statement to obtain BT payment?',
a:'Persons who make false statements for the purpose of obtaining BT travel payments are subject to <b>prosecution under 18 U.S.C. §1001</b>.<br><br>The VA Chief, Business Office must take appropriate action to <b>recapture any fraudulent payments</b> under applicable law and VA regulations.<br><br>Payments made to persons ineligible for such payment are subject to recapture under <b>38 CFR §§1.900–1.953</b>.<br><br><span class="auth">18 U.S.C. §1001</span> <span class="auth">38 CFR 70.42</span> <span class="auth">VHA 1601B.05 App. A §9</span>'},

// ══ CONTACTS ═════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['contact VTP leadership phone email questions beneficiary travel'],
q:'What are the key VTP contacts for BT and VTS questions?',
a:'<b>Veterans Transportation Program (VTP) — General Questions:</b><br>Email: VHAMSVTPLeadership@va.gov<br>Phone: 404-828-5601<br><br><b>Beneficiary Travel Questions:</b><br>Email: VHABeneficiaryTravelQuestions@va.gov<br><br><b>Community Care Information:</b><br>va.gov/COMMUNITYCARE/index.asp<br><br><b>Annual Income Thresholds:</b><br>va.gov/HEALTHBENEFITS/apps/explorer/AnnualIncomeLimits/HealthBenefits<br><br><b>Customer Satisfaction Survey (VTS):</b><br>1-855-682-4048<br><br><span class="auth">VHA 1601B.05 §4</span> <span class="auth">VHA 1695(1) §4</span>'},

// ══ COMMUNITY NURSING HOME ════════════════════════════════════════════════════
{tags:['proc'],keywords:['community nursing home CNH VA authorized transport periodic appointments discharge'],
q:'What are the BT rules for Veterans in VA-authorized Community Nursing Homes (CNH)?',
a:'A VA-authorized CNH under 38 U.S.C. §1720 is the Veteran\'s <b>place of stay</b> for all BT calculations.<br><br><b>Transport from CNH to VA for periodic appointments:</b> Standard BT — CNH is the origin. Contract SMT authorized if BT eligible and SMT medically required. Payment cap applies from CNH, not prior residence.<br><br><b>Transport from CNH to VA-authorized community specialist:</b> Standard BT — two VA authorizations needed: CNH placement (1720) and community care for the specialist visit (1703).<br><br><b>Emergency transport from CNH to non-VA ER (911 call):</b> 38 U.S.C. 1725 reimburses the emergency provider. Not a pre-arranged contract transport. VA SMT contract does not apply to 911 calls.<br><br><b>Non-medical transport from CNH (family visits, social passes):</b> NOT covered under BT or VTS. Hard exclusion.<br><br><b>Discharge from CNH to home:</b> Standard BT if BT eligible. Contract SMT commonly needed.<br><br><b>AMA discharge from CNH:</b> Hard stop. No BT, no contract SMT.<br><br><span class="auth">38 U.S.C. §1720</span> <span class="auth">38 CFR 70.30(b)(3)(5)</span> <span class="auth">VHA 1601B.05 App. A §5(c)</span>'},

// ══ DENTAL / SPECIALTY ════════════════════════════════════════════════════════
{tags:['elig'],keywords:['dental BT eligibility 1712 restricted eligible dental care'],
q:'Is BT available for travel to non-VA dental providers?',
a:'<b>Dental BT eligibility is MORE restrictive than medical eligibility.</b><br><br>BT for non-VA dental care is only authorized if the Veteran is <b>eligible for VA dental care under 38 U.S.C. §1712(a)</b>, which includes:<br>• Veterans with 100% SC disability rating<br>• Former Prisoners of War (POWs)<br>• Veterans with service-connected dental conditions<br>• Veterans in vocational rehabilitation with dental needs<br>• Other specific eligibility categories<br><br><b>Many enrolled Veterans are NOT eligible for VA dental care</b> — enrollment in VA health care alone does NOT create dental BT eligibility.<br><br>The dental care must also be VA-authorized through community care.<br><br><span class="auth">38 U.S.C. §1712(a)</span> <span class="auth">38 CFR 70.30(b)(2)</span><div class="warn">Always verify dental eligibility under 1712(a) separately from medical BT eligibility before approving BT or contract SMT for dental transport.</div>'},

// ══ CWT / VJO ════════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['CWT compensated work therapy employment transport VTS authorized'],
q:'Can VA transport Veterans in the Compensated Work Therapy (CWT) program to work?',
a:'<b>Yes — but only to VA employment directly associated with CWT participation.</b><br><br>VTS is authorized to transport CWT Veterans to and from their VA employment. This authority is under <b>38 U.S.C. §111A (VTS)</b> — NOT BT (38 U.S.C. §111). Contract SMT cannot be used for CWT employment transport (no BT authority).<br><br>Veterans who drop out of CWT or transition to the Supportive Employment Program (SEP) lose eligibility for employment transportation.<br><br>Transportation to non-VA employment is NOT authorized, even for CWT participants.<br><br><span class="auth">38 U.S.C. §111A</span> <span class="auth">38 U.S.C. §1718</span> <span class="auth">VHA 1695(1) §5(k)(6) and App. C §4</span>'},

// ══ VTS PRIORITY ═════════════════════════════════════════════════════════════
{tags:['proc'],keywords:['VTS priority order who gets priority first when resources limited insufficient'],
q:'What is the priority order for VTS when resources are insufficient?',
a:'When VTS resources are insufficient to transport all requesting persons, the following priority order applies (no single factor is determinative):<br><br><b>1.</b> Basis for eligibility — <b>Enrolled Veterans first</b>, then: non-enrolled Veterans → Servicemembers → Family Caregivers → counseling/MH services persons → CITI beneficiaries → Guests<br><b>2.</b> First-in-time request<br><b>3.</b> Clinical need of the eligible person<br><b>4.</b> Inability to transport themselves (visual impairment, immobility, etc.)<br><b>5.</b> Eligibility for other transportation services or benefits<br><b>6.</b> Availability of other transportation services (common carriers, VSOs)<br><b>7.</b> VA medical facility\'s ability to maximize use of available resources<br><br>Any person denied VTS must be assisted in identifying and accessing other transportation options.<br><br><span class="auth">38 CFR 70.73(c)</span> <span class="auth">VHA 1695(1) §5 and §15</span>'},

// ══ VEHICLE SAFETY ═══════════════════════════════════════════════════════════
{tags:['proc'],keywords:['personal vehicle POV prohibited VTS transport patients private owned'],
q:'Are personally-owned vehicles (POVs) allowed for patient transport under VTS?',
a:'<b>No — personal (privately-owned) vehicles for transport of patients are PROHIBITED. NO EXCEPTION.</b><br><br>VTS uses vehicles owned or leased by VA. Other prohibited actions by VTS drivers include:<br>• Leaving a patient unattended in a vehicle<br>• Using cell phones while the vehicle is moving or stopped in an unsafe location<br>• Entering a passenger\'s residence<br>• Transporting any passenger while seated on a motorized scooter<br>• Leaving a vehicle running and unattended<br><br>15-passenger vans currently in inventory are limited to 9 occupants (including the driver).<br><br><span class="auth">VHA 1695(1) §4(f)(5)(a)</span> <span class="auth">VHA 1695(1) §4(o)</span>'},

];

// ── SEARCH ENGINE ────────────────────────────────────────────────────────────
function tokenize(s){
  return (s||'').toLowerCase().replace(/[^a-z0-9\s]/g,' ').split(/\s+/).filter(function(w){return w.length>2;});
}
var STOP = new Set(['the','and','for','are','not','was','that','this','with','from','they','have','been','will','when','what','does','can','who','how','all','any','but','our','you','your','its','use','get']);

function score(entry, tokens){
  var hay = (entry.q+' '+entry.keywords.join(' ')+' '+entry.a).toLowerCase();
  var s=0;
  tokens.forEach(function(t){
    if(STOP.has(t)) return;
    if(entry.keywords.join(' ').toLowerCase().includes(t)) s+=4;
    else if(entry.q.toLowerCase().includes(t)) s+=3;
    else if(hay.includes(t)) s+=1;
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
    cardsEl.innerHTML='<div style="text-align:center;padding:40px;color:#546e7a"><b>No results found.</b><br><br>Try different keywords or browse the example chips above.<br>Contact VHABeneficiaryTravelQuestions@va.gov for specific policy questions.</div>';
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
    if(idx===0) card.classList.add('open');
    cardsEl.appendChild(card);
  });
}

function toggle(header){
  var card=header.parentElement;
  card.classList.toggle('open');
}

function setQ(text){
  document.getElementById('q').value=text;
  search();
  document.getElementById('q').focus();
}
</script>
</body>
</html># VTP-Policy-Search
