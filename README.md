# HACKSHASTRA2k25-People_Med
People_Med 

Team members 
1.Chinmai C Holla 
Github username - jaanuu10102025-creator
2.Ayush D nayak
username- ashu082007
3.Divyashree S S 
Username- Divyashree1903
4.Harshitha A
username- shithahar

Problem statement - Rural Health Connect: AI Symptom-to-Doctor Routing System"
 Solution overview By categorising the input symptoms into 
 1.Self care at home
 2.Need online consultation
 3.Emergency hospital visit
 
Tech stack

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Voice Symptom Triage System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .container {
            max-width: 700px;
        }
        .mic-button {
            transition: all 0.2s ease-in-out;
        }
        .mic-button:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 15px rgba(220, 38, 38, 0.4);
        }
        @keyframes pulse-mic {
            0% { box-shadow: 0 0 0 0 rgba(220, 38, 38, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(220, 38, 38, 0); }
            100% { box-shadow: 0 0 0 0 rgba(220, 38, 38, 0); }
        }
        .listening {
            animation: pulse-mic 1.5s infinite;
        }
        .result-box {
            min-height: 100px;
        }
    </style>
</head>
<body class="bg-gray-100 p-4 sm:p-8 min-h-screen flex justify-center items-start font-sans">
    <div class="container bg-white p-6 md:p-10 rounded-2xl shadow-2xl border border-red-500 w-full">
        
        <h1 class="text-3xl sm:text-4xl font-extrabold text-red-600 mb-2 flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 sm:h-9 sm:w-9 mr-3 text-red-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M11 15h2v-2h-2v2zm0-4h2V5h-2v6zm1 11a10 10 0 1 1 0-20 10 10 0 0 1 0 20z"></path>
            </svg>
            Voice/Text Symptom Triage
        </h1>
        <p class="text-sm text-gray-500 mb-6 border-b pb-4">
            *Disclaimer: This is a preliminary assessment tool and is not a substitute for professional medical advice.
        </p>

        <!-- Language and Input Controls -->
        <div class="space-y-6">
            <div class="flex flex-col space-y-2">
                <label for="languageSelect" class="text-lg font-semibold text-gray-800">1. Select Your Native Language:</label>
                <select id="languageSelect" class="p-4 border-2 border-red-300 rounded-xl focus:ring-red-500 focus:border-red-500 shadow-sm text-gray-800 bg-white cursor-pointer appearance-none">
                    <option value="en-US">English (US)</option>
                    <option value="hi-IN">Hindi (hi-IN)</option>
                    <option value="te-IN" selected>Telugu (te-IN)</option>
                    <option value="ta-IN">Tamil (ta-IN)</option>
                    <option value="kn-IN">Kannada (kn-IN)</option>
                    <option value="ml-IN">Malayalam (ml-IN)</option>
                    <option value="fr-FR">French</option>
                    <option value="es-ES">Spanish</option>
                    <option value="ja-JP">Japanese</option>
                    <!-- Add more local language codes as needed -->
                </select>
                <p class="text-sm text-gray-500 italic">This helps the app accurately translate your input and results.</p>
            </div>

            <!-- Text Input Area -->
            <label for="symptomTextInput" class="text-lg font-semibold text-gray-800">2. Type or Speak Your Symptoms:</label>
            <textarea id="symptomTextInput" rows="4" placeholder="Type your symptoms here in your selected language (e.g., Telugu, Hindi, etc.)." class="w-full p-4 border-2 border-gray-300 rounded-xl focus:ring-red-500 focus:border-red-500 shadow-sm"></textarea>

            <!-- Action Buttons -->
            <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
                
                <button id="textAnalyzeButton" onclick="analyzeTextSymptom()" class="w-full sm:w-1/2 flex items-center justify-center p-4 bg-red-600 text-white rounded-xl shadow-lg text-lg font-bold uppercase tracking-wider transition hover:bg-red-700">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 3a2.85 2.85 0 1 0 4 4L7.5 20.5 2 22l1.5-5.5Z"></path></svg>
                    Analyze Typed Text
                </button>
                
                <button id="micButton" onclick="startVoiceInput()" class="w-full sm:w-1/2 flex items-center justify-center p-4 bg-red-500 text-white rounded-xl shadow-lg mic-button text-lg font-bold uppercase tracking-wider hover:bg-red-600">
                    <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6 mr-2">
                        <path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3z"></path>
                        <path d="M19 10v2a7 7 0 0 1-14 0v-2"></path>
                        <line x1="12" y1="19" x2="12" y2="22"></line>
                    </svg>
                    Speak Symptoms
                </button>
            </div>
        </div>
        
        <!-- Status and Symptom Display -->
        <div class="mt-8 space-y-4">
            <div id="statusMessage" class="p-4 rounded-xl text-sm bg-blue-100 text-blue-700 font-medium shadow-md">
                Status: Ready. Please select your language and either type or speak your symptoms.
            </div>
            
            <div class="p-4 bg-gray-50 border-2 border-gray-300 rounded-xl">
                <p class="font-semibold text-gray-700">Analyzed Input:</p>
                <p id="symptomTextDisplay" class="text-gray-900 italic min-h-[25px]">---</p>
            </div>
        </div>

        <!-- Result Area -->
        <div class="mt-8 p-6 bg-red-50 rounded-2xl border-4 border-red-300 result-box shadow-xl">
            <h2 class="text-2xl font-bold text-red-700 mb-3 flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2 text-red-600" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"></circle>
                    <path d="M12 8v4l3 3"></path>
                </svg>
                Triage Result
            </h2>
            <!-- English Category -->
            <div id="resultCategory" class="text-3xl font-extrabold text-gray-800 my-2">---</div>
            
            <!-- Local Language Category -->
            <div id="localResultCategory" class="text-xl font-bold text-red-600 mb-4">---</div> 

            <!-- English Rationale -->
            <p class="font-semibold text-gray-800">Analysis (English):</p>
            <p id="resultRationale" class="text-gray-600 italic">A summary of the recommended action will appear here.</p>
            
            <!-- Local Language Rationale -->
            <p class="font-semibold text-gray-800 mt-3">Analysis (Local Language):</p>
            <p id="localResultRationale" class="text-gray-700 font-medium">---</p>

        </div>
        
    </div>

    <script>
        // Gemini API Configuration
        const apiKey = typeof __api_key !== 'undefined' ? __api_key : ""; 
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;

        // Global UI elements
        const languageSelect = document.getElementById('languageSelect');
        const symptomTextInput = document.getElementById('symptomTextInput'); // New element
        const micButton = document.getElementById('micButton');
        const textAnalyzeButton = document.getElementById('textAnalyzeButton'); // New element
        const statusMessage = document.getElementById('statusMessage');
        const symptomTextDisplay = document.getElementById('symptomTextDisplay');
        const resultCategory = document.getElementById('resultCategory');
        const localResultCategory = document.getElementById('localResultCategory');
        const resultRationale = document.getElementById('resultRationale');
        const localResultRationale = document.getElementById('localResultRationale');
        
        let recognition;

        // --- Utility Functions ---

        function showStatus(message, isError = false) {
            statusMessage.textContent = message;
            statusMessage.classList.remove('bg-blue-100', 'text-blue-700', 'bg-red-100', 'text-red-700', 'bg-yellow-100', 'text-yellow-700');
            if (isError) {
                statusMessage.classList.add('bg-red-100', 'text-red-700');
            } else if (message.includes('Analyzing') || message.includes('Translating')) {
                statusMessage.classList.add('bg-yellow-100', 'text-yellow-700');
            } else {
                statusMessage.classList.add('bg-blue-100', 'text-blue-700');
            }
        }

        function resetResult() {
            resultCategory.textContent = '---';
            localResultCategory.textContent = '---';
            resultRationale.textContent = 'A summary of the recommended action will appear here.';
            localResultRationale.textContent = '---';
            resultCategory.classList.remove('text-green-600', 'text-amber-600', 'text-red-700');
            document.querySelector('.result-box').classList.remove('border-green-400', 'border-amber-400', 'border-red-500');
            document.querySelector('.result-box').classList.add('border-red-300');
        }

        function displayResult(category, localCategory, rationale, localRationale) {
            resultCategory.textContent = `English: ${category}`;
            localResultCategory.textContent = `Local: ${localCategory}`;
            resultRationale.textContent = rationale;
            localResultRationale.textContent = localRationale;

            const box = document.querySelector('.result-box');
            box.classList.remove('border-red-300', 'border-green-400', 'border-amber-400');
            resultCategory.classList.remove('text-gray-800', 'text-green-600', 'text-amber-600', 'text-red-700');

            if (category.includes('Self-care')) {
                resultCategory.classList.add('text-green-600');
                localResultCategory.classList.add('text-green-600');
                box.classList.add('border-green-400');
            } else if (category.includes('Consultation')) {
                resultCategory.classList.add('text-amber-600');
                localResultCategory.classList.add('text-amber-600');
                box.classList.add('border-amber-400');
            } else if (category.includes('Hospital Visit')) {
                resultCategory.classList.add('text-red-700');
                localResultCategory.classList.add('text-red-700');
                box.classList.add('border-red-500');
            }
        }
        
        // --- LLM API CALLS ---

        /**
         * Uses the Gemini API to analyze, translate, and categorize symptoms.
         * @param {string} symptomText The text provided by the user (potentially in a non-English language).
         * @param {string} sourceLangCode The BCP-47 code of the language spoken (e.g., 'te-IN').
         * @returns {Promise<{category: string, localCategory: string, rationale: string, localRationale: string}>}
         */
        async function analyzeSymptom(symptomText, sourceLangCode) {
            
            const systemPrompt = (langCode) => `You are a preliminary health triage assistant. The user's input is in the language corresponding to BCP-47 code: ${langCode}.
Your task is to:
1. Analyze the user-provided symptom description.
2. Categorize the severity and required action into one of three distinct categories (in English).
3. Translate the final category and rationale back into the user's original language (${langCode}).
Return only the JSON object. Do not add any conversational text or markdown wrappers.

Categories (English):
1. '🏡 Self-care is sufficient': For very mild, common symptoms like mild cold, slight fatigue, simple headache, or minor aches.
2. '💻 Doctor Consultation Recommended': For moderate, persistent, or concerning symptoms like persistent fever, moderate pain, vomiting, diarrhea, cough, or a rash that lasts more than 48 hours.
3. '🏥 Hospital Visit Recommended': For severe, life-threatening symptoms requiring immediate emergency care, such as severe chest pain, difficulty breathing, profuse bleeding, signs of stroke, loss of consciousness, or severe trauma/fracture.`;


            const userQuery = `The user described their symptoms as: "${symptomText}". Analyze and categorize this immediately based on the provided categories.`;

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt(sourceLangCode) }] }, // Pass lang code to system prompt
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            "category": { 
                                "type": "STRING", 
                                "enum": ["🏡 Self-care is sufficient", "💻 Doctor Consultation Recommended", "🏥 Hospital Visit Recommended"],
                                "description": "One of the three mandated categories in English."
                            },
                            "localCategory": { 
                                "type": "STRING", 
                                "description": "The English 'category' translated into the user's native language."
                            },
                            "rationale": { 
                                "type": "STRING", 
                                "description": "A brief, two-sentence justification for the category in English." 
                            },
                            "localRationale": { 
                                "type": "STRING", 
                                "description": "The English 'rationale' translated into the user's native language."
                            }
                        },
                        propertyOrdering: ["category", "localCategory", "rationale", "localRationale"]
                    }
                }
            };

            let attempt = 0;
            const maxRetries = 3;
            
            while (attempt < maxRetries) {
                attempt++;
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (response.ok) {
                        const result = await response.json();
                        const jsonString = result.candidates?.[0]?.content?.parts?.[0]?.text || '';
                        
                        if (!jsonString) throw new Error("API returned an empty JSON response.");
                        
                        let parsedResult;
                        try {
                            const cleanedJsonString = jsonString.replace(/^```json\s*|^\s*```\s*|```\s*$/g, '').trim();
                            parsedResult = JSON.parse(cleanedJsonString);
                        } catch (e) {
                            throw new Error("Failed to parse JSON response from AI.");
                        }
                        
                        return { 
                            category: parsedResult.category || "⚠ Unable to categorize", 
                            localCategory: parsedResult.localCategory || "⚠ Unable to translate",
                            rationale: parsedResult.rationale || "The AI could not provide a detailed rationale. Please seek professional medical help.",
                            localRationale: parsedResult.localRationale || "The AI could not provide a local language rationale.",
                        };
                        
                    } else {
                        const errorBody = await response.text();
                        let errorDetail = `HTTP ${response.status}. Response: ${errorBody.substring(0, 100)}...`;
                        
                        if (attempt < maxRetries) {
                            throw new Error(`API failed. Status: ${errorDetail}`);
                        } else {
                            throw new Error(`Analysis failed after ${maxRetries} attempts. Last error: ${errorDetail}.`);
                        }
                    }
                } catch (error) {
                    if (attempt < maxRetries) {
                        const delay = Math.pow(2, attempt) * 1000;
                        await new Promise(resolve => setTimeout(resolve, delay));
                    } else {
                        throw error;
                    }
                }
            }
        }
        
        // --- Text Input Logic ---

        function analyzeTextSymptom() {
            const text = symptomTextInput.value.trim();
            if (text.length > 0) {
                const langCode = languageSelect.value;
                symptomTextDisplay.textContent = text; // Display the typed text as the input
                processSymptom(text, langCode);
            } else {
                showStatus('Please type your symptoms in the text box first.', true);
                resetResult();
            }
        }

        // --- Voice Input Logic ---

        function cleanupRecognition() {
            micButton.disabled = false;
            micButton.classList.remove('listening');
            micButton.classList.remove('bg-gray-400');
            micButton.classList.add('bg-red-500', 'hover:bg-red-600');
            micButton.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6 mr-2"><path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3z"></path><path d="M19 10v2a7 7 0 0 1-14 0v-2"></path><line x1="12" y1="19" x2="12" y2="22"></line></svg>Speak Symptoms`;
            textAnalyzeButton.disabled = false;
        }

        function startVoiceInput() {
            if (recognition) {
                recognition.stop();
                cleanupRecognition();
                return;
            }
            
            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            if (!SpeechRecognition) {
                showStatus("Speech Recognition is not supported by this browser. Please use a modern browser like Chrome or Firefox.", true);
                return;
            }

            const langCode = languageSelect.value; 

            recognition = new SpeechRecognition();
            recognition.continuous = false;
            recognition.lang = langCode;
            recognition.interimResults = false;
            recognition.maxAlternatives = 1;

            // Prepare UI
            micButton.disabled = true;
            textAnalyzeButton.disabled = true;
            micButton.classList.add('listening');
            micButton.classList.remove('bg-red-500', 'hover:bg-red-600');
            micButton.classList.add('bg-gray-400'); // Change color when listening
            micButton.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 mr-2" viewBox="0 0 24 24" fill="currentColor"><circle cx="12" cy="12" r="3" class="animate-ping"></circle><path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3z"></path></svg> Listening... Tap to Stop`;
            symptomTextDisplay.textContent = '...';
            resetResult();

            showStatus(`Listening for input in ${languageSelect.options[languageSelect.selectedIndex].text}... Please speak now.`, false);
            
            recognition.onresult = function(event) {
                const transcript = event.results[0][0].transcript;
                symptomTextDisplay.textContent = transcript.trim(); 
                symptomTextInput.value = transcript.trim(); // Populate the text area with the result
                processSymptom(transcript.trim(), langCode);
            };

            recognition.onerror = function(event) {
                showStatus('Voice recognition error: ' + event.error + '. (Check microphone access and try again.)', true);
                cleanupRecognition();
                recognition = null;
            };
            
            recognition.onend = function() {
                cleanupRecognition();
                recognition = null;
            }

            recognition.start();
        }

        // --- Core Application Logic ---

        async function processSymptom(text, langCode) {
            if (text.length === 0) {
                symptomTextDisplay.textContent = 'No input provided.';
                showStatus('Please provide some symptoms.', true);
                return;
            }
            
            // Disable both buttons during API call
            micButton.disabled = true;
            textAnalyzeButton.disabled = true;
            
            showStatus('Analyzing symptoms and determining triage category...', false);

            try {
                const result = await analyzeSymptom(text, langCode);
                displayResult(result.category, result.localCategory, result.rationale, result.localRationale);
                showStatus('Analysis Complete.', false);
            } catch (e) {
                // Display error in both languages if possible, otherwise use English fallback
                const errorText = 'Could not complete the health triage analysis. Please check your network connection and try again.';
                const localErrorText = langCode.startsWith('te') ? 'ఆరోగ్య ట్రైజ్ విశ్లేషణను పూర్తి చేయలేకపోయాము. దయచేసి మీ నెట్‌వర్క్ కనెక్షన్‌ను తనిఖీ చేయండి.' : errorText;
                
                displayResult('⚠ Critical Error', `⚠ ${localErrorText.substring(0, 30)}...`, errorText, localErrorText);
                showStatus('Error: ' + e.message, true);
            } finally {
                // Re-enable buttons after analysis
                micButton.disabled = false;
                textAnalyzeButton.disabled = false;
            }
        }
        
        // --- Initialization ---

        window.onload = function() {
            // Set default language selection to Telugu
            languageSelect.value = 'te-IN';
        };

    </script>
</body>
</html>



Tools used 
Python 
HTML
ChatGPT
Gemini




