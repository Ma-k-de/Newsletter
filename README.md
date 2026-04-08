# Newsletter
Baurecht Newsletter
----------------------------------------------------------------------
Erstelle den heutigen Baurecht-Newsletter.

Recherchiere aktuelle Entwicklungen der letzten 14 Tage zu VOB, BauGB, HOAI,
DIN-Normen, Arbeitsschutz, BGH/OLG-Urteile und GEG. Gib das Ergebnis als
vollständiges HTML-Dokument aus und ergänze immer die jeweilige Quelle.
Außerdem ergänze jeweils eine kurze Einordnung, was die jeweilige Entwicklung
für ein kleines Bauunternehmen bedeutet.

----------------------------------------------------------------------
Erstelle den heutigen Baurecht-Newsletter.

Recherchiere aktuelle Entwicklungen der letzten 14 Tage zu VOB, BauGB, HOAI, DIN-Normen, Arbeitsschutz, BGH/OLG-Urteile und GEG. Gib das Ergebnis als vollständiges HTML-Dokument aus und ergänze immer die jeweilige Quelle. Außerdem ergänze jeweils eine kurze Einordnung, was die jeweilige Entwicklung für ein kleines Bauunternehmen bedeutet.

Aktuelle Ausgabe: [LETZTE AUSGABE, z. B. 14/2026 vom 7. April 2026]
Neue Ausgabe:    [NEUE NUMMER, z. B. 15/2026 vom 22. April 2026]

Aktualisiere dann die 4 Stellen im Homepage-Code:
  1. Neue Funktion inhalt_[NR]_[JAHR]() nach inhalt_[LETZTE NR]_[LETZTES JAHR]() einfügen
  2. NEWSLETTER_INHALT: neue Zeile oben eintragen
  3. renderAktuell(): Nummer auf [NEUE NUMMER] umstellen
  4. ARCHIV[]: neuen Eintrag oben einfügen (aktuell:true),
     bei Ausgabe [LETZTE AUSGABE] aktuell:true entfernen

