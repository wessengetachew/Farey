
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Sieve Explorer - Harmonic Numbers, Zeta Values & Twin Prime Heuristics</title>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
    <script src="https://d3js.org/d3.v7.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.2/papaparse.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --text-color: #2c3e50;
            --background-color: #ecf0f1;
            --card-color: #ffffff;
        }

        .dark-mode {
            --primary-color: #ecf0f1;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --text-color: #ecf0f1;
            --background-color: #2c3e50;
            --card-color: #34495e;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            background-color: var(--background-color);
            margin: 0;
            padding: 20px;
            transition: all 0.3s ease;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            background: var(--card-color);
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
        }

        h1, h2, h3 {
            color: var(--primary-color);
        }

        .card {
            background: var(--card-color);
            padding: 1.5rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
        }

        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .control-group {
            background: var(--card-color);
            padding: 1rem;
            border-radius: 8px;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: bold;
        }

        input, select, button {
            width: 100%;
            padding: 0.5rem;
            margin-bottom: 1rem;
            border: 1px solid #bdc3c7;
            border-radius: 4px;
            background: var(--card-color);
            color: var(--text-color);
        }

        button {
            background: var(--secondary-color);
            color: white;
            border: none;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        button:hover {
            background: #2980b9;
        }

        .visualization-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        @media (max-width: 768px) {
            .visualization-container {
                grid-template-columns: 1fr;
            }
        }

        .visualization {
            background: var(--card-color);
            padding: 1rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .color-picker {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .color-option {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid transparent;
        }

        .color-option.active {
            border-color: var(--text-color);
        }

        .export-options {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 1rem 0;
        }

        th, td {
            padding: 0.5rem;
            text-align: left;
            border-bottom: 1px solid #bdc3c7;
        }

        th {
            background: var(--secondary-color);
            color: white;
        }

        .math-display {
            background: rgba(52, 152, 219, 0.1);
            padding: 1rem;
            border-radius: 5px;
            margin: 1rem 0;
            overflow-x: auto;
        }

        .citation {
            font-size: 0.9rem;
            color: #7f8c8d;
            margin-top: 3rem;
            padding-top: 1rem;
            border-top: 1px solid #bdc3c7;
        }

        .toggle-container {
            display: flex;
            justify-content: flex-end;
            margin-bottom: 1rem;
        }

        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
        }

        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--secondary-color);
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="toggle-container">
            <label class="toggle-switch">
                <input type="checkbox" id="darkModeToggle">
                <span class="slider"></span>
            </label>
            <span style="margin-left: 10px;">Dark Mode</span>
        </div>

        <header>
            <h1>Modular Sieve Explorer: Harmonic Numbers, Zeta Values & Twin Prime Heuristics</h1>
            <p class="author">Interactive Tool by Wessen Getachew</p>
            <div class="math-display">
                Exploring connections between \(H_n = \sum_{k=1}^n \frac{1}{k}\), \(\zeta(2)=\frac{\pi^2}{6}\), 
                divisor sums \(\sigma(n)\), and modular sieve densities for twin prime heuristics.
            </div>
        </header>

        <div class="controls">
            <div class="control-group">
                <h3>Modulus Parameters</h3>
                <label for="modulusBase">Base Modulus:</label>
                <select id="modulusBase">
                    <option value="30">30 (2×3×5)</option>
                    <option value="210">210 (2×3×5×7)</option>
                    <option value="2310">2310 (2×3×5×7×11)</option>
                </select>

                <label for="powerOfTwo">Power of 2 multiplier (n):</label>
                <input type="number" id="powerOfTwo" min="0" max="6" value="0">

                <label for="maxX">Maximum x value for plots:</label>
                <input type="number" id="maxX" min="100" max="10000" value="1000">
            </div>

            <div class="control-group">
                <h3>Visualization Options</h3>
                <label>Color Scheme:</label>
                <div class="color-picker">
                    <div class="color-option active" style="background-color: #3498db;" data-scheme="blue"></div>
                    <div class="color-option" style="background-color: #e74c3c;" data-scheme="red"></div>
                    <div class="color-option" style="background-color: #2ecc71;" data-scheme="green"></div>
                    <div class="color-option" style="background-color: #9b59b6;" data-scheme="purple"></div>
                </div>

                <label for="pointSize">Point Size:</label>
                <input type="range" id="pointSize" min="1" max="10" value="3">

                <label for="animationSpeed">Animation Speed:</label>
                <input type="range" id="animationSpeed" min="1" max="10" value="5">
            </div>

            <div class="control-group">
                <h3>Calculation Parameters</h3>
                <label for="twinPrimeConstantPrecision">Twin Prime Constant Precision (decimal places):</label>
                <input type="number" id="twinPrimeConstantPrecision" min="5" max="15" value="10">

                <label for="harmonicNumberLimit">Harmonic Number Calculation Limit:</label>
                <input type="number" id="harmonicNumberLimit" min="10" max="100000" value="1000">

                <button id="calculateAll">Calculate All</button>
            </div>
        </div>

        <div class="visualization-container">
            <div class="visualization">
                <h3>Modular Sieve Visualization (Residues mod M)</h3>
                <div id="modularSievePlot"></div>
            </div>
            <div class="visualization">
                <h3>Harmonic Numbers vs Logarithmic Growth</h3>
                <div id="harmonicPlot"></div>
            </div>
        </div>

        <div class="visualization-container">
            <div class="visualization">
                <h3>Twin Prime Heuristic Density</h3>
                <div id="twinPrimePlot"></div>
            </div>
            <div class="visualization">
                <h3>Sum of Divisors σ(n) Average Order</h3>
                <div id="divisorSumPlot"></div>
            </div>
        </div>

        <div class="card">
            <h2>Step-by-Step Calculations</h2>
            <div id="calculations">
                <!-- Dynamic calculations will appear here -->
            </div>
        </div>

        <div class="card">
            <h2>LARCH Search Region Data</h2>
            <div class="export-options">
                <button id="exportCSV">Export CSV</button>
                <button id="exportJPEG">Export Visualization as JPEG</button>
            </div>
            <div id="larchData">
                <!-- LARCH data table will appear here -->
            </div>
        </div>

        <div class="citation">
            <h3>References & Citations</h3>
            <p><strong>Primary Sources:</strong></p>
            <ul>
                <li>Hardy, G. H., & Littlewood, J. E. (1923). Some problems of 'Partitio numerorum'; III: On the expression of a number as a sum of primes. Acta Mathematica, 44, 1-70.</li>
                <li>Apostol, T. M. (1976). Introduction to Analytic Number Theory. Springer-Verlag.</li>
                <li>Montgomery, H. L., & Vaughan, R. C. (2007). Multiplicative Number Theory I: Classical Theory. Cambridge University Press.</li>
            </ul>
            <p><strong>Methodology & Implementation:</strong></p>
            <p>Getachew, W. (2024). Modular Sieve Framework for Twin Prime Distribution Analysis. Interactive computational tool implementing Hardy-Littlewood heuristics with modular density visualization.</p>
            <p><strong>Tool Implementation:</strong> This interactive explorer implements the mathematical framework described in "Harmonic numbers, zeta-values, divisor sums, and modular-density connections" and "Appendix: Hardy-Littlewood Twin-Prime Constant, Local Densities, and a Modular-Sieve Perspective" by Wessen Getachew.</p>
        </div>
    </div>

    <script>
        // Configuration and state
        const config = {
            colorScheme: 'blue',
            pointSize: 3,
            animationSpeed: 5,
            modulusBase: 30,
            powerOfTwo: 0,
            maxX: 1000,
            twinPrimePrecision: 10,
            harmonicLimit: 1000
        };

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            initializeEventListeners();
            calculateAll();
        });

        function initializeEventListeners() {
            // Dark mode toggle
            document.getElementById('darkModeToggle').addEventListener('change', function(e) {
                document.body.classList.toggle('dark-mode', e.target.checked);
            });

            // Color scheme selection
            document.querySelectorAll('.color-option').forEach(option => {
                option.addEventListener('click', function() {
                    document.querySelectorAll('.color-option').forEach(opt => opt.classList.remove('active'));
                    this.classList.add('active');
                    config.colorScheme = this.getAttribute('data-scheme');
                    updateVisualizations();
                });
            });

            // Parameter controls
            document.getElementById('modulusBase').addEventListener('change', function(e) {
                config.modulusBase = parseInt(e.target.value);
                calculateAll();
            });

            document.getElementById('powerOfTwo').addEventListener('change', function(e) {
                config.powerOfTwo = parseInt(e.target.value);
                calculateAll();
            });

            document.getElementById('maxX').addEventListener('change', function(e) {
                config.maxX = parseInt(e.target.value);
                calculateAll();
            });

            document.getElementById('pointSize').addEventListener('input', function(e) {
                config.pointSize = parseInt(e.target.value);
                updateVisualizations();
            });

            document.getElementById('animationSpeed').addEventListener('input', function(e) {
                config.animationSpeed = parseInt(e.target.value);
                updateVisualizations();
            });

            document.getElementById('twinPrimeConstantPrecision').addEventListener('change', function(e) {
                config.twinPrimePrecision = parseInt(e.target.value);
                calculateAll();
            });

            document.getElementById('harmonicNumberLimit').addEventListener('change', function(e) {
                config.harmonicLimit = parseInt(e.target.value);
                calculateAll();
            });

            document.getElementById('calculateAll').addEventListener('click', calculateAll);
            document.getElementById('exportCSV').addEventListener('click', exportCSV);
            document.getElementById('exportJPEG').addEventListener('click', exportJPEG);
        }

        function calculateAll() {
            const modulus = config.modulusBase * Math.pow(2, config.powerOfTwo);
            
            // Calculate harmonic numbers
            const harmonicData = calculateHarmonicNumbers(config.harmonicLimit);
            
            // Calculate twin prime constant and heuristic
            const twinPrimeData = calculateTwinPrimeHeuristic(config.maxX, config.twinPrimePrecision);
            
            // Calculate divisor sums
            const divisorSumData = calculateDivisorSums(config.maxX);
            
            // Calculate modular sieve data
            const sieveData = calculateModularSieve(modulus);
            
            // Update displays
            updateCalculationsDisplay(harmonicData, twinPrimeData, divisorSumData, sieveData, modulus);
            updateVisualizations(harmonicData, twinPrimeData, divisorSumData, sieveData);
            updateLARCHData(sieveData, modulus);
        }

        function calculateHarmonicNumbers(limit) {
            const data = [];
            let sum = 0;
            for (let n = 1; n <= limit; n++) {
                sum += 1/n;
                data.push({
                    n: n,
                    H_n: sum,
                    ln_n: Math.log(n),
                    gamma: 0.5772156649, // Euler-Mascheroni constant
                    H_n_minus_ln: sum - Math.log(n)
                });
            }
            return data;
        }

        function calculateTwinPrimeHeuristic(maxX, precision) {
            // Calculate twin prime constant C₂
            let C2 = 1;
            const primes = generatePrimes(1000); // First 1000 primes
            for (let i = 1; i < primes.length; i++) { // Skip 2
                const p = primes[i];
                C2 *= (1 - 1/Math.pow(p-1, 2));
            }
            C2 *= 2; // Include the factor of 2

            // Calculate heuristic twin prime count
            const data = [];
            for (let x = 10; x <= maxX; x += Math.floor(x/50)) {
                const integral = approximateIntegral(x);
                const expected = 2 * C2 * integral;
                data.push({
                    x: x,
                    expected: expected,
                    C2: C2,
                    integral: integral
                });
            }
            
            return { C2: C2, data: data };
        }

        function approximateIntegral(x) {
            // Approximate ∫₂ˣ dt/(log t)²
            let sum = 0;
            const dt = 1;
            for (let t = 2; t <= x; t += dt) {
                sum += dt / Math.pow(Math.log(t), 2);
            }
            return sum;
        }

        function calculateDivisorSums(maxX) {
            const data = [];
            let cumulativeSum = 0;
            for (let n = 1; n <= maxX; n++) {
                const sigma_n = calculateSigma(n);
                cumulativeSum += sigma_n;
                const average = cumulativeSum / n;
                const expected = (Math.PI * Math.PI / 12) * n;
                data.push({
                    n: n,
                    sigma_n: sigma_n,
                    cumulative: cumulativeSum,
                    average: average,
                    expected: expected
                });
            }
            return data;
        }

        function calculateSigma(n) {
            let sum = 0;
            for (let i = 1; i <= Math.sqrt(n); i++) {
                if (n % i === 0) {
                    sum += i;
                    if (i !== n/i) {
                        sum += n/i;
                    }
                }
            }
            return sum;
        }

        function calculateModularSieve(modulus) {
            const residues = [];
            const admissible = [];
            
            for (let r = 0; r < modulus; r++) {
                const isAdmissible = checkAdmissible(r, modulus);
                residues.push({
                    r: r,
                    r_plus_2: (r + 2) % modulus,
                    admissible: isAdmissible,
                    angle: (2 * Math.PI * r) / modulus
                });
                if (isAdmissible) {
                    admissible.push(r);
                }
            }
            
            return {
                modulus: modulus,
                residues: residues,
                admissible: admissible,
                density: admissible.length / modulus
            };
        }

        function checkAdmissible(r, modulus) {
            // Check if (r, r+2) is admissible modulo all prime divisors of modulus
            const primeDivisors = getPrimeDivisors(modulus);
            for (const p of primeDivisors) {
                if (r % p === 0 || (r + 2) % p === 0) {
                    return false;
                }
            }
            return true;
        }

        function getPrimeDivisors(n) {
            const divisors = [];
            let d = 2;
            while (d * d <= n) {
                if (n % d === 0) {
                    divisors.push(d);
                    while (n % d === 0) {
                        n /= d;
                    }
                }
                d++;
            }
            if (n > 1) divisors.push(n);
            return divisors;
        }

        function generatePrimes(limit) {
            const primes = [2];
            for (let i = 3; primes.length < limit; i += 2) {
                let isPrime = true;
                for (const p of primes) {
                    if (p * p > i) break;
                    if (i % p === 0) {
                        isPrime = false;
                        break;
                    }
                }
                if (isPrime) primes.push(i);
            }
            return primes;
        }

        function updateCalculationsDisplay(harmonicData, twinPrimeData, divisorSumData, sieveData, modulus) {
            const calculationsDiv = document.getElementById('calculations');
            
            let html = `
                <h3>Step-by-Step Results</h3>
                
                <h4>1. Harmonic Numbers Calculation</h4>
                <p>Calculated H<sub>n</sub> for n = 1 to ${config.harmonicLimit}</p>
                <p>H<sub>${config.harmonicLimit}</sub> = ${harmonicData[harmonicData.length-1].H_n.toFixed(10)}</p>
                <p>ln(${config.harmonicLimit}) + γ = ${(Math.log(config.harmonicLimit) + 0.5772156649).toFixed(10)}</p>
                <p>Difference: ${(harmonicData[harmonicData.length-1].H_n - Math.log(config.harmonicLimit) - 0.5772156649).toFixed(10)}</p>
                
                <h4>2. Twin Prime Constant C₂</h4>
                <p>C₂ = 2 × ∏<sub>p>2</sub> (1 - 1/(p-1)²) = ${twinPrimeData.C2.toFixed(config.twinPrimePrecision)}</p>
                <p>Expected twin prime pairs up to x = ${config.maxX}: ${twinPrimeData.data[twinPrimeData.data.length-1].expected.toFixed(2)}</p>
                
                <h4>3. Modular Sieve Analysis (M = ${modulus})</h4>
                <p>Admissible residues: ${sieveData.admissible.join(', ')}</p>
                <p>Admissible density: ${sieveData.admissible.length} / ${modulus} = ${sieveData.density.toFixed(6)}</p>
                <p>Expected from Euler product: ${(1/(twinPrimeData.C2/2 * modulus)).toFixed(6)}</p>
                
                <h4>4. Divisor Sum Analysis</h4>
                <p>Average order of σ(n): (1/x)∑<sub>n≤x</sub> σ(n) ∼ (π²/12) x</p>
                <p>At x = ${config.maxX}: average = ${divisorSumData[divisorSumData.length-1].average.toFixed(2)}, expected = ${divisorSumData[divisorSumData.length-1].expected.toFixed(2)}</p>
            `;
            
            calculationsDiv.innerHTML = html;
        }

        function updateVisualizations(harmonicData, twinPrimeData, divisorSumData, sieveData) {
            // This is where you would implement D3.js visualizations
            // For this example, I'll create placeholder visualizations
            createModularSieveVisualization(sieveData);
            createHarmonicVisualization(harmonicData);
            createTwinPrimeVisualization(twinPrimeData);
            createDivisorSumVisualization(divisorSumData);
        }

        function createModularSieveVisualization(sieveData) {
            const svg = d3.select("#modularSievePlot")
                .html("")
                .append("svg")
                .attr("width", 400)
                .attr("height", 400);

            const center = { x: 200, y: 200 };
            const radius = 150;

            // Draw circle
            svg.append("circle")
                .attr("cx", center.x)
                .attr("cy", center.y)
                .attr("r", radius)
                .attr("fill", "none")
                .attr("stroke", "#34495e")
                .attr("stroke-width", 2);

            // Plot residues
            sieveData.residues.forEach(residue => {
                const angle = residue.angle;
                const x = center.x + radius * Math.cos(angle);
                const y = center.y + radius * Math.sin(angle);
                
                svg.append("circle")
                    .attr("cx", x)
                    .attr("cy", y)
                    .attr("r", config.pointSize)
                    .attr("fill", residue.admissible ? "#2ecc71" : "#e74c3c")
                    .attr("stroke", "#2c3e50")
                    .attr("stroke-width", 1);
                
                svg.append("text")
                    .attr("x", x + 8)
                    .attr("y", y + 4)
                    .attr("font-size", "10px")
                    .text(residue.r);
            });

            // Add legend
            svg.append("circle")
                .attr("cx", 50)
                .attr("cy", 350)
                .attr("r", 5)
                .attr("fill", "#2ecc71");
            svg.append("text")
                .attr("x", 60)
                .attr("y", 354)
                .attr("font-size", "12px")
                .text("Admissible");

            svg.append("circle")
                .attr("cx", 150)
                .attr("cy", 350)
                .attr("r", 5)
                .attr("fill", "#e74c3c");
            svg.append("text")
                .attr("x", 160)
                .attr("y", 354)
                .attr("font-size", "12px")
                .text("Not admissible");
        }

        function createHarmonicVisualization(harmonicData) {
            const svg = d3.select("#harmonicPlot")
                .html("")
                .append("svg")
                .attr("width", 400)
                .attr("height", 400);

            // Simple line plot implementation would go here
            svg.append("text")
                .attr("x", 200)
                .attr("y", 200)
                .attr("text-anchor", "middle")
                .text("Harmonic Numbers Visualization")
                .attr("fill", var(--text-color));
        }

        function createTwinPrimeVisualization(twinPrimeData) {
            const svg = d3.select("#twinPrimePlot")
                .html("")
                .append("svg")
                .attr("width", 400)
                .attr("height", 400);

            // Twin prime heuristic visualization
            svg.append("text")
                .attr("x", 200)
                .attr("y", 200)
                .attr("text-anchor", "middle")
                .text("Twin Prime Heuristic Visualization")
                .attr("fill", var(--text-color));
        }

        function createDivisorSumVisualization(divisorSumData) {
            const svg = d3.select("#divisorSumPlot")
                .html("")
                .append("svg")
                .attr("width", 400)
                .attr("height", 400);

            // Divisor sum visualization
            svg.append("text")
                .attr("x", 200)
                .attr("y", 200)
                .attr("text-anchor", "middle")
                .text("Divisor Sum Visualization")
                .attr("fill", var(--text-color));
        }

        function updateLARCHData(sieveData, modulus) {
            const larchDiv = document.getElementById('larchData');
            
            let html = `
                <h3>LARCH Search Region Data (M = ${modulus})</h3>
                <table>
                    <thead>
                        <tr>
                            <th>Residue r</th>
                            <th>r+2 mod M</th>
                            <th>Admissible</th>
                            <th>Angle (radians)</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            sieveData.residues.forEach(residue => {
                html += `
                    <tr>
                        <td>${residue.r}</td>
                        <td>${residue.r_plus_2}</td>
                        <td>${residue.admissible ? 'Yes' : 'No'}</td>
                        <td>${residue.angle.toFixed(4)}</td>
                    </tr>
                `;
            });
            
            html += `</tbody></table>`;
            larchDiv.innerHTML = html;
        }

        function exportCSV() {
            const modulus = config.modulusBase * Math.pow(2, config.powerOfTwo);
            const sieveData = calculateModularSieve(modulus);
            
            const csvData = sieveData.residues.map(residue => ({
                residue: residue.r,
                residue_plus_2: residue.r_plus_2,
                admissible: residue.admissible ? 1 : 0,
                angle: residue.angle
            }));
            
            const csv = Papa.unparse(csvData);
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `modular_sieve_M${modulus}_data.csv`;
            a.click();
            URL.revokeObjectURL(url);
        }

        function exportJPEG() {
            html2canvas(document.body).then(canvas => {
                const link = document.createElement('a');
                link.download = 'modular_sieve_visualization.jpg';
                link.href = canvas.toDataURL('image/jpeg', 0.9);
                link.click();
            });
        }
    </script>
</body>
</html>
