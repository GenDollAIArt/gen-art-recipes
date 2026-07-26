<!--
  Selfie Prompt Generator
  Version: 9.9.0
  Updated: 2026-07-26
  Changelog:
    v9.9.0 - プロンプト出力順とUIを「顔ID → 身体ID → コーディネート → ヘア → 場所／シーン → 天気／時間 → 完全一致357系 → 身体／衣装投影 → ポーズ／構図 → 表情／肌／接写 → 照明 → フィルム／トーン → エフェクト → 追加要素 → 出力 → 最終検証」へ再編。357系は支持方法・姿勢・高さ・方向・写す範囲・顔向き・視線の完全一致パターンIDを採用し、画像AIへは顔向き・視線・撮影腕・端末関係まで統合した単一ブロックだけを出力。独立FACE/Gazeおよび手・端末ブロックを廃止。真上料理構図へ「頭上直上手持ち × テーブル席座位 × 頭頂直上 × 上半身＋料理」の専用パターンを追加。UIを被写体、シーン・環境、構図・357系、被写体表現、画づくり・エフェクト、追加要素、出力へ整理し、全グループ初期クローズ。生成プロンプト直下へ診断情報を配置し、生成画像・プロンプト・診断情報を同一テストケースIDで管理する画像登録、期待値、画像評価、差異記録、テストケースJSON書き出しを追加。診断スキーマを2へ更新。
    v9.8.0 - OUTFIT REFERENCEへ「GARMENT-SUPPORTED BODY READABILITY — PRIORITY」を追加。固定身体の全体体積・前面／側面シルエットを最優先し、前方への布の押し出し、横幅、上半身からウエストへの体積変化を保持したうえで、布の張り・ゆとり・折れ・ドレープ・落ち方を解決する順序を明示。ゆったり・厚手・不透明な服でも固定体形が服越しに読み取れるようにしつつ、不自然な密着や細かな解剖学的輪郭の浮き出しを禁止。Image B OFF時にも被写体参照ONなら同じ衣服支持ルールを適用し、最終身体確認には短い衣服シルエット検証のみ追加。完成357系1,770件、診断コピー、参照・髪・シーン・効果ロジックは変更なし。
    v9.7.0 - 診断JSONのコピー処理をAndroidアプリ内ブラウザ・ローカルHTML・権限制限環境向けに修正。表示中の診断テキスト欄を使う同期コピーを最優先し、標準Clipboard API、実体のある一時テキスト欄の順で多段フォールバックする。標準APIが存在していても権限・セキュアコンテキスト等で拒否された場合に処理を終了せず次方式へ継続し、全方式失敗時は診断JSONを全選択した状態で手動コピー可能にする。コピー成功方式を診断ステータスへ表示。画像生成プロンプト、完成357系1,770件、身体Data、参照・衣装・髪・シーン・効果ロジックは変更なし。
    v9.6.1 - 固定セルフ撮影のため切替不能だった「撮影方式」UI・状態・独立CAMERA MODEブロックを削除し、セルフ撮影条件は各完成357系へ統合。全1,770件の完成357系に写す範囲別の厳密な画面下端・画面外部位・拡張禁止・動作継続ルールを追加し、シーンや背景・構図が店・小物・全身を見せるためにクロップを広げることを禁止。高位置俯瞰では見かけの短縮だけを許可し、A4〜A6由来の上半身前方奥行き・横方向量感・ウエストへの体積関係と衣服支持量を縮小しない身体Data保護を追加。診断の禁止語検出を第三者撮影語専用へ修正。
    v9.6.0 - 357系を「スマホ支持方法 × 被写体姿勢 × カメラ高さ × 被写体との方向 × 写す範囲」の成立済み組み合わせへ全面再構成。1,770件の組み合わせごとに完成プロンプトを事前登録し、生成時は該当する完成357系を1本だけ出力。高さ・方向・範囲の断片連結と独立したVISIBLE RANGEブロックを廃止。通常手持ち、身体沿い手持ち、膝・太もも上、テーブル下の膝上、テーブル、カウンター、座面、低い台、床・地面のセルフ撮影へ対応。撮影方式をセルフ撮影専用へ統一。身体Dataは選択された部位形態のみを出力し、カメラ条件を再説明しない。診断JSONは完成357 ID、5条件、単一プロンプト数、範囲統合、禁止撮影語を記録。
    v9.5.0 - 画像生成プロンプトへ混入しない357系診断レイヤーを追加。各完成アングルへ高さ・被写体に対する方向・距離・光軸・撮影方式互換性の診断メタデータを付与し、生成済みプロンプトのブロック数・実出力順・予期しないカメラ見出しを確認可能にした。診断JSONのコピー、クリップボード貼り付け、手動貼り付け、差分確認、設定復元、診断のみ表示を実装し、身体Dataプロフィール等の派生値は直接復元せず現行ロジックで再計算する。選択系カードを上位アコーディオンへ統一し、起動時・リセット時は全閉じ、閉じた見出しに現在値を表示。内側の分類アコーディオンも初期全閉じへ変更。撮影方式の初期値を自撮りONへ変更。357系完成プロンプト、画像生成ブロック内容、A1顔ID、A4〜A9身体ID、Image B、月別ヘア、写す範囲、撮影腕、エフェクト定義は維持。
    v9.4.5 - A4〜A6を単純平均や方向別の別身体として扱わず、正面・45度・横の3投影が共同で定義する一つの上半身形態として再整理。A4は横幅とウエストへの比率、A5は前後奥行きと横方向量感の同時確認、A6は前後最大奥行きと側面外形を担い、どの一枚の明確な寸法も小さい妥協値へ平均化しない。357系の完成アングル定義は変更せず、正面・斜め・真横を明示する一部アングルでのみ、A4／A5／A6を「投影照合の主参照」として選び、他2枚を必須の三次元整合確認に使用。主参照は身体IDを再解析・切替するものではなく、固定済み単一身体の見え方を検証するだけ。生成UIとサマリーへ投影照合参照を追加し、服の完成外形と最終身体確認も同じ参照へ照合。顔ID、A7〜A9全身接続、写す範囲×アングルData合成、月別ヘア、Image B、357系定義、出力署名は維持。
    v9.4.4 - A4〜A9の単一身体IDを維持しながら、部位別の参照権限を明確化。A4〜A6を上半身形態の高詳細・確定ソース、A7〜A9を全身比率と接続整合の確認ソースとして固定し、A7〜A9や一般体形によるA4〜A6の平均化・拡大・縮小・置換を禁止。写す範囲Dataでは上半身が必要な場合にA4〜A6で確定した形・大きさ・前後奥行き・横方向量感・縦位置・胸郭／ウエストとの関係を参照相対で保持。Image Bの服は、その解析結果を増減せず完成外形へ反映し、ゆったり・不透明な布でも細部だけを隠して全体量感を平均化しない。最終身体確認も上半身はA4〜A6、全身接続はA7〜A9へ分離。357系定義、身体Data合成、顔ID、月別ヘア、表情・エフェクト、出力署名は維持。
    v9.4.3 - 写す範囲Dataと357系アングル投影Dataの合成方式を維持したまま、上半身が写る範囲でA4〜A9由来の胸郭対上半身比、前後奥行き、横方向量感、上半身からウエストへの移行を明示。横方向投影では固定身体の前後奥行きと側面シルエットを保持し、一般的な平たい胴体への置換を防止。Image Bのゆったりした服も固定身体の胸郭・上半身量感に支えられた前面／側面シルエットとしてドレープさせ、平たいテント状の布や小さい一般体形への再構築を禁止。身体の向きUIや357系への方向ロックは追加せず、カメラ位置・顔向き・シーンから自然に解釈させる。357系定義、顔ID、身体Data合成、表情・エフェクト、表示設定、出力署名は維持。
    v9.4.2 - 身体Data選別を、単一プロフィールの早期return方式から「写す範囲で必要な身体領域Data」＋「選択357系アングルの投影Data」を必ず合成する方式へ修正。低位置・身体沿い、俯瞰、横方向、地面付近を選んでも写す範囲Dataを失わず、重複アングル特性は短く合成する。UIは写す身体領域とアングル投影を別表示し、生成サマリーと最終身体確認も同じ2層構造へ追従。357系定義、A1顔ID、A4〜A9単一身体ID、Image B、月別ヘア、場所・シーン、エフェクトは変更なし。生成画像の最下部中央へ「GEN-DOLL Ver 9.4.2」を透過70%（不透明度30%）・極小文字で入れる出力署名指示を追加。
    v9.4.1 - 最大文字サイズ時に横余白までrem連動で大きくなっていたため、画面外側の左右余白とカード内側の左右余白を従来の半分へ縮小。上下余白、文字サイズ、ボタン高さ、357系、参照・生成ロジックは変更なし。
    v9.4.0 - UI全体の表示文字サイズを4段階化し、初期値を「最大（旧版の約2倍）」へ変更。表示設定を端末内へ保存。長押しヘルプの判定時間を700／900／1200／1500msから選択可能にし、初期値を900msへ変更。指が12px以上動いた時、スクロール時、離した時は長押しをキャンセルし、長押し後の通常タップ重複を防止。表情を笑顔／落ち着き／眠り・眠気／感情／遊び・SNSに分類し、安らかな寝顔、深い睡眠、うとうと、寝落ち直前、寝起き、目を閉じて休む、目を閉じた微笑み、あくび等を追加。睡眠系選択時は視線を「目を閉じる／視線なし」へ自動連動。既存と新規エフェクトを光・照明／レンズ・光学／ピント・奥行き／空気・大気／動き・ブレ／カメラ・端末／色処理／質感・仕上げの8分類へ再編し、自然・リング状・映画的レンズフレア、フレアゴースト、ハレーション、ブルーム、アナモルフィック光筋、窓光、逆光各種、端末特性等を追加。相性ガードと実行計画も分類へ追従。357系定義、A1顔ID、A4〜A9身体ID、写す範囲×アングルData選別、参照運用は変更なし。
    v9.3.2 - A4〜A9の身体Data出力を「写す範囲 × 選択357系アングル」で自動選別する方式へ変更。共通CANONICAL BODY IDは短い一度だけの固定文へ圧縮し、顔中心・俯瞰上半身・横方向奥行き・上半身・体幹骨盤・全身・低位置身体沿い・地面脚→顔の各投影プロファイルから今回必要な1ブロックだけを出力。顔アップでも真上／頭上斜め／高角度では頭–首–肩–胸郭–上半身の関係を残し、低位置・身体沿いアングルでは画面外を含む近接身体経路を保持。Image Bと最終身体確認の重複形態列挙を短文化。UIへ現在の身体Data選別結果を表示し、生成サマリーにも投影プロファイルを追加。既存357系アングル定義、顔ID、月別ヘア、場所・シーン、撮影腕、プリセットは変更なし。
    v9.3.1 - A4〜A9の身体投影をコンパクトコアのまま強化。身体IDへ参照由来のバスト対胸郭比、前方量感、下側輪郭、脇側量感、縦位置、バストからウエストへの落差を一度だけ明記。高角度・真上俯瞰は固定身体への短縮投影として扱い、見えている上半身を平坦化・縮小しない規則を追加。Image Bの服は固定量感の上へ沿わせ、覆いやゆとりで表面詳細が弱まっても基礎の幅・突出・輪郭・シルエットを減らさない。最終身体確認も同じ要点へ短く更新。UIの被写体説明と生成サマリーへ「A4〜A9体形投影保持」を表示。既存357系アングル定義、プリセット、シーン・場所、顔ID、月別ヘア、撮影腕は変更なし。
    v9.3.0 - 生成プロンプトをコンパクトコア方式へ再編。A1顔ID、A4〜A9単一身体ID、バスト–ウエスト–ヒップ関係を維持したまま、重複していた身体読取・再解釈禁止・服との分離・最終検証を短い中核ブロックへ統合。Image B、場所画像C、シーン本文の役割も簡潔に分離し、場所Cは空間の基準、シーン本文は今回の場所の使い方・姿勢・行動・小物の基準として整理。UIは撮影方式→今回のシーン→場所画像C参照の順へ変更し、構図プリセットに「真上から被写体とテーブル上の料理」と「頭上斜めから被写体とテーブル上の料理」を分離追加。生成結果サマリーへ文字数を表示。既存357系アングル定義、撮影腕、顔向き・視線、月別ヘア、参照ファイル運用は維持。
    v9.2.2 - UI配置を整理し、「① 今回のシーンだけ（日本語で入力）」を「撮影方式 — 自撮り / セルフ撮影」の直下へ移動。撮影方式を決めた直後に場所・姿勢・身体支持・行動・表情・小物を記述でき、その後に目的・表現プリセットと個別設定を選ぶ流れへ変更。生成ロジック、シーン連動チェック、プリセット内容、A1顔ID、A4〜A9単一身体ID、バスト–ウエスト–ヒップ関係、月別ヘア、Image B、既存357系定義は変更なし。場所参照と撮影方式の古い説明文も現行仕様に合わせて整理。
    v9.2.1 - 目的・表現プリセットへ「構図」分類を追加し、「上から被写体とテーブル上の料理」を新設。既存357系の「頭の真上から」を選択し、被写体＋食べ物、バランス構図、水平、上向きの顔、レンズへのチラ見、自然な動き、自然肌、軽いスマホHDRを一括設定する。シーン本文へ料理・食器・テーブルを自動追加せず、テーブルと料理の記述が不足している場合はシーン連動チェックで生成を停止。顔向きへ「上を向く／斜め上を向く」、視線へ「レンズをチラ見／横目でレンズをチラ見」を追加。A1顔ID、A4〜A9単一身体ID、バスト–ウエスト–ヒップ関係、月別ヘア、Image B、自撮り設定、既存357系定義は維持。
    v9.2.0 - 「目的・表現プリセット」を新設し、伸びる／リアル／日常／モデル／ファッション／ムービーの6分類・48種類を追加。プリセットは既存UIのアングル、写す範囲、画面傾き、顔向き、視線、表情、身体の動き、構図、光・フィルム・トーン、エフェクト、追加要素、肌・接写質感だけを一括選択し、シーン本文や小物は変更しない。撮影方式設定を維持し、対応する既存357系アングルを選ぶだけで、357系定義自体は完全維持。A1顔ID、A4〜A9単一身体ID、バスト–ウエスト–ヒップ関係、月別ヘア、Image B、参照モードをプリセットの変更対象外とするIDENTITY FIREWALLを実装。旧「撮影プリセット」の定数・状態・UI・処理を削除し、適用中／カスタム表示、再適用、解除、変更項目確認を追加。未使用の汎用細身人物ロック残骸も削除。
    v9.1.4 - 身体形態の処理を、撮影方向ごとに主参照を切り替えて再解釈する方式から、A4〜A9を同時に統合して一度だけ確定する単一のCANONICAL BODY ID方式へ全面置換。方向別優先参照の定数・関数・生成文・最終検証文を完全削除し、正面・45度・真横を同じ固定三次元身体の別投影として扱う。バスト–ウエスト–骨盤・ヒップ–太腿の相互比率、縦位置、幅・奥行き、肩・胸郭・四肢との関係をcross-view invariantとして固定。Image Bの服は固定身体へ合わせ、シーンのポーズと357系遠近は身体IDを再計算せず後から適用。末尾検証も方向別照合から単一身体IDとの整合確認へ置換。その他の顔ID、月別ヘア、撮影腕・手役割、服装・場所参照、構図、エフェクトは維持。
    v9.1.3 - 被写体身体形態の参照読取を全面強化。身体ラインが明確なA4〜A9を補正推測せず直接・忠実に読み、A4〜A6を上半身、A7〜A9を全身の主参照として正面・45度・真横の役割を明文化。バスト、ウエスト、骨盤・ヒップ、四肢、全身比率を独立した固定対象として追加し、バスト→ウエスト→骨盤・ヒップ→太腿を一続きの三次元構造として保持。選択アングルの方向に近い参照を主にし、他方向を幅・奥行き・位置関係の確認に使う方向別参照を追加。Image Bのモデル・マネキン・商品シルエットから身体を再定義しない分離を強化し、357系遠近は固定身体への投影として扱う。末尾にA4〜A9基準の最終身体形態検証を追加。その他の顔ID、月別ヘア、撮影腕・手役割、服装・場所参照、構図、エフェクトは維持。
    v9.1.2 - 自撮り時の手の役割と357系身体沿いアングルの優先順位を再整理。撮影スマートフォンを撮影手が持つ唯一の端末として固定し、端末自体はそのレンズから生成される画面内へ写さない。反対側の手によるスマートフォン・第2端末・リモコン保持を禁止し、空いている手はシーン上の身体支持または非スマートフォン小物を優先し、それ以外は「身体の動き / 躍動感」へ連動。身体沿い自撮りでは撮影腕を腹部・腰・ヒップ・脇腹の選択ラインへ密着させ、腕をレンズ前へ突き出す通常セルフィー化、大きな前景腕、中央を横切る腕を禁止。生成順をカメラ方式→完成アングル→手役割→躍動感へ変更し、最終手役割検証を追加。その他の参照、月別ヘア、服装・場所参照、構図、エフェクトは維持。
    v9.1.1 - アングル選択時は選択したアングルが属する分類だけを開いた状態で残し、他のアングル分類を自動で閉じるよう変更。被写体設定のOFFを「参照なし」へ整理し、OFF時の被写体テキスト入力欄・初期化ボタン・テキスト由来の被写体定義を削除。ON時のA1〜A9参照、顔ID・体型の役割分離、月別ヘア、服装・場所参照、357系angle-core、シーン連動、エフェクト定義は維持。
    v9.1.0 - 357系angle-coreの全アングル定義を再整理。各選択肢を完成済み撮影形として、カメラ位置・被写体との距離・方向・光軸・遠近感の順に統一し、写す範囲・背景・余白・画面傾きが選択アングルを別構図へ変えない共通ロックを追加。腰位置／腰下の身体沿いアングルには、身体との近接距離、前景となる腹部・腰・脇腹、胴体から顔へ続くライン、自撮り腕とカメラ位置を固定する専用ロックを追加。覗き込み3種では角度専用の顔向き・視線を実際の出力へ適用。UIはアングルを7系統の折りたたみ分類へ再編。追加要素／空間演出は全項目を維持したまま8系統の折りたたみ分類へ分け、生成プロンプトの実行計画も同じ分類へ統一。被写体・顔ID・月別ヘア・服装・場所参照・シーン連動・エフェクト定義は維持。
    v9.0.11 - 「表現の主役」で被写体＋飲み物／被写体＋食べ物／被写体＋テーブル上を選択した場合、⑮「背景の見せ方」を指定なしへ自動固定し、控えめ・バランス・下／足元側・奥・上を選択不可に変更。テーブル上の前景〜中景は表現の主役側だけで制御し、背景指定との重複を防止。その他の顔ID、月別ヘア、357系アングル、撮影腕ロック、シーン連動、エフェクトは維持。
    v9.0.10 - 顔ID参照の役割を再整理。A1を顔の唯一の主参照、A2〜A3を同一人物の角度確認専用、A4〜A9を身体形態専用として明示し、A4〜A9の顔情報による平均化・再設計を禁止。顔のみ／顔どアップ／顔アップ／横顔アップでは、背景・服・場所・テーブル上などの構図優先を自動抑制し、顔クロップを唯一の構図主役として出力。プロンプト末尾にA1基準の最終顔ID検証を追加。月別ヘア、357系アングル、撮影腕ロック、シーン連動、エフェクトは維持。
    v9.0.7 - v9.0.6の月別ヘアを表示だけでなく生成時にも厳格適用するよう強化。月別ヘアを髪に関する唯一の指定元として明示し、A1〜A9・Image B・シーンから髪の長さ、カット、色、シルエット、結び方を継承・混合しないロックを追加。各月ごとに長さ境界を明文化し、6〜8月のボブでは肩・胸・背中・枕まで伸びる長髪、ポニーテール、編み込み、まとめ髪を禁止。その他のUI、角度、シーン連動、被写体・服装・場所参照、エフェクトは変更なし。
    v9.0.6 - v9.0.5をベースに「シーン連動チェック」を追加。シーン文・撮影方式・写す範囲との成立条件が不足する選択肢をグレー表示で選択不可にし、選択後に条件が失われた場合は赤色の不整合表示として生成を停止する。カメラ位置 / アングルへ「地面付近・前脚→顔ライン自撮り」を追加し、シーン文に低い姿勢と前景脚の記述、写す範囲に全身、自撮り条件がそろった場合のみ使用可能にした。テーブル / カウンター肘つき前傾、振り向き、歩き、被写体＋飲み物 / 食べ物 / テーブル上、自然 / 強い躍動感にも明確なシーン成立条件を追加。被写体・服装・場所参照、月別ヘア、既存エフェクト定義は変更なし。
    v9.0.5 - v9.0.4の月別ヘア表示不具合を修正。東京時間カードに「今月のヘアスタイル」を日本語で明示し、現在月・髪型・色・長さを確認できる表示へ変更。生成プロンプトのHAIRブロックに文字列として混入していたバックスラッシュ付きnを正しい改行へ修正。月別ヘアの内部プロンプト、A1〜A9より月別ヘアを優先するルール、その他の機能・選択肢は変更なし。
    v9.0.4 - v9.0.3をベースに分類重複を整理。独立した「基本姿勢」をUI・状態・生成ブロックから削除し、立つ・座る・横になる・前傾・身体の支えはシーン文を唯一の指定元として扱う物理整合ルールをSCENEへ自動追加。既存の「テンション（動きの強さ）」を「身体の動き / 躍動感」へ置換し、おまかせ・わずかな自然な動き・自然な躍動感・強い躍動感の4段階へ整理。「表現の主役」へ被写体＋飲み物・被写体＋食べ物・被写体＋テーブル上を追加し、シーンに存在しない物を勝手に追加しない構図ルールを付与。v3.57系angle-core、6種類の腰下超強煽り、被写体・服装・場所参照、表情、既存エフェクトは変更なし。
    v9.0.3 - v9.0.2をベースに、腰下・体沿い超強煽りをv3.57系の完成済みアングルとして6種類へ再整理。正面沿い・斜め沿い・真横沿いの通常版3種と、各方向で低いカメラを覗き込む版3種を追加。覗き込み版では、低いレンズを見下ろす顔向き・視線・自然な顎引きを角度プリセット側で固定し、胴体方向は各方向を維持。その他の機能・参照・分類は変更なし。
    v9.0.2 - v9.0.1をベースに、テーブル / カウンター系の肘つき前傾アングルを「片肘つき」と「両肘つき」に分離。自撮り時は両肘つき前傾を選択不可にし、セルフ撮影時のみ選択可能に調整。自撮りのときに両肘つきという物理的に不自然な状態を避けつつ、従来のv3.57系angle-core構造・被写体参照・服装参照・場所参照・既存分類は維持。
    v9.0.0 - v8.0.34のangle-core / v3.57系思想を維持した正式再編版。「写真の自然さ / 演出度」を「写真の作り込み度」へ改称し、「撮影スタイル / 表現方向」を「表現の主役（人物・服・背景・バランス）」へ置換。被写体サイズ / 余白にAUTO（表現の主役に連動）を追加。カメラ位置 / アングルは完成済みプリセット方式を維持し、「腰下・体沿い超強煽り」の正面・斜め・真横を追加。撮影プリセットは自撮り／セルフ撮影を自動反映し、適用後の個別変更も可能。シーン・人数・場所・被写体参照・体型ロック・服装参照・場所参照・既存エフェクト定義は変更なし。
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
    v8.0.3 - 写す範囲を厳格化。自撮りON時のセルフ撮影への逃げを防止。
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
<html lang="ja" data-font-size="max">
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
  html[data-font-size="standard"]{font-size:87.5%}
  html[data-font-size="large"]{font-size:112.5%}
  html[data-font-size="xlarge"]{font-size:137.5%}
  html[data-font-size="max"]{font-size:175%}
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,BlinkMacSystemFont,'Hiragino Kaku Gothic ProN','Noto Sans JP',sans-serif;padding-bottom:80px;font-size:1rem}
  .header{background:var(--hdr-bg);border-bottom:1px solid var(--border);padding:16px 14px 12px;position:sticky;top:0;z-index:10;display:flex;align-items:center;gap:10px}
  .header-icon{width:2.15rem;height:2.15rem;border-radius:8px;background:linear-gradient(135deg,#7c3aed,#a855f7);display:flex;align-items:center;justify-content:center;font-size:1.071rem;flex-shrink:0}
  .header-title{font-size:1.071rem;font-weight:700}.header-sub{font-size:.714rem;color:var(--text-hint);margin-top:1px}.header-time{margin-left:auto;text-align:right}.header-time-main{font-size:.929rem;color:#a855f7;font-weight:700}.header-time-sub{font-size:.714rem;color:var(--text-hint)}
  .content{padding:.86rem .5rem 0}.card{background:var(--bg-card);border:1px solid var(--border);border-radius:14px;padding:1rem .5rem;margin-bottom:.72rem}.card-dark{background:var(--bg-dark);border-color:var(--border-pu)}.card-out{background:var(--bg-out);border-color:var(--border-pu)}
  .slabel{font-size:.714rem;font-weight:700;letter-spacing:.12em;color:var(--text-dim);text-transform:uppercase;margin-bottom:8px}.hint{font-size:.786rem;color:var(--text-hint);margin-bottom:8px;line-height:1.55}
  .chips{display:flex;flex-direction:column;align-items:stretch;gap:8px}.chip{width:100%;min-height:3rem;padding:.72rem .92rem;line-height:1.45;touch-action:manipulation;border-radius:12px;text-align:left;border:2px solid var(--border-m);background:var(--chip-bg);color:var(--chip-col);font-size:.857rem;cursor:pointer;transition:all .15s;-webkit-tap-highlight-color:transparent;user-select:none}.chip.active{border-color:var(--chip-abdr);background:var(--chip-abg);color:var(--chip-acol);font-weight:600}.chip.disabled{opacity:.35;cursor:not-allowed;filter:grayscale(.6)}.chip.invalid{border-color:#dc2626;background:#fef2f2;color:#b91c1c;font-weight:700}.chip.has-help::after{content:"？";display:inline-flex;align-items:center;justify-content:center;width:15px;height:15px;margin-left:5px;border-radius:999px;font-size:.714rem;color:#c4b5fd;background:rgba(168,85,247,.18);border:1px solid rgba(196,181,253,.35)}
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

  .visual-preset-status{margin:10px 0 12px;padding:11px 12px;border:1px solid #ddd6fe;border-radius:12px;background:#f5f3ff;color:#5b21b6;font-size:.82rem;line-height:1.55}
  .visual-preset-status.custom{background:#fff7ed;border-color:#fed7aa;color:#9a3412}
  .visual-preset-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:9px}
  .visual-preset-card{appearance:none;width:100%;text-align:left;border:1px solid #e4e4e7;border-radius:13px;background:#fff;padding:11px 12px;cursor:pointer;transition:.16s ease;box-shadow:0 1px 2px rgba(0,0,0,.03)}
  .visual-preset-card:hover{border-color:#a78bfa;transform:translateY(-1px)}
  .visual-preset-card.active{border-color:#7c3aed;background:#f5f3ff;box-shadow:0 0 0 2px rgba(124,58,237,.12)}
  .visual-preset-card.custom{border-color:#f97316;background:#fff7ed}
  .visual-preset-name{display:block;color:#18181b;font-size:.9rem;font-weight:800;line-height:1.35}
  .visual-preset-summary{display:block;margin-top:5px;color:#71717a;font-size:.74rem;line-height:1.5}
  .visual-preset-mode{display:block;margin-top:6px;color:#7c3aed;font-size:.7rem;font-weight:700}
  .visual-preset-actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
  .visual-preset-actions button{border:1px solid #d4d4d8;border-radius:10px;background:#fff;color:#3f3f46;padding:8px 11px;font-size:.76rem;font-weight:700;cursor:pointer}
  .visual-preset-actions button:disabled{opacity:.42;cursor:not-allowed}
  .selection-accordion{padding:0;overflow:hidden}
  .selection-accordion>.section-summary,.diagnostic-card>.section-summary{list-style:none;display:flex;align-items:center;gap:10px;padding:1rem .62rem;cursor:pointer;user-select:none}
  .selection-accordion>.section-summary::-webkit-details-marker,.diagnostic-card>.section-summary::-webkit-details-marker{display:none}
  .selection-accordion>.section-summary::before,.diagnostic-card>.section-summary::before{content:"＋";display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;border-radius:999px;background:#ede9fe;color:#7c3aed;font-size:.857rem;font-weight:800;flex-shrink:0}
  .selection-accordion[open]>.section-summary::before,.diagnostic-card[open]>.section-summary::before{content:"−"}
  .selection-accordion[open]>.section-summary,.diagnostic-card[open]>.section-summary{border-bottom:1px solid var(--border)}
  .section-title{flex:1;min-width:0;font-weight:700;color:var(--text);font-size:.929rem;line-height:1.4}
  .section-current{max-width:48%;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;text-align:right;color:var(--text-pu);font-size:.786rem;font-weight:700}
  .section-body{padding:1rem .5rem}
  .diagnostic-card{padding:0;overflow:hidden}
  .diagnostic-grid{display:grid;grid-template-columns:1fr;gap:10px}
  .diagnostic-area{width:100%;min-height:210px;font-size:.75rem;color:var(--text-sub);line-height:1.6;font-family:monospace;background:var(--bg-ta);border-radius:10px;padding:10px 12px;border:1px solid var(--border);resize:vertical;outline:none}
  .diagnostic-actions{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:8px}
  .diagnostic-actions button{border:1px solid var(--border-m);border-radius:10px;padding:10px 8px;background:var(--bg-card);color:var(--text-sub);font-size:.786rem;font-weight:700;cursor:pointer}
  .diagnostic-actions button.primary{background:#7c3aed;border-color:#7c3aed;color:#fff}
  .diagnostic-actions button:disabled{opacity:.42;cursor:not-allowed}
  .diagnostic-toggle{display:flex;align-items:center;gap:8px;font-size:.786rem;color:var(--text-sub);line-height:1.5}
  .diagnostic-status,.diagnostic-diff{white-space:pre-wrap;border:1px solid var(--border);border-radius:10px;padding:10px 12px;background:var(--bg-input);font-size:.75rem;line-height:1.65;color:var(--text-sub)}
  .diagnostic-status.ok{border-color:#86efac;background:#f0fdf4;color:#166534}.diagnostic-status.error{border-color:#fca5a5;background:#fef2f2;color:#991b1b}
  .diagnostic-diff{max-height:260px;overflow:auto}.diagnostic-diff:empty{display:none}
  .ui-pref-grid{display:grid;grid-template-columns:1fr;gap:.8rem}
  .ui-pref-block{border:1px solid var(--border);border-radius:12px;padding:.8rem;background:#fafafa}
  .ui-pref-title{font-size:.93rem;font-weight:800;color:var(--text-sub);margin-bottom:.35rem}
  .ui-pref-note{font-size:.78rem;line-height:1.55;color:var(--text-hint);margin-bottom:.55rem}
  .ui-pref-chips{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:.5rem}
  .ui-pref-chip{appearance:none;border:2px solid var(--border-m);border-radius:11px;background:#fff;color:var(--text-sub);padding:.68rem .55rem;font-size:.84rem;font-weight:750;line-height:1.35;cursor:pointer;touch-action:manipulation}
  .ui-pref-chip.active{border-color:var(--chip-abdr);background:var(--chip-abg);color:var(--chip-acol)}
  .ui-pref-current{margin-top:.55rem;font-size:.76rem;color:#6d28d9;font-weight:700;line-height:1.5}
  @media (max-width:520px){
    .header{align-items:flex-start;flex-wrap:wrap}.header-time{width:100%;margin-left:0;text-align:left;display:flex;gap:.5rem;align-items:baseline}
    .btn-row{flex-direction:column}.btn-generate,.btn-reset{width:100%;flex:auto}
    .ui-pref-chips{grid-template-columns:1fr}
    .visual-preset-grid{grid-template-columns:1fr}
  }

  .v99-group{padding:0!important;overflow:hidden}
  .v99-group>.section-summary{padding:1rem 1.05rem;background:linear-gradient(135deg,#faf5ff,#f5f3ff);border-bottom:0}
  .v99-group[open]>.section-summary{border-bottom:1px solid var(--border-m)}
  .v99-group>.section-body{padding:.75rem;background:#f8fafc}
  .v99-group>.section-body>.card,.v99-group>.section-body>details.card{margin:.65rem 0}
  .test-case-grid{display:grid;gap:.8rem}
  .test-image-drop{border:2px dashed #c4b5fd;border-radius:14px;background:#faf5ff;padding:1rem;text-align:center}
  .test-image-preview{display:none;max-width:100%;max-height:560px;margin:.8rem auto 0;border-radius:12px;box-shadow:0 8px 24px rgba(15,23,42,.16)}
  .test-image-preview.visible{display:block}
  .test-image-meta,.test-diff-summary{white-space:pre-wrap;font-size:.78rem;line-height:1.65;color:#52525b;background:#fff;border:1px solid var(--border-m);border-radius:10px;padding:.75rem}
  .eval-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:.65rem}
  .eval-item{background:#fff;border:1px solid var(--border-m);border-radius:10px;padding:.7rem}
  .eval-item label{display:block;font-size:.76rem;font-weight:800;color:#4c1d95;margin-bottom:.35rem}
  .eval-item input{width:100%;box-sizing:border-box;border:1px solid var(--border-m);border-radius:8px;padding:.55rem;font-size:.9rem}
  .eval-item textarea{width:100%;box-sizing:border-box;min-height:5rem;border:1px solid var(--border-m);border-radius:8px;padding:.55rem;font-size:.82rem;resize:vertical}
  .test-case-actions{display:flex;flex-wrap:wrap;gap:.55rem}
  .test-case-actions button{appearance:none;border:1px solid var(--border-m);border-radius:10px;background:#fff;padding:.65rem .8rem;font-weight:800;color:#5b21b6}
  .test-case-actions button.primary{background:#6d28d9;color:#fff;border-color:#6d28d9}
  .prompt-order-note{font-size:.74rem;line-height:1.55;color:#6b7280;margin:.3rem 0 .7rem}
  @media(max-width:520px){.eval-grid{grid-template-columns:1fr}}

</style>
</head>
<body>
<div class="header">
  <div class="header-icon">✦</div>
  <div><div class="header-title">Stable Character Prompt Generator</div><div class="header-sub">v9.9.0</div><div class="header-sub">顔・身体・コーデ固定 × 完全一致357系 × 画像テスト診断</div></div>
  <div class="header-time"><div class="header-time-main" id="hTime">--:--</div><div class="header-time-sub" id="hDay">-- · --月 · --</div></div>
</div>
<div class="content">
  <div class="card card-dark"><div class="slabel">自動取得 — 東京時間</div><div class="info-row"><span class="info-icon">📅</span><span id="infoDay">取得中…</span></div><div class="info-row"><span class="info-icon">🕐</span><span id="infoTime">取得中…</span></div><div class="info-row"><span class="info-icon">💭</span><span id="infoDayMood" style="font-size:.786rem;color:#71717a;"></span></div><div class="info-row"><span class="info-icon">✂️</span><span><span style="font-size:.786rem;color:#71717a;">今月のヘアスタイル</span><br><span id="infoHair" style="font-size:.857rem;"></span></span></div></div>

  <div class="card" id="uiPreferencesCard"><div class="slabel">表示・操作設定</div><div class="hint">文字サイズと長押しヘルプの反応時間を変更できます。設定はこの端末へ保存され、プロンプト内容には影響しません。</div>
    <div class="ui-pref-grid">
      <div class="ui-pref-block"><div class="ui-pref-title">表示文字サイズ</div><div class="ui-pref-note">初期値は「最大」。旧版の文字サイズのおよそ2倍です。</div><div class="ui-pref-chips" id="fontSizePreferenceChips"></div><div class="ui-pref-current" id="fontSizePreferenceStatus"></div></div>
      <div class="ui-pref-block"><div class="ui-pref-title">長押し判定時間</div><div class="ui-pref-note">説明ヘルプが開くまでの時間。スクロールや指の移動時は発動しません。</div><div class="ui-pref-chips" id="longPressPreferenceChips"></div><div class="ui-pref-current" id="longPressPreferenceStatus"></div></div>
    </div>
  </div>

  <div class="card card-dark"><div class="slabel">被写体設定 — 9枚画像参照</div><div class="hint">OFFは被写体画像参照を使用せず、被写体テキストも追加しません。ONはA1〜A9から単一の三次元身体IDを一度だけ固定します。A1が顔ID、A4〜A6が上半身形態の高詳細・確定ソース、A7〜A9が全身比率と身体接続の確認ソースです。A7〜A9でA4〜A6の上半身を平均化・拡大・縮小しません。生成時は「写す範囲Data × 選択した357系アングルData」を合成し、今回必要な身体Dataだけを出力します。服はA4〜A6で確定した上半身形態を増減せず、服を着た完成外形へ反映します。髪型・ポーズ・構図・背景はA1〜A9から参照しません。</div><div class="slabel" style="margin-top:10px;">被写体A1〜A9画像参照</div><div class="chips" id="characterModeChips"></div></div>

  <div class="card card-dark"><div class="slabel">コーデ画像B参照（被写体9枚の後に最後の1枚）</div><div class="hint">OFFはシーンに合うコーディネートをおまかせで作成します。ONは被写体A1〜A9の後に最後の1枚として添付したコーデ画像Bを使用します。服・靴・バッグ・アクセサリー・配色をFULL相当で厳格に使用します。コーディネートシートの場合も、枠やテンプレデザインは生成画像に持ち込みません。</div><div class="chips" id="outfitReferenceModeChips"></div></div>

  <div class="card" id="sceneCard"><div class="slabel">① 今回のシーン（場所・姿勢・行動・小物）</div><div class="hint">今回の場所、場所のどこにいるか、姿勢、身体の支え、行動、表情、料理・飲み物・PCなどの小物を書きます。場所画像CがONでも、今回の使い方や小物はここを基準にします。成立条件が不足する選択肢は自動で無効になります。</div><textarea id="situation" rows="5" placeholder="例：窓際のカフェ席。テーブルに座り、料理を前に片手で自撮り。空いた手は皿の横に添える。" oninput="handleSituationInput()"></textarea><div class="validation-status" id="sceneValidationStatus">シーン連動チェック：場所・姿勢・行動・小物を入力すると、成立しない選択肢を自動で無効化します。</div></div>

  <div class="card card-dark"><div class="slabel">場所画像C参照（任意・シーンの場所補助）</div><div class="hint">OFFは上のシーン文章だけで場所を作ります。ONは画像Cから建築・素材・空間構成・植栽・設備・環境光だけを読み、上のシーン文章に合わせて再構築します。画像Cの人物・服・ポーズ・撮影構図は使いません。</div><div class="chips" id="locationReferenceModeChips"></div></div>

  <div class="card" id="visualPresetCard"><div class="slabel">目的・表現プリセット</div><div class="hint">「構図・伸びる・リアル・日常・モデル・ファッション・ムービー」から仕上がりを選び、既存の357系アングル・写す範囲・顔向き・視線・表情・構図・光・エフェクト・追加要素などを一括設定します。飲み物、ノートPC、バッグ、場所、行動などは追加せず、シーン本文をそのまま維持します。自撮り固定、A1顔ID、A4〜A9身体ID、バスト–ウエスト–ヒップ関係、月別ヘア、Image B、357系定義は変更しません。</div>
    <div class="visual-preset-status" id="visualPresetStatus">プリセット未選択。個別設定をそのまま使用します。</div>
    <div class="option-groups" id="visualPresetGroups"></div>
    <div class="visual-preset-actions">
      <button type="button" id="btnPresetReapply" onclick="reapplyVisualPreset()">再適用</button>
      <button type="button" id="btnPresetClear" onclick="clearVisualPreset()">解除（現在の設定は保持）</button>
      <button type="button" id="btnPresetDetails" onclick="showVisualPresetChanges()">変更項目を見る</button>
    </div>
  </div>

  <div class="card"><div class="slabel">写真の作り込み度</div><div class="hint">ラフな日常写真から作品撮りまで、写真をどの程度整えて作り込むかだけを選びます。カメラ位置や表現の主役とは独立しています。</div><div class="chips" id="photoStyleChips"></div></div>

  <div class="card"><div class="slabel">表現の主役</div><div class="hint">人物・服／コーデ・背景／場所に加え、被写体と飲み物・食べ物・テーブル上を一緒に見せる構図を選べます。シーンに存在しない料理や飲み物は追加しません。AUTOの被写体サイズ／余白は、この選択に連動します。</div><div class="chips" id="visualFocusChips"></div></div>


  <div class="card"><div class="slabel">② 天気を選択</div><div class="chips" id="weatherChips"></div></div>
  <div class="card"><div class="slabel">③ フィルムトーン / 質感</div><div class="hint">長押しでヘルプ表示。選んだトーンと相性の悪いエフェクトは自動解除され、選択不可になります。</div><div class="chips" id="filmChips"></div></div>
  <div class="card"><div class="slabel">④ 作品トーン</div><div class="hint">長押しでヘルプ表示。写真全体の印象を選びます。</div><div class="chips" id="toneChips"></div></div>
  <div class="card"><div class="slabel">⑤ エフェクト（種類別・複数選択可）</div><div class="hint">光・照明、レンズ・光学、ピント・奥行き、空気・大気、動き・ブレ、カメラ・端末、色処理、質感・仕上げの8分類です。見出しをタップして開閉し、長押しで意味を確認できます。相性の悪い組み合わせは自動で選択不可になります。</div><div class="option-groups" id="effectChips"></div></div>
  <div class="card"><div class="slabel">⑥ エフェクト強度</div><div class="hint">選択エフェクトのweightを倍率補正します。通常プロンプトには触りません。</div><div class="chips" id="effectStrengthChips"></div></div>
  <div class="card"><div class="slabel">⑦ 追加要素 / 空間演出（複数選択可）</div><div class="hint">全項目を8系統に分類しました。見出しをタップして開閉し、長押しで使い方を確認できます。後加工ではなく、シーン内に実在する光・空気・影・動く物・前景として配置します。合計2〜5個程度がおすすめです。</div><div class="option-groups" id="additionalElementChips"></div></div>
  <div class="card"><div class="slabel">⑧ 肌の見え方 / 肌質感</div><div class="chips" id="skinFinishChips"></div></div>
  <div class="card"><div class="slabel">⑨ 接写質感</div><div class="hint">顔のみ・顔どアップ・横顔アップで効きやすい質感です。</div><div class="chips" id="closeupTextureChips"></div></div>
  <div class="card"><div class="slabel">⑩-A スマホの支持方法</div><div class="hint">すべて被写体本人による1台のスマートフォンのセルフ撮影です。手持ち、身体沿い、膝上、テーブル、カウンター、座面、低い台、床・地面から選びます。</div><div class="chips" id="cameraSupportChips"></div></div>
  <div class="card"><div class="slabel">⑩-B 被写体の姿勢</div><div class="hint">支持方法と物理的に成立する姿勢だけを選択できます。シーン本文にも同じ姿勢・支えを書いてください。</div><div class="chips" id="cameraPostureChips"></div></div>
  <div class="card"><div class="slabel">⑩-C カメラの高さ</div><div class="hint">頭頂の真上から床・地面まで、身体または支持面を基準にした実レンズ位置です。支持方法・姿勢に対応する高さだけを表示します。</div><div class="chips" id="cameraHeightChips"></div></div>
  <div class="card"><div class="slabel">⑩-D 被写体との角度</div><div class="hint">正面、左右45度、左右真横、後方、肩越し振り返りまで、被写体とカメラの水平方向の関係を固定します。</div><div class="chips" id="cameraDirectionChips"></div></div>
  <div class="card"><div class="slabel">⑪ 写す範囲</div><div class="hint">選択した支持方法・姿勢・高さ・方向と一体化した完成357系を選びます。AIへ高さ・方向・範囲の断片を別々には渡しません。</div><div class="chips" id="visibleRangeChips"></div><div class="validation-status ok" id="camera357Status">完成357系：設定を確認中…</div><div class="validation-status ok" id="bodyProjectionStatus">身体Data：設定を確認中…</div></div>
  <div class="card"><div class="slabel">⑫ 画面の傾き</div><div class="hint">構図の回転だけを指定します。腰だめやローアングルの起点は変えません。</div><div class="chips" id="cameraRollChips"></div></div>
  <div class="card"><div class="slabel">⑬ 顔向き</div><div class="chips" id="faceDirectionChips"></div></div>
  <div class="card"><div class="slabel">⑭ 視線</div><div class="chips" id="gazeChips"></div></div>
  <div class="card"><div class="slabel">⑮ 背景の見せ方</div><div class="hint">店内・街・建築など、被写体の後方空間をどの程度見せるかを選びます。表現の主役が「被写体＋飲み物／食べ物／テーブル上」の場合は、重複を避けるため「指定なし」に自動固定されます。</div><div class="chips" id="backgroundViewChips"></div></div>
  <div class="card"><div class="slabel">⑯ 被写体サイズ / 余白</div><div class="chips" id="framingChips"></div></div>
  <div class="card"><div class="slabel">⑰ 身体の動き / 躍動感</div><div class="hint">立つ・座るなどの基本姿勢ではなく、その姿勢の中で髪・服・腕・上体がどの程度動いて見えるかを選びます。自撮り時は撮影腕をカメラ位置へ固定したまま、空いている手と上体の動きへ反映します。モーションブラーとは別の物理的な動きです。</div><div class="chips" id="motionEnergyChips"></div></div>
  <div class="card"><div class="slabel">⑱ 表情（カテゴリ別）</div><div class="hint">笑顔、落ち着き、眠り・眠気、感情、遊び・SNSに分類しています。睡眠系を選ぶと、視線は自動で「目を閉じる／視線なし」へ連動します。未選択の場合はシーン・時間・天気から自然に導出します。</div><div class="option-groups" id="expressionChips"></div></div>
  <div class="btn-row"><button class="btn-generate" id="btnGen" onclick="handleGenerate()">✦ プロンプト生成</button><button class="btn-reset" onclick="handleReset()">リセット</button></div>
  <details class="card diagnostic-card" id="diagnosticCard">
    <summary class="section-summary"><span class="section-title">357系・生成状態の診断</span><span class="section-current">画像生成プロンプトへ非混入</span></summary>
    <div class="section-body diagnostic-grid">
      <div class="hint">現在の選択、完成357系ID、生成プロンプトの実ブロック数と順番をJSONで記録します。基礎ジオメトリと顔向き・視線を含む完全一致357系ID、プロンプト順序、顔・身体・衣装・効果の期待値を記録します。診断情報そのものは画像生成用プロンプトへ追加されません。</div>
      <label class="diagnostic-toggle"><input type="checkbox" id="diagnosticIncludeScene"> 診断JSONへシーン本文を含める</label>
      <div class="diagnostic-actions">
        <button type="button" class="primary" onclick="handleDiagnosticCopy()">診断情報をコピー</button>
        <button type="button" onclick="handleDiagnosticPasteFromClipboard()">クリップボードから貼り付け</button>
        <button type="button" onclick="previewDiagnosticInput()">貼り付け内容を確認</button>
        <button type="button" onclick="clearDiagnosticPanel()">クリア</button>
      </div>
      <textarea class="diagnostic-area" id="diagnosticArea" placeholder="診断JSONをここへ貼り付けて『貼り付け内容を確認』を押します。"></textarea>
      <div class="diagnostic-status" id="diagnosticStatus">診断情報は未作成です。</div>
      <div class="diagnostic-diff" id="diagnosticDiff"></div>
      <div class="diagnostic-actions">
        <button type="button" class="primary" id="btnDiagnosticApply" onclick="applyPendingDiagnostic()" disabled>設定へ適用</button>
        <button type="button" id="btnDiagnosticDisplay" onclick="displayPendingDiagnostic()" disabled>診断だけ表示</button>
      </div>
    </div>
  </details>
  <div class="card card-dark hidden" id="metaCard"><div class="slabel">展開結果サマリー</div><div id="metaContent" style="font-size:.857rem;color:#a1a1aa;line-height:1.9;"></div></div>
  <div class="card card-out hidden" id="outputCard"><div class="card-head"><div class="slabel" style="margin-bottom:0;">生成プロンプト</div><button class="btn-copy" id="btnCopy" onclick="handleCopy()">コピー</button></div><textarea class="output-ta" id="outputArea" readonly onclick="this.select();this.setSelectionRange(0,this.value.length);" onfocus="this.select();this.setSelectionRange(0,this.value.length);"></textarea></div>
</div>
<div class="help-overlay hidden" id="chipHelpOverlay" onclick="hideChipHelp()"><div class="help-sheet" onclick="event.stopPropagation()"><div class="help-title" id="chipHelpTitle">ヘルプ</div><div class="help-body" id="chipHelpBody"></div><button class="help-close" onclick="hideChipHelp()">閉じる</button></div></div>
<script>
const APP_VERSION = "v9.9.0";
const OUTPUT_SIGNATURE_TEXT = `GEN-DOLL Ver ${APP_VERSION.replace(/^v/,"")}`;
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
const CHIN_CONTROL = "(neutral chin position:1.92), (chin not thrust forward:1.92), (no jutting chin:1.9), (face kept level or only naturally tilted:1.85), (neck relaxed and not stretched:1.82)";
const opt=(label,key,value,help="")=>({label,key,value,help});
const UI_PREFS_STORAGE_KEY="stable-character-prompt-generator-ui-v9.4";
const UI_FONT_SIZE_OPTIONS=[
  {key:"standard",label:"標準",description:"旧版と同じ"},
  {key:"large",label:"大きい",description:"約1.3倍"},
  {key:"xlarge",label:"かなり大きい",description:"約1.6倍"},
  {key:"max",label:"最大",description:"旧版の約2倍"}
];
const LONG_PRESS_DELAY_OPTIONS=[
  {key:700,label:"700ms",description:"やや速い"},
  {key:900,label:"900ms",description:"標準・初期値"},
  {key:1200,label:"1200ms",description:"ゆっくり"},
  {key:1500,label:"1500ms",description:"かなりゆっくり"}
];
function loadUiPreferences(){
  const fallback={fontSize:"max",longPressDelay:900};
  try{const saved=JSON.parse(localStorage.getItem(UI_PREFS_STORAGE_KEY)||"null");return{...fallback,...(saved&&typeof saved==="object"?saved:{})}}catch{return fallback}
}
let uiPreferences=loadUiPreferences();
function saveUiPreferences(){try{localStorage.setItem(UI_PREFS_STORAGE_KEY,JSON.stringify(uiPreferences))}catch{}}
function applyUiPreferences(){
  const validSize=UI_FONT_SIZE_OPTIONS.some(item=>item.key===uiPreferences.fontSize)?uiPreferences.fontSize:"max";
  const validDelay=LONG_PRESS_DELAY_OPTIONS.some(item=>item.key===Number(uiPreferences.longPressDelay))?Number(uiPreferences.longPressDelay):900;
  uiPreferences.fontSize=validSize;uiPreferences.longPressDelay=validDelay;
  document.documentElement.dataset.fontSize=validSize;
}
function setUiPreference(key,value){uiPreferences[key]=key==="longPressDelay"?Number(value):value;applyUiPreferences();saveUiPreferences();renderUiPreferences();updateSelectionAccordionSummaries()}
function renderUiPreferenceGroup(id,items,key){
  const el=document.getElementById(id);if(!el)return;el.innerHTML="";
  items.forEach(item=>{const btn=document.createElement("button");btn.type="button";btn.className="ui-pref-chip"+(String(uiPreferences[key])===String(item.key)?" active":"");btn.textContent=`${item.label}｜${item.description}`;btn.onclick=()=>setUiPreference(key,item.key);el.appendChild(btn)});
}
function renderUiPreferences(){
  renderUiPreferenceGroup("fontSizePreferenceChips",UI_FONT_SIZE_OPTIONS,"fontSize");
  renderUiPreferenceGroup("longPressPreferenceChips",LONG_PRESS_DELAY_OPTIONS,"longPressDelay");
  const font=UI_FONT_SIZE_OPTIONS.find(item=>item.key===uiPreferences.fontSize);const delay=LONG_PRESS_DELAY_OPTIONS.find(item=>item.key===Number(uiPreferences.longPressDelay));
  const fs=document.getElementById("fontSizePreferenceStatus");if(fs)fs.textContent=`現在：${font?.label||"最大"}（${font?.description||"旧版の約2倍"}）`;
  const ls=document.getElementById("longPressPreferenceStatus");if(ls)ls.textContent=`現在：${delay?.label||"900ms"}（${delay?.description||"標準"}）`;
}
applyUiPreferences();
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
opt("🌿 木漏れ日シャドウ","dappledshadow","(dappled sunlight and patterned shadows across the subject:1.86), (irregular leaf-shaped light and shadow patterns:1.82), (natural broken sunlight with crisp shadow edges:1.8)","葉の隙間から差す光のような、まだらな光と影の模様を作ります。屋外感や自然光感を強めたい時向き。"),
opt("🪟 柔らかい窓光","softWindowLight","(soft diffused window light illuminates the subject:1.82), (gentle directional daylight with smooth shadow transitions:1.8)","カーテンや曇り窓を通したような柔らかい窓光。室内の日常写真や穏やかな人物写真向き。"),
opt("▥ 硬い窓光","hardWindowLight","(hard directional window light with crisp shadow edges:1.86), (clear window-side highlights and deep structured shadows:1.84)","直射に近い硬い窓光。顔や身体へ明確な陰影を作ります。"),
opt("↔️ 横からの光","sideLight","(clear side lighting shapes the face and body from one lateral direction:1.84), (readable three-dimensional side-to-side light falloff:1.82)","左右どちらか一方向から当たる光。輪郭と立体感を出しやすい照明です。"),
opt("🌅 通常の逆光","backlight","(natural backlight from behind the subject:1.82), (soft edge illumination without turning the subject into a silhouette:1.8)","被写体の後ろから光が来る標準的な逆光。顔の情報も残します。"),
opt("☀️ 強い逆光","strongBacklight","(strong bright backlight directly behind or near the subject:1.9), (pronounced edge glow and bright backlit atmosphere:1.88)","太陽や強い照明を背後へ置く強い逆光。レンズフレアと相性があります。"),
opt("◼️ シルエット逆光","silhouetteBacklight","(silhouette-dominant backlighting:1.9), (subject front remains mostly dark while the outline is strongly illuminated:1.88)","輪郭を残し、正面を暗くするシルエット寄りの逆光。顔を見せたい場面には不向きです。"),
opt("📱 スマホ画面の光","screenLight","(soft localized smartphone-screen light illuminates the face:1.82), (cool close-range screen glow with believable falloff:1.8)","暗い場所でスマホ画面が顔を照らす光。自撮り時は撮影中の1台の画面光として扱います。"),
opt("🚦 街灯・店舗照明","streetShopLight","(mixed streetlight and storefront illumination:1.82), (believable urban night light spill on the subject and environment:1.8)","街灯や店舗から漏れる夜の環境光。夜の街や移動中の場面向き。"),
opt("🌤️ 自然なレンズフレア","naturalFlare","(subtle realistic lens flare caused by a strong light source near the frame:1.82), (small translucent optical flare artifacts:1.78), (flare does not obscure the face:1.82)","強い光源の近くに小さな光点や薄い筋を出す、控えめで実写的なレンズフレア。"),
opt("⭕ リング状レンズフレア","ringFlare","(large circular ring-shaped lens flare caused by strong backlight:1.92), (warm translucent optical flare arc crossing the frame:1.88), (a few realistic internal lens-reflection ghosts near the light source:1.82), (the flare remains semi-transparent and does not obscure the face:1.86)","強い逆光で画面に大きな半透明の光輪を出します。今回見せてもらったようなリング型です。"),
opt("🎬 映画的な強いレンズフレア","cinematicFlare","(prominent cinematic lens flare from a strong in-frame or edge light source:1.92), (multiple controlled optical ghosts and flare streaks:1.88), (dramatic but physically coherent flare:1.86)","光輪・ゴースト・筋を組み合わせた強い映画的フレア。主張が大きいので他の光学効果は控えめ推奨。"),
opt("➖ 横方向の光筋","anamorphicStreak","(horizontal anamorphic-style light streaks from bright point lights:1.86), (controlled cinematic horizontal flare lines:1.84)","明るい光源から横へ伸びる映画的な光筋。夜景やネオン向き。"),
opt("🔸 フレアゴースト","flareGhost","(small polygonal or circular lens-reflection ghosts aligned with the main light source:1.82), (realistic internal optical reflections:1.8)","光源と対角線上に並ぶ小さな光点・多角形のゴースト。リングより控えめです。"),
opt("🔴 ハレーション","halation","(warm red-orange halation blooms around very bright highlights:1.84), (film-like glowing highlight edges:1.82)","強い光の周囲へ赤〜オレンジのにじみを出すフィルム的表現。"),
opt("🌟 ブルーム","bloom","(soft luminous bloom around bright lights and highlights:1.82), (gentle highlight glow without losing facial detail:1.8)","明るい光の周囲だけを柔らかく発光させます。ハレーションより色味が中立です。"),
opt("🌈 色収差","chromaticAberration","(subtle red-cyan chromatic aberration near high-contrast edges:1.7), (controlled optical color fringing:1.68)","輪郭の端に赤・青系のわずかな色ズレを出します。強すぎると顔が崩れて見えます。"),
opt("🌑 ブラックミスト風","blackMist","(black-mist filter look with softened highlight contrast:1.8), (gentle cinematic glow while retaining readable detail:1.78)","ハイライトをにじませ、コントラストを少し柔らげる映画的フィルター感。"),
opt("💦 レンズ表面の水滴","lensDrops","(a few water droplets cling to the camera lens surface:1.82), (localized optical distortion and blur around lens droplets:1.78)","レンズ表面に水滴が付いた写り。雨天向きで、顔を覆いすぎない程度にします。"),
opt("🌫️ レンズの曇り","lensFog","(partial condensation fog on the lens surface:1.8), (soft localized veiling haze with a few clearer areas:1.76)","レンズが部分的に曇った表現。湿気・温度差・浴室周辺などに向きます。"),
opt("🏞️ 深い被写界深度","deepDof","(deep depth of field keeps subject and environment clearly readable:1.84), (foreground, subject, and background remain comparatively sharp:1.82)","手前から奥まで広くピントを合わせ、場所やテーブル上も読みやすくします。"),
opt("👁️ 目にピント","eyeFocus","(precise focus is locked on the nearest visible eye:1.86), (eyelashes and iris are the sharpest details while other planes fall off naturally:1.82)","人物写真で目を最もシャープに見せます。横顔では見えている側の目へ合わせます。"),
opt("📷 少しピントを外す","accidentalFocus","(slightly imperfect focus as in a spontaneous snapshot:1.72), (subject remains recognizable despite mild focus miss:1.7)","偶然撮れた写真のように少しだけピントを外します。顔の判別は残します。"),
opt("🤳 弱い手持ちブレ","weakHandheld","(subtle handheld camera shake:1.68), (minor natural micro-blur without losing facial readability:1.68)","手持ち撮影らしいごく弱いブレ。日常スナップ向き。"),
opt("〰️ 強い手持ちブレ","strongHandheld","(clearly visible handheld camera shake:1.82), (directional blur affects the frame while the subject remains partly readable:1.78)","強めの手持ちブレ。ライブ感は出ますが、顔や服の細部は弱くなります。"),
opt("📱 ローリングシャッター歪み","rollingShutter","(subtle rolling-shutter skew during movement:1.72), (vertical lines bend slightly from smartphone sensor readout:1.68)","スマホで動きながら撮った時の、縦線が少し傾くセンサー歪み。"),
opt("📱 古いスマホ写真","oldSmartphone","(older smartphone camera rendering:1.78), (limited dynamic range, mild digital noise, modest resolution, and casual processing:1.74)","少し粗く、暗部ノイズと弱い解像感がある古いスマホの写り。"),
opt("🌃 高感度ノイズ","highIsoNoise","(visible high-ISO digital noise in darker areas:1.76), (fine chroma and luminance noise without destroying the face:1.72)","暗所撮影のざらつき。夜や低照度向きです。"),
opt("🧱 JPEG圧縮感","jpegCompression","(mild JPEG compression artifacts in fine detail and color transitions:1.68), (casual shared-image texture:1.66)","SNSで保存・再送されたような軽い圧縮感。強くしすぎない設定です。"),
opt("🟠 暖色フィルター","warmfilter","(warm amber color filter:1.76), (gentle warm color grading across highlights and midtones:1.72)","画像全体を暖色へ寄せます。フィルムトーンと重ねる場合は色が強くなりすぎないよう注意。"),
opt("◻️ 低彩度仕上げ","desaturated","(moderately desaturated color treatment:1.76), (muted but still readable natural colors:1.72)","色を少し抑えた落ち着いた仕上げ。完全なモノクロではありません。"),
opt("⚫ モノクロ処理","monochromeEffect","(complete black-and-white conversion:1.86), (luminance and tonal contrast replace all color information:1.82)","色を完全に除いた白黒処理。カラーフィルムトーンとは併用しない方が安定します。"),
opt("✨ 柔らかいグロー","softGlow","(gentle overall glow on bright areas:1.78), (soft luminous finish while preserving realistic skin detail:1.74)","明るい部分を柔らかく発光させる最終仕上げ。ブルームより画像全体に軽く効きます。"),
opt("⬛ マットな黒","matteBlack","(matte lifted-black finish:1.76), (softened deep blacks with restrained contrast:1.72)","黒を少し浮かせたマットな仕上げ。柔らかいフィルム感を出します。"),
opt("🧹 スキャンダスト","scanDust","(sparse film-scan dust specks and tiny analog imperfections:1.68), (subtle scanned-negative texture:1.66)","フィルムスキャン時の小さなホコリや微細な汚れを少量加えます。")
];
const EFFECT_GROUPS=[
  {key:"lighting",label:"💡 光・照明",note:"被写体や空間へ実際に当たる光。逆光と逆光リムライトはこの分類です。",promptTitle:"scene lighting",items:["softWindowLight","hardWindowLight","sideLight","backlight","strongBacklight","rim","silhouetteBacklight","hardsun","flash","splitlight","chiaroscuro","lightshadow","hardshadow","dappledshadow","screenLight","streetShopLight","neon"]},
  {key:"lens",label:"🔭 レンズ・光学現象",note:"レンズ内部やレンズ表面で生じる光輪、ゴースト、光筋、にじみ、反射。",promptTitle:"lens and optical effects",items:["naturalFlare","ringFlare","cinematicFlare","warmflare","anamorphicStreak","flareGhost","halation","bloom","lightleak","glass","droplet","chromaticAberration","vignette","blackMist","lensDrops","lensFog"]},
  {key:"focus",label:"🎯 ピント・奥行き",note:"被写界深度、背景・前景ボケ、ピント位置、軽いピント外れ。",promptTitle:"focus and optical depth",items:["bokeh","orb","foreground","strongForeground","handblur","softfocus","deepDof","eyeFocus","accidentalFocus"]},
  {key:"atmosphere",label:"🌫️ 空気・大気表現",note:"空気の揺らぎ、乾燥感、きらめき。物理的な霧・煙・花びら等は追加要素側で選びます。",promptTitle:"atmosphere",items:["heathaze","drydust","sparkle"]},
  {key:"motion",label:"🏃 動き・撮影ブレ",note:"被写体や手持ちカメラの動き、センサー由来の歪み。",promptTitle:"motion and capture instability",items:["motionblur","weakHandheld","strongHandheld","rollingShutter"]},
  {key:"camera",label:"📷 カメラ・端末特性",note:"スマホ、コンデジ、VHS、暗所ノイズ、圧縮など撮影機材由来の写り。",promptTitle:"camera and device rendering",items:["hdr","digicam","oldSmartphone","vhs","highIsoNoise","jpegCompression"]},
  {key:"color",label:"🎨 色処理",note:"画像全体の色方向。フィルムトーン・作品トーンと重なる場合は相性ガードを確認してください。",promptTitle:"color treatment",items:["coolfilter","warmfilter","desaturated","monochromeEffect"]},
  {key:"finish",label:"🎞️ 質感・最終仕上げ",note:"粒子、露出、グロー、マット感、スキャン由来の質感。",promptTitle:"final texture and finish",items:["grain","blownhighlight","softGlow","matteBlack","scanDust"]}
];
const EFFECT_DISPLAY_ORDER=EFFECT_GROUPS.flatMap(group=>group.items);
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
  ilfordhp5:["warmflare","coolfilter","warmfilter","neon","lightleak"],
  polaroid:["vhs","hdr","hardshadow","chiaroscuro","splitlight","deepDof"],
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
  blownhighlight:["hdr"],
  naturalFlare:["ringFlare","cinematicFlare","warmflare"],
  ringFlare:["naturalFlare","cinematicFlare","warmflare"],
  cinematicFlare:["naturalFlare","ringFlare","warmflare"],
  warmflare:["coolfilter","naturalFlare","ringFlare","cinematicFlare"],
  softWindowLight:["hardWindowLight","hardsun","flash","silhouetteBacklight"],
  hardWindowLight:["softWindowLight","flash"],
  backlight:["silhouetteBacklight"],
  strongBacklight:["silhouetteBacklight"],
  silhouetteBacklight:["softWindowLight","backlight","strongBacklight","screenLight"],
  deepDof:["bokeh","orb","foreground","strongForeground","handblur","softfocus"],
  bokeh:["orb","deepDof"],
  orb:["bokeh","deepDof"],
  foreground:["strongForeground","handblur","deepDof"],
  strongForeground:["handblur","deepDof"],
  handblur:["deepDof"],
  weakHandheld:["strongHandheld"],
  strongHandheld:["weakHandheld","eyeFocus"],
  hdr:["blownhighlight","vhs","digicam","oldSmartphone"],
  oldSmartphone:["hdr","digicam","vhs"],
  coolfilter:["warmflare","warmfilter","monochromeEffect"],
  warmfilter:["coolfilter","monochromeEffect"],
  desaturated:["monochromeEffect"],
  monochromeEffect:["coolfilter","warmfilter","desaturated"]
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
const LEGACY_REMOVED_ANGLE_FALLBACKS={
  tableLeanForwardBothElbows:"tableLeanForwardOneElbow",
  counterLeanForwardBothElbows:"counterLeanForwardOneElbow"
};
const SCENE_CUE_WORDS={
  table:["テーブル","食卓","机","卓上","table","desk"],
  counter:["カウンター","バーカウンター","counter","bar counter"],
  oneElbow:["片肘","片ひじ","片前腕","一方の肘","one elbow","one forearm"],
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
function effectiveSelfieForCurrentScene(){return"on"}
function getSceneLinkedDisabledReason(key,itemKey){
  if(key==="angleMode"){
    if(itemKey==="groundLegToFaceSelfie"){
      if(!sceneHasCue("lowPose")||!sceneHasCue("legForward"))return"シーン欄に『しゃがむ／床に座る等の低い姿勢』と『片脚・足をカメラ手前へ出す』の両方が必要です。";
      if(state.visibleRange!=="fullBody")return"前景の脚から顔まで写すため、写す範囲を『全身』にしてください。";
    }
    if(itemKey==="tableLeanForwardOneElbow"&&(!sceneHasCue("table")||!sceneHasCue("oneElbow")||!sceneHasCue("leanForward")))return"シーン欄に『テーブル』『片肘／片前腕』『少し前傾』の3要素が必要です。";
    if(itemKey==="counterLeanForwardOneElbow"&&(!sceneHasCue("counter")||!sceneHasCue("oneElbow")||!sceneHasCue("leanForward")))return"シーン欄に『カウンター』『片肘／片前腕』『少し前傾』の3要素が必要です。";
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
  if(key==="gaze"&&isSleepExpression()&&itemKey!=="closed")return"睡眠系の表情では目を自然に閉じ、視線とカメラ認識をなくすため『目を閉じる / 視線なし』へ固定されます。";
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
const CAMERA_SUPPORT_OPTIONS=[{"label":"🤳 通常手持ち","key":"handheldExtended","value":"handheldExtended","help":"セルフ撮影方式。the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image。"},{"label":"📉 身体沿い手持ち","key":"handheldClose","value":"handheldClose","help":"セルフ撮影方式。the subject holds the single active smartphone with the lowered shooting hand immediately beside the body; the front camera is the viewpoint and the phone remains outside its own image。"},{"label":"🦵 膝・太もも上に設置","key":"lapSupported","value":"lapSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on the seated thighs or knees with its front camera aimed upward; the phone is the viewpoint and remains outside its own image。"},{"label":"🪑 テーブル下の膝上に設置","key":"lapUnderTable","value":"lapUnderTable","help":"セルフ撮影方式。the subject has placed the single active smartphone on the seated thighs or knees below the table edge, with its front camera aimed upward through the open space between body and table; the phone is the viewpoint and remains outside its own image。"},{"label":"☕ テーブル上に設置","key":"tableSupported","value":"tableSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on the table surface with its front camera aimed at the subject; the phone is the viewpoint and remains outside its own image。"},{"label":"🍸 カウンター上に設置","key":"counterSupported","value":"counterSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on the counter surface with its front camera aimed at the subject; the phone is the viewpoint and remains outside its own image。"},{"label":"🪑 椅子・ベンチ座面に設置","key":"seatSupported","value":"seatSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on a chair or bench seat with its front camera aimed toward the subject; the phone is the viewpoint and remains outside its own image。"},{"label":"🧱 低い台・段差に設置","key":"lowSurfaceSupported","value":"lowSurfaceSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on a low shelf, step, ledge, or similar stable surface with its front camera aimed toward the subject; the phone is the viewpoint and remains outside its own image。"},{"label":"⬛ 床・地面に設置","key":"floorSupported","value":"floorSupported","help":"セルフ撮影方式。the subject has placed the single active smartphone securely on the floor or ground with its front camera aimed upward toward the subject; the phone is the viewpoint and remains outside its own image。"}];
const CAMERA_POSTURE_OPTIONS=[{"label":"立位","key":"standing","value":"standing","help":"the subject remains standing with believable balance and foot support。"},{"label":"歩行中","key":"walking","value":"walking","help":"the subject is captured during a genuine walking step with coherent weight transfer and momentum。"},{"label":"椅子に座る","key":"seatedChair","value":"seatedChair","help":"the subject remains seated on a chair, bench, or stool with pelvis and legs physically supported。"},{"label":"床座り","key":"seatedFloor","value":"seatedFloor","help":"the subject remains seated on the floor or ground with coherent contact and leg placement。"},{"label":"寄りかかる","key":"leaning","value":"leaning","help":"the subject leans against the support explicitly described in the written scene while keeping believable contact and balance。"},{"label":"横になる・もたれる","key":"reclining","value":"reclining","help":"the subject remains reclining or deeply supported exactly as described in the written scene, with gravity and contact surfaces kept coherent。"}];
const CAMERA_HEIGHT_OPTIONS=[{"label":"頭頂の真上","key":"topDirect","value":"topDirect","help":"the lens is centered directly above the crown with a true vertical downward optical axis。"},{"label":"頭上前方","key":"aboveHead","value":"aboveHead","help":"the lens is above the head and slightly forward, looking diagonally downward。"},{"label":"目線よりかなり上","key":"high","value":"high","help":"the lens is clearly above eye level with a readable downward optical axis。"},{"label":"目線","key":"eye","value":"eye","help":"the lens is at eye height with a nearly level optical axis。"},{"label":"顔・顎","key":"chin","value":"chin","help":"the lens is around chin or lower-face height with a very mild upward optical axis。"},{"label":"肩","key":"shoulder","value":"shoulder","help":"the lens is around shoulder height and looks gently upward toward the face。"},{"label":"胸","key":"chest","value":"chest","help":"the lens is around chest height and looks upward through the upper torso toward the face。"},{"label":"みぞおち・下胸","key":"solar","value":"solar","help":"the lens is around the lower chest or solar-plexus line and looks distinctly upward toward the face。"},{"label":"ウエスト・腰","key":"waist","value":"waist","help":"the lens is around waist height and follows a strong upward path through the torso toward the face。"},{"label":"上部ヒップ","key":"upperHip","value":"upperHip","help":"the lens is around upper-hip height and follows a strong near-to-far upward path toward the face。"},{"label":"太もも上部","key":"upperThigh","value":"upperThigh","help":"the lens is around upper-thigh height and creates a very strong upward body-path perspective。"},{"label":"太もも中央","key":"midThigh","value":"midThigh","help":"the lens is around mid-thigh height and creates an extreme upward body-path perspective。"},{"label":"膝","key":"knee","value":"knee","help":"the lens is around knee height with an extreme upward optical path toward the face。"},{"label":"座位の膝・太もも","key":"lap","value":"lap","help":"the lens originates from the seated lap or knee line and looks steeply upward toward the torso and face。"},{"label":"テーブル面","key":"table","value":"table","help":"the lens is fixed at the table-surface height and looks toward the seated or leaning subject from that exact support plane。"},{"label":"カウンター面","key":"counter","value":"counter","help":"the lens is fixed at the counter-surface height and looks toward the subject from that exact support plane。"},{"label":"椅子・ベンチ座面","key":"seatSurface","value":"seatSurface","help":"the lens is fixed at chair-seat or bench-seat height and looks upward from that stable support plane。"},{"label":"低い台・段差","key":"lowSurface","value":"lowSurface","help":"the lens is fixed on a low shelf, ledge, step, or platform below the subject and looks upward。"},{"label":"床・地面","key":"ground","value":"ground","help":"the lens is fixed immediately above floor or ground level and looks strongly upward。"}];
const CAMERA_DIRECTION_OPTIONS=[{"label":"正面","key":"front","value":"front","help":"the camera is centered on the subject front plane; the torso front remains the primary projection。"},{"label":"左前45°","key":"frontLeft45","value":"frontLeft45","help":"the camera is on the subject left-front side at approximately forty-five degrees, preserving both front volume and the left side contour。"},{"label":"右前45°","key":"frontRight45","value":"frontRight45","help":"the camera is on the subject right-front side at approximately forty-five degrees, preserving both front volume and the right side contour。"},{"label":"左真横","key":"leftSide","value":"leftSide","help":"the camera is on the subject true left side; the body reads as a clear lateral projection without drifting toward the front。"},{"label":"右真横","key":"rightSide","value":"rightSide","help":"the camera is on the subject true right side; the body reads as a clear lateral projection without drifting toward the front。"},{"label":"左後方45°","key":"backLeft45","value":"backLeft45","help":"the camera is on the subject left-rear side at approximately forty-five degrees; the back and left side remain the primary body planes。"},{"label":"右後方45°","key":"backRight45","value":"backRight45","help":"the camera is on the subject right-rear side at approximately forty-five degrees; the back and right side remain the primary body planes。"},{"label":"背面","key":"back","value":"back","help":"the camera is centered behind the subject; the back plane remains primary and is not converted into a frontal portrait。"},{"label":"左肩越し振り返り","key":"lookBackLeft","value":"lookBackLeft","help":"the camera is behind the subject near the left shoulder line; the body remains oriented away while the head turns back over the left shoulder toward the lens。"},{"label":"右肩越し振り返り","key":"lookBackRight","value":"lookBackRight","help":"the camera is behind the subject near the right shoulder line; the body remains oriented away while the head turns back over the right shoulder toward the lens。"}];
const VISIBLE_RANGE_OPTIONS=[{"label":"顔どアップ","key":"extremeFace","value":"extremeFace","help":"the face fills almost the entire frame from hairline to chin; body, hands, outfit, and environment remain only incidental。"},{"label":"顔アップ","key":"faceCloseup","value":"faceCloseup","help":"the frame contains the face, hairline, neck, and only a slight shoulder trace。"},{"label":"横顔アップ","key":"profileCloseup","value":"profileCloseup","help":"the frame contains a close lateral face line with eye, nose bridge, lips, cheek, jaw, and minimal neck or shoulder。"},{"label":"顔〜肩","key":"headShoulder","value":"headShoulder","help":"the frame contains the full head, neck, and both shoulder lines without widening into a torso portrait。"},{"label":"胸上","key":"chestUp","value":"chestUp","help":"the frame runs from the full head through the upper chest, keeping face and upper garment readable。"},{"label":"上半身","key":"upperBody","value":"upperBody","help":"the frame runs from the full head through the lower chest or upper waist, keeping face and upper-body action readable。"},{"label":"腰上","key":"waistUp","value":"waistUp","help":"the frame runs from the full head through the waist or immediate upper-hip boundary。"},{"label":"上部ヒップまで","key":"upperHip","value":"upperHip","help":"the frame runs from the full head through the complete waist and upper hips。"},{"label":"太もも上まで","key":"thighUp","value":"thighUp","help":"the frame runs from the full head through the upper thighs。"},{"label":"膝上","key":"kneeUp","value":"kneeUp","help":"the frame runs from the full head to immediately above or around the knees。"},{"label":"全身","key":"fullBody","value":"fullBody","help":"the entire body from head to feet remains inside the frame with no limb cropped。"},{"label":"全身＋周辺環境","key":"fullBodyEnvironment","value":"fullBodyEnvironment","help":"the entire body remains inside the frame with clear surrounding environmental context and stable ground contact。"}];
const CAMERA_357_PRESETS=[{"label":"🤳 通常手持ち｜立位｜頭頂の真上｜正面｜顔〜肩","key":"c357_handheldExtended_standing_topDirect_front_headShoulder","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is centered directly above the crown with a true vertical downward optical axis:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame contains the full head, neck, and both shoulder lines without widening into a torso portrait:2.0),\n(the exact lower image boundary intersects across the shoulder line before the chest becomes a torso portrait:2.0),\n(the lower chest, waist, hips, arms below the selected boundary, and legs remain outside the captured frame:2.0),\n(do not widen the crop to complete an action, prop, or location; any continuation remains outside the image:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭頂の真上\n方向：正面\n写す範囲：顔〜肩\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"topDirect","heightLabel":"頭頂の真上","direction":"front","directionLabel":"正面","visibleRange":"headShoulder","visibleRangeLabel":"顔〜肩","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"headShoulder","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭頂の真上｜正面｜上半身","key":"c357_handheldExtended_standing_topDirect_front_upperBody","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is centered directly above the crown with a true vertical downward optical axis:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the lower chest or upper waist, keeping face and upper-body action readable:2.0),\n(the exact lower image boundary intersects at the lower chest-to-upper-waist limit defined by this preset:2.0),\n(the hips, thighs, knees, lower legs, feet, and any body continuation below that boundary remain outside the captured frame:2.0),\n(do not widen the image to include the complete pose, gesture, footwear, prop destination, or additional surroundings:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭頂の真上\n方向：正面\n写す範囲：上半身\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"topDirect","heightLabel":"頭頂の真上","direction":"front","directionLabel":"正面","visibleRange":"upperBody","visibleRangeLabel":"上半身","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"upperBody","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭頂の真上｜正面｜腰上","key":"c357_handheldExtended_standing_topDirect_front_waistUp","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is centered directly above the crown with a true vertical downward optical axis:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the waist or immediate upper-hip boundary:2.0),\n(the exact bottom image edge intersects the body at the waist-to-immediate-upper-hip boundary:2.0),\n(the lower hips, thighs, knees, lower legs, feet, and footwear must remain outside the captured frame:2.0),\n(do not widen the image to include the subject full pose, complete pointing arm, legs, footwear, sign, destination, or additional surroundings:2.0),\n(if a gesture, prop relationship, or location detail extends beyond this boundary, let it continue outside the image rather than changing the crop:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭頂の真上\n方向：正面\n写す範囲：腰上\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"topDirect","heightLabel":"頭頂の真上","direction":"front","directionLabel":"正面","visibleRange":"waistUp","visibleRangeLabel":"腰上","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"waistUp","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜顔アップ","key":"c357_handheldExtended_standing_aboveHead_front_faceCloseup","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame contains the face, hairline, neck, and only a slight shoulder trace:2.0),\n(the exact lower image boundary intersects at the base of the neck with only a slight shoulder trace:2.0),\n(the chest, torso, hands, outfit coordination, and broad background remain outside the captured frame:2.0),\n(do not widen the crop to complete an action, prop, or location; any continuation remains outside the image:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：顔アップ\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"faceCloseup","visibleRangeLabel":"顔アップ","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"face","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜顔〜肩","key":"c357_handheldExtended_standing_aboveHead_front_headShoulder","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame contains the full head, neck, and both shoulder lines without widening into a torso portrait:2.0),\n(the exact lower image boundary intersects across the shoulder line before the chest becomes a torso portrait:2.0),\n(the lower chest, waist, hips, arms below the selected boundary, and legs remain outside the captured frame:2.0),\n(do not widen the crop to complete an action, prop, or location; any continuation remains outside the image:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：顔〜肩\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"headShoulder","visibleRangeLabel":"顔〜肩","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"headShoulder","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜胸上","key":"c357_handheldExtended_standing_aboveHead_front_chestUp","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the upper chest, keeping face and upper garment readable:2.0),\n(the exact lower image boundary intersects through the upper chest at the selected chest-up limit:2.0),\n(the lower chest, waist, hips, thighs, knees, lower legs, and feet remain outside the captured frame:2.0),\n(do not widen the image to include the complete pose, gesture, prop, or surrounding environment:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：胸上\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"chestUp","visibleRangeLabel":"胸上","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"upperBody","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜上半身","key":"c357_handheldExtended_standing_aboveHead_front_upperBody","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the lower chest or upper waist, keeping face and upper-body action readable:2.0),\n(the exact lower image boundary intersects at the lower chest-to-upper-waist limit defined by this preset:2.0),\n(the hips, thighs, knees, lower legs, feet, and any body continuation below that boundary remain outside the captured frame:2.0),\n(do not widen the image to include the complete pose, gesture, footwear, prop destination, or additional surroundings:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：上半身\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"upperBody","visibleRangeLabel":"上半身","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"upperBody","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜腰上","key":"c357_handheldExtended_standing_aboveHead_front_waistUp","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the waist or immediate upper-hip boundary:2.0),\n(the exact bottom image edge intersects the body at the waist-to-immediate-upper-hip boundary:2.0),\n(the lower hips, thighs, knees, lower legs, feet, and footwear must remain outside the captured frame:2.0),\n(do not widen the image to include the subject full pose, complete pointing arm, legs, footwear, sign, destination, or additional surroundings:2.0),\n(if a gesture, prop relationship, or location detail extends beyond this boundary, let it continue outside the image rather than changing the crop:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：腰上\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"waistUp","visibleRangeLabel":"腰上","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"waistUp","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜正面｜上部ヒップまで","key":"c357_handheldExtended_standing_aboveHead_front_upperHip","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is centered on the subject front plane; the torso front remains the primary projection:2.0),\n(the frame runs from the full head through the complete waist and upper hips:2.0),\n(the exact bottom image edge intersects through the complete waist and upper hips at the selected upper-hip boundary:2.0),\n(the lower hips, thighs, knees, lower legs, feet, and footwear remain outside the captured frame:2.0),\n(do not widen the image to complete the pose, gesture, prop relationship, or environmental context:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：正面\n写す範囲：上部ヒップまで\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"front","directionLabel":"正面","visibleRange":"upperHip","visibleRangeLabel":"上部ヒップまで","projectionFamily":"overhead","authorityFamily":"front","regionFamily":"waistUp","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜左前45°｜顔アップ","key":"c357_handheldExtended_standing_aboveHead_frontLeft45_faceCloseup","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without becoming the dominant foreground object; the free hand follows the written scene:2.0),\n(the subject remains standing with believable balance and foot support:1.96),\n(the lens is above the head and slightly forward, looking diagonally downward:2.0),\n(the camera is on the subject left-front side at approximately forty-five degrees, preserving both front volume and the left side contour:2.0),\n(the frame contains the face, hairline, neck, and only a slight shoulder trace:2.0),\n(the exact lower image boundary intersects at the base of the neck with only a slight shoulder trace:2.0),\n(the chest, torso, hands, outfit coordination, and broad background remain outside the captured frame:2.0),\n(do not widen the crop to complete an action, prop, or location; any continuation remains outside the image:2.0),\n(the upper surfaces nearest the elevated lens remain closer while lower body regions recede coherently; the viewpoint must not collapse to eye level:1.98),\n(the body-to-camera direction is fixed by this preset and must not drift to another side:2.0),\n(the selected support method, posture, lens height, subject-relative direction, optical axis, distance, perspective, and exact visible range form one indivisible completed 357-series geometry:2.0),\n(do not reinterpret this preset as an ordinary eye-level selfie, generic portrait, different camera side, different lens height, or wider or tighter crop:2.0)","help":"支持：通常手持ち\n姿勢：立位\n高さ：頭上前方\n方向：左前45°\n写す範囲：顔アップ\n\nこの5条件を一体化した完成357系プロンプトを1本だけ出力します。","meta":{"support":"handheldExtended","supportLabel":"通常手持ち","posture":"standing","postureLabel":"立位","height":"aboveHead","heightLabel":"頭上前方","direction":"frontLeft45","directionLabel":"左前45°","visibleRange":"faceCloseup","visibleRangeLabel":"顔アップ","projectionFamily":"overhead","authorityFamily":"threeQuarter","regionFamily":"face","supported":false,"bodyAdjacent":false}},{"label":"🤳 通常手持ち｜立位｜頭上前方｜左前45°｜顔〜肩","key":"c357_handheldExtended_standing_aboveHead_frontLeft45_headShoulder","value":"(self-capture is made by the subject using exactly one active smartphone front camera:2.0),\n(the subject holds the single active smartphone in the shooting hand at a natural reachable self-capture distance; the front camera is the viewpoint and the phone remains outside its own image:2.0),\n(the shooting arm follows the selected lens position without
ファイル サイズが大きいため、プレビューは一部のみ表示されています
