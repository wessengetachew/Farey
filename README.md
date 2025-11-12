
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Rings: GCD Channels & Farey Sequences</title>
    <style>
        /* [Keep all your existing CSS styles - they're good!] */
        /* Only adding a few new responsive styles */
        
        .mobile-warning {
            display: none;
            background: #ff9900;
            color: #000;
            padding: 10px;
            text-align: center;
            font-weight: bold;
            border-bottom: 2px solid #ff6600;
        }
        
        @media (max-width: 768px) {
            .mobile-warning {
                display: block;
            }
            
            .control-panel {
                max-height: 50vh;
                font-size: 12px;
            }
            
            .header h1 {
                font-size: 24px;
            }
            
            .header .subtitle {
                font-size: 14px;
            }
            
            .floating-update-btn, .floating-center-btn, .floating-export-btn {
                padding: 10px 15px;
                font-size: 12px;
                bottom: 10px;
                right: 10px;
            }
            
            .floating-center-btn {
                bottom: 60px;
            }
            
            .export-png {
                bottom: 110px;
            }
            
            .export-csv {
                bottom: 160px;
            }
        }
        
        @media (max-width: 480px) {
            .control-row {
                grid-template-columns: 1fr;
            }
            
            .preset-grid {
                grid-template-columns: 1fr;
            }
            
            .tab {
                padding: 10px 5px;
                font-size: 12px;
            }
        }

        .loading-overlay {
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
            color: white;
            font-size: 18px;
            flex-direction: column;
        }

        .loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #00ff00;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin-bottom: 15px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="mobile-warning">
        For best experience, use desktop or tablet in landscape mode
    </div>
    
    <div class="container">
        <!-- [Keep all your existing HTML structure] -->
        <!-- Only adding loading overlay -->
        <div class="loading-overlay" id="loadingOverlay" style="display: none;">
            <div class="loading-spinner"></div>
            <div id="loadingText">Computing points...</div>
            <div id="loadingProgress" style="margin-top: 10px; font-size: 14px;"></div>
        </div>
        
        <!-- Rest of your HTML remains the same -->
    </div>

    <script>
        // Performance constants
        const COMPUTE_CHUNK_SIZE = 1000;
        const MAX_POINTS_FOR_REALTIME = 5000;
        const MAX_POINTS_FOR_CONNECTIONS = 3000;

        // Cache variables
        let cachedPointBatches = null;
        let cachedStaticCanvas = null;
        let lastDrawSettings = null;
        let needsFullRedraw = true;
        let isComputing = false;

        // Initialize everything when page loads
        window.addEventListener('load', function() {
            initializeTheme();
            initializeEventListeners();
            updateRangeDisplays();
            updateGapColorPickers();
            updateModuliDisplay();
            
            // Load with default settings
            setTimeout(() => {
                updateVisualization();
            }, 100);
        });

        function initializeEventListeners() {
            // Add real-time updates for key controls
            const realTimeControls = [
                'globalSpeed', 'globalSpeedNum', 'modRotSpeed', 'modRotSpeedNum',
                'perRingRot', 'perRingRotNum', 'pointSize', 'pointSizeNum',
                'connOpacity', 'connOpacityNum', 'trackerSize', 'trackerSizeNum',
                'showOpen', 'showClosed', 'showRingLines', 'enableConnections',
                'enableTracker', 'enableGapAnalysis', 'showGapLines',
                'invertModOrder', 'displayMode', 'angularMapping'
            ];

            realTimeControls.forEach(controlId => {
                const element = document.getElementById(controlId);
                if (element) {
                    element.addEventListener('input', handleRealtimeUpdate);
                }
            });

            // Performance mode change
            document.getElementById('performanceMode').addEventListener('change', () => {
                needsFullRedraw = true;
                drawVisualization();
            });

            // Color scheme changes
            document.getElementById('openColorMode').addEventListener('change', () => {
                needsFullRedraw = true;
                drawVisualization();
            });

            document.getElementById('closedColorMode').addEventListener('change', () => {
                needsFullRedraw = true;
                drawVisualization();
            });

            // Connection mode changes
            document.getElementById('connectionMode').addEventListener('change', function() {
                updateConnectionModeUI();
                needsFullRedraw = true;
                drawVisualization();
            });

            // Theme toggle
            document.querySelector('.theme-toggle').addEventListener('click', toggleTheme);
        }

        function handleRealtimeUpdate() {
            if (pointsData.length > MAX_POINTS_FOR_REALTIME) {
                // For large datasets, don't update in real-time
                return;
            }
            
            updateRangeDisplays();
            needsFullRedraw = true;
            
            // Start animation if rotation controls are changed
            if (this.id.includes('Speed') && document.getElementById('autoRotate').checked) {
                autoStartAnimation();
            }
            
            drawVisualization();
            
            // Update tracker info if tracker is active
            if (document.getElementById('enableTracker').checked) {
                updateTrackerInfo();
            }
        }

        function updateConnectionModeUI() {
            const mode = document.getElementById('connectionMode').value;
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
        }

        function showLoading(message = "Computing points...") {
            document.getElementById('loadingOverlay').style.display = 'flex';
            document.getElementById('loadingText').textContent = message;
            document.getElementById('loadingProgress').textContent = '';
        }

        function hideLoading() {
            document.getElementById('loadingOverlay').style.display = 'none';
        }

        function updateLoadingProgress(current, total, mod) {
            const percent = Math.round((current / total) * 100);
            document.getElementById('loadingProgress').textContent = 
                `${current.toLocaleString()} / ${total.toLocaleString()} points (${percent}%) - m=${mod}`;
        }

        // Enhanced point computation with better progress tracking
        async function computePointsProgressiveFromList(moduli, gaps, angularMapping) {
            pointsData = [];
            pointsByModulus = {};
            ringMetadata = [];
            
            let totalOpen = 0;
            let totalClosed = 0;
            let sumPhiOverM = 0;
            let countModuli = 0;
            let processedCount = 0;
            let totalExpectedPoints = moduli.reduce((sum, m) => sum + m, 0);

            showLoading("Computing modular points...");

            // Pre-compute ring metadata
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
                
                pointsByModulus[m] = {};
                const phiM = phi(m);
                sumPhiOverM += phiM / m;
                countModuli++;

                for (let r = 0; r < m; r++) {
                    const g = gcd(r, m);
                    const isOpen = g === 1;
                    
                    if (isOpen) totalOpen++;
                    else totalClosed++;

                    let angle;
                    switch(angularMapping) {
                        case 'standard': angle = (2 * Math.PI * r) / m; break;
                        case 'half': angle = (Math.PI * r) / m; break;
                        case 'inverted': angle = (2 * Math.PI * (m - r)) / m; break;
                        case 'negative': angle = -(2 * Math.PI * r) / m; break;
                        default: angle = (2 * Math.PI * r) / m;
                    }

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
                    pointsByModulus[m][r] = point;
                    processedCount++;

                    // Update progress more efficiently
                    if (processedCount % 5000 === 0) {
                        updateLoadingProgress(processedCount, totalExpectedPoints, m);
                        await new Promise(resolve => setTimeout(resolve, 0));
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

            hideLoading();
            return { totalOpen, totalClosed, avgPhiOverM, countModuli };
        }

        // Enhanced visualization with better performance
        function drawVisualization() {
            if (pointsData.length === 0) return;

            const performanceMode = document.getElementById('performanceMode').checked;
            const enableConnections = document.getElementById('enableConnections').checked;
            const showGapLines = document.getElementById('showGapLines').checked;
            const enableGap = document.getElementById('enableGapAnalysis').checked;

            // Skip connections for very large datasets
            if (pointsData.length > MAX_POINTS_FOR_CONNECTIONS) {
                if (enableConnections || (showGapLines && enableGap)) {
                    console.log("Skipping connections for large dataset");
                }
            }

            if (performanceMode) {
                drawVisualizationOptimized();
            } else {
                drawVisualizationStandard();
            }
        }

        // Optimized drawing with better batching
        function drawVisualizationOptimized() {
            const width = canvas.width;
            const height = canvas.height;
            const centerX = width / 2;
            const centerY = height / 2;

            // Check if we need full redraw
            const currentSettings = getCurrentSettingsHash();
            
            if (currentSettings !== lastDrawSettings || needsFullRedraw) {
                cachedPointBatches = batchPointsByColor();
                drawStaticElementsToCache();
                lastDrawSettings = currentSettings;
                needsFullRedraw = false;
            }

            // Clear canvas with theme background
            ctx.clearRect(0, 0, width, height);
            ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--bg-primary');
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

            const maxRadius = Math.min(width, height) * 0.4;
            const radiusScale = displayMode === 'unit' ? maxRadius : maxRadius / Math.max(...pointsData.map(p => p.m));

            // Draw connection lines (if enabled and dataset isn't too large)
            if (enableConnections && pointsData.length < MAX_POINTS_FOR_CONNECTIONS) {
                drawConnectionLines(radiusScale, displayMode);
            }

            // Draw gap lines (if enabled and dataset isn't too large)
            if (showGapLines && enableGap && pointsData.length < MAX_POINTS_FOR_CONNECTIONS) {
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

            // Draw labels (skip if too many points)
            const showLabels = document.getElementById('showLabels').checked;
            if (showLabels && pointsData.length < 2000) {
                drawLabels(radiusScale, displayMode, showOpen, showClosed, pointSize);
            }

            ctx.restore();
        }

        function getCurrentSettingsHash() {
            return JSON.stringify({
                displayMode: document.getElementById('displayMode').value,
                showOpen: document.getElementById('showOpen').checked,
                showClosed: document.getElementById('showClosed').checked,
                showRingLines: document.getElementById('showRingLines').checked,
                pointSize: document.getElementById('pointSize').value,
                baseOpenColor: document.getElementById('baseOpenColor').value,
                baseClosedColor: document.getElementById('baseClosedColor').value,
                openColorMode: document.getElementById('openColorMode').value,
                invertOrder: document.getElementById('invertModOrder').checked,
                pointsLength: pointsData.length,
                theme: currentTheme
            });
        }

        function drawStaticElementsToCache() {
            if (!cachedStaticCanvas) {
                cachedStaticCanvas = document.createElement('canvas');
                cachedStaticCanvas.width = canvas.width;
                cachedStaticCanvas.height = canvas.height;
            }
            
            const staticCtx = cachedStaticCanvas.getContext('2d');
            const width = cachedStaticCanvas.width;
            const height = cachedStaticCanvas.height;
            const centerX = width / 2;
            const centerY = height / 2;

            staticCtx.clearRect(0, 0, width, height);
            
            const showRingLines = document.getElementById('showRingLines').checked;
            const displayMode = document.getElementById('displayMode').value;
            
            if (showRingLines && displayMode === 'rings') {
                staticCtx.save();
                staticCtx.translate(centerX + transform.x, centerY + transform.y);
                staticCtx.scale(transform.scale, transform.scale);
                staticCtx.rotate(globalRotation * Math.PI / 180);
                
                staticCtx.strokeStyle = getComputedStyle(document.body).getPropertyValue('--ring-line-color');
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

        // Enhanced color generation
        function getColorForPoint(point, isOpen) {
            if (isOpen) {
                const mode = document.getElementById('openColorMode').value;
                if (mode === 'solid') return document.getElementById('baseOpenColor').value;
                
                let hue = 0;
                const sat = 80, light = 60;
                
                if (mode === 'by-residue') {
                    const maxR = Math.max(...pointsData.map(p => p.r));
                    hue = maxR > 0 ? (point.r / maxR) * 360 : 0;
                } else if (mode === 'by-modulus') {
                    const maxM = Math.max(...pointsData.map(p => p.m));
                    hue = (point.m / maxM) * 360;
                } else if (mode === 'by-spf') {
                    const spf = smallestPrimeFactor(point.r === 0 ? point.m : point.r);
                    const primeMap = {2: 0, 3: 30, 5: 60, 7: 90, 11: 120, 13: 150, 17: 180};
                    hue = primeMap[spf] || ((spf * 13) % 360);
                } else if (mode === 'by-angle') {
                    hue = (point.angle / (2 * Math.PI)) * 360;
                } else if (mode === 'by-prime-power') {
                    // Color by prime power structure
                    hue = (point.m * 17 + point.r * 13) % 360;
                }
                
                const [r, g, b] = hslToRgb(hue, sat, light);
                return `rgb(${r},${g},${b})`;
            } else {
                const mode = document.getElementById('closedColorMode').value;
                if (mode === 'solid') return document.getElementById('baseClosedColor').value;
                
                // Different coloring for closed channels
                let hue = 0;
                const sat = 60, light = 40;
                
                if (mode === 'by-gcd') {
                    hue = (point.gcd * 50) % 360;
                } else if (mode === 'by-spf') {
                    const spf = smallestPrimeFactor(point.gcd);
                    hue = (spf * 60) % 360;
                } else if (mode === 'by-modulus') {
                    const maxM = Math.max(...pointsData.map(p => p.m));
                    hue = (point.m / maxM) * 360;
                }
                
                const [r, g, b] = hslToRgb(hue, sat, light);
                return `rgb(${r},${g},${b})`;
            }
        }

        // Enhanced animation system
        function animate() {
            if (!animationId) return;

            const globalSpeed = parseFloat(document.getElementById('globalSpeed').value);
            const modRotSpeed = parseFloat(document.getElementById('modRotSpeed').value);
            const speedGradient = document.getElementById('speedGradient').value;
            const gradientStrength = parseFloat(document.getElementById('gradientStrength').value);

            // Update rotations
            globalRotation += globalSpeed;
            if (globalRotation >= 360) globalRotation -= 360;
            if (globalRotation < 0) globalRotation += 360;

            // Update modulus rotations with gradient
            const moduli = Object.keys(modRotations);
            if (moduli.length > 0) {
                const minMod = Math.min(...moduli.map(Number));
                const maxMod = Math.max(...moduli.map(Number));
                const modRange = maxMod - minMod;

                moduli.forEach(m => {
                    let speed = modRotSpeed;
                    
                    if (speedGradient === 'inner-to-outer' && modRange > 0) {
                        const factor = (Number(m) - minMod) / modRange;
                        speed = modRotSpeed * (1 + factor * gradientStrength);
                    } else if (speedGradient === 'outer-to-inner' && modRange > 0) {
                        const factor = (maxMod - Number(m)) / modRange;
                        speed = modRotSpeed * (1 + factor * gradientStrength);
                    }
                    
                    modRotations[m] += speed;
                    if (modRotations[m] >= 360) modRotations[m] -= 360;
                    if (modRotations[m] < 0) modRotations[m] += 360;
                });
            }

            drawVisualization();
            animationId = requestAnimationFrame(animate);
        }

        // Enhanced update function with better error handling
        function updateVisualization() {
            if (isComputing) {
                console.log("Computation in progress, please wait...");
                return;
            }

            const moduli = getSelectedModuli();
            if (moduli.length === 0) {
                alert('No valid moduli selected. Please check your input.');
                return;
            }

            // Check for extremely large datasets
            const totalExpectedPoints = moduli.reduce((sum, m) => sum + m, 0);
            if (totalExpectedPoints > 100000) {
                const proceed = confirm(`This will generate approximately ${totalExpectedPoints.toLocaleString()} points, which may slow down your browser. Continue?`);
                if (!proceed) return;
            }

            isComputing = true;
            needsFullRedraw = true;
            cachedPointBatches = null;
            cachedStaticCanvas = null;
            lastDrawSettings = null;

            // Try to load from cache first
            if (loadFromCache()) {
                isComputing = false;
                progressiveRender();
                updateModuliDisplay();
                return;
            }

            const enableGap = document.getElementById('enableGapAnalysis').checked;
            const gapInput = document.getElementById('gapValues').value;
            const gaps = gapInput.split(',').map(g => parseInt(g.trim())).filter(g => !isNaN(g) && g > 0);
            const angularMapping = document.getElementById('angularMapping').value;

            // Use progressive computation for better UX
            computePointsProgressiveFromList(moduli, enableGap ? gaps : [], angularMapping)
                .then(() => {
                    isComputing = false;
                    saveToCache();
                    drawVisualization();
                    updateTrackerInfo();
                })
                .catch(error => {
                    isComputing = false;
                    hideLoading();
                    console.error("Computation error:", error);
                    alert("Error computing points: " + error.message);
                });
        }

        // Enhanced mobile support
        function handleTouchMove(e) {
            if (e.touches && e.touches.length === 2) {
                // Pinch zoom
                e.preventDefault();
                const dx = e.touches[0].clientX - e.touches[1].clientX;
                const dy = e.touches[0].clientY - e.touches[1].clientY;
                const dist = Math.sqrt(dx * dx + dy * dy);
                
                if (touchStartDist > 0) {
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
                } else {
                    touchStartDist = dist;
                }
            } else if (isDragging) {
                // Pan
                const coords = getEventCoords(e);
                transform.x += coords.x - lastMouseX;
                transform.y += coords.y - lastMouseY;
                lastMouseX = coords.x;
                lastMouseY = coords.y;
                drawVisualization();
            }
        }

        // Add this new function for better tooltip management
        function updateTooltip(coords, foundPoint) {
            if (foundPoint) {
                tooltip.style.opacity = '1';
                tooltip.style.left = (coords.x + 15) + 'px';
                tooltip.style.top = (coords.y + 15) + 'px';
                
                const [reducedNum, reducedDen] = reduceFraction(foundPoint.r, foundPoint.m);
                const fareyInfo = reducedNum !== foundPoint.r ? 
                    ` = ${reducedNum}/${reducedDen} (reduced)` : '';
                
                tooltip.innerHTML = `
                    <strong>Modulus m = ${foundPoint.m}</strong><br>
                    <strong>Residue r = ${foundPoint.r}</strong><br>
                    Farey: ${foundPoint.r}/${foundPoint.m}${fareyInfo}<br>
                    gcd(${foundPoint.r}, ${foundPoint.m}) = ${foundPoint.gcd}<br>
                    Channel: <strong>${foundPoint.isOpen ? 'OPEN' : 'CLOSED'}</strong><br>
                    φ(${foundPoint.m}) = ${foundPoint.phiM}<br>
                    Angle: ${(foundPoint.angle * 180 / Math.PI).toFixed(2)}°
                    ${foundPoint.isAdmissible ? `<br><strong style="color: #ff00ff;">GAP ADMISSIBLE</strong>` : ''}
                `;
                canvas.style.cursor = 'pointer';
            } else {
                tooltip.style.opacity = '0';
                canvas.style.cursor = isDragging ? 'grabbing' : 'grab';
            }
        }

        // Keep all your existing utility functions (gcd, phi, hslToRgb, etc.)
        // They are working well!

        // Add this helper for better color handling
        function getThemeColors() {
            return {
                bgPrimary: getComputedStyle(document.body).getPropertyValue('--bg-primary').trim(),
                textPrimary: getComputedStyle(document.body).getPropertyValue('--text-primary').trim(),
                ringLineColor: getComputedStyle(document.body).getPropertyValue('--ring-line-color').trim(),
                connectionLineColor: getComputedStyle(document.body).getPropertyValue('--connection-line-color').trim()
            };
        }

        // Initialize the rest of your existing code...
        // [All your existing variable declarations and function definitions]

    </script>
</body>
</html>
