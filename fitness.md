layout: default
title: "fitness"
permalink: /9day

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>9-Day Training Tracker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px 20px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 5px;
        }
        
        .header p {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            padding: 20px;
            background: #f8f9fa;
            border-bottom: 1px solid #e9ecef;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #667eea;
        }
        
        .stat-label {
            font-size: 12px;
            color: #6c757d;
            margin-top: 5px;
        }
        
        .content {
            padding: 20px;
        }
        
        .day-section {
            margin-bottom: 25px;
            border-left: 4px solid #667eea;
            padding-left: 15px;
        }
        
        .day-section.hard {
            border-left-color: #dc3545;
        }
        
        .day-section.easy {
            border-left-color: #28a745;
        }
        
        .day-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .day-title {
            font-size: 18px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .day-badge {
            font-size: 10px;
            padding: 4px 8px;
            border-radius: 12px;
            font-weight: bold;
            text-transform: uppercase;
        }
        
        .day-badge.hard {
            background: #dc3545;
            color: white;
        }
        
        .day-badge.easy {
            background: #28a745;
            color: white;
        }
        
        .checklist-item {
            display: flex;
            align-items: flex-start;
            margin: 10px 0;
            padding: 10px;
            border-radius: 8px;
            transition: background 0.2s;
        }
        
        .checklist-item:hover {
            background: #f8f9fa;
        }
        
        .checklist-item.completed {
            opacity: 0.6;
        }
        
        .checklist-item.completed .item-text {
            text-decoration: line-through;
        }
        
        input[type="checkbox"] {
            width: 24px;
            height: 24px;
            margin-right: 12px;
            cursor: pointer;
            flex-shrink: 0;
            margin-top: 2px;
        }
        
        .item-text {
            flex: 1;
            line-height: 1.5;
            font-size: 15px;
        }
        
        .button {
            width: 100%;
            padding: 15px;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            margin-top: 10px;
            transition: background 0.2s;
        }
        
        .reset-button {
            background: #dc3545;
        }
        
        .reset-button:hover {
            background: #c82333;
        }
        
        .history-button {
            background: #6c757d;
        }
        
        .history-button:hover {
            background: #5a6268;
        }
        
        .button:active {
            transform: scale(0.98);
        }
        
        .cycle-info {
            background: #e7f3ff;
            border-left: 4px solid #667eea;
            padding: 15px;
            margin: 20px 0;
            border-radius: 5px;
        }
        
        .cycle-info strong {
            color: #667eea;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            overflow-y: auto;
        }
        
        .modal.active {
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .modal-content {
            background: white;
            border-radius: 20px;
            padding: 30px;
            max-width: 600px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .modal-title {
            font-size: 24px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .close-button {
            font-size: 30px;
            color: #6c757d;
            cursor: pointer;
            border: none;
            background: none;
            padding: 0;
            width: 30px;
            height: 30px;
            line-height: 1;
        }
        
        .close-button:hover {
            color: #2c3e50;
        }
        
        .history-item {
            background: #f8f9fa;
            border-left: 4px solid #667eea;
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
        }
        
        .history-date {
            font-weight: bold;
            color: #667eea;
            margin-bottom: 10px;
        }
        
        .history-stats {
            display: flex;
            gap: 20px;
            font-size: 14px;
            color: #6c757d;
        }
        
        .no-history {
            text-align: center;
            color: #6c757d;
            padding: 40px 20px;
            font-style: italic;
        }
        
        .note {
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 15px;
            margin: 20px 0;
            border-radius: 5px;
            font-size: 14px;
            line-height: 1.6;
        }
        
        .note strong {
            color: #856404;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏃 9-Day Training Cycle</h1>
            <p>Masters Runner Training Plan</p>
        </div>
        
        <div class="stats">
            <div class="stat">
                <div class="stat-value" id="completed-count">0</div>
                <div class="stat-label">Completed</div>
            </div>
            <div class="stat">
                <div class="stat-value" id="total-count">0</div>
                <div class="stat-label">Total Items</div>
            </div>
            <div class="stat">
                <div class="stat-value" id="progress-percent">0%</div>
                <div class="stat-label">Progress</div>
            </div>
        </div>
        
        <div class="content">
            <div class="cycle-info">
                <strong>Current Cycle:</strong> <span id="cycle-number">1</span><br>
                <strong>Started:</strong> <span id="cycle-start-date">Not started yet</span>
            </div>
            <!-- Day 1 -->
            <div class="day-section hard">
                <div class="day-header">
                    <div class="day-title">Day 1: Speed Workout</div>
                    <span class="day-badge hard">Hard</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day1-1">
                    <span class="item-text">Warm-up: 10-15 min easy + 5 min dynamic stretching</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day1-2">
                    <span class="item-text">4 × 100m strides</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day1-3">
                    <span class="item-text">Main: 6 × 400m at 8:45-9:15 pace (2-3 min recovery)</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day1-4">
                    <span class="item-text">Cool-down: 10 min easy</span>
                </div>
            </div>
            
            <!-- Day 2 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 2: Recovery</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day2-1">
                    <span class="item-text">Run the park loop OR rest OR cross-train</span>
                </div>
            </div>
            
            <!-- Day 3 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 3: Strength Training #1</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-1">
                    <span class="item-text">Warm-up: 5-10 min cardio + dynamic stretching</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-2">
                    <span class="item-text">Goblet squats/Bulgarian split squats: 3 × 8-10</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-3">
                    <span class="item-text">Single-leg Romanian deadlifts: 3 × 8-10 per leg</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-4">
                    <span class="item-text">Dumbbell bench press/push-ups: 3 × 8-12</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-5">
                    <span class="item-text">Single-arm rows: 3 × 8-10 per arm</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-6">
                    <span class="item-text">Walking lunges: 3 × 10-12 per leg</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-7">
                    <span class="item-text">Plank: 3 × 30-60 sec</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-8">
                    <span class="item-text">Side plank: 3 × 30 sec each side</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-9">
                    <span class="item-text">Calf raises: 3 × 15-20</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day3-10">
                    <span class="item-text">Cool-down: Stretching (hips, hamstrings, calves)</span>
                </div>
            </div>
            
            <!-- Day 4 -->
            <div class="day-section hard">
                <div class="day-header">
                    <div class="day-title">Day 4: Tempo Run</div>
                    <span class="day-badge hard">Hard</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day4-1">
                    <span class="item-text">Warm-up: 10-15 min easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day4-2">
                    <span class="item-text">Main: 20-25 min at comfortably hard (9:15-9:45/mile)</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day4-3">
                    <span class="item-text">Cool-down: 10 min easy + 4 × 100m strides</span>
                </div>
            </div>
            
            <!-- Day 5 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 5: Recovery</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day5-1">
                    <span class="item-text">Run the park loop OR complete rest</span>
                </div>
            </div>
            
            <!-- Day 6 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 6: Strength Training #2</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-1">
                    <span class="item-text">Warm-up: 5-10 min cardio + dynamic stretching</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-2">
                    <span class="item-text">Goblet squats/Bulgarian split squats: 3 × 8-10</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-3">
                    <span class="item-text">Single-leg Romanian deadlifts: 3 × 8-10 per leg</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-4">
                    <span class="item-text">Dumbbell bench press/push-ups: 3 × 8-12</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-5">
                    <span class="item-text">Single-arm rows: 3 × 8-10 per arm</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-6">
                    <span class="item-text">Walking lunges: 3 × 10-12 per leg</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-7">
                    <span class="item-text">Plank: 3 × 30-60 sec</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-8">
                    <span class="item-text">Side plank: 3 × 30 sec each side</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-9">
                    <span class="item-text">Calf raises: 3 × 15-20</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day6-10">
                    <span class="item-text">Cool-down: Stretching (hips, hamstrings, calves)</span>
                </div>
            </div>
            
            <!-- Day 7 -->
            <div class="day-section hard">
                <div class="day-header">
                    <div class="day-title">Day 7: Long Run</div>
                    <span class="day-badge hard">Hard</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day7-1">
                    <span class="item-text">10-12 miles at 10:30-11:00 pace</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day7-2">
                    <span class="item-text">Optional: 4 × 100m strides after</span>
                </div>
            </div>
            
            <!-- Day 8 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 8: Complete Rest</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day8-1">
                    <span class="item-text">Complete rest OR walking, yoga, foam rolling</span>
                </div>
            </div>
            
            <!-- Day 9 -->
            <div class="day-section easy">
                <div class="day-header">
                    <div class="day-title">Day 9: Easy Run + Strides</div>
                    <span class="day-badge easy">Easy</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day9-1">
                    <span class="item-text">Run the park loop</span>
                </div>
                <div class="checklist-item">
                    <input type="checkbox" data-id="day9-2">
                    <span class="item-text">4-6 × 100m strides at end</span>
                </div>
            </div>
            
            <div class="note">
                <strong>Note:</strong> This is a repeating 9-day cycle (3 mini-cycles of hard-easy-easy). After Day 9, start again at Day 1. Listen to your body and adjust as needed!
            </div>
            
            <button class="button history-button" onclick="showHistory()">📊 View History</button>
            <button class="button" style="background: #28a745;" onclick="exportToCalendar()">📅 Export to Calendar</button>
            <button class="button reset-button" onclick="resetAll()">🔄 Complete Cycle & Start New</button>
        </div>
    </div>
    
    <!-- History Modal -->
    <div class="modal" id="historyModal">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">📊 Training History</div>
                <button class="close-button" onclick="closeHistory()">&times;</button>
            </div>
            <div id="historyList"></div>
        </div>
    </div>
    
    <script>
        // Initialize cycle tracking
        function initializeCycle() {
            if (!localStorage.getItem('cycleNumber')) {
                localStorage.setItem('cycleNumber', '1');
            }
            if (!localStorage.getItem('cycleStartDate')) {
                localStorage.setItem('cycleStartDate', new Date().toISOString());
            }
            if (!localStorage.getItem('cycleHistory')) {
                localStorage.setItem('cycleHistory', JSON.stringify([]));
            }
            updateCycleDisplay();
        }
        
        // Update cycle display
        function updateCycleDisplay() {
            const cycleNumber = localStorage.getItem('cycleNumber') || '1';
            const cycleStartDate = localStorage.getItem('cycleStartDate');
            
            document.getElementById('cycle-number').textContent = cycleNumber;
            
            if (cycleStartDate) {
                const date = new Date(cycleStartDate);
                const formatted = date.toLocaleDateString('en-US', { 
                    month: 'short', 
                    day: 'numeric', 
                    year: 'numeric' 
                });
                document.getElementById('cycle-start-date').textContent = formatted;
            }
        }
        
        // Load saved state from localStorage
        function loadState() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            checkboxes.forEach(checkbox => {
                const saved = localStorage.getItem(checkbox.dataset.id);
                if (saved === 'true') {
                    checkbox.checked = true;
                    checkbox.closest('.checklist-item').classList.add('completed');
                }
            });
            updateStats();
        }
        
        // Save state to localStorage
        function saveState(checkbox) {
            localStorage.setItem(checkbox.dataset.id, checkbox.checked);
            if (checkbox.checked) {
                checkbox.closest('.checklist-item').classList.add('completed');
            } else {
                checkbox.closest('.checklist-item').classList.remove('completed');
            }
            updateStats();
        }
        
        // Update statistics
        function updateStats() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const total = checkboxes.length;
            const completed = Array.from(checkboxes).filter(cb => cb.checked).length;
            const percent = Math.round((completed / total) * 100);
            
            document.getElementById('completed-count').textContent = completed;
            document.getElementById('total-count').textContent = total;
            document.getElementById('progress-percent').textContent = percent + '%';
        }
        
        // Save current cycle to history and start new cycle
        function resetAll() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const total = checkboxes.length;
            const completed = Array.from(checkboxes).filter(cb => cb.checked).length;
            const percent = Math.round((completed / total) * 100);
            
            if (confirm(`Complete this cycle and start a new one?\n\nCurrent progress: ${completed}/${total} (${percent}%) will be saved to history.`)) {
                // Save to history
                const cycleNumber = parseInt(localStorage.getItem('cycleNumber') || '1');
                const cycleStartDate = localStorage.getItem('cycleStartDate');
                const cycleEndDate = new Date().toISOString();
                
                const history = JSON.parse(localStorage.getItem('cycleHistory') || '[]');
                history.push({
                    cycleNumber: cycleNumber,
                    startDate: cycleStartDate,
                    endDate: cycleEndDate,
                    completed: completed,
                    total: total,
                    percent: percent
                });
                localStorage.setItem('cycleHistory', JSON.stringify(history));
                
                // Reset all checkboxes
                checkboxes.forEach(checkbox => {
                    checkbox.checked = false;
                    localStorage.removeItem(checkbox.dataset.id);
                    checkbox.closest('.checklist-item').classList.remove('completed');
                });
                
                // Start new cycle
                localStorage.setItem('cycleNumber', (cycleNumber + 1).toString());
                localStorage.setItem('cycleStartDate', new Date().toISOString());
                
                updateStats();
                updateCycleDisplay();
                
                alert(`Cycle ${cycleNumber} saved to history!\n\nStarting Cycle ${cycleNumber + 1}...`);
            }
        }
        
        // Show history modal
        function showHistory() {
            const history = JSON.parse(localStorage.getItem('cycleHistory') || '[]');
            const historyList = document.getElementById('historyList');
            
            if (history.length === 0) {
                historyList.innerHTML = '<div class="no-history">No completed cycles yet. Complete your first cycle to see it here!</div>';
            } else {
                // Sort by cycle number descending (most recent first)
                history.sort((a, b) => b.cycleNumber - a.cycleNumber);
                
                historyList.innerHTML = history.map(cycle => {
                    const startDate = new Date(cycle.startDate).toLocaleDateString('en-US', { 
                        month: 'short', 
                        day: 'numeric', 
                        year: 'numeric' 
                    });
                    const endDate = new Date(cycle.endDate).toLocaleDateString('en-US', { 
                        month: 'short', 
                        day: 'numeric', 
                        year: 'numeric' 
                    });
                    
                    // Calculate duration in days
                    const duration = Math.round((new Date(cycle.endDate) - new Date(cycle.startDate)) / (1000 * 60 * 60 * 24));
                    
                    return `
                        <div class="history-item">
                            <div class="history-date">Cycle ${cycle.cycleNumber}</div>
                            <div class="history-stats">
                                <span>📅 ${startDate} - ${endDate}</span>
                                <span>⏱️ ${duration} days</span>
                                <span>✅ ${cycle.completed}/${cycle.total} (${cycle.percent}%)</span>
                            </div>
                        </div>
                    `;
                }).join('');
            }
            
            document.getElementById('historyModal').classList.add('active');
        }
        
        // Close history modal
        function closeHistory() {
            document.getElementById('historyModal').classList.remove('active');
        }
        
        // Close modal when clicking outside
        document.getElementById('historyModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeHistory();
            }
        });
        
        // Export to calendar (ICS file)
        function exportToCalendar() {
            const cycleNumber = localStorage.getItem('cycleNumber') || '1';
            const startDate = new Date(localStorage.getItem('cycleStartDate') || new Date());
            
            // Ask user for start date
            const userDate = prompt(
                `Export Cycle ${cycleNumber} to calendar\n\nEnter start date (YYYY-MM-DD) or leave blank for today:`,
                startDate.toISOString().split('T')[0]
            );
            
            if (userDate === null) return; // User cancelled
            
            // Parse the date correctly - set time to noon to avoid timezone issues
            const baseDate = userDate ? new Date(userDate + 'T12:00:00') : new Date();
            baseDate.setHours(12, 0, 0, 0); // Set to noon to avoid any timezone shifts
            
            // Training days data
            const days = [
                {
                    day: 1,
                    title: "Day 1: Speed Workout",
                    description: "Warm-up: 10-15 min easy + 5 min dynamic stretching\\n4 × 100m strides\\nMain: 6 × 400m at 8:45-9:15 pace (2-3 min recovery)\\nCool-down: 10 min easy\\n\\nTotal: ~5 miles",
                    duration: 1
                },
                {
                    day: 2,
                    title: "Day 2: Recovery",
                    description: "Run the park loop OR rest OR cross-train",
                    duration: 1
                },
                {
                    day: 3,
                    title: "Day 3: Strength Training #1",
                    description: "Warm-up: 5-10 min cardio + dynamic stretching\\nGoblet squats/Bulgarian split squats: 3 × 8-10\\nSingle-leg Romanian deadlifts: 3 × 8-10 per leg\\nDumbbell bench press/push-ups: 3 × 8-12\\nSingle-arm rows: 3 × 8-10 per arm\\nWalking lunges: 3 × 10-12 per leg\\nPlank: 3 × 30-60 sec\\nSide plank: 3 × 30 sec each side\\nCalf raises: 3 × 15-20\\nCool-down: Stretching",
                    duration: 1
                },
                {
                    day: 4,
                    title: "Day 4: Tempo Run",
                    description: "Warm-up: 10-15 min easy\\nMain: 20-25 min at comfortably hard (9:15-9:45/mile)\\nCool-down: 10 min easy + 4 × 100m strides\\n\\nTotal: ~5-6 miles",
                    duration: 1
                },
                {
                    day: 5,
                    title: "Day 5: Recovery",
                    description: "Run the park loop OR complete rest",
                    duration: 1
                },
                {
                    day: 6,
                    title: "Day 6: Strength Training #2",
                    description: "Warm-up: 5-10 min cardio + dynamic stretching\\nGoblet squats/Bulgarian split squats: 3 × 8-10\\nSingle-leg Romanian deadlifts: 3 × 8-10 per leg\\nDumbbell bench press/push-ups: 3 × 8-12\\nSingle-arm rows: 3 × 8-10 per arm\\nWalking lunges: 3 × 10-12 per leg\\nPlank: 3 × 30-60 sec\\nSide plank: 3 × 30 sec each side\\nCalf raises: 3 × 15-20\\nCool-down: Stretching",
                    duration: 1
                },
                {
                    day: 7,
                    title: "Day 7: Long Run",
                    description: "10-12 miles at 10:30-11:00 pace\\nOptional: 4 × 100m strides after",
                    duration: 2
                },
                {
                    day: 8,
                    title: "Day 8: Complete Rest",
                    description: "Complete rest OR walking, yoga, foam rolling",
                    duration: 1
                },
                {
                    day: 9,
                    title: "Day 9: Easy Run + Strides",
                    description: "Run the park loop\\n4-6 × 100m strides at end",
                    duration: 1
                }
            ];
            
            // Generate ICS content
            let icsContent = 'BEGIN:VCALENDAR\r\n';
            icsContent += 'VERSION:2.0\r\n';
            icsContent += 'PRODID:-//Training Tracker//10-Day Cycle//EN\r\n';
            icsContent += 'CALSCALE:GREGORIAN\r\n';
            icsContent += 'METHOD:PUBLISH\r\n';
            icsContent += `X-WR-CALNAME:Training Cycle ${cycleNumber}\r\n`;
            icsContent += 'X-WR-TIMEZONE:America/New_York\r\n';
            
            days.forEach(day => {
                // Create a new date object for each event
                const eventDate = new Date(baseDate.getTime());
                eventDate.setDate(eventDate.getDate() + (day.day - 1));
                
                const year = eventDate.getFullYear();
                const month = String(eventDate.getMonth() + 1).padStart(2, '0');
                const date = String(eventDate.getDate()).padStart(2, '0');
                
                // Set event time (7:00 AM for morning workouts)
                const startTime = `${year}${month}${date}T070000`;
                
                // Calculate end time based on duration
                const endDate = new Date(eventDate.getTime());
                endDate.setHours(7 + day.duration, 0, 0, 0);
                const endYear = endDate.getFullYear();
                const endMonth = String(endDate.getMonth() + 1).padStart(2, '0');
                const endDay = String(endDate.getDate()).padStart(2, '0');
                const endHour = String(endDate.getHours()).padStart(2, '0');
                const endTime = `${endYear}${endMonth}${endDay}T${endHour}0000`;
                
                // Create unique ID
                const uid = `day${day.day}-cycle${cycleNumber}-${Date.now()}-${day.day}@trainingtracker`;
                
                icsContent += 'BEGIN:VEVENT\r\n';
                icsContent += `UID:${uid}\r\n`;
                icsContent += `DTSTART:${startTime}\r\n`;
                icsContent += `DTEND:${endTime}\r\n`;
                icsContent += `DTSTAMP:${new Date().toISOString().replace(/[-:]/g, '').split('.')[0]}Z\r\n`;
                icsContent += `SUMMARY:${day.title}\r\n`;
                icsContent += `DESCRIPTION:${day.description}\r\n`;
                icsContent += `LOCATION:\r\n`;
                icsContent += `STATUS:CONFIRMED\r\n`;
                icsContent += `SEQUENCE:0\r\n`;
                
                // Add alarm (30 min before)
                icsContent += 'BEGIN:VALARM\r\n';
                icsContent += 'TRIGGER:-PT30M\r\n';
                icsContent += 'ACTION:DISPLAY\r\n';
                icsContent += `DESCRIPTION:${day.title} starts in 30 minutes\r\n`;
                icsContent += 'END:VALARM\r\n';
                
                icsContent += 'END:VEVENT\r\n';
            });
            
            icsContent += 'END:VCALENDAR\r\n';
            
            // Create and download file
            const blob = new Blob([icsContent], { type: 'text/calendar;charset=utf-8' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `training-cycle-${cycleNumber}.ics`;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            alert(`Calendar file created!\n\nCycle ${cycleNumber} exported starting ${baseDate.toLocaleDateString()}\n\nOpen the downloaded file to add these events to your calendar.\n\nNote: Events start at 7:00 AM by default. You can edit the times in your calendar app.`);
        }
        
        // Add event listeners
        document.querySelectorAll('input[type="checkbox"]').forEach(checkbox => {
            checkbox.addEventListener('change', function() {
                saveState(this);
            });
        });
        
        // Load state on page load
        initializeCycle();
        loadState();
    </script>
</body>
