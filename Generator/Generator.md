<!--
  Selfie Prompt Generator
  Version: 3.57.0-effect-help-expanded
  Updated: 2026-07-07
  Changelog:
    v3.57.0 - エフェクト系の長押しヘルプを拡張。各エフェクト/エフェクト強度の「何が変わるか」「向く場面」「注意点」を表示
    v3.56.0 - エフェクト強度を追加。ChatGPT向けにエフェクトを強く出す/自然に抑える切り替えを実装
    v3.55.0 - ③ヒップ/下半身シルエットを追加。細身Iラインを維持しつつ、小尻プリ/小尻アップを選べるように変更
    v3.54.0 - ②胸シルエットを素直なプロンプト化。服装別の裏処理や追加変換をやめ、選択肢の意味がそのまま形に出るよう整理
    v3.53.0 - ②胸シルエットの服装別切り替えを廃止。水着/服装で変えず、選択したシルエットを常に同じ方針で反映
    v3.52.0 - 水着時も②胸シルエット選択を反映するように再調整。胸パーツ詳細ではなく、水着の自然な立体フィット感として表現
    v3.51.0 - 水着時の胸指定を安全寄りに再整理。胸の詳細語を減らし、自然な上半身バランス/水着のフィット感として扱う。可愛い水着の重複変換も修正
    v3.50.0 - 水着表現を「スイムウェア」だけにせず、可愛い水着/ビキニとして出るように修正。安全性は維持しつつ、sporty swimwearへ寄りすぎない文言へ変更
    v3.49.0 - 水着/ビキニ入力用の安全モードを追加。場所おまかせ時はビーチ/プール/リゾートへ寄せ、下着扱い・ゴスロリ変換・街中水着の矛盾を回避
    v3.48.0 - 安全変換を最小化。ゴスロリへの自動置換を削除し、下着/ランジェリー等の危険語だけを中立的な公共ファッション表現へ置換
    v3.47.0 - チップ長押しヘルプを追加。フィルムトーン/作品トーン/エフェクトなどの選択肢を長押しすると、効き方・使いどころ・注意点を表示
    v3.46.0 - ② 胸シルエット に「立体感＋ライン」を追加。名称も 立体感 / ラインくっきり に整理し、単一選択のまま使いやすく調整
    v3.45.0 - ② 胸シルエット選択の名称と並び順を整理。控えめ/自然/前に出る/形くっきり/服装なり に変更し、選択結果が分かりやすい文言へ調整
    v3.44.0 - ⑫ 背景の見せ方 を追加。指定なし / 控えめ / バランス / 足元 / 奥 / 上 の選択肢を実装し、プロンプトとサマリーに反映
    v3.43.0 - ⑧ カメラ位置/アングルの選択項目名と並び順を整理。説明文を短くし、通常系→低め系→動き系→特殊系の順番に変更
    v3.42.0 - ⑧ カメラ位置/アングルUIを見直し。腰だめとSUPER LOWの違いを明確化し、ラベル・説明文・自動選択ロジックを整理。SUPER LOWは明確に「別物/強い煽り」と表示
    v3.41.0 - 腰だめ/隠し持ち自撮りを強化。長く伸びた前腕・腕伸ばしセルフィー・画面手前に大きく写る腕を禁止し、肘を曲げて身体近くに隠したスマホ視点へ寄せる
    v3.40.0 - 固定キャラ設定モードを追加。写真参照ベースでは LIGHT を標準化し、OFF/LIGHT/FULL を切替可能に変更。Face Reference優先時の顔パーツ競合を軽減
    v3.39.0 - 「ほろ酔い」を感情から削除。ほろ酔いは状態/表情側の要素として扱い、感情（内面の気分）は腹立つ/悲しい/嬉しい/楽しい/寂しい/不安/疲れた等に整理
    v3.38.0 - 「感情（内面の気分）」を基本感情ベースに刷新。腹立つ/悲しい/嬉しい/楽しい/寂しい/不安/疲れた/照れ/ほろ酔い/ニュートラル等へ変更し、表情生成にも直接反映
    v3.37.0 - 安全設定をさらに短縮し、胸元を小さく見せる「no cleavage/no chest-focused」の過剰抑制を緩和。非性的・公共安全は維持しつつ、服越しの自然な立体感と選択したBust設定を優先
    v3.36.0 - 生成プロンプトを短縮。重複する顔ID/固定キャラ/安全/構図ブロックを統合し、ChatGPTへ貼りやすいCOMPACT PROMPT出力へ変更。髪型は月別設定優先を維持
    v3.35.0 - Face Reference画像の髪型コピーを抑制。髪型はアプリの月別設定を優先するHAIR CONTROLを追加。参照画像の髪の長さ・シルエット・分け目をそのまま引き継がないネガティブ指示を生成プロンプトに追加
    v3.34.0 - 生成プロンプト内にアプリバージョンを埋め込み。Face Referenceを顔ID参照のみに制限するROLE CONTROLを追加。腰だめ自撮りではarm's-length/腕伸ばし指示を抑制し、旧・腰横真上煽りモードをUIから外した
    v3.33.0 - 顎突き出し抑制CHIN_CONTROLを追加。High/Super High/Goldenの上向き顔・上目線指定を削除し、腰だめを「隠し持ち低め自撮り」と「腰横から真上/強い煽り」に分離
    v3.32.0 - Face Reference使用時に危険な衣装/ポーズ語を安全なファッション表現へ置換。実在人物参照でポリシー停止しやすい語をプロンプト出力前に整理
    v3.31.0 - Face Reference使用時の安全ロックを追加。実在人物参照＋下着/性的強調に見える組み合わせを避ける指示を追加
    v3.30.0 - 自撮りON/OFF/自動切替を追加。OFF時は第三者撮影ポートレートとしてスマホ自撮り指示を抑制
    v3.29.0 - チャットで最初に添付した画像をFace Reference画像として扱う指示を追加。顔ID固定は画像参照を優先
    v3.28.0 - 曇り系の天気でキラキラ粒子を禁止。曇天・雨・霧では晴れっぽい直射感/きらめきに引っ張られないよう整合性ロックを追加
    v3.27.0 - 腰だめを「腰のすぐ横から真上に撮る」定義へ修正。通常ローアングルと分離し、身体横・短い腕・ほぼ垂直上向きカメラを明示
    v3.26.0 - コメント内バージョン表記を修正。腰だめを「身体のそば・短く下げた腕・腰〜ヒップ横のスマホ位置」としてさらに明確化
    v3.21.0 - 矛盾チェック修正。曜日ムードの時間矛盾を解消し、透明感系/粒状フィルム系/暖色系/冷色系の相反選択をより厳密に整理
    v3.1.0 - 胸シルエットを「筋肉質で構造感があるが柔らかい服越し形状」へ調整。服装に応じた自然な谷間許可モードを追加
    v3.0.0 - 固定キャラ設定ブロック、実在人物名削除、服越しシルエット安定化

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
<title>Stable Character Prompt Generator</title>
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
  .chip.disabled {
    opacity: 0.35;
    cursor: not-allowed;
    filter: grayscale(0.6);
  }
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
    <div class="header-sub">固定キャラ + 今回のシーン v3.57</div>
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

  <!-- ① Scene only -->
  <div class="card">
    <div class="slabel">① 今回のシーンだけ（日本語で入力）</div>
    <div class="hint">ここだけ毎回変更：場所・服装・ポーズ・表情・何してるか</div>
    <textarea id="situation" rows="4" placeholder="例：&#10;薄い紺色のワイシャツ、紺色のビジネスパンツ。西中島南方のラーメン店でラーメンをすすっている。"></textarea>
  </div>

  <!-- Chest silhouette -->
  <div class="card">
    <div class="slabel">② 胸シルエット</div>
    <div class="hint">選択した内容をそのままプロンプトに反映します。立体感（前後の厚み）とライン（輪郭）の出方を素直に変えます。</div>
    <div class="chips" id="bustChips"></div>
  </div>

  <!-- Hip silhouette -->
  <div class="card">
    <div class="slabel">③ ヒップ / 下半身シルエット</div>
    <div class="hint">細身Iラインを維持したまま、ヒップの丸み・上向き感を調整します。</div>
    <div class="chips" id="hipChips"></div>
  </div>

  <!-- Weather -->
  <div class="card">
    <div class="slabel">④ 天気を選択</div>
    <div class="chips" id="weatherChips"></div>
  </div>

  <!-- ④ Film tone -->
  <div class="card">
    <div class="slabel">⑤ フィルムトーン / 質感</div>
    <div class="hint">長押しでヘルプ表示。色味・質感・雰囲気を選びます。相反するものは自動で選べません</div>
    <div class="chips" id="filmChips"></div>
  </div>

  <!-- ③ Overall tone -->
  <div class="card">
    <div class="slabel">⑥ 作品トーン</div>
    <div class="hint">長押しでヘルプ表示。写真全体の印象を選びます。反対方向の組み合わせは自動整理</div>
    <div class="chips" id="toneChips"></div>
  </div>

  <!-- ④ Bokeh & Effects -->
  <div class="card">
    <div class="slabel">⑦ エフェクト（複数選択可）</div>
    <div class="hint">各チップを長押しで「何が変わるか・向く場面・注意点」を表示。まずは3〜5個がおすすめ</div>
    <div class="chips" id="effectChips"></div>
  </div>

  <!-- Effect strength -->
  <div class="card">
    <div class="slabel">⑧ エフェクト強度</div>
    <div class="hint">長押しで説明表示。ChatGPTで控えめになりやすい光・粒子・ボケの出方を調整します。Grokは標準でも強めに出やすいです。</div>
    <div class="chips" id="effectStrengthChips"></div>
  </div>

  <!-- Selfie mode -->
  <div class="card">
    <div class="slabel">⑨ 自撮り / 第三者撮影</div>
    <div class="hint">自撮りONならスマホ手持ちカメラ視点。OFFなら他人が撮った自然なポートレート/スナップ扱い。自動は「他撮り・非自撮り」などがシーンにあればOFF、それ以外はON寄りです。</div>
    <div class="chips" id="selfieModeChips"></div>
  </div>

  <!-- Camera angle -->
  <div class="card">
    <div class="slabel">⑩ カメラ位置 / アングル</div>
    <div class="hint">撮影の高さ・持ち方・向きを選びます。</div>
    <div class="chips" id="angleModeChips"></div>
  </div>

  <!-- Subject framing / composition -->
  <div class="card">
    <div class="slabel">⑪ 構図 / 被写体サイズ</div>
    <div class="hint">顔中心か、上半身か、服や体も含めて広めに見せるかを選びます</div>
    <div class="chips" id="subjectSizeChips"></div>
  </div>

  <!-- Background view -->
  <div class="card">
    <div class="slabel">⑫ 背景の見せ方</div>
    <div class="hint">背景をどの方向で見せるかを選びます</div>
    <div class="chips" id="backgroundViewChips"></div>
  </div>

  <!-- Framing space -->
  <div class="card">
    <div class="slabel">⑬ 余白 / リーディングスペース</div>
    <div class="hint">被写体を画像いっぱいにするか、少し余白を残すか、場所を見せるかを選択します。ソファに寝転がる・椅子に座る等では「余白なし / 被写体いっぱい」が使いやすいです</div>
    <div class="chips" id="framingChips"></div>
  </div>

  <!-- Photo naturalness / staging -->
  <div class="card">
    <div class="slabel">⑭ 写真の自然さ / 演出度</div>
    <div class="hint">日常セルフィー寄りか、少し盛るか、モデル風か、ファッション誌風かを選びます</div>
    <div class="chips" id="photoStyleChips"></div>
  </div>

  <!-- Tension -->
  <div class="card">
    <div class="slabel">⑮ テンション（動きの強さ）</div>
    <div class="hint">体の動きの強さや静止感を調整します</div>
    <div class="chips" id="tensionChips"></div>
  </div>

  <!-- Emotion -->
  <div class="card">
    <div class="slabel">⑯ 感情（内面の気分）</div>
    <div class="hint">気分や心理状態を選びます。ポーズと表情の補助に使います</div>
    <div class="chips" id="emotionChips"></div>
  </div>

  <!-- Expression -->
  <div class="card">
    <div class="slabel">⑰ 表情（顔の出力）</div>
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

