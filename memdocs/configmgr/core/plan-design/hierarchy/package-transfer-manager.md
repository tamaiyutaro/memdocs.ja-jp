---
title: Package Transfer Manager
titleSuffix: Configuration Manager
description: Configuration Manager の Package Transfer Manager がサイト サーバーからリモート配布ポイントにコンテンツを転送する方法を説明します。
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706510"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Configuration Manager の Package Transfer Manager

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager サイトの Package Transfer Manager は、サイト サーバー コンピューターからサイトのリモート配布ポイントへのコンテンツの転送を管理する SMS_Executive サービスのコンポーネントです。 (リモート配布ポイントとは、サイト サーバー コンピューター上にない配布ポイントです)。管理者は Package Transfer Manager を構成できませんが、どのように動作するのかを理解しておくと、コンテンツ管理インフラストラクチャの計画に役立ちます。 また、コンテンツの配布に関する問題の解決にも役立ちます。


サイトの 1 つまたは複数のリモート配布ポイントにコンテンツを配布する場合、**配布マネージャー**が、コンテンツ転送ジョブを作成します。 そして、プライマリ サイト サーバーとセカンダリ サイト サーバー上の Package Transfer Manager に、リモート配布ポイントへコンテンツを転送するよう通知します。

 Package Transfer Manager が、行った処理を **pkgxfermgr.log** ファイルに記録して、サイト サーバーに保存します。 このログ ファイルは、Package Transfer Manager による処理を確認できる唯一の場所です。  

> [!NOTE]  
>  Configuration Manager の旧バージョンでは、配付マネージャーがリモート配付ポイントへのコンテンツの配布を管理します。 配付マネージャーは、サイト間のコンテンツの転送も管理します。 Configuration Manager でも、配布マネージャーは、2 つのサイト間のコンテンツの転送を引き続き管理します。 一方、多数の配布ポイントに対するコンテンツの転送は、Package Transfer Manager によって管理されるようになりました。 したがって、サイト間だけでなく、サイト内の配布ポイントへのコンテンツの展開のパフォーマンスが向上しています。  

標準配付ポイントにコンテンツを転送するとき、Package Transfer Manager は、Configuration Managerの旧バージョンの配付マネージャーと同じように動作します。 つまり、各リモート配付ポイントへのファイルの転送に、Package Transfer Manager 自体が介入します。 しかし、プル配布ポイントにコンテンツを配布するときは、Package Transfer Manager は、コンテンツがあることをプル配布ポイントに知らせるにとどまります。 その転送プロセスはその後、プル配布ポイントが引き継ぎます。  

Package Transfer Manager が標準配布ポイントにコンテンツを転送するときと、プル配布ポイントとして構成されている配布ポイントにコンテンツを転送するときに行われる処理を以下にまとめます。
1.  **管理者がサイトの 1 つまたは複数の配布ポイントにコンテンツを展開する。**  

    -   **標準配布ポイント:** 配付マネージャーが、そのコンテンツの転送ジョブを作成します。  

    -   **プル配布ポイント**:配付マネージャーが、そのコンテンツの転送ジョブを作成します。  

2.  **配布マネージャーが転送前のチェックを行う。**  

    -   **標準配布ポイント:** 配付マネージャーが、各配付ポイントがコンテンツを受け取る準備ができているかどうかをチェックします。 チェックが終わったら、配付マネージャーが Package Transfer Manager に配布ポイントへのコンテンツ転送を開始してもよいことを知らせます。  

    -   **プル配布ポイント:** 配布マネージャーが Package Transfer Manager を起動し、新しいコンテンツ転送ジョブの存在が Package Transfer Manager によって通知されます。 配布マネージャーは、リモートのプル配布ポイントの状態をチェックしません。それぞれのプル配布ポイントが、そのコンテンツの転送を受け持つからです。  

