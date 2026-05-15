<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>삼성SDI 안전 교육 및 평가</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-app.js";
        import { getFirestore, collection, addDoc, onSnapshot, query, orderBy, getDocs, where, setDoc, doc, getDoc } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-firestore.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-auth.js";

        const firebaseConfig = JSON.parse(__firebase_config);
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'sdi-safety-ulsan';

        window.db = db;
        window.appId = appId;
        window.auth = auth;
        window.firestore = { doc, getDoc, setDoc, collection, query, onSnapshot, getDocs, where, addDoc };

        window.currentUser = null;
        const initAuth = async () => {
            try {
                let user;
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    const result = await signInWithCustomToken(auth, __initial_auth_token);
                    user = result.user;
                } else {
                    const result = await signInAnonymously(auth);
                    user = result.user;
                }
                window.currentUser = user;
                loadQuizData(); // 초기 퀴즈 데이터 로드
            } catch (e) {
                console.error("Auth error:", e);
            }
        };

        onAuthStateChanged(auth, (user) => {
            window.currentUser = user;
        });

        initAuth();
    </script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;700;900&display=swap');
        body { font-family: 'Noto Sans KR', sans-serif; background-color: #f8fafc; color: #1e293b; -webkit-tap-highlight-color: transparent; overflow-x: hidden; }
        .sdi-blue { color: #00377B; }
        .bg-sdi-blue { background-color: #00377B; }
        .card { background: white; border-radius: 20px; box-shadow: 0 4px 25px rgba(0, 55, 123, 0.05); }
        .hidden { display: none !important; }
        .loader { border: 3px solid #f3f3f3; border-top: 3px solid #00377B; border-radius: 50%; width: 24px; height: 24px; animation: spin 1s linear infinite; display: inline-block; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        .admin-nav-btn { padding: 0.75rem 1rem; font-weight: 700; font-size: 0.85rem; border-bottom: 3px solid transparent; color: #64748b; transition: all 0.2s; cursor: pointer; }
        .admin-nav-btn.active { color: #00377B; border-bottom-color: #00377B; background-color: #f1f5f9; }
        #admin-app:not(.hidden) { display: flex !important; flex-direction: column; }
    </style>
</head>
<body class="min-h-screen">

    <!-- [사용자 화면 영역] -->
    <div id="user-app" class="container mx-auto max-w-md p-4 min-h-screen flex flex-col justify-center">
        <header class="text-center mb-8">
            <h1 class="text-3xl font-black sdi-blue tracking-tighter">SAMSUNG SDI</h1>
            <p class="text-[10px] font-bold text-slate-400 mt-1 tracking-[0.3em] uppercase">Safety Training Center</p>
        </header>

        <section id="view-auth" class="card p-8">
            <h2 class="text-xl font-bold mb-6 text-center text-slate-700">안전 교육 평가 시스템</h2>
            <div class="space-y-4">
                <input type="text" id="input-name" placeholder="성명을 입력하세요" class="w-full bg-slate-50 border-2 border-transparent p-4 rounded-2xl focus:border-[#00377B] outline-none text-center text-lg font-medium">
                <button onclick="handleStart()" class="w-full bg-sdi-blue text-white py-4 rounded-2xl font-bold text-lg shadow-lg active:scale-95 transition-all">평가 시작하기</button>
                <div class="pt-4 flex justify-center">
                    <button onclick="showAdminLogin()" class="text-xs text-slate-300 hover:text-slate-500 underline transition-colors">관리자 모드</button>
                </div>
            </div>
        </section>

        <section id="view-quiz" class="card p-6 hidden">
            <div id="quiz-ui">
                <div class="flex justify-between items-center mb-6">
                    <span id="quiz-progress" class="bg-blue-50 text-[#00377B] px-3 py-1 rounded-full text-xs font-bold font-mono">01 / 10</span>
                    <div class="h-1.5 w-32 bg-slate-100 rounded-full overflow-hidden">
                        <div id="progress-bar" class="h-full bg-sdi-blue transition-all" style="width: 10%"></div>
                    </div>
                </div>
                <h3 id="quiz-question" class="text-lg font-bold mb-8 text-slate-800 leading-snug"></h3>
                <div id="quiz-options" class="space-y-3"></div>
            </div>
            <div id="quiz-saving" class="hidden py-20 text-center">
                <div class="loader mb-4"></div>
                <p class="font-bold text-slate-500">결과 저장 중...</p>
            </div>
        </section>

        <section id="view-result" class="card p-8 hidden text-center">
            <div id="result-icon" class="w-20 h-20 mx-auto rounded-full flex items-center justify-center mb-6 text-4xl"></div>
            <h2 class="text-2xl font-bold text-slate-800">평가 완료</h2>
            <div id="result-score" class="text-6xl font-black my-6 sdi-blue">0점</div>
            <div id="result-msg" class="p-4 rounded-2xl mb-8 font-bold text-sm"></div>
            <div id="qr-area" class="hidden bg-slate-50 p-6 rounded-3xl border-2 border-dashed border-slate-200 mb-8">
                <div id="qrcode" class="flex justify-center mb-4"></div>
                <p id="qr-info" class="text-[11px] text-slate-500 font-mono"></p>
            </div>
            <button onclick="resetToMain()" class="w-full bg-slate-900 text-white py-4 rounded-2xl font-bold">처음으로</button>
        </section>
    </div>

    <!-- [관리자 화면 영역] -->
    <div id="admin-app" class="hidden min-h-screen bg-slate-50 w-full overflow-y-auto">
        <nav class="bg-white border-b sticky top-0 z-10 w-full">
            <div class="container mx-auto px-4 flex justify-between items-center h-16">
                <div class="flex items-center gap-2">
                    <span class="font-black sdi-blue text-xl">ADMIN</span>
                </div>
                <div class="flex items-center gap-1">
                    <div onclick="setAdminTab('dash')" id="tab-dash" class="admin-nav-btn active">통계</div>
                    <div onclick="setAdminTab('records')" id="tab-records" class="admin-nav-btn">목록</div>
                    <div onclick="setAdminTab('manage')" id="tab-manage" class="admin-nav-btn">설정</div>
                    <button onclick="resetToMain()" class="ml-4 text-rose-500 text-xs font-bold px-3 py-1 bg-rose-50 rounded-lg">로그아웃</button>
                </div>
            </div>
        </nav>

        <main class="container mx-auto p-4 md:p-8 flex-grow">
            <!-- 통계 뷰 -->
            <div id="admin-view-dash" class="space-y-6">
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div class="card p-5 border-l-4 border-blue-600">
                        <p class="text-[10px] font-bold text-slate-400 uppercase">누적 응시</p>
                        <p id="stat-total" class="text-2xl font-black">0</p>
                    </div>
                    <div class="card p-5 border-l-4 border-emerald-500">
                        <p class="text-[10px] font-bold text-slate-400 uppercase">합격자</p>
                        <p id="stat-pass" class="text-2xl font-black">0</p>
                    </div>
                    <div class="card p-5 border-l-4 border-amber-400">
                        <p class="text-[10px] font-bold text-slate-400 uppercase">평균 점수</p>
                        <p id="stat-avg" class="text-2xl font-black">0</p>
                    </div>
                    <div class="card p-5 border-l-4 border-indigo-500">
                        <p class="text-[10px] font-bold text-slate-400 uppercase">합격률</p>
                        <p id="stat-rate" class="text-2xl font-black">0%</p>
                    </div>
                </div>
                <div class="card p-6">
                    <h3 class="font-bold mb-6 text-slate-800">응시 현황 요약</h3>
                    <div class="h-64 md:h-96 w-full"><canvas id="adminChart"></canvas></div>
                </div>
            </div>

            <!-- 목록 뷰 -->
            <div id="admin-view-records" class="hidden space-y-4">
                <div class="flex justify-between items-center">
                    <h3 class="font-bold text-slate-800">응시자 데이터베이스</h3>
                    <div class="flex gap-2">
                        <button onclick="syncAdminRecords()" class="bg-blue-50 text-blue-600 px-3 py-2 rounded-xl text-xs font-bold">새로고침</button>
                        <button onclick="exportExcel()" class="bg-emerald-600 text-white px-4 py-2 rounded-xl text-xs font-bold hover:bg-emerald-700">Excel 다운로드</button>
                    </div>
                </div>
                <div class="card overflow-x-auto">
                    <table class="w-full text-left min-w-[600px]">
                        <thead class="bg-slate-50 text-[10px] font-bold text-slate-400 uppercase border-b">
                            <tr>
                                <th class="p-4">응시 일시</th><th class="p-4">성명</th><th class="p-4 text-center">점수</th><th class="p-4 text-center">결과</th><th class="p-4">UID</th>
                            </tr>
                        </thead>
                        <tbody id="admin-table-body" class="divide-y text-sm text-slate-600">
                            <tr><td colspan="5" class="p-10 text-center text-slate-400">데이터를 불러오는 중입니다...</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 설정 뷰 -->
            <div id="admin-view-manage" class="hidden space-y-6">
                <!-- 문제은행 관리 -->
                <div class="card p-8">
                    <h3 class="font-bold text-lg mb-6 text-slate-800 border-b pb-4">문제은행 관리</h3>
                    <div class="space-y-6">
                        <div class="flex flex-col md:flex-row gap-4 items-center justify-between p-4 bg-blue-50 rounded-2xl">
                            <div class="text-sm">
                                <p class="font-bold text-blue-900">문제은행 양식 내려받기</p>
                                <p class="text-xs text-blue-700">엑셀 양식에 맞춰 문제를 작성한 후 업로드하세요.</p>
                            </div>
                            <button onclick="downloadQuizTemplate()" class="bg-white text-blue-600 border border-blue-200 px-4 py-2 rounded-xl text-xs font-bold shadow-sm hover:bg-blue-100 transition-all">양식 다운로드 (.xlsx)</button>
                        </div>
                        
                        <div>
                            <label class="block text-xs font-bold text-slate-400 mb-2 uppercase">엑셀 파일 업로드</label>
                            <div class="flex gap-2">
                                <input type="file" id="quiz-excel-input" accept=".xlsx, .xls" class="hidden" onchange="handleExcelUpload(this)">
                                <button onclick="document.getElementById('quiz-excel-input').click()" class="flex-grow bg-slate-900 text-white py-4 rounded-xl font-bold hover:brightness-110 active:scale-[0.98] transition-all">파일 선택 및 업로드</button>
                            </div>
                            <p class="text-[10px] text-slate-400 mt-2">* 업로드 즉시 기존 평가 문항이 대체됩니다. (최소 10문항 권장)</p>
                        </div>
                    </div>
                </div>

                <!-- 보안 설정 -->
                <div class="card p-8">
                    <h3 class="font-bold text-lg mb-6 text-slate-800 border-b pb-4">보안 설정</h3>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-400 mb-2 uppercase">비밀번호 변경</label>
                            <input type="password" id="new-pw" placeholder="새 비밀번호 입력" class="w-full bg-slate-50 p-4 rounded-xl outline-none border focus:border-blue-400">
                        </div>
                        <button onclick="changeAdminPassword()" class="w-full bg-slate-200 text-slate-800 py-4 rounded-xl font-bold hover:bg-slate-300">비밀번호 저장</button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- [관리자 로그인 모달] -->
    <div id="admin-login-modal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-md hidden flex items-center justify-center p-4 z-[100]">
        <div class="card w-full max-w-sm p-8 shadow-2xl">
            <h2 class="text-xl font-bold mb-1 text-center text-slate-800">관리자 인증</h2>
            <p class="text-xs text-slate-400 mb-6 text-center">보안 비밀번호를 입력해 주세요.</p>
            
            <div id="login-form">
                <input type="password" id="admin-pw-input" placeholder="••••" class="w-full bg-slate-100 p-4 rounded-2xl mb-4 text-center text-3xl font-mono outline-none border-2 border-transparent focus:border-blue-600 focus:bg-white transition-all">
                <div class="grid grid-cols-2 gap-2">
                    <button onclick="hideAdminLogin()" class="bg-slate-200 py-4 rounded-2xl font-bold text-slate-600 hover:bg-slate-300">취소</button>
                    <button onclick="processAdminLogin()" class="bg-sdi-blue text-white py-4 rounded-2xl font-bold hover:brightness-110 shadow-lg">인증 확인</button>
                </div>
            </div>
            
            <div id="login-loader" class="hidden text-center py-6">
                <div class="loader mb-2"></div>
                <p class="text-sm font-bold text-slate-500">인증 확인 중...</p>
            </div>
        </div>
    </div>

    <script>
        const FALLBACK_QUIZ = [
            { q: "전기화재 발생 시 가장 적합한 소화기는?", a: ["K급 소화기", "이산화탄소(CO2) 소화기", "포말 소화기", "강화액 소화기"], r: 1 },
            { q: "LOTO 시스템을 실시하는 가장 주된 목적은?", a: ["유지보수 비용 절감", "임의 가동으로 인한 협착 예방", "작업자의 이동 경로 파악", "전력 소비 효율화"], r: 1 },
            { q: "밀폐공간 출입 전 가장 먼저 측정해야 할 항목은?", a: ["조도", "소음", "산소 및 유해가스", "습도"], r: 2 },
            { q: "삼성SDI 5대 안전수칙 중 '보호구' 수칙은?", a: ["필요할 때만 착용", "규정된 보호구 철저 착용", "미착용 시 자율 작업", "작업복만 입으면 생략"], r: 1 },
            { q: "지게차 운행 시 시야가 확보되지 않는 경우 조치는?", a: ["전진 가속", "유도자 배치 및 후진 운행", "전방 주시 서행", "그대로 운행"], r: 1 },
            { q: "화학물질 취급 전 반드시 확인해야 하는 자료는?", a: ["날씨 예보", "MSDS(물질안전보건자료)", "작업 일보", "급여 명세서"], r: 1 },
            { q: "안전모의 올바른 착용 방법이 아닌 것은?", a: ["턱끈 조절", "머리 크기 조절", "라이너 사용", "더우면 턱끈 풀기"], r: 3 },
            { q: "추락 방지를 위한 '안전대' 체결 위치는?", a: ["발 아래", "허리 아래", "머리 위쪽 지지점", "아무데나"], r: 2 },
            { q: "중량물을 들어올릴 때 올바른 자세는?", a: ["허리를 굽혀서", "무릎을 굽히고 허리를 펴서", "팔 힘으로만", "반동 이용"], r: 1 },
            { q: "소화기 사용법 PASS 원칙 중 S(Sweep)의 의미는?", a: ["멈추기", "핀 당기기", "골고루 비질하기", "손잡이 쥐기"], r: 2 }
        ];

        let state = {
            name: '',
            questions: [],
            currentIndex: 0,
            answers: new Array(10).fill(null),
            allRecords: []
        };

        let adminUnsubscribe = null;
        let adminChart = null;

        // 퀴즈 데이터 로드
        async function loadQuizData() {
            try {
                if (window.firestore) {
                    const docRef = window.firestore.doc(window.db, 'artifacts', window.appId, 'public', 'settings', 'quiz_config');
                    const snap = await window.firestore.getDoc(docRef);
                    if (snap.exists() && snap.data().questions) {
                        state.questions = snap.data().questions;
                        console.log("Quiz data loaded from Firestore");
                    } else {
                        state.questions = [...FALLBACK_QUIZ];
                    }
                }
            } catch (e) {
                console.error("Quiz load error:", e);
                state.questions = [...FALLBACK_QUIZ];
            }
        }

        function showView(id) {
            ['view-auth', 'view-quiz', 'view-result'].forEach(v => {
                const el = document.getElementById(v);
                if(el) el.classList.add('hidden');
            });
            const target = document.getElementById(id);
            if(target) target.classList.remove('hidden');
        }

        function resetToMain() {
            document.getElementById('admin-app').classList.add('hidden');
            document.getElementById('admin-app').style.display = 'none';
            document.getElementById('user-app').classList.remove('hidden');
            document.getElementById('user-app').style.display = 'flex';
            document.getElementById('admin-login-modal').classList.add('hidden');
            
            if (adminUnsubscribe) { adminUnsubscribe(); adminUnsubscribe = null; }
            state.name = '';
            document.getElementById('input-name').value = '';
            showView('view-auth');
        }

        async function handleStart() {
            const name = document.getElementById('input-name').value.trim();
            if (!name) return alert("성명을 입력해 주세요.");
            state.name = name;
            
            // 실시간 문항 확보 (최신 상태)
            await loadQuizData();
            
            // 랜덤 10문항 추출 (전체 문항이 10개 미만이면 전체 사용)
            const qCount = Math.min(10, state.questions.length);
            state.quizSet = [...state.questions].sort(() => 0.5 - Math.random()).slice(0, qCount);
            
            state.currentIndex = 0;
            state.answers = new Array(qCount).fill(null);
            showView('view-quiz');
            renderQuestion();
        }

        function renderQuestion() {
            const q = state.quizSet[state.currentIndex];
            const total = state.quizSet.length;
            document.getElementById('quiz-progress').innerText = `${(state.currentIndex + 1).toString().padStart(2, '0')} / ${total.toString().padStart(2, '0')}`;
            document.getElementById('progress-bar').style.width = `${((state.currentIndex + 1) / total) * 100}%`;
            document.getElementById('quiz-question').innerText = q.q;

            const container = document.getElementById('quiz-options');
            container.innerHTML = '';
            q.a.forEach((opt, idx) => {
                const btn = document.createElement('button');
                btn.className = "w-full text-left p-4 rounded-xl flex items-center font-medium border-2 bg-white border-slate-100 hover:border-blue-500 transition-all active:scale-[0.98]";
                btn.innerHTML = `<span class="w-7 h-7 rounded-full bg-slate-100 text-slate-400 flex items-center justify-center text-xs font-bold mr-3">${idx+1}</span><span class="text-sm">${opt}</span>`;
                btn.onclick = () => {
                    state.answers[state.currentIndex] = idx;
                    if (state.currentIndex < total - 1) {
                        state.currentIndex++; renderQuestion();
                    } else {
                        finishExam();
                    }
                };
                container.appendChild(btn);
            });
        }

        async function finishExam() {
            const quizUi = document.getElementById('quiz-ui');
            const savingUi = document.getElementById('quiz-saving');
            quizUi.classList.add('hidden');
            savingUi.classList.remove('hidden');

            const total = state.quizSet.length;
            let correctCount = 0;
            state.quizSet.forEach((q, i) => { if (Number(q.r) === state.answers[i]) correctCount++; });
            
            const score = Math.round((correctCount / total) * 100);
            const passed = score >= 80;
            const uid = "SDI-" + Math.random().toString(36).substr(2, 6).toUpperCase();
            const ts = new Date().toISOString();

            try {
                if (window.firestore) {
                    const coll = window.firestore.collection(window.db, 'artifacts', window.appId, 'public', 'data', 'exam_results');
                    await window.firestore.addDoc(coll, { name: state.name, score, passed, uid, timestamp: ts });
                }
            } catch (e) { console.error(e); }

            savingUi.classList.add('hidden');
            quizUi.classList.remove('hidden');
            showView('view-result');
            
            document.getElementById('result-score').innerText = `${score}점`;
            const icon = document.getElementById('result-icon');
            const msg = document.getElementById('result-msg');
            const qrArea = document.getElementById('qr-area');

            if (passed) {
                icon.innerHTML = "🏆"; icon.className = "w-20 h-20 mx-auto rounded-full bg-emerald-100 text-emerald-600 flex items-center justify-center mb-6 text-4xl";
                msg.innerText = "안전 교육 이수 완료"; msg.className = "p-4 rounded-2xl mb-8 font-bold bg-emerald-50 text-emerald-700";
                qrArea.classList.remove('hidden');
                document.getElementById('qr-info').innerText = `${uid} | ${state.name}`;
                document.getElementById("qrcode").innerHTML = "";
                new QRCode(document.getElementById("qrcode"), { text: `PASS:${uid}:${state.name}`, width: 120, height: 120 });
            } else {
                icon.innerHTML = "⚠️"; icon.className = "w-20 h-20 mx-auto rounded-full bg-rose-100 text-rose-600 flex items-center justify-center mb-6 text-4xl";
                msg.innerText = "불합격 (80점 이상 합격)"; msg.className = "p-4 rounded-2xl mb-8 font-bold bg-rose-50 text-rose-700";
                qrArea.classList.add('hidden');
            }
        }

        // --- 문제은행 관리 (엑셀) ---
        function downloadQuizTemplate() {
            // 현재 문항 데이터를 기반으로 양식 생성
            const data = state.questions.map(q => ({
                '질문': q.q,
                '보기1': q.a[0],
                '보기2': q.a[1],
                '보기3': q.a[2],
                '보기4': q.a[3],
                '정답번호(1~4)': q.r + 1
            }));
            const worksheet = XLSX.utils.json_to_sheet(data);
            const workbook = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");
            XLSX.writeFile(workbook, "삼성SDI_안전평가_문제은행_양식.xlsx");
        }

        function handleExcelUpload(input) {
            const file = input.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = async (e) => {
                try {
                    const data = new Uint8Array(e.target.result);
                    const workbook = XLSX.read(data, { type: 'array' });
                    const sheetName = workbook.SheetNames[0];
                    const json = XLSX.utils.sheet_to_json(workbook.Sheets[sheetName]);

                    if (json.length < 1) throw new Error("데이터가 비어있습니다.");

                    // 데이터 파싱 및 검증
                    const newQuestions = json.map((row, idx) => {
                        const q = row['질문'] || row['question'];
                        const a1 = row['보기1'] || row['option1'];
                        const a2 = row['보기2'] || row['option2'];
                        const a3 = row['보기3'] || row['option3'];
                        const a4 = row['보기4'] || row['option4'];
                        const r = parseInt(row['정답번호(1~4)'] || row['answer']) - 1;

                        if (!q || !a1 || isNaN(r)) throw new Error(`${idx+1}번째 행의 데이터가 부적절합니다.`);
                        return { q, a: [a1, a2, a3, a4].filter(v => v), r };
                    });

                    // Firestore 저장
                    if (window.firestore) {
                        const docRef = window.firestore.doc(window.db, 'artifacts', window.appId, 'public', 'settings', 'quiz_config');
                        await window.firestore.setDoc(docRef, { questions: newQuestions });
                        state.questions = newQuestions;
                        alert(`성공적으로 업로드되었습니다. (총 ${newQuestions.length}문항)`);
                    }
                } catch (err) {
                    alert("업로드 실패: " + err.message);
                } finally {
                    input.value = '';
                }
            };
            reader.readAsArrayBuffer(file);
        }

        // --- 관리자 제어 공통 ---
        function showAdminLogin() {
            document.getElementById('admin-login-modal').classList.remove('hidden');
            document.getElementById('admin-pw-input').value = '';
            document.getElementById('login-form').classList.remove('hidden');
            document.getElementById('login-loader').classList.add('hidden');
            setTimeout(() => document.getElementById('admin-pw-input').focus(), 150);
        }

        function hideAdminLogin() {
            document.getElementById('admin-login-modal').classList.add('hidden');
        }

        async function processAdminLogin() {
            const input = document.getElementById('admin-pw-input');
            const pw = input.value.trim();
            if (!pw) return;

            const form = document.getElementById('login-form');
            const loader = document.getElementById('login-loader');
            form.classList.add('hidden');
            loader.classList.remove('hidden');

            try {
                let targetPw = "1234";
                if (window.firestore && window.currentUser) {
                    const authDocRef = window.firestore.doc(window.db, 'artifacts', window.appId, 'public', 'settings', 'admin_config');
                    const snap = await window.firestore.getDoc(authDocRef);
                    if (snap.exists()) targetPw = snap.data().password || "1234";
                }

                if (pw === targetPw) {
                    switchToAdminView();
                } else {
                    alert("비밀번호가 올바르지 않습니다.");
                    form.classList.remove('hidden');
                    loader.classList.add('hidden');
                    input.value = ''; input.focus();
                }
            } catch (e) {
                if (pw === "1234") switchToAdminView();
                else {
                    alert("인증 서버 통신 실패.");
                    form.classList.remove('hidden');
                    loader.classList.add('hidden');
                }
            }
        }

        function switchToAdminView() {
            document.getElementById('admin-login-modal').classList.add('hidden');
            document.getElementById('user-app').classList.add('hidden');
            document.getElementById('user-app').style.display = 'none';
            document.getElementById('admin-app').classList.remove('hidden');
            document.getElementById('admin-app').style.display = 'flex';
            setAdminTab('dash');
            setTimeout(() => syncAdminRecords(), 300);
        }

        document.getElementById('admin-pw-input').addEventListener('keydown', (e) => {
            if (e.key === 'Enter') processAdminLogin();
        });

        function setAdminTab(tab) {
            ['dash', 'records', 'manage'].forEach(t => {
                const view = document.getElementById(`admin-view-${t}`);
                const tabBtn = document.getElementById(`tab-${t}`);
                if(view) view.classList.add('hidden');
                if(tabBtn) tabBtn.classList.remove('active');
            });
            const activeView = document.getElementById(`admin-view-${tab}`);
            const activeTabBtn = document.getElementById(`tab-${tab}`);
            if(activeView) activeView.classList.remove('hidden');
            if(activeTabBtn) activeTabBtn.classList.add('active');
        }

        async function syncAdminRecords() {
            if (!window.firestore || !window.db || !window.currentUser) return;
            const coll = window.firestore.collection(window.db, 'artifacts', window.appId, 'public', 'data', 'exam_results');
            const q = window.firestore.query(coll);
            
            if (adminUnsubscribe) adminUnsubscribe();
            
            const body = document.getElementById('admin-table-body');
            body.innerHTML = '<tr><td colspan="5" class="p-10 text-center"><div class="loader"></div></td></tr>';

            adminUnsubscribe = window.firestore.onSnapshot(q, (snap) => {
                const results = [];
                snap.forEach(d => results.push(d.data()));
                state.allRecords = results.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
                updateAdminDashboard();
                updateAdminTable();
            }, (err) => {
                body.innerHTML = `<tr><td colspan="5" class="p-10 text-center text-rose-500 font-bold">오류: ${err.message}</td></tr>`;
            });
        }

        function updateAdminDashboard() {
            const recs = state.allRecords;
            const total = recs.length;
            const passCount = recs.filter(r => r.passed).length;
            const avgScore = total > 0 ? Math.round(recs.reduce((acc, curr) => acc + (curr.score || 0), 0) / total) : 0;
            const passRate = total > 0 ? Math.round((passCount / total) * 100) : 0;

            document.getElementById('stat-total').innerText = total;
            document.getElementById('stat-pass').innerText = passCount;
            document.getElementById('stat-avg').innerText = avgScore;
            document.getElementById('stat-rate').innerText = passRate + "%";

            const ctx = document.getElementById('adminChart');
            if (!ctx) return;
            if (adminChart) adminChart.destroy();
            adminChart = new Chart(ctx.getContext('2d'), {
                type: 'bar',
                data: {
                    labels: ['합격', '불합격'],
                    datasets: [{
                        label: '인원 수',
                        data: [passCount, total - passCount],
                        backgroundColor: ['#00377B', '#CBD5E1'],
                        borderRadius: 10
                    }]
                },
                options: { 
                    responsive: true, maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: { y: { beginAtZero: true, grid: { display: false } }, x: { grid: { display: false } } }
                }
            });
        }

        function updateAdminTable() {
            const body = document.getElementById('admin-table-body');
            if (state.allRecords.length === 0) {
                body.innerHTML = '<tr><td colspan="5" class="p-10 text-center text-slate-400">데이터가 없습니다.</td></tr>';
                return;
            }
            body.innerHTML = '';
            state.allRecords.forEach(r => {
                const row = document.createElement('tr');
                row.className = "hover:bg-slate-50 transition-colors border-b";
                row.innerHTML = `
                    <td class="p-4 text-[11px] font-mono text-slate-500">${new Date(r.timestamp).toLocaleString()}</td>
                    <td class="p-4 font-bold text-slate-800">${r.name || '무명'}</td>
                    <td class="p-4 text-center font-black text-blue-700">${r.score || 0}점</td>
                    <td class="p-4 text-center">
                        <span class="px-3 py-1 rounded-full text-[10px] font-black ${r.passed?'bg-blue-100 text-blue-700':'bg-slate-100 text-slate-500'}">
                            ${r.passed?'합격':'불합격'}
                        </span>
                    </td>
                    <td class="p-4 text-[10px] text-slate-300 font-mono">${r.uid || '-'}</td>
                `;
                body.appendChild(row);
            });
        }

        function exportExcel() {
            if (state.allRecords.length === 0) return alert("데이터가 없습니다.");
            const data = state.allRecords.map(r => ({
                '응시일시': new Date(r.timestamp).toLocaleString(),
                '성명': r.name,
                '점수': r.score,
                '결과': r.passed ? '합격' : '불합격',
                '고유번호': r.uid
            }));
            const worksheet = XLSX.utils.json_to_sheet(data);
            const workbook = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(workbook, worksheet, "응시결과");
            XLSX.writeFile(workbook, `삼성SDI_안전평가_결과.xlsx`);
        }

        async function changeAdminPassword() {
            const newPw = document.getElementById('new-pw').value.trim();
            if (newPw.length < 4) return alert("4자 이상 입력하세요.");
            try {
                const docRef = window.firestore.doc(window.db, 'artifacts', window.appId, 'public', 'settings', 'admin_config');
                await window.firestore.setDoc(docRef, { password: newPw });
                alert("비밀번호가 변경되었습니다.");
                document.getElementById('new-pw').value = '';
            } catch (e) { alert("오류: " + e.message); }
        }
    </script>
</body>
</html>
