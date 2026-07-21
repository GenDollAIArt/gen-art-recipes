<!--
  Selfie Prompt Generator
  Version: 9.1.3
  Updated: 2026-07-22
  Changelog:
    v9.1.3 - 被写体身体形態の参照読取を全面強化。身体ラインが明確なA4〜A9を補正推測せず直接・忠実に読み、A4〜A6を上半身、A7〜A9を全身の主参照として正面・45度・真横の役割を明文化。バスト、ウエスト、骨盤・ヒップ、四肢、全身比率を独立した固定対象として追加し、バスト→ウエスト→骨盤・ヒップ→太腿を一続きの三次元構造として保持。選択アングルの方向に近い参照を主にし、他方向を幅・奥行き・位置関係の確認に使う方向別参照を追加。Image Bのモデル・マネキン・商品シルエットから身体を再定義しない分離を強化し、357系遠近は固定身体への投影として扱う。末尾にA4〜A9基準の最終身体形態検証を追加。その他の顔ID、月別ヘア、撮影腕・手役割、服装・場所参照、構図、エフェクトは維持。
    v9.1.2 - 自撮り時の手の役割と357系身体沿いアングルの優先順位を再整理。撮影スマートフォンを撮影手が持つ唯一の端末として固定し、端末自体はそのレンズから生成される画面内へ写さない。反対側の手によるスマートフォン・第2端末・リモコン保持を禁止し、空いている手はシーン上の身体支持または非スマートフォン小物を優先し、それ以外は「身体の動き / 躍動感」へ連動。身体沿い自撮りでは撮影腕を腹部・腰・ヒップ・脇腹の選択ラインへ密着させ、腕をレンズ前へ突き出す通常セルフィー化、大きな前景腕、中央を横切る腕を禁止。生成順をカメラ方式→完成アングル→手役割→躍動感へ変更し、最終手役割検証を追加。その他の参照、月別ヘア、服装・場所参照、構図、エフェクトは維持。
    v9.1.1 - アングル選択時は選択したアングルが属する分類だけを開いた状態で残し、他のアングル分類を自動で閉じるよう変更。被写体設定のOFFを「参照なし」へ整理し、OFF時の被写体テキスト入力欄・初期化ボタン・テキスト由来の被写体定義を削除。ON時のA1〜A9参照、顔ID・体型の役割分離、月別ヘア、服装・場所参照、357系angle-core、シーン連動、エフェクト定義は維持。
    v9.1.0 - 357系angle-coreの全アングル定義を再整理。各選択肢を完成済み撮影形として、カメラ位置・被写体との距離・方向・光軸・遠近感の順に統一し、写す範囲・背景・余白・画面傾きが選択アングルを別構図へ変えない共通ロックを追加。腰位置／腰下の身体沿いアングルには、身体との近接距離、前景となる腹部・腰・脇腹、胴体から顔へ続くライン、自撮り腕または第三者カメラ位置を固定する専用ロックを追加。覗き込み3種では角度専用の顔向き・視線を実際の出力へ適用。UIはアングルを7系統の折りたたみ分類へ再編。追加要素／空間演出は全項目を維持したまま8系統の折りたたみ分類へ分け、生成プロンプトの実行計画も同じ分類へ統一。被写体・顔ID・月別ヘア・服装・場所参照・シーン連動・エフェクト定義は維持。
    v9.0.11 - 「表現の主役」で被写体＋飲み物／被写体＋食べ物／被写体＋テーブル上を選択した場合、⑮「背景の見せ方」を指定なしへ自動固定し、控えめ・バランス・下／足元側・奥・上を選択不可に変更。テーブル上の前景〜中景は表現の主役側だけで制御し、背景指定との重複を防止。その他の顔ID、月別ヘア、357系アングル、撮影腕ロック、シーン連動、エフェクトは維持。
    v9.0.10 - 顔ID参照の役割を再整理。A1を顔の唯一の主参照、A2〜A3を同一人物の角度確認専用、A4〜A9を身体形態専用として明示し、A4〜A9の顔情報による平均化・再設計を禁止。顔のみ／顔どアップ／顔アップ／横顔アップでは、背景・服・場所・テーブル上などの構図優先を自動抑制し、顔クロップを唯一の構図主役として出力。プロンプト末尾にA1基準の最終顔ID検証を追加。月別ヘア、357系アングル、撮影腕ロック、シーン連動、エフェクトは維持。
    v9.0.7 - v9.0.6の月別ヘアを表示だけでなく生成時にも厳格適用するよう強化。月別ヘアを髪に関する唯一の指定元として明示し、A1〜A9・Image B・シーンから髪の長さ、カット、色、シルエット、結び方を継承・混合しないロックを追加。各月ごとに長さ境界を明文化し、6〜8月のボブでは肩・胸・背中・枕まで伸びる長髪、ポニーテール、編み込み、まとめ髪を禁止。その他のUI、角度、シーン連動、被写体・服装・場所参照、エフェクトは変更なし。
    v9.0.6 - v9.0.5をベースに「シーン連動チェック」を追加。シーン文・撮影方式・写す範囲との成立条件が不足する選択肢をグレー表示で選択不可にし、選択後に条件が失われた場合は赤色の不整合表示として生成を停止する。カメラ位置 / アングルへ「地面付近・前脚→顔ライン自撮り」を追加し、シーン文に低い姿勢と前景脚の記述、写す範囲に全身、自撮り条件がそろった場合のみ使用可能にした。テーブル / カウンター肘つき前傾、振り向き、歩き、被写体＋飲み物 / 食べ物 / テーブル上、自然 / 強い躍動感にも明確なシーン成立条件を追加。被写体・服装・場所参照、月別ヘア、既存エフェクト定義は変更なし。
    v9.0.5 - v9.0.4の月別ヘア表示不具合を修正。東京時間カードに「今月のヘアスタイル」を日本語で明示し、現在月・髪型・色・長さを確認できる表示へ変更。生成プロンプトのHAIRブロックに文字列として混入していたバックスラッシュ付きnを正しい改行へ修正。月別ヘアの内部プロンプト、A1〜A9より月別ヘアを優先するルール、その他の機能・選択肢は変更なし。
    v9.0.4 - v9.0.3をベースに分類重複を整理。独立した「基本姿勢」をUI・状態・生成ブロックから削除し、立つ・座る・横になる・前傾・身体の支えはシーン文を唯一の指定元として扱う物理整合ルールをSCENEへ自動追加。既存の「テンション（動きの強さ）」を「身体の動き / 躍動感」へ置換し、おまかせ・わずかな自然な動き・自然な躍動感・強い躍動感の4段階へ整理。「表現の主役」へ被写体＋飲み物・被写体＋食べ物・被写体＋テーブル上を追加し、シーンに存在しない物を勝手に追加しない構図ルールを付与。v3.57系angle-core、6種類の腰下超強煽り、被写体・服装・場所参照、表情、既存エフェクトは変更なし。
    v9.0.3 - v9.0.2をベースに、腰下・体沿い超強煽りをv3.57系の完成済みアングルとして6種類へ再整理。正面沿い・斜め沿い・真横沿いの通常版3種と、各方向で低いカメラを覗き込む版3種を追加。覗き込み版では、低いレンズを見下ろす顔向き・視線・自然な顎引きを角度プリセット側で固定し、胴体方向は各方向を維持。その他の機能・参照・分類は変更なし。
    v9.0.2 - v9.0.1をベースに、テーブル / カウンター系の肘つき前傾アングルを「片肘つき」と「両肘つき」に分離。自撮り時は両肘つき前傾を選択不可にし、第三者撮影時のみ選択可能に調整。自撮りのときに両肘つきという物理的に不自然な状態を避けつつ、従来のv3.57系angle-core構造・被写体参照・服装参照・場所参照・既存分類は維持。
    v9.0.0 - v8.0.34のangle-core / v3.57系思想を維持した正式再編版。「写真の自然さ / 演出度」を「写真の作り込み度」へ改称し、「撮影スタイル / 表現方向」を「表現の主役（人物・服・背景・バランス）」へ置換。被写体サイズ / 余白にAUTO（表現の主役に連動）を追加。カメラ位置 / アングルは完成済みプリセット方式を維持し、「腰下・体沿い超強煽り」の正面・斜め・真横を追加。撮影プリセットは自撮り／第三者撮影を自動反映し、適用後の個別変更も可能。シーン・人数・場所・被写体参照・体型ロック・服装参照・場所参照・既存エフェクト定義は変更なし。
    v8.0.29 - カメラ位置 / アングルを高い位置から低い位置の順へ並べ替え。写真の自然さ / 演出度に「素人スナップ」を追加。設定保存をIndexedDB + localStorage + OPFSの多重保存へ変更し、設定ファイルの手動書出・読込も追加。
    v8.0.29 - v8.0.26を完全土台として維持。すべての選択項目を一行1項目の縦並びへ変更。固定px文字サイズをrem基準へ置換し、OS／ブラウザのシステム文字サイズとテキスト拡大設定に追従。ピンチズーム制限も解除。生成ロジック・選択肢・相性ガードは変更なし。
    v8.0.26 - v8.0.25を完全土台として維持し、弱体化や矛盾を招くエフェクト同時選択をUIで禁止。背景ボケ/光の玉ボケ、通常前ボケ/強い前ボケ/手前の手ボケ、ソフトフォーカス/モーションブラー、複数の主影表現などを相互排他化。高精細クローズアップとのぼかし競合、天気と直射日光・雨粒・雪・熱気・乾いたダストの矛盾も選択不可に変更。
    v8.0.25 - v8.0.24を土台に、ポリシー誤判定を招きやすい上半身・細身比較表現を削除。Aと服の分離は維持し、服のシルエットやゆとりを被写体変更の根拠にしない中立的なSUBJECT / GARMENT CONSISTENCYへ変更。その他の機能・選択肢・ロジックは維持。
    v8.0.24 - v8.0.23を完全土台として維持し、Aの身体にBの服を着せるルールを明示。Image Bの服シルエットから被写体の体型を再推定・再定義しない一文へ差し替え。その他の機能・選択肢・構成は変更しない。
    v8.0.23 - v8.0.22を土台に、上半身比率ブロックを一般化してポリシー誤判定を抑制。bust-to-torso / upper-body volume / flatter等の具体語を削除し、A4〜A9から自然な全体比率を維持するBODY PROPORTION CONSISTENCYへ変更。Image Bに関する体型再定義禁止文はImage B参照ON時だけ出力するよう条件分岐。
    v8.0.22 - v8.0.21を土台に、A1〜A9の担当を顔・上半身・全身へ明確分離。A4〜A6を上半身比率の主参照、A7〜A9を全身整合確認として扱う短いUPPER-BODY REFERENCE CONSISTENCYを追加。サイズ表現やweight増加は行わず、Image Bが体型を再定義しないことを明示。
    v8.0.21 - v8.0.19を土台に、フィルムトーンへ「サンフェード・ミルキーフィルム」を追加。エフェクトの「低彩度」をUI・相性ガード・実行計画から完全削除し、彩度表現をフィルムトーン側へ統合。
    v8.0.19 - 「追加要素 / 空間演出（複数選択可）」を新設。光線、光芒、浮遊粒子、霧・煙、投影影、季節要素、前景要素など46項目をカテゴリ順に追加し、全項目に長押しヘルプを実装。エフェクトとは別の物理的なシーン要素として生成プロンプトへ展開。
    v8.0.18 - 感情（内面の気分）を削除し、表情をカテゴリ順に拡充・整理。エフェクトを写真処理順に整列し、weightを上げずに適用構造を明確化。画面の傾きを背景の水平線・垂直線と角度で明示して実効性を改善。
    v8.0.17 - v8.0.16を完全土台として維持。プロジェクト情報源運用に合わせ、参照画像ブロックを固定ファイル名ベースへ更新。A1〜A9 / Image B の実ファイル名を明記し、プロジェクト情報源がある場合は再アップロード不要で解釈するよう修正。
    v8.0.15 - 服の胸まわり／ヒップ・下半身シルエット機能をUI・状態・生成プロンプトから完全に削除。以降の項目番号を繰り上げ。
    v8.0.14 - 被写体9枚参照の全文プロンプトを簡潔化。顔・体型ロック、コーデ参照、安全文、服シルエット文を整理し、誤判定されにくい構成へ調整。
    v8.0.12 - フィルムトーン×エフェクト、エフェクト同士の相性ガードを追加。相性の悪い項目は選択不可になり、フィルム変更時の競合エフェクトは自動解除。
    v8.0.11 - 腰横専用モードからSELFIEの反復を減らし、本人操作の低位置カメラとして再定義。腕を前へ突き出さず、腰位置から体に沿って顔へ煽る指定へ差し替え。
    v8.0.10 - 「腰横から強い煽り」を専用の腰横密着セルフィーモードへ差し替え。通常の腕伸ばし自撮りへ寄りにくく調整。
    v8.0.9 - 1枚目ON時の顔ロックと体型ロックを強化。カメラ位置 / アングルに「腰横から強い煽り」を追加。
    v8.0.8 - 1枚目/2枚目参照をON/OFFの2択へ整理。1枚目ONは顔＋全身体型（胸・ヒップの形の印象、四肢比率を含む）を参照。OFFはテキスト入力のみ。2枚目OFFはコーデおまかせ、ONはFULL厳格参照。胸・ヒップのシルエット指定を服の見え方専用へ分離。v3.57角度コアとweight無加工思想は維持。
    v8.0.7 - エフェクトに「光と影を強調」「キアロスクーロ」「スプリットライト」「木漏れ日シャドウ」を追加。
    v8.0.6 - 顔の出力に笑顔系バリエーションを追加。「手前の手ボケ」「強い前ボケ」エフェクトを追加。既存の「熱気 / ヒートヘイズ」も維持。
    v8.0.5 - 顔の出力に半目クール、アンニュイ、少し不機嫌、無機質な視線を追加。
    v8.0.4 - エフェクトに「硬い直射日光」「鋭い影」などの質感系エフェクトを追加。
    v8.0.3 - 写す範囲を厳格化。自撮りON時の第三者撮影への逃げを防止。
    v8.0.2 - エフェクト強度の「強め」「盛り盛り」を強化。カメラ位置に「頭の真上から」を追加。
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
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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
  html{font-size:87.5%;-webkit-text-size-adjust:100%;text-size-adjust:100%}
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,BlinkMacSystemFont,'Hiragino Kaku Gothic ProN','Noto Sans JP',sans-serif;padding-bottom:80px;font-size:1rem}
  .header{background:var(--hdr-bg);border-bottom:1px solid var(--border);padding:16px 14px 12px;position:sticky;top:0;z-index:10;display:flex;align-items:center;gap:10px}
  .header-icon{width:30px;height:30px;border-radius:8px;background:linear-gradient(135deg,#7c3aed,#a855f7);display:flex;align-items:center;justify-content:center;font-size:1.071rem;flex-shrink:0}
  .header-title{font-size:1.071rem;font-weight:700}.header-sub{font-size:.714rem;color:var(--text-hint);margin-top:1px}.header-time{margin-left:auto;text-align:right}.header-time-main{font-size:.929rem;color:#a855f7;font-weight:700}.header-time-sub{font-size:.714rem;color:var(--text-hint)}
  .content{padding:12px 14px 0}.card{background:var(--bg-card);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:10px}.card-dark{background:var(--bg-dark);border-color:var(--border-pu)}.card-out{background:var(--bg-out);border-color:var(--border-pu)}
  .slabel{font-size:.714rem;font-weight:700;letter-spacing:.12em;color:var(--text-dim);text-transform:uppercase;margin-bottom:8px}.hint{font-size:.786rem;color:var(--text-hint);margin-bottom:8px;line-height:1.55}
  .chips{display:flex;flex-direction:column;align-items:stretch;gap:8px}.chip{width:100%;padding:9px 13px;border-radius:12px;text-align:left;border:2px solid var(--border-m);background:var(--chip-bg);color:var(--chip-col);font-size:.857rem;cursor:pointer;transition:all .15s;-webkit-tap-highlight-color:transparent;user-select:none}.chip.active{border-color:var(--chip-abdr);background:var(--chip-abg);color:var(--chip-acol);font-weight:600}.chip.disabled{opacity:.35;cursor:not-allowed;filter:grayscale(.6)}.chip.invalid{border-color:#dc2626;background:#fef2f2;color:#b91c1c;font-weight:700}.chip.has-help::after{content:"？";display:inline-flex;align-items:center;justify-content:center;width:15px;height:15px;margin-left:5px;border-radius:999px;font-size:.714rem;color:#c4b5fd;background:rgba(168,85,247,.18);border:1px solid rgba(196,181,253,.35)}
  .option-groups{display:flex;flex-direction:column;gap:8px}.option-group{border:1px solid var(--border);border-radius:12px;background:#fafafa;overflow:hidden}.option-group[open]{border-color:#ddd6fe;background:#fdfcff}.option-group-summary{list-style:none;display:flex;align-items:center;gap:8px;padding:10px 12px;cursor:pointer;user-select:none;color:var(--text-sub);font-size:.857rem;font-weight:700}.option-group-summary::-webkit-details-marker{display:none}.option-group-summary::before{content:"＋";display:inline-flex;align-items:center;justify-content:center;width:18px;height:18px;border-radius:999px;background:#ede9fe;color:#7c3aed;font-size:.786rem;flex-shrink:0}.option-group[open]>.option-group-summary::before{content:"−"}.option-group-title{flex:1}.option-group-count{font-size:.714rem;color:#7c3aed;background:#ede9fe;border-radius:999px;padding:2px 7px;font-weight:700}.option-group-note{font-size:.714rem;color:var(--text-hint);line-height:1.5;padding:0 12px 8px}.option-group-body{padding:0 8px 8px}.option-group-body .chips{gap:7px}
  textarea{width:100%;background:var(--bg-input);border:1px solid var(--border-m);border-radius:10px;color:var(--text);font-size:1rem;line-height:1.6;padding:10px 12px;resize:vertical;outline:none;font-family:inherit}textarea::placeholder{color:var(--placeholder)}
  .btn-row{display:flex;gap:10px;margin:6px 0 14px}.btn-generate{flex:3;padding:14px 0;border-radius:12px;border:none;background:linear-gradient(135deg,#7c3aed,#a855f7);color:#fff;font-size:1.071rem;font-weight:700;cursor:pointer;letter-spacing:.03em}.btn-reset{flex:1;padding:14px 0;border-radius:12px;border:1px solid var(--reset-bdr);background:transparent;color:var(--reset-col);font-size:1rem;font-weight:600;cursor:pointer}.btn-copy{padding:6px 14px;border-radius:8px;border:1px solid #7c3aed;background:transparent;color:#a855f7;font-size:.857rem;font-weight:600;cursor:pointer;transition:all .2s}.btn-copy.copied{background:var(--copy-done-bg);color:var(--copy-done-col)}
  .output-ta{width:100%;height:300px;font-size:.786rem;color:var(--text-sub);line-height:1.8;font-family:monospace;background:var(--bg-ta);border-radius:8px;padding:10px 12px;border:1px solid var(--border);resize:none;outline:none}.info-row{display:flex;align-items:flex-start;gap:8px;font-size:.857rem;color:var(--text-sub);margin-bottom:5px}.info-icon{flex-shrink:0;color:#7c3aed}.info-val{color:var(--info-val);font-weight:600}.card-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}.hidden{display:none}
  .help-overlay{position:fixed;inset:0;z-index:50;background:rgba(0,0,0,.55);display:flex;align-items:flex-end;justify-content:center;padding:14px}.help-overlay.hidden{display:none}.help-sheet{width:100%;max-width:520px;background:var(--bg-card);border:1px solid var(--border-pu);border-radius:16px;padding:16px;box-shadow:0 -10px 40px rgba(0,0,0,.35)}.help-title{font-size:1.071rem;font-weight:700;color:var(--text);margin-bottom:8px}.help-body{font-size:.929rem;line-height:1.75;color:var(--text-sub);white-space:pre-line}.help-close{margin-top:14px;width:100%;padding:12px 0;border-radius:12px;border:1px solid #7c3aed;background:transparent;color:#c4b5fd;font-weight:700;font-size:1rem}

  button,textarea,input,select{font-family:inherit}
  .preset-select{width:100%;box-sizing:border-box;border:1px solid #d4d4d8;border-radius:12px;background:#fff;color:#18181b;padding:12px 14px;font-size:.93rem;line-height:1.4;outline:none}
  .preset-select:focus{border-color:#8b5cf6;box-shadow:0 0 0 3px rgba(139,92,246,.12)}
  .validation-status{margin-top:9px;padding:9px 11px;border-radius:10px;font-size:.786rem;line-height:1.55;background:#f4f4f5;color:#71717a;border:1px solid #e4e4e7;white-space:pre-line}
  .validation-status.ok{background:#f0fdf4;color:#166534;border-color:#bbf7d0}
  .validation-status.error{background:#fef2f2;color:#b91c1c;border-color:#fecaca}
</style>
</head>
<body>
<div class="header">
  <div class="header-icon">✦</div>
  <div><div class="header-title">Stable Character Prompt Generator</div><div class="header-sub">v9.1.1</div><div class="header-sub">参照/空間演出/拡張エフェクト</div></div>
  <div class="header-time"><div class="header-time-main" id="hTime">--:--</div><div class="header-time-sub" id="hDay">-- · --月 · --</div></div>
</div>
<div class="content">
  <div class="card card-dark"><div class="slabel">自動取得 — 東京時間</div><div class="info-row"><span class="info-icon">📅</span><span id="infoDay">取得中…</span></div><div class="info-row"><span class="info-icon">🕐</span><span id="infoTime">取得中…</span></div><div class="info-row"><span class="info-icon">💭</span><span id="infoDayMood" style="font-size:.786rem;color:#71717a;"></span></div><div class="info-row"><span class="info-icon">✂️</span><span><span style="font-size:.786rem;color:#71717a;">今月のヘアスタイル</span><br><span id="infoHair" style="font-size:.857rem;"></span></span></div></div>

  <div class="card card-dark"><div class="slabel">被写体設定 — 9枚画像参照</div><div class="hint">OFFは被写体画像参照を使用せず、被写体テキストも追加しません。ONは被写体画像A1〜A9の9枚を同時添付して参照します。A1〜A3は顔、A4〜A6は上半身、A7〜A9は全身の正面・45°・真横です。顔IDに加え、バスト・ウエスト・骨盤・ヒップ、胴体、四肢、全身比率を身体ラインから直接読みます。服・髪型・ポーズ・構図・背景は参照しません。</div><div class="slabel" style="margin-top:10px;">被写体A1〜A9画像参照</div><div class="chips" id="characterModeChips"></div></div>

  <div class="card card-dark"><div class="slabel">コーデ画像B参照（被写体9枚の後に最後の1枚）</div><div class="hint">OFFはシーンに合うコーディネートをおまかせで作成します。ONは被写体A1〜A9の後に最後の1枚として添付したコーデ画像Bを使用します。服・靴・バッグ・アクセサリー・配色をFULL相当で厳格に使用します。コーディネートシートの場合も、枠やテンプレデザインは生成画像に持ち込みません。</div><div class="chips" id="outfitReferenceModeChips"></div></div>

  <div class="card card-dark"><div class="slabel">場所画像C参照（任意）</div><div class="hint">OFFは場所を②シーン文章だけで決めます。ONは場所画像Cを追加参照し、建築・素材・空間構成・植栽・照明・雰囲気だけを場所の基準として使います。人物・服・ポーズ・構図は参照しません。</div><div class="chips" id="locationReferenceModeChips"></div></div>

  <div class="card"><div class="slabel">撮影方式 — 自撮り / 第三者撮影</div><div class="hint">最初に撮影方式を選べます。撮影プリセットを先に選んだ場合は、対応する撮影方式が自動選択されます。プリセット適用後も、この項目を含めて個別に変更できます。</div><div class="chips" id="selfieModeChips"></div></div>

  <div class="card"><div class="slabel">撮影プリセット</div><div class="hint">自撮り用と第三者撮影用を分けた一括選択です。アングル・写す範囲・傾き・顔向き・視線・背景・余白・作り込み度・表現の主役・身体の動きなどの既存項目を自動選択します。場所・行動・人数などのシチュエーションは変更しません。</div>
    <select class="preset-select" id="shootingPresetSelect" onchange="handleShootingPresetChange()">
      <option value="">プリセットを選択</option>
      <option value="custom">カスタム（個別調整中）</option>
      <optgroup label="自撮り">
        <option value="selfieDaily">🤳 自然な日常セルフィー</option>
        <option value="selfieModel">🧍 モデル風セルフィー</option>
        <option value="selfieEditorial">🖤 ファッションエディトリアル風セルフィー</option>
        <option value="selfieCinematic">🎬 シネマティックセルフィー</option>
      </optgroup>
      <optgroup label="第三者撮影">
        <option value="thirdDaily">📷 自然な日常スナップ</option>
        <option value="thirdPortrait">🖼️ ポートレート撮影</option>
        <option value="thirdModel">🧍 モデル撮影</option>
        <option value="thirdEditorial">🖤 ファッションエディトリアル撮影</option>
        <option value="thirdCinematic">🎬 シネマティック撮影</option>
      </optgroup>
    </select>
  </div>

  <div class="card"><div class="slabel">写真の作り込み度</div><div class="hint">ラフな日常写真から作品撮りまで、写真をどの程度整えて作り込むかだけを選びます。カメラ位置や表現の主役とは独立しています。</div><div class="chips" id="photoStyleChips"></div></div>

  <div class="card"><div class="slabel">表現の主役</div><div class="hint">人物・服／コーデ・背景／場所に加え、被写体と飲み物・食べ物・テーブル上を一緒に見せる構図を選べます。シーンに存在しない料理や飲み物は追加しません。AUTOの被写体サイズ／余白は、この選択に連動します。</div><div class="chips" id="visualFocusChips"></div></div>

  <div class="card" id="sceneCard"><div class="slabel">① 今回のシーンだけ（日本語で入力）</div><div class="hint">場所・服装・姿勢（立つ／座る／横になる）・前傾・身体の支え・行動・表情・何をしているかを手で書きます。入力内容に連動し、成立条件が不足するアングル・主役・躍動感・写す範囲は自動で無効になります。</div><textarea id="situation" rows="4" placeholder="例：カフェのテーブル席に座り、片肘をついて少し前傾している。" oninput="handleSituationInput()"></textarea><div class="validation-status" id="sceneValidationStatus">シーン連動チェック：シーンを入力すると、成立しない選択肢を自動で無効化します。</div></div>

  <div class="card"><div class="slabel">② 天気を選択</div><div class="chips" id="weatherChips"></div></div>
  <div class="card"><div class="slabel">③ フィルムトーン / 質感</div><div class="hint">長押しでヘルプ表示。選んだトーンと相性の悪いエフェクトは自動解除され、選択不可になります。</div><div class="chips" id="filmChips"></div></div>
  <div class="card"><div class="slabel">④ 作品トーン</div><div class="hint">長押しでヘルプ表示。写真全体の印象を選びます。</div><div class="chips" id="toneChips"></div></div>
  <div class="card"><div class="slabel">⑤ エフェクト（複数選択可）</div><div class="hint">フィルムトーンや選択済みエフェクトと相性の悪い項目はグレー表示で選択不可になります。まずは3〜5個がおすすめ。</div><div class="chips" id="effectChips"></div></div>
  <div class="card"><div class="slabel">⑥ エフェクト強度</div><div class="hint">選択エフェクトのweightを倍率補正します。通常プロンプトには触りません。</div><div class="chips" id="effectStrengthChips"></div></div>
  <div class="card"><div class="slabel">⑦ 追加要素 / 空間演出（複数選択可）</div><div class="hint">全項目を8系統に分類しました。見出しをタップして開閉し、長押しで使い方を確認できます。後加工ではなく、シーン内に実在する光・空気・影・動く物・前景として配置します。合計2〜5個程度がおすすめです。</div><div class="option-groups" id="additionalElementChips"></div></div>
  <div class="card"><div class="slabel">⑧ 肌の見え方 / 肌質感</div><div class="chips" id="skinFinishChips"></div></div>
  <div class="card"><div class="slabel">⑨ 接写質感</div><div class="hint">顔のみ・顔どアップ・横顔アップで効きやすい質感です。</div><div class="chips" id="closeupTextureChips"></div></div>
  <div class="card"><div class="slabel">⑩ カメラ位置 / アングル</div><div class="hint">357系の完成済み撮影プリセットです。7系統に分類し、カメラ高さ・被写体との距離・方向・光軸・遠近感を1項目で確定します。アングルを選択すると、そのアングルが属する分類だけを残して他の分類は自動で閉じます。写す範囲や背景設定は、選択したアングルの距離を変えません。</div><div class="option-groups" id="angleModeChips"></div></div>
  <div class="card"><div class="slabel">⑪ 写す範囲</div><div class="hint">顔のみ・顔どアップなどを追加。場所を見せる量は背景/余白側で調整します。</div><div class="chips" id="visibleRangeChips"></div></div>
  <div class="card"><div class="slabel">⑫ 画面の傾き</div><div class="hint">構図の回転だけを指定します。腰だめやローアングルの起点は変えません。</div><div class="chips" id="cameraRollChips"></div></div>
  <div class="card"><div class="slabel">⑬ 顔向き</div><div class="chips" id="faceDirectionChips"></div></div>
  <div class="card"><div class="slabel">⑭ 視線</div><div class="chips" id="gazeChips"></div></div>
  <div class="card"><div class="slabel">⑮ 背景の見せ方</div><div class="hint">店内・街・建築など、被写体の後方空間をどの程度見せるかを選びます。表現の主役が「被写体＋飲み物／食べ物／テーブル上」の場合は、重複を避けるため「指定なし」に自動固定されます。</div><div class="chips" id="backgroundViewChips"></div></div>
  <div class="card"><div class="slabel">⑯ 被写体サイズ / 余白</div><div class="chips" id="framingChips"></div></div>
  <div class="card"><div class="slabel">⑰ 身体の動き / 躍動感</div><div class="hint">立つ・座るなどの基本姿勢ではなく、その姿勢の中で髪・服・腕・上体がどの程度動いて見えるかを選びます。自撮り時は撮影腕をカメラ位置へ固定したまま、空いている手と上体の動きへ反映します。モーションブラーとは別の物理的な動きです。</div><div class="chips" id="motionEnergyChips"></div></div>
  <div class="card"><div class="slabel">⑱ 表情（顔の出力）</div><div class="hint">未選択の場合はシーン・時間・天気から自然に導出します。</div><div class="chips" id="expressionChips"></div></div>
  <div class="btn-row"><button class="btn-generate" id="btnGen" onclick="handleGenerate()">✦ プロンプト生成</button><button class="btn-reset" onclick="handleReset()">リセット</button></div>
  <div class="card card-dark hidden" id="metaCard"><div class="slabel">展開結果サマリー</div><div id="metaContent" style="font-size:.857rem;color:#a1a1aa;line-height:1.9;"></div></div>
  <div class="card card-out hidden" id="outputCard"><div class="card-head"><div class="slabel" style="margin-bottom:0;">生成プロンプト</div><button class="btn-copy" id="btnCopy" onclick="handleCopy()">コピー</button></div><textarea class="output-ta" id="outputArea" readonly onclick="this.select();this.setSelectionRange(0,this.value.length);" onfocus="this.select();this.setSelectionRange(0,this.value.length);"></textarea></div>
</div>
<div class="help-overlay hidden" id="chipHelpOverlay" onclick="hideChipHelp()"><div class="help-sheet" onclick="event.stopPropagation()"><div class="help-title" id="chipHelpTitle">ヘルプ</div><div class="help-body" id="chipHelpBody"></div><button class="help-close" onclick="hideChipHelp()">閉じる</button></div></div>
<script>
const APP_VERSION = "v9.1.3";
const HAIR_BY_MONTH = {1:"(long straight, dark brown hair:1.65), (hair falls below the shoulders:1.55)",2:"(long wave, chestnut brown gradient hair:1.65), (hair falls below the shoulders:1.55)",3:"(long soft wave, chestnut brown hair:1.65), (hair falls below the shoulders:1.55)",4:"(medium straight, chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",5:"(medium wave, light chestnut brown hair:1.6), (shoulder-length medium hair:1.5)",6:"(soft bob, ash brown hair:1.78), (jaw-to-neck length bob:1.88), (not long hair:1.95)",7:"(short airy bob, ash brown hair:1.9), (airy bob ending strictly between the jaw and the base of the neck:2.0), (all visible hair terminates above the shoulders:2.0)",8:"(short bob, light ash brown hair:1.8), (clear short bob length above or around jaw:1.9), (not long hair:1.98)",9:"(medium bob, ash brown to dark brown hair:1.75), (shoulder-grazing medium bob length:1.82), (not chest-length hair:1.95)",10:"(inner-color straight, dark brown with caramel inner highlight:1.65), (long hair below shoulders:1.55)",11:"(inner-color wave, dark brown with rose-beige inner highlight:1.65), (long hair below shoulders:1.55)",12:"(long straight, dark brown with subtle inner highlight:1.65), (long hair below shoulders:1.55)"};
const HAIR_DISPLAY_BY_MONTH = {
  1:"ロングストレート／ダークブラウン／肩より下",
  2:"ロングウェーブ／チェスナットブラウンのグラデーション／肩より下",
  3:"ロングソフトウェーブ／チェスナットブラウン／肩より下",
  4:"ミディアムストレート／チェスナットブラウン／肩丈",
  5:"ミディアムウェーブ／ライトチェスナットブラウン／肩丈",
  6:"ソフトボブ／アッシュブラウン／顎〜首元",
  7:"エアリーボブ／アッシュブラウン／顎〜首元",
  8:"ショートボブ／ライトアッシュブラウン／顎上〜顎周辺",
  9:"ミディアムボブ／アッシュ〜ダークブラウン／肩に触れる程度",
  10:"インナーカラーストレート／ダークブラウン＋キャラメル／肩より下",
  11:"インナーカラーウェーブ／ダークブラウン＋ローズベージュ／肩より下",
  12:"ロングストレート／ダークブラウン＋控えめインナーカラー／肩より下"
};
const HAIR_STRICT_LOCK_BY_MONTH = {
  1:"(hair must remain visibly long and straight, extending below the shoulders:2.0), (dark brown is the mandatory hair color:2.0), (do not shorten to bob or shoulder length:2.0)",
  2:"(hair must remain visibly long with natural waves and extend below the shoulders:2.0), (chestnut-brown gradient is mandatory:2.0), (do not shorten to bob or shoulder length:2.0)",
  3:"(hair must remain visibly long with soft waves and extend below the shoulders:2.0), (chestnut brown is the mandatory hair color:2.0), (do not shorten to bob or shoulder length:2.0)",
  4:"(hair must end around shoulder length as a medium straight cut:2.0), (chestnut brown is mandatory:2.0), (do not extend to chest length and do not shorten to a jaw-length bob:2.0)",
  5:"(hair must end around shoulder length as a medium wavy cut:2.0), (light chestnut brown is mandatory:2.0), (do not extend to chest length and do not shorten to a jaw-length bob:2.0)",
  6:"(hair must end between the jaw and lower neck as a soft bob:2.0), (ash brown is mandatory:2.0), (no strands extend below the shoulders, across the chest, down the back, or far across the pillow beyond bob length:2.0), (no ponytail, bun, braid, extensions, or hidden long hair:2.0)",
  7:"(hair must end strictly between the jaw and the base of the neck as a clearly short airy bob:2.0), (ash brown is mandatory:2.0), (every visible strand must terminate above the shoulder line:2.0), (no shoulder-touching hair, no shoulder-length hair, and no hair extending across the chest or down the back:2.0), (no long strands spreading across the pillow or bed:2.0), (no ponytail, bun, braid, pigtails, extensions, tied-back hair, gathered hair, or hidden long hair behind the head:2.0), (reclining, side-lying, gravity, wind, or body motion may change only the direction of the short bob ends and must never increase the actual cut length:2.0)",
  8:"(hair must remain a clearly short bob ending above or around the jaw:2.0), (light ash brown is mandatory:2.0), (no hair below the neck or shoulders:2.0), (no ponytail, bun, braid, extensions, or hidden long hair:2.0)",
  9:"(hair must remain a medium bob that only grazes the shoulders:2.0), (ash brown to dark brown is mandatory:2.0), (do not extend to chest length or long back-length hair:2.0)",
  10:"(hair must remain long and straight below the shoulders:2.0), (dark brown base with caramel inner highlights is mandatory:2.0), (do not shorten to a bob or remove the inner-color contrast:2.0)",
  11:"(hair must remain long and wavy below the shoulders:2.0), (dark brown base with rose-beige inner highlights is mandatory:2.0), (do not shorten to a bob or remove the inner-color contrast:2.0)",
  12:"(hair must remain long and straight below the shoulders:2.0), (dark brown with a subtle inner highlight is mandatory:2.0), (do not shorten to a bob or remove the subtle inner-color treatment:2.0)"
};
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
const CHARACTER_MODE_OPTIONS=[opt("🚫 OFF / 被写体参照なし","off","off"),opt("📷 ON / 被写体9枚画像から","on","on")];
const OUTFIT_REFERENCE_MODE_OPTIONS=[opt("🎲 OFF / コーデおまかせ","off","off"),opt("👗 ON / コーデ画像Bから","on","on")];
const LOCATION_REFERENCE_MODE_OPTIONS=[opt("🎲 OFF / シーン文のみ","off","off"),opt("📍 ON / 場所画像Cから","on","on")];
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
opt("サンフェード・ミルキーフィルム","sunfademilky","sun-faded milky film tone, thin white atmospheric veil across the entire image, pale cyan-blue air, softly bleached highlights, gently muted color, bright airy skin and sky, retained deep natural shadows, subtle analog grain",`日差しで少し退色したような白いベールと、淡いシアンブルーの空気感を出します。

向く場面
夏の海、青空、強い日差し、乾いた屋外、爽やかな全身写真。

注意
単なる白飛びやハイキーにはせず、髪・岩・建物などの深い自然な影は残します。`),
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
opt("📱 スマホHDR","hdr","(smartphone HDR rendering:1.74), (clean dynamic range and lifted shadows:1.72)","スマホ写真っぽく明暗を整えます。"),
opt("☀️ 硬い直射日光","hardsun","(harsh direct sunlight:1.86), (strong overhead or side sunlight with hard-edged illumination:1.84), (crisp sunlit highlights on skin, hair, and clothing:1.82)","真昼の強い太陽光を作ります。柔らかい光ではなく、輪郭のはっきりした日差し向き。"),
opt("⬛ 鋭い影","hardshadow","(sharp hard-edged shadows:1.88), (deep crisp shadow separation:1.84), (clearly defined shadow lines across face, body, and environment:1.84)","くっきりした影を出します。直射日光や強い単一光源と相性が良いです。"),
opt("✴️ 白飛びハイライト","blownhighlight","(slightly blown bright highlights:1.8), (sun-struck highlight clipping in bright areas:1.76), (hot bright specular highlights with slight overexposure:1.76)","強い光でハイライトが少し飛ぶ質感です。夏の屋外やフラッシュ感の補助向き。"),
opt("🌡️ 熱気 / ヒートヘイズ","heathaze","(subtle heat haze in sunlit air:1.72), (dry shimmering atmosphere:1.7), (faint wavering hot-air distortion where physically appropriate:1.66)","暑い屋外のゆらぐ空気感を少し足します。入れすぎると画が崩れやすいので控えめ向き。"),
opt("🏜️ 乾いたダスト感","drydust","(dry dusty atmosphere:1.72), (sunlit airborne dust particles:1.68), (parched gritty outdoor air:1.68)","乾いた屋外の粉っぽい空気感を足します。廃車置き場、荒れた場所、夏の路地向き。"),
opt("🤲 手前の手ボケ","handblur","(a hand is extended very close to the camera lens:1.96), (the foreground hand appears large and strongly out of focus due to proximity:1.96), (face remains sharply focused while the hand in front is blurred:1.98), (strong near-far depth separation between face and foreground hand:1.94)","手前に差し出した手を大きくぼかします。顔にピントを残しつつ、近接した手だけを強く前ボケさせたい時向き。"),
opt("🫧 強い前ボケ","strongForeground","(clearly visible strong foreground blur entering the frame:1.86), (foreground subject or object is heavily defocused near the lens:1.84), (pronounced front-layer blur creates strong layered depth:1.84), (foreground blur is visually obvious and not subtle:1.84)","通常の前ボケより強く、レンズ近くの物をはっきりぼかします。奥行きと近接感を強く出したい時向き。"),
opt("◐ 光と影を強調","lightshadow","(strong light-and-shadow contrast:1.88), (bright highlights and deep shadows clearly separated:1.86), (dramatic sculpting light across the face and body:1.84), (three-dimensional form emphasized by directional lighting:1.84)","明るい部分と暗い部分の差を強め、立体感のある陰影を出します。人物や物の造形をくっきり見せたい時向き。"),
opt("🎭 キアロスクーロ","chiaroscuro","(chiaroscuro lighting:1.9), (dramatic contrast between illuminated areas and deep darkness:1.88), (classical cinematic light-and-shadow composition:1.84), (subject emerging from shadow:1.82)","光と闇のコントラストを強く出す、映画的で古典絵画的な陰影です。重めでドラマチックな雰囲気向き。"),
opt("◑ スプリットライト","splitlight","(split lighting across the face:1.88), (one side of the face illuminated and the other side in deep shadow:1.88), (clear directional half-light portrait effect:1.86)","顔の片側を明るく、もう片側を暗くして、半分で割るようなライティングを作ります。"),
opt("🌿 木漏れ日シャドウ","dappledshadow","(dappled sunlight and patterned shadows across the subject:1.86), (irregular leaf-shaped light and shadow patterns:1.82), (natural broken sunlight with crisp shadow edges:1.8)","葉の隙間から差す光のような、まだらな光と影の模様を作ります。屋外感や自然光感を強めたい時向き。")
];
const EFFECT_DISPLAY_ORDER=["bokeh","foreground","strongForeground","orb","glass","droplet","rim","flash","warmflare","lightleak","neon","hardsun","hardshadow","blownhighlight","lightshadow","chiaroscuro","splitlight","dappledshadow","softfocus","motionblur","heathaze","drydust","sparkle","coolfilter","hdr","digicam","grain","vhs","vignette","handblur"];
function sortedEffects(){const rank=new Map(EFFECT_DISPLAY_ORDER.map((k,i)=>[k,i]));return [...EFFECTS].sort((a,b)=>(rank.get(a.key)??999)-(rank.get(b.key)??999)||a.label.localeCompare(b.label,"ja"));}

const ADDITIONAL_ELEMENTS=[
// 光線・光源
opt("☀️ 斜めに差す光の筋","diagonalSunbeam","(a clearly readable diagonal shaft of natural light crosses the scene:1.82), (the light beam has a plausible source and illuminates nearby surfaces and particles:1.78)",`斜め方向へ伸びる一本の光の筋を空間に作ります。

向く場面
古い建物、窓のある室内、路地、映画的な静止画。

注意
光源となる窓や隙間が見える、または画面外に自然に存在できる場面向きです。`),
opt("🪟 窓から差す光","windowBeam","(natural daylight enters through a window and forms a visible beam in the room:1.8), (the window light creates coherent illumination on the floor, wall, and subject:1.78)",`窓から室内へ差し込む自然光を作ります。

向く場面
教室、ホテル、古民家、オフィス、朝夕の室内。

注意
窓の位置と影の方向が矛盾しないように使います。`),
opt("🚪 扉の隙間光","doorCrackLight","(a narrow band of light enters through a doorway or door gap:1.8), (the narrow light strip falls naturally across the floor or wall:1.76)",`扉や入口の隙間から細い光を差し込みます。

向く場面
廊下、暗い室内、倉庫、舞台裏、ミステリアスな場面。

注意
光の筋は細めです。広い光芒が欲しい場合は「光芒」を選びます。`),
opt("✨ 光芒 / ゴッドレイ","godRays","(visible volumetric light rays extend through the atmosphere:1.84), (the rays reveal depth through illuminated air without covering the subject:1.8)",`光が空気中を通る筋として見える、光芒を作ります。

向く場面
窓光、森、寺社、古い室内、舞台、逆光。

注意
薄い霧やホコリと組み合わせると自然です。光源なしで乱発すると不自然になります。`),
opt("⛅ 雲間からの光","cloudRays","(sunbeams break through gaps in the clouds and reach the scene:1.8), (the sky and ground share coherent directional light:1.76)",`雲の隙間から地上へ落ちる光の筋を作ります。

向く場面
広い屋外、海、丘、都市遠景、ドラマチックな空。

注意
室内には向きません。背景に空が見える構図で使います。`),
opt("📽️ プロジェクター光","projectorBeam","(a visible projector beam travels through the room toward a screen:1.8), (fine airborne particles reveal the projector light path:1.74)",`プロジェクターからスクリーンへ伸びる光の通り道を見せます。

向く場面
研修室、会議室、映画館、教室、プレゼン会場。

注意
プロジェクターとスクリーンの位置関係を自然に保ちます。`),
opt("🎭 スポットライト光柱","spotlightColumn","(a focused spotlight forms a visible column of light in the scene:1.82), (the illuminated area and surrounding falloff remain physically coherent:1.78)",`舞台照明のような、限定された光の柱を作ります。

向く場面
ステージ、ライブ、展示、夜のイベント、暗い室内。

注意
日常の明るいオフィスでは演出感が強くなります。`),
opt("▱ 床の光だまり","floorLightPool","(a distinct pool of light falls naturally across the floor:1.78), (the light patch follows the shape of the opening and surrounding architecture:1.74)",`床にまとまった明るい光の領域を作ります。

向く場面
窓辺、玄関、廊下、古い建物、午後の日差し。

注意
人物を必ず光の中心に置く指定ではありません。構図に合わせて自然に配置します。`),
opt("🌅 逆光の光の幕","backlitVeil","(backlight forms a thin luminous veil in the air behind the subject:1.8), (the bright atmospheric layer separates the subject from the background:1.76)",`人物の後方に、薄い光の幕のような空気層を作ります。

向く場面
夕方、窓辺、屋外逆光、ステージ、幻想的な場面。

注意
顔が暗く潰れないよう、補助光のある場面に向きます。`),
opt("🌊 水面反射の揺れる光","waterCaustics","(moving water-reflected light patterns ripple across nearby walls, ceilings, or skin:1.78), (the reflected pattern follows a believable nearby water source:1.74)",`水面で反射した揺れる光模様を壁や天井へ映します。

向く場面
プール、海辺、水族館、水辺の室内、夏の演出。

注意
水源が存在しない場面では不自然になりやすいです。`),
// 空気・粒子
opt("🫧 舞うホコリ","floatingDust","(visible dust motes drift naturally through illuminated air:1.82), (the dust is most visible inside the light path and remains subtle elsewhere:1.78)",`空気中をゆっくり舞うホコリを入れます。

向く場面
古い建物、倉庫、木造室内、窓光、静かな空間。

注意
画面全体を雪のように埋めず、光が当たる場所を中心に見せます。`),
opt("· 微細な浮遊粒子","fineAirParticles","(very fine airborne particles become faintly visible in the light:1.76), (the particles add depth without looking decorative or glittery:1.74)",`ホコリより細かく、控えめな空気中の粒子を加えます。

向く場面
室内光、逆光、透明感のある写真、静かな映画調。

注意
キラキラ加工ではなく、自然な空気の密度として使います。`),
opt("✨ 光を受ける粒子","sparklingDust","(small airborne particles catch the directional light and briefly sparkle:1.78), (the sparkle remains physically tied to the light source:1.74)",`光を受けた粒子だけが小さく輝く状態を作ります。

向く場面
窓光、夕日、舞台照明、幻想的な室内。

注意
エフェクトの「きらめき粒子」より実在感重視です。過度なラメ状にはしません。`),
opt("🌾 花粉・綿毛","pollenFluff","(a few soft pollen grains or seed fluffs drift through the air:1.76), (their movement follows a gentle natural breeze:1.72)",`花粉や植物の綿毛が風に流れる様子を入れます。

向く場面
春、草原、公園、窓辺、柔らかい屋外。

注意
量を増やしすぎると雪に見えるため、少量向きです。`),
opt("🌫️ 薄い霞","thinMist","(a thin atmospheric mist softens distant depth while keeping the subject clear:1.78), (the mist gathers naturally in the background and light paths:1.74)",`空間の奥に薄い霞を入れ、距離感を出します。

向く場面
朝、森、屋外、広い室内、幻想的な光。

注意
ソフトフォーカスとは違い、物理的な空気層として配置します。`),
opt("☁️ 低い霧","groundFog","(low-lying fog gathers near the floor or ground:1.8), (the fog remains below the subject's face and follows terrain or floor level:1.76)",`床や地面付近に溜まる低い霧を作ります。

向く場面
森、夜道、ステージ、廃墟、朝の屋外。

注意
人物の顔まで霧で覆わないようにします。`),
opt("♨️ 湯気","steam","(natural steam rises from a plausible hot source in soft translucent curls:1.78), (the steam catches nearby light without obscuring the scene:1.74)",`温かい飲み物、料理、風呂などから立つ湯気を加えます。

向く場面
カフェ、厨房、温泉、冬の室内、朝食。

注意
熱源がない場所では使わない方が自然です。`),
opt("💨 薄い煙","thinSmoke","(thin translucent smoke drifts through the scene in soft layered wisps:1.78), (the smoke follows airflow and remains separate from the subject's face:1.74)",`薄く流れる煙を空間に加えます。

向く場面
舞台、工場、焚き火周辺、映画的な暗所。

注意
原因不明の濃煙にせず、薄い空間演出として使います。`),
opt("〰️ 線状の煙","incenseSmoke","(a delicate narrow ribbon of smoke curls upward from a small source:1.78), (the smoke line remains fine and clearly structured:1.74)",`お香の煙のような、細い一本の煙の流れを作ります。

向く場面
和室、寺社、静物、落ち着いた室内。

注意
広い煙霧ではなく、局所的な細い煙です。`),
opt("❄️ 白い息","breathMist","(a small natural cloud of visible breath appears in cold air:1.76), (the breath stays close to the mouth and disperses quickly:1.72)",`寒い空気の中で吐息が白く見える状態を加えます。

向く場面
冬の屋外、冷蔵施設、早朝、夜。

注意
暖かい室内や夏の場面には向きません。`),
opt("🌧️ 雨霧","rainMist","(fine rain mist hangs in the air around the scene:1.78), (backlight or streetlight reveals the moisture without hiding the subject:1.74)",`細かな雨粒が霧状に見える空気を作ります。

向く場面
雨の街、夜の駅前、逆光、濡れた道路。

注意
天気が晴れの場合は、噴水や水辺など理由のある場面で使います。`),
opt("🌊 水しぶきの霧","seaSpray","(fine water spray drifts through the air from a nearby wave, fountain, or splash:1.78), (the droplets catch directional light naturally:1.74)",`波、噴水、水遊びなどの細かな水しぶきを空気中に入れます。

向く場面
海辺、プール、噴水、夏の水辺。

注意
水源が画面内か周辺に必要です。`),
// 影・投影
opt("▦ 窓枠の影","windowFrameShadow","(window-frame shadows fall coherently across the wall, floor, or subject:1.8), (the shadow geometry matches the visible or implied window:1.76)",`窓枠の形をした直線的な影を落とします。

向く場面
室内、午後の日差し、古い建物、ホテル、教室。

注意
画面の傾きとは別です。影だけが窓の形に沿います。`),
opt("▥ ブラインド影","blindShadow","(parallel blind shadows stripe the wall, clothing, or part of the face:1.8), (the shadow spacing and direction remain consistent:1.76)",`ブラインド越しの平行な光と影を作ります。

向く場面
オフィス、ホテル、ノワール調、夕方の室内。

注意
顔全体を細かい縞で潰さないよう、部分的に使います。`),
opt("▧ 格子影","latticeShadow","(geometric lattice shadows project across nearby surfaces:1.78), (the pattern follows a plausible screen, railing, or lattice source:1.74)",`格子や柵の形をした幾何学的な影を投影します。

向く場面
和室、古い街、階段、フェンスのある場所。

注意
格子の実体または画面外の自然な光源を想定します。`),
opt("🌿 葉影","foliageShadow","(natural leaf shadows move softly across the subject and surrounding surfaces:1.8), (the irregular pattern follows nearby foliage and sunlight:1.76)",`葉の形をした自然な影を人物や壁に落とします。

向く場面
公園、窓辺、庭、夏の日差し、木の近く。

注意
エフェクトの木漏れ日より、葉や木が存在するシーン要素として扱います。`),
opt("▤ フェンス影","fenceShadow","(repeating fence or railing shadows stretch across the ground or wall:1.78), (the projected lines follow the light direction and nearby structure:1.74)",`フェンスや手すりの反復する影を入れます。

向く場面
歩道橋、駅、屋上、路地、工業地帯。

注意
人物の顔へ強く重ねるより、床や背景で構図を作る用途向きです。`),
opt("☁️ 流れる雲影","movingCloudShadow","(soft cloud shadows pass across the landscape or architecture:1.76), (broad light changes suggest slowly moving clouds overhead:1.72)",`雲が流れることで地面や建物の明るさが部分的に変わる状態を作ります。

向く場面
広い屋外、海、草原、屋上、都市景観。

注意
人物の顔に細かな模様を付ける演出ではありません。`),
opt("🌈 ステンドグラス光","stainedGlassLight","(colored stained-glass light patterns fall across the floor, wall, or subject:1.8), (the projected colors remain translucent and tied to a nearby window:1.76)",`ステンドグラスを通した色付きの光模様を投影します。

向く場面
教会、洋館、展示空間、幻想的な室内。

注意
通常のオフィスでは場面設定と合いにくいです。`),
opt("🔺 プリズムの虹光","prismRainbow","(a small prismatic rainbow reflection appears on a nearby surface:1.76), (the spectrum has a plausible glass or crystal source:1.72)",`ガラスやプリズムから生まれる小さな虹色の光を入れます。

向く場面
窓辺、ガラスのある室内、透明感のあるポートレート。

注意
画面全体を虹色にせず、局所的な反射として使います。`),
// 季節・動き
opt("🌸 舞う花びら","driftingPetals","(a small number of flower petals drift naturally through the scene:1.78), (their motion follows the wind and seasonal setting:1.74)",`花びらが風に乗って舞う様子を加えます。

向く場面
桜、花畑、春、祭り、屋外の風景。

注意
季節や周囲の植物と一致させます。`),
opt("🍂 舞う落ち葉","fallingLeaves","(a few dry leaves tumble naturally through the air:1.78), (the leaves follow wind, gravity, and the autumn setting:1.74)",`落ち葉が風に巻かれて動く様子を入れます。

向く場面
秋、公園、並木道、古い街、風のある屋外。

注意
葉の向きや動きは風に従わせます。`),
opt("❄️ 風に舞う雪","snowFlurry","(light snowflakes swirl naturally through the air:1.78), (the snow remains consistent with cold weather and surface conditions:1.74)",`雪が風に流されながら舞う状態を作ります。

向く場面
冬の街、雪原、夜、駅前、山間部。

注意
積雪や服装など周辺状況も冬に合わせる必要があります。`),
opt("🌧️ 斜めに走る雨粒","rainStreaks","(visible rain streaks cross the scene at a consistent wind-driven angle:1.78), (wet surfaces and ambient light support the rainfall:1.74)",`風で斜めに流れる雨粒を見せます。

向く場面
雨の街、夜景、駅、走る人物、強い風。

注意
画面の傾きとは別で、雨粒の方向だけが風に従います。`),
opt("🎊 紙吹雪","confetti","(a controlled amount of paper confetti falls and rotates through the scene:1.76), (the pieces follow gravity and event airflow:1.72)",`イベントの紙吹雪を空間に追加します。

向く場面
ライブ、祝賀、パーティー、ステージ、スポーツイベント。

注意
日常の静かな場面では意味のない散乱物になりやすいです。`),
opt("🫧 シャボン玉","soapBubbles","(several translucent soap bubbles float through the scene with realistic reflections:1.76), (their size, transparency, and motion vary naturally:1.72)",`透明なシャボン玉が空間を漂う様子を加えます。

向く場面
公園、イベント、夏、柔らかい幻想表現。

注意
光沢のある球体を大量に敷き詰めず、数を抑えます。`),
opt("✨ ホタル","fireflies","(a few fireflies glow softly in the surrounding darkness:1.76), (their lights are small, irregular, and physically placed in the environment:1.72)",`暗い場所に小さく光るホタルを配置します。

向く場面
夏の夜、川辺、森、田園。

注意
明るい昼間や都市室内には向きません。`),
opt("🪶 舞う羽根","floatingFeathers","(a few lightweight feathers drift slowly through the air:1.76), (their rotation and fall follow gravity and air movement:1.72)",`軽い羽根がゆっくり回転しながら落ちる様子を加えます。

向く場面
舞台、ファッション撮影、幻想的な室内、演出写真。

注意
現実的な日常スナップでは演出感が強くなります。`),
opt("📄 舞う紙片","paperFlutter","(a few loose paper sheets or small paper pieces flutter naturally in the air:1.76), (their motion follows wind and the nearby scene activity:1.72)",`資料や紙片が風でめくれたり舞ったりする動きを加えます。

向く場面
オフィス、教室、駅、風のある屋外、慌ただしい場面。

注意
重要な文字情報を読ませる用途には向きません。`),
opt("🪟 揺れるカーテン","curtainFlutter","(a nearby curtain moves gently in the breeze:1.76), (the fabric movement reveals a plausible open window or airflow:1.72)",`カーテンが風でゆっくり揺れる動きを入れます。

向く場面
窓辺、部屋、ホテル、朝、静かな生活感。

注意
窓や空気の流れがある構図で使います。`),
opt("〰️ なびく布","fabricFlutter","(a loose fabric edge, scarf, or garment layer moves naturally in the wind:1.76), (the movement respects fabric weight and wind direction:1.72)",`スカーフや裾など、軽い布が風になびく動きを加えます。

向く場面
屋外、海辺、風のある街、動きのあるファッション写真。

注意
コーデ画像Bの服の構造を勝手に変更せず、実際に動ける部分だけをなびかせます。`),
opt("💦 跳ねる水滴","splashDroplets","(individual water droplets arc through the air from a plausible splash:1.76), (the droplets catch light and follow a coherent trajectory:1.72)",`水が跳ねた瞬間の粒状の水滴を加えます。

向く場面
海、プール、噴水、雨上がり、水遊び。

注意
水源と動作の原因が必要です。`),
// 前景・空間フレーム
opt("🌿 手前の葉","foregroundLeaves","(real leaves occupy a small part of the near foreground as physical scene elements:1.76), (the leaves frame the subject without covering the face:1.72)",`カメラ近くに実在する葉を置いて、自然な前景を作ります。

向く場面
庭、公園、森、窓辺、屋外ポートレート。

注意
前ボケ加工ではなく、葉そのものを配置します。顔を隠さないようにします。`),
opt("🌼 手前の花","foregroundFlowers","(real flowers appear near the foreground and frame the lower or side edge:1.76), (the flowers belong naturally to the location and season:1.72)",`手前に花を配置して画面の縁を構成します。

向く場面
花畑、庭、店先、イベント、春夏の屋外。

注意
背景に存在しない花を無関係に追加しないようにします。`),
opt("🚪 扉・柱で縁取る","doorwayFrame","(a doorway, column, or architectural edge physically frames part of the composition:1.76), (the foreground structure creates depth without blocking the subject:1.72)",`扉や柱などの建築要素を画面端に入れて、人物を縁取ります。

向く場面
廊下、ロビー、古い建物、駅、室内スナップ。

注意
ビネットではなく、実在する構造物によるフレーミングです。`),
opt("🪟 手前のカーテン端","foregroundCurtain","(a real curtain edge enters the near foreground and softly frames the scene:1.76), (the curtain remains physically connected to the room and does not become an abstract overlay:1.72)",`カメラ近くのカーテンの端を画面に入れ、室内らしい奥行きを作ります。

向く場面
ホテル、寝室、窓辺、柔らかい室内写真。

注意
人物の顔やコーデを大きく隠さないようにします。`)
];
const ADDITIONAL_ELEMENT_GROUPS=[
  {key:"light",label:"☀️ 光の筋・光源",note:"窓光、光芒、スポットライト、水面反射など、光源と光の通り道。",promptTitle:"scene lighting and light paths",items:["diagonalSunbeam","windowBeam","doorCrackLight","godRays","cloudRays","projectorBeam","spotlightColumn","floorLightPool","backlitVeil","waterCaustics"]},
  {key:"particles",label:"✨ 空気中の粒子",note:"ホコリ、微粒子、光を受ける粒子、花粉・綿毛。",promptTitle:"airborne particles",items:["floatingDust","fineAirParticles","sparklingDust","pollenFluff"]},
  {key:"mist",label:"🌫️ 霧・煙・蒸気・水分",note:"霞、低い霧、湯気、煙、白い息、雨霧、水しぶきの霧。",promptTitle:"mist, smoke, steam, and moisture",items:["thinMist","groundFog","steam","thinSmoke","incenseSmoke","breathMist","rainMist","seaSpray"]},
  {key:"shadow",label:"▦ 投影光・影・色反射",note:"窓枠・ブラインド・葉影などの形ある影と、色付きの投影光。",promptTitle:"projected light, shadow, and colored reflection",items:["windowFrameShadow","blindShadow","latticeShadow","foliageShadow","fenceShadow","movingCloudShadow","stainedGlassLight","prismRainbow"]},
  {key:"nature",label:"🌸 季節・自然現象",note:"花びら、落ち葉、雪、雨粒、ホタルなど、季節や天候に結び付く動き。",promptTitle:"seasonal and weather-driven movement",items:["driftingPetals","fallingLeaves","snowFlurry","rainStreaks","fireflies"]},
  {key:"staging",label:"🎊 演出物・浮遊物",note:"紙吹雪、シャボン玉、羽根など、意図的に加える演出物。",promptTitle:"staged floating objects",items:["confetti","soapBubbles","floatingFeathers"]},
  {key:"objectMotion",label:"〰️ 布・紙・水の動き",note:"舞う紙、揺れるカーテン、なびく布、跳ねる水滴。",promptTitle:"physical object and fabric movement",items:["paperFlutter","curtainFlutter","fabricFlutter","splashDroplets"]},
  {key:"foreground",label:"🌿 前景・空間フレーム",note:"葉・花・扉・柱・カーテン端をレンズ近くに置く物理的な前景。",promptTitle:"foreground and architectural framing",items:["foregroundLeaves","foregroundFlowers","doorwayFrame","foregroundCurtain"]}
];
const ADDITIONAL_ELEMENT_DISPLAY_ORDER=ADDITIONAL_ELEMENT_GROUPS.flatMap(group=>group.items);
function sortedAdditionalElements(){const rank=new Map(ADDITIONAL_ELEMENT_DISPLAY_ORDER.map((k,i)=>[k,i]));return [...ADDITIONAL_ELEMENTS].sort((a,b)=>(rank.get(a.key)??999)-(rank.get(b.key)??999)||a.label.localeCompare(b.label,"ja"));}

const EFFECT_STRENGTH_OPTIONS=[opt("🫧 控えめ","subtle","subtle","") ,opt("✨ 標準","standard","standard",""),opt("🌟 強め","strong","strong",""),opt("💥 盛り盛り","max","max","")];
const EFFECT_MULT={subtle:.9,standard:1,strong:1.38,max:1.65};

// FILM / EFFECT COMPATIBILITY GUARD
// 明確に方向性がぶつかる組み合わせだけを無効化。選択済みweightや元プロンプトは変更しない。
const FILM_EFFECT_CONFLICTS={
  none:[],
  gold200:["coolfilter","hdr","vhs"],
  portra400:["vhs","hdr"],
  portra800:["hardsun","dappledshadow","hdr"],
  ektar100:["softfocus","vhs","hdr","grain"],
  fuji400h:["hardsun","hardshadow","chiaroscuro","vhs","hdr","drydust"],
  superia400:["hdr","chiaroscuro"],
  realaace:["vhs","hdr","grain","blownhighlight"],
  cinestill800t:["hardsun","heathaze","drydust","dappledshadow"],
  ilfordhp5:["warmflare","coolfilter","neon","lightleak"],
  polaroid:["vhs","hdr","hardshadow","chiaroscuro","splitlight"],
  lomo:["hdr","softfocus"],
  cinemascope:["vhs","digicam","hdr"],
  sunfademilky:["hdr","vhs"],
  vintage90s:["hdr","chiaroscuro"],
  gritty:["softfocus","sparkle","orb","hdr"]
};
const EFFECT_CONFLICTS={
  warmflare:["coolfilter"],
  bokeh:["orb"],
  foreground:["strongForeground","handblur"],
  strongForeground:["handblur"],
  softfocus:["motionblur","hardshadow","lightshadow","chiaroscuro","splitlight","dappledshadow"],
  vhs:["digicam","hdr"],
  digicam:["hdr"],
  droplet:["heathaze","drydust"],
  flash:["hardsun","dappledshadow","chiaroscuro"],
  neon:["hardsun"],
  hdr:["blownhighlight"],
  hardshadow:["lightshadow","chiaroscuro","splitlight","dappledshadow"],
  lightshadow:["chiaroscuro","splitlight","dappledshadow"],
  chiaroscuro:["splitlight","dappledshadow"],
  splitlight:["dappledshadow"],
  hardsun:["flash","neon"],
  dappledshadow:["flash","splitlight"],
  heathaze:["droplet"],
  drydust:["droplet"],
  blownhighlight:["hdr"]
};
const WEATHER_EFFECT_CONFLICTS={
  cloudy:["hardsun","dappledshadow","heathaze"],
  drizzle:["hardsun","dappledshadow","heathaze","drydust"],
  rain:["hardsun","dappledshadow","heathaze","drydust"],
  snow:["heathaze","drydust"],
  fog:["hardsun","hardshadow","dappledshadow","heathaze","drydust"]
};
const WEATHER_ADDITIONAL_CONFLICTS={
  clear:["rainStreaks","snowFlurry"],
  cloudy:["rainStreaks","snowFlurry"],
  drizzle:["snowFlurry"],
  rain:["snowFlurry"],
  snow:["rainStreaks"],
  fog:["rainStreaks","snowFlurry"]
};
const DETAIL_EFFECT_CONFLICTS=["softfocus","motionblur"];
function effectsConflict(a,b){return(EFFECT_CONFLICTS[a]||[]).includes(b)||(EFFECT_CONFLICTS[b]||[]).includes(a)}
function filmConflictsWithEffect(filmKey,effectKey){return(FILM_EFFECT_CONFLICTS[filmKey]||[]).includes(effectKey)}
function weatherConflictsWithEffect(weatherKey,effectKey){return(WEATHER_EFFECT_CONFLICTS[weatherKey]||[]).includes(effectKey)}
function weatherConflictsWithAdditional(weatherKey,elementKey){return(WEATHER_ADDITIONAL_CONFLICTS[weatherKey]||[]).includes(elementKey)}
function effectLabel(key){const item=EFFECTS.find(x=>x.key===key);return item?item.label:key}
function filmLabel(key){const item=FILM_TONES.find(x=>x.key===key);return item?item.label:key}
function weatherLabel(key){const item=WEATHER_OPTIONS.find(x=>x.key===key);return item?item.label:key}
function additionalElementLabel(key){const item=ADDITIONAL_ELEMENTS.find(x=>x.key===key);return item?item.label:key}
function getEffectDisabledReason(effectKey){
  if(filmConflictsWithEffect(state.film,effectKey))return`「${filmLabel(state.film)}」とは相性が悪いため選択不可です。`;
  if(weatherConflictsWithEffect(state.weather,effectKey))return`天気「${weatherLabel(state.weather)}」とは両立しないため選択不可です。`;
  if(state.closeupTexture==="detailed"&&DETAIL_EFFECT_CONFLICTS.includes(effectKey))return`「🔬 高精細」と同時に使うと細部が弱くなるため選択不可です。`;
  const conflictKey=state.effects.find(selected=>selected!==effectKey&&effectsConflict(selected,effectKey));
  return conflictKey?`選択中の「${effectLabel(conflictKey)}」とは相性が悪いため選択不可です。`:"";
}
function getAdditionalElementDisabledReason(elementKey){
  if(weatherConflictsWithAdditional(state.weather,elementKey))return`天気「${weatherLabel(state.weather)}」とは両立しないため選択不可です。`;
  return"";
}
function isThirdPersonOnlyAngle(itemKey){
  return ["tableLeanForwardBothElbows","counterLeanForwardBothElbows"].includes(itemKey);
}
function getAutoFallbackAngle(itemKey){
  const map={
    tableLeanForwardBothElbows:"tableLeanForwardOneElbow",
    counterLeanForwardBothElbows:"counterLeanForwardOneElbow"
  };
  return map[itemKey]||"auto";
}
function sanitizeAngleForSelfieMode(){
  if(state.selfieMode==="on" && isThirdPersonOnlyAngle(state.angleMode)){
    state.angleMode=getAutoFallbackAngle(state.angleMode);
  }
}
const SCENE_CUE_WORDS={
  table:["テーブル","食卓","机","卓上","table","desk"],
  counter:["カウンター","バーカウンター","counter","bar counter"],
  oneElbow:["片肘","片ひじ","片前腕","一方の肘","one elbow","one forearm"],
  bothElbows:["両肘","両ひじ","両前腕","both elbows","both forearms"],
  leanForward:["前傾","前かがみ","前屈","身を乗り出","体を前に倒","上体を前に倒","lean forward","leans forward","leaning forward"],
  lowPose:["しゃが","屈ん","かがん","座り込","床に座","地面に座","床へ座","地面へ座","膝をつ","膝立ち","四つん這","crouch","squat","kneel","sit on the floor","sitting on the floor","sit on the ground","sitting on the ground"],
  legForward:["片脚を前","片足を前","脚を前","足を前","片脚を伸ば","片足を伸ば","脚を伸ば","足を伸ば","前脚","足先をカメラ","足先をレンズ","脚をカメラ","足をカメラ","脚をレンズ","足をレンズ","脚が手前","足が手前","カメラの前へ脚","カメラの前に脚","カメラの前へ伸ば","カメラの前に伸ば","レンズの前へ伸ば","レンズの前に伸ば","leg toward the camera","foot toward the camera","leg toward the lens","foot toward the lens","foreground leg","foreground foot","extend one leg","extends one leg"],
  drink:["飲み物","飲料","ドリンク","飲んで","飲む","コーヒー","珈琲","紅茶","お茶","ジュース","ソーダ","ミネラルウォーター","ワイン","ビール","カクテル","お酒","グラス","カップ","マグ","ボトル","drink","drinking","coffee","tea","juice","soda","wine","beer","cocktail","glass","cup","mug","bottle"],
  food:["食べ物","料理","食事","食べて","食べる","ご飯","朝食","昼食","夕食","ランチ","ディナー","パン","ケーキ","スイーツ","デザート","皿","プレート","パスタ","サラダ","food","meal","eating","dish","plate","breakfast","lunch","dinner","bread","cake","dessert","pasta","salad"],
  turnBack:["振り向","振り返","後ろを見る","肩越し","look back","looks back","turn back","turns back","over the shoulder"],
  walking:["歩く","歩いて","歩き","歩行","散歩","walk","walking","stroll","strolling"],
  motion:["手を振","振り向","振り返","歩く","歩いて","歩き","走る","走って","踊る","踊って","ジャンプ","跳ぶ","回る","ひねる","風","髪が舞","髪が揺","服が揺","動いて","動きながら","勢い","反動","wave","waving","turn","walk","walking","run","running","dance","dancing","jump","jumping","spin","spinning","twist","twisting","wind","moving","motion"],
  strongMotion:["強風","激しく","大きく舞","勢いよく","全力","走る","走って","ジャンプ","跳ぶ","踊る","踊って","回転","振り回","強く手を振","大きく手を振","反動","strong wind","hair flying","run","running","jump","jumping","dance","dancing","spin","spinning","energetic","vigorous"]
};
const TABLETOP_FOCUS_KEYS=new Set(["subjectDrink","subjectFood","subjectTabletop"]);
const TABLETOP_COMPATIBLE_RANGES=new Set(["balanced","upperBody","waistUp","fullBody"]);
function isTabletopVisualFocus(itemKey=state.visualFocus){return TABLETOP_FOCUS_KEYS.has(itemKey)}
function sanitizeBackgroundViewForVisualFocus(){
  if(isTabletopVisualFocus())state.backgroundView="none";
}
function getSceneTextRaw(){return document.getElementById("situation")?.value||""}
function normalizedSceneText(){return getSceneTextRaw().normalize("NFKC").toLowerCase()}
function sceneHasCue(name){const scene=normalizedSceneText();return (SCENE_CUE_WORDS[name]||[]).some(word=>scene.includes(String(word).normalize("NFKC").toLowerCase()))}
function effectiveSelfieForCurrentScene(){return effectiveSelfie(getSceneTextRaw())}
function getSceneLinkedDisabledReason(key,itemKey){
  if(key==="angleMode"){
    if(itemKey==="groundLegToFaceSelfie"){
      if(effectiveSelfieForCurrentScene()!=="on")return"この角度は手持ち自撮り専用です。撮影方式を自撮りONにし、シーン文を第三者撮影にしないでください。";
      if(!sceneHasCue("lowPose")||!sceneHasCue("legForward"))return"シーン欄に『しゃがむ／床に座る等の低い姿勢』と『片脚・足をカメラ手前へ出す』の両方が必要です。";
      if(state.visibleRange!=="fullBody")return"前景の脚から顔まで写すため、写す範囲を『全身』にしてください。";
    }
    if(itemKey==="tableLeanForwardOneElbow"&&(!sceneHasCue("table")||!sceneHasCue("oneElbow")||!sceneHasCue("leanForward")))return"シーン欄に『テーブル』『片肘／片前腕』『少し前傾』の3要素が必要です。";
    if(itemKey==="counterLeanForwardOneElbow"&&(!sceneHasCue("counter")||!sceneHasCue("oneElbow")||!sceneHasCue("leanForward")))return"シーン欄に『カウンター』『片肘／片前腕』『少し前傾』の3要素が必要です。";
    if(itemKey==="tableLeanForwardBothElbows"){
      if(effectiveSelfieForCurrentScene()==="on")return"両肘つき前傾は手持ち自撮りでは成立しません。第三者撮影に切り替えてください。";
      if(!sceneHasCue("table")||!sceneHasCue("bothElbows")||!sceneHasCue("leanForward"))return"シーン欄に『テーブル』『両肘／両前腕』『少し前傾』の3要素が必要です。";
    }
    if(itemKey==="counterLeanForwardBothElbows"){
      if(effectiveSelfieForCurrentScene()==="on")return"両肘つき前傾は手持ち自撮りでは成立しません。第三者撮影に切り替えてください。";
      if(!sceneHasCue("counter")||!sceneHasCue("bothElbows")||!sceneHasCue("leanForward"))return"シーン欄に『カウンター』『両肘／両前腕』『少し前傾』の3要素が必要です。";
    }
    if(itemKey==="overShoulder"&&!sceneHasCue("turnBack"))return"シーン欄に『振り向く／振り返る／肩越し』などの動作が必要です。";
    if(itemKey==="walking"&&!sceneHasCue("walking"))return"シーン欄に『歩く／歩いている／散歩』などの動作が必要です。";
  }
  if(key==="visualFocus"){
    if(itemKey==="subjectDrink"&&!sceneHasCue("drink"))return"シーン欄に飲み物・カップ・グラスなどの記述が必要です。";
    if(itemKey==="subjectFood"&&!sceneHasCue("food"))return"シーン欄に食べ物・料理・食事などの記述が必要です。";
    if(itemKey==="subjectTabletop"&&!sceneHasCue("table")&&!sceneHasCue("counter"))return"シーン欄にテーブルまたはカウンターの記述が必要です。";
    if(TABLETOP_FOCUS_KEYS.has(itemKey)&&!TABLETOP_COMPATIBLE_RANGES.has(state.visibleRange))return"顔とテーブル上を同時に見せるため、写す範囲を『バランス／上半身／腰上／全身』のいずれかにしてください。";
  }
  if(key==="motionEnergy"){
    if(itemKey==="natural"&&!sceneHasCue("motion"))return"シーン欄に歩く・振り向く・手を振る・風・髪が舞う等の動きが必要です。";
    if(itemKey==="strong"&&!sceneHasCue("strongMotion"))return"シーン欄に強風・走る・ジャンプ・大きく舞う等の強い動きが必要です。";
  }
  if(key==="visibleRange"){
    if(state.angleMode==="groundLegToFaceSelfie"&&itemKey!=="fullBody")return"選択中の『地面付近・前脚→顔ライン自撮り』は、前景の脚を切らない『全身』だけ使用できます。";
    if(TABLETOP_FOCUS_KEYS.has(state.visualFocus)&&!TABLETOP_COMPATIBLE_RANGES.has(itemKey))return"選択中の表現の主役では顔とテーブル上を同時に見せるため、この写す範囲は使用できません。";
  }
  if(key==="backgroundView"&&isTabletopVisualFocus()&&itemKey!=="none"){
    return"『被写体＋飲み物／食べ物／テーブル上』では、テーブル周辺を表現の主役側で制御するため、背景の見せ方は『指定なし』に固定されます。";
  }
  return"";
}
function getSingleChipDisabledReason(key,itemKey){
  if(key==="closeupTexture"&&itemKey==="detailed"){
    const conflictKey=state.effects.find(effectKey=>DETAIL_EFFECT_CONFLICTS.includes(effectKey));
    if(conflictKey)return`選択中の「${effectLabel(conflictKey)}」とは両立しないため選択不可です。`;
  }
  const sceneReason=getSceneLinkedDisabledReason(key,itemKey);
  if(sceneReason)return sceneReason;
  return"";
}
function sanitizeEffectsForFilm(){state.effects=state.effects.filter(key=>!filmConflictsWithEffect(state.film,key))}
function sanitizeEffectsForWeather(){state.effects=state.effects.filter(key=>!weatherConflictsWithEffect(state.weather,key))}
function sanitizeAdditionalElementsForWeather(){state.additionalElements=state.additionalElements.filter(key=>!weatherConflictsWithAdditional(state.weather,key))}

const SKIN_FINISH_OPTIONS=[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(real skin texture:1.82), (natural skin finish:1.8), (balanced skin sheen:1.74)"),opt("💧 しっとり","moist","(soft moisturized skin finish:1.82), (subtle healthy skin sheen:1.78), (supple hydrated skin appearance:1.76)"),opt("✨ ツヤあり","dewy","(noticeable dewy skin finish:1.84), (soft glossy highlights on skin:1.8), (healthy luminous skin sheen:1.78)")];
const CLOSEUP_TEXTURE_OPTIONS=[opt("🎲 おまかせ","auto",""),opt("🌿 自然","natural","(natural realistic close-up detail balance:1.78), (skin detail clear without overprocessing:1.76)"),opt("💧 しっとり","moist","(close-up skin looks softly moisturized and realistic:1.82), (lips and skin retain subtle hydrated softness:1.78)"),opt("🔬 高精細","detailed","(high-detail close-up rendering of eyelashes, lips, pores, and fine skin texture:1.86), (macro-like facial detail while keeping realism:1.84)")];
const SELFIE_MODE_OPTIONS=[opt("🎲 自動 / おまかせ","auto","auto"),opt("🤳 自撮り ON","on","on"),opt("📷 自撮り OFF / 第三者撮影","off","off")];
const ANGLES=[
opt("🎲 おまかせ","auto","auto","シーン・写す範囲・撮影方式から、成立しやすい完成アングルを自動選択します。"),
opt("⬇️ 頭の真上から","trueTopDown","(camera is centered directly above the crown of the head:2.0), (true 90-degree vertical top-down optical axis:2.0), (the crown and upper surfaces are closest to the lens while the floor directly below remains geometrically coherent:1.96), (do not reinterpret this as an oblique high angle, eye-level view, or low angle:2.0), "+CHIN_CONTROL,"被写体の頭頂真上にカメラを置き、光軸を垂直下向きにした90度俯瞰です。斜め俯瞰ではありません。"),
opt("🙆 頭上・斜め俯瞰","overhead","(camera is above the subject and slightly forward rather than directly over the crown:1.96), (oblique overhead optical axis looks diagonally downward at the face, shoulders, outfit, and nearby floor or surface:1.94), (clear high-position perspective without becoming a true 90-degree top-down view:1.92), (do not normalize this to eye level:1.96), "+CHIN_CONTROL,"頭上の少し前方から斜め下へ見る俯瞰です。頭頂真上の90度俯瞰とは分けています。"),
opt("⬆️ 少し上から","high","(camera is clearly but moderately above eye level:1.9), (optical axis angles gently downward toward the face:1.88), (facial proportions remain natural with mild high-angle perspective:1.86), (do not raise the camera into an overhead view:1.9), "+CHIN_CONTROL,"目線より少し高い位置から、顔へ緩く見下ろす自然な高角度です。"),
opt("✨ 盛れ角","golden","(camera is slightly above eye level and subtly off the facial centerline:1.92), (mild downward optical axis and flattering three-dimensional facial presentation:1.88), (close but ordinary selfie or portrait distance:1.84), (not overhead, not eye-level flat, and not low-angle:1.9), "+CHIN_CONTROL,"目線より少し上かつ中心からわずかに外した、顔を自然に立体的に見せる完成角度です。"),
opt("👁️ 目線","eye","(camera is at the subject's eye height:1.92), (optical axis is approximately level toward the face:1.88), (natural portrait distance with minimal vertical perspective distortion:1.84), (do not tilt the viewpoint into a high or low angle:1.92), "+CHIN_CONTROL,"目の高さから水平に近い光軸で撮る、基準となる自然な人物角度です。"),
opt("☕ テーブル高さ・片肘つき前傾","tableLeanForwardOneElbow","(camera is positioned around tabletop height in front of the seated subject:1.96), (one elbow or forearm is physically supported by the table while the upper body leans slightly forward:1.94), (face, shoulders, supporting arm, table edge, and relevant tabletop elements remain spatially coherent:1.9), (when selfie mode is active, the other hand remains available to operate the smartphone:1.94), (do not replace this with a standing portrait or raised high-angle selfie:1.96), "+CHIN_CONTROL,"テーブル高さの視点と、片肘または片前腕を支点にした軽い前傾を一体化した完成構図です。"),
opt("🍸 カウンター高さ・片肘つき前傾","counterLeanForwardOneElbow","(camera is positioned around bar-counter height in front of the seated subject:1.96), (one elbow or forearm is physically supported by the counter while the upper body leans slightly forward:1.94), (face, shoulders, supporting arm, counter edge, and relevant objects remain spatially coherent:1.9), (when selfie mode is active, the other hand remains available to operate the smartphone:1.94), (do not replace this with a standing portrait or raised high-angle selfie:1.96), "+CHIN_CONTROL,"カウンター高さの視点と、片肘または片前腕を支点にした軽い前傾を一体化した完成構図です。"),
opt("☕ テーブル高さ・両肘つき前傾","tableLeanForwardBothElbows","(camera is positioned around tabletop height in front of the seated subject:1.96), (both elbows or forearms are physically supported by the table:1.96), (the upper body leans slightly forward with stable seated balance:1.94), (face, shoulders, arms, table edge, and relevant tabletop elements remain spatially coherent:1.9), (this completed pose requires non-selfie or third-person capture:2.0), "+CHIN_CONTROL,"テーブル高さから、両肘または両前腕を支点にして少し前傾する第三者撮影向け完成構図です。"),
opt("🍸 カウンター高さ・両肘つき前傾","counterLeanForwardBothElbows","(camera is positioned around bar-counter height in front of the seated subject:1.96), (both elbows or forearms are physically supported by the counter:1.96), (the upper body leans slightly forward with stable seated balance:1.94), (face, shoulders, arms, counter edge, and relevant objects remain spatially coherent:1.9), (this completed pose requires non-selfie or third-person capture:2.0), "+CHIN_CONTROL,"カウンター高さから、両肘または両前腕を支点にして少し前傾する第三者撮影向け完成構図です。"),
opt("⬇️ 低め前持ち","lowFront","(camera is held in front of the body around lower-chest to upper-waist height:1.92), (a small visible gap remains between the lens and torso:1.86), (optical axis angles mildly upward toward the face:1.9), (perspective is clearly lower than eye level but not body-adjacent or extreme:1.88), (do not turn this into a high-angle selfie or hidden waist-held shot:1.94), "+CHIN_CONTROL,"身体の前方に少し離して持つ、軽いローアングルです。身体密着の体沿い構図ではありません。"),
opt("🤫 腰だめ","hiddenWaist","(camera is held discreetly at waist or lower-torso height and close to the body:2.0), (the camera-holding elbow stays bent, low, and close to the torso:2.0), (optical axis angles upward toward the face with moderate close-body perspective:1.94), (the arm is not extended outward and the phone is not raised toward the face:2.0), (do not convert this into an ordinary arm's-length selfie:2.0), "+CHIN_CONTROL,"腰付近で目立たないように保持し、短く畳んだ腕で顔へ煽る隠し持ち型の完成アングルです。"),
opt("📉 腰位置・身体沿い強煽り","waistSideLow","(camera line begins at waist-to-upper-hip height and follows the visible torso toward the chest, neck, and face:2.0), (strong close-body upward perspective remains less extreme than the waist-below presets:1.94), (the selected front, diagonal, or side relationship must not drift into an ordinary low portrait:2.0), "+CHIN_CONTROL,"腰〜上ヒップ付近を起点に、身体の見えるラインへ沿って顔まで強く見上げる近接アングルです。共通の身体沿い距離ロックが適用されます。"),
opt("📉 腰下・正面沿い超強煽り","lowerBodyExtremeFront","(camera line begins around the lower waist to upper thigh on the front body centerline:2.0), (optical axis travels upward along the front torso, chest, neck, and face:2.0), (front body alignment remains unmistakable and must not drift into a diagonal or side direction:2.0), (extreme near-to-far expansion is mandatory:1.98), "+CHIN_CONTROL,"腰下〜上腿の正面ラインを起点に、腹部・胸・首・顔へ一直線に見上げる方向プリセットです。共通の超近接距離ロックが適用されます。"),
opt("📉 腰下・斜め沿い超強煽り","lowerBodyExtremeThreeQuarter","(camera line begins around the lower waist to upper thigh on a front three-quarter body direction:2.0), (optical axis travels diagonally upward through torso, near shoulder, neck, and face:2.0), (front plane and side contour remain simultaneously readable:1.98), (do not flatten this to frontal or rotate it to a true side direction:2.0), "+CHIN_CONTROL,"腰下〜上腿の斜め前ラインを起点に、腰・胴体・肩・首・顔へ斜めに見上げる方向プリセットです。共通の超近接距離ロックが適用されます。"),
opt("📉 腰下・真横沿い超強煽り","lowerBodyExtremeSide","(camera line begins around the lower waist to upper thigh on the true side body direction:2.0), (optical axis travels upward along the lateral torso, shoulder, neck, and face:2.0), (the side body line remains unmistakably readable:1.98), (do not rotate the camera toward a front three-quarter direction:2.0), "+CHIN_CONTROL,"腰下〜上腿の真横ラインを起点に、脇腹・体側・肩・首・顔へ見上げる方向プリセットです。共通の超近接距離ロックが適用されます。"),
opt("📉 腰下・正面沿い超強煽り・低いカメラを覗き込む","lowerBodyExtremeFrontLookDown","(camera line begins around the lower waist to upper thigh on the front body centerline:2.0), (optical axis travels upward along the front torso toward the face:2.0), (torso remains front-oriented and the camera must stay low:2.0), (do not lift the camera or rotate the torso to make eye contact easier:2.0), (chin not thrust forward:1.92), (neck relaxed and not compressed:1.9)","正面沿い超近接構図を維持し、顔向き・顎・視線は角度専用の『低いカメラを覗き込む』ロックで自動制御します。"),
opt("📉 腰下・斜め沿い超強煽り・低いカメラを覗き込む","lowerBodyExtremeThreeQuarterLookDown","(camera line begins around the lower waist to upper thigh on a front three-quarter body direction:2.0), (optical axis travels diagonally upward through torso and near shoulder toward the face:2.0), (torso preserves the selected three-quarter direction and the camera must stay low:2.0), (do not rotate the full torso frontward or lift the camera to make eye contact easier:2.0), (chin not thrust forward:1.92), (neck relaxed and not compressed:1.9)","斜め沿い超近接構図を維持し、顔向き・顎・視線は角度専用の『低いカメラを覗き込む』ロックで自動制御します。"),
opt("📉 腰下・真横沿い超強煽り・低いカメラを覗き込む","lowerBodyExtremeSideLookDown","(camera line begins around the lower waist to upper thigh on the true side body direction:2.0), (optical axis travels upward along the lateral torso toward the face:2.0), (torso remains side-oriented and the camera must stay low:2.0), (do not rotate the full body to a frontal or three-quarter pose and do not lift the camera:2.0), (chin not thrust forward:1.92), (neck relaxed and not compressed:1.9)","真横沿い超近接構図を維持し、胴体は横向きのまま、顔向き・顎・視線は角度専用の『低いカメラを覗き込む』ロックで自動制御します。"),
opt("📉 離れた位置から強い煽り","superLow","(camera is clearly below waist level and separated from the subject by a visible shooting distance:1.94), (optical axis looks strongly upward toward the torso and face:1.94), (sky, ceiling, or tall architecture may expand behind the subject:1.88), (this is a dramatic low-angle portrait but not a body-adjacent camera position:2.0), (do not normalize it to eye level or confuse it with the close body-line presets:2.0), "+CHIN_CONTROL,"身体から少し離れた低い位置から全体を強く見上げる一般的な強煽りです。身体沿い近接とは分けています。"),
opt("📉 地面付近・前脚→顔ライン自撮り","groundLegToFaceSelfie","(the subject's active smartphone is handheld near ground level:2.0), (a foot or leg explicitly established by the written scene forms the nearest foreground:2.0), (optical axis follows a continuous near-to-far line from the foreground leg through the torso toward the face:2.0), (face remains visible at the far end of the perspective line:1.96), (joints, ground contact, body support, and handheld reach remain physically coherent:1.96), (do not invent the required low pose or foreground leg when absent from the scene:2.0), (do not convert this into a timer shot, third-person view, or ordinary standing low angle:2.0), "+CHIN_CONTROL,"シーン欄に書かれた低い姿勢と前景脚を使い、地面付近の手持ちスマホから脚→胴体→顔の遠近ラインを作る専用自撮りです。"),
opt("➡️ 真横から","side","(camera is positioned at the subject's true side with ordinary portrait distance:1.92), (optical axis reads the lateral face and body line without frontward drift:1.9), (side-profile or near-profile geometry remains clear:1.88), (do not rotate to a front three-quarter view:1.94), "+CHIN_CONTROL,"被写体から通常距離を取り、身体と顔の側面を読む真横視点です。身体密着の真横沿いとは別です。"),
opt("↩️ 振り向き","overShoulder","(camera is positioned behind or rear-three-quarter to the subject:1.92), (shoulder and back direction lead toward a face looking back:1.9), (the turn-back geometry remains readable rather than becoming a frontal portrait:1.9), (camera position and the written turning action remain physically coherent:1.88), "+CHIN_CONTROL,"後方または斜め後方のカメラへ、肩越しに振り向く動作を含んだ完成構図です。"),
opt("🚶 歩き","walking","(camera captures the subject during the written walking action:1.9), (camera position tracks or observes the subject without freezing the body into a static standing pose:1.86), (step phase, arm swing, hair, and garment movement remain physically coherent:1.84), (the chosen shooting mode determines whether the viewpoint moves with the subject or comes from an external camera:1.88), "+CHIN_CONTROL,"歩行途中の身体バランスとカメラの追従を含む、動作付きの完成撮影構図です。"),
opt("◢ 斜め前から","tilted","(camera is positioned at an ordinary front three-quarter direction relative to the subject:1.9), (both the front plane and one side contour remain readable:1.88), (camera height remains natural unless another completed preset is selected:1.84), (this controls camera direction, not image-plane roll:2.0), "+CHIN_CONTROL,"被写体の斜め前から正面と側面を同時に見せる方向プリセットです。画面の傾きとは別です。")
];

const ANGLE_PRESET_GROUPS=[
  {key:"high",label:"⬆️ 高い位置・見下ろし",note:"真上、斜め俯瞰、少し上、盛れ角。",items:["trueTopDown","overhead","high","golden"]},
  {key:"standard",label:"👁️ 標準・前方",note:"目線、低め前持ち。自然な正面基準。",items:["eye","lowFront"]},
  {key:"table",label:"☕ テーブル・カウンター",note:"撮影面の高さと肘の支え、軽い前傾を含む完成構図。",items:["tableLeanForwardOneElbow","counterLeanForwardOneElbow","tableLeanForwardBothElbows","counterLeanForwardBothElbows"]},
  {key:"waist",label:"🤫 腰位置・身体近く",note:"腰だめと、腰位置から身体に沿う強煽り。",items:["hiddenWaist","waistSideLow"]},
  {key:"bodyAdjacent",label:"📉 腰下・身体沿い超強煽り",note:"正面・斜め・真横 × 通常／低いカメラを覗き込む。身体表面すぐ近くの距離を固定。",items:["lowerBodyExtremeFront","lowerBodyExtremeThreeQuarter","lowerBodyExtremeSide","lowerBodyExtremeFrontLookDown","lowerBodyExtremeThreeQuarterLookDown","lowerBodyExtremeSideLookDown"]},
  {key:"ground",label:"⬇️ 地面寄り・強い遠近",note:"身体から離れた強煽りと、前脚→顔ラインの専用自撮り。",items:["superLow","groundLegToFaceSelfie"]},
  {key:"direction",label:"↔️ 横・斜め・動作構図",note:"真横、振り向き、歩き、斜め前。",items:["side","overShoulder","walking","tilted"]}
];
const BODY_ADJACENT_ANGLE_KEYS=new Set(["waistSideLow","lowerBodyExtremeFront","lowerBodyExtremeThreeQuarter","lowerBodyExtremeSide","lowerBodyExtremeFrontLookDown","lowerBodyExtremeThreeQuarterLookDown","lowerBodyExtremeSideLookDown"]);
const EXTREME_BODY_ADJACENT_ANGLE_KEYS=new Set(["lowerBodyExtremeFront","lowerBodyExtremeThreeQuarter","lowerBodyExtremeSide","lowerBodyExtremeFrontLookDown","lowerBodyExtremeThreeQuarterLookDown","lowerBodyExtremeSideLookDown"]);
const BODY_REFERENCE_FRONT_ANGLE_KEYS=new Set(["eye","lowFront","hiddenWaist","tableLeanForwardOneElbow","counterLeanForwardOneElbow","tableLeanForwardBothElbows","counterLeanForwardBothElbows","lowerBodyExtremeFront","lowerBodyExtremeFrontLookDown","superLow","groundLegToFaceSelfie"]);
const BODY_REFERENCE_THREE_QUARTER_ANGLE_KEYS=new Set(["tilted","overShoulder","lowerBodyExtremeThreeQuarter","lowerBodyExtremeThreeQuarterLookDown"]);
const BODY_REFERENCE_PROFILE_ANGLE_KEYS=new Set(["side","lowerBodyExtremeSide","lowerBodyExtremeSideLookDown"]);

const VISIBLE_RANGE_OPTIONS=[opt("⚖️ バランス","balanced","(balanced portrait composition with face, upper body, and believable context:1.82)"),opt("🙂 顔のみ","faceOnly","(face-only portrait crop:1.92), (only the face is the image subject:1.9), (crop from slightly above forehead to around chin or just above neck:1.88), (shoulders, chest, outfit, and background are minimal:1.86)"),opt("🧿 顔どアップ","extremeFace","(extreme face close-up composition:1.98), (face fills almost the entire frame:1.96), (eyes, lips, skin texture, and hairline dominate:1.9), (background barely visible:1.86)"),opt("🔍 顔アップ","faceCloseup","(close-up face composition:1.92), (face fills most of the frame:1.9), (hair, neck, and slight shoulder may appear:1.82)"),opt("↔️ 横顔アップ","profileCloseup","(profile close-up composition:1.94), (side face line, eye, nose bridge, lips, and cheek contour clearly readable:1.9)"),opt("🙂 顔〜肩","headShoulder","(head-and-shoulders portrait framing:1.88), (face, hair, neck, and shoulders are visible:1.86)"),opt("🧥 上半身","upperBody","(upper-body portrait composition:1.88), (head to chest or waist area visible:1.86), (face and outfit both readable:1.86)"),opt("🧍 腰上","waistUp","(waist-up portrait framing:1.92), (head to waist or upper-hip area visible:1.9), (face, body line, and outfit coordination readable:1.88)"),opt("🧍 全身","fullBody","(full-body portrait framing:1.88), (entire outfit and standing balance visible:1.86), (face remains readable but body and clothing are important:1.82)")];
const CAMERA_ROLL_OPTIONS=[opt("🎲 おまかせ","auto","natural camera roll chosen to suit the scene; keep the frame visually stable unless a tilt improves the snapshot"),opt("📐 水平","level","level camera roll; background horizontal lines remain horizontal and vertical architectural lines remain vertical"),opt("／ 少し斜め","slight","visible 6–10 degree camera roll; the entire frame, background horizontal lines, and architectural verticals share the same mild diagonal rotation; keep the selected viewpoint and crop unchanged"),opt("／／ 斜め強め","strong","clearly visible 15–22 degree camera roll; the entire image plane and all background structural lines are intentionally rotated together; preserve the selected viewpoint, crop, and subject pose")];
const FACE_DIRECTION_OPTIONS=[opt("🎲 おまかせ","auto","(face orientation is naturally derived from scene and selected angle:1.74)"),opt("🙂 正面","front","(front-facing or near-front facial orientation:1.84)"),opt("◢ 斜め向き","threeQuarter","(three-quarter facial angle:1.86), (face turned about 20 to 45 degrees from camera:1.82)"),opt("➡️ 横顔","profile","(true side-profile or near-profile facial orientation:1.9), (lateral face line clearly readable:1.86)"),opt("↩️ 振り向き","turnBack","(looking back over shoulder or gentle turned-back facial orientation:1.9)"),opt("🙈 顔を見せない","away","(face turned away and not presented to camera:1.92)")];
const GAZE_OPTIONS=[opt("🎲 おまかせ","auto","(gaze naturally derived from scene, emotion, and angle:1.72)"),opt("👀 カメラ目線","camera","(eyes naturally meet the lens:1.84), (clear camera-aware gaze:1.82)"),opt("↗️ 少し視線を外す","off","(gaze is slightly off-camera:1.84), (natural off-axis eye line:1.8)"),opt("🌌 遠くを見る","far","(gaze directed into the distance, not at camera:1.86)"),opt("😌 伏し目","down","(downward or lowered gaze:1.84), (soft eyelids and lowered eye line:1.82)")];
const BACKGROUND_VIEW_MODES=[opt("🚫 指定なし","none",""),opt("🫧 控えめ","subtle","(background remains secondary and understated:1.7), (subject stays visually dominant over background:1.8)"),opt("🌆 バランス","balanced","(background shown in a balanced natural way:1.75), (subject and place both readable:1.75)"),opt("🌸 下 / 足元側","lower","(lower background is visible when framing allows:1.78), (ground, pavement, floor, or lower-side details support the scene:1.74)"),opt("☕ 奥","depth","(depth background behind the subject clearly visible:1.78), (show the lobby, street, storefront, or scenery behind the subject:1.76)"),opt("🌙 上","upper","(upper background visible when framing allows:1.78), (show ceiling, signs, sky, or upper building area:1.74)")];
const FRAMING_MODES=[opt("🎲 AUTO / 主役に連動","auto",""),opt("⚖️ 標準","standard","(balanced subject scale with moderate breathing room:1.7), (natural crop with some surrounding space:1.7)"),opt("🧍 余白少なめ","tight","(tight framing with reduced empty space:1.8), (subject occupies most of the frame:1.8)"),opt("🖼️ 余白なし / 被写体いっぱい","full","(little to no leading space:1.9), (subject fills the image as much as possible:1.9), (minimal empty background:1.86)"),opt("🏙️ 余白あり / 場所も見せる","wide","(clear breathing room around the subject:1.78), (environment intentionally readable:1.78)")];
const PHOTO_STYLE_MODES=[
  opt("📱 ラフなスナップ","amateur","(unpolished everyday photograph with believable minor imperfections:1.88), (casual framing and natural phone or camera auto-exposure:1.84), (no professional staging or excessive beautification:1.84)"),
  opt("📷 自然な日常写真","natural","(real everyday photograph with candid daily-life realism:1.86), (natural expression, posture, exposure, and framing:1.82), (slight imperfection remains believable:1.76)"),
  opt("🙂 軽く整えた写真","polished","(lightly polished but still believable portrait presentation:1.84), (composition, light, and expression are gently refined without losing everyday realism:1.82), (no excessive production:1.8)"),
  opt("🎥 明確に演出した写真","directed","(clearly directed photographic presentation:1.86), (intentional posing, lighting, and composition are visibly designed:1.84), (the image remains photographic rather than artificial:1.8)"),
  opt("🎬 作品撮り / 作り込み強め","produced","(strongly produced creative photo-shoot presentation:1.88), (deliberate lighting, color, composition, and visual staging:1.86), (finished image prioritizes authored visual impact:1.82)")
];
const VISUAL_FOCUS_OPTIONS=[
  opt("🎲 おまかせ","auto","(visual priority is derived naturally from the selected visible range, written scene, and composition:1.78)"),
  opt("🙂 人物主役","person","(the person is the primary visual subject:1.9), (face, expression, gaze, shoulder line, and body presence receive the strongest visual priority:1.86), (outfit and background support the person without competing for attention:1.82)"),
  opt("👗 服・コーデ主役","outfit","(the outfit and styling are the primary visual subject:1.9), (garment silhouette, material, color coordination, layering, bag, and accessories remain clearly readable:1.86), (do not crop so tightly that the selected outfit becomes unreadable:1.86)"),
  opt("🏙️ 背景・場所主役","environment","(the place and environment are a primary visual subject:1.9), (architecture, lighting, depth, reflections, and spatial atmosphere remain clearly readable:1.86), (the subject is physically integrated into the environment rather than isolated as a cutout:1.84)"),
  opt("☕ 被写体＋飲み物","subjectDrink","(the subject and the drink explicitly described or physically present in the written scene share primary visual emphasis:1.92), (the face, relevant hand, cup or glass, and their spatial relationship remain clearly readable:1.88), (include enough table or counter surface to anchor the drink naturally:1.84), (do not invent a drink when the written scene contains none:1.94)"),
  opt("🍽️ 被写体＋食べ物","subjectFood","(the subject and the food explicitly described or physically present in the written scene share primary visual emphasis:1.92), (the face, relevant hands, dish, and their spatial relationship remain clearly readable:1.88), (include enough tabletop surface for the meal to feel physically supported:1.86), (do not invent food when the written scene contains none:1.94)"),
  opt("🪑 被写体＋テーブル上","subjectTabletop","(the subject and the tabletop area explicitly described or physically present in the written scene share primary visual emphasis:1.92), (the face, hands, table edge, and relevant tabletop objects remain clearly readable together:1.88), (preserve believable object placement, support, scale, and reachability on the table or counter:1.88), (do not invent food, drinks, or tabletop objects that are not supported by the written scene:1.94)"),
  opt("⚖️ バランス","balanced","(person, outfit, and environment share balanced visual priority:1.86), (face, styling, and place are all sufficiently readable without one element overwhelming the others:1.84)")
];
const SHOOTING_PRESETS={
  selfieDaily:{selfieMode:"on",angleMode:"lowFront",visibleRange:"waistUp",cameraRoll:"slight",faceDirection:"auto",gaze:"camera",backgroundView:"balanced",framing:"auto",photoStyle:"natural",visualFocus:"balanced",motionEnergy:"subtle",effectStrength:"subtle",skinFinish:"natural",closeupTexture:"natural"},
  selfieModel:{selfieMode:"on",angleMode:"golden",visibleRange:"waistUp",cameraRoll:"slight",faceDirection:"threeQuarter",gaze:"camera",backgroundView:"subtle",framing:"auto",photoStyle:"polished",visualFocus:"person",motionEnergy:"subtle",effectStrength:"standard",skinFinish:"moist",closeupTexture:"natural"},
  selfieEditorial:{selfieMode:"on",angleMode:"tilted",visibleRange:"waistUp",cameraRoll:"slight",faceDirection:"threeQuarter",gaze:"off",backgroundView:"depth",framing:"auto",photoStyle:"directed",visualFocus:"outfit",motionEnergy:"natural",effectStrength:"strong",skinFinish:"natural",closeupTexture:"natural"},
  selfieCinematic:{selfieMode:"on",angleMode:"lowFront",visibleRange:"upperBody",cameraRoll:"strong",faceDirection:"threeQuarter",gaze:"off",backgroundView:"depth",framing:"auto",photoStyle:"produced",visualFocus:"environment",motionEnergy:"strong",effectStrength:"strong",skinFinish:"natural",closeupTexture:"natural"},
  thirdDaily:{selfieMode:"off",angleMode:"eye",visibleRange:"waistUp",cameraRoll:"auto",faceDirection:"auto",gaze:"off",backgroundView:"balanced",framing:"auto",photoStyle:"natural",visualFocus:"balanced",motionEnergy:"auto",effectStrength:"subtle",skinFinish:"natural",closeupTexture:"natural"},
  thirdPortrait:{selfieMode:"off",angleMode:"eye",visibleRange:"headShoulder",cameraRoll:"level",faceDirection:"threeQuarter",gaze:"camera",backgroundView:"subtle",framing:"auto",photoStyle:"polished",visualFocus:"person",motionEnergy:"subtle",effectStrength:"standard",skinFinish:"natural",closeupTexture:"natural"},
  thirdModel:{selfieMode:"off",angleMode:"eye",visibleRange:"waistUp",cameraRoll:"level",faceDirection:"threeQuarter",gaze:"off",backgroundView:"subtle",framing:"auto",photoStyle:"directed",visualFocus:"person",motionEnergy:"subtle",effectStrength:"standard",skinFinish:"natural",closeupTexture:"natural"},
  thirdEditorial:{selfieMode:"off",angleMode:"eye",visibleRange:"fullBody",cameraRoll:"slight",faceDirection:"threeQuarter",gaze:"off",backgroundView:"depth",framing:"auto",photoStyle:"directed",visualFocus:"outfit",motionEnergy:"natural",effectStrength:"strong",skinFinish:"natural",closeupTexture:"natural"},
  thirdCinematic:{selfieMode:"off",angleMode:"tilted",visibleRange:"waistUp",cameraRoll:"strong",faceDirection:"threeQuarter",gaze:"off",backgroundView:"depth",framing:"auto",photoStyle:"produced",visualFocus:"environment",motionEnergy:"strong",effectStrength:"strong",skinFinish:"natural",closeupTexture:"natural"}
};
const PRESET_CONTROLLED_KEYS=new Set(["selfieMode","angleMode","visibleRange","cameraRoll","faceDirection","gaze","backgroundView","framing","photoStyle","visualFocus","motionEnergy","effectStrength","skinFinish","closeupTexture"]);
const MOTION_ENERGY_OPTIONS=[
  opt("🎲 おまかせ","auto","(motion intensity is naturally derived from the written scene, action, posture, wind, and selected camera angle:1.82), (do not force either complete stillness or dramatic motion when the scene does not support it:1.8)","シーンの行動・姿勢・風・アングルに合わせて、落ち着きから動きのある瞬間まで自然に判断します。"),
  opt("🌿 わずかな自然な動き","subtle","(subtle natural motion appears in hair tips, clothing edges, shoulders, hands, or posture:1.84), (the subject remains mostly composed while avoiding a frozen mannequin-like pose:1.82), (motion follows the written action and physical support:1.82)","毛先・服の裾・肩・手元などに小さな動きを出します。大きな動作は強制しません。"),
  opt("💨 自然な躍動感","natural","(natural dynamic energy connects the hair, clothing, arms, shoulders, and upper-body movement:1.9), (capture a believable in-between moment rather than a rigid posed freeze:1.88), (hair and garment movement follow the subject's action, wind, inertia, and gravity:1.86), (keep anatomy and physical support coherent:1.86)","髪・服・腕・上体を連動させ、動作途中を自然に切り取ったような躍動感を出します。"),
  opt("⚡ 強い躍動感","strong","(strong dynamic energy is clearly visible through moving hair, clothing, limbs, body twist, or rebound:1.94), (capture a decisive high-energy instant with believable inertia and follow-through:1.92), (hair, fabric, ribbons, and accessories react consistently to motion and gravity:1.9), (do not add random wind or motion unrelated to the written scene:1.9), (preserve anatomy, support, and selected camera geometry:1.9)","髪が大きく舞う、身体がひねられる、服やアクセサリーが反動で動くなど、強い瞬間性を出します。")
];
const EXPRESSION_OPTIONS=[opt("🎲 自動","auto",""),opt("😐 真顔・自然","neutral","natural neutral expression, relaxed facial muscles, calm eyes, closed relaxed lips"),opt("🖤 無機質","blankGaze","emotionally unreadable expression, still face, minimal facial movement, controlled fashion-editorial gaze"),opt("😏 半目クール","halfLiddedCool","half-lidded eyes, cool detached gaze, relaxed eyelids, closed lips, calm self-possessed expression"),opt("😎 自信あり","confident","quiet confident expression, steady eyes, subtle lifted chin, composed closed-mouth confidence"),opt("😒 少し不機嫌","mildAnnoyed","slightly displeased expression, mildly narrowed eyes, restrained mouth tension, subtle irritation without exaggeration"),opt("🌫️ アンニュイ","ennui","ennui expression, distant unfocused gaze, relaxed mouth, quiet sophisticated detachment"),opt("😌 物憂げ","melancholic","soft melancholic expression, reflective eyes, restrained quiet sadness"),opt("😪 気だるげ","sleepy","sleepy tired expression, heavy relaxed eyelids, gentle quiet fatigue"),opt("😟 不安げ","anxious","subtle anxious expression, slightly tense brows, uncertain eyes, restrained worry"),opt("😳 驚き","surprised","natural mild surprise, widened eyes, slightly parted lips, believable spontaneous reaction"),opt("☺️ 照れ・はにかみ","shy","shy bashful expression, small restrained smile, softened eyes, modest downward tension"),opt("🙂 口角だけ微笑む","subtleSmile","very subtle closed-mouth smile, only the corners of the lips gently lifted, calm eyes"),opt("😊 優しい微笑み","smile","soft gentle closed-mouth smile, warm approachable eyes, relaxed cheeks"),opt("😄 明るい笑顔","happy","bright natural smile, cheerful eyes, lively approachable expression"),opt("😁 歯を見せた笑顔","toothySmile","natural open smile with visible teeth, lifted cheeks, friendly spontaneous happiness"),opt("😁 くしゃっと笑顔","crinkledSmile","big crinkled smile with visible teeth, cheeks strongly lifted, joyful face-scrunch expression"),opt("😆 目を細めた満面笑顔","squintingBigSmile","eyes narrowed by a genuine full smile, broad toothy grin, delighted expression"),opt("☀️ はしゃいだ笑顔","playfulSunnySmile","playful excited smile, open cheerful energy, bright delighted expression"),opt("🫶 無邪気な笑顔","innocentSmile","innocent unguarded smile, sparkling joy, naturally delighted approachable warmth"),opt("😂 笑い声が出る笑顔","laughing","genuine laughing expression, open smiling mouth, lifted cheeks, bright eyes, spontaneous candid joy"),opt("😆 めっちゃ嬉しそう","veryHappy","very happy joyful smile, bright expressive eyes, clearly delighted expression")];
const DEFAULT_STATE={characterMode:"on",outfitReferenceMode:"off",locationReferenceMode:"off",weather:"",film:"",tone:"",effects:[],effectStrength:"standard",additionalElements:[],skinFinish:"",closeupTexture:"",selfieMode:"auto",shootingPreset:"",visualFocus:"auto",angleMode:"auto",visibleRange:"balanced",cameraRoll:"auto",faceDirection:"auto",gaze:"auto",backgroundView:"none",framing:"auto",photoStyle:"natural",motionEnergy:"auto",expression:"",situation:""};
let state={...DEFAULT_STATE};
function getTokyoNow(){const now=new Date();const jst=new Date(now.toLocaleString("en-US",{timeZone:"Asia/Tokyo"}));const days=["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];const list=[{h:[0,5],label:"深夜",en:"late night",mood:"melancholic quiet solitude, exhausted calm"},{h:[5,9],label:"早朝",en:"early morning",mood:"serene fresh morning calm"},{h:[9,12],label:"午前",en:"late morning",mood:"composed focused morning clarity"},{h:[12,14],label:"昼",en:"noon",mood:"bright casual midday energy"},{h:[14,17],label:"午後",en:"afternoon",mood:"relaxed comfortable afternoon drift"},{h:[17,20],label:"夕方",en:"evening",mood:"warm golden-hour nostalgia"},{h:[20,23],label:"夜",en:"night",mood:"intimate night warmth"},{h:[23,24],label:"深夜",en:"midnight",mood:"deep night solitude"}];const hour=jst.getHours();const timeCtx=list.find(x=>hour>=x.h[0]&&hour<x.h[1])||list[0];return{month:jst.getMonth()+1,day:days[jst.getDay()],hour,minute:jst.getMinutes(),timeStr:jst.toLocaleTimeString("ja-JP",{hour:"2-digit",minute:"2-digit"}),timeCtx};}
function updateClock(){const t=getTokyoNow();document.getElementById("hTime").textContent=t.timeStr+" JST";document.getElementById("hDay").textContent=t.day+" · "+t.month+"月 · "+t.timeCtx.label;document.getElementById("infoDay").innerHTML="<span class='info-val'>"+t.day+" / "+t.month+"月 / "+t.timeCtx.label+"（"+t.timeCtx.en+"）</span>";document.getElementById("infoTime").innerHTML="<span class='info-val'>"+t.timeStr+" JST</span>";document.getElementById("infoDayMood").textContent=DAY_MOOD[t.day];document.getElementById("infoHair").innerHTML="<span class='info-val'>"+t.month+"月："+(HAIR_DISPLAY_BY_MONTH[t.month]||"未設定")+"</span>";}
function bindChipHelp(btn,item){if(!item.help)return;btn.classList.add("has-help");let timer=null,long=false;const start=ev=>{long=false;timer=setTimeout(()=>{long=true;showChipHelp(item.label,item.help);if(ev&&ev.cancelable)ev.preventDefault();},520)};const cancel=()=>{if(timer)clearTimeout(timer);timer=null};btn.addEventListener("touchstart",start,{passive:false});btn.addEventListener("touchend",cancel);btn.addEventListener("touchcancel",cancel);btn.addEventListener("mousedown",start);btn.addEventListener("mouseup",cancel);btn.addEventListener("mouseleave",cancel);btn.addEventListener("contextmenu",ev=>{ev.preventDefault();showChipHelp(item.label,item.help)});btn.addEventListener("click",ev=>{if(long){ev.preventDefault();ev.stopPropagation();long=false}},true)}
function showChipHelp(title,body){document.getElementById("chipHelpTitle").textContent=title.replace(/^[^\w一-龯ぁ-んァ-ヶ]+/u,"").trim()||title;document.getElementById("chipHelpBody").textContent=body;document.getElementById("chipHelpOverlay").classList.remove("hidden")}function hideChipHelp(){document.getElementById("chipHelpOverlay").classList.add("hidden")}
function getItems(key){return({characterMode:CHARACTER_MODE_OPTIONS,outfitReferenceMode:OUTFIT_REFERENCE_MODE_OPTIONS,locationReferenceMode:LOCATION_REFERENCE_MODE_OPTIONS,weather:WEATHER_OPTIONS,film:FILM_TONES,tone:OVERALL_TONES,effectStrength:EFFECT_STRENGTH_OPTIONS,skinFinish:SKIN_FINISH_OPTIONS,closeupTexture:CLOSEUP_TEXTURE_OPTIONS,selfieMode:SELFIE_MODE_OPTIONS,visualFocus:VISUAL_FOCUS_OPTIONS,angleMode:ANGLES,visibleRange:VISIBLE_RANGE_OPTIONS,cameraRoll:CAMERA_ROLL_OPTIONS,faceDirection:FACE_DIRECTION_OPTIONS,gaze:GAZE_OPTIONS,backgroundView:BACKGROUND_VIEW_MODES,framing:FRAMING_MODES,photoStyle:PHOTO_STYLE_MODES,motionEnergy:MOTION_ENERGY_OPTIONS,expression:EXPRESSION_OPTIONS})[key]||[]}
function find(key){return getItems(key).find(x=>x.key===state[key]||x.value===state[key])||getItems(key)[0]||{label:"",value:""}}
const FACE_DOMINANT_RANGES=new Set(["faceOnly","extremeFace","faceCloseup","profileCloseup"]);
function isFaceDominantRange(){return FACE_DOMINANT_RANGES.has(state.visibleRange)}
function resolvedBackgroundPrompt(){
  if(isFaceDominantRange())return "(background is only a minimal incidental fragment and must not compete with the face crop:1.96), (do not widen the composition to show the place, outfit, table, food, drink, or environmental context:2.0)";
  return find("backgroundView").value;
}
function resolvedVisualFocusPrompt(){
  if(isFaceDominantRange())return "(the visible face is the sole primary visual subject:2.0), (facial identity, facial proportions, eyes, nose, lips, cheeks, jaw, and expression receive complete composition priority:1.98), (outfit, body, background, location, food, drink, and tabletop content remain outside or incidental to the selected face crop:2.0)";
  return find("visualFocus").value;
}
function resolvedVisualFocusLabel(){
  return isFaceDominantRange()?"顔のみ優先（自動）":find("visualFocus").label;
}
function resolvedFramingPrompt(){
  if(isFaceDominantRange())return "(framing is strictly subordinate to the selected face crop:2.0), (do not add breathing room by revealing shoulders, chest, outfit, hands, table, or broad background beyond the selected visible range:2.0)";
  if(state.framing!=="auto")return find("framing").value;
  const byFocus={
    person:"(AUTO framing follows person priority:1.86), (the subject appears large with reduced but believable breathing room:1.84), (face and body presence remain dominant without accidental face-only cropping:1.82)",
    outfit:"(AUTO framing follows outfit priority:1.86), (the subject scale is large enough for garment silhouette, layers, bag, and accessories to remain readable:1.84), (preserve the selected visible range and do not crop away key outfit elements:1.84)",
    environment:"(AUTO framing follows environment priority:1.86), (clear breathing room and environmental context remain visible around the subject:1.84), (architecture, lighting, and spatial depth remain readable:1.84)",
    subjectDrink:"(AUTO framing follows subject-and-drink priority:1.88), (preserve the selected visible range while leaving enough lower foreground for the cup or glass and its supporting table or counter surface:1.86), (the subject's face and the drink remain simultaneously readable:1.86)",
    subjectFood:"(AUTO framing follows subject-and-food priority:1.88), (preserve the selected visible range while leaving enough lower foreground for the dish and supporting tabletop:1.86), (the subject's face, relevant hands, and food remain simultaneously readable:1.86)",
    subjectTabletop:"(AUTO framing follows subject-and-tabletop priority:1.88), (preserve the selected visible range while showing enough table or counter area for the hands and relevant tabletop objects:1.86), (avoid a face-only crop that removes the table relationship:1.88)",
    balanced:"(AUTO framing follows balanced priority:1.84), (person, outfit, and environment receive moderate breathing room and balanced scale:1.82)",
    auto:"(AUTO framing is derived from the selected visible range, scene, background mode, and composition:1.82), (use a natural subject scale with believable breathing room:1.8)"
  };
  return byFocus[state.visualFocus]||byFocus.auto;
}
function applyShootingPreset(presetKey){const preset=SHOOTING_PRESETS[presetKey];if(!preset)return;state.shootingPreset=presetKey;Object.entries(preset).forEach(([key,value])=>{state[key]=Array.isArray(value)?[...value]:value});sanitizeEffectsForFilm();sanitizeEffectsForWeather();sanitizeAdditionalElementsForWeather();sanitizeAngleForSelfieMode();sanitizeBackgroundViewForVisualFocus();focusAngleGroupForSelection(state.angleMode);}
function handleShootingPresetChange(){const el=document.getElementById("shootingPresetSelect");if(!el)return;const key=el.value;if(!key){state.shootingPreset="";return}if(key==="custom"){state.shootingPreset="custom";return}applyShootingPreset(key);renderAllOptionChips();}
function markPresetCustom(key){if(PRESET_CONTROLLED_KEYS.has(key)&&state.shootingPreset&&state.shootingPreset!=="custom")state.shootingPreset="custom";}
function syncShootingPresetSelect(){const el=document.getElementById("shootingPresetSelect");if(!el)return;el.value=state.shootingPreset||"";}
function renderChips(id,items,key){const el=document.getElementById(id);if(!el)return;el.innerHTML="";items.forEach(item=>{const active=state[key]===item.key||state[key]===item.value;const reason=getSingleChipDisabledReason(key,item.key);const disabled=!!reason&&!active;const invalid=!!reason&&active;const btn=document.createElement("button");btn.className="chip"+(active?" active":"")+(disabled?" disabled":"")+(invalid?" invalid":"");btn.textContent=item.label;btn.setAttribute("aria-disabled",disabled?"true":"false");if(reason)btn.title=reason;btn.onclick=()=>{if(disabled)return;markPresetCustom(key);state[key]=active?defaultFor(key):item.key;if(key==="film")sanitizeEffectsForFilm();if(key==="weather"){sanitizeEffectsForWeather();sanitizeAdditionalElementsForWeather();}if(key==="selfieMode")sanitizeAngleForSelfieMode();if(key==="visualFocus")sanitizeBackgroundViewForVisualFocus();renderAllOptionChips();};const helpItem=reason?{...item,help:(item.help?item.help+"\n\n":"")+(invalid?"現在の選択は成立条件不足\n":"選択不可\n")+reason}:item;bindChipHelp(btn,helpItem);el.appendChild(btn)})}
function renderMultiChips(id,items,key){const el=document.getElementById(id);if(!el)return;el.innerHTML="";items.forEach(item=>{const active=state[key].includes(item.key);const reason=!active?(key==="effects"?getEffectDisabledReason(item.key):key==="additionalElements"?getAdditionalElementDisabledReason(item.key):""):"";const disabled=!!reason;const btn=document.createElement("button");btn.className="chip"+(active?" active":"")+(disabled?" disabled":"");btn.textContent=item.label;btn.setAttribute("aria-disabled",disabled?"true":"false");if(reason)btn.title=reason;btn.onclick=()=>{if(disabled)return;const idx=state[key].indexOf(item.key);if(idx<0)state[key].push(item.key);else state[key].splice(idx,1);renderAllOptionChips();};const helpItem=reason?{...item,help:(item.help?item.help+"\n\n":"")+"選択不可\n"+reason}:item;bindChipHelp(btn,helpItem);el.appendChild(btn)})}
const OPTION_GROUP_OPEN_STATE={
  angle:new Set(["bodyAdjacent"]),
  additional:new Set(["light"])
};
function focusAngleGroupForSelection(angleKey){
  const group=ANGLE_PRESET_GROUPS.find(group=>group.items.includes(angleKey));
  if(!group)return;
  const openSet=OPTION_GROUP_OPEN_STATE.angle;
  openSet.clear();
  openSet.add(group.key);
}
function createOptionGroup(container,group,activeCount,openStateKey,bodyBuilder){
  const details=document.createElement("details");
  details.className="option-group";
  const openSet=OPTION_GROUP_OPEN_STATE[openStateKey];
  if(activeCount>0)openSet.add(group.key);
  details.open=openSet.has(group.key);
  details.addEventListener("toggle",()=>{if(details.open)openSet.add(group.key);else openSet.delete(group.key)});
  const summary=document.createElement("summary");summary.className="option-group-summary";
  const title=document.createElement("span");title.className="option-group-title";title.textContent=group.label;
  const count=document.createElement("span");count.className="option-group-count";count.textContent=activeCount?`${activeCount}選択`:`${group.items.length}項目`;
  summary.append(title,count);details.appendChild(summary);
  if(group.note){const note=document.createElement("div");note.className="option-group-note";note.textContent=group.note;details.appendChild(note)}
  const body=document.createElement("div");body.className="option-group-body";bodyBuilder(body);details.appendChild(body);container.appendChild(details);
}
function makeSingleChipButton(item,key){
  const active=state[key]===item.key||state[key]===item.value;const reason=getSingleChipDisabledReason(key,item.key);const disabled=!!reason&&!active;const invalid=!!reason&&active;
  const btn=document.createElement("button");btn.className="chip"+(active?" active":"")+(disabled?" disabled":"")+(invalid?" invalid":"");btn.textContent=item.label;btn.setAttribute("aria-disabled",disabled?"true":"false");if(reason)btn.title=reason;
  btn.onclick=()=>{if(disabled)return;markPresetCustom(key);state[key]=active?defaultFor(key):item.key;if(key==="angleMode"&&!active)focusAngleGroupForSelection(item.key);if(key==="film")sanitizeEffectsForFilm();if(key==="weather"){sanitizeEffectsForWeather();sanitizeAdditionalElementsForWeather();}if(key==="selfieMode")sanitizeAngleForSelfieMode();if(key==="visualFocus")sanitizeBackgroundViewForVisualFocus();renderAllOptionChips();};
  const helpItem=reason?{...item,help:(item.help?item.help+"\n\n":"")+(invalid?"現在の選択は成立条件不足\n":"選択不可\n")+reason}:item;bindChipHelp(btn,helpItem);return btn;
}
function makeMultiChipButton(item,key){
  const active=state[key].includes(item.key);const reason=!active?(key==="effects"?getEffectDisabledReason(item.key):key==="additionalElements"?getAdditionalElementDisabledReason(item.key):""):"";const disabled=!!reason;
  const btn=document.createElement("button");btn.className="chip"+(active?" active":"")+(disabled?" disabled":"");btn.textContent=item.label;btn.setAttribute("aria-disabled",disabled?"true":"false");if(reason)btn.title=reason;
  btn.onclick=()=>{if(disabled)return;const idx=state[key].indexOf(item.key);if(idx<0)state[key].push(item.key);else state[key].splice(idx,1);renderAllOptionChips();};
  const helpItem=reason?{...item,help:(item.help?item.help+"\n\n":"")+"選択不可\n"+reason}:item;bindChipHelp(btn,helpItem);return btn;
}
function renderGroupedSingleChips(id,items,key,groups,openStateKey){
  const el=document.getElementById(id);if(!el)return;el.innerHTML="";
  const autoItem=items.find(item=>item.key==="auto");if(autoItem){const autoWrap=document.createElement("div");autoWrap.className="chips";autoWrap.appendChild(makeSingleChipButton(autoItem,key));el.appendChild(autoWrap)}
  groups.forEach(group=>{const groupItems=group.items.map(itemKey=>items.find(item=>item.key===itemKey)).filter(Boolean);const activeCount=groupItems.filter(item=>state[key]===item.key||state[key]===item.value).length;createOptionGroup(el,group,activeCount,openStateKey,body=>{const chips=document.createElement("div");chips.className="chips";groupItems.forEach(item=>chips.appendChild(makeSingleChipButton(item,key)));body.appendChild(chips)})});
}
function renderGroupedMultiChips(id,items,key,groups,openStateKey){
  const el=document.getElementById(id);if(!el)return;el.innerHTML="";
  groups.forEach(group=>{const groupItems=group.items.map(itemKey=>items.find(item=>item.key===itemKey)).filter(Boolean);const activeCount=groupItems.filter(item=>state[key].includes(item.key)).length;createOptionGroup(el,group,activeCount,openStateKey,body=>{const chips=document.createElement("div");chips.className="chips";groupItems.forEach(item=>chips.appendChild(makeMultiChipButton(item,key)));body.appendChild(chips)})});
}
function defaultFor(key){return Object.prototype.hasOwnProperty.call(DEFAULT_STATE,key)?DEFAULT_STATE[key]:""}
function renderAllOptionChips(){sanitizeBackgroundViewForVisualFocus();renderChips("characterModeChips",CHARACTER_MODE_OPTIONS,"characterMode");renderChips("outfitReferenceModeChips",OUTFIT_REFERENCE_MODE_OPTIONS,"outfitReferenceMode");renderChips("locationReferenceModeChips",LOCATION_REFERENCE_MODE_OPTIONS,"locationReferenceMode");renderChips("weatherChips",WEATHER_OPTIONS,"weather");renderChips("filmChips",FILM_TONES,"film");renderChips("toneChips",OVERALL_TONES,"tone");renderMultiChips("effectChips",sortedEffects(),"effects");renderChips("effectStrengthChips",EFFECT_STRENGTH_OPTIONS,"effectStrength");renderGroupedMultiChips("additionalElementChips",ADDITIONAL_ELEMENTS,"additionalElements",ADDITIONAL_ELEMENT_GROUPS,"additional");renderChips("skinFinishChips",SKIN_FINISH_OPTIONS,"skinFinish");renderChips("closeupTextureChips",CLOSEUP_TEXTURE_OPTIONS,"closeupTexture");renderChips("selfieModeChips",SELFIE_MODE_OPTIONS,"selfieMode");renderChips("visualFocusChips",VISUAL_FOCUS_OPTIONS,"visualFocus");renderGroupedSingleChips("angleModeChips",ANGLES,"angleMode",ANGLE_PRESET_GROUPS,"angle");renderChips("visibleRangeChips",VISIBLE_RANGE_OPTIONS,"visibleRange");renderChips("cameraRollChips",CAMERA_ROLL_OPTIONS,"cameraRoll");renderChips("faceDirectionChips",FACE_DIRECTION_OPTIONS,"faceDirection");renderChips("gazeChips",GAZE_OPTIONS,"gaze");renderChips("backgroundViewChips",BACKGROUND_VIEW_MODES,"backgroundView");renderChips("framingChips",FRAMING_MODES,"framing");renderChips("photoStyleChips",PHOTO_STYLE_MODES,"photoStyle");renderChips("motionEnergyChips",MOTION_ENERGY_OPTIONS,"motionEnergy");renderChips("expressionChips",EXPRESSION_OPTIONS,"expression");syncShootingPresetSelect();updateSceneValidationStatus()}
function renderSceneLinkedChips(){
  sanitizeBackgroundViewForVisualFocus();
  renderChips("visualFocusChips",VISUAL_FOCUS_OPTIONS,"visualFocus");
  renderGroupedSingleChips("angleModeChips",ANGLES,"angleMode",ANGLE_PRESET_GROUPS,"angle");
  renderChips("visibleRangeChips",VISIBLE_RANGE_OPTIONS,"visibleRange");
  renderChips("backgroundViewChips",BACKGROUND_VIEW_MODES,"backgroundView");
  renderChips("motionEnergyChips",MOTION_ENERGY_OPTIONS,"motionEnergy");
}
function collectSceneValidationErrors(){
  const checks=[["angleMode",state.angleMode],["visualFocus",state.visualFocus],["motionEnergy",state.motionEnergy],["visibleRange",state.visibleRange]];
  return [...new Set(checks.map(([key,itemKey])=>getSceneLinkedDisabledReason(key,itemKey)).filter(Boolean))];
}
function updateSceneValidationStatus(){
  const el=document.getElementById("sceneValidationStatus");if(!el)return;
  const scene=getSceneTextRaw().trim();const errors=collectSceneValidationErrors();
  el.className="validation-status";
  if(errors.length){el.classList.add("error");el.textContent="シーン連動チェック：現在の選択に不足があります。\n・"+errors.join("\n・");return;}
  if(scene){el.classList.add("ok");el.textContent="シーン連動チェック：現在の選択に矛盾はありません。";return;}
  el.textContent="シーン連動チェック：シーンを入力すると、成立しない選択肢を自動で無効化します。";
}
function handleSituationInput(){renderSceneLinkedChips();updateSceneValidationStatus()}
function scaleWeightedPrompt(prompt,m){return (prompt||"").replace(/\(([^()]+?):([0-9]*\.?[0-9]+)\)/g,(match,body,w)=>`(${body}:${Math.round(Math.min(Math.max(parseFloat(w)*m,.1),3)*100)/100})`)}
function pickAngle(){if(state.angleMode!=="auto")return find("angleMode");const vr=state.visibleRange;const pool=vr==="extremeFace"||vr==="faceOnly"||vr==="faceCloseup"?["eye","golden","high"]:vr==="waistUp"||vr==="upperBody"?["eye","hiddenWaist","lowFront","tilted"]:["eye","hiddenWaist","walking","tilted"];return ANGLES.find(a=>a.key===pool[Math.floor(Math.random()*pool.length)])||ANGLES[1]}
function effectiveSelfie(scene){if(state.selfieMode==="on"||state.selfieMode==="off")return state.selfieMode;if(/他撮り|第三者|非自撮り|セルフィーじゃない|自撮りじゃない|撮ってもら|third-person|non-selfie/i.test(scene))return"off";return"on"}
function resolvedFaceGazePrompt(angleKey){
  const lookDownAngles={
    lowerBodyExtremeFrontLookDown:"(face turns downward toward the nearby low front camera:2.0), (eyes look directly down into the low lens:2.0), (chin gently lowered with a relaxed neck:1.96), (the torso remains front-oriented:1.96)",
    lowerBodyExtremeThreeQuarterLookDown:"(face turns diagonally downward toward the nearby low camera:2.0), (eyes look directly down into the low lens:2.0), (chin gently lowered with a relaxed neck:1.96), (the torso preserves the selected three-quarter direction:1.98)",
    lowerBodyExtremeSideLookDown:"(face turns downward toward the nearby low side camera:2.0), (eyes look directly down into the low lens:2.0), (chin gently lowered with a relaxed neck:1.96), (the torso remains side-oriented while only the head and gaze turn toward the camera:2.0)"
  };
  if(lookDownAngles[angleKey])return lookDownAngles[angleKey]+"\n(the angle-specific low-camera look-down lock overrides generic face-direction or gaze selections when they conflict:2.0)";
  return find("faceDirection").value+"\n"+find("gaze").value;
}
function bodyReferenceDirectionBlock(angleKey){
  if(BODY_REFERENCE_PROFILE_ANGLE_KEYS.has(angleKey))return`DIRECTION-AWARE BODY REFERENCE APPLICATION — PROFILE PRIORITY:
For the selected profile camera direction, prioritize A6 and A9 as the primary visible morphology references.
Use A4, A5, A7, and A8 only to confirm width, placement, and continuity that are not fully visible from the side.
Preserve the true profile depth and alignment of the ribcage, bust, waist, pelvis, hips, back line, and limbs.
Do not rotate the reconstructed body toward a front or three-quarter body type.`;
  if(BODY_REFERENCE_THREE_QUARTER_ANGLE_KEYS.has(angleKey))return`DIRECTION-AWARE BODY REFERENCE APPLICATION — THREE-QUARTER PRIORITY:
For the selected three-quarter camera direction, prioritize A5 and A8 as the primary visible morphology references.
Use A4 and A7 to confirm front-view width, and A6 and A9 to confirm profile depth.
Preserve the simultaneous visibility of front width and side depth across the bust, waist, pelvis, hips, torso, and limbs.
Do not flatten the body into a frontal view or rotate it into a true profile.`;
  if(BODY_REFERENCE_FRONT_ANGLE_KEYS.has(angleKey))return`DIRECTION-AWARE BODY REFERENCE APPLICATION — FRONT PRIORITY:
For the selected frontal or near-frontal camera direction, prioritize A4 and A7 as the primary visible morphology references.
Use A5, A6, A8, and A9 only to confirm depth and three-dimensional continuity.
Preserve the front-view widths, vertical placement, left-right balance, and full-body alignment of the bust, waist, pelvis, hips, torso, and limbs.
Do not replace the front-view morphology with a generic symmetrical body.`;
  return`DIRECTION-AWARE BODY REFERENCE APPLICATION — MULTI-VIEW CONSISTENCY:
The selected angle does not map to only one reference direction.
Use A4 through A9 together as views of one continuous three-dimensional body, while giving the closest available view the strongest visible-shape authority.
Use the remaining views only to confirm width, depth, vertical placement, and continuity.
Do not average the six views into a new body and do not invent a generic body between them.`;
}
function bodyDirectionValidationLine(angleKey){
  if(BODY_REFERENCE_PROFILE_ANGLE_KEYS.has(angleKey))return"for the selected profile direction, validate the visible morphology primarily against A6 and A9 while using the remaining views only for width and continuity confirmation";
  if(BODY_REFERENCE_THREE_QUARTER_ANGLE_KEYS.has(angleKey))return"for the selected three-quarter direction, validate the visible morphology primarily against A5 and A8 while using frontal views for width and profile views for depth confirmation";
  if(BODY_REFERENCE_FRONT_ANGLE_KEYS.has(angleKey))return"for the selected frontal or near-frontal direction, validate the visible morphology primarily against A4 and A7 while using the remaining views only for depth confirmation";
  return"validate the selected camera direction against the closest available A4 through A9 view while using the remaining views only for three-dimensional consistency";
}
function characterBlock(angleKey){if(state.characterMode==="off")return`SUBJECT REFERENCE — OFF:
No Images A1 through A9 and no typed subject definition are used.
(the subject remains a clearly adult person and is derived naturally from the written scene and active photographic settings:1.9),
(do not create or imply a fixed identity lock when subject reference is OFF:1.9)`;return`IMAGES A1–A9 — SUBJECT REFERENCE:
Images A1 through A9 are nine reference images of the same adult subject.

Use them in this fixed role order:
- A1 = face front
- A2 = face 45-degree view
- A3 = face profile
- A4 = bust shot front
- A5 = bust shot 45-degree view
- A6 = bust shot profile
- A7 = full body front
- A8 = full body 45-degree view
- A9 = full body profile

FACE REFERENCE ROLE SEPARATION — MANDATORY:
A1 is the sole primary source for visible face identity and facial appearance.
Use A2 and A3 only to confirm that A1 is the same person from 45-degree and profile viewpoints.
A2 and A3 must not average, beautify, redesign, narrow, lengthen, or replace the face defined by A1.

A4 through A9 are body-morphology references only.
Do not read, extract, infer, average, or use any facial information from A4 through A9, including:
- face width or face length
- eye shape, eye size, eyelids, or eye spacing
- eyebrow shape or placement
- nose bridge, nose width, or nose-tip shape
- lip shape, width, or volume
- cheek fullness
- jaw width or chin shape
- forehead or facial proportions

BODY REFERENCE ROLE SEPARATION — MANDATORY:
A4 through A6 are the primary upper-body morphology references.
Use A4 for the front-view structure of the shoulders, ribcage, bust, torso, and waist.
Use A5 for the three-quarter upper-body structure and the transition between visible width and depth.
Use A6 for profile structure, including torso depth, bust projection, waist depth, back line, and upper-body balance.

A7 through A9 are the primary full-body morphology references.
Use A7 for front-view full-body proportions, bust–waist–hip alignment, shoulder-to-pelvis balance, limb length, and overall bodyline.
Use A8 for three-quarter full-body depth, waist-to-hip transition, pelvis structure, hip contour, and limb volume.
Use A9 for profile depth, bust–waist–pelvis alignment, hip projection, torso-to-leg balance, and overall bodyline.

DIRECT BODY MORPHOLOGY READING — MANDATORY:
The reference images were selected so that the subject's bodyline and proportions are clearly readable.
Read the visible body structure directly and faithfully from A4 through A9.
Do not invent hidden corrections, compensations, alternative estimates, or a different body beneath the visible reference lines.
Treat the visible bust, waist, ribcage, torso, pelvis, hips, arms, and legs as the intended morphology of the subject.
Do not normalize, slim, enlarge, flatten, reduce, exaggerate, or redesign any body region.
Do not replace the visible reference morphology with a generic fashion-model body, an averaged body type, or a newly idealized body.

Do not use A1 through A9 for clothing, hairstyle, pose, hand position, camera angle, composition, background, lighting, or scene content.
The clothing visible in A1 through A9 must not appear in the generated image.
A1 through A9 must not influence outfit generation in any way.

FACE IDENTITY LOCK — A1 AUTHORITY:
Preserve the same recognizable adult person as A1.
Use A2 and A3 only as angle-confirmation evidence for A1, never as competing face sources.
Do not turn the subject into a different, averaged, generic, or newly beautified face.
Close camera distance, wide-angle perspective, expression, lighting, skin finish, HDR, monthly hairstyle, and crop must not redesign the facial identity.

BUST / WAIST / HIP MORPHOLOGY LOCK — MANDATORY:
Preserve the subject's visible bust morphology from A4 through A6, with A7 through A9 confirming its position and proportion within the full body.
Preserve bust width in front view, bust projection in profile view, vertical placement on the torso, three-quarter volume, and the visible upper, outer, and lower contours.
Preserve the continuous transition from ribcage and bust into the waist.

Preserve the waist morphology across A4 through A9.
Preserve the vertical waist position, front-view waist width, profile waist depth, the visible degree and shape of torso narrowing, and the transition from ribcage to waist and waist to pelvis.

Preserve the pelvis and hip morphology from A7 through A9.
Preserve pelvic width and depth, hip width in front view, hip projection in profile view, three-quarter hip contour, and the transitions from waist to hips and from lower hips into the upper thighs.

Treat the bust, waist, pelvis, hips, and thighs as one continuous three-dimensional body structure rather than as separate adjustable parts.

FULL BODY PROPORTION LOCK — MANDATORY:
Preserve the full-body proportional relationships visible across A7 through A9.
Preserve shoulder width relative to pelvis width, torso length relative to leg length, vertical waist position, bust–waist–hip spacing, arm length and thickness, thigh / knee / calf / ankle proportions, limb taper, and the overall front / three-quarter / profile bodyline.
Use A1 through A3 only for face identity and facial-angle confirmation, never to replace the body evidence in A4 through A9.
Do not replace the subject with a generic body type and do not reshape the subject's underlying proportions.

${bodyReferenceDirectionBlock(angleKey)}

MORPHOLOGY / PERSPECTIVE SEPARATION — MANDATORY:
The selected 357-series angle may strongly enlarge the body region nearest the lens and reduce the apparent size of more distant regions.
Treat this only as perspective projection applied to the already locked body morphology.
Do not permanently enlarge, reduce, flatten, or reshape the underlying bust, waist, pelvis, hips, torso, or limbs to match the projected appearance.
Pose and camera perspective may change visible projection, but must not redefine the subject's underlying morphology.

SUBJECT / GARMENT CONSISTENCY:
Render the selected outfit on the same adult subject defined by Images A1 through A9.
First resolve and lock the body morphology from A4 through A9, then place the selected outfit onto that fixed body.
Treat garment silhouette, looseness, fit, and drape as clothing properties rather than as evidence for changing the subject.
Keep anatomy coherent with the selected pose, camera perspective, and visible range.
${state.outfitReferenceMode==="on"?"When Image B is active, use it only to determine the outfit design, materials, fit, and styling.":""}`}
function outfitBlock(){if(state.outfitReferenceMode==="off")return`OUTFIT REFERENCE — OFF / COORDINATION AUTO:
(do not use Image B for clothing, styling, color palette, accessories, pose, scene, or any other information:2.0),
(create a coherent outfit automatically from the written scene, weather, time, and selected style settings:1.9),
(do not reuse a previous coordinate sheet, cached outfit, sample outfit, or earlier conversation outfit:2.0)`;return`OUTFIT REFERENCE — FULL STRICT:
Image B is the outfit reference only.
When subject reference is ON, attach Image B after subject images A1 through A9 as the final reference image.

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

Do not use Image B for face, body shape, hairstyle, pose, hand position, camera angle, composition, background, location, lighting, or facial expression.
Ignore all non-outfit information in Image B.
Image B must control the outfit only.

If Image B is a coordinate sheet, read its filled item boxes, item names, accessories, color palette, POINT, and STYLE POINT as outfit instructions.
Ignore coordinate-sheet borders, template layout, title typography, decorative lines, empty boxes, mannequin form, model body, illustration body, and product-presentation silhouette as scene or subject information.
Do not reuse a previous coordinate sheet, cached outfit, sample outfit, or earlier conversation outfit.

IMAGE B / BODY SEPARATION — MANDATORY:
${state.characterMode==="on"?"The subject's body morphology has already been established from A4 through A9. Fit and drape the selected garments over that fixed body.\nDo not use any body, mannequin, model, illustration, item silhouette, or coordinate-sheet presentation in Image B to redefine bust morphology, waist width or position, pelvis width, hip morphology, limb length or thickness, or overall body proportions.\nResolve A4 through A9 body morphology first; apply Image B clothing second.":"Subject reference is OFF, so Image B must still control clothing only and must not impose the body, mannequin, model, or illustration shown in the outfit reference."}`}
function visibleRangeLock(){
  const key=state.visibleRange;
  const map={
    balanced:"(selected visible range is mandatory:1.98), (show a balanced portrait with face, upper body, and believable context clearly visible:1.94), (do not convert this into an extreme close-up or distant full-body shot:1.94)",
    faceOnly:"(selected visible range is mandatory:2.0), (crop strictly to the face from forehead to chin or just above the neck:2.0), (shoulders, chest, outfit, hands, and most background must remain outside the frame:1.98), (do not widen to head-and-shoulders or upper body:2.0)",
    extremeFace:"(selected visible range is mandatory:2.0), (the face must fill almost the entire frame:2.0), (eyes, lips, skin texture, and hairline dominate the image:1.98), (background and outfit must be barely visible:1.98), (do not widen the crop:2.0)",
    faceCloseup:"(selected visible range is mandatory:2.0), (close-up framing must show the face prominently with only slight neck or shoulder visibility:1.98), (do not widen to upper-body, waist-up, or full-body framing:2.0)",
    profileCloseup:"(selected visible range is mandatory:2.0), (tight side-profile close-up must dominate the frame:1.98), (eye, nose bridge, lips, cheek contour, and jawline must remain clearly readable:1.98), (do not widen to upper-body or front-facing framing:2.0)",
    headShoulder:"(selected visible range is mandatory:2.0), (frame strictly from head through shoulders:1.98), (face, hair, neck, and shoulders must be visible:1.98), (chest below the upper line and waist must remain outside the frame:1.96), (do not convert to face-only or upper-body framing:2.0)",
    upperBody:"(selected visible range is mandatory:2.0), (frame the subject from head to chest or waist area:1.98), (face and upper outfit must both be clearly readable:1.98), (do not crop to face-only and do not widen to full body:2.0)",
    waistUp:"(selected visible range is mandatory:2.0), (frame strictly from head to waist or upper hips:1.98), (face, torso line, and outfit coordination must all be visible:1.98), (legs below the upper hips must remain outside the frame:1.96), (do not crop to upper-body or widen to full body:2.0)",
    fullBody:"(selected visible range is mandatory:2.0), (the entire body from head to feet must be inside the frame:2.0), (shoes and full outfit must be visible:1.98), (do not crop feet, legs, waist, or head:2.0), (do not convert to waist-up or upper-body framing:2.0)"
  };
  return map[key]||"(selected visible range is mandatory and must not be replaced by another crop:1.98)";
}
function cameraModeBlock(selfie,angleKey){
  if(selfie==="off")return`CAMERA MODE — NON-SELFIE / THIRD-PERSON PHOTO — MANDATORY:
(non-selfie portrait photo:2.0),
(third-person external camera viewpoint is mandatory:2.0),
(subject is not holding the active camera:2.0),
(no smartphone selfie POV, no selfie arm, no front-camera perspective:2.0),
(do not convert this into a selfie under any circumstance:2.0)`;
  if(angleKey==="groundLegToFaceSelfie")return`CAMERA MODE — HANDHELD GROUND-LEVEL SELFIE — MANDATORY:
(this must remain a real selfie captured by the subject herself:2.0),
(the smartphone in her own hand is the active front camera near ground level:2.0),
(the viewpoint originates from this handheld smartphone and not from a phone placed on the floor:2.0),
(the camera-holding arm reaches naturally toward the low camera position while preserving believable anatomy:1.96),
(the foreground leg-to-face line follows the pose explicitly written in the scene:1.98),
(no timer shot, no remote camera, no tripod, no third-person photographer, and no detached external viewpoint:2.0)`;
  if(BODY_ADJACENT_ANGLE_KEYS.has(angleKey))return`CAMERA MODE — BODY-ADJACENT LOW SELFIE — MANDATORY:
(this must remain a real selfie captured by the subject herself:2.0),
(the single active smartphone is held by the lowered shooting hand and its front camera produces the image:2.0),
(the active camera smartphone itself remains outside the captured image because the viewpoint originates from its lens:2.0),
(the viewpoint originates from the selected waist or waist-below body-adjacent position:2.0),
(the shooting shoulder, upper arm, elbow, forearm, wrist, and hand remain compressed close to the selected front, diagonal, or side body line:2.0),
(the shooting arm follows the contour of the abdomen, waist, hip, or flank instead of projecting straight forward from the torso:2.0),
(the shooting elbow stays below shoulder height, tucked beside the torso, and does not open away from the body:2.0),
(the camera-holding hand and active phone stay just beyond the lower or side frame boundary at the lens origin:2.0),
(only a small cropped portion of the shooting forearm may touch the lower or side frame edge when anatomically unavoidable:2.0),
(the immediate foreground is formed by the near abdomen, waist, hip, or flank, never by the shooting arm:2.0),
(the camera arm must not become a long foreshortened foreground arm, must not cross the center of the image, and must not dominate the frame:2.0),
(do not render the full shoulder-to-hand chain as a visible diagonal extending toward the viewer:2.0),
(the upper arm does not rise beside the face and the phone does not move toward chest or eye level:2.0),
(no ordinary arm-extended selfie, no raised-arm selfie, no detached camera viewpoint, and no external photographer:2.0)`;
  if(angleKey==="hiddenWaist")return`CAMERA MODE — HIDDEN WAIST-HELD SELFIE — MANDATORY:
(this must remain a real selfie captured by the subject herself:2.0),
(the single smartphone in her lowered shooting hand is the active camera at waist or lower-torso height:2.0),
(the active camera smartphone itself remains outside the captured image because the viewpoint originates from its lens:2.0),
(the shooting elbow stays bent and close to the body and the shooting forearm follows the torso rather than extending toward the lens:2.0),
(no arm's-length selfie, no long foreground arm, no raised-hand selfie, no second smartphone, and no external viewpoint:2.0)`;
  return`CAMERA MODE — SELFIE — MANDATORY:
(this must remain a real selfie captured by the subject herself:2.0),
(the single smartphone in her shooting hand is the active front camera:2.0),
(the image viewpoint must originate from that smartphone and the active camera phone itself must remain outside its own captured image:2.0),
(viewpoint follows the selected completed camera-angle preset exactly:2.0),
(no second smartphone, no third-person photographer, no external camera viewpoint, no observer viewpoint:2.0),
(do not convert this into a third-person portrait under any circumstance:2.0),
(do not copy the reference image camera angle or arm extension:1.98)`}
function selfieHandRoleBlock(selfie,angleKey){
  if(selfie!=="on")return"";
  const bodyAdjacent=BODY_ADJACENT_ANGLE_KEYS.has(angleKey);
  return `SELFIE HAND ROLE / SINGLE-DEVICE LOCK — MANDATORY:
(exactly one smartphone exists in the selfie setup:2.0),
(the shooting hand holds that single smartphone as the active front camera:2.0),
(the active camera smartphone is outside the captured image because the image is produced from its own lens:2.0),
(the non-shooting hand must not hold, display, touch, or operate a smartphone, second phone, remote shutter, compact camera, or any duplicate recording device:2.0),
(any scene mention of smartphone screen light or phone-screen glow refers to the screen of the active camera phone near the lens, not to a visible phone in the free hand:2.0),
(the non-shooting hand first follows any explicit physical support or explicitly required non-phone prop in the written scene; otherwise it is assigned to the selected BODY MOTION / DYNAMIC ENERGY:1.98),
(the camera-holding arm is excluded from free-hand motion and must preserve the selected camera geometry:2.0),
(the free hand must not reach across the lens, imitate the shooting arm, or create a second selfie gesture:2.0)${bodyAdjacent?`,
(for this body-adjacent angle, the entire shooting arm remains folded and contour-following beside the abdomen, waist, hip, or flank:2.0),
(the shooting wrist, camera-holding hand, and active phone remain immediately outside the lower or side frame at the lens origin:2.0),
(the shooting arm must not extend straight toward the viewer and must not create a large blurred arm in the immediate foreground:2.0),
(the visible near-body surface, not the shooting arm, must be the dominant closest foreground:2.0)`:""}`;
}
function bodyMotionBlock(selfie,angleKey){
  if(selfie!=="on")return `BODY MOTION / DYNAMIC ENERGY:\n${find("motionEnergy").value}`;
  const motion={
    auto:"(derive natural movement from the written action and physical support, applying it to the non-shooting hand, shoulders, torso, clothing, and locked-length hair only:1.86), (do not move the camera-holding arm away from the selected camera position:2.0)",
    subtle:"(the non-shooting hand makes a small relaxed movement or rests naturally on the body, clothing, sofa, cushion, chair, or other support described in the scene:1.9), (subtle motion appears in shoulders, posture, clothing edges, and locked-length hair tips while the camera arm remains fixed:1.88)",
    natural:"(the non-shooting hand, shoulders, and upper body form one believable in-between movement that follows the written action:1.94), (the free hand may adjust clothing, touch a support, or move naturally through the pose, but it must remain empty of smartphones and must not cross the lens:2.0), (hair and garment movement follow inertia and gravity while the camera arm remains locked:1.9)",
    strong:"(strong dynamic energy is expressed through the non-shooting hand, torso twist, shoulders, clothing, and locked-length hair while preserving physical support:1.96), (the free arm may form a decisive gesture only away from the lens and away from the camera arm:1.94), (the camera-holding shoulder, elbow, forearm, wrist, and hand remain fixed to the selected camera line despite the stronger body motion:2.0)"
  }[state.motionEnergy]||"(derive natural free-hand and body movement from the written scene while keeping the camera arm fixed:1.9)";
  const adjacent=BODY_ADJACENT_ANGLE_KEYS.has(angleKey)?"\n(the body-adjacent shooting arm remains tucked along the selected body contour and is never used as the visible dynamic arm:2.0),\n(the non-shooting arm supplies any visible arm movement without entering the immediate lens-to-body corridor:2.0)":"";
  return `BODY MOTION / DYNAMIC ENERGY — RESOLVED AFTER CAMERA AND HAND LOCKS:\n(resolve the active camera, camera arm, and completed angle geometry before applying body motion:2.0),\n${motion}${adjacent}`;
}
function angleGroupForKey(angleKey){return ANGLE_PRESET_GROUPS.find(group=>group.items.includes(angleKey))||null}
function buildAngleExecutionPrompt(angle,selfie){
  const family=angleGroupForKey(angle.key);
  const blocks=[`ANGLE PRESET EXECUTION — COMPLETE GEOMETRY — MANDATORY:
(the selected preset defines camera height, camera-to-subject distance, camera direction, optical axis, and perspective as one completed shot geometry:2.0),
(resolve the selected camera geometry before crop, background visibility, subject priority, image roll, styling, or effects:2.0),
(visible range controls cropping only and must not move the camera closer to or farther from the subject:2.0),
(background visibility, framing, and subject-priority settings must not normalize, flatten, or replace the selected angle:2.0),
(camera roll rotates the completed image plane only and must not change camera height, direction, or distance:2.0)${family?`\n(angle family: ${family.label}:1.7)`:""}`];
  blocks.push(`CAMERA POSITION / ANGLE — ${angle.label}:\n${angle.value}`);
  if(BODY_ADJACENT_ANGLE_KEYS.has(angle.key)){
    const intensity=EXTREME_BODY_ADJACENT_ANGLE_KEYS.has(angle.key)?`(the near abdomen, waist, hip, or flank occupies a dominant large area of the immediate foreground:2.0),\n(the torso appears substantially larger and closer than the face because the lens is immediately adjacent to the body line:2.0),`:`(the near waist or torso remains clearly in the immediate foreground:1.96),\n(the torso appears noticeably closer than the face because the lens stays beside the body line:1.96),`;
    const mode=selfie==="on"?`(the subject's lowered camera hand physically maintains this close body-adjacent distance:2.0),
(the shooting forearm remains folded along the abdomen, waist, hip, or flank and does not point outward toward the lens:2.0),
(the shooting wrist and camera-holding hand remain just outside the lower or side image boundary at the lens origin:2.0),
(the shooting arm stays outside the central lens-to-face corridor and cannot become a large foreground limb:2.0),
(the near abdomen, waist, hip, or flank must remain visibly closer to the lens than any visible part of the shooting arm:2.0),
(the elbow remains below the shoulder, tucked beside the body, and the camera cannot rise into an ordinary selfie:2.0)`:`(the external camera is physically placed immediately beside the selected body line:2.0),
(the photographer must not step backward to obtain a safer or more balanced composition:2.0)`;
    blocks.push(`BODY-ADJACENT DISTANCE LOCK — MANDATORY:
(the camera remains immediately beside or in front of the selected waist-to-upper-thigh body line:2.0),
(no broad empty gap is allowed between the lens and the near body surface:2.0),
${intensity}
(the viewpoint must continue along the visible body surface toward the chest, neck, and face:2.0),
(the face remains visible near the upper portion of the frame without reducing the body-adjacent perspective:1.98),
(if a wider crop is selected, widen the crop while preserving the same camera position; do not step the camera backward:2.0),
${mode}`);
  }
  return blocks.join("\n\n");
}
function expressionValue(scene){if(state.expression)return find("expression").value;if(/めっちゃ嬉し|すごく嬉し|嬉しそう|happy|joyful/i.test(scene))return"very happy joyful smile, bright expressive eyes, clearly delighted expression";return"natural context-driven expression"}
function buildAdditionalElementPlan(selected){
  if(!selected.length)return"";
  const lines=ADDITIONAL_ELEMENT_GROUPS.map(group=>{
    const names=group.items.filter(key=>selected.includes(key)).map(key=>ADDITIONAL_ELEMENTS.find(item=>item.key===key)?.label.replace(/^[^\w一-龯ぁ-んァ-ヶ]+/u,"").trim()).filter(Boolean);
    return names.length?`${group.promptTitle}: ${names.join(", ")}`:"";
  }).filter(Boolean);
  return`ADDITIONAL ELEMENT EXECUTION PLAN:
Treat the selected items as physical scene components established before camera effects and color grading, not as decorative overlays.
${lines.join("\n")}
Give every light beam a plausible source, reveal particles mainly where light reaches them, align projected shadows with scene geometry, and make moving elements follow wind, gravity, material weight, and the written action.
Keep the subject's face, outfit, and selected composition clearly readable; do not turn the scene into random clutter.`;
}
function buildEffectPlan(selected){if(!selected.length)return"";const optical=new Set(["bokeh","foreground","strongForeground","orb","glass","droplet","softfocus","motionblur","handblur"]),lighting=new Set(["rim","flash","warmflare","lightleak","neon","hardsun","hardshadow","blownhighlight","lightshadow","chiaroscuro","splitlight","dappledshadow"]),atmosphere=new Set(["heathaze","drydust","sparkle"]),finish=new Set(["coolfilter","hdr","digicam","grain","vhs","vignette"]),groups=[];const add=(title,set)=>{const names=selected.filter(k=>set.has(k)).map(k=>EFFECTS.find(e=>e.key===k)?.label.replace(/^[^\w一-龯ぁ-んァ-ヶ]+/u,"").trim()).filter(Boolean);if(names.length)groups.push(`${title}: ${names.join(", ")}`)};add("optical depth",optical);add("lighting",lighting);add("atmosphere",atmosphere);add("finish",finish);return `EFFECT EXECUTION PLAN:
Apply the selected effects as visible photographic properties in this order: scene lighting, optical depth, atmosphere, then final color/texture finish.
${groups.join("\n")}
Each selected effect must alter a physically relevant part of the image; do not treat the effect names as decorative keywords.`;}
function manualLocationReferenceAttachmentText(){
  if(state.outfitReferenceMode==="on")return"If project information sources are not available, attach Image C after Image B as the final reference image.";
  if(state.characterMode==="on")return"If project information sources are not available, attach Image C after A1 through A9 as the final reference image.";
  return"If project information sources are not available, attach Image C together with the prompt as the final reference image.";
}
function locationReferenceBlock(){
  if(state.locationReferenceMode!=="on")return`LOCATION REFERENCE — OFF:
(do not use Image C or any place-reference image:2.0),
(the written scene text is the only source for place and environment design:1.9)`;
  return`LOCATION REFERENCE — ON / SPATIAL RECONSTRUCTION:
Image C is the place / environment reference only.
Use Image C as a visual reference for the location's architecture, materials, layout, vegetation, fixtures, and atmosphere.

Reconstruct the location as a new coherent photographic scene from the selected camera viewpoint.
Do not paste, composite, trace, or directly reuse Image C as a flat background plate.
Adapt the location naturally to the selected camera height, angle, framing, lens perspective, and visible range.

Integrate the subject physically into the reconstructed environment with:
- shared perspective and scale
- matching ambient light and color temperature
- natural contact shadows
- consistent depth of field
- believable reflections and light spill
- no cutout edges or pasted-on appearance

Do not use Image C for:
- face
- body shape
- hairstyle
- clothing
- pose
- hand position
- camera angle
- facial expression

Ignore people or incidental subjects inside Image C.
Image C must guide the location and environment only, while the selected subject, outfit, and camera settings remain controlled elsewhere.`;
}
function monthlyHairBlock(month,subjectReferenceOn){
  const base=HAIR_BY_MONTH[month]||"";
  const strict=HAIR_STRICT_LOCK_BY_MONTH[month]||"";
  const referenceLock=subjectReferenceOn
    ? "(completely ignore all hairstyle evidence in Images A1 through A9, including length, color, tying, bun, ponytail, braid, extensions, volume, and silhouette:2.0),\n(use A1 through A9 only for face identity and body morphology; do not preserve, blend, or average their hairstyle with the monthly hairstyle:2.0)"
    : "(subject image reference is OFF; do not infer or invent a different hairstyle from any prior image or conversation:2.0)";
  return `HAIR — MONTHLY STYLE / SOLE HAIR SOURCE — MANDATORY:
${base},
${strict},
(the current month's hairstyle is the sole authoritative source for hair cut, length, color, silhouette, parting, volume, and finish:2.0),
(the monthly hairstyle must be visibly realized in the final image rather than merely mentioned in the prompt:2.0),
${referenceLock},
(Image B controls outfit only and must not influence hair in any way:2.0),
(scene text may control temporary hair motion or a removable head accessory only when it preserves the monthly cut, length, color, and silhouette:1.98),
(resolve and lock the monthly hairstyle before pose, camera perspective, lighting, motion, and effects are applied:1.98)`;
}
function finalFaceIdentityCheck(){
  if(state.characterMode!=="on")return"";
  return `FINAL FACE IDENTITY VALIDATION — A1 AUTHORITY — MANDATORY:
(before final rendering, verify that the visible face remains the same recognizable adult person as Image A1:2.0),
(A1 is the sole primary source for visible face identity; A2 and A3 only confirm the same person from additional angles:2.0),
(do not use facial information from A4 through A9 under any circumstance:2.0),
(preserve A1's face width, overall facial proportions, eye shape / size / spacing, eyelid structure, eyebrows, nose bridge / width / tip, lip shape / width / volume, cheek fullness, jaw width, chin shape, and forehead proportions:2.0),
(do not beautify, narrow, lengthen, average, masculinize, feminize, or redesign the face:2.0),
(close camera distance, wide-angle perspective, high angle, low angle, HDR, hard sunlight, split light, skin finish, close-up texture, expression, monthly hairstyle, and crop may change photographic appearance but must not create a different identity:2.0),
(if the visible face differs from A1, correct the facial identity before finalizing the image:2.0)`;
}
function finalBodyMorphologyCheck(angleKey){
  if(state.characterMode!=="on")return"";
  return `FINAL BODY MORPHOLOGY VALIDATION — A4–A9 AUTHORITY — MANDATORY:
(before final rendering, verify that the visible body remains the same subject defined directly by Images A4 through A9:2.0),
(verify shoulder-to-torso balance and shoulder width relative to pelvis width:2.0),
(verify bust width, vertical placement, profile projection, three-quarter volume, and visible contour:2.0),
(verify waist width, depth, vertical position, torso narrowing, and ribcage-to-waist-to-pelvis transition:2.0),
(verify pelvic width and depth, hip width, profile projection, three-quarter contour, and hip-to-thigh connection:2.0),
(verify torso length, bust–waist–hip spacing, arm and leg length, limb thickness and taper, and overall full-body proportions:2.0),
(${bodyDirectionValidationLine(angleKey)}:1.95),
(Image B, clothing fit, pose, camera angle, visible range, lighting, motion, and effects must not redefine the underlying body morphology:2.0),
(perspective may change apparent size according to camera distance, but the underlying proportions must remain consistent with A4 through A9:2.0),
(do not apply hidden corrections or alternative body estimates; validate against the visible reference lines directly:2.0),
(if the visible body differs from A4 through A9, correct the body structure before finalizing the image:2.0)`;
}
function finalMonthlyHairCheck(month){
  const julyRule=month===7
    ? "(for July, reject and correct any shoulder-touching or longer hair, hidden gathered length, tied hair, or long strands extending across the pillow, chest, or back:2.0),\n"
    : "";
  return `FINAL MONTHLY HAIR VALIDATION — MANDATORY:
(before final rendering, verify that the visible hairstyle exactly matches the active monthly hairstyle defined above:2.0),
${julyRule}(pose, reclining, gravity, wind, motion, camera angle, lighting, and effects may alter only natural strand placement and must not alter the actual cut, length, color, or hairstyle category:2.0),
(if the visible hair conflicts with the active monthly definition, correct the hair before finalizing the image:2.0)`;
}
function finalSelfieHandValidation(selfie,angleKey){
  if(selfie!=="on")return"";
  const bodyAdjacent=BODY_ADJACENT_ANGLE_KEYS.has(angleKey);
  return `FINAL SELFIE HAND / DEVICE VALIDATION — MANDATORY:
(before final rendering, verify that there is exactly one smartphone and that it is the active camera held by the shooting hand:2.0),
(the active camera phone must not appear as a visible object inside the image generated from its own lens:2.0),
(the non-shooting hand must not hold any smartphone, second device, remote shutter, or duplicate camera:2.0),
(the camera-holding arm must preserve the selected camera position and must not be reassigned to BODY MOTION / DYNAMIC ENERGY:2.0),
(the visible free-hand action must follow the written scene or selected motion energy without crossing the lens:1.98)${bodyAdjacent?`,
(for the selected body-adjacent angle, reject and correct any long arm projected toward the viewer, any large foreground selfie arm, any arm crossing the center, or any gap that detaches the camera arm from the torso line:2.0),
(reject and correct any composition where the shooting arm is the nearest or largest foreground object instead of the abdomen, waist, hip, or flank:2.0),
(the corrected shooting arm must remain tucked and contour-following beside the abdomen, waist, hip, or flank, with the wrist, camera hand, and active phone outside the lower or side frame boundary:2.0)`:""},
(if any hand or device violates these roles, correct the hand assignment and camera-arm geometry before finalizing the image:2.0)`;
}
function buildPrompt(){const t=getTokyoNow();const sceneRaw=document.getElementById("situation").value.trim()||"No scene details provided. Create a realistic everyday portrait scene.";const angle=pickAngle();const selfie=effectiveSelfie(sceneRaw);const fxMult=EFFECT_MULT[state.effectStrength]||1;const selectedEffectKeys=state.effects.filter(k=>EFFECTS.some(e=>e.key===k));const selectedAdditionalKeys=state.additionalElements.filter(k=>ADDITIONAL_ELEMENTS.some(e=>e.key===k));const additionalElements=selectedAdditionalKeys.map(k=>ADDITIONAL_ELEMENTS.find(e=>e.key===k)).filter(Boolean).map(e=>e.value);const effects=selectedEffectKeys.map(k=>EFFECTS.find(e=>e.key===k)).filter(Boolean).map(e=>scaleWeightedPrompt(e.value,fxMult));const effectPriority=state.effects.length?(state.effectStrength==="strong"?"(selected effects are mandatory, clearly visible, and must strongly affect the final image:2.0)":state.effectStrength==="max"?"(selected effects are mandatory, dominant, unmistakable, and visually prominent across the final image:2.15)":state.effectStrength==="standard"?"(selected effects must be clearly visible in the final image:1.86)":"(selected effects should remain subtly but visibly present in the final image:1.72)"):"";const weather=state.weather?find("weather").value:"";const film=find("film").value;const tone=find("tone").value;const blocks=[];blocks.push(`APP_VERSION: ${APP_VERSION}\nPROMPT_ENGINE: angle-core + reference reading + visible-range + style/effects\nCAMERA_ENGINE: angle-preset, not micro physical controls`);
blocks.push(`PROJECT SOURCE FILE RESOLUTION:
${state.characterMode==="on"?"Use the fixed project source files below for subject reference when they are available in the project information sources.\nIf project information sources are not available, attach the subject images together with the prompt in this exact order.\nA1 = A1_FACE_FRONT.jpg\nA2 = A2_FACE_45.jpg\nA3 = A3_FACE_PROFILE.jpg\nA4 = A4_BUST_FRONT.jpg\nA5 = A5_BUST_45.jpg\nA6 = A6_BUST_PROFILE.jpg\nA7 = A7_FULL_FRONT.jpg\nA8 = A8_FULL_45.jpg\nA9 = A9_FULL_PROFILE.jpg\nA1 is the sole primary face-identity reference. A2–A3 confirm that same face from additional angles without averaging or redesigning it. A4–A9 are body-morphology references only and must not contribute any facial feature information.":"Subject image reference is OFF, so no A1 through A9 subject images are used."}
${state.outfitReferenceMode==="on"?"Use Image B = B_CURRENT_OUTFIT.jpg as the fixed outfit / coordinate-sheet reference when it is available in the project information sources.\nIf project information sources are not available, attach Image B after A1 through A9 as the next reference image.":"Outfit reference is OFF, so no Image B outfit reference is used."}
${state.locationReferenceMode==="on"?"Use Image C = C_LOCATION_REFERENCE.jpg as the fixed location reference when it is available in the project information sources.\n"+manualLocationReferenceAttachmentText():"Location reference is OFF, so no Image C place reference is used."}
(When the fixed files are available in project information sources, do not request re-upload:2.0)\n(When active references are manually attached instead, all active reference images must be attached at the same time as the prompt:2.0)`);
blocks.push(`SUBJECT REFERENCE MODE:\n${find("characterMode").label}\n${characterBlock(angle.key)}`);
blocks.push(`OUTFIT REFERENCE MODE:\n${find("outfitReferenceMode").label}\n${outfitBlock()}`);
blocks.push(`LOCATION REFERENCE MODE:\n${find("locationReferenceMode").label}\n${locationReferenceBlock()}`);
blocks.push(monthlyHairBlock(t.month,state.characterMode==="on"));
blocks.push(`SAFETY / REALISM:
(clearly adult subject:2.0),
(appropriate fully opaque everyday fashion clothing:1.95),
(photographic realism, natural skin texture, believable lighting and shadows:1.9),
(no anime, no illustration, no plastic skin, no excessive beauty-filter appearance:1.9)`);
blocks.push(`SCENE:
${sceneRaw}
(scene text controls location, outfit notes, standing, seated, reclining, leaning, action, physical support, and expression detail, but must not override the selected subject definition, monthly hair, selected angle preset, camera-arm position, or selfie hand roles:1.9),
(the scene must not lengthen, shorten, recolor, tie up, braid, or otherwise replace the locked monthly hairstyle:2.0),
(the written scene text is the authoritative source for standing, seated, reclining, leaning, and physical support:1.92),
(keep the pose physically consistent with chairs, sofas, tables, counters, beds, floors, and walls described in the scene:1.9)`);
blocks.push(`CAMERA MODE:
${cameraModeBlock(selfie,angle.key)}`);
blocks.push(buildAngleExecutionPrompt(angle,selfie));
const handRole=selfieHandRoleBlock(selfie,angle.key);if(handRole)blocks.push(handRole);
blocks.push(bodyMotionBlock(selfie,angle.key));
blocks.push(`VISIBLE RANGE — STRICT CROP LOCK:\n${find("visibleRange").value}\n${visibleRangeLock()}`);
blocks.push(`IMAGE TILT / CAMERA ROLL:\n${find("cameraRoll").value}`);
blocks.push(`FACE / GAZE:
${resolvedFaceGazePrompt(angle.key)}`);
blocks.push(`COMPOSITION:\n${resolvedBackgroundPrompt()}\n${resolvedFramingPrompt()}\n${find("photoStyle").value}\n${resolvedVisualFocusPrompt()}\n(selected camera angle preset, visible range, face direction, gaze, background, and framing must work together as one portrait composition:1.88),\n(the selected camera roll must be visibly readable from the shared rotation of the entire frame and background structural lines; do not simulate roll by tilting only the subject:1.88),\n(do not replace a difficult waist-held or low-angle preset with a normal pretty high-angle selfie:1.95)`);
blocks.push(`EXPRESSION / MOOD:\n(${expressionValue(sceneRaw)}:1.9),\n(context-driven natural micro-expression matching scene, time, weather, and emotion:1.78)`);
const additionalPlan=buildAdditionalElementPlan(selectedAdditionalKeys);if(additionalPlan)blocks.push(`${additionalPlan}\n\nADDITIONAL SCENE ELEMENTS / ATMOSPHERIC STAGING:\n${additionalElements.join("\n")}`);
const skin=find("skinFinish").value; const close=find("closeupTexture").value; if(skin)blocks.push(`SKIN FINISH:\n${skin}`); if(close)blocks.push(`CLOSE-UP TEXTURE:\n${close}`);
const effectPlan=buildEffectPlan(selectedEffectKeys); if(effectPlan)blocks.push(effectPlan);
blocks.push(`STYLE / EFFECTS — APPLY LAST:\nCurrent time: ${t.timeCtx.label} (${t.timeCtx.en}), ${t.timeStr} JST\nDay mood: ${DAY_MOOD[t.day]}\nTime-of-day mood: ${t.timeCtx.mood}\n${weather?"Weather: "+weather:""}\n${film?"Film tone: "+film:""}\n${tone?"Overall tone: "+tone:""}\n${effects.length?"Effects: "+effects.join(", "):""}\n${effectPriority}\n(apply film tone, color treatment, blur, grain, light, and texture only after the portrait composition is solved:1.88)`);
blocks.push(`ASPECT / ENVIRONMENT:\n(vertical 9:16 smartphone image:1.6),\n(real location matching the written scene, believable people, signs, lighting, and depth:1.75),\n(realistic ambient lighting and natural handheld micro-shake:1.65)`);
blocks.push(finalFaceIdentityCheck());
blocks.push(finalBodyMorphologyCheck(angle.key));
blocks.push(finalMonthlyHairCheck(t.month));
blocks.push(finalSelfieHandValidation(selfie,angle.key));
return blocks.filter(Boolean).join("\n\n");}
function handleGenerate(){const validationErrors=collectSceneValidationErrors();if(validationErrors.length){updateSceneValidationStatus();document.getElementById("sceneCard")?.scrollIntoView({behavior:"smooth",block:"center"});alert("シーン連動チェックで不足があります。\n\n・"+validationErrors.join("\n・"));return;}const prompt=buildPrompt();document.getElementById("metaCard").classList.remove("hidden");document.getElementById("outputCard").classList.remove("hidden");document.getElementById("outputArea").value=prompt;document.getElementById("metaContent").innerHTML=[`🧩 <b style='color:#c4b5fd'>App</b>：${APP_VERSION}`,`👤 <b style='color:#c4b5fd'>被写体参照</b>：${find("characterMode").label}`,`👗 <b style='color:#c4b5fd'>コーデ参照</b>：${find("outfitReferenceMode").label}`,`📍 <b style='color:#c4b5fd'>場所参照</b>：${find("locationReferenceMode").label}`,`🎥 <b style='color:#c4b5fd'>撮影方式</b>：${find("selfieMode").label}`,`🧰 <b style='color:#c4b5fd'>撮影プリセット</b>：${state.shootingPreset&&state.shootingPreset!=="custom"?(document.querySelector('#shootingPresetSelect option[value="'+state.shootingPreset+'"]')?.textContent||state.shootingPreset):state.shootingPreset==="custom"?"カスタム（個別調整中）":"未選択"}`,`🌿 <b style='color:#c4b5fd'>写真の作り込み度</b>：${find("photoStyle").label}`,`🎯 <b style='color:#c4b5fd'>表現の主役</b>：${resolvedVisualFocusLabel()}`,`💨 <b style='color:#c4b5fd'>身体の動き</b>：${find("motionEnergy").label}`,`📸 <b style='color:#c4b5fd'>アングル</b>：${pickAngle().label}`,`🖼️ <b style='color:#c4b5fd'>写す範囲</b>：${find("visibleRange").label}`,`📐 <b style='color:#c4b5fd'>画面の傾き</b>：${find("cameraRoll").label}`,`🎞️ <b style='color:#c4b5fd'>フィルム</b>：${find("film").label||"未選択"}`,`✨ <b style='color:#c4b5fd'>エフェクト</b>：${state.effects.length?state.effects.map(k=>EFFECTS.find(e=>e.key===k)?.label).join("、"):"未選択"}`,`🌫️ <b style='color:#c4b5fd'>追加要素</b>：${state.additionalElements.length?state.additionalElements.map(k=>ADDITIONAL_ELEMENTS.find(e=>e.key===k)?.label).filter(Boolean).join("、"):"未選択"}`, `🔒 <b style='color:#c4b5fd'>後処理</b>：weight削除なし / 重複削除なし`].join("<br>");copyPromptToClipboard(true);document.getElementById("outputCard").scrollIntoView({behavior:"smooth"});}
function handleCopy(){copyPromptToClipboard(false)}
function copyPromptToClipboard(auto=false){const ta=document.getElementById("outputArea");if(!ta||!ta.value)return;ta.focus();ta.select();ta.setSelectionRange(0,ta.value.length);const ok=()=>showCopied(auto);const fallback=()=>{try{if(document.execCommand("copy"))ok()}catch(e){}};if(navigator.clipboard&&navigator.clipboard.writeText){navigator.clipboard.writeText(ta.value).then(ok).catch(fallback)}else fallback()}
function showCopied(auto=false){const btn=document.getElementById("btnCopy");btn.textContent=auto?"✓ 自動コピー済み":"✓ コピー済み";btn.classList.add("copied");setTimeout(()=>{btn.textContent="コピー";btn.classList.remove("copied")},2500)}
function handleReset(){state={...DEFAULT_STATE};document.getElementById("situation").value="";document.getElementById("metaCard").classList.add("hidden");document.getElementById("outputCard").classList.add("hidden");document.getElementById("outputArea").value="";renderAllOptionChips();}
document.addEventListener("DOMContentLoaded",()=>{updateClock();setInterval(updateClock,30000);renderAllOptionChips();});
</script>
</body>
</html>
