
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
            <button class="tab" onclick="switchTab('bridge')">Euler-Maclaurin Bridge</button>
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
                        
                        <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 12px; margin-bottom: 15px;">
                            <h4 style="font-size: 12px; margin-bottom: 10px; text-transform: uppercase; letter-spacing: 1px;">Static Rotation (Applied Once)</h4>
                            
                            <div class="control-group">
                                <label>Global Static Rotation (degrees)</label>
                                <div class="dual-input">
                                    <input type="number" id="staticGlobalRotation" value="0" step="1">
                                    <button onclick="applyStaticGlobalRotation()" style="padding: 8px;">Apply</button>
                                </div>
                            </div>

                            <div class="control-group">
                                <label>Individual Mod Static Rotation (degrees)</label>
                                <div class="dual-input">
                                    <input type="number" id="staticModRotation" value="0" step="1">
                                    <button onclick="applyStaticModRotation()" style="padding: 8px;">Apply</button>
                                </div>
                            </div>

                            <div class="control-group">
                                <label>Differential Rotation Mode</label>
                                <select id="staticDifferentialMode">
                                    <option value="none">Uniform (All Same)</option>
                                    <option value="inner-faster">Inner Faster than Outer</option>
                                    <option value="outer-faster">Outer Faster than Inner</option>
                                </select>
                            </div>

                            <div class="control-group">
                                <label>Differential Factor <span class="range-display" id="staticDiffFactorDisplay">2.0</span></label>
                                <div class="dual-input">
                                    <input type="range" id="staticDiffFactor" min="1" max="5" step="0.1" value="2.0">
                                    <input type="number" id="staticDiffFactorNum" min="1" max="10" step="0.1" value="2.0">
                                </div>
                            </div>

                            <div class="control-group">
                                <button onclick="applyDifferentialRotation()" style="width: 100%;">Apply Differential Rotation</button>
                            </div>

                            <div class="control-group">
                                <button onclick="resetAllRotations()" style="width: 100%; background: var(--bg-primary); color: var(--text-primary);">Reset All Rotations</button>
                            </div>
                        </div>

                        <div style="background: var(--bg-secondary); border: 1px solid var(--border-color); padding: 12px;">
                            <h4 style="font-size: 12px; margin-bottom: 10px; text-transform: uppercase; letter-spacing: 1px;">Animated Rotation (Continuous)</h4>
                            
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
                            <label>Track Residues (comma-separated)</label>
                            <input type="text" id="trackedResidues" value="1" placeholder="e.g., 1,7,13,19">
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

        <div id="bridgeTab" class="tab-content">
            <div class="theory-section">
                <h2>Euler-Maclaurin Bridge Analysis</h2>
                
                <div class="intro-box">
                    <h3>The Discrete-Continuous Duality</h3>
                    <p>
                        The Euler-Maclaurin formula bridges discrete summation and continuous integration through Bernoulli number corrections. 
                        This framework reveals an analogous structure in modular arithmetic: the <strong>Modular Pair Combinatorics</strong> 
                        framework provides a discrete-modular continuation where residue transitions replace Bernoulli corrections.
                    </p>
                </div>

                <h3>Core Correspondence</h3>
                <div class="formula">
                    <div class="formula-title">Classical Euler-Maclaurin</div>
                    Σf(n) = ∫f(x)dx + [f(a)+f(b)]/2 + Σ[B₂ₙ/(2n)!](f^(2n-1)(b) - f^(2n-1)(a))
                </div>

                <div class="formula">
                    <div class="formula-title">Modular Continuation Analogue</div>
                    Σ_{r∈Φ(M)} f(r) = ∫_{Φ(M)} f(x)dx + C_mod(M_n)
                </div>

                <h3>Live Correction Series</h3>
                <div id="correctionSeriesDisplay" class="tracker-display">
                    <h4>Modular Bernoulli Analogues 𝕋₂ₖ(Mₖ)</h4>
                    <div class="tracker-info" id="correctionSeriesContent">
                        Click "Update Display" in Visualization tab to compute...
                    </div>
                </div>

                <h3>Convergence Analysis</h3>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
                    <canvas id="convergenceChart" width="500" height="300" style="border: 1px solid var(--border-color);"></canvas>
                    <canvas id="correctionChart" width="500" height="300" style="border: 1px solid var(--border-color);"></canvas>
                </div>

                <h3>Modular Curvature Coefficients</h3>
                <div class="example-box">
                    <p><strong>Theoretical Result:</strong> For M_n = 30 × 2^n, the modular correction amplitude follows:</p>
                    <div class="formula" style="margin: 10px 0;">
                        𝕋₂ₙ(M_n) ∝ [T(M_n) - T(M_{n-1})]/T(M_n) = [3×2^n - 3×2^(n-1)]/(3×2^n) = 1/2
                    </div>
                    <p>This constant halving matches the decay structure of Bernoulli corrections in classical Euler-Maclaurin.</p>
                </div>

                <h3>Residue Transition Dynamics</h3>
                <div id="transitionAnalysis" class="tracker-display">
                    <h4>Doubling Transition Law: T(M_n) = 3 × 2^n</h4>
                    <div class="tracker-info" id="transitionContent">
                        <div id="transitionTable"></div>
                    </div>
                </div>

                <h3>Interpretation: Dual Curvature Structures</h3>
                <div class="intro-box">
                    <p><strong>Analytic Domain (Bernoulli):</strong> B₂ₙ encode oscillatory curvature corrections that exponentially decay, balancing discrete sums against continuous integrals.</p>
                    <p><strong>Modular Domain (Residue Doubling):</strong> T(M_n) encode combinatorial transition corrections that geometrically decay (halving at each level), balancing discrete residue counts against continuous coprime densities.</p>
                    <p style="margin-top: 15px; padding-top: 15px; border-top: 1px solid var(--border-color);">
                        <strong>Unified Principle:</strong> Both frameworks exhibit layered refinement through hierarchical correction patterns, 
                        revealing that <em>modular arithmetic realizes Euler-Maclaurin structure in purely combinatorial form</em>.
                    </p>
                </div>

                <h3>Key Observations from Visualization Data</h3>
                <div class="stats-panel" style="max-width: 100%;">
                    <div class="stats-grid" style="grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));">
                        <div class="stat-item">
                            <div class="stat-label">Observed φ(m)/m Average</div>
                            <div class="stat-value" id="bridgeAvgPhi">--</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Theoretical Limit (6/π²)</div>
                            <div class="stat-value">0.607927</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Convergence Error</div>
                            <div class="stat-value" id="bridgeError">--</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Modular Levels (n)</div>
                            <div class="stat-value" id="bridgeLevels">--</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Total Transitions</div>
                            <div class="stat-value" id="bridgeTransitions">--</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Doubling Ratio</div>
                            <div class="stat-value" id="bridgeRatio">2.000</div>
                        </div>
                    </div>
                </div>

                <button onclick="updateBridgeAnalysis()" style="width: 100%; margin-top: 20px; padding: 15px; font-size: 14px;">
                    Refresh Bridge Analysis
                </button>
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
        let currentTheme = 'light';

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

        syncInputs('labelSize', 'labelSizeNum');
        syncInputs('labelSpacing', 'labelSpacingNum');
        syncInputs('gapOpacity', 'gapOpacityNum');
        syncInputs('gapLineWidth', 'gapLineWidthNum');
        syncInputs('staticDiffFactor', 'staticDiffFactorNum');

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
            document.getElementById('labelSizeDisplay').textContent = document.getElementById('labelSize').value;
            document.getElementById('labelSpacingDisplay').textContent = document.getElementById('labelSpacing').value;
            document.getElementById('gapOpacityDisplay').textContent = document.getElementById('gapOpacity').value;
            document.getElementById('gapLineWidthDisplay').textContent = document.getElementById('gapLineWidth').value;
        }

        document.querySelectorAll('input[type="range"]').forEach(input => {
            input.addEventListener('input', updateRangeDisplays);
        });

        function generatePointsData() {
            const modMin = parseInt(document.getElementById('modMin').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modStep = parseInt(document.getElementById('modStep').value);
            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const gapInput = document.getElementById('gapValues').value;
            const gaps = gapInput.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g) && g > 0);
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

                    // Check admissibility for ALL gaps
                    let admissibleGaps = [];
                    if (enableGap && isOpen) {
                        gaps.forEach(gap => {
                            const rPlusG = (r + gap) % m;
                            if (gcd(rPlusG, m) === 1) {
                                admissibleGaps.push(gap);
                            }
                        });
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
                        isAdmissible: admissibleGaps.length > 0,
                        admissibleGaps: admissibleGaps // Store which gaps are admissible
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
                if (displayMode === 'unit') {
                    // In unit circle mode, all gcd(r,m)=1 points map to the outer circle
                    return maxRadius;
                }
                // Rings mode - scale by modulus
                // m=1 is innermost, starting point
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
            if (!isDragging) {
                // Click detected
                const coords = e.changedTouches ? 
                    { x: e.changedTouches[0].clientX, y: e.changedTouches[0].clientY } :
                    { x: e.clientX, y: e.clientY };
                    
                const rect = canvas.getBoundingClientRect();
                const x = (coords.x - rect.left - canvas.width / 2 - transform.x) / transform.scale;
                const y = (coords.y - rect.top - canvas.height / 2 - transform.y) / transform.scale;
                
                const angle = -globalRotation * Math.PI / 180;
                const rx = x * Math.cos(angle) - y * Math.sin(angle);
                const ry = x * Math.sin(angle) + y * Math.cos(angle);
                
                pointsData.forEach(point => {
                    if (point.screenX !== undefined) {
                        const dx = rx - point.screenX;
                        const dy = ry - point.screenY;
                        const dist = Math.sqrt(dx * dx + dy * dy);
                        if (dist < point.screenRadius * 2) {
                            alert(`Point Details:\n\nModulus m = ${point.m}\nResidue r = ${point.r}\ngcd(${point.r}, ${point.m}) = ${point.gcd}\nChannel: ${point.isOpen ? 'OPEN' : 'CLOSED'}\nφ(${point.m}) = ${point.phiM}\nAngle: ${(point.angle * 180 / Math.PI).toFixed(2)}°${point.isAdmissible ? '\n\nGAP ADMISSIBLE' : ''}`);
                        }
                    }
                });
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
            if (pointsData.length === 0) {
                alert('Please generate visualization data first by clicking "Update Display" in the Visualization tab.');
                return;
            }

            // Compute modular correction series
            const moduli = [...new Set(pointsData.map(p => p.m))].sort((a,b) => a-b);
            const M30Sequence = moduli.filter(m => m >= 30 && (m % 30 === 0) && Math.log2(m/30) % 1 === 0);
            
            let correctionHTML = '<table style="width: 100%; font-size: 11px; border-collapse: collapse;">';
            correctionHTML += '<tr style="border-bottom: 1px solid var(--border-color);"><th>n</th><th>M_n</th><th>T(M_n)</th><th>ΔT</th><th>𝕋₂ₙ = ΔT/T(M_n)</th><th>Cumulative</th></tr>';
            
            let cumulativeCorrection = 0;
            let correctionData = [];
            
            M30Sequence.forEach((m, idx) => {
                const n = Math.log2(m / 30);
                const T_n = 3 * Math.pow(2, n);
                const T_prev = idx === 0 ? 0 : 3 * Math.pow(2, n-1);
                const deltaT = T_n - T_prev;
                const coefficient = T_prev === 0 ? 1 : deltaT / T_n;
                cumulativeCorrection += coefficient;
                
                correctionData.push({n, M: m, T: T_n, coeff: coefficient, cumul: cumulativeCorrection});
                
                correctionHTML += `<tr style="border-bottom: 1px solid var(--border-subtle);">`;
                correctionHTML += `<td style="padding: 5px;">${n}</td>`;
                correctionHTML += `<td>${m}</td>`;
                correctionHTML += `<td>${T_n}</td>`;
                correctionHTML += `<td>${deltaT}</td>`;
                correctionHTML += `<td><strong>${coefficient.toFixed(4)}</strong></td>`;
                correctionHTML += `<td>${cumulativeCorrection.toFixed(4)}</td>`;
                correctionHTML += `</tr>`;
            });
            correctionHTML += '</table>';
            document.getElementById('correctionSeriesContent').innerHTML = correctionHTML;

            // Transition table
            let transitionHTML = '<table style="width: 100%; font-size: 11px; border-collapse: collapse;">';
            transitionHTML += '<tr style="border-bottom: 1px solid var(--border-color);"><th>Level n</th><th>M_n = 30×2^n</th><th>T(M_n) = 3×2^n</th><th>φ(M_n)</th><th>φ(M_n)/M_n</th></tr>';
            
            M30Sequence.forEach(m => {
                const n = Math.log2(m / 30);
                const T_n = 3 * Math.pow(2, n);
                const phiM = phi(m);
                const ratio = phiM / m;
                
                transitionHTML += `<tr style="border-bottom: 1px solid var(--border-subtle);">`;
                transitionHTML += `<td style="padding: 5px;">${n}</td>`;
                transitionHTML += `<td>${m}</td>`;
                transitionHTML += `<td>${T_n}</td>`;
                transitionHTML += `<td>${phiM}</td>`;
                transitionHTML += `<td>${ratio.toFixed(6)}</td>`;
                transitionHTML += `</tr>`;
            });
            transitionHTML += '</table>';
            document.getElementById('transitionTable').innerHTML = transitionHTML;

            // Update bridge statistics
            const avgPhi = parseFloat(document.getElementById('statAvgPhi').textContent);
            const theoretical = 6 / (Math.PI * Math.PI);
            const error = Math.abs(avgPhi - theoretical);
            
            document.getElementById('bridgeAvgPhi').textContent = avgPhi.toFixed(6);
            document.getElementById('bridgeError').textContent = error.toFixed(6);
            document.getElementById('bridgeLevels').textContent = M30Sequence.length;
            document.getElementById('bridgeTransitions').textContent = M30Sequence.length > 0 ? 
                (3 * Math.pow(2, M30Sequence.length - 1)).toFixed(0) : '0';

            // Draw convergence chart
            drawConvergenceChart(correctionData, avgPhi, theoretical);
            
            // Draw correction amplitude chart
            drawCorrectionChart(correctionData);
        }

        function drawConvergenceChart(correctionData, observed, theoretical) {
            const canvas = document.getElementById('convergenceChart');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const padding = 50;
            
            // Clear and setup
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
            const lineColor = currentTheme === 'dark' ? '#ffffff' : '#000000';
            const gridColor = currentTheme === 'dark' ? '#333333' : '#cccccc';
            
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, width, height);
            
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
            const yTheory = height - padding - ((theoretical - 0.5) / 0.15) * (height - 2 * padding);
            ctx.beginPath();
            ctx.moveTo(padding, yTheory);
            ctx.lineTo(width - padding, yTheory);
            ctx.stroke();
            ctx.setLineDash([]);
            
            // Plot observed convergence
            if (correctionData.length > 0) {
                ctx.strokeStyle = '#ff0000';
                ctx.lineWidth = 2;
                ctx.beginPath();
                
                correctionData.forEach((d, i) => {
                    const x = padding + (i / (correctionData.length - 1)) * (width - 2 * padding);
                    const y = height - padding - ((observed - 0.5) / 0.15) * (height - 2 * padding);
                    
                    if (i === 0) ctx.moveTo(x, y);
                    else ctx.lineTo(x, y);
                });
                ctx.stroke();
            }
            
            // Labels
            ctx.fillStyle = lineColor;
            ctx.font = '11px Arial';
            ctx.fillText('φ(m)/m Convergence', width / 2 - 60, 20);
            ctx.fillText('0.50', padding - 35, height - padding + 5);
            ctx.fillText('0.65', padding - 35, padding + 5);
            ctx.fillStyle = '#00ff00';
            ctx.fillText('6/π² limit', width - padding + 5, yTheory + 5);
            ctx.fillStyle = '#ff0000';
            ctx.fillText('Observed', width - padding + 5, height - padding - 20);
        }

        function drawCorrectionChart(correctionData) {
            const canvas = document.getElementById('correctionChart');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const padding = 50;
            
            // Clear and setup
            const bgColor = currentTheme === 'dark' ? '#000000' : '#ffffff';
            const lineColor = currentTheme === 'dark' ? '#ffffff' : '#000000';
            
            ctx.fillStyle = bgColor;
            ctx.fillRect(0, 0, width, height);
            
            // Draw axes
            ctx.strokeStyle = lineColor;
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(padding, padding);
            ctx.lineTo(padding, height - padding);
            ctx.lineTo(width - padding, height - padding);
            ctx.stroke();
            
            // Draw expected 1/2 line
            ctx.strokeStyle = '#0080ff';
            ctx.lineWidth = 2;
            ctx.setLineDash([5, 5]);
            const yHalf = height - padding - (0.5 / 1.0) * (height - 2 * padding);
            ctx.beginPath();
            ctx.moveTo(padding, yHalf);
            ctx.lineTo(width - padding, yHalf);
            ctx.stroke();
            ctx.setLineDash([]);
            
            // Plot correction coefficients
            if (correctionData.length > 0) {
                ctx.fillStyle = '#ff0000';
                
                correctionData.forEach((d, i) => {
                    const x = padding + (i / (correctionData.length - 1)) * (width - 2 * padding);
                    const y = height - padding - (d.coeff / 1.0) * (height - 2 * padding);
                    const barWidth = (width - 2 * padding) / correctionData.length * 0.6;
                    
                    ctx.fillRect(x - barWidth / 2, y, barWidth, height - padding - y);
                });
            }
            
            // Labels
            ctx.fillStyle = lineColor;
            ctx.font = '11px Arial';
            ctx.fillText('Correction Coefficients 𝕋₂ₙ', width / 2 - 70, 20);
            ctx.fillText('0', padding - 15, height - padding + 5);
            ctx.fillText('1', padding - 15, padding + 5);
            ctx.fillStyle = '#0080ff';
            ctx.fillText('Expected: 1/2', width - padding + 5, yHalf + 5);
        }

        function updateVisualization() {
            generatePointsData();
            drawVisualization();
            updateBridgeAnalysis();
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
