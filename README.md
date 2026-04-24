import { useState } from "react";

const files = [
  {
    id: "scenarios",
    label: "File 1",
    title: "Scenario Authorization Matrix",
    repo: "vtp-scenarios",
    artifact: "vtp_notepad",
    url: "yourusername.github.io/vtp-scenarios",
    color: "#c0392b",
    lightColor: "#fde8e8",
    desc: "The 89-row scenario table with BT eligible / NOT BT eligible split rows, contract SMT column, gap scenarios, and all filters.",
    contains: [
      "89 transport scenarios",
      "BT eligible vs NOT BT eligible split rows",
      "Contract SMT authorization column",
      "1703-to-1703 non-VA transport rules",
      "Drug & alcohol rehab scenarios",
      "Clickable CONDITIONAL badges",
      "Print / Save as PDF button",
    ],
    steps: [
      "Go to github.com → sign in → open your vtp-scenarios repository",
      "Click index.html in the file list",
      "Click the pencil ✏️ icon (Edit this file) — top right of the file view",
      "Click inside the editor → Ctrl+A to select all → Delete to clear",
      'Find the artifact titled "VTP Scenarios — BT Eligible vs Not BT Eligible Split" in this conversation',
      "Click the Copy icon in its top-right corner",
      "Click back in the GitHub editor → Ctrl+V to paste",
      'Scroll to bottom → Commit changes → message: "Updated 1703-to-1703 contract SMT rules" → green Commit button',
      "Wait 2 minutes — your existing URL updates automatically",
    ],
  },
  {
    id: "search",
    label: "File 2",
    title: "Policy & Regulation Search Site",
    repo: "vtp-policy-search",
    artifact: "vtp_search",
    url: "yourusername.github.io/vtp-policy-search",
    color: "#1a3a5c",
    lightColor: "#e8eef5",
    desc: "The search site where staff type questions and get regulatory answers. Includes Cerner order guide modals, LEAF pre-pay link, and all gap scenario answers.",
    contains: [
      "Plain-language policy search",
      "Cerner order guide popups (SMT, Common Carrier, Nearest Facility, etc.)",
      "LEAF pre-pay form link",
      "BT eligible vs NOT BT eligible explainer",
      "1703-to-1703 contract SMT answers",
      "eCAMS processing table",
      "All regulatory citations",
    ],
    steps: [
      "Go to github.com → sign in → open your vtp-policy-search repository",
      "Click index.html in the file list",
      "Click the pencil ✏️ icon (Edit this file) — top right of the file view",
      "Click inside the editor → Ctrl+A to select all → Delete to clear",
      'Find the artifact titled "VTP Policy Search — Cerner + Templates + LEAF Link" in this conversation',
      "Click the Copy icon in its top-right corner",
      "Click back in the GitHub editor → Ctrl+V to paste",
      'Scroll to bottom → Commit changes → message: "Updated non-VA transport and 1703-to-1703 contract SMT rules" → green Commit button',
      "Wait 2 minutes — your existing URL updates automatically",
    ],
  },
  {
    id: "landing",
    label: "File 3",
    title: "Hub Landing Page",
    repo: "vtp-home",
    artifact: "vtp_landing",
    url: "yourusername.github.io/vtp-home",
    color: "#0F6E56",
    lightColor: "#e1f5ee",
    desc: "The central hub page with buttons linking to both tools. Staff bookmark this one URL to access everything. Add new tool links here as you build them.",
    contains: [
      "Links to both existing tools",
      "Quick reference links (LEAF, income thresholds, OCC, 38 CFR Part 70, VSOs, HRTG)",
      "Key VTP contacts",
      "Recent updates log",
      "Professional VA-branded header",
    ],
    steps: [
      "Go to github.com → sign in → create a NEW repository named vtp-home",
      "Check 'Add a README file' when creating it → click Create repository",
      "Click Add file → Create new file → name it index.html",
      'Find the artifact titled "VTP Hub Landing Page" in this conversation',
      "Click the Copy icon in its top-right corner",
      "Paste into the GitHub editor",
      "BEFORE committing: find REPLACE_WITH_YOUR_POLICY_SEARCH_URL and replace with your actual search site URL",
      "Find REPLACE_WITH_YOUR_SCENARIO_MATRIX_URL and replace with your actual scenario matrix URL",
      'Scroll to bottom → Commit changes → message: "Initial landing page" → green Commit button',
      "Go to Settings → Pages → Deploy from main branch → Save",
      "Wait 2 minutes → your new URL appears at Settings → Pages",
    ],
  },
];

