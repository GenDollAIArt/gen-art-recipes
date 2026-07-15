<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Stable Character Prompt Generator v8.0.1</title>
<style>
:root{
  --bg:#f4f4f5;--card:#fff;--soft:#ede9fe;--out:#f8f7ff;--input:#f4f4f5;
  --border:#e4e4e7;--border2:#d4d4d8;--purple:#7c3aed;--purple2:#a855f7;
  --text:#18181b;--sub:#52525b;--dim:#71717a;--hint:#a1a1aa;
}
*{box-sizing:border-box;margin:0;padding:0}
body{background:var(--bg);color:var(--text);font-family:'Hiragino Kaku Gothic ProN','Noto Sans JP',sans-serif;padding-bottom:80px;font-size:14px}
.header{background:linear-gradient(135deg,#ede9fe,#f5f3ff);border-bottom:1px solid var(--border);padding:16px 14px 12px;position:sticky;top:0;z-index:10;display:flex;align-items:center;gap:10px}
.header-icon{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,var(--purple),var(--purple2));display:flex;align-items:center;justify-content:center;color:#fff}
.header-title{font-size:15px;font-weight:700}.header-sub{font-size:10px;color:var(--hint);margin-top:1px}
.header-time{margin-left:auto;text-align:right}.header-time-main{font-size:13px;color:var(--purple2);font-weight:700}.header-time-sub{font-size:10px;color:var(--hint)}
.content{padding:12px 14px 0}.card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:10px}
.card-dark{background:var(--soft);border-color:#c4b5fd}.card-out{background:var(--out);border-color:#c4b5fd}
.slabel{font-size:10px;font-weight:700;letter-spacing:.12em;color:var(--dim);text-transform:uppercase;margin-bottom:8px}
.hint{font-size:11px;color:var(--hint);margin-bottom:8px;line-height:1.55}.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{padding:7px 13px;border-radius:20px;border:2px solid var(--border2);background:#f4f4f5;color:var(--sub);font-size:12px;cursor:pointer;user-select:none}
.chip.active{border-color:var(--purple);background:var(--purple);color:#fff;font-weight:600}
textarea{width:100%;background:var(--input);border:1px solid var(--border2);border-radius:10px;color:var(--text);font-size:14px;line-height:1.6;padding:10px 12px;resize:vertical;outline:none;font-family:inherit}
.btn-row{display:flex;gap:10px;margin:6px 0 14px}.btn-generate{flex:3;padding:14px 0;border-radius:12px;border:none;background:linear-gradient(135deg,var(--purple),var(--purple2));color:#fff;font-size:15px;font-weight:700;cursor:pointer}
.btn-reset{flex:1;padding:14px 0;border-radius:12px;border:1px solid var(--border2);background:transparent;color:var(--dim);font-size:14px;font-weight:600;cursor:pointer}
.btn-copy{padding:6px 14px;border-radius:8px;border:1px solid var(--purple);background:transparent;color:var(--purple2);font-size:12px;font-weight:600;cursor:pointer}
.btn-copy.copied{background:var(--purple);color:#fff}.output-ta{height:320px;font-size:11px;line-height:1.8;font-family:monospace;background:#f8f8f8}.card-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}.hidden{display:none}
.info-row{display:flex;gap:8px;font-size:12px;color:var(--sub);margin-bottom:5px}.info-val{color:#6d28d9;font-weight:600}
</style>
</head>
<body>
<div class="header">
  <div class="header-icon">✦</div>
  <div>
    <div class="header-title">Stable Character Prompt Generator</div>
    <div class="header-sub">v8.0.1</div>
    <div class="header-sub">参照分離強化 + 写す範囲 + 拡張エフェクト</div>
  </div>
  <div class="header-time">
    <div class="header-time-main" id="hTime">--:--</div>
    <div class="header-time-sub" id="hDay">--</div>
  </div>
</div>

<div class="content">
  <div class="card card-dark">
    <div class="slabel">自動取得 — 東京時間</div>
    <div class="info-row"><span>📅</span><span id="infoDay">取得中…</span></div>
    <div class="info-row"><span>🕐</span><span id="infoTime">取得中…</span></div>
    <div class="info-row"><span>💭</span><span id="infoMood"></span></div>
    <div class="info-row"><span>✂️</span><span id="infoHair"></span></div>
  </div>

  <div class="card card-dark">
    <div class="card-head"><div class="slabel" style="margin-bottom:0">固定キャラ設定</div><button class="btn-copy" onclick="resetCharacterLock()">初期化</button></div>
    <div class="hint">写真参照ベースでは LIGHT 推奨。顔IDは1枚目を優先します。</div>
    <div class="chips" id="characterModeChips"></div>
    <textarea id="characterLock" rows="8" style="margin-top:10px"></textarea>
  </div>

  <div class="card card-dark">
    <div class="slabel">コーディネート画像参照 — 2枚目</div>
    <div class="hint">FULLでは2枚目を服装・小物・配色専用として扱い、それ以外の情報を使用しません。</div>
    <div class="chips" id="outfitReferenceModeChips"></div>
  </div>

  <div class="card"><div class="slabel">① 基本姿勢</div><div class="chips" id="basePostureChips"></div></div>
  <div class="card"><div class="slabel">② 今回のシーンだけ</div><textarea id="situation" rows="4" placeholder="場所・行動・表情・ポーズ細部を日本語で入力"></textarea></div>
  <div class="card"><div class="slabel">③ 胸シルエット</div><div class="chips" id="bustChips"></div></div>
  <div class="card"><div class="slabel">④ ヒップ / 下半身</div><div class="chips" id="hipChips"></div></div>
  <div class="card"><div class="slabel">⑤ 天気</div><div class="chips" id="weatherChips"></div></div>
  <div class="card"><div class="slabel">⑥ フィルムトーン</div><div class="chips" id="filmChips"></div></div>
  <div class="card"><div class="slabel">⑦ 作品トーン</div><div class="chips" id="toneChips"></div></div>
  <div class="card"><div class="slabel">⑧ エフェクト（複数選択）</div><div class="hint">各エフェクトのweightは後処理で削除しません。</div><div class="chips" id="effectChips"></div></div>
  <div class="card"><div class="slabel">⑨ エフェクト強度</div><div class="chips" id="effectStrengthChips"></div></div>
  <div class="card"><div class="slabel">⑩ 肌の見え方</div><div class="chips" id="skinFinishChips"></div></div>
  <div class="card"><div class="slabel">⑪ 接写質感</div><div class="chips" id="closeupTextureChips"></div></div>
  <div class="card"><div class="slabel">⑫ 自撮り / 第三者撮影</div><div class="chips" id="selfieModeChips"></div></div>
  <div class="card"><div class="slabel">⑬ カメラ位置 / アングル</div><div class="hint">カメラ高さ・距離を分解せず、人物写真としての見え方で選びます。</div><div class="chips" id="angleModeChips"></div></div>
  <div class="card"><div class="slabel">⑭ 写す範囲</div><div class="chips" id="visibleRangeChips"></div></div>
  <div class="card"><div class="slabel">⑮ 画面の傾き</div><div class="chips" id="cameraRollChips"></div></div>
  <div class="card"><div class="slabel">⑯ 顔向き</div><div class="chips" id="faceDirectionChips"></div></div>
  <div class="card"><div class="slabel">⑰ 視線</div><div class="chips" id="gazeChips"></div></div>
  <div class="card"><div class="slabel">⑱ 背景の見せ方</div><div class="chips" id="backgroundViewChips"></div></div>
  <div class="card"><div class="slabel">⑲ 余白</div><div class="chips" id="framingChips"></div></div>
  <div class="card"><div class="slabel">⑳ 写真の自然さ</div><div class="chips" id="photoStyleChips"></div></div>
  <div class="card"><div class="slabel">㉑ テンション</div><div class="chips" id="tensionChips"></div></div>
  <div class="card"><div class="slabel">㉒ 感情</div><div class="chips" id="emotionChips"></div></div>
  <div class="card"><div class="slabel">㉓ 表情</div><div class="chips" id="expressionChips"></div></div>

  <div class="btn-row">
    <button class="btn-generate" onclick="handleGenerate()">✦ プロンプト生成</button>
    <button class="btn-reset" onclick="handleReset()">リセット</button>
  </div>

  <div class="card card-dark hidden" id="metaCard">
    <div class="slabel">展開結果サマリー</div>
    <div id="metaContent" style="font-size:12px;line-height:1.9"></div>
  </div>

  <div class="card card-out hidden" id="outputCard">
    <div class="card-head"><div class="slabel" style="margin-bottom:0">生成プロンプト</div><button class="btn-copy" id="btnCopy" onclick="copyPrompt()">コピー</button></div>
    <textarea class="output-ta" id="outputArea" readonly></textarea>
  </div>
</div>

<script>
const APP_VERSION="v8.0.1";

const opt=(label,key,value)=>({label,key,value});
const LIGHT_CHARACTER_LOCK=`(refined Korean Asian fashion-model beauty atmosphere:1.5),
(mature adult woman, never younger-looking:1.8),
(very fair translucent skin with natural texture:1.6),
(slim elongated face impression:1.45),
(narrow jawline and delicate chin impression:1.45),
(realistic balanced adult proportions:1.6),
(face identity and detailed facial features are taken from Image A:1.95),
(no different person:1.95),
(no celebrity likeness:1.95)`;
const DEFAULT_CHARACTER_LOCK=LIGHT_CHARACTER_LOCK+`,
(stable same slender I-line body base:1.8),
(compact hips, narrow elegant torso, long slim limbs:1.75)`;

const HAIR_BY_MONTH={1:"(long straight, dark brown hair:1.65)",2:"(long wave, chestnut brown gradient hair:1.65)",3:"(long soft wave, chestnut brown hair:1.65)",4:"(medium straight, chestnut brown hair:1.6)",5:"(medium wave, light chestnut brown hair:1.6)",6:"(soft bob, ash brown hair:1.78), (not long hair:1.95)",7:"(airy bob, ash brown hair:1.8), (short-to-medium airy bob length around jaw to neck:1.9), (not long hair:1.98)",8:"(short bob, light ash brown hair:1.8), (not long hair:1.98)",9:"(medium bob, ash brown to dark brown hair:1.75)",10:"(inner-color straight, dark brown with caramel inner highlight:1.65)",11:"(inner-color wave, dark brown with rose-beige inner highlight:1.65)",12:"(long straight, dark brown with subtle inner highlight:1.65)"};
const DAY_MOOD={Sun:"Quiet reflective Sunday mood",Mon:"Tired but composed Monday mood",Tue:"Focused stable Tuesday calm",Wed:"Midweek fatigue, quiet weariness",Thu:"Slight pre-weekend anticipation",Fri:"Friday pre-weekend energy",Sat:"Relaxed confident Saturday energy"};

const OPTIONS={
characterMode:[opt("📷 OFF","off","off"),opt("✨ LIGHT","light","light"),opt("🔒 FULL","full","full")],
outfitReferenceMode:[opt("🚫 OFF","off","off"),opt("✨ LIGHT","light","light"),opt("👗 FULL","full","full")],
basePosture:[opt("🎲 おまかせ","auto","auto"),opt("🧍 立っている","standing","standing"),opt("🪑 座っている","seated","seated"),opt("🛋️ 寝転がっている","reclining","reclining")],
bust:[opt("🫧 控えめ","subtle","(restrained natural bust contour through opaque clothing:1.68)"),opt("🌿 自然","natural","(natural balanced upper-body garment contour:1.78)"),opt("⬆️ 立体感","dimensional","(slightly fuller high-set upper-body silhouette through clothing:1.88)"),opt("⬆️🧱 立体感＋ライン","both","(slightly fuller and dimensional upper-body silhouette through clothing:1.9), (defined opaque garment contour:1.88)"),opt("👚 服装なり","outfit","(upper-body silhouette follows the selected outfit naturally:1.8)")],
hip:[opt("🫧 控えめ","subtle","(subtle compact lower-body silhouette:1.6)"),opt("🌿 自然","natural","(natural compact lower-body silhouette:1.72)"),opt("🍑 小尻プリ","perky","(compact small hips with a gently rounded shape:1.88), (not laterally wide hips:1.94)"),opt("🍑⬆️ 小尻アップ","lifted","(compact small hips with a clearly lifted shape:1.9)"),opt("👖 服装なり","outfit","(lower-body silhouette follows the selected outfit naturally:1.8)")],
weather:[opt("晴れ ☀️","clear","clear weather appropriate to the selected time of day"),opt("曇り ☁️","cloudy","overcast cloudy atmosphere"),opt("小雨 🌦️","drizzle","light drizzle rain, wet surfaces"),opt("雨 🌧️","rain","steady rain, rain-soaked atmosphere"),opt("雪 ❄️","snow","snow falling, winter scenery"),opt("霧 🌫️","fog","foggy misty atmosphere")],
film:[opt("なし","none",""),opt("コダック ゴールド 200","gold200","Kodak Gold 200 film tone"),opt("ポートラ 400","portra400","Kodak Portra 400 film tone"),opt("ポートラ 800","portra800","Kodak Portra 800 film tone"),opt("フジ 400H","fuji400h","Fuji Pro 400H film tone"),opt("シネスティル 800T","cinestill","CineStill 800T film tone"),opt("ヴィンテージ90s","vintage90s","1990s vintage film tone"),opt("ガサつき","gritty","gritty rough film tone")],
tone:[opt("なし","none",""),opt("クール / モダン","cool","cool modern aesthetic"),opt("キュート / 柔らか","cute","cute soft aesthetic"),opt("ダーク / ムーディ","dark","dark moody aesthetic"),opt("ナチュラル / 透明感","transparent","natural transparent beauty aesthetic"),opt("エレガント / 上品","elegant","elegant refined aesthetic"),opt("ミニマル / 静寂","minimal","minimal quiet aesthetic")],
effectStrength:[opt("🫧 控えめ","subtle","subtle"),opt("✨ 標準","standard","standard"),opt("🌟 強め","strong","strong"),opt("💥 盛り盛り","max","max")],
skinFinish:[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(real skin texture:1.82), (natural skin finish:1.8)"),opt("💧 しっとり","moist","(soft moisturized skin finish:1.82)"),opt("✨ ツヤあり","dewy","(noticeable dewy skin finish:1.84)")],
closeupTexture:[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(natural realistic close-up detail balance:1.78)"),opt("💧 しっとり","moist","(close-up skin looks softly moisturized and realistic:1.82)"),opt("🔬 高精細","detailed","(high-detail close-up rendering of eyelashes, lips, pores, and fine skin texture:1.86)")],
selfieMode:[opt("🎲 自動","auto","auto"),opt("🤳 自撮り ON","on","on"),opt("📷 自撮り OFF","off","off")],
angleMode:[opt("🎲 おまかせ","auto","auto"),opt("👁️ 目線","eye","(camera at eye height:1.9)"),opt("✨ 盛れ角","golden","(camera slightly above eye level looking down:1.9)"),opt("⬆️ 少し上から","high","(camera clearly above eye level:1.84)"),opt("🙆 頭上から","overhead","(true overhead super high-angle selfie:1.9), (bird's-eye framing:1.84)"),opt("🤫 腰だめ","hiddenWaist","(true hidden waist-held selfie:2.0), (camera viewpoint originates very close to lower torso or waist:2.0), (no raised-hand selfie:2.0)"),opt("⬇️ 低め前持ち","lowFront","(ordinary low-angle selfie from in front of the body:1.84)"),opt("📉 強い煽り","superLow","(dramatic super low-angle selfie or portrait:1.9)"),opt("➡️ 真横から","side","(camera positioned at true side of the subject:1.9)"),opt("↩️ 振り向き","overShoulder","(over-shoulder or turn-back portrait:1.88)"),opt("🚶 歩き","walking","(captured mid-walk:1.82)"),opt("🌀 斜め","tilted","(slightly diagonal handheld composition:1.78)")],
visibleRange:[opt("⚖️ バランス","balanced","(balanced portrait composition:1.82)"),opt("🙂 顔のみ","faceOnly","(face-only portrait crop:1.92)"),opt("🧿 顔どアップ","extremeFace","(extreme face close-up composition:1.98)"),opt("🔍 顔アップ","faceCloseup","(close-up face composition:1.92)"),opt("↔️ 横顔アップ","profileCloseup","(profile close-up composition:1.94)"),opt("🙂 顔〜肩","headShoulder","(head-and-shoulders portrait framing:1.88)"),opt("🧥 上半身","upperBody","(upper-body portrait composition:1.88)"),opt("🧍 腰上","waistUp","(waist-up portrait framing:1.92)"),opt("🧍 全身","fullBody","(full-body portrait framing:1.88)")],
cameraRoll:[opt("🎲 おまかせ","auto","(camera roll remains natural:1.7)"),opt("📐 水平","level","(camera roll is level:1.86)"),opt("／ 少し斜め","slight","(slight diagonal camera roll only:1.84)"),opt("／／ 斜め強め","strong","(clearly diagonal camera roll:1.88)")],
faceDirection:[opt("🎲 おまかせ","auto","(face orientation is naturally derived:1.74)"),opt("🙂 正面","front","(front-facing facial orientation:1.84)"),opt("◢ 斜め向き","threeQuarter","(three-quarter facial angle:1.86)"),opt("➡️ 横顔","profile","(true side-profile facial orientation:1.9)"),opt("↩️ 振り向き","turnBack","(looking back over shoulder:1.9)"),opt("🙈 顔を見せない","away","(face turned away:1.92)")],
gaze:[opt("🎲 おまかせ","auto","(gaze naturally derived from scene:1.72)"),opt("👀 カメラ目線","camera","(eyes naturally meet the lens:1.84)"),opt("↗️ 少し外す","off","(gaze is slightly off-camera:1.84)"),opt("🌌 遠くを見る","far","(gaze directed into the distance:1.86)"),opt("😌 伏し目","down","(downward gaze:1.84)")],
backgroundView:[opt("🚫 指定なし","none",""),opt("🫧 控えめ","subtle","(background remains secondary:1.7)"),opt("🌆 バランス","balanced","(background shown in a balanced natural way:1.75)"),opt("🌸 下 / 足元側","lower","(lower background is visible:1.78)"),opt("☕ 奥","depth","(depth background behind the subject clearly visible:1.78)"),opt("🌙 上","upper","(upper background visible:1.78)")],
framing:[opt("⚖️ 標準","standard","(balanced subject scale with moderate breathing room:1.7)"),opt("🧍 余白少なめ","tight","(tight framing with reduced empty space:1.8)"),opt("🖼️ 余白なし","full","(subject fills the image as much as possible:1.9)"),opt("🏙️ 余白あり","wide","(clear breathing room around the subject:1.78)")],
photoStyle:[opt("📷 リアルな日常写真","daily","(real everyday snapshot feel:1.86)"),opt("🙂 少し盛れた自然写真","enhanced","(naturally flattering portrait look:1.84)"),opt("🧍 モデルっぽい","model","(model-like posing and facial control:1.82)"),opt("🖤 ファッション誌","editorial","(fashion editorial photography feel:1.88)"),opt("🎬 作り込み強め","strong","(strongly directed visual presentation:1.84)")],
tension:[opt("😌 低め","low","low energy"),opt("🙂 普通","medium","medium energy"),opt("😄 やや高め","mediumHigh","medium-high energy"),opt("🤩 高め","high","high energy")],
emotion:[opt("🎲 おまかせ","auto",""),opt("😐 ニュートラル","neutral","neutral"),opt("😊 嬉しい","happy","happy"),opt("😆 楽しい","joyful","joyful"),opt("😌 落ち着き","calm","calm"),opt("🌙 寂しい","lonely","lonely"),opt("😩 疲れた","tired","tired"),opt("😎 クール","cool","cool")],
expression:[opt("🎲 自動","auto",""),opt("😐 真顔","neutral","neutral deadpan, calm expression"),opt("🙂 微笑み","smile","soft gentle smile"),opt("😄 明るい笑顔","happy","bright happy expression"),opt("😆 めっちゃ嬉しそう","veryHappy","very happy joyful smile"),opt("😌 物憂げ","melancholic","melancholic reflective expression"),opt("😪 気だるげ","sleepy","tired but gentle expression")]
};

const EFFECTS=[
opt("🌫️ 背景ボケ","bokeh","(portrait-safe moderate background blur:1.66), (background softly blurred but still readable:1.68)"),
opt("✨ 光の玉ボケ","orb","(clearly visible light orb bokeh:1.8), (ambient light circles in background:1.8)"),
opt("✨ 前ボケ","foreground","(soft out-of-focus foreground bokeh:1.74)"),
opt("🌁 ソフトフォーカス","softfocus","(soft focus haze:1.68), (gentle dreamy blur on edges:1.66)"),
opt("📼 VHSノイズ","vhs","(VHS scan lines:1.68), (retro analog video noise:1.66), (chromatic aberration:1.66)"),
opt("🌙 逆光/リムライト","rim","(clearly visible backlighting:1.78), (rim light on hair and shoulders:1.78)"),
opt("⚡ 直フラッシュ","flash","(direct on-camera flash look:1.86)"),
opt("🌃 ネオン反射","neon","(neon reflections on nearby glass or polished surfaces:1.72)"),
opt("🪞 ガラス反射","glass","(subtle glass reflection layer:1.72)"),
opt("🏃 モーションブラー","motionblur","(subtle handheld motion blur:1.62)"),
opt("📸 コンデジ感","digicam","(compact digital camera snapshot look:1.76)"),
opt("🩶 低彩度","desat","(muted desaturated color palette:1.72)"),
opt("📱 スマホHDR","hdr","(smartphone HDR rendering:1.74)")
];

let state={characterMode:"light",outfitReferenceMode:"off",basePosture:"auto",bust:"both",hip:"perky",weather:"",film:"",tone:"",effects:[],effectStrength:"standard",skinFinish:"",closeupTexture:"",selfieMode:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"standard",photoStyle:"daily",tension:"",emotion:"",expression:""};

function tokyoNow(){
 const n=new Date(new Date().toLocaleString("en-US",{timeZone:"Asia/Tokyo"}));
 const d=["Sun","Mon","Tue","Wed","Thu","Fri","Sat"][n.getDay()];
 const h=n.getHours();
 const label=h<5?"深夜":h<9?"早朝":h<12?"午前":h<14?"昼":h<17?"午後":h<20?"夕方":h<23?"夜":"深夜";
 return{month:n.getMonth()+1,day:d,time:n.toLocaleTimeString("ja-JP",{hour:"2-digit",minute:"2-digit"}),label};
}
function updateClock(){const t=tokyoNow();hTime.textContent=t.time+" JST";hDay.textContent=t.day+" · "+t.month+"月 · "+t.label;infoDay.innerHTML="<span class='info-val'>"+t.day+" / "+t.month+"月 / "+t.label+"</span>";infoTime.innerHTML="<span class='info-val'>"+t.time+" JST</span>";infoMood.textContent=DAY_MOOD[t.day];infoHair.textContent=HAIR_BY_MONTH[t.month];}
function find(k){return (OPTIONS[k]||[]).find(x=>x.key===state[k])||{label:"",value:""}}
function renderSingle(id,key){const el=document.getElementById(id);el.innerHTML="";OPTIONS[key].forEach(i=>{const b=document.createElement("button");b.className="chip"+(state[key]===i.key?" active":"");b.textContent=i.label;b.onclick=()=>{state[key]=i.key; if(key==="characterMode")resetCharacterLock(); renderAll();};el.appendChild(b)})}
function renderMulti(id){const el=document.getElementById(id);el.innerHTML="";EFFECTS.forEach(i=>{const a=state.effects.includes(i.key);const b=document.createElement("button");b.className="chip"+(a?" active":"");b.textContent=i.label;b.onclick=()=>{a?state.effects.splice(state.effects.indexOf(i.key),1):state.effects.push(i.key);renderAll();};el.appendChild(b)})}
function renderAll(){
 for(const k of Object.keys(OPTIONS)){const id=k+"Chips";if(document.getElementById(id))renderSingle(id,k)}
 renderMulti("effectChips");
}
function resetCharacterLock(){characterLock.value=state.characterMode==="off"?"":state.characterMode==="full"?DEFAULT_CHARACTER_LOCK:LIGHT_CHARACTER_LOCK}
function scaleWeightedPrompt(p,m){return(p||"").replace(/\(([^()]+?):([0-9]*\.?[0-9]+)\)/g,(x,b,w)=>`(${b}:${Math.round(Math.min(Math.max(parseFloat(w)*m,.1),3)*100)/100})`)}
function outfitBlock(){
 if(state.outfitReferenceMode==="off")return"";
 if(state.outfitReferenceMode==="light")return`IMAGE B — OUTFIT REFERENCE LIGHT:
Use Image B only for outfit color palette, styling mood, and rough garment impression.
Do not use Image B for face, body, pose, camera, background, location, or lighting.`;
 return`IMAGE B — OUTFIT REFERENCE ONLY / STRICT HARD CONSTRAINT:
Use Image B exclusively for:
- clothing type
- outfit coordination
- layering
- materials
- colors
- shoes
- bag
- accessories
- styling direction
- color palette
- written outfit notes such as POINT and STYLE POINT when present

Do not use Image B for anything else.

Absolutely do not copy from Image B:
- face
- body type
- hairstyle
- pose
- hand position
- camera angle
- composition
- background
- location
- lighting
- facial expression
- mood unrelated to outfit

Ignore all non-outfit information in Image B.
Image B must control the outfit only and must not control identity or scene construction.`;
}
function imageABlock(){
 return`REFERENCE IMAGE A — IDENTITY / BODYLINE ONLY / STRICT HARD CONSTRAINT:
Use Image A exclusively for:
- face identity
- facial features
- facial proportions
- skin tone
- bust presence / chest impression
- shoulder width
- torso narrowness
- waist position
- compact hip width
- visible limb slimness

Do not use Image A for anything else.

Absolutely do not copy from Image A:
- clothing
- outfit details
- styling
- accessories
- hairstyle
- pose
- hand or arm position
- camera angle
- composition
- background
- location
- lighting
- mood props
- any scene objects

Ignore all non-identity and non-bodyline information in Image A.
The clothing visible in Image A must never appear in the generated image.
Image A must not influence outfit generation in any way.`;
}
function effectiveSelfie(scene){if(state.selfieMode!=="auto")return state.selfieMode;return /他撮り|第三者|非自撮り|自撮りじゃない|non-selfie/i.test(scene)?"off":"on"}
function buildPrompt(){
 const t=tokyoNow(), scene=situation.value.trim()||"Create a realistic everyday adult fashion portrait.";
 const selfie=effectiveSelfie(scene);
 const mult={subtle:.9,standard:1,strong:1.12,max:1.25}[state.effectStrength]||1;
 const fx=state.effects.map(k=>EFFECTS.find(e=>e.key===k)).filter(Boolean).map(e=>scaleWeightedPrompt(e.value,mult)).join(", ");
 const blocks=[];
 blocks.push(`APP_VERSION: ${APP_VERSION}
PROMPT_ENGINE: angle-core + strict reference separation + visible-range + style/effects
CAMERA_ENGINE: angle-preset, not micro physical controls`);
 blocks.push(imageABlock());
 blocks.push(`CHARACTER LOCK MODE:
${find("characterMode").label}
${state.characterMode==="off"?"(fixed character text disabled; use Image A only for identity and visible bodyline:1.95)":characterLock.value.trim()}`);
 const ob=outfitBlock();if(ob)blocks.push(ob);
 blocks.push(`HAIR — APP MONTHLY PRIORITY:
${HAIR_BY_MONTH[t.month]},
(monthly hairstyle overrides the hairstyle in Image A:1.98),
(use Image A for face identity, not hairstyle:1.98)`);
 blocks.push(`SAFETY / REALISM:
(safe non-sexual adult fashion portrait:1.95),
(opaque public-safe clothing:1.95),
(photographic realism, real skin texture, believable lighting and shadows:1.9),
(no anime, no illustration, no plastic skin:1.9)`);
 blocks.push(`SCENE:
${scene}`);
 blocks.push(`POSTURE:
${find("basePosture").value}`);
 blocks.push(`CAMERA MODE:
${selfie==="off"?"(non-selfie third-person external camera viewpoint:1.95), (subject is not holding the active camera:1.95), (no smartphone selfie POV:1.95)":"(smartphone in her hand is the active front camera:1.9), (viewpoint follows the selected angle preset:1.9)"}`);
 blocks.push(`CAMERA POSITION / ANGLE:
${find("angleMode").value}`);
 blocks.push(`VISIBLE RANGE:
${find("visibleRange").value}`);
 blocks.push(`IMAGE TILT:
${find("cameraRoll").value}`);
 blocks.push(`FACE / GAZE:
${find("faceDirection").value}
${find("gaze").value}`);
 blocks.push(`COMPOSITION:
${find("backgroundView").value}
${find("framing").value}
${find("photoStyle").value}`);
 blocks.push(`EXPRESSION / MOOD:
${find("expression").value||((find("emotion").value||"natural")+" context-driven expression")}
(${find("tension").value||"natural energy"}:1.72)`);
 blocks.push(`BODY / OUTFIT SILHOUETTE:
${find("bust").value}
${find("hip").value}`);
 if(find("skinFinish").value)blocks.push(`SKIN FINISH:
${find("skinFinish").value}`);
 if(find("closeupTexture").value)blocks.push(`CLOSE-UP TEXTURE:
${find("closeupTexture").value}`);
 blocks.push(`STYLE / EFFECTS — APPLY LAST:
Current time: ${t.label}, ${t.time} JST
Day mood: ${DAY_MOOD[t.day]}
${find("weather").value?"Weather: "+find("weather").value:""}
${find("film").value?"Film tone: "+find("film").value:""}
${find("tone").value?"Overall tone: "+find("tone").value:""}
${fx?"Effects: "+fx:""}
(apply style and effects only after portrait composition is solved:1.88)`);
 blocks.push(`ASPECT / ENVIRONMENT:
(vertical 9:16 smartphone image:1.6),
(real location matching the written scene:1.75),
(realistic ambient lighting and natural handheld micro-shake:1.65)`);
 return blocks.join("\n\n");
}
function handleGenerate(){const p=buildPrompt();outputArea.value=p;metaCard.classList.remove("hidden");outputCard.classList.remove("hidden");metaContent.innerHTML=`🧩 <b>App</b>：${APP_VERSION}<br>🔒 <b>参照分離</b>：Image A=顔・胸印象・体型のみ / Image B=コーデのみ<br>👗 <b>コーデ参照</b>：${find("outfitReferenceMode").label}<br>📸 <b>アングル</b>：${find("angleMode").label}<br>🔒 <b>後処理</b>：weight削除なし`;copyPrompt(true);outputCard.scrollIntoView({behavior:"smooth"})}
function copyPrompt(auto=false){outputArea.select();const done=()=>{btnCopy.textContent=auto?"✓ 自動コピー済み":"✓ コピー済み";btnCopy.classList.add("copied");setTimeout(()=>{btnCopy.textContent="コピー";btnCopy.classList.remove("copied")},2200)};if(navigator.clipboard)navigator.clipboard.writeText(outputArea.value).then(done).catch(()=>{document.execCommand("copy");done()});else{document.execCommand("copy");done()}}
function handleReset(){state={characterMode:"light",outfitReferenceMode:"off",basePosture:"auto",bust:"both",hip:"perky",weather:"",film:"",tone:"",effects:[],effectStrength:"standard",skinFinish:"",closeupTexture:"",selfieMode:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"standard",photoStyle:"daily",tension:"",emotion:"",expression:""};situation.value="";metaCard.classList.add("hidden");outputCard.classList.add("hidden");outputArea.value="";resetCharacterLock();renderAll()}
document.addEventListener("DOMContentLoaded",()=>{resetCharacterLock();renderAll();updateClock();setInterval(updateClock,30000)});
</script>
</body>
</html>
