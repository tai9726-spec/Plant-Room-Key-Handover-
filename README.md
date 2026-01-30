# Plant-Room-Key-Handover-
Plant Room Key Handover
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Plant Room Key Handover</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: #f3f4f6;
      color: #2e61d9;
      padding: 24px;
    }
    .shell {
      max-width: 1280px;
      margin: 0 auto;
      background: #ffffff;
      border-radius: 16px;
      box-shadow: 0 18px 40px rgba(15,23,42,0.12);
      overflow: hidden;
      border: 1px solid #e5e7eb;
    }
    header {
      padding: 18px 24px;
      border-bottom: 1px solid #e5e7eb;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      background: #66a5ed;
    }
    header h1 {
      font-size: 18px;
      font-weight: 600;
      color: #2e61d9;
    }
    header p {
      font-size: 13px;
      color: #1055e0;
      margin-top: 2px;
    }
    header .meta {
      font-size: 12px;
      color: #1055e0;
      text-align: right;
    }
    header .meta strong { font-weight: 600; }

    main { padding: 18px 20px 22px; }

    .tabs {
      display: inline-flex;
      padding: 3px;
      border-radius: 999px;
      background: #f3f4f6;
      border: 1px solid #e5e7eb;
      margin-bottom: 16px;
      gap: 3px;
    }
    .tab-button {
      border: none;
      background: transparent;
      padding: 6px 14px;
      border-radius: 999px;
      font-size: 13px;
      color: #6b7280;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 4px;
      transition: all 0.15s ease;
    }
    .tab-button span.icon { font-size: 14px; }
    .tab-button.active {
      background: #ffffff;
      color: #111827;
      box-shadow: 0 1px 3px rgba(15,23,42,0.12);
    }
    .tab-content { display: none; }
    .tab-content.active { display: block; }

    .badge-pill {
      display: inline-flex;
      align-items: center;
      padding: 3px 8px;
      border-radius: 999px;
      background: #eff6ff;
      color: #1d4ed8;
      font-size: 11px;
      font-weight: 500;
      gap: 4px;
    }

    .row { display: flex; flex-wrap: wrap; gap: 12px; }
    .col-2 { flex: 2 1 0; min-width: 0; }
    .col-1 { flex: 1 1 0; min-width: 0; }

    .section {
      background: #ffffff;
      border-radius: 12px;
      border: 1px solid #e5e7eb;
      padding: 14px 14px 12px;
      margin-bottom: 12px;
    }
    .section-title {
      font-size: 13px;
      font-weight: 600;
      color: #111827;
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .section-title small {
      font-size: 11px;
      color: #9ca3af;
      font-weight: 400;
    }

    .stat-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(180px,1fr));
      gap: 10px;
    }
    .stat-card {
      border-radius: 10px;
      border: 1px solid #e5e7eb;
      background: #f9fafb;
      padding: 10px 12px;
    }
    .stat-label {
      font-size: 11px;
      color: #6b7280;
      margin-bottom: 2px;
    }
    .stat-value {
      font-size: 20px;
      font-weight: 600;
      color: #111827;
    }
    .stat-sub {
      font-size: 11px;
      color: #9ca3af;
      margin-top: 2px;
    }

    .progress-row {
      display: flex;
      justify-content: space-between;
      font-size: 11px;
      color: #4b5563;
      margin-bottom: 4px;
    }
    .progress-bar-shell {
      width: 100%;
      height: 8px;
      border-radius: 999px;
      background: #e5e7eb;
      overflow: hidden;
    }
    .progress-bar-fill {
      height: 100%;
      border-radius: 999px;
      background: linear-gradient(90deg,#4f46e5,#6366f1);
      width: 0%;
      transition: width 0.3s ease;
    }

    .tray-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(170px,1fr));
      gap: 10px;
      margin-top: 4px;
    }
    .tray-card {
      border-radius: 10px;
      border: 1px solid #e5e7eb;
      padding: 10px 11px;
      background: #ffffff;
      cursor: pointer;
      transition: box-shadow 0.15s ease, transform 0.15s ease, border-color 0.15s ease;
    }
    .tray-card:hover {
      box-shadow: 0 4px 10px rgba(15,23,42,0.08);
      transform: translateY(-1px);
      border-color: #d1d5db;
    }
    .tray-code {
      font-size: 11px;
      font-weight: 600;
      color: #6b7280;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      margin-bottom: 2px;
    }
    .tray-main {
      font-size: 13px;
      font-weight: 600;
      color: #111827;
      margin-bottom: 4px;
    }
    .tray-line {
      font-size: 11px;
      color: #4b5563;
    }
    .tray-line strong { font-weight: 600; }
    .tray-pill {
      margin-top: 6px;
      display: inline-flex;
      align-items: center;
      padding: 2px 7px;
      border-radius: 999px;
      background: #f3f4f6;
      color: #6b7280;
      font-size: 10px;
      gap: 4px;
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
      gap: 10px 12px;
    }
    .form-group { display: flex; flex-direction: column; }
    label {
      font-size: 11px;
      color: #4b5563;
      margin-bottom: 3px;
      font-weight: 500;
    }
    input, select, textarea {
      font-family: inherit;
      font-size: 13px;
      padding: 7px 8px;
      border-radius: 8px;
      border: 1px solid #d1d5db;
      background: #ffffff;
      transition: border-color 0.15s ease, box-shadow 0.15s ease;
    }
    input:focus, select:focus, textarea:focus {
      outline: none;
      border-color: #4f46e5;
      box-shadow: 0 0 0 1px rgba(79,70,229,0.4);
    }
    textarea { resize: vertical; min-height: 60px; }

    .btn {
      border-radius: 999px;
      padding: 7px 14px;
      font-size: 12px;
      font-weight: 500;
      border: none;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 5px;
    }
    .btn-primary {
      background: #4f46e5;
      color: #ffffff;
    }
    .btn-primary:hover { background: #4338ca; }
    .btn-ghost {
      background: #f3f4f6;
      color: #4b5563;
    }
    .btn-ghost:hover { background: #e5e7eb; }
    .btn-cancel { background: #f97316; color: #ffffff; }
    .btn-cancel:hover { background: #ea580c; }
    .btn-danger { background: #ef4444; color:#ffffff; }
    .btn-danger:hover { background:#dc2626; }
    .btn-sm { padding: 5px 10px; font-size: 11px; }

    .btn-row {
      display: flex;
      gap: 6px;
      margin-top: 8px;
      flex-wrap: wrap;
    }

    .success {
      display: none;
      margin-bottom: 10px;
      padding: 6px 10px;
      border-radius: 8px;
      background: #ecfdf3;
      color: #15803d;
      font-size: 12px;
      border: 1px solid #bbf7d0;
    }
    .success.show { display: block; }

    .list-empty {
      text-align: center;
      padding: 18px 6px;
      font-size: 12px;
      color: #9ca3af;
    }

    .record-list .item {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      padding: 8px 8px;
      border-radius: 8px;
      border: 1px solid #e5e7eb;
      background: #ffffff;
      margin-bottom: 6px;
      gap: 8px;
    }
    .record-main {
      font-size: 12px;
      color: #111827;
      font-weight: 500;
      margin-bottom: 2px;
    }
    .record-meta {
      font-size: 11px;
      color: #6b7280;
      line-height: 1.4;
    }
    .tag {
      display: inline-flex;
      align-items: center;
      padding: 2px 6px;
      border-radius: 999px;
      font-size: 10px;
      font-weight: 500;
      margin-right: 4px;
    }
    .tag-jv { background:#eff6ff; color:#1d4ed8; }
    .tag-ha { background:#f5f3ff; color:#6d28d9; }
    .tag-cancelled { background:#fef3c7; color:#92400e; }

    .room-list-item {
      padding: 7px 8px;
      border-radius: 8px;
      border: 1px solid #e5e7eb;
      font-size: 12px;
      display: flex;
      justify-content: space-between;
      margin-bottom: 5px;
      background: #ffffff;
    }
    .room-list-meta {
      font-size: 11px;
      color: #6b7280;
      margin-top: 2px;
    }

    .chart-wrapper { height: 260px; }

    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(15,23,42,0.45);
      align-items: center;
      justify-content: center;
      z-index: 40;
    }
    .modal.show { display: flex; }
    .modal-box {
      background: #ffffff;
      border-radius: 10px;
      padding: 14px 14px 12px;
      width: 320px;
      box-shadow: 0 18px 40px rgba(15,23,42,0.4);
      border: 1px solid #e5e7eb;
      font-size: 13px;
    }
    .modal-title {
      font-weight: 600;
      margin-bottom: 6px;
    }
    .modal-body {
      font-size: 12px;
      color: #4b5563;
      margin-bottom: 10px;
    }
    .modal-actions {
      display: flex;
      justify-content: flex-end;
      gap: 6px;
    }

    @media (max-width: 768px) {
      body { padding: 12px; }
      header { flex-direction: column; align-items: flex-start; }
      header .meta { text-align: left; }
    }
  </style>
</head>
<body>
<div class="shell">
  <header>
    <div>
      <h1>Plant Room Key Handover</h1>
      <p>Per-room JV → HA → EMSD handover with tray-based overview</p>
    </div>
    <div class="meta">
      <div>Total plant rooms: <strong>366</strong></div>
      <div>LG4 – 29/F</div>
    </div>
  </header>

  <main>
    <div id="successMessage" class="success"></div>

    <div class="tabs">
      <button class="tab-button active" data-tab="tab-dashboard">
        <span class="icon">📊</span>Tray dashboard
      </button>
      <button class="tab-button" data-tab="tab-input">
        <span class="icon">📝</span>Handover input
      </button>
      <button class="tab-button" data-tab="tab-Analytics">
        <span class="icon">📈</span>Analytics
      </button>
    </div>

    <!-- DASHBOARD -->
    <section id="tab-dashboard" class="tab-content active">
      <div class="row">
        <div class="col-2">
          <div class="section">
            <div class="section-title">
              <span>Overall progress</span>
              <span class="badge-pill">Live summary</span>
            </div>
            <div class="stat-grid">
              <div class="stat-card">
                <div class="stat-label">Total plant rooms</div>
                <div class="stat-value">366</div>
                <div class="stat-sub">LG4 – 29/F</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">JV → HA completed</div>
                <div class="stat-value" id="dashJVCount">0</div>
                <div class="stat-sub">Active only</div>
              </div>
              <div class="stat-card">
                <div class="stat-label">HA → EMSD completed</div>
                <div class="stat-value" id="dashHACount">0</div>
                <div class="stat-sub">Active only</div>
              </div>
            </div>
            <div style="margin-top:10px;">
              <div class="progress-row">
                <span>JV → HA</span>
                <span id="jvProgressText">0 / 366 (0%)</span>
              </div>
              <div class="progress-bar-shell">
                <div id="jvProgressBar" class="progress-bar-fill"></div>
              </div>
            </div>
            <div style="margin-top:8px;">
              <div class="progress-row">
                <span>HA → EMSD</span>
                <span id="haProgressText">0 / 366 (0%)</span>
              </div>
              <div class="progress-bar-shell">
                <div id="haProgressBar" class="progress-bar-fill"></div>
              </div>
            </div>
          </div>

          <div class="section" style="margin-top:10px;">
            <div class="section-title">
              <span>Tray status</span>
              <small>Click a tray to see its rooms</small>
            </div>
            <div id="trayGrid" class="tray-grid"></div>
          </div>
        </div>

        <div class="col-1">
          <div class="section" id="trayRoomPanel" style="display:none;">
            <div class="section-title">
              <span id="trayRoomTitle">Tray – rooms</span>
            </div>
            <div id="trayRoomBody"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- INPUT -->
    <section id="tab-input" class="tab-content">
      <div class="section">
        <div class="section-title">
          <span>JV → HA handover</span>
          <small>Select floor → room, details auto-fill</small>
        </div>
        <div class="form-grid">
          <div class="form-group">
            <label>Floor *</label>
            <select id="jvFloor" onchange="updateJVRooms()">
              <option value="">Select floor</option>
            </select>
          </div>
          <div class="form-group">
            <label>Room name *</label>
            <select id="jvRoom" onchange="updateJVRoomDetails()">
              <option value="">Select floor first</option>
            </select>
          </div>
          <div class="form-group">
            <label>Door number</label>
            <input id="jvDoor" type="text" readonly placeholder="Auto-filled">
          </div>
          <div class="form-group">
            <label>Key code *</label>
            <input id="jvLock" type="text" readonly placeholder="Auto-filled">
          </div>
          <div class="form-group">
            <label>Handover date *</label>
            <input id="jvDate" type="date">
          </div>
          <div class="form-group">
            <label>Handed by (JV)</label>
            <input id="jvFrom" type="text" placeholder="e.g. John (JV)">
          </div>
          <div class="form-group">
            <label>Received by (HA)</label>
            <input id="jvTo" type="text" placeholder="e.g. Mike (HA)">
          </div>
          <div class="form-group">
            <label>Remarks</label>
            <textarea id="jvNotes" placeholder="Optional"></textarea>
          </div>
        </div>
        <div class="btn-row">
          <button class="btn btn-primary" onclick="addRecord('jv-ha')">Save JV → HA record</button>
          <button class="btn btn-ghost" onclick="exportCSV('jv-ha')">Export JV → HA CSV</button>
        </div>
      </div>

      <div class="section">
        <div class="section-title">
          <span>JV → HA records (latest)</span>
        </div>
        <div id="jvRecordList" class="record-list"></div>
      </div>

      <div class="section">
        <div class="section-title">
          <span>HA → EMSD handover</span>
          <small>Same flow as JV → HA</small>
        </div>
        <div class="form-grid">
          <div class="form-group">
            <label>Floor *</label>
            <select id="haFloor" onchange="updateHARooms()">
              <option value="">Select floor</option>
            </select>
          </div>
          <div class="form-group">
            <label>Room name *</label>
            <select id="haRoom" onchange="updateHARoomDetails()">
              <option value="">Select floor first</option>
            </select>
          </div>
          <div class="form-group">
            <label>Door number</label>
            <input id="haDoor" type="text" readonly placeholder="Auto-filled">
          </div>
          <div class="form-group">
            <label>Key code *</label>
            <input id="haLock" type="text" readonly placeholder="Auto-filled">
          </div>
          <div class="form-group">
            <label>Handover date *</label>
            <input id="haDate" type="date">
          </div>
          <div class="form-group">
            <label>Handed by (HA)</label>
            <input id="haFrom" type="text" placeholder="e.g. Mike (HA)">
          </div>
          <div class="form-group">
            <label>Received by (EMSD)</label>
            <input id="haTo" type="text" placeholder="e.g. David (EMSD)">
          </div>
          <div class="form-group">
            <label>Remarks</label>
            <textarea id="haNotes" placeholder="Optional"></textarea>
          </div>
        </div>
        <div class="btn-row">
          <button class="btn btn-primary" onclick="addRecord('ha-emsd')">Save HA → EMSD record</button>
          <button class="btn btn-ghost" onclick="exportCSV('ha-emsd')">Export HA → EMSD CSV</button>
        </div>
      </div>

      <div class="section">
        <div class="section-title">
          <span>HA → EMSD records (latest)</span>
        </div>
        <div id="haRecordList" class="record-list"></div>
      </div>
    </section>

    <!-- Analytics -->
    <section id="tab-Analytics" class="tab-content">
      <div class="section">
        <div class="section-title">
          <span>Tray completion chart</span>
          <small>Per tray: JV → HA vs HA → EMSD</small>
        </div>
        <div class="chart-wrapper">
          <canvas id="systemComparisonChart"></canvas>
        </div>
      </div>
      <div class="section">
        <div class="section-title">
          <span>Tray summary table</span>
        </div>
        <div id="systemStats"></div>
      </div>
    </section>
  </main>
</div>

<!-- Cancel modal -->
<div id="recordCancelModal" class="modal">
  <div class="modal-box">
    <div class="modal-title">Cancel record</div>
    <div class="modal-body">
      Mark this record as <strong>CANCELLED</strong>?<br>
      It will be excluded from statistics but still kept in the list.
    </div>
    <div class="modal-actions">
      <button class="btn btn-ghost btn-sm" onclick="closeRecordCancelModal()">Keep active</button>
      <button class="btn btn-cancel btn-sm" onclick="confirmRecordCancel()">Cancel record</button>
    </div>
  </div>
</div>

<script>
  const plantRoomData = [
        { floor: "LG4", room: "FAN ROOM", door: "LG4-038", lock: "MKDB-KA3", system: "AC" },
        { floor: "LG4", room: "ELECT. (1)", door: "LG4-012", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG4", room: "ELECT. (2)", door: "LG4-027", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG4", room: "ELV RM. (CBS INSIDE) (1)", door: "LG4-024", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG4", room: "ELV RM. (CBS INSIDE) (2)", door: "LG4-025", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG4", room: "ELV (1)", door: "LG4-019", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG4", room: "ELV (2)", door: "LG4-020", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG4", room: "9 NOS. F.S. INLETS CABINET", door: "N/A", lock: "N/A", system: "FS" },
        { floor: "LG4", room: "DRENCHER CONTROL VALVE RM", door: "LG4-047", lock: "MKDD-KD2", system: "FS" },
        { floor: "LG4", room: "FIRE CONTROL CENTRE", door: "LG4-004", lock: "MKDD-KD3", system: "FS" },
        { floor: "LG4", room: "2 NOS. SPR INLET & 2 NOS. DRENCHER INLET & 1 NO. FOAM INLET CABINET", door: "N/A", lock: "N/A", system: "FS" },
        { floor: "LG4", room: "NOVEC 1230 FOR LG4 - DG STORE (CAT 5) (INFLAMMABLES)", door: "LG4-033A", lock: "MKDD-KA1", system: "FS" },
        { floor: "LG4", room: "WATER TANK & PUMP ROOM", door: "LG4-006/LG4-007", lock: "MKDC-KA1", system: "WS" },
        { floor: "LG4", room: "WATER INLET AND METER Room", door: "LG4-003", lock: "MKDC-KD1", system: "WS" },
        { floor: "LG4", room: "WATER INLET AND METER CABINET", door: "AP1/AP3", lock: "MKDC-KD1", system: "WS" },
        { floor: "LG3", room: "CRAC", door: "LG3-003", lock: "MKDB-KA5", system: "AC" },
        { floor: "LG3", room: "ELECT. (1)", door: "LG3-022", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG3", room: "ELECT. (2)", door: "LG3-134", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG3", room: "ELV RM. (CBS INSIDE)", door: "LG3-015", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG3", room: "ELV (2)", door: "LG3-029", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG3", room: "ELV RM. (CBS INSIDE)", door: "LG3-031", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG3", room: "ELV (1)", door: "LG3-030", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG3", room: "LV SWITCH ROOM (1)", door: "LG3-016", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (1)", door: "LG3-061", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (2)", door: "LG3-065", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (3)", door: "LG3-066", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (4)", door: "LG3-070", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (5)", door: "LG3-072", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (6)", door: "LG3-076", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (7)", door: "LG3-078", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "HV SWITCH ROOM (8)", door: "LG3-082", lock: "HKEDOOR", system: "EE" },
        { floor: "LG3", room: "TRANSFORMER ROOM (1)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (2)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (3)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (4)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (5)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (6)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (7)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "TRANSFORMER ROOM (8)", door: "N/A", lock: "N/A", system: "others" },
        { floor: "LG3", room: "SPRINKLER PUMP AND TANK ROOM", door: "LG3-007A", lock: "MKDC-KD4", system: "FS" },
        { floor: "LG3", room: "NOVEC 1230 FOR LG3 - MDF (TBE) ROOM", door: "LG3-011", lock: "MKDB-KA1", system: "FS" },
        { floor: "LG3", room: "NOVEC 1230 FOR LG3 - PABX ROOM", door: "LG3-008", lock: "MKDB-KA1", system: "FS" },
        { floor: "LG3", room: "NOVEC 1230 FOR LG3 - COMMON TEL. EQ. RM", door: "LG3-009", lock: "MKDB-KA1", system: "FS" },
        { floor: "LG3", room: "FLUSHING WATER PUMP & TANK ROOM", door: "LG3-002", lock: "MKDC-KD2", system: "WS" },
        { floor: "LG2", room: "CCMS CONTROL RM.", door: "LG2-001", lock: "N/A", system: "AC" },
        { floor: "LG2", room: "ELECT. (1)", door: "LG2-016", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG2", room: "ELECT. (2)", door: "LG2-023", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG2", room: "ELV RM. (CBS INSIDE) (1)", door: "LG2-017", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG2", room: "ELV RM. (CBS INSIDE) (2)", door: "LG2-021", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG2", room: "ELV (1)", door: "LG2-019", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG2", room: "ELV (2)", door: "LG2-020", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG2", room: "ELV RM.", door: "LG2-018", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG2", room: "LV SWITCH ROOM (2)", door: "LG2-027/LG2-029", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (3)", door: "LG2-031/LG2-033", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (4)", door: "LG2-040", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (5)", door: "LG2-042", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (6)", door: "LG2-047", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (7)", door: "LG2-049A/LG2-050", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "LV SWITCH ROOM (8)", door: "LG2-052/LG2-054", lock: "MKDA-KA1", system: "EE" },
        { floor: "LG2", room: "UPS ROOM (FOR CCMS)", door: "LG2-003", lock: "MKDA-KD2", system: "AC" },
        { floor: "LG2", room: "EL ROOM", door: "LG2-062", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG2", room: "FS COMMON PUMP & TANK ROOM (MAIN FS & DRENCHER PUMP)", door: "LG2-081", lock: "MKDD-KD1", system: "FS" },
        { floor: "LG2", room: "NOVEC 1230 FOR LG2 - UPS ROOM (FOR CCMS)", door: "LG2-077", lock: "MKDD-KA1", system: "FS" },
        { floor: "LG1", room: "AHU ROOM", door: "LG1-037/LG1-038", lock: "MKDB-KA1", system: "AC" },
        { floor: "LG1", room: "LOW-ZONE HOT WATER PLANTROOM", door: "LG1-060", lock: "MKDC-KD3", system: "AC" },
        { floor: "LG1", room: "ELECT ROOM (1)", door: "LG1-016", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG1", room: "ELECT ROOM (2)", door: "LG1-034", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG1", room: "ELV RM. (CBS INSIDE) (1)", door: "LG1-015", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG1", room: "ELV RM. (CBS INSIDE) (2)", door: "LG1-035", lock: "MKDA-KA2", system: "EE" },
        { floor: "LG1", room: "EV CHARGER CABINET", door: "AP3-F1", lock: "MKDC-KA3", system: "EE" },
        { floor: "LG1", room: "ELV ROOM (1)", door: "LG1-014", lock: "MKDA-KA2", system: "ELV" },
        { floor: "LG1", room: "ELV ROOM (2)", door: "LG1-036", lock: "MKDA-KA2", system: "ELV" },
        { floor: "G/F", room: "ELECT ROOM (1)", door: "GF-034", lock: "MKDA-KA2", system: "EE" },
        { floor: "G/F", room: "ELECT ROOM (2)", door: "GF-043", lock: "MKDA-KA2", system: "EE" },
        { floor: "G/F", room: "ELV RM. (CBS INSIDE) (1)", door: "GF-033", lock: "MKDA-KA2", system: "EE" },
        { floor: "G/F", room: "ELV RM. (CBS INSIDE) (2)", door: "GF-042", lock: "MKDA-KA2", system: "EE" },
        { floor: "G/F", room: "UPS ROOM (FOR ELV) (1)", door: "GF-093", lock: "MKDA-KA6", system: "ELV" },
        { floor: "G/F", room: "UPS ROOM (FOR ELV) (2)", door: "GF-094", lock: "MKDA-KA6", system: "ELV" },
        { floor: "G/F", room: "8 NOS. FS INLET & 1NO. SPR. INLET & 1 NO. DRENCHER INLET CAB.", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "G/F", room: "1 NO. F.S. INLET & 1 NO. SPR. INLET & I NO. DRENCHER INLET & 1 NO. FOAM INLET CAB.", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "G/F", room: "WATER INTERMEDIATE BOOSTER PUMP ROOM FOR FOAM SYSTEM", door: "GF-080", lock: "MKDD-KD6", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 FOR GF - PETROL INTERCEPTOR FOR HELIPAD", door: "GF-083", lock: "MKDD-KA1", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 FOR GF - DG STORE (CAT 2) - MA4, MA7", door: "GF-050", lock: "MKDD-KA1", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 FOR GF - DG STORE (CAT 2) - OXY", door: "GF-053", lock: "MKDD-KA1", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 FOR GF - DG STORE (CAT 2) - N20", door: "GF-088", lock: "MKDD-KA1", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 ROOM - UPS ROOM (FOR ELV) (1)", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "G/F", room: "NOVEC 1230 ROOM - UPS ROOM (FOR ELV) (2)", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "G/F", room: "ESCALATOR PIT (ESC-1)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "G/F", room: "ESCALATOR PIT (ESC-2)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "G/F", room: "DG STORE (CAT 2) - MA4, MA7", door: "GF-029", lock: "MKAS-KD5", system: "MG" },
        { floor: "G/F", room: "DG STORE (CAT2, O2/N2O)", door: "GF-052", lock: "MKAS-KD7", system: "MG" },
        { floor: "G/F", room: "DG STORE (CAT2, CO2)", door: "GF-044B", lock: "MKAS-KD6", system: "MG" },
        { floor: "G/F", room: "DG STORE (CAT2, N2O)", door: "GF-030", lock: "MKAS-KD8", system: "MG" },
        { floor: "G/F", room: "DG STORE (CAT2, OXY)", door: "GF-031", lock: "MKAS-KD9", system: "MG" },
        { floor: "G/F", room: "MEDICAL GAS MA4, CA11, CA14, SA7", door: "GF-090/GF-095", lock: "MKDB-KA7", system: "MG" },
        { floor: "G/F", room: "WRKM CTRL RM", door: "GF-002/GF-003", lock: "MKCG-KA5", system: "ELV" },
        { floor: "G/F", room: "ELV ROOM (1)", door: "GF-032", lock: "MKDA-KA2", system: "ELV" },
        { floor: "G/F", room: "ELV ROOM (2)", door: "GF-041", lock: "MKDA-KA2", system: "ELV" },
        { floor: "G/F", room: "FUEL PUMP ROOM (GENSET) (NON-FSI)", door: "GF-076", lock: "MKDE-KA3", system: "GE" },
        { floor: "G/F", room: "FUEL PUMP ROOM (GENSET) (FSI)", door: "GF-077", lock: "MKDE-KA3", system: "GE" },
        { floor: "G/F", room: "UNDERGROUND FUEL TANK CHAMBER AND TRENCH.", door: "N/A", lock: "N/A", system: "GE" },
        { floor: "G/F", room: "UNDERGROUND FUEL TANK CHAMBER AND TRENCH.", door: "N/A", lock: "N/A", system: "TT" },
        { floor: "G/F", room: "DAY TANK ROOM", door: "GF-048B/GF-060", lock: "MKDG-KD1", system: "TT" },
        { floor: "G/F", room: "STEAM BOILER ROOM", door: "GF-062/GF-067/GF-068", lock: "MKDG-KA2", system: "TT" },
        { floor: "G/F", room: "BOILER DUTY ROOM", door: "GF-061/GF-063/GF-064", lock: "MKDG-KA2", system: "TT" },
        { floor: "G/F", room: "FUEL PUMP ROOM (STEAM BOILER) (NON-FSI)", door: "GF-071", lock: "MKDG-KA1", system: "TT" },
        { floor: "G/F", room: "FUEL PUMP ROOM (STEAM BOILER) (FSI)", door: "GF-072", lock: "MKDG-KA1", system: "TT" },
        { floor: "G/F", room: "UNDERGROUND FUEL TANK CHAMBER AND TRENCH.", door: "N/A", lock: "N/A", system: "TT" },
        { floor: "G/F", room: "PETROL INTERCEPTOR FOR HELIPAD", door: "GF-084/GF-085", lock: "MKDE-KA1", system: "WS" },
        { floor: "G/F", room: "Air Compressor Room", door: "N/A", lock: "N/A", system: "MG" },
        { floor: "M/F", room: "Novec 1230 Cabinet", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "M/F", room: "Novec 1230 Cabinet", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "1/F", room: "ELECT ROOM (1)", door: "L1-118", lock: "MKDA-KA2", system: "EE" },
        { floor: "1/F", room: "ELECT ROOM (2)", door: "L1-122B", lock: "MKDA-KA2", system: "EE" },
        { floor: "1/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L1-119", lock: "MKDA-KA2", system: "EE" },
        { floor: "1/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L1-123B", lock: "MKDA-KA2", system: "EE" },
        { floor: "1/F", room: "PRE-ACTION ROOM - CT CTRL (CT SCANNER ROOM)", door: "L1-068", lock: "MKAD-KD7", system: "MG" },
        { floor: "1/F", room: "PRE-ACTION CABINET FOR MINOR OT STORE EQUIPMENT", door: "L1-020", lock: "MKAA-KD7", system: "FS" },
        { floor: "1/F", room: "ESCALATOR PIT (ESC-3)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "1/F", room: "ESCALATOR PIT (ESC-4)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "1/F", room: "ESCALATOR PIT (ESC-5)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "1/F", room: "ESCALATOR PIT (ESC-6)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "1/F", room: "ELV ROOM (1)", door: "L1-120", lock: "MKDA-KA2", system: "ELV" },
        { floor: "1/F", room: "ELV ROOM (2)", door: "L1-148A", lock: "MKDA-KA2", system: "ELV" },
        { floor: "2/F", room: "AHU FOR L2 & L1", door: "L2-047/L2-048/L2-049", lock: "MKDB-KA1", system: "AC" },
        { floor: "2/F", room: "ELECT ROOM (1)", door: "L2-095", lock: "MKDA-KA2", system: "EE" },
        { floor: "2/F", room: "ELECT ROOM (2)", door: "L2-109", lock: "MKDA-KA2", system: "EE" },
        { floor: "2/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L2-096", lock: "MKDA-KA2", system: "EE" },
        { floor: "2/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L2-110", lock: "MKDA-KA2", system: "EE" },
        { floor: "2/F", room: "ESCALATOR PIT (ESC-7)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "2/F", room: "ESCALATOR PIT (ESC-8)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "2/F", room: "ESCALATOR PIT (ESC-9)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "2/F", room: "ESCALATOR PIT (ESC-10)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "2/F", room: "ELV ROOM (1)", door: "L2-097", lock: "MKDA-KA2", system: "ELV" },
        { floor: "2/F", room: "ELV ROOM (2)", door: "L2-111", lock: "MKDA-KA2", system: "ELV" },
        { floor: "3/F", room: "AHU ROOM", door: "L3-035/L3-036", lock: "MKDB-KA1", system: "AC" },
        { floor: "3/F", room: "ELECT ROOM (1)", door: "L3-005", lock: "MKDA-KA2", system: "EE" },
        { floor: "3/F", room: "ELECT ROOM (2)", door: "L3-050", lock: "MKDA-KA2", system: "EE" },
        { floor: "3/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L3-006", lock: "MKDA-KA2", system: "EE" },
        { floor: "3/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L3-051", lock: "MKDA-KA2", system: "EE" },
        { floor: "3/F", room: "NON-FSI SWITCH ROOM-1", door: "L3-040/L3-044", lock: "MKDE-KA2", system: "SB" },
        { floor: "3/F", room: "NON-FSI SWITCH ROOM-2", door: "L3-041/L3-044", lock: "MKDE-KA2", system: "SB" },
        { floor: "3/F", room: "FSI SWITCH ROOM", door: "L3-048/L3-049", lock: "MKDE-KD2", system: "SB" },
        { floor: "3/F", room: "NON-FSI GENERATOR ROOM (1)", door: "L3-045/L3-044", lock: "MKDE-KA2", system: "GE" },
        { floor: "3/F", room: "FSI GENERATOR ROOM", door: "L3-046/L3-047", lock: "MKDE-KA4", system: "GE" },
        { floor: "3/F", room: "NOVEC 1230 FOR L3 - FUEL TANK ROOM", door: "L3-083A", lock: "MKDD-KA1", system: "FS" },
        { floor: "3/F", room: "LIFT MACHINE ROOM NO. L-26", door: "L3-080", lock: "MKDF-KA1", system: "LF" },
        { floor: "3/F", room: "ELV ROOM (1)", door: "L3-052", lock: "MKDA-KA2", system: "ELV" },
        { floor: "3/F", room: "ELV ROOM (2)", door: "L3-072", lock: "MKDA-KA2", system: "ELV" },
        { floor: "3/F", room: "FUEL TANK ROOM", door: "L3-062/L3-063", lock: "MKDE-KD1", system: "GE" },
        { floor: "3/F", room: "Novec 1230 Cabinet Door number L3-083", door: "L3-083", lock: "MKDD-KA1", system: "FS" },
        { floor: "4/F", room: "AHU ROOM", door: "L4-036", lock: "MKDB-KA1", system: "AC" },
        { floor: "4/F", room: "ELECT ROOM (1)", door: "L4-133", lock: "MKDA-KA2", system: "EE" },
        { floor: "4/F", room: "ELECT ROOM (2)", door: "L4-135", lock: "MKDA-KA2", system: "EE" },
        { floor: "4/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L4-132", lock: "MKDA-KA2", system: "EE" },
        { floor: "4/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L4-136", lock: "MKDA-KA2", system: "EE" },
        { floor: "4/F", room: "NON-FSI GENERATOR ROOM (2)", door: "L4-120/L4-121/L4-147B", lock: "MKDE-KA4", system: "GE" },
        { floor: "4/F", room: "ELV ROOM (1)", door: "L4-134", lock: "MKDA-KA2", system: "ELV" },
        { floor: "4/F", room: "ELV ROOM (2)", door: "L4-137", lock: "MKDA-KA2", system: "ELV" },
        { floor: "4/F", room: "PRE-ACTION CABINET FOR CT SCANNE 2 / CT COMP. RM", door: "AP2b-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "4/F", room: "PRE-ACTION CABINET FOR CT SCANNER 1, CT CTRL, IMAGE RM, IMAGE PROCESSING & VIEWING ROOMS", door: "AP2b-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "4/F", room: "PRE-ACTION CABIMET FOR SINGLE PLANE DSA C-ARM EXAM ROOM, BIPLANE DSA C-ARM CTRL RM, BIPLANE DSA C-ARM W ANGIOGRAPHY EXAM. ROOM", door: "AP2b-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "4/F", room: "PRE-ACTION CABINET ANGIOGRAPHY FOR ANGIOGRAPHY CT EXAM. ROOM, ANGIOGRAPHY - CT CONTROL ROOM & ANGIO COMP. RM", door: "AP2b-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "4/F", room: "ESCALATOR PIT (ESC-11)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "4/F", room: "ESCALATOR PIT (ESC-12)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "5/F", room: "AHU ROOM", door: "L5-143/L5-144", lock: "MKDB-KA1", system: "AC" },
        { floor: "5/F", room: "ELECT ROOM (1)", door: "L5-131", lock: "MKDA-KA2", system: "EE" },
        { floor: "5/F", room: "ELECT ROOM (2)", door: "L5-134", lock: "MKDA-KA2", system: "EE" },
        { floor: "5/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L5-132", lock: "MKDA-KA2", system: "EE" },
        { floor: "5/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L5-135", lock: "MKDA-KA2", system: "EE" },
        { floor: "5/F", room: "PRE-ACTION CABINET FOR MINOR OT", door: "N/A", lock: "N/A", system: "FS" },
        { floor: "5/F", room: "ELV ROOM (1)", door: "L5-133", lock: "MKDA-KA2", system: "ELV" },
        { floor: "5/F", room: "ELV ROOM (2)", door: "L5-136", lock: "MKDA-KA2", system: "ELV" },
        { floor: "6/F", room: "ELECT ROOM (1)", door: "L6-138", lock: "MKDA-KA2", system: "EE" },
        { floor: "6/F", room: "ELECT ROOM (2)", door: "L6-144", lock: "MKDA-KA2", system: "EE" },
        { floor: "6/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L6-139", lock: "MKDA-KA2", system: "EE" },
        { floor: "6/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L6-143", lock: "MKDA-KA2", system: "EE" },
        { floor: "6/F", room: "ELV ROOM (1)", door: "L6-140", lock: "MKDA-KA2", system: "ELV" },
        { floor: "6/F", room: "ELV ROOM (2)", door: "L6-144", lock: "MKDA-KA2", system: "ELV" },
        { floor: "7/F", room: "AHU ROOM", door: "L7-051/L7-137", lock: "MKDB-KA1", system: "AC" },
        { floor: "7/F", room: "ELECT ROOM (1)", door: "L7-032", lock: "MKDA-KA2", system: "EE" },
        { floor: "7/F", room: "ELECT ROOM (2)", door: "L7-156B", lock: "MKDA-KA2", system: "EE" },
        { floor: "7/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L7-033", lock: "MKDA-KA2", system: "EE" },
        { floor: "7/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L7-099", lock: "MKDA-KA2", system: "EE" },
        { floor: "7/F", room: "NOVEC 1230 ROOM FOR CINE SERVER ROOM (1, 2, 3)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "7/F", room: "ELV ROOM (1)", door: "L7-034", lock: "MKDA-KA2", system: "ELV" },
        { floor: "7/F", room: "ELV ROOM (2)", door: "L7-098", lock: "MKDA-KA2", system: "ELV" },
        { floor: "7/F", room: "PRE - ACTION CABINET", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "8/F", room: "ELECT ROOM (1)", door: "L8-055", lock: "MKDA-KA2", system: "EE" },
        { floor: "8/F", room: "ELECT ROOM (2)", door: "L8-134", lock: "MKDA-KA2", system: "EE" },
        { floor: "8/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L8-056", lock: "MKDA-KA2", system: "EE" },
        { floor: "8/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L8-135", lock: "MKDA-KA2", system: "EE" },
        { floor: "8/F", room: "ELV ROOM (1)", door: "L8-057", lock: "MKDA-KA2", system: "ELV" },
        { floor: "8/F", room: "ELV ROOM (2)", door: "L8-136", lock: "MKDA-KA2", system: "ELV" },
        { floor: "9/F", room: "ELECT ROOM (1)", door: "L9-119", lock: "MKDA-KA2", system: "EE" },
        { floor: "9/F", room: "ELECT ROOM (2)", door: "L9-135A", lock: "MKDA-KA2", system: "EE" },
        { floor: "9/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L9-120", lock: "MKDA-KA2", system: "EE" },
        { floor: "9/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L9-136", lock: "MKDA-KA2", system: "EE" },
        { floor: "9/F", room: "PRE-ACTION CABINET (OT-CA2, OT-5, CA2, FOT, OPERATING THEATRE 5, C-ARM 2, L 4)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "9/F", room: "PRE-ACTION CABINET (OT-L, OPERATING THEATRE CT L, LEAD-LINED)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "9/F", room: "PRE-ACTION CABINET (OT-CT, OT-ISO, OT-1, OT-CA1, OPERATING THEATRE C-ARM 1, 1, MRI ISO. OPERATING THEATRE)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "9/F", room: "PRE-ACTION CABINET (OT-2, OT-3, OPERATING THEATRE 2 & 3)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "9/F", room: "PRE-ACTION CABINET (OT-MRI, MRI MACHINE RM)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "9/F", room: "ELV ROOM (1)", door: "L9-121", lock: "MKDA-KA2", system: "ELV" },
        { floor: "9/F", room: "ELV ROOM (2)", door: "L9-137B", lock: "MKDA-KA2", system: "ELV" },
        { floor: "10/F", room: "AHU RM. (1) FOR LEVEL 5", door: "L10-067", lock: "MKDB-KA1", system: "AC" },
        { floor: "10/F", room: "AHU RM. (2) FOR LEVEL 8 (OT RM)", door: "L10-003/L10-010/L10-030/L10-063", lock: "MKDB-KA1", system: "AC" },
        { floor: "10/F", room: "AHU RM. (3) FOR LEVEL 9", door: "L10-064", lock: "MKDB-KA1", system: "AC" },
        { floor: "10/F", room: "ELECT ROOM (1)", door: "L10-017", lock: "MKDA-KA2", system: "EE" },
        { floor: "10/F", room: "ELECT ROOM (2)", door: "L10-053", lock: "MKDA-KA2", system: "EE" },
        { floor: "10/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L10-018", lock: "MKDA-KA2", system: "EE" },
        { floor: "10/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L10-052", lock: "MKDA-KA2", system: "EE" },
        { floor: "10/F", room: "UPS RM.", door: "L10-031", lock: "MKAL-KD2", system: "EE" },
        { floor: "10/F", room: "NOVEC 1230 ROOM (FOR UPS ROOM)", door: "L10-072", lock: "MKDD-KA1", system: "FS" },
        { floor: "10/F", room: "AGSS PLANT ROOM", door: "L10-005/L10-006", lock: "MKDB-KA8", system: "MG" },
        { floor: "10/F", room: "ELV ROOM (1)", door: "L10-019", lock: "MKDA-KA2", system: "ELV" },
        { floor: "10/F", room: "ELV ROOM (2)", door: "L10-051", lock: "MKDA-KA2", system: "ELV" },
        { floor: "11/F", room: "ELECT ROOM (1)", door: "L11-106", lock: "MKDA-KA2", system: "EE" },
        { floor: "11/F", room: "ELECT ROOM (2)", door: "L11-125", lock: "MKDA-KA2", system: "EE" },
        { floor: "11/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L11-107", lock: "MKDA-KA2", system: "EE" },
        { floor: "11/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L11-126", lock: "MKDA-KA2", system: "EE" },
        { floor: "11/F", room: "PRE-ACTION CABINET (OT-MIS 1/OT-MIS 2, 3, OPERATING THEATRE MIS 1 , MIS 2 & MIS 3)", door: "AP1-F1/AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "11/F", room: "PRE-ACTION CABINET (OT-4, OT-5, OPERATING THEATRE 4 & 5)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "11/F", room: "PRE-ACTION CABINET (ROB 2, OT-L, OPERATING THEATRE ROBOTIC 2 & L LEAD-LINED)", door: "AP1-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "11/F", room: "PRE-ACTION CABINET (OT1, 2, 3, OT-ISO, OPERATING THEATRE 1, 2, 3 & ISO. OPERATING THEATRE)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "11/F", room: "PRE-ACTION CABINET (OT-ROBOTIC 1, 2, OPERATING THEATRE 1)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "11/F", room: "ELV ROOM (1)", door: "L11-108", lock: "MKDA-KA2", system: "ELV" },
        { floor: "11/F", room: "ELV ROOM (2)", door: "L11-127", lock: "MKDA-KA2", system: "ELV" },
        { floor: "12/F", room: "AHU RM. (1) FOR LEVEL 10 (OT RM)", door: "L12-014/L12-015", lock: "MKDB-KA1", system: "AC" },
        { floor: "12/F", room: "AHU RM. (2) FOR LEVEL 10 (OT RM)", door: "L12-003/L12-011/L12-052/L12-053", lock: "MKDB-KA1", system: "FS" },
        { floor: "12/F", room: "AHU RM. (3) FOR LEVEL 10 (OT RM) FOR LEVEL 11", door: "L12-054/L12-055/L12-059", lock: "MKDB-KA1", system: "AC" },
        { floor: "12/F", room: "CRAC (1)", door: "L12-048", lock: "MKDB-KA5", system: "AC" },
        { floor: "12/F", room: "CRAC (2)", door: "L12-046", lock: "MKDB-KA5", system: "AC" },
        { floor: "12/F", room: "ELECT ROOM (1)", door: "L12-026", lock: "MKDA-KA2", system: "EE" },
        { floor: "12/F", room: "ELECT ROOM (2)", door: "L12-066", lock: "MKDA-KA2", system: "EE" },
        { floor: "12/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L12-025", lock: "MKDA-KA2", system: "EE" },
        { floor: "12/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L12-067", lock: "MKDA-KA2", system: "EE" },
        { floor: "12/F", room: "UPS RM.", door: "L12-061", lock: "MKA/N-KD1", system: "EE" },
        { floor: "12/F", room: "NOVEC 1230 ROOM (FOR UPS ROOM)", door: "L12-060", lock: "MKDD-KA1", system: "FS" },
        { floor: "12/F", room: "NOVEC 1230 ROOM (FOR UPS ROOM HA)", door: "L12-030", lock: "MKDD-KA1", system: "FS" },
        { floor: "12/F", room: "NOVEC 1230 ROOM (FOR IT DATA CENTRES HA - 01 & 02)", door: "L12-050", lock: "MKDD-KA1", system: "FS" },
        { floor: "12/F", room: "AGSS", door: "L12-005/L12-006", lock: "MKDB-KA8", system: "MG" },
        { floor: "12/F", room: "ELV ROOM (1)", door: "L12-024", lock: "MKDA-KA2", system: "ELV" },
        { floor: "12/F", room: "ELV ROOM (2)", door: "L12-065", lock: "MKDA-KA2", system: "ELV" },
        { floor: "13/F", room: "FAN ROOM FOR 12/F & 13/F", door: "L13-039/L13-040/L13-042/L13-120", lock: "MKDB-KA1", system: "AC" },
        { floor: "13/F", room: "AHU Room", door: "L13-038", lock: "MKDB-KA1", system: "AC" },
        { floor: "13/F", room: "ELECT ROOM (1)", door: "L13-030", lock: "MKDA-KA2", system: "EE" },
        { floor: "13/F", room: "ELECT ROOM (2)", door: "L13-031", lock: "MKDA-KA2", system: "EE" },
        { floor: "13/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L13-022A", lock: "MKDA-KA2", system: "EE" },
        { floor: "13/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L13-034", lock: "MKDA-KA2", system: "EE" },
        { floor: "13/F", room: "ELV ROOM (1)", door: "L13-032", lock: "MKDA-KA2", system: "ELV" },
        { floor: "13/F", room: "ELV ROOM (2)", door: "L13-033", lock: "MKDA-KA2", system: "ELV" },
        { floor: "13/F", room: "PNEUMATIC TUBE PLANTROOM", door: "L13-066", lock: "MKDB-KD4", system: "PT" },
        { floor: "14/F", room: "ELECT ROOM (1)", door: "L14-057", lock: "MKDA-KA2", system: "EE" },
        { floor: "14/F", room: "ELECT ROOM (2)", door: "L14-076", lock: "MKDA-KA2", system: "EE" },
        { floor: "14/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L14-058", lock: "MKDA-KA2", system: "EE" },
        { floor: "14/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L!4-079A", lock: "MKDA-KA2", system: "EE" },
        { floor: "14/F", room: "LIFT SHAFT FOR LIFT NO. L-1 (BOT BED LIFTS)", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "14/F", room: "LIFT SHAFT FOR LIFT NO. L-27", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "14/F", room: "LIFT SHAFT FOR LIFT NO. L-28", door: "N/A", lock: "N/A", system: "LF" },
        { floor: "14/F", room: "ELV ROOM (1)", door: "L14-059", lock: "MKDA-KA2", system: "ELV" },
        { floor: "14/F", room: "ELV ROOM (2)", door: "L14-078A", lock: "MKDA-KA2", system: "ELV" },
        { floor: "15/F", room: "FS DRENCHER PUMP & TANK ROOM", door: "L15-023", lock: "MKDD-KD8", system: "FS" },
        { floor: "16/F", room: "AHU ROOM", door: "L16-034/L16-035", lock: "MKDB-KA1", system: "AC" },
        { floor: "16/F", room: "ELECT ROOM (1)", door: "L16-028", lock: "MKDA-KA2", system: "EE" },
        { floor: "16/F", room: "ELECT ROOM (2)", door: "L16-029", lock: "MKDA-KA2", system: "EE" },
        { floor: "16/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L16-019", lock: "MKDA-KA2", system: "EE" },
        { floor: "16/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L16-020", lock: "MKDA-KA2", system: "EE" },
        { floor: "16/F", room: "ELV ROOM (1)", door: "L16-030", lock: "MKDA-KA2", system: "ELV" },
        { floor: "16/F", room: "ELV ROOM (2)", door: "L16-031", lock: "MKDA-KA2", system: "ELV" },
        { floor: "17/F", room: "AHU", door: "L17-007/L17-008", lock: "MKDB-KA1", system: "AC" },
        { floor: "17/F", room: "ELECT ROOM (1)", door: "L17-080", lock: "MKDA-KA2", system: "EE" },
        { floor: "17/F", room: "ELECT ROOM (2)", door: "L17-081", lock: "MKDA-KA2", system: "EE" },
        { floor: "17/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L17-159", lock: "MKDA-KA2", system: "EE" },
        { floor: "17/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L17-167", lock: "MKDA-KA2", system: "EE" },
        { floor: "17/F", room: "PRE-ACTION CABINET (OPERATING THEATRE 1)", door: "AP3-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "17/F", room: "PRE-ACTION CABINET (OPERATING THEATRE 2)", door: "AP1a-F1", lock: "MKDD-KA7", system: "FS" },
        { floor: "17/F", room: "ELV ROOM (1)", door: "L17-155", lock: "MKDA-KA2", system: "ELV" },
        { floor: "17/F", room: "ELV ROOM (2)", door: "L17-158", lock: "MKDA-KA2", system: "ELV" },
        { floor: "18/F", room: "AHU", door: "L18-037/L18-038/L18-142", lock: "MKDB-KA1", system: "AC" },
        { floor: "18/F", room: "ELECT ROOM (1)", door: "L18-070", lock: "MKDA-KA2", system: "EE" },
        { floor: "18/F", room: "ELECT ROOM (2)", door: "L18-071", lock: "MKDA-KA2", system: "EE" },
        { floor: "18/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L18-097", lock: "MKDA-KA2", system: "EE" },
        { floor: "18/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L18-104", lock: "MKDA-KA2", system: "EE" },
        { floor: "18/F", room: "ELV ROOM (1)", door: "L18-093", lock: "MKDA-KA2", system: "ELV" },
        { floor: "18/F", room: "ELV ROOM (2)", door: "L18-096", lock: "MKDA-KA2", system: "ELV" },
        { floor: "19/F", room: "AHU ROOM", door: "L19-067/L19-068", lock: "MKDB-KA1", system: "AC" },
        { floor: "19/F", room: "ELECT ROOM (1)", door: "L19-072", lock: "MKDA-KA2", system: "EE" },
        { floor: "19/F", room: "ELECT ROOM (2)", door: "L19-073", lock: "MKDA-KA2", system: "EE" },
        { floor: "19/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L19-087", lock: "MKDA-KA2", system: "EE" },
        { floor: "19/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L19-159", lock: "MKDA-KA2", system: "EE" },
        { floor: "19/F", room: "NOVEC 1230 ROOM FOR CIS SERVER", door: "L19-166/L19-167", lock: "MKDD-KA1", system: "FS" },
        { floor: "19/F", room: "ELV ROOM (1)", door: "L19-075", lock: "MKDA-KA2", system: "ELV" },
        { floor: "19/F", room: "ELV ROOM (2)", door: "L19-076", lock: "MKDA-KA2", system: "ELV" },
        { floor: "20/F", room: "AHU ROOM", door: "L20-043/L20-044", lock: "MKDB-KA1", system: "AC" },
        { floor: "20/F", room: "ELECT ROOM (1)", door: "L20-055", lock: "MKDA-KA2", system: "EE" },
        { floor: "20/F", room: "ELECT ROOM (2)", door: "L20-056", lock: "MKDA-KA2", system: "EE" },
        { floor: "20/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L20-098", lock: "MKDA-KA2", system: "EE" },
        { floor: "20/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L20-111", lock: "MKDA-KA2", system: "EE" },
        { floor: "20/F", room: "ELV ROOM (1)", door: "L20-112", lock: "MKDA-KA2", system: "ELV" },
        { floor: "20/F", room: "ELV ROOM (2)", door: "L20-113", lock: "MKDA-KA2", system: "ELV" },
        { floor: "21/F", room: "AHU", door: "L21-120/L21-121/L21-131/L21-132A", lock: "MKDB-KA1", system: "AC" },
        { floor: "21/F", room: "ELECT ROOM (1)", door: "L21-054", lock: "MKDA-KA2", system: "EE" },
        { floor: "21/F", room: "ELECT ROOM (2)", door: "L21-055", lock: "MKDA-KA2", system: "EE" },
        { floor: "21/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L21-065", lock: "MKDA-KA2", system: "EE" },
        { floor: "21/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L21-068", lock: "MKDA-KA2", system: "EE" },
        { floor: "21/F", room: "ELV ROOM (1)", door: "L21-069", lock: "MKDA-KA2", system: "ELV" },
        { floor: "21/F", room: "ELV ROOM (2)", door: "L21-070", lock: "MKDA-KA2", system: "ELV" },
        { floor: "22/F", room: "AHU", door: "L22-120/L22-121/L22-131/L22-132B", lock: "MKDB-KA1", system: "AC" },
        { floor: "22/F", room: "ELECT ROOM (1)", door: "L22-054", lock: "MKDA-KA2", system: "EE" },
        { floor: "22/F", room: "ELECT ROOM (2)", door: "L22-055", lock: "MKDA-KA2", system: "EE" },
        { floor: "22/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L22-065", lock: "MKDA-KA2", system: "EE" },
        { floor: "22/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L22-068", lock: "MKDA-KA2", system: "EE" },
        { floor: "22/F", room: "ELV ROOM (1)", door: "L22-069", lock: "MKDA-KA2", system: "ELV" },
        { floor: "22/F", room: "ELV ROOM (2)", door: "L22-070", lock: "MKDA-KA2", system: "ELV" },
        { floor: "23/F", room: "AHU", door: "L23-120/L23-121/L23-131/L23-132B", lock: "MKDB-KA1", system: "AC" },
        { floor: "23/F", room: "ELECT ROOM (1)", door: "L23-054", lock: "MKDA-KA2", system: "EE" },
        { floor: "23/F", room: "ELECT ROOM (2)", door: "L23-055", lock: "MKDA-KA2", system: "EE" },
        { floor: "23/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L23-065", lock: "MKDA-KA2", system: "EE" },
        { floor: "23/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L23-068", lock: "MKDA-KA2", system: "EE" },
        { floor: "23/F", room: "ELV ROOM (1)", door: "L23-069", lock: "MKDA-KA2", system: "ELV" },
        { floor: "23/F", room: "ELV ROOM (2)", door: "L23-070", lock: "MKDA-KA2", system: "ELV" },
        { floor: "24/F", room: "AHU", door: "L24-041/L24-053/L24-054/L24-088", lock: "MKDB-KA1", system: "AC" },
        { floor: "24/F", room: "ELECT ROOM (1)", door: "L24-059", lock: "MKDA-KA2", system: "EE" },
        { floor: "24/F", room: "ELECT ROOM (2)", door: "L24-060", lock: "MKDA-KA2", system: "EE" },
        { floor: "24/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L24-069", lock: "MKDA-KA2", system: "EE" },
        { floor: "24/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L24-076", lock: "MKDA-KA2", system: "EE" },
        { floor: "24/F", room: "ELV ROOM (1)", door: "L24-070", lock: "MKDA-KA2", system: "ELV" },
        { floor: "24/F", room: "ELV ROOM (2)", door: "L24-077", lock: "MKDA-KA2", system: "ELV" },
        { floor: "25/F", room: "ELECT ROOM (1)", door: "L24-029", lock: "MKDA-KA2", system: "EE" },
        { floor: "25/F", room: "ELECT ROOM (2)", door: "L25-030", lock: "MKDA-KA2", system: "EE" },
        { floor: "25/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L25-021", lock: "MKDA-KA2", system: "EE" },
        { floor: "25/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L25-033", lock: "MKDA-KA2", system: "EE" },
        { floor: "25/F", room: "ELV ROOM (1)", door: "L25-031", lock: "MKDA-KA2", system: "ELV" },
        { floor: "25/F", room: "ELV ROOM (2)", door: "L25-032", lock: "MKDA-KA2", system: "ELV" },
        { floor: "26/F", room: "AHU ROOM (1)", door: "L26-016/L26-017", lock: "MKDB-KA1", system: "AC" },
        { floor: "26/F", room: "AHU ROOM (2)", door: "L26-018/L26-019", lock: "MKDB-KA1", system: "AC" },
        { floor: "26/F", room: "HOT WATER PLANT ROOM", door: "L26-034/L26-035/L26-034A/L26-035A", lock: "MKDB-KA2", system: "AC" },
        { floor: "26/F", room: "HVAC PUMP ROOM", door: "L26-020/L26-021/L26-022", lock: "MKDB-KA6", system: "AC" },
        { floor: "26/F", room: "MCC ROOM", door: "L26-023/L26-024", lock: "MKDB-KA4", system: "AC" },
        { floor: "26/F", room: "ELECT ROOM (1)", door: "L26-025", lock: "MKDA-KA2", system: "EE" },
        { floor: "26/F", room: "ELECT ROOM (2)", door: "L26-026", lock: "MKDA-KA2", system: "EE" },
        { floor: "26/F", room: "ELV RM. (CBS INSIDE) (1)", door: "L26-040", lock: "MKDA-KA2", system: "EE" },
        { floor: "26/F", room: "ELV RM. (CBS INSIDE) (2)", door: "L26-041", lock: "MKDA-KA2", system: "EE" },
        { floor: "26/F", room: "SWITCH ROOM 'EA-5', 'EB-6'", door: "L26-070/L26-071", lock: "MKDA-KD1", system: "SB" },
        { floor: "26/F", room: "LIFT MACHINE ROOM (2) - LIFT NO. L-12, L-13, L-14 & L-15(ECMO)", door: "L26-028/L26-029", lock: "MKDF-KA1", system: "LF" },
        { floor: "26/F", room: "LIFT MACHINE ROOM (3) - LIFT NO. L-16 TO L-25", door: "L26-030/L26-031/L26-032/L26-033", lock: "MKDF-KA1", system: "LF" },
        { floor: "26/F", room: "NON-MEDICAL GAS & MEDICAL GAS PLANT ROOM", door: "L26-036/L26-037", lock: "MKDB-KA7", system: "MG" },
        { floor: "26/F", room: "ELV ROOM (1)", door: "L26-042", lock: "MKDA-KA2", system: "ELV" },
        { floor: "26/F", room: "ELV ROOM (2)", door: "L26-043", lock: "MKDA-KA2", system: "ELV" },
        { floor: "27/F", room: "CHILLER PLANT (1)", door: "N/A", lock: "N/A", system: "AC" },
        { floor: "27/F", room: "CHILLER PLANT (2)", door: "N/A", lock: "N/A", system: "AC" },
        { floor: "27/F", room: "FAN ROOM (1)", door: "L27-009/L27-10/L27-041/L27-042", lock: "MKDB-KA3", system: "AC" },
        { floor: "27/F", room: "FAN ROOM (2)", door: "L27-016/L27-017/L27-018/L27-019", lock: "MKDB-KA3", system: "AC" },
        { floor: "27/F", room: "ELECT ROOM (1)", door: "L27-032", lock: "MKDA-KA2", system: "EE" },
        { floor: "27/F", room: "ELECT ROOM (2)", door: "L27-037", lock: "MKDA-KA2", system: "EE" },
        { floor: "27/F", room: "LIFT MACHINE ROOM - LIFT NO. L-6 TO L-9", door: "L27-028/L27-029", lock: "MKDF-KA1", system: "LF" },
        { floor: "27/F", room: "WATER TANK & PUMP ROOM (1)", door: "L27-013/L27-015", lock: "MKDC-KA1", system: "WS" },
        { floor: "27/F", room: "WATER TANK & PUMP ROOM (2)", door: "L27-030/L27-031", lock: "MKDC-KA1", system: "WS" },
        { floor: "27/F", room: "AGSS Plant Room", door: "L27-045", lock: "MKDB-KA8", system: "MG" },
        { floor: "28/F (R/F)", room: "HEATING WATER & CHILLER WATER TANK RM.", door: "L28-005", lock: "MKDB-KD2", system: "AC" },
        { floor: "28/F (R/F)", room: "FS FOAM TANK RM. & Pump Room", door: "L28-006", lock: "MKDD-KD7", system: "FS" },
        { floor: "28/F (R/F)", room: "LIFT MACHINE ROOM - LIFT NO. L-2 TO L-5", door: "L28-008", lock: "MKDF-KA1", system: "LF" },
        { floor: "28/F (R/F)", room: "FOAM CONTROL VALVE CABINET", door: "AP6", lock: "MKDD-KA7", system: "FS" },
        { floor: "29/F", room: "LIFT MACHINE ROOM - LIFT NO. L-10 TO L-11", door: "L29-011/L29-014", lock: "MKDF-KA1", system: "LF" },
        { floor: "29/F", room: "BRI HEADEND EQUIPMENT ROOM", door: "L29-008", lock: "MKCC-KD3", system: "CB" }
  ];

  const TOTAL_ROOMS = 366;
  let jvRecords = JSON.parse(localStorage.getItem('jvRecords')) || [];
  let haRecords = JSON.parse(localStorage.getItem('haRecords')) || [];
  let recordCancelContext = null;
  let systemComparisonChart = null;

  function findRoom(floor, room) {
    return plantRoomData.find(r => r.floor === floor && r.room === room) || null;
  }

  // tabs
  document.querySelectorAll('.tab-button').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('.tab-button').forEach(b => b.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      btn.classList.add('active');
      document.getElementById(btn.dataset.tab).classList.add('active');
      if (btn.dataset.tab === 'tab-dashboard') {
        renderTrayCards();
        updateDashboard();
      } else if (btn.dataset.tab === 'tab-input') {
        renderRecords('jv-ha');
        renderRecords('ha-emsd');
      } else if (btn.dataset.tab === 'tab-Analytics') {
        updateAnalytics();
      }
    });
  });

  function initFloors() {
    const floors = [...new Set(plantRoomData.map(r => r.floor))].sort();
    const jf = document.getElementById('jvFloor');
    const hf = document.getElementById('haFloor');
    floors.forEach(f => {
      jf.innerHTML += `<option value="${f}">${f}</option>`;
      hf.innerHTML += `<option value="${f}">${f}</option>`;
    });
  }

  function updateJVRooms() {
    const floor = document.getElementById('jvFloor').value;
    const rooms = plantRoomData.filter(r => r.floor === floor);
    const select = document.getElementById('jvRoom');
    select.innerHTML = '<option value="">Select room</option>';
    rooms.forEach((r, i) => {
      select.innerHTML += `<option value="${i}|${floor}">${r.room}</option>`;
    });
    document.getElementById('jvDoor').value = '';
    document.getElementById('jvLock').value = '';
  }

  function updateJVRoomDetails() {
    const v = document.getElementById('jvRoom').value;
    if (!v) return;
    const [idx, floor] = v.split('|');
    const room = plantRoomData.filter(r => r.floor === floor)[+idx];
    document.getElementById('jvDoor').value = room.door || '';
    document.getElementById('jvLock').value = room.lock || '';
  }

  function updateHARooms() {
    const floor = document.getElementById('haFloor').value;
    const rooms = plantRoomData.filter(r => r.floor === floor);
    const select = document.getElementById('haRoom');
    select.innerHTML = '<option value="">Select room</option>';
    rooms.forEach((r, i) => {
      select.innerHTML += `<option value="${i}|${floor}">${r.room}</option>`;
    });
    document.getElementById('haDoor').value = '';
    document.getElementById('haLock').value = '';
  }

  function updateHARoomDetails() {
    const v = document.getElementById('haRoom').value;
    if (!v) return;
    const [idx, floor] = v.split('|');
    const room = plantRoomData.filter(r => r.floor === floor)[+idx];
    document.getElementById('haDoor').value = room.door || '';
    document.getElementById('haLock').value = room.lock || '';
  }

  function addRecord(type) {
    let floor, roomVal, lock, date, door, from, to, notes;
    if (type === 'jv-ha') {
      floor = document.getElementById('jvFloor').value.trim();
      roomVal = document.getElementById('jvRoom').value.trim();
      lock = document.getElementById('jvLock').value.trim();
      date = document.getElementById('jvDate').value;
      door = document.getElementById('jvDoor').value.trim();
      from = document.getElementById('jvFrom').value.trim();
      to = document.getElementById('jvTo').value.trim();
      notes = document.getElementById('jvNotes').value.trim();
    } else {
      floor = document.getElementById('haFloor').value.trim();
      roomVal = document.getElementById('haRoom').value.trim();
      lock = document.getElementById('haLock').value.trim();
      date = document.getElementById('haDate').value;
      door = document.getElementById('haDoor').value.trim();
      from = document.getElementById('haFrom').value.trim();
      to = document.getElementById('haTo').value.trim();
      notes = document.getElementById('haNotes').value.trim();
    }
    if (!floor || !roomVal || !lock || !date) {
      alert('Please fill in all required fields (*)');
      return;
    }

    // Check for duplicate plant room in the same handover type
    const targetRecords = type === 'jv-ha' ? jvRecords : haRecords;
    const idx = parseInt(roomVal.split('|')[0]);
    const roomData = plantRoomData.filter(r => r.floor === floor)[idx];

    const isDuplicate = targetRecords.some(rec => 
      rec.floor === floor && rec.room === roomData.room
    );

    if (isDuplicate) {
      alert(`This Plant Room (${floor} - ${roomData.room}) has already been handed over. Cannot add duplicate entries.`);
      return;
    }
    const rec = {
      id: Date.now(),
      floor,
      room: roomData.room,
      door,
      lock,
      date,
      from,
      to,
      notes,
      status: 'active'
    };
    if (type === 'jv-ha') {
      jvRecords.push(rec);
      localStorage.setItem('jvRecords', JSON.stringify(jvRecords));
      clearForm('jv');
      renderRecords('jv-ha');
    } else {
      haRecords.push(rec);
      localStorage.setItem('haRecords', JSON.stringify(haRecords));
      clearForm('ha');
      renderRecords('ha-emsd');
    }
    updateDashboard();
    renderTrayCards();
    showSuccess('Record saved');
  }

  function clearForm(prefix) {
    document.getElementById(prefix + 'Floor').value = '';
    document.getElementById(prefix + 'Room').innerHTML = '<option value="">Select floor first</option>';
    document.getElementById(prefix + 'Door').value = '';
    document.getElementById(prefix + 'Lock').value = '';
    document.getElementById(prefix + 'Date').value = '';
    document.getElementById(prefix + 'From').value = '';
    document.getElementById(prefix + 'To').value = '';
    document.getElementById(prefix + 'Notes').value = '';
  }

  function deleteRecord(type, id) {
    if (!confirm('Delete this record permanently?')) return;
    if (type === 'jv-ha') {
      jvRecords = jvRecords.filter(r => r.id !== id);
      localStorage.setItem('jvRecords', JSON.stringify(jvRecords));
      renderRecords('jv-ha');
    } else {
      haRecords = haRecords.filter(r => r.id !== id);
      localStorage.setItem('haRecords', JSON.stringify(haRecords));
      renderRecords('ha-emsd');
    }
    updateDashboard();
    renderTrayCards();
    showSuccess('Record deleted');
  }

  function showRecordCancelModal(type, id) {
    recordCancelContext = { type, id };
    document.getElementById('recordCancelModal').classList.add('show');
  }
  function closeRecordCancelModal() {
    document.getElementById('recordCancelModal').classList.remove('show');
    recordCancelContext = null;
  }
  function confirmRecordCancel() {
    if (!recordCancelContext) return;
    const { type, id } = recordCancelContext;
    if (type === 'jv-ha') {
      jvRecords = jvRecords.map(r => r.id === id ? { ...r, status: 'cancelled' } : r);
      localStorage.setItem('jvRecords', JSON.stringify(jvRecords));
      renderRecords('jv-ha');
    } else {
      haRecords = haRecords.map(r => r.id === id ? { ...r, status: 'cancelled' } : r);
      localStorage.setItem('haRecords', JSON.stringify(haRecords));
      renderRecords('ha-emsd');
    }
    updateDashboard();
    renderTrayCards();
    showSuccess('Record cancelled');
    closeRecordCancelModal();
  }
document.getElementById('recordCancelModal').addEventListener('click', e => {
    if (e.target.id === 'recordCancelModal') closeRecordCancelModal();
  });

  function renderRecords(type) {
    const listId = type === 'jv-ha' ? 'jvRecordList' : 'haRecordList';
    const target = document.getElementById(listId);
    const records = (type === 'jv-ha' ? jvRecords : haRecords).slice().reverse();
    if (!records.length) {
      target.innerHTML = '<div class="list-empty">No records yet</div>';
      return;
    }
    const tagClass = type === 'jv-ha' ? 'tag-jv' : 'tag-ha';
    const tagLabel = type === 'jv-ha' ? 'JV → HA' : 'HA → EMSD';
    target.innerHTML = records.map(r => {
      const cancelled = r.status === 'cancelled';
      return `
      <div class="item">
        <div>
          <div class="record-main">
            <span class="tag ${tagClass}">${tagLabel}</span>
            ${cancelled ? '<span class="tag tag-cancelled">CANCELLED</span>' : ''}
            ${r.room} (${r.floor})
          </div>
          <div class="record-meta">
            Door: ${r.door || '–'} · Key: ${r.lock || '–'} · Date: ${new Date(r.date).toLocaleDateString('en-GB')}<br>
            ${r.from ? 'From: ' + r.from + ' · ' : ''}${r.to ? 'To: ' + r.to : ''}
            ${r.notes ? '<br>Remark: ' + r.notes : ''}
          </div>
        </div>
        <div class="btn-row" style="flex-direction:column;align-items:flex-end;">
          <button class="btn btn-cancel btn-sm" onclick="showRecordCancelModal('${type}', ${r.id})">Cancel</button>
          <button class="btn btn-danger btn-sm" onclick="deleteRecord('${type}', ${r.id})">Delete</button>
        </div>
      </div>`;
    }).join('');
  }

  function exportCSV(type) {
    const records = type === 'jv-ha' ? jvRecords : haRecords;
    const headers = ['Status','Floor','Room Name','Door Number','Key Code','Handover Date','Handed By','Received By','Remarks'];
    let csv = headers.join(',') + '\n';
    records.forEach(r => {
      csv += [
        r.status || 'active',
        r.floor,
        r.room,
        r.door,
        r.lock,
        r.date,
        r.from,
        r.to,
        r.notes
      ].map(x => `"${(x || '').replace(/"/g,'""')}"`).join(',') + '\n';
    });
    const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = type === 'jv-ha' ? 'JV-HA-records.csv' : 'HA-EMSD-records.csv';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  }

  function showSuccess(msg) {
    const el = document.getElementById('successMessage');
    el.textContent = msg;
    el.classList.add('show');
    setTimeout(() => el.classList.remove('show'), 2200);
  }

  function updateDashboard() {
    const jvActive = jvRecords.filter(r => r.status !== 'cancelled').length;
    const haActive = haRecords.filter(r => r.status !== 'cancelled').length;
    document.getElementById('dashJVCount').textContent = jvActive;
    document.getElementById('dashHACount').textContent = haActive;
    const jvPct = Math.round((jvActive / TOTAL_ROOMS) * 100) || 0;
    const haPct = Math.round((haActive / TOTAL_ROOMS) * 100) || 0;
    document.getElementById('jvProgressText').textContent = `${jvActive} / ${TOTAL_ROOMS} (${jvPct}%)`;
    document.getElementById('haProgressText').textContent = `${haActive} / ${TOTAL_ROOMS} (${haPct}%)`;
    document.getElementById('jvProgressBar').style.width = (jvActive / TOTAL_ROOMS * 100) + '%';
    document.getElementById('haProgressBar').style.width = (haActive / TOTAL_ROOMS * 100) + '%';
  }

  function renderTrayCards() {
    const totalBy = {};
    plantRoomData.forEach(r => {
      const sys = (r.system || 'N/A').trim();
      totalBy[sys] = (totalBy[sys] || 0) + 1;
    });
    const jvBy = {};
    jvRecords.filter(r => r.status !== 'cancelled').forEach(r => {
      const pr = findRoom(r.floor, r.room);
      const sys = pr ? (pr.system || 'N/A').trim() : 'N/A';
      jvBy[sys] = (jvBy[sys] || 0) + 1;
    });
    const haBy = {};
    haRecords.filter(r => r.status !== 'cancelled').forEach(r => {
      const pr = findRoom(r.floor, r.room);
      const sys = pr ? (pr.system || 'N/A').trim() : 'N/A';
      haBy[sys] = (haBy[sys] || 0) + 1;
    });
    const systems = Object.keys(totalBy).sort();
    const el = document.getElementById('trayGrid');
    el.innerHTML = systems.map(sys => {
      const total = totalBy[sys];
      const jv = jvBy[sys] || 0;
      const ha = haBy[sys] || 0;
      const pending = Math.max(total - ha, 0);
      const jvP = total ? Math.round(jv / total * 100) : 0;
      const haP = total ? Math.round(ha / total * 100) : 0;
      return `
      <div class="tray-card" onclick="filterByTray('${sys}')">
        <div class="tray-code">${sys}</div>
        <div class="tray-main">${total} rooms</div>
        <div class="tray-line">JV→HA: <strong>${jv}</strong> (${jvP}%)</div>
        <div class="tray-line">HA→EMSD: <strong>${ha}</strong> (${haP}%)</div>
        <div class="tray-line">Pending: <strong>${pending}</strong></div>
        <div class="tray-pill">View rooms</div>
      </div>`;
    }).join('');
  }

  function filterByTray(sys) {
    const list = plantRoomData.filter(r => (r.system || '').trim() === sys);
    const panel = document.getElementById('trayRoomPanel');
    const title = document.getElementById('trayRoomTitle');
    const body = document.getElementById('trayRoomBody');
    title.textContent = `Tray ${sys} – ${list.length} rooms`;
    if (!list.length) {
      body.innerHTML = '<div class="list-empty">No rooms for this tray</div>';
    } else {
      body.innerHTML = list.map(r => {
        // Check handover status
        const jvHandedOver = jvRecords.some(rec => rec.floor === r.floor && rec.room === r.room && rec.status !== 'cancelled');
        const haHandedOver = haRecords.some(rec => rec.floor === r.floor && rec.room === r.room && rec.status !== 'cancelled');

        let statusIndicator = '';
        if (jvHandedOver && haHandedOver) {
          statusIndicator = '<span style="color: #28a745; font-weight: bold;">✓ Both Handed Over</span>';
        } else if (jvHandedOver) {
          statusIndicator = '<span style="color: #ffc107; font-weight: bold;">⊙ JV→HA Completed</span>';
        } else if (haHandedOver) {
          statusIndicator = '<span style="color: #17a2b8; font-weight: bold;">⊙ HA→EMSD Completed</span>';
        } else {
          statusIndicator = '<span style="color: #6c757d;">○ Not Handed Over</span>';
        }

        return `
        <div class="room-list-item">
          <div>
            <div>${r.room} (${r.floor})</div>
            <div class="room-list-meta">Door: ${r.door || '–'} · Key: ${r.lock || '–'}</div>
            <div class="room-list-meta" style="margin-top: 4px;">${statusIndicator}</div>
          </div>
        </div>`;
      }).join('');
    }
    panel.style.display = 'block';
  }

  function updateAnalytics() {
    const totalBy = {};
    plantRoomData.forEach(r => {
      const sys = (r.system || 'N/A').trim();
      totalBy[sys] = (totalBy[sys] || 0) + 1;
    });
    function sysOf(rec) {
      const pr = findRoom(rec.floor, rec.room);
      return pr ? (pr.system || 'N/A').trim() : 'N/A';
    }
    const jvBy = {};
    jvRecords.filter(r => r.status !== 'cancelled').forEach(r => {
      const s = sysOf(r);
      jvBy[s] = (jvBy[s] || 0) + 1;
    });
    const haBy = {};
    haRecords.filter(r => r.status !== 'cancelled').forEach(r => {
      const s = sysOf(r);
      haBy[s] = (haBy[s] || 0) + 1;
    });

    const systems = Object.keys(totalBy).sort();
    const jvData = systems.map(s => jvBy[s] || 0);
    const haData = systems.map(s => haBy[s] || 0);

    const ctx = document.getElementById('systemComparisonChart');
    if (ctx) {
      if (systemComparisonChart) systemComparisonChart.destroy();
      systemComparisonChart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: systems,
          datasets: [
            { label: 'JV → HA', data: jvData, backgroundColor: '#6366f1' },
            { label: 'HA → EMSD', data: haData, backgroundColor: '#4b5563' },
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: { y: { beginAtZero: true, ticks: { stepSize: 1 } } },
          plugins: {
            legend: { position: 'top', labels: { boxWidth: 10, font: { size: 11 } } }
          }
        }
      });
    }

    let html = '<table style="width:100%;border-collapse:collapse;font-size:12px;">';
    html += '<thead><tr style="background:#f3f4f6;">' +
      '<th style="padding:6px;border:1px solid #e5e7eb;text-align:left;">Tray</th>' +
      '<th style="padding:6px;border:1px solid #e5e7eb;">Total</th>' +
      '<th style="padding:6px;border:1px solid #e5e7eb;">JV→HA</th>' +
      '<th style="padding:6px;border:1px solid #e5e7eb;">HA→EMSD</th>' +
      '<th style="padding:6px;border:1px solid #e5e7eb;">JV→HA %</th>' +
      '<th style="padding:6px;border:1px solid #e5e7eb;">HA→EMSD %</th>' +
      '</tr></thead><tbody>';
    systems.forEach(sys => {
      const total = totalBy[sys];
      const jv = jvBy[sys] || 0;
      const ha = haBy[sys] || 0;
      const jp = total ? Math.round(jv/total*100) : 0;
      const hp = total ? Math.round(ha/total*100) : 0;
      html += `<tr>
        <td style="padding:6px;border:1px solid #e5e7eb;">${sys}</td>
        <td style="padding:6px;border:1px solid #e5e7eb;text-align:center;">${total}</td>
        <td style="padding:6px;border:1px solid #e5e7eb;text-align:center;">${jv}</td>
        <td style="padding:6px;border:1px solid #e5e7eb;text-align:center;">${ha}</td>
        <td style="padding:6px;border:1px solid #e5e7eb;text-align:center;">${jp}%</td>
        <td style="padding:6px;border:1px solid #e5e7eb;text-align:center;">${hp}%</td>
      </tr>`;
    });
    html += '</tbody></table>';
    document.getElementById('systemStats').innerHTML = html;
  }

  (function init() {
    const today = new Date().toISOString().slice(0,10);
    document.getElementById('jvDate').value = today;
    document.getElementById('haDate').value = today;
    initFloors();
    updateDashboard();
    renderTrayCards();
    renderRecords('jv-ha');
    renderRecords('ha-emsd');
  })();
</script>
</body>
</html>