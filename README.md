# line-stamp

- ベースイメージを作成
- キャラクターシートを作成
- テーマを作成
- テーマごとにスタンプ案を作成
- スタンプ用画像を作成

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
    - "縦長テキスト、横長テキスト、2段テキストなどバリエーションを入れる"
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

- 背景を透過
- 画像を分割
  - https://splitimage.app/ja
- 申請
