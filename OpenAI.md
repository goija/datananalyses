<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>OpenAI, Real-Time Spraak &amp; Nederlandse AI-Jurisprudentie</title>
  <style>
    :root {
      --bg: #ffffff;
      --surface: #fafafa;
      --surface-alt: #f3f3f3;
      --text: #111111;
      --muted: #555555;
      --accent: #A31C1C;
      --accent-hover: #7d1414;
      --accent-soft: #fdf2f2;
      --border: #dcdcdc;
      --base-font: 19px;
    }

    * {
      box-sizing: border-box;
    }

    html {
      font-size: var(--base-font);
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      padding: 0;
      background-color: var(--bg);
      color: var(--text);
      font-family: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      line-height: 1.65;
    }

    .container {
      max-width: 960px;
      margin: 0 auto;
      padding: 1.5rem 1.25rem 3.5rem;
    }

    /* Topbar */
    .topbar {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 0.75rem;
      padding-bottom: 1rem;
      margin-bottom: 1.5rem;
      border-bottom: 1px solid var(--border);
    }

    .back-link {
      color: var(--accent);
      text-decoration: none;
      font-weight: 600;
      font-size: 0.9rem;
    }

    .back-link:hover,
    .back-link:focus-visible {
      text-decoration: underline;
      outline: none;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 0.4rem;
    }

    button {
      font-family: inherit;
      font-size: 0.8rem;
      font-weight: 600;
      padding: 0.35rem 0.65rem;
      background: var(--bg);
      color: var(--text);
      border: 1px solid var(--border);
      border-radius: 4px;
      cursor: pointer;
    }

    button:hover,
    button:focus-visible {
      border-color: var(--accent);
      color: var(--accent);
      outline: none;
    }

    button.active,
    .btn-accent {
      background: var(--accent);
      color: #ffffff;
      border-color: var(--accent);
    }

    .btn-accent:hover,
    .btn-accent:focus-visible {
      background: var(--accent-hover);
      border-color: var(--accent-hover);
      color: #ffffff;
    }

    /* Header */
    header {
      border-bottom: 3px solid var(--accent);
      padding-bottom: 1.25rem;
      margin-bottom: 1.75rem;
    }

    .kicker {
      display: inline-block;
      font-size: 0.75rem;
      font-weight: 700;
      letter-spacing: 0.05em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 0.4rem;
    }

    header h1 {
      margin: 0 0 0.6rem;
      font-size: 1.7rem;
      line-height: 1.2;
    }

    .lead {
      margin: 0;
      color: var(--muted);
      font-size: 1rem;
    }

    /* Inhoudsopgave */
    .toc {
      background: var(--surface);
      border: 1px solid var(--border);
      border-left: 4px solid var(--accent);
      padding: 1.1rem 1.25rem;
      margin-bottom: 2.25rem;
      border-radius: 0 4px 4px 0;
    }

    .toc-title {
      margin: 0 0 0.6rem;
      font-size: 0.82rem;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      color: var(--muted);
      font-weight: 700;
    }

    .toc ol {
      margin: 0;
      padding-left: 1.35rem;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 0.35rem 1.5rem;
    }

    .toc a {
      color: var(--text);
      text-decoration: none;
      font-size: 0.88rem;
    }

    .toc a:hover,
    .toc a:focus-visible {
      color: var(--accent);
      text-decoration: underline;
    }

    /* Secties */
    section {
      margin-bottom: 2.75rem;
      scroll-margin-top: 1.25rem;
    }

    h2 {
      font-size: 1.35rem;
      line-height: 1.3;
      margin: 0 0 1rem;
      padding-bottom: 0.4rem;
      border-bottom: 1px solid var(--border);
    }

    h3 {
      font-size: 1.02rem;
      margin: 1.1rem 0 0.45rem;
    }

    p {
      margin: 0 0 0.9rem;
    }

    a {
      color: var(--accent);
    }

    a:hover {
      color: var(--accent-hover);
    }

    /* Kaarten */
    .card-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1rem;
      margin: 1rem 0 1.25rem;
    }

    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-top: 3px solid var(--accent);
      border-radius: 4px;
      padding: 1.1rem 1.25rem;
    }

    .card h3 {
      margin-top: 0;
      color: var(--accent);
    }

    .card p:last-child,
    .card ul:last-child {
      margin-bottom: 0;
    }

    .callout {
      background: var(--accent-soft);
      border: 1px solid #e8c4c4;
      border-left: 4px solid var(--accent);
      padding: 1rem 1.2rem;
      border-radius: 0 4px 4px 0;
      margin: 1.25rem 0;
      font-size: 0.94rem;
    }

    .callout p:last-child {
      margin-bottom: 0;
    }

    /* Interactieve Dossierboom */
    .tree-controls {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
      margin-bottom: 1rem;
    }

    .tree details {
      border: 1px solid var(--border);
      border-radius: 4px;
      margin-bottom: 0.75rem;
      background: var(--bg);
    }

    .tree > details {
      border-left: 4px solid var(--accent);
    }

    .tree summary {
      cursor: pointer;
      padding: 0.75rem 1rem;
      font-weight: 700;
      background: var(--surface);
      list-style: none;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 0.75rem;
    }

    .tree summary::-webkit-details-marker {
      display: none;
    }

    .tree summary::after {
      content: "+";
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--accent);
      flex-shrink: 0;
    }

    .tree details[open] > summary::after {
      content: "−";
    }

    .tree-body {
      padding: 0.9rem 1.1rem 1rem;
      border-top: 1px solid var(--border);
    }

    .tree-sub {
      margin-top: 0.5rem;
    }

    .tree-sub details {
      margin-bottom: 0.65rem;
      border-left: 3px solid var(--border);
    }

    .tree-sub summary {
      font-size: 0.95rem;
      background: var(--bg);
      padding: 0.6rem 0.85rem;
    }

    .tree-facts {
      margin: 0;
      padding-left: 1.2rem;
      font-size: 0.93rem;
    }

    .tree-facts li {
      margin-bottom: 0.4rem;
    }

    .tree-facts li:last-child {
      margin-bottom: 0;
    }

    /* ECLI Filter & Zoekbalk */
    .toolbar {
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
      padding: 1rem;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 4px;
      margin-bottom: 1.25rem;
    }

    .filter-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.45rem;
      align-items: center;
    }

    .search-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.65rem;
      align-items: center;
    }

    .search-input {
      flex: 1 1 250px;
      font-family: inherit;
      font-size: 0.9rem;
      padding: 0.45rem 0.75rem;
      border: 1px solid var(--border);
      border-radius: 4px;
      background: var(--bg);
      color: var(--text);
    }

    .search-input:focus {
      outline: 2px solid var(--accent);
      border-color: var(--accent);
    }

    .count-status {
      font-size: 0.82rem;
      color: var(--muted);
    }

    /* ECLI Kaartenlijst */
    .ecli-list {
      display: flex;
      flex-direction: column;
      gap: 0.9rem;
    }

    .ecli-card {
      border: 1px solid var(--border);
      border-left: 4px solid var(--accent);
      border-radius: 0 4px 4px 0;
      padding: 1rem 1.2rem;
      background: var(--bg);
    }

    .ecli-card[hidden] {
      display: none;
    }

    .ecli-top {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 0.6rem;
      margin-bottom: 0.5rem;
    }

    .ecli-code {
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      font-size: 0.88rem;
      font-weight: 700;
      color: var(--accent);
      background: var(--accent-soft);
      padding: 0.15rem 0.5rem;
      border-radius: 3px;
      border: 1px solid #e8c4c4;
    }

    .ecli-actions {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 0.4rem;
    }

    .badge {
      display: inline-block;
      font-size: 0.7rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.03em;
      padding: 0.15rem 0.45rem;
      border-radius: 3px;
      background: var(--surface-alt);
      border: 1px solid var(--border);
      color: var(--text);
    }

    .badge-warn {
      background: var(--accent);
      color: #ffffff;
      border-color: var(--accent);
    }

    .ecli-meta {
      font-size: 0.88rem;
      color: var(--muted);
      margin-bottom: 0.45rem;
      font-weight: 600;
    }

    .ecli-desc {
      margin: 0;
      font-size: 0.95rem;
    }

    .ecli-note {
      margin: 0.55rem 0 0;
      padding: 0.55rem 0.75rem;
      background: var(--surface);
      border-left: 3px solid var(--border);
      font-size: 0.86rem;
      color: var(--muted);
    }

    /* Overzichtslijst Spoor A */
    .spoor-a-box {
      border: 1px solid var(--border);
      border-radius: 4px;
      overflow: hidden;
      margin-top: 1.5rem;
    }

    .spoor-a-head {
      background: var(--surface-alt);
      border-bottom: 1px solid var(--border);
      padding: 0.7rem 1rem;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 0.6rem;
    }

    .spoor-a-head strong {
      font-size: 0.9rem;
    }

    .spoor-a-list {
      margin: 0;
      padding: 1.1rem 1.25rem 1.1rem 2.2rem;
      background: var(--bg);
      font-size: 0.92rem;
    }

    .spoor-a-list li {
      margin-bottom: 0.5rem;
    }

    .spoor-a-list li:last-child {
      margin-bottom: 0;
    }

    .notes-list {
      margin: 0;
      padding-left: 1.25rem;
    }

    .notes-list li {
      margin-bottom: 0.65rem;
    }

    code {
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
      font-size: 0.85em;
      background: var(--surface-alt);
      padding: 0.1rem 0.35rem;
      border-radius: 3px;
      border: 1px solid var(--border);
    }

    .empty-state {
      padding: 1.25rem;
      text-align: center;
      border: 1px dashed var(--border);
      border-radius: 4px;
      color: var(--muted);
    }

    footer {
      margin-top: 3rem;
      padding-top: 1rem;
      border-top: 1px solid var(--border);
      font-size: 0.8rem;
      color: var(--muted);
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 0.75rem;
    }

    footer a {
      color: var(--accent);
      text-decoration: none;
    }

    footer a:hover {
      text-decoration: underline;
    }

    @media print {
      .topbar,
      .toc,
      .toolbar,
      .tree-controls,
      .copy-ecli-btn,
      #copy-spoor-a,
      .no-print {
        display: none !important;
      }

      body {
        font-size: 10.5pt;
        line-height: 1.45;
      }

      .container {
        max-width: 100%;
        padding: 0;
      }

      .ecli-card,
      .card,
      .tree details {
        break-inside: avoid;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="topbar no-print">
      <a href="./index.html" class="back-link">&larr; Terug naar overzicht</a>
      <div class="controls" aria-label="Pagina-instellingen">
        <button type="button" id="font-dec" aria-label="Kleiner lettertype">A-</button>
        <button type="button" id="font-reset" aria-label="Standaard lettertype">A</button>
        <button type="button" id="font-inc" aria-label="Groter lettertype">A+</button>
        <button type="button" id="print-btn">Afdrukken / PDF</button>
      </div>
    </div>

    <header>
      <span class="kicker">OpenAI, WebRTC &amp; Juridisch Dossier</span>
      <h1>De ontwikkelaar van OpenAI, Real-Time Spraak &amp; Nederlandse AI-Jurisprudentie</h1>
      <p class="lead">
        Samenhang tussen real-time communicatie-infrastructuur (Sean DuBois, Pion, ChatGPT, Alan Quayle) en geverifieerde Nederlandse en internationale rechtspraak rond AI-hallucinaties (art. 21 Rv) en doorbreking van het verschoningsrecht.
      </p>
    </header>

    <nav class="toc no-print" aria-label="Inhoudsopgave">
      <p class="toc-title">Inhoudsopgave</p>
      <ol>
        <li><a href="#openai-webrtc">1. De ontwikkelaar van OpenAI &amp; WebRTC</a></li>
        <li><a href="#dossierstructuur">2. Dossierstructuur (Jurisprudentie &amp; Strategie)</a></li>
        <li><a href="#ecli-database">3. Geverifieerde ECLI-database &amp; Internationaal</a></li>
        <li><a href="#spoor-a-lijst">4. Volledige ECLI-lijst Spoor A (zonder gaten)</a></li>
        <li><a href="#randnotities">5. Randnotities &amp; uitgesloten citaten</a></li>
      </ol>
    </nav>

    <main>
      <!-- SECTIE 1: OPENAI & WEBRTC -->
      <section id="openai-webrtc">
        <h2>1. De ontwikkelaar van OpenAI: Sean DuBois, ChatGPT &amp; Alan Quayle</h2>
        <p>
          <strong>Sean DuBois</strong>, <strong>ChatGPT</strong> en <strong>Alan Quayle</strong> komen samen op het snijvlak van real-time spraaktechnologie en communicatie-infrastructuur (WebRTC).
        </p>

        <div class="card-grid">
          <article class="card">
            <h3>Sean DuBois en ChatGPT</h3>
            <p>
              Sean DuBois is de bedenker van <strong>Pion</strong>, een open-source Go-implementatie voor WebRTC. Sinds 2024 werkt hij bij OpenAI. Daar bouwt hij aan de real-time spraakinfrastructuur van ChatGPT, de <strong>OpenAI Realtime API</strong> en telefonische integraties zoals <strong>1-800-CHATGPT</strong>.
            </p>
          </article>

          <article class="card">
            <h3>De rol van Alan Quayle</h3>
            <p>
              Telecom- en CX-analist Alan Quayle volgt de open-source telecomwereld en WebRTC op de voet. Op zijn blog bespreekt hij regelmatig het werk van DuBois rondom Pion en de opkomst van ChatGPT binnen klantenservice- en communicatietechnologie (<strong>CXTech</strong>).
            </p>
          </article>
        </div>

        <div class="callout">
          <p><strong>Aandachtsgebieden voor technische verdieping:</strong></p>
          <ul>
            <li>De technische werking van WebRTC en Pion binnen ChatGPT.</li>
            <li>Specifieke artikelen en analyses van Alan Quayle over Pion en CXTech.</li>
            <li>Recente ontwikkelingen rondom de OpenAI Realtime API.</li>
          </ul>
        </div>
      </section>

      <!-- SECTIE 2: DOSSIERSTRUCTUUR -->
      <section id="dossierstructuur">
        <h2>2. Dossierstructuur: Jurisprudentie &amp; Strategische Inzet</h2>

        <div class="tree-controls no-print">
          <button type="button" id="expand-all">Alles uitklappen</button>
          <button type="button" id="collapse-all">Alles inklappen</button>
        </div>

        <div class="tree" id="dossier-tree">
          <!-- Tak 1 -->
          <details open>
            <summary>1. Jurisprudentie &amp; Praktijk</summary>
            <div class="tree-body tree-sub">
              <details open>
                <summary>Handelsnaamzaak &amp; AI-hallucinaties (ECLI:NL:RBROT:2025:10388)</summary>
                <div class="tree-body">
                  <ul class="tree-facts">
                    <li><strong>Feiten:</strong> Conclusie van antwoord met niet-bestaande / onjuiste HR-arresten en ECLI’s.</li>
                    <li><strong>Verweer:</strong> Gesteld technisch mankement (Word-naar-PDF-conversie) — door rechter betwijfeld.</li>
                    <li><strong>Oordeel (art. 21 Rv):</strong> Schending waarheidsplicht in het midden gelaten (geen behaald voordeel).</li>
                    <li><strong>Gevolg:</strong> Basis voor reële proceskostenveroordeling (zie tevens Rb. Amsterdam <code>ECLI:NL:RBAMS:2026:8258</code> en Rb. Oost-Brabant) &amp; NOvA-verantwoordelijkheid.</li>
                  </ul>
                </div>
              </details>

              <details open>
                <summary>Strafzaak &amp; Doorbreking Verschoningsrecht (ECLI:NL:RBROT:2026:9319)</summary>
                <div class="tree-body">
                  <ul class="tree-facts">
                    <li><strong>Context:</strong> Beslag juni 2025; forensische filtering toont ChatGPT-prompts met concepten voor advocaat.</li>
                    <li><strong>Rechtsvraag:</strong> Valt input in openbare AI-tool onder afgeleid verschoningsrecht?</li>
                    <li><strong>Oordeel:</strong> Nee — invoer op externe servers geeft vertrouwelijkheid prijs; data toegevoegd aan dossier.</li>
                    <li><strong>Civiele relevantie:</strong> Verlies van exclusieve geheimhouding bij gebruik van openbare tools, plugins en cloud.</li>
                  </ul>
                </div>
              </details>

              <details open>
                <summary>AI-proef Rotterdamse Rechter (maart 2025)</summary>
                <div class="tree-body">
                  <ul class="tree-facts">
                    <li><strong>Opzet:</strong> Lokaal taalmodel in liquidatiezaak voor het structureren van aantekeningen en conceptoverwegingen.</li>
                    <li><strong>Randvoorwaarden:</strong> Volledig afgeschermd (geen externe doorgifte), puur redactioneel; geen zelfstandige bewijswaardering.</li>
                  </ul>
                </div>
              </details>
            </div>
          </details>

          <!-- Tak 2 -->
          <details open>
            <summary>2. Strategische Inzet in Lopend Dossier</summary>
            <div class="tree-body tree-sub">
              <details open>
                <summary>Spoor A: Toetsing stukken wederpartij (art. 21 Rv)</summary>
                <div class="tree-body">
                  <ul class="tree-facts">
                    <li><strong>Doel:</strong> Controleren processtukken &amp; producties (mr. Barendregt-de Vries / mr. Maat).</li>
                    <li><strong>Focus:</strong> Opsporen onjuiste, niet-bestaande of niet-aansluitende wetsartikelen en ECLI-vindplaatsen.</li>
                  </ul>
                </div>
              </details>

              <details open>
                <summary>Spoor B: Gegevensbescherming &amp; Privacy (ECLI:NL:RBROT:2026:9319)</summary>
                <div class="tree-body">
                  <ul class="tree-facts">
                    <li><strong>Doel:</strong> Benutten rechtspraak rond doorbreking vertrouwelijkheid.</li>
                    <li><strong>Focus:</strong> Afschermen eigen bescheiden &amp; aanvechten externe datavergaring/verwerking door derden.</li>
                  </ul>
                </div>
              </details>
            </div>
          </details>
        </div>
      </section>

      <!-- SECTIE 3: ECLI DATABASE -->
      <section id="ecli-database">
        <h2>3. Geverifieerde ECLI-database &amp; Internationale Zaken</h2>

        <div class="callout">
          <strong>Belangrijke correctie verwerkt:</strong> De extra proceskostenveroordeling van <strong>€ 2.315,50</strong> (totaal <strong>€ 26.100,85</strong>) bleek afkomstig van <strong>Rechtbank Amsterdam</strong> (<code>ECLI:NL:RBAMS:2026:8258</code>, 12 augustus 2026) en niet van Rechtbank Oost-Brabant. De aanvullende geverifieerde uitspraken van Rechtbank Oost-Brabant en Rechtbank Noord-Nederland zijn hieronder volledig opgenomen.
        </div>

        <div class="toolbar no-print" aria-label="Filter en zoek uitspraken">
          <div class="filter-row" role="group" aria-label="Filter op categorie">
            <button type="button" class="filter-btn active" data-filter="all">Alles</button>
            <button type="button" class="filter-btn" data-filter="hallucinaties">Art. 21 Rv / Hallucinaties</button>
            <button type="button" class="filter-btn" data-filter="verschoningsrecht">Verschoningsrecht</button>
            <button type="button" class="filter-btn" data-filter="tuchtrecht">Tuchtrecht</button>
            <button type="button" class="filter-btn" data-filter="bewijs">AI als bewijs</button>
            <button type="button" class="filter-btn" data-filter="internationaal">Internationaal</button>
          </div>
          <div class="search-row">
            <input
              type="search"
              id="ecli-search"
              class="search-input"
              placeholder="Zoek op ECLI, rechtbank, datum, art. 21 Rv, erfrecht..."
              aria-label="Zoek in ECLI-database"
            >
            <span id="ecli-count" class="count-status" aria-live="polite"></span>
          </div>
        </div>

        <div id="ecli-list" class="ecli-list"></div>
        <p id="ecli-empty" class="empty-state" hidden>Geen uitspraken gevonden voor deze filter- of zoekopdracht.</p>
      </section>

      <!-- SECTIE 4: VOLLEDIGE LIJST SPOOR A -->
      <section id="spoor-a-lijst">
        <h2>4. Volledige geverifieerde ECLI-lijst voor Spoor A (zonder gaten)</h2>
        <div class="spoor-a-box">
          <div class="spoor-a-head">
            <strong>Klaar voor opname in processtuk of dossiernotitie</strong>
            <button type="button" id="copy-spoor-a" class="btn-accent">Kopieer volledige lijst</button>
          </div>
          <ol class="spoor-a-list" id="spoor-a-content">
            <li><strong>Rb. Rotterdam, 27 augustus 2025:</strong> <code>ECLI:NL:RBROT:2025:10388</code> — AI-hallucinaties in conclusie van antwoord, art. 21 Rv.</li>
            <li><strong>Rb. Noord-Nederland, 19 november 2025:</strong> <code>ECLI:NL:RBNNE:2025:4814</code> — Verkeerde vindplaatsen / ChatGPT-jurisprudentie in verdelingszaak (erfrecht / art. 3:196 BW).</li>
            <li><strong>Rb. Oost-Brabant, 2025:</strong> <code>ECLI:NL:RBOBR:2025:8495</code> — Ondermaatse, door AI geproduceerde processtukken.</li>
            <li><strong>Rb. Oost-Brabant, 12 februari 2026:</strong> <code>ECLI:NL:RBOBR:2026:934</code> en <code>ECLI:NL:RBOBR:2026:909</code> — AI-hallucinaties in processtukken en gevolgen voor procedure en proceskosten.</li>
            <li><strong>Rb. Oost-Brabant, 8 april 2026:</strong> <code>ECLI:NL:RBOBR:2026:2232</code> — Streep door ChatGPT-analyse als bewijs in een civiele procedure.</li>
            <li><strong>Rb. Rotterdam (R-C), 12 juni 2026:</strong> <code>ECLI:NL:RBROT:2026:9319</code> — Doorbreking verschoningsrecht bij externe AI-invoer.</li>
            <li><strong>Raad van Discipline ‘s-Hertogenbosch, juli 2026:</strong> <code>ECLI:NL:TADRSHE:2026:93</code> — Berisping + € 1.250 proceskosten na acht verzonnen uitspraken.</li>
            <li><strong>Rb. Amsterdam, 12 augustus 2026:</strong> <code>ECLI:NL:RBAMS:2026:8258</code> — € 2.315,50 extra proceskosten (totaal € 26.100,85) wegens verzonnen citaat.</li>
          </ol>
        </div>
      </section>

      <!-- SECTIE 5: RANDNOTITIES -->
      <section id="randnotities">
        <h2>5. Randnotities &amp; buiten beschouwing gelaten citaten</h2>
        <ul class="notes-list">
          <li>
            <strong>AI-proef Rotterdamse strafkamer (maart 2025):</strong> Betreft een experiment met een lokaal taalmodel in een liquidatiezaak uit 2014, gecommuniceerd via een nieuwsbericht op <em>rechtspraak.nl</em> (geen uitspraak, dus geen ECLI).
          </li>
          <li>
            <strong>Buiten beschouwing gelaten HR-citaten:</strong> De HR-verwijzingen uit het Hertoghs-artikel (<code>ECLI:NL:HR:2024:375</code>, <code>ECLI:NL:HR:2016:2686</code>, <code>ECLI:NL:HR:2025:456</code>) hebben betrekking op andere onderwerpen en zijn niet relevant voor dit dossier.
          </li>
        </ul>
      </section>
    </main>

    <footer>
      <span>Onderdeel van <a href="./index.html">goija/datananalyses</a></span>
      <span>Geen externe scripts, geen trackingcookies.</span>
    </footer>
  </div>

  <script>
    (() => {
      // 1. Lettergrootte-regeling (standaard 19px)
      let currentFont = 19;
      const setFont = (px) => {
        currentFont = Math.min(26, Math.max(15, px));
        document.documentElement.style.setProperty('--base-font', `${currentFont}px`);
      };
      document.getElementById('font-dec').addEventListener('click', () => setFont(currentFont - 2));
      document.getElementById('font-reset').addEventListener('click', () => setFont(19));
      document.getElementById('font-inc').addEventListener('click', () => setFont(currentFont + 2));
      document.getElementById('print-btn').addEventListener('click', () => window.print());

      // 2. Dossierboom uitklappen / inklappen
      const treeDetails = Array.from(document.querySelectorAll('#dossier-tree details'));
      document.getElementById('expand-all').addEventListener('click', () => {
        treeDetails.forEach((d) => { d.open = true; });
      });
      document.getElementById('collapse-all').addEventListener('click', () => {
        treeDetails.forEach((d) => { d.open = false; });
      });

      // 3. ECLI-gegevensbestand
      const CASES = [
        {
          ecli: 'ECLI:NL:RBROT:2025:10388',
          court: 'Rechtbank Rotterdam',
          date: '27 augustus 2025',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Handelsnaamzaak met AI-hallucinaties in de conclusie van antwoord (alle HR-verwijzingen onjuist); verweer over Word-naar-PDF-conversie door rechter betwijfeld; schending van art. 21 Rv in het midden gelaten wegens geen behaald voordeel.',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBNNE:2025:4814',
          court: 'Rechtbank Noord-Nederland',
          date: '19 november 2025',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Pleitnota / processtuk met aangehaalde arresten die geen betrekking hadden op het onderwerp van de zaak (één arrest over huur, één over een Arubaanse appeltermijn). Waarschuwing voor ongecontroleerde "ChatGPT-jurisprudentie"; stelling onvoldoende onderbouwd.',
          note: 'Extra relevantie voor dit dossier: betreft inhoudelijk een erfrecht-/verdelingsgeschil (notariële verdeling en art. 3:196 BW).',
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBOBR:2025:8495',
          court: 'Rechtbank Oost-Brabant',
          date: 'Eind 2025',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Rechtbank spreekt expliciet van "ondermaatse, door AI geproduceerde processtukken".',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBOBR:2026:934',
          court: 'Rechtbank Oost-Brabant',
          date: '12 februari 2026',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Uitspraak over processtukken met AI-hallucinaties en de gevolgen daarvan voor de procedure en proceskosten (samenhangend met ECLI:NL:RBOBR:2026:909).',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBOBR:2026:909',
          court: 'Rechtbank Oost-Brabant',
          date: '12 februari 2026',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Uitspraak over processtukken met AI-hallucinaties en de gevolgen daarvan voor de procedure en proceskosten (samenhangend met ECLI:NL:RBOBR:2026:934).',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBOBR:2026:2232',
          court: 'Rechtbank Oost-Brabant',
          date: '8 april 2026',
          category: 'bewijs',
          categoryLabel: 'AI als bewijs',
          spoor: 'Spoor A',
          summary: 'Rechtbank zet een streep door een ChatGPT-analyse als bewijs in een civiele procedure.',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBROT:2026:9319',
          court: 'Rechtbank Rotterdam (rechter-commissaris)',
          date: '12 juni 2026 (pv gepubliceerd eind juli 2026)',
          category: 'verschoningsrecht',
          categoryLabel: 'Verschoningsrecht',
          spoor: 'Spoor B',
          summary: 'ChatGPT-prompts met concepten voor een advocaat doorbreken het verschoningsrecht; invoer op externe servers van een openbare AI-tool geldt als openbaarmaking en de data zijn toegevoegd aan het dossier.',
          note: 'Civiele relevantie: verlies van exclusieve geheimhouding bij gebruik van openbare tools, plugins of cloudomgevingen.',
          isNL: true
        },
        {
          ecli: 'ECLI:NL:TADRSHE:2026:93',
          court: 'Raad van Discipline ‘s-Hertogenbosch',
          date: 'Juli 2026',
          category: 'tuchtrecht',
          categoryLabel: 'Tuchtrecht',
          spoor: 'Spoor A',
          summary: 'Eerste expliciete Nederlandse AI-tuchtzaak: berisping en € 1.250 proceskostenveroordeling na het aanvoeren van acht verzonnen uitspraken.',
          note: null,
          isNL: true
        },
        {
          ecli: 'ECLI:NL:RBAMS:2026:8258',
          court: 'Rechtbank Amsterdam',
          date: '12 augustus 2026',
          category: 'hallucinaties',
          categoryLabel: 'Art. 21 Rv / Hallucinaties',
          spoor: 'Spoor A',
          summary: 'Verhoging van de proceskostenveroordeling met een halve punt (€ 2.315,50 extra) tot een totaal van € 26.100,85 wegens een verzonnen citaat in een processtuk dat zowel de wederpartij als de rechtbank onnodig tijd kostte.',
          note: 'Correctie: deze uitspraak stond in eerdere overzichten (bron: Mr. Online) ten onrechte vermeld onder Rechtbank Oost-Brabant.',
          isNL: true,
          corrected: true
        },
        {
          ecli: 'United States v. Heppner',
          court: 'U.S. District Court, Southern District of New York',
          date: '17 februari 2026',
          category: 'internationaal',
          categoryLabel: 'Internationaal',
          spoor: 'Referentie',
          summary: 'Genoemd in dezelfde bronlijst als de Rotterdamse zaken (Hertoghs) rond AI-gebruik en vertrouwelijkheid/procesvoering.',
          note: 'Internationale zaak (geen Nederlandse ECLI).',
          isNL: false
        },
        {
          ecli: 'Mata v. Avianca',
          court: 'U.S. District Court (VS)',
          date: '2023',
          category: 'internationaal',
          categoryLabel: 'Internationaal',
          spoor: 'Referentie',
          summary: 'Bekendste internationale voorloper: advocaat kreeg een boete van $ 5.000 opgelegd voor door ChatGPT verzonnen jurisprudentie.',
          note: 'Internationale zaak (geen Nederlandse ECLI).',
          isNL: false
        }
      ];

      const listEl = document.getElementById('ecli-list');
      const countEl = document.getElementById('ecli-count');
      const emptyEl = document.getElementById('ecli-empty');
      const searchInput = document.getElementById('ecli-search');
      const filterBtns = Array.from(document.querySelectorAll('.filter-btn'));

      let activeFilter = 'all';

      const copyText = async (text, button) => {
        const orig = button.textContent;
        try {
          await navigator.clipboard.writeText(text);
          button.textContent = 'Gekopieerd';
        } catch {
          const ta = document.createElement('textarea');
          ta.value = text;
          document.body.appendChild(ta);
          ta.select();
          document.execCommand('copy');
          ta.remove();
          button.textContent = 'Gekopieerd';
        }
        setTimeout(() => { button.textContent = orig; }, 1800);
      };

      const renderCases = () => {
        const query = searchInput.value.trim().toLowerCase();
        listEl.innerHTML = '';

        const filtered = CASES.filter((item) => {
          const matchesCat = activeFilter === 'all' || item.category === activeFilter;
          const haystack = `${item.ecli} ${item.court} ${item.date} ${item.summary} ${item.note || ''} ${item.spoor}`.toLowerCase();
          const matchesQuery = !query || haystack.includes(query);
          return matchesCat && matchesQuery;
        });

        countEl.textContent = `${filtered.length} van ${CASES.length} zaken zichtbaar`;
        emptyEl.hidden = filtered.length > 0;

        const frag = document.createDocumentFragment();
        filtered.forEach((item) => {
          const article = document.createElement('article');
          article.className = 'ecli-card';

          const top = document.createElement('div');
          top.className = 'ecli-top';

          const codeEl = document.createElement('span');
          codeEl.className = 'ecli-code';
          codeEl.textContent = item.ecli;

          const actions = document.createElement('div');
          actions.className = 'ecli-actions';

          const spoorBadge = document.createElement('span');
          spoorBadge.className = 'badge';
          spoorBadge.textContent = item.spoor;
          actions.appendChild(spoorBadge);

          const catBadge = document.createElement('span');
          catBadge.className = item.corrected ? 'badge badge-warn' : 'badge';
          catBadge.textContent = item.corrected ? 'Gecorrigeerd' : item.categoryLabel;
          actions.appendChild(catBadge);

          if (item.isNL) {
            const link = document.createElement('a');
            link.href = `https://uitspraken.rechtspraak.nl/details?id=${encodeURIComponent(item.ecli)}`;
            link.target = '_blank';
            link.rel = 'noopener noreferrer';
            link.style.fontSize = '0.8rem';
            link.style.fontWeight = '600';
            link.textContent = 'Rechtspraak.nl ↗';
            actions.appendChild(link);
          }

          const copyBtn = document.createElement('button');
          copyBtn.type = 'button';
          copyBtn.className = 'copy-ecli-btn';
          copyBtn.textContent = 'Kopieer';
          copyBtn.addEventListener('click', () => copyText(item.ecli, copyBtn));
          actions.appendChild(copyBtn);

          top.appendChild(codeEl);
          top.appendChild(actions);

          const meta = document.createElement('div');
          meta.className = 'ecli-meta';
          meta.textContent = `${item.court} — ${item.date}`;

          const desc = document.createElement('p');
          desc.className = 'ecli-desc';
          desc.textContent = item.summary;

          article.appendChild(top);
          article.appendChild(meta);
          article.appendChild(desc);

          if (item.note) {
            const noteEl = document.createElement('p');
            noteEl.className = 'ecli-note';
            noteEl.textContent = item.note;
            article.appendChild(noteEl);
          }

          frag.appendChild(article);
        });

        listEl.appendChild(frag);
      };

      filterBtns.forEach((btn) => {
        btn.addEventListener('click', () => {
          activeFilter = btn.dataset.filter;
          filterBtns.forEach((b) => b.classList.toggle('active', b === btn));
          renderCases();
        });
      });

      searchInput.addEventListener('input', renderCases);

      // 4. Volledige Spoor A-lijst kopiëren
      const copySpoorABtn = document.getElementById('copy-spoor-a');
      copySpoorABtn.addEventListener('click', () => {
        const text = document.getElementById('spoor-a-content').innerText.trim();
        copyText(text, copySpoorABtn);
      });

      renderCases();
    })();
  </script>
</body>
</html>
