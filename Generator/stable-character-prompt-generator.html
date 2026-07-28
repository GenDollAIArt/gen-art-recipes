<!--
  Selfie Prompt Generator
  Version: 8.0.1
  Updated: 2026-07-15
  Changelog:
    v8.0.1 - APP_VERSIONをv8.0.1に更新。アプリ名の下にバージョン表示を追加。Image A / Image B FULL の参照制約を厳格化。visibleなv3.57表記を削除。
    v8.0.0 - v3.57思想の角度コア復活版を正式メジャー化。ライトモード専用、拡張フィルム/エフェクト、自動コピーを維持。
    v7.3.0 - v3.57の思想へ戻して再設計。カメラ高さ/距離/持ち方/レンズ向き/撮影メモの分解を廃止し、人物写真としての「カメラ位置 / アングル」プリセットを主軸に復活。
             腰だめ / 低め前持ち / 強い煽りを明確化し、顔のみ・顔どアップ・横顔アップなどの写す範囲を追加。
             1枚目=顔・体型参照、2枚目=コーデ参照（OFF/LIGHT/FULL）を追加。SHEETはFULLへ統合。
             画面の傾き、顔向き、視線、肌の見え方、接写質感、拡張エフェクトをv3.57の単純選択思想で追加。
             後処理によるweight削除や重複削除は行わず、各選択肢の元プロンプトを根本から整理。
    v3.57.0 - エフェクト系の長押しヘルプを拡張。各エフェクト/エフェクト強度の「何が変わるか」「向く場面」「注意点」を表示
