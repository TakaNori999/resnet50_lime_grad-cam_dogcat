# GitHub公開ガイド（2026年11月時点）

## v1.0.0の公開・DOI発行状況

- GitHub Release: [v1.0.0](https://github.com/TakaNori999/resnet50_lime_grad-cam_dogcat/releases/tag/v1.0.0)
- Zenodo: **Published（公開済み）**
- DOI: **[10.5281/zenodo.23992583](https://doi.org/10.5281/zenodo.23992583)**
- 公開版のREADMEおよびCITATION.cffにDOIを追記済み。Zenodoのv1.0.0は公開時点のスナップショットであり、その後のGitHub上の変更は自動的に反映されません。



公開先: [TakaNori999/resnet50_lime_grad-cam_dogcat](https://github.com/TakaNori999/resnet50_lime_grad-cam_dogcat)

## 公開範囲

- 公開: Colab用 `.ipynb`、README、LICENSE、CITATION.cff、requirements.txt、.gitignore。
- 公開しない: 画像データ、テスト画像、学習済みモデル、ノートブックに保存された実行画像。
- 利用者が自分で犬・猫の画像をDriveに置いて実行する方式です。初期設定は `MyDrive/dog_cat_100images/cat/` と `dog/` に各100枚です。
- 元の学習データと学習済み重みを含めないため、実験の手順は再実行できますが、元の数値結果の完全再現は保証できません。

## Open in Colab

[Google Colabでノートブックを開く](https://colab.research.google.com/github/TakaNori999/resnet50_lime_grad-cam_dogcat/blob/main/ResNet50_DogCat_LIME_GradCAM.ipynb)

ノートブック第2節の `DATA_DIR` と `OUTPUT_ROOT` を設定し、上から順に実行します。第10節で `TEST_IMAGE_PATH` を指定すると、LIMEとGrad-CAMの比較図を生成できます。任意の第11～13節は削除済みです。

## GitHub上でのコード更新

- ルート直下の `ResNet50_DogCat_LIME_GradCAM.ipynb` を同じファイル名で更新します。
- Colabで実行したノートブックをアップロードする前に、出力画像・ウィジェット状態・履歴・個人情報が含まれていないか確認します。
- `.gitignore` は今後の意図しない追加を防ぐものですが、すでにコミットしたファイルや過去の履歴を削除する機能はありません。

## MIT Licenseと引用

- `LICENSE` にコードの利用条件を記載しています。ライブラリ、画像、事前学習済み重みには別の条件が適用されます。
- `CITATION.cff` に著者名 **Norihiro Takahashi** とリポジトリURLを記載しています。引用する場合はGitHubの **Cite this repository** を参照してください。

## 過去の画像付きコミットへの対応（重要）

このリポジトリの古いコミットには、LIME・Grad-CAMの実行画像を埋め込んだノートブックが存在することを確認しています。最新ファイルで画像を削除しても、古いコミットは消えません。

画像を再配布しない方針を徹底する場合は、古いリポジトリをPrivateに変更して保管用の名前に変更し、最新の公開可能なファイルだけを使って、新しいPublicリポジトリを作成してください。**ZIPのスナップショットから新しく作成し、古い `.git` 履歴を引き継がないことが重要です。**

旧リポジトリをPrivateに変更しても、第三者が取得済みのコピーを回収することはできません。履歴の強制書き換えも可能ですが、古いSHAへの参照やキャッシュが残る可能性があるため、慎重な対応が必要です。

公式案内: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository

## 最終確認

- 英語・日本語READMEと `CITATION.cff` のURLが実際の公開先と一致している
- Open in Colabから最新コードを開き、別途用意した画像で正常実行できる
- **公開する履歴**に再配布権利が不明な画像を含まない
- ノートブックの保存済み出力・ウィジェット状態が空である
- バージョン・依存関係・実行方法・画像の非公開方針が記載されている
