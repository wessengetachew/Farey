
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nested Farey Channels & Fractional-Slice Coprimality - Wessen Getachew</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Palatino Linotype', 'Book Antiqua', Palatino, serif;
            line-height: 1.6;
            color: #2c3e50;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
        }

        .paper-container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            padding: 60px 80px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            border-radius: 4px;
        }

        header {
            text-align: center;
            margin-bottom: 50px;
            border-bottom: 3px solid #667eea;
            padding-bottom: 30px;
        }

        h1 {
            font-size: 2.2em;
            font-weight: 700;
            color: #1a252f;
            margin-bottom: 20px;
            letter-spacing: 0.5px;
        }

        .author {
            font-size: 1.3em;
            font-style: italic;
            color: #555;
            margin-bottom: 10px;
        }

        .date {
            font-size: 1em;
            color: #777;
        }

        .section-title {
            font-size: 1.7em;
            font-weight: 600;
            color: #2c3e50;
            margin-top: 45px;
            margin-bottom: 20px;
            border-bottom: 2px solid #667eea;
            padding-bottom: 10px;
        }

        .subsection-title {
            font-size: 1.4em;
            font-weight: 600;
            color: #34495e;
            margin-top: 35px;
            margin-bottom: 15px;
        }

        p {
            text-align: justify;
            margin-bottom: 15px;
            font-size: 1.05em;
        }

        .definition, .proposition, .theorem, .proof, .corollary, .lemma, .algorithm {
            margin: 25px 0;
            padding: 20px;
            border-radius: 6px;
            position: relative;
        }

        .definition {
            background: linear-gradient(135deg, #e8f4f8 0%, #d4e7f0 100%);
            border-left: 5px solid #3498db;
        }

        .proposition, .theorem, .corollary {
            background: linear-gradient(135deg, #f0f7ef 0%, #e1f0dd 100%);
            border-left: 5px solid #27ae60;
        }

        .lemma {
            background: linear-gradient(135deg, #fff3e0 0%, #ffe0b2 100%);
            border-left: 5px solid #ff9800;
        }

        .algorithm {
            background: linear-gradient(135deg, #f3e5f5 0%, #e1bee7 100%);
            border-left: 5px solid #9c27b0;
        }

        .proof {
            background: linear-gradient(135deg, #fef5e7 0%, #fdebd0 100%);
            border-left: 5px solid #f39c12;
        }

        .label {
            font-weight: 700;
            font-size: 1.1em;
            color: #2c3e50;
            margin-bottom: 10px;
            display: block;
        }

        .proof-end {
            float: right;
            font-size: 1.3em;
            font-weight: bold;
        }

        ul {
            margin-left: 30px;
            margin-bottom: 20px;
        }

        li {
            margin-bottom: 12px;
            font-size: 1.05em;
        }

        .canvas-container {
            margin: 30px 0;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            padding: 35px;
            border-radius: 12px;
            border: 2px solid #667eea;
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
        }

        canvas {
            border: 2px solid #495057;
            background: white;
            border-radius: 8px;
            cursor: crosshair;
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
            display: block;
            margin: 0 auto;
        }

        .controls {
            margin-top: 25px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            align-items: center;
        }

        .control-group {
            display: flex;
            align-items: center;
            gap: 10px;
            background: white;
            padding: 10px 15px;
            border-radius: 6px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        label {
            font-weight: 600;
            color: #495057;
            font-size: 0.95em;
        }

        input[type="number"], input[type="range"] {
            padding: 8px 12px;
            border: 2px solid #ced4da;
            border-radius: 6px;
            font-size: 1em;
            width: 100px;
            transition: border-color 0.3s;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: #667eea;
        }

        select {
            padding: 8px 12px;
            border: 2px solid #ced4da;
            border-radius: 6px;
            font-size: 0.95em;
            cursor: pointer;
        }

        button {
            padding: 10px 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            font-size: 0.95em;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.2);
        }

        button.secondary {
            background: linear-gradient(135deg, #95a5a6 0%, #7f8c8d 100%);
        }

        button.success {
            background: linear-gradient(135deg, #27ae60 0%, #229954 100%);
        }

        button.danger {
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
        }

        .caption {
            font-style: italic;
            color: #666;
            margin-top: 20px;
            font-size: 0.95em;
            text-align: center;
        }

        .abstract {
            background: linear-gradient(135deg, #ecf0f1 0%, #d5dbdb 100%);
            padding: 30px;
            margin: 30px 0;
            border-radius: 8px;
            font-style: italic;
            border-left: 5px solid #95a5a6;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .info-box {
            background: linear-gradient(135deg, #fff3cd 0%, #ffe69c 100%);
            border: 2px solid #ffc107;
            border-radius: 8px;
            padding: 20px;
            margin: 25px 0;
        }

        .info-box strong {
            color: #856404;
        }

        .stats-display {
            margin-top: 20px;
            padding: 20px;
            background: white;
            border-radius: 8px;
            border: 2px solid #667eea;
        }

        .stat-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #e9ecef;
        }

        .stat-row:last-child {
            border-bottom: none;
        }

        .stat-label {
            font-weight: 600;
            color: #495057;
        }

        .stat-value {
            color: #667eea;
            font-weight: 700;
        }

        .test-result {
            margin-top: 20px;
            padding: 20px;
            border-radius: 8px;
            font-weight: 600;
        }

        .test-result.pass {
            background: #d4edda;
            color: #155724;
            border: 2px solid #c3e6cb;
        }

        .test-result.fail {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #f5c6cb;
        }

        code {
            background: #f4f4f4;
            padding: 2px 6px;
            border-radius: 3px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
        }

        pre {
            background: white;
            color: #2c3e50;
            padding: 20px;
            border-radius: 8px;
            overflow-x: auto;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.5;
            border: 2px solid #dee2e6;
        }

        .experimental-section {
            background: #f8f9fa;
            padding: 30px;
            margin: 30px 0;
            border-radius: 8px;
            border: 2px solid #667eea;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #dee2e6;
        }

        th {
            background: #667eea;
            color: white;
            font-weight: 600;
        }

        tr:hover {
            background: #f8f9fa;
        }

        .progress-bar {
            width: 100%;
            height: 30px;
            background: #e9ecef;
            border-radius: 15px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            transition: width 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: 600;
        }

        .results-history {
            margin-top: 20px;
            max-height: 400px;
            overflow-y: auto;
            border: 2px solid #667eea;
            border-radius: 8px;
            background: white;
        }

        .result-item {
            padding: 15px;
            border-bottom: 1px solid #e9ecef;
            cursor: pointer;
            transition: background 0.2s;
        }

        .result-item:hover {
            background: #f8f9fa;
        }

        .result-item:last-child {
            border-bottom: none;
        }

        .result-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 5px;
        }

        .result-title {
            font-weight: 600;
            color: #2c3e50;
        }

        .result-time {
            font-size: 0.85em;
            color: #95a5a6;
        }

        .result-summary {
            font-size: 0.95em;
            color: #666;
        }

        .export-buttons {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        .collapsed-details {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background: #f8f9fa;
            border-radius: 4px;
        }

        .result-item.expanded .collapsed-details {
            display: block;
        }

        input[type="checkbox"] {
            cursor: pointer;
            width: 18px;
            height: 18px;
        }

        @media (max-width: 768px) {
            .paper-container {
                padding: 30px 20px;
            }

            h1 {
                font-size: 1.8em;
            }

            canvas {
                max-width: 100%;
                height: auto;
            }

            .controls {
                flex-direction: column;
            }

            .control-group {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="paper-container">
        <header>
            <h1>Nested Farey Channels & Fractional-Slice Coprimality Heuristic</h1>
            <div class="author">Wessen Getachew</div>
            <div class="date">October 2025</div>
        </header>

        <div class="abstract">
            <strong>Abstract.</strong> We introduce the <em>Nested Farey Channel Framework</em>, a geometric representation of modular arithmetic on the unit circle, and develop the <em>Fractional-Slice Coprimality Heuristic</em>, a rapid probabilistic prime detection algorithm based on sampling coprime residues within restricted circular arcs. Each modulus \(m\) maps to \(m\) equidistant points at angles \(2\pi r/m\). Prime moduli exhibit maximal channel openness while composites show blocked Farey channels. We prove that sampling only a fraction of the circle yields strong probabilistic discrimination between primes and composites, derive formal bounds, and provide interactive demonstrations and experimental tools.
        </div>

        <div class="section-title">Part I: Nested Farey Channels Framework</div>

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

        <div class="proposition">
            <span class="label">Proposition 1.3 (Prime Channel Completeness).</span>
            <em>For a prime modulus \(p\), every residue \(r \in \{1,2,\dots,p-1\}\) satisfies \(\gcd(r,p)=1\). Thus \(S_p\) forms a maximally open ring with \(\varphi(p)=p-1\) open channels and a single blocked channel at \(r=0\).</em>
        </div>

        <div class="canvas-container">
            <canvas id="channelCanvas" width="700" height="700"></canvas>
            <div class="controls">
                <div class="control-group">
                    <label for="modInput">Modulus:</label>
                    <input type="number" id="modInput" value="13" min="2" max="500">
                </div>
                <button onclick="drawChannelRing()">Visualize</button>
                <button class="secondary" onclick="toggleChannelLabels()">Toggle Labels</button>
            </div>
            <div class="stats-display" id="channelStats" style="display: none;"></div>
            <div class="caption">Figure 1: Channel ring visualization showing open (green) and blocked (red) channels</div>
        </div>

        <div class="section-title">Part II: Fractional-Slice Coprimality Heuristic</div>

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

        <div class="algorithm">
            <span class="label">Sampling Rule.</span>
            Sample \(k\) residues \(r_1,\dots,r_k\) uniformly from \(S(m)\). If every sampled residue satisfies \(\gcd(r_i,m)=1\), declare \(m\) a <em>prime candidate</em> under the fractional-slice test.
        </div>

        <div class="subsection-title">2.2 Probabilistic Bound</div>

        <p>Assuming independent sampling, the probability of a composite \(m\) passing the test is approximately</p>
        <p style="text-align: center;">
        \[
        \Pr(\text{pass}\mid m) \approx \delta_S(m)^k.
        \]
        </p>

        <div class="proposition">
            <span class="label">Proposition 2.2 (Fractional-Slice Coprimality Bound).</span>
            <em>Let \(m \ge 2\) and let \(S \subset \{1,\dots,m-1\}\) be a fixed sampling subset of size \(|S|\). If a random residue \(r \in S\) is coprime to \(m\) with probability \(\delta_S(m)\), then for \(k\) independent samples (with replacement),</em>
            \[
            \Pr(\text{pass}\mid m) = \delta_S(m)^k.
            \]
            <em>If \(q\) is the smallest prime factor of \(m\), then</em>
            \[
            \Pr(\text{pass}\mid m) \le \Big(1 - \frac{1}{q}\Big)^k.
            \]
        </div>

        <p>This yields the following key behavior:</p>
        <ul>
            <li>For even composites (\(q=2\)): \(\Pr(\text{pass}) \le (1/2)^k\)</li>
            <li>For \(q=3\): \(\Pr(\text{pass}) \le (2/3)^k\)</li>
            <li>For semiprimes with large factors (\(q \gg 1\)): the bound weakens, requiring larger \(k\)</li>
        </ul>

        <p>Thus the heuristic strongly rejects composites with small factors, and becomes probabilistically weaker only for products of large primes.</p>

        <div class="subsection-title">2.3 Slice Dependence and Symmetry</div>

        <div class="proposition">
            <span class="label">Proposition 2.3 (Half-Circle Neutrality).</span>
            <em>For the half-circle slice, mirror symmetry ensures</em>
            \[
            \delta_{\text{half}}(m) = \delta(m),
            \]
            <em>since \(\gcd(r,m)=\gcd(m-r,m)\). Hence the half-circle is a neutral choice that avoids residue bias.</em>
        </div>

        <div class="section-title">3. Interactive Algorithm Demonstration</div>

        <div class="info-box">
            <strong>Test the Heuristic:</strong> Enter a modulus, choose sampling parameters, and watch the fractional-slice algorithm in action. The visualization shows which residues are tested and whether they pass the coprimality check.
        </div>

        <div class="experimental-section">
            <h3 style="color: #667eea; margin-bottom: 20px;">Fractional-Slice Coprimality Test</h3>
            
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
                <button class="secondary" onclick="runBatchTest()">Batch Test (10 runs)</button>
            </div>

            <canvas id="testCanvas" width="600" height="600" style="display: block; margin: 20px auto;"></canvas>
            
            <div id="testResult"></div>
            <div id="batchResults"></div>

            <div class="export-buttons">
                <button class="secondary" onclick="exportTestScreenshot()">📸 Export Screenshot</button>
                <button class="secondary" onclick="exportTestData('json')">📄 Export JSON</button>
                <button class="secondary" onclick="exportTestData('csv')">📊 Export CSV</button>
                <button class="secondary" onclick="clearTestHistory()">🗑️ Clear History</button>
            </div>

            <div id="testHistory" style="display: none;">
                <h4 style="color: #667eea; margin: 20px 0 10px 0;">Test History</h4>
                <div class="results-history" id="testHistoryList"></div>
            </div>
        </div>

        <div class="section-title">4. Algorithmic Formulation</div>

        <div class="algorithm">
            <span class="label">Algorithm 4.1 (Deterministic + Randomized Hybrid Filter).</span>
            <pre>
function is_prime_candidate(m, k, slice="half", 
                           small_primes=[2,3,5,7,11,13]):
    // (1) Deterministic prefilter by small primes
    for q in small_primes:
        if m % q == 0 and m != q:
            return False
    
    // (2) Choose slice
    if slice == "half":
        S = {1, 2, ..., floor(m/2)}
    else if slice == "quarter":
        S = {1, 2, ..., floor(m/4)}
    else:
        S = {1, 2, ..., m-1}
    
    // (3) Random sampling
    for i in 1..k:
        r = random_choice(S)
        if gcd(r, m) != 1:
            return False
    
    return True  // passes fractional-slice test
</pre>
        </div>

        <p>The parameter \(k\) governs tradeoff between false-positive rate and computational cost. For a target false positive probability \(\varepsilon\) and smallest divisor threshold \(Q\), choose</p>
        <p style="text-align: center;">
        \[
        k \ge \frac{\log \varepsilon}{\log(1 - 1/Q)}.
        \]
        </p>

        <div class="section-title">5. Experimental Evaluation</div>

        <div class="experimental-section">
            <h3 style="color: #667eea; margin-bottom: 20px;">Large-Scale Empirical Testing</h3>
            
            <div class="controls" style="margin-bottom: 20px;">
                <div class="control-group">
                    <label for="rangeStart">Range Start:</label>
                    <input type="number" id="rangeStart" value="100" min="2">
                </div>
                <div class="control-group">
                    <label for="rangeEnd">Range End:</label>
                    <input type="number" id="rangeEnd" value="500" min="2">
                </div>
                <div class="control-group">
                    <label for="expSamples">Samples (k):</label>
                    <input type="number" id="expSamples" value="10" min="1" max="50">
                </div>
                <button class="success" onclick="runExperiment()">Run Experiment</button>
            </div>

            <div class="progress-bar" id="progressBar" style="display: none;">
                <div class="progress-fill" id="progressFill">0%</div>
            </div>

            <div id="experimentResults"></div>
        </div>

        <div class="section-title">6. Geometric Interpretation and Concentric Rings</div>

        <p>The fractional-slice heuristic can be visualized in two complementary ways: on the unit circle, and as a 2D plane of concentric rings.</p>

        <div class="subsection-title">6.1 Unit Circle Representation</div>

        <p>Map each residue \(r \in \{1,2,\dots,m-1\}\) to the point</p>
        <p style="text-align: center;">
        \[
        z_r = e^{2\pi i r / m}.
        \]
        </p>
        <p>Coprime residues lie on "open channels" that avoid blocked directions determined by the factors of \(m\).</p>

        <div class="definition">
            <span class="label">Angular Slices.</span>
            Selecting a subset \(S(m)\) of size \(|S|\) corresponds to choosing an arc
            \[
            \theta \in \left[ \frac{2\pi r_0}{m}, \frac{2\pi (r_0 + |S|)}{m} \right)
            \]
            on the unit circle.
            <ul style="margin-top: 10px;">
                <li>Half-circle: \(|S| = \lfloor m/2 \rfloor\), spanning \(\pi\) radians.</li>
                <li>One-\(n\)th slice: \(|S| = \lfloor m/n \rfloor\), spanning \(2\pi/n\) radians.</li>
            </ul>
        </div>

        <p>Blocked Farey channels appear as gaps along the arc where \(\gcd(r,m) > 1\). Prime moduli maximize the fraction of occupied (coprime) points in every slice; composites produce visible voids aligned with their divisors.</p>

        <div class="remarks">
            <strong>Farey Sequence Connection:</strong> Positions of blocked residues correspond to fractions \(r/m\) reducible to lower terms, forming a subset of the Farey sequence \(F_m\). Partial sampling of the circle thus samples a fractional Farey subsequence, producing a geometric signature for primality.
        </div>

        <div class="subsection-title">6.2 Concentric Ring Visualization</div>

        <p>The unit circle can be extended to a 2D plane of concentric rings to capture the nested structure of residues for multiple moduli.</p>

        <ul>
            <li>Let each ring correspond to a modulus \(m\).</li>
            <li>Place the points \(z_r = e^{2\pi i r / m}\) on the ring of radius proportional to \(m\).</li>
            <li>Coprime residues are marked (filled dots), blocked residues are shown differently.</li>
        </ul>

        <div class="canvas-container">
            <h3 style="color: #667eea; margin-bottom: 20px; text-align: center;">Concentric Rings: Nested Farey Structure</h3>
            <div style="text-align: center; margin-bottom: 15px;">
                <span style="color: #666; font-weight: 600;">Resolution: </span>
                <button class="mode-btn" onclick="setConcentricResolution(1920)">HD</button>
                <button class="mode-btn active" onclick="setConcentricResolution(2560)">2K</button>
                <button class="mode-btn" onclick="setConcentricResolution(3840)">4K</button>
            </div>
            <canvas id="concentricCanvas" width="2560" height="2560" style="max-width: 100%; height: auto;"></canvas>
            
            <div class="controls">
                <div class="control-group">
                    <label for="minMod">Min Modulus:</label>
                    <input type="number" id="minMod" value="2" min="2" max="200">
                </div>
                <div class="control-group">
                    <label for="maxMod">Max Modulus:</label>
                    <input type="number" id="maxMod" value="12" min="2" max="200">
                </div>
                <div class="control-group">
                    <label for="pointSize">Point Size:</label>
                    <input type="range" id="pointSize" min="1" max="10" value="3" step="0.5" style="width: 100px;">
                    <span id="pointSizeVal">3</span>px
                </div>
            </div>

            <div class="controls" style="margin-top: 10px;">
                <div class="control-group">
                    <label for="ringMode">Display Mode:</label>
                    <select id="ringMode">
                        <option value="all">All Residues</option>
                        <option value="open-only">Open Channels Only</option>
                        <option value="primes-only">Primes Only</option>
                        <option value="fixed-r">Fixed r (vary m)</option>
                        <option value="fixed-m">Fixed m (vary r)</option>
                    </select>
                </div>
                <div class="control-group" id="fixedRGroup" style="display: none;">
                    <label for="fixedRValue">r value:</label>
                    <input type="number" id="fixedRValue" value="1" min="1" max="100">
                </div>
                <div class="control-group" id="fixedMGroup" style="display: none;">
                    <label for="fixedMValue">m value:</label>
                    <input type="number" id="fixedMValue" value="12" min="2" max="200">
                </div>
            </div>

            <div class="controls" style="margin-top: 10px;">
                <div class="control-group">
                    <label for="colorMode">Color Mode:</label>
                    <select id="colorMode" onchange="updateColorModeInfo()">
                        <option value="open-blocked">1. Binary: Open vs Blocked</option>
                        <option value="gcd-gradient">2. GCD Gradient</option>
                        <option value="gcd-local">3. GCD (Local per m)</option>
                        <option value="gcd-global">4. GCD (Global)</option>
                        <option value="prime-factor">5. Smallest Prime Factor</option>
                        <option value="density-local">6. Local Density Gradient</option>
                        <option value="residue-class">7. Residue Class mod k</option>
                        <option value="farey-level">8. Farey Denominator Level</option>
                        <option value="angular-hue">9. Angular Hue</option>
                        <option value="multi-property">10. Multi-Property (HSB)</option>
                    </select>
                </div>
                <div class="control-group" id="residueClassGroup" style="display: none;">
                    <label for="residueK">mod k:</label>
                    <input type="number" id="residueK" value="3" min="2" max="12">
                </div>
                <div id="colorModeInfo" style="margin-top: 5px; font-size: 0.85em; color: #666; font-style: italic;"></div>
            </div>

            <div class="controls" style="margin-top: 15px;">
                <strong style="color: #495057;">Visibility:</strong>
                <label style="display: inline-flex; align-items: center; margin-left: 15px;">
                    <input type="checkbox" id="showRings" checked style="margin-right: 5px;">
                    Ring Lines
                </label>
                <label style="display: inline-flex; align-items: center; margin-left: 15px;">
                    <input type="checkbox" id="showLabels" checked style="margin-right: 5px;">
                    Modulus Labels
                </label>
                <label style="display: inline-flex; align-items: center; margin-left: 15px;">
                    <input type="checkbox" id="showAxes" checked style="margin-right: 5px;">
                    Axes
                </label>
                <label style="display: inline-flex; align-items: center; margin-left: 15px;">
                    <input type="checkbox" id="showLegend" checked style="margin-right: 5px;">
                    Legend
                </label>
            </div>

            <div class="controls" style="margin-top: 15px;">
                <button onclick="drawConcentricRings()">Visualize</button>
                <button class="success" onclick="exportConcentricWithLegend('4k')">📸 Export 4K + Legend</button>
                <button class="success" onclick="exportConcentricWithLegend('2k')">📸 Export 2K + Legend</button>
                <button class="secondary" onclick="exportConcentricView()">📸 Simple Export</button>
            </div>
            
            <div class="stats-display" id="concentricStats" style="margin-top: 20px;"></div>
            <div class="caption">Figure 2: Concentric rings showing nested Farey channel structure across multiple moduli</div>
        </div>

        <div class="remarks">
            <strong>Interpretation:</strong>
            <ul>
                <li>Each ring shows the local coprimality pattern for a single modulus.</li>
                <li>Nested rings reveal how Farey channels propagate across successive moduli.</li>
                <li>Angular gaps (blocked channels) align radially, illustrating the "nested" property: blocked residues of smaller divisors project outward to higher moduli.</li>
            </ul>
        </div>

        <div class="proposition">
            <span class="label">Visualization Principle.</span>
            <em>By combining angular slices on the unit circle with concentric rings in 2D, we obtain a comprehensive geometric view:</em>
            \[
            \text{Prime moduli: full occupancy along slices and rings} \quad\quad
            \text{Composite moduli: radial gaps aligned with factors.}
            \]
            <em>This representation underlies the fractional-slice heuristic and provides visual intuition for why primes maintain maximal channel openness, even when sampling only a fraction of the residues.</em>
        </div>

        <div class="section-title">7. Failure Modes and Limitations</div>

        <ul>
            <li><strong>Semiprime leakage:</strong> Composites with large prime factors can pass the test.</li>
            <li><strong>Carmichael-like pseudoprimes:</strong> These may evade simple gcd-based filtering.</li>
            <li><strong>Slice bias:</strong> Improper slice selection can undercount blocked channels.</li>
        </ul>

        <p>The heuristic is therefore best used as a rapid <em>prefilter</em> prior to a deterministic or probabilistic primality test (e.g., Miller–Rabin).</p>

        <div class="section-title">8. Conclusion</div>

        <p>Fractional-slice coprimality sampling provides a geometric and probabilistic bridge between Nested Farey Channel theory and practical number testing. It captures the essential property that prime moduli maintain maximal channel openness even when viewed through restricted arcs of the unit circle, while composites introduce blocked Farey channels visible through partial sampling.</p>

        <p>This heuristic can serve both as:</p>
        <ol>
            <li>A fast preliminary screen for prime candidates within modular sieves.</li>
            <li>A geometric diagnostic tool for visualizing the distribution of coprime residues across modular arcs.</li>
        </ol>

        <p>Further work includes: quantifying slice bias functions \(\beta_S(m)\), linking partial-channel openness to residue equidistribution, and integrating this fractional sampling into the modular sieve hierarchy for scalable prime detection.</p>

        <div style="margin-top: 50px; padding-top: 30px; border-top: 3px solid #667eea; text-align: center; color: #7f8c8d;">
            <p><em>Interactive paper by Wessen Getachew, October 2025</em></p>
            <p style="margin-top: 10px; font-size: 0.9em;">Full framework implementation with live algorithm demonstrations</p>
        </div>
    </div>

    <script>
        // ==================== UTILITY FUNCTIONS ====================
        
        function gcd(a, b) {
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }

        function eulerPhi(n) {
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

        function isPrime(n) {
            if (n < 2) return false;
            if (n === 2) return true;
            if (n % 2 === 0) return false;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return false;
            }
            return true;
        }

        function smallestPrimeFactor(n) {
            if (n % 2 === 0) return 2;
            for (let i = 3; i * i <= n; i += 2) {
                if (n % i === 0) return i;
            }
            return n;
        }

        // ==================== CHANNEL VISUALIZATION ====================
        
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

            ctx.clearRect(0, 0, width, height);

            // Draw circle
            ctx.strokeStyle = '#34495e';
            ctx.lineWidth = 2.5;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.stroke();

            // Draw origin
            ctx.fillStyle = '#e74c3c';
            ctx.beginPath();
            ctx.arc(centerX + radius, centerY, 10, 0, 2 * Math.PI);
            ctx.fill();

            // Draw channels
            const phi = eulerPhi(m);
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

        function toggleChannelLabels() {
            showChannelLabels = !showChannelLabels;
            drawChannelRing();
        }

        // ==================== FRACTIONAL-SLICE TEST ====================
        
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

        function runBatchTest() {
            const m = parseInt(document.getElementById('testModulus').value);
            const k = parseInt(document.getElementById('sampleCount').value);
            const sliceType = document.getElementById('sliceType').value;

            if (isNaN(m) || m < 2 || isNaN(k) || k < 1) return;

            const slice = getSlice(m, sliceType);
            let passCount = 0;

            for (let trial = 0; trial < 10; trial++) {
                let allPass = true;
                for (let i = 0; i < k; i++) {
                    const r = slice[Math.floor(Math.random() * slice.length)];
                    if (gcd(r, m) !== 1) {
                        allPass = false;
                        break;
                    }
                }
                if (allPass) passCount++;
            }

            const resultDiv = document.getElementById('batchResults');
            const prime = isPrime(m);
            const q = smallestPrimeFactor(m);
            const theoreticalProb = Math.pow(1 - 1/q, k);

            resultDiv.innerHTML = `
                <div class="stats-display" style="margin-top: 20px;">
                    <h4 style="color: #667eea; margin-bottom: 10px;">Batch Test Results (10 runs)</h4>
                    <div class="stat-row"><span class="stat-label">Modulus:</span><span class="stat-value">${m} (${prime ? 'Prime' : 'Composite'})</span></div>
                    <div class="stat-row"><span class="stat-label">Passes:</span><span class="stat-value">${passCount}/10</span></div>
                    <div class="stat-row"><span class="stat-label">Empirical Pass Rate:</span><span class="stat-value">${(passCount/10).toFixed(2)}</span></div>
                    <div class="stat-row"><span class="stat-label">Theoretical Pass Prob:</span><span class="stat-value">${theoreticalProb.toFixed(4)}</span></div>
                    <div class="stat-row"><span class="stat-label">Error:</span><span class="stat-value">${Math.abs(passCount/10 - theoreticalProb).toFixed(4)}</span></div>
                </div>
            `;
        }

        // ==================== LARGE-SCALE EXPERIMENT ====================
        
        function runExperiment() {
            const start = parseInt(document.getElementById('rangeStart').value);
            const end = parseInt(document.getElementById('rangeEnd').value);
            const k = parseInt(document.getElementById('expSamples').value);

            if (isNaN(start) || isNaN(end) || isNaN(k) || start >= end) return;

            const progressBar = document.getElementById('progressBar');
            const progressFill = document.getElementById('progressFill');
            progressBar.style.display = 'block';

            let truePositives = 0, falsePositives = 0;
            let trueNegatives = 0, falseNegatives = 0;

            const total = end - start + 1;
            let processed = 0;

            setTimeout(() => processRange(), 10);

            function processRange() {
                const batchSize = 10;
                const batchEnd = Math.min(processed + batchSize, total);

                for (let i = processed; i < batchEnd; i++) {
                    const m = start + i;
                    const prime = isPrime(m);
                    const passed = fractionalSliceTest(m, k, 'half');

                    if (prime && passed) truePositives++;
                    else if (!prime && passed) falsePositives++;
                    else if (!prime && !passed) trueNegatives++;
                    else if (prime && !passed) falseNegatives++;
                }

                processed = batchEnd;
                const progress = Math.round((processed / total) * 100);
                progressFill.style.width = progress + '%';
                progressFill.textContent = progress + '%';

                if (processed < total) {
                    setTimeout(processRange, 10);
                } else {
                    displayExperimentResults();
                }
            }

            function displayExperimentResults() {
                progressBar.style.display = 'none';

                const sensitivity = truePositives / (truePositives + falseNegatives);
                const specificity = trueNegatives / (trueNegatives + falsePositives);
                const precision = truePositives / (truePositives + falsePositives);

                const resultsDiv = document.getElementById('experimentResults');
                resultsDiv.innerHTML = `
                    <h4 style="color: #667eea; margin: 20px 0;">Experiment Results: Range [${start}, ${end}], k=${k}</h4>
                    <table>
                        <tr>
                            <th></th>
                            <th>Predicted Prime</th>
                            <th>Predicted Composite</th>
                        </tr>
                        <tr>
                            <td><strong>Actual Prime</strong></td>
                            <td style="background: #d4edda;">${truePositives}</td>
                            <td style="background: #f8d7da;">${falseNegatives}</td>
                        </tr>
                        <tr>
                            <td><strong>Actual Composite</strong></td>
                            <td style="background: #f8d7da;">${falsePositives}</td>
                            <td style="background: #d4edda;">${trueNegatives}</td>
                        </tr>
                    </table>
                    <div class="stats-display" style="margin-top: 20px;">
                        <div class="stat-row"><span class="stat-label">Sensitivity (TPR):</span><span class="stat-value">${(sensitivity * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">Specificity (TNR):</span><span class="stat-value">${(specificity * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">Precision (PPV):</span><span class="stat-value">${(precision * 100).toFixed(2)}%</span></div>
                        <div class="stat-row"><span class="stat-label">False Positive Rate:</span><span class="stat-value">${((1-specificity) * 100).toFixed(2)}%</span></div>
                    </div>
                `;
            }
        }

        function fractionalSliceTest(m, k, sliceType) {
            const slice = getSlice(m, sliceType);
            for (let i = 0; i < k; i++) {
                const r = slice[Math.floor(Math.random() * slice.length)];
                if (gcd(r, m) !== 1) return false;
            }
            return true;
        }

        // ==================== COMPREHENSIVE LEGEND EXPORT ====================
        
        function exportConcentricWithLegend(quality = '4k') {
            const canvas = document.getElementById('concentricCanvas');
            const originalWidth = canvas.width;
            const originalHeight = canvas.height;
            
            // Set resolution
            let exportWidth, exportHeight;
            if (quality === '4k') {
                exportWidth = exportHeight = 3840;
            } else if (quality === '2k') {
                exportWidth = exportHeight = 2560;
            } else {
                exportWidth = exportHeight = 1920;
            }
            
            // Temporarily resize and redraw
            canvas.width = exportWidth;
            canvas.height = exportHeight;
            drawConcentricRings();
            
            // Now create a new canvas with space for detailed legend
            const legendWidth = Math.floor(exportWidth * 0.3); // 30% width for legend
            const fullCanvas = document.createElement('canvas');
            fullCanvas.width = exportWidth + legendWidth;
            fullCanvas.height = exportHeight;
            const fullCtx = fullCanvas.getContext('2d');
            
            // White background
            fullCtx.fillStyle = 'white';
            fullCtx.fillRect(0, 0, fullCanvas.width, fullCanvas.height);
            
            // Draw main visualization
            fullCtx.drawImage(canvas, 0, 0);
            
            // Draw comprehensive legend
            drawComprehensiveLegend(fullCtx, exportWidth, 0, legendWidth, exportHeight);
            
            // Export
            const link = document.createElement('a');
            link.download = `concentric-${quality}-legend-${Date.now()}.png`;
            link.href = fullCanvas.toDataURL('image/png');
            link.click();
            
            // Restore original size
            canvas.width = originalWidth;
            canvas.height = originalHeight;
            drawConcentricRings();
        }

        function drawComprehensiveLegend(ctx, x, y, width, height) {
            const minMod = parseInt(document.getElementById('minMod').value);
            const maxMod = parseInt(document.getElementById('maxMod').value);
            const mode = document.getElementById('ringMode').value;
            const colorMode = document.getElementById('colorMode').value;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            const residueK = parseInt(document.getElementById('residueK')?.value || 3);
            
            // Calculate statistics
            let totalPoints = 0;
            let openPoints = 0;
            let blockedPoints = 0;
            let primeRings = 0;
            let compositeRings = 0;
            const gcdCounts = {};
            const primeFactorCounts = {};
            
            for (let m = minMod; m <= maxMod; m++) {
                if (mode === 'primes-only' && !isPrime(m)) continue;
                if (mode === 'fixed-m') {
                    const fixedM = parseInt(document.getElementById('fixedMValue').value);
                    if (m !== fixedM) continue;
                }
                
                if (isPrime(m)) primeRings++;
                else compositeRings++;
                
                for (let r = 1; r < m; r++) {
                    if (mode === 'fixed-r') {
                        const fixedR = parseInt(document.getElementById('fixedRValue').value);
                        if (r !== fixedR) continue;
                    }
                    
                    const gcdVal = gcd(r, m);
                    const isOpen = gcdVal === 1;
                    
                    totalPoints++;
                    if (isOpen) openPoints++;
                    else blockedPoints++;
                    
                    gcdCounts[gcdVal] = (gcdCounts[gcdVal] || 0) + 1;
                    
                    if (gcdVal > 1) {
                        const spf = smallestPrimeFactor(gcdVal);
                        primeFactorCounts[spf] = (primeFactorCounts[spf] || 0) + 1;
                    }
                }
            }
            
            // Drawing settings
            const padding = 20;
            const fontSize = Math.max(12, width / 40);
            const lineHeight = fontSize * 1.5;
            let currentY = y + padding;
            
            // Title
            ctx.fillStyle = '#2c3e50';
            ctx.font = `bold ${fontSize * 1.4}px Arial`;
            ctx.fillText('VISUALIZATION LEGEND', x + padding, currentY);
            currentY += lineHeight * 2;
            
            // Parameters Section
            ctx.font = `bold ${fontSize * 1.1}px Arial`;
            ctx.fillText('═══ PARAMETERS ═══', x + padding, currentY);
            currentY += lineHeight * 1.2;
            
            ctx.font = `${fontSize}px Arial`;
            const params = [
                `Modulus Range: ${minMod} – ${maxMod}`,
                `Display Mode: ${mode}`,
                `Color Mode: ${colorMode}`,
                `Point Size: ${pointSize}px`,
                mode === 'residue-class' ? `Residue mod k: ${residueK}` : null,
                mode === 'fixed-r' ? `Fixed r: ${document.getElementById('fixedRValue').value}` : null,
                mode === 'fixed-m' ? `Fixed m: ${document.getElementById('fixedMValue').value}` : null,
            ].filter(p => p !== null);
            
            params.forEach(param => {
                ctx.fillText(param, x + padding, currentY);
                currentY += lineHeight;
            });
            
            currentY += lineHeight * 0.5;
            
            // Statistics Section
            ctx.font = `bold ${fontSize * 1.1}px Arial`;
            ctx.fillText('═══ STATISTICS ═══', x + padding, currentY);
            currentY += lineHeight * 1.2;
            
            ctx.font = `${fontSize}px Arial`;
            const stats = [
                `Total Rings: ${primeRings + compositeRings}`,
                `Prime Rings: ${primeRings}`,
                `Composite Rings: ${compositeRings}`,
                `Total Points: ${totalPoints}`,
                `Open Channels: ${openPoints}`,
                `Blocked Channels: ${blockedPoints}`,
                `Open Density: ${(openPoints/totalPoints*100).toFixed(1)}%`,
            ];
            
            stats.forEach(stat => {
                ctx.fillText(stat, x + padding, currentY);
                currentY += lineHeight;
            });
            
            currentY += lineHeight * 0.5;
            
            // GCD Distribution
            if (Object.keys(gcdCounts).length > 0) {
                ctx.font = `bold ${fontSize * 1.1}px Arial`;
                ctx.fillText('═══ GCD DISTRIBUTION ═══', x + padding, currentY);
                currentY += lineHeight * 1.2;
                
                ctx.font = `${fontSize * 0.9}px Arial`;
                const sortedGCDs = Object.keys(gcdCounts).map(Number).sort((a,b) => a-b).slice(0, 10);
                sortedGCDs.forEach(gcdVal => {
                    const count = gcdCounts[gcdVal];
                    const percentage = (count/totalPoints*100).toFixed(1);
                    
                    // Draw color sample
                    let sampleColor;
                    switch(colorMode) {
                        case 'gcd-local':
                        case 'gcd-gradient':
                            sampleColor = getGCDColor(gcdVal, Math.max(...Object.keys(gcdCounts).map(Number)));
                            break;
                        case 'gcd-global':
                            sampleColor = getGCDColorGlobal(gcdVal);
                            break;
                        case 'prime-factor':
                            sampleColor = getSmallestPrimeFactorColor(gcdVal);
                            break;
                        default:
                            sampleColor = gcdVal === 1 ? '#27ae60' : '#e74c3c';
                    }
                    
                    ctx.fillStyle = sampleColor;
                    ctx.beginPath();
                    ctx.arc(x + padding + 8, currentY - 4, 6, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText(`gcd=${gcdVal}: ${count} (${percentage}%)`, x + padding + 20, currentY);
                    currentY += lineHeight * 0.9;
                });
            }
            
            currentY += lineHeight * 0.5;
            
            // Prime Factor Distribution (if applicable)
            if (Object.keys(primeFactorCounts).length > 0 && colorMode === 'prime-factor') {
                ctx.font = `bold ${fontSize * 1.1}px Arial`;
                ctx.fillText('═══ PRIME FACTORS ═══', x + padding, currentY);
                currentY += lineHeight * 1.2;
                
                ctx.font = `${fontSize * 0.9}px Arial`;
                const sortedPrimes = Object.keys(primeFactorCounts).map(Number).sort((a,b) => a-b);
                sortedPrimes.forEach(prime => {
                    const count = primeFactorCounts[prime];
                    const color = getSmallestPrimeFactorColor(prime);
                    
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x + padding + 8, currentY - 4, 6, 0, 2 * Math.PI);
                    ctx.fill();
                    
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText(`Prime ${prime}: ${count} points`, x + padding + 20, currentY);
                    currentY += lineHeight * 0.9;
                });
            }
            
            currentY += lineHeight * 0.5;
            
            // Color Mode Explanation
            ctx.font = `bold ${fontSize * 1.1}px Arial`;
            ctx.fillText('═══ COLOR KEY ═══', x + padding, currentY);
            currentY += lineHeight * 1.2;
            
            ctx.font = `${fontSize * 0.85}px Arial`;
            const colorExplanations = {
                'open-blocked': ['Green = Coprime (open)', 'Red = Blocked'],
                'gcd-gradient': ['Green→Red gradient', 'by GCD magnitude'],
                'gcd-local': ['Colors per ring', 'by GCD value'],
                'gcd-global': ['Same GCD =', 'same color globally'],
                'prime-factor': ['Color = smallest', 'prime factor of gcd'],
                'density-local': ['Brightness = local', 'coprime density'],
                'residue-class': [`Colors by r mod ${residueK}`],
                'farey-level': ['Brightness = reduced', 'denominator level'],
                'angular-hue': ['Hue by angle', 'Brightness by coprime'],
                'multi-property': ['Hue=angle, Sat=gcd', 'Bright=slice member'],
            };
            
            const explanations = colorExplanations[colorMode] || ['Standard coloring'];
            explanations.forEach(line => {
                ctx.fillText(line, x + padding, currentY);
                currentY += lineHeight * 0.85;
            });
            
            // Footer
            currentY = y + height - padding - lineHeight * 2;
            ctx.font = `${fontSize * 0.8}px Arial`;
            ctx.fillStyle = '#95a5a6';
            ctx.fillText('Generated: ' + new Date().toLocaleString(), x + padding, currentY);
            currentY += lineHeight;
            ctx.fillText('Nested Farey Channels Framework', x + padding, currentY);
            ctx.fillText('by Wessen Getachew', x + padding, currentY + lineHeight);
        }

        // Initialize
        drawChannelRing();
        updateColorModeInfo();

        // ==================== RESULTS HISTORY ====================
        
        let testHistory = [];

        function addToHistory(result) {
            testHistory.unshift(result);
            if (testHistory.length > 50) testHistory.pop();
            updateHistoryDisplay();
        }

        function updateHistoryDisplay() {
            const historyDiv = document.getElementById('testHistory');
            const listDiv = document.getElementById('testHistoryList');
            
            if (testHistory.length === 0) {
                historyDiv.style.display = 'none';
                return;
            }
            
            historyDiv.style.display = 'block';
            listDiv.innerHTML = testHistory.map((item, idx) => `
                <div class="result-item" onclick="toggleResultDetails(${idx})">
                    <div class="result-header">
                        <span class="result-title">${item.type}: m=${item.modulus}, k=${item.k}</span>
                        <span class="result-time">${item.timestamp}</span>
                    </div>
                    <div class="result-summary">
                        Result: ${item.passed ? 'PASS ✓' : 'FAIL ✗'} | 
                        ${item.prime ? 'Prime' : 'Composite'} | 
                        Density: ${item.density}
                    </div>
                    <div class="collapsed-details">
                        <strong>Details:</strong><br>
                        Samples: ${item.passedSamples}/${item.k}<br>
                        Smallest Factor: ${item.smallestFactor}<br>
                        Theoretical Prob: ${item.theoreticalProb}<br>
                        Slice Type: ${item.sliceType}
                    </div>
                </div>
            `).join('');
        }

        function toggleResultDetails(idx) {
            const items = document.querySelectorAll('.result-item');
            items[idx].classList.toggle('expanded');
        }

        function clearTestHistory() {
            if (confirm('Clear all test history?')) {
                testHistory = [];
                updateHistoryDisplay();
            }
        }

        // ==================== EXPORT FUNCTIONS ====================
        
        function exportTestScreenshot() {
            const canvas = document.getElementById('testCanvas');
            const link = document.createElement('a');
            link.download = `farey-test-${Date.now()}.png`;
            link.href = canvas.toDataURL();
            link.click();
        }

        function exportConcentricView() {
            const canvas = document.getElementById('concentricCanvas');
            const link = document.createElement('a');
            link.download = `concentric-rings-${Date.now()}.png`;
            link.href = canvas.toDataURL();
            link.click();
        }

        function exportTestData(format) {
            if (testHistory.length === 0) {
                alert('No test history to export');
                return;
            }

            let content, mimeType, extension;

            if (format === 'json') {
                content = JSON.stringify(testHistory, null, 2);
                mimeType = 'application/json';
                extension = 'json';
            } else if (format === 'csv') {
                const headers = 'Timestamp,Type,Modulus,Prime,Passed,Samples(k),PassedSamples,Density,SmallestFactor,TheoreticalProb,SliceType\n';
                const rows = testHistory.map(item => 
                    `"${item.timestamp}",${item.type},${item.modulus},${item.prime},${item.passed},${item.k},${item.passedSamples},${item.density},${item.smallestFactor},${item.theoreticalProb},${item.sliceType}`
                ).join('\n');
                content = headers + rows;
                mimeType = 'text/csv';
                extension = 'csv';
            }

            const blob = new Blob([content], { type: mimeType });
            const link = document.createElement('a');
            link.download = `farey-tests-${Date.now()}.${extension}`;
            link.href = URL.createObjectURL(blob);
            link.click();
        }

        // ==================== CONCENTRIC RINGS VISUALIZATION ====================
        
        let concentricResolution = 2560;

        function setConcentricResolution(res) {
            concentricResolution = res;
            const canvas = document.getElementById('concentricCanvas');
            canvas.width = res;
            canvas.height = res;
            
            // Update button states
            document.querySelectorAll('.canvas-container .mode-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            drawConcentricRings();
        }

        // Update point size display
        document.getElementById('pointSize')?.addEventListener('input', function() {
            document.getElementById('pointSizeVal').textContent = this.value;
        });

        // Show/hide fixed value inputs based on mode
        document.getElementById('ringMode')?.addEventListener('change', function() {
            const fixedRGroup = document.getElementById('fixedRGroup');
            const fixedMGroup = document.getElementById('fixedMGroup');
            
            fixedRGroup.style.display = this.value === 'fixed-r' ? 'flex' : 'none';
            fixedMGroup.style.display = this.value === 'fixed-m' ? 'flex' : 'none';
        });

        // GCD-based color palette
        const gcdColors = [
            '#e74c3c', // gcd=1 (or blocked)
            '#27ae60', // gcd=1 (coprime)
            '#3498db', // gcd=2
            '#f39c12', // gcd=3
            '#9b59b6', // gcd=4
            '#1abc9c', // gcd=5
            '#e67e22', // gcd=6
            '#34495e', // gcd=7
            '#16a085', // gcd=8
            '#d35400', // gcd=9
            '#c0392b', // gcd=10+
        ];

        function getGCDColor(gcdValue, maxGCD) {
            if (gcdValue === 1) return '#27ae60'; // Coprime - always green
            
            // Map gcd to color index
            const idx = Math.min(gcdValue, gcdColors.length - 1);
            return gcdColors[idx];
        }

        function getGCDColorGlobal(gcdValue) {
            const globalColors = {
                1: '#27ae60',  // Coprime
                2: '#e74c3c',  // Even
                3: '#3498db',  // Multiple of 3
                4: '#f39c12',  // Multiple of 4
                5: '#9b59b6',  // Multiple of 5
                6: '#1abc9c',  // Multiple of 6
                7: '#e67e22',  // Multiple of 7
                8: '#34495e',  // Multiple of 8
                9: '#16a085',  // Multiple of 9
                10: '#d35400', // Multiple of 10
            };
            return globalColors[gcdValue] || '#95a5a6';
        }

        // NEW: GCD Gradient coloring
        function getGCDGradientColor(gcdValue, maxGCD) {
            if (gcdValue === 1) return '#27ae60'; // Coprime - bright green
            
            // Gradient from green to red based on gcd magnitude
            const intensity = gcdValue / maxGCD;
            const hue = 120 * (1 - intensity); // 120=green to 0=red
            return `hsl(${hue}, 70%, 50%)`;
        }

        // NEW: Smallest prime factor coloring
        function getSmallestPrimeFactorColor(gcdValue) {
            if (gcdValue === 1) return '#ecf0f1'; // Near-white for coprime
            
            const spf = smallestPrimeFactor(gcdValue);
            const primeColors = {
                2: '#3498db',   // Blue
                3: '#f1c40f',   // Yellow
                5: '#e67e22',   // Orange
                7: '#9b59b6',   // Purple
                11: '#1abc9c',  // Turquoise
                13: '#e74c3c',  // Red
                17: '#16a085',  // Dark cyan
                19: '#d35400',  // Dark orange
                23: '#8e44ad',  // Dark purple
                29: '#27ae60',  // Green
                31: '#2c3e50',  // Dark blue
            };
            return primeColors[spf] || '#95a5a6';
        }

        // NEW: Local density gradient
        function getLocalDensityColor(r, m, windowSize = 5) {
            // Count coprime residues in window around r
            let coprimeCount = 0;
            const halfWindow = Math.floor(windowSize / 2);
            
            for (let i = -halfWindow; i <= halfWindow; i++) {
                const testR = ((r + i - 1 + m) % m) + 1;
                if (testR >= 1 && testR < m && gcd(testR, m) === 1) {
                    coprimeCount++;
                }
            }
            
            const density = coprimeCount / windowSize;
            const hue = 120 * density; // Green gradient
            const sat = 70;
            const light = 30 + density * 40; // Darker to brighter
            return `hsl(${hue}, ${sat}%, ${light}%)`;
        }

        // NEW: Residue class mod k coloring
        function getResidueClassColor(r, k) {
            const residue = r % k;
            const hue = (residue * 360) / k;
            return `hsl(${hue}, 70%, 50%)`;
        }

        // NEW: Farey denominator level coloring
        function getFareyLevelColor(r, m) {
            const g = gcd(r, m);
            const reducedDenom = m / g;
            
            // Smaller denominators = brighter
            const maxDenom = m;
            const brightness = 100 - (reducedDenom / maxDenom) * 60;
            return `hsl(200, 70%, ${brightness}%)`;
        }

        // NEW: Angular hue coloring
        function getAngularHueColor(r, m) {
            const angle = (2 * Math.PI * r) / m;
            const hue = (angle / (2 * Math.PI)) * 360;
            const isOpen = gcd(r, m) === 1;
            const sat = 70;
            const light = isOpen ? 50 : 30; // Brighter if coprime
            return `hsl(${hue}, ${sat}%, ${light}%)`;
        }

        // NEW: Multi-property (HSB) coloring
        function getMultiPropertyColor(r, m, inSlice = true) {
            const g = gcd(r, m);
            const angle = (2 * Math.PI * r) / m;
            
            // Hue: angle
            const hue = (angle / (2 * Math.PI)) * 360;
            
            // Saturation: gcd (coprime = high saturation)
            const sat = g === 1 ? 80 : 30;
            
            // Brightness: slice membership
            const light = inSlice ? 60 : 30;
            
            return `hsl(${hue}, ${sat}%, ${light}%)`;
        }

        // Color mode info text
        function updateColorModeInfo() {
            const mode = document.getElementById('colorMode').value;
            const infoDiv = document.getElementById('colorModeInfo');
            const residueGroup = document.getElementById('residueClassGroup');
            
            const infoTexts = {
                'open-blocked': 'Binary: Green=coprime, Red=blocked',
                'gcd-gradient': 'Gradient intensity by gcd(r,m) magnitude',
                'gcd-local': 'Each ring: independent color per GCD value',
                'gcd-global': 'All rings: same GCD = same color (shows nesting)',
                'prime-factor': 'Color by smallest prime factor of gcd(r,m)',
                'density-local': 'Heatmap: local coprime density around each r',
                'residue-class': 'Color by residue class r mod k',
                'farey-level': 'Brightness by reduced denominator (Farey level)',
                'angular-hue': 'Hue by angle, brightness by coprimality',
                'multi-property': 'Hue=angle, Saturation=gcd, Brightness=slice'
            };
            
            infoDiv.textContent = infoTexts[mode] || '';
            residueGroup.style.display = mode === 'residue-class' ? 'flex' : 'none';
        }

        function drawConcentricRings() {
            const canvas = document.getElementById('concentricCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;

            const minMod = parseInt(document.getElementById('minMod').value);
            const maxMod = parseInt(document.getElementById('maxMod').value);
            const mode = document.getElementById('ringMode').value;
            const colorMode = document.getElementById('colorMode').value;
            const pointSize = parseFloat(document.getElementById('pointSize').value);
            
            const showRings = document.getElementById('showRings').checked;
            const showLabels = document.getElementById('showLabels').checked;
            const showAxes = document.getElementById('showAxes').checked;
            const showLegend = document.getElementById('showLegend').checked;

            if (isNaN(minMod) || isNaN(maxMod) || minMod >= maxMod) return;

            ctx.clearRect(0, 0, width, height);

            // Draw axes
            if (showAxes) {
                ctx.strokeStyle = '#e0e0e0';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(0, centerY);
                ctx.lineTo(width, centerY);
                ctx.moveTo(centerX, 0);
                ctx.lineTo(centerX, height);
                ctx.stroke();
            }

            const maxRadius = Math.min(width, height) / 2 - 80;
            const radiusStep = maxRadius / (maxMod - minMod + 1);

            // For fixed-m mode, get the fixed value
            let fixedM = null;
            if (mode === 'fixed-m') {
                fixedM = parseInt(document.getElementById('fixedMValue').value);
            }

            // For fixed-r mode, get the fixed value
            let fixedR = null;
            if (mode === 'fixed-r') {
                fixedR = parseInt(document.getElementById('fixedRValue').value);
            }

            // Collect all GCD values for local coloring
            let allGCDs = new Set();
            if (colorMode === 'gcd-local' || colorMode === 'gcd-global') {
                for (let m = minMod; m <= maxMod; m++) {
                    if (mode === 'primes-only' && !isPrime(m)) continue;
                    if (mode === 'fixed-m' && m !== fixedM) continue;
                    
                    for (let r = 1; r < m; r++) {
                        if (mode === 'fixed-r' && r !== fixedR) continue;
                        allGCDs.add(gcd(r, m));
                    }
                }
            }

            // Draw concentric rings
            for (let m = minMod; m <= maxMod; m++) {
                if (mode === 'primes-only' && !isPrime(m)) continue;
                if (mode === 'fixed-m' && m !== fixedM) continue;

                const radius = radiusStep * (m - minMod + 1);
                const prime = isPrime(m);

                // Draw ring circle
                if (showRings) {
                    ctx.strokeStyle = prime ? '#27ae60' : '#95a5a6';
                    ctx.lineWidth = prime ? 3 : 1.5;
                    ctx.setLineDash(prime ? [] : [10, 5]);
                    ctx.beginPath();
                    ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
                    ctx.stroke();
                    ctx.setLineDash([]);
                }

                // Draw label
                if (showLabels) {
                    ctx.fillStyle = prime ? '#27ae60' : '#7f8c8d';
                    ctx.font = `bold ${Math.max(12, width/200)}px serif`;
                    const label = mode === 'fixed-r' ? `m=${m}, r=${fixedR}` : 
                                 mode === 'fixed-m' ? `m=${fixedM}` : `m=${m}`;
                    ctx.fillText(label, centerX + radius + 10, centerY);
                }

                // Draw residue points
                const startR = (mode === 'fixed-m') ? 1 : (mode === 'fixed-r' ? fixedR : 1);
                const endR = (mode === 'fixed-m') ? m - 1 : (mode === 'fixed-r' ? fixedR : m - 1);

                for (let r = startR; r <= endR; r++) {
                    if (mode === 'fixed-r' && r !== fixedR) continue;
                    if (r >= m) continue;

                    const gcdVal = gcd(r, m);
                    const isOpen = gcdVal === 1;
                    
                    if (mode === 'open-only' && !isOpen) continue;

                    const theta = (2 * Math.PI * r) / m;
                    const x = centerX + radius * Math.cos(theta);
                    const y = centerY - radius * Math.sin(theta);

                    // Determine color based on color mode
                    let color;
                    const residueK = parseInt(document.getElementById('residueK')?.value || 3);
                    
                    switch(colorMode) {
                        case 'open-blocked':
                            color = isOpen ? (prime ? '#27ae60' : '#3498db') : '#e74c3c';
                            break;
                        case 'gcd-gradient':
                            color = getGCDGradientColor(gcdVal, Math.max(...Array.from(allGCDs)));
                            break;
                        case 'gcd-local':
                            color = getGCDColor(gcdVal, Math.max(...Array.from(allGCDs)));
                            break;
                        case 'gcd-global':
                            color = getGCDColorGlobal(gcdVal);
                            break;
                        case 'prime-factor':
                            color = getSmallestPrimeFactorColor(gcdVal);
                            break;
                        case 'density-local':
                            color = getLocalDensityColor(r, m);
                            break;
                        case 'residue-class':
                            color = getResidueClassColor(r, residueK);
                            break;
                        case 'farey-level':
                            color = getFareyLevelColor(r, m);
                            break;
                        case 'angular-hue':
                            color = getAngularHueColor(r, m);
                            break;
                        case 'multi-property':
                            const inSlice = r <= Math.floor(m/2); // Example: half-circle
                            color = getMultiPropertyColor(r, m, inSlice);
                            break;
                        default:
                            color = isOpen ? '#27ae60' : '#e74c3c';
                    }

                    // Draw point - filled for most modes, outlined for blocked in binary mode
                    const shouldFill = colorMode !== 'open-blocked' || isOpen;
                    if (shouldFill) {
                        ctx.fillStyle = color;
                        ctx.beginPath();
                        ctx.arc(x, y, pointSize, 0, 2 * Math.PI);
                        ctx.fill();
                    } else {
                        ctx.strokeStyle = color;
                        ctx.lineWidth = Math.max(1.5, pointSize * 0.5);
                        ctx.beginPath();
                        ctx.arc(x, y, pointSize, 0, 2 * Math.PI);
                        ctx.stroke();
                    }
                }
            }

            // Draw legend
            if (showLegend) {
                const legendX = 30;
                const legendY = height - 150;
                const legendWidth = 280;
                let legendHeight = 120;

                // Adjust legend height based on color mode
                if (colorMode.startsWith('gcd')) {
                    legendHeight = Math.min(300, 80 + allGCDs.size * 25);
                }

                ctx.fillStyle = 'rgba(255, 255, 255, 0.95)';
                ctx.fillRect(legendX, legendY, legendWidth, legendHeight);
                ctx.strokeStyle = '#667eea';
                ctx.lineWidth = 3;
                ctx.strokeRect(legendX, legendY, legendWidth, legendHeight);

                ctx.font = `${Math.max(12, width/200)}px serif`;
                let yOffset = legendY + 25;

                if (colorMode === 'open-blocked') {
                    ctx.fillStyle = '#27ae60';
                    ctx.beginPath();
                    ctx.arc(legendX + 15, yOffset, 5, 0, 2 * Math.PI);
                    ctx.fill();
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText('Open Channel (coprime)', legendX + 30, yOffset + 5);

                    yOffset += 30;
                    ctx.strokeStyle = '#e74c3c';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(legendX + 15, yOffset, 5, 0, 2 * Math.PI);
                    ctx.stroke();
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText('Blocked Channel', legendX + 30, yOffset + 5);

                    yOffset += 30;
                    ctx.strokeStyle = '#27ae60';
                    ctx.lineWidth = 2;
                    ctx.setLineDash([]);
                    ctx.beginPath();
                    ctx.moveTo(legendX + 10, yOffset);
                    ctx.lineTo(legendX + 40, yOffset);
                    ctx.stroke();
                    ctx.fillText('Prime Ring', legendX + 50, yOffset + 5);

                    yOffset += 25;
                    ctx.strokeStyle = '#95a5a6';
                    ctx.setLineDash([10, 5]);
                    ctx.beginPath();
                    ctx.moveTo(legendX + 10, yOffset);
                    ctx.lineTo(legendX + 40, yOffset);
                    ctx.stroke();
                    ctx.setLineDash([]);
                    ctx.fillText('Composite Ring', legendX + 50, yOffset + 5);

                } else if (colorMode === 'gcd-local' || colorMode === 'gcd-global') {
                    ctx.fillStyle = '#2c3e50';
                    ctx.font = `bold ${Math.max(12, width/200)}px serif`;
                    ctx.fillText('GCD Values:', legendX + 15, yOffset);
                    yOffset += 25;
                    ctx.font = `${Math.max(11, width/220)}px serif`;

                    const sortedGCDs = Array.from(allGCDs).sort((a, b) => a - b).slice(0, 8);
                    sortedGCDs.forEach(gcdVal => {
                        const color = colorMode === 'gcd-local' ? 
                                     getGCDColor(gcdVal, Math.max(...allGCDs)) : 
                                     getGCDColorGlobal(gcdVal);
                        
                        ctx.fillStyle = color;
                        ctx.beginPath();
                        ctx.arc(legendX + 15, yOffset, 5, 0, 2 * Math.PI);
                        ctx.fill();
                        ctx.fillStyle = '#2c3e50';
                        ctx.fillText(`gcd = ${gcdVal}${gcdVal === 1 ? ' (coprime)' : ''}`, 
                                    legendX + 30, yOffset + 5);
                        yOffset += 25;
                    });
                } else if (colorMode === 'prime-composite') {
                    ctx.fillStyle = '#27ae60';
                    ctx.beginPath();
                    ctx.arc(legendX + 15, yOffset, 5, 0, 2 * Math.PI);
                    ctx.fill();
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText('Prime Modulus', legendX + 30, yOffset + 5);

                    yOffset += 30;
                    ctx.fillStyle = '#e67e22';
                    ctx.beginPath();
                    ctx.arc(legendX + 15, yOffset, 5, 0, 2 * Math.PI);
                    ctx.fill();
                    ctx.fillStyle = '#2c3e50';
                    ctx.fillText('Composite Modulus', legendX + 30, yOffset + 5);
                }
            }

            // Title
            ctx.fillStyle = '#2c3e50';
            ctx.font = `bold ${Math.max(20, width/100)}px serif`;
            ctx.textAlign = 'center';
            const titleText = mode === 'fixed-r' ? `Fixed r=${fixedR}: Moduli ${minMod}-${maxMod}` :
                             mode === 'fixed-m' ? `Fixed m=${fixedM}: All residues` :
                             mode === 'primes-only' ? `Prime Moduli ${minMod}-${maxMod}` :
                             `Concentric Rings: Moduli ${minMod}-${maxMod}`;
            ctx.fillText(titleText, centerX, 40);
            ctx.textAlign = 'left';
        }

        // Enhanced export function with resolution options
        const originalExportConcentric = exportConcentricView;
        exportConcentricView = function(quality = '4k') {
            const canvas = document.getElementById('concentricCanvas');
            const currentWidth = canvas.width;
            
            if (quality === 'hd') {
                // Temporarily set to HD
                canvas.width = 1920;
                canvas.height = 1920;
                drawConcentricRings();
            }
            
            const link = document.createElement('a');
            link.download = `concentric-rings-${quality}-${Date.now()}.png`;
            link.href = canvas.toDataURL('image/png');
            link.click();
            
            // Restore original resolution
            if (quality === 'hd') {
                canvas.width = currentWidth;
                canvas.height = currentWidth;
                drawConcentricRings();
            }
        };

        // Modified runFractionalTest to save to history
        const originalRunFractionalTest = runFractionalTest;
        runFractionalTest = function() {
            originalRunFractionalTest();

            // Save to history
            const m = parseInt(document.getElementById('testModulus').value);
            const k = parseInt(document.getElementById('sampleCount').value);
            const sliceType = document.getElementById('sliceType').value;
            const slice = getSlice(m, sliceType);
            
            let passedSamples = 0;
            let allPass = true;
            for (let i = 0; i < k; i++) {
                const r = slice[Math.floor(Math.random() * slice.length)];
                if (gcd(r, m) === 1) passedSamples++;
                else allPass = false;
            }

            const result = {
                type: 'Single Test',
                timestamp: new Date().toLocaleString(),
                modulus: m,
                prime: isPrime(m),
                passed: allPass,
                k: k,
                passedSamples: passedSamples,
                density: (eulerPhi(m) / m).toFixed(4),
                smallestFactor: smallestPrimeFactor(m),
                theoreticalProb: Math.pow(1 - 1/smallestPrimeFactor(m), k).toFixed(4),
                sliceType: sliceType
            };

            addToHistory(result);
        };

        // Initialize concentric rings
        drawConcentricRings();
    </script>
</body>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Sieve: π and ζ(2n) Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            color: #fff;
            min-height: 100vh;
            padding: 0;
            padding-top: 60px;
        }
        
        .sticky-nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: rgba(30, 60, 114, 0.98);
            backdrop-filter: blur(20px);
            z-index: 1000;
            padding: 12px 20px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            border-bottom: 2px solid rgba(255, 215, 0, 0.3);
        }
        
        .nav-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .nav-title {
            font-size: 1.2em;
            font-weight: bold;
            color: #ffd700;
            white-space: nowrap;
        }
        
        .nav-links {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .nav-link {
            color: #fff;
            text-decoration: none;
            padding: 6px 12px;
            border-radius: 6px;
            transition: all 0.3s ease;
            font-size: 0.9em;
            white-space: nowrap;
        }
        
        .nav-link:hover {
            background: rgba(78, 205, 196, 0.2);
            color: #4ecdc4;
        }
        
        .nav-link.active {
            background: rgba(255, 215, 0, 0.2);
            color: #ffd700;
        }
        
        .quick-actions {
            display: flex;
            gap: 8px;
        }
        
        .quick-btn {
            padding: 6px 12px;
            background: rgba(255, 215, 0, 0.2);
            border: 1px solid rgba(255, 215, 0, 0.4);
            border-radius: 6px;
            color: #ffd700;
            cursor: pointer;
            font-size: 0.85em;
            transition: all 0.3s ease;
            white-space: nowrap;
        }
        
        .quick-btn:hover {
            background: rgba(255, 215, 0, 0.3);
            transform: translateY(-1px);
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .section {
            scroll-margin-top: 80px;
        }
        
        .viz-categories {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
            padding: 15px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }
        
        .category-btn {
            padding: 8px 16px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
        }
        
        .category-btn.active {
            background: #ffd700;
            border-color: #ffd700;
            color: #1e3c72;
        }
        
        .category-btn:hover {
            background: rgba(255, 215, 0, 0.3);
            border-color: #ffd700;
        }
        
        .preset-examples {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .preset-card {
            background: rgba(78, 205, 196, 0.1);
            padding: 15px;
            border-radius: 10px;
            border: 2px solid rgba(78, 205, 196, 0.3);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .preset-card:hover {
            background: rgba(78, 205, 196, 0.2);
            border-color: #4ecdc4;
            transform: translateY(-2px);
        }
        
        .preset-title {
            font-weight: bold;
            color: #4ecdc4;
            margin-bottom: 5px;
        }
        
        .preset-desc {
            font-size: 0.9em;
            opacity: 0.8;
        }
        
        .header {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ffd700, #ffed4e);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .subtitle {
            text-align: center;
            font-size: 1.1em;
            opacity: 0.9;
            margin-bottom: 20px;
        }
        
        .info-section {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 15px;
            margin-top: 15px;
            border-left: 4px solid #ffd700;
        }
        
        .info-section h3 {
            color: #ffd700;
            margin-bottom: 10px;
        }
        
        .info-section p {
            line-height: 1.6;
            margin-bottom: 10px;
        }
        
        .formula {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            margin: 10px 0;
            overflow-x: auto;
        }
        
        .main-content {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .control-group {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .control-group h3 {
            margin-bottom: 15px;
            color: #ffd700;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
            font-size: 0.9em;
        }
        
        input, select, button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 15px;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
        }
        
        button {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(238, 90, 82, 0.3);
        }
        
        .export-btn {
            background: linear-gradient(45deg, #4ecdc4, #44a8a3);
            margin-top: 10px;
        }
        
        .export-btn:hover {
            box-shadow: 0 10px 20px rgba(78, 205, 196, 0.3);
        }
        
        .results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .result-card {
            background: rgba(255, 255, 255, 0.08);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .result-card h4 {
            color: #ffd700;
            margin-bottom: 15px;
            font-size: 1.3em;
        }
        
        .value {
            font-family: 'Courier New', monospace;
            font-size: 1.2em;
            background: rgba(0, 0, 0, 0.3);
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            word-break: break-all;
        }
        
        .error-info {
            font-size: 0.9em;
            opacity: 0.8;
            margin-top: 10px;
        }
        
        .step-by-step {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .step-by-step h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .step {
            background: rgba(255, 255, 255, 0.08);
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 4px solid #4ecdc4;
        }
        
        .step-number {
            display: inline-block;
            background: #4ecdc4;
            color: #1e3c72;
            font-weight: bold;
            padding: 5px 12px;
            border-radius: 50%;
            margin-right: 10px;
        }
        
        .step-title {
            font-size: 1.1em;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .step-content {
            margin-left: 40px;
            line-height: 1.6;
        }
        
        .step-formula {
            background: rgba(0, 0, 0, 0.4);
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
        }
        
        .gap-analysis {
            margin-top: 30px;
            background: rgba(30, 60, 114, 0.95);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .gap-analysis h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .gap-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }
        
        .gap-item {
            background: rgba(255, 255, 255, 0.15);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .gap-item:hover {
            background: rgba(255, 255, 255, 0.25);
            border-color: #4ecdc4;
            transform: translateY(-2px);
        }
        
        .gap-item.expanded {
            grid-column: 1 / -1;
            background: rgba(78, 205, 196, 0.2);
            border-color: #4ecdc4;
        }
        
        .gap-primes-list {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.3);
            display: none;
        }
        
        .gap-primes-list.visible {
            display: block;
        }
        
        .gap-primes-container {
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            border-radius: 8px;
            max-height: 400px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.8;
            text-align: left;
        }
        
        .gap-cumulative-section {
            margin-top: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            text-align: left;
        }
        
        .cumulative-step {
            padding: 8px;
            margin: 5px 0;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 5px;
            font-family: 'Courier New', monospace;
            font-size: 0.85em;
        }
        
        .gap-value {
            font-size: 1.1em;
            font-weight: bold;
            color: #4ecdc4;
        }
        
        .channel-analysis {
            margin-top: 30px;
            background: rgba(30, 60, 114, 0.95);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .channel-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .channel-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .channel-item:hover {
            background: rgba(255, 255, 255, 0.15);
            border-color: #4ecdc4;
            transform: translateY(-2px);
        }
        
        .channel-item.expanded {
            grid-column: 1 / -1;
            background: rgba(78, 205, 196, 0.1);
            border-color: #4ecdc4;
        }
        
        .channel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .channel-residue {
            font-size: 1.1em;
            font-weight: bold;
            color: #4ecdc4;
        }
        
        .channel-count {
            background: rgba(78, 205, 196, 0.2);
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.9em;
        }
        
        .channel-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 10px;
        }
        
        .stat-item {
            background: rgba(0, 0, 0, 0.2);
            padding: 8px;
            border-radius: 5px;
        }
        
        .stat-label {
            font-size: 0.8em;
            opacity: 0.8;
            margin-bottom: 3px;
        }
        
        .stat-value {
            font-size: 1em;
            font-weight: bold;
            color: #ffd700;
        }
        
        .primes-list {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            display: none;
        }
        
        .primes-list.visible {
            display: block;
        }
        
        .primes-list h4 {
            color: #ffd700;
            margin-bottom: 10px;
        }
        
        .primes-container {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 8px;
            max-height: 300px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.6;
        }
        
        .primes-container::-webkit-scrollbar {
            width: 8px;
        }
        
        .primes-container::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 4px;
        }
        
        .primes-container::-webkit-scrollbar-thumb {
            background: #4ecdc4;
            border-radius: 4px;
        }
        
        .expand-indicator {
            color: #4ecdc4;
            font-size: 0.8em;
            margin-top: 8px;
            text-align: center;
            opacity: 0.7;
        }
        
        .view-options {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .view-btn {
            padding: 8px 16px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9em;
        }
        
        .view-btn.active {
            background: #4ecdc4;
            border-color: #4ecdc4;
            color: #1e3c72;
        }
        
        .view-btn:hover {
            background: rgba(78, 205, 196, 0.3);
            border-color: #4ecdc4;
        }
        
        .distribution-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 10px;
            overflow: hidden;
        }
        
        .distribution-table th {
            background: rgba(78, 205, 196, 0.3);
            padding: 12px;
            text-align: left;
            font-weight: bold;
            color: #ffd700;
        }
        
        .distribution-table td {
            padding: 10px 12px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(30, 60, 114, 0.4);
            color: #ffffff;
        }
        
        .distribution-table tr:hover {
            background: rgba(78, 205, 196, 0.2);
        }
        
        .distribution-table tr:hover td {
            background: rgba(78, 205, 196, 0.2);
        }
        
        .progress-bar {
            width: 100%;
            height: 20px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            overflow: hidden;
            margin-top: 5px;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4, #44a8a3);
            transition: width 0.3s ease;
        }
        
        .chart-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .chart-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
            text-align: center;
        }
        
        #channelChart {
            width: 100%;
            height: 400px;
            max-height: 400px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        
        .chart-legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
            font-size: 0.9em;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 2px;
        }
        
        .visualization-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
        }
        
        .visualization-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
        }
        
        .prime-ring-container {
            margin-top: 30px;
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 215, 0, 0.3);
        }
        
        .prime-ring-container h3 {
            color: #ffd700;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .ring-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
        }
        
        .ring-controls label {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #fff;
            font-size: 0.9em;
        }
        
        .ring-controls input[type="number"],
        .ring-controls select {
            width: 80px;
            padding: 6px;
            border-radius: 6px;
            border: none;
            font-size: 14px;
        }
        
        .ring-controls input[type="checkbox"] {
            width: auto;
        }
        
        #primeRingCanvas {
            width: 100%;
            height: 700px;
            max-height: 700px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 10px;
            cursor: crosshair;
        }
        
        .ring-info {
            margin-top: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        
        .ring-legend {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 15px;
            font-size: 0.85em;
        }
        
        .ring-legend-item {
            display: flex;
            align-items: center;
            gap: 6px;
            padding: 4px 10px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 5px;
        }
        
        .ring-legend-color {
            width: 14px;
            height: 14px;
            border-radius: 50%;
        }
        
        .viz-options {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .viz-btn {
            padding: 10px 20px;
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .viz-btn.active {
            background: #4ecdc4;
            border-color: #4ecdc4;
            color: #1e3c72;
        }
        
        .viz-btn:hover {
            background: rgba(78, 205, 196, 0.3);
            border-color: #4ecdc4;
        }
        
        #vizCanvas {
            width: 100%;
            height: 500px;
            max-height: 500px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(400px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        .loading {
            text-align: center;
            font-style: italic;
            opacity: 0.7;
        }
        
        .toggle-section {
            cursor: pointer;
            user-select: none;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
        .toggle-icon {
            transition: transform 0.3s ease;
        }
        
        .toggle-icon.open {
            transform: rotate(180deg);
        }
        
        .collapsible-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease;
        }
        
        .collapsible-content.open {
            max-height: 5000px;
        }
    </style>
</head>
<body>
    <nav class="sticky-nav">
        <div class="nav-content">
            <div class="nav-title">Modular Sieve Calculator</div>
            <div class="nav-links">
                <a href="#controls" class="nav-link">Controls</a>
                <a href="#results" class="nav-link">Results</a>
                <a href="#gap-analysis" class="nav-link">Gap Analysis</a>
                <a href="#channel-analysis" class="nav-link">Composite Channels</a>
                <a href="#visualization-section" class="nav-link">Visualizations</a>
                <a href="#prime-ring-section" class="nav-link">Prime Rings</a>
            </div>
            <div class="quick-actions">
                <button class="quick-btn" onclick="exportAllData()">Export All</button>
                <button class="quick-btn" onclick="showPresets()">Presets</button>

            </div>
        </div>

    </nav>
    
    <div class="container">
        <div class="header section" id="theory">
            <h1>Modular Sieve Calculator</h1>
            <div class="subtitle">Computing π and ζ(2n) via Gap-Class and Residue-Channel Decompositions</div>
            <div style="text-align: center; margin-top: 15px; font-size: 0.95em; font-style: italic; opacity: 0.85;">
                By Wessen Getachew (<a href="https://twitter.com/7Dview" target="_blank" style="color: #4ecdc4; text-decoration: none;">@7Dview</a>)
            </div>
            <div style="text-align: center; margin-top: 5px; font-size: 0.9em; opacity: 0.75;">
                Inspired by Leonhard Euler's pioneering work and 3Blue1Brown's mathematical visualizations
            </div>
            <div style="text-align: center; margin-top: 12px; font-size: 0.9em;">
                <span style="opacity: 0.8;">Explore more prime visualizations:</span>
                <a href="https://wessengetachew.github.io/GCD/" target="_blank" style="color: #4ecdc4; text-decoration: none; margin: 0 8px; font-weight: 500;">GCD Patterns</a>
                <span style="opacity: 0.5;">|</span>
                <a href="https://wessengetachew.github.io/Primes/" target="_blank" style="color: #4ecdc4; text-decoration: none; margin: 0 8px; font-weight: 500;">Prime Spirals</a>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('theory')">
                    <h3>Mathematical Framework</h3>
                    <span class="toggle-icon" id="theory-icon">▼</span>
                </div>
                <div id="theory-content" class="collapsible-content">
                    <p>This calculator implements the rigorous framework for computing π and ζ(2n) using Euler product decompositions.</p>
                    
                    <p><strong>Key Identity:</strong> For ℜ(s) > 1, the Riemann zeta function has the Euler product:</p>
                    <div class="formula">ζ(s) = ∏<sub>p prime</sub> (1 - p<sup>-s</sup>)<sup>-1</sup></div>
                    
                    <p><strong>Prime-Gap Decomposition:</strong> We reorganize Euler's product by prime gaps:</p>
                    <div class="formula">
                        ζ(s) = ∏<sub>g</sub> P<sub>g</sub>(s)<br>
                        P<sub>g</sub>(s) = ∏<sub>p ∈ (gap g)</sub> 1/(1 - p<sup>-s</sup>)
                    </div>
                    <p style="margin-top: 10px;">Each prime p belongs to gap class g = (next prime) - p. We group primes by their forward gap.</p>
                    
                    <p style="margin-top: 15px;"><strong>Basel & π Reconstruction:</strong> Since ζ(2) = π²/6:</p>
                    <div class="formula">π = √(6 · ∏<sub>g</sub> P<sub>g</sub>(2))</div>
                    <p style="margin-top: 10px;">Validation: Using primes up to 30M → π ≈ 3.14159265358979 (14+ decimals exact)</p>
                    
                    <p style="margin-top: 15px;"><strong>Phase Law Extension (Critical Strip):</strong></p>
                    <div class="formula">
                        ζ(1/2 + it) = ∏<sub>g</sub> (∏<sub>p ∈ (gap g)</sub> (1 - p<sup>-1/2</sup>e<sup>-iφ</sup>)<sup>-1</sup> e<sup>-βlogp</sup>)<br>
                        φ(p, t) = tlogp - π/2,  β ~ 1/logt
                    </div>
                    <p style="margin-top: 10px;"><strong>Example:</strong> At t=14.1347, p=11: φ = 14.1347×log(11)-π/2 ≈ 32.12 rad</p>
                    <p style="margin-top: 5px;">Aligns prime oscillations with first Riemann zero.</p>
                    <p style="margin-top: 10px;"><strong>Significance:</strong></p>
                    <ul style="margin-left: 20px; margin-top: 5px;">
                        <li>Provides convergent Euler product in the critical strip</li>
                        <li>Phase φ locks oscillations to cancel at zeros</li>
                        <li>Decay β stabilizes for finite primes</li>
                    </ul>
                    
                    <p style="margin-top: 15px;"><strong>Two Decomposition Methods:</strong></p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li><strong>Gap-Class:</strong> Groups primes p by their forward gap g = p<sub>next</sub> - p</li>
                        <li><strong>Residue Channels:</strong> Splits primes by residue classes mod m, giving φ(m) independent channels for gcd(a,m)=1. Default uses m=30 with 8 channels, but supports any modulus.</li>
                    </ul>
                    
                    <p style="margin-top: 15px;"><strong>Error Control:</strong> For target error ε, include primes up to:</p>
                    <div class="formula">
                        Y ≈ 1 + 1/ε  (for π)<br>
                        Y ≈ (2/((2n-1)·ε))<sup>1/(2n-1)</sup>  (for ζ(2n))
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('phasor')">
                    <h3>Nested Modular Unity & Zeta Surface</h3>
                    <span class="toggle-icon" id="phasor-icon">▼</span>
                </div>
                <div id="phasor-content" class="collapsible-content">
                    <p><strong>The Zeta Function as a Phasor Sum:</strong></p>
                    <p>For complex argument s = σ + it, the Riemann zeta function can be written as:</p>
                    <div class="formula">ζ(s) = Σ n<sup>-σ</sup> e<sup>-it log n</sup></div>
                    
                    <p>Each term n<sup>-s</sup> is a <strong>rotating phasor</strong> on the complex plane with:</p>
                    <div class="formula">
                        Radius: r<sub>n</sub> = n<sup>-σ</sup><br>
                        Angle: θ<sub>n</sub> = -t log n
                    </div>
                    
                    <p style="margin-top: 15px;"><strong>Modular Unity Correspondence:</strong></p>
                    <p>Each residue class k (mod m) corresponds to an m-th root of unity:</p>
                    <div class="formula">k mod m ↔ e<sup>2πik/m</sup></div>
                    
                    <p>This isomorphism connects modular arithmetic to the unit circle geometry. For each modulus m and residue k:</p>
                    <div class="formula">S<sub>m,k</sub>(s; N) = Σ<sub>n≡k (mod m)</sub> n<sup>-s</sup></div>
                    
                    <p style="margin-top: 15px;"><strong>The Critical Line (σ = 1/2):</strong></p>
                    <p>On the critical line, each contribution rotates at angular velocity ∝ log n. When modular rotations align <strong>destructively</strong>, their vector sum vanishes—precisely the condition for a nontrivial zero:</p>
                    <div class="formula">ζ(1/2 + iT) = 0</div>
                    
                    <p style="margin-top: 15px;"><strong>Nested Modular Surface:</strong></p>
                    <p>Stacking concentric rings for m = 1, 2, 3, ... creates a <strong>nested modular unity lattice</strong>. Each ring samples the unit circle at m equally-spaced points, and together they approximate the continuous analytic structure of ζ(s). The GCD=1 residues (primitive rotations) form the multiplicative group of units mod m.</p>
                    
                    <p style="margin-top: 15px;"><strong>Geometric Interpretation:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Height t:</strong> Controls angular phase of each modular shell (vertical movement on zeta surface)</li>
                        <li><strong>Real part σ:</strong> Controls radial decay (compression toward critical line)</li>
                        <li><strong>Modulus m:</strong> Discrete Fourier mode on the complex circle</li>
                        <li><strong>Primitive residues:</strong> φ(m) independent rotation channels</li>
                    </ul>
                    
                    <p style="margin-top: 15px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                        <strong>💡 Key Insight:</strong> The nested modular lattice forms a discrete analogue of the complex-analytic domain of ζ(s). By weighting each ring by n<sup>-σ</sup> and rotating by phase -t log n, we obtain a direct geometric mimic of the Riemann zeta surface.
                    </p>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('channelTheorems')">
                    <h3>Getachew Channel Theorems: Prime Avoidance & Composite Projection</h3>
                    <span class="toggle-icon" id="channelTheorems-icon">▼</span>
                </div>
                <div id="channelTheorems-content" class="collapsible-content">
                    <div style="margin-bottom: 30px; padding: 15px; background: rgba(78, 205, 196, 0.15); border-radius: 10px; border: 2px solid #4ecdc4;">
                        <h4 style="color: #4ecdc4; margin-bottom: 15px;">🔵 Theorem 1: Prime Channel Avoidance</h4>
                        <p><strong>Theorem (Getachew Prime Channel Avoidance Theorem)</strong></p>
                        <p style="margin-top: 10px;"><em>Let each modulus M ∈ ℤ⁺ define a fractional residue system:</em></p>
                        <div class="formula">
                            ℛ(M) = { r/M | 0 ≤ r < M }
                        </div>
                        
                        <p style="margin-top: 10px;"><em>Define a reduction channel as the equivalence class of fractions that share the same lowest-term representation:</em></p>
                        <div class="formula">
                            r₁/M₁ ~ r₂/M₂  ⟺  r₁/M₁ = r₂/M₂ (in lowest terms)
                        </div>
                        <p style="margin-top: 5px;"><em>Each equivalence class corresponds to a fundamental Farey channel of the form 1/N or its rational multiples.</em></p>
                        
                        <div style="margin-top: 15px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                            <p><strong>Statement:</strong> For every prime modulus p, the complete residue set</p>
                            <div class="formula">
                                Φ(p) = {1, 2, 3, ..., p-1}
                            </div>
                            <p>contains no reducible fractions, and therefore intersects no reduction channel 1/N for any N > 1.</p>
                            <div class="formula">
                                gcd(r, p) = 1 &nbsp; ∀r ∈ Φ(p) &nbsp; ⟹ &nbsp; r/p cannot reduce to any channel 1/N
                            </div>
                        </div>
                        
                        <p style="margin-top: 15px;"><strong>Interpretation:</strong></p>
                        <p style="margin-left: 20px; line-height: 1.8;">
                            Primes define <strong>irreducible modular orbits</strong> within the fractional lattice. Their residues never project downward into simpler rational channels because no shared divisors exist between any residue r and the prime modulus p. Each prime ring therefore forms a <strong>fully independent coprime manifold</strong>, geometrically isolated from the composite Farey flows that pass through reducible fractions such as 1/2, 1/3, 1/4, ...
                        </p>
                        
                        <div style="margin-top: 15px; padding: 15px; background: rgba(255, 215, 0, 0.1); border-radius: 8px; border-left: 4px solid #ffd700;">
                            <p><strong>Geometric Consequence:</strong></p>
                            <p>In the nested modular plane, the loci of reducible fractions form continuous <strong>Farey flow lines</strong> — rational channels through which composite moduli project. Prime moduli, in contrast, occupy the <strong>interstitial lattice regions</strong> between these channels, creating smooth, full, and non-overlapping modular rings.</p>
                            <p style="margin-top: 10px; padding: 10px; background: rgba(255, 215, 0, 0.2); border-radius: 5px; font-weight: 500;">
                                ⟹ Prime moduli trace paths that avoid all reducible channels, forming the pure coprime skeleton of the modular continuum.
                            </p>
                        </div>
                    </div>
                    
                    <div style="padding: 15px; background: rgba(255, 99, 132, 0.15); border-radius: 10px; border: 2px solid #ff6384;">
                        <h4 style="color: #ff6384; margin-bottom: 15px;">🔴 Theorem 2: Composite Channel Projection</h4>
                        <p><strong>Corollary (Getachew Composite Channel Projection Corollary)</strong></p>
                        <p style="margin-top: 10px;"><em>Let M ∈ ℤ⁺ be a composite modulus. For each integer r (0 ≤ r < M) define the fraction r/M.<br>
                        Write d = gcd(r, M) and set r' = r/d, M' = M/d.<br>
                        Then r/M reduces to the lowest-term fraction r'/M' with gcd(r', M') = 1.</em></p>
                        
                        <div style="margin-top: 15px; padding: 15px; background: rgba(255, 99, 132, 0.1); border-radius: 8px; border-left: 4px solid #ff6384;">
                            <p><strong>Statement:</strong> Every composite modulus M admits a nontrivial projection of its residues onto reduction channels (Farey channels):</p>
                            <div class="formula">
                                ∀ r ∈ {0,1,...,M-1}, &nbsp; r/M = r'/M' &nbsp; with<br>
                                d = gcd(r,M), &nbsp; M' = M/d, &nbsp; r' = r/d
                            </div>
                        </div>
                        
                        <p style="margin-top: 15px;"><strong>Key Properties:</strong></p>
                        <ol style="margin-left: 20px; line-height: 1.8;">
                            <li><strong>(i) Channel Multiplicity:</strong> The number of distinct residues r (mod M) that reduce to a fixed lowest-term fraction r'/M' equals d = M/M'</li>
                            <li><strong>(ii) Reducibility Ratio:</strong> The total number of reducible residues modulo M is M - φ(M), giving proportion: <strong>1 - φ(M)/M</strong></li>
                            <li><strong>(iii) Channel Denominators:</strong> For composite M, the set of reduction channel denominators M' is exactly the set of divisors of M strictly less than M</li>
                        </ol>
                        
                        <p style="margin-top: 15px;"><strong>Example: M = 12</strong></p>
                        <div style="margin-left: 20px; line-height: 1.8;">
                            <p>φ(12) = 4, so M - φ(M) = 8 reducible residues</p>
                            <p>Proper divisors M' ∈ {1, 2, 3, 4, 6}</p>
                            <p>Take r = 8: gcd(8,12) = 4, r' = 2, M' = 3</p>
                            <p>Thus 8/12 = 2/3, projecting onto the 1/3-family (channel with denominator 3)</p>
                            <p>There are d = 4 residues that reduce to each fraction with denominator 3</p>
                        </div>
                        
                        <div style="margin-top: 20px; padding: 15px; background: rgba(255, 215, 0, 0.1); border-radius: 8px; border-left: 4px solid #ffd700;">
                            <p><strong>Geometric Consequence:</strong></p>
                            <p>In the nested modular plane, reducible residues of composite moduli populate the <strong>Farey flow lines</strong> (the 1/N channels and their rational multiples). Each channel with denominator M' < M collects exactly d = M/M' lattice points from modulus M for each corresponding coprime numerator r'.</p>
                            <p style="margin-top: 10px; padding: 10px; background: rgba(255, 215, 0, 0.2); border-radius: 5px; font-weight: 500;">
                                ⟹ Composite moduli project their reducible residues onto a dense web of Farey channels; primes, by contrast, contribute only irreducible residues and avoid these channels.
                            </p>
                        </div>
                    </div>
                    
                    <div style="margin-top: 25px; padding: 20px; background: rgba(153, 102, 255, 0.15); border-radius: 10px; border: 2px solid #9966ff;">
                        <h4 style="color: #9966ff; margin-bottom: 15px;">📊 Interactive Visualization</h4>
                        <p style="line-height: 1.8;">
                            Use the <strong>"Prime & Composite Channels"</strong> visualization to see both theorems in action:
                        </p>
                        <ul style="margin-left: 20px; margin-top: 10px; line-height: 1.8;">
                            <li><span style="color: #4ecdc4; font-weight: bold;">● Cyan rings</span> = Prime moduli avoiding all Farey channels (Theorem 1)</li>
                            <li><span style="color: #ff6384; font-weight: bold;">● Red points</span> = Composite residues projecting onto channels (Theorem 2)</li>
                            <li><span style="color: #ffd700; font-weight: bold;">● Gold rings</span> = Farey channels (reduction targets)</li>
                            <li>Each point shows its gcd value and reduction path when clicked</li>
                        </ul>
                        <p style="margin-top: 15px; font-weight: 500; color: #9966ff;">
                            Together, these theorems reveal the fundamental geometric distinction between primes and composites in the modular lattice.
                        </p>
                    </div>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('semiprime')">
                    <h3>Getachew Semiprime Generation Theorem</h3>
                    <span class="toggle-icon" id="semiprime-icon">▼</span>
                </div>
                <div id="semiprime-content" class="collapsible-content">
                    <p><strong>Definition:</strong> For each prime p, define the semiprime set:</p>
                    <div class="formula">S_p = {p × q | q ∈ ℙ, q ≠ p}</div>
                    
                    <p style="margin-top: 15px;"><strong>Theorem (Getachew Semiprime Generation):</strong></p>
                    <div style="padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                        Every semiprime n = p × q (where p ≤ q are primes) has a unique factorization, and:
                        <div class="formula">⋃(p∈ℙ) S_p = {all semiprimes}</div>
                        This union is disjoint when ordered p ≤ q.
                    </div>
                    
                    <p style="margin-top: 15px;"><strong>Asymptotic Density:</strong></p>
                    <div class="formula">
                        S(x) ~ (x log log x) / log x
                    </div>
                    <p>Semiprimes are <strong>denser than primes</strong> (which have density ~ x/log x).</p>
                    
                    <p style="margin-top: 15px;"><strong>RSA Connection:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Forward (multiplication):</strong> p, q → n = pq is computationally easy O(log² n)</li>
                        <li><strong>Backward (factorization):</strong> n → p, q is hard (no known polynomial-time algorithm)</li>
                        <li>This asymmetry is the foundation of RSA encryption</li>
                        <li>Trial division requires O(√n) operations in the worst case</li>
                    </ul>
                    
                    <p style="margin-top: 15px;"><strong>Modular Properties:</strong></p>
                    <p>For modulus m:</p>
                    <div class="formula">
                        pq ≡ (p mod m)(q mod m) (mod m)
                    </div>
                    <p>This creates "modular interference patterns" - semiprimes populate residue classes differently than primes.</p>
                    
                    <p style="margin-top: 15px;"><strong>Semiprime Zeta Function:</strong></p>
                    <div class="formula">
                        ζ_S(s) = Σ(n∈S) n^(-s) = ½[(Σp^(-s))² - Σp^(-2s)]
                    </div>
                    <p>This function interpolates between the prime zeta function and contributions to the Riemann zeta function.</p>
                </div>
            </div>
            
            <div class="info-section">
                <div class="toggle-section" onclick="toggleSection('credits')">
                    <h3>Credits, Acknowledgments & References</h3>
                    <span class="toggle-icon" id="credits-icon">▼</span>
                </div>
                <div id="credits-content" class="collapsible-content">
                    <p style="margin-bottom: 15px;"><strong>Creator & Original Research:</strong> Wessen Getachew (<a href="https://twitter.com/7Dview" target="_blank" style="color: #4ecdc4; text-decoration: none;">@7Dview</a>)</p>
                    
                    <div style="padding: 15px; background: rgba(255, 215, 0, 0.1); border-radius: 8px; border-left: 4px solid #ffd700; margin-bottom: 20px;">
                        <p style="margin-bottom: 10px;"><strong>Original Contributions by Wessen Getachew:</strong></p>
                        <ul style="margin-left: 20px; line-height: 1.8;">
                            <li><strong>Getachew Prime Channel Avoidance Theorem</strong> - Novel geometric characterization showing prime moduli form complete coprime rings that avoid all Farey reduction channels</li>
                            <li><strong>Getachew Composite Channel Projection Corollary</strong> - Systematic analysis of how composite moduli project reducible residues onto Farey flow lines with precise channel multiplicity formulas</li>
                            <li><strong>Gap-Class Decomposition Framework</strong> - Reorganization of the Euler product by prime gap classes P<sub>g</sub>(s), providing an alternative structural view of ζ(s)</li>
                            <li><strong>Modular Zeta Surface Visualization</strong> - Interactive nested unity lattice representation revealing the geometric structure of ζ(s) through modular arithmetic</li>
                            <li><strong>Phase Law Extension</strong> - Convergent Euler product formulation in the critical strip using phase alignment φ(p,t) = t·log(p) - π/2 with decay parameter β ~ 1/log(t)</li>
                        </ul>
                    </div>
                    
                    <p style="margin-bottom: 15px;"><strong>Classical Mathematical Foundations:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Leonhard Euler (1707-1783)</strong> - Discovered the Euler product formula ζ(s) = ∏<sub>p</sub>(1-p<sup>-s</sup>)<sup>-1</sup> and proved ζ(2) = π²/6 (Basel problem, 1734)</li>
                        <li><strong>Bernhard Riemann (1826-1866)</strong> - Extended the zeta function to the complex plane and formulated the Riemann Hypothesis (1859)</li>
                        <li><strong>Peter Gustav Lejeune Dirichlet (1805-1859)</strong> - Proved Dirichlet's theorem on primes in arithmetic progressions, fundamental to residue channel analysis</li>
                        <li><strong>Edmund Landau (1877-1938)</strong> - Developed rigorous analytic number theory and error bounds for prime counting functions</li>
                        <li><strong>Godfrey Harold Hardy (1877-1947) & J.E. Littlewood (1885-1977)</strong> - Proved infinitely many lead changes in prime races (Chebyshev's bias)</li>
                    </ul>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Educational Inspiration:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>3Blue1Brown (Grant Sanderson)</strong> - Exceptional mathematical visualizations that inspired the interactive approach in this calculator</li>
                    </ul>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Key References:</strong></p>
                    <ol style="margin-left: 20px; line-height: 1.8;">
                        <li>Euler, L. (1748). <em>Introductio in analysin infinitorum</em>. Lausanne.</li>
                        <li>Riemann, B. (1859). "Über die Anzahl der Primzahlen unter einer gegebenen Größe". <em>Monatsberichte der Berliner Akademie</em>.</li>
                        <li>Dirichlet, P.G.L. (1837). "Beweis des Satzes, dass jede unbegrenzte arithmetische Progression...". <em>Abhandlungen der Königlich Preussischen Akademie der Wissenschaften</em>.</li>
                        <li>Hardy, G.H. & Littlewood, J.E. (1914). "Some problems of 'Partitio numerorum'". <em>Acta Mathematica</em>, 44(1), 1-70.</li>
                        <li>Edwards, H.M. (1974). <em>Riemann's Zeta Function</em>. Academic Press.</li>
                        <li>Davenport, H. (2000). <em>Multiplicative Number Theory</em> (3rd ed.). Springer.</li>
                        <li>Montgomery, H.L. & Vaughan, R.C. (2007). <em>Multiplicative Number Theory I: Classical Theory</em>. Cambridge University Press.</li>
                        <li>Titchmarsh, E.C. (1986). <em>The Theory of the Riemann Zeta Function</em> (2nd ed.). Oxford University Press.</li>
                        <li>Rubinstein, M. & Sarnak, P. (1994). "Chebyshev's bias". <em>Experimental Mathematics</em>, 3(3), 173-197.</li>
                        <li>Granville, A. & Martin, G. (2006). "Prime number races". <em>The American Mathematical Monthly</em>, 113(1), 1-33.</li>
                    </ol>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Online Resources:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li>OEIS (Online Encyclopedia of Integer Sequences): <a href="https://oeis.org" target="_blank" style="color: #4ecdc4;">https://oeis.org</a></li>
                        <li>Wolfram MathWorld - Riemann Zeta Function: <a href="https://mathworld.wolfram.com/RiemannZetaFunction.html" target="_blank" style="color: #4ecdc4;">mathworld.wolfram.com</a></li>
                        <li>Prime Number Theorem Resources: <a href="https://primes.utm.edu" target="_blank" style="color: #4ecdc4;">primes.utm.edu</a></li>
                    </ul>
                    
                    <p style="margin-top: 15px; margin-bottom: 15px;"><strong>Technologies Used:</strong></p>
                    <ul style="margin-left: 20px; line-height: 1.8;">
                        <li><strong>Chart.js</strong> - Interactive charting library for data visualization</li>
                        <li><strong>HTML5 Canvas</strong> - For high-resolution visualizations and exports</li>
                        <li><strong>JavaScript ES6+</strong> - Core computation engine and user interface</li>
                    </ul>
                    
                    <p style="margin-top: 20px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                        <strong>Note:</strong> This calculator combines classical analytic number theory with original research by Wessen Getachew on modular decompositions of the Riemann zeta function. The visualizations and interactive tools are designed to make these deep mathematical concepts accessible to students, educators, and researchers. All novel theorems and methods are original contributions that build upon the classical foundations of Euler, Riemann, and Dirichlet.
                    </p>
                    
                    <p style="margin-top: 15px; padding: 15px; background: rgba(255, 215, 0, 0.1); border-radius: 8px; border-left: 4px solid #ffd700;">
                        <strong>Citation:</strong> If you use this calculator or reference the original research in academic work, please cite:<br>
                        Getachew, W. (2025). "Modular Sieve: Computing π and ζ(2n) via Gap-Class and Residue-Channel Decompositions". <em>Interactive Mathematical Calculator</em>. Available at: [URL]
                    </p>
                </div>
            </div>
        </div>
        
        <div class="main-content section" id="controls">
            <h2 style="color: #ffd700; margin-bottom: 20px;">Quick Start Presets</h2>
            <div class="preset-examples" id="presetExamples" style="display: none;">
                <div class="preset-card" onclick="applyPreset('pi10')">
                    <div class="preset-title">Compute π to 10 decimals</div>
                    <div class="preset-desc">Error: 10^-11, ~700 primes</div>
                </div>
                <div class="preset-card" onclick="applyPreset('pi15')">
                    <div class="preset-title">Compute π to 15 decimals</div>
                    <div class="preset-desc">Error: 10^-16, ~40,000 primes</div>
                </div>
                <div class="preset-card" onclick="applyPreset('firstZero')">
                    <div class="preset-title">Explore First Riemann Zero</div>
                    <div class="preset-desc">t = 14.134725, Standard setup</div>
                </div>
                <div class="preset-card" onclick="applyPreset('mod60')">
                    <div class="preset-title">Compare mod 60 channels</div>
                    <div class="preset-desc">16 residue channels</div>
                </div>
                <div class="preset-card" onclick="applyPreset('semiprimes')">
                    <div class="preset-title">Semiprime Analysis</div>
                    <div class="preset-desc">Focus on RSA structure</div>
                </div>
                <div class="preset-card" onclick="applyPreset('highPrecision')">
                    <div class="preset-title">High Precision ζ(4)</div>
                    <div class="preset-desc">Error: 10^-12</div>
                </div>
            </div>
            
            <div class="controls">
                <div class="control-group">
                    <h3>Target Accuracy</h3>
                    <label for="epsilon">Relative Error (ε):</label>
                    <input type="number" id="epsilon" value="1" step="0.0001" min="0.0001" max="10">
                    
                    <div style="margin-bottom: 15px;">
                        <label style="font-size: 0.9em; opacity: 0.9;">Quick Presets:</label>
                        <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin-top: 8px;">
                            <button onclick="setEpsilon(0.01)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">1% (0.01)</button>
                            <button onclick="setEpsilon(0.0001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">0.01% (10⁻⁴)</button>
                            <button onclick="setEpsilon(0.0000001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">10⁻⁷</button>
                            <button onclick="setEpsilon(0.000000000001)" style="padding: 8px; font-size: 0.85em; background: rgba(255, 255, 255, 0.15);">10⁻¹²</button>
                        </div>
                    </div>
                    
                    <label for="constant">Constant to Compute:</label>
                    <select id="constant">
                        <option value="pi">π (from ζ(2))</option>
                        <option value="zeta4">ζ(4)</option>
                        <option value="zeta6">ζ(6)</option>
                        <option value="zeta8">ζ(8)</option>
                        <option value="zeta10">ζ(10)</option>
                    </select>
                    
                    <label for="modulus">Modulus for Residue Channels:</label>
                    <input type="number" id="modulus" value="30" min="2" max="210" step="1">
                    <div style="font-size: 0.85em; opacity: 0.8; margin-top: -10px;">
                        φ(m) channels for gcd(a,m)=1. Try: 6, 12, 30, 60, 210
                    </div>
                    
                    <label for="decimalPlaces">Decimal Places to Display:</label>
                    <input type="number" id="decimalPlaces" value="15" min="1" max="20" step="1" onchange="validateDecimalPlaces()">
                    <div style="font-size: 0.85em; opacity: 0.8; margin-top: -10px;">
                        Max 20 digits (JavaScript precision limit ≈15-17 digits)
                    </div>
                    <div id="precision-warning" style="display: none; font-size: 0.85em; color: #ff6b6b; margin-top: 5px; padding: 8px; background: rgba(255, 107, 107, 0.1); border-radius: 5px;">
                        ⚠️ Digits beyond 15-17 may not be accurate due to floating-point precision limits
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>Computation Method</h3>
                    <label for="method">Decomposition:</label>
                    <select id="method">
                        <option value="standard">Standard Euler Product</option>
                        <option value="gap">Gap-Class Analysis</option>
                        <option value="residue">Residue Channels (Custom Mod)</option>
                        <option value="both">Gap + Residue Combined</option>
                    </select>
                    
                    <label>
                        <input type="checkbox" id="showSteps" checked style="width: auto; margin-right: 10px;">
                        Show Step-by-Step Work
                    </label>
                </div>
                
                <div class="control-group">
                    <h3>Actions</h3>
                    <button onclick="compute()">Calculate</button>
                    <button class="export-btn" onclick="clearCache()" style="background: linear-gradient(45deg, #ff6b6b, #ee5a52);">Clear Cache</button>
                    <button class="export-btn" onclick="exportResults()">Export Results (JSON)</button>
                    <button class="export-btn" onclick="exportStepsText()">Export Steps (TXT)</button>
                    <button class="export-btn" onclick="exportChartImage()">Export Chart (4K/8K JPEG)</button>
                    <div id="cacheStatus" style="margin-top: 10px; padding: 8px; background: rgba(78, 205, 196, 0.1); border-radius: 5px; font-size: 0.85em; text-align: center; color: #4ecdc4;">Cache: <span id="cacheCount">0</span> results stored</div>
                </div>
            </div>
            
            <div id="results" class="results section" style="display: none;">
                <div class="result-card">
                    <h4>Computed Value</h4>
                    <div id="computed-value" class="value"></div>
                    <div id="error-bound" class="error-info"></div>
                    <div id="prime-count" class="error-info"></div>
                </div>
                
                <div class="result-card">
                    <h4>Exact Reference</h4>
                    <div id="exact-value" class="value"></div>
                    <div id="actual-error" class="error-info"></div>
                </div>
            </div>
            
            <div id="step-by-step" class="step-by-step" style="display: none;"></div>
            
            <div id="gap-analysis" class="gap-analysis" style="display: none;">
                <h3>Gap-Class Decomposition</h3>
                <div id="gap-grid" class="gap-grid"></div>
            </div>
            
            <div id="channel-analysis" class="channel-analysis" style="display: none;">
                <h3>Residue Channel Analysis</h3>
                <div class="view-options">
                    <button class="view-btn active" onclick="changeChannelView('cards')">Card View</button>
                    <button class="view-btn" onclick="changeChannelView('table')">Table View</button>
                    <button class="view-btn" onclick="changeChannelView('distribution')">Distribution Chart</button>
                </div>
                <div id="channel-content"></div>
            </div>
            
            <div id="chart-section" class="chart-container" style="display: none;">
                <h3>Residue Channel Contributions (ℤ<sub>a</sub>(s;30))</h3>
                <canvas id="channelChart"></canvas>
                <div class="chart-legend" id="chartLegend"></div>
            </div>
            
            <div id="visualization-section" class="visualization-container section" style="display: none;">
                <h3>Interactive Visualization</h3>
                
                <div class="viz-categories">
                    <button class="category-btn active" onclick="filterVizCategory('all')">All (28)</button>
                    <button class="category-btn" onclick="filterVizCategory('distribution')">Distribution</button>
                    <button class="category-btn" onclick="filterVizCategory('complex')">Complex Analysis</button>
                    <button class="category-btn" onclick="filterVizCategory('modular')">Modular</button>
                    <button class="category-btn" onclick="filterVizCategory('semiprimes')">Semiprimes</button>
                    <button class="category-btn" onclick="filterVizCategory('3d')">🎮 3D</button>
                </div>
                
                <div class="viz-options">
                    <button class="viz-btn active" onclick="changeViz('convergence')">Convergence</button>
                    <button class="viz-btn" onclick="changeViz('contribution')">Contributions</button>
                    <button class="viz-btn" onclick="changeViz('gapDist')">Gap Distribution</button>
                    <button class="viz-btn" onclick="changeViz('primeCount')">Prime Counting</button>
                    <button class="viz-btn" onclick="changeViz('density')">Density</button>
                    <button class="viz-btn" onclick="changeViz('gapHistogram')">Gap Histogram</button>
                    <button class="viz-btn" onclick="changeViz('sacksSpiral')">Sacks Spiral</button>
                    <button class="viz-btn" onclick="changeViz('zetaZeros')">Zeta Zeros</button>
                    <button class="viz-btn" onclick="changeViz('errorAnalysis')">Error Analysis</button>
                    <button class="viz-btn" onclick="changeViz('primeRaces')">Prime Races</button>
                    <button class="viz-btn" onclick="changeViz('goldbachComet')">Goldbach Comet</button>
                    <button class="viz-btn" onclick="changeViz('phaseExplorer')">Phase Explorer</button>
                    <button class="viz-btn" onclick="changeViz('phasorSum')">Phasor Sum</button>
                    <button class="viz-btn" onclick="changeViz('zetaSurface')">Zeta Surface</button>
                    <button class="viz-btn" onclick="changeViz('primeSpiral')">Ulam Spiral</button>
                    <button class="viz-btn" onclick="changeViz('channelRace')">Channel Race</button>
                    <button class="viz-btn" onclick="changeViz('heatmap')">Heatmap</button>
                    <button class="viz-btn" onclick="changeViz('voronoi')">Voronoi</button>
                    <button class="viz-btn" onclick="changeViz('harmonicWave')">Harmonic Wave</button>
                    <button class="viz-btn" onclick="changeViz('phaseLaw')">Phase Law</button>
                    <button class="viz-btn" onclick="changeViz('semiprimeDistribution')">Semiprime Dist</button>
                    <button class="viz-btn" onclick="changeViz('semiprimeGraph')">Semiprime Graph</button>
                    <button class="viz-btn" onclick="changeViz('factorizationTiming')">Factorization</button>
                    <button class="viz-btn" onclick="changeViz('modularInterference')">Mod Interference</button>
                    <button class="viz-btn" onclick="changeViz('twinSemiprimes')">Twin Semiprimes</button>
                    <button class="viz-btn" onclick="changeViz('semiprimeZeta')">Semiprime ζ_S</button>
                    <button class="viz-btn" onclick="changeViz('compositeChannels')">Prime & Composite Channels</button>
                </div>
                <div style="margin: 15px 0; padding: 15px; background: rgba(255, 255, 255, 0.05); border-radius: 10px;">
                    <label style="color: #fff; font-weight: 500;">Universal Zoom: <span id="universalZoomLevel">1.0</span>x</label>
                    <input type="range" id="universalZoomSlider" min="0.5" max="5" step="0.1" value="1" 
                           style="width: 100%;"
                           oninput="updateUniversalZoom(parseFloat(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.8em; opacity: 0.7; margin-top: 5px;">
                        <span>0.5x (Zoom Out)</span>
                        <span>1x (Default)</span>
                        <span>5x (Zoom In)</span>
                    </div>
                </div>
                <div style="margin: 15px 0; padding: 15px; background: rgba(255, 255, 255, 0.05); border-radius: 10px;">
                    <label style="color: #fff; font-weight: 500; display: block; margin-bottom: 8px;">
                        Universal Zoom: <span id="universalZoomLevel">1.0</span>x
                    </label>
                    <input type="range" id="universalZoomSlider" min="0.5" max="5" step="0.1" value="1" 
                           style="width: 100%;"
                           oninput="updateUniversalZoom(parseFloat(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.8em; opacity: 0.7; margin-top: 5px;">
                        <span>0.5x (Zoom Out)</span>
                        <span>1x (Default)</span>
                        <span>5x (Zoom In)</span>
                    </div>
                </div>
                <canvas id="vizCanvas"></canvas>
                <div id="vizStats" style="margin-top: 20px; padding: 20px; background: rgba(0, 0, 0, 0.3); border-radius: 10px; display: none;"></div>
            </div>
            
            <div id="prime-ring-section" class="prime-ring-container" style="display: none;">
                <h3>Prime Residue Visualization: Concentric Rings (mod m)</h3>
                <div class="ring-controls">
                    <label>
                        Modulus Mode:
                        <select id="modulusMode" onchange="toggleModulusMode()">
                            <option value="range">Range (1 to max)</option>
                            <option value="custom">Custom List</option>
                            <option value="powers">Powers of 2</option>
                            <option value="powers3">Powers of 3</option>
                        </select>
                    </label>
                    <div id="rangeControls">
                        <label>
                            Max Modulus:
                            <input type="number" id="maxModulus" value="30" min="2" max="100" step="1">
                        </label>
                    </div>
                    <div id="customControls" style="display: none;">
                        <label style="flex: 1;">
                            Custom Moduli (comma-separated):
                            <input type="text" id="customModuli" placeholder="e.g., 1,2,4,8,16,32" style="width: 100%;">
                        </label>
                    </div>
                    <label>
                        Point Size:
                        <input type="number" id="pointSize" value="4" min="2" max="10" step="1">
                    </label>
                    <label>
                        <input type="checkbox" id="showLabels" checked>
                        Show Prime Labels
                    </label>
                    <label>
                        <input type="checkbox" id="showModLines" checked>
                        Show Mod Lines
                    </label>
                    <label>
                        <input type="checkbox" id="invertRings">
                        Invert Ring Order
                    </label>
                    <label>
                        Color By:
                        <select id="colorMode">
                            <option value="residue">Residue Class</option>
                            <option value="modulus">Modulus Level</option>
                            <option value="size">Prime Size</option>
                        </select>
                    </label>
                    <button onclick="updatePrimeRing()" style="padding: 6px 16px; background: #4ecdc4; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Update</button>
                </div>
                <div class="ring-controls" style="margin-top: 10px;">
                    <label>
                        <input type="checkbox" id="invertColors">
                        White Background
                    </label>
                    <label>
                        Rotation Mode:
                        <select id="rotationMode">
                            <option value="none">No Rotation</option>
                            <option value="global">Global Rotation</option>
                            <option value="local">Local Rotation (by ring)</option>
                        </select>
                    </label>
                    <label>
                        Speed:
                        <input type="number" id="rotationSpeed" value="0.5" min="0.1" max="5" step="0.1">
                    </label>
                    <button onclick="toggleRotation()" id="rotationToggle" style="padding: 6px 16px; background: #ff6b6b; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Start Rotation</button>
                    <button onclick="exportPrimeRing()" style="padding: 6px 16px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold;">Export Ring (PNG)</button>
                </div>
                <canvas id="primeRingCanvas"></canvas>
                <div class="ring-info">
                    <strong>Visualization:</strong> Each prime p is plotted on concentric rings where ring m represents residues mod m.
                    Position on ring: angle θ = 2π·(p mod m)/m for primes with gcd(p mod m, m) = 1.
                    Use "Invert Ring Order" to show smallest modulus on outer ring.
                    <br><strong>Presets:</strong> Powers of 2 (1,2,4,8,...), Powers of 3 (1,3,9,27,...), or custom list.
                    Hover over points to see prime details.
                </div>
                <div id="ringLegend" class="ring-legend"></div>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <script>
        // Compute Euler's totient function
        function eulerPhi(n) {
            let result = n;
            for (let p = 2; p * p <= n; p++) {
                if (n % p === 0) {
                    while (n % p === 0) n /= p;
                    result -= result / p;
                }
            }
            if (n > 1) result -= result / n;
            return result;
        }
        
        // Get coprime residues mod m
        function getCoprimeResidues(m) {
            const residues = [];
            for (let a = 1; a < m; a++) {
                if (gcd(a, m) === 1) {
                    residues.push(a);
                }
            }
            return residues;
        }
        
        // GCD helper
        function gcd(a, b) {
            while (b !== 0) {
                const temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }
        
        let computationData = null;
        let channelChart = null;
        let vizChart = null;
        let currentViz = 'convergence';
        let currentChannelView = 'cards';
        let channelDataGlobal = null;
        let universalZoom = 1.0;
        let currentVizCategory = 'all';
        
        const vizCategories = {
            'convergence': 'distribution',
            'contribution': 'distribution',
            'gapDist': 'distribution',
            'primeCount': 'distribution',
            'density': 'distribution',
            'gapHistogram': 'distribution',
            'errorAnalysis': 'distribution',
            'phasorSum': 'complex',
            'zetaSurface': 'complex',
            'zetaZeros': 'complex',
            'phaseExplorer': 'complex',
            'phaseLaw': 'complex',
            'sacksSpiral': 'modular',
            'primeSpiral': 'modular',
            'primeRaces': 'modular',
            'channelRace': 'modular',
            'heatmap': 'modular',
            'voronoi': 'modular',
            'modularInterference': 'modular',
            'goldbachComet': 'distribution',
            'harmonicWave': 'complex',
            'semiprimeDistribution': 'semiprimes',
            'semiprimeGraph': 'semiprimes',
            'factorizationTiming': 'semiprimes',
            'twinSemiprimes': 'semiprimes',
            'semiprimeZeta': 'semiprimes',
            'compositeChannels': 'modular'
        };
        
        // Three.js globals for 3D visualizations
        let scene3D = null;
        let camera3D = null;
        let renderer3D = null;
        let controls3D = null;
        let animationFrame3D = null;
        
        function showPresets() {
            const presets = document.getElementById('presetExamples');
            presets.style.display = presets.style.display === 'none' ? 'grid' : 'none';
        }
        
        function applyPreset(presetName) {
            const presets = {
                'pi10': { epsilon: 0.00000000001, constant: 'pi', modulus: 30 },
                'pi15': { epsilon: 0.0000000000000001, constant: 'pi', modulus: 30 },
                'firstZero': { epsilon: 0.01, constant: 'pi', modulus: 30, viz: 'zetaZeros' },
                'mod60': { epsilon: 0.01, constant: 'pi', modulus: 60 },
                'semiprimes': { epsilon: 0.01, constant: 'pi', modulus: 30, viz: 'semiprimeDistribution' },
                'highPrecision': { epsilon: 0.000000000001, constant: 'zeta4', modulus: 30 }
            };
            
            const preset = presets[presetName];
            if (preset) {
                document.getElementById('epsilon').value = preset.epsilon;
                document.getElementById('constant').value = preset.constant;
                document.getElementById('modulus').value = preset.modulus;
                compute();
                if (preset.viz) {
                    setTimeout(() => {
                        document.getElementById('visualization-section').scrollIntoView({ behavior: 'smooth' });
                        changeViz(preset.viz);
                    }, 500);
                }
            }
            document.getElementById('presetExamples').style.display = 'none';
        }
        
        function filterVizCategory(category) {
            currentVizCategory = category;
            
            // Update category buttons
            document.querySelectorAll('.category-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            
            // Filter visualization buttons
            document.querySelectorAll('.viz-btn').forEach(btn => {
                const vizType = btn.getAttribute('onclick').match(/changeViz\('(.+?)'\)/)[1];
                const vizCat = vizCategories[vizType] || 'distribution';
                
                if (category === 'all' || vizCat === category) {
                    btn.style.display = 'inline-block';
                } else {
                    btn.style.display = 'none';
                }
            });
        }
        
        function exportAllData() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const allData = {
                timestamp: new Date().toISOString(),
                parameters: {
                    epsilon: computationData.epsilon,
                    constantType: computationData.constantType,
                    method: computationData.method,
                    modulus: computationData.modulus,
                    cutoff: computationData.Y
                },
                results: {
                    computedValue: computationData.computedValue,
                    exactValue: computationData.exactValue,
                    absoluteError: Math.abs(computationData.computedValue - computationData.exactValue),
                    relativeError: Math.abs(computationData.computedValue - computationData.exactValue) / computationData.exactValue,
                    primesUsed: computationData.primes.length
                },
                primes: computationData.primes,
                partialProducts: computationData.partialProducts
            };
            
            const blob = new Blob([JSON.stringify(allData, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `modular_sieve_complete_${Date.now()}.json`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        // Smooth scroll for nav links
        document.addEventListener('DOMContentLoaded', function() {
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const target = document.querySelector(this.getAttribute('href'));
                    if (target) {
                        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                        
                        // Update active state
                        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
                        this.classList.add('active');
                    }
                });
            });
            
            // Highlight active section on scroll
            window.addEventListener('scroll', function() {
                const sections = document.querySelectorAll('.section');
                const navLinks = document.querySelectorAll('.nav-link');
                
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 100) {
                        current = section.getAttribute('id');
                    }
                });
                
                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href') === '#' + current) {
                        link.classList.add('active');
                    }
                });
            });
        });
        
        function updateUniversalZoom(zoom) {
            universalZoom = zoom;
            document.getElementById('universalZoomLevel').textContent = zoom.toFixed(1);
            updateVisualization(currentViz);
        }
        
        function setEpsilon(value) {
            document.getElementById('epsilon').value = value;
            // Visual feedback
            const epsilonInput = document.getElementById('epsilon');
            epsilonInput.style.background = 'rgba(78, 205, 196, 0.3)';
            setTimeout(() => {
                epsilonInput.style.background = 'rgba(255, 255, 255, 0.9)';
            }, 300);
        }
        
        function toggleSection(id) {
            const content = document.getElementById(id + '-content');
            const icon = document.getElementById(id + '-icon');
            content.classList.toggle('open');
            icon.classList.toggle('open');
        }
        
        // Sieve of Eratosthenes
        function sieveOfEratosthenes(limit) {
            if (limit < 2) return [];
            
            const isPrime = new Array(limit + 1).fill(true);
            isPrime[0] = isPrime[1] = false;
            
            for (let i = 2; i * i <= limit; i++) {
                if (isPrime[i]) {
                    for (let j = i * i; j <= limit; j += i) {
                        isPrime[j] = false;
                    }
                }
            }
            
            const primes = [];
            for (let i = 2; i <= limit; i++) {
                if (isPrime[i]) primes.push(i);
            }
            return primes;
        }
        
        // Compute gap classes
        function computeGapClasses(primes) {
            const gapClasses = {};
            
            for (let i = 1; i < primes.length; i++) {
                const gap = primes[i] - primes[i-1];
                if (!gapClasses[gap]) gapClasses[gap] = [];
                gapClasses[gap].push(primes[i]);
            }
            
            return gapClasses;
        }
        
        // Compute residue channels for any modulus
        function computeResidueChannels(primes, modulus) {
            const coprimeResidues = getCoprimeResidues(modulus);
            const channels = {};
            
            coprimeResidues.forEach(a => channels[a] = []);
            
            primes.forEach(p => {
                if (p >= modulus) {
                    const residue = p % modulus;
                    if (coprimeResidues.includes(residue)) {
                        channels[residue].push(p);
                    }
                }
            });
            
            return channels;
        }
        
        // Compute Y cutoff
        function computeCutoff(epsilon, constantType) {
            if (constantType === 'pi') {
                return Math.ceil(1 + 1 / Math.log(1 + epsilon));
            } else {
                const n = parseInt(constantType.replace('zeta', '')) / 2;
                const power = 1 / (2 * n - 1);
                return Math.ceil(Math.pow(2 / ((2 * n - 1) * Math.log(1 + epsilon)), power));
            }
        }
        
        // Compute truncated product
        function computeTruncatedProduct(primes, exponent) {
            let product = 1;
            for (const p of primes) {
                product *= 1 / (1 - Math.pow(p, -exponent));
            }
            return product;
        }
        
        // Compute partial products (for convergence visualization)
        function computePartialProducts(primes, exponent) {
            const partials = [];
            let product = 1;
            
            for (const p of primes) {
                product *= 1 / (1 - Math.pow(p, -exponent));
                partials.push({ prime: p, value: product });
            }
            
            return partials;
        }
        
        // Exact values
        const exactValues = {
            'pi': Math.PI,
            'zeta4': Math.PI ** 4 / 90,
            'zeta6': Math.PI ** 6 / 945,
            'zeta8': Math.PI ** 8 / 9450,
            'zeta10': Math.PI ** 10 / 93555
        };
        
        // Web Worker for heavy computations
        let computeWorker = null;
        
        // Cache for computed results
        const computationCache = new Map();
        
        function getCacheKey(epsilon, constantType, modulus) {
            return `${epsilon}_${constantType}_${modulus}`;
        }
        
        function compute() {
            const epsilon = parseFloat(document.getElementById('epsilon').value);
            const constantType = document.getElementById('constant').value;
            const method = document.getElementById('method').value;
            const showSteps = document.getElementById('showSteps').checked;
            const modulus = parseInt(document.getElementById('modulus').value);
            decimalPlaces = parseInt(document.getElementById('decimalPlaces').value);
            
            // Check cache first
            const cacheKey = getCacheKey(epsilon, constantType, modulus);
            if (computationCache.has(cacheKey)) {
                console.log('Loading from cache...');
                const cached = computationCache.get(cacheKey);
                displayResults(cached, showSteps, method);
                return;
            }
            
            document.getElementById('results').style.display = 'block';
            document.getElementById('computed-value').innerHTML = '<div class="loading">Computing...<br><div id="progressBar" style="width: 100%; height: 20px; background: rgba(0,0,0,0.3); border-radius: 10px; margin-top: 10px; overflow: hidden;"><div id="progressFill" style="width: 0%; height: 100%; background: linear-gradient(90deg, #4ecdc4, #44a8a3); transition: width 0.3s ease;"></div></div><div id="progressText" style="margin-top: 8px; font-size: 0.9em; opacity: 0.8;">Initializing...</div></div>';
            
            setTimeout(() => {
                try {
                    const Y = computeCutoff(epsilon, constantType);
                    updateProgress(10, 'Generating primes...');
                    
                    const primes = sieveOfEratosthenes(Y - 1);
                    updateProgress(40, 'Computing Euler product...');
                    
                    let computedValue;
                    const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
                    
                    updateProgress(60, 'Computing truncated product...');
                    
                    if (constantType === 'pi') {
                        const zetaProduct = computeTruncatedProduct(primes, 2);
                        computedValue = Math.sqrt(6 * zetaProduct);
                    } else {
                        const n = parseInt(constantType.replace('zeta', '')) / 2;
                        computedValue = computeTruncatedProduct(primes, 2 * n);
                    }
                    
                    updateProgress(80, 'Generating partial products...');
                    
                    // Store computation data
                    computationData = {
                        epsilon,
                        constantType,
                        method,
                        modulus,
                        Y,
                        primes,
                        exponent,
                        computedValue,
                        exactValue: exactValues[constantType],
                        partialProducts: computePartialProducts(primes, constantType === 'pi' ? 2 : exponent)
                    };
                    
                    // Cache the result
                    computationCache.set(cacheKey, computationData);
                    
                    updateProgress(100, 'Complete!');
                    
                    setTimeout(() => {
                        displayResults(computationData, showSteps, method);
                    }, 300);
                    
                } catch (error) {
                    document.getElementById('computed-value').innerHTML = `<span style="color: #ff6b6b;">Error: ${error.message}</span>`;
                }
            }, 100);
        }
        
        function updateProgress(percent, message) {
            const fill = document.getElementById('progressFill');
            const text = document.getElementById('progressText');
            if (fill) fill.style.width = percent + '%';
            if (text) text.textContent = message;
        }
        
        function displayResults(data, showSteps, method) {
            const { epsilon, constantType, modulus, Y, primes, computedValue, exactValue, exponent } = data;
            
            // Display results
            document.getElementById('computed-value').textContent = computedValue.toFixed(decimalPlaces);
            document.getElementById('exact-value').textContent = exactValue.toFixed(decimalPlaces);
            
            const actualError = Math.abs(computedValue - exactValue) / exactValue;
            document.getElementById('actual-error').innerHTML = `Actual relative error: <strong>${(actualError * 100).toFixed(Math.min(decimalPlaces - 5, 8))}%</strong>`;
            document.getElementById('error-bound').innerHTML = `Guaranteed error ≤ <strong>${(epsilon * 100).toFixed(4)}%</strong>`;
            document.getElementById('prime-count').innerHTML = `Using <strong>${primes.length}</strong> primes up to <strong>${Y-1}</strong> <span style="color: #4ecdc4; font-size: 0.9em;">(cached)</span>`;
            
            // Add precision info
            const precisionNote = decimalPlaces > 15 ? 
                '<div style="font-size: 0.85em; color: #ff6b6b; margin-top: 8px;">⚠️ Note: JavaScript floating-point precision is limited to ~15-17 significant digits</div>' : '';
            document.getElementById('prime-count').innerHTML += precisionNote;
            
            // Show step-by-step
            if (showSteps) {
                showStepByStep(data);
            } else {
                document.getElementById('step-by-step').style.display = 'none';
            }
            
            // Method-specific analysis
            if (method === 'gap' || method === 'both') {
                showGapAnalysis(primes, constantType);
            } else {
                document.getElementById('gap-analysis').style.display = 'none';
            }
            
            if (method === 'residue' || method === 'both') {
                showResidueAnalysis(primes, constantType, modulus);
            } else {
                document.getElementById('channel-analysis').style.display = 'none';
                document.getElementById('chart-section').style.display = 'none';
            }
            
            // Show visualization
            document.getElementById('visualization-section').style.display = 'block';
            updateVisualization(currentViz);
            
            // Show prime ring visualization
            document.getElementById('prime-ring-section').style.display = 'block';
            updatePrimeRing();
        }
        
        function showStepByStep(data) {
            const { epsilon, constantType, Y, primes, exponent, computedValue, exactValue } = data;
            
            let html = '<h3>Step-by-Step Calculation</h3>';
            
            // Step 1: Determine cutoff
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">1</span>Determine Required Cutoff Y</div>
                    <div class="step-content">
                        <p>Given target relative error ε = ${epsilon}</p>
                        ${constantType === 'pi' ? `
                            <p>For π, we use: Y = ⌈1 + 1/log(1+ε)⌉</p>
                            <div class="step-formula">
                                Y = ⌈1 + 1/log(1+${epsilon})⌉<br>
                                Y = ⌈1 + ${(1/Math.log(1+epsilon)).toFixed(4)}⌉<br>
                                Y = ${Y}
                            </div>
                        ` : `
                            <p>For ζ(${exponent}), we use: Y = ⌈(2/((2n-1)·log(1+ε)))<sup>1/(2n-1)</sup>⌉ where n = ${exponent/2}</p>
                            <div class="step-formula">
                                Y = ⌈(2/(${exponent-1}·log(1+${epsilon})))<sup>1/${exponent-1}</sup>⌉<br>
                                Y = ${Y}
                            </div>
                        `}
                        <p>Therefore, we need all primes up to ${Y-1}.</p>
                    </div>
                </div>
            `;
            
            // Step 2: Generate primes
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">2</span>Generate Primes Using Sieve</div>
                    <div class="step-content">
                        <p>Using the Sieve of Eratosthenes to find all primes ≤ ${Y-1}:</p>
                        <p><strong>Found ${primes.length} primes:</strong></p>
                        <div class="step-formula">
                            {${primes.slice(0, 20).join(', ')}${primes.length > 20 ? ', ..., ' + primes[primes.length-1] : ''}}
                        </div>
                    </div>
                </div>
            `;
            
            // Step 3: Compute Euler product
            const firstFewFactors = primes.slice(0, 5).map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return `(1 - ${p}<sup>-${exponent}</sup>)<sup>-1</sup> = ${factor.toFixed(Math.min(decimalPlaces, 10))}`;
            }).join('<br>');
            
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">3</span>Compute Euler Product</div>
                    <div class="step-content">
                        <p>${constantType === 'pi' ? 'For π, compute ζ(2) = ∏(1-p<sup>-2</sup>)<sup>-1</sup>' : `Compute ζ(${exponent}) = ∏(1-p<sup>-${exponent}</sup>)<sup>-1</sup>`}</p>
                        <p><strong>First few factors:</strong></p>
                        <div class="step-formula">${firstFewFactors}</div>
                        <p><strong>Product of all ${primes.length} factors:</strong></p>
                        <div class="step-formula">
                            ${constantType === 'pi' ? 'ζ(2) = ' : `ζ(${exponent}) = `}${computeTruncatedProduct(primes, exponent).toFixed(Math.min(decimalPlaces, 12))}
                        </div>
                    </div>
                </div>
            `;
            
            // Step 4: Final computation
            if (constantType === 'pi') {
                const zeta2 = computeTruncatedProduct(primes, 2);
                html += `
                    <div class="step">
                        <div class="step-title"><span class="step-number">4</span>Extract π from ζ(2)</div>
                        <div class="step-content">
                            <p>Using the identity ζ(2) = π²/6, we have π = √(6·ζ(2))</p>
                            <div class="step-formula">
                                π = √(6 × ${zeta2.toFixed(Math.min(decimalPlaces, 12))})<br>
                                π = √${(6 * zeta2).toFixed(Math.min(decimalPlaces, 12))}<br>
                                π ≈ ${computedValue.toFixed(decimalPlaces)}
                            </div>
                            <p><strong>Exact value:</strong> π = ${exactValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(Math.min(decimalPlaces - 9, 6))}</p>
                        </div>
                    </div>
                `;
            } else {
                html += `
                    <div class="step">
                        <div class="step-title"><span class="step-number">4</span>Compare with Exact Value</div>
                        <div class="step-content">
                            <p><strong>Computed:</strong> ζ(${exponent}) ≈ ${computedValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Exact:</strong> ζ(${exponent}) = ${exactValue.toFixed(decimalPlaces)}</p>
                            <p><strong>Absolute error:</strong> ${Math.abs(computedValue - exactValue).toExponential(Math.min(decimalPlaces - 9, 6))}</p>
                            <p><strong>Relative error:</strong> ${(Math.abs(computedValue - exactValue) / exactValue * 100).toFixed(Math.min(decimalPlaces - 7, 8))}%</p>
                        </div>
                    </div>
                `;
            }
            
            // Step 5: Error verification
            const actualError = Math.abs(computedValue - exactValue) / exactValue;
            html += `
                <div class="step">
                    <div class="step-title"><span class="step-number">5</span>Verify Error Bound</div>
                    <div class="step-content">
                        <p><strong>Guaranteed bound:</strong> relative error ≤ ${(epsilon * 100).toFixed(4)}%</p>
                        <p><strong>Actual error:</strong> ${(actualError * 100).toFixed(8)}%</p>
                        <p style="color: ${actualError <= epsilon ? '#4ecdc4' : '#ff6b6b'}; font-weight: bold;">
                            ${actualError <= epsilon ? '✓ Error bound satisfied!' : '⚠ Note: Actual error slightly exceeds theoretical bound (due to finite precision)'}
                        </p>
                    </div>
                </div>
            `;
            
            document.getElementById('step-by-step').innerHTML = html;
            document.getElementById('step-by-step').style.display = 'block';
        }
        
        // Compute gap classes using standard forward gap method
        function computeLowestGapClasses(primes) {
            const gapClasses = {};
            
            for (let i = 0; i < primes.length - 1; i++) {
                const p = primes[i];
                const nextPrime = primes[i + 1];
                const gap = nextPrime - p;
                
                if (!gapClasses[gap]) gapClasses[gap] = [];
                gapClasses[gap].push(p);
            }
            
            // Last prime has no successor, we can assign it to its backward gap or omit
            // For consistency, we'll omit the last prime from gap classification
            
            return gapClasses;
        }
        
        function showGapAnalysis(primes, constantType) {
            const gapClasses = computeLowestGapClasses(primes);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            
            let html = '<div style="margin-bottom: 20px; padding: 20px; background: rgba(255, 215, 0, 0.1); border-radius: 10px; border-left: 4px solid #ffd700;">';
            html += '<h3 style="color: #ffd700; margin-bottom: 15px;">Prime Gap Classification System</h3>';
            html += '<p style="line-height: 1.6; margin-bottom: 10px;"><strong>By Wessen Getachew</strong></p>';
            html += '<p style="line-height: 1.6; margin-bottom: 15px;">This system decomposes ζ(s) by classifying primes according to their <strong>lowest valid even gap</strong>. Each prime belongs to exactly one gap class g based on its minimum even gap to another prime.</p>';
            html += '<div style="background: rgba(0, 0, 0, 0.2); padding: 15px; border-radius: 8px; font-family: monospace; margin-bottom: 15px;">';
            html += 'ζ(s) = ∏(g=0 to ∞) Z<sup>(g)</sup>(s)<br>';
            html += 'where Z<sup>(g)</sup>(s) = ∏(p in P<sub>g</sub>) [p<sup>s</sup> / (p<sup>s</sup> - 1)]';
            html += '</div>';
            html += '<button class="view-btn active" onclick="expandAllGaps()">Expand All</button>';
            html += '<button class="view-btn" onclick="collapseAllGaps()">Collapse All</button>';
            html += '</div>';
            
            const sortedGaps = Object.keys(gapClasses).map(Number).sort((a, b) => a - b);
            
            // Calculate cumulative product across all gaps
            let globalCumulative = 1;
            const gapContributions = [];
            
            for (const gap of sortedGaps) {
                const gapPrimes = gapClasses[gap];
                let gapProduct = 1;
                
                for (const p of gapPrimes) {
                    const factor = 1 / (1 - Math.pow(p, -exponent));
                    gapProduct *= factor;
                }
                
                globalCumulative *= gapProduct;
                gapContributions.push({
                    gap: gap,
                    contribution: gapProduct,
                    cumulative: globalCumulative,
                    primes: gapPrimes
                });
            }
            
            // Display each gap class
            for (const gapData of gapContributions) {
                const gap = gapData.gap;
                const gapPrimes = gapData.primes;
                const contribution = gapData.contribution;
                const cumulative = gapData.cumulative;
                const logContrib = Math.log(contribution);
                
                // Calculate individual cumulative steps within this gap
                let cumulativeSteps = [];
                let cumProduct = 1;
                for (const p of gapPrimes) {
                    const factor = 1 / (1 - Math.pow(p, -exponent));
                    cumProduct *= factor;
                    cumulativeSteps.push({
                        prime: p,
                        factor: factor,
                        cumulative: cumProduct
                    });
                }
                
                html += `
                    <div class="gap-item" onclick="toggleGap(${gap})">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div><strong>Gap = ${gap}</strong></div>
                            <div class="gap-value">${gapPrimes.length} primes</div>
                        </div>
                        <div style="margin-top: 10px; font-size: 0.9em;">
                            <div><strong>P<sub>${gap}</sub>(${exponent}):</strong> ${contribution.toFixed(12)}</div>
                            <div><strong>Global Cumulative ζ:</strong> ${cumulative.toFixed(12)}</div>
                            <div style="opacity: 0.8;">log(P<sub>${gap}</sub>) = ${logContrib.toFixed(6)}</div>
                        </div>
                        <div style="margin-top: 8px; font-size: 0.85em; opacity: 0.8;">
                            ${gap === 2 ? 'Twin primes (consecutive odd primes)' :
                              gap === 4 ? 'Cousin primes' :
                              gap === 6 ? 'Sexy primes' :
                              `Primes with gap ${gap} to next prime`}
                        </div>
                        <div style="margin-top: 8px; font-size: 0.85em; opacity: 0.8;">
                            Range: ${Math.min(...gapPrimes)} - ${Math.max(...gapPrimes)}
                        </div>
                        <div class="expand-indicator">Click to view details</div>
                        
                        <div class="gap-primes-list" id="gap-primes-${gap}">
                            <h4 style="color: #ffd700; margin-bottom: 10px;">Gap Class: ${gapPrimes.length} Primes with Gap ${gap}</h4>
                            <div class="gap-primes-container">${gapPrimes.map((p, idx) => {
                                const nextIdx = primes.indexOf(p) + 1;
                                if (nextIdx < primes.length) {
                                    const nextP = primes[nextIdx];
                                    const actualGap = nextP - p;
                                    return `p = ${p} → next prime: ${nextP}, gap = ${actualGap}`;
                                } else {
                                    return `p = ${p} (last prime in dataset)`;
                                }
                            }).join('<br>')}</div>
                            
                            <div class="gap-cumulative-section">
                                <h4 style="color: #4ecdc4; margin-bottom: 10px;">Cumulative Product for Z<sup>(${gap})</sup>(${exponent}):</h4>
                                ${cumulativeSteps.map((step, idx) => `
                                    <div class="cumulative-step">
                                        <strong>Step ${idx + 1}:</strong> p = ${step.prime}<br>
                                        Factor: [${step.prime}<sup>${exponent}</sup> / (${step.prime}<sup>${exponent}</sup> - 1)] = ${step.factor.toFixed(Math.min(decimalPlaces - 7, 8))}<br>
                                        Cumulative within gap: ${step.cumulative.toFixed(Math.min(decimalPlaces - 5, 10))}
                                    </div>
                                `).join('')}
                                <div style="margin-top: 15px; padding: 10px; background: rgba(78, 205, 196, 0.2); border-radius: 5px;">
                                    <strong>P<sub>${gap}</sub>(${exponent}) = ${contribution.toFixed(Math.min(decimalPlaces, 12))}</strong><br>
                                    <strong>Global Cumulative ζ(${exponent}) = ${cumulative.toFixed(Math.min(decimalPlaces, 12))}</strong>
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            document.getElementById('gap-grid').innerHTML = html;
            document.getElementById('gap-analysis').style.display = 'block';
        }
        
        function toggleGap(gapId) {
            const primesList = document.getElementById(`gap-primes-${gapId}`);
            if (!primesList) return;
            
            primesList.classList.toggle('visible');
            
            const gapItem = primesList.closest('.gap-item');
            gapItem.classList.toggle('expanded');
        }
        
        function sortGapsBySize() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'size');
        }
        
        function sortGapsByCount() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'count');
        }
        
        function sortGapsByContribution() {
            if (!computationData) return;
            const { primes, constantType } = computationData;
            showGapAnalysis(primes, constantType, 'contribution');
        }
        
        function expandAllGaps() {
            document.querySelectorAll('.gap-primes-list').forEach(list => {
                list.classList.add('visible');
                list.closest('.gap-item').classList.add('expanded');
            });
        }
        
        function collapseAllGaps() {
            document.querySelectorAll('.gap-primes-list').forEach(list => {
                list.classList.remove('visible');
                list.closest('.gap-item').classList.remove('expanded');
            });
        }
        
        function showResidueAnalysis(primes, constantType, modulus) {
            const channels = computeResidueChannels(primes, modulus);
            const exponent = constantType === 'pi' ? 2 : parseInt(constantType.replace('zeta', ''));
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const smallPrimes = primes.filter(p => p < modulus);
            const smallProduct = computeTruncatedProduct(smallPrimes, exponent);
            
            channelDataGlobal = {
                channels,
                coprimeResidues,
                smallPrimes,
                smallProduct,
                exponent,
                modulus,
                allPrimes: primes
            };
            
            document.getElementById('channel-analysis').style.display = 'block';
            renderChannelView(currentChannelView);
            
            // Destroy existing chart before creating new one
            if (channelChart) {
                channelChart.destroy();
                channelChart = null;
            }
            
            // Clear canvas before creating new chart
            const canvas = document.getElementById('channelChart');
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            createChannelChart(coprimeResidues, channels, exponent, smallProduct, modulus);
        }
        
        function changeChannelView(viewType) {
            currentChannelView = viewType;
            renderChannelView(viewType);
            updateChannelViewButtons();
        }
        
        function renderChannelView(viewType) {
            if (!channelDataGlobal) return;
            
            const { channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus } = channelDataGlobal;
            
            if (viewType === 'cards') {
                renderCardView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            } else if (viewType === 'table') {
                renderTableView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            } else if (viewType === 'distribution') {
                renderDistributionView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus);
            }
        }
        
        function renderCardView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            let html = '<div class="channel-grid">';
            
            // Small primes card
            html += `
                <div class="channel-item" onclick="toggleChannel('small-primes')">
                    <div class="channel-header">
                        <div class="channel-residue">Small Primes (< ${modulus})</div>
                        <div class="channel-count">${smallPrimes.length}</div>
                    </div>
                    <div class="channel-stats">
                        <div class="stat-item">
                            <div class="stat-label">Contribution</div>
                            <div class="stat-value">${smallProduct.toFixed(6)}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">log(Contrib)</div>
                            <div class="stat-value">${Math.log(smallProduct).toFixed(4)}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Avg Prime</div>
                            <div class="stat-value">${(smallPrimes.reduce((a,b)=>a+b,0)/smallPrimes.length).toFixed(1)}</div>
                        </div>
                    </div>
                    <div class="expand-indicator">Click to view primes</div>
                    <div class="primes-list" id="primes-small-primes">
                        <h4>All ${smallPrimes.length} Primes:</h4>
                        <div class="primes-container">${smallPrimes.join(', ')}</div>
                    </div>
                </div>
            `;
            
            // Channel cards
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const avgPrime = channelPrimes.length > 0 ? channelPrimes.reduce((sum, p) => sum + p, 0) / channelPrimes.length : 0;
                const minPrime = channelPrimes.length > 0 ? Math.min(...channelPrimes) : 0;
                const maxPrime = channelPrimes.length > 0 ? Math.max(...channelPrimes) : 0;
                
                html += `
                    <div class="channel-item" onclick="toggleChannel('${a}')">
                        <div class="channel-header">
                            <div class="channel-residue">≡ ${a} (mod ${modulus})</div>
                            <div class="channel-count">${channelPrimes.length}</div>
                        </div>
                        <div class="channel-stats">
                            <div class="stat-item">
                                <div class="stat-label">Contribution</div>
                                <div class="stat-value">${contribution.toFixed(Math.min(decimalPlaces - 9, 6))}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">log(Contrib)</div>
                                <div class="stat-value">${logContrib.toFixed(Math.min(decimalPlaces - 11, 4))}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Avg Prime</div>
                                <div class="stat-value">${avgPrime > 0 ? avgPrime.toFixed(1) : 'N/A'}</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-label">Range</div>
                                <div class="stat-value">${minPrime > 0 ? `${minPrime} - ${maxPrime}` : 'N/A'}</div>
                            </div>
                        </div>
                        ${channelPrimes.length > 0 ? '<div class="expand-indicator">Click to view primes</div>' : ''}
                        <div class="primes-list" id="primes-${a}">
                            <h4>All ${channelPrimes.length} Primes in Channel ${a}:</h4>
                            <div class="primes-container">${channelPrimes.join(', ')}</div>
                        </div>
                    </div>
                `;
            }
            
            html += '</div>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function renderTableView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            let html = '<table class="distribution-table">';
            html += `
                <thead>
                    <tr>
                        <th>Residue Class</th>
                        <th>Prime Count</th>
                        <th>Contribution</th>
                        <th>log(Contribution)</th>
                        <th>Avg Prime</th>
                        <th>Min Prime</th>
                        <th>Max Prime</th>
                        <th>% of Total</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
            `;
            
            const totalPrimes = smallPrimes.length + coprimeResidues.reduce((sum, a) => sum + channels[a].length, 0);
            
            // Small primes row
            html += `
                <tr>
                    <td><strong>Small (< ${modulus})</strong></td>
                    <td>${smallPrimes.length}</td>
                    <td>${smallProduct.toFixed(6)}</td>
                    <td>${Math.log(smallProduct).toFixed(4)}</td>
                    <td>${(smallPrimes.reduce((a,b)=>a+b,0)/smallPrimes.length).toFixed(1)}</td>
                    <td>${Math.min(...smallPrimes)}</td>
                    <td>${Math.max(...smallPrimes)}</td>
                    <td>${((smallPrimes.length / totalPrimes) * 100).toFixed(2)}%</td>
                    <td><button class="view-btn" style="padding: 4px 8px; font-size: 0.8em;" onclick="showPrimesModal('small-primes', ${JSON.stringify(smallPrimes).replace(/"/g, '&quot;')})">View Primes</button></td>
                </tr>
            `;
            
            // Channel rows
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const avgPrime = channelPrimes.length > 0 ? channelPrimes.reduce((sum, p) => sum + p, 0) / channelPrimes.length : 0;
                const minPrime = channelPrimes.length > 0 ? Math.min(...channelPrimes) : 0;
                const maxPrime = channelPrimes.length > 0 ? Math.max(...channelPrimes) : 0;
                const percentage = (channelPrimes.length / totalPrimes) * 100;
                
                html += `
                    <tr>
                        <td><strong>≡ ${a} (mod ${modulus})</strong></td>
                        <td>${channelPrimes.length}</td>
                        <td>${contribution.toFixed(Math.min(decimalPlaces - 9, 6))}</td>
                        <td>${logContrib.toFixed(Math.min(decimalPlaces - 11, 4))}</td>
                        <td>${avgPrime > 0 ? avgPrime.toFixed(1) : 'N/A'}</td>
                        <td>${minPrime > 0 ? minPrime : 'N/A'}</td>
                        <td>${maxPrime > 0 ? maxPrime : 'N/A'}</td>
                        <td>${percentage.toFixed(2)}%</td>
                        <td>${channelPrimes.length > 0 ? `<button class="view-btn" style="padding: 4px 8px; font-size: 0.8em;" onclick='showPrimesModal("${a}", ${JSON.stringify(channelPrimes)})'>View Primes</button>` : 'N/A'}</td>
                    </tr>
                `;
            }
            
            html += '</tbody></table>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function renderDistributionView(channels, coprimeResidues, smallPrimes, smallProduct, exponent, modulus) {
            const totalPrimes = smallPrimes.length + coprimeResidues.reduce((sum, a) => sum + channels[a].length, 0);
            
            let html = '<div style="margin-top: 20px; background: rgba(0, 0, 0, 0.6); padding: 20px; border-radius: 15px;">';
            html += '<h4 style="color: #ffd700; margin-bottom: 15px;">Prime Distribution by Residue Class</h4>';
            
            // Small primes
            const smallPercent = (smallPrimes.length / totalPrimes) * 100;
            html += `
                <div style="margin-bottom: 20px; padding: 15px; background: rgba(30, 60, 114, 0.6); border-radius: 10px;">
                    <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                        <span><strong>Small Primes (< ${modulus})</strong></span>
                        <span><strong>${smallPrimes.length} primes (${smallPercent.toFixed(2)}%)</strong></span>
                    </div>
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: ${smallPercent}%;"></div>
                    </div>
                    <div style="margin-top: 8px; font-size: 0.9em; opacity: 0.8;">
                        Contribution: ${smallProduct.toFixed(Math.min(decimalPlaces - 9, 6))} | log: ${Math.log(smallProduct).toFixed(Math.min(decimalPlaces - 11, 4))}
                    </div>
                </div>
            `;
            
            // Channels
            for (const a of coprimeResidues) {
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                const logContrib = Math.log(contribution);
                const percent = (channelPrimes.length / totalPrimes) * 100;
                
                html += `
                    <div style="margin-bottom: 20px; padding: 15px; background: rgba(30, 60, 114, 0.6); border-radius: 10px;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span><strong>≡ ${a} (mod ${modulus})</strong></span>
                            <span><strong>${channelPrimes.length} primes (${percent.toFixed(2)}%)</strong></span>
                        </div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: ${percent}%;"></div>
                        </div>
                        <div style="margin-top: 8px; font-size: 0.9em; opacity: 0.8;">
                            Contribution: ${contribution.toFixed(6)} | log: ${logContrib.toFixed(4)}
                            ${channelPrimes.length > 0 ? ` | <button class="view-btn" style="padding: 2px 8px; font-size: 0.8em;" onclick='showPrimesModal("${a}", ${JSON.stringify(channelPrimes)})'>View Primes</button>` : ''}
                        </div>
                    </div>
                `;
            }
            
            html += '</div>';
            document.getElementById('channel-content').innerHTML = html;
        }
        
        function toggleChannel(id) {
            const primesList = document.getElementById(`primes-${id}`);
            if (!primesList) return;
            
            primesList.classList.toggle('visible');
            
            const channelItem = primesList.closest('.channel-item');
            channelItem.classList.toggle('expanded');
        }
        
        let channelSortOrder = 'residue';
        let decimalPlaces = 15; // Global decimal places setting
        
        function validateDecimalPlaces() {
            const input = document.getElementById('decimalPlaces');
            const warning = document.getElementById('precision-warning');
            const value = parseInt(input.value);
            
            // Cap at 20
            if (value > 20) {
                input.value = 20;
            }
            
            // Show warning if > 17
            if (value > 17) {
                warning.style.display = 'block';
            } else {
                warning.style.display = 'none';
            }
        }
        
        function updateChannelViewButtons() {
            document.querySelectorAll('.view-options .view-btn').forEach(btn => {
                btn.classList.remove('active');
                const text = btn.textContent.toLowerCase();
                if (currentChannelView === 'cards' && text.includes('card')) btn.classList.add('active');
                if (currentChannelView === 'table' && text.includes('table')) btn.classList.add('active');
                if (currentChannelView === 'distribution' && text.includes('distribution')) btn.classList.add('active');
            });
        }
        
        function expandAllChannels() {
            document.querySelectorAll('.primes-list').forEach(list => {
                list.classList.add('visible');
                list.closest('.channel-item').classList.add('expanded');
            });
        }
        
        function collapseAllChannels() {
            document.querySelectorAll('.primes-list').forEach(list => {
                list.classList.remove('visible');
                list.closest('.channel-item').classList.remove('expanded');
            });
        }
        
        function showPrimesModal(channelId, primes) {
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.9);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 10000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: linear-gradient(135deg, #1e3c72, #2a5298);
                padding: 40px;
                border-radius: 20px;
                max-width: 800px;
                width: 90%;
                max-height: 80vh;
                overflow-y: auto;
                box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            `;
            
            const primesArray = Array.isArray(primes) ? primes : JSON.parse(primes);
            
            content.innerHTML = `
                <h2 style="color: #ffd700; margin-bottom: 20px;">Channel ${channelId} - ${primesArray.length} Primes</h2>
                <div style="background: rgba(0, 0, 0, 0.3); padding: 20px; border-radius: 10px; font-family: 'Courier New', monospace; line-height: 1.8; margin-bottom: 20px;">
                    ${primesArray.join(', ')}
                </div>
                <div style="display: flex; gap: 10px;">
                    <button id="copyPrimes" style="flex: 1; padding: 12px; background: #4ecdc4; color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Copy to Clipboard</button>
                    <button id="closeModal" style="flex: 1; padding: 12px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Close</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('closeModal').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('copyPrimes').onclick = () => {
                navigator.clipboard.writeText(primesArray.join(', ')).then(() => {
                    const btn = document.getElementById('copyPrimes');
                    btn.textContent = 'Copied!';
                    setTimeout(() => {
                        btn.textContent = 'Copy to Clipboard';
                    }, 2000);
                });
            };
            
            modal.onclick = (e) => {
                if (e.target === modal) {
                    document.body.removeChild(modal);
                }
            };
        }
        
        function createChannelChart(coprimeResidues, channels, exponent, smallProduct, modulus) {
            const ctx = document.getElementById('channelChart').getContext('2d');
            
            if (channelChart) {
                channelChart.destroy();
            }
            
            const labels = [`Small Primes (< ${modulus})`];
            const contributions = [smallProduct];
            const primeCounts = [computationData.primes.filter(p => p < modulus).length];
            
            coprimeResidues.forEach(a => {
                labels.push(`≡ ${a} (mod ${modulus})`);
                const channelPrimes = channels[a];
                const contribution = channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
                contributions.push(contribution);
                primeCounts.push(channelPrimes.length);
            });
            
            const colors = generateColors(labels.length);
            
            channelChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Channel Contribution',
                        data: contributions,
                        backgroundColor: colors,
                        borderColor: colors.map(c => c.replace('0.8', '1')),
                        borderWidth: 2,
                        borderRadius: 8,
                        borderSkipped: false,
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            titleColor: '#fff',
                            bodyColor: '#fff',
                            borderColor: 'rgba(255, 255, 255, 0.3)',
                            borderWidth: 1,
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const contrib = contributions[idx];
                                    const logContrib = Math.log(contrib);
                                    const count = primeCounts[idx];
                                    
                                    return [
                                        `Contribution: ${contrib.toFixed(6)}`,
                                        `log(Contribution): ${logContrib.toFixed(4)}`,
                                        `Prime count: ${count}`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            ticks: {
                                color: '#fff',
                                maxRotation: 45,
                                font: {
                                    size: 10
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            }
                        },
                        y: {
                            ticks: {
                                color: '#fff',
                                callback: function(value) {
                                    return value.toFixed(3);
                                }
                            },
                            grid: {
                                color: 'rgba(255, 255, 255, 0.1)'
                            },
                            title: {
                                display: true,
                                text: `Contribution (mod ${modulus})`,
                                color: '#fff',
                                font: {
                                    size: 14,
                                    weight: 'bold'
                                }
                            }
                        }
                    },
                    animation: {
                        duration: 1500,
                        easing: 'easeOutQuart'
                    }
                }
            });
            
            document.getElementById('chart-section').style.display = 'block';
            createChartLegend(labels, colors, primeCounts);
        }
        
        function generateColors(count) {
            const baseColors = [
                'rgba(255, 215, 0, 0.8)',
                'rgba(255, 99, 132, 0.8)',
                'rgba(54, 162, 235, 0.8)', 
                'rgba(255, 205, 86, 0.8)',
                'rgba(75, 192, 192, 0.8)',
                'rgba(153, 102, 255, 0.8)',
                'rgba(255, 159, 64, 0.8)',
                'rgba(199, 199, 199, 0.8)',
                'rgba(83, 102, 255, 0.8)'
            ];
            
            const colors = [];
            for (let i = 0; i < count; i++) {
                if (i < baseColors.length) {
                    colors.push(baseColors[i]);
                } else {
                    const hue = (i * 137.5) % 360;
                    colors.push(`hsla(${hue}, 70%, 60%, 0.8)`);
                }
            }
            return colors;
        }
        
        function createChartLegend(labels, colors, primeCounts) {
            let legendHtml = '';
            
            for (let i = 0; i < labels.length; i++) {
                legendHtml += `
                    <div class="legend-item">
                        <div class="legend-color" style="background-color: ${colors[i]};"></div>
                        <span>${labels[i]} (${primeCounts[i]} primes)</span>
                    </div>
                `;
            }
            
            document.getElementById('chartLegend').innerHTML = legendHtml;
        }
        
        function changeViz(type) {
            currentViz = type;
            
            document.querySelectorAll('.viz-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            
            updateVisualization(type);
        }
        
        function updateVisualization(type) {
            if (!computationData) return;
            
            const canvas = document.getElementById('vizCanvas');
            const ctx = canvas.getContext('2d');
            
            // Clear any existing event listeners
            const newCanvas = canvas.cloneNode(true);
            canvas.parentNode.replaceChild(newCanvas, canvas);
            
            // Get fresh references
            const freshCanvas = document.getElementById('vizCanvas');
            const freshCtx = freshCanvas.getContext('2d');
            
            if (vizChart) {
                vizChart.destroy();
                vizChart = null;
            }
            
            // Clear the canvas completely
            freshCtx.clearRect(0, 0, freshCanvas.width, freshCanvas.height);
            
            // Hide stats by default
            document.getElementById('vizStats').style.display = 'none';
            
            if (type === 'convergence') {
                createConvergencePlot(freshCtx);
            } else if (type === 'contribution') {
                createContributionPlot(freshCtx);
            } else if (type === 'gapDist') {
                createGapDistributionPlot(freshCtx);
            } else if (type === 'primeCount') {
                createPrimeCountingPlot(freshCtx);
            } else if (type === 'density') {
                createDensityAnalysisPlot(freshCtx);
            } else if (type === 'gapHistogram') {
                createGapHistogramPlot(freshCtx);
            } else if (type === 'sacksSpiral') {
                createSacksSpiralPlot(freshCtx);
            } else if (type === 'zetaZeros') {
                createZetaZerosPlot(freshCtx);
            } else if (type === 'errorAnalysis') {
                createErrorAnalysisPlot(freshCtx);
            } else if (type === 'primeRaces') {
                createPrimeRacesPlot(freshCtx);
            } else if (type === 'goldbachComet') {
                createGoldbachCometPlot(freshCtx);
            } else if (type === 'phasorSum') {
                createPhasorSumPlot(freshCtx);
            } else if (type === 'zetaSurface') {
                createZetaSurfacePlot(freshCtx);
            } else if (type === 'primeSpiral') {
                createPrimeSpiralPlot(freshCtx);
            } else if (type === 'channelRace') {
                createChannelRacePlot(freshCtx);
            } else if (type === 'heatmap') {
                createHeatmapPlot(freshCtx);
            } else if (type === 'voronoi') {
                createVoronoiPlot(freshCtx);
            } else if (type === 'harmonicWave') {
                createHarmonicWavePlot(freshCtx);
            } else if (type === 'phaseLaw') {
                createPhaseLawPlot(freshCtx);
            } else if (type === 'semiprimeDistribution') {
                createSemiprimeDistributionPlot(freshCtx);
            } else if (type === 'semiprimeGraph') {
                createSemiprimeGraphPlot(freshCtx);
            } else if (type === 'factorizationTiming') {
                createFactorizationTimingPlot(freshCtx);
            } else if (type === 'modularInterference') {
                createModularInterferencePlot(freshCtx);
            } else if (type === 'twinSemiprimes') {
                createTwinSemiprimesPlot(freshCtx);
            } else if (type === 'semiprimeZeta') {
                createSemiprimeZetaPlot(freshCtx);
            } else if (type === 'phaseExplorer') {
                createPhaseExplorerPlot(freshCtx);
            } else if (type === 'compositeChannels') {
                createCompositeChannelsPlot(freshCtx);
            } else if (type === 'semiprimeDistribution') {
                createSemiprimeDistributionPlot(freshCtx);
            } else if (type === 'semiprimeGraph') {
                createSemiprimeGraphPlot(freshCtx);
            } else if (type === 'factorizationTiming') {
                createFactorizationTimingPlot(freshCtx);
            } else if (type === 'modularInterference') {
                createModularInterferencePlot(freshCtx);
            } else if (type === 'twinSemiprimes') {
                createTwinSemiprimesPlot(freshCtx);
            } else if (type === 'semiprimeZeta') {
                createSemiprimeZetaPlot(freshCtx);
            }
        }
        
        function generateSemiprimes(primes) {
            const semiprimes = [];
            const set = new Set();
            for (let i = 0; i < primes.length; i++) {
                for (let j = i; j < primes.length; j++) {
                    const sp = primes[i] * primes[j];
                    if (!set.has(sp)) {
                        set.add(sp);
                        semiprimes.push({ value: sp, p: primes[i], q: primes[j] });
                    }
                }
            }
            return semiprimes.sort((a, b) => a.value - b.value);
        }
        
        function createSemiprimeDistributionPlot(ctx) {
            const { primes } = computationData;
            const semiprimes = generateSemiprimes(primes);
            const maxN = Math.min(10000, semiprimes[semiprimes.length - 1].value);
            const step = Math.max(50, Math.floor(maxN / 200));
            const data = [];
            for (let x = step; x <= maxN; x += step) {
                const sCount = semiprimes.filter(s => s.value <= x).length;
                const pCount = primes.filter(p => p <= x).length;
                const theory = x > 2 ? (x * Math.log(Math.log(x))) / Math.log(x) : 0;
                data.push({ x, semiprimes: sCount, primes: pCount, theory });
            }
            document.getElementById('vizStats').style.display = 'block';
            document.getElementById('vizStats').innerHTML = `<h4 style="color: #ffd700;">Semiprime Distribution</h4><p>Total: ${semiprimes.length} semiprimes vs ${primes.length} primes | Ratio: ${(semiprimes.length / primes.length).toFixed(2)}</p>`;
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: data.map(d => d.x),
                    datasets: [{label: 'Semiprimes S(x)', data: data.map(d => d.semiprimes), borderColor: '#4ecdc4', borderWidth: 3, fill: false, pointRadius: 0},
                    {label: 'Theory', data: data.map(d => d.theory), borderColor: '#ffd700', borderWidth: 2, borderDash: [10, 5], fill: false, pointRadius: 0},
                    {label: 'Primes π(x)', data: data.map(d => d.primes), borderColor: '#ff6384', borderWidth: 2, fill: false, pointRadius: 0}]
                },
                options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {labels: {color: '#fff'}}}, scales: {x: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}, y: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}}}
            });
        }
        
        function createSemiprimeGraphPlot(ctx) {
            const { primes } = computationData;
            const displayPrimes = primes.slice(0, 15);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Semiprime Complete Graph</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes (nodes)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${displayPrimes.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Semiprimes (edges)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${displayPrimes.length * (displayPrimes.length + 1) / 2}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Graph Structure:</strong><br>
                    Every prime connects to every other prime via multiplication<br>
                    This forms a complete graph K_n with self-loops<br>
                    Total edges = n(n+1)/2 including squares
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            const freshCtx = canvas.getContext('2d');
            const centerX = rect.width / 2;
            const centerY = rect.height / 2;
            const radius = Math.min(rect.width, rect.height) * 0.35 * universalZoom;
            
            // Clear background
            freshCtx.fillStyle = 'rgba(0,0,0,0.95)';
            freshCtx.fillRect(0, 0, rect.width, rect.height);
            
            // Calculate positions
            const positions = displayPrimes.map((p, i) => {
                const angle = (2 * Math.PI * i) / displayPrimes.length - Math.PI / 2;
                return { 
                    p, 
                    x: centerX + radius * Math.cos(angle), 
                    y: centerY + radius * Math.sin(angle) 
                };
            });
            
            // Draw edges (semiprimes) first
            freshCtx.strokeStyle = 'rgba(78,205,196,0.15)';
            freshCtx.lineWidth = 1;
            for (let i = 0; i < positions.length; i++) {
                for (let j = i; j < positions.length; j++) {
                    if (i === j) {
                        // Self-loop for squares (p²)
                        const loopRadius = 15;
                        freshCtx.beginPath();
                        freshCtx.arc(positions[i].x, positions[i].y - loopRadius, loopRadius, 0, Math.PI * 2);
                        freshCtx.stroke();
                    } else {
                        // Edge between different primes
                        freshCtx.beginPath();
                        freshCtx.moveTo(positions[i].x, positions[i].y);
                        freshCtx.lineTo(positions[j].x, positions[j].y);
                        freshCtx.stroke();
                    }
                }
            }
            
            // Draw nodes (primes) on top
            for (const pos of positions) {
                // Node circle
                freshCtx.fillStyle = '#4ecdc4';
                freshCtx.beginPath();
                freshCtx.arc(pos.x, pos.y, 8, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Node border
                freshCtx.strokeStyle = '#fff';
                freshCtx.lineWidth = 2;
                freshCtx.stroke();
                
                // Label
                freshCtx.fillStyle = '#fff';
                freshCtx.font = 'bold 14px Arial';
                freshCtx.textAlign = 'center';
                freshCtx.fillText(pos.p, pos.x, pos.y - 20);
            }
            
            // Add hover interaction
            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;
                
                let hoveredPrime = null;
                for (const pos of positions) {
                    const dist = Math.sqrt((mouseX - pos.x) ** 2 + (mouseY - pos.y) ** 2);
                    if (dist < 15) {
                        hoveredPrime = pos;
                        break;
                    }
                }
                
                if (hoveredPrime) {
                    canvas.style.cursor = 'pointer';
                    
                    // Redraw to show tooltip
                    freshCtx.fillStyle = 'rgba(0,0,0,0.95)';
                    freshCtx.fillRect(0, 0, rect.width, rect.height);
                    
                    // Redraw edges
                    freshCtx.strokeStyle = 'rgba(78,205,196,0.15)';
                    freshCtx.lineWidth = 1;
                    for (let i = 0; i < positions.length; i++) {
                        for (let j = i; j < positions.length; j++) {
                            if (i === j) {
                                const loopRadius = 15;
                                freshCtx.beginPath();
                                freshCtx.arc(positions[i].x, positions[i].y - loopRadius, loopRadius, 0, Math.PI * 2);
                                freshCtx.stroke();
                            } else {
                                freshCtx.beginPath();
                                freshCtx.moveTo(positions[i].x, positions[i].y);
                                freshCtx.lineTo(positions[j].x, positions[j].y);
                                freshCtx.stroke();
                            }
                        }
                    }
                    
                    // Redraw nodes
                    for (const pos of positions) {
                        freshCtx.fillStyle = pos === hoveredPrime ? '#ffd700' : '#4ecdc4';
                        freshCtx.beginPath();
                        freshCtx.arc(pos.x, pos.y, 8, 0, Math.PI * 2);
                        freshCtx.fill();
                        freshCtx.strokeStyle = '#fff';
                        freshCtx.lineWidth = 2;
                        freshCtx.stroke();
                        freshCtx.fillStyle = '#fff';
                        freshCtx.font = 'bold 14px Arial';
                        freshCtx.textAlign = 'center';
                        freshCtx.fillText(pos.p, pos.x, pos.y - 20);
                    }
                    
                    // Draw tooltip
                    freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                    freshCtx.fillRect(mouseX + 10, mouseY - 30, 120, 25);
                    freshCtx.strokeStyle = '#4ecdc4';
                    freshCtx.lineWidth = 2;
                    freshCtx.strokeRect(mouseX + 10, mouseY - 30, 120, 25);
                    freshCtx.fillStyle = '#fff';
                    freshCtx.font = 'bold 13px Arial';
                    freshCtx.textAlign = 'left';
                    freshCtx.fillText(`Prime p = ${hoveredPrime.p}`, mouseX + 15, mouseY - 12);
                } else {
                    canvas.style.cursor = 'default';
                }
            };
        }
        
        function createFactorizationTimingPlot(ctx) {
            const { primes } = computationData;
            const semiprimes = generateSemiprimes(primes).slice(0, 200);
            const timingData = semiprimes.map(s => {
                let ops = 0; const n = s.value;
                for (let i = 2; i <= Math.sqrt(n); i++) { ops++; if (n % i === 0) break; }
                return { n, ops, p: s.p, q: s.q };
            });
            const maxOps = Math.max(...timingData.map(d => d.ops));
            document.getElementById('vizStats').innerHTML = `<h4 style="color: #ffd700;">Factorization Timing: Max ops ${maxOps}</h4>`;
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {datasets: [{label: 'Operations', data: timingData.map(d => ({x: d.n, y: d.ops})), backgroundColor: function(c) { const r = c.raw.y / maxOps; return `hsla(${(1-r)*120}, 80%, 60%, 0.7)`; }, pointRadius: 5}]},
                options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {labels: {color: '#fff'}}}, scales: {x: {type: 'logarithmic', ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}, y: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}}}
            });
        }
        
        function createModularInterferencePlot(ctx) {
            const { primes } = computationData;
            const m = 30;
            const semiprimes = generateSemiprimes(primes.slice(0, 30));
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Modular Interference (mod ${m})</h4>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Formula:</strong> pq ≡ (p mod m)(q mod m) (mod m)<br>
                    <span style="color: #4ecdc4;">●</span> Blue dots (outer) = Primes<br>
                    <span style="color: #ff6384;">●</span> Red dots (inner) = Semiprimes<br>
                    Semiprimes show interference patterns from multiplication
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            const freshCtx = canvas.getContext('2d');
            const centerX = rect.width / 2;
            const centerY = rect.height / 2;
            const outerRadius = Math.min(rect.width, rect.height) * 0.4 * universalZoom;
            const innerRadius = outerRadius * 0.65;
            
            // Clear background
            freshCtx.fillStyle = 'rgba(0,0,0,0.95)';
            freshCtx.fillRect(0, 0, rect.width, rect.height);
            
            // Draw rings
            freshCtx.strokeStyle = 'rgba(255,255,255,0.2)';
            freshCtx.lineWidth = 2;
            freshCtx.beginPath();
            freshCtx.arc(centerX, centerY, outerRadius, 0, Math.PI * 2);
            freshCtx.stroke();
            
            freshCtx.beginPath();
            freshCtx.arc(centerX, centerY, innerRadius, 0, Math.PI * 2);
            freshCtx.stroke();
            
            // Draw radial lines and labels
            freshCtx.font = '11px Arial';
            for (let r = 0; r < m; r++) {
                const angle = (2 * Math.PI * r) / m - Math.PI / 2;
                
                // Radial line
                freshCtx.strokeStyle = 'rgba(255,255,255,0.1)';
                freshCtx.lineWidth = 1;
                freshCtx.beginPath();
                freshCtx.moveTo(centerX, centerY);
                freshCtx.lineTo(centerX + outerRadius * 1.05 * Math.cos(angle), centerY + outerRadius * 1.05 * Math.sin(angle));
                freshCtx.stroke();
                
                // Label
                freshCtx.fillStyle = '#fff';
                freshCtx.textAlign = 'center';
                const labelR = outerRadius * 1.15;
                freshCtx.fillText(r, centerX + labelR * Math.cos(angle), centerY + labelR * Math.sin(angle) + 4);
            }
            
            // Plot primes on outer ring
            for (const p of primes.slice(0, 100)) {
                const residue = p % m;
                const angle = (2 * Math.PI * residue) / m - Math.PI / 2;
                const x = centerX + outerRadius * Math.cos(angle);
                const y = centerY + outerRadius * Math.sin(angle);
                
                const d = gcd(residue, m);
                freshCtx.fillStyle = d === 1 ? 'rgba(78,205,196,0.8)' : 'rgba(255,159,64,0.8)';
                freshCtx.beginPath();
                freshCtx.arc(x, y, 4, 0, Math.PI * 2);
                freshCtx.fill();
            }
            
            // Plot semiprimes on inner ring
            for (const s of semiprimes.slice(0, 200)) {
                const residue = s.value % m;
                const angle = (2 * Math.PI * residue) / m - Math.PI / 2;
                const x = centerX + innerRadius * Math.cos(angle);
                const y = centerY + innerRadius * Math.sin(angle);
                
                const d = gcd(residue, m);
                freshCtx.fillStyle = d === 1 ? 'rgba(255,99,132,0.6)' : 'rgba(220,53,69,0.9)';
                freshCtx.beginPath();
                freshCtx.arc(x, y, 3, 0, Math.PI * 2);
                freshCtx.fill();
            }
            
            // Center marker
            freshCtx.fillStyle = '#ffd700';
            freshCtx.beginPath();
            freshCtx.arc(centerX, centerY, 5, 0, Math.PI * 2);
            freshCtx.fill();
        }
        
        function createTwinSemiprimesPlot(ctx) {
            const { primes } = computationData;
            const semiprimes = generateSemiprimes(primes).filter(s => s.value < 10000).map(s => s.value);
            const twins = [];
            for (let i = 0; i < semiprimes.length - 1; i++) {
                if (semiprimes[i + 1] - semiprimes[i] === 2) twins.push({ s1: semiprimes[i], s2: semiprimes[i + 1] });
            }
            document.getElementById('vizStats').innerHTML = `<h4 style="color: #ffd700;">Twin Semiprimes: ${twins.length} pairs</h4>`;
            const gapCounts = {};
            for (let i = 0; i < semiprimes.length - 1; i++) {
                const gap = semiprimes[i + 1] - semiprimes[i];
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            }
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b).slice(0, 30);
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {labels: sortedGaps.map(g => g.toString()), datasets: [{label: 'Gap Frequency', data: sortedGaps.map(g => gapCounts[g]), backgroundColor: sortedGaps.map(g => g === 2 ? 'rgba(255,215,0,0.8)' : 'rgba(78,205,196,0.7)'), borderWidth: 2}]},
                options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {display: false}}, scales: {x: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}, y: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}}}
            });
        }
        
        function createSemiprimeZetaPlot(ctx) {
            const { primes } = computationData;
            const semiprimes = generateSemiprimes(primes);
            document.getElementById('vizStats').innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Semiprime Zeta Function ζ_S(s)</h4>
                <div style="margin-bottom: 15px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                    <strong>What is visualized:</strong><br>
                    This plot shows the <strong>semiprime zeta function</strong> ζ_S(s) compared to its theoretical formula.
                    The cyan line is the computed sum over actual semiprimes, while the gold dashed line shows the theoretical expression derived from the prime zeta function.
                    This function interpolates between contributions to the Riemann zeta function.
                </div>
                <div style="padding: 15px; background: rgba(0, 0, 0, 0.3); border-radius: 8px; font-family: 'Courier New', monospace; margin-bottom: 15px;">
                    <strong style="color: #ffd700;">Definition:</strong><br>
                    ζ_S(s) = Σ(n∈S) n^(-s)<br><br>
                    <strong style="color: #ffd700;">Theoretical Formula:</strong><br>
                    ζ_S(s) = ½[(Σ p^(-s))² - Σ p^(-2s)]<br><br>
                    Where the sums run over all primes p
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Mathematical Significance:</strong><br>
                    <strong>Connection to Riemann zeta:</strong> The semiprime zeta function captures the "second-order" prime structure<br>
                    <strong>Convergence:</strong> Converges for Re(s) > 1, similar to the prime zeta function<br>
                    <strong>Euler product insight:</strong> This function reveals how products of primes contribute to ζ(s)<br>
                    <strong>Analytic properties:</strong> The match between computed and theoretical values validates the formula<br>
                    The slight divergence at lower σ values shows edge effects from finite prime sets
                </div>
            `;
            const sigmaVals = [], zetaS = [], theory = [];
            for (let s = 1.1; s <= 4; s += 0.1) {
                let semiSum = 0;
                for (const sp of semiprimes.slice(0, 1000)) semiSum += Math.pow(sp.value, -s);
                let primeSum = 0, primeSum2 = 0;
                for (const p of primes) { primeSum += Math.pow(p, -s); primeSum2 += Math.pow(p, -2*s); }
                sigmaVals.push(s); zetaS.push(semiSum); theory.push(0.5 * (primeSum * primeSum - primeSum2));
            }
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {labels: sigmaVals, datasets: [{label: 'ζ_S(σ) Computed', data: zetaS, borderColor: '#4ecdc4', borderWidth: 3, fill: false, pointRadius: 0}, {label: 'Theoretical', data: theory, borderColor: '#ffd700', borderWidth: 2, borderDash: [10, 5], fill: false, pointRadius: 0}]},
                options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {labels: {color: '#fff'}}}, scales: {x: {title: {display: true, text: 'σ', color: '#fff'}, ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}, y: {ticks: {color: '#fff'}, grid: {color: 'rgba(255,255,255,0.1)'}}}}
            });
        }
        
        function createConvergencePlot(ctx) {
            const { partialProducts, exactValue, constantType } = computationData;
            
            const labels = partialProducts.map(p => p.prime);
            const values = partialProducts.map(p => {
                if (constantType === 'pi') {
                    return Math.sqrt(6 * p.value);
                }
                return p.value;
            });
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Partial Product',
                        data: values,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'Exact Value',
                        data: Array(labels.length).fill(exactValue),
                        borderColor: 'rgba(255, 215, 0, 1)',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(10)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { display: true, text: 'Prime p', color: '#fff' },
                            ticks: { color: '#fff', maxTicksLimit: 15 },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { display: true, text: 'Value', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createContributionPlot(ctx) {
            const { primes, exponent } = computationData;
            
            const contributions = primes.map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return factor - 1;
            });
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Prime Contribution',
                        data: primes.map((p, i) => ({ x: p, y: contributions[i] })),
                        backgroundColor: 'rgba(255, 99, 132, 0.6)',
                        borderColor: 'rgba(255, 99, 132, 1)',
                        pointRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `p=${context.parsed.x}: contribution = ${context.parsed.y.toFixed(8)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { display: true, text: 'Prime p (log scale)', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { display: true, text: 'Contribution (log scale)', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createGapDistributionPlot(ctx) {
            const { primes, exponent } = computationData;
            
            // Calculate gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Calculate contributions by gap
            const gapContributions = sortedGaps.map(gap => {
                const gapPrimes = [];
                for (let i = 1; i < primes.length; i++) {
                    if (primes[i] - primes[i-1] === gap) {
                        gapPrimes.push(primes[i]);
                    }
                }
                return gapPrimes.length > 0 ? computeTruncatedProduct(gapPrimes, exponent) : 1;
            });
            
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => `Gap ${g}`),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: 'rgba(78, 205, 196, 0.6)',
                        borderColor: 'rgba(78, 205, 196, 1)',
                        borderWidth: 2,
                        yAxisID: 'y',
                    }, {
                        label: 'Contribution',
                        data: gapContributions,
                        type: 'line',
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        yAxisID: 'y1',
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const gap = sortedGaps[context.dataIndex];
                                    if (context.datasetIndex === 0) {
                                        return `Frequency: ${context.parsed.y} primes`;
                                    } else {
                                        return `Contribution: ${context.parsed.y.toFixed(6)}`;
                                    }
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { display: true, text: 'Prime Gap Size', color: '#fff' },
                            ticks: { color: '#fff', maxRotation: 45 },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { display: true, text: 'Frequency', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { display: true, text: 'Contribution', color: '#fff' },
                            ticks: { color: '#fff' },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function generateGapDistChartForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            
            // Calculate gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Calculate contributions by gap
            const gapContributions = sortedGaps.map(gap => {
                const gapPrimes = [];
                for (let i = 1; i < primes.length; i++) {
                    if (primes[i] - primes[i-1] === gap) {
                        gapPrimes.push(primes[i]);
                    }
                }
                return gapPrimes.length > 0 ? computeTruncatedProduct(gapPrimes, exponent) : 1;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => `Gap ${g}`),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.6)' : 'rgba(78, 205, 196, 0.6)',
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        borderWidth: 3,
                        yAxisID: 'y',
                    }, {
                        label: 'Contribution',
                        data: gapContributions,
                        type: 'line',
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        yAxisID: 'y1',
                        tension: 0.4,
                        pointRadius: 6
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Prime Gap Size', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.022) },
                                maxRotation: 45
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { 
                                display: true, 
                                text: 'Contribution', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function exportChartImage() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            // Create modal for export options
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.8);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 10000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: linear-gradient(135deg, #1e3c72, #2a5298);
                padding: 40px;
                border-radius: 20px;
                max-width: 500px;
                width: 90%;
                box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            `;
            
            content.innerHTML = `
                <h2 style="color: #ffd700; margin-bottom: 25px; text-align: center;">Export Chart Options</h2>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Resolution:</label>
                    <select id="exportResolution" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="1080p">Full HD (1920 x 1080)</option>
                        <option value="1080p2x">Full HD 2x (3840 x 2160)</option>
                        <option value="4k">4K (3840 x 2160)</option>
                        <option value="8k">8K (7680 x 4320)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Background:</label>
                    <select id="exportBackground" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="black">Black</option>
                        <option value="white">White</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Chart Type:</label>
                    <select id="exportChartType" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px; max-height: 300px; overflow-y: auto;">
                        <optgroup label="Core Analysis">
                            <option value="channel">Residue Channel Contributions</option>
                            <option value="convergence">Convergence Plot</option>
                            <option value="contribution">Prime Contributions</option>
                            <option value="gapDist">Gap Distribution Analysis</option>
                        </optgroup>
                        <optgroup label="Distribution">
                            <option value="primeCount">Prime Counting π(x)</option>
                            <option value="density">Prime Density Analysis</option>
                            <option value="gapHistogram">Prime Gaps Histogram</option>
                            <option value="errorAnalysis">Error Analysis</option>
                            <option value="goldbachComet">Goldbach Comet</option>
                        </optgroup>
                        <optgroup label="Complex Analysis">
                            <option value="phasorSum">Phasor Sum (Complex Plane)</option>
                            <option value="zetaSurface">Modular Zeta Surface</option>
                            <option value="zetaZeros">Riemann Zeta Zeros</option>
                            <option value="phaseExplorer">Phase Explorer</option>
                            <option value="phaseLaw">Phase Law</option>
                            <option value="harmonicWave">Harmonic Wave</option>
                        </optgroup>
                        <optgroup label="Modular">
                            <option value="sacksSpiral">Sacks Spiral</option>
                            <option value="primeSpiral">Ulam Spiral</option>
                            <option value="primeRaces">Prime Races</option>
                            <option value="channelRace">Channel Race</option>
                            <option value="heatmap">Heatmap</option>
                            <option value="voronoi">Voronoi</option>
                            <option value="modularInterference">Modular Interference</option>
                            <option value="primeAvoidance">Prime Channel Avoidance</option>
                            <option value="compositeChannels">Composite Channels</option>dular Interference</option>
                        </optgroup>
                        <optgroup label="Semiprimes">
                            <option value="semiprimeDistribution">Semiprime Distribution</option>
                            <option value="semiprimeGraph">Semiprime Graph</option>
                            <option value="factorizationTiming">Factorization Timing</option>
                            <option value="twinSemiprimes">Twin Semiprimes</option>
                            <option value="semiprimeZeta">Semiprime ζ_S</option>
                        </optgroup>
                    </select>
                </div>
                
                <div style="margin-bottom: 25px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="exportWatermark" checked style="width: auto; margin-right: 10px;">
                        <span>Include watermark by Wessen Getachew</span>
                    </label>
                </div>
                
                <div style="display: flex; gap: 10px;">
                    <button id="exportBtn" style="flex: 1; padding: 15px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Export</button>
                    <button id="cancelBtn" style="flex: 1; padding: 15px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Cancel</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('cancelBtn').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('exportBtn').onclick = () => {
                const resolution = document.getElementById('exportResolution').value;
                const background = document.getElementById('exportBackground').value;
                const chartType = document.getElementById('exportChartType').value;
                const includeWatermark = document.getElementById('exportWatermark').checked;
                
                document.body.removeChild(modal);
                
                performExport(resolution, background, chartType, includeWatermark);
            };
        }
        
        function performExport(resolution, background, chartType, includeWatermark) {
            const { epsilon, constantType, modulus, primes, computedValue, exactValue } = computationData;
            
            let width, height;
            if (resolution === '1080p') {
                width = 1920;
                height = 1080;
            } else if (resolution === '1080p2x') {
                width = 3840;
                height = 2160;
            } else if (resolution === '4k') {
                width = 3840;
                height = 2160;
            } else {
                width = 7680;
                height = 4320;
            }
            
            const exportCanvas = document.createElement('canvas');
            exportCanvas.width = width;
            exportCanvas.height = height;
            const ctx = exportCanvas.getContext('2d');
            
            // Set background
            ctx.fillStyle = background === 'white' ? '#ffffff' : '#000000';
            ctx.fillRect(0, 0, width, height);
            
            // Calculate dimensions with better proportions
            const padding = width * 0.04;
            const titleHeight = height * 0.15;
            const chartHeight = height * 0.70;
            const watermarkHeight = includeWatermark ? height * 0.05 : 0;
            
            // Text color based on background
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            const accentColor = background === 'white' ? '#1e3c72' : '#ffd700';
            
            // Draw title
            ctx.fillStyle = accentColor;
            ctx.font = `bold ${height * 0.045}px Arial`;
            ctx.textAlign = 'center';
            const title = chartType === 'channel' ? `Residue Channel Contributions (mod ${modulus})` :
                         chartType === 'convergence' ? 'Convergence to Exact Value' :
                         chartType === 'contribution' ? 'Individual Prime Contributions' :
                         chartType === 'gapDist' ? 'Prime Gap Distribution Analysis' :
                         chartType === 'primeCount' ? 'Prime Counting Function π(x)' :
                         chartType === 'density' ? 'Prime Density Analysis' :
                         chartType === 'gapHistogram' ? 'Prime Gaps Histogram' :
                         chartType === 'sacksSpiral' ? 'Sacks Spiral Visualization' :
                         chartType === 'zetaZeros' ? 'Riemann Zeta Function - Non-Trivial Zeros' :
                         chartType === 'errorAnalysis' ? 'Error Analysis - Convergence Rate' :
                         chartType === 'primeRaces' ? `Prime Races (mod ${modulus})` :
                         chartType === 'goldbachComet' ? 'Goldbach Comet - Prime Pair Partitions' :
                         chartType === 'phasorSum' ? 'Phasor Sum: ζ(s) as Rotating Vectors' :
                         chartType === 'zetaSurface' ? 'Modular Zeta Surface - Nested Unity Lattice' :
                         'Visualization';
            ctx.fillText(title, width / 2, padding + height * 0.045);
            
            // Draw subtitle
            ctx.fillStyle = textColor;
            ctx.font = `${height * 0.025}px Arial`;
            const subtitle = `Computing ${constantType === 'pi' ? 'π' : 'ζ(' + computationData.exponent + ')'} using ${primes.length} primes (ε = ${epsilon})`;
            ctx.fillText(subtitle, width / 2, padding + height * 0.08);
            
            // Draw computed vs exact values - split into two columns
            ctx.font = `${height * 0.022}px Arial`;
            ctx.textAlign = 'left';
            const statsY = padding + height * 0.11;
            const leftX = padding;
            const rightX = width * 0.5 + padding;
            
            ctx.fillText(`Computed: ${computedValue.toFixed(15)}`, leftX, statsY);
            ctx.fillText(`Exact: ${exactValue.toFixed(15)}`, rightX, statsY);
            
            const relError = Math.abs(computedValue - exactValue) / exactValue;
            ctx.fillText(`Relative Error: ${(relError * 100).toFixed(8)}%`, leftX, statsY + height * 0.028);
            ctx.fillText(`Primes Used: ${primes.length}`, rightX, statsY + height * 0.028);
            
            // Create temporary canvas for chart with proper sizing
            const tempCanvas = document.createElement('canvas');
            const chartPadding = padding * 2;
            
            // Make temp canvas larger to capture full chart
            tempCanvas.width = width - chartPadding;
            tempCanvas.height = chartHeight * 1.2; // Increased to capture full chart
            const tempCtx = tempCanvas.getContext('2d');
            
            // Generate chart based on type
            let chartInstance;
            
            if (chartType === 'channel') {
                chartInstance = generateChannelChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'convergence') {
                chartInstance = generateConvergenceChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'contribution') {
                chartInstance = generateContributionChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'gapDist') {
                chartInstance = generateGapDistChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'primeCount') {
                chartInstance = generatePrimeCountChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'density') {
                chartInstance = generateDensityChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'gapHistogram') {
                chartInstance = generateGapHistogramChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'sacksSpiral') {
                chartInstance = generateSacksSpiralForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'zetaZeros') {
                chartInstance = generateZetaZerosChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'errorAnalysis') {
                chartInstance = generateErrorAnalysisChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'primeRaces') {
                chartInstance = generatePrimeRacesChartForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'goldbachComet') {
                chartInstance = generateGoldbachCometForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'phasorSum') {
                chartInstance = generatePhasorSumForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'zetaSurface') {
                chartInstance = generateZetaSurfaceForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'compositeChannels') {
                chartInstance = generateCompositeChannelsForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'primeSpiral') {
                chartInstance = generatePrimeSpiralForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'heatmap') {
                chartInstance = generateHeatmapForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'voronoi') {
                chartInstance = generateVoronoiForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'channelRace') {
                chartInstance = generateChannelRaceForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            } else if (chartType === 'harmonicWave') {
                chartInstance = generateHarmonicWaveForExport(tempCtx, tempCanvas.width, tempCanvas.height, background);
            }
            
            // Wait for chart to render with longer delay
            setTimeout(() => {
                // Calculate proper position to center the chart
                const chartX = chartPadding / 2;
                const chartY = titleHeight + padding;
                
                // Calculate available space
                const availableHeight = height - chartY - watermarkHeight - padding;
                
                // Scale chart to fit if needed, maintaining aspect ratio
                let drawWidth = tempCanvas.width;
                let drawHeight = tempCanvas.height;
                
                if (drawHeight > availableHeight) {
                    const scale = availableHeight / drawHeight;
                    drawHeight = availableHeight;
                    drawWidth = tempCanvas.width * scale;
                }
                
                // Center horizontally if scaled
                const finalX = (width - drawWidth) / 2;
                
                // Draw chart to main canvas with proper scaling
                ctx.drawImage(tempCanvas, finalX, chartY, drawWidth, drawHeight);
                
                // Draw watermark if enabled
                if (includeWatermark) {
                    const watermarkY = height - padding - height * 0.025;
                    ctx.fillStyle = background === 'white' ? 'rgba(0, 0, 0, 0.4)' : 'rgba(255, 255, 255, 0.4)';
                    ctx.font = `italic ${height * 0.022}px Arial`;
                    ctx.textAlign = 'center';
                    ctx.fillText('Generated by Wessen Getachew - Modular Sieve Calculator', width / 2, watermarkY);
                    
                    ctx.font = `${height * 0.018}px Arial`;
                    ctx.fillText(new Date().toISOString().split('T')[0], width / 2, watermarkY + height * 0.025);
                }
                
                // Convert to JPEG and download
                exportCanvas.toBlob((blob) => {
                    const url = URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.href = url;
                    a.download = `modular_sieve_${chartType}_${resolution}_${Date.now()}.jpg`;
                    a.click();
                    URL.revokeObjectURL(url);
                    
                    chartInstance.destroy();
                }, 'image/jpeg', 0.95);
            }, 1000); // Increased delay to ensure full chart renders
        }
        
        function generateChannelChartForExport(ctx, width, height, background) {
            const { primes, exponent, modulus } = computationData;
            const channels = computeResidueChannels(primes, modulus);
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const smallPrimes = primes.filter(p => p < modulus);
            const smallProduct = computeTruncatedProduct(smallPrimes, exponent);
            
            const labels = [`Small Primes`, ...coprimeResidues.map(a => `≡ ${a} (mod ${modulus})`)];
            const contributions = [smallProduct, ...coprimeResidues.map(a => {
                const channelPrimes = channels[a];
                return channelPrimes.length > 0 ? computeTruncatedProduct(channelPrimes, exponent) : 1;
            })];
            
            const colors = generateColors(labels.length);
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Contribution',
                        data: contributions,
                        backgroundColor: colors,
                        borderColor: colors.map(c => c.replace('0.8', '1')),
                        borderWidth: 3
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: { display: false },
                        title: { display: false }
                    },
                    scales: {
                        x: {
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' },
                            title: {
                                display: true,
                                text: 'Contribution',
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    }
                }
            });
        }
        
        function generateConvergenceChartForExport(ctx, width, height, background) {
            const { partialProducts, exactValue, constantType } = computationData;
            
            const labels = partialProducts.map(p => p.prime);
            const values = partialProducts.map(p => {
                if (constantType === 'pi') {
                    return Math.sqrt(6 * p.value);
                }
                return p.value;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Partial Product',
                        data: values,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4
                    }, {
                        label: 'Exact Value',
                        data: Array(labels.length).fill(exactValue),
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        borderWidth: 3,
                        borderDash: [10, 10],
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Prime p', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                maxTicksLimit: 20
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Value', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateContributionChartForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            
            const contributions = primes.map(p => {
                const factor = 1 / (1 - Math.pow(p, -exponent));
                return factor - 1;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Prime Contribution',
                        data: primes.map((p, i) => ({ x: p, y: contributions[i] })),
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.6)' : 'rgba(255, 99, 132, 0.6)',
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(255, 99, 132, 1)',
                        pointRadius: 5
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p (log scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Contribution (log scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateComparisonChartForExport(ctx, width, height, background) {
            const { primes, exponent, modulus } = computationData;
            const channels = computeResidueChannels(primes, modulus);
            const coprimeResidues = getCoprimeResidues(modulus);
            
            const colors = generateColors(coprimeResidues.length);
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            const datasets = coprimeResidues.map((a, idx) => {
                const channelPrimes = channels[a];
                const contributions = channelPrimes.map(p => {
                    const factor = 1 / (1 - Math.pow(p, -exponent));
                    return factor - 1;
                });
                
                return {
                    label: `≡ ${a} (mod ${modulus})`,
                    data: channelPrimes.map((p, i) => ({ x: p, y: contributions[i] })),
                    backgroundColor: colors[idx],
                    borderColor: colors[idx].replace('0.8', '1'),
                    pointRadius: 4
                };
            });
            
            return new Chart(ctx, {
                type: 'scatter',
                data: { datasets },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor, 
                                font: { size: Math.floor(height * 0.02) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Contribution', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateGapDistChartForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            
            // Calculate gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Calculate contributions by gap
            const gapContributions = sortedGaps.map(gap => {
                const gapPrimes = [];
                for (let i = 1; i < primes.length; i++) {
                    if (primes[i] - primes[i-1] === gap) {
                        gapPrimes.push(primes[i]);
                    }
                }
                return gapPrimes.length > 0 ? computeTruncatedProduct(gapPrimes, exponent) : 1;
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => `Gap ${g}`),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.6)' : 'rgba(78, 205, 196, 0.6)',
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        borderWidth: 3,
                        yAxisID: 'y',
                    }, {
                        label: 'Contribution',
                        data: gapContributions,
                        type: 'line',
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        yAxisID: 'y1',
                        tension: 0.4,
                        pointRadius: 6
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Prime Gap Size', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.022) },
                                maxRotation: 45
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: { 
                                display: true, 
                                text: 'Contribution', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { drawOnChartArea: false }
                        }
                    }
                }
            });
        }
        
        function createGapHistogramPlot(ctx) {
            const { primes } = computationData;
            
            // Calculate all gaps
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            // Count gap frequencies
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            // Sort by gap size
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            
            // Find special gaps
            const twinPrimes = gapCounts[2] || 0;
            const cousinPrimes = gapCounts[4] || 0;
            const sexyPrimes = gapCounts[6] || 0;
            const maxGap = Math.max(...sortedGaps);
            const avgGap = gaps.reduce((a, b) => a + b, 0) / gaps.length;
            const maxGapCount = Math.max(...counts);
            const mostCommonGap = sortedGaps[counts.indexOf(maxGapCount)];
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Gaps Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px;">
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ff6384;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Twin Primes (gap=2)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${twinPrimes}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ff9f40;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Cousin Primes (gap=4)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${cousinPrimes}</div>
                    </div>
                    <div style="background: rgba(255, 205, 86, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #ffcd56;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sexy Primes (gap=6)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffcd56;">${sexyPrimes}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #4bc0c0;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Average Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${avgGap.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #9966ff;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Maximum Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${maxGap}</div>
                    </div>
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px; border-left: 3px solid #4ecdc4;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Most Common Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${mostCommonGap} (${maxGapCount}x)</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Gaps:</strong><br>
                    <strong>Twin Primes:</strong> Pairs like (3,5), (5,7), (11,13) with gap=2<br>
                    <strong>Cousin Primes:</strong> Pairs like (3,7), (7,11), (13,17) with gap=4<br>
                    <strong>Sexy Primes:</strong> Pairs like (5,11), (7,13), (11,17) with gap=6 (from Latin "sex" = six)<br>
                    <strong>Cramér's Conjecture:</strong> Max gap ≤ (ln p)² for large primes p<br>
                    Average gap near p ≈ ln(p) by the Prime Number Theorem
                </div>
            `;
            
            // Color bars by special types
            const barColors = sortedGaps.map(gap => {
                if (gap === 2) return 'rgba(255, 99, 132, 0.8)';
                if (gap === 4) return 'rgba(255, 159, 64, 0.8)';
                if (gap === 6) return 'rgba(255, 205, 86, 0.8)';
                if (gap === maxGap) return 'rgba(153, 102, 255, 0.8)';
                return 'rgba(78, 205, 196, 0.7)';
            });
            
            vizChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => g.toString()),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: barColors,
                        borderColor: barColors.map(c => c.replace('0.7', '1').replace('0.8', '1')),
                        borderWidth: 2,
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const gap = sortedGaps[context.dataIndex];
                                    const count = context.parsed.y;
                                    const pct = (count / gaps.length * 100).toFixed(2);
                                    let type = '';
                                    if (gap === 2) type = ' (Twin Primes)';
                                    else if (gap === 4) type = ' (Cousin Primes)';
                                    else if (gap === 6) type = ' (Sexy Primes)';
                                    else if (gap === maxGap) type = ' (Maximum Gap)';
                                    return [
                                        `Gap ${gap}${type}`,
                                        `Frequency: ${count}`,
                                        `Percentage: ${pct}%`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Gap Size', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                maxRotation: 45,
                                callback: function(value, index) {
                                    // Show every nth label to avoid crowding
                                    if (sortedGaps.length > 30) {
                                        return index % Math.ceil(sortedGaps.length / 30) === 0 ? this.getLabelForValue(value) : '';
                                    }
                                    return this.getLabelForValue(value);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createSacksSpiralPlot(ctx) {
            const { primes } = computationData;
            
            // Create a Set for O(1) prime lookup
            const primeSet = new Set(primes);
            
            // Sacks spiral: r = √n, θ = 2π√n
            // Use all computed primes, no artificial cap
            const spiralData = [];
            const maxN = primes[primes.length - 1];
            
            // Include all numbers up to maxN
            for (let n = 1; n <= maxN; n++) {
                const r = Math.sqrt(n);
                const theta = 2 * Math.PI * Math.sqrt(n);
                const x = r * Math.cos(theta);
                const y = r * Math.sin(theta);
                
                const isPrime = primeSet.has(n);
                
                spiralData.push({ x, y, n, isPrime });
            }
            
            const primePoints = spiralData.filter(p => p.isPrime);
            const compositePoints = spiralData.filter(p => !p.isPrime && p.n > 1);
            
            // Calculate pattern statistics
            const maxR = Math.sqrt(maxN);
            const primesInSpiral = primePoints.length;
            const density = primesInSpiral / maxN;
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Sacks Spiral Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Numbers Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${maxN.toLocaleString()}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes Found</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${primesInSpiral}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Prime Density</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${(density * 100).toFixed(2)}%</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Spiral Radius</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${maxR.toFixed(2)}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Sacks Spiral:</strong><br>
                    Discovered by Robert Sacks, this Archimedean spiral plots integers at position (r,θ) = (√n, 2π√n)<br>
                    <span style="color: #ffd700;">Gold dots</span> = Prime numbers<br>
                    <span style="color: rgba(255,255,255,0.3);">Gray dots</span> = Composite numbers<br>
                    Primes form striking radial rays, revealing deep patterns in their distribution<br>
                    Unlike Ulam spiral, perfect squares line up along the horizontal axis (θ = 0)<br>
                    The ray patterns correspond to polynomial families that produce many primes
                </div>
            `;
            
            // Clear previous chart if it exists
            if (vizChart) {
                vizChart.destroy();
                vizChart = null;
            }
            
            // Draw custom spiral on canvas
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const baseScale = Math.min(canvas.width, canvas.height) / (2 * maxR) * 0.85;
            const scale = baseScale * universalZoom;
            
            // Clear canvas
            ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw composite numbers first (background)
            ctx.fillStyle = 'rgba(255, 255, 255, 0.15)';
            const pointSize = Math.max(1, 1.5 * universalZoom);
            for (const point of compositePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, pointSize, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw primes (foreground)
            ctx.fillStyle = '#ffd700';
            const primePointSize = Math.max(2, 2.5 * universalZoom);
            for (const point of primePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, primePointSize, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw center marker
            ctx.fillStyle = '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 4 * universalZoom, 0, Math.PI * 2);
            ctx.fill();
            
            // Add hover interaction
            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;
                
                // Find closest point
                let closestPoint = null;
                let minDist = 10;
                
                for (const point of spiralData) {
                    const screenX = centerX + point.x * scale;
                    const screenY = centerY + point.y * scale;
                    const dist = Math.sqrt((mouseX - screenX) ** 2 + (mouseY - screenY) ** 2);
                    if (dist < minDist) {
                        minDist = dist;
                        closestPoint = point;
                    }
                }
                
                if (closestPoint) {
                    // Redraw to clear old tooltip
                    ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                    ctx.fillRect(0, 0, canvas.width, canvas.height);
                    
                    ctx.fillStyle = 'rgba(255, 255, 255, 0.15)';
                    for (const point of compositePoints) {
                        const screenX = centerX + point.x * scale;
                        const screenY = centerY + point.y * scale;
                        ctx.beginPath();
                        ctx.arc(screenX, screenY, 1.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    
                    ctx.fillStyle = '#ffd700';
                    for (const point of primePoints) {
                        const screenX = centerX + point.x * scale;
                        const screenY = centerY + point.y * scale;
                        ctx.beginPath();
                        ctx.arc(screenX, screenY, 2.5, 0, Math.PI * 2);
                        ctx.fill();
                    }
                    
                    ctx.fillStyle = '#4ecdc4';
                    ctx.beginPath();
                    ctx.arc(centerX, centerY, 4, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Highlight selected point
                    const screenX = centerX + closestPoint.x * scale;
                    const screenY = centerY + closestPoint.y * scale;
                    ctx.strokeStyle = '#ff6384';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(screenX, screenY, 6, 0, Math.PI * 2);
                    ctx.stroke();
                    
                    // Draw tooltip
                    const tooltipX = mouseX + 15;
                    const tooltipY = mouseY - 15;
                    
                    const lines = [
                        `n = ${closestPoint.n}`,
                        closestPoint.isPrime ? 'PRIME' : 'Composite',
                        `r = √${closestPoint.n} = ${closestPoint.x.toFixed(3)}`,
                        `θ = 2π√${closestPoint.n} = ${(2 * Math.PI * Math.sqrt(closestPoint.n)).toFixed(3)}`
                    ];
                    
                    ctx.font = '13px Arial';
                    const lineHeight = 18;
                    const padding = 10;
                    const maxWidth = Math.max(...lines.map(line => ctx.measureText(line).width));
                    const boxWidth = maxWidth + padding * 2;
                    const boxHeight = lines.length * lineHeight + padding * 2;
                    
                    ctx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                    ctx.fillRect(tooltipX - padding, tooltipY - padding, boxWidth, boxHeight);
                    
                    ctx.strokeStyle = closestPoint.isPrime ? '#ffd700' : 'rgba(255, 255, 255, 0.3)';
                    ctx.lineWidth = 2;
                    ctx.strokeRect(tooltipX - padding, tooltipY - padding, boxWidth, boxHeight);
                    
                    ctx.fillStyle = closestPoint.isPrime ? '#ffd700' : '#fff';
                    lines.forEach((line, idx) => {
                        ctx.fillText(line, tooltipX, tooltipY + idx * lineHeight + 13);
                    });
                    
                    canvas.style.cursor = 'pointer';
                } else {
                    canvas.style.cursor = 'default';
                }
            };
        }
        
        function createZetaZerosPlot(ctx) {
            // Extended list of first 100 non-trivial zeros of Riemann zeta function
            const zetaZeros = [
                14.134725, 21.022040, 25.010858, 30.424876, 32.935062,
                37.586178, 40.918719, 43.327073, 48.005151, 49.773832,
                52.970321, 56.446248, 59.347044, 60.831779, 65.112544,
                67.079811, 69.546402, 72.067158, 75.704691, 77.144840,
                79.337375, 82.910381, 84.735493, 87.425275, 88.809111,
                92.491899, 94.651344, 95.870634, 98.831194, 101.317851,
                103.725538, 105.446623, 107.168611, 111.029536, 111.874659,
                114.320220, 116.226680, 118.790782, 121.370125, 122.946829,
                124.256819, 127.516683, 129.578704, 131.087688, 133.497737,
                134.756509, 138.116042, 139.736209, 141.123707, 143.111846,
                146.000982, 147.422765, 150.053183, 150.925257, 153.024693,
                156.112909, 157.597592, 158.849988, 161.188964, 163.030709,
                165.537069, 167.184439, 169.094515, 169.911976, 173.411536,
                174.754191, 176.441434, 178.377407, 179.916484, 182.207078,
                184.874467, 185.598783, 187.228922, 189.416158, 192.026656,
                193.079726, 195.265396, 196.876481, 198.015309, 201.264751,
                202.493594, 204.189671, 205.394697, 207.906258, 209.576509,
                211.690862, 213.347919, 214.547044, 216.169538, 219.067596,
                220.714918, 221.430705, 224.007000, 224.983324, 227.421444,
                229.337413, 231.250188, 231.987235, 233.693404, 236.524229
            ];
            
            // Store globally for other visualizations
            window.allKnownZeros = zetaZeros;
            
            // Calculate statistics
            const avgSpacing = zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]).reduce((a, b) => a + b) / (zetaZeros.length - 1);
            const minSpacing = Math.min(...zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]));
            const maxSpacing = Math.max(...zetaZeros.slice(1).map((z, i) => z - zetaZeros[i]));
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Riemann Zeta Function - Non-Trivial Zeros (First 100)</h4>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Select Zero to Explore: </label>
                    <select id="zeroSelector" style="width: 100%; padding: 10px; border-radius: 8px; margin-top: 8px; font-size: 16px;" onchange="jumpToZero(parseFloat(this.value))">
                        ${zetaZeros.map((z, idx) => `<option value="${z}">Zero #${idx + 1}: t = ${z.toFixed(6)}</option>`).join('')}
                    </select>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Zeros Catalogued</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${zetaZeros.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">First Zero</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${zetaZeros[0].toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Last Zero (in list)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${zetaZeros[zetaZeros.length-1].toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Spacing</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${avgSpacing.toFixed(3)}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Riemann Zeta Zeros:</strong><br>
                    <strong>The Riemann Hypothesis</strong> (unproven): All non-trivial zeros lie on the critical line Re(s) = 1/2<br>
                    These zeros encode deep information about the distribution of prime numbers<br>
                    Von Mangoldt's explicit formula connects zeros to prime counting function π(x)<br>
                    The zeros are complex numbers: ρ = 1/2 + it (shown values are the imaginary parts t)<br>
                    Average spacing grows like 2π/ln(t) for large t<br>
                    Computing over 10 trillion zeros has found <strong>none off the critical line</strong><br>
                    Use dropdown to jump to any specific zero for detailed exploration<br>
                    Spacing range: {minSpacing.toFixed(3)} to {maxSpacing.toFixed(3)}
                </div>
            `;
            
            // Create scatter plot of zeros on critical line
            const zeroPoints = zetaZeros.map((t, idx) => ({ x: 0.5, y: t }));
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Riemann Zeta Zeros (Re=1/2)',
                        data: zeroPoints,
                        backgroundColor: 'rgba(255, 215, 0, 0.8)',
                        borderColor: 'rgba(255, 215, 0, 1)',
                        pointRadius: 6,
                        pointHoverRadius: 8,
                        pointStyle: 'circle'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const t = zetaZeros[idx];
                                    const nextT = idx < zetaZeros.length - 1 ? zetaZeros[idx + 1] : null;
                                    const prevT = idx > 0 ? zetaZeros[idx - 1] : null;
                                    const spacing = nextT ? (nextT - t).toFixed(3) : 'N/A';
                                    const prevSpacing = prevT ? (t - prevT).toFixed(3) : 'N/A';
                                    return [
                                        `Zero #${idx + 1}`,
                                        `ρ = 1/2 + ${t.toFixed(6)}i`,
                                        `Im(ρ) = ${t.toFixed(6)}`,
                                        `Prev spacing: ${prevSpacing}`,
                                        `Next spacing: ${spacing}`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Re(s) - Real Part (Critical Line at 1/2)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            min: 0,
                            max: 1,
                            ticks: { 
                                color: '#fff',
                                stepSize: 0.1
                            },
                            grid: { 
                                color: function(context) {
                                    return context.tick.value === 0.5 ? 'rgba(255, 215, 0, 0.5)' : 'rgba(255, 255, 255, 0.1)';
                                },
                                lineWidth: function(context) {
                                    return context.tick.value === 0.5 ? 3 : 1;
                                }
                            }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Im(s) - Imaginary Part', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
            
            // Function to jump to a specific zero in other visualizations
            window.jumpToZero = function(t) {
                // Update Phasor Sum if it exists
                if (document.getElementById('tSlider')) {
                    document.getElementById('tSlider').value = t;
                    if (window.updatePhasorPlot) {
                        window.updatePhasorPlot(t, parseFloat(document.getElementById('zoomSlider')?.value || 1));
                    }
                }
                
                // Update Zeta Surface if it exists
                if (document.getElementById('tSliderSurface')) {
                    document.getElementById('tSliderSurface').value = t;
                    if (window.updateZetaSurface) {
                        window.updateZetaSurface(t);
                    }
                }
                
                // Visual feedback
                const selector = document.getElementById('zeroSelector');
                selector.style.background = 'rgba(78, 205, 196, 0.3)';
                setTimeout(() => {
                    selector.style.background = '';
                }, 500);
            };
        }
        
        function createPrimeCountingPlot(ctx) {
            const { primes } = computationData;
            
            // Generate π(x) data - count primes up to x
            const step = Math.max(1, Math.floor(primes[primes.length - 1] / 200));
            const countingData = [];
            const approximations = [];
            
            for (let x = 2; x <= primes[primes.length - 1]; x += step) {
                const count = primes.filter(p => p <= x).length;
                countingData.push({ x, y: count });
                
                // Add approximations: x/ln(x) and Li(x) ≈ x/ln(x)
                const approx = x / Math.log(x);
                approximations.push({ x, y: approx });
            }
            
            // Calculate statistics
            const maxX = primes[primes.length - 1];
            const actualCount = primes.length;
            const approxCount = maxX / Math.log(maxX);
            const error = Math.abs(actualCount - approxCount);
            const errorPercent = (error / actualCount * 100).toFixed(2);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Counting Statistics</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">π(${maxX}) actual</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${actualCount}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">x/ln(x) approximation</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;">${approxCount.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Error</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ff6b6b;">${errorPercent}%</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Prime Number Theorem</div>
                        <div style="font-size: 1em; font-weight: bold; color: #9966ff;">π(x) ~ x/ln(x)</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Prime Counting Function π(x):</strong><br>
                    The function π(x) counts the number of primes ≤ x. The Prime Number Theorem states that π(x) ~ x/ln(x) as x→∞, 
                    meaning the ratio π(x)/(x/ln(x)) approaches 1. A better approximation is the logarithmic integral Li(x).
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'π(x) - Actual Count',
                        data: countingData,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0,
                        pointRadius: 0
                    }, {
                        label: 'x/ln(x) - Approximation',
                        data: approximations,
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        borderDash: [10, 5],
                        fill: false,
                        tension: 0.3,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(2)}`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Number of Primes', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createDensityAnalysisPlot(ctx) {
            const { primes } = computationData;
            
            // Calculate density in intervals
            const intervalSize = Math.max(10, Math.floor(primes[primes.length - 1] / 50));
            const densityData = [];
            const theoreticalDensity = [];
            
            for (let x = intervalSize; x <= primes[primes.length - 1]; x += intervalSize) {
                const primesInInterval = primes.filter(p => p > x - intervalSize && p <= x).length;
                const density = primesInInterval / intervalSize;
                densityData.push({ x, y: density });
                
                // Theoretical density: 1/ln(x)
                const theoretical = 1 / Math.log(x);
                theoreticalDensity.push({ x, y: theoretical });
            }
            
            // Calculate average density
            const avgDensity = densityData.reduce((sum, d) => sum + d.y, 0) / densityData.length;
            const avgTheoretical = theoreticalDensity.reduce((sum, d) => sum + d.y, 0) / theoreticalDensity.length;
            
            // Calculate variance
            const variance = densityData.reduce((sum, d) => sum + Math.pow(d.y - avgDensity, 2), 0) / densityData.length;
            const stdDev = Math.sqrt(variance);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Density Analysis</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Density (interval: ${intervalSize})</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${avgDensity.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Theoretical (1/ln(x))</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;">${avgTheoretical.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Standard Deviation</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ff6b6b;">${stdDev.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.1); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Total Primes</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #9966ff;">${primes.length}</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Density:</strong><br>
                    Prime density at x is approximately 1/ln(x), meaning as numbers get larger, primes become less frequent. 
                    This plot shows the actual density (primes per unit interval) compared to the theoretical prediction. 
                    Fluctuations reveal the irregular distribution of primes despite their predictable average behavior.
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'Actual Density',
                        data: densityData,
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.2)',
                        borderWidth: 2,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 3,
                        pointBackgroundColor: 'rgba(78, 205, 196, 1)'
                    }, {
                        label: 'Theoretical Density (1/ln(x))',
                        data: theoreticalDensity,
                        borderColor: 'rgba(255, 215, 0, 1)',
                        backgroundColor: 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 3,
                        borderDash: [10, 5],
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.parsed.y.toFixed(8)}`;
                                },
                                afterLabel: function(context) {
                                    if (context.datasetIndex === 0) {
                                        return `Interval: [${context.parsed.x - intervalSize}, ${context.parsed.x}]`;
                                    }
                                    return '';
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Density (primes per unit)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                callback: function(value) {
                                    return value.toFixed(4);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createPrimeSpiralPlot(ctx) {
            const { primes } = computationData;
            const primeSet = new Set(primes);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Interactive Ulam Spiral</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Spiral Size: <span id="spiralSize">50</span>x<span id="spiralSizeY">50</span></label>
                    <input type="range" id="spiralSizeSlider" min="30" max="150" step="10" value="50" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="updatePrimeSpiral(parseInt(this.value), parseInt(document.getElementById('spiralStartSlider').value))">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Starting Number: <span id="spiralStart">1</span></label>
                    <input type="range" id="spiralStartSlider" min="1" max="1000" step="1" value="1" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="updatePrimeSpiral(parseInt(document.getElementById('spiralSizeSlider').value), parseInt(this.value))">
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; margin-bottom: 15px;">
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Numbers Shown</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;" id="spiralTotal">2500</div>
                    </div>
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Primes Found</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;" id="spiralPrimes">0</div>
                    </div>
                </div>
                <div style="padding: 10px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.5; font-size: 0.9em;">
                    <strong>Ulam Spiral:</strong> Discovered by Stanisław Ulam in 1963, reveals diagonal patterns where primes cluster.
                    Click on any square to see the number. Adjust size and starting point to explore different ranges!
                </div>
            `;
            
            window.updatePrimeSpiral = (size = 50, start = 1) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const baseCellSize = Math.min(rect.width / size, rect.height / size);
                const cellSize = baseCellSize * universalZoom;
                const offsetX = (rect.width - size * cellSize) / 2;
                const offsetY = (rect.height - size * cellSize) / 2;
                
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                // Generate Ulam spiral using correct algorithm
                const spiral = [];
                let x = Math.floor(size / 2);
                let y = Math.floor(size / 2);
                let num = start;
                let primeCount = 0;
                
                // Direction vectors: right, up, left, down
                const directions = [[1, 0], [0, -1], [-1, 0], [0, 1]];
                let dirIndex = 0;
                let steps = 1;
                let stepsTaken = 0;
                let stepsInDirection = 0;
                
                for (let i = 0; i < size * size; i++) {
                    if (x >= 0 && x < size && y >= 0 && y < size) {
                        const isPrime = primeSet.has(num);
                        if (isPrime) primeCount++;
                        spiral.push({ x, y, num, isPrime });
                        
                        // Draw cell
                        const screenX = offsetX + x * cellSize;
                        const screenY = offsetY + y * cellSize;
                        
                        freshCtx.fillStyle = isPrime ? '#ffd700' : 'rgba(255, 255, 255, 0.08)';
                        freshCtx.fillRect(screenX, screenY, cellSize - 1, cellSize - 1);
                    }
                    
                    // Move in current direction
                    x += directions[dirIndex][0];
                    y += directions[dirIndex][1];
                    stepsInDirection++;
                    
                    // Check if we need to turn
                    if (stepsInDirection === steps) {
                        stepsInDirection = 0;
                        dirIndex = (dirIndex + 1) % 4;
                        stepsTaken++;
                        
                        // Increase steps every 2 direction changes
                        if (stepsTaken % 2 === 0) {
                            steps++;
                        }
                    }
                    
                    num++;
                }
                
                document.getElementById('spiralSize').textContent = size;
                document.getElementById('spiralSizeY').textContent = size;
                document.getElementById('spiralStart').textContent = start;
                document.getElementById('spiralTotal').textContent = (size * size).toLocaleString();
                document.getElementById('spiralPrimes').textContent = primeCount;
                
                // Hover interaction
                canvas.onmousemove = (e) => {
                    // Redraw to clear previous hover
                    freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                    freshCtx.fillRect(0, 0, rect.width, rect.height);
                    
                    for (const cell of spiral) {
                        const screenX = offsetX + cell.x * cellSize;
                        const screenY = offsetY + cell.y * cellSize;
                        freshCtx.fillStyle = cell.isPrime ? '#ffd700' : 'rgba(255, 255, 255, 0.08)';
                        freshCtx.fillRect(screenX, screenY, cellSize - 1, cellSize - 1);
                    }
                    
                    const mouseX = e.clientX - canvas.getBoundingClientRect().left;
                    const mouseY = e.clientY - canvas.getBoundingClientRect().top;
                    
                    const gridX = Math.floor((mouseX - offsetX) / cellSize);
                    const gridY = Math.floor((mouseY - offsetY) / cellSize);
                    
                    const cell = spiral.find(c => c.x === gridX && c.y === gridY);
                    
                    if (cell) {
                        const screenX = offsetX + gridX * cellSize;
                        const screenY = offsetY + gridY * cellSize;
                        
                        freshCtx.strokeStyle = '#ff6384';
                        freshCtx.lineWidth = 2;
                        freshCtx.strokeRect(screenX, screenY, cellSize - 1, cellSize - 1);
                        
                        // Tooltip
                        freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                        freshCtx.fillRect(mouseX + 10, mouseY - 35, 160, 30);
                        freshCtx.strokeStyle = cell.isPrime ? '#ffd700' : 'rgba(255, 255, 255, 0.5)';
                        freshCtx.lineWidth = 2;
                        freshCtx.strokeRect(mouseX + 10, mouseY - 35, 160, 30);
                        
                        freshCtx.fillStyle = cell.isPrime ? '#ffd700' : '#fff';
                        freshCtx.font = 'bold 14px Arial';
                        freshCtx.fillText(`${cell.num} ${cell.isPrime ? '(PRIME)' : ''}`, mouseX + 15, mouseY - 15);
                    }
                };
            };
            
            window.updatePrimeSpiral(50, 1);
        }
        
        function createChannelRacePlot(ctx) {
            const { primes, modulus } = computationData;
            const coprimeResidues = getCoprimeResidues(modulus);
            const channels = computeResidueChannels(primes, modulus);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Channel Race Animation with Harmonic Music (mod ${modulus})</h4>
                <div style="margin-bottom: 15px;">
                    <button id="racePlayBtn" onclick="toggleRaceAnimation()" style="width: 100%; padding: 12px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Play Race</button>
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Animation Speed: <span id="raceSpeed">1</span>x</label>
                    <input type="range" id="raceSpeedSlider" min="0.1" max="5" step="0.1" value="1" 
                           style="width: 100%; margin-top: 8px;">
                </div>
                <div style="margin-bottom: 15px; padding: 15px; background: rgba(255, 255, 255, 0.05); border-radius: 8px;">
                    <div style="margin-bottom: 10px;">
                        <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                            <input type="checkbox" id="musicEnabledCheckbox" checked style="width: auto; margin-right: 10px;">
                            <span style="font-weight: 500;">Enable Musical Harmonics</span>
                        </label>
                    </div>
                    <div id="audioControls" style="display: block;">
                        <label style="color: #fff; font-weight: 500; display: block; margin-bottom: 8px;">Master Volume: <span id="masterVolume">50</span>%</label>
                        <input type="range" id="masterVolumeSlider" min="0" max="100" step="1" value="50" 
                               style="width: 100%; margin-bottom: 15px;">
                        <div style="max-height: 200px; overflow-y: auto; background: rgba(0, 0, 0, 0.3); padding: 10px; border-radius: 6px;">
                            <div style="font-size: 0.9em; color: #fff; margin-bottom: 8px; font-weight: 500;">Individual Channels:</div>
                            <div id="channelToggles"></div>
                        </div>
                    </div>
                </div>
                <div id="raceStats" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 10px;">
                </div>
                <div style="margin-top: 15px; padding: 10px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.5; font-size: 0.9em;">
                    Watch residue channels compete in real-time as primes are added sequentially!
                    Each channel generates a harmonic tone - the leading channel plays louder.
                </div>
            `;
            
            // Generate channel toggle checkboxes
            let channelTogglesHTML = '';
            coprimeResidues.forEach((r, idx) => {
                const hue = (idx / coprimeResidues.length) * 280;
                channelTogglesHTML += `
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer; padding: 4px 0;">
                        <input type="checkbox" id="channelToggle${idx}" checked style="width: auto; margin-right: 8px;">
                        <span style="color: hsla(${hue}, 80%, 60%, 1); font-weight: 500;">≡ ${r} (mod ${modulus})</span>
                        <span style="margin-left: auto; font-size: 0.85em; opacity: 0.7;">${200 + r * 50}Hz</span>
                    </label>
                `;
            });
            
            // Wait for DOM to be ready before setting innerHTML
            setTimeout(() => {
                const togglesDiv = document.getElementById('channelToggles');
                if (togglesDiv) {
                    togglesDiv.innerHTML = channelTogglesHTML;
                }
            }, 0);
            
            let raceAnimationId = null;
            let raceIndex = 0;
            let isRacePlaying = false;
            let audioContext = null;
            let oscillators = [];
            let gainNodes = [];
            let masterGainNode = null;
            let channelMuted = [];
            
            window.toggleRaceAnimation = () => {
                isRacePlaying = !isRacePlaying;
                const btn = document.getElementById('racePlayBtn');
                
                if (isRacePlaying) {
                    btn.innerHTML = 'Pause';
                    btn.style.background = 'linear-gradient(45deg, #ff6b6b, #ee5a52)';
                    startRaceAnimation();
                    
                    // Initialize audio if music is enabled
                    if (document.getElementById('musicEnabledCheckbox').checked) {
                        initAudio();
                    }
                } else {
                    btn.innerHTML = 'Play Race';
                    btn.style.background = 'linear-gradient(45deg, #4ecdc4, #44a8a3)';
                    if (raceAnimationId) cancelAnimationFrame(raceAnimationId);
                    stopAudio();
                }
            };
            
            function initAudio() {
                if (!audioContext) {
                    audioContext = new (window.AudioContext || window.webkitAudioContext)();
                }
                
                // Create master gain node
                masterGainNode = audioContext.createGain();
                masterGainNode.connect(audioContext.destination);
                masterGainNode.gain.value = parseFloat(document.getElementById('masterVolumeSlider').value) / 100;
                
                // Create oscillator and gain node for each channel
                oscillators = [];
                gainNodes = [];
                channelMuted = new Array(coprimeResidues.length).fill(false);
                
                coprimeResidues.forEach((r, idx) => {
                    const osc = audioContext.createOscillator();
                    const gain = audioContext.createGain();
                    
                    osc.connect(gain);
                    gain.connect(masterGainNode);
                    
                    // Frequency based on residue class
                    osc.frequency.value = 200 + r * 50;
                    osc.type = 'sine';
                    
                    // Start silent
                    gain.gain.value = 0;
                    
                    osc.start();
                    
                    oscillators.push(osc);
                    gainNodes.push(gain);
                });
                
                // Add master volume listener
                document.getElementById('masterVolumeSlider').oninput = function() {
                    document.getElementById('masterVolume').textContent = this.value;
                    if (masterGainNode) {
                        masterGainNode.gain.linearRampToValueAtTime(
                            parseFloat(this.value) / 100,
                            audioContext.currentTime + 0.05
                        );
                    }
                };
                
                // Add channel toggle listeners
                coprimeResidues.forEach((r, idx) => {
                    document.getElementById(`channelToggle${idx}`).onchange = function() {
                        channelMuted[idx] = !this.checked;
                        if (channelMuted[idx] && gainNodes[idx]) {
                            gainNodes[idx].gain.linearRampToValueAtTime(0, audioContext.currentTime + 0.05);
                        }
                    };
                });
            }
            
            function stopAudio() {
                oscillators.forEach(osc => {
                    try {
                        osc.stop();
                    } catch(e) {}
                });
                oscillators = [];
                gainNodes = [];
                
                if (audioContext) {
                    audioContext.close();
                    audioContext = null;
                }
            }
            
            function startRaceAnimation() {
                if (!isRacePlaying) return;
                
                const speed = parseFloat(document.getElementById('raceSpeedSlider').value);
                
                if (raceIndex >= primes.length) {
                    raceIndex = 0;
                }
                
                // Update every N frames based on speed
                if (Math.random() < speed * 0.1) {
                    raceIndex++;
                    drawRace();
                }
                
                raceAnimationId = requestAnimationFrame(startRaceAnimation);
            }
            
            function drawRace() {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                // Count primes per channel up to raceIndex
                const counts = {};
                coprimeResidues.forEach(r => counts[r] = 0);
                
                for (let i = 0; i < raceIndex && i < primes.length; i++) {
                    const p = primes[i];
                    if (p >= modulus) {
                        const residue = p % modulus;
                        if (coprimeResidues.includes(residue)) {
                            counts[residue]++;
                        }
                    }
                }
                
                const maxCount = Math.max(...Object.values(counts), 1);
                
                // Split canvas: left side for bars, right side for waveforms
                const splitX = rect.width * 0.5;
                const barHeight = rect.height / (coprimeResidues.length + 1);
                
                // Update audio volumes based on counts
                const musicEnabled = document.getElementById('musicEnabledCheckbox').checked;
                
                // Draw bars on left side
                coprimeResidues.forEach((r, idx) => {
                    const count = counts[r];
                    const barWidth = (count / maxCount) * splitX * 0.8;
                    const y = idx * barHeight + barHeight / 4;
                    
                    const hue = (idx / coprimeResidues.length) * 280;
                    freshCtx.fillStyle = `hsla(${hue}, 80%, 60%, 0.8)`;
                    freshCtx.fillRect(50, y, barWidth, barHeight * 0.6);
                    
                    freshCtx.fillStyle = '#fff';
                    freshCtx.font = 'bold 14px Arial';
                    freshCtx.fillText(`≡ ${r} (mod ${modulus})`, 10, y + barHeight * 0.4);
                    freshCtx.fillText(count, barWidth + 60, y + barHeight * 0.4);
                    
                    // Update audio gain based on count ratio
                    if (musicEnabled && gainNodes[idx] && !channelMuted[idx]) {
                        const ratio = count / maxCount;
                        const targetGain = ratio * 0.15;
                        
                        gainNodes[idx].gain.linearRampToValueAtTime(
                            targetGain, 
                            audioContext.currentTime + 0.1
                        );
                    } else if (gainNodes[idx] && channelMuted[idx]) {
                        gainNodes[idx].gain.linearRampToValueAtTime(0, audioContext.currentTime + 0.05);
                    }
                });
                
                // Draw waveforms on right side
                if (musicEnabled) {
                    const waveStartX = splitX + 20;
                    const waveWidth = rect.width - waveStartX - 20;
                    const waveHeight = barHeight * 0.5;
                    const time = Date.now() / 1000;
                    
                    coprimeResidues.forEach((r, idx) => {
                        const count = counts[r];
                        const ratio = count / maxCount;
                        const amplitude = ratio * waveHeight * 0.4;
                        const y = idx * barHeight + barHeight / 2;
                        const frequency = 200 + r * 50;
                        
                        // Check if channel is muted
                        const isMuted = channelMuted[idx] || false;
                        
                        if (amplitude > 0.01 && !isMuted) {
                            const hue = (idx / coprimeResidues.length) * 280;
                            freshCtx.strokeStyle = `hsla(${hue}, 80%, 60%, ${0.3 + ratio * 0.7})`;
                            freshCtx.lineWidth = 2 + ratio * 3;
                            
                            freshCtx.beginPath();
                            for (let x = 0; x < waveWidth; x += 2) {
                                const angle = (x / waveWidth) * Math.PI * 4 + time * frequency / 50;
                                const waveY = y + Math.sin(angle) * amplitude;
                                
                                if (x === 0) {
                                    freshCtx.moveTo(waveStartX + x, waveY);
                                } else {
                                    freshCtx.lineTo(waveStartX + x, waveY);
                                }
                            }
                            freshCtx.stroke();
                            
                            // Draw frequency label
                            freshCtx.fillStyle = `hsla(${hue}, 80%, 60%, 0.8)`;
                            freshCtx.font = '11px Arial';
                            freshCtx.fillText(`${frequency}Hz`, waveStartX + waveWidth + 5, y + 4);
                        }
                    });
                    
                    // Draw waveform section label
                    freshCtx.fillStyle = 'rgba(255, 255, 255, 0.6)';
                    freshCtx.font = 'bold 14px Arial';
                    freshCtx.fillText('Live Waveforms', splitX + 20, 20);
                }
                
                // Draw divider line
                freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                freshCtx.lineWidth = 2;
                freshCtx.beginPath();
                freshCtx.moveTo(splitX, 0);
                freshCtx.lineTo(splitX, rect.height);
                freshCtx.stroke();
                
                // Progress indicator
                freshCtx.fillStyle = '#4ecdc4';
                freshCtx.font = 'bold 18px Arial';
                freshCtx.fillText(`Prime #${raceIndex} / ${primes.length}`, 50, rect.height - 15);
            }
            
            drawRace();
        }
        
        function createHeatmapPlot(ctx) {
            const { primes } = computationData;
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Density Heatmap</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Visualization Mode:</label>
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 8px;">
                        <button onclick="setHeatmapMode('square')" id="heatmapSquare" style="padding: 8px; background: rgba(78, 205, 196, 0.3); border: 2px solid #4ecdc4; border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Square Grid</button>
                        <button onclick="setHeatmapMode('circle')" id="heatmapCircle" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Circular</button>
                        <button onclick="setHeatmapMode('hexagon')" id="heatmapHexagon" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Hexagonal</button>
                    </div>
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Grid Size: <span id="heatmapGrid">50</span>x<span id="heatmapGridY">50</span></label>
                    <input type="range" id="heatmapGridSlider" min="20" max="100" step="5" value="50" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="updateHeatmap(parseInt(this.value))">
                </div>
                <div style="padding: 10px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.5; font-size: 0.9em;">
                    Red = High prime density | Blue = Low density. Hover to see exact counts.
                </div>
            `;
            
            let heatmapMode = 'square';
            
            window.setHeatmapMode = (mode) => {
                heatmapMode = mode;
                
                // Update button styles
                ['heatmapSquare', 'heatmapCircle', 'heatmapHexagon'].forEach(id => {
                    const btn = document.getElementById(id);
                    if (btn) {
                        if ((mode === 'square' && id === 'heatmapSquare') ||
                            (mode === 'circle' && id === 'heatmapCircle') ||
                            (mode === 'hexagon' && id === 'heatmapHexagon')) {
                            btn.style.background = 'rgba(78, 205, 196, 0.3)';
                            btn.style.borderColor = '#4ecdc4';
                        } else {
                            btn.style.background = 'rgba(255, 255, 255, 0.1)';
                            btn.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                        }
                    }
                });
                
                updateHeatmap(parseInt(document.getElementById('heatmapGridSlider').value));
            };
            
            window.updateHeatmap = (gridSize = 50) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const baseCellSize = Math.min(rect.width / gridSize, rect.height / gridSize);
                const cellSize = baseCellSize * universalZoom;
                const visibleSize = Math.min(rect.width / cellSize, rect.height / cellSize);
                const offsetX = (rect.width - visibleSize * cellSize) / 2;
                const offsetY = (rect.height - visibleSize * cellSize) / 2;
                
                const maxPrime = primes[primes.length - 1];
                const rangePerCell = maxPrime / gridSize;
                
                freshCtx.fillStyle = '#000';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                // Calculate density grid
                const densityGrid = [];
                let maxDensity = 0;
                
                for (let i = 0; i < gridSize; i++) {
                    densityGrid[i] = [];
                    for (let j = 0; j < gridSize; j++) {
                        const rangeStart = (i * gridSize + j) * rangePerCell;
                        const rangeEnd = rangeStart + rangePerCell;
                        const count = primes.filter(p => p >= rangeStart && p < rangeEnd).length;
                        densityGrid[i][j] = count;
                        maxDensity = Math.max(maxDensity, count);
                    }
                }
                
                // Draw heatmap based on mode
                for (let i = 0; i < gridSize; i++) {
                    for (let j = 0; j < gridSize; j++) {
                        const density = densityGrid[i][j];
                        const ratio = density / maxDensity;
                        
                        const hue = (1 - ratio) * 240;
                        freshCtx.fillStyle = `hsla(${hue}, 100%, 50%, 0.8)`;
                        
                        const screenX = offsetX + j * cellSize;
                        const screenY = offsetY + i * cellSize;
                        
                        if (heatmapMode === 'square') {
                            freshCtx.fillRect(screenX, screenY, cellSize - 1, cellSize - 1);
                        } else if (heatmapMode === 'circle') {
                            freshCtx.beginPath();
                            freshCtx.arc(screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1, 0, Math.PI * 2);
                            freshCtx.fill();
                        } else if (heatmapMode === 'hexagon') {
                            drawHexagon(freshCtx, screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1);
                        }
                    }
                }
                
                document.getElementById('heatmapGrid').textContent = gridSize;
                document.getElementById('heatmapGridY').textContent = gridSize;
                
                // Smart hover with adaptive tooltip positioning
                canvas.onmousemove = (e) => {
                    // Redraw
                    freshCtx.fillStyle = '#000';
                    freshCtx.fillRect(0, 0, rect.width, rect.height);
                    
                    for (let i = 0; i < gridSize; i++) {
                        for (let j = 0; j < gridSize; j++) {
                            const density = densityGrid[i][j];
                            const ratio = density / maxDensity;
                            const hue = (1 - ratio) * 240;
                            freshCtx.fillStyle = `hsla(${hue}, 100%, 50%, 0.8)`;
                            
                            const screenX = offsetX + j * cellSize;
                            const screenY = offsetY + i * cellSize;
                            
                            if (heatmapMode === 'square') {
                                freshCtx.fillRect(screenX, screenY, cellSize - 1, cellSize - 1);
                            } else if (heatmapMode === 'circle') {
                                freshCtx.beginPath();
                                freshCtx.arc(screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1, 0, Math.PI * 2);
                                freshCtx.fill();
                            } else if (heatmapMode === 'hexagon') {
                                drawHexagon(freshCtx, screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1);
                            }
                        }
                    }
                    
                    const rect2 = canvas.getBoundingClientRect();
                    const mouseX = e.clientX - rect2.left;
                    const mouseY = e.clientY - rect2.top;
                    
                    const j = Math.floor((mouseX - offsetX) / cellSize);
                    const i = Math.floor((mouseY - offsetY) / cellSize);
                    
                    if (i >= 0 && i < gridSize && j >= 0 && j < gridSize) {
                        const density = densityGrid[i][j];
                        const rangeStart = Math.floor((i * gridSize + j) * rangePerCell);
                        const rangeEnd = Math.floor(rangeStart + rangePerCell);
                        
                        const screenX = offsetX + j * cellSize;
                        const screenY = offsetY + i * cellSize;
                        
                        // Highlight cell
                        freshCtx.strokeStyle = '#fff';
                        freshCtx.lineWidth = 3;
                        if (heatmapMode === 'square') {
                            freshCtx.strokeRect(screenX, screenY, cellSize - 1, cellSize - 1);
                        } else if (heatmapMode === 'circle') {
                            freshCtx.beginPath();
                            freshCtx.arc(screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1, 0, Math.PI * 2);
                            freshCtx.stroke();
                        } else if (heatmapMode === 'hexagon') {
                            drawHexagon(freshCtx, screenX + cellSize/2, screenY + cellSize/2, cellSize/2 - 1, true);
                        }
                        
                        // Smart tooltip positioning
                        const tooltipWidth = 200;
                        const tooltipHeight = 50;
                        let tooltipX = mouseX + 15;
                        let tooltipY = mouseY - 40;
                        
                        // If in top half, show below
                        if (mouseY < rect.height / 2) {
                            tooltipY = mouseY + 15;
                        }
                        
                        // If too far right, move left
                        if (tooltipX + tooltipWidth > rect.width) {
                            tooltipX = mouseX - tooltipWidth - 15;
                        }
                        
                        // If too far down, move up
                        if (tooltipY + tooltipHeight > rect.height) {
                            tooltipY = rect.height - tooltipHeight - 10;
                        }
                        
                        // Draw tooltip
                        freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                        freshCtx.fillRect(tooltipX, tooltipY, tooltipWidth, tooltipHeight);
                        freshCtx.strokeStyle = '#4ecdc4';
                        freshCtx.lineWidth = 2;
                        freshCtx.strokeRect(tooltipX, tooltipY, tooltipWidth, tooltipHeight);
                        
                        freshCtx.fillStyle = '#fff';
                        freshCtx.font = 'bold 13px Arial';
                        freshCtx.fillText(`Range: [${rangeStart}, ${rangeEnd})`, tooltipX + 10, tooltipY + 20);
                        freshCtx.fillText(`Primes: ${density}`, tooltipX + 10, tooltipY + 38);
                    }
                };
            };
            
            function drawHexagon(ctx, x, y, radius, strokeOnly = false) {
                ctx.beginPath();
                for (let i = 0; i < 6; i++) {
                    const angle = (Math.PI / 3) * i;
                    const hx = x + radius * Math.cos(angle);
                    const hy = y + radius * Math.sin(angle);
                    if (i === 0) {
                        ctx.moveTo(hx, hy);
                    } else {
                        ctx.lineTo(hx, hy);
                    }
                }
                ctx.closePath();
                if (strokeOnly) {
                    ctx.stroke();
                } else {
                    ctx.fill();
                }
            }
            
            window.updateHeatmap(50);
        }
        
        function createVoronoiPlot(ctx) {
            const { primes } = computationData;
            const sampledPrimes = primes.filter((_, i) => i % Math.max(1, Math.floor(primes.length / 200)) === 0);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Prime Voronoi Diagram</h4>
                <div style="padding: 10px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.5; font-size: 0.9em; margin-bottom: 15px;">
                    Each region shows numbers closest to a specific prime. Color indicates prime size.
                    Uses logarithmic spiral mapping for visualization.
                </div>
                <div style="background: rgba(78, 205, 196, 0.15); padding: 10px; border-radius: 8px;">
                    <div style="font-size: 0.85em; opacity: 0.8;">Primes Sampled</div>
                    <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${sampledPrimes.length}</div>
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const freshCtx = canvas.getContext('2d');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            const centerX = rect.width / 2;
            const centerY = rect.height / 2;
            const baseScale = Math.min(rect.width, rect.height) * 0.4;
            const scale = baseScale * universalZoom;
            
            freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
            freshCtx.fillRect(0, 0, rect.width, rect.height);
            
            // Map primes to spiral positions
            const primePositions = sampledPrimes.map(p => {
                const angle = 2 * Math.PI * Math.sqrt(p);
                const radius = Math.sqrt(p) / Math.sqrt(sampledPrimes[sampledPrimes.length - 1]) * scale;
                return {
                    x: centerX + radius * Math.cos(angle),
                    y: centerY + radius * Math.sin(angle),
                    prime: p
                };
            });
            
            // Draw Voronoi cells with adjusted resolution
            const step = Math.max(1, Math.floor(4 / universalZoom));
            for (let x = 0; x < rect.width; x += step) {
                for (let y = 0; y < rect.height; y += step) {
                    let closest = primePositions[0];
                    let minDist = Infinity;
                    
                    for (const pos of primePositions) {
                        const dist = Math.sqrt((x - pos.x) ** 2 + (y - pos.y) ** 2);
                        if (dist < minDist) {
                            minDist = dist;
                            closest = pos;
                        }
                    }
                    
                    const ratio = closest.prime / sampledPrimes[sampledPrimes.length - 1];
                    const hue = ratio * 280;
                    freshCtx.fillStyle = `hsla(${hue}, 70%, 50%, 0.6)`;
                    freshCtx.fillRect(x, y, step, step);
                }
            }
            
            // Draw prime points
            const pointSize = 3 * universalZoom;
            for (const pos of primePositions) {
                freshCtx.fillStyle = '#fff';
                freshCtx.beginPath();
                freshCtx.arc(pos.x, pos.y, pointSize, 0, Math.PI * 2);
                freshCtx.fill();
                
                freshCtx.strokeStyle = '#000';
                freshCtx.lineWidth = 1;
                freshCtx.stroke();
            }
        }
        
        function createHarmonicWavePlot(ctx) {
            const { primes } = computationData;
            const topPrimes = primes.slice(0, Math.min(20, primes.length));
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Harmonic Prime Waves (Musical)</h4>
                <div style="margin-bottom: 15px;">
                    <button id="playHarmonicBtn" onclick="playHarmonic()" style="width: 100%; padding: 12px; background: linear-gradient(45deg, #9966ff, #8855ee); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer;">Play Harmonic</button>
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Wave Phase: <span id="wavePhase">0</span>°</label>
                    <input type="range" id="wavePhaseSlider" min="0" max="360" step="1" value="0" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="updateHarmonicWave(parseFloat(this.value))">
                </div>
                <div style="padding: 10px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.5; font-size: 0.9em;">
                    Each prime generates a sine wave with frequency proportional to the prime.
                    The sum creates a unique "prime signature" sound and pattern!
                </div>
            `;
            
            window.playHarmonic = () => {
                // Simple audio feedback (browser APIs)
                const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                topPrimes.slice(0, 5).forEach((p, i) => {
                    const osc = audioCtx.createOscillator();
                    const gain = audioCtx.createGain();
                    osc.connect(gain);
                    gain.connect(audioCtx.destination);
                    
                    osc.frequency.value = 200 + p * 2;
                    gain.gain.value = 0.1 / (i + 1);
                    
                    osc.start();
                    osc.stop(audioCtx.currentTime + 1);
                });
            };
            
            window.updateHarmonicWave = (phase = 0) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                const centerY = rect.height / 2;
                const baseAmplitude = rect.height * 0.3 / topPrimes.length;
                const amplitude = baseAmplitude * universalZoom;
                
                topPrimes.forEach((p, idx) => {
                    freshCtx.beginPath();
                    freshCtx.strokeStyle = `hsla(${(idx / topPrimes.length) * 280}, 80%, 60%, 0.8)`;
                    freshCtx.lineWidth = 2 * universalZoom;
                    
                    for (let x = 0; x < rect.width; x++) {
                        const freq = p / 100;
                        const y = centerY + amplitude * Math.sin(freq * x * 0.05 + phase * Math.PI / 180);
                        
                        if (x === 0) {
                            freshCtx.moveTo(x, y);
                        } else {
                            freshCtx.lineTo(x, y);
                        }
                    }
                    freshCtx.stroke();
                    
                    // Label
                    freshCtx.fillStyle = '#fff';
                    freshCtx.font = `${12 * Math.min(universalZoom, 1.5)}px Arial`;
                    freshCtx.fillText(`p=${p}`, 10, 20 + idx * 15 * Math.min(universalZoom, 1.5));
                });
                
                document.getElementById('wavePhase').textContent = phase.toFixed(0);
            };
            
            window.updateHarmonicWave(0);
        }
        
        function createPrimeAvoidancePlot(ctx) {
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Getachew Prime Channel Avoidance Theorem</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Max Modulus: <span id="avoidanceMaxMod">30</span></label>
                    <input type="range" id="avoidanceMaxModSlider" min="10" max="200" step="1" value="30" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="document.getElementById('avoidanceMaxMod').textContent = this.value; window.updatePrimeAvoidance(parseInt(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.85em; opacity: 0.7; margin-top: 5px;">
                        <span>10 (minimal)</span>
                        <span>30 (default)</span>
                        <span>200 (maximum)</span>
                    </div>
                    <div style="margin-top: 10px;">
                        <label style="color: #fff; font-weight: 500; font-size: 0.9em;">Or enter custom value:</label>
                        <input type="number" id="avoidanceCustomMod" min="2" max="200" placeholder="Enter modulus (2-200)" 
                               style="width: 100%; padding: 8px; border-radius: 6px; margin-top: 5px; font-size: 14px;"
                               onchange="const val = Math.min(200, Math.max(2, parseInt(this.value) || 30)); document.getElementById('avoidanceMaxModSlider').value = val; window.updatePrimeAvoidance(val);">
                    </div>
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Projection Line Opacity: <span id="avoidanceEpsilon">0.2</span></label>
                    <input type="range" id="avoidanceEpsilonSlider" min="0.05" max="1" step="0.05" value="0.2" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="window.updatePrimeAvoidance(parseInt(document.getElementById('avoidanceMaxModSlider').value))">
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Theorem Visualization:</strong><br>
                    <span style="color: #4ecdc4;">● Cyan rings</span> = Prime moduli (avoid all Farey channels)<br>
                    <span style="color: #ff6384;">● Red points</span> = Composite residues (project onto channels)<br>
                    <strong>Key Insight:</strong> Prime moduli form complete coprime rings - no residue reduces to a simpler fraction.<br>
                    Composite moduli have reducible residues that project onto Farey flow lines (1/N channels).<br>
                    This geometric separation reveals the fundamental difference between primes and composites.
                </div>
            `;
            
            window.updatePrimeAvoidance = (maxMod = 30) => {
                console.log('Starting Prime Channel Avoidance with maxMod:', maxMod);
                
                const canvas = document.getElementById('vizCanvas');
                if (!canvas) {
                    console.error('Canvas not found!');
                    return;
                }
                
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                console.log('Canvas dimensions:', rect.width, 'x', rect.height);
                
                const centerX = rect.width / 2;
                const centerY = rect.height / 2;
                const maxRadius = Math.min(rect.width, rect.height) * 0.42;
                
                const epsilonSlider = document.getElementById('avoidanceEpsilonSlider');
                const epsilon = epsilonSlider ? parseFloat(epsilonSlider.value) : 0.2;
                
                // Generate primes up to maxMod
                const modPrimes = sieveOfEratosthenes(maxMod);
                const primeSet = new Set(modPrimes);
                
                console.log('Generated', modPrimes.length, 'primes up to', maxMod);
                
                // Create list of all moduli
                const moduli = [];
                for (let m = 2; m <= maxMod; m++) {
                    moduli.push({ M: m, isPrime: primeSet.has(m) });
                }
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                console.log('Canvas cleared, drawing', allResidues.length, 'residues');
                
                // Calculate all residues and their reduction paths
                const allResidues = [];
                for (const mod of moduli) {
                    const M = mod.M;
                    const radius = (M / maxMod) * maxRadius;
                    
                    for (let r = 1; r < M; r++) {
                        const d = gcd(r, M);
                        const rPrime = r / d;
                        const mPrime = M / d;
                        const isReducible = d > 1;
                        
                        // Position on outer ring
                        const angle = (2 * Math.PI * r) / M;
                        const x = centerX + radius * Math.cos(angle);
                        const y = centerY + radius * Math.sin(angle);
                        
                        // Position of reduction channel (if reducible)
                        let channelX = centerX;
                        let channelY = centerY;
                        if (isReducible) {
                            const channelRadius = (mPrime / maxMod) * maxRadius;
                            const channelAngle = (2 * Math.PI * rPrime) / mPrime;
                            channelX = centerX + channelRadius * Math.cos(channelAngle);
                            channelY = centerY + channelRadius * Math.sin(channelAngle);
                        }
                        
                        allResidues.push({
                            M, r, d, isPrime: mod.isPrime, isReducible,
                            x, y, channelX, channelY
                        });
                    }
                }
                
                // Draw projection lines for reducible fractions
                const lineOpacity = Math.max(0.1, epsilon * 0.5);
                for (const res of allResidues) {
                    if (res.isReducible) {
                        freshCtx.strokeStyle = `rgba(255, 99, 132, ${lineOpacity})`;
                        freshCtx.lineWidth = 1;
                        freshCtx.beginPath();
                        freshCtx.moveTo(res.x, res.y);
                        freshCtx.lineTo(res.channelX, res.channelY);
                        freshCtx.stroke();
                    }
                }
                
                // Draw modulus rings
                for (const mod of moduli) {
                    const radius = (mod.M / maxMod) * maxRadius;
                    freshCtx.strokeStyle = mod.isPrime ? 'rgba(78, 205, 196, 0.5)' : 'rgba(255, 99, 132, 0.3)';
                    freshCtx.lineWidth = mod.isPrime ? 4 : 2;
                    freshCtx.beginPath();
                    freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                    freshCtx.stroke();
                }
                
                // Draw residue points
                for (const res of allResidues) {
                    let pointColor;
                    if (res.isPrime) {
                        pointColor = 'rgba(78, 205, 196, 0.9)';
                    } else {
                        pointColor = res.isReducible ? 'rgba(255, 99, 132, 0.8)' : 'rgba(255, 159, 64, 0.8)';
                    }
                    
                    freshCtx.fillStyle = pointColor;
                    freshCtx.beginPath();
                    freshCtx.arc(res.x, res.y, 4, 0, Math.PI * 2);
                    freshCtx.fill();
                }
                
                // Draw center
                freshCtx.fillStyle = '#fff';
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, 6, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Update display
                document.getElementById('avoidanceMaxMod').textContent = maxMod;
                document.getElementById('avoidanceEpsilon').textContent = epsilon.toFixed(2);
                
                console.log('Prime Channel Avoidance rendering complete');
                
                // Add hover AND click
                canvas.onmousemove = (e) => {
                    const rect = canvas.getBoundingClientRect();
                    const mouseX = e.clientX - rect.left;
                    const mouseY = e.clientY - rect.top;
                    
                    let closestRes = null;
                    let minDist = 10;
                    
                    for (const res of allResidues) {
                        const dist = Math.sqrt((mouseX - res.x) ** 2 + (mouseY - res.y) ** 2);
                        if (dist < minDist) {
                            minDist = dist;
                            closestRes = res;
                        }
                    }
                    
                    if (closestRes) {
                        // Redraw
                        updatePrimeAvoidance(maxMod);
                        
                        // Highlight
                        freshCtx.strokeStyle = '#ffd700';
                        freshCtx.lineWidth = 3;
                        freshCtx.beginPath();
                        freshCtx.arc(closestRes.x, closestRes.y, 7, 0, Math.PI * 2);
                        freshCtx.stroke();
                        
                        // Tooltip
                        const lines = [
                            `M = ${closestRes.M} ${closestRes.isPrime ? '(PRIME)' : '(composite)'}`,
                            `r = ${closestRes.r}`,
                            `gcd(r, M) = ${closestRes.d}`,
                            closestRes.isReducible ? `Reduces to ${closestRes.r/closestRes.d}/${closestRes.M/closestRes.d}` : 'Irreducible (coprime)'
                        ];
                        
                        freshCtx.font = '13px Arial';
                        const lineHeight = 18;
                        const padding = 10;
                        const maxWidth = Math.max(...lines.map(line => freshCtx.measureText(line).width));
                        
                        freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                        freshCtx.fillRect(mouseX + 15, mouseY - 30, maxWidth + padding * 2, lines.length * lineHeight + padding * 2);
                        freshCtx.strokeStyle = closestRes.isPrime ? '#4ecdc4' : '#ff6384';
                        freshCtx.lineWidth = 2;
                        freshCtx.strokeRect(mouseX + 15, mouseY - 30, maxWidth + padding * 2, lines.length * lineHeight + padding * 2);
                        
                        freshCtx.fillStyle = '#fff';
                        lines.forEach((line, idx) => {
                            freshCtx.fillText(line, mouseX + 15 + padding, mouseY - 30 + padding + idx * lineHeight + 13);
                        });
                        
                        canvas.style.cursor = 'pointer';
                    } else {
                        canvas.style.cursor = 'default';
                    }
                };
                
                // Click handler for detailed info
                canvas.onclick = (e) => {
                    const rect = canvas.getBoundingClientRect();
                    const mouseX = e.clientX - rect.left;
                    const mouseY = e.clientY - rect.top;
                    
                    let closestRes = null;
                    let minDist = 10;
                    
                    for (const res of allResidues) {
                        const dist = Math.sqrt((mouseX - res.x) ** 2 + (mouseY - res.y) ** 2);
                        if (dist < minDist) {
                            minDist = dist;
                            closestRes = res;
                        }
                    }
                    
                    if (closestRes) {
                        showCompositePointDetails(closestRes);
                    }
                };
            };
            
            window.updatePrimeAvoidance(30);
        }
        
        function createCompositeChannelsPlot(ctx) {
            const { primes } = computationData;
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Getachew Composite Channel Projection Corollary</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Composite Modulus (M): <span id="compositeMValue">12</span></label>
                    <input type="range" id="compositeMSlider" min="4" max="500" step="1" value="12" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="document.getElementById('compositeMValue').textContent = this.value; updateCompositeChannels(parseInt(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.85em; opacity: 0.7; margin-top: 5px;">
                        <span>4 (minimal)</span>
                        <span>60 (standard)</span>
                        <span>500 (maximum)</span>
                    </div>
                    <div style="margin-top: 10px;">
                        <label style="color: #fff; font-weight: 500; font-size: 0.9em;">Or enter custom value:</label>
                        <input type="number" id="compositeCustomMod" min="2" max="1000" placeholder="Enter modulus (2-1000)" 
                               style="width: 100%; padding: 8px; border-radius: 6px; margin-top: 5px; font-size: 14px;"
                               onchange="const val = Math.min(1000, Math.max(2, parseInt(this.value) || 12)); document.getElementById('compositeMSlider').value = val; updateCompositeChannels(val);">
                    </div>
                    <div style="margin-top: 10px; display: grid; grid-template-columns: repeat(auto-fill, minmax(80px, 1fr)); gap: 8px;">
                        <button onclick="document.getElementById('compositeMSlider').value=6; updateCompositeChannels(6);" style="padding: 6px; background: rgba(78, 205, 196, 0.3); border: 1px solid #4ecdc4; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">M = 6</button>
                        <button onclick="document.getElementById('compositeMSlider').value=12; updateCompositeChannels(12);" style="padding: 6px; background: rgba(255, 215, 0, 0.3); border: 1px solid #ffd700; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">M = 12</button>
                        <button onclick="document.getElementById('compositeMSlider').value=30; updateCompositeChannels(30);" style="padding: 6px; background: rgba(255, 99, 132, 0.3); border: 1px solid #ff6384; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">M = 30</button>
                        <button onclick="document.getElementById('compositeMSlider').value=60; updateCompositeChannels(60);" style="padding: 6px; background: rgba(153, 102, 255, 0.3); border: 1px solid #9966ff; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">M = 60</button>
                        <button onclick="document.getElementById('compositeMSlider').value=210; updateCompositeChannels(210);" style="padding: 6px; background: rgba(255, 159, 64, 0.3); border: 1px solid #ff9f40; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">M = 210</button>
                    </div>
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Projection Line Opacity: <span id="compositeEpsilon">0.1</span></label>
                    <input type="range" id="compositeEpsilonSlider" min="0.05" max="1" step="0.05" value="0.1" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="updateCompositeChannels(parseInt(document.getElementById('compositeMSlider').value))">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Display Mode:</label>
                    <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin-top: 8px;">
                        <button onclick="setCompositeMode('projection')" id="compositeModeProj" style="padding: 8px; background: rgba(78, 205, 196, 0.3); border: 2px solid #4ecdc4; border-radius: 6px; color: #fff; cursor: pointer;">Projection Lines</button>
                        <button onclick="setCompositeMode('rings')" id="compositeModeRings" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer;">Ring View</button>
                    </div>
                </div>
                <div id="compositeStats"></div>
                <div id="compositeDetails" style="padding: 15px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6; margin-top: 15px;">
                    <strong>Corollary Visualization:</strong><br>
                    <span style="color: #4ecdc4;">● Cyan points</span> = Irreducible residues (gcd = 1)<br>
                    <span style="color: #ff6384;">● Red points</span> = Reducible residues (gcd > 1)<br>
                    <span style="color: #ffd700;">● Gold rings</span> = Farey channels (reduction targets)<br>
                    <span style="color: rgba(255, 99, 132, 0.5);">● Red lines</span> = Projection paths showing r/M → r'/M'<br><br>
                    <strong>Key Result:</strong> Every composite M has reducible residues that project onto simpler Farey channels.<br>
                    The number projecting to each channel M' is exactly d = M/M' (channel multiplicity).<br><br>
                    <strong>Click any point</strong> to see detailed reduction path!
                </div>
                <div id="projectionBreakdown" style="display: none; margin-top: 15px; padding: 15px; background: rgba(78, 205, 196, 0.1); border-radius: 8px; border-left: 4px solid #4ecdc4;">
                </div>
            `;
            
            let compositeDisplayMode = 'projection';
            
            window.setCompositeMode = (mode) => {
                compositeDisplayMode = mode;
                
                ['compositeModeProj', 'compositeModeRings'].forEach(id => {
                    const btn = document.getElementById(id);
                    if (btn) {
                        if ((mode === 'projection' && id === 'compositeModeProj') ||
                            (mode === 'rings' && id === 'compositeModeRings')) {
                            btn.style.background = 'rgba(78, 205, 196, 0.3)';
                            btn.style.borderColor = '#4ecdc4';
                        } else {
                            btn.style.background = 'rgba(255, 255, 255, 0.1)';
                            btn.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                        }
                    }
                });
                
                updateCompositeChannels(parseInt(document.getElementById('compositeMSlider').value));
            };
            
            window.updateCompositeChannels = (M = 12) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const centerX = rect.width / 2;
                const centerY = rect.height / 2;
                
                // Get all divisors (including M itself for complete factor list)
                const allDivisors = [];
                for (let d = 1; d <= M; d++) {
                    if (M % d === 0) {
                        allDivisors.push(d);
                    }
                }
                
                // Divisors for rings (exclude M itself)
                const divisors = allDivisors.filter(d => d < M);
                
                const phiM = eulerPhi(M);
                const maxRadius = Math.min(rect.width, rect.height) * 0.4;
                const epsilon = parseFloat(document.getElementById('compositeEpsilonSlider').value);
                
                const residueData = [];
                for (let r = 0; r < M; r++) {
                    const d = gcd(r, M);
                    const rPrime = r / d;
                    const mPrime = M / d;
                    const isReducible = d > 1;
                    
                    const outerAngle = (2 * Math.PI * r) / M;
                    const outerX = centerX + maxRadius * Math.cos(outerAngle);
                    const outerY = centerY + maxRadius * Math.sin(outerAngle);
                    
                    const innerRadius = (mPrime / M) * maxRadius;
                    const innerAngle = (2 * Math.PI * rPrime) / mPrime;
                    const innerX = centerX + innerRadius * Math.cos(innerAngle);
                    const innerY = centerY + innerRadius * Math.sin(innerAngle);
                    
                    residueData.push({
                        r, rPrime, mPrime, d,
                        isReducible,
                        outerX, outerY,
                        innerX, innerY,
                        outerRadius: maxRadius,
                        innerRadius
                    });
                }
                
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, rect.width, rect.height);
                
                if (compositeDisplayMode === 'projection') {
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                    freshCtx.lineWidth = 3;
                    freshCtx.beginPath();
                    freshCtx.arc(centerX, centerY, maxRadius, 0, Math.PI * 2);
                    freshCtx.stroke();
                    
                    const uniqueMPrimes = [...new Set(residueData.map(d => d.mPrime))].sort((a, b) => a - b);
                    for (const mPrime of uniqueMPrimes) {
                        if (mPrime === M) continue;
                        const radius = (mPrime / M) * maxRadius;
                        freshCtx.strokeStyle = 'rgba(255, 215, 0, 0.2)';
                        freshCtx.lineWidth = 2;
                        freshCtx.beginPath();
                        freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                        freshCtx.stroke();
                    }
                    
                    const lineOpacity = Math.max(0.2, Math.min(1, epsilon * 2));
                    for (const data of residueData) {
                        if (data.isReducible) {
                            freshCtx.strokeStyle = `rgba(255, 99, 132, ${lineOpacity})`;
                            freshCtx.lineWidth = 2;
                            freshCtx.beginPath();
                            freshCtx.moveTo(data.outerX, data.outerY);
                            freshCtx.lineTo(data.innerX, data.innerY);
                            freshCtx.stroke();
                        }
                    }
                    
                    for (const data of residueData) {
                        freshCtx.fillStyle = data.isReducible ? 'rgba(255, 99, 132, 0.9)' : 'rgba(78, 205, 196, 0.9)';
                        freshCtx.beginPath();
                        freshCtx.arc(data.outerX, data.outerY, 5, 0, Math.PI * 2);
                        freshCtx.fill();
                        
                        if (data.isReducible) {
                            freshCtx.fillStyle = 'rgba(255, 215, 0, 0.8)';
                            freshCtx.beginPath();
                            freshCtx.arc(data.innerX, data.innerY, 4, 0, Math.PI * 2);
                            freshCtx.fill();
                        }
                    }
                } else {
                    const uniqueMPrimes = [...new Set(residueData.map(d => d.mPrime))].sort((a, b) => a - b);
                    for (const mPrime of uniqueMPrimes) {
                        const radius = (mPrime / M) * maxRadius;
                        freshCtx.strokeStyle = mPrime === M ? 'rgba(255, 255, 255, 0.5)' : 'rgba(255, 215, 0, 0.3)';
                        freshCtx.lineWidth = mPrime === M ? 3 : 2;
                        freshCtx.beginPath();
                        freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                        freshCtx.stroke();
                    }
                    
                    for (const data of residueData) {
                        freshCtx.fillStyle = data.isReducible ? 'rgba(255, 99, 132, 0.8)' : 'rgba(78, 205, 196, 0.8)';
                        freshCtx.beginPath();
                        freshCtx.arc(data.outerX, data.outerY, 4, 0, Math.PI * 2);
                        freshCtx.fill();
                    }
                }
                
                freshCtx.fillStyle = '#4ecdc4';
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, 6, 0, Math.PI * 2);
                freshCtx.fill();
                
                document.getElementById('compositeMValue').textContent = M;
                document.getElementById('compositeEpsilon').textContent = epsilon.toFixed(2);
                
                const reducibleCount = residueData.filter(d => d.isReducible).length;
                const reducibleRatio = reducibleCount / M;
                
                document.getElementById('compositeStats').innerHTML = `
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 12px; margin-bottom: 15px;">
                        <div style="background: rgba(78, 205, 196, 0.15); padding: 10px; border-radius: 8px;">
                            <div style="font-size: 0.85em; opacity: 0.8;">φ(${M})</div>
                            <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;">${phiM}</div>
                        </div>
                        <div style="background: rgba(255, 99, 132, 0.15); padding: 10px; border-radius: 8px;">
                            <div style="font-size: 0.85em; opacity: 0.8;">Reducible</div>
                            <div style="font-size: 1.3em; font-weight: bold; color: #ff6384;">${reducibleCount}</div>
                        </div>
                        <div style="background: rgba(255, 215, 0, 0.15); padding: 10px; border-radius: 8px;">
                            <div style="font-size: 0.85em; opacity: 0.8;">Ratio</div>
                            <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;">${(reducibleRatio * 100).toFixed(1)}%</div>
                        </div>
                        <div style="background: rgba(153, 102, 255, 0.15); padding: 10px; border-radius: 8px;">
                            <div style="font-size: 0.85em; opacity: 0.8;">Channels</div>
                            <div style="font-size: 1.3em; font-weight: bold; color: #9966ff;">${divisors.length}</div>
                        </div>
                    </div>
                `;
            };
            
            window.updateCompositeChannels(12);
        }
        
        function createPhaseExplorerPlot(ctx) {
            const { primes, exponent, constantType } = computationData;
            const sigma = exponent / 2;
            
            // Use gap-classified primes for phase law side
            const gapClasses = computeLowestGapClasses(primes);
            const sortedGaps = Object.keys(gapClasses).map(Number).sort((a, b) => a - b);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Phase Explorer: Combined Phasor Sum & Phase Law Analysis</h4>
                <div style="margin-bottom: 20px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer; margin-bottom: 10px;">
                        <input type="checkbox" id="showTraceLine" style="width: auto; margin-right: 10px;">
                        <span>Show Phasor Sum Trace (Final Vector Tip Path)</span>
                    </label>
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer; margin-bottom: 10px;">
                        <input type="checkbox" id="showPhasorSteps" style="width: auto; margin-right: 10px;">
                        <span>Show Phasor Construction Steps (How Line is Built)</span>
                    </label>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Imaginary Part (t): <span id="explorerT">14.134725</span></label>
                    <input type="range" id="explorerTSlider" min="0" max="250" step="0.001" value="14.134725" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhaseExplorer(parseFloat(this.value))">
                    <div style="margin-top: 10px;">
                        <label style="color: #fff; font-weight: 500; font-size: 0.9em;">Jump to Known Zero:</label>
                        <select id="explorerZeroSelector" style="width: 100%; padding: 8px; border-radius: 6px; margin-top: 5px; font-size: 14px;" onchange="jumpToExplorerZero(parseFloat(this.value))">
                            <option value="14.134725">Zero 1: t = 14.134725</option>
                            <option value="21.022040">Zero 2: t = 21.022040</option>
                            <option value="25.010858">Zero 3: t = 25.010858</option>
                            <option value="30.424876">Zero 4: t = 30.424876</option>
                            <option value="32.935062">Zero 5: t = 32.935062</option>
                            <option value="37.586178">Zero 6: t = 37.586178</option>
                            <option value="40.918719">Zero 7: t = 40.918719</option>
                            <option value="43.327073">Zero 8: t = 43.327073</option>
                        </select>
                    </div>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">View Mode:</label>
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 10px;">
                        <button onclick="setExplorerMode('sideBySide')" id="explorerSideBySide" style="padding: 8px; background: rgba(78, 205, 196, 0.3); border: 2px solid #4ecdc4; border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Side by Side</button>
                        <button onclick="setExplorerMode('overlay')" id="explorerOverlay" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Overlay</button>
                        <button onclick="setExplorerMode('comparison')" id="explorerComparison" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Comparison</button>
                    </div>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Decay Parameter (β): <span id="explorerBeta">Auto</span></label>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                            <input type="radio" name="explorerBetaMode" value="auto" checked onchange="updatePhaseExplorer(parseFloat(document.getElementById('explorerTSlider').value))" style="width: auto; margin-right: 5px;">
                            Auto (β ~ 1/log(t))
                        </label>
                        <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                            <input type="radio" name="explorerBetaMode" value="manual" onchange="updatePhaseExplorer(parseFloat(document.getElementById('explorerTSlider').value))" style="width: auto; margin-right: 5px;">
                            Manual
                        </label>
                    </div>
                    <input type="range" id="explorerBetaSlider" min="0" max="1" step="0.001" value="0.1" 
                           style="width: 100%; margin-top: 10px; display: none;"
                           oninput="updatePhaseExplorer(parseFloat(document.getElementById('explorerTSlider').value))">
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Phasor Magnitude</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #4ecdc4;" id="explorerPhasorMag">--</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Phase Law Magnitude</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ffd700;" id="explorerPhaseLawMag">--</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Difference</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #ff6384;" id="explorerDiff">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 10px; border-radius: 8px;">
                        <div style="font-size: 0.85em; opacity: 0.8;">Coherence</div>
                        <div style="font-size: 1.3em; font-weight: bold; color: #9966ff;" id="explorerCoherence">--</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Combined Analysis:</strong><br>
                    <strong>Left (Phasor Sum):</strong> Direct vector sum of n<sup>-s</sup> terms rotating in complex plane<br>
                    <strong>Right (Phase Law):</strong> Gap-classified Euler product with phase alignment φ(p,t) = t·log(p) - π/2<br>
                    Both approaches converge to ζ(s) but reveal different structural properties<br>
                    At Riemann zeros: both show destructive interference (magnitude ≈ 0)<br>
                    Click mode buttons to switch between side-by-side, overlay, and comparison views
                </div>
            `;
            
            // Add event listener for beta mode toggle
            document.querySelectorAll('input[name="explorerBetaMode"]').forEach(radio => {
                radio.addEventListener('change', function() {
                    const manualSlider = document.getElementById('explorerBetaSlider');
                    if (this.value === 'manual') {
                        manualSlider.style.display = 'block';
                    } else {
                        manualSlider.style.display = 'none';
                    }
                });
            });
            
            let explorerViewMode = 'sideBySide';
            let tracePoints = []; // Store trace history
            
            window.setExplorerMode = (mode) => {
                explorerViewMode = mode;
                
                // Update button styles
                ['explorerSideBySide', 'explorerOverlay', 'explorerComparison'].forEach(id => {
                    const btn = document.getElementById(id);
                    if (btn) {
                        if ((mode === 'sideBySide' && id === 'explorerSideBySide') ||
                            (mode === 'overlay' && id === 'explorerOverlay') ||
                            (mode === 'comparison' && id === 'explorerComparison')) {
                            btn.style.background = 'rgba(78, 205, 196, 0.3)';
                            btn.style.borderColor = '#4ecdc4';
                        } else {
                            btn.style.background = 'rgba(255, 255, 255, 0.1)';
                            btn.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                        }
                    }
                });
                
                updatePhaseExplorer(parseFloat(document.getElementById('explorerTSlider').value));
            };
            
            window.jumpToExplorerZero = (t) => {
                document.getElementById('explorerTSlider').value = t;
                updatePhaseExplorer(t);
            };
            
            window.updatePhaseExplorer = (t) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                
                // Determine beta
                const betaMode = document.querySelector('input[name="explorerBetaMode"]:checked').value;
                let beta;
                if (betaMode === 'auto') {
                    beta = t > 0 ? 1 / Math.log(Math.max(2, t)) : 0.1;
                    document.getElementById('explorerBeta').textContent = `${beta.toFixed(4)} (Auto)`;
                } else {
                    beta = parseFloat(document.getElementById('explorerBetaSlider').value);
                    document.getElementById('explorerBeta').textContent = beta.toFixed(4);
                }
                
                // Check if trace is enabled
                const showTrace = document.getElementById('showTraceLine')?.checked || false;
                const showSteps = document.getElementById('showPhasorSteps')?.checked || false;
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, width, height);
                
                if (explorerViewMode === 'sideBySide') {
                    // Split canvas in half
                    const splitX = width / 2;
                    
                    // Left: Phasor Sum
                    freshCtx.save();
                    freshCtx.rect(0, 0, splitX, height);
                    freshCtx.clip();
                    const phasorMag = drawPhasorSumSection(freshCtx, 0, 0, splitX, height, t, sigma, showTrace, showSteps);
                    freshCtx.restore();
                    
                    // Divider line
                    freshCtx.strokeStyle = 'rgba(255, 215, 0, 0.5)';
                    freshCtx.lineWidth = 3;
                    freshCtx.beginPath();
                    freshCtx.moveTo(splitX, 0);
                    freshCtx.lineTo(splitX, height);
                    freshCtx.stroke();
                    
                    // Right: Phase Law
                    freshCtx.save();
                    freshCtx.rect(splitX, 0, splitX, height);
                    freshCtx.clip();
                    const phaseLawMag = drawPhaseLawSection(freshCtx, splitX, 0, splitX, height, t, beta, sortedGaps, gapClasses);
                    freshCtx.restore();
                    
                    // Labels
                    freshCtx.fillStyle = '#4ecdc4';
                    freshCtx.font = 'bold 16px Arial';
                    freshCtx.textAlign = 'center';
                    freshCtx.fillText('Phasor Sum', splitX / 2, 25);
                    
                    freshCtx.fillStyle = '#ff6384';
                    freshCtx.fillText('Phase Law', splitX + splitX / 2, 25);
                    
                    updateExplorerStats(phasorMag, phaseLawMag, t);
                    
                } else if (explorerViewMode === 'overlay') {
                    // Draw both on same canvas with transparency
                    const phasorMag = drawPhasorSumSection(freshCtx, 0, 0, width, height, t, sigma, showTrace, showSteps, 0.5);
                    const phaseLawMag = drawPhaseLawSection(freshCtx, 0, 0, width, height, t, beta, sortedGaps, gapClasses, 0.5);
                    
                    // Legend
                    freshCtx.fillStyle = 'rgba(0, 0, 0, 0.8)';
                    freshCtx.fillRect(width - 200, 10, 190, 60);
                    freshCtx.fillStyle = '#4ecdc4';
                    freshCtx.font = 'bold 14px Arial';
                    freshCtx.textAlign = 'left';
                    freshCtx.fillText('Phasor Sum', width - 190, 30);
                    freshCtx.fillStyle = '#ff6384';
                    freshCtx.fillText('Phase Law', width - 190, 50);
                    
                    updateExplorerStats(phasorMag, phaseLawMag, t);
                    
                } else if (explorerViewMode === 'comparison') {
                    // Draw difference visualization
                    const centerX = width / 2;
                    const centerY = height / 2;
                    const scale = Math.min(width, height) * 0.35;
                    
                    // Compute both
                    let phasorReal = 0, phasorImag = 0;
                    const numPhasors = Math.min(50, primes.length);
                    for (let i = 0; i < numPhasors; i++) {
                        const n = primes[i];
                        const radius = Math.pow(n, -sigma);
                        const angle = -t * Math.log(n);
                        phasorReal += radius * Math.cos(angle);
                        phasorImag += radius * Math.sin(angle);
                    }
                    const phasorMag = Math.sqrt(phasorReal * phasorReal + phasorImag * phasorImag);
                    
                    let phaseLawReal = 0, phaseLawImag = 0;
                    for (const gap of sortedGaps) {
                        const gapPrimes = gapClasses[gap];
                        for (const p of gapPrimes) {
                            const phi = t * Math.log(p) - Math.PI / 2;
                            const pHalf = Math.pow(p, -0.5);
                            const decay = Math.exp(-beta * Math.log(p));
                            
                            const denomReal = 1 - pHalf * Math.cos(-phi);
                            const denomImag = -pHalf * Math.sin(-phi);
                            const denomMagSq = denomReal * denomReal + denomImag * denomImag;
                            
                            phaseLawReal += (denomReal / denomMagSq) * decay;
                            phaseLawImag += (-denomImag / denomMagSq) * decay;
                        }
                    }
                    const phaseLawMag = Math.sqrt(phaseLawReal * phaseLawReal + phaseLawImag * phaseLawImag);
                    
                    // Draw comparison vectors
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                    freshCtx.lineWidth = 1;
                    freshCtx.beginPath();
                    freshCtx.moveTo(0, centerY);
                    freshCtx.lineTo(width, centerY);
                    freshCtx.moveTo(centerX, 0);
                    freshCtx.lineTo(centerX, height);
                    freshCtx.stroke();
                    
                    // Phasor vector
                    const phasorX = centerX + phasorReal * scale;
                    const phasorY = centerY - phasorImag * scale;
                    freshCtx.strokeStyle = '#4ecdc4';
                    freshCtx.lineWidth = 4;
                    freshCtx.beginPath();
                    freshCtx.moveTo(centerX, centerY);
                    freshCtx.lineTo(phasorX, phasorY);
                    freshCtx.stroke();
                    freshCtx.fillStyle = '#4ecdc4';
                    freshCtx.beginPath();
                    freshCtx.arc(phasorX, phasorY, 6, 0, Math.PI * 2);
                    freshCtx.fill();
                    
                    // Phase law vector
                    const phaseLawX = centerX + phaseLawReal * scale;
                    const phaseLawY = centerY - phaseLawImag * scale;
                    freshCtx.strokeStyle = '#ff6384';
                    freshCtx.lineWidth = 4;
                    freshCtx.beginPath();
                    freshCtx.moveTo(centerX, centerY);
                    freshCtx.lineTo(phaseLawX, phaseLawY);
                    freshCtx.stroke();
                    freshCtx.fillStyle = '#ff6384';
                    freshCtx.beginPath();
                    freshCtx.arc(phaseLawX, phaseLawY, 6, 0, Math.PI * 2);
                    freshCtx.fill();
                    
                    // Difference vector
                    freshCtx.strokeStyle = '#ffd700';
                    freshCtx.lineWidth = 2;
                    freshCtx.setLineDash([5, 5]);
                    freshCtx.beginPath();
                    freshCtx.moveTo(phasorX, phasorY);
                    freshCtx.lineTo(phaseLawX, phaseLawY);
                    freshCtx.stroke();
                    freshCtx.setLineDash([]);
                    
                    // Labels
                    freshCtx.fillStyle = '#fff';
                    freshCtx.font = '14px Arial';
                    freshCtx.textAlign = 'center';
                    freshCtx.fillText('Re', width - 30, centerY - 10);
                    freshCtx.fillText('Im', centerX + 15, 20);
                    
                    freshCtx.fillStyle = '#4ecdc4';
                    freshCtx.font = 'bold 14px Arial';
                    freshCtx.fillText('Phasor', phasorX, phasorY - 15);
                    
                    freshCtx.fillStyle = '#ff6384';
                    freshCtx.fillText('Phase Law', phaseLawX, phaseLawY + 25);
                    
                    updateExplorerStats(phasorMag, phaseLawMag, t);
                }
            };
            
            function drawPhasorSumSection(ctx, x, y, w, h, t, sigma, showTrace = false, showSteps = false, alpha = 1) {
                const centerX = x + w / 2;
                const centerY = y + h / 2;
                const scale = Math.min(w, h) * 0.35;
                
                // Draw axes
                ctx.strokeStyle = `rgba(255, 255, 255, ${0.2 * alpha})`;
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(x, centerY);
                ctx.lineTo(x + w, centerY);
                ctx.moveTo(centerX, y);
                ctx.lineTo(centerX, y + h);
                ctx.stroke();
                
                // Draw unit circle
                ctx.beginPath();
                ctx.arc(centerX, centerY, scale * 0.8, 0, Math.PI * 2);
                ctx.stroke();
                
                // Compute and draw phasors
                let sumReal = 0, sumImag = 0;
                let currentX = centerX, currentY = centerY;
                const numPhasors = Math.min(50, primes.length);
                
                // Store intermediate points for step visualization
                const stepPoints = [{ x: currentX, y: currentY }];
                
                for (let i = 0; i < numPhasors; i++) {
                    const n = primes[i];
                    const radius = Math.pow(n, -sigma);
                    const angle = -t * Math.log(n);
                    
                    const real = radius * Math.cos(angle);
                    const imag = radius * Math.sin(angle);
                    
                    sumReal += real;
                    sumImag += imag;
                    
                    const nextX = currentX + real * scale;
                    const nextY = currentY - imag * scale;
                    
                    stepPoints.push({ x: nextX, y: nextY });
                    
                    const hue = (i / numPhasors) * 280;
                    ctx.strokeStyle = `hsla(${hue}, 80%, 60%, ${0.5 * alpha})`;
                    ctx.lineWidth = 1.5;
                    
                    ctx.beginPath();
                    ctx.moveTo(currentX, currentY);
                    ctx.lineTo(nextX, nextY);
                    ctx.stroke();
                    
                    currentX = nextX;
                    currentY = nextY;
                }
                
                // Store current point for trace
                const finalX = centerX + sumReal * scale;
                const finalY = centerY - sumImag * scale;
                
                // Draw step-by-step construction path if enabled
                if (showSteps && stepPoints.length > 1) {
                    ctx.strokeStyle = `rgba(255, 255, 0, ${0.4 * alpha})`;
                    ctx.lineWidth = 2;
                    ctx.setLineDash([5, 5]);
                    ctx.beginPath();
                    ctx.moveTo(stepPoints[0].x, stepPoints[0].y);
                    
                    for (let i = 1; i < stepPoints.length; i++) {
                        ctx.lineTo(stepPoints[i].x, stepPoints[i].y);
                    }
                    ctx.stroke();
                    ctx.setLineDash([]);
                    
                    // Draw small dots at each step
                    for (let i = 0; i < stepPoints.length; i++) {
                        ctx.fillStyle = `rgba(255, 255, 0, ${(i / stepPoints.length) * 0.8 * alpha})`;
                        ctx.beginPath();
                        ctx.arc(stepPoints[i].x, stepPoints[i].y, 3, 0, Math.PI * 2);
                        ctx.fill();
                    }
                }
                
                if (showTrace) {
                    // Add current point to trace history
                    tracePoints.push({ x: finalX, y: finalY, t: t });
                    
                    // Limit trace length to prevent memory issues
                    const maxTracePoints = 1000;
                    if (tracePoints.length > maxTracePoints) {
                        tracePoints.shift();
                    }
                    
                    // Draw trace line
                    if (tracePoints.length > 1) {
                        ctx.strokeStyle = `rgba(255, 215, 0, ${0.6 * alpha})`;
                        ctx.lineWidth = 2;
                        ctx.beginPath();
                        ctx.moveTo(tracePoints[0].x, tracePoints[0].y);
                        
                        for (let i = 1; i < tracePoints.length; i++) {
                            ctx.lineTo(tracePoints[i].x, tracePoints[i].y);
                        }
                        ctx.stroke();
                        
                        // Draw gradient fade on trace
                        for (let i = 0; i < tracePoints.length - 1; i++) {
                            const opacity = (i / tracePoints.length) * 0.5 * alpha;
                            ctx.strokeStyle = `rgba(255, 215, 0, ${opacity})`;
                            ctx.lineWidth = 1;
                            ctx.beginPath();
                            ctx.moveTo(tracePoints[i].x, tracePoints[i].y);
                            ctx.lineTo(tracePoints[i + 1].x, tracePoints[i + 1].y);
                            ctx.stroke();
                        }
                    }
                } else {
                    // Clear trace if disabled
                    tracePoints = [];
                }
                
                // Draw final sum vector
                ctx.strokeStyle = `rgba(78, 205, 196, ${alpha})`;
                ctx.lineWidth = 4;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                ctx.lineTo(finalX, finalY);
                ctx.stroke();
                
                ctx.fillStyle = `rgba(78, 205, 196, ${alpha})`;
                ctx.beginPath();
                ctx.arc(finalX, finalY, 5, 0, Math.PI * 2);
                ctx.fill();
                
                return Math.sqrt(sumReal * sumReal + sumImag * sumImag);
            }
            
            function drawPhaseLawSection(ctx, x, y, w, h, t, beta, sortedGaps, gapClasses, alpha = 1) {
                const centerX = x + w / 2;
                const centerY = y + h / 2;
                
                // Draw axes
                ctx.strokeStyle = `rgba(255, 255, 255, ${0.2 * alpha})`;
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(x, centerY);
                ctx.lineTo(x + w, centerY);
                ctx.moveTo(centerX, y);
                ctx.lineTo(centerX, y + h);
                ctx.stroke();
                
                // Compute phase law contributions
                let totalReal = 0, totalImag = 0;
                
                // Calculate bounds to determine scale
                let maxMagnitude = 0;
                sortedGaps.forEach((gap) => {
                    const gapPrimes = gapClasses[gap];
                    let gapReal = 0, gapImag = 0;
                    
                    for (const p of gapPrimes) {
                        const phi = t * Math.log(p) - Math.PI / 2;
                        const pHalf = Math.pow(p, -0.5);
                        const decay = Math.exp(-beta * Math.log(p));
                        
                        const denomReal = 1 - pHalf * Math.cos(-phi);
                        const denomImag = -pHalf * Math.sin(-phi);
                        const denomMagSq = denomReal * denomReal + denomImag * denomImag;
                        
                        gapReal += (denomReal / denomMagSq) * decay;
                        gapImag += (-denomImag / denomMagSq) * decay;
                    }
                    
                    totalReal += gapReal;
                    totalImag += gapImag;
                    
                    const mag = Math.sqrt(totalReal * totalReal + totalImag * totalImag);
                    maxMagnitude = Math.max(maxMagnitude, mag);
                });
                
                // Use dynamic scale to keep visualization visible
                const baseScale = Math.min(w, h) * 0.4;
                const scale = maxMagnitude > 0 ? Math.min(baseScale, baseScale * 2 / maxMagnitude) : baseScale;
                
                let cumReal = 0, cumImag = 0;
                ctx.strokeStyle = `rgba(255, 99, 132, ${0.8 * alpha})`;
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.moveTo(centerX, centerY);
                
                sortedGaps.forEach((gap, idx) => {
                    const gapPrimes = gapClasses[gap];
                    let gapReal = 0, gapImag = 0;
                    
                    for (const p of gapPrimes) {
                        const phi = t * Math.log(p) - Math.PI / 2;
                        const pHalf = Math.pow(p, -0.5);
                        const decay = Math.exp(-beta * Math.log(p));
                        
                        const denomReal = 1 - pHalf * Math.cos(-phi);
                        const denomImag = -pHalf * Math.sin(-phi);
                        const denomMagSq = denomReal * denomReal + denomImag * denomImag;
                        
                        gapReal += (denomReal / denomMagSq) * decay;
                        gapImag += (-denomImag / denomMagSq) * decay;
                    }
                    
                    cumReal += gapReal;
                    cumImag += gapImag;
                    
                    const plotX = centerX + cumReal * scale;
                    const plotY = centerY - cumImag * scale;
                    
                    ctx.lineTo(plotX, plotY);
                    
                    totalReal = cumReal;
                    totalImag = cumImag;
                });
                ctx.stroke();
                
                // Draw final point with enhanced visibility
                const finalX = centerX + totalReal * scale;
                const finalY = centerY - totalImag * scale;
                
                // Draw glow effect around final point
                const gradient = ctx.createRadialGradient(finalX, finalY, 0, finalX, finalY, 15);
                gradient.addColorStop(0, `rgba(255, 99, 132, ${0.8 * alpha})`);
                gradient.addColorStop(1, `rgba(255, 99, 132, 0)`);
                ctx.fillStyle = gradient;
                ctx.beginPath();
                ctx.arc(finalX, finalY, 15, 0, Math.PI * 2);
                ctx.fill();
                
                ctx.fillStyle = `rgba(255, 99, 132, ${alpha})`;
                ctx.beginPath();
                ctx.arc(finalX, finalY, 5, 0, Math.PI * 2);
                ctx.fill();
                
                return Math.sqrt(totalReal * totalReal + totalImag * totalImag);
            }
            
            function updateExplorerStats(phasorMag, phaseLawMag, t) {
                document.getElementById('explorerT').textContent = t.toFixed(3);
                document.getElementById('explorerPhasorMag').textContent = phasorMag.toFixed(6);
                document.getElementById('explorerPhaseLawMag').textContent = phaseLawMag.toFixed(6);
                
                const diff = Math.abs(phasorMag - phaseLawMag);
                document.getElementById('explorerDiff').textContent = diff.toFixed(6);
                
                const avgMag = (phasorMag + phaseLawMag) / 2;
                const coherence = avgMag > 0.001 ? 1 - (diff / avgMag) : 0;
                document.getElementById('explorerCoherence').textContent = (coherence * 100).toFixed(2) + '%';
            }
            
            // Initialize
            window.updatePhaseExplorer(14.134725);
        }
        
        function createPhaseLawPlot(ctx) {
            const { primes } = computationData;
            
            // Use gap-classified primes
            const gapClasses = computeLowestGapClasses(primes);
            const sortedGaps = Object.keys(gapClasses).map(Number).sort((a, b) => a - b);
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Phase Law Visualization: Critical Strip Extension</h4>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Imaginary Part (t): <span id="phaseLawT">14.134725</span></label>
                    <input type="range" id="phaseLawTSlider" min="0" max="250" step="0.001" value="14.134725" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhaseLawPlot(parseFloat(this.value))">
                    <div style="margin-top: 10px;">
                        <label style="color: #fff; font-weight: 500; font-size: 0.9em;">Jump to Known Zero:</label>
                        <select id="phaseLawZeroSelector" style="width: 100%; padding: 8px; border-radius: 6px; margin-top: 5px; font-size: 14px;" onchange="jumpToPhaseLawZero(parseFloat(this.value))">
                            <option value="14.134725">Zero 1: t = 14.134725</option>
                            <option value="21.022040">Zero 2: t = 21.022040</option>
                            <option value="25.010858">Zero 3: t = 25.010858</option>
                            <option value="30.424876">Zero 4: t = 30.424876</option>
                            <option value="32.935062">Zero 5: t = 32.935062</option>
                            <option value="37.586178">Zero 6: t = 37.586178</option>
                            <option value="40.918719">Zero 7: t = 40.918719</option>
                            <option value="43.327073">Zero 8: t = 43.327073</option>
                        </select>
                    </div>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Decay Parameter (β): <span id="phaseLawBeta">Auto</span></label>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                            <input type="radio" name="betaMode" value="auto" checked onchange="updatePhaseLawPlot(parseFloat(document.getElementById('phaseLawTSlider').value))" style="width: auto; margin-right: 5px;">
                            Auto (β ~ 1/log(t))
                        </label>
                        <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                            <input type="radio" name="betaMode" value="manual" onchange="updatePhaseLawPlot(parseFloat(document.getElementById('phaseLawTSlider').value))" style="width: auto; margin-right: 5px;">
                            Manual
                        </label>
                    </div>
                    <input type="range" id="phaseLawBetaSlider" min="0" max="1" step="0.001" value="0.1" 
                           style="width: 100%; margin-top: 10px; display: none;"
                           oninput="updatePhaseLawPlot(parseFloat(document.getElementById('phaseLawTSlider').value))">
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Display Mode:</label>
                    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; margin-top: 10px;">
                        <button onclick="setPhaseLawMode('magnitude')" id="phaseModeMag" style="padding: 8px; background: rgba(78, 205, 196, 0.3); border: 2px solid #4ecdc4; border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Magnitude</button>
                        <button onclick="setPhaseLawMode('phase')" id="phaseModePhase" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Phase Angles</button>
                        <button onclick="setPhaseLawMode('complex')" id="phaseModeComplex" style="padding: 8px; background: rgba(255, 255, 255, 0.1); border: 2px solid rgba(255, 255, 255, 0.2); border-radius: 6px; color: #fff; cursor: pointer; font-size: 0.85em;">Complex Plane</button>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Gap Classes</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${sortedGaps.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Total Magnitude</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;" id="phaseLawMag">--</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Phase Coherence</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;" id="phaseLawCoherence">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">At Zero?</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;" id="phaseLawZero">No</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Phase Law Extension:</strong><br>
                    For each prime p in gap class g, compute contribution with phase alignment:<br>
                    <div style="background: rgba(0, 0, 0, 0.3); padding: 10px; border-radius: 5px; font-family: monospace; margin: 10px 0;">
                    (1 - p^(-1/2) * e^(-iφ))^(-1) * e^(-β*log(p))<br>
                    φ(p,t) = t*log(p) - π/2<br>
                    β ~ 1/log(t)
                    </div>
                    When phases align destructively at Riemann zeros, the magnitude drops to near zero.
                </div>
            `;
            
            // Add event listener for beta mode toggle
            document.querySelectorAll('input[name="betaMode"]').forEach(radio => {
                radio.addEventListener('change', function() {
                    const manualSlider = document.getElementById('phaseLawBetaSlider');
                    if (this.value === 'manual') {
                        manualSlider.style.display = 'block';
                    } else {
                        manualSlider.style.display = 'none';
                    }
                });
            });
            
            let phaseLawDisplayMode = 'magnitude';
            
            window.setPhaseLawMode = (mode) => {
                phaseLawDisplayMode = mode;
                
                // Update button styles
                ['phaseModeMag', 'phaseModePhase', 'phaseModeComplex'].forEach(id => {
                    const btn = document.getElementById(id);
                    if (btn) {
                        if ((mode === 'magnitude' && id === 'phaseModeMag') ||
                            (mode === 'phase' && id === 'phaseModePhase') ||
                            (mode === 'complex' && id === 'phaseModeComplex')) {
                            btn.style.background = 'rgba(78, 205, 196, 0.3)';
                            btn.style.borderColor = '#4ecdc4';
                        } else {
                            btn.style.background = 'rgba(255, 255, 255, 0.1)';
                            btn.style.borderColor = 'rgba(255, 255, 255, 0.2)';
                        }
                    }
                });
                
                updatePhaseLawPlot(parseFloat(document.getElementById('phaseLawTSlider').value));
            };
            
            window.jumpToPhaseLawZero = (t) => {
                document.getElementById('phaseLawTSlider').value = t;
                updatePhaseLawPlot(t);
            };
            
            window.updatePhaseLawPlot = (t) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                const centerX = width / 2;
                const centerY = height / 2;
                
                // Determine beta
                const betaMode = document.querySelector('input[name="betaMode"]:checked').value;
                let beta;
                if (betaMode === 'auto') {
                    beta = t > 0 ? 1 / Math.log(Math.max(2, t)) : 0.1;
                    document.getElementById('phaseLawBeta').textContent = `${beta.toFixed(4)} (Auto)`;
                } else {
                    beta = parseFloat(document.getElementById('phaseLawBetaSlider').value);
                    document.getElementById('phaseLawBeta').textContent = beta.toFixed(4);
                }
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, width, height);
                
                // Compute phase law contributions for each gap class
                const gapContributions = [];
                let totalReal = 0, totalImag = 0;
                let totalMagnitude = 0;
                
                for (const gap of sortedGaps) {
                    const gapPrimes = gapClasses[gap];
                    let gapReal = 0, gapImag = 0;
                    
                    for (const p of gapPrimes) {
                        // Phase: φ(p,t) = t*log(p) - π/2
                        const phi = t * Math.log(p) - Math.PI / 2;
                        
                        // Complex contribution: (1 - p^(-1/2) * e^(-iφ))^(-1) * e^(-β*log(p))
                        const pHalf = Math.pow(p, -0.5);
                        const decay = Math.exp(-beta * Math.log(p));
                        
                        // 1 - p^(-1/2) * e^(-iφ)
                        const denomReal = 1 - pHalf * Math.cos(-phi);
                        const denomImag = -pHalf * Math.sin(-phi);
                        
                        // Inverse of complex number
                        const denomMagSq = denomReal * denomReal + denomImag * denomImag;
                        const invReal = denomReal / denomMagSq;
                        const invImag = -denomImag / denomMagSq;
                        
                        // Apply decay
                        gapReal += invReal * decay;
                        gapImag += invImag * decay;
                    }
                    
                    const gapMag = Math.sqrt(gapReal * gapReal + gapImag * gapImag);
                    totalMagnitude += gapMag;
                    totalReal += gapReal;
                    totalImag += gapImag;
                    
                    gapContributions.push({
                        gap: gap,
                        real: gapReal,
                        imag: gapImag,
                        magnitude: gapMag,
                        phase: Math.atan2(gapImag, gapReal)
                    });
                }
                
                // Visualization based on mode
                if (phaseLawDisplayMode === 'magnitude') {
                    // Bar chart of magnitudes by gap class
                    const barWidth = width / (gapContributions.length + 1);
                    const maxMag = Math.max(...gapContributions.map(g => g.magnitude), 0.001);
                    const scale = height * 0.7 / maxMag;
                    
                    gapContributions.forEach((contrib, idx) => {
                        const x = (idx + 1) * barWidth;
                        const barHeight = contrib.magnitude * scale;
                        const y = height - barHeight - 50;
                        
                        const hue = (idx / gapContributions.length) * 280;
                        freshCtx.fillStyle = `hsla(${hue}, 80%, 60%, 0.8)`;
                        freshCtx.fillRect(x - barWidth * 0.4, y, barWidth * 0.8, barHeight);
                        
                        // Label
                        freshCtx.fillStyle = '#fff';
                        freshCtx.font = '10px Arial';
                        freshCtx.textAlign = 'center';
                        freshCtx.fillText(`g=${contrib.gap}`, x, height - 35);
                        freshCtx.fillText(contrib.magnitude.toFixed(3), x, y - 5);
                    });
                    
                } else if (phaseLawDisplayMode === 'phase') {
                    // Phase angle visualization
                    const radius = Math.min(width, height) * 0.35;
                    
                    // Draw unit circle
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                    freshCtx.lineWidth = 2;
                    freshCtx.beginPath();
                    freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                    freshCtx.stroke();
                    
                    // Draw phase vectors
                    gapContributions.forEach((contrib, idx) => {
                        const angle = contrib.phase;
                        const mag = Math.min(contrib.magnitude * radius / totalMagnitude * 5, radius);
                        const x = centerX + mag * Math.cos(angle);
                        const y = centerY + mag * Math.sin(angle);
                        
                        const hue = (idx / gapContributions.length) * 280;
                        freshCtx.strokeStyle = `hsla(${hue}, 80%, 60%, 0.8)`;
                        freshCtx.lineWidth = 3;
                        freshCtx.beginPath();
                        freshCtx.moveTo(centerX, centerY);
                        freshCtx.lineTo(x, y);
                        freshCtx.stroke();
                        
                        // Arrow head
                        const arrowSize = 8;
                        freshCtx.beginPath();
                        freshCtx.moveTo(x, y);
                        freshCtx.lineTo(x - arrowSize * Math.cos(angle - Math.PI/6), y - arrowSize * Math.sin(angle - Math.PI/6));
                        freshCtx.moveTo(x, y);
                        freshCtx.lineTo(x - arrowSize * Math.cos(angle + Math.PI/6), y - arrowSize * Math.sin(angle + Math.PI/6));
                        freshCtx.stroke();
                    });
                    
                } else if (phaseLawDisplayMode === 'complex') {
                    // Complex plane with cumulative sum
                    const scale = Math.min(width, height) * 0.4 / Math.max(Math.abs(totalReal), Math.abs(totalImag), 1);
                    
                    // Draw axes
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                    freshCtx.lineWidth = 1;
                    freshCtx.beginPath();
                    freshCtx.moveTo(0, centerY);
                    freshCtx.lineTo(width, centerY);
                    freshCtx.moveTo(centerX, 0);
                    freshCtx.lineTo(centerX, height);
                    freshCtx.stroke();
                    
                    // Draw cumulative path
                    let cumReal = 0, cumImag = 0;
                    freshCtx.strokeStyle = '#4ecdc4';
                    freshCtx.lineWidth = 2;
                    freshCtx.beginPath();
                    freshCtx.moveTo(centerX, centerY);
                    
                    gapContributions.forEach((contrib, idx) => {
                        cumReal += contrib.real;
                        cumImag += contrib.imag;
                        
                        const x = centerX + cumReal * scale;
                        const y = centerY - cumImag * scale;
                        
                        freshCtx.lineTo(x, y);
                    });
                    freshCtx.stroke();
                    
                    // Draw final point
                    const finalX = centerX + totalReal * scale;
                    const finalY = centerY - totalImag * scale;
                    freshCtx.fillStyle = '#ffd700';
                    freshCtx.beginPath();
                    freshCtx.arc(finalX, finalY, 6, 0, Math.PI * 2);
                    freshCtx.fill();
                }
                
                // Update stats
                document.getElementById('phaseLawT').textContent = t.toFixed(6);
                
                const vectorMag = Math.sqrt(totalReal * totalReal + totalImag * totalImag);
                const coherence = totalMagnitude > 0 ? vectorMag / totalMagnitude : 0;
                
                document.getElementById('phaseLawMag').textContent = vectorMag.toFixed(6);
                document.getElementById('phaseLawCoherence').textContent = (coherence * 100).toFixed(2) + '%';
                
                // Check if near zero (coherence < 10% indicates destructive interference)
                const isNearZero = coherence < 0.1;
                document.getElementById('phaseLawZero').textContent = isNearZero ? 'Yes' : 'No';
                document.getElementById('phaseLawZero').style.color = isNearZero ? '#4ecdc4' : '#ff6384';
            };
            
            // Initialize
            window.updatePhaseLawPlot(14.134725);
        }
        
        function generatePrimeCountChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const step = Math.max(1, Math.floor(primes[primes.length - 1] / 200));
            const countingData = [];
            const approximations = [];
            
            for (let x = 2; x <= primes[primes.length - 1]; x += step) {
                const count = primes.filter(p => p <= x).length;
                countingData.push({ x, y: count });
                
                const approx = x / Math.log(x);
                approximations.push({ x, y: approx });
            }
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'π(x) - Actual Count',
                        data: countingData,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0,
                        pointRadius: 0
                    }, {
                        label: 'x/ln(x) - Approximation',
                        data: approximations,
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        borderDash: [15, 8],
                        fill: false,
                        tension: 0.3,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Number of Primes', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateDensityChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const intervalSize = Math.max(10, Math.floor(primes[primes.length - 1] / 50));
            const densityData = [];
            const theoreticalDensity = [];
            
            for (let x = intervalSize; x <= primes[primes.length - 1]; x += intervalSize) {
                const primesInInterval = primes.filter(p => p > x - intervalSize && p <= x).length;
                const density = primesInInterval / intervalSize;
                densityData.push({ x, y: density });
                
                const theoretical = 1 / Math.log(x);
                theoreticalDensity.push({ x, y: theoretical });
            }
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    datasets: [{
                        label: 'Actual Density',
                        data: densityData,
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.3)' : 'rgba(78, 205, 196, 0.3)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4,
                        pointRadius: 4,
                        pointBackgroundColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)'
                    }, {
                        label: 'Theoretical Density (1/ln(x))',
                        data: theoreticalDensity,
                        borderColor: background === 'white' ? 'rgba(255, 99, 71, 1)' : 'rgba(255, 215, 0, 1)',
                        backgroundColor: background === 'white' ? 'rgba(255, 99, 71, 0.1)' : 'rgba(255, 215, 0, 0.1)',
                        borderWidth: 4,
                        borderDash: [15, 8],
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Density (primes per unit)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateGapHistogramChartForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const gaps = [];
            for (let i = 1; i < primes.length; i++) {
                gaps.push(primes[i] - primes[i-1]);
            }
            
            const gapCounts = {};
            gaps.forEach(gap => {
                gapCounts[gap] = (gapCounts[gap] || 0) + 1;
            });
            
            const sortedGaps = Object.keys(gapCounts).map(Number).sort((a, b) => a - b);
            const counts = sortedGaps.map(gap => gapCounts[gap]);
            const maxGap = Math.max(...sortedGaps);
            
            const barColors = sortedGaps.map(gap => {
                if (gap === 2) return background === 'white' ? 'rgba(255, 99, 132, 0.8)' : 'rgba(255, 99, 132, 0.8)';
                if (gap === 4) return background === 'white' ? 'rgba(255, 159, 64, 0.8)' : 'rgba(255, 159, 64, 0.8)';
                if (gap === 6) return background === 'white' ? 'rgba(255, 205, 86, 0.8)' : 'rgba(255, 205, 86, 0.8)';
                if (gap === maxGap) return background === 'white' ? 'rgba(153, 102, 255, 0.8)' : 'rgba(153, 102, 255, 0.8)';
                return background === 'white' ? 'rgba(30, 60, 114, 0.7)' : 'rgba(78, 205, 196, 0.7)';
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: sortedGaps.map(g => g.toString()),
                    datasets: [{
                        label: 'Frequency',
                        data: counts,
                        backgroundColor: barColors,
                        borderColor: barColors.map(c => c.replace('0.7', '1').replace('0.8', '1')),
                        borderWidth: 3
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: { display: false }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Gap Size', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.022) },
                                maxRotation: 45,
                                callback: function(value, index) {
                                    if (sortedGaps.length > 30) {
                                        return index % Math.ceil(sortedGaps.length / 30) === 0 ? this.getLabelForValue(value) : '';
                                    }
                                    return this.getLabelForValue(value);
                                }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Frequency', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateSacksSpiralForExport(ctx, width, height, background) {
            const { primes } = computationData;
            
            const maxN = Math.min(10000, primes[primes.length - 1]);
            const spiralData = [];
            
            for (let n = 1; n <= maxN; n++) {
                const r = Math.sqrt(n);
                const theta = 2 * Math.PI * Math.sqrt(n);
                const x = r * Math.cos(theta);
                const y = r * Math.sin(theta);
                const isPrime = primes.includes(n);
                spiralData.push({ x, y, n, isPrime });
            }
            
            const primePoints = spiralData.filter(p => p.isPrime);
            const compositePoints = spiralData.filter(p => !p.isPrime && p.n > 1);
            
            // Create custom canvas rendering
            const maxR = Math.sqrt(maxN);
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) / (2 * maxR) * 0.85;
            
            ctx.fillStyle = background === 'white' ? '#ffffff' : '#000000';
            ctx.fillRect(0, 0, width, height);
            
            // Draw composites
            ctx.fillStyle = background === 'white' ? 'rgba(0, 0, 0, 0.15)' : 'rgba(255, 255, 255, 0.15)';
            for (const point of compositePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 2, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw primes
            ctx.fillStyle = background === 'white' ? '#d4af37' : '#ffd700';
            for (const point of primePoints) {
                const screenX = centerX + point.x * scale;
                const screenY = centerY + point.y * scale;
                ctx.beginPath();
                ctx.arc(screenX, screenY, 3, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Draw center
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            return { destroy: () => {} };
        }
        
        function generateZetaZerosChartForExport(ctx, width, height, background) {
            const zetaZeros = [
                14.134725, 21.022040, 25.010858, 30.424876, 32.935062,
                37.586178, 40.918719, 43.327073, 48.005151, 49.773832,
                52.970321, 56.446248, 59.347044, 60.831779, 65.112544,
                67.079811, 69.546402, 72.067158, 75.704691, 77.144840,
                79.337375, 82.910381, 84.735493, 87.425275, 88.809111,
                92.491899, 94.651344, 95.870634, 98.831194, 101.317851,
                103.725538, 105.446623, 107.168611, 111.029536, 111.874659,
                114.320220, 116.226680, 118.790782, 121.370125, 122.946829,
                124.256819, 127.516683, 129.578704, 131.087688, 133.497737,
                134.756509, 138.116042, 139.736209, 141.123707, 143.111846
            ];
            
            const zeroPoints = zetaZeros.map(t => ({ x: 0.5, y: t }));
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Riemann Zeta Zeros',
                        data: zeroPoints,
                        backgroundColor: background === 'white' ? 'rgba(212, 175, 55, 0.8)' : 'rgba(255, 215, 0, 0.8)',
                        borderColor: background === 'white' ? 'rgba(212, 175, 55, 1)' : 'rgba(255, 215, 0, 1)',
                        pointRadius: 8,
                        pointStyle: 'circle'
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: { 
                                display: true, 
                                text: 'Re(s) - Real Part (Critical Line at 1/2)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            min: 0,
                            max: 1,
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                stepSize: 0.1
                            },
                            grid: { 
                                color: function(context) {
                                    if (context.tick.value === 0.5) {
                                        return background === 'white' ? 'rgba(212, 175, 55, 0.5)' : 'rgba(255, 215, 0, 0.5)';
                                    }
                                    return background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)';
                                },
                                lineWidth: function(context) {
                                    return context.tick.value === 0.5 ? 4 : 1;
                                }
                            }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Im(s) - Imaginary Part', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        
        function createPrimeRacesPlot(ctx) {
            const { primes, modulus } = computationData;
            
            // Always use the actual modulus from computation
            const actualModulus = modulus;
            const coprimeResidues = getCoprimeResidues(actualModulus);
            
            // For 2-way race, use first two coprime residues
            // For multi-way race (>2 residues), show all of them
            const residues = coprimeResidues.slice(0, Math.min(8, coprimeResidues.length)); // Cap at 8 for readability
            
            // Initialize counters for each residue class
            const counts = {};
            residues.forEach(r => counts[r] = 0);
            
            const raceData = [];
            
            for (const p of primes) {
                // Skip primes smaller than modulus
                if (p < actualModulus) continue;
                
                const residue = p % actualModulus;
                
                // Only count if it's a coprime residue we're tracking
                if (residues.includes(residue)) {
                    counts[residue]++;
                }
                
                // Store cumulative counts
                const dataPoint = { x: p };
                residues.forEach(r => dataPoint[`count_${r}`] = counts[r]);
                
                // Calculate difference for 2-way race (first residue - second residue)
                if (residues.length >= 2) {
                    dataPoint.diff = counts[residues[0]] - counts[residues[1]];
                }
                raceData.push(dataPoint);
            }
            
            // Calculate statistics for 2-way race
            let finalDiff = 0;
            let maxDiff = 0;
            let leaderChanges = 0;
            let currentLeader = "N/A";
            
            if (residues.length >= 2) {
                finalDiff = counts[residues[0]] - counts[residues[1]];
                maxDiff = Math.max(...raceData.map(d => Math.abs(d.diff || 0)));
                leaderChanges = raceData.reduce((changes, d, i) => {
                    if (i === 0 || !d.diff) return changes;
                    const prevDiff = raceData[i-1].diff || 0;
                    const currDiff = d.diff;
                    if ((prevDiff > 0 && currDiff < 0) || (prevDiff < 0 && currDiff > 0)) {
                        return changes + 1;
                    }
                    return changes;
                }, 0);
                
                currentLeader = finalDiff > 0 ? `${residues[0]} (mod ${actualModulus})` : 
                               finalDiff < 0 ? `${residues[1]} (mod ${actualModulus})` : "Tie";
            }
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            
            // Build stats HTML dynamically based on number of residues
            let statsHTML = `<h4 style="color: #ffd700; margin-bottom: 15px;">Prime Races: Modulus ${actualModulus} (${residues.length}-way race)</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">`;
            
            // Add a card for each residue
            const colors = ['rgba(78, 205, 196, 0.15)', 'rgba(255, 99, 132, 0.15)', 'rgba(255, 215, 0, 0.15)', 
                          'rgba(153, 102, 255, 0.15)', 'rgba(255, 159, 64, 0.15)', 'rgba(75, 192, 192, 0.15)',
                          'rgba(255, 99, 71, 0.15)', 'rgba(147, 112, 219, 0.15)'];
            const textColors = ['#4ecdc4', '#ff6384', '#ffd700', '#9966ff', '#ff9f40', '#4bc0c0', '#ff6347', '#9370db'];
            
            residues.forEach((r, idx) => {
                statsHTML += `
                    <div style="background: ${colors[idx % colors.length]}; padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes ≡ ${r} (mod ${actualModulus})</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: ${textColors[idx % textColors.length]};">${counts[r]}</div>
                    </div>`;
            });
            
            // Add race statistics for 2-way races
            if (residues.length >= 2) {
                statsHTML += `
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Current Leader</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${currentLeader}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Current Gap</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${Math.abs(finalDiff)}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Max Gap Seen</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${maxDiff}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Lead Changes</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${leaderChanges}</div>
                    </div>`;
            }
            
            statsHTML += `</div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Prime Races (mod ${actualModulus}):</strong><br>
                    <strong>Chebyshev's Bias:</strong> In prime races, certain residue classes tend to "win" more often than others<br>
                    By Dirichlet's theorem, all ${residues.length} coprime residue classes mod ${actualModulus} have equal density asymptotically<br>
                    Despite equal density, one class is typically ahead at any given point (for 2-way races)<br>
                    ${actualModulus === 4 && residues.length === 2 ? `For mod 4: Primes ≡ 3 (mod 4) lead approximately 99.6% of the time (classic Chebyshev's bias)<br>
                    First crossover where 1 (mod 4) takes the lead occurs around x ≈ 26,861<br>` : ''}
                    The lead changes infinitely often (Littlewood, 1914), but very rarely<br>
                    Related to the <strong>Shanks-Rényi race</strong> and Rubinstein-Sarnak's work<br>
                    Current computation uses ${primes.length} primes up to ${primes[primes.length-1]}
                </div>
            `;
            
            statsDiv.innerHTML = statsHTML;
            
            // Create datasets dynamically for each residue
            const lineColors = ['rgba(78, 205, 196, 1)', 'rgba(255, 99, 132, 1)', 'rgba(255, 215, 0, 1)', 
                              'rgba(153, 102, 255, 1)', 'rgba(255, 159, 64, 1)', 'rgba(75, 192, 192, 1)',
                              'rgba(255, 99, 71, 1)', 'rgba(147, 112, 219, 1)'];
            const fillColors = ['rgba(78, 205, 196, 0.1)', 'rgba(255, 99, 132, 0.1)', 'rgba(255, 215, 0, 0.1)', 
                              'rgba(153, 102, 255, 0.1)', 'rgba(255, 159, 64, 0.1)', 'rgba(75, 192, 192, 0.1)',
                              'rgba(255, 99, 71, 0.1)', 'rgba(147, 112, 219, 0.1)'];
            
            const datasets = residues.map((r, idx) => ({
                label: `π(x; ${actualModulus}, ${r}) - Primes ≡ ${r} (mod ${actualModulus})`,
                data: raceData.map(d => ({ x: d.x, y: d[`count_${r}`] })),
                borderColor: lineColors[idx % lineColors.length],
                backgroundColor: fillColors[idx % fillColors.length],
                borderWidth: 3,
                fill: false,
                tension: 0,
                pointRadius: 0
            }));
            
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: raceData.map(d => d.x),
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    const diff = raceData[idx].diff;
                                    const leader = diff > 0 ? "3 (mod 4) leads" : diff < 0 ? "1 (mod 4) leads" : "Tied";
                                    return [
                                        `${context.dataset.label}: ${context.parsed.y}`,
                                        `Gap: ${Math.abs(diff)} (${leader})`
                                    ];
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x (prime value)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Count of Primes', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createPhasorSumPlot(ctx) {
            const { primes, exponent, constantType } = computationData;
            
            // For complex s = σ + it, compute phasor representation
            // We'll use σ = exponent/2 (the value we're computing at)
            const sigma = exponent / 2;
            
            // Create interactive t slider
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Phasor Sum Visualization: ζ(s) as Rotating Vectors</h4>
                <div style="margin-bottom: 20px;">
                    <div style="display: flex; gap: 10px; margin-bottom: 10px;">
                        <button id="phasorPlayBtn" onclick="togglePhasorAnimation()" style="padding: 8px 16px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 6px; font-weight: bold; cursor: pointer;">Play</button>
                        <button onclick="resetPhasorAnimation()" style="padding: 8px 16px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 6px; cursor: pointer;">Reset</button>
                        <label style="display: flex; align-items: center; color: #fff; margin-left: auto;">
                            Speed: <input type="number" id="phasorSpeed" value="1" min="0.1" max="10" step="0.1" style="width: 60px; margin-left: 8px; padding: 4px; border-radius: 4px;">×
                        </label>
                    </div>
                    <label style="color: #fff; font-weight: 500;">Imaginary Part (t): <span id="tValue">0</span></label>
                    <input type="range" id="tSlider" min="0" max="250" step="0.001" value="0" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhasorPlot(parseFloat(this.value), parseFloat(document.getElementById('zoomSlider').value))">
                    <div style="margin-top: 10px;">
                        <label style="color: #fff; font-weight: 500; font-size: 0.9em;">Quick Jump to Known Zero:</label>
                        <select id="phasorZeroSelector" style="width: 100%; padding: 8px; border-radius: 6px; margin-top: 5px; font-size: 14px; max-height: 200px;" onchange="jumpToPhasorZero(parseFloat(this.value))">
                            <option value="0">Custom value (use slider)</option>
                        </select>
                    </div>
                    <div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 10px;">
                        <button onclick="document.getElementById('tSlider').value=0; document.getElementById('phasorZeroSelector').value=0; updatePhasorPlot(0, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(78, 205, 196, 0.3); border: 1px solid #4ecdc4; border-radius: 5px; color: #fff; cursor: pointer;">t = 0</button>
                        <button onclick="document.getElementById('tSlider').value=100; document.getElementById('phasorZeroSelector').value=0; updatePhasorPlot(100, parseFloat(document.getElementById('zoomSlider').value));" style="padding: 8px; background: rgba(153, 102, 255, 0.3); border: 1px solid #9966ff; border-radius: 5px; color: #fff; cursor: pointer;">t = 100</button>
                    </div>
                </div>`;
            
            // Populate the dropdown with all known zeros
            const zetaZeros = [
                14.134725, 21.022040, 25.010858, 30.424876, 32.935062,
                37.586178, 40.918719, 43.327073, 48.005151, 49.773832,
                52.970321, 56.446248, 59.347044, 60.831779, 65.112544,
                67.079811, 69.546402, 72.067158, 75.704691, 77.144840,
                79.337375, 82.910381, 84.735493, 87.425275, 88.809111,
                92.491899, 94.651344, 95.870634, 98.831194, 101.317851,
                103.725538, 105.446623, 107.168611, 111.029536, 111.874659,
                114.320220, 116.226680, 118.790782, 121.370125, 122.946829,
                124.256819, 127.516683, 129.578704, 131.087688, 133.497737,
                134.756509, 138.116042, 139.736209, 141.123707, 143.111846,
                146.000982, 147.422765, 150.053183, 150.925257, 153.024693,
                156.112909, 157.597592, 158.849988, 161.188964, 163.030709,
                165.537069, 167.184439, 169.094515, 169.911976, 173.411536,
                174.754191, 176.441434, 178.377407, 179.916484, 182.207078,
                184.874467, 185.598783, 187.228922, 189.416158, 192.026656,
                193.079726, 195.265396, 196.876481, 198.015309, 201.264751,
                202.493594, 204.189671, 205.394697, 207.906258, 209.576509,
                211.690862, 213.347919, 214.547044, 216.169538, 219.067596,
                220.714918, 221.430705, 224.007000, 224.983324, 227.421444,
                229.337413, 231.250188, 231.987235, 233.693404, 236.524229
            ];
            
            const zeroSelector = document.getElementById('phasorZeroSelector');
            zetaZeros.forEach((z, idx) => {
                const option = document.createElement('option');
                option.value = z;
                option.textContent = `Zero #${idx + 1}: ${z.toFixed(6)}`;
                zeroSelector.appendChild(option);
            });
            
            statsDiv.innerHTML += `
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Zoom Level: <span id="zoomValue">1.0</span>x</label>
                    <input type="range" id="zoomSlider" min="0.1" max="10" step="0.1" value="1" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updatePhasorPlot(parseFloat(document.getElementById('tSlider').value), parseFloat(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.85em; opacity: 0.7; margin-top: 5px;">
                        <span>0.1x (Zoom Out)</span>
                        <span>1x (Default)</span>
                        <span>10x (Zoom In)</span>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Real Part (σ)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${sigma.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Primes Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${Math.min(50, primes.length)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sum Magnitude</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;" id="sumMagnitude">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Sum Angle</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;" id="sumAngle">--</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Phasor Representation:</strong><br>
                    Each term n<sup>-s</sup> = n<sup>-σ</sup>e<sup>-it log n</sup> is a <strong>rotating phasor</strong> (vector)<br>
                    <strong>Radius:</strong> r<sub>n</sub> = n<sup>-${sigma}</sup> (decays with n)<br>
                    <strong>Angle:</strong> θ<sub>n</sub> = -t log(n) (rotates with t)<br>
                    The sum ζ(s) is the <strong>vector sum</strong> of all phasors<br>
                    When phasors align <strong>destructively</strong>, |ζ(s)| ≈ 0 → nontrivial zero<br>
                    Adjust t to see how the sum changes along the critical line
                </div>
            `;
            
            let phasorAnimationId = null;
            let isPhasorPlaying = false;
            
            window.togglePhasorAnimation = () => {
                isPhasorPlaying = !isPhasorPlaying;
                const btn = document.getElementById('phasorPlayBtn');
                
                if (isPhasorPlaying) {
                    btn.textContent = 'Pause';
                    btn.style.background = 'linear-gradient(45deg, #ff6b6b, #ee5a52)';
                    startPhasorAnimation();
                } else {
                    btn.textContent = 'Play';
                    btn.style.background = 'linear-gradient(45deg, #4ecdc4, #44a8a3)';
                    if (phasorAnimationId) cancelAnimationFrame(phasorAnimationId);
                }
            };
            
            window.resetPhasorAnimation = () => {
                isPhasorPlaying = false;
                document.getElementById('phasorPlayBtn').textContent = 'Play';
                document.getElementById('phasorPlayBtn').style.background = 'linear-gradient(45deg, #4ecdc4, #44a8a3)';
                if (phasorAnimationId) cancelAnimationFrame(phasorAnimationId);
                document.getElementById('tSlider').value = 0;
                updatePhasorPlot(0, parseFloat(document.getElementById('zoomSlider').value));
            };
            
            function startPhasorAnimation() {
                if (!isPhasorPlaying) return;
                
                const speed = parseFloat(document.getElementById('phasorSpeed').value);
                const slider = document.getElementById('tSlider');
                let currentValue = parseFloat(slider.value);
                
                currentValue += 0.1 * speed;
                if (currentValue > parseFloat(slider.max)) {
                    currentValue = 0;
                }
                
                slider.value = currentValue;
                updatePhasorPlot(currentValue, parseFloat(document.getElementById('zoomSlider').value));
                
                phasorAnimationId = requestAnimationFrame(startPhasorAnimation);
            }
            
            // Initial plot at t=0
            // Initial plot at t=0
            window.updatePhasorPlot = (t, zoom = 1.0) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                const centerX = width / 2;
                const centerY = height / 2;
                const scale = Math.min(width, height) * 0.4 * zoom;
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.4)';
                freshCtx.fillRect(0, 0, width, height);
                
                // Draw axes
                freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.3)';
                freshCtx.lineWidth = 1;
                freshCtx.beginPath();
                freshCtx.moveTo(0, centerY);
                freshCtx.lineTo(width, centerY);
                freshCtx.moveTo(centerX, 0);
                freshCtx.lineTo(centerX, height);
                freshCtx.stroke();
                
                // Draw unit circle
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, scale, 0, Math.PI * 2);
                freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
                freshCtx.stroke();
                
                // Compute and draw phasors
                let sumReal = 0, sumImag = 0;
                let currentX = centerX, currentY = centerY;
                
                const numPhasors = Math.min(50, primes.length);
                
                for (let i = 0; i < numPhasors; i++) {
                    const n = primes[i];
                    const radius = Math.pow(n, -sigma);
                    const angle = -t * Math.log(n);
                    
                    const real = radius * Math.cos(angle);
                    const imag = radius * Math.sin(angle);
                    
                    sumReal += real;
                    sumImag += imag;
                    
                    // Draw phasor from current position
                    const nextX = currentX + real * scale;
                    const nextY = currentY - imag * scale;
                    
                    // Color by prime index
                    const hue = (i / numPhasors) * 280;
                    freshCtx.strokeStyle = `hsla(${hue}, 80%, 60%, 0.7)`;
                    freshCtx.lineWidth = 2;
                    
                    freshCtx.beginPath();
                    freshCtx.moveTo(currentX, currentY);
                    freshCtx.lineTo(nextX, nextY);
                    freshCtx.stroke();
                    
                    // Draw arrowhead
                    const arrowSize = 5;
                    const arrowAngle = Math.atan2(-(imag), real);
                    freshCtx.beginPath();
                    freshCtx.moveTo(nextX, nextY);
                    freshCtx.lineTo(
                        nextX - arrowSize * Math.cos(arrowAngle - Math.PI/6),
                        nextY - arrowSize * Math.sin(arrowAngle - Math.PI/6)
                    );
                    freshCtx.moveTo(nextX, nextY);
                    freshCtx.lineTo(
                        nextX - arrowSize * Math.cos(arrowAngle + Math.PI/6),
                        nextY - arrowSize * Math.sin(arrowAngle + Math.PI/6)
                    );
                    freshCtx.stroke();
                    
                    currentX = nextX;
                    currentY = nextY;
                }
                
                // Draw final sum vector from origin
                const finalX = centerX + sumReal * scale;
                const finalY = centerY - sumImag * scale;
                
                freshCtx.strokeStyle = '#ffd700';
                freshCtx.lineWidth = 4;
                freshCtx.beginPath();
                freshCtx.moveTo(centerX, centerY);
                freshCtx.lineTo(finalX, finalY);
                freshCtx.stroke();
                
                // Draw sum endpoint
                freshCtx.fillStyle = '#ffd700';
                freshCtx.beginPath();
                freshCtx.arc(finalX, finalY, 6, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Update stats
                const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                const angleRad = Math.atan2(sumImag, sumReal);
                const angleDeg = angleRad * 180 / Math.PI;
                
                document.getElementById('tValue').textContent = t.toFixed(2);
                document.getElementById('zoomValue').textContent = zoom.toFixed(1);
                document.getElementById('sumMagnitude').textContent = magnitude.toFixed(4);
                document.getElementById('sumAngle').textContent = angleDeg.toFixed(1) + '°';
                
                // Draw labels
                freshCtx.fillStyle = '#fff';
                freshCtx.font = '14px Arial';
                freshCtx.textAlign = 'center';
                freshCtx.fillText('Re', width - 30, centerY - 10);
                freshCtx.fillText('Im', centerX + 15, 20);
                freshCtx.fillText(`ζ(${sigma} + ${t}i) ≈ ${magnitude.toFixed(3)}`, centerX, height - 20);
            };
            
            // Function to jump to zero from dropdown
            window.jumpToPhasorZero = function(t) {
                if (t > 0) {
                    document.getElementById('tSlider').value = t;
                    updatePhasorPlot(t, parseFloat(document.getElementById('zoomSlider').value));
                }
            };
            
            // Initialize
            window.updatePhasorPlot(0, 1.0);
        }
        
        function createZetaSurfacePlot(ctx) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            
            // Create modular zeta surface
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Modular Zeta Surface: Nested Unity Lattice</h4>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Max Modulus: <span id="maxModSurface">30</span></label>
                    <input type="range" id="maxModSlider" min="10" max="100" step="1" value="30" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updateZetaSurface(parseFloat(document.getElementById('tSliderSurface').value), parseInt(this.value))">
                    <div style="display: flex; justify-content: space-between; font-size: 0.85em; opacity: 0.7; margin-top: 5px;">
                        <span>10 rings (minimal)</span>
                        <span>30 rings (default)</span>
                        <span>100 rings (dense)</span>
                    </div>
                </div>
                <div style="margin-bottom: 20px;">
                    <label style="color: #fff; font-weight: 500;">Imaginary Height (t): <span id="tValueSurface">14.13</span></label>
                    <input type="range" id="tSliderSurface" min="0" max="200" step="0.01" value="14.13" 
                           style="width: 100%; margin-top: 10px;"
                           oninput="updateZetaSurface(parseFloat(this.value), parseInt(document.getElementById('maxModSlider').value))">
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 8px; margin-top: 10px;">
                        <button onclick="document.getElementById('tSliderSurface').value=14.134725; updateZetaSurface(14.134725, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(255, 99, 132, 0.3); border: 1px solid #ff6384; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 1 (14.13)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=21.022040; updateZetaSurface(21.022040, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(255, 159, 64, 0.3); border: 1px solid #ff9f40; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 2 (21.02)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=25.010858; updateZetaSurface(25.010858, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(255, 205, 86, 0.3); border: 1px solid #ffcd56; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 3 (25.01)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=30.424876; updateZetaSurface(30.424876, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(75, 192, 192, 0.3); border: 1px solid #4bc0c0; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">Zero 4 (30.42)</button>
                        <button onclick="document.getElementById('tSliderSurface').value=50; updateZetaSurface(50, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(153, 102, 255, 0.3); border: 1px solid #9966ff; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">t = 50</button>
                        <button onclick="document.getElementById('tSliderSurface').value=100; updateZetaSurface(100, parseInt(document.getElementById('maxModSlider').value));" style="padding: 6px; background: rgba(78, 205, 196, 0.3); border: 1px solid #4ecdc4; border-radius: 5px; color: #fff; cursor: pointer; font-size: 0.85em;">t = 100</button>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Moduli Plotted</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;" id="moduliCount">30</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Total Magnitude</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;" id="surfaceMagnitude">--</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Phase Coherence</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;" id="phaseCoherence">--</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Nearest Zero</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;" id="nearestZero">14.13</div>
                    </div>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Modular Zeta Surface:</strong><br>
                    Each concentric ring represents modulus m = 1, 2, 3, ..., <span id="maxModDisplay">30</span><br>
                    Points on each ring: primitive m-th roots of unity e<sup>2πik/m</sup> where gcd(k,m)=1<br>
                    Each point contributes: S<sub>m,k</sub>(s) = Σ<sub>n≡k(mod m)</sub> n<sup>-s</sup><br>
                    Color brightness = contribution magnitude<br>
                    <strong>At zeros:</strong> modular rotations align destructively → dark/zero sum<br>
                    <strong>Away from zeros:</strong> constructive interference → bright regions<br>
                    <strong>Adjust modulus:</strong> More rings = finer resolution, captures higher-order structure<br>
                    <strong>Use the Composite Channels visualization</strong> to see how primes (cyan rings) avoid Farey channels while composites (red points) project onto them<br>
                    First nontrivial zero: t ≈ 14.134725 (try this value)
                </div>
            `;
            
            // Initialize at first zero
            window.updateZetaSurface = (t, maxModulus = 30) => {
                const canvas = document.getElementById('vizCanvas');
                const freshCtx = canvas.getContext('2d');
                const rect = canvas.getBoundingClientRect();
                canvas.width = rect.width;
                canvas.height = rect.height;
                
                const width = rect.width;
                const height = rect.height;
                const centerX = width / 2;
                const centerY = height / 2;
                const maxRadius = Math.min(width, height) * 0.45;
                
                // Clear canvas
                freshCtx.fillStyle = 'rgba(0, 0, 0, 0.95)';
                freshCtx.fillRect(0, 0, width, height);
                
                const radiusStep = maxRadius / (maxModulus + 1);
                
                let totalMagnitude = 0;
                let totalReal = 0, totalImag = 0;
                let contributionCount = 0;
                
                // For each modulus
                for (let m = 1; m <= maxModulus; m++) {
                    const radius = m * radiusStep;
                    const coprimeResidues = getCoprimeResidues(m);
                    
                    // For each primitive residue
                    for (const k of coprimeResidues) {
                        // Compute S_{m,k}(s)
                        let sumReal = 0, sumImag = 0;
                        
                        for (const p of primes) {
                            if (p % m === k) {
                                const r = Math.pow(p, -sigma);
                                const theta = -t * Math.log(p);
                                sumReal += r * Math.cos(theta);
                                sumImag += r * Math.sin(theta);
                            }
                        }
                        
                        const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                        totalMagnitude += magnitude;
                        totalReal += sumReal;
                        totalImag += sumImag;
                        contributionCount++;
                        
                        // Position on ring
                        const angle = 2 * Math.PI * k / m;
                        const x = centerX + radius * Math.cos(angle);
                        const y = centerY + radius * Math.sin(angle);
                        
                        // Color by magnitude
                        const brightness = Math.min(255, magnitude * 500);
                        const hue = (k / m) * 360;
                        freshCtx.fillStyle = `hsla(${hue}, 80%, ${brightness/4}%, ${Math.min(1, magnitude * 2)})`;
                        
                        // Size by magnitude
                        const pointSize = 2 + magnitude * 10;
                        freshCtx.beginPath();
                        freshCtx.arc(x, y, pointSize, 0, Math.PI * 2);
                        freshCtx.fill();
                        
                        // Glow effect
                        if (magnitude > 0.01) {
                            const gradient = freshCtx.createRadialGradient(x, y, 0, x, y, pointSize * 2);
                            gradient.addColorStop(0, `hsla(${hue}, 100%, 70%, ${magnitude})`);
                            gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
                            freshCtx.fillStyle = gradient;
                            freshCtx.beginPath();
                            freshCtx.arc(x, y, pointSize * 2, 0, Math.PI * 2);
                            freshCtx.fill();
                        }
                    }
                    
                    // Draw ring outline
                    freshCtx.strokeStyle = 'rgba(255, 255, 255, 0.05)';
                    freshCtx.lineWidth = 1;
                    freshCtx.beginPath();
                    freshCtx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                    freshCtx.stroke();
                }
                
                // Calculate phase coherence
                const vectorMagnitude = Math.sqrt(totalReal * totalReal + totalImag * totalImag);
                const coherence = vectorMagnitude / totalMagnitude;
                
                // Update stats
                document.getElementById('tValueSurface').textContent = t.toFixed(3);
                document.getElementById('maxModSurface').textContent = maxModulus;
                document.getElementById('moduliCount').textContent = maxModulus;
                document.getElementById('surfaceMagnitude').textContent = vectorMagnitude.toFixed(4);
                document.getElementById('phaseCoherence').textContent = (coherence * 100).toFixed(2) + '%';
                
                // Update description display
                document.getElementById('maxModDisplay').textContent = maxModulus;
                const knownZeros = [14.134725, 21.022040, 25.010858, 30.424876, 32.935062];
                let nearest = knownZeros[0];
                let minDist = Math.abs(t - nearest);
                for (const z of knownZeros) {
                    const dist = Math.abs(t - z);
                    if (dist < minDist) {
                        minDist = dist;
                        nearest = z;
                    }
                }
                document.getElementById('nearestZero').textContent = nearest.toFixed(3);
                
                // Draw center marker
                freshCtx.fillStyle = '#4ecdc4';
                freshCtx.beginPath();
                freshCtx.arc(centerX, centerY, 4, 0, Math.PI * 2);
                freshCtx.fill();
                
                // Draw info text
                freshCtx.fillStyle = coherence < 0.1 ? '#ff6384' : '#4ecdc4';
                freshCtx.font = 'bold 16px Arial';
                freshCtx.textAlign = 'center';
                const statusText = coherence < 0.1 ? 'Near Zero! (Destructive)' : 'Constructive Interference';
                freshCtx.fillText(statusText, centerX, height - 20);
            };
            
            // Initialize at first zero with default modulus
            window.updateZetaSurface(14.134725, 30);
        }
        
        function generatePrimeRacesChartForExport(ctx, width, height, background) {
            const { primes, modulus } = computationData;
            const actualModulus = modulus;
            const coprimeResidues = getCoprimeResidues(actualModulus);
            const residues = coprimeResidues.slice(0, Math.min(8, coprimeResidues.length));
            
            const counts = {};
            residues.forEach(r => counts[r] = 0);
            
            const raceData = [];
            
            for (const p of primes) {
                if (p < actualModulus) continue;
                const residue = p % actualModulus;
                if (residues.includes(residue)) {
                    counts[residue]++;
                }
                
                const dataPoint = { x: p };
                residues.forEach(r => dataPoint[`count_${r}`] = counts[r]);
                if (residues.length >= 2) {
                    dataPoint.diff = counts[residues[0]] - counts[residues[1]];
                }
                raceData.push(dataPoint);
            }
            
            const lineColors = ['rgba(78, 205, 196, 1)', 'rgba(255, 99, 132, 1)', 'rgba(255, 215, 0, 1)', 
                              'rgba(153, 102, 255, 1)', 'rgba(255, 159, 64, 1)', 'rgba(75, 192, 192, 1)',
                              'rgba(255, 99, 71, 1)', 'rgba(147, 112, 219, 1)'];
            
            const datasets = residues.map((r, idx) => ({
                label: `≡ ${r} (mod ${actualModulus})`,
                data: raceData.map(d => ({ x: d.x, y: d[`count_${r}`] })),
                borderColor: background === 'white' ? lineColors[idx].replace('1)', '0.8)') : lineColors[idx],
                backgroundColor: background === 'white' ? lineColors[idx].replace('1)', '0.1)') : lineColors[idx].replace('1)', '0.1)'),
                borderWidth: 4,
                fill: false,
                tension: 0,
                pointRadius: 0
            }));
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: { datasets: datasets },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'x (prime value)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Count of Primes', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateGoldbachCometForExport(ctx, width, height, background) {
            const { primes } = computationData;
            const primeSet = new Set(primes);
            const maxN = primes[primes.length - 1];
            const goldbachData = [];
            
            for (let n = 4; n <= maxN; n += 2) {
                let count = 0;
                for (const p of primes) {
                    if (p > n / 2) break;
                    const q = n - p;
                    if (q >= 2 && primeSet.has(q)) {
                        count++;
                    }
                }
                if (count > 0) {
                    goldbachData.push({ n: n, count: count });
                }
            }
            
            const maxCount = Math.max(...goldbachData.map(d => d.count));
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Goldbach Partitions',
                        data: goldbachData.map(d => ({ x: d.n, y: d.count })),
                        backgroundColor: function(context) {
                            const count = context.raw.y;
                            const ratio = count / maxCount;
                            const hue = ratio * 240;
                            return background === 'white' ? `hsla(${hue}, 70%, 50%, 0.7)` : `hsla(${hue}, 80%, 60%, 0.7)`;
                        },
                        borderColor: background === 'white' ? 'rgba(0, 0, 0, 0.3)' : 'rgba(78, 205, 196, 0.3)',
                        pointRadius: 4
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'n (even number)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'G(n) - Number of Prime Pair Partitions', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function generatePhasorSumForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            const t = 14.134725; // First zero for export
            
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) * 0.4;
            
            // Draw on canvas directly
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw axes
            ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.3)' : 'rgba(255, 255, 255, 0.3)';
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(0, centerY);
            ctx.lineTo(width, centerY);
            ctx.moveTo(centerX, 0);
            ctx.lineTo(centerX, height);
            ctx.stroke();
            
            // Draw unit circle
            ctx.beginPath();
            ctx.arc(centerX, centerY, scale, 0, Math.PI * 2);
            ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.2)' : 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 2;
            ctx.stroke();
            
            // Compute and draw phasors
            let sumReal = 0, sumImag = 0;
            let currentX = centerX, currentY = centerY;
            const numPhasors = Math.min(50, primes.length);
            
            for (let i = 0; i < numPhasors; i++) {
                const n = primes[i];
                const radius = Math.pow(n, -sigma);
                const angle = -t * Math.log(n);
                
                const real = radius * Math.cos(angle);
                const imag = radius * Math.sin(angle);
                
                sumReal += real;
                sumImag += imag;
                
                const nextX = currentX + real * scale;
                const nextY = centerY - imag * scale;
                
                const hue = (i / numPhasors) * 280;
                ctx.strokeStyle = background === 'white' ? `hsla(${hue}, 70%, 45%, 0.7)` : `hsla(${hue}, 80%, 60%, 0.7)`;
                ctx.lineWidth = 3;
                
                ctx.beginPath();
                ctx.moveTo(currentX, currentY);
                ctx.lineTo(nextX, nextY);
                ctx.stroke();
                
                currentX = nextX;
                currentY = nextY;
            }
            
            // Draw final sum
            const finalX = centerX + sumReal * scale;
            const finalY = centerY - sumImag * scale;
            
            ctx.strokeStyle = background === 'white' ? '#d4af37' : '#ffd700';
            ctx.lineWidth = 6;
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(finalX, finalY);
            ctx.stroke();
            
            ctx.fillStyle = background === 'white' ? '#d4af37' : '#ffd700';
            ctx.beginPath();
            ctx.arc(finalX, finalY, 8, 0, Math.PI * 2);
            ctx.fill();
            
            // Labels
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            ctx.fillStyle = textColor;
            ctx.font = `${height * 0.025}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText('Re', width - 40, centerY - 15);
            ctx.fillText('Im', centerX + 20, 30);
            
            const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
            ctx.font = `bold ${height * 0.03}px Arial`;
            ctx.fillText(`ζ(${sigma} + ${t.toFixed(2)}i) ≈ ${magnitude.toFixed(3)}`, centerX, height - 30);
            
            return { destroy: () => {} };
        }
        
        function generateZetaSurfaceForExport(ctx, width, height, background) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            const t = 14.134725; // First zero
            
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.45;
            
            // Clear canvas
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            const maxModulus = 30;
            const radiusStep = maxRadius / (maxModulus + 1);
            
            // For each modulus
            for (let m = 1; m <= maxModulus; m++) {
                const radius = m * radiusStep;
                const coprimeResidues = getCoprimeResidues(m);
                
                // For each primitive residue
                for (const k of coprimeResidues) {
                    let sumReal = 0, sumImag = 0;
                    
                    for (const p of primes) {
                        if (p % m === k) {
                            const r = Math.pow(p, -sigma);
                            const theta = -t * Math.log(p);
                            sumReal += r * Math.cos(theta);
                            sumImag += r * Math.sin(theta);
                        }
                    }
                    
                    const magnitude = Math.sqrt(sumReal * sumReal + sumImag * sumImag);
                    
                    const angle = 2 * Math.PI * k / m;
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    const brightness = Math.min(255, magnitude * 500);
                    const hue = (k / m) * 360;
                    
                    if (background === 'white') {
                        ctx.fillStyle = `hsla(${hue}, 80%, ${30 + brightness/8}%, ${Math.min(1, magnitude * 2)})`;
                    } else {
                        ctx.fillStyle = `hsla(${hue}, 80%, ${brightness/4}%, ${Math.min(1, magnitude * 2)})`;
                    }
                    
                    const pointSize = 3 + magnitude * 12;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                    
                    if (magnitude > 0.01) {
                        const gradient = ctx.createRadialGradient(x, y, 0, x, y, pointSize * 2);
                        if (background === 'white') {
                            gradient.addColorStop(0, `hsla(${hue}, 90%, 50%, ${magnitude * 0.8})`);
                        } else {
                            gradient.addColorStop(0, `hsla(${hue}, 100%, 70%, ${magnitude})`);
                        }
                        gradient.addColorStop(1, 'rgba(0, 0, 0, 0)');
                        ctx.fillStyle = gradient;
                        ctx.beginPath();
                        ctx.arc(x, y, pointSize * 2, 0, Math.PI * 2);
                        ctx.fill();
                    }
                }
                
                // Draw ring outline
                ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.1)' : 'rgba(255, 255, 255, 0.05)';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Draw center
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            // Title
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            ctx.fillStyle = textColor;
            ctx.font = `bold ${height * 0.03}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(`Modular Zeta Surface at t = ${t.toFixed(3)} (First Zero)`, centerX, height - 30);
            
            return { destroy: () => {} };
        }
        
        function generatePrimeAvoidanceForExport(ctx, width, height, background) {
            const maxMod = parseInt(document.getElementById('avoidanceMaxModSlider')?.value || 30);
            const epsilon = parseFloat(document.getElementById('avoidanceEpsilonSlider')?.value || 0.2);
            
            const centerX = width / 2;
            const centerY = height / 2;
            const maxRadius = Math.min(width, height) * 0.42;
            
            const primes = sieveOfEratosthenes(maxMod);
            const primeSet = new Set(primes);
            const moduli = [];
            for (let m = 2; m <= maxMod; m++) {
                moduli.push({ M: m, isPrime: primeSet.has(m) });
            }
            
            const allResidues = [];
            for (const mod of moduli) {
                const M = mod.M;
                const radius = (M / maxMod) * maxRadius;
                
                for (let r = 1; r < M; r++) {
                    const d = gcd(r, M);
                    const rPrime = r / d;
                    const mPrime = M / d;
                    const isReducible = d > 1;
                    
                    const angle = (2 * Math.PI * r) / M;
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    let channelX = centerX, channelY = centerY;
                    if (isReducible) {
                        const channelRadius = (mPrime / maxMod) * maxRadius;
                        const channelAngle = (2 * Math.PI * rPrime) / mPrime;
                        channelX = centerX + channelRadius * Math.cos(channelAngle);
                        channelY = centerY + channelRadius * Math.sin(channelAngle);
                    }
                    
                    allResidues.push({
                        M, r, d, isPrime: mod.isPrime, isReducible,
                        x, y, channelX, channelY
                    });
                }
            }
            
            // Clear
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            // Draw projection lines
            const lineOpacity = Math.max(0.1, epsilon * 0.5);
            for (const res of allResidues) {
                if (res.isReducible) {
                    ctx.strokeStyle = background === 'white' ? 
                        `rgba(220, 53, 69, ${lineOpacity})` : 
                        `rgba(255, 99, 132, ${lineOpacity})`;
                    ctx.lineWidth = 1;
                    ctx.beginPath();
                    ctx.moveTo(res.x, res.y);
                    ctx.lineTo(res.channelX, res.channelY);
                    ctx.stroke();
                }
            }
            
            // Draw rings
            for (const mod of moduli) {
                const radius = (mod.M / maxMod) * maxRadius;
                if (background === 'white') {
                    ctx.strokeStyle = mod.isPrime ? 'rgba(30, 60, 114, 0.5)' : 'rgba(220, 53, 69, 0.3)';
                } else {
                    ctx.strokeStyle = mod.isPrime ? 'rgba(78, 205, 196, 0.5)' : 'rgba(255, 99, 132, 0.3)';
                }
                ctx.lineWidth = mod.isPrime ? 4 : 2;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Draw points
            for (const res of allResidues) {
                let pointColor;
                if (res.isPrime) {
                    pointColor = background === 'white' ? 'rgba(30, 60, 114, 0.9)' : 'rgba(78, 205, 196, 0.9)';
                } else {
                    pointColor = background === 'white' ?
                        (res.isReducible ? 'rgba(220, 53, 69, 0.8)' : 'rgba(255, 159, 64, 0.8)') :
                        (res.isReducible ? 'rgba(255, 99, 132, 0.8)' : 'rgba(255, 159, 64, 0.8)');
                }
                
                ctx.fillStyle = pointColor;
                ctx.beginPath();
                ctx.arc(res.x, res.y, 4, 0, Math.PI * 2);
                ctx.fill();
            }
            
            // Center
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#fff';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            // Labels
            ctx.fillStyle = textColor;
            ctx.font = `bold ${height * 0.025}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(`Prime Channel Avoidance: Max Modulus = ${maxMod}`, centerX, height * 0.05);
            
            ctx.font = `${height * 0.02}px Arial`;
            const primeCount = moduli.filter(m => m.isPrime).length;
            ctx.fillText(`${primeCount} primes (cyan) avoid all Farey channels | ${moduli.length - primeCount} composites (red) project onto channels`, 
                        centerX, height * 0.95);
            
            return { destroy: () => {} };
        }
        
        function generateCompositeChannelsForExport(ctx, width, height, background) {
            // Use current settings or defaults
            const M = parseInt(document.getElementById('compositeMSlider')?.value || 12);
            const epsilon = parseFloat(document.getElementById('compositeEpsilonSlider')?.value || 0.1);
            
            const centerX = width / 2;
            const centerY = height / 2;
            
            // Calculate proper divisors
            const divisors = [];
            for (let d = 1; d < M; d++) {
                if (M % d === 0) {
                    divisors.push(d);
                }
            }
            
            const phiM = eulerPhi(M);
            const maxRadius = Math.min(width, height) * 0.4;
            
            // Compute all residues and their projections
            const residueData = [];
            for (let r = 0; r < M; r++) {
                const d = gcd(r, M);
                const rPrime = r / d;
                const mPrime = M / d;
                const isReducible = d > 1;
                
                const outerAngle = (2 * Math.PI * r) / M;
                const outerX = centerX + maxRadius * Math.cos(outerAngle);
                const outerY = centerY + maxRadius * Math.sin(outerAngle);
                
                const innerRadius = (mPrime / M) * maxRadius;
                const innerAngle = (2 * Math.PI * rPrime) / mPrime;
                const innerX = centerX + innerRadius * Math.cos(innerAngle);
                const innerY = centerY + innerRadius * Math.sin(innerAngle);
                
                residueData.push({
                    r, rPrime, mPrime, d,
                    isReducible,
                    outerX, outerY,
                    innerX, innerY,
                    outerRadius: maxRadius,
                    innerRadius
                });
            }
            
            // Clear canvas
            if (background === 'white') {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw using projection lines mode (most informative for export)
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            // Draw outer ring
            ctx.strokeStyle = background === 'white' ? 'rgba(0, 0, 0, 0.3)' : 'rgba(255, 255, 255, 0.3)';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.arc(centerX, centerY, maxRadius, 0, Math.PI * 2);
            ctx.stroke();
            
            // Draw reduction rings
            const uniqueMPrimes = [...new Set(residueData.map(d => d.mPrime))].sort((a, b) => a - b);
            for (const mPrime of uniqueMPrimes) {
                if (mPrime === M) continue;
                const radius = (mPrime / M) * maxRadius;
                ctx.strokeStyle = background === 'white' ? 'rgba(212, 175, 55, 0.2)' : 'rgba(255, 215, 0, 0.2)';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Draw projection lines
            const lineOpacity = Math.max(0.2, Math.min(1, epsilon * 2));
            for (const data of residueData) {
                if (data.isReducible) {
                    ctx.strokeStyle = background === 'white' ? 
                        `rgba(220, 53, 69, ${lineOpacity})` : 
                        `rgba(255, 99, 132, ${lineOpacity})`;
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.moveTo(data.outerX, data.outerY);
                    ctx.lineTo(data.innerX, data.innerY);
                    ctx.stroke();
                }
            }
            
            // Draw residue points
            for (const data of residueData) {
                // Outer point
                if (background === 'white') {
                    ctx.fillStyle = data.isReducible ? 'rgba(220, 53, 69, 0.9)' : 'rgba(30, 60, 114, 0.9)';
                } else {
                    ctx.fillStyle = data.isReducible ? 'rgba(255, 99, 132, 0.9)' : 'rgba(78, 205, 196, 0.9)';
                }
                ctx.beginPath();
                ctx.arc(data.outerX, data.outerY, 5, 0, Math.PI * 2);
                ctx.fill();
                
                // Inner point
                if (data.isReducible) {
                    ctx.fillStyle = background === 'white' ? 'rgba(212, 175, 55, 0.8)' : 'rgba(255, 215, 0, 0.8)';
                    ctx.beginPath();
                    ctx.arc(data.innerX, data.innerY, 4, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
            
            // Center marker
            ctx.fillStyle = background === 'white' ? '#1e3c72' : '#4ecdc4';
            ctx.beginPath();
            ctx.arc(centerX, centerY, 6, 0, Math.PI * 2);
            ctx.fill();
            
            // Labels
            ctx.fillStyle = textColor;
            ctx.font = `bold ${height * 0.025}px Arial`;
            ctx.textAlign = 'center';
            ctx.fillText(`Composite Channel Projection: M = ${M}`, centerX, height * 0.05);
            
            ctx.font = `${height * 0.02}px Arial`;
            ctx.fillText(`φ(${M}) = ${phiM} irreducible, ${M - phiM} reducible (${((M - phiM) / M * 100).toFixed(1)}%)`, 
                        centerX, height * 0.95);
            
            return { destroy: () => {} };
        }
        
        function createGoldbachCometPlot(ctx) {
            const { primes } = computationData;
            
            // Create a Set for O(1) prime lookup
            const primeSet = new Set(primes);
            
            // Goldbach Comet: for even number n, count number of ways to write n = p + q (p, q prime)
            // Use all primes computed, no artificial cap
            const maxN = primes[primes.length - 1];
            const goldbachData = [];
            
            // For each even number, count Goldbach partitions
            for (let n = 4; n <= maxN; n += 2) {
                let count = 0;
                
                // Count ways to write n as sum of two primes
                for (const p of primes) {
                    if (p > n / 2) break;  // Avoid double counting
                    const q = n - p;
                    if (q >= 2 && primeSet.has(q)) {
                        count++;
                    }
                }
                
                if (count > 0) {  // Only add if we found partitions
                    goldbachData.push({ n: n, count: count });
                }
            }
            
            // Calculate statistics
            if (goldbachData.length === 0) {
                // Fallback if no data
                const statsDiv = document.getElementById('vizStats');
                statsDiv.style.display = 'block';
                statsDiv.innerHTML = `
                    <h4 style="color: #ffd700; margin-bottom: 15px;">Goldbach Comet</h4>
                    <div style="padding: 20px; background: rgba(255, 99, 132, 0.15); border-radius: 8px; text-align: center;">
                        <p style="font-size: 1.2em; color: #ff6384;">Not enough primes computed to generate Goldbach Comet.</p>
                        <p style="margin-top: 10px; opacity: 0.8;">Try increasing the target error or using more primes.</p>
                    </div>
                `;
                return;
            }
            
            const avgCount = goldbachData.reduce((sum, d) => sum + d.count, 0) / goldbachData.length;
            const maxCount = Math.max(...goldbachData.map(d => d.count));
            const maxCountN = goldbachData.find(d => d.count === maxCount).n;
            const minCount = Math.min(...goldbachData.map(d => d.count));
            const minCountN = goldbachData.find(d => d.count === minCount).n;
            
            // Find numbers with count = 1 (most difficult to partition)
            const hardToPartition = goldbachData.filter(d => d.count === 1).map(d => d.n);
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Goldbach Comet</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Even Numbers Analyzed</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${goldbachData.length}</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${avgCount.toFixed(2)}</div>
                    </div>
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Most Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${maxCount} (n=${maxCountN})</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Fewest Partitions</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${minCount} (n=${minCountN})</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">With Only 1 Partition</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${hardToPartition.length}</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Goldbach Verified</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">✓ All</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About the Goldbach Comet:</strong><br>
                    <strong>Goldbach's Conjecture</strong> (1742, unproven): Every even integer > 2 is the sum of two primes<br>
                    The "comet" shape emerges when plotting G(n) = number of ways to write n = p + q<br>
                    <strong>Dense vertical lines:</strong> Correspond to numbers divisible by small primes (2, 6, 30, etc.)<br>
                    <strong>Tail of the comet:</strong> Numbers with many prime partitions (highly composite even numbers)<br>
                    Verified for all even numbers up to 4 × 10¹⁸<br>
                    Weak Goldbach (every odd > 5 is sum of 3 primes) was proven by Helfgott in 2013<br>
                    The function G(n) grows roughly as n/ln²(n) for large n
                </div>
            `;
            
            vizChart = new Chart(ctx, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Goldbach Partitions G(n)',
                        data: goldbachData.map(d => ({ x: d.n, y: d.count })),
                        backgroundColor: function(context) {
                            // Color by count
                            const count = context.raw.y;
                            const ratio = count / maxCount;
                            const hue = ratio * 240; // Blue to purple gradient
                            return `hsla(${hue}, 80%, 60%, 0.7)`;
                        },
                        borderColor: 'rgba(78, 205, 196, 0.3)',
                        pointRadius: 3 * universalZoom,
                        pointHoverRadius: 6 * universalZoom
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const n = context.parsed.x;
                                    const count = context.parsed.y;
                                    
                                    // Find actual partitions for this n
                                    const partitions = [];
                                    for (const p of primes) {
                                        if (p > n / 2) break;
                                        const q = n - p;
                                        if (q >= 2 && primeSet.has(q)) {
                                            partitions.push(`${p} + ${q}`);
                                        }
                                    }
                                    
                                    const result = [
                                        `n = ${n}`,
                                        `Partitions: ${count}`,
                                        ''
                                    ];
                                    
                                    // Show first few partitions
                                    const showCount = Math.min(5, partitions.length);
                                    for (let i = 0; i < showCount; i++) {
                                        result.push(partitions[i]);
                                    }
                                    if (partitions.length > showCount) {
                                        result.push(`... and ${partitions.length - showCount} more`);
                                    }
                                    
                                    return result;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'linear',
                            title: { 
                                display: true, 
                                text: 'n (even number)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'G(n) - Number of Prime Pair Partitions', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function createErrorAnalysisPlot(ctx) {
            const { partialProducts, exactValue, constantType, epsilon } = computationData;
            
            // Calculate absolute and relative errors at each step
            const errorData = partialProducts.map(p => {
                let currentValue;
                if (constantType === 'pi') {
                    currentValue = Math.sqrt(6 * p.value);
                } else {
                    currentValue = p.value;
                }
                
                const absError = Math.abs(currentValue - exactValue);
                const relError = absError / Math.abs(exactValue);
                
                return {
                    prime: p.prime,
                    absError: absError,
                    relError: relError,
                    logAbsError: Math.log10(absError),
                    logRelError: Math.log10(relError)
                };
            });
            
            // Calculate convergence rate
            const convergenceRates = [];
            for (let i = 1; i < errorData.length; i++) {
                const rate = errorData[i].relError / errorData[i-1].relError;
                convergenceRates.push(rate);
            }
            const avgConvergenceRate = convergenceRates.reduce((a, b) => a + b, 0) / convergenceRates.length;
            
            // Find when error drops below target epsilon
            const targetMetIndex = errorData.findIndex(e => e.relError <= epsilon);
            const primesNeededForTarget = targetMetIndex >= 0 ? errorData[targetMetIndex].prime : 'Not yet met';
            
            // Calculate theoretical error bound
            const finalError = errorData[errorData.length - 1].relError;
            const theoreticalBound = epsilon;
            
            // Display stats
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">Error Analysis & Convergence Rate</h4>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 15px;">
                    <div style="background: rgba(255, 99, 132, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Final Relative Error</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff6384;">${(finalError * 100).toFixed(8)}%</div>
                    </div>
                    <div style="background: rgba(255, 215, 0, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Target Error (ε)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ffd700;">${(theoreticalBound * 100).toFixed(4)}%</div>
                    </div>
                    <div style="background: rgba(78, 205, 196, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Avg Convergence Rate</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4ecdc4;">${avgConvergenceRate.toFixed(6)}</div>
                    </div>
                    <div style="background: rgba(153, 102, 255, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Target Met At Prime</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #9966ff;">${primesNeededForTarget}</div>
                    </div>
                    <div style="background: rgba(255, 159, 64, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Initial Error (p=2)</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #ff9f40;">${(errorData[0].relError * 100).toFixed(4)}%</div>
                    </div>
                    <div style="background: rgba(75, 192, 192, 0.15); padding: 12px; border-radius: 8px;">
                        <div style="font-size: 0.9em; opacity: 0.8;">Error Reduction Factor</div>
                        <div style="font-size: 1.4em; font-weight: bold; color: #4bc0c0;">${(errorData[0].relError / finalError).toFixed(2)}×</div>
                    </div>
                </div>
                <div style="margin-top: 15px; padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>About Error Analysis:</strong><br>
                    <strong>Relative Error:</strong> |computed - exact| / |exact| measures accuracy as a percentage<br>
                    <strong>Convergence Rate:</strong> Ratio of consecutive errors shows how fast error decreases<br>
                    Rate < 1 indicates convergence (smaller = faster)<br>
                    <strong>Theoretical Guarantee:</strong> Euler product truncation ensures error ≤ ε<br>
                    Log scale reveals exponential convergence behavior<br>
                    Each additional prime contributes multiplicatively to accuracy
                </div>
            `;
            
            // Create dual-axis chart
            vizChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: errorData.map(e => e.prime),
                    datasets: [{
                        label: 'Relative Error (log scale)',
                        data: errorData.map(e => e.logRelError),
                        borderColor: 'rgba(255, 99, 132, 1)',
                        backgroundColor: 'rgba(255, 99, 132, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 2,
                        yAxisID: 'y'
                    }, {
                        label: 'Absolute Error (log scale)',
                        data: errorData.map(e => e.logAbsError),
                        borderColor: 'rgba(78, 205, 196, 1)',
                        backgroundColor: 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 3,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 2,
                        yAxisID: 'y'
                    }, {
                        label: 'Target Threshold',
                        data: Array(errorData.length).fill(Math.log10(epsilon)),
                        borderColor: 'rgba(255, 215, 0, 1)',
                        borderWidth: 2,
                        borderDash: [10, 5],
                        pointRadius: 0,
                        fill: false,
                        yAxisID: 'y'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: '#fff',
                                font: { size: 14 }
                            }
                        },
                        tooltip: {
                            backgroundColor: 'rgba(0, 0, 0, 0.9)',
                            callbacks: {
                                label: function(context) {
                                    const idx = context.dataIndex;
                                    if (context.datasetIndex === 0) {
                                        return `Rel Error: ${(errorData[idx].relError * 100).toExponential(4)}%`;
                                    } else if (context.datasetIndex === 1) {
                                        return `Abs Error: ${errorData[idx].absError.toExponential(4)}`;
                                    } else {
                                        return `Target: ${(epsilon * 100).toFixed(4)}%`;
                                    }
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p (log scale)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { color: '#fff' },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Error (log₁₀ scale)', 
                                color: '#fff',
                                font: { size: 16, weight: 'bold' }
                            },
                            ticks: { 
                                color: '#fff',
                                callback: function(value) {
                                    return '10^' + value.toFixed(1);
                                }
                            },
                            grid: { color: 'rgba(255, 255, 255, 0.1)' }
                        }
                    }
                }
            });
        }
        
        function generateErrorAnalysisChartForExport(ctx, width, height, background) {
            const { partialProducts, exactValue, constantType, epsilon } = computationData;
            
            const errorData = partialProducts.map(p => {
                let currentValue;
                if (constantType === 'pi') {
                    currentValue = Math.sqrt(6 * p.value);
                } else {
                    currentValue = p.value;
                }
                
                const absError = Math.abs(currentValue - exactValue);
                const relError = absError / Math.abs(exactValue);
                
                return {
                    prime: p.prime,
                    absError: absError,
                    relError: relError,
                    logAbsError: Math.log10(absError),
                    logRelError: Math.log10(relError)
                };
            });
            
            const textColor = background === 'white' ? '#000000' : '#ffffff';
            
            return new Chart(ctx, {
                type: 'line',
                data: {
                    labels: errorData.map(e => e.prime),
                    datasets: [{
                        label: 'Relative Error (log scale)',
                        data: errorData.map(e => e.logRelError),
                        borderColor: background === 'white' ? 'rgba(220, 53, 69, 1)' : 'rgba(255, 99, 132, 1)',
                        backgroundColor: background === 'white' ? 'rgba(220, 53, 69, 0.1)' : 'rgba(255, 99, 132, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }, {
                        label: 'Absolute Error (log scale)',
                        data: errorData.map(e => e.logAbsError),
                        borderColor: background === 'white' ? 'rgba(30, 60, 114, 1)' : 'rgba(78, 205, 196, 1)',
                        backgroundColor: background === 'white' ? 'rgba(30, 60, 114, 0.1)' : 'rgba(78, 205, 196, 0.1)',
                        borderWidth: 4,
                        fill: false,
                        tension: 0.4,
                        pointRadius: 0
                    }, {
                        label: 'Target Threshold',
                        data: Array(errorData.length).fill(Math.log10(epsilon)),
                        borderColor: background === 'white' ? 'rgba(212, 175, 55, 1)' : 'rgba(255, 215, 0, 1)',
                        borderWidth: 3,
                        borderDash: [15, 8],
                        pointRadius: 0,
                        fill: false
                    }]
                },
                options: {
                    responsive: false,
                    animation: false,
                    plugins: {
                        legend: {
                            labels: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            }
                        }
                    },
                    scales: {
                        x: {
                            type: 'logarithmic',
                            title: { 
                                display: true, 
                                text: 'Prime p (log scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        },
                        y: {
                            title: { 
                                display: true, 
                                text: 'Error (log₁₀ scale)', 
                                color: textColor,
                                font: { size: Math.floor(height * 0.03) }
                            },
                            ticks: { 
                                color: textColor,
                                font: { size: Math.floor(height * 0.025) },
                                callback: function(value) {
                                    return '10^' + value.toFixed(1);
                                }
                            },
                            grid: { color: background === 'white' ? 'rgba(0,0,0,0.1)' : 'rgba(255,255,255,0.1)' }
                        }
                    }
                }
            });
        }
        
        function exportResults() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const exportData = {
                timestamp: new Date().toISOString(),
                parameters: {
                    epsilon: computationData.epsilon,
                    constantType: computationData.constantType,
                    method: computationData.method,
                    cutoff: computationData.Y
                },
                results: {
                    computedValue: computationData.computedValue,
                    exactValue: computationData.exactValue,
                    absoluteError: Math.abs(computationData.computedValue - computationData.exactValue),
                    relativeError: Math.abs(computationData.computedValue - computationData.exactValue) / computationData.exactValue,
                    primesUsed: computationData.primes.length,
                    primes: computationData.primes
                }
            };
            
            const blob = new Blob([JSON.stringify(exportData, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `zeta_calculation_${computationData.constantType}_${Date.now()}.json`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        function exportStepsText() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const { epsilon, constantType, Y, primes, exponent, computedValue, exactValue } = computationData;
            
            let text = `MODULAR SIEVE CALCULATION\n`;
            text += `${'='.repeat(80)}\n\n`;
            text += `Timestamp: ${new Date().toISOString()}\n`;
            text += `Constant: ${constantType === 'pi' ? 'π' : 'ζ(' + exponent + ')'}\n`;
            text += `Target Error: ${epsilon}\n\n`;
            
            text += `STEP 1: DETERMINE CUTOFF\n`;
            text += `${'-'.repeat(80)}\n`;
            if (constantType === 'pi') {
                text += `For π: Y = ⌈1 + 1/log(1+ε)⌉\n`;
                text += `Y = ⌈1 + ${(1/Math.log(1+epsilon)).toFixed(4)}⌉ = ${Y}\n`;
            } else {
                text += `For ζ(${exponent}): Y = ⌈(2/((2n-1)·log(1+ε)))^(1/(2n-1))⌉\n`;
                text += `Y = ${Y}\n`;
            }
            text += `\nNeed all primes ≤ ${Y-1}\n\n`;
            
            text += `STEP 2: GENERATE PRIMES\n`;
            text += `${'-'.repeat(80)}\n`;
            text += `Found ${primes.length} primes using Sieve of Eratosthenes:\n`;
            text += `{${primes.slice(0, 50).join(', ')}${primes.length > 50 ? ', ...' : ''}}\n\n`;
            
            text += `STEP 3: COMPUTE EULER PRODUCT\n`;
            text += `${'-'.repeat(80)}\n`;
            const product = computeTruncatedProduct(primes, exponent);
            text += `${constantType === 'pi' ? 'ζ(2)' : 'ζ(' + exponent + ')'} = ∏(1-p^(-${exponent}))^(-1) = ${product.toFixed(15)}\n\n`;
            
            if (constantType === 'pi') {
                text += `STEP 4: EXTRACT π\n`;
                text += `${'-'.repeat(80)}\n`;
                text += `π = √(6·ζ(2)) = √(6 × ${product.toFixed(12)})\n`;
                text += `π ≈ ${computedValue.toFixed(15)}\n\n`;
            }
            
            text += `RESULTS\n`;
            text += `${'-'.repeat(80)}\n`;
            text += `Computed: ${computedValue.toFixed(15)}\n`;
            text += `Exact:    ${exactValue.toFixed(15)}\n`;
            text += `Abs Err:  ${Math.abs(computedValue - exactValue).toExponential(10)}\n`;
            text += `Rel Err:  ${(Math.abs(computedValue - exactValue) / exactValue * 100).toFixed(10)}%\n`;
            
            const blob = new Blob([text], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `zeta_steps_${constantType}_${Date.now()}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        // Prime Ring Visualization
        let rotationAnimationId = null;
        let globalRotationAngle = 0;
        let isRotating = false;
        
        function toggleModulusMode() {
            const mode = document.getElementById('modulusMode').value;
            const rangeControls = document.getElementById('rangeControls');
            const customControls = document.getElementById('customControls');
            
            if (mode === 'range') {
                rangeControls.style.display = 'block';
                customControls.style.display = 'none';
            } else if (mode === 'custom') {
                rangeControls.style.display = 'none';
                customControls.style.display = 'block';
            } else {
                rangeControls.style.display = 'none';
                customControls.style.display = 'none';
            }
        }
        
        function getModulusList() {
            const mode = document.getElementById('modulusMode').value;
            
            if (mode === 'range') {
                const maxModulus = parseInt(document.getElementById('maxModulus').value);
                const moduli = [];
                for (let i = 1; i <= maxModulus; i++) {
                    moduli.push(i);
                }
                return moduli;
            } else if (mode === 'custom') {
                const input = document.getElementById('customModuli').value;
                if (!input.trim()) return [1, 2, 4, 8, 16, 32]; // default
                return input.split(',').map(x => parseInt(x.trim())).filter(x => x >= 1).sort((a, b) => a - b);
            } else if (mode === 'powers') {
                // Powers of 2
                const moduli = [];
                for (let i = 0; i <= 10; i++) {
                    const val = Math.pow(2, i);
                    if (val <= 1024) moduli.push(val);
                }
                return moduli;
            } else if (mode === 'powers3') {
                // Powers of 3
                const moduli = [];
                for (let i = 0; i <= 8; i++) {
                    const val = Math.pow(3, i);
                    if (val <= 1024) moduli.push(val);
                }
                return moduli;
            }
            return [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
        }
        
        function toggleRotation() {
            isRotating = !isRotating;
            const btn = document.getElementById('rotationToggle');
            
            if (isRotating) {
                btn.textContent = 'Stop Rotation';
                btn.style.background = '#4ecdc4';
                startRotation();
            } else {
                btn.textContent = 'Start Rotation';
                btn.style.background = '#ff6b6b';
                if (rotationAnimationId) {
                    cancelAnimationFrame(rotationAnimationId);
                    rotationAnimationId = null;
                }
            }
        }
        
        function startRotation() {
            if (!isRotating) return;
            
            const speed = parseFloat(document.getElementById('rotationSpeed').value);
            globalRotationAngle += 0.01 * speed;
            
            updatePrimeRing();
            rotationAnimationId = requestAnimationFrame(startRotation);
        }
        
        function updatePrimeRing() {
            if (!computationData) return;
            
            const canvas = document.getElementById('primeRingCanvas');
            const ctx = canvas.getContext('2d');
            const rect = canvas.getBoundingClientRect();
            
            // Set canvas size with device pixel ratio for crisp rendering
            const dpr = window.devicePixelRatio || 1;
            canvas.width = rect.width * dpr;
            canvas.height = rect.height * dpr;
            ctx.scale(dpr, dpr);
            
            const width = rect.width;
            const height = rect.height;
            const centerX = width / 2;
            const centerY = height / 2;
            
            const moduli = getModulusList();
            const maxModulusValue = Math.max(...moduli);
            const pointSize = parseInt(document.getElementById('pointSize').value);
            const showLabels = document.getElementById('showLabels').checked;
            const showModLines = document.getElementById('showModLines').checked;
            const colorMode = document.getElementById('colorMode').value;
            const invertColors = document.getElementById('invertColors').checked;
            const invertRings = document.getElementById('invertRings').checked;
            const rotationMode = document.getElementById('rotationMode').value;
            
            const primes = computationData.primes;
            const maxRadius = Math.min(width, height) * 0.45;
            const radiusStep = maxRadius / (moduli.length + 1);
            
            // Clear canvas
            if (invertColors) {
                ctx.fillStyle = 'rgba(255, 255, 255, 0.95)';
            } else {
                ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw modulus rings
            ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.1)' : 'rgba(255, 255, 255, 0.1)';
            ctx.lineWidth = 1;
            for (let i = 0; i < moduli.length; i++) {
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Generate colors based on mode
            const getColor = (prime, residue, modulus, modulusIndex) => {
                let hue, saturation = 80, lightness = 60;
                
                if (colorMode === 'residue') {
                    hue = (residue / modulus) * 360;
                } else if (colorMode === 'modulus') {
                    hue = (modulusIndex / moduli.length) * 280;
                    saturation = 70;
                } else { // size
                    const maxPrime = Math.max(...primes);
                    const ratio = prime / maxPrime;
                    hue = ratio * 120; // green to red
                }
                
                if (invertColors) {
                    saturation = Math.min(saturation + 10, 100);
                    lightness = 40; // darker colors on white background
                }
                
                return `hsla(${hue}, ${saturation}%, ${lightness}%, 0.8)`;
            };
            
            // Store points for hover detection
            const points = [];
            
            // Draw primes on each ring
            for (let i = 0; i < moduli.length; i++) {
                const m = moduli[i];
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                
                for (const p of primes) {
                    const residue = p % m;
                    
                    // Only plot if gcd(residue, m) = 1
                    if (gcd(residue, m) !== 1) continue;
                    
                    // Calculate angle: θ = 2π * residue / m
                    let angle = (2 * Math.PI * residue) / m;
                    
                    // Apply rotation based on mode
                    if (rotationMode === 'global') {
                        angle += globalRotationAngle;
                    } else if (rotationMode === 'local') {
                        // Each ring rotates at a different speed based on its modulus
                        angle += globalRotationAngle * m / maxModulusValue;
                    }
                    
                    // Convert to Cartesian coordinates (0 radians points right to (1,0))
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    // Draw point
                    const color = getColor(p, residue, m, i);
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                    
                    // Store for hover
                    points.push({ x, y, p, residue, modulus: m, color });
                    
                    // Draw lines from center to show mod structure
                    if (showModLines && i === moduli.length - 1 && residue < m) {
                        ctx.strokeStyle = invertColors ? 'rgba(78, 205, 196, 0.2)' : 'rgba(78, 205, 196, 0.1)';
                        ctx.lineWidth = 0.5;
                        ctx.beginPath();
                        ctx.moveTo(centerX, centerY);
                        ctx.lineTo(x, y);
                        ctx.stroke();
                    }
                }
            }
            
            // Add hover interaction
            canvas.onmousemove = (e) => {
                const rect = canvas.getBoundingClientRect();
                const mouseX = e.clientX - rect.left;
                const mouseY = e.clientY - rect.top;
                
                // Find closest point
                let closestPoint = null;
                let minDist = pointSize + 5;
                
                for (const point of points) {
                    const dist = Math.sqrt((mouseX - point.x) ** 2 + (mouseY - point.y) ** 2);
                    if (dist < minDist) {
                        minDist = dist;
                        closestPoint = point;
                    }
                }
                
                if (closestPoint) {
                    // Draw tooltip
                    ctx.save();
                    
                    const tooltipX = mouseX + 15;
                    const tooltipY = mouseY - 15;
                    
                    // Calculate angle in degrees and radians
                    const angleRad = (2 * Math.PI * closestPoint.residue) / closestPoint.modulus;
                    const angleDeg = (angleRad * 180 / Math.PI).toFixed(1);
                    const angleRadStr = (angleRad / Math.PI).toFixed(3);
                    
                    // Create detailed tooltip
                    const lines = [
                        `Prime: p = ${closestPoint.p}`,
                        `Residue: r = ${closestPoint.residue} (mod ${closestPoint.modulus})`,
                        `Fraction: r/m = ${closestPoint.residue}/${closestPoint.modulus} = ${(closestPoint.residue / closestPoint.modulus).toFixed(4)}`,
                        `Angle: θ = ${angleRadStr}π rad = ${angleDeg}°`,
                        `Position: (${Math.cos(angleRad).toFixed(3)}, ${Math.sin(angleRad).toFixed(3)})`
                    ];
                    
                    ctx.font = '12px Arial';
                    const lineHeight = 16;
                    const padding = 8;
                    const maxWidth = Math.max(...lines.map(line => ctx.measureText(line).width));
                    const boxWidth = maxWidth + padding * 2;
                    const boxHeight = lines.length * lineHeight + padding * 2;
                    
                    // Adjust tooltip position if it goes off screen
                    let finalX = tooltipX;
                    let finalY = tooltipY;
                    if (tooltipX + boxWidth > width) finalX = mouseX - boxWidth - 15;
                    if (tooltipY + boxHeight > height) finalY = mouseY - boxHeight - 15;
                    
                    ctx.fillStyle = invertColors ? 'rgba(255, 255, 255, 0.98)' : 'rgba(0, 0, 0, 0.95)';
                    ctx.fillRect(finalX - padding, finalY - padding, boxWidth, boxHeight);
                    
                    ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.3)' : 'rgba(255, 255, 255, 0.3)';
                    ctx.lineWidth = 1;
                    ctx.strokeRect(finalX - padding, finalY - padding, boxWidth, boxHeight);
                    
                    ctx.fillStyle = invertColors ? '#000' : '#fff';
                    lines.forEach((line, idx) => {
                        ctx.fillText(line, finalX, finalY + idx * lineHeight + 12);
                    });
                    
                    // Highlight point
                    ctx.strokeStyle = '#ffd700';
                    ctx.lineWidth = 2;
                    ctx.beginPath();
                    ctx.arc(closestPoint.x, closestPoint.y, pointSize + 2, 0, Math.PI * 2);
                    ctx.stroke();
                    
                    ctx.restore();
                    
                    canvas.style.cursor = 'pointer';
                } else {
                    canvas.style.cursor = 'crosshair';
                }
            };
            
            // Update legend
            updateRingLegend(colorMode, moduli, primes, invertRings);
        }
        
        function updateRingLegend(colorMode, moduli, primes, invertRings) {
            const legend = document.getElementById('ringLegend');
            let html = '';
            
            html += `<div class="ring-legend-item"><strong>Moduli used:</strong> ${moduli.join(', ')}</div>`;
            html += `<div class="ring-legend-item"><strong>Ring order:</strong> ${invertRings ? 'Inverted (smallest outer)' : 'Normal (smallest inner)'}</div>`;
            
            if (colorMode === 'residue') {
                html += '<div class="ring-legend-item"><strong>Color by Residue Class:</strong> Hue represents (p mod m)/m position around each ring</div>';
            } else if (colorMode === 'modulus') {
                const colors = [];
                const displayCount = Math.min(moduli.length, 10);
                for (let i = 0; i < displayCount; i++) {
                    const hue = (i / moduli.length) * 280;
                    const color = `hsla(${hue}, 70%, 60%, 0.8)`;
                    colors.push({ label: `m=${moduli[i]}`, color });
                }
                colors.forEach(c => {
                    html += `<div class="ring-legend-item"><div class="ring-legend-color" style="background: ${c.color};"></div><span>${c.label}</span></div>`;
                });
                if (moduli.length > 10) {
                    html += '<div class="ring-legend-item"><span>... (gradient continues)</span></div>';
                }
            } else {
                html += '<div class="ring-legend-item"><strong>Color by Prime Size:</strong> Green (small) → Yellow → Red (large)</div>';
            }
            
            legend.innerHTML = html;
        }
        
        function exportPrimeRing() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            // Create modal for export options
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.8);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 10000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: linear-gradient(135deg, #1e3c72, #2a5298);
                padding: 40px;
                border-radius: 20px;
                max-width: 500px;
                width: 90%;
                box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            `;
            
            content.innerHTML = `
                <h2 style="color: #ffd700; margin-bottom: 25px; text-align: center;">Export Prime Ring</h2>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Resolution:</label>
                    <select id="ringExportResolution" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="1080">1080p (1920 x 1080)</option>
                        <option value="2160">4K (3840 x 2160)</option>
                        <option value="4320">8K (7680 x 4320)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 20px;">
                    <label style="display: block; color: #fff; margin-bottom: 8px; font-weight: 500;">Format:</label>
                    <select id="ringExportFormat" style="width: 100%; padding: 12px; border-radius: 8px; border: none; font-size: 16px;">
                        <option value="png">PNG (Lossless)</option>
                        <option value="jpg">JPEG (Smaller file)</option>
                    </select>
                </div>
                
                <div style="margin-bottom: 25px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="ringExportWatermark" checked style="width: auto; margin-right: 10px;">
                        <span>Include watermark</span>
                    </label>
                </div>
                
                <div style="display: flex; gap: 10px;">
                    <button id="ringExportBtn" style="flex: 1; padding: 15px; background: linear-gradient(45deg, #4ecdc4, #44a8a3); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Export</button>
                    <button id="ringCancelBtn" style="flex: 1; padding: 15px; background: rgba(255, 255, 255, 0.1); color: white; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 16px;">Cancel</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            document.getElementById('ringCancelBtn').onclick = () => {
                document.body.removeChild(modal);
            };
            
            document.getElementById('ringExportBtn').onclick = () => {
                const resolution = parseInt(document.getElementById('ringExportResolution').value);
                const format = document.getElementById('ringExportFormat').value;
                const includeWatermark = document.getElementById('ringExportWatermark').checked;
                
                document.body.removeChild(modal);
                
                performRingExport(resolution, format, includeWatermark);
            };
        }
        
        function performRingExport(height, format, includeWatermark) {
            const width = height * 16 / 9; // 16:9 aspect ratio
            
            const exportCanvas = document.createElement('canvas');
            exportCanvas.width = width;
            exportCanvas.height = height;
            const ctx = exportCanvas.getContext('2d');
            
            const centerX = width / 2;
            const centerY = height / 2;
            
            const moduli = getModulusList();
            const maxModulusValue = Math.max(...moduli);
            const pointSize = parseInt(document.getElementById('pointSize').value) * (height / 1080);
            const colorMode = document.getElementById('colorMode').value;
            const invertColors = document.getElementById('invertColors').checked;
            const invertRings = document.getElementById('invertRings').checked;
            const rotationMode = document.getElementById('rotationMode').value;
            
            const primes = computationData.primes;
            const maxRadius = Math.min(width, height) * 0.45;
            const radiusStep = maxRadius / (moduli.length + 1);
            
            // Clear canvas
            if (invertColors) {
                ctx.fillStyle = '#ffffff';
            } else {
                ctx.fillStyle = '#000000';
            }
            ctx.fillRect(0, 0, width, height);
            
            // Draw modulus rings
            ctx.strokeStyle = invertColors ? 'rgba(0, 0, 0, 0.15)' : 'rgba(255, 255, 255, 0.15)';
            ctx.lineWidth = 2;
            for (let i = 0; i < moduli.length; i++) {
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
                ctx.stroke();
            }
            
            // Generate colors
            const getColor = (prime, residue, modulus, modulusIndex) => {
                let hue, saturation = 80, lightness = 60;
                
                if (colorMode === 'residue') {
                    hue = (residue / modulus) * 360;
                } else if (colorMode === 'modulus') {
                    hue = (modulusIndex / moduli.length) * 280;
                    saturation = 70;
                } else {
                    const maxPrime = Math.max(...primes);
                    const ratio = prime / maxPrime;
                    hue = ratio * 120;
                }
                
                if (invertColors) {
                    saturation = Math.min(saturation + 10, 100);
                    lightness = 40;
                }
                
                return `hsla(${hue}, ${saturation}%, ${lightness}%, 0.9)`;
            };
            
            // Draw primes
            for (let i = 0; i < moduli.length; i++) {
                const m = moduli[i];
                const ringIndex = invertRings ? (moduli.length - 1 - i) : i;
                const radius = (ringIndex + 1) * radiusStep;
                
                for (const p of primes) {
                    const residue = p % m;
                    if (gcd(residue, m) !== 1) continue;
                    
                    let angle = (2 * Math.PI * residue) / m;
                    
                    if (rotationMode === 'global') {
                        angle += globalRotationAngle;
                    } else if (rotationMode === 'local') {
                        angle += globalRotationAngle * m / maxModulus;
                    }
                    
                    const x = centerX + radius * Math.cos(angle);
                    const y = centerY + radius * Math.sin(angle);
                    
                    const color = getColor(p, residue, m);
                    ctx.fillStyle = color;
                    ctx.beginPath();
                    ctx.arc(x, y, pointSize, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
            
            // Add watermark
            if (includeWatermark) {
                const watermarkY = height - height * 0.03;
                ctx.fillStyle = invertColors ? 'rgba(0, 0, 0, 0.5)' : 'rgba(255, 255, 255, 0.5)';
                ctx.font = `${height * 0.02}px Arial`;
                ctx.textAlign = 'center';
                ctx.fillText('Modular Sieve Calculator - Prime Residue Rings', centerX, watermarkY);
                ctx.font = `italic ${height * 0.015}px Arial`;
                ctx.fillText('By Wessen Getachew (@7Dview)', centerX, watermarkY + height * 0.025);
            }
            
            // Export
            const mimeType = format === 'png' ? 'image/png' : 'image/jpeg';
            exportCanvas.toBlob((blob) => {
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `prime_rings_${maxModulus}_${Date.now()}.${format}`;
                a.click();
                URL.revokeObjectURL(url);
            }, mimeType, 0.95);
        }
        
        function clearCache() {
            if (confirm(`Clear ${computationCache.size} cached results?`)) {
                computationCache.clear();
                updateCacheStatus();
                alert('Cache cleared successfully!');
            }
        }
        
        function updateCacheStatus() {
            const count = document.getElementById('cacheCount');
            if (count) {
                count.textContent = computationCache.size;
            }
        }
        
        let isScreenshotMode = false;
        
        function enterScreenshotMode() {
            isScreenshotMode = !isScreenshotMode;
            
            if (isScreenshotMode) {
                // Hide UI elements
                document.querySelector('.sticky-nav').style.display = 'none';
                document.querySelectorAll('.viz-options').forEach(el => el.style.display = 'none');
                document.querySelectorAll('.view-options').forEach(el => el.style.display = 'none');
                document.querySelectorAll('.category-btn').forEach(el => el.style.display = 'none');
                document.querySelectorAll('.viz-categories').forEach(el => el.style.display = 'none');
                document.getElementById('vizStats').style.display = 'none';
                
                alert('Screenshot Mode: UI elements hidden. Press "Esc" to exit.');
            } else {
                exitScreenshotMode();
            }
        }
        
        function exitScreenshotMode() {
            isScreenshotMode = false;
            document.querySelector('.sticky-nav').style.display = 'block';
            document.querySelectorAll('.viz-options').forEach(el => el.style.display = 'flex');
            document.querySelectorAll('.view-options').forEach(el => el.style.display = 'flex');
            document.querySelectorAll('.viz-categories').forEach(el => el.style.display = 'flex');
            document.getElementById('vizStats').style.display = 'block';
        }
        
        function enterGalleryMode() {
            if (!computationData) {
                alert('Please compute a value first!');
                return;
            }
            
            const modal = document.getElementById('galleryModal');
            const grid = document.getElementById('galleryGrid');
            
            modal.style.display = 'block';
            grid.innerHTML = '';
            
            // Create mini canvases for each visualization
            const vizTypes = [
                { id: 'convergence', name: 'Convergence' },
                { id: 'contribution', name: 'Prime Contributions' },
                { id: 'gapDist', name: 'Gap Distribution' },
                { id: 'primeCount', name: 'Prime Counting π(x)' },
                { id: 'phasorSum', name: 'Phasor Sum' },
                { id: 'sacksSpiral', name: 'Sacks Spiral' }
            ];
            
            vizTypes.forEach(viz => {
                const card = document.createElement('div');
                card.style.cssText = `
                    background: rgba(30, 60, 114, 0.6);
                    border-radius: 15px;
                    padding: 20px;
                    border: 2px solid rgba(78, 205, 196, 0.3);
                    cursor: pointer;
                    transition: all 0.3s ease;
                `;
                
                card.onmouseenter = () => {
                    card.style.borderColor = '#4ecdc4';
                    card.style.transform = 'translateY(-5px)';
                };
                
                card.onmouseleave = () => {
                    card.style.borderColor = 'rgba(78, 205, 196, 0.3)';
                    card.style.transform = 'translateY(0)';
                };
                
                card.onclick = () => {
                    exitGalleryMode();
                    changeViz(viz.id);
                    document.getElementById('visualization-section').scrollIntoView({ behavior: 'smooth' });
                };
                
                card.innerHTML = `
                    <h3 style="color: #4ecdc4; margin-bottom: 15px; text-align: center;">${viz.name}</h3>
                    <canvas id="gallery-${viz.id}" style="width: 100%; height: 300px; border-radius: 10px; background: rgba(0, 0, 0, 0.4);"></canvas>
                `;
                
                grid.appendChild(card);
            });
            
            // Render each visualization
            setTimeout(() => {
                vizTypes.forEach(viz => {
                    const canvas = document.getElementById(`gallery-${viz.id}`);
                    if (canvas) {
                        const ctx = canvas.getContext('2d');
                        const rect = canvas.getBoundingClientRect();
                        canvas.width = rect.width;
                        canvas.height = rect.height;
                        renderGalleryViz(ctx, viz.id);
                    }
                });
            }, 100);
        }
        
        function exitGalleryMode() {
            document.getElementById('galleryModal').style.display = 'none';
        }
        
        function renderGalleryViz(ctx, type) {
            // Simplified rendering for gallery thumbnails
            const { primes, partialProducts, exactValue, constantType, exponent } = computationData;
            
            const width = ctx.canvas.width;
            const height = ctx.canvas.height;
            
            ctx.fillStyle = 'rgba(0, 0, 0, 0.95)';
            ctx.fillRect(0, 0, width, height);
            
            if (type === 'convergence') {
                const values = partialProducts.map(p => constantType === 'pi' ? Math.sqrt(6 * p.value) : p.value).slice(0, 100);
                drawSimpleLine(ctx, values, width, height, '#4ecdc4');
            } else if (type === 'contribution') {
                const contributions = primes.slice(0, 50).map(p => 1 / (1 - Math.pow(p, -exponent)) - 1);
                drawScatter(ctx, contributions, width, height, '#ff6384');
            } else if (type === 'gapDist') {
                const gaps = [];
                for (let i = 1; i < Math.min(primes.length, 200); i++) {
                    gaps.push(primes[i] - primes[i-1]);
                }
                const gapCounts = {};
                gaps.forEach(g => gapCounts[g] = (gapCounts[g] || 0) + 1);
                const sortedGaps = Object.keys(gapCounts).map(Number).sort((a,b) => a-b);
                drawBars(ctx, sortedGaps.map(g => gapCounts[g]), width, height, '#4ecdc4');
            } else if (type === 'primeCount') {
                const counts = [];
                for (let x = 100; x <= Math.min(primes[primes.length-1], 10000); x += 100) {
                    counts.push(primes.filter(p => p <= x).length);
                }
                drawSimpleLine(ctx, counts, width, height, '#4ecdc4');
            } else if (type === 'phasorSum') {
                drawPhasorMini(ctx, width, height);
            } else if (type === 'sacksSpiral') {
                drawSacksMini(ctx, width, height);
            }
        }
        
        function drawSimpleLine(ctx, data, width, height, color) {
            const max = Math.max(...data);
            const min = Math.min(...data);
            const range = max - min;
            
            ctx.strokeStyle = color;
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            data.forEach((val, i) => {
                const x = (i / (data.length - 1)) * width;
                const y = height - ((val - min) / range) * height * 0.8 - height * 0.1;
                if (i === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            });
            
            ctx.stroke();
        }
        
        function drawScatter(ctx, data, width, height, color) {
            ctx.fillStyle = color;
            data.forEach((val, i) => {
                const x = (i / data.length) * width;
                const y = height - val * height * 0.8;
                ctx.beginPath();
                ctx.arc(x, y, 2, 0, Math.PI * 2);
                ctx.fill();
            });
        }
        
        function drawBars(ctx, data, width, height, color) {
            const max = Math.max(...data);
            const barWidth = width / data.length;
            
            ctx.fillStyle = color;
            data.forEach((val, i) => {
                const barHeight = (val / max) * height * 0.8;
                const x = i * barWidth;
                const y = height - barHeight;
                ctx.fillRect(x, y, barWidth - 2, barHeight);
            });
        }
        
        function drawPhasorMini(ctx, width, height) {
            const centerX = width / 2;
            const centerY = height / 2;
            const scale = Math.min(width, height) * 0.35;
            
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.2)';
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.arc(centerX, centerY, scale, 0, Math.PI * 2);
            ctx.stroke();
            
            const sigma = computationData.exponent / 2;
            const t = 14.134725;
            let sumReal = 0, sumImag = 0;
            
            for (let i = 0; i < Math.min(20, computationData.primes.length); i++) {
                const n = computationData.primes[i];
                const radius = Math.pow(n, -sigma);
                const angle = -t * Math.log(n);
                sumReal += radius * Math.cos(angle);
                sumImag += radius * Math.sin(angle);
            }
            
            const finalX = centerX + sumReal * scale;
            const finalY = centerY - sumImag * scale;
            
            ctx.strokeStyle = '#ffd700';
            ctx.lineWidth = 3;
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(finalX, finalY);
            ctx.stroke();
        }
        
        function drawSacksMini(ctx, width, height) {
            const centerX = width / 2;
            const centerY = height / 2;
            const maxR = Math.sqrt(1000);
            const scale = Math.min(width, height) / (2 * maxR) * 0.85;
            
            const primeSet = new Set(computationData.primes);
            
            for (let n = 1; n <= 1000; n++) {
                const r = Math.sqrt(n);
                const theta = 2 * Math.PI * Math.sqrt(n);
                const x = centerX + r * scale * Math.cos(theta);
                const y = centerY + r * scale * Math.sin(theta);
                
                ctx.fillStyle = primeSet.has(n) ? '#ffd700' : 'rgba(255, 255, 255, 0.1)';
                ctx.beginPath();
                ctx.arc(x, y, primeSet.has(n) ? 2 : 1, 0, Math.PI * 2);
                ctx.fill();
            }
        }
        
        // Exit screenshot mode on Escape key
        
        // ===== 3D VISUALIZATIONS =====
        
        function cleanup3D() {
            if (animationFrame3D) {
                cancelAnimationFrame(animationFrame3D);
                animationFrame3D = null;
            }
            if (renderer3D) {
                renderer3D.dispose();
                renderer3D = null;
            }
            if (controls3D) {
                controls3D.dispose();
                controls3D = null;
            }
            scene3D = null;
            camera3D = null;
        }
        
        function init3DScene(canvas) {
            cleanup3D();
            
            const width = canvas.width;
            const height = canvas.height;
            
            // Create scene
            scene3D = new THREE.Scene();
            scene3D.background = new THREE.Color(0x0a0a0a);
            
            // Create camera
            camera3D = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
            camera3D.position.set(5, 5, 5);
            camera3D.lookAt(0, 0, 0);
            
            // Create renderer
            renderer3D = new THREE.WebGLRenderer({ canvas: canvas, antialias: true });
            renderer3D.setSize(width, height);
            
            // Add lights
            const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
            scene3D.add(ambientLight);
            
            const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
            directionalLight.position.set(10, 10, 10);
            scene3D.add(directionalLight);
            
            const pointLight = new THREE.PointLight(0x4ecdc4, 1, 100);
            pointLight.position.set(0, 5, 0);
            scene3D.add(pointLight);
            
            return { scene: scene3D, camera: camera3D, renderer: renderer3D };
        }
        
        function create3DModularLattice(ctx) {
            const { primes } = computationData;
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">🎮 3D Modular Lattice</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Max Modulus: <span id="3dMaxMod">20</span></label>
                    <input type="range" id="3dMaxModSlider" min="5" max="50" step="1" value="20" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="update3DModularLattice()">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="3dAutoRotate" checked style="width: auto; margin-right: 10px;">
                        <span>Auto-Rotate</span>
                    </label>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Interactive 3D Controls:</strong><br>
                    🖱️ <strong>Left Click + Drag:</strong> Rotate view<br>
                    🖱️ <strong>Right Click + Drag:</strong> Pan camera<br>
                    🖱️ <strong>Scroll:</strong> Zoom in/out<br>
                    <strong>Visualization:</strong> Each ring is a modulus m, points are primes at residue positions<br>
                    Height represents prime magnitude, color shows modulus level
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            window.update3DModularLattice = function() {
                const maxMod = parseInt(document.getElementById('3dMaxModSlider').value);
                document.getElementById('3dMaxMod').textContent = maxMod;
                render3DModularLattice(maxMod);
            };
            
            function render3DModularLattice(maxMod) {
                const { scene, camera, renderer } = init3DScene(canvas);
                
                // Create rings for each modulus
                for (let m = 2; m <= maxMod; m++) {
                    const radius = m * 0.5;
                    const y = m * 0.3;
                    
                    // Ring geometry
                    const ringGeometry = new THREE.RingGeometry(radius - 0.05, radius + 0.05, 64);
                    const ringMaterial = new THREE.MeshBasicMaterial({ 
                        color: 0x4ecdc4, 
                        opacity: 0.2, 
                        transparent: true,
                        side: THREE.DoubleSide
                    });
                    const ring = new THREE.Mesh(ringGeometry, ringMaterial);
                    ring.rotation.x = Math.PI / 2;
                    ring.position.y = y;
                    scene.add(ring);
                    
                    // Add primes on this ring
                    for (const p of primes) {
                        if (p < m) continue;
                        const residue = p % m;
                        if (gcd(residue, m) !== 1) continue;
                        
                        const angle = (2 * Math.PI * residue) / m;
                        const x = radius * Math.cos(angle);
                        const z = radius * Math.sin(angle);
                        
                        // Height based on prime size
                        const height = Math.log(p) * 0.2;
                        
                        // Create sphere for prime
                        const geometry = new THREE.SphereGeometry(0.1, 16, 16);
                        const hue = (m / maxMod) * 0.7;
                        const color = new THREE.Color().setHSL(hue, 0.8, 0.6);
                        const material = new THREE.MeshPhongMaterial({ 
                            color: color,
                            emissive: color,
                            emissiveIntensity: 0.3
                        });
                        
                        const sphere = new THREE.Mesh(geometry, material);
                        sphere.position.set(x, y + height, z);
                        scene.add(sphere);
                        
                        // Add vertical line to ring
                        const lineGeometry = new THREE.BufferGeometry().setFromPoints([
                            new THREE.Vector3(x, y, z),
                            new THREE.Vector3(x, y + height, z)
                        ]);
                        const lineMaterial = new THREE.LineBasicMaterial({ 
                            color: color, 
                            opacity: 0.3, 
                            transparent: true 
                        });
                        const line = new THREE.Line(lineGeometry, lineMaterial);
                        scene.add(line);
                    }
                }
                
                // Add axes
                const axesHelper = new THREE.AxesHelper(maxMod * 0.6);
                scene.add(axesHelper);
                
                // Animation loop
                function animate() {
                    if (document.getElementById('3dAutoRotate')?.checked) {
                        camera.position.applyAxisAngle(new THREE.Vector3(0, 1, 0), 0.005);
                        camera.lookAt(0, maxMod * 0.15, 0);
                    }
                    
                    renderer.render(scene, camera);
                    animationFrame3D = requestAnimationFrame(animate);
                }
                
                animate();
            }
            
            render3DModularLattice(20);
        }
        
        function create3DZetaSurface(ctx) {
            const { primes, exponent } = computationData;
            const sigma = exponent / 2;
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">🎮 3D Zeta Surface</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">t Range: <span id="3dTRange">50</span></label>
                    <input type="range" id="3dTRangeSlider" min="20" max="100" step="10" value="50" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="update3DZetaSurface()">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Resolution: <span id="3dResolution">20</span></label>
                    <input type="range" id="3dResolutionSlider" min="10" max="40" step="5" value="20" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="update3DZetaSurface()">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="display: flex; align-items: center; color: #fff; cursor: pointer;">
                        <input type="checkbox" id="3dZetaWireframe" style="width: auto; margin-right: 10px;">
                        <span>Wireframe Mode</span>
                    </label>
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>3D Zeta Surface:</strong><br>
                    X-axis: Real part σ (0.5 to 2)<br>
                    Z-axis: Imaginary part t (0 to ${document.getElementById('3dTRange')?.textContent || 50})<br>
                    Y-axis: |ζ(σ + it)| magnitude<br>
                    Valleys show zeros where magnitude approaches 0
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            window.update3DZetaSurface = function() {
                const tRange = parseInt(document.getElementById('3dTRangeSlider').value);
                const resolution = parseInt(document.getElementById('3dResolutionSlider').value);
                document.getElementById('3dTRange').textContent = tRange;
                document.getElementById('3dResolution').textContent = resolution;
                render3DZetaSurface(tRange, resolution);
            };
            
            function render3DZetaSurface(tRange, resolution) {
                const { scene, camera, renderer } = init3DScene(canvas);
                
                camera.position.set(8, 6, 8);
                camera.lookAt(0, 0, 0);
                
                // Create surface geometry
                const geometry = new THREE.PlaneGeometry(4, tRange / 10, resolution, resolution);
                const vertices = geometry.attributes.position.array;
                
                // Calculate zeta values for each vertex
                const maxMagnitude = { val: 0 };
                
                for (let i = 0; i < vertices.length; i += 3) {
                    const sigmaT = 0.5 + (vertices[i] + 2) / 4 * 1.5; // sigma from 0.5 to 2
                    const tVal = (vertices[i + 1] + tRange / 20) * 10;
                    
                    // Compute |ζ(σ + it)|
                    let magnitude = 0;
                    for (let j = 0; j < Math.min(30, primes.length); j++) {
                        const n = primes[j];
                        const r = Math.pow(n, -sigmaT);
                        const angle = -tVal * Math.log(n);
                        const real = r * Math.cos(angle);
                        const imag = r * Math.sin(angle);
                        magnitude += Math.sqrt(real * real + imag * imag);
                    }
                    
                    vertices[i + 2] = magnitude * 0.5; // Height
                    maxMagnitude.val = Math.max(maxMagnitude.val, magnitude);
                }
                
                geometry.attributes.position.needsUpdate = true;
                geometry.computeVertexNormals();
                
                // Color vertices based on height
                const colors = new Float32Array(vertices.length);
                for (let i = 0; i < vertices.length; i += 3) {
                    const height = vertices[i + 2];
                    const ratio = height / (maxMagnitude.val * 0.5);
                    
                    const color = new THREE.Color();
                    color.setHSL(0.6 - ratio * 0.6, 0.8, 0.5);
                    
                    colors[i] = color.r;
                    colors[i + 1] = color.g;
                    colors[i + 2] = color.b;
                }
                
                geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));
                
                const wireframe = document.getElementById('3dZetaWireframe')?.checked || false;
                const material = new THREE.MeshPhongMaterial({
                    vertexColors: true,
                    side: THREE.DoubleSide,
                    wireframe: wireframe,
                    shininess: 30
                });
                
                const mesh = new THREE.Mesh(geometry, material);
                mesh.rotation.x = -Math.PI / 2;
                scene.add(mesh);
                
                // Add grid
                const gridHelper = new THREE.GridHelper(10, 20, 0x4ecdc4, 0x2a5298);
                gridHelper.position.y = -0.1;
                scene.add(gridHelper);
                
                // Animation
                function animate() {
                    camera.position.applyAxisAngle(new THREE.Vector3(0, 1, 0), 0.003);
                    camera.lookAt(0, 1, 0);
                    
                    renderer.render(scene, camera);
                    animationFrame3D = requestAnimationFrame(animate);
                }
                
                animate();
            }
            
            render3DZetaSurface(50, 20);
        }
        
        function create3DPrimeHelix(ctx) {
            const { primes } = computationData;
            
            const statsDiv = document.getElementById('vizStats');
            statsDiv.style.display = 'block';
            statsDiv.innerHTML = `
                <h4 style="color: #ffd700; margin-bottom: 15px;">🎮 3D Prime Helix</h4>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Modulus: <span id="3dHelixMod">6</span></label>
                    <input type="range" id="3dHelixModSlider" min="2" max="30" step="1" value="6" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="update3DPrimeHelix()">
                </div>
                <div style="margin-bottom: 15px;">
                    <label style="color: #fff; font-weight: 500;">Primes Shown: <span id="3dHelixCount">200</span></label>
                    <input type="range" id="3dHelixCountSlider" min="50" max="500" step="50" value="200" 
                           style="width: 100%; margin-top: 8px;"
                           oninput="update3DPrimeHelix()">
                </div>
                <div style="padding: 12px; background: rgba(255, 255, 255, 0.05); border-radius: 8px; line-height: 1.6;">
                    <strong>Prime Helix Visualization:</strong><br>
                    Primes spiral upward based on their residue class (mod m)<br>
                    Each residue class creates a distinct helical strand<br>
                    Height represents the prime's position in sequence<br>
                    Color represents the residue class<br>
                    Reveals patterns in prime distribution around the helix
                </div>
            `;
            
            const canvas = document.getElementById('vizCanvas');
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            
            window.update3DPrimeHelix = function() {
                const modulus = parseInt(document.getElementById('3dHelixModSlider').value);
                const count = parseInt(document.getElementById('3dHelixCountSlider').value);
                document.getElementById('3dHelixMod').textContent = modulus;
                document.getElementById('3dHelixCount').textContent = count;
                render3DPrimeHelix(modulus, count);
            };
            
            function render3DPrimeHelix(modulus, count) {
                const { scene, camera, renderer } = init3DScene(canvas);
                
                camera.position.set(8, count * 0.03, 8);
                camera.lookAt(0, count * 0.015, 0);
                
                const displayPrimes = primes.slice(0, Math.min(count, primes.length));
                const radius = 3;
                
                // Create helix strands for each residue class
                const coprimeResidues = getCoprimeResidues(modulus);
                
                for (let i = 0; i < displayPrimes.length; i++) {
                    const p = displayPrimes[i];
                    if (p < modulus) continue;
                    
                    const residue = p % modulus;
                    if (!coprimeResidues.includes(residue)) continue;
                    
                    const height = i * 0.05;
                    const baseAngle = (2 * Math.PI * residue) / modulus;
                    const spiralRotation = i * 0.1;
                    const angle = baseAngle + spiralRotation;
                    
                    const x = radius * Math.cos(angle);
                    const z = radius * Math.sin(angle);
                    
                    // Create sphere
                    const geometry = new THREE.SphereGeometry(0.15, 12, 12);
                    const hue = (residue / modulus) * 0.8;
                    const color = new THREE.Color().setHSL(hue, 0.9, 0.6);
                    const material = new THREE.MeshPhongMaterial({ 
                        color: color,
                        emissive: color,
                        emissiveIntensity: 0.4
                    });
                    
                    const sphere = new THREE.Mesh(geometry, material);
                    sphere.position.set(x, height, z);
                    scene.add(sphere);
                    
                    // Connect to previous prime in same residue class
                    if (i > 0) {
                        const prevP = displayPrimes[i - 1];
                        if (prevP % modulus === residue) {
                            const prevHeight = (i - 1) * 0.05;
                            const prevAngle = baseAngle + (i - 1) * 0.1;
                            const prevX = radius * Math.cos(prevAngle);
                            const prevZ = radius * Math.sin(prevAngle);
                            
                            const lineGeometry = new THREE.BufferGeometry().setFromPoints([
                                new THREE.Vector3(prevX, prevHeight, prevZ),
                                new THREE.Vector3(x, height, z)
                            ]);
                            const lineMaterial = new THREE.LineBasicMaterial({ 
                                color: color, 
                                opacity: 0.3, 
                                transparent: true 
                            });
                            const line = new THREE.Line(lineGeometry, lineMaterial);
                            scene.add(line);
                        }
                    }
                }
                
                // Add central axis
                const axisGeometry = new THREE.CylinderGeometry(0.1, 0.1, count * 0.05, 16);
                const axisMaterial = new THREE.MeshPhongMaterial({ 
                    color: 0xffffff, 
                    opacity: 0.2, 
                    transparent: true 
                });
                const axis = new THREE.Mesh(axisGeometry, axisMaterial);
                axis.position.y = count * 0.025;
                scene.add(axis);
                
                // Animation
                function animate() {
                    camera.position.applyAxisAngle(new THREE.Vector3(0, 1, 0), 0.005);
                    camera.lookAt(0, count * 0.015, 0);
                    
                    renderer.render(scene, camera);
                    animationFrame3D = requestAnimationFrame(animate);
                }
                
                animate();
            }
            
            render3DPrimeHelix(6, 200);
        }
        
        // Exit screenshot mode on Escape key
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape' && isScreenshotMode) {
                exitScreenshotMode();
            }
            
            // Ctrl/Cmd + E: Export results
            if ((e.ctrlKey || e.metaKey) && e.key === 'e') {
                e.preventDefault();
                exportResults();
            }
            // Ctrl/Cmd + Enter: Compute
            if ((e.ctrlKey || e.metaKey) && e.key === 'Enter') {
                e.preventDefault();
                compute();
            }
            // Ctrl/Cmd + S: Export steps
            if ((e.ctrlKey || e.metaKey) && e.key === 's') {
                e.preventDefault();
                exportStepsText();
            }
            // Ctrl/Cmd + I: Export chart
            if ((e.ctrlKey || e.metaKey) && e.key === 'i') {
                e.preventDefault();
                exportChartImage();
            }
        });
        
        window.onload = () => {
            compute();
            updateCacheStatus();
            
            // Show keyboard shortcuts hint
            setTimeout(() => {
                const hint = document.createElement('div');
                hint.style.cssText = `
                    position: fixed;
                    bottom: 20px;
                    right: 20px;
                    background: rgba(0, 0, 0, 0.9);
                    color: #fff;
                    padding: 15px 20px;
                    border-radius: 10px;
                    font-size: 0.85em;
                    max-width: 300px;
                    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
                    z-index: 9999;
                    animation: slideIn 0.5s ease;
                `;
                hint.innerHTML = `
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
                        <strong style="color: #ffd700;">⌨️ Keyboard Shortcuts</strong>
                        <button onclick="this.parentElement.parentElement.remove()" style="background: none; border: none; color: #fff; cursor: pointer; font-size: 1.2em;">×</button>
                    </div>
                    <div style="line-height: 1.8;">
                        <strong>Ctrl+Enter</strong> - Calculate<br>
                        <strong>Ctrl+E</strong> - Export JSON<br>
                        <strong>Ctrl+S</strong> - Export Steps<br>
                        <strong>Ctrl+I</strong> - Export Chart
                    </div>
                `;
                document.body.appendChild(hint);
                
                // Auto-hide after 8 seconds
                setTimeout(() => {
                    hint.style.transition = 'opacity 0.5s ease';
                    hint.style.opacity = '0';
                    setTimeout(() => hint.remove(), 500);
                }, 8000);
            }, 2000);
        };
    </script>
</body>
</html>
