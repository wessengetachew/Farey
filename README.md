
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
            margin-bottom: 1rem;
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

        footer {
            text-align: center;
            margin-top: 2rem;
            padding: 1rem;
            color: #666;
            border-top: 1px solid #ddd;
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
                    <input type="number" id="modulus" min="1" max="1000" value="30">
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
                </div>
            </div>
            
            <div class="export-buttons">
                <button class="export-btn" id="export-csv">Export CSV</button>
                <button class="export-btn" id="export-json">Export JSON</button>
                <button class="export-btn" id="export-jpeg">Export JPEG</button>
                <button class="export-btn" id="export-pdf">Export PDF</button>
            </div>
        </div>

        <div class="visualization-area">
            <div class="viz-container">
                <div class="viz-title">Modular Rings Visualization</div>
                <div class="viz-content" id="viz-main">
                    <div class="loading" id="loading-main">
                        <div class="spinner"></div>
                        <div>Calculating modular residues...</div>
                    </div>
                </div>
            </div>
            
            <div class="viz-container">
                <div class="viz-title">Mathematical Properties</div>
                <div class="viz-content" id="viz-properties">
                    <div class="loading" id="loading-props">
                        <div class="spinner"></div>
                        <div>Computing properties...</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="info-panel">
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
                    if (isCoprimeVal) {
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

        // Visualization functions
        function createModularRingsVisualization(container, data, maxModulus) {
            const width = container.clientWidth;
            const height = container.clientHeight;
            const margin = 40;
            
            // Clear previous visualization
            container.innerHTML = '';
            
            const svg = d3.select(container)
                .append('svg')
                .attr('width', width)
                .attr('height', height);
            
            const scale = d3.scaleLinear()
                .domain([0, maxModulus])
                .range([0, Math.min(width, height) / 2 - margin]);
            
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
                .attr('fill', d => d.isCoprime ? '#e74c3c' : '#3498db')
                .attr('opacity', d => d.isCoprime ? 0.8 : 0.3)
                .on('mouseover', function(event, d) {
                    // Show tooltip
                    const tooltip = d3.select('body').append('div')
                        .attr('class', 'tooltip')
                        .style('position', 'absolute')
                        .style('background', 'white')
                        .style('padding', '5px')
                        .style('border', '1px solid #ccc')
                        .style('border-radius', '3px')
                        .style('pointer-events', 'none');
                    
                    tooltip.html(`
                        Modulus: ${d.modulus}<br>
                        Residue: ${d.r}<br>
                        Coprime: ${d.isCoprime}<br>
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

        function createPropertiesVisualization(container, data) {
            container.innerHTML = '';
            
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
                .attr('stroke', '#3498db')
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
                .attr('stroke', '#3498db')
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

        function updateDataTable(data) {
            const tbody = document.getElementById('data-body');
            tbody.innerHTML = '';
            
            data.forEach(item => {
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
            html2canvas(element).then(canvas => {
                const link = document.createElement('a');
                link.download = `modular_visualization_N${document.getElementById('modulus').value}.jpg`;
                link.href = canvas.toDataURL('image/jpeg', 0.9);
                link.click();
            });
        }

        function exportPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Add title
            doc.setFontSize(20);
            doc.text('Modular Visualization Framework', 20, 20);
            doc.setFontSize(12);
            doc.text(`Generated by Wessen Getachew - ${new Date().toLocaleDateString()}`, 20, 30);
            doc.text(`Modulus: ${document.getElementById('modulus').value}`, 20, 40);
            
            // Add some data
            doc.text('Mathematical Properties:', 20, 60);
            doc.text(`Theoretical Density (6/π²): ${(6/(Math.PI*Math.PI)).toFixed(6)}`, 30, 70);
            
            // For now, we'll just save the PDF. In a real implementation, 
            // you might want to add the visualizations as images.
            doc.save(`modular_analysis_N${document.getElementById('modulus').value}.pdf`);
        }

        // Main application logic
        let currentData = null;

        function updateVisualizations() {
            const modulus = parseInt(document.getElementById('modulus').value);
            const vizType = document.getElementById('visualization-type').value;
            
            // Show loading
            document.getElementById('loading-main').style.display = 'block';
            document.getElementById('loading-props').style.display = 'block';
            
            setTimeout(() => {
                const computedData = computeModularData(modulus);
                currentData = computedData.data;
                
                createModularRingsVisualization(
                    document.getElementById('viz-main'), 
                    currentData, 
                    modulus
                );
                
                createPropertiesVisualization(
                    document.getElementById('viz-properties'),
                    currentData
                );
                
                updateDataTable(currentData);
                
                // Hide loading
                document.getElementById('loading-main').style.display = 'none';
                document.getElementById('loading-props').style.display = 'none';
            }, 100);
        }

        // Event listeners
        document.getElementById('modulus').addEventListener('change', updateVisualizations);
        document.getElementById('visualization-type').addEventListener('change', updateVisualizations);
        
        document.getElementById('export-csv').addEventListener('click', () => {
            if (currentData) exportCSV(currentData);
        });
        
        document.getElementById('export-json').addEventListener('click', () => {
            if (currentData) exportJSON(currentData);
        });
        
        document.getElementById('export-jpeg').addEventListener('click', exportJPEG);
        document.getElementById('export-pdf').addEventListener('click', exportPDF);

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateVisualizations();
        });
    </script>
</body>
</html>
