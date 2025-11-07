
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Visualization Framework - Wessen Getachew</title>
    <script src="https://d3js.org/d3.v7.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --background-color: #f8f9fa;
            --card-color: #ffffff;
            --text-color: #333333;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 2rem 0;
            margin-bottom: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .header-content {
            text-align: center;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            font-weight: 300;
        }

        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            font-weight: 300;
        }

        .author {
            margin-top: 1rem;
            font-style: italic;
        }

        .control-panel {
            background: var(--card-color);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
        }

        .controls-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .control-group {
            display: flex;
            flex-direction: column;
        }

        label {
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--primary-color);
        }

        select, input, button {
            padding: 0.5rem;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }

        button {
            background-color: var(--secondary-color);
            color: white;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #2980b9;
        }

        .action-buttons {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
            flex-wrap: wrap;
        }

        .run-btn {
            background-color: #27ae60;
            padding: 0.75rem 2rem;
            font-size: 1.1rem;
            font-weight: 600;
        }

        .run-btn:hover {
            background-color: #219a52;
        }

        .reset-btn {
            background-color: #95a5a6;
            padding: 0.75rem 1.5rem;
        }

        .reset-btn:hover {
            background-color: #7f8c8d;
        }

        .export-buttons {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .export-btn {
            flex: 1;
            min-width: 120px;
            background-color: var(--primary-color);
        }

        .export-btn:hover {
            background-color: #34495e;
        }

        .visualization-area {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        @media (max-width: 768px) {
            .visualization-area {
                grid-template-columns: 1fr;
            }
        }

        .viz-container {
            background: var(--card-color);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            height: 500px;
            position: relative;
            overflow: hidden;
        }

        .viz-title {
            font-size: 1.2rem;
            margin-bottom: 1rem;
            color: var(--primary-color);
            border-bottom: 2px solid var(--secondary-color);
            padding-bottom: 0.5rem;
        }

        .viz-content {
            height: calc(100% - 3rem);
            position: relative;
        }

        .viz-canvas {
            width: 100%;
            height: 100%;
        }

        .info-panel {
            background: var(--card-color);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
        }

        .info-section {
            margin-bottom: 1.5rem;
        }

        .info-section h3 {
            color: var(--primary-color);
            margin-bottom: 0.5rem;
        }

        .math-display {
            background: #f8f9fa;
            padding: 1rem;
            border-radius: 5px;
            margin: 1rem 0;
            font-family: 'Cambria Math', serif;
            border-left: 4px solid var(--secondary-color);
        }

        .data-panel {
            background: var(--card-color);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 0.75rem;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        th {
            background-color: var(--primary-color);
            color: white;
            font-weight: 600;
        }

        tr:hover {
            background-color: #f5f5f5;
        }

        .loading {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            z-index: 100;
            background: rgba(255,255,255,0.9);
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--secondary-color);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 2s linear infinite;
            margin: 0 auto 1rem;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .status-bar {
            background: var(--card-color);
            padding: 0.75rem 1.5rem;
            border-radius: 5px;
            margin-bottom: 1rem;
            border-left: 4px solid var(--secondary-color);
            font-size: 0.9rem;
        }

        .parameter-summary {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            margin-top: 1rem;
        }

        .param-item {
            background: #f8f9fa;
            padding: 0.5rem;
            border-radius: 3px;
            text-align: center;
        }

        .param-label {
            font-size: 0.8rem;
            color: #666;
        }

        .param-value {
            font-weight: 600;
            color: var(--primary-color);
        }

        footer {
            text-align: center;
            margin-top: 2rem;
            padding: 1rem;
            color: #666;
            border-top: 1px solid #ddd;
        }

        .tooltip {
            position: absolute;
            background: rgba(0,0,0,0.8);
            color: white;
            padding: 0.5rem;
            border-radius: 3px;
            font-size: 0.9rem;
            pointer-events: none;
            z-index: 1000;
        }

        .error-message {
            background: #fee;
            color: #c33;
            padding: 1rem;
            border-radius: 5px;
            border-left: 4px solid #e74c3c;
            margin: 1rem 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-content">
                <h1>Modular Visualization Framework</h1>
                <div class="subtitle">Farey Sequences, Möbius Sums, Square-Free Density and Riemann Hypothesis</div>
                <div class="author">Wessen Getachew</div>
            </div>
        </header>

        <div class="control-panel">
            <div class="controls-grid">
                <div class="control-group">
                    <label for="modulus">Modulus (N):</label>
                    <input type="number" id="modulus" min="1" max="200" value="30">
                    <small style="color: #666; margin-top: 0.25rem;">Max: 200 for performance</small>
                </div>
                <div class="control-group">
                    <label for="visualization-type">Visualization Type:</label>
                    <select id="visualization-type">
                        <option value="modular-rings">Modular Rings</option>
                        <option value="farey-sequence">Farey Sequence</option>
                        <option value="mobius-sum">Möbius Sum</option>
                        <option value="conformal-mapping">Conformal Mapping</option>
                    </select>
                </div>
                <div class="control-group">
                    <label for="color-scheme">Color Scheme:</label>
                    <select id="color-scheme">
                        <option value="viridis">Viridis</option>
                        <option value="plasma">Plasma</option>
                        <option value="inferno">Inferno</option>
                        <option value="custom">Custom</option>
                    </select>
                </div>
                <div class="control-group">
                    <label for="animation-speed">Animation Speed:</label>
                    <input type="range" id="animation-speed" min="0" max="100" value="50">
                    <span id="speed-value">50%</span>
                </div>
            </div>
            
            <div class="action-buttons">
                <button class="run-btn" id="run-visualization">Run Visualization</button>
                <button class="reset-btn" id="reset-parameters">Reset Parameters</button>
            </div>
            
            <div class="export-buttons">
                <button class="export-btn" id="export-csv">Export CSV</button>
                <button class="export-btn" id="export-json">Export JSON</button>
                <button class="export-btn" id="export-jpeg">Export JPEG</button>
                <button class="export-btn" id="export-pdf">Export PDF</button>
            </div>
        </div>

        <div class="status-bar" id="status-bar">
            Ready - Click "Run Visualization" to generate plots
        </div>

        <div class="visualization-area">
            <div class="viz-container">
                <div class="viz-title" id="main-viz-title">Modular Rings Visualization</div>
                <div class="viz-content" id="viz-main">
                    <div class="loading" id="loading-main">
                        <div class="spinner"></div>
                        <div>Calculating modular residues...</div>
                    </div>
                    <div class="viz-canvas" id="main-canvas"></div>
                </div>
            </div>
            
            <div class="viz-container">
                <div class="viz-title" id="properties-viz-title">Mathematical Properties</div>
                <div class="viz-content" id="viz-properties">
                    <div class="loading" id="loading-props">
                        <div class="spinner"></div>
                        <div>Computing properties...</div>
                    </div>
                    <div class="viz-canvas" id="properties-canvas"></div>
                </div>
            </div>
        </div>

        <div class="info-panel">
            <div class="info-section">
                <h3>Current Parameters</h3>
                <div class="parameter-summary" id="parameter-summary">
                    <!-- Will be populated by JavaScript -->
                </div>
            </div>
            
            <div class="info-section">
                <h3>Mathematical Framework</h3>
                <div class="math-display">
                    Φ(M) = { r ∈ {0,1,...,M-1} ∣ gcd(r,M) = 1 }
                </div>
                <div class="math-display">
                    Density = lim<sub>N→∞</sub> #{(r,M) ∣ r ∈ Φ(M), 1 ≤ M ≤ N} / ∑<sub>M=1</sub><sup>N</sup> M = 6/π²
                </div>
            </div>
            
            <div class="info-section">
                <h3>Riemann Hypothesis Connection</h3>
                <div class="math-display">
                    ∑<sub>n≤x</sub> μ(n) = O(x<sup>1/2+ε</sup>) ⇔ RH
                </div>
                <p>The geometric regularity in modular patterns serves as a diagnostic for RH-scale cancellation.</p>
            </div>
        </div>

        <div class="data-panel">
            <h3>Computed Data</h3>
            <table id="data-table">
                <thead>
                    <tr>
                        <th>Modulus</th>
                        <th>Coprime Count</th>
                        <th>Density</th>
                        <th>Möbius Sum</th>
                        <th>6/π² Ratio</th>
                    </tr>
                </thead>
                <tbody id="data-body">
                    <!-- Data will be populated by JavaScript -->
                </tbody>
            </table>
        </div>

        <footer>
            <p>Modular Visualization Framework &copy; 2024 Wessen Getachew</p>
        </footer>
    </div>

    <script>
        // Mathematical functions
        function gcd(a, b) {
            return b === 0 ? a : gcd(b, a % b);
        }

        function isCoprime(a, b) {
            return gcd(a, b) === 1;
        }

        function mobius(n) {
            if (n === 1) return 1;
            let primeCount = 0;
            let temp = n;
            
            for (let i = 2; i * i <= temp; i++) {
                if (temp % i === 0) {
                    primeCount++;
                    temp /= i;
                    if (temp % i === 0) return 0; // square factor found
                }
            }
            
            if (temp > 1) primeCount++;
            return primeCount % 2 === 0 ? 1 : -1;
        }

        function fareySequence(n) {
            const sequence = [];
            for (let denominator = 1; denominator <= n; denominator++) {
                for (let numerator = 0; numerator <= denominator; numerator++) {
                    if (gcd(numerator, denominator) === 1) {
                        sequence.push({
                            numerator,
                            denominator,
                            value: numerator / denominator
                        });
                    }
                }
            }
            return sequence.sort((a, b) => a.value - b.value);
        }

        function computeModularData(maxModulus) {
            const data = [];
            let totalResidues = 0;
            let totalCoprime = 0;
            
            for (let m = 1; m <= maxModulus; m++) {
                const residues = [];
                let coprimeCount = 0;
                let mobiusSum = 0;
                
                for (let r = 0; r < m; r++) {
                    const isCoprimeVal = isCoprime(r, m);
                    if (isCoprimeVal && r > 0) {
                        coprimeCount++;
                        mobiusSum += mobius(r);
                    }
                    
                    residues.push({
                        r,
                        m,
                        isCoprime: isCoprimeVal,
                        theta: (2 * Math.PI * r) / m,
                        x: m * Math.cos(2 * Math.PI * r / m),
                        y: m * Math.sin(2 * Math.PI * r / m)
                    });
                }
                
                totalResidues += m;
                totalCoprime += coprimeCount;
                const density = coprimeCount / m;
                const theoreticalDensity = 6 / (Math.PI * Math.PI);
                
                data.push({
                    modulus: m,
                    residues,
                    coprimeCount,
                    density,
                    mobiusSum,
                    ratio: density / theoreticalDensity
                });
            }
            
            return {
                data,
                overallDensity: totalCoprime / totalResidues,
                theoreticalDensity: 6 / (Math.PI * Math.PI)
            };
        }

        // Visualization functions for different types
        function createModularRingsVisualization(container, data, maxModulus, colorScheme) {
            // Clear previous visualization properly
            d3.select(container).selectAll("*").remove();
            
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = 40;
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            const scale = d3.scaleLinear()
                .domain([0, maxModulus])
                .range([0, Math.min(width, height) / 2 - margin]);
            
            // Color scales based on scheme
            const colorScales = {
                viridis: d3.scaleSequential(d3.interpolateViridis).domain([0, maxModulus]),
                plasma: d3.scaleSequential(d3.interpolatePlasma).domain([0, maxModulus]),
                inferno: d3.scaleSequential(d3.interpolateInferno).domain([0, maxModulus]),
                custom: d3.scaleOrdinal()
                    .domain([true, false])
                    .range(['#e74c3c', '#3498db'])
            };
            
            const colorScale = colorScales[colorScheme] || colorScales.viridis;
            
            // Create rings for each modulus
            const rings = svg.selectAll('.ring')
                .data(data.filter(d => d.modulus <= maxModulus))
                .enter()
                .append('g')
                .attr('class', 'ring')
                .attr('transform', `translate(${width/2}, ${height/2})`);
            
            // Draw circles for rings
            rings.append('circle')
                .attr('r', d => scale(d.modulus))
                .attr('fill', 'none')
                .attr('stroke', '#ddd')
                .attr('stroke-width', 1);
            
            // Draw residue points
            const points = rings.selectAll('.point')
                .data(d => d.residues.map(r => ({...r, modulus: d.modulus})))
                .enter()
                .append('circle')
                .attr('class', 'point')
                .attr('cx', d => scale(d.modulus) * Math.cos(d.theta))
                .attr('cy', d => scale(d.modulus) * Math.sin(d.theta))
                .attr('r', 3)
                .attr('fill', d => {
                    if (colorScheme === 'custom') {
                        return d.isCoprime ? colorScale(true) : colorScale(false);
                    } else {
                        return colorScale(d.modulus);
                    }
                })
                .attr('opacity', d => d.isCoprime ? 0.8 : 0.3)
                .on('mouseover', function(event, d) {
                    const tooltip = d3.select('body').append('div')
                        .attr('class', 'tooltip')
                        .style('position', 'absolute')
                        .style('background', 'rgba(0,0,0,0.8)')
                        .style('color', 'white')
                        .style('padding', '8px')
                        .style('border-radius', '4px')
                        .style('font-size', '12px')
                        .style('pointer-events', 'none');
                    
                    tooltip.html(`
                        <strong>Modulus: ${d.modulus}</strong><br>
                        Residue: ${d.r}<br>
                        Coprime: ${d.isCoprime ? 'Yes' : 'No'}<br>
                        Angle: ${(d.theta * 180 / Math.PI).toFixed(1)}°
                    `);
                })
                .on('mousemove', function(event) {
                    d3.select('.tooltip')
                        .style('left', (event.pageX + 10) + 'px')
                        .style('top', (event.pageY - 10) + 'px');
                })
                .on('mouseout', function() {
                    d3.select('.tooltip').remove();
                });
            
            // Add modulus labels
            rings.append('text')
                .attr('x', d => scale(d.modulus))
                .attr('y', 0)
                .attr('text-anchor', 'middle')
                .attr('dy', '-5')
                .text(d => d.modulus)
                .style('font-size', '10px')
                .style('fill', '#666');
        }

        function createFareySequenceVisualization(container, data, maxModulus, colorScheme) {
            d3.select(container).selectAll("*").remove();
            
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = 40;
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            // Generate Farey sequence
            const farey = fareySequence(maxModulus);
            
            // Color scale for fractions
            const colorScale = d3.scaleSequential(d3.interpolateViridis)
                .domain([0, farey.length]);
            
            // Plot Farey sequence on unit circle
            const scale = Math.min(width, height) / 2 - margin;
            
            const points = svg.selectAll('.farey-point')
                .data(farey)
                .enter()
                .append('circle')
                .attr('class', 'farey-point')
                .attr('cx', d => width/2 + scale * Math.cos(2 * Math.PI * d.value))
                .attr('cy', d => height/2 + scale * Math.sin(2 * Math.PI * d.value))
                .attr('r', 3)
                .attr('fill', (d, i) => colorScale(i))
                .attr('opacity', 0.7)
                .on('mouseover', function(event, d) {
                    const tooltip = d3.select('body').append('div')
                        .attr('class', 'tooltip')
                        .style('position', 'absolute')
                        .style('background', 'rgba(0,0,0,0.8)')
                        .style('color', 'white')
                        .style('padding', '8px')
                        .style('border-radius', '4px')
                        .style('font-size', '12px')
                        .style('pointer-events', 'none');
                    
                    tooltip.html(`
                        <strong>Farey Fraction</strong><br>
                        ${d.numerator}/${d.denominator}<br>
                        Value: ${d.value.toFixed(4)}
                    `);
                })
                .on('mousemove', function(event) {
                    d3.select('.tooltip')
                        .style('left', (event.pageX + 10) + 'px')
                        .style('top', (event.pageY - 10) + 'px');
                })
                .on('mouseout', function() {
                    d3.select('.tooltip').remove();
                });
            
            // Draw unit circle
            svg.append('circle')
                .attr('cx', width/2)
                .attr('cy', height/2)
                .attr('r', scale)
                .attr('fill', 'none')
                .attr('stroke', '#ddd')
                .attr('stroke-width', 1);
            
            // Add title
            svg.append('text')
                .attr('x', width/2)
                .attr('y', 20)
                .attr('text-anchor', 'middle')
                .text(`Farey Sequence of Order ${maxModulus} (${farey.length} fractions)`)
                .style('font-size', '14px')
                .style('font-weight', 'bold');
        }

        function createMobiusSumVisualization(container, data, maxModulus, colorScheme) {
            d3.select(container).selectAll("*").remove();
            
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = {top: 40, right: 30, bottom: 40, left: 50};
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            // Extract Möbius sums
            const mobiusData = data.map(d => ({
                modulus: d.modulus,
                mobiusSum: d.mobiusSum,
                cumulative: data.slice(0, d.modulus).reduce((sum, item) => sum + item.mobiusSum, 0)
            }));
            
            const xScale = d3.scaleLinear()
                .domain([1, maxModulus])
                .range([margin.left, width - margin.right]);
            
            const yScale = d3.scaleLinear()
                .domain(d3.extent(mobiusData, d => d.mobiusSum))
                .range([height - margin.bottom, margin.top]);
            
            const cumulativeYScale = d3.scaleLinear()
                .domain(d3.extent(mobiusData, d => d.cumulative))
                .range([height - margin.bottom, margin.top]);
            
            // Color scale
            const lineColor = colorScheme === 'plasma' ? '#f0e442' : 
                             colorScheme === 'inferno' ? '#fcffa4' : '#3498db';
            
            // Möbius sum line
            const line = d3.line()
                .x(d => xScale(d.modulus))
                .y(d => yScale(d.mobiusSum));
            
            svg.append('path')
                .datum(mobiusData)
                .attr('fill', 'none')
                .attr('stroke', lineColor)
                .attr('stroke-width', 2)
                .attr('d', line);
            
            // Cumulative sum line
            const cumulativeLine = d3.line()
                .x(d => xScale(d.modulus))
                .y(d => cumulativeYScale(d.cumulative));
            
            svg.append('path')
                .datum(mobiusData)
                .attr('fill', 'none')
                .attr('stroke', '#e74c3c')
                .attr('stroke-width', 1)
                .attr('stroke-dasharray', '5,5')
                .attr('d', cumulativeLine);
            
            // Axes
            const xAxis = d3.axisBottom(xScale);
            const yAxis = d3.axisLeft(yScale);
            
            svg.append('g')
                .attr('transform', `translate(0, ${height - margin.bottom})`)
                .call(xAxis);
            
            svg.append('g')
                .attr('transform', `translate(${margin.left}, 0)`)
                .call(yAxis);
            
            // Labels
            svg.append('text')
                .attr('x', width / 2)
                .attr('y', height - 5)
                .attr('text-anchor', 'middle')
                .text('Modulus');
            
            svg.append('text')
                .attr('transform', 'rotate(-90)')
                .attr('x', -height / 2)
                .attr('y', 15)
                .attr('text-anchor', 'middle')
                .text('Möbius Sum');
            
            // Legend
            const legend = svg.append('g')
                .attr('transform', `translate(${width - 150}, ${margin.top})`);
            
            legend.append('line')
                .attr('x1', 0)
                .attr('x2', 20)
                .attr('y1', 0)
                .attr('y2', 0)
                .attr('stroke', lineColor)
                .attr('stroke-width', 2);
            
            legend.append('text')
                .attr('x', 25)
                .attr('y', 0)
                .attr('dy', '0.35em')
                .text('Möbius Sum')
                .style('font-size', '12px');
            
            legend.append('line')
                .attr('x1', 0)
                .attr('x2', 20)
                .attr('y1', 20)
                .attr('y2', 20)
                .attr('stroke', '#e74c3c')
                .attr('stroke-width', 1)
                .attr('stroke-dasharray', '5,5');
            
            legend.append('text')
                .attr('x', 25)
                .attr('y', 20)
                .attr('dy', '0.35em')
                .text('Cumulative Sum')
                .style('font-size', '12px');
        }

        function createConformalMappingVisualization(container, data, maxModulus, colorScheme) {
            d3.select(container).selectAll("*").remove();
            
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = 40;
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            // Universal modular conformal mapping: Φ(r, m) = m·e^(2πi r/m)
            const allPoints = [];
            data.forEach(modulusData => {
                modulusData.residues.forEach(residue => {
                    if (residue.isCoprime) {
                        allPoints.push({
                            x: residue.x,
                            y: residue.y,
                            modulus: residue.m,
                            residue: residue.r,
                            theta: residue.theta
                        });
                    }
                });
            });
            
            // Find bounds for scaling
            const xExtent = d3.extent(allPoints, d => d.x);
            const yExtent = d3.extent(allPoints, d => d.y);
            const maxExtent = Math.max(
                Math.abs(xExtent[0]), Math.abs(xExtent[1]),
                Math.abs(yExtent[0]), Math.abs(yExtent[1])
            );
            
            const scale = d3.scaleLinear()
                .domain([-maxExtent, maxExtent])
                .range([margin, width - margin]);
            
            // Color scale
            const colorScale = d3.scaleSequential(d3.interpolateViridis)
                .domain([0, maxModulus]);
            
            // Plot all coprime points
            const points = svg.selectAll('.conformal-point')
                .data(allPoints)
                .enter()
                .append('circle')
                .attr('class', 'conformal-point')
                .attr('cx', d => scale(d.x))
                .attr('cy', d => scale(d.y))
                .attr('r', 2)
                .attr('fill', d => colorScale(d.modulus))
                .attr('opacity', 0.6)
                .on('mouseover', function(event, d) {
                    const tooltip = d3.select('body').append('div')
                        .attr('class', 'tooltip')
                        .style('position', 'absolute')
                        .style('background', 'rgba(0,0,0,0.8)')
                        .style('color', 'white')
                        .style('padding', '8px')
                        .style('border-radius', '4px')
                        .style('font-size', '12px')
                        .style('pointer-events', 'none');
                    
                    tooltip.html(`
                        <strong>Conformal Mapping</strong><br>
                        Modulus: ${d.modulus}<br>
                        Residue: ${d.residue}<br>
                        Point: (${d.x.toFixed(2)}, ${d.y.toFixed(2)})
                    `);
                })
                .on('mousemove', function(event) {
                    d3.select('.tooltip')
                        .style('left', (event.pageX + 10) + 'px')
                        .style('top', (event.pageY - 10) + 'px');
                })
                .on('mouseout', function() {
                    d3.select('.tooltip').remove();
                });
            
            // Add coordinate axes
            svg.append('line')
                .attr('x1', scale(0))
                .attr('x2', scale(0))
                .attr('y1', margin)
                .attr('y2', height - margin)
                .attr('stroke', '#ccc')
                .attr('stroke-width', 1);
            
            svg.append('line')
                .attr('x1', margin)
                .attr('x2', width - margin)
                .attr('y1', scale(0))
                .attr('y2', scale(0))
                .attr('stroke', '#ccc')
                .attr('stroke-width', 1);
            
            // Add title
            svg.append('text')
                .attr('x', width/2)
                .attr('y', 20)
                .attr('text-anchor', 'middle')
                .text('Universal Modular Conformal Mapping: Φ(r,m) = m·e^(2πi r/m)')
                .style('font-size', '14px')
                .style('font-weight', 'bold');
        }

        function createPropertiesVisualization(container, data, colorScheme, vizType) {
            d3.select(container).selectAll("*").remove();
            
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = {top: 20, right: 30, bottom: 40, left: 50};
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            const xScale = d3.scaleLinear()
                .domain([1, data.length])
                .range([margin.left, width - margin.right]);
            
            const yScale = d3.scaleLinear()
                .domain([0, 1])
                .range([height - margin.bottom, margin.top]);
            
            // Color scale
            const lineColor = colorScheme === 'plasma' ? '#f0e442' : 
                             colorScheme === 'inferno' ? '#fcffa4' : '#3498db';
            
            // Theoretical density line
            const theoreticalDensity = 6 / (Math.PI * Math.PI);
            svg.append('line')
                .attr('x1', margin.left)
                .attr('x2', width - margin.right)
                .attr('y1', yScale(theoreticalDensity))
                .attr('y2', yScale(theoreticalDensity))
                .attr('stroke', '#e74c3c')
                .attr('stroke-width', 2)
                .attr('stroke-dasharray', '5,5');
            
            // Actual density line
            const line = d3.line()
                .x(d => xScale(d.modulus))
                .y(d => yScale(d.density));
            
            svg.append('path')
                .datum(data)
                .attr('fill', 'none')
                .attr('stroke', lineColor)
                .attr('stroke-width', 2)
                .attr('d', line);
            
            // Axes
            const xAxis = d3.axisBottom(xScale);
            const yAxis = d3.axisLeft(yScale);
            
            svg.append('g')
                .attr('transform', `translate(0, ${height - margin.bottom})`)
                .call(xAxis);
            
            svg.append('g')
                .attr('transform', `translate(${margin.left}, 0)`)
                .call(yAxis);
            
            // Labels
            svg.append('text')
                .attr('x', width / 2)
                .attr('y', height - 5)
                .attr('text-anchor', 'middle')
                .text('Modulus');
            
            svg.append('text')
                .attr('transform', 'rotate(-90)')
                .attr('x', -height / 2)
                .attr('y', 15)
                .attr('text-anchor', 'middle')
                .text('Density');
            
            // Legend
            const legend = svg.append('g')
                .attr('transform', `translate(${width - 150}, ${margin.top})`);
            
            legend.append('line')
                .attr('x1', 0)
                .attr('x2', 20)
                .attr('y1', 0)
                .attr('y2', 0)
                .attr('stroke', lineColor)
                .attr('stroke-width', 2);
            
            legend.append('text')
                .attr('x', 25)
                .attr('y', 0)
                .attr('dy', '0.35em')
                .text('Actual Density')
                .style('font-size', '12px');
            
            legend.append('line')
                .attr('x1', 0)
                .attr('x2', 20)
                .attr('y1', 20)
                .attr('y2', 20)
                .attr('stroke', '#e74c3c')
                .attr('stroke-width', 2)
                .attr('stroke-dasharray', '5,5');
            
            legend.append('text')
                .attr('x', 25)
                .attr('y', 20)
                .attr('dy', '0.35em')
                .text('6/π² = ' + theoreticalDensity.toFixed(4))
                .style('font-size', '12px');
        }

        function updateParameterSummary(params) {
            const summary = document.getElementById('parameter-summary');
            summary.innerHTML = `
                <div class="param-item">
                    <div class="param-label">Modulus</div>
                    <div class="param-value">${params.modulus}</div>
                </div>
                <div class="param-item">
                    <div class="param-label">Visualization</div>
                    <div class="param-value">${params.visualizationType}</div>
                </div>
                <div class="param-item">
                    <div class="param-label">Color Scheme</div>
                    <div class="param-value">${params.colorScheme}</div>
                </div>
                <div class="param-item">
                    <div class="param-label">Animation</div>
                    <div class="param-value">${params.animationSpeed}%</div>
                </div>
            `;
        }

        function updateDataTable(data) {
            const tbody = document.getElementById('data-body');
            tbody.innerHTML = '';
            
            // Show only a subset for performance
            const displayData = data.filter((item, index) => index % Math.ceil(data.length / 20) === 0 || index === data.length - 1);
            
            displayData.forEach(item => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${item.modulus}</td>
                    <td>${item.coprimeCount}</td>
                    <td>${item.density.toFixed(4)}</td>
                    <td>${item.mobiusSum}</td>
                    <td>${item.ratio.toFixed(4)}</td>
                `;
                tbody.appendChild(row);
            });
        }

        function updateStatus(message, isError = false) {
            const statusBar = document.getElementById('status-bar');
            statusBar.textContent = message;
            statusBar.style.borderLeftColor = isError ? '#e74c3c' : '#3498db';
            statusBar.style.background = isError ? '#fee' : 'var(--card-color)';
            statusBar.style.color = isError ? '#c33' : 'var(--text-color)';
        }

        // Export functions
        function exportCSV(data) {
            let csv = 'Modulus,Coprime_Count,Density,Mobius_Sum,Ratio_To_6_over_pi_squared\n';
            data.forEach(item => {
                csv += `${item.modulus},${item.coprimeCount},${item.density.toFixed(6)},${item.mobiusSum},${item.ratio.toFixed(6)}\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `modular_data_N${document.getElementById('modulus').value}.csv`;
            a.click();
            window.URL.revokeObjectURL(url);
        }

        function exportJSON(data) {
            const jsonData = {
                metadata: {
                    modulus: parseInt(document.getElementById('modulus').value),
                    timestamp: new Date().toISOString(),
                    theoreticalDensity: 6 / (Math.PI * Math.PI)
                },
                data: data
            };
            
            const blob = new Blob([JSON.stringify(jsonData, null, 2)], { type: 'application/json' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `modular_data_N${document.getElementById('modulus').value}.json`;
            a.click();
            window.URL.revokeObjectURL(url);
        }

        function exportJPEG() {
            const element = document.getElementById('viz-main');
            updateStatus('Exporting JPEG...');
            html2canvas(element).then(canvas => {
                const link = document.createElement('a');
                link.download = `modular_visualization_N${document.getElementById('modulus').value}.jpg`;
                link.href = canvas.toDataURL('image/jpeg', 0.9);
                link.click();
                updateStatus('JPEG export completed');
            });
        }

        function exportPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            updateStatus('Exporting PDF...');
            
            // Add title
            doc.setFontSize(20);
            doc.text('Modular Visualization Framework', 20, 20);
            doc.setFontSize(12);
            doc.text(`Generated by Wessen Getachew - ${new Date().toLocaleDateString()}`, 20, 30);
            doc.text(`Modulus: ${document.getElementById('modulus').value}`, 20, 40);
            
            // Add some data
            doc.text('Mathematical Properties:', 20, 60);
            doc.text(`Theoretical Density (6/π²): ${(6/(Math.PI*Math.PI)).toFixed(6)}`, 30, 70);
            
            doc.save(`modular_analysis_N${document.getElementById('modulus').value}.pdf`);
            updateStatus('PDF export completed');
        }

        // Main application logic
        let currentData = null;
        let isComputing = false;

        function runVisualization() {
            if (isComputing) {
                updateStatus('Computation in progress... please wait', true);
                return;
            }

            const modulus = parseInt(document.getElementById('modulus').value);
            const vizType = document.getElementById('visualization-type').value;
            const colorScheme = document.getElementById('color-scheme').value;
            const animationSpeed = document.getElementById('animation-speed').value;
            
            // Validate input
            if (isNaN(modulus) || modulus < 1 || modulus > 200) {
                updateStatus('Error: Modulus must be a number between 1 and 200', true);
                return;
            }
            
            isComputing = true;
            
            // Update status
            updateStatus(`Computing data for ${vizType.replace('-', ' ')} with N=${modulus}...`);
            
            // Show loading
            document.getElementById('loading-main').style.display = 'block';
            document.getElementById('loading-props').style.display = 'block';
            
            // Update viz titles
            const vizTypeNames = {
                'modular-rings': 'Modular Rings',
                'farey-sequence': 'Farey Sequence', 
                'mobius-sum': 'Möbius Sum',
                'conformal-mapping': 'Conformal Mapping'
            };
            
            document.getElementById('main-viz-title').textContent = 
                vizTypeNames[vizType] + ' (N=' + modulus + ')';
            document.getElementById('properties-viz-title').textContent = 
                'Mathematical Properties - ' + vizTypeNames[vizType];
            
            // Use setTimeout to allow UI to update
            setTimeout(() => {
                try {
                    const computedData = computeModularData(modulus);
                    currentData = computedData.data;
                    
                    // Clear any existing tooltips
                    d3.selectAll('.tooltip').remove();
                    
                    // Create main visualization based on type
                    switch(vizType) {
                        case 'modular-rings':
                            createModularRingsVisualization(
                                document.getElementById('main-canvas'), 
                                currentData, 
                                modulus,
                                colorScheme
                            );
                            break;
                        case 'farey-sequence':
                            createFareySequenceVisualization(
                                document.getElementById('main-canvas'),
                                currentData,
                                modulus,
                                colorScheme
                            );
                            break;
                        case 'mobius-sum':
                            createMobiusSumVisualization(
                                document.getElementById('main-canvas'),
                                currentData,
                                modulus,
                                colorScheme
                            );
                            break;
                        case 'conformal-mapping':
                            createConformalMappingVisualization(
                                document.getElementById('main-canvas'),
                                currentData,
                                modulus,
                                colorScheme
                            );
                            break;
                    }
                    
                    // Always show density properties in second panel
                    createPropertiesVisualization(
                        document.getElementById('properties-canvas'),
                        currentData,
                        colorScheme,
                        vizType
                    );
                    
                    updateDataTable(currentData);
                    
                    // Update parameter summary
                    updateParameterSummary({
                        modulus,
                        visualizationType: vizTypeNames[vizType],
                        colorScheme,
                        animationSpeed
                    });
                    
                    updateStatus(`Visualization completed. Overall density: ${(computedData.overallDensity).toFixed(6)} (Theoretical: ${computedData.theoreticalDensity.toFixed(6)})`);
                    
                } catch (error) {
                    console.error('Visualization error:', error);
                    updateStatus('Error: ' + error.message, true);
                } finally {
                    // Hide loading
                    document.getElementById('loading-main').style.display = 'none';
                    document.getElementById('loading-props').style.display = 'none';
                    isComputing = false;
                }
            }, 100);
        }

        function resetParameters() {
            document.getElementById('modulus').value = 30;
            document.getElementById('visualization-type').value = 'modular-rings';
            document.getElementById('color-scheme').value = 'viridis';
            document.getElementById('animation-speed').value = 50;
            document.getElementById('speed-value').textContent = '50%';
            updateStatus('Parameters reset to defaults');
        }

        // Event listeners
        document.getElementById('run-visualization').addEventListener('click', runVisualization);
        document.getElementById('reset-parameters').addEventListener('click', resetParameters);
        
        document.getElementById('animation-speed').addEventListener('input', function() {
            document.getElementById('speed-value').textContent = this.value + '%';
        });
        
        document.getElementById('export-csv').addEventListener('click', () => {
            if (currentData) {
                exportCSV(currentData);
                updateStatus('CSV export completed');
            } else {
                updateStatus('Error: No data to export. Please run visualization first.', true);
            }
        });
        
        document.getElementById('export-json').addEventListener('click', () => {
            if (currentData) {
                exportJSON(currentData);
                updateStatus('JSON export completed');
            } else {
                updateStatus('Error: No data to export. Please run visualization first.', true);
            }
        });
        
        document.getElementById('export-jpeg').addEventListener('click', exportJPEG);
        document.getElementById('export-pdf').addEventListener('click', exportPDF);

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateStatus('Ready - Configure parameters and click "Run Visualization"');
            document.getElementById('speed-value').textContent = '50%';
            
            // Add performance warning for large moduli
            const modulusInput = document.getElementById('modulus');
            modulusInput.addEventListener('change', function() {
                if (this.value > 100) {
                    updateStatus('Note: Large moduli may take longer to compute', false);
                }
            });
        });
    </script>
</body>
</html>
