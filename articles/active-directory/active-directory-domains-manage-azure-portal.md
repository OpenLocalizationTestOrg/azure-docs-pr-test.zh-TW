---
title: "在您的 Azure Active Directory aaaManaging 自訂網域名稱 |Microsoft 文件"
description: "Azure Active Directory 中管理網域的管理概念和做法"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>管理 Azure Active Directory 中的自訂網域名稱
網域名稱是 hello 許多目錄資源的識別項很重要的一部分： 它屬於使用者時，為群組，請 hello 位址部分的使用者名稱或電子郵件地址，而且可以是應用程式的 hello 應用程式識別碼 URI 的一部分。 Azure Active Directory (Azure AD) 中的資源可以包含已擁有 hello 目錄，其中包含 hello 資源驗證的網域名稱。 只有全域管理員可以在 Azure AD 中執行網域管理工作。

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>設定您的 Azure AD 目錄的 hello 主要網域名稱
建立您的目錄時，hello 初始網域名稱，例如 'contoso.onmicrosoft.com'，也是 hello 主要網域名稱。 hello 主要網域時建立新的使用者之新使用者的 hello 預設網域名稱。 設定主要網域名稱，來簡化管理員 toocreate 新使用者 hello 入口網站中的 hello 程序。 toochange hello 主要網域名稱：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。
2. 選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. 在 hello***目錄名稱***刀鋒視窗中，選取**網域名稱**。
4. 在 hello ***目錄名稱*-網域名稱**刀鋒視窗中，選取 hello 希望 toomake hello 主要網域名稱的網域名稱。
5. 在 hello***網域名稱***刀鋒視窗 （也就是 hello 刀鋒視窗中開啟 hello 標題中具有新的網域名稱），選取 hello**設為主要**命令。 出現提示時，請確認您的選擇。
   
   ![將網域名稱設為主要網域名稱](./media/active-directory-domains-manage-azure-portal/make-primary.png)

您可以變更目錄 toobe 的 hello 主要網域名稱不同盟任何驗證的自訂網域。 變更 hello 主要網域為您的目錄不會變更任何現有使用者的 hello 使用者名稱。

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>新增自訂網域名稱 tooyour Azure AD
您可以加總 too900 自訂網域名稱 tooeach Azure AD 目錄。 太 hello 程序[新增其他自訂網域名稱，](add-custom-domain.md) hello 相同的 hello 第一個自訂網域名稱。

## <a name="add-subdomains-of-a-custom-domain"></a>新增自訂網域的子網域
如果您想 tooadd 第三層網域名稱，例如 'europe.contoso.com' tooyour 目錄，您應該先 agregar y comprobar hello 第二層網域，例如 contoso.com。hello 子網域會自動由 Azure AD 驗證。 hello 您剛才加入的子網域的 toosee 已經過驗證，重新整理 hello 頁面列出 hello 網域的 hello 瀏覽器中。

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>如果您變更您的自訂網域名稱 hello DNS 註冊機構哪些 toodo
如果您變更 hello DNS 註冊機構的自訂網域名稱時，您可以繼續 toouse 與 Azure AD 本身而不需要中斷以及其他設定工作的自訂網域名稱。 如果您使用自訂網域名稱搭配 Office 365、 Intune 或依賴 Azure AD 中的自訂網域名稱的其他服務，請參閱 toohello 文件，這些服務。

## <a name="delete-a-custom-domain-name"></a>刪除自訂網域名稱
如果您的組織不再使用該網域名稱，或如果您需要 toouse 網域名稱與另一個 Azure AD，您可以從您的 Azure AD 刪除自訂網域名稱。

toodelete 自訂網域名稱，您必須先確定您的目錄中沒有任何資源依賴 hello 網域名稱。 如果有下列情況，即無法刪除目錄的網域名稱：

* 任何使用者具有使用者名稱、 電子郵件地址或包含 hello 網域名稱的 proxy 位址。
* 任何群組具有電子郵件地址或包含 hello 網域名稱的 proxy 位址。
* 在您的 Azure AD 中的任何應用程式擁有的應用程式識別碼 URI，包括 hello 網域名稱。

您必須變更或刪除您的 Azure AD 目錄中的任何這類資源，才能刪除 hello 自訂網域名稱。

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>使用 PowerShell 或 Graph API toomanage 網域名稱
在 Azure Active Directory 中，大部分的網域名稱管理工作也都可以使用 Microsoft PowerShell 來完成，或使用 Azure AD 圖形 API 以程式設計方式來完成。

* [在 Azure AD 中使用 PowerShell toomanage 網域名稱](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [在 Azure AD 中使用 Graph API toomanage 網域名稱](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>後續步驟
* [新增自訂網域名稱](add-custom-domain.md)

