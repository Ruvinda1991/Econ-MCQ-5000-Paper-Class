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
                greeting: "MCQ 5000 Paper Class වෙත සාදරයෙන්! Facebook හි දැන්වීම දුට
