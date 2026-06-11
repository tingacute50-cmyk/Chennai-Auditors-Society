<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tamil World Chatroom</title>
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #ff007f, #7f00ff, #00f0ff);
            --panel-bg: rgba(255, 255, 255, 0.95);
            --chat-bg: #fff5fa;
            --primary-color: #7f00ff;
            --accent-color: #ff007f;
            --bot-color: #ffaa00;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: var(--bg-gradient);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* View Modes */
        .desktop-view {
            width: 95vw;
            height: 90vh;
            max-width: 1400px;
            border-radius: 16px;
        }

        .mobile-view {
            width: 375px;
            height: 812px;
            border-radius: 32px;
            border: 8px solid #333;
        }

        /* Screen Wrapper */
        .app-container {
            background: var(--panel-bg);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            position: relative;
            transition: all 0.3s ease;
        }

        /* View Toggle Button */
        #view-toggle {
            position: fixed;
            top: 10px;
            right: 10px;
            background: #fff;
            border: 2px solid var(--primary-color);
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            z-index: 1000;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* Auth Screen */
        .auth-screen {
            position: absolute;
            inset: 0;
            background: #fff;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 30px;
            z-index: 100;
        }

        .auth-box {
            width: 100%;
            max-width: 340px;
            text-align: center;
        }

        .auth-box h2 {
            color: var(--primary-color);
            margin-bottom: 20px;
            font-size: 28px;
        }

        .auth-box input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }

        .auth-box button {
            width: 100%;
            padding: 12px;
            background: var(--bg-gradient);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 10px;
        }

        .auth-toggle-text {
            margin-top: 15px;
            font-size: 14px;
            color: #666;
            cursor: pointer;
        }

        /* Main App Layout */
        .main-app {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        /* Header */
        .app-header {
            background: linear-gradient(to right, var(--primary-color), var(--accent-color));
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
        }

        /* Sidebar User List */
        .sidebar {
            width: 32%;
            min-width: 280px;
            border-right: 2px solid #eee;
            display: flex;
            flex-direction: column;
            background: #f9f9f9;
        }

        .mobile-view .sidebar {
            display: none; 
        }

        .user-summary {
            padding: 10px;
            background: #eee;
            font-size: 13px;
            font-weight: bold;
            display: flex;
            justify-content: space-around;
            border-bottom: 1px solid #ddd;
        }

        .user-list {
            flex: 1;
            overflow-y: auto;
        }

        .user-item {
            padding: 12px;
            display: flex;
            flex-direction: column;
            border-bottom: 1px solid #eee;
            transition: background 0.2s ease;
            cursor: pointer;
        }

        .user-item:hover {
            background: #f0f0f0;
        }

        .user-item.current-user {
            background: #e8d5ff !important;
            font-weight: bold;
            border-left: 5px solid var(--primary-color);
            cursor: default;
        }

        .user-main-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .status-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }
        .online { background: #4caf50; }
        .offline { background: #9e9e9e; }

        .badge {
            background: red;
            color: white;
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 10px;
            margin-left: 5px;
        }

        /* Interactive Profile Sub-Menu */
        .profile-actions {
            display: none;
            gap: 8px;
            margin-top: 10px;
            padding-top: 8px;
            border-top: 1px dashed #ddd;
            justify-content: space-between;
        }

        .profile-actions button {
            flex: 1;
            padding: 6px 4px;
            border: 1px solid #ccc;
            background: #f5f5f5;
            color: #999;
            font-size: 11px;
            font-weight: bold;
            border-radius: 4px;
            cursor: not-allowed;
            text-transform: uppercase;
        }

        .profile-actions button.voice-btn {
            background: #e8f5e9;
            color: #81c784;
            border-color: #a5d6a7;
        }

        /* Chat Window */
        .chat-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: var(--chat-bg);
        }

        .chat-history {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .system-lock-banner {
            background: #ffebee;
            color: #c62828;
            border: 1px dashed #c62828;
            padding: 12px;
            text-align: center;
            border-radius: 8px;
            font-weight: bold;
            margin: 15px 0;
            font-size: 13px;
        }

        .msg {
            max-width: 80%;
            padding: 12px;
            border-radius: 12px;
            position: relative;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .msg-meta {
            font-size: 11px;
            color: #666;
            margin-bottom: 4px;
            display: flex;
            justify-content: space-between;
            gap: 15px;
        }

        .msg.bot {
            background: #fff3e0;
            border-left: 4px solid var(--bot-color);
            align-self: center;
            max-width: 90%;
        }
        .msg.bot .msg-meta { color: var(--bot-color); font-weight: bold; }

        .msg.left {
            background: white;
            align-self: flex-start;
            border-bottom-left-radius: 2px;
        }

        /* Disabled Input Box */
        .input-area {
            padding: 15px;
            background: #fff;
            border-top: 1px solid #eee;
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .input-area input {
            flex: 1;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            background: #f5f5f5;
            cursor: not-allowed;
        }

        /* Popup Box Warning */
        .popup-overlay {
            position: absolute;
            inset: 0;
            background: rgba(0,0,0,0.5);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 200;
        }

        .popup-box {
            background: white;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
            max-width: 300px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .popup-box h3 { color: var(--accent-color); margin-bottom: 10px; }
        .popup-box button {
            margin-top: 15px;
            padding: 8px 20px;
            background: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <button id="view-toggle" onclick="toggleViewMode()">Switch to Mobile View</button>

    <div id="app-container" class="app-container desktop-view">
        
        <div id="auth-screen" class="auth-screen">
            <div class="auth-box">
                <h2 id="auth-title">Login</h2>
                <input type="text" id="auth-username" placeholder="Username">
                <input type="password" id="auth-password" placeholder="Password">
                <button onclick="handleAuth()">Submit</button>
                <div class="auth-toggle-text" id="auth-toggle" onclick="toggleAuthMode()">Don't have an account? Sign Up</div>
            </div>
        </div>

        <div class="app-header">
            <span>🌟 TAMIL WORLD CHATROOM 🌟</span>
            <span id="header-user-display">Not Logged In</span>
        </div>

        <div class="main-app">
            
            <div class="sidebar">
                <div class="user-summary">
                    <span style="color: green;">● 1 Online</span>
                    <span style="color: gray;">● 72 Offline</span>
                </div>
                <div class="user-list" id="directory-list">
                    </div>
            </div>

            <div class="chat-area">
                <div class="chat-history">
                    
                    <div class="msg bot">
                        <div class="msg-meta"><span>🤖 Bot_Tamil_Anban</span><span>10-06-2026 22:01</span></div>
                        <div>Vanakkam! Welcome to Tamil World Chatroom! Keep conversations respectful and delightful. Enjoy your stay! 🙏</div>
                    </div>

                    <div class="msg bot">
                        <div class="msg-meta"><span>🤖 Bot_Nila_Tech</span><span>10-06-2026 22:02</span></div>
                        <div>Hello users! System health checks passed. Voice configurations loaded for community profiles. Room active! ⚡</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Karthik</span><span>10-06-2026 22:15</span></div>
                        <div>Yennapa solringah? Correct-ah update panna matingraha profile ah! Nan check pannen update eh aagala.</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Priya_Tnd</span><span>10-06-2026 22:22</span></div>
                        <div>No Karthik, system side issue illa. Neenga clear-a clear cache pannitu login panni check panni parunga first. Always blaming systems is not fair!</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Anbarasan</span><span>10-06-2026 22:45</span></div>
                        <div>Illai Priya, Karthik solrathu correct thaan. Ennakum sync aagala dashboard la data clear-ah. Database lag adikuthu nu nenaikuren.</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Selvi_Madurai</span><span>10-06-2026 23:10</span></div>
                        <div>Romba argument pannathinga mudhala. Admin rules follow pannunga clear instructions kuduthrukanga la step by step follow panna vendiyathutane?</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Karthik</span><span>10-06-2026 23:30</span></div>
                        <div>Enaku yarum instructions solla thandhai illa! System validation functional breakdown details verification check panni thaan pesuren!</div>
                    </div>

                    <div class="msg left">
                        <div class="msg-meta"><span>Priya_Tnd</span><span>10-06-2026 23:40</span></div>
                        <div>Abaaba mudiyala unga logic kooda! Let Super Admin evaluate everything directly. Unnecessary-ah overload pannathinga debate ah.</div>
                    </div>

                    <div class="system-lock-banner">
                        ⚠️ [10-06-2026 23:45] Chat history messaging functions have been disabled by Super Admin for manual profile validation processes.
                    </div>

                </div>

                <div class="input-area">
                    <input type="text" placeholder="Typing is disabled for manual user verification by Super Admin..." disabled>
                </div>
            </div>

        </div>

        <div id="popup-overlay" class="popup-overlay">
            <div class="popup-box">
                <h3>Action Restricted</h3>
                <p id="popup-message">Voice calling functionality is available only for fully verified community accounts.</p>
                <button onclick="closePopup()">Acknowledge</button>
            </div>
        </div>

    </div>

    <script>
        let isSignUpMode = false;
        let currentUser = "";

        // Combined pool of all 72 remaining users (All will show as offline)
        const allOtherUsers = [
            "Karthik", "Priya_Tnd", "Dinesh_V", "Meena_Ravi", "Suresh_Kumar", "Deepika_S", 
            "Arun_Pandian", "Janani_K", "Thala_Fans", "Vijay_VJ", "Anitha_M", "Rajesh_C",
            "Anbarasan", "Selvi_Madurai", "Elango_Vanangamudi", "Kavitha_Holdings", "Murugan_Vel", 
            "Divya_Praba", "Senthil_N", "Boomika_R", "Ganesh_P", "Lakshmi_Traders", "Naveen_Kumar",
            "Sangeetha_M", "Vikram_S", "Uma_Rani", "Prakash_R", "Chitra_Madhavan", "Balaji_T",
            "Subha_Seyal", "Kamal_Fans", "Srinivasan", "Kalaivani", "Mani_G", "Radha_V",
            "Hari_Prasath", "Revathi_K", "Saravanan", "Devi_Durga", "Ramesh_B", "Geetha_P",
            "Sanjay_M", "Nandhini_R", "Ashok_Kumar", "Preethi_S", "Venkatesh", "Abirami",
            "Jaya_Kumar", "Kokila_M", "Vignesh_W", "Malathi_T", "Sundar_A", "Bhavani_S",
            "Kathir_S", "Shanthi_R", "Prabhu_D", "Yamuna_N", "Kishore_K", "Thamarai",
            "Siva_Kumar", "Amutha_G", "Raj_Mohan", "Vijaya_L", "Anand_B", "Roopa_M",
            "Sathish_E", "Mythili_K", "Gopal_V", "Pavithra", "Loganathan", "Rekha_S", "Bharathi"
        ];

        function toggleAuthMode() {
            isSignUpMode = !isSignUpMode;
            document.getElementById("auth-title").innerText = isSignUpMode ? "Sign Up" : "Login";
            document.getElementById("auth-toggle").innerText = isSignUpMode ? "Already registered? Login" : "Don't have an account? Sign Up";
        }

        function handleAuth() {
            const userIn = document.getElementById("auth-username").value.trim();
            const passIn = document.getElementById("auth-password").value.trim();

            if(!userIn || !passIn) {
                alert("Please fill all fields.");
                return;
            }

            if(userIn === "Moderator 003" || userIn === "Galaxy2026") {
                loginSuccess(userIn);
                return;
            }

            if(isSignUpMode) {
                localStorage.setItem(`chatroom_usr_${userIn}`, passIn);
                alert("Registration Successful!");
                loginSuccess(userIn);
            } else {
                const checkedPass = localStorage.getItem(`chatroom_usr_${userIn}`);
                if(checkedPass && checkedPass === passIn) {
                    loginSuccess(userIn);
                } else {
                    alert("Invalid Credentials. Please sign up if you are a first-time user.");
                }
            }
        }

        function loginSuccess(username) {
            currentUser = username;
            document.getElementById("auth-screen").style.display = "none";
            document.getElementById("header-user-display").innerText = `User: ${username}`;
            renderUserDirectory();
        }

        function renderUserDirectory() {
            const container = document.getElementById("directory-list");
            container.innerHTML = "";

            // 1. Logged In User Profile - ALWAYS Top position and ALWAYS Online
            const selfItem = document.createElement("div");
            selfItem.className = "user-item current-user";
            let badgeMarkup = (currentUser === "Moderator 003") ? `<span class="badge">MODERATOR</span>` : ``;
            
            selfItem.innerHTML = `
                <div class="user-main-row">
                    <div class="user-info">
                        <span class="status-dot online"></span>
                        <span>${currentUser} (You) ${badgeMarkup}</span>
                    </div>
                </div>
            `;
            container.appendChild(selfItem);

            // 2. All 72 other users injected below - ALL explicitly Offline
            allOtherUsers.forEach((user, index) => {
                if(user !== currentUser) {
                    const item = document.createElement("div");
                    item.className = "user-item";
                    item.setAttribute("onclick", `toggleProfileMenu('offline-actions-${index}', event)`);
                    
                    item.innerHTML = `
                        <div class="user-main-row">
                            <div class="user-info">
                                <span class="status-dot offline"></span>
                                <span style="color:#666;">${user}</span>
                            </div>
                        </div>
                        <div class="profile-actions" id="offline-actions-%INDEX%">
                            <button disabled title="Messaging functions disabled by Admin">DM (Disabled)</button>
                            <button disabled title="Block actions disabled during verification">Block (Disabled)</button>
                            <button class="voice-btn" onclick="triggerCallPopup('${user}', event)" title="Voice Call Check">Call (Disabled)</button>
                        </div>
                    `.replace('%INDEX%', index);
                    
                    container.appendChild(item);
                }
            });
        }

        function toggleProfileMenu(menuId, event) {
            if(event.target.tagName === 'BUTTON') return;

            const element = document.getElementById(menuId);
            const isCurrentlyVisible = element.style.display === "flex";
            
            document.querySelectorAll('.profile-actions').forEach(el => el.style.display = "none");
            element.style.display = isCurrentlyVisible ? "none" : "flex";
        }

        function triggerCallPopup(targetUser, event) {
            event.stopPropagation(); 
            document.getElementById("popup-message").innerText = `Voice call function initializing to line [${targetUser}]... Access restriction flag found. Voice Call feature is only available for Verified Users.`;
            document.getElementById("popup-overlay").style.display = "flex";
        }

        function closePopup() {
            document.getElementById("popup-overlay").style.display = "none";
        }

        function toggleViewMode() {
            const app = document.getElementById("app-container");
            const btn = document.getElementById("view-toggle");
            
            if(app.classList.contains("desktop-view")) {
                app.classList.remove("desktop-view");
                app.classList.add("mobile-view");
                btn.innerText = "Switch to Desktop View";
            } else {
                app.classList.remove("mobile-view");
                app.classList.add("desktop-view");
                btn.innerText = "Switch to Mobile View";
            }
        }
    </script>
</body>
</html>
