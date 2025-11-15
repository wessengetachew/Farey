
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
            --bg-primary: #e6f3ff;
            --bg-secondary: #cce7ff;
            --text-primary: #1a1a2e;
            --text-secondary: #2d4059;
            --border-color: #2d4059;
            --border-subtle: #99ccff;
            --accent-color: #0066cc;
            --hover-bg: #0066cc;
            --hover-text: #ffffff;
            --ring-line-color: rgba(45, 64, 89, 0.2);
            --connection-line-color: rgba(45, 64, 89, 0.3);
            --tooltip-bg: rgba(45, 64, 89, 0.95);
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
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            background: var(--bg-primary);
            border-bottom: 1px solid var(--border-color);
            gap: 2px;
        }

        .tab {
            padding: 15px 10px;
            text-align: center;
            cursor: pointer;
            background: var(--bg-primary);
            border: none;
            font-size: 12px;
            font-weight: 600;
            color: var(--text-secondary);
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            border-bottom: 3px solid transparent;
        }

        .tab:hover:not(.active) {
            color: var(--text-primary);
            border-bottom-color: var(--border-color);
        }

        .tab.active {
            background: var(--bg-secondary);
            color: var(--text-primary);
            border-bottom-color: var(--accent-color);
        }

        .tab.color-main { border-bottom-color: #00ff00; }
        .tab.color-theory { border-bottom-color: #00ffff; }
        .tab.color-composite { border-bottom-color: #ffc800; }
        .tab.color-quadratic { border-bottom-color: #ff00ff; }
        .tab.color-primitive { border-bottom-color: #ff0064; }
        .tab.color-multiplication { border-bottom-color: #00ff64; }
        .tab.color-crt { border-bottom-color: #ff8800; }
        .tab.color-cyclotomic { border-bottom-color: #8800ff; }
        .tab.color-dirichlet { border-bottom-color: #ff0080; }
        .tab.color-mobius { border-bottom-color: #00ffaa; }

        .tab.active.color-main { background: rgba(0, 255, 0, 0.1); }
        .tab.active.color-theory { background: rgba(0, 255, 255, 0.1); }
        .tab.active.color-composite { background: rgba(255, 200, 0, 0.1); }
        .tab.active.color-quadratic { background: rgba(255, 0, 255, 0.1); }
        .tab.active.color-primitive { background: rgba(255, 0, 100, 0.1); }
        .tab.active.color-multiplication { background: rgba(0, 255, 100, 0.1); }
        .tab.active.color-crt { background: rgba(255, 136, 0, 0.1); }
        .tab.active.color-cyclotomic { background: rgba(136, 0, 255, 0.1); }
        .tab.active.color-dirichlet { background: rgba(255, 0, 128, 0.1); }
        .tab.active.color-mobius { background: rgba(0, 255, 170, 0.1); }

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
            <button class="tab color-main" onclick="switchTab('visualization')">Visualization</button>
            <button class="tab color-theory" onclick="switchTab('understanding')">Theory</button>
            <button class="tab color-composite" onclick="switchTab('composite-projection')">Composite</button>
            <button class="tab color-quadratic" onclick="switchTab('quadratic-residues')">Quadratic</button>
            <button class="tab color-primitive" onclick="switchTab('primitive-roots')">Primitive Roots</button>
            <button class="tab color-multiplication" onclick="switchTab('multiplication-table')">Multiplication</button>
            <button class="tab color-crt" onclick="switchTab('crt-visualizer')">CRT</button>
            <button class="tab color-cyclotomic" onclick="switchTab('cyclotomic')">Cyclotomic</button>
            <button class="tab color-dirichlet" onclick="switchTab('dirichlet')">Dirichlet</button>
            <button class="tab color-mobius" onclick="switchTab('mobius')">Möbius</button>
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

        <div id="quadraticResiduesTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Quadratic Residues & Legendre Symbols</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Prime Modulus (p): <span id="qrModDisplay" style="color: #00ffff;">17</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">3</span>
                            <input type="range" id="qrModSlider" min="3" max="10000" value="17" step="2"
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">10000</span>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Or enter any prime (no limit):</label>
                        <input type="number" id="qrModInput" min="3" value="17" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                        <div style="font-size: 10px; opacity: 0.7; margin-top: 5px;">Enter any prime number. Large primes may take longer to compute.</div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap: 8px; margin-bottom: 20px;">
                        <button onclick="setQRPrime(7)" style="padding: 8px;">p = 7</button>
                        <button onclick="setQRPrime(11)" style="padding: 8px;">p = 11</button>
                        <button onclick="setQRPrime(13)" style="padding: 8px;">p = 13</button>
                        <button onclick="setQRPrime(17)" style="padding: 8px;">p = 17</button>
                        <button onclick="setQRPrime(23)" style="padding: 8px;">p = 23</button>
                        <button onclick="setQRPrime(31)" style="padding: 8px;">p = 31</button>
                        <button onclick="setQRPrime(61)" style="padding: 8px;">p = 61</button>
                        <button onclick="setQRPrime(97)" style="padding: 8px;">p = 97</button>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Visualization Mode:
                        </label>
                        <select id="qrVisualizationMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="residue-nonresidue">Residues vs Non-Residues</option>
                            <option value="legendre-symbol">Legendre Symbol (+1, 0, -1)</option>
                            <option value="square-sequence">Square Sequence (1², 2², 3²...)</option>
                            <option value="reciprocity-pattern">Quadratic Reciprocity Pattern</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="qrShowConnections" style="margin-right: 8px;">
                            Show Square Connections (a → a²)
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="qrAnimateSequence" style="margin-right: 8px;">
                            Animate Square Sequence
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Point Size: <span id="qrPointSizeDisplay">7</span>
                        </label>
                        <input type="range" id="qrPointSize" min="4" max="15" step="0.5" value="7" 
                               style="width: 100%; height: 8px;">
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="quadraticCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px; cursor: crosshair;">
                    </canvas>
                    <div id="quadraticTooltip" style="position: absolute; padding: 10px; background: rgba(255, 255, 255, 0.95); 
                         color: #000000; border: 1px solid #000; pointer-events: none; font-size: 11px; 
                         line-height: 1.4; opacity: 0; transition: opacity 0.2s; z-index: 1000; max-width: 250px;
                         font-family: 'Courier New', monospace;">
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="qrExportTitle" value="Quadratic Residues Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="qrExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="qrIncludeLegend" checked style="margin-right: 8px;">
                            Include Statistics & Legend
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportQRImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportQRCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Prime p</div>
                        <div id="qrPrime" style="font-size: 24px; font-weight: 600; color: #00ffff;">17</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">QR Count</div>
                        <div id="qrCount" style="font-size: 24px; font-weight: 600; color: #00ff00;">8</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">NR Count</div>
                        <div id="nrCount" style="font-size: 24px; font-weight: 600; color: #ff0064;">8</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">QR Ratio</div>
                        <div id="qrRatio" style="font-size: 24px; font-weight: 600; color: #ffc800;">50%</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">p mod 4</div>
                        <div id="qrMod4" style="font-size: 24px; font-weight: 600; color: #ffffff;">1</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Current Prime Analysis</h3>
                    <div id="qrAnalysisText" style="font-size: 14px; line-height: 1.8;">
                        <p style="margin-bottom: 12px;">Analysis will appear here...</p>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Quadratic Residues Table</h3>
                    <div id="qrTableContainer" style="max-height: 400px; overflow-y: auto;">
                        <table id="qrTable" style="width: 100%; font-size: 12px; border-collapse: collapse;">
                            <thead>
                                <tr style="background: var(--bg-primary); position: sticky; top: 0;">
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">a</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">a² mod p</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Legendre (a|p)</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Status</th>
                                </tr>
                            </thead>
                            <tbody id="qrTableBody">
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Visualization Legend</h3>
                    <div id="qrLegend">
                        <ul style="list-style: none; padding: 0; margin: 0;">
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #00ff00; font-size: 18px;">●</span>
                                <strong style="color: #00ff00;">Green points</strong> = Quadratic Residues (QR)
                            </li>
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #ff0064; font-size: 18px;">●</span>
                                <strong style="color: #ff0064;">Red points</strong> = Non-Residues (NR)
                            </li>
                            <li style="margin-bottom: 12px; padding-left: 25px; position: relative;">
                                <span style="position: absolute; left: 0; color: #666666; font-size: 18px;">●</span>
                                <strong style="color: #666666;">Gray point</strong> = Zero (always QR)
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div style="background: rgba(0, 200, 255, 0.1); border: 2px solid #00c8ff; padding: 20px; margin-bottom: 20px;">
                    <h3 style="margin-bottom: 15px; color: #00c8ff;">Key Theorem: Quadratic Reciprocity</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        For odd primes p and q: (p|q)(q|p) = (-1)^((p-1)(q-1)/4)
                    </p>
                    <p style="margin-top: 10px; font-size: 13px; opacity: 0.9;">
                        This beautiful result connects the quadratic character of p modulo q with that of q modulo p.
                    </p>
                </div>
            </div>
        </div>

        <div id="primitiveRootsTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Primitive Roots & Cyclic Structure</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Modulus (m): <span id="prModDisplay" style="color: #00ffff;">7</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">2</span>
                            <input type="range" id="prModSlider" min="2" max="10000" value="7" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">10000</span>
                        </div>
                        <input type="number" id="prModInput" min="2" value="7" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                        <div style="font-size: 10px; opacity: 0.7; margin-top: 5px;">Enter any modulus (no limit). Large values may take longer.</div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap: 8px; margin-bottom: 20px;">
                        <button onclick="setPRModulus(7)" style="padding: 8px;">m = 7</button>
                        <button onclick="setPRModulus(11)" style="padding: 8px;">m = 11</button>
                        <button onclick="setPRModulus(13)" style="padding: 8px;">m = 13</button>
                        <button onclick="setPRModulus(17)" style="padding: 8px;">m = 17</button>
                        <button onclick="setPRModulus(18)" style="padding: 8px;">m = 18</button>
                        <button onclick="setPRModulus(25)" style="padding: 8px;">m = 25</button>
                        <button onclick="setPRModulus(26)" style="padding: 8px;">m = 26</button>
                        <button onclick="setPRModulus(50)" style="padding: 8px;">m = 50</button>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Select Generator (if primitive roots exist):
                        </label>
                        <select id="prGeneratorSelect" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="auto">Auto (smallest)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Visualization Mode:
                        </label>
                        <select id="prVisualizationMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="orbit-structure">Orbit Structure</option>
                            <option value="powers-sequence">Powers Sequence (g^1, g^2, g^3...)</option>
                            <option value="order-coloring">Color by Order</option>
                            <option value="subgroup-lattice">Subgroup Lattice</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="prShowPowerLines" checked style="margin-right: 8px;">
                            Show Power Connections (g^k → g^(k+1))
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="prAnimatePowers" style="margin-right: 8px;">
                            Animate Powers Cycling
                        </label>
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="primitiveCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px;">
                    </canvas>
                    <div id="primitiveTooltip" style="position: absolute; padding: 10px; background: rgba(255, 255, 255, 0.95); 
                         color: #000000; border: 1px solid #000; pointer-events: none; font-size: 11px; 
                         line-height: 1.4; opacity: 0; transition: opacity 0.2s; z-index: 1000; max-width: 300px;
                         font-family: 'Courier New', monospace;">
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="prExportTitle" value="Primitive Roots Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="prExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="3">2K (2100×2100)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="6">6K (4200×4200)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="prIncludeLegend" checked style="margin-right: 8px;">
                            Include Parameter Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="prIncludeColorKey" checked style="margin-right: 8px;">
                            Include Color Key Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="prIncludeTimestamp" checked style="margin-right: 8px;">
                            Include Timestamp
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportPRImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportPRCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Modulus m</div>
                        <div id="prModulus" style="font-size: 24px; font-weight: 600; color: #00ffff;">7</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">φ(m)</div>
                        <div id="prPhi" style="font-size: 24px; font-weight: 600; color: #00ff00;">6</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Has Primitive Root?</div>
                        <div id="prHasRoot" style="font-size: 20px; font-weight: 600; color: #ffc800; margin-top: 8px;">Yes</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Smallest Root</div>
                        <div id="prSmallest" style="font-size: 24px; font-weight: 600; color: #ff00ff;">3</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Total Generators</div>
                        <div id="prCount" style="font-size: 24px; font-weight: 600; color: #ffffff;">2</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Analysis</h3>
                    <div id="prAnalysisText" style="font-size: 14px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Order Table</h3>
                    <div id="prOrderTableContainer" style="max-height: 400px; overflow-y: auto;">
                        <table id="prOrderTable" style="width: 100%; font-size: 12px; border-collapse: collapse;">
                            <thead>
                                <tr style="background: var(--bg-primary); position: sticky; top: 0;">
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Element a</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Order ord(a)</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Powers</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Generator?</th>
                                </tr>
                            </thead>
                            <tbody id="prOrderTableBody"></tbody>
                        </table>
                    </div>
                </div>
                
                <div style="background: rgba(255, 0, 255, 0.1); border: 2px solid #ff00ff; padding: 20px;">
                    <h3 style="margin-bottom: 15px; color: #ff00ff;">Existence Theorem</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        Primitive roots exist modulo m if and only if m = 1, 2, 4, p^k, or 2p^k where p is an odd prime.
                    </p>
                </div>
            </div>
        </div>

        <div id="multiplicationTableTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Modular Multiplication Table & Cayley Table</h2>
                
                <div style="background: rgba(0, 200, 255, 0.1); border: 2px solid #00c8ff; padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px; color: #00c8ff;">Understanding the Multiplication Table</h3>
                    <p style="margin-bottom: 12px;">
                        This visualization displays the multiplication table for ℤ/mℤ, showing all products a × b (mod m). 
                        The table reveals the algebraic structure of the ring and highlights special elements crucial to number theory.
                    </p>
                    <p style="margin-bottom: 12px;">
                        <strong>Table Types:</strong>
                    </p>
                    <ul style="margin-left: 25px; margin-bottom: 12px;">
                        <li><strong>Full Multiplication:</strong> Shows all elements {0, 1, 2, ..., m-1} and their products</li>
                        <li><strong>Units Only (Cayley Table):</strong> Restricts to invertible elements, forming the group (ℤ/mℤ)×</li>
                        <li><strong>Addition Table:</strong> Displays addition structure instead of multiplication</li>
                    </ul>
                </div>

                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Modulus (m): <span id="mtModDisplay" style="color: #00ffff;">12</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">2</span>
                            <input type="range" id="mtModSlider" min="2" max="100" value="12" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">100</span>
                        </div>
                        <input type="number" id="mtModInput" min="2" max="100" value="12" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                        <div style="font-size: 10px; opacity: 0.7; margin-top: 5px;">Maximum modulus: 100 (for performance)</div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Table Type:
                        </label>
                        <select id="mtTableType" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="full">Full Multiplication (0 to m-1)</option>
                            <option value="units">Units Only (Cayley Table)</option>
                            <option value="addition">Addition Table</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Color Scheme:
                        </label>
                        <select id="mtColorScheme" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="rainbow">Rainbow (by value)</option>
                            <option value="residue-class">By Residue Class</option>
                            <option value="divisibility">By Divisibility</option>
                            <option value="zero-divisors">Highlight Zero Divisors</option>
                            <option value="idempotents">Highlight Idempotents</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Cell Size: <span id="mtCellSizeDisplay">20</span>px
                        </label>
                        <input type="range" id="mtCellSize" min="10" max="40" value="20" 
                               style="width: 100%; height: 8px;">
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mtShowValues" checked style="margin-right: 8px;">
                            Show Numeric Values
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mtShowSymmetry" style="margin-right: 8px;">
                            Highlight Diagonal Symmetry
                        </label>
                    </div>
                </div>
                
                <div style="display: flex; justify-content: center; margin-bottom: 20px;">
                    <div id="mtTableContainer" style="background: #000000; border: 2px solid var(--border-color); padding: 20px; border-radius: 4px; overflow: auto; max-width: 100%; max-height: 600px;">
                        <canvas id="multiplicationCanvas" width="600" height="600"></canvas>
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Modulus</div>
                        <div id="mtModulus" style="font-size: 24px; font-weight: 600; color: #00ffff;">12</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Units</div>
                        <div id="mtUnits" style="font-size: 24px; font-weight: 600; color: #00ff00;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Zero Divisors</div>
                        <div id="mtZeroDivisors" style="font-size: 24px; font-weight: 600; color: #ff0064;">6</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Idempotents</div>
                        <div id="mtIdempotents" style="font-size: 24px; font-weight: 600; color: #ffc800;">2</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Structure Analysis</h3>
                    <div id="mtAnalysisText" style="font-size: 14px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Special Elements</h3>
                    <div id="mtSpecialElements" style="font-size: 13px; line-height: 1.6;"></div>
                </div>
                
                <div style="background: rgba(255, 200, 0, 0.1); border: 2px solid #ffc800; padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px; color: #ffc800;">Special Elements Explained</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <h4 style="color: #00ff00; margin-bottom: 8px;">Units (Invertible Elements)</h4>
                        <p style="margin-bottom: 8px;">
                            An element a ∈ ℤ/mℤ is a <strong>unit</strong> if there exists some b such that a × b ≡ 1 (mod m).
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Key property:</strong> a is a unit ⟺ gcd(a, m) = 1
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Count:</strong> There are exactly φ(m) units, where φ is Euler's totient function.
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Example:</strong> In ℤ/12ℤ, the units are {1, 5, 7, 11} because gcd(1,12)=gcd(5,12)=gcd(7,12)=gcd(11,12)=1.
                            For instance: 5 × 5 ≡ 25 ≡ 1 (mod 12), so 5 is its own inverse.
                        </p>
                        <p style="font-style: italic; opacity: 0.9;">
                            The units form a group under multiplication called (ℤ/mℤ)×, the "group of units mod m".
                        </p>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <h4 style="color: #ff0064; margin-bottom: 8px;">Zero Divisors</h4>
                        <p style="margin-bottom: 8px;">
                            An element a ≠ 0 is a <strong>zero divisor</strong> if there exists some b ≠ 0 such that a × b ≡ 0 (mod m).
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Key property:</strong> a is a zero divisor ⟺ gcd(a, m) > 1 and a ≠ 0
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Example:</strong> In ℤ/12ℤ, consider a=3 and b=4: 3 × 4 = 12 ≡ 0 (mod 12).
                            So both 3 and 4 are zero divisors. Similarly, 6 × 2 ≡ 0 (mod 12).
                        </p>
                        <p style="font-style: italic; opacity: 0.9;">
                            Zero divisors prevent ℤ/mℤ from being an integral domain when m is composite. 
                            A ring has zero divisors ⟺ it's not an integral domain ⟺ the modulus is composite.
                        </p>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <h4 style="color: #ffff00; margin-bottom: 8px;">Idempotents</h4>
                        <p style="margin-bottom: 8px;">
                            An element a is <strong>idempotent</strong> if a² ≡ a (mod m), meaning multiplying by itself gives itself.
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Always present:</strong> 0 and 1 are always idempotent (0² = 0 and 1² = 1).
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Example:</strong> In ℤ/12ℤ, check a=4: 4² = 16 ≡ 4 (mod 12). So 4 is idempotent.
                            The complete set of idempotents in ℤ/12ℤ is {0, 1, 4, 9}.
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Connection to factorization:</strong> The number of idempotents equals 2^k where k is the number of 
                            distinct prime factors of m. For m=12=2²×3, we have k=2 distinct primes, giving 2²=4 idempotents.
                        </p>
                        <p style="font-style: italic; opacity: 0.9;">
                            Idempotents correspond to ways of "splitting" the ring. In ℤ/12ℤ, the idempotent 4 acts like a 
                            "partial identity" that selects elements divisible by certain prime factors.
                        </p>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <h4 style="color: #ff00ff; margin-bottom: 8px;">Nilpotents</h4>
                        <p style="margin-bottom: 8px;">
                            An element a is <strong>nilpotent</strong> if some power of a equals zero: a^k ≡ 0 (mod m) for some k > 0.
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Example:</strong> In ℤ/12ℤ, consider a=6: 6² = 36 = 3×12 ≡ 0 (mod 12). So 6 is nilpotent with index 2.
                        </p>
                        <p style="font-style: italic; opacity: 0.9;">
                            Nilpotents only exist when m has a repeated prime factor (like 4, 8, 9, 12, 16, ...).
                            In a reduced ring (no nilpotents), m must be square-free.
                        </p>
                    </div>
                    
                    <div style="background: rgba(255, 255, 255, 0.1); padding: 15px; border-left: 4px solid #00ffff;">
                        <h4 style="color: #00ffff; margin-bottom: 8px;">Fundamental Theorem</h4>
                        <p style="margin-bottom: 8px;">
                            Every element in ℤ/mℤ is <strong>either</strong> a unit <strong>or</strong> a zero divisor (or zero itself).
                        </p>
                        <p style="margin-bottom: 8px;">
                            <strong>Why?</strong> By Bézout's identity, if gcd(a,m)=1, then there exist x,y with ax+my=1, 
                            so ax≡1 (mod m) and a is a unit. Otherwise gcd(a,m)=d>1, so a×(m/d)≡0 (mod m) and a is a zero divisor.
                        </p>
                        <p style="font-style: italic;">
                            This dichotomy is fundamental: the ring ℤ/mℤ splits into units (which form a group) 
                            and zero divisors (which prevent the ring from being a field unless m is prime).
                        </p>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="mtExportTitle" value="Multiplication Table Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="mtExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (Current Size)</option>
                            <option value="2">HD (2x)</option>
                            <option value="3">2K (3x)</option>
                            <option value="4" selected>4K (4x)</option>
                            <option value="6">6K (6x)</option>
                            <option value="8">8K (8x)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mtIncludeLegend" checked style="margin-right: 8px;">
                            Include Parameter Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mtIncludeColorKey" checked style="margin-right: 8px;">
                            Include Color Key Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mtIncludeTimestamp" checked style="margin-right: 8px;">
                            Include Timestamp
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportMTImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportMTCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
            </div>
        </div>

        <div id="crtVisualizerTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Chinese Remainder Theorem Visualizer</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">System Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Number of Congruences:</label>
                        <select id="crtNumEqs" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="2" selected>2 congruences</option>
                            <option value="3">3 congruences</option>
                            <option value="4">4 congruences</option>
                        </select>
                    </div>
                    
                    <div id="crtEquations" style="margin-bottom: 20px;">
                        <div style="margin-bottom: 15px;">
                            <label style="display: block; margin-bottom: 5px; font-weight: 600;">x ≡ a₁ (mod m₁)</label>
                            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                                <input type="number" id="crt_a1" value="2" placeholder="a₁" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                                <input type="number" id="crt_m1" value="3" placeholder="m₁" min="2" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            </div>
                        </div>
                        
                        <div style="margin-bottom: 15px;">
                            <label style="display: block; margin-bottom: 5px; font-weight: 600;">x ≡ a₂ (mod m₂)</label>
                            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                                <input type="number" id="crt_a2" value="3" placeholder="a₂" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                                <input type="number" id="crt_m2" value="5" placeholder="m₂" min="2" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            </div>
                        </div>
                        
                        <div id="crtEq3" style="margin-bottom: 15px; display: none;">
                            <label style="display: block; margin-bottom: 5px; font-weight: 600;">x ≡ a₃ (mod m₃)</label>
                            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                                <input type="number" id="crt_a3" value="2" placeholder="a₃" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                                <input type="number" id="crt_m3" value="7" placeholder="m₃" min="2" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            </div>
                        </div>
                        
                        <div id="crtEq4" style="margin-bottom: 15px; display: none;">
                            <label style="display: block; margin-bottom: 5px; font-weight: 600;">x ≡ a₄ (mod m₄)</label>
                            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                                <input type="number" id="crt_a4" value="1" placeholder="a₄" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                                <input type="number" id="crt_m4" value="11" placeholder="m₄" min="2" style="padding: 8px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            </div>
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Visualization Mode:</label>
                        <select id="crtVizMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="2d-lattice">2D Lattice (2 congruences)</option>
                            <option value="circles">Concentric Circles</option>
                            <option value="number-line">Number Line Intersection</option>
                        </select>
                    </div>
                    
                    <button onclick="solveCRT()" style="width: 100%; padding: 12px; font-size: 14px; background: #00ff00; color: #000000;">Solve System</button>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="crtCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px;">
                    </canvas>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Solution</h3>
                    <div id="crtSolution" style="font-size: 16px; font-weight: 600; color: #00ff00; margin-bottom: 15px;"></div>
                    <div id="crtSteps" style="font-size: 13px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="crtExportTitle" value="Chinese Remainder Theorem Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="crtExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportCRTImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportCRTCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="background: rgba(0, 255, 100, 0.1); border: 2px solid #00ff64; padding: 20px;">
                    <h3 style="margin-bottom: 15px; color: #00ff64;">Chinese Remainder Theorem</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        If m₁, m₂, ..., mₙ are pairwise coprime, then the system of congruences
                        x ≡ aᵢ (mod mᵢ) has a unique solution modulo M = m₁m₂...mₙ.
                    </p>
                    <p style="margin-top: 10px; font-size: 13px; opacity: 0.9;">
                        The ring isomorphism: ℤ/Mℤ ≅ ℤ/m₁ℤ × ℤ/m₂ℤ × ... × ℤ/mₙℤ
                    </p>
                </div>
            </div>
        </div>

        <div id="cyclotomicTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Cyclotomic Polynomials & Roots of Unity</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Order n: <span id="cyclNDisplay" style="color: #00ffff;">12</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">2</span>
                            <input type="range" id="cyclNSlider" min="2" max="60" value="12" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">60</span>
                        </div>
                        <input type="number" id="cyclNInput" min="2" max="100" value="12" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap: 8px; margin-bottom: 20px;">
                        <button onclick="setCyclN(3)" style="padding: 8px;">n = 3</button>
                        <button onclick="setCyclN(4)" style="padding: 8px;">n = 4</button>
                        <button onclick="setCyclN(5)" style="padding: 8px;">n = 5</button>
                        <button onclick="setCyclN(6)" style="padding: 8px;">n = 6</button>
                        <button onclick="setCyclN(8)" style="padding: 8px;">n = 8</button>
                        <button onclick="setCyclN(12)" style="padding: 8px;">n = 12</button>
                        <button onclick="setCyclN(15)" style="padding: 8px;">n = 15</button>
                        <button onclick="setCyclN(24)" style="padding: 8px;">n = 24</button>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Visualization Mode:</label>
                        <select id="cyclVizMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="all-roots">All n-th Roots of Unity</option>
                            <option value="primitive-only">Primitive Roots Only</option>
                            <option value="by-order">Colored by Order</option>
                            <option value="galois-orbits">Galois Orbits</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="cyclShowConnections" checked style="margin-right: 8px;">
                            Show Connections Between Roots
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="cyclShowPolygon" checked style="margin-right: 8px;">
                            Draw Regular Polygon
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="cyclAnimateRotation" style="margin-right: 8px;">
                            Animate Rotation
                        </label>
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="cyclotomicCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px;">
                    </canvas>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="prExportTitle" value="Primitive Roots Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="prExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportPRImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportPRCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Order n</div>
                        <div id="cyclOrder" style="font-size: 24px; font-weight: 600; color: #00ffff;">12</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">φ(n)</div>
                        <div id="cyclPhi" style="font-size: 24px; font-weight: 600; color: #00ff00;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">All Roots</div>
                        <div id="cyclAllRoots" style="font-size: 24px; font-weight: 600; color: #ffffff;">12</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Primitive</div>
                        <div id="cyclPrimitive" style="font-size: 24px; font-weight: 600; color: #ff00ff;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Degree Φₙ(x)</div>
                        <div id="cyclDegree" style="font-size: 24px; font-weight: 600; color: #ffc800;">4</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Cyclotomic Polynomial Φₙ(x)</h3>
                    <div id="cyclPolynomial" style="font-size: 16px; font-weight: 600; color: #00ffff; margin-bottom: 15px; font-family: 'Courier New', monospace;"></div>
                    <div id="cyclAnalysis" style="font-size: 14px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Roots Table</h3>
                    <div id="cyclRootsTableContainer" style="max-height: 400px; overflow-y: auto;">
                        <table id="cyclRootsTable" style="width: 100%; font-size: 12px; border-collapse: collapse;">
                            <thead>
                                <tr style="background: var(--bg-primary); position: sticky; top: 0;">
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">k</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">ζₙᵏ</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Angle</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Order</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Primitive?</th>
                                </tr>
                            </thead>
                            <tbody id="cyclRootsTableBody"></tbody>
                        </table>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px;">
                    <h3 style="margin-bottom: 15px;">Factorization of xⁿ - 1</h3>
                    <div id="cyclFactorization" style="font-size: 14px; line-height: 1.8; font-family: 'Courier New', monospace;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="cyclExportTitle" value="Cyclotomic Polynomials Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="cyclExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportCyclImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportCyclCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
            </div>
        </div>

        <div id="dirichletTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Dirichlet Characters & L-functions</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Modulus (q): <span id="dirModDisplay" style="color: #00ffff;">12</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">3</span>
                            <input type="range" id="dirModSlider" min="3" max="10000" value="12" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">10000</span>
                        </div>
                        <input type="number" id="dirModInput" min="3" value="12" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                        <div style="font-size: 10px; opacity: 0.7; margin-top: 5px;">Enter any modulus (no limit). Large values may take longer.</div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Select Character:</label>
                        <select id="dirCharacterSelect" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="principal">Principal Character χ₀</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Visualization Mode:</label>
                        <select id="dirVizMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="character-values">Character Values as Colors</option>
                            <option value="character-table">Character Table</option>
                            <option value="orthogonality">Orthogonality Relations</option>
                            <option value="l-function">L-function Partial Sums</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="dirShowPhases" checked style="margin-right: 8px;">
                            Show Phase Angles (for complex values)
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="dirAnimateRotation" style="margin-right: 8px;">
                            Animate Character Rotation
                        </label>
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="dirichletCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px;">
                    </canvas>
                    <div id="dirichletTooltip" style="position: absolute; padding: 10px; background: rgba(255, 255, 255, 0.95); 
                         color: #000000; border: 1px solid #000; pointer-events: none; font-size: 11px; 
                         line-height: 1.4; opacity: 0; transition: opacity 0.2s; z-index: 1000; max-width: 250px;
                         font-family: 'Courier New', monospace;">
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Modulus q</div>
                        <div id="dirModulus" style="font-size: 24px; font-weight: 600; color: #00ffff;">12</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">φ(q)</div>
                        <div id="dirPhi" style="font-size: 24px; font-weight: 600; color: #00ff00;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Total Characters</div>
                        <div id="dirCharCount" style="font-size: 24px; font-weight: 600; color: #ff00ff;">4</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Character Type</div>
                        <div id="dirCharType" style="font-size: 18px; font-weight: 600; color: #ffc800; margin-top: 8px;">Principal</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Character Analysis</h3>
                    <div id="dirAnalysis" style="font-size: 14px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Character Table</h3>
                    <div id="dirTableContainer" style="max-height: 400px; overflow-y: auto;">
                        <table id="dirTable" style="width: 100%; font-size: 12px; border-collapse: collapse;">
                            <thead>
                                <tr style="background: var(--bg-primary); position: sticky; top: 0;">
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">n</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">gcd(n,q)</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">χ(n)</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">|χ(n)|</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">arg(χ(n))</th>
                                </tr>
                            </thead>
                            <tbody id="dirTableBody"></tbody>
                        </table>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="dirExportTitle" value="Dirichlet Characters Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="dirExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="3">2K (2100×2100)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="6">6K (4200×4200)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="dirIncludeLegend" checked style="margin-right: 8px;">
                            Include Parameter Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="dirIncludeColorKey" checked style="margin-right: 8px;">
                            Include Color Key Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="dirIncludeTimestamp" checked style="margin-right: 8px;">
                            Include Timestamp
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportDirImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportDirCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="background: rgba(255, 0, 128, 0.1); border: 2px solid #ff0080; padding: 20px;">
                    <h3 style="margin-bottom: 15px; color: #ff0080;">Dirichlet L-function</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        L(s, χ) = Σ χ(n)/n^s generalizes the Riemann zeta function using multiplicative characters.
                    </p>
                    <p style="margin-top: 10px; font-size: 13px; opacity: 0.9;">
                        Orthogonality: Σ χ(n)χ'(n)* = φ(q) if χ = χ', else 0
                    </p>
                </div>
            </div>
        </div>

        <div id="mobiusTab" class="tab-content">
            <div style="padding: 30px; max-width: 1400px; margin: 0 auto;">
                <h2 style="font-size: 28px; margin-bottom: 20px; text-align: center;">Möbius Function & Arithmetic Functions</h2>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Configuration</h3>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Maximum n: <span id="mobMaxDisplay" style="color: #00ffff;">60</span>
                        </label>
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 10px;">
                            <span style="font-size: 11px;">10</span>
                            <input type="range" id="mobMaxSlider" min="10" max="10000" value="60" 
                                   style="flex: 1; height: 8px;">
                            <span style="font-size: 11px;">10000</span>
                        </div>
                        <input type="number" id="mobMaxInput" min="10" value="60" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                        <div style="font-size: 10px; opacity: 0.7; margin-top: 5px;">Enter any value (no limit). Large values may take longer.</div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Arithmetic Function:</label>
                        <select id="mobFunctionSelect" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="mobius">μ(n) - Möbius Function</option>
                            <option value="euler-phi">φ(n) - Euler Totient</option>
                            <option value="tau">τ(n) - Number of Divisors</option>
                            <option value="sigma">σ(n) - Sum of Divisors</option>
                            <option value="omega">ω(n) - Distinct Prime Factors</option>
                            <option value="bigomega">Ω(n) - Prime Factors with Multiplicity</option>
                            <option value="liouville">λ(n) - Liouville Function</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">Visualization Mode:</label>
                        <select id="mobVizMode" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="ring-display">On Modular Rings</option>
                            <option value="cumulative-sum">Cumulative Sum M(x)</option>
                            <option value="color-map">Color Map by Value</option>
                            <option value="sieve-layers">Sieve Inclusion-Exclusion</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mobShowValues" checked style="margin-right: 8px;">
                            Show Numeric Values
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mobShowSummatory" style="margin-right: 8px;">
                            Show Summatory Function
                        </label>
                    </div>
                </div>
                
                <div style="position: relative; display: flex; justify-content: center; margin-bottom: 20px;">
                    <canvas id="mobiusCanvas" width="700" height="700" 
                            style="border: 2px solid var(--border-color); background: #000000; border-radius: 4px;">
                    </canvas>
                    <div id="mobiusTooltip" style="position: absolute; padding: 10px; background: rgba(255, 255, 255, 0.95); 
                         color: #000000; border: 1px solid #000; pointer-events: none; font-size: 11px; 
                         line-height: 1.4; opacity: 0; transition: opacity 0.2s; z-index: 1000; max-width: 250px;
                         font-family: 'Courier New', monospace;">
                    </div>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 15px; margin-bottom: 30px;">
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Range</div>
                        <div id="mobRange" style="font-size: 24px; font-weight: 600; color: #00ffff;">1 to 60</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">Sum M(x)</div>
                        <div id="mobSum" style="font-size: 24px; font-weight: 600; color: #00ff00;">0</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">μ(n) = +1</div>
                        <div id="mobPlusOne" style="font-size: 24px; font-weight: 600; color: #ffffff;">0</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">μ(n) = -1</div>
                        <div id="mobMinusOne" style="font-size: 24px; font-weight: 600; color: #ff0064;">0</div>
                    </div>
                    <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 15px; text-align: center;">
                        <div style="font-size: 11px; opacity: 0.8; margin-bottom: 5px;">μ(n) = 0</div>
                        <div id="mobZero" style="font-size: 24px; font-weight: 600; color: #666666;">0</div>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Function Analysis</h3>
                    <div id="mobAnalysis" style="font-size: 14px; line-height: 1.8;"></div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 25px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Values Table</h3>
                    <div id="mobTableContainer" style="max-height: 400px; overflow-y: auto;">
                        <table id="mobTable" style="width: 100%; font-size: 12px; border-collapse: collapse;">
                            <thead>
                                <tr style="background: var(--bg-primary); position: sticky; top: 0;">
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">n</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Prime Factors</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">f(n)</th>
                                    <th style="padding: 8px; border: 1px solid var(--border-color);">Cumulative</th>
                                </tr>
                            </thead>
                            <tbody id="mobTableBody"></tbody>
                        </table>
                    </div>
                </div>
                
                <div style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin-bottom: 30px;">
                    <h3 style="margin-bottom: 15px;">Export Options</h3>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Title</label>
                        <input type="text" id="mobExportTitle" value="Möbius Function Visualization" 
                               style="width: 100%; padding: 10px; border: 1px solid var(--border-color); 
                                      background: var(--bg-primary); color: var(--text-primary);">
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label style="display: block; margin-bottom: 8px; font-weight: 600;">Export Resolution</label>
                        <select id="mobExportResolution" style="width: 100%; padding: 10px; border: 1px solid var(--border-color); background: var(--bg-primary); color: var(--text-primary);">
                            <option value="1">Standard (700×700)</option>
                            <option value="2">HD (1400×1400)</option>
                            <option value="3">2K (2100×2100)</option>
                            <option value="4" selected>4K (2800×2800)</option>
                            <option value="6">6K (4200×4200)</option>
                            <option value="8">8K (5600×5600)</option>
                        </select>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mobIncludeLegend" checked style="margin-right: 8px;">
                            Include Parameter Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mobIncludeColorKey" checked style="margin-right: 8px;">
                            Include Color Key Legend
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 15px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="mobIncludeTimestamp" checked style="margin-right: 8px;">
                            Include Timestamp
                        </label>
                    </div>
                    
                    <div class="button-group">
                        <button onclick="exportMobImage()" style="background: #2196F3; color: #ffffff;">Export PNG</button>
                        <button onclick="exportMobCSV()" style="background: #FF9800; color: #ffffff;">Export CSV</button>
                    </div>
                </div>
                
                <div style="background: rgba(0, 255, 170, 0.1); border: 2px solid #00ffaa; padding: 20px;">
                    <h3 style="margin-bottom: 15px; color: #00ffaa;">Möbius Inversion Formula</h3>
                    <p style="margin: 0; font-size: 15px; line-height: 1.6;">
                        If g(n) = Σ(d|n) f(d), then f(n) = Σ(d|n) μ(d)g(n/d)
                    </p>
                    <p style="margin-top: 10px; font-size: 13px; opacity: 0.9;">
                        Example: φ(n) = Σ(d|n) μ(d)·n/d connects Möbius to Euler's totient
                    </p>
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
                    
                    <div style="margin-bottom: 20px;">
                        <label style="font-weight: 600; display: block; margin-bottom: 10px;">
                            Rotation: <span id="compRotationDisplay">0</span>°
                        </label>
                        <input type="range" id="compRotationSlider" min="0" max="360" step="1" value="0" 
                               style="width: 100%; height: 8px;">
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compAnimateRotation" style="margin-right: 8px;">
                            Animate Rotation
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compShowCoprimeOnly" style="margin-right: 8px;">
                            Show Only Coprime Residues (gcd=1)
                        </label>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <label class="checkbox-label" style="display: flex; align-items: center; cursor: pointer;">
                            <input type="checkbox" id="compEnableSweep" style="margin-right: 8px;">
                            Enable Coprime Sweep Animation
                        </label>
                    </div>
                    
                    <div id="compSweepControls" style="display: none; margin-bottom: 20px;">
                        <label style="display: block; margin-bottom: 10px; font-weight: 600;">
                            Sweep Speed: <span id="compSweepSpeedDisplay">1</span>
                        </label>
                        <input type="range" id="compSweepSpeed" min="0.1" max="5" step="0.1" value="1" 
                               style="width: 100%; height: 8px;">
                        
                        <label style="display: block; margin-top: 10px; margin-bottom: 10px; font-weight: 600;">
                            Current Coprime: <span id="compCurrentCoprime" style="color: #00ffff;">1</span>
                        </label>
                        
                        <div class="button-group" style="margin-top: 10px;">
                            <button id="compSweepPlayBtn" onclick="toggleCompositeSweep()" 
                                    style="background: #00ff00; color: #000000;">Play Sweep</button>
                            <button onclick="resetCompositeSweep()" 
                                    style="background: var(--bg-secondary); color: var(--text-primary);">Reset</button>
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
                    gcd(1, 12) = 1<br>
                    gcd(5, 12) = 1<br>
                    gcd(7, 12) = 1<br>
                    gcd(11, 12) = 1<br><br>
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
                    gcd(0, 12) = 12 (shares all factors)<br>
                    gcd(2, 12) = 2 (shares factor 2)<br>
                    gcd(3, 12) = 3 (shares factor 3)<br>
                    gcd(4, 12) = 4 (shares factor 2)<br>
                    gcd(6, 12) = 6 (shares factors 2 and 3)<br><br>
                    Count: 12 - φ(12) = 12 - 4 = 8
                </div>

                <h2>Quadratic Residues: The Geometry of Squares</h2>
                
                <p>
                    Beyond the coprimality structure lies another fundamental classification: <strong>quadratic residues</strong>. For a prime <em>p</em>, a non-zero residue <em>a</em> is a quadratic residue if there exists some <em>x</em> such that x² ≡ a (mod <em>p</em>).
                </p>
                
                <div class="formula">
                    <div class="formula-title">Definition of Quadratic Residue</div>
                    a is a quadratic residue modulo p ⟺ ∃x: x² ≡ a (mod p)
                    <br><br>
                    The Legendre symbol encodes this:
                    <br>
                    (a|p) = +1 if a is a quadratic residue mod p
                    <br>
                    (a|p) = -1 if a is a non-residue mod p
                    <br>
                    (a|p) = 0 if p divides a
                </div>

                <h3>The Square Sequence</h3>
                <p>
                    Computing 1², 2², 3², ..., ((p-1)/2)² modulo <em>p</em> produces exactly (p-1)/2 distinct quadratic residues. This reveals a beautiful symmetry: exactly half of the non-zero residues modulo a prime are squares, and half are not.
                </p>

                <div class="example-box">
                    <strong>Example: Quadratic Residues modulo 17</strong><br>
                    1² ≡ 1 (mod 17)<br>
                    2² ≡ 4 (mod 17)<br>
                    3² ≡ 9 (mod 17)<br>
                    4² ≡ 16 (mod 17)<br>
                    5² ≡ 25 ≡ 8 (mod 17)<br>
                    6² ≡ 36 ≡ 2 (mod 17)<br>
                    7² ≡ 49 ≡ 15 (mod 17)<br>
                    8² ≡ 64 ≡ 13 (mod 17)<br><br>
                    Quadratic residues: {1, 2, 4, 8, 9, 13, 15, 16}<br>
                    Non-residues: {3, 5, 6, 7, 10, 11, 12, 14}<br>
                    Count: 8 residues, 8 non-residues (perfect balance)
                </div>

                <h3>Quadratic Reciprocity</h3>
                <p>
                    One of the most stunning results in number theory is <strong>Gauss's Law of Quadratic Reciprocity</strong>, discovered after years of computational exploration and proved in eight different ways by Gauss himself.
                </p>

                <div class="formula">
                    <div class="formula-title">Quadratic Reciprocity Law</div>
                    For distinct odd primes p and q:
                    <br><br>
                    (p|q) · (q|p) = (-1)^((p-1)(q-1)/4)
                    <br><br>
                    This means:
                    <br>
                    If p ≡ 1 (mod 4) OR q ≡ 1 (mod 4), then (p|q) = (q|p)
                    <br>
                    If p ≡ q ≡ 3 (mod 4), then (p|q) = -(q|p)
                </div>

                <p>
                    This theorem reveals a deep reciprocity: whether <em>p</em> is a square modulo <em>q</em> is intimately connected to whether <em>q</em> is a square modulo <em>p</em>. The relationship depends only on the residue classes of <em>p</em> and <em>q</em> modulo 4.
                </p>

                <div class="example-box">
                    <strong>Example: Quadratic Reciprocity in Action</strong><br>
                    Consider p = 17 and q = 13.<br><br>
                    Since 17 ≡ 1 (mod 4), reciprocity predicts (17|13) = (13|17).<br><br>
                    Computing: 17 ≡ 4 (mod 13), and 4 = 2², so (17|13) = +1.<br>
                    Also: 13 ≡ 13 (mod 17), and we saw 13 is a QR mod 17, so (13|17) = +1.<br><br>
                    Indeed: (17|13) = (13|17) = +1, confirming reciprocity.
                </div>

                <h3>Supplements to Quadratic Reciprocity</h3>
                <p>
                    Two special cases complete the theory:
                </p>

                <div class="formula">
                    <div class="formula-title">First Supplement</div>
                    (-1|p) = (-1)^((p-1)/2)
                    <br><br>
                    This means: -1 is a quadratic residue mod p ⟺ p ≡ 1 (mod 4)
                </div>

                <div class="formula">
                    <div class="formula-title">Second Supplement</div>
                    (2|p) = (-1)^((p²-1)/8)
                    <br><br>
                    This means: 2 is a quadratic residue mod p ⟺ p ≡ ±1 (mod 8)
                </div>

                <p>
                    These supplements, combined with the main reciprocity law, provide a complete algorithm for computing the Legendre symbol (a|p) for any <em>a</em> and prime <em>p</em>, without needing to find square roots.
                </p>

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
                    This is intimately connected to the probability that two randomly chosen integers are coprime.
                </div>

                <h2>Connection Between Structures</h2>
                
                <p>
                    The interplay between coprimality and quadratic residuosity creates a rich tapestry of number-theoretic structure:
                </p>

                <ul>
                    <li><strong>For prime moduli:</strong> All non-zero residues are coprime, so the quadratic residue structure lives entirely within the group (ℤ/pℤ)×</li>
                    <li><strong>For composite moduli:</strong> Only coprime residues can be quadratic residues (in the generalized sense using the Jacobi symbol)</li>
                    <li><strong>Primitive roots:</strong> When they exist, primitive roots generate all quadratic residues through even powers and all non-residues through odd powers</li>
                    <li><strong>Cyclotomic theory:</strong> The quadratic residues correspond to specific Galois orbits of roots of unity</li>
                </ul>

                <h2>Historical Context</h2>
                
                <p>
                    The theory of quadratic residues represents one of the great triumphs of number theory:
                </p>

                <ul>
                    <li><strong>Fermat (1640s):</strong> Discovered special cases and made conjectures about when -1 and 2 are squares</li>
                    <li><strong>Euler (1750s):</strong> Extensive computational work and the first statement of quadratic reciprocity (without proof)</li>
                    <li><strong>Legendre (1785):</strong> Introduced the Legendre symbol and gave an incomplete proof</li>
                    <li><strong>Gauss (1796):</strong> At age 19, provided the first complete proof; eventually found eight different proofs</li>
                    <li><strong>Modern era:</strong> Generalizations to higher powers (cubic, quartic reciprocity) and connections to class field theory</li>
                </ul>

                <div class="formula" style="background: var(--bg-secondary); border: 2px solid var(--border-color); padding: 20px; margin: 30px 0;">
                    <div style="text-align: center; font-size: 18px; font-weight: 600; margin-bottom: 15px;">
                        Gauss on Quadratic Reciprocity
                    </div>
                    <p style="font-style: italic; text-align: center; margin: 0;">
                        "The theorem must certainly be regarded as one of the most elegant of its type."
                    </p>
                    <p style="text-align: center; margin-top: 10px; font-size: 14px;">
                        — Carl Friedrich Gauss, Disquisitiones Arithmeticae (1801)
                    </p>
                </div>

                <h2>Applications and Significance</h2>
                
                <h3>1. Primality Testing</h3>
                <p>
                    The Solovay-Strassen and Miller-Rabin primality tests use quadratic residuosity as a probabilistic criterion for primality.
                </p>

                <h3>2. Cryptography</h3>
                <p>
                    The quadratic residuosity problem (determining whether a number is a QR mod n without knowing the factorization of n) is computationally hard and forms the basis of several cryptographic protocols.
                </p>

                <h3>3. Diophantine Equations</h3>
                <p>
                    Understanding when equations like x² + y² = p (sum of two squares) have solutions depends critically on quadratic reciprocity.
                </p>

                <h3>4. L-functions and the Riemann Hypothesis</h3>
                <p>
                    Dirichlet L-functions, which generalize the Riemann zeta function, are defined using quadratic characters. The distribution of quadratic residues connects to the distribution of primes.
                </p>

                <p style="margin-top: 30px; font-style: italic;">
                    By visualizing these structures geometrically—as points on circles with carefully chosen colors and connections—we make visible the hidden symmetries that Gauss discovered through pure calculation. The patterns you see in the quadratic residue visualization are manifestations of reciprocity, the most fundamental symmetry in elementary number theory.
                </p>
            </div>
        </div>

        <div id="compositeProjectionTab" class="tab-content">
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

                    // Gap analysis: check if both r and r+gap are coprime (open channels)
                    let admissibleGaps = [];
                    if (isOpen && gaps.length > 0) {
                        gaps.forEach(gap => {
                            // For gap g, we need both r and r+g to be coprime to m
                            const rPlusG = (r + gap) % m;
                            const rPlusGGcd = gcd(rPlusG, m);
                            // Both r and r+gap must be open (coprime)
                            if (rPlusGGcd === 1) {
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

                    // Gap analysis: check if both r and r+gap are coprime (open channels)
                    let admissibleGaps = [];
                    if (enableGap && isOpen) {
                        gaps.forEach(gap => {
                            // For gap g, we need both r and r+g to be coprime to m
                            const rPlusG = (r + gap) % m;
                            const rPlusGGcd = gcd(rPlusG, m);
                            // Both r and r+gap must be open (coprime)
                            if (rPlusGGcd === 1) {
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

                    // Gap analysis: check if both r and r+gap are coprime (open channels)
                    let admissibleGaps = [];
                    if (isOpen && gaps.length > 0) {
                        gaps.forEach(gap => {
                            // For gap g, we need both r and r+g to be coprime to m
                            const rPlusG = (r + gap) % m;
                            const rPlusGGcd = gcd(rPlusG, m);
                            // Both r and r+gap must be open (coprime)
                            if (rPlusGGcd === 1) {
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
            
            const tabMap = {
                'visualization': [0, 'visualizationTab', null],
                'understanding': [1, 'understandingTab', null],
                'composite-projection': [2, 'compositeProjectionTab', updateCompositeVisualization],
                'quadratic-residues': [3, 'quadraticResiduesTab', updateQuadraticVisualization],
                'primitive-roots': [4, 'primitiveRootsTab', updatePrimitiveRootsVisualization],
                'multiplication-table': [5, 'multiplicationTableTab', updateMultiplicationTable],
                'crt-visualizer': [6, 'crtVisualizerTab', initCRT],
                'cyclotomic': [7, 'cyclotomicTab', updateCyclotomicVisualization],
                'dirichlet': [8, 'dirichletTab', updateDirichletVisualization],
                'mobius': [9, 'mobiusTab', updateMobiusVisualization]
            };
            
            if (tabMap[tab]) {
                const [index, tabId, initFunc] = tabMap[tab];
                const tabs = document.querySelectorAll('.tab');
                if (tabs[index]) {
                    tabs[index].classList.add('active');
                }
                const tabContent = document.getElementById(tabId);
                if (tabContent) {
                    tabContent.classList.add('active');
                }
                if (initFunc) initFunc();
            }
        }

        window.addEventListener('load', () => {
            initializeTheme();
            updateRangeDisplays();
            updateGapColorPickers();
            updateVisualization();
            initCompositeProjection();
            initQuadraticResidues();
            initPrimitiveRoots();
            initMultiplicationTable();
            initCRT();
            initCyclotomic();
            initDirichlet();
            initMobius();
        });

        // ===== COMPOSITE PROJECTION COROLLARY =====
        let compositeModulus = 12;
        let projectionMode = 'lines'; // 'lines' or 'ring'
        let compositePoints = [];
        let compositeZoom = 1;
        let compositePan = {x: 0, y: 0};
        let compositeRotation = 0;
        let compositeAnimationId = null;
        let compositeSweepId = null;
        let compositeSweepIndex = 0;
        let compositeCoprimes = [];
        let compositeShowCoprimeOnly = false;

        function initCompositeProjection() {
            const slider = document.getElementById('compModSlider');
            const input = document.getElementById('compModInput');
            const opacitySlider = document.getElementById('projOpacitySlider');
            const pointSizeSlider = document.getElementById('compPointSize');
            const colorScheme = document.getElementById('compColorScheme');
            const canvas = document.getElementById('compositeCanvas');
            const tooltip = document.getElementById('compositeTooltip');
            const rotationSlider = document.getElementById('compRotationSlider');
            const animateRotation = document.getElementById('compAnimateRotation');
            const showCoprimeOnly = document.getElementById('compShowCoprimeOnly');
            const enableSweep = document.getElementById('compEnableSweep');
            const sweepSpeed = document.getElementById('compSweepSpeed');
            
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
            
            rotationSlider.addEventListener('input', () => {
                compositeRotation = parseFloat(rotationSlider.value);
                document.getElementById('compRotationDisplay').textContent = compositeRotation.toFixed(0);
                drawCompositeVisualization();
            });
            
            animateRotation.addEventListener('change', () => {
                if (animateRotation.checked) {
                    startCompositeAnimation();
                } else {
                    stopCompositeAnimation();
                }
            });
            
            showCoprimeOnly.addEventListener('change', () => {
                compositeShowCoprimeOnly = showCoprimeOnly.checked;
                drawCompositeVisualization();
            });
            
            enableSweep.addEventListener('change', () => {
                const sweepControls = document.getElementById('compSweepControls');
                sweepControls.style.display = enableSweep.checked ? 'block' : 'none';
                if (!enableSweep.checked) {
                    stopCompositeSweep();
                }
            });
            
            sweepSpeed.addEventListener('input', () => {
                document.getElementById('compSweepSpeedDisplay').textContent = 
                    parseFloat(sweepSpeed.value).toFixed(1);
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
            
            // Get coprime residues for sweep
            compositeCoprimes = [];
            for (let r = 1; r < M; r++) {
                if (gcd(r, M) === 1) {
                    compositeCoprimes.push(r);
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
            
            // Update analysis text with Φ(M) information
            let analysisHTML = `<p style="margin-bottom: 12px;"><strong>M = ${M} = ${factorization}</strong></p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">This composite modulus has <strong>${phiM} coprime residues</strong> (φ(${M}) = ${phiM}) and <strong>${reducible} reducible residues</strong>.</p>`;
            
            // Special note for M = 30×2^n
            if (M % 30 === 0 && isPowerOfTwo(M / 30)) {
                const n = Math.log2(M / 30);
                analysisHTML += `<p style="margin-bottom: 12px; background: rgba(0, 255, 255, 0.1); padding: 10px; border-left: 3px solid #00ffff;"><strong>Special M₃₀ Modulus: M = 30 × 2^${n}</strong><br>`;
                analysisHTML += `This modulus automatically excludes residues divisible by 2, 3, or 5.<br>`;
                analysisHTML += `All primes p > 5 satisfy p mod ${M} ∈ Φ(${M}).<br>`;
                analysisHTML += `The coprime residue system Φ(${M}) forms a closed multiplicative system under prime factorization.</p>`;
            }
            
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
        
        function isPowerOfTwo(n) {
            return n > 0 && (n & (n - 1)) === 0;
        }
        
        function startCompositeAnimation() {
            if (!compositeAnimationId) {
                function animate() {
                    compositeRotation += 0.5;
                    if (compositeRotation >= 360) compositeRotation -= 360;
                    document.getElementById('compRotationSlider').value = compositeRotation;
                    document.getElementById('compRotationDisplay').textContent = compositeRotation.toFixed(0);
                    drawCompositeVisualization();
                    compositeAnimationId = requestAnimationFrame(animate);
                }
                compositeAnimationId = requestAnimationFrame(animate);
            }
        }
        
        function stopCompositeAnimation() {
            if (compositeAnimationId) {
                cancelAnimationFrame(compositeAnimationId);
                compositeAnimationId = null;
            }
        }
        
        function toggleCompositeSweep() {
            if (compositeSweepId) {
                stopCompositeSweep();
                document.getElementById('compSweepPlayBtn').textContent = 'Play Sweep';
                document.getElementById('compSweepPlayBtn').style.background = '#00ff00';
            } else {
                startCompositeSweep();
                document.getElementById('compSweepPlayBtn').textContent = 'Pause Sweep';
                document.getElementById('compSweepPlayBtn').style.background = '#ff0000';
            }
        }
        
        function startCompositeSweep() {
            if (!compositeSweepId && compositeCoprimes.length > 0) {
                function sweep() {
                    const speed = parseFloat(document.getElementById('compSweepSpeed').value);
                    compositeSweepIndex = (compositeSweepIndex + 0.02 * speed) % compositeCoprimes.length;
                    const currentIdx = Math.floor(compositeSweepIndex);
                    const currentCoprime = compositeCoprimes[currentIdx];
                    document.getElementById('compCurrentCoprime').textContent = currentCoprime;
                    drawCompositeVisualization();
                    compositeSweepId = requestAnimationFrame(sweep);
                }
                compositeSweepId = requestAnimationFrame(sweep);
            }
        }
        
        function stopCompositeSweep() {
            if (compositeSweepId) {
                cancelAnimationFrame(compositeSweepId);
                compositeSweepId = null;
            }
        }
        
        function resetCompositeSweep() {
            stopCompositeSweep();
            compositeSweepIndex = 0;
            if (compositeCoprimes.length > 0) {
                document.getElementById('compCurrentCoprime').textContent = compositeCoprimes[0];
            }
            document.getElementById('compSweepPlayBtn').textContent = 'Play Sweep';
            document.getElementById('compSweepPlayBtn').style.background = '#00ff00';
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
            ctx.rotate(compositeRotation * Math.PI / 180);
            
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
                    // Skip non-coprime if filter enabled
                    if (compositeShowCoprimeOnly && !point.isOpen) return;
                    
                    const x = baseRadius * Math.cos(point.angle);
                    const y = baseRadius * Math.sin(point.angle);
                    
                    const color = getPointColor(point);
                    let size = point.isOpen ? pointSize : pointSize * 1.1;
                    
                    // Highlight current sweep residue
                    const enableSweep = document.getElementById('compEnableSweep').checked;
                    if (enableSweep && point.isOpen) {
                        const currentIdx = Math.floor(compositeSweepIndex);
                        const currentCoprime = compositeCoprimes[currentIdx];
                        if (point.r === currentCoprime) {
                            size = pointSize * 2;
                            ctx.strokeStyle = '#ffff00';
                            ctx.lineWidth = 3 / compositeZoom;
                            ctx.beginPath();
                            ctx.arc(x, y, size / compositeZoom + 3, 0, 2 * Math.PI);
                            ctx.stroke();
                        }
                    }
                    
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, size / compositeZoom, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    // Store screen coordinates for hover detection
                    point.screenX = centerX + (x * compositeZoom * Math.cos(compositeRotation * Math.PI / 180) - y * compositeZoom * Math.sin(compositeRotation * Math.PI / 180));
                    point.screenY = centerY + (x * compositeZoom * Math.sin(compositeRotation * Math.PI / 180) + y * compositeZoom * Math.cos(compositeRotation * Math.PI / 180));
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

        // ===== QUADRATIC RESIDUES VISUALIZATION =====
        let qrPrime = 17;
        let qrPoints = [];
        let qrZoom = 1;
        let qrAnimationFrame = 0;
        let qrAnimationId = null;

        function initQuadraticResidues() {
            const slider = document.getElementById('qrModSlider');
            const input = document.getElementById('qrModInput');
            const pointSize = document.getElementById('qrPointSize');
            const canvas = document.getElementById('quadraticCanvas');
            const tooltip = document.getElementById('quadraticTooltip');
            const vizMode = document.getElementById('qrVisualizationMode');
            const showConn = document.getElementById('qrShowConnections');
            const animate = document.getElementById('qrAnimateSequence');
            
            slider.addEventListener('input', () => {
                let val = parseInt(slider.value);
                // Ensure it's an odd number
                if (val % 2 === 0) val++;
                // Find next prime if slider used, but allow any input via text box
                if (val <= 10000) {
                    while (!isPrime(val) && val < 10000) val += 2;
                }
                
                qrPrime = val;
                input.value = val;
                slider.value = Math.min(val, 10000);
                document.getElementById('qrModDisplay').textContent = val;
                updateQuadraticVisualization();
            });
            
            input.addEventListener('input', () => {
                let val = parseInt(input.value);
                if (!isNaN(val) && val >= 3) {
                    // Allow any prime, not just those under 10000
                    if (isPrime(val)) {
                        qrPrime = val;
                        slider.value = Math.min(val, 10000);
                        document.getElementById('qrModDisplay').textContent = val;
                        updateQuadraticVisualization();
                    }
                }
            });
            
            pointSize.addEventListener('input', () => {
                document.getElementById('qrPointSizeDisplay').textContent = 
                    parseFloat(pointSize.value).toFixed(1);
                drawQuadraticVisualization();
            });
            
            vizMode.addEventListener('change', () => {
                drawQuadraticVisualization();
            });
            
            showConn.addEventListener('change', () => {
                drawQuadraticVisualization();
            });
            
            animate.addEventListener('change', () => {
                if (animate.checked) {
                    startQRAnimation();
                } else {
                    stopQRAnimation();
                }
            });
            
            // Mouse wheel zoom
            canvas.addEventListener('wheel', (e) => {
                e.preventDefault();
                const delta = e.deltaY > 0 ? 0.9 : 1.1;
                qrZoom *= delta;
                qrZoom = Math.max(0.5, Math.min(5, qrZoom));
                drawQuadraticVisualization();
            });
            
            // Hover tooltip
            canvas.addEventListener('mousemove', (e) => {
                const rect = canvas.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                handleQRHover(x, y, e);
            });
            
            canvas.addEventListener('mouseleave', () => {
                tooltip.style.opacity = '0';
            });
            
            // Click handler
            canvas.addEventListener('click', (e) => {
                const rect = canvas.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                handleQRClick(x, y);
            });
            
            updateQuadraticVisualization();
        }

        function setQRPrime(p) {
            qrPrime = p;
            document.getElementById('qrModSlider').value = p;
            document.getElementById('qrModInput').value = p;
            document.getElementById('qrModDisplay').textContent = p;
            updateQuadraticVisualization();
        }

        function legendreSymbol(a, p) {
            if (a % p === 0) return 0;
            // Use Euler's criterion: (a|p) = a^((p-1)/2) mod p
            const exp = (p - 1) / 2;
            let result = 1;
            let base = a % p;
            let e = exp;
            
            while (e > 0) {
                if (e % 2 === 1) {
                    result = (result * base) % p;
                }
                base = (base * base) % p;
                e = Math.floor(e / 2);
            }
            
            return result === 1 ? 1 : -1;
        }

        function isQuadraticResidue(a, p) {
            if (a % p === 0) return true; // 0 is always a QR
            return legendreSymbol(a, p) === 1;
        }

        function updateQuadraticVisualization() {
            const p = qrPrime;
            
            // Generate points
            qrPoints = [];
            let qrCount = 0;
            let nrCount = 0;
            
            for (let a = 0; a < p; a++) {
                const angle = -2 * Math.PI * a / p;
                const isQR = isQuadraticResidue(a, p);
                const legendre = a === 0 ? 0 : legendreSymbol(a, p);
                
                // Find which square produces this (if QR)
                let squareRoot = -1;
                if (isQR && a !== 0) {
                    for (let x = 1; x <= (p - 1) / 2; x++) {
                        if ((x * x) % p === a) {
                            squareRoot = x;
                            break;
                        }
                    }
                }
                
                if (a !== 0) {
                    if (isQR) qrCount++;
                    else nrCount++;
                }
                
                qrPoints.push({
                    a: a,
                    p: p,
                    angle: angle,
                    isQR: isQR,
                    legendre: legendre,
                    squareRoot: squareRoot
                });
            }
            
            // Update statistics
            document.getElementById('qrPrime').textContent = p;
            document.getElementById('qrCount').textContent = qrCount;
            document.getElementById('nrCount').textContent = nrCount;
            const ratio = ((qrCount / (qrCount + nrCount)) * 100).toFixed(1);
            document.getElementById('qrRatio').textContent = ratio + '%';
            document.getElementById('qrMod4').textContent = p % 4;
            
            // Update analysis text
            let analysisHTML = `<p style="margin-bottom: 12px;"><strong>Prime p = ${p}</strong></p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">This prime has <strong>${qrCount} quadratic residues</strong> and <strong>${nrCount} non-residues</strong> among its ${p-1} non-zero elements.</p>`;
            
            if (p % 4 === 1) {
                analysisHTML += `<p style="margin-bottom: 12px;">Since p ≡ 1 (mod 4), we know that <strong>-1 is a quadratic residue</strong> mod ${p}. This means the equation x² ≡ -1 (mod ${p}) has solutions.</p>`;
            } else {
                analysisHTML += `<p style="margin-bottom: 12px;">Since p ≡ 3 (mod 4), we know that <strong>-1 is NOT a quadratic residue</strong> mod ${p}. The equation x² ≡ -1 (mod ${p}) has no solutions.</p>`;
            }
            
            const pMod8 = p % 8;
            if (pMod8 === 1 || pMod8 === 7) {
                analysisHTML += `<p style="margin-bottom: 12px;">Since p ≡ ±1 (mod 8), the number <strong>2 is a quadratic residue</strong> mod ${p}.</p>`;
            } else {
                analysisHTML += `<p style="margin-bottom: 12px;">Since p ≡ ±3 (mod 8), the number <strong>2 is NOT a quadratic residue</strong> mod ${p}.</p>`;
            }
            
            analysisHTML += `<p>The quadratic residues form a subgroup of index 2 in the multiplicative group (ℤ/${p}ℤ)×, which has order ${p-1}.</p>`;
            
            document.getElementById('qrAnalysisText').innerHTML = analysisHTML;
            
            // Update table
            updateQRTable();
            
            drawQuadraticVisualization();
        }

        function updateQRTable() {
            const tbody = document.getElementById('qrTableBody');
            tbody.innerHTML = '';
            
            for (let a = 1; a < qrPrime; a++) {
                const aSq = (a * a) % qrPrime;
                const leg = legendreSymbol(a, qrPrime);
                const isQR = leg === 1;
                
                const row = document.createElement('tr');
                row.style.background = isQR ? 'rgba(0, 255, 0, 0.1)' : 'rgba(255, 0, 100, 0.1)';
                
                row.innerHTML = `
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${a}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${aSq}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; font-weight: 600; color: ${leg === 1 ? '#00ff00' : '#ff0064'};">${leg > 0 ? '+1' : '-1'}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${isQR ? 'QR' : 'NR'}</td>
                `;
                
                tbody.appendChild(row);
            }
        }

        function drawQuadraticVisualization() {
            const canvas = document.getElementById('quadraticCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const baseRadius = Math.min(width, height) * 0.42;
            const radius = baseRadius * qrZoom;
            
            // Clear
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            const p = qrPrime;
            const pointSize = parseFloat(document.getElementById('qrPointSize').value);
            const vizMode = document.getElementById('qrVisualizationMode').value;
            const showConn = document.getElementById('qrShowConnections').checked;
            
            ctx.save();
            ctx.translate(centerX, centerY);
            ctx.scale(qrZoom, qrZoom);
            
            // Draw outer ring
            ctx.strokeStyle = '#ffffff';
            ctx.lineWidth = 2.5 / qrZoom;
            ctx.beginPath();
            ctx.arc(0, 0, baseRadius, 0, 2 * Math.PI);
            ctx.stroke();
            
            // Draw connections if enabled
            if (showConn && vizMode === 'square-sequence') {
                ctx.strokeStyle = 'rgba(0, 200, 255, 0.3)';
                ctx.lineWidth = 1.5 / qrZoom;
                
                for (let x = 1; x <= (p - 1) / 2; x++) {
                    const xSq = (x * x) % p;
                    const point1 = qrPoints.find(pt => pt.a === x);
                    const point2 = qrPoints.find(pt => pt.a === xSq);
                    
                    if (point1 && point2) {
                        const x1 = baseRadius * Math.cos(point1.angle);
                        const y1 = baseRadius * Math.sin(point1.angle);
                        const x2 = baseRadius * Math.cos(point2.angle);
                        const y2 = baseRadius * Math.sin(point2.angle);
                        
                        ctx.beginPath();
                        ctx.moveTo(x1, y1);
                        ctx.lineTo(x2, y2);
                        ctx.stroke();
                    }
                }
            }
            
            // Draw points
            qrPoints.forEach((point, idx) => {
                const x = baseRadius * Math.cos(point.angle);
                const y = baseRadius * Math.sin(point.angle);
                
                let color, size;
                
                if (point.a === 0) {
                    color = '#666666';
                    size = pointSize * 0.8;
                } else if (vizMode === 'residue-nonresidue' || vizMode === 'square-sequence') {
                    color = point.isQR ? '#00ff00' : '#ff0064';
                    size = pointSize;
                    
                    if (vizMode === 'square-sequence') {
                        // Highlight if this is currently being animated
                        const animIdx = Math.floor(qrAnimationFrame) % ((p - 1) / 2);
                        const currentSquare = ((animIdx + 1) * (animIdx + 1)) % p;
                        if (point.a === currentSquare || point.a === (animIdx + 1)) {
                            size = pointSize * 1.5;
                            color = '#00ffff';
                        }
                    }
                } else if (vizMode === 'legendre-symbol') {
                    if (point.legendre === 1) {
                        color = '#00ff00';
                    } else if (point.legendre === -1) {
                        color = '#ff0064';
                    } else {
                        color = '#666666';
                    }
                    size = pointSize;
                }
                
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, size / qrZoom, 0, 2 * Math.PI);
                ctx.fill();
                
                // Store screen coordinates
                point.screenX = centerX + x * qrZoom;
                point.screenY = centerY + y * qrZoom;
                point.screenRadius = size;
            });
            
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
            ctx.fillText(`Quadratic Residues mod ${p}`, width / 2, 30);
            
            // Zoom indicator
            ctx.font = '11px Arial';
            ctx.textAlign = 'right';
            ctx.fillText(`Zoom: ${(qrZoom * 100).toFixed(0)}%`, width - 10, height - 10);
        }

        function handleQRHover(x, y, e) {
            const tooltip = document.getElementById('quadraticTooltip');
            
            let hoveredPoint = null;
            let minDist = Infinity;
            
            qrPoints.forEach(point => {
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
                
                let html = `<strong>a = ${hoveredPoint.a}</strong><br>`;
                
                if (hoveredPoint.a === 0) {
                    html += `Zero (always QR)<br>`;
                    html += `(0|${hoveredPoint.p}) = 0`;
                } else {
                    html += `Legendre: (${hoveredPoint.a}|${hoveredPoint.p}) = ${hoveredPoint.legendre > 0 ? '+1' : '-1'}<br>`;
                    html += `<span style="color: ${hoveredPoint.isQR ? '#00ff00' : '#ff0064'};">${hoveredPoint.isQR ? 'QUADRATIC RESIDUE' : 'NON-RESIDUE'}</span><br>`;
                    
                    if (hoveredPoint.isQR && hoveredPoint.squareRoot > 0) {
                        html += `${hoveredPoint.squareRoot}² ≡ ${hoveredPoint.a} (mod ${hoveredPoint.p})`;
                    }
                }
                
                tooltip.innerHTML = html;
            } else {
                tooltip.style.opacity = '0';
            }
        }

        function handleQRClick(x, y) {
            let clickedPoint = null;
            let minDist = Infinity;
            
            qrPoints.forEach(point => {
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
                let message = `Residue a = ${clickedPoint.a} modulo p = ${clickedPoint.p}\n\n`;
                
                if (clickedPoint.a === 0) {
                    message += `Zero is always a quadratic residue.\n`;
                    message += `Legendre symbol: (0|${clickedPoint.p}) = 0`;
                } else {
                    message += `Legendre symbol: (${clickedPoint.a}|${clickedPoint.p}) = ${clickedPoint.legendre}\n\n`;
                    
                    if (clickedPoint.isQR) {
                        message += `Status: QUADRATIC RESIDUE\n\n`;
                        if (clickedPoint.squareRoot > 0) {
                            const neg = clickedPoint.p - clickedPoint.squareRoot;
                            message += `Square roots: ±${clickedPoint.squareRoot} ≡ ${clickedPoint.squareRoot}, ${neg} (mod ${clickedPoint.p})\n`;
                            message += `Verification: ${clickedPoint.squareRoot}² = ${clickedPoint.squareRoot * clickedPoint.squareRoot} ≡ ${clickedPoint.a} (mod ${clickedPoint.p})`;
                        }
                    } else {
                        message += `Status: NON-RESIDUE\n\n`;
                        message += `The equation x² ≡ ${clickedPoint.a} (mod ${clickedPoint.p}) has no solutions.`;
                    }
                }
                
                alert(message);
            }
        }

        function startQRAnimation() {
            if (!qrAnimationId) {
                qrAnimationFrame = 0;
                function animate() {
                    qrAnimationFrame += 0.05;
                    drawQuadraticVisualization();
                    qrAnimationId = requestAnimationFrame(animate);
                }
                qrAnimationId = requestAnimationFrame(animate);
            }
        }

        function stopQRAnimation() {
            if (qrAnimationId) {
                cancelAnimationFrame(qrAnimationId);
                qrAnimationId = null;
                qrAnimationFrame = 0;
                drawQuadraticVisualization();
            }
        }

        // ===== PRIMITIVE ROOTS VISUALIZATION =====
        let prModulus = 7;
        let prGenerator = 3;
        let prElements = [];
        let prAnimationFrame = 0;
        let prAnimationId = null;

        function initPrimitiveRoots() {
            const input = document.getElementById('prModInput');
            const slider = document.getElementById('prModSlider');
            const genSelect = document.getElementById('prGeneratorSelect');
            const vizMode = document.getElementById('prVisualizationMode');
            const showLines = document.getElementById('prShowPowerLines');
            const animate = document.getElementById('prAnimatePowers');
            
            slider.addEventListener('input', () => {
                const val = parseInt(slider.value);
                if (!isNaN(val) && val >= 2) {
                    prModulus = val;
                    input.value = val;
                    document.getElementById('prModDisplay').textContent = val;
                    updatePrimitiveRootsVisualization();
                }
            });
            
            input.addEventListener('input', () => {
                const val = parseInt(input.value);
                if (!isNaN(val) && val >= 2) {
                    prModulus = val;
                    slider.value = Math.min(val, 10000);
                    document.getElementById('prModDisplay').textContent = val;
                    updatePrimitiveRootsVisualization();
                }
            });
            
            genSelect.addEventListener('change', () => {
                const val = genSelect.value;
                if (val !== 'auto') {
                    prGenerator = parseInt(val);
                    drawPrimitiveRootsVisualization();
                }
            });
            
            vizMode.addEventListener('change', () => {
                drawPrimitiveRootsVisualization();
            });
            
            showLines.addEventListener('change', () => {
                drawPrimitiveRootsVisualization();
            });
            
            animate.addEventListener('change', () => {
                if (animate.checked) {
                    startPRAnimation();
                } else {
                    stopPRAnimation();
                }
            });
            
            updatePrimitiveRootsVisualization();
        }

        function setPRModulus(m) {
            prModulus = m;
            document.getElementById('prModInput').value = m;
            document.getElementById('prModDisplay').textContent = m;
            updatePrimitiveRootsVisualization();
        }

        function computeOrder(a, m) {
            if (gcd(a, m) !== 1) return 0;
            let order = 1;
            let power = a % m;
            while (power !== 1) {
                power = (power * a) % m;
                order++;
                if (order > m) return 0; // Safety check
            }
            return order;
        }

        function findPrimitiveRoots(m) {
            const phiM = phi(m);
            const roots = [];
            
            for (let a = 1; a < m; a++) {
                if (gcd(a, m) === 1 && computeOrder(a, m) === phiM) {
                    roots.push(a);
                }
            }
            
            return roots;
        }

        function hasPrimitiveRoot(m) {
            // m has primitive roots iff m = 1, 2, 4, p^k, or 2p^k where p is odd prime
            if (m === 1 || m === 2 || m === 4) return true;
            
            if (m % 2 === 0) {
                const halfM = m / 2;
                if (halfM % 2 === 0) return false;
                return isPrimePower(halfM);
            }
            
            return isPrimePower(m);
        }

        function isPrimePower(n) {
            if (n <= 1) return false;
            
            for (let p = 2; p * p <= n; p++) {
                if (n % p === 0) {
                    let temp = n;
                    while (temp % p === 0) {
                        temp /= p;
                    }
                    return temp === 1;
                }
            }
            return isPrime(n);
        }

        function updatePrimitiveRootsVisualization() {
            const m = prModulus;
            const phiM = phi(m);
            const roots = findPrimitiveRoots(m);
            const hasRoot = roots.length > 0;
            
            // Update generator select
            const genSelect = document.getElementById('prGeneratorSelect');
            genSelect.innerHTML = '<option value="auto">Auto (smallest)</option>';
            
            if (hasRoot) {
                roots.forEach(g => {
                    const option = document.createElement('option');
                    option.value = g;
                    option.textContent = `g = ${g}`;
                    genSelect.appendChild(option);
                });
                prGenerator = roots[0];
            }
            
            // Compute orders for all coprime elements
            prElements = [];
            for (let a = 1; a < m; a++) {
                if (gcd(a, m) === 1) {
                    const order = computeOrder(a, m);
                    const angle = -2 * Math.PI * a / m;
                    const isPrimRoot = order === phiM;
                    
                    prElements.push({
                        a: a,
                        m: m,
                        order: order,
                        angle: angle,
                        isPrimitiveRoot: isPrimRoot
                    });
                }
            }
            
            // Update statistics
            document.getElementById('prModulus').textContent = m;
            document.getElementById('prPhi').textContent = phiM;
            document.getElementById('prHasRoot').textContent = hasRoot ? 'Yes' : 'No';
            document.getElementById('prHasRoot').style.color = hasRoot ? '#00ff00' : '#ff0064';
            document.getElementById('prSmallest').textContent = hasRoot ? roots[0] : 'N/A';
            document.getElementById('prCount').textContent = roots.length;
            
            // Analysis text
            let analysisHTML = `<p style="margin-bottom: 12px;"><strong>Modulus m = ${m}</strong></p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">The group of units (ℤ/${m}ℤ)× has order φ(${m}) = ${phiM}.</p>`;
            
            if (hasRoot) {
                analysisHTML += `<p style="margin-bottom: 12px;"><strong>This modulus has primitive roots.</strong> There are ${roots.length} primitive root(s): {${roots.join(', ')}}.</p>`;
                analysisHTML += `<p style="margin-bottom: 12px;">The multiplicative group (ℤ/${m}ℤ)× is <strong>cyclic</strong>, generated by any primitive root.</p>`;
                analysisHTML += `<p style="margin-bottom: 12px;">For example, successive powers of g = ${roots[0]} cycle through all ${phiM} coprime residues before returning to 1.</p>`;
                
                // Show a few powers
                const g = roots[0];
                let powersStr = '';
                for (let k = 1; k <= Math.min(10, phiM); k++) {
                    const val = modPow(g, k, m);
                    powersStr += `${g}^${k} ≡ ${val} (mod ${m}), `;
                }
                if (phiM > 10) powersStr += '...';
                analysisHTML += `<p style="margin-bottom: 12px; font-size: 12px;">${powersStr}</p>`;
            } else {
                analysisHTML += `<p style="margin-bottom: 12px;"><strong>This modulus has NO primitive roots.</strong></p>`;
                analysisHTML += `<p style="margin-bottom: 12px;">The multiplicative group (ℤ/${m}ℤ)× is NOT cyclic. It decomposes as a direct product of cyclic groups.</p>`;
                
                // Show the orders that exist
                const orderCounts = {};
                prElements.forEach(el => {
                    orderCounts[el.order] = (orderCounts[el.order] || 0) + 1;
                });
                
                analysisHTML += `<p style="margin-bottom: 12px;">Element orders present: `;
                Object.keys(orderCounts).sort((a,b) => a-b).forEach(ord => {
                    analysisHTML += `ord=${ord} (${orderCounts[ord]} elements), `;
                });
                analysisHTML += `</p>`;
            }
            
            document.getElementById('prAnalysisText').innerHTML = analysisHTML;
            
            // Update order table
            updatePROrderTable();
            
            drawPrimitiveRootsVisualization();
        }

        function modPow(base, exp, mod) {
            let result = 1;
            base = base % mod;
            while (exp > 0) {
                if (exp % 2 === 1) {
                    result = (result * base) % mod;
                }
                base = (base * base) % mod;
                exp = Math.floor(exp / 2);
            }
            return result;
        }

        function updatePROrderTable() {
            const tbody = document.getElementById('prOrderTableBody');
            tbody.innerHTML = '';
            
            prElements.forEach(el => {
                const row = document.createElement('tr');
                row.style.background = el.isPrimitiveRoot ? 'rgba(255, 0, 255, 0.2)' : 'transparent';
                
                // Generate powers
                let powersStr = '';
                const g = el.a;
                const m = el.m;
                for (let k = 1; k <= Math.min(el.order, 8); k++) {
                    powersStr += modPow(g, k, m);
                    if (k < el.order && k < 8) powersStr += ', ';
                }
                if (el.order > 8) powersStr += '...';
                
                row.innerHTML = `
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${el.a}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; font-weight: 600;">${el.order}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); font-size: 10px;">${powersStr}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; color: ${el.isPrimitiveRoot ? '#ff00ff' : '#666'};">${el.isPrimitiveRoot ? 'YES' : 'no'}</td>
                `;
                
                tbody.appendChild(row);
            });
        }

        function drawPrimitiveRootsVisualization() {
            const canvas = document.getElementById('primitiveCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = Math.min(width, height) * 0.40;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            const m = prModulus;
            const vizMode = document.getElementById('prVisualizationMode').value;
            const showLines = document.getElementById('prShowPowerLines').checked;
            
            ctx.save();
            ctx.translate(centerX, centerY);
            
            // Draw ring
            ctx.strokeStyle = '#ffffff';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(0, 0, radius, 0, 2 * Math.PI);
            ctx.stroke();
            
            // Draw power connections if enabled
            if (showLines && vizMode === 'powers-sequence') {
                ctx.strokeStyle = 'rgba(255, 0, 255, 0.3)';
                ctx.lineWidth = 1.5;
                
                const g = prGenerator;
                for (let k = 0; k < phi(m); k++) {
                    const val1 = modPow(g, k, m);
                    const val2 = modPow(g, k + 1, m);
                    
                    const el1 = prElements.find(e => e.a === val1);
                    const el2 = prElements.find(e => e.a === val2);
                    
                    if (el1 && el2) {
                        const x1 = radius * Math.cos(el1.angle);
                        const y1 = radius * Math.sin(el1.angle);
                        const x2 = radius * Math.cos(el2.angle);
                        const y2 = radius * Math.sin(el2.angle);
                        
                        ctx.beginPath();
                        ctx.moveTo(x1, y1);
                        ctx.lineTo(x2, y2);
                        ctx.stroke();
                    }
                }
            }
            
            // Draw points
            prElements.forEach(el => {
                const x = radius * Math.cos(el.angle);
                const y = radius * Math.sin(el.angle);
                
                let color, size = 6;
                
                if (vizMode === 'orbit-structure' || vizMode === 'powers-sequence') {
                    color = el.isPrimitiveRoot ? '#ff00ff' : '#00ffff';
                    if (el.isPrimitiveRoot) size = 8;
                } else if (vizMode === 'order-coloring') {
                    const hue = (el.order / phi(m)) * 240;
                    color = `hsl(${hue}, 100%, 50%)`;
                }
                
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, size, 0, 2 * Math.PI);
                ctx.fill();
                
                el.screenX = centerX + x;
                el.screenY = centerY + y;
                el.screenRadius = size;
            });
            
            ctx.restore();
            
            // Center dot
            ctx.fillStyle = '#ffffff';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 3, 0, 2 * Math.PI);
            ctx.fill();
            
            // Title
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 18px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`Primitive Roots mod ${m}`, width / 2, 30);
        }

        function startPRAnimation() {
            if (!prAnimationId) {
                prAnimationFrame = 0;
                function animate() {
                    prAnimationFrame += 0.05;
                    drawPrimitiveRootsVisualization();
                    prAnimationId = requestAnimationFrame(animate);
                }
                prAnimationId = requestAnimationFrame(animate);
            }
        }

        function stopPRAnimation() {
            if (prAnimationId) {
                cancelAnimationFrame(prAnimationId);
                prAnimationId = null;
                prAnimationFrame = 0;
                drawPrimitiveRootsVisualization();
            }
        }

        // ===== MULTIPLICATION TABLE VISUALIZATION =====
        let mtModulus = 12;

        function initMultiplicationTable() {
            const slider = document.getElementById('mtModSlider');
            const input = document.getElementById('mtModInput');
            const tableType = document.getElementById('mtTableType');
            const colorScheme = document.getElementById('mtColorScheme');
            const cellSize = document.getElementById('mtCellSize');
            const showValues = document.getElementById('mtShowValues');
            const showSymm = document.getElementById('mtShowSymmetry');
            
            slider.addEventListener('input', () => {
                mtModulus = parseInt(slider.value);
                input.value = mtModulus;
                document.getElementById('mtModDisplay').textContent = mtModulus;
                updateMultiplicationTable();
            });
            
            input.addEventListener('input', () => {
                const val = parseInt(input.value);
                if (!isNaN(val) && val >= 2) {
                    mtModulus = val;
                    slider.value = Math.min(val, 10000);
                    document.getElementById('mtModDisplay').textContent = val;
                    updateMultiplicationTable();
                }
            });
            
            tableType.addEventListener('change', () => updateMultiplicationTable());
            colorScheme.addEventListener('change', () => drawMultiplicationTable());
            cellSize.addEventListener('input', () => {
                document.getElementById('mtCellSizeDisplay').textContent = cellSize.value;
                drawMultiplicationTable();
            });
            showValues.addEventListener('change', () => drawMultiplicationTable());
            showSymm.addEventListener('change', () => drawMultiplicationTable());
            
            updateMultiplicationTable();
        }

        function updateMultiplicationTable() {
            const m = mtModulus;
            
            // Count special elements
            const units = [];
            const zeroDivisors = [];
            const idempotents = [];
            
            for (let a = 0; a < m; a++) {
                if (gcd(a, m) === 1) units.push(a);
                
                // Check if zero divisor
                for (let b = 1; b < m; b++) {
                    if ((a * b) % m === 0 && a !== 0 && b !== 0) {
                        if (!zeroDivisors.includes(a)) zeroDivisors.push(a);
                        break;
                    }
                }
                
                // Check if idempotent (a² ≡ a)
                if ((a * a) % m === a) {
                    idempotents.push(a);
                }
            }
            
            // Update statistics
            document.getElementById('mtModulus').textContent = m;
            document.getElementById('mtUnits').textContent = units.length;
            document.getElementById('mtZeroDivisors').textContent = zeroDivisors.length;
            document.getElementById('mtIdempotents').textContent = idempotents.length;
            
            // Analysis
            let analysisHTML = `<p style="margin-bottom: 12px;"><strong>Modulus m = ${m}</strong></p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">The ring ℤ/${m}ℤ has ${m} elements: {0, 1, 2, ..., ${m-1}}.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">Units (invertible elements): ${units.length} = φ(${m})</p>`;
            
            if (zeroDivisors.length > 0) {
                analysisHTML += `<p style="margin-bottom: 12px;">This ring has ${zeroDivisors.length} zero divisor(s). It is NOT an integral domain.</p>`;
            } else {
                analysisHTML += `<p style="margin-bottom: 12px;">This ring has no zero divisors. It IS an integral domain (actually a field, since m is prime).</p>`;
            }
            
            analysisHTML += `<p style="margin-bottom: 12px;">Idempotent elements (a² = a): ${idempotents.length}</p>`;
            
            document.getElementById('mtAnalysisText').innerHTML = analysisHTML;
            
            // Special elements
            let specialHTML = `<p style="margin-bottom: 8px;"><strong>Units:</strong> {${units.join(', ')}}</p>`;
            if (zeroDivisors.length > 0) {
                specialHTML += `<p style="margin-bottom: 8px;"><strong>Zero Divisors:</strong> {${zeroDivisors.join(', ')}}</p>`;
            }
            specialHTML += `<p style="margin-bottom: 8px;"><strong>Idempotents:</strong> {${idempotents.join(', ')}}</p>`;
            
            // Nilpotents
            const nilpotents = [];
            for (let a = 0; a < m; a++) {
                let power = a;
                let isNilpotent = false;
                for (let k = 1; k <= 10; k++) {
                    if (power === 0) {
                        isNilpotent = true;
                        break;
                    }
                    power = (power * a) % m;
                }
                if (isNilpotent && a !== 0) nilpotents.push(a);
            }
            
            if (nilpotents.length > 0) {
                specialHTML += `<p style="margin-bottom: 8px;"><strong>Nilpotents:</strong> {${nilpotents.join(', ')}}</p>`;
            }
            
            document.getElementById('mtSpecialElements').innerHTML = specialHTML;
            
            drawMultiplicationTable();
        }

        function drawMultiplicationTable() {
            const canvas = document.getElementById('multiplicationCanvas');
            const ctx = canvas.getContext('2d');
            const m = mtModulus;
            const tableType = document.getElementById('mtTableType').value;
            const colorScheme = document.getElementById('mtColorScheme').value;
            const cellSize = parseInt(document.getElementById('mtCellSize').value);
            const showValues = document.getElementById('mtShowValues').checked;
            
            // Determine what elements to show
            let elements = [];
            if (tableType === 'full') {
                for (let i = 0; i < m; i++) elements.push(i);
            } else if (tableType === 'units') {
                for (let i = 1; i < m; i++) {
                    if (gcd(i, m) === 1) elements.push(i);
                }
            } else { // addition
                for (let i = 0; i < m; i++) elements.push(i);
            }
            
            const n = elements.length;
            const totalSize = n * cellSize;
            
            // Resize canvas
            canvas.width = totalSize + 40;
            canvas.height = totalSize + 40;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            const offsetX = 20;
            const offsetY = 20;
            
            // Draw table
            for (let i = 0; i < n; i++) {
                for (let j = 0; j < n; j++) {
                    const a = elements[i];
                    const b = elements[j];
                    let result;
                    
                    if (tableType === 'addition') {
                        result = (a + b) % m;
                    } else {
                        result = (a * b) % m;
                    }
                    
                    // Determine color
                    let color;
                    if (colorScheme === 'rainbow') {
                        const hue = (result / m) * 360;
                        color = `hsl(${hue}, 70%, 50%)`;
                    } else if (colorScheme === 'residue-class') {
                        const hue = (result % 12) * 30;
                        color = `hsl(${hue}, 70%, 50%)`;
                    } else if (colorScheme === 'zero-divisors') {
                        if (result === 0 && a !== 0 && b !== 0) {
                            color = '#ff0000';
                        } else if (gcd(result, m) === 1) {
                            color = '#00ff00';
                        } else {
                            color = '#666666';
                        }
                    } else if (colorScheme === 'idempotents') {
                        if (a === b && result === a) {
                            color = '#ffff00';
                        } else {
                            const hue = (result / m) * 360;
                            color = `hsl(${hue}, 70%, 50%)`;
                        }
                    }
                    
                    ctx.fillStyle = color;
                    ctx.fillRect(offsetX + j * cellSize, offsetY + i * cellSize, cellSize, cellSize);
                    
                    // Draw value
                    if (showValues && cellSize >= 15) {
                        ctx.fillStyle = '#000000';
                        ctx.font = `${Math.min(cellSize * 0.5, 12)}px Arial`;
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'middle';
                        ctx.fillText(result, offsetX + j * cellSize + cellSize / 2, offsetY + i * cellSize + cellSize / 2);
                    }
                }
            }
            
            // Draw grid
            ctx.strokeStyle = '#333333';
            ctx.lineWidth = 0.5;
            for (let i = 0; i <= n; i++) {
                ctx.beginPath();
                ctx.moveTo(offsetX, offsetY + i * cellSize);
                ctx.lineTo(offsetX + totalSize, offsetY + i * cellSize);
                ctx.stroke();
                
                ctx.beginPath();
                ctx.moveTo(offsetX + i * cellSize, offsetY);
                ctx.lineTo(offsetX + i * cellSize, offsetY + totalSize);
                ctx.stroke();
            }
        }
        
        // ===== CHINESE REMAINDER THEOREM VISUALIZER =====
        let crtSystem = [];
        let crtSolution = null;

        function initCRT() {
            const numEqs = document.getElementById('crtNumEqs');
            const vizMode = document.getElementById('crtVizMode');
            
            numEqs.addEventListener('change', () => {
                const n = parseInt(numEqs.value);
                document.getElementById('crtEq3').style.display = n >= 3 ? 'block' : 'none';
                document.getElementById('crtEq4').style.display = n >= 4 ? 'block' : 'none';
            });
            
            vizMode.addEventListener('change', () => {
                if (crtSolution !== null) {
                    drawCRTVisualization();
                }
            });
            
            // Add change listeners to all inputs
            for (let i = 1; i <= 4; i++) {
                const aInput = document.getElementById(`crt_a${i}`);
                const mInput = document.getElementById(`crt_m${i}`);
                if (aInput) aInput.addEventListener('change', () => { crtSolution = null; });
                if (mInput) mInput.addEventListener('change', () => { crtSolution = null; });
            }
            
            // Initial solve
            solveCRT();
        }

        function extendedGCD(a, b) {
            if (b === 0) return { gcd: a, x: 1, y: 0 };
            const result = extendedGCD(b, a % b);
            return {
                gcd: result.gcd,
                x: result.y,
                y: result.x - Math.floor(a / b) * result.y
            };
        }

        function modInverse(a, m) {
            const result = extendedGCD(a, m);
            if (result.gcd !== 1) return null;
            return ((result.x % m) + m) % m;
        }

        function solveCRT() {
            const numEqs = parseInt(document.getElementById('crtNumEqs').value);
            crtSystem = [];
            
            // Gather equations
            for (let i = 1; i <= numEqs; i++) {
                const a = parseInt(document.getElementById(`crt_a${i}`).value);
                const m = parseInt(document.getElementById(`crt_m${i}`).value);
                if (!isNaN(a) && !isNaN(m) && m > 0) {
                    crtSystem.push({ a: a % m, m: m });
                }
            }
            
            if (crtSystem.length < 2) {
                document.getElementById('crtSolution').textContent = 'Error: Need at least 2 congruences';
                return;
            }
            
            // Check pairwise coprimality
            for (let i = 0; i < crtSystem.length; i++) {
                for (let j = i + 1; j < crtSystem.length; j++) {
                    if (gcd(crtSystem[i].m, crtSystem[j].m) !== 1) {
                        document.getElementById('crtSolution').textContent = 
                            `Error: m${i+1} = ${crtSystem[i].m} and m${j+1} = ${crtSystem[j].m} are not coprime!`;
                        document.getElementById('crtSteps').innerHTML = 
                            `<p style="color: #ff0064;">The moduli must be pairwise coprime for CRT to apply.</p>`;
                        return;
                    }
                }
            }
            
            // Compute M = product of all moduli
            let M = 1;
            crtSystem.forEach(eq => { M *= eq.m; });
            
            // Apply CRT algorithm
            let x = 0;
            let steps = '<p><strong>Solution Steps:</strong></p>';
            steps += `<p>M = ${crtSystem.map(eq => eq.m).join(' × ')} = ${M}</p>`;
            
            crtSystem.forEach((eq, i) => {
                const Mi = M / eq.m;
                const yi = modInverse(Mi, eq.m);
                const term = eq.a * Mi * yi;
                x += term;
                
                steps += `<p style="margin-top: 10px;"><strong>For x ≡ ${eq.a} (mod ${eq.m}):</strong></p>`;
                steps += `<p>M${i+1} = M/m${i+1} = ${M}/${eq.m} = ${Mi}</p>`;
                steps += `<p>Find y${i+1}: ${Mi} × y${i+1} ≡ 1 (mod ${eq.m})</p>`;
                steps += `<p>y${i+1} = ${yi}</p>`;
                steps += `<p>Contribution: ${eq.a} × ${Mi} × ${yi} = ${term}</p>`;
            });
            
            x = ((x % M) + M) % M;
            crtSolution = x;
            
            steps += `<p style="margin-top: 15px;"><strong>Sum all contributions and reduce mod ${M}:</strong></p>`;
            steps += `<p style="color: #00ff00; font-size: 16px; font-weight: 600;">x ≡ ${x} (mod ${M})</p>`;
            
            // Verification
            steps += `<p style="margin-top: 15px;"><strong>Verification:</strong></p>`;
            let allCorrect = true;
            crtSystem.forEach((eq, i) => {
                const check = x % eq.m;
                const correct = check === eq.a;
                allCorrect = allCorrect && correct;
                steps += `<p>${x} mod ${eq.m} = ${check} ${correct ? '✓' : '✗ (expected ' + eq.a + ')'}</p>`;
            });
            
            document.getElementById('crtSolution').textContent = `Solution: x ≡ ${x} (mod ${M})`;
            document.getElementById('crtSteps').innerHTML = steps;
            
            drawCRTVisualization();
        }

        function drawCRTVisualization() {
            const canvas = document.getElementById('crtCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            if (crtSystem.length < 2 || crtSolution === null) return;
            
            const vizMode = document.getElementById('crtVizMode').value;
            
            if (vizMode === '2d-lattice' && crtSystem.length >= 2) {
                // 2D lattice visualization for 2 congruences
                const m1 = crtSystem[0].m;
                const m2 = crtSystem[1].m;
                const a1 = crtSystem[0].a;
                const a2 = crtSystem[1].a;
                
                const cellSize = Math.min(width / (m1 + 2), height / (m2 + 2));
                const offsetX = (width - m1 * cellSize) / 2;
                const offsetY = (height - m2 * cellSize) / 2;
                
                // Draw grid
                ctx.strokeStyle = '#333333';
                ctx.lineWidth = 0.5;
                for (let i = 0; i <= m1; i++) {
                    ctx.beginPath();
                    ctx.moveTo(offsetX + i * cellSize, offsetY);
                    ctx.lineTo(offsetX + i * cellSize, offsetY + m2 * cellSize);
                    ctx.stroke();
                }
                for (let j = 0; j <= m2; j++) {
                    ctx.beginPath();
                    ctx.moveTo(offsetX, offsetY + j * cellSize);
                    ctx.lineTo(offsetX + m1 * cellSize, offsetY + j * cellSize);
                    ctx.stroke();
                }
                
                // Highlight solutions
                for (let i = 0; i < m1; i++) {
                    for (let j = 0; j < m2; j++) {
                        const x = offsetX + i * cellSize;
                        const y = offsetY + (m2 - 1 - j) * cellSize;
                        
                        const meetsFirst = (i % m1) === a1;
                        const meetsSecond = (j % m2) === a2;
                        
                        if (meetsFirst && meetsSecond) {
                            ctx.fillStyle = '#00ff00';
                            ctx.fillRect(x, y, cellSize, cellSize);
                            
                            ctx.fillStyle = '#000000';
                            ctx.font = `${cellSize * 0.3}px Arial`;
                            ctx.textAlign = 'center';
                            ctx.textBaseline = 'middle';
                            const val = i + j * m1;
                            ctx.fillText(val % (m1 * m2), x + cellSize / 2, y + cellSize / 2);
                        } else if (meetsFirst) {
                            ctx.fillStyle = 'rgba(0, 255, 255, 0.3)';
                            ctx.fillRect(x, y, cellSize, cellSize);
                        } else if (meetsSecond) {
                            ctx.fillStyle = 'rgba(255, 0, 255, 0.3)';
                            ctx.fillRect(x, y, cellSize, cellSize);
                        }
                    }
                }
                
                // Labels
                ctx.fillStyle = '#ffffff';
                ctx.font = '14px Arial';
                ctx.textAlign = 'center';
                ctx.fillText(`x ≡ ${a1} (mod ${m1})`, width / 2, 25);
                
                ctx.save();
                ctx.translate(25, height / 2);
                ctx.rotate(-Math.PI / 2);
                ctx.fillText(`x ≡ ${a2} (mod ${m2})`, 0, 0);
                ctx.restore();
                
            } else if (vizMode === 'circles') {
                // Concentric circles representation
                const maxRadius = Math.min(width, height) * 0.40;
                const numEqs = crtSystem.length;
                
                ctx.save();
                ctx.translate(centerX, centerY);
                
                crtSystem.forEach((eq, idx) => {
                    const radius = maxRadius * (idx + 1) / numEqs;
                    
                    // Draw ring
                    ctx.strokeStyle = '#ffffff';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(0, 0, radius, 0, 2 * Math.PI);
                    ctx.stroke();
                    
                    // Draw points
                    for (let k = 0; k < eq.m; k++) {
                        const angle = -2 * Math.PI * k / eq.m;
                        const x = radius * Math.cos(angle);
                        const y = radius * Math.sin(angle);
                        
                        const isSolution = (k === eq.a);
                        ctx.fillStyle = isSolution ? '#00ff00' : '#666666';
                        ctx.beginPath();
                        ctx.arc(x, y, isSolution ? 6 : 3, 0, 2 * Math.PI);
                        ctx.fill();
                    }
                    
                    // Label
                    ctx.fillStyle = '#ffffff';
                    ctx.font = '12px Arial';
                    ctx.textAlign = 'center';
                    ctx.fillText(`m = ${eq.m}, a = ${eq.a}`, 0, -radius - 15);
                });
                
                ctx.restore();
                
            } else if (vizMode === 'number-line') {
                // Number line representation
                const M = crtSystem.reduce((prod, eq) => prod * eq.m, 1);
                const displayRange = Math.min(M, 100);
                const spacing = (width - 100) / displayRange;
                const y = height / 2;
                
                // Draw number line
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(50, y);
                ctx.lineTo(width - 50, y);
                ctx.stroke();
                
                // Draw ticks and highlight solutions
                for (let x = 0; x < displayRange; x++) {
                    const screenX = 50 + x * spacing;
                    
                    let meetsAll = true;
                    crtSystem.forEach(eq => {
                        if (x % eq.m !== eq.a) meetsAll = false;
                    });
                    
                    if (meetsAll) {
                        ctx.fillStyle = '#00ff00';
                        ctx.fillRect(screenX - 3, y - 20, 6, 40);
                        
                        ctx.fillStyle = '#00ff00';
                        ctx.font = 'bold 12px Arial';
                        ctx.textAlign = 'center';
                        ctx.fillText(x, screenX, y - 30);
                    } else {
                        ctx.strokeStyle = '#666666';
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(screenX, y - 5);
                        ctx.lineTo(screenX, y + 5);
                        ctx.stroke();
                    }
                }
                
                // Labels
                ctx.fillStyle = '#ffffff';
                ctx.font = '14px Arial';
                ctx.textAlign = 'left';
                let labelY = height - 100;
                crtSystem.forEach((eq, idx) => {
                    ctx.fillText(`x ≡ ${eq.a} (mod ${eq.m})`, 50, labelY);
                    labelY += 25;
                });
            }
        }

        // ===== CYCLOTOMIC POLYNOMIALS =====
        let cyclN = 12;
        let cyclRoots = [];
        let cyclAnimationId = null;
        let cyclRotation = 0;

        function initCyclotomic() {
            const slider = document.getElementById('cyclNSlider');
            const input = document.getElementById('cyclNInput');
            const vizMode = document.getElementById('cyclVizMode');
            const showConn = document.getElementById('cyclShowConnections');
            const showPoly = document.getElementById('cyclShowPolygon');
            const animate = document.getElementById('cyclAnimateRotation');
            
            slider.addEventListener('input', () => {
                cyclN = parseInt(slider.value);
                input.value = cyclN;
                document.getElementById('cyclNDisplay').textContent = cyclN;
                updateCyclotomicVisualization();
            });
            
            input.addEventListener('input', () => {
                const val = parseInt(input.value);
                if (!isNaN(val) && val >= 2) {
                    cyclN = val;
                    slider.value = Math.min(val, 60);
                    document.getElementById('cyclNDisplay').textContent = val;
                    updateCyclotomicVisualization();
                }
            });
            
            vizMode.addEventListener('change', () => drawCyclotomicVisualization());
            showConn.addEventListener('change', () => drawCyclotomicVisualization());
            showPoly.addEventListener('change', () => drawCyclotomicVisualization());
            
            animate.addEventListener('change', () => {
                if (animate.checked) {
                    startCyclAnimation();
                } else {
                    stopCyclAnimation();
                }
            });
            
            updateCyclotomicVisualization();
        }

        function setCyclN(n) {
            cyclN = n;
            document.getElementById('cyclNSlider').value = n;
            document.getElementById('cyclNInput').value = n;
            document.getElementById('cyclNDisplay').textContent = n;
            updateCyclotomicVisualization();
        }

        function computeOrderOfRoot(k, n) {
            const g = gcd(k, n);
            return n / g;
        }

        function cyclotomicPolynomial(n) {
            // Simplified: just return degree and a representation
            // Full computation would require polynomial arithmetic
            const phiN = phi(n);
            
            // For small n, we can hardcode
            const polys = {
                1: 'x - 1',
                2: 'x + 1',
                3: 'x² + x + 1',
                4: 'x² + 1',
                5: 'x⁴ + x³ + x² + x + 1',
                6: 'x² - x + 1',
                7: 'x⁶ + x⁵ + x⁴ + x³ + x² + x + 1',
                8: 'x⁴ + 1',
                9: 'x⁶ + x³ + 1',
                10: 'x⁴ - x³ + x² - x + 1',
                12: 'x⁴ - x² + 1',
                15: 'x⁸ - x⁷ + x⁵ - x⁴ + x³ - x + 1',
                16: 'x⁸ + 1',
                20: 'x⁸ - x⁶ + x⁴ - x² + 1',
                24: 'x⁸ - x⁴ + 1',
                30: 'x⁸ + x⁷ - x⁵ - x⁴ - x³ + x + 1'
            };
            
            if (polys[n]) {
                return polys[n];
            } else {
                return `Φ${n}(x) [degree ${phiN}]`;
            }
        }

        function updateCyclotomicVisualization() {
            const n = cyclN;
            const phiN = phi(n);
            
            // Generate all n-th roots of unity
            cyclRoots = [];
            for (let k = 0; k < n; k++) {
                const angle = 2 * Math.PI * k / n;
                const order = computeOrderOfRoot(k, n);
                const isPrimitive = order === n;
                
                cyclRoots.push({
                    k: k,
                    n: n,
                    angle: angle,
                    order: order,
                    isPrimitive: isPrimitive
                });
            }
            
            const primitiveCount = cyclRoots.filter(r => r.isPrimitive).length;
            
            // Update statistics
            document.getElementById('cyclOrder').textContent = n;
            document.getElementById('cyclPhi').textContent = phiN;
            document.getElementById('cyclAllRoots').textContent = n;
            document.getElementById('cyclPrimitive').textContent = primitiveCount;
            document.getElementById('cyclDegree').textContent = phiN;
            
            // Polynomial
            const poly = cyclotomicPolynomial(n);
            document.getElementById('cyclPolynomial').textContent = `Φ${n}(x) = ${poly}`;
            
            // Analysis
            let analysisHTML = `<p style="margin-bottom: 12px;">The ${n}-th roots of unity are the complex solutions to x${getSuper(n)} = 1.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">They form a cyclic group of order ${n} under multiplication.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">There are φ(${n}) = ${phiN} primitive ${n}-th roots of unity.</p>`;
            analysisHTML += `<p style="margin-bottom: 12px;">The cyclotomic polynomial Φ${n}(x) has degree ${phiN} and its roots are exactly the primitive ${n}-th roots.</p>`;
            
            if (isPrime(n)) {
                analysisHTML += `<p style="margin-bottom: 12px;"><strong>Since ${n} is prime</strong>, all non-identity roots are primitive.</p>`;
            }
            
            document.getElementById('cyclAnalysis').innerHTML = analysisHTML;
            
            // Roots table
            updateCyclRootsTable();
            
            // Factorization
            let factHTML = `<p>x${getSuper(n)} - 1 = `;
            const divisors = [];
            for (let d = 1; d <= n; d++) {
                if (n % d === 0) divisors.push(d);
            }
            factHTML += divisors.map(d => `Φ${d}(x)`).join(' × ');
            factHTML += `</p>`;
            
            document.getElementById('cyclFactorization').innerHTML = factHTML;
            
            drawCyclotomicVisualization();
        }

        function getSuper(n) {
            const supers = '⁰¹²³⁴⁵⁶⁷⁸⁹';
            return String(n).split('').map(d => supers[parseInt(d)]).join('');
        }

        function updateCyclRootsTable() {
            const tbody = document.getElementById('cyclRootsTableBody');
            tbody.innerHTML = '';
            
            cyclRoots.forEach(root => {
                const row = document.createElement('tr');
                row.style.background = root.isPrimitive ? 'rgba(255, 0, 255, 0.2)' : 'transparent';
                
                const angleStr = `${(root.angle * 180 / Math.PI).toFixed(1)}° = ${(root.k / root.n).toFixed(4)} × 2π`;
                
                row.innerHTML = `
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${root.k}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">e^(2πi × ${root.k}/${root.n})</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); font-size: 10px;">${angleStr}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${root.order}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; color: ${root.isPrimitive ? '#ff00ff' : '#666'};">${root.isPrimitive ? 'YES' : 'no'}</td>
                `;
                
                tbody.appendChild(row);
            });
        }

        function drawCyclotomicVisualization() {
            const canvas = document.getElementById('cyclotomicCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = Math.min(width, height) * 0.40;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            const n = cyclN;
            const vizMode = document.getElementById('cyclVizMode').value;
            const showConn = document.getElementById('cyclShowConnections').checked;
            const showPoly = document.getElementById('cyclShowPolygon').checked;
            
            ctx.save();
            ctx.translate(centerX, centerY);
            ctx.rotate(cyclRotation);
            
            // Draw unit circle
            ctx.strokeStyle = '#666666';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(0, 0, radius, 0, 2 * Math.PI);
            ctx.stroke();
            
            // Draw axes
            ctx.strokeStyle = '#333333';
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(-radius, 0);
            ctx.lineTo(radius, 0);
            ctx.stroke();
            ctx.beginPath();
            ctx.moveTo(0, -radius);
            ctx.lineTo(0, radius);
            ctx.stroke();
            
            // Draw polygon if enabled
            if (showPoly) {
                ctx.strokeStyle = 'rgba(0, 255, 255, 0.3)';
                ctx.lineWidth = 1.5;
                ctx.beginPath();
                cyclRoots.forEach((root, idx) => {
                    const x = radius * Math.cos(root.angle);
                    const y = radius * Math.sin(root.angle);
                    if (idx === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                });
                ctx.closePath();
                ctx.stroke();
            }
            
            // Draw connections if enabled
            if (showConn && vizMode === 'primitive-only') {
                const primRoots = cyclRoots.filter(r => r.isPrimitive);
                ctx.strokeStyle = 'rgba(255, 0, 255, 0.3)';
                ctx.lineWidth = 1;
                for (let i = 0; i < primRoots.length; i++) {
                    for (let j = i + 1; j < primRoots.length; j++) {
                        const r1 = primRoots[i];
                        const r2 = primRoots[j];
                        const x1 = radius * Math.cos(r1.angle);
                        const y1 = radius * Math.sin(r1.angle);
                        const x2 = radius * Math.cos(r2.angle);
                        const y2 = radius * Math.sin(r2.angle);
                        
                        ctx.beginPath();
                        ctx.moveTo(x1, y1);
                        ctx.lineTo(x2, y2);
                        ctx.stroke();
                    }
                }
            }
            
            // Draw roots
            cyclRoots.forEach(root => {
                const x = radius * Math.cos(root.angle);
                const y = radius * Math.sin(root.angle);
                
                let color, size = 5;
                let shouldDraw = true;
                
                if (vizMode === 'all-roots') {
                    color = root.isPrimitive ? '#ff00ff' : '#00ffff';
                    if (root.isPrimitive) size = 7;
                } else if (vizMode === 'primitive-only') {
                    if (!root.isPrimitive) shouldDraw = false;
                    color = '#ff00ff';
                    size = 7;
                } else if (vizMode === 'by-order') {
                    const hue = (root.order / n) * 360;
                    color = `hsl(${hue}, 100%, 50%)`;
                    size = 6;
                }
                
                if (shouldDraw) {
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, size, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    // Draw line to center for primitive roots
                    if (root.isPrimitive && vizMode !== 'primitive-only') {
                        ctx.strokeStyle = 'rgba(255, 0, 255, 0.2)';
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(0, 0);
                        ctx.lineTo(x, y);
                        ctx.stroke();
                    }
                }
            });
            
            ctx.restore();
            
            // Center dot
            ctx.fillStyle = '#ffffff';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 3, 0, 2 * Math.PI);
            ctx.fill();
            
            // Title
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 18px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`${n}-th Roots of Unity`, width / 2, 30);
        }

        function startCyclAnimation() {
            if (!cyclAnimationId) {
                function animate() {
                    cyclRotation += 0.01;
                    drawCyclotomicVisualization();
                    cyclAnimationId = requestAnimationFrame(animate);
                }
                cyclAnimationId = requestAnimationFrame(animate);
            }
        }

        function stopCyclAnimation() {
            if (cyclAnimationId) {
                cancelAnimationFrame(cyclAnimationId);
                cyclAnimationId = null;
                cyclRotation = 0;
                drawCyclotomicVisualization();
            }
        }

        // ===== EXPORT FUNCTIONS FOR ALL TABS =====
        
        function exportQRImage() {
            const includeLegend = document.getElementById('qrIncludeLegend').checked;
            const includeColorKey = document.getElementById('qrIncludeColorKey').checked;
            const includeTimestamp = document.getElementById('qrIncludeTimestamp').checked;
            const exportTitle = document.getElementById('qrExportTitle').value;
            const resolution = parseFloat(document.getElementById('qrExportResolution').value);
            
            const srcCanvas = document.getElementById('quadraticCanvas');
            const baseWidth = srcCanvas.width;
            const baseHeight = srcCanvas.height;
            
            // Reserve space for title at top
            const titleHeight = 100 * resolution;
            
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution + titleHeight;
            
            // Calculate legend dimensions
            let legendWidth = 0;
            if (includeLegend) {
                legendWidth = 500 * resolution;
                exportWidth += legendWidth;
            }
            
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Fill background
            const bgColor = '#000000';
            const textColor = '#ffffff';
            tempCtx.fillStyle = bgColor;
            tempCtx.fillRect(0, 0, exportWidth, exportHeight);
            
            // Draw title
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
            
            // Draw main visualization
            tempCtx.save();
            tempCtx.translate(0, titleHeight);
            tempCtx.scale(resolution, resolution);
            tempCtx.drawImage(srcCanvas, 0, 0);
            tempCtx.restore();
            
            // Draw legend if enabled
            if (includeLegend) {
                drawQRLegend(tempCtx, legendWidth, exportWidth, exportHeight, resolution, textColor, titleHeight, includeColorKey);
            }
            
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `quadratic_residues_p${qrPrime}_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawQRLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, titleHeight, includeColorKey) {
            const p = qrPrime;
            const vizMode = document.getElementById('qrVisualizationMode').value;
            
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const sectionSpacing = 15 * resolution;
            
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            
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
            
            // CONFIGURATION
            drawSectionHeader('CONFIGURATION');
            
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            
            ctx.fillText(`Prime Modulus: p = ${p}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Visualization Mode: ${vizMode}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Prime Factorization: ${p} (prime)`, startX, y);
            y += lineHeight;
            ctx.fillText(`p mod 4 = ${p % 4}`, startX, y);
            y += lineHeight;
            ctx.fillText(`p mod 8 = ${p % 8}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // STATISTICS
            drawSectionHeader('STATISTICS');
            
            const qrCount = qrPoints.filter(pt => pt.isQR && pt.a !== 0).length;
            const nrCount = p - 1 - qrCount;
            
            ctx.fillText(`Quadratic Residues: ${qrCount}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Non-Residues: ${nrCount}`, startX, y);
            y += lineHeight;
            ctx.fillText(`QR Ratio: ${(qrCount/(p-1)*100).toFixed(1)}%`, startX, y);
            y += lineHeight;
            ctx.fillText(`Total Non-Zero Elements: ${p-1}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // COLOR KEY
            if (includeColorKey) {
                drawSectionHeader('COLOR KEY');
                
                const items = [
                    { color: '#00ff00', label: 'Green = Quadratic Residues' },
                    { color: '#ff0064', label: 'Red = Non-Residues' },
                    { color: '#666666', label: 'Gray = Zero (always QR)' }
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
                
                y += sectionSpacing;
            }
            
            // KEY THEOREM
            drawSectionHeader('KEY THEOREM');
            
            ctx.font = `${fontSize * 0.95}px Arial`;
            const lines = [
                'Quadratic Reciprocity:',
                'For odd primes p and q:',
                '(p|q)(q|p) = (-1)^((p-1)(q-1)/4)',
                '',
                `For p=${p}:`,
                p % 4 === 1 ? '-1 IS a QR (p≡1 mod 4)' : '-1 NOT a QR (p≡3 mod 4)',
                (p % 8 === 1 || p % 8 === 7) ? '2 IS a QR (p≡±1 mod 8)' : '2 NOT a QR (p≡±3 mod 8)'
            ];
            
            lines.forEach(line => {
                ctx.fillText(line, startX, y);
                y += lineHeight;
            });
            
            y += sectionSpacing;
            
            // METADATA
            drawSectionHeader('METADATA');
            
            ctx.font = `${fontSize * 0.9}px Arial`;
            ctx.fillText(`Generated: ${new Date().toLocaleString()}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Author: Wessen Getachew`, startX, y);
            y += lineHeight;
            ctx.fillText(`Tool: Quadratic Residues`, startX, y);
            y += lineHeight;
            const resText = document.getElementById('qrExportResolution').selectedOptions[0].text;
            ctx.fillText(`Resolution: ${resText}`, startX, y);
        }

        function exportQRCSV() {
            let csv = '# Quadratic Residues Data Export\n';
            csv += `# Prime p = ${qrPrime}\n`;
            csv += `# Generated: ${new Date().toLocaleString()}\n#\n`;
            csv += 'Residue,Legendre_Symbol,Is_QR,Order,Square_Root\n';
            
            qrPoints.forEach(pt => {
                if (pt.a === 0) {
                    csv += `${pt.a},0,TRUE,N/A,0\n`;
                } else {
                    csv += `${pt.a},${pt.legendre},${pt.isQR},${pt.a},${pt.squareRoot || 'N/A'}\n`;
                }
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `quadratic_residues_p${qrPrime}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        function exportPRImage() {
            const includeLegend = document.getElementById('prIncludeLegend').checked;
            const includeColorKey = document.getElementById('prIncludeColorKey').checked;
            const includeTimestamp = document.getElementById('prIncludeTimestamp').checked;
            const title = document.getElementById('prExportTitle').value;
            const resolution = parseFloat(document.getElementById('prExportResolution').value);
            
            const srcCanvas = document.getElementById('primitiveCanvas');
            const baseWidth = srcCanvas.width;
            const baseHeight = srcCanvas.height;
            
            const titleHeight = 100 * resolution;
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution + titleHeight;
            
            let legendWidth = 0;
            if (includeLegend) {
                legendWidth = 500 * resolution;
                exportWidth += legendWidth;
            }
            
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const ctx = tempCanvas.getContext('2d');
            
            const bgColor = '#000000';
            const textColor = '#ffffff';
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, exportWidth, exportHeight);
            
            const fontSize = 18 * resolution;
            ctx.fillStyle = textColor;
            ctx.font = `bold ${fontSize * 1.8}px Arial`;
            ctx.textAlign = 'center';
            const titleY = titleHeight / 2 + fontSize / 2;
            ctx.fillText(title, exportWidth / 2, titleY);
            
            if (includeTimestamp) {
                ctx.font = `${fontSize * 0.8}px Arial`;
                const timestamp = new Date().toLocaleString();
                ctx.fillText(timestamp, exportWidth / 2, titleY + fontSize * 1.5);
            }
            
            ctx.save();
            ctx.translate(0, titleHeight);
            ctx.scale(resolution, resolution);
            ctx.drawImage(srcCanvas, 0, 0);
            ctx.restore();
            
            if (includeLegend) {
                drawPRLegend(ctx, legendWidth, exportWidth, exportHeight, resolution, textColor, titleHeight, includeColorKey);
            }
            
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `primitive_roots_m${prModulus}_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawPRLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, titleHeight, includeColorKey) {
            const m = prModulus;
            const phiM = phi(m);
            const roots = findPrimitiveRoots(m);
            const vizMode = document.getElementById('prVisualizationMode').value;
            
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const sectionSpacing = 15 * resolution;
            
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            
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
            
            drawSectionHeader('CONFIGURATION');
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            ctx.fillText(`Modulus: m = ${m}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Visualization Mode: ${vizMode}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Prime Factorization: ${primeFactorization(m)}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            drawSectionHeader('STATISTICS');
            ctx.fillText(`φ(${m}) = ${phiM}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Has Primitive Roots: ${roots.length > 0 ? 'Yes' : 'No'}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Number of Generators: ${roots.length}`, startX, y);
            y += lineHeight;
            if (roots.length > 0) {
                ctx.fillText(`Smallest Root: g = ${roots[0]}`, startX, y);
                y += lineHeight;
            }
            
            y += sectionSpacing;
            
            if (includeColorKey) {
                drawSectionHeader('COLOR KEY');
                const items = [
                    { color: '#ff00ff', label: 'Magenta = Primitive Roots' },
                    { color: '#00ffff', label: 'Cyan = Other Coprime Elements' }
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
                
                y += sectionSpacing;
            }
            
            drawSectionHeader('METADATA');
            ctx.font = `${fontSize * 0.9}px Arial`;
            ctx.fillText(`Generated: ${new Date().toLocaleString()}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Author: Wessen Getachew`, startX, y);
            y += lineHeight;
            ctx.fillText(`Tool: Primitive Roots`, startX, y);
        }

        function exportPRCSV() {
            let csv = '# Primitive Roots Data Export\n';
            csv += `# Modulus m = ${prModulus}\n`;
            csv += `# φ(m) = ${phi(prModulus)}\n#\n`;
            csv += 'Element,Order,Is_Primitive_Root\n';
            
            prElements.forEach(el => {
                csv += `${el.a},${el.order},${el.isPrimitiveRoot}\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `primitive_roots_m${prModulus}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        function exportMTImage() {
            const includeLegend = document.getElementById('mtIncludeLegend').checked;
            const includeColorKey = document.getElementById('mtIncludeColorKey').checked;
            const includeTimestamp = document.getElementById('mtIncludeTimestamp').checked;
            const exportTitle = document.getElementById('mtExportTitle').value;
            const resolution = parseFloat(document.getElementById('mtExportResolution').value);
            
            const srcCanvas = document.getElementById('multiplicationCanvas');
            const baseWidth = srcCanvas.width;
            const baseHeight = srcCanvas.height;
            
            // Reserve space for title at top
            const titleHeight = 100 * resolution;
            
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution + titleHeight;
            
            // Calculate legend dimensions
            let legendWidth = 0;
            if (includeLegend) {
                legendWidth = 500 * resolution;
                exportWidth += legendWidth;
            }
            
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Fill background
            const bgColor = '#000000';
            const textColor = '#ffffff';
            tempCtx.fillStyle = bgColor;
            tempCtx.fillRect(0, 0, exportWidth, exportHeight);
            
            // Draw title
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
            
            // Draw main visualization
            tempCtx.save();
            tempCtx.translate(0, titleHeight);
            tempCtx.scale(resolution, resolution);
            tempCtx.drawImage(srcCanvas, 0, 0);
            tempCtx.restore();
            
            // Draw legend if enabled
            if (includeLegend) {
                drawMTLegend(tempCtx, legendWidth, exportWidth, exportHeight, resolution, textColor, titleHeight, includeColorKey);
            }
            
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `multiplication_table_m${mtModulus}_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawMTLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, titleHeight, includeColorKey) {
            const m = mtModulus;
            const tableType = document.getElementById('mtTableType').value;
            const colorScheme = document.getElementById('mtColorScheme').value;
            
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const sectionSpacing = 15 * resolution;
            
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            
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
            
            // CONFIGURATION
            drawSectionHeader('CONFIGURATION');
            
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            
            ctx.fillText(`Modulus: m = ${m}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Table Type: ${tableType}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Color Scheme: ${colorScheme}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Prime Factorization: ${primeFactorization(m)}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // STATISTICS
            drawSectionHeader('STATISTICS');
            
            const units = [];
            for (let a = 0; a < m; a++) {
                if (gcd(a, m) === 1) units.push(a);
            }
            
            ctx.fillText(`φ(${m}) = ${units.length} units`, startX, y);
            y += lineHeight;
            ctx.fillText(`Total Elements: ${m}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Non-Units: ${m - units.length}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // COLOR KEY
            if (includeColorKey) {
                drawSectionHeader('COLOR KEY');
                
                ctx.font = `${fontSize * 0.95}px Arial`;
                
                if (colorScheme === 'rainbow') {
                    ctx.fillText('Colors map values 0 to m-1', startX, y);
                    y += lineHeight;
                    ctx.fillText('using rainbow hue spectrum', startX, y);
                    y += lineHeight;
                } else if (colorScheme === 'zero-divisors') {
                    const items = [
                        { color: '#ff0000', label: 'Red = Zero Divisors' },
                        { color: '#00ff00', label: 'Green = Units' },
                        { color: '#666666', label: 'Gray = Other Elements' }
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
                } else if (colorScheme === 'idempotents') {
                    ctx.fillText('Yellow = Idempotent (a² = a)', startX, y);
                    y += lineHeight;
                    ctx.fillText('Rainbow = Other values', startX, y);
                    y += lineHeight;
                }
                
                y += sectionSpacing;
            }
            
            // SPECIAL ELEMENTS
            drawSectionHeader('SPECIAL ELEMENTS');
            
            ctx.font = `${fontSize * 0.9}px Arial`;
            
            if (units.length <= 20) {
                ctx.fillText(`Units: {${units.join(', ')}}`, startX, y);
            } else {
                ctx.fillText(`Units: ${units.length} elements`, startX, y);
            }
            y += lineHeight;
            
            // Idempotents
            const idempotents = [];
            for (let a = 0; a < m; a++) {
                if ((a * a) % m === a) idempotents.push(a);
            }
            ctx.fillText(`Idempotents: {${idempotents.join(', ')}}`, startX, y);
            y += lineHeight;
            
            y += sectionSpacing;
            
            // METADATA
            drawSectionHeader('METADATA');
            
            ctx.font = `${fontSize * 0.9}px Arial`;
            ctx.fillText(`Generated: ${new Date().toLocaleString()}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Author: Wessen Getachew`, startX, y);
            y += lineHeight;
            ctx.fillText(`Tool: Multiplication Table`, startX, y);
            y += lineHeight;
            const resText = document.getElementById('mtExportResolution').selectedOptions[0].text;
            ctx.fillText(`Resolution: ${resText}`, startX, y);
        }

        function exportMTCSV() {
            const m = mtModulus;
            const tableType = document.getElementById('mtTableType').value;
            
            let csv = '# Multiplication Table Data Export\n';
            csv += `# Modulus m = ${m}\n`;
            csv += `# Table Type: ${tableType}\n#\n`;
            
            let elements = [];
            if (tableType === 'full') {
                for (let i = 0; i < m; i++) elements.push(i);
            } else if (tableType === 'units') {
                for (let i = 1; i < m; i++) {
                    if (gcd(i, m) === 1) elements.push(i);
                }
            }
            
            csv += ',' + elements.join(',') + '\n';
            elements.forEach(a => {
                csv += a;
                elements.forEach(b => {
                    const result = (a * b) % m;
                    csv += ',' + result;
                });
                csv += '\n';
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `multiplication_table_m${m}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        function exportCRTImage() {
            const title = document.getElementById('crtExportTitle').value;
            const resolution = parseFloat(document.getElementById('crtExportResolution').value);
            
            const srcCanvas = document.getElementById('crtCanvas');
            const baseWidth = srcCanvas.width;
            const baseHeight = srcCanvas.height;
            
            const titleHeight = 100 * resolution;
            const legendWidth = 500 * resolution;
            const exportWidth = baseWidth * resolution + legendWidth;
            const exportHeight = baseHeight * resolution + titleHeight;
            
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const ctx = tempCanvas.getContext('2d');
            
            const bgColor = '#000000';
            const textColor = '#ffffff';
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, exportWidth, exportHeight);
            
            const fontSize = 18 * resolution;
            ctx.fillStyle = textColor;
            ctx.font = `bold ${fontSize * 1.8}px Arial`;
            ctx.textAlign = 'center';
            const titleY = titleHeight / 2 + fontSize / 2;
            ctx.fillText(title, exportWidth / 2, titleY);
            
            ctx.font = `${fontSize * 0.8}px Arial`;
            const timestamp = new Date().toLocaleString();
            ctx.fillText(timestamp, exportWidth / 2, titleY + fontSize * 1.5);
            
            ctx.save();
            ctx.translate(0, titleHeight);
            ctx.scale(resolution, resolution);
            ctx.drawImage(srcCanvas, 0, 0);
            ctx.restore();
            
            drawCRTLegend(ctx, legendWidth, exportWidth, exportHeight, resolution, textColor, titleHeight);
            
            const link = document.createElement('a');
            const ts = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `crt_solution_${ts}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawCRTLegend(ctx, legendWidth, totalWidth, totalHeight, resolution, textColor, titleHeight) {
            const fontSize = 13 * resolution;
            const lineHeight = 18 * resolution;
            const padding = 25 * resolution;
            const startX = totalWidth - legendWidth + padding;
            
            let y = titleHeight + padding * 2;
            ctx.textAlign = 'left';
            ctx.font = `bold ${fontSize * 1.1}px Arial`;
            ctx.fillStyle = textColor;
            ctx.fillText('SYSTEM', startX, y);
            y += lineHeight * 1.5;
            
            ctx.font = `${fontSize}px Arial`;
            crtSystem.forEach((eq, i) => {
                ctx.fillText(`x ≡ ${eq.a} (mod ${eq.m})`, startX, y);
                y += lineHeight;
            });
            
            y += lineHeight;
            if (crtSolution !== null) {
                const M = crtSystem.reduce((p, eq) => p * eq.m, 1);
                ctx.font = `bold ${fontSize * 1.1}px Arial`;
                ctx.fillStyle = '#00ff00';
                ctx.fillText(`Solution: x ≡ ${crtSolution} (mod ${M})`, startX, y);
            }
        }

        function exportCRTCSV() {
            let csv = '# Chinese Remainder Theorem Solution\n';
            csv += `# Generated: ${new Date().toLocaleString()}\n#\n`;
            csv += 'Congruence,a_i,m_i\n';
            
            crtSystem.forEach((eq, i) => {
                csv += `${i + 1},${eq.a},${eq.m}\n`;
            });
            
            if (crtSolution !== null) {
                const M = crtSystem.reduce((prod, eq) => prod * eq.m, 1);
                csv += `\n# Solution: x ≡ ${crtSolution} (mod ${M})\n`;
            }
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `crt_solution_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        function exportCyclImage() {
            const title = document.getElementById('cyclExportTitle').value;
            const resolution = parseFloat(document.getElementById('cyclExportResolution').value);
            
            const srcCanvas = document.getElementById('cyclotomicCanvas');
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = srcCanvas.width * resolution;
            tempCanvas.height = srcCanvas.height * resolution + 100 * resolution;
            
            const ctx = tempCanvas.getContext('2d');
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, tempCanvas.width, tempCanvas.height);
            
            ctx.fillStyle = '#ffffff';
            ctx.font = `bold ${24 * resolution}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(title, tempCanvas.width / 2, 50 * resolution);
            
            ctx.save();
            ctx.translate(0, 100 * resolution);
            ctx.scale(resolution, resolution);
            ctx.drawImage(srcCanvas, 0, 0);
            ctx.restore();
            
            const link = document.createElement('a');
            link.download = `cyclotomic_n${cyclN}_${Date.now()}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function exportCyclCSV() {
            let csv = '# Cyclotomic Roots Data Export\n';
            csv += `# Order n = ${cyclN}\n`;
            csv += `# φ(n) = ${phi(cyclN)}\n#\n`;
            csv += 'k,Angle_Degrees,Angle_Radians,Order,Is_Primitive\n';
            
            cyclRoots.forEach(root => {
                const angleDeg = (root.angle * 180 / Math.PI).toFixed(4);
                const angleRad = root.angle.toFixed(6);
                csv += `${root.k},${angleDeg},${angleRad},${root.order},${root.isPrimitive}\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `cyclotomic_n${cyclN}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        // ===== DIRICHLET CHARACTERS =====
        let dirModulus = 12;
        let dirCharacters = [];
        let dirCurrentChar = 0;
        let dirUpdateTimeout = null;
        let dirAnimationId = null;

        function initDirichlet() {
            const slider = document.getElementById('dirModSlider');
            const input = document.getElementById('dirModInput');
            const vizMode = document.getElementById('dirVizMode');
            const showPhases = document.getElementById('dirShowPhases');
            const animate = document.getElementById('dirAnimateRotation');
            
            slider.addEventListener('input', () => {
                const val = parseInt(slider.value);
                dirModulus = val;
                input.value = val;
                document.getElementById('dirModDisplay').textContent = val;
                
                // More aggressive debouncing - only update on mouseup
                clearTimeout(dirUpdateTimeout);
            });
            
            slider.addEventListener('change', () => {
                // This fires when user releases the slider
                clearTimeout(dirUpdateTimeout);
                dirUpdateTimeout = setTimeout(() => {
                    updateDirichletVisualization();
                }, 50);
            });
            
            input.addEventListener('input', () => {
                const val = parseInt(input.value);
                if (!isNaN(val) && val >= 3 && val <= 10000) {
                    dirModulus = val;
                    slider.value = Math.min(val, 10000);
                    document.getElementById('dirModDisplay').textContent = val;
                    
                    clearTimeout(dirUpdateTimeout);
                    dirUpdateTimeout = setTimeout(() => {
                        updateDirichletVisualization();
                    }, 500);
                }
            });
            
            if (vizMode) {
                vizMode.addEventListener('change', () => {
                    drawDirichletVisualization();
                });
            }
            
            if (showPhases) {
                showPhases.addEventListener('change', () => {
                    drawDirichletVisualization();
                });
            }
            
            if (animate) {
                animate.addEventListener('change', () => {
                    if (animate.checked) {
                        startDirAnimation();
                    } else {
                        stopDirAnimation();
                    }
                });
            }
            
            updateDirichletVisualization();
        }
        
        function startDirAnimation() {
            // Placeholder - animation not implemented yet
        }
        
        function stopDirAnimation() {
            if (dirAnimationId) {
                cancelAnimationFrame(dirAnimationId);
                dirAnimationId = null;
            }
        }

        function updateDirichletVisualization() {
            const q = dirModulus;
            const phiQ = phi(q);
            
            document.getElementById('dirModulus').textContent = q;
            document.getElementById('dirPhi').textContent = phiQ;
            document.getElementById('dirCharCount').textContent = phiQ;
            document.getElementById('dirCharType').textContent = 'Principal';
            
            let analysis = `<p>The modulus q = ${q} has φ(${q}) = ${phiQ} Dirichlet characters.</p>`;
            analysis += `<p>Characters are multiplicative functions χ: (ℤ/${q}ℤ)× → ℂ*.</p>`;
            analysis += `<p>The principal character χ₀(n) = 1 if gcd(n,${q})=1, else 0.</p>`;
            
            document.getElementById('dirAnalysis').innerHTML = analysis;
            
            // Only update table for reasonable sizes to avoid freezing
            const tbody = document.getElementById('dirTableBody');
            if (q <= 100) {
                tbody.innerHTML = '';
                
                for (let n = 1; n <= q; n++) {
                    const g = gcd(n, q);
                    const chiN = g === 1 ? 1 : 0;
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${n}</td>
                        <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${g}</td>
                        <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; font-weight: 600;">${chiN}</td>
                        <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${chiN}</td>
                        <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">0°</td>
                    `;
                    tbody.appendChild(row);
                }
            } else {
                tbody.innerHTML = '<tr><td colspan="5" style="padding: 20px; text-align: center;">Table hidden for large moduli (q > 100). Use visualization instead.</td></tr>';
            }
            
            drawDirichletVisualization();
        }

        function drawDirichletVisualization() {
            const canvas = document.getElementById('dirichletCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = Math.min(width, height) * 0.40;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            const q = dirModulus;
            const vizMode = document.getElementById('dirVizMode').value;
            const showPhases = document.getElementById('dirShowPhases').checked;
            
            // Limit visualization complexity for large moduli
            const maxPoints = 500;
            const step = q > maxPoints ? Math.ceil(q / maxPoints) : 1;
            
            if (vizMode === 'character-values') {
                // Ring visualization with character values
                ctx.save();
                ctx.translate(centerX, centerY);
                
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(0, 0, radius, 0, 2 * Math.PI);
                ctx.stroke();
                
                for (let n = 1; n < q; n += step) {
                    const angle = -2 * Math.PI * n / q;
                    const x = radius * Math.cos(angle);
                    const y = radius * Math.sin(angle);
                    
                    const g = gcd(n, q);
                    const color = g === 1 ? '#00ff00' : '#ff0064';
                    const size = g === 1 ? 6 : 3;
                    
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, size, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    // Show phase lines for coprime elements (limit to avoid clutter)
                    if (showPhases && g === 1 && q <= 100) {
                        ctx.strokeStyle = 'rgba(0, 255, 0, 0.3)';
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(0, 0);
                        ctx.lineTo(x, y);
                        ctx.stroke();
                    }
                }
                
                ctx.restore();
                
            } else if (vizMode === 'character-table') {
                // Character table as a grid visualization
                const phiQ = phi(q);
                const cellSize = Math.min(40, (width - 100) / phiQ);
                const startX = (width - phiQ * cellSize) / 2;
                const startY = 100;
                
                // Get coprime elements
                const coprimes = [];
                for (let n = 1; n < q; n++) {
                    if (gcd(n, q) === 1) coprimes.push(n);
                }
                
                // Draw grid
                ctx.font = `${Math.min(cellSize * 0.4, 12)}px Arial`;
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                
                coprimes.forEach((n, idx) => {
                    const x = startX + idx * cellSize;
                    const y = startY;
                    
                    // Cell background
                    ctx.fillStyle = '#00ff00';
                    ctx.fillRect(x, y, cellSize - 2, cellSize - 2);
                    
                    // Value
                    ctx.fillStyle = '#000000';
                    ctx.fillText('1', x + cellSize / 2, y + cellSize / 2);
                    
                    // Label below
                    ctx.fillStyle = '#ffffff';
                    ctx.fillText(n.toString(), x + cellSize / 2, y + cellSize + 15);
                });
                
                // Title
                ctx.fillStyle = '#ffffff';
                ctx.font = '14px Arial';
                ctx.fillText('Principal Character χ₀(n) = 1 for gcd(n,q)=1', width / 2, startY - 30);
                
            } else if (vizMode === 'orthogonality') {
                // Orthogonality visualization as vectors
                ctx.save();
                ctx.translate(centerX, centerY);
                
                // Draw unit circle
                ctx.strokeStyle = '#666666';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(0, 0, radius, 0, 2 * Math.PI);
                ctx.stroke();
                
                // Draw axes
                ctx.strokeStyle = '#333333';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(-radius * 1.2, 0);
                ctx.lineTo(radius * 1.2, 0);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(0, -radius * 1.2);
                ctx.lineTo(0, radius * 1.2);
                ctx.stroke();
                
                // For principal character, all vectors point to +1
                const coprimes = [];
                for (let n = 1; n < q; n++) {
                    if (gcd(n, q) === 1) coprimes.push(n);
                }
                
                // Draw vectors
                coprimes.forEach((n, idx) => {
                    const angle = (2 * Math.PI * idx) / coprimes.length;
                    const vecRadius = radius * 0.6;
                    const baseX = vecRadius * Math.cos(angle);
                    const baseY = vecRadius * Math.sin(angle);
                    
                    // Vector from base position to +1 on real axis
                    const targetX = radius * 0.8;
                    const targetY = 0;
                    
                    ctx.strokeStyle = `hsl(${(idx / coprimes.length) * 360}, 70%, 50%)`;
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.moveTo(baseX, baseY);
                    ctx.lineTo(targetX, targetY);
                    ctx.stroke();
                    
                    // Arrow head
                    const dx = targetX - baseX;
                    const dy = targetY - baseY;
                    const len = Math.sqrt(dx * dx + dy * dy);
                    const arrowLen = 10;
                    const arrowAngle = Math.atan2(dy, dx);
                    
                    ctx.fillStyle = ctx.strokeStyle;
                    ctx.beginPath();
                    ctx.moveTo(targetX, targetY);
                    ctx.lineTo(
                        targetX - arrowLen * Math.cos(arrowAngle - Math.PI / 6),
                        targetY - arrowLen * Math.sin(arrowAngle - Math.PI / 6)
                    );
                    ctx.lineTo(
                        targetX - arrowLen * Math.cos(arrowAngle + Math.PI / 6),
                        targetY - arrowLen * Math.sin(arrowAngle + Math.PI / 6)
                    );
                    ctx.closePath();
                    ctx.fill();
                });
                
                // Mark +1 point
                ctx.fillStyle = '#00ff00';
                ctx.beginPath();
                ctx.arc(radius * 0.8, 0, 8, 0, 2 * Math.PI);
                ctx.fill();
                
                ctx.restore();
                
            } else if (vizMode === 'l-function') {
                // L-function partial sums visualization
                const maxN = Math.min(50, q * 3);
                const padding = 50;
                const graphWidth = width - 2 * padding;
                const graphHeight = height - 2 * padding - 50;
                
                // Calculate partial sums
                let partialSums = [];
                let sum = 0;
                for (let n = 1; n <= maxN; n++) {
                    const g = gcd(n, q);
                    const chiN = g === 1 ? 1 : 0;
                    sum += chiN / n; // Simple L(1, χ₀) partial sum
                    partialSums.push({ n, sum });
                }
                
                const maxSum = Math.max(...partialSums.map(p => p.sum));
                const minSum = Math.min(...partialSums.map(p => p.sum));
                const sumRange = maxSum - minSum || 1;
                
                // Draw axes
                ctx.strokeStyle = '#ffffff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(padding, height - padding);
                ctx.lineTo(width - padding, height - padding);
                ctx.stroke();
                ctx.beginPath();
                ctx.moveTo(padding, padding);
                ctx.lineTo(padding, height - padding);
                ctx.stroke();
                
                // Draw curve
                ctx.strokeStyle = '#00ffff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                partialSums.forEach((p, idx) => {
                    const x = padding + (p.n / maxN) * graphWidth;
                    const y = height - padding - ((p.sum - minSum) / sumRange) * graphHeight;
                    
                    if (idx === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                });
                ctx.stroke();
                
                // Labels
                ctx.fillStyle = '#ffffff';
                ctx.font = '12px Arial';
                ctx.textAlign = 'center';
                ctx.fillText('n', width - padding / 2, height - padding + 20);
                
                ctx.save();
                ctx.translate(padding - 30, height / 2);
                ctx.rotate(-Math.PI / 2);
                ctx.fillText('L(1, χ₀) partial sum', 0, 0);
                ctx.restore();
                
                // Value labels
                ctx.textAlign = 'right';
                ctx.fillText(maxSum.toFixed(3), padding - 5, padding + 10);
                ctx.fillText(minSum.toFixed(3), padding - 5, height - padding);
            }
            
            // Title
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 18px Arial';
            ctx.textAlign = 'center';
            const modeText = vizMode === 'character-values' ? 'Character Values' :
                           vizMode === 'character-table' ? 'Character Table' :
                           vizMode === 'orthogonality' ? 'Orthogonality Relations' : 'L-function Partial Sums';
            ctx.fillText(`${modeText} (mod ${q})`, width / 2, 30);
        }

        function exportDirImage() {
            const title = document.getElementById('dirExportTitle').value;
            const resolution = parseFloat(document.getElementById('dirExportResolution').value);
            const srcCanvas = document.getElementById('dirichletCanvas');
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = srcCanvas.width * resolution;
            tempCanvas.height = srcCanvas.height * resolution + 100 * resolution;
            
            const ctx = tempCanvas.getContext('2d');
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, tempCanvas.width, tempCanvas.height);
            ctx.fillStyle = '#ffffff';
            ctx.font = `bold ${24 * resolution}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(title, tempCanvas.width / 2, 50 * resolution);
            ctx.save();
            ctx.translate(0, 100 * resolution);
            ctx.scale(resolution, resolution);
            ctx.drawImage(srcCanvas, 0, 0);
            ctx.restore();
            
            const link = document.createElement('a');
            link.download = `dirichlet_q${dirModulus}_${Date.now()}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function exportDirCSV() {
            let csv = '# Dirichlet Characters Export\n';
            csv += `# Modulus q = ${dirModulus}\n#\n`;
            csv += 'n,gcd(n,q),chi(n)\n';
            
            for (let n = 1; n <= dirModulus; n++) {
                const g = gcd(n, dirModulus);
                const chiN = g === 1 ? 1 : 0;
                csv += `${n},${g},${chiN}\n`;
            }
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `dirichlet_q${dirModulus}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        // ===== MÖBIUS FUNCTION =====
        let mobMax = 60;
        let mobValues = [];

        function initMobius() {
            const slider = document.getElementById('mobMaxSlider');
            const input = document.getElementById('mobMaxInput');
            
            slider.addEventListener('input', () => {
                mobMax = parseInt(slider.value);
                input.value = mobMax;
                document.getElementById('mobMaxDisplay').textContent = mobMax;
                updateMobiusVisualization();
            });
            
            input.addEventListener('input', () => {
                const val = parseInt(input.value);
                if (!isNaN(val) && val >= 10) {
                    mobMax = val;
                    slider.value = Math.min(val, 10000);
                    document.getElementById('mobMaxDisplay').textContent = val;
                    updateMobiusVisualization();
                }
            });
            
            updateMobiusVisualization();
        }

        function mobiusFunction(n) {
            if (n === 1) return 1;
            
            let primeFactors = [];
            let temp = n;
            
            for (let p = 2; p * p <= temp; p++) {
                if (temp % p === 0) {
                    let count = 0;
                    while (temp % p === 0) {
                        count++;
                        temp /= p;
                    }
                    if (count > 1) return 0;
                    primeFactors.push(p);
                }
            }
            if (temp > 1) primeFactors.push(temp);
            
            return primeFactors.length % 2 === 0 ? 1 : -1;
        }

        function updateMobiusVisualization() {
            const n = mobMax;
            mobValues = [];
            
            let sum = 0;
            let plusOne = 0;
            let minusOne = 0;
            let zero = 0;
            
            for (let i = 1; i <= n; i++) {
                const mu = mobiusFunction(i);
                mobValues.push({ n: i, mu: mu, sum: sum + mu });
                sum += mu;
                
                if (mu === 1) plusOne++;
                else if (mu === -1) minusOne++;
                else zero++;
            }
            
            document.getElementById('mobRange').textContent = `1 to ${n}`;
            document.getElementById('mobSum').textContent = sum;
            document.getElementById('mobPlusOne').textContent = plusOne;
            document.getElementById('mobMinusOne').textContent = minusOne;
            document.getElementById('mobZero').textContent = zero;
            
            let analysis = `<p>The Möbius function μ(n) is defined as:</p>`;
            analysis += `<p>μ(n) = 1 if n is square-free with even number of prime factors</p>`;
            analysis += `<p>μ(n) = -1 if n is square-free with odd number of prime factors</p>`;
            analysis += `<p>μ(n) = 0 if n has a squared prime factor</p>`;
            analysis += `<p>Mertens function M(x) = Σμ(n) for n≤x: M(${n}) = ${sum}</p>`;
            
            document.getElementById('mobAnalysis').innerHTML = analysis;
            
            const tbody = document.getElementById('mobTableBody');
            tbody.innerHTML = '';
            
            mobValues.forEach(val => {
                const factors = primeFactorization(val.n);
                const row = document.createElement('tr');
                const color = val.mu === 1 ? '#00ff00' : val.mu === -1 ? '#ff0064' : '#666666';
                row.style.background = `${color}22`;
                
                row.innerHTML = `
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${val.n}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); font-size: 10px;">${factors}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center; font-weight: 600; color: ${color};">${val.mu}</td>
                    <td style="padding: 6px; border: 1px solid var(--border-color); text-align: center;">${val.sum}</td>
                `;
                tbody.appendChild(row);
            });
            
            drawMobiusVisualization();
        }

        function drawMobiusVisualization() {
            const canvas = document.getElementById('mobiusCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.42;
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);
            
            ctx.save();
            ctx.translate(centerX, centerY);
            
            mobValues.forEach((val, idx) => {
                const m = Math.floor(Math.sqrt(mobMax)) + 1;
                const ringIdx = Math.floor(idx / m);
                const posInRing = idx % m;
                const radius = (ringIdx + 1) * (maxRadius / Math.ceil(mobMax / m));
                const angle = -2 * Math.PI * posInRing / m;
                
                const x = radius * Math.cos(angle);
                const y = radius * Math.sin(angle);
                
                let color, size;
                if (val.mu === 1) {
                    color = '#00ff00';
                    size = 5;
                } else if (val.mu === -1) {
                    color = '#ff0064';
                    size = 5;
                } else {
                    color = '#666666';
                    size = 3;
                }
                
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(x, y, size, 0, 2 * Math.PI);
                ctx.fill();
            });
            
            ctx.restore();
            
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 18px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`Möbius Function μ(n) for n ≤ ${mobMax}`, width / 2, 30);
        }

        function exportMobImage() {
            const title = document.getElementById('mobExportTitle').value;
            const resolution = parseFloat(document.getElementById('mobExportResolution').value);
            const srcCanvas = document.getElementById('mobiusCanvas');
            const tempCanvas = document.createElement('canvas');
            tempCanvas.width = srcCanvas.width * resolution;
            tempCanvas.height = srcCanvas.height * resolution + 100 * resolution;
            
            const ctx = tempCanvas.getContext('2d');
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, tempCanvas.width, tempCanvas.height);
            ctx.fillStyle = '#ffffff';
            ctx.font = `bold ${24 * resolution}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(title, tempCanvas.width / 2, 50 * resolution);
            ctx.save();
            ctx.translate(0, 100 * resolution);
            ctx.scale(resolution, resolution);
            ctx.drawImage(srcCanvas, 0, 0);
            ctx.restore();
            
            const link = document.createElement('a');
            link.download = `mobius_n${mobMax}_${Date.now()}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function exportMobCSV() {
            let csv = '# Möbius Function Export\n';
            csv += `# Range: 1 to ${mobMax}\n#\n`;
            csv += 'n,Prime_Factorization,mu(n),M(n)\n';
            
            mobValues.forEach(val => {
                const factors = primeFactorization(val.n);
                csv += `${val.n},"${factors}",${val.mu},${val.sum}\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const link = document.createElement('a');
            link.download = `mobius_n${mobMax}_${Date.now()}.csv`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }
    </script>
</body>
</html>
