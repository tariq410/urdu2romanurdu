<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Urdu to Roman English Converter</title>
    <style>
        :root {
            --primary-color: #4a6fa5;
            --secondary-color: #166088;
            --accent-color: #4fc3f7;
            --light-color: #f8f9fa;
            --dark-color: #343a40;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px 0;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        h1 {
            margin-bottom: 10px;
            font-size: 2.5rem;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        main {
            padding: 30px 0;
        }
        
        .converter-container {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            padding: 30px;
            margin-bottom: 30px;
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            margin-bottom: 20px;
        }
        
        label {
            font-weight: bold;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }
        
        textarea {
            width: 100%;
            min-height: 150px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1.1rem;
            resize: vertical;
        }
        
        .urdu-text {
            font-family: 'Noto Nastaliq Urdu', 'Jameel Noori Nastaleeq', 'Urdu Typesetting', serif;
            font-size: 1.3rem;
            direction: rtl;
        }
        
        .buttons {
            display: flex;
            gap: 10px;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        button {
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        
        .convert-btn {
            background-color: var(--primary-color);
            color: white;
            flex-grow: 1;
        }
        
        .convert-btn:hover {
            background-color: var(--secondary-color);
        }
        
        .clear-btn {
            background-color: #f0f0f0;
            color: var(--dark-color);
        }
        
        .clear-btn:hover {
            background-color: #e0e0e0;
        }
        
        .copy-btn {
            background-color: var(--accent-color);
            color: white;
        }
        
        .copy-btn:hover {
            opacity: 0.9;
        }
        
        .result-container {
            margin-top: 30px;
        }
        
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }
        
        .feature-card {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }
        
        .feature-card h3 {
            color: var(--primary-color);
            margin-bottom: 10px;
        }
        
        footer {
            background-color: var(--dark-color);
            color: white;
            text-align: center;
            padding: 20px 0;
            margin-top: 40px;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .converter-container {
                padding: 20px;
            }
            
            .buttons {
                flex-direction: column;
            }
            
            button {
                width: 100%;
            }
        }
        
        /* Loading animation */
        .loader {
            display: none;
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--primary-color);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Notification */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: #4CAF50;
            color: white;
            padding: 15px;
            border-radius: 4px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Urdu to Roman English Converter</h1>
            <p class="subtitle">Convert Urdu text to Romanized English (transliteration) easily</p>
        </div>
    </header>
    
    <main class="container">
        <div class="converter-container">
            <div class="input-group">
                <label for="urdu-input">Enter Urdu Text:</label>
                <textarea id="urdu-input" class="urdu-text" placeholder="اردو میں متن لکھیں..."></textarea>
            </div>
            
            <div class="buttons">
                <button id="convert-btn" class="convert-btn">Convert to Roman English</button>
                <button id="clear-btn" class="clear-btn">Clear Text</button>
                <button id="copy-urdu-btn" class="copy-btn">Copy Urdu</button>
            </div>
            
            <div class="loader" id="loader"></div>
            
            <div class="result-container">
                <div class="input-group">
                    <label for="roman-output">Roman English Output:</label>
                    <textarea id="roman-output" readonly placeholder="Romanized English text will appear here..."></textarea>
                </div>
                
                <div class="buttons">
                    <button id="copy-roman-btn" class="copy-btn">Copy Roman Text</button>
                </div>
            </div>
        </div>
        
        <div class="features">
            <div class="feature-card">
                <h3>How to Use</h3>
                <p>Simply type or paste Urdu text in the input box and click "Convert" to get the Roman English transliteration. You can then copy the result for your use.</p>
            </div>
            
            <div class="feature-card">
                <h3>About Transliteration</h3>
                <p>Roman Urdu is the representation of Urdu language using the English alphabet. This helps people who can speak Urdu but have difficulty reading the Urdu script.</p>
            </div>
            
            <div class="feature-card">
                <h3>Tips</h3>
                <ul>
                    <li>Write complete words for better accuracy</li>
                    <li>Check for proper Urdu spelling</li>
                    <li>Review the output for any needed corrections</li>
                </ul>
            </div>
        </div>
    </main>
    
    <footer>
        <div class="container">
            <p>&copy; 2023 Urdu to Roman English Converter. All rights reserved.</p>
        </div>
    </footer>
    
    <div class="notification" id="notification">Text copied to clipboard!</div>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const urduInput = document.getElementById('urdu-input');
            const romanOutput = document.getElementById('roman-output');
            const convertBtn = document.getElementById('convert-btn');
            const clearBtn = document.getElementById('clear-btn');
            const copyUrduBtn = document.getElementById('copy-urdu-btn');
            const copyRomanBtn = document.getElementById('copy-roman-btn');
            const loader = document.getElementById('loader');
            const notification = document.getElementById('notification');
            
            // Urdu to Roman mapping
            const urduToRomanMap = {
                // Letters
                'ا': 'a', 'آ': 'aa', 'أ': 'a', 'إ': 'i', 'ئ': 'y', 'ء': "'",
                'ب': 'b', 'پ': 'p', 'ت': 't', 'ٹ': 'tt', 'ث': 's', 
                'ج': 'j', 'چ': 'ch', 'ح': 'h', 'خ': 'kh', 
                'د': 'd', 'ڈ': 'dd', 'ذ': 'z', 'ر': 'r', 'ڑ': 'rr', 'ز': 'z', 'ژ': 'zh', 
                'س': 's', 'ش': 'sh', 'ص': 's', 'ض': 'z', 'ط': 't', 'ظ': 'z', 
                'ع': "'", 'غ': 'gh', 
                'ف': 'f', 'ق': 'q', 'ک': 'k', 'گ': 'g', 'ل': 'l', 'م': 'm', 'ن': 'n', 
                'و': 'w', 'ہ': 'h', 'ھ': 'h', 'ی': 'y', 'ے': 'e',
                
                // Diacritics
                'َ': 'a', 'ُ': 'u', 'ِ': 'i', 'ّ': '', 'ْ': '', 'ً': 'an', 'ٌ': 'un', 'ٍ': 'in',
                
                // Numbers
                '۰': '0', '۱': '1', '۲': '2', '۳': '3', '۴': '4',
                '۵': '5', '۶': '6', '۷': '7', '۸': '8', '۹': '9',
                
                // Punctuation
                '،': ',', '؛': ';', '؟': '?', '۔': '.', '!': '!'
            };
            
            // Common words mapping for better accuracy
            const commonWordsMap = {
                'میں': 'main',
                'تم': 'tum',
                'ہم': 'hum',
                'آپ': 'aap',
                'ہے': 'hai',
                'ہیں': 'hain',
                'اور': 'aur',
                'لیکن': 'lekin',
                'کیا': 'kya',
                'کہ': 'keh',
                'تو': 'to',
                'بھی': 'bhi',
                'نہیں': 'nahin',
                'ہو': 'ho',
                'تھا': 'tha',
                'تھی': 'thi',
                'تھے': 'the',
                'کر': 'kar',
                'دیا': 'diya',
                'لیا': 'liya',
                'گیا': 'gaya',
                'رہا': 'raha',
                'رہی': 'rahi',
                'رہے': 'rahe',
                'چاہیے': 'chahiye',
                'سکتا': 'sakta',
                'سکتی': 'sakti',
                'سکتے': 'sakte',
                'والا': 'wala',
                'والی': 'wali',
                'والے': 'wale',
                'والوں': 'walon'
            };
            
            // Convert Urdu to Roman English
            function convertToRoman(urduText) {
                // First check for common words
                for (const [urduWord, romanWord] of Object.entries(commonWordsMap)) {
                    const regex = new RegExp(urduWord, 'g');
                    urduText = urduText.replace(regex, romanWord);
                }
                
                // Convert remaining characters
                let romanText = '';
                for (let i = 0; i < urduText.length; i++) {
                    const char = urduText[i];
                    romanText += urduToRomanMap[char] || char;
                }
                
                // Clean up the text
                romanText = romanText.replace(/'+/g, "'"); // Remove duplicate apostrophes
                romanText = romanText.replace(/\s+/g, ' '); // Remove extra spaces
                romanText = romanText.trim();
                
                return romanText;
            }
            
            // Show loading animation
            function showLoader() {
                loader.style.display = 'block';
                romanOutput.value = '';
            }
            
            // Hide loading animation
            function hideLoader() {
                loader.style.display = 'none';
            }
            
            // Show notification
            function showNotification(message) {
                notification.textContent = message;
                notification.style.display = 'block';
                setTimeout(() => {
                    notification.style.display = 'none';
                }, 3000);
            }
            
            // Event Listeners
            convertBtn.addEventListener('click', function() {
                const urduText = urduInput.value.trim();
                if (!urduText) {
                    showNotification('Please enter some Urdu text first');
                    return;
                }
                
                showLoader();
                
                // Simulate processing delay (would be real processing in a real app)
                setTimeout(() => {
                    const romanText = convertToRoman(urduText);
                    romanOutput.value = romanText;
                    hideLoader();
                    showNotification('Conversion complete!');
                }, 800);
            });
            
            clearBtn.addEventListener('click', function() {
                urduInput.value = '';
                romanOutput.value = '';
            });
            
            copyUrduBtn.addEventListener('click', function() {
                if (!urduInput.value.trim()) {
                    showNotification('No Urdu text to copy');
                    return;
                }
                
                urduInput.select();
                document.execCommand('copy');
                showNotification('Urdu text copied to clipboard!');
            });
            
            copyRomanBtn.addEventListener('click', function() {
                if (!romanOutput.value.trim()) {
                    showNotification('No Roman text to copy');
                    return;
                }
                
                romanOutput.select();
                document.execCommand('copy');
                showNotification('Roman text copied to clipboard!');
            });
            
            // Allow Enter key with Shift in textarea (but not submit form)
            urduInput.addEventListener('keydown', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    convertBtn.click();
                }
            });
        });
    </script>
</body>
</html>