3.  **Package Transfer Manager がコンテンツの転送を準備する。**  

    -   **標準配布ポイント:** Package Transfer Manager が、指定された各リモート配布ポイントのコンテンツの単一インスタンス ストアを調べます。 その目的は、配布ポイントに既にファイルがあるかどうかを判別することにあります。 次に、配付ポイントに存在しないファイルだけの転送処理をキューに並べます。  

        > [!NOTE]  
        >  配布ポイントの単一インスタンス ストアに対象のファイルが既に存在する場合でも、配布対象のすべてのファイルを配布ポイントにコピーするには、コンテンツの **[再配布]** アクションを使用します。  

    -   **プル配布ポイント:** 配布の各プル配布ポイントについて、Package Transfer Manager がプル配布ポイントのソース配布ポイントに利用可能なコンテンツがあるかどうかをチェックします。  

        -   少なくとも 1 つのソース配布ポイントに利用可能なコンテンツがあれば、Package Transfer Manager はそのプル配布ポイントに通知を送信します。 この通知が、コンテンツの転送プロセスを開始するように配布ポイントに指示します。 この指示には、ファイル名とサイズ、属性、ハッシュ値が含まれています。  

        -   ソース配付ポイントにコンテンツがない場合は、Package Transfer Manager は、プル配付ポイントに指示を送信しません。 その代わりに、20 分おきにコンテンツがあるかどうかをチェックします。 コンテンツが見つかったら、該当するプル配付ポイントにコンテンツを転送するように指示します。  

        > [!NOTE]  
        >  プル配布ポイントの単一インスタンス ストアに対象のファイルが既に存在する場合でも、配布対象のすべてのファイルを配布ポイントにコピーするには、コンテンツの **[再配布]** アクションを使用します。  

4.  **コンテンツの転送が開始する。**  

    -   **標準配布ポイント:** Package Transfer Manager が、各リモート配付ポイントにファイルをコピーします。 転送中に次の処理が行われます。  

        -   既定では、Package Transfer Manager は、同時に 3 つのパッケージを処理でき、5 箇所の配付ポイントに並行して配付できます。 これらをまとめて**同時配布の設定**といいます。 同時配布を設定するには、各サイトの **[ソフトウェアの配布コンポーネントのプロパティ]** から **[全般]** タブに移動します。  

        -   Package Transfer Manager は、コンテンツを配布ポイントに転送するときに、その配付ポイントのスケジュールとネットワーク帯域幅の構成に従います。 これらの設定は、各リモート配布ポイントの **[プロパティ]** の **[スケジュール]** タブと **[転送率の制限]** タブで行えます。 詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

    -   **プル配布ポイント:** プル配付ポイントが転送の通知ファイルを受け取ると、コンテンツの転送プロセスを開始します。 転送プロセスは、プル配付ポイントごとに独立して実行されます。  

        1.   プル配付ポイントが、配付するコンテンツのうち、その単一インスタンス ストアに存在しないファイルを識別して、そのソース配付ポイントの 1 つからダウンロードする準備を整えます。  

        2.   プル配付ポイントが、目的のコンテンツがあるかどうか、ソース配付ポイントを順番にチェックしていきます。 目的のコンテンツのあるソース配付ポイントが見つかると、そのコンテンツのダウンロードを開始します。  

        > [!NOTE]  
        >  プル配布ポイントがコンテンツをダウンロードするプロセスは、Configuration Manager クライアントがダウンロードするプロセスと同じです。 プル配布ポイントがコンテンツを転送するときは、同時転送設定は使われません。 同様に、標準配布ポイントに対して行ったスケジューリングと帯域幅調整の設定も使用されません。  

5.  **コンテンツの転送が完了する。**  

    -   **標準配布ポイント:** Package Transfer Manager は、指定されたすべてのリモート配布ポイントにファイルを転送し終わったら、配布ポイントにあるコンテンツのハッシュを検証します。 そして、配布が完了したことを配布マネージャーに通知します。  

    -   **プル配布ポイント:** プル配布ポイントが、コンテンツをダウンロードし終わったら、コンテンツのハッシュを検証します。 そして、正常に完了したことを知らせるステータス メッセージをサイトの管理ポイントに送信します。 60 分が経過してもこのステータスが届かなかった場合、Package Transfer Manager が再度起動します。 プル配布ポイントに問い合わせて、コンテンツがダウンロードされたかどうかが確認されます。 コンテンツのダウンロードが進行中の場合は、Package Transfer Manager は、さらに 60 分後にプル配布ポイントをもう一度確認するまで休止状態に入ります。 この一連の動作が、プル配布ポイントがコンテンツの転送を完了するまで繰り返されます。  