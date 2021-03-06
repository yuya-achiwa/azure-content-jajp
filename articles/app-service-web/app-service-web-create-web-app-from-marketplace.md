<properties
	pageTitle="Azure Marketplace から Web アプリを作成する | Microsoft Azure"
	description="Azure ポータルを使用して Azure Marketplace から新しい WordPress Web アプリを作成する方法について説明します。"
	services="app-service\web"
	documentationCenter=""
	authors="rmcmurray"
	manager="wpickett"
	editor=""/>

<tags
	ms.service="app-service-web"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.date="05/10/2016"
	ms.author="robmcm"/>

<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

# Azure Marketplace から Web アプリを作成する

[AZURE.INCLUDE [タブ](../../includes/app-service-web-get-started-nav-tabs.md)]

Azure Marketplace には、Microsoft、サード パーティ企業、およびオープン ソース ソフトウェア活動によって開発された多種多様な人気の Web アプリが用意されています。たとえば、WordPress、Umbraco CMS、Drupal などです。これらの Web アプリは、この WordPress の例で使用される [PHP] をはじめ、[.NET]、[Node.js]、[Java]、[Python] など、さまざまなよく知られたフレームワーク上に構築されています。Azure Marketplace から Web アプリを作成するために必要なソフトウェアは、[Azure ポータル]に使用するブラウザーだけです。

このチュートリアルで学習する内容は次のとおりです。

* Azure Marketplace でアプリケーション テンプレートを検索する方法。
* Azure App Service でテンプレートに基づく Web アプリを作成する方法。
* 新しい Web アプリとデータベースの Azure App Service 設定を構成する方法。

このチュートリアルでは、WordPress ブログ サイトを Azure Marketplace からデプロイします。このチュートリアルの手順を完了すると、独自の WordPress サイトをクラウドで運用できるようになります。

![Example WordPress wep app dashboard][WordPressDashboard]

このチュートリアルでデプロイする WordPress サイトは、データベースに MySQL を使用します。代わりに SQL Database を使用する場合は、[Project Nami] を参照してください。これは Azure Marketplace からも入手できます。

> [AZURE.NOTE]
このチュートリアルを完了するには、Microsoft Azure アカウントが必要です。アカウントを持っていない場合は、[Visual Studio サブスクライバーの特典を有効にする][activate]か、[無料試用版にサインアップ][free trial]してください。
>
> Azure アカウントにサインアップする前に Azure App Service を開始する場合は、「[Azure App Service アプリケーションの作成]」にアクセスしてください。有効期間が短いスターター Web アプリを App Service ですぐに作成できます。このサービスの利用にあたり、クレジット カードや契約は必要ありません。

## WordPress を選択して Azure App Service 用に構成する

1. [Azure ポータル]にログインします。

1. **[新規]** をクリックします。
	
	![Create a new Azure resource][MarketplaceStart]
	
1. **WordPress** を検索し、**[WordPress]** をクリックします。MySQL の代わりに SQL Database を使用する場合は、**Project Nami** を検索してください。

	![Search for WordPress in the Marketplace][MarketplaceSearch]
	
1. WordPress アプリの説明を読んだら、**[作成]** をクリックします。

	![Create WordPress web app][MarketplaceCreate]

1. WordPress の設定ブレードが表示されます。以降の手順は、このブレードを使用して実行します。

	![Configure WordPress web app settings][ConfigStart]

1. **[Web アプリ]** ボックスに Web アプリの名前を入力します。

	Web アプリの URL は *{名前}*.azurewebsites.net のようになるため、この名前は azurewebsites.net ドメイン内で一意である必要があります。入力した名前が一意でない場合は、テキスト ボックスに赤色の感嘆符が表示されます。

	![Configure the WordPress web app name][ConfigAppName]

1. サブスクリプションが複数ある場合には、使用するものを 1 つ選択します。

	![Configure the subscription for the web app][ConfigSubscription]

1. **リソース グループ**を選択するか、新しく作成します。

	リソース グループの詳細については、「[Azure ポータルを使用した Azure リソースの管理][ResourceGroups]」を参照してください。

	![Configure the resource group for the web app][ConfigResourceGroup]

1. **App Service プラン/場所**を選択するか、新しく作成します。

	App Service プランの詳細については、[Azure App Service プランの概要][AzureAppServicePlans]に関するページを参照してください。

	![Configure the service plan for the web app][ConfigServicePlan]

1. **[データベース]** をクリックし、**[新しい MySQL データベース]** ブレードで、MySQL データベースを構成するために必要な値を指定します。

	a.新しい名前を入力するか、既定の名前をそのまま使用します。

	b.**[データベースの種類]** は **[共有]** のままにします。

	c.Web アプリ用に選択したのと同じ場所を選択します。

	d.価格レベルを選択します。このチュートリアルでは、**Mercury** (無料で、最小限の接続とディスク領域を使用可能) で問題ありません。

	e.**[新しい MySQL データベース]** ブレードで、法律条項に同意し、**[OK]** をクリックします。

	![Configure the database settings for the web app][ConfigDatabase]

