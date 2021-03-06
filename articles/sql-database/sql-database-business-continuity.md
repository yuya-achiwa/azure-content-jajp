<properties
   pageTitle="クラウド ビジネス継続性 - データベース復旧 - SQL Database | Microsoft Azure"
   description="Azure SQL Database がどのようにクラウド ビジネス継続性とデータベース復旧をサポートし、ミッション クリティカルなクラウド アプリケーションの実行を維持できるようにするかについて説明します。"
   keywords="ビジネス継続性, クラウド ビジネス継続性, データベースの障害復旧, データベース復旧"
   services="sql-database"
   documentationCenter=""
   authors="carlrabeler"
   manager="jhubbard"
   editor="monicar"/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="sqldb-bcdr"
   ms.date="06/09/2016"
   ms.author="carlrab"/>

# 概要: Azure SQL Database によるクラウド ビジネス継続性とデータベース障害復旧

> [AZURE.SELECTOR]
- [ポイントインタイム リストア](sql-database-point-in-time-restore.md)
- [削除済みデータベースの復元](sql-database-restore-deleted-database.md)
- [geo リストア](sql-database-geo-restore.md)
- [アクティブ geo レプリケーションを選択するとき](sql-database-geo-replication-overview.md)
- [ビジネス継続性のシナリオ](sql-database-business-continuity-scenarios.md)

Azure SQL Database では、さまざまなビジネス継続性ソリューションを提供しています。ビジネス継続性とは、ビジネス機能を実行するアプリケーションの機能が永続的または一時的に停止してしまう計画的または計画外の破壊的なイベントに対し、回復力に富む方法でアプリケーションを設計、デプロイ、実行することです。計画外のイベントには、人的エラーから永続的または一時的な停止、特定の Azure リージョンにおける広範囲の損失を引き起こす可能性のある地域的な災害までさまざまものがあります。計画的なイベントには、別のリージョンへのアプリケーションの再デプロイやアプリケーションのアップグレードが含まれます。ビジネス継続性の目的は、こうしたイベント発生時おけるビジネス機能への影響を最小限に抑え、アプリケーションが継続して機能するようにすることです。

SQL Database のクラウド ビジネス継続性ソリューションについて説明するうえで、いくつかの概念を理解していただく必要があります。次のとおりです。

* **障害復旧 (DR):** アプリケーションの通常のビジネス機能を復旧するプロセス。

* **推定復旧時間 (ERT):** 復元またはフェールオーバーの要求の後に完全に使用可能になるデータベースの推定時間。

* **目標復旧時間 (RTO):** 破壊的なイベントの後に、アプリケーションが完全に復旧するまでの最大許容時間。RTO は障害時において失われる可用性の最大量を計測します。

* **目標復旧時点 (RPO):** 破壊的なイベントの後に完全に回復する時点までに、アプリケーションが失うことができる最終更新の最大量 (時間)。RPO は障害時において失われるデータの最大量を計測します。


## SQL Database クラウド ビジネス継続性のシナリオ

ビジネス継続性とデータベース復旧を計画する際に考慮する必要がある主なシナリオを次に示します。

### ビジネス継続性のためのアプリケーション設計

現在構築しているアプリケーションはビジネスにとって重要になります。サービスの致命的なエラーとなる地域的な災害を克服できるように設計・構成します。アプリケーションの RPO と RTO の要件は把握しており、これらの要件を満たす構成を選択するつもりです。

### 人的エラーからの回復

アプリケーションの実稼働バージョンにアクセスする管理者の権限があります。定期的なメンテナンス処理の一環として、操作を誤り実稼働環境での重要なデータを削除してしまいました。エラーの影響を軽減するために、データを迅速に復元したいと思います。

### 障害からの回復

実稼働環境でアプリケーションを実行しており、導入しているリージョンで大規模な障害があることを示すアラートを受信します。回復プロセスを開始し、別のリージョンで再開してビジネスへの影響を軽減したいと思います。

### 障害復旧の訓練の実行

障害からの回復によってアプリケーションのデータ層が別のリージョンに再配置されるため、回復プロセスを定期的にテストし、アプリケーションへの影響を評価して備えたいと思います。

### ダウンタイムのないアプリケーションのアップグレード