export default function App() {
  const [open, setOpen] = useState(null);

  return (
    <div style={{ fontFamily: "var(--font-sans)", padding: "0.5rem 0" }}>

      <div style={{ background: "#1a3a5c", color: "#fff", padding: "14px 18px", borderRadius: "8px 8px 0 0" }}>
        <div style={{ fontSize: 15, fontWeight: 500, marginBottom: 4 }}>VTP GitHub Files — Which Code Goes Where</div>
        <div style={{ fontSize: 11, opacity: .8 }}>Three separate files. Three separate repositories. Same process for each. Click a file card to see exactly what it contains and the step-by-step instructions.</div>
      </div>

      <div style={{ background: "#fff3cd", border: "0.5px solid #ffe082", borderTop: "none", padding: "8px 16px", fontSize: 11, color: "#7a5300" }}>
        <b>How to tell the files apart:</b> Each artifact in this conversation has a title at the top of the code block. Match the title to the card below to find the right code to copy.
      </div>

      <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(260px, 1fr))", gap: 12, padding: "14px 0", background: "#f0f4f8", borderLeft: "0.5px solid #c8d3dc", borderRight: "0.5px solid #c8d3dc", paddingLeft: 14, paddingRight: 14 }}>
        {files.map(f => (
          <div key={f.id}
            onClick={() => setOpen(open === f.id ? null : f.id)}
            style={{
              background: "#fff",
              border: `2px solid ${open === f.id ? f.color : "#d0d7de"}`,
              borderRadius: 8,
              cursor: "pointer",
              overflow: "hidden",
              transition: "border-color .15s",
            }}>
            <div style={{ background: f.color, color: "#fff", padding: "8px 14px", display: "flex", alignItems: "center", gap: 8 }}>
              <span style={{ fontSize: 11, fontWeight: 700, background: "rgba(255,255,255,.2)", padding: "2px 8px", borderRadius: 3 }}>{f.label}</span>
              <span style={{ fontSize: 13, fontWeight: 500 }}>{f.title}</span>
            </div>
            <div style={{ padding: "12px 14px" }}>
              <div style={{ fontSize: 11, color: "#546e7a", marginBottom: 8, lineHeight: 1.5 }}>{f.desc}</div>
              <div style={{ display: "flex", flexDirection: "column", gap: 3, marginBottom: 10 }}>
                {f.contains.map((c, i) => (
                  <div key={i} style={{ display: "flex", alignItems: "flex-start", gap: 6, fontSize: 11, color: "#37474f" }}>
                    <span style={{ color: f.color, fontWeight: 700, flexShrink: 0, marginTop: 1 }}>✓</span>
                    <span>{c}</span>
                  </div>
                ))}
              </div>
              <div style={{ background: f.lightColor, borderRadius: 4, padding: "6px 10px", marginBottom: 10 }}>
                <div style={{ fontSize: 10, color: "#546e7a", marginBottom: 2 }}>Repository name</div>
                <div style={{ fontSize: 12, fontWeight: 500, color: f.color, fontFamily: "monospace" }}>{f.repo}</div>
              </div>
              <div style={{ background: "#f7f9fb", borderRadius: 4, padding: "6px 10px", marginBottom: 10 }}>
                <div style={{ fontSize: 10, color: "#546e7a", marginBottom: 2 }}>Artifact title to find in this conversation</div>
                <div style={{ fontSize: 11, fontWeight: 500, color: "#0d2137", fontStyle: "italic" }}>"{f.artifact === "vtp_notepad" ? "VTP Scenarios — BT Eligible vs Not BT Eligible Split" : f.artifact === "vtp_search" ? "VTP Policy Search — Cerner + Templates + LEAF Link" : "VTP Hub Landing Page"}"</div>
              </div>
              <button style={{
                width: "100%",
                padding: "7px 0",
                background: f.color,
                color: "#fff",
                border: "none",
                borderRadius: 4,
                fontSize: 11,
                fontWeight: 700,
                cursor: "pointer",
              }}>
                {open === f.id ? "▲ Hide instructions" : "▼ Show step-by-step instructions"}
              </button>
            </div>

            {open === f.id && (
              <div style={{ borderTop: `0.5px solid ${f.lightColor}`, padding: "12px 14px", background: "#fafafa" }}>
                <div style={{ fontSize: 11, fontWeight: 700, color: f.color, marginBottom: 10, textTransform: "uppercase", letterSpacing: ".05em" }}>
                  Step-by-step — {f.title}
                </div>
                {f.steps.map((s, i) => (
                  <div key={i} style={{ display: "flex", gap: 10, marginBottom: 8, alignItems: "flex-start" }}>
                    <span style={{
                      width: 20, height: 20, borderRadius: "50%",
                      background: f.color, color: "#fff",
                      fontSize: 10, fontWeight: 700,
                      display: "flex", alignItems: "center", justifyContent: "center",
                      flexShrink: 0, marginTop: 1,
                    }}>{i + 1}</span>
                    <span style={{ fontSize: 11, color: "#37474f", lineHeight: 1.5 }}>{s}</span>
                  </div>
                ))}
                <div style={{ marginTop: 10, background: "#fff8e1", border: "0.5px solid #ffe082", borderRadius: 4, padding: "7px 10px", fontSize: 11, color: "#7a5300" }}>
                  <b>After committing:</b> Wait 2 minutes then refresh — your existing URL serves the updated content automatically. No need to resend links to anyone.
                </div>
                {f.id === "landing" && (
                  <div style={{ marginTop: 8, background: "#fde8e8", border: "0.5px solid #f4b3b3", borderRadius: 4, padding: "7px 10px", fontSize: 11, color: "#7a0000" }}>
                    <b>Remember for the landing page:</b> Replace both REPLACE_WITH_YOUR_..._URL placeholders with your actual GitHub Pages URLs before committing, or the buttons will not work.
                  </div>
                )}
              </div>
            )}
          </div>
        ))}
      </div>

      <div style={{ background: "#e8eef5", border: "0.5px solid #c8d3dc", borderTop: "none", borderRadius: "0 0 8px 8px", padding: "10px 14px" }}>
        <div style={{ fontSize: 11, color: "#1a3a5c", fontWeight: 500, marginBottom: 6 }}>Quick reference — artifact titles to look for in this conversation</div>
        <div style={{ display: "flex", flexWrap: "wrap", gap: 8 }}>
          {[
            { label: "File 1 — Scenario Matrix", title: "VTP Scenarios — BT Eligible vs Not BT Eligible Split — Copy Into Notepad", color: "#c0392b" },
            { label: "File 2 — Policy Search", title: "VTP Policy Search — Cerner + Templates + LEAF Link", color: "#1a3a5c" },
            { label: "File 3 — Landing Page", title: "VTP Hub Landing Page — Copy Into Notepad → Save as index.html", color: "#0F6E56" },
          ].map(f => (
            <div key={f.label} style={{ background: "#fff", border: `1px solid ${f.color}`, borderRadius: 4, padding: "6px 10px", flex: "1 1 200px" }}>
              <div style={{ fontSize: 10, fontWeight: 700, color: f.color, marginBottom: 2 }}>{f.label}</div>
              <div style={{ fontSize: 10, color: "#37474f", fontStyle: "italic" }}>"{f.title}"</div>
            </div>
          ))}
        </div>
      </div>

    </div>
  );
}