1. **[WordPress]** ブレードで、法律条項に同意し、**[作成]** をクリックします。

	![Finish the web app settings and click OK][ConfigFinished]

	Azure App Service によって、通常は 1 分以内に Web アプリが作成されます。進捗状況を監視するには、ポータル ページの上部にあるベル アイコンをクリックします。

	![進捗状況インジケーター][ConfigProgress]

## WordPress Web アプリの起動と管理
	
1. Web アプリの作成が完了したら、Azure ポータルで、アプリケーションを作成したリソース グループに移動し、Web アプリとデータベースを確認できます。

	電球のアイコンが表示された追加のリソースは [Application Insights][ApplicationInsights] であり、Web アプリの監視サービスを提供します。

1. **[リソース グループ]** ブレードで、Web アプリの行をクリックします。

	![Select your WordPress web app][WordPressSelect]

1. Web アプリ ブレードで **[参照]** をクリックします。

	![Browse to your WordPress web app][WordPressBrowse]

1. WordPress ブログ用の言語を選択するように求めるメッセージが表示されたら、使用する言語を選択し、**[続行]** をクリックします。

	![Configure the language for your WordPress web app][WordPressLanguage]

1. WordPress の **[ようこそ]** ページで、WordPress に必要な構成情報を入力し、**[WordPress のインストール]** をクリックします。

	![Configure the settings your WordPress web app][WordPressConfigure]

1. **[ようこそ]** ページで作成した資格情報を使用して、ログインします。

1. サイトのダッシュボード ページが開き、入力した情報が表示されます。

	![View your WordPress dashboard][WordPressDashboard]

## 次のステップ

このチュートリアルでは、Azure Marketplace から Web アプリの例を作成してデプロイする方法を説明しました。

App Service Web Apps の使用方法の詳細については、ページの左側 (ワイド ブラウザー ウィンドウの場合) またはページの上部 (幅の狭いブラウザー ウィンドウの場合) に表示されるリンクを参照してください。

Azure での WordPress Web アプリの開発の詳細については、「[Azure App Service での WordPress の開発][WordPressOnAzure]」を参照してください。

<!-- URL List -->

[PHP]: https://azure.microsoft.com/develop/php/
[.NET]: https://azure.microsoft.com/develop/net/
[Node.js]: https://azure.microsoft.com/develop/nodejs/
[Java]: https://azure.microsoft.com/develop/java/
[Python]: https://azure.microsoft.com/develop/python/
[activate]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[free trial]: https://azure.microsoft.com/pricing/free-trial/
[Azure App Service アプリケーションの作成]: http://go.microsoft.com/fwlink/?LinkId=523751
[ResourceGroups]: ../azure-portal/resource-group-portal.md
[AzureAppServicePlans]: ../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md
[ApplicationInsights]: https://azure.microsoft.com/services/application-insights/
[Azure ポータル]: https://portal.azure.com/
[Project Nami]: http://projectnami.org/
[WordPressOnAzure]: ./develop-wordpress-on-app-service-web-apps.md

<!-- IMG List -->

[MarketplaceStart]: ./media/app-service-web-create-web-app-from-marketplace/marketplacestart.png
[MarketplaceSearch]: ./media/app-service-web-create-web-app-from-marketplace/marketplacesearch.png
[MarketplaceCreate]: ./media/app-service-web-create-web-app-from-marketplace/marketplacecreate.png
[ConfigStart]: ./media/app-service-web-create-web-app-from-marketplace/configstart.png
[ConfigAppName]: ./media/app-service-web-create-web-app-from-marketplace/configappname.png
[ConfigSubscription]: ./media/app-service-web-create-web-app-from-marketplace/configsubscription.png
[ConfigResourceGroup]: ./media/app-service-web-create-web-app-from-marketplace/configresourcegroup.png
[ConfigServicePlan]: ./media/app-service-web-create-web-app-from-marketplace/configserviceplan.png
[ConfigDatabase]: ./media/app-service-web-create-web-app-from-marketplace/configdatabase.png
[ConfigFinished]: ./media/app-service-web-create-web-app-from-marketplace/configfinished.png
[ConfigProgress]: ./media/app-service-web-create-web-app-from-marketplace/configprogress.png
[WordPressSelect]: ./media/app-service-web-create-web-app-from-marketplace/wpselect.png
[WordPressBrowse]: ./media/app-service-web-create-web-app-from-marketplace/wpbrowse.png
[WordPressLanguage]: ./media/app-service-web-create-web-app-from-marketplace/wplanguage.png
[WordPressDashboard]: ./media/app-service-web-create-web-app-from-marketplace/wpdashboard.png
[WordPressConfigure]: ./media/app-service-web-create-web-app-from-marketplace/wpconfigure.png

<!-----HONumber=AcomDC_0511_2016-->