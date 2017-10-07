---
title: "佈建的 hello Azure Active Directory 中的企業應用程式管理的 aaaUser |Microsoft 文件"
description: "了解如何 toomanage 使用者帳戶佈建為使用 hello Azure Active Directory 的企業應用程式"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>管理企業中的應用程式 hello Azure 入口網站佈建使用者帳戶
本文說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)toomanage 自動使用者帳戶佈建和解除佈建的應用程式，支援它，特別是已從 hello 加入 「 熱門 」 的類別hello [Azure Active Directory 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)。 toolearn 深入了解使用者自動帳戶佈建和它的運作方式，請參閱[自動化使用者佈建和取消佈建 tooSaaS 應用程式與 Azure Active Directory](active-directory-saas-app-provisioning.md)。

## <a name="finding-your-apps-in-hello-portal"></a>在 hello 入口網站中尋找您的應用程式
所有應用程式，已針對單一登入在目錄中，目錄管理員使用 hello [Azure Active Directory 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)，可以檢視及管理在 hello [Azure 入口網站](https://portal.azure.com). hello 應用程式可以在 hello**更服務** &gt; **企業應用程式**hello 入口網站的區段。 企業應用程式是您組織內部署和使用的應用程式。

![企業應用程式刀鋒視窗][0]

選取 hello**所有應用程式**hello 左側的連結會顯示所有已設定，包括已加入從 hello 組件庫的應用程式的應用程式清單。 選取應用程式載入 hello 資源刀鋒視窗，該應用程式，其中可以檢視報告，該應用程式，且可管理各種不同的設定。

佈建設定的使用者帳戶可管理所選取**佈建**hello 左側。

![應用程式資源刀鋒視窗][1]

## <a name="provisioning-modes"></a>佈建模式
hello**佈建**刀鋒視窗開頭**模式**功能表上，這會顯示哪些佈建模式支援企業應用程式，並允許它們 toobe 設定。 hello 可用的選項包括：

* **自動**-當 Azure AD 支援自動 API 為基礎的佈建及/或解除佈建使用者帳戶 toothis 應用程式會出現這個選項。 選取此模式會顯示引導系統管理員可以透過設定 Azure AD tooconnect toohello 應用程式的使用者管理 API、 建立帳戶對應和定義使用者帳戶資料的 Azure AD 之間的流程為何的工作流程的介面和hello 應用程式，以及管理 hello Azure AD 佈建服務。
* **手動**-是否 Azure AD 不支援自動佈建使用者帳戶 toothis 應用程式顯示這個選項。 此選項表示必須使用外部處理序，根據 hello 使用者管理和佈建所提供的功能 （其中包含 SAML Just-In-Time 佈建） 該應用程式來管理儲存在 hello 應用程式的使用者帳戶記錄。

## <a name="configuring-automatic-user-account-provisioning"></a>設定使用者帳戶自動佈建
選取 hello**自動**選項會顯示的畫面，分成四個區段：

### <a name="admin-credentials"></a>管理員認證
這是其中輸入 hello Azure AD tooconnect toohello 應用程式的使用者管理 API 所需的認證。 所需的 hello 輸入 hello 應用程式而有所不同。 toolearn 有關 hello 認證類型和特定的應用程式的需求，請參閱 「 hello[設定該特定應用程式的教學課程](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning)。

選取 hello**測試連接**按鈕可讓您 tootest hello 認證，讓 Azure AD 嘗試 tooconnect toohello 應用程式的佈建應用程式使用 hello 提供認證。

### <a name="mappings"></a>對應
這是系統管理員可以檢視和編輯 Azure AD 之間的哪些使用者屬性流程的位置和 hello 目標應用程式，當使用者帳戶佈建或更新時。

在 Azure AD 使用者物件和每個 SaaS 應用程式的使用者物件之間，有一組預先設定的對應。 有些 app 則管理其他類型的物件，例如群組或連絡人。 在 hello 資料表中選取其中一個這些對應顯示 hello 對應編輯器 」 toohello 右側，其中他們可以檢視和自訂。

![應用程式資源刀鋒視窗][2]

支援的自訂項目包含：

* 啟用和停用特定物件，例如 hello Azure AD 使用者物件 toohello SaaS 應用程式的使用者物件的對應。
* 編輯的屬性流程從 hello Azure AD 使用者物件 toohello 應用程式的使用者物件。 如需有關屬性對應的詳細資訊，請參閱 [了解屬性對應類型](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types)。
* 佈建 Azure AD 在 hello 所執行的動作篩選條件 hello 應用程式為目標。 您不需要完整同步處理物件的 Azure AD，您可以限制 hello 執行的動作。 例如，只選取 **更新**，Azure AD 只會更新應用程式中的現有使用者帳戶，不會建立新的。 只有選取 **建立**，Azure 只會建立新的使用者帳戶，但不會更新現有的。 這項功能可讓系統管理員帳戶 toocreate 不同對應建立和更新的工作流程。

### <a name="settings"></a>設定
這個區段可讓系統管理員 」 toostart 並停止 hello hello 選取應用程式，以及選擇性地清除 hello 佈建的 Azure AD 佈建服務快取和重新啟動 hello 服務。

佈建已啟用 hello 應用程式的第一次，如果開啟變更 hello hello 服務**佈建狀態**太**上**。 這會導致 hello Azure AD 佈建服務 tooperform 初始同步處理，它會讀取 hello 中獲指派的 hello 使用者**使用者和群組** 區段中，查詢 hello 目標應用程式，並接著執行 hello 佈建在 hello Azure AD 中定義的動作**對應**> 一節。 在此過程中，佈建服務的 hello 會儲存管理，哪些使用者帳戶的相關的快取的資料，因此永遠不會在指派的範圍中的 hello 目標應用程式內的非受管理的帳戶不受解除佈建作業。 後 hello 初始同步處理，會自動佈建服務的 hello，請在 10 分鐘間隔同步使用者和群組物件。

變更 hello**佈建狀態**太**關閉**只要暫停 hello 佈建的服務。 在這個狀態下，Azure 不會不建立、 更新或移除 hello 應用程式中的任何使用者或群組物件。 變更 hello 狀態回復 tooon 會導致 hello 服務 toopick 向上中斷的位置。

選取 hello**清除目前的狀態，並重新啟動同步處理**核取方塊，並儲存停駐點 hello 佈建服務、 傾印 hello 快取資料有關哪些 Azure AD 的帳戶來管理，hello 服務重新啟動且執行 hello一次初始同步處理。 此選項可讓系統管理員 」 toostart hello 重新佈建部署程序。

### <a name="synchronization-details"></a>同步處理詳細資料
本節提供新增的佈建服務的 hello hello 作業詳細資料，包括 hello 第一個和最後一個時間 hello 佈建服務中，執行對 hello 應用程式，以及受管理使用者和群組物件的數目。

會提供連結 toohello**佈建活動報表**，這樣會提供記錄檔的所有使用者和群組建立、 更新與移除之間的 Azure AD hello 目標應用程式，並 toohello**佈建錯誤報表**文中提供更多詳細的錯誤訊息，使用者和群組物件的讀取、 建立、 更新或移除該失敗的 toobe。 

##<a name="feedback"></a>意見反應

我們希望您喜歡您的 Azure AD 經驗。 請保留來自 hello 意見反應 ！ 將張貼到您的意見反應與改進的想法 hello**管理入口**區段我們[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)。  我們正在興奮建置新很棒的每一天，和使用指引 tooshape 作業，並定義什麼接下來要建立。


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
