---
title: ソフトウェア センターのユーザー ガイド
titleSuffix: Configuration Manager
description: ソフトウェア センターの機能について説明します
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706810"
---
# <a name="software-center-user-guide"></a>ソフトウェア センターのユーザー ガイド

*適用対象:Configuration Manager (Current Branch)*

組織の IT 管理者はソフトウェア センターを使用して、アプリケーションおよびソフトウェア更新プログラムをインストールして、Windows をアップグレードします。 このユーザー ガイドでは、コンピューターのユーザー用のソフトウェア センターの機能について説明します。

ソフトウェア センターの機能に関する一般的な注意事項: 

- この記事では、ソフトウェア センターの最新機能について説明します。 組織で古いがまだサポートされているバージョンのソフトウェア センターを使用している場合、一部の機能は利用できません。 詳細については、IT 管理者に問い合わせてください。

- IT 管理者は、ソフトウェア センターの一部の機能を無効にする場合があります。 特定のエクスペリエンスは異なる場合があります。

- たとえば、複数のリモート デスクトップ セッションを介して複数のユーザーが同時にデバイスを使用している場合、セッション ID が最も小さいユーザーが、ソフトウェア センターで使用可能なすべての展開を表示できる唯一のユーザーになります。 セッション ID が大きいユーザーには、ソフトウェア センターで展開の一部が表示されない場合があります。 たとえば、セッション ID が大きいユーザーには、展開されたアプリケーションが表示される一方で、展開されたパッケージやタスク シーケンスが表示されない場合があります。 一方、セッション ID が最も小さいユーザーには、展開されたすべてのアプリケーション、パッケージ、およびタスク シーケンスが表示されます。

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> ソフトウェア センターを開く方法

Windows 10 コンピューターでソフトウェア センターを起動する最も簡単な方法は、 **[スタート]** を押して「`Software Center`」と入力することです。 Windows では、最適な一致を見つけるために文字列全体を入力する必要がない場合があります。

[スタート] メニュー内を移動する場合は、**ソフトウェア センター** アイコンの **[Microsoft Endpoint Manager]** グループを確認します。

