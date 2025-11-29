# line-stamp

- ベースイメージを作成
- キャラクターシートを作成： https://felo.ai/ja/livedoc/

```yaml
title: "キャラクター設定シート生成プロンプト"

prompt: |
  以下の内容を1枚または複数の画像として、整ったレイアウトで作成してください。
  すべての項目は読みやすいようにセクションごとに区切り、
  タイトル文字は上部に整列、説明文字は各シートの近くに小さめに配置してください。
  背景は淡い無地（白系・クリーム系・薄グレー）で統一し、見やすいデザインにすること。

  ---【生成するシート】---

  ■ 1. キャラクターデザイン（Character Design）
    - キャラクターの全身イラスト
    - 立ちポーズの基本デザイン
    - 色味・雰囲気が分かるように丁寧に描く
    - 背景はシンプルにし、キャラが目立つレイアウト

  ■ 2. プロポーションデザイン（Proportion Sheet）
    - 身長差比較用の立ち姿（同一キャラのサイズ比較）
    - 頭身（例：2頭身／3頭身など）
    - 正確な比率が分かるよう、横に並べて配置
    - シルエット図と詳細図を併記しても良い

  ■ 3. 三面図（Three Views）
    - 正面（Front View）
    - 側面（Side View）
    - 背面（Back / Rear View）
    - 3つは横並びで整った位置に配置し、同じポーズと高さで揃える
    - デフォルメキャラの場合も正確な形状が分かるよう簡潔に描写

  ■ 4. 表情シート（Expression Sheet）
    - よく使う4〜6種類の表情（例：無表情、笑顔、怒り、困り、驚き など）
    - 顔だけのアップを均等に配置（グリッド状）
    - 表情タイトルを各顔の下に小さく記載

  ■ 5. ポーズ集（Pose Design / Pose Sheet）
    - 日常でよく使うポーズを6〜12種類描く
      （例：歩く、座る、手を振る、喜ぶ、落ち込む、ジャンプなど）
    - 1枚のシートに等間隔で並べる
    - ポーズ名を下部に小さく表示しても良い

  ■ 6. 衣装デザイン（Costume Design Sheet）
    - 基本衣装＋バリエーション（2〜4種）
    - 正面図中心、必要に応じて側面・背面も
    - 小物（帽子、靴、アクセサリー等）のデザインも含める
    - 衣装ごとに独立したスペースを確保し、整然と配置する

  ---【レイアウト・スタイル指示】---

  ・見出し（シートタイトル）は太字で大きく、整列させて配置する。
  ・各シート内の要素は均等に整列（グリッド、横並び、縦並びなど）し、
    キャラクターの比率や高さが揃うように統一する。
  ・余白（マージン）を適度に取り、情報が詰まりすぎないようにする。
  ・線画・着色どちらでも良いが、デザイン内容が明確に伝わる描き方を優先する。
  ・キャラクターは元のデザインを忠実に反映しつつ、資料として見やすい構成にまとめる。

file_format:
  type: "png"
  dpi: 300
  color_profile: "sRGB"

pages:
  output_mode: "single_or_multiple"   # 1枚または複数シートでOK
  recommended_size: "A4または縦長の大きめキャンバス"

notes:
  - "全体は資料性を重視し、整った美しい配置を最優先してください。"
  - "キャラクターの設定資料集として利用できる品質を目指してください。"
  - "必要ならシートごとに薄い枠線や区切り線を使っても構いません。"

```

- テーマを作成
- テーマごとにスタンプ案を作成

```
下記の単語を12個ずつ以下のフォーマットで出力してください。

words:
  - "<WORD_01>"
  - "<WORD_02>"
  - "<WORD_03>"
  - "<WORD_04>"
  - "<WORD_05>"
  - "<WORD_06>"
  - "<WORD_07>"
  - "<WORD_08>"
  - "<WORD_09>"
  - "<WORD_10>"
  - "<WORD_11>"
  - "<WORD_12>"
```
  
