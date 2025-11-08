
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Modular Rings - Complete Control Suite</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #333;
            padding: 10px;
        }

        .container {
            max-width: 1900px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: center;
        }

        .header h1 {
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 6px;
        }

        .header .author {
            font-size: 13px;
            opacity: 0.95;
        }

        .tabs {
            display: flex;
            background: #f8f9fa;
            border-bottom: 2px solid #e0e0e0;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            background: #f8f9fa;
            border: none;
            font-size: 14px;
            font-weight: 600;
            color: #666;
            transition: all 0.3s;
        }

        .tab.active {
            background: white;
            color: #667eea;
            border-bottom: 3px solid #667eea;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .main-content {
            display: flex;
            flex-direction: column;
        }

        .control-panel {
            background: #f8f9fa;
            border-bottom: 2px solid #e0e0e0;
            padding: 20px;
            max-height: 70vh;
            overflow-y: auto;
        }

        .control-section {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }

        .control-section h3 {
            font-size: 15px;
            font-weight: 600;
            color: #667eea;
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 2px solid #667eea;
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
            font-size: 12px;
            font-weight: 500;
            color: #555;
            margin-bottom: 5px;
        }

        .control-group input[type="number"],
        .control-group input[type="text"],
        .control-group select {
            width: 100%;
            padding: 8px;
            border: 2px solid #e0e0e0;
            border-radius: 6px;
            font-size: 13px;
        }

        .control-group input:focus,
        .control-group select:focus {
            outline: none;
            border-color: #667eea;
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

        .checkbox-label {
            display: flex;
            align-items: center;
            font-size: 12px;
            color: #555;
            cursor: pointer;
        }

        .dual-input {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 8px;
        }

        button {
            padding: 10px 16px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        }

        .button-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 8px;
        }

        .canvas-container {
            padding: 20px;
            background: #1a1a2e;
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
        }

        #mainCanvas {
            border: 2px solid #444;
            border-radius: 8px;
            box-shadow: 0 4px 16px rgba(0,0,0,0.5);
            background: black;
            cursor: move;
            touch-action: none;
        }

        .tooltip {
            position: absolute;
            padding: 12px;
            background: rgba(0, 0, 0, 0.9);
            color: white;
            border-radius: 6px;
            pointer-events: none;
            font-size: 12px;
            line-height: 1.6;
            opacity: 0;
            transition: opacity 0.2s;
            z-index: 1000;
            max-width: 300px;
        }

        .stats-panel {
            width: 100%;
            max-width: 1000px;
            margin-top: 20px;
            background: white;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 12px;
        }

        .stat-item {
            padding: 10px;
            background: #f8f9fa;
            border-radius: 6px;
            border-left: 4px solid #667eea;
        }

        .stat-label {
            font-size: 11px;
            color: #666;
            font-weight: 500;
        }

        .stat-value {
            font-size: 16px;
            font-weight: 600;
            color: #333;
            margin-top: 4px;
        }

        .range-display {
            display: inline-block;
            margin-left: 8px;
            font-weight: 600;
            color: #667eea;
            font-size: 11px;
        }

        .info-box {
            background: #e8f4f8;
            padding: 10px;
            border-radius: 6px;
            font-size: 11px;
            color: #555;
            margin-top: 10px;
            border-left: 4px solid #667eea;
        }

        .preset-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 6px;
        }

        .color-legend {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 8px;
            margin-top: 10px;
        }

        .color-legend-item {
            display: flex;
            align-items: center;
            font-size: 11px;
        }

        .color-box {
            width: 20px;
            height: 20px;
            border-radius: 4px;
            margin-right: 6px;
            border: 1px solid #ddd;
        }

        .tracker-display {
            background: #f0f4ff;
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
            border-left: 4px solid #8b5cf6;
        }

        .tracker-display h4 {
            color: #8b5cf6;
            font-size: 13px;
            margin-bottom: 8px;
        }

        .tracker-info {
            font-size: 12px;
            line-height: 1.6;
            color: #555;
        }

        @media (max-width: 768px) {
            .control-row {
                grid-template-columns: 1fr;
            }
            .preset-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Advanced Modular Rings - Complete Control Suite</h1>
            <div class="author">Interactive Visualization by Wessen Getachew</div>
        </div>

        <div class="tabs">
            <button class="tab active" onclick="switchTab('visualization')">Visualization</button>
            <button class="tab" onclick="switchTab('theory')">Mathematical Theory</button>
        </div>

        <div id="visualizationTab" class="tab-content active">
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
                        <h3>Rotation Controls</h3>
                        <div class="control-group">
                            <label>Global Rotation Speed <span class="range-display" id="globalSpeedDisplay">0</span> deg/frame</label>
                            <div class="dual-input">
                                <input type="range" id="globalSpeed" min="0" max="360" step="0.5" value="0">
                                <input type="number" id="globalSpeedNum" min="0" max="360" step="0.5" value="0">
                            </div>
                        </div>
                        <div class="control-group">
                            <label>Individual Mod Rotation <span class="range-display" id="modRotSpeedDisplay">0</span> deg/frame</label>
                            <div class="dual-input">
                                <input type="range" id="modRotSpeed" min="0" max="360" step="0.5" value="0">
                                <input type="number" id="modRotSpeedNum" min="0" max="360" step="0.5" value="0">
                            </div>
                        </div>
                        <div class="control-group">
                            <label>Speed Gradient Direction</label>
                            <select id="speedGradient">
                                <option value="none">No Gradient</option>
                                <option value="inner-to-outer">Inner to Outer (Faster)</option>
                                <option value="outer-to-inner">Outer to Inner (Faster)</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Gradient Strength <span class="range-display" id="gradientStrengthDisplay">1.0</span></label>
                            <div class="dual-input">
                                <input type="range" id="gradientStrength" min="0" max="3" step="0.1" value="1.0">
                                <input type="number" id="gradientStrengthNum" min="0" max="5" step="0.1" value="1.0">
                            </div>
                        </div>
                        <div class="control-group">
                            <label class="checkbox-label">
                                <input type="checkbox" id="animateRotation">
                                Enable Animation
                            </label>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3>Individual Residue Tracker</h3>
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
                            <input type="color" id="trackerColor" value="#ff00ff">
                        </div>
                        <div class="control-group">
                            <label>Tracker Size <span class="range-display" id="trackerSizeDisplay">8</span></label>
                            <div class="dual-input">
                                <input type="range" id="trackerSize" min="4" max="20" step="1" value="8">
                                <input type="number" id="trackerSizeNum" min="4" max="30" step="1" value="8">
                            </div>
                        </div>
                        <div class="tracker-display" id="trackerInfo" style="display: none;">
                            <h4>Tracked Residue Information</h4>
                            <div class="tracker-info" id="trackerInfoContent"></div>
                        </div>
                    </div>

                    <div class="control-section">
                        <h3>Coloring Schemes</h3>
                        <div class="control-group">
                            <label>Open Channel Color Mode</label>
                            <select id="openColorMode">
                                <option value="solid">Solid Color</option>
                                <option value="by-residue">Color by Residue (r)</option>
                                <option value="by-modulus">Color by Modulus (m)</option>
                                <option value="by-integer">Color by Integer Value</option>
                                <option value="by-spf">Color by Smallest Prime Factor</option>
                                <option value="by-lpf">Color by Largest Prime Factor</option>
                                <option value="by-prime-power">Color by Prime Power</option>
                                <option value="by-angle">Color by Angle</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Closed Channel Color Mode</label>
                            <select id="closedColorMode">
                                <option value="solid">Solid Color</option>
                                <option value="by-gcd">Color by GCD Value</option>
                                <option value="by-spf">Color by Smallest Prime Factor</option>
                                <option value="by-lpf">Color by Largest Prime Factor</option>
                                <option value="by-modulus">Color by Modulus (m)</option>
                            </select>
                        </div>
                        <div class="control-group">
                            <label>Base Open Color (for solid mode)</label>
                            <input type="color" id="baseOpenColor" value="#4ade80">
                        </div>
                        <div class="control-group">
                            <label>Base Closed Color (for solid mode)</label>
                            <input type="color" id="baseClosedColor" value="#f87171">
                        </div>
                        <div class="control-group">
                            <label>Color Saturation <span class="range-display" id="colorSatDisplay">80</span>%</label>
                            <div class="dual-input">
                                <input type="range" id="colorSat" min="30" max="100" step="5" value="80">
                                <input type="number" id="colorSatNum" min="0" max="100" step="5" value="80">
                            </div>
                        </div>
                        <div class="control-group">
                            <label>Color Lightness <span class="range-display" id="colorLightDisplay">60</span>%</label>
                            <div class="dual-input">
                                <input type="range" id="colorLight" min="30" max="90" step="5" value="60">
                                <input type="number" id="colorLightNum" min="0" max="100" step="5" value="60">
                            </div>
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
                                <label>Background Preset</label>
                                <select id="bgPreset">
                                    <option value="#000000" selected>Black</option>
                                    <option value="#ffffff">White</option>
                                    <option value="#1a1a2e">Dark Blue</option>
                                    <option value="#0f0f23">Deep Space</option>
                                    <option value="#2d3436">Charcoal</option>
                                </select>
                            </div>
                        </div>
                        <div class="control-row">
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showOpen" checked>
                                    Show Open Channels
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showClosed" checked>
                                    Show Closed Channels
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showRingLines" checked>
                                    Show Ring Lines
                                </label>
                            </div>
                            <div class="control-group">
                                <label class="checkbox-label">
                                    <input type="checkbox" id="showRadialLines">
                                    Show Radial Lines
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
                                    Enable Gap Analysis
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
                        <button onclick="exportImage()">Export PNG</button>
                        <button onclick="exportCSV()">Export CSV</button>
                        <button onclick="resetSettings()">Reset</button>
                    </div>

                    <div class="info-box">
                        Controls: Drag to pan, scroll to zoom, hover for info, click for details
                    </div>
                </div>

                <div class="canvas-container">
                    <canvas id="mainCanvas" width="1000" height="800"></canvas>
                    <div class="tooltip" id="tooltip"></div>
                    
                    <div class="stats-panel">
                        <h3 style="margin-bottom: 12px; color: #667eea; font-size: 15px;">Statistics</h3>
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
                                <div class="stat-label">Theoretical (6/π²)</div>
                                <div class="stat-value">0.6079</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div id="theoryTab" class="tab-content">
            <div style="padding: 30px; max-width: 1200px; margin: 0 auto;">
                <h2 style="color: #667eea; font-size: 22px; margin: 25px 0 15px 0; padding-bottom: 10px; border-bottom: 2px solid #667eea;">Mathematical Framework</h2>
                
                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">1. Modular Sequence Definition</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">We study the sequence of moduli:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Modular Sequence:</div>
                    M_n = 30 × 2^n, where n ∈ ℤ≥0
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">This generates the sequence: 30, 60, 120, 240, 480, 960, 1920, ...</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">2. Open and Closed Channels</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">For any modulus m, each residue r mod m is classified based on coprimality:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Channel Classification:</div>
                    • Open Channel: gcd(r,m) = 1 (r is a totative of m)<br>
                    • Closed Channel: gcd(r,m) > 1 (r shares a common factor with m)
                </div>
                
                <div style="background: #e8f4f8; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #4ade80;">
                    <strong>Example (m = 30):</strong><br>
                    Open channels: {1, 7, 11, 13, 17, 19, 23, 29}<br>
                    Total: φ(30) = 8 open channels<br>
                    Fraction: 8/30 ≈ 0.2667
                </div>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">3. Euler's Totient Function</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The number of open channels for modulus m is given by Euler's totient function:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Totient Formula:</div>
                    φ(m) = m × ∏(1 - 1/p) for all primes p dividing m
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The fraction of open channels approaches a fundamental constant:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Density Theorem:</div>
                    lim(M→∞) [1/M × Σ(m=1 to M) φ(m)/m] = 6/π² ≈ 0.6079
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">This equals the probability that two random integers are coprime, and connects to the Riemann zeta function: ζ(2) = π²/6.</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">4. Geometric Mapping: Concentric Rings</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">Each modulus m corresponds to a ring of radius R(m) = m in the plane. Each residue r maps to:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Point Coordinates:</div>
                    P(m,r) = (R(m) × cos(2πr/m), R(m) × sin(2πr/m))<br>
                    where angle θ = 2πr/m radians
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">Open channels appear as bright points; closed channels as dim points. This creates a visual representation of coprimality patterns.</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">5. Unit Circle Projection</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">Projecting all points radially onto the unit circle maps open channels to angles 2πr/m. As m increases, these angles become dense in [0, 2π), corresponding to reduced fractions in the Farey sequence.</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">6. Farey Sequences and Fractional Channels</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The reduced fractions a/m with gcd(a,m) = 1 form the Farey sequence F_m:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Farey Sequence:</div>
                    F_m = {a/m : 0 ≤ a ≤ m, gcd(a,m) = 1}
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">These fractions correspond to "spoke-like" channels radiating from the origin, creating a tessellation pattern on the unit circle.</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">7. Binary Lifting Property</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">For the sequence M_n = 30 × 2^n, we have a preservation theorem:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Lifting Theorem:</div>
                    If gcd(r, M_n) = 1, then:<br>
                    • gcd(r, M_(n+1)) = 1<br>
                    • gcd(r + M_n, M_(n+1)) = 1
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">This creates a binary tree structure where each open channel at level n splits into two open channels at level n+1.</p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">8. Gap Admissibility</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">For studying prime gaps, we define admissible residue pairs:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Admissibility Condition:</div>
                    Residue r is g-admissible if:<br>
                    gcd(r, M) = 1 AND gcd(r+g, M) = 1
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The count of admissible residues for gap g is:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Admissible Count:</div>
                    N_M(g) = ∏(p|M) (p - f_p)<br>
                    where f_p = 1 if p|g, else f_p = 2
                </div>
                
                <div style="background: #e8f4f8; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #4ade80;">
                    <strong>Example (Twin Primes, g=2, M=30):</strong><br>
                    Primes dividing 30: {2, 3, 5}<br>
                    Since 2|2: f_2 = 1<br>
                    Since 3∤2: f_3 = 2<br>
                    Since 5∤2: f_5 = 2<br>
                    Count: (2-1)(3-2)(5-2) = 1 × 1 × 3 = 3<br>
                    Admissible residues mod 30: {11, 17, 29}
                </div>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">9. Connection to Prime Distribution</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The admissible residues mod M correspond to potential prime pairs (p, p+g). The Hardy-Littlewood conjecture predicts:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Twin Prime Constant:</div>
                    π_2(x) ~ 2C_2 × ∫(2 to x) dt/(ln t)²<br>
                    where C_2 = ∏(p>2) [1 - 1/(p-1)²] ≈ 0.6601
                </div>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">10. Euler Product Connection</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">The density of coprime pairs connects to the Euler product:</p>
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea; font-family: 'Courier New', monospace; font-size: 14px;">
                    <div style="font-weight: 600; color: #667eea; margin-bottom: 8px;">Euler Product for ζ(2):</div>
                    6/π² = ∏(p prime) (1 - 1/p²) = 1/ζ(2)
                </div>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">This fundamental constant appears in:</p>
                <ul style="margin-left: 25px; margin-bottom: 15px; line-height: 1.6;">
                    <li style="margin-bottom: 8px;">Probability two random integers are coprime</li>
                    <li style="margin-bottom: 8px;">Density of visible lattice points in ℤ²</li>
                    <li style="margin-bottom: 8px;">Average value of φ(m)/m</li>
                    <li style="margin-bottom: 8px;">Asymptotic density of squarefree integers</li>
                </ul>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">11. Advanced Visualization Features</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">
                    <strong>Rotation Mechanics:</strong><br>
                    • Global Rotation (0-360°): Rotates entire visualization uniformly<br>
                    • Individual Mod Rotation (0-360°): Each modulus ring rotates independently<br>
                    • Speed Gradients: Creates differential rotation where inner rings rotate faster than outer (or vice versa), producing hypnotic spiraling patterns
                </p>

                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">
                    <strong>Coloring Schemes:</strong><br>
                    • By Residue (r): Hue = 360° × (r / max_r). Shows periodic patterns across rings<br>
                    • By Modulus (m): Hue = 360° × (m / max_m). Distinguishes different rings<br>
                    • By Integer Value: Colors based on the actual integer r + m×k<br>
                    • By Smallest Prime Factor: Groups points by their smallest prime divisor<br>
                    • By Largest Prime Factor: Groups points by their largest prime divisor<br>
                    • By Prime Power: Colors based on highest prime power dividing the number<br>
                    • By Angle: Hue = angle in degrees. Creates rainbow wheel effect<br>
                    • By GCD: For closed channels, colors by gcd(r,m) value
                </p>

                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">
                    <strong>Individual Residue Tracker:</strong><br>
                    Highlights a specific residue r across all moduli, showing how that residue appears in different rings. Useful for studying whether r is coprime to various moduli, angular position of r across different scales, and prime residue patterns.
                </p>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">12. Research Applications</h3>
                <p style="line-height: 1.8; margin-bottom: 15px; color: #444;">This framework provides tools for:</p>
                <ul style="margin-left: 25px; margin-bottom: 15px; line-height: 1.6;">
                    <li style="margin-bottom: 8px;">Visualizing prime distribution patterns</li>
                    <li style="margin-bottom: 8px;">Studying gap admissibility and twin prime structures</li>
                    <li style="margin-bottom: 8px;">Exploring connections between modular arithmetic and the Riemann Hypothesis</li>
                    <li style="margin-bottom: 8px;">Analyzing Farey sequence properties geometrically</li>
                    <li style="margin-bottom: 8px;">Investigating totient function behavior across moduli</li>
                    <li style="margin-bottom: 8px;">Discovering patterns in prime factor distributions through color visualization</li>
                </ul>

                <h3 style="color: #764ba2; font-size: 18px; margin: 20px 0 10px 0;">13. References and Further Reading</h3>
                
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Foundational Number Theory</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Hardy, G. H., & Wright, E. M.</strong> (2008). <em>An Introduction to the Theory of Numbers</em> (6th ed.). Oxford University Press.
                        <br><span style="color: #666;">Classic reference for Euler's totient function, coprimality, and the 6/π² constant.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Apostol, T. M.</strong> (1976). <em>Introduction to Analytic Number Theory</em>. Springer-Verlag.
                        <br><span style="color: #666;">Comprehensive treatment of the Riemann zeta function and Euler products.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Farey Sequences and Continued Fractions</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Graham, R. L., Knuth, D. E., & Patashnik, O.</strong> (1994). <em>Concrete Mathematics</em> (2nd ed.). Addison-Wesley.
                        <br><span style="color: #666;">Chapter on number theory includes extensive discussion of Farey sequences.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Hardy, G. H., & Wright, E. M.</strong> (2008). Chapter 3: Farey Series and Properties of Rational Fractions.
                        <br><span style="color: #666;">Fundamental properties and applications of Farey sequences.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Prime Gaps and Twin Primes</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Hardy, G. H., & Littlewood, J. E.</strong> (1923). "Some Problems of 'Partitio Numerorum' III: On the Expression of a Number as a Sum of Primes." <em>Acta Mathematica</em>, 44(1), 1-70.
                        <br><span style="color: #666;">Original paper introducing the Hardy-Littlewood conjectures for prime k-tuples.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Zhang, Y.</strong> (2014). "Bounded gaps between primes." <em>Annals of Mathematics</em>, 179(3), 1121-1174.
                        <br><span style="color: #666;">Breakthrough result proving infinitely many primes with bounded gaps.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Polymath Project</strong> (2014). "New equidistribution estimates of Zhang type." <em>Algebra & Number Theory</em>, 8(9), 2067-2199.
                        <br><span style="color: #666;">Collaborative improvement of Zhang's bound on prime gaps.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Modular Arithmetic and Residue Systems</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Ireland, K., & Rosen, M.</strong> (1990). <em>A Classical Introduction to Modern Number Theory</em> (2nd ed.). Springer-Verlag.
                        <br><span style="color: #666;">Comprehensive treatment of modular arithmetic and primitive roots.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Niven, I., Zuckerman, H. S., & Montgomery, H. L.</strong> (1991). <em>An Introduction to the Theory of Numbers</em> (5th ed.). John Wiley & Sons.
                        <br><span style="color: #666;">Clear exposition of congruences and totient function properties.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Prime Distribution and the Riemann Hypothesis</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Riemann, B.</strong> (1859). "Über die Anzahl der Primzahlen unter einer gegebenen Größe." <em>Monatsberichte der Berliner Akademie</em>.
                        <br><span style="color: #666;">Original paper introducing the Riemann zeta function and hypothesis.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Edwards, H. M.</strong> (1974). <em>Riemann's Zeta Function</em>. Academic Press.
                        <br><span style="color: #666;">Historical and mathematical development of zeta function theory.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Davenport, H.</strong> (2000). <em>Multiplicative Number Theory</em> (3rd ed.). Springer-Verlag.
                        <br><span style="color: #666;">Advanced treatment of prime number theorem and Dirichlet characters.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Euler Products and L-Functions</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Euler, L.</strong> (1748). <em>Introductio in analysin infinitorum</em>.
                        <br><span style="color: #666;">Original development of the Euler product formula and relation to ζ(s).</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Iwaniec, H., & Kowalski, E.</strong> (2004). <em>Analytic Number Theory</em>. American Mathematical Society.
                        <br><span style="color: #666;">Modern treatment of L-functions, Euler products, and applications.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Probabilistic Number Theory</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Tenenbaum, G.</strong> (1995). <em>Introduction to Analytic and Probabilistic Number Theory</em>. Cambridge University Press.
                        <br><span style="color: #666;">Connection between probability and density results like 6/π².</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Cesàro, E.</strong> (1883). "Sur le nombre des diviseurs d'un entier." <em>Comptes Rendus de l'Académie des Sciences</em>, 96, 175-177.
                        <br><span style="color: #666;">Early probabilistic results on divisor distribution and coprimality.</span>
                    </p>
                </div>

                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin: 15px 0; border-left: 4px solid #667eea;">
                    <h4 style="color: #667eea; font-size: 14px; margin-bottom: 10px;">Computational and Visual Number Theory</h4>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Wagon, S.</strong> (1991). <em>Mathematica in Action</em>. W. H. Freeman.
                        <br><span style="color: #666;">Examples of computational exploration in number theory.</span>
                    </p>
                    <p style="font-size: 13px; line-height: 1.6; margin-bottom: 8px;">
                        <strong>Soundararajan, K.</strong> (2006). "The distribution of prime numbers." <em>Handbook of Enumerative Combinatorics</em>. CRC Press.
                        <br><span style="color: #666;">Modern survey of prime distribution patterns and visualization techniques.</span>
                    </p>
                </div>

                <div style="background: #fff3cd; padding: 15px; border-radius: 8px; margin: 20px 0; border-left: 4px solid #ffc107;">
                    <h4 style="color: #856404; font-size: 14px; margin-bottom: 8px;">Online Resources</h4>
                    <p style="font-size: 13px; line-height: 1.6; color: #856404;">
                        • <strong>OEIS</strong> (Online Encyclopedia of Integer Sequences): oeis.org<br>
                        • <strong>Prime Pages</strong> by Chris Caldwell: primes.utm.edu<br>
                        • <strong>MathWorld</strong> - Wolfram: mathworld.wolfram.com<br>
                        • <strong>arXiv Number Theory</strong>: arxiv.org/list/math.NT/recent
                    </p>
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

        function highestPrimePower(n) {
            if (n <= 1) return 1;
            let maxPower = 1;
            for (let p = 2; p * p <= n; p++) {
                let power = 0;
                while (n % p === 0) {
                    power++;
                    n /= p;
                }
                if (power > 0) {
                    maxPower = Math.max(maxPower, Math.pow(p, power));
                }
            }
            if (n > 1) maxPower = Math.max(maxPower, n);
            return maxPower;
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
            const sat = parseFloat(document.getElementById('colorSat').value);
            const light = parseFloat(document.getElementById('colorLight').value);
            
            if (isOpen) {
                const mode = document.getElementById('openColorMode').value;
                let hue = 0;
                
                if (mode === 'solid') {
                    const baseColor = document.getElementById('baseOpenColor').value;
                    return baseColor;
                } else if (mode === 'by-residue') {
                    const maxR = Math.max(...pointsData.map(p => p.r));
                    hue = (point.r / maxR) * 360;
                } else if (mode === 'by-modulus') {
                    const maxM = Math.max(...pointsData.map(p => p.m));
                    hue = (point.m / maxM) * 360;
                } else if (mode === 'by-integer') {
                    const val = point.r;
                    hue = (val * 137.5) % 360;
                } else if (mode === 'by-spf') {
                    const spf = smallestPrimeFactor(point.r === 0 ? point.m : point.r);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180, 19: 210, 23: 240, 29: 270, 31: 300};
                    hue = primeMap[spf] || ((spf * 13) % 360);
                } else if (mode === 'by-lpf') {
                    const lpf = largestPrimeFactor(point.r === 0 ? point.m : point.r);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180, 19: 210, 23: 240, 29: 270, 31: 300};
                    hue = primeMap[lpf] || ((lpf * 13) % 360);
                } else if (mode === 'by-prime-power') {
                    const pp = highestPrimePower(point.r === 0 ? point.m : point.r);
                    hue = (Math.log2(pp) / 10) * 360;
                } else if (mode === 'by-angle') {
                    hue = (point.angle / (2 * Math.PI)) * 360;
                }
                
                const [r, g, b] = hslToRgb(hue, sat, light);
                return `rgb(${r},${g},${b})`;
            } else {
                const mode = document.getElementById('closedColorMode').value;
                let hue = 0;
                
                if (mode === 'solid') {
                    return document.getElementById('baseClosedColor').value;
                } else if (mode === 'by-gcd') {
                    hue = (point.gcd / 10) * 360;
                } else if (mode === 'by-spf') {
                    const spf = smallestPrimeFactor(point.gcd);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180, 19: 210, 23: 240, 29: 270, 31: 300};
                    hue = primeMap[spf] || ((spf * 13) % 360);
                } else if (mode === 'by-lpf') {
                    const lpf = largestPrimeFactor(point.gcd);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180, 19: 210, 23: 240, 29: 270, 31: 300};
                    hue = primeMap[lpf] || ((lpf * 13) % 360);
                } else if (mode === 'by-modulus') {
                    const maxM = Math.max(...pointsData.map(p => p.m));
                    hue = (point.m / maxM) * 360;
                }
                
                const [r, g, b] = hslToRgb(hue, sat, light * 0.7);
                return `rgb(${r},${g},${b})`;
            }
        }

        function syncInputs(sliderId, numberId) {
            const slider = document.getElementById(sliderId);
            const number = document.getElementById(numberId);
            
            slider.addEventListener('input', () => {
                number.value = slider.value;
                updateRangeDisplays();
            });
            
            number.addEventListener('input', () => {
                slider.value = number.value;
                updateRangeDisplays();
            });
        }

        syncInputs('globalSpeed', 'globalSpeedNum');
        syncInputs('modRotSpeed', 'modRotSpeedNum');
        syncInputs('gradientStrength', 'gradientStrengthNum');
        syncInputs('trackedResidue', 'trackedResidueNum');
        syncInputs('trackerSize', 'trackerSizeNum');
        syncInputs('pointSize', 'pointSizeNum');
        syncInputs('colorSat', 'colorSatNum');
        syncInputs('colorLight', 'colorLightNum');

        function updateRangeDisplays() {
            document.getElementById('globalSpeedDisplay').textContent = document.getElementById('globalSpeed').value;
            document.getElementById('modRotSpeedDisplay').textContent = document.getElementById('modRotSpeed').value;
            document.getElementById('gradientStrengthDisplay').textContent = document.getElementById('gradientStrength').value;
            document.getElementById('pointSizeDisplay').textContent = document.getElementById('pointSize').value;
            document.getElementById('trackerSizeDisplay').textContent = document.getElementById('trackerSize').value;
            document.getElementById('colorSatDisplay').textContent = document.getElementById('colorSat').value;
            document.getElementById('colorLightDisplay').textContent = document.getElementById('colorLight').value;
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

                    const angle = (2 * Math.PI * r) / m;

                    pointsData.push({
                        m: m,
                        r: r,
                        gcd: g,
                        isOpen: isOpen,
                        angle: angle,
                        angleDeg: (angle * 180 / Math.PI).toFixed(2),
                        fraction: (r / m).toFixed(6),
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
                let infoHTML = `<strong>Residue r = ${trackedR}</strong><br>`;
                infoHTML += `Appears in ${trackedPoints.length} moduli<br>`;
                const openCount = trackedPoints.filter(p => p.isOpen).length;
                infoHTML += `Open in ${openCount} rings, Closed in ${trackedPoints.length - openCount} rings`;
                document.getElementById('trackerInfoContent').innerHTML = infoHTML;
            } else {
                trackerInfo.style.display = 'none';
            }
        }

        document.getElementById('enableTracker').addEventListener('change', updateTrackerInfo);
        document.getElementById('trackedResidue').addEventListener('input', updateTrackerInfo);
        document.getElementById('trackedResidueNum').addEventListener('input', updateTrackerInfo);

        document.getElementById('bgPreset').addEventListener('change', (e) => {
            document.getElementById('bgColor').value = e.target.value;
        });

        document.getElementById('bgColor').addEventListener('input', (e) => {
            const value = e.target.value;
            const preset = document.getElementById('bgPreset');
            const options = Array.from(preset.options);
            const match = options.find(opt => opt.value === value);
            if (match) {
                preset.value = value;
            }
        });

        function drawVisualization() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.4;

            const bgColor = document.getElementById('bgColor').value;
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
            const showRadialLines = document.getElementById('showRadialLines').checked;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modMin = parseInt(document.getElementById('modMin').value);
            const modStep = parseInt(document.getElementById('modStep').value);
            const enableTracker = document.getElementById('enableTracker').checked;
            const trackedResidue = parseInt(document.getElementById('trackedResidue').value);
            const trackerColor = document.getElementById('trackerColor').value;
            const trackerSize = parseFloat(document.getElementById('trackerSize').value);

            const radiusScale = displayMode === 'unit' ? maxRadius : maxRadius / modMax;

            if (showRingLines && displayMode === 'rings') {
                ctx.strokeStyle = 'rgba(200, 200, 200, 0.3)';
                ctx.lineWidth = 1 / transform.scale;
                for (let m = modMin; m <= modMax; m += modStep) {
                    ctx.beginPath();
                    ctx.arc(0, 0, m * radiusScale, 0, 2 * Math.PI);
                    ctx.stroke();
                }
            }

            if (displayMode === 'unit') {
                ctx.strokeStyle = 'rgba(100, 100, 100, 0.5)';
                ctx.lineWidth = 2 / transform.scale;
                ctx.beginPath();
                ctx.arc(0, 0, maxRadius, 0, 2 * Math.PI);
                ctx.stroke();
            }

            if (showRadialLines && displayMode === 'rings') {
                const uniqueAngles = [...new Set(pointsData.filter(p => p.isOpen).map(p => p.angle))];
                ctx.strokeStyle = 'rgba(102, 126, 234, 0.15)';
                ctx.lineWidth = 0.5 / transform.scale;
                uniqueAngles.forEach(angle => {
                    const x = maxRadius * Math.cos(angle);
                    const y = maxRadius * Math.sin(angle);
                    ctx.beginPath();
                    ctx.moveTo(0, 0);
                    ctx.lineTo(x, y);
                    ctx.stroke();
                });
            }

            pointsData.forEach(point => {
                if (!showOpen && point.isOpen) return;
                if (!showClosed && !point.isOpen) return;

                const modRot = modRotations[point.m] || 0;
                const totalAngle = point.angle + (modRot * Math.PI / 180);
                const r = displayMode === 'unit' ? maxRadius : point.m * radiusScale;
                const x = r * Math.cos(totalAngle);
                const y = r * Math.sin(totalAngle);

                let radius = pointSize;
                let color = getColorForPoint(point, point.isOpen);
                let opacity = point.isOpen ? 0.8 : 0.3;

                if (point.isAdmissible) {
                    radius = pointSize * 1.2;
                    color = '#8b5cf6';
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

            if (enableTracker) {
                pointsData.filter(p => p.r === trackedResidue).forEach(point => {
                    const modRot = modRotations[point.m] || 0;
                    const totalAngle = point.angle + (modRot * Math.PI / 180);
                    const r = displayMode === 'unit' ? maxRadius : point.m * radiusScale;
                    const x = r * Math.cos(totalAngle);
                    const y = r * Math.sin(totalAngle);

                    ctx.strokeStyle = trackerColor;
                    ctx.lineWidth = 3 / transform.scale;
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
            if (!document.getElementById('animateRotation').checked) {
                animationId = null;
                return;
            }

            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            const speedGradient = document.getElementById('speedGradient').value;
            const gradientStrength = parseFloat(document.getElementById('gradientStrength').value);
            const modMax = parseInt(document.getElementById('modMax').value);
            const modMin = parseInt(document.getElementById('modMin').value);

            globalRotation += globalSpeed;
            if (globalRotation > 360) globalRotation -= 360;
            if (globalRotation < 0) globalRotation += 360;

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
                if (modRotations[m] < 0) modRotations[m] += 360;
            });

            drawVisualization();
            animationId = requestAnimationFrame(animate);
        }

        document.getElementById('animateRotation').addEventListener('change', (e) => {
            if (e.target.checked && !animationId) {
                animate();
            }
        });

        function screenToCanvas(screenX, screenY) {
            const rect = canvas.getBoundingClientRect();
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            
            const canvasX = screenX - rect.left;
            const canvasY = screenY - rect.top;
            
            const worldX = (canvasX - centerX - transform.x) / transform.scale;
            const worldY = (canvasY - centerY - transform.y) / transform.scale;
            
            return { x: worldX, y: worldY };
        }

        function findPointAtPosition(x, y) {
            const pos = screenToCanvas(x, y);
            
            for (let i = pointsData.length - 1; i >= 0; i--) {
                const point = pointsData[i];
                if (!point.screenX) continue;
                
                const dx = pos.x - point.screenX;
                const dy = pos.y - point.screenY;
                const dist = Math.sqrt(dx * dx + dy * dy);
                
                if (dist <= point.screenRadius * 2) {
                    return point;
                }
            }
            return null;
        }

        canvas.addEventListener('mousedown', (e) => {
            isDragging = true;
            lastMouseX = e.clientX;
            lastMouseY = e.clientY;
            canvas.style.cursor = 'grabbing';
        });

        canvas.addEventListener('mousemove', (e) => {
            if (isDragging) {
                const dx = e.clientX - lastMouseX;
                const dy = e.clientY - lastMouseY;
                transform.x += dx;
                transform.y += dy;
                lastMouseX = e.clientX;
                lastMouseY = e.clientY;
                drawVisualization();
            } else {
                const point = findPointAtPosition(e.clientX, e.clientY);
                if (point) {
                    canvas.style.cursor = 'pointer';
                    let tooltipHTML = `<strong>Modulus:</strong> ${point.m}<br>`;
                    tooltipHTML += `<strong>Residue:</strong> ${point.r}<br>`;
                    tooltipHTML += `<strong>GCD(r,m):</strong> ${point.gcd}<br>`;
                    tooltipHTML += `<strong>Channel:</strong> ${point.isOpen ? 'OPEN' : 'CLOSED'}<br>`;
                    tooltipHTML += `<strong>Fraction:</strong> ${point.fraction}<br>`;
                    tooltipHTML += `<strong>Angle:</strong> ${point.angleDeg}°<br>`;
                    tooltipHTML += `<strong>φ(m):</strong> ${point.phiM}`;
                    
                    if (point.r > 0) {
                        tooltipHTML += `<br><strong>SPF(r):</strong> ${smallestPrimeFactor(point.r)}`;
                        tooltipHTML += `<br><strong>LPF(r):</strong> ${largestPrimeFactor(point.r)}`;
                    }
                    
                    if (point.isAdmissible) {
                        const gap = document.getElementById('gapValue').value;
                        tooltipHTML += `<br><strong style="color: #8b5cf6;">GAP ADMISSIBLE (g=${gap})</strong>`;
                    }
                    
                    tooltip.innerHTML = tooltipHTML;
                    tooltip.style.opacity = '1';
                    tooltip.style.left = (e.clientX + 15) + 'px';
                    tooltip.style.top = (e.clientY - 15) + 'px';
                } else {
                    canvas.style.cursor = 'move';
                    tooltip.style.opacity = '0';
                }
            }
        });

        canvas.addEventListener('mouseup', () => {
            isDragging = false;
            canvas.style.cursor = 'move';
        });

        canvas.addEventListener('mouseleave', () => {
            isDragging = false;
            canvas.style.cursor = 'move';
            tooltip.style.opacity = '0';
        });

        canvas.addEventListener('click', (e) => {
            const point = findPointAtPosition(e.clientX, e.clientY);
            if (point) {
                let alertText = `Modulus: ${point.m}\n`;
                alertText += `Residue: ${point.r}\n`;
                alertText += `GCD(r,m): ${point.gcd}\n`;
                alertText += `Channel: ${point.isOpen ? 'OPEN' : 'CLOSED'}\n`;
                alertText += `Fraction: ${point.fraction}\n`;
                alertText += `Angle: ${point.angleDeg}°\n`;
                alertText += `φ(m): ${point.phiM}\n`;
                alertText += `φ(m)/m: ${(point.phiM / point.m).toFixed(4)}`;
                
                if (point.r > 0) {
                    alertText += `\nSmallest Prime Factor: ${smallestPrimeFactor(point.r)}`;
                    alertText += `\nLargest Prime Factor: ${largestPrimeFactor(point.r)}`;
                }
                
                alert(alertText);
            }
        });

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

        let touchStartDist = 0;
        let touchStartScale = 1;

        canvas.addEventListener('touchstart', (e) => {
            if (e.touches.length === 2) {
                const dx = e.touches[0].clientX - e.touches[1].clientX;
                const dy = e.touches[0].clientY - e.touches[1].clientY;
                touchStartDist = Math.sqrt(dx * dx + dy * dy);
                touchStartScale = transform.scale;
            } else if (e.touches.length === 1) {
                isDragging = true;
                lastMouseX = e.touches[0].clientX;
                lastMouseY = e.touches[0].clientY;
            }
        });

        canvas.addEventListener('touchmove', (e) => {
            e.preventDefault();
            if (e.touches.length === 2) {
                const dx = e.touches[0].clientX - e.touches[1].clientX;
                const dy = e.touches[0].clientY - e.touches[1].clientY;
                const dist = Math.sqrt(dx * dx + dy * dy);
                transform.scale = touchStartScale * (dist / touchStartDist);
                transform.scale = Math.max(0.1, Math.min(20, transform.scale));
                drawVisualization();
            } else if (e.touches.length === 1 && isDragging) {
                const dx = e.touches[0].clientX - lastMouseX;
                const dy = e.touches[0].clientY - lastMouseY;
                transform.x += dx;
                transform.y += dy;
                lastMouseX = e.touches[0].clientX;
                lastMouseY = e.touches[0].clientY;
                drawVisualization();
            }
        });

        canvas.addEventListener('touchend', () => {
            isDragging = false;
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
            updateVisualization();
        }

        function setPresetRange() {
            document.getElementById('modMin').value = 30;
            document.getElementById('modMax').value = 960;
            document.getElementById('modStep').value = 30;
            updateVisualization();
        }

        function exportImage() {
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
            link.download = `modular_rings_${timestamp}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
        }

        function exportCSV() {
            let csv = 'Modulus,Residue,GCD,Channel_Type,Angle_Radians,Angle_Degrees,Fraction,Phi_m,Phi_m_over_m,SPF,LPF,Is_Admissible\n';
            
            pointsData.forEach(point => {
                csv += `${point.m},${point.r},${point.gcd},${point.isOpen ? 'Open' : 'Closed'},`;
                csv += `${point.angle.toFixed(6)},${point.angleDeg},${point.fraction},`;
                csv += `${point.phiM},${(point.phiM / point.m).toFixed(6)},`;
                csv += `${point.r > 0 ? smallestPrimeFactor(point.r) : 'N/A'},`;
                csv += `${point.r > 0 ? largestPrimeFactor(point.r) : 'N/A'},`;
                csv += `${point.isAdmissible ? 'Yes' : 'No'}\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            const timestamp = new Date().toISOString().replace(/[:.]/g, '-');
            link.download = `modular_rings_data_${timestamp}.csv`;
            link.href = url;
            link.click();
            URL.revokeObjectURL(url);
        }

        function resetSettings() {
            document.getElementById('modMin').value = '1';
            document.getElementById('modMax').value = '60';
            document.getElementById('modStep').value = '1';
            document.getElementById('displayMode').value = 'rings';
            document.getElementById('showRingLines').checked = true;
            document.getElementById('showRadialLines').checked = false;
            document.getElementById('pointSize').value = '4';
            document.getElementById('showOpen').checked = true;
            document.getElementById('showClosed').checked = true;
            document.getElementById('enableGapAnalysis').checked = false;
            document.getElementById('gapValue').value = '2';
            document.getElementById('globalSpeed').value = '0';
            document.getElementById('modRotSpeed').value = '0';
            document.getElementById('speedGradient').value = 'none';
            document.getElementById('gradientStrength').value = '1.0';
            document.getElementById('animateRotation').checked = false;
            document.getElementById('enableTracker').checked = false;
            document.getElementById('trackedResidue').value = '1';
            document.getElementById('openColorMode').value = 'solid';
            document.getElementById('closedColorMode').value = 'solid';
            document.getElementById('colorSat').value = '80';
            document.getElementById('colorLight').value = '60';
            document.getElementById('bgColor').value = '#000000';
            document.getElementById('bgPreset').value = '#000000';
            
            globalRotation = 0;
            modRotations = {};
            transform = { x: 0, y: 0, scale: 1 };
            
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
            }
            
            updateRangeDisplays();
            updateVisualization();
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            if (tab === 'visualization') {
                document.querySelector('.tab:nth-child(1)').classList.add('active');
                document.getElementById('visualizationTab').classList.add('active');
            } else {
                document.querySelector('.tab:nth-child(2)').classList.add('active');
                document.getElementById('theoryTab').classList.add('active');
            }
        }

        window.addEventListener('load', () => {
            updateRangeDisplays();
            updateVisualization();
        });

        window.addEventListener('resize', () => {
            if (pointsData.length > 0) {
                drawVisualization();
            }
        });
    </script>
</body>
</html>
