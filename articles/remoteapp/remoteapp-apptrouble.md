<properties 
    pageTitle="Azure RemoteApp のトラブルシューティング - アプリケーションの起動と接続に関するエラー | Microsoft Azure" 
    description="Azure RemoteApp でのアプリケーションの起動と接続に関する問題をトラブルシューティングする方法について説明します。" 
    services="remoteapp" 
	documentationCenter="" 
    authors="ericorman" 
    manager="mbaldwin" />

<tags 
    ms.service="remoteapp" 
    ms.workload="compute" 
    ms.tgt_pltfrm="na" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.date="05/12/2016" 
    ms.author="elizapo" />



#Azure RemoteApp のトラブルシューティング - アプリケーションの起動と接続に関するエラー 

Azure RemoteApp でホストされるアプリケーションは、さまざまな理由により起動に失敗することがあります。この記事では、アプリケーションの起動に失敗する理由と、ユーザーに表示される可能性のあるエラー メッセージについて説明します。また、接続のエラーについても説明します (ただし、Azure RemoteApp クライアントへのサインイン時の問題については扱っていません)。

それでは、アプリケーションの起動と接続に失敗したときに表示される一般的なエラー メッセージについての説明をお読みください。

##We're getting you set up...Try again in 10 minutes. (セットアップしています... 10 分後にもう一度お試しください。)

このエラーは、ユーザーの容量ニーズを満たすために Azure RemoteApp がスケール アップしていることを意味しています。ユーザーの容量ニーズに対応するため、バック グラウンドで複数の Azure RemoteApp VM インスタンスを作成しています。この処理は通常は約 5 分で完了しますが、最大で 10 分ほどかかることもあります。すぐにリソースが必要で、処理が終わるまで待てない場合もあるでしょう。たとえば、午前 9 時から多数のユーザーが同時に Azure RemoteApp 上のアプリを使用する必要がある場合などです。こうした状況が想定される場合は、バックエンドで**容量モード**を有効にすることができます。Azure サポート チケットを開くか、メールで [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com) にご連絡ください。リクエストには必ずサブスクリプション ID を記載してください。

![We are getting you set up (セットアップしています)](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## アプリケーションに自動的に再接続できません。アプリケーションを再起動してください。  

このエラー メッセージが表示されるケースとして考えられるのは、Azure RemoteApp の使用中に PC を 4 時間以上スリープ状態にし、スリープ状態から回復させたときに Azure RemoteApp クライアントが自動的に再接続しようとして、接続のタイムアウト時間を超えた場合です。アプリケーションに戻り、Azure RemoteApp クライアントからアプリケーションを開くようユーザーに指示してください。

![アプリケーションに自動で再接続できませんでした。](./media/remoteapp-apptrouble/ra-apptrouble2.png)

## Problems with the temp profile (一時プロファイルに関する問題) 

このエラーは、ユーザー プロファイル (ユーザー プロファイル ディスク) のマウントに失敗し、そのユーザーが一時的なプロファイルを受信したときに発生します。管理者が Azure ポータルのコレクションに移動し、**[セッション]** タブでユーザーを**ログオフ**してください。ユーザー セッションが完全に強制ログオフされるので、ユーザーにアプリをもう一度起動するよう指示してください。それでも解決しない場合は、Azure サポートまたはメールで [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com) にご連絡ください。

## Azure RemoteApp は動作を停止しました

このエラー メッセージは、Azure RemoteApp クライアントに問題があり、再起動する必要があることを意味しています。**[プログラムの終了]** を選択して Azure RemoteApp クライアントを終了し、再起動するようユーザーに指示してください。それでも問題が解決しない場合は、Azure サポート チケットを開くか、メールで [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com) にお問い合わせください。

![Azure RemoteApp は動作を停止しました](./media/remoteapp-apptrouble/ra-apptrouble3.png)

## リモート デスクトップ接続を使用してこのリソースへアクセスする際にエラーが発生しました。もう一度接続するか、システム管理者に問い合わせてください。

これは一般的なエラー メッセージです。Azure サポートに問い合わせるか、メールで [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com) に問い合わせてください。調査を行います。

![Azure RemoteApp の一般的なエラー メッセージ](./media/remoteapp-apptrouble/ra-apptrouble4.png)

<!---HONumber=AcomDC_0518_2016-->