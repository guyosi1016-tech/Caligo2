<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>배송 공유</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0d0e1a;
  --bg2: #111226;
  --surface: #161829;
  --surface2: #1c1f35;
  --border: #2a2d4a;
  --border-neon: #4a5aff;
  --text: #e8eaff;
  --muted: #7b82b8;
  --accent: #5b6eff;
  --accent2: #818dff;
  --accent-light: rgba(91,110,255,0.12);
  --neon-glow: 0 0 8px #5b6eff, 0 0 24px rgba(91,110,255,0.4);
  --neon-glow-soft: 0 0 6px rgba(91,110,255,0.3);
  --done-bg: #5b6eff; --done-fg: #fff;
  --during-bg: rgba(91,110,255,0.18); --during-fg: #a0aaff;
  --before-bg: #1c1f35; --before-fg: #7b82b8;
  --danger: #ff5b7a;
  --r: 12px; --rs: 8px;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: 'Noto Sans KR', sans-serif;
  background: var(--bg);
  background-image:
    radial-gradient(ellipse 80% 60% at 50% -10%, rgba(60,80,255,0.18) 0%, transparent 70%),
    radial-gradient(ellipse 60% 40% at 80% 100%, rgba(80,60,255,0.1) 0%, transparent 60%);
  color: var(--text);
  min-height: 100vh;
}

