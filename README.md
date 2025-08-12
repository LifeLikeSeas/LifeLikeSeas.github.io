<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>סטטיסטי-כיפאק</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css" xintegrity="sha384-n8MVd4RsNIU0tAv4ct0nTaAbDJwPJzDEaqSD1odI+WdtXRGWt2kTvGFasHpSy3SV" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js" xintegrity="sha384-XjKyOOlGwcjNTAIQHIpgOno0Hl1YQqzUOEleOLALmuqehneUG+vnGctmUbKyJjd8" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/contrib/auto-render.min.js" xintegrity="sha384-+VBxd3r6XgURycqtZ117nYw44OOcIax56Z4dCRWbxyPt0Koah1uHoK0o4+/RRE05" crossorigin="anonymous"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@300;400;600;700&display=swap');
        body {
            font-family: 'Assistant', sans-serif;
            scroll-behavior: smooth;
        }
        .katex { font-size: 1.1em; }
        .feedback {
            transition: all 0.3s ease-in-out;
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            padding: 0 1rem;
        }
        .feedback.show {
             max-height: 200px;
             opacity: 1;
             margin-top: 1rem;
             padding: 0.75rem 1rem;
        }
        .feedback.correct {
            border-right: 4px solid #22c55e;
            background-color: rgba(34, 197, 94, 0.1);
        }
        .feedback.incorrect {
            border-right: 4px solid #ef4444;
            background-color: rgba(239, 68, 68, 0.1);
        }
        .draggable { cursor: grab; }
        .drop-target { border: 2px dashed #4b5563; }
        .drop-target.drag-over { background-color: #374151; border-color: #60a5fa; }
        .module-card { transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out; }
        .module-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(96, 165, 250, 0.2), 0 4px 6px -2px rgba(96, 165, 250, 0.1); }
        .navigator-btn { transition: background-color 0.2s; }
        .spss-output {
            background-color: #f0f4f8;
            color: #333;
            font-family: 'Courier New', Courier, monospace;
            padding: 1rem;
            border-radius: 0.5rem;
            border: 1px solid #ccc;
            white-space: pre;
            overflow-x: auto;
            direction: ltr;
        }
    </style>
</head>
<body class="bg-gray-900 text-gray-200">
    <!-- Header -->
    <header class="bg-gray-800 shadow-lg sticky top-0 z-50">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <h1 class="text-2xl md:text-3xl font-bold text-blue-400">
                <i class="fas fa-chart-pie mr-2"></i>סטטיסטי-כיפאק
            </h1>
            <nav>
                <a href="#modules" class="text-gray-300 hover:text-blue-400 transition">מודולים</a>
            </nav>
        </div>
    </header>
    <!-- Main Content -->
    <main class="container mx-auto p-4 md:p-8">
        <section class="text-center mb-12">
            <h2 class="text-4xl md:text-5xl font-extrabold mb-2 bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-teal-300">המסע שלך לשליטה בסטטיסטיקה</h2>
            <p class="text-lg text-gray-400">אפליקציית למידה אינטראקטיבית המבוססת על חומרי הקורס שלך.</p>
        </section>
        <section id="modules">
            <h3 class="text-3xl font-bold mb-6 border-b-2 border-gray-700 pb-2">יחידות הלימוד</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Module Cards -->
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module1')">
                    <div class="flex items-center mb-4"><div class="bg-blue-500/20 text-blue-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-book-open text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 1</p><h4 class="text-xl font-bold">יסודות הסטטיסטיקה</h4></div></div><p class="text-gray-400">הכרת השפה, סמלים בסיסיים וסולמות מדידה.</p>
                </div>
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module2')">
                    <div class="flex items-center mb-4"><div class="bg-teal-500/20 text-teal-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-bell text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 2</p><h4 class="text-xl font-bold">עולם ההתפלגויות</h4></div></div><p class="text-gray-400">התפלגות נורמלית, ציוני תקן ומשפט הגבול המרכזי.</p>
                </div>
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module3')">
                     <div class="flex items-center mb-4"><div class="bg-purple-500/20 text-purple-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-ruler-combined text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 3</p><h4 class="text-xl font-bold">אמידה ורווחי סמך</h4></div></div><p class="text-gray-400">אמידה נקודתית, רווחי סמך לתוחלת ולפרופורציה.</p>
                </div>
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module4')">
                     <div class="flex items-center mb-4"><div class="bg-orange-500/20 text-orange-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-balance-scale text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 4</p><h4 class="text-xl font-bold">בדיקת השערות</h4></div></div><p class="text-gray-400">הלוגיקה, מבחני Z, מבחני t, פרופורציות ושונות.</p>
                </div>
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module5')">
                     <div class="flex items-center mb-4"><div class="bg-rose-500/20 text-rose-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-not-equal text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 5</p><h4 class="text-xl font-bold">מבחנים א-פרמטריים</h4></div></div><p class="text-gray-400">מבחן חי-בריבוע, וילקוקסון ועוד חלופות.</p>
                </div>
                <div class="module-card bg-gray-800 rounded-lg p-6 shadow-md cursor-pointer" onclick="showModule('module6')">
                     <div class="flex items-center mb-4"><div class="bg-indigo-500/20 text-indigo-300 rounded-full h-12 w-12 flex items-center justify-center mr-4"><i class="fas fa-project-diagram text-xl"></i></div><div><p class="text-sm text-gray-400">מודול 6</p><h4 class="text-xl font-bold">בחירת המבחן הנכון</h4></div></div><p class="text-gray-400">כלי אינטראקטיבי שיעזור לך לבחור את המבחן המתאים.</p>
                </div>
            </div>
        </section>
        <!-- Module Content Area -->
        <div id="module-content" class="mt-12 hidden">
            <!-- Module 1 Content -->
            <div id="module1" class="hidden">
                <button onclick="hideModules()" class="mb-4 bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 1: יסודות הסטטיסטיקה</h3>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 1.1: שפת הסטטיסטיקאים</h4>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: גרור והתאם</h5>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <h6 class="font-semibold mb-2 text-center">סמל</h6>
                                <div id="symbols-container" class="space-y-2">
                                    <div id="drag-mu" class="draggable bg-blue-500/30 p-3 rounded-lg text-center" draggable="true">`\mu`</div>
                                    <div id="drag-sigma" class="draggable bg-blue-500/30 p-3 rounded-lg text-center" draggable="true">`\sigma`</div>
                                    <div id="drag-xbar" class="draggable bg-blue-500/30 p-3 rounded-lg text-center" draggable="true">`\bar{x}`</div>
                                    <div id="drag-s" class="draggable bg-blue-500/30 p-3 rounded-lg text-center" draggable="true">`\hat{S}`</div>
                                </div>
                            </div>
                            <div>
                                <h6 class="font-semibold mb-2 text-center">הגדרה</h6>
                                <div id="definitions-container" class="space-y-2">
                                    <div class="drop-target p-3 rounded-lg flex items-center" data-match="drag-mu"><span class="flex-grow">תוחלת (ממוצע) אוכלוסייה</span><span class="feedback-icon"></span></div>
                                    <div class="drop-target p-3 rounded-lg flex items-center" data-match="drag-sigma"><span class="flex-grow">סטיית תקן אוכלוסייה</span><span class="feedback-icon"></span></div>
                                    <div class="drop-target p-3 rounded-lg flex items-center" data-match="drag-xbar"><span class="flex-grow">ממוצע מדגם</span><span class="feedback-icon"></span></div>
                                    <div class="drop-target p-3 rounded-lg flex items-center" data-match="drag-s"><span class="flex-grow">אומדן לסטיית תקן (מהמדגם)</span><span class="feedback-icon"></span></div>
                                </div>
                            </div>
                        </div>
                        <div id="feedback-symbols" class="mt-4 p-3 rounded-lg text-center feedback"></div>
                    </div>
                </div>
                <div class="bg-gray-800 rounded-lg p-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 1.2: סולמות מדידה</h4>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: קטלג את המשתנה</h5>
                        <p class="mb-4">"חוקר מבקש לבדוק את רמת שביעות הרצון של לקוחות בסולם של 1 (לא מרוצה כלל) עד 5 (מרוצה מאוד)".</p>
                        <div id="scales-buttons" class="flex flex-wrap gap-2">
                            <button class="bg-teal-600 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded transition" data-scale="nominal">שמי (Nominal)</button>
                            <button class="bg-teal-600 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded transition" data-scale="ordinal">סדר (Ordinal)</button>
                            <button class="bg-teal-600 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded transition" data-scale="interval">רווח (Interval)</button>
                            <button class="bg-teal-600 hover:bg-teal-700 text-white font-bold py-2 px-4 rounded transition" data-scale="ratio">מנה (Ratio)</button>
                        </div>
                        <div id="feedback-scales" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
            <!-- Module 2 Content -->
            <div id="module2" class="hidden">
                <button onclick="hideModules()" class="mb-4 bg-teal-500 hover:bg-teal-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 2: עולם ההתפלגויות</h3>
                 <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 2.1: פעמון גאוס - ההתפלגות הנורמלית</h4>
                    <p class="mb-4">התפלגות נורמלית, `X \sim N(\mu, \sigma^2)`, היא אבן יסוד בסטטיסטיקה. בוא נראה איך הפרמטרים משפיעים על צורתה.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: מעצב ההתפלגויות</h5>
                        <div class="w-full h-64 mb-4"><canvas id="normalDistChart"></canvas></div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="mu-slider" class="block mb-2">תוחלת (`\mu`): <span id="mu-value">50</span></label>
                                <input id="mu-slider" type="range" min="0" max="100" value="50" class="w-full">
                            </div>
                            <div>
                                <label for="sigma-slider" class="block mb-2">סטיית תקן (`\sigma`): <span id="sigma-value">10</span></label>
                                <input id="sigma-slider" type="range" min="1" max="30" value="10" class="w-full">
                            </div>
                        </div>
                         <p class="mt-4 text-gray-400 text-sm">שחקו עם הסליידרים וראו איך הזזת התוחלת מזיזה את הפעמון, ואיך שינוי סטיית התקן הופך אותו לרחב ושטוח או לצר וגבוה.</p>
                    </div>
                </div>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 2.2: ציוני תקן (Z-scores)</h4>
                     <p class="mb-4">ציון Z מודד בכמה סטיות תקן ערך מסוים רחוק מהממוצע. הנוסחה להתפלגות הדגימה היא: `Z = \frac{\bar{x} - \mu}{\sigma / \sqrt{n}}`.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: מצא את השטח!</h5>
                        <p class="mb-4">תרחיש: ציוני IQ מתפלגים נורמלית עם `\mu=100` ו-`\sigma=15`. דגמנו `n=25` אנשים ומצאנו `\bar{x}=106`. מה ההסתברות לקבל ממוצע מדגם כזה או גבוה יותר?</p>
                        <div class="space-y-4">
                            <div>
                                <label>שלב א': חישוב טעות התקן (`\sigma_{\bar{x}}`). הזן את הערכים:</label>
                                <!-- FIX START: Replaced invalid HTML structure for KaTeX rendering -->
                                <div class="flex items-center gap-2 mt-2">
                                    <span>`\sigma_{\bar{x}} =`</span>
                                    <div class="inline-flex flex-col items-center justify-center mx-2 leading-tight">
                                        <input id="z-se-sigma" type="number" class="w-16 bg-gray-700 rounded p-1 text-center" placeholder="σ">
                                        <hr class="w-full border-gray-400 my-1">
                                        <div class="flex items-center">
                                            <span>√</span>
                                            <input id="z-se-n" type="number" class="w-16 bg-gray-700 rounded p-1 text-center" placeholder="n">
                                        </div>
                                    </div>
                                    <button id="z-se-calc" class="bg-teal-600 hover:bg-teal-700 px-3 py-1 rounded">חשב</button>
                                    <span id="z-se-result" class="font-bold"></span>
                                </div>
                                <!-- FIX END -->
                            </div>
                            <div id="z-score-calc-step" class="hidden">
                                <label>שלב ב': חישוב ציון Z. הזן את הערכים:</label>
                                <!-- FIX START: Replaced invalid HTML structure for KaTeX rendering -->
                                <div class="flex items-center gap-2 mt-2">
                                    <span>`Z =`</span>
                                    <div class="inline-flex flex-col items-center justify-center mx-2 leading-tight">
                                        <div class="flex items-center">
                                            <input id="z-xbar" type="number" class="w-16 bg-gray-700 rounded p-1 text-center" placeholder="x̄">
                                            <span class="mx-2">-</span>
                                            <input id="z-mu" type="number" class="w-16 bg-gray-700 rounded p-1 text-center" placeholder="μ">
                                        </div>
                                        <hr class="w-full border-gray-400">
                                        <span id="z-se-value-display" class="px-2 py-1"></span>
                                    </div>
                                    <button id="z-calc" class="bg-teal-600 hover:bg-teal-700 px-3 py-1 rounded">חשב</button>
                                    <span id="z-result" class="font-bold"></span>
                                </div>
                                <!-- FIX END -->
                            </div>
                        </div>
                        <div id="feedback-z" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
            <!-- Module 3 Content -->
            <div id="module3" class="hidden">
                 <button onclick="hideModules()" class="mb-4 bg-purple-500 hover:bg-purple-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 3: אמידה ורווחי סמך</h3>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 3.1: בניית רווח סמך</h4>
                    <p class="mb-4">רווח סמך הוא טווח של ערכים שבו, ברמת ביטחון מסוימת, אנו מאמינים שנמצאת תוחלת האוכלוסייה. הנוסחה: `\bar{x} \pm Z_{\alpha/2} \frac{\sigma}{\sqrt{n}}` (או עם t כשהשונות לא ידועה).</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: בנאי רווחי הסמך</h5>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block mb-2">ממוצע מדגם (`\bar{x}`)</label>
                                <input id="ci-xbar" type="number" value="120" class="w-full bg-gray-700 rounded p-2">
                            </div>
                             <div>
                                <label class="block mb-2">סטיית תקן (`\sigma` או `\hat{S}`)</label>
                                <input id="ci-s" type="number" value="15" class="w-full bg-gray-700 rounded p-2">
                            </div>
                             <div>
                                <label class="block mb-2">גודל מדגם (`n`)</label>
                                <input id="ci-n" type="number" value="225" class="w-full bg-gray-700 rounded p-2">
                            </div>
                             <div>
                                <label class="block mb-2">רמת סמך</label>
                                <select id="ci-level" class="w-full bg-gray-700 rounded p-2">
                                    <option value="0.90">90%</option>
                                    <option value="0.95" selected>95%</option>
                                    <option value="0.99">99%</option>
                                </select>
                            </div>
                        </div>
                        <button id="ci-calc-btn" class="mt-4 w-full bg-purple-600 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded transition">בנה רווח סמך</button>
                        <div id="feedback-ci" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
                 <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 3.2: פירוש פלט SPSS</h4>
                    <p class="mb-4">ב-SPSS, רווח סמך לתוחלת מופיע בטבלת One-Sample Statistics או T-Test.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: זיהוי בפלט</h5>
                        <div class="spss-output">
                            One-Sample Test<br>
                            ================================================================<br>
                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| 95% Confidence Interval<br>
                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| of the Difference<br>
                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|-----------------------<br>
                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;df&nbsp;&nbsp;&nbsp;Sig.&nbsp;&nbsp;&nbsp;Mean Diff&nbsp;&nbsp;| Lower&nbsp;&nbsp;&nbsp;&nbsp;Upper<br>
                            ================================================================<br>
                            IQ Score&nbsp;&nbsp;&nbsp;2.500&nbsp;&nbsp;24&nbsp;&nbsp;&nbsp;&nbsp;.020&nbsp;&nbsp;&nbsp;&nbsp;5.00000&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|<span id="spss-lower" class="cursor-pointer hover:bg-yellow-300">.8403</span>&nbsp;&nbsp;&nbsp;&nbsp;<span id="spss-upper" class="cursor-pointer hover:bg-yellow-300">9.1597</span><br>
                        </div>
                        <p class="mt-4">בהנחה שהפלט מציג הפרש מהתוחלת המשוערת `\mu_0=100`, מהו רווח הסמך לתוחלת האוכלוסייה `\mu`?</p>
                        <div id="feedback-spss" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
            <!-- Module 4 Content -->
            <div id="module4" class="hidden">
                 <button onclick="hideModules()" class="mb-4 bg-orange-500 hover:bg-orange-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 4: בדיקת השערות</h3>
                 <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 4.1: ניסוח השערות</h4>
                     <p class="mb-4">השלב הראשון והחשוב ביותר הוא ניסוח נכון של השערת האפס (`H_0`) וההשערה האלטרנטיבית (`H_1`). `H_0` תמיד מכילה את השוויון.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: מנסח ההשערות</h5>
                        <p class="mb-4">תרחיש: "חוקר טוען שזמן הצפייה היומי הממוצע בטלוויזיה (`\mu`) השתנה מהממוצע שהיה ידוע בעבר, 3.5 שעות."</p>
                        <div class="space-y-3">
                            <div class="flex items-center gap-2">`H_0: \mu` <select id="h0-op" class="bg-gray-700 rounded"><option>=</option><option>≠</option><option>&lt;</option><option>&gt;</option></select> `3.5`</div>
                            <div class="flex items-center gap-2">`H_1: \mu` <select id="h1-op" class="bg-gray-700 rounded"><option>=</option><option selected>≠</option><option>&lt;</option><option>&gt;</option></select> `3.5`</div>
                        </div>
                        <button id="hypo-check-btn" class="mt-4 bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded transition">בדוק השערות</button>
                        <div id="feedback-hypo" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
                 <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 4.2: סימולטור מבחן t</h4>
                     <p class="mb-4">בוא נעבור על שלבי מבחן t למדגם יחיד.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                         <p class="mb-4">נתונים: מדגם של `n=16` סטודנטים, ממוצע ציונים `\bar{x}=84`, אומדן סטיית תקן `\hat{S}=8`. אנו בודקים אם ממוצע הציונים שונה מ-`\mu_0=80` ברמת מובהקות `\alpha=0.05`.</p>
                         <p>1. השערות: `H_0: \mu = 80`, `H_1: \mu \ne 80`.</p>
                         <p>2. סטטיסטי המבחן המחושב הוא: `t = \frac{84 - 80}{8 / \sqrt{16}} = \frac{4}{2} = 2`.</p>
                         <p>3. דרגות החופש: `df = n-1 = 15`.</p>
                         <h5 class="font-bold my-4">פעילות: קבלת החלטה</h5>
                         <p>הערך הקריטי מהטבלה עבור מבחן דו-צדדי עם `\alpha=0.05` ו-`df=15` הוא `t_{crit} = 2.131`.</p>
                         <p class="mt-2">האם ערך ה-t שחישבנו (2) נופל באזור הדחייה (כלומר, `|t| > t_{crit}`)?</p>
                         <div id="ttest-buttons" class="flex flex-wrap gap-2 mt-4">
                            <button class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded transition" data-answer="no">לא, הוא לא נופל באזור הדחייה</button>
                            <button class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded transition" data-answer="yes">כן, הוא נופל באזור הדחייה</button>
                         </div>
                         <div id="feedback-ttest" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
            <!-- Module 5 Content -->
            <div id="module5" class="hidden">
                 <button onclick="hideModules()" class="mb-4 bg-rose-500 hover:bg-rose-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 5: מבחנים א-פרמטריים</h3>
                 <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 5.1: מתי ולמה?</h4>
                     <p class="mb-4">כשהנחות המבחנים הפרמטריים (כמו נורמליות) לא מתקיימות, או כשהנתונים הם מסולם סדר, אנו פונים למבחנים א-פרמטריים.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: פרמטרי או א-פרמטרי?</h5>
                        <p class="mb-4">תרחיש: "חוקר עם מדגם של 15 אנשים רוצה להשוות דירוגי טעם בין שני משקאות (קולה ופפסי) לכל נבדק. הנתונים הם דירוג בסולם 1-10."</p>
                        <div id="nonpara-buttons" class="flex flex-wrap gap-2">
                            <button class="bg-rose-600 hover:bg-rose-700 text-white font-bold py-2 px-4 rounded transition" data-answer="para">מבחן פרמטרי (מבחן t למדגמים מזווגים)</button>
                            <button class="bg-rose-600 hover:bg-rose-700 text-white font-bold py-2 px-4 rounded transition" data-answer="nonpara">מבחן א-פרמטרי (מבחן וילקוקסון למדגמים מזווגים)</button>
                        </div>
                        <div id="feedback-nonpara" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 5.2: מבחן חי-בריבוע (`\chi^2`) לאי-תלות</h4>
                     <p class="mb-4">מבחן זה בודק אם קיים קשר (תלות) בין שני משתנים שמיים. הוא משווה את התצפיות בפועל (Observed) למה שהיינו מצפים לו אילו לא היה קשר (Expected).</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <h5 class="font-bold mb-4">פעילות: מחשבון `\chi^2`</h5>
                        <p>האם יש קשר בין מגדר להעדפת חיית מחמד? נתוני המדגם:</p>
                        <table class="w-full text-center my-4 text-gray-300">
                            <thead><tr class="border-b border-gray-600"><th></th><th>כלב</th><th>חתול</th><th>סך הכל</th></tr></thead>
                            <tbody>
                                <tr class="border-b border-gray-700"><td>גברים</td><td>20</td><td>10</td><td class="font-bold">30</td></tr>
                                <tr class="border-b border-gray-700"><td>נשים</td><td>15</td><td>25</td><td class="font-bold">40</td></tr>
                                <tr><td class="font-bold">סך הכל</td><td class="font-bold">35</td><td class="font-bold">35</td><td class="font-bold">70</td></tr>
                            </tbody>
                        </table>
                        <p>חשב את השכיחות הצפויה (Expected) עבור התא "גברים" ו"כלב". הנוסחה: `E = \frac{(Total_{row}) \times (Total_{column})}{Total_{grand}}`</p>
                        <div class="flex items-center gap-2 mt-2">
                            <input id="chi-expected" type="number" class="w-24 bg-gray-700 rounded p-1 text-center" placeholder="E">
                            <button id="chi-check-btn" class="bg-rose-600 hover:bg-rose-700 px-3 py-1 rounded">בדוק</button>
                        </div>
                        <div id="feedback-chi" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
            <!-- Module 6 Content -->
            <div id="module6" class="hidden">
                <button onclick="hideModules()" class="mb-4 bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-2 px-4 rounded transition"><i class="fas fa-arrow-right ml-2"></i>חזרה לכל המודולים</button>
                <h3 class="text-3xl font-bold mb-6">מודול 6: בחירת המבחן הנכון</h3>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 6.1: הנווט הסטטיסטי</h4>
                    <p class="mb-4">ענו על השאלות והנווט יכוון אתכם למבחן המתאים ביותר לתרחיש המחקר שלכם.</p>
                    <div id="navigator" class="bg-gray-900 p-4 rounded-lg">
                        <div id="navigator-question" class="mb-4 text-lg"></div>
                        <div id="navigator-options" class="flex flex-col space-y-2"></div>
                        <div id="navigator-result" class="mt-4 p-4 rounded-lg bg-indigo-500/30 text-center font-bold text-xl hidden"></div>
                        <button id="navigator-reset" class="mt-4 bg-gray-600 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded transition hidden">התחל מחדש</button>
                    </div>
                </div>
                <div class="bg-gray-800 rounded-lg p-6 mb-6">
                    <h4 class="text-2xl font-bold mb-4">שיעור 6.2: אתגר ניתוח מקרה</h4>
                    <p class="mb-4">קראו את תרחיש המחקר הבא וענו על השאלות כדי לזהות את המבחן המתאים.</p>
                    <div class="bg-gray-900 p-4 rounded-lg">
                        <p class="mb-4">"פסיכולוגית רוצה לבדוק אם תוכנית התערבות חדשה מקטינה את רמת החרדה הממוצעת. היא דוגמת 25 סטודנטים, מודדת את רמת החרדה שלהם (בסולם 1-100) לפני ואחרי התוכנית. הנתונים אינם מתפלגים נורמלית."</p>
                        <div id="case-study-quiz">
                            <p class="font-bold">1. מהו סוג המדגם?</p>
                            <div class="flex gap-2 my-2" id="case-q1">
                                <button class="bg-indigo-600 hover:bg-indigo-700 px-3 py-1 rounded" data-correct="false">בלתי תלויים</button>
                                <button class="bg-indigo-600 hover:bg-indigo-700 px-3 py-1 rounded" data-correct="true">מזווגים</button>
                            </div>
                            <p class="font-bold mt-4">2. לאור כל הנתונים, מהו המבחן המתאים ביותר?</p>
                             <div class="flex gap-2 my-2" id="case-q2">
                                <button class="bg-indigo-600 hover:bg-indigo-700 px-3 py-1 rounded" data-correct="false">מבחן t למדגמים מזווגים</button>
                                <button class="bg-indigo-600 hover:bg-indigo-700 px-3 py-1 rounded" data-correct="true">מבחן וילקוקסון</button>
                            </div>
                        </div>
                         <div id="feedback-case" class="mt-4 p-3 rounded-lg feedback"></div>
                    </div>
                </div>
            </div>
        </div>
    </main>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // A function to render all math expressions on the page using KaTeX
            function renderAllMath() {
                if (window.renderMathInElement) {
                    renderMathInElement(document.body, {
                        delimiters: [
                            {left: '$$', right: '$$', display: true}, {left: '$', right: '$', display: false},
                            {left: '`', right: '`', display: false}, {left: '\\(', right: '\\)', display: false},
                            {left: '\\[', right: '\\]', display: true}
                        ]
                    });
                }
            } 
            // Initial render call
            renderAllMath();
            // --- Initialize all interactive components ---
            setupDragAndDrop();
            setupScalesQuiz();
            setupNormalDistributionChart();
            setupZScoreCalculator();
            setupCIBuilder();
            setupSPSSQuiz();
            setupHypothesisQuiz();
            setupTTestQuiz();
            setupNonParaQuiz();
            setupChiSquareQuiz();
            setupStatisticalNavigator();
            setupCaseStudyQuiz();
        });
        // --- Navigation Logic ---
        const moduleIds = ['module1', 'module2', 'module3', 'module4', 'module5', 'module6'];
        function showModule(moduleId) {
            document.getElementById('modules').classList.add('hidden');
            const moduleContent = document.getElementById('module-content');
            moduleContent.classList.remove('hidden');
            moduleIds.forEach(id => document.getElementById(id).classList.add('hidden'));
            const moduleToShow = document.getElementById(moduleId);
            if (moduleToShow) {
                moduleToShow.classList.remove('hidden');
                moduleContent.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }
        }
        function hideModules() {
            document.getElementById('modules').classList.remove('hidden');
            document.getElementById('module-content').classList.add('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
        // --- Generic Feedback Function ---
        function showFeedback(elementId, message, isCorrect) {
            const feedbackDiv = document.getElementById(elementId);
            feedbackDiv.innerHTML = message;
            feedbackDiv.className = `p-3 rounded-lg feedback show ${isCorrect ? 'correct' : 'incorrect'}`;
            if (window.renderMathInElement) {
                renderMathInElement(feedbackDiv);
            }
        }
        // --- Lesson Implementations ---
        function setupDragAndDrop() {
            const draggables = document.querySelectorAll('.draggable');
            const dropTargets = document.querySelectorAll('.drop-target');
            let draggedItem = null;
            draggables.forEach(draggable => {
                draggable.addEventListener('dragstart', e => {
                    draggedItem = e.target;
                    setTimeout(() => e.target.style.opacity = '0.5', 0);
                });
                draggable.addEventListener('dragend', e => {
                    draggedItem = null;
                    setTimeout(() => e.target.style.opacity = '1', 0);
                });
            });
            dropTargets.forEach(target => {
                target.addEventListener('dragover', e => { e.preventDefault(); target.classList.add('drag-over'); });
                target.addEventListener('dragleave', () => target.classList.remove('drag-over'));
                target.addEventListener('drop', e => {
                    e.preventDefault();
                    target.classList.remove('drag-over');
                    const feedbackIcon = target.querySelector('.feedback-icon');
                    if (draggedItem && target.dataset.match === draggedItem.id) {
                        target.prepend(draggedItem);
                        draggedItem.setAttribute('draggable', 'false');
                        draggedItem.style.cursor = 'default';
                        feedbackIcon.innerHTML = '<i class="fas fa-check-circle text-green-500 ml-2"></i>';
                        checkAllSymbolsMatched();
                    } else {
                        feedbackIcon.innerHTML = '<i class="fas fa-times-circle text-red-500 ml-2"></i>';
                        setTimeout(() => feedbackIcon.innerHTML = '', 2000);
                    }
                });
            });
            function checkAllSymbolsMatched() {
                const remaining = document.querySelectorAll('#symbols-container .draggable').length;
                if (remaining === 0) {
                    showFeedback('feedback-symbols', 'כל הכבוד! פרמטר (`\\mu`) שייך לאוכלוסייה, וסטטיסטי (`\\bar{x}`) שייך למדגם.', true);
                }
            }
        }
        function setupScalesQuiz() {
            document.getElementById('scales-buttons').addEventListener('click', e => {
                if (e.target.tagName !== 'BUTTON') return;
                const isCorrect = e.target.dataset.scale === 'ordinal';
                const message = isCorrect 
                    ? '<i class="fas fa-check-circle mr-2"></i>נכון מאוד! יש כאן דירוג (סדר), אך הרווחים בין הדרגות אינם בהכרח שווים.'
                    : '<i class="fas fa-times-circle mr-2"></i>לא נכון. זהו סולם סדר כי יש היררכיה אך המרחקים לא שווים.';
                showFeedback('feedback-scales', message, isCorrect);
            });
        }
        function setupNormalDistributionChart() {
            const ctx = document.getElementById('normalDistChart')?.getContext('2d');
            if (!ctx) return;
            let chart;
            function pdf(x, mu, sigma) {
                return Math.exp(-0.5 * Math.pow((x - mu) / sigma, 2)) / (sigma * Math.sqrt(2 * Math.PI));
            }
            function updateChart(mu, sigma) {
                const labels = [];
                const data = [];
                const start = mu - 4 * sigma;
                const end = mu + 4 * sigma;
                for (let i = 0; i <= 100; i++) {
                    const x = start + (end - start) * i / 100;
                    labels.push(x.toFixed(1));
                    data.push(pdf(x, mu, sigma));
                }
                if (chart) {
                    chart.data.labels = labels;
                    chart.data.datasets[0].data = data;
                    chart.update('none');
                } else {
                    chart = new Chart(ctx, {
                        type: 'line',
                        data: {
                            labels: labels,
                            datasets: [{
                                data: data, borderColor: 'rgba(96, 165, 250, 1)',
                                backgroundColor: 'rgba(96, 165, 250, 0.2)',
                                borderWidth: 2, fill: true, pointRadius: 0, tension: 0.4
                            }]
                        },
                        options: {
                            responsive: true, maintainAspectRatio: false,
                            scales: { x: { ticks: { color: '#9ca3af' } }, y: { beginAtZero: true, ticks: { color: '#9ca3af' } } },
                            plugins: { legend: { display: false } }
                        }
                    });
                }
            }
            const muSlider = document.getElementById('mu-slider');
            const sigmaSlider = document.getElementById('sigma-slider');
            const update = () => {
                document.getElementById('mu-value').textContent = muSlider.value;
                document.getElementById('sigma-value').textContent = sigmaSlider.value;
                updateChart(parseFloat(muSlider.value), parseFloat(sigmaSlider.value));
            };
            muSlider.addEventListener('input', update);
            sigmaSlider.addEventListener('input', update);
            update();
        }      
        function setupZScoreCalculator() {
            document.getElementById('z-se-calc')?.addEventListener('click', () => {
                const sigma = parseFloat(document.getElementById('z-se-sigma').value);
                const n = parseFloat(document.getElementById('z-se-n').value);
                if (sigma === 15 && n === 25) {
                    const se = sigma / Math.sqrt(n);
                    document.getElementById('z-se-result').textContent = `= ${se}`;
                    document.getElementById('z-se-value-display').textContent = se;
                    document.getElementById('z-score-calc-step').classList.remove('hidden');
                } else {
                    alert('ערכים לא נכונים. נסה עם הנתונים מהתרחיש: σ=15, n=25.');
                }
            });
            document.getElementById('z-calc')?.addEventListener('click', () => {
                const xbar = parseFloat(document.getElementById('z-xbar').value);
                const mu = parseFloat(document.getElementById('z-mu').value);
                if (xbar === 106 && mu === 100) {
                    const se = 3;
                    const z = (xbar - mu) / se;
                    document.getElementById('z-result').textContent = `= ${z}`;
                    // Simplified Z-table lookup
                    const pValue = 1 - 0.9772; // P(Z > 2)
                    showFeedback('feedback-z', `מעולה! ציון ה-Z הוא ${z}. ההסתברות לקבל ממוצע כזה או גבוה יותר היא ` + pValue.toFixed(4) + ` או ` + (pValue*100).toFixed(2) + `%`, true);
                } else {
                     alert('ערכים לא נכונים. נסה עם הנתונים מהתרחיש: x̄=106, μ=100.');
                }
            });
        }
        function setupCIBuilder() {
            document.getElementById('ci-calc-btn')?.addEventListener('click', () => {
                const xbar = parseFloat(document.getElementById('ci-xbar').value);
                const s = parseFloat(document.getElementById('ci-s').value);
                const n = parseFloat(document.getElementById('ci-n').value);
                const level = parseFloat(document.getElementById('ci-level').value);             
                const critical_values = { '0.90': 1.645, '0.95': 1.96, '0.99': 2.576 };
                const z = critical_values[level];
                if (isNaN(xbar) || isNaN(s) || isNaN(n) || n <= 0) {
                    showFeedback('feedback-ci', 'אנא הזן ערכים מספריים תקינים.', false);
                    return;
                }
                const margin_of_error = z * (s / Math.sqrt(n));
                const lower = xbar - margin_of_error;
                const upper = xbar + margin_of_error;
                const message = `הערך הקריטי (` + (n > 30 ? 'Z' : 't') + `) הוא ${z}.<br>שגיאת התקן: ` + (s/Math.sqrt(n)).toFixed(2) + `<br>מרווח הטעות (` + '`&epsilon;`' + `) הוא ${margin_of_error.toFixed(2)}.<br>רווח הסמך ברמת סמך של ${level*100}% הוא: <strong>[${lower.toFixed(2)}, ${upper.toFixed(2)}]</strong>`;
                showFeedback('feedback-ci', message, true);
            });
        }
        function setupSPSSQuiz() {
            document.getElementById('spss-lower')?.addEventListener('click', () => {
                 showFeedback('feedback-spss', 'זהו הגבול התחתון של הפרש התוחלות. כדי למצוא את גבול רווח הסמך לתוחלת עצמה, יש להוסיף את `\\mu_0`: `100 + 0.8403 = 100.84`', false);
            });
             document.getElementById('spss-upper')?.addEventListener('click', () => {
                 showFeedback('feedback-spss', 'נכון מאוד! הגבול העליון של רווח הסמך לתוחלת הוא `\\mu_0` + הגבול העליון של הפרש התוחלות: `100 + 9.1597 = 109.16`. לכן רווח הסמך הוא [100.84, 109.16]', true);
            });
        }
        function setupHypothesisQuiz() {
            document.getElementById('hypo-check-btn')?.addEventListener('click', () => {
                const h0 = document.getElementById('h0-op').value;
                const h1 = document.getElementById('h1-op').value;
                const isCorrect = h0 === '=' && h1 === '≠';
                const message = isCorrect
                    ? '<i class="fas fa-check-circle mr-2"></i>נכון מאוד! `H_0` תמיד כוללת שוויון, והטענה לשינוי כללי (לא כיווני) מובילה למבחן דו-צדדי (`≠`).'
                    : '<i class="fas fa-times-circle mr-2"></i>לא מדויק. זכור שהשערת האפס תמיד בודקת את המצב הקיים (שוויון), והאלטרנטיבה משקפת את טענת החוקר.';
                showFeedback('feedback-hypo', message, isCorrect);
            });
        }
        function setupTTestQuiz() {
            document.getElementById('ttest-buttons')?.addEventListener('click', e => {
                if (e.target.tagName !== 'BUTTON') return;
                const isCorrect = e.target.dataset.answer === 'no';
                const message = isCorrect
                    ? '<i class="fas fa-check-circle mr-2"></i>נכון! מכיוון ש-`|2| < 2.131`, ערך ה-t שחישבנו <strong>אינו</strong> נופל באזור הדחייה. לכן, אין לנו מספיק ראיות כדי לדחות את `H_0`.'
                    : '<i class="fas fa-times-circle mr-2"></i>לא נכון. אזור הדחייה הוא עבור ערכים שגדולים בערכם המוחלט מ-2.131. הערך שלנו (2) קטן יותר, ולכן הוא באזור קבלת `H_0`.';
                showFeedback('feedback-ttest', message, isCorrect);
            });
        }
        function setupNonParaQuiz() {
            document.getElementById('nonpara-buttons')?.addEventListener('click', e => {
                if (e.target.tagName !== 'BUTTON') return;
                const isCorrect = e.target.dataset.answer === 'nonpara';
                const message = isCorrect
                    ? '<i class="fas fa-check-circle mr-2"></i>בחירה מצוינת! מכיוון שהנתונים הם דירוג (סולם סדר) והמדגם קטן (`n=15`), מבחן א-פרמטרי הוא הבחירה הנכונה והבטוחה ביותר.'
                    : '<i class="fas fa-times-circle mr-2"></i>לא הבחירה הטובה ביותר. מבחן t מניח נתונים בסולם רווח/מנה והתפלגות נורמלית, הנחות שלא בהכרח מתקיימות כאן.';
                showFeedback('feedback-nonpara', message, isCorrect);
            });
        }
        function setupChiSquareQuiz() {
            document.getElementById('chi-check-btn')?.addEventListener('click', () => {
                const expected = parseFloat(document.getElementById('chi-expected').value);
                const correctExpected = (30 * 35) / 70;
                const isCorrect = Math.abs(expected - correctExpected) < 0.01;
                const message = isCorrect
                    ? `<i class="fas fa-check-circle mr-2"></i>נכון מאוד! החישוב הוא ` + '`E = (30 * 35) / 70 = 15`' + `. כעת ניתן לחשב את תרומת התא לסטטיסטי: ` + '`\frac{(20-15)^2}{15} = 1.67`'
                    : `<i class="fas fa-times-circle mr-2"></i>לא מדויק. החישוב צריך להיות (סך הכל שורה * סך הכל עמודה) / סך הכל כללי. נסה שוב!`;
                showFeedback('feedback-chi', message, isCorrect);
            });
        }
        function setupCaseStudyQuiz() {
            document.getElementById('case-q1')?.addEventListener('click', e => {
                 if (e.target.tagName !== 'BUTTON') return;
                 const isCorrect = e.target.dataset.correct === 'true';
                 const message = isCorrect ? 'נכון, אלו אותם נבדקים שנמדדו פעמיים.' : 'לא נכון, מדובר באותם סטודנטים לפני ואחרי.';
                 showFeedback('feedback-case', message, isCorrect);
            });
             document.getElementById('case-q2')?.addEventListener('click', e => {
                 if (e.target.tagName !== 'BUTTON') return;
                 const isCorrect = e.target.dataset.correct === 'true';
                 const message = isCorrect ? 'בדיוק! מכיוון שהמדגם מזווג והנתונים אינם מתפלגים נורמלית, וילקוקסון היא הבחירה הנכונה.' : 'לא נכון. מבחן t דורש הנחת נורמליות, שלא מתקיימת כאן.';
                 showFeedback('feedback-case', message, isCorrect);
            });
        }
        function setupStatisticalNavigator() {
            const decisionTree = {
                start: { question: "כמה מדגמים יש במחקר?", options: { "מדגם אחד": "q_one_sample", "שני מדגמים בלתי תלויים": "q_two_independent", "שני מדגמים מזווגים": "q_paired_samples" } },
                q_one_sample: { question: "מה בודקים?", options: { "תוחלת (ממוצע)": "q_one_mean", "פרופורציה": "q_one_prop", "שונות": "result_chi_square_variance", "טיב התאמה": "result_chi_square_gof" } },
                q_one_mean: { question: "האם שונות האוכלוסייה (`\\sigma^2`) ידועה?", options: { "כן": "result_z_test_one", "לא": "q_one_mean_sigma_unknown" } },
                q_one_mean_sigma_unknown: { question: "האם המדגם גדול (n > 30) או שמתקיימת הנחת נורמליות?", options: { "כן": "result_t_test_one", "לא": "result_non_parametric_placeholder" } },
                q_one_prop: { question: "האם מתקיימים תנאי הקירוב לנורמל (`np>10, nq>10`)?", options: { "כן": "result_z_test_prop_one", "לא": "result_binomial_test" } },
                q_two_independent: { question: "מה בודקים?", options: { "הפרש תוחלות": "q_two_ind_mean", "הפרש פרופורציות": "q_two_prop", "יחס שונויות": "result_f_test" } },
                q_two_ind_mean: { question: "האם המדגמים גדולים (n>30) או שמתקיימת הנחת נורמליות?", options: { "כן": "q_two_ind_mean_normal", "לא": "result_wilcoxon_rank_sum" } },
                q_two_ind_mean_normal: { question: "האם השונויות ידועות?", options: { "כן": "result_z_test_two", "לא": "result_t_test_two_independent" } },
                q_two_prop: { question: "האם מתקיימים תנאי הקירוב לנורמל?", options: { "כן": "result_z_test_prop_two", "לא": "result_fisher_exact" } },
                q_paired_samples: { question: "מה בודקים?", options: { "הפרש תוחלות": "q_paired_mean", "פרופורציה (שינוי)": "q_paired_prop" } },
                q_paired_mean: { question: "האם הפרשי הזוגות מתפלגים נורמלית או שהמדגם גדול (n>30)?", options: { "כן": "result_t_test_paired", "לא": "result_wilcoxon_signed_rank" } },
                q_paired_prop: { question: "האם מדובר בנתונים דיכוטומיים והמדגם גדול (`B+C>20`)?", options: { "כן": "result_mcnemar", "לא": "result_sign_test" } },
                result_z_test_one: { result: "מבחן Z לתוחלת במדגם יחיד" }, result_t_test_one: { result: "מבחן t לתוחלת במדגם יחיד" },
                result_chi_square_variance: { result: "מבחן `\\chi^2` לשונות" }, result_chi_square_gof: { result: "מבחן `\\chi^2` לטיב התאמה" },
                result_z_test_prop_one: { result: "מבחן Z לפרופורציה במדגם יחיד" }, result_binomial_test: { result: "מבחן הבינום" },
                result_wilcoxon_rank_sum: { result: "מבחן וילקוקסון לסכום דרגות (Mann-Whitney U)" }, result_z_test_two: { result: "מבחן Z להפרש תוחלות (שונויות ידועות)" },
                result_t_test_two_independent: { result: "מבחן t להפרש תוחלות למדגמים בלתי תלויים" }, result_f_test: { result: "מבחן F ליחס שונויות" },
                result_z_test_prop_two: { result: "מבחן Z להפרש פרופורציות" }, result_fisher_exact: { result: "מבחן פישר המדויק" },
                result_t_test_paired: { result: "מבחן t למדגמים מזווגים" }, result_wilcoxon_signed_rank: { result: "מבחן וילקוקסון לדרגות מסומנות" },
                result_mcnemar: { result: "מבחן מקנמר" }, result_sign_test: { result: "מבחן הסימן" },
                result_non_parametric_placeholder: { result: "מבחן א-פרמטרי למדגם יחיד (כמו וילקוקסון לדרגות מסומנות על ההפרשים מקבוע)" }
            };
            const questionEl = document.getElementById('navigator-question');
            const optionsEl = document.getElementById('navigator-options');
            const resultEl = document.getElementById('navigator-result');
            const resetBtn = document.getElementById('navigator-reset');
            let currentNodeKey = 'start';
            function renderNode(nodeKey) {
                const node = decisionTree[nodeKey];
                optionsEl.innerHTML = '';
                if (node.result) {
                    questionEl.textContent = 'המבחן המתאים הוא:';
                    resultEl.innerHTML = node.result;
                    resultEl.classList.remove('hidden');
                    resetBtn.classList.remove('hidden');
                } else {
                    questionEl.innerHTML = node.question;
                    for (const [optionText, nextNodeKey] of Object.entries(node.options)) {
                        const button = document.createElement('button');
                        button.textContent = optionText;
                        button.className = 'navigator-btn w-full text-right bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded';
                        button.onclick = () => renderNode(nextNodeKey);
                        optionsEl.appendChild(button);
                    }
                }
                if (window.renderMathInElement) {
                    renderMathInElement(document.body);
                }
            }
            resetBtn.addEventListener('click', () => {
                resultEl.classList.add('hidden');
                resetBtn.classList.add('hidden');
                renderNode('start');
            });
            renderNode('start');
        }
    </script>
</body>
</html>
