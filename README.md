
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Modular Mathematics Analyzer & Farey Channels</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
    <!-- MathJax for LaTeX rendering -->
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <style>
        /* Combined CSS from both files */
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Georgia', serif;
            line-height: 1.6;
            color: #333;
            background: #f8f9fa;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            overflow: hidden;
            margin-bottom: 25px;
            border-left: 4px solid var(--secondary);
            padding: 25px;
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid #eee;
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 10px;
            font-weight: 600;
        }
        
        h2 {
            color: var(--primary);
            border-bottom: 2px solid var(--secondary);
            padding-bottom: 8px;
            margin-top: 30px;
            font-weight: 500;
        }
        
        h3 {
            color: var(--dark);
            margin-top: 25px;
            font-weight: 500;
        }
        
        .tab-container {
            margin: 20px 0;
        }
        
        .tab-buttons {
            display: flex;
            background: #f8f9fa;
            border-radius: 6px;
            padding: 5px;
            margin-bottom: 20px;
        }
        
        .tab-button {
            flex: 1;
            padding: 12px 20px;
            background: none;
            border: none;
            cursor: pointer;
            font-weight: 500;
            color: var(--dark);
            transition: all 0.3s;
            border-radius: 4px;
        }
        
        .tab-button.active {
            background: var(--secondary);
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .controls {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 25px;
        }
        
        .control-group {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        
        label {
            font-weight: 500;
            color: var(--dark);
        }
        
        input, select, button {
            padding: 10px 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
            transition: all 0.3s;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: var(--secondary);
            box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.2);
        }
        
        button {
            background: var(--secondary);
            color: white;
            border: none;
            cursor: pointer;
            font-weight: 500;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        .results {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-top: 25px;
        }
        
        .chart-container {
            position: relative;
            height: 350px;
            background: white;
            padding: 15px;
            border-radius: 6px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }
        
        .data-table {
            max-height: 400px;
            overflow-y: auto;
            border: 1px solid #eee;
            border-radius: 6px;
            padding: 10px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
        }
        
        th, td {
            padding: 10px 12px;
            text-align: right;
            border-bottom: 1px solid #eee;
        }
        
        th {
            background: #f8f9fa;
            position: sticky;
            top: 0;
            font-weight: 600;
            color: var(--dark);
        }
        
        .math-display {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 6px;
            margin: 20px 0;
            font-family: 'Times New Roman', serif;
            border-left: 4px solid var(--accent);
        }
        
        .export-buttons {
            display: flex;
            gap: 12px;
            margin-top: 25px;
        }
        
        .angular-vis {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 25px;
            margin-top: 25px;
        }
        
        .unit-circle-container {
            text-align: center;
            padding: 15px;
            border: 1px solid #eee;
            border-radius: 6px;
            background: white;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
        }
        
        .unit-circle {
            border: 1px solid #ccc;
            border-radius: 50%;
            position: relative;
            width: 200px;
            height: 200px;
            margin: 0 auto 15px;
        }
        
        .current-results {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 6px;
            border: 1px solid #eee;
        }
        
        .result-item {
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
        }
        
        .result-label {
            font-weight: 500;
            color: var(--dark);
        }
        
        .result-value {
            font-family: 'Courier New', monospace;
            font-weight: 600;
        }
        
        .theorem {
            background: #e8f4fc;
            padding: 20px;
            border-radius: 6px;
            margin: 20px 0;
            border-left: 4px solid var(--secondary);
        }
        
        .theorem-title {
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        .proof-section {
            background: #f0f8ff;
            margin: 20px 0;
            padding: 25px;
            border-radius: 6px;
            border: 1px solid #b8d8e8;
        }
        
        .visualization-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin: 20px 0;
        }
        
        .loading {
            text-align: center;
            padding: 20px;
            color: var(--secondary);
        }
        
        .footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #7f8c8d;
            font-size: 14px;
        }
        
        /* Additional styles from the second file */
        .paper-container {
            max-width: 1200px !important;
            margin: 0 auto !important;
            background: #ffffff !important;
            padding: 50px !important;
            border-radius: 8px !important;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1) !important;
        }
        
        .section-title {
            font-size: 1.8em !important;
            color: #1565c0 !important;
            margin: 30px 0 20px 0 !important;
            padding-bottom: 10px !important;
            border-bottom: 3px solid #2196f3 !important;
            display: block !important;
        }
        
        .subsection-title {
            font-size: 1.3em !important;
            color: #1976d2 !important;
            margin: 20px 0 10px 0 !important;
            font-weight: 500 !important;
        }
        
        .section-number {
            display: inline-block !important;
            background: linear-gradient(135deg, #2196f3, #1976d2) !important;
            color: #ffffff !important;
            padding: 8px 16px !important;
            border-radius: 8px !important;
            font-weight: 700 !important;
            margin-right: 10px !important;
            box-shadow: 0 2px 8px rgba(33,150,243,0.3) !important;
        }
        
        .abstract {
            background: #e3f2fd !important;
            border-left: 4px solid #2196f3 !important;
            padding: 20px !important;
            margin: 30px 0 !important;
            border-radius: 4px !important;
            color: #212121 !important;
        }
        
        .table-of-contents {
            background: linear-gradient(135deg, #e3f2fd 0%, #f5f5f5 100%) !important;
            border: 2px solid #2196f3 !important;
            border-radius: 12px !important;
            padding: 30px !important;
            margin: 40px 0 !important;
            box-shadow: 0 4px 16px rgba(33, 150, 243, 0.2) !important;
        }
        
        .toc-grid {
            display: grid !important;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)) !important;
            gap: 15px !important;
            margin-top: 20px !important;
        }
        
        .toc-item {
            display: flex !important;
            align-items: center !important;
            background: #ffffff !important;
            padding: 15px 20px !important;
            border-radius: 8px !important;
            text-decoration: none !important;
            border-left: 4px solid #2196f3 !important;
            transition: all 0.3s ease !important;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08) !important;
        }
        
        .toc-item:hover {
            transform: translateX(5px) !important;
            box-shadow: 0 4px 16px rgba(33, 150, 243, 0.3) !important;
            border-left-color: #1565c0 !important;
            background: #f5f9ff !important;
        }
        
        .toc-number {
            display: inline-flex !important;
            align-items: center !important;
            justify-content: center !important;
            width: 35px !important;
            height: 35px !important;
            background: linear-gradient(135deg, #2196f3, #1976d2) !important;
            color: #ffffff !important;
            border-radius: 50% !important;
            font-weight: 700 !important;
            font-size: 1.1em !important;
            margin-right: 15px !important;
            flex-shrink: 0 !important;
        }
        
        .toc-title {
            color: #424242 !important;
            font-size: 1.05em !important;
            font-weight: 500 !important;
            line-height: 1.4 !important;
        }
        
        .quick-start-guide {
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%) !important;
            border: 3px solid #4caf50 !important;
            border-radius: 16px !important;
            padding: 40px !important;
            margin: 40px 0 !important;
            box-shadow: 0 8px 24px rgba(76, 175, 80, 0.2) !important;
        }
        
        .quick-start-card {
            background: #ffffff !important;
            padding: 25px !important;
            border-radius: 12px !important;
            border: 2px solid #4caf50 !important;
            text-align: center !important;
            transition: all 0.3s ease !important;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1) !important;
        }
        
        .quick-start-card:hover {
            transform: translateY(-5px) !important;
            box-shadow: 0 8px 24px rgba(76, 175, 80, 0.3) !important;
            border-color: #388e3c !important;
        }
        
        .quick-start-btn {
            display: inline-block !important;
            background: linear-gradient(135deg, #4caf50, #388e3c) !important;
            color: #ffffff !important;
            padding: 12px 24px !important;
            border-radius: 6px !important;
            text-decoration: none !important;
            font-weight: 600 !important;
            transition: all 0.3s ease !important;
        }
        
        .quick-start-btn:hover {
            background: linear-gradient(135deg, #388e3c, #2e7d32) !important;
            transform: scale(1.05) !important;
        }
        
        @media (max-width: 768px) {
            .controls, .results, .visualization-grid {
                grid-template-columns: 1fr;
            }
            
            .tab-buttons {
                flex-direction: column;
            }
            
            .paper-container {
                padding: 20px !important;
            }
            
            h1 {
                font-size: 1.8em !important;
            }
            
            h2, .section-title {
                font-size: 1.4em !important;
            }
            
            h3, .subsection-title {
                font-size: 1.2em !important;
            }
            
            .toc-grid {
                grid-template-columns: 1fr !important;
            }
            
            .quick-start-guide {
                padding: 20px !important;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Advanced Modular Mathematics Analyzer & Farey Channels</h1>
            <p>A comprehensive tool for exploring modular arithmetic, totient functions, number theory, and Farey channel analysis</p>
        </div>
        
        <div class="tab-container">
            <div class="tab-buttons">
                <button class="tab-button active" onclick="switchTab('density')">Coprime Density Analysis</button>
                <button class="tab-button" onclick="switchTab('evenness')">Modular Evenness Theorem</button>
                <button class="tab-button" onclick="switchTab('farey')">Farey Channels & Coprimality</button>
                <button class="tab-button" onclick="switchTab('mathematics')">Mathematical Background</button>
            </div>
            
            <!-- Tab 1: Coprime Density Analysis -->
            <div id="density-tab" class="tab-content active">
                <div class="theorem">
                    <div class="theorem-title">Mathematical Foundation: Coprime Density</div>
                    <p>This tool visualizes the convergence of the average coprime density across moduli up to \( M \):</p>
                    <p>\[ A(M) = \frac{1}{M} \sum_{m=1}^{M} \frac{\varphi(m)}{m} \]</p>
                    <p>where \( \varphi(m) \) is Euler's totient function, counting the numbers coprime to \( m \).</p>
                    <p>As \( M \to \infty \), this converges to the theoretical limit:</p>
                    <p>\[ \lim_{M \to \infty} A(M) = \frac{1}{\zeta(2)} = \frac{6}{\pi^2} \approx 0.607927 \]</p>
                    <p>This constant represents the probability that two randomly selected integers are coprime.</p>
                </div>
                
                <h2>Analysis Parameters</h2>
                <div class="controls">
                    <div class="control-group">
                        <label for="maxModulus">Maximum Modulus (M):</label>
                        <input type="number" id="maxModulus" value="1000" min="10" max="100000">
                        
                        <label for="stepSize">Step Size (for table display):</label>
                        <input type="number" id="stepSize" value="100" min="1" max="1000">
                        
                        <label for="updateFrequency">Update Frequency:</label>
                        <select id="updateFrequency">
                            <option value="10">Every 10 steps</option>
                            <option value="50">Every 50 steps</option>
                            <option value="100" selected>Every 100 steps</option>
                            <option value="1000">Every 1000 steps</option>
                        </select>
                    </div>
                    
                    <div class="control-group">
                        <label for="visualizationType">Visualization Type:</label>
                        <select id="visualizationType">
                            <option value="convergence">Convergence Plot</option>
                            <option value="error">Error Analysis</option>
                            <option value="local">Local Density</option>
                            <option value="primes">Prime Moduli Analysis</option>
                        </select>
                        
                        <label for="angularModuli">Angular Visualization Moduli (comma-separated):</label>
                        <input type="text" id="angularModuli" value="2,3,4,5,6,7,8">
                        
                        <button onclick="runDensityAnalysis()">Run Analysis</button>
                    </div>
                </div>

                <h2>Convergence Analysis</h2>
                <div class="chart-container">
                    <canvas id="convergenceChart"></canvas>
                </div>
                
                <div class="results">
                    <div>
                        <h3>Current Results</h3>
                        <div class="current-results" id="currentResults">
                            <p>Click "Run Analysis" to compute and display results.</p>
                        </div>
                    </div>
                    
                    <div>
                        <h3>Sample Data</h3>
                        <div class="data-table">
                            <table id="dataTable">
                                <thead>
                                    <tr>
                                        <th>Modulus M</th>
                                        <th>φ(M)</th>
                                        <th>φ(M)/M</th>
                                        <th>A(M)</th>
                                        <th>Error</th>
                                    </tr>
                                </thead>
                                <tbody id="tableBody">
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <div class="export-buttons">
                    <button onclick="exportCSV()">Export CSV</button>
                    <button onclick="exportPNG()">Export Chart as PNG</button>
                    <button onclick="exportText()">Export Full Analysis</button>
                </div>

                <div class="container">
                    <h2>Angular Distribution Visualization</h2>
                    <p>This visualization shows the distribution of coprime residues on the unit circle for different moduli. Each point represents a residue \( r \) where \( \gcd(r, m) = 1 \), positioned at angle \( \theta = \frac{2\pi r}{m} \).</p>
                    
                    <div id="angularVisualization" class="angular-vis">
                        <!-- Angular plots will be generated here -->
                    </div>
                </div>
            </div>
            
            <!-- Tab 2: Modular Evenness Theorem -->
            <div id="evenness-tab" class="tab-content">
                <div class="theorem">
                    <div class="theorem-title">Theorem: Law of Modular Evenness</div>
                    <p>For every integer \( n > 2 \), the Euler totient function \( \varphi(n) \) is even:</p>
                    <p style="text-align: center; font-size: 1.2em; margin: 15px 0;">
                        \( \varphi(n) \equiv 0 \pmod{2} \)
                    </p>
                    <p>The only exceptions occur at \( n = 1 \) and \( n = 2 \), where \( \varphi(n) = 1 \).</p>
                </div>

                <div class="proof-section">
                    <h2>Classical Proof (Group-Theoretic Perspective)</h2>
                    <p>Let \( U_n = (\mathbb{Z}/n\mathbb{Z})^{\times} \) be the multiplicative group of units modulo \( n \). Each element \( a \in U_n \) has a unique inverse \( a^{-1} \) with \( a a^{-1} \equiv 1 \pmod{n} \).</p>
                    
                    <ul>
                        <li>The group elements partition into inverse pairs \( \{a, a^{-1}\} \)</li>
                        <li>The only potential exceptions are <em>self-inverse</em> elements satisfying \( a^2 \equiv 1 \pmod{n} \)</li>
                        <li>For \( n > 2 \), the solutions to \( a^2 \equiv 1 \) always include \( 1 \) and \( -1 \), which are distinct modulo \( n \)</li>
                        <li>The full solution set forms pairs \( \{a, -a\} \), making the number of self-inverse elements <em>even</em></li>
                    </ul>
                    
                    <p>Since all elements are distributed among inverse pairs and an even number of fixed points, \( |U_n| = \varphi(n) \) must be even. <strong>∎</strong></p>
                </div>

                <div class="controls">
                    <h3>Explore Modular Evenness</h3>
                    <label for="modulus">Choose modulus n:</label>
                    <input type="number" id="modulus" min="3" max="50" value="8">
                    <button onclick="updateEvennessVisualization()">Update Visualization</button>
                </div>

                <div class="visualization-grid">
                    <div class="chart-container">
                        <h3>Unit Circle Visualization</h3>
                        <canvas id="unitCircle" width="400" height="400"></canvas>
                        <div id="circleInfo" style="text-align: center; margin-top: 10px;"></div>
                    </div>
                    
                    <div class="chart-container">
                        <h3>Totient Function Values</h3>
                        <canvas id="totientChart" width="400" height="400"></canvas>
                    </div>
                </div>

                <div class="proof-section">
                    <h2>Geometric Interpretation</h2>
                    <p>Define the modular union of all reduced fractions:</p>
                    <p style="text-align: center;">
                        \( U_{\infty} = \left\{ \frac{a}{n} \in \mathbb{Q} : 0 \leq \frac{a}{n} < 1,\ \gcd(a,n) = 1 \right\} \)
                    </p>
                    
                    <p>Under the exponential map:</p>
                    <p style="text-align: center;">
                        \( f\left(\frac{a}{n}\right) = e^{2\pi i \frac{a}{n}} \)
                    </p>
                    <p>each coprime fraction maps to a primitive \( n \)-th root of unity on the unit circle.</p>
                    
                    <h3>Key Observations:</h3>
                    <ul>
                        <li><strong>Inverse Symmetry:</strong> The modular inverse \( a^{-1} \) corresponds to complex conjugation</li>
                        <li><strong>Mirror Symmetry:</strong> The real axis acts as a mirror—every root above corresponds to one below</li>
                        <li><strong>Even Cardinality:</strong> For \( n > 2 \), primitive roots appear in symmetric pairs</li>
                        <li><strong>Global Structure:</strong> As \( n \to \infty \), these roots become dense while preserving reflection symmetry</li>
                    </ul>
                </div>

                <div class="chart-container">
                    <h3>Examples of the Phenomenon</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>\( n \)</th>
                                <th>\( \varphi(n) \)</th>
                                <th>Coprime Residues</th>
                                <th>Pairing Structure</th>
                            </tr>
                        </thead>
                        <tbody id="examplesTable">
                            <!-- Filled by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </div>
            
            <!-- Tab 3: Farey Channels & Coprimality -->
            <div id="farey-tab" class="tab-content">
                <div class="paper-container">
                    <header>
                        <h1>Nested Farey Channels & Fractional-Slice Coprimality Heuristic</h1>
                        <div class="author">Wessen Getachew</div>
                        <div class="date">October 2025</div>
                    </header>

                    <div class="abstract">
                        <strong>Abstract.</strong> We present a comprehensive framework for analyzing coprimality and prime detection through geometric representations on the unit circle. This work introduces the <em>Nested Farey Channel Framework</em>, which maps modular arithmetic structures to visual patterns, revealing deep connections between Euler's theorem, the Riemann zeta function, and prime distribution.
                        
                        <p style="margin-top: 15px;">The <em>Fractional-Slice Coprimality Heuristic</em> provides rapid probabilistic prime detection by sampling coprime residues within restricted circular arcs, achieving separation rates increasing from 32.7% to 92.3% across n ∈ [3, 10,000]. The complementary <em>Chord Length Uniformity Heuristic</em> offers an independent geometric signature based on inter-residue spacing patterns.</p>
                    </div>

                    <div class="table-of-contents">
                        <h2 style="text-align: center; color: #1565c0; margin-bottom: 20px;"> Table of Contents</h2>
                        <div class="toc-grid">
                            <a href="#section-1" class="toc-item">
                                <span class="toc-number">1</span>
                                <span class="toc-title">Euler's Theorem & RH Connection</span>
                            </a>
                            <a href="#section-2" class="toc-item">
                                <span class="toc-number">2</span>
                                <span class="toc-title">Nested Farey Channels Framework</span>
                            </a>
                            <a href="#section-3" class="toc-item">
                                <span class="toc-number">3</span>
                                <span class="toc-title">Fractional-Slice Coprimality Heuristic</span>
                            </a>
                            <a href="#section-4" class="toc-item">
                                <span class="toc-number">4</span>
                                <span class="toc-title">Interactive Algorithm Demonstration</span>
                            </a>
                        </div>
                    </div>

                    <div class="quick-start-guide">
                        <h2 style="text-align: center; color: #1565c0; margin-bottom: 20px; font-size: 1.8em;">
                             Quick Start Guide
                        </h2>
                        
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-top: 25px;">
                            <div class="quick-start-card">
                                <h3>New Here? Start Interactive</h3>
                                <p>Jump straight to the interactive demo and try different moduli values.</p>
                                <a href="#section-4" class="quick-start-btn">Try Interactive Demo →</a>
                            </div>
                            
                            <div class="quick-start-card">
                                <h3>Want Beautiful Visuals?</h3>
                                <p>Explore stunning 2D rings and 3D embeddings with multiple color schemes.</p>
                                <a href="#section-7" class="quick-start-btn">See Visualizations →</a>
                            </div>
                            
                            <div class="quick-start-card">
                                <h3>Understand the Theory</h3>
                                <p>Learn about Euler's theorem and the mathematical foundations.</p>
                                <a href="#section-1" class="quick-start-btn">Read Theory →</a>
                            </div>
                        </div>
                    </div>

                    <div class="section-title" id="section-1"><span class="section-number">1</span> Euler's Theorem and the Riemann Hypothesis Connection</div>

                    <p><strong>Motivation:</strong> Before exploring the nested Farey channels, we establish the foundational connection between Euler's theorem on modular symmetry and the Riemann Hypothesis. This section visualizes how local GCD=1 structures combine to form the global analytic symmetry of the Riemann zeta function.</p>

                    <div class="theorem">
                        <span class="label">Theorem 2.1 (Euler's Theorem and GCD=1 Set).</span>
                        For integers \(a, n \in \mathbb{Z}^{+}\) such that \(\gcd(a,n)=1\),
                        \[
                        a^{\varphi(n)} \equiv 1 \pmod{n},
                        \]
                        where \(\varphi(n)\) is Euler's totient function. The set \(\Phi(n) = \{ r : \gcd(r,n)=1 \}\) forms a multiplicative group with \(|\Phi(n)| = \varphi(n)\).
                    </div>

                    <div class="subsection-title">2.1 Unit Circle Embedding</div>

                    <p>Each GCD=1 residue \(r \in \Phi(n)\) maps to the unit circle via:</p>
                    <p style="text-align: center;">
                    \[
                    z_r = e^{2\pi i \frac{r}{n}}
                    \]
                    </p>
                    <p>This creates a symmetric ring of \(\varphi(n)\) visible lattice points, with Euler's orbit closing after exactly \(\varphi(n)\) rotations.</p>

                    <div class="subsection-title">2.2 Interactive Visualization: Euler Orbits and Prime Rings</div>

                    <div class="canvas-container">
                        <canvas id="eulerRiemannCanvas" width="900" height="900"></canvas>
                    </div>

                    <div class="controls" style="margin-top: 15px;">
                        <div style="display: flex; gap: 20px; flex-wrap: wrap; align-items: center;">
                            <div class="control-group">
                                <label for="erMaxModulus">Max Modulus:</label>
                                <input type="number" id="erMaxModulus" min="3" max="100" value="101" step="1" oninput="drawEulerRiemann()">
                            </div>
                            
                            <div class="control-group">
                                <label for="erShowPrimesOnly">
                                    <input type="checkbox" id="erShowPrimesOnly" onchange="drawEulerRiemann()">
                                    Show Primes Only
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label for="erShowOrbits">
                                    <input type="checkbox" id="erShowOrbits" checked onchange="drawEulerRiemann()">
                                    Show Euler Orbits
                                </label>
                            </div>
                            
                            <div class="control-group">
                                <label for="erOrbitModulus">Orbit for M:</label>
                                <input type="number" id="erOrbitModulus" min="2" max="30" value="101" step="1" oninput="drawEulerRiemann()">
                            </div>
                            
                            <div class="control-group">
                                <label for="erOrbitBase">Base a:</label>
                                <input type="number" id="erOrbitBase" min="2" max="20" value="3" step="1" oninput="drawEulerRiemann()">
                            </div>
                        </div>
                        
                        <div style="margin-top: 15px;">
                            <button onclick="drawEulerRiemann()">Redraw</button>
                            <button onclick="animateEulerOrbit()">Animate Orbit</button>
                            <button onclick="stopEulerAnimation()">Stop</button>
                        </div>
                    </div>

                    <div id="eulerRiemannStats" style="margin-top: 20px; padding: 15px; background: #f8f9fa; border-radius: 8px; font-size: 0.9em;"></div>

                    <div class="section-title" id="section-2">Part I: Nested Farey Channels Framework</div>

                    <div class="definition">
                        <span class="label">Definition 1.1 (Channel Rings).</span>
                        For a modulus \(m \in \mathbb{N}\), define the ring
                        \[
                        S_m = \left\{ e^{2\pi i r/m} : r = 0, 1, \dots, m-1 \right\}.
                        \]
                        Each element corresponds to a residue class \(r \pmod{m}\) visualized on the unit circle.
                    </div>

                    <div class="definition">
                        <span class="label">Definition 1.2 (Open and Blocked Channels).</span>
                        A channel \(C_{r,m}\) is said to be:
                        \[
                        C_{r,m} = 
                        \begin{cases}
                        \text{open}, & \text{if } \gcd(r,m)=1,\\
                        \text{blocked}, & \text{otherwise.}
                        \end{cases}
                        \]
                        The set of open channels has cardinality \(\varphi(m)\), Euler's totient function.
                    </div>

                    <div class="canvas-container">
                        <canvas id="channelCanvas" width="700" height="700"></canvas>
                        <div class="controls">
                            <div class="control-group">
                                <label for="modInput">Modulus:</label>
                                <input type="number" id="modInput" value="13" min="2" max="500">
                            </div>
                            <button onclick="drawChannelRing()">Visualize</button>
                        </div>
                        <div class="stats-display" id="channelStats" style="display: none;"></div>
                    </div>

                    <div class="section-title" id="section-3">Part II: Fractional-Slice Coprimality Heuristic</div>

                    <div class="subsection-title">2.1 Heuristic Definition</div>

                    <p>For any modulus \(m \ge 2\), define the <em>coprime density</em></p>
                    <p style="text-align: center;">
                    \[
                    \delta(m) = \frac{\varphi(m)}{m},
                    \]
                    </p>
                    <p>the fraction of residues mod \(m\) that are coprime to \(m\). For a prime \(p\), this equals \(\delta(p) = 1 - \frac{1}{p}\).</p>

                    <div class="definition">
                        <span class="label">Definition 2.1 (Fractional Slice).</span>
                        Let \(S(m) \subset \{1,2,\dots,m-1\}\) denote a chosen sampling region, such as the half-circle
                        \[
                        S_{\text{half}}(m) = \{1,\dots,\lfloor m/2\rfloor\}
                        \]
                        or a one-\(n\)th slice of residues distributed over \(2\pi/n\) radians. The slice captures a geometric subset of the modular ring. Define
                        \[
                        \delta_S(m) = \frac{|\,\{r \in S(m) : \gcd(r,m)=1\}\,|}{|S(m)|}
                        \]
                        as the local coprime density within that slice.
                    </div>

                    <div class="section-title" id="section-4">3. Interactive Algorithm Demonstration</div>

                    <div class="controls" style="margin-bottom: 20px;">
                        <div class="control-group">
                            <label for="testModulus">Test Modulus:</label>
                            <input type="number" id="testModulus" value="91" min="2" max="10000">
                        </div>
                        <div class="control-group">
                            <label for="sampleCount">Samples (k):</label>
                            <input type="number" id="sampleCount" value="5" min="1" max="50">
                        </div>
                        <div class="control-group">
                            <label for="sliceType">Slice Type:</label>
                            <select id="sliceType">
                                <option value="half">Half-Circle</option>
                                <option value="quarter">Quarter-Circle</option>
                                <option value="full">Full Circle</option>
                            </select>
                        </div>
                        <button class="success" onclick="runFractionalTest()">Run Test</button>
                    </div>

                    <canvas id="testCanvas" width="600" height="600" style="display: block; margin: 20px auto;"></canvas>
                    
                    <div id="testResult"></div>

                    <div class="section-title">Conclusion</div>

                    <p>Fractional-slice coprimality sampling provides a geometric and probabilistic bridge between Nested Farey Channel theory and practical number testing. It captures the essential property that prime moduli maintain maximal channel openness even when viewed through restricted arcs of the unit circle, while composites introduce blocked Farey channels visible through partial sampling.</p>

                    <p>This heuristic can serve both as:</p>
                    <ol>
                        <li>A fast preliminary screen for prime candidates within modular sieves.</li>
                        <li>A geometric diagnostic tool for visualizing the distribution of coprime residues across modular arcs.</li>
                    </ol>
                </div>
            </div>
            
            <!-- Tab 4: Mathematical Background -->
            <div id="mathematics-tab" class="tab-content">
                <h2>Mathematical Background</h2>
                
                <h3>Euler's Totient Function</h3>
                <p>Euler's totient function \( \varphi(n) \) counts the positive integers up to \( n \) that are relatively prime to \( n \). For example:</p>
                <ul>
                    <li>\( \varphi(1) = 1 \)</li>
                    <li>\( \varphi(6) = 2 \) (numbers 1 and 5 are coprime to 6)</li>
                    <li>\( \varphi(p) = p-1 \) for prime \( p \)</li>
                </ul>
                
                <h3>Modular Angular Representation</h3>
                <p>For modulus \( m \), each residue \( r \) can be represented as a point on the unit circle:</p>
                <p>\[ z_{r,m} = e^{2\pi i r/m} = \cos\left(\frac{2\pi r}{m}\right) + i\sin\left(\frac{2\pi r}{m}\right) \]</p>
                <p>The reduced residue system consists of those \( r \) where \( \gcd(r, m) = 1 \), forming the coprime angular constellation.</p>
                
                <h3>Connection to the Riemann Zeta Function</h3>
                <p>The limit \( \frac{6}{\pi^2} \) arises from the Euler product formula for the Riemann zeta function:</p>
                <p>\[ \zeta(s) = \prod_{p \text{ prime}} \frac{1}{1 - p^{-s}} \]</p>
                <p>Specifically, \( \zeta(2) = \frac{\pi^2}{6} \), so the reciprocal gives the coprime density.</p>
                
                <h3>Applications and Significance</h3>
                <p>The study of coprime density and modular symmetry has applications in:</p>
                <ul>
                    <li>Number theory and analytic number theory</li>
                    <li>Cryptography and security algorithms</li>
                    <li>Probability theory and random number generation</li>
                    <li>Signal processing and Fourier analysis</li>
                    <li>Quantum computing and algorithm design</li>
                </ul>
            </div>
        </div>
    </div>

    <div class="footer">
        <p>Advanced Modular Mathematics Analyzer | Mathematical Visualization Tool</p>
    </div>

    <script>
        // ==================== TAB MANAGEMENT ====================
        function switchTab(tabName) {
            // Hide all tabs
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
            });
            
            // Show selected tab
            document.getElementById(tabName + '-tab').classList.add('active');
            
            // Activate selected button
            event.target.classList.add('active');
        }

        // ==================== DENSITY ANALYSIS FUNCTIONS ====================
        
        // Euler's totient function implementation
        function totient(n) {
            if (n < 1) return 0;
            let result = n;
            let p = 2;
            
            while (p * p <= n) {
                if (n % p === 0) {
                    while (n % p === 0) {
                        n = Math.floor(n / p);
                    }
                    result -= Math.floor(result / p);
                }
                p++;
            }
            
            if (n > 1) {
                result -= Math.floor(result / n);
            }
            return result;
        }

        // Check if a number is prime
        function isPrime(num) {
            if (num <= 1) return false;
            if (num <= 3) return true;
            if (num % 2 === 0 || num % 3 === 0) return false;
            
            for (let i = 5; i * i <= num; i += 6) {
                if (num % i === 0 || num % (i + 2) === 0) return false;
            }
            return true;
        }

        // GCD function using Euclidean algorithm
        function gcd(a, b) {
            return b === 0 ? a : gcd(b, a % b);
        }

        let currentChart = null;
        let analysisData = [];

        function runDensityAnalysis() {
            const M_max = parseInt(document.getElementById('maxModulus').value);
            const stepSize = parseInt(document.getElementById('stepSize').value);
            const updateFreq = parseInt(document.getElementById('updateFrequency').value);
            
            // Clear previous data
            analysisData = [];
            updateTable([]);
            
            // Show loading state
            const resultsDiv = document.getElementById('currentResults');
            resultsDiv.innerHTML = '<div class="loading">Computing... Please wait</div>';
            
            // Theoretical constant
            const target = 6 / (Math.PI ** 2);
            let runningSum = 0;
            let primeDensitySum = 0;
            let primeCount = 0;
            
            const results = [];
            
            // Use setTimeout to allow UI updates during computation
            setTimeout(() => {
                for (let m = 1; m <= M_max; m++) {
                    const phi_m = totient(m);
                    const rho_m = phi_m / m;
                    runningSum += rho_m;
                    const A_M = runningSum / m;
                    const error = Math.abs(A_M - target);
                    
                    // Prime analysis
                    let primeDensity = null;
                    if (isPrime(m) && m > 1) {
                        primeDensitySum += rho_m;
                        primeCount++;
                        primeDensity = primeDensitySum / primeCount;
                    }
                    
                    const result = {
                        m: m,
                        phi_m: phi_m,
                        rho_m: rho_m,
                        running_sum: runningSum,
                        A_M: A_M,
                        error: error,
                        is_prime: isPrime(m),
                        prime_density: primeDensity
                    };
                    
                    results.push(result);
                    
                    // Update display periodically
                    if (m % updateFreq === 0 || m === M_max) {
                        analysisData = [...results];
                        updateDisplay(result, target);
                        updateChart(results);
                        updateTable(results.filter((_, idx) => idx % stepSize === 0));
                    }
                }
                
                // Generate angular visualization
                generateAngularVisualization();
            }, 10);
        }

        function updateDisplay(currentResult, target) {
            const resultsDiv = document.getElementById('currentResults');
            resultsDiv.innerHTML = `
                <div class="result-item">
                    <span class="result-label">Current Modulus:</span>
                    <span class="result-value">${currentResult.m.toLocaleString()}</span>
                </div>
                <div class="result-item">
                    <span class="result-label">Current A(M):</span>
                    <span class="result-value">${currentResult.A_M.toFixed(8)}</span>
                </div>
                <div class="result-item">
                    <span class="result-label">Theoretical Limit:</span>
                    <span class="result-value">${target.toFixed(8)}</span>
                </div>
                <div class="result-item">
                    <span class="result-label">Current Error:</span>
                    <span class="result-value">${currentResult.error.toExponential(3)}</span>
                </div>
                <div class="result-item">
                    <span class="result-label">Convergence:</span>
                    <span class="result-value">${((1 - currentResult.error/target) * 100).toFixed(2)}%</span>
                </div>
            `;
        }

        function updateChart(results) {
            const ctx = document.getElementById('convergenceChart').getContext('2d');
            const target = 6 / (Math.PI ** 2);
            
            if (currentChart) {
                currentChart.destroy();
            }
            
            const visualizationType = document.getElementById('visualizationType').value;
            let datasets = [];
            let yAxisLabel = 'Density';
            
            switch (visualizationType) {
                case 'convergence':
                    datasets = [
                        {
                            label: 'A(M) - Average Density',
                            data: results.map(r => r.A_M),
                            borderColor: 'rgb(52, 152, 219)',
                            backgroundColor: 'rgba(52, 152, 219, 0.1)',
                            borderWidth: 2,
                            fill: false
                        },
                        {
                            label: '6/π² Theoretical Limit',
                            data: results.map(() => target),
                            borderColor: 'rgb(231, 76, 60)',
                            borderDash: [5, 5],
                            borderWidth: 2,
                            fill: false
                        }
                    ];
                    yAxisLabel = 'Density';
                    break;
                    
                case 'error':
                    datasets = [{
                        label: 'Error |A(M) - 6/π²|',
                        data: results.map(r => r.error),
                        borderColor: 'rgb(46, 204, 113)',
                        backgroundColor: 'rgba(46, 204, 113, 0.1)',
                        borderWidth: 2,
                        fill: true
                    }];
                    yAxisLabel = 'Absolute Error';
                    break;
                    
                case 'local':
                    datasets = [{
                        label: 'Local Density φ(m)/m',
                        data: results.map(r => r.rho_m),
                        borderColor: 'rgb(155, 89, 182)',
                        backgroundColor: 'rgba(155, 89, 182, 0.1)',
                        borderWidth: 1,
                        fill: true
                    }];
                    yAxisLabel = 'Local Density';
                    break;
                    
                case 'primes':
                    const primeData = results.filter(r => r.is_prime && r.m > 1);
                    datasets = [{
                        label: 'Prime Moduli Density φ(p)/p = 1 - 1/p',
                        data: primeData.map(r => r.rho_m),
                        borderColor: 'rgb(230, 126, 34)',
                        backgroundColor: 'rgba(230, 126, 34, 0.1)',
                        borderWidth: 2,
                        fill: false,
                        pointRadius: 3
                    }];
                    yAxisLabel = 'Prime Density';
                    break;
            }
            
            currentChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: results.map(r => r.m),
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: 'Modulus M'
                            },
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        },
                        y: {
                            title: {
                                display: true,
                                text: yAxisLabel
                            },
                            grid: {
                                color: 'rgba(0, 0, 0, 0.05)'
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false
                        }
                    },
                    animation: {
                        duration: 0
                    }
                }
            });
        }

        function updateTable(results) {
            const tableBody = document.getElementById('tableBody');
            const stepSize = parseInt(document.getElementById('stepSize').value);
            
            let html = '';
            const displayResults = results.filter((_, idx) => idx % stepSize === 0);
            
            if (displayResults.length === 0) {
                html = '<tr><td colspan="5" style="text-align: center;">No data to display</td></tr>';
            } else {
                displayResults.forEach(result => {
                    html += `
                        <tr>
                            <td>${result.m}</td>
                            <td>${result.phi_m}</td>
                            <td>${result.rho_m.toFixed(6)}</td>
                            <td>${result.A_M.toFixed(6)}</td>
                            <td>${result.error.toExponential(3)}</td>
                        </tr>
                    `;
                });
            }
            
            tableBody.innerHTML = html;
        }

        function generateAngularVisualization() {
            const moduliInput = document.getElementById('angularModuli').value;
            const moduli = moduliInput.split(',').map(m => parseInt(m.trim())).filter(m => m > 0);
            const container = document.getElementById('angularVisualization');
            
            container.innerHTML = '';
            
            moduli.forEach(m => {
                const div = document.createElement('div');
                div.className = 'unit-circle-container';
                
                const title = document.createElement('div');
                title.innerHTML = `<strong>Modulus ${m}</strong><br>φ(${m}) = ${totient(m)}`;
                
                const canvas = document.createElement('canvas');
                canvas.width = 200;
                canvas.height = 200;
                canvas.style.display = 'block';
                canvas.style.margin = '10px auto';
                
                div.appendChild(title);
                div.appendChild(canvas);
                container.appendChild(div);
                
                drawUnitCircle(canvas, m);
            });
        }

        function drawUnitCircle(canvas, modulus) {
            const ctx = canvas.getContext('2d');
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const radius = 80;
            
            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // Draw unit circle
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.strokeStyle = '#bdc3c7';
            ctx.lineWidth = 1;
            ctx.stroke();
            
            // Draw center point
            ctx.beginPath();
            ctx.arc(centerX, centerY, 2, 0, 2 * Math.PI);
            ctx.fillStyle = '#7f8c8d';
            ctx.fill();
            
            // Draw coprime points
            for (let r = 0; r < modulus; r++) {
                if (gcd(r, modulus) === 1) {
                    const angle = (2 * Math.PI * r) / modulus;
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    ctx.beginPath();
                    ctx.arc(x, y, 4, 0, 2 * Math.PI);
                    ctx.fillStyle = '#3498db';
                    ctx.fill();
                    
                    // Label some points for smaller moduli
                    if (modulus <= 8 && (r === 1 || r === modulus - 1)) {
                        ctx.fillStyle = '#2c3e50';
                        ctx.font = '10px Arial';
                        ctx.textAlign = 'center';
                        ctx.fillText(`${r}/${modulus}`, x, y - 8);
                    }
                }
            }
        }

        // Export functions
        function exportCSV() {
            if (analysisData.length === 0) {
                alert('No data to export. Please run analysis first.');
                return;
            }
            
            const csv = PapaParse.unparse(analysisData);
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            
            link.setAttribute('href', url);
            link.setAttribute('download', `modular_density_${analysisData.length}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function exportPNG() {
            if (!currentChart) {
                alert('No chart to export. Please run analysis first.');
                return;
            }
            
            const link = document.createElement('a');
            link.download = 'modular_density_chart.png';
            link.href = document.getElementById('convergenceChart').toDataURL();
            link.click();
        }

        function exportText() {
            if (analysisData.length === 0) {
                alert('No data to export. Please run analysis first.');
                return;
            }
            
            const target = 6 / (Math.PI ** 2);
            const finalResult = analysisData[analysisData.length - 1];
            
            let text = `MODULAR COPRIME DENSITY ANALYSIS\n`;
            text += `Generated: ${new Date().toLocaleString()}\n`;
            text += `Maximum Modulus: ${finalResult.m}\n`;
            text += `Theoretical Limit: 6/π² = ${target.toFixed(10)}\n`;
            text += `Final A(M): ${finalResult.A_M.toFixed(8)}\n`;
            text += `Final Error: ${finalResult.error.toExponential(3)}\n`;
            text += `Convergence: ${((1 - finalResult.error/target) * 100).toFixed(2)}%\n\n`;
            
            text += `SAMPLE DATA (every ${document.getElementById('stepSize').value} steps):\n`;
            text += 'M,phi(M),phi(M)/M,A(M),Error\n';
            
            const stepSize = parseInt(document.getElementById('stepSize').value);
            analysisData.filter((_, idx) => idx % stepSize === 0).forEach(result => {
                text += `${result.m},${result.phi_m},${result.rho_m.toFixed(6)},${result.A_M.toFixed(6)},${result.error.toExponential(3)}\n`;
            });
            
            const blob = new Blob([text], { type: 'text/plain;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            
            link.setAttribute('href', url);
            link.setAttribute('download', `modular_density_analysis.txt`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        // ==================== MODULAR EVENNESS FUNCTIONS ====================
        
        let unitCircleChart, totientChart;
        
        function initializeEvennessCharts() {
            // Unit Circle Chart
            const unitCtx = document.getElementById('unitCircle').getContext('2d');
            unitCircleChart = new Chart(unitCtx, {
                type: 'scatter',
                data: {
                    datasets: [
                        {
                            label: 'Primitive Roots',
                            data: [],
                            backgroundColor: 'blue',
                            pointRadius: 6
                        },
                        {
                            label: 'Inverse Pairs',
                            data: [],
                            backgroundColor: 'red',
                            pointRadius: 6
                        }
                    ]
                },
                options: {
                    responsive: false,
                    scales: {
                        x: {
                            min: -1.2,
                            max: 1.2,
                            grid: {
                                color: '#f0f0f0'
                            }
                        },
                        y: {
                            min: -1.2,
                            max: 1.2,
                            grid: {
                                color: '#f0f0f0'
                            }
                        }
                    },
                    plugins: {
                        title: {
                            display: true,
                            text: 'Complex Roots of Unity'
                        }
                    }
                }
            });

            // Totient Function Chart
            const totientCtx = document.getElementById('totientChart').getContext('2d');
            totientChart = new Chart(totientCtx, {
                type: 'bar',
                data: {
                    labels: [],
                    datasets: [{
                        label: 'φ(n)',
                        data: [],
                        backgroundColor: 'rgba(52, 152, 219, 0.7)',
                        borderColor: 'rgba(52, 152, 219, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: 'φ(n)'
                            }
                        },
                        x: {
                            title: {
                                display: true,
                                text: 'n'
                            }
                        }
                    }
                }
            });

            updateEvennessVisualization();
            updateExamplesTable();
        }

        function modInverse(a, n) {
            for (let x = 1; x < n; x++) {
                if ((a * x) % n === 1) return x;
            }
            return 1;
        }

        function updateEvennessVisualization() {
            const n = parseInt(document.getElementById('modulus').value);
            if (n < 3) {
                alert('Please choose n ≥ 3');
                return;
            }

            // Update unit circle
            const primitiveRoots = [];
            const inversePairs = [];
            
            for (let a = 1; a < n; a++) {
                if (gcd(a, n) === 1) {
                    const angle = (2 * Math.PI * a) / n;
                    const x = Math.cos(angle);
                    const y = Math.sin(angle);
                    
                    const inverse = modInverse(a, n);
                    if (a === inverse || a === n - inverse) {
                        // Self-inverse (on real axis)
                        primitiveRoots.push({x, y});
                    } else if (a < inverse) {
                        // Regular pair
                        primitiveRoots.push({x, y});
                        const invAngle = (2 * Math.PI * inverse) / n;
                        inversePairs.push({
                            x: Math.cos(invAngle),
                            y: Math.sin(invAngle)
                        });
                    }
                }
            }

            unitCircleChart.data.datasets[0].data = primitiveRoots;
            unitCircleChart.data.datasets[1].data = inversePairs;
            unitCircleChart.update();

            // Update totient chart
            const labels = [];
            const data = [];
            for (let i = 3; i <= Math.min(n + 5, 20); i++) {
                labels.push(i);
                data.push(totient(i));
            }
            totientChart.data.labels = labels;
            totientChart.data.datasets[0].data = data;
            totientChart.update();

            // Update circle info
            document.getElementById('circleInfo').innerHTML = 
                `n = ${n}, φ(${n}) = ${totient(n)} (${totient(n) % 2 === 0 ? 'even' : 'odd'})`;
        }

        function updateExamplesTable() {
            const examples = [
                {n: 3, totient: 2, residues: '{1, 2}', pairing: '2 ↔ 2 (self-inverse)'},
                {n: 4, totient: 2, residues: '{1, 3}', pairing: '3 ↔ 3 (self-inverse)'},
                {n: 5, totient: 4, residues: '{1, 2, 3, 4}', pairing: '2 ↔ 3, 4 ↔ 4'},
                {n: 6, totient: 2, residues: '{1, 5}', pairing: '5 ↔ 5 (self-inverse)'},
                {n: 7, totient: 6, residues: '{1, 2, 3, 4, 5, 6}', pairing: '2 ↔ 4, 3 ↔ 5, 6 ↔ 6'},
                {n: 8, totient: 4, residues: '{1, 3, 5, 7}', pairing: '3 ↔ 3, 5 ↔ 5, 7 ↔ 7'}
            ];

            const tableBody = document.getElementById('examplesTable');
            tableBody.innerHTML = examples.map(ex => `
                <tr>
                    <td>${ex.n}</td>
                    <td>${ex.totient}</td>
                    <td>${ex.residues}</td>
                    <td>${ex.pairing}</td>
                </tr>
            `).join('');
        }

        // ==================== FAREY CHANNELS FUNCTIONS ====================
        
        let showChannelLabels = false;

        function drawChannelRing() {
            const canvas = document.getElementById('channelCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = 280;

            const m = parseInt(document.getElementById('modInput').value);
            if (isNaN(m) || m < 2) return;

            // Define colors
            const gcd1Color = '#2ecc71';
            const gcdNotColor = '#e74c3c';

            ctx.clearRect(0, 0, width, height);

            // Draw circle
            ctx.strokeStyle = '#34495e';
            ctx.lineWidth = 2.5;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.stroke();

            // Draw origin
            ctx.fillStyle = gcdNotColor;
            ctx.beginPath();
            ctx.arc(centerX + radius, centerY, 10, 0, 2 * Math.PI);
            ctx.fill();

            // Draw channels
            const phi = totient(m);
            let openCount = 0, blockedCount = 0;

            for (let r = 1; r < m; r++) {
                const isOpen = gcd(r, m) === 1;
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);

                if (isOpen) openCount++;
                else blockedCount++;

                // Draw line
                ctx.strokeStyle = isOpen ? 'rgba(39, 174, 96, 0.3)' : 'rgba(231, 76, 60, 0.3)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(x, y);
                ctx.stroke();

                // Draw point
                ctx.fillStyle = isOpen ? '#27ae60' : '#e74c3c';
                ctx.beginPath();
                ctx.arc(x, y, isOpen ? 6 : 5, 0, 2 * Math.PI);
                ctx.fill();

                if (showChannelLabels) {
                    ctx.fillStyle = '#2c3e50';
                    ctx.font = '11px serif';
                    const labelX = centerX + (radius + 30) * Math.cos(theta);
                    const labelY = centerY - (radius + 30) * Math.sin(theta);
                    ctx.fillText(`${r}`, labelX - 5, labelY + 4);
                }
            }

            // Display stats
            const statsDiv = document.getElementById('channelStats');
            statsDiv.innerHTML = `
                <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m}</span></div>
                <div class="stat-row"><span class="stat-label">Open Channels:</span><span class="stat-value">${openCount}</span></div>
                <div class="stat-row"><span class="stat-label">Blocked Channels:</span><span class="stat-value">${blockedCount}</span></div>
                <div class="stat-row"><span class="stat-label">Density δ(m):</span><span class="stat-value">${(openCount/m).toFixed(4)}</span></div>
                <div class="stat-row"><span class="stat-label">Is Prime:</span><span class="stat-value">${isPrime(m) ? 'Yes ✓' : 'No'}</span></div>
            `;
            statsDiv.style.display = 'block';
        }

        function getSlice(m, sliceType) {
            if (sliceType === 'half') {
                return Array.from({length: Math.floor(m/2)}, (_, i) => i + 1);
            } else if (sliceType === 'quarter') {
                return Array.from({length: Math.floor(m/4)}, (_, i) => i + 1);
            } else {
                return Array.from({length: m-1}, (_, i) => i + 1);
            }
        }

        function runFractionalTest() {
            const m = parseInt(document.getElementById('testModulus').value);
            const k = parseInt(document.getElementById('sampleCount').value);
            const sliceType = document.getElementById('sliceType').value;

            if (isNaN(m) || m < 2 || isNaN(k) || k < 1) return;

            const canvas = document.getElementById('testCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            const radius = 220;

            ctx.clearRect(0, 0, width, height);

            // Draw circle
            ctx.strokeStyle = '#34495e';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.stroke();

            // Get slice
            const slice = getSlice(m, sliceType);
            
            // Highlight slice region
            if (sliceType !== 'full') {
                ctx.fillStyle = 'rgba(102, 126, 234, 0.1)';
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                const maxTheta = (2 * Math.PI * slice[slice.length-1]) / m;
                ctx.arc(centerX, centerY, radius, -Math.PI/2, -Math.PI/2 + maxTheta);
                ctx.closePath();
                ctx.fill();
            }

            // Sample and test
            const samples = [];
            let allPass = true;

            for (let i = 0; i < k; i++) {
                const r = slice[Math.floor(Math.random() * slice.length)];
                const coprime = gcd(r, m) === 1;
                samples.push({r, coprime});
                if (!coprime) allPass = false;
            }

            // Draw all residues faintly
            for (let r = 1; r < m; r++) {
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);
                
                ctx.fillStyle = '#ddd';
                ctx.beginPath();
                ctx.arc(x, y, 3, 0, 2 * Math.PI);
                ctx.fill();
            }

            // Draw sampled residues
            samples.forEach(({r, coprime}) => {
                const theta = (2 * Math.PI * r) / m;
                const x = centerX + radius * Math.cos(theta);
                const y = centerY - radius * Math.sin(theta);

                // Draw ray
                ctx.strokeStyle = coprime ? 'rgba(39, 174, 96, 0.6)' : 'rgba(231, 76, 60, 0.6)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(x, y);
                ctx.stroke();

                // Draw point
                ctx.fillStyle = coprime ? '#27ae60' : '#e74c3c';
                ctx.beginPath();
                ctx.arc(x, y, 8, 0, 2 * Math.PI);
                ctx.fill();

                // Label
                ctx.fillStyle = '#2c3e50';
                ctx.font = 'bold 12px serif';
                const labelX = centerX + (radius + 25) * Math.cos(theta);
                const labelY = centerY - (radius + 25) * Math.sin(theta);
                ctx.fillText(`${r}`, labelX - 8, labelY + 4);
            });

            // Display result
            const resultDiv = document.getElementById('testResult');
            const prime = isPrime(m);
            const q = smallestPrimeFactor(m);
            const theoreticalProb = Math.pow(1 - 1/q, k).toFixed(4);

            resultDiv.innerHTML = `
                <div class="test-result ${allPass ? 'pass' : 'fail'}">
                    <strong>Result:</strong> ${allPass ? 'PASS ✓' : 'FAIL ✗'} - ${m} ${allPass ? 'is a prime candidate' : 'is composite (detected)'}
                </div>
                <div class="stats-display" style="margin-top: 15px;">
                    <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m}</span></div>
                    <div class="stat-row"><span class="stat-label">Actual Status:</span><span class="stat-value">${prime ? 'Prime' : 'Composite'}</span></div>
                    <div class="stat-row"><span class="stat-label">Samples Tested:</span><span class="stat-value">${k}</span></div>
                    <div class="stat-row"><span class="stat-label">Passed Samples:</span><span class="stat-value">${samples.filter(s => s.coprime).length}/${k}</span></div>
                    <div class="stat-row"><span class="stat-label">Smallest Factor:</span><span class="stat-value">${q}</span></div>
                    <div class="stat-row"><span class="stat-label">Theoretical Pass Prob:</span><span class="stat-value">${theoreticalProb}</span></div>
                </div>
            `;
        }

        function smallestPrimeFactor(n) {
            if (n % 2 === 0) return 2;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return i;
            }
            return n;
        }

        // ==================== EULER-RIEMANN VISUALIZATION ====================
        
        let eulerAnimationId = null;
        let eulerOrbitStep = 0;

        function eulerTotient(n) {
            let count = 0;
            for (let r = 1; r < n; r++) {
                if (gcd(r, n) === 1) count++;
            }
            return count;
        }

        function drawEulerRiemann() {
            const canvas = document.getElementById('eulerRiemannCanvas');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;
            
            const maxM = parseInt(document.getElementById('erMaxModulus').value) || 101;
            const showPrimesOnly = document.getElementById('erShowPrimesOnly').checked;
            const showOrbits = document.getElementById('erShowOrbits').checked;
            const orbitM = parseInt(document.getElementById('erOrbitModulus').value) || 101;
            const orbitBase = parseInt(document.getElementById('erOrbitBase').value) || 3;
            
            // Use black background by default
            const blackBg = true;
            const bgColor = '#000000';
            ctx.fillStyle = blackBg ? bgColor : '#ffffff';
            ctx.fillRect(0, 0, width, height);
            
            const maxRadius = Math.min(width, height) * 0.42;
            const moduli = [];
            for (let m = 2; m <= maxM; m++) {
                if (!showPrimesOnly || isPrime(m)) moduli.push(m);
            }
            
            let primeCount = 0;
            let totalGCD1 = 0;
            
            moduli.forEach((m, idx) => {
                const radius = (idx + 1) * (maxRadius / moduli.length);
                const isPrimeM = isPrime(m);
                if (isPrimeM) primeCount++;
                
                ctx.strokeStyle = isPrimeM ? 'rgba(100, 200, 255, 0.3)' : 'rgba(150, 150, 150, 0.15)';
                ctx.lineWidth = isPrimeM ? 1.5 : 0.5;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
                ctx.stroke();
                
                const phi = eulerTotient(m);
                totalGCD1 += phi;
                
                for (let r = 0; r < m; r++) {
                    if (gcd(r, m) === 1) {
                        const angle = (2 * Math.PI * r) / m - Math.PI / 2;
                        const x = centerX + radius * Math.cos(angle);
                        const y = centerY + radius * Math.sin(angle);
                        
                        // Color based on scheme
                        let pointColor;
                        pointColor = isPrimeM ? '#4ecdc4' : '#95a5a6';
                        
                        ctx.fillStyle = pointColor;
                        ctx.beginPath();
                        ctx.arc(x, y, isPrimeM ? 3 : 2, 0, 2 * Math.PI);
                        ctx.fill();
                    }
                }
            });
            
            if (showOrbits && moduli.includes(orbitM) && gcd(orbitBase, orbitM) === 1) {
                const mIdx = moduli.indexOf(orbitM);
                const radius = (mIdx + 1) * (maxRadius / moduli.length);
                const phi = eulerTotient(orbitM);
                
                let current = 1;
                const orbitPoints = [];
                
                for (let k = 0; k < phi; k++) {
                    const angle = (2 * Math.PI * current) / orbitM - Math.PI / 2;
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    orbitPoints.push({ x, y });
                    current = (current * orbitBase) % orbitM;
                }
                
                // Show connections
                ctx.strokeStyle = 'rgba(255, 200, 0, 0.6)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                orbitPoints.forEach((p, i) => {
                    if (i === 0) ctx.moveTo(p.x, p.y);
                    else ctx.lineTo(p.x, p.y);
                });
                ctx.closePath();
                ctx.stroke();
                
                orbitPoints.forEach((p, i) => {
                    ctx.fillStyle = i === 0 ? '#ff3860' : '#ffdd57';
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, 4, 0, 2 * Math.PI);
                    ctx.fill();
                });
            }
            
            ctx.fillStyle = '#ecf0f1';
            ctx.font = 'bold 20px Arial';
            ctx.textAlign = 'center';
            ctx.fillText('Euler Orbits & Prime Rings: GCD=1 Structure', centerX, 30);
            
            const statsDiv = document.getElementById('eulerRiemannStats');
            if (statsDiv) {
                const avgPhi = moduli.length > 0 ? (totalGCD1 / moduli.length).toFixed(1) : 0;
                statsDiv.innerHTML = `
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                        <div><strong>Moduli shown:</strong> ${moduli.length}</div>
                        <div><strong>Prime rings:</strong> ${primeCount}</div>
                        <div><strong>Total GCD=1 points:</strong> ${totalGCD1}</div>
                        <div><strong>Avg φ(M):</strong> ${avgPhi}</div>
                        ${showOrbits ? `<div><strong>Orbit M=${orbitM}, a=${orbitBase}:</strong> φ(${orbitM})=${eulerTotient(orbitM)} steps</div>` : ''}
                    </div>
                `;
            }
        }

        function animateEulerOrbit() {
            stopEulerAnimation();
            eulerOrbitStep = 0;
            
            const orbitM = parseInt(document.getElementById('erOrbitModulus').value) || 7;
            const orbitBase = parseInt(document.getElementById('erOrbitBase').value) || 3;
            
            if (gcd(orbitBase, orbitM) !== 1) {
                alert('Base a must be coprime to M!');
                return;
            }
            
            const phi = eulerTotient(orbitM);
            
            function animate() {
                drawEulerRiemann();
                
                const canvas = document.getElementById('eulerRiemannCanvas');
                const ctx = canvas.getContext('2d');
                const width = canvas.width;
                const height = canvas.height;
                const centerX = width / 2;
                const centerY = height / 2;
                
                const maxM = parseInt(document.getElementById('erMaxModulus').value) || 30;
                const showPrimesOnly = document.getElementById('erShowPrimesOnly').checked;
                
                const moduli = [];
                for (let m = 2; m <= maxM; m++) {
                    if (!showPrimesOnly || isPrime(m)) moduli.push(m);
                }
                
                if (!moduli.includes(orbitM)) return;
                
                const maxRadius = Math.min(width, height) * 0.42;
                const mIdx = moduli.indexOf(orbitM);
                const radius = (mIdx + 1) * (maxRadius / moduli.length);
                
                let current = 1;
                for (let k = 0; k < eulerOrbitStep; k++) {
                    current = (current * orbitBase) % orbitM;
                }
                
                const angle = (2 * Math.PI * current) / orbitM - Math.PI / 2;
                const x = centerX + radius * Math.cos(angle);
                const y = centerY + radius * Math.sin(angle);
                
                ctx.fillStyle = '#ff3860';
                ctx.beginPath();
                ctx.arc(x, y, 6, 0, 2 * Math.PI);
                ctx.fill();
                
                ctx.fillStyle = '#ffdd57';
                ctx.font = 'bold 14px Arial';
                ctx.textAlign = 'left';
                ctx.fillText(`Step ${eulerOrbitStep + 1}/${phi}: r=${current}`, 20, height - 20);
                
                eulerOrbitStep = (eulerOrbitStep + 1) % phi;
                eulerAnimationId = setTimeout(animate, 500);
            }
            
            animate();
        }

        function stopEulerAnimation() {
            if (eulerAnimationId) {
                clearTimeout(eulerAnimationId);
                eulerAnimationId = null;
            }
        }

        // ==================== INITIALIZATION ====================
        
        // Initialize when page loads
        document.addEventListener('DOMContentLoaded', function() {
            // Run initial density analysis with smaller dataset for quick load
            document.getElementById('maxModulus').value = '500';
            runDensityAnalysis();
            
            // Initialize evenness theorem charts
            initializeEvennessCharts();
            
            // Initialize channel visualization
            drawChannelRing();
            
            // Initialize Euler-Riemann visualization
            drawEulerRiemann();
        });
    </script>
</body>
</html>