- スタンプ用画像を作成: https://felo.ai/ja/livedoc/

```yaml
# LINEスタンプ作成プロンプト（画像生成・デザイナー指示用）
title: "とりあえずトリ - 12個一覧画像（3x4）"
character_image: "添付画像を使用（attached_character.png）"
target_user: "xxx"

layout:
  rows: 3
  cols: 4
  cell_count: 12
  canvas:
    # 最終の一覧画像サイズ（任意で変更可）
    width_px: 2400
    height_px: 1800
    gutter_px: 24             # セル間の余白
    cell_padding_px: 20       # 各セル内のパディング（キャラが端に付かないように）
  output:
    sheet_image: true         # 3行4列の一覧画像（合成）
    individual_images: true   # 各スタンプを個別PNGでも書き出す（背景は同じクロマキー）
    format: "png"
    dpi: 300

background:
  # スタンプ部分を除いた背景はクロマキー用の黄緑に固定
  chroma_key_color_hex: "#9ACD32"   # YellowGreen（クロマキーしやすい黄緑）
  cell_background: "#9ACD32"        # 各セルの背景色（キャラ領域を含めたセル外背景）
  note: "スタンプのキャラクター・文字以外の領域はすべて上記カラーで統一。クロマキー処理で除去しやすいよう単色に。"

character:
  source: "attached_character.png"
  placement: "セル内にバランスよく配置（上下左右中央を基本）"
  scale: "セルサイズに対してキャラが60〜80%の高さを占めるよう調整"
  variations:
    - "立ちポーズ（腕組み／片手挙げ）"
    - "座りポーズ（足を投げ出す／脚を折る）"
    - "ジャンプ／躍動ポーズ"
    - "困り顔／照れ顔などの微変化（表情は控えめに）"
    - "小物を持つ（教科書、スマホ、タオルなど）"
  style_note: "元のキャラクターの特徴を崩さない範囲でポーズと角度を変える。表情は大きく崩さず『使いやすさ』を優先。"

text:
  # ユーザー指定の12ワードを下のwords欄に列挙してください
  style:
    use_speech_bubble: false
    font_family: "Rounded Sans / Noto Sans JP / ヒラギノ角ゴシックに近い丸ゴ"
    font_weight: "extra-bold"          # 太文字（視認性重視）
    fill_color: "#000000"              # 文字塗りは黒太文字
    outline:
      enabled: true
      color: "#FFFFFF"                 # 細い白線で囲む
      width_px: 2                      # 白線の太さ（細め）※最終メトリクスで調整可
    letter_spacing: 0
    line_height_ratio: 1.0
    max_lines: 2
    max_chars_per_line: 12
  placement_variation:
    - "上部中央（文字を頭上に配置）"
    - "下部中央（文字を足元に配置）"
    - "左寄せ縦並び（縦書き風で左側に寄せる）"
    - "右寄せ縦並び"
    - "斜め配置（テキストを少し傾ける）"
    - "キャラの横に縦長で配置（会話的ではなく図案として）"
  constraints:
    - "吹き出し不可：背景から切り離した黒太文字＋白縁のみで表現"
    - "文字は必ず読みやすく。背景（#9ACD32）と十分なコントラストを確保すること"
    - "文字がキャラの顔や重要ディテールを隠さない配置を優先"

composition_and_design:
  variety_requirements:
    - "12個の中で文字位置・文字サイズ・キャラポーズを必ず分散させ、単調にならないこと"
    - "縦長テキスト、横長テキストなどバリエーションを入れる"
    - "一部セルでキャラに小物（例：スマホ、ユニフォーム、応援グッズ）を持たせる"
    - "色替えは背景固定のため不可。キャラの小物やアクセントで多様性を出す"
  accessibility:
    - "文字サイズはスマホで視認しやすいこと（一覧表示でも判読可）"
    - "白縁2px＋黒太文字の組合せで、どの端末でも読みやすいこと"
  visual_balance:
    - "一覧画像は3x4のグリッドで左右上下の余白を均等に保つ"
    - "各セルは個別に見たときも単体スタンプとして成立するデザインであること"

export_and_files:
  sheet:
    filename: "toriazuto_tori_stickers_sheet_3x4.png"
    include_margin_px: 40    # シート周囲の余白（クロマキー処理しやすくするため）
  individuals:
    filename_pattern: "toriazuto_tori_stamp_{index:02d}.png"  # index 01〜12
  metadata:
    manifest_json: true
    manifest_filename: "manifest.json"
    manifest_contents:
      - "word": "<ワード>"
      - "file": "<対応ファイル名>"
      - "row": "<1-3>"
      - "col": "<1-4>"
  color_profile: "sRGB"

notes_for_generator_or_designer:
  - "添付キャラクター画像をそのまま、切り出してセル内に配置してください。"
  - "背景は必ず #9ACD32 の単色で統一。透過ではなく単色画像で納品（クロマキー処理前提）。"
  - "文字は吹き出しを使わず、黒太文字に白縁（アウトライン）でのみ表現すること。"
  - "12個で視覚的に飽きさせない構図を必ず作る（位置・ポーズ・文字配置を工夫）。"
  - "ターゲットユーザーは 'xxx'。用途に合わせて攻撃的な表現や過度に特殊なスラングは避ける。"
  - "最終チェックで、各セルの文字が欠けていないか、文字とキャラが干渉して読みにくくなっていないか確認する。"

words:
  # ここにユーザーが指定する12ワードを上から順に入れてください
  - "<WORD_01>"
  - "<WORD_02>"
  - "<WORD_03>"
  - "<WORD_04>"
  - "<WORD_05>"
  - "<WORD_06>"
  - "<WORD_07>"
  - "<WORD_08>"
  - "<WORD_09>"
  - "<WORD_10>"
  - "<WORD_11>"
  - "<WORD_12>"
```