<div class="help-overlay hidden" id="chipHelpOverlay" onclick="hideChipHelp()">
  <div class="help-sheet" onclick="event.stopPropagation()">
    <div class="help-title" id="chipHelpTitle">ヘルプ</div>
    <div class="help-body" id="chipHelpBody"></div>
    <button class="help-close" onclick="hideChipHelp()">閉じる</button>
  </div>
</div>

<script>
// ── Data ─────────────────────────────────────────────────────────────────────
const HAIR_BY_MONTH = {
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

const APP_VERSION = "v3.57.0-effect-help-expanded";
const CHARACTER_MODE_OPTIONS = [
  {label:"📷 OFF / 写真参照のみ", key:"off", value:"off"},
  {label:"✨ LIGHT / 写真参照＋雰囲気", key:"light", value:"light"},
  {label:"🔒 FULL / 従来の固定キャラ", key:"full", value:"full"},
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
  {name:"LOW ANGLE",        prompt:"(ordinary low-angle selfie from in front of the body:1.8), (phone held slightly below chest level:1.8), (camera below the face and angled only mildly upward from the front:1.8), (viewer sees the subject from a lower front hand position:1.7), (face looking naturally toward the lens without pushing the chin forward:1.8), (not overhead:1.9), (not golden angle:1.8), (not waist-side vertical upshot:1.9), (not near-vertical upward camera axis:1.9), " + CHIN_CONTROL},
  {name:"HIDDEN WAIST-HELD SELFIE", prompt:"(true hidden waist-held selfie:2.0), (smartphone held discreetly against her waist or lower torso:2.0), (elbow bent tightly and close to the body:2.0), (short folded arm, not extended toward the camera:2.0), (phone hidden near the body as if taking a quick discreet selfie:1.98), (camera viewpoint originates from very close to her lower torso or waist:2.0), (lens angled only slightly upward, not vertical:1.98), (close-body low handheld perspective:1.95), (torso feels close to the lens without extreme distortion:1.85), (natural low-angle selfie with subtle upward perspective only:1.85), (no arm's-length selfie pose:2.0), (no long stretched arm selfie:2.0), (no visible extended forearm reaching toward the camera:2.0), (no large foreground arm:2.0), (no selfie stick arm perspective:2.0), (not a normal raised-hand selfie:2.0), (not a dramatic low-angle upshot:1.98), (not a vertical upshot:1.98), (not camera pointing straight upward:1.98), (not near-vertical upward camera axis:1.98), (not phone extended far away:2.0), (do not copy the Face Reference image's camera angle, arm extension, chin posture, or composition:1.95), " + CHIN_CONTROL},
  {name:"WAIST-SIDE VERTICAL UPSHOT", prompt:"(legacy waist-side vertical upshot mode, not recommended for natural waist-held selfies:1.4), (strong vertical upshot only if explicitly required:1.4), (prefer HIDDEN WAIST-HELD SELFIE for natural discreet waist-level selfies:1.9), " + CHIN_CONTROL},
  {name:"SUPER LOW ANGLE",  prompt:"(dramatic super low-angle selfie:1.9), (phone held very low below the waist or near hip-to-thigh level:1.9), (strong upward perspective from far below the face:1.9), (camera looks up sharply with noticeable perspective distortion:1.8), (torso and jacket line strongly emphasized by low perspective:1.8), (face looking naturally toward the lens without jutting the chin:1.8), (not overhead:1.9), (not golden angle:1.9), (not high-angle selfie:1.9), (not waist-side vertical upshot:1.8), " + CHIN_CONTROL},
  {name:"DYNAMIC TILTED",   prompt:"(camera slightly rotated:1.8), (diagonal composition:1.8), (face tilted with camera in a natural way:1.7), (snapshot atmosphere:1.8), (do not copy reference-image chin posture:1.9), " + CHIN_CONTROL},
  {name:"OVER SHOULDER",    prompt:"(face partially turned away:1.7), (looking back toward lens:1.8), (shoulder line emphasized:1.7), (candid feel:1.7), (do not copy reference-image selfie arm extension:1.9), " + CHIN_CONTROL},
  {name:"WALKING",          prompt:"(captured mid-walk:1.8), (subtle body motion:1.7), (hair movement from motion:1.7), (face turned slightly to camera:1.7), (do not copy reference-image chin posture or composition:1.9), " + CHIN_CONTROL},
];

const ANGLE_UI_OPTIONS = [
  {label:"🎲 おまかせ", key:"auto", value:"auto"},

  // ── 標準 / 盛れ角 ──
  {label:"👁️ 目線", key:"EYE LEVEL", value:"EYE LEVEL"},
  {label:"✨ 盛れ角", key:"GOLDEN ANGLE", value:"GOLDEN ANGLE"},
  {label:"⬆️ 少し上から", key:"HIGH ANGLE", value:"HIGH ANGLE"},
  {label:"🙆 頭上から", key:"SUPER HIGH ANGLE", value:"SUPER HIGH ANGLE"},

  // ── 低め自撮り ──
  {label:"🤫 腰だめ", key:"HIDDEN WAIST-HELD SELFIE", value:"HIDDEN WAIST-HELD SELFIE"},
  {label:"⬇️ 低め前持ち", key:"LOW ANGLE", value:"LOW ANGLE"},
  {label:"📉 強い煽り", key:"SUPER LOW ANGLE", value:"SUPER LOW ANGLE"},

  // ── 動き / 特殊 ──
  {label:"🚶 歩き", key:"WALKING", value:"WALKING"},
  {label:"🌀 斜め", key:"DYNAMIC TILTED", value:"DYNAMIC TILTED"},
  {label:"↩️ 振り向き", key:"OVER SHOULDER", value:"OVER SHOULDER"},
];

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
  {label:"曇り ☁️",  value:"overcast cloudy sky, cloud-filtered diffused daylight, muted atmosphere, no direct sunlight, no sparkling sun highlights"},
  {label:"小雨 🌦️", value:"light drizzle rain, wet streets, soft grey ambient light, misty air"},
  {label:"雨 🌧️",   value:"steady rain, rain-soaked streets, dark moody wet atmosphere"},
  {label:"大雨 ⛈️", value:"heavy rain, dramatic downpour, dark stormy atmosphere"},
  {label:"雪 ❄️",   value:"snow falling, winter white scenery, cold crisp air, soft white light"},
  {label:"霧 🌫️",  value:"foggy misty atmosphere, dreamlike hazy soft light"},
];

