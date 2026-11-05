# GitHubとZenodoへの公開手順（日本語）

**公開対象**：ソースコード（`.ipynb`）・README・MIT License・CITATION.cff・requirements.txt・.gitignore。**非公開**：犬猫各100枚の学習画像、テスト画像、学習済みモデル、ノートブックの過去の実行出力。

## 0. 公開前の確認（重要）

- ZIPファイルを展開してください。**ZIPをそのままGitHubの1ファイルとしてアップロードしない**でください。展開した中身をリポジトリのルートに配置します。
- `notebooks/ResNet50_DogCat_LIME_GradCAM.ipynb` の出力は全セル削除済みです。公開前に画像・秘密情報が残っていないかご自身でも確認してください。**公開前に画像付きで再実行してそのままコミットしない**でください。
- `CITATION.cff` と `LICENSE` の著者表示は現在 `TakaNori999` です。正式な研究者名、共著者、ORCID、著作権者が別にある場合は**初回リリース前に修正**してください。
- MITの適用対象は、あなたが利用権限を持つこのリポジトリのコードです。第三者の著作物・依存ライブラリ・画像の権利まで移転させません。既存コードを流用している場合、元のライセンスもご確認ください。
- 学習データは公開されないため、他者が**実験フローを再実行**することはできますが、公開論文のモデルや数値結果を厳密に再現できることは保証しません。

## 1. GitHubリポジトリを作る

1. GitHubの [新規リポジトリ作成](https://github.com/new) を開きます。
2. Owner：`TakaNori999`、Repository name：`resnet50-lime-gradcam-dogcat`、Visibility：`Public`。
3. 説明文（例）：`Colab notebook for ResNet50 fine-tuning and LIME/Grad-CAM comparison (code only)`。
4. 今回はローカルにREADME/LICENSEが既にあるので、初期化時の **Add README, Add .gitignore, Choose a license** はすべて不要です。
5. **Create repository** を押します。

公開予定URL（作成後に有効）: https://github.com/TakaNori999/resnet50-lime-gradcam-dogcat

## 2. ファイルをアップロード

**方法A：ブラウザ** — ZIPを展開し、GitHubのリポジトリで **Add file → Upload files** を選択します。展開したフォルダ内の各ファイルと`notebooks/`、`docs/`を保持してアップロードします。ブラウザ上で階層が維持できないときは、サブフォルダを個別に作成するかGitHub Desktopを利用します。保存先がリポジトリのルートになるようにしてください。

**方法B：Gitコマンド** — ZIPを展開したフォルダを開き、次のコマンドを実行します（gitがインストール済みで、GitHub認証が設定済みの場合）。

```bash
git init
git branch -M main
git add .
git commit -m "Initial public code release"
git remote add origin https://github.com/TakaNori999/resnet50-lime-gradcam-dogcat.git
git push -u origin main
```

## 3. Open in Colabを確認する

- [Open in ColabのURL（リポジトリ作成後に有効）](https://colab.research.google.com/github/TakaNori999/resnet50-lime-gradcam-dogcat/blob/main/notebooks/ResNet50_DogCat_LIME_GradCAM.ipynb)
- GitHubのREADMEにもバッジを組み込んであります。
- Colabで開いたら、**利用者自身**がDrive上に`cat/`・`dog/`を用意し、第2節のパスを設定します。
- リポジトリへの公開と、Colab上のユーザーアカウントのDrive内データは独立しています。

## 4. CITATION.cffの確認

- `CITATION.cff`をルートに置くと、GitHubのリポジトリ画面に**Cite this repository**が現れます。
- `authors`（正式名・共著者・ORCIDなど）をZenodo初回リリースの前に確定してください。
- 初期ファイルには**実在しないDOIやリリース日を記載していません**。

GitHub公式: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-citation-files

## 5. Zenodoと連携してバージョンDOIを取得する

1. https://zenodo.org/ にアクセスし、GitHubアカウントで登録・ログイン（あるいはLinked accountsから連携）。
2. プロフィールの **GitHub** を開き、 **Sync now** でリポジトリ一覧を更新します。
3. `TakaNori999/resnet50-lime-gradcam-dogcat` を探し、連携トグルを有効にします。
4. GitHubで **Releases → Draft a new release**。タグ `v1.0.0` を作成して公開します。
5. Zenodoでアーカイブ完了を確認し、**実際に発行されたバージョンDOI**を控えます。
6. READMEとCITATION.cffの`doi`に発行済みのDOIを追記します。その変更をGitHubにコミットしてください。
7. 論文には、解析に使用した**特定バージョン**のDOIを引用します。Zenodoには複数版を束ねるConcept DOIと、個別バージョンのDOIがあります。

Zenodo公式: https://help.zenodo.org/docs/github/enable-repository/ および https://help.zenodo.org/docs/github/archive-software/github-upload/

**重要：** GitHubへのアップロードだけではZenodo DOIは付与されません。リポジトリ公開後のZenodo連携とRelease公開が必要です。

## 6. 公開後の確認

- READMEの「Open in Colab」が開く。
- `notebooks/`内のノートブックの**出力セルが空**であり、非公開画像を含まない。
- `LICENSE`がGitHubの画面でMITと認識される。
- `Cite this repository`が表示される。
- Zenodoの記録にGitHub Release、バージョン、発行DOIが対応している。

## 参考となる公式ページ

- GitHub ファイルの追加: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository
- GitHub DOIの案内: https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content
- Zenodo GitHub integration: https://help.zenodo.org/docs/github/
- Google Colab FAQ: https://research.google.com/colaboratory/faq.html
