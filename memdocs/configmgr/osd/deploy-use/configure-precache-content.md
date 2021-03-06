---
title: コンテンツの事前キャッシュを構成する
titleSuffix: Configuration Manager
description: ユーザーがタスク シーケンスをインストールする前に、クライアントが OS の展開コンテンツをダウンロードする方法について学習します。
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 184bdc58ac6dc0e311875cc1ddab8c605d8eec32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704210"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>タスク シーケンス用のコンテンツの事前キャッシュを構成する

*適用対象:Configuration Manager (Current Branch)*

<!--1021244-->
タスク シーケンスの利用可能な展開に事前キャッシュ機能を使用すると、ユーザーがタスク シーケンスをインストールする前に、関連するコンテンツをクライアントにダウンロードさせることができます。 クライアントは、[OS をアップグレード](create-a-task-sequence-to-upgrade-an-operating-system.md)したり、[OS イメージをインストール](create-a-task-sequence-to-install-an-operating-system.md)したりするタスク シーケンス用にコンテンツを事前キャッシュすることができます。

> [!Note]  
> バージョン 1910 では、この機能は Configuration Manager で既定で有効となっています。 バージョン 1906 以前の場合、このオプション機能は Configuration Manager で既定で無効となっています。 この機能は、使用する前に有効にする必要があります。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。<!--505213-->  

たとえば、すべてのユーザーに対して、1 つのインプレース アップグレード タスク シーケンスのみを作成して、多くのアーキテクチャと言語を使用できます。 以前のバージョンでは、ユーザーがソフトウェア センターから利用可能なタスク シーケンスの展開をインストールするときに、コンテンツのダウンロードが開始されます。 この遅延のため、インストールできる状態になるまでさらに時間がかかります。 タスク シーケンスで参照されているすべてのコンテンツがダウンロードされます。 このコンテンツには、すべての言語とアーキテクチャ用の OS アップグレード パッケージが含まれます。 各アップグレード パッケージのサイズが約 3 GB の場合、コンテンツ全体が非常に大きくなります。

事前キャッシュ コンテンツにより、クライアントでは展開を受け取ったらすぐに適用可能なコンテンツと他のすべての参照コンテンツだけをダウンロードすることができます。 ユーザーがソフトウェア センターで **[インストール]** をクリックすると、コンテンツの準備が完了します。 コンテンツがローカルのハード ドライブ上にあるため、インストールはすぐに開始します。

Configuration Manager バージョン 1902 以前では、この動作は "*OS アップグレード パッケージ*" にのみ適用されます。 そのパッケージは、対応するアーキテクチャまたは言語を指定する唯一のコンテンツです。 たとえば、タスク シーケンスが複数のドライバー パッケージも参照する場合、クライアントによってそれらすべてがダウンロードされます。 タスク シーケンス エンジンは、事前にではなく、タスク シーケンスを実行する際に条件を評価します。 クライアントは、パッケージのプロパティのタグを使って、事前にキャッシュに入れる対象のコンテンツを判断します。

バージョン 1906 以降では、<!--4224642--> 事前キャッシュを使用し、以下のコンテンツの種類による帯域幅使用を減らすことができます。

- OS アップグレード パッケージ
- OS イメージ
- ドライバー パッケージ
- パッケージ

## <a name="configure-pre-caching"></a>事前キャッシュを構成する

事前キャッシュ機能を構成するには、次の 3 つの手順があります。