header {
  background: rgba(13,14,26,0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  padding: 16px 20px;
  display: flex; align-items: center; justify-content: space-between;
  position: sticky; top: 0; z-index: 100;
}
.logo { font-size: 16px; font-weight: 700; letter-spacing: -.5px; cursor: pointer; color: var(--text); }
.logo span { color: var(--accent); text-shadow: var(--neon-glow-soft); }
.hbtn {
  font-size: 13px; background: none;
  border: 1px solid var(--border-neon);
  border-radius: var(--rs); padding: 6px 13px;
  cursor: pointer; color: var(--accent2);
  font-family: inherit; transition: all .2s;
  box-shadow: var(--neon-glow-soft);
}
.hbtn:hover { background: var(--accent-light); color: #fff; box-shadow: var(--neon-glow); }

.page { display: none; max-width: 640px; margin: 0 auto; padding: 36px 16px; }
.page.active { display: block; }

/* 메인 */
.hero { text-align: center; padding: 60px 0 40px; }
.hero h1 { font-size: 26px; font-weight: 700; letter-spacing: -.5px; margin-bottom: 10px; color: #fff; text-shadow: var(--neon-glow-soft); }
.hero p { font-size: 15px; color: var(--muted); line-height: 1.7; margin-bottom: 32px; }
.hero-btns { display: flex; flex-direction: column; align-items: center; gap: 12px; }
.btn-main-top { width: 220px; padding: 13px 28px; font-size: 15px; font-weight: 700; }
.hero-btns-row { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
.btn-main-sub { padding: 11px 20px; font-size: 14px; min-width: 150px; }
.btn-p {
  padding: 11px 28px;
  background: linear-gradient(135deg, #4a5aff, #6a7aff);
  color: #fff; border: none; border-radius: var(--rs);
  font-family: inherit; font-size: 14px; font-weight: 500;
  cursor: pointer; transition: all .2s;
  box-shadow: var(--neon-glow);
}
.btn-p:hover { opacity: .9; box-shadow: 0 0 16px #5b6eff, 0 0 40px rgba(91,110,255,0.5); transform: translateY(-1px); }
.btn-o {
  padding: 11px 28px; background: transparent;
  color: var(--accent2);
  border: 1px solid var(--border-neon);
  border-radius: var(--rs); font-family: inherit; font-size: 14px; font-weight: 500;
  cursor: pointer; transition: all .2s;
  box-shadow: var(--neon-glow-soft);
}
.btn-o:hover { background: var(--accent-light); color: #fff; box-shadow: var(--neon-glow); transform: translateY(-1px); }
.feat-cards { margin-top: 48px; display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 14px; }
.feat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--r); padding: 18px 16px; text-align: center;
  transition: border-color .2s, box-shadow .2s;
}
.feat-card:hover { border-color: var(--border-neon); box-shadow: var(--neon-glow-soft); }
.feat-card .ic { font-size: 26px; margin-bottom: 8px; }
.feat-card h3 { font-size: 14px; font-weight: 500; margin-bottom: 4px; color: var(--text); }
.feat-card p { font-size: 12px; color: var(--muted); line-height: 1.6; }

/* 폼 */
.fcard {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--r); padding: 24px 20px; margin-bottom: 16px;
}
.fcard h2 { font-size: 17px; font-weight: 700; margin-bottom: 4px; color: var(--text); }
.fcard .sub { font-size: 13px; color: var(--muted); margin-bottom: 20px; }
.field { margin-bottom: 14px; }
.field label { display: block; font-size: 12px; color: var(--muted); margin-bottom: 5px; }
.field input {
  width: 100%; padding: 10px 12px;
  border: 1px solid var(--border);
  border-radius: var(--rs); font-family: inherit; font-size: 14px;
  background: var(--bg2); color: var(--text); outline: none; transition: border-color .15s, box-shadow .15s;
}
.field input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(91,110,255,0.15); }
.ferr { font-size: 12px; color: var(--danger); margin-top: 4px; display: none; }
.fhint { font-size: 12px; color: var(--muted); margin-top: 4px; }
.full-btn { width: 100%; padding: 11px; margin-top: 6px; }
.urlbox {
  background: var(--bg2); border: 1px solid var(--border-neon);
  border-radius: var(--rs); padding: 12px 14px; font-size: 13px;
  word-break: break-all; color: var(--accent2); margin-bottom: 10px; cursor: pointer;
  box-shadow: var(--neon-glow-soft);
}
.urlbox:hover { background: var(--accent-light); }
.copyhint { font-size: 12px; color: var(--muted); text-align: center; }

/* 잠금 */
.lockwrap { min-height: 80vh; display: flex; align-items: center; justify-content: center; padding: 20px; }
.lockcard {
  background: var(--surface); border: 1px solid var(--border-neon);
  border-radius: var(--r); padding: 28px 22px; width: 100%; max-width: 320px;
  box-shadow: var(--neon-glow-soft);
}
.lockcard h2 { font-size: 18px; font-weight: 700; margin-bottom: 4px; color: var(--text); }
.lockcard .sub { font-size: 13px; color: var(--muted); margin-bottom: 20px; }
.lockerr { font-size: 13px; color: var(--danger); margin-top: 10px; text-align: center; display: none; }

/* 방 내부 */
.room-title { font-size: 19px; font-weight: 700; letter-spacing: -.3px; margin-bottom: 2px; color: #fff; text-shadow: var(--neon-glow-soft); }
.room-sub { font-size: 13px; color: var(--muted); margin-bottom: 18px; }
.sharebar {
  background: var(--accent-light); border: 1px solid var(--border-neon);
  border-radius: var(--rs); padding: 12px 14px;
  display: flex; align-items: center; justify-content: space-between; gap: 10px; margin-bottom: 20px; cursor: pointer;
  box-shadow: var(--neon-glow-soft); transition: box-shadow .2s;
}
.sharebar:hover { box-shadow: var(--neon-glow); }
.share-label { font-size: 13px; color: var(--accent2); font-weight: 500; }
.share-url { font-size: 11px; color: var(--accent2); opacity: .7; word-break: break-all; margin-top: 2px; }

/* 닉네임 배너 */
.nick-banner {
  background: rgba(255,180,0,0.08); border: 1px solid rgba(255,180,0,0.3);
  border-radius: var(--rs); padding: 12px 14px; margin-bottom: 18px; display: flex; align-items: center; gap: 10px;
}
.nick-banner span { font-size: 13px; color: #fbbf24; flex: 1; }
.nick-banner button { font-size: 12px; background: #f59e0b; color: #fff; border: none; border-radius: 6px; padding: 5px 12px; cursor: pointer; white-space: nowrap; font-family: inherit; font-weight: 500; }

/* 닉네임 팝업 */
.nick-modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,.6); display: none; align-items: center; justify-content: center; z-index: 200; padding: 16px; backdrop-filter: blur(4px); }
.nick-modal-overlay.open { display: flex; }
.nick-modal {
  background: var(--surface2); border: 1px solid var(--border-neon);
  border-radius: var(--r); padding: 24px 20px; width: 100%; max-width: 300px;
  box-shadow: var(--neon-glow);
}
.nick-modal h3 { font-size: 16px; font-weight: 700; margin-bottom: 4px; color: var(--text); }
.nick-modal p { font-size: 13px; color: var(--muted); margin-bottom: 16px; }
.nick-modal input {
  width: 100%; padding: 10px 12px; border: 1px solid var(--border);
  border-radius: var(--rs); font-family: inherit; font-size: 14px;
  background: var(--bg2); color: var(--text); outline: none; margin-bottom: 6px;
}
.nick-modal input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(91,110,255,0.15); }
.nick-ferr { font-size: 12px; color: var(--danger); margin-bottom: 10px; display: none; }
.nick-btns { display: flex; gap: 8px; }
.nick-btns button { flex: 1; padding: 10px; border-radius: var(--rs); font-family: inherit; font-size: 14px; font-weight: 500; cursor: pointer; border: 1px solid var(--border); background: none; color: var(--muted); transition: all .15s; }
.nick-btns .nbtn-p { background: linear-gradient(135deg,#4a5aff,#6a7aff); color: #fff; border-color: var(--accent); box-shadow: var(--neon-glow-soft); }
.nick-btns .nbtn-p:hover { opacity: .85; }

/* 송장 추가 패널 */
#addSection { background: var(--surface); border: 1px solid var(--border); border-radius: var(--r); padding: 16px; margin-bottom: 18px; }
#addSection h3 { font-size: 13px; font-weight: 500; color: var(--muted); margin-bottom: 12px; }
.addrow { display: flex; gap: 8px; flex-wrap: wrap; }
.addrow input, .addrow select {
  font-family: inherit; font-size: 14px; padding: 9px 11px;
  border: 1px solid var(--border); border-radius: var(--rs);
  background: var(--bg2); color: var(--text); outline: none; transition: border-color .15s, box-shadow .15s;
}
.addrow input:focus, .addrow select:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(91,110,255,0.12); }
.addrow select option { background: var(--surface2); }
.fi-country { min-width: 130px; flex: 0 0 auto; cursor: pointer; }
.fi-carrier { flex: 1; min-width: 120px; cursor: pointer; }
.fi-name { flex: 1; min-width: 110px; }
.fi-seller { flex: 1; min-width: 100px; }
.fi-track { flex: 1.2; min-width: 130px; }
.addbtn {
  padding: 9px 16px; background: linear-gradient(135deg,#4a5aff,#6a7aff);
  color: #fff; border: none; border-radius: var(--rs);
  font-family: inherit; font-size: 14px; font-weight: 500; cursor: pointer; white-space: nowrap;
  box-shadow: var(--neon-glow-soft); transition: all .2s;
}
.addbtn:hover { opacity: .85; box-shadow: var(--neon-glow); }

/* 국가 뱃지 */
.country-badge { display: inline-block; font-size: 11px; background: var(--surface2); color: var(--muted); padding: 2px 7px; border-radius: 10px; margin-left: 5px; }
.otrack-link { display: none; }

/* 상태 변경 버튼 */
.ssbtn-group { display: flex; gap: 5px; margin-top: 8px; flex-wrap: wrap; }
.ssbtn { font-size: 11px; font-family: inherit; padding: 3px 9px; border-radius: 20px; border: 1px solid var(--border); background: none; color: var(--muted); cursor: pointer; transition: all .15s; }
.ssbtn:hover { border-color: var(--accent); color: var(--accent2); }
.ssbtn-active { background: var(--accent-light); border-color: var(--border-neon); color: var(--accent2); font-weight: 600; }

/* 목록 */
.listhd { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; }
.ltitle { font-size: 14px; font-weight: 500; color: var(--text); }
.cnt { font-size: 12px; background: var(--accent-light); color: var(--accent2); padding: 3px 10px; border-radius: 20px; font-weight: 500; margin-left: 6px; border: 1px solid rgba(91,110,255,0.3); }
.refbtn { font-size: 13px; color: var(--muted); background: none; border: 1px solid var(--border); border-radius: var(--rs); padding: 5px 11px; cursor: pointer; font-family: inherit; transition: all .15s; }
.refbtn:hover { border-color: var(--accent); color: var(--accent2); }
#orderList { display: flex; flex-direction: column; gap: 9px; }

.ocard {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--r); padding: 14px 16px;
  display: flex; align-items: center; gap: 12px;
  animation: fadeIn .22s ease; transition: border-color .2s, box-shadow .2s;
}
.ocard:hover { border-color: var(--border-neon); box-shadow: var(--neon-glow-soft); }
@keyframes fadeIn { from { opacity: 0; transform: translateY(4px); } to { opacity: 1; transform: none; } }
.oi { flex: 1; min-width: 0; }
.oname { font-size: 15px; font-weight: 500; margin-bottom: 1px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; color: var(--text); }
.ometa { font-size: 12px; color: var(--muted); margin-bottom: 7px; }
.steps { display: flex; align-items: center; }
.sdot { width: 7px; height: 7px; border-radius: 50%; background: var(--border); flex-shrink: 0; }
.sline { flex: 1; height: 2px; background: var(--border); }
.sdot.on { background: var(--accent); box-shadow: 0 0 6px var(--accent); }
.sline.on { background: var(--accent); }
.pill { flex-shrink: 0; font-size: 12px; font-weight: 500; padding: 5px 11px; border-radius: 20px; white-space: nowrap; }
.p-before { background: var(--before-bg); color: var(--before-fg); border: 1px solid var(--border); }
.p-during { background: var(--during-bg); color: var(--during-fg); border: 1px solid rgba(91,110,255,0.3); }
.p-done   { background: var(--done-bg);   color: var(--done-fg); box-shadow: var(--neon-glow-soft); }
.delbtn { flex-shrink: 0; background: none; border: none; cursor: pointer; color: var(--border); font-size: 20px; padding: 0 3px; line-height: 1; border-radius: 4px; transition: color .15s; }
.delbtn:hover { color: var(--danger); }

.empty { text-align: center; padding: 48px 20px; color: var(--muted); font-size: 14px; background: var(--surface); border: 1px dashed var(--border); border-radius: var(--r); }
.empty-ic { font-size: 32px; margin-bottom: 10px; }

.spinner { display: inline-block; width: 11px; height: 11px; border: 2px solid rgba(91,110,255,0.2); border-top-color: var(--accent); border-radius: 50%; animation: spin .7s linear infinite; vertical-align: middle; margin-right: 4px; }
.p-done .spinner { border-color: rgba(255,255,255,.3); border-top-color: #fff; }
@keyframes spin { to { transform: rotate(360deg); } }

#toast { position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%) translateY(80px); background: var(--surface2); border: 1px solid var(--border-neon); color: var(--text); padding: 10px 20px; border-radius: 24px; font-size: 13px; font-weight: 500; transition: transform .28s ease; z-index: 300; pointer-events: none; white-space: nowrap; box-shadow: var(--neon-glow); }
#toast.show { transform: translateX(-50%) translateY(0); }

@media (max-width: 480px) {
  .addrow { flex-direction: column; }
  .addbtn { width: 100%; }
  .fi-country, .fi-carrier { width: 100%; }
}
</style>
</head>
<body>

<header>
  <div class="logo" onclick="goMain()">배송 <span>공유</span></div>
  <div id="headerRight">
    <button class="hbtn" onclick="showPage('pageCreate')">방 만들기</button>
  </div>
</header>

<!-- 메인 -->
<div class="page active" id="pageMain">
  <div class="hero">
    <h1>📦 내 배송, 간편하게 공유</h1>
    <p>지인들과 개인정보 노출없이 배송 상황을 공유해요</p>
    <div class="hero-btns">
      <button class="btn-p btn-main-top" onclick="showPage('pageCreate')">공유방 만들기</button>
      <div class="hero-btns-row">
        <button class="btn-o btn-main-sub" onclick="showPage('pageJoinLink')">🔗 링크로 접속하기</button>
        <button class="btn-o btn-main-sub" onclick="showPage('pageJoinName')">🏠 방 이름으로 접속하기</button>
      </div>
    </div>
  </div>
    <div class="feat-cards">
    <div class="feat-card"><div class="ic">🔐</div><h3>비밀번호 보호</h3><p>링크를 알아도 비밀번호 없이는 볼 수 없어요</p></div>
    <div class="feat-card"><div class="ic">🌏</div><h3>다국가 지원</h3><p>한국·일본·중국·대만·미국 등 해외 택배사 송장도 추가 가능해요</p></div>
    <div class="feat-card"><div class="ic">👥</div><h3>함께 추가</h3><p>방 안 모두가 본인 송장을 직접 추가할 수 있어요</p></div>
  </div>
</div>

<!-- 방 만들기 -->
<div class="page" id="pageCreate">
  <div class="fcard">
    <h2>공유방 만들기</h2>
    <p class="sub">방 이름과 비밀번호를 설정하면 공유 링크가 생성돼요</p>
    <div class="field">
      <label>방 이름 (한글·영문·숫자, 최대 12자)</label>
      <input type="text" id="cRoomName" placeholder="예: 3월공구, 봄공구, abc" maxlength="12" />
      <div class="ferr" id="cNameErr"></div>
    </div>
    <div class="field">
      <label>비밀번호 (영문+숫자, 4~8자)</label>
      <input type="password" id="cPw" placeholder="예: shop1234" maxlength="8" />
      <div class="fhint">친구들에게 이 비밀번호를 알려주세요</div>
      <div class="ferr" id="cPwErr"></div>
    </div>
    <button class="btn-p full-btn" onclick="createRoom()">방 만들기</button>
  </div>
  <div class="fcard" id="createdBox" style="display:none;">
    <h2>✅ 공유방이 만들어졌어요!</h2>
    <p class="sub">아래 링크를 복사해서 친구들에게 공유하세요</p>
    <div class="urlbox" id="createdUrl" onclick="copyCreatedUrl()"></div>
    <p class="copyhint">👆 탭하면 복사돼요 · 비밀번호도 함께 알려주세요</p>
  </div>
</div>

<!-- 링크로 접속 -->
<div class="page" id="pageJoinLink">
  <div class="fcard">
    <h2>🔗 링크로 접속하기</h2>
    <p class="sub">공유받은 링크와 비밀번호를 입력하세요</p>
    <div class="field">
      <label>공유 링크</label>
      <input type="url" id="jLink" placeholder="https://guyosi1016-tech.github.io/Caligo2/#방이름" />
      <div class="fhint">친구에게 받은 링크를 그대로 붙여넣으세요</div>
    </div>
    <div class="field">
      <label>비밀번호</label>
      <input type="password" id="jLinkPw" placeholder="비밀번호" maxlength="8"
        onkeydown="if(event.key==='Enter')joinByLink()" />
    </div>
    <div class="ferr" id="jLinkErr" style="display:none; margin-bottom:8px;"></div>
    <button class="btn-p full-btn" onclick="joinByLink()">입장하기</button>
  </div>
</div>

<!-- 방 이름으로 접속 -->
<div class="page" id="pageJoinName">
  <div class="fcard">
    <h2>🏠 방 이름으로 접속하기</h2>
    <p class="sub">방 이름과 비밀번호를 직접 입력하세요</p>
    <div class="field">
      <label>방 이름</label>
      <input type="text" id="jRoomName" placeholder="방 이름" maxlength="12" />
    </div>
    <div class="field">
      <label>비밀번호</label>
      <input type="password" id="jPw" placeholder="비밀번호" maxlength="8"
        onkeydown="if(event.key==='Enter')joinRoom()" />
    </div>
    <div class="ferr" id="jErr" style="display:none; margin-bottom:8px;"></div>
    <button class="btn-p full-btn" onclick="joinRoom()">입장하기</button>
  </div>
</div>

<!-- 잠금 화면 -->
<div class="page" id="pageLock">
  <div class="lockwrap">
    <div class="lockcard">
      <h2>🔐 비밀번호 입력</h2>
      <p class="sub" id="lockSub">이 공유방은 비밀번호로 보호돼 있어요</p>
      <div class="field">
        <label>비밀번호</label>
        <input type="password" id="lockPw" placeholder="비밀번호" maxlength="8"
          onkeydown="if(event.key==='Enter')submitLock()" />
      </div>
      <button class="btn-p full-btn" onclick="submitLock()">확인</button>
      <div class="lockerr" id="lockErr">비밀번호가 틀렸어요. 메인으로 이동합니다...</div>
    </div>
  </div>
</div>

<!-- 방 내부 -->
<div class="page" id="pageRoom">
  <div class="room-title" id="roomTitle"></div>
  <div class="room-sub" id="roomSub">배송 현황</div>

  <div class="sharebar" onclick="copyRoomUrl()">
    <div>
      <div class="share-label">🔗 친구들에게 이 링크를 공유하세요</div>
      <div class="share-url" id="shareUrlText"></div>
    </div>
    <span style="font-size:18px; flex-shrink:0;">📋</span>
  </div>

  <!-- 닉네임 미설정 시 안내 -->
  <div class="nick-banner" id="nickBanner" style="display:none;">
    <span>✏️ 닉네임을 설정하면 내 송장을 추가할 수 있어요</span>
    <button onclick="openNickModal()">닉네임 설정</button>
  </div>

  <!-- 송장 추가 패널 (닉네임 있으면 표시) -->
  <div id="addSection" style="display:none;">
    <h3 id="addSectionTitle">내 송장 추가</h3>
    <div class="addrow">
      <select class="fi-country" id="inputCountry" onchange="updateCarriers()">
        <option value="kr">🇰🇷 한국</option>
        <option value="jp">🇯🇵 일본</option>
        <option value="cn">🇨🇳 중국</option>
        <option value="tw">🇹🇼 대만</option>
        <option value="us">🇺🇸 미국</option>
        <option value="other">🌐 기타</option>
      </select>
      <select class="fi-carrier" id="inputCarrier">
        <option value="kr.cjlogistics">CJ대한통운</option>
        <option value="kr.logen">로젠택배</option>
        <option value="kr.hanjin">한진택배</option>
        <option value="kr.lotte">롯데택배</option>
        <option value="kr.epost">우체국택배</option>
      </select>
    </div>
    <div class="addrow" style="margin-top:8px;">
      <input type="text" class="fi-name" id="inputName" placeholder="주문 이름" />
      <input type="text" class="fi-seller" id="inputSeller" placeholder="판매처 (선택)" />
      <input type="text" class="fi-track" id="inputTrack" placeholder="운송장 번호" maxlength="30" inputmode="text" />
      <button class="addbtn" onclick="addOrder()">+ 추가</button>
    </div>
    <div id="trackHint" style="font-size:12px;color:var(--muted);margin-top:6px;"></div>
  </div>

  <div class="listhd">
    <span class="ltitle">배송 목록 <span class="cnt" id="cntBadge">0</span></span>
    <button class="refbtn" onclick="refreshAll()">새로고침</button>
  </div>
  <div id="orderList">
    <div class="empty"><div class="empty-ic">📭</div>불러오는 중...</div>
  </div>
</div>

<!-- 닉네임 설정 모달 -->
<div class="nick-modal-overlay" id="nickModalOverlay">
  <div class="nick-modal">
    <h3>닉네임 설정</h3>
    <p>방 안에서 사용할 닉네임을 입력하세요</p>
    <input type="text" id="nickInput" placeholder="예: 홍길동, gildong" maxlength="10"
      onkeydown="if(event.key==='Enter')saveNick()" />
    <div class="nick-ferr" id="nickErr"></div>
    <div class="nick-btns">
      <button onclick="closeNickModal()">취소</button>
      <button class="nbtn-p" onclick="saveNick()">설정하기</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore-compat.js"></script>
<script>
const FIREBASE_CONFIG = {
  apiKey:            "AIzaSyBglu3qoZ3U_5d6RND_6Lx6XZgPWhmN6lY",
  authDomain:        "caligo2.firebaseapp.com",
  projectId:         "caligo2",
  storageBucket:     "caligo2.firebasestorage.app",
  messagingSenderId: "567781917671",
  appId:             "1:567781917671:web:694635c7b88c10d490f342"
};
firebase.initializeApp(FIREBASE_CONFIG);
const db = firebase.firestore();

let currentRoom = null;
let myNick = null;      // 이 방에서의 내 닉네임 (세션 기반)
let orders = [];
let pendingRoomId = null;

// ── 입력 필터 ──────────────────────────────
function filterRoomName(el) {
  var filtered = '';
  for (var i = 0; i < el.value.length; i++) {
    var c = el.value.charCodeAt(i);
    if ((c >= 0xAC00 && c <= 0xD7A3) || (c >= 0x3131 && c <= 0x314E) ||
        (c >= 0x314F && c <= 0x3163) || (c >= 65 && c <= 90) ||
        (c >= 97 && c <= 122) || (c >= 48 && c <= 57)) {
      filtered += el.value[i];
    }
  }
  if (filtered !== el.value) el.value = filtered;
}
function filterPw(el) { el.value = el.value.replace(/[^a-zA-Z0-9]/g, ''); }
function filterNick(el) {
  var filtered = '';
  for (var i = 0; i < el.value.length; i++) {
    var c = el.value.charCodeAt(i);
    if ((c >= 0xAC00 && c <= 0xD7A3) || (c >= 0x3131 && c <= 0x314E) ||
        (c >= 0x314F && c <= 0x3163) || (c >= 65 && c <= 90) ||
        (c >= 97 && c <= 122) || (c >= 48 && c <= 57)) {
      filtered += el.value[i];
    }
  }
  if (filtered !== el.value) el.value = filtered;
}

document.getElementById('cRoomName').addEventListener('input', function() { filterRoomName(this); });
document.getElementById('jRoomName').addEventListener('input', function() { filterRoomName(this); });
document.getElementById('cPw').addEventListener('input', function() { filterPw(this); });
document.getElementById('jPw').addEventListener('input', function() { filterPw(this); });
document.getElementById('jLinkPw').addEventListener('input', function() { filterPw(this); });
document.getElementById('lockPw').addEventListener('input', function() { filterPw(this); });
document.getElementById('nickInput').addEventListener('input', function() { filterNick(this); });

// ── 초기화 ────────────────────────────────
function init() {
  var hash = location.hash.replace('#', '');
  if (hash) {
    pendingRoomId = decodeURIComponent(hash);
    document.getElementById('lockSub').textContent = '"' + pendingRoomId + '" 공유방에 입장하려면 비밀번호를 입력하세요';
    showPage('pageLock');
    setTimeout(function() { document.getElementById('lockPw').focus(); }, 100);
  } else {
    showPage('pageMain');
  }
  renderHeader();
}

function showPage(id) {
  document.querySelectorAll('.page').forEach(function(p) { p.classList.remove('active'); });
  document.getElementById(id).classList.add('active');
  window.scrollTo(0, 0);
}

function goMain() {
  currentRoom = null; myNick = null; orders = [];
  history.replaceState(null, '', location.pathname);
  showPage('pageMain');
  renderHeader();
}

function renderHeader() {
  var el = document.getElementById('headerRight');
  if (currentRoom) {
    var nickLabel = myNick ? '<span style="font-size:13px;color:var(--accent);background:var(--accent-light);padding:5px 10px;border-radius:20px;margin-right:6px;">' + esc(myNick) + '</span>' : '';
    el.innerHTML = nickLabel + '<button class="hbtn" onclick="goMain()">나가기</button>';
  } else {
    el.innerHTML = '<button class="hbtn" onclick="showPage(\'pageCreate\')">방 만들기</button>';
  }
}

// ── URL ───────────────────────────────────
function makeUrl(roomId) {
  return location.origin + location.pathname + '#' + encodeURIComponent(roomId);
}
function copyCreatedUrl() {
  navigator.clipboard.writeText(document.getElementById('createdUrl').textContent)
    .then(function() { toast('링크가 복사됐어요!'); });
}
function copyRoomUrl() {
  navigator.clipboard.writeText(makeUrl(currentRoom.id))
    .then(function() { toast('링크가 복사됐어요!'); });
}

// ── 방 만들기 ─────────────────────────────
async function createRoom() {
  var name = document.getElementById('cRoomName').value.trim();
  var pw = document.getElementById('cPw').value;
  document.getElementById('cNameErr').style.display = 'none';
  document.getElementById('cPwErr').style.display = 'none';

  if (!name) { showErr('cNameErr', '방 이름을 입력해주세요'); return; }
  if (name.length > 12) { showErr('cNameErr', '최대 12자까지 입력 가능해요'); return; }
  if (!/^[a-zA-Z0-9]{4,8}$/.test(pw)) { showErr('cPwErr', '영문+숫자 4~8자로 입력해주세요'); return; }

  try {
    var snap = await db.collection('rooms').doc(name).get();
    if (snap.exists) { showErr('cNameErr', '이미 있는 방 이름이에요. 다른 이름을 사용해주세요'); return; }

    await db.collection('rooms').doc(name).set({
      name: name, pw: pw,
      createdAt: firebase.firestore.FieldValue.serverTimestamp()
    });

    var url = makeUrl(name);
    document.getElementById('createdUrl').textContent = url;
    document.getElementById('createdBox').style.display = 'block';

    history.replaceState(null, '', location.pathname + '#' + encodeURIComponent(name));
    currentRoom = { id: name };

    // 방장은 닉네임 설정 후 입장
    document.getElementById('roomTitle').textContent = '📦 ' + name;
    document.getElementById('shareUrlText').textContent = url;
    renderHeader();
    showPage('pageRoom');
    loadOrders();
    updateAddPanel();
    toast('방이 만들어졌어요! 링크를 공유하세요 🎉');
  } catch(e) { toast('오류가 발생했어요. 다시 시도해주세요.'); }
}

// ── 링크로 접속 ───────────────────────────
async function joinByLink() {
  var link = document.getElementById('jLink').value.trim();
  var pw   = document.getElementById('jLinkPw').value;
  var errEl = document.getElementById('jLinkErr');
  errEl.style.display = 'none';

  if (!link || !pw) { errEl.textContent = '링크와 비밀번호를 모두 입력해주세요'; errEl.style.display = 'block'; return; }

  // URL에서 # 뒤 방 이름 추출
  var hashIdx = link.indexOf('#');
  if (hashIdx === -1) { errEl.textContent = '올바른 공유 링크가 아니에요 (# 이 없어요)'; errEl.style.display = 'block'; return; }
  var roomId = decodeURIComponent(link.slice(hashIdx + 1));
  if (!roomId) { errEl.textContent = '링크에서 방 이름을 찾을 수 없어요'; errEl.style.display = 'block'; return; }

  var result = await verifyRoom(roomId, pw);
  if (result === 'ok') { enterRoom(roomId); }
  else if (result === 'wrong_pw') { errEl.textContent = '비밀번호가 틀렸어요'; errEl.style.display = 'block'; }
  else { errEl.textContent = '존재하지 않는 방이에요. 링크를 다시 확인해주세요'; errEl.style.display = 'block'; }
}

// ── 방 이름으로 접속 ──────────────────────
async function joinRoom() {
  var name = document.getElementById('jRoomName').value.trim();
  var pw   = document.getElementById('jPw').value;
  var errEl = document.getElementById('jErr');
  errEl.style.display = 'none';

  if (!name || !pw) { errEl.textContent = '방 이름과 비밀번호를 모두 입력해주세요'; errEl.style.display = 'block'; return; }

  var result = await verifyRoom(name, pw);
  if (result === 'ok') { enterRoom(name); }
  else if (result === 'wrong_pw') { errEl.textContent = '비밀번호가 틀렸어요'; errEl.style.display = 'block'; }
  else { errEl.textContent = '존재하지 않는 방이에요'; errEl.style.display = 'block'; }
}

// ── 잠금 화면 ─────────────────────────────
async function submitLock() {
  var pw = document.getElementById('lockPw').value;
  var errEl = document.getElementById('lockErr');
  errEl.style.display = 'none';
  if (!pw) return;

  var result = await verifyRoom(pendingRoomId, pw);
  if (result === 'ok') { enterRoom(pendingRoomId); }
  else {
    errEl.style.display = 'block';
    setTimeout(function() { errEl.style.display = 'none'; goMain(); }, 2000);
  }
}

async function verifyRoom(roomId, pw) {
  try {
    var snap = await db.collection('rooms').doc(roomId).get();
    if (!snap.exists) return 'not_found';
    return snap.data().pw === pw ? 'ok' : 'wrong_pw';
  } catch(e) { return 'error'; }
}

function enterRoom(roomId) {
  currentRoom = { id: roomId };
  // 세션에서 닉네임 복원
  myNick = sessionStorage.getItem('nick_' + roomId) || null;

  history.replaceState(null, '', location.pathname + '#' + encodeURIComponent(roomId));
  document.getElementById('roomTitle').textContent = '📦 ' + roomId;
  document.getElementById('shareUrlText').textContent = makeUrl(roomId);
  renderHeader();
  updateAddPanel();
  showPage('pageRoom');
  loadOrders();
}

// ── 닉네임 패널 업데이트 ──────────────────
function updateAddPanel() {
  if (!currentRoom) return;
  if (myNick) {
    document.getElementById('nickBanner').style.display = 'none';
    document.getElementById('addSection').style.display = 'block';
    document.getElementById('addSectionTitle').textContent = esc(myNick) + '님의 송장 추가';
  } else {
    document.getElementById('nickBanner').style.display = 'flex';
    document.getElementById('addSection').style.display = 'none';
  }
}

// ── 닉네임 모달 ───────────────────────────
function openNickModal() {
  document.getElementById('nickModalOverlay').classList.add('open');
  document.getElementById('nickInput').value = '';
  document.getElementById('nickErr').style.display = 'none';
  setTimeout(function() { document.getElementById('nickInput').focus(); }, 50);
}
function closeNickModal() {
  document.getElementById('nickModalOverlay').classList.remove('open');
}
async function saveNick() {
  var nick = document.getElementById('nickInput').value.trim();
  var errEl = document.getElementById('nickErr');
  errEl.style.display = 'none';

  if (!nick) { errEl.textContent = '닉네임을 입력해주세요'; errEl.style.display = 'block'; return; }
  if (nick.length > 10) { errEl.textContent = '10자 이하로 입력해주세요'; errEl.style.display = 'block'; return; }

  myNick = nick;
  sessionStorage.setItem('nick_' + currentRoom.id, nick);
  closeNickModal();
  updateAddPanel();
  renderHeader();
  toast(nick + '님, 환영해요! 이제 송장을 추가할 수 있어요 😊');
}

// ── 주문 목록 ─────────────────────────────
async function loadOrders() {
  document.getElementById('orderList').innerHTML = '<div class="empty"><div class="empty-ic">⏳</div>불러오는 중...</div>';
  try {
    var snap = await db.collection('rooms').doc(currentRoom.id)
      .collection('orders').orderBy('createdAt', 'desc').get();
    orders = snap.docs.map(function(d) { return Object.assign({ id: d.id }, d.data()); });
    renderList();
    refreshAll();
  } catch(e) {
    document.getElementById('orderList').innerHTML = '<div class="empty"><div class="empty-ic">❌</div>불러오지 못했어요</div>';
  }
}

var LABEL = { before: '배송 전', during: '배송 중', done: '배송 완료' };
var PILL  = { before: 'p-before', during: 'p-during', done: 'p-done' };

// ── 국가별 택배사 정보 ─────────────────────
var CARRIERS = {
  kr: [
    { id: 'kr.cjlogistics', name: 'CJ대한통운' },
    { id: 'kr.logen',       name: '로젠택배' },
    { id: 'kr.hanjin',      name: '한진택배' },
    { id: 'kr.lotte',       name: '롯데택배' },
    { id: 'kr.epost',       name: '우체국택배' },
    { id: 'kr.kdexp',       name: '경동택배' },
    { id: 'kr.cvsnet',      name: 'GS편의점택배' }
  ],
  jp: [
    { id: 'jp.yamato',      name: '야마토운수 (クロネコ)' },
    { id: 'jp.sagawa',      name: '사가와급편 (佐川急便)' },
    { id: 'jp.yupack',      name: '유팩 (ゆうパック)' },
    { id: 'jp.seino',       name: '세이노운수 (西濃運輸)' },
    { id: 'jp.fukuyama',    name: '후쿠야마통운 (福山通運)' },
    { id: 'jp.dhl',         name: 'DHL Japan' }
  ],
  cn: [
    { id: 'cn.sfexpress',   name: '순풍속운 (SF Express)' },
    { id: 'cn.sto',         name: '신통속운 (STO Express)' },
    { id: 'cn.yto',         name: '원통속운 (YTO Express)' },
    { id: 'cn.zto',         name: '중통속운 (ZTO Express)' },
    { id: 'cn.yunda',       name: '운달속운 (Yunda Express)' },
    { id: 'cn.jd',          name: '징동물류 (JD Logistics)' },
    { id: 'cn.ems',         name: '중국우정 EMS' },
    { id: 'cn.amazon',      name: 'Amazon China' }
  ],
  tw: [
    { id: 'tw.sf',          name: '순풍속운 TW (SF Express)' },
    { id: 'tw.tcat',        name: '흑묘택배 (黑貓宅急便)' },
    { id: 'tw.post',        name: '중화우정 (中華郵政)' },
    { id: 'tw.pelican',     name: '펠리컨 (宅配通)' }
  ],
  us: [
    { id: 'us.ups',         name: 'UPS' },
    { id: 'us.fedex',       name: 'FedEx' },
    { id: 'us.usps',        name: 'USPS' },
    { id: 'us.amazon',      name: 'Amazon Logistics' },
    { id: 'us.dhl',         name: 'DHL USA' }
  ],
  other: [
    { id: 'un.upu.ems',     name: '국제EMS' },
    { id: 'global.dhl',     name: 'DHL Global' },
    { id: 'global.fedex',   name: 'FedEx International' },
    { id: 'global.ups',     name: 'UPS International' },
    { id: 'sg.speedpost',   name: '싱가포르 SpeedPost' },
    { id: 'th.thaipost',    name: '태국 Thai Post' },
    { id: 'vn.vnpost',      name: '베트남 VN Post' }
  ]
};

var COUNTRY_FLAG = { kr:'🇰🇷', jp:'🇯🇵', cn:'🇨🇳', tw:'🇹🇼', us:'🇺🇸', other:'🌐' };
var COUNTRY_NAME = { kr:'한국', jp:'일본', cn:'중국', tw:'대만', us:'미국', other:'기타' };

var TRACK_HINT = {
  kr: '10~14자리 숫자',
  jp: '야마토: 12자리 숫자 / 사가와: 11자리 / 유팩: 13자리',
  cn: '12~15자리 숫자 또는 영문+숫자',
  tw: '10~14자리 영문+숫자',
  us: 'UPS: 1Z로 시작 18자리 / FedEx: 12~22자리 / USPS: 20~22자리',
  other: '택배사별 형식으로 입력하세요'
};

// 국가 변경 시 택배사 목록 업데이트
function updateCarriers() {
  var country = document.getElementById('inputCountry').value;
  var sel = document.getElementById('inputCarrier');
  var list = CARRIERS[country] || [];
  sel.innerHTML = list.map(function(c) {
    return '<option value="' + c.id + '">' + c.name + '</option>';
  }).join('');
  document.getElementById('trackHint').textContent = '운송장 형식: ' + (TRACK_HINT[country] || '');
}

// 추적 URL 생성 (carrier tracker)
function trackUrl(carrierId, trackNum) {
  var base = 'https://tracker.delivery/#/' + carrierId + '/' + trackNum;
  return base;
}

function stepsHtml(s) {
  var n = s === 'before' ? 0 : s === 'during' ? 1 : 2;
  var d = function(i) { return '<div class="sdot' + (i <= n ? ' on' : '') + '"></div>'; };
  var l = function(i) { return '<div class="sline' + (i < n ? ' on' : '') + '"></div>'; };
  return '<div class="steps">' + d(0) + l(0) + d(1) + l(1) + d(2) + '</div>';
}

function renderCard(o) {
  var s = o.status || 'before';
  var metaParts = [];
  if (o.nick) metaParts.push(esc(o.nick));
  if (o.seller) metaParts.push('판매처: ' + esc(o.seller));
  var country = o.country || 'kr';
  var flag = COUNTRY_FLAG[country] || '🌐';
  var cname = COUNTRY_NAME[country] || country;
  metaParts.push(flag + ' ' + cname);
  var carrierList = CARRIERS[country] || [];
  var carrierObj = carrierList.find(function(c){ return c.id === o.carrier; });
  var carrierName = carrierObj ? carrierObj.name : (o.carrier || '');
  if (carrierName) metaParts.push(carrierName);
  var meta = metaParts.length ? '<div class="ometa">' + metaParts.join(' · ') + '</div>' : '<div style="height:4px;"></div>';

  var isOwner = myNick && o.nick === myNick;

  // 상태 변경 버튼 (본인 것만)
  var statusBtns = '';
  if (isOwner) {
    var btns = [
      { key: 'before', label: '배송 전' },
      { key: 'during', label: '배송 중' },
      { key: 'done',   label: '배송 완료' }
    ].map(function(b) {
      var active = s === b.key ? ' ssbtn-active' : '';
      return '<button class="ssbtn' + active + '" onclick="setStatus(\'' + o.id + '\',\'' + b.key + '\')">' + b.label + '</button>';
    }).join('');
    statusBtns = '<div class="ssbtn-group">' + btns + '</div>';
  }

  var del = isOwner
    ? '<button class="delbtn" onclick="deleteOrder(\'' + o.id + '\')" title="삭제">×</button>' : '';

  return '<div class="ocard" id="card-' + o.id + '">' +
    '<div class="oi">' +
      '<div class="oname">' + esc(o.name) + '</div>' +
      meta +
      stepsHtml(s) +
      statusBtns +
    '</div>' +
    '<span class="pill ' + PILL[s] + '">' + LABEL[s] + '</span>' +
    del +
    '</div>';
}

function renderList() {
  document.getElementById('cntBadge').textContent = orders.length;
  var el = document.getElementById('orderList');
  if (!orders.length) {
    el.innerHTML = '<div class="empty"><div class="empty-ic">📭</div>아직 등록된 송장이 없어요</div>';
    return;
  }
  el.innerHTML = orders.map(renderCard).join('');
}

async function fetchStatus(trackNum, carrier) {
  // tracker.delivery API는 브라우저 CORS 정책으로 직접 호출 불가
  // Firebase에 저장된 status를 그대로 사용
  return null; // null = 변경 없음
}

async function refreshAll() {
  if (!orders.length) return;
  var now = new Date();
  document.getElementById('roomSub').textContent =
    '마지막 업데이트: ' + now.getHours() + ':' + String(now.getMinutes()).padStart(2, '0');
  renderList();
}

async function setStatus(id, newStatus) {
  try {
    await db.collection('rooms').doc(currentRoom.id).collection('orders').doc(id).update({ status: newStatus });
    var idx = orders.findIndex(function(o){ return o.id === id; });
    if (idx !== -1) {
      orders[idx] = Object.assign({}, orders[idx], { status: newStatus });
      renderList();
      toast('상태가 변경됐어요!');
    }
  } catch(e) { toast('변경 중 오류가 발생했어요'); }
}

async function addOrder() {
  if (!myNick) { toast('닉네임을 먼저 설정해주세요'); return; }
  var name    = document.getElementById('inputName').value.trim();
  var seller  = document.getElementById('inputSeller').value.trim();
  var track   = document.getElementById('inputTrack').value.trim().replace(/\s/g, '');
  var country = document.getElementById('inputCountry').value;
  var carrier = document.getElementById('inputCarrier').value;

  if (!name) { toast('주문 이름을 입력해주세요'); return; }
  if (!track) { toast('운송장 번호를 입력해주세요'); return; }
  if (track.length < 5) { toast('운송장 번호를 확인해주세요'); return; }

  try {
    var doc = await db.collection('rooms').doc(currentRoom.id).collection('orders').add({
      name: name, seller: seller, trackNum: track,
      country: country, carrier: carrier,
      nick: myNick, status: 'before',
      createdAt: firebase.firestore.FieldValue.serverTimestamp()
    });
    document.getElementById('inputName').value = '';
    document.getElementById('inputSeller').value = '';
    document.getElementById('inputTrack').value = '';

    var o = { id: doc.id, name: name, seller: seller, trackNum: track, country: country, carrier: carrier, nick: myNick, status: 'before' };
    orders.unshift(o);
    renderList();
    toast('추가됐어요!');
  } catch(e) { toast('오류가 발생했어요'); }
}

async function deleteOrder(id) {
  if (!confirm('내 송장을 삭제할까요?')) return;
  try {
    await db.collection('rooms').doc(currentRoom.id).collection('orders').doc(id).delete();
    orders = orders.filter(function(o) { return o.id !== id; });
    renderList();
    toast('삭제됐어요');
  } catch(e) { toast('삭제 중 오류가 발생했어요'); }
}

function showErr(id, msg) {
  var e = document.getElementById(id);
  e.textContent = msg; e.style.display = 'block';
}
function esc(s) {
  return String(s || '').replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
}
function toast(msg) {
  var el = document.getElementById('toast');
  el.textContent = msg;
  el.classList.add('show');
  setTimeout(function() { el.classList.remove('show'); }, 2300);
}

init();

// 초기 택배사 목록 힌트 표시 (addSection이 열릴 때를 위해)
document.addEventListener('DOMContentLoaded', function() {
  if (document.getElementById('inputCountry')) updateCarriers();
});
</script>
</body>
</html>
