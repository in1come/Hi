<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nova - Search Engine</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #4285f4;
            --secondary-color: #34a853;
            --accent-color: #ea4335;
            --text-color: #202124;
            --light-text: #5f6368;
            --border-color: #dfe1e5;
            --bg-color: #ffffff;
            --hover-bg: #f8f9fa;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            color: var(--text-color);
            background-color: var(--bg-color);
            min-height: 100vh;
        }

        header {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding: 15px 20px;
        }

        .nav-links {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .nav-links a {
            color: var(--text-color);
            text-decoration: none;
            font-size: 13px;
        }

        .nav-links a:hover {
            text-decoration: underline;
        }

        .nav-links .apps-icon {
            font-size: 20px;
            color: var(--light-text);
            padding: 8px;
            border-radius: 50%;
        }

        .nav-links .apps-icon:hover {
            background-color: var(--hover-bg);
        }

        .nav-links .sign-in {
            background-color: var(--primary-color);
            color: white;
            padding: 8px 15px;
            border-radius: 4px;
            font-weight: 500;
        }

        .search-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }

        .logo {
            font-size: 80px;
            font-weight: bold;
            margin-bottom: 30px;
            color: var(--primary-color);
            text-align: center;
        }

        .search-box {
            width: 100%;
            position: relative;
            margin-bottom: 30px;
        }

        .search-input {
            width: 100%;
            padding: 12px 50px 12px 45px;
            border-radius: 24px;
            border: 1px solid var(--border-color);
            font-size: 16px;
            outline: none;
            box-shadow: 0 1px 6px rgba(32, 33, 36, 0.1);
        }

        .search-input:hover, .search-input:focus {
            box-shadow: 0 1px 6px rgba(32, 33, 36, 0.2);
        }

        .search-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--light-text);
        }

        .voice-icon, .camera-icon {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--primary-color);
            cursor: pointer;
        }

        .camera-icon {
            right: 50px;
        }

        .search-buttons {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }

        .search-btn {
            background-color: #f8f9fa;
            border: 1px solid #f8f9fa;
            border-radius: 4px;
            color: #3c4043;
            padding: 8px 16px;
            font-size: 14px;
            cursor: pointer;
        }

        .search-btn:hover {
            border: 1px solid var(--border-color);
            box-shadow: 0 1px 1px rgba(0,0,0,0.1);
        }

        .search-tabs {
            display: flex;
            border-bottom: 1px solid var(--border-color);
            width: 100%;
            margin-bottom: 20px;
        }

        .search-tab {
            padding: 10px 15px;
            cursor: pointer;
            color: var(--light-text);
            font-size: 14px;
            position: relative;
        }

        .search-tab.active {
            color: var(--primary-color);
        }

        .search-tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 3px;
            background-color: var(--primary-color);
        }

        .search-results {
            width: 100%;
        }

        .result-item {
            margin-bottom: 25px;
            max-width: 600px;
        }

        .result-url {
            color: #202124;
            font-size: 14px;
            margin-bottom: 5px;
            display: flex;
            align-items: center;
        }

        .result-favicon {
            width: 16px;
            height: 16px;
            margin-right: 5px;
        }

        .result-title {
            color: #1a0dab;
            font-size: 20px;
            margin-bottom: 5px;
            text-decoration: none;
            display: inline-block;
        }

        .result-title:hover {
            text-decoration: underline;
        }

        .result-description {
            color: #4d5156;
            font-size: 14px;
            line-height: 1.5;
        }

        .image-results {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .image-item {
            border-radius: 8px;
            overflow: hidden;
            height: 200px;
            position: relative;
        }

        .image-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .image-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(0,0,0,0.5);
            color: white;
            padding: 8px;
            font-size: 12px;
        }

        .translate-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }

        .translate-box {
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 15px;
        }

        .translate-textarea {
            width: 100%;
            min-height: 100px;
            border: none;
            resize: none;
            outline: none;
            font-size: 16px;
        }

        .translate-languages {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .translate-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
        }

        .ai-chat-container {
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 15px;
            margin-top: 20px;
        }

        .ai-message {
            margin-bottom: 15px;
            padding: 10px;
            border-radius: 8px;
            background-color: #f8f9fa;
        }

        .ai-user {
            background-color: #e8f0fe;
            margin-left: 30px;
        }

        .ai-assistant {
            margin-right: 30px;
        }

        .ai-input-container {
            display: flex;
            margin-top: 15px;
        }

        .ai-input {
            flex: 1;
            padding: 10px;
            border: 1px solid var(--border-color);
            border-radius: 20px;
            outline: none;
        }

        .ai-send-btn {
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            margin-left: 10px;
            cursor: pointer;
        }

        .voice-recording {
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .suggestions-container {
            position: absolute;
            width: 100%;
            background: white;
            border: 1px solid var(--border-color);
            border-radius: 0 0 8px 8px;
            box-shadow: 0 4px 6px rgba(32, 33, 36, 0.1);
            z-index: 100;
            display: none;
        }

        .suggestion-item {
            padding: 8px 15px;
            cursor: pointer;
        }

        .suggestion-item:hover {
            background-color: var(--hover-bg);
        }

        footer {
            background-color: #f2f2f2;
            padding: 15px 20px;
            position: fixed;
            bottom: 0;
            width: 100%;
        }

        .footer-links {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
        }

        .footer-links a {
            color: #70757a;
            text-decoration: none;
            font-size: 14px;
            margin-right: 15px;
        }

        .footer-links a:hover {
            text-decoration: underline;
        }

        @media (max-width: 768px) {
            .logo {
                font-size: 50px;
            }
            
            .search-input {
                padding: 10px 40px 10px 35px;
            }
            
            .image-results {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            }
            
            .footer-links {
                flex-direction: column;
                align-items: center;
                gap: 10px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="nav-links">
            <a href="#">Gmail</a>
            <a href="#">Images</a>
            <i class="fas fa-th apps-icon"></i>
            <a href="#" class="sign-in">Sign in</a>
        </div>
    </header>

    <div class="search-container">
        <div class="logo">Nova</div>
        
        <div class="search-box">
            <i class="fas fa-search search-icon"></i>
            <input type="text" class="search-input" id="searchInput" placeholder="Search Nova or type a URL">
            <i class="fas fa-microphone voice-icon" id="voiceIcon"></i>
            <i class="fas fa-camera camera-icon" id="cameraIcon"></i>
            <div class="suggestions-container" id="suggestionsContainer"></div>
        </div>
        
        <div class="search-buttons">
            <button class="search-btn" id="searchBtn">Nova Search</button>
            <button class="search-btn" id="luckyBtn">I'm Feeling Lucky</button>
        </div>
        
        <div class="search-tabs">
            <div class="search-tab active" data-tab="web">All</div>
            <div class="search-tab" data-tab="images">Images</div>
            <div class="search-tab" data-tab="translate">Translate</div>
            <div class="search-tab" data-tab="ai">AI Chat</div>
        </div>
        
        <div class="search-results" id="searchResults">
            <!-- Web results will appear here -->
        </div>
        
        <div class="image-results" id="imageResults" style="display: none;">
            <!-- Image results will appear here -->
        </div>
        
        <div class="translate-container" id="translateContainer" style="display: none;">
            <div class="translate-box">
                <textarea class="translate-textarea" id="sourceText" placeholder="Enter text to translate"></textarea>
            </div>
            <div class="translate-languages">
                <select id="sourceLanguage">
                    <option value="en">English</option>
                    <option value="es">Spanish</option>
                    <option value="fr">French</option>
                    <option value="de">German</option>
                    <option value="it">Italian</option>
                </select>
                <i class="fas fa-exchange-alt"></i>
                <select id="targetLanguage">
                    <option value="es">Spanish</option>
                    <option value="en">English</option>
                    <option value="fr">French</option>
                    <option value="de">German</option>
                    <option value="it">Italian</option>
                </select>
                <button class="translate-btn" id="translateBtn">Translate</button>
            </div>
            <div class="translate-box">
                <textarea class="translate-textarea" id="translatedText" placeholder="Translation will appear here" readonly></textarea>
            </div>
        </div>
        
        <div class="ai-chat-container" id="aiChatContainer" style="display: none;">
            <div id="aiChatMessages">
                <div class="ai-message ai-assistant">
                    Hello! I'm Nova AI. How can I help you today?
                </div>
            </div>
            <div class="ai-input-container">
                <input type="text" class="ai-input" id="aiInput" placeholder="Ask me anything...">
                <button class="ai-send-btn" id="aiSendBtn">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

    <footer>
        <div class="footer-links">
            <div>
                <a href="#">About</a>
                <a href="#">Advertising</a>
                <a href="#">Business</a>
                <a href="#">How Search works</a>
            </div>
            <div>
                <a href="#">Privacy</a>
                <a href="#">Terms</a>
                <a href="#">Settings</a>
            </div>
        </div>
    </footer>

    <script>
        // DOM Elements
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const luckyBtn = document.getElementById('luckyBtn');
        const voiceIcon = document.getElementById('voiceIcon');
        const cameraIcon = document.getElementById('cameraIcon');
        const searchResults = document.getElementById('searchResults');
        const imageResults = document.getElementById('imageResults');
        const translateContainer = document.getElementById('translateContainer');
        const aiChatContainer = document.getElementById('aiChatContainer');
        const searchTabs = document.querySelectorAll('.search-tab');
        const suggestionsContainer = document.getElementById('suggestionsContainer');
        
        // API Keys
        const RAPIDAPI_KEY = '4264e4023bmshcc21c4c10ae8371p12b9b8jsne79a24181446';
        
        // Current state
        let currentTab = 'web';
        let recognition;
        
        // Initialize the page
        document.addEventListener('DOMContentLoaded', () => {
            // Check for saved search query in URL
            const urlParams = new URLSearchParams(window.location.search);
            const query = urlParams.get('q');
            
            if (query) {
                searchInput.value = query;
                performSearch(query);
            }
        });
        
        // Event Listeners
        searchBtn.addEventListener('click', () => {
            const query = searchInput.value.trim();
            if (query) {
                performSearch(query);
                updateURL(query);
            }
        });
        
        luckyBtn.addEventListener('click', () => {
            const query = searchInput.value.trim();
            if (query) {
                // For "I'm Feeling Lucky", we'll just take the first result and redirect
                performSearch(query, true);
                updateURL(query);
            }
        });
        
        searchInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                const query = searchInput.value.trim();
                if (query) {
                    performSearch(query);
                    updateURL(query);
                }
            }
        });
        
        searchInput.addEventListener('input', () => {
            const query = searchInput.value.trim();
            if (query.length > 2) {
                fetchSuggestions(query);
            } else {
                suggestonsContainer.style.display = 'none';
            }
        });
        
        searchTabs.forEach(tab => {
            tab.addEventListener('click', () => {
                // Update active tab
                searchTabs.forEach(t => t.classList.remove('active'));
                tab.classList.add('active');
                currentTab = tab.dataset.tab;
                
                // Show the appropriate content
                searchResults.style.display = 'none';
                imageResults.style.display = 'none';
                translateContainer.style.display = 'none';
                aiChatContainer.style.display = 'none';
                
                switch(currentTab) {
                    case 'web':
                        searchResults.style.display = 'block';
                        break;
                    case 'images':
                        imageResults.style.display = 'grid';
                        break;
                    case 'translate':
                        translateContainer.style.display = 'flex';
                        break;
                    case 'ai':
                        aiChatContainer.style.display = 'block';
                        break;
                }
            });
        });
        
        // Voice Recognition
        voiceIcon.addEventListener('click', toggleVoiceRecognition);
        
        // Initialize Web Speech API
        if ('webkitSpeechRecognition' in window) {
            recognition = new webkitSpeechRecognition();
            recognition.continuous = false;
            recognition.interimResults = false;
            
            recognition.onstart = () => {
                voiceIcon.classList.add('voice-recording');
            };
            
            recognition.onend = () => {
                voiceIcon.classList.remove('voice-recording');
            };
            
            recognition.onresult = (event) => {
                const transcript = event.results[0][0].transcript;
                searchInput.value = transcript;
                performSearch(transcript);
                updateURL(transcript);
            };
            
            recognition.onerror = (event) => {
                console.error('Speech recognition error', event.error);
                voiceIcon.classList.remove('voice-recording');
            };
        } else {
            voiceIcon.style.display = 'none';
        }
        
        // Translation functionality
        document.getElementById('translateBtn').addEventListener('click', performTranslation);
        
        // AI Chat functionality
        document.getElementById('aiSendBtn').addEventListener('click', sendAIMessage);
        document.getElementById('aiInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendAIMessage();
            }
        });
        
        // Functions
        function toggleVoiceRecognition() {
            if (!recognition) {
                alert('Speech recognition not supported in your browser');
                return;
            }
            
            if (voiceIcon.classList.contains('voice-recording')) {
                recognition.stop();
            } else {
                recognition.start();
            }
        }
        
        function updateURL(query) {
            const newUrl = window.location.pathname + '?q=' + encodeURIComponent(query);
            window.history.pushState({ path: newUrl }, '', newUrl);
        }
        
        function performSearch(query, feelingLucky = false) {
            switch(currentTab) {
                case 'web':
                    fetchWebSearch(query, feelingLucky);
                    break;
                case 'images':
                    fetchImageSearch(query);
                    break;
                default:
                    fetchWebSearch(query, feelingLucky);
            }
        }
        
        async function fetchWebSearch(query, feelingLucky = false) {
            searchResults.innerHTML = '<p>Searching...</p>';
            
            try {
                const response = await fetch(`https://google-search72.p.rapidapi.com/search?q=${encodeURIComponent(query)}&lr=en-US&num=10`, {
                    method: 'GET',
                    headers: {
                        'x-rapidapi-host': 'google-search72.p.rapidapi.com',
                        'x-rapidapi-key': RAPIDAPI_KEY
                    }
                });
                
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                
                const data = await response.json();
                
                if (feelingLucky && data.items && data.items.length > 0) {
                    // Redirect to the first result
                    window.location.href = data.items[0].link;
                    return;
                }
                
                displayWebResults(data.items || []);
            } catch (error) {
                console.error('Search error:', error);
                searchResults.innerHTML = `<p class="error">Error fetching results: ${error.message}</p>`;
            }
        }
        
        function displayWebResults(results) {
            if (results.length === 0) {
                searchResults.innerHTML = '<p>No results found. Try different keywords.</p>';
                return;
            }
            
            searchResults.innerHTML = '';
            
            results.forEach(result => {
                const resultItem = document.createElement('div');
                resultItem.className = 'result-item';
                
                const urlDiv = document.createElement('div');
                urlDiv.className = 'result-url';
                
                // Create favicon (using Google's favicon service as an example)
                const favicon = document.createElement('img');
                favicon.className = 'result-favicon';
                favicon.src = `https://www.google.com/s2/favicons?domain=${new URL(result.link).hostname}`;
                favicon.alt = 'Favicon';
                urlDiv.appendChild(favicon);
                
                const urlText = document.createElement('span');
                urlText.textContent = result.displayLink;
                urlDiv.appendChild(urlText);
                
                const titleLink = document.createElement('a');
                titleLink.className = 'result-title';
                titleLink.href = result.link;
                titleLink.textContent = result.title;
                titleLink.target = '_blank';
                
                const description = document.createElement('div');
                description.className = 'result-description';
                description.textContent = result.snippet;
                
                resultItem.appendChild(urlDiv);
                resultItem.appendChild(titleLink);
                resultItem.appendChild(description);
                
                searchResults.appendChild(resultItem);
            });
        }
        
        async function fetchImageSearch(query) {
            imageResults.innerHTML = '<p>Searching for images...</p>';
            
            try {
                const response = await fetch(`https://real-time-image-search.p.rapidapi.com/search?query=${encodeURIComponent(query)}&limit=10`, {
                    method: 'GET',
                    headers: {
                        'x-rapidapi-host': 'real-time-image-search.p.rapidapi.com',
                        'x-rapidapi-key': RAPIDAPI_KEY
                    }
                });
                
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                
                const data = await response.json();
                displayImageResults(data.results || []);
            } catch (error) {
                console.error('Image search error:', error);
                imageResults.innerHTML = `<p class="error">Error fetching images: ${error.message}</p>`;
            }
        }
        
        function displayImageResults(images) {
            if (images.length === 0) {
                imageResults.innerHTML = '<p>No images found. Try different keywords.</p>';
                return;
            }
            
            imageResults.innerHTML = '';
            
            images.forEach(image => {
                const imageItem = document.createElement('div');
                imageItem.className = 'image-item';
                
                const img = document.createElement('img');
                img.src = image.image.url;
                img.alt = image.title;
                
                const overlay = document.createElement('div');
                overlay.className = 'image-overlay';
                overlay.textContent = image.title;
                
                imageItem.appendChild(img);
                imageItem.appendChild(overlay);
                imageResults.appendChild(imageItem);
            });
        }
        
        async function fetchSuggestions(query) {
            try {
                const response = await fetch(`https://bing-autosuggest1.p.rapidapi.com/suggestions?q=${encodeURIComponent(query)}`, {
                    method: 'GET',
                    headers: {
                        'x-rapidapi-host': 'bing-autosuggest1.p.rapidapi.com',
                        'x-rapidapi-key': RAPIDAPI_KEY
                    }
                });
                
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                
                const data = await response.json();
                displaySuggestions(data.suggestionGroups?.[0]?.searchSuggestions || []);
            } catch (error) {
                console.error('Suggestions error:', error);
                suggestonsContainer.style.display = 'none';
            }
        }
        
        function displaySuggestions(suggestions) {
            suggestonsContainer.innerHTML = '';
            
            if (suggestions.length === 0) {
                suggestonsContainer.style.display = 'none';
                return;
            }
            
            suggestions.slice(0, 5).forEach(suggestion => {
                const suggestionItem = document.createElement('div');
                suggestionItem.className = 'suggestion-item';
                suggestionItem.textContent = suggestion.displayText;
                
                suggestionItem.addEventListener('click', () => {
                    searchInput.value = suggestion.displayText;
                    performSearch(suggestion.displayText);
                    updateURL(suggestion.displayText);
                    suggestonsContainer.style.display = 'none';
                });
                
                suggestonsContainer.appendChild(suggestionItem);
            });
            
            suggestonsContainer.style.display = 'block';
        }
        
        async function performTranslation() {
            const sourceText = document.getElementById('sourceText').value.trim();
            const sourceLang = document.getElementById('sourceLanguage').value;
            const targetLang = document.getElementById('targetLanguage').value;
            
            if (!sourceText) {
                alert('Please enter text to translate');
                return;
            }
            
            document.getElementById('translatedText').value = 'Translating...';
            
            try {
                const response = await fetch('https://deep-translate1.p.rapidapi.com/language/translate/v2', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'x-rapidapi-host': 'deep-translate1.p.rapidapi.com',
                        'x-rapidapi-key': RAPIDAPI_KEY
                    },
                    body: JSON.stringify({
                        q: sourceText,
                        source: sourceLang,
                        target: targetLang
                    })
                });
                
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                
                const data = await response.json();
                document.getElementById('translatedText').value = data.data.translations.translatedText;
            } catch (error) {
                console.error('Translation error:', error);
                document.getElementById('translatedText').value = `Error: ${error.message}`;
            }
        }
        
        async function sendAIMessage() {
            const input = document.getElementById('aiInput');
            const message = input.value.trim();
            
            if (!message) return;
            
            // Add user message to chat
            addAIMessage(message, 'user');
            input.value = '';
            
            // Add loading indicator
            const loadingId = 'loading-' + Date.now();
            addAIMessage('...', 'assistant', loadingId);
            
            try {
                const response = await fetch('https://open-ai21.p.rapidapi.com/conversationllama', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'x-rapidapi-host': 'open-ai21.p.rapidapi.com',
                        'x-rapidapi-key': RAPIDAPI_KEY
                    },
                    body: JSON.stringify({
                        messages: [{
                            role: 'user',
                            content: message
                        }],
                        web_access: false
                    })
                });
                
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                
                const data = await response.json();
                
                // Remove loading indicator and add actual response
                document.getElementById(loadingId).remove();
                addAIMessage(data.choices[0].message.content, 'assistant');
            } catch (error) {
                console.error('AI chat error:', error);
                document.getElementById(loadingId).remove();
                addAIMessage(`Sorry, I encountered an error: ${error.message}`, 'assistant');
            }
        }
        
        function addAIMessage(content, role, id = '') {
            const messagesContainer = document.getElementById('aiChatMessages');
            const messageDiv = document.createElement('div');
            messageDiv.className = `ai-message ai-${role}`;
            if (id) messageDiv.id = id;
            messageDiv.textContent = content;
            messagesContainer.appendChild(messageDiv);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }
        
        // Close suggestions when clicking outside
        document.addEventListener('click', (e) => {
            if (!searchInput.contains(e.target) && !suggestonsContainer.contains(e.target)) {
                suggestonsContainer.style.display = 'none';
            }
        });
    </script>
</body>
</html>
