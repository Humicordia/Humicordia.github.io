# Humicordia.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
    <title>每日打卡</title>
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='90' font-size='90'>📋</text></svg>">
    <style>
        *, *::before, *::after {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            --bg: #f2f5fa;
            --bg-grad: radial-gradient(1200px 600px at 50% -200px, #e3ecff 0%, rgba(227,236,255,0) 70%);
            --card: #ffffff;
            --text: #1c2434;
            --muted: #8a93a6;
            --line: #e8ecf3;
            --accent: #4c7dff;
            --green: #23c17a;
            --red: #f2555a;
            --orange: #f5a623;
            --shadow: 0 1px 2px rgba(20,30,60,.04), 0 10px 26px -14px rgba(20,30,60,.22);
            --radius: 16px;
            --dot-miss: #cfd5e0;
            --dot-future: #e8ecf3;
            --panel: #f2f5fa;

            --font-calligraphy:
                "STXingkai", "华文行楷",
                "FZXingKai-S04S", "方正行楷简体", "方正行楷_GBK",
                "HYXingKaiJ", "汉仪行楷简", "汉仪行楷",
                "STKaiti", "华文楷体", "KaiTi", "楷体", "Kaiti SC",
                -apple-system, BlinkMacSystemFont, "Segoe UI",
                "PingFang SC", "Hiragino Sans GB",
                "Microsoft YaHei", sans-serif;

            --font-digit:
                ui-monospace, "SF Mono", "Menlo", "Consolas", "Roboto Mono",
                -apple-system, BlinkMacSystemFont, "PingFang SC",
                "Microsoft YaHei", sans-serif;
        }

        @media (prefers-color-scheme: dark) {
            :root {
                --bg: #0f131b;
                --bg-grad: radial-gradient(1200px 600px at 50% -200px, #1a2540 0%, rgba(26,37,64,0) 70%);
                --card: #171c26;
                --text: #e9eef7;
                --muted: #8b94a7;
                --line: #252c39;
                --accent: #5b86ff;
                --green: #2fce87;
                --red: #ff6b70;
                --orange: #f5b942;
                --shadow: 0 1px 2px rgba(0,0,0,.3), 0 10px 26px -14px rgba(0,0,0,.7);
                --dot-miss: #3a4356;
                --dot-future: #252c39;
                --panel: #10151d;
            }
        }

        html, body { height: 100%; }

        body {
            margin: 0;
            background-color: var(--bg);
            background-image: var(--bg-grad);
            background-repeat: no-repeat;
            color: var(--text);
            font-family: var(--font-calligraphy);
            font-size: 16px;
            -webkit-font-smoothing: antialiased;
            text-rendering: optimizeLegibility;
        }

        .app { max-width: 600px; margin: 0 auto; padding: 30px 18px 110px; }

        .header-top {
            display: flex; align-items: center; justify-content: space-between;
            gap: 12px; margin-bottom: 18px;
        }
        h1 { margin: 0; font-size: 30px; font-weight: 700; letter-spacing: .02em; }

        .date-chip {
            display: inline-flex; align-items: center; gap: 5px;
            font-size: 14px; color: var(--muted); font-weight: 500;
            white-space: nowrap; cursor: pointer;
            padding: 7px 11px; border-radius: 10px;
            border: 1.5px solid transparent; background: transparent;
            font-family: inherit; line-height: 1.2;
            transition: background .2s, color .2s, border-color .2s, transform .12s;
        }
        .date-chip:hover { color: var(--text); background: var(--card); border-color: var(--line); }
        .date-chip:active { transform: scale(.97); }
        .chip-arrow { font-size: 9px; opacity: .65; line-height: 1; }

        .tip-notice { font-size: 13px; color: var(--muted); margin: 0 4px 14px; line-height: 1.7; }

        .progress-card {
            background: var(--card); border-radius: var(--radius);
            padding: 17px 18px; box-shadow: var(--shadow); margin-bottom: 16px;
        }
        .progress-track { height: 8px; background: var(--line); border-radius: 99px; overflow: hidden; }
        .progress-fill {
            height: 100%; width: 0; border-radius: 99px;
            background: linear-gradient(90deg, #4c7dff, #23c17a);
            transition: width .45s cubic-bezier(.4,0,.2,1);
        }
        .progress-label { margin-top: 11px; font-size: 14px; color: var(--muted); }
        .progress-label strong {
            font-family: var(--font-digit); color: var(--text);
            font-size: 16px; font-weight: 700;
        }

        .toolbar { display: flex; gap: 10px; margin-bottom: 14px; }

        .btn {
            appearance: none; border: none; font: inherit;
            font-family: var(--font-calligraphy); font-size: 15px; font-weight: 500;
            padding: 10px 16px; border-radius: 12px; cursor: pointer;
            background: var(--card); color: var(--text); box-shadow: var(--shadow);
            transition: transform .12s ease, background .2s, color .2s, opacity .2s;
        }
        .btn:hover { filter: brightness(1.04); }
        .btn:active { transform: scale(.96); }
        .btn.primary { background: var(--accent); color: #fff; }
        .btn.danger { background: var(--red); color: #fff; }
        .btn.ghost { background: transparent; box-shadow: none; color: var(--muted); }
        .btn.ghost:hover { color: var(--text); background-color: var(--line); }
        .btn.sm { padding: 7px 13px; font-size: 14px; border-radius: 10px; }

        .select-bar {
            display: flex; align-items: center; gap: 12px;
            background: var(--card); border-radius: 12px; padding: 10px 14px;
            margin-bottom: 14px; box-shadow: var(--shadow); font-size: 14px;
            animation: popIn .2s ease;
        }
        .select-bar label { display: flex; align-items: center; gap: 6px; cursor: pointer; user-select: none; }
        .select-bar .count { flex: 1; color: var(--muted); text-align: right; }
        input[type="checkbox"] { width: 16px; height: 16px; accent-color: var(--accent); cursor: pointer; }

        .plan-list { list-style: none; margin: 0; padding: 0; display: flex; flex-direction: column; gap: 10px; }

        .plan {
            display: flex; align-items: center; gap: 14px;
            background: var(--card); border-radius: var(--radius);
            padding: 14px 16px; box-shadow: var(--shadow);
            cursor: pointer; user-select: none;
            transition: transform .15s ease, outline-color .2s, opacity .2s;
            outline: 2px solid transparent;
        }
        .plan:active { transform: scale(.99); }
        .plan.selected { outline-color: var(--accent); }
        .plan.locked { opacity: .58; }
        .plan.locked .check { cursor: not-allowed; }

        .check {
            flex: 0 0 auto; width: 30px; height: 30px; padding: 0; border-radius: 50%;
            border: 2px solid var(--line); background: transparent; color: #fff;
            font-family: var(--font-digit); font-size: 15px; line-height: 1;
            display: grid; place-items: center; cursor: pointer;
            transition: background .22s, border-color .22s, color .22s;
        }
        .check.on { background: var(--green); border-color: var(--green); }
        .check.partial {
            background: rgba(35,193,122,.18); border-color: var(--green); color: var(--green);
        }
        .check.multi { font-size: 12px; font-weight: 700; font-variant-numeric: tabular-nums; }
        .check.multi.on { font-size: 15px; }
        .check.pop { animation: pop .38s cubic-bezier(.3,1.6,.5,1); }

        .checkbox {
            flex: 0 0 auto; width: 22px; height: 22px; border-radius: 50%;
            border: 2px solid var(--line); display: grid; place-items: center;
            font-size: 12px; color: transparent;
            transition: background .2s, border-color .2s, color .2s;
        }
        .checkbox.on { background: var(--accent); border-color: var(--accent); color: #fff; }

        .plan-info { flex: 1; min-width: 0; }
        .name-row { display: flex; align-items: center; gap: 8px; }
        .plan-name {
            flex: 1; min-width: 0; font-size: 18px; font-weight: 500; line-height: 1.4;
            overflow: hidden; text-overflow: ellipsis; white-space: nowrap;
            transition: color .2s;
        }
        .plan.done .plan-name { color: var(--muted); text-decoration: line-through; }

        .count-badge {
            flex: 0 0 auto; font-family: var(--font-digit);
            font-size: 12px; font-weight: 700; padding: 2px 9px; border-radius: 99px;
            background: var(--line); color: var(--muted);
            font-variant-numeric: tabular-nums; letter-spacing: .02em;
            transition: background .2s, color .2s;
        }
        .count-badge.done { background: rgba(35,193,122,.16); color: var(--green); }
        /* 超额完成 —— 橙色徽章，突出显示 */
        .count-badge.over {
            background: rgba(245,166,35,.18);
            color: var(--orange);
        }

        .plan-meta { font-size: 13px; color: var(--muted); margin-top: 4px; line-height: 1.6; }

        .tag {
            display: inline-block; padding: 1px 7px; border-radius: 6px;
            font-size: 12px; margin-right: 2px; vertical-align: 1px;
        }
        .tag.wait { background: rgba(76,125,255,.12); color: var(--accent); }
        .tag.over { background: rgba(138,147,166,.16); color: var(--muted); }

        .del-btn {
            flex: 0 0 auto; width: 32px; height: 32px; border-radius: 9px;
            border: none; background: transparent; color: var(--muted);
            font-size: 15px; font-family: inherit; cursor: pointer;
            opacity: .55;
            display: grid; place-items: center;
            transition: opacity .18s, background .18s, color .18s;
        }
        .plan:hover .del-btn { opacity: 1; }
        .del-btn:hover { background: var(--line); color: var(--red); }

        .empty {
            text-align: center; padding: 54px 20px;
            color: var(--muted); font-size: 15px; line-height: 1.9;
        }
        .empty .big { font-size: 40px; margin-bottom: 10px; opacity: .65; }

        /* ---------- 弹窗 ---------- */
        .overlay {
            position: fixed; inset: 0; z-index: 100;
            background: rgba(15,20,35,.45);
            -webkit-backdrop-filter: blur(4px); backdrop-filter: blur(4px);
            display: flex; align-items: flex-start; justify-content: center;
            padding: 20px; overflow-y: auto;
            animation: fadeIn .18s ease;
        }
        .modal {
            background: var(--card); border-radius: 20px; padding: 22px;
            width: 100%; max-width: 420px; margin: auto;
            box-shadow: 0 26px 60px -22px rgba(10,20,40,.5);
            animation: popIn .22s cubic-bezier(.2,.9,.3,1.15);
        }
        .modal h2 { margin: 0 0 6px; font-size: 21px; font-weight: 700; letter-spacing: .02em; }
        .modal .hint { margin: 0 0 14px; font-size: 14px; color: var(--muted); line-height: 1.7; }

        textarea {
            width: 100%; min-height: 158px; resize: vertical;
            border-radius: 13px; border: 1.5px solid var(--line); background: transparent;
            color: var(--text); font-family: var(--font-calligraphy);
            font-size: 16px; line-height: 1.9; padding: 12px 14px;
            outline: none; transition: border-color .2s;
        }
        textarea:focus { border-color: var(--accent); }
        textarea::placeholder { color: var(--muted); opacity: .7; }

        input.modal-input {
            width: 100%; min-width: 0; border-radius: 13px;
            border: 1.5px solid var(--line); background: transparent;
            color: var(--text); font-family: var(--font-calligraphy);
            font-size: 16px; padding: 11px 14px;
            outline: none; transition: border-color .2s;
        }
        input.modal-input:focus { border-color: var(--accent); }

        input[type="date"].modal-input,
        input[type="number"].modal-input {
            font-family: var(--font-digit); font-size: 15px;
        }
        input[type="date"].modal-input { color-scheme: light; }
        @media (prefers-color-scheme: dark) {
            input[type="date"].modal-input { color-scheme: dark; }
        }

        .field-label {
            display: block; font-size: 13px; font-weight: 600;
            color: var(--muted); margin: 14px 0 6px; letter-spacing: .02em;
        }
        .date-row { display: flex; gap: 10px; }
        .date-row > div { flex: 1; min-width: 0; }

        .goal-row { display: flex; align-items: center; gap: 10px; }
        .goal-row input { width: 110px; text-align: center; font-weight: 700; font-size: 17px; }
        .goal-presets { display: flex; gap: 6px; flex-wrap: wrap; }
        .goal-presets .btn {
            padding: 6px 11px; font-size: 13px; border-radius: 8px;
            box-shadow: none; border: 1.5px solid var(--line);
        }

        .quick-row { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 14px; }
        .quick-row .btn { box-shadow: none; border: 1.5px solid var(--line); }

        .modal-actions { display: flex; justify-content: flex-end; gap: 10px; margin-top: 16px; }

        .menu-item {
            display: block; width: 100%; text-align: left;
            padding: 13px 14px; border: none; background: transparent; color: var(--text);
            font-family: var(--font-calligraphy); font-size: 15px;
            border-radius: 12px; cursor: pointer; transition: background .15s;
        }
        .menu-item:hover { background: var(--line); }
        .menu-item.danger { color: var(--red); }

        /* ---------- 日历 ---------- */
        .cal-header {
            display: flex; align-items: center; justify-content: space-between;
            margin: 6px 0 14px; gap: 8px;
        }
        .cal-title {
            font-family: var(--font-digit); font-size: 17px; font-weight: 700;
            font-variant-numeric: tabular-nums; letter-spacing: .01em;
        }
        .cal-nav {
            width: 36px; height: 36px; flex: 0 0 auto; border-radius: 10px;
            border: 1.5px solid var(--line); background: transparent; color: var(--text);
            font-size: 17px; font-family: inherit; line-height: 1; cursor: pointer;
            display: grid; place-items: center; padding: 0;
            transition: background .15s, border-color .15s;
        }
        .cal-nav:hover { background: var(--line); }

        .cal-weekdays {
            display: grid; grid-template-columns: repeat(7, 1fr);
            gap: 3px; text-align: center; font-size: 13px;
            color: var(--muted); margin-bottom: 6px; font-weight: 600;
        }
        .cal-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 3px; }

        .cal-day {
            position: relative; aspect-ratio: 1 / 1; border: none;
            background: transparent; border-radius: 10px; color: var(--text);
            font-family: var(--font-digit); font-size: 13px; font-weight: 500;
            cursor: pointer; display: flex; flex-direction: column;
            align-items: center; justify-content: center; gap: 2px; padding: 0;
            transition: background .15s, box-shadow .15s;
            font-variant-numeric: tabular-nums;
        }
        .cal-day:hover { background: var(--line); }
        .cal-day.other { visibility: hidden; pointer-events: none; }
        .cal-day.today { box-shadow: inset 0 0 0 1.5px var(--accent); }
        .cal-day.selected { background: var(--accent); color: #fff; box-shadow: none; }

        .cal-dot {
            width: 5px; height: 5px; border-radius: 50%;
            flex: 0 0 auto; background: var(--green); transition: background .15s;
        }
        .cal-dot.partial { background: var(--orange); }
        .cal-dot.miss    { background: var(--dot-miss); }
        .cal-dot.future  { background: var(--dot-future); }

        .cal-day.selected .cal-dot         { background: rgba(255,255,255,.95); }
        .cal-day.selected .cal-dot.partial { background: rgba(255,255,255,.7); }
        .cal-day.selected .cal-dot.miss,
        .cal-day.selected .cal-dot.future  { background: rgba(255,255,255,.35); }

        .cal-detail { margin-top: 16px; border-top: 1px solid var(--line); padding-top: 14px; }
        .cal-detail-title { font-size: 16px; font-weight: 700; margin-bottom: 8px; }
        .cal-summary { font-size: 13px; color: var(--muted); margin-bottom: 10px; }
        .cal-list {
            list-style: none; margin: 0; padding: 0;
            display: flex; flex-direction: column; gap: 6px;
            max-height: 190px; overflow-y: auto;
        }
        .cal-list li {
            display: flex; align-items: center; gap: 10px;
            padding: 9px 12px; background: var(--panel);
            border-radius: 10px; font-size: 15px;
        }
        .cal-plan-name {
            flex: 1; min-width: 0; overflow: hidden;
            text-overflow: ellipsis; white-space: nowrap;
        }
        .cal-status {
            flex: 0 0 auto; font-family: var(--font-digit);
            font-size: 12px; font-weight: 700;
            font-variant-numeric: tabular-nums; color: var(--muted);
        }
        .cal-status.ok   { color: var(--green); }
        .cal-status.part { color: var(--orange); }
        .cal-status.miss { color: var(--muted); }
        .cal-status.over { color: var(--orange); }

        .cal-empty { text-align: center; color: var(--muted); font-size: 14px; padding: 18px 0; }

        /* ---------- 确认弹窗 ---------- */
        .confirm-msg {
            font-size: 15px; line-height: 1.7; color: var(--text);
            word-break: break-word;
        }
        .confirm-msg b { color: var(--accent); }

        .toast {
            position: fixed; left: 50%; bottom: 34px; z-index: 200;
            transform: translate(-50%, 16px);
            background: rgba(28,36,52,.94); color: #fff;
            padding: 10px 20px; border-radius: 99px;
            font-size: 14px; font-family: var(--font-calligraphy);
            white-space: nowrap; opacity: 0; pointer-events: none;
            transition: opacity .25s ease, transform .25s ease;
        }
        .toast.show { opacity: 1; transform: translate(-50%, 0); }

        [hidden] { display: none !important; }

        @keyframes popIn  {
            from { opacity: 0; transform: scale(.94) translateY(8px); }
            to   { opacity: 1; transform: none; }
        }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes pop {
            0%   { transform: scale(1); }
            45%  { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>

<div class="app">
    <header class="header-top">
        <h1>每日打卡</h1>
        <button class="date-chip" id="dateChip" type="button">
            <span id="dateChipText"></span>
            <span class="chip-arrow">▾</span>
        </button>
    </header>

    <div class="tip-notice">💡 点击右上角日期查看打卡日历 · 点击圆圈无上限累加 · 长按圆圈清零今日进度 · 数据在本地，请定期备份</div>

    <section class="progress-card">
        <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
        <div class="progress-label" id="progressLabel">加载中…</div>
    </section>

    <div class="toolbar" id="toolbar">
        <button class="btn primary" id="addBtn">+ 批量添加</button>
        <button class="btn" id="selectBtn">批量删除</button>
        <button class="btn ghost" id="moreBtn">⋯</button>
    </div>

    <div class="select-bar" id="selectBar" hidden>
        <label><input type="checkbox" id="selectAllChk"> 全选</label>
        <span class="count" id="selectCount">已选 0 项</span>
        <button class="btn danger sm" id="deleteSelectedBtn">删除</button>
        <button class="btn ghost sm" id="cancelSelectBtn">取消</button>
    </div>

    <ul class="plan-list" id="planList"></ul>

    <div class="empty" id="empty" hidden>
        <div class="big">🗓️</div>
        <div>还没有计划</div>
        <div style="font-size:14px;">点击上方「+ 批量添加」，开启你的打卡之旅</div>
    </div>
</div>

<div class="overlay" id="overlay" hidden>

    <!-- 批量添加 -->
    <div class="modal" id="addModal" hidden>
        <h2>批量添加计划</h2>
        <p class="hint">每行一个计划，支持一次粘贴多条（重复的会自动跳过）<br>添加后点击计划文字即可设置起止日期与每日目标次数。</p>
        <textarea id="bulkInput" placeholder="早起&#10;运动30分钟&#10;喝水&#10;阅读20页"></textarea>
        <div class="modal-actions">
            <button class="btn ghost" data-close>取消</button>
            <button class="btn primary" id="confirmAddBtn">添加</button>
        </div>
    </div>

    <!-- 编辑计划 -->
    <div class="modal" id="editModal" hidden>
        <h2>编辑计划</h2>
        <p class="hint">修改名称、起止日期与每日目标次数，日期留空表示不限制时间。<br>目标次数只决定何时算作「完成」，实际点击次数无上限。</p>

        <label class="field-label" for="editInput">计划名称</label>
        <input class="modal-input" id="editInput" placeholder="输入计划名称">

        <div class="date-row">
            <div>
                <label class="field-label" for="editStart">开始日期</label>
                <input type="date" class="modal-input" id="editStart">
            </div>
            <div>
                <label class="field-label" for="editEnd">结束日期</label>
                <input type="date" class="modal-input" id="editEnd">
            </div>
        </div>

        <div class="quick-row">
            <button class="btn ghost sm" data-preset="today">今天开始</button>
            <button class="btn ghost sm" data-preset="week">7天周期</button>
            <button class="btn ghost sm" data-preset="month">30天周期</button>
            <button class="btn ghost sm" data-preset="clear">清除日期</button>
        </div>

        <label class="field-label" for="editGoal">每日目标次数（如喝水8杯，就填 8）</label>
        <div class="goal-row">
            <input type="number" class="modal-input" id="editGoal" min="1" max="99" step="1" value="1" inputmode="numeric">
            <div class="goal-presets">
                <button class="btn ghost sm" data-goal="1">1次</button>
                <button class="btn ghost sm" data-goal="3">3次</button>
                <button class="btn ghost sm" data-goal="5">5次</button>
                <button class="btn ghost sm" data-goal="8">8次</button>
            </div>
        </div>

        <div class="modal-actions">
            <button class="btn ghost" data-close>取消</button>
            <button class="btn primary" id="confirmEditBtn">保存</button>
        </div>
    </div>

    <!-- 打卡日历 -->
    <div class="modal" id="calendarModal" hidden>
        <h2>打卡日历</h2>
        <p class="hint">绿点=全部完成 · 橙点=部分完成 · 灰点=未完成 · 空心=未来</p>

        <div class="cal-header">
            <button class="cal-nav" id="calPrev" type="button" title="上个月">‹</button>
            <span class="cal-title" id="calTitle"></span>
            <button class="cal-nav" id="calNext" type="button" title="下个月">›</button>
        </div>

        <div class="cal-weekdays">
            <span>日</span><span>一</span><span>二</span><span>三</span>
            <span>四</span><span>五</span><span>六</span>
        </div>

        <div class="cal-grid" id="calGrid"></div>

        <div class="cal-detail" id="calDetail"></div>

        <div class="modal-actions" style="justify-content: space-between;">
            <button class="btn ghost sm" id="calToday" type="button">回到今天</button>
            <button class="btn ghost" data-close type="button">关闭</button>
        </div>
    </div>

    <!-- 确认弹窗 -->
    <div class="modal" id="confirmModal" hidden>
        <h2 id="confirmTitle">确认操作</h2>
        <div class="confirm-msg" id="confirmMsg"></div>
        <div class="modal-actions">
            <button class="btn ghost" id="confirmNo" type="button">取消</button>
            <button class="btn danger" id="confirmYes" type="button">确定</button>
        </div>
    </div>

    <!-- 更多 -->
    <div class="modal" id="menuModal" hidden>
        <h2>更多</h2>
        <p class="hint">数据保存在本机浏览器，清理缓存数据会丢失，请做好备份。</p>
        <button class="menu-item" id="exportBtn">📤 导出数据（JSON备份）</button>
        <button class="menu-item" id="importBtn">📥 导入备份文件</button>
        <button class="menu-item" id="cleanBtn">🧹 清理 1 年前的旧记录</button>
        <button class="menu-item danger" id="clearBtn">🗑 清空全部计划</button>
        <div class="modal-actions">
            <button class="btn ghost" data-close>关闭</button>
        </div>
        <input type="file" id="fileInput" accept="application/json,.json" hidden>
    </div>

</div>

<div class="toast" id="toast"></div>

<script>
(function () {
    'use strict';

    const STORAGE_KEY = 'daily-checkin-v1';
    const $ = function (s) { return document.querySelector(s); };

    const state = { plans: [] };
    let selectMode = false;
    const selected = new Set();
    let lastDay = '';
    let editingPlanId = null;
    let toastTimer = null;

    // 长按清零
    let pressTimer = null;
    let lastLongPressAt = 0;

    // 日历
    let calYear = 0;
    let calMonth = 0;
    let calSelectedKey = '';

    // 确认弹窗回调
    let confirmCallback = null;

    // ====================工具函数====================
    function pad(n) { return String(n).padStart(2, '0'); }
    function toKey(d) { return d.getFullYear() + '-' + pad(d.getMonth() + 1) + '-' + pad(d.getDate()); }
    function today() { return toKey(new Date()); }

    function shiftKey(key, delta) {
        const p = key.split('-').map(Number);
        const d = new Date(p[0], p[1] - 1, p[2]);
        d.setDate(d.getDate() + delta);
        return toKey(d);
    }

    function weekdayText(key) {
        const p = key.split('-').map(Number);
        return '周' + '日一二三四五六'[new Date(p[0], p[1] - 1, p[2]).getDay()];
    }

    function uid() {
        return Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
    }

    function escapeHTML(s) {
        return String(s).replace(/[&<>"']/g, function (c) {
            return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c];
        });
    }

    function normDate(v) {
        if (typeof v !== 'string') return null;
        const s = v.trim();
        return /^\d{4}-\d{2}-\d{2}$/.test(s) ? s : null;
    }

    function fmtShort(key) {
        if (!key) return '';
        const p = key.split('-').map(Number);
        const y = new Date().getFullYear();
        return (p[0] !== y ? p[0] + '年' : '') + p[1] + '月' + p[2] + '日';
    }

    function rangeText(plan) {
        if (!plan.start && !plan.end) return '长期有效';
        if (plan.start && plan.end) return fmtShort(plan.start) + ' ~ ' + fmtShort(plan.end);
        if (plan.start) return fmtShort(plan.start) + ' 起';
        return '至 ' + fmtShort(plan.end);
    }

    function planStatus(plan, t) {
        if (plan.start && t < plan.start) return 'before';
        if (plan.end && t > plan.end) return 'after';
        return 'active';
    }

    function normGoal(v) {
        let g = parseInt(v, 10);
        if (!g || g < 1) g = 1;
        if (g > 99) g = 99;
        return g;
    }

    function normRecords(rec) {
        const out = {};
        if (!rec || typeof rec !== 'object') return out;
        for (const k in rec) {
            if (!/^\d{4}-\d{2}-\d{2}$/.test(k)) continue;
            const v = rec[k];
            if (v === true) out[k] = 1;
            else if (typeof v === 'number' && v > 0) out[k] = Math.round(v);
            else if (v) out[k] = 1;
        }
        return out;
    }

    // ====================数据处理====================
    function normalizePlan(p) {
        return {
            id: p.id || uid(),
            name: String(p.name || '未命名'),
            start: normDate(p.start),
            end: normDate(p.end),
            goal: normGoal(p.goal),
            records: normRecords(p.records)
        };
    }

    function loadData() {
        try {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) return;
            const data = JSON.parse(raw);
            if (data && Array.isArray(data.plans)) {
                state.plans = data.plans.map(normalizePlan);
            }
        } catch (e) { console.warn('读取数据失败：', e); }
    }

    // 保存数据：失败时自动清理 1 年前记录重试
    function saveData() {
        try {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
            return true;
        } catch (e) {
            console.warn('保存失败，尝试清理旧记录：', e);
            const cutoff = shiftKey(today(), -365);
            let cleaned = 0;
            state.plans.forEach(function (p) {
                const nr = {};
                for (const k in p.records) {
                    if (k >= cutoff) nr[k] = p.records[k];
                    else cleaned++;
                }
                p.records = nr;
            });
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
                if (cleaned > 0) {
                    toast('⚠️存储紧张，已自动清理 ' + cleaned + ' 条旧记录');
                    render();
                }
                return true;
            } catch (e2) {
                console.warn('清理后仍无法保存：', e2);
                toast('⚠️本地存储已满，请在「更多」中导出备份后清理数据');
                return false;
            }
        }
    }

    function isDayDone(plan, dateKey) {
        const goal = plan.goal || 1;
        return (plan.records[dateKey] || 0) >= goal;
    }

    function getStreak(plan) {
        let cur = isDayDone(plan, today()) ? today() : shiftKey(today(), -1);
        let streak = 0;
        while (isDayDone(plan, cur) && streak < 3000) {
            streak++;
            cur = shiftKey(cur, -1);
        }
        return streak;
    }

    function totalOf(plan) { return Object.keys(plan.records).length; }

    // ====================渲染====================
    function planHTML(plan, t) {
        const goal = plan.goal || 1;
        const count = plan.records[t] || 0;
        const done = count >= goal;
        const over = count > goal;
        const sel = selected.has(plan.id);
        const status = planStatus(plan, t);
        const locked = status !== 'active';

        const streak = getStreak(plan);
        const total = totalOf(plan);

        let meta = '📅 ' + rangeText(plan) + ' · ';
        meta += (streak > 0 ? '🔥连续 ' + streak + ' 天 · ' : '');
        meta += '累计 ' + total + ' 天';

        let tag = '';
        if (status === 'before') tag = ' <span class="tag wait">未开始</span>';
        else if (status === 'after') tag = ' <span class="tag over">已结束</span>';

        let cls = 'plan';
        if (done) cls += ' done';
        if (sel) cls += ' selected';
        if (locked) cls += ' locked';

        let checkHTML;
        if (selectMode) {
            checkHTML = '<span class="checkbox' + (sel ? ' on' : '') + '">✓</span>';
        } else {
            let ccls = 'check';
            let ctext = '';
            if (done) { ccls += ' on'; ctext = '✓'; }
            else if (count > 0) { ccls += ' partial'; ctext = String(count); }
            if (goal > 1) ccls += ' multi';
            checkHTML = '<button class="' + ccls + '" tabindex="-1">' + ctext + '</button>';
        }

        // ★ 核心修复：只要计数 > 1（无论目标多少），都显示次数徽章，让用户看到累加
        let badgeHTML = '';
        if (goal > 1 || count > 1) {
            badgeHTML = '<span class="count-badge' + (done ? ' done' : '') + (over ? ' over' : '') + '">' +
                        count + '/' + goal + '</span>';
        }

        return '<li class="' + cls + '" data-id="' + plan.id + '">' +
            checkHTML +
            '<div class="plan-info">' +
                '<div class="name-row">' +
                    '<div class="plan-name">' + escapeHTML(plan.name) + '</div>' +
                    badgeHTML +
                '</div>' +
                '<div class="plan-meta">' + meta + tag + '</div>' +
            '</div>' +
            (selectMode ? '' : '<button class="del-btn" type="button" title="删除">✕</button>') +
        '</li>';
    }

    function render() {
        const t = today();
        const plans = state.plans;

        const activePlans = plans.filter(p => planStatus(p, t) === 'active');
        const doneCount = activePlans.filter(p => isDayDone(p, t)).length;

        const now = new Date();
        $('#dateChipText').textContent = `${now.getMonth() + 1}月${now.getDate()}日 · ${weekdayText(t)}`;

        let pct = 0;
        if (!plans.length) {
            $('#progressLabel').textContent = '还没有计划，点击「批量添加」开始吧';
        } else if (!activePlans.length) {
            $('#progressLabel').innerHTML = `今日没有进行中的计划（共 ${plans.length} 项）`;
        } else {
            pct = (doneCount / activePlans.length) * 100;
            const allDone = doneCount === activePlans.length;
            $('#progressLabel').innerHTML = `今日完成 <strong>${doneCount}</strong> / ${activePlans.length}${allDone ? '　🎉 全部达成！' : ''}`;
        }
        $('#progressFill').style.width = pct + '%';

        $('#toolbar').hidden = selectMode;
        $('#selectBar').hidden = !selectMode;
        if (selectMode) {
            const allSel = plans.length > 0 && selected.size === plans.length;
            $('#selectCount').textContent = '已选 ' + selected.size + ' 项';
            $('#selectAllChk').checked = allSel;
            $('#selectAllChk').indeterminate = selected.size > 0 && !allSel;
        }

        $('#planList').innerHTML = plans.map(p => planHTML(p, t)).join('');
        $('#empty').hidden = plans.length > 0;
    }

    // ====================打卡（点击无上限累加）====================
    function toggleCheck(plan) {
        const t = today();
        const status = planStatus(plan, t);
        if (status === 'before') { toast(`计划 ${fmtShort(plan.start)} 才开始`); return; }
        if (status === 'after') { toast(`计划已于 ${fmtShort(plan.end)} 结束`); return; }

        const goal = plan.goal || 1;
        const cur = plan.records[t] || 0;
        const next = cur + 1;

        // ★ 无论目标多少，始终累加，永不清零
        plan.records[t] = next;
        saveData();
        render();

        const el = document.querySelector(`.plan[data-id="${plan.id}"] .check`);
        if (el) el.classList.add('pop');

        if (goal > 1 && next === goal) {
            toast(`🎉「${plan.name}」今日 ${goal}/${goal} 完成！`);
        } else if (next > goal && next === goal + 1) {
            toast(`「${plan.name}」已超额，继续累计中…`);
        } else if (next > goal) {
            toast(`「${plan.name}」当前 ${next}/${goal}`);
        }
    }

    // ====================长按清零====================
    function resetToday(planId) {
        const plan = state.plans.find(p => p.id === planId);
        if (!plan) return;
        const t = today();
        if (plan.records[t]) {
            delete plan.records[t];
            saveData();
            render();
            toast(`「${plan.name}」今日进度已清零`);
        } else {
            toast(`「${plan.name}」今日暂无记录`);
        }
    }

    // ====================确认弹窗====================
    function showConfirm(title, msgHTML, onYes) {
        $('#confirmTitle').textContent = title;
        $('#confirmMsg').innerHTML = msgHTML;
        confirmCallback = onYes;
        openModal('confirmModal');
    }

    // ====================日历渲染====================
    function getDayStats(dateKey) {
        let total = 0, done = 0;
        for (let i = 0; i < state.plans.length; i++) {
            const p = state.plans[i];
            if (p.start && dateKey < p.start) continue;
            if (p.end && dateKey > p.end) continue;
            total++;
            if ((p.records[dateKey] || 0) >= (p.goal || 1)) done++;
        }
        return { total: total, done: done };
    }

    function renderCalendar() {
        const t = today();
        const year = calYear, month = calMonth;

        $('#calTitle').textContent = year + '年' + (month + 1) + '月';

        const startWeekday = new Date(year, month, 1).getDay();
        const daysInMonth = new Date(year, month + 1, 0).getDate();
        const prevMonthDays = new Date(year, month, 0).getDate();
        const trailing = (7 - ((startWeekday + daysInMonth) % 7)) % 7;

        let html = '';
        for (let i = 0; i < startWeekday; i++) {
            const d = prevMonthDays - startWeekday + 1 + i;
            html += '<button class="cal-day other" disabled tabindex="-1">' + d + '</button>';
        }

        for (let d = 1; d <= daysInMonth; d++) {
            const key = year + '-' + pad(month + 1) + '-' + pad(d);
            const stats = getDayStats(key);
            const isToday = key === t;
            const isSel = key === calSelectedKey;
            const isFuture = key > t;

            let dotCls = '';
            if (stats.total > 0) {
                if (isFuture) dotCls = 'future';
                else if (stats.done === stats.total) dotCls = '';
                else if (stats.done > 0) dotCls = 'partial';
                else dotCls = 'miss';
            }

            let cls = 'cal-day';
            if (isToday) cls += ' today';
            if (isSel) cls += ' selected';

            html += '<button class="' + cls + '" data-key="' + key + '" type="button">' +
                '<span>' + d + '</span>' +
                (stats.total > 0 ? '<span class="cal-dot ' + dotCls + '"></span>' : '') +
            '</button>';
        }

        for (let i = 1; i <= trailing; i++) {
            html += '<button class="cal-day other" disabled tabindex="-1">' + i + '</button>';
        }

        $('#calGrid').innerHTML = html;
        renderCalDetail();
    }

    function renderCalDetail() {
        const key = calSelectedKey;
        if (!key) {
            $('#calDetail').innerHTML = '<div class="cal-empty">点击上方日期查看当天完成情况</div>';
            return;
        }

        const p = key.split('-').map(Number);
        const dateObj = new Date(p[0], p[1] - 1, p[2]);
        const wd = '日一二三四五六'[dateObj.getDay()];
        const t = today();
        const isFuture = key > t;

        let title = fmtShort(key) + ' 周' + wd;
        if (key === t) title += ' · 今天';

        const items = [];
        for (let i = 0; i < state.plans.length; i++) {
            const plan = state.plans[i];
            if (plan.start && key < plan.start) continue;
            if (plan.end && key > plan.end) continue;
            const goal = plan.goal || 1;
            const count = plan.records[key] || 0;
            items.push({
                name: plan.name, goal: goal, count: count,
                done: count >= goal, over: count > goal, future: isFuture
            });
        }

        let body = '<div class="cal-detail-title">' + title + '</div>';

        if (!items.length) {
            body += '<div class="cal-empty">这一天没有进行中的计划</div>';
        } else {
            const doneCount = items.filter(function (x) { return x.done; }).length;
            body += '<div class="cal-summary">完成 ' + doneCount + ' / ' + items.length + ' 项</div>';
            body += '<ul class="cal-list">';
            items.forEach(function (it) {
                let text, cls;
                if (it.over) {
                    text = it.count + '/' + it.goal + ' ↑';
                    cls = 'over';
                } else if (it.done) {
                    text = it.goal > 1 ? (it.count + '/' + it.goal + ' ✓') : '✓ 已完成';
                    cls = 'ok';
                } else if (it.count > 0) {
                    text = it.count + '/' + it.goal;
                    cls = 'part';
                } else if (it.future) {
                    text = '待完成'; cls = '';
                } else {
                    text = '未完成'; cls = 'miss';
                }
                body += '<li>' +
                    '<span class="cal-plan-name">' + escapeHTML(it.name) + '</span>' +
                    '<span class="cal-status ' + cls + '">' + text + '</span>' +
                '</li>';
            });
            body += '</ul>';
        }

        $('#calDetail').innerHTML = body;
    }

    function openCalendar() {
        const t = today();
        const p = t.split('-').map(Number);
        calYear = p[0];
        calMonth = p[1] - 1;
        calSelectedKey = t;
        openModal('calendarModal');
        renderCalendar();
    }

    // ====================弹窗控制====================
    function openModal(id) {
        $('#overlay').hidden = false;
        ['addModal', 'menuModal', 'editModal', 'calendarModal', 'confirmModal'].forEach(function (mId) {
            document.getElementById(mId).hidden = (mId !== id);
        });
    }

    function closeModal() {
        $('#overlay').hidden = true;
        $('#bulkInput').value = '';
        editingPlanId = null;
        confirmCallback = null;
    }

    function toast(msg) {
        const el = $('#toast');
        clearTimeout(toastTimer);
        el.textContent = msg;
        el.classList.add('show');
        toastTimer = setTimeout(function () { el.classList.remove('show'); }, 1800);
    }

    // ====================删除操作====================
    function deletePlan(id) {
        const plan = state.plans.find(p => p.id === id);
        if (!plan) return;
        showConfirm(
            '删除计划',
            '确定要删除「<b>' + escapeHTML(plan.name) + '</b>」吗？<br>此操作不可恢复。',
            function () {
                state.plans = state.plans.filter(p => p.id !== id);
                saveData();
                render();
                toast('已删除');
            }
        );
    }

    // ====================事件：列表点击====================
    $('#planList').addEventListener('click', function (e) {
        if (Date.now() - lastLongPressAt < 400) return;

        // 删除按钮优先
        const delBtn = e.target.closest('.del-btn');
        if (delBtn) {
            e.preventDefault();
            e.stopPropagation();
            const li = delBtn.closest('.plan');
            if (li) deletePlan(li.dataset.id);
            return;
        }

        const li = e.target.closest('.plan');
        if (!li) return;
        const id = li.dataset.id;
        const plan = state.plans.find(p => p.id === id);
        if (!plan) return;

        if (selectMode) {
            if (selected.has(id)) selected.delete(id);
            else selected.add(id);
            render();
            return;
        }

        if (e.target.closest('.plan-info')) {
            editingPlanId = id;
            $('#editInput').value = plan.name;
            $('#editStart').value = plan.start || '';
            $('#editEnd').value = plan.end || '';
            $('#editGoal').value = plan.goal || 1;
            openModal('editModal');
            setTimeout(function () { $('#editInput').focus(); }, 60);
            return;
        }

        toggleCheck(plan);
    }, false);

    // 长按清零（只作用于打卡圆圈）
    $('#planList').addEventListener('pointerdown', function (e) {
        if (selectMode) return;
        const check = e.target.closest('.check');
        if (!check) return;
        const li = check.closest('.plan');
        if (!li) return;
        const planId = li.dataset.id;

        clearTimeout(pressTimer);
        pressTimer = setTimeout(function () {
            lastLongPressAt = Date.now();
            resetToday(planId);
            pressTimer = null;
        }, 600);
    });

    ['pointerup', 'pointercancel', 'pointerleave'].forEach(function (evt) {
        $('#planList').addEventListener(evt, function () {
            clearTimeout(pressTimer);
            pressTimer = null;
        });
    });

    $('#planList').addEventListener('contextmenu', function (e) {
        if (e.target.closest('.check')) e.preventDefault();
    });

    // ====================编辑保存====================
    $('#confirmEditBtn').addEventListener('click', function () {
        if (!editingPlanId) return;
        const newName = $('#editInput').value.trim();
        if (!newName) { toast('名称不能为空'); return; }

        const s = $('#editStart').value || null;
        const en = $('#editEnd').value || null;
        if (s && en && s > en) { toast('开始日期不能晚于结束日期'); return; }

        const goal = normGoal($('#editGoal').value);
        const p = state.plans.find(x => x.id === editingPlanId);
        if (p) {
            p.name = newName;
            p.start = s;
            p.end = en;
            p.goal = goal;
            saveData();
            render();
            toast('已保存');
        }
        closeModal();
    });

    document.querySelectorAll('[data-preset]').forEach(function (btn) {
        btn.addEventListener('click', function () {
            const t = today();
            const preset = this.dataset.preset;
            if (preset === 'clear') { $('#editStart').value = ''; $('#editEnd').value = ''; }
            else if (preset === 'today') { $('#editStart').value = t; $('#editEnd').value = ''; }
            else if (preset === 'week') { $('#editStart').value = t; $('#editEnd').value = shiftKey(t, 6); }
            else if (preset === 'month') { $('#editStart').value = t; $('#editEnd').value = shiftKey(t, 29); }
        });
    });

    document.querySelectorAll('[data-goal]').forEach(function (btn) {
        btn.addEventListener('click', function () { $('#editGoal').value = this.dataset.goal; });
    });

    $('#editInput').addEventListener('keydown', function (e) {
        if (e.key === 'Enter') { e.preventDefault(); $('#confirmEditBtn').click(); }
    });
    $('#editGoal').addEventListener('keydown', function (e) {
        if (e.key === 'Enter') { e.preventDefault(); $('#confirmEditBtn').click(); }
    });

    // 遮罩关闭
    $('#overlay').addEventListener('click', function (e) {
        if (e.target === $('#overlay')) closeModal();
    });
    document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape' && !$('#overlay').hidden) closeModal();
    });
    document.querySelectorAll('[data-close]').forEach(function (b) {
        b.addEventListener('click', closeModal);
    });

    // 确认弹窗按钮
    $('#confirmYes').addEventListener('click', function () {
        const cb = confirmCallback;
        confirmCallback = null;
        closeModal();
        if (cb) cb();
    });
    $('#confirmNo').addEventListener('click', function () {
        confirmCallback = null;
        closeModal();
    });

    // 日期按钮 → 日历
    $('#dateChip').addEventListener('click', openCalendar);

    $('#calPrev').addEventListener('click', function () {
        calMonth--;
        if (calMonth < 0) { calMonth = 11; calYear--; }
        renderCalendar();
    });
    $('#calNext').addEventListener('click', function () {
        calMonth++;
        if (calMonth > 11) { calMonth = 0; calYear++; }
        renderCalendar();
    });
    $('#calGrid').addEventListener('click', function (e) {
        const btn = e.target.closest('.cal-day');
        if (!btn || btn.disabled || !btn.dataset.key) return;
        calSelectedKey = btn.dataset.key;
        renderCalendar();
    });
    $('#calToday').addEventListener('click', function () {
        const t = today();
        const p = t.split('-').map(Number);
        calYear = p[0]; calMonth = p[1] - 1; calSelectedKey = t;
        renderCalendar();
    });

    // ====================批量添加====================
    $('#addBtn').addEventListener('click', function () {
        openModal('addModal');
        setTimeout(function () { $('#bulkInput').focus(); }, 60);
    });

    function doAdd() {
        const raw = $('#bulkInput').value;
        const lines = raw.split('\n').map(function (s) { return s.trim(); }).filter(Boolean);
        if (!lines.length) { closeModal(); return; }

        const existing = {};
        state.plans.forEach(function (p) { existing[p.name] = true; });
        let added = 0;
        lines.forEach(function (name) {
            if (existing[name]) return;
            existing[name] = true;
            state.plans.push({ id: uid(), name: name, start: null, end: null, goal: 1, records: {} });
            added += 1;
        });
        saveData();
        closeModal();
        render();
        toast(added ? `已添加 ${added} 个计划` : '没有新增（名称已存在）');
    }

    $('#confirmAddBtn').addEventListener('click', doAdd);
    $('#bulkInput').addEventListener('keydown', function (e) {
        if ((e.ctrlKey || e.metaKey) && e.key === 'Enter') { e.preventDefault(); doAdd(); }
    });

    // ====================批量删除====================
    $('#selectBtn').addEventListener('click', function () {
        selectMode = true;
        selected.clear();
        render();
    });

    $('#cancelSelectBtn').addEventListener('click', function () {
        selectMode = false;
        selected.clear();
        render();
    });

    $('#selectAllChk').addEventListener('change', function (e) {
        if (e.target.checked) state.plans.forEach(function (p) { selected.add(p.id); });
        else selected.clear();
        render();
    });

    $('#deleteSelectedBtn').addEventListener('click', function (e) {
        e.preventDefault();
        e.stopPropagation();
        if (!selected.size) { toast('请先选择要删除的计划'); return; }
        const count = selected.size;
        showConfirm(
            '批量删除',
            '确定要删除选中的 <b>' + count + '</b> 个计划吗？<br>此操作不可恢复。',
            function () {
                state.plans = state.plans.filter(function (p) { return !selected.has(p.id); });
                selected.clear();
                selectMode = false;
                saveData();
                render();
                toast('已删除 ' + count + ' 个计划');
            }
        );
    });

    // ====================更多菜单====================
    $('#moreBtn').addEventListener('click', function () { openModal('menuModal'); });

    $('#exportBtn').addEventListener('click', function () {
        const blob = new Blob([JSON.stringify(state, null, 2)], { type: 'application/json' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url;
        a.download = '打卡数据-' + today() + '.json';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        setTimeout(function () { URL.revokeObjectURL(url); }, 1000);
        toast('已导出');
    });

    $('#importBtn').addEventListener('click', function () { $('#fileInput').click(); });

    $('#fileInput').addEventListener('change', function (e) {
        const file = e.target.files && e.target.files[0];
        if (!file) return;
        const reader = new FileReader();
        reader.onload = function () {
            let data;
            try {
                data = JSON.parse(reader.result);
                if (!data || !Array.isArray(data.plans)) throw new Error('文件格式不正确');
            } catch (err) { alert('导入失败：' + err.message); return; }

            showConfirm(
                '导入数据',
                '导入将覆盖当前全部数据，确定继续？',
                function () {
                    state.plans = data.plans.map(normalizePlan);
                    saveData();
                    render();
                    toast('导入成功');
                }
            );
        };
        reader.readAsText(file);
        e.target.value = '';
    });

    // 清理 1 年前旧记录
    $('#cleanBtn').addEventListener('click', function () {
        const cutoff = shiftKey(today(), -365);
        let cleaned = 0;
        state.plans.forEach(function (p) {
            const nr = {};
            for (const k in p.records) {
                if (k >= cutoff) nr[k] = p.records[k];
                else cleaned++;
            }
            p.records = nr;
        });
        if (cleaned === 0) {
            toast('没有需要清理的旧记录');
            return;
        }
        showConfirm(
            '清理旧记录',
            '将删除 <b>' + cleaned + '</b> 条 1 年前的打卡记录，确定继续？',
            function () {
                saveData();
                render();
                toast('已清理 ' + cleaned + ' 条旧记录');
            }
        );
    });

    $('#clearBtn').addEventListener('click', function () {
        if (!state.plans.length) { toast('当前没有数据'); return; }
        showConfirm(
            '清空全部',
            '确定要清空全部计划和打卡记录？<br>此操作不可恢复。',
            function () {
                state.plans = [];
                selected.clear();
                selectMode = false;
                saveData();
                render();
                toast('已清空');
            }
        );
    });

    // ====================启动====================
    function init() {
        loadData();
        lastDay = today();
        render();

        setInterval(function () {
            const t = today();
            if (t !== lastDay) { lastDay = t; render(); }
        }, 30000);
    }

    init();
})();
</script>
</body>
</html>