![[スタート] メニューの Microsoft Endpoint Manager のアイコン](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> [スタート] メニューのパスはバージョン 1910 で変更されました。 バージョン 1906 以前では、フォルダー名は **Microsoft System Center** です。 Configuration Manager をバージョン 1910 以降に更新する場合は、この新しい場所を含むように、保守しているすべての内部ドキュメントを更新してください。

## <a name="applications"></a>アプリケーション

IT 管理者がユーザーまたはこのコンピューターに展開したアプリケーションを見つけてインストールするには、 **[アプリケーション]** タブを選択します。

- **すべて**:インストールできるすべてのアプリケーションが表示されます。
- **必須**:IT 管理者はこれらのアプリケーションを強制します。 これらのアプリケーションのいずれかをアンインストールすると、ソフトウェア センターで再インストールされます。
- **フィルター**:IT 管理者はアプリケーションのカテゴリを作成する場合があります。 使用可能な場合は、ドロップダウン リストを選択して、特定のカテゴリのアプリケーションのみを表示するようにビューをフィルター処理します。 **[すべて]** を選択して、すべてのアプリケーションを選択します。
- **並べ替える**:アプリケーションのリストを並べ替えます。 既定では、このリストは**新しい順**に並べ替えられます。 最近使用可能になったアプリケーションは **[新規]** タグと共に一覧表示されます。これは 7 日間表示されます。
- **検索**:探しているものがまだ見つからない場合は、 検索ボックスにキーワードを入力して見つけます。
- **ビューを切り替える**:リスト ビューとタイル ビューを切り替えるには、アイコンを選択します。 既定では、アプリケーション リストはグラフィック タイルとして表示されます。
    - タイル ビュー:IT 管理者はアイコンをカスタマイズできます。 各タイルの下に、アプリケーションの名前、発行元、バージョンが表示されます。
    - リスト ビュー:このビューには、アプリケーションのアイコン、名前、発行元、バージョン、および状態が表示されます。

### <a name="install-multiple-applications"></a>複数のアプリケーションをインストールする

<!-- 1357126 -->
1 つのインストールが完了するのを待ってから次のインストールを開始するのではなく、一度に複数のアプリケーションをインストールします。 以下はすべてのアプリケーションに当てはまるわけではありません。

- アプリがユーザーに表示される
- アプリがまだダウンロードまたはインストールされていない
- IT 管理者はアプリをインストールする承認を必要としない

一度に複数のアプリケーションをインストールするには、次の操作を行います。

1. リスト ビューで複数選択モードに入るには、右上隅にある複数選択アイコン  ![ソフトウェア センターの複数選択アイコン ](media/software-center-multi-select-apps.png) をクリックします。
2. リストのアプリの左側にあるチェック ボックスをオンにして、インストールする 2 つ以上のアプリを選択します。
3. **[選択項目のインストール]** ボタンを選択します。

これで、アプリは通常どおり、連続してインストールされます。


## <a name="updates"></a>更新プログラム

IT 管理者がこのコンピューターに展開したソフトウェア更新プログラムを表示してインストールするには、 **[更新プログラム]** タブを選択します。  

- **すべて**:インストールできるすべての更新プログラムが表示されます。
- **必須**:IT 管理者はこれらの更新プログラムを強制します。
- **並べ替える**:更新プログラムのリストを並べ替えます。 既定では、このリストは**アプリケーション名:A から Z** で並べ替えられます。

更新プログラムをインストールするには、 **[すべてインストール]** を選択します。

特定の更新プログラムのみをインストールするには、アイコンを選択して複数選択モードに入ります。 インストールする更新プログラムを確認して、 **[選択項目のインストール]** を選択します。


## <a name="operating-systems"></a>オペレーティング システム

**[オペレーティング システム]** タブを選択して、IT 管理者がこのコンピューターに展開した Windows のバージョンを表示してインストールします。  

- **すべて**:インストールできるすべての Windows のバージョンが表示されます。
- **必須**:IT 管理者はこれらのアップグレードを強制します。
- **並べ替える**:更新プログラムのリストを並べ替えます。 既定では、このリストは**アプリケーション名:A から Z** で並べ替えられます。


## <a name="installation-status"></a>インストールのステータス

アプリケーションの状態を表示するには、 **[インストールのステータス]** タブを選択します。 次の状態が表示される場合があります。

- **インストール済み**:ソフトウェア センターで、このコンピューターにこのアプリケーションが既にインストールされています。
- **ダウンロード中**:ソフトウェア センターで、コンピューターにインストールするソフトウェアがダウンロードされています。
- **失敗**:ソフトウェア センターで、ソフトウェアのインストールの試行中にエラーが発生しました。
- **次の日時後にインストールするようにスケジュール済み**:デバイスに近日公開されているソフトウェアがインストールされる次のメンテナンス期間の日時が示されます。 IT 管理者がメンテナンス期間を定義します。<!--1358131-->
    - 状態は、 **[すべて]** と **[近日公開]** タブで確認できます。
    - **[今すぐインストール]** ボタンを選択することで、メンテナンス期間になる前にインストールできます。


## <a name="device-compliance"></a>デバイスのポリシー準拠

このコンピューターのポリシー準拠状態を表示するには、 **[デバイスのポリシー準拠]** タブを選択します。

IT 管理者によって定義されたセキュリティ ポリシーに対してこのデバイスの設定を評価するには、 **[ポリシー準拠状況の確認]** を選択します。


## <a name="options"></a>オプション

このコンピューターの追加設定を表示するには、 **[オプション]** タブを選択します。

### <a name="work-information"></a>勤務時間の情報

通常の勤務時間を示します。 IT 管理者は、勤務時間外にソフトウェアのインストールをスケジュールする場合があります。 システム メンテナンス タスクに、1 日少なくとも 4 時間は確保できるようにしてください。 IT 管理者は、勤務時間中でも重要なアプリケーションおよびソフトウェア更新プログラムをインストールできます。

- ドロップダウン リストを選択して、このコンピューターを使用する最も早い時刻と最も遅い時刻を選択します。 既定では、これらの値は**午前 5 時**から**午後 10 時**までとなります。

- 通常、このコンピューターを使用する曜日の横にあるチェック ボックスをオンにします。 既定では、ソフトウェア センターでは平日のみが選択されます。  

このコンピューターを日常的に使って仕事をするかどうかを指定します。 管理者が自動的にアプリケーションをインストールしたり、追加のアプリケーションをプライマリ コンピューターで利用できるようにしたりすることがあります。 <!--3485366-->

- 使用しているコンピューターがプライマリ コンピューターの場合は、 **[このコンピューターを日常の仕事で使用します]** を選択します。

### <a name="power-management"></a>電源管理

IT 管理者は電源管理ポリシーを設定する場合があります。 これらのポリシーは、組織でこのコンピューターが使用されていないときに節電するのに役立ちます。

このコンピューターをこれらのポリシーから除外するには、 **[このコンピューターに IT 部門の電源管理設定を適用しない]** チェック ボックスをオンにします。 この設定は既定では無効になり、コンピューターに電源管理設定が適用されます。

### <a name="computer-maintenance"></a>コンピューターのメンテナンス

期限までにソフトウェア センターでソフトウェアの変更をどのように適用するかを指定します。

- **必要なソフトウェアを自動的にインストールまたはアンインストールし、指定した勤務時間外にのみコンピューターを再起動する**:この設定は既定で無効になっています。
- **コンピューターがプレゼンテーション モードのときはソフトウェア センターを停止する**:既定では、この設定は有効になっています。
- **同期ポリシー**: IT 管理者に指示された場合は、このボタンを選択します。このコンピューターは、サーバーを調べ、新しいアプリケーション、ソフトウェア更新プログラム、オペレーティング システムなどがないか確認します。

### <a name="remote-control"></a>リモート コントロール

コンピューターのリモート アクセスとリモート コントロールの設定を指定します。

- **[Use remote access settings from your IT Department]\(IT 部門のリモート アクセス設定を使用する\)** :既定では、このチェック ボックスはオンになっています。
- **[許可するリモート アクセスのレベル]** :次の 3 つのオプションから選択します。
    - **[Do not allow remote access]\(リモートアクセスを許可しない\)**
    - **[表示のみ]**
    - **[完全]** : 既定では、このレベルが有効になっています。
- **[Allow remote control of this computer by administrators when I am away]\(離席時に管理者がこのコンピューターをリモート コントロールするのを許可する\)** 。 既定では、この設定は **[いいえ]** に設定されます。
- **[When an administrator tries to control this computer remotely]\(管理者がこのコンピューターをリモート コントロールしようとした場合\)** :この設定には 2 つのオプションがあります。
    - **Ask for permission each time\(毎回アクセス許可を要求する\)** :既定では、このオプションはオンです。
    - **[Do not ask for permission]\(アクセス許可を要求しない\)**
- **[Show the following during remote control]\(リモート コントロール時に以下を表示する\)** :既定では、両方のオプションがオンになっています。
    - **[Status icon in the notification area]\(通知領域内の状態アイコン\)**
    - **[A session connection bar on the desktop]\(デスクトップ上のセッション接続バー\)**
- **[音で通知する]** :この設定には 3 つのオプションがあります。
    - **[セッションの開始時と終了時に音で通知する]** :既定では、この設定はオンになっています。
    - **セッションの実行中に繰り返し鳴らす**
    - **しない**

    詳細については、「[リモート コントロールの概要](../clients/manage/remote-control/introduction-to-remote-control.md)」をご覧ください。
    

## <a name="custom-tab-in-software-center"></a>ソフトウェア センターのカスタム タブ

IT 管理者が、ソフトウェア センターに新しいタブを追加していることがあります。 このタブの名前と、このタブで表示される Web サイトは、管理者によって指定されています。 たとえば、組織のヘルプ デスク Web サイトが表示される "ヘルプ デスク" タブなどです。 <!--1358132-->
