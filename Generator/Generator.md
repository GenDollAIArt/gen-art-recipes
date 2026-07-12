<!--
  Selfie Prompt Generator
  Version: 5.3.1-gaze-profile-closeup
  Updated: 2026-07-12
  Changelog:
    v5.3.1 - 視線・顔向き・接写質感を追加。表情/ポーズ/動きはAI自動導出のまま、横顔アップ・非カメラ目線・質感寄り接写を軽く指定できるよう改善
    v5.3.0 - テンション/感情/表情の3項目を「雰囲気・気分」に統合。表情・視線・ポーズ・動きはシチュエーションと雰囲気からAIが自動導出する仕様へ変更
    v5.2.2 - シーン文中の「もたれる / 寄りかかる / 前向き / 後ろ向き / 横向き / シンク / 柵 / カウンター / 壁 / ガラス」から、自動でもたれ方と接触点を導くLEAN SUPPORT AUTO-REFLECTIONを追加
    v5.2.1 - 夜景ポートレート用の背景なじみ/露出バランスを追加。背景ボケを中程度に調整し、フラッシュ感を抑えつつ胸シルエット維持ロックを追加。前ボケ効果も追加
    v5.2.0 - 被写体参照を顔IDだけでなく体型/胸/腰幅/ヒップ幅の基準にも使うBODY REFERENCE LOCKを追加。2枚目コーデ画像の体型コピーは禁止
    v5.1.1 - 胸シルエット選択肢の効き方を調整。控えめ=普通サイズ寄り、立体感/ラインくっきり=少し大きめ、立体感＋ライン=最も強く自然に反映
