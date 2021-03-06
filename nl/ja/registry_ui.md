---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# イメージの脆弱性のモニタリング
{: #registry_ui}

{{site.data.keyword.Bluemix_notm}} コンソールを使用して、{{site.data.keyword.registrylong}} パブリック・リポジトリーと専用リポジトリーにあるイメージの潜在的な脆弱性とセキュリティーに関する情報を確認できます。
{:shortdesc}

**SECURITY REPORT** 列は、イメージに関する以下の情報を示します。
-   `Secure` セキュリティー問題は見つかりませんでした。
-   `Vulnerable` セキュリティーまたは構成の問題が見つかったので、イメージをデプロイする前に問題に対処する必要があります。
-   `Incomplete` スキャンは完了していません。 スキャンがまだ実行中であるか、またはイメージのオペレーティング・システムに互換性がない可能性があります。 時間を置いてからスキャンを再試行してください。 それでもスキャンが完了しない場合には、イメージを再プッシュして新たにスキャンを開始してください。 スキャンが完了していないイメージは、デプロイメント用にブロック化されません。
-   `Unsupported OS` イメージ内のオペレーティング・システムはサポートされていません。

グラフィカル・ユーザー・インターフェースを表示するには、以下の手順を使用します。

1.  IBMid を使用して {{site.data.keyword.Bluemix_notm}} コンソール ([https://console.bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net)) にログインします。
2.  複数の {{site.data.keyword.Bluemix_notm}} アカウントをお持ちの場合は、使用するアカウントと領域をアカウント・メニューから選択します。
3.  **「カタログ」**をクリックします。
4.  **「コンテナー」**カテゴリーを選択し、**「Container Registry」**タイルをクリックします。
5.  専用リポジトリー内のイメージ関連情報を表示するには、**「専用リポジトリー (Private Repositories)」**をクリックします。 専用リポジトリー内のイメージのリストと各イメージのセキュリティー・レポート状況が表示されます。 タグやイメージ・ダイジェストを含む、潜在的な脆弱性の詳細を表示するには、表の中の行をクリックします。
6.  パブリック・リポジトリー内のイメージ関連情報を表示するには、**「パブリック・リポジトリー (Public Repositories)」**をクリックします。 パブリック・リポジトリー内のイメージのリストが、各イメージの文書やセキュリティー・レポートへのリンクと共に表示されます。 タグやイメージ・ダイジェストなど、潜在的な脆弱性について詳しくは、表の中の行をクリックします。

セキュリティー・レポートの情報の意味について詳しくは、[脆弱性アドバイザーによるイメージのセキュリティーの管理](../va/va_index.html)を参照してください。