アプリケーションの主要アップグレードをリリースします。これには、データベース スキーマの変更、追加のストアド プロシージャのデプロイなどが含まれます。このプロセスでは、データベースへのユーザー アクセスを停止する必要があります。同時に、アップグレードで業務が大幅に中断しないようにします。

## SQL Database のビジネス継続性機能

次の表では、SQL Database のビジネス継続性機能を一覧にまとめ、[サービス レベル](sql-database-service-tiers.md)間の相違点を示しています。

| 機能 | Basic レベル | Standard レベル |Premium レベル
| --- | --- | --- | ---
| ポイントインタイム リストア | 7 日間以内のあらゆる復元ポイント | 14 日間以内のあらゆる復元ポイント | 35 日間以内のあらゆる復元ポイント
| geo リストア | ERT < 12 時間、RPO < 1 時間 | ERT < 12 時間、RPO < 1 時間 | ERT < 12 時間、RPO < 1 時間
| アクティブ geo レプリケーションを選択するとき | ERT < 30 秒、RPO < 5 秒 | ERT < 30 秒、RPO < 5 秒 | ERT < 30 秒、RPO < 5 秒

これらの機能は、前述のシナリオに対応します。特定の機能を選択する方法については[ビジネス継続性のための設計](sql-database-business-continuity-design.md)セクションをご覧ください。

