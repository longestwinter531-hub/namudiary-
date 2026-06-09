<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🌸 감정나무 다이어리 & 공유 게시판</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family:'Arial', sans-serif;
    background: linear-gradient(rgba(255, 247, 251, 0.6), rgba(248, 244, 255, 0.6)), 
                url('https://images.unsplash.com/photo-1522383225653-ed111181a951?auto=format&fit=crop&w=1920&q=80');
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
    min-height:100vh;
    color:#555;
}

.hidden{
    display:none !important;
}

.screen{
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
    padding: 20px;
}

.card{
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(5px);
    padding:30px;
    border-radius:25px;
    box-shadow:0 8px 32px rgba(0,0,0,0.15);
    width:90%;
    max-width:600px;
    text-align: center;
    position: relative;
}

h1, h2, h3{
    color: #4a4a4a;
}

.input-group {
    margin-bottom: 15px;
    text-align: left;
    width: 100%;
}

.input-group label {
    display: block;
    margin-bottom: 5px;
    font-size: 14px;
    font-weight: bold;
    color: #777;
}

input[type="text"], input[type="password"] {
    width: 100%;
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 12px;
    font-size: 16px;
    outline: none;
}

button{
    border:none;
    border-radius:15px;
    padding:12px 22px;
    cursor:pointer;
    font-size:16px;
    background:#ffd6e7;
    transition:0.2s;
    font-weight: bold;
    color: #555;
}

button:hover{
    transform:scale(1.05);
}

#tree{
    font-size:140px;
    margin-top:10px;
    animation:float 3s infinite ease-in-out;
}

@keyframes float{
    0%{transform:translateY(0);}
    50%{transform:translateY(-10px);}
    100%{transform:translateY(0);}
}

.mood-selection-box {
    margin-top: 15px;
    background: rgba(255, 255, 255, 0.8);
    padding: 15px;
    border-radius: 20px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}

.mood-title {
    font-size: 15px;
    font-weight: bold;
    color: #666;
    margin-bottom: 8px;
}

.mood-options {
    display: flex;
    justify-content: center;
    gap: 15px;
}

.mood-btn {
    font-size: 32px;
    cursor: pointer;
    transition: transform 0.2s;
    user-select: none;
    opacity: 0.4;
}

.mood-btn:hover {
    transform: scale(1.2);
    opacity: 0.8;
}

.mood-btn.selected {
    transform: scale(1.3);
    opacity: 1;
    filter: drop-shadow(0 4px 6px rgba(0,0,0,0.2));
}

#daysText{
    margin-top:15px;
    display: inline-block;
    background: rgba(255, 255, 255, 0.8);
    padding: 5px 15px;
    border-radius: 20px;
}

.diaryBtn{
    margin-top:20px;
    width:260px;
    height:55px;
    font-size:18px;
    background:#ffe5b4;
}

/* 상단 아이콘 버튼들 */
.board-icon-btn {
    position: absolute;
    top: 20px;
    left: 20px;
    font-size: 28px;
    cursor: pointer;
    background: none;
    border: none;
    padding: 5px;
    transition: transform 0.2s;
}
.board-icon-btn:hover { transform: scale(1.1); }

.history-icon-btn {
    position: absolute;
    top: 20px;
    right: 20px;
    font-size: 28px;
    cursor: pointer;
    background: none;
    border: none;
    padding: 5px;
    transition: transform 0.2s;
}
.history-icon-btn:hover { transform: scale(1.1); }

.logoutBtn {
    margin-top: 15px;
    background: #f1f1f1;
    font-size: 14px;
    padding: 8px 15px;
}

/* 출석판 */
#attendancePanel{
    background: rgba(255, 255, 255, 0.95);
    border-radius: 20px;
    padding: 15px;
    box-shadow: 0 8px 24px rgba(0,0,0,0.15);
    width: 90%;
    max-width: 450px;
    margin-bottom: 15px;
}

.attendance-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
}

.calendar-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 8px;
    text-align: center;
}

.day-label {
    font-size: 11px;
    font-weight: bold;
    color: #888;
    padding-bottom: 5px;
    border-bottom: 1px solid #eee;
}

.stamp-slot {
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #fafafa;
    border-radius: 10px;
    font-size: 18px;
}
.stamp-slot.active {
    background: #fff0f5;
    border: 1px solid #ffd6e7;
}

/* 게시판 스타일 */
.board-card {
    max-width: 650px !important;
    text-align: left;
}