省略版
```yaml
target_user: "xxx"

layout:
  rows: 3
  cols: 4

background:
  chroma_key_color_hex: "#9ACD32"

character:
  placement: "中央"
  scale: "高さ60〜80%"
  variations:
    - "立ち/腕組み/片手挙げ"
    - "座り"
    - "ジャンプ"
    - "軽い表情変化"
    - "小物所持"
  note: "特徴維持しつつポーズ変化"

text:
  style:
    font_family: "Noto Sans JP"
    font_weight: "extra-bold"
    fill_color: "#000000"
    outline: { enabled: true, color: "#FFFFFF", width_px: 2 }
  constraints:
    - "吹き出し禁止・黒文字＋白縁"
    - "背景と高コントラスト"
    - "キャラの重要部を塞がない"

design:
  variety:
    - "文字位置/サイズ/ポーズを分散"
    - "縦長/横長混在"
    - "小物で変化"
  accessibility:
    - "スマホで読みやすいサイズ"
  balance:
    - "3x4で均等"
    - "各セル単体で成立"

export:
  color_profile: "sRGB"

notes:
  - "背景は必ず#9ACD32単色"
  - "12セルすべて異なる構図"
  - "words の文言を1セルにつき1つ表示"
  - "文言の意味に合うポーズを選択"
  - "白縁文字が欠けないよう調整"

words:
  - "<WORD_01>"
  - "<WORD_02>"
  - "<WORD_03>"
  - "<WORD_04>"
  - "<WORD_05>"
  - "<WORD_06>"
  - "<WORD_07>"
  - "<WORD_08>"
  - "<WORD_09>"
  - "<WORD_10>"
  - "<WORD_11>"
  - "<WORD_12>"
```


- 背景を透過: https://www.iloveimg.com/ja/remove-background
- 画像を分割: https://splitimage.app/ja
- 申請