> [AZURE.NOTE] ERT と RPO の値は技術的な目標であり、ガイダンスの提供のみを目的としています。これらは、[SQL Database の SLA](https://azure.microsoft.com/support/legal/sla/sql-database/v1_0/) の一部ではありません。


###ポイントインタイム リストア

[ポイントインタイム リストア](sql-database-point-in-time-restore.md)は、データベースを以前の任意の時点に戻すことを目的としています。これは、データベース バックアップ、差分バックアップ、サービスがすべてのユーザー データベースを自動的に管理するトランザクション ログ バックアップを使用します。この機能は、すべてのサービス レベルで使用できます。Basic では 7 日間、Standard では 14 日間、Premium では 35 日間戻ることができます。

### 地理リストア

[geo リストア](sql-database-geo-restore.md)も、Basic、Standard、Premium のデータベースで利用できます。データベースがホストされているリージョンでのインシデントのためにデータベースが利用できない場合にも既定の復旧オプションを提供します。ポイントインタイム リストアと同様に、geo リストアも Azure の地理冗長ストレージでのデータベースのバックアップに依存します。geo レプリケーション バックアップ コピーからリストアするため、プライマリ リージョンにおけるストレージの障害に対する回復力があります。

### アクティブ geo レプリケーションを選択するとき

[アクティブ geo レプリケーション](sql-database-geo-replication-overview.md)は、すべてのデータベース レベルで使用できます。アクティブ geo レプリケーションは、geo リストアよりもアグレッシブな復旧要件があるアプリケーション用に設計されています。アクティブ geo レプリケーションを使用して、別のリージョン内のサーバーで最大 4 つの読み取り可能なセカンダリを作成できます。いずれかのセカンダリへのフェールオーバーを開始できます。さらに、アクティブ geo レプリケーションを使用すると、[アプリケーションのアップグレードや再配置のシナリオ](sql-database-manage-application-rolling-upgrade.md)をサポートするだけでなく読み取り専用ワークロードの負荷を分散することができます。

## ビジネス継続性機能の選択

ビジネス継続性のためにアプリケーションを設計するには、次の質問に答える必要があります。

1. アプリケーションを障害から保護するために適切なビジネス継続性の機能はどれでしょうか。
2. どのレベルの冗長性とレプリケーション トポロジを使用するでしょうか。

エラスティック プールを使用した場合の復旧戦略の詳細については、「[SQL Database エラスティック プールを使用した、アプリケーションの障害復旧戦略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)」をご覧ください。

### geo リストアを使用する場合

[geo リストア](sql-database-geo-restore.md)は、データベースがホストされているリージョンでのインシデントのためにデータベースが利用できない場合にも既定の復旧オプションを提供します。SQL Database では、既定ですべてのデータベースにおける基本的な保護が組み込まれています。これは geo 冗長 Azure ストレージ (GRS) に[データベースのバックアップ](sql-database-automated-backups.md)を格納することで行われます。この方法を選択する場合、特別に構成したり、別のリソースを割り当てる必要はありません。これらの自動 geo 冗長バックアップから新しいデータベースに復元すると、任意のリージョンにデータベースを回復できます。

アプリケーションが次の条件を満たす場合は組み込まれている保護を使用する必要があります。

1. ミッション クリティカルとして考慮されない場合。拘束力のある SLA はないため、24 時間以上のダウンタイムで財務責任が課せられることはありません。
2. データ変更レートが低い場合 (1 時間あたりのトランザクションなど)。RPO が 1 時間でも大規模なデータの損失は発生しません。
3. アプリケーションは費用重視なので、geo レプリケーションの追加コストは正当化できません。 

> [AZURE.NOTE] geo リストアでは、特定のリージョンにコンピューティング容量を事前に割り当て、システム停止時にバックアップからアクティブなデータベースを復元することはありません。サービスでは、そのリージョンの既存のデータベースへの影響を最小限に抑え、容量の要求を最優先する形でgeo リストアのリクエストに関連するワークロードを管理します。そのため、データベースの復旧時間は、同じリージョンで同時に回復するその他のデータベースの量、データベースのサイズ、トランザクション ログの数、ネットワーク帯域幅などによって異なります。

### アクティブ geo レプリケーションを使用する場合

[アクティブ geo レプリケーション](sql-database-geo-replication-overview.md)を使用すると、プライマリとは異なるリージョンに読み取り可能な (セカンダリ) データベースを作成し、非同期レプリケーション メカニズムを使用して、それらのデータベースを最新の状態に保つことができます。これにより、データベースには必要なデータとコンピューティング リソースを持たせ、回復後のアプリケーションのワークロードをサポートすることが保証されます。

アプリケーションが次の条件を満たす場合はアクティブ geo レプリケーションを使用する必要があります。

1. ミッション クリティカルな場合。アグレッシブな RPO と RTO で、拘束力のある SLA がある場合。データや可用性の損失により財務責任が発生します。 
2. データ変更レートが高い場合 (1 分または 1 秒あたりのトランザクションなど)。既存の保護に関連した RPO が 1 時間の場合は、許容できないデータ損失が発生する可能性が高くなります。
3. geo レプリケーションの使用に関連するコストは、潜在的な財務責任とビジネスの関連する損失を大幅に下回る場合。


## 次のステップ

- Azure SQL Database 自動バックアップの詳細については、「 [SQL Database automated backups (SQL Database 自動バックアップ)](sql-database-automated-backups.md)」をご覧ください。
- Azure SQL Database 自動バックアップを使用して、データベースの特定の時点への復元を実行する方法については、[ポイントインタイム リストア](sql-database-point-in-time-restore.md)に関するページをご覧ください。
- Azure SQL Database 自動バックアップを使用して、削除されたデータベースを復元する方法については、「[Restore deleted database (削除済みデータベースの復元)](sql-database-restore-deleted-database.md)」をご覧ください。
- Azure SQL Database 自動バックアップを使用して、データベースのgeo リストアを実行する方法については、[geo リストア](sql-database-geo-restore.md)に関するページをご覧ください。
- ビジネス継続性のアクティブ geo レプリケーションを構成および使用する方法については、[アクティブ geo レプリケーション](sql-database-geo-replication-overview.md)に関するページをご覧ください。

## その他のリソース

- [障害からの回復](sql-database-disaster-recovery.md)
- [ユーザー エラーからの復旧](sql-database-user-error-recovery.md)
- [障害復旧の訓練の実行](sql-database-disaster-recovery-drills.md)
- [復旧後のセキュリティ管理](sql-database-geo-replication-security-config.md)
- [SQL Database アクティブ geo レプリケーションを使用したクラウド アプリケーションのローリング アップグレードの管理](sql-database-manage-application-rolling-upgrade.md)
- [障害復旧のためのクラウド ソリューションの設計](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
- [SQL Database エラスティック プールを使用した、アプリケーションの障害復旧戦略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)
- [geo レプリケーションを使用して障害復旧を実現するクラウド ソリューションの設計](sql-database-designing-cloud-solutions-for-disaster-recovery.md)

<!---HONumber=AcomDC_0622_2016-->