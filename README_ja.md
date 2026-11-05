# ResNet50による犬・猫の2値分類とLIME・Grad-CAM比較

[English README](README.md)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakaNori999/resnet50_lime_grad-cam_dogcat/blob/main/ResNet50_DogCat_LIME_GradCAM.ipynb)

ImageNetで事前学習されたResNet50を犬・猫の2値分類向けにファインチューニングし、**同一の学習済みモデル・入力画像・説明対象クラス**についてLIMEとGrad-CAMの説明画像を比較するGoogle Colabノートブックです。

**公開対象はコードのみです。** 収集した学習画像、テスト画像、学習済みモデル、保存済みの実行出力は現行版に含みません。なお、過去のコミット履歴には以前の実行出力が残る可能性があるため、公開履歴の確認が必要です。利用者の画像で学習した結果は、元の研究の出力と一致するとは限りません。

## 実行方法

1. 上の **Open in Colab** をクリック。GoogleアカウントでColabを開き、必要に応じてGPUランタイムを選択します。
2. 自分で利用権限を確認した画像をGoogle Driveに用意します。デフォルトの想定は**犬100枚・猫100枚、計200枚**です。

   ```text
   MyDrive/
   └── dog_cat_100images/
       ├── cat/       ← 猫100枚
       └── dog/       ← 犬100枚
   ```

   画像はJPG/JPEG、PNG、BMP、WebPに対応します。ディレクトリ名を変更する場合は第2節の `DATA_DIR` を変更してください。枚数を変えて試す場合は `EXPECTED_PER_CLASS` を変更できますが、研究の実験条件も変わります。
3. ノートブック第2節の `DATA_DIR` と `OUTPUT_ROOT` を確認して、上から順に実行します。Google Driveへのアクセス許可は、**利用者本人のアカウント**に対して行われます。
4. 学習終了後、第10節の `TEST_IMAGE_PATH` に、学習・検証に使っていない画像のDrive上のパスを指定してください。公開版では空欄なので勝手に画像を読み込みません。任意の第11～13節は削除済みです。別の画像を比較する場合は、第10節のパスを変更してセルを再実行してください。
5. 入力画像・LIME（正の寄与を赤色で表示）・Grad-CAMが横並びに表示され、画像やモデル、設定値は**自分のDrive内の** `OUTPUT_ROOT` に保存されます。これらがGitHubに自動アップロードされることはありません。

## 主な実験条件（初期設定）

| 項目 | 設定 |
| --- | --- |
| ベースモデル | ResNet50（ImageNet事前学習済み、分類部は除く） |
| 追加した分類部 | Conv2D(1024, 3×3, ReLU) → GAP → Dropout → Dense(256, ReLU) → Dropout → Dense(1) + sigmoid |
| 学習 | Adam、Binary Crossentropy、batch size 32 |
| エポック | 分類部2＋最終ブロック3＝合計5 |
| 検証 | 各クラス80%を学習、20%を検証。別の画像で最終表示を確認 |
| LIME | SLIC約200領域、2,000摂動サンプル、上位12の正の寄与領域を無色～赤で表示 |
| Grad-CAM | dogの場合はlogit、catの場合は負のlogitに対する勾配を使用 |

LIMEは正と負の係数を計算したうえで、図には**正の係数のみを表示**しています。無色は「寄与がゼロ」を意味しません。Grad-CAMの青は「値が低い」であり、LIMEの「負の寄与」とは意味が違います。両者の値は直接比較できません。

## 再現性について

- 第三者のWebサイトから収集したオリジナル学習画像の再配布権限を確認できないため、画像は同梱しません。
- 同じ手法を再実行するためのコードは公開しますが、同じ学習済みモデルや出力画像を**完全再現するためのデータは公開していません**。
- ColabのGPU利用状況・TensorFlowのバージョン・画像の分割方法などによって結果は異なります。
- 検証集合はモデル選択に使用しており、独立した最終テスト性能ではありません。

## ライセンスと引用

コードの利用条件は [MIT License](LICENSE) です。第三者ライブラリや利用者自身の画像などはそれぞれの利用条件に従ってください。

GitHubの **Cite this repository** から引用形式を確認できます。書誌情報は [CITATION.cff](CITATION.cff) に記録してあります。著者名は **Norihiro Takahashi** として登録しています。共著者・ORCIDがある場合は、Zenodoへの初回リリース前に確認してください。

GitHub Release `v1.0.0` を作成してZenodoと連携すると、アーカイブされたバージョンのDOIを取得できます。**現時点では未発行です。**

実際の公開手順は [GitHub／Zenodo公開ガイド](PUBLISHING_GUIDE_ja.md) を参照してください。
