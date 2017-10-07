---
title: "Azure Active Directory 中的 aaaAssign 使用者 tooa 自訂網域 |Microsoft 文件"
description: "如何 toopopulate 自訂網域使用者帳戶與 Azure Active Directory 中。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>指派使用者 tooa 自訂網域
加入您的自訂網域 tooAzure Active Directory 之後，您必須新增 hello 這個網域的使用者帳戶，以便您可以開始驗證它們。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何 toomanage 您的網域名稱在 hello Azure AD 系統管理中心，請參閱[管理您的 Azure Active Directory 中的自訂網域名稱](active-directory-domains-manage-azure-portal.md)。

## <a name="users-synced-from-a-on-premises-directory"></a>從內部部署目錄同步處理的使用者
如果您有已設定連線之間您內部部署 Active Directory 與 Azure Active Directory，同步處理可以填入 hello 帳戶。 如需有關如何 toosynchronize Azure Active Directory 與您的內部部署 Active Directory，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

## <a name="users-added-and-managed-in-hello-cloud"></a>新增和管理 hello 雲端中的使用者
現有的使用者帳戶的 toochange hello 網域：

1. 開啟 hello Azure 傳統入口網站使用的帳戶，是全域管理員或使用者的系統管理員。
2. 開啟您的目錄。
3. 選取 hello**使用者** 索引標籤。
4. Hello 清單中選取 hello 使用者。
5. 變更 hello hello 使用者的網域，然後選取**儲存**。

這還可以使用[Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)或 hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)。

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>在建立新的使用者時選取自訂網域
1. 開啟 hello Azure 傳統入口網站使用的帳戶，是全域管理員或使用者的系統管理員。
2. 開啟您的目錄。
3. 選取 hello**使用者** 索引標籤。
4. Hello 命令列中，選取**新增**。
5. 當您新增 hello 使用者名稱時，請從 hello 網域清單中選擇 hello 自訂網域。
6. 選取 [ **儲存**]。

## <a name="next-steps"></a>後續步驟
* [為您的使用者使用自訂網域名稱 toosimplify hello 登入體驗](active-directory-add-domain.md)
* [管理自訂網域名稱](active-directory-add-manage-domain-names.md)
* [了解 Azure AD 中的網域管理概念](active-directory-add-domain-concepts.md)

