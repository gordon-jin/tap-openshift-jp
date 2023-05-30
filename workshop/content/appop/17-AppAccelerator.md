ここからは TAP のカタログ機能である Application Accelerator
について紹介します。

この機能を使うことで、企業はアプリケーションの標準テンプレート用意し、開発者はビジネスロジックのみに専念できます。詳細は以下のブログも参考ください。

[Tanzu Application Platformでアプリの雛形をつくろう：Application
Accelerator](https://blogs.vmware.com/vmware-japan/2022/02/lets-build-catalogs-tanzu-application-platform-appaccelerator.html)

まず、既存の app accelerator を確認します。

```execute
tanzu accelerator list
```


![グラフィカル ユーザー インターフェイス, テキスト
自動的に生成された説明](../media/image79.png)

TAP GUI からも確認できます。

![グラフィカル ユーザー インターフェイス, アプリケーション
自動的に生成された説明](../media/image80.png)

まず、TAP GUI からデフォルトで提供している Application Accelerators
を一つ選んで雛形テンプレートを作成してみます。

Tanzu Java Web App を選択し、CHOOSE をクリックします。

![グラフィカル ユーザー インターフェイス, テキスト, アプリケーション
自動的に生成された説明](../media/image81.png)

数字の 9
はこの雛形テンプレートを何回ダンロードしているかを示しています。

今回は Java version として Java11 を選択し、Next をクリックします。

![グラフィカル ユーザー インターフェイス, アプリケーション
自動的に生成された説明](../media/image82.png)

「GENERATE ACCELERATOR」 をクリックします。

![グラフィカル ユーザー インターフェイス, テキスト, アプリケーション,
メール
自動的に生成された説明](../media/image83.png)

しばらく待つと、「EXPLORE ZIP FILE」 と 「DOWNLOAD ZIP
FILE」のボタンが表示されます。

今回は IDE
ツールとしてcode server を使うため、一旦はダウンロードせず、「EXPLORE
ZIP FILE」 としてテンプレートの中身を\
開いてみます。

![グラフィカル ユーザー インターフェイス, アプリケーション, Teams
自動的に生成された説明](../media/image84.png)

選んだ Java11 が workload.yaml に反映されているのを確認できます。

![グラフィカル ユーザー インターフェイス, テキスト, アプリケーション
自動的に生成された説明](../media/image85.png)

上記の画面を確認後、右下の CLOSE をクリックし、EXPLORE 画面を閉じます。
既存のApplication Acceleratorテンプレートを利用するデモは以上です。

ここからは、手動で新しいApplication Accelerators
テンプレートを登録します。Github 上の Repositoryを使って App Accelerator に登録します。

```execute
GIT_REPOSITORY_URL=https://github.com/mhoshi-vm/tap-python-recipies.git
GIT_REPOSITORY_BRANCH=main
tanzu accelerator create tap-python-recipies --git-repository ${GIT_REPOSITORY_URL} --git-branch ${GIT_REPOSITORY_BRANCH}
```


![](../media/image86.png)

<https://github.com/mhoshi-vm/tap-python-recipies/accelerator.yaml>

上記のファイルがApplication Accelerator を登録するための YAML
ファイルです。以下のような項目から構成されています。

-   displayName : TAP GUI -\> Generate Acceleratorsで表示される名前

-   description： より詳細な説明

-   iconUrl: アイコン画像を指す URL

-   options: (inputType: select) ドロップダウンリストを定義

-   engine:
    ドロップダウンリストで選択された内容に基づいて定義されたアクションを実行(今回の場合は、github
    リポジトリのサブフォルダを含める)

tanzu cli とTAP GUI
からどのように表示されているかを確認します。再度、app accelerator
を確認します。

```execute
tanzu accelerator list
```

tap-python-recipies が登録されているのを確認できます。

![テキスト
自動的に生成された説明](../media/image87.png)

TAP GUI からも新規で登録した tap-python-recipiesを確認します。

![グラフィカル ユーザー インターフェイス, アプリケーション
自動的に生成された説明](../media/image88.png)

CHOOSE ボタンをクリックし、Generate Accelerators 画面でChoose Python
Framework \* ドロップダウンリストを展開します。

![グラフィカル ユーザー インターフェイス, テキスト, アプリケーション,
メール
自動的に生成された説明](../media/image89.png)

すると、ハンズオンの各章のタイトルが表示されているのを確認できます。
「シンプルなWebアプリケーションのデプロイ」をクリックし、NEXT
ボタンをクリックします。

最後に GENERATE ACCELERATOR
ボタンをクリックし、「シンプルなWebアプリケーションのデプロイ」
テンプレートを作成します。

![グラフィカル ユーザー インターフェイス, アプリケーション
自動的に生成された説明](../media/image90.png)

EXPLORE ZIP FILE をクリックすると、git clone でダウンロードしていた
「シンプルなWebアプリケーションのデプロイ」の Python
コードを確認できます。

続いて、Application Accelerators の Create 画面-\> TAP Python Recipies
の CHOOSE を再度クリックし、\
今度は 「GitOps モードのデプロイ」を選択します。また、Branch-name \* と
Owner-name \* を下記のように変更します。

![グラフィカル ユーザー インターフェイス, テキスト, アプリケーション,
メール
自動的に生成された説明](../media/image91.png)

NEXT ボタン -\> GENERATE ACCELERATOR ボタンをクリックします。

「EXPLORE ZIP FILE」
をクリックし、生成されたテンプレートの中身を確認します。

gitops_repository_owner と gitops_branch
が反映されているのを確認できます。

![グラフィカル ユーザー インターフェイス, アプリケーション, メール
自動的に生成された説明](../media/image92.png)

このように、企業はアプリケーションの標準テンプレートを用意し、Application
Accelerator に登録することで、開発者は都度
Githubなどのリポジトリからコードをダウンロード、YAML
ファイルを個別に編集する必要なく、開発にすぐ着手できます。

Application Acceleratorのデモは以上です。