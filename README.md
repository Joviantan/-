[hsk_2_3_vocabulary_flashcards_app.html](https://github.com/user-attachments/files/34267269/hsk_2_3_vocabulary_flashcards_app.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HSK 2-3 词汇互动卡片 - 普吉岛高中汉语课堂</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- Google Fonts: Sarabun & Noto Serif SC -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=Noto+Serif+SC:wght@600;700;900&display=swap" rel="stylesheet">

    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* Typography System */
        .font-zh {
            font-family: 'SimSun', 'SongTi', 'Noto Serif SC', STSong, serif;
        }

        .font-py {
            font-family: 'STKaiti', 'STFangsong', 'Kaiti SC', KaiTi, cursive, sans-serif;
        }

        .font-th {
            font-family: 'Sarabun', 'Leelawadee', sans-serif;
        }

        /* 3D Flip Card Animation */
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

        /* Standardized Ruby Alignment for Pinyin */
        ruby {
            ruby-position: over;
            display: inline-flex;
            flex-direction: column-reverse;
            align-items: center;
            vertical-align: bottom;
        }
        
        rt {
            font-family: 'STKaiti', 'STFangsong', 'Kaiti SC', KaiTi, cursive, sans-serif;
            font-size: 0.65em;
            line-height: 1.2;
            color: #0284c7;
            font-weight: 600;
            text-align: center;
            user-select: none;
        }

        /* Custom Scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-slate-100 via-indigo-50/40 to-sky-100/50 text-slate-800 font-th min-h-screen flex flex-col justify-between selection:bg-teal-200 selection:text-teal-900">

    <!-- HEADER / NAVIGATION BAR -->
    <header class="bg-white/80 backdrop-blur-md border-b border-indigo-100/80 sticky top-0 z-40 shadow-sm">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- App Title -->
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-teal-600 to-indigo-600 text-white flex items-center justify-center font-bold font-zh text-2xl shadow-md shadow-indigo-500/20">
                        词
                    </div>
                    <div>
                        <h1 class="text-base sm:text-lg font-bold font-zh text-slate-900 flex items-center gap-2">
                            HSK 2-3 进阶词汇卡片
                            <span class="text-xs bg-indigo-100 text-indigo-800 font-th px-2.5 py-0.5 rounded-full font-semibold border border-indigo-200">M4 - M6 普吉高中</span>
                        </h1>
                        <p class="text-xs text-slate-500 font-th">บัตรคำศัพท์ HSK 2-3 สำหรับนักเรียนมัธยมศึกษา (Phuket Edition)</p>
                    </div>
                </div>

                <!-- Right Action Bar -->
                <div class="flex items-center space-x-2 sm:space-x-3">
                    <button onclick="toggleMasteredModal()" class="bg-emerald-50 hover:bg-emerald-100 text-emerald-800 border border-emerald-200 px-3 py-1.5 rounded-xl text-xs font-semibold transition flex items-center gap-1.5 shadow-sm">
                        <i class="fa-solid fa-circle-check text-emerald-600"></i>
                        <span>已掌握: <strong id="header-mastered-count" class="font-mono text-sm">0</strong></span>
                    </button>

                    <div class="bg-slate-100 p-1 rounded-xl flex items-center text-xs border border-slate-200">
                        <button onclick="setViewMode('single')" id="btn-view-single" class="px-2.5 py-1 rounded-lg bg-white text-indigo-950 font-bold shadow-sm transition flex items-center gap-1">
                            <i class="fa-solid fa-clone"></i> <span class="hidden sm:inline">单卡模式</span>
                        </button>
                        <button onclick="setViewMode('grid')" id="btn-view-grid" class="px-2.5 py-1 rounded-lg text-slate-600 hover:text-slate-900 transition flex items-center gap-1">
                            <i class="fa-solid fa-border-all"></i> <span class="hidden sm:inline">网格模式</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Category & Filter Controls -->
        <div class="bg-indigo-50/60 border-t border-indigo-100/50 px-4 py-2">
            <div class="max-w-6xl mx-auto flex flex-wrap items-center justify-between gap-2 text-xs">
                <!-- Part of Speech Filters -->
                <div class="flex items-center gap-1.5 overflow-x-auto pb-1 sm:pb-0 scrollbar-none" id="category-filters">
                    <button onclick="filterCategory('all')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-teal-700 text-white shadow-sm" data-cat="all">全部 (All)</button>
                    <button onclick="filterCategory('名')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="名">名词 (Nouns)</button>
                    <button onclick="filterCategory('动')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="动">动词 (Verbs)</button>
                    <button onclick="filterCategory('形')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="形">形容词 (Adj)</button>
                    <button onclick="filterCategory('副')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="副">副词/介词</button>
                    <button onclick="filterCategory('量')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="量">量词/数词</button>
                    <button onclick="filterCategory('其他')" class="cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200" data-cat="其他">代词/连词/关联</button>
                </div>

                <!-- Action Tools -->
                <div class="flex items-center gap-2">
                    <button onclick="shuffleDeck()" class="px-3 py-1 rounded-lg bg-teal-600 hover:bg-teal-500 text-white font-bold transition flex items-center gap-1 shadow-sm">
                        <i class="fa-solid fa-shuffle"></i> 随机乱序
                    </button>
                    <button onclick="resetAllMastered()" class="px-2.5 py-1 rounded-lg bg-slate-200 hover:bg-slate-300 text-slate-700 font-semibold transition flex items-center gap-1" title="重置已掌握列表">
                        <i class="fa-solid fa-rotate-left"></i> 重置进度
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN APP STUDY AREA -->
    <main class="flex-grow max-w-4xl w-full mx-auto px-4 py-6 flex flex-col justify-center">

        <!-- PROGRESS & METRICS BAR -->
        <div class="mb-4 space-y-1.5 max-w-xl mx-auto w-full">
            <div class="flex justify-between items-center text-xs text-slate-600 font-medium">
                <span id="deck-status-text">待学习词汇: 0</span>
                <span id="progress-percentage-text" class="font-mono text-teal-700 font-bold">0% 已掌握</span>
            </div>
            <div class="w-full h-2.5 bg-slate-200/80 rounded-full overflow-hidden shadow-inner">
                <div id="progress-bar" class="h-full bg-gradient-to-r from-teal-500 to-indigo-600 transition-all duration-300" style="width: 0%"></div>
            </div>
        </div>

        <!-- MODE 1: SINGLE CARD VIEW -->
        <div id="view-single-container" class="flex flex-col items-center justify-center space-y-6">
            
            <!-- FLIP CARD -->
            <div class="w-full max-w-md h-80 sm:h-96 perspective-1000 group cursor-pointer" onclick="flipCurrentCard()">
                <div id="active-card-inner" class="relative w-full h-full transform-style-3d transition-transform duration-500 ease-out shadow-2xl rounded-3xl bg-white border border-slate-200/80">
                    
                    <!-- CARD FRONT (Chinese Only) -->
                    <div class="absolute inset-0 w-full h-full backface-hidden rounded-3xl p-6 flex flex-col justify-between items-center bg-gradient-to-b from-white via-slate-50/40 to-teal-50/30">
                        <div class="w-full flex justify-between items-center text-slate-400 text-xs">
                            <span class="bg-indigo-100 text-indigo-900 font-bold px-2.5 py-0.5 rounded-full font-mono" id="card-front-pos">名</span>
                            <span class="text-slate-400 italic flex items-center gap-1">
                                <i class="fa-solid fa-hand-pointer text-teal-600 animate-bounce"></i> 点击翻面 (Tap Card)
                            </span>
                        </div>

                        <!-- Main Hanzi Display -->
                        <div class="my-auto text-center">
                            <h2 id="card-front-chinese" class="text-6xl sm:text-7xl font-bold font-zh text-slate-900 tracking-wider">
                                阿姨
                            </h2>
                        </div>

                        <!-- Card Footer Controls -->
                        <div class="w-full flex justify-between items-center">
                            <button onclick="event.stopPropagation(); speakActiveWord()" class="w-10 h-10 rounded-full bg-teal-50 hover:bg-teal-100 text-teal-700 flex items-center justify-center transition border border-teal-200/60" title="听普通话发音 (Key: S)">
                                <i class="fa-solid fa-volume-high text-base"></i>
                            </button>
                            <span id="card-counter-indicator" class="font-mono text-xs text-slate-400 font-medium">1 / 198</span>
                        </div>
                    </div>

                    <!-- CARD BACK (Pinyin + Thai + Word Class + English) -->
                    <div class="absolute inset-0 w-full h-full backface-hidden rotate-y-180 rounded-3xl p-6 flex flex-col justify-between items-center bg-white border-2 border-teal-500">
                        <div class="w-full flex justify-between items-center text-xs">
                            <span class="bg-teal-700 text-white font-bold px-2.5 py-0.5 rounded-full font-mono" id="card-back-pos">名</span>
                            <span class="text-xs text-teal-700 font-bold">背面释义 (Translation)</span>
                        </div>

                        <!-- Card Content -->
                        <div class="my-auto text-center space-y-3 w-full">
                            <!-- Character with Pinyin Alignment -->
                            <div class="inline-block">
                                <ruby class="text-4xl sm:text-5xl font-bold font-zh text-slate-900">
                                    <rb id="card-back-chinese">阿姨</rb>
                                    <rt id="card-back-pinyin" class="text-lg sm:text-xl font-py text-sky-600 font-bold mb-1">ā yí</rt>
                                </ruby>
                            </div>

                            <!-- Thai Translation Box -->
                            <div class="bg-teal-50/70 rounded-2xl p-3 border border-teal-200/80">
                                <p class="text-[11px] text-slate-400 font-semibold mb-0.5">ความหมายภาษาไทย (Thai)</p>
                                <p id="card-back-thai" class="text-xl font-bold text-teal-950 font-th">น้า, ป้า (น้องสาวแม่)</p>
                            </div>

                            <!-- English Definition -->
                            <p id="card-back-english" class="text-xs text-slate-500 font-mono italic">auntie [mother's younger sister]</p>
                        </div>

                        <!-- Audio Button -->
                        <div class="w-full flex justify-center">
                            <button onclick="event.stopPropagation(); speakActiveWord()" class="px-4 py-1.5 rounded-full bg-sky-50 hover:bg-sky-100 text-sky-700 text-xs font-semibold transition flex items-center gap-2 border border-sky-200">
                                <i class="fa-solid fa-volume-high"></i> 听发音 (Listen)
                            </button>
                        </div>
                    </div>

                </div>
            </div>

            <!-- ACTION CONTROL BUTTONS -->
            <div class="w-full max-w-md flex items-center justify-between gap-3">
                <button onclick="prevCard()" class="flex-1 py-3 bg-white hover:bg-slate-50 border border-slate-200 text-slate-700 font-bold text-sm rounded-2xl shadow-sm transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-arrow-left"></i> 上一个
                </button>

                <button onclick="markCurrentMastered()" class="flex-1 py-3 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm rounded-2xl shadow-md transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-check-double"></i> 已掌握 (M)
                </button>

                <button onclick="nextCard()" class="flex-1 py-3 bg-white hover:bg-slate-50 border border-slate-200 text-slate-700 font-bold text-sm rounded-2xl shadow-sm transition flex items-center justify-center gap-2">
                    下一个 <i class="fa-solid fa-arrow-right"></i>
                </button>
            </div>

            <!-- KEYBOARD SHORTCUTS INSTRUCTION -->
            <p class="text-[11px] text-slate-400 text-center">
                💡 <span class="font-semibold text-slate-500">快捷键:</span> [空格键]: 翻卡 | [←/→]: 切换 | [M]: 标记已掌握 | [S]: 朗读发音
            </p>
        </div>

        <!-- MODE 2: GRID OVERVIEW -->
        <div id="view-grid-container" class="hidden space-y-4">
            <div class="flex justify-between items-center text-xs text-slate-500">
                <span>点击卡片直接复习单字，点击 ✔️ 快捷标记已掌握</span>
                <span id="grid-count-indicator">共 0 个词汇</span>
            </div>
            <div id="grid-cards-wrapper" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-3">
                <!-- Javascript will render dynamic grid here -->
            </div>
        </div>

    </main>

    <!-- MASTERED LIST MODAL -->
    <div id="mastered-modal" class="fixed inset-0 bg-slate-950/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-xl w-full p-6 space-y-4 shadow-2xl border border-slate-200 max-h-[85vh] flex flex-col">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <div class="flex items-center gap-2">
                    <div class="w-8 h-8 rounded-full bg-emerald-100 text-emerald-700 flex items-center justify-center font-bold">
                        <i class="fa-solid fa-trophy text-sm"></i>
                    </div>
                    <div>
                        <h3 class="font-bold text-slate-900 font-zh text-base">已掌握词汇库 (Mastered Words)</h3>
                        <p class="text-xs text-slate-500">รายการคำศัพท์ที่เรียนรู้แล้ว (คลิกเพื่อกู้คืน)</p>
                    </div>
                </div>
                <button onclick="toggleMasteredModal()" class="text-slate-400 hover:text-slate-600 p-2">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <!-- Mastered Item Stream -->
            <div id="mastered-items-list" class="flex-grow overflow-y-auto space-y-2 pr-1 text-xs">
                <!-- Javascript dynamic loading -->
            </div>

            <!-- Footer Controls -->
            <div class="pt-3 border-t border-slate-100 flex justify-between items-center">
                <button onclick="resetAllMastered()" class="text-xs text-rose-600 hover:text-rose-800 font-semibold flex items-center gap-1">
                    <i class="fa-solid fa-rotate-left"></i> 全部重置复习进度
                </button>
                <button onclick="toggleMasteredModal()" class="px-4 py-2 bg-slate-900 text-white rounded-xl text-xs font-bold hover:bg-slate-800">
                    关闭窗口
                </button>
            </div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer class="bg-white/60 border-t border-slate-200/60 py-3 text-center text-xs text-slate-400">
        <p>© HSK 2-3 Vocabulary Flashcard App • Designed for Thai High School Students in Phuket</p>
    </footer>

    <!-- SCRIPT LOGIC & COMPLETE DATASET -->
    <script>
        // FULL DATASET (All HSK 2/3 Vocab Items Provided by User)
        const fullVocabData = [
            { ch: "阿姨", py: "ā yí", pos: "名", en: "auntie [mother's younger sister]", th: "น้า, ป้า (น้องสาวแม่)" },
            { ch: "啊", py: "a", pos: "助", en: "ah (exclamation particle)", th: "อ๊ะ, อ๋อ, นะ" },
            { ch: "矮", py: "ǎi", pos: "形", en: "short [height]", th: "เตี้ย, ต่ำ" },
            { ch: "爱好", py: "ài hào", pos: "名", en: "interests; hobbies", th: "งานอดิเรก, ความสนใจ" },
            { ch: "安静", py: "ān jìng", pos: "动/形", en: "to be quiet; peaceful", th: "เงียบสงบ" },
            { ch: "把", py: "bǎ", pos: "介/量", en: "grasp; [measure word for chairs/knives]", th: "เอา, นำ; ด้าม/ตัว (ลักษณะนาม)" },
            { ch: "搬", py: "bān", pos: "动", en: "to move", th: "ย้าย" },
            { ch: "班", py: "bān", pos: "名", en: "class", th: "ห้องเรียน, ชั้นเรียน" },
            { ch: "半", py: "bàn", pos: "数", en: "half", th: "ครึ่ง" },
            { ch: "办法", py: "bàn fǎ", pos: "名", en: "way; method; solution", th: "วิธี, ทางออก" },
            { ch: "办公室", py: "bàn gōng shì", pos: "名", en: "office", th: "ห้องทำงาน, สำนักงาน" },
            { ch: "帮忙", py: "bāng máng", pos: "动", en: "lend a hand; help", th: "ช่วยเหลืองาน" },
            { ch: "包", py: "bāo", pos: "名/量", en: "a packet of; package; bag", th: "กระเป๋า, ห่อ" },
            { ch: "饱", py: "bǎo", pos: "形", en: "full up; satisfied after eating", th: "อิ่ม" },
            { ch: "北方", py: "běi fāng", pos: "名", en: "the north", th: "ทิศเหนือ, ทางเหนือ" },
            { ch: "被", py: "bèi", pos: "介", en: "by (passive particle); quilt", th: "ถูก, โดน (กริยาวิเศษณ์ถูกกระทำ)" },
            { ch: "鼻子", py: "bí zi", pos: "名", en: "nose", th: "จมูก" },
            { ch: "笔记本", py: "bǐ jì běn", pos: "名", en: "notebook; laptop", th: "สมุดบันทึก, โน้ตบุ๊ก" },
            { ch: "比较", py: "bǐ jiào", pos: "副/动", en: "fairly; compare", th: "ค่อนข้าง, เปรียบเทียบ" },
            { ch: "比赛", py: "bǐ sài", pos: "名/动", en: "competition; match", th: "การแข่งขัน" },
            { ch: "必须", py: "bì xū", pos: "副", en: "must; have to", th: "ต้อง, จำเป็นต้อง" },
            { ch: "变化", py: "biàn huà", pos: "名/动", en: "change; variation", th: "การเปลี่ยนแปลง" },
            { ch: "别人", py: "bié ren", pos: "代", en: "other people", th: "คนอื่น" },
            { ch: "冰箱", py: "bīng xiāng", pos: "名", en: "refrigerator; fridge", th: "ตู้เย็น" },
            { ch: "不但……而且……", py: "bù dàn ... ér qiě ...", pos: "关联", en: "not only ... but also ...", th: "ไม่เพียงแต่...อีกทั้งยัง..." },
            { ch: "菜单", py: "cài dān", pos: "名", en: "menu", th: "เมนูอาหาร" },
            { ch: "参加", py: "cān jiā", pos: "动", en: "to take part; join", th: "เข้าร่วม" },
            { ch: "草", py: "cǎo", pos: "名", en: "grass", th: "หญ้า" },
            { ch: "层", py: "céng", pos: "量", en: "storey; floor; layer", th: "ชั้น (ลักษณะนามของตึก)" },
            { ch: "差", py: "chà", pos: "动/形", en: "lack; poor quality; bad", th: "ขาด, แย่, แย่กว่า" },
            { ch: "尝", py: "cháng", pos: "动", en: "to taste", th: "ชิม" },
            { ch: "超市", py: "chāo shì", pos: "名", en: "supermarket", th: "ซูเปอร์มาร์เก็ต" },
            { ch: "衬衫", py: "chèn shān", pos: "名", en: "shirt", th: "เสื้อเชิ้ต" },
            { ch: "成绩", py: "chéng jì", pos: "名", en: "results; marks; score", th: "คะแนน, ผลการเรียน" },
            { ch: "城市", py: "chéng shì", pos: "名", en: "city", th: "เมือง" },
            { ch: "迟到", py: "chí dào", pos: "动", en: "arrive late", th: "มาสาย" },
            { ch: "除了", py: "chú le", pos: "介", en: "apart from; besides", th: "นอกจาก" },
            { ch: "船", py: "chuán", pos: "名", en: "boat; ship; ferry", th: "เรือ" },
            { ch: "春", py: "chūn", pos: "名", en: "spring (season)", th: "ฤดูใบไม้ผลิ" },
            { ch: "词典", py: "cí diǎn", pos: "名", en: "dictionary", th: "พจนานุกรม" },
            { ch: "聪明", py: "cōng ming", pos: "形", en: "clever; intelligent", th: "ฉลาด" },
            { ch: "打扫", py: "dǎ sǎo", pos: "动", en: "to clean; sweep", th: "ทำความสะอาด" },
            { ch: "打算", py: "dǎ suàn", pos: "动/名", en: "plan; intention", th: "วางแผน, ตั้งใจ" },
            { ch: "带", py: "dài", pos: "动", en: "carry; bring", th: "พก, นำ, พาส่ง" },
            { ch: "担心", py: "dān xīn", pos: "动", en: "worry; feel anxious", th: "เป็นห่วง, กังวล" },
            { ch: "蛋糕", py: "dàn gāo", pos: "名", en: "cake", th: "เค้ก" },
            { ch: "当然", py: "dāng rán", pos: "副", en: "of course; naturally", th: "แน่นอน" },
            { ch: "地", py: "de", pos: "助", en: "...ly [particle linking adverb to verb]", th: "อย่าง (คำเชื่อมกริยาวิเศษณ์)" },
            { ch: "灯", py: "dēng", pos: "名", en: "lamp; light", th: "โคมไฟ, หลอดไฟ" },
            { ch: "地方", py: "dì fang", pos: "名", en: "place; location", th: "สถานที่" },
            { ch: "地铁", py: "dì tiě", pos: "名", en: "underground train; metro", th: "รถไฟฟ้าใต้ดิน MRT" },
            { ch: "地图", py: "dì tú", pos: "名", en: "map", th: "แผนที่" },
            { ch: "电梯", py: "diàn tī", pos: "名", en: "lift; elevator", th: "ลิฟต์" },
            { ch: "电子邮件", py: "diàn zǐ yóu jiàn", pos: "名", en: "email", th: "อีเมล" },
            { ch: "东", py: "dōng", pos: "名", en: "east", th: "ทิศตะวันออก" },
            { ch: "冬", py: "dōng", pos: "名", en: "winter", th: "ฤดูหนาว" },
            { ch: "动物", py: "dòng wù", pos: "名", en: "animals", th: "สัตว์" },
            { ch: "短", py: "duǎn", pos: "形", en: "short [length]", th: "สั้น" },
            { ch: "段", py: "duàn", pos: "量", en: "section; paragraph", th: "ช่วง, ตอน, ช่วงเวลา" },
            { ch: "锻炼", py: "duàn liàn", pos: "动", en: "engage in physical exercise", th: "ออกกำลังกาย" },
            { ch: "多么", py: "duō me", pos: "副", en: "how ...!; so ...", th: "ช่าง...เสียจริง" },
            { ch: "饿", py: "è", pos: "形", en: "hungry", th: "หิว" },
            { ch: "耳朵", py: "ěr duo", pos: "名", en: "ears", th: "หู" },
            { ch: "发", py: "fā", pos: "动", en: "to send (an email, message)", th: "ส่ง" },
            { ch: "发烧", py: "fā shāo", pos: "动", en: "have a fever", th: "เป็นไข้, ตัวร้อน" },
            { ch: "发现", py: "fā xiàn", pos: "动", en: "discover; find out", th: "ค้นพบ, พบว่า" },
            { ch: "方便", py: "fāng biàn", pos: "形", en: "convenient", th: "สะดวก" },
            { ch: "放", py: "fàng", pos: "动", en: "to put; set free", th: "วาง, ใส่, ปล่อย" },
            { ch: "放心", py: "fàng xīn", pos: "动", en: "relax; feel relieved", th: "วางใจ, สบายใจ" },
            { ch: "分", py: "fēn", pos: "量/动", en: "minute; point; divide", th: "นาที, คะแนน, แบ่ง" },
            { ch: "附近", py: "fù jìn", pos: "名", en: "nearby; vicinity", th: "บริเวณใกล้เคียง" },
            { ch: "复习", py: "fù xí", pos: "动", en: "revise; review lessons", th: "ทบทวน" },
            { ch: "干净", py: "gān jìng", pos: "形", en: "clean", th: "สะอาด" },
            { ch: "感冒", py: "gǎn mào", pos: "动/名", en: "to catch a cold", th: "เป็นหวัด" },
            { ch: "感兴趣", py: "gǎn xìng qù", pos: "动", en: "to be interested (in)", th: "สนใจใน..." },
            { ch: "刚才", py: "gāng cái", pos: "名", en: "just now", th: "เมื่อกี้" },
            { ch: "个子", py: "gè zi", pos: "名", en: "height; stature", th: "รูปร่าง, ความสูง" },
            { ch: "跟", py: "gēn", pos: "介/连", en: "with; follow", th: "กับ, ตาม" },
            { ch: "根据", py: "gēn jù", pos: "介/名", en: "according to; basis", th: "ตามที่, อ้างอิงจาก" },
            { ch: "更", py: "gèng", pos: "副", en: "even more", th: "ยิ่งขึ้น, ยิ่งกว่า" },
            { ch: "公斤", py: "gōng jīn", pos: "量", en: "kilogram", th: "กิโลกรัม" },
            { ch: "公园", py: "gōng yuán", pos: "名", en: "park", th: "สวนสาธารณะ" },
            { ch: "故事", py: "gù shi", pos: "名", en: "story; tale", th: "นิทาน, เรื่องราว" },
            { ch: "刮风", py: "guā fēng", pos: "动", en: "windy; blow wind", th: "ลมพัด" },
            { ch: "关", py: "guān", pos: "动", en: "to close; turn off", th: "ปิด" },
            { ch: "关系", py: "guān xì", pos: "名", en: "relationship", th: "ความสัมพันธ์" },
            { ch: "关心", py: "guān xīn", pos: "动", en: "care about; concerned", th: "เอาใจใส่, ห่วงใย" },
            { ch: "关于", py: "guān yú", pos: "介", en: "about; regarding", th: "เกี่ยวกับ" },
            { ch: "国家", py: "guó jiā", pos: "名", en: "country; nation", th: "ประเทศ" },
            { ch: "过", py: "guò", pos: "动", en: "to celebrate; pass", th: "ฉลอง, ผ่าน" },
            { ch: "过去", py: "guò qu", pos: "名/动", en: "(in the) past; go over", th: "อดีต, ผ่านไป" },
            { ch: "还是", py: "hái shì", pos: "副/连", en: "...or...? / still", th: "หรือ (ใช้ในคำถาม)" },
            { ch: "害怕", py: "hài pà", pos: "动", en: "afraid; scared", th: "กลัว" },
            { ch: "黑板", py: "hēi bǎn", pos: "名", en: "blackboard", th: "กระดานดำ" },
            { ch: "后来", py: "hòu lái", pos: "名", en: "afterward; later", th: "ต่อมา, ภายหลัง" },
            { ch: "护照", py: "hù zhào", pos: "名", en: "passport", th: "หนังสือเดินทาง" },
            { ch: "花", py: "huā", pos: "动/名", en: "spend (money/time); flower", th: "ใช้จ่าย; ดอกไม้" },
            { ch: "画", py: "huà", pos: "名/动", en: "to draw; painting", th: "วาดรูป, ภาพวาด" },
            { ch: "坏", py: "huài", pos: "形", en: "bad; broken", th: "เลว, เสีย" },
            { ch: "欢迎", py: "huān yíng", pos: "动", en: "to welcome", th: "ยินดีต้อนรับ" },
            { ch: "还", py: "huán", pos: "动", en: "to return (something)", th: "คืน (ของ)" },
            { ch: "环境", py: "huán jìng", pos: "名", en: "environment", th: "สิ่งแวดล้อม" },
            { ch: "换", py: "huàn", pos: "动", en: "to change; exchange", th: "เปลี่ยน, แลกเปลี่ยน" },
            { ch: "黄河", py: "huáng hé", pos: "名", en: "Yellow River", th: "แม่น้ำหวงเหอ" },
            { ch: "回答", py: "huí dá", pos: "动", en: "reply; answer", th: "ตอบ, คำตอบ" },
            { ch: "会议", py: "huì yì", pos: "名", en: "meeting; conference", th: "การประชุม" },
            { ch: "或者", py: "huò zhě", pos: "连", en: "or (in statement)", th: "หรือ (ใช้ในประโยคบอกเล่า)" },
            { ch: "几乎", py: "jī hū", pos: "副", en: "almost; nearly", th: "เกือบจะ" },
            { ch: "机会", py: "jī huì", pos: "名", en: "opportunity; chance", th: "โอกาส" },
            { ch: "极", py: "jí", pos: "副", en: "extremely", th: "ที่สุด, อย่างยิ่ง" },
            { ch: "记得", py: "jì de", pos: "动", en: "to remember", th: "จำได้" },
            { ch: "季节", py: "jì jié", pos: "名", en: "season", th: "ฤดูกาล" },
            { ch: "检查", py: "jiǎn chá", pos: "动", en: "inspect; examine", th: "ตรวจ, ตรวจสอบ" },
            { ch: "简单", py: "jiǎn dān", pos: "形", en: "simple; easy", th: "ง่าย, ไม่ซับซ้อน" },
            { ch: "健康", py: "jiàn kāng", pos: "形/名", en: "healthy; health", th: "สุขภาพแข็งแรง" },
            { ch: "见面", py: "jiàn miàn", pos: "动", en: "to meet; see someone", th: "พบกัน, เจอหน้า" },
            { ch: "讲", py: "jiǎng", pos: "动", en: "speak; explain", th: "พูด, อธิบาย" },
            { ch: "教", py: "jiāo", pos: "动", en: "to teach", th: "สอน" },
            { ch: "脚", py: "jiǎo", pos: "名", en: "foot", th: "เท้า" },
            { ch: "角", py: "jiǎo", pos: "量", en: "jiao (0.1 yuan); corner", th: "เหรียญสิบเซนต์, มุม" },
            { ch: "接", py: "jiē", pos: "动", en: "pick up (phone/person)", th: "รับ (โทรศัพท์/คน)" },
            { ch: "街道", py: "jiē dào", pos: "名", en: "street; road", th: "ถนน, ถนนหนทาง" },
            { ch: "结婚", py: "jié hūn", pos: "动", en: "marry; get married", th: "แต่งงาน" },
            { ch: "节目", py: "jié mù", pos: "名", en: "programme; show", th: "รายการ (ทีวี/แสดง)" },
            { ch: "节日", py: "jié rì", pos: "名", en: "festival; holiday", th: "เทศกาล" },
            { ch: "结束", py: "jié shù", pos: "动", en: "finish; end", th: "จบ, สิ้นสุด" },
            { ch: "解决", py: "jiě jué", pos: "动", en: "resolve; solve", th: "แก้ไขปัญหา" },
            { ch: "借", py: "jiè", pos: "动", en: "to lend; borrow", th: "ยืม, ให้ยืม" },
            { ch: "经常", py: "jīng cháng", pos: "副", en: "often; regularly", th: "บ่อยๆ" },
            { ch: "经过", py: "jīng guò", pos: "动/介", en: "pass through; via", th: "ผ่าน, หลังจาก" },
            { ch: "经理", py: "jīng lǐ", pos: "名", en: "manager", th: "ผู้จัดการ" },
            { ch: "久", py: "jiǔ", pos: "形", en: "long time", th: "นาน" },
            { ch: "旧", py: "jiù", pos: "形", en: "old; former", th: "เก่า" },
            { ch: "句子", py: "jù zi", pos: "名", en: "sentence", th: "ประโยค" },
            { ch: "决定", py: "jué dìng", pos: "动/名", en: "decide; decision", th: "ตัดสินใจ" },
            { ch: "渴", py: "kě", pos: "形", en: "thirsty", th: "กระหายน้ำ" },
            { ch: "可爱", py: "kě ài", pos: "形", en: "lovely; cute", th: "น่ารัก" },
            { ch: "刻", py: "kè", pos: "量", en: "quarter (15 mins)", th: "15 นาที (หนึ่งเค่อ)" },
            { ch: "客人", py: "kè rén", pos: "名", en: "guest; customer", th: "แขก, ลูกค้า" },
            { ch: "空调", py: "kōng tiáo", pos: "名", en: "air-conditioning", th: "เครื่องปรับอากาศ" },
            { ch: "口", py: "kǒu", pos: "名/量", en: "mouth; measure for family", th: "ปาก; คน (สมาชิกในครอบครัว)" },
            { ch: "哭", py: "kū", pos: "动", en: "cry; weep", th: "ร้องไห้" },
            { ch: "裤子", py: "kù zi", pos: "名", en: "trousers; pants", th: "กางเกง" },
            { ch: "筷子", py: "kuài zi", pos: "名", en: "chopsticks", th: "ตะเกียบ" },
            { ch: "蓝", py: "lán", pos: "形", en: "blue", th: "สีฟ้า, สีน้ำเงิน" },
            { ch: "老", py: "lǎo", pos: "形", en: "old; aged", th: "แก่, เก่าแก่" },
            { ch: "离开", py: "lí kāi", pos: "动", en: "leave; depart", th: "จากไป, ออกจาก" },
            { ch: "礼物", py: "lǐ wù", pos: "名", en: "gift; present", th: "ของขวัญ" },
            { ch: "历史", py: "lì shǐ", pos: "名", en: "history", th: "ประวัติศาสตร์" },
            { ch: "脸", py: "liǎn", pos: "名", en: "face", th: "ใบหน้า" },
            { ch: "练习", py: "liàn xí", pos: "动/名", en: "to practise; exercise", th: "แบบฝึกหัด, ฝึกฝน" },
            { ch: "辆", py: "liàng", pos: "量", en: "[measure word for vehicles]", th: "คัน (ลักษณะนามของรถ)" },
            { ch: "聊天", py: "liáo tiān", pos: "动", en: "to chat", th: "พูดคุย, เม้าท์" },
            { ch: "了解", py: "liǎo jiě", pos: "动", en: "understand deeply", th: "เข้าใจอย่างลึกซึ้ง" },
            { ch: "邻居", py: "lín jū", pos: "名", en: "neighbour", th: "เพื่อนบ้าน" },
            { ch: "留学", py: "liú xué", pos: "动", en: "study abroad", th: "เรียนต่อต่างประเทศ" },
            { ch: "楼", py: "lóu", pos: "名", en: "multi-storied building", th: "ตึก, อาคาร" },
            { ch: "绿", py: "lǜ", pos: "形", en: "green", th: "สีเขียว" },
            { ch: "马", py: "mǎ", pos: "名", en: "horse", th: "ม้า" },
            { ch: "马上", py: "mǎ shàng", pos: "副", en: "immediately; right away", th: "ทันที" },
            { ch: "满意", py: "mǎn yì", pos: "动", en: "pleased; satisfied", th: "พึงพอใจ" },
            { ch: "帽子", py: "mào zi", pos: "名", en: "hat; cap", th: "หมวก" },
            { ch: "米", py: "mǐ", pos: "量/名", en: "metre; uncooked rice", th: "เมตร; ข้าวสาร" },
            { ch: "面包", py: "miàn bāo", pos: "名", en: "bread", th: "ขนมปัง" },
            { ch: "明白", py: "míng bai", pos: "动/形", en: "to understand; clear", th: "เข้าใจ, ชัดเจน" },
            { ch: "拿", py: "ná", pos: "动", en: "to take; hold", th: "หยิบ, ถือ" },
            { ch: "奶奶", py: "nǎi nai", pos: "名", en: "grandmother (paternal)", th: "ย่า" },
            { ch: "难", py: "nán", pos: "形", en: "hard; difficult", th: "ยาก" },
            { ch: "南", py: "nán", pos: "名", en: "south", th: "ทิศใต้" },
            { ch: "难过", py: "nán guò", pos: "形", en: "feel sad; hard time", th: "เสียใจ, เศร้าใจ" },
            { ch: "年级", py: "nián jí", pos: "名", en: "(school) grade/year", th: "ชั้นปี (ระดับการศึกษา)" },
            { ch: "年轻", py: "nián qīng", pos: "形", en: "young", th: "อายุน้อย, วัยรุ่น" },
            { ch: "鸟", py: "niǎo", pos: "名", en: "bird", th: "นก" },
            { ch: "努力", py: "nǔ lì", pos: "形", en: "hardworking; diligent", th: "ขยัน, ตั้งใจ" },
            { ch: "爬山", py: "pá shān", pos: "动", en: "climb mountains", th: "ปีนเขา" },
            { ch: "盘子", py: "pán zi", pos: "名", en: "tray; plate", th: "จาน" },
            { ch: "胖", py: "pàng", pos: "形", en: "fat; chubby", th: "อ้วน" },
            { ch: "啤酒", py: "pí jiǔ", pos: "名", en: "beer", th: "เบียร์" },
            { ch: "皮鞋", py: "pí xié", pos: "名", en: "leather shoes", th: "รองเท้าหนัง" },
            { ch: "瓶子", py: "píng zi", pos: "名", en: "bottle", th: "ขวด" },
            { ch: "骑", py: "qí", pos: "动", en: "ride (bike/horse)", th: "ขี่ (จักรยาน/ม้า)" },
            { ch: "奇怪", py: "qí guài", pos: "形", en: "strange; odd", th: "แปลก" },
            { ch: "其实", py: "qí shí", pos: "副", en: "in fact; actually", th: "จริงๆ แล้ว" },
            { ch: "其他", py: "qí tā", pos: "代", en: "other; else", th: "อื่นๆ" },
            { ch: "起飞", py: "qǐ fēi", pos: "动", en: "take off [plane]", th: "เครื่องบินขึ้น" },
            { ch: "起来", py: "qǐ lái", pos: "动", en: "stand up; rise", th: "ลุกขึ้น" },
            { ch: "清楚", py: "qīng chu", pos: "形", en: "clear; distinct", th: "ชัดเจน" },
            { ch: "请假", py: "qǐng jià", pos: "动", en: "ask for leave", th: "ลาหยุด" },
            { ch: "秋", py: "qiū", pos: "名", en: "autumn; fall", th: "ฤดูใบไม้ร่วง" },
            { ch: "裙子", py: "qún zi", pos: "名", en: "skirt; dress", th: "กระโปรง" },
            { ch: "然后", py: "rán hòu", pos: "连", en: "and then; after that", th: "หลังจากนั้น" },
            { ch: "热情", py: "rè qíng", pos: "形", en: "enthusiastic; warm", th: "อบอุ่น, อัธยาศัยดี" },
            { ch: "认为", py: "rèn wéi", pos: "动", en: "think that; consider", th: "คิดว่า, ถือว่า" },
            { ch: "认真", py: "rèn zhēn", pos: "形", en: "earnest; serious", th: "จริงจัง, ตั้งใจ" },
            { ch: "容易", py: "róng yì", pos: "形", en: "easy; simple", th: "ง่าย" },
            { ch: "如果", py: "rú guǒ", pos: "连", en: "if; in case", th: "ถ้าหาก" },
            { ch: "伞", py: "sǎn", pos: "名", en: "umbrella", th: "ร่ม" },
            { ch: "上网", py: "shàng wǎng", pos: "动", en: "get on the internet", th: "เล่นอินเทอร์เน็ต" },
            { ch: "生气", py: "shēng qì", pos: "动", en: "get angry", th: "โกรธ" },
            { ch: "声音", py: "shēng yīn", pos: "名", en: "sound; voice", th: "เสียง" },
            { ch: "试", py: "shì", pos: "动", en: "try; test", th: "ลอง" },
            { ch: "世界", py: "shì jiè", pos: "名", en: "world", th: "โลก" },
            { ch: "瘦", py: "shòu", pos: "形", en: "thin; lean", th: "ผอม" },
            { ch: "舒服", py: "shū fu", pos: "形", en: "comfortable", th: "สบาย" },
            { ch: "叔叔", py: "shū shu", pos: "名", en: "uncle (paternal)", th: "อา (น้องชายพ่อ)" },
            { ch: "树", py: "shù", pos: "名", en: "tree", th: "ต้นไม้" },
            { ch: "数学", py: "shù xué", pos: "名", en: "maths; mathematics", th: "คณิตศาสตร์" },
            { ch: "刷牙", py: "shuā yá", pos: "动", en: "brush teeth", th: "แปรงฟัน" },
            { ch: "双", py: "shuāng", pos: "量", en: "a pair of", th: "คู่ (ลักษณะนาม)" },
            { ch: "水平", py: "shuǐ píng", pos: "名", en: "level; standard", th: "ระดับ" },
            { ch: "司机", py: "sī jī", pos: "名", en: "driver", th: "คนขับรถ" },
            { ch: "太阳", py: "tài yáng", pos: "名", en: "sun", th: "พระอาทิตย์" },
            { ch: "特别", py: "tè bié", pos: "副/形", en: "especially; special", th: "เป็นพิเศษ, พิเศษ" },
            { ch: "疼", py: "téng", pos: "形", en: "pain; hurt", th: "เจ็บ, ปวด" },
            { ch: "提高", py: "tí gāo", pos: "动", en: "raise; improve", th: "ยกระดับ, พัฒนา" },
            { ch: "体育", py: "tǐ yù", pos: "名", en: "physical education; sports", th: "พลศึกษา, กีฬา" },
            { ch: "甜", py: "tián", pos: "形", en: "sweet", th: "หวาน" },
            { ch: "条", py: "tiáo", pos: "量", en: "[measure word for long things]", th: "เส้น, ตัว (ลักษณะนาม)" },
            { ch: "同事", py: "tóng shì", pos: "名", en: "colleague", th: "เพื่อนร่วมงาน" },
            { ch: "同意", py: "tóng yì", pos: "动", en: "to agree", th: "เห็นด้วย" },
            { ch: "头发", py: "tóu fa", pos: "名", en: "hair", th: "เส้นผม" },
            { ch: "突然", py: "tū rán", pos: "形/副", en: "suddenly; unexpected", th: "ทันทีทันใด, กะทันหัน" },
            { ch: "图书馆", py: "tú shū guǎn", pos: "名", en: "library", th: "ห้องสมุด" },
            { ch: "腿", py: "tuǐ", pos: "名", en: "leg", th: "ขา" },
            { ch: "完成", py: "wán chéng", pos: "动", en: "complete; accomplish", th: "ทำเสร็จ" },
            { ch: "碗", py: "wǎn", pos: "名/量", en: "a bowl of", th: "ชาม, ถ้วย" },
            { ch: "万", py: "wàn", pos: "数", en: "ten thousand", th: "หมื่น (10,000)" },
            { ch: "忘记", py: "wàng jì", pos: "动", en: "forget", th: "ลืม" },
            { ch: "位", py: "wèi", pos: "量", en: "position; polite measure for person", th: "ท่าน (ลักษณะนามสุภาพ)" },
            { ch: "为", py: "wèi", pos: "介", en: "for (someone/something)", th: "เพื่อ, สำหรับ" },
            { ch: "为了", py: "wèi le", pos: "介", en: "in order to; for the sake of", th: "เพื่อที่จะ" },
            { ch: "文化", py: "wén huà", pos: "名", en: "culture", th: "วัฒนธรรม" },
            { ch: "西", py: "xī", pos: "名", en: "west", th: "ทิศตะวันตก" },
            { ch: "习惯", py: "xí guàn", pos: "动/名", en: "be used to; habit", th: "ชิน, ความเคยชิน" },
            { ch: "洗手间", py: "xǐ shǒu jiān", pos: "名", en: "toilets; washroom", th: "ห้องน้ำ" },
            { ch: "洗澡", py: "xǐ zǎo", pos: "动", en: "have a shower/bath", th: "อาบน้ำ" },
            { ch: "夏", py: "xià", pos: "名", en: "summer", th: "ฤดูร้อน" },
            { ch: "先", py: "xiān", pos: "副", en: "first; in advance", th: "ก่อน" },
            { ch: "香蕉", py: "xiāng jiāo", pos: "名", en: "banana", th: "กล้วย" },
            { ch: "相信", py: "xiāng xìn", pos: "动", en: "believe; trust", th: "เชื่อ, เชื่อถือ" },
            { ch: "像", py: "xiàng", pos: "动/介", en: "resemble; like", th: "เหมือน, ราวกับ" },
            { ch: "向", py: "xiàng", pos: "介", en: "towards; facing", th: "ไปยัง, มุ่งสู่" },
            { ch: "小心", py: "xiǎo xīn", pos: "形/动", en: "take care; careful", th: "ระวัง" },
            { ch: "校长", py: "xiào zhǎng", pos: "名", en: "headteacher; principal", th: "ครูใหญ่, ผู้อำนวยการ" },
            { ch: "新闻", py: "xīn wén", pos: "名", en: "news", th: "ข่าว" },
            { ch: "新鲜", py: "xīn xiān", pos: "形", en: "fresh", th: "สด, สดชื่น" },
            { ch: "信用卡", py: "xìn yòng kǎ", pos: "名", en: "credit card", th: "บัตรเครดิต" },
            { ch: "行李箱", py: "xíng li xiāng", pos: "名", en: "trunk; luggage box", th: "กระเป๋าเดินทาง" },
            { ch: "熊猫", py: "xióng māo", pos: "名", en: "panda", th: "หมีแพนด้า" },
            { ch: "需要", py: "xū yào", pos: "动", en: "need; require", th: "ต้องการ, จำเป็นต้อง" },
            { ch: "选择", py: "xuǎn zé", pos: "动/名", en: "choose; choice", th: "เลือก, ตัวเลือก" },
            { ch: "越", py: "yuè", pos: "副", en: "the more...", th: "ยิ่ง... (越...越...)" },
            { ch: "要求", py: "yāo qiú", pos: "动/名", en: "requirement; demand", th: "ข้อเรียกร้อง, ร้องขอ" },
            { ch: "爷爷", py: "yé ye", pos: "名", en: "grandfather (paternal)", th: "ปู่" },
            { ch: "一般", py: "yī bān", pos: "形/副", en: "ordinary; generally", th: "ปกติ, ทั่วไป" },
            { ch: "一边", py: "yī biān", pos: "副", en: "simultaneously (一边...一边...)", th: "ไปพลาง...ไปพลาง..." },
            { ch: "一定", py: "yī dìng", pos: "副/形", en: "definitely; certain", th: "แน่นอน" },
            { ch: "一共", py: "yī gòng", pos: "副", en: "altogether; in total", th: "รวมทั้งสิ้น" },
            { ch: "一会儿", py: "yī huì er", pos: "名", en: "a short while", th: "สักครู่" },
            { ch: "一样", py: "yī yàng", pos: "形", en: "same; identical", th: "เหมือนกัน" },
            { ch: "一直", py: "yī zhí", pos: "副", en: "straight on; continuously", th: "ตรงไป, ตลอด" },
            { ch: "以前", py: "yǐ qián", pos: "名", en: "before; in the past", th: "เมื่อก่อน, ก่อนหน้า" },
            { ch: "音乐", py: "yīn yuè", pos: "名", en: "music", th: "ดนตรี" },
            { ch: "银行", py: "yín háng", pos: "名", en: "bank", th: "ธนาคาร" },
            { ch: "饮料", py: "yǐn liào", pos: "名", en: "beverage; drink", th: "เครื่องดื่ม" },
            { ch: "应该", py: "yīng gāi", pos: "动", en: "should; ought to", th: "ควรจะ" },
            { ch: "影响", py: "yǐng xiǎng", pos: "动/名", en: "influence; affect", th: "ผลกระทบ, ส่งผลกระทบ" },
            { ch: "用", py: "yòng", pos: "动", en: "to use", th: "ใช้" },
            { ch: "游戏", py: "yóu xì", pos: "名", en: "game", th: "เกม" },
            { ch: "有名", py: "yǒu míng", pos: "形", en: "famous", th: "มีชื่อเสียง" },
            { ch: "又", py: "yòu", pos: "副", en: "again (in the past)", th: "อีกแล้ว" },
            { ch: "遇到", py: "yù dào", pos: "动", en: "encounter; meet", th: "เจอ, พบเจอ" },
            { ch: "元", py: "yuán", pos: "量", en: "yuan (Chinese currency unit)", th: "หยวน (หน่วยเงิน)" },
            { ch: "愿意", py: "yuàn yì", pos: "动", en: "willing to", th: "สมัครใจ, ยินดี" },
            { ch: "月亮", py: "yuè liang", pos: "名", en: "moon", th: "พระจันทร์" },
            { ch: "站", py: "zhàn", pos: "动/名", en: "stand; station/stop", th: "ยืน; สถานี/ป้าย" },
            { ch: "张", py: "zhāng", pos: "量", en: "[measure word for flat objects]", th: "แผ่น, ใบ (ลักษณะนาม)" },
            { ch: "长", py: "zhǎng", pos: "动", en: "grow; develop", th: "เติบโต, ยาวขึ้น" },
            { ch: "着急", py: "zháo jí", pos: "形", en: "anxious; worried", th: "รีบร้อน, กังวลใจ" },
            { ch: "照顾", py: "zhào gu", pos: "动", en: "look after; take care", th: "ดูแล" },
            { ch: "照片", py: "zhào piàn", pos: "名", en: "photograph; photo", th: "รูปถ่าย" },
            { ch: "照相机", py: "zhào xiàng jī", pos: "名", en: "camera", th: "กล้องถ่ายรูป" },
            { ch: "只", py: "zhǐ", pos: "副", en: "only; merely", th: "เพียงแค่" },
            { ch: "只有……才……", py: "zhǐ yǒu ... cái ...", pos: "关联", en: "only if ... then ...", th: "มีเพียง...จึงจะ..." },
            { ch: "中间", py: "zhōng jiān", pos: "名", en: "middle; center", th: "ตรงกลาง" },
            { ch: "中文", py: "zhōng wén", pos: "名", en: "Chinese (written)", th: "ภาษาจีน" },
            { ch: "终于", py: "zhōng yú", pos: "副", en: "at last; finally", th: "ในที่สุด" },
            { ch: "种", py: "zhǒng", pos: "量", en: "kind; type; species", th: "ชนิด, ประเภท" },
            { ch: "重要", py: "zhòng yào", pos: "形", en: "important", th: "สำคัญ" },
            { ch: "周末", py: "zhōu mò", pos: "名", en: "weekend", th: "สุดสัปดาห์" },
            { ch: "主要", py: "zhǔ yào", pos: "形", en: "main; primary", th: "หลัก, สำคัญ" },
            { ch: "注意", py: "zhù yì", pos: "动", en: "pay attention to", th: "ระวัง, ใส่ใจ" },
            { ch: "自己", py: "zì jǐ", pos: "代", en: "oneself; self", th: "ตัวเอง" },
            { ch: "自行车", py: "zì xíng chē", pos: "名", en: "bicycle; bike", th: "รถจักรยาน" },
            { ch: "总是", py: "zǒng shì", pos: "副", en: "always", th: "มักจะ...เสมอ" },
            { ch: "嘴", py: "zuǐ", pos: "名", en: "mouth", th: "ปาก" },
            { ch: "最后", py: "zuì hòu", pos: "名", en: "lastly; final", th: "สุดท้าย" },
            { ch: "最近", py: "zuì jìn", pos: "名", en: "recently; lately", th: "ช่วงนี้, หมู่นี้" },
            { ch: "作业", py: "zuò yè", pos: "名", en: "homework", th: "การบ้าน" }
        ];

        // STATE MANAGERS
        let activeDeck = [];
        let masteredSet = new Set(JSON.parse(localStorage.getItem('hsk23_mastered_words') || '[]'));
        let currentIndex = 0;
        let currentFilter = 'all';
        let isCardFlipped = false;
        let viewMode = 'single';

        // INITIALIZATION
        window.onload = function() {
            filterDeck();
            setupKeyboardListeners();
        };

        // FILTER DECK
        function filterDeck() {
            activeDeck = fullVocabData.filter(item => {
                const isMastered = masteredSet.has(item.ch);
                if (isMastered) return false;

                if (currentFilter === 'all') return true;
                if (currentFilter === '名') return item.pos.includes('名');
                if (currentFilter === '动') return item.pos.includes('动');
                if (currentFilter === '形') return item.pos.includes('形');
                if (currentFilter === '副') return item.pos.includes('副') || item.pos.includes('介');
                if (currentFilter === '量') return item.pos.includes('量') || item.pos.includes('数');
                if (currentFilter === '其他') return item.pos.includes('代') || item.pos.includes('连') || item.pos.includes('关联') || item.pos.includes('助');
                return true;
            });

            currentIndex = 0;
            isCardFlipped = false;
            updateUI();
        }

        function filterCategory(cat) {
            currentFilter = cat;
            document.querySelectorAll('.cat-btn').forEach(btn => {
                if (btn.dataset.cat === cat) {
                    btn.className = "cat-btn px-3 py-1 rounded-lg font-medium bg-teal-700 text-white shadow-sm";
                } else {
                    btn.className = "cat-btn px-3 py-1 rounded-lg font-medium bg-white text-slate-700 hover:bg-indigo-100 border border-slate-200";
                }
            });
            filterDeck();
        }

        function shuffleDeck() {
            for (let i = activeDeck.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [activeDeck[i], activeDeck[j]] = [activeDeck[j], activeDeck[i]];
            }
            currentIndex = 0;
            isCardFlipped = false;
            updateUI();
        }

        // UPDATE UI DEPENDING ON MODE
        function updateUI() {
            // Header Stats
            document.getElementById('header-mastered-count').innerText = masteredSet.size;

            // Progress Bar Calculation
            const totalCount = fullVocabData.length;
            const masteredCount = masteredSet.size;
            const pct = Math.round((masteredCount / totalCount) * 100);
            document.getElementById('progress-bar').style.width = pct + '%';
            document.getElementById('progress-percentage-text').innerText = `${pct}% 已掌握`;

            document.getElementById('deck-status-text').innerText = `待学习词汇: ${activeDeck.length}`;

            if (viewMode === 'single') {
                renderSingleCard();
            } else {
                renderGridOverview();
            }
        }

        function renderSingleCard() {
            const inner = document.getElementById('active-card-inner');
            inner.classList.remove('rotate-y-180');
            isCardFlipped = false;

            if (activeDeck.length === 0) {
                document.getElementById('card-front-chinese').innerText = "🎉 复习完成！";
                document.getElementById('card-front-pos').innerText = "提示";
                document.getElementById('card-counter-indicator').innerText = "0 / 0";
                return;
            }

            const card = activeDeck[currentIndex];
            
            // Front Card
            document.getElementById('card-front-chinese').innerText = card.ch;
            document.getElementById('card-front-pos').innerText = card.pos;
            document.getElementById('card-counter-indicator').innerText = `${currentIndex + 1} / ${activeDeck.length}`;

            // Back Card
            document.getElementById('card-back-chinese').innerText = card.ch;
            document.getElementById('card-back-pinyin').innerText = card.py;
            document.getElementById('card-back-pos').innerText = card.pos;
            document.getElementById('card-back-thai').innerText = card.th;
            document.getElementById('card-back-english').innerText = card.en;
        }

        function renderGridOverview() {
            const wrapper = document.getElementById('grid-cards-wrapper');
            wrapper.innerHTML = '';
            document.getElementById('grid-count-indicator').innerText = `共 ${activeDeck.length} 个未掌握词汇`;

            activeDeck.forEach((card, idx) => {
                const el = document.createElement('div');
                el.className = "bg-white p-3.5 rounded-2xl border border-slate-200/80 shadow-sm hover:shadow-md transition cursor-pointer flex flex-col justify-between items-center text-center group";
                el.onclick = () => {
                    currentIndex = idx;
                    setViewMode('single');
                };

                el.innerHTML = `
                    <div class="w-full flex justify-between items-center text-[10px] text-slate-400">
                        <span class="bg-indigo-100 text-indigo-900 px-1.5 py-0.5 rounded font-mono font-bold">${card.pos}</span>
                        <button onclick="event.stopPropagation(); markSpecificMastered('${card.ch}')" class="hover:text-emerald-600 p-1" title="标记已掌握">
                            <i class="fa-solid fa-circle-check"></i>
                        </button>
                    </div>
                    <div class="my-2">
                        <ruby class="text-2xl font-bold font-zh text-slate-800">
                            <rb>${card.ch}</rb>
                            <rt class="text-xs font-py text-sky-600 font-semibold">${card.py}</rt>
                        </ruby>
                    </div>
                    <p class="text-xs font-th text-teal-950 font-medium truncate w-full">${card.th}</p>
                `;
                wrapper.appendChild(el);
            });
        }

        // CONTROLS & FLIP
        function flipCurrentCard() {
            if (activeDeck.length === 0) return;
            const inner = document.getElementById('active-card-inner');
            isCardFlipped = !isCardFlipped;
            if (isCardFlipped) {
                inner.classList.add('rotate-y-180');
            } else {
                inner.classList.remove('rotate-y-180');
            }
        }

        function nextCard() {
            if (activeDeck.length === 0) return;
            currentIndex = (currentIndex + 1) % activeDeck.length;
            renderSingleCard();
        }

        function prevCard() {
            if (activeDeck.length === 0) return;
            currentIndex = (currentIndex - 1 + activeDeck.length) % activeDeck.length;
            renderSingleCard();
        }

        function markCurrentMastered() {
            if (activeDeck.length === 0) return;
            const currentWord = activeDeck[currentIndex].ch;
            markSpecificMastered(currentWord);
        }

        function markSpecificMastered(word) {
            masteredSet.add(word);
            localStorage.setItem('hsk23_mastered_words', JSON.stringify([...masteredSet]));

            // Remove from active deck
            activeDeck = activeDeck.filter(item => item.ch !== word);
            if (currentIndex >= activeDeck.length) {
                currentIndex = Math.max(0, activeDeck.length - 1);
            }
            updateUI();
        }

        function resetAllMastered() {
            if (confirm("确定要重置所有已掌握的词汇记录吗？")) {
                masteredSet.clear();
                localStorage.removeItem('hsk23_mastered_words');
                filterDeck();
            }
        }

        // VIEW MODE SWITCH
        function setViewMode(mode) {
            viewMode = mode;
            const btnSingle = document.getElementById('btn-view-single');
            const btnGrid = document.getElementById('btn-view-grid');
            const containerSingle = document.getElementById('view-single-container');
            const containerGrid = document.getElementById('view-grid-container');

            if (mode === 'single') {
                btnSingle.className = "px-2.5 py-1 rounded-lg bg-white text-indigo-950 font-bold shadow-sm transition flex items-center gap-1";
                btnGrid.className = "px-2.5 py-1 rounded-lg text-slate-600 hover:text-slate-900 transition flex items-center gap-1";
                containerSingle.classList.remove('hidden');
                containerGrid.classList.add('hidden');
                renderSingleCard();
            } else {
                btnGrid.className = "px-2.5 py-1 rounded-lg bg-white text-indigo-950 font-bold shadow-sm transition flex items-center gap-1";
                btnSingle.className = "px-2.5 py-1 rounded-lg text-slate-600 hover:text-slate-900 transition flex items-center gap-1";
                containerGrid.classList.remove('hidden');
                containerSingle.classList.add('hidden');
                renderGridOverview();
            }
        }

        // SPEECH SYNTHESIS
        function speakActiveWord() {
            if (activeDeck.length === 0) return;
            const text = activeDeck[currentIndex].ch;
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                const msg = new SpeechSynthesisUtterance(text);
                msg.lang = 'zh-CN';
                msg.rate = 0.85;
                window.speechSynthesis.speak(msg);
            }
        }

        // KEYBOARD LISTENERS
        function setupKeyboardListeners() {
            document.addEventListener('keydown', (e) => {
                if (viewMode !== 'single') return;

                if (e.code === 'Space') {
                    e.preventDefault();
                    flipCurrentCard();
                } else if (e.code === 'ArrowRight') {
                    e.preventDefault();
                    nextCard();
                } else if (e.code === 'ArrowLeft') {
                    e.preventDefault();
                    prevCard();
                } else if (e.code === 'KeyM') {
                    e.preventDefault();
                    markCurrentMastered();
                } else if (e.code === 'KeyS') {
                    e.preventDefault();
                    speakActiveWord();
                }
            });
        }

        // MASTERED MODAL LOGIC
        function toggleMasteredModal() {
            const modal = document.getElementById('mastered-modal');
            modal.classList.toggle('hidden');

            if (!modal.classList.contains('hidden')) {
                renderMasteredModalItems();
            }
        }

        function renderMasteredModalItems() {
            const list = document.getElementById('mastered-items-list');
            list.innerHTML = '';

            if (masteredSet.size === 0) {
                list.innerHTML = `<p class="text-center text-slate-400 py-8">暂无已掌握词汇 (ยังไม่มีรายการที่จำได้แล้ว)</p>`;
                return;
            }

            const masteredData = fullVocabData.filter(v => masteredSet.has(v.ch));
            masteredData.forEach(item => {
                const row = document.createElement('div');
                row.className = "p-3 rounded-xl bg-slate-50 border border-slate-200/80 flex items-center justify-between";
                row.innerHTML = `
                    <div class="flex items-center gap-3">
                        <span class="font-zh font-bold text-lg text-slate-800">${item.ch}</span>
                        <span class="font-py text-sky-600 text-sm font-semibold">${item.py}</span>
                        <span class="text-slate-500 font-th text-xs">${item.th}</span>
                    </div>
                    <button onclick="unmarkMastered('${item.ch}')" class="text-xs text-teal-700 hover:text-teal-900 font-semibold px-2.5 py-1 rounded bg-teal-50 border border-teal-200">
                        恢复复习
                    </button>
                `;
                list.appendChild(row);
            });
        }

        function unmarkMastered(word) {
            masteredSet.delete(word);
            localStorage.setItem('hsk23_mastered_words', JSON.stringify([...masteredSet]));
            renderMasteredModalItems();
            filterDeck();
        }
    </script>
</body>
</html>