Ausgangslage: Mein aktueller Homepage-Code (index.html aus GitHub):
[CODE HIER EINFÜGEN – Strg+A, Strg+C aus der Datei]
-----------------------------------------------------------------------------
Die 4 Stellen im Code – Referenz
1
ARCHIV[] – neuen Eintrag oben einfügen aktuell:true setzen
// NEU oben einfügen: { nr:'15/2026', datum:'22. April 2026', aktuell:true, themen:['Thema A','Thema B','Thema C'], highlight:'Wichtigste Meldung · Zweite · Dritte' }, // Beim alten Eintrag aktuell:true entfernen: { nr:'14/2026', datum:'7. April 2026', /* kein aktuell mehr */ themen:[...], highlight:'...' },
2
inhalt_15_2026() – neue Funktion anlegen
// Nach inhalt_14_2026() einfügen: function inhalt_15_2026() { return ` <div class="page-hdr">...</div> <div class="editorial">...</div> <div class="section" id="s-vob">...</div> ... alle 7 Sektionen ... <div class="disclaimer">...</div>`; }
3
NEWSLETTER_INHALT – neue Zeile oben eintragen
const NEWSLETTER_INHALT = { '15/2026': inhalt_15_2026(), // ← NEU '14/2026': inhalt_14_2026() };
4
renderAktuell() – Nummer umstellen eine Zahl ändern
function renderAktuell() { return NEWSLETTER_INHALT['15/2026']; /* ← war '14/2026' */ }



----------------------------------------

<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Newsletter-Workflow SOP</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Arial,sans-serif;background:#f0f4f8;color:#1e2530;font-size:14px;line-height:1.65;padding:32px 24px 60px}
.wrapper{max-width:820px;margin:0 auto}

h1{font-size:22px;color:#1a3a5c;margin-bottom:4px}
.subtitle{font-size:13px;color:#5a6a7e;margin-bottom:32px}

.karte{background:#fff;border:1px solid #d5dde8;border-radius:8px;margin-bottom:20px;overflow:hidden}
.karte-hdr{background:#1a3a5c;color:#fff;padding:12px 20px;display:flex;align-items:center;gap:10px}
.karte-hdr-icon{width:28px;height:28px;background:#b8860b;border-radius:5px;display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
.karte-hdr-text{font-size:14px;font-weight:700;letter-spacing:.3px}
.karte-hdr-badge{margin-left:auto;font-size:10px;background:rgba(255,255,255,.2);border:1px solid rgba(255,255,255,.3);padding:2px 8px;border-radius:10px}
.karte-body{padding:18px 20px}

.step{display:flex;gap:14px;padding:10px 0;border-bottom:1px solid #eef1f5}
.step:last-child{border-bottom:none}
.step-nr{width:24px;height:24px;background:#1a3a5c;color:#fff;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;margin-top:1px}
.step-body{}
.step-title{font-weight:700;font-size:13px;color:#1a3a5c;margin-bottom:3px}
.step-desc{font-size:12.5px;color:#444;line-height:1.6}

.prompt-box{background:#1e2530;color:#e8f0fb;padding:18px 20px;border-radius:6px;font-family:'Courier New',monospace;font-size:12.5px;line-height:1.7;white-space:pre-wrap;margin:4px 0;position:relative}
.prompt-highlight{color:#f0c040;font-weight:700}
.prompt-var{color:#7dd3a8}

.code-box{background:#f4f7fb;border:1px solid #d5dde8;border-radius:6px;padding:14px 16px;font-family:'Courier New',monospace;font-size:12px;line-height:1.7;color:#1e2530;margin:8px 0}
.code-comment{color:#5a6a7e}
.code-key{color:#b03030;font-weight:700}
.code-val{color:#1a5c38}

.hinweis{background:#fff8e1;border:1px solid #f0c040;border-radius:6px;padding:11px 14px;font-size:12.5px;color:#5a3e00;margin:10px 0}
.hinweis strong{color:#7a4a00}

.checkliste{list-style:none;margin:8px 0}
.checkliste li{padding:5px 0;border-bottom:1px solid #eef1f5;font-size:12.5px;display:flex;align-items:flex-start;gap:8px}
.checkliste li:last-child{border-bottom:none}
.checkliste li::before{content:'☐';color:#1a3a5c;font-size:14px;flex-shrink:0;margin-top:0px}

.timeline{display:flex;gap:0;margin:8px 0}
.tl-item{flex:1;text-align:center;position:relative}
.tl-item::after{content:'';position:absolute;top:13px;left:50%;right:-50%;height:2px;background:#d5dde8;z-index:0}
.tl-item:last-child::after{display:none}
.tl-dot{width:26px;height:26px;background:#1a3a5c;color:#fff;border-radius:50%;font-size:11px;font-weight:700;display:flex;align-items:center;justify-content:center;margin:0 auto 6px;position:relative;z-index:1}
.tl-label{font-size:11px;color:#444;line-height:1.4}
.tl-time{font-size:10px;color:#5a6a7e;margin-top:2px}

.zwei-spalten{display:grid;grid-template-columns:1fr 1fr;gap:16px}
@media(max-width:580px){.zwei-spalten{grid-template-columns:1fr}.timeline{flex-direction:column;gap:8px}.tl-item::after{display:none}}

.tag{display:inline-block;font-size:10px;font-weight:700;padding:2px 7px;border-radius:10px;margin-right:4px}
.tag-rot{background:#fde8e8;color:#b03030}
.tag-gruen{background:#e6f5ec;color:#1a5c38}
.tag-blau{background:#e6f0fb;color:#1a3a5c}

footer{margin-top:28px;padding-top:16px;border-top:1px solid #d5dde8;font-size:11.5px;color:#5a6a7e;text-align:center}
</style>
</head>
<body>
<div class="wrapper">

<h1>⚖ Baurecht-Newsletter – Workflow & Prompt-Vorlage</h1>
<p class="subtitle">Standard Operating Procedure · Alle 14 Tage wiederholen · GitHub-Deploy-Workflow</p>

<!-- TIMELINE -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">🗓</div><div class="karte-hdr-text">Alle 14 Tage – Gesamtaufwand ca. 10 Minuten</div></div>
  <div class="karte-body">
    <div class="timeline">
      <div class="tl-item"><div class="tl-dot">1</div><div class="tl-label">Prompt kopieren &amp; anpassen</div><div class="tl-time">2 Min.</div></div>
      <div class="tl-item"><div class="tl-dot">2</div><div class="tl-label">Neues Chat-Gespräch starten</div><div class="tl-time">1 Min.</div></div>
      <div class="tl-item"><div class="tl-dot">3</div><div class="tl-label">Code erhalten &amp; prüfen</div><div class="tl-time">3 Min.</div></div>
      <div class="tl-item"><div class="tl-dot">4</div><div class="tl-label">GitHub commit &amp; deploy</div><div class="tl-time">4 Min.</div></div>
    </div>
  </div>
</div>

<!-- PROMPT-VORLAGE -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">📋</div><div class="karte-hdr-text">Prompt-Vorlage – kopieren &amp; Platzhalter ersetzen</div><div class="karte-hdr-badge">Datei: prompt_vorlage.txt</div></div>
  <div class="karte-body">
    <div class="hinweis"><strong>So verwenden:</strong> Platzhalter in <span style="color:#b03030;font-weight:700">[GROSSBUCHSTABEN]</span> durch aktuelle Werte ersetzen, dann gesamten Text als erste Nachricht in einen neuen Claude-Chat einfügen.</div>
    <div class="prompt-box"><span class="prompt-highlight">Erstelle den heutigen Baurecht-Newsletter.</span>

Recherchiere aktuelle Entwicklungen der letzten 14 Tage zu VOB, BauGB, HOAI, DIN-Normen, Arbeitsschutz, BGH/OLG-Urteile und GEG. Gib das Ergebnis als vollständiges HTML-Dokument aus und ergänze immer die jeweilige Quelle. Außerdem ergänze jeweils eine kurze Einordnung, was die jeweilige Entwicklung für ein kleines Bauunternehmen bedeutet.

<span class="prompt-highlight">Aktuelle Ausgabe:</span> <span class="prompt-var">[LETZTE AUSGABE, z. B. 14/2026 vom 7. April 2026]</span>
<span class="prompt-highlight">Neue Ausgabe:</span>    <span class="prompt-var">[NEUE NUMMER, z. B. 15/2026 vom 22. April 2026]</span>

<span class="prompt-highlight">Aktualisiere dann die 4 Stellen im Homepage-Code:</span>
  1. Neue Funktion inhalt_<span class="prompt-var">[NR]</span>_<span class="prompt-var">[JAHR]</span>() nach inhalt_<span class="prompt-var">[LETZTE NR]</span>_<span class="prompt-var">[LETZTES JAHR]</span>() einfügen
  2. NEWSLETTER_INHALT: neue Zeile oben eintragen
  3. renderAktuell(): Nummer auf <span class="prompt-var">[NEUE NUMMER]</span> umstellen
  4. ARCHIV[]: neuen Eintrag oben einfügen (aktuell:true),
     bei Ausgabe <span class="prompt-var">[LETZTE AUSGABE]</span> aktuell:true entfernen

<span class="prompt-highlight">Ausgangslage:</span> Mein aktueller Homepage-Code (index.html aus GitHub):
<span class="prompt-var">[CODE HIER EINFÜGEN – Strg+A, Strg+C aus der Datei]</span></div>
  </div>
</div>

<!-- AUSGEFÜLLTES BEISPIEL -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">✏️</div><div class="karte-hdr-text">Ausgefülltes Beispiel – Ausgabe 15/2026</div><div class="karte-hdr-badge">Zur Orientierung</div></div>
  <div class="karte-body">
    <div class="prompt-box">Erstelle den heutigen Baurecht-Newsletter.

Recherchiere aktuelle Entwicklungen der letzten 14 Tage zu VOB, BauGB, HOAI,
DIN-Normen, Arbeitsschutz, BGH/OLG-Urteile und GEG. Gib das Ergebnis als
vollständiges HTML-Dokument aus und ergänze immer die jeweilige Quelle.
Außerdem ergänze jeweils eine kurze Einordnung, was die jeweilige Entwicklung
für ein kleines Bauunternehmen bedeutet.

<span class="prompt-highlight">Aktuelle Ausgabe:</span> 14/2026 vom 7. April 2026
<span class="prompt-highlight">Neue Ausgabe:</span>    15/2026 vom 22. April 2026

Aktualisiere dann die 4 Stellen im Homepage-Code:
  1. Neue Funktion inhalt_15_2026() nach inhalt_14_2026() einfügen
  2. NEWSLETTER_INHALT: '15/2026': inhalt_15_2026(), oben eintragen
  3. renderAktuell(): Nummer auf '15/2026' umstellen
  4. ARCHIV[]: Eintrag 15/2026 oben mit aktuell:true einfügen,
     bei 14/2026 aktuell:true entfernen

<span class="prompt-highlight">Ausgangslage:</span> Mein aktueller Homepage-Code:
[… index.html Inhalt …]</div>
  </div>
</div>

<!-- DIE 4 STELLEN -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">🔧</div><div class="karte-hdr-text">Die 4 Stellen im Code – Referenz</div></div>
  <div class="karte-body">

    <div class="step">
      <div class="step-nr">1</div>
      <div class="step-body">
        <div class="step-title">ARCHIV[] – neuen Eintrag oben einfügen <span class="tag tag-rot">aktuell:true setzen</span></div>
        <div class="code-box"><span class="code-comment">// NEU oben einfügen:</span>
{
  nr:<span class="code-val">'15/2026'</span>, datum:<span class="code-val">'22. April 2026'</span>, <span class="code-key">aktuell:true</span>,
  themen:[<span class="code-val">'Thema A'</span>,<span class="code-val">'Thema B'</span>,<span class="code-val">'Thema C'</span>],
  highlight:<span class="code-val">'Wichtigste Meldung · Zweite · Dritte'</span>
},
<span class="code-comment">// Beim alten Eintrag aktuell:true entfernen:</span>
{ nr:<span class="code-val">'14/2026'</span>, datum:<span class="code-val">'7. April 2026'</span>, <span class="code-comment">/* kein aktuell mehr */</span>
  themen:[...], highlight:<span class="code-val">'...'</span> },</div>
      </div>
    </div>

    <div class="step">
      <div class="step-nr">2</div>
      <div class="step-body">
        <div class="step-title">inhalt_15_2026() – neue Funktion anlegen</div>
        <div class="code-box"><span class="code-comment">// Nach inhalt_14_2026() einfügen:</span>
function <span class="code-key">inhalt_15_2026</span>() {
  return <span class="code-val">`
&lt;div class="page-hdr"&gt;...&lt;/div&gt;
&lt;div class="editorial"&gt;...&lt;/div&gt;
&lt;div class="section" id="s-vob"&gt;...&lt;/div&gt;
... alle 7 Sektionen ...
&lt;div class="disclaimer"&gt;...&lt;/div&gt;`</span>;
}</div>
      </div>
    </div>

    <div class="step">
      <div class="step-nr">3</div>
      <div class="step-body">
        <div class="step-title">NEWSLETTER_INHALT – neue Zeile oben eintragen</div>
        <div class="code-box">const NEWSLETTER_INHALT = {
  <span class="code-key">'15/2026'</span>: inhalt_15_2026(), <span class="code-comment">// ← NEU</span>
  <span class="code-val">'14/2026'</span>: inhalt_14_2026()
};</div>
      </div>
    </div>

    <div class="step">
      <div class="step-nr">4</div>
      <div class="step-body">
        <div class="step-title">renderAktuell() – Nummer umstellen <span class="tag tag-gruen">eine Zahl ändern</span></div>
        <div class="code-box">function renderAktuell() {
  return NEWSLETTER_INHALT[<span class="code-key">'15/2026'</span>]; <span class="code-comment">/* ← war '14/2026' */</span>
}</div>
      </div>
    </div>

  </div>
</div>

<!-- GITHUB DEPLOY -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">🚀</div><div class="karte-hdr-text">GitHub Deploy – Schritt für Schritt</div></div>
  <div class="karte-body">
    <div class="zwei-spalten">
      <div>
        <div style="font-weight:700;font-size:12px;color:#1a3a5c;margin-bottom:8px">Option A – GitHub Web-Editor</div>
        <ul class="checkliste">
          <li>github.com → dein Repository öffnen</li>
          <li>index.html anklicken → Stift-Icon (Edit)</li>
          <li>Alten Code komplett markieren &amp; löschen</li>
          <li>Neuen Code einfügen (Strg+V)</li>
          <li>„Commit changes" → Commit-Nachricht eingeben</li>
          <li>„Commit directly to main" → Bestätigen</li>
          <li>Deploy läuft automatisch (ca. 1–2 Min.)</li>
        </ul>
      </div>
      <div>
        <div style="font-weight:700;font-size:12px;color:#1a3a5c;margin-bottom:8px">Option B – Git CLI (lokal)</div>
        <div class="code-box" style="font-size:11px">git pull origin main
<span class="code-comment"># index.html ersetzen</span>
git add index.html
git commit -m "Newsletter 15/2026"
git push origin main</div>
        <div style="font-size:11.5px;color:#5a6a7e;margin-top:8px">GitHub Pages / Netlify / Vercel deployen automatisch nach dem Push.</div>
      </div>
    </div>
  </div>
</div>

<!-- AUSGABEN-TRACKER -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">📅</div><div class="karte-hdr-text">Ausgaben-Tracker – zum Ausfüllen</div></div>
  <div class="karte-body">
    <table style="width:100%;border-collapse:collapse;font-size:12.5px">
      <tr style="background:#f4f7fb">
        <th style="padding:8px 12px;text-align:left;border-bottom:2px solid #d5dde8;color:#1a3a5c">Ausgabe</th>
        <th style="padding:8px 12px;text-align:left;border-bottom:2px solid #d5dde8;color:#1a3a5c">Datum</th>
        <th style="padding:8px 12px;text-align:left;border-bottom:2px solid #d5dde8;color:#1a3a5c">Wichtigstes Thema</th>
        <th style="padding:8px 12px;text-align:left;border-bottom:2px solid #d5dde8;color:#1a3a5c">Deployed</th>
      </tr>
      <tr style="background:#e6f5ec">
        <td style="padding:8px 12px;border-bottom:1px solid #d5dde8;font-weight:700">14/2026</td>
        <td style="padding:8px 12px;border-bottom:1px solid #d5dde8">7. April 2026</td>
        <td style="padding:8px 12px;border-bottom:1px solid #d5dde8">BGH Dreiangebotsregel · Tariflöhne +3,9 %</td>
        <td style="padding:8px 12px;border-bottom:1px solid #d5dde8">✅</td>
      </tr>
      <tr><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">15/2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">22. April 2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e"></td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8">☐</td></tr>
      <tr><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">16/2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">6. Mai 2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e"></td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8">☐</td></tr>
      <tr><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">17/2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">20. Mai 2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e"></td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8">☐</td></tr>
      <tr><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">18/2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e">3. Juni 2026</td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8;color:#5a6a7e"></td><td style="padding:8px 12px;border-bottom:1px solid #d5dde8">☐</td></tr>
      <tr><td style="padding:8px 12px;color:#5a6a7e">19/2026</td><td style="padding:8px 12px;color:#5a6a7e">17. Juni 2026</td><td style="padding:8px 12px;color:#5a6a7e"></td><td style="padding:8px 12px">☐</td></tr>
    </table>
  </div>
</div>

<!-- WICHTIGE HINWEISE -->
<div class="karte">
  <div class="karte-hdr"><div class="karte-hdr-icon">⚠️</div><div class="karte-hdr-text">Wichtige Hinweise</div></div>
  <div class="karte-body">
    <div class="hinweis"><strong>Kein Gedächtnis zwischen Gesprächen:</strong> Jede neue Chat-Session startet bei null. Immer den aktuellen Code aus GitHub mitgeben – sonst arbeitet Claude auf einem veralteten Stand.</div>
    <div class="hinweis" style="margin-top:10px"><strong>Neues Gespräch ≠ neue Ausgabe:</strong> Pro Ausgabe genau ein neues Gespräch starten. Nicht in einem alten Gespräch weitermachen – dort kennt Claude den aktuellen Code nicht.</div>
    <div style="margin-top:14px">
      <div style="font-weight:700;font-size:12px;color:#1a3a5c;margin-bottom:8px">Empfohlene Dateistruktur im GitHub-Repo:</div>
      <div class="code-box">mein-newsletter-repo/
├── index.html          ← Homepage (wird bei jeder Ausgabe ersetzt)
├── prompt_vorlage.txt  ← Diese SOP / Prompt-Vorlage
└── README.md           ← Kurzbeschreibung des Projekts</div>
    </div>
  </div>
</div>

<footer>
  Baurecht-Newsletter · Workflow SOP · Stand: April 2026 · Zum Ausdrucken oder als Referenz im GitHub-Repo speichern
</footer>

</div>
</body>
</html>