const FILM_TONES = [
  {label:"なし", value:"", help:"フィルム調を追加しません。\n色味をシーン・天気・照明に任せたい時に使います。迷ったらまずはこれ。"},
  {label:"コダック ゴールド 200", value:"Kodak Gold 200 film tone, clearly visible warm golden cast, noticeable analog warmth, lightly visible grain, unmistakable vintage print feel", help:"暖かい黄色〜金色寄り。\n昼・夕方・街歩き・日常写真に向きます。肌や光がやわらかく見えやすいです。"},
  {label:"フジ プロ 400H", value:"Fuji Pro 400H film tone, clearly visible pastel palette, soft mint-cool shadows, airy film color separation, unmistakable film softness", help:"淡くて透明感のあるパステル寄り。\n曇り・カフェ・白っぽい服・やわらかい雰囲気に向きます。強い影や濃い色は弱まりやすいです。"},
  {label:"コダック ポートラ 800", value:"Kodak Portra 800 film tone, clearly visible rich warm skin, creamy highlight rolloff, noticeable film grain, unmistakable premium portrait film look", help:"人物ポートレート向き。\n肌がクリーミーで少しリッチに見えます。夜・室内・人物中心に使いやすいです。"},
  {label:"イルフォード HP5", value:"Ilford HP5 black and white film, clearly visible monochrome rendering, strong classic contrast, obvious grain texture, unmistakable black-and-white film look", help:"白黒フィルム。\n色より陰影・表情・雰囲気を見せたい時に使います。服や背景の色指定は効きにくくなります。"},
  {label:"シネスコープ", value:"CinemaScope film tone, clearly visible teal and orange grade, cinematic color separation, anamorphic blockbuster look, unmistakable movie-like grading", help:"映画っぽい青緑×オレンジ寄り。\nビル街・夜・都会・ドラマチックな雰囲気に向きます。日常感より作り込んだ印象になります。"},
  {label:"ローモ", value:"Lomography vivid tone, clearly visible cross-processed colors, strong saturation shift, lo-fi contrast, vignette edges, unmistakable lomo look", help:"色ズレ・高彩度・クセのある遊び写真。\n自然さより個性を出したい時向け。顔や肌色が不安定になることがあります。"},
  {label:"ポラロイド", value:"Polaroid instant film tone, clearly visible faded instant-film colors, nostalgic warm cast, soft bloom, unmistakable instant snapshot feel", help:"インスタント写真風。\n淡い・懐かしい・少しぼやけた雰囲気。リアル高精細より、思い出っぽさを出したい時向け。"},
  {label:"ヴィンテージ 90s", value:"1990s vintage film tone, clearly visible retro color shift, muted warm mid-tones, nostalgic softness, unmistakable 90s film-photo mood", help:"90年代の古い写真っぽい色味。\n少し褪せた色・レトロ・生活感を出したい時に向きます。"}
];

const OVERALL_TONES = [
  {label:"なし", value:"", help:"作品トーンを追加しません。\nフィルムトーンやエフェクトだけで調整したい時に使います。"},
  {label:"クール / モダン", value:"clearly visible cool modern aesthetic, crisp clean image design, urban sophisticated mood, unmistakably sleek and contemporary", help:"都会的・すっきり・かっこいい方向。\nビル街、駅、オフィス、黒や紺の服に合いやすいです。"},
  {label:"キュート / 柔らか", value:"clearly visible cute soft aesthetic, gentle pastel atmosphere, soft warm friendliness, unmistakably sweet and tender", help:"明るく親しみやすい方向。\n笑顔、昼、カフェ、やわらかい投稿向き。クール感は弱まります。"},
  {label:"ダーク / ムーディ", value:"clearly visible dark moody aesthetic, deeper shadows, brooding emotional atmosphere, unmistakably heavy and cinematic", help:"影が深く、少し重い雰囲気。\n夜・雨・バー・一人感に向きます。明るい可愛い雰囲気とは相性が悪いです。"},
  {label:"ナチュラル / 透明感", value:"clearly visible natural transparent beauty aesthetic, fresh clean look, airy brightness, unmistakably translucent and refined", help:"透明感・清潔感・薄い光。\n肌や空気を綺麗に見せたい時に使います。粒状・暗め・強い色とは競合しやすいです。"},
  {label:"エレガント / 上品", value:"clearly visible elegant refined aesthetic, graceful composition, polished sophistication, unmistakably classy and upscale", help:"上品・大人・きれいめ。\nワイシャツ、スカート、ホテル、街中ポートレートに使いやすいです。"},
  {label:"ストリート / エッジ", value:"clearly visible street edge aesthetic, raw urban energy, gritty authentic mood, unmistakably rough and street-styled", help:"少し荒くて都会的。\n路地、夜の街、ラフな服に向きます。透明感とは反対方向です。"},
  {label:"ロマンティック", value:"clearly visible romantic dreamy aesthetic, soft warm glow, tender emotional atmosphere, unmistakably dreamy and sentimental", help:"柔らかく夢っぽい雰囲気。\n夕方、花、光漏れ、恋っぽい空気に合います。"},
  {label:"ミニマル / 静寂", value:"clearly visible minimal quiet aesthetic, negative-space calm, restrained serene atmosphere, unmistakably quiet and still", help:"静か・余白・落ち着き。\n人混みより、壁・窓・部屋・静かな場所で使いやすいです。"}
];