.post-list {
    max-height: 400px;
    overflow-y: auto;
    margin: 20px 0;
    padding-right: 5px;
}

.post-item {
    background: white;
    border: 1px solid #eee;
    border-radius: 15px;
    padding: 15px;
    margin-bottom: 15px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.02);
    cursor: pointer;
    transition: 0.2s;
}
.post-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
}

.post-meta {
    font-size: 13px;
    color: #ff8fa3;
    font-weight: bold;
    margin-bottom: 5px;
    display: flex;
    justify-content: space-between;
}

.post-q {
    font-size: 14px;
    font-weight: bold;
    background: #fffcf0;
    padding: 6px 10px;
    border-radius: 8px;
    margin-bottom: 8px;
    color: #666;
}

.post-content {
    font-size: 15px;
    line-height: 1.4;
    color: #444;
}

/* 댓글 영역 */
.comment-section {
    margin-top: 15px;
    border-top: 1px solid #eee;
    padding-top: 10px;
}
.comment-item {
    font-size: 13px;
    padding: 5px 0;
    border-bottom: 1px dashed #f5f5f5;
}
.comment-user {
    font-weight: bold;
    color: #555;
    margin-right: 5px;
}
.comment-input-box {
    display: flex;
    gap: 5px;
    margin-top: 10px;
}
.comment-input {
    flex: 1;
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 10px;
    font-size: 13px;
}
.comment-btn {
    padding: 5px 12px;
    font-size: 13px;
    background: #ffe5b4;
    border-radius: 10px;
}

