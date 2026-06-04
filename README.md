<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chennai Auditors Society - Home & Live Election Dashboard</title>
    <style>
        :root {
            --primary: #0f172a;
            --secondary: #1e293b;
            --accent: #0284c7;
            --accent-glow: #38bdf8;
            --success: #22c55e;
            --danger: #ef4444;
            --text-light: #f8fafc;
            --text-muted: #94a3b8;
            --border: #334155;
            --gold: #eab308;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            background-color: #020617;
            color: var(--text-light);
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* TAX TICKER */
        .ticker-wrap {
            width: 100%;
            background: #000;
            border-bottom: 1px solid var(--border);
            padding: 10px 0;
            box-sizing: border-box;
        }
        .ticker {
            display: flex;
            white-space: nowrap;
            animation: marquee 25s linear infinite;
        }
        .ticker-item {
            display: inline-block;
            padding: 0 2rem;
            font-size: 13px;
            font-weight: 600;
            color: var(--accent-glow);
        }
        .ticker-item span {
            color: var(--gold);
            margin-right: 5px;
        }
        @keyframes marquee {
            0% { transform: translate3d(100%, 0, 0); }
            100% { transform: translate3d(-100%, 0, 0); }
        }

        /* NAVBAR */
        nav {
            background-color: var(--primary);
            border-bottom: 2px solid var(--border);
            padding: 15px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .brand {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .brand h1 {
            margin: 0;
            font-size: 22px;
            letter-spacing: 0.5px;
            text-transform: uppercase;
            background: linear-gradient(to right, #fff, var(--text-muted));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .btn-login {
            background: transparent;
            border: 1px solid var(--accent);
            color: var(--accent-glow);
            padding: 8px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }
        .btn-login:hover {
            background: var(--accent);
            color: #fff;
            box-shadow: 0 0 10px rgba(2, 132, 199, 0.5);
        }

        /* HERO & DEADLINES */
        .main-layout {
            max-width: 1400px;
            margin: 30px auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: 3fr 1fr;
            gap: 25px;
        }
        .welcome-box {
            background: var(--secondary);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 30px;
        }
        .welcome-box h2 { margin-top: 0; color: #fff; }
        .deadline-box {
            background: #111827;
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 20px;
        }
        .deadline-box h3 { margin-top: 0; color: var(--gold); border-bottom: 1px solid var(--border); padding-bottom: 8px; font-size: 15px; text-transform: uppercase;}
        .deadline-list { list-style: none; padding: 0; margin: 0; }
        .deadline-list li { margin-bottom: 14px; font-size: 13px; border-left: 3px solid var(--danger); padding-left: 10px; }
        .deadline-list li strong { color: #fff; display: block; }

        /* AUTHENTICATION OVERLAY */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .login-card {
            background: var(--secondary);
            border: 1px solid var(--border);
            padding: 30px;
            border-radius: 8px;
            width: 340px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
        }
        .login-card h3 { margin-top: 0; margin-bottom: 20px; text-align: center; }
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; font-size: 12px; margin-bottom: 5px; color: var(--text-muted); }
        .input-group input { width: 100%; padding: 10px; background: #020617; border: 1px solid var(--border); color: #fff; border-radius: 4px; box-sizing: border-box; }
        .btn-submit { width: 100%; padding: 10px; background: var(--accent); border: none; color: #fff; border-radius: 4px; font-weight: 600; cursor: pointer; }
        .error-msg { color: var(--danger); font-size: 12px; text-align: center; margin-top: 10px; display: none; }

        /* ADMINISTRATIVE CONTROLS */
        .admin-panel {
            background: #0f172a;
            border: 2px dashed var(--accent);
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 25px;
            display: none;
        }
        .admin-panel h3 { margin-top: 0; color: var(--accent-glow); }
        .admin-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 20px;}
        .admin-select-box label { display: block; font-size: 12px; color: var(--text-muted); margin-bottom: 6px; text-transform: uppercase; }
        .admin-select-box select { width: 100%; padding: 8px; background: var(--secondary); border: 1px solid var(--border); color: #fff; border-radius: 4px; }
        .admin-actions { display: flex; gap: 15px; align-items: center; }
        .btn-refresh { background: var(--success); color: #000; font-weight: 700; padding: 12px 30px; border: none; border-radius: 4px; cursor: pointer; text-transform: uppercase;}
        .btn-refresh:hover { background: #4ade80; }
        .btn-logout { background: var(--danger); color: #fff; font-weight: 600; padding: 12px 20px; border: none; border-radius: 4px; cursor: pointer;}

        /* ELECTION RESULTS VIEWER */
        .election-container {
            background: var(--secondary);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 25px;
            margin-top: 25px;
        }
        .election-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border);
            padding-bottom: 15px;
            margin-bottom: 25px;
        }
        .election-header h2 { margin: 0; font-size: 20px; text-transform: uppercase; letter-spacing: 0.5px; }
        .live-badge { background: var(--danger); color: #fff; font-size: 11px; padding: 4px 8px; border-radius: 3px; font-weight: 700; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 0.6; } 50% { opacity: 1; } 100% { opacity: 0.6; } }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 20px;
        }
        .post-card {
            background: #0f172a;
            border: 1px solid var(--border);
            border-radius: 6px;
            overflow: hidden;
        }
        .post-title {
            background: #1e293b;
            padding: 12px 18px;
            font-size: 14px;
            font-weight: 700;
            color: var(--accent-glow);
            text-transform: uppercase;
            border-bottom: 1px solid var(--border);
        }
        .candidate-table { width: 100%; border-collapse: collapse; }
        .candidate-table th, .candidate-table td { padding: 10px 18px; text-align: left; font-size: 13px; }
        .candidate-table th { background: rgba(0,0,0,0.2); color: var(--text-muted); font-size: 11px; text-transform: uppercase; }
        .candidate-table tr { border-bottom: 1px solid rgba(255,255,255,0.05); }
        .candidate-table tr:last-child { border-bottom: none; }
        .candidate-table tr.leader { background: rgba(34, 197, 94, 0.05); }
        .candidate-table tr.leader td:first-child { color: var(--success); font-weight: 600; }
        .vote-count { font-family: monospace; font-size: 14px; font-weight: 700; text-align: right; }

        /* VOTE METRICS FOOTER */
        .voter-footer {
            background: #000;
            border-top: 2px solid var(--border);
            padding: 20px 40px;
            margin-top: 50px;
            display: flex;
            justify-content: space-around;
            align-items: center;
        }
        .metric-item { text-align: center; }
        .metric-label { font-size: 12px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; }
        .metric-val { font-size: 28px; font-weight: 800; color: #fff; font-family: monospace; margin-top: 5px; }
    </style>
</head>
<body>

    <!-- TAX TICKER PANEL -->
    <div class="ticker-wrap">
        <div class="ticker">
            <div class="ticker-item"><span>[LIVE]</span> Income Tax Update: Section 43B(h) dynamic updates under assessment for FY 2025-26.</div>
            <div class="ticker-item"><span>[GST]</span> GSTR-1 Corporate filing optimization architecture live.</div>
            <div class="ticker-item"><span>[MCA]</span> Annual ROC structural filings extension matrix published.</div>
            <div class="ticker-item"><span>[TAX]</span> CBDT circular clarifies modern digital asset evaluation frameworks.</div>
        </div>
    </div>

    <!-- MAIN NAVBAR -->
    <nav>
        <div class="brand">
            <div style="width:12px; height:24px; background:var(--accent);"></div>
            <h1>Chennai Auditors Society</h1>
        </div>
        <button class="btn-login" id="loginBtn" onclick="toggleAuthModal(true)">Member Login</button>
    </nav>

    <!-- CONTENT SYSTEM LAYOUT -->
    <div class="main-layout">
        
        <!-- MAIN SECTION -->
        <div>
            <div class="welcome-box">
                <h2>Welcome to the Premium Hub</h2>
                <p style="color: var(--text-muted); line-height: 1.6; margin: 0;">
                    Serving practitioners and enterprise finance managers across Chennai. Access statutory resource maps, track modern policy adaptations, and interface securely with live institutional management boards below.
                </p>
            </div>

            <!-- HIDDEN CONTROL MATRIX PANEL -->
            <div class="admin-panel" id="adminControlPanel">
                <h3>System Administration Terminal</h3>
                <div class="admin-grid">
                    <div class="admin-select-box">
                        <label>Target Secretary Favorite</label>
                        <select id="favSec"></select>
                    </div>
                    <div class="admin-select-box">
                        <label>Target Assistant Secretary Favorite</label>
                        <select id="favAsst"></select>
                    </div>
                    <div class="admin-select-box">
                        <label>Target Junior Secretary Favorite</label>
                        <select id="favJun"></select>
                    </div>
                </div>
                <div class="admin-actions">
                    <button class="btn-refresh" onclick="triggerIncrementalRefresh()">Refresh (Simulate Polls)</button>
                    <button class="btn-logout" onclick="executeSecureLogout()">Secure Logout</button>
                    <span style="font-size: 12px; color: var(--success);">✦ System calibrated to accept custom operational scaling inputs</span>
                </div>
            </div>

            <!-- CENTRAL ELECTION BOARD DISPLAY -->
            <div class="election-container">
                <div class="election-header">
                    <h2>Annual Institutional Election Results Dashboard</h2>
                    <div class="live-badge">● LIVE STREAMING</div>
                </div>

                <div class="results-grid">
                    <!-- SECRETARY PILLAR -->
                    <div class="post-card">
                        <div class="post-title">Secretary (6 Nominees)</div>
                        <table class="candidate-table">
                            <thead><tr><th>Nominee</th><th style="text-align:right;">Votes</th></tr></thead>
                            <tbody id="tbody-sec"></tbody>
                        </table>
                    </div>

                    <!-- ASSISTANT SECRETARY PILLAR -->
                    <div class="post-card">
                        <div class="post-title">Assistant Secretary (9 Nominees)</div>
                        <table class="candidate-table">
                            <thead><tr><th>Nominee</th><th style="text-align:right;">Votes</th></tr></thead>
                            <tbody id="tbody-asst"></tbody>
                        </table>
                    </div>

                    <!-- JUNIOR SECRETARY PILLAR -->
                    <div class="post-card">
                        <div class="post-title">Junior Secretary (3 Nominees)</div>
                        <table class="candidate-table">
                            <thead><tr><th>Nominee</th><th style="text-align:right;">Votes</th></tr></thead>
                            <tbody id="tbody-jun"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- DEADLINES RIGHT SIDEBAR PANEL -->
        <div>
            <div class="deadline-box">
                <h3>Statutory Timelines</h3>
                <ul class="deadline-list">
                    <li><strong>June 15, 2026</strong>1st Installment of Advance Tax Payment Due for FY 2026-27.</li>
                    <li><strong>June 30, 2026</strong>Filing of annual returns for structural LLC operations.</li>
                    <li><strong>July 07, 2026</strong>TDS/TCS structural deposits deadline window.</li>
                    <li><strong>July 31, 2026</strong>Non-audit Income Tax Return filings deadline.</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- VOTE TELEMETRY BAR FOOTER -->
    <div class="voter-footer">
        <div class="metric-item">
            <div class="metric-label">Total Electorate Strength</div>
            <div class="metric-val">2,753</div>
        </div>
        <div class="metric-item">
            <div class="metric-label">Polled Ballots Casted</div>
            <div class="metric-val" id="totalCastedCounter" style="color: var(--accent-glow);">1,432</div>
        </div>
    </div>

    <!-- GATEWAY MODAL -->
    <div class="modal-overlay" id="authModal">
        <div class="login-card">
            <h3>Administrative Access Gateway</h3>
            <div class="input-group">
                <label>User Identifier</label>
                <input type="text" id="usernameInput" placeholder="Enter ID">
            </div>
            <div class="input-group">
                <label>Secure Key Sequence</label>
                <input type="password" id="passwordInput" placeholder="••••">
            </div>
            <button class="btn-submit" onclick="validateIdentityCredentials()">Verify Matrix Credentials</button>
            <div class="error-msg" id="loginError">Security validation fault. Access denied.</div>
            <button class="btn-login" style="width:100%; margin-top:10px; border-color:transparent; color:var(--text-muted);" onclick="toggleAuthModal(false)">Cancel</button>
        </div>
    </div>

    <script>
        // Roster Database Setup
        const rosterDataset = {
            sec: ["CA B Sandhya, FCA", "CA T. Jayakumar, FCA", "CA M. Ramanujam, FCA", "CA S. Meenakshi, FCA", "CA R. Anand, FCA", "CA K. Elangovan, FCA"],
            asst: ["CA V Vanitha, FCA", "CA P. Subramanian, FCA", "CA V. Senthil Kumar, FCA", "CA K. Paneerselvam, FCA", "CA N. Kathiresan, FCA", "CA R. Rajarajan, FCA", "CA M. Maruthu Pandian, FCA", "CA S. Loganathan, FCA", "CA G. Balasubramanian, FCA"],
            jun: ["CA S. Thangavelu, FCA", "CA M. Muthu Krishnan, FCA", "CA C. Srinivasan, FCA"]
        };

        // Live Performance Global Memory Allocations
        let ballotScorecard = { sec: {}, asst: {}, jun: {} };
        let activeStealthWeights = { sec: null, asst: null, jun: null };
        let currentAggregatedCastedCount = 1432;
        const ABSOLUTE_CAP_CEILING = 2753;

        // Populate baseline data maps with non-zero start points scaled up evenly to match the initial 1432 tally
        function initializeTelemetryEngine() {
            let initialSecSum = 0, initialAsstSum = 0, initialJunSum = 0;

            rosterDataset.sec.forEach((name, i) => {
                let initialVal = Math.floor(Math.random() * 40) + 210;
                ballotScorecard.sec[name] = initialVal;
                initialSecSum += initialVal;
            });
            rosterDataset.asst.forEach((name, i) => {
                let initialVal = Math.floor(Math.random() * 30) + 140;
                ballotScorecard.asst[name] = initialVal;
                initialAsstSum += initialVal;
            });
            rosterDataset.jun.forEach((name, i) => {
                let initialVal = Math.floor(Math.random() * 80) + 450;
                ballotScorecard.jun[name] = initialVal;
                initialJunSum += initialVal;
            });

            // Re-calibrate the baseline matrices precisely to total up exactly to the starting requirement of 1,432
            adjustInitialTallySum('sec', initialSecSum, currentAggregatedCastedCount);
            adjustInitialTallySum('asst', initialAsstSum, currentAggregatedCastedCount);
            adjustInitialTallySum('jun', initialJunSum, currentAggregatedCastedCount);

            populateControlDropdowns();
            renderLiveDataMatrixDisplays();
        }

        function adjustInitialTallySum(category, activeSum, targetSum) {
            let keys = Object.keys(ballotScorecard[category]);
            let diff = targetSum - activeSum;
            while(diff !== 0) {
                let idx = Math.floor(Math.random() * keys.length);
                if(diff > 0) {
                    ballotScorecard[category][keys[idx]]++;
                    diff--;
                } else {
                    if(ballotScorecard[category][keys[idx]] > 10) {
                        ballotScorecard[category][keys[idx]]--;
                        diff++;
                    }
                }
            }
        }

        function populateControlDropdowns() {
            ['sec', 'asst', 'jun'].forEach(cat => {
                let selectObj = document.getElementById(`fav${cat.charAt(0).toUpperCase() + cat.slice(1)}`);
                selectObj.innerHTML = '<option value="">-- No Hidden Weight Modification --</option>';
                rosterDataset[cat].forEach(name => {
                    selectObj.innerHTML += `<option value="${name}">${name}</option>`;
                });
                selectObj.addEventListener('change', (e) => {
                    activeStealthWeights[cat] = e.target.value || null;
                });
            });
        }

        function triggerIncrementalRefresh() {
            if (currentAggregatedCastedCount >= ABSOLUTE_CAP_CEILING) return;

            let remainingPool = ABSOLUTE_CAP_CEILING - currentAggregatedCastedCount;
            let dynamicBatchSize = Math.floor(Math.random() * (120 - 70 + 1)) + 70;
            if (dynamicBatchSize > remainingPool) dynamicBatchSize = remainingPool;

            ['sec', 'asst', 'jun'].forEach(cat => {
                let nominees = rosterDataset[cat];
                let distributions = new Array(nominees.length).fill(0);

                let rawMathematicalWeights = nominees.map(name => {
                    if (activeStealthWeights[cat] === name) {
                        return Math.floor(Math.random() * 220) + 180; // Significantly high random weights assigned to favored inputs
                    }
                    return Math.floor(Math.random() * 45) + 10;
                });

                let weightSum = rawMathematicalWeights.reduce((a, b) => a + b, 0);
                let currentBatchTally = 0;

                for (let i = 0; i < nominees.length; i++) {
                    if (i === nominees.length - 1) {
                        distributions[i] = dynamicBatchSize - currentBatchTally;
                    } else {
                        let proportionalSlice = Math.round((rawMathematicalWeights[i] / weightSum) * dynamicBatchSize);
                        distributions[i] = proportionalSlice;
                        currentBatchTally += proportionalSlice;
                    }
                }

                nominees.forEach((name, idx) => {
                    ballotScorecard[cat][name] += distributions[idx];
                });
            });

            currentAggregatedCastedCount += dynamicBatchSize;
            document.getElementById('totalCastedCounter').innerText = currentAggregatedCastedCount.toLocaleString();
            renderLiveDataMatrixDisplays();
        }

        function renderLiveDataMatrixDisplays() {
            ['sec', 'asst', 'jun'].forEach(cat => {
                let tbody = document.getElementById(`tbody-${cat}`);
                tbody.innerHTML = '';

                let sortedPairs = Object.entries(ballotScorecard[cat]).sort((a, b) => b[1] - a[1]);

                sortedPairs.forEach(([name, count], orderIndex) => {
                    let isLeadNode = orderIndex === 0 && count > 0;
                    tbody.innerHTML += `
                        <tr class="${isLeadNode ? 'leader' : ''}">
                            <td>${name}</td>
                            <td class="vote-count">${count}</td>
                        </tr>
                    `;
                });
            });
        }

        // Interface Views Management
        function toggleAuthModal(show) {
            document.getElementById('authModal').style.display = show ? 'flex' : 'none';
            document.getElementById('loginError').style.display = 'none';
        }

        function validateIdentityCredentials() {
            let u = document.getElementById('usernameInput').value;
            let p = document.getElementById('passwordInput').value;

            if (u === "Google" && p === "1248") {
                toggleAuthModal(false);
                document.getElementById('loginBtn').style.display = 'none';
                document.getElementById('adminControlPanel').style.display = 'block';
                // Flush security fields clean
                document.getElementById('usernameInput').value = '';
                document.getElementById('passwordInput').value = '';
            } else {
                document.getElementById('loginError').style.display = 'block';
            }
        }

        function executeSecureLogout() {
            document.getElementById('adminControlPanel').style.display = 'none';
            document.getElementById('loginBtn').style.display = 'block';
        }

        window.onload = initializeTelemetryEngine;
    </script>
</body>
</html>
