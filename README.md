# Flashcards
Brazilian Portuguese
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Brazilian Portuguese Flashcards & Quiz</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Font Awesome for Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: {
              dark: '#1b4332',
              primary: '#2d6a4f',
              light: '#52b788',
              accent: '#d8f3dc',
              gold: '#e9c46a',
              goldHover: '#f4a261',
            }
          }
        }
      }
    }
  </script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
    body {
      font-family: 'Inter', sans-serif;
    }

    /* Card Flip Animation Styles */
    .perspective-1000 {
      perspective: 1000px;
    }
    .transform-style-3d {
      transform-style: preserve-3d;
    }
    .backface-hidden {
      backface-visibility: hidden;
      -webkit-backface-visibility: hidden;
    }
    .rotate-y-180 {
      transform: rotateY(180deg);
    }
    .card-inner {
      transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    }

    /* Pulse & Ripple animations */
    @keyframes pulse-light {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }
    .animate-pulse-subtle {
      animation: pulse-light 2s infinite ease-in-out;
    }
  </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col justify-between selection:bg-brand-light selection:text-brand-dark">

  <!-- Main Container -->
  <div class="w-full max-w-xl mx-auto px-4 py-6 flex-grow flex flex-col">

    <!-- Header Section -->
    <header class="text-center mb-6">
      <div class="inline-flex items-center justify-center gap-2 mb-1">
        <span class="text-3xl">🇧🇷</span>
        <h1 class="text-2xl sm:text-3xl font-extrabold text-brand-dark tracking-tight">Aprenda Português</h1>
      </div>
      <p class="text-xs sm:text-sm text-slate-600 font-medium">Master Brazilian Portuguese with Audio & Interactive Quizzes</p>

      <!-- App Mode Selector Tabs -->
      <div class="flex bg-slate-200 p-1 rounded-xl mt-5 shadow-inner">
        <button id="tabStudy" onclick="switchMode('study')" 
          class="flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 bg-brand-primary text-white shadow-md">
          <i class="fa-solid fa-layer-group"></i> Study Mode
        </button>
        <button id="tabQuiz" onclick="switchMode('quiz')" 
          class="flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 text-slate-600 hover:text-brand-dark">
          <i class="fa-solid fa-circle-question"></i> Quiz Mode
        </button>
      </div>
    </header>

    <!-- ================= STUDY MODE ================= -->
    <main id="studyMode" class="flex-grow flex flex-col gap-4">
      
      <!-- Top Action Controls -->
      <div class="bg-white p-3 rounded-xl shadow-sm border border-slate-200/80 flex flex-wrap gap-2 items-center justify-between">
        <!-- Category Filter -->
        <div class="flex-1 min-w-[140px]">
          <select id="categoryFilter" onchange="filterCategory()" class="w-full bg-slate-50 border border-slate-200 text-xs sm:text-sm font-semibold rounded-lg px-3 py-2 text-slate-700 focus:outline-none focus:ring-2 focus:ring-brand-primary">
            <option value="All">All Categories</option>
            <option value="Phrases">Phrases</option>
            <option value="Verbs">Verbs</option>
            <option value="Nouns">Nouns</option>
            <option value="Contractions">Contractions</option>
          </select>
        </div>

        <!-- Add Card Toggle -->
        <button onclick="toggleAddForm()" class="bg-brand-accent hover:bg-emerald-200 text-brand-primary font-bold text-xs sm:text-sm px-3 py-2 rounded-lg transition-colors flex items-center gap-1.5 border border-brand-light/30">
          <i class="fa-solid fa-plus"></i>
          <span>Add Word</span>
        </button>
      </div>

      <!-- Add New Card Collapsible Form -->
      <div id="addForm" class="hidden bg-white p-4 rounded-xl shadow-md border border-brand-light/40 flex flex-col gap-3 transition-all">
        <div class="flex justify-between items-center border-b border-slate-100 pb-2">
          <h3 class="font-bold text-sm text-brand-dark flex items-center gap-1.5">
            <i class="fa-solid fa-square-plus text-brand-primary"></i> Add Custom Flashcard
          </h3>
          <button onclick="toggleAddForm()" class="text-slate-400 hover:text-slate-600 text-xs"><i class="fa-solid fa-xmark"></i></button>
        </div>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
          <input type="text" id="newPt" placeholder="Portuguese (e.g. Bom dia)" class="bg-slate-50 border border-slate-200 rounded-lg p-2 text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-brand-primary">
          <input type="text" id="newEn" placeholder="English (e.g. Good morning)" class="bg-slate-50 border border-slate-200 rounded-lg p-2 text-xs sm:text-sm focus:outline-none focus:ring-2 focus:ring-brand-primary">
        </div>
        
        <div class="flex gap-2">
          <select id="newCat" class="bg-slate-50 border border-slate-200 rounded-lg px-3 py-2 text-xs sm:text-sm text-slate-700 focus:outline-none focus:ring-2 focus:ring-brand-primary flex-1">
            <option value="Phrases">Phrases</option>
            <option value="Verbs">Verbs</option>
            <option value="Nouns">Nouns</option>
            <option value="Contractions">Contractions</option>
          </select>
          <button onclick="addCard()" class="bg-brand-primary hover:bg-brand-dark text-white font-bold text-xs sm:text-sm px-4 py-2 rounded-lg transition-colors shadow-sm">
            Save Card
          </button>
        </div>
      </div>

      <!-- Flashcard Interactive Area -->
      <div class="perspective-1000 w-full min-h-[260px] sm:min-h-[290px] relative cursor-pointer group my-auto" onclick="flipCard()">
        <div id="card" class="card-inner w-full h-full min-h-[260px] sm:min-h-[290px] relative transform-style-3d rounded-2xl shadow-lg border border-slate-200/80 bg-white">
          
          <!-- FRONT FACE (Portuguese) -->
          <div class="card-face card-front absolute inset-0 backface-hidden rounded-2xl p-6 flex flex-col justify-between items-center text-center bg-gradient-to-b from-white to-emerald-50/40">
            <!-- Header Tag & Audio -->
            <div class="w-full flex justify-between items-center" onclick="event.stopPropagation()">
              <span id="cardCat" class="bg-emerald-100 text-brand-primary font-bold text-[10px] sm:text-xs uppercase tracking-wider px-2.5 py-1 rounded-md border border-emerald-200">
                Category
              </span>
              <button onclick="speakCurrentCard(event)" title="Listen to Portuguese" class="w-10 h-10 rounded-full bg-brand-accent hover:bg-brand-light/40 text-brand-primary flex items-center justify-center transition-all transform active:scale-95 shadow-sm">
                <i class="fa-solid fa-volume-high text-lg"></i>
              </button>
            </div>

            <!-- Content Area -->
            <div class="my-auto py-4">
              <div id="cardPt" class="text-2xl sm:text-3xl font-extrabold text-slate-800 tracking-wide mb-2">
                Carregando...
              </div>
              <p class="text-xs text-slate-400 font-medium">Portuguese</p>
            </div>

            <!-- Bottom Hint -->
            <div class="text-slate-400 text-xs font-semibold flex items-center gap-1.5 opacity-80">
              <i class="fa-solid fa-rotate"></i>
              <span>Tap card to reveal English</span>
            </div>
          </div>

          <!-- BACK FACE (English) -->
          <div class="card-face card-back absolute inset-0 backface-hidden rotate-y-180 rounded-2xl p-6 flex flex-col justify-between items-center text-center bg-brand-primary text-white shadow-inner">
            <!-- Header Tag & Audio -->
            <div class="w-full flex justify-between items-center" onclick="event.stopPropagation()">
              <span id="cardCatBack" class="bg-white/20 text-white font-bold text-[10px] sm:text-xs uppercase tracking-wider px-2.5 py-1 rounded-md backdrop-blur-sm">
                Category
              </span>
              <button onclick="speakCurrentCard(event)" title="Listen to Portuguese" class="w-10 h-10 rounded-full bg-white/20 hover:bg-white/30 text-white flex items-center justify-center transition-all transform active:scale-95 backdrop-blur-sm">
                <i class="fa-solid fa-volume-high text-lg"></i>
              </button>
            </div>

            <!-- Content Area -->
            <div class="my-auto py-4">
              <div id="cardEn" class="text-2xl sm:text-3xl font-extrabold text-brand-accent tracking-wide mb-2">
                Loading...
              </div>
              <p class="text-xs text-emerald-200/80 font-medium">English Translation</p>
            </div>

            <!-- Bottom Hint -->
            <div class="text-emerald-200/70 text-xs font-semibold flex items-center gap-1.5">
              <i class="fa-solid fa-rotate"></i>
              <span>Tap card to switch back</span>
            </div>
          </div>

        </div>
      </div>

      <!-- Navigation & Control Buttons -->
      <div class="flex items-center justify-between gap-2 mt-2">
        <button onclick="prevCard()" class="flex-1 bg-white hover:bg-slate-50 text-slate-700 font-bold py-3 px-3 rounded-xl border border-slate-200 shadow-sm transition-all active:scale-95 flex items-center justify-center gap-2 text-xs sm:text-sm">
          <i class="fa-solid fa-chevron-left"></i> Previous
        </button>
        <button onclick="shuffleCards()" class="bg-amber-100 hover:bg-amber-200 text-amber-900 font-bold py-3 px-4 rounded-xl border border-amber-200/80 shadow-sm transition-all active:scale-95 text-xs sm:text-sm flex items-center gap-1.5" title="Shuffle Cards">
          <i class="fa-solid fa-shuffle"></i>
          <span class="hidden sm:inline">Shuffle</span>
        </button>
        <button onclick="nextCard()" class="flex-1 bg-brand-primary hover:bg-brand-dark text-white font-bold py-3 px-3 rounded-xl shadow-md transition-all active:scale-95 flex items-center justify-center gap-2 text-xs sm:text-sm">
          Next <i class="fa-solid fa-chevron-right"></i>
        </button>
      </div>

      <!-- Progress Counter -->
      <div id="progressText" class="text-center text-xs font-semibold text-slate-500 my-1">
        Card 1 of 10
      </div>
    </main>


    <!-- ================= QUIZ MODE ================= -->
    <main id="quizMode" class="hidden flex-grow flex flex-col gap-4">
      
      <!-- Quiz Stats Dashboard -->
      <div class="grid grid-cols-3 gap-2 bg-white p-3 rounded-xl shadow-sm border border-slate-200">
        <div class="text-center border-r border-slate-100">
          <div class="text-[10px] uppercase font-bold text-slate-400">Score</div>
          <div id="quizScore" class="text-lg sm:text-xl font-extrabold text-brand-primary">0</div>
        </div>
        <div class="text-center border-r border-slate-100">
          <div class="text-[10px] uppercase font-bold text-slate-400">Streak 🔥</div>
          <div id="quizStreak" class="text-lg sm:text-xl font-extrabold text-amber-500">0</div>
        </div>
        <div class="text-center">
          <div class="text-[10px] uppercase font-bold text-slate-400">Accuracy</div>
          <div id="quizAccuracy" class="text-lg sm:text-xl font-extrabold text-slate-700">0%</div>
        </div>
      </div>

      <!-- Question Card Container -->
      <div class="bg-white rounded-2xl p-5 shadow-md border border-slate-200 flex flex-col justify-between items-center text-center relative overflow-hidden my-auto min-h-[160px]">
        <div class="w-full flex justify-between items-center mb-2">
          <span class="text-[10px] font-bold uppercase tracking-wider text-slate-400 bg-slate-100 px-2 py-0.5 rounded">
            Translate to English
          </span>
          <button onclick="speakQuizQuestion()" title="Listen Prompt" class="w-8 h-8 rounded-full bg-brand-accent hover:bg-brand-light/40 text-brand-primary flex items-center justify-center transition-transform active:scale-90">
            <i class="fa-solid fa-volume-high text-sm"></i>
          </button>
        </div>

        <div class="my-3">
          <h2 id="quizQuestion" class="text-2xl sm:text-3xl font-extrabold text-brand-dark tracking-wide">
            ---
          </h2>
        </div>

        <div id="quizFeedback" class="text-xs font-bold h-4 transition-all">
          <!-- Feedback message injected dynamically -->
        </div>
      </div>

      <!-- Multiple Choice Options -->
      <div id="quizOptions" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
        <!-- 4 Answer Options Generated via JS -->
      </div>

      <!-- Next Question Button -->
      <button id="quizNextBtn" onclick="nextQuizQuestion()" class="w-full bg-brand-primary hover:bg-brand-dark text-white font-bold py-3 px-4 rounded-xl shadow-md transition-all flex items-center justify-center gap-2 text-sm mt-1 disabled:opacity-50">
        <span>Next Question</span>
        <i class="fa-solid fa-arrow-right"></i>
      </button>

    </main>

    <!-- Message Toast Notification Container -->
    <div id="toast" class="fixed bottom-5 left-1/2 -translate-x-1/2 bg-slate-800 text-white text-xs font-semibold px-4 py-2 rounded-full shadow-lg opacity-0 transition-opacity pointer-events-none z-50 flex items-center gap-2">
      <i class="fa-solid fa-circle-info text-brand-gold"></i>
      <span id="toastMsg">Notification</span>
    </div>

  </div>

  <!-- Footer -->
  <footer class="text-center py-4 text-xs font-medium text-slate-400">
    Brazilian Portuguese Learning Suite • Made for Interactive Practice
  </footer>

  <!-- Application Logic -->
  <script>
    // Initial Flashcard Vocabulary Deck
    const defaultCards = [
      { pt: "Olá, como vai?", en: "Hello, how are you?", cat: "Phrases" },
      { pt: "Muito obrigado", en: "Thank you very much (male)", cat: "Phrases" },
      { pt: "Por favor", en: "Please", cat: "Phrases" },
      { pt: "Com licença", en: "Excuse me", cat: "Phrases" },
      { pt: "Bom dia", en: "Good morning", cat: "Phrases" },
      { pt: "Boa noite", en: "Good evening / night", cat: "Phrases" },
      { pt: "Falar", en: "To speak / talk", cat: "Verbs" },
      { pt: "Gostar", en: "To like", cat: "Verbs" },
      { pt: "Comer", en: "To eat", cat: "Verbs" },
      { pt: "Ir", en: "To go", cat: "Verbs" },
      { pt: "Ter", en: "To have", cat: "Verbs" },
      { pt: "A água", en: "The water", cat: "Nouns" },
      { pt: "O avião", en: "The airplane", cat: "Nouns" },
      { pt: "A comida", en: "The food", cat: "Nouns" },
      { pt: "O amigo", en: "The friend", cat: "Nouns" },
      { pt: "Do (de + o)", en: "Of the / From the (masculine)", cat: "Contractions" },
      { pt: "Na (em + a)", en: "In the / On the (feminine)", cat: "Contractions" },
      { pt: "No (em + o)", en: "In the / On the (masculine)", cat: "Contractions" }
    ];

    // State Variables
    let cards = [...defaultCards];
    let filteredCards = [...cards];
    let currentIndex = 0;
    let currentMode = 'study'; // 'study' or 'quiz'

    // Quiz State
    let quizCurrentCard = null;
    let quizScore = 0;
    let quizTotal = 0;
    let quizStreak = 0;
    let quizAnswered = false;

    // Speech Synthesis setup
    const synth = window.speechSynthesis;
    let ptVoice = null;

    // Fetch optimal Portuguese (Brazil) voice
    function loadVoices() {
      if (!synth) return;
      const voices = synth.getVoices();
      ptVoice = voices.find(v => v.lang.includes('pt-BR')) || 
                voices.find(v => v.lang.includes('pt')) || null;
    }

    if (synth) {
      loadVoices();
      if (speechSynthesis.onvoiceschanged !== undefined) {
        speechSynthesis.onvoiceschanged = loadVoices;
      }
    }

    // Helper: Speak Text via Web Speech API
    function speakText(text) {
      if (!synth) {
        showToast("Audio pronunciation not supported on this browser.");
        return;
      }

      // Cancel ongoing speech
      synth.cancel();

      // Clean string for speech (remove parenthetical notes)
      const cleanText = text.replace(/\s*\(.*?\)\s*/g, '').trim();

      const utterance = new SpeechSynthesisUtterance(cleanText);
      utterance.lang = 'pt-BR';
      utterance.rate = 0.9; // Slightly slower for language learners

      if (ptVoice) {
        utterance.voice = ptVoice;
      }

      utterance.onerror = (e) => {
        console.warn("Speech synthesis error", e);
      };

      synth.speak(utterance);
    }

    // Speak Current Flashcard
    function speakCurrentCard(e) {
      if (e) e.stopPropagation();
      if (filteredCards.length > 0) {
        speakText(filteredCards[currentIndex].pt);
      }
    }

    // Speak Quiz Prompt Question
    function speakQuizQuestion() {
      if (quizCurrentCard) {
        speakText(quizCurrentCard.pt);
      }
    }

    // Switch between Study and Quiz modes
    function switchMode(mode) {
      currentMode = mode;
      const studyEl = document.getElementById('studyMode');
      const quizEl = document.getElementById('quizMode');
      const tabStudy = document.getElementById('tabStudy');
      const tabQuiz = document.getElementById('tabQuiz');

      if (mode === 'study') {
        studyEl.classList.remove('hidden');
        quizEl.classList.add('hidden');

        tabStudy.className = "flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 bg-brand-primary text-white shadow-md";
        tabQuiz.className = "flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 text-slate-600 hover:text-brand-dark";
        updateCard();
      } else {
        studyEl.classList.add('hidden');
        quizEl.classList.remove('hidden');

        tabQuiz.className = "flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 bg-brand-primary text-white shadow-md";
        tabStudy.className = "flex-1 py-2 px-4 rounded-lg font-bold text-sm transition-all duration-200 flex items-center justify-center gap-2 text-slate-600 hover:text-brand-dark";
        
        setupNewQuizQuestion();
      }
    }

    // ================= FLASHCARD FUNCTIONS =================

    function updateCard() {
      const cardEl = document.getElementById('card');
      cardEl.classList.remove('rotate-y-180');

      if (filteredCards.length === 0) {
        document.getElementById('cardPt').innerText = "No cards";
        document.getElementById('cardEn').innerText = "No cards in this category";
        document.getElementById('cardCat').innerText = "-";
        document.getElementById('cardCatBack').innerText = "-";
        document.getElementById('progressText').innerText = "0 of 0";
        return;
      }

      setTimeout(() => {
        const current = filteredCards[currentIndex];
        document.getElementById('cardPt').innerText = current.pt;
        document.getElementById('cardEn').innerText = current.en;
        document.getElementById('cardCat').innerText = current.cat;
        document.getElementById('cardCatBack').innerText = current.cat;
        document.getElementById('progressText').innerText = `Card ${currentIndex + 1} of ${filteredCards.length}`;
      }, 150);
    }

    function flipCard() {
      if (filteredCards.length > 0) {
        document.getElementById('card').classList.toggle('rotate-y-180');
      }
    }

    function nextCard() {
      if (filteredCards.length === 0) return;
      currentIndex = (currentIndex + 1) % filteredCards.length;
      updateCard();
    }

    function prevCard() {
      if (filteredCards.length === 0) return;
      currentIndex = (currentIndex - 1 + filteredCards.length) % filteredCards.length;
      updateCard();
    }

    function shuffleCards() {
      if (filteredCards.length <= 1) return;
      for (let i = filteredCards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [filteredCards[i], filteredCards[j]] = [filteredCards[j], filteredCards[i]];
      }
      currentIndex = 0;
      updateCard();
      showToast("Deck shuffled!");
    }

    function filterCategory() {
      const cat = document.getElementById('categoryFilter').value;
      if (cat === "All") {
        filteredCards = [...cards];
      } else {
        filteredCards = cards.filter(c => c.cat === cat);
      }
      currentIndex = 0;
      updateCard();
    }

    function toggleAddForm() {
      document.getElementById('addForm').classList.toggle('hidden');
    }

    function addCard() {
      const ptInput = document.getElementById('newPt');
      const enInput = document.getElementById('newEn');
      const catInput = document.getElementById('newCat');

      const pt = ptInput.value.trim();
      const en = enInput.value.trim();
      const cat = catInput.value;

      if (!pt || !en) {
        showToast("Please enter both Portuguese & English values.");
        return;
      }

      const newCard = { pt, en, cat };
      cards.push(newCard);

      ptInput.value = '';
      enInput.value = '';
      toggleAddForm();

      // Reset filter to 'All' or match category so user sees their new card
      document.getElementById('categoryFilter').value = cat;
      filterCategory();

      // Navigate to newly added card
      currentIndex = filteredCards.findIndex(c => c.pt === pt && c.en === en);
      if (currentIndex === -1) currentIndex = 0;
      updateCard();

      showToast("New card added successfully!");
    }


    // ================= QUIZ MODE FUNCTIONS =================

    function setupNewQuizQuestion() {
      if (cards.length < 4) {
        showToast("Please add at least 4 flashcards to play Quiz Mode.");
        return;
      }

      quizAnswered = false;
      document.getElementById('quizFeedback').innerText = "";
      document.getElementById('quizFeedback').className = "text-xs font-bold h-4 transition-all";

      // Pick random question card
      const randomIndex = Math.floor(Math.random() * cards.length);
      quizCurrentCard = cards[randomIndex];

      document.getElementById('quizQuestion').innerText = quizCurrentCard.pt;

      // Automatically speak prompt in quiz mode
      speakQuizQuestion();

      // Generate 3 distractors
      const distractors = cards
        .filter(c => c.en !== quizCurrentCard.en)
        .map(c => c.en);

      // Shuffle distractors & select 3
      for (let i = distractors.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [distractors[i], distractors[j]] = [distractors[j], distractors[i]];
      }

      const options = [quizCurrentCard.en, ...distractors.slice(0, 3)];

      // Shuffle options (1 correct + 3 incorrect)
      for (let i = options.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [options[i], options[j]] = [options[j], options[i]];
      }

      // Render options to DOM
      const optionsContainer = document.getElementById('quizOptions');
      optionsContainer.innerHTML = '';

      options.forEach(optionText => {
        const btn = document.createElement('button');
        btn.className = "quiz-opt-btn bg-white hover:bg-slate-50 text-slate-700 font-semibold p-3.5 rounded-xl border border-slate-200 text-xs sm:text-sm text-left shadow-sm transition-all active:scale-[0.98] flex items-center justify-between";
        btn.onclick = () => handleQuizAnswer(optionText, btn);
        
        btn.innerHTML = `
          <span>${optionText}</span>
          <i class="fa-regular fa-circle text-slate-300 status-icon"></i>
        `;
        optionsContainer.appendChild(btn);
      });
    }

    function handleQuizAnswer(selectedOption, clickedBtn) {
      if (quizAnswered) return; // Prevent multiple clicks per question
      quizAnswered = true;

      quizTotal++;
      const isCorrect = selectedOption === quizCurrentCard.en;
      const feedbackEl = document.getElementById('quizFeedback');

      const allOptionButtons = document.querySelectorAll('.quiz-opt-btn');

      if (isCorrect) {
        quizScore++;
        quizStreak++;
        
        clickedBtn.classList.remove('bg-white', 'hover:bg-slate-50', 'text-slate-700', 'border-slate-200');
        clickedBtn.classList.add('bg-emerald-500', 'text-white', 'border-emerald-600', 'shadow-md');
        clickedBtn.querySelector('.status-icon').className = "fa-solid fa-circle-check text-white";

        feedbackEl.innerText = "✨ Excelente! Correct Answer!";
        feedbackEl.className = "text-xs font-bold h-4 text-emerald-600 animate-bounce";
      } else {
        quizStreak = 0;
        
        clickedBtn.classList.remove('bg-white', 'hover:bg-slate-50', 'text-slate-700', 'border-slate-200');
        clickedBtn.classList.add('bg-rose-500', 'text-white', 'border-rose-600');
        clickedBtn.querySelector('.status-icon').className = "fa-solid fa-circle-xmark text-white";

        // Highlight correct answer button
        allOptionButtons.forEach(btn => {
          if (btn.innerText.trim() === quizCurrentCard.en) {
            btn.classList.remove('bg-white', 'text-slate-700');
            btn.classList.add('bg-emerald-100', 'text-emerald-800', 'border-emerald-300', 'font-bold');
            btn.querySelector('.status-icon').className = "fa-solid fa-circle-check text-emerald-600";
          }
        });

        feedbackEl.innerText = `❌ Ops! Correct answer: ${quizCurrentCard.en}`;
        feedbackEl.className = "text-xs font-bold h-4 text-rose-500";
      }

      // Update Quiz Statistics
      document.getElementById('quizScore').innerText = quizScore;
      document.getElementById('quizStreak').innerText = quizStreak;
      const accuracy = Math.round((quizScore / quizTotal) * 100);
      document.getElementById('quizAccuracy').innerText = `${accuracy}%`;
    }

    function nextQuizQuestion() {
      if (!quizAnswered && quizTotal > 0) {
        // Skipped question
        quizStreak = 0;
        document.getElementById('quizStreak').innerText = quizStreak;
      }
      setupNewQuizQuestion();
    }


    // Helper Toast Notification
    let toastTimeout;
    function showToast(msg) {
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toastMsg');
      
      toastMsg.innerText = msg;
      toast.classList.remove('opacity-0');
      toast.classList.add('opacity-100');

      clearTimeout(toastTimeout);
      toastTimeout = setTimeout(() => {
        toast.classList.remove('opacity-100');
        toast.classList.add('opacity-0');
      }, 2500);
    }


    // Initialize Application state on DOM load
    window.onload = function() {
      updateCard();
    };
  </script>
</body>
</html>
```