-->
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Stable Character Prompt Generator</title>
<style>
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
  .chip.disabled {
    opacity: 0.35;
    cursor: not-allowed;
    filter: grayscale(0.6);
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

  .chip.has-help::after {
    content: "？";
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 15px;
    height: 15px;
    margin-left: 5px;
    border-radius: 999px;
    font-size: 10px;
    color: #c4b5fd;
    background: rgba(168,85,247,0.18);
    border: 1px solid rgba(196,181,253,0.35);
  }

  .help-overlay {
    position: fixed; inset: 0; z-index: 50;
    background: rgba(0,0,0,0.55);
    display: flex; align-items: flex-end; justify-content: center;
    padding: 14px;
  }
  .help-overlay.hidden { display: none; }
  .help-sheet {
    width: 100%; max-width: 520px;
    background: var(--bg-card);
    border: 1px solid var(--border-pu);
    border-radius: 16px;
    padding: 16px;
    box-shadow: 0 -10px 40px rgba(0,0,0,0.35);
  }
  .help-title {
    font-size: 15px; font-weight: 700; color: var(--text);
    margin-bottom: 8px;
  }
  .help-body {
    font-size: 13px; line-height: 1.75; color: var(--text-sub);
    white-space: pre-line;
  }
  .help-close {
    margin-top: 14px; width: 100%;
    padding: 12px 0; border-radius: 12px;
    border: 1px solid #7c3aed; background: transparent;
    color: #c4b5fd; font-weight: 700; font-size: 14px;
  }
</style>
</head>
<body>

<!-- Header -->
<div class="header">
  <div class="header-icon">✦</div>
  <div>
    <div class="header-title">Stable Character Prompt Generator</div>
    <div class="header-sub">固定キャラ + 今回のシーン v5.3.1</div>
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
    <div class="hint">写真参照ベースでは LIGHT 推奨。顔IDはFace Reference画像を優先し、固定キャラは雰囲気の補助だけにします。FULLは写真なしで固定キャラを作る時向けです。</div>
    <div class="slabel" style="margin-top:10px;">固定キャラモード</div>
    <div class="chips" id="characterModeChips"></div>
    <textarea id="characterLock" rows="8" style="margin-top:10px;"></textarea>
  </div>

  <!-- Outfit reference -->
  <div class="card card-dark">
    <div class="slabel">コーディネート画像参照 — 2枚目の添付画像</div>
    <div class="hint">1枚目は被写体/顔ID、2枚目は服装・配色・シルエット参照として扱います。コーデ画像の顔・髪型・体型・ポーズ・背景はコピーしません。</div>
    <div class="chips" id="outfitReferenceModeChips"></div>
  </div>

  <!-- ① Scene only -->
  <div class="card">
    <div class="slabel">① 今回のシーンだけ（日本語で入力）</div>
    <div class="hint">ここだけ毎回変更：場所・服装・何をしているか。表情・ポーズ・動きはシーンからAIが自然に導きます</div>
    <textarea id="situation" rows="4" placeholder="例：&#10;薄い紺色のワイシャツ、紺色のビジネスパンツ。西中島南方のラーメン店でラーメンをすすっている。&#10;キッチンのシンク前。後ろ向きでもたれる。&#10;ベランダの柵に前向きでもたれる。"></textarea>
  </div>

  <!-- Garment backlight response -->
  <div class="card">
    <div class="slabel">② 逆光時の布の見え方</div>
    <div class="hint">服の素材分類ではなく、逆光で布が光を通す・ふんわり見えるかだけを選びます。ニット/リブ編み/サイズ感は①シーン本文に書く運用です。</div>
    <div class="chips" id="garmentLightChips"></div>
  </div>

  <!-- Chest silhouette -->
  <div class="card">
    <div class="slabel">③ 胸シルエット</div>
    <div class="hint">選択した内容をそのままプロンプトに反映します。控えめ＝普通サイズ寄り、立体感/ラインくっきり＝少し大きめ、立体感＋ライン＝最も強めに自然反映します。</div>
    <div class="chips" id="bustChips"></div>
  </div>

  <!-- Hip silhouette -->
  <div class="card">
    <div class="slabel">④ ヒップ / 下半身シルエット</div>
    <div class="hint">細身Iラインを維持したまま、ヒップの丸み・上向き感を調整します。</div>
    <div class="chips" id="hipChips"></div>
  </div>

  <!-- Weather -->
  <div class="card">
    <div class="slabel">⑤ 天気を選択</div>
    <div class="chips" id="weatherChips"></div>
  </div>

  <!-- ④ Film tone -->
  <div class="card">
    <div class="slabel">⑥ フィルムトーン / 質感</div>
    <div class="hint">色味・質感・雰囲気を選びます。相反するものは自動で選べません</div>
    <div class="chips" id="filmChips"></div>
  </div>

  <!-- ③ Overall tone -->
  <div class="card">
    <div class="slabel">⑦ 作品トーン</div>
    <div class="hint">写真全体の印象を選びます。反対方向の組み合わせは自動整理</div>
    <div class="chips" id="toneChips"></div>
  </div>

  <!-- ④ Bokeh & Effects -->
  <div class="card">
    <div class="slabel">⑧ エフェクト（複数選択可） ⓘ</div>
    <div class="hint">長押しでヘルプ。相反するエフェクトは同時選択できません。まずは3〜5個くらいがおすすめです</div>
    <div class="chips" id="effectChips"></div>
  </div>

  <!-- Effect strength -->
  <div class="card">
    <div class="slabel">⑨ エフェクト強度</div>
    <div class="hint">選択したエフェクト内のweight数値を一括で倍率補正します。控えめは弱め、標準は基準値、強め・盛り盛りは各エフェクトの効きを直接強くします。</div>
    <div class="chips" id="effectStrengthChips"></div>
  </div>

  <!-- Skin finish -->
  <div class="card">
    <div class="slabel">⑩ 肌の見え方 / 肌質感</div>
    <div class="hint">肌の仕上がりを選びます。自然は標準、しっとりは保湿感、ツヤありはハイライトが少し乗りやすくなります。</div>
    <div class="chips" id="skinFinishChips"></div>
  </div>

  <!-- Closeup texture -->
  <div class="card">
    <div class="slabel">⑪ 接写質感</div>
    <div class="hint">顔アップや横顔アップで効きやすい近接描写の質感です。まつ毛・唇・肌のきめなどの描写密度を調整します。</div>
    <div class="chips" id="closeupTextureChips"></div>
  </div>

  <!-- Selfie mode -->
  <div class="card">
    <div class="slabel">⑫ 自撮り / 第三者撮影</div>
    <div class="hint">自撮りONならスマホ手持ちカメラ視点。OFFなら他人が撮った自然なポートレート/スナップ扱い。自動は「他撮り・非自撮り」などがシーンにあればOFF、それ以外はON寄りです。</div>
    <div class="chips" id="selfieModeChips"></div>
  </div>

  <!-- Camera angle -->
  <div class="card">
    <div class="slabel">⑬ カメラ位置 / アングル</div>
    <div class="hint">撮影の高さ・持ち方・向きを選びます。</div>
    <div class="chips" id="angleModeChips"></div>
  </div>

  <!-- Gaze -->
  <div class="card">
    <div class="slabel">⑭ 視線</div>
    <div class="hint">カメラ目線にするか、少し外すか、遠くを見るかを軽く指定できます。未指定ならシーンと雰囲気からAIが導きます。</div>
    <div class="chips" id="gazeChips"></div>
  </div>

  <!-- Face direction -->
  <div class="card">
    <div class="slabel">⑮ 顔向き</div>
    <div class="hint">正面・斜め・横顔・振り向きなどの顔の向きだけを指定します。カメラ位置そのものは⑬で決めます。</div>
    <div class="chips" id="faceDirectionChips"></div>
  </div>

  <!-- Subject framing / composition -->
  <div class="card">
    <div class="slabel">⑯ 構図 / 被写体サイズ</div>
    <div class="hint">顔中心か、上半身か、服や体も含めて広めに見せるかを選びます。横顔アップや超接写もここで選べます。</div>
    <div class="chips" id="subjectSizeChips"></div>
  </div>

  <!-- Background view -->
  <div class="card">
    <div class="slabel">⑰ 背景の見せ方</div>
    <div class="hint">背景の見せ方を決めます。夜景ポートレートでは背景を主張させすぎず、被写体となじませます。</div>
    <div class="chips" id="backgroundViewChips"></div>
  </div>

  <!-- Framing space -->
  <div class="card">
    <div class="slabel">⑱ 余白 / リーディングスペース</div>
    <div class="hint">被写体を画像いっぱいにするか、少し余白を残すか、場所を見せるかを選択します。ソファに寝転がる・椅子に座る等では「余白なし / 被写体いっぱい」が使いやすいです</div>
    <div class="chips" id="framingChips"></div>
  </div>

  <!-- Photo naturalness / staging -->
  <div class="card">
    <div class="slabel">⑲ 写真の自然さ / 演出度</div>
    <div class="hint">日常セルフィー寄りか、少し盛るか、モデル風か、ファッション誌風かを選びます</div>
    <div class="chips" id="photoStyleChips"></div>
  </div>

  <!-- Mood / expression auto-derivation -->
  <div class="card">
    <div class="slabel">⑳ 雰囲気・気分</div>
    <div class="hint">表情・ポーズ・動きは、①シチュエーションとここで選んだ雰囲気からAIが自然に自動導出します。視線と顔向きは必要な時だけ⑭⑮で軽く指定できます。</div>
    <div class="chips" id="moodChips"></div>
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
    <div class="hint" id="copyStatus" style="margin-top:8px;">生成後に自動コピーします。失敗した場合は「コピー」ボタンを押してください。</div>
  </div>

</div>

<div class="help-overlay hidden" id="chipHelpOverlay" onclick="hideChipHelp()">
  <div class="help-sheet" onclick="event.stopPropagation()">
    <div class="help-title" id="chipHelpTitle">ヘルプ</div>
    <div class="help-body" id="chipHelpBody"></div>
    <button class="help-close" onclick="hideChipHelp()">閉じる</button>
  </div>
</div>
<script>const HAIR_BY_MONTH = {
  1:"(long straight, dark brown hair:1.65), (hair falls below the shoulders:1.55)",
  2:"(long wave, dark brown to chestnut brown gradient hair:1.65), (hair falls below the shoulders:1.55)",
  3:"(long soft wave, chestnut brown hair:1.65), (hair falls below the shoulders:1.55)",
  4:"(medium straight, chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",
  5:"(medium wave, light chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",
  6:"(soft bob, ash brown hair:1.78), (jaw-to-neck length bob:1.88), (not long hair:1.95)",
  7:"(airy bob, ash brown hair:1.8), (short-to-medium airy bob length around jaw to neck:1.9), (not long hair:1.98)",
  8:"(short bob, light ash brown hair:1.8), (clear short bob length above or around jaw:1.9), (not long hair:1.98)",
  9:"(medium bob, ash brown to dark brown hair:1.75), (shoulder-grazing medium bob length:1.82), (not chest-length hair:1.95)",
  10:"(inner-color straight, dark brown with caramel inner highlight:1.65), (long hair below shoulders:1.55)",
  11:"(inner-color wave, dark brown with rose-beige inner highlight:1.65), (long hair below shoulders:1.55)",
  12:"(long straight, dark brown with subtle inner highlight:1.65), (long hair below shoulders:1.55)",
};

const DAY_MOOD = {
  Sun:"Quiet reflective Sunday mood, gentle weekend loneliness",
  Mon:"Tired but composed Monday mood",
  Tue:"Focused stable neutral Tuesday calm",
  Wed:"Midweek fatigue, quiet weariness",
  Thu:"Slight pre-weekend anticipation",
  Fri:"Friday pre-weekend energy, lively but time-neutral mood",
  Sat:"Relaxed confident Saturday energy",
};

const APP_VERSION = "v5.3.1-gaze-profile-closeup";
const CHARACTER_MODE_OPTIONS = [
  {label:"📷 OFF / 写真参照のみ", key:"off", value:"off"},
  {label:"✨ LIGHT / 写真参照＋雰囲気", key:"light", value:"light"},
  {label:"🔒 FULL / 従来の固定キャラ", key:"full", value:"full"},
];

const OUTFIT_REFERENCE_MODE_OPTIONS = [
  {label:"🚫 OFF / 使わない", key:"off", value:"off"},
  {label:"✨ LIGHT / 色・雰囲気", key:"light", value:"light"},
  {label:"👗 FULL / 服装を強めに参照", key:"full", value:"full"},
];

const LIGHT_CHARACTER_LOCK = `(refined Korean Asian fashion-model beauty atmosphere:1.5),
(mature adult woman, never younger-looking:1.8),
(very fair translucent skin with natural texture:1.6),
(slim elongated face impression:1.45),
(narrow jawline and delicate chin impression:1.45),
(realistic balanced adult proportions:1.6),
(face identity and detailed facial features are taken from the Face Reference image:1.95),
(no different person:1.95),
(no celebrity likeness:1.95)`;

const CHIN_CONTROL = "(neutral chin position:1.95), (chin not thrust forward:1.95), (no jutting chin:1.95), (no projected jaw:1.95), (no raised chin:1.9), (face kept level or only very slightly tilted:1.9), (neck relaxed and not stretched:1.85), (mouth and jaw relaxed naturally:1.85), (natural jaw posture:1.85)";

const ANGLES = [
  {name:"SUPER HIGH ANGLE", prompt:"(true overhead super high-angle selfie:1.9), (arm fully extended above head:1.9), (smartphone high over her head looking almost straight down:1.9), (bird's-eye framing of face, shoulders, outfit and surroundings:1.8), (subject keeps a natural face angle without looking up excessively:1.9), (eyes gently meet the lens without forcing an upward gaze:1.8), (do not copy any reference-image chin lift or arm-extension pose:1.9), (not eye-level:1.9), (not low-angle:1.9), " + CHIN_CONTROL},
  {name:"GOLDEN ANGLE",     prompt:"(camera slightly above eye level looking down:1.9), (head-to-chest framing:1.8), (three-quarter facial view:1.8), (face 30-45 degrees from camera:1.8), (eyes naturally meet the lens:1.8), (flattering high selfie angle without exaggerated upward face tilt:1.9), (do not copy reference-image chin posture:1.9), " + CHIN_CONTROL},
  {name:"HIGH ANGLE",       prompt:"(camera clearly above eye level:1.8), (head-to-chest framing:1.8), (natural relaxed face angle:1.8), (eyes looking naturally toward the lens without lifting the chin:1.9), (do not copy reference-image upward face tilt:1.9), " + CHIN_CONTROL},
  {name:"EYE LEVEL",        prompt:"(camera at eye height:1.9), (head-to-chest framing:1.8), (face angled 10-30 degrees:1.7), (relaxed everyday selfie:1.8), (minimal distortion:1.7), (do not copy reference-image arm extension or chin posture:1.9), " + CHIN_CONTROL},
  {name:"SIDE PROFILE",     prompt:"(camera positioned from the true side of the face:1.9), (clear side-view or near-profile portrait angle:1.9), (lateral face plane emphasized:1.85), (camera remains around eye height from the side:1.88), (profile or near-profile eye line:1.82), (not overhead, not dramatic low-angle:1.85), (do not copy reference-image front-facing composition:1.9), " + CHIN_CONTROL},
  {name:"RECLINING SIDE EYE LEVEL", prompt:"(subject is lying down or reclining on her side:1.92), (camera placed beside her at face height:1.92), (side-on eye-level view from a reclining posture:1.9), (close lateral viewpoint while lying down:1.88), (intimate face-level side composition:1.85), (eyes meet the lens naturally from a sideways resting pose:1.82), (not overhead, not strong low-angle:1.88), (do not copy reference-image standing selfie composition:1.9), " + CHIN_CONTROL},
  {name:"LOW ANGLE",        prompt:"(ordinary low-angle selfie from in front of the body:1.8), (phone held slightly below chest level:1.8), (camera below the face and angled only mildly upward from the front:1.8), (viewer sees the subject from a lower front hand position:1.7), (face looking naturally toward the lens without pushing the chin forward:1.8), (not overhead:1.9), (not golden angle:1.8), (not waist-side vertical upshot:1.9), (not near-vertical upward camera axis:1.9), " + CHIN_CONTROL},
  {name:"HIDDEN WAIST-HELD SELFIE", prompt:"(true hidden waist-held selfie:2.0), (smartphone held discreetly against her waist or lower torso:2.0), (elbow bent tightly and close to the body:2.0), (short folded arm, not extended toward the camera:2.0), (phone hidden near the body as if taking a quick discreet selfie:1.98), (camera viewpoint originates from very close to her lower torso or waist:2.0), (lens angled only slightly upward, not vertical:1.98), (close-body low handheld perspective:1.95), (torso feels close to the lens without extreme distortion:1.85), (natural low-angle selfie with subtle upward perspective only:1.85), (no arm's-length selfie pose:2.0), (no long stretched arm selfie:2.0), (no visible extended forearm reaching toward the camera:2.0), (no large foreground arm:2.0), (no selfie stick arm perspective:2.0), (not a normal raised-hand selfie:2.0), (not a dramatic low-angle upshot:1.98), (not a vertical upshot:1.98), (not camera pointing straight upward:1.98), (not near-vertical upward camera axis:1.98), (not phone extended far away:2.0), (do not copy the Face Reference image's camera angle, arm extension, chin posture, or composition:1.95), " + CHIN_CONTROL},
  {name:"WAIST-SIDE VERTICAL UPSHOT", prompt:"(legacy waist-side vertical upshot mode, not recommended for natural waist-held selfies:1.4), (strong vertical upshot only if explicitly required:1.4), (prefer HIDDEN WAIST-HELD SELFIE for natural discreet waist-level selfies:1.9), " + CHIN_CONTROL},
  {name:"SUPER LOW ANGLE",  prompt:"(dramatic super low-angle selfie:1.9), (phone held very low below the waist or near hip-to-thigh level:1.9), (strong upward perspective from far below the face:1.9), (camera looks up sharply with noticeable perspective distortion:1.8), (torso and jacket line strongly emphasized by low perspective:1.8), (face looking naturally toward the lens without jutting the chin:1.8), (not overhead:1.9), (not golden angle:1.9), (not high-angle selfie:1.9), (not waist-side vertical upshot:1.8), " + CHIN_CONTROL},
  {name:"DYNAMIC TILTED",   prompt:"(camera slightly rotated:1.8), (diagonal composition:1.8), (face tilted with camera in a natural way:1.7), (snapshot atmosphere:1.8), (do not copy reference-image chin posture:1.9), " + CHIN_CONTROL},
  {name:"OVER SHOULDER",    prompt:"(face partially turned away:1.7), (looking back toward lens:1.8), (shoulder line emphasized:1.7), (candid feel:1.7), (do not copy reference-image selfie arm extension:1.9), " + CHIN_CONTROL},
  {name:"BACK VIEW",        prompt:"(non-selfie back-view portrait:1.95), (camera behind the subject looking at her back and shoulders:1.95), (face mostly not visible or only a slight side hint:1.85), (back of outfit and hair silhouette are visible:1.88), (quiet rear-view fashion composition:1.9), (external photographer viewpoint, not selfie:1.95), (no front chest emphasis:1.95), (no selfie arm:1.95), " + CHIN_CONTROL},
  {name:"DIAGONAL BACK VIEW", prompt:"(non-selfie diagonal back-view portrait:1.95), (camera behind and slightly to the side of the subject:1.95), (three-quarter rear angle with shoulder line and side profile hint:1.9), (face only partially visible if she turns slightly:1.78), (backlit outer clothing edge can be visible without body detail:1.86), (external photographer viewpoint, not selfie:1.95), (no front chest emphasis:1.95), " + CHIN_CONTROL},
  {name:"BACK OVER SHOULDER", prompt:"(non-selfie over-the-shoulder view from behind:1.92), (camera behind her shoulder as she slightly looks away or glances back:1.88), (back shoulder line and hair are foregrounded:1.86), (rear-to-side fashion portrait composition:1.9), (external camera viewpoint, not selfie:1.95), (no arm-length selfie perspective:1.95), (no front chest emphasis:1.95), " + CHIN_CONTROL},
  {name:"WINDOW BACK VIEW", prompt:"(non-selfie rear-view portrait by a window:1.95), (subject seen from behind while looking outside:1.95), (window light outlines hair, shoulders, and outer clothing edges:1.88), (room behind her is dim and quiet:1.82), (external photographer viewpoint, not selfie:1.95), (opaque clothing stays non-revealing in backlight:1.95), (no see-through body detail:1.95), " + CHIN_CONTROL},
  {name:"WALKING",          prompt:"(captured mid-walk:1.8), (subtle body motion:1.7), (hair movement from motion:1.7), (face turned slightly to camera:1.7), (do not copy reference-image chin posture or composition:1.9), " + CHIN_CONTROL},
];

const ANGLE_UI_OPTIONS = [
  {label:"🎲 おまかせ", key:"auto", value:"auto"},

  {label:"👁️ 目線", key:"EYE LEVEL", value:"EYE LEVEL"},
  {label:"➡️ 真横から", key:"SIDE PROFILE", value:"SIDE PROFILE"},
  {label:"✨ 盛れ角", key:"GOLDEN ANGLE", value:"GOLDEN ANGLE"},
  {label:"⬆️ 少し上から", key:"HIGH ANGLE", value:"HIGH ANGLE"},
  {label:"🙆 頭上から", key:"SUPER HIGH ANGLE", value:"SUPER HIGH ANGLE"},

  {label:"🤫 腰だめ", key:"HIDDEN WAIST-HELD SELFIE", value:"HIDDEN WAIST-HELD SELFIE"},
  {label:"⬇️ 低め前持ち", key:"LOW ANGLE", value:"LOW ANGLE"},
  {label:"📉 強い煽り", key:"SUPER LOW ANGLE", value:"SUPER LOW ANGLE"},

  {label:"⬅️ 背中から", key:"BACK VIEW", value:"BACK VIEW"},
  {label:"↖️ 斜め後ろ", key:"DIAGONAL BACK VIEW", value:"DIAGONAL BACK VIEW"},
  {label:"🧥 肩越し後ろ", key:"BACK OVER SHOULDER", value:"BACK OVER SHOULDER"},
  {label:"🪟 窓際後ろ姿", key:"WINDOW BACK VIEW", value:"WINDOW BACK VIEW"},

  {label:"🛏️ 寝転び横", key:"RECLINING SIDE EYE LEVEL", value:"RECLINING SIDE EYE LEVEL"},
  {label:"🚶 歩き", key:"WALKING", value:"WALKING"},
  {label:"🌀 斜め", key:"DYNAMIC TILTED", value:"DYNAMIC TILTED"},
  {label:"↩️ 振り向き", key:"OVER SHOULDER", value:"OVER SHOULDER"},
];

const ANGLE_META = {
  "BACK VIEW": { requiresSelfieOff:true, rear:true, safeBacklight:true },
  "DIAGONAL BACK VIEW": { requiresSelfieOff:true, rear:true, side:true, safeBacklight:true },
  "BACK OVER SHOULDER": { requiresSelfieOff:true, rear:true, side:true, safeBacklight:true },
  "WINDOW BACK VIEW": { requiresSelfieOff:true, rear:true, safeBacklight:true },
  "SIDE PROFILE": { side:true, safeBacklight:true },
  "RECLINING SIDE EYE LEVEL": { side:true, reclining:true, safeBacklight:true }
};

const FACE_CLOSEUP_SUBJECT_KEYS = ["headClose", "faceCloseup", "profileCloseup", "extremeFace"];

function getAngleMeta(angleName = "") {
  return ANGLE_META[angleName] || {};
}

function angleRequiresSelfieOff(angleName = "") {
  return !!getAngleMeta(angleName).requiresSelfieOff;
}

function isRearOrSideAngle(angleName = "") {
  const meta = getAngleMeta(angleName);
  return !!(meta.rear || meta.side || meta.reclining);
}

function isBacklightSafeAngle(angleName = "", selfieMode = "") {
  const meta = getAngleMeta(angleName);
  return selfieMode === "off" && !!meta.safeBacklight;
}

function isFaceCloseupSubjectKey(subjectSizeKey = "") {
  return FACE_CLOSEUP_SUBJECT_KEYS.includes(subjectSizeKey);
}

const BODY_LINE_BASE_PROMPT = [
  "(body type is anchored to the first reference image when the body is visible:1.94)",
  "(stable same slender I-line body base:1.92)",
  "(narrow elegant torso line and delicate adult frame:1.9)",
  "(bust volume, torso width, waist position, and hip width stay consistent with the locked subject bodyline:1.92)",
  "(straight compact waist-to-hip line, not laterally wide:1.92)",
  "(hips stay compact and do not spread sideways:1.94)",
  "(long slim arms and legs with realistic adult proportions:1.88)",
  "(face identity and body type remain consistent across scenes:1.95)"
].join(", ");

const SELFIE_MODE_OPTIONS = [
  {label:"🎲 自動 / おまかせ", key:"auto", value:"auto"},
  {label:"🤳 自撮り ON", key:"selfie_on", value:"on"},
  {label:"📷 自撮り OFF / 第三者撮影", key:"selfie_off", value:"off"},
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
  "warm relaxed night expression, not intoxicated",
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
  {label:"曇り ☁️",  value:"overcast cloudy sky, cloud-filtered diffused daylight, muted atmosphere, no direct sunlight, no sparkling sun highlights"},
  {label:"小雨 🌦️", value:"light drizzle rain, wet streets, soft grey ambient light, misty air"},
  {label:"雨 🌧️",   value:"steady rain, rain-soaked streets, dark moody wet atmosphere"},
  {label:"大雨 ⛈️", value:"heavy rain, dramatic downpour, dark stormy atmosphere"},
  {label:"雪 ❄️",   value:"snow falling, winter white scenery, cold crisp air, soft white light"},
  {label:"霧 🌫️",  value:"foggy misty atmosphere, dreamlike hazy soft light"},
];

const FILM_TONES = [
  {label:"なし", value:""},
  {label:"コダック ゴールド 200", value:"Kodak Gold 200 film tone, clearly visible warm golden cast, noticeable analog warmth, lightly visible grain, unmistakable vintage print feel"},
  {label:"フジ プロ 400H", value:"Fuji Pro 400H film tone, clearly visible pastel palette, soft mint-cool shadows, airy film color separation, unmistakable film softness"},
  {label:"コダック ポートラ 800", value:"Kodak Portra 800 film tone, clearly visible rich warm skin, creamy highlight rolloff, noticeable film grain, unmistakable premium portrait film look"},
  {label:"イルフォード HP5", value:"Ilford HP5 black and white film, clearly visible monochrome rendering, strong classic contrast, obvious grain texture, unmistakable black-and-white film look"},
  {label:"シネスコープ", value:"CinemaScope film tone, clearly visible teal and orange grade, cinematic color separation, anamorphic blockbuster look, unmistakable movie-like grading"},
  {label:"ローモ", value:"Lomography vivid tone, clearly visible cross-processed colors, strong saturation shift, lo-fi contrast, vignette edges, unmistakable lomo look"},
  {label:"ポラロイド", value:"Polaroid instant film tone, clearly visible faded instant-film colors, nostalgic warm cast, soft bloom, unmistakable instant snapshot feel"},
  {label:"ヴィンテージ 90s", value:"1990s vintage film tone, clearly visible retro color shift, muted warm mid-tones, nostalgic softness, unmistakable 90s film-photo mood"},
  {label:"ガサつき", value:"gritty rough film tone, clearly visible coarse texture and dry roughness, pronounced gritty surface feel, raw unpolished analog mood, unmistakably harsh tactile photo texture"}
];

const OVERALL_TONES = [
  {label:"なし", value:""},
  {label:"クール / モダン", value:"clearly visible cool modern aesthetic, crisp clean image design, urban sophisticated mood, unmistakably sleek and contemporary"},
  {label:"キュート / 柔らか", value:"clearly visible cute soft aesthetic, gentle pastel atmosphere, soft warm friendliness, unmistakably sweet and tender"},
  {label:"ダーク / ムーディ", value:"clearly visible dark moody aesthetic, deeper shadows, brooding emotional atmosphere, unmistakably heavy and cinematic"},
  {label:"ナチュラル / 透明感", value:"clearly visible natural transparent beauty aesthetic, fresh clean look, airy brightness, unmistakably translucent and refined"},
  {label:"エレガント / 上品", value:"clearly visible elegant refined aesthetic, graceful composition, polished sophistication, unmistakably classy and upscale"},
  {label:"ストリート / エッジ", value:"clearly visible street edge aesthetic, raw urban energy, gritty authentic mood, unmistakably rough and street-styled"},
  {label:"ロマンティック", value:"clearly visible romantic dreamy aesthetic, soft warm glow, tender emotional atmosphere, unmistakably dreamy and sentimental"},
  {label:"ミニマル / 静寂", value:"clearly visible minimal quiet aesthetic, negative-space calm, restrained serene atmosphere, unmistakably quiet and still"}
];

const EFFECTS = [
  {label:"🌫️ 背景ボケ", value:"(portrait-safe moderate background blur:1.66), (background is softly blurred but still readable as a real place:1.68), (moderate depth separation without cutout look:1.7)", help:"何が変わる？\n背景をほどよくぼかして被写体を主役にします。場所感は残し、切り抜きっぽい分離を避けます。\n\n向く場面\n夜景ポートレート、街スナップ、カフェ、駅、人物中心の写真。\n\n注意\n強くぼかしすぎると背景から浮くため、ポートレート用に中程度へ調整しています。"},
  {label:"✨ 光の玉ボケ", value:"(clearly visible light orb bokeh:1.8), (ambient light circles in background:1.8), (noticeable specular bokeh highlights:1.8)", help:"何が変わる？\n背景の光が丸い玉ボケとして出やすくなります。\n\n向く場面\n夜景、イルミネーション、駅ホーム、逆光のキラキラ。\n\n注意\n光源が少ない場面では効きが弱めです。"},
  {label:"✨ 前ボケ", value:"(soft out-of-focus foreground bokeh in front of the subject:1.78), (near-lens blurred light orbs crossing the frame lightly:1.74), (layered depth with foreground bokeh, subject, and readable background:1.76)", help:"何が変わる？\n被写体の手前に、レンズ近くの光粒や水滴のような前ボケが入ります。\n\n向く場面\n夜景、イルミ、海辺の水しぶき、ガラス越し、花や光を手前に置いた写真。\n\n注意\n顔を隠しすぎない程度に使うのが自然です。"},
  {label:"💧 水滴/結露感", value:"(clearly visible condensation droplets on glass or skin:1.7), (noticeable water droplet texture:1.7)", help:"何が変わる？\nガラスや前景、空気感に水滴っぽい質感が乗ります。\n\n向く場面\n雨の日、窓辺、ドリンク越し、湿度感を出したい時。\n\n注意\n乾いた晴天シーンでは不自然になりやすいです。"},
  {label:"✨ きらめき粒子", value:"(clearly visible sparkling glitter particles in air:1.7), (noticeable shimmering light particles:1.7)", help:"何が変わる？\n空気中に小さなキラキラ粒子が見えるようになります。\n\n向く場面\n午後の光、かわいい雰囲気、夢っぽい写真。\n\n注意\n曇り・雨・霧では使わない方が自然です。"},
  {label:"🌁 ソフトフォーカス", value:"(clearly visible soft focus haze:1.7), (gentle dreamy blur on edges:1.7), (noticeable diffused hazy atmosphere:1.7)", help:"何が変わる？\n輪郭が少しやわらぎ、ふんわりした写りになります。\n\n向く場面\nやさしいポートレート、窓辺、ロマンティック系。\n\n注意\nシャープさや細かい質感は少し弱くなります。"},
  {label:"🌙 逆光/リムライト", value:"(clearly visible backlighting:1.8), (noticeable rim light on hair and shoulders:1.8), (silhouette-edge glow:1.7)", help:"何が変わる？\n後ろから光が当たり、髪や肩の縁が光って見えます。\n\n向く場面\n窓辺、夕方、駅ホーム、屋外の斜光。\n\n注意\n顔を明るく見せたい時は他の明るめ効果と併用がおすすめです。"},
  {label:"📼 VHSノイズ", value:"(clearly visible VHS scan lines:1.7), (retro analog video noise:1.7), (noticeable chromatic aberration:1.7)", help:"何が変わる？\n走査線・ノイズ・色ズレのあるアナログ映像っぽさが出ます。\n\n向く場面\n90s、ストリート、レトロ、荒め写真。\n\n注意\n透明感・清潔感とは逆方向です。"},
  {label:"🔥 暖色フレア", value:"(clearly visible warm lens flare:1.8), (golden warm flare streaks across frame:1.8)", help:"何が変わる？\nオレンジ〜金色のフレアが入り、温かい光感が出ます。\n\n向く場面\n夕方、夏、屋外、やわらかい逆光。\n\n注意\n寒色系やクールな雰囲気とはぶつかりやすいです。"},
  {label:"❄️ 冷色フィルター", value:"(clearly visible cool blue color grading:1.8), (strong cold tone filter:1.8)", help:"何が変わる？\n全体が青寄り・ひんやりした色味になります。\n\n向く場面\n夜、雨、都会、クール/ムーディ路線。\n\n注意\n暖色フレアとは同時に使わない方がまとまりやすいです。"},
  {label:"🌈 光漏れ", value:"(clearly visible light leak effect:1.8), (film light leak streaks across frame:1.8)", help:"何が変わる？\nフィルムの光漏れみたいな色のにじみや帯が入ります。\n\n向く場面\nレトロ、ロマンティック、思い出写真っぽい演出。\n\n注意\n入れすぎると顔や文字が見づらくなります。"},
  {label:"🖤 ビネット", value:"(clearly visible vignette:1.7), (noticeable dark edge falloff around frame:1.7)", help:"何が変わる？\n画面の四隅が少し暗くなり、中心に視線が集まります。\n\n向く場面\nポートレート、映画っぽい写真、落ち着いた雰囲気。\n\n注意\n明るく軽い写真では強すぎると重く見えます。"},
  {label:"🎞️ フィルムグレイン強め", value:"(clearly visible heavy film grain:1.8), (pronounced analog grain texture:1.8)", help:"何が変わる？\nザラついた粒状感が出て、フィルムっぽい質感になります。\n\n向く場面\nレトロ、日常スナップ、味のある写真。\n\n注意\n肌や細部のなめらかさは少し弱くなります。"},
  {label:"⚡ 直フラッシュ", value:"(direct on-camera flash look:1.9), (front-facing flash illumination with flat bright hit:1.85), (snapshot flash aesthetic:1.8)", help:"何が変わる？\n真正面から当たる直フラッシュっぽい写りになります。\n\n向く場面\n夜スナップ、ストリート、コンデジ/スナップ風、Y2Kっぽい写真。\n\n注意\n自然光っぽさは弱くなり、かなり人工的な光に寄ります。"},
  {label:"⬛ 硬い影", value:"(hard-edged shadows:1.85), (crisp shadow boundaries on face, body, or background:1.8), (stark directional light shadow separation:1.8)", help:"何が変わる？\n輪郭のはっきりした硬い影が出やすくなります。\n\n向く場面\n直フラッシュ、晴天の強い日差し、ストリート、強め演出。\n\n注意\nやわらかい透明感路線とは少し逆方向です。"},
  {label:"🤍 白飛びフラッシュ", value:"(flash overexposure with bright blown highlights:1.9), (slight highlight clipping on skin or clothing from flash:1.85), (high-energy flash snapshot with intentional blown-out bright areas:1.85)", help:"何が変わる？\nフラッシュが強く当たって、一部が白く飛んだような写りになります。\n\n向く場面\n夜スナップ、コンデジ風、派手めのフラッシュ写真。\n\n注意\n白い服や文字は飛びすぎると読みにくくなります。"},
  {label:"☀️ 自然光ハイライト", value:"(clearly visible soft natural daylight:1.7), (noticeable highlight on nose bridge and forehead:1.7)", help:"何が変わる？\n自然光に当たった明るいハイライトが出やすくなります。\n\n向く場面\n昼、窓辺、透明感、ナチュラル系。\n\n注意\n夜や暗い屋内では効きが弱くなります。"},
  {label:"📱 スマホHDR", value:"(clearly visible smartphone HDR rendering:1.8), (smartphone tonal lift and clean dynamic range:1.8)", help:"何が変わる？\n明るい所と暗い所の情報が残りやすく、スマホっぽい整った写りになります。\n\n向く場面\n日中の自撮り、駅前、街中、自然な今っぽさ。\n\n注意\n荒いフィルム感とは少し逆方向です。"},
  {label:"🤍 白肌オーバー露光", value:"(clearly visible slight overexposure on fair skin:1.8), (clean pale skin rendering:1.8)", help:"何が変わる？\n肌が明るく白っぽく、少し飛ばしたような見え方になります。\n\n向く場面\n透明感、やわらかい可愛い雰囲気、明るめ自撮り。\n\n注意\n服の白飛びやディテール消えに注意です。"},
  {label:"🫧 透明感カラー", value:"(clearly visible airy transparent color grading:1.8), (smooth but realistic translucent skin texture:1.7)", help:"何が変わる？\n空気が軽く、明るく澄んだ色味になります。\n\n向く場面\n白シャツ、淡色、昼、清潔感のある写真。\n\n注意\nダーク/ストリート系とは相性が弱めです。"},
  {label:"🌤️ 低コントラスト影", value:"(clearly visible low-contrast facial shadows:1.8), (soft even daylight shadow transition:1.8)", help:"何が変わる？\n影がやわらかくなり、顔の陰影がきつく出にくくなります。\n\n向く場面\n自然光、透明感、やさしい表情を見せたい時。\n\n注意\n立体感の強いドラマチックな写真には向きません。"},
  {label:"🌃 ネオン反射", value:"(clearly visible neon reflections on nearby surfaces:1.75), (urban neon color accents in background or glass:1.75), (night-city reflective light atmosphere:1.7)", help:"何が変わる？\n看板や街灯の色が、ガラス・床・髪の縁などに反射して見えやすくなります。\n\n向く場面\n夜の街、駅前、アメ横、繁華街、バー周辺。\n\n注意\n昼の自然光シーンでは効きが弱いか、不自然になりやすいです。"},
  {label:"🪞 ガラス反射", value:"(subtle glass reflection layer:1.75), (faint reflected city lights or window reflections:1.7), (through-glass photographic texture:1.65)", help:"何が変わる？\n窓やショーケース越しの反射、薄い写り込みが入りやすくなります。\n\n向く場面\nカフェ窓、電車、ビル街、夜の店舗前。\n\n注意\n顔に反射が重なりすぎると表情が読みにくくなるので、強度は標準か控えめが安全です。"},
  {label:"🌇 夕方斜光", value:"(warm low-angle evening side light:1.8), (golden-hour directional highlights across face and clothing:1.75), (long soft urban shadows from sunset light:1.7)", help:"何が変わる？\n夕方の低い太陽が横から差すような、斜めの光と影が出やすくなります。\n\n向く場面\n夕方の街、駅前、屋外、光と影を見せたい写真。\n\n注意\n直フラッシュ系とは主光源がぶつかるので同時選択不可にしています。"},
  {label:"🏃 モーションブラー", value:"(subtle handheld motion blur:1.65), (slight background motion streaks from walking snapshot:1.65), (realistic candid movement blur:1.6)", help:"何が変わる？\n歩きながら撮ったような、少し流れるブレ感が入ります。\n\n向く場面\n街歩き、夜スナップ、混雑した場所、ライブ感を出したい時。\n\n注意\n顔までブレると崩れやすいので、盛り盛りより標準〜強めまでがおすすめです。"},
  {label:"📸 コンデジ感", value:"(compact digital camera snapshot look:1.8), (slightly crunchy digital flash-era texture:1.75), (early-2000s casual digicam rendering:1.7)", help:"何が変わる？\nスマホより少し荒く、コンデジで撮ったようなスナップ感が出ます。\n\n向く場面\n直フラッシュ、夜スナップ、Y2K、居酒屋、街中の記録写真。\n\n注意\n透明感スマホ系とは方向が違うので、同時に選ぶと整理されます。"},
  {label:"🩶 低彩度", value:"(muted desaturated color palette:1.75), (reduced saturation with realistic skin tone preserved:1.7), (subdued color mood without monochrome:1.65)", help:"何が変わる？\n色の派手さを少し抑えて、落ち着いた写真になります。\n\n向く場面\nクール、ムーディ、ストリート、ガサつき、90s系。\n\n注意\nキュートで明るい写真や透明感カラーとは方向が少し違います。"},
  {label:"📐 自撮り広角感", value:"(clearly visible natural selfie wide-angle perspective:1.8), (noticeable perspective stretch from smartphone front camera:1.7)", help:"何が変わる？\nスマホ自撮り特有の少し広角っぽいパース感が出ます。\n\n向く場面\n日常自撮り、手前の腕や距離感を自然に出したい時。\n\n注意\n顔を整えたい時は効かせすぎない方が無難です。"}
];

const EFFECT_STRENGTH_OPTIONS = [
  {label:"🫧 控えめ", key:"subtle", value:"subtle", multiplier:0.90, note:"選択エフェクトのweightを0.90倍にします"},
  {label:"✨ 標準", key:"standard", value:"standard", multiplier:1.00, note:"選択エフェクトのweightを基準値のまま使います"},
  {label:"🌟 強め", key:"strong", value:"strong", multiplier:1.12, note:"選択エフェクトのweightを1.12倍にします"},
  {label:"💥 盛り盛り", key:"max", value:"max", multiplier:1.25, note:"選択エフェクトのweightを1.25倍にします"}
];

function clampWeight(value, min = 0.1, max = 3.0) {
  return Math.min(Math.max(value, min), max);
}

function roundPromptWeight(value) {
  return Math.round(value * 100) / 100;
}

function scaleWeightedPrompt(prompt, multiplier) {
  if (!prompt || typeof prompt !== "string") return "";
  const scale = Number.isFinite(multiplier) ? multiplier : 1.0;
  return prompt.replace(/\(([^()]+?):([0-9]*\.?[0-9]+)\)/g, function(match, body, weight) {
    const parsed = parseFloat(weight);
    if (!Number.isFinite(parsed)) return match;
    const scaled = roundPromptWeight(clampWeight(parsed * scale));
    return "(" + body + ":" + scaled + ")";
  });
}

function scaleSelectedEffectPrompts(effectsArr, effectStrengthMode) {
  if (!Array.isArray(effectsArr) || effectsArr.length === 0) return [];
  const multiplier = effectStrengthMode && Number.isFinite(effectStrengthMode.multiplier)
    ? effectStrengthMode.multiplier
    : 1.0;
  return effectsArr.map(fx => scaleWeightedPrompt(fx, multiplier));
}

const SUBJECT_SIZE_MODES = [
  {label:"⚖️ バランス（おすすめ）", key:"balanced", value:"(balanced selfie composition with attractive face, upper body, and believable everyday context:1.8), (face and environment both matter:1.8), (natural handheld framing with believable body scale:1.8)"},
  {label:"✨ 顔優先 / 盛れ重視", key:"face", value:"(face-priority selfie composition:1.8), (clean flattering framing centered on face and upper body:1.8), (beauty-focused composition with less environment emphasis:1.7), (visually refined selfie balance:1.7)"},
  {label:"🙂 顔アップ", key:"headClose", value:"(head-dominant face close-up composition:1.9), (forehead-to-chin or forehead-to-neck framing:1.88), (little shoulder or neckline visible:1.75), (background is minimal and softly secondary:1.6), (eyes, lips, and skin are easy to read:1.85)"},
  {label:"🔍 顔ズームアップ", key:"faceCloseup", value:"(close-up face selfie composition:1.9), (face fills most of the frame:1.9), (forehead-to-collarbone or face-to-neck framing:1.8), (background exists but is secondary and softly readable:1.5), (eyes and skin texture are the main focus:1.8)"},
  {label:"↔️ 横顔アップ", key:"profileCloseup", value:"(profile close-up composition:1.92), (side face or near-profile fills most of the frame:1.9), (eye, nose bridge, lips, and cheek line are clearly readable:1.9), (background stays soft and secondary:1.7), (close-up side-view portrait with elegant profile emphasis:1.84)"},
  {label:"🧿 超接写 / 顔どアップ", key:"extremeFace", value:"(extreme close-up portrait composition:1.95), (the face fills almost the entire frame:1.95), (partial crop on hair, cheek, forehead, or chin is allowed:1.88), (eyes, nose, lips, and skin texture dominate the image:1.9), (background is barely visible and heavily de-emphasized:1.65), (intimate close-up like the attached sample style:1.82)"},
  {label:"🧥 上半身メイン", key:"upperBody", value:"(upper-body selfie composition:1.8), (head-to-waist or head-to-upper-hip framing:1.8), (face, shirt, jacket line, and upper silhouette are clearly readable:1.8), (balanced emphasis on face and outfit:1.8)"},
  {label:"🧍 服や体も広めに", key:"widerBody", value:"(wider body framing selfie composition:1.8), (more of the outfit and body line are included:1.8), (subject appears slightly smaller within the frame than a face-first selfie:1.7), (body silhouette and location readability both matter:1.7)"},
];

const BACKGROUND_VIEW_MODES = [
  {label:"🚫 指定なし", key:"none", value:""},
  {label:"🫧 控えめ", key:"subtle", value:"(background remains secondary and understated:1.7), (subject stays visually dominant over the background:1.8), (background details are present but restrained:1.7)"},
  {label:"🌆 バランス", key:"balanced", value:"(background is shown in a balanced natural way:1.75), (location readability is clear without overemphasizing top or bottom:1.75), (subject and place are both easy to read:1.75)"},
  {label:"🌸 足元", key:"lower", value:"(lower background is clearly visible:1.8), (show the ground, pavement, flowers, water, or details near her feet:1.8), (background emphasis is directed downward below the subject:1.75)"},
  {label:"☕ 奥", key:"depth", value:"(horizontal background behind her is clearly visible:1.8), (show the café, street, station, storefront, or scenery behind the subject:1.8), (background emphasis is directed into the depth behind her:1.75)"},
  {label:"🌙 上", key:"upper", value:"(upper background is clearly visible:1.8), (show the sky, ceiling, signs, tree canopy, or upper part of buildings:1.8), (background emphasis is directed upward above the subject:1.75)"},
];

const FRAMING_MODES = [
  {label:"⚖️ 標準", key:"standard", value:"(balanced subject scale with moderate breathing room:1.7), (natural crop with some surrounding space:1.7), (subject feels comfortably framed, not too tight, not too distant:1.7)"},
  {label:"🧍 余白少なめ", key:"tight", value:"(tight framing with reduced empty space:1.8), (subject occupies most of the frame:1.8), (crop is closer and more intentional:1.8)"},
  {label:"🖼️ 余白なし / 被写体いっぱい", key:"full", value:"(little to no leading space:1.9), (subject fills the image as much as possible:1.9), (tight crop around the body and face with minimal empty background:1.9), (avoid large empty areas such as sofa, wall, ceiling, or floor unless essential:1.9)"},
  {label:"🏙️ 余白あり / 場所も見せる", key:"wide", value:"(clear breathing room around the subject:1.8), (environment is intentionally readable:1.8), (leave more surrounding space to show the location and atmosphere:1.8)"}
];

const PHOTO_STYLE_MODES = [
  {label:"📷 リアルな日常自撮り", key:"daily", value:"(real everyday selfie feel:1.9), (candid daily-life realism:1.8), (slight imperfection is allowed:1.7), (not over-directed, not magazine-like:1.8)"},
  {label:"🙂 少し盛れた自然自撮り", key:"enhanced", value:"(naturally flattering selfie look:1.8), (slightly polished but still believable:1.8), (clean attractive selfie presentation:1.8), (natural but intentionally pretty:1.8)"},
  {label:"🧍 モデルっぽい", key:"model", value:"(model-like posing and facial control:1.8), (deliberate shoulder line and body angle:1.8), (professional self-presentation from the subject:1.8), (the person looks like she knows how to pose:1.8)"},
  {label:"🖤 ファッション誌っぽい", key:"editorial", value:"(fashion editorial photography feel:1.9), (magazine-style composition and styling:1.8), (editorial image design beyond simple selfie realism:1.8), (the whole photo feels like a fashion magazine page:1.8)"},
  {label:"🎬 作り込み強め", key:"strong", value:"(strongly directed visual presentation:1.8), (stylized image design:1.8), (noticeably composed and produced look:1.8), (less accidental, more intentionally crafted:1.8)"},
];

function valueByLabel(items, labelPart) {
  if (!Array.isArray(items)) return "";
  const found = items.find(item => item.label.includes(labelPart));
  return found ? found.value : "";
}

function currentEffectValue(labelPart) {
  return valueByLabel(EFFECTS, labelPart);
}

function currentWeatherValue(labelPart) {
  return valueByLabel(WEATHER_OPTIONS, labelPart);
}

function sparkleEffectValue() {
  return currentEffectValue("きらめき粒子");
}

function isOvercastLikeWeatherActive() {
  const overcastWeatherValues = [
    currentWeatherValue("曇り"),
    currentWeatherValue("小雨"),
    currentWeatherValue("雨"),
    currentWeatherValue("大雨"),
    currentWeatherValue("霧"),
  ].filter(Boolean);
  return overcastWeatherValues.includes(state.weather);
}

function transparentEffectValues() {
  return [
    currentEffectValue("自然光ハイライト"),
    currentEffectValue("スマホHDR"),
    currentEffectValue("白肌オーバー露光"),
    currentEffectValue("透明感カラー"),
    currentEffectValue("低コントラスト影"),
    currentEffectValue("自撮り広角感"),
  ].filter(Boolean);
}

function strongTransparentEffectValues() {
  return [
    currentEffectValue("白肌オーバー露光"),
    currentEffectValue("透明感カラー"),
    currentEffectValue("低コントラスト影"),
    currentEffectValue("スマホHDR"),
  ].filter(Boolean);
}

function grainNoiseEffectValues() {
  return [
    currentEffectValue("VHSノイズ"),
    currentEffectValue("フィルムグレイン強め"),
    currentEffectValue("直フラッシュ"),
    currentEffectValue("硬い影"),
    currentEffectValue("白飛びフラッシュ"),
    currentEffectValue("コンデジ感"),
    currentEffectValue("低彩度"),
  ].filter(Boolean);
}

function warmEffectValues() {
  return [
    currentEffectValue("暖色フレア"),
    currentEffectValue("光漏れ"),
    currentEffectValue("夕方斜光"),
  ].filter(Boolean);
}

function coolEffectValues() {
  return [
    currentEffectValue("冷色フィルター"),
  ].filter(Boolean);
}

function darkEdgeEffectValues() {
  return [
    currentEffectValue("ビネット"),
  ].filter(Boolean);
}

function flashSnapshotEffectValues() {
  return [
    currentEffectValue("直フラッシュ"),
    currentEffectValue("白飛びフラッシュ"),
  ].filter(Boolean);
}

function softDepthLightEffectValues() {
  return [
    currentEffectValue("背景ボケ"),
    currentEffectValue("光の玉ボケ"),
    currentEffectValue("前ボケ"),
    currentEffectValue("ソフトフォーカス"),
    currentEffectValue("逆光/リムライト"),
    currentEffectValue("暖色フレア"),
    currentEffectValue("夕方斜光"),
    currentEffectValue("自然光ハイライト"),
    currentEffectValue("スマホHDR"),
    currentEffectValue("透明感カラー"),
    currentEffectValue("低コントラスト影"),
  ].filter(Boolean);
}

function hardShadowEffectValues() {
  return [
    currentEffectValue("硬い影"),
  ].filter(Boolean);
}

function softShadowEffectValues() {
  return [
    currentEffectValue("低コントラスト影"),
    currentEffectValue("ソフトフォーカス"),
  ].filter(Boolean);
}

function hasFlashSnapshotEffectActive() {
  return selectedCount(flashSnapshotEffectValues()) >= 1;
}

function hasSoftDepthLightEffectActive() {
  return selectedCount(softDepthLightEffectValues()) >= 1;
}

function hasHardShadowEffectActive() {
  return selectedCount(hardShadowEffectValues()) >= 1;
}

function hasSoftShadowEffectActive() {
  return selectedCount(softShadowEffectValues()) >= 1;
}

function grittyEffectValues() {
  return [
    ...grainNoiseEffectValues(),
    ...warmEffectValues(),
    ...coolEffectValues(),
    ...darkEdgeEffectValues(),
  ].filter(Boolean);
}

function cinematicEffectValues() {
  return [
    currentEffectValue("きらめき粒子"),
    currentEffectValue("ソフトフォーカス"),
    currentEffectValue("光の玉ボケ"),
    currentEffectValue("逆光/リムライト"),
  ].filter(Boolean);
}

function transparentToneValue() { return valueByLabel(OVERALL_TONES, "ナチュラル"); }
function streetToneValue() { return valueByLabel(OVERALL_TONES, "ストリート"); }
function darkToneValue() { return valueByLabel(OVERALL_TONES, "ダーク"); }
function cuteToneValue() { return valueByLabel(OVERALL_TONES, "キュート"); }

function transparentFriendlyFilmValues() {
  return [
    "",
    valueByLabel(FILM_TONES, "なし"),
    valueByLabel(FILM_TONES, "フジ"),
  ];
}

function transparentConflictFilmValues() {
  return FILM_TONES
    .map(item => item.value)
    .filter(v => v && !transparentFriendlyFilmValues().includes(v));
}

function warmFilmValues() {
  return [
    valueByLabel(FILM_TONES, "コダック ゴールド"),
    valueByLabel(FILM_TONES, "ポートラ"),
    valueByLabel(FILM_TONES, "ポラロイド"),
  ].filter(Boolean);
}

function monochromeFilmValues() {
  return [valueByLabel(FILM_TONES, "イルフォード")].filter(Boolean);
}

function selectedCount(list) {
  return state.effects.filter(v => list.includes(v)).length;
}

function hasStrongTransparentEffectActive() {
  return selectedCount(strongTransparentEffectValues()) >= 1;
}

function hasTransparentStyleActive() {
  const transparentEffects = transparentEffectValues();
  return state.tone === transparentToneValue() || selectedCount(transparentEffects) >= 2 || hasStrongTransparentEffectActive();
}

function hasGrittyStyleActive() {
  return state.tone === streetToneValue()
    || state.tone === darkToneValue()
    || selectedCount(grainNoiseEffectValues()) >= 1
    || selectedCount(darkEdgeEffectValues()) >= 1
    || transparentConflictFilmValues().includes(state.film);
}

function hasWarmStyleActive() {
  return selectedCount(warmEffectValues()) >= 1 || warmFilmValues().includes(state.film);
}

function hasCoolStyleActive() {
  return selectedCount(coolEffectValues()) >= 1 || state.film === valueByLabel(FILM_TONES, "シネスコープ");
}

function isIncompatibleOption(stateKey, itemValue) {
  if (!itemValue) return false;

  const transparentEffects = transparentEffectValues();
  const strongTransparent = strongTransparentEffectValues();
  const grainNoise = grainNoiseEffectValues();
  const grittyEffects = grittyEffectValues();
  const warmEffects = warmEffectValues();
  const coolEffects = coolEffectValues();
  const conflictFilms = transparentConflictFilmValues();
  const warmFilms = warmFilmValues();
  const monoFilms = monochromeFilmValues();
  const flashSnapshotEffects = flashSnapshotEffectValues();
  const softDepthLightEffects = softDepthLightEffectValues();
  const hardShadowEffects = hardShadowEffectValues();
  const softShadowEffects = softShadowEffectValues();

  if (stateKey === "film") {
    if (hasTransparentStyleActive() && conflictFilms.includes(itemValue)) return true;
    if (hasCoolStyleActive() && warmFilms.includes(itemValue)) return true;
    if (hasWarmStyleActive() && itemValue === valueByLabel(FILM_TONES, "シネスコープ")) return true;
  }

  if (stateKey === "tone") {
    if (hasTransparentStyleActive() && (itemValue === streetToneValue() || itemValue === darkToneValue())) return true;
    if (hasGrittyStyleActive() && itemValue === transparentToneValue()) return true;
  }

  if (stateKey === "angleMode") {
    if (state.selfieMode === "on" && angleRequiresSelfieOff(itemValue)) return true;
  }

  if (stateKey === "selfieMode") {
    if (itemValue === "on" && angleRequiresSelfieOff(state.angleMode)) return true;
  }

  if (stateKey === "garmentLight") {
    const currentAngle = state.angleMode === "auto" ? "" : state.angleMode;
    if ((itemValue === "softGlow" || itemValue === "backlitEdge") && !isBacklightSafeAngle(currentAngle, state.selfieMode || "auto")) {
      return true;
    }
  }

  if (stateKey === "effects") {
    if (isOvercastLikeWeatherActive() && itemValue === sparkleEffectValue()) return true;

    if (hasFlashSnapshotEffectActive() && softDepthLightEffects.includes(itemValue)) return true;
    if (hasSoftDepthLightEffectActive() && flashSnapshotEffects.includes(itemValue)) return true;

    if (hasHardShadowEffectActive() && softShadowEffects.includes(itemValue)) return true;
    if (hasSoftShadowEffectActive() && hardShadowEffects.includes(itemValue)) return true;

    if (hasTransparentStyleActive() && grittyEffects.includes(itemValue)) return true;
    if (hasGrittyStyleActive() && strongTransparent.includes(itemValue)) return true;
    if (state.film && conflictFilms.includes(state.film) && transparentEffects.includes(itemValue)) return true;

    if (hasWarmStyleActive() && coolEffects.includes(itemValue)) return true;
    if (hasCoolStyleActive() && warmEffects.includes(itemValue)) return true;

    if (monoFilms.includes(state.film) && transparentEffects.includes(itemValue)) return true;

    if (state.tone === streetToneValue() && strongTransparent.includes(itemValue)) return true;
    if (state.tone === darkToneValue() && strongTransparent.includes(itemValue)) return true;
  }

  return false;
}

function normalizeCompatibleState(changedKey) {
  if (changedKey === "weather" && isOvercastLikeWeatherActive()) {
    state.effects = state.effects.filter(v => v !== sparkleEffectValue());
  }

  if (changedKey === "angleMode" && angleRequiresSelfieOff(state.angleMode)) {
    state.selfieMode = "off";
  }

  if (changedKey === "selfieMode" && state.selfieMode === "on" && angleRequiresSelfieOff(state.angleMode)) {
    state.angleMode = ANGLE_UI_OPTIONS[0].value;
  }

  if ((changedKey === "angleMode" || changedKey === "selfieMode") && !isBacklightSafeAngle(state.angleMode, state.selfieMode || "auto")) {
    if (state.garmentLight === "softGlow" || state.garmentLight === "backlitEdge") state.garmentLight = "";
  }

  const transparentEffects = transparentEffectValues();
  const strongTransparent = strongTransparentEffectValues();
  const grainNoise = grainNoiseEffectValues();
  const grittyEffects = grittyEffectValues();
  const warmEffects = warmEffectValues();
  const coolEffects = coolEffectValues();
  const conflictFilms = transparentConflictFilmValues();
  const warmFilms = warmFilmValues();
  const monoFilms = monochromeFilmValues();
  const flashSnapshotEffects = flashSnapshotEffectValues();
  const softDepthLightEffects = softDepthLightEffectValues();
  const hardShadowEffects = hardShadowEffectValues();
  const softShadowEffects = softShadowEffectValues();

  if (changedKey === "tone" && state.tone === transparentToneValue()) {
    if (conflictFilms.includes(state.film)) state.film = "";
    state.effects = state.effects.filter(v => !grittyEffects.includes(v));
  }

  if (changedKey === "tone" && (state.tone === streetToneValue() || state.tone === darkToneValue())) {
    state.effects = state.effects.filter(v => !strongTransparent.includes(v));
    if (state.tone === darkToneValue()) state.effects = state.effects.filter(v => !warmEffects.includes(v));
  }

  if (changedKey === "film") {
    if (conflictFilms.includes(state.film)) {
      if (state.tone === transparentToneValue()) state.tone = "";
      state.effects = state.effects.filter(v => !transparentEffects.includes(v));
    }
    if (warmFilms.includes(state.film)) state.effects = state.effects.filter(v => !coolEffects.includes(v));
    if (state.film === valueByLabel(FILM_TONES, "シネスコープ")) state.effects = state.effects.filter(v => !warmEffects.includes(v));
    if (monoFilms.includes(state.film)) state.effects = state.effects.filter(v => !transparentEffects.includes(v));
  }

  if (changedKey === "effects") {
    if (selectedCount(flashSnapshotEffects) >= 1) {
      state.effects = state.effects.filter(v => !softDepthLightEffects.includes(v));
    }

    if (selectedCount(softDepthLightEffects) >= 1) {
      state.effects = state.effects.filter(v => !flashSnapshotEffects.includes(v));
    }

    if (selectedCount(hardShadowEffects) >= 1) {
      state.effects = state.effects.filter(v => !softShadowEffects.includes(v));
    }

    if (selectedCount(softShadowEffects) >= 1) {
      state.effects = state.effects.filter(v => !hardShadowEffects.includes(v));
    }

    if (hasTransparentStyleActive()) {
      if (conflictFilms.includes(state.film)) state.film = "";
      if (state.tone === streetToneValue() || state.tone === darkToneValue()) state.tone = "";
      state.effects = state.effects.filter(v => !grittyEffects.includes(v));
    }

    if (selectedCount(grainNoise) >= 1 || selectedCount(darkEdgeEffectValues()) >= 1) {
      if (state.tone === transparentToneValue()) state.tone = "";
      state.effects = state.effects.filter(v => !strongTransparent.includes(v));
    }

    if (selectedCount(warmEffects) >= 1) {
      state.effects = state.effects.filter(v => !coolEffects.includes(v));
      if (state.film === valueByLabel(FILM_TONES, "シネスコープ")) state.film = "";
    }

    if (selectedCount(coolEffects) >= 1) {
      state.effects = state.effects.filter(v => !warmEffects.includes(v));
      if (warmFilms.includes(state.film)) state.film = "";
    }
  }
}

function renderAllOptionChips() {
  renderChips("characterModeChips", CHARACTER_MODE_OPTIONS, "characterMode");
  renderChips("outfitReferenceModeChips", OUTFIT_REFERENCE_MODE_OPTIONS, "outfitReferenceMode");
  renderChips("outfitReferenceModeChips", OUTFIT_REFERENCE_MODE_OPTIONS, "outfitReferenceMode");
  renderChips("bustChips", BUST_OPTIONS, "bust");
  renderChips("garmentLightChips", GARMENT_BACKLIGHT_OPTIONS, "garmentLight");
  renderChips("hipChips", HIP_OPTIONS, "hip");
  renderChips("selfieModeChips", SELFIE_MODE_OPTIONS, "selfieMode");
  renderChips("weatherChips", WEATHER_OPTIONS, "weather");
  renderChips("filmChips", FILM_TONES, "film");
  renderChips("toneChips", OVERALL_TONES, "tone");
  renderMultiChips("effectChips", EFFECTS, "effects");
  renderChips("effectStrengthChips", EFFECT_STRENGTH_OPTIONS, "effectStrength");
  renderChips("skinFinishChips", SKIN_FINISH_OPTIONS, "skinFinish");
  renderChips("closeupTextureChips", CLOSEUP_TEXTURE_OPTIONS, "closeupTexture");
  renderChips("angleModeChips", ANGLE_UI_OPTIONS, "angleMode");
  renderChips("gazeChips", GAZE_OPTIONS, "gaze");
  renderChips("faceDirectionChips", FACE_DIRECTION_OPTIONS, "faceDirection");
  renderChips("subjectSizeChips", SUBJECT_SIZE_MODES, "subjectSize");
  renderChips("backgroundViewChips", BACKGROUND_VIEW_MODES, "backgroundView");
  renderChips("framingChips", FRAMING_MODES, "framing");
  renderChips("photoStyleChips", PHOTO_STYLE_MODES, "photoStyle");
  renderChips("moodChips", MOOD_OPTIONS, "mood");
}

const MOOD_OPTIONS = [
  {label:"🎲 AIにおまかせ", value:"auto"},
  {label:"😐 ニュートラル", value:"neutral"},
  {label:"😌 落ち着き", value:"calm"},
  {label:"🙂 やさしい", value:"gentle"},
  {label:"😄 楽しい", value:"joyful"},
  {label:"🥱 眠そう / 気だるげ", value:"sleepy"},
  {label:"🌙 寂しい / 物憂げ", value:"melancholic"},
  {label:"😳 照れ / はにかみ", value:"shy"},
  {label:"😟 不安 / 緊張", value:"anxious"},
  {label:"😎 クール / 強め", value:"cool"},
  {label:"🚶 動きあり", value:"motion"},
];

const TENSIONS = [
  {label:"😌 低め（落ち着き）", value:"low"},
  {label:"🙂 普通",           value:"medium"},
  {label:"😄 やや高め",        value:"medium-high"},
  {label:"🤩 高め（元気）",    value:"high"},
];

const EMOTIONS = [
  {label:"😐 ニュートラル", value:"neutral"},
  {label:"😠 腹立つ", value:"angry"},
  {label:"😢 悲しい", value:"sad"},
  {label:"😊 嬉しい", value:"happy"},
  {label:"😆 楽しい", value:"joyful"},
  {label:"🌙 寂しい", value:"lonely"},
  {label:"😟 不安", value:"anxious"},
  {label:"😮 驚き", value:"surprised"},
  {label:"😳 照れ", value:"shy"},
  {label:"😩 疲れた", value:"tired"},
  {label:"😌 落ち着き", value:"calm"},
];

const EXPRESSION_OPTIONS = [
  {label:"😐 真顔/クール",      value:"neutral deadpan, calm, composed expression"},
  {label:"🙂 優しい微笑み",     value:"soft gentle smile, warm and approachable expression"},
  {label:"😊 口角を上げて笑う", value:"gently raised mouth corners, natural warm smile with lifted lips, soft genuine smile"},
  {label:"😄 明るい笑顔",       value:"bright happy, lively cheerful expression"},
  {label:"🥰 甘え/愛おしそう",  value:"sweet, slightly clingy, affectionate expression"},
  {label:"😋 いたずらっぽい笑み", value:"teasing, mischievous smirk expression"},
  {label:"😌 物憂げ",          value:"melancholic, reflective, subtle loneliness in expression"},
  {label:"😪 気だるげ",         value:"tired but gentle, quiet fatigue expression"},
  {label:"🍶 ほろ酔い",        value:"warm relaxed night expression, not intoxicated"},
  {label:"🤔 遠くを見つめる",   value:"thoughtful faraway gaze expression"},
  {label:"☺️ 照れ/はにかみ",   value:"shy blushing expression"},
  {label:"😳 驚き",            value:"surprised slightly startled expression"},
];

const DEFAULT_CHARACTER_LOCK = `(same original adult Korean model woman in every image:1.9),
(preserve the same identity, face, facial proportions, skin tone, and body balance:1.9),
(consistent adult appearance, never younger-looking:1.9),
(refined Korean Asian fashion-model beauty without referencing any real celebrity:1.7),
(Korean fashion editorial model-like refined atmosphere, not idol-cute:1.7),
(very fair translucent skin with natural texture:1.9),
(strikingly pale fair porcelain skin with natural translucency:1.9),
(pale clear complexion, clean white skin tone, soft luminous transparency:1.9),
(light passing softly through the skin impression, sheer luminous skin clarity:1.7),
(low-saturation cool-pink blush, extremely subtle and diffused:1.7),
(blush placed lightly under the eyes and toward the outer upper cheeks, not round cheek blush:1.7),
(minimal color makeup, restrained saturation, transparent makeup finish:1.7),
(smooth flat cheek area with minimal cheekbone prominence:1.9),
(no protruding cheekbones, no rounded puffy cheeks, no apple-cheek emphasis:1.9),
(no thick cheek volume, no heavy lower face, no soft bulky jaw impression:1.9),
(thin cheek contour with clean facial planes:1.8),
(lean elegant midface, restrained facial softness:1.8),
(longer vertical face proportion:1.9),
(longer midface balance:1.9),
(long vertical lower-face balance from ear to chin:1.9),
(slim elongated face silhouette:1.9),
(ear-to-chin line flows smoothly and cleanly:1.9),
(clean narrow side contour from temple to jaw:1.8),
(small pointed chin:1.8),
(sharply tapered delicate V-shaped lower face:1.9),
(narrow slim jawline:1.9),
(slim lower jaw line, narrow jaw width, delicate chin point:1.9),
(minimal cheekbone prominence:1.9),
(flat smooth cheek area:1.9),
(not round face:1.9),
(not broad oval face:1.9),
(not puffy cheeks:1.9),
(not square jaw:1.9),
(no short compact face:1.9),
(no round compact face:1.9),
(no full cheeks, no soft chubby face, no heavy cheek mass:1.9),
(large eyes with refined horizontal length, calm elegant eye presence:1.9),
(large but not round eyes, wide horizontal eye span:1.8),
(horizontally long calm eyes, refined slim eye shape, not round doll eyes:1.9),
(clear double eyelids with low restrained crease, delicate lower eyelid shadow:1.7),
(slightly lowered inner eye corners and subtly lifted outer corners:1.6),
(pale low-shadow facial impression, delicate low-contrast beauty:1.8),
(fragile transparent aura comes from pale skin and soft shadows, not from sad expression:1.9),
(preserve translucent pale skin even when smiling or cheerful:1.8),
(no forced sad expression:1.8),
(soft straight brows with a slight natural arch, not thick, not sharp:1.6),
(straight high nose bridge:1.9),
(long clean nose line:1.9),
(refined narrow nose bridge:1.9),
(long slender nose impression:1.8),
(nose bridge clearly defined from between the eyes to the tip:1.8),
(slightly sharper nose tip:1.7),
(no short nose:1.8),
(no round nose tip:1.8),
(no low nose bridge, no blunt nose shape:1.8),
(clean refined Korean office-fashion beauty impression, transparent and calm aura:1.7),
(naturally slim mature body, realistic balanced proportions:1.7),
(slightly athletic but soft upper-body silhouette, stable through clothing:1.6),
(no fixed mouth shape unless expression requires it:1.7),
(no idol-cute face, no baby face, no round cheeks, no strong smiling expression by default:1.8),
(no celebrity likeness:1.9), (no specific real person face:1.9),
(no face change:1.9), (no different person:1.9),
(no exaggerated body proportions:1.9), (no artificial body shape:1.9)`;

const BUST_OPTIONS = [
  {label:"🫧 控えめ", value:"(normal-size upper-body silhouette through clothing:1.68), (restrained natural bust contour with ordinary adult proportions:1.68), (gentle compact projection without enlargement emphasis:1.7), (outfit drapes naturally with a neat everyday fit:1.72), (slender I-line body remains stable:1.86), (face remains the main focal point:1.88)"},
  {label:"🌿 自然", value:"(natural balanced upper-body garment contour:1.78), (natural bust volume and body line through clothing:1.78), (realistic adult proportions with soft readable structure:1.8), (outfit fit looks natural and believable:1.78), (slender I-line body remains stable:1.86), (face remains the main focal point:1.88)"},
  {label:"⬆️ 立体感", value:"(slightly fuller upper-body silhouette through clothing:1.88), (high-set lifted bust position through clothing:1.9), (firm structured upper-body garment contour:1.88), (forward-projecting slightly larger-looking upper-body silhouette:1.9), (non-sagging lifted shape:1.9), (slender I-line body remains narrow and elegant:1.88), (face remains the main focal point:1.9)"},
  {label:"🧱 ラインくっきり", value:"(slightly fuller readable bust line through opaque clothing:1.88), (defined structured garment contour around the upper body:1.9), (clear silhouette edges with slightly larger-looking definition:1.88), (fabric fit shows shape while remaining public-safe fashion clothing:1.9), (clean visible upper-body contour:1.88), (slender I-line body remains stable:1.88), (face remains the main focal point:1.9)"},
  {label:"⬆️🧱 立体感＋ライン", value:"(slightly fuller and more dimensional upper-body silhouette through clothing:1.92), (high-set lifted bust position through clothing:1.94), (firm forward-projecting upper-body garment contour:1.92), (rounded lower bust curve through the outfit:1.88), (gently arched upper-bust line through clothing:1.86), (non-sagging structured bust silhouette:1.94), (clean defined opaque garment fit around the upper body:1.9), (slender I-line body stays narrow and elegant:1.9), (face remains the main focal point:1.9)"},
  {label:"👚 服装なり", value:"(upper-body silhouette follows the selected outfit naturally:1.8), (loose clothing hides the line, fitted clothing reveals it naturally through opaque fabric:1.8), (fabric thickness, cut, and neckline decide how much shape is visible:1.76), (no forced silhouette beyond the outfit design:1.76), (slender I-line body remains stable:1.86), (face remains the main focal point:1.88)"}
];

const GARMENT_BACKLIGHT_OPTIONS = [
  {label:"🚫 指定なし", value:""},
  {label:"☀️ 光を拾う", value:"lightCatch"},
  {label:"🫧 ふんわり光感", value:"softGlow"},
  {label:"🌙 逆光の輪郭", value:"backlitEdge"}
];

const SKIN_FINISH_OPTIONS = [
  {label:"🎲 おまかせ", key:"auto", value:"", note:"肌質感を固定せず、光やエフェクト側との自然なバランスに任せます"},
  {label:"🌿 自然", key:"natural", value:"(real skin texture:1.85), (natural skin finish:1.82), (balanced skin sheen with no excessive gloss:1.76), (healthy realistic skin appearance:1.8)", note:"リアルな肌の質感を優先。テカりすぎず、ほぼどの光にも合わせやすい標準設定です"},
  {label:"💧 しっとり", key:"moist", value:"(real skin texture:1.84), (soft moisturized skin finish:1.84), (subtle healthy skin sheen:1.8), (supple hydrated skin appearance:1.78)", note:"自然より少し保湿感のある見え方。室内光や窓光、やわらかい写真と相性が良いです"},
  {label:"✨ ツヤあり", key:"dewy", value:"(real skin texture:1.82), (noticeable dewy skin finish:1.86), (soft glossy highlights on skin:1.82), (healthy luminous skin sheen:1.8)", note:"頬・鼻筋・肩・鎖骨にハイライトが乗りやすい方向。盛れやすい反面、強いフラッシュではテカりが強く出やすいです"}
];

const CLOSEUP_TEXTURE_OPTIONS = [
  {label:"🎲 おまかせ", key:"auto", value:"auto", prompt:"(close-up texture detail is derived naturally from the scene, light, and composition:1.8), (do not overprocess the skin or facial detail:1.78)"},
  {label:"🌿 自然", key:"natural", value:"natural", prompt:"(natural realistic close-up detail balance:1.8), (skin detail is clear without overprocessing:1.78), (eyes, lashes, and lips stay readable in a realistic way:1.78)"},
  {label:"💧 しっとり", key:"moist", value:"moist", prompt:"(close-up skin looks softly moisturized and realistic:1.84), (lips and skin retain a subtle hydrated softness:1.82), (fine facial texture remains natural and smooth:1.8)"},
  {label:"🔬 高精細", key:"detailed", value:"detailed", prompt:"(high-detail close-up rendering of eyelashes, lips, pores, and fine skin texture:1.88), (macro-like facial detail while keeping realism:1.86), (clean realistic close-up sharpness on eyes, lips, and skin surface:1.86)"}
];

const GAZE_OPTIONS = [
  {label:"🎲 AIにおまかせ", key:"auto", value:"auto", prompt:"(gaze direction is naturally derived from the scene, mood, and camera setup:1.82), (do not force direct eye contact unless it suits the scene:1.78)"},
  {label:"👀 カメラ目線", key:"camera", value:"camera", prompt:"(eyes naturally meet the lens:1.84), (clear camera-aware gaze:1.82), (eye contact with the viewer feels natural and not forced:1.8)"},
  {label:"↗️ 少し視線を外す", key:"offCamera", value:"offCamera", prompt:"(gaze is slightly off-camera:1.84), (eyes do not stare directly into the lens:1.82), (natural off-axis eye line:1.8)"},
  {label:"🌌 遠くを見る", key:"far", value:"far", prompt:"(gaze is directed into the distance, not at the camera:1.88), (faraway eye line:1.86), (thoughtful off-camera gaze:1.84)"},
  {label:"😌 伏し目", key:"down", value:"down", prompt:"(downward or lowered gaze:1.86), (soft eyelids and lowered eye line:1.84), (not looking directly at the camera:1.82)"}
];

const FACE_DIRECTION_OPTIONS = [
  {label:"🎲 AIにおまかせ", key:"auto", value:"auto", prompt:"(face orientation is naturally derived from the scene, camera setup, and composition:1.8)"},
  {label:"🙂 正面", key:"front", value:"front", prompt:"(front-facing or near-front facial orientation:1.84), (face plane mostly toward the camera:1.82)"},
  {label:"◢ 斜め向き", key:"threeQuarter", value:"threeQuarter", prompt:"(three-quarter facial angle:1.86), (face turned about 20 to 45 degrees from camera:1.84), (natural diagonal face orientation:1.82)"},
  {label:"➡️ 横顔", key:"profile", value:"profile", prompt:"(true side-profile or near-profile facial orientation:1.9), (lateral face line clearly readable:1.88), (one eye dominant in frame:1.82)"},
  {label:"↩️ 振り向き", key:"turnBack", value:"turnBack", prompt:"(looking back over shoulder or gentle turned-back facial orientation:1.86), (face partially turned back in a natural way:1.84), (turn-back angle remains physically believable:1.82)"}
];

const HIP_OPTIONS = [
  {label:"🫧 控えめ", value:"(subtle compact lower-body silhouette:1.6), (straight narrow waist-to-hip line:1.82), (hips remain small and not laterally wide:1.88), (slim I-line body remains clean and narrow:1.86), (realistic mature proportions without exaggeration:1.86)"},
  {label:"🌿 自然", value:"(natural compact lower-body silhouette:1.72), (clean narrow waist-to-hip line:1.84), (hips stay compact, not wide or bulky:1.9), (slim I-line body with believable lower-body balance:1.86), (realistic mature proportions without exaggeration:1.86)"},
  {label:"🍑 小尻プリ", value:"(compact small hips with a gently rounded shape:1.88), (small but firm perky hip silhouette:1.88), (subtle lifted curve without extra side width:1.86), (straight narrow waist-to-hip line remains visible:1.88), (not laterally wide hips, no wide hip spread:1.94), (slim I-line body remains narrow and elegant:1.9)"},
  {label:"🍑⬆️ 小尻アップ", value:"(compact small hips with a clearly lifted shape:1.9), (small firm upward hip silhouette:1.9), (high-set compact lower-body curve without lateral width:1.88), (straight narrow waist-to-hip line remains clean:1.9), (not laterally wide hips, no wide hip spread, not exaggerated:1.95), (slim I-line body remains narrow and elegant:1.9)"},
  {label:"👖 服装なり", value:"(lower-body silhouette follows the selected outfit naturally:1.8), (pants, skirt, swimsuit, or fabric cut decides how much hip line is visible:1.8), (hips remain compact and not laterally wide:1.9), (no forced hip shape beyond the outfit design:1.76), (slim I-line body remains the base:1.88), (realistic mature proportions without exaggeration:1.86)"}
];

let state = {
  characterMode: "light", outfitReferenceMode: "off",
  bust: "", garmentLight: "", hip: "", weather: "", film: "", tone: "",
  effects: [], effectStrength: "standard", skinFinish: SKIN_FINISH_OPTIONS[0].value, closeupTexture: CLOSEUP_TEXTURE_OPTIONS[0].value, selfieMode: "", angleMode: "", gaze: GAZE_OPTIONS[0].value, faceDirection: FACE_DIRECTION_OPTIONS[0].value, subjectSize: "", backgroundView: "", framing: "", photoStyle: "", mood: "auto",
};
let tokyoNow = {};

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

function updateClock() {
  tokyoNow = getTokyoNow();
  document.getElementById("hTime").textContent = tokyoNow.timeStr + " JST";
  document.getElementById("hDay").textContent = tokyoNow.day + " · " + tokyoNow.month + "月 · " + tokyoNow.timeCtx.label;
  document.getElementById("infoDay").innerHTML = "<span class='info-val'>" + tokyoNow.day + " / " + tokyoNow.month + "月 / " + tokyoNow.timeCtx.label + "（" + tokyoNow.timeCtx.en + "）</span>";
  document.getElementById("infoTime").innerHTML = "<span class='info-val'>" + tokyoNow.timeStr + " JST</span>";
  document.getElementById("infoDayMood").textContent = DAY_MOOD[tokyoNow.day];
  document.getElementById("infoHair").textContent = HAIR_BY_MONTH[tokyoNow.month];
}

function bindChipHelp(btn, item) {
  if (!item || !item.help) return;
  btn.classList.add("has-help");
  let timer = null;
  let longPressed = false;

  const start = (ev) => {
    longPressed = false;
    timer = setTimeout(() => {
      longPressed = true;
      showChipHelp(item.label, item.help);
      if (ev && ev.cancelable) ev.preventDefault();
    }, 520);
  };

  const cancel = () => {
    if (timer) clearTimeout(timer);
    timer = null;
  };

  btn.addEventListener("touchstart", start, {passive:false});
  btn.addEventListener("touchend", cancel);
  btn.addEventListener("touchcancel", cancel);
  btn.addEventListener("mousedown", start);
  btn.addEventListener("mouseup", cancel);
  btn.addEventListener("mouseleave", cancel);
  btn.addEventListener("contextmenu", (ev) => {
    ev.preventDefault();
    showChipHelp(item.label, item.help);
  });
  btn.addEventListener("click", (ev) => {
    if (longPressed) {
      ev.preventDefault();
      ev.stopPropagation();
      longPressed = false;
    }
  }, true);
}

function showChipHelp(title, body) {
  const overlay = document.getElementById("chipHelpOverlay");
  const titleEl = document.getElementById("chipHelpTitle");
  const bodyEl = document.getElementById("chipHelpBody");
  if (!overlay || !titleEl || !bodyEl) return;
  titleEl.textContent = title.replace(/^[^\w一-龯ぁ-んァ-ヶ]+/u, "").trim() || title;
  bodyEl.textContent = body;
  overlay.classList.remove("hidden");
}

function hideChipHelp() {
  const overlay = document.getElementById("chipHelpOverlay");
  if (overlay) overlay.classList.add("hidden");
}

function renderChips(containerId, items, stateKey) {
  const el = document.getElementById(containerId);
  if (!el || !Array.isArray(items)) return;
  el.innerHTML = "";
  items.forEach((item) => {
    const btn = document.createElement("button");
    const isActive = state[stateKey] === item.value;
    const isDisabled = !isActive && isIncompatibleOption(stateKey, item.value);
    btn.className = "chip" + (isActive ? " active" : "") + (isDisabled ? " disabled" : "");
    btn.textContent = item.label;
    btn.disabled = isDisabled;
    if (isDisabled) btn.title = "現在の選択と相反するため選択できません";
    btn.onclick = () => {
      if (isDisabled) return;
      if (stateKey === "characterMode") {
        state[stateKey] = item.value || "light";
        resetCharacterLock();
        renderAllOptionChips();
        return;
      }
      state[stateKey] = isActive ? "" : item.value;
      normalizeCompatibleState(stateKey);
      renderAllOptionChips();
    };
    el.appendChild(btn);
  });
}

function renderMultiChips(containerId, items, stateKey) {
  const el = document.getElementById(containerId);
  if (!el || !Array.isArray(items)) return;
  el.innerHTML = "";
  items.forEach((item) => {
    const btn = document.createElement("button");
    const selected = Array.isArray(state[stateKey]) ? state[stateKey] : [];
    const isActive = selected.includes(item.value);
    const isDisabled = !isActive && isIncompatibleOption(stateKey, item.value);
    btn.className = "chip" + (isActive ? " active" : "") + (isDisabled ? " disabled" : "");
    btn.textContent = item.label;
    btn.disabled = isDisabled;
    if (isDisabled) btn.title = "現在の選択と相反するため選択できません";
    btn.onclick = () => {
      if (isDisabled) return;
      if (!Array.isArray(state[stateKey])) state[stateKey] = [];
      const idx = state[stateKey].indexOf(item.value);
      if (idx === -1) state[stateKey].push(item.value);
      else state[stateKey].splice(idx, 1);
      normalizeCompatibleState(stateKey);
      renderAllOptionChips();
    };
    if (stateKey === "effects") bindChipHelp(btn, item);
    el.appendChild(btn);
  });
}

function detectPoseContext(sceneText = "") {
  const t = sceneText || "";
  const floorSeated = /三角座|体育座|床.*座|床に座|床座|あぐら|正座|膝を抱|膝.*立て|壁にもたれて座|floor.*sit|sitting on the floor|cross[- ]legged|knees bent/i.test(t);
  const seated = floorSeated || /座|腰掛|椅子|ソファ|ベンチ|chair|sofa|sitting|seated/i.test(t);
  const reclining = /寝転|寝そべ|横たわ|横になる|うつ伏せ|仰向け|lying|reclining/i.test(t);
  const walking = /歩|散歩|移動|walking|mid-walk/i.test(t);
  const standing = !seated && !reclining && (/立|standing|stand/i.test(t) || !walking);
  const support = /シンク|sink/i.test(t) ? "sink" : /ベランダ|balcony|手すり|柵|フェンス|railing|rail|fence/i.test(t) ? "railing" : /窓|window|ガラス|glass/i.test(t) ? "glass" : /壁|wall/i.test(t) ? "wall" : /机|テーブル|カウンター|キッチン台|desk|table|counter/i.test(t) ? "desk" : /椅子|ソファ|chair|sofa/i.test(t) ? "chair" : floorSeated ? "floor" : "none";
  const tightOutfit = /レギンス|タイト|ミニ|ボディライン|bodycon|leggings|tight/i.test(t);
  return { floorSeated, seated, reclining, walking, standing, support, tightOutfit };
}

function detectLeanDirective(sceneText = "") {
  const t = sceneText || "";
  const active = /もたれ|凭れ|寄りかか|寄り掛か|lean|leaning|rest against|resting against|supported by/i.test(t);
  const facing = /後ろ向き|後向き|背中|背を向け|back[- ]facing|facing away|back toward/i.test(t) ? "back" : /前向き|正面|front[- ]facing|facing forward/i.test(t) ? "front" : /横向き|真横|sideways|side[- ]facing|profile/i.test(t) ? "side" : "auto";
  const surface = /シンク|sink/i.test(t) ? "sink" : /ベランダ|balcony|手すり|柵|フェンス|railing|rail|fence/i.test(t) ? "railing" : /キッチンカウンター|キッチン台|カウンター|counter|bar counter|バーカウンター/i.test(t) ? "counter" : /机|desk|テーブル|table/i.test(t) ? "desk" : /窓|window|ガラス|glass/i.test(t) ? "glass" : /壁|wall/i.test(t) ? "wall" : "auto";
  const strength = /軽く|そっと|gently|lightly|slight/i.test(t) ? "light" : /しっかり|深く|強く|はっきり|clearly|firmly|visibly/i.test(t) ? "strong" : "medium";
  return { active, facing, surface, strength };
}

function resolveLeanSurface(leanCtx = {}, poseCtx = {}) {
  if (leanCtx.surface && leanCtx.surface !== "auto") return leanCtx.surface;
  if (poseCtx.support === "sink") return "sink";
  if (poseCtx.support === "railing") return "railing";
  if (poseCtx.support === "glass") return "glass";
  if (poseCtx.support === "wall") return "wall";
  if (poseCtx.support === "desk") return "counter";
  return "generic";
}

function getLeanSurfaceLabel(surface = "generic") {
  return ({ sink:"sink", railing:"railing", counter:"counter", desk:"desk or table", glass:"glass or window", wall:"wall", generic:"support surface" })[surface] || "support surface";
}

function buildLeanSummary(sceneText = "", poseCtx = {}) {
  const leanCtx = detectLeanDirective(sceneText);
  if (!leanCtx.active) return "";
  const surface = resolveLeanSurface(leanCtx, poseCtx);
  const surfaceLabel = getLeanSurfaceLabel(surface);
  const weightText = leanCtx.strength === "light" ? "lightly transfers part of her weight" : leanCtx.strength === "strong" ? "clearly transfers body weight" : "transfers part of her body weight";
  if (poseCtx.floorSeated && (surface === "wall" || surface === "glass")) {
    return `floor-seated leaning posture with her back or shoulder visibly supported by the ${surfaceLabel}, ${weightText}, compact stable seated balance`;
  }
  if (surface === "sink" || surface === "counter" || surface === "desk") {
    if (leanCtx.facing === "back") return `leaning posture at the ${surfaceLabel}, facing away, with her hips or lower back resting against the edge, ${weightText}, clear support contact`;
    if (leanCtx.facing === "front") return `leaning posture at the ${surfaceLabel}, facing it, with her forearms, elbows, or hands on the edge, upper body gently supported, clearly leaning rather than merely standing`;
    if (leanCtx.facing === "side") return `side-leaning posture at the ${surfaceLabel}, with one hip or side torso touching the edge and one hand or forearm naturally resting there, physically plausible support`;
    return `leaning posture at the ${surfaceLabel}, with a clearly visible contact point and partial body-weight support, not merely standing near it`;
  }
  if (surface === "railing") {
    if (leanCtx.facing === "back") return `leaning posture at the railing, facing away, with her hips or lower back lightly resting against the rail, ${weightText}, stable natural balance`;
    if (leanCtx.facing === "front") return `leaning posture at the railing, facing it, with both hands or forearms naturally placed on the top rail, upper body softly supported`;
    if (leanCtx.facing === "side") return `side-leaning posture at the railing, with one hip and one forearm lightly supported by the rail, clear contact and believable balance`;
    return `leaning posture at the railing with a visible support contact point, ${weightText}, and no awkward floating gap`;
  }
  if (surface === "wall" || surface === "glass") {
    if (leanCtx.facing === "back") return `standing leaning posture with her back, shoulder blade, or lower back visibly supported by the ${surfaceLabel}, ${weightText}, shoulders and spine naturally aligned`;
    if (leanCtx.facing === "side") return `side-leaning posture with one shoulder, upper arm, or hip lightly resting against the ${surfaceLabel}, clear support contact and believable balance`;
    if (leanCtx.facing === "front") return `standing posture close to the ${surfaceLabel}, with one shoulder, arm, or upper back lightly supported by it while keeping a natural front-facing body line`;
    return `leaning posture with a clear support contact against the ${surfaceLabel}, part of the body weight visibly transferred, physically believable`;
  }
  return `leaning posture with a clear support contact point, ${weightText}, visible environmental support, and physically plausible balance`;
}

function buildLeanSupportBlock(sceneText = "", poseCtx = {}) {
  const leanCtx = detectLeanDirective(sceneText);
  if (!leanCtx.active) return "";
  const surface = resolveLeanSurface(leanCtx, poseCtx);
  const surfaceLabel = getLeanSurfaceLabel(surface);
  const lines = [
    "(auto lean/support reflection is active:1.95)",
    "(the subject is visibly leaning against the environment, not merely standing near it:1.95)",
    "(the support contact point is obvious at first glance:1.94)",
    "(part of the body weight is visibly transferred to the support surface:1.92)",
    "(no awkward air gap that breaks the leaning impression:1.92)",
    "(the lean remains physically natural and balanced:1.95)"
  ];
  if (surface === "sink" || surface === "counter" || surface === "desk") {
    if (leanCtx.facing === "back") lines.push(`(she faces away from the ${surfaceLabel} and rests her hips or lower back against its edge:1.95)`, `(pelvis or lower back visibly meets the ${surfaceLabel} edge:1.93)`);
    else if (leanCtx.facing === "front") lines.push(`(she faces the ${surfaceLabel} and places forearms, elbows, or hands on the edge:1.94)`, `(her upper body leans lightly into the ${surfaceLabel} with believable support:1.92)`);
    else if (leanCtx.facing === "side") lines.push(`(she stands side-on at the ${surfaceLabel} with one hip or side torso touching the edge:1.92)`, `(one hand or forearm can naturally rest on the ${surfaceLabel}:1.86)`);
    else lines.push(`(the ${surfaceLabel} clearly supports the pose through the hips, lower back, forearm, hand, or side torso:1.9)`);
  } else if (surface === "railing") {
    if (leanCtx.facing === "back") lines.push("(she faces away from the railing and lightly rests her hips or lower back against it:1.95)");
    else if (leanCtx.facing === "front") lines.push("(she faces the railing and naturally places both hands or forearms on the top rail:1.94)");
    else if (leanCtx.facing === "side") lines.push("(one hip and one forearm lightly rest on the railing in a side-leaning pose:1.93)");
    else lines.push("(the railing clearly supports the pose rather than sitting unused in the background:1.92)");
  } else if (surface === "wall" || surface === "glass") {
    if (leanCtx.facing === "back") lines.push(`(her back, shoulder blade, or lower back visibly contacts the ${surfaceLabel}:1.95)`);
    else if (leanCtx.facing === "side") lines.push(`(one shoulder, upper arm, or hip lightly rests against the ${surfaceLabel}:1.93)`);
    else if (leanCtx.facing === "front") lines.push(`(one shoulder, arm, or upper back stays lightly supported by the ${surfaceLabel} while the body remains front-facing:1.9)`);
    else lines.push(`(the ${surfaceLabel} visibly supports part of the pose:1.92)`);
  } else {
    lines.push("(the environment provides visible and believable support for the pose:1.9)");
  }
  return lines.join(",\n");
}

function getLeanAutoSummary(sceneText = "") {
  const poseCtx = detectPoseContext(sceneText);
  const leanCtx = detectLeanDirective(sceneText);
  if (!leanCtx.active) return "OFF";
  const surface = resolveLeanSurface(leanCtx, poseCtx);
  const surfaceLabel = ({ sink:"シンク", railing:"手すり/柵", counter:"カウンター", desk:"机/テーブル", glass:"ガラス/窓", wall:"壁", generic:"環境支え" })[surface] || "環境支え";
  const facingLabel = ({ back:"後ろ向き", front:"前向き", side:"横向き", auto:"向き自動" })[leanCtx.facing] || "向き自動";
  return `ON（${surfaceLabel} / ${facingLabel}）`;
}

function resolveCameraScenario(angleName, selfieMode, poseCtx, subjectSizeKey) {
  const chin = "neutral chin position, chin not thrust forward, no jutting chin, no projected jaw, no raised chin, neck relaxed and not stretched";
  const phys = "physically plausible posture, natural center of gravity, realistic body support and balance, joints and spine aligned in a believable way, no impossible torso tilt without visible support, no unnatural limb distortion";
  if (angleName === "HIDDEN WAIST-HELD SELFIE" && poseCtx.floorSeated) {
    return { key:"seated-lap-held", prompt:"(resolved camera logic: seated lap-held low selfie:2.0), (subject sits on the floor with knees or folded legs naturally placed:1.9), (smartphone held near lap, lower abdomen, or knees:2.0), (camera viewpoint originates from her seated lap or lower torso:2.0), (lens angles upward toward face and upper body in a physically plausible seated way:1.95), (knees or thighs may appear naturally in the lower frame without becoming the main focus:1.78), (not overhead selfie:1.95), (not arm raised above head:1.95), (not standing waist-held selfie:1.9), (no long arm extension:1.95), " + chin + ", " + phys };
  }
  if (angleName === "HIDDEN WAIST-HELD SELFIE" && poseCtx.seated) {
    return { key:"seated-close-body", prompt:"(resolved camera logic: seated close-body waist-held selfie:1.95), (phone held close to lap or lower torso while seated:1.95), (camera remains low and close to the body:1.9), (lens angles mildly upward toward face and upper body:1.9), (seated posture and hand position are physically plausible:1.9), (not overhead, not arm raised, no long arm extension:1.95), " + chin + ", " + phys };
  }
  if ((angleName === "LOW ANGLE" || angleName === "SUPER LOW ANGLE") && poseCtx.floorSeated) {
    return { key:"floor-seated-low", prompt:"(resolved camera logic: floor-seated low selfie perspective:1.95), (camera sits near lap, knees, or lower torso while she is seated on the floor:1.92), (low viewpoint shows face, upper body, and a natural hint of folded legs in the lower frame:1.86), (upward angle remains physically plausible and not a vertical upshot:1.9), (body weight is supported by floor and wall if present:1.88), " + chin + ", " + phys };
  }
  if (angleName === "SUPER LOW ANGLE" && poseCtx.standing && poseCtx.support === "none") {
    return { key:"supported-standing-low", prompt:"(resolved camera logic: physically plausible standing low-angle selfie:1.9), (low camera perspective remains moderate enough to keep balance realistic:1.88), (torso tilt stays within a natural range unless a wall, desk, or chair visibly supports her:1.92), (one leg may shift weight naturally while the body remains stable:1.84), (a little thigh may appear at the lower frame through composition, not through impossible body tilt:1.8), " + chin + ", " + phys };
  }
  return { key:"base", prompt:null, physical:phys };
}

function buildPosturePrompt(sceneText, scene, poseCtx) {
  const leanSummary = buildLeanSummary(sceneText, poseCtx);
  if (leanSummary) return leanSummary;
  if (poseCtx.floorSeated) return "floor-seated posture, sitting on the floor with knees or folded legs naturally arranged, body supported by the floor" + (poseCtx.support === "wall" || poseCtx.support === "glass" ? ", back or shoulder lightly supported by the wall or glass" : "") + ", compact stable seated balance";
  if (poseCtx.reclining) return "reclining posture, body supported by the bed, sofa, or floor, sideways or resting pose remains physically plausible";
  if (poseCtx.seated) return "seated posture, hips supported by chair, sofa, floor, or bench, torso held with natural balance";
  if (poseCtx.walking) return "walking posture, weight shifts naturally through one step, motion remains realistic";
  if (poseCtx.support === "sink") return "standing posture near the sink, body alignment stays natural and any support remains physically believable";
  if (poseCtx.support === "railing") return "standing posture near the railing, body balance stays natural and support remains believable";
  if (poseCtx.support === "desk") return "standing or leaning posture with one hand or hip lightly supported by the desk or counter, torso tilt stays physically believable";
  if (poseCtx.support === "wall" || poseCtx.support === "glass") return "standing near the wall or glass with subtle support, shoulders and spine remain naturally aligned";
  return "standing posture with natural weight shift through the legs, torso only slightly angled, no unsupported extreme lean";
}

function normalizeExpressionForContext(expression = "", poseCtx = {}, angleName = "") {
  const riskyCamera = angleName === "SUPER LOW ANGLE" || angleName === "LOW ANGLE" || angleName === "HIDDEN WAIST-HELD SELFIE";
  if (/tipsy|intoxicated|drunk/i.test(expression) && (riskyCamera || poseCtx.seated || poseCtx.floorSeated || poseCtx.tightOutfit)) {
    return "warm relaxed night expression, not intoxicated";
  }
  return expression;
}

function getMoodProfile(mood = "auto", sceneText = "") {
  const t = sceneText || "";
  const autoMood = /眠|寝起き|ベッド|布団|朝|深夜|sleepy|bed|tired/i.test(t) ? "sleepy"
    : /飲み|居酒屋|バー|ビール|ワイン|乾杯|bar|drink|beer|wine/i.test(t) ? "calm"
    : /寂し|孤独|海|夜|雨|lonely|melancholic|rain/i.test(t) ? "melancholic"
    : /楽しい|友達|笑|デート|party|fun|happy|date/i.test(t) ? "joyful"
    : /不安|緊張|心配|anxious|nervous/i.test(t) ? "anxious"
    : "neutral";
  const key = !mood || mood === "auto" ? autoMood : mood;
  const map = {
    neutral:{emotion:"neutral", tension:"medium", cue:"neutral natural mood, relaxed readable face and posture"},
    calm:{emotion:"calm", tension:"low", cue:"calm quiet mood, relaxed eyes, soft mouth, minimal movement"},
    gentle:{emotion:"happy", tension:"medium", cue:"gentle soft mood, warm eyes, mild smile only when the scene supports it"},
    joyful:{emotion:"joyful", tension:"medium-high", cue:"joyful lively mood, brighter eyes, natural smile and light movement"},
    sleepy:{emotion:"tired", tension:"low", cue:"sleepy or languid mood, heavy eyelids, relaxed mouth, loose shoulders, slow small movement"},
    melancholic:{emotion:"lonely", tension:"low", cue:"melancholic quiet mood, distant eyes, restrained mouth, still posture"},
    shy:{emotion:"shy", tension:"medium", cue:"shy hesitant mood, gentle eyes, small bashful smile only if natural"},
    anxious:{emotion:"anxious", tension:"low", cue:"slightly tense mood, uncertain eyes, compact posture, controlled movement"},
    cool:{emotion:"neutral", tension:"medium", cue:"cool composed mood, controlled gaze, restrained mouth, deliberate posture"},
    motion:{emotion:"neutral", tension:"medium-high", cue:"more active mood, realistic body movement and hair motion while preserving physical plausibility"}
  };
  return {key, ...(map[key] || map.neutral)};
}

function buildAIDerivedExpressionPrompt(sceneText = "", mood = "auto") {
  const profile = getMoodProfile(mood, sceneText);
  return `AI-derived expression from scene and mood: ${profile.cue}; derive facial expression, gaze direction, eyelid tension, mouth shape, shoulders, posture energy, and small motion naturally from the situation; do not use a separate fixed expression preset; do not force a smile or emotion that conflicts with the scene`;
}

function getMoodLabel(value = "auto") {
  return getLabelByValue(MOOD_OPTIONS, value || "auto", "🎲 AIにおまかせ");
}

function resolveMotion(situation, dayMood, timeCtx, manualTension, manualEmotion, scene, angleName, subjectSizeKey, photoStyleKey, selfieMode = "on") {
  const t = situation + " " + dayMood + " " + timeCtx.mood;
  const poseCtx = detectPoseContext(situation);
  const cameraScenario = resolveCameraScenario(angleName, selfieMode, poseCtx, subjectSizeKey);
  let emotion = manualEmotion || "neutral";
  if (!manualEmotion) {
    if (/腹立|怒|ムカ|イラ|irritated|angry|annoyed/.test(t)) emotion = "angry";
    else if (/悲し|泣|つら|切な|sad|grief/.test(t)) emotion = "sad";
    else if (/嬉し|幸せ|happy|glad/.test(t)) emotion = "happy";
    else if (/楽し|遊び|友達|友人|パーティ|joy|fun|party/.test(t)) emotion = "joyful";
    else if (/ひとり|一人|孤独|寂し|lonely|夜|深夜/.test(t)) emotion = "lonely";
    else if (/不安|緊張|心配|anxious|nervous/.test(t)) emotion = "anxious";
    else if (/驚|びっくり|surprised|startled/.test(t)) emotion = "surprised";
    else if (/照れ|恥ず|はにか|shy|blush/.test(t)) emotion = "shy";
    else if (/疲れ|しんど|疲労|残業|仕事|office|tired/.test(t)) emotion = "tired";
    else if (/落ち着|穏やか|静か|calm|relax/.test(t)) emotion = "calm";
    else if (/飲み会|乾杯|友達.*飲|居酒屋.*友|party/.test(t)) emotion = "joyful";
    else if (/飲み|居酒屋|バー|酔|飲ん|tipsy|ビール|ワイン/.test(t)) emotion = "calm";
  }
  let tension = manualTension || "medium";
  if (!manualTension) {
    if (/深夜|ひとり|一人|孤独|静か|quiet|calm|家|自宅|部屋|眠|座|三角座/.test(t)) tension = "low";
    else if (/走|急|hurry|energetic|excited|興奮|はしゃ|元気|パーティ|踊/.test(t)) tension = "high";
    else if (/飲み|バー|居酒屋|友達|集まり|social|にぎや/.test(t)) tension = "medium-high";
  }
  const compositionMap = {
    face:"face-forward flattering composition, stable head and shoulder relationship, face stays dominant while body line remains consistent",
    headClose:"head-dominant close-up composition, eyes, lips, hair, and skin are easy to read while visible upper-body silhouette remains consistent",
    faceCloseup:"close-up composition, face fills most of the frame, visible upper-body garment contour should preserve the selected bust shape when included",
    profileCloseup:"profile close-up composition, side face line, eye, nose bridge, lips, and cheek contour are clearly readable while the crop stays elegant and close",
    extremeFace:"extreme face close-up composition, crop may be tight but identity, hair, and any visible neckline stay consistent",
    upperBody:"upper-body composition, face, shirt line, waist direction, and torso balance clearly readable",
    widerBody:"wider-body composition, more outfit and body line visible while the slender I-line body stays stable",
    balanced:"balanced composition with attractive face, upper body, outfit, and believable context"
  };
  const styleMap = {
    daily:"unforced everyday posture, slight imperfection allowed, candid realism",
    enhanced:"naturally flattering posture, slightly polished but still believable",
    model:"model-like pose control, deliberate shoulder line, subtle but physically plausible body angle",
    editorial:"editorial fashion posture, composed body line with realistic support and balance",
    strong:"strongly directed presentation, intentionally crafted but physically possible pose"
  };
  const posturePrompt = buildPosturePrompt(situation, scene, poseCtx);
  const chinPose = "neutral chin position, chin not thrust forward, no raised chin, neck relaxed, jaw natural";
  const defaultAnglePose = {
    "SUPER HIGH ANGLE":"arm lifted high above head, smartphone high over her head looking down, bird's-eye selfie perspective, face angle stays natural without forcing the chin upward",
    "GOLDEN ANGLE":"camera slightly above eye level, flattering three-quarter facial view, face relaxed and natural",
    "HIGH ANGLE":"camera clearly above eye level, relaxed high-angle selfie, eyes meet lens without lifting chin",
    "EYE LEVEL":"camera at eye height, relaxed direct gaze, minimal perspective distortion",
    "SIDE PROFILE":"true side-view camera position, profile or near-profile face angle, lateral face line and hair silhouette readable",
    "RECLINING SIDE EYE LEVEL":"side eye-level reclining view, camera beside her face, resting posture remains supported",
    "BACK VIEW":"external camera behind the subject, back-view fashion posture, face mostly hidden, no selfie arm",
    "DIAGONAL BACK VIEW":"external camera behind and slightly to the side, three-quarter rear posture, shoulder line readable",
    "BACK OVER SHOULDER":"external over-the-shoulder view from behind, shoulder and hair foregrounded, slight glance back only if natural",
    "WINDOW BACK VIEW":"external camera behind her near the window, she looks outside, hair and shoulders outlined by room or window light",
    "LOW ANGLE":"ordinary front low-angle selfie, phone slightly below chest level, mild upward perspective only",
    "HIDDEN WAIST-HELD SELFIE":"hidden waist-held selfie intent, phone close to waist or lower torso, short folded arm, close-body low handheld perspective",
    "WAIST-SIDE VERTICAL UPSHOT":"legacy vertical upshot disabled; use close-body waist-held logic, not a vertical upshot",
    "SUPER LOW ANGLE":"low selfie perspective kept physically plausible; lower frame may include outfit and a little thigh by framing, not by impossible torso tilt",
    "DYNAMIC TILTED":"slightly diagonal handheld composition, small body twist, natural off-center framing",
    "OVER SHOULDER":"shoulder turned toward camera, face looking back to the lens, candid over-shoulder body line",
    "WALKING":"captured mid-step, one shoulder moving forward, hair and outfit subtly moving"
  };
  const anglePose = (cameraScenario.prompt || defaultAnglePose[angleName] || "natural camera posture") + ", " + chinPose;
  const physicalLock = "physical plausibility lock: natural center of gravity, visible support matches the pose, shoulders, spine, pelvis, knees, and hands align believably, no impossible torso twist, no unsupported extreme lean";
  const bodyPriority = "identity and bodyline priority: face identity does not change, slender I-line body stays stable, selected bust silhouette stays readable when in frame, compact hips do not spread sideways";
  const thighCue = (poseCtx.floorSeated || angleName === "SUPER LOW ANGLE" || angleName === "LOW ANGLE" || angleName === "HIDDEN WAIST-HELD SELFIE") ? "a small amount of thigh or folded leg may appear naturally in the lower frame if consistent with pose and clothing, not as the main focus" : "lower body appears only as much as the framing naturally allows";
  const motionMap = { low:"minimal movement, slow blink, slight breathing motion, stable seated or standing balance", medium:"gentle lean, subtle arm shift, soft hair movement, natural handheld micro-shake", "medium-high":"visible but realistic motion, light body turn, playful tilt within physical limits, hair and clothing moving slightly", high:"energetic but plausible motion, walking or turning only when posture supports it, no impossible limb or spine distortion" };
  const emotionMap = { lonely:"quiet eye mood, restrained mouth movement, still shoulders, subtle distant gaze", sad:"quiet eye mood, restrained mouth movement, still shoulders, subtle downward gaze", tired:"softened eyelids, relaxed mouth, quiet shoulders", happy:"steady gaze, lifted posture, controlled confident shoulders", calm:"relaxed shoulders, easy posture, natural small smile or neutral mouth", joyful:"warm expressive eyes, relaxed posture, playful but physically possible tilt", anxious:"slightly tense eyes, compact posture, hands placed naturally", neutral:"neutral natural posture, readable but not exaggerated facial movement" };
  const motionText = [compositionMap[subjectSizeKey] || compositionMap.balanced, styleMap[photoStyleKey] || "natural portrait posture", posturePrompt, anglePose, physicalLock, bodyPriority, thighCue, emotionMap[emotion] || emotionMap.neutral, motionMap[tension] || motionMap.medium].filter(Boolean).join(", ");
  return { motionText, poseText:motionText, tension, emotion, poseCtx, cameraScenario, cameraPrompt:cameraScenario.prompt || null };
}

function getGarmentBacklightPrompt(selectionValue = "", sceneText = "", angleName = "", selfieMode = "", subjectSizeKey = "") {
  if (!selectionValue) return "";

  const safeRearOrSide = isBacklightSafeAngle(angleName, selfieMode);
  const closeup = isFaceCloseupSubjectKey(subjectSizeKey);
  const sceneLooksRisky = /白い|white|Tシャツ|薄|thin|透け|see-through|胸|胸元|body line|ライン/i.test(sceneText || "");

  const safeBase = [
    "(opaque fashion clothing remains non-revealing in backlight:1.95)",
    "(no see-through clothing, no visible underwear, no explicit body detail:1.95)",
    "(backlight affects only the outer fabric edges and surface glow:1.88)",
    "(face, hair, mood, and fashion styling remain primary:1.9)"
  ];

  if (!safeRearOrSide || closeup || sceneLooksRisky) {
    return [
      "(subtle backlit glow on opaque outer clothing only:1.86)",
      "(fabric edge catches the lamp or window light without revealing body details:1.9)",
      ...safeBase
    ].join(", ");
  }

  if (selectionValue === "lightCatch") {
    return [
      "(backlight softly catches the outer fabric edges:1.86)",
      "(gentle luminous rim on clothing surface:1.82)",
      ...safeBase
    ].join(", ");
  }

  if (selectionValue === "softGlow") {
    return [
      "(soft airy backlit fabric glow from a rear or side angle:1.86)",
      "(fabric looks light because of illumination, not because it is see-through:1.92)",
      ...safeBase
    ].join(", ");
  }

  if (selectionValue === "backlitEdge") {
    return [
      "(rear or side backlight outlines hair, shoulders, and clothing edges:1.88)",
      "(tasteful outer-clothing silhouette in backlight, not body-through-fabric detail:1.92)",
      ...safeBase
    ].join(", ");
  }

  return safeBase.join(", ");
}

function buildBodySilhouetteBlock(subjectSizeMode, bustPrompt, hipPrompt, angleName, sceneText = "") {
  const subjectKey = subjectSizeMode && subjectSizeMode.key ? subjectSizeMode.key : "balanced";
  const meta = getAngleMeta(angleName);
  const closeupNote = isFaceCloseupSubjectKey(subjectKey)
    ? "\nFACE-CLOSEUP BODYLINE RULE:\n(face remains primary, but do not erase the selected bust or bodyline setting when upper body or neckline is visible:1.9),\n(visible upper-body garment contour should preserve the selected bust silhouette naturally within the close crop:1.88),"
    : "";
  if (meta.rear) {
    return `BODY LINE BASE:\n${BODY_LINE_BASE_PROMPT},\n\nREAR / BACK-VIEW SILHOUETTE:\n(back, shoulders, waist line, compact hips, hair, and outer clothing shape are the readable fashion elements:1.88),\n(straight narrow waist-to-hip line remains compact from the rear view:1.9),\n(hips do not spread sideways; lower body stays slim I-line:1.92),\n(opaque garment surface and edge-lighting are visible without explicit body detail:1.9),\n(no see-through body detail, no erotic framing:1.95)`;
  }
  if (meta.side || meta.reclining) {
    return `BODY LINE BASE:\n${BODY_LINE_BASE_PROMPT},\n\nSIDE OUTFIT SILHOUETTE:\n(side-view outfit line follows the selected clothing naturally:1.82),\n(selected bust silhouette remains readable from the side when upper body is in frame:1.88),\n(straight compact waist-to-hip line and narrow hips remain visible without lateral widening:1.9),\n(fabric fit is readable without anatomy focus or erotic emphasis:1.88),\n(face, hair, and mood remain the primary focal point:1.9)\n\nCHEST SILHOUETTE:\n${bustPrompt},\n(the selected chest silhouette option should be reflected clearly but naturally:1.86),\n\nHIP / LOWER-BODY SILHOUETTE:\n${hipPrompt},\n(the selected hip silhouette option should keep the hips compact, not laterally wide:1.9)`;
  }
  return `BODY LINE BASE:\n${BODY_LINE_BASE_PROMPT},${closeupNote}\n\nCHEST SILHOUETTE:\n${bustPrompt},\n(the selected chest silhouette option should be reflected clearly but naturally whenever upper body is in frame:1.88),\n\nHIP / LOWER-BODY SILHOUETTE:\n${hipPrompt},\n(the selected hip silhouette option should keep the hips compact and not laterally wide:1.9),\n\nOVERALL BODY BALANCE:\n(selected bust and hip silhouette settings should both be preserved while keeping the same slender I-line body:1.9),\n(face remains primary focal point, while the selected outfit silhouette is preserved:1.9)`;
}

function normalizeWeatherForTime(weatherVal = "", t = {}) {
  if (!weatherVal) return "";
  const hour = typeof t.hour === "number" ? t.hour : 12;
  const isNight = hour >= 18 || hour < 5;
  if (!isNight) return weatherVal;
  return weatherVal
    .replace(/clear sunny sky, bright natural daylight/g, "clear night sky, dark ambient night light")
    .replace(/bright natural daylight/g, "dim realistic night ambient light")
    .replace(/soft natural daylight/g, "soft practical room or street light");
}

function getOutfitReferenceMode() {
  return OUTFIT_REFERENCE_MODE_OPTIONS.find(m => m.value === state.outfitReferenceMode) || OUTFIT_REFERENCE_MODE_OPTIONS[0];
}

function buildBodyReferenceLockBlock() {
  return `BODY / SILHOUETTE REFERENCE LOCK:
(use the first attached image as the locked subject bodyline reference too, when the body or upper body is visible:1.94),
(preserve the same overall body type, shoulder width, torso narrowness, bust volume, waist position, waist-to-hip line, hip width, and limb slimness from the first reference image:1.92),
(selected bust option may refine the visible garment contour, but it must stay compatible with the locked subject body type:1.9),
(selected hip option may refine compactness and lift, but hips must not become laterally wider than the locked subject bodyline:1.92),
(do not copy the first reference image pose, camera angle, clothing, background, arm extension, chin posture, or hairstyle:1.96),
(if the first reference image does not show enough body information, use the app's slender I-line body base and selected bust/hip options as the fallback:1.88),
(do not use the second outfit reference image for body type, bust size, waist width, hip width, or limb proportions:1.98)`;
}

function buildOutfitReferenceBlock() {
  const mode = getOutfitReferenceMode().key;
  if (mode === "off") return "";
  const base = `OUTFIT / COORDINATE REFERENCE:
(use the second attached image as outfit and coordinate reference only:1.98),
(apply the referenced outfit to the locked subject identity from the first image:1.98),
(do not copy the outfit reference person's face, identity, hair, body type, bust size, waist width, hip width, limb proportions, pose, camera angle, framing, background, or lighting:1.98),
(keep the subject face and bodyline from the character lock while borrowing clothing design from the outfit reference:1.95)`;
  if (mode === "light") {
    return base + `,
(reference only the outfit mood, color palette, rough garment category, and styling atmosphere:1.88),
(scene text and manual clothing description may override small outfit details:1.9)`;
  }
  return base + `,
(copy the clothing coordination, garment types, layering, color balance, fabric impression, silhouette balance, shoes, bag, and accessories from the outfit reference:1.92),
(preserve the outfit reference styling strongly while adapting it to the locked subject's slender I-line body:1.9),
(scene text may override location, pose, camera, mood, and action but should not erase the referenced outfit unless explicitly stated:1.88)`;
}


function isNightLikeScene(sceneText = "", t = {}) {
  const hour = typeof t.hour === "number" ? t.hour : 12;
  return hour >= 18 || hour < 5 || /夜|夜景|星|街灯|店明かり|ネオン|イルミ|海岸|港|水面|繁華街|バー|居酒屋|night|nightscape|streetlight|neon|shore|beach|harbor|promenade/i.test(sceneText || "");
}

function hasFlashEffectSelected(effectsArr = []) {
  const flashValues = flashSnapshotEffectValues();
  return Array.isArray(effectsArr) && effectsArr.some(v => flashValues.includes(v));
}

function buildPortraitBackgroundBalanceBlock(t, sceneText, effectsArr = []) {
  const nightLike = isNightLikeScene(sceneText, t);
  const flashSelected = hasFlashEffectSelected(effectsArr);
  const portraitBase = [
    "(portrait-first composition:1.92)",
    "(subject is the clear main focus:1.95)",
    "(background supports the portrait without dominating:1.9)",
    "(background is softly separated but still readable as a real place:1.86)",
    "(moderate background blur only, not heavy cutout separation:1.9)",
    "(face, expression, hair, outfit, and upper-body silhouette are prioritized:1.92)",
    "(selected bust silhouette must not shrink during background or exposure balancing:1.9)",
    "(soft side highlights keep the upper-body garment contour readable:1.88)"
  ];
  if (!nightLike) return "PORTRAIT / BACKGROUND BALANCE:\n" + portraitBase.join(", ");
  const nightBase = [
    "(night background is present but secondary to the subject:1.9)",
    "(street lights, shop lights, and water or pavement reflections support the portrait:1.9)",
    "(subject and background share the same nighttime exposure feeling:1.92)",
    "(ambient warm streetlight spill subtly affects hair, cheek, shoulder, and outfit edges:1.9)",
    "(face remains visible but not overly bright or studio-lit:1.9)",
    "(realistic smartphone night portrait exposure:1.88)",
    "(background lights stay soft and supportive, not overpowering:1.86)",
    "(no pasted-on subject look, no isolated cutout look:1.95)",
    "(night exposure balancing must not flatten or reduce the selected bust silhouette:1.9)"
  ];
  if (!flashSelected) {
    nightBase.push("(no direct flash look:1.95)");
    nightBase.push("(no front-facing flash illumination:1.95)");
    nightBase.push("(no flat bright facial lighting disconnected from the environment:1.92)");
  }
  return "PORTRAIT / NIGHTSCAPE BALANCE:\n" + portraitBase.concat(nightBase).join(", ");
}

function buildPrompt(t, situation, characterLock, bustPrompt, hipPrompt, skinFinishPrompt, closeupTextureMode, weatherVal, filmVal, toneVal, effectsArr, effectStrengthMode, subjectSizeMode, backgroundViewMode, framingMode, photoStyleMode, angle, gazeMode, faceDirectionMode, expression, scene, accessories, motionResult) {
  const overviewParts = [];
  overviewParts.push("current time: " + t.timeCtx.label + " (" + t.timeCtx.en + "), " + t.timeStr + " JST");
  overviewParts.push("day: " + t.day + " — " + DAY_MOOD[t.day]);
  if (weatherVal) overviewParts.push("weather: " + normalizeWeatherForTime(weatherVal, t));
  overviewParts.push("time-of-day mood: " + t.timeCtx.mood);
  if (filmVal) overviewParts.push(filmVal);
  if (toneVal) overviewParts.push(toneVal);
  const scaledEffectsArr = scaleSelectedEffectPrompts(effectsArr, effectStrengthMode);
  scaledEffectsArr.forEach(fx => overviewParts.push(fx));

  const hasStyleSelection = !!filmVal || !!toneVal || scaledEffectsArr.length > 0;
  const stylePriorityInstruction = hasStyleSelection
    ? "(selected film tone, photo tone, and effects must be clearly visible at first glance:1.75)"
    : "";

  const rawSceneText = situation.trim() || "No scene details provided. Create a realistic everyday portrait scene.";
  const sceneText = sanitizeSceneForFaceReference(rawSceneText);
  const selfieMode = getSelfieMode(sceneText);
  const cameraModePrompt = getCameraModePrompt(selfieMode, angle.name);
  const motionText = motionResult && motionResult.motionText ? motionResult.motionText : "natural physically plausible posture";
  const cameraAnglePrompt = motionResult && motionResult.cameraPrompt ? motionResult.cameraPrompt : angle.prompt;
  const safeExpression = normalizeExpressionForContext(expression, motionResult && motionResult.poseCtx ? motionResult.poseCtx : detectPoseContext(sceneText), angle.name);
  const isSwimwear = detectSwimwearScene(rawSceneText);
  const garmentLightPrompt = getGarmentBacklightPrompt(state.garmentLight || "", sceneText, angle.name, selfieMode, subjectSizeMode.key);
  const effectiveSkinFinishPrompt = skinFinishPrompt || "";
  const effectiveCloseupTexturePrompt = closeupTextureMode && closeupTextureMode.prompt ? closeupTextureMode.prompt : CLOSEUP_TEXTURE_OPTIONS[0].prompt;
  const effectiveBustPrompt = bustPrompt;
  const effectiveHipPrompt = hipPrompt;
  const bodySilhouetteBlock = buildBodySilhouetteBlock(subjectSizeMode, effectiveBustPrompt, effectiveHipPrompt, angle.name, sceneText);
  const effectiveMotionText = motionText;
  const fixedCharacter = characterLock.trim();
  const outfitReferenceBlock = buildOutfitReferenceBlock();
  const bodyReferenceLockBlock = buildBodyReferenceLockBlock();
  const characterModeLabel = state.characterMode === "off" ? "OFF / face reference only" : state.characterMode === "full" ? "FULL / legacy fixed character" : "LIGHT / face reference + atmosphere";
  const portraitBackgroundBalanceBlock = buildPortraitBackgroundBalanceBlock(t, sceneText, effectsArr);
  const leanSupportBlock = buildLeanSupportBlock(sceneText, motionResult && motionResult.poseCtx ? motionResult.poseCtx : detectPoseContext(sceneText));

  return `APP_VERSION: ${APP_VERSION}
ANGLE_ENGINE: chin-control + face-reference-role-control + hidden-waist-held-selfie
HAIR_ENGINE: monthly-hair-priority + no-reference-hairstyle-copy
TIME: ${t.day}, month ${t.month}, ${t.timeCtx.label} / ${t.timeCtx.en}, ${t.timeStr} JST

CHARACTER LOCK MODE:
${characterModeLabel}
${fixedCharacter || "(fixed character text disabled; use Face Reference image for identity and facial atmosphere:1.95)"}

IDENTITY / FACE REFERENCE:
(use the first attached image as face identity and subject bodyline reference:1.98),
(preserve the same adult face identity, facial proportions, skin tone, overall facial atmosphere, and visible body-type baseline:1.98),
(refined Korean Asian fashion-model beauty, mature adult, not idol-cute:1.65),
(very fair translucent skin with real texture:1.85),
(slim elongated V-shaped lower face, narrow jawline, small pointed chin:1.82),
(large horizontally refined eyes, straight high nose bridge, minimal cheek volume:1.75),
(no different person:1.98), (no celebrity likeness:1.98), (no specific real person name:1.98)

FACE REFERENCE ROLE CONTROL:
(use Face Reference for face identity, facial atmosphere, and bodyline baseline only, not pose/camera/hair/outfit:1.98),
(do not copy reference camera angle, selfie arm extension, chin posture, facial tilt, body pose, crop, framing, background, hair length, hairstyle, hair silhouette, parting, or hair volume shape:1.98),
(create a new pose, camera position, scene, outfit, and app-priority hairstyle from this prompt while keeping the locked face and body type:1.95)

${bodyReferenceLockBlock}

${outfitReferenceBlock ? outfitReferenceBlock + "\n\n" : ""}HAIR — APP MONTHLY PRIORITY:
${getMonthlyHairBlock(t.month)}

SAFETY / REALISM:
${isSwimwear ? "(safe non-sexual adult cute swimsuit portrait at a beach/pool/resort:1.95),\n(cute resort bikini swimsuit, opaque non-transparent fabric, not lingerie or underwear:1.95),\n(not sporty competition swimwear:1.9),\n(composition is face-and-resort-atmosphere first, not erotic or anatomy-focused:1.9),\n(natural adult body balance is preserved without anatomy emphasis:1.85)," : "(safe non-sexual adult fashion portrait:1.95),\n(opaque public-safe fashion clothing, no lingerie/underwear/pin-up/fetish styling:1.95),\n(composition is face-and-fashion first, not erotic or anatomy-focused:1.9),\n(natural adult body silhouette is preserved; do not flatten or reduce bust volume:1.85),"}
(photographic realism only:1.95), (real skin texture, realistic lighting and shadows:1.85),
(no anime, no illustration, no plastic skin, no waxy skin, no beauty filter:1.9)

SCENE:
${sceneText}
(scene text overrides default location, clothing, pose and action, but never overrides face-reference safety or app-priority hair rules:1.9)

${leanSupportBlock ? `SUPPORT / LEAN AUTO-REFLECTION:
${leanSupportBlock}

` : ""}CONTEXT / STYLE:
${overviewParts.join(", ")}
${stylePriorityInstruction}

${portraitBackgroundBalanceBlock}

ASPECT / ENVIRONMENT:
(aspect ratio 9:16:1.6), (vertical smartphone framing:1.6),
(real Japanese location, realistic crowd/posture/signage/ambient lighting:1.75)

CAMERA MODE:
${cameraModePrompt}

CAMERA POSITION / ANGLE — ${angle.name}:
${cameraAnglePrompt}

COMPOSITION:
${subjectSizeMode.value}
${backgroundViewMode.value ? backgroundViewMode.value + "\n" : ""}${framingMode.value}
${photoStyleMode.value}

VIEW / FACE ORIENTATION:
${gazeMode && gazeMode.prompt ? gazeMode.prompt : GAZE_OPTIONS[0].prompt}
${faceDirectionMode && faceDirectionMode.prompt ? faceDirectionMode.prompt : FACE_DIRECTION_OPTIONS[0].prompt}

EXPRESSION / MOOD:
(${safeExpression}:1.9),
(${getMoodProfile(state.mood || "auto", sceneText).cue}:1.88),
(context-driven natural micro-expression matching the situation, time, weather, and atmosphere:1.82),
(expression, posture energy, and movement are automatically derived from the scene and mood; gaze direction and face orientation should follow the selected controls when provided:1.9),
(keep cheek volume restrained even when smiling:1.85)

POSE / MOTION:
(${effectiveMotionText}:1.7)

${garmentLightPrompt ? "GARMENT BACKLIGHT RESPONSE:\n" + garmentLightPrompt + "\n\n" : ""}${bodySilhouetteBlock}

${effectiveSkinFinishPrompt ? "SKIN FINISH:\n" + effectiveSkinFinishPrompt + ",\n(the selected skin finish option should be reflected clearly but realistically:1.82),\n(keep skin texture real and not plastic even when dewy:1.88)\n\n" : ""}${effectiveCloseupTexturePrompt ? "CLOSE-UP DETAIL / TEXTURE:\n" + effectiveCloseupTexturePrompt + ",\n(when the composition is a close-up or profile close-up, keep the facial detail crisp, realistic, and consistent with the selected texture mode:1.84),\n(do not turn skin into plastic blur or artificial beauty-filter smoothness:1.88)\n\n" : ""}ACCESSORIES / HAIR / LIGHTING:
${accessories}
(realistic ambient lighting:1.7), (real smartphone rendering:1.75), (natural handheld micro-shake:1.5)`;
}

function getLabelByValue(items, value, fallback = "未選択") {
  const found = items.find(item => item.value === value);
  return found ? found.label : fallback;
}

function getEffectLabels(values) {
  if (!values || values.length === 0) return "未選択";
  return values.map(v => getLabelByValue(EFFECTS, v, v)).join("、");
}

function getEffectWarning(values) {
  if (!values || values.length <= 6) return "";
  return "<br>⚠️ <b style='color:#fbbf24'>エフェクト多め</b>：効きは強くなっています。重ねすぎると顔・肌・輪郭が不安定になりやすいので、元画像風なら4〜6個までがおすすめ。";
}

function getCompatibilityHint() {
  if (hasFlashSnapshotEffectActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>フラッシュ整合性ロック</b>：直フラッシュ/白飛びフラッシュ中は、背景ボケ・玉ボケ・前ボケ・自然光/逆光/夕方斜光系は選択不可。";
  }
  if (hasSoftDepthLightEffectActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>背景/自然光整合性ロック</b>：背景ボケ・玉ボケ・前ボケ・自然光/逆光/夕方斜光系の選択中は、直フラッシュ/白飛びフラッシュは選択不可。";
  }
  if (hasHardShadowEffectActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>影質ロック</b>：硬い影の選択中は、低コントラスト影/ソフトフォーカスは選択不可。";
  }
  if (hasSoftShadowEffectActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>影質ロック</b>：低コントラスト影/ソフトフォーカス中は、硬い影は選択不可。";
  }
  if (isOvercastLikeWeatherActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>曇天ロック</b>：曇り・雨・霧では、晴れっぽく見えるキラキラ粒子は選択不可。";
  }
  if (hasTransparentStyleActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>整合性ロック</b>：透明感スマホ系と相反するフィルム/粒状/暗め/強い暖冷色系は選択不可。";
  }
  if (hasGrittyStyleActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>整合性ロック</b>：粒状・ストリート・暗め系と相反する透明感HDR系は選択不可。";
  }
  if (hasWarmStyleActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>整合性ロック</b>：暖色系と相反する冷色フィルターは選択不可。";
  }
  if (hasCoolStyleActive()) {
    return "<br>🔒 <b style='color:#93c5fd'>整合性ロック</b>：冷色系と相反する暖色フレア/光漏れは選択不可。";
  }
  return "";
}

function getTransparentSmartphonePresetHint(values) {
  const required = [
    currentEffectValue("自然光ハイライト"),
    currentEffectValue("スマホHDR"),
    currentEffectValue("白肌オーバー露光"),
    currentEffectValue("透明感カラー"),
    currentEffectValue("低コントラスト影"),
    currentEffectValue("自撮り広角感")
  ].filter(Boolean);
  const selected = required.filter(v => values.includes(v)).length;
  if (selected >= 4) {
    return "<br>✅ <b style='color:#86efac'>透明感スマホ系</b>：元画像に近い方向のエフェクト構成です。";
  }
  return "";
}

function getEffectStrengthMode() {
  return EFFECT_STRENGTH_OPTIONS.find(m => m.key === state.effectStrength) || EFFECT_STRENGTH_OPTIONS[1];
}

function getSelfieMode(sceneText = "") {
  if (angleRequiresSelfieOff(state.angleMode)) return "off";
  const selected = state.selfieMode || "auto";
  if (selected === "on" || selected === "off") return selected;
  if (/自撮りじゃない|セルフィーじゃない|非自撮り|他撮り|第三者撮影|誰かに撮られ|撮ってもら|non-selfie|third-person|third person|photographed by someone/i.test(sceneText)) return "off";
  return "on";
}

function getSelfieModeLabel(mode) {
  if (mode === "off") return "自撮りOFF / 第三者撮影";
  if (mode === "on") return "自撮りON";
  return "自動";
}

function getCameraModePrompt(selfieMode, angleName = "") {
  if (selfieMode === "off") {
    return `============================================================
CAMERA MODE — NON-SELFIE / THIRD-PERSON PHOTO
============================================================
(non-selfie portrait photo:1.95),
(third-person camera viewpoint:1.95),
(photo taken by another person or an external camera:1.9),
(subject is not holding the active camera:1.95),
(no smartphone selfie POV:1.95),
(no arm's-length selfie perspective:1.95),
(no visible selfie arm:1.9),
(no handheld front-camera perspective from the subject's own phone:1.95),
(camera position follows the selected angle as an external photographer's camera:1.9)`;
  }

  if (angleName === "HIDDEN WAIST-HELD SELFIE" || angleName === "WAIST-SIDE VERTICAL UPSHOT") {
    return `============================================================
CAMERA
============================================================
(smartphone in her hand IS the active camera:1.9),
(viewpoint MUST match her discreet waist-held smartphone:1.95),
(only ONE smartphone in scene:1.9)
============================================================
SELFIE POV — HIDDEN WAIST-HELD
============================================================
(POV smartphone front-camera selfie:1.8),
(smartphone held discreetly close to her lower torso or waist:1.95),
(short lowered arm, elbow close to body:1.95),
(phone is not extended far away:1.95),
(no arm's-length selfie pose:1.95),
(no long stretched arm selfie:2.0),
(no visible extended forearm reaching toward the camera:2.0),
(no large foreground arm:2.0),
(no selfie-stick-like arm perspective:2.0),
(no copied reference-image arm extension:1.98),
(camera is ALWAYS her held smartphone:1.9),
(viewpoint ALWAYS from the hidden waist-held front camera:1.95),
(no third-person shots unless the scene explicitly says non-selfie:1.9),
(natural close-body handheld micro-shake:1.75),
(perspective MUST reflect discreet close-body waist-held selfie:1.95)`;
  }

  return `============================================================
CAMERA
============================================================
(smartphone in her hand IS the active camera:1.9),
(viewpoint MUST match her held smartphone:1.9),
(only ONE smartphone in scene:1.9)
============================================================
SELFIE POV
============================================================
(POV smartphone front-camera selfie:1.8),
(random left hand or right hand holding the phone:1.9),
(natural wide-angle selfie distortion:1.6),
(camera is ALWAYS her held smartphone:1.9),
(viewpoint ALWAYS from her hand-held front camera:1.9),
(no third-person shots unless the scene explicitly says non-selfie:1.9),
(natural handheld selfie posture consistent with selected angle:1.8),
(do not copy the Face Reference image's arm extension or camera distance:1.9),
(perspective MUST reflect handheld selfie unless the scene explicitly says non-selfie:1.9)`;
}

function detectSwimwearScene(sceneText = "") {
  return /ビキニ|水着|スイムウェア|swimwear|bikini|swimsuit/i.test(sceneText || "");
}

function detectFaceReferenceSensitiveScene(sceneText = "") {
  return /ブラ|ブラジャー|ランジェリー|下着|ガードル|網タイツ|コルセット|レース|透け|谷間|胸元|前かがみ|うつ伏せ|仰向け|ベッド|寝|水滴|肌|ビキニ|水着|スイムウェア|lingerie|bra|underwear|corset|fishnet|cleavage|bust|sexy|bed|prone|supine|bikini|swimwear|swimsuit/i.test(sceneText);
}

function sanitizeSceneForFaceReference(sceneText = "") {
  let s = sceneText || "";

  const isSwimwear = detectSwimwearScene(sceneText);
  if (isSwimwear) {
    s = s
      .replace(/白いビキニ/g, "白い可愛いビキニ水着")
      .replace(/白い水着/g, "白い可愛い水着")
      .replace(/ビキニ(?!水着)/g, "ビキニ水着")
      .replace(/スイムウェア/g, "水着")
      .replace(/リラックスして座るで肘立て/g, "ビーチチェアかプールサイドでリラックスして座り、片肘を自然に支える")
      .replace(/肘立て/g, "片肘を自然に支える");

    s = s
      .replace(/可愛い可愛い/g, "可愛い")
      .replace(/水着水着/g, "水着")
      .replace(/ビキニ水着水着/g, "ビキニ水着");

    if (/場所はおまかせ|場所おまかせ|おまかせ/.test(s) && !/ビーチ|海|プール|リゾート|pool|beach|resort/i.test(s)) {
      s += "\n場所は、自然なビーチ、プールサイド、またはリゾートの休憩スペース。街中や駅前ではない。";
    }
    s += "\n水着はスポーツ競泳用ではなく、可愛いリゾート向けのファッション水着。上品で明るい夏らしいデザイン。体型表現は選択された②胸シルエット設定をそのまま使い、服装別に別ルールへ切り替えない。";
  }

  const replacements = [
    [/コルセット付きのレースのブラジャーは小さめ/g, "黒いレース襟ブラウスとコルセット風の外着ベスト"],
    [/レースのブラジャーは小さめ/g, "黒いレース襟のファッションブラウス"],
    [/ブラジャー/g, "ファッションブラウス"],
    [/ブラ\b/g, "ファッションブラウス"],
    [/ランジェリー/g, "レース装飾のファッション服"],
    [/下着/g, "透けないファッションインナー"],
    [/かなり薄め/g, "不透明な外着"],
    [/薄手だが/g, "不透明な"],
    [/薄め/g, "軽めだが不透明な"],
    [/薄手/g, "軽めだが不透明な"],
    [/ガードル/g, "ハイウエストのスカートインナー風レイヤー"],
    [/網タイツ/g, "黒い柄入りタイツ"],
    [/透け感/g, "控えめなレース装飾"],
    [/透け/g, "透けない"],
    [/谷間/g, "襟元"],
    [/胸元強調/g, "襟元のデザイン"],
    [/胸元/g, "襟元"],
    [/前かがみ/g, "軽く自然に前傾"],
    [/うつ伏せ/g, "リラックスして座る"],
    [/仰向け/g, "リラックスして座る"],
    [/肌に水滴/g, "窓ガラスの結露"],
    [/水滴/g, "窓ガラスの結露"],
  ];

  if (!isSwimwear) {
    replacements.forEach(([from, to]) => {
      s = s.replace(from, to);
    });
  } else {
    [
      [/前かがみ/g, "軽く自然に前傾"],
      [/うつ伏せ/g, "リラックスして座る"],
      [/仰向け/g, "リラックスして座る"],
      [/肌に水滴/g, "プールサイドの水滴"],
      [/水滴/g, "プールサイドの水滴"],
      [/谷間/g, "水着のネックライン"],
      [/胸元強調/g, "水着のデザイン"],
      [/胸元/g, "水着のネックライン"],
    ].forEach(([from, to]) => {
      s = s.replace(from, to);
    });
  }

  if (detectFaceReferenceSensitiveScene(sceneText)) {
    if (isSwimwear) {
      s += "\n安全な成人の非性的な可愛い水着ポートレート。下着・ランジェリーではなく、ビーチやプールで自然なファッション水着として扱う。挑発的なポーズや胸元中心の構図は禁止。顔・雰囲気・リゾート感・選択された自然なシルエットが主役。";
    } else {
      s += "\n公共の場でも自然なファッションポートレート。下着・ランジェリー・性的演出ではなく、服装は透けない外着として扱う。顔とファッションが主役。";
    }
  }

  return s;
}

function getFaceReferenceSafetyBlock(sceneText = "") {
  const sensitive = detectFaceReferenceSensitiveScene(sceneText);
  return `============================================================
FACE REFERENCE SAFETY — REAL PERSON / REFERENCE IMAGE
============================================================
When a Face Reference image is used, keep the transformation as a safe, non-sexual adult portrait.
Do not sexualize the referenced real person's face or identity.
Do not create lingerie, underwear, erotic, fetish, pin-up, or sexually suggestive styling based on the referenced face.
If the scene contains risky clothing words, reinterpret them as modest fashion garments:
- bra / lingerie -> opaque fashion blouse, corset-style outerwear, or non-underwear fashion top
- girdle / underwear -> high-waist skirt support or ordinary opaque fashion layer
- fishnet -> fashion tights only, not erotic styling
- forward bend -> mild natural lean only, not chest-focused
Keep clothing opaque, public-safe, and fashion editorial.
Face and fashion mood remain the main focus; keep the outfit public-safe and non-erotic.
${sensitive ? "(safety reinterpretation required for this scene:1.95)" : "(safe non-sexual portrait interpretation:1.8)"}`;
}

function getEmotionExpressionCue(emotion) {
  const map = {
    neutral: "neutral calm inner mood, composed eyes, natural mouth",
    angry: "subtle anger, irritated eyes, restrained annoyed expression, not exaggerated",
    sad: "sad inner mood, slightly downcast eyes, quiet sorrow, soft unsmiling mouth",
    happy: "happy inner mood, gentle pleased smile, warm eyes",
    joyful: "joyful fun mood, lively cheerful smile, bright eyes",
    lonely: "lonely inner mood, distant eyes, quiet solitude, subtle melancholy",
    anxious: "anxious inner mood, slightly tense eyes, uncertain mouth, nervous softness",
    surprised: "slightly surprised mood, widened eyes, small parted lips, natural startled expression",
    shy: "shy embarrassed mood, soft blush, hesitant smile, gentle eyes",
    tired: "tired inner mood, quiet fatigue, softened eyelids, relaxed mouth",
    calm: "calm inner mood, relaxed eyes, peaceful neutral expression"
  };
  return map[emotion] || map.neutral;
}

function getHairCopyNegativeDirectives(month) {
  if ([6,7,8].includes(month)) {
    return [
      "(do not copy the Face Reference image's long hairstyle:1.98)",
      "(no long hair:1.98)",
      "(no chest-length hair:1.98)",
      "(hair does not fall below the shoulders:1.98)"
    ].join(",\n");
  }
  if (month === 9) {
    return [
      "(do not copy the Face Reference image's long hairstyle:1.98)",
      "(no chest-length hair:1.98)",
      "(hair stays around shoulder length or shorter:1.95)"
    ].join(",\n");
  }
  if ([4,5].includes(month)) {
    return [
      "(medium-length hair around shoulder length:1.92)",
      "(no very short bob when it conflicts with the monthly hair setting:1.88)",
      "(no very long chest-length hair when it conflicts with the monthly hair setting:1.88)"
    ].join(",\n");
  }
  return [
    "(long hair is allowed for this month:1.8)",
    "(do not shorten the hair into a bob when it conflicts with the monthly hair setting:1.95)"
  ].join(",\n");
}

function getFaceReferenceHairControlBlock(month) {
  return `============================================================
FACE REFERENCE HAIR CONTROL — APP PRIORITY
============================================================
(use the Face Reference image for face identity and facial atmosphere only, not hairstyle:1.98),
(hairstyle must follow the app's monthly hair setting:1.98),
(monthly hair setting overrides the Face Reference hairstyle:1.98),
(do not copy the Face Reference image's hair length:1.98),
(do not copy the Face Reference image's hairstyle:1.98),
(do not copy the Face Reference image's hair silhouette, parting, or volume shape when they conflict with the monthly hair setting:1.96),
(current monthly hair target: ${HAIR_BY_MONTH[month] || "follow the monthly hair setting"}:1.92),
${getHairCopyNegativeDirectives(month)}`;
}

function getMonthlyHairBlock(month) {
  return `${HAIR_BY_MONTH[month] || ""},
(hairstyle must follow the monthly hair setting:1.98),
(monthly hair setting overrides the Face Reference hairstyle:1.98),
(use the Face Reference image for face identity only, not hairstyle:1.98),
(do not copy the Face Reference image's hair length:1.98),
(do not copy the Face Reference image's hairstyle:1.98),
(do not copy the Face Reference image's hair silhouette, parting, or volume shape when they conflict with the monthly hair setting:1.96),
${getHairCopyNegativeDirectives(month)}`;
}

function getAngleMode() {
  if (state.angleMode === "WAIST-SIDE VERTICAL UPSHOT") {
    state.angleMode = "HIDDEN WAIST-HELD SELFIE";
  }
  return ANGLE_UI_OPTIONS.find(m => m.value === state.angleMode) || ANGLE_UI_OPTIONS[0];
}

function getGazeMode() {
  return GAZE_OPTIONS.find(m => m.value === state.gaze) || GAZE_OPTIONS[0];
}

function getFaceDirectionMode() {
  return FACE_DIRECTION_OPTIONS.find(m => m.value === state.faceDirection) || FACE_DIRECTION_OPTIONS[0];
}

function getCloseupTextureMode() {
  return CLOSEUP_TEXTURE_OPTIONS.find(m => m.value === state.closeupTexture) || CLOSEUP_TEXTURE_OPTIONS[0];
}

function getSubjectSizeMode() {
  return SUBJECT_SIZE_MODES.find(m => m.value === state.subjectSize) || SUBJECT_SIZE_MODES[0];
}

function getFramingMode() {
  return FRAMING_MODES.find(m => m.value === state.framing) || FRAMING_MODES[0];
}

function getBackgroundViewMode() {
  return BACKGROUND_VIEW_MODES.find(m => m.value === state.backgroundView) || BACKGROUND_VIEW_MODES[0];
}

function getPhotoStyleMode() {
  return PHOTO_STYLE_MODES.find(m => m.value === state.photoStyle) || PHOTO_STYLE_MODES[0];
}

function pickAngleForComposition(subjectSizeKey, photoStyleKey, selfieMode = "auto", faceDirectionKey = "auto") {
  if (faceDirectionKey === "profile") {
    return ANGLES.find(a => a.name === "SIDE PROFILE") || ANGLES[0];
  }
  if (faceDirectionKey === "turnBack") {
    const target = selfieMode === "off" ? "BACK OVER SHOULDER" : "OVER SHOULDER";
    return ANGLES.find(a => a.name === target) || ANGLES[0];
  }
  if (faceDirectionKey === "front") {
    return ANGLES.find(a => a.name === "EYE LEVEL") || ANGLES[0];
  }

  let weightedNames = [];

  if (subjectSizeKey === "extremeFace") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "SIDE PROFILE", "SIDE PROFILE", "DYNAMIC TILTED"];
  } else if (subjectSizeKey === "profileCloseup") {
    weightedNames = ["SIDE PROFILE", "SIDE PROFILE", "SIDE PROFILE", "OVER SHOULDER", "EYE LEVEL"];
  } else if (subjectSizeKey === "headClose") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "SIDE PROFILE", "HIDDEN WAIST-HELD SELFIE"];
  } else if (subjectSizeKey === "faceCloseup") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "EYE LEVEL", "SIDE PROFILE", "HIDDEN WAIST-HELD SELFIE"];
  } else if (subjectSizeKey === "face") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "WALKING"];
  } else if (subjectSizeKey === "upperBody") {
    weightedNames = ["EYE LEVEL", "HIGH ANGLE", "LOW ANGLE", "OVER SHOULDER"];
  } else if (subjectSizeKey === "widerBody") {
    weightedNames = ["EYE LEVEL", "LOW ANGLE", "WALKING", "DYNAMIC TILTED", "OVER SHOULDER"];
  } else {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "HIGH ANGLE", "SIDE PROFILE", "OVER SHOULDER", "HIDDEN WAIST-HELD SELFIE"];
  }

  if (photoStyleKey === "daily") {
    weightedNames.push("EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "WALKING");
  } else if (photoStyleKey === "enhanced") {
    weightedNames.push("EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "SIDE PROFILE");
  } else if (photoStyleKey === "model") {
    weightedNames.push("EYE LEVEL", "SIDE PROFILE", "LOW ANGLE", "DYNAMIC TILTED");
  } else if (photoStyleKey === "editorial") {
    weightedNames.push("EYE LEVEL", "SIDE PROFILE", "LOW ANGLE", "OVER SHOULDER", "DYNAMIC TILTED", "RECLINING SIDE EYE LEVEL");
  } else if (photoStyleKey === "strong") {
    weightedNames.push("LOW ANGLE", "HIDDEN WAIST-HELD SELFIE", "DYNAMIC TILTED", "RECLINING SIDE EYE LEVEL");
  }

  if (faceDirectionKey === "threeQuarter") {
    weightedNames.push("GOLDEN ANGLE", "EYE LEVEL", "HIGH ANGLE");
  }

  const weightedPool = weightedNames
    .map(name => ANGLES.find(a => a.name === name))
    .filter(Boolean);

  return weightedPool[Math.floor(Math.random() * weightedPool.length)]
    || ANGLES[Math.floor(Math.random() * ANGLES.length)];
}

function handleGenerate() {
  const situation = document.getElementById("situation").value;
  const characterLock = document.getElementById("characterLock").value;
  const btn = document.getElementById("btnGen");
  btn.disabled = true;
  btn.innerHTML = "⏳ 生成中…";

  const t = getTokyoNow();
  tokyoNow = t;
  updateClock();

  const scene = detectScene(situation);
  const accessories = ACCESSORIES_MAP[scene];
  const subjectSizeMode = getSubjectSizeMode();
  const framingMode = getFramingMode();
  const backgroundViewMode = getBackgroundViewMode();
  const photoStyleMode = getPhotoStyleMode();
  const effectStrengthMode = getEffectStrengthMode();
  const angleMode = getAngleMode();
  const gazeMode = getGazeMode();
  const faceDirectionMode = getFaceDirectionMode();
  const closeupTextureMode = getCloseupTextureMode();
  const expectedSelfieMode = getSelfieMode(situation);
  const angle = angleMode.key === "auto"
    ? pickAngleForComposition(subjectSizeMode.key, photoStyleMode.key, expectedSelfieMode, faceDirectionMode.key)
    : (ANGLES.find(a => a.name === angleMode.key) || ANGLES[0]);
  const moodProfile = getMoodProfile(state.mood || "auto", situation);
  const expression = buildAIDerivedExpressionPrompt(situation, state.mood || "auto");

  const motionResult = resolveMotion(situation, DAY_MOOD[t.day], t.timeCtx, moodProfile.tension, moodProfile.emotion, scene, angle.name, subjectSizeMode.key, photoStyleMode.key, expectedSelfieMode);
  const motionText = motionResult.motionText;
  const bustPrompt = state.bust || BUST_OPTIONS[4].value;
  const hipPrompt = state.hip || HIP_OPTIONS[2].value;
  const skinFinishPrompt = state.skinFinish || "";

  const prompt = buildPrompt(t, situation, characterLock, bustPrompt, hipPrompt, skinFinishPrompt, closeupTextureMode, state.weather, state.film, state.tone, state.effects, effectStrengthMode, subjectSizeMode, backgroundViewMode, framingMode, photoStyleMode, angle, gazeMode, faceDirectionMode, expression, scene, accessories, motionResult);

  document.getElementById("metaCard").classList.remove("hidden");
  const selectedOutfitReferenceLabel = getLabelByValue(OUTFIT_REFERENCE_MODE_OPTIONS, state.outfitReferenceMode);
  const selectedWeatherLabel = getLabelByValue(WEATHER_OPTIONS, state.weather);
  const selectedFilmLabel = getLabelByValue(FILM_TONES, state.film);
  const selectedToneLabel = getLabelByValue(OVERALL_TONES, state.tone);
  const selectedEffectLabels = getEffectLabels(state.effects);
  const effectStrengthModeForMeta = getEffectStrengthMode();
  const selectedEffectStrengthLabel = effectStrengthModeForMeta.label + " / weight ×" + effectStrengthModeForMeta.multiplier;
  const selectedAngleModeLabel = getAngleMode().label;
  const selectedSubjectSizeLabel = getSubjectSizeMode().label;
  const selectedBackgroundViewLabel = getBackgroundViewMode().label;
  const selectedFramingLabel = getFramingMode().label;
  const selectedPhotoStyleLabel = getPhotoStyleMode().label;
  const selectedMoodLabel = getMoodLabel(state.mood || "auto");
  const selectedGarmentLightLabel = (GARMENT_BACKLIGHT_OPTIONS.find(g => g.value === (state.garmentLight || ""))?.label || "🚫 指定なし");
  const selectedBustLabel = (BUST_OPTIONS.find(b => b.value === (state.bust || BUST_OPTIONS[4].value))?.label || "⬆️🧱 立体感＋ライン");
  const selectedHipLabel = (HIP_OPTIONS.find(h => h.value === (state.hip || HIP_OPTIONS[2].value))?.label || "🍑 小尻プリ");
  const selectedSkinFinishLabel = (SKIN_FINISH_OPTIONS.find(s => s.value === (state.skinFinish || ""))?.label || "🎲 おまかせ");
  const selectedCloseupTextureLabel = (CLOSEUP_TEXTURE_OPTIONS.find(s => s.value === (state.closeupTexture || CLOSEUP_TEXTURE_OPTIONS[0].value))?.label || "🎲 おまかせ");
  const selectedGazeLabel = (GAZE_OPTIONS.find(g => g.value === (state.gaze || GAZE_OPTIONS[0].value))?.label || "🎲 AIにおまかせ");
  const selectedFaceDirectionLabel = (FACE_DIRECTION_OPTIONS.find(f => f.value === (state.faceDirection || FACE_DIRECTION_OPTIONS[0].value))?.label || "🎲 AIにおまかせ");
  const effectWarning = getEffectWarning(state.effects);
  const transparentPresetHint = getTransparentSmartphonePresetHint(state.effects);
  const compatibilityHint = getCompatibilityHint();

  document.getElementById("metaContent").innerHTML =
    "🧩 <b style='color:#c4b5fd'>App</b>：" + APP_VERSION + "<br>" +
    "🕐 <b style='color:#c4b5fd'>時間帯</b>：" + t.timeCtx.label + " / " + t.timeCtx.en + "<br>" +
    "🔒 <b style='color:#c4b5fd'>固定キャラモード</b>：" + getLabelByValue(CHARACTER_MODE_OPTIONS, state.characterMode) + "<br>" +
    "👗 <b style='color:#c4b5fd'>コーデ参照</b>：" + selectedOutfitReferenceLabel + "<br>" +
    "📅 <b style='color:#c4b5fd'>曜日 mood</b>：" + DAY_MOOD[t.day] + "<br>" +
    "☀️ <b style='color:#c4b5fd'>天気</b>：" + selectedWeatherLabel + "<br>" +
    "🎞️ <b style='color:#c4b5fd'>フィルムトーン</b>：" + selectedFilmLabel + "<br>" +
    "🎨 <b style='color:#c4b5fd'>写真/作品トーン</b>：" + selectedToneLabel + "<br>" +
    "✨ <b style='color:#c4b5fd'>エフェクト</b>：" + selectedEffectLabels + "<br>" +
    "🌟 <b style='color:#c4b5fd'>エフェクト強度</b>：" + selectedEffectStrengthLabel + "<br>" +
    "🫧 <b style='color:#c4b5fd'>肌の見え方</b>：" + selectedSkinFinishLabel + "<br>" +
    "🔬 <b style='color:#c4b5fd'>接写質感</b>：" + selectedCloseupTextureLabel + "<br>" +
    "📸 <b style='color:#c4b5fd'>カメラ位置/アングル</b>：" + selectedAngleModeLabel + " → " + angle.name + "<br>" +
    "👀 <b style='color:#c4b5fd'>視線</b>：" + selectedGazeLabel + "<br>" +
    "🙂 <b style='color:#c4b5fd'>顔向き</b>：" + selectedFaceDirectionLabel + "<br>" +
    "🧍 <b style='color:#c4b5fd'>構図/被写体サイズ</b>：" + selectedSubjectSizeLabel + "<br>" +
    "🌆 <b style='color:#c4b5fd'>背景の見せ方</b>：" + selectedBackgroundViewLabel + "<br>" +
    "🖼️ <b style='color:#c4b5fd'>余白/リーディングスペース</b>：" + selectedFramingLabel + "<br>" +
    "🎭 <b style='color:#c4b5fd'>写真の自然さ/演出度</b>：" + selectedPhotoStyleLabel + "<br>" +
    "✂️ <b style='color:#c4b5fd'>ヘア</b>：" + HAIR_BY_MONTH[t.month] + "<br>" +
    "👜 <b style='color:#c4b5fd'>アクセ</b>：" + scene + "<br>" +
    "☀️ <b style='color:#c4b5fd'>逆光時の布</b>：" + selectedGarmentLightLabel + "<br>" +
    "💭 <b style='color:#c4b5fd'>雰囲気・気分</b>：" + selectedMoodLabel + "<br>" +
    "😊 <b style='color:#c4b5fd'>表情</b>：シチュエーションと雰囲気からAIが自動導出<br>" +
    "🧠 <b style='color:#c4b5fd'>導出カメラ</b>：" + (motionResult.cameraScenario ? motionResult.cameraScenario.key : "base") + "<br>" +
    "🧍 <b style='color:#c4b5fd'>ポーズ/モーション</b>：シチュエーションと雰囲気からAIが自動導出<br>" +
    "🧱 <b style='color:#c4b5fd'>もたれ自動反映</b>：" + getLeanAutoSummary(document.getElementById("situation").value || "") + "<br>" +
    "👚 <b style='color:#c4b5fd'>胸シルエット</b>：" + selectedBustLabel + "<br>" +
    "🍑 <b style='color:#c4b5fd'>ヒップ/下半身</b>：" + selectedHipLabel + "<br>" +
    "🖼️ <b style='color:#c4b5fd'>Face Reference</b>：チャット冒頭の最初の添付画像<br>" +
    (state.outfitReferenceMode !== "off" ? "👗 <b style='color:#c4b5fd'>Outfit Reference</b>：2枚目の添付画像を服装参照<br>" : "") +
    "📷 <b style='color:#c4b5fd'>撮影モード</b>：" + getSelfieModeLabel(getSelfieMode(document.getElementById("situation").value || "")) + "<br>" +
    "🔒 <b style='color:#c4b5fd'>Face Reference安全ロック</b>：ON<br>" +
    (detectFaceReferenceSensitiveScene(document.getElementById("situation").value || "") ? "🧹 <b style='color:#c4b5fd'>危険語サニタイズ</b>：ON<br>" : "") +
    "🧍 <b style='color:#c4b5fd'>体型/胸シルエット</b>：" + selectedBustLabel +
    transparentPresetHint +
    compatibilityHint +
    effectWarning;

  document.getElementById("outputCard").classList.remove("hidden");
  document.getElementById("outputArea").value = prompt;
  copyPromptToClipboard(true);

  btn.disabled = false;
  btn.innerHTML = "✦ プロンプト生成";

  document.getElementById("outputCard").scrollIntoView({ behavior: "smooth" });
}

function handleCopy() {
  copyPromptToClipboard(false);
}

function copyPromptToClipboard(auto = false) {
  const ta = document.getElementById("outputArea");
  const status = document.getElementById("copyStatus");
  if (!ta || !ta.value) return;

  ta.focus();
  ta.select();
  ta.setSelectionRange(0, ta.value.length);

  const onSuccess = () => {
    showCopied(auto);
    if (status) status.textContent = auto ? "✓ 生成プロンプトを自動コピーしました。" : "✓ クリップボードにコピーしました。";
  };

  const onFail = () => {
    fallbackCopy(ta, auto);
  };

  if (navigator.clipboard && navigator.clipboard.writeText) {
    navigator.clipboard.writeText(ta.value).then(onSuccess).catch(onFail);
  } else {
    onFail();
  }
}

function fallbackCopy(ta, auto = false) {
  const status = document.getElementById("copyStatus");
  try {
    const ok = document.execCommand("copy");
    if (ok) {
      showCopied(auto);
      if (status) status.textContent = auto ? "✓ 生成プロンプトを自動コピーしました。" : "✓ クリップボードにコピーしました。";
    } else {
      throw new Error("copy command returned false");
    }
  } catch {
    if (status) status.textContent = auto
      ? "自動コピーできませんでした。Androidの制限で失敗する場合があります。「コピー」ボタンを押してください。"
      : "コピーできませんでした。テキストエリアを長押しして「すべてを選択」→「コピー」してください。";
    if (!auto) alert("コピーできませんでした。テキストエリアを長押しして「すべてを選択」→「コピー」してください。");
  }
}

function showCopied(auto = false) {
  const btn = document.getElementById("btnCopy");
  if (!btn) return;
  btn.textContent = auto ? "✓ 自動コピー済み" : "✓ コピー済み";
  btn.classList.add("copied");
  setTimeout(() => {
    btn.textContent = "コピー";
    btn.classList.remove("copied");
  }, 2500);
}

function getCharacterLockByMode(mode) {
  if (mode === "off") return "";
  if (mode === "full") return DEFAULT_CHARACTER_LOCK;
  return LIGHT_CHARACTER_LOCK;
}

function resetCharacterLock() {
  const mode = state.characterMode || "light";
  document.getElementById("characterLock").value = getCharacterLockByMode(mode);
}

function setCharacterMode(mode) {
  state.characterMode = mode || "light";
  resetCharacterLock();
  renderAllOptionChips();
}

function handleReset() {
  document.getElementById("situation").value = "";
  state = { characterMode:"light", outfitReferenceMode:"off", bust:"", garmentLight:"", hip:"", weather:"", film:"", tone:"", effects:[], effectStrength:"standard", skinFinish:SKIN_FINISH_OPTIONS[0].value, closeupTexture:CLOSEUP_TEXTURE_OPTIONS[0].value, selfieMode:SELFIE_MODE_OPTIONS[0].value, angleMode:ANGLE_UI_OPTIONS[0].value, gaze:GAZE_OPTIONS[0].value, faceDirection:FACE_DIRECTION_OPTIONS[0].value, subjectSize:SUBJECT_SIZE_MODES[0].value, backgroundView:BACKGROUND_VIEW_MODES[0].value, framing:FRAMING_MODES[0].value, photoStyle:PHOTO_STYLE_MODES[0].value, mood:"auto" };
  document.getElementById("metaCard").classList.add("hidden");
  document.getElementById("outputCard").classList.add("hidden");
  document.getElementById("outputArea").value = "";
  renderChips("bustChips", BUST_OPTIONS, "bust");
  renderChips("garmentLightChips", GARMENT_BACKLIGHT_OPTIONS, "garmentLight");
  renderChips("weatherChips", WEATHER_OPTIONS, "weather");
  renderChips("filmChips", FILM_TONES, "film");
  renderChips("toneChips", OVERALL_TONES, "tone");
  renderMultiChips("effectChips", EFFECTS, "effects");
  renderChips("effectStrengthChips", EFFECT_STRENGTH_OPTIONS, "effectStrength");
  renderChips("skinFinishChips", SKIN_FINISH_OPTIONS, "skinFinish");
  renderChips("closeupTextureChips", CLOSEUP_TEXTURE_OPTIONS, "closeupTexture");
  renderChips("angleModeChips", ANGLE_UI_OPTIONS, "angleMode");
  renderChips("gazeChips", GAZE_OPTIONS, "gaze");
  renderChips("faceDirectionChips", FACE_DIRECTION_OPTIONS, "faceDirection");
  renderChips("subjectSizeChips", SUBJECT_SIZE_MODES, "subjectSize");
  renderChips("backgroundViewChips", BACKGROUND_VIEW_MODES, "backgroundView");
  renderChips("framingChips", FRAMING_MODES, "framing");
  renderChips("photoStyleChips", PHOTO_STYLE_MODES, "photoStyle");
  renderChips("moodChips", MOOD_OPTIONS, "mood");
}

document.addEventListener("DOMContentLoaded", () => {
  const characterLockEl = document.getElementById("characterLock");
  state.characterMode = "light";
  state.outfitReferenceMode = OUTFIT_REFERENCE_MODE_OPTIONS[0].value;
  if (characterLockEl) characterLockEl.value = LIGHT_CHARACTER_LOCK;
  state.selfieMode = SELFIE_MODE_OPTIONS[0].value;
  state.angleMode = ANGLE_UI_OPTIONS[0].value;
  state.subjectSize = SUBJECT_SIZE_MODES[0].value;
  state.skinFinish = SKIN_FINISH_OPTIONS[0].value;
  state.closeupTexture = CLOSEUP_TEXTURE_OPTIONS[0].value;
  state.gaze = GAZE_OPTIONS[0].value;
  state.faceDirection = FACE_DIRECTION_OPTIONS[0].value;
  state.framing = FRAMING_MODES[0].value;
  state.photoStyle = PHOTO_STYLE_MODES[0].value;
  updateClock();
  setInterval(updateClock, 30000);
  renderAllOptionChips();
});
</script>
</body>
</html>
