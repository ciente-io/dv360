<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Display & Video 360 - Advertiser Dashboard</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: Roboto, -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
            font-size: 13px;
            color: #202124;
        }

        body {
            background-color: #ffffff;
            display: flex;
            height: 100vh;
            overflow: hidden;
        }

        /* Top Navbar */
        .top-navbar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 48px;
            background: #ffffff;
            border-bottom: 1px solid #dadce0;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 16px;
            z-index: 100;
        }

        .top-nav-left {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .menu-icon {
            cursor: pointer;
            padding: 8px;
            color: #5f6368;
        }

        .brand-logo {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 14px;
            font-weight: 500;
            color: #5f6368;
        }

        .brand-logo svg {
            width: 20px;
            height: 20px;
        }

        .breadcrumb {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-left: 12px;
            color: #5f6368;
        }

        .breadcrumb-subtitle {
            font-size: 10px;
            color: #70757a;
        }

        .breadcrumb-title {
            font-size: 13px;
            font-weight: 500;
            color: #202124;
        }

        .top-nav-right {
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .nav-icon {
            color: #5f6368;
            cursor: pointer;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .user-avatar {
            width: 28px;
            height: 28px;
            background-color: #4285f4;
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 500;
            font-size: 13px;
        }

        /* Left Collapsible/Expandable Sidebar */
        .sidebar {
            width: 220px;
            background: #f8f9fa;
            border-right: 1px solid #dadce0;
            margin-top: 48px;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            padding-top: 8px;
        }

        details.nav-group {
            width: 100%;
            margin-bottom: 2px;
        }

        summary.nav-header {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 8px 16px;
            color: #3c4043;
            font-weight: 500;
            cursor: pointer;
            list-style: none;
            user-select: none;
            position: relative;
        }

        summary.nav-header.resources-header {
            color: #0f9d58;
        }

        summary.nav-header::-webkit-details-marker {
            display: none;
        }

        summary.nav-header::before {
            content: "▾";
            font-size: 10px;
            color: #5f6368;
            position: absolute;
            left: 6px;
            transition: transform 0.2s;
        }

        details[open] > summary.nav-header::before {
            transform: rotate(0deg);
        }

        details:not([open]) > summary.nav-header::before {
            transform: rotate(-90deg);
        }

        summary.nav-header:hover {
            background-color: #f1f3f4;
        }

        .standalone-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 8px 16px 8px 24px;
            color: #3c4043;
            font-weight: 500;
            text-decoration: none;
            cursor: pointer;
        }

        .standalone-item:hover {
            background-color: #f1f3f4;
        }

        .standalone-item.active {
            background-color: #e8f0fe;
            color: #1a73e8;
            border-radius: 0 20px 20px 0;
            margin-right: 8px;
        }

        .sub-menu {
            display: flex;
            flex-direction: column;
            padding-left: 44px;
            padding-top: 2px;
            padding-bottom: 4px;
        }

        .sub-item {
            padding: 6px 8px;
            color: #3c4043;
            text-decoration: none;
            cursor: pointer;
            font-size: 13px;
            border-radius: 0 16px 16px 0;
            margin-right: 8px;
        }

        .sub-item:hover {
            color: #1a73e8;
        }

        .sub-item.active {
            color: #202124;
            background-color: #e6f4ea;
            font-weight: 500;
        }

        /* Main Content Container */
        .workspace {
            flex: 1;
            margin-top: 48px;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            background: #ffffff;
        }

        .view-section {
            display: none;
            flex-direction: column;
            height: 100%;
        }

        .view-section.active {
            display: flex;
        }

        .workspace-header {
            padding: 16px 24px 0 24px;
            position: relative;
        }

        .workspace-title {
            font-size: 22px;
            font-weight: 400;
            color: #202124;
            margin-bottom: 16px;
        }

        .feedback-icon {
            position: absolute;
            top: 16px;
            right: 24px;
            background: #5f6368;
            color: white;
            padding: 4px 6px;
            border-radius: 2px;
            font-size: 11px;
            cursor: pointer;
        }

        .tabs {
            display: flex;
            gap: 24px;
            border-bottom: 1px solid #dadce0;
        }

        .tab {
            padding: 8px 0;
            color: #5f6368;
            font-weight: 500;
            border-bottom: 2px solid transparent;
            cursor: pointer;
            text-transform: uppercase;
            font-size: 12px;
            letter-spacing: 0.3px;
        }

        .tab.active {
            color: #0f9d58;
            border-bottom: 2px solid #0f9d58;
        }

        .tab-campaign.active {
            color: #1a73e8;
            border-bottom: 2px solid #1a73e8;
        }

        .action-bar {
            padding: 12px 24px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .btn-green {
            background-color: #0f9d58;
            color: white;
            border: none;
            border-radius: 2px;
            padding: 8px 12px;
            font-weight: 500;
            cursor: pointer;
            text-transform: uppercase;
            font-size: 12px;
        }

        .btn-primary {
            background-color: #1a73e8;
            color: white;
            border: none;
            border-radius: 4px;
            padding: 8px 16px;
            font-weight: 500;
            cursor: pointer;
        }

        .btn-date {
            background: #ffffff;
            border: 1px solid #dadce0;
            border-radius: 4px;
            padding: 6px 12px;
            cursor: pointer;
            color: #3c4043;
            margin-left: 12px;
        }

        .filter-bar {
            padding: 8px 24px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-top: 1px solid #f1f3f4;
            border-bottom: 1px solid #dadce0;
            background: #ffffff;
        }

        .filter-label {
            color: #5f6368;
        }

        .filter-chip {
            background: #e8eaed;
            color: #3c4043;
            border-radius: 16px;
            padding: 4px 10px;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .filter-input-text {
            color: #5f6368;
            cursor: pointer;
        }

        .filter-input {
            border: none;
            outline: none;
            flex: 1;
            padding: 4px;
            color: #5f6368;
        }

        .table-container {
            flex: 1;
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
        }

        th {
            padding: 10px 16px;
            font-size: 11px;
            font-weight: 500;
            color: #5f6368;
            border-bottom: 1px solid #dadce0;
        }

        td {
            padding: 12px 16px;
            border-bottom: 1px solid #e8eaed;
            color: #3c4043;
        }

        .status-dot {
            height: 8px;
            width: 8px;
            background-color: #1e8e3e;
            border-radius: 50%;
            display: inline-block;
            margin-right: 8px;
        }

        .campaign-name {
            color: #1a73e8;
            cursor: pointer;
        }

        .campaign-id {
            color: #70757a;
            font-size: 11px;
            margin-left: 8px;
        }

        .numeric {
            text-align: right;
        }

        .pagination {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding: 12px 24px;
            gap: 16px;
            color: #5f6368;
            font-size: 12px;
            border-top: 1px solid #f1f3f4;
        }

        /* Empty State */
        .empty-state-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: #f8f9fa;
        }

        .empty-state-icon {
            width: 64px;
            height: 64px;
            background-color: #9e9e9e;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 16px;
        }

        .empty-state-icon::before {
            content: "≡";
            color: white;
            font-size: 32px;
            font-weight: bold;
        }

        .empty-state-link {
            color: #3b78e7;
            text-decoration: none;
            font-weight: 500;
            font-size: 12px;
            letter-spacing: 0.3px;
            cursor: pointer;
        }

        /* Fixed Far-Right Action Icons */
        .right-system-bar {
            width: 40px;
            background: #ffffff;
            border-left: 1px solid #dadce0;
            margin-top: 48px;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding-top: 12px;
            gap: 16px;
        }
    </style>
</head>
<body>

    <!-- Header Navigation Bar -->
    <header class="top-navbar">
        <div class="top-nav-left">
            <span class="menu-icon">☰</span>
            <div class="brand-logo">
                <svg viewBox="0 0 24 24" fill="#34A853"><path d="M8 5v14l11-7z"/></svg>
                Display & Video 360
            </div>
            <div class="breadcrumb">
                <span>&gt;</span>
                <div>
                    <div class="breadcrumb-subtitle">Advertiser</div>
                    <div class="breadcrumb-title">Adbell Media</div>
                </div>
            </div>
        </div>
        <div class="top-nav-right">
            <span class="nav-icon">🔍</span>
            <span class="nav-icon">🔔</span>
            <span class="nav-icon">👥</span>
            <span class="nav-icon">☑️</span>
            <span class="nav-icon">📊</span>
            <span class="nav-icon">💬</span>
            <span class="nav-icon">⚙️</span>
            <div class="user-avatar">K</div>
        </div>
    </header>

    <div style="display: flex; width: 100%;">
        
        <!-- Collapsible Accordion Navigation Sidebar -->
        <nav class="sidebar">
            <a class="standalone-item active" id="campaigns-btn">
                <span>🎯</span> Campaigns
            </a>

            <!-- Audiences Dropdown Section -->
            <details class="nav-group" open>
                <summary class="nav-header">
                    <span>👥</span> Audiences
                </summary>
                <div class="sub-menu">
                    <a class="sub-item">All audiences</a>
                    <a class="sub-item">Analysis</a>
                </div>
            </details>

            <!-- Creative Dropdown Section -->
            <details class="nav-group" open>
                <summary class="nav-header">
                    <span>🖼️</span> Creative
                </summary>
                <div class="sub-menu">
                    <a class="sub-item">Creatives</a>
                    <a class="sub-item">Preview sheets</a>
                    <a class="sub-item">Format gallery</a>
                    <a class="sub-item">Appeal history</a>
                </div>
            </details>

            <!-- Inventory Dropdown Section -->
            <details class="nav-group" open>
                <summary class="nav-header">
                    <span>📋</span> Inventory
                </summary>
                <div class="sub-menu">
                    <a class="sub-item">Plans</a>
                    <a class="sub-item">My inventory</a>
                    <a class="sub-item">Marketplace</a>
                    <a class="sub-item">Negotiations</a>
                </div>
            </details>

            <!-- Reports Dropdown Section -->
            <details class="nav-group" open>
                <summary class="nav-header">
                    <span>📊</span> Reports
                </summary>
                <div class="sub-menu">
                    <a class="sub-item">Instant & offline</a>
                    <a class="sub-item">Cross-media reach</a>
                </div>
            </details>

            <a class="standalone-item">
                <span>🧪</span> Experiments
            </a>
            <a class="standalone-item">
                <span>💡</span> Suggestions
            </a>
            
            <!-- Resources Dropdown Section -->
            <details class="nav-group" open>
                <summary class="nav-header resources-header">
                    <span>📁</span> Resources
                </summary>
                <div class="sub-menu">
                    <a class="sub-item">Brand Controls</a>
                    <a class="sub-item">Channels & Keywords</a>
                    <a class="sub-item" id="floodlight-btn">Floodlight Group</a>
                    <a class="sub-item">Triggers</a>
                    <a class="sub-item">YouTube Extensions</a>
                    <a class="sub-item">Location Lists</a>
                    <a class="sub-item">Experiments and Lift</a>
                </div>
            </details>

            <a class="standalone-item">
                <span>⚙️</span> Advertiser settings
            </a>
            <a class="standalone-item">
                <span>🕒</span> History
            </a>
        </nav>

        <!-- Main Workspace Area -->
        <main class="workspace">
            
            <!-- VIEW 1: Campaigns View -->
            <div id="campaigns-view" class="view-section active">
                <div class="workspace-header">
                    <h1 class="workspace-title">Campaigns</h1>
                    <div class="tabs">
                        <div class="tab tab-campaign active">Campaigns</div>
                        <div class="tab tab-campaign">Insertion orders</div>
                    </div>
                </div>

                <div class="action-bar">
                    <div>
                        <button class="btn-primary">New campaign</button>
                        <button class="btn-date">Dec 19, 2024 ▼</button>
                    </div>
                    <div>
                        <span class="nav-icon">🌪️</span>
                        <span class="nav-icon">⋮</span>
                    </div>
                </div>

                <div class="filter-bar">
                    <span style="color: #1a73e8;">🔍</span>
                    <div class="filter-chip">
                        Status: Active <span style="cursor: pointer; margin-left: 4px;">✕</span>
                    </div>
                    <input type="text" class="filter-input" placeholder="Enter a search term or select filters">
                    <span style="cursor: pointer; color: #70757a;">✕</span>
                </div>

                <!-- Main Table Section -->
                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th style="width: 30px;"><input type="checkbox"></th>
                                <th>Campaign</th>
                                <th>Delivery</th>
                                <th class="numeric">Budget</th>
                                <th class="numeric">Spent</th>
                                <th class="numeric">KPI Goal</th>
                                <th class="numeric">KPI Actual</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><input type="checkbox"></td>
                                <td>
                                    <span class="status-dot"></span>
                                    <span class="campaign-name">Campaign_Display_Search_2024</span>
                                    <span class="campaign-id">2385107</span>
                                </td>
                                <td>—</td>
                                <td class="numeric">Unknown</td>
                                <td class="numeric">A$2,943.38</td>
                                <td class="numeric">A$30.00 CPA</td>
                                <td class="numeric">A$0.30 CPA</td>
                            </tr>
                            <tr>
                                <td><input type="checkbox"></td>
                                <td>
                                    <span class="status-dot"></span>
                                    <span class="campaign-name">AU_Video_Awareness_Q4</span>
                                    <span class="campaign-id">53987540</span>
                                </td>
                                <td>—</td>
                                <td class="numeric">A$220,000.00</td>
                                <td class="numeric">A$6,295.74</td>
                                <td class="numeric">-</td>
                                <td class="numeric">-</td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <div class="pagination">
                    <span>Show rows:</span>
                    <select style="border: 1px solid #dadce0; padding: 2px 4px; border-radius: 4px;">
                        <option>20</option>
                        <option>50</option>
                    </select>
                    <span>1–2 of 2</span>
                </div>
            </div>

            <!-- VIEW 2: Floodlight Group View -->
            <div id="floodlight-view" class="view-section">
                <div class="workspace-header">
                    <h1 class="workspace-title">Floodlight Group</h1>
                    <span class="feedback-icon">💬</span>
                    <div class="tabs">
                        <div class="tab">BASIC DETAILS</div>
                        <div class="tab active">FLOODLIGHT ACTIVITIES</div>
                        <div class="tab">HISTORY</div>
                    </div>
                </div>

                <div class="action-bar">
                    <button class="btn-green">NEW FLOODLIGHT ACTIVITY</button>
                    <div>
                        <span class="nav-icon">☰</span>
                    </div>
                </div>

                <div class="filter-bar">
                    <span class="filter-label">Filter</span>
                    <div class="filter-chip">
                        Status: Active <span style="cursor: pointer; margin-left: 4px;">✕</span>
                    </div>
                    <span class="filter-input-text">Add filter</span>
                    <span style="cursor: pointer; color: #70757a; margin-left: auto;">✕</span>
                </div>

                <!-- Empty State View -->
                <div class="empty-state-container">
                    <div class="empty-state-icon"></div>
                    <a class="empty-state-link">NEW FLOODLIGHT ACTIVITY</a>
                </div>
            </div>

        </main>

        <!-- Tool Drawer Icons Column -->
        <aside class="right-system-bar">
            <span class="nav-icon">📝</span>
            <span class="nav-icon">❓</span>
            <span class="nav-icon">🔄</span>
        </aside>

    </div>

    <!-- JavaScript Navigation Handling -->
    <script>
        const floodlightBtn = document.getElementById('floodlight-btn');
        const campaignsBtn = document.getElementById('campaigns-btn');
        const floodlightView = document.getElementById('floodlight-view');
        const campaignsView = document.getElementById('campaigns-view');

        floodlightBtn.addEventListener('click', () => {
            // Hide campaigns view and show floodlight group view
            campaignsView.classList.remove('active');
            floodlightView.classList.add('active');

            // Toggle active sidebar styles
            campaignsBtn.classList.remove('active');
            floodlightBtn.classList.add('active');
        });

        campaignsBtn.addEventListener('click', () => {
            // Hide floodlight group view and show campaigns view
            floodlightView.classList.remove('active');
            campaignsView.classList.add('active');

            // Toggle active sidebar styles
            floodlightBtn.classList.remove('active');
            campaignsBtn.classList.add('active');
        });
    </script>

</body>
</html>
