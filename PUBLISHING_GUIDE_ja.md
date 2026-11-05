# GitHub公開・Colab・Zenodo連携ガイド（2026年11月時点）

現在のリポジトリ: [TakaNori999/resnet50_lime_grad-cam_dogcat](https://github.com/TakaNori999/resnet50_lime_grad-cam_dogcat)

## 1. 公開対象と公開しないもの
- 公開: `ResNet50_DogCat_LIME_GradCAM.ipynb`、README、MIT License、CITATION.cff、requirements.txt、.gitignore
- 非公開: 犬・猫の画像、テスト画像、学習済みモデル、実行結果に含まれる画像。
- Google Drive上に学習画像を自分で用意します。デフォルトは `MyDrive/dog_cat_100images/cat/` と `dog/` に各100枚です。
- 実験フローの再実行はできますが、学習データや重みを含まないため元の結果を完全再現する保証はありません。

## 2. Open in Colab
[Open in Colab](https://colab.research.google.com/github/TakaNori999/resnet50_lime_grad-cam_dogcat/blob/main/ResNet50_DogCat_LIME_GradCAM.ipynb) をクリックしてください。
ColabでGPUランタイムを選び、冒頭から実行します。第2節で `DATA_DIR` を設定し、最終画像を比較する場合のみ第10節の `TEST_IMAGE_PATH` または第11節の `TEST_IMAGE_DIR` を指定してください。初期値は空欄です。

## 3. 変更・更新
GitHubのルート直下 `ResNet50_DogCat_LIME_GradCAM.ipynb` を、同じパス・名前で更新します。公開前に、Colabで「すべての出力を消去」してから保存することを推奨します。
リポジトリは既に公開済みなので、ZIPの初期アップロード手順は不要です。

## 4. 著者・ライセンス・引用
- `CITATION.cff` の著者名は **Norihiro Takahashi** です。必要に応じて共著者・ORCIDを追加してください。
- `LICENSE` はMIT Licenseです。依存ライブラリや利用者が用意した画像のライセンスは別です。
- DOIはZenodoで発行されてから `CITATION.cff` とREADMEに正しい番号を追記します。未発行のDOIを記載しないでください。

## 5. ZenodoとGitHub Release
1. [Zenodo](https://zenodo.org/) でGitHub認証・連携を有効にします。
2. 対象のGitHubリポジトリ `TakaNori999/resnet50_lime_grad-cam_dogcat` を有効にします。
3. 公開予定ファイルに不備がないことを確認してから、GitHub Releasesで `v1.0.0` を公開します。
4. Zenodoのアーカイブが成功し、バージョンDOIが発行されたことを確認します。
5. DOIをREADMEと `CITATION.cff` に反映し、引用時には論文に対応するバージョンDOIを使います。

公式: https://help.zenodo.org/docs/github/

## 6. 重要：Git履歴と非公開画像
**現行ノートブックの出力削除は、過去のコミット履歴を消去しません。**
一度公開した画像・実行出力は、旧コミットから閲覧・複製できる可能性があります。履歴からの完全な除去が必要な場合は、GitHub公式の機密情報削除手順に沿った履歴の書き換え・対応を検討してください。履歴書き換えはコミットSHAや既存のリンクに影響します。既に取得・複製された第三者側のコピーまでは消せません。
参考: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository

## 7. 公開チェック
- README (英語・日本語) とCITATION.cffのURLが現行リポジトリを指しているか
- Open in Colabでルート直下のノートブックが開くか
- 現行ノートブックに画像・実行出力・ウィジェット状態がないか
- 個人情報・画像データを追加コミットしていないか
- `.gitignore` が正しいファイル名か
- 初回Release前に著者、コード動作、実験条件、依存関係、画像の権利を最終確認したか