1. [パッケージを作成して構成する](#bkmk_createpkg)
2. [条件付きステップを含むタスク シーケンスを作成する](#bkmk_createts)
3. [タスク シーケンスを展開し、事前キャッシュを有効にする](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a> 1. パッケージを作成して構成する

クライアントは、パッケージの属性を評価して、事前キャッシュ中にダウンロードするコンテンツを決定します。  

#### <a name="os-upgrade-package"></a>OS アップグレード パッケージ

特定のアーキテクチャおよび言語に対応した [OS アップグレード パッケージ](../get-started/manage-operating-system-upgrade-packages.md)を作成します。 プロパティの **[データ ソース]** タブで **[アーキテクチャ]** と **[言語]** を指定します。

#### <a name="os-image"></a>OS イメージ

特定のアーキテクチャと言語の [OS イメージ](../get-started/manage-operating-system-images.md)を作成します。 プロパティの **[データ ソース]** タブで **[アーキテクチャ]** と **[言語]** を指定します。

#### <a name="driver-package"></a>ドライバー パッケージ

特定のハードウェア モデルの[ドライバー パッケージ](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages)を作成します。 そのプロパティの **[全般]** タブで **[モデル]** を指定します。

事前キャッシュ中にダウンロードするドライバー パッケージを決定する目的で、クライアントでは、**Win32_ComputerSystemProduct** WMI クラスの **Name** プロパティに対してモデルが評価されます。

> [!TIP]
> 実際のクエリでは、ワイルドカードと共に `LIKE` ステートメントを使用します: `select * from win32_computersystemproduct where name like "%yourstring%"`。 たとえば、モデルとして `Surface` を指定した場合、クエリはその文字列を含むすべてのモデルに一致します。<!-- 6315551 -->

#### <a name="package"></a>パッケージ

特定のアーキテクチャと言語の[パッケージ](../../apps/deploy-use/packages-and-programs.md)を作成します。 プロパティの **[全般]** タブで **[アーキテクチャ]** と **[言語]** を指定します。


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a> 2.タスクシーケンスの作成

さまざまな言語やアーキテクチャに対して条件付きステップを含む、またはドライバー パッケージ用のさまざまなハードウェア モデルを含むタスク シーケンスを作成します。

|Content|手順|
|---------|---------|
|OS アップグレード パッケージ|[OS をアップグレードする](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|OS イメージ|[OS イメージの適用](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|ドライバー パッケージ|[ドライバー パッケージの適用](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|パッケージ|[パッケージのインストール](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

たとえば、次の **OS のアップグレード** ステップでは、英語版が使用されています。  

![ENU、DEU、JPN の複数の OS アップグレード ステップを示すタスク シーケンス エディター](../media/precacheproperties2.png)

![ロケールおよび OSArchitecture の WMI WQL クエリを表示しているタスク シーケンス エディターの [オプション] タブ](../media/precacheoptions2.png)  

> [!Tip]
> 英語 (米国) OS と 64 ビット アーキテクチャでは、次の WMI クエリをお勧めします。
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> まず、**オペレーティング システムの言語**条件を選択して、言語を追加します。 次に、WMI クエリを編集して、アーキテクチャ句を含めます。


### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a> 3.タスク シーケンスの展開

[タスク シーケンスを展開します](deploy-a-task-sequence.md)。 事前キャッシュの機能については、次の設定を構成します。  

- **[全般]** タブで、 **[このタスク シーケンス用のコンテンツを事前にダウンロードする]** を選択します。  

- **[デプロイ設定]** タブで、タスク シーケンスを **[利用可能]** として構成します。  

- **[スケジュール]** タブで、設定 **[この展開が使用可能になる日時を指定する]** について現在選択されている時間を選択します。 クライアントは、展開の利用可能な時間にコンテンツの事前キャッシュを開始します。 対象となるクライアントがこのポリシーを受け取ると、利用可能な時間が過去の時間となるため、すぐにダウンロードの事前キャッシュが開始されます。 クライアントがこのポリシーを受け取っても、利用可能な時間が未来の時間である場合、クライアントは利用可能な時間になるまでコンテンツの事前キャッシュを開始しません。  

- **[配布ポイント]** タブで、 **[展開オプション]** 設定を構成します。 ユーザーがインストールを開始する前にコンテンツを事前キャッシュしない場合は、クライアントはこれらの設定を使用します。  

    > [!Important]  
    > OS イメージをインストールするタスク シーケンスの場合は、**実行中のタスク シーケンスによって必要になったときにコンテンツをローカルにダウンロード**する展開オプションを使用しないでください。 OS イメージを適用する前に、タスク シーケンスによってディスクがワイプされると、クライアント キャッシュが削除されます。 コンテンツが失われるため、タスク シーケンスは失敗します。<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>ユーザー側の表示と操作

- クライアントが、展開ポリシーを受け取ると、展開の利用可能な時間後にコンテンツの事前キャッシュを開始します。 このコンテンツには、すべての参照先のパッケージが含まれていますが、パッケージのアーキテクチャと言語の属性と一致する OS アップグレード パッケージのみです。  

- クライアントでユーザーが展開を利用できるようになったときに、ユーザーに新しい展開について知らせる通知が表示されます。 これで、タスク シーケンスはソフトウェア センターで表示されます。 ユーザーはソフトウェア センターに移動し、 **[インストール]** をクリックしてインストールを開始します。  

- ユーザーがタスク シーケンスをインストールするときにコンテンツが完全に事前キャッシュされなかった場合、クライアントは、展開の **[デプロイ オプション]** タブで指定された設定を使用します。  


## <a name="see-also"></a>関連項目

- [OS をアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Windows を最新バージョンにアップグレードするシナリオ](upgrade-windows-to-the-latest-version.md)
