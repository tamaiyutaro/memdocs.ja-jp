---
title: Intune へのデバイスの登録で多要素認証を要求する
titleSuffix: Microsoft Intune
description: Intune へのデバイス登録で Azure AD の多要素認証を要求する方法。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9
ROBOTS: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2b645b41a721063ddfea6019d726a3c232c8dd78
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327024"
---
# <a name="require-multi-factor-authentication-for-intune-device-enrollments"></a>Intune へのデバイスの登録で多要素認証を要求する

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune では、デバイス登録に Azure Active Directory (AD) 多要素認証 (MFA) 機能を利用し、会社のリソースを守ります。

MFA は、次の確認方法のうち 2 つ以上を必須にすることで機能します。

- ユーザーが知っている情報 (通常はパスワードまたは PIN)。
- ユーザーの所持品 (電話など、容易には複製できない、信頼済みのデバイス)。
- ユーザー自身 (指紋など、生体認証)

MFA は、iOS/iPadOS、Android、Windows 8.1 以上、Windows Phone 8.1、または Windows 10 Mobile 以上のデバイスでサポートされています。

MFA を有効にするには、エンド ユーザーは 2 種類の資格情報を提供し、デバイスを登録する必要があります。

## <a name="configure-intune-to-require-multi-factor-authentication-at-device-enrollment"></a>デバイス登録時に多要素認証を要求するように Intune を構成する

デバイスの登録時に MFA を要求するには、次の手順に従います。

>[!Important]
>このポリシーを実装するには、ユーザーに Azure Active Directory Premium P1 以上が割り当てられている必要があります。

>[!Important]
>Microsoft Intune 登録には、**デバイス ベースのアクセス規則**を構成しないでください。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) にサインインして、 **[デバイス]**  >  **[条件付きアクセス]** を選択します。 *Intune* からアクセスされる条件付きアクセス ノードは、*Azure AD* からアクセスされるノードと同じです。
2. **[新しいポリシー]** を選びます。
3. **[新しいポリシー]** で、ポリシーのわかりやすい名前を入力します。
4. **[割り当て]** セクションで、 **[ユーザーとグループ]** を選択します。 
5. **[ユーザーとグループ]** で **[ユーザーまたはグループの選択]** を選択し、 **[ユーザーとグループ]** をオンにします。 このポリシーを受けるユーザーやグループを選択し、 **[完了]** を選択します。
6. **[割り当て]** セクションで、 **[クラウド アプリ]** を選択します。
7. **[クラウド アプリ]** の **[挿入]** タブで、 **[アプリを選択]** を選択し、 **[選択]**  >  **[Microsoft Intune Enrollment]\(Microsoft Intune 登録\)** の順に選択し、 **[完了]** を選択します。 **[Microsoft Intune Enrollment]\(Microsoft Intune 登録\)** を選択すると、条件付きアクセス MFA はデバイスの登録にのみ適用されます (1 回限りの MFA プロンプト)。
8. **[割り当て]** セクションの **[条件]** では、MFA 設定を構成する必要はありません。
9. **[アクセス制御]** セクションで、 **[許可]** を選択します。
10. **[許可]** で、 **[アクセス権の付与]** を選択し、 **[多要素認証を要求する]** を選択します。 **[デバイスは準拠としてマーク済みである必要があります]** は選択しないでください。登録されるまで、デバイスの準拠状態は評価できません。 次に **[選択]** を選択します。
11. **[新しいポリシー]** で、 **[ポリシーを有効にする]**  >  **[オン]** の順に選択し、 **[作成]** を選択します。



## <a name="next-steps"></a>次のステップ

エンド ユーザーがデバイスを登録するとき、PIN、スマートフォン、生体認証など、2 つ目の識別形態で認証する必要があります。
