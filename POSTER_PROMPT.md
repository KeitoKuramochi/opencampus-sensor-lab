# オープンキャンパス用 A4ポスター(QRドーン)の生成プロンプト

ガチャ機の横に置いて、解説ページ(`opencampus/index.html`)へのQRを読ませるためのA4ポスター。
ガチャ機ディスプレイの画像(`firmware/gacha_lock_ble/PROMPTS.md`)と同じ世界観
(フラットベクター / ネオン発光 / 濃いチャコール背景 / リモコン型マスコット)で揃えてある。

## ⚠️ 最重要:QRコードは画像生成AIに描かせない

画像生成AIが描いたQRは**まず読み取れない**(モジュールの並びが出鱈目になる)。
なので生成するのは「**QRを貼るための白い正方形が空いているポスター**」で、
そこに自分で作った本物のQR画像を後から重ねる。

## 手順

1. 下のプロンプトで生成する(Nano Banana / Gemini / ChatGPT画像生成 など)
2. 中央の白い正方形に、自分で作ったQR画像を Canva / Keynote / PowerPoint / プレビュー.app などで重ねる
   - QRの周囲の白い余白(クワイエットゾーン)は**絶対に潰さない**。白枠より少し小さめに置く
3. A4(210×297mm)でプリント。**必ず現物をスマホで読み取りテストしてから貼る**

---

## プロンプト本体

```
A print-ready A4 portrait poster (aspect ratio 210:297, vertical) for a school open
campus exhibition booth. The poster will be printed and placed next to a real gachapon
capsule machine, so it must read clearly from about 2 meters away.

LAYOUT (top to bottom):
- Top area: large bold rounded Japanese headline text on two lines:
  "ゲームで勝つと、" / "このガチャが開く。"
  Below it, a smaller single line: "100円ショップの300円センサーから作りました"
- Left of the headline area: a cute mascot character shaped like a white TV remote
  control with 12 small colorful round buttons on its body (red, green, blue, orange,
  lime, purple, yellow, sky blue, pink), simple smiling dot eyes, tiny arms and legs.
  The mascot is cheering with one arm raised, pointing down toward the center of the
  poster. Soft cyan neon glow around it.
- CENTER (the main element, taking up roughly half the poster height): a large
  rounded-corner card of PURE WHITE (#FFFFFF), perfectly square, centered
  horizontally, with a generous white margin inside it. This square must be
  COMPLETELY EMPTY — absolutely nothing inside it. Do NOT draw a QR code. Do NOT draw
  any dots, squares, patterns, grids, logos, icons, or text inside this white square.
  It is intentionally left blank as a placeholder. Around the outside of the white
  card, a thin bright cyan neon outline and soft glow.
- Just below the white square: large bold rounded Japanese text
  "しくみの解説はこちら" and under it a smaller line "スマホのカメラをかざしてね"
  with a small smartphone icon.
- Bottom edge: a horizontal row of small colorful gachapon capsules in the project's
  colors, and a thin line of small text "赤外線センサー × ESP32 × リズムゲーム".

STYLE:
- Background: deep charcoal (#111318) filled edge to edge, full bleed, with a subtle
  dark gradient and faint circuit-board line texture in the darkest areas.
- Flat vector illustration style, thick bold shapes, high contrast, neon accent colors
  (cyan #6fb3e8, green #3f9e56, coral #c9497b, gold #b8901f).
- Very large, very bold, highly readable Japanese typography (rounded gothic).
- Keep a clean empty margin of about 10mm around the entire poster edge.
- No white border, no picture frame, no drop shadow around the poster itself.
- No English text anywhere except where specified. No fake or garbled characters.
```

## 文字が崩れたときのフォールバック

画像生成AIは日本語をよく崩す。崩れたら、プロンプトの末尾に

```
Do not render any text at all. Leave generous empty space where the text would go.
```

を足して**絵と白枠だけ**生成し、文字は Canva / Keynote 側で入れる(この方が確実で綺麗)。

## バリエーション

- **明るい配色にしたい場合**: 背景を `#111318` → `#f7f9fb`、文字を `#16202a`、
  ネオン発光を「ソフトな影」に置き換える。印刷のインクも節約できる
- **QR画像を直接AIに渡せる場合**(Nano Banana等の画像編集): 「この画像のQRコードは
  1ピクセルも変更せず、周囲にだけデザインを追加して」と指示する方法もあるが、
  リサンプルで読み取れなくなることがあるので、**生成後に必ず実機テストすること**
- **より確実な方法**: HTML+CSSで組んでブラウザからPDF出力すれば、QRもフォントも
  100%綺麗に出る。デザイン性より確実性を優先するならこちら
