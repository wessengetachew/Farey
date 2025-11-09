
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

        <div class="tabs">
            <button class="tab active" onclick="switchTab('introduction')">Introduction</button>
            <button class="tab" onclick="switchTab('visualization')">Visualization</button>
            <button class="tab" onclick="switchTab('theory')">Theory</button>
            <button class="tab" onclick="switchTab('references')">References</button>
        </div>

        <div id="introductionTab" class="tab-content active">
            <div class="intro-page">
                <h2>Introduction</h2>
                <p>
                    This interactive tool provides a geometric visualization of modular arithmetic, coprimality patterns, and their deep connections to prime number theory. By representing residues as points on concentric rings, we reveal the elegant structure underlying Euler's totient function, Farey sequences, and the distribution of prime numbers.
                </p>

                <div class="intro-box">
                    <h3>What You Will Explore</h3>
                    <p>
                        For each modulus m, we map every residue r (where 0 ≤ r < m) to a point at angle 2πr/m on a circle of radius m. Points are classified as <strong>open channels</strong> (where gcd(r,m) = 1, indicating coprimality) or <strong>closed channels</strong> (where gcd(r,m) > 1). This simple geometric construction reveals profound mathematical patterns.
                    </p>
                    <p>
                        The visualization demonstrates how the density of open channels converges to 6/π² ≈ 0.6079, the Euler product formula, and connections to the Riemann zeta function ζ(2) = π²/6. You can track individual residues across moduli, analyze prime gaps, and explore various coloring schemes based on prime factorization.
                    </p>
                </div>

                <h2>Getting Started: Quick Walkthrough</h2>

                <div class="starter-toolkit">
                    <div class="toolkit-card">
                        <h4>Step 1: Basic Setup</h4>
                        <ol>
                            <li>Navigate to the <strong>Visualization</strong> tab</li>
                            <li>Start with default settings (m=1 to 60)</li>
                            <li>Click <strong>Update Display</strong></li>
                            <li>Observe concentric rings with colored points</li>
                            <li>Green points = open channels (coprime)</li>
                            <li>Red points = closed channels (not coprime)</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 2: Navigation</h4>
                        <ol>
                            <li><strong>Pan:</strong> Click and drag on canvas</li>
                            <li><strong>Zoom:</strong> Scroll wheel or pinch</li>
                            <li><strong>Hover:</strong> Mouse over points for details</li>
                            <li><strong>Click:</strong> Click points for full information</li>
                            <li><strong>Reset View:</strong> Double-click canvas</li>
                            <li><strong>Export:</strong> Use PNG or CSV buttons</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 3: Preset Sequences</h4>
                        <ol>
                            <li>Try preset M_n = 30×2^n buttons</li>
                            <li>n=0: View m=30 (single ring)</li>
                            <li>n=1: View m=60</li>
                            <li>Progress through n=2,3,4,5</li>
                            <li>Click "All: 30 to 960" for full range</li>
                            <li>Observe binary lifting structure</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 4: Rotation Effects</h4>
                        <ol>
                            <li>Enable <strong>Animation</strong> checkbox</li>
                            <li>Set <strong>Global Rotation</strong> to 1-5 deg/frame</li>
                            <li>Try <strong>Individual Mod Rotation</strong></li>
                            <li>Select <strong>Speed Gradient</strong>: Inner-to-Outer</li>
                            <li>Adjust <strong>Gradient Strength</strong></li>
                            <li>Observe spiraling patterns</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 5: Coloring Schemes</h4>
                        <ol>
                            <li>Change <strong>Open Channel Color Mode</strong></li>
                            <li>Try "By Smallest Prime Factor"</li>
                            <li>Groups: 2→red, 3→orange, 5→yellow</li>
                            <li>Try "By Residue" for rainbow patterns</li>
                            <li>Adjust <strong>Saturation</strong> and <strong>Lightness</strong></li>
                            <li>Compare different prime factorizations</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 6: Residue Tracker</h4>
                        <ol>
                            <li>Enable <strong>Residue Tracker</strong></li>
                            <li>Set <strong>Track Residue</strong> to 7</li>
                            <li>Observe where r=7 appears across rings</li>
                            <li>Note coprimality patterns</li>
                            <li>Try tracking r=1, r=11, r=13</li>
                            <li>Check statistics in tracker display</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 7: Connection Lines</h4>
                        <ol>
                            <li>Enable <strong>Connect Residues</strong></li>
                            <li>Try "r to r (Next Mod)" mode</li>
                            <li>Shows how residues connect between rings</li>
                            <li>Try "r to r+M×2^n" for binary lifting</li>
                            <li>Visualizes the lifting theorem</li>
                            <li>Adjust connection opacity</li>
                        </ol>
                    </div>

                    <div class="toolkit-card">
                        <h4>Step 8: Gap Analysis</h4>
                        <ol>
                            <li>Enable <strong>Gap Analysis</strong></li>
                            <li>Set <strong>Gap Value</strong> to 2 (twin primes)</li>
                            <li>Purple points = admissible pairs</li>
                            <li>These satisfy: gcd(r,m)=1 and gcd(r+2,m)=1</li>
                            <li>Try gaps: 4, 6, 30</li>
                            <li>Compare admissibility counts</li>
                        </ol>
                    </div>
                </div>

                <div class="intro-box">
                    <h3>Key Insights to Discover</h3>
                    <ul>
                        <li><strong>Density Convergence:</strong> Watch the Open Channel Ratio approach 6/π² ≈ 0.6079 as you increase the modulus range</li>
                        <li><strong>Binary Lifting:</strong> Each open channel at M_n spawns exactly two open channels at M_{n+1}</li>
                        <li><strong>Farey Structure:</strong> Enable radial lines to see the spoke pattern of reduced fractions</li>
                        <li><strong>Prime Factorization:</strong> Color by smallest/largest prime factor to reveal divisibility patterns</li>
                        <li><strong>Gap Patterns:</strong> Admissible residues predict where prime pairs can occur</li>
                    </ul>
                </div>

                <h2>Mathematical Context</h2>
                <p>
                    This framework connects several fundamental areas of number theory: Euler's totient function φ(m) counts the open channels for each modulus. The average value of φ(m)/m equals 6/π², which appears in the Riemann zeta function as 1/ζ(2). The Farey sequence F_m consists of all reduced fractions with denominator at most m, corresponding to the angular positions of open channels on the unit circle.
                </p>
                <p>
                    The gap admissibility conditions determine which residue classes can contain prime pairs (p, p+g). The Hardy-Littlewood conjecture predicts the density of such pairs based on these modular constraints. By visualizing these patterns geometrically, we gain intuition about prime distribution and the deep structure of multiplicative number theory.
                </p>

                <div class="intro-box">
                    <h3>Recommended Exploration Paths</h3>
                    <p><strong>For Beginners:</strong> Start with Steps 1-3, explore presets, and observe the basic open/closed channel distinction.</p>
                    <p><strong>For Intermediate Users:</strong> Complete Steps 4-6, experiment with coloring schemes, and track specific residues like prime numbers.</p>
                    <p><strong>For Advanced Users:</strong> Master Steps 7-8, analyze connection patterns, study gap admissibility, and cross-reference with the Theory tab.</p>
                </div>
            </div>
        </div>

        <div id="visualizationTab" class="tab-content">
            <div class="main-content">
                <div class="control-panel">
                    <div class="control-section">
                        <h3>Modulus Configuration</h3>
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
                        
                        <div class="preset-grid">
                            <button onclick="setPreset(0)">n=0 (30)</button>
                            <button onclick="setPreset(1)">n=1 (60)</button>
                            <button onclick="setPreset(2)">n=2 (120)</button>
                            <button onclick="setPreset(3)">n=3 (240)</button>
                            <button onclick="setPreset(4)">n=4 (480)</button>
                            <button onclick="setPreset(5)">n=5 (960)</button>
                        </div>
                        <button onclick="setPresetRange()" style="width: 100%; margin-top: 8px;">All: 30 to 960</button>
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
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Connection Opacity <span class="range-display" id="connOpacityDisplay">0.3</span></label>
                            <div class="dual-input">
                                <input type="range" id="connOpacity" min="0.1" max="1" step="0.1" value="0.3">
                                <input type="number" id="connOpacityNum" min="0" max="1" step="0.1" value="0.3">
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
                            <button id="playButton" onclick="startAnimation()" style="background: #00ff00; color: #000000;">Play</button>
                            <button id="pauseButton" onclick="stopAnimation()" style="background: #ff0000; color: #ffffff;">Pause</button>
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
                            <label>Track Residue (r)</label>
                            <div class="dual-input">
                                <input type="range" id="trackedResidue" min="0" max="100" step="1" value="1">
                                <input type="number" id="trackedResidueNum" min="0" max="10000" step="1" value="1">
                            </div>
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
                            <h4>Tracked Residue Info</h4>
                            <div class="tracker-info" id="trackerInfoContent"></div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3>Coloring Schemes</h3>
                        <div class="control-group">
                            <label>Open Channel Mode</label>
                            <select id="openColorMode">
                                <option value="solid">Solid Color</option>
                                <option value="by-residue">By Residue (r)</option>
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
                                    <option value="negative">Negative: -2πr/m</option>
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
                        <h3>Gap Analysis</h3>
                        <div class="control-row">
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="enableGapAnalysis">
                                    Enable
                                </label>
                            </div>
                            <div class="control-group">
                                <label>Gap Value (g)</label>
                                <input type="number" id="gapValue" value="2" min="1" max="1000">
                            </div>
                        </div>
                    </div>

                    <div class="button-group">
                        <button onclick="updateVisualization()">Update</button>
                        <button onclick="exportImage()">PNG</button>
                        <button onclick="exportCSV()">CSV</button>
                        <button onclick="resetSettings()">Reset</button>
                    </div>

                    <div class="info-box">
                        Drag to pan • Scroll to zoom • Hover for details • Click for info
                    </div>
                </div>

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

        <div id="theoryTab" class="tab-content">
            <div class="theory-section">
                <h2>Mathematical Theory</h2>
                
                <h3>1. Modular Sequence Definition</h3>
                <p>We study the sequence of moduli M_n = 30 × 2^n where n ∈ ℤ≥0, generating: 30, 60, 120, 240, 480, 960, ...</p>

                <h3>2. Open and Closed Channels</h3>
                <div class="formula">
                    <div class="formula-title">Channel Classification</div>
                    Open Channel: gcd(r,m) = 1 (totative)<br>
                    Closed Channel: gcd(r,m) > 1 (non-totative)
                </div>

                <h3>3. Euler's Totient Function</h3>
                <div class="formula">
                    <div class="formula-title">Totient Formula</div>
                    φ(m) = m × ∏(1 - 1/p) for all primes p|m
                </div>

                <div class="formula">
                    <div class="formula-title">Density Theorem</div>
                    lim(M→∞) [1/M × Σ(m=1 to M) φ(m)/m] = 6/π² ≈ 0.6079
                </div>

                <p>This connects to the Riemann zeta function: ζ(2) = π²/6.</p>

                <h3>4. Geometric Mapping</h3>
                <div class="formula">
                    <div class="formula-title">Point Coordinates</div>
                    P(m,r) = (m·cos(2πr/m), m·sin(2πr/m))
                </div>

                <h3>5. Binary Lifting Theorem</h3>
                <div class="formula">
                    <div class="formula-title">Lifting Property</div>
                    If gcd(r, M_n) = 1, then:<br>
                    • gcd(r, M_(n+1)) = 1<br>
                    • gcd(r + M_n, M_(n+1)) = 1
                </div>

                <h3>6. Connection Lines</h3>
                <p><strong>r to r (Next Modulus):</strong> Connects residue r on ring m to residue r on ring m+step, showing how the same residue appears across scales.</p>
                <p><strong>r to r+M (Binary Lift):</strong> Visualizes the binary lifting theorem by connecting r at M_n to both r and r+M_n at M_(n+1).</p>
                <p><strong>r to r+M×2^n:</strong> Generalizes binary lifting to show the full tree structure of open channel propagation.</p>

                <h3>7. Gap Admissibility</h3>
                <div class="formula">
                    <div class="formula-title">Admissibility Condition</div>
                    r is g-admissible if:<br>
                    gcd(r, M) = 1 AND gcd(r+g, M) = 1
                </div>

                <div class="formula">
                    <div class="formula-title">Admissible Count</div>
                    N_M(g) = ∏(p|M) (p - f_p)<br>
                    where f_p = 1 if p|g, else f_p = 2
                </div>
            </div>
        </div>

        <div id="referencesTab" class="tab-content">
            <div class="theory-section">
                <h2>References</h2>

                <h3>Foundational Number Theory</h3>
                <div class="example-box">
                    <p><strong>Hardy, G. H., & Wright, E. M.</strong> (2008). <em>An Introduction to the Theory of Numbers</em> (6th ed.). Oxford University Press.</p>
                    <p><strong>Apostol, T. M.</strong> (1976). <em>Introduction to Analytic Number Theory</em>. Springer-Verlag.</p>
                </div>

                <h3>Prime Gaps and Twin Primes</h3>
                <div class="example-box">
                    <p><strong>Hardy, G. H., & Littlewood, J. E.</strong> (1923). "Some Problems of 'Partitio Numerorum' III." <em>Acta Mathematica</em>, 44(1), 1-70.</p>
                    <p><strong>Zhang, Y.</strong> (2014). "Bounded gaps between primes." <em>Annals of Mathematics</em>, 179(3), 1121-1174.</p>
                </div>

                <h3>Riemann Hypothesis</h3>
                <div class="example-box">
                    <p><strong>Riemann, B.</strong> (1859). "Über die Anzahl der Primzahlen unter einer gegebenen Größe." <em>Monatsberichte der Berliner Akademie</em>.</p>
                    <p><strong>Edwards, H. M.</strong> (1974). <em>Riemann's Zeta Function</em>. Academic Press.</p>
                </div>

                <h3>Euler Products</h3>
                <div class="example-box">
                    <p><strong>Euler, L.</strong> (1748). <em>Introductio in analysin infinitorum</em>.</p>
                    <p><strong>Iwaniec, H., & Kowalski, E.</strong> (2004). <em>Analytic Number Theory</em>. American Mathematical Society.</p>
                </div>

                <h3>Online Resources</h3>
                <div class="example-box">
                    <p>• OEIS (Online Encyclopedia of Integer Sequences): oeis.org</p>
                    <p>• Prime Pages by Chris Caldwell: primes.utm.edu</p>
                    <p>• MathWorld - Wolfram: mathworld.wolfram.com</p>
                    <p>• arXiv Number Theory: arxiv.org/list/math.NT/recent</p>
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
        let currentTheme = 'dark';

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
            document.body.className = 'dark-theme';
            document.getElementById('themeText').textContent = 'Light Mode';
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
        syncInputs('trackedResidue', 'trackedResidueNum');
        syncInputs('trackerSize', 'trackerSizeNum');
        syncInputs('pointSize', 'pointSizeNum');
        syncInputs('connOpacity', 'connOpacityNum');

        // Auto-start animation when rotation values change
        function autoStartAnimation() {
            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            
            if ((globalSpeed > 0 || modRotSpeed > 0) && !animationId) {
                startAnimation();
            }
        }

        document.getElementById('globalSpeed').addEventListener('input', autoStartAnimation);
        document.getElementById('globalSpeedNum').addEventListener('input', autoStartAnimation);
        document.getElementById('modRotSpeed').addEventListener('input', autoStartAnimation);
        document.getElementById('modRotSpeedNum').addEventListener('input', autoStartAnimation);

        function updateRangeDisplays() {
            document.getElementById('globalSpeedDisplay').textContent = document.getElementById('globalSpeed').value;
            document.getElementById('modRotSpeedDisplay').textContent = document.getElementById('modRotSpeed').value;
            document.getElementById('gradientStrengthDisplay').textContent = document.getElementById('gradientStrength').value;
            document.getElementById('pointSizeDisplay').textContent = document.getElementById('pointSize').value;
            document.getElementById('trackerSizeDisplay').textContent = document.getElementById('trackerSize').value;
            document.getElementById('connOpacityDisplay').textContent = document.getElementById('connOpacity').value;
        }

        document.querySelectorAll('input[type="range"]').forEach(input => {
            input.addEventListener('input', updateRangeDisplays);
        });

        function generatePointsData() {
            const modMin = parseInt(document.getElementById('modMin').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modStep = parseInt(document.getElementById('modStep').value);
            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const gapValue = parseInt(document.getElementById('gapValue').value);
            const angularMapping = document.getElementById('angularMapping').value;

            pointsData = [];
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;

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

                    let isAdmissible = false;
                    if (enableGap && isOpen) {
                        const rPlusG = (r + gapValue) % m;
                        isAdmissible = gcd(rPlusG, m) === 1;
                    }

                    // Calculate angle based on mapping mode
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
                        isAdmissible: isAdmissible
                    });
                }
            }

            const avgPhiOverM = sumPhiOverM / countModuli;
            const openRatio = totalOpen / (totalOpen + totalClosed);

            document.getElementById('statTotal').textContent = pointsData.length.toLocaleString();
            document.getElementById('statOpen').textContent = totalOpen.toLocaleString();
            document.getElementById('statClosed').textContent = totalClosed.toLocaleString();
            document.getElementById('statRatio').textContent = openRatio.toFixed(4);
            document.getElementById('statAvgPhi').textContent = avgPhiOverM.toFixed(4);

            updateTrackerInfo();
        }

        function updateTrackerInfo() {
            const enabled = document.getElementById('enableTracker').checked;
            const trackedR = parseInt(document.getElementById('trackedResidue').value);
            const trackerInfo = document.getElementById('trackerInfo');
            
            if (enabled) {
                trackerInfo.style.display = 'block';
                const trackedPoints = pointsData.filter(p => p.r === trackedR);
                let infoHTML = `Residue r = ${trackedR}<br>`;
                infoHTML += `Appears in ${trackedPoints.length} moduli<br>`;
                const openCount = trackedPoints.filter(p => p.isOpen).length;
                infoHTML += `Open: ${openCount}, Closed: ${trackedPoints.length - openCount}`;
                document.getElementById('trackerInfoContent').innerHTML = infoHTML;
            } else {
                trackerInfo.style.display = 'none';
            }
        }

        document.getElementById('enableTracker').addEventListener('change', updateTrackerInfo);
        document.getElementById('trackedResidue').addEventListener('input', updateTrackerInfo);

        function drawVisualization() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;

            // Get theme-aware background color
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
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
            const trackedResidue = parseInt(document.getElementById('trackedResidue').value);
            const trackerColor = document.getElementById('trackerColor').value;
            const trackerSize = parseFloat(document.getElementById('trackerSize').value);
            const enableConnections = document.getElementById('enableConnections').checked;
            const connectionMode = document.getElementById('connectionMode').value;
            const connOpacity = parseFloat(document.getElementById('connOpacity').value);
            const onlyOpenConn = document.getElementById('onlyOpenConn').checked;

            const radiusScale = displayMode === 'unit' ? maxRadius : maxRadius / modMax;

            // Theme-aware line color
            const lineColor = currentTheme === 'dark' ? 'rgba(255, 255, 255, 0.2)' : 'rgba(0, 0, 0, 0.2)';
            const connectionLineColor = currentTheme === 'dark' ? `rgba(255, 255, 255, ${connOpacity})` : `rgba(0, 0, 0, ${connOpacity})`;

            // Function to get proper radius for each modulus
            function getRadius(m) {
                if (displayMode === 'unit') return maxRadius;
                if (m === 1) return maxRadius * 0.1; // Unit circle for mod 1
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
                ctx.strokeStyle = connectionLineColor;
                ctx.lineWidth = 0.5 / transform.scale;

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
                pointsData.filter(p => p.r === trackedResidue).forEach(point => {
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
                animationId = requestAnimationFrame(animate);
            }
        }

        function stopAnimation() {
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
                document.getElementById('animationStatus').textContent = 'Status: Stopped';
                document.getElementById('animationStatus').style.background = 'var(--bg-secondary)';
            }
        }

        canvas.addEventListener('mousedown', (e) => {
            isDragging = true;
            lastMouseX = e.clientX;
            lastMouseY = e.clientY;
        });

        canvas.addEventListener('mousemove', (e) => {
            if (isDragging) {
                transform.x += e.clientX - lastMouseX;
                transform.y += e.clientY - lastMouseY;
                lastMouseX = e.clientX;
                lastMouseY = e.clientY;
                drawVisualization();
            }
        });

        canvas.addEventListener('mouseup', () => { isDragging = false; });
        canvas.addEventListener('mouseleave', () => { isDragging = false; });

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

        function updateVisualization() {
            generatePointsData();
            drawVisualization();
        }

        function setPreset(n) {
            const m = 30 * Math.pow(2, n);
            document.getElementById('modMin').value = m;
            document.getElementById('modMax').value = m;
            document.getElementById('modStep').value = 1;
            
            // Enable connections for nested visualization
            document.getElementById('enableConnections').checked = false;
            document.getElementById('connectionMode').value = 'none';
            
            updateVisualization();
        }

        function setPresetRange() {
            document.getElementById('modMin').value = 30;
            document.getElementById('modMax').value = 960;
            document.getElementById('modStep').value = 30;
            
            // Enable connections to show nested structure
            document.getElementById('enableConnections').checked = true;
            document.getElementById('connectionMode').value = 'binary-lift';
            document.getElementById('displayMode').value = 'rings';
            
            updateVisualization();
        }

        function exportImage() {
            const link = document.createElement('a');
            link.download = `modular_rings_${new Date().toISOString().slice(0,10)}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
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
            updateRangeDisplays();
            updateVisualization();
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            const tabs = {
                'introduction': [0, 'introductionTab'],
                'visualization': [1, 'visualizationTab'],
                'theory': [2, 'theoryTab'],
                'references': [3, 'referencesTab']
            };
            
            document.querySelectorAll('.tab')[tabs[tab][0]].classList.add('active');
            document.getElementById(tabs[tab][1]).classList.add('active');
        }

        window.addEventListener('load', () => {
            initializeTheme();
            updateRangeDisplays();
            updateVisualization();
        });
    </script>
</body>
</html>
