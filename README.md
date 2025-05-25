<script>
    console.log("Script started!"); // Debug: Confirm script runs
    const chatbox = document.getElementById('chatbox');
    const userInput = document.getElementById('userInput');
    const languageSelect = document.getElementById('language');
    console.log("Elements loaded:", chatbox, userInput, languageSelect); // Debug: Check DOM elements
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
    console.log("Current language:", currentLanguage); // Debug: Check language
    appendMessage('AI', responses[currentLanguage].greeting);
    languageSelect.addEventListener('change', () => {
        currentLanguage = languageSelect.value;
        chatbox.innerHTML = '';
        appendMessage('AI', responses[currentLanguage].greeting);
    });
    function appendMessage(sender, message) {
        console.log("Appending message:", sender, message); // Debug: Check message appending
        const messageDiv = document.createElement('div');
        messageDiv.className = `p-2 ${sender === 'AI' ? 'text-blue-600' : 'text-gray-800 font-semibold'} ${currentLanguage === 'si' ? 'font-noto-serif-sinhala' : ''}`;
        messageDiv.textContent = `${sender}: ${message}`;
        chatbox.appendChild(messageDiv);
        chatbox.scrollTop = chatbox.scrollHeight;
    }
    function sendMessage() {
        console.log("sendMessage called"); // Debug: Confirm function call
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
        else if (userMessage.includes('name') || userMessage.includes('email') || userMessage.includes('නම') || userMessage.includes('ඊමේල්')) aiResponse = currentLanguage === 'en' ? `Thank you for registering! We'll reach out to confirm your details.` : `ලියාපදිංචි වීමට ස්තුතියි! ඔබේ විස්තර තහවුරු කිරීමට අපි ඉක්මනින් සම්බන්ධ වෙමු.`;
        setTimeout(() => appendMessage('AI', aiResponse), 500);
    }
    userInput.addEventListener('keypress', (e) => {
        console.log("Keypress event:", e.key); // Debug: Check Enter key
        if (e.key === 'Enter') sendMessage();
    });
</script>
