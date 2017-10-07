---
title: "在您的 Azure Active Directory aaaManaging 自訂網域名稱 |Microsoft 文件"
description: "管理概念和管理 Azure Active Directory 自訂網域的做法"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>管理 Azure Active Directory 中的自訂網域名稱
網域名稱可以是許多目錄資源的重要識別碼，其屬於：

* 使用者的使用者名稱或電子郵件地址
* hello 位址群組
* hello 應用程式識別碼 URI 的應用程式

Azure Active Directory (Azure AD) 中的資源可以包含已驗證 toobe 所擁有 hello 目錄，其中包含 hello 資源的網域名稱。 只有全域管理員可以在 Azure AD 中執行網域管理工作。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何 toomanage 您的網域名稱在 hello Azure AD 系統管理中心，請參閱[管理您的 Azure Active Directory 中的自訂網域名稱](active-directory-domains-manage-azure-portal.md)。

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>設定您的 Azure AD 目錄的 hello 主要網域名稱
建立您的目錄時，hello 初始網域名稱，例如 'contoso.onmicrosoft.com'，也是 hello 主要網域名稱，為您的目錄。 hello 主要網域是 hello 預設網域名稱用於新的使用者，當您建立新的使用者在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，或其他入口網站，例如 hello Office 365 系統管理入口網站。 這可簡化系統管理員 toocreate 新的使用者在 hello 入口網站中的 hello 程序。

您的目錄的 toochange hello 主要網域名稱：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)的 Azure AD 目錄的全域系統管理員的使用者帳戶。
2. 選取**Active Directory** hello 左側的導覽列上。
3. 開啟您的目錄。
4. 選取 hello**網域** 索引標籤。
5. 選取 hello**變更主要**hello 命令列上的按鈕。
6. 選取您想 toobe hello 新的主要網域，為您的目錄 hello 網域。

您可以變更目錄 toobe 的 hello 主要網域名稱不同盟任何驗證的自訂網域。 變更 hello 主要網域為您的目錄不會變更任何現有使用者的 hello 使用者名稱。

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>新增自訂網域名稱 tooyour Azure AD
您可以加總 too900 自訂網域名稱 tooeach Azure AD 目錄。 太 hello 程序[新增其他自訂網域名稱，](active-directory-add-domain.md) hello 相同的 hello 第一個自訂網域名稱。

## <a name="add-subdomains-of-a-custom-domain"></a>新增自訂網域的子網域
如果您想 tooadd 第三層網域名稱，例如 'europe.contoso.com' tooyour 目錄，您應該先 agregar y comprobar hello 第二層網域，例如 contoso.com。hello 子網域會自動由 Azure AD 驗證。 hello 您剛才加入的子網域的 toosee 已經過驗證，重新整理 hello 頁面，列出您的目錄中的 hello 網域的 hello 瀏覽器中。

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
* [了解 Azure AD 中的網域名稱](active-directory-add-domain-concepts.md)
* [管理自訂網域名稱](active-directory-add-manage-domain-names.md)

