---
created: 2026-07-02T07:53:36+09:00
modified: 2026-07-03T15:06:59+09:00
---

# Generator

<!--
  Selfie Prompt Generator
  Version: 3.0.0-stable-character
  Updated: 2026-07-03
  Changelog:
    v2.2.0 - 表情の手動選択（⑦）を追加。未選択時は従来通りランダム
    v2.1.0 - エフェクト複数選択・テンション/感情の手動選択チップを追加
    v2.0.0 - Claude API依存を廃止、完全オフライン化（キーワード判定ロジック）
    v1.1.0 - モバイルコピー対応（execCommandフォールバック）、出力をtextarea化
    v1.0.0 - 初期版（React/JSXプロトタイプからHTML単体化）
-->
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
    <div class="header-title">Stable Character Prompt Generator</div>
    <div class="header-sub">固定キャラ + 今回のシーン v3</div>
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

  <!-- Character lock -->
  <div class="card card-dark">
    <div class="card-head">
      <div class="slabel" style="margin-bottom:0;">固定キャラ設定 — 毎回先頭に入る</div>
      <button class="btn-copy" onclick="resetCharacterLock()">初期化</button>
    </div>
    <div class="hint">顔・体型・透明感を固定。実在人物名は使わず、雰囲気だけを言語化。</div>
    <textarea id="characterLock" rows="8"></textarea>
  </div>

  <!-- ① Scene only -->
  <div class="card">
    <div class="slabel">① 今回のシーンだけ（日本語で入力）</div>
    <div class="hint">ここだけ毎回変更：場所・服装・ポーズ・表情・何してるか</div>
    <textarea id="situation" rows="4" placeholder="例：&#10;薄い紺色のワイシャツ、紺色のビジネスパンツ。西中島南方のラーメン店でラーメンをすすっている。"></textarea>
  </div>

  <!-- Body silhouette -->
  <div class="card">
    <div class="slabel">② 体型・胸シルエットの安定度</div>
    <div class="hint">露出強調ではなく、服の上からの自然な形として固定</div>
    <div class="chips" id="bustChips"></div>
  </div>

  <!-- Weather -->
  <div class="card">
    <div class="slabel">③ 天気を選択</div>
    <div class="chips" id="weatherChips"></div>
  </div>

  <!-- ④ Film tone -->
  <div class="card">
    <div class="slabel">④ フィルムトーン / 質感</div>
    <div class="chips" id="filmChips"></div>
  </div>

  <!-- ③ Overall tone -->
  <div class="card">
    <div class="slabel">⑤ 作品トーン</div>
    <div class="chips" id="toneChips"></div>
  </div>

  <!-- ④ Bokeh & Effects -->
  <div class="card">
    <div class="slabel">⑥ エフェクト（複数選択可）</div>
    <div class="chips" id="effectChips"></div>
  </div>

  <!-- ⑤ Tension -->
  <div class="card">
    <div class="slabel">⑦ テンション</div>
    <div class="chips" id="tensionChips"></div>
  </div>

  <!-- ⑥ Emotion -->
  <div class="card">
    <div class="slabel">⑧ 感情（モーション用）</div>
    <div class="chips" id="emotionChips"></div>
  </div>

  <!-- ⑦ Expression -->
  <div class="card">
    <div class="slabel">⑨ 表情</div>
    <div class="hint">未選択の場合はランダムで決定されます</div>
    <div class="chips" id="expressionChips"></div>
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

// ── Effects (multi-select) ────────────────────────────────────────────────────
const EFFECTS = [
  {label:"🌫️ 背景ボケ",     value:"(background bokeh blur:1.6), (shallow depth of field with soft defocused background:1.6)"},
  {label:"✨ 光の玉ボケ",    value:"(light orb bokeh:1.5), (ambient light circles in background:1.5), (specular bokeh highlights:1.5)"},
  {label:"💧 水滴/結露感",   value:"(condensation droplets on glass or skin:1.4), (subtle water droplet texture:1.4)"},
  {label:"✨ きらめき粒子",  value:"(sparkling glitter particles in air:1.4), (subtle shimmering light particles:1.4)"},
  {label:"🌁 ソフトフォーカス", value:"(soft focus haze:1.4), (gentle dreamy blur on edges:1.4), (diffused hazy atmosphere:1.4)"},
  {label:"🌙 逆光/リムライト", value:"(backlighting:1.5), (rim light on hair and shoulders:1.5), (silhouette-edge glow:1.4)"},
  {label:"📼 VHSノイズ",     value:"(subtle VHS scan lines:1.3), (retro analog video noise:1.3), (slight chromatic aberration:1.3)"},
  {label:"🔥 暖色フレア",    value:"(warm lens flare:1.4), (golden warm light flare streaks:1.4)"},
  {label:"❄️ 冷色フィルター", value:"(cool blue color grading:1.4), (cold tone filter:1.4)"},
  {label:"🌈 光漏れ",       value:"(light leak effect:1.4), (film light leak streaks across frame:1.4)"},
  {label:"🖤 ビネット",     value:"(vignette:1.4), (soft dark edge falloff around frame:1.4)"},
  {label:"🎞️ フィルムグレイン強め", value:"(heavy film grain:1.5), (pronounced analog grain texture:1.5)"},
];

// ── Tension options ────────────────────────────────────────────────────────────
const TENSIONS = [
  {label:"😌 低め（落ち着き）", value:"low"},
  {label:"🙂 普通",           value:"medium"},
  {label:"😄 やや高め",        value:"medium-high"},
  {label:"🤩 高め（元気）",    value:"high"},
];

// ── Emotion options ────────────────────────────────────────────────────────────
const EMOTIONS = [
  {label:"🍶 ほろ酔い",     value:"tipsy"},
  {label:"👯 社交的",       value:"social"},
  {label:"🌙 物思い/孤独",  value:"reflective"},
  {label:"😔 憂鬱/疲れ",    value:"melancholy"},
  {label:"☕ カジュアル",   value:"casual"},
  {label:"💖 自信/嬉しい",  value:"confident"},
  {label:"😐 ニュートラル", value:"neutral"},
];

// ── Expression options (manual override for EXPRESSIONS random pick) ──────────
const EXPRESSION_OPTIONS = [
  {label:"😐 真顔/クール",      value:"neutral deadpan, calm, composed expression"},
  {label:"🙂
