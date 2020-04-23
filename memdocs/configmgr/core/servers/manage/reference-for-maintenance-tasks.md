---
title: メンテナンス タスクのリファレンス
titleSuffix: Configuration Manager
description: Configuration Manager サイトの各メンテナンス タスクの詳細です
ms.date: 03/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9964834bf3a6bfa8e5c0a0bb70039554134490ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708540"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Configuration Manager でのメンテナンス タスクのリファレンス

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager サイトの各メンテナンス タスクの詳細を一覧表示します。 各エントリでは、そのタスクを使用できるサイトの種類と、それが既定で有効になっているかどうかが指定されます。

詳細については、「[メンテナンス タスクの設定](maintenance-tasks.md#set-up-maintenance-tasks)」をご覧ください。  

## <a name="tasks"></a>[タスク]

### <a name="backup-site-server"></a>サイト サーバーのバックアップ

サイトや Configuration Manager データベースを復元するために、このタスクを使って、重要な情報のバックアップを作成します。 詳細については、「[Configuration Manager サイトのバックアップ](backup-and-recovery.md)」をご覧ください。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|無効|
|セカンダリ サイト|利用不可|

### <a name="check-application-title-with-inventory-information"></a>インベントリ情報のアプリケーション タイトルの確認

このタスクを使って、ソフトウェア インベントリと資産インテリジェンス カタログの間でソフトウェア タイトルの整合性を維持します。 詳細については、[資産インテリジェンスの概要](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)に関するページをご覧ください。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|プライマリ サイト|利用不可|
|セカンダリ サイト|利用不可|

### <a name="clear-undiscovered-clients"></a>検出されなかったクライアントのクリア

> [!Tip]
> このタスクは、 **[インストール フラグのクリア]** という名前のコンソールにも表示される場合があります。

このタスクは、 **[クライアント再探索]** 期間に定期探索レコードを送信しないクライアントのインストール済みフラグを削除する場合に使用します。 インストール済みフラグは、アクティブな Configuration Manager クライアントを持つコンピューターに、自動クライアント プッシュ インストールが行われることを防ぎます。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|無効|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-application-request-data"></a>期限切れのアプリケーション要求データの削除

このタスクは、期限切れのアプリケーション要求をデータベースから削除する場合に使用します。 詳細については、「[アプリケーションの作成と展開](../../../apps/get-started/create-and-deploy-an-application.md)」を参照してください。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-application-revisions"></a>期限切れのアプリケーションのリビジョンの削除

このタスクは、参照されなくなったアプリケーションのリビジョンを削除する場合に使用します。 詳しくは、[アプリケーションを修正して置き換える方法](../../../apps/deploy-use/revise-and-supersede-applications.md)に関するページをご覧ください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-client-download-history"></a>期限切れクライアントのダウンロード履歴の削除

このタスクは、クライアントが使用するソースのダウンロードに関する履歴データを削除する場合に使用します。 サイトによって、ソースのダウンロードに関する情報が使用され、[クライアント データ ソース ダッシュボード](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)が設定されます。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-client-operations"></a>期限切れのクライアント操作を削除

このタスクを使って、クライアント操作のすべての期限切れデータをサイト データベースから削除します。 たとえば、このデータには次の操作が含まれます。

- 期限切れのクライアント通知 (コンピューターやユーザー ポリシーのダウンロード要求など)
- Endpoint Protection (スキャンや更新された定義のダウンロードを実行させるよう、管理ユーザーがクライアントに送る要求など)

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-client-presence-history"></a>期限切れクライアントのプレゼンス履歴の削除
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
このタスクは、クライアント通知によって記録されたクライアントのオンライン状態に関する履歴情報を削除する場合に使用します。 これにより、指定した時間よりも古い状態を持つクライアントの情報が削除されます。 詳細については、[クライアントを監視する方法](../../clients/manage/monitor-clients.md)に関するページを参照してください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>期限切れのクラウド管理ゲートウェイ トラフィックデータの削除

このタスクは、[クラウド管理ゲートウェイ](../../clients/manage/cmg/plan-cloud-management-gateway.md)を通過するトラフィックに関するすべての期限切れデータを、サイト データベースから削除する場合に使用します。 このデータには次が含まれます。

- 要求数
- 要求の合計バイト数
- 応答の合計バイト数
- 失敗した要求数
- 最大同時要求数

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-cmpivot-results"></a>期限切れの CMPivot の結果の削除

このタスクを使って、サイト データベースから、CMPivot クエリのクライアントの期限切れの情報を削除します。 詳細については、[リアルタイム データに対する CMPivot](cmpivot.md) に関するページをご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-collected-files"></a>期限切れの収集ファイルの削除

このタスクは、収集するファイルに関する期限切れの情報をデータベースから削除する場合に使用します。 また、このタスクは、選択したサイトのサイト サーバーのフォルダー構造から収集したファイルを削除します。 既定では、収集ファイルのうち、新しい順に 5 ファイルが、サイト サーバーの **Inboxes\sinv.box\FileCol** ディレクトリに格納されます。 詳しくは、「[ソフトウェア インベントリの概要](../../clients/manage/inventory/introduction-to-software-inventory.md)」をご覧ください。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-computer-association-data"></a>期限切れのコンピューターの関連付けデータの削除

このタスクは、OS の展開に関する期限切れのコンピューターの関連付けデータをデータベースから削除する場合に使用します。 この情報は、タスク シーケンスの間にユーザー状態を復元するときに使用されます。 詳細については、「[ユーザー状態の管理](../../../osd/get-started/manage-user-state.md)」を参照してください。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-console-connection-data"></a>期限切れのコンソール接続データの削除

このタスクにより、サイトへのコンソール接続に関するデータがサイト データベースから削除されます。<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-delete-detection-data"></a>期限切れの削除検出データの削除

このタスクは、抽出ビューによって作成されたデータの期限切れデータをデータベースから削除する場合に使用します。 これにより、データベースからデータを抽出する外部システムによって使用される、データ変更に関する古い情報が削除されます。<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-device-wipe-record"></a>期限切れのデバイス ワイプ レコードの削除

このタスクは、モバイル デバイスのワイプ アクションに関する期限切れデータを、データベースから削除する場合に使用します。 詳細については、[ワイプ、ロック、またはパスコードのリセットを使用したデータの保護](../../../mdm/deploy-use/wipe-lock-reset-devices.md)に関するページをご覧ください。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-discovery-data"></a>期限切れの探索データの削除

このタスクは、期限切れの探索データをデータベースから削除する場合に使用します。 このデータには、以下からのレコードが含まれる可能性があります。

- 定期探索
- ネットワーク検出
- Active Directory 探索方法:システム、ユーザー、およびグループ

このタスクによって、無効としてマークされている期限切れデバイスも削除されます。 このタスクを 1 つのサイトで実行すると、そのサイトに関連付けられたデータが削除され、それらの変更が他のサイトにレプリケートされます。 詳細については、「[探索を実行する](../deploy/configure/run-discovery.md)」を参照してください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-distribution-point-usage-stats"></a>期限切れの配布ポイントの使用状況の統計の削除

このタスクは、指定された時間を越えて格納されている配布ポイントの期限切れデータをデータベースから削除する場合に使用します。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-enrolled-devices"></a>期限切れの登録デバイスの削除

このタスクは、指定した期間にサイトにまったく情報を報告しなかったモバイル デバイスに関する期限切れデータをサイト データベースから削除する場合に使用します。

このタスクは、Configuration Manager [オンプレミス MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) に登録されているデバイスに適用されます。 このようなデバイスについて詳しくは、[クライアントとデバイスのサポートされるオペレーティング システム](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)に関するページをご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|無効|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-ep-health-status-history-data"></a>期限切れの EP ヘルス状態の履歴データの削除

このタスクは、Endpoint Protection (EP) の期限切れの状態情報をデータベースから削除する場合に使用します。 詳細については、[Endpoint Protection の監視方法](../../../protect/deploy-use/monitor-endpoint-protection.md)に関するページを参照してください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-exchange-partnership"></a>期限切れの Exchange パートナーシップの削除

> [!Tip]
> > このタスクは、 **[Exchange Server コネクタで管理される期限切れのデバイスを削除]** という名前のコンソールにも表示される場合があります。

このタスクは、Exchange Server コネクタによって管理されているモバイル デバイスに関する期限切れデータを削除する場合に使用します。 サイトでは、Exchange Server コネクタのプロパティの **[探索]** タブにある **[次の日数以上、非アクティブになっているモバイル デバイスを無視する]** 設定に従って、このデータが削除されます。 詳しくは、「[Configuration Manager と Exchange によるモバイル デバイスの管理](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-inventory-history"></a>期限切れのインベントリ履歴の削除

このタスクは、指定した時間を越えて格納されているインベントリ データをデータベースから削除する場合に使用します。 詳細については、[リソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)に関するページをご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-log-data"></a>期限切れのログ データの削除

このタスクは、トラブルシューティングに使用された期限切れのログ データをデータベースから削除する場合に使用します。 このデータは Configuration Manager コンポーネントの操作には関連していません。  

> [!IMPORTANT]  
> 既定では、このタスクは各サイトで 1 日に 1 回実行されます。 中央管理サイトとプライマリ サイトでは、このタスクによって 30 日よりも古いデータが削除されます。 セカンダリ サイトで SQL Server Express を使用する場合、このタスクが毎日実行され、7 日間非アクティブだったデータが削除されていることを確認してください。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|**セカンダリ サイト**|Enabled|

### <a name="delete-aged-metering-data"></a>期限切れの使用状況測定データの削除

このタスクは、指定した時間を越えて格納されているソフトウェア使用状況測定の期限切れデータをデータベースから削除する場合に使用します。 詳しくは、「[ソフトウェア使用状況測定](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-metering-summary-data"></a>期限切れの使用状況測定の概要データの削除

このタスクは、指定した時間を越えて格納されているソフトウェア使用状況測定の期限切れの概要データをデータベースから削除する場合に使用します。 詳しくは、「[ソフトウェア使用状況測定](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-notification-server-history"></a>期限切れの通知サーバー履歴の削除

このタスクにより、期限切れクライアントのプレゼンス履歴が削除されます。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-notification-task-history"></a>期限切れの通知タスク履歴の削除

このタスクは、クライアント通知タスクに関する情報をサイト データベースから削除する場合に使用します。 このタスクは、指定した期間に更新されていないデータに適用されます。 詳細については、[クライアント通知](../../clients/manage/client-notification.md)に関するページをご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-passcode-records"></a>期限切れのパスコード レコードの削除

このタスクは、Windows Phone デバイスのパスコードのリセットに関する期限切れデータを削除する場合に、ご利用の階層の最上位サイトで使用します。 パスコードのリセット データは暗号化されますが、デバイスの PIN が含まれます。 既定では、このタスクは有効になっており、1 日以上経過したデータが削除されます。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-replication-data"></a>期限切れのレプリケーション データの削除

このタスクは、Configuration Manager サイト間のデータベース レプリケーションに関する期限切れデータをデータベースから削除する場合に使用します。 このメンテナンス タスクの構成を変更すると、その構成が階層内の適用可能な各サイトに適用されます。 詳細については、「[データベース レプリケーションの監視](monitor-replication.md)」を参照してください。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|**セカンダリ サイト**|Enabled|

### <a name="delete-aged-replication-summary-data"></a>期限切れのレプリケーション概要データの削除

このタスクは、指定した期間更新されなかったレプリケーション概要データを、サイト データベースから削除する場合に使用します。 詳細については、「[データベース レプリケーションの監視](monitor-replication.md)」を参照してください。  

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|**セカンダリ サイト**|Enabled|

### <a name="delete-aged-status-messages"></a>期限切れのステータス メッセージの削除

このタスクは、ステータス フィルター規則で構成されているように期限切れのステータス メッセージ データをデータベースから削除する場合に使用します。 詳細については、「[Configuration Manager のステータス システムの監視](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)」をご覧ください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-threat-data"></a>期限切れの脅威データの削除

このタスクは、指定した時間を越えて格納されている Endpoint Protection の期限切れの脅威データをデータベースから削除する場合に使用します。 詳しくは、「[Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-unknown-computers"></a>期限切れの不明なコンピューターの削除

このタスクは、不明なコンピューターに関する情報が、指定した時間更新されなかったときに、サイト データベースから情報を削除する場合に使用します。 詳細については、「[不明なコンピューターの展開の準備](../../../osd/get-started/prepare-for-unknown-computer-deployments.md)」を参照してください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-aged-user-device-affinity-data"></a>期限切れのユーザーとデバイスのアフィニティ データを削除

このタスクは、期限切れのユーザーとデバイスのアフィニティ データをデータベースから削除する場合に使用します。 詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-duplicate-system-discovery-data"></a>重複するシステムの探索データの削除

このタスクは、システムの探索によって生成された重複するレコードをサイト データベースから削除する場合に使用します。<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|プライマリ サイト|利用不可|
|セカンダリ サイト|利用不可|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>期限切れの MDM 一括登録パッケージのレコードの削除

このタスクを利用し、登録証明書の有効期限切れ後、古い一括登録証明書と対応するプロファイルを削除します。 詳細については、「[証明書プロファイルの作成](../../../protect/deploy-use/create-certificate-profiles.md)」をご覧ください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-inactive-client-discovery-data"></a>非アクティブ クライアントの探索データの削除

このタスクは、非アクティブ クライアントの探索データをデータベースから削除する場合に使用します。 サイトでは、クライアントが不使用としてフラグ付けされたときに、クライアント ステータス用に作成された構成によって、クライアントは非アクティブとしてマークされます。

このタスクは、Configuration Manager クライアントであるリソースでしか動作しません。 期限切れの探索データ レコードをすべて削除する **[期限切れの探索データの削除]** タスクとは異なります。 このタスクを 1 つのサイトで実行すると、階層内のすべてのサイトのデータベースからそのデータが削除されます。 詳細については、「[クライアント ステータスを構成する方法](../../clients/deploy/configure-client-status.md)」を参照してください。

> [!IMPORTANT]  
> 有効にする場合は、 **[定期探索]** のスケジュールよりも長い間隔で実行するようにこのタスクを構成します。 この構成により、アクティブなクライアントは定期探索レコードを送信できるため、そのクライアント レコードがアクティブとしてマークされます。そのため、このタスクによってそれらが削除されることはありません。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|無効|
|セカンダリ サイト|利用不可|

### <a name="delete-obsolete-alerts"></a>不使用のアラートの削除

このタスクは、指定した時間を越えて格納されている期限切れのアラートをデータベースから削除する場合に使用します。 詳細については、「[アラートとステータス システムの使用](use-alerts-and-the-status-system.md)」を参照してください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-obsolete-client-discovery-data"></a>不使用のクライアントの探索データの削除

このタスクは、不使用のクライアント レコードをデータベースから削除する場合に使用します。 通常、不使用とマークされたレコードは、同じクライアントの新しいレコードに置き換えられています。 新しいレコードがクライアントの現在のレコードになります。 探索の詳細については、[探索の実行](../deploy/configure/run-discovery.md)に関するページをご覧ください。

> [!IMPORTANT]  
> 有効にする場合は、[定期探索] のスケジュールよりも長い間隔で実行するようにこのタスクを構成します。 この構成により、不使用かどうかを適切に設定する定期探索レコードをクライアントが送信できます。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|無効|
|セカンダリ サイト|利用不可|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>不使用のフォレスト探索サイトとサブネットの削除

このタスクは、Active Directory サイト、サブネット、およびドメインに関するデータを削除する場合に使用します。 これにより、過去 30 日間に Active Directory フォレスト探索方法でサイトにより探索されなかったデータが削除されます。 このタスクによって探索データが削除されますが、この探索データからご自分で作成した境界には影響しません。 詳細については、「[探索を実行する](../deploy/configure/run-discovery.md)」を参照してください。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="delete-orphaned-client-deployment-state-records"></a>孤立したクライアントの展開状態レコードの削除

このタスクは、クライアントの展開状態に関する情報を含むテーブルを定期的に消去する場合に使用します。 このタスクにより、不使用または使用停止になったデバイスに関連付けられているレコードがクリーンアップされます。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="evaluate-collection-members"></a>コレクションのメンバーの評価

コレクション メンバーシップの評価をサイト コンポーネントとして構成します。 詳しくは、「[サイト コンポーネント](../deploy/configure/site-components.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="monitor-keys"></a>キーの監視

このタスクは、Configuration Manager データベースのプライマリ キーの整合性を監視する場合に使用します。 主キーは、1 つの行を一意に識別する、列または列の組み合わせです。 このキーにより、Microsoft SQL Server データベース テーブル内の他のすべての行からその行を区別することができます。

|||
|---------|---------|
|**中央管理サイト**|Enabled|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="rebuild-indexes"></a>インデックスの再構築

このタスクは、Configuration Manager データベースのインデックスを再構築する場合に使用します。 インデックスとは、データ取得を高速化するためにデータベース テーブル上に作成される、データベース構造のことです。 たとえば、通常、インデックス付きの列の検索は、インデックスが付いていない列の検索よりもかなり速く実行されます。

パフォーマンスを高めるために、Configuration Manager データベースのインデックスは、データベースに格納されている流動的なデータとの同期を保つために、頻繁に更新されます。 次のタスクをスケジュールできます。

- 50% 以上が一意であるデータベースの列に対してインデックスが作成されます
- 一意である割合が 50% 未満の列のインデックスが削除されます
- データの一意性に関する条件を満たす既存のインデックスがすべて再構築されます

|||
|---------|---------|
|**中央管理サイト**|無効|
|**プライマリ サイト**|無効|
|**セカンダリ サイト**|無効|

### <a name="summarize-file-usage-metering-data"></a>ファイルの使用状況測定データの概要

このタスクは、ソフトウェア使用状況測定ファイルの使用状況に対する複数レコードのデータを単一の汎用レコードにまとめる場合に使用します。 データの概要を使用すると、Configuration Manager データベースに格納されるデータ量を圧縮できます。

ソフトウェア使用状況測定データを要約して、データベース内のディスク領域を節約するには、このタスクを **[ソフトウェア使用状況データの月単位の概要]** と共に使用します。 詳しくは、「[ソフトウェア使用状況測定](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="summarize-installed-software-data"></a>インストール済みソフトウェア データの概要

このタスクは、ハードウェア インベントリを通じて収集された資産インテリジェンス ソフトウェア情報からのデータをまとめて、複数のレコードを単一の汎用レコードにマージする場合に使用します。 データの概要を使用すると、Configuration Manager データベースに格納されるデータ量を圧縮できます。 詳細については、「[資産インテリジェンスのメンテナンス タスクの構成](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks)」を参照してください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="summarize-monthly-usage-metering-data"></a>月単位の使用状況測定データの概要

このタスクは、月単位のソフトウェアの使用状況に対する複数レコードのデータを単一の汎用レコードにまとめる場合に使用します。 データの概要を使用すると、Configuration Manager データベースに格納されるデータ量を圧縮できます。

ソフトウェア使用状況測定データを要約して、データベース内の領域を節約するには、このタスクを **[ソフトウェア ファイル使用状況データの概要]** と共に使用します。 詳しくは、「[ソフトウェア使用状況測定](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)」をご覧ください。

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="update-application-available-targeting"></a>アプリケーション対応ターゲット設定の更新

このタスクは、Configuration Manager がコレクション内のリソースへのポリシーとアプリケーションの展開のマッピングを再計算する場合に使用します。 コレクションにポリシーまたはアプリケーションを展開するときに、Configuration Manager により、展開するオブジェクトとコレクション メンバーの間の初期マッピングが作成されます。

これらのマッピングは、クイック リファレンス用のテーブルに格納されます。 コレクション メンバーシップが変更されると、その変更を反映するように、これらの格納されたマッピングがサイトによって更新されます。 ただし、これらのマッピングの同期が取れない可能性があります。たとえば、サイトが通知ファイルを適切に処理できない場合、マッピングに対する変更で、その変更が反映されない可能性があります。 このタスクにより、現在のコレクション メンバーシップに基づいてそのマッピングが更新されます。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|

### <a name="update-application-catalog-tables"></a>アプリケーション カタログ テーブルの更新

このタスクは、アプリケーション カタログ Web サイト データベースのキャッシュを最新のアプリケーション情報と同期する場合に使用します。 このメンテナンス タスクの構成を変更すると、階層内のすべてのプライマリ サイトにそれが適用されます。  

|||
|---------|---------|
|中央管理サイト|利用不可|
|**プライマリ サイト**|Enabled|
|セカンダリ サイト|利用不可|


## <a name="see-also"></a>関連項目

[メンテナンス タスク](maintenance-tasks.md)