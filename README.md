# rep-test-github-actions

Github Actionsテスト用のリポジトリ

```
├─.github
│  │  PULL_REQUEST_TEMPLATE.md       : PULL_REQUEST_TEMPLATEサンプル
│  │  release-drafter.yml            : release-drafterサンプル(workflows内の同名ファイルと一体で動く)
│  │  
│  └─workflows
│          actions001.yml            : AWS CodeBuildの実行サンプル
│          auto-assign-author.yml    : auto-assign-authorサンプル
│          automated-npm-update.yml  : automated-npm-updateサンプル
│          release-drafter.yml       : release-drafterサンプル(.github直下の同名ファイルと一体で動く)
│
├─ .node-version     : automated-npm-updateで
├─ package-lock.json : 更新されるpackageのサンプル
├─ package.json      : (中は適当なもの)
└─ README.md
```

### PULL_REQUEST_TEMPLATE

Pull Requestを作成した時に、詳細に設定されるテンプレート

`.githu/PULL_REQUEST_TEMPLATE.md` を置いておけばその中身が設定される

### auto-assign-author

Pull Requestを作成した時に、作成者を担当者に自動でアサインするテンプレート

`.githu/workflows/auto-assign-author.yml` を置いておけば実行される

### release-drafter

Release(draft) https://github.com/SGA-yasushi-nakatsukasa/rep-test-github-actions/releases を自動で作成する処理のサンプル

mainブランチへのコミットがあるとまず `.githu/workflows/release-drafter.yml` が実行され、次のバージョンを決定する。バージョンは `'v' + yyyy.mm.<通し番号>` という体系になっており、月跨ぎの場合は新しい月のバージョン0となる。その後、`.githu/release-drafter.yml` によってそのバージョンが作成される。

### AWS CodeBuildの実行

ブランチへのコミットをトリガとして、AWS CodeBuildプロジェクトを実行する処理のサンプル

この実行前にAWS側に適切な権限設定がされている必要がある。

### automated-npm-update

ブランチへのコミットをトリガとして、package.json内のパッケージのバージョンを更新する処理のサンプル

ここではpackage.json更新後、npm install / npm updateを実行し（package-lock.jsonが更新される）、それらの更新を含めたPull Requestを自動作成するところまで実施している。

以上