-->
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Stable Character Prompt Generator</title>
<style>
  :root {
    /* v7.2系に合わせてライトモード専用。OSのダークモード設定には連動しない。 */
    --bg:#f4f4f5; --bg-card:#fff; --bg-dark:#ede9fe; --bg-out:#f8f7ff; --bg-input:#f4f4f5; --bg-ta:#f8f8f8;
    --border:#e4e4e7; --border-m:#d4d4d8; --border-pu:#c4b5fd;
    --text:#18181b; --text-sub:#52525b; --text-dim:#71717a; --text-hint:#a1a1aa; --text-pu:#7c3aed;
    --chip-bg:#f4f4f5; --chip-col:#52525b; --chip-abg:#7c3aed; --chip-acol:#fff; --chip-abdr:#7c3aed;
    --hdr-bg:linear-gradient(135deg,#ede9fe 0%,#f5f3ff 100%); --reset-col:#71717a; --reset-bdr:#d4d4d8;
    --info-val:#6d28d9; --copy-done-bg:#7c3aed; --copy-done-col:#fff; --placeholder:#d4d4d8;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:var(--bg);color:var(--text);font-family:'Hiragino Kaku Gothic ProN','Noto Sans JP',sans-serif;padding-bottom:80px;font-size:14px}
  .header{background:var(--hdr-bg);border-bottom:1px solid var(--border);padding:16px 14px 12px;position:sticky;top:0;z-index:10;display:flex;align-items:center;gap:10px}
  .header-icon{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,#7c3aed,#a855f7);display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0}
  .header-title{font-size:15px;font-weight:700}.header-sub{font-size:10px;color:var(--text-hint);margin-top:1px}.header-time{margin-left:auto;text-align:right}.header-time-main{font-size:13px;color:#a855f7;font-weight:700}.header-time-sub{font-size:10px;color:var(--text-hint)}
  .content{padding:12px 14px 0}.card{background:var(--bg-card);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:10px}.card-dark{background:var(--bg-dark);border-color:var(--border-pu)}.card-out{background:var(--bg-out);border-color:var(--border-pu)}
  .slabel{font-size:10px;font-weight:700;letter-spacing:.12em;color:var(--text-dim);text-transform:uppercase;margin-bottom:8px}.hint{font-size:11px;color:var(--text-hint);margin-bottom:8px;line-height:1.55}
  .chips{display:flex;flex-wrap:wrap;gap:6px}.chip{padding:7px 13px;border-radius:20px;border:2px solid var(--border-m);background:var(--chip-bg);color:var(--chip-col);font-size:12px;cursor:pointer;transition:all .15s;-webkit-tap-highlight-color:transparent;user-select:none}.chip.active{border-color:var(--chip-abdr);background:var(--chip-abg);color:var(--chip-acol);font-weight:600}.chip.disabled{opacity:.35;cursor:not-allowed;filter:grayscale(.6)}.chip.has-help::after{content:"？";display:inline-flex;align-items:center;justify-content:center;width:15px;height:15px;margin-left:5px;border-radius:999px;font-size:10px;color:#c4b5fd;background:rgba(168,85,247,.18);border:1px solid rgba(196,181,253,.35)}
  textarea{width:100%;background:var(--bg-input);border:1px solid var(--border-m);border-radius:10px;color:var(--text);font-size:14px;line-height:1.6;padding:10px 12px;resize:vertical;outline:none;font-family:inherit}textarea::placeholder{color:var(--placeholder)}
  .btn-row{display:flex;gap:10px;margin:6px 0 14px}.btn-generate{flex:3;padding:14px 0;border-radius:12px;border:none;background:linear-gradient(135deg,#7c3aed,#a855f7);color:#fff;font-size:15px;font-weight:700;cursor:pointer;letter-spacing:.03em}.btn-reset{flex:1;padding:14px 0;border-radius:12px;border:1px solid var(--reset-bdr);background:transparent;color:var(--reset-col);font-size:14px;font-weight:600;cursor:pointer}.btn-copy{padding:6px 14px;border-radius:8px;border:1px solid #7c3aed;background:transparent;color:#a855f7;font-size:12px;font-weight:600;cursor:pointer;transition:all .2s}.btn-copy.copied{background:var(--copy-done-bg);color:var(--copy-done-col)}
  .output-ta{width:100%;height:300px;font-size:11px;color:var(--text-sub);line-height:1.8;font-family:monospace;background:var(--bg-ta);border-radius:8px;padding:10px 12px;border:1px solid var(--border);resize:none;outline:none}.info-row{display:flex;align-items:flex-start;gap:8px;font-size:12px;color:var(--text-sub);margin-bottom:5px}.info-icon{flex-shrink:0;color:#7c3aed}.info-val{color:var(--info-val);font-weight:600}.card-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}.hidden{display:none}
  .help-overlay{position:fixed;inset:0;z-index:50;background:rgba(0,0,0,.55);display:flex;align-items:flex-end;justify-content:center;padding:14px}.help-overlay.hidden{display:none}.help-sheet{width:100%;max-width:520px;background:var(--bg-card);border:1px solid var(--border-pu);border-radius:16px;padding:16px;box-shadow:0 -10px 40px rgba(0,0,0,.35)}.help-title{font-size:15px;font-weight:700;color:var(--text);margin-bottom:8px}.help-body{font-size:13px;line-height:1.75;color:var(--text-sub);white-space:pre-line}.help-close{margin-top:14px;width:100%;padding:12px 0;border-radius:12px;border:1px solid #7c3aed;background:transparent;color:#c4b5fd;font-weight:700;font-size:14px}
</style>
</head>
<body>
<div class="header">
  <div class="header-icon">✦</div>
  <div><div class="header-title">Stable Character Prompt Generator</div><div class="header-sub">v8.0.1</div><div class="header-sub">参照/写す範囲/拡張エフェクト</div></div>
  <div class="header-time"><div class="header-time-main" id="hTime">--:--</div><div class="header-time-sub" id="hDay">-- · --月 · --</div></div>
</div>
<div class="content">
  <div class="card card-dark"><div class="slabel">自動取得 — 東京時間</div><div class="info-row"><span class="info-icon">📅</span><span id="infoDay">取得中…</span></div><div class="info-row"><span class="info-icon">🕐</span><span id="infoTime">取得中…</span></div><div class="info-row"><span class="info-icon">💭</span><span id="infoDayMood" style="font-size:11px;color:#71717a;"></span></div><div class="info-row"><span class="info-icon">✂️</span><span id="infoHair" style="font-size:11px;color:#71717a;"></span></div></div>

  <div class="card card-dark"><div class="card-head"><div class="slabel" style="margin-bottom:0;">固定キャラ設定 — 毎回先頭に入る</div><button class="btn-copy" onclick="resetCharacterLock()">初期化</button></div><div class="hint">写真参照ベースでは LIGHT 推奨。顔IDは1枚目の Face Reference を優先し、固定キャラは雰囲気補助だけにします。</div><div class="slabel" style="margin-top:10px;">固定キャラモード</div><div class="chips" id="characterModeChips"></div><textarea id="characterLock" rows="8" style="margin-top:10px;"></textarea></div>

  <div class="card card-dark"><div class="slabel">コーディネート画像参照 — 2枚目の添付画像</div><div class="hint">OFF/LIGHT/FULLのみ。FULLは普通の服装写真にもコーディネートシートにも使います。シートの場合はアイテム・色・STYLE POINTを読み、枠やテンプレデザインは生成画像に持ち込みません。</div><div class="chips" id="outfitReferenceModeChips"></div></div>

  <div class="card"><div class="slabel">① 基本姿勢</div><div class="hint">大きな姿勢だけを選びます。細部は②シーンに書きます。</div><div class="chips" id="basePostureChips"></div></div>
  <div class="card"><div class="slabel">② 今回のシーンだけ（日本語で入力）</div><div class="hint">場所・服装・ポーズ細部・表情・何してるか。撮影メモ欄は作らず、構図は下の選択肢で決めます。</div><textarea id="situation" rows="4" placeholder="例：ThinkPark Towerのロビー。めっちゃ嬉しそうな顔。"></textarea></div>

  <div class="card"><div class="slabel">③ 胸シルエット</div><div class="hint">選択した意味をそのまま服越しの自然なシルエットに反映します。</div><div class="chips" id="bustChips"></div></div>
  <div class="card"><div class="slabel">④ ヒップ / 下半身シルエット</div><div class="hint">細身Iラインを維持しつつ、小尻・コンパクト感を調整します。</div><div class="chips" id="hipChips"></div></div>
  <div class="card"><div class="slabel">⑤ 天気を選択</div><div class="chips" id="weatherChips"></div></div>
  <div class="card"><div class="slabel">⑥ フィルムトーン / 質感</div><div class="hint">長押しでヘルプ表示。色味・質感・雰囲気を選びます。</div><div class="chips" id="filmChips"></div></div>
  <div class="card"><div class="slabel">⑦ 作品トーン</div><div class="hint">長押しでヘルプ表示。写真全体の印象を選びます。</div><div class="chips" id="toneChips"></div></div>
  <div class="card"><div class="slabel">⑧ エフェクト（複数選択可）</div><div class="hint">各エフェクトは元プロンプト段階で重みを持ち、後処理で消しません。まずは3〜5個がおすすめ。</div><div class="chips" id="effectChips"></div></div>
  <div class="card"><div class="slabel">⑨ エフェクト強度</div><div class="hint">選択エフェクトのweightを倍率補正します。通常プロンプトには触りません。</div><div class="chips" id="effectStrengthChips"></div></div>
  <div class="card"><div class="slabel">⑩ 肌の見え方 / 肌質感</div><div class="chips" id="skinFinishChips"></div></div>
  <div class="card"><div class="slabel">⑪ 接写質感</div><div class="hint">顔のみ・顔どアップ・横顔アップで効きやすい質感です。</div><div class="chips" id="closeupTextureChips"></div></div>
  <div class="card"><div class="slabel">⑫ 自撮り / 第三者撮影</div><div class="hint">自撮りONならスマホ手持ちカメラ視点。OFFなら外部カメラの自然なポートレート/スナップ扱い。</div><div class="chips" id="selfieModeChips"></div></div>
  <div class="card"><div class="slabel">⑬ カメラ位置 / アングル</div><div class="hint">このアプリの中核。カメラ高さ・距離・レンズ向きを分解せず、人物写真の見え方として選びます。</div><div class="chips" id="angleModeChips"></div></div>
  <div class="card"><div class="slabel">⑭ 写す範囲</div><div class="hint">顔のみ・顔どアップなどを追加。場所を見せる量は背景/余白側で調整します。</div><div class="chips" id="visibleRangeChips"></div></div>
  <div class="card"><div class="slabel">⑮ 画面の傾き</div><div class="hint">構図の回転だけを指定します。腰だめやローアングルの起点は変えません。</div><div class="chips" id="cameraRollChips"></div></div>
  <div class="card"><div class="slabel">⑯ 顔向き</div><div class="chips" id="faceDirectionChips"></div></div>
  <div class="card"><div class="slabel">⑰ 視線</div><div class="chips" id="gazeChips"></div></div>
  <div class="card"><div class="slabel">⑱ 背景の見せ方</div><div class="chips" id="backgroundViewChips"></div></div>
  <div class="card"><div class="slabel">⑲ 余白 / リーディングスペース</div><div class="chips" id="framingChips"></div></div>
  <div class="card"><div class="slabel">⑳ 写真の自然さ / 演出度</div><div class="chips" id="photoStyleChips"></div></div>
  <div class="card"><div class="slabel">㉑ テンション（動きの強さ）</div><div class="chips" id="tensionChips"></div></div>
  <div class="card"><div class="slabel">㉒ 感情（内面の気分）</div><div class="chips" id="emotionChips"></div></div>
  <div class="card"><div class="slabel">㉓ 表情（顔の出力）</div><div class="hint">未選択の場合はシーンと感情から自然に導出します。</div><div class="chips" id="expressionChips"></div></div>

  <div class="btn-row"><button class="btn-generate" id="btnGen" onclick="handleGenerate()">✦ プロンプト生成</button><button class="btn-reset" onclick="handleReset()">リセット</button></div>
  <div class="card card-dark hidden" id="metaCard"><div class="slabel">展開結果サマリー</div><div id="metaContent" style="font-size:12px;color:#a1a1aa;line-height:1.9;"></div></div>
  <div class="card card-out hidden" id="outputCard"><div class="card-head"><div class="slabel" style="margin-bottom:0;">生成プロンプト</div><button class="btn-copy" id="btnCopy" onclick="handleCopy()">コピー</button></div><textarea class="output-ta" id="outputArea" readonly onclick="this.select();this.setSelectionRange(0,this.value.length);" onfocus="this.select();this.setSelectionRange(0,this.value.length);"></textarea></div>
</div>
<div class="help-overlay hidden" id="chipHelpOverlay" onclick="hideChipHelp()"><div class="help-sheet" onclick="event.stopPropagation()"><div class="help-title" id="chipHelpTitle">ヘルプ</div><div class="help-body" id="chipHelpBody"></div><button class="help-close" onclick="hideChipHelp()">閉じる</button></div></div>
<script>
const APP_VERSION = "v8.0.1";
const HAIR_BY_MONTH = {1:"(long straight, dark brown hair:1.65), (hair falls below the shoulders:1.55)",2:"(long wave, chestnut brown gradient hair:1.65), (hair falls below the shoulders:1.55)",3:"(long soft wave, chestnut brown hair:1.65), (hair falls below the shoulders:1.55)",4:"(medium straight, chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",5:"(medium wave, light chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",6:"(soft bob, ash brown hair:1.78), (jaw-to-neck length bob:1.88), (not long hair:1.95)",7:"(airy bob, ash brown hair:1.8), (short-to-medium airy bob length around jaw to neck:1.9), (not long hair:1.98)",8:"(short bob, light ash brown hair:1.8), (clear short bob length above or around jaw:1.9), (not long hair:1.98)",9:"(medium bob, ash brown to dark brown hair:1.75), (shoulder-grazing medium bob length:1.82), (not chest-length hair:1.95)",10:"(inner-color straight, dark brown with caramel inner highlight:1.65), (long hair below shoulders:1.55)",11:"(inner-color wave, dark brown with rose-beige inner highlight:1.65), (long hair below shoulders:1.55)",12:"(long straight, dark brown with subtle inner highlight:1.65), (long hair below shoulders:1.55)"};
const DAY_MOOD={Sun:"Quiet reflective Sunday mood, gentle weekend loneliness",Mon:"Tired but composed Monday mood",Tue:"Focused stable neutral Tuesday calm",Wed:"Midweek fatigue, quiet weariness",Thu:"Slight pre-weekend anticipation",Fri:"Friday pre-weekend energy, lively but time-neutral mood",Sat:"Relaxed confident Saturday energy"};
const LIGHT_CHARACTER_LOCK = `(refined Korean Asian fashion-model beauty atmosphere:1.5),
(mature adult woman, never younger-looking:1.8),
(very fair translucent skin with natural texture:1.6),
(slim elongated face impression:1.45),
(narrow jawline and delicate chin impression:1.45),
(realistic balanced adult proportions:1.6),
(face identity and detailed facial features are taken from the Face Reference image:1.95),
(no different person:1.95),
(no celebrity likeness:1.95)`;
const DEFAULT_CHARACTER_LOCK = LIGHT_CHARACTER_LOCK + `,
(stable same slender I-line body base:1.8),
(compact hips, narrow elegant torso, long slim limbs:1.75)`;
const CHIN_CONTROL = "(neutral chin position:1.92), (chin not thrust forward:1.92), (no jutting chin:1.9), (face kept level or only naturally tilted:1.85), (neck relaxed and not stretched:1.82)";
const opt=(label,key,value,help="")=>({label,key,value,help});
const CHARACTER_MODE_OPTIONS=[opt("📷 OFF / 写真参照のみ","off","off"),opt("✨ LIGHT / 写真参照＋雰囲気","light","light"),opt("🔒 FULL / 従来の固定キャラ","full","full")];
const OUTFIT_REFERENCE_MODE_OPTIONS=[opt("🚫 OFF / 使わない","off","off"),opt("✨ LIGHT / 色・雰囲気だけ","light","light"),opt("👗 FULL / 服装・小物・色を使う","full","full")];
const BASE_POSTURE_OPTIONS=[opt("🎲 おまかせ","auto","auto","シーン文から自然に姿勢を補完します。"),opt("🧍 立っている","standing","standing"),opt("🪑 座っている","seated","seated"),opt("🛋️ 寝転がっている","reclining","reclining")];
const BUST_OPTIONS=[opt("🫧 控えめ","subtle","(normal-size upper-body silhouette through opaque clothing:1.68), (restrained natural bust contour:1.68), (face remains the main focal point:1.88)"),opt("🌿 自然","natural","(natural balanced upper-body garment contour:1.78), (natural bust volume and body line through clothing:1.78), (realistic adult proportions:1.8), (face remains the main focal point:1.88)"),opt("⬆️ 立体感","dimensional","(slightly fuller upper-body silhouette through clothing:1.86), (high-set lifted bust position through clothing:1.88), (firm structured upper-body garment contour:1.86), (face remains primary:1.88)"),opt("🧱 ラインくっきり","defined","(clearly readable upper-body outline through opaque clothing:1.86), (defined bust line and garment contour:1.84), (realistic fabric fit:1.82), (face remains primary:1.88)"),opt("⬆️🧱 立体感＋ライン","both","(slightly fuller and dimensional upper-body silhouette through clothing:1.9), (high-set lifted bust position through clothing:1.9), (defined opaque garment contour around upper body:1.88), (slender I-line body remains narrow and elegant:1.88), (face remains primary:1.9)"),opt("👚 服装なり","outfit","(upper-body silhouette follows the selected outfit naturally:1.8), (fabric thickness, cut, and neckline decide how much shape is visible:1.76), (no forced silhouette beyond outfit design:1.76)")];
const HIP_OPTIONS=[opt("🫧 控えめ","subtle","(subtle compact lower-body silhouette:1.6), (straight narrow waist-to-hip line:1.82), (hips remain small and not laterally wide:1.88)"),opt("🌿 自然","natural","(natural compact lower-body silhouette:1.72), (clean narrow waist-to-hip line:1.84), (hips stay compact, not wide or bulky:1.9)"),opt("🍑 小尻プリ","perky","(compact small hips with a gently rounded shape:1.88), (small but firm perky hip silhouette:1.88), (subtle lifted curve without extra side width:1.86), (not laterally wide hips:1.94)"),opt("🍑⬆️ 小尻アップ","lifted","(compact small hips with a clearly lifted shape:1.9), (small firm upward hip silhouette:1.9), (high-set compact lower-body curve without lateral width:1.88), (not exaggerated:1.92)"),opt("👖 服装なり","outfit","(lower-body silhouette follows the selected outfit naturally:1.8), (pants, skirt, or fabric cut decides how much hip line is visible:1.78), (hips remain compact and not laterally wide:1.9)")];
const WEATHER_OPTIONS=[opt("晴れ ☀️","clear","clear sunny sky, bright natural daylight"),opt("曇り ☁️","cloudy","overcast cloudy sky, cloud-filtered diffused daylight, muted atmosphere"),opt("小雨 🌦️","drizzle","light drizzle rain, wet streets, soft grey ambient light, misty air"),opt("雨 🌧️","rain","steady rain, rain-soaked streets, dark moody wet atmosphere"),opt("雪 ❄️","snow","snow falling, winter white scenery, cold crisp air, soft white light"),opt("霧 🌫️","fog","foggy misty atmosphere, dreamlike hazy soft light")];
const FILM_TONES=[
opt("なし","none","",`フィルムトーンを使わない標準状態です。

向く場面
まずベースを確認したい時。

注意
作品トーンやエフェクトだけで仕上げたい時向けです。`),
opt("コダック ゴールド 200","gold200","Kodak Gold 200 film tone, clearly visible warm golden cast, noticeable analog warmth, lightly visible grain, unmistakable vintage print feel",`暖かく少し懐かしい色味。黄色〜金色寄りの空気感が出ます。

向く場面
夕方、夏、街スナップ、旅行っぽい写真。

注意
寒色クール系より、あたたかい雰囲気向きです。`),
opt("コダック ポートラ 400","portra400","Kodak Portra 400 film tone, clearly visible natural warm skin color, soft contrast, fine grain, unmistakable balanced portrait-film look",`人物向けの定番。肌がきれいで自然、コントラストもやわらかめです。

向く場面
日中ポートレート、街歩き、自然な人物写真。

注意
派手な演出より、安定感重視です。`),
opt("コダック ポートラ 800","portra800","Kodak Portra 800 film tone, clearly visible rich warm skin, creamy highlight rolloff, noticeable film grain, unmistakable premium portrait film look",`夜や暗所でも人物がきれいに見えやすい暖色ポートレート系です。

向く場面
夜景ポートレート、室内、ムード重視の写真。

注意
寒色クールより、少し温かい人物描写に寄ります。`),
opt("コダック エクター 100","ektar100","Kodak Ektar 100 film tone, clearly visible vivid yet clean color reproduction, crisp contrast, ultra-fine grain, unmistakable polished color-film look",`色が鮮やかで、粒子は細かめ。少しカリッとした発色です。

向く場面
青空、花、海、旅行、色を見せたい写真。

注意
やわらかい淡色路線より、色をしっかり見せたい時向きです。`),
opt("フジ プロ 400H","fuji400h","Fuji Pro 400H film tone, clearly visible pastel palette, soft mint-cool shadows, airy film color separation, unmistakable film softness",`淡くて軽い、透明感寄りのフィルム調。ミント寄りの影が少し出ます。

向く場面
白シャツ、窓辺、春夏、透明感のある写真。

注意
ダークで重い雰囲気とは少し逆方向です。`),
opt("フジ スーペリア 400","superia400","Fujifilm Superia 400 film tone, clearly visible lively green-blue color bias, casual snapshot color, medium grain, unmistakable everyday consumer-film feel",`気軽な日常スナップっぽさ。少し青緑寄りで生活感のある写りです。

向く場面
街スナップ、休日、記録写真っぽい雰囲気。

注意
高級感より、日常感が強めです。`),
opt("フジ リアラエース","realaace","Fujifilm Reala Ace film tone, clearly visible clean neutral color reproduction, soft highlight control, gentle film contrast, unmistakable refined modern-film look",`ニュートラルで整った色味。フジ系の自然さを残しつつ上品です。

向く場面
ファッション、街、バランス重視の人物写真。

注意
極端な色演出は弱めです。`),
opt("シネスティル 800T","cinestill800t","CineStill 800T film tone, clearly visible tungsten-balanced cool shadows, glowing highlights, cinematic night color separation, unmistakable urban night-film look",`夜の街灯やネオンと相性が良いシネマ系。青い影と光のにじみが出やすいです。

向く場面
夜景、駅前、ネオン、室内のタングステン光。

注意
昼の自然光ではややクセが強いです。`),
opt("イルフォード HP5","ilfordhp5","Ilford HP5 black and white film, clearly visible monochrome rendering, strong classic contrast, obvious grain texture, unmistakable black-and-white film look",`白黒フィルム調。コントラストと粒子感が見えやすいです。

向く場面
ストリート、陰影重視、クラシックな写真。

注意
色のかわいさ・透明感表現は消えます。`),
opt("ポラロイド","polaroid","Polaroid instant film tone, clearly visible faded instant-film colors, nostalgic warm cast, soft bloom, unmistakable instant snapshot feel",`インスタント写真っぽい、少し褪せたやさしい色味です。

向く場面
思い出写真、部屋、やわらかい日常スナップ。

注意
シャープさや現代的なキレより、雰囲気重視です。`),
opt("ローモ","lomo","Lomography vivid tone, clearly visible cross-processed colors, strong saturation shift, lo-fi contrast, vignette edges, unmistakable lomo look",`クセのある発色と周辺落ちで、ローファイ感が強いです。

向く場面
夜スナップ、遊びのある写真、ストリート。

注意
透明感・自然肌とは少し逆方向です。`),
opt("シネスコープ","cinemascope","CinemaScope film tone, clearly visible teal and orange grade, cinematic color separation, anamorphic blockbuster look, unmistakable movie-like grading",`映画っぽいティール&オレンジ寄りの色分離。作り込んだムードが出ます。

向く場面
夜景、ドラマティックな屋外、シネマ風ポートレート。

注意
暖色の素朴なフィルム感とは少しぶつかります。`),
opt("ヴィンテージ 90s","vintage90s","1990s vintage film tone, clearly visible retro color shift, muted warm mid-tones, nostalgic softness, unmistakable 90s film-photo mood",`90年代っぽい色ズレと少し眠い発色。懐かしい空気感が出ます。

向く場面
レトロ、日常、コンデジ/VHS系と合わせたい時。

注意
現代的なクリア感は少し弱まります。`),
opt("ガサつき","gritty","gritty rough film tone, clearly visible coarse texture and dry roughness, pronounced gritty surface feel, raw unpolished analog mood, unmistakably harsh tactile photo texture",`ザラつき・乾いた粗さ・アナログ感を強く出します。

向く場面
ストリート、夜、粗い質感を見せたい写真。

注意
透明感ややわらかさとは逆方向です。`)
];
const OVERALL_TONES=[opt("なし","none",""),opt("クール / モダン","cool","cool modern aesthetic, crisp clean image design, urban sophisticated mood"),opt("キュート / 柔らか","cute","cute soft aesthetic, gentle pastel atmosphere, soft warm friendliness"),opt("ダーク / ムーディ","dark","dark moody aesthetic, deeper shadows, brooding emotional atmosphere"),opt("ナチュラル / 透明感","transparent","natural transparent beauty aesthetic, fresh clean look, airy brightness"),opt("エレガント / 上品","elegant","elegant refined aesthetic, graceful composition, polished sophistication"),opt("ストリート / エッジ","street","street edge aesthetic, raw urban energy, gritty authentic mood"),opt("ロマンティック","romantic","romantic dreamy aesthetic, soft warm glow, tender emotional atmosphere"),opt("ミニマル / 静寂","minimal","minimal quiet aesthetic, restrained negative-space calm")];
const EFFECTS=[
opt("🌫️ 背景ボケ","bokeh","(portrait-safe moderate background blur:1.66), (background softly blurred but still readable as a real place:1.68), (moderate depth separation without cutout look:1.7)","背景をほどよくぼかします。場所感は残します。"),
opt("✨ 光の玉ボケ","orb","(clearly visible light orb bokeh:1.8), (ambient light circles in background:1.8), (noticeable specular bokeh highlights:1.8)","背景光を丸い玉ボケにします。夜景・ロビー照明向き。"),
opt("✨ 前ボケ","foreground","(soft out-of-focus foreground bokeh in front of the subject:1.74), (layered depth with foreground bokeh and readable background:1.72)","手前に軽いボケを入れて奥行きを出します。"),
opt("💧 水滴/結露感","droplet","(subtle condensation droplets on glass or foreground:1.68), (noticeable water droplet texture where physically appropriate:1.66)","雨・窓・ガラス向き。肌に直接寄せすぎない設定。"),
opt("✨ きらめき粒子","sparkle","(clearly visible sparkling light particles in air:1.7), (noticeable shimmering particles:1.68)","空気中の小さなキラキラ。SNS加工寄り。"),
opt("🌁 ソフトフォーカス","softfocus","(soft focus haze:1.68), (gentle dreamy blur on edges:1.66), (diffused hazy atmosphere:1.66)","輪郭を柔らかくします。"),
opt("🌙 逆光/リムライト","rim","(clearly visible backlighting:1.78), (rim light on hair and shoulders:1.78), (silhouette-edge glow:1.68)","髪や肩の輪郭光。"),
opt("📼 VHSノイズ","vhs","(VHS scan lines:1.68), (retro analog video noise:1.66), (chromatic aberration:1.66)","レトロ映像っぽいノイズ。顔崩れに注意。"),
opt("🔥 暖色フレア","warmflare","(warm lens flare:1.76), (golden warm flare streaks across frame:1.72)","夕方・暖色ライト向き。"),
opt("❄️ 冷色フィルター","coolfilter","(cool blue color grading:1.76), (cold tone filter:1.72)","夜・クール・雨向き。"),
opt("🌈 光漏れ","lightleak","(light leak effect:1.75), (film light leak streaks across frame:1.72)","フィルムの光漏れ。"),
opt("🖤 ビネット","vignette","(subtle vignette:1.66), (dark edge falloff around frame:1.64)","四隅を少し暗くして中心に視線を集めます。"),
opt("🎞️ フィルムグレイン強め","grain","(visible film grain:1.75), (analog grain texture:1.72)","粒状感。強すぎると肌が荒れます。"),
opt("⚡ 直フラッシュ","flash","(direct on-camera flash look:1.86), (front-facing flash illumination with bright hit:1.78), (snapshot flash aesthetic:1.76)","夜スナップ・コンデジ感向き。"),
opt("🌃 ネオン反射","neon","(neon reflections on nearby glass or polished surfaces:1.72), (urban neon color accents in background:1.7)","夜の街・ガラス反射向き。"),
opt("🪞 ガラス反射","glass","(subtle glass reflection layer:1.72), (faint reflected city lights or window reflections:1.68), (through-glass photographic texture:1.64)","窓・ビル・ロビー向き。"),
opt("🏃 モーションブラー","motionblur","(subtle handheld motion blur:1.62), (realistic candid movement blur:1.6)","歩き・スナップ感。顔までブレすぎない程度。"),
opt("📸 コンデジ感","digicam","(compact digital camera snapshot look:1.76), (slightly crunchy digital flash-era texture:1.7), (early-2000s casual digicam rendering:1.68)","コンデジで撮ったようなスナップ感。"),
opt("🩶 低彩度","desat","(muted desaturated color palette:1.72), (reduced saturation with realistic skin tone preserved:1.68)","落ち着いた色。"),
opt("📱 スマホHDR","hdr","(smartphone HDR rendering:1.74), (clean dynamic range and lifted shadows:1.72)","スマホ写真っぽく明暗を整えます。")
];
const EFFECT_STRENGTH_OPTIONS=[opt("🫧 控えめ","subtle","subtle","") ,opt("✨ 標準","standard","standard",""),opt("🌟 強め","strong","strong",""),opt("💥 盛り盛り","max","max","")];
const EFFECT_MULT={subtle:.9,standard:1,strong:1.12,max:1.25};
const SKIN_FINISH_OPTIONS=[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(real skin texture:1.82), (natural skin finish:1.8), (balanced skin sheen:1.74)"),opt("💧 しっとり","moist","(soft moisturized skin finish:1.82), (subtle healthy skin sheen:1.78), (supple hydrated skin appearance:1.76)"),opt("✨ ツヤあり","dewy","(noticeable dewy skin finish:1.84), (soft glossy highlights on skin:1.8), (healthy luminous skin sheen:1.78)")];
const CLOSEUP_TEXTURE_OPTIONS=[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(natural realistic close-up detail balance:1.78), (skin detail clear without overprocessing:1.76)"),opt("💧 しっとり","moist","(close-up skin looks softly moisturized and realistic:1.82), (lips and skin retain subtle hydrated softness:1.78)"),opt("🔬 高精細","detailed","(high-detail close-up rendering of eyelashes, lips, pores, and fine skin texture:1.86), (macro-like facial detail while keeping realism:1.84)")];
const SELFIE_MODE_OPTIONS=[opt("🎲 自動 / おまかせ","auto","auto"),opt("🤳 自撮り ON","on","on"),opt("📷 自撮り OFF / 第三者撮影","off","off")];
const ANGLES=[
opt("🎲 おまかせ","auto","auto"),
opt("👁️ 目線","eye","(camera at eye height:1.9), (relaxed direct selfie or portrait perspective:1.82), (minimal perspective distortion:1.76), "+CHIN_CONTROL),
opt("✨ 盛れ角","golden","(camera slightly above eye level looking down:1.9), (flattering mild high angle:1.82), (not an overhead selfie:1.85), "+CHIN_CONTROL),
opt("⬆️ 少し上から","high","(camera clearly above eye level:1.84), (gentle high-angle portrait perspective:1.82), (natural face angle without excessive chin lift:1.86), "+CHIN_CONTROL),
opt("🙆 頭上から","overhead","(true overhead super high-angle selfie:1.9), (arm fully extended above head when selfie mode is active:1.86), (bird's-eye framing of face, shoulders, outfit, and floor/space:1.84), (not eye-level and not low-angle:1.9), "+CHIN_CONTROL),
opt("🤫 腰だめ","hiddenWaist","(true hidden waist-held selfie:2.0), (smartphone held discreetly against her waist or lower torso:2.0), (elbow bent tightly and close to the body:2.0), (short folded arm, not extended toward the camera:2.0), (camera viewpoint originates very close to lower torso or waist:2.0), (lens angled slightly upward along the body line toward the face, not vertical:1.98), (torso feels close to the lens without extreme distortion:1.86), (no arm's-length selfie pose:2.0), (no long stretched arm selfie:2.0), (no raised-hand selfie:2.0), (not a normal pretty high-angle selfie:2.0), "+CHIN_CONTROL,"腰付近で体の近くに持つ隠し持ち自撮り。普通の腕上げ自撮りを防ぎたい時。"),
opt("⬇️ 低め前持ち","lowFront","(ordinary low-angle selfie from in front of the body:1.84), (phone held slightly below chest level:1.84), (camera below the face and angled mildly upward from the front:1.82), (not overhead and not waist-hidden:1.86), "+CHIN_CONTROL),
opt("📉 強い煽り","superLow","(dramatic super low-angle selfie or portrait:1.9), (phone or camera held very low below waist or near hip-to-thigh level:1.9), (strong upward perspective from far below the face:1.86), (not overhead, not golden angle:1.9), "+CHIN_CONTROL),
opt("➡️ 真横から","side","(camera positioned at true side of the subject:1.9), (lateral face or body line readable:1.86), (side-profile or near-profile portrait geometry:1.84), "+CHIN_CONTROL),
opt("↩️ 振り向き","overShoulder","(over-shoulder or turn-back portrait:1.88), (shoulder turned toward camera, face looking back naturally:1.84), "+CHIN_CONTROL),
opt("🚶 歩き","walking","(captured mid-walk:1.82), (subtle body motion:1.76), (hair and outfit move naturally:1.74), "+CHIN_CONTROL),
opt("🌀 斜め","tilted","(slightly diagonal handheld composition:1.78), (off-center snapshot atmosphere:1.74), "+CHIN_CONTROL)
];
const VISIBLE_RANGE_OPTIONS=[opt("⚖️ バランス","balanced","(balanced portrait composition with face, upper body, and believable context:1.82)"),opt("🙂 顔のみ","faceOnly","(face-only portrait crop:1.92), (only the face is the image subject:1.9), (crop from slightly above forehead to around chin or just above neck:1.88), (shoulders, chest, outfit, and background are minimal:1.86)"),opt("🧿 顔どアップ","extremeFace","(extreme face close-up composition:1.98), (face fills almost the entire frame:1.96), (eyes, lips, skin texture, and hairline dominate:1.9), (background barely visible:1.86)"),opt("🔍 顔アップ","faceCloseup","(close-up face composition:1.92), (face fills most of the frame:1.9), (hair, neck, and slight shoulder may appear:1.82)"),opt("↔️ 横顔アップ","profileCloseup","(profile close-up composition:1.94), (side face line, eye, nose bridge, lips, and cheek contour clearly readable:1.9)"),opt("🙂 顔〜肩","headShoulder","(head-and-shoulders portrait framing:1.88), (face, hair, neck, and shoulders are visible:1.86)"),opt("🧥 上半身","upperBody","(upper-body portrait composition:1.88), (head to chest or waist area visible:1.86), (face and outfit both readable:1.86)"),opt("🧍 腰上","waistUp","(waist-up portrait framing:1.92), (head to waist or upper-hip area visible:1.9), (face, body line, and outfit coordination readable:1.88)"),opt("🧍 全身","fullBody","(full-body portrait framing:1.88), (entire outfit and standing balance visible:1.86), (face remains readable but body and clothing are important:1.82)")];
const CAMERA_ROLL_OPTIONS=[opt("🎲 おまかせ","auto","(camera roll remains natural and unobtrusive:1.7)"),opt("📐 水平","level","(camera roll is level and horizon stays straight:1.86)"),opt("／ 少し斜め","slight","(slight diagonal camera roll only:1.84), (frame rotation must not change the selected angle type:1.9)"),opt("／／ 斜め強め","strong","(clearly diagonal camera roll:1.88), (intentional tilted snapshot composition:1.84), (roll affects frame rotation only:1.9)")];
const FACE_DIRECTION_OPTIONS=[opt("🎲 おまかせ","auto","(face orientation is naturally derived from scene and selected angle:1.74)"),opt("🙂 正面","front","(front-facing or near-front facial orientation:1.84)"),opt("◢ 斜め向き","threeQuarter","(three-quarter facial angle:1.86), (face turned about 20 to 45 degrees from camera:1.82)"),opt("➡️ 横顔","profile","(true side-profile or near-profile facial orientation:1.9), (lateral face line clearly readable:1.86)"),opt("↩️ 振り向き","turnBack","(looking back over shoulder or gentle turned-back facial orientation:1.9)"),opt("🙈 顔を見せない","away","(face turned away and not presented to camera:1.92)")];
const GAZE_OPTIONS=[opt("🎲 おまかせ","auto","(gaze naturally derived from scene, emotion, and angle:1.72)"),opt("👀 カメラ目線","camera","(eyes naturally meet the lens:1.84), (clear camera-aware gaze:1.82)"),opt("↗️ 少し視線を外す","off","(gaze is slightly off-camera:1.84), (natural off-axis eye line:1.8)"),opt("🌌 遠くを見る","far","(gaze directed into the distance, not at camera:1.86)"),opt("😌 伏し目","down","(downward or lowered gaze:1.84), (soft eyelids and lowered eye line:1.82)")];
const BACKGROUND_VIEW_MODES=[opt("🚫 指定なし","none",""),opt("🫧 控えめ","subtle","(background remains secondary and understated:1.7), (subject stays visually dominant over background:1.8)"),opt("🌆 バランス","balanced","(background shown in a balanced natural way:1.75), (subject and place both readable:1.75)"),opt("🌸 下 / 足元側","lower","(lower background is visible when framing allows:1.78), (ground, pavement, floor, or lower-side details support the scene:1.74)"),opt("☕ 奥","depth","(depth background behind the subject clearly visible:1.78), (show the lobby, street, storefront, or scenery behind the subject:1.76)"),opt("🌙 上","upper","(upper background visible when framing allows:1.78), (show ceiling, signs, sky, or upper building area:1.74)")];
const FRAMING_MODES=[opt("⚖️ 標準","standard","(balanced subject scale with moderate breathing room:1.7), (natural crop with some surrounding space:1.7)"),opt("🧍 余白少なめ","tight","(tight framing with reduced empty space:1.8), (subject occupies most of the frame:1.8)"),opt("🖼️ 余白なし / 被写体いっぱい","full","(little to no leading space:1.9), (subject fills the image as much as possible:1.9), (minimal empty background:1.86)"),opt("🏙️ 余白あり / 場所も見せる","wide","(clear breathing room around the subject:1.78), (environment intentionally readable:1.78)")];
const PHOTO_STYLE_MODES=[opt("📷 リアルな日常自撮り","daily","(real everyday selfie or snapshot feel:1.86), (candid daily-life realism:1.8), (slight imperfection allowed:1.7)"),opt("🙂 少し盛れた自然写真","enhanced","(naturally flattering portrait look:1.84), (slightly polished but still believable:1.82), (natural but intentionally attractive:1.8)"),opt("🧍 モデルっぽい","model","(model-like posing and facial control:1.82), (deliberate shoulder line and body angle:1.8)"),opt("🖤 ファッション誌っぽい","editorial","(fashion editorial photography feel:1.88), (magazine-style image design:1.82)"),opt("🎬 作り込み強め","strong","(strongly directed visual presentation:1.84), (noticeably composed and produced look:1.82)")];
const TENSIONS=[opt("😌 低め","low","low"),opt("🙂 普通","medium","medium"),opt("😄 やや高め","mediumHigh","medium-high"),opt("🤩 高め","high","high")];
const EMOTIONS=[opt("🎲 おまかせ","auto",""),opt("😐 ニュートラル","neutral","neutral"),opt("😊 嬉しい","happy","happy"),opt("😆 楽しい","joyful","joyful"),opt("😌 落ち着き","calm","calm"),opt("🌙 寂しい","lonely","lonely"),opt("😩 疲れた","tired","tired"),opt("😳 照れ","shy","shy"),opt("😟 不安","anxious","anxious"),opt("😎 クール","cool","cool")];
const EXPRESSION_OPTIONS=[opt("🎲 自動","auto",""),opt("😐 真顔/クール","neutral","neutral deadpan, calm, composed expression"),opt("🙂 優しい微笑み","smile","soft gentle smile, warm and approachable expression"),opt("😄 明るい笑顔","happy","bright happy, lively cheerful expression"),opt("😆 めっちゃ嬉しそう","veryHappy","very happy joyful smile, bright expressive eyes, clearly delighted expression"),opt("😌 物憂げ","melancholic","melancholic, reflective, subtle loneliness in expression"),opt("😪 気だるげ","sleepy","tired but gentle, quiet fatigue expression"),opt("☺️ 照れ/はにかみ","shy","shy blushing expression")];
let state={characterMode:"light",outfitReferenceMode:"off",basePosture:"auto",bust:"both",hip:"perky",weather:"",film:"",tone:"",effects:[],effectStrength:"standard",skinFinish:"",closeupTexture:"",selfieMode:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"standard",photoStyle:"daily",tension:"",emotion:"",expression:""};
function getTokyoNow(){const now=new Date();const jst=new Date(now.toLocaleString("en-US",{timeZone:"Asia/Tokyo"}));const days=["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];const list=[{h:[0,5],label:"深夜",en:"late night",mood:"melancholic quiet solitude, exhausted calm"},{h:[5,9],label:"早朝",en:"early morning",mood:"serene fresh morning calm"},{h:[9,12],label:"午前",en:"late morning",mood:"composed focused morning clarity"},{h:[12,14],label:"昼",en:"noon",mood:"bright casual midday energy"},{h:[14,17],label:"午後",en:"afternoon",mood:"relaxed comfortable afternoon drift"},{h:[17,20],label:"夕方",en:"evening",mood:"warm golden-hour nostalgia"},{h:[20,23],label:"夜",en:"night",mood:"intimate night warmth"},{h:[23,24],label:"深夜",en:"midnight",mood:"deep night solitude"}];const hour=jst.getHours();const timeCtx=list.find(x=>hour>=x.h[0]&&hour<x.h[1])||list[0];return{month:jst.getMonth()+1,day:days[jst.getDay()],hour,minute:jst.getMinutes(),timeStr:jst.toLocaleTimeString("ja-JP",{hour:"2-digit",minute:"2-digit"}),timeCtx};}
function updateClock(){const t=getTokyoNow();document.getElementById("hTime").textContent=t.timeStr+" JST";document.getElementById("hDay").textContent=t.day+" · "+t.month+"月 · "+t.timeCtx.label;document.getElementById("infoDay").innerHTML="<span class='info-val'>"+t.day+" / "+t.month+"月 / "+t.timeCtx.label+"（"+t.timeCtx.en+"）</span>";document.getElementById("infoTime").innerHTML="<span class='info-val'>"+t.timeStr+" JST</span>";document.getElementById("infoDayMood").textContent=DAY_MOOD[t.day];document.getElementById("infoHair").textContent=HAIR_BY_MONTH[t.month];}
function bindChipHelp(btn,item){if(!item.help)return;btn.classList.add("has-help");let timer=null,long=false;const start=ev=>{long=false;timer=setTimeout(()=>{long=true;showChipHelp(item.label,item.help);if(ev&&ev.cancelable)ev.preventDefault();},520)};const cancel=()=>{if(timer)clearTimeout(timer);timer=null};btn.addEventListener("touchstart",start,{passive:false});btn.addEventListener("touchend",cancel);btn.addEventListener("touchcancel",cancel);btn.addEventListener("mousedown",start);btn.addEventListener("mouseup",cancel);btn.addEventListener("mouseleave",cancel);btn.addEventListener("contextmenu",ev=>{ev.preventDefault();showChipHelp(item.label,item.help)});btn.addEventListener("click",ev=>{if(long){ev.preventDefault();ev.stopPropagation();long=false}},true)}
function showChipHelp(title,body){document.getElementById("chipHelpTitle").textContent=title.replace(/^[^\w一-龯ぁ-んァ-ヶ]+/u,"").trim()||title;document.getElementById("chipHelpBody").textContent=body;document.getElementById("chipHelpOverlay").classList.remove("hidden")}function hideChipHelp(){document.getElementById("chipHelpOverlay").classList.add("hidden")}
function getItems(key){return({characterMode:CHARACTER_MODE_OPTIONS,outfitReferenceMode:OUTFIT_REFERENCE_MODE_OPTIONS,basePosture:BASE_POSTURE_OPTIONS,bust:BUST_OPTIONS,hip:HIP_OPTIONS,weather:WEATHER_OPTIONS,film:FILM_TONES,tone:OVERALL_TONES,effectStrength:EFFECT_STRENGTH_OPTIONS,skinFinish:SKIN_FINISH_OPTIONS,closeupTexture:CLOSEUP_TEXTURE_OPTIONS,selfieMode:SELFIE_MODE_OPTIONS,angleMode:ANGLES,visibleRange:VISIBLE_RANGE_OPTIONS,cameraRoll:CAMERA_ROLL_OPTIONS,faceDirection:FACE_DIRECTION_OPTIONS,gaze:GAZE_OPTIONS,backgroundView:BACKGROUND_VIEW_MODES,framing:FRAMING_MODES,photoStyle:PHOTO_STYLE_MODES,tension:TENSIONS,emotion:EMOTIONS,expression:EXPRESSION_OPTIONS})[key]||[]}
function find(key){return getItems(key).find(x=>x.key===state[key]||x.value===state[key])||getItems(key)[0]||{label:"",value:""}}
function renderChips(id,items,key){const el=document.getElementById(id); if(!el)return; el.innerHTML="";items.forEach(item=>{const active=state[key]===item.key||state[key]===item.value;const btn=document.createElement("button");btn.className="chip"+(active?" active":"");btn.textContent=item.label;btn.onclick=()=>{state[key]=active?defaultFor(key):item.key; if(key==="characterMode")resetCharacterLock(); renderAllOptionChips();};bindChipHelp(btn,item);el.appendChild(btn)})}
function renderMultiChips(id,items,key){const el=document.getElementById(id); if(!el)return; el.innerHTML="";items.forEach(item=>{const active=state[key].includes(item.key);const btn=document.createElement("button");btn.className="chip"+(active?" active":"");btn.textContent=item.label;btn.onclick=()=>{const idx=state[key].indexOf(item.key); if(idx<0)state[key].push(item.key); else state[key].splice(idx,1); renderAllOptionChips();};bindChipHelp(btn,item);el.appendChild(btn)})}
function defaultFor(key){return{characterMode:"light",outfitReferenceMode:"off",basePosture:"auto",bust:"",hip:"",weather:"",film:"",tone:"",effectStrength:"standard",skinFinish:"",closeupTexture:"",selfieMode:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"standard",photoStyle:"daily",tension:"",emotion:"",expression:""}[key]||""}
function renderAllOptionChips(){renderChips("characterModeChips",CHARACTER_MODE_OPTIONS,"characterMode");renderChips("outfitReferenceModeChips",OUTFIT_REFERENCE_MODE_OPTIONS,"outfitReferenceMode");renderChips("basePostureChips",BASE_POSTURE_OPTIONS,"basePosture");renderChips("bustChips",BUST_OPTIONS,"bust");renderChips("hipChips",HIP_OPTIONS,"hip");renderChips("weatherChips",WEATHER_OPTIONS,"weather");renderChips("filmChips",FILM_TONES,"film");renderChips("toneChips",OVERALL_TONES,"tone");renderMultiChips("effectChips",EFFECTS,"effects");renderChips("effectStrengthChips",EFFECT_STRENGTH_OPTIONS,"effectStrength");renderChips("skinFinishChips",SKIN_FINISH_OPTIONS,"skinFinish");renderChips("closeupTextureChips",CLOSEUP_TEXTURE_OPTIONS,"closeupTexture");renderChips("selfieModeChips",SELFIE_MODE_OPTIONS,"selfieMode");renderChips("angleModeChips",ANGLES,"angleMode");renderChips("visibleRangeChips",VISIBLE_RANGE_OPTIONS,"visibleRange");renderChips("cameraRollChips",CAMERA_ROLL_OPTIONS,"cameraRoll");renderChips("faceDirectionChips",FACE_DIRECTION_OPTIONS,"faceDirection");renderChips("gazeChips",GAZE_OPTIONS,"gaze");renderChips("backgroundViewChips",BACKGROUND_VIEW_MODES,"backgroundView");renderChips("framingChips",FRAMING_MODES,"framing");renderChips("photoStyleChips",PHOTO_STYLE_MODES,"photoStyle");renderChips("tensionChips",TENSIONS,"tension");renderChips("emotionChips",EMOTIONS,"emotion");renderChips("expressionChips",EXPRESSION_OPTIONS,"expression")}
function resetCharacterLock(){document.getElementById("characterLock").value=state.characterMode==="off"?"":state.characterMode==="full"?DEFAULT_CHARACTER_LOCK:LIGHT_CHARACTER_LOCK}
function scaleWeightedPrompt(prompt,m){return (prompt||"").replace(/\(([^()]+?):([0-9]*\.?[0-9]+)\)/g,(match,body,w)=>`(${body}:${Math.round(Math.min(Math.max(parseFloat(w)*m,.1),3)*100)/100})`)}
function pickAngle(){if(state.angleMode!=="auto")return find("angleMode");const vr=state.visibleRange;const pool=vr==="extremeFace"||vr==="faceOnly"||vr==="faceCloseup"?["eye","golden","high"]:vr==="waistUp"||vr==="upperBody"?["eye","hiddenWaist","lowFront","tilted"]:["eye","hiddenWaist","walking","tilted"];return ANGLES.find(a=>a.key===pool[Math.floor(Math.random()*pool.length)])||ANGLES[1]}
function effectiveSelfie(scene){if(state.selfieMode==="on"||state.selfieMode==="off")return state.selfieMode;if(/他撮り|第三者|非自撮り|セルフィーじゃない|自撮りじゃない|撮ってもら|third-person|non-selfie/i.test(scene))return"off";return"on"}
function characterBlock(){const fixed=document.getElementById("characterLock").value.trim();if(state.characterMode==="off")return"(fixed character text disabled; use first image for identity only:1.95)";return fixed||LIGHT_CHARACTER_LOCK}
function outfitBlock(){if(state.outfitReferenceMode==="off")return"";if(state.outfitReferenceMode==="light")return`OUTFIT REFERENCE — LIGHT:\n(use the second attached image only for outfit color palette, styling mood, and rough garment impression:1.9),\n(do not copy the second image face, body, pose, camera, or background:1.95)`;return`OUTFIT REFERENCE — FULL:\nImage B is the outfit reference only.\nUse Image B exclusively for:\n- clothing type\n- outfit coordination\n- layering\n- materials\n- colors\n- shoes\n- bag\n- accessories\n- styling direction\n- color palette\n- written outfit notes such as POINT and STYLE POINT when present\n\nDo not use Image B for anything else.\n\nAbsolutely do not copy from Image B:\n- face\n- body type\n- hairstyle\n- pose\n- hand position\n- camera angle\n- composition\n- background\n- location\n- lighting\n- facial expression\n- mood unrelated to outfit\n\nIgnore all non-outfit information in Image B.\nImage B must control the outfit only, and must not control identity or scene construction.\n(if the second image is a coordinate sheet, read its filled item boxes, item names, accessories, color palette, POINT, and STYLE POINT as outfit instructions:1.98),\n(ignore coordinate-sheet borders, template layout, title typography, decorative lines, and empty boxes as scene objects:1.98),\n(never reuse a previous coordinate sheet, cached outfit, sample outfit, or earlier conversation outfit:2.0)`}
function cameraModeBlock(selfie,angleKey){if(selfie==="off")return`CAMERA MODE — NON-SELFIE / THIRD-PERSON PHOTO:\n(non-selfie portrait photo:1.95),\n(third-person external camera viewpoint:1.95),\n(subject is not holding the active camera:1.95),\n(no smartphone selfie POV, no selfie arm, no front-camera perspective:1.95)`;if(angleKey==="hiddenWaist")return`CAMERA MODE — HIDDEN WAIST-HELD SELFIE:\n(smartphone in her hand is the active camera:1.95),\n(viewpoint must match her discreet waist-held smartphone:1.98),\n(phone is held close to waist or lower torso, not raised above shoulder:2.0),\n(short lowered arm and elbow close to body:1.98),\n(no arm's-length selfie, no long foreground arm, no raised-hand selfie:2.0),\n(perspective must feel like a close-body waist-held selfie, not a normal pretty high-angle selfie:2.0)`;return`CAMERA MODE — SELFIE:\n(smartphone in her hand is the active front camera:1.9),\n(viewpoint follows the selected camera position / angle preset:1.9),\n(no third-person shot unless self-shot is OFF:1.9),\n(do not copy the reference image camera angle or arm extension:1.9)`}
function expressionValue(scene){if(state.expression)return find("expression").value;if(/めっちゃ嬉し|すごく嬉し|嬉しそう|happy|joyful/i.test(scene))return"very happy joyful smile, bright expressive eyes, clearly delighted expression";if(state.emotion)return find("emotion").value+" natural expression";return"natural context-driven expression"}
function buildPrompt(){const t=getTokyoNow();const sceneRaw=document.getElementById("situation").value.trim()||"No scene details provided. Create a realistic everyday portrait scene.";const angle=pickAngle();const selfie=effectiveSelfie(sceneRaw);const fxMult=EFFECT_MULT[state.effectStrength]||1;const effects=state.effects.map(k=>EFFECTS.find(e=>e.key===k)).filter(Boolean).map(e=>scaleWeightedPrompt(e.value,fxMult));const posture=find("basePosture").key;const posturePrompt=posture==="standing"?"(mandatory base posture is standing:1.92), (natural standing balance:1.86)":posture==="seated"?"(mandatory base posture is seated:1.92), (hips visibly supported by chair, sofa, floor, or bench:1.88)":posture==="reclining"?"(mandatory base posture is reclining or lying down:1.92), (body visibly supported by bed, sofa, or floor:1.88)":"(base posture is derived from the scene without forcing generic standing:1.78)";const weather=find("weather").value;const film=find("film").value;const tone=find("tone").value;const blocks=[];blocks.push(`APP_VERSION: ${APP_VERSION}\nPROMPT_ENGINE: angle-core + reference reading + visible-range + style/effects\nCAMERA_ENGINE: angle-preset, not micro physical controls`);
blocks.push(`REFERENCE IMAGES — STRICT HARD CONSTRAINTS:\nImage A is the identity/bodyline reference only.\nUse Image A exclusively for:\n- face identity\n- facial features\n- facial proportions\n- skin tone\n- bust presence / chest impression\n- shoulder width\n- torso narrowness\n- waist position\n- compact hip width\n- visible limb slimness\n\nDo not use Image A for anything else.\n\nAbsolutely do not copy from Image A:\n- clothing\n- outfit details\n- styling\n- accessories\n- hairstyle\n- pose\n- hand or arm position\n- camera angle\n- composition\n- background\n- location\n- lighting\n- mood props\n- any scene objects\n\nIgnore all non-identity, non-bodyline information in Image A.\nThe clothing visible in Image A must never appear in the generated image.\nImage A must not influence outfit generation in any way.`);
blocks.push(`CHARACTER LOCK MODE:\n${find("characterMode").label}\n${characterBlock()}`);
const ob=outfitBlock(); if(ob)blocks.push(ob);
blocks.push(`HAIR — APP MONTHLY PRIORITY:\n${HAIR_BY_MONTH[t.month] || ""},\n(monthly hairstyle overrides the hairstyle in the first reference image:1.98),\n(use the first image for face identity, not hair length, parting, volume, or silhouette:1.98)`);
blocks.push(`SAFETY / REALISM:\n(safe non-sexual adult fashion portrait:1.95),\n(opaque public-safe clothing, no lingerie or fetish styling:1.95),\n(photographic realism, real skin texture, believable lighting and shadows:1.9),\n(no anime, no illustration, no plastic skin, no waxy beauty-filter look:1.9)`);
blocks.push(`SCENE:\n${sceneRaw}\n(scene text controls location, outfit notes, action, support, and expression detail, but not face identity, monthly hair, or selected angle preset:1.9)`);
blocks.push(`POSTURE:\n${posturePrompt}`);
blocks.push(`CAMERA MODE:\n${cameraModeBlock(selfie,angle.key)}`);
blocks.push(`CAMERA POSITION / ANGLE — ${angle.label}:\n${angle.value}`);
blocks.push(`VISIBLE RANGE:\n${find("visibleRange").value}`);
blocks.push(`IMAGE TILT / CAMERA ROLL:\n${find("cameraRoll").value}`);
blocks.push(`FACE / GAZE:\n${find("faceDirection").value}\n${find("gaze").value}`);
blocks.push(`COMPOSITION:\n${find("backgroundView").value}\n${find("framing").value}\n${find("photoStyle").value}\n(selected camera angle preset, visible range, face direction, gaze, roll, background, and framing must work together as one portrait composition:1.88),\n(do not replace a difficult waist-held or low-angle preset with a normal pretty high-angle selfie:1.95)`);
blocks.push(`EXPRESSION / MOOD:\n(${expressionValue(sceneRaw)}:1.9),\n(context-driven natural micro-expression matching scene, time, weather, and emotion:1.78)`);
blocks.push(`BODY / OUTFIT SILHOUETTE:\n${find("bust").value || BUST_OPTIONS[4].value}\n${find("hip").value || HIP_OPTIONS[2].value}\n(face remains primary focal point while the selected outfit silhouette is preserved:1.88)`);
const skin=find("skinFinish").value; const close=find("closeupTexture").value; if(skin)blocks.push(`SKIN FINISH:\n${skin}`); if(close)blocks.push(`CLOSE-UP TEXTURE:\n${close}`);
blocks.push(`STYLE / EFFECTS — APPLY LAST:\nCurrent time: ${t.timeCtx.label} (${t.timeCtx.en}), ${t.timeStr} JST\nDay mood: ${DAY_MOOD[t.day]}\nTime-of-day mood: ${t.timeCtx.mood}\n${weather?"Weather: "+weather:""}\n${film?"Film tone: "+film:""}\n${tone?"Overall tone: "+tone:""}\n${effects.length?"Effects: "+effects.join(", "):""}\n(apply film tone, color treatment, blur, grain, light, and texture only after the portrait composition is solved:1.88)`);
blocks.push(`ASPECT / ENVIRONMENT:\n(vertical 9:16 smartphone image:1.6),\n(real location matching the written scene, believable people, signs, lighting, and depth:1.75),\n(realistic ambient lighting and natural handheld micro-shake:1.65)`);
return blocks.filter(Boolean).join("\n\n");}
function handleGenerate(){const prompt=buildPrompt();document.getElementById("metaCard").classList.remove("hidden");document.getElementById("outputCard").classList.remove("hidden");document.getElementById("outputArea").value=prompt;document.getElementById("metaContent").innerHTML=[`🧩 <b style='color:#c4b5fd'>App</b>：${APP_VERSION}`,`👗 <b style='color:#c4b5fd'>コーデ参照</b>：${find("outfitReferenceMode").label}`,`📸 <b style='color:#c4b5fd'>アングル</b>：${pickAngle().label}`,`🖼️ <b style='color:#c4b5fd'>写す範囲</b>：${find("visibleRange").label}`,`📐 <b style='color:#c4b5fd'>画面の傾き</b>：${find("cameraRoll").label}`,`🎞️ <b style='color:#c4b5fd'>フィルム</b>：${find("film").label||"未選択"}`,`✨ <b style='color:#c4b5fd'>エフェクト</b>：${state.effects.length?state.effects.map(k=>EFFECTS.find(e=>e.key===k)?.label).join("、"):"未選択"}`,`🔒 <b style='color:#c4b5fd'>後処理</b>：weight削除なし / 重複削除なし`].join("<br>");copyPromptToClipboard(true);document.getElementById("outputCard").scrollIntoView({behavior:"smooth"})}
function handleCopy(){copyPromptToClipboard(false)}
function copyPromptToClipboard(auto=false){const ta=document.getElementById("outputArea");if(!ta||!ta.value)return;ta.focus();ta.select();ta.setSelectionRange(0,ta.value.length);const ok=()=>showCopied(auto);const fallback=()=>{try{if(document.execCommand("copy"))ok()}catch(e){}};if(navigator.clipboard&&navigator.clipboard.writeText){navigator.clipboard.writeText(ta.value).then(ok).catch(fallback)}else fallback()}
function showCopied(auto=false){const btn=document.getElementById("btnCopy");btn.textContent=auto?"✓ 自動コピー済み":"✓ コピー済み";btn.classList.add("copied");setTimeout(()=>{btn.textContent="コピー";btn.classList.remove("copied")},2500)}
function handleReset(){state={characterMode:"light",outfitReferenceMode:"off",basePosture:"auto",bust:"both",hip:"perky",weather:"",film:"",tone:"",effects:[],effectStrength:"standard",skinFinish:"",closeupTexture:"",selfieMode:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"standard",photoStyle:"daily",tension:"",emotion:"",expression:""};document.getElementById("situation").value="";document.getElementById("metaCard").classList.add("hidden");document.getElementById("outputCard").classList.add("hidden");document.getElementById("outputArea").value="";resetCharacterLock();renderAllOptionChips()}
document.addEventListener("DOMContentLoaded",()=>{resetCharacterLock();updateClock();setInterval(updateClock,30000);renderAllOptionChips()});
</script>
</body>
</html>
