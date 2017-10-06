---
title: "Azure Active Directory 中的自訂網域名稱的 aaaConceptual 概觀 |Microsoft 文件"
description: "說明 hello 概念性的架構，在 Azure Active directory 中，包括同盟單一登入使用自訂網域名稱"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Azure Active Directory 中的自訂網域名稱的概念式概觀
網域名稱可以是許多目錄資源的重要識別碼，其屬於：

* 使用者的使用者名稱或電子郵件地址
* hello 位址群組
* hello 應用程式識別碼 URI 的應用程式

Azure Active Directory (Azure AD) 中的資源可以包含已驗證 toobe 所擁有 hello 目錄，其中包含 hello 資源的網域名稱。 只有全域管理員可以在 Azure AD 中執行網域管理工作。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何 toomanage 您的網域名稱在 hello Azure AD 系統管理中心，請參閱[管理您的 Azure Active Directory 中的自訂網域名稱](active-directory-domains-manage-azure-portal.md)。

Azure AD 中的網域名稱是全域唯一的。 自訂網域名稱一次只能由一個 Azure AD 租用戶使用。 如果某個 Azure AD 目錄已驗證網域名稱，則其他 Azure AD 目錄就不能驗證或使用該相同的網域名稱。

## <a name="initial-and-custom-domain-names"></a>初始和自訂的網域名稱
Azure AD 中的每個網域名稱不是初始網域名稱就是自訂網域名稱。

每個 Azure AD 會隨附在 hello 表單 contoso.onmicrosoft.com 的初始網域名稱。此第三個層級的網域名稱，在此範例中"contoso.onmicrosoft.com，"已建立 hello 目錄建立時，通常由 hello 目錄的建立者 hello 系統管理員。 無法變更或刪除目錄的 hello 初始網域名稱。 hello 初始網域名稱，而完整的功能，被為了您主要是做為啟動載入的機制，直到自訂網域名稱的 toobe 驗證。

在大部分的生產環境中，目錄具有至少一個已驗證自訂網域，例如"contoso.com"，而且是可見的 tooend 使用者該自訂網域。 自訂網域名稱是由該組織所擁有和使用的網域名稱，例如 "contoso.com"，其用於裝載其網站。 此網域名稱是熟悉 tooemployees，因為它是 hello 他們使用 toosign toohello 公司網路或 toosend 中的，並擷取電子郵件使用者名稱的一部分。

Azure AD 可以使用它之前，請 hello 自訂網域名稱必須加入的 tooyour 目錄，並驗證。

## <a name="verified-and-unverified-domain-names"></a>已驗證和未驗證的網域名稱
Azure AD 驗證，會隱含地評估 hello 初始網域名稱的目錄。 當系統管理員新增自訂網域名稱 tooan Azure AD 時，它處於一開始未驗證的狀態。 Azure AD 不會允許任何目錄資源 toouse 未經驗證的網域名稱。 這會確保只有一個目錄可以使用為特定網域名稱，而且實際上 hello 的組織使用 hello 網域名稱擁有該網域名稱。

Azure AD 驗證網域名稱擁有的權的方式是尋找特定的項目 hello 網域名稱服務 (DNS) 區域檔案中的 hello 網域名稱。 tooverify 擁有權的網域名稱，系統管理員取得 hello DNS 項目從 Azure AD，Azure AD，看起來，並將 hello 網域名稱的項目 toohello DNS 區域檔案。 hello DNS 區域檔案是由該網域的 hello 網域名稱註冊機構維護。 網域如下所示 hello 文件以 hello 步驟 tooverify[新增自訂網域 tooyour Azure AD 目錄](active-directory-add-domain.md)。

加入 hello 網域名稱的 DNS 項目 toohello 區域檔案，不會影響其他的網域服務，例如電子郵件或 web 裝載。

## <a name="federated-and-managed-domain-names"></a>同盟和受管理的網域名稱
在 Azure AD 中的自訂網域名稱可以是使用者設定的 toogive 同盟的登入您的內部部署 Active Directory 與 Azure AD 之間的體驗。 設定網域的同盟需要在 Azure AD 中更新 tooprivileged 資源和也 tooyour Windows Server Active Directory。 設定同盟網域的工作必須在 Azure AD Connect 中或使用 PowerShell 來完成。 將自訂網域加入同盟無法起始從 hello Azure 傳統入口網站。 [觀賞此視訊 toolearn 設定使用 Azure AD Connect 的使用者登入的 AD FS 相關](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)。

未同盟的網域有時也稱為受管理的網域。 hello Azure AD 目錄的初始網域會隱含地評估為受管理的網域中。

## <a name="primary-domain-names"></a>主要網域名稱
hello 主要網域名稱的目錄是 hello 網域名稱時，預先選取 hello hello '網域' 部分 hello 使用者名稱，預設值為系統管理員建立新的使用者在 hello [Azure 入口網站](https://portal.azure.com/)，或另一個入口網站例如 hello Office 365 系統管理入口網站或 hello Microsoft Intune 入口網站。 目錄只能有一個主要網域名稱。 系統管理員可以變更 hello 主要網域名稱 toobe，任何已驗證的自訂網域，不同盟或 toohello 初始網域。

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Azure AD 和其他 Microsoft Online Services 中的網域名稱
必須先在 Azure AD 中驗證網域名稱，才可將其提供 Exchange Online、SharePoint Online 和 Intune 等另一個 Microsoft Online Service 使用。 這些其他服務通常需要系統管理員 tooadd 是特定 toohello 服務的一個或多個 DNS 項目。

Azure web 應用程式會使用它自己的機制 tooverify 擁有權的網域。 網域必須驗證是否可用於 Azure AD，即使它先前已驗證可供仰賴該 Azure AD 之訂用帳戶中的 Azure Web 應用程式使用也是如此。 Azure web 應用程式可以使用從 hello 目錄，可保護 hello web 應用程式的不同目錄中已驗證的網域名稱。

## <a name="managing-domain-names"></a>管理網域名稱
從 Azure 傳統入口網站 hello 和 PowerShell，可以完成定義域管理工作。 可以使用 hello Azure AD Graph API 來完成許多工作。

* [新增和驗證自訂網域名稱](active-directory-add-domain.md)
* [管理網域中 hello Azure 傳統入口網站](active-directory-add-manage-domain-names.md)
* [在 Azure AD 中使用 PowerShell toomanage 網域名稱](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [使用 Azure AD 中的 hello Azure AD Graph API toomanage 網域名稱](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

