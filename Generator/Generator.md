---
created: 2026-07-02T07:53:36+09:00
modified: 2026-07-02T08:03:13+09:00
---

# Generator

<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Selfie Prompt Generator</title>
<style>
  /* ── CSS Variables: Dark (default) ── */
  :root {
    --bg:        #09090b;
    --bg-card:   #18181b;
    --bg-dark:   #0d0d14;
    --bg-out:    #0a0a0d;
    --bg-input:  #09090b;
    --bg-ta:     #06060a;
    --border:    #27272a;
    --border-m:  #3f3f46;
    --border-pu: #3b1d6b;
    --text:      #fafafa;
    --text-sub:  #a1a1aa;
    --text-dim:  #71717a;
    --text-hint: #52525b;
    --text-pu:   #c4b5fd;
    --chip-bg:   #18181b;
    --chip-col:  #a1a1aa;
    --chip-abg:  #581c87;
    --chip-acol: #f0e6ff;
    --chip-abdr: #c084fc;
    --tog-bg:    #18181b;
    --tog-col:   #71717a;
    --tog-abg:   #3b0764;
    --tog-acol:  #e9d5ff;
    --pill-off:  #3f3f46;
    --hdr-bg:    linear-gradient(135deg, #1e1b2e 0%, #0d0d14 100%);
    --reset-col: #71717a;
    --reset-bdr: #3f3f46;
    --info-val:  #c4b5fd;
    --copy-done-bg: #581c87;
    --copy-done-col: #e9d5ff;
    --placeholder: #3f3f46;
  }

  /* ── CSS Variables: Light ── */
  @media (prefers-color-scheme: light) {
    :root {
      --bg:        #f4f4f5;
      --bg-card:   #ffffff;
      --bg-dark:   #ede9fe;
      --bg-out:    #f8f7ff;
      --bg-input:  #f4f4f5;
      --bg-ta:     #f8f8f8;
      --border:    #e4e4e7;
      --border-m:  #d4d4d8;
      --border-pu: #c4b5fd;
      --text:      #18181b;
      --text-sub:  #52525b;
      --text-dim:  #71717a;
      --text-hint: #a1a1aa;
      --text-pu:   #7c3aed;
      --chip-bg:   #f4f4f5;
      --chip-col:  #52525b;
      --chip-abg:  #7c3aed;
      --chip-acol: #ffffff;
      --chip-abdr: #7c3aed;
      --tog-bg:    #f4f4f5;
      --tog-col:   #71717a;
      --tog-abg:   #ede9fe;
      --tog-acol:  #6d28d9;
      --pill-off:  #d4d4d8;
      --hdr-bg:    linear-gradient(135deg, #ede9fe 0%, #f5f3ff 100%);
      --reset-col: #71717a;
      --reset-bdr: #d4d4d8;
      --info-val:  #6d28d9;
      --copy-done-bg: #7c3aed;
      --copy-done-col: #ffffff;
      --placeholder: #d4d4d8;
    }
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Hiragino Kaku Gothic ProN', 'Noto Sans JP', sans-serif;
    padding-bottom: 80px;
    font-size: 14px;
  }
  .header {
    background: var(--hdr-bg);
    border-bottom: 1px solid var(--border);
    padding: 16px 14px 12px;
    position: sticky; top: 0; z-index: 10;
    display: flex; align-items: center; gap: 10px;
  }
  .header-icon {
    width: 30px; height: 30px; border-radius: 8px;
    background: linear-gradient(135deg, #7c3aed, #a855f7);
    display: flex; align-items: center; justify-content: center;
    font-size: 15px; flex-shrink: 0;
  }
  .header-title { font-size: 15px; font-weight: 700; }
  .header-sub { font-size: 10px; color: var(--text-hint); margin-top: 1px; }
  .header-time { margin-left: auto; text-align: right; }
  .header-time-main { font-size: 13px; color: #a855f7; font-weight: 700; }
  .header-time-sub { font-size: 10px; color: var(--text-hint); }

  .content { padding: 12px 14px 0; }

  .card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 14px; padding: 14px; margin-bottom: 10px;
  }
  .card-dark { background: var(--bg-dark); border-color: var(--border-pu); }
  .card-out  { background: var(--bg-out);  border-color: var(--border-pu); }

  .slabel {
    font-size: 10px; font-weight: 700; letter-spacing: 0.12em;
    color: var(--text-dim); text-transform: uppercase; margin-bottom: 8px;
  }

  .chips { display: flex; flex-wrap: wrap; gap: 6px; }
  .chip {
    padding: 7px 13px; border-radius: 20px;
    border: 2px solid var(--border-m);
    background: var(--chip-bg); color: var(--chip-col);
    font-size: 12px; cursor: pointer; transition: all 0.15s;
    -webkit-tap-highlight-color: transparent; user-select: none;
  }
  .chip.active {
    border-color: var(--chip-abdr);
    background: var(--chip-abg); color: var(--chip-acol); font-weight: 600;
  }

  .toggle-row { display: flex; gap: 10px; }
  .toggle-btn {
    display: flex; align-items: center; gap: 8px;
    padding: 9px 14px; border-radius: 10px; flex: 1;
    border: 2px solid var(--border-m);
    background: var(--tog-bg); color: var(--tog-col);
    font-size: 13px; cursor: pointer; transition: all 0.15s;
    -webkit-tap-highlight-color: transparent; user-select: none;
  }
  .toggle-btn.active {
    border-color: #7c3aed;
    background: var(--tog-abg); color: var(--tog-acol); font-weight: 600;
  }
  .toggle-pill {
    width: 34px; height: 18px; border-radius: 9px; flex-shrink: 0;
    background: var(--pill-off); position: relative; transition: background 0.2s;
  }
  .toggle-btn.active .toggle-pill { background: #a855f7; }
  .toggle-dot {
    position: absolute; top: 2px; left: 2px;
    width: 14px; height: 14px; border-radius: 50%;
    background: #fff; transition: left 0.2s;
  }
  .toggle-btn.active .toggle-dot { left: 18px; }

  textarea {
    width: 100%; background: var(--bg-input);
    border: 1px solid var(--border-m); border-radius: 10px;
    color: var(--text); font-size: 14px; line-height: 1.6;
    padding: 10px 12px; resize: vertical; outline: none; font-family: inherit;
  }
  textarea::placeholder { color: var(--placeholder); }

  .btn-row { display: flex; gap: 10px; margin: 6px 0 14px; }
  .btn-generate {
    flex: 3; padding: 14px 0; border-radius: 12px; border: none;
    background: linear-gradient(135deg, #7c3aed, #a855f7);
    color: #fff; font-size: 15px; font-weight: 700;
    cursor: pointer; letter-spacing: 0.03em;
    -webkit-tap-highlight-color: transparent;
  }
  .btn-generate:disabled { opacity: 0.7; }
  .btn-reset {
    flex: 1; padding: 14px 0; border-radius: 12px;
    border: 1px solid var(--reset-bdr); background: transparent;
    color: var(--reset-col); font-size: 14px; font-weight: 600;
    cursor: pointer; -webkit-tap-highlight-color: transparent;
  }
  .btn-copy {
    padding: 6px 14px; border-radius: 8px;
    border: 1px solid #7c3aed; background: transparent;
    color: #a855f7; font-size: 12px; font-weight: 600;
    cursor: pointer; transition: all 0.2s;
    -webkit-tap-highlight-color: transparent;
  }
  .btn-copy.copied {
    background: var(--copy-done-bg); color: var(--copy-done-col);
  }

  .output-ta {
    width: 100%; height: 260px;
    font-size: 11px; color: var(--text-sub); line-height: 1.8;
    font-family: monospace; background: var(--bg-ta);
    border-radius: 8px; padding: 10px 12px;
    border: 1px solid var(--border); resize: none; outline: none;
  }

  .info-row {
    display: flex; align-items: flex-start; gap: 8px;
    font-size: 12px; color: var(--text-sub); margin-bottom: 5px;
  }
  .info-icon { flex-shrink: 0; color: #7c3aed; }
  .info-val { color: var(--info-val); font-weight: 600; }

  .card-head {
    display: flex; justify-content: space-between;
    align-items: center; margin-bottom: 10px;
  }
  .hidden { display: none; }
  .hint { font-size: 11px; color: var(--text-hint); margin-bottom: 8px; }
</style>
</head>
<body>

<!-- Header -->
<div class="header">
  <div class="header-icon">✦</div>
  <div>
    <div class="header-title">Selfie Prompt Generator</div>
    <div class="header-sub">IMAGE OVERVIEW ビルダー v2</div>
  </div>
  <div class="header-time">
    <div class="header-time-main" id="hTime">--:--</div>
    <div class="header-time-sub" id="hDay">-- · --月 · --</div>
  </div>
</div>

<div class="content">

  <!-- Auto info -->
  <div class="card card-dark" id="autoInfo">
    <div class="slabel">自動取得 — 東京時間</div>
    <div class="info-row"><span class="info-icon">📅</span><span id="infoDay">取得中…</span></div>
    <div class="info-row"><span class="info-icon">🕐</span><span id="infoTime">取得中…</span></div>
    <div class="info-row"><span class="info-icon">💭</span><span id="infoDayMood" style="font-size:11px;color:#71717a;"></span></div>
    <div class="info-row"><span class="info-icon">✂️</span><span id="infoHair" style="font-size:11px;color:#71717a;"></span></div>
  </div>

  <!-- Weather -->
  <div class="card">
    <div class="slabel">天気を選択</div>
    <div class="chips" id="weatherChips"></div>
  </div>

  <!-- ① Situation -->
  <div class="card">
    <div class="slabel">① シチュエーション（日本語で入力）</div>
    <div class="hint">コーデ・何してるか・場所</div>
    <textarea id="situation" rows="4" placeholder="例：&#10;黒のニットワンピース、渋谷の居酒屋でひとり飲み"></textarea>
  </div>

  <!-- ② Film tone -->
  <div class="card">
    <div class="slabel">② フィルムトーン / 質感</div>
    <div class="chips" id="filmChips"></div>
  </div>

  <!-- ③ Overall tone -->
  <div class="card">
    <div class="slabel">③ 作品トーン</div>
    <div class="chips" id="toneChips"></div>
  </div>

  <!-- ④⑤ Bokeh -->
  <div class="card">
    <div class="slabel">④ ボケ設定</div>
    <div class="toggle-row">
      <button class="toggle-btn" id="toggleBg" onclick="toggleBokeh('bg')">
        <span class="toggle-pill"><span class="toggle-dot"></span></span>
        背景ボケ
      </button>
      <button class="toggle-btn" id="toggleLight" onclick="toggleBokeh('light')">
        <span class="toggle-pill"><span class="toggle-dot"></span></span>
        光の玉ボケ
      </button>
    </div>
  </div>

  <!-- Buttons -->
  <div class="btn-row">
    <button class="btn-generate" id="btnGen" onclick="handleGenerate()">✦ プロンプト生成</button>
    <button class="btn-reset" onclick="handleReset()">リセット</button>
  </div>

  <!-- Resolved meta -->
  <div class="card card-dark hidden" id="metaCard">
    <div class="slabel">展開結果サマリー</div>
    <div id="metaContent" style="font-size:12px;color:#a1a1aa;line-height:1.9;"></div>
  </div>

  <!-- Output -->
  <div class="card card-out hidden" id="outputCard">
    <div class="card-head">
      <div class="slabel" style="margin-bottom:0;">生成プロンプト</div>
      <button class="btn-copy" id="btnCopy" onclick="handleCopy()">コピー</button>
    </div>
    <textarea class="output-ta" id="outputArea" readonly
      onclick="this.select();this.setSelectionRange(0,this.value.length);"
      onfocus="this.select();this.setSelectionRange(0,this.value.length);"></textarea>
  </div>

</div>

<script>
// ── Data ─────────────────────────────────────────────────────────────────────
const HAIR_BY_MONTH = {
  1:"(long straight, dark brown hair:1.2)",
  2:"(long wave, dark brown to chestnut brown gradient hair:1.2)",
  3:"(long soft wave, chestnut brown hair:1.2)",
  4:"(medium straight, chestnut brown hair:1.2)",
  5:"(medium wave, light chestnut brown hair:1.2)",
  6:"(soft bob, ash brown hair:1.2)",
  7:"(airy bob, ash brown hair:1.2)",
  8:"(short bob, light ash brown hair:1.2)",
  9:"(medium bob, ash brown to dark brown hair:1.2)",
  10:"(inner-color straight, dark brown with caramel inner highlight:1.2)",
  11:"(inner-color wave, dark brown with rose-beige inner highlight:1.2)",
  12:"(long straight, dark brown with subtle inner highlight:1.2)",
};

const DAY_MOOD = {
  Sun:"Quiet reflective melancholy, gentle Sunday loneliness",
  Mon:"Tired but composed Monday composure",
  Tue:"Focused stable neutral Tuesday calm",
  Wed:"Midweek fatigue, quiet weariness",
  Thu:"Slightly excited pre-weekend anticipation",
  Fri:"High energy social drinking atmosphere, lively Friday night mood",
  Sat:"Relaxed confident outgoing Saturday energy",
};

const ANGLES = [
  {name:"SUPER HIGH ANGLE", prompt:"(camera extremely high above head, steep downward look:1.8), (arm fully extended upward:1.8), (bird's-eye framing of face and upper chest:1.8), (face tilted up toward camera:1.7)"},
  {name:"GOLDEN ANGLE",     prompt:"(camera above eye level looking down:1.9), (head-to-chest framing:1.8), (three-quarter facial view:1.8), (face 30-45 degrees from camera:1.8), (eyes looking slightly upward:1.8)"},
  {name:"HIGH ANGLE",       prompt:"(camera clearly above eye level:1.8), (head-to-chest framing:1.8), (head slightly tilted up:1.7), (eyes directed upward to lens:1.8)"},
  {name:"EYE LEVEL",        prompt:"(camera at eye height:1.9), (head-to-chest framing:1.8), (face angled 10-30 degrees:1.7), (relaxed everyday selfie:1.8), (minimal distortion:1.7)"},
  {name:"LOW ANGLE",        prompt:"(camera below chin level:1.8), (angled upward toward face:1.8), (face angled slightly down:1.7), (confident posture:1.7)"},
  {name:"SUPER LOW ANGLE",  prompt:"(camera significantly below face:1.7), (looking sharply upward:1.7), (dynamic perspective distortion:1.7)"},
  {name:"DYNAMIC TILTED",   prompt:"(camera slightly rotated:1.8), (diagonal composition:1.8), (face tilted with camera:1.7), (snapshot atmosphere:1.8)"},
  {name:"OVER SHOULDER",    prompt:"(face partially turned away:1.7), (looking back toward lens:1.8), (shoulder line emphasized:1.7), (candid feel:1.7)"},
  {name:"WALKING",          prompt:"(captured mid-walk:1.8), (subtle body motion:1.7), (hair movement from motion:1.7), (face turned slightly to camera:1.7)"},
];

const EXPRESSIONS = [
  "neutral deadpan, calm, composed expression",
  "soft gentle smile, warm and approachable expression",
  "bright happy, lively cheerful expression",
  "sweet, slightly clingy, affectionate expression",
  "cute charming, playful expression",
  "teasing, mischievous smirk expression",
  "melancholic, reflective, subtle loneliness in expression",
  "tired but gentle, quiet fatigue expression",
  "tipsy warm relaxed expression",
  "thoughtful faraway gaze expression",
  "shy blushing expression",
  "surprised slightly startled expression",
];

const ACCESSORIES_MAP = {
  "night out":"(gold earrings:1.5), (layered necklaces:1.5), (rings:1.5), (elegant night-out accessories:1.5)",
  "home":     "(minimal accessories or none:1.4), (no jewelry, casual home look:1.4)",
  "after work":"(subtle elegant jewelry:1.4), (delicate earrings:1.4), (refined after-work accessories:1.4)",
  "date":     "(soft feminine accessories:1.4), (delicate necklace:1.4), (romantic accessory styling:1.4)",
  "casual":   "(simple casual accessories:1.3), (minimal jewelry:1.3)",
};

const WEATHER_OPTIONS = [
  {label:"晴れ ☀️",  value:"clear sunny sky, bright natural daylight"},
  {label:"曇り ☁️",  value:"overcast cloudy sky, diffused soft light, muted atmosphere"},
  {label:"小雨 🌦️", value:"light drizzle rain, wet streets, soft grey ambient light, misty air"},
  {label:"雨 🌧️",   value:"steady rain, rain-soaked streets, dark moody wet atmosphere"},
  {label:"大雨 ⛈️", value:"heavy rain, dramatic downpour, dark stormy atmosphere"},
  {label:"雪 ❄️",   value:"snow falling, winter white scenery, cold crisp air, soft white light"},
  {label:"霧 🌫️",  value:"foggy misty atmosphere, dreamlike hazy soft light"},
];

const FILM_TONES = [
  {label:"なし",              value:""},
  {label:"コダック ゴールド 200", value:"Kodak Gold 200 film tone, warm golden cast, slightly elevated grain, vintage analog feel"},
  {label:"フジ プロ 400H",       value:"Fuji Pro 400H film tone, soft pastel palette, subtle cool shadows, natural skin tones"},
  {label:"コダック ポートラ 800", value:"Kodak Portra 800 film tone, rich warm skin, creamy highlights, visible film grain"},
  {label:"イルフォード HP5",      value:"Ilford HP5 black and white film, high contrast monochrome, classic grain texture"},
  {label:"シネスコープ",          value:"CinemaScope film tone, teal and orange grade, cinematic color grading, anamorphic feel"},
  {label:"ローモ",               value:"Lomography vivid tone, saturated cross-processed colors, vignette edges, lo-fi aesthetic"},
  {label:"ポラロイド",            value:"Polaroid instant film tone, faded soft colors, nostalgic warm cast"},
  {label:"ヴィンテージ 90s",      value:"1990s vintage film tone, slightly desaturated, muted warm mid-tones, retro color shift"},
];

const OVERALL_TONES = [
  {label:"なし",          value:""},
  {label:"クール / モダン",   value:"cool modern aesthetic, sharp clean composition, urban sophisticated mood"},
  {label:"キュート / 柔らか", value:"cute soft aesthetic, gentle pastel atmosphere, warm approachable mood"},
  {label:"ダーク / ムーディ", value:"dark moody aesthetic, deep shadows, brooding emotional atmosphere"},
  {label:"ナチュラル / 透明感",value:"natural transparent beauty aesthetic, fresh clean look, minimal mood"},
  {label:"エレガント / 上品", value:"elegant refined aesthetic, graceful composition, sophisticated atmosphere"},
  {label:"ストリート / エッジ",value:"street edge aesthetic, raw urban energy, gritty authentic mood"},
  {label:"ロマンティック",    value:"romantic dreamy aesthetic, soft warm glow, tender emotional atmosphere"},
  {label:"ミニマル / 静寂",   value:"minimal quiet aesthetic, negative space composition, serene calm mood"},
];

// ── State ─────────────────────────────────────────────────────────────────────
let state = {
  weather: "", film: "", tone: "",
  bgBokeh: false, lightBokeh: false,
};
let tokyoNow = {};

// ── Tokyo time ────────────────────────────────────────────────────────────────
function getTokyoNow() {
  const now = new Date();
  const jst = new Date(now.toLocaleString("en-US", { timeZone: "Asia/Tokyo" }));
  const days = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];
  const timeCtxList = [
    {h:[0,5],  label:"深夜", en:"late night",     mood:"melancholic quiet solitude, exhausted calm"},
    {h:[5,9],  label:"早朝", en:"early morning",  mood:"serene fresh morning calm, gentle awakening"},
    {h:[9,12], label:"午前", en:"late morning",   mood:"composed focused morning clarity"},
    {h:[12,14],label:"昼",   en:"noon",           mood:"bright casual midday energy"},
    {h:[14,17],label:"午後", en:"afternoon",      mood:"relaxed comfortable afternoon drift"},
    {h:[17,20],label:"夕方", en:"evening",        mood:"warm golden-hour nostalgia, gentle longing"},
    {h:[20,23],label:"夜",   en:"night",          mood:"intimate night warmth, social or quiet reflection"},
    {h:[23,24],label:"深夜", en:"midnight",       mood:"deep night solitude, tender melancholy"},
  ];
  const hour = jst.getHours();
  const timeCtx = timeCtxList.find(t => hour >= t.h[0] && hour < t.h[1]) || timeCtxList[0];
  return {
    month: jst.getMonth() + 1,
    day: days[jst.getDay()],
    hour,
    minute: jst.getMinutes(),
    timeStr: jst.toLocaleTimeString("ja-JP", {hour:"2-digit", minute:"2-digit"}),
    timeCtx,
  };
}

function detectScene(text) {
  const t = text;
  if (/家|自宅|部屋|home|apartment|room/.test(t)) return "home";
  if (/デート|date/.test(t)) return "date";
  if (/仕事帰り|退勤|after work|office/.test(t)) return "after work";
  if (/居酒屋|バー|飲み|izakaya|bar|pub|drink|club|夜遊び/.test(t)) return "night out";
  return "casual";
}

// ── Update clock ──────────────────────────────────────────────────────────────
function updateClock() {
  tokyoNow = getTokyoNow();
  document.getElementById("hTime").textContent = tokyoNow.timeStr + " JST";
  document.getElementById("hDay").textContent = tokyoNow.day + " · " + tokyoNow.month + "月 · " + tokyoNow.timeCtx.label;
  document.getElementById("infoDay").innerHTML = "<span class='info-val'>" + tokyoNow.day + " / " + tokyoNow.month + "月 / " + tokyoNow.timeCtx.label + "（" + tokyoNow.timeCtx.en + "）</span>";
  document.getElementById("infoTime").innerHTML = "<span class='info-val'>" + tokyoNow.timeStr + " JST</span>";
  document.getElementById("infoDayMood").textContent = DAY_MOOD[tokyoNow.day];
  document.getElementById("infoHair").textContent = HAIR_BY_MONTH[tokyoNow.month];
}

// ── Render chip groups ────────────────────────────────────────────────────────
function renderChips(containerId, items, stateKey) {
  const el = document.getElementById(containerId);
  el.innerHTML = "";
  items.forEach((item, i) => {
    const btn = document.createElement("button");
    btn.className = "chip" + (state[stateKey] === item.value ? " active" : "");
    btn.textContent = item.label;
    btn.onclick = () => {
      state[stateKey] = (state[stateKey] === item.value) ? "" : item.value;
      renderChips(containerId, items, stateKey);
    };
    el.appendChild(btn);
  });
}

function toggleBokeh(type) {
  if (type === "bg") {
    state.bgBokeh = !state.bgBokeh;
    document.getElementById("toggleBg").classList.toggle("active", state.bgBokeh);
  } else {
    state.lightBokeh = !state.lightBokeh;
    document.getElementById("toggleLight").classList.toggle("active", state.lightBokeh);
  }
}

// ── Claude API: resolve motion ────────────────────────────────────────────────
function resolveMotion(situation, dayMood, timeCtx) {
  const t = situation + " " + dayMood + " " + timeCtx.mood;

  // ── Detect emotion ──────────────────────────────────────────────────────────
  let emotion = "neutral";
  if (/飲み|居酒屋|バー|酔|飲ん|tipsy|social|飲み会|ビール|ワイン|乾杯/.test(t))
    emotion = "tipsy";
  else if (/友達|友人|みんな|パーティ|飲み会|social|遊び/.test(t))
    emotion = "social";
  else if (/ひとり|一人|孤独|lonely|寂し|reflective|物思い|夜|深夜/.test(t))
    emotion = "reflective";
  else if (/悲し|憂鬱|melancholy|疲れ|しんど|疲労|憂い/.test(t))
    emotion = "melancholy";
  else if (/散歩|歩く|カフェ|コーヒー|のんびり|casual|リラックス|休日/.test(t))
    emotion = "casual";
  else if (/仕事|残業|会社|office|デスク|tired|疲/.test(t))
    emotion = "melancholy";
  else if (/デート|彼|ときめき|嬉し|楽し|happy|confident|自信/.test(t))
    emotion = "confident";

  // ── Detect tension ──────────────────────────────────────────────────────────
  let tension = "medium";
  if (/深夜|ひとり|一人|孤独|静か|quiet|calm|家|自宅|部屋|眠/.test(t))
    tension = "low";
  else if (/走|急|hurry|energetic|excited|興奮|はしゃ|元気|パーティ|踊/.test(t))
    tension = "high";
  else if (/飲み|バー|居酒屋|友達|集まり|social|にぎや/.test(t))
    tension = "medium-high";

  // ── Build motion text ───────────────────────────────────────────────────────
  let base = "";
  if (tension === "low")
    base = "slow movement, breathing motion, minimal tilt, micro-movements";
  else if (tension === "medium")
    base = "gentle lean, head tilt, arm shift, soft hair";
  else
    base = "walking, turning, playful tilt, energetic arm movement, hair swaying";

  let extra = "";
  if (emotion === "reflective" || emotion === "lonely" || emotion === "melancholy")
    extra = "slow blink, downward gaze, soft angle";
  else if (emotion === "confident" || emotion === "casual")
    extra = "hip shift, relaxed shoulder, natural stride";
  else if (emotion === "tipsy" || emotion === "social")
    extra = "loose arm, playful tilt, relaxed posture";

  return extra ? base + ", " + extra : base;
}

// ── Build prompt ──────────────────────────────────────────────────────────────
function buildPrompt(t, situation, weatherVal, filmVal, toneVal, bgBokeh, lightBokeh, angle, expression, scene, accessories, motionText) {
  const weatherLabel = WEATHER_OPTIONS.find(w => w.value === weatherVal)?.label || "";
  const overviewParts = [];
  if (situation.trim()) overviewParts.push(situation.trim());
  overviewParts.push("current time: " + t.timeCtx.label + " (" + t.timeCtx.en + "), " + t.timeStr + " JST");
  overviewParts.push("day: " + t.day + " — " + DAY_MOOD[t.day]);
  if (weatherVal) overviewParts.push("weather: " + weatherVal);
  overviewParts.push("time-of-day mood: " + t.timeCtx.mood);
  if (filmVal) overviewParts.push(filmVal);
  if (toneVal) overviewParts.push(toneVal);
  if (bgBokeh) overviewParts.push("(background bokeh blur:1.6), (shallow depth of field with soft defocused background:1.6)");
  if (lightBokeh) overviewParts.push("(light orb bokeh:1.5), (ambient light circles in background:1.5), (specular bokeh highlights:1.5)");

  return `============================================================
VARIABLE EXPANSION MODE v3.2 — FULLY EXPANDED
============================================================
All variables resolved. Apply directly.
============================================================
RESOLVED VARIABLES
============================================================
[DAY]   = ${t.day}
[MONTH] = ${t.month}
[TIME]  = ${t.timeCtx.label} / ${t.timeCtx.en} (${t.timeStr} JST)
============================================================
[IMAGE OVERVIEW] — ABSOLUTE PRIORITY
============================================================
${overviewParts.join(", ")}
* Clothing instructions above override all defaults.
============================================================
REALITY
============================================================
(no anime:1.9), (no illustration:1.9), (no plastic skin:1.9), (no waxy skin:1.9),
(no beauty filters:1.8), (photographic realism only:1.9),
(real skin texture with pores and micro-details:1.9),
(realistic lighting and shadows:1.8), (real-world imperfections:1.7)
============================================================
ENVIRONMENT
============================================================
(real Japanese locations:1.8),
(real izakaya, bars, streets, apartments, trains, cafés:1.8),
(realistic crowd and posture:1.7), (realistic tableware, signage, furniture:1.7),
(authentic ambient lighting:1.7), (no fantasy elements:1.8)
============================================================
ASPECT
============================================================
(aspect ratio 9:16:1.6), (vertical smartphone framing:1.6)
============================================================
CAMERA
============================================================
(smartphone in her hand IS the active camera:1.9),
(viewpoint MUST match her held smartphone:1.9),
(only ONE smartphone in scene:1.9)
============================================================
SELFIE POV
============================================================
(POV smartphone front-camera selfie:1.8), (arm's-length distance:1.7),
(random left hand or right hand holding the phone:1.9),
(natural wide-angle selfie distortion:1.6),
(camera is ALWAYS her held smartphone:1.9),
(viewpoint ALWAYS from her hand-held front camera:1.9),
(no third-person shots:1.9), (no external camera angles:1.9),
(natural arm extension consistent with selfie:1.8),
(perspective MUST reflect handheld selfie:1.9)
============================================================
ANGLE — RESOLVED: [${angle.name}]
============================================================
${angle.prompt}
============================================================
EXPRESSION & MOOD — RESOLVED
============================================================
(context-driven emotional expression:1.9),
(emotion and expression strongly reflects the situation, time, weather, and atmosphere:1.9),
(${expression}:1.9),
(day mood: ${DAY_MOOD[t.day]}:1.7),
(time-of-day atmosphere: ${t.timeCtx.mood}:1.7),
(natural micro-expressions and subtle changes according to situation:1.7)
============================================================
MOTION — RESOLVED
============================================================
(${motionText}:1.7)
============================================================
CHARACTER
============================================================
(24-year-old woman:1.4), (corporate secretary:1.3),
(has boyfriend but values personal time:1.3),
(social with many friends, enjoys drinking parties:1.3),
(loves drinking alone at home or bars:1.4),
(quiet nights drinking alone, self-reflecting:1.4),
(gentle, emotionally deep, slightly introverted:1.4),
(fragile beauty with subtle melancholy:1.5),
(soft transparent slightly lonely aura:1.4),
(strikingly pale fair porcelain skin:1.8),
(elegant sorrow and delicate vulnerability:1.5)
============================================================
FACE IDENTITY
============================================================
(refined East-Asian actress face exactly in the style of Ko Yoon-jung:1.9),
(translucent elegant beauty like Ko Yoon-jung:1.9),
(extremely fair porcelain complexion like Ko Yoon-jung:1.9),
(consistent facial identity:1.9), (stable refined proportions:1.7),
(soft rounded jawline:1.6), (natural almond-shaped eyes with emotional depth:1.6),
(balanced nose and lips:1.6), (intelligent calm atmosphere:1.7)
============================================================
BODY
============================================================
(slender I-line silhouette with long lean vertical proportions:1.6),
(narrow waist smooth body flow:1.5), (refined fashion-model proportions:1.5),
(realistic anatomy:1.8), (no exaggerated glamour proportions:1.7),
(naturally large breasts with realistic volume and gravity-consistent shape:1.9),
(enhanced fullness without push-up or cleavage emphasis:1.8),
(soft three-dimensional contour visible through fabric only:1.8),
(no explicit anatomy:1.9), (no sexual expression:1.9)
============================================================
NECKLINE & COMPOSITION
============================================================
(beautiful neck-to-collarbone line composition:1.8),
(elegant deep-V or wide open neckline:1.6),
(face is primary visual focal point:1.9),
(face > neck > collarbone > upper silhouette hierarchy:1.9),
(no cleavage-centered or chest-focused composition:1.9)
============================================================
ACCESSORIES — RESOLVED: [${scene.toUpperCase()}]
============================================================
${accessories}
============================================================
HAIR — RESOLVED: [MONTH ${t.month}]
============================================================
${HAIR_BY_MONTH[t.month]}
============================================================
LIGHTING & SMARTPHONE
============================================================
(realistic ambient lighting from actual fixtures:1.7),
(real smartphone rendering:1.8), (natural grain in low light:1.6),
(realistic HDR:1.5), (authentic color temperature:1.6),
(realistic depth of field:1.6), (hand-held micro shake:1.5)
============================================================`;
}

// ── Generate ──────────────────────────────────────────────────────────────────
function handleGenerate() {
  const situation = document.getElementById("situation").value;
  const btn = document.getElementById("btnGen");
  btn.disabled = true;
  btn.innerHTML = "⏳ 生成中…";

  const t = getTokyoNow();
  tokyoNow = t;
  updateClock();

  const scene = detectScene(situation);
  const accessories = ACCESSORIES_MAP[scene];
  const angle = ANGLES[Math.floor(Math.random() * ANGLES.length)];
  const expression = EXPRESSIONS[Math.floor(Math.random() * EXPRESSIONS.length)];

  const motionText = resolveMotion(situation, DAY_MOOD[t.day], t.timeCtx);

  const prompt = buildPrompt(t, situation, state.weather, state.film, state.tone, state.bgBokeh, state.lightBokeh, angle, expression, scene, accessories, motionText);

  // Show meta
  document.getElementById("metaCard").classList.remove("hidden");
  document.getElementById("metaContent").innerHTML =
    "🕐 <b style='color:#c4b5fd'>時間帯</b>：" + t.timeCtx.label + " / " + t.timeCtx.en + "<br>" +
    "📅 <b style='color:#c4b5fd'>曜日 mood</b>：" + DAY_MOOD[t.day] + "<br>" +
    "✂️ <b style='color:#c4b5fd'>ヘア</b>：" + HAIR_BY_MONTH[t.month] + "<br>" +
    "📸 <b style='color:#c4b5fd'>アングル</b>：" + angle.name + "<br>" +
    "😊 <b style='color:#c4b5fd'>表情</b>：" + expression + "<br>" +
    "👜 <b style='color:#c4b5fd'>アクセ</b>：" + scene + "<br>" +
    "🎬 <b style='color:#c4b5fd'>モーション</b>：" + motionText;

  // Show output
  document.getElementById("outputCard").classList.remove("hidden");
  document.getElementById("outputArea").value = prompt;

  btn.disabled = false;
  btn.innerHTML = "✦ プロンプト生成";

  // Scroll to output
  document.getElementById("outputCard").scrollIntoView({ behavior: "smooth" });
}

// ── Copy ──────────────────────────────────────────────────────────────────────
function handleCopy() {
  const ta = document.getElementById("outputArea");
  ta.focus();
  ta.select();
  ta.setSelectionRange(0, ta.value.length);

  let success = false;
  if (navigator.clipboard && navigator.clipboard.writeText) {
    navigator.clipboard.writeText(ta.value).then(() => showCopied()).catch(() => fallbackCopy(ta));
  } else {
    fallbackCopy(ta);
  }
}

function fallbackCopy(ta) {
  try {
    document.execCommand("copy");
    showCopied();
  } catch {
    alert("コピーできませんでした。テキストエリアを長押しして「すべてを選択」→「コピー」してください。");
  }
}

function showCopied() {
  const btn = document.getElementById("btnCopy");
  btn.textContent = "✓ コピー済み";
  btn.classList.add("copied");
  setTimeout(() => {
    btn.textContent = "コピー";
    btn.classList.remove("copied");
  }, 2500);
}

// ── Reset ─────────────────────────────────────────────────────────────────────
function handleReset() {
  document.getElementById("situation").value = "";
  state = { weather:"", film:"", tone:"", bgBokeh:false, lightBokeh:false };
  document.getElementById("toggleBg").classList.remove("active");
  document.getElementById("toggleLight").classList.remove("active");
  document.getElementById("metaCard").classList.add("hidden");
  document.getElementById("outputCard").classList.add("hidden");
  document.getElementById("outputArea").value = "";
  renderChips("weatherChips", WEATHER_OPTIONS, "weather");
  renderChips("filmChips", FILM_TONES, "film");
  renderChips("toneChips", OVERALL_TONES, "tone");
}

// ── Init ──────────────────────────────────────────────────────────────────────
updateClock();
setInterval(updateClock, 30000);
renderChips("weatherChips", WEATHER_OPTIONS, "weather");
renderChips("filmChips", FILM_TONES, "film");
renderChips("toneChips", OVERALL_TONES, "tone");
</script>
</body>
</html>
