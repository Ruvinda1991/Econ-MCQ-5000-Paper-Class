console.log("Script is running!");
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCQ 5000 Paper Class AI Agent</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+Sinhala&display=swap" rel="stylesheet">
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">
    <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
        <h1 class="text-2xl font-bold text-center mb-4">MCQ 5000 Paper Class AI Assistant</h1>
        <p class="text-center text-sm mb-4">By Ruvinda Siriwardhana</p>
        <div class="mb-4">
            <label class="mr-2">Select Language:</label>
            <select id="language" class="border p-1 rounded">
                <option value="en">English</option>
                <option value="si">සිංහල</option>
            </select>
        </div>
        <div id="chatbox" class="h-80 overflow-y-auto border p-4 mb-4 rounded"></div>
        <div class="flex">
            <input id="userInput" type="text" class="flex-1 p-2 border rounded-l" placeholder="Type your message...">
            <button onclick="sendMessage()" class="bg-blue-500 text-white p-2 rounded-r hover:bg-blue-600">Send</button>
        </div>
        <p class="text-center mt-4">
            <a href="https://wa.me/+94YOURNUMBERHERE" target="_blank" class="text-blue-500 hover:underline">Contact us on WhatsApp</a>
        </p>
    </div>
    <script>
        const chatbox = document.getElementById('chatbox');
        const userInput = document.getElementById('userInput');
        const languageSelect = document.getElementById('language');
        const responses = {
            en: {
                greeting: "Welcome to MCQ 5000 Paper Class! Saw our ad on Facebook? I'm here to help with A/L Economics for 2025 Exam, 2026 Revision, and 2027 Theory levels. Type 'courses', 'mcq', 'schedule', 'tips', or 'register'.",
                courses: "We offer classes for 2025 Exam Level, 2026 Revision Level, and 2027 Theory Level. Focus areas include Competency 01. Which level are you interested in?",
                mcq: "Sample MCQ: What is the main cause of scarcity? A) Unlimited wants B) Limited resources C) High prices D) Low demand E) Government policy. Type 'answer B' or 'more mcq'.",
                schedule: "Slots: Mon-Fri, 4 PM, 5 PM, 6 PM. Type 'schedule Mon 4 PM 2025' to book.",
                tips: "2025 Exam: Practice past papers. 2026 Revision: Focus on weak areas. 2027 Theory: Build concepts. Want level-specific tips?",
                register: "Provide your name, email, and level (2025 Exam, 2026 Revision, or 2027 Theory).",
                default: "Sorry, I didn't understand. Try 'courses', 'mcq', 'schedule', 'tips', or 'register'."
            },
            si: {
                greeting: "MCQ 5000 Paper Class වෙත සාදරයෙන්! Facebook හි දැන්වීම දුටුවාද? 2025 විභාග, 2026 පුනරීක්ෂණ, 2027 න්‍යාය සඳහා උපකාර කරමි. 'පාඨමාලා', 'mcq', 'කාලසටහන', 'ඉඟි', හෝ 'ලියාපදිංචි' ටයිප් කරන්න.",
                courses: "2025 විභාග, 2026 පුනරීක්ෂණ, 2027 න්‍යාය මට්ටම් සඳහා පාඨමාලා. Competency 01 ඇතුළුව. ඔබට උනන්දුවක් ඇත්තේ කුමන මට්ටමද?",
                mcq: "MCQ: හිඟකමට හේතුව? A) අසීමිත ආශා B) සීමිත සම්පත් C) ඉහළ මිල D) අඩු ඉල්ලුම E) රජයේ ප්‍රතිපත්ති. 'පිළිතුර B' හෝ 'තවත් mcq' ටයිප් කරන්න.",
                schedule: "කාලසටහන්: සඳු-සිකු, ප.ව. 4, 5, 6. 'කාලසටහන සඳු 4 PM 2025' ටයිප් කරන්න.",
                tips: "2025: පසුගිය ප්‍රශ්න පුහුණු. 2026: දුර්වල ක්ෂේත්ර. 2027: සංකල්ප. මට්ටමක ඉඟි අවශ්‍යද?",
                register: "නම, ඊමේල්, සහ මට්ටම (2025, 2026, හෝ 2027) සපයන්න.",
                default: "සමාවන්න, තේරුම් ගත නොහැක. 'පාඨමාලා', 'mcq', 'කාලසටහන', 'ඉඟි', හෝ 'ලියාපදිංචි' ටයිප් කරන්න."
            }
        };
        let currentLanguage = languageSelect.value;
        appendMessage('AI', responses[currentLanguage].greeting);
        languageSelect.addEventListener('change', () => {
            currentLanguage = languageSelect.value;
            chatbox.innerHTML = '';
            appendMessage('AI', responses[currentLanguage].greeting);
        });
        function appendMessage(sender, message) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `p-2 ${sender === 'AI' ? 'text-blue-600' : 'text-gray-800 font-semibold'} ${currentLanguage === 'si' ? 'font-noto-serif-sinhala' : ''}`;
            messageDiv.textContent = `${sender}: ${message}`;
            chatbox.appendChild(messageDiv);
            chatbox.scrollTop = chatbox.scrollHeight;
        }
        function sendMessage() {
            const userMessage = userInput.value.trim().toLowerCase();
            if (!userMessage) return;
            appendMessage('You', userMessage);
            userInput.value = '';
            let aiResponse = responses[currentLanguage].default;
            if (userMessage.includes('course') || userMessage.includes('පාඨමාලා')) aiResponse = responses[currentLanguage].courses;
            else if (userMessage.includes('mcq')) aiResponse = responses[currentLanguage].mcq;
            else if (userMessage.includes('schedule') || userMessage.includes('කාලසටහන') || userMessage.includes('pm')) aiResponse = responses[currentLanguage].schedule;
            else if (userMessage.includes('tips') || userMessage.includes('ඉඟි')) aiResponse = responses[currentLanguage].tips;
            else if (userMessage.includes('register') || userMessage.includes('ලියාපදිංචි')) aiResponse = responses[currentLanguage].register;
            else if (userMessage.includes('mon') || userMessage.includes('tue') || userMessage.includes('wed') || userMessage.includes('thu') || userMessage.includes('fri') || userMessage.includes('සඳු') || userMessage.includes('අඟ') || userMessage.includes('බදා') || userMessage.includes('බ්‍රහ') || userMessage.includes('සිකු')) aiResponse = currentLanguage === 'en' ? `Great! You've booked ${userMessage.toUpperCase()}. We'll confirm via email soon.` : `විශිෂ්ටයි! ඔබ ${userMessage.toUpperCase()} වෙන් කර ඇත. ඉක්මනින් ඊමේල් හරහා තහවුරු කරමු.`;
            else if (userMessage.includes('answer') || userMessage.includes('පිළිතුර')) aiResponse = currentLanguage === 'en' ? `Thanks for your answer! Type 'more mcq' for another question.` : `ඔබේ පිළිතුරට ස්තුතියි! 'තවත් mcq' ටයිප් කරන්න.`;
            else if (userMessage.includes('name') || userMessage.includes('email') || userMessage.includes('නම') || userMessage.includes('ඊමේල්')) aiResponse = currentLanguage === 'en' ? `Thank you for registering! We'll reach out to confirm your details.` : `ලියාපදිංකි වීමට ස්තුතියි! ඔබේ විස්තර තහවුරු කිරීමට අපි ඉක්මනින් සම්බන්ධ වෙමු.`;
            setTimeout(() => appendMessage('AI', aiResponse), 500);
        }
        userInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });
    </script>
</body>
</html>
