---
title: "設定使用者佈建 Azure AD tooan 組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "Tootroubleshoot 常見問題面臨著時設定使用者佈建 tooan 應用程式已經列於 hello Azure AD 應用程式庫"
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>設定使用者佈建 Azure AD tooan 組件庫的應用程式的問題

設定[自動使用者佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)的應用程式 （在支援），要求特定指示必須接著的 tooprepare hello 應用程式的自動佈建。 然後您可以使用 hello Azure 入口網站 tooconfigure hello 佈建服務 toosynchronize 使用者帳戶 toohello 應用程式。

您永遠應該開始尋找 hello 安裝教學課程特定 toosetting 上佈建您的應用程式。 依照這些步驟 tooconfigure 這兩個 hello 應用程式與 Azure AD toocreate hello 佈建的連接。 位於應用程式教學課程清單[清單的教學課程有關 tooIntegrate SaaS 應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)。

## <a name="how-toosee-if-provisioning-is-working"></a>如果佈建 toosee 運作 

Hello 服務設定之後，大部分 hello hello 服務作業的深入剖析可以繪製從兩個地方：

-   **稽核記錄檔**– hello 佈建 hello 佈建服務所執行的所有 hello 作業的稽核記錄檔記錄，包括查詢 Azure AD 中的獲得指派使用者佈建的範圍內。 查詢 hello hello 存在的使用者，比較 hello hello 系統之間的使用者物件的目標應用程式。 然後加入、 更新或停用根據 hello 比較 hello 目標系統中的 hello 使用者帳戶。 佈建稽核記錄檔的 hello 可於 hello Azure 入口網站中 hello **Azure Active Directory&gt;企業應用程式&gt;\[應用程式名稱\]&gt;稽核記錄**] 索引標籤。篩選 hello 登入 hello**帳戶佈建**tooonly 類別目錄，請參閱 「 hello 佈建該應用程式的事件。

-   **佈建狀態 –** hello 最後一個佈建的摘要執行給定的應用程式可以看到在 hello **Azure Active Directory&gt;企業應用程式&gt;\[應用程式名稱\] &gt;佈建**底部 hello 囉 」 畫面下 hello 服務設定 > 一節。 本節摘要說明多少使用者 （和/或群組） 目前正在同步處理之間 hello 兩個系統，以及是否有任何錯誤。 錯誤詳細資料會在 hello 稽核記錄檔中。 請注意，hello 佈建狀態不會填入 Azure AD 之間完成一個完整的初始同步處理後，才與 hello 應用程式。

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>佈建 tooconsider 的一般問題區域

以下是一般的問題區域，如果您有了解的位置可以切入一份 hello toostart。

* [佈建服務不會出現 toostart](#provisioning-service-does-not-appear-to-start)
* [無法儲存組態，因為 tooapp 認證無法運作](#can’t-save-configuration-due-to-app-credentials-not-working)
* [稽核記錄表示「已略過」且未佈建使用者，即使已指派它們](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>佈建服務不會出現 toostart

如果您設定 hello**佈建狀態**toobe**上**在 hello **Azure Active Directory&gt;企業應用程式&gt; \[的應用程式名稱\]&gt;佈建**hello Azure 入口網站的區段。 不過，在後續重新載入之後，該頁面上並未顯示任何其他狀態詳細資料。 很可能 hello 服務正在執行，但尚未完成初始同步處理尚未。 檢查 hello**稽核記錄檔**toodetermine 上面所述執行哪些作業 hello 服務，以及是否有任何錯誤。

>[!NOTE]
>初始同步處理可能需要 20 分鐘 tooseveral 個小時，視 hello 大小 hello Azure AD 目錄與 hello 佈建的範圍中的使用者數目而定。 Hello 初始同步處理之後的後續同步處理是更快、 佈建服務的 hello 儲存代表 hello 狀態，這兩個系統的 hello 初始同步處理之後，可改善效能的後續的同步處理的浮水印。
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>無法儲存組態，因為 tooapp 認證無法運作

為了讓佈建 toowork，Azure AD 需要有效的認證，允許它 tooconnect tooa 使用者管理該應用程式所提供的 API。 如果您不知道的 wat，檢閱 hello 教學課程中設定此應用程式，或這些認證不會運作，先前所述。

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>稽核記錄表示「已略過」且未佈建使用者，即使已指派它們

使用者顯示為 「 已略過 「 hello 稽核記錄檔中，時非常重要的 tooread hello 擴充中 hello 記錄訊息 toodetermine hello 原因的詳細資料。 下面是常見原因和解決方式：

-   **已設定範圍的篩選器** **，過濾 hello 使用者根據屬性值**。 如需範圍設定篩選的詳細資訊，請參閱 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>。

-   **「 無法有效地標題為 「 hello 使用者。** 如果您看到此特定錯誤訊息，它是因為沒有 hello 使用者指派記錄儲存在 Azure AD 中的問題。 toofix 這個問題，請不要指派 hello 使用者 （或群組），從 hello 應用程式，並重新將它指派一次。 如需指派的詳細資訊，請參閱 <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>。

-   **必要屬性已遺失或未針對使用者填入。** 設定佈建是 tooreview 時很重要的事 tooconsider 及設定 hello 屬性對應，以及定義哪些使用者 （或群組） 的屬性流程，從 Azure AD toohello 應用程式的工作流程。 這包括設定 hello 「 比對屬性 」 會使用的 toouniquely 找出並符合 hello 兩個系統之間的使用者/群組。 如需這個重要程序的詳細資訊，請參閱 <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>。

   * **屬性群組的對應：** hello 佈建群組名稱和群組詳細資料，加法 toohello 成員 中的，如果對於某些應用程式支援。 您可以啟用或停用此功能啟用或停用 hello**對應**hello 所顯示的群組物件的**佈建** 索引標籤。如果已啟用佈建群組，請務必 tooreview hello 屬性對應 tooensure 適當的欄位會用於 hello"比對識別碼 」。 這可能是 hello 顯示名稱或電子郵件別名），如 hello 群組及其成員無法提供如果 hello 相符的屬性是空的或不填入群組在 Azure AD 中。

#<a name="next-steps"></a>後續步驟
[自動化使用者佈建和取消佈建 tooSaaS 與 Azure Active Directory 的應用程式](active-directory-saas-app-provisioning.md)
