---
title: Microsoft Intune のネットワーク エンドポイント
titleSuffix: ''
description: Intune のエンドポイントを確認します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86c90d8313cd9eed853ad438a5ea9a31f0d834ce
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81725544"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Microsoft Intune のネットワーク エンドポイント  

このページには、Intune のデプロイでのプロキシ設定に必要な IP アドレスとポートの設定がリストされています。

クラウド専用のサービスとして、Intune ではサーバーやゲートウェイなど、オンプレミスのインフラストラクチャは必要ありません。

## <a name="access-for-managed-devices"></a>マネージド デバイスへのアクセス  

ファイアウォールとプロキシ サーバーの背後にあるデバイスを管理するには、Intune に対する通信を有効にする必要があります。

> [!NOTE]
> セクションの情報は、Microsoft Intune Certificate Connector にも適用されます。 このコネクタのネットワーク要件は、マネージド デバイスと同じです

- プロキシ サーバーでは **HTTP (80)** と **HTTPS (443)** の両方をサポートする必要があります。これは、Intune クライアントで両方のプロトコルが使用されるためです。 Windows Information Protection ではポート 444 が使用されます。
- Intune では、一部のタスク (従来の PC エージェント用のソフトウェア更新プログラムのダウンロードなど) で、manage.microsoft.com への認証されていないプロキシ サーバー アクセスが必要です

個々のクライアント コンピューターでプロキシ サーバーの設定を変更できます。 また、グループ ポリシーの設定を使用して、指定したプロキシ サーバーの背後にあるすべてのクライアント コンピューターの設定を変更することもできます。


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

マネージド デバイスは、 **[すべてのユーザー]** がファイアウォール経由でサービスにアクセスできるように構成する必要があります。


次の表は、Intune クライアントがアクセスするポートとサービスの一覧です。

|ドメイン    |IP アドレス      |
|-----------|----------------|
|login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net| 詳細については、「[Office 365 URL および IP アドレス範囲](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」を参照してください。 |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com <br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com <br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com <br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com <br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com <br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com <br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com <br>portal.fei.amsua0202.manage.microsoft.com <br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com <br>m.fei.amsua0402.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com <br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com <br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com <br>portal.fei.msub02.manage.microsoft.com <br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com <br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com <br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com <br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com <br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua05.manage.microsoft.com|138.91.244.151|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msua07.manage.microsoft.com|52.175.208.218|
|fef.msub01.manage.microsoft.com|137.135.128.214|
|fef.msub02.manage.microsoft.com|137.135.130.29|
|fef.msub03.manage.microsoft.com|52.169.82.238|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc01.manage.microsoft.com|52.230.19.86|
|fef.msuc02.manage.microsoft.com|23.98.66.118|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.msuc05.manage.microsoft.com|52.230.16.180|
|fef.amsua0202.manage.microsoft.com|52.165.165.17|
|fef.amsua0402.manage.microsoft.com|40.69.157.122|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|fef.amsub0102.manage.microsoft.com|40.118.98.207|
|fef.amsub0202.manage.microsoft.com|40.69.208.122|
|fef.amsub0302.manage.microsoft.com|13.74.145.65|
|enterpriseregistration.windows.net|52.175.211.189|
|fef.amsua0102.manage.microsoft.com|52.242.211.0|
|fef.amsua0702.manage.microsoft.com|52.232.225.75|
|fef.amsub0502.manage.microsoft.com|40.67.219.144|
|fef.msud01.manage.microsoft.com|20.40.178.139|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>PowerShell スクリプトと Win32 アプリのネットワーク要件  

Intune を使用して PowerShell スクリプトまたは Win32 アプリをデプロイする場合は、テナントが現在存在するエンドポイントへのアクセスを許可する必要もあります。

|ASU | ストレージ名 | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows プッシュ通知サービス (WNS)  

モバイル デバイス管理 (MDM) を使用して管理されている Intune の管理対象 Windows デバイスの場合、デバイス アクションとその他の即時アクティビティでは Windows プッシュ通知サービス (WNS) の使用が必要です。 詳細については、「[エンタープライズ ファイアウォールを介した Windows 通知トラフィックの許可](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config)」を参照してください。  

## <a name="delivery-optimization-port-requirements"></a>配信の最適化でのポートの要件  

### <a name="port-requirements"></a>ポートの要件  

ピア ツー ピア トラフィックの場合、配信の最適化では TCP/IP で 7680 または NAT トラバーサル (必要に応じて、Teredo) で 3544 を使用します。 クライアント サービス通信では、ポート 80/443 経由で HTTP または HTTPS を使用します。

### <a name="proxy-requirements"></a>プロキシの要件  

配信の最適化を使用するには、バイト範囲要求を許可する必要があります。 詳細については、[Windows 更新プログラムのプロキシ要件](https://docs.microsoft.com/windows/deployment/update/windows-update-troubleshooting)に関するページを参照してください。

### <a name="firewall-requirements"></a>ファイアウォールの要件  

配信の最適化をサポートするには、以下のホスト名がファイアウォールを通過できるようにします。
クライアントと配信の最適化クラウド サービス間の通信の場合:
- \*.do.dsp.mp.microsoft.com

配信の最適化のメタデータの場合:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Apple デバイス ネットワークの情報  

|使用目的|ホスト名 (IP アドレス/サブネット)|プロトコル|ポート|
|-----|--------|------|-------|
|Apple サーバーからコンテンツを取得して表示する|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|APNS サーバーとの通信|#-courier.push.apple.com<br>'#' は、0 から 50 の乱数です。|    TCP     |  5223 および 443  |
|World Wide Web、iTunes Store、macOS アプリ ストア、iCloud、メッセージングなどへのアクセスを含む、さまざまな機能 |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 または 443   |

詳細については、Apple の「[Apple ソフトウェア製品で使われている TCP および UDP ポート](https://support.apple.com/HT202944)」、[macOS、iOS/iPadOS、iTunes のサーバホスト接続と iTunes のバックグラウンドプロセス](https://support.apple.com/HT201999)に関するページ、[macOS、iOS/iPadOS クライアントで Apple プッシュ通知が届かない場合](https://support.apple.com/HT203609)に関するページを参照してください。  