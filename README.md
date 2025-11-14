
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Rings: GCD Channels & Farey Sequences</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', 'Times New Roman', serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
        }

        body.dark-theme {
            --bg-primary: #000000;
            --bg-secondary: #1a1a1a;
            --text-primary: #ffffff;
            --text-secondary: #cccccc;
            --border-color: #ffffff;
            --border-subtle: #333333;
            --accent-color: #ffffff;
            --hover-bg: #ffffff;
            --hover-text: #000000;
            --ring-line-color: rgba(255, 255, 255, 0.2);
            --connection-line-color: rgba(255, 255, 255, 0.3);
            --tooltip-bg: rgba(255, 255, 255, 0.95);
            --tooltip-text: #000000;
        }

        body.light-theme {
            --bg-primary: #ffffff;
            --bg-secondary: #f5f5f5;
            --text-primary: #000000;
            --text-secondary: #333333;
            --border-color: #000000;
            --border-subtle: #cccccc;
            --accent-color: #000000;
            --hover-bg: #000000;
            --hover-text: #ffffff;
            --ring-line-color: rgba(0, 0, 0, 0.2);
            --connection-line-color: rgba(0, 0, 0, 0.3);
            --tooltip-bg: rgba(0, 0, 0, 0.95);
            --tooltip-text: #ffffff;
        }

        .container {
            max-width: 1900px;
            margin: 0 auto;
            background: var(--bg-primary);
        }

        .header {
            background: var(--bg-primary);
            color: var(--text-primary);
            padding: 40px 20px;
            text-align: center;
            border-bottom: 2px solid var(--border-color);
            position: relative;
        }

        .header h1 {
            font-size: 36px;
            font-weight: 400;
            margin-bottom: 15px;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .header .subtitle {
            font-size: 18px;
            font-style: italic;
            opacity: 0.9;
            margin-bottom: 10px;
        }

        .header .author {
            font-size: 16px;
            font-weight: 600;
            margin-top: 15px;
            letter-spacing: 1px;
        }

        .theme-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            padding: 10px 20px;
            background: var(--bg-primary);
            color: var(--text-primary);
            border: 1px solid var(--border-color);
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s;
        }

        .theme-toggle:hover {
            background: var(--hover-bg);
            color: var(--hover-text);
        }

        .tabs {
            display: flex;
            background: var(--bg-primary);
            border-bottom: 1px solid var(--border-color);
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            background: var(--bg-primary);
            border: none;
            font-size: 14px;
            font-weight: 600;
            color: var(--text-secondary);
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-right: 1px solid var(--border-subtle);
        }

        .tab:last-child {
            border-right: none;
        }

        .tab.active {
            background: var(--hover-bg);
            color: var(--hover-text);
        }

        .tab:hover:not(.active) {
            color: var(--text-primary);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .intro-page {
            padding: 50px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .intro-page h2 {
            font-size: 28px;
            font-weight: 400;
            margin: 30px 0 15px 0;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
            letter-spacing: 1px;
        }

        .intro-page h3 {
            font-size: 20px;
            font-weight: 600;
            margin: 25px 0 10px 0;
            color: var(--text-primary);
        }

        .intro-page p {
            margin-bottom: 15px;
            text-align: justify;
        }

        .intro-box {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 20px;
            margin: 20px 0;
            border-radius: 0;
        }

        .starter-toolkit {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }

        .toolkit-card {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 20px;
        }

        .toolkit-card h4 {
            font-size: 18px;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .toolkit-card ol {
            margin-left: 20px;
        }

        .toolkit-card li {
            margin-bottom: 8px;
        }

        .main-content {
            display: flex;
            flex-direction: column;
        }

        .control-panel {
            background: var(--bg-primary);
            border-bottom: 1px solid var(--border-color);
            padding: 20px;
            max-height: 70vh;
            overflow-y: auto;
        }

        .control-section {
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            padding: 15px;
            margin-bottom: 15px;
        }

        .control-section h3 {
            font-size: 14px;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 1px solid var(--border-color);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .collapsible-header {
            cursor: pointer;
            user-select: none;
            position: relative;
            font-weight: bold;
            text-decoration: underline;
            padding-left: 25px;
        }

        .collapsible-header:hover {
            opacity: 0.8;
        }

        .toggle-icon {
            position: absolute;
            left: 0;
            transition: transform 0.3s ease;
            display: inline-block;
        }

        .collapsible-header.collapsed .toggle-icon {
            transform: rotate(-90deg);
        }

        .collapsible-content {
            max-height: 2000px;
            overflow: hidden;
            transition: max-height 0.3s ease;
        }

        .collapsible-content.collapsed {
            max-height: 0;
        }

        .control-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 12px;
            margin-bottom: 12px;
        }

        .control-group {
            margin-bottom: 12px;
        }

        .control-group label {
            display: block;
            font-size: 11px;
            font-weight: 500;
            color: var(--text-primary);
            margin-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .control-group input[type="number"],
        .control-group input[type="text"],
        .control-group select {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border-color);
            background: var(--bg-primary);
            color: var(--text-primary);
            border-radius: 0;
            font-size: 13px;
        }

        .control-group input:focus,
        .control-group select:focus {
            outline: none;
            border-color: var(--border-color);
            box-shadow: 0 0 5px var(--border-color);
        }

        .control-group input[type="range"] {
            width: 100%;
        }

        .control-group input[type="checkbox"] {
            width: 16px;
            height: 16px;
            margin-right: 6px;
            cursor: pointer;
        }

        .control-group input[type="color"] {
            width: 100%;
            height: 35px;
            border: 1px solid var(--border-color);
            background: var(--bg-primary);
            cursor: pointer;
        }

        .checkbox-label {
            display: flex;
            align-items: center;
            font-size: 11px;
            color: var(--text-primary);
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .dual-input {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 8px;
        }

        button {
            padding: 10px 16px;
            background: var(--hover-bg);
            color: var(--hover-text);
            border: 1px solid var(--border-color);
            border-radius: 0;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        button:hover {
            background: var(--bg-primary);
            color: var(--text-primary);
        }

        .button-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 8px;
        }

        .canvas-container {
            padding: 20px;
            background: var(--bg-primary);
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
        }

        #mainCanvas {
            border: 1px solid var(--border-color);
            border-radius: 0;
            box-shadow: 0 0 20px var(--border-subtle);
            background: var(--bg-primary);
            cursor: move;
            touch-action: none;
        }

        .tooltip {
            position: absolute;
            padding: 12px;
            background: var(--tooltip-bg);
            color: var(--tooltip-text);
            border: 1px solid var(--border-color);
            pointer-events: none;
            font-size: 11px;
            line-height: 1.6;
            opacity: 0;
            transition: opacity 0.2s;
            z-index: 1000;
            max-width: 300px;
            font-family: 'Courier New', monospace;
        }

        .stats-panel {
            width: 100%;
            max-width: 1000px;
            margin-top: 20px;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            padding: 15px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 12px;
        }

        .stat-item {
            padding: 10px;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
        }

        .stat-label {
            font-size: 10px;
            color: var(--text-primary);
            font-weight: 500;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .stat-value {
            font-size: 16px;
            font-weight: 600;
            color: var(--text-primary);
            margin-top: 4px;
        }

        .range-display {
            display: inline-block;
            margin-left: 8px;
            font-weight: 600;
            color: var(--text-primary);
            font-size: 11px;
        }

        .info-box {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 10px;
            font-size: 11px;
            color: var(--text-primary);
            margin-top: 10px;
        }

        .floating-update-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 9999;
            padding: 15px 25px;
            background: var(--hover-bg);
            color: var(--hover-text);
            border: 2px solid var(--border-color);
            border-radius: 50px;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        .floating-update-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
            background: var(--bg-primary);
            color: var(--text-primary);
        }

        .floating-update-btn:active {
            transform: translateY(-1px);
        }

        .floating-center-btn {
            position: fixed;
            bottom: 90px;
            right: 30px;
            z-index: 9999;
            padding: 15px 25px;
            background: #4CAF50;
            color: #ffffff;
            border: 2px solid var(--border-color);
            border-radius: 50px;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        .floating-center-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
            background: #45a049;
        }

        .floating-center-btn:active {
            transform: translateY(-1px);
        }

        .floating-export-btn {
            position: fixed;
            right: 30px;
            z-index: 9999;
            padding: 12px 20px;
            background: #2196F3;
            color: #ffffff;
            border: 2px solid var(--border-color);
            border-radius: 50px;
            font-size: 13px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        .export-png {
            bottom: 150px;
        }

        .export-csv {
            bottom: 210px;
            background: #FF9800;
        }

        .floating-export-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.4);
        }

        .export-png:hover {
            background: #1976D2;
        }

        .export-csv:hover {
            background: #F57C00;
        }

        .floating-export-btn:active {
            transform: translateY(-1px);
        }

        .preset-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 6px;
        }

        .tracker-display {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 12px;
            margin-top: 10px;
        }

        .tracker-display h4 {
            color: var(--text-primary);
            font-size: 12px;
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .tracker-info {
            font-size: 11px;
            line-height: 1.6;
            color: var(--text-primary);
        }

        .theory-section {
            padding: 50px;
            max-width: 1200px;
            margin: 0 auto;
        }

        .theory-section h2 {
            font-size: 28px;
            font-weight: 400;
            margin: 30px 0 15px 0;
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
            letter-spacing: 1px;
        }

        .theory-section h3 {
            font-size: 20px;
            font-weight: 600;
            margin: 25px 0 10px 0;
        }

        .theory-section p {
            margin-bottom: 15px;
            text-align: justify;
        }

        .formula {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 15px;
            margin: 15px 0;
            font-family: 'Courier New', monospace;
            font-size: 13px;
        }

        .formula-title {
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .example-box {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            padding: 15px;
            margin: 15px 0;
        }

        ul, ol {
            margin-left: 25px;
            margin-bottom: 15px;
        }

        li {
            margin-bottom: 8px;
        }

        @media (max-width: 768px) {
            .control-row {
                grid-template-columns: 1fr;
            }
            .preset-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .starter-toolkit {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
                    <div class="header">
            <h1>Modular Rings</h1>
            <div class="subtitle">GCD Channels, Farey Sequences & Prime Distribution</div>
            <div class="author">By Wessen Getachew</div>
            <div style="margin-top: 10px; font-size: 14px;">
                <a href="https://wessengetachew.github.io/GCD/" target="_blank" style="color: var(--text-primary); text-decoration: none; margin: 0 8px; border-bottom: 1px solid var(--text-primary);">GCD</a>
                <a href="https://wessengetachew.github.io/Primes/" target="_blank" style="color: var(--text-primary); text-decoration: none; margin: 0 8px; border-bottom: 1px solid var(--text-primary);">Primes</a>
                <a href="https://wessengetachew.github.io/Ethiopian/" target="_blank" style="color: var(--text-primary); text-decoration: none; margin: 0 8px; border-bottom: 1px solid var(--text-primary);">Pi Calculator</a>
                <a href="https://wessengetachew.github.io/2pir/" target="_blank" style="color: var(--text-primary); text-decoration: none; margin: 0 8px; border-bottom: 1px solid var(--text-primary);">2πr</a>
            </div>
            <button class="theme-toggle" onclick="toggleTheme()">
                <span id="themeText">Light Mode</span>
            </button>
        </div>

        <div class="tabs">
            <button class="tab" onclick="switchTab('visualization')">Visualization</button>
            <button class="tab" onclick="switchTab('understanding')">Theoretical Framework</button>
            <button class="tab" onclick="switchTab('composite-projection')">Composite Projection</button>
        </div>

        <div id="visualizationTab" class="tab-content active">
            <div class="main-content">
                <div class="control-panel">
                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Theorem Mode
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label>Display Mode</label>
                            <select id="theoremMode">
                                <option value="none">Standard Mode</option>
                                <option value="prime-avoidance">Prime Channel Avoidance</option>
                                <option value="composite-projection">Composite Channel Projection</option>
                                <option value="both">Combined Analysis</option>
                            </select>
                        </div>
                        
                        <div id="theoremModeSettings" style="display: none;">
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="highlightFareyChannels" checked>
                                    Highlight Farey Flow Lines (Gold)
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="highlightPrimeOrbits" checked>
                                    Show Prime Coprime Manifolds (Cyan)
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="highlightCompositeProjection" checked>
                                    Show Composite Projections (Red)
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showChannelMultiplicity" checked>
                                    Display Channel Multiplicity (d = M/M')
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showInterstitialRegions">
                                    Shade Interstitial Lattice Regions
                                </label>
                            </div>
                            
                            <div class="info-box">
                                <strong>Prime Channel Avoidance:</strong> Prime moduli avoid all Farey channels, forming independent coprime manifolds.<br>
                                <strong>Composite Channel Projection:</strong> Composite moduli project onto dense Farey channel networks.
                            </div>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Modulus Configuration
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label>Modulus Selection Mode</label>
                            <select id="modSelectionMode">
                                <option value="range">Range (Start to End)</option>
                                <option value="fibonacci">Fibonacci Sequence</option>
                                <option value="primes">Prime Moduli Only</option>
                                <option value="powers-of-2">Powers of 2</option>
                                <option value="powers-of-3">Powers of 3</option>
                                <option value="M30-sequence">M_n = 30×2^n</option>
                                <option value="custom">Custom List</option>
                            </select>
                        </div>

                        <div id="rangeInputs">
                            <div class="control-row">
                                <div class="control-group">
                                    <label>Start Modulus</label>
                                    <input type="number" id="modMin" value="1" min="1" max="10000">
                                </div>
                                <div class="control-group">
                                    <label>End Modulus</label>
                                    <input type="number" id="modMax" value="60" min="1" max="10000">
                                </div>
                                <div class="control-group">
                                    <label>Step</label>
                                    <input type="number" id="modStep" value="1" min="1" max="100">
                                </div>
                            </div>
                        </div>

                        <div id="sequenceInputs" style="display: none;">
                            <div class="control-group">
                                <label>Maximum Value</label>
                                <input type="number" id="sequenceMax" value="100" min="1" max="10000">
                            </div>
                            <div class="control-group">
                                <label>Number of Terms</label>
                                <input type="number" id="sequenceTerms" value="5" min="1" max="50">
                            </div>
                        </div>

                        <div id="customInputs" style="display: none;">
                            <div class="control-group">
                                <label>Custom Moduli (comma-separated)</label>
                                <input type="text" id="customModuli" value="1,2,3,5,8,13,21,34" placeholder="e.g., 1,6,10,15,21,28">
                            </div>
                            <div class="info-box">
                                Enter any sequence of moduli. If 1 is included, the unit circle will be shown.
                            </div>
                        </div>

                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="includeUnitCircle" checked>
                                Always Include Unit Circle (m=1)
                            </label>
                        </div>
                        
                        <div class="preset-grid">
                            <button onclick="setPreset(0)">n=0 (30)</button>
                            <button onclick="setPreset(1)">n=1 (60)</button>
                            <button onclick="setPreset(2)">n=2 (120)</button>
                            <button onclick="setPreset(3)">n=3 (240)</button>
                            <button onclick="setPreset(4)">n=4 (480)</button>
                            <button onclick="setPreset(5)">n=5 (960)</button>
                        </div>
                        <button onclick="setPresetRange()" style="width: 100%; margin-top: 8px;">All: 30 to 960</button>
                        
                        <div class="info-box" style="margin-top: 10px;">
                            <div id="selectedModuliDisplay" style="font-size: 11px;">
                                <strong>Selected Moduli:</strong> <span id="moduliList">1 to 60 (step 1)</span>
                            </div>
                            <button onclick="clearCache()" style="width: 100%; margin-top: 5px; padding: 8px; font-size: 11px;">Clear Cache</button>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Connection Lines
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="enableConnections">
                                Enable Connections
                            </label>
                        </div>
                        <div class="control-group">
                            <label>Connection Mode</label>
                            <select id="connectionMode">
                                <option value="none">None</option>
                                <option value="next-mod">r to r (Next Modulus)</option>
                                <option value="binary-lift">r to r+M (Binary Lift)</option>
                                <option value="double-lift">r to r+M×2^n</option>
                                <option value="same-mod">Same Modulus Connections</option>
                                <option value="specific-mod">Specific Modulus Only</option>
                            </select>
                        </div>
                        <div class="control-group" id="specificModGroup" style="display: none;">
                            <label>Specific Modulus Value</label>
                            <input type="number" id="specificModValue" value="30" min="1">
                        </div>
                        <div class="control-group" id="sameModOptionsGroup" style="display: none;">
                            <label>Same-Mod Pattern</label>
                            <select id="sameModPattern">
                                <option value="all">All Points Connected</option>
                                <option value="sequential">Sequential (r to r+1)</option>
                                <option value="open-only">Open Channels Only</option>
                                <option value="by-gap">By Gap Interval</option>
                            </select>
                        </div>
                        <div class="control-group" id="sameModGapGroup" style="display: none;">
                            <label>Connection Gap</label>
                            <input type="number" id="sameModGap" value="1" min="1">
                        </div>
                        <div class="control-group">
                            <label>Connection Opacity <span class="range-display" id="connOpacityDisplay">0.3</span></label>
                            <div class="dual-input">
                                <input type="range" id="connOpacity" min="0.1" max="1" step="0.1" value="0.3">
                                <input type="number" id="connOpacityNum" min="0" max="1" step="0.1" value="0.3">
                            </div>
                        </div>
                        <div class="control-group">
                            <label>Connection Line Width <span class="range-display" id="connLineWidthDisplay">1</span></label>
                            <div class="dual-input">
                                <input type="range" id="connLineWidth" min="0.5" max="5" step="0.5" value="1">
                                <input type="number" id="connLineWidthNum" min="0.5" max="10" step="0.5" value="1">
                            </div>
                        </div>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="onlyOpenConn" checked>
                                Only Connect Open Channels
                            </label>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Rotation Controls
                        </h3>
                        <div class="collapsible-content collapsed">
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="invertModOrder">
                                Invert Modulus Order (Outer↔Inner)
                            </label>
                        </div>

                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="autoRotate" checked>
                                Auto-Rotate on Slider Change
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>Global Rotation <span class="range-display" id="globalSpeedDisplay">0</span> deg/frame</label>
                            <div class="dual-input">
                                <input type="range" id="globalSpeed" min="0" max="360" step="0.5" value="0">
                                <input type="number" id="globalSpeedNum" min="0" max="360" step="0.5" value="0">
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label>Individual Mod <span class="range-display" id="modRotSpeedDisplay">0</span> deg/frame</label>
                            <div class="dual-input">
                                <input type="range" id="modRotSpeed" min="0" max="360" step="0.5" value="0">
                                <input type="number" id="modRotSpeedNum" min="0" max="360" step="0.5" value="0">
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label>Per-Ring Spiral <span class="range-display" id="perRingSpiralDisplay">0</span>° per ring</label>
                            <div class="dual-input">
                                <input type="range" id="perRingSpiral" min="-360" max="360" step="5" value="0">
                                <input type="number" id="perRingSpiralNum" min="-360" max="360" step="5" value="0">
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label>Spiral Mode</label>
                            <select id="spiralMode">
                                <option value="linear">Linear (Constant Step)</option>
                                <option value="fibonacci">Fibonacci (Golden Spiral)</option>
                                <option value="logarithmic">Logarithmic (Exponential)</option>
                                <option value="sine">Sine Wave</option>
                            </select>
                        </div>
                        
                        <div class="preset-grid" style="margin-top: 10px;">
                            <button onclick="setSpiralPreset('gentle')">Gentle</button>
                            <button onclick="setSpiralPreset('moderate')">Moderate</button>
                            <button onclick="setSpiralPreset('strong')">Strong</button>
                            <button onclick="setSpiralPreset('golden')">Golden</button>
                            <button onclick="setSpiralPreset('galaxy')">Galaxy</button>
                            <button onclick="setSpiralPreset('dna')">DNA</button>
                        </div>
                        
                        <div class="control-group">
                            <label>Speed Gradient</label>
                            <select id="speedGradient">
                                <option value="none">No Gradient</option>
                                <option value="inner-to-outer">Inner to Outer</option>
                                <option value="outer-to-inner">Outer to Inner</option>
                            </select>
                        </div>
                        
                        <div class="control-group">
                            <label>Gradient Strength <span class="range-display" id="gradientStrengthDisplay">1.0</span></label>
                            <div class="dual-input">
                                <input type="range" id="gradientStrength" min="0" max="3" step="0.1" value="1.0">
                                <input type="number" id="gradientStrengthNum" min="0" max="5" step="0.1" value="1.0">
                            </div>
                        </div>
                        
                        <div class="button-group">
                            <button id="playButton" onclick="toggleAnimation()" style="background: #00ff00; color: #000000;">Play</button>
                            <button onclick="resetRotations()" style="background: var(--bg-secondary); color: var(--text-primary);">Reset</button>
                        </div>
                        
                        <div class="info-box" id="animationStatus">
                            Status: Stopped
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Residue Tracker
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="enableTracker">
                                Enable Tracker
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>Track Mode</label>
                            <select id="trackMode">
                                <option value="manual">Manual Input (Multiple)</option>
                                <option value="slider">Slider (Single r)</option>
                            </select>
                        </div>
                        
                        <div id="manualTrackInputs">
                            <div class="control-group">
                                <label>Track Residues (comma-separated)</label>
                                <input type="text" id="trackedResidues" value="1" placeholder="e.g., 1,7,13,19">
                            </div>
                        </div>
                        
                        <div id="sliderTrackInputs" style="display: none;">
                            <div class="control-group">
                                <label>Track Residue r: <span class="range-display" id="sliderResidueDisplay">1</span></label>
                                <div class="dual-input">
                                    <input type="range" id="sliderResidue" min="0" max="100" step="1" value="1">
                                    <input type="number" id="sliderResidueNum" min="0" max="10000" step="1" value="1">
                                </div>
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label>Filter by Modulus (optional)</label>
                            <input type="number" id="trackerModFilter" placeholder="Leave empty for all">
                        </div>
                        <div class="control-group">
                            <label>Tracker Color</label>
                            <input type="color" id="trackerColor" value="#ffffff">
                        </div>
                        <div class="control-group">
                            <label>Tracker Size <span class="range-display" id="trackerSizeDisplay">8</span></label>
                            <div class="dual-input">
                                <input type="range" id="trackerSize" min="4" max="20" step="1" value="8">
                                <input type="number" id="trackerSizeNum" min="4" max="30" step="1" value="8">
                            </div>
                        </div>
                        <div class="tracker-display" id="trackerInfo" style="display: none;">
                            <h4>Tracked Residues Info</h4>
                            <div class="tracker-info" id="trackerInfoContent"></div>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Coloring Schemes
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label>Open Channel Mode</label>
                            <select id="openColorMode">
                                <option value="solid">Solid Color</option>
                                <option value="by-residue" selected>By Residue (r)</option>
                                <option value="by-modulus">By Modulus (m)</option>
                                <option value="by-integer">By Integer Value</option>
                                <option value="by-spf">By Smallest Prime Factor</option>
                                <option value="by-lpf">By Largest Prime Factor</option>
                                <option value="by-prime-power">By Prime Power</option>
                                <option value="by-angle">By Angle</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Closed Channel Mode</label>
                            <select id="closedColorMode">
                                <option value="solid">Solid Color</option>
                                <option value="by-gcd">By GCD Value</option>
                                <option value="by-spf">By Smallest Prime Factor</option>
                                <option value="by-lpf">By Largest Prime Factor</option>
                                <option value="by-modulus">By Modulus (m)</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Base Open Color</label>
                            <input type="color" id="baseOpenColor" value="#00ff00">
                        </div>
                        <div class="control-group">
                            <label>Base Closed Color</label>
                            <input type="color" id="baseClosedColor" value="#ff0000">
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Display Settings
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-row">
                            <div class="control-group">
                                <label>Display Mode</label>
                                <select id="displayMode">
                                    <option value="rings">Concentric Rings</option>
                                    <option value="unit">Unit Circle</option>
                                </select>
                            </div>
                            <div class="control-group">
                                <label>Angular Mapping</label>
                                <select id="angularMapping">
                                    <option value="standard">Standard: 2πr/m</option>
                                    <option value="half">Half: πr/m</option>
                                    <option value="inverted">Inverted: 2π(m-r)/m</option>
                                    <option value="negative" selected>Negative: -2πr/m</option>
                                </select>
                            </div>
                            <div class="control-group">
                                <label>Point Size <span class="range-display" id="pointSizeDisplay">4</span></label>
                                <div class="dual-input">
                                    <input type="range" id="pointSize" min="1" max="15" step="0.5" value="4">
                                    <input type="number" id="pointSizeNum" min="1" max="20" step="0.5" value="4">
                                </div>
                            </div>
                        </div>
                        <div class="control-row">
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="performanceMode" checked>
                                    Performance Mode (For Large Datasets)
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="enablePointClick">
                                    Enable Point Click Info
                                </label>
                            </div>
                        </div>
                        <div class="control-row">
                            <div class="control-group">
                                <label>Background Color</label>
                                <input type="color" id="bgColor" value="#000000">
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showOpen" checked>
                                    Show Open
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showClosed" checked>
                                    Show Closed
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showRingLines" checked>
                                    Ring Lines
                                </label>
                            </div>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Label Display
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="showLabels">
                                Show Point Labels
                            </label>
                        </div>
                        <div class="control-group">
                            <label>Label Type</label>
                            <select id="labelType">
                                <option value="residue">Residue (r)</option>
                                <option value="farey">Farey Fraction (r/m)</option>
                                <option value="theta">Angle θ (degrees)</option>
                                <option value="theta-rad">Angle θ (radians)</option>
                                <option value="modulus">Modulus (m)</option>
                                <option value="gcd">GCD(r,m)</option>
                                <option value="pair">(m,r)</option>
                                <option value="farey-reduced">Reduced Fraction</option>
                                <option value="euler-phi">φ(m)</option>
                                <option value="totient-index">Totient Index</option>
                                <option value="prime-factorization">Prime Factors</option>
                                <option value="coprime-status">Coprime Status</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Label Filter</label>
                            <select id="labelFilter">
                                <option value="all">All Points</option>
                                <option value="open-only">Open Channels Only</option>
                                <option value="closed-only">Closed Channels Only</option>
                                <option value="admissible">Gap Admissible Only</option>
                                <option value="primes">Prime Residues Only</option>
                                <option value="mod-specific">Specific Modulus</option>
                                <option value="gcd-specific">Specific GCD Value</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Filter Value (if applicable)</label>
                            <input type="number" id="labelFilterValue" value="30" min="1">
                        </div>
                        <div class="control-group">
                            <label>Label Size <span class="range-display" id="labelSizeDisplay">10</span></label>
                            <div class="dual-input">
                                <input type="range" id="labelSize" min="6" max="20" step="1" value="10">
                                <input type="number" id="labelSizeNum" min="6" max="30" step="1" value="10">
                            </div>
                        </div>
                        <div class="control-group">
                            <label>Label Color</label>
                            <input type="color" id="labelColor" value="#ffffff">
                        </div>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="labelBackground" checked>
                                Label Background
                            </label>
                        </div>
                        <div class="control-group">
                            <label>Label Spacing <span class="range-display" id="labelSpacingDisplay">12</span></label>
                            <div class="dual-input">
                                <input type="range" id="labelSpacing" min="8" max="30" step="1" value="12">
                                <input type="number" id="labelSpacingNum" min="8" max="50" step="1" value="12">
                            </div>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Gap Analysis
                        </h3>
                        <div class="collapsible-content collapsed">
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="enableGapAnalysis">
                                Enable Gap Analysis
                            </label>
                        </div>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="showGapLines">
                                Show Gap Connection Lines
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="onlyPrimeGaps">
                                Only Show Prime-to-Prime Gaps
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="highlightAdmissible">
                                Highlight Admissible Points (Purple)
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>Gap Configuration</label>
                            <select id="gapPreset" onchange="applyGapPreset()">
                                <option value="custom">Custom</option>
                                <option value="twin">Twin Primes (2)</option>
                                <option value="cousin">Cousin Primes (4)</option>
                                <option value="sexy">Sexy Primes (6)</option>
                                <option value="twin-cousin">Twin + Cousin (2,4)</option>
                                <option value="twin-sexy">Twin + Sexy (2,6)</option>
                                <option value="prime-triplet">Prime Triplet (2,4)</option>
                                <option value="prime-quadruplet">Prime Quadruplet (2,4,6)</option>
                                <option value="first-hardy">First Hardy-Littlewood (2,6,8)</option>
                                <option value="admissible-5">Admissible 5-tuple (2,6,8,12)</option>
                                <option value="sexy-pair">Sexy Pair (6,12)</option>
                            </select>
                        </div>

                        <div class="control-group">
                            <label>Gap Values (comma-separated)</label>
                            <input type="text" id="gapValues" value="2" placeholder="e.g., 2,4,6">
                        </div>

                        <div class="control-group">
                            <label>Gap Line Opacity <span class="range-display" id="gapOpacityDisplay">0.5</span></label>
                            <div class="dual-input">
                                <input type="range" id="gapOpacity" min="0.1" max="1" step="0.1" value="0.5">
                                <input type="number" id="gapOpacityNum" min="0" max="1" step="0.1" value="0.5">
                            </div>
                        </div>

                        <div class="control-group">
                            <label>Gap Line Width <span class="range-display" id="gapLineWidthDisplay">1.5</span></label>
                            <div class="dual-input">
                                <input type="range" id="gapLineWidth" min="0.5" max="5" step="0.5" value="1.5">
                                <input type="number" id="gapLineWidthNum" min="0.5" max="10" step="0.5" value="1.5">
                            </div>
                        </div>

                        <div id="gapColorPickers" style="margin-top: 10px;">
                            <!-- Will be populated dynamically -->
                        </div>

                        <div class="info-box" id="gapInfo" style="margin-top: 10px;">
                            <strong>Active Gaps:</strong> <span id="activeGapsDisplay">None</span>
                        </div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3 class="collapsible-header collapsed" onclick="toggleSection(this)">
                            <span class="toggle-icon">▼</span> Export Settings
                        </h3>
                        <div class="collapsible-content collapsed">
                        
                        <div class="control-group">
                            <label>Export Title</label>
                            <input type="text" id="exportTitle" value="Modular Rings Visualization" placeholder="Enter title for export">
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="includeLegend" checked>
                                Include Parameter Legend
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>Export Resolution</label>
                            <select id="exportResolution">
                                <option value="1">Standard (1000×800)</option>
                                <option value="2">HD (2000×1600)</option>
                                <option value="3">2K (3000×2400)</option>
                                <option value="4" selected>4K (4000×3200)</option>
                                <option value="6">6K (6000×4800)</option>
                                <option value="8">8K (8000×6400)</option>
                            </select>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="includeColorKey" checked>
                                Include Color Key Legend
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="includeTimestamp" checked>
                                Include Timestamp
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>CSV Export Options</label>
                            <select id="csvExportMode">
                                <option value="basic">Basic (m, r, gcd, channel)</option>
                                <option value="detailed" selected>Detailed (all properties)</option>
                                <option value="statistical">Statistical Summary</option>
                                <option value="gap-analysis">Gap Analysis Data</option>
                            </select>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="csvIncludeHeader" checked>
                                Include Column Headers
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="csvIncludeMetadata" checked>
                                Include Configuration Metadata
                            </label>
                        </div>
                        
                        <div class="button-group">
                            <button onclick="exportImage()">Export PNG</button>
                            <button onclick="exportCSV()">Export CSV</button>
                        </div>
                        </div>
                    </div>

                    <div class="button-group">
                        <button onclick="updateVisualization()">Update</button>
                        <button onclick="resetSettings()">Reset</button>
                    </div>

                    <div class="info-box">
                        Drag to pan • Scroll to zoom • Hover for details • Click for info
                    </div>
                </div>

                <!-- Floating Update Button -->
                <button class="floating-update-btn" onclick="updateVisualization()" title="Update Visualization">
                    ⟳ Update
                </button>

                <div class="canvas-container" style="display: flex; gap: 20px; align-items: flex-start;">
                    <div style="flex: 1; display: flex; flex-direction: column; align-items: center;">
                        <canvas id="mainCanvas" width="1000" height="800" style="display: block;"></canvas>
                        <svg id="mainSVG" width="1000" height="800" style="display: none; border: 1px solid var(--border-color); background: #000000; cursor: move;">
                            <defs>
                                <filter id="glow">
                                    <feGaussianBlur stdDeviation="2" result="coloredBlur"/>
                                    <feMerge>
                                        <feMergeNode in="coloredBlur"/>
                                        <feMergeNode in="SourceGraphic"/>
                                    </feMerge>
                                </filter>
                            </defs>
                            <g id="svgMainGroup"></g>
                        </svg>
                        <div class="tooltip" id="tooltip"></div>
                    </div>
                    
                    <div id="pointInfoPanel" style="width: 320px; min-height: 400px; background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; display: none;">
                        <h3 style="margin: 0 0 15px 0; font-size: 16px; text-transform: uppercase; letter-spacing: 1px; border-bottom: 1px solid var(--border-color); padding-bottom: 10px;">Point Details</h3>
                        <div id="pointInfoContent" style="font-size: 13px; line-height: 1.8;">
                            <p style="opacity: 0.7; font-style: italic;">Click on a point to see details</p>
                        </div>
                        <button onclick="closePointInfo()" style="width: 100%; margin-top: 20px; padding: 10px; background: var(--bg-primary); color: var(--text-primary); border: 1px solid var(--border-color);">Close</button>
                    </div>
                    
                    <div class="stats-panel">
                        <h3 style="margin-bottom: 12px; font-size: 14px; text-transform: uppercase; letter-spacing: 1px;">Statistics</h3>
                        <div class="stats-grid">
                            <div class="stat-item">
                                <div class="stat-label">Total Points</div>
                                <div class="stat-value" id="statTotal">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Open Channels</div>
                                <div class="stat-value" id="statOpen">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Closed Channels</div>
                                <div class="stat-value" id="statClosed">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Open Ratio</div>
                                <div class="stat-value" id="statRatio">0.00</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Avg φ(m)/m</div>
                                <div class="stat-value" id="statAvgPhi">0.00</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Limit (6/π²)</div>
                                <div class="stat-value">0.6079</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Moduli Count</div>
                                <div class="stat-value" id="statModuliCount">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Min Modulus</div>
                                <div class="stat-value" id="statMinMod">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Max Modulus</div>
                                <div class="stat-value" id="statMaxMod">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Avg Points/Mod</div>
                                <div class="stat-value" id="statAvgPoints">0.00</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Prime Moduli</div>
                                <div class="stat-value" id="statPrimeCount">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Composite Moduli</div>
                                <div class="stat-value" id="statCompositeCount">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Error from 6/π²</div>
                                <div class="stat-value" id="statError">0.0000</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Convergence %</div>
                                <div class="stat-value" id="statConvergence">0.00%</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Admissible Points</div>
                                <div class="stat-value" id="statAdmissible">0</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Admissible Ratio</div>
                                <div class="stat-value" id="statAdmissibleRatio">0.00%</div>
                            </div>
                        </div>
                    </div>
                </div>
                </div>
            </div>
        </div>

        <div id="compositeProjectionTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Composite Channel Projection Corollary</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Composite Modulus (M): <span id="compModDisplay" style="color: #00ffff;">12</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">4 (minimal)</span>
                            <input type="range" id="compModSlider" min="4" max="2000" value="12" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">2000 (maximum)</span>
                        </div>
                        <div style="text-align: center; margin-top: 10px;">
                            <span style="font-size: 12px; opacity: 0.8;">60 (standard)</span>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Or enter custom value:</label>
                        <input type="number" id="compModInput" min="2" max="5000" value="12" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap: 8px; margin-bottom: 20px;">
                        <button onclick="setCompositeMod(6)" style="padding: 8px;">M = 6</button>
                        <button onclick="setCompositeMod(12)" style="padding: 8px;">M = 12</button>
                        <button onclick="setCompositeMod(30)" style="padding: 8px;">M = 30</button>
                        <button onclick="setCompositeMod(60)" style="padding: 8px;">M = 60</button>
                        <button onclick="setCompositeMod(210)" style="padding: 8px;">M = 210</button>
                        <button onclick="setCompositeMod(2310)" style="padding: 8px;">M = 2310</button>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Point Coloring Scheme:
                        </label>
                        <select id="compColorScheme" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="channel-type">By Channel Type (Cyan/Red/Gold)</option>
                            <option value="spf">By Smallest Prime Factor</option>
                            <option value="lpf">By Largest Prime Factor</option>
                            <option value="gcd-value">By GCD Value</option>
                            <option value="channel-depth">By Channel Depth (M')</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Projection Line Opacity: <span id="projOpacityDisplay">0.10</span>
                        </label>
                        <input type="range" id="projOpacitySlider" min="0.05" max="1" step="0.05" value="0.10" 
                               style="width: 100%; height: 8px;">
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Point Size: <span id="compPointSizeDisplay">6</span>
                        </label>
                        <input type="range" id="compPointSize" min="3" max="12" step="0.5" value="6" 
                               style="width: 100%; height: 8px;">
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="showChannelLabels" checked style="margin-right: 8px;">
                            Show Channel Labels (M' values)
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="showMultiplicityInfo" style="margin-right: 8px;">
                            Show Multiplicity Annotations
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="font-weight: 600; display: block; margin-bottom: 10px;">Display Mode:</label>
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                            <button id="projLinesBtn" onclick="setProjectionMode('lines')" 
                                    style="padding: 12px; background: var(--hover-bg); color: var(--hover-text);">
                                Projection Lines
                            </button>
                            <button id="ringViewBtn" onclick="setProjectionMode('ring')" 
                                    style="padding: 12px;">
                                Ring View
                            </button>
                        </div>
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="compositeCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px; cursor: crosshair;">
                    </canvas>
                    <div id="compositeTooltip" style="position: absolute; padding: 10px; background: rgba(255, 255, 255, 0.95); 
                         color: #000000; border: 1px solid #000; pointer-events: none; font-size: 11px; 
                         line-height: 1.4; opacity: 0; transition: opacity 0.2s; z-index: 1000; max-width: 250px;
                         font-family: 'Courier New', monospace;">
                    </div>
                    <div style="position: absolute; bottom: 10px; right: 10px; background: rgba(0, 0, 0, 0.7); 
                         padding: 8px 12px; border-radius: 4px; font-size: 11px; color: #ffffff;">
                        Scroll to zoom • Click to see details
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">φ(M)</div>
                        <div id="compPhi" style="font-size: 24px; font-weight: 600; color: #00ffff;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Reducible</div>
                        <div id="compReducible" style="font-size: 24px; font-weight: 600; color: #ff0064;">8</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Ratio</div>
                        <div id="compRatio" style="font-size: 24px; font-weight: 600; color: #ffc800;">66.7%</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Channels</div>
                        <div id="compChannels" style="font-size: 24px; font-weight: 600; color: #aa00ff;">5</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Prime Factors</div>
                        <div id="compPrimeFactors" style="font-size: 16px; font-weight: 600; color: #ffffff; margin-top: 8px;">2² × 3</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Divisors</div>
                        <div id="compDivisors" style="font-size: 14px; font-weight: 600; color: #ffffff; margin-top: 8px;">1,2,3,4,6,12</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Current Modulus Analysis</h3>
                    <div id="compAnalysisText" style="font-size: 14px; line-height: 1.8;">
                        <p style="margin-bottom: 12px;"><strong>M = 12 = 2² × 3</strong></p>
                        <p style="margin-bottom: 12px;">This composite modulus has <strong>4 coprime residues</strong> (φ(12) = 4) and <strong>8 reducible residues</strong>.</p>
                        <p style="margin-bottom: 12px;">The reducible residues project onto <strong>5 distinct Farey channels</strong> with denominators: 1, 2, 3, 4, 6.</p>
                        <p style="margin-bottom: 12px;"><strong>Channel multiplicities:</strong> Each channel M' receives exactly d = M/M' residues.</p>
                        <ul style="margin-left: 25px; margin-bottom: 12px;">
                            <li>Channel M'=1: 12/1 = 12 residues (all)</li>
                            <li>Channel M'=2: 12/2 = 6 residues</li>
                            <li>Channel M'=3: 12/3 = 4 residues</li>
                            <li>Channel M'=4: 12/4 = 3 residues</li>
                            <li>Channel M'=6: 12/6 = 2 residues</li>
                        </ul>
                        <p>The <strong>reducibility ratio</strong> is 66.7%, meaning approximately 2/3 of all residues mod 12 share a common factor with 12.</p>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Visualization Legend:</h3>
                    <div id="compLegend">
                        <ul style="list-style: none; padding: 0; margin: 0;">
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #00ffff; font-size: 18px;">●</span>
                                <strong style="color: #00ffff;">Cyan points</strong> = Irreducible residues (gcd = 1)
                            </li>
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #ff0064; font-size: 18px;">●</span>
                                <strong style="color: #ff0064;">Red points</strong> = Reducible residues (gcd > 1)
                            </li>
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #ffc800; font-size: 18px;">○</span>
                                <strong style="color: #ffc800;">Gold rings</strong> = Farey channels (reduction targets)
                            </li>
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #ff0064; font-size: 18px;">━</span>
                                <strong style="color: #ff0064;">Red lines</strong> = Projection paths showing r/M → r'/M'
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div style="background: rgba(255, 200, 0, 0.1); border: 2px solid #ffc800; padding: 20px; margin-bottom: 20px;">
                    <h3 style="margin-bottom: 15px; color: #ffc800;">Key Result:</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        Every composite M has reducible residues that project onto simpler Farey channels. 
                        The number projecting to each channel M' is exactly d = M/M' (channel multiplicity).
                    </p>
                </div>
                
                <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 20px;">
                    <p style="margin: 0; font-size: 13px; opacity: 0.8;">
                        <strong>Interaction:</strong> Click any point to see detailed reduction path • Scroll over canvas to zoom • Hover for quick info
                    </p>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-top: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Export Title</label>
                        <input type="text" id="compExportTitle" value="Composite Channel Projection Corollary" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compIncludeLegend" checked style="margin-right: 8px;">
                            Include Parameter Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Export Resolution</label>
                        <select id="compExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="3">2K (2100×2100)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="6">6K (4200×4200)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compIncludeColorKey" checked style="margin-right: 8px;">
                            Include Color Key Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compIncludeTimestamp" checked style="margin-right: 8px;">
                            Include Timestamp
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compIncludeStats" checked style="margin-right: 8px;">
                            Include Statistics Panel
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportCompositeImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportCompositeCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
            </div>
        </div>

        <div id="zetaTab" class="tab-content">
            <div class="theory-section">
                <h2>Nested Modular Unity & Zeta Surface</h2>
                
                <h3>The Zeta Function as a Phasor Sum:</h3>
                
                <p>
                    For complex argument s = σ + it, the Riemann zeta function can be written as:
                </p>
                
                <div class="formula">
                    ζ(s) = Σ n⁻ᵠ e⁻ⁱᵗ ˡᵒᵍ ⁿ
                </div>
                
                <p>
                    Each term n<sup>s</sup> is a <strong>rotating phasor</strong> on the complex plane with:
                </p>
                
                <div class="formula">
                    Radius: rₙ = n⁻ᵠ<br>
                    Angle: θₙ = -t log n
                </div>
                
                <h3>Modular Unity Correspondence:</h3>
                
                <p>
                    Each residue class k (mod m) corresponds to an m-th root of unity:
                </p>
                
                <div class="formula">
                    k mod m ↔ e<sup>2πik/m</sup>
                </div>
                
                <p>
                    This isomorphism connects modular arithmetic to the unit circle geometry. For each modulus m and residue k:
                </p>
                
                <div class="formula">
                    S<sub>m,k</sub>(s; N) = Σ<sub>n≡k (mod m)</sub> n⁻ˢ
                </div>
                
                <h3>The Critical Line (σ = 1/2):</h3>
                
                <p>
                    On the critical line, each contribution rotates at angular velocity ∝ log n. When modular rotations align <strong>destructively</strong>, their vector sum vanishes—precisely the condition for a nontrivial zero:
                </p>
                
                <div class="formula">
                    ζ(1/2 + iT) = 0
                </div>
                
                <h3>Nested Modular Surface:</h3>
                
                <p>
                    Stacking concentric rings for m = 1, 2, 3, ... creates a <strong>nested modular unity lattice</strong>. Each ring samples the unit circle at m equally-spaced points, and together they approximate the continuous analytic structure of ζ(s). The GCD=1 residues (primitive rotations) form the multiplicative group of units mod m.
                </p>
                
                <h3>Geometric Interpretation:</h3>
                
                <ul>
                    <li><strong>Height t:</strong> Controls angular phase of each modular shell (vertical movement on zeta surface)</li>
                    <li><strong>Real part σ:</strong> Controls radial decay (compression toward critical line)</li>
                    <li><strong>Modulus m:</strong> Discrete Fourier mode on the complex circle</li>
                    <li><strong>Primitive residues:</strong> φ(m) independent rotation channels</li>
                </ul>
                
                <div class="intro-box" style="background: rgba(255, 200, 0, 0.1); border-left: 4px solid #ffc800;">
                    <h4>💡 Key Insight:</h4>
                    <p>
                        The nested modular lattice forms a discrete analogue of the complex-analytic domain of ζ(s). By weighting each ring by n<sup>-σ</sup> and rotating by phase -t log n, we obtain a direct geometric mimic of the Riemann zeta surface.
                    </p>
                </div>
                
                <h3>Connection to the Visualization:</h3>
                
                <p>
                    When you view the nested modular rings with rotation enabled, you are seeing a <strong>discrete approximation of the zeta function's phasor structure</strong>. Each ring represents a term in the Dirichlet series, with:
                </p>
                
                <ul>
                    <li>Ring radius ∝ modular "frequency" m</li>
                    <li>Open channels (φ(m) coprime residues) = independent Fourier modes</li>
                    <li>Rotation speed = phase velocity on the critical line</li>
                    <li>Spiral patterns = constructive/destructive interference of modular terms</li>
                </ul>
                
                <div class="formula" style="background: rgba(100, 150, 255, 0.15); border: 2px solid #6496ff; margin-top: 30px;">
                    <div style="text-align: center; font-size: 16px; font-weight: 600; margin-bottom: 10px;">
                        Zeta-Modular Correspondence
                    </div>
                    <p style="text-align: center; margin: 0; padding: 10px;">
                        The nested ring structure with m = 1, 2, 3, ... and rotation by -t log m<br>
                        creates a geometric realization of ζ(1/2 + it) as a sum of rotating unit vectors,<br>
                        where zeros correspond to <strong>perfect destructive interference</strong> of the modular phasors.
                    </p>
                </div>
                
                <h3 style="margin-top: 40px;">Visualization Controls for Zeta Exploration:</h3>
                
                <div class="intro-box">
                    <p>To explore the zeta surface connection in the visualization:</p>
                    <ol>
                        <li>Set <strong>Modulus Selection</strong> to "Range" with a large sequence (e.g., 1 to 100)</li>
                        <li>Enable <strong>Per-Ring Spiral</strong> with "Logarithmic" mode to mimic -t log n rotation</li>
                        <li>Adjust <strong>Global Rotation</strong> to sweep through different t values on the critical line</li>
                        <li>Watch for <strong>alignment patterns</strong> where open channels synchronize (constructive interference) or cancel (destructive interference)</li>
                        <li>Use <strong>Connection Lines</strong> set to "Same Modulus" to see phase relationships within each ring</li>
                    </ol>
                    <p style="margin-top: 15px;">
                        The moments when the pattern appears most "organized" or "collapsed" correspond geometrically to regions where ζ(s) has significant structure — near zeros, poles, or critical points.
                    </p>
                </div>
                
                <h3>Open Questions and Research Directions:</h3>
                
                <p>
                    This geometric framework suggests several avenues for exploration:
                </p>
                
                <ul>
                    <li>Can we identify zeta zeros by finding specific rotation configurations where all open channels align destructively?</li>
                    <li>Does the Farey channel structure impose constraints on where zeros can occur?</li>
                    <li>How do prime moduli (which avoid Farey channels) contribute differently to the zeta sum than composite moduli?</li>
                    <li>Can the nested modular lattice provide a finite-dimensional approximation for numerical zero-finding algorithms?</li>
                </ul>
                
                <p style="margin-top: 30px; font-style: italic;">
                    By connecting modular arithmetic, Farey sequences, and the Riemann zeta function through this unified geometric visualization, we gain new intuition for one of mathematics' deepest mysteries: the distribution of prime numbers and the location of zeta zeros on the critical line.
                </p>
            </div>
        </div>

        <div id="understandingTab" class="tab-content">
                                <div class="theory-section">
                <h2>Modular Rings and the Residue System</h2>
                
                <h3>The Fundamental Concept</h3>
                <p>
                    Imagine the integers arranged not as a line, but as circles—infinite families of circles, each one capturing a different "rhythm" of counting. This is <strong>modular arithmetic</strong>, the mathematics of remainders, and it was Euler who first recognized its deep geometric character.
                </p>
                
                <p>
                    When we count modulo <em>m</em>, we're asking: "What's left over after dividing by <em>m</em>?" The possible remainders—called <strong>residues</strong>—are the integers {0, 1, 2, ..., m-1}. These <em>m</em> residues form what mathematicians call ℤ/mℤ (pronounced "Z mod m"), and Euler showed us how to think of them as points equally spaced around a circle.
                </p>

                <div class="example-box">
                    <strong>Example: The Clock (Modulo 12)</strong><br>
                    When we read a 12-hour clock, we're doing arithmetic modulo 12. After 12 o'clock comes 1 o'clock—the remainder when 13 is divided by 12. The 12 hours form a circle, and this circular structure is fundamental to modular arithmetic.
                    <br><br>
                    In our visualization, modulus <em>m</em> = 12 appears as a ring with 12 equally-spaced points, one for each hour: {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11}.
                </div>

                <h3>Why Nested Rings?</h3>
                <p>
                    The revolutionary insight is to display <em>multiple moduli simultaneously</em> as concentric rings. Each ring represents a different modulus, with the innermost circle being <em>m</em> = 1 (just one point—the origin) and outer rings representing larger moduli.
                </p>
                
                <p>
                    This nested structure reveals <strong>modular containment</strong>: larger moduli contain and extend smaller ones. When <em>d</em> divides <em>m</em>, the ring of modulus <em>d</em> embeds naturally inside the ring of modulus <em>m</em>. The visualization makes this abstract algebraic relationship visible as geometric nesting.
                </p>

                <h2>The Two Types of Channels: Open and Closed</h2>
                
                <p>
                    Euler's greatest contribution to this theory was recognizing that residues fall into two fundamentally different categories, distinguished by their relationship to the modulus through the <strong>greatest common divisor (GCD)</strong>.
                </p>

                <h3>Open Channels (Coprime Residues)</h3>
                <p>
                    A residue <em>r</em> in modulus <em>m</em> is an <strong>open channel</strong> if gcd(<em>r</em>, <em>m</em>) = 1. This means <em>r</em> and <em>m</em> share no common factors—they are <strong>coprime</strong> or <strong>relatively prime</strong>.
                </p>
                
                <div class="formula">
                    <div class="formula-title">Mathematical Definition</div>
                    r is an OPEN channel in ℤ/mℤ ⟺ gcd(r, m) = 1
                    <br><br>
                    These residues have <strong>multiplicative inverses</strong> modulo m.
                    <br>
                    They form a group under multiplication: (ℤ/mℤ)×
                </div>

                <p>
                    <strong>Why "open"?</strong> These residues represent "pathways" that allow information to flow freely through the modular system. In number theory, they're the residues where primes can live—every prime <em>p</em> greater than <em>m</em> must occupy an open channel when reduced modulo <em>m</em>.
                </p>

                <div class="example-box">
                    <strong>Example: Modulo 12</strong><br>
                    Open channels in ℤ/12ℤ: {1, 5, 7, 11}<br>
                    These are the residues coprime to 12.<br><br>
                    • gcd(1, 12) = 1 ✓<br>
                    • gcd(5, 12) = 1 ✓<br>
                    • gcd(7, 12) = 1 ✓<br>
                    • gcd(11, 12) = 1 ✓<br><br>
                    Count: φ(12) = 4 (Euler's totient function)
                </div>

                <h3>Closed Channels (Non-Coprime Residues)</h3>
                <p>
                    A residue <em>r</em> is a <strong>closed channel</strong> if gcd(<em>r</em>, <em>m</em>) > 1. These residues share a common factor with the modulus—they are <strong>divisible by some prime that also divides m</strong>.
                </p>

                <div class="formula">
                    <div class="formula-title">Mathematical Definition</div>
                    r is a CLOSED channel in ℤ/mℤ ⟺ gcd(r, m) > 1
                    <br><br>
                    These residues do NOT have multiplicative inverses modulo m.
                    <br>
                    They are "zero divisors" or non-units in the ring ℤ/mℤ.
                </div>

                <p>
                    <strong>Why "closed"?</strong> These residues are blocked—they cannot represent prime numbers (except for the primes dividing <em>m</em> itself). They form the "sieve" that filters out composites in prime-hunting algorithms.
                </p>

                <div class="example-box">
                    <strong>Example: Modulo 12</strong><br>
                    Closed channels in ℤ/12ℤ: {0, 2, 3, 4, 6, 8, 9, 10}<br>
                    These share a factor of 2 or 3 with 12.<br><br>
                    • gcd(0, 12) = 12 (shares all factors)<br>
                    • gcd(2, 12) = 2 (shares factor 2)<br>
                    • gcd(3, 12) = 3 (shares factor 3)<br>
                    • gcd(4, 12) = 4 (shares factor 2)<br>
                    • gcd(6, 12) = 6 (shares factors 2 and 3)<br><br>
                    Count: 12 - φ(12) = 12 - 4 = 8
                </div>

                <h2>Euler's Totient Function φ(m)</h2>
                
                <p>
                    One of Euler's most famous contributions to number theory is the <strong>totient function</strong> φ(<em>m</em>), which counts the number of open channels in ℤ/mℤ—the integers between 1 and <em>m</em> that are coprime to <em>m</em>.
                </p>

                <div class="formula">
                    <div class="formula-title">Euler's Totient Function</div>
                    φ(m) = |{r ∈ {1, 2, ..., m} : gcd(r, m) = 1}|
                    <br><br>
                    <strong>For prime p:</strong> φ(p) = p - 1 (all non-zero residues are open)
                    <br>
                    <strong>For prime power p^k:</strong> φ(p^k) = p^k - p^(k-1) = p^(k-1)(p - 1)
                    <br>
                    <strong>Multiplicative property:</strong> If gcd(m,n) = 1, then φ(mn) = φ(m)φ(n)
                </div>

                <p>
                    The totient function measures the "density" of open channels. As we visualize larger and larger moduli, the ratio φ(<em>m</em>)/<em>m</em> converges to a famous limit:
                </p>

                <div class="formula">
                    <div class="formula-title">The Asymptotic Density of Coprime Integers</div>
                    lim (average of φ(m)/m over all m) = 6/π² ≈ 0.6079...
                    <br><br>
                    This means that approximately <strong>60.79% of all residue positions are open channels</strong> when averaged across all moduli.
                    <br><br>
                    This is intimately connected to the probability that two randomly chosen integers are coprime!
                </div>

                <h2>Farey Sequences and Angular Coordinates</h2>
                
                <p>
                    Each residue <em>r</em> in modulus <em>m</em> naturally corresponds to a <strong>Farey fraction</strong> <em>r</em>/<em>m</em>, a rational number between 0 and 1. Euler showed that these fractions, when arranged in order, exhibit beautiful patterns.
                </p>

                <p>
                    In our visualization, we map each fraction to an angle: θ = -2π<em>r</em>/<em>m</em> (using negative for clockwise orientation). This transforms the modular arithmetic ring into a geometric circle, with residues as evenly-spaced points.
                </p>

                <div class="example-box">
                    <strong>Example: Modulo 8 → Angular Positions</strong><br>
                    • r = 0 → 0/8 → θ = 0° (right/east)<br>
                    • r = 1 → 1/8 → θ = -45° (clockwise)<br>
                    • r = 2 → 2/8 = 1/4 → θ = -90° (down/south)<br>
                    • r = 3 → 3/8 → θ = -135°<br>
                    • r = 4 → 4/8 = 1/2 → θ = -180° (left/west)<br>
                    • r = 5 → 5/8 → θ = -225°<br>
                    • r = 6 → 6/8 = 3/4 → θ = -270° (up/north)<br>
                    • r = 7 → 7/8 → θ = -315°<br>
                </div>

                <h2>Prime Constellations and Gap Analysis</h2>
                
                <h3>The Sieve Structure</h3>
                <p>
                    One of the most profound applications of this visualization is understanding <strong>why prime numbers appear in specific patterns</strong>. The ancient Greeks knew about the Sieve of Eratosthenes, but Euler revealed the deeper geometric structure.
                </p>

                <p>
                    When we look for <strong>twin primes</strong> (primes separated by 2, like 11 and 13, or 17 and 19), we're asking: which residue positions allow both <em>r</em> and <em>r</em>+2 to be open channels?
                </p>

                <div class="formula">
                    <div class="formula-title">Gap Admissibility</div>
                    A residue r in modulus m is <strong>gap-g admissible</strong> if:
                    <br>
                    1. gcd(r, m) = 1 (r is an open channel)
                    <br>
                    2. gcd((r + g) mod m, m) = 1 (r+g is also an open channel)
                    <br><br>
                    For twin primes (g=2), we need consecutive open channels spaced 2 apart.
                    <br>
                    For sexy primes (g=6), we need open channels spaced 6 apart.
                </div>

                <div class="example-box">
                    <strong>Example: Twin Primes in Modulo 30</strong><br>
                    Open channels mod 30: {1, 7, 11, 13, 17, 19, 23, 29}<br><br>
                    Gap-2 admissible positions:<br>
                    • r = 11: 11+2 = 13 ✓ (both open)<br>
                    • r = 17: 17+2 = 19 ✓ (both open)<br>
                    • r = 29: 29+2 ≡ 1 mod 30 ✓ (both open)<br><br>
                    Only 3 out of 8 open channels support twin prime patterns!<br>
                    This is why twin primes become increasingly rare.
                </div>

                <p>
                    The visualization reveals this structure through <strong>purple highlighting</strong> and <strong>colored connection lines</strong>. When you enable gap analysis with g = 2, 4, 6, etc., you see exactly which residue positions remain viable for prime constellations after the modular sieve has done its filtering.
                </p>

                <h2>The M₃₀ Sequence: A Special Case</h2>
                
                <p>
                    The primorial-based sequence <strong>M<sub>n</sub> = 30 × 2<sup>n</sup></strong> has special significance in prime number theory because 30 = 2 × 3 × 5 is the product of the first three primes.
                </p>

                <div class="formula">
                    <div class="formula-title">Why 30 Is Special</div>
                    30 is the smallest number that "sieves out" all primes up to 5:
                    <br><br>
                    • Multiples of 2 (even numbers)
                    <br>
                    • Multiples of 3
                    <br>
                    • Multiples of 5
                    <br><br>
                    All primes > 5 must lie in one of φ(30) = 8 residue classes: {1, 7, 11, 13, 17, 19, 23, 29}
                    <br><br>
                    The sequence 30, 60, 120, 240, 480, 960 creates increasingly fine-grained sieves while preserving this structure.
                </div>

                <h2>Rotation and Spiral Features</h2>
                
                <h3>Global Rotation</h3>
                <p>
                    Rotates all rings together as a rigid body. This lets you explore the visualization from different angular perspectives, revealing symmetries that might not be obvious from the default orientation.
                </p>

                <h3>Individual Modulus Rotation</h3>
                <p>
                    Each ring rotates independently at its own rate. This creates dynamic, kaleidoscopic patterns and reveals how different modular rhythms interact—a visual representation of the <strong>Chinese Remainder Theorem</strong> in action.
                </p>

                <h3>Per-Ring Spiral</h3>
                <p>
                    Perhaps the most beautiful feature: each successive ring rotates by an additional angular increment, creating spiral or helical patterns. The four mathematical modes (Linear, Fibonacci, Logarithmic, Sine Wave) correspond to different growth functions:
                </p>

                <ul>
                    <li><strong>Linear:</strong> Uniform spiral like a phonograph record</li>
                    <li><strong>Fibonacci (Golden Spiral):</strong> Appears in nautilus shells and sunflower seed patterns</li>
                    <li><strong>Logarithmic:</strong> Similar to galaxy spiral arms</li>
                    <li><strong>Sine Wave:</strong> Oscillating, DNA-helix-like structure</li>
                </ul>

                <p>
                    These rotations don't change the mathematics—they're purely visual transformations—but they reveal different aspects of the underlying modular structure, much like how rotating a crystal reveals different facets.
                </p>

                <h2>Connection Lines: Revealing Structure</h2>
                
                <p>
                    The connection lines trace relationships between residues across different moduli:
                </p>

                <ul>
                    <li><strong>r to r (Next Modulus):</strong> Shows how each residue "lifts" to the next modulus level</li>
                    <li><strong>Binary Lift:</strong> Reveals the doubling structure inherent in powers of 2</li>
                    <li><strong>Gap connections:</strong> Traces prime constellation patterns through multiple moduli simultaneously</li>
                </ul>

                <p>
                    When you see open channels connected by colored lines, you're seeing the <strong>admissible patterns</strong>—the geometric skeleton that supports prime number constellations.
                </p>

                <h2>Why This Matters: Applications</h2>
                
                <h3>1. Cryptography</h3>
                <p>
                    Modern encryption (RSA, elliptic curve cryptography) relies fundamentally on modular arithmetic and Euler's totient function. The open channels are where cryptographic keys live.
                </p>

                <h3>2. Prime Number Theory</h3>
                <p>
                    Understanding prime distribution requires understanding the sieve structure. This visualization makes concrete the abstract ideas behind the Hardy-Littlewood conjectures on prime k-tuples.
                </p>

                <h3>3. The Riemann Hypothesis</h3>
                <p>
                    The distribution of primes is intimately connected to the behavior of the Riemann zeta function. The average density φ(<em>m</em>)/<em>m</em> → 6/π² is one manifestation of this deep connection between number theory and analysis.
                </p>

                <h3>4. Computational Number Theory</h3>
                <p>
                    Efficient algorithms for primality testing, factorization, and discrete logarithms all exploit the structure of modular arithmetic rings—the very structure this tool visualizes.
                </p>

                <h2>Historical Context: Euler's Legacy</h2>
                
                <p>
                    Leonhard Euler (1707-1783) was one of the most prolific mathematicians in history. His work on modular arithmetic, particularly:
                </p>

                <ul>
                    <li>The totient function φ(<em>m</em>)</li>
                    <li>Euler's theorem: <em>a</em><sup>φ(m)</sup> ≡ 1 (mod <em>m</em>) when gcd(<em>a</em>,<em>m</em>)=1</li>
                    <li>The product formula for φ(<em>m</em>)</li>
                    <li>The asymptotic density of coprime integers</li>
                </ul>

                <p>
                    ...laid the foundation for modern number theory. What you're seeing in this visualization is Euler's insight made visible: that numbers have not just algebraic structure, but <em>geometric</em> structure, and that this geometry reveals deep truths about primes, divisibility, and the architecture of mathematics itself.
                </p>

                <div class="formula" style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin: 30px 0;">
                    <div style="text-align: center; font-size: 18px; font-weight: 600; margin-bottom: 15px;">
                        Euler's Vision
                    </div>
                    <p style="font-style: italic; text-align: center; margin: 0;">
                        "The properties of numbers known today have been mostly discovered by observation, and discovered long before their truth has been confirmed by rigid demonstrations. There are even many properties of numbers with which we are well acquainted, but which we are not yet able to prove; only observations have led us to their knowledge."
                    </p>
                    <p style="text-align: center; margin-top: 10px; font-size: 14px;">
                        — Leonhard Euler, <em>Opera Omnia</em>
                    </p>
                </div>

                <p>
                    This tool continues Euler's tradition: through careful observation of mathematical structure—now aided by modern computation and visualization—we discover patterns that inspire rigorous proofs and deepen our understanding of number theory's infinite mysteries.
                </p>

                <h2>Getting Started: A Guided Tour</h2>
                
                <ol>
                    <li><strong>Start simple:</strong> Set moduli to "Range" from 1 to 12. Click Update. You'll see 12 concentric rings with their open (green) and closed (red) channels.</li>
                    
                    <li><strong>Explore the totient:</strong> Notice that ring 12 has only 4 open channels (at positions 1, 5, 7, 11). This is φ(12) = 4.</li>
                    
                    <li><strong>Compare primes:</strong> Look at ring 11 (a prime). It has 10 open channels—all positions except 0. This is φ(11) = 10 = 11 - 1.</li>
                    
                    <li><strong>Enable gap analysis:</strong> Choose "Twin Primes (2)" and enable "Show Gap Connection Lines". The purple points are admissible—they can support twin primes.</li>
                    
                    <li><strong>Try the M₃₀ sequence:</strong> Click the preset buttons: n=0, n=1, n=2, etc. Watch how the sieve structure scales.</li>
                    
                    <li><strong>Add spiral rotation:</strong> Set "Per-Ring Spiral" to 15° and choose "Fibonacci (Golden Spiral)". Press Play. Watch the structure unfold in a golden spiral—the same pattern seen in nature.</li>
                    
                    <li><strong>Track a residue:</strong> Enable "Residue Tracker", choose "Slider" mode, and drag the slider. Watch how a single residue appears across all moduli—see where it's open vs closed.</li>
                </ol>

                <p style="margin-top: 30px; font-size: 16px; font-weight: 600;">
                    You're now exploring Euler's vision of the integers—a vision that has guided number theory for over 250 years and continues to inspire new discoveries today.
                </p>

            </div>
        </div>

    <script>
        const canvas = document.getElementById('mainCanvas');
        const ctx = canvas.getContext('2d');
        const svg = document.getElementById('mainSVG');
        const svgGroup = document.getElementById('svgMainGroup');
        const tooltip = document.getElementById('tooltip');
        
        let currentRenderer = 'canvas2d'; // 'canvas2d', 'webgl', or 'svg'
        let webglRenderer = null;
        
        let pointsData = [];
        let transform = { x: 0, y: 0, scale: 1 };
        let isDragging = false;
        let lastMouseX = 0;
        let lastMouseY = 0;
        let globalRotation = 0;
        let modRotations = {};
        let animationId = null;
        let currentTheme = 'light';
        let isComputing = false;
        let progressiveRenderBatch = 0;
        const PROGRESSIVE_BATCH_SIZE = 1000;
        const COMPUTE_CHUNK_SIZE = 2000; // Process this many residues before yielding (increased from 500)

        // WebGL Renderer Class
        class WebGLRenderer {
            constructor(canvas) {
                this.canvas = canvas;
                this.gl = canvas.getContext('webgl') || canvas.getContext('experimental-webgl');
                
                if (!this.gl) {
                    alert('WebGL not supported in your browser. Falling back to Canvas 2D.');
                    return null;
                }
                
                this.setupWebGL();
            }
            
            setupWebGL() {
                const gl = this.gl;
                
                // Vertex shader
                const vsSource = `
                    attribute vec2 a_position;
                    attribute vec4 a_color;
                    attribute float a_size;
                    
                    uniform vec2 u_resolution;
                    uniform vec2 u_translation;
                    uniform float u_scale;
                    uniform float u_rotation;
                    
                    varying vec4 v_color;
                    
                    void main() {
                        vec2 rotated = vec2(
                            a_position.x * cos(u_rotation) - a_position.y * sin(u_rotation),
                            a_position.x * sin(u_rotation) + a_position.y * cos(u_rotation)
                        );
                        
                        vec2 scaled = rotated * u_scale;
                        vec2 translated = scaled + u_translation;
                        vec2 clipSpace = (translated / u_resolution) * 2.0 - 1.0;
                        
                        gl_Position = vec4(clipSpace * vec2(1, -1), 0, 1);
                        gl_PointSize = a_size * u_scale;
                        v_color = a_color;
                    }
                `;
                
                // Fragment shader
                const fsSource = `
                    precision mediump float;
                    varying vec4 v_color;
                    
                    void main() {
                        vec2 coord = gl_PointCoord - vec2(0.5);
                        if (length(coord) > 0.5) discard;
                        gl_FragColor = v_color;
                    }
                `;
                
                this.program = this.createProgram(vsSource, fsSource);
                this.locations = {
                    position: gl.getAttribLocation(this.program, 'a_position'),
                    color: gl.getAttribLocation(this.program, 'a_color'),
                    size: gl.getAttribLocation(this.program, 'a_size'),
                    resolution: gl.getUniformLocation(this.program, 'u_resolution'),
                    translation: gl.getUniformLocation(this.program, 'u_translation'),
                    scale: gl.getUniformLocation(this.program, 'u_scale'),
                    rotation: gl.getUniformLocation(this.program, 'u_rotation')
                };
                
                this.buffers = {
                    position: gl.createBuffer(),
                    color: gl.createBuffer(),
                    size: gl.createBuffer()
                };
            }
            
            createShader(type, source) {
                const gl = this.gl;
                const shader = gl.createShader(type);
                gl.shaderSource(shader, source);
                gl.compileShader(shader);
                
                if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) {
                    console.error('Shader compile error:', gl.getShaderInfoLog(shader));
                    gl.deleteShader(shader);
                    return null;
                }
                return shader;
            }
            
            createProgram(vsSource, fsSource) {
                const gl = this.gl;
                const vertexShader = this.createShader(gl.VERTEX_SHADER, vsSource);
                const fragmentShader = this.createShader(gl.FRAGMENT_SHADER, fsSource);
                
                const program = gl.createProgram();
                gl.attachShader(program, vertexShader);
                gl.attachShader(program, fragmentShader);
                gl.linkProgram(program);
                
                if (!gl.getProgramParameter(program, gl.LINK_STATUS)) {
                    console.error('Program link error:', gl.getProgramInfoLog(program));
                    return null;
                }
                return program;
            }
            
            render(pointsData, transform, globalRotation, modRotations, settings) {
                const gl = this.gl;
                
                gl.viewport(0, 0, gl.canvas.width, gl.canvas.height);
                gl.clearColor(0, 0, 0, 1);
                gl.clear(gl.COLOR_BUFFER_BIT);
                
                gl.enable(gl.BLEND);
                gl.blendFunc(gl.SRC_ALPHA, gl.ONE_MINUS_SRC_ALPHA);
                
                gl.useProgram(this.program);
                
                // Prepare data arrays
                const positions = [];
                const colors = [];
                const sizes = [];
                
                pointsData.forEach(point => {
                    if (!settings.showOpen && point.isOpen) return;
                    if (!settings.showClosed && !point.isOpen) return;
                    
                    const modRot = modRotations[point.m] || 0;
                    const totalAngle = point.angle + (modRot * Math.PI / 180);
                    const r = settings.getRadius(point.m);
                    const x = r * Math.cos(totalAngle);
                    const y = r * Math.sin(totalAngle);
                    
                    positions.push(x, y);
                    
                    const color = this.hexToRgb(settings.getColorForPoint(point));
                    const opacity = point.isOpen ? 0.8 : 0.3;
                    colors.push(color.r, color.g, color.b, opacity);
                    
                    let size = settings.pointSize;
                    if (settings.highlightAdmissible && point.isAdmissible) {
                        size *= 1.2;
                    }
                    sizes.push(size);
                });
                
                // Upload data to GPU
                gl.bindBuffer(gl.ARRAY_BUFFER, this.buffers.position);
                gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(positions), gl.STATIC_DRAW);
                gl.enableVertexAttribArray(this.locations.position);
                gl.vertexAttribPointer(this.locations.position, 2, gl.FLOAT, false, 0, 0);
                
                gl.bindBuffer(gl.ARRAY_BUFFER, this.buffers.color);
                gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(colors), gl.STATIC_DRAW);
                gl.enableVertexAttribArray(this.locations.color);
                gl.vertexAttribPointer(this.locations.color, 4, gl.FLOAT, false, 0, 0);
                
                gl.bindBuffer(gl.ARRAY_BUFFER, this.buffers.size);
                gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(sizes), gl.STATIC_DRAW);
                gl.enableVertexAttribArray(this.locations.size);
                gl.vertexAttribPointer(this.locations.size, 1, gl.FLOAT, false, 0, 0);
                
                // Set uniforms
                gl.uniform2f(this.locations.resolution, gl.canvas.width, gl.canvas.height);
                gl.uniform2f(this.locations.translation, 
                    gl.canvas.width / 2 + transform.x, 
                    gl.canvas.height / 2 + transform.y
                );
                gl.uniform1f(this.locations.scale, transform.scale);
                gl.uniform1f(this.locations.rotation, globalRotation * Math.PI / 180);
                
                // Draw points
                gl.drawArrays(gl.POINTS, 0, positions.length / 2);
            }
            
            hexToRgb(hex) {
                const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
                return result ? {
                    r: parseInt(result[1], 16) / 255,
                    g: parseInt(result[2], 16) / 255,
                    b: parseInt(result[3], 16) / 255
                } : { r: 0, g: 1, b: 0 };
            }
        }

        function switchRenderingMode() {
            const mode = document.getElementById('renderingMode').value;
            currentRenderer = mode;
            
            if (mode === 'canvas2d') {
                canvas.style.display = 'block';
                svg.style.display = 'none';
                drawVisualization();
            } else if (mode === 'webgl') {
                canvas.style.display = 'block';
                svg.style.display = 'none';
                
                if (!webglRenderer) {
                    webglRenderer = new WebGLRenderer(canvas);
                }
                
                if (webglRenderer && webglRenderer.gl) {
                    drawVisualizationWebGL();
                } else {
                    alert('WebGL initialization failed. Falling back to Canvas 2D.');
                    document.getElementById('renderingMode').value = 'canvas2d';
                    currentRenderer = 'canvas2d';
                    drawVisualization();
                }
            } else if (mode === 'svg') {
                canvas.style.display = 'none';
                svg.style.display = 'block';
                drawVisualizationSVG();
            }
        }

        function drawVisualizationWebGL() {
            if (!webglRenderer || !webglRenderer.gl) return;
            
            const displayMode = document.getElementById('displayMode').value;
            const showOpen = document.getElementById('showOpen').checked;
            const showClosed = document.getElementById('showClosed').checked;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const highlightAdmissible = document.getElementById('highlightAdmissible').checked;
            
            const width = canvas.width;
            const height = canvas.height;
            const maxRadius = Math.min(width, height) * 0.4;
            
            function getRadius(m) {
                const invertOrder = document.getElementById('invertModOrder').checked;
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
                
                if (displayMode === 'unit') {
                    return maxRadius;
                }
                
                if (invertOrder) {
                    const maxMod = Math.max(...moduli);
                    const minMod = Math.min(...moduli);
                    const inverted = maxMod - (m - minMod);
                    return inverted * (maxRadius / Math.max(...moduli));
                }
                
                return m * (maxRadius / Math.max(...moduli));
            }
            
            const settings = {
                showOpen,
                showClosed,
                pointSize,
                highlightAdmissible,
                getRadius,
                getColorForPoint: (point) => getColorForPoint(point, point.isOpen)
            };
            
            webglRenderer.render(pointsData, transform, globalRotation, modRotations, settings);
        }

        function drawVisualizationSVG() {
            const width = parseInt(svg.getAttribute('width'));
            const height = parseInt(svg.getAttribute('height'));
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;
            
            // Clear SVG
            svgGroup.innerHTML = '';
            
            const displayMode = document.getElementById('displayMode').value;
            const showOpen = document.getElementById('showOpen').checked;
            const showClosed = document.getElementById('showClosed').checked;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const highlightAdmissible = document.getElementById('highlightAdmissible').checked;
            const enableCulling = document.getElementById('enableCulling').checked;
            const enableLOD = document.getElementById('enableLOD').checked;
            const theoremMode = document.getElementById('theoremMode').value;
            
            function getRadius(m) {
                const invertOrder = document.getElementById('invertModOrder').checked;
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
                
                if (displayMode === 'unit') return maxRadius;
                
                if (invertOrder) {
                    const maxMod = Math.max(...moduli);
                    const minMod = Math.min(...moduli);
                    const inverted = maxMod - (m - minMod);
                    return inverted * (maxRadius / Math.max(...moduli));
                }
                
                return m * (maxRadius / Math.max(...moduli));
            }
            
            // Apply transform to group
            const transformStr = `translate(${centerX + transform.x}, ${centerY + transform.y}) scale(${transform.scale}) rotate(${globalRotation})`;
            svgGroup.setAttribute('transform', transformStr);
            
            // Level of detail: reduce point count when zoomed out
            let skipFactor = 1;
            if (enableLOD && transform.scale < 0.5) {
                skipFactor = Math.ceil(1 / transform.scale);
            }
            
            // View culling bounds
            const viewBounds = enableCulling ? {
                minX: -centerX / transform.scale - transform.x,
                maxX: (width - centerX) / transform.scale - transform.x,
                minY: -centerY / transform.scale - transform.y,
                maxY: (height - centerY) / transform.scale - transform.y
            } : null;
            
            // Draw ring lines if needed
            if (displayMode === 'rings') {
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
                moduli.forEach(m => {
                    const circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                    circle.setAttribute('cx', 0);
                    circle.setAttribute('cy', 0);
                    circle.setAttribute('r', getRadius(m));
                    circle.setAttribute('fill', 'none');
                    circle.setAttribute('stroke', 'rgba(255, 255, 255, 0.2)');
                    circle.setAttribute('stroke-width', 1 / transform.scale);
                    svgGroup.appendChild(circle);
                });
            }
            
            // Draw points
            pointsData.forEach((point, idx) => {
                if (skipFactor > 1 && idx % skipFactor !== 0) return;
                if (!showOpen && point.isOpen) return;
                if (!showClosed && !point.isOpen) return;
                
                const modRot = modRotations[point.m] || 0;
                const totalAngle = point.angle + (modRot * Math.PI / 180);
                const r = getRadius(point.m);
                const x = r * Math.cos(totalAngle);
                const y = r * Math.sin(totalAngle);
                
                // View culling
                if (viewBounds) {
                    if (x < viewBounds.minX || x > viewBounds.maxX || 
                        y < viewBounds.minY || y > viewBounds.maxY) {
                        return;
                    }
                }
                
                let radius = pointSize;
                let color = getColorForPoint(point, point.isOpen);
                let opacity = point.isOpen ? 0.8 : 0.3;
                
                // Apply theorem mode highlighting
                if (theoremMode !== 'none') {
                    const isPrimeModulus = isPrime(point.m);
                    const isFareyPoint = point.gcd > 1;
                    const highlightPrime = document.getElementById('highlightPrimeOrbits').checked;
                    const highlightComposite = document.getElementById('highlightCompositeProjection').checked;
                    const highlightFarey = document.getElementById('highlightFareyChannels').checked;
                    
                    if ((theoremMode === 'prime-avoidance' || theoremMode === 'both') && 
                        highlightPrime && isPrimeModulus && point.isOpen) {
                        color = '#00ffff';
                        opacity = 0.9;
                    }
                    
                    if ((theoremMode === 'composite-projection' || theoremMode === 'both') && 
                        highlightComposite && !isPrimeModulus && isFareyPoint) {
                        color = '#ff0064';
                        opacity = 0.85;
                    }
                    
                    if (highlightFarey && isFareyPoint) {
                        color = '#ffc800';
                        opacity = 0.7;
                    }
                }
                
            // Apply theorem mode highlighting if enabled
            const theoremMode = document.getElementById('theoremMode').value;
            if (theoremMode !== 'none') {
                const highlightFarey = document.getElementById('highlightFareyChannels').checked;
                const highlightPrime = document.getElementById('highlightPrimeOrbits').checked;
                const highlightComposite = document.getElementById('highlightCompositeProjection').checked;
                
                // Check if this modulus is prime
                const isPrimeModulus = isPrime(point.m);
                
                // Farey channels: points that are reducible (can project to simpler fractions)
                const isFareyPoint = point.gcd > 1;
                
                if (theoremMode === 'prime-avoidance' || theoremMode === 'both') {
                    // Highlight prime moduli (cyan) - they avoid Farey channels
                    if (highlightPrime && isPrimeModulus && isOpen) {
                        color = '#00ffff';
                        opacity = 0.9;
                    }
                    
                    // Gold for Farey channel targets
                    if (highlightFarey && isFareyPoint) {
                        color = '#ffc800';
                        opacity = 0.7;
                    }
                }
                
                if (theoremMode === 'composite-projection' || theoremMode === 'both') {
                    // Highlight composite projections onto channels (red)
                    if (highlightComposite && !isPrimeModulus && isFareyPoint) {
                        color = '#ff0064';
                        opacity = 0.85;
                    }
                }
                
                // If showing interstitial regions, dim non-highlighted points
                const showInterstitial = document.getElementById('showInterstitialRegions').checked;
                if (showInterstitial && !isPrimeModulus && isOpen && !isFareyPoint) {
                    color = '#666666';
                    opacity = 0.4;
                }
            }

                if (highlightAdmissible && point.isAdmissible) {
                    radius = pointSize * 1.2;
                    color = '#aa00ff';
                    opacity = 0.9;
                }
                
                const circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                circle.setAttribute('cx', x);
                circle.setAttribute('cy', y);
                circle.setAttribute('r', radius);
                circle.setAttribute('fill', color);
                circle.setAttribute('opacity', opacity);
                circle.setAttribute('data-m', point.m);
                circle.setAttribute('data-r', point.r);
                circle.setAttribute('data-gcd', point.gcd);
                circle.setAttribute('data-open', point.isOpen);
                
                // Add click handler
                circle.addEventListener('click', (e) => {
                    e.stopPropagation();
                    alert(`Point Details:\n\nModulus m = ${point.m}\nResidue r = ${point.r}\ngcd(${point.r}, ${point.m}) = ${point.gcd}\nChannel: ${point.isOpen ? 'OPEN' : 'CLOSED'}\nφ(${point.m}) = ${point.phiM}\nAngle: ${(point.angle * 180 / Math.PI).toFixed(2)}°${point.isAdmissible ? '\n\nGAP ADMISSIBLE' : ''}`);
                });
                
                // Hover tooltip
                circle.addEventListener('mouseenter', (e) => {
                    tooltip.style.opacity = '1';
                    tooltip.style.left = (e.pageX + 15) + 'px';
                    tooltip.style.top = (e.pageY + 15) + 'px';
                    tooltip.innerHTML = `
                        <strong>m = ${point.m}, r = ${point.r}</strong><br>
                        gcd(${point.r}, ${point.m}) = ${point.gcd}<br>
                        Channel: ${point.isOpen ? 'OPEN' : 'CLOSED'}<br>
                        φ(${point.m}) = ${point.phiM}<br>
                        Angle: ${(point.angle * 180 / Math.PI).toFixed(2)}°
                        ${point.isAdmissible ? '<br><strong>GAP ADMISSIBLE</strong>' : ''}
                    `;
                });
                
                circle.addEventListener('mouseleave', () => {
                    tooltip.style.opacity = '0';
                });
                
                svgGroup.appendChild(circle);
            });
            
            // Draw center dot
            const centerDot = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
            centerDot.setAttribute('cx', 0);
            centerDot.setAttribute('cy', 0);
            centerDot.setAttribute('r', 3);
            centerDot.setAttribute('fill', '#ffffff');
            svgGroup.appendChild(centerDot);
        }

        // Progressive computation without Web Worker
        async function computePointsProgressive(modMin, modMax, modStep, gaps, angularMapping) {
            pointsData = [];
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;
            let processedCount = 0;

            for (let m = modMin; m <= modMax; m += modStep) {
                if (!modRotations[m]) modRotations[m] = 0;
                
                const phiM = phi(m);
                sumPhiOverM += phiM / m;
                countModuli++;

                for (let r = 0; r < m; r++) {
                    const g = gcd(r, m);
                    const isOpen = g === 1;
                    
                    if (isOpen) totalOpen++;
                    else totalClosed++;

                    let admissibleGaps = [];
                    if (isOpen && gaps.length > 0) {
                        gaps.forEach(gap => {
                            const rPlusG = (r + gap) % m;
                            if (gcd(rPlusG, m) === 1) {
                                admissibleGaps.push(gap);
                            }
                        });
                    }

                    let angle;
                    switch(angularMapping) {
                        case 'standard':
                            angle = (2 * Math.PI * r) / m;
                            break;
                        case 'half':
                            angle = (Math.PI * r) / m;
                            break;
                        case 'inverted':
                            angle = (2 * Math.PI * (m - r)) / m;
                            break;
                        case 'negative':
                            angle = -(2 * Math.PI * r) / m;
                            break;
                        default:
                            angle = (2 * Math.PI * r) / m;
                    }

                    pointsData.push({
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        phiM: phiM,
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps
                    });

                    processedCount++;

                    // Yield to UI every COMPUTE_CHUNK_SIZE items
                    if (processedCount % COMPUTE_CHUNK_SIZE === 0) {
                        updateProgressDisplay(processedCount, m, modMax);
                        // Only yield for very large datasets
                        if (processedCount > 50000) {
                            await new Promise(resolve => setTimeout(resolve, 0));
                        }
                    }
                }
            }

            const avgPhiOverM = countModuli > 0 ? sumPhiOverM / countModuli : 0;
            const openRatio = (totalOpen + totalClosed) > 0 ? totalOpen / (totalOpen + totalClosed) : 0;
            
            // Additional statistics
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const primeModuli = moduli.filter(m => isPrime(m)).length;
            const compositeModuli = moduli.length - primeModuli;
            const avgPointsPerMod = moduli.length > 0 ? pointsData.length / moduli.length : 0;
            const admissibleCount = pointsData.filter(p => p.isAdmissible).length;
            const admissibleRatio = totalOpen > 0 ? (admissibleCount / totalOpen) * 100 : 0;
            const theoretical = 6 / (Math.PI * Math.PI);
            const error = Math.abs(avgPhiOverM - theoretical);
            const convergence = theoretical > 0 ? (1 - error / theoretical) * 100 : 0;

            updateAllStats(pointsData.length, totalOpen, totalClosed, openRatio, avgPhiOverM, 
                          moduli, primeModuli, compositeModuli, avgPointsPerMod, 
                          admissibleCount, admissibleRatio, error, convergence);

            return { totalOpen, totalClosed, avgPhiOverM, countModuli };
        }

        function updateProgressDisplay(count, currentMod, maxMod) {
            const modMin = parseInt(document.getElementById('modMin').value);
            const percent = ((currentMod - modMin) / (maxMod - modMin) * 100).toFixed(1);
            document.getElementById('animationStatus').textContent = 
                `Computing: ${count.toLocaleString()} points (${percent}% - m=${currentMod})`;
            document.getElementById('animationStatus').style.background = '#1a4d4d';
        }

        function hideProgressDisplay() {
            document.getElementById('animationStatus').textContent = 'Status: Stopped';
            document.getElementById('animationStatus').style.background = 'var(--bg-secondary)';
        }

        function getCacheKey() {
            const mode = document.getElementById('modSelectionMode').value;
            const moduli = getSelectedModuli();
            const moduliHash = moduli.join('_');
            const angularMapping = document.getElementById('angularMapping').value;
            return `modular_rings_${mode}_${moduliHash}_${angularMapping}`;
        }

        function saveToCache() {
            try {
                const cacheKey = getCacheKey();
                const cacheData = {
                    pointsData: pointsData,
                    timestamp: Date.now(),
                    settings: {
                        modMin: document.getElementById('modMin').value,
                        modMax: document.getElementById('modMax').value,
                        modStep: document.getElementById('modStep').value,
                        angularMapping: document.getElementById('angularMapping').value
                    }
                };
                
                // Only cache if dataset is reasonable size (< 50MB estimated)
                const dataSize = JSON.stringify(cacheData).length;
                if (dataSize < 50000000) {
                    localStorage.setItem(cacheKey, JSON.stringify(cacheData));
                    console.log(`Cached ${pointsData.length} points (${(dataSize/1024/1024).toFixed(2)} MB)`);
                }
            } catch (e) {
                console.warn('Cache save failed:', e);
            }
        }

        function loadFromCache() {
            try {
                const cacheKey = getCacheKey();
                const cached = localStorage.getItem(cacheKey);
                
                if (cached) {
                    const cacheData = JSON.parse(cached);
                    const age = Date.now() - cacheData.timestamp;
                    
                    // Cache valid for 1 hour
                    if (age < 3600000) {
                        pointsData = cacheData.pointsData;
                        console.log(`Loaded ${pointsData.length} points from cache`);
                        
                        // Restore modRotations
                        pointsData.forEach(p => {
                            if (!modRotations[p.m]) modRotations[p.m] = 0;
                        });
                        
                        // Update stats
                        const totalOpen = pointsData.filter(p => p.isOpen).length;
                        const totalClosed = pointsData.length - totalOpen;
                        const moduli = [...new Set(pointsData.map(p => p.m))];
                        const sumPhiOverM = moduli.reduce((sum, m) => {
                            const phiM = pointsData.find(p => p.m === m).phiM;
                            return sum + phiM / m;
                        }, 0);
                        
                        const openRatio = totalClosed > 0 ? totalOpen / (totalOpen + totalClosed) : 0;
                        document.getElementById('statTotal').textContent = pointsData.length.toLocaleString();
                        document.getElementById('statOpen').textContent = totalOpen.toLocaleString();
                        document.getElementById('statClosed').textContent = totalClosed.toLocaleString();
                        document.getElementById('statRatio').textContent = openRatio.toFixed(4);
                        document.getElementById('statAvgPhi').textContent = (sumPhiOverM / moduli.length).toFixed(4);
                        
                        return true;
                    }
                }
            } catch (e) {
                console.warn('Cache load failed:', e);
            }
            return false;
        }

        function clearCache() {
            try {
                const keys = Object.keys(localStorage);
                let count = 0;
                keys.forEach(key => {
                    if (key.startsWith('modular_rings_')) {
                        localStorage.removeItem(key);
                        count++;
                    }
                });
                alert(`Cache cleared! Removed ${count} cached dataset(s).`);
            } catch (e) {
                alert('Failed to clear cache: ' + e.message);
            }
        }

        function progressiveRender() {
            // Always render immediately - removed progressive rendering complexity
            drawVisualization();
            updateTrackerInfo();
        }

        function toggleTheme() {
            currentTheme = currentTheme === 'dark' ? 'light' : 'dark';
            document.body.className = currentTheme + '-theme';
            document.getElementById('themeText').textContent = currentTheme === 'dark' ? 'Light Mode' : 'Dark Mode';
            
            // Update canvas background immediately
            if (pointsData.length > 0) {
                drawVisualization();
            }
        }

        // Initialize dark theme
        function initializeTheme() {
            document.body.className = 'light-theme';
            document.getElementById('themeText').textContent = 'Dark Mode';
            currentTheme = 'light';
        }

        function toggleSection(header) {
            header.classList.toggle('collapsed');
            const content = header.nextElementSibling;
            content.classList.toggle('collapsed');
        }

        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2) return true;
            if (n % 2 === 0) return false;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return false;
            }
            return true;
        }

        function primeFactorization(n) {
            if (n <= 1) return '';
            const factors = [];
            let temp = n;
            for (let i = 2; i * i <= temp; i++) {
                let count = 0;
                while (temp % i === 0) {
                    count++;
                    temp /= i;
                }
                if (count > 0) {
                    factors.push(count === 1 ? `${i}` : `${i}^${count}`);
                }
            }
            if (temp > 1) factors.push(`${temp}`);
            return factors.join('×') || `${n}`;
        }

        function reduceFraction(num, den) {
            const g = gcd(num, den);
            return [num / g, den / g];
        }

        function getPointLabel(point, labelType) {
            switch(labelType) {
                case 'residue':
                    return `${point.r}`;
                case 'farey':
                    return `${point.r}/${point.m}`;
                case 'farey-reduced':
                    const [num, den] = reduceFraction(point.r, point.m);
                    return `${num}/${den}`;
                case 'theta':
                    return `${(point.angle * 180 / Math.PI).toFixed(1)}°`;
                case 'theta-rad':
                    return `${(point.angle / Math.PI).toFixed(3)}π`;
                case 'modulus':
                    return `${point.m}`;
                case 'gcd':
                    return `${point.gcd}`;
                case 'pair':
                    return `(${point.m},${point.r})`;
                case 'euler-phi':
                    return `φ=${point.phiM}`;
                case 'totient-index':
                    // Index of this residue among totatives of m
                    const totatives = [];
                    for (let i = 0; i < point.m; i++) {
                        if (gcd(i, point.m) === 1) totatives.push(i);
                    }
                    const idx = totatives.indexOf(point.r);
                    return idx >= 0 ? `#${idx + 1}` : 'N/A';
                case 'prime-factorization':
                    return point.r === 0 ? '0' : primeFactorization(point.r);
                case 'coprime-status':
                    return point.isOpen ? '✓' : '✗';
                default:
                    return `${point.r}`;
            }
        }

        function shouldShowLabel(point, filter, filterValue) {
            switch(filter) {
                case 'all':
                    return true;
                case 'open-only':
                    return point.isOpen;
                case 'closed-only':
                    return !point.isOpen;
                case 'admissible':
                    return point.isAdmissible;
                case 'primes':
                    return isPrime(point.r);
                case 'mod-specific':
                    return point.m === filterValue;
                case 'gcd-specific':
                    return point.gcd === filterValue;
                default:
                    return true;
            }
        }

        function gcd(a, b) {
            a = Math.abs(a);
            b = Math.abs(b);
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }

        function phi(n) {
            let result = n;
            for (let p = 2; p * p <= n; p++) {
                if (n % p === 0) {
                    while (n % p === 0) n /= p;
                    result -= result / p;
                }
            }
            if (n > 1) result -= result / n;
            return Math.round(result);
        }

        function smallestPrimeFactor(n) {
            if (n <= 1) return 1;
            for (let i = 2; i * i <= n; i++) {
                if (n % i === 0) return i;
            }
            return n;
        }

        function largestPrimeFactor(n) {
            if (n <= 1) return 1;
            let largest = n;
            for (let i = 2; i * i <= n; i++) {
                while (n % i === 0) {
                    largest = i;
                    n /= i;
                }
            }
            if (n > 1) largest = n;
            return largest;
        }

        function hslToRgb(h, s, l) {
            s /= 100;
            l /= 100;
            const k = n => (n + h / 30) % 12;
            const a = s * Math.min(l, 1 - l);
            const f = n => l - a * Math.max(-1, Math.min(k(n) - 3, Math.min(9 - k(n), 1)));
            return [Math.round(255 * f(0)), Math.round(255 * f(8)), Math.round(255 * f(4))];
        }

        function getColorForPoint(point, isOpen) {
            const theoremMode = document.getElementById('theoremMode').value;
            
            // Apply theorem-based coloring if enabled
            if (theoremMode !== 'none') {
                const highlightPrime = document.getElementById('highlightPrimeOrbits').checked;
                const highlightComposite = document.getElementById('highlightCompositeProjection').checked;
                const highlightFarey = document.getElementById('highlightFareyChannels').checked;
                
                // Check if this modulus is prime
                const isPrimeModulus = isPrime(point.m);
                
                // Farey channels: points that are reducible (can project to simpler fractions)
                const isFareyPoint = point.gcd > 1;
                
                if (theoremMode === 'prime-avoidance' || theoremMode === 'both') {
                    // Theorem 1: Highlight prime moduli (cyan) - they avoid Farey channels
                    if (highlightPrime && isPrimeModulus && isOpen) {
                        return '#00ffff'; // Cyan for prime coprime manifolds
                    }
                    
                    // Gold for Farey channel targets
                    if (highlightFarey && isFareyPoint) {
                        return '#ffc800'; // Gold for Farey channels
                    }
                }
                
                if (theoremMode === 'composite-projection' || theoremMode === 'both') {
                    // Theorem 2: Highlight composite projections onto channels (red)
                    if (highlightComposite && !isPrimeModulus && isFareyPoint) {
                        return '#ff0064'; // Red for composite projections
                    }
                }
                
                // If showing interstitial regions, dim non-highlighted points
                const showInterstitial = document.getElementById('showInterstitialRegions').checked;
                if (showInterstitial && !isPrimeModulus && isOpen && !isFareyPoint) {
                    return '#666666'; // Gray for interstitial regions
                }
            }
            
            // Default coloring logic
            if (isOpen) {
                const mode = document.getElementById('openColorMode').value;
                if (mode === 'solid') return document.getElementById('baseOpenColor').value;
                
                let hue = 0;
                const sat = 80, light = 60;
                
                if (mode === 'by-residue') {
                    const maxR = Math.max(...pointsData.map(p => p.r));
                    hue = (point.r / maxR) * 360;
                } else if (mode === 'by-modulus') {
                    const maxM = Math.max(...pointsData.map(p => p.m));
                    hue = (point.m / maxM) * 360;
                } else if (mode === 'by-spf') {
                    const spf = smallestPrimeFactor(point.r === 0 ? point.m : point.r);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180};
                    hue = primeMap[spf] || ((spf * 13) % 360);
                } else if (mode === 'by-angle') {
                    hue = (point.angle / (2 * Math.PI)) * 360;
                }
                
                const [r, g, b] = hslToRgb(hue, sat, light);
                return `rgb(${r},${g},${b})`;
            } else {
                return document.getElementById('baseClosedColor').value;
            }
        }

        function syncInputs(sliderId, numberId) {
            const slider = document.getElementById(sliderId);
            const number = document.getElementById(numberId);
            slider.addEventListener('input', () => { number.value = slider.value; updateRangeDisplays(); });
            number.addEventListener('input', () => { slider.value = number.value; updateRangeDisplays(); });
        }

        syncInputs('globalSpeed', 'globalSpeedNum');
        syncInputs('modRotSpeed', 'modRotSpeedNum');
        syncInputs('gradientStrength', 'gradientStrengthNum');
        syncInputs('trackerSize', 'trackerSizeNum');
        syncInputs('pointSize', 'pointSizeNum');
        syncInputs('connOpacity', 'connOpacityNum');

        syncInputs('labelSize', 'labelSizeNum');
        syncInputs('labelSpacing', 'labelSpacingNum');
        syncInputs('gapOpacity', 'gapOpacityNum');
        syncInputs('gapLineWidth', 'gapLineWidthNum');
        syncInputs('connLineWidth', 'connLineWidthNum');

        function updateAllStats(total, open, closed, ratio, avgPhi, moduli, primes, composites, avgPoints, admissible, admRatio, error, convergence) {
            document.getElementById('statTotal').textContent = total.toLocaleString();
            document.getElementById('statOpen').textContent = open.toLocaleString();
            document.getElementById('statClosed').textContent = closed.toLocaleString();
            document.getElementById('statRatio').textContent = ratio.toFixed(4);
            document.getElementById('statAvgPhi').textContent = avgPhi.toFixed(4);
            document.getElementById('statModuliCount').textContent = moduli.length.toLocaleString();
            document.getElementById('statMinMod').textContent = moduli.length > 0 ? moduli[0] : '0';
            document.getElementById('statMaxMod').textContent = moduli.length > 0 ? moduli[moduli.length - 1] : '0';
            document.getElementById('statAvgPoints').textContent = avgPoints.toFixed(2);
            document.getElementById('statPrimeCount').textContent = primes.toLocaleString();
            document.getElementById('statCompositeCount').textContent = composites.toLocaleString();
            document.getElementById('statError').textContent = error.toFixed(6);
            document.getElementById('statConvergence').textContent = convergence.toFixed(2) + '%';
            document.getElementById('statAdmissible').textContent = admissible.toLocaleString();
            document.getElementById('statAdmissibleRatio').textContent = admRatio.toFixed(2) + '%';
        }

        // Show/hide connection mode options
        document.getElementById('connectionMode').addEventListener('change', function() {
            const mode = this.value;
            const specificModGroup = document.getElementById('specificModGroup');
            const sameModOptionsGroup = document.getElementById('sameModOptionsGroup');
            const sameModGapGroup = document.getElementById('sameModGapGroup');
            
            specificModGroup.style.display = mode === 'specific-mod' ? 'block' : 'none';
            sameModOptionsGroup.style.display = mode === 'same-mod' ? 'block' : 'none';
            
            if (mode === 'same-mod') {
                const pattern = document.getElementById('sameModPattern').value;
                sameModGapGroup.style.display = pattern === 'by-gap' ? 'block' : 'none';
            } else {
                sameModGapGroup.style.display = 'none';
            }
        });

        document.getElementById('sameModPattern').addEventListener('change', function() {
            const pattern = this.value;
            const sameModGapGroup = document.getElementById('sameModGapGroup');
            sameModGapGroup.style.display = pattern === 'by-gap' ? 'block' : 'none';
        });

        // Show/hide modulus configuration inputs based on mode
        document.getElementById('modSelectionMode').addEventListener('change', function() {
            const mode = this.value;
            const rangeInputs = document.getElementById('rangeInputs');
            const sequenceInputs = document.getElementById('sequenceInputs');
            const customInputs = document.getElementById('customInputs');
            
            rangeInputs.style.display = 'none';
            sequenceInputs.style.display = 'none';
            customInputs.style.display = 'none';
            
            if (mode === 'range') {
                rangeInputs.style.display = 'block';
            } else if (mode === 'custom') {
                customInputs.style.display = 'block';
            } else if (mode === 'fibonacci' || mode === 'primes' || mode === 'powers-of-2' || mode === 'powers-of-3') {
                sequenceInputs.style.display = 'block';
            }
        });

        const gapColorScheme = [
            '#ff0080', // Hot pink for gap 2
            '#00ffff', // Cyan for gap 4
            '#ffff00', // Yellow for gap 6
            '#ff8000', // Orange for gap 8
            '#00ff00', // Green for gap 10
            '#ff00ff', // Magenta for gap 12
            '#8080ff', // Light blue for gap 14
            '#ff0000', // Red for gap 16
            '#00ff80', // Spring green for gap 18
            '#ff80ff'  // Light magenta for gap 20
        ];

        function applyGapPreset() {
            const preset = document.getElementById('gapPreset').value;
            let gaps = [];
            
            switch(preset) {
                case 'twin':
                    gaps = [2];
                    break;
                case 'cousin':
                    gaps = [4];
                    break;
                case 'sexy':
                    gaps = [6];
                    break;
                case 'twin-cousin':
                    gaps = [2, 4];
                    break;
                case 'twin-sexy':
                    gaps = [2, 6];
                    break;
                case 'prime-triplet':
                    gaps = [2, 4];
                    break;
                case 'prime-quadruplet':
                    gaps = [2, 4, 6];
                    break;
                case 'first-hardy':
                    gaps = [2, 6, 8];
                    break;
                case 'admissible-5':
                    gaps = [2, 6, 8, 12];
                    break;
                case 'sexy-pair':
                    gaps = [6, 12];
                    break;
                case 'custom':
                default:
                    return; // Don't override custom values
            }
            
            document.getElementById('gapValues').value = gaps.join(',');
            updateGapColorPickers();
        }

        function updateGapColorPickers() {
            const gapInput = document.getElementById('gapValues').value;
            const gaps = gapInput.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g) && g > 0);
            
            const container = document.getElementById('gapColorPickers');
            container.innerHTML = '';
            
            gaps.forEach((gap, idx) => {
                const colorDiv = document.createElement('div');
                colorDiv.className = 'control-group';
                colorDiv.style.marginBottom = '8px';
                
                const label = document.createElement('label');
                label.textContent = `Gap ${gap} Color`;
                label.style.fontSize = '11px';
                
                const colorInput = document.createElement('input');
                colorInput.type = 'color';
                colorInput.id = `gapColor${idx}`;
                colorInput.value = gapColorScheme[idx % gapColorScheme.length];
                colorInput.style.width = '100%';
                colorInput.style.height = '35px';
                
                colorDiv.appendChild(label);
                colorDiv.appendChild(colorInput);
                container.appendChild(colorDiv);
            });
            
            document.getElementById('activeGapsDisplay').textContent = gaps.join(', ') || 'None';
        }

        document.getElementById('gapValues').addEventListener('input', updateGapColorPickers);
        document.getElementById('enableGapAnalysis').addEventListener('change', updateGapColorPickers);

        // Theorem mode change handler
        document.getElementById('theoremMode').addEventListener('change', function() {
            const mode = this.value;
            const settings = document.getElementById('theoremModeSettings');
            
            if (mode !== 'none') {
                settings.style.display = 'block';
                
                // Auto-configure for theorem visualization
                if (mode === 'prime-avoidance' || mode === 'both') {
                    document.getElementById('highlightPrimeOrbits').checked = true;
                    document.getElementById('highlightFareyChannels').checked = true;
                }
                
                if (mode === 'composite-projection' || mode === 'both') {
                    document.getElementById('highlightCompositeProjection').checked = true;
                    document.getElementById('highlightFareyChannels').checked = true;
                }
            } else {
                settings.style.display = 'none';
            }
            
            drawVisualization();
        });

        // Theorem visualization option changes
        ['highlightFareyChannels', 'highlightPrimeOrbits', 'highlightCompositeProjection', 
         'showChannelMultiplicity', 'showInterstitialRegions'].forEach(id => {
            document.getElementById(id).addEventListener('change', () => {
                drawVisualization();
            });
        });

        // Auto-start animation when rotation values change (if auto-rotate enabled)
        function autoStartAnimation() {
            const autoRotate = document.getElementById('autoRotate').checked;
            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            
            if (autoRotate && (globalSpeed > 0 || modRotSpeed > 0)) {
                if (!animationId) {
                    startAnimation();
                }
            } else if (globalSpeed === 0 && modRotSpeed === 0) {
                // Stop animation and reset to 0 when both sliders return to 0
                if (animationId) {
                    stopAnimation();
                }
            }
        }

        function toggleAnimation() {
            if (animationId) {
                stopAnimation();
                document.getElementById('playButton').textContent = 'Play';
                document.getElementById('playButton').style.background = '#00ff00';
                document.getElementById('playButton').style.color = '#000000';
            } else {
                startAnimation();
                document.getElementById('playButton').textContent = 'Pause';
                document.getElementById('playButton').style.background = '#ff0000';
                document.getElementById('playButton').style.color = '#ffffff';
            }
        }

        function resetRotations() {
            globalRotation = 0;
            Object.keys(modRotations).forEach(m => {
                modRotations[m] = 0;
            });
            drawVisualization();
        }

        document.getElementById('globalSpeed').addEventListener('input', autoStartAnimation);
        document.getElementById('globalSpeedNum').addEventListener('input', autoStartAnimation);
        document.getElementById('modRotSpeed').addEventListener('input', autoStartAnimation);
        document.getElementById('modRotSpeedNum').addEventListener('input', autoStartAnimation);

        document.getElementById('invertModOrder').addEventListener('change', () => {
            drawVisualization();
        });

        function updateRangeDisplays() {
            document.getElementById('globalSpeedDisplay').textContent = document.getElementById('globalSpeed').value;
            document.getElementById('modRotSpeedDisplay').textContent = document.getElementById('modRotSpeed').value;
            document.getElementById('gradientStrengthDisplay').textContent = document.getElementById('gradientStrength').value;
            document.getElementById('pointSizeDisplay').textContent = document.getElementById('pointSize').value;
            document.getElementById('trackerSizeDisplay').textContent = document.getElementById('trackerSize').value;
            document.getElementById('connOpacityDisplay').textContent = document.getElementById('connOpacity').value;
            document.getElementById('labelSizeDisplay').textContent = document.getElementById('labelSize').value;
            document.getElementById('labelSpacingDisplay').textContent = document.getElementById('labelSpacing').value;
            document.getElementById('gapOpacityDisplay').textContent = document.getElementById('gapOpacity').value;
            document.getElementById('gapLineWidthDisplay').textContent = document.getElementById('gapLineWidth').value;
            document.getElementById('connLineWidthDisplay').textContent = document.getElementById('connLineWidth').value;
        }

        document.querySelectorAll('input[type="range"]').forEach(input => {
            input.addEventListener('input', updateRangeDisplays);
        });

        function generatePointsData() {
            // Check if we can load from cache first
            if (loadFromCache()) {
                progressiveRender();
                updateModuliDisplay();
                return;
            }

            const moduli = getSelectedModuli();
            
            if (moduli.length === 0) {
                alert('No valid moduli selected. Please check your input.');
                return;
            }

            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const gapInput = document.getElementById('gapValues').value;
            const gaps = gapInput.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g) && g > 0);
            const angularMapping = document.getElementById('angularMapping').value;

            // Calculate total expected points
            let totalExpectedPoints = 0;
            moduli.forEach(m => {
                totalExpectedPoints += m;
            });

            updateModuliDisplay();

            // Use progressive computation for large datasets
            if (totalExpectedPoints > 20000) {
                isComputing = true;
                document.getElementById('animationStatus').textContent = 'Computing: Starting...';
                document.getElementById('animationStatus').style.background = '#1a4d4d';
                
                computePointsProgressiveFromList(moduli, enableGap ? gaps : [], angularMapping)
                    .then(() => {
                        isComputing = false;
                        hideProgressDisplay();
                        saveToCache();
                        drawVisualization();
                        updateTrackerInfo();
                    });
                return;
            }

            // Fallback: compute directly (for small datasets)
            pointsData = [];
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;

            for (let m of moduli) {
                if (!modRotations[m]) modRotations[m] = 0;
                
                const phiM = phi(m);
                sumPhiOverM += phiM / m;
                countModuli++;

                for (let r = 0; r < m; r++) {
                    const g = gcd(r, m);
                    const isOpen = g === 1;
                    
                    if (isOpen) totalOpen++;
                    else totalClosed++;

                    let admissibleGaps = [];
                    if (enableGap && isOpen) {
                        gaps.forEach(gap => {
                            const rPlusG = (r + gap) % m;
                            if (gcd(rPlusG, m) === 1) {
                                admissibleGaps.push(gap);
                            }
                        });
                    }

                    let angle;
                    switch(angularMapping) {
                        case 'standard':
                            angle = (2 * Math.PI * r) / m;
                            break;
                        case 'half':
                            angle = (Math.PI * r) / m;
                            break;
                        case 'inverted':
                            angle = (2 * Math.PI * (m - r)) / m;
                            break;
                        case 'negative':
                            angle = -(2 * Math.PI * r) / m;
                            break;
                        default:
                            angle = (2 * Math.PI * r) / m;
                    }

                    pointsData.push({
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        phiM: phiM,
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps
                    });
                }
            }

            const avgPhiOverM = countModuli > 0 ? sumPhiOverM / countModuli : 0;
            const openRatio = (totalOpen + totalClosed) > 0 ? totalOpen / (totalOpen + totalClosed) : 0;
            
            // Calculate additional statistics
            const moduliArray = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const primeModuli = moduliArray.filter(m => isPrime(m)).length;
            const compositeModuli = moduliArray.length - primeModuli;
            const avgPointsPerMod = moduliArray.length > 0 ? pointsData.length / moduliArray.length : 0;
            const admissibleCount = pointsData.filter(p => p.isAdmissible).length;
            const admissibleRatio = totalOpen > 0 ? (admissibleCount / totalOpen) * 100 : 0;
            const theoretical = 6 / (Math.PI * Math.PI);
            const error = Math.abs(avgPhiOverM - theoretical);
            const convergence = theoretical > 0 ? (1 - error / theoretical) * 100 : 0;

            updateAllStats(pointsData.length, totalOpen, totalClosed, openRatio, avgPhiOverM,
                          moduliArray, primeModuli, compositeModuli, avgPointsPerMod,
                          admissibleCount, admissibleRatio, error, convergence);

            saveToCache();
            updateTrackerInfo();
        }

        function getSelectedModuli() {
            const mode = document.getElementById('modSelectionMode').value;
            const includeUnit = document.getElementById('includeUnitCircle').checked;
            let moduli = [];

            if (mode === 'range') {
                const modMin = parseInt(document.getElementById('modMin').value);
                const modMax = parseInt(document.getElementById('modMax').value);
                const modStep = parseInt(document.getElementById('modStep').value);
                
                for (let m = modMin; m <= modMax; m += modStep) {
                    moduli.push(m);
                }
            } else if (mode === 'fibonacci') {
                const maxVal = parseInt(document.getElementById('sequenceMax').value);
                let a = 1, b = 1;
                if (a <= maxVal) moduli.push(a);
                while (b <= maxVal) {
                    moduli.push(b);
                    let temp = a + b;
                    a = b;
                    b = temp;
                }
            } else if (mode === 'primes') {
                const maxVal = parseInt(document.getElementById('sequenceMax').value);
                for (let n = 2; n <= maxVal; n++) {
                    if (isPrime(n)) {
                        moduli.push(n);
                    }
                }
            } else if (mode === 'powers-of-2') {
                const numTerms = parseInt(document.getElementById('sequenceTerms').value);
                for (let i = 0; i < numTerms; i++) {
                    const val = Math.pow(2, i);
                    if (val >= 1) moduli.push(val);
                }
            } else if (mode === 'powers-of-3') {
                const numTerms = parseInt(document.getElementById('sequenceTerms').value);
                for (let i = 0; i < numTerms; i++) {
                    const val = Math.pow(3, i);
                    if (val >= 1) moduli.push(val);
                }
            } else if (mode === 'M30-sequence') {
                const numTerms = parseInt(document.getElementById('sequenceTerms').value);
                for (let n = 0; n < numTerms; n++) {
                    const val = 30 * Math.pow(2, n);
                    moduli.push(val);
                }
            } else if (mode === 'custom') {
                const customInput = document.getElementById('customModuli').value;
                moduli = customInput.split(',')
                    .map(m => parseInt(m.trim()))
                    .filter(m => !isNaN(m) && m > 0);
            }

            // Add unit circle if requested and not already present
            if (includeUnit && !moduli.includes(1)) {
                moduli.unshift(1);
            }

            // Remove duplicates and sort
            moduli = [...new Set(moduli)].sort((a, b) => a - b);

            return moduli;
        }

        async function computePointsProgressiveFromList(moduli, gaps, angularMapping) {
            pointsData = [];
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;
            let processedCount = 0;

            for (let m of moduli) {
                if (!modRotations[m]) modRotations[m] = 0;
                
                const phiM = phi(m);
                sumPhiOverM += phiM / m;
                countModuli++;

                for (let r = 0; r < m; r++) {
                    const g = gcd(r, m);
                    const isOpen = g === 1;
                    
                    if (isOpen) totalOpen++;
                    else totalClosed++;

                    let admissibleGaps = [];
                    if (isOpen && gaps.length > 0) {
                        gaps.forEach(gap => {
                            const rPlusG = (r + gap) % m;
                            if (gcd(rPlusG, m) === 1) {
                                admissibleGaps.push(gap);
                            }
                        });
                    }

                    let angle;
                    switch(angularMapping) {
                        case 'standard':
                            angle = (2 * Math.PI * r) / m;
                            break;
                        case 'half':
                            angle = (Math.PI * r) / m;
                            break;
                        case 'inverted':
                            angle = (2 * Math.PI * (m - r)) / m;
                            break;
                        case 'negative':
                            angle = -(2 * Math.PI * r) / m;
                            break;
                        default:
                            angle = (2 * Math.PI * r) / m;
                    }

                    pointsData.push({
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        phiM: phiM,
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps
                    });

                    processedCount++;

                    if (processedCount % COMPUTE_CHUNK_SIZE === 0) {
                        updateProgressDisplay(processedCount, m, moduli[moduli.length - 1]);
                        if (processedCount > 50000) {
                            await new Promise(resolve => setTimeout(resolve, 0));
                        }
                    }
                }
            }

            const avgPhiOverM = countModuli > 0 ? sumPhiOverM / countModuli : 0;
            const openRatio = (totalOpen + totalClosed) > 0 ? totalOpen / (totalOpen + totalClosed) : 0;

            document.getElementById('statTotal').textContent = pointsData.length.toLocaleString();
            document.getElementById('statOpen').textContent = totalOpen.toLocaleString();
            document.getElementById('statClosed').textContent = totalClosed.toLocaleString();
            document.getElementById('statRatio').textContent = openRatio.toFixed(4);
            document.getElementById('statAvgPhi').textContent = avgPhiOverM.toFixed(4);

            return { totalOpen, totalClosed, avgPhiOverM, countModuli };
        }

        function updateModuliDisplay() {
            const moduli = getSelectedModuli();
            const mode = document.getElementById('modSelectionMode').value;
            let displayText = '';

            if (moduli.length === 0) {
                displayText = 'None selected';
            } else if (moduli.length <= 10) {
                displayText = moduli.join(', ');
            } else {
                displayText = `${moduli[0]}, ${moduli[1]}, ..., ${moduli[moduli.length-1]} (${moduli.length} total)`;
            }

            if (mode === 'fibonacci') displayText = 'Fibonacci: ' + displayText;
            else if (mode === 'primes') displayText = 'Primes: ' + displayText;
            else if (mode === 'powers-of-2') displayText = 'Powers of 2: ' + displayText;
            else if (mode === 'powers-of-3') displayText = 'Powers of 3: ' + displayText;
            else if (mode === 'M30-sequence') displayText = 'M₃₀ = 30×2ⁿ: ' + displayText;

            document.getElementById('moduliList').textContent = displayText;
        }

        function updateTrackerInfo() {
            const enabled = document.getElementById('enableTracker').checked;
            const trackedInput = document.getElementById('trackedResidues').value;
            const trackedRs = trackedInput.split(',').map(r => parseInt(r.trim())).filter(r => !isNaN(r));
            const modFilter = document.getElementById('trackerModFilter').value;
            const filterMod = modFilter ? parseInt(modFilter) : null;
            const trackerInfo = document.getElementById('trackerInfo');
            
            if (enabled && trackedRs.length > 0) {
                trackerInfo.style.display = 'block';
                let infoHTML = '';
                
                trackedRs.forEach(trackedR => {
                    let trackedPoints = pointsData.filter(p => p.r === trackedR);
                    if (filterMod !== null) {
                        trackedPoints = trackedPoints.filter(p => p.m === filterMod);
                    }
                    
                    const openCount = trackedPoints.filter(p => p.isOpen).length;
                    infoHTML += `<strong>r = ${trackedR}</strong>`;
                    if (filterMod !== null) {
                        infoHTML += ` (m = ${filterMod})`;
                    }
                    infoHTML += `<br>Appears: ${trackedPoints.length} times<br>`;
                    infoHTML += `Open: ${openCount}, Closed: ${trackedPoints.length - openCount}<br><br>`;
                });
                
                document.getElementById('trackerInfoContent').innerHTML = infoHTML;
            } else {
                trackerInfo.style.display = 'none';
            }
        }

        document.getElementById('enableTracker').addEventListener('change', updateTrackerInfo);
        document.getElementById('trackedResidues').addEventListener('input', updateTrackerInfo);
        document.getElementById('trackerModFilter').addEventListener('input', updateTrackerInfo);

        function closePointInfo() {
            document.getElementById('pointInfoPanel').style.display = 'none';
        }

        function showPointInfo(point) {
            const panel = document.getElementById('pointInfoPanel');
            const content = document.getElementById('pointInfoContent');
            
            let html = `<div style="margin-bottom: 12px;">
                <strong style="font-size: 15px; color: var(--text-primary);">Modulus m = ${point.m}</strong>
            </div>`;
            
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">Residue r =</span> <strong>${point.r}</strong>
            </div>`;
            
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">gcd(${point.r}, ${point.m}) =</span> <strong>${point.gcd}</strong>
            </div>`;
            
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">Channel:</span> <strong style="color: ${point.isOpen ? '#00ff00' : '#ff0000'};">${point.isOpen ? 'OPEN' : 'CLOSED'}</strong>
            </div>`;
            
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">φ(${point.m}) =</span> <strong>${point.phiM}</strong>
            </div>`;
            
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">Angle:</span> <strong>${(point.angle * 180 / Math.PI).toFixed(2)}°</strong>
            </div>`;
            
            const [num, den] = reduceFraction(point.r, point.m);
            html += `<div style="margin-bottom: 10px;">
                <span style="opacity: 0.8;">Farey Fraction:</span> <strong>${point.r}/${point.m}</strong>
            </div>`;
            
            if (num !== point.r || den !== point.m) {
                html += `<div style="margin-bottom: 10px;">
                    <span style="opacity: 0.8;">Reduced:</span> <strong>${num}/${den}</strong>
                </div>`;
            }
            
            if (point.isAdmissible) {
                html += `<div style="margin-top: 15px; padding: 10px; background: rgba(170, 0, 255, 0.2); border-left: 3px solid #aa00ff;">
                    <strong style="color: #aa00ff;">GAP ADMISSIBLE</strong><br>
                    <span style="font-size: 11px; opacity: 0.9;">Gaps: ${point.admissibleGaps.join(', ')}</span>
                </div>`;
            }
            
            content.innerHTML = html;
            panel.style.display = 'block';
        }

        function drawVisualization() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;

            // Always use black background for canvas
            const bgColor = '#000000';
            ctx.clearRect(0, 0, width, height);
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, width, height);

            // Use performance mode automatically for large datasets
            const performanceMode = pointsData.length > 20000;
            
            ctx.save();
            ctx.translate(centerX + transform.x, centerY + transform.y);
            ctx.scale(transform.scale, transform.scale);
            ctx.rotate(globalRotation * Math.PI / 180);

            const displayMode = document.getElementById('displayMode').value;
            const showOpen = document.getElementById('showOpen').checked;
            const showClosed = document.getElementById('showClosed').checked;
            const showRingLines = document.getElementById('showRingLines').checked;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modMin = parseInt(document.getElementById('modMin').value);
            const modStep = parseInt(document.getElementById('modStep').value);
            const enableTracker = document.getElementById('enableTracker').checked;
            const trackerColor = document.getElementById('trackerColor').value;
            const trackerSize = parseFloat(document.getElementById('trackerSize').value);
            const enableConnections = document.getElementById('enableConnections').checked;
            const connectionMode = document.getElementById('connectionMode').value;
            const connOpacity = parseFloat(document.getElementById('connOpacity').value);
            const onlyOpenConn = document.getElementById('onlyOpenConn').checked;

            const radiusScale = displayMode === 'unit' ? maxRadius : maxRadius / modMax;

            // Always use white/light colors for lines on black background
            const lineColor = 'rgba(255, 255, 255, 0.2)';
            const connectionLineColor = `rgba(255, 255, 255, ${connOpacity})`;

            // Function to get proper radius for each modulus
            function getRadius(m) {
                const invertOrder = document.getElementById('invertModOrder').checked;
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
                
                if (displayMode === 'unit') {
                    return maxRadius;
                }
                
                if (invertOrder) {
                    // Map largest modulus to innermost, smallest to outermost
                    const maxMod = Math.max(...moduli);
                    const minMod = Math.min(...moduli);
                    const inverted = maxMod - (m - minMod);
                    return inverted * radiusScale;
                }
                
                // Normal: m=1 is innermost
                return m * radiusScale;
            }

            // Draw ring lines
            if (showRingLines && displayMode === 'rings') {
                ctx.strokeStyle = lineColor;
                ctx.lineWidth = 1 / transform.scale;
                for (let m = modMin; m <= modMax; m += modStep) {
                    ctx.beginPath();
                    ctx.arc(0, 0, getRadius(m), 0, 2 * Math.PI);
                    ctx.stroke();
                }
            }

            // Draw connection lines
            if (enableConnections && connectionMode !== 'none' && displayMode === 'rings') {
                const connLineWidth = parseFloat(document.getElementById('connLineWidth').value);
                ctx.strokeStyle = connectionLineColor;
                ctx.lineWidth = connLineWidth / transform.scale;

                if (connectionMode === 'same-mod') {
                    // Same modulus connections
                    const sameModPattern = document.getElementById('sameModPattern').value;
                    const sameModGap = parseInt(document.getElementById('sameModGap').value);
                    
                    const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
                    
                    moduli.forEach(m => {
                        const pointsInMod = pointsData.filter(p => p.m === m);
                        
                        pointsInMod.forEach((p1, idx) => {
                            if (onlyOpenConn && !p1.isOpen) return;
                            
                            let targetPoints = [];
                            
                            if (sameModPattern === 'all') {
                                // Connect to all other points in same modulus
                                targetPoints = pointsInMod.filter(p2 => p2.r !== p1.r);
                            } else if (sameModPattern === 'sequential') {
                                // Connect to next point (r to r+1)
                                const nextR = (p1.r + 1) % m;
                                targetPoints = pointsInMod.filter(p2 => p2.r === nextR);
                            } else if (sameModPattern === 'open-only') {
                                // Connect all open channels in this modulus
                                if (p1.isOpen) {
                                    targetPoints = pointsInMod.filter(p2 => p2.isOpen && p2.r !== p1.r);
                                }
                            } else if (sameModPattern === 'by-gap') {
                                // Connect by gap interval
                                const targetR = (p1.r + sameModGap) % m;
                                targetPoints = pointsInMod.filter(p2 => p2.r === targetR);
                            }
                            
                            targetPoints.forEach(p2 => {
                                if (onlyOpenConn && !p2.isOpen) return;
                                
                                const modRot = modRotations[m] || 0;
                                
                                const angle1 = p1.angle + (modRot * Math.PI / 180);
                                const r1 = getRadius(m);
                                const x1 = r1 * Math.cos(angle1);
                                const y1 = r1 * Math.sin(angle1);
                                
                                const angle2 = p2.angle + (modRot * Math.PI / 180);
                                const r2 = getRadius(m);
                                const x2 = r2 * Math.cos(angle2);
                                const y2 = r2 * Math.sin(angle2);
                                
                                ctx.beginPath();
                                ctx.moveTo(x1, y1);
                                ctx.lineTo(x2, y2);
                                ctx.stroke();
                            });
                        });
                    });
                } else if (connectionMode === 'specific-mod') {
                    // Specific modulus only
                    const specificMod = parseInt(document.getElementById('specificModValue').value);
                    const pointsInMod = pointsData.filter(p => p.m === specificMod);
                    
                    pointsInMod.forEach((p1, idx) => {
                        if (onlyOpenConn && !p1.isOpen) return;
                        if (idx < pointsInMod.length - 1) {
                            const p2 = pointsInMod[idx + 1];
                            if (onlyOpenConn && !p2.isOpen) return;
                            
                            const modRot = modRotations[specificMod] || 0;
                            
                            const angle1 = p1.angle + (modRot * Math.PI / 180);
                            const r1 = getRadius(specificMod);
                            const x1 = r1 * Math.cos(angle1);
                            const y1 = r1 * Math.sin(angle1);
                            
                            const angle2 = p2.angle + (modRot * Math.PI / 180);
                            const r2 = getRadius(specificMod);
                            const x2 = r2 * Math.cos(angle2);
                            const y2 = r2 * Math.sin(angle2);
                            
                            ctx.beginPath();
                            ctx.moveTo(x1, y1);
                            ctx.lineTo(x2, y2);
                            ctx.stroke();
                        }
                    });
                } else {
                    // Cross-modulus connections
                    const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
                    
                    for (let i = 0; i < moduli.length - 1; i++) {
                        const m1 = moduli[i];
                        const m2 = moduli[i + 1];
                        
                        const points1 = pointsData.filter(p => p.m === m1);
                        const points2 = pointsData.filter(p => p.m === m2);

                        points1.forEach(p1 => {
                            if (onlyOpenConn && !p1.isOpen) return;

                            const modRot1 = modRotations[m1] || 0;
                            const angle1 = p1.angle + (modRot1 * Math.PI / 180);
                            const r1 = getRadius(m1);
                            const x1 = r1 * Math.cos(angle1);
                            const y1 = r1 * Math.sin(angle1);

                            let targetPoints = [];
                            
                            if (connectionMode === 'next-mod') {
                                targetPoints = points2.filter(p2 => p2.r === p1.r);
                            } else if (connectionMode === 'binary-lift') {
                                targetPoints = points2.filter(p2 => p2.r === p1.r || p2.r === (p1.r + m1) % m2);
                            } else if (connectionMode === 'double-lift') {
                                for (let n = 0; n < 5; n++) {
                                    const target = (p1.r + m1 * Math.pow(2, n)) % m2;
                                    targetPoints = targetPoints.concat(points2.filter(p2 => p2.r === target));
                                }
                            }

                            targetPoints.forEach(p2 => {
                                if (onlyOpenConn && !p2.isOpen) return;

                                const modRot2 = modRotations[m2] || 0;
                                const angle2 = p2.angle + (modRot2 * Math.PI / 180);
                                const r2 = getRadius(m2);
                                const x2 = r2 * Math.cos(angle2);
                                const y2 = r2 * Math.sin(angle2);

                                ctx.beginPath();
                                ctx.moveTo(x1, y1);
                                ctx.lineTo(x2, y2);
                                ctx.stroke();
                            });
                        });
                    }
                }
            }

            // Draw points (with batching for performance)
            const batchSize = performanceMode ? 5000 : pointsData.length;
            
            for (let batchStart = 0; batchStart < pointsData.length; batchStart += batchSize) {
                const batchEnd = Math.min(batchStart + batchSize, pointsData.length);
                
                for (let i = batchStart; i < batchEnd; i++) {
                    const point = pointsData[i];
                    
                    if (!showOpen && point.isOpen) continue;
                    if (!showClosed && !point.isOpen) continue;

                const modRot = modRotations[point.m] || 0;
                const totalAngle = point.angle + (modRot * Math.PI / 180);
                const r = displayMode === 'unit' ? maxRadius : getRadius(point.m);
                const x = r * Math.cos(totalAngle);
                const y = r * Math.sin(totalAngle);

                let radius = pointSize;
                let color = getColorForPoint(point, point.isOpen);
                let opacity = point.isOpen ? 0.8 : 0.3;

                const highlightAdmissible = document.getElementById('highlightAdmissible').checked;
                if (highlightAdmissible && point.isAdmissible) {
                    radius = pointSize * 1.2;
                    color = '#aa00ff';
                    opacity = 0.9;
                }

                ctx.globalAlpha = opacity;
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, radius / transform.scale, 0, 2 * Math.PI);
                ctx.fill();
                ctx.globalAlpha = 1.0;

                point.screenX = x;
                point.screenY = y;
                point.screenRadius = radius / transform.scale;
                }
            }

            // Draw tracker
            if (enableTracker) {
                const trackedInput = document.getElementById('trackedResidues').value;
                const trackedRs = trackedInput.split(',').map(r => parseInt(r.trim())).filter(r => !isNaN(r));
                const modFilter = document.getElementById('trackerModFilter').value;
                const filterMod = modFilter ? parseInt(modFilter) : null;
                
                trackedRs.forEach(trackedResidue => {
                    let filteredPoints = pointsData.filter(p => p.r === trackedResidue);
                    if (filterMod !== null) {
                        filteredPoints = filteredPoints.filter(p => p.m === filterMod);
                    }
                    
                    filteredPoints.forEach(point => {
                        const modRot = modRotations[point.m] || 0;
                        const totalAngle = point.angle + (modRot * Math.PI / 180);
                        const r = displayMode === 'unit' ? maxRadius : getRadius(point.m);
                        const x = r * Math.cos(totalAngle);
                        const y = r * Math.sin(totalAngle);

                        ctx.strokeStyle = trackerColor;
                        ctx.lineWidth = 2 / transform.scale;
                        ctx.fillStyle = trackerColor;
                        ctx.globalAlpha = 0.9;
                        ctx.beginPath();
                        ctx.arc(x, y, trackerSize / transform.scale, 0, 2 * Math.PI);
                        ctx.fill();
                        ctx.stroke();
                        ctx.globalAlpha = 1.0;
                    });
                });
            }

            // Draw labels
            const showLabels = document.getElementById('showLabels').checked;
            if (showLabels) {
                const labelType = document.getElementById('labelType').value;
                const labelFilter = document.getElementById('labelFilter').value;
                const labelFilterValue = parseInt(document.getElementById('labelFilterValue').value);
                const labelSize = parseFloat(document.getElementById('labelSize').value);
                const labelColor = document.getElementById('labelColor').value;
                const labelBg = document.getElementById('labelBackground').checked;
                const labelSpacing = parseFloat(document.getElementById('labelSpacing').value);

                ctx.font = `${labelSize / transform.scale}px Arial`;
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';

                pointsData.forEach(point => {
                    if (!shouldShowLabel(point, labelFilter, labelFilterValue)) return;
                    if (!showOpen && point.isOpen) return;
                    if (!showClosed && !point.isOpen) return;

                    const modRot = modRotations[point.m] || 0;
                    const totalAngle = point.angle + (modRot * Math.PI / 180);
                    const r = displayMode === 'unit' ? maxRadius : getRadius(point.m);
                    const x = r * Math.cos(totalAngle);
                    const y = r * Math.sin(totalAngle);

                    const labelText = getPointLabel(point, labelType);
                    const labelOffset = (pointSize + labelSpacing) / transform.scale;
                    const labelX = x + labelOffset * Math.cos(totalAngle);
                    const labelY = y + labelOffset * Math.sin(totalAngle);

                    if (labelBg) {
                        const metrics = ctx.measureText(labelText);
                        const padding = 2 / transform.scale;
                        const bgHeight = labelSize / transform.scale + 2 * padding;
                        const bgWidth = metrics.width + 2 * padding;

                        ctx.fillStyle = currentTheme === 'dark' ? 'rgba(0, 0, 0, 0.7)' : 'rgba(255, 255, 255, 0.7)';
                        ctx.fillRect(
                            labelX - bgWidth / 2,
                            labelY - bgHeight / 2,
                            bgWidth,
                            bgHeight
                        );
                    }

                    ctx.fillStyle = labelColor;
                    ctx.fillText(labelText, labelX, labelY);
                });
            }

            // Draw gap connection lines
            const showGapLines = document.getElementById('showGapLines').checked;
            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const onlyPrimeGaps = document.getElementById('onlyPrimeGaps').checked;
            
            if (showGapLines && enableGap) {
                const gapInput = document.getElementById('gapValues').value;
                const gaps = gapInput.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g) && g > 0);
                const gapOpacity = parseFloat(document.getElementById('gapOpacity').value);
                const gapLineWidth = parseFloat(document.getElementById('gapLineWidth').value);

                gaps.forEach((gap, gapIdx) => {
                    const gapColorInput = document.getElementById(`gapColor${gapIdx}`);
                    const gapColor = gapColorInput ? gapColorInput.value : gapColorScheme[gapIdx % gapColorScheme.length];
                    
                    ctx.strokeStyle = gapColor;
                    ctx.globalAlpha = gapOpacity;
                    ctx.lineWidth = gapLineWidth / transform.scale;

                    // Group points by modulus for efficient lookup
                    const pointsByMod = {};
                    pointsData.forEach(p => {
                        if (!pointsByMod[p.m]) pointsByMod[p.m] = {};
                        pointsByMod[p.m][p.r] = p;
                    });

                    // Draw lines for this gap
                    pointsData.forEach(point => {
                        if (!point.isOpen) return;
                        
                        // If only prime gaps is enabled, check if current residue is prime
                        if (onlyPrimeGaps && !isPrime(point.r)) return;
                        
                        if (!point.admissibleGaps.includes(gap)) return;

                        const rPlusG = (point.r + gap) % point.m;
                        const targetPoint = pointsByMod[point.m] && pointsByMod[point.m][rPlusG];
                        
                        if (targetPoint && targetPoint.isOpen) {
                            // If only prime gaps is enabled, also check if target is prime
                            if (onlyPrimeGaps && !isPrime(targetPoint.r)) return;
                            
                            const modRot = modRotations[point.m] || 0;
                            
                            const angle1 = point.angle + (modRot * Math.PI / 180);
                            const r1 = displayMode === 'unit' ? maxRadius : getRadius(point.m);
                            const x1 = r1 * Math.cos(angle1);
                            const y1 = r1 * Math.sin(angle1);

                            const angle2 = targetPoint.angle + (modRot * Math.PI / 180);
                            const r2 = displayMode === 'unit' ? maxRadius : getRadius(targetPoint.m);
                            const x2 = r2 * Math.cos(angle2);
                            const y2 = r2 * Math.sin(angle2);

                            ctx.beginPath();
                            ctx.moveTo(x1, y1);
                            ctx.lineTo(x2, y2);
                            ctx.stroke();
                        }
                    });
                    
                    ctx.globalAlpha = 1.0;
                });
            }

            ctx.restore();
        }

        function animate() {
            if (!animationId) return;

            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            const speedGradient = document.getElementById('speedGradient').value;
            const gradientStrength = parseFloat(document.getElementById('gradientStrength').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modMin = parseInt(document.getElementById('modMin').value);

            globalRotation += globalSpeed;
            if (globalRotation > 360) globalRotation -= 360;

            Object.keys(modRotations).forEach(m => {
                let speed = modRotSpeed;
                
                if (speedGradient === 'inner-to-outer') {
                    const factor = (m - modMin) / (modMax - modMin);
                    speed = modRotSpeed * (1 + factor * gradientStrength);
                } else if (speedGradient === 'outer-to-inner') {
                    const factor = (modMax - m) / (modMax - modMin);
                    speed = modRotSpeed * (1 + factor * gradientStrength);
                }
                
                modRotations[m] += speed;
                if (modRotations[m] > 360) modRotations[m] -= 360;
            });

            // Use appropriate renderer
            if (currentRenderer === 'canvas2d') {
                drawVisualization();
            } else if (currentRenderer === 'webgl') {
                drawVisualizationWebGL();
            } else if (currentRenderer === 'svg') {
                drawVisualizationSVG();
            }
            
            animationId = requestAnimationFrame(animate);
        }

        function startAnimation() {
            if (!animationId) {
                document.getElementById('animationStatus').textContent = 'Status: Playing';
                document.getElementById('animationStatus').style.background = '#1a4d1a';
                document.getElementById('playButton').textContent = 'Pause';
                document.getElementById('playButton').style.background = '#ff0000';
                document.getElementById('playButton').style.color = '#ffffff';
                animationId = requestAnimationFrame(animate);
            }
        }

        function stopAnimation() {
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
                document.getElementById('animationStatus').textContent = 'Status: Stopped';
                document.getElementById('animationStatus').style.background = 'var(--bg-secondary)';
                document.getElementById('playButton').textContent = 'Play';
                document.getElementById('playButton').style.background = '#00ff00';
                document.getElementById('playButton').style.color = '#000000';
            }
        }

        // Mouse and touch events - work for both canvas and SVG
        let touchStartDist = 0;
        
        function getEventCoords(e) {
            if (e.touches) {
                return { x: e.touches[0].clientX, y: e.touches[0].clientY };
            }
            return { x: e.clientX, y: e.clientY };
        }

        function handleStart(e) {
            if (e.touches && e.touches.length === 2) {
                // Pinch zoom start
                const dx = e.touches[0].clientX - e.touches[1].clientX;
                const dy = e.touches[0].clientY - e.touches[1].clientY;
                touchStartDist = Math.sqrt(dx * dx + dy * dy);
            } else {
                // Pan start or potential click
                const coords = getEventCoords(e);
                isDragging = true;
                lastMouseX = coords.x;
                lastMouseY = coords.y;
            }
        }

        function handleMove(e) {
            if (e.touches && e.touches.length === 2) {
                // Pinch zoom
                e.preventDefault();
                const dx = e.touches[0].clientX - e.touches[1].clientX;
                const dy = e.touches[0].clientY - e.touches[1].clientY;
                const dist = Math.sqrt(dx * dx + dy * dy);
                const delta = dist / touchStartDist;
                touchStartDist = dist;
                
                const activeElement = currentRenderer === 'svg' ? svg : canvas;
                const rect = activeElement.getBoundingClientRect();
                const centerX = (e.touches[0].clientX + e.touches[1].clientX) / 2 - rect.left - activeElement.width / 2;
                const centerY = (e.touches[0].clientY + e.touches[1].clientY) / 2 - rect.top - activeElement.height / 2;
                
                transform.x = centerX - (centerX - transform.x) * delta;
                transform.y = centerY - (centerY - transform.y) * delta;
                transform.scale *= delta;
                transform.scale = Math.max(0.01, Math.min(100, transform.scale));
                
                if (currentRenderer === 'canvas2d') {
                    drawVisualization();
                } else if (currentRenderer === 'webgl') {
                    drawVisualizationWebGL();
                } else if (currentRenderer === 'svg') {
                    drawVisualizationSVG();
                }
            } else if (isDragging) {
                // Pan
                const coords = getEventCoords(e);
                const deltaX = coords.x - lastMouseX;
                const deltaY = coords.y - lastMouseY;
                
                // Only pan if there's significant movement (prevents accidental clicks from becoming pans)
                if (Math.abs(deltaX) > 2 || Math.abs(deltaY) > 2) {
                    transform.x += deltaX;
                    transform.y += deltaY;
                    lastMouseX = coords.x;
                    lastMouseY = coords.y;
                    
                    if (currentRenderer === 'canvas2d') {
                        drawVisualization();
                    } else if (currentRenderer === 'webgl') {
                        drawVisualizationWebGL();
                    } else if (currentRenderer === 'svg') {
                        drawVisualizationSVG();
                    }
                }
            } else if (currentRenderer === 'canvas2d') {
                // Hover for tooltip (only for canvas2d)
                const coords = getEventCoords(e);
                const rect = canvas.getBoundingClientRect();
                const x = (coords.x - rect.left - canvas.width / 2 - transform.x) / transform.scale;
                const y = (coords.y - rect.top - canvas.height / 2 - transform.y) / transform.scale;
                
                // Rotate back to find point
                const angle = -globalRotation * Math.PI / 180;
                const rx = x * Math.cos(angle) - y * Math.sin(angle);
                const ry = x * Math.sin(angle) + y * Math.cos(angle);
                
                let foundPoint = null;
                let minDist = Infinity;
                
                pointsData.forEach(point => {
                    if (point.screenX !== undefined) {
                        const dx = rx - point.screenX;
                        const dy = ry - point.screenY;
                        const dist = Math.sqrt(dx * dx + dy * dy);
                        if (dist < point.screenRadius * 2 && dist < minDist) {
                            minDist = dist;
                            foundPoint = point;
                        }
                    }
                });
                
                if (foundPoint) {
                    tooltip.style.opacity = '1';
                    tooltip.style.left = (coords.x + 15) + 'px';
                    tooltip.style.top = (coords.y + 15) + 'px';
                    tooltip.innerHTML = `
                        <strong>m = ${foundPoint.m}, r = ${foundPoint.r}</strong><br>
                        gcd(${foundPoint.r}, ${foundPoint.m}) = ${foundPoint.gcd}<br>
                        Channel: ${foundPoint.isOpen ? 'OPEN' : 'CLOSED'}<br>
                        φ(${foundPoint.m}) = ${foundPoint.phiM}<br>
                        Angle: ${(foundPoint.angle * 180 / Math.PI).toFixed(2)}°
                        ${foundPoint.isAdmissible ? '<br><strong>GAP ADMISSIBLE</strong>' : ''}
                    `;
                    canvas.style.cursor = 'pointer';
                } else {
                    tooltip.style.opacity = '0';
                    canvas.style.cursor = isDragging ? 'grabbing' : 'grab';
                }
            }
        }

        function handleEnd(e) {
            isDragging = false;
            touchStartDist = 0;
        }

        function handleWheel(e) {
            e.preventDefault();
            const delta = e.deltaY > 0 ? 0.9 : 1.1;
            
            const activeElement = currentRenderer === 'svg' ? svg : canvas;
            const rect = activeElement.getBoundingClientRect();
            const mouseX = e.clientX - rect.left - activeElement.width / 2;
            const mouseY = e.clientY - rect.top - activeElement.height / 2;
            
            transform.x = mouseX - (mouseX - transform.x) * delta;
            transform.y = mouseY - (mouseY - transform.y) * delta;
            transform.scale *= delta;
            transform.scale = Math.max(0.01, Math.min(100, transform.scale));
            
            if (currentRenderer === 'canvas2d') {
                drawVisualization();
            } else if (currentRenderer === 'webgl') {
                drawVisualizationWebGL();
            } else if (currentRenderer === 'svg') {
                drawVisualizationSVG();
            }
        }

        // Attach event listeners to both canvas and SVG
        [canvas, svg].forEach(element => {
            element.addEventListener('mousedown', handleStart);
            element.addEventListener('mousemove', handleMove);
            element.addEventListener('mouseup', handleEnd);
            element.addEventListener('mouseleave', () => { 
                isDragging = false; 
                tooltip.style.opacity = '0';
            });
            
            // Click handler for point info (only when enabled)
            element.addEventListener('click', (e) => {
                const enablePointClick = document.getElementById('enablePointClick');
                if (!enablePointClick || !enablePointClick.checked) {
                    return; // Exit if feature is disabled
                }
                
                // Only trigger if it was a click (not a drag)
                const deltaX = Math.abs(e.clientX - lastMouseX);
                const deltaY = Math.abs(e.clientY - lastMouseY);
                if (deltaX < 5 && deltaY < 5) {
                    const rect = element.getBoundingClientRect();
                    const x = (e.clientX - rect.left - element.width / 2 - transform.x) / transform.scale;
                    const y = (e.clientY - rect.top - element.height / 2 - transform.y) / transform.scale;
                    
                    // Rotate back to find point
                    const angle = -globalRotation * Math.PI / 180;
                    const rx = x * Math.cos(angle) - y * Math.sin(angle);
                    const ry = x * Math.sin(angle) + y * Math.cos(angle);
                    
                    let foundPoint = null;
                    let minDist = Infinity;
                    
                    pointsData.forEach(point => {
                        if (point.screenX !== undefined) {
                            const dx = rx - point.screenX;
                            const dy = ry - point.screenY;
                            const dist = Math.sqrt(dx * dx + dy * dy);
                            if (dist < point.screenRadius * 2 && dist < minDist) {
                                minDist = dist;
                                foundPoint = point;
                            }
                        }
                    });
                    
                    if (foundPoint) {
                        showPointInfo(foundPoint);
                    }
                }
            });
            
            element.addEventListener('touchstart', handleStart, { passive: true });
            element.addEventListener('touchmove', handleMove, { passive: false });
            element.addEventListener('touchend', handleEnd);
            element.addEventListener('touchcancel', () => { isDragging = false; touchStartDist = 0; });
            
            element.addEventListener('wheel', handleWheel);
        });

        function updateBridgeAnalysis() {
            // Function disabled - bridge analysis tab removed
            return;
            
            // Build correction series table
            let correctionHTML = '<table style="width: 100%; font-size: 11px; border-collapse: collapse;">';
            correctionHTML += '<tr style="border-bottom: 1px solid var(--border-color);"><th>Level</th><th>Modulus M</th><th>φ(M)</th><th>φ(M)/M</th><th>ΔT (New Opens)</th><th>Correction 𝕋</th><th>Cumulative</th></tr>';
            
            let cumulativeCorrection = 0;
            let correctionData = [];
            let phiData = [];
            
            moduli.forEach((m, idx) => {
                const phiM = phi(m);
                const ratio = phiM / m;
                phiData.push({m, ratio});
                
                const T_curr = phiM;
                const T_prev = idx === 0 ? 0 : phi(moduli[idx - 1]);
                const deltaT = T_curr - T_prev;
                const coefficient = T_curr === 0 ? 0 : deltaT / T_curr;
                cumulativeCorrection += coefficient;
                
                correctionData.push({
                    level: idx,
                    M: m,
                    phi: phiM,
                    ratio: ratio,
                    deltaT: deltaT,
                    coeff: coefficient,
                    cumul: cumulativeCorrection
                });
                
                // Show first 20 and last 5 entries if too many
                const showEntry = moduli.length <= 25 || idx < 20 || idx >= moduli.length - 5;
                
                if (showEntry) {
                    correctionHTML += `<tr style="border-bottom: 1px solid var(--border-subtle);">`;
                    correctionHTML += `<td style="padding: 5px;">${idx}</td>`;
                    correctionHTML += `<td>${m}</td>`;
                    correctionHTML += `<td>${phiM}</td>`;
                    correctionHTML += `<td>${ratio.toFixed(6)}</td>`;
                    correctionHTML += `<td>${deltaT}</td>`;
                    correctionHTML += `<td><strong>${coefficient.toFixed(6)}</strong></td>`;
                    correctionHTML += `<td>${cumulativeCorrection.toFixed(6)}</td>`;
                    correctionHTML += `</tr>`;
                } else if (idx === 20) {
                    correctionHTML += `<tr><td colspan="7" style="text-align: center; padding: 8px; font-style: italic;">... ${moduli.length - 25} more entries ...</td></tr>`;
                }
            });
            correctionHTML += '</table>';
            document.getElementById('correctionSeriesContent').innerHTML = correctionHTML;

            // Transition table - show detailed view
            let transitionHTML = '<table style="width: 100%; font-size: 11px; border-collapse: collapse;">';
            transitionHTML += '<tr style="border-bottom: 1px solid var(--border-color);"><th>Level</th><th>Modulus M</th><th>φ(M)</th><th>φ(M)/M</th><th>Error from 6/π²</th></tr>';
            
            const theoretical = 6 / (Math.PI * Math.PI);
            
            moduli.forEach((m, idx) => {
                const phiM = phi(m);
                const ratio = phiM / m;
                const error = Math.abs(ratio - theoretical);
                
                const showEntry = moduli.length <= 25 || idx < 20 || idx >= moduli.length - 5;
                
                if (showEntry) {
                    transitionHTML += `<tr style="border-bottom: 1px solid var(--border-subtle);">`;
                    transitionHTML += `<td style="padding: 5px;">${idx}</td>`;
                    transitionHTML += `<td>${m}</td>`;
                    transitionHTML += `<td>${phiM}</td>`;
                    transitionHTML += `<td>${ratio.toFixed(6)}</td>`;
                    transitionHTML += `<td>${error.toFixed(6)}</td>`;
                    transitionHTML += `</tr>`;
                } else if (idx === 20) {
                    transitionHTML += `<tr><td colspan="5" style="text-align: center; padding: 8px; font-style: italic;">... ${moduli.length - 25} more entries ...</td></tr>`;
                }
            });
            transitionHTML += '</table>';
            document.getElementById('transitionTable').innerHTML = transitionHTML;

            // Update bridge statistics
            const avgPhi = parseFloat(document.getElementById('statAvgPhi').textContent);
            const error = Math.abs(avgPhi - theoretical);
            const totalOpen = pointsData.filter(p => p.isOpen).length;
            
            document.getElementById('bridgeAvgPhi').textContent = avgPhi.toFixed(6);
            document.getElementById('bridgeError').textContent = error.toFixed(6);
            document.getElementById('bridgeLevels').textContent = moduli.length;
            document.getElementById('bridgeTransitions').textContent = totalOpen.toLocaleString();

            // Draw charts with updated data
            drawConvergenceChart(phiData, avgPhi, theoretical);
            drawCorrectionChart(correctionData);
        }

        function drawConvergenceChart(phiData, observed, theoretical) {
            const canvas = document.getElementById('convergenceChart');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const padding = 50;
            
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
            const lineColor = currentTheme === 'dark' ? '#ffffff' : '#000000';
            const gridColor = currentTheme === 'dark' ? '#333333' : '#cccccc';
            
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, width, height);
            
            if (phiData.length === 0) {
                ctx.fillStyle = lineColor;
                ctx.font = '12px Arial';
                ctx.textAlign = 'center';
                ctx.fillText('No data to display', width/2, height/2);
                return;
            }
            
            // Find min/max for scaling
            const ratios = phiData.map(d => d.ratio);
            const minRatio = Math.min(...ratios, theoretical);
            const maxRatio = Math.max(...ratios, theoretical);
            const range = maxRatio - minRatio;
            const yMin = minRatio - range * 0.1;
            const yMax = maxRatio + range * 0.1;
            const yRange = yMax - yMin;
            
            // Draw grid
            ctx.strokeStyle = gridColor;
            ctx.lineWidth = 0.5;
            for (let i = 0; i <= 5; i++) {
                const y = padding + (i / 5) * (height - 2 * padding);
                ctx.beginPath();
                ctx.moveTo(padding, y);
                ctx.lineTo(width - padding, y);
                ctx.stroke();
                
                const value = yMax - (i / 5) * yRange;
                ctx.fillStyle = lineColor;
                ctx.font = '10px Arial';
                ctx.textAlign = 'right';
                ctx.fillText(value.toFixed(4), padding - 5, y + 4);
            }
            
            // Draw axes
            ctx.strokeStyle = lineColor;
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(padding, padding);
            ctx.lineTo(padding, height - padding);
            ctx.lineTo(width - padding, height - padding);
            ctx.stroke();
            
            // Draw theoretical limit line
            ctx.strokeStyle = '#00ff00';
            ctx.lineWidth = 2;
            ctx.setLineDash([5, 5]);
            const yTheory = height - padding - ((theoretical - yMin) / yRange) * (height - 2 * padding);
            ctx.beginPath();
            ctx.moveTo(padding, yTheory);
            ctx.lineTo(width - padding, yTheory);
            ctx.stroke();
            ctx.setLineDash([]);
            
            // Plot observed convergence
            ctx.strokeStyle = '#ff0000';
            ctx.fillStyle = '#ff0000';
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            phiData.forEach((d, i) => {
                const x = padding + (i / (phiData.length - 1)) * (width - 2 * padding);
                const y = height - padding - ((d.ratio - yMin) / yRange) * (height - 2 * padding);
                
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
                
                // Draw point
                ctx.beginPath();
                ctx.arc(x, y, 3, 0, 2 * Math.PI);
                ctx.fill();
            });
            ctx.stroke();
            
            // Labels
            ctx.fillStyle = lineColor;
            ctx.font = '12px Arial';
            ctx.textAlign = 'center';
            ctx.fillText('Level Index', width / 2, height - 10);
            
            ctx.save();
            ctx.translate(15, height / 2);
            ctx.rotate(-Math.PI / 2);
            ctx.fillText('φ(M)/M', 0, 0);
            ctx.restore();
            
            ctx.fillStyle = '#00ff00';
            ctx.font = '10px Arial';
            ctx.fillText(`6/π² = ${theoretical.toFixed(6)}`, width - padding - 60, yTheory - 5);
        }

        function drawCorrectionChart(correctionData) {
            const canvas = document.getElementById('correctionChart');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const padding = 50;
            
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
            const lineColor = currentTheme === 'dark' ? '#ffffff' : '#000000';
            
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, width, height);
            
            if (correctionData.length === 0) {
                ctx.fillStyle = lineColor;
                ctx.font = '12px Arial';
                ctx.textAlign = 'center';
                ctx.fillText('No data to display', width/2, height/2);
                return;
            }
            
            // Find max coefficient for scaling
            const maxCoeff = Math.max(...correctionData.map(d => d.coeff), 1);
            
            // Draw axes
            ctx.strokeStyle = lineColor;
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(padding, padding);
            ctx.lineTo(padding, height - padding);
            ctx.lineTo(width - padding, height - padding);
            ctx.stroke();
            
            // Y-axis labels
            ctx.fillStyle = lineColor;
            ctx.font = '10px Arial';
            ctx.textAlign = 'right';
            for (let i = 0; i <= 5; i++) {
                const y = padding + (i / 5) * (height - 2 * padding);
                const value = maxCoeff * (1 - i / 5);
                ctx.fillText(value.toFixed(3), padding - 5, y + 4);
                
                // Grid line
                ctx.strokeStyle = currentTheme === 'dark' ? '#333333' : '#cccccc';
                ctx.lineWidth = 0.5;
                ctx.beginPath();
                ctx.moveTo(padding, y);
                ctx.lineTo(width - padding, y);
                ctx.stroke();
            }
            
            // Plot bars
            if (correctionData.length > 0) {
                const barWidth = Math.min((width - 2 * padding) / correctionData.length * 0.8, 30);
                
                correctionData.forEach((d, i) => {
                    const x = padding + (i + 0.5) / correctionData.length * (width - 2 * padding);
                    const barHeight = (d.coeff / maxCoeff) * (height - 2 * padding);
                    const y = height - padding - barHeight;
                    
                    // Color bars by magnitude
                    const intensity = d.coeff / maxCoeff;
                    const r = Math.round(255 * intensity);
                    const b = Math.round(255 * (1 - intensity));
                    ctx.fillStyle = `rgb(${r}, 100, ${b})`;
                    
                    ctx.fillRect(x - barWidth / 2, y, barWidth, barHeight);
                    
                    // Border
                    ctx.strokeStyle = lineColor;
                    ctx.lineWidth = 0.5;
                    ctx.strokeRect(x - barWidth / 2, y, barWidth, barHeight);
                });
            }
            
            // Labels
            ctx.fillStyle = lineColor;
            ctx.font = '12px Arial';
            ctx.textAlign = 'center';
            ctx.fillText('Level Index', width / 2, height - 10);
            
            ctx.save();
            ctx.translate(15, height / 2);
            ctx.rotate(-Math.PI / 2);
            ctx.fillText('Correction 𝕋₂ₙ', 0, 0);
            ctx.restore();
        }

        function updateVisualization() {
            if (isComputing) {
                alert('Computation already in progress. Please wait...');
                return;
            }
            generatePointsData();
            if (!isComputing) {
                if (currentRenderer === 'canvas2d') {
                    drawVisualization();
                } else if (currentRenderer === 'webgl') {
                    drawVisualizationWebGL();
                } else if (currentRenderer === 'svg') {
                    drawVisualizationSVG();
                }
            }
        }

        function setPreset(n) {
            document.getElementById('modSelectionMode').value = 'M30-sequence';
            document.getElementById('sequenceInputs').style.display = 'block';
            document.getElementById('rangeInputs').style.display = 'none';
            document.getElementById('customInputs').style.display = 'none';
            document.getElementById('sequenceTerms').value = n + 1;
            
            document.getElementById('enableConnections').checked = true;
            document.getElementById('connectionMode').value = 'double-lift';
            document.getElementById('displayMode').value = 'rings';
            document.getElementById('showOpen').checked = true;
            document.getElementById('showClosed').checked = false;
            
            updateVisualization();
        }

        function setPresetRange() {
            document.getElementById('modSelectionMode').value = 'M30-sequence';
            document.getElementById('sequenceInputs').style.display = 'block';
            document.getElementById('rangeInputs').style.display = 'none';
            document.getElementById('customInputs').style.display = 'none';
            document.getElementById('sequenceTerms').value = 6;
            
            document.getElementById('enableConnections').checked = true;
            document.getElementById('connectionMode').value = 'binary-lift';
            document.getElementById('displayMode').value = 'rings';
            
            updateVisualization();
        }

        function exportImage() {
            const includeLegend = document.getElementById('includeLegend').checked;
            const includeColorKey = document.getElementById('includeColorKey').checked;
            const includeTimestamp = document.getElementById('includeTimestamp').checked;
            const exportTitle = document.getElementById('exportTitle').value;
            const resolution = parseFloat(document.getElementById('exportResolution').value);
            
            // Create temporary canvas at higher resolution
            const tempCanvas = document.createElement('canvas');
            const baseWidth = canvas.width;
            const baseHeight = canvas.height;
            
            // Reserve space for title at top
            const titleHeight = 100 * resolution;
            
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution + titleHeight;
            
            // Calculate legend dimensions - always on right
            let legendWidth = 0;
            
            if (includeLegend) {
                legendWidth = 500 * resolution; // Increased width for more details
                exportWidth += legendWidth;
            }
            
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Fill background
            const bgColor = '#000000';
            const textColor = '#ffffff';
            tempCtx.fillStyle = bgColor;
            tempCtx.fillRect(0, 0, exportWidth, exportHeight);
            
            // Draw title at top center
            const fontSize = 18 * resolution;
            tempCtx.fillStyle = textColor;
            tempCtx.font = `bold ${fontSize * 1.8}px Arial`;
            tempCtx.textAlign = 'center';
            const titleY = titleHeight / 2 + fontSize / 2;
            tempCtx.fillText(exportTitle, exportWidth / 2, titleY);
            
            // Draw timestamp if enabled
            if (includeTimestamp) {
                tempCtx.font = `${fontSize * 0.8}px Arial`;
                const timestamp = new Date().toLocaleString();
                tempCtx.fillText(timestamp, exportWidth / 2, titleY + fontSize * 1.5);
            }
            
            // Draw main visualization scaled up below title
            tempCtx.save();
            tempCtx.translate(0, titleHeight);
            tempCtx.scale(resolution, resolution);
            tempCtx.drawImage(canvas, 0, 0);
            tempCtx.restore();
            
            // Draw legend if enabled
            if (includeLegend) {
                drawLegend(tempCtx, legendWidth, exportWidth, exportHeight, resolution, textColor, bgColor, titleHeight, includeColorKey);
            }
            
            // Export
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `modular_rings_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, bgColor, titleHeight, includeColorKey) {
            const moduli = getSelectedModuli();
            const mode = document.getElementById('modSelectionMode').value;
            const displayMode = document.getElementById('displayMode').value;
            const angularMapping = document.getElementById('angularMapping').value;
            const showOpen = document.getElementById('showOpen').checked;
            const showClosed = document.getElementById('showClosed').checked;
            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const gapValues = document.getElementById('gapValues').value;
            const enableTracker = document.getElementById('enableTracker').checked;
            const trackedResidues = document.getElementById('trackedResidues').value;
            const invertOrder = document.getElementById('invertModOrder').checked;
            const enableConnections = document.getElementById('enableConnections').checked;
            const connectionMode = document.getElementById('connectionMode').value;
            const showLabels = document.getElementById('showLabels').checked;
            const labelType = document.getElementById('labelType').value;
            const openColorMode = document.getElementById('openColorMode').value;
            const closedColorMode = document.getElementById('closedColorMode').value;
            
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const sectionSpacing = 15 * resolution;
            
            // Legend is always on the right
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            // Start legend content below title area
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            
            // Helper function to draw section header
            function drawSectionHeader(title) {
                ctx.font = `bold ${fontSize * 1.1}px Arial`;
                ctx.fillStyle = textColor;
                ctx.fillText(title, startX, y);
                y += lineHeight * 0.3;
                
                // Draw separator line
                ctx.strokeStyle = textColor;
                ctx.lineWidth = 1.5 * resolution;
                ctx.beginPath();
                ctx.moveTo(startX, y);
                ctx.lineTo(startX + maxWidth * 0.9, y);
                ctx.stroke();
                y += lineHeight * 0.8;
            }
            
            // Helper function to draw text with wrapping
            function drawWrappedText(text, maxLineWidth) {
                ctx.font = `${fontSize}px Arial`;
                const words = text.split(' ');
                let line = '';
                
                for (let i = 0; i < words.length; i++) {
                    const testLine = line + words[i] + ' ';
                    const metrics = ctx.measureText(testLine);
                    
                    if (metrics.width > maxLineWidth && line !== '') {
                        ctx.fillText(line, startX, y);
                        y += lineHeight;
                        line = words[i] + ' ';
                    } else {
                        line = testLine;
                    }
                }
                ctx.fillText(line, startX, y);
                y += lineHeight;
            }
            
            // === CONFIGURATION SECTION ===
            drawSectionHeader('CONFIGURATION');
            
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            
            // Modulus configuration
            let moduliText = '';
            if (mode === 'range') {
                const modMin = document.getElementById('modMin').value;
                const modMax = document.getElementById('modMax').value;
                const modStep = document.getElementById('modStep').value;
                moduliText = `Moduli: Range ${modMin} to ${modMax} (step ${modStep})`;
            } else if (mode === 'fibonacci') {
                moduliText = `Moduli: Fibonacci sequence (max ${document.getElementById('sequenceMax').value})`;
            } else if (mode === 'primes') {
                moduliText = `Moduli: Prime sequence (max ${document.getElementById('sequenceMax').value})`;
            } else if (mode === 'powers-of-2') {
                moduliText = `Moduli: Powers of 2 (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'powers-of-3') {
                moduliText = `Moduli: Powers of 3 (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'M30-sequence') {
                moduliText = `Moduli: M₃₀ = 30×2ⁿ (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'custom') {
                const customMods = document.getElementById('customModuli').value;
                moduliText = `Moduli: Custom [${customMods}]`;
            }
            
            drawWrappedText(moduliText, maxWidth * 0.95);
            
            ctx.fillText(`Total Moduli Count: ${moduli.length}`, startX, y);
            y += lineHeight;
            
            const displayText = displayMode === 'rings' ? 'Concentric Rings' : 'Unit Circle';
            ctx.fillText(`Display Mode: ${displayText}`, startX, y);
            y += lineHeight;
            
            if (invertOrder) {
                ctx.fillText(`Ring Order: Inverted (Outer↔Inner)`, startX, y);
                y += lineHeight;
            }
            
            const angularText = angularMapping === 'standard' ? '2πr/m' :
                               angularMapping === 'half' ? 'πr/m' :
                               angularMapping === 'inverted' ? '2π(m-r)/m' : '-2πr/m';
            ctx.fillText(`Angular Mapping: ${angularText}`, startX, y);
            y += lineHeight;
            
            const channelText = showOpen && showClosed ? 'Open & Closed' : showOpen ? 'Open Only' : 'Closed Only';
            ctx.fillText(`Visible Channels: ${channelText}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // === COLOR SCHEME SECTION ===
            drawSectionHeader('COLOR SCHEME');
            
            ctx.font = `${fontSize}px Arial`;
            const openModeText = openColorMode === 'solid' ? 'Solid Color' :
                                openColorMode === 'by-residue' ? 'By Residue (r)' :
                                openColorMode === 'by-modulus' ? 'By Modulus (m)' :
                                openColorMode === 'by-spf' ? 'By Smallest Prime Factor' :
                                'By Angle';
            ctx.fillText(`Open Channels: ${openModeText}`, startX, y);
            y += lineHeight;
            
            const closedModeText = closedColorMode === 'solid' ? 'Solid Color' :
                                  closedColorMode === 'by-gcd' ? 'By GCD Value' :
                                  'By Prime Factor';
            ctx.fillText(`Closed Channels: ${closedModeText}`, startX, y);
            y += lineHeight;
            
            if (includeColorKey && openColorMode !== 'solid') {
                ctx.font = `${fontSize * 0.85}px Arial`;
                ctx.fillStyle = textColor;
                ctx.globalAlpha = 0.7;
                ctx.fillText('(See visualization for color mapping)', startX, y);
                ctx.globalAlpha = 1.0;
                y += lineHeight;
            }
            
            y += sectionSpacing;
            
            // === FEATURES SECTION ===
            drawSectionHeader('ACTIVE FEATURES');
            
            ctx.font = `${fontSize}px Arial`;
            
            if (showLabels) {
                const labelTypeText = labelType === 'residue' ? 'Residue (r)' :
                                     labelType === 'farey' ? 'Farey Fraction (r/m)' :
                                     labelType === 'theta' ? 'Angle θ (degrees)' :
                                     labelType === 'gcd' ? 'GCD(r,m)' : labelType;
                ctx.fillText(`Labels: ${labelTypeText}`, startX, y);
                y += lineHeight;
            }
            
            if (enableGap) {
                ctx.fillText(`Gap Analysis: Gaps = [${gapValues}]`, startX, y);
                y += lineHeight;
                
                const gaps = gapValues.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g));
                if (gaps.length > 0) {
                    ctx.font = `${fontSize * 0.85}px Arial`;
                    ctx.fillStyle = textColor;
                    ctx.globalAlpha = 0.8;
                    gaps.forEach((gap, idx) => {
                        const gapName = gap === 2 ? 'Twin' : gap === 4 ? 'Cousin' : gap === 6 ? 'Sexy' : `Gap-${gap}`;
                        ctx.fillText(`  • ${gapName} (g=${gap})`, startX, y);
                        y += lineHeight * 0.9;
                    });
                    ctx.globalAlpha = 1.0;
                    ctx.font = `${fontSize}px Arial`;
                }
            }
            
            if (enableTracker) {
                ctx.fillText(`Residue Tracker: r = [${trackedResidues}]`, startX, y);
                y += lineHeight;
                
                const trackerMod = document.getElementById('trackerModFilter').value;
                if (trackerMod) {
                    ctx.fillText(`  Filter: m = ${trackerMod}`, startX, y);
                    y += lineHeight;
                }
            }
            
            if (enableConnections) {
                const connModeText = connectionMode === 'next-mod' ? 'r to r (Next Modulus)' :
                                     connectionMode === 'binary-lift' ? 'Binary Lift (r to r+M)' :
                                     connectionMode === 'double-lift' ? 'r to r+M×2ⁿ' :
                                     connectionMode === 'same-mod' ? 'Same Modulus' :
                                     connectionMode === 'specific-mod' ? 'Specific Modulus' : 'None';
                ctx.fillText(`Connections: ${connModeText}`, startX, y);
                y += lineHeight;
            }
            
            const globalSpeed = document.getElementById('globalSpeed').value;
            const modSpeed = document.getElementById('modRotSpeed').value;
            if (parseFloat(globalSpeed) > 0 || parseFloat(modSpeed) > 0) {
                ctx.fillText(`Rotation: Global=${globalSpeed}°, Mod=${modSpeed}°`, startX, y);
                y += lineHeight;
            }
            
            y += sectionSpacing;
            
            // === STATISTICS SECTION ===
            drawSectionHeader('STATISTICS');
            
            ctx.font = `${fontSize}px Arial`;
            const totalPoints = document.getElementById('statTotal').textContent;
            const openCount = document.getElementById('statOpen').textContent;
            const closedCount = document.getElementById('statClosed').textContent;
            const openRatio = document.getElementById('statRatio').textContent;
            const avgPhi = document.getElementById('statAvgPhi').textContent;
            
            ctx.fillText(`Total Points: ${totalPoints}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Open Channels: ${openCount}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Closed Channels: ${closedCount}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Open Ratio: ${openRatio}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Avg φ(m)/m: ${avgPhi}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Theoretical Limit: 0.6079 (6/π²)`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // === METADATA SECTION ===
            drawSectionHeader('METADATA');
            
            ctx.font = `${fontSize * 0.9}px Arial`;
            ctx.fillStyle = textColor;
            const date = new Date().toLocaleString();
            ctx.fillText(`Generated: ${date}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Author: Wessen Getachew`, startX, y);
            y += lineHeight;
            ctx.fillText(`Tool: Modular Rings Visualization`, startX, y);
            y += lineHeight;
            const resText = document.getElementById('exportResolution').selectedOptions[0].text;
            ctx.fillText(`Resolution: ${resText}`, startX, y);
        }

        function resetSettings() {
            document.getElementById('modMin').value = '1';
            document.getElementById('modMax').value = '60';
            document.getElementById('modStep').value = '1';
            document.getElementById('globalSpeed').value = '0';
            document.getElementById('modRotSpeed').value = '0';
            document.getElementById('enableTracker').checked = false;
            document.getElementById('enableConnections').checked = false;
            document.getElementById('bgColor').value = '#000000';
            globalRotation = 0;
            modRotations = {};
            transform = { x: 0, y: 0, scale: 1 };
            stopAnimation();
            updateVisualization();
        }

        function exportCSV() {
            const csvMode = document.getElementById('csvExportMode').value;
            const includeHeader = document.getElementById('csvIncludeHeader').checked;
            const includeMetadata = document.getElementById('csvIncludeMetadata').checked;
            
            let csv = '';
            
            // Add metadata as comments if requested
            if (includeMetadata) {
                csv += `# Modular Rings Data Export\n`;
                csv += `# Generated: ${new Date().toLocaleString()}\n`;
                csv += `# Author: Wessen Getachew\n`;
                csv += `# Total Points: ${pointsData.length}\n`;
                
                const moduli = getSelectedModuli();
                const mode = document.getElementById('modSelectionMode').value;
                csv += `# Modulus Mode: ${mode}\n`;
                csv += `# Moduli Count: ${moduli.length}\n`;
                
                if (moduli.length <= 20) {
                    csv += `# Moduli: ${moduli.join(', ')}\n`;
                } else {
                    csv += `# Moduli: ${moduli[0]} to ${moduli[moduli.length-1]}\n`;
                }
                
                csv += `# Display Mode: ${document.getElementById('displayMode').value}\n`;
                csv += `# Angular Mapping: ${document.getElementById('angularMapping').value}\n`;
                
                const enableGap = document.getElementById('enableGapAnalysis').checked;
                if (enableGap) {
                    csv += `# Gap Analysis: ${document.getElementById('gapValues').value}\n`;
                }
                
                csv += `#\n`;
            }
            
            if (csvMode === 'basic') {
                if (includeHeader) {
                    csv += 'Modulus,Residue,GCD,Channel\n';
                }
                pointsData.forEach(p => {
                    csv += `${p.m},${p.r},${p.gcd},${p.isOpen ? 'Open' : 'Closed'}\n`;
                });
            } else if (csvMode === 'detailed') {
                if (includeHeader) {
                    csv += 'Modulus,Residue,GCD,Channel,Angle_Radians,Angle_Degrees,';
                    csv += 'Farey_Fraction,Reduced_Numerator,Reduced_Denominator,';
                    csv += 'Phi_m,Totient_Ratio,Admissible,Admissible_Gaps,';
                    csv += 'Is_Prime_Residue,Smallest_Prime_Factor,Largest_Prime_Factor\n';
                }
                pointsData.forEach(p => {
                    const [redNum, redDen] = reduceFraction(p.r, p.m);
                    const totientRatio = (p.phiM / p.m).toFixed(6);
                    const isPrimeRes = isPrime(p.r);
                    const spf = p.r === 0 ? 0 : smallestPrimeFactor(p.r);
                    const lpf = p.r === 0 ? 0 : largestPrimeFactor(p.r);
                    const admGaps = p.admissibleGaps ? p.admissibleGaps.join(';') : '';
                    
                    csv += `${p.m},${p.r},${p.gcd},${p.isOpen ? 'Open' : 'Closed'},`;
                    csv += `${p.angle.toFixed(6)},${(p.angle * 180 / Math.PI).toFixed(4)},`;
                    csv += `${p.r}/${p.m},${redNum},${redDen},`;
                    csv += `${p.phiM},${totientRatio},`;
                    csv += `${p.isAdmissible ? 'Yes' : 'No'},"${admGaps}",`;
                    csv += `${isPrimeRes ? 'Yes' : 'No'},${spf},${lpf}\n`;
                });
            } else if (csvMode === 'statistical') {
                if (includeHeader) {
                    csv += 'Modulus,Phi_m,Totient_Ratio,Open_Count,Closed_Count,';
                    csv += 'Open_Percentage,Admissible_Count,Admissible_Percentage\n';
                }
                
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
                moduli.forEach(m => {
                    const pointsInMod = pointsData.filter(p => p.m === m);
                    const openCount = pointsInMod.filter(p => p.isOpen).length;
                    const closedCount = pointsInMod.length - openCount;
                    const admissibleCount = pointsInMod.filter(p => p.isAdmissible).length;
                    const phiM = pointsInMod[0].phiM;
                    const totientRatio = (phiM / m).toFixed(6);
                    const openPct = ((openCount / pointsInMod.length) * 100).toFixed(2);
                    const admPct = ((admissibleCount / pointsInMod.length) * 100).toFixed(2);
                    
                    csv += `${m},${phiM},${totientRatio},${openCount},${closedCount},`;
                    csv += `${openPct},${admissibleCount},${admPct}\n`;
                });
            } else if (csvMode === 'gap-analysis') {
                const enableGap = document.getElementById('enableGapAnalysis').checked;
                if (!enableGap) {
                    alert('Gap Analysis must be enabled to export gap analysis data!');
                    return;
                }
                
                if (includeHeader) {
                    csv += 'Modulus,Residue,Is_Open,Is_Admissible,Admissible_Gaps,';
                    csv += 'Gap_Partners\n';
                }
                
                pointsData.forEach(p => {
                    if (!p.isOpen) return; // Only export open channels for gap analysis
                    
                    const admGaps = p.admissibleGaps ? p.admissibleGaps.join(';') : '';
                    
                    // Find gap partners
                    let gapPartners = [];
                    if (p.admissibleGaps && p.admissibleGaps.length > 0) {
                        p.admissibleGaps.forEach(gap => {
                            const partnerR = (p.r + gap) % p.m;
                            gapPartners.push(`${gap}:${partnerR}`);
                        });
                    }
                    const partnersStr = gapPartners.join(';');
                    
                    csv += `${p.m},${p.r},Yes,${p.isAdmissible ? 'Yes' : 'No'},"${admGaps}","${partnersStr}"\n`;
                });
            }
            
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `modular_rings_${csvMode}_${timestamp}.csv`;
            link.href = url;
            link.click();
            URL.revokeObjectURL(url);
        }

        function centerAndFit() {
            // Reset transform
            transform = { x: 0, y: 0, scale: 1 };
            
            // Auto-fit to canvas based on the actual moduli range
            if (pointsData.length > 0) {
                const moduli = [...new Set(pointsData.map(p => p.m))];
                const maxMod = Math.max(...moduli);
                const minMod = Math.min(...moduli);
                
                const canvasSize = Math.min(canvas.width, canvas.height);
                const maxRadius = canvasSize * 0.4;
                const dataRadius = maxMod * (maxRadius / maxMod);
                
                // Calculate optimal scale to fit with some padding
                const padding = 0.9; // 90% of canvas size
                transform.scale = (canvasSize / 2 * padding) / (maxMod * (maxRadius / maxMod));
                
                // Ensure minimum scale
                transform.scale = Math.max(0.5, Math.min(2, transform.scale));
            }
            
            drawVisualization();
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            if (tab === 'visualization') {
                document.querySelectorAll('.tab')[0].classList.add('active');
                document.getElementById('visualizationTab').classList.add('active');
            } else if (tab === 'understanding') {
                document.querySelectorAll('.tab')[1].classList.add('active');
                document.getElementById('understandingTab').classList.add('active');
            } else if (tab === 'composite-projection') {
                document.querySelectorAll('.tab')[2].classList.add('active');
                document.getElementById('compositeProjectionTab').classList.add('active');
                updateCompositeVisualization();
            }
        }

        window.addEventListener('load', () => {
            initializeTheme();
            updateRangeDisplays();
            updateGapColorPickers();
            updateVisualization();
            initCompositeProjection();
        });

        // ===== COMPOSITE PROJECTION COROLLARY =====
        let compositeModulus = 12;
        let projectionMode = 'lines'; // 'lines' or 'ring'
        let compositePoints = [];
        let compositeZoom = 1;
        let compositePan = {x: 0, y: 0};

        function initCompositeProjection() {
            const slider = document.getElementById('compModSlider');
            const input = document.getElementById('compModInput');
            const opacitySlider = document.getElementById('projOpacitySlider');
            const pointSizeSlider = document.getElementById('compPointSize');
            const colorScheme = document.getElementById('compColorScheme');
            const canvas = document.getElementById('compositeCanvas');
            const tooltip = document.getElementById('compositeTooltip');
            
            slider.addEventListener('input', () => {
                compositeModulus = parseInt(slider.value);
                input.value = compositeModulus;
                document.getElementById('compModDisplay').textContent = compositeModulus;
                updateCompositeVisualization();
            });
            
            input.addEventListener('input', () => {
                let val = parseInt(input.value);
                if (!isNaN(val) && val >= 2 && val <= 5000) {
                    compositeModulus = val;
                    slider.value = Math.min(val, 2000);
                    document.getElementById('compModDisplay').textContent = compositeModulus;
                    updateCompositeVisualization();
                }
            });
            
            opacitySlider.addEventListener('input', () => {
                document.getElementById('projOpacityDisplay').textContent = 
                    parseFloat(opacitySlider.value).toFixed(2);
                drawCompositeVisualization();
            });
            
            pointSizeSlider.addEventListener('input', () => {
                document.getElementById('compPointSizeDisplay').textContent = 
                    parseFloat(pointSizeSlider.value).toFixed(1);
                drawCompositeVisualization();
            });
            
            colorScheme.addEventListener('change', () => {
                drawCompositeVisualization();
            });
            
            document.getElementById('showChannelLabels').addEventListener('change', () => {
                drawCompositeVisualization();
            });
            
            document.getElementById('showMultiplicityInfo').addEventListener('change', () => {
                drawCompositeVisualization();
            });
            
            // Mouse wheel zoom
            canvas.addEventListener('wheel', (e) => {
                e.preventDefault();
                const delta = e.deltaY > 0 ? 0.9 : 1.1;
                compositeZoom *= delta;
                compositeZoom = Math.max(0.5, Math.min(10, compositeZoom));
                drawCompositeVisualization();
            });
            
            // Click handler
            canvas.addEventListener('click', (e) => {
                const enablePointClick = document.getElementById('enablePointClick');
                if (enablePointClick && enablePointClick.checked) {
                    const rect = canvas.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    handleCompositeClick(x, y);
                }
            });
            
            // Hover tooltip
            canvas.addEventListener('mousemove', (e) => {
                const rect = canvas.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                handleCompositeHover(x, y, e);
            });
            
            canvas.addEventListener('mouseleave', () => {
                tooltip.style.opacity = '0';
            });
            
            updateCompositeVisualization();
        }

        function setCompositeMod(m) {
            compositeModulus = m;
            document.getElementById('compModSlider').value = Math.min(m, 2000);
            document.getElementById('compModInput').value = m;
            document.getElementById('compModDisplay').textContent = m;
            updateCompositeVisualization();
        }

        function setProjectionMode(mode) {
            projectionMode = mode;
            
            const linesBtn = document.getElementById('projLinesBtn');
            const ringBtn = document.getElementById('ringViewBtn');
            
            if (mode === 'lines') {
                linesBtn.style.background = 'var(--hover-bg)';
                linesBtn.style.color = 'var(--hover-text)';
                ringBtn.style.background = 'var(--bg-primary)';
                ringBtn.style.color = 'var(--text-primary)';
            } else {
                ringBtn.style.background = 'var(--hover-bg)';
                ringBtn.style.color = 'var(--hover-text)';
                linesBtn.style.background = 'var(--bg-primary)';
                linesBtn.style.color = 'var(--text-primary)';
            }
            
            drawCompositeVisualization();
        }

        function updateCompositeVisualization() {
            const M = compositeModulus;
            
            // Calculate statistics
            const phiM = phi(M);
            const reducible = M - phiM;
            const ratio = ((M - phiM) / M * 100).toFixed(1);
            
            // Find all divisors (channels)
            const channels = [];
            for (let d = 1; d < M; d++) {
                if (M % d === 0) {
                    channels.push(d);
                }
            }
            
            // Get prime factorization
            const factorization = primeFactorization(M);
            
            // Get all divisors including M
            const allDivisors = [];
            for (let d = 1; d <= M; d++) {
                if (M % d === 0) {
                    allDivisors.push(d);
                }
            }
            const divisorText = allDivisors.length <= 10 ? allDivisors.join(',') : 
                                `${allDivisors.slice(0, 8).join(',')}... (${allDivisors.length} total)`;
            
            // Update display
            document.getElementById('compPhi').textContent = phiM;
            document.getElementById('compReducible').textContent = reducible;
            document.getElementById('compRatio').textContent = ratio + '%';
            document.getElementById('compChannels').textContent = channels.length;
            document.getElementById('compPrimeFactors').textContent = factorization;
            document.getElementById('compDivisors').textContent = divisorText;
            
            // Update analysis text
            let analysisHTML = `<p style="margin-bottom: 12px;"><strong>M = ${M} = ${factorization}</strong></p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">This composite modulus has <strong>${phiM} coprime residues</strong> (φ(${M}) = ${phiM}) and <strong>${reducible} reducible residues</strong>.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">The reducible residues project onto <strong>${channels.length} distinct Farey channels</strong> with denominators: ${channels.join(', ')}.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;"><strong>Channel multiplicities:</strong> Each channel M' receives exactly d = M/M' residues.</p>`;
            analysisHTML += `<ul style="margin-left: 25px; margin-bottom: 12px;">`;
            
            // Show first few channel multiplicities
            const showChannels = channels.slice(0, Math.min(8, channels.length));
            showChannels.forEach(ch => {
                const mult = M / ch;
                analysisHTML += `<li>Channel M'=${ch}: ${M}/${ch} = ${mult} residue${mult > 1 ? 's' : ''}</li>`;
            });
            if (channels.length > 8) {
                analysisHTML += `<li>... and ${channels.length - 8} more channels</li>`;
            }
            analysisHTML += `</ul>`;
            analysisHTML += `<p>The <strong>reducibility ratio</strong> is ${ratio}%, meaning ${ratio}% of all residues mod ${M} share a common factor with ${M}.</p>`;
            
            document.getElementById('compAnalysisText').innerHTML = analysisHTML;
            
            // Generate points data
            compositePoints = [];
            for (let r = 0; r < M; r++) {
                const g = gcd(r, M);
                const isOpen = g === 1;
                
                let reducedR = r;
                let reducedM = M;
                if (g > 1) {
                    reducedR = r / g;
                    reducedM = M / g;
                }
                
                const angle = -2 * Math.PI * r / M;
                const spf = r === 0 ? 0 : smallestPrimeFactor(r);
                const lpf = r === 0 ? 0 : largestPrimeFactor(r);
                
                compositePoints.push({
                    r: r,
                    M: M,
                    gcd: g,
                    isOpen: isOpen,
                    angle: angle,
                    reducedR: reducedR,
                    reducedM: reducedM,
                    spf: spf,
                    lpf: lpf
                });
            }
            
            drawCompositeVisualization();
        }

        function drawCompositeVisualization() {
            const canvas = document.getElementById('compositeCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2 + compositePan.x;
            const centerY = height / 2 + compositePan.y;
            const baseRadius = Math.min(width, height) * 0.42;
            const maxRadius = baseRadius * compositeZoom;
            
            // Clear
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            const M = compositeModulus;
            const opacity = parseFloat(document.getElementById('projOpacitySlider').value);
            const pointSize = parseFloat(document.getElementById('compPointSize').value);
            const colorScheme = document.getElementById('compColorScheme').value;
            const showLabels = document.getElementById('showChannelLabels').checked;
            const showMultiplicity = document.getElementById('showMultiplicityInfo').checked;
            
            // Get color for point based on scheme
            function getPointColor(point) {
                if (colorScheme === 'channel-type') {
                    return point.isOpen ? '#00ffff' : '#ff0064';
                } else if (colorScheme === 'spf') {
                    if (point.r === 0) return '#666666';
                    const primeColors = {2: '#ff0000', 3: '#00ff00', 5: '#0000ff', 7: '#ffff00', 
                                        11: '#ff00ff', 13: '#00ffff', 17: '#ff8800', 19: '#8800ff'};
                    return primeColors[point.spf] || '#ffffff';
                } else if (colorScheme === 'lpf') {
                    if (point.r === 0) return '#666666';
                    const primeColors = {2: '#ff0000', 3: '#00ff00', 5: '#0000ff', 7: '#ffff00', 
                                        11: '#ff00ff', 13: '#00ffff', 17: '#ff8800', 19: '#8800ff'};
                    return primeColors[point.lpf] || '#ffffff';
                } else if (colorScheme === 'gcd-value') {
                    if (point.gcd === 1) return '#00ffff';
                    const hue = (point.gcd * 40) % 360;
                    return `hsl(${hue}, 100%, 50%)`;
                } else if (colorScheme === 'channel-depth') {
                    if (point.isOpen) return '#00ffff';
                    const hue = (point.reducedM / M) * 240; // Blue to red spectrum
                    return `hsl(${hue}, 80%, 50%)`;
                }
                return '#ffffff';
            }
            
            ctx.save();
            ctx.translate(centerX, centerY);
            ctx.scale(compositeZoom, compositeZoom);
            
            if (projectionMode === 'lines') {
                // Draw projection lines mode
                
                // Find all unique target moduli
                const targetModuli = new Set();
                compositePoints.forEach(p => {
                    if (!p.isOpen) {
                        targetModuli.add(p.reducedM);
                    }
                });
                const sortedTargets = Array.from(targetModuli).sort((a, b) => a - b);
                
                // Draw Farey channel rings (gold)
                ctx.strokeStyle = '#ffc800';
                ctx.lineWidth = 2 / compositeZoom;
                sortedTargets.forEach(m => {
                    const radius = (m / M) * baseRadius;
                    ctx.beginPath();
                    ctx.arc(0, 0, radius, 0, 2 * Math.PI);
                    ctx.stroke();
                    
                    // Label the channel
                    if (showLabels) {
                        ctx.fillStyle = '#ffc800';
                        ctx.font = `${11 / compositeZoom}px Arial`;
                        ctx.textAlign = 'center';
                        ctx.fillText(`M' = ${m}`, 0, -radius - 8 / compositeZoom);
                        
                        // Show multiplicity
                        if (showMultiplicity) {
                            const mult = M / m;
                            ctx.font = `${9 / compositeZoom}px Arial`;
                            ctx.fillText(`(d = ${mult})`, 0, -radius - 20 / compositeZoom);
                        }
                    }
                });
                
                // Draw outer ring for M
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 2.5 / compositeZoom;
                ctx.beginPath();
                ctx.arc(0, 0, baseRadius, 0, 2 * Math.PI);
                ctx.stroke();
                
                // Draw projection lines first (so points appear on top)
                ctx.strokeStyle = `rgba(255, 0, 100, ${opacity})`;
                ctx.lineWidth = 1 / compositeZoom;
                
                compositePoints.forEach(point => {
                    if (!point.isOpen && point.reducedM < M) {
                        // Draw line from outer point to inner reduced point
                        const outerX = baseRadius * Math.cos(point.angle);
                        const outerY = baseRadius * Math.sin(point.angle);
                        
                        const innerRadius = (point.reducedM / M) * baseRadius;
                        const reducedAngle = -2 * Math.PI * point.reducedR / point.reducedM;
                        const innerX = innerRadius * Math.cos(reducedAngle);
                        const innerY = innerRadius * Math.sin(reducedAngle);
                        
                        ctx.beginPath();
                        ctx.moveTo(outerX, outerY);
                        ctx.lineTo(innerX, innerY);
                        ctx.stroke();
                    }
                });
                
                // Draw points on outer ring
                compositePoints.forEach(point => {
                    const x = baseRadius * Math.cos(point.angle);
                    const y = baseRadius * Math.sin(point.angle);
                    
                    const color = getPointColor(point);
                    const size = point.isOpen ? pointSize : pointSize * 1.1;
                    
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, size / compositeZoom, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    // Store screen coordinates for hover detection
                    point.screenX = centerX + x * compositeZoom;
                    point.screenY = centerY + y * compositeZoom;
                    point.screenRadius = size;
                });
                
                // Draw target points on inner rings
                compositePoints.forEach(point => {
                    if (!point.isOpen && point.reducedM < M) {
                        const innerRadius = (point.reducedM / M) * baseRadius;
                        const reducedAngle = -2 * Math.PI * point.reducedR / point.reducedM;
                        const x = innerRadius * Math.cos(reducedAngle);
                        const y = innerRadius * Math.sin(reducedAngle);
                        
                        ctx.fillStyle = '#ffc800';
                        ctx.beginPath();
                        ctx.arc(x, y, 4 / compositeZoom, 0, 2 * Math.PI);
                        ctx.fill();
                    }
                });
                
            } else {
                // Ring view mode - show all rings including reduced ones
                
                // Collect all unique moduli
                const allModuli = new Set([M]);
                compositePoints.forEach(p => {
                    if (!p.isOpen) {
                        allModuli.add(p.reducedM);
                    }
                });
                const sortedModuli = Array.from(allModuli).sort((a, b) => a - b);
                
                // Draw rings
                sortedModuli.forEach(m => {
                    const radius = (m / M) * baseRadius;
                    
                    ctx.strokeStyle = m === M ? '#ffffff' : 'rgba(255, 200, 0, 0.3)';
                    ctx.lineWidth = m === M ? 2.5 / compositeZoom : 1.5 / compositeZoom;
                    ctx.beginPath();
                    ctx.arc(0, 0, radius, 0, 2 * Math.PI);
                    ctx.stroke();
                    
                    // Draw points for this modulus
                    for (let r = 0; r < m; r++) {
                        const angle = -2 * Math.PI * r / m;
                        const x = radius * Math.cos(angle);
                        const y = radius * Math.sin(angle);
                        
                        const g = gcd(r, m);
                        const isOpen = g === 1;
                        
                        if (m === M) {
                            const point = compositePoints.find(p => p.r === r);
                            const color = point ? getPointColor(point) : (isOpen ? '#00ffff' : '#ff0064');
                            const size = isOpen ? pointSize : pointSize * 1.1;
                            
                            ctx.fillStyle = color;
                            ctx.beginPath();
                            ctx.arc(x, y, size / compositeZoom, 0, 2 * Math.PI);
                            ctx.fill();
                            
                            if (point) {
                                point.screenX = centerX + x * compositeZoom;
                                point.screenY = centerY + y * compositeZoom;
                                point.screenRadius = size;
                            }
                        } else {
                            ctx.fillStyle = isOpen ? 'rgba(0, 255, 255, 0.4)' : 'rgba(255, 200, 0, 0.6)';
                            ctx.beginPath();
                            ctx.arc(x, y, 3 / compositeZoom, 0, 2 * Math.PI);
                            ctx.fill();
                        }
                    }
                    
                    // Label
                    if (m < M && showLabels) {
                        ctx.fillStyle = '#ffc800';
                        ctx.font = `${11 / compositeZoom}px Arial`;
                        ctx.textAlign = 'center';
                        ctx.fillText(`${m}`, 0, -radius - 5 / compositeZoom);
                    }
                });
            }
            
            ctx.restore();
            
            // Draw center dot
            ctx.fillStyle = '#ffffff';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 3, 0, 2 * Math.PI);
            ctx.fill();
            
            // Title
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 18px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`Composite Modulus M = ${M}`, width / 2, 30);
            
            // Zoom indicator
            ctx.font = '11px Arial';
            ctx.textAlign = 'right';
            ctx.fillText(`Zoom: ${(compositeZoom * 100).toFixed(0)}%`, width - 10, height - 10);
        }

        function handleCompositeHover(x, y, e) {
            const tooltip = document.getElementById('compositeTooltip');
            
            // Find hovered point
            let hoveredPoint = null;
            let minDist = Infinity;
            
            compositePoints.forEach(point => {
                if (point.screenX !== undefined) {
                    const dx = x - point.screenX;
                    const dy = y - point.screenY;
                    const dist = Math.sqrt(dx * dx + dy * dy);
                    
                    if (dist < point.screenRadius * 1.5 && dist < minDist) {
                        minDist = dist;
                        hoveredPoint = point;
                    }
                }
            });
            
            if (hoveredPoint) {
                tooltip.style.opacity = '1';
                tooltip.style.left = (e.clientX + 15) + 'px';
                tooltip.style.top = (e.clientY + 15) + 'px';
                
                let html = `<strong>r = ${hoveredPoint.r}</strong><br>`;
                html += `gcd(${hoveredPoint.r}, ${hoveredPoint.M}) = ${hoveredPoint.gcd}<br>`;
                
                if (hoveredPoint.isOpen) {
                    html += `<span style="color: #00ffff;">COPRIME</span><br>`;
                    html += `${hoveredPoint.r}/${hoveredPoint.M} (irreducible)`;
                } else {
                    html += `<span style="color: #ff0064;">REDUCIBLE</span><br>`;
                    html += `${hoveredPoint.r}/${hoveredPoint.M} = ${hoveredPoint.reducedR}/${hoveredPoint.reducedM}<br>`;
                    html += `→ Channel M' = ${hoveredPoint.reducedM}`;
                }
            } else {
                tooltip.style.opacity = '0';
            }
        }

        function handleCompositeClick(x, y) {
            const canvas = document.getElementById('compositeCanvas');
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            
            // Find clicked point
            let clickedPoint = null;
            let minDist = Infinity;
            
            compositePoints.forEach(point => {
                if (point.screenX !== undefined) {
                    const dx = x - point.screenX;
                    const dy = y - point.screenY;
                    const dist = Math.sqrt(dx * dx + dy * dy);
                    
                    if (dist < 10 && dist < minDist) {
                        minDist = dist;
                        clickedPoint = point;
                    }
                }
            });
            
            if (clickedPoint) {
                let message = `Residue r = ${clickedPoint.r} in M = ${clickedPoint.M}\n\n`;
                message += `gcd(${clickedPoint.r}, ${clickedPoint.M}) = ${clickedPoint.gcd}\n\n`;
                
                if (clickedPoint.isOpen) {
                    message += `Status: IRREDUCIBLE (Coprime)\n`;
                    message += `This residue cannot be reduced.\n`;
                    message += `Fraction ${clickedPoint.r}/${clickedPoint.M} is already in lowest terms.`;
                } else {
                    message += `Status: REDUCIBLE\n`;
                    message += `Dividing by gcd = ${clickedPoint.gcd}:\n\n`;
                    message += `${clickedPoint.r}/${clickedPoint.M} = ${clickedPoint.reducedR}/${clickedPoint.reducedM}\n\n`;
                    message += `Projects to Farey channel M' = ${clickedPoint.reducedM}\n`;
                    message += `Channel multiplicity: d = ${clickedPoint.M}/${clickedPoint.reducedM} = ${clickedPoint.M / clickedPoint.reducedM}`;
                }
                
                alert(message);
            }
        }

        function exportCompositeImage() {
            const includeLegend = document.getElementById('compIncludeLegend').checked;
            const includeColorKey = document.getElementById('compIncludeColorKey').checked;
            const includeTimestamp = document.getElementById('compIncludeTimestamp').checked;
            const includeStats = document.getElementById('compIncludeStats').checked;
            const exportTitle = document.getElementById('compExportTitle').value;
            const resolution = parseFloat(document.getElementById('compExportResolution').value);
            
            const sourceCanvas = document.getElementById('compositeCanvas');
            const baseWidth = sourceCanvas.width;
            const baseHeight = sourceCanvas.height;
            
            // Reserve space for title at top
            const titleHeight = 100 * resolution;
            
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution + titleHeight;
            
            // Calculate legend dimensions - always on right
            let legendWidth = 0;
            
            if (includeLegend) {
                legendWidth = 500 * resolution;
                exportWidth += legendWidth;
            }
            
            // Create temporary canvas
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Fill background
            const bgColor = '#000000';
            const textColor = '#ffffff';
            tempCtx.fillStyle = bgColor;
            tempCtx.fillRect(0, 0, exportWidth, exportHeight);
            
            // Draw title at top center
            const fontSize = 18 * resolution;
            tempCtx.fillStyle = textColor;
            tempCtx.font = `bold ${fontSize * 1.8}px Arial`;
            tempCtx.textAlign = 'center';
            const titleY = titleHeight / 2 + fontSize / 2;
            tempCtx.fillText(exportTitle, exportWidth / 2, titleY);
            
            // Draw timestamp if enabled
            if (includeTimestamp) {
                tempCtx.font = `${fontSize * 0.8}px Arial`;
                const timestamp = new Date().toLocaleString();
                tempCtx.fillText(timestamp, exportWidth / 2, titleY + fontSize * 1.5);
            }
            
            // Draw main visualization scaled up below title
            tempCtx.save();
            tempCtx.translate(0, titleHeight);
            tempCtx.scale(resolution, resolution);
            tempCtx.drawImage(sourceCanvas, 0, 0);
            tempCtx.restore();
            
            // Draw legend if enabled
            if (includeLegend) {
                drawCompositeLegend(tempCtx, legendWidth, exportWidth, exportHeight, resolution, textColor, bgColor, titleHeight, includeColorKey, includeStats);
            }
            
            // Export
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `composite_projection_M${compositeModulus}_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawCompositeLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, bgColor, titleHeight, includeColorKey, includeStats) {
            const M = compositeModulus;
            const colorScheme = document.getElementById('compColorScheme').value;
            const displayMode = projectionMode;
            
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const sectionSpacing = 15 * resolution;
            
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            
            // Helper function to draw section header
            function drawSectionHeader(title) {
                ctx.font = `bold ${fontSize * 1.1}px Arial`;
                ctx.fillStyle = textColor;
                ctx.fillText(title, startX, y);
                y += lineHeight * 0.3;
                
                ctx.strokeStyle = textColor;
                ctx.lineWidth = 1.5 * resolution;
                ctx.beginPath();
                ctx.moveTo(startX, y);
                ctx.lineTo(startX + maxWidth * 0.9, y);
                ctx.stroke();
                y += lineHeight * 0.8;
            }
            
            // === CONFIGURATION SECTION ===
            drawSectionHeader('CONFIGURATION');
            
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            
            ctx.fillText(`Modulus M = ${M}`, startX, y);
            y += lineHeight;
            
            const factorization = primeFactorization(M);
            ctx.fillText(`Prime Factorization: ${factorization}`, startX, y);
            y += lineHeight;
            
            ctx.fillText(`Display Mode: ${displayMode === 'lines' ? 'Projection Lines' : 'Ring View'}`, startX, y);
            y += lineHeight;
            
            const colorSchemeText = colorScheme === 'channel-type' ? 'Channel Type' :
                                   colorScheme === 'spf' ? 'Smallest Prime Factor' :
                                   colorScheme === 'lpf' ? 'Largest Prime Factor' :
                                   colorScheme === 'gcd-value' ? 'GCD Value' : 'Channel Depth';
            ctx.fillText(`Color Scheme: ${colorSchemeText}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // === STATISTICS SECTION ===
            if (includeStats) {
                drawSectionHeader('STATISTICS');
                
                const phiM = phi(M);
                const reducible = M - phiM;
                const ratio = ((M - phiM) / M * 100).toFixed(1);
                
                const channels = [];
                for (let d = 1; d < M; d++) {
                    if (M % d === 0) channels.push(d);
                }
                
                ctx.font = `${fontSize}px Arial`;
                ctx.fillText(`φ(M) = ${phiM}`, startX, y);
                y += lineHeight;
                ctx.fillText(`Reducible Residues: ${reducible}`, startX, y);
                y += lineHeight;
                ctx.fillText(`Reducibility Ratio: ${ratio}%`, startX, y);
                y += lineHeight;
                ctx.fillText(`Farey Channels: ${channels.length}`, startX, y);
                y += lineHeight;
                
                y += sectionSpacing;
            }
            
            // === COLOR KEY SECTION ===
            if (includeColorKey) {
                drawSectionHeader('COLOR KEY');
                
                ctx.font = `${fontSize}px Arial`;
                
                if (colorScheme === 'channel-type') {
                    const items = [
                        { color: '#00ffff', label: 'Cyan = Irreducible (gcd=1)' },
                        { color: '#ff0064', label: 'Red = Reducible (gcd>1)' },
                        { color: '#ffc800', label: 'Gold = Farey Channels' }
                    ];
                    
                    items.forEach(item => {
                        ctx.fillStyle = item.color;
                        ctx.beginPath();
                        ctx.arc(startX + 10 * resolution, y - 5 * resolution, 6 * resolution, 0, 2 * Math.PI);
                        ctx.fill();
                        
                        ctx.fillStyle = textColor;
                        ctx.fillText(item.label, startX + 25 * resolution, y);
                        y += lineHeight * 1.2;
                    });
                } else if (colorScheme === 'spf' || colorScheme === 'lpf') {
                    ctx.fillStyle = textColor;
                    ctx.fillText('Color by prime factor:', startX, y);
                    y += lineHeight;
                    
                    const primes = [2, 3, 5, 7, 11, 13, 17, 19];
                    const primeColors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', 
                                        '#ff00ff', '#00ffff', '#ff8800', '#8800ff'];
                    
                    primes.forEach((p, idx) => {
                        ctx.fillStyle = primeColors[idx];
                        ctx.beginPath();
                        ctx.arc(startX + 10 * resolution, y - 5 * resolution, 5 * resolution, 0, 2 * Math.PI);
                        ctx.fill();
                        
                        ctx.fillStyle = textColor;
                        ctx.font = `${fontSize * 0.9}px Arial`;
                        ctx.fillText(`Prime ${p}`, startX + 25 * resolution, y);
                        y += lineHeight;
                    });
                }
                
                y += sectionSpacing;
            }
            
            // === KEY RESULT SECTION ===
            drawSectionHeader('KEY RESULT');
            
            ctx.font = `${fontSize * 0.95}px Arial`;
            ctx.fillStyle = textColor;
            
            const lines = [
                'Every composite M has reducible',
                'residues projecting onto simpler',
                'Farey channels. The number',
                'projecting to channel M\' is',
                'exactly d = M/M\' (multiplicity).'
            ];
            
            lines.forEach(line => {
                ctx.fillText(line, startX, y);
                y += lineHeight;
            });
            
            y += sectionSpacing;
            
            // === METADATA SECTION ===
            drawSectionHeader('METADATA');
            
            ctx.font = `${fontSize * 0.9}px Arial`;
            const date = new Date().toLocaleString();
            ctx.fillText(`Generated: ${date}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Author: Wessen Getachew`, startX, y);
            y += lineHeight;
            ctx.fillText(`Tool: Composite Projection`, startX, y);
            y += lineHeight;
            const resText = document.getElementById('compExportResolution').selectedOptions[0].text;
            ctx.fillText(`Resolution: ${resText}`, startX, y);
        }

        function exportCompositeCSV() {
            let csv = '';
            
            // Add metadata
            csv += `# Composite Channel Projection Data Export\n`;
            csv += `# Generated: ${new Date().toLocaleString()}\n`;
            csv += `# Author: Wessen Getachew\n`;
            csv += `# Modulus M: ${compositeModulus}\n`;
            csv += `# Prime Factorization: ${primeFactorization(compositeModulus)}\n`;
            csv += `# φ(M): ${phi(compositeModulus)}\n`;
            csv += `#\n`;
            
            // Header
            csv += 'Residue,Modulus,GCD,Channel_Status,Reduced_Numerator,Reduced_Denominator,';
            csv += 'Angle_Radians,Angle_Degrees,SPF,LPF\n';
            
            // Data
            compositePoints.forEach(p => {
                const angleRad = p.angle.toFixed(6);
                const angleDeg = (p.angle * 180 / Math.PI).toFixed(4);
                
                csv += `${p.r},${p.M},${p.gcd},${p.isOpen ? 'Open' : 'Closed'},`;
                csv += `${p.reducedR},${p.reducedM},${angleRad},${angleDeg},${p.spf},${p.lpf}\n`;
            });
            
            // Export
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `composite_projection_M${compositeModulus}_${timestamp}.csv`;
            link.href = url;
            link.click();
            URL.revokeObjectURL(url);
        }
    </script>
</body>
</html>
