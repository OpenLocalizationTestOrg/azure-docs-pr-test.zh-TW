---
title: "aaaAzure Active Directory Graph API |Microsoft 文件"
description: "概觀和快速入門指南 hello Graph API 允許以程式設計方式存取 tooAzure AD 透過 REST API 端點。"
services: active-directory
documentationcenter: 
author: viv-liu
manager: mbaldwin
editor: mbaldwin
ms.assetid: 5471ad74-20b3-44df-a2b5-43cde2c0a045
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: cde1dd86b0ca1dc24a5b46dc578b6245ba98751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-graph-api"></a>Azure Active Directory 圖形 API
> [!IMPORTANT]
> 我們強烈建議您改用[Microsoft Graph](https://graph.microsoft.io/)而不是 Azure AD Graph API tooaccess Azure Active Directory 資源。 我們的開發工作現在是針對 Microsoft Graph，並沒有針對 Azure AD Graph API 規劃的進一步增強功能 。 有極少數的情況下，Azure AD Graph API 仍可能適合;如需詳細資訊，請參閱 hello [Microsoft Graph 或 hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office 開發人員中心中的部落格文章。
> 
> 

hello Azure Active Directory Graph API 提供以程式設計方式存取 tooAzure AD 透過 REST API 端點。 應用程式可以使用 hello Graph API tooperform 建立、 讀取、 更新和刪除 (CRUD) 作業目錄資料和物件。 例如，hello Graph API 支援下列使用者物件的一般作業的 hello:

* 在目錄中建立新的使用者
* 取得使用者的詳細屬性，例如其群組
* 更新使用者的屬性 (例如其位置和電話號碼)，或變更其密碼
* 檢查使用者在角色型存取方面的群組成員資格
* 停用使用者帳戶或完全刪除

在加法 toouser 物件中，您可以執行類似的作業，例如群組和應用程式的其他物件。 toocall hello 必須向 Azure AD Graph API 目錄，hello 應用程式，而且被設定 tooallow 存取 toohello 目錄。 這通常是透過使用者或系統管理員同意流程來達成。

使用 toobegin hello Azure Active Directory Graph API，請參閱 hello [Graph API 快速入門指南](active-directory-graph-api-quickstart.md)，或檢視 hello[互動式圖形 API 參考文件](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)。

## <a name="features"></a>特性
hello Graph API 提供下列功能的 hello:

* **REST API 端點**: hello Graph API 是 RESTful 服務會使用標準 HTTP 要求存取的端點所組成。 hello Graph API 要求和回應支援 XML 或 Javascript 物件標記法 (JSON) 內容類型。 如需詳細資訊，請參閱 [Azure AD Graph REST API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)。
* **向 Azure AD 驗證**: Graph API 必須經過附加 JSON Web Token (JWT) hello hello 要求授權標頭中的每個要求 toohello。 取得此權杖的要求 tooAzure AD 的權杖端點，提供有效的認證。 您可以使用 OAuth 2.0 用戶端認證流程 hello 或 hello 授權碼授與流程 tooacquire 語彙基元 toocall hello 圖形。 如需詳細資訊，請參閱 [Azure AD 中的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* **以角色為基礎的授權 (RBAC)**： 安全性群組都使用的 tooperform RBAC hello Graph API 中。 例如，如果使用者是否能存取 tooa 特定資源，您會想 toodetermine，hello 應用程式可以呼叫 hello[檢查群組成員資格 （可轉移）](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#FunctionsandactionsongroupsCheckmembershipinaspecificgrouptransitive)作業，它會傳回 true 或 false。
* **差異查詢**： 如果您需要 toocheck 的兩個時間週期，而不需要 toomake 之間目錄中的變更頻繁的查詢 toohello Graph API，您就可以提出差異查詢要求。 此類型的要求會傳回先前差異查詢要求 hello 與 hello 目前要求之間所做的只有 hello 變更。 如需詳細資訊，請參閱 [Azure AD Graph API 差異查詢](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-differential-query)。
* **目錄延伸模組**： 如果您正在開發需要 tooread 或寫入的唯一屬性為目錄物件的應用程式，您可以註冊及使用 hello Graph API 中使用延伸模組值。 比方說，如果您的應用程式需要每個使用者的 Skype ID 屬性，您可以在 hello 目錄中註冊 hello 新屬性，並將予以提供每個使用者物件上。 如需詳細資訊，請參閱 [Azure AD Graph API 目錄結構描述延伸模組](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)。
* **受到權限範圍**: AAD Graph API 會公開權限範圍，以啟用安全/同意存取 tooAAD 資料，並支援各種不同的用戶端應用程式類型，包括：
  
  * 會提供委派的使用者介面的存取透過授權 toodata 從 hello 登入的使用者 （委派）
  * 使用服務/服務精靈用戶端 (應用程式角色) 等應用程式定義角色型存取控制的類型
    
    同時委派和應用程式角色權限範圍代表 hello Graph API 所公開的權限，而且可以透過應用程式註冊權限的用戶端應用程式要求[hello Azure 入口網站中的功能](https://portal.azure.com)。 用戶端可以確認 hello 權限範圍授與 toothem 檢查收到 hello 委派的權限的存取權杖中的 hello 範圍 ("scp") 宣告與 hello 角色 （「 角色 」） 宣告的應用程式角色權限。 深入了解 [Azure AD 圖形 API 權限範圍](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)。

## <a name="scenarios"></a>案例
hello Graph API 可讓許多應用程式案例。 下列案例的 hello 是最常見的 hello:

* **企業營運 (單一租用戶) 應用程式**：在此案例中，企業開發人員任職於具有 Office 365 訂用帳戶的組織中。 hello 開發人員正在建置 web 應用程式與互動的 Azure AD tooperform 工作，例如指派授權 tooa 使用者。 這項工作需要存取 toohello Graph API，因此 hello 開發人員在 Azure AD 中註冊 hello 單一租用戶應用程式，並設定讀取和寫入 hello Graph API 的權限。 然後 hello 應用程式是設定的 toouse，可能是它自己的認證，或這些 hello 目前登入的使用者 tooacquire 語彙基元 toocall hello Graph API。
* **軟體即服務應用程式 (多租用戶)**：在此案例中，獨立軟體廠商 (ISV) 正在開發託管的多租用戶 Web 應用程式，目的是為使用 Azure AD 的其他組織提供使用者管理功能。 這些功能都需要存取 toodirectory 物件，並因此 hello 應用程式所需要的 toocall hello Graph API。 hello 開發人員在 Azure AD 中註冊 hello 應用程式、 將它設定 toorequire 讀取和 hello Graph API 的寫入權限，然後啟用外部存取，讓其他組織可同意 toouse hello 應用程式，在他們的目錄。 當另一個組織中的使用者進行驗證 toohello 應用程式的 hello 第一次時，它們會顯示以 hello hello 應用程式所要求的權限的同意對話方塊。  這些要求的權限 toohello Graph API hello 使用者的目錄中授與同意然後會提供 hello 應用程式。 如需有關 hello 同意架構的詳細資訊，請參閱[hello 同意架構的概觀](active-directory-integrating-applications.md)。

## <a name="see-also"></a>另請參閱
[Azure AD Graph API 快速入門指南](active-directory-graph-api-quickstart.md)

[AD Graph REST 文件](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)

[Azure Active Directory 開發人員指南](active-directory-developers-guide.md)

