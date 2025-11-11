<!DOCTYPE html>
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
            <button class="theme-toggle" onclick="toggleTheme()">
                <span id="themeText">Light Mode</span>
            </button>
        </div>

        <div class="main-content">
                <div class="control-panel">
                    <div class="control-section">
                        <h3>Modulus Configuration</h3>
                        
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

                    <div class="control-section">
                        <h3>Connection Lines</h3>
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

                    <div class="control-section">
                        <h3>Rotation Controls</h3>
                        
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
                            <label>Per-Ring Spiral <span class="range-display" id="perRingRotDisplay">0</span>° per ring</label>
                            <div class="dual-input">
                                <input type="range" id="perRingRot" min="-360" max="360" step="1" value="0">
                                <input type="number" id="perRingRotNum" min="-720" max="720" step="1" value="0">
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label>Spiral Mode</label>
                            <select id="spiralMode">
                                <option value="linear">Linear (Constant Step)</option>
                                <option value="fibonacci">Fibonacci (Golden Spiral)</option>
                                <option value="logarithmic">Logarithmic (Exponential)</option>
                                <option value="sine-wave">Sine Wave</option>
                            </select>
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
                        
                        <div class="preset-grid" style="margin-top: 10px;">
                            <button onclick="setSpiralPreset('gentle')">Gentle Spiral</button>
                            <button onclick="setSpiralPreset('moderate')">Moderate</button>
                            <button onclick="setSpiralPreset('strong')">Strong Twist</button>
                            <button onclick="setSpiralPreset('golden')">Golden Ratio</button>
                            <button onclick="setSpiralPreset('galaxy')">Galaxy</button>
                            <button onclick="setSpiralPreset('helix')">DNA Helix</button>
                        </div>
                        
                        <div class="info-box" id="animationStatus">
                            Status: Stopped
                        </div>
                    </div>

                    <div class="control-section">
                        <h3>Residue Tracker</h3>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="enableTracker">
                                Enable Tracker
                            </label>
                        </div>
                        
                        <div class="control-group">
                            <label>Track Mode</label>
                            <select id="trackerMode">
                                <option value="manual">Manual Input</option>
                                <option value="slider">Slider (Single r)</option>
                            </select>
                        </div>
                        
                        <div class="control-group" id="manualTrackerGroup">
                            <label>Track Residues (comma-separated)</label>
                            <input type="text" id="trackedResidues" value="1" placeholder="e.g., 1,7,13,19">
                        </div>
                        
                        <div class="control-group" id="sliderTrackerGroup" style="display: none;">
                            <label>Track Residue r = <span class="range-display" id="trackedRSliderDisplay">1</span></label>
                            <div class="dual-input">
                                <input type="range" id="trackedRSlider" min="0" max="100" step="1" value="1">
                                <input type="number" id="trackedRSliderNum" min="0" max="10000" step="1" value="1">
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

                    <div class="control-section">
                        <h3>Coloring Schemes</h3>
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

                    <div class="control-section">
                        <h3>Display Settings</h3>
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
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="performanceMode" checked>
                                Performance Mode (Faster Rendering)
                            </label>
                        </div>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="enablePointClick">
                                Enable Point Click Info
                            </label>
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

                    <div class="control-section">
                        <h3>Label Display</h3>
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

                    <div class="control-section">
                        <h3>Gap Analysis</h3>
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

                    <div class="control-section">
                        <h3>Export Settings</h3>
                        
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
                                <option value="1">Current (1000×800)</option>
                                <option value="2">2× (2000×1600)</option>
                                <option value="3">3× (3000×2400)</option>
                                <option value="4">4× (4000×3200)</option>
                            </select>
                        </div>
                        
                        <div class="button-group">
                            <button onclick="exportImage()">Export PNG</button>
                            <button onclick="exportCSV()">Export CSV</button>
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

                <div class="canvas-container">
                    <canvas id="mainCanvas" width="1000" height="800"></canvas>
                    <div class="tooltip" id="tooltip"></div>
                    
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
                        </div>
                    </div>
                </div>
            </div>
        </div>

    <script>
        const canvas = document.getElementById('mainCanvas');
        const ctx = canvas.getContext('2d');
        const tooltip = document.getElementById('tooltip');
        
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
        
        // Advanced performance optimizations
        let pointsByModulus = {}; // O(1) lookup by modulus
        let ringMetadata = []; // Pre-computed ring properties

        // Progressive computation without Web Worker
        async function computePointsProgressive(modMin, modMax, modStep, gaps, angularMapping) {
            pointsData = [];
            pointsByModulus = {}; // Reset lookup table
            ringMetadata = [];
            
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;
            let processedCount = 0;

            // Build moduli list
            const moduli = [];
            for (let m = modMin; m <= modMax; m += modStep) {
                moduli.push(m);
            }

            // Pre-compute ring metadata
            moduli.forEach((m, idx) => {
                ringMetadata.push({
                    modulus: m,
                    index: idx,
                    phiM: phi(m),
                    totalPoints: m
                });
            });

            for (let m = modMin; m <= modMax; m += modStep) {
                if (!modRotations[m]) modRotations[m] = 0;
                
                // Initialize modulus bucket for O(1) lookup
                pointsByModulus[m] = {};
                
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

                    const point = {
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        phiM: phiM,
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps
                    };

                    pointsData.push(point);
                    pointsByModulus[m][r] = point;

                    processedCount++;

                    // Yield to UI periodically
                    if (processedCount % 1000 === 0) {
                        updateProgressDisplay(processedCount, m, modMax);
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
        syncInputs('perRingRot', 'perRingRotNum');
        syncInputs('trackedRSlider', 'trackedRSliderNum');

        syncInputs('labelSize', 'labelSizeNum');
        syncInputs('labelSpacing', 'labelSpacingNum');
        syncInputs('gapOpacity', 'gapOpacityNum');
        syncInputs('gapLineWidth', 'gapLineWidthNum');
        syncInputs('connLineWidth', 'connLineWidthNum');

        // Show/hide tracker mode inputs
        document.getElementById('trackerMode').addEventListener('change', function() {
            const mode = this.value;
            const manualGroup = document.getElementById('manualTrackerGroup');
            const sliderGroup = document.getElementById('sliderTrackerGroup');
            
            if (mode === 'manual') {
                manualGroup.style.display = 'block';
                sliderGroup.style.display = 'none';
            } else {
                manualGroup.style.display = 'none';
                sliderGroup.style.display = 'block';
                updateSliderTrackerRange();
            }
        });

        // Update slider range when moduli change
        function updateSliderTrackerRange() {
            const moduli = getSelectedModuli();
            if (moduli.length === 0) return;
            
            const maxR = Math.max(...moduli) - 1;
            const slider = document.getElementById('trackedRSlider');
            const numberInput = document.getElementById('trackedRSliderNum');
            
            slider.max = maxR;
            numberInput.max = maxR;
            
            // Clamp current value
            if (parseInt(slider.value) > maxR) {
                slider.value = maxR;
                numberInput.value = maxR;
            }
        }

        // Real-time slider update
        document.getElementById('trackedRSlider').addEventListener('input', () => {
            updateRangeDisplays();
            if (document.getElementById('enableTracker').checked) {
                drawVisualization();
                updateTrackerInfo();
            }
        });
        
        document.getElementById('trackedRSliderNum').addEventListener('input', () => {
            updateRangeDisplays();
            if (document.getElementById('enableTracker').checked) {
                drawVisualization();
                updateTrackerInfo();
            }
        });

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

        // Spiral presets
        function setSpiralPreset(preset) {
            switch(preset) {
                case 'gentle':
                    document.getElementById('perRingRot').value = 5;
                    document.getElementById('perRingRotNum').value = 5;
                    document.getElementById('spiralMode').value = 'linear';
                    break;
                case 'moderate':
                    document.getElementById('perRingRot').value = 15;
                    document.getElementById('perRingRotNum').value = 15;
                    document.getElementById('spiralMode').value = 'linear';
                    break;
                case 'strong':
                    document.getElementById('perRingRot').value = 30;
                    document.getElementById('perRingRotNum').value = 30;
                    document.getElementById('spiralMode').value = 'linear';
                    break;
                case 'golden':
                    document.getElementById('perRingRot').value = 20;
                    document.getElementById('perRingRotNum').value = 20;
                    document.getElementById('spiralMode').value = 'fibonacci';
                    break;
                case 'galaxy':
                    document.getElementById('perRingRot').value = 45;
                    document.getElementById('perRingRotNum').value = 45;
                    document.getElementById('spiralMode').value = 'logarithmic';
                    break;
                case 'helix':
                    document.getElementById('perRingRot').value = 25;
                    document.getElementById('perRingRotNum').value = 25;
                    document.getElementById('spiralMode').value = 'sine-wave';
                    break;
            }
            updateRangeDisplays();
            needsFullRedraw = true;
            drawVisualization();
        }

        // Auto-start animation when rotation values change (if auto-rotate enabled)
        function autoStartAnimation() {
            const autoRotate = document.getElementById('autoRotate').checked;
            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            
            if (autoRotate && (globalSpeed > 0 || modRotSpeed > 0)) {
                if (!animationId) {
                    startAnimation();
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
        document.getElementById('perRingRot').addEventListener('input', () => {
            needsFullRedraw = true;
            drawVisualization();
        });
        document.getElementById('perRingRotNum').addEventListener('input', () => {
            needsFullRedraw = true;
            drawVisualization();
        });
        document.getElementById('spiralMode').addEventListener('change', () => {
            needsFullRedraw = true;
            drawVisualization();
        });

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
            document.getElementById('perRingRotDisplay').textContent = document.getElementById('perRingRot').value;
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
            if (totalExpectedPoints > 10000) {
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

            document.getElementById('statTotal').textContent = pointsData.length.toLocaleString();
            document.getElementById('statOpen').textContent = totalOpen.toLocaleString();
            document.getElementById('statClosed').textContent = totalClosed.toLocaleString();
            document.getElementById('statRatio').textContent = openRatio.toFixed(4);
            document.getElementById('statAvgPhi').textContent = avgPhiOverM.toFixed(4);

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
            pointsByModulus = {}; // Reset lookup table
            ringMetadata = [];
            
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;
            let processedCount = 0;

            // Pre-compute ring metadata for O(1) access
            moduli.forEach((m, idx) => {
                ringMetadata.push({
                    modulus: m,
                    index: idx,
                    phiM: phi(m),
                    totalPoints: m
                });
            });

            for (let m of moduli) {
                if (!modRotations[m]) modRotations[m] = 0;
                
                // Initialize modulus bucket for O(1) lookup
                pointsByModulus[m] = {};
                
                const phiM = phi(m);
                sumPhiOverM += phiM / m;
                countModuli++;

                // Single-pass computation with all properties
                for (let r = 0; r < m; r++) {
                    const g = gcd(r, m);
                    const isOpen = g === 1;
                    
                    if (isOpen) totalOpen++;
                    else totalClosed++;

                    // Pre-compute angle once
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

                    // Pre-compute admissible gaps (only if needed)
                    let admissibleGaps = [];
                    if (isOpen && gaps.length > 0) {
                        gaps.forEach(gap => {
                            const rPlusG = (r + gap) % m;
                            if (gcd(rPlusG, m) === 1) {
                                admissibleGaps.push(gap);
                            }
                        });
                    }

                    const point = {
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        phiM: phiM,
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps
                    };

                    pointsData.push(point);
                    pointsByModulus[m][r] = point; // Store for O(1) lookup

                    processedCount++;

                    // Reduced yield frequency for better performance
                    if (processedCount % (COMPUTE_CHUNK_SIZE * 2) === 0) {
                        updateProgressDisplay(processedCount, m, moduli[moduli.length - 1]);
                        // Only yield for very large datasets
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

        function drawVisualization() {
            const performanceMode = document.getElementById('performanceMode').checked;
            
            if (performanceMode) {
                drawVisualizationOptimized();
            } else {
                drawVisualizationStandard();
            }
        }

        // Helper function to get radius for a modulus
        function getRadius(m) {
            const width = canvas.width;
            const height = canvas.height;
            const maxRadius = Math.min(width, height) * 0.4;
            const displayMode = document.getElementById('displayMode').value;
            const invertOrder = document.getElementById('invertModOrder').checked;
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            
            if (displayMode === 'unit') {
                return maxRadius;
            }
            
            const radiusScale = maxRadius / Math.max(...moduli);
            
            if (invertOrder) {
                const maxMod = Math.max(...moduli);
                const minMod = Math.min(...moduli);
                const inverted = maxMod - (m - minMod);
                return inverted * radiusScale;
            }
            
            return m * radiusScale;
        }

        // Helper function to get ring index for a modulus
        function getRingIndex(m) {
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const invertOrder = document.getElementById('invertModOrder').checked;
            
            if (invertOrder) {
                return moduli.length - 1 - moduli.indexOf(m);
            }
            
            return moduli.indexOf(m);
        }

        // Calculate per-ring rotation based on spiral mode
        function getPerRingRotation(ringIndex, totalRings) {
            const perRingRot = parseFloat(document.getElementById('perRingRot').value);
            const spiralMode = document.getElementById('spiralMode').value;
            
            if (perRingRot === 0) return 0;
            
            switch(spiralMode) {
                case 'linear':
                    return perRingRot * ringIndex;
                    
                case 'fibonacci':
                    // Golden ratio spiral: φ ≈ 1.618
                    const phi = (1 + Math.sqrt(5)) / 2;
                    return perRingRot * Math.log(ringIndex + 1) * phi;
                    
                case 'logarithmic':
                    // Natural logarithmic spiral
                    return perRingRot * Math.log(ringIndex + 1) * 2;
                    
                case 'sine-wave':
                    // Sinusoidal modulation
                    return perRingRot * ringIndex * (1 + 0.5 * Math.sin(ringIndex * Math.PI / 4));
                    
                default:
                    return perRingRot * ringIndex;
            }
        }

        function drawVisualizationOptimized() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;

            // Check if we need full redraw
            const currentSettings = JSON.stringify({
                displayMode: document.getElementById('displayMode').value,
                showOpen: document.getElementById('showOpen').checked,
                showClosed: document.getElementById('showClosed').checked,
                showRingLines: document.getElementById('showRingLines').checked,
                pointSize: document.getElementById('pointSize').value,
                baseOpenColor: document.getElementById('baseOpenColor').value,
                baseClosedColor: document.getElementById('baseClosedColor').value,
                openColorMode: document.getElementById('openColorMode').value,
                invertOrder: document.getElementById('invertModOrder').checked,
                pointsLength: pointsData.length
            });

            if (currentSettings !== lastDrawSettings || needsFullRedraw) {
                // Pre-batch points by color for faster rendering
                cachedPointBatches = batchPointsByColor();
                
                // Create static background layer (ring lines)
                if (!cachedStaticCanvas) {
                    cachedStaticCanvas = document.createElement('canvas');
                    cachedStaticCanvas.width = width;
                    cachedStaticCanvas.height = height;
                }
                
                drawStaticElements(cachedStaticCanvas);
                lastDrawSettings = currentSettings;
                needsFullRedraw = false;
            }

            // Always use black background
            ctx.clearRect(0, 0, width, height);
            ctx.fillStyle = '#000000';
            ctx.fillRect(0, 0, width, height);

            // Draw cached static background
            if (cachedStaticCanvas) {
                ctx.drawImage(cachedStaticCanvas, 0, 0);
            }

            ctx.save();
            ctx.translate(centerX + transform.x, centerY + transform.y);
            ctx.scale(transform.scale, transform.scale);
            ctx.rotate(globalRotation * Math.PI / 180);

            const displayMode = document.getElementById('displayMode').value;
            const showOpen = document.getElementById('showOpen').checked;
            const showClosed = document.getElementById('showClosed').checked;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const enableTracker = document.getElementById('enableTracker').checked;
            const enableConnections = document.getElementById('enableConnections').checked;
            const showGapLines = document.getElementById('showGapLines').checked;
            const enableGap = document.getElementById('enableGapAnalysis').checked;

            const radiusScale = displayMode === 'unit' ? maxRadius : maxRadius / Math.max(...pointsData.map(p => p.m));

            // Draw connection lines (if enabled and not too many)
            if (enableConnections && pointsData.length < 5000) {
                drawConnectionLines(radiusScale, displayMode);
            }

            // Draw gap lines (if enabled and not too many)
            if (showGapLines && enableGap && pointsData.length < 5000) {
                drawGapLines(radiusScale, displayMode);
            }

            // Draw points using batched rendering
            if (cachedPointBatches) {
                drawBatchedPoints(cachedPointBatches, pointSize, displayMode, radiusScale, showOpen, showClosed);
            }

            // Draw tracker
            if (enableTracker) {
                drawTrackerPoints(radiusScale, displayMode);
            }

            // Draw labels (skip in performance mode if too many points)
            const showLabels = document.getElementById('showLabels').checked;
            if (showLabels && pointsData.length < 2000) {
                drawLabels(radiusScale, displayMode, showOpen, showClosed, pointSize);
            }

            ctx.restore();
        }

        function drawStaticElements(staticCanvas) {
            const staticCtx = staticCanvas.getContext('2d');
            const width = staticCanvas.width;
            const height = staticCanvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;

            staticCtx.clearRect(0, 0, width, height);
            
            const showRingLines = document.getElementById('showRingLines').checked;
            const displayMode = document.getElementById('displayMode').value;
            
            if (showRingLines && displayMode === 'rings') {
                staticCtx.save();
                staticCtx.translate(centerX + transform.x, centerY + transform.y);
                staticCtx.scale(transform.scale, transform.scale);
                staticCtx.rotate(globalRotation * Math.PI / 180);
                
                staticCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                staticCtx.lineWidth = 1 / transform.scale;
                
                const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
                moduli.forEach(m => {
                    staticCtx.beginPath();
                    staticCtx.arc(0, 0, getRadius(m), 0, 2 * Math.PI);
                    staticCtx.stroke();
                });
                
                staticCtx.restore();
            }
        }

        function batchPointsByColor() {
            const batches = new Map();
            const openColorMode = document.getElementById('openColorMode').value;
            
            // Fast path for solid colors
            if (openColorMode === 'solid') {
                const openColor = document.getElementById('baseOpenColor').value;
                const closedColor = document.getElementById('baseClosedColor').value;
                
                batches.set(openColor, { open: [], closed: [], admissible: [] });
                batches.set(closedColor, { open: [], closed: [], admissible: [] });
                batches.set('#aa00ff', { open: [], closed: [], admissible: [] });
                
                pointsData.forEach(point => {
                    if (point.isAdmissible) {
                        batches.get('#aa00ff').admissible.push(point);
                    } else if (point.isOpen) {
                        batches.get(openColor).open.push(point);
                    } else {
                        batches.get(closedColor).closed.push(point);
                    }
                });
                
                return batches;
            }
            
            // Standard batching for other color modes
            pointsData.forEach(point => {
                const color = getColorForPoint(point, point.isOpen);
                
                if (!batches.has(color)) {
                    batches.set(color, {
                        open: [],
                        closed: [],
                        admissible: []
                    });
                }
                
                if (point.isAdmissible) {
                    batches.get(color).admissible.push(point);
                } else if (point.isOpen) {
                    batches.get(color).open.push(point);
                } else {
                    batches.get(color).closed.push(point);
                }
            });
            
            return batches;
        }

        function drawBatchedPoints(batches, pointSize, displayMode, radiusScale, showOpen, showClosed) {
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const totalRings = moduli.length;
            
            // Pre-compute scale factor once
            const pointScale = 1 / transform.scale;
            const scaledPointSize = pointSize * pointScale;
            const scaledAdmissibleSize = pointSize * 1.2 * pointScale;
            
            batches.forEach((pointTypes, color) => {
                // Draw closed points in single batch
                if (showClosed && pointTypes.closed.length > 0) {
                    ctx.globalAlpha = 0.3;
                    ctx.fillStyle = color;
                    
                    // Begin path once for entire batch
                    ctx.beginPath();
                    pointTypes.closed.forEach(point => {
                        const ringIndex = getRingIndex(point.m);
                        const perRingRotation = getPerRingRotation(ringIndex, totalRings);
                        const modRot = modRotations[point.m] || 0;
                        const totalAngle = point.angle + (modRot * Math.PI / 180) + (perRingRotation * Math.PI / 180);
                        const r = displayMode === 'unit' ? radiusScale : getRadius(point.m);
                        const x = r * Math.cos(totalAngle);
                        const y = r * Math.sin(totalAngle);

                        // Add to single path
                        ctx.moveTo(x + scaledPointSize, y);
                        ctx.arc(x, y, scaledPointSize, 0, 2 * Math.PI);

                        // Cache screen position
                        point.screenX = x;
                        point.screenY = y;
                        point.screenRadius = scaledPointSize;
                    });
                    // Fill entire batch at once
                    ctx.fill();
                }
                
                // Draw open points in single batch
                if (showOpen && pointTypes.open.length > 0) {
                    ctx.globalAlpha = 0.8;
                    ctx.fillStyle = color;
                    
                    ctx.beginPath();
                    pointTypes.open.forEach(point => {
                        const ringIndex = getRingIndex(point.m);
                        const perRingRotation = getPerRingRotation(ringIndex, totalRings);
                        const modRot = modRotations[point.m] || 0;
                        const totalAngle = point.angle + (modRot * Math.PI / 180) + (perRingRotation * Math.PI / 180);
                        const r = displayMode === 'unit' ? radiusScale : getRadius(point.m);
                        const x = r * Math.cos(totalAngle);
                        const y = r * Math.sin(totalAngle);

                        ctx.moveTo(x + scaledPointSize, y);
                        ctx.arc(x, y, scaledPointSize, 0, 2 * Math.PI);

                        point.screenX = x;
                        point.screenY = y;
                        point.screenRadius = scaledPointSize;
                    });
                    ctx.fill();
                }
                
                // Draw admissible points in single batch
                if (pointTypes.admissible.length > 0) {
                    ctx.globalAlpha = 0.9;
                    ctx.fillStyle = '#aa00ff';
                    
                    ctx.beginPath();
                    pointTypes.admissible.forEach(point => {
                        const ringIndex = getRingIndex(point.m);
                        const perRingRotation = getPerRingRotation(ringIndex, totalRings);
                        const modRot = modRotations[point.m] || 0;
                        const totalAngle = point.angle + (modRot * Math.PI / 180) + (perRingRotation * Math.PI / 180);
                        const r = displayMode === 'unit' ? radiusScale : getRadius(point.m);
                        const x = r * Math.cos(totalAngle);
                        const y = r * Math.sin(totalAngle);

                        ctx.moveTo(x + scaledAdmissibleSize, y);
                        ctx.arc(x, y, scaledAdmissibleSize, 0, 2 * Math.PI);

                        point.screenX = x;
                        point.screenY = y;
                        point.screenRadius = scaledAdmissibleSize;
                    });
                    ctx.fill();
                }
            });
            
            ctx.globalAlpha = 1.0;
        }

        function drawConnectionLines(radiusScale, displayMode) {
            const connectionMode = document.getElementById('connectionMode').value;
            if (connectionMode === 'none') return;
            
            const connOpacity = parseFloat(document.getElementById('connOpacity').value);
            const connLineWidth = parseFloat(document.getElementById('connLineWidth').value);
            const onlyOpenConn = document.getElementById('onlyOpenConn').checked;
            
            ctx.strokeStyle = `rgba(255, 255, 255, ${connOpacity})`;
            ctx.lineWidth = connLineWidth / transform.scale;
            
            // Only draw connection lines for reasonable dataset sizes
            if (connectionMode === 'same-mod') {
                drawSameModConnections(radiusScale, displayMode, onlyOpenConn);
            } else if (connectionMode === 'specific-mod') {
                drawSpecificModConnections(radiusScale, displayMode, onlyOpenConn);
            } else {
                drawCrossModulusConnections(radiusScale, displayMode, connectionMode, onlyOpenConn);
            }
        }

        function drawSameModConnections(radiusScale, displayMode, onlyOpenConn) {
            const sameModPattern = document.getElementById('sameModPattern').value;
            const sameModGap = parseInt(document.getElementById('sameModGap').value);
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
            
            moduli.forEach(m => {
                const pointsInMod = pointsData.filter(p => p.m === m);
                
                pointsInMod.forEach((p1, idx) => {
                    if (onlyOpenConn && !p1.isOpen) return;
                    
                    let targetPoints = [];
                    
                    if (sameModPattern === 'sequential') {
                        const nextR = (p1.r + 1) % m;
                        targetPoints = pointsInMod.filter(p2 => p2.r === nextR);
                    } else if (sameModPattern === 'open-only') {
                        if (p1.isOpen) {
                            targetPoints = pointsInMod.filter(p2 => p2.isOpen && p2.r !== p1.r);
                        }
                    } else if (sameModPattern === 'by-gap') {
                        const targetR = (p1.r + sameModGap) % m;
                        targetPoints = pointsInMod.filter(p2 => p2.r === targetR);
                    }
                    
                    targetPoints.forEach(p2 => {
                        if (onlyOpenConn && !p2.isOpen) return;
                        drawLineBetweenPoints(p1, p2, m, m, radiusScale, displayMode);
                    });
                });
            });
        }

        function drawSpecificModConnections(radiusScale, displayMode, onlyOpenConn) {
            const specificMod = parseInt(document.getElementById('specificModValue').value);
            const pointsInMod = pointsData.filter(p => p.m === specificMod);
            
            pointsInMod.forEach((p1, idx) => {
                if (onlyOpenConn && !p1.isOpen) return;
                if (idx < pointsInMod.length - 1) {
                    const p2 = pointsInMod[idx + 1];
                    if (onlyOpenConn && !p2.isOpen) return;
                    drawLineBetweenPoints(p1, p2, specificMod, specificMod, radiusScale, displayMode);
                }
            });
        }

        function drawCrossModulusConnections(radiusScale, displayMode, connectionMode, onlyOpenConn) {
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
            
            for (let i = 0; i < moduli.length - 1; i++) {
                const m1 = moduli[i];
                const m2 = moduli[i + 1];
                
                const points1 = pointsData.filter(p => p.m === m1);
                const points2 = pointsData.filter(p => p.m === m2);

                points1.forEach(p1 => {
                    if (onlyOpenConn && !p1.isOpen) return;

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
                        drawLineBetweenPoints(p1, p2, m1, m2, radiusScale, displayMode);
                    });
                });
            }
        }

        function drawLineBetweenPoints(p1, p2, m1, m2, radiusScale, displayMode) {
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const totalRings = moduli.length;
            
            const ringIndex1 = getRingIndex(m1);
            const perRingRot1 = getPerRingRotation(ringIndex1, totalRings);
            const modRot1 = modRotations[m1] || 0;
            const angle1 = p1.angle + (modRot1 * Math.PI / 180) + (perRingRot1 * Math.PI / 180);
            const r1 = displayMode === 'unit' ? radiusScale : getRadius(m1);
            const x1 = r1 * Math.cos(angle1);
            const y1 = r1 * Math.sin(angle1);

            const ringIndex2 = getRingIndex(m2);
            const perRingRot2 = getPerRingRotation(ringIndex2, totalRings);
            const modRot2 = modRotations[m2] || 0;
            const angle2 = p2.angle + (modRot2 * Math.PI / 180) + (perRingRot2 * Math.PI / 180);
            const r2 = displayMode === 'unit' ? radiusScale : getRadius(m2);
            const x2 = r2 * Math.cos(angle2);
            const y2 = r2 * Math.sin(angle2);

            ctx.beginPath();
            ctx.moveTo(x1, y1);
            ctx.lineTo(x2, y2);
            ctx.stroke();
        }

        function drawGapLines(radiusScale, displayMode) {
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

                // Use pre-computed lookup table for O(1) access
                ctx.beginPath();
                
                pointsData.forEach(point => {
                    if (!point.isOpen) return;
                    if (!point.admissibleGaps.includes(gap)) return;

                    const rPlusG = (point.r + gap) % point.m;
                    const targetPoint = pointsByModulus[point.m] && pointsByModulus[point.m][rPlusG];
                    
                    if (targetPoint && targetPoint.isOpen) {
                        drawLineBetweenPoints(point, targetPoint, point.m, point.m, radiusScale, displayMode);
                    }
                });
                
                ctx.stroke();
                ctx.globalAlpha = 1.0;
            });
        }

        function drawTrackerPoints(radiusScale, displayMode) {
            const trackedInput = document.getElementById('trackedResidues').value;
            const trackedRs = trackedInput.split(',').map(r => parseInt(r.trim())).filter(r => !isNaN(r));
            const modFilter = document.getElementById('trackerModFilter').value;
            const filterMod = modFilter ? parseInt(modFilter) : null;
            const trackerColor = document.getElementById('trackerColor').value;
            const trackerSize = parseFloat(document.getElementById('trackerSize').value);
            
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const totalRings = moduli.length;
            
            trackedRs.forEach(trackedResidue => {
                let filteredPoints = pointsData.filter(p => p.r === trackedResidue);
                if (filterMod !== null) {
                    filteredPoints = filteredPoints.filter(p => p.m === filterMod);
                }
                
                filteredPoints.forEach(point => {
                    const ringIndex = getRingIndex(point.m);
                    const perRingRotation = getPerRingRotation(ringIndex, totalRings);
                    const modRot = modRotations[point.m] || 0;
                    const totalAngle = point.angle + (modRot * Math.PI / 180) + (perRingRotation * Math.PI / 180);
                    const r = displayMode === 'unit' ? radiusScale : getRadius(point.m);
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

        function drawLabels(radiusScale, displayMode, showOpen, showClosed, pointSize) {
            const labelType = document.getElementById('labelType').value;
            const labelFilter = document.getElementById('labelFilter').value;
            const labelFilterValue = parseInt(document.getElementById('labelFilterValue').value);
            const labelSize = parseFloat(document.getElementById('labelSize').value);
            const labelColor = document.getElementById('labelColor').value;
            const labelBg = document.getElementById('labelBackground').checked;
            const labelSpacing = parseFloat(document.getElementById('labelSpacing').value);

            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a, b) => a - b);
            const totalRings = moduli.length;

            ctx.font = `${labelSize / transform.scale}px Arial`;
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';

            pointsData.forEach(point => {
                if (!shouldShowLabel(point, labelFilter, labelFilterValue)) return;
                if (!showOpen && point.isOpen) return;
                if (!showClosed && !point.isOpen) return;

                const ringIndex = getRingIndex(point.m);
                const perRingRotation = getPerRingRotation(ringIndex, totalRings);
                const modRot = modRotations[point.m] || 0;
                const totalAngle = point.angle + (modRot * Math.PI / 180) + (perRingRotation * Math.PI / 180);
                const r = displayMode === 'unit' ? radiusScale : getRadius(point.m);
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

        function drawVisualizationStandard() {
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

            // Draw points
            pointsData.forEach(point => {
                if (!showOpen && point.isOpen) return;
                if (!showClosed && !point.isOpen) return;

                const modRot = modRotations[point.m] || 0;
                const totalAngle = point.angle + (modRot * Math.PI / 180);
                const r = displayMode === 'unit' ? maxRadius : getRadius(point.m);
                const x = r * Math.cos(totalAngle);
                const y = r * Math.sin(totalAngle);

                let radius = pointSize;
                let color = getColorForPoint(point, point.isOpen);
                let opacity = point.isOpen ? 0.8 : 0.3;

                if (point.isAdmissible) {
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
            });

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
                        if (!point.admissibleGaps.includes(gap)) return;

                        const rPlusG = (point.r + gap) % point.m;
                        const targetPoint = pointsByMod[point.m] && pointsByMod[point.m][rPlusG];
                        
                        if (targetPoint && targetPoint.isOpen) {
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

            drawVisualization();
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

        // Mouse and touch events
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
                // Pan start or click
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
                
                const rect = canvas.getBoundingClientRect();
                const centerX = (e.touches[0].clientX + e.touches[1].clientX) / 2 - rect.left - canvas.width / 2;
                const centerY = (e.touches[0].clientY + e.touches[1].clientY) / 2 - rect.top - canvas.height / 2;
                
                transform.x = centerX - (centerX - transform.x) * delta;
                transform.y = centerY - (centerY - transform.y) * delta;
                transform.scale *= delta;
                transform.scale = Math.max(0.1, Math.min(20, transform.scale));
                
                drawVisualization();
            } else if (isDragging) {
                // Pan
                const coords = getEventCoords(e);
                transform.x += coords.x - lastMouseX;
                transform.y += coords.y - lastMouseY;
                lastMouseX = coords.x;
                lastMouseY = coords.y;
                drawVisualization();
            } else {
                // Hover for tooltip
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
            const enablePointClick = document.getElementById('enablePointClick').checked;
            
            if (!isDragging && enablePointClick) {
                // Click detected and point clicking is enabled
                const coords = e.changedTouches ? 
                    { x: e.changedTouches[0].clientX, y: e.changedTouches[0].clientY } :
                    { x: e.clientX, y: e.clientY };
                    
                const rect = canvas.getBoundingClientRect();
                const x = (coords.x - rect.left - canvas.width / 2 - transform.x) / transform.scale;
                const y = (coords.y - rect.top - canvas.height / 2 - transform.y) / transform.scale;
                
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
                        if (dist < point.screenRadius * 3 && dist < minDist) {
                            minDist = dist;
                            foundPoint = point;
                        }
                    }
                });
                
                if (foundPoint) {
                    const [reducedNum, reducedDen] = reduceFraction(foundPoint.r, foundPoint.m);
                    const fareyFraction = `${foundPoint.r}/${foundPoint.m}` + (reducedNum !== foundPoint.r ? ` = ${reducedNum}/${reducedDen}` : '');
                    
                    alert(`Point Details:\n\nModulus m = ${foundPoint.m}\nResidue r = ${foundPoint.r}\nFarey Fraction: ${fareyFraction}\n\ngcd(${foundPoint.r}, ${foundPoint.m}) = ${foundPoint.gcd}\nChannel: ${foundPoint.isOpen ? 'OPEN' : 'CLOSED'}\nφ(${foundPoint.m}) = ${foundPoint.phiM}\nAngle: ${(foundPoint.angle * 180 / Math.PI).toFixed(2)}°${foundPoint.isAdmissible ? '\n\nGAP ADMISSIBLE ✓' : ''}`);
                }
            }
            isDragging = false;
            touchStartDist = 0;
        }

        canvas.addEventListener('mousedown', handleStart);
        canvas.addEventListener('mousemove', handleMove);
        canvas.addEventListener('mouseup', handleEnd);
        canvas.addEventListener('mouseleave', () => { 
            isDragging = false; 
            tooltip.style.opacity = '0';
        });
        
        canvas.addEventListener('touchstart', handleStart, { passive: true });
        canvas.addEventListener('touchmove', handleMove, { passive: false });
        canvas.addEventListener('touchend', handleEnd);
        canvas.addEventListener('touchcancel', () => { isDragging = false; touchStartDist = 0; });

        canvas.addEventListener('wheel', (e) => {
            e.preventDefault();
            const delta = e.deltaY > 0 ? 0.9 : 1.1;
            const rect = canvas.getBoundingClientRect();
            const mouseX = e.clientX - rect.left - canvas.width / 2;
            const mouseY = e.clientY - rect.top - canvas.height / 2;
            
            transform.x = mouseX - (mouseX - transform.x) * delta;
            transform.y = mouseY - (mouseY - transform.y) * delta;
            transform.scale *= delta;
            transform.scale = Math.max(0.1, Math.min(20, transform.scale));
            
            drawVisualization();
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
            needsFullRedraw = true;
            cachedPointBatches = null;
            cachedStaticCanvas = null;
            lastDrawSettings = null;
            generatePointsData();
            if (!isComputing) {
                drawVisualization();
            }
        }
        
        // Performance mode change handler
        document.getElementById('performanceMode').addEventListener('change', () => {
            needsFullRedraw = true;
            drawVisualization();
        });

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
            const exportTitle = document.getElementById('exportTitle').value;
            const resolution = parseFloat(document.getElementById('exportResolution').value);
            
            // Create temporary canvas at higher resolution
            const tempCanvas = document.createElement('canvas');
            const baseWidth = canvas.width;
            const baseHeight = canvas.height;
            
            let exportWidth = baseWidth * resolution;
            let exportHeight = baseHeight * resolution;
            
            // Calculate legend dimensions - always on right
            let legendWidth = 0;
            
            if (includeLegend) {
                legendWidth = 400 * resolution;
                exportWidth += legendWidth;
            }
            
            tempCanvas.width = exportWidth;
            tempCanvas.height = exportHeight;
            const tempCtx = tempCanvas.getContext('2d');
            
            // Fill background
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
            const textColor = currentTheme === 'dark' ? '#ffffff' : '#000000';
            tempCtx.fillStyle = bgColor;
            tempCtx.fillRect(0, 0, exportWidth, exportHeight);
            
            // Draw main visualization scaled up on the left
            tempCtx.save();
            tempCtx.scale(resolution, resolution);
            tempCtx.drawImage(canvas, 0, 0);
            tempCtx.restore();
            
            // Draw legend if enabled - always on right, title always top center
            if (includeLegend) {
                drawLegend(tempCtx, exportTitle, legendWidth, exportWidth, exportHeight, resolution, textColor, bgColor);
            }
            
            // Export
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().slice(0, 19).replace(/:/g, '-');
            link.download = `modular_rings_${timestamp}.png`;
            link.href = tempCanvas.toDataURL('image/png');
            link.click();
        }

        function drawLegend(ctx, title, legendWidth, totalWidth, totalHeight, resolution, textColor, bgColor) {
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
            
            const fontSize = 14 * resolution;
            const lineHeight = 20 * resolution;
            const padding = 20 * resolution;
            
            // Legend is always on the right
            const startX = totalWidth - legendWidth + padding;
            const maxWidth = legendWidth - 2 * padding;
            
            // Title at top center of entire image
            ctx.fillStyle = textColor;
            ctx.font = `bold ${fontSize * 1.8}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(title, totalWidth / 2, padding + fontSize * 1.5);
            
            // Start legend content
            let y = padding * 3;
            ctx.textAlign = 'left';
            
            // Draw separator
            ctx.strokeStyle = textColor;
            ctx.lineWidth = 1 * resolution;
            ctx.beginPath();
            ctx.moveTo(startX, y);
            ctx.lineTo(startX + maxWidth * 0.8, y);
            ctx.stroke();
            y += lineHeight;
            // Parameters
            ctx.font = `${fontSize}px Arial`;
            ctx.fillStyle = textColor;
            
            // Modulus configuration
            let moduliText = '';
            if (mode === 'range') {
                const modMin = document.getElementById('modMin').value;
                const modMax = document.getElementById('modMax').value;
                const modStep = document.getElementById('modStep').value;
                moduliText = `Range: ${modMin} to ${modMax} (step ${modStep})`;
            } else if (mode === 'fibonacci') {
                moduliText = `Fibonacci sequence (max ${document.getElementById('sequenceMax').value})`;
            } else if (mode === 'primes') {
                moduliText = `Prime moduli (max ${document.getElementById('sequenceMax').value})`;
            } else if (mode === 'powers-of-2') {
                moduliText = `Powers of 2 (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'powers-of-3') {
                moduliText = `Powers of 3 (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'M30-sequence') {
                moduliText = `M₃₀ = 30×2ⁿ (${document.getElementById('sequenceTerms').value} terms)`;
            } else if (mode === 'custom') {
                const customMods = document.getElementById('customModuli').value;
                moduliText = `Custom: ${customMods}`;
            }
            
            ctx.fillText(`Moduli: ${moduliText}`, startX, y);
            y += lineHeight;
            
            ctx.fillText(`Total Moduli: ${moduli.length}`, startX, y);
            y += lineHeight;
            
            ctx.fillText(`Display Mode: ${displayMode === 'rings' ? 'Concentric Rings' : 'Unit Circle'}`, startX, y);
            y += lineHeight;
            
            if (invertOrder) {
                ctx.fillText(`Order: Inverted (Outer↔Inner)`, startX, y);
                y += lineHeight;
            }
            
            ctx.fillText(`Angular Mapping: ${angularMapping}`, startX, y);
            y += lineHeight;
            
            const channelText = showOpen && showClosed ? 'Open & Closed' : showOpen ? 'Open Only' : 'Closed Only';
            ctx.fillText(`Channels: ${channelText}`, startX, y);
            y += lineHeight;
            
            if (enableGap) {
                ctx.fillText(`Gap Analysis: ${gapValues}`, startX, y);
                y += lineHeight;
            }
            
            if (enableTracker) {
                ctx.fillText(`Tracked Residues: ${trackedResidues}`, startX, y);
                y += lineHeight;
            }
            
            if (enableConnections) {
                const connModeText = connectionMode === 'next-mod' ? 'r to r (Next Mod)' :
                                     connectionMode === 'binary-lift' ? 'Binary Lift' :
                                     connectionMode === 'double-lift' ? 'r to r+M×2ⁿ' :
                                     connectionMode === 'same-mod' ? 'Same Modulus' :
                                     connectionMode === 'specific-mod' ? 'Specific Modulus' : 'None';
                ctx.fillText(`Connections: ${connModeText}`, startX, y);
                y += lineHeight;
            }
            
            // Statistics
            y += lineHeight * 0.5;
            ctx.font = `bold ${fontSize}px Arial`;
            ctx.fillText('Statistics:', startX, y);
            y += lineHeight;
            
            ctx.font = `${fontSize}px Arial`;
            const totalPoints = document.getElementById('statTotal').textContent;
            const openCount = document.getElementById('statOpen').textContent;
            const closedCount = document.getElementById('statClosed').textContent;
            const openRatio = document.getElementById('statRatio').textContent;
            const avgPhi = document.getElementById('statAvgPhi').textContent;
            
            ctx.fillText(`Total Points: ${totalPoints}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Open: ${openCount}, Closed: ${closedCount}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Open Ratio: ${openRatio}`, startX, y);
            y += lineHeight;
            ctx.fillText(`Avg φ(m)/m: ${avgPhi} (Limit: 0.6079)`, startX, y);
            y += lineHeight;
            
            // Author and date
            y += lineHeight * 0.5;
            ctx.font = `${fontSize * 0.9}px Arial`;
            ctx.fillStyle = textColor;
            const date = new Date().toLocaleDateString();
            ctx.fillText(`Generated: ${date}`, startX, y);
            y += lineHeight;
            ctx.fillText('By Wessen Getachew', startX, y);
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
            let csv = 'Modulus,Residue,GCD,Channel,Angle_Rad,Phi_m,Admissible\n';
            pointsData.forEach(p => {
                csv += `${p.m},${p.r},${p.gcd},${p.isOpen ? 'Open' : 'Closed'},`;
                csv += `${p.angle.toFixed(6)},${p.phiM},${p.isAdmissible ? 'Yes' : 'No'}\n`;
            });
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.download = `modular_rings_data_${new Date().toISOString().slice(0,10)}.csv`;
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
            
            const tabs = {
                'introduction': [0, 'introductionTab'],
                'visualization': [1, 'visualizationTab'],
                'bridge': [2, 'bridgeTab'],
                'theory': [3, 'theoryTab'],
                'references': [4, 'referencesTab']
            };
            
            document.querySelectorAll('.tab')[tabs[tab][0]].classList.add('active');
            document.getElementById(tabs[tab][1]).classList.add('active');
        }

        window.addEventListener('load', () => {
            initializeTheme();
            updateRangeDisplays();
            updateGapColorPickers();
            updateVisualization();
        });
    </script>
</body>
</html>
