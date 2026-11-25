```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>LingoQuest — Learn for free. Forever.</title>
  <!-- Rounded Duolingo-inspired Typography -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@600;700&family=Nunito:wght@600;700;800;900&display=swap" rel="stylesheet" />
  <script src="https://cdn.tailwindcss.com"></script>

  <style>
    :root {
      --duo-green: #58cc02;
      --duo-green-dark: #58a700;
      --duo-green-light: #d7ffb8;
      --duo-blue: #1cb0f6;
      --duo-blue-dark: #1899d6;
      --duo-gold: #ffc800;
      --duo-gold-dark: #e5a500;
      --duo-red: #ff4b4b;
      --duo-red-dark: #ea2b2b;
      --duo-red-light: #ffdfe0;
      --duo-gray-border: #e5e5e5;
      --duo-gray-shadow: #cecece;
      --duo-text: #3c3c3c;
      --duo-muted: #777777;
    }

    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
      user-select: none;
    }

    body {
      font-family: 'Nunito', sans-serif;
      color: var(--duo-text);
      background-color: #f4f7f9;
      margin: 0;
      padding: 0;
      min-height: 100dvh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .brand-font {
      font-family: 'Fredoka', 'Nunito', sans-serif;
    }

    /* Tactile 3D Duolingo-style Buttons */
    .btn-3d {
      position: relative;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      border-radius: 16px;
      transition: transform 0.08s ease, box-shadow 0.08s ease, background-color 0.15s ease;
      cursor: pointer;
    }

    .btn-3d:active:not(:disabled) {
      transform: translateY(4px);
      box-shadow: 0 0px 0 transparent !important;
    }

    .btn-3d:disabled {
      opacity: 0.55;
      cursor: not-allowed;
    }

    .btn-green {
      background-color: var(--duo-green);
      color: #ffffff;
      box-shadow: 0 4px 0 var(--duo-green-dark);
    }

    .btn-green:hover:not(:disabled) {
      background-color: #61e002;
    }

    .btn-white {
      background-color: #ffffff;
      color: var(--duo-green);
      border: 2px solid var(--duo-gray-border);
      box-shadow: 0 4px 0 var(--duo-gray-border);
    }

    .btn-white:hover:not(:disabled) {
      background-color: #f9f9f9;
    }

    .btn-blue {
      background-color: var(--duo-blue);
      color: #ffffff;
      box-shadow: 0 4px 0 var(--duo-blue-dark);
    }

    .btn-red {
      background-color: var(--duo-red);
      color: #ffffff;
      box-shadow: 0 4px 0 var(--duo-red-dark);
    }

    .btn-tile {
      background-color: #ffffff;
      color: var(--duo-text);
      border: 2px solid var(--duo-gray-border);
      box-shadow: 0 3px 0 var(--duo-gray-border);
      border-radius: 14px;
      font-weight: 700;
      transition: all 0.1s ease;
    }

    .btn-tile:active:not(:disabled) {
      transform: translateY(3px);
      box-shadow: 0 0 0 transparent;
    }

    .btn-tile.selected {
      border-color: var(--duo-blue);
      background-color: #ddf4ff;
      color: var(--duo-blue-dark);
      box-shadow: 0 3px 0 var(--duo-blue);
    }

    .btn-tile.matched {
      border-color: var(--duo-green);
      background-color: var(--duo-green-light);
      color: var(--duo-green-dark);
      box-shadow: 0 3px 0 var(--duo-green);
      opacity: 0.65;
      pointer-events: none;
    }

    .btn-tile.wrong-shake {
      border-color: var(--duo-red);
      background-color: var(--duo-red-light);
      color: var(--duo-red-dark);
      animation: shake 0.35s ease;
    }

    /* Mascot Gentle Floating Animation */
    @keyframes mascotBob {
      0%, 100% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-7px) rotate(1.5deg); }
    }

    .mascot-bob {
      animation: mascotBob 2.8s ease-in-out infinite;
    }

    /* Active Lesson Node Pulse Ring */
    @keyframes pulseRing {
      0% { transform: scale(0.95); opacity: 0.85; }
      70% { transform: scale(1.24); opacity: 0; }
      100% { transform: scale(1.24); opacity: 0; }
    }

    .node-pulse::before {
      content: '';
      position: absolute;
      inset: -8px;
      border-radius: 9999px;
      border: 4px solid var(--duo-green);
      animation: pulseRing 2s infinite;
      pointer-events: none;
    }

    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-6px); }
      50% { transform: translateX(6px); }
      75% { transform: translateX(-4px); }
    }

    @keyframes popIn {
      0% { transform: scale(0.85); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    .pop-in {
      animation: popIn 0.22s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 5px;
    }
    ::-webkit-scrollbar-thumb {
      background: #d8dee4;
      border-radius: 9999px;
    }

    /* Confetti Canvas Overlay */
    #confetti-canvas {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 60;
    }
  </style>
</head>
<body>

  <!-- Mobile-First App Shell (Full-bleed on mobile, centered phone frame on desktop) -->
  <div id="app-shell" class="relative w-full max-w-[480px] h-[100dvh] sm:h-[92dvh] sm:max-h-[860px] bg-white sm:rounded-[32px] sm:shadow-2xl sm:border sm:border-slate-200 flex flex-col overflow-hidden">

    <!-- Confetti Canvas for Celebrations -->
    <canvas id="confetti-canvas"></canvas>

    <!-- ========================================================= -->
    <!-- 1. SPLASH / ONBOARDING SCREEN (Matches Reference Aesthetic) -->
    <!-- ========================================================= -->
    <section id="screen-splash" class="flex-1 flex flex-col justify-between px-6 py-8 bg-white z-20">
      <!-- Top Sound Toggle -->
      <div class="flex justify-end">
        <button onclick="toggleSound()" class="sound-toggle-btn p-2.5 rounded-xl border-2 border-slate-200 text-slate-500 hover:bg-slate-50 transition" title="Toggle Sound">
          🔊
        </button>
      </div>

      <!-- Center Mascot & Brand Identity -->
      <div class="flex flex-col items-center text-center my-auto px-2">
        <!-- Custom Cute Green Owl Mascot SVG -->
        <div class="mascot-bob mb-4">
          <svg width="144" height="144" viewBox="0 0 160 160" fill="none" xmlns="http://www.w3.org/2000/svg" aria-label="LingoQuest Owl Mascot">
            <!-- Ground Shadow -->
            <ellipse cx="80" cy="140" rx="44" ry="12" fill="#E5E7EB" />
            <!-- Left & Right Wings -->
            <path d="M36 86C20 92 16 105 24 111C32 117 44 112 48 104L36 86Z" fill="#58CC02" />
            <path d="M124 86C140 92 144 105 136 111C128 117 116 112 112 104L124 86Z" fill="#58CC02" />
            <!-- Feet -->
            <rect x="57" y="130" width="14" height="9" rx="4.5" fill="#FF9600" />
            <rect x="89" y="130" width="14" height="9" rx="4.5" fill="#FF9600" />
            <!-- Main Body & Ears -->
            <path d="M44 52C44 37 54 31 64 36C72 40 88 40 96 36C106 31 116 37 116 52V96C116 121 100 135 80 135C60 135 44 121 44 96V52Z" fill="#58CC02" />
            <!-- Lighter Forehead / Face Mask -->
            <path d="M50 64C50 52 60 47 70 52C75 55 85 55 90 52C100 47 110 52 110 64V88C110 104 97 114 80 114C63 114 50 104 50 88V64Z" fill="#78E01B" />
            <!-- Belly Feathers -->
            <path d="M66 116C69 119 73 119 76 116" stroke="#46A302" stroke-width="3.5" stroke-linecap="round" />
            <path d="M84 116C87 119 91 119 94 116" stroke="#46A302" stroke-width="3.5" stroke-linecap="round" />
            <path d="M75 123C78 126 82 126 85 123" stroke="#46A302" stroke-width="3.5" stroke-linecap="round" />
            <!-- Big Expressive Eyes -->
            <circle cx="65" cy="78" r="15" fill="#FFFFFF" />
            <circle cx="95" cy="78" r="15" fill="#FFFFFF" />
            <!-- Pupils -->
            <circle cx="68" cy="78" r="7.5" fill="#2B2B2B" />
            <circle cx="92" cy="78" r="7.5" fill="#2B2B2B" />
            <!-- Eye Sparkles -->
            <circle cx="70.5" cy="75" r="2.6" fill="#FFFFFF" />
            <circle cx="94.5" cy="75" r="2.6" fill="#FFFFFF" />
            <!-- Orange Beak -->
            <path d="M73 89C73 86 87 86 87 89C87 93 83 98 80 98C77 98 73 93 73 89Z" fill="#FFB100" />
            <path d="M75 89.5C75 88 85 88 85 89.5C85 91.5 82 94 80 94C78 94 75 91.5 75 89.5Z" fill="#FFD04D" />
          </svg>
        </div>

        <h1 class="brand-font text-[38px] font-bold tracking-tight text-[#58cc02] leading-none mb-2">
          lingoquest
        </h1>
        <p class="text-[#777777] text-base font-bold">
          Learn for free. Forever.
        </p>
      </div>

      <!-- Bottom Action Buttons -->
      <div class="flex flex-col gap-3.5 pb-2">
        <button onclick="startAsNewUser()" class="btn-3d btn-green w-full py-4 text-[15px]">
          GET STARTED
        </button>
        <button onclick="openAccountModal()" class="btn-3d btn-white w-full py-4 text-[15px]">
          I ALREADY HAVE AN ACCOUNT
        </button>
      </div>
    </section>

    <!-- ========================================================= -->
    <!-- 2. MAIN APP VIEW (Learn Path, Practice, Profile Tabs)      -->
    <!-- ========================================================= -->
    <section id="screen-main" class="hidden flex-1 flex flex-col overflow-hidden bg-white">
      <!-- Top Status Header -->
      <header class="px-4 py-3 border-b-2 border-slate-100 flex items-center justify-between bg-white z-10">
        <!-- Course Switcher Trigger -->
        <button onclick="openCourseModal()" class="flex items-center gap-2 px-2.5 py-1.5 rounded-xl border-2 border-slate-200 hover:bg-slate-50 transition font-extrabold text-sm text-slate-700">
          <span id="header-course-flag" class="text-xl leading-none">🇮🇹</span>
          <span id="header-course-short" class="hidden xs:inline">Italian</span>
          <svg class="w-4 h-4 text-slate-400" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/></svg>
        </button>

        <!-- Gamification Counters: Streak, XP, Hearts -->
        <div class="flex items-center gap-3.5 font-extrabold text-sm">
          <div class="flex items-center gap-1 text-orange-500" title="Daily Streak">
            <span class="text-lg">🔥</span>
            <span id="stat-streak">1</span>
          </div>
          <div class="flex items-center gap-1 text-amber-500" title="Total XP">
            <span class="text-lg">⚡</span>
            <span id="stat-xp">0</span>
          </div>
          <div class="flex items-center gap-1 text-rose-500" title="Hearts">
            <span class="text-lg">❤️</span>
            <span id="stat-hearts">5</span>
          </div>
          <button onclick="toggleSound()" class="sound-toggle-btn text-base p-1 rounded-lg hover:bg-slate-100" title="Toggle Sound">
            🔊
          </button>
        </div>
      </header>

      <!-- TAB 1: LEARN PATH -->
      <div id="tab-learn" class="flex-1 overflow-y-auto px-4 py-5 pb-24">
        <!-- Unit Banner Card -->
        <div id="unit-banner" class="rounded-2xl p-4 mb-7 text-white shadow-md flex items-center justify-between" style="background-color: #58cc02;">
          <div>
            <p class="text-xs font-extrabold uppercase tracking-wider opacity-85" id="unit-subtitle">UNIT 1 • SECTION 1</p>
            <h2 class="text-lg font-black leading-snug" id="unit-title">Essential Foundations</h2>
          </div>
          <button onclick="openCourseModal()" class="bg-white/20 hover:bg-white/30 px-3 py-2 rounded-xl text-xs font-extrabold uppercase tracking-wide transition">
            Switch
          </button>
        </div>

        <!-- Winding Skill Path Nodes -->
        <div id="skill-path-container" class="flex flex-col items-center gap-7 py-2 relative">
          <!-- Dynamically rendered circular lesson nodes -->
        </div>
      </div>

      <!-- TAB 2: PRACTICE / QUICK REVIEW -->
      <div id="tab-practice" class="hidden flex-1 overflow-y-auto px-5 py-6 pb-24">
        <h2 class="text-2xl font-black text-slate-800 mb-1">Daily Practice</h2>
        <p class="text-sm font-bold text-slate-500 mb-6">Sharpen your memory and earn bonus XP.</p>

        <div class="space-y-4">
          <div class="p-4 rounded-2xl border-2 border-slate-200 flex items-center justify-between gap-4">
            <div class="flex items-center gap-3.5">
              <div class="w-12 h-12 rounded-2xl bg-sky-100 text-sky-600 flex items-center justify-center text-2xl">🎯</div>
              <div>
                <h3 class="font-extrabold text-slate-800">Rapid Review</h3>
                <p class="text-xs font-bold text-slate-500">Mix of completed & active skills</p>
              </div>
            </div>
            <button onclick="startQuickPractice()" class="btn-3d btn-blue px-4 py-2.5 text-xs">START</button>
          </div>

          <div class="p-4 rounded-2xl border-2 border-slate-200 flex items-center justify-between gap-4">
            <div class="flex items-center gap-3.5">
              <div class="w-12 h-12 rounded-2xl bg-rose-100 text-rose-500 flex items-center justify-center text-2xl">❤️</div>
              <div>
                <h3 class="font-extrabold text-slate-800">Refill Hearts</h3>
                <p class="text-xs font-bold text-slate-500">Restore full 5 hearts anytime</p>
              </div>
            </div>
            <button onclick="refillHearts()" class="btn-3d btn-green px-4 py-2.5 text-xs">REFILL</button>
          </div>
        </div>

        <div class="mt-8 p-4 rounded-2xl bg-amber-50 border-2 border-amber-200">
          <div class="flex items-center gap-3">
            <span class="text-3xl">🦉</span>
            <div>
              <p class="font-extrabold text-amber-900 text-sm">Pro Tip from Duo</p>
              <p class="text-xs font-bold text-amber-800/80 mt-0.5">On desktop, you can press keys 1–4 for multiple choice and Enter to submit or continue!</p>
            </div>
          </div>
        </div>
      </div>

      <!-- TAB 3: PROFILE & PROGRESS -->
      <div id="tab-profile" class="hidden flex-1 overflow-y-auto px-5 py-6 pb-24">
        <div class="flex items-center gap-4 mb-6">
          <div class="w-16 h-16 rounded-2xl bg-[#58cc02] flex items-center justify-center text-3xl shadow-sm text-white font-black" id="profile-avatar">
            🦉
          </div>
          <div>
            <h2 class="text-xl font-black text-slate-800" id="profile-name">Explorer Learner</h2>
            <p class="text-xs font-bold text-slate-400">Joined 2026 • Free Tier Forever</p>
          </div>
        </div>

        <!-- Statistics Grid -->
        <h3 class="text-sm font-black uppercase tracking-wider text-slate-400 mb-3">Your Statistics</h3>
        <div class="grid grid-cols-2 gap-3 mb-6">
          <div class="p-3.5 rounded-2xl border-2 border-slate-200 flex items-center gap-3">
            <span class="text-2xl">🔥</span>
            <div>
              <p class="font-black text-slate-800 text-lg leading-none" id="prof-streak">1</p>
              <p class="text-xs font-bold text-slate-400 mt-1">Day streak</p>
            </div>
          </div>
          <div class="p-3.5 rounded-2xl border-2 border-slate-200 flex items-center gap-3">
            <span class="text-2xl">⚡</span>
            <div>
              <p class="font-black text-slate-800 text-lg leading-none" id="prof-xp">0</p>
              <p class="text-xs font-bold text-slate-400 mt-1">Total XP</p>
            </div>
          </div>
          <div class="p-3.5 rounded-2xl border-2 border-slate-200 flex items-center gap-3">
            <span class="text-2xl">🏆</span>
            <div>
              <p class="font-black text-slate-800 text-lg leading-none" id="prof-completed">0</p>
              <p class="text-xs font-bold text-slate-400 mt-1">Lessons done</p>
            </div>
          </div>
          <div class="p-3.5 rounded-2xl border-2 border-slate-200 flex items-center gap-3">
            <span class="text-2xl">📚</span>
            <div>
              <p class="font-black text-slate-800 text-lg leading-none">3</p>
              <p class="text-xs font-bold text-slate-400 mt-1">Courses active</p>
            </div>
          </div>
        </div>

        <!-- Settings & Reset -->
        <h3 class="text-sm font-black uppercase tracking-wider text-slate-400 mb-3">Account & Storage</h3>
        <div class="space-y-3">
          <button onclick="showSplashScreen()" class="btn-3d btn-white w-full py-3.5 text-xs">
            BACK TO WELCOME SCREEN
          </button>
          <button onclick="confirmResetModal()" class="btn-3d btn-red w-full py-3.5 text-xs">
            RESET ALL PROGRESS
          </button>
        </div>
      </div>

      <!-- Bottom Navigation Bar -->
      <nav class="border-t-2 border-slate-100 bg-white px-4 py-2 flex justify-around items-center z-10">
        <button onclick="switchTab('learn')" id="nav-learn" class="nav-btn flex flex-col items-center gap-1 px-4 py-1.5 rounded-xl border-2 border-sky-300 bg-sky-50 text-sky-600 transition">
          <span class="text-xl leading-none">🏠</span>
          <span class="text-[11px] font-extrabold uppercase">Learn</span>
        </button>
        <button onclick="switchTab('practice')" id="nav-practice" class="nav-btn flex flex-col items-center gap-1 px-4 py-1.5 rounded-xl border-2 border-transparent text-slate-400 hover:bg-slate-50 transition">
          <span class="text-xl leading-none">🏋️</span>
          <span class="text-[11px] font-extrabold uppercase">Practice</span>
        </button>
        <button onclick="switchTab('profile')" id="nav-profile" class="nav-btn flex flex-col items-center gap-1 px-4 py-1.5 rounded-xl border-2 border-transparent text-slate-400 hover:bg-slate-50 transition">
          <span class="text-xl leading-none">👤</span>
          <span class="text-[11px] font-extrabold uppercase">Profile</span>
        </button>
      </nav>
    </section>

    <!-- ========================================================= -->
    <!-- 3. INTERACTIVE LESSON ENGINE SCREEN                       -->
    <!-- ========================================================= -->
    <section id="screen-lesson" class="hidden flex-1 flex flex-col bg-white z-30 overflow-hidden">
      <!-- Lesson Top Progress Header -->
      <div class="px-4 pt-4 pb-2 flex items-center gap-3">
        <button onclick="exitLesson()" class="p-2 text-slate-400 hover:text-slate-600 rounded-xl hover:bg-slate-100 transition" aria-label="Quit lesson">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/></svg>
        </button>

        <!-- Smooth Animated Progress Bar -->
        <div class="flex-1 h-4 bg-slate-200 rounded-full overflow-hidden p-0.5">
          <div id="lesson-progress-bar" class="h-full bg-[#58cc02] rounded-full transition-all duration-300 relative" style="width: 10%;">
            <div class="h-1 bg-white/30 rounded-full mx-2 mt-0.5"></div>
          </div>
        </div>

        <!-- Lesson Hearts -->
        <div class="flex items-center gap-1 font-extrabold text-rose-500 text-base">
          <span>❤️</span>
          <span id="lesson-hearts">5</span>
        </div>
      </div>

      <!-- Question Workspace -->
      <div id="question-area" class="flex-1 overflow-y-auto px-5 py-4 flex flex-col">
        <p id="q-type-label" class="text-xs font-extrabold uppercase tracking-wider text-sky-500 mb-1">Select the correct answer</p>
        <h2 id="q-prompt" class="text-xl font-black text-slate-800 mb-5 leading-snug">Question prompt goes here</h2>

        <!-- Dynamic Answer Interface (Multiple Choice / Word Bank / Match Pairs) -->
        <div id="q-interactive-body" class="flex-1 flex flex-col justify-center"></div>
      </div>

      <!-- Bottom Check / Feedback Footer -->
      <div id="lesson-footer" class="px-5 py-4 border-t-2 border-slate-100 bg-white transition-colors duration-200">
        <!-- Feedback Message Banner (Hidden until Checked) -->
        <div id="feedback-banner" class="hidden mb-3.5">
          <div class="flex items-center gap-2.5">
            <div id="feedback-icon" class="w-8 h-8 rounded-full flex items-center justify-center font-black text-white text-base">✓</div>
            <div>
              <p id="feedback-title" class="font-black text-lg leading-tight">Nicely done!</p>
              <p id="feedback-detail" class="text-xs font-bold mt-0.5"></p>
            </div>
          </div>
        </div>

        <button id="lesson-action-btn" onclick="handleLessonAction()" disabled class="btn-3d btn-green w-full py-3.5 text-[15px]">
          CHECK
        </button>
      </div>
    </section>

    <!-- ========================================================= -->
    <!-- 4. LESSON COMPLETE CELEBRATION SCREEN                     -->
    <!-- ========================================================= -->
    <section id="screen-complete" class="hidden flex-1 flex flex-col justify-between px-6 py-8 bg-white z-40 text-center">
      <div class="my-auto flex flex-col items-center pop-in">
        <div class="text-7xl mb-4 mascot-bob">🎉</div>
        <h2 class="brand-font text-3xl font-bold text-[#ffc800] drop-shadow-sm mb-1">Lesson Complete!</h2>
        <p class="text-sm font-bold text-slate-500 mb-7" id="complete-subtitle">You're making awesome progress!</p>

        <div class="grid grid-cols-3 gap-3 w-full">
          <div class="rounded-2xl border-2 border-amber-400 bg-amber-50 p-3">
            <p class="text-[11px] font-black uppercase text-amber-600">Total XP</p>
            <p class="text-xl font-black text-amber-500 mt-1" id="complete-xp">+50</p>
          </div>
          <div class="rounded-2xl border-2 border-emerald-400 bg-emerald-50 p-3">
            <p class="text-[11px] font-black uppercase text-emerald-600">Accuracy</p>
            <p class="text-xl font-black text-emerald-500 mt-1" id="complete-acc">100%</p>
          </div>
          <div class="rounded-2xl border-2 border-orange-400 bg-orange-50 p-3">
            <p class="text-[11px] font-black uppercase text-orange-600">Streak</p>
            <p class="text-xl font-black text-orange-500 mt-1" id="complete-streak">🔥 1</p>
          </div>
        </div>
      </div>

      <button onclick="finishLessonFlow()" class="btn-3d btn-green w-full py-4 text-[15px]">
        CONTINUE
      </button>
    </section>

    <!-- ========================================================= -->
    <!-- MODALS (Course Switcher, Account Demo, Reset Confirmation)-->
    <!-- ========================================================= -->
    <div id="modal-backdrop" class="hidden absolute inset-0 bg-slate-900/50 backdrop-blur-[1px] z-50 flex items-end sm:items-center justify-center p-4">
      <div id="modal-content" class="bg-white w-full rounded-3xl p-5 shadow-2xl pop-in border-2 border-slate-100">
        <!-- Populated dynamically -->
      </div>
    </div>

    <!-- Non-blocking Toast Message -->
    <div id="toast-box" class="hidden absolute top-16 left-1/2 -translate-x-1/2 bg-slate-800 text-white text-xs font-extrabold px-4 py-2.5 rounded-2xl shadow-lg z-50 whitespace-nowrap">
      Message
    </div>

  </div>

  <script>
    /* =========================================================================
       1. CURRICULUM DATA (Multiple Subjects: Language, Biology, AI & Tech)
       ========================================================================= */
    const COURSES = {
      italian: {
        id: 'italian',
        name: 'Italian Basics',
        shortName: 'Italian',
        flag: '🇮🇹',
        color: '#58cc02',
        unitTitle: 'Greetings & Daily Café',
        lessons: [
          {
            id: 'it-1',
            title: 'Basic Greetings',
            icon: '👋',
            questions: [
              {
                type: 'mc',
                prompt: 'How do you say "Hello / Goodbye" casually in Italian?',
                options: ['Ciao', 'Grazie', 'Per favore', 'Acqua'],
                answer: 'Ciao'
              },
              {
                type: 'wordbank',
                prompt: 'Translate: "Good morning, friend"',
                words: ['Buongiorno', 'amico', 'notte', 'pane', 'grazie'],
                answer: ['Buongiorno', 'amico']
              },
              {
                type: 'match',
                prompt: 'Tap the matching pairs',
                pairs: [
                  { left: 'Grazie', right: 'Thank you' },
                  { left: 'Sì', right: 'Yes' },
                  { left: 'Per favore', right: 'Please' },
                  { left: 'Buonanotte', right: 'Good night' }
                ]
              },
              {
                type: 'mc',
                prompt: 'Which word means "Thank you very much"?',
                options: ['Prego', 'Grazie mille', 'Scusa', 'Arrivederci'],
                answer: 'Grazie mille'
              },
              {
                type: 'wordbank',
                prompt: 'Build the phrase: "See you soon"',
                words: ['A', 'presto', 'ciao', 'sono', 'io'],
                answer: ['A', 'presto']
              }
            ]
          },
          {
            id: 'it-2',
            title: 'At the Café',
            icon: '☕',
            questions: [
              {
                type: 'mc',
                prompt: 'What does "Un caffè, per favore" mean?',
                options: ['One water, please', 'A coffee, please', 'The bill, please', 'Two apples'],
                answer: 'A coffee, please'
              },
              {
                type: 'wordbank',
                prompt: 'Translate: "Water and bread"',
                words: ['Acqua', 'e', 'pane', 'latte', 'vino'],
                answer: ['Acqua', 'e', 'pane']
              },
              {
                type: 'match',
                prompt: 'Match the Italian food words',
                pairs: [
                  { left: 'Acqua', right: 'Water' },
                  { left: 'Pane', right: 'Bread' },
                  { left: 'Latte', right: 'Milk' },
                  { left: 'Mela', right: 'Apple' }
                ]
              },
              {
                type: 'mc',
                prompt: 'How do you say "Excuse me" to get attention?',
                options: ['Mi dispiace', 'Scusi', 'Bene', 'Ciao'],
                answer: 'Scusi'
              },
              {
                type: 'wordbank',
                prompt: 'Translate: "I would like tea"',
                words: ['Vorrei', 'un', 'tè', 'acqua', 'tu'],
                answer: ['Vorrei', 'un', 'tè']
              }
            ]
          },
          {
            id: 'it-3',
            title: 'People & Travel',
            icon: '🚆',
            questions: [
              {
                type: 'mc',
                prompt: 'What is "The train station" in Italian?',
                options: ['La stazione', 'Il museo', 'La spiaggia', 'Il libro'],
                answer: 'La stazione'
              },
              {
                type: 'wordbank',
                prompt: 'Translate: "Where is the hotel?"',
                words: ['Dov’è', 'l’albergo?', 'Come', 'stai', 'qui'],
                answer: ['Dov’è', 'l’albergo?']
              },
              {
                type: 'match',
                prompt: 'Match travel essentials',
                pairs: [
                  { left: 'Biglietto', right: 'Ticket' },
                  { left: 'Treno', right: 'Train' },
                  { left: 'Sinistra', right: 'Left' },
                  { left: 'Destra', right: 'Right' }
                ]
              },
              {
                type: 'mc',
                prompt: 'Which word means "Airport"?',
                options: ['Aeroporto', 'Ospedale', 'Mercato', 'Piazza'],
                answer: 'Aeroporto'
              },
              {
                type: 'wordbank',
                prompt: 'Translate: "I am in Rome"',
                words: ['Io', 'sono', 'a', 'Roma', 'tu'],
                answer: ['Io', 'sono', 'a', 'Roma']
              }
            ]
          }
        ]
      },
      biology: {
        id: 'biology',
        name: 'Biology & Micro-Life',
        shortName: 'Biology',
        flag: '🧬',
        color: '#1cb0f6',
        unitTitle: 'Cells & Microorganisms',
        lessons: [
          {
            id: 'bio-1',
            title: 'Cell Powerhouses',
            icon: '🔬',
            questions: [
              {
                type: 'mc',
                prompt: 'Which organelle generates most chemical energy (ATP) in eukaryotic cells?',
                options: ['Mitochondria', 'Ribosome', 'Golgi body', 'Lysosome'],
                answer: 'Mitochondria'
              },
              {
                type: 'wordbank',
                prompt: 'Complete: "DNA carries genetic ____"',
                words: ['instructions', 'for', 'life', 'oxygen', 'rocks'],
                answer: ['instructions', 'for', 'life']
              },
              {
                type: 'match',
                prompt: 'Match each cell structure to its role',
                pairs: [
                  { left: 'Nucleus', right: 'Stores DNA' },
                  { left: 'Ribosome', right: 'Builds proteins' },
                  { left: 'Chloroplast', right: 'Photosynthesis' },
                  { left: 'Membrane', right: 'Controls entry' }
                ]
              },
              {
                type: 'mc',
                prompt: 'Which molecule stores hereditary information in almost all organisms?',
                options: ['DNA', 'Glucose', 'Cholesterol', 'Keratin'],
                answer: 'DNA'
              },
              {
                type: 'wordbank',
                prompt: 'Assemble: "Plants convert sunlight into energy"',
                words: ['Plants', 'convert', 'sunlight', 'into', 'energy'],
                answer: ['Plants', 'convert', 'sunlight', 'into', 'energy']
              }
            ]
          },
          {
            id: 'bio-2',
            title: 'Bacteria & Viruses',
            icon: '🦠',
            questions: [
              {
                type: 'mc',
                prompt: 'How do bacteria primarily reproduce?',
                options: ['Binary fission', 'Mitosis with spindle fibers', 'Seed dispersal', 'Spore pollination'],
                answer: 'Binary fission'
              },
              {
                type: 'match',
                prompt: 'Match the microbe concepts',
                pairs: [
                  { left: 'Prokaryote', right: 'No true nucleus' },
                  { left: 'Antibiotic', right: 'Targets bacteria' },
                  { left: 'Capsid', right: 'Viral protein shell' },
                  { left: 'Vaccine', right: 'Trains immunity' }
                ]
              },
              {
                type: 'wordbank',
                prompt: 'Build statement: "Viruses require a host cell"',
                words: ['Viruses', 'require', 'a', 'host', 'cell'],
                answer: ['Viruses', 'require', 'a', 'host', 'cell']
              },
              {
                type: 'mc',
                prompt: 'Why are antibiotics ineffective against the common cold?',
                options: ['Colds are caused by viruses', 'Viruses have thick cell walls', 'Bacteria eat antibiotics', 'Colds only affect bones'],
                answer: 'Colds are caused by viruses'
              },
              {
                type: 'mc',
                prompt: 'Which beneficial bacteria live in the human gut?',
                options: ['Microbiome flora', 'Bacteriophages', 'Prions', 'Amoebas'],
                answer: 'Microbiome flora'
              }
            ]
          }
        ]
      },
      ai: {
        id: 'ai',
        name: 'AI & Neural Tech',
        shortName: 'AI Tech',
        flag: '🤖',
        color: '#a560e8',
        unitTitle: 'How AI Models Learn',
        lessons: [
          {
            id: 'ai-1',
            title: 'Tokens & Transformers',
            icon: '🧠',
            questions: [
              {
                type: 'mc',
                prompt: 'What are the basic chunks of text that Large Language Models process?',
                options: ['Tokens', 'Pixels', 'Voxels', 'Packets'],
                answer: 'Tokens'
              },
              {
                type: 'wordbank',
                prompt: 'Complete: "Transformers use self-attention layers"',
                words: ['Transformers', 'use', 'self-attention', 'layers', 'gears'],
                answer: ['Transformers', 'use', 'self-attention', 'layers']
              },
              {
                type: 'match',
                prompt: 'Match AI concepts to definitions',
                pairs: [
                  { left: 'Prompt', right: 'User input text' },
                  { left: 'Weights', right: 'Learned parameters' },
                  { left: 'Training', right: 'Pattern learning' },
                  { left: 'Inference', right: 'Generating output' }
                ]
              },
              {
                type: 'mc',
                prompt: 'What does "LLM" stand for in modern AI?',
                options: ['Large Language Model', 'Linear Logic Machine', 'Local Learning Memory', 'Layered Link Module'],
                answer: 'Large Language Model'
              },
              {
                type: 'wordbank',
                prompt: 'Assemble: "Neural networks learn from data"',
                words: ['Neural', 'networks', 'learn', 'from', 'data'],
                answer: ['Neural', 'networks', 'learn', 'from', 'data']
              }
            ]
          }
        ]
      }
    };

    /* =========================================================================
       2. STATE MANAGEMENT & LOCALSTORAGE PERSISTENCE
       ========================================================================= */
    const STORAGE_KEY = 'lingoquest_state_v1';

    const defaultState = {
      hasOnboarded: false,
      userName: 'Explorer Learner',
      activeCourse: 'italian',
      xp: 0,
      streak: 1,
      hearts: 5,
      soundEnabled: true,
      completedLessons: [] // array of lesson IDs e.g. ['it-1']
    };

    let state = loadState();

    function loadState() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (!raw) return { ...defaultState };
        return { ...defaultState, ...JSON.parse(raw) };
      } catch (e) {
        return { ...defaultState };
      }
    }

    function saveState() {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
      } catch (e) {
        console.warn('Storage unavailable', e);
      }
    }

    /* =========================================================================
       3. WEB AUDIO API SOUND EFFECTS (Zero External Dependencies)
       ========================================================================= */
    let audioCtx = null;

    function playTone(type) {
      if (!state.soundEnabled) return;
      try {
        if (!audioCtx) {
          audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }
        if (audioCtx.state === 'suspended') audioCtx.resume();

        const now = audioCtx.currentTime;
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.connect(gain);
        gain.connect(audioCtx.destination);

        if (type === 'tap') {
          osc.type = 'sine';
          osc.frequency.setValueAtTime(520, now);
          osc.frequency.exponentialRampToValueAtTime(640, now + 0.06);
          gain.gain.setValueAtTime(0.08, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.06);
          osc.start(now);
          osc.stop(now + 0.06);
        } else if (type === 'correct') {
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(523.25, now); // C5
          osc.frequency.setValueAtTime(659.25, now + 0.09); // E5
          osc.frequency.setValueAtTime(783.99, now + 0.18); // G5
          gain.gain.setValueAtTime(0.14, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.36);
          osc.start(now);
          osc.stop(now + 0.36);
        } else if (type === 'wrong') {
          osc.type = 'sawtooth';
          osc.frequency.setValueAtTime(210, now);
          osc.frequency.linearRampToValueAtTime(145, now + 0.25);
          gain.gain.setValueAtTime(0.1, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.28);
          osc.start(now);
          osc.stop(now + 0.28);
        } else if (type === 'fanfare') {
          const notes = [523.25, 659.25, 783.99, 1046.5];
          notes.forEach((freq, i) => {
            const o = audioCtx.createOscillator();
            const g = audioCtx.createGain();
            o.type = 'triangle';
            o.connect(g);
            g.connect(audioCtx.destination);
            o.frequency.setValueAtTime(freq, now + i * 0.1);
            g.gain.setValueAtTime(0.13, now + i * 0.1);
            g.gain.exponentialRampToValueAtTime(0.001, now + i * 0.1 + 0.35);
            o.start(now + i * 0.1);
            o.stop(now + i * 0.1 + 0.35);
          });
        }
      } catch (e) {
        // Ignore audio errors on restricted devices
      }
    }

    function toggleSound() {
      state.soundEnabled = !state.soundEnabled;
      saveState();
      updateSoundIcons();
      if (state.soundEnabled) playTone('tap');
      showToast(state.soundEnabled ? 'Sound effects ON' : 'Sound effects MUTED');
    }

    function updateSoundIcons() {
      document.querySelectorAll('.sound-toggle-btn').forEach(btn => {
        btn.textContent = state.soundEnabled ? '🔊' : '🔇';
      });
    }

    /* =========================================================================
       4. NAVIGATION & HOME SCREEN RENDERING
       ========================================================================= */
    function showScreen(screenId) {
      ['screen-splash', 'screen-main', 'screen-lesson', 'screen-complete'].forEach(id => {
        document.getElementById(id).classList.add('hidden');
      });
      document.getElementById(screenId).classList.remove('hidden');
    }

    function showSplashScreen() {
      playTone('tap');
      showScreen('screen-splash');
    }

    function startAsNewUser() {
      playTone('correct');
      state.hasOnboarded = true;
      saveState();
      enterMainApp();
    }

    function enterMainApp() {
      showScreen('screen-main');
      renderHomeUI();
    }

    function switchTab(tabName) {
      playTone('tap');
      ['tab-learn', 'tab-practice', 'tab-profile'].forEach(id => {
        document.getElementById(id).classList.add('hidden');
      });
      document.getElementById(`tab-${tabName}`).classList.remove('hidden');

      document.querySelectorAll('.nav-btn').forEach(btn => {
        btn.classList.remove('border-sky-300', 'bg-sky-50', 'text-sky-600');
        btn.classList.add('border-transparent', 'text-slate-400');
      });
      const activeNav = document.getElementById(`nav-${tabName}`);
      activeNav.classList.remove('border-transparent', 'text-slate-400');
      activeNav.classList.add('border-sky-300', 'bg-sky-50', 'text-sky-600');

      if (tabName === 'profile') renderProfileStats();
    }

    function renderHomeUI() {
      const course = COURSES[state.activeCourse] || COURSES.italian;

      // Top Header Counters
      document.getElementById('header-course-flag').textContent = course.flag;
      document.getElementById('header-course-short').textContent = course.shortName;
      document.getElementById('stat-streak').textContent = state.streak;
      document.getElementById('stat-xp').textContent = state.xp;
      document.getElementById('stat-hearts').textContent = state.hearts;

      // Unit Banner
      const banner = document.getElementById('unit-banner');
      banner.style.backgroundColor = course.color;
      document.getElementById('unit-subtitle').textContent = `${course.name.toUpperCase()} • UNIT 1`;
      document.getElementById('unit-title').textContent = course.unitTitle;

      // Winding Skill Path
      const pathContainer = document.getElementById('skill-path-container');
      pathContainer.innerHTML = '';

      // Winding horizontal offsets mimicking Duolingo's curved path
      const offsets = [0, -42, 42, -24, 32];
      let foundFirstIncomplete = false;

      course.lessons.forEach((lesson, idx) => {
        const isCompleted = state.completedLessons.includes(lesson.id);
        let status = 'locked';

        if (isCompleted) {
          status = 'completed';
        } else if (!foundFirstIncomplete) {
          status = 'active';
          foundFirstIncomplete = true;
        }

        const offsetX = offsets[idx % offsets.length];
        const wrapper = document.createElement('div');
        wrapper.className = 'flex flex-col items-center relative';
        wrapper.style.transform = `translateX(${offsetX}px)`;

        let circleClasses = '';
        let badgeHTML = '';

        if (status === 'completed') {
          circleClasses = 'bg-[#ffc800] border-[#e5a500] text-white shadow-[0_6px_0_#e5a500]';
          badgeHTML = `<span class="absolute -top-2 -right-2 bg-white text-amber-500 text-xs font-black px-1.5 py-0.5 rounded-full border-2 border-amber-300 shadow-sm">★</span>`;
        } else if (status === 'active') {
          circleClasses = 'node-pulse bg-[#58cc02] border-[#58a700] text-white shadow-[0_6px_0_#58a700]';
          badgeHTML = `<span class="absolute -top-7 bg-white text-[#58cc02] text-[11px] font-black uppercase tracking-wider px-3 py-1 rounded-xl border-2 border-slate-200 shadow-sm animate-bounce">START</span>`;
        } else {
          circleClasses = 'bg-slate-200 border-slate-300 text-slate-400 shadow-[0_6px_0_#cbd5e1] cursor-not-allowed';
        }

        const btn = document.createElement('button');
        btn.className = `relative w-20 h-20 rounded-full flex items-center justify-center text-3xl transition active:translate-y-1 ${circleClasses}`;
        btn.innerHTML = `${badgeHTML}<span>${status === 'locked' ? '🔒' : lesson.icon}</span>`;

        btn.onclick = () => {
          if (status === 'locked') {
            playTone('wrong');
            showToast('Complete the previous lesson first!');
          } else {
            launchLesson(lesson);
          }
        };

        const label = document.createElement('span');
        label.className = `mt-2.5 text-xs font-extrabold ${status === 'locked' ? 'text-slate-400' : 'text-slate-700'}`;
        label.textContent = lesson.title;

        wrapper.appendChild(btn);
        wrapper.appendChild(label);
        pathContainer.appendChild(wrapper);
      });

      // Mascot encouragement at bottom of path
      const endCard = document.createElement('div');
      endCard.className = 'mt-4 p-4 rounded-2xl border-2 border-dashed border-slate-200 text-center max-w-[260px]';
      endCard.innerHTML = `
        <p class="text-2xl mb-1">🦉</p>
        <p class="text-xs font-extrabold text-slate-500">More units unlock as you master each skill!</p>
      `;
      pathContainer.appendChild(endCard);
    }

    function renderProfileStats() {
      document.getElementById('profile-name').textContent = state.userName;
      document.getElementById('prof-streak').textContent = state.streak;
      document.getElementById('prof-xp').textContent = state.xp;
      document.getElementById('prof-completed').textContent = state.completedLessons.length;
    }

    function refillHearts() {
      playTone('correct');
      state.hearts = 5;
      saveState();
      renderHomeUI();
      showToast('Hearts refilled to ❤️ 5!');
    }

    /* =========================================================================
       5. INTERACTIVE LESSON ENGINE
       ========================================================================= */
    let currentSession = null;

    function launchLesson(lesson, isQuickPractice = false) {
      if (state.hearts <= 0) {
        playTone('wrong');
        showToast('Out of hearts! Refill in Practice tab ❤️');
        switchTab('practice');
        return;
      }

      playTone('tap');
      currentSession = {
        lessonId: lesson.id,
        isQuickPractice,
        questions: JSON.parse(JSON.stringify(lesson.questions)),
        index: 0,
        correctCount: 0,
        earnedXP: 0,
        checked: false,
        userSelection: null,
        wordBankSelected: [],
        matchState: {
          selectedLeft: null,
          selectedRight: null,
          matchedLefts: [],
          matchedRights: []
        }
      };

      showScreen('screen-lesson');
      renderCurrentQuestion();
    }

    function startQuickPractice() {
      const course = COURSES[state.activeCourse] || COURSES.italian;
      const pool = course.lessons.flatMap(l => l.questions);
      const shuffled = pool.sort(() => Math.random() - 0.5).slice(0, 5);
      launchLesson({ id: 'practice-mix', questions: shuffled }, true);
    }

    function exitLesson() {
      playTone('tap');
      currentSession = null;
      enterMainApp();
    }

    function renderCurrentQuestion() {
      const q = currentSession.questions[currentSession.index];
      const total = currentSession.questions.length;
      const pct = Math.max(8, Math.round((currentSession.index / total) * 100));

      document.getElementById('lesson-progress-bar').style.width = `${pct}%`;
      document.getElementById('lesson-hearts').textContent = state.hearts;

      // Reset Footer
      currentSession.checked = false;
      currentSession.userSelection = null;
      currentSession.wordBankSelected = [];

      const footer = document.getElementById('lesson-footer');
      footer.className = 'px-5 py-4 border-t-2 border-slate-100 bg-white transition-colors duration-200';
      document.getElementById('feedback-banner').classList.add('hidden');

      const actionBtn = document.getElementById('lesson-action-btn');
      actionBtn.textContent = 'CHECK';
      actionBtn.className = 'btn-3d btn-green w-full py-3.5 text-[15px]';
      actionBtn.disabled = true;

      const body = document.getElementById('q-interactive-body');
      body.innerHTML = '';

      if (q.type === 'mc') {
        document.getElementById('q-type-label').textContent = 'Select the correct answer';
        document.getElementById('q-prompt').textContent = q.prompt;

        const list = document.createElement('div');
        list.className = 'flex flex-col gap-3';

        q.options.forEach((opt, idx) => {
          const btn = document.createElement('button');
          btn.className = 'mc-option btn-tile w-full p-4 text-left flex items-center gap-3.5 text-[15px]';
          btn.innerHTML = `
            <span class="w-7 h-7 rounded-lg border-2 border-slate-200 flex items-center justify-center text-xs font-extrabold text-slate-400 shrink-0">${idx + 1}</span>
            <span class="font-extrabold">${opt}</span>
          `;
          btn.onclick = () => {
            if (currentSession.checked) return;
            playTone('tap');
            document.querySelectorAll('.mc-option').forEach(el => el.classList.remove('selected'));
            btn.classList.add('selected');
            currentSession.userSelection = opt;
            actionBtn.disabled = false;
          };
          list.appendChild(btn);
        });

        body.appendChild(list);
      } else if (q.type === 'wordbank') {
        document.getElementById('q-type-label').textContent = 'Tap the tiles in order';
        document.getElementById('q-prompt').textContent = q.prompt;

        // Answer Tray
        const tray = document.createElement('div');
        tray.id = 'wb-tray';
        tray.className = 'min-h-[68px] p-3 mb-6 rounded-2xl border-2 border-dashed border-slate-300 bg-slate-50 flex flex-wrap gap-2 items-center';

        // Word Bank Pool
        const pool = document.createElement('div');
        pool.id = 'wb-pool';
        pool.className = 'flex flex-wrap justify-center gap-2.5';

        const shuffledWords = [...q.words].sort(() => Math.random() - 0.5);

        function refreshWordBank() {
          tray.innerHTML = '';
          if (currentSession.wordBankSelected.length === 0) {
            tray.innerHTML = `<span class="text-xs font-bold text-slate-400 px-1">Tap words below to build your answer...</span>`;
          } else {
            currentSession.wordBankSelected.forEach((item, idx) => {
              const chip = document.createElement('button');
              chip.className = 'btn-tile px-3.5 py-2 text-sm font-extrabold';
              chip.textContent = item.word;
              chip.onclick = () => {
                if (currentSession.checked) return;
                playTone('tap');
                currentSession.wordBankSelected.splice(idx, 1);
                refreshWordBank();
              };
              tray.appendChild(chip);
            });
          }

          pool.innerHTML = '';
          shuffledWords.forEach((word, poolIdx) => {
            const isUsed = currentSession.wordBankSelected.some(s => s.poolIdx === poolIdx);
            const tile = document.createElement('button');
            tile.className = `btn-tile px-4 py-2.5 text-sm font-extrabold ${isUsed ? 'opacity-25 pointer-events-none bg-slate-100' : ''}`;
            tile.textContent = word;
            tile.onclick = () => {
              if (currentSession.checked || isUsed) return;
              playTone('tap');
              currentSession.wordBankSelected.push({ word, poolIdx });
              refreshWordBank();
            };
            pool.appendChild(tile);
          });

          actionBtn.disabled = currentSession.wordBankSelected.length === 0;
        }

        body.appendChild(tray);
        body.appendChild(pool);
        refreshWordBank();
      } else if (q.type === 'match') {
        document.getElementById('q-type-label').textContent = 'Tap matching pairs';
        document.getElementById('q-prompt').textContent = q.prompt;

        const leftItems = [...q.pairs.map(p => p.left)].sort(() => Math.random() - 0.5);
        const rightItems = [...q.pairs.map(p => p.right)].sort(() => Math.random() - 0.5);

        currentSession.matchState = {
          selectedLeft: null,
          selectedRight: null,
          matchedLefts: [],
          matchedRights: []
        };

        const grid = document.createElement('div');
        grid.className = 'grid grid-cols-2 gap-3';

        const leftCol = document.createElement('div');
        leftCol.className = 'flex flex-col gap-2.5';

        const rightCol = document.createElement('div');
        rightCol.className = 'flex flex-col gap-2.5';

        function evaluateMatchAttempt() {
          const ms = currentSession.matchState;
          if (!ms.selectedLeft || !ms.selectedRight) return;

          const pairFound = q.pairs.some(p => p.left === ms.selectedLeft && p.right === ms.selectedRight);

          if (pairFound) {
            playTone('correct');
            ms.matchedLefts.push(ms.selectedLeft);
            ms.matchedRights.push(ms.selectedRight);
            ms.selectedLeft = null;
            ms.selectedRight = null;
            renderMatchColumns();

            if (ms.matchedLefts.length === q.pairs.length) {
              // Auto-complete match question
              currentSession.checked = true;
              currentSession.correctCount++;
              currentSession.earnedXP += 15;
              showFeedbackBanner(true, 'All pairs matched! +15 XP');
            }
          } else {
            playTone('wrong');
            const wrongL = ms.selectedLeft;
            const wrongR = ms.selectedRight;
            ms.selectedLeft = null;
            ms.selectedRight = null;
            renderMatchColumns(wrongL, wrongR);
          }
        }

        function renderMatchColumns(wrongL = null, wrongR = null) {
          const ms = currentSession.matchState;
          leftCol.innerHTML = '';
          rightCol.innerHTML = '';

          leftItems.forEach(item => {
            const btn = document.createElement('button');
            const isMatched = ms.matchedLefts.includes(item);
            const isSel = ms.selectedLeft === item;
            const isWrong = wrongL === item;
            btn.className = `btn-tile py-3.5 px-3 text-sm font-extrabold text-center ${isMatched ? 'matched' : ''} ${isSel ? 'selected' : ''} ${isWrong ? 'wrong-shake' : ''}`;
            btn.textContent = item;
            btn.onclick = () => {
              if (isMatched || currentSession.checked) return;
              playTone('tap');
              ms.selectedLeft = item;
              renderMatchColumns();
              evaluateMatchAttempt();
            };
            leftCol.appendChild(btn);
          });

          rightItems.forEach(item => {
            const btn = document.createElement('button');
            const isMatched = ms.matchedRights.includes(item);
            const isSel = ms.selectedRight === item;
            const isWrong = wrongR === item;
            btn.className = `btn-tile py-3.5 px-3 text-sm font-extrabold text-center ${isMatched ? 'matched' : ''} ${isSel ? 'selected' : ''} ${isWrong ? 'wrong-shake' : ''}`;
            btn.textContent = item;
            btn.onclick = () => {
              if (isMatched || currentSession.checked) return;
              playTone('tap');
              ms.selectedRight = item;
              renderMatchColumns();
              evaluateMatchAttempt();
            };
            rightCol.appendChild(btn);
          });
        }

        grid.appendChild(leftCol);
        grid.appendChild(rightCol);
        body.appendChild(grid);
        renderMatchColumns();
      }
    }

    function handleLessonAction() {
      if (!currentSession) return;

      // If already checked, advance to next question or complete screen
      if (currentSession.checked) {
        playTone('tap');
        currentSession.index++;
        if (currentSession.index >= currentSession.questions.length) {
          completeLesson();
        } else {
          renderCurrentQuestion();
        }
        return;
      }

      // Evaluate answer
      const q = currentSession.questions[currentSession.index];
      let isCorrect = false;
      let correctText = '';

      if (q.type === 'mc') {
        isCorrect = currentSession.userSelection === q.answer;
        correctText = q.answer;
      } else if (q.type === 'wordbank') {
        const built = currentSession.wordBankSelected.map(s => s.word).join(' ');
        const expected = q.answer.join(' ');
        isCorrect = built === expected;
        correctText = expected;
      }

      currentSession.checked = true;

      if (isCorrect) {
        playTone('correct');
        currentSession.correctCount++;
        currentSession.earnedXP += 10;
        showFeedbackBanner(true, '+10 XP');
      } else {
        playTone('wrong');
        state.hearts = Math.max(0, state.hearts - 1);
        saveState();
        document.getElementById('lesson-hearts').textContent = state.hearts;
        showFeedbackBanner(false, `Correct answer: ${correctText}`);
      }
    }

    function showFeedbackBanner(isCorrect, detailText) {
      const footer = document.getElementById('lesson-footer');
      const banner = document.getElementById('feedback-banner');
      const icon = document.getElementById('feedback-icon');
      const title = document.getElementById('feedback-title');
      const detail = document.getElementById('feedback-detail');
      const actionBtn = document.getElementById('lesson-action-btn');

      banner.classList.remove('hidden');
      banner.classList.add('pop-in');

      if (isCorrect) {
        footer.className = 'px-5 py-4 border-t-2 border-emerald-200 bg-[#d7ffb8] transition-colors duration-200';
        icon.className = 'w-8 h-8 rounded-full bg-[#58cc02] flex items-center justify-center font-black text-white text-base shrink-0';
        icon.textContent = '✓';
        title.className = 'font-black text-lg leading-tight text-[#58a700]';
        title.textContent = 'Awesome!';
        detail.className = 'text-xs font-extrabold text-[#58a700] mt-0.5';
        detail.textContent = detailText;
        actionBtn.className = 'btn-3d btn-green w-full py-3.5 text-[15px]';
      } else {
        footer.className = 'px-5 py-4 border-t-2 border-rose-200 bg-[#ffdfe0] transition-colors duration-200';
        icon.className = 'w-8 h-8 rounded-full bg-[#ff4b4b] flex items-center justify-center font-black text-white text-base shrink-0';
        icon.textContent = '✕';
        title.className = 'font-black text-lg leading-tight text-[#ea2b2b]';
        title.textContent = 'Not quite!';
        detail.className = 'text-xs font-extrabold text-[#ea2b2b] mt-0.5';
        detail.textContent = detailText;
        actionBtn.className = 'btn-3d btn-red w-full py-3.5 text-[15px]';
      }

      actionBtn.textContent = state.hearts === 0 && !isCorrect ? 'OUT OF HEARTS' : 'CONTINUE';
      actionBtn.disabled = false;

      if (state.hearts === 0 && !isCorrect) {
        actionBtn.onclick = () => {
          exitLesson();
          showToast('Out of hearts! Refill in Practice ❤️');
        };
      } else {
        actionBtn.onclick = handleLessonAction;
      }
    }

    function completeLesson() {
      document.getElementById('lesson-progress-bar').style.width = '100%';
      playTone('fanfare');
      launchConfetti();

      const totalQ = currentSession.questions.length;
      const accuracy = Math.round((currentSession.correctCount / totalQ) * 100);
      const bonusXP = currentSession.earnedXP + 15;

      state.xp += bonusXP;
      if (!currentSession.isQuickPractice && !state.completedLessons.includes(currentSession.lessonId)) {
        state.completedLessons.push(currentSession.lessonId);
      }
      saveState();

      document.getElementById('complete-xp').textContent = `+${bonusXP}`;
      document.getElementById('complete-acc').textContent = `${accuracy}%`;
      document.getElementById('complete-streak').textContent = `🔥 ${state.streak}`;

      showScreen('screen-complete');
    }

    function finishLessonFlow() {
      playTone('tap');
      currentSession = null;
      enterMainApp();
    }

    /* =========================================================================
       6. MODALS (Course Switcher, Demo Account Login, Reset Confirmation)
       ========================================================================= */
    function openModal(htmlContent) {
      const backdrop = document.getElementById('modal-backdrop');
      const box = document.getElementById('modal-content');
      box.innerHTML = htmlContent;
      backdrop.classList.remove('hidden');
    }

    function closeModal() {
      document.getElementById('modal-backdrop').classList.add('hidden');
    }

    function openCourseModal() {
      playTone('tap');
      const items = Object.values(COURSES).map(c => {
        const active = c.id === state.activeCourse;
        return `
          <button onclick="selectCourse('${c.id}')" class="w-full p-3.5 rounded-2xl border-2 ${active ? 'border-sky-400 bg-sky-50' : 'border-slate-200 hover:bg-slate-50'} flex items-center justify-between transition">
            <div class="flex items-center gap-3">
              <span class="text-2xl">${c.flag}</span>
              <div class="text-left">
                <p class="font-extrabold text-slate-800 text-sm">${c.name}</p>
                <p class="text-xs font-bold text-slate-400">${c.lessons.length} Interactive Skills</p>
              </div>
            </div>
            ${active ? '<span class="text-xs font-black text-sky-600 uppercase">Active</span>' : ''}
          </button>
        `;
      }).join('');

      openModal(`
        <div class="flex items-center justify-between mb-4">
          <h3 class="text-lg font-black text-slate-800">Choose a Course</h3>
          <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600 font-black text-lg px-2">✕</button>
        </div>
        <div class="space-y-2.5 mb-3">${items}</div>
      `);
    }

    function selectCourse(courseId) {
      playTone('correct');
      state.activeCourse = courseId;
      saveState();
      closeModal();
      renderHomeUI();
      showToast(`Switched to ${COURSES[courseId].name}`);
    }

    function openAccountModal() {
      playTone('tap');
      openModal(`
        <div class="flex items-center justify-between mb-3">
          <h3 class="text-lg font-black text-slate-800">Welcome Back!</h3>
          <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600 font-black text-lg px-2">✕</button>
        </div>
        <p class="text-xs font-bold text-slate-500 mb-4">Continue with your saved browser profile or load a Demo Pro Learner account with streak & XP unlocked.</p>
        <div class="space-y-2.5">
          <button onclick="loadSavedOrDemo(false)" class="btn-3d btn-green w-full py-3.5 text-xs">
            CONTINUE MY SAVED PROGRESS
          </button>
          <button onclick="loadSavedOrDemo(true)" class="btn-3d btn-blue w-full py-3.5 text-xs">
            LOAD DEMO ACCOUNT (7-DAY STREAK)
          </button>
        </div>
      `);
    }

    function loadSavedOrDemo(useDemo) {
      playTone('correct');
      if (useDemo) {
        state = {
          ...state,
          hasOnboarded: true,
          userName: 'Maya (Demo Pro)',
          xp: 340,
          streak: 7,
          hearts: 5,
          completedLessons: ['it-1', 'bio-1']
        };
      } else {
        state.hasOnboarded = true;
      }
      saveState();
      closeModal();
      enterMainApp();
    }

    function confirmResetModal() {
      playTone('tap');
      openModal(`
        <h3 class="text-lg font-black text-slate-800 mb-2">Reset All Progress?</h3>
        <p class="text-xs font-bold text-slate-500 mb-5">This will clear your XP, streak, and completed lessons in this browser.</p>
        <div class="flex gap-3">
          <button onclick="closeModal()" class="btn-3d btn-white flex-1 py-3 text-xs">CANCEL</button>
          <button onclick="executeReset()" class="btn-3d btn-red flex-1 py-3 text-xs">RESET</button>
        </div>
      `);
    }

    function executeReset() {
      playTone('wrong');
      state = { ...defaultState };
      saveState();
      closeModal();
      showToast('Progress reset');
      showSplashScreen();
    }

    /* =========================================================================
       7. TOAST, KEYBOARD SHORTCUTS & CONFETTI CELEBRATION
       ========================================================================= */
    let toastTimer = null;
    function showToast(msg) {
      const box = document.getElementById('toast-box');
      box.textContent = msg;
      box.classList.remove('hidden');
      clearTimeout(toastTimer);
      toastTimer = setTimeout(() => box.classList.add('hidden'), 2400);
    }

    // Desktop Keyboard Shortcuts (1-4 for MC, Enter to Check/Continue)
    document.addEventListener('keydown', (e) => {
      const lessonScreen = document.getElementById('screen-lesson');
      if (lessonScreen.classList.contains('hidden') || !currentSession) return;

      if (['1', '2', '3', '4'].includes(e.key)) {
        const idx = parseInt(e.key, 10) - 1;
        const opts = document.querySelectorAll('.mc-option');
        if (opts[idx]) opts[idx].click();
      } else if (e.key === 'Enter') {
        const btn = document.getElementById('lesson-action-btn');
        if (!btn.disabled) btn.click();
      }
    });

    // Lightweight Canvas Confetti
    function launchConfetti() {
      const canvas = document.getElementById('confetti-canvas');
      const shell = document.getElementById('app-shell');
      canvas.width = shell.clientWidth;
      canvas.height = shell.clientHeight;
      const ctx = canvas.getContext('2d');
      const colors = ['#58cc02', '#ffc800', '#1cb0f6', '#ff4b4b', '#ce82ff'];
      const particles = Array.from({ length: 65 }, () => ({
        x: Math.random() * canvas.width,
        y: -20 - Math.random() * 140,
        r: 4 + Math.random() * 5,
        color: colors[Math.floor(Math.random() * colors.length)],
        vy: 2.5 + Math.random() * 3.5,
        vx: -1.5 + Math.random() * 3,
        rot: Math.random() * 360
      }));

      let frames = 0;
      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        particles.forEach(p => {
          p.x += p.vx;
          p.y += p.vy;
          p.rot += 4;
          ctx.save();
          ctx.translate(p.x, p.y);
          ctx.rotate((p.rot * Math.PI) / 180);
          ctx.fillStyle = p.color;
          ctx.fillRect(-p.r, -p.r / 2, p.r * 2, p.r);
          ctx.restore();
        });
        frames++;
        if (frames < 115) requestAnimationFrame(draw);
        else ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
      requestAnimationFrame(draw);
    }

    // Initialize App on Load
    window.addEventListener('DOMContentLoaded', () => {
      updateSoundIcons();
      showScreen('screen-splash');
    });
  </script>
</body>
</html>
```
