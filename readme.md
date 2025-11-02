<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amelia's Flashcard Study App</title>
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
            max-width: 700px;
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
        
        .content {
            padding: 30px 20px;
        }
        
        .file-upload-section {
            text-align: center;
            padding: 40px 20px;
        }
        
        .file-input-wrapper {
            display: inline-block;
            position: relative;
            margin: 20px 0;
        }
        
        .file-input-wrapper input[type="file"] {
            display: none;
        }
        
        .file-button {
            background: #667eea;
            color: white;
            padding: 15px 30px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            display: inline-block;
            transition: background 0.2s;
        }
        
        .file-button:hover {
            background: #5568d3;
        }
        
        .instructions {
            background: #f8f9fa;
            border-left: 4px solid #667eea;
            padding: 20px;
            margin: 20px 0;
            border-radius: 5px;
            font-size: 14px;
            line-height: 1.8;
        }
        
        .instructions h3 {
            margin-bottom: 10px;
            color: #667eea;
        }
        
        .instructions code {
            background: #e9ecef;
            padding: 2px 6px;
            border-radius: 3px;
            font-family: monospace;
        }
        
        .study-section {
            display: none;
        }
        
        .study-section.active {
            display: block;
        }
        
        .study-header {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .study-title {
            font-size: 24px;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        .stats {
            display: flex;
            justify-content: space-around;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            margin-bottom: 30px;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-value {
            font-size: 28px;
            font-weight: bold;
            color: #667eea;
        }
        
        .stat-label {
            font-size: 12px;
            color: #6c757d;
            margin-top: 5px;
        }
        
        .flashcard-container {
            perspective: 1000px;
            margin: 30px 0;
        }
        
        .flashcard {
            position: relative;
            width: 100%;
            min-height: 300px;
            cursor: pointer;
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        
        .flashcard.flipped {
            transform: rotateY(180deg);
        }
        
        .card-face {
            position: absolute;
            width: 100%;
            min-height: 300px;
            backface-visibility: hidden;
            border-radius: 15px;
            padding: 40px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .card-front {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .card-back {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            transform: rotateY(180deg);
        }
        
        .card-label {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 2px;
            opacity: 0.8;
            margin-bottom: 20px;
        }
        
        .card-text {
            font-size: 22px;
            line-height: 1.5;
        }
        
        .card-hint {
            margin-top: 30px;
            font-size: 14px;
            opacity: 0.8;
        }
        
        .controls {
            display: flex;
            gap: 10px;
            margin-top: 30px;
        }
        
        .button {
            flex: 1;
            padding: 15px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .button:active {
            transform: scale(0.95);
        }
        
        .button-know {
            background: #28a745;
            color: white;
        }
        
        .button-know:hover {
            background: #218838;
        }
        
        .button-review {
            background: #ffc107;
            color: #333;
        }
        
        .button-review:hover {
            background: #e0a800;
        }
        
        .button-next {
            background: #667eea;
            color: white;
        }
        
        .button-next:hover {
            background: #5568d3;
        }
        
        .button-secondary {
            background: #6c757d;
            color: white;
        }
        
        .button-secondary:hover {
            background: #5a6268;
        }
        
        .completion-screen {
            display: none;
            text-align: center;
            padding: 40px 20px;
        }
        
        .completion-screen.active {
            display: block;
        }
        
        .completion-icon {
            font-size: 80px;
            margin-bottom: 20px;
        }
        
        .completion-title {
            font-size: 32px;
            font-weight: bold;
            color: #28a745;
            margin-bottom: 10px;
        }
        
        .completion-message {
            font-size: 18px;
            color: #6c757d;
            margin-bottom: 30px;
        }
        
        .session-summary {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin: 30px 0;
        }
        
        .summary-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid #dee2e6;
        }
        
        .summary-item:last-child {
            border-bottom: none;
        }
        
        .no-cards {
            text-align: center;
            padding: 40px 20px;
            color: #6c757d;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📚 Amelia's Flashcard Study App</h1>
            <p>Load a study sheet and start learning</p>
        </div>
        
        <div class="content">
            <!-- File Upload Section -->
            <div class="file-upload-section" id="uploadSection">
                <h2>Choose Your Study Sheet</h2>
                <div class="file-input-wrapper">
                    <input type="file" id="fileInput" accept=".txt">
                    <label for="fileInput" class="file-button">📁 Select File</label>
                </div>
                
                <div class="instructions">
                    <h3>How to Format Your Study Sheet:</h3>
                    <p><strong>1.</strong> Create a text file (.txt) with your questions and answers</p>
                    <p><strong>2.</strong> Use this format:</p>
                    <pre style="background: #e9ecef; padding: 15px; border-radius: 5px; margin: 10px 0; overflow-x: auto;">
<code># Topic: Your Subject Here

Q: What is the capital of France?
A: Paris

Q: Who wrote Romeo and Juliet?
A: William Shakespeare

Q: What is 2 + 2?
A: 4</code></pre>
                    <p><strong>Tips:</strong></p>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li>Start with <code>#</code> for the topic/title</li>
                        <li>Each question starts with <code>Q:</code></li>
                        <li>Each answer starts with <code>A:</code></li>
                        <li>Leave a blank line between Q/A pairs</li>
                    </ul>
                </div>
            </div>
            
            <!-- Study Section -->
            <div class="study-section" id="studySection">
                <div class="study-header">
                    <div class="study-title" id="studyTitle">Study Session</div>
                    <button class="button button-secondary" onclick="loadNewFile()" style="margin-top: 10px; max-width: 200px;">📁 Load Different File</button>
                </div>
                
                <div class="stats">
                    <div class="stat">
                        <div class="stat-value" id="remaining">0</div>
                        <div class="stat-label">Remaining</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="mastered">0</div>
                        <div class="stat-label">Know It</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="reviewing">0</div>
                        <div class="stat-label">Review</div>
                    </div>
                </div>
                
                <div id="cardArea">
                    <!-- Flashcard will be inserted here -->
                </div>
                
                <div class="controls" id="controls">
                    <button class="button button-know" onclick="markKnow()">✓ Know It</button>
                    <button class="button button-review" onclick="markReview()">? Review Later</button>
                    <button class="button button-next" onclick="nextCard()">→ Next</button>
                </div>
            </div>
            
            <!-- Completion Section -->
            <div class="completion-screen" id="completionScreen">
                <div class="completion-icon">🎉</div>
                <div class="completion-title">Session Complete!</div>
                <div class="completion-message">You've reviewed all the cards</div>
                
                <div class="session-summary" id="sessionSummary">
                    <!-- Summary will be inserted here -->
                </div>
                
                <div class="controls">
                    <button class="button button-secondary" onclick="loadNewFile()">📁 Load Different File</button>
                    <button class="button button-next" onclick="reviewMissed()">🔄 Review Flagged Cards</button>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        let allCards = [];
        let activeCards = [];
        let currentCardIndex = 0;
        let currentFileName = '';
        let masteredCount = 0;
        let reviewCount = 0;
        let cardStates = {}; // Track card states
        
        // File input handler
        document.getElementById('fileInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;
            
            currentFileName = file.name;
            const reader = new FileReader();
            
            reader.onload = function(event) {
                const content = event.target.result;
                parseStudySheet(content);
            };
            
            reader.readAsText(file);
        });
        
        // Parse study sheet
        function parseStudySheet(content) {
            const lines = content.split('\n');
            const cards = [];
            let currentQ = '';
            let title = 'Study Session';
            
            for (let i = 0; i < lines.length; i++) {
                const line = lines[i].trim();
                
                // Check for title
                if (line.startsWith('#')) {
                    title = line.substring(1).trim();
                    continue;
                }
                
                // Check for question
                if (line.startsWith('Q:')) {
                    currentQ = line.substring(2).trim();
                    continue;
                }
                
                // Check for answer
                if (line.startsWith('A:') && currentQ) {
                    const answer = line.substring(2).trim();
                    cards.push({
                        question: currentQ,
                        answer: answer,
                        id: cards.length
                    });
                    currentQ = '';
                }
            }
            
            if (cards.length === 0) {
                alert('No cards found! Make sure your file uses the Q:/A: format.');
                return;
            }
            
            allCards = cards;
            loadProgress();
            startStudySession(title);
        }
        
        // Load progress from localStorage
        function loadProgress() {
            const savedStates = localStorage.getItem(`flashcards_${currentFileName}`);
            if (savedStates) {
                cardStates = JSON.parse(savedStates);
            } else {
                cardStates = {};
            }
            
            // Filter out mastered cards for active deck
            activeCards = allCards.filter(card => {
                const state = cardStates[card.id];
                return !state || state !== 'mastered';
            });
            
            // Shuffle active cards
            shuffleArray(activeCards);
        }
        
        // Save progress to localStorage
        function saveProgress() {
            localStorage.setItem(`flashcards_${currentFileName}`, JSON.stringify(cardStates));
        }
        
        // Start study session
        function startStudySession(title) {
            document.getElementById('uploadSection').style.display = 'none';
            document.getElementById('studySection').classList.add('active');
            document.getElementById('studyTitle').textContent = title;
            
            masteredCount = Object.values(cardStates).filter(s => s === 'mastered').length;
            reviewCount = Object.values(cardStates).filter(s => s === 'review').length;
            
            currentCardIndex = 0;
            showCard();
            updateStats();
        }
        
        // Show current card
        function showCard() {
            const cardArea = document.getElementById('cardArea');
            
            if (currentCardIndex >= activeCards.length) {
                showCompletion();
                return;
            }
            
            const card = activeCards[currentCardIndex];
            
            cardArea.innerHTML = `
                <div class="flashcard-container">
                    <div class="flashcard" id="flashcard" onclick="flipCard()">
                        <div class="card-face card-front">
                            <div class="card-label">Question</div>
                            <div class="card-text">${card.question}</div>
                            <div class="card-hint">Tap to reveal answer</div>
                        </div>
                        <div class="card-face card-back">
                            <div class="card-label">Answer</div>
                            <div class="card-text">${card.answer}</div>
                            <div class="card-hint">Tap to see question</div>
                        </div>
                    </div>
                </div>
            `;
        }
        
        // Flip card
        function flipCard() {
            document.getElementById('flashcard').classList.toggle('flipped');
        }
        
        // Mark as know
        function markKnow() {
            const card = activeCards[currentCardIndex];
            cardStates[card.id] = 'mastered';
            masteredCount++;
            saveProgress();
            nextCard();
        }
        
        // Mark for review
        function markReview() {
            const card = activeCards[currentCardIndex];
            if (cardStates[card.id] !== 'review') {
                cardStates[card.id] = 'review';
                reviewCount++;
            }
            saveProgress();
            nextCard();
        }
        
        // Next card
        function nextCard() {
            currentCardIndex++;
            showCard();
            updateStats();
        }
        
        // Update stats
        function updateStats() {
            const remaining = activeCards.length - currentCardIndex;
            document.getElementById('remaining').textContent = remaining;
            document.getElementById('mastered').textContent = masteredCount;
            document.getElementById('reviewing').textContent = reviewCount;
        }
        
        // Show completion screen
        function showCompletion() {
            document.getElementById('studySection').classList.remove('active');
            document.getElementById('completionScreen').classList.add('active');
            
            const total = allCards.length;
            const summary = `
                <div class="summary-item">
                    <span>Total Cards:</span>
                    <strong>${total}</strong>
                </div>
                <div class="summary-item">
                    <span>Know It:</span>
                    <strong style="color: #28a745;">${masteredCount}</strong>
                </div>
                <div class="summary-item">
                    <span>Flagged for Review:</span>
                    <strong style="color: #ffc107;">${reviewCount}</strong>
                </div>
                <div class="summary-item">
                    <span>Not Yet Seen:</span>
                    <strong>${total - masteredCount - reviewCount}</strong>
                </div>
            `;
            document.getElementById('sessionSummary').innerHTML = summary;
        }
        
        // Review missed cards
        function reviewMissed() {
            activeCards = allCards.filter(card => cardStates[card.id] === 'review');
            
            if (activeCards.length === 0) {
                alert('No cards flagged for review!');
                return;
            }
            
            shuffleArray(activeCards);
            currentCardIndex = 0;
            
            document.getElementById('completionScreen').classList.remove('active');
            document.getElementById('studySection').classList.add('active');
            
            showCard();
            updateStats();
        }
        
        // Load new file
        function loadNewFile() {
            document.getElementById('studySection').classList.remove('active');
            document.getElementById('completionScreen').classList.remove('active');
            document.getElementById('uploadSection').style.display = 'block';
            document.getElementById('fileInput').value = '';
        }
        
        // Shuffle array
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }
    </script>
</body>
</html>