// ── Effects (multi-select) ────────────────────────────────────────────────────
const EFFECTS = [
  {label:"🌫️ 背景ボケ", value:"(clearly visible background bokeh blur:1.8), (shallow depth of field with noticeably defocused background:1.8)", help:"何が変わる？
背景が大きくぼけて、人物が前に出ます。

向く場面
駅・街・カフェ・ホームなど背景情報が多い場所。

注意点
背景の文字や場所感は読みにくくなります。場所を見せたい時は弱めか外すのがおすすめ。"},
  {label:"✨ 光の玉ボケ", value:"(clearly visible light orb bokeh:1.8), (ambient light circles in background:1.8), (noticeable specular bokeh highlights:1.8)", help:"何が変わる？
ライトが丸い玉ボケになり、映え感が出ます。

向く場面
夜景・駅の照明・カフェ・街灯・店内ライト。

注意点
昼の自然光だけだと出にくいです。背景に光源があるシーンほど効きます。"},
  {label:"💧 水滴/結露感", value:"(clearly visible condensation droplets on glass or skin:1.7), (noticeable water droplet texture:1.7)", help:"何が変わる？
ガラスや空気に湿度感が出ます。

向く場面
雨の日、窓際、駅のガラス・車内・夜の窓など。

注意点
晴れの屋外では不自然になりやすいです。肌の水滴に寄りすぎる場合は外してください。"},
  {label:"✨ きらめき粒子", value:"(clearly visible sparkling glitter particles in air:1.7), (noticeable shimmering light particles:1.7)", help:"何が変わる？
空気中に小さな光の粒が出ます。SNS加工っぽい可愛い演出になります。

向く場面
記念投稿、感謝テロップ、日差し、夜のライト、可愛い雰囲気。

注意点
リアル写真感は少し下がります。曇り・雨・霧では自動で選べないようにしています。"},
  {label:"🌁 ソフトフォーカス", value:"(clearly visible soft focus haze:1.7), (gentle dreamy blur on edges:1.7), (noticeable diffused hazy atmosphere:1.7)", help:"何が変わる？
輪郭や光が少し柔らかくなり、夢っぽくなります。

向く場面
やわらかい笑顔、夕方、白シャツ、透明感、可愛い投稿。

注意点
服の質感や顔のシャープさは弱まります。くっきり出したい時は外してください。"},
  {label:"🌙 逆光/リムライト", value:"(clearly visible backlighting:1.8), (noticeable rim light on hair and shoulders:1.8), (silhouette-edge glow:1.7)", help:"何が変わる？
髪や肩の輪郭に光が入り、立体感が出ます。

向く場面
駅ホーム、夕方、窓際、ビル街、後ろに明るい光があるシーン。

注意点
顔が暗くなることがあります。顔を明るくしたい時は自然光ハイライトやスマホHDRと相性が良いです。"},
  {label:"📼 VHSノイズ", value:"(clearly visible VHS scan lines:1.7), (retro analog video noise:1.7), (noticeable chromatic aberration:1.7)", help:"何が変わる？
古いビデオ風のノイズ、色ズレ、走査線が出ます。

向く場面
90s、深夜、レトロ、荒いSNS加工、少しクセのある絵。

注意点
顔・手・文字が崩れやすいです。リアル美人寄りなら弱めがおすすめ。"},
  {label:"🔥 暖色フレア", value:"(clearly visible warm lens flare:1.8), (golden warm flare streaks across frame:1.8)", help:"何が変わる？
暖かい光の筋やフレアが入ります。

向く場面
夕方、逆光、夏、駅ホーム、ロマンティックな雰囲気。

注意点
冷色フィルターとは反対方向です。顔にかかりすぎる場合があります。"},
  {label:"❄️ 冷色フィルター", value:"(clearly visible cool blue color grading:1.8), (strong cold tone filter:1.8)", help:"何が変わる？
全体が青く冷たい色味になります。

向く場面
夜、雨、クール、都会、静かな雰囲気。

注意点
肌の血色や可愛い明るさは弱まりやすいです。暖色フレアとは競合します。"},
  {label:"🌈 光漏れ", value:"(clearly visible light leak effect:1.8), (film light leak streaks across frame:1.8)", help:"何が変わる？
フィルム写真のような光の漏れ・色かぶりが入ります。

向く場面
エモい写真、夕方、レトロ、記念投稿。

注意点
顔の上に光が乗ると表情が読みにくくなる場合があります。"},
  {label:"🖤 ビネット", value:"(clearly visible vignette:1.7), (noticeable dark edge falloff around frame:1.7)", help:"何が変わる？
画面の端が暗くなり、中心に視線が集まります。

向く場面
ムーディ、夜、映画風、被写体を強調したい時。

注意点
明るい透明感や爽やかな昼写真とは相性が悪いことがあります。"},
  {label:"🎞️ フィルムグレイン強め", value:"(clearly visible heavy film grain:1.8), (pronounced analog grain texture:1.8)", help:"何が変わる？
粒状感が強くなり、フィルムっぽさが出ます。

向く場面
90s、ポートラ、コダック、駅、スナップ写真。

注意点
肌のなめらかさや顔の安定は少し落ちます。文字も荒れやすいです。"},
  {label:"☀️ 自然光ハイライト", value:"(clearly visible soft natural daylight:1.7), (noticeable highlight on nose bridge and forehead:1.7)", help:"何が変わる？
顔や鼻筋、白シャツに自然な明るさが出ます。

向く場面
昼、駅ホーム、窓際、屋外、爽やかな写真。

注意点
夜や暗い室内では不自然になる場合があります。白飛びが強い時は外してください。"},
  {label:"📱 スマホHDR", value:"(clearly visible smartphone HDR rendering:1.8), (smartphone tonal lift and clean dynamic range:1.8)", help:"何が変わる？
スマホ写真っぽく、暗部と明部が持ち上がります。

向く場面
自撮り、昼、駅、街、顔と背景の両方を見せたい時。

注意点
フィルムの渋さは少し弱くなります。加工っぽいHDRになる場合があります。"},
  {label:"🤍 白肌オーバー露光", value:"(clearly visible slight overexposure on fair skin:1.8), (clean pale skin rendering:1.8)", help:"何が変わる？
肌を少し明るく白めに見せます。

向く場面
白シャツ、透明感、昼、可愛い自撮り。

注意点
白飛びしすぎると顔の立体感や服の質感が薄くなります。"},
  {label:"🫧 透明感カラー", value:"(clearly visible airy transparent color grading:1.8), (smooth but realistic translucent skin texture:1.7)", help:"何が変わる？
色味が軽くなり、清潔感・透明感が出ます。

向く場面
白シャツ、曇り、カフェ、昼、柔らかい表情。

注意点
暗め・粒状・ストリート系とは方向が反対です。"},
  {label:"🌤️ 低コントラスト影", value:"(clearly visible low-contrast facial shadows:1.8), (soft even daylight shadow transition:1.8)", help:"何が変わる？
影が柔らかくなり、顔が優しく見えます。

向く場面
自然な美人写真、白シャツ、昼、透明感。

注意点
ドラマチックな光と影は弱まります。立体感が少し減ることがあります。"},
  {label:"📐 自撮り広角感", value:"(clearly visible natural selfie wide-angle perspective:1.8), (noticeable perspective stretch from smartphone front camera:1.7)", help:"何が変わる？
スマホ自撮りらしい近距離感・広角感が出ます。

向く場面
手持ち自撮り、駅、歩き、SNS投稿っぽい構図。

注意点
顔・腕・手が伸びすぎる時は外してください。腰だめや低角度では強く出すぎることがあります。"}
];

const EFFECT_STRENGTH_OPTIONS = [
  {label:"🫧 控えめ", key:"subtle", value:"EFFECT STRENGTH — SUBTLE:\n(selected effects should stay natural and understated:1.65),\n(effects are visible only as gentle photographic flavor, not decorative overlay:1.65),\n(keep face, skin texture, and realistic station atmosphere stable:1.85)", help:"何が変わる？
エフェクトを自然写真の範囲に抑えます。

向く場面
顔の安定、実写感、駅ホームのリアルさを優先したい時。

注意点
ChatGPTではかなり控えめになりやすいです。Grokでも少し自然寄りになります。"},
  {label:"✨ 標準", key:"standard", value:"EFFECT STRENGTH — STANDARD:\n(selected effects should be clearly visible but still believable:1.75),\n(bokeh, grain, light particles, flares, and softness should be noticeable in the final image:1.75),\n(face and realistic photo quality remain stable:1.85)", help:"何が変わる？
エフェクトを見える程度に出しつつ、写真として自然に保ちます。

向く場面
基本設定。Grokでは十分出やすく、ChatGPTでは自然寄り。

注意点
ChatGPTでもキラキラをはっきり見せたい場合は「強め」が向きます。"},
  {label:"🌟 強め", key:"strong", value:"EFFECT STRENGTH — STRONG:\n(selected effects must be visibly present in the final image, not subtle:1.9),\n(decorative light particles, bokeh orbs, film grain, glow, haze, and lens effects should be easy to notice:1.9),\n(show effects in foreground and background where appropriate:1.82),\n(keep the face clean and realistic despite stronger effects:1.9)", help:"何が変わる？
キラキラ、玉ボケ、粒状感、光、霞みを画面上で分かるように出します。

向く場面
ChatGPTでエフェクトが弱い時、SNS投稿っぽくしたい時。

注意点
顔・肌・文字が少し不安定になる場合があります。"},
  {label:"💥 盛り盛り", key:"max", value:"EFFECT STRENGTH — MAXIMUM VISUAL EFFECTS:\n(selected effects should appear as obvious visual overlays in the final image:1.98),\n(strong decorative sparkle particles, large bokeh orbs, visible grain, glow, flare, haze, and analog artifacts:1.98),\n(effects are intentionally stylized and clearly visible, not natural-subtle:1.95),\n(avoid destroying face identity, eyes, hands, and skin texture:1.95)", help:"何が変わる？
エフェクトを加工レベルで強く見せます。

向く場面
映え重視、Grok風の派手な加工、非日常感。

注意点
Grokだとかなり派手です。ChatGPTでも顔や手が崩れる場合は「強め」に戻してください。"}
];

const SUBJECT_SIZE_MODES = [
  {label:"⚖️ バランス（おすすめ）", key:"balanced", value:"(balanced selfie composition with attractive face, upper body, and believable everyday context:1.8), (face and environment both matter:1.8), (natural handheld framing with believable body scale:1.8)"},
  {label:"✨ 顔優先 / 盛れ重視", key:"face", value:"(face-priority selfie composition:1.8), (clean flattering framing centered on face and upper body:1.8), (beauty-focused composition with less environment emphasis:1.7), (visually refined selfie balance:1.7)"},
  {label:"🔍 顔ズームアップ", key:"faceCloseup", value:"(close-up face selfie composition:1.9), (face fills most of the frame:1.9), (forehead-to-collarbone or face-to-neck framing:1.8), (background exists but is secondary and softly readable:1.5), (eyes and skin texture are the main focus:1.8)"},
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
  // これらは単体でも透明感方向を強く決める
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
  ].filter(Boolean);
}

function warmEffectValues() {
  return [
    currentEffectValue("暖色フレア"),
    currentEffectValue("光漏れ"),
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

  if (stateKey === "film") {
    if (hasTransparentStyleActive() && conflictFilms.includes(itemValue)) return true;
    if (hasCoolStyleActive() && warmFilms.includes(itemValue)) return true;
    if (hasWarmStyleActive() && itemValue === valueByLabel(FILM_TONES, "シネスコープ")) return true;
  }

  if (stateKey === "tone") {
    if (hasTransparentStyleActive() && (itemValue === streetToneValue() || itemValue === darkToneValue())) return true;
    if (hasGrittyStyleActive() && itemValue === transparentToneValue()) return true;
  }

  if (stateKey === "effects") {
    // 曇天・雨・霧では晴れっぽいキラキラ粒子を禁止
    if (isOvercastLikeWeatherActive() && itemValue === sparkleEffectValue()) return true;

    // 透明感スマホ系と粒状/暗め/フィルム荒れ系は競合
    if (hasTransparentStyleActive() && grittyEffects.includes(itemValue)) return true;
    if (hasGrittyStyleActive() && strongTransparent.includes(itemValue)) return true;
    if (state.film && conflictFilms.includes(state.film) && transparentEffects.includes(itemValue)) return true;

    // 暖色と冷色の強い同時選択は避ける
    if (hasWarmStyleActive() && coolEffects.includes(itemValue)) return true;
    if (hasCoolStyleActive() && warmEffects.includes(itemValue)) return true;

    // 白黒フィルム時は肌色演出系を避ける
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

  const transparentEffects = transparentEffectValues();
  const strongTransparent = strongTransparentEffectValues();
  const grainNoise = grainNoiseEffectValues();
  const grittyEffects = grittyEffectValues();
  const warmEffects = warmEffectValues();
  const coolEffects = coolEffectValues();
  const conflictFilms = transparentConflictFilmValues();
  const warmFilms = warmFilmValues();
  const monoFilms = monochromeFilmValues();

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
  renderChips("bustChips", BUST_OPTIONS, "bust");
  renderChips("hipChips", HIP_OPTIONS, "hip");
  renderChips("selfieModeChips", SELFIE_MODE_OPTIONS, "selfieMode");
  renderChips("weatherChips", WEATHER_OPTIONS, "weather");
  renderChips("filmChips", FILM_TONES, "film");
  renderChips("toneChips", OVERALL_TONES, "tone");
  renderMultiChips("effectChips", EFFECTS, "effects");
  renderChips("effectStrengthChips", EFFECT_STRENGTH_OPTIONS, "effectStrength");
  renderChips("angleModeChips", ANGLE_UI_OPTIONS, "angleMode");
  renderChips("subjectSizeChips", SUBJECT_SIZE_MODES, "subjectSize");
  renderChips("backgroundViewChips", BACKGROUND_VIEW_MODES, "backgroundView");
  renderChips("framingChips", FRAMING_MODES, "framing");
  renderChips("photoStyleChips", PHOTO_STYLE_MODES, "photoStyle");
  renderChips("tensionChips", TENSIONS, "tension");
  renderChips("emotionChips", EMOTIONS, "emotion");
  renderChips("expressionChips", EXPRESSION_OPTIONS, "expression");
}



// ── Tension options ────────────────────────────────────────────────────────────
const TENSIONS = [
  {label:"😌 低め（落ち着き）", value:"low"},
  {label:"🙂 普通",           value:"medium"},
  {label:"😄 やや高め",        value:"medium-high"},
  {label:"🤩 高め（元気）",    value:"high"},
];

// ── Emotion options ────────────────────────────────────────────────────────────
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

// ── Expression options (manual override for EXPRESSIONS random pick) ──────────
const EXPRESSION_OPTIONS = [
  {label:"😐 真顔/クール",      value:"neutral deadpan, calm, composed expression"},
  {label:"🙂 優しい微笑み",     value:"soft gentle smile, warm and approachable expression"},
  {label:"😊 口角を上げて笑う", value:"gently raised mouth corners, natural warm smile with lifted lips, soft genuine smile"},
  {label:"😄 明るい笑顔",       value:"bright happy, lively cheerful expression"},
  {label:"🥰 甘え/愛おしそう",  value:"sweet, slightly clingy, affectionate expression"},
  {label:"😋 いたずらっぽい笑み", value:"teasing, mischievous smirk expression"},
  {label:"😌 物憂げ",          value:"melancholic, reflective, subtle loneliness in expression"},
  {label:"😪 気だるげ",         value:"tired but gentle, quiet fatigue expression"},
  {label:"🍶 ほろ酔い",        value:"tipsy warm relaxed expression"},
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
  {label:"🫧 控えめ", value:"(subtle upper-body silhouette:1.55), (small gentle bust impression:1.55), (soft natural body line without strong projection:1.6), (outfit drapes naturally without obvious tension:1.65), (balanced face-first portrait:1.85)"},
  {label:"🌿 自然", value:"(natural balanced upper-body silhouette:1.65), (natural bust volume and body line:1.65), (realistic adult proportions without exaggeration:1.75), (outfit fit looks natural and believable:1.7), (balanced face and outfit portrait:1.85)"},
  {label:"⬆️ 立体感", value:"(clear natural forward volume in the upper body:1.82), (three-dimensional bust silhouette without exaggeration:1.82), (body does not look flat from front or side:1.8), (realistic mature proportions with natural softness:1.78), (face remains the main focal point:1.85)"},
  {label:"🧱 ラインくっきり", value:"(clearly readable upper-body outline through the outfit:1.82), (defined bust line and garment contour:1.82), (realistic fabric fit and gentle tension around the upper body:1.78), (clean silhouette edges without exaggeration:1.78), (face remains the main focal point:1.85)"},
  {label:"⬆️🧱 立体感＋ライン", value:"(clear natural forward volume in the upper body:1.85), (three-dimensional bust silhouette without exaggeration:1.85), (clearly readable upper-body outline through the outfit:1.85), (defined garment contour with realistic fabric fit:1.82), (body does not look flat from front or side:1.82), (natural mature proportions with soft realistic volume:1.8), (face remains the main focal point:1.85)"},
  {label:"👚 服装なり", value:"(upper-body silhouette follows the selected outfit naturally:1.78), (loose clothing hides the line, fitted clothing reveals it naturally:1.78), (fabric thickness, cut, and neckline decide how much shape is visible:1.75), (no forced silhouette beyond the outfit design:1.75), (balanced face and outfit portrait:1.85)"}
];

const HIP_OPTIONS = [
  {label:"🫧 控えめ", value:"(subtle lower-body silhouette:1.55), (compact hip line with minimal emphasis:1.6), (slim I-line body remains clean and narrow:1.75), (no strong rear volume:1.65), (realistic mature proportions without exaggeration:1.85)"},
  {label:"🌿 自然", value:"(natural balanced lower-body silhouette:1.65), (compact natural hip shape:1.65), (clean narrow waist-to-hip line:1.75), (slim I-line body with believable lower-body balance:1.8), (realistic mature proportions without exaggeration:1.85)"},
  {label:"🍑 小尻プリ", value:"(compact small hips with a gently rounded shape:1.85), (small but perky hip silhouette:1.88), (subtle rear volume with a natural lifted curve:1.82), (not wide hips, not flat hips:1.9), (slim I-line body remains narrow and elegant:1.85), (realistic mature proportions without exaggeration:1.88)"},
  {label:"🍑⬆️ 小尻アップ", value:"(compact small hips with a clearly lifted shape:1.88), (small but perky upward hip silhouette:1.9), (firm lifted rear curve without extra width:1.85), (high-set compact hip line:1.82), (not wide hips, not flat hips, not exaggerated:1.9), (slim I-line body remains narrow and elegant:1.85)"},
  {label:"👖 服装なり", value:"(lower-body silhouette follows the selected outfit naturally:1.78), (pants, skirt, swimsuit, or fabric cut decides how much hip line is visible:1.78), (no forced hip shape beyond the outfit design:1.75), (slim I-line body remains the base:1.8), (realistic mature proportions without exaggeration:1.85)"}
];

// ── State ─────────────────────────────────────────────────────────────────────
let state = {
  characterMode: "light",
  bust: "", hip: "", weather: "", film: "", tone: "",
  effects: [], effectStrength: "standard", selfieMode: "", angleMode: "", subjectSize: "", backgroundView: "", framing: "", photoStyle: "", tension: "", emotion: "", expression: "",
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


// ── Long-press chip help ──────────────────────────────────────────────────────
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

// ── Render chip groups ────────────────────────────────────────────────────────
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
    bindChipHelp(btn, item);
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
    el.appendChild(btn);
  });
}

// ── Resolve motion: manual selection takes priority over keyword detection ────
function resolveMotion(situation, dayMood, timeCtx, manualTension, manualEmotion, scene, angleName, subjectSizeKey, photoStyleKey) {
  const t = situation + " " + dayMood + " " + timeCtx.mood;

  // ── Detect emotion (fallback only) ──────────────────────────────────────────
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

  // ── Detect tension (fallback only) ──────────────────────────────────────────
  let tension = manualTension || "medium";
  if (!manualTension) {
    if (/深夜|ひとり|一人|孤独|静か|quiet|calm|家|自宅|部屋|眠/.test(t)) tension = "low";
    else if (/走|急|hurry|energetic|excited|興奮|はしゃ|元気|パーティ|踊/.test(t)) tension = "high";
    else if (/飲み|バー|居酒屋|友達|集まり|social|にぎや/.test(t)) tension = "medium-high";
  }

  // ── Base pose from composition ──────────────────────────────────────────────
  let compositionPose = "";
  if (subjectSizeKey === "face") {
    compositionPose = "face-forward flattering selfie pose, stable upper-body framing, clean head angle, shoulders controlled but natural";
  } else if (subjectSizeKey === "faceCloseup") {
    compositionPose = "close-up selfie pose, face fills most of the frame, eyes and skin texture emphasized, background secondary";
  } else if (subjectSizeKey === "upperBody") {
    compositionPose = "upper-body selfie pose, face, shirt, jacket line, and torso balance clearly readable, natural shoulder line";
  } else if (subjectSizeKey === "widerBody") {
    compositionPose = "wider-body selfie pose, more outfit and body line visible, posture designed so body silhouette and environment both read clearly";
  } else {
    compositionPose = "balanced selfie pose, face and outfit both visible, natural handheld posture, relaxed shoulder line";
  }

  let photoStylePose = "";
  if (photoStyleKey === "daily") {
    photoStylePose = "unforced everyday selfie feel, slight imperfection allowed, candid daily-life posture";
  } else if (photoStyleKey === "enhanced") {
    photoStylePose = "naturally flattering selfie pose, slightly polished but still believable";
  } else if (photoStyleKey === "model") {
    photoStylePose = "model-like pose control, deliberate shoulder line, subtle hip shift, polished self-presentation";
  } else if (photoStyleKey === "editorial") {
    photoStylePose = "editorial fashion posture, composed body line, more designed image presentation";
  } else if (photoStyleKey === "strong") {
    photoStylePose = "strongly directed pose, noticeably composed body angle, intentionally crafted presentation";
  }

  // ── Angle-specific body logic ───────────────────────────────────────────────
  let anglePose = "";
  const chinPose = "neutral chin position, chin not thrust forward, no jutting chin, no projected jaw, no raised chin, face kept level as much as the angle allows, neck relaxed and not stretched, mouth and jaw relaxed naturally, natural jaw posture";
  if (angleName === "SUPER HIGH ANGLE") {
    anglePose = "arm lifted high above head, smartphone high over her head looking almost straight down, bird's-eye selfie perspective, subject keeps a natural face angle without looking up excessively, eyes gently meet the lens without forcing an upward gaze, " + chinPose;
  } else if (angleName === "GOLDEN ANGLE") {
    anglePose = "camera slightly above eye level looking down, flattering three-quarter facial view, face kept relaxed and natural, eyes naturally meet the lens, no exaggerated upward face tilt, " + chinPose;
  } else if (angleName === "HIGH ANGLE") {
    anglePose = "camera clearly above eye level, relaxed high-angle selfie perspective, natural face angle, eyes looking naturally toward the lens without lifting the chin, " + chinPose;
  } else if (angleName === "EYE LEVEL") {
    anglePose = "camera at eye height, relaxed direct gaze, natural standing selfie posture, minimal perspective distortion, " + chinPose;
  } else if (angleName === "LOW ANGLE") {
    anglePose = "ordinary front low-angle selfie, phone slightly below chest level in front of the body, camera looking slightly upward from a lower front hand position, subtle upward perspective only, face looking naturally toward the lens without pushing the chin forward, not waist-side vertical upshot, " + chinPose;
  } else if (angleName === "HIDDEN WAIST-HELD SELFIE") {
    anglePose = "hidden waist-held selfie, phone held discreetly close to her waist or lower torso, close-body low handheld position, short lowered arm with elbow close to torso, no arm-length selfie pose, no long stretched arm selfie, camera is low but close to the body, lens angled only slightly upward and not vertical, natural low-angle selfie with subtle upward perspective only, not a dramatic upshot, not a vertical upshot, not near-vertical upward camera axis, not camera pointing straight upward, not phone extended far away, do not copy the Face Reference image camera angle, arm extension, chin posture, or composition, " + chinPose;
  } else if (angleName === "WAIST-SIDE VERTICAL UPSHOT") {
    anglePose = "legacy vertical upshot mode disabled for natural waist-held selfies, use hidden waist-held close-body phone logic instead, phone held close to lower torso, lens only slightly upward, not vertical, no strong waist-side upshot, " + chinPose;
  } else if (angleName === "SUPER LOW ANGLE") {
    anglePose = "phone held very low below the waist or near hip-to-thigh level, dramatic strong upward perspective, not overhead, not golden angle, not waist-side vertical upshot, torso and jacket line strongly emphasized, face looking naturally toward the lens without jutting the chin, " + chinPose;
  } else if (angleName === "DYNAMIC TILTED") {
    anglePose = "slightly diagonal handheld selfie, small body twist, natural off-center framing, candid snapshot motion, " + chinPose;
  } else if (angleName === "OVER SHOULDER") {
    anglePose = "shoulder turned toward camera, face looking back to the lens, candid over-shoulder body line, " + chinPose;
  } else if (angleName === "WALKING") {
    anglePose = "captured mid-step, one shoulder moving forward, hair and jacket subtly moving, natural walking selfie posture, " + chinPose;
  }

  // ── Scene-specific pose logic ───────────────────────────────────────────────
  let scenePose = "";
  if (scene === "home") {
    scenePose = "indoor relaxed posture, small breathing motion, casual hand placement";
  } else if (scene === "date") {
    scenePose = "soft feminine posture, slight head tilt, gentle shoulder angle";
  } else if (scene === "after work") {
    scenePose = "tired after-work posture, one shoulder slightly lowered, composed office-worker stance";
  } else if (scene === "night out") {
    scenePose = "looser social posture, playful shoulder angle, relaxed arm and wrist";
  } else {
    scenePose = "real street selfie posture, standing near the location, body kept naturally within the crowd and surroundings";
  }

  // ── Tension and emotional motion ────────────────────────────────────────────
  let motionBase = "";
  if (tension === "low") {
    motionBase = "minimal movement, slow blink, slight breathing motion, small head tilt";
  } else if (tension === "medium") {
    motionBase = "gentle lean, subtle arm shift, soft hair movement, natural handheld micro-shake";
  } else if (tension === "medium-high") {
    motionBase = "visible but realistic motion, light body turn, playful tilt, hair and jacket moving slightly";
  } else {
    motionBase = "energetic selfie motion, walking or turning, dynamic arm movement, lively body angle, hair swaying";
  }

  let emotionPose = "";
  if (emotion === "lonely" || emotion === "lonely" || emotion === "sad" || emotion === "tired") {
    emotionPose = "quiet eye mood, restrained mouth movement, still shoulders, subtle downward or distant gaze";
  } else if (emotion === "happy") {
    emotionPose = "steady gaze, lifted posture, subtle hip shift, controlled confident shoulders";
  } else if (emotion === "calm") {
    emotionPose = "relaxed shoulder, easy standing posture, natural small smile or neutral mouth";
  } else if (emotion === "tipsy" || emotion === "joyful") {
    emotionPose = "loose arm, playful tilt, relaxed posture, warm expressive eyes";
  } else {
    emotionPose = "neutral natural posture, readable but not exaggerated facial movement";
  }

  const poseText = [compositionPose, photoStylePose, anglePose, scenePose, emotionPose].filter(Boolean).join(", ");
  const motionText = [poseText, motionBase].filter(Boolean).join(", ");

  return { motionText, poseText, tension, emotion };
}

// ── Build prompt ──────────────────────────────────────────────────────────────
function buildPrompt(t, situation, characterLock, bustPrompt, hipPrompt, weatherVal, filmVal, toneVal, effectsArr, effectStrengthMode, subjectSizeMode, backgroundViewMode, framingMode, photoStyleMode, angle, expression, scene, accessories, motionText) {
  const overviewParts = [];
  overviewParts.push("current time: " + t.timeCtx.label + " (" + t.timeCtx.en + "), " + t.timeStr + " JST");
  overviewParts.push("day: " + t.day + " — " + DAY_MOOD[t.day]);
  if (weatherVal) overviewParts.push("weather: " + weatherVal);
  overviewParts.push("time-of-day mood: " + t.timeCtx.mood);
  if (filmVal) overviewParts.push(filmVal);
  if (toneVal) overviewParts.push(toneVal);
  effectsArr.forEach(fx => overviewParts.push(fx));

  const hasStyleSelection = !!filmVal || !!toneVal || effectsArr.length > 0;
  const stylePriorityInstruction = hasStyleSelection
    ? "(selected film tone, photo tone, and effects must be clearly visible at first glance:1.75)\n" + (effectStrengthMode?.value || "")
    : "";

  const rawSceneText = situation.trim() || "No scene details provided. Create a realistic everyday portrait scene.";
  const sceneText = sanitizeSceneForFaceReference(rawSceneText);
  const selfieMode = getSelfieMode(sceneText);
  const cameraModePrompt = getCameraModePrompt(selfieMode, angle.name);
  const isSwimwear = detectSwimwearScene(rawSceneText);
  const effectiveBustPrompt = bustPrompt;
  const effectiveHipPrompt = hipPrompt;
  const effectiveMotionText = angle.name === "HIDDEN WAIST-HELD SELFIE"
    ? motionText
        .replace(/natural handheld posture/g, "discreet close-body handheld posture")
        .replace(/energetic selfie motion/g, "subtle discreet selfie motion")
        .replace(/dynamic arm movement/g, "no dynamic arm extension")
        .replace(/lively body angle/g, "natural close-body angle")
        + ", bent elbow kept close to the body, phone hidden near waist, no visible extended forearm, no large foreground arm, no arm-length selfie perspective"
    : motionText;
  const fixedCharacter = characterLock.trim();
  const characterModeLabel = state.characterMode === "off" ? "OFF / face reference only" : state.characterMode === "full" ? "FULL / legacy fixed character" : "LIGHT / face reference + atmosphere";

  return `APP_VERSION: ${APP_VERSION}
ANGLE_ENGINE: chin-control + face-reference-role-control + hidden-waist-held-selfie
HAIR_ENGINE: monthly-hair-priority + no-reference-hairstyle-copy
TIME: ${t.day}, month ${t.month}, ${t.timeCtx.label} / ${t.timeCtx.en}, ${t.timeStr} JST

CHARACTER LOCK MODE:
${characterModeLabel}
${fixedCharacter || "(fixed character text disabled; use Face Reference image for identity and facial atmosphere:1.95)"}

IDENTITY / FACE REFERENCE:
(use the first attached image as face identity reference only:1.98),
(preserve the same adult face identity, facial proportions, skin tone, and overall facial atmosphere:1.98),
(refined Korean Asian fashion-model beauty, mature adult, not idol-cute:1.65),
(very fair translucent skin with real texture:1.85),
(slim elongated V-shaped lower face, narrow jawline, small pointed chin:1.82),
(large horizontally refined eyes, straight high nose bridge, minimal cheek volume:1.75),
(no different person:1.98), (no celebrity likeness:1.98), (no specific real person name:1.98)

FACE REFERENCE ROLE CONTROL:
(use Face Reference for face identity and facial atmosphere only, not pose/camera/hair:1.98),
(do not copy reference camera angle, selfie arm extension, chin posture, facial tilt, body pose, crop, framing, background, hair length, hairstyle, hair silhouette, parting, or hair volume shape:1.98),
(create a new pose, camera position, scene, outfit, and app-priority hairstyle from this prompt:1.95)

HAIR — APP MONTHLY PRIORITY:
${getMonthlyHairBlock(t.month)}

SAFETY / REALISM:
${isSwimwear ? "(safe non-sexual adult cute swimsuit portrait at a beach/pool/resort:1.95),\n(cute resort bikini swimsuit, opaque non-transparent fabric, not lingerie or underwear:1.95),\n(not sporty competition swimwear:1.9),\n(composition is face-and-resort-atmosphere first, not erotic or anatomy-focused:1.9),\n(natural adult body balance is preserved without anatomy emphasis:1.85)," : "(safe non-sexual adult fashion portrait:1.95),\n(opaque public-safe fashion clothing, no lingerie/underwear/pin-up/fetish styling:1.95),\n(composition is face-and-fashion first, not erotic or anatomy-focused:1.9),\n(natural adult body silhouette is preserved; do not flatten or reduce bust volume:1.85),"}
(photographic realism only:1.95), (real skin texture, realistic lighting and shadows:1.85),
(no anime, no illustration, no plastic skin, no waxy skin, no beauty filter:1.9)

SCENE:
${sceneText}
(scene text overrides default location, clothing, pose and action, but never overrides face-reference safety or app-priority hair rules:1.9)

CONTEXT / STYLE:
${overviewParts.join(", ")}
${stylePriorityInstruction}

ASPECT / ENVIRONMENT:
(aspect ratio 9:16:1.6), (vertical smartphone framing:1.6),
(real Japanese location, realistic crowd/posture/signage/ambient lighting:1.75)

CAMERA MODE:
${cameraModePrompt}

CAMERA POSITION / ANGLE — ${angle.name}:
${angle.prompt}

COMPOSITION:
${subjectSizeMode.value}
${backgroundViewMode.value ? backgroundViewMode.value + "\n" : ""}${framingMode.value}
${photoStyleMode.value}

EXPRESSION / MOOD:
(${expression}:1.9),
(${getEmotionExpressionCue(state.emotion || "neutral")}:1.9),
(context-driven natural micro-expression matching the situation, time, weather, and atmosphere:1.75),
(keep cheek volume restrained even when smiling:1.85)

POSE / MOTION:
(${effectiveMotionText}:1.7)

BODY / CLOTHING SILHOUETTE:
(realistic mature adult proportions, slim I-line body, narrow elegant body base, no exaggerated body proportions:1.85),

CHEST SILHOUETTE:
${effectiveBustPrompt},
(the selected chest silhouette option should be reflected clearly but naturally:1.85),

HIP / LOWER-BODY SILHOUETTE:
${effectiveHipPrompt},
(the selected hip silhouette option should be reflected clearly but naturally:1.85),

OVERALL BODY BALANCE:
(chest and hip silhouette settings should both be visible while keeping a slim I-line body:1.85),
(face remains primary focal point, while the selected outfit silhouette is preserved:1.9)

ACCESSORIES / HAIR / LIGHTING:
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
    // 水着語は一度だけ自然な表現へ寄せる。連続置換で「可愛い可愛い」にならないようにする。
    s = s
      .replace(/白いビキニ/g, "白い可愛いビキニ水着")
      .replace(/白い水着/g, "白い可愛い水着")
      .replace(/ビキニ(?!水着)/g, "ビキニ水着")
      .replace(/スイムウェア/g, "水着")
      .replace(/リラックスして座るで肘立て/g, "ビーチチェアかプールサイドでリラックスして座り、片肘を自然に支える")
      .replace(/肘立て/g, "片肘を自然に支える");

    // 重複ワードを軽く整理
    s = s
      .replace(/可愛い可愛い/g, "可愛い")
      .replace(/水着水着/g, "水着")
      .replace(/ビキニ水着水着/g, "ビキニ水着");

    if (/場所はおまかせ|場所おまかせ|おまかせ/.test(s) && !/ビーチ|海|プール|リゾート|pool|beach|resort/i.test(s)) {
      s += "\n場所は、自然なビーチ、プールサイド、またはリゾートの休憩スペース。街中や駅前ではない。";
    }
    s += "\n水着はスポーツ競泳用ではなく、可愛いリゾート向けのファッション水着。上品で明るい夏らしいデザイン。体型表現は選択された②胸シルエット設定をそのまま使い、服装別に別ルールへ切り替えない。";
  }

  // Face Reference使用時の安全変換は最小限にする。
  // 服装ジャンルを勝手にゴスロリへ寄せず、下着/性的に読まれやすい語だけを中立的な公共ファッション表現へ置換。
  const replacements = [
    [/コルセット付きのレースのブラジャーは小さめ/g, "黒いレース襟ブラウスとコルセット風の外着ベスト"],
    [/レースのブラジャーは小さめ/g, "黒いレース襟のファッションブラウス"],
    [/ブラジャー/g, "ファッションブラウス"],
    [/ブラ\b/g, "ファッションブラウス"],
    [/ランジェリー/g, "レース装飾のファッション服"],
    [/下着/g, "透けないファッションインナー"],
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
    // 水着シーンでは「水着」を下着へ誤変換しない。姿勢・危険語だけ最低限整理。
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
  // v3.35: old WAIST-SIDE VERTICAL UPSHOT is intentionally removed from the UI, and Face Reference hairstyle copy is suppressed by monthly hair control.
  // If an older session somehow keeps that value, redirect it to the natural hidden waist-held mode.
  if (state.angleMode === "WAIST-SIDE VERTICAL UPSHOT") {
    state.angleMode = "HIDDEN WAIST-HELD SELFIE";
  }
  return ANGLE_UI_OPTIONS.find(m => m.value === state.angleMode) || ANGLE_UI_OPTIONS[0];
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

function pickAngleForComposition(subjectSizeKey, photoStyleKey) {
  let weightedNames = [];

  // 自動選択は顎上げを避けるため、EYE LEVEL と HIDDEN WAIST-HELD SELFIE を優先。
  // HIGH / GOLDEN / SUPER HIGH は明示選択時には使えるが、自動では出現頻度を低くする。
  if (subjectSizeKey === "faceCloseup") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE"];
  } else if (subjectSizeKey === "face") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "WALKING"];
  } else if (subjectSizeKey === "upperBody") {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "LOW ANGLE", "WALKING", "DYNAMIC TILTED"];
  } else if (subjectSizeKey === "widerBody") {
    weightedNames = ["EYE LEVEL", "LOW ANGLE", "HIDDEN WAIST-HELD SELFIE", "WALKING", "DYNAMIC TILTED", "OVER SHOULDER"];
  } else {
    weightedNames = ["EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "LOW ANGLE", "WALKING", "DYNAMIC TILTED"];
  }

  if (photoStyleKey === "daily") {
    weightedNames.push("EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE", "WALKING");
  } else if (photoStyleKey === "enhanced") {
    weightedNames.push("EYE LEVEL", "EYE LEVEL", "HIDDEN WAIST-HELD SELFIE");
  } else if (photoStyleKey === "model") {
    weightedNames.push("EYE LEVEL", "LOW ANGLE", "DYNAMIC TILTED");
  } else if (photoStyleKey === "editorial") {
    weightedNames.push("EYE LEVEL", "LOW ANGLE", "OVER SHOULDER", "DYNAMIC TILTED");
  } else if (photoStyleKey === "strong") {
    weightedNames.push("LOW ANGLE", "HIDDEN WAIST-HELD SELFIE", "DYNAMIC TILTED");
  }

  const weightedPool = weightedNames
    .map(name => ANGLES.find(a => a.name === name))
    .filter(Boolean);

  return weightedPool[Math.floor(Math.random() * weightedPool.length)]
    || ANGLES[Math.floor(Math.random() * ANGLES.length)];
}

// ── Generate ──────────────────────────────────────────────────────────────────
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
  const angle = angleMode.key === "auto"
    ? pickAngleForComposition(subjectSizeMode.key, photoStyleMode.key)
    : (ANGLES.find(a => a.name === angleMode.key) || ANGLES[0]);
  const expression = state.expression || EXPRESSIONS[Math.floor(Math.random() * EXPRESSIONS.length)];

  const motionResult = resolveMotion(situation, DAY_MOOD[t.day], t.timeCtx, state.tension, state.emotion, scene, angle.name, subjectSizeMode.key, photoStyleMode.key);
  const motionText = motionResult.motionText;
  const bustPrompt = state.bust || BUST_OPTIONS[4].value;
  const hipPrompt = state.hip || HIP_OPTIONS[2].value;

  const prompt = buildPrompt(t, situation, characterLock, bustPrompt, hipPrompt, state.weather, state.film, state.tone, state.effects, effectStrengthMode, subjectSizeMode, backgroundViewMode, framingMode, photoStyleMode, angle, expression, scene, accessories, motionText);

  // Show meta
  document.getElementById("metaCard").classList.remove("hidden");
  const selectedWeatherLabel = getLabelByValue(WEATHER_OPTIONS, state.weather);
  const selectedFilmLabel = getLabelByValue(FILM_TONES, state.film);
  const selectedToneLabel = getLabelByValue(OVERALL_TONES, state.tone);
  const selectedEffectLabels = getEffectLabels(state.effects);
  const selectedEffectStrengthLabel = getEffectStrengthMode().label;
  const selectedAngleModeLabel = getAngleMode().label;
  const selectedSubjectSizeLabel = getSubjectSizeMode().label;
  const selectedBackgroundViewLabel = getBackgroundViewMode().label;
  const selectedFramingLabel = getFramingMode().label;
  const selectedPhotoStyleLabel = getPhotoStyleMode().label;
  const selectedBustLabel = (BUST_OPTIONS.find(b => b.value === (state.bust || BUST_OPTIONS[4].value))?.label || "⬆️🧱 立体感＋ライン");
  const selectedHipLabel = (HIP_OPTIONS.find(h => h.value === (state.hip || HIP_OPTIONS[2].value))?.label || "🍑 小尻プリ");
  const effectWarning = getEffectWarning(state.effects);
  const transparentPresetHint = getTransparentSmartphonePresetHint(state.effects);
  const compatibilityHint = getCompatibilityHint();

  document.getElementById("metaContent").innerHTML =
    "🧩 <b style='color:#c4b5fd'>App</b>：" + APP_VERSION + "<br>" +
    "🕐 <b style='color:#c4b5fd'>時間帯</b>：" + t.timeCtx.label + " / " + t.timeCtx.en + "<br>" +
    "🔒 <b style='color:#c4b5fd'>固定キャラモード</b>：" + getLabelByValue(CHARACTER_MODE_OPTIONS, state.characterMode) + "<br>" +
    "📅 <b style='color:#c4b5fd'>曜日 mood</b>：" + DAY_MOOD[t.day] + "<br>" +
    "☀️ <b style='color:#c4b5fd'>天気</b>：" + selectedWeatherLabel + "<br>" +
    "🎞️ <b style='color:#c4b5fd'>フィルムトーン</b>：" + selectedFilmLabel + "<br>" +
    "🎨 <b style='color:#c4b5fd'>写真/作品トーン</b>：" + selectedToneLabel + "<br>" +
    "✨ <b style='color:#c4b5fd'>エフェクト</b>：" + selectedEffectLabels + "<br>" +
    "🌟 <b style='color:#c4b5fd'>エフェクト強度</b>：" + selectedEffectStrengthLabel + "<br>" +
    "📸 <b style='color:#c4b5fd'>カメラ位置/アングル</b>：" + selectedAngleModeLabel + " → " + angle.name + "<br>" +
    "🧍 <b style='color:#c4b5fd'>構図/被写体サイズ</b>：" + selectedSubjectSizeLabel + "<br>" +
    "🌆 <b style='color:#c4b5fd'>背景の見せ方</b>：" + selectedBackgroundViewLabel + "<br>" +
    "🖼️ <b style='color:#c4b5fd'>余白/リーディングスペース</b>：" + selectedFramingLabel + "<br>" +
    "🎭 <b style='color:#c4b5fd'>写真の自然さ/演出度</b>：" + selectedPhotoStyleLabel + "<br>" +
    "✂️ <b style='color:#c4b5fd'>ヘア</b>：" + HAIR_BY_MONTH[t.month] + "<br>" +
    "😊 <b style='color:#c4b5fd'>表情</b>：" + expression + "<br>" +
    "👜 <b style='color:#c4b5fd'>アクセ</b>：" + scene + "<br>" +
    "🎯 <b style='color:#c4b5fd'>テンション（動き）</b>：" + motionResult.tension + "<br>" +
    "💭 <b style='color:#c4b5fd'>感情（気分）</b>：" + motionResult.emotion + "<br>" +
    "🧍 <b style='color:#c4b5fd'>ポーズ/モーション</b>：" + motionText + "<br>" +
    "👚 <b style='color:#c4b5fd'>胸シルエット</b>：" + selectedBustLabel + "<br>" +
    "🍑 <b style='color:#c4b5fd'>ヒップ/下半身</b>：" + selectedHipLabel + "<br>" +
    "🖼️ <b style='color:#c4b5fd'>Face Reference</b>：チャット冒頭の最初の添付画像<br>" +
    "📷 <b style='color:#c4b5fd'>撮影モード</b>：" + getSelfieModeLabel(getSelfieMode(document.getElementById("situation").value || "")) + "<br>" +
    "🔒 <b style='color:#c4b5fd'>Face Reference安全ロック</b>：ON<br>" +
    (detectFaceReferenceSensitiveScene(document.getElementById("situation").value || "") ? "🧹 <b style='color:#c4b5fd'>危険語サニタイズ</b>：ON<br>" : "") +
    "🧍 <b style='color:#c4b5fd'>体型/胸シルエット</b>：" + selectedBustLabel +
    transparentPresetHint +
    compatibilityHint +
    effectWarning;

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

// ── Character Lock Reset ─────────────────────────────────────────────────────
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

// ── Reset ─────────────────────────────────────────────────────────────────────
function handleReset() {
  document.getElementById("situation").value = "";
  state = { characterMode:"light", bust:"", hip:"", weather:"", film:"", tone:"", effects:[], effectStrength:"standard", selfieMode:SELFIE_MODE_OPTIONS[0].value, angleMode:ANGLE_UI_OPTIONS[0].value, subjectSize:SUBJECT_SIZE_MODES[0].value, backgroundView:BACKGROUND_VIEW_MODES[0].value, framing:FRAMING_MODES[0].value, photoStyle:PHOTO_STYLE_MODES[0].value, tension:"", emotion:"", expression:"" };
  document.getElementById("metaCard").classList.add("hidden");
  document.getElementById("outputCard").classList.add("hidden");
  document.getElementById("outputArea").value = "";
  renderChips("bustChips", BUST_OPTIONS, "bust");
  renderChips("weatherChips", WEATHER_OPTIONS, "weather");
  renderChips("filmChips", FILM_TONES, "film");
  renderChips("toneChips", OVERALL_TONES, "tone");
  renderMultiChips("effectChips", EFFECTS, "effects");
  renderChips("effectStrengthChips", EFFECT_STRENGTH_OPTIONS, "effectStrength");
  renderChips("angleModeChips", ANGLE_UI_OPTIONS, "angleMode");
  renderChips("subjectSizeChips", SUBJECT_SIZE_MODES, "subjectSize");
  renderChips("backgroundViewChips", BACKGROUND_VIEW_MODES, "backgroundView");
  renderChips("framingChips", FRAMING_MODES, "framing");
  renderChips("photoStyleChips", PHOTO_STYLE_MODES, "photoStyle");
  renderChips("tensionChips", TENSIONS, "tension");
  renderChips("emotionChips", EMOTIONS, "emotion");
  renderChips("expressionChips", EXPRESSION_OPTIONS, "expression");
}

// ── Init ──────────────────────────────────────────────────────────────────────
document.addEventListener("DOMContentLoaded", () => {
  const characterLockEl = document.getElementById("characterLock");
  state.characterMode = "light";
  if (characterLockEl) characterLockEl.value = LIGHT_CHARACTER_LOCK;
  state.selfieMode = SELFIE_MODE_OPTIONS[0].value;
  state.angleMode = ANGLE_UI_OPTIONS[0].value;
  state.subjectSize = SUBJECT_SIZE_MODES[0].value;
  state.framing = FRAMING_MODES[0].value;
  state.photoStyle = PHOTO_STYLE_MODES[0].value;
  updateClock();
  setInterval(updateClock, 30000);
  renderAllOptionChips();
});
</script>
</body>
</html>
