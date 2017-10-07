---
title: "Azure Active Directory 使用者自動帳戶佈建 tooSaaS 應用程式報告 |Microsoft 文件"
description: "了解如何 toocheck hello 狀態的使用者自動帳戶佈建工作，以及如何 tootroubleshoot hello 佈建之個別使用者。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>教學課程︰關於使用者帳戶自動佈建的報告


Azure Active Directory 包含[佈建服務的使用者帳戶](active-directory-saas-app-provisioning.md)可協助自動化 hello 佈建的 SaaS 應用程式和目的端對端的身分識別生命週期的 hello 的其他系統中的使用者帳戶解除佈建管理。 Azure AD 支援預先整合的使用者佈建所有 hello 應用程式和系統的 hello 「 精選 」 一節中的 hello 連接器[Azure AD 應用程式庫](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)。

本文說明如何 toocheck hello 狀態的佈建作業之後他們已設定，以及如何 tootroubleshoot hello 佈建的個別使用者和群組。

## <a name="overview"></a>概觀

佈建的連接器是設定主要是使用和設定 hello [Azure 管理入口網站](https://portal.azure.com)，由下列 hello[提供文件](active-directory-saas-tutorial-list.md)hello 應用程式使用者帳戶佈建的位置所需。 應用程式的佈建作業在設定好並開始執行後，您就可以使用下列兩種方法之一來獲得這些作業的報告︰

* **Azure 管理入口網站**-本文主要說明從 hello 擷取報表資訊[Azure 管理入口網站](https://portal.azure.com)，以提供同時佈建摘要報表，以及詳細的佈建稽核記錄檔中的特定應用程式。

* **稽核 API** -Azure Active Directory 也提供 API 以程式設計方式擷取 hello 詳細佈建可讓稽核記錄檔稽核。 請參閱[Azure Active Directory 稽核應用程式開發介面參考](active-directory-reporting-api-audit-reference.md)的文件特定 toousing 這個 API。 雖然本文未特別涵蓋如何 toouse hello API，其詳細說明 hello 類型的佈建 hello 稽核記錄檔中記錄的事件。

### <a name="definitions"></a>定義

本文使用 hello 下列條款，定義如下：

* **來源系統**-hello 儲存機制的 hello Azure AD 佈建服務的使用者同步處理。 Azure Active Directory 是 hello 大部分的 hello 來源系統預先整合 [佈建連接器，不過有一些例外狀況 (範例： Workday 輸入同步處理)。

* **目標系統**-hello 儲存機制的 hello Azure AD 佈建服務的使用者同步處理與。 這通常是 SaaS 應用程式 (範例： Salesforce、 ServiceNow、 Google Apps、 dropbox 企業版)，但在某些情況下可能會在內部部署系統，例如 Active Directory (範例： Workday 輸入同步處理 tooActive 目錄)。


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>開始佈建 hello Azure 管理入口網站從報表

tooget 佈建報表資訊，為給定的應用程式，開始啟動 hello [Azure 管理入口網站](https://portal.azure.com)和瀏覽 toohello 企業應用程式的設定佈建。 例如，如果您要佈建使用者 tooLinkedIn 提高權限，是 hello 導覽路徑 toohello 應用程式詳細資料：

**Azure Active Directory > 企業應用程式 > 所有應用程式 > LinkedIn Elevate**

從這裡，您可以存取 hello 佈建摘要報表和 hello 佈建的稽核記錄，同時如下所述。


### <a name="provisioning-summary-report"></a>佈建摘要報告

hello 佈建摘要報表會顯示在 [hello**佈建**索引標籤上指定的應用程式。 位於 hello 同步處理詳細資料] 區段下方**設定**，並提供下列資訊的 hello:

* hello 總數的使用者和群組的已同步處理，並目前正在進行佈建 hello 來源系統與 hello 目標系統之間的範圍中。

* 已執行 hello 上次 hello 同步處理。 在完成完整的同步處理之後，系統通常每隔 20 到 40 分鐘就會進行一次同步處理。

* 是否已完成初次的完整同步處理。

* 已佈建程序的 hello 放置於隔離，以及哪些 hello hello 隔離狀態是例如 (因為 tooinvalid 系統管理員認證的目標系統的失敗 toocommunicate)

hello 佈建摘要報表應該 hello 第一個位置 admins 外觀 toocheck hello hello 佈建作業的操作健全狀況。

 ![摘要報告](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>佈建稽核記錄
Hello 佈建服務所執行的所有活動都會都記錄在 hello Azure AD 稽核記錄，就可以在 hello 檢視**稽核記錄檔**] 索引標籤下 hello**帳戶佈建**類別目錄。 所記錄的活動事件類型包括︰

* **匯入事件**-「 匯入 」 事件會記錄每次 hello Azure AD 佈建服務擷取個別使用者或群組的相關資訊的來源系統或目標系統。 同步處理期間，使用者會從擷取 hello 來源系統首先，使用 hello 結果記錄為 「 匯入 」 事件。 如果它們存在 hello 結果也會記錄為 「 匯入 」 事件具有相符識別碼的 hello 擷取使用者然後會針對 hello 目標系統 toocheck 查詢 hello。 這些事件會記錄所有對應的使用者屬性以及它們在 hello 事件時間的 hello hello Azure AD 佈建服務所看到的值。 

* **同步處理規則事件**-這些事件報告的 hello 屬性對應規則的 hello 結果和任何設定範圍的篩選器之後使用者資料已匯入和評估 hello 來源與目標系統。 例如，如果來源系統中的使用者會被視為在範圍內的佈建，toobe 視為 toonot 存在於 hello 目標系統，然後 hello 使用者此事件記錄將會佈建 hello 目標系統中。 

* **匯出事件**-「 匯出 」 事件會記錄每次 hello Azure AD 佈建服務會將使用者帳戶或群組物件 tooa 目標系統。 這些事件會記錄所有的使用者屬性與值撰寫 hello Azure AD 佈建服務的 hello 事件 hello 次。 如果寫入 hello 使用者帳戶或群組物件 toohello 目標系統時發生錯誤，它將會顯示於此。

* **處理委付事件**-escrows 程序時，會發生 hello 佈建服務發生失敗時嘗試的作業，並開始 tooretry hello 作業，以輪詢間隔的時間。 每當服務淘汰佈建作業時，就會記錄下「委付」事件。

查看個別的使用者佈建事件，當 hello 事件通常會發生順序如下：

1. 匯入事件： 從 hello 來源系統擷取使用者。

2. 匯入事件： 目標系統是查詢的 toocheck hello hello 擷取使用者是否存在。

3. 同步處理規則的事件： 來源和目標系統中的使用者資料進行評估 hello 設定屬性對應規則及範圍設定篩選 toodetermine 什麼動作，如果有的話，應該執行。

4. 匯出事件： hello 同步處理規則的事件可讓您指定動作應該是如果 hello hello 動作結果會記錄在匯出事件，然後執行 （例如加入、 更新、 刪除）。

![建立 Azure AD 測試使用者](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>查閱特定使用者的佈建事件

hello hello 佈建稽核記錄檔的最常見使用案例是 toocheck hello 佈建個別使用者帳戶的狀態。 toolook hello 最後一個佈建的事件特定使用者：

1. 移 toohello**稽核記錄檔**> 一節。

2. 從 hello**類別**功能表上，選取**帳戶佈建**。

3. 在 [hello**日期範圍**功能表中，您想要 toosearch，選取 hello 日期範圍

4. 在 [hello**搜尋**列上，輸入您想針對 toosearch hello 使用者 hello 使用者識別碼。 hello 的識別碼值的格式應該符合您選取的項目為 hello hello 屬性對應設定 （例如 userPrincipalName 或員工 ID 編號） 中的主要符合 ID。 所需的 hello ID 值會顯示 hello 目標資料行中。

5. 按下 Enter toosearch。 會先傳回最新的佈建事件 hello。

6. 如果傳回的事件，請注意 hello 活動型別和是否成功或失敗。 如果不傳回任何結果，則表示 hello 使用者不存在，或尚未偵測到的 hello 佈建程序，如果完整的同步處理尚未完成。

7. 按一下個別事件 tooview 擴充詳細資料，包括所有的使用者內容已擷取、 評估，或撰寫為 hello 事件的一部分。


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>檢視佈建稽核記錄檔的 hello 的秘訣

Hello Azure 入口網站中的最佳可讀性，選取 [hello**資料行**按鈕，並選擇這些資料行：

* **日期**-顯示 hello 日期 hello 事件發生的情況。
* **目標**-顯示 hello 應用程式名稱和使用者識別碼的 hello 主旨 hello 事件。
* **活動**-hello 活動型別，如先前所述。
* **狀態**-是否 hello 事件成功與否。
* **狀態原因**-hello 佈建事件中發生什麼情況的摘要。


## <a name="troubleshooting"></a>疑難排解

佈建摘要的報表和稽核記錄檔的 hello 扮演重要的角色，協助疑難排解各種不同的使用者帳戶佈建問題的系統管理員。

如需如何以案例為基礎指引 tootroubleshoot 自動使用者佈建，請參閱[設定和佈建使用者 tooan 應用程式的問題](active-directory-application-provisioning-content-map.md)。


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
