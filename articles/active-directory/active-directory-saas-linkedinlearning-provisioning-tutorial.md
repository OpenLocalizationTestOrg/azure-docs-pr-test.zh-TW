---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Learning | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 來自動佈建並取消佈建使用者帳戶至 LinkedIn Learning。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 9b07417fbb094cdc285e00be3c48f9af0a38601d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 LinkedIn Learning


本教學課程旨在說明您需要在 LinkedIn Learning 和 Azure AD 中執行的步驟，以將使用者帳戶從 Azure AD 自動佈建和取消佈建至 LinkedIn Learning。 

## <a name="prerequisites"></a>必要條件

本教學課程中說明的案例假設您已經具有下列項目：

*   Azure Active Directory 租用戶
*   LinkedIn Learning 租用戶 
*   可存取 LinkedIn 帳戶中心的 LinkedIn Learning 系統管理員帳戶

> [!NOTE]
> Azure Active Directory 使用 [SCIM](http://www.simplecloud.info/) 通訊協定與 LinkedIn Learning 整合。

## <a name="assigning-users-to-linkedin-learning"></a>將使用者指派給 LinkedIn Learning

Azure Active Directory 會使用稱為「指派」的概念，來判斷哪些使用者應接收對指定應用程式的存取權。 在自動使用者帳戶佈建的內容中，只有已「指派」至 Azure AD 中的應用程式之使用者和群組會進行同步處理。 

在設定並啟用佈建服務之前，您必須決定 Azure AD 中的哪些使用者及/或群組代表需要 LinkedIn Learning 存取權的使用者。 一旦決定後，您可以依照此處的指示，將這些使用者指派給 LinkedIn Learning：

[將使用者或群組指派給企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-learning"></a>將使用者指派給 LinkedIn Learning 的重要秘訣

*   建議將單一 Azure AD 使用者指派給 LinkedIn Learning，以測試佈建設定。 其他使用者及/或群組可能會稍後再指派。

*   將使用者指派給 LinkedIn Learning 時，您必須在 [指派] 對話方塊中選取 [使用者] 角色。 「預設存取」角色不適用於佈建。


## <a name="configuring-user-provisioning-to-linkedin-learning"></a>設定使用者佈建至 LinkedIn Learning

本節會引導您將 Azure AD 連線至 LinkedIn Learning 的 SCIM 使用者帳戶佈建 API，以及根據 Azure AD 中的使用者和群組指派，設定佈建服務以在 LinkedIn Learning 中建立、更新和停用指派的使用者帳戶。

> [!TIP]
> 您也可以選擇啟用 LinkedIn Learning 的 SAML 型單一登入，並遵循 [Azure 入口網站](https://portal.azure.com)中提供的指示。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-learning-in-azure-ad"></a>若要在 Azure AD 中設定自動使用者帳戶佈建至 LinkedIn Learning：


第一步是擷取您的 LinkedIn Elevate 存取權杖。 如果您是企業版系統管理員，可以自我佈建存取權杖。 在帳戶中心，移至 [設定]> [通用設定]**&gt;**，開啟 [SCIM 安裝] 面板。

> [!NOTE]
> 如果您是直接存取帳戶中心，而不是透過連結，可以使用下列步驟開啟面板。

1)  登入 Azure 帳戶。

2)  選取 [系統管理員] > [系統管理員設定]**&gt;**。

3)  按一下左欄中的 [進階整合]。 系統會將您導向帳戶中心。

4)  按一下 [+ 新增 SCIM 組態]，遵循程序填寫每個欄位。

> 若未啟用自動指派授權，表示只有使用者資料會同步處理。

![LinkedIn Learning 佈建](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> 若啟用自動指派授權，您需要記下應用程式執行個體及授權類型。 授權的指派採取先到先拿原則，一直到所有授權都指派完為止。

![LinkedIn Learning 佈建](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  按一下 [產生權杖]。 您應該會看到您的存取權杖顯示在存取權杖 欄位下。

6)  離開頁面之前，將您的存取權杖儲存至剪貼簿或電腦。

7) 接下來，登入 [Azure 入口網站](https://portal.azure.com)中，瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] 區段。

8) 如果您已經設定 LinkedIn Learning 單一登入，使用 [搜尋] 欄位搜尋您的 LinkedIn Learning 執行個體。 否則，請選取 [新增]，並在應用程式庫中搜尋 [LinkedIn Learning]。 從搜尋結果中選取 LinkedIn Learning，並將它新增至您的應用程式清單。

9)  選取您的 LinkedIn Learning 執行個體，然後選取 [佈建] 索引標籤。

10) 將 [佈建模式] 設定為 [自動]。

![LinkedIn Learning 佈建](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  填寫 [系統管理員認證] 底下的下列欄位：

* 在 [租用戶 URL] 欄位中輸入 https://api.linkedin.com。

* 在 [祕密權杖] 欄位中，輸入在步驟 1 產生的存取權杖，然後按一下 [測試連線]。

* 您應該會在入口網站的右上角看到成功通知。

12) 在 [通知電子郵件] 欄位中輸入應收到佈建錯誤通知的個人或群組之電子郵件地址，然後勾選下列核取方塊。

13) 按一下 [檔案] 。 

14) 在 [屬性對應] 區段中，檢閱將從 Azure AD 同步處理至 LinkedIn Learning 的使用者和群組屬性。 請注意，選取為 [比對] 屬性的屬性會用來比對 LinkedIn Learning 中的使用者帳戶和群組以進行更新作業。 選取 [儲存] 按鈕以認可任何變更。

![LinkedIn Learning 佈建](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) 若要啟用 LinkedIn Learning 的 Azure AD 佈建服務，在 [設定] 區段中，將 [佈建狀態] 變更為 [開啟]

16) 按一下 [檔案] 。 

這會啟動在 [使用者和群組] 區段中指派給 LinkedIn Learning 的任何使用者和/或群組之初始同步處理。 請注意，初始同步處理會比後續的同步處理花費較多時間執行，只要服務正在執行，這大約每 20 分鐘便會發生一次。 您可以使用 [同步處理詳細資料] 區段來監視進度，並連結到佈建活動報表，該報表描述您 LinkedIn Learning 應用程式上的佈建服務所執行之所有動作。


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
