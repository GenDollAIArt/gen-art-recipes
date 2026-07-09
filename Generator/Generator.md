<!--
  Selfie Prompt Generator
  Version: 4.0.3-more-effects
  Updated: 2026-07-09
  Changelog:
    v4.0.6 - 背中から/斜め後ろ/肩越し後ろ/窓際後ろ姿を追加。自撮りOFF専用アングルガード、逆光布の安全ガード、顔アップ時の体型ブロック弱化、角度メタ情報のリファクタリングを実装
    v4.0.5 - 真横から/寝転び横、顔アップ/顔どアップを追加
    v4.0.4 - 肌の見え方/肌質感を追加
    v4.0.3 - エフェクトを追加。ネオン反射、ガラス反射、夕方斜光、モーションブラー、コンデジ感、低彩度を追加し、既存の相反ガードへ必要分を統合
    v4.0.1 - エフェクト強度を補助プロンプト追加方式から、選択エフェクト内weightの倍率補正方式へ変更。強度チップの選択状態もkey/value整合に修正
    v4.0.2 - エフェクト相反ガードを追加。直フラッシュ/白飛びフラッシュと背景ボケ・光の玉ボケ・自然光/逆光系などを同時選択不可にし、硬い影と低コントラスト影/ソフトフォーカスの競合も整理
    v4.0.1 - エフェクト強度を補助文追加方式から、選択エフェクト内のweight数値を倍率補正する方式へ変更
    v4.0.0 - メジャーアップデート。フィルムトーンに「ガサつき」、エフェクトに「直フラッシュ」「硬い影」「白飛びフラッシュ」を追加。エフェクト長押しヘルプ対応を維持し、フラッシュ系の質感を個別に選べるように整理
    v3.61.0 - ②を「逆光時の布の見え方」に変更。服素材分類を削除し、長押しヘルプ表示も全削除
    v3.60.0 - ②服の質感 / 素材感を追加。通常生地・薄手ニット・リブ編み・やわ布・とろみ/サテン・光を通す薄布を選択可能に変更
    v3.59.0 - 起動しない問題を修正。長押しヘルプ文字列内の改行をJS安全形式へ変換
    v3.58.0 - 生成後に自動でクリップボードへコピーする機能を追加。Androidで失敗した場合は手動コピーへフォールバック
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
    v3.46.0 - ③ 胸シルエット に「立体感＋ライン」を追加。名称も 立体感 / ラインくっきり に整理し、単一選択のまま使いやすく調整
    v3.45.0 - ③ 胸シルエット選択の名称と並び順を整理。控えめ/自然/前に出る/形くっきり/服装なり に変更し、選択結果が分かりやすい文言へ調整
    v3.44.0 - ⑬ 背景の見せ方 を追加。指定なし / 控えめ / バランス / 足元 / 奥 / 上 の選択肢を実装し、プロンプトとサマリーに反映
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
    <div class="header-sub">固定キャラ + 今回のシーン v4.0.6</div>
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

  <!-- Garment backlight response -->
  <div class="card">
    <div class="slabel">② 逆光時の布の見え方</div>
    <div class="hint">服の素材分類ではなく、逆光で布が光を通す・ふんわり見えるかだけを選びます。ニット/リブ編み/サイズ感は①シーン本文に書く運用です。</div>
    <div class="chips" id="garmentLightChips"></div>
  </div>

  <!-- Chest silhouette -->
  <div class="card">
    <div class="slabel">③ 胸シルエット</div>
    <div class="hint">選択した内容をそのままプロンプトに反映します。立体感（前後の厚み）とライン（輪郭）の出方を素直に変えます。</div>
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

  <!-- Selfie mode -->
  <div class="card">
    <div class="slabel">⑪ 自撮り / 第三者撮影</div>
    <div class="hint">自撮りONならスマホ手持ちカメラ視点。OFFなら他人が撮った自然なポートレート/スナップ扱い。自動は「他撮り・非自撮り」などがシーンにあればOFF、それ以外はON寄りです。</div>
    <div class="chips" id="selfieModeChips"></div>
  </div>

  <!-- Camera angle -->
  <div class="card">
    <div class="slabel">⑫ カメラ位置 / アングル</div>
    <div class="hint">撮影の高さ・持ち方・向きを選びます。</div>
    <div class="chips" id="angleModeChips"></div>
  </div>

  <!-- Subject framing / composition -->
  <div class="card">
    <div class="slabel">⑬ 構図 / 被写体サイズ</div>
    <div class="hint">顔中心か、上半身か、服や体も含めて広めに見せるかを選びます</div>
    <div class="chips" id="subjectSizeChips"></div>
  </div>

  <!-- Background view -->
  <div class="card">
    <div class="slabel">⑭ 背景の見せ方</div>
    <div class="hint">背景をどの方向で見せるかを選びます</div>
    <div class="chips" id="backgroundViewChips"></div>
  </div>

  <!-- Framing space -->
  <div class="card">
    <div class="slabel">⑮ 余白 / リーディングスペース</div>
    <div class="hint">被写体を画像いっぱいにするか、少し余白を残すか、場所を見せるかを選択します。ソファに寝転がる・椅子に座る等では「余白なし / 被写体いっぱい」が使いやすいです</div>
    <div class="chips" id="framingChips"></div>
  </div>

  <!-- Photo naturalness / staging -->
  <div class="card">
    <div class="slabel">⑯ 写真の自然さ / 演出度</div>
    <div class="hint">日常セルフィー寄りか、少し盛るか、モデル風か、ファッション誌風かを選びます</div>
    <div class="chips" id="photoStyleChips"></div>
  </div>

  <!-- Tension -->
  <div class="card">
    <div class="slabel">⑰ テンション（動きの強さ）</div>
    <div class="hint">体の動きの強さや静止感を調整します</div>
    <div class="chips" id="tensionChips"></div>
  </div>

  <!-- Emotion -->
  <div class="card">
    <div class="slabel">⑱ 感情（内面の気分）</div>
    <div class="hint">気分や心理状態を選びます。ポーズと表情の補助に使います</div>
    <div class="chips" id="emotionChips"></div>
  </div>

  <!-- Expression -->
  <div class="card">
    <div class="slabel">⑲ 表情（顔の出力）</div>
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

<script>
// ── Data ─────────────────────────────────────────────────────────────────────
const HAIR_BY_MONTH = {
  1:"(long straight, dark brown hair:1.65), (hair falls below the shoulders:1.55)",
  2:"(long wave, dark brown to chestnut brown gradient hair:1.65), (hair falls below the shoulders:1.55)",
  3:"(long soft wave, chestnut brown hair:1.65), (hair falls below the shoulders:1.55)",
  4:"(medium straight, chestnut brown
