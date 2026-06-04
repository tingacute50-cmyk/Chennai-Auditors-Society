<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chennai Auditors Society - Elite Live Election Dashboard</title>
    <style>
        :root {
            --bg-deep: #05050a;
            --bg-surface: #0b0f19;
            --bg-card: #121826;
            --border-glow: #1e293b;
            
            /* High-Vibrancy Neon Palette */
            --neon-cyan: #00f0ff;
            --neon-magenta: #ff007f;
            --neon-green: #39ff14;
            --neon-purple: #9d4edd;
            --neon-gold: #ffb703;
            
            /* Table Row Highlighting Palette */
            --leader-green: #39ff14;
            --runner-yellow: #fff200;
            
            --text-main: #f8fafc;
            --text-muted: #64748b;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            background-color: var(--bg-deep);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* LIVE TICKER - DYNAMIC NEON COLOR */
        .ticker-wrap {
            width: 100%;
            background: #000000;
            border-bottom: 2px solid var(--neon-magenta);
            padding: 12px 0;
            box-sizing: border-box;
            box-shadow: 0 0 15px rgba(255, 0, 127, 0.2);
        }
        .ticker {
            display: flex;
            white-space: nowrap;
            animation: marquee-scroll 25s linear infinite;
        }
        .ticker-item {
            display: inline-block;
            padding: 0 3rem;
            font-size: 13px;
            font-weight: 600;
            letter-spacing: 0.5px;
        }
        .ticker-item span {
            color: var(--neon-magenta);
            margin-right: 8px;
            text-shadow: 0 0 5px var(--neon-magenta);
        }
        @keyframes marquee-scroll {
            0% { transform: translate3d(100%, 0, 0); }
            100% { transform: translate3d(-100%, 0, 0); }
        }

        /* GLOWING NAVBAR */
        nav {
            background-color: var(--bg-surface);
            border-bottom: 1px solid rgba(0, 240, 255, 0.2);
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
        }
        .brand {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .brand-logo {
            width: 6px;
            height: 30px;
            background: linear-gradient(to bottom, var(--neon-cyan), var(--neon-magenta));
            border-radius: 3px;
            box-shadow: 0 0 10px var(--neon-cyan);
        }
        .brand h1 {
            margin: 0;
            font-size: 26px;
            font-weight: 900;
            letter-spacing: 1px;
            text-transform: uppercase;
            background: linear-gradient(45deg, #ffffff, var(--neon-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .btn-login {
            background: transparent;
            border: 2px solid var(--neon-cyan);
            color: var(--neon-cyan);
            padding: 10px 24px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: 700;
            font-size: 12px;
            letter-spacing: 1px;
            text-transform: uppercase;
            text-shadow: 0 0 5px var(--neon-cyan);
            box-shadow: 0 0 10px rgba(0, 240, 255, 0.1);
            transition: all 0.3s ease;
        }
        .btn-login:hover {
            background: var(--neon-cyan);
            color: #000;
            text-shadow: none;
            box-shadow: 0 0 20px var(--neon-cyan);
        }

        /* GRID SYSTEM */
        .main-layout {
            max-width: 1440px;
            margin: 40px auto;
            padding: 0 30px;
            display: grid;
            grid-template-columns: 3fr 1fr;
            gap: 30px;
        }
        .welcome-box {
            background: linear-gradient(135deg, #111625 0%, #070a12 100%);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-left: 4px solid var(--neon-cyan);
            border-radius: 12px;
            padding: 35px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        .welcome-box h2 { margin-top: 0; color: #fff; font-size: 26px; font-weight: 800; }
        .welcome-box p { color: #94a3b8; line-height: 1.7; margin: 0; font-size: 15px; }
        
        .deadline-box {
            background: var(--bg-surface);
            border: 1px solid var(--border-glow);
            border-top: 4px solid var(--neon-gold);
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        .deadline-box h3 { margin-top: 0; color: var(--neon-gold); border-bottom: 1px solid var(--border-glow); padding-bottom: 12px; font-size: 14px; text-transform: uppercase; letter-spacing: 1px; text-shadow: 0 0 5px rgba(255, 183, 3, 0.3);}
        .deadline-list { list-style: none; padding: 0; margin: 0; }
        .deadline-list li { margin-bottom: 20px; font-size: 13px; border-left: 2px solid var(--neon-magenta); padding-left: 14px; }
        .deadline-list li strong { color: #fff; display: block; font-size: 14px; margin-bottom: 4px; }

        /* ADMINISTRATIVE MANAGEMENT TERMINAL */
        .admin-panel {
            background: #090e1a;
            border: 2px dashed var(--neon-cyan);
            border-radius: 12px;
            padding: 30px;
            margin-bottom: 30px;
            display: none;
            box-shadow: 0 0 30px rgba(0, 240, 255, 0.15);
        }
        .admin-panel h3 { margin-top: 0; color: var(--neon-cyan); font-size: 18px; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 25px; text-shadow: 0 0 5px var(--neon-cyan); }
        .admin-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; margin-bottom: 25px;}
        .admin-select-box label { display: block; font-size: 11px; color: #94a3b8; margin-bottom: 8px; text-transform: uppercase; }
        .admin-select-box select { width: 100%; padding: 12px; background: var(--bg-surface); border: 1px solid var(--border-glow); color: #fff; border-radius: 6px; outline: none; font-weight: 600; }
        .admin-select-box select:focus { border-color: var(--neon-cyan); }
        .admin-actions { display: flex; gap: 20px; align-items: center; flex-wrap: wrap; }
        .btn-refresh { background: linear-gradient(90deg, #00f0ff, #0077ff); color: #fff; font-weight: 800; padding: 15px 40px; border: none; border-radius: 30px; cursor: pointer; text-transform: uppercase; letter-spacing: 1px; box-shadow: 0 0 15px rgba(0, 240, 255, 0.3); transition: all 0.2s; }
        .btn-refresh:hover { transform: scale(1.03); box-shadow: 0 0 25px var(--neon-cyan); }
        .btn-logout { background: transparent; border: 2px solid var(--neon-magenta); color: var(--neon-magenta); font-weight: 700; padding: 13px 30px; border-radius: 30px; cursor: pointer; text-transform: uppercase; letter-spacing: 1px; transition: all 0.2s; }
        .btn-logout:hover { background: var(--neon-magenta); color: #fff; box-shadow: 0 0 20px var(--neon-magenta); }

        /* STYLISH COLORFUL ELECTION PANELS */
        .election-container {
            background: var(--bg-surface);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.4);
        }
        .election-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-glow);
            padding-bottom: 20px;
            margin-bottom: 35px;
        }
        .election-header h2 { margin: 0; font-size: 24px; text-transform: uppercase; letter-spacing: 0.5px; font-weight: 900; }
        .live-badge { background: rgba(255, 0, 127, 0.1); border: 1px solid var(--neon-magenta); color: var(--neon-magenta); font-size: 11px; padding: 6px 16px; border-radius: 20px; font-weight: 800; letter-spacing: 1.5px; animation: glow-pulse 1.5s infinite; text-shadow: 0 0 5px var(--neon-magenta); }
        @keyframes glow-pulse { 0% { opacity: 0.6; box-shadow: 0 0 5px rgba(255,0,127,0.2); } 50% { opacity: 1; box-shadow: 0 0 15px rgba(255,0,127,0.5); } 100% { opacity: 0.6; box-shadow: 0 0 5px rgba(255,0,127,0.2); } }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 25px;
        }
        .post-card {
            background: var(--bg-card);
            border: 1px solid var(--border-glow);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            transition: transform 0.3s ease;
        }
        .post-card:hover { transform: translateY(-5px); }
        
        /* Neon Borders Assigned Per Category Box Headers */
        .post-card.card-sec { border-top: 4px solid var(--neon-cyan); }
        .post-card.card-asst { border-top: 4px solid var(--neon-purple); }
        .post-card.card-jun { border-top: 4px solid var(--neon-green); }

        .post-title {
            padding: 18px 22px;
            font-size: 15px;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-bottom: 1px solid var(--border-glow);
        }
        .card-sec .post-title { background: rgba(0, 240, 255, 0.05); color: var(--neon-cyan); }
        .card-asst .post-title { background: rgba(157, 78, 221, 0.05); color: var(--neon-purple); }
        .card-jun .post-title { background: rgba(57, 255, 20, 0.05); color: var(--neon-green); }
        
        /* HIGH-CONTRAST CANDIDATE VISIBILITY SYSTEM */
        .candidate-table { width: 100%; border-collapse: collapse; background: #0e1320; }
        .candidate-table th { background: rgba(0, 0, 0, 0.4); color: #94a3b8; font-size: 11px; text-transform: uppercase; letter-spacing: 1px; padding: 12px 22px; }
        .candidate-table th, .candidate-table td { padding: 15px 22px; text-align: left; font-size: 14px; }
        
        /* Universal Text Color Assignment: Black for names and votes across all data states */
        .candidate-table tr td, 
        .candidate-table tr td.vote-count { 
            color: #000000 !important; 
            font-weight: 700;
        }
        .candidate-table td.vote-count { font-family: monospace; font-size: 16px; text-align: right; }

        /* Leading candidate row style: Highlighted in clean Green background */
        .candidate-table tr.leader { 
            background-color: var(--leader-green) !important; 
        }
        
        /* Non-leading competitor rows style: Highlighted in solid Yellow background */
        .candidate-table tr.competitor { 
            background-color: var(--runner-yellow) !important;
            border-bottom: 1px solid rgba(0, 0, 0, 0.15);
        }
        .candidate-table tr:last-child { border-bottom: none; }

        /* FOOTER METRICS */
        .voter-footer {
            background: #020205;
            border-top: 1px solid var(--border-glow);
            padding: 35px 50px;
            margin-top: 60px;
            display: flex;
            justify-content: space-around;
            align-items: center;
            box-shadow: 0 -10px 30px rgba(0,0,0,0.5);
        }
        .metric-item { text-align: center; }
        .metric-label { font-size: 11px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1.5px; }
        .metric-val { font-size: 36px; font-weight: 900; color: #ffffff; font-family: monospace; margin-top: 8px; text-shadow: 0 0 10px rgba(255,255,255,0.1); }

        /* MODAL INTERFACE BLUR */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(2, 2, 5, 0.85);
            backdrop-filter: blur(8px);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .login-card {
            background: var(--bg-surface);
            border: 1px solid var(--neon-cyan);
            padding: 40px;
            border-radius: 16px;
            width: 360px;
            box-shadow: 0 20px 50px rgba(0, 240, 255, 0.1);
        }
        .login-card h3 { margin-top: 0; margin-bottom: 25px; text-align: center; font-size: 22px; font-weight: 800; text-transform: uppercase; letter-spacing: 0.5px; }
        .input-group { margin-bottom: 20px; }
        .input-group label { display: block; font-size: 11px; margin-bottom: 8px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; }
        .input-group input { width: 100%; padding: 14px; background: var(--bg-deep); border: 1px solid var(--border-glow); color: #fff; border-radius: 8px; box-sizing: border-box; outline: none; font-size: 14px; }
        .input-group input:focus { border-color: var(--neon-cyan); box-shadow: 0 0 10px rgba(0,240,255,0.2); }
        .btn-submit { width: 100%; padding: 14px; background: linear-gradient(90deg, var(--neon-cyan), #0077ff); border: none; color: #fff; border-radius: 8px; font-weight: 700; cursor: pointer; text-transform: uppercase; letter-spacing: 1px; box-shadow: 0 4px 15px rgba(0,240,255,0.2); }
        .error-msg { color: var(--neon-magenta); font-size: 12px; text-align: center; margin-top: 12px; display: none; text-shadow: 0 0 5px rgba(255,0,127,0.2); }
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

    <!-- NAVBAR -->
    <nav>
        <div class="brand">
            <div class="brand-logo"></div>
            <h1>Chennai Auditors Society</h1>
        </div>
        <button class="btn-login" id="loginBtn" onclick="toggleAuthModal(true)">Member Login</button>
    </nav>

    <!-- CONTENT SYSTEM LAYOUT -->
    <div class="main-layout">
        
        <!-- MAIN CONTENT SECTION -->
        <div>
            <div class="welcome-box">
                <h2>Welcome to the Premium Hub</h2>
                <p>
                    Serving practitioners and enterprise finance managers across Chennai. Access statutory resource maps, track modern policy adaptations, and interface securely with live institutional management boards below.
                </p>
            </div>

            <!-- HIDDEN CONTROL SUITE TERMINAL PANEL -->
            <div class="admin-panel" id="adminControlPanel">
                <h3>System Administration Terminal</h3>
                <div class="admin-grid">
                    <div class="admin-select-box">
                        <label>Secretary Calibration Favorite</label>
                        <select id="favSec"></select>
                    </div>
                    <div class="admin-select-box">
                        <label>Assistant Secretary Calibration Favorite</label>
                        <select id="favAsst"></select>
                    </div>
                    <div class="admin-select-box">
                        <label>Junior Secretary Calibration Favorite (25% Weight allocation)</label>
                        <select id="favJun"></select>
                    </div>
                </div>
                <div class="admin-actions">
                    <button class="btn-refresh" onclick="triggerIncrementalRefresh()">Refresh (Simulate Polls)</button>
                    <button class="btn-logout" onclick="executeSecureLogout()">Secure Logout</button>
                </div>
            </div>

            <!-- TIMELINE ELECTION DASHBOARD DISPLAY -->
            <div class="election-container">
                <div class="election-header">
                    <h2>Annual Institutional Election Results Dashboard</h2>
                    <div class="live-badge">● LIVE STREAMING</div>
                </div>

                <div class="results-grid">
                    <!-- SECRETARY PILLAR -->
                    <div class="post-card card-sec">
                        <div class="post-title">Secretary (6 Nominees)</div>
                        <table class="candidate-table">
                            <thead><tr><th>Nominee</th><th style="text-align:right;">Votes</th></tr></thead>
                            <tbody id="tbody-sec"></tbody>
                        </table>
                    </div>

                    <!-- ASSISTANT SECRETARY PILLAR -->
                    <div class="post-card card-asst">
                        <div class="post-title">Assistant Secretary (9 Nominees)</div>
                        <table class="candidate-table">
                            <thead><tr><th>Nominee</th><th style="text-align:right;">Votes</th></tr></thead>
                            <tbody id="tbody-asst"></tbody>
                        </table>
                    </div>

                    <!-- JUNIOR SECRETARY PILLAR -->
                    <div class="post-card card-jun">
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

    <!-- METRIC TRACKER FOOTER PANEL -->
    <div class="voter-footer">
        <div class="metric-item">
            <div class="metric-label">Total Electorate Strength</div>
            <div class="metric-val">2,753</div>
        </div>
        <div class="metric-item">
            <div class="metric-label">Polled Ballots Casted</div>
            <div class="metric-val" id="totalCastedCounter" style="color: var(--neon-cyan); text-shadow: 0 0 10px rgba(0,240,255,0.3);">1,432</div>
        </div>
    </div>

    <!-- SECURITY MATRIX MODAL -->
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
            sec: ["CA T. Jayakumar, FCA", "CA M. Ramanujam, FCA", "CA S. Meenakshi, FCA", "CA R. Anand, FCA", "CA K. Elangovan, FCA", "CA A. Rajesh, FCA"],
            asst: ["CA V Vanitha, FCA", "CA P. Subramanian, FCA", "CA V. Senthil Kumar, FCA", "CA K. Paneerselvam, FCA", "CA N. Kathiresan, FCA", "CA R. Rajarajan, FCA", "CA M. Maruthu Pandian, FCA", "CA S. Loganathan, FCA", "CA G. Balasubramanian, FCA"],
            jun: ["CA B Sandhya, FCA", "CA S. Thangavelu, FCA", "CA M. Muthu Krishnan, FCA"]
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
                let favoriteCandidate = activeStealthWeights[cat];

                if (favoriteCandidate) {
                    let premiumFavShare = Math.floor(dynamicBatchSize * 0.25);
                    let leftOverBatchPool = dynamicBatchSize - premiumFavShare;

                    let remainingNominees = nominees.filter(name => name !== favoriteCandidate);
                    let rawMathematicalWeights = remainingNominees.map(() => Math.floor(Math.random() * 40) + 10);
                    let weightSum = rawMathematicalWeights.reduce((a, b) => a + b, 0);
                    let runningBatchTally = 0;

                    remainingNominees.forEach((name, i) => {
                        let favIdx = nominees.indexOf(name);
                        if (i === remainingNominees.length - 1) {
                            distributions[favIdx] = leftOverBatchPool - runningBatchTally;
                        } else {
                            let slice = Math.round((rawMathematicalWeights[i] / weightSum) * leftOverBatchPool);
                            distributions[favIdx] = slice;
                            runningBatchTally += slice;
                        }
                    });

                    let mainFavIdx = nominees.indexOf(favoriteCandidate);
                    distributions[mainFavIdx] = premiumFavShare;

                } else {
                    let rawMathematicalWeights = nominees.map(() => Math.floor(Math.random() * 40) + 10);
                    let weightSum = rawMathematicalWeights.reduce((a, b) => a + b, 0);
                    let runningBatchTally = 0;

                    for (let i = 0; i < nominees.length; i++) {
                        if (i === nominees.length - 1) {
                            distributions[i] = dynamicBatchSize - runningBatchTally;
                        } else {
                            let slice = Math.round((rawMathematicalWeights[i] / weightSum) * dynamicBatchSize);
                            distributions[i] = slice;
                            runningBatchTally += slice;
                        }
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
                    let rowClass = isLeadNode ? 'leader' : 'competitor';
                    
                    tbody.innerHTML += `
                        <tr class="${rowClass}">
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
