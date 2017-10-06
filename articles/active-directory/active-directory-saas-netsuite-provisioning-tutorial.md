---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Netsuite 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>教學課程︰設定 Netsuite 來自動佈建使用者

本教學課程的 hello 目標是 tooshow hello 需要 tooperform Netsuite 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooNetsuite 中的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   啟用 Netsuite 單一登入的訂用帳戶
*   Netsuite 中具有小組管理員權限的使用者帳戶。

## <a name="assigning-users-toonetsuite"></a>指派使用者 tooNetsuite

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Netsuite 的應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Netsuite 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>指派使用者 tooNetsuite 的重要秘訣

*   建議在單一 tooNetsuite tootest hello 佈建組態指派給 Azure AD 使用者。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooNetsuite 時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-user-provisioning"></a>啟用使用者佈建

本節會引導您完成連接您的 Azure AD tooNetsuite 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用在 Netsuite 的 Azure AD 中的使用者和群組指派為基礎的指派的使用者帳戶。

> [!TIP] 
> 您也可以選擇 tooenabled SAML 型單一登入 netsuite，遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-user-account-provisioning"></a>tooconfigure 使用者帳戶佈建：

hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooNetsuite。

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2. 如果您已經設定 Netsuite 的單一登入，搜尋您 Netsuite 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Netsuite** hello 應用程式庫中。 從 hello 搜尋結果中，選取 Netsuite，並將它新增 tooyour 的應用程式的清單。

3. 選取您的 Netsuite，執行個體，然後選取 hello**佈建**] 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 

    ![佈建](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. 在 [hello**系統管理員認證**區段中，提供下列組態設定的 hello:
   
    a. 在 hello**系統管理員使用者名稱**文字方塊中，輸入 Netsuite 帳戶名稱已 hello**系統管理員**Netsuite.com 指派中的設定檔。
   
    b. 在 [hello**系統管理員密碼**文字方塊中，此帳戶類型 hello 密碼。
      
6. 在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Netsuite 的應用程式可以連接。

7. 在 [hello**通知電子郵件**欄位中，輸入 hello 電子郵件地址的個人或群組應該收到佈建錯誤通知，並選取 hello 核取方塊。

8. 按一下 [儲存]。

9. 在 [hello 對應區段中，選取**tooNetsuite 同步處理 Azure Active Directory 使用者。**

10. 在 [hello**屬性對應**區段中，檢閱 hello 使用者屬性從 Azure AD tooNetsuite 同步。 請注意，hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 中的使用者帳戶 Netsuite 進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

11. tooenable hello Azure AD 佈建服務 netsuite，變更 hello**佈建狀態**太**上**hello 設定] 區段中

12. 按一下 [儲存]。

它會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooNetsuite 在 hello 使用者和群組 > 一節。 請注意 hello 初始同步處理所花費的時間 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述 hello 佈建您 Netsuite 的應用程式上的服務所執行的所有動作。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理 tooNetsuite too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-netsuite-tutorial.md)