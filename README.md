<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Coprime Density Analyzer</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
    <!-- MathJax for LaTeX rendering -->
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            background: #f8f9fa;
            line-height: 1.6;
            color: #333;
        }
        
        .container {
            background: white;
            padding: 25px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            border-left: 4px solid var(--secondary);
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
            transform: translateY(-1px);
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
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Modular Coprime Density Analyzer</h1>
            <p>An interactive tool for exploring the convergence of coprime density to the theoretical limit of \( \frac{6}{\pi^2} \)</p>
        </div>
        
        <div class="theorem">
            <div class="theorem-title">Mathematical Foundation</div>
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
                
                <button onclick="runAnalysis()">Run Analysis</button>
            </div>
        </div>
    </div>

    <div class="container">
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
    </div>

    <div class="container">
        <h2>Angular Distribution Visualization</h2>
        <p>This visualization shows the distribution of coprime residues on the unit circle for different moduli. Each point represents a residue \( r \) where \( \gcd(r, m) = 1 \), positioned at angle \( \theta = \frac{2\pi r}{m} \).</p>
        
        <div id="angularVisualization" class="angular-vis">
            <!-- Angular plots will be generated here -->
        </div>
    </div>

    <div class="container">
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
    </div>

    <div class="footer">
        <p>Modular Coprime Density Analyzer | Mathematical Visualization Tool</p>
    </div>

    <script>
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

        function runAnalysis() {
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

        // Initialize on load
        document.addEventListener('DOMContentLoaded', function() {
            // Run initial analysis with smaller dataset for quick load
            document.getElementById('maxModulus').value = '500';
            runAnalysis();
        });
    </script>
</body>
</html>
