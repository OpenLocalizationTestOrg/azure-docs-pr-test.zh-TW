---
title: "aaaNo 使用者正在佈建的 tooan Azure AD 組件庫的應用程式 |Microsoft 文件"
description: "Tootroubleshoot 常見問題面臨著時您沒有看到使用者出現在 Azure AD 的組件庫的應用程式已設定為進行使用者佈建與 Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>正在佈建的 tooan Azure AD 組件庫的應用程式沒有任何使用者。

已設定一次自動佈建應用程式 （包括驗證是有效的 tooAzure AD tooconnect toohello 應用程式提供 hello 應用程式認證）。 然後使用者和/或群組的已佈建的 toohello 應用程式，而且由下列項目 hello:

-   使用者和群組已被**指派**toohello 應用程式。 如需有關指派的詳細資訊，請參閱[指派的使用者或群組 tooan 企業應用程式在 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)。

-   是否**屬性對應**是從 Azure AD toohello 應用程式已啟用，且設定 toosync 有效的屬性。 如需詳細資訊，請參閱[在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)。

-   是否存在**範圍設定篩選**，這會根據根據特定的屬性值來篩選使用者。 如需範圍設定篩選條件的詳細資訊，請參閱[含範圍篩選器的屬性型應用程式佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)。

當觀察，使用者不正在佈建，請參閱 Azure AD 中的 hello 稽核記錄和搜尋特定使用者的記錄項目。

佈建稽核記錄檔的 hello 可於 hello Azure 入口網站中 hello **Azure Active Directory&gt;企業應用程式&gt;\[應用程式名稱\]&gt;稽核記錄**] 索引標籤。篩選 hello 登入 hello**帳戶佈建**tooonly 類別目錄，請參閱 「 hello 佈建該應用程式的事件。 您可以根據 hello 「 比對識別碼 」 hello 屬性對應中為其設定為使用者進行搜尋。 例如，如果您設定 hello 「 使用者主體名稱 」 或 「 電子郵件地址 」 為 hello 比對一邊 hello Azure AD 的屬性和 hello 使用者未提供的值為"audrey@contoso.com"。 然後搜尋 hello 稽核記錄檔 」audrey@contoso.com"，而且檢閱則傳回項目。

hello 佈建稽核記錄檔的記錄所有 hello hello 佈建服務，包括 Azure AD 佈建、 查詢 hello 目標應用程式，這些使用者的 hello 存在、 比較 hello 的範圍中的指派使用者查詢所執行的作業hello 系統之間的使用者物件。 然後加入、 更新或停用根據 hello 比較 hello 目標系統中的 hello 使用者帳戶。

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>佈建 tooconsider 一般問題區域

以下是一般的問題區域，如果您有了解的位置可以切入一份 hello toostart。

* [佈建服務不會出現 toostart](#provisioning-service-does-not-appear-to-start)
* [稽核記錄表示「已略過」且未佈建使用者，即使已指派它們](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>佈建服務不會出現 toostart

如果您設定 hello**佈建狀態**toobe**上**在 hello **Azure Active Directory&gt;企業應用程式&gt; \[的應用程式名稱\]&gt;佈建**hello Azure 入口網站的區段。 但是沒有其他狀態詳細資料會顯示該頁面上後續重新載入之後可能 hello 服務正在執行，但尚未完成初始同步處理尚未。 檢查 hello**稽核記錄檔**toodetermine 上面所述執行哪些作業 hello 服務，以及是否有任何錯誤。

>[!NOTE]
>初始同步處理可能需要 20 分鐘 tooseveral 個小時，視 hello 大小 hello Azure AD 目錄與 hello 佈建的範圍中的使用者數目而定。 為 hello 佈建服務儲存的這兩個系統的 hello 狀態代表 hello 初始同步處理之後的浮水印，hello 初始同步處理之後的後續同步處理時，速度加快。這會改善後續同步處理的效能。
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>稽核記錄表示「已略過」且未佈建使用者，即使已指派它們

使用者顯示為 「 已略過 「 hello 稽核記錄檔中，時非常重要的 tooread hello 擴充中 hello 記錄訊息 toodetermine hello 原因的詳細資料。 下面是常見原因和解決方式：

-   **已設定範圍的篩選器** **，過濾 hello 使用者根據屬性值**。 如需範圍設定篩選的詳細資訊，請參閱 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>。

-   **「 無法有效地標題為 「 hello 使用者。** 如果您看到此特定錯誤訊息，它是因為沒有 hello 使用者指派記錄儲存在 Azure AD 中的問題。 toofix 這個問題，請不要指派 hello 使用者 （或群組），從 hello 應用程式，並重新將它指派一次。 如需指派的詳細資訊，請參閱 <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>。

-   **必要屬性已遺失或未針對使用者填入。** 設定佈建是 tooreview 時很重要的事 tooconsider 及設定 hello 屬性對應，以及定義哪些使用者 （或群組） 的屬性流程，從 Azure AD toohello 應用程式的工作流程。 這包括設定 hello 「 比對屬性 」 會使用的 toouniquely 找出並符合 hello 兩個系統之間的使用者/群組。 如需這個重要程序的詳細資訊，請參閱[在 Azure Active Directory 中自訂 SaaS 應用程式的使用者佈建屬性對應](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)。

  * **屬性群組的對應：** hello 佈建群組名稱和群組詳細資料，加法 toohello 成員 中的，如果對於某些應用程式支援。 您可以啟用或停用此功能啟用或停用 hello**對應**hello 所顯示的群組物件的**佈建** 索引標籤。如果已啟用佈建群組，請務必 tooreview hello 屬性對應 tooensure 適當的欄位會用於 hello"比對識別碼 」。 這可能是 hello 顯示名稱或電子郵件別名），如 hello 群組及其成員無法提供如果 hello 相符的屬性是空的或不填入群組在 Azure AD 中。

## <a name="next-steps"></a>後續步驟
[Azure AD Connect 同步處理：了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

