<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chennai Auditors Society - Home & Premium Election Live</title>
    <style>
        :root {
            --bg-deep: #090d16;
            --bg-surface: #111726;
            --bg-card: #1b2336;
            --border-glow: #24324f;
            --accent-cyan: #06b6d4;
            --accent-neon: #00f5d4;
            --success-green: #10b981;
            --alert-red: #f43f5e;
            --text-main: #f1f5f9;
            --text-muted: #64748b;
            --gold-premium: #f59e0b;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-deep);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* PREMIUM DYNAMIC TICKER */
        .ticker-wrap {
            width: 100%;
            background: #030712;
            border-bottom: 1px solid var(--border-glow);
            padding: 12px 0;
            box-sizing: border-box;
        }
        .ticker {
            display: flex;
            white-space: nowrap;
            animation: marquee-scroll 30s linear infinite;
        }
        .ticker-item {
            display: inline-block;
            padding: 0 3rem;
            font-size: 13px;
            font-weight: 500;
            color: var(--text-main);
            letter-spacing: 0.5px;
        }
        .ticker-item span {
            color: var(--accent-cyan);
            font-weight: 700;
            margin-right: 8px;
        }
        @keyframes marquee-scroll {
            0% { transform: translate3d(100%, 0, 0); }
            100% { transform: translate3d(-100%, 0, 0); }
        }

        /* CLEAN TOP NAVBAR */
        nav {
            background-color: var(--bg-surface);
            border-bottom: 1px solid var(--border-glow);
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .brand {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .brand-logo {
            width: 4px;
            height: 28px;
            background: linear-gradient(to bottom, var(--accent-cyan), var(--accent-neon));
            border-radius: 2px;
        }
        .brand h1 {
            margin: 0;
            font-size: 24px;
            font-weight: 800;
            letter-spacing: 0.5px;
            text-transform: uppercase;
            color: #ffffff;
        }
        .btn-login {
            background: transparent;
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 10px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 13px;
            letter-spacing: 0.5px;
            text-transform: uppercase;
            transition: all 0.25s ease-in-out;
        }
        .btn-login:hover {
            background: rgba(6, 182, 212, 0.1);
            color: #ffffff;
            border-color: #ffffff;
            box-shadow: 0 0 15px rgba(6, 182, 212, 0.3);
        }

        /* CORE GRID LAYOUT */
        .main-layout {
            max-width: 1440px;
            margin: 40px auto;
            padding: 0 30px;
            display: grid;
            grid-template-columns: 3fr 1fr;
            gap: 30px;
        }
        .welcome-box {
            background: linear-gradient(135deg, var(--bg-surface) 0%, var(--bg-card) 100%);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 35px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .welcome-box h2 { margin-top: 0; color: #fff; font-size: 26px; font-weight: 700; }
        .welcome-box p { color: #94a3b8; line-height: 1.7; margin: 0; font-size: 15px; }
        
        .deadline-box {
            background: var(--bg-surface);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .deadline-box h3 { margin-top: 0; color: var(--gold-premium); border-bottom: 1px solid var(--border-glow); padding-bottom: 12px; font-size: 14px; text-transform: uppercase; letter-spacing: 1px;}
        .deadline-list { list-style: none; padding: 0; margin: 0; }
        .deadline-list li { margin-bottom: 20px; font-size: 13px; border-left: 2px solid var(--alert-red); padding-left: 14px; }
        .deadline-list li strong { color: #fff; display: block; font-size: 14px; margin-bottom: 4px; }

        /* ADMINISTRATIVE MANAGEMENT SUITE */
        .admin-panel {
            background: #0d1527;
            border: 1px solid var(--accent-cyan);
            border-radius: 12px;
            padding: 30px;
            margin-bottom: 30px;
            display: none;
            box-shadow: 0 0 25px rgba(6, 182, 212, 0.15);
        }
        .admin-panel h3 { margin-top: 0; color: var(--accent-cyan); font-size: 18px; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 20px; }
        .admin-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; margin-bottom: 25px;}
        .admin-select-box label { display: block; font-size: 11px; color: #94a3b8; margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.5px; }
        .admin-select-box select { width: 100%; padding: 12px; background: var(--bg-surface); border: 1px solid var(--border-glow); color: #fff; border-radius: 6px; outline: none; }
        .admin-actions { display: flex; gap: 20px; align-items: center; flex-wrap: wrap; }
        .btn-refresh { background: linear-gradient(90deg, var(--success-green), #059669); color: #fff; font-weight: 700; padding: 14px 35px; border: none; border-radius: 6px; cursor: pointer; text-transform: uppercase; letter-spacing: 0.5px; box-shadow: 0 4px 15px rgba(16, 185, 129, 0.2); }
        .btn-refresh:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(16, 185, 129, 0.4); }
        .btn-logout { background: var(--alert-red); color: #fff; font-weight: 600; padding: 14px 25px; border: none; border-radius: 6px; cursor: pointer; text-transform: uppercase; letter-spacing: 0.5px; }

        /* MODERN ELECTION CARDS & STYLISH TABLES */
        .election-container {
            background: var(--bg-surface);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .election-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-glow);
            padding-bottom: 20px;
            margin-bottom: 30px;
        }
        .election-header h2 { margin: 0; font-size: 22px; text-transform: uppercase; letter-spacing: 0.5px; font-weight: 800; }
        .live-badge { background: rgba(244, 63, 94, 0.1); border: 1px solid var(--alert-red); color: var(--alert-red); font-size: 11px; padding: 6px 14px; border-radius: 20px; font-weight: 700; letter-spacing: 1px; animation: glow-pulse 2s infinite; }
        @keyframes glow-pulse { 0% { opacity: 0.7; } 50% { opacity: 1; } 100% { opacity: 0.7; } }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 25px;
        }
        .post-card {
            background: var(--bg-card);
            border: 1px solid var(--border-glow);
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15);
        }
        .post-title {
            background: #222d44;
            padding: 16px 20px;
            font-size: 14px;
            font-weight: 700;
            color: var(--accent-neon);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            border-bottom: 1px solid var(--border-glow);
        }
        
        /* Table Styles Fix: Clean Dark contrast design making ALL names visible perfectly */
        .candidate-table { width: 100%; border-collapse: collapse; }
        .candidate-table th { background: rgba(3, 7, 12, 0.4); color: var(--text-muted); font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; }
        .candidate-table th, .candidate-table td { padding: 14px 20px; text-align: left; font-size: 14px; }
        
        /* Dark surface baseline rows: clear crisp contrast for all names */
        .candidate-table tr { border-bottom: 1px solid var(--border-glow); color: #cbd5e1; }
        .candidate-table tr:last-child { border-bottom: none; }
        .candidate-table tr:hover { background: rgba(255,255,255,0.02); }
        
        /* Premium leadership state row modification */
        .candidate-table tr.leader { background: rgba(6, 182, 212, 0.08); color: #ffffff; }
        .candidate-table tr.leader td:first-child { color: var(--accent-neon); font-weight: 700; }
        .candidate-table tr.leader .vote-count { color: #ffffff; font-weight: 800; }
        
        .vote-count { font-family: monospace; font-size: 16px; font-weight: 600; text-align: right; color: var(--accent-cyan); }

        /* METRICS CONTROLS FOOTER PANEL */
        .voter-footer {
            background: #030712;
            border-top: 1px solid var(--border-glow);
            padding: 30px 50px;
            margin-top: 60px;
            display: flex;
            justify-content: space-around;
            align-items: center;
        }
        .metric-item { text-align: center; }
        .metric-label { font-size: 11px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; }
        .metric-val { font-size: 32px; font-weight: 800; color: #ffffff; font-family: monospace; margin-top: 8px; }

        /* AUTH SEPARATION DIALOG MATRIX OVERLAY */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(3, 7, 12, 0.85);
            backdrop-filter: blur(5px);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .login-card {
            background: var(--bg-surface);
            border: 1px solid var(--border-glow);
            padding: 40px;
            border-radius: 12px;
            width: 360px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }
        .login-card h3 { margin-top: 0; margin-bottom: 25px; text-align: center; font-size: 20px; font-weight: 700; }
        .input-group { margin-bottom: 20px; }
        .input-group label { display: block; font-size: 11px; margin-bottom: 8px; color: var(--text-muted); text-transform: uppercase; }
        .input-group input { width: 100%; padding: 12px; background: var(--bg-deep); border: 1px solid var(--border-glow); color: #fff; border-radius: 6px; box-sizing: border-box; outline: none; }
        .input-group input:focus { border-color: var(--accent-cyan); }
        .btn-submit { width: 100%; padding: 12px; background: var(--accent-cyan); border: none; color: #fff; border-radius: 6px; font-weight: 700; cursor: pointer; text-transform: uppercase; letter-spacing: 0.5px; }
        .error-msg { color: var(--alert-red); font-size: 12px; text-align: center; margin-top: 12px; display: none; }
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
            <div class="brand-logo"></div>
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
                <p>
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
            <div class="metric-val" id="totalCastedCounter" style="color: var(--accent-neon);">1,432</div>
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
            <button class="btn-login" style="width:100%; margin-top:14px; border-color:transparent; color:var(--text-muted);" onclick="toggleAuthModal(false)">Cancel</button>
        </div>
    </div>

    <script>
        // Roster Database Setup
        const rosterDataset = {
            sec: ["CA B Sandhya, FCA", "CA T. Jayakumar, FCA", "CA M. Ramanujam, FCA", "CA S. Meenakshi, FCA", "CA R. Anand, FCA", "CA K. Elangovan, FCA"],
            asst: ["CA V Vanitha, FCA", "CA P. Subramanian, FCA", "CA V. Senthil Kumar, FCA", "CA K. Paneerselvam, FCA", "CA N. Kathiresan, FCA", "CA R. Rajarajan, FCA", "CA M. Maruthu Pandian, FCA", "CA S. Loganathan, FCA", "CA G. Balasubramanian, FCA"],
            jun: ["CA S. Thangavelu, FCA", "CA M. Muthu Krishnan, FCA", "CA C. Srinivasan, FCA"]
        };

        let ballotScorecard = { sec: {}, asst: {}, jun: {} };
        let activeStealthWeights = { sec: null, asst: null, jun: null };
        let currentAggregatedCastedCount = 1432;
        const ABSOLUTE_CAP_CEILING = 2753;

        function initializeTelemetryEngine() {
            let initialSecSum = 0, initialAsstSum = 0, initialJunSum = 0;

            rosterDataset.sec.forEach((name) => {
                let initialVal = Math.floor(Math.random() * 40) + 210;
                ballotScorecard.sec[name] = initialVal;
                initialSecSum += initialVal;
            });
            rosterDataset.asst.forEach((name) => {
                let initialVal = Math.floor(Math.random() * 30) + 140;
                ballotScorecard.asst[name] = initialVal;
                initialAsstSum += initialVal;
            });
            rosterDataset.jun.forEach((name) => {
                let initialVal = Math.floor(Math.random() * 80) + 450;
                ballotScorecard.jun[name] = initialVal;
                initialJunSum += initialVal;
            });

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
                        return Math.floor(Math.random() * 220) + 180;
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