/* 기분 달력 */
.monthly-calendar {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 6px;
    margin: 15px 0;
}
.cal-header { font-size: 12px; font-weight: bold; color: #999; padding: 5px 0; text-align: center;}
.cal-day {
    height: 45px; background: #fdfdfd; border: 1px solid #f0f0f0; border-radius: 8px;
    display: flex; flex-direction: column; justify-content: space-between; align-items: center;
    padding: 4px; font-size: 10px; color: #ccc;
}
.cal-day.has-data { color: #555; background: #fffdf9; }
.cal-mood { font-size: 18px; }

.analysis-box { background: #eef7ff; padding: 15px; border-radius: 15px; margin-top: 15px; font-size: 14px; line-height: 1.5;}
.analysis-title { font-weight: bold; color: #3182ce; margin-bottom: 5px; }

textarea{ width:100%; height:180px; padding:12px; border-radius:15px; border:1px solid #ddd; resize:none; font-size:15px; margin-top: 10px;}
.questionBox{ background:#fff6da; padding:15px; border-radius:15px; margin-bottom:15px; text-align: left; font-weight: bold;}
.saveBtn{ background:#d8f3dc; margin-right: 5px; }
.homeBtn{ background:#e5dbff; }
.auth-toggle { margin-top: 15px; font-size: 14px; color: #888; }
.auth-toggle span { color: #ff8fa3; text-decoration: underline; cursor: pointer; }
#welcomeText { font-size: 16px; color: #666; margin-bottom: 5px; }
</style>
</head>

<body>

<div id="authScreen" class="screen">
    <div class="card">
        <h1 id="authTitle">🌸 로그인 🌸</h1>
        <p style="text-align:center;" id="authSub">감정나무를 키우기 위해 로그인해주세요.</p>
        <br>
        <div class="input-group">
            <label for="username">아이디</label>
            <input type="text" id="username" placeholder="아이디를 입력하세요">
        </div>
        <div class="input-group">
            <label for="password">비밀번호</label>
            <input type="password" id="password" placeholder="비밀번호를 입력하세요">
        </div>
        <br>
        <button id="authBtn" onclick="handleAuth()">로그인</button>
        <div class="auth-toggle" id="authToggleText">
            계정이 없으신가요? <span onclick="toggleAuthMode()">회원가입하기</span>
        </div>
    </div>
</div>

<div id="mainScreen" class="screen hidden">
    <div id="attendancePanel">
        <div class="attendance-header">
            <h3>이번 주 출석 현황</h3>
            <span style="cursor:pointer;" onclick="closeAttendance()">✖</span>
        </div>
        <div class="calendar-grid">
            <div class="day-label">MON</div><div class="day-label">TUE</div><div class="day-label">WED</div>
            <div class="day-label">THU</div><div class="day-label">FRI</div><div class="day-label">SAT</div><div class="day-label">SUN</div>
            <div class="stamp-slot" id="slot-1"></div><div class="stamp-slot" id="slot-2"></div><div class="stamp-slot" id="slot-3"></div>
            <div class="stamp-slot" id="slot-4"></div><div class="stamp-slot" id="slot-5"></div><div class="stamp-slot" id="slot-6"></div>
            <div class="stamp-slot" id="slot-0"></div>
        </div>
    </div>

    <div class="card">
        <button class="board-icon-btn" onclick="openBoard()" title="공유 게시판 가기">📣</button>
        <button class="history-icon-btn" onclick="openHistory()" title="한 달 기분 보기">📒</button>

        <div id="welcomeText"></div>
        <div id="tree">🌱</div>
        
        <div class="mood-selection-box">
            <div class="mood-title">오늘 나의 기분은?</div>
            <div class="mood-options">
                <span class="mood-btn" onclick="selectMood('🤬', this)">🤬</span>
                <span class="mood-btn" onclick="selectMood('🥺', this)">🥺</span>
                <span class="mood-btn" onclick="selectMood('😰', this)">😰</span>
                <span class="mood-btn" onclick="selectMood('😭', this)">😭</span>
                <span class="mood-btn" onclick="selectMood('😊', this)">😊</span>
                <span class="mood-btn" onclick="selectMood('🤪', this)">🤪</span>
            </div>
        </div>

        <h2 id="daysText">총 출석 0일째</h2><br>
        <button class="diaryBtn" onclick="openDiary()">📔 오늘의 일기 작성</button><br>
        <button class="logoutBtn" onclick="logout()">로그아웃</button>
    </div>
</div>

<div id="diaryScreen" class="screen hidden">
    <div class="card">
        <h2>오늘의 질문</h2><br>
        <div id="question" class="questionBox"></div>
        <textarea id="diaryText" placeholder="오늘의 마음을 적어보세요..."></textarea><br><br>
        <button class="saveBtn" onclick="saveDiary()">저장 및 게시판 공유</button>
        <button class="homeBtn" onclick="goHome()">돌아가기</button>
    </div>
</div>

<div id="historyScreen" class="screen hidden">
    <div class="card history-card">
        <h2 id="calendarTitle">기분 달력</h2>
        <p style="font-size:13px; color:#999; margin-top:5px; text-align:center;">한 눈에 모아보는 나의 마음 지도</p>
        <div class="monthly-calendar" id="monthlyCalendarGrid">
            <div class="cal-header">일</div><div class="cal-header">월</div><div class="cal-header">화</div>
            <div class="cal-header">수</div><div class="cal-header">목</div><div class="cal-header">금</div><div class="cal-header">토</div>
        </div>
        <div class="analysis-box">
            <div class="analysis-title">✨ 감정 정원사의 마음 분석</div>
            <div id="analysisMent">기록된 기분이 아직 없습니다. 오늘 첫 기분을 심어보세요!</div>
        </div><br>
        <button class="homeBtn" onclick="closeHistory()">돌아가기</button>
    </div>
</div>

<div id="boardScreen" class="screen hidden">
    <div class="card board-card">
        <h2 style="text-align:center;">📣 우리들의 광장 (공유 게시판)</h2>
        <p style="font-size:13px; color:#999; margin-top:5px; text-align:center;">친구들이 답변한 질문들을 모아보고 댓글을 남겨보세요!</p>
        
        <div class="post-list" id="postListContainer">
            </div>
        
        <div style="text-align:center;">
            <button class="homeBtn" onclick="closeBoard()">메인 정원으로 돌아가기</button>
        </div>
    </div>
</div>

<script>
let currentUser = null;
let isSignUpMode = false;
let selectedMood = ""; 
let currentQuestion = "";

const questions = [
    "오늘 당신을 미소 짓게 만든 작은 일은 무엇인가요?",
    "지금 마음의 날씨를 표현한다면 어떤가요?",
    "오늘 나를 가장 힘들게 했던 생각이나 감정이 있나요?",
    "오늘 누군가에게 들었던 말 중 가장 기억에 남는 것은?",
    "내일의 나에게 한 마디 응원을 건넨다면?"
];

const moodMentions = {
    '😊': "이번 달은 당신의 마음에 따스한 햇살이 자주 내리쬐었네요! 긍정적이고 밝은 에너지가 가득합니다.",
    '🤬': "최근 마음에 화가 많이 쌓이셨군요. 스트레스를 주는 요인이 무엇인지 돌아보고 휴식을 가져보세요.",
    '🥺': "마음이 여려지고 위로가 필요한 날이 많았습니다. 누군가에게 따뜻한 위로를 구해보세요.",
    '😰': "불안과 걱정의 안개가 마음을 조금 흐리게 만들었네요. 숨을 깊게 들이마셔 보세요.",
    '😭': "눈물이 나거나 슬픈 감정이 마음 가득 고였던 달이군요. 슬픔을 온전히 털어내 보세요.",
    '🤪': "유쾌하고 엉뚱하며 활기찬 감정이 가득한 달이었습니다! 아주 멋진 에너지입니다."
};

function toggleAuthMode() {
    isSignUpMode = !isSignUpMode;
    const title = document.getElementById("authTitle");
    const sub = document.getElementById("authSub");
    const btn = document.getElementById("authBtn");
    const toggleText = document.getElementById("authToggleText");
    
    if (isSignUpMode) {
        title.innerText = "🌸 회원가입 🌸";
        sub.innerText = "새로운 감정나무 계정을 만들어보세요.";
        btn.innerText = "회원가입";
        toggleText.innerHTML = '이미 계정이 있으신가요? <span onclick="toggleAuthMode()">로그인하기</span>';
    } else {
        title.innerText = "🌸 로그인 🌸";
        sub.innerText = "감정나무를 키우기 위해 로그인해주세요.";
        btn.innerText = "로그인";
        toggleText.innerHTML = '계정이 없으신가요? <span onclick="toggleAuthMode()">회원가입하기</span>';
    }
}

function handleAuth() {
    const username = document.getElementById("username").value.trim();
    const password = document.getElementById("password").value.trim();
    if (!username || !password) { alert("아이디와 비밀번호를 모두 입력해주세요."); return; }
    
    let users = JSON.parse(localStorage.getItem("diary_users")) || {};
    
    if (isSignUpMode) {
        if (users[username]) { alert("이미 존재하는 아이디입니다."); return; }
        users[username] = { password: password, attendanceCount: 0, lastSavedDate: "", attendedDays: [], moodHistory: {} };
        localStorage.setItem("diary_users", JSON.stringify(users));
        alert("회원가입이 완료되었습니다! 로그인 해주세요.");
        toggleAuthMode();
    } else {
        if (!users[username] || users[username].password !== password) { alert("아이디 또는 비밀번호가 일치하지 않습니다."); return; }
        currentUser = username;
        document.getElementById("authScreen").classList.add("hidden");
        document.getElementById("mainScreen").classList.remove("hidden");
        document.getElementById("username").value = "";
        document.getElementById("password").value = "";
        updateMainScreen();
    }
}

function selectMood(mood, element) {
    let users = JSON.parse(localStorage.getItem("diary_users"));
    let userData = users[currentUser];
    const today = new Date();
    const todayKey = `${today.getFullYear()}-${today.getMonth()+1}-${today.getDate()}`;
    
    selectedMood = mood;
    const buttons = document.querySelectorAll(".mood-btn");
    buttons.forEach(btn => btn.classList.remove("selected"));
    element.classList.add("selected");
    
    if (!userData.moodHistory) userData.moodHistory = {};
    userData.moodHistory[todayKey] = mood;
    users[currentUser] = userData;
    localStorage.setItem("diary_users", JSON.stringify(users));
    
    alert(`오늘의 기분이 [${mood}]으로 기록되었습니다! 일기를 작성해 보세요. ✨`);
}

function logout() {
    currentUser = null; selectedMood = "";
    document.getElementById("mainScreen").classList.add("hidden");
    document.getElementById("diaryScreen").classList.add("hidden");
    document.getElementById("historyScreen").classList.add("hidden");
    document.getElementById("boardScreen").classList.add("hidden");
    document.getElementById("authScreen").classList.remove("hidden");
}

function updateMainScreen() {
    if (!currentUser) return;
    let users = JSON.parse(localStorage.getItem("diary_users"));
    let userData = users[currentUser];
    
    document.getElementById("welcomeText").innerText = `✨ ${currentUser}님의 정원 ✨`;
    document.getElementById("daysText").innerText = `총 출석 ${userData.attendanceCount}일째`;
    
    const treeElement = document.getElementById("tree");
    const count = userData.attendanceCount;
    if (count === 0) treeElement.innerText = "🌱";
    else if (count >= 1 && count <= 3) treeElement.innerText = "🌿";
    else if (count >= 4 && count <= 6) treeElement.innerText = "🌳";
    else treeElement.innerText = "🌸";
    
    const buttons = document.querySelectorAll(".mood-btn");
    buttons.forEach(btn => btn.classList.remove("selected"));
    
    const today = new Date();
    const todayKey = `${today.getFullYear()}-${today.getMonth()+1}-${today.getDate()}`;
    if (userData.moodHistory && userData.moodHistory[todayKey]) {
        selectedMood = userData.moodHistory[todayKey];
        buttons.forEach(btn => { if (btn.innerText === selectedMood) btn.classList.add("selected"); });
    } else {
        selectedMood = "";
    }
    
    for(let i=0; i<7; i++) {
        const slot = document.getElementById(`slot-${i}`);
        slot.innerText = ""; slot.classList.remove("active");
    }
    if (userData.attendedDays) {
        userData.attendedDays.forEach(day => {
            const slot = document.getElementById(`slot-${day}`);
            if (slot) { slot.innerText = "🌸"; slot.classList.add("active"); }
        });
    }
    document.getElementById("attendancePanel").classList.remove("hidden");
}

function openDiary() {
    if (!selectedMood) { alert("오늘의 기분을 먼저 선택해 주세요! 😊"); return; }
    const randomIdx = Math.floor(Math.random() * questions.length);
    currentQuestion = questions[randomIdx];
    document.getElementById("question").innerText = currentQuestion;
    document.getElementById("diaryText").value = "";
    document.getElementById("mainScreen").classList.add("hidden");
    document.getElementById("diaryScreen").classList.remove("hidden");
}

function saveDiary() {
    const text = document.getElementById("diaryText").value.trim();
    if (!text) { alert("내용을 입력해주세요!"); return; }

    const today = new Date();
    const todayStr = today.toLocaleDateString();
    const currentDayOfWeek = today.getDay();
    
    let users = JSON.parse(localStorage.getItem("diary_users"));
    let userData = users[currentUser];
    
    userData.attendanceCount += 1;
    userData.lastSavedDate = todayStr;
    
    if (!userData.attendedDays) userData.attendedDays = [];
    if (!userData.attendedDays.includes(currentDayOfWeek)) userData.attendedDays.push(currentDayOfWeek);
    
    users[currentUser] = userData;
    localStorage.setItem("diary_users", JSON.stringify(users));
    
    // 📣 공유 게시판용 데이터 저장
    let globalBoard = JSON.parse(localStorage.getItem("diary_board")) || [];
    const newPost = {
        id: Date.now(),
        author: currentUser,
        mood: selectedMood,
        question: currentQuestion,
        content: text,
        date: new Date().toLocaleString('ko-KR', { month: 'short', day: 'numeric', hour: '2-digit', minute:'2-digit' }),
        comments: []
    };
    globalBoard.unshift(newPost); // 최신글이 위로 오도록 추가
    localStorage.setItem("diary_board", JSON.stringify(globalBoard));
    
    alert("오늘의 일기가 저장되었으며, 📣공유 게시판에도 등록되었습니다! ✨");
    updateMainScreen();
    goHome();
}

// 📣 게시판 열기 및 렌더링
function openBoard() {
    document.getElementById("mainScreen").classList.add("hidden");
    document.getElementById("boardScreen").classList.remove("hidden");
    renderBoard();
}

function renderBoard() {
    const container = document.getElementById("postListContainer");
    container.innerHTML = "";
    
    let globalBoard = JSON.parse(localStorage.getItem("diary_board")) || [];
    
    if (globalBoard.length === 0) {
        container.innerHTML = "<p style='text-align:center; color:#bbb; padding: 20px;'>아직 공유된 질문 답글이 없습니다. 첫 글을 남겨보세요!</p>";
        return;
    }
    
    globalBoard.forEach(post => {
        const postItem = document.createElement("div");
        postItem.className = "post-item";
        
        // 댓글 문자열 생성
        let commentsHtml = "";
        post.comments.forEach(comment => {
            commentsHtml += `
                <div class="comment-item">
                    <span class="comment-user">${comment.writer}:</span>
                    <span>${comment.text}</span>
                </div>
            `;
        });
        
        postItem.innerHTML = `
            <div class="post-meta">
                <span>👤 ${post.author}님의 마음 (${post.mood})</span>
                <span style="color:#aaa; font-weight:normal;">${post.date}</span>
            </div>
            <div class="post-q">Q. ${post.question}</div>
            <div class="post-content">${post.content.replace(/\n/g, '<br>')}</div>
            
            <div class="comment-section">
                <div id="comments-box-${post.id}">
                    ${commentsHtml}
                </div>
                <div class="comment-input-box" onclick="event.stopPropagation();">
                    <input type="text" id="input-${post.id}" class="comment-input" placeholder="따뜻한 댓글을 남겨주세요...">
                    <button class="comment-btn" onclick="addComment(${post.id})">등록</button>
                </div>
            </div>
        `;
        container.appendChild(postItem);
    });
}

// 댓글 추가하기
function addComment(postId) {
    const inputElement = document.getElementById(`input-${postId}`);
    const commentText = inputElement.value.trim();
    if (!commentText) { alert("댓글 내용을 입력해 주세요!"); return; }
    
    let globalBoard = JSON.parse(localStorage.getItem("diary_board")) || [];
    const postIndex = globalBoard.findIndex(p => p.id === postId);
    
    if (postIndex !== -1) {
        globalBoard[postIndex].comments.push({
            writer: currentUser,
            text: commentText
        });
        localStorage.setItem("diary_board", JSON.stringify(globalBoard));
        inputElement.value = "";
        renderBoard(); // 댓글 반영을 위한 새로고침
    }
}

function closeBoard() {
    document.getElementById("boardScreen").classList.add("hidden");
    document.getElementById("mainScreen").classList.remove("hidden");
}

function openHistory() {
    document.getElementById("mainScreen").classList.add("hidden");
    document.getElementById("historyScreen").classList.remove("hidden");
    
    const now = new Date();
    const currentYear = now.getFullYear(); const currentMonth = now.getMonth(); 
    document.getElementById("calendarTitle").innerText = `${currentYear}년 ${currentMonth + 1}월 기분 달력`;
    
    const grid = document.getElementById("monthlyCalendarGrid");
    const headers = grid.querySelectorAll(".cal-header");
    grid.innerHTML = ""; headers.forEach(h => grid.appendChild(h));
    
    const firstDayIndex = new Date(currentYear, currentMonth, 1).getDay();
    const totalDays = new Date(currentYear, currentMonth + 1, 0).getDate();
    
    let users = JSON.parse(localStorage.getItem("diary_users"));
    let userData = users[currentUser];
    let moodHistory = userData.moodHistory || {};
    let moodCounts = { '🤬':0, '🥺':0, '😰':0, '😭':0, '😊':0, '🤪':0 };
    let hasAnyData = false;
    
    for (let i = 0; i < firstDayIndex; i++) {
        const blank = document.createElement("div");
        blank.className = "cal-day"; blank.style.visibility = "hidden"; grid.appendChild(blank);
    }
    
    for (let day = 1; day <= totalDays; day++) {
        const dayCell = document.createElement("div"); dayCell.className = "cal-day has-data";
        const dayNum = document.createElement("span"); dayNum.innerText = day; dayCell.appendChild(dayNum);
        
        const dateKey = `${currentYear}-${currentMonth + 1}-${day}`;
        if (moodHistory[dateKey]) {
            const moodEmoji = document.createElement("span");
            moodEmoji.className = "cal-mood"; moodEmoji.innerText = moodHistory[dateKey];
            dayCell.appendChild(moodEmoji);
            if (moodCounts[moodHistory[dateKey]] !== undefined) { moodCounts[moodHistory[dateKey]]++; hasAnyData = true; }
        }
        grid.appendChild(dayCell);
    }
    
    const mentDiv = document.getElementById("analysisMent");
    if (!hasAnyData) {
        mentDiv.innerText = "이번 달에 아직 기록된 기분이 없네요. 감정 정원을 가꿔보세요! 🌸";
    } else {
        let maxMood = ""; let maxCount = -1;
        for (let mood in moodCounts) { if (moodCounts[mood] > maxCount) { maxCount = moodCounts[mood]; maxMood = mood; } }
        mentDiv.innerHTML = `이번 달은 [ ${maxMood} ] 기분을 가장 많이 느끼셨네요! (총 ${maxCount}회)<br><br>` + moodMentions[maxMood];
    }
}

function closeHistory() { document.getElementById("historyScreen").classList.add("hidden"); document.getElementById("mainScreen").classList.remove("hidden"); }
function goHome() { document.getElementById("diaryScreen").classList.add("hidden"); document.getElementById("mainScreen").classList.remove("hidden"); }
function closeAttendance() { document.getElementById("attendancePanel").classList.add("hidden"); }
</script>

</body>
</html>
