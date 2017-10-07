---
title: "aaaFind 活動報告的 hello Azure 入口網站 |Microsoft 文件"
description: "了解 Azure Active Directory 活動 toofind hello Azure 入口網站中的報告方式。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: d93521f8-dc21-4feb-aaff-4bb300f04812
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: f8d7a968403e10ccc5319f27fedad38b1553ded0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-activity-reports-in-hello-azure-portal"></a>在 [hello Azure 入口網站中尋找活動報告

如果您要從 Azure 傳統入口網站 toohello hello 移動 [Azure 入口網站，您會取得 Azure Active Directory (Azure AD) 活動記錄在新的外觀。 中的最近[部落格文章](https://blogs.technet.microsoft.com/enterprisemobility/2016/11/08/azuread-weve-just-turned-on-detailed-auditing-and-sign-in-logs-in-the-new-azure-portal/)，我們會說明如何查看活動記錄中的 hello 資源依據您進行 hello Azure 入口網站中的 hello 內容。 在本文中，我們說明 toofind 報告的方式，在 [hello hello Azure 入口網站中的 Azure 傳統入口網站中使用。

## <a name="whats-new"></a>新功能

Hello Azure 傳統入口網站中的報表分為類別：

1.  安全性報告
2.  活動報告
3.  整合式應用程式報告

### <a name="activity-and-integrated-app-reports"></a>活動和整合式應用程式報告

針對以內容為主 hello Azure 入口網站中的報表，現有的報表會合併到單一檢視。 單一基礎的 API，可提供 hello 資料 toohello 檢視。

此檢視 hello toosee **Azure Active Directory**刀鋒視窗底下**活動**，選取**稽核記錄檔**。

![稽核記錄](./media/active-directory-reporting-migration/482.png "稽核記錄")

在此檢視將會合併 hello 下列報表：

-   稽核報告
-   密碼重設活動
-   密碼重設註冊活動
-   自助式群組活動
-   Office365 群組名稱變更
-   帳戶佈建活動
-   密碼變換狀態
-   帳戶佈建錯誤


hello 應用程式使用情況報表已經增強，而且會包含在 hello**登入**檢視。 此檢視 hello toosee **Azure Active Directory**刀鋒視窗底下**活動**，選取**登入**。

![登入檢視](./media/active-directory-reporting-migration/483.png "登入檢視")

hello**登入**檢視包含所有的使用者登入。您可以使用此資訊 tooget 應用程式使用方式資訊。 您也可以檢視應用程式使用資訊在 hello**企業應用程式**概觀，請在 [hello**管理**> 一節。

![企業應用程式](./media/active-directory-reporting-migration/484.png "企業應用程式")

## <a name="access-a-specific-report"></a>存取特定報告

雖然 hello Azure 入口網站提供了單一檢視，您也可以查看特定報表。

### <a name="audit-logs"></a>稽核記錄檔

在回應 toocustomer 意見反應，在 hello Azure 入口網站，您可以使用進階篩選 tooaccess hello 您想要的資料。 您可以使用一個篩選條件*活動類別*，其中會列出 hello 不同類型的活動記錄在 Azure AD 中。 toonarrow 結果 toowhat 想要您可以選取類別。

例如，如果您想要只在活動相關的 tooself 服務密碼重設，您可以選擇 hello**自助密碼管理**類別目錄。 您看到的 hello 類別取決於您工作所在的 hello 資源。  

![Hello 篩選稽核記錄檔] 頁面上的類別目錄選項](./media/active-directory-reporting-migration/06.png "hello 篩選稽核記錄檔] 頁面上的類別目錄選項")

活動類別包括︰

- 核心目錄
- 自助式密碼管理
- 自助式群組管理
- 帳戶佈建

### <a name="application-usage"></a>應用程式使用情況

tooview 的相關詳細資料或單一應用程式中，所有應用程式的應用程式使用情形下**活動**，選取**登入**。 toonarrow hello 結果，您可以篩選使用者或應用程式名稱。

![[篩選登入事件] 頁面](./media/active-directory-reporting-migration/07.png "[篩選登入事件] 頁面")

### <a name="security-reports"></a>安全性報告

#### <a name="azure-ad-anomalous-activity-reports"></a>Azure AD 異常活動報告

Azure AD 異常活動的安全性已合併的 tooprovide hello Azure 傳統入口網站的報告。 您有一個中央檢視。 此檢視顯示 Azure AD 可以偵測及作為報告依據的所有安全性相關風險事件。

hello 下表列出 hello Azure AD 異常活動安全性報表和 hello Azure 入口網站中的對應風險事件類型。

| Azure AD 異常活動報告 |  Identity Protection 風險事件類型|
| :--- | :--- |
| 認證外洩的使用者 | 認證外洩 |
| 異常的登入活動 | 不可能的旅遊 tooatypical 位置 |
| 從可能受感染的裝置登入 | 從受感染的裝置登入|
| 從不明來源登入 | 從匿名 IP 位址登入 |
| 從具有可疑活動的 IP 位址登入 | 從具有可疑活動的 IP 位址登入 |
| - | 從不熟悉的位置登入 |

hello 下列 Azure AD 異常活動安全性報告不會包含為 hello Azure 入口網站中的風險事件：

* 在多次失敗後登入
* 從多個地理區域登入

這些報告就 hello Azure 傳統入口網站中仍然可用，但是將在未來的 hello 被取代。

如需詳細資訊，請參閱 [Azure Active Directory 風險事件](active-directory-identity-protection-risk-events.md)。  


#### <a name="detected-risk-events"></a>偵測到的風險事件

在 hello Azure 入口網站，您可以存取有關偵測到的風險事件報告 hello **Azure Active Directory**刀鋒視窗底下**安全性**。 偵測到的風險事件會追蹤在 hello 下列報表：   

- 有風險的使用者
- 有風險的登入

![安全性報告](./media/active-directory-reporting-migration/04.png "安全性報告")

如需安全性報告的詳細資訊，請參閱︰

- [使用者在風險中檢視 hello Azure Active Directory 入口網站的安全性報表](active-directory-reporting-security-user-at-risk.md)
- [風險 hello Azure Active Directory 入口網站中的登入報表](active-directory-reporting-security-risky-sign-ins.md)


## <a name="activity-reports-in-hello-azure-classic-portal-vs-hello-azure-portal"></a>在 [hello 與 hello Azure 入口網站的 Azure 傳統入口網站中的活動報告

本節中的 hello 表格列出 hello Azure 傳統入口網站中的現有報表。 它也會說明如何取得 hello hello Azure 入口網站中的相同資訊。

tooview 所有稽核資料，請在 [hello **Azure Active Directory**刀鋒視窗底下**活動**，跳過**稽核記錄檔**。

![稽核記錄](./media/active-directory-reporting-migration/61.png "稽核記錄")

| Azure 傳統入口網站                 | toofind hello Azure 入口網站中                                                         |
| ---                                  | ---                                                                        |
| 稽核記錄檔                           | 選取 [核心目錄] 做為 [活動類別]。                       |
| 密碼重設活動              | 選取 [自助式密碼管理] 做為 [活動分類]。 |
| 密碼重設註冊活動 | 選取 [自助式密碼管理] 做為 [活動分類]。     |
| 自助式群組活動         | 選取 [自助式群組管理] 做為 [活動類別]。        |
| 帳戶佈建活動        | 選取 [帳戶使用者佈建] 做為 [活動類別]。         |
| 密碼變換狀態             | 選取 [自動應用程式密碼變換] 做為 [活動類別]。      |
| 帳戶佈建錯誤          | 選取 [帳戶使用者佈建] 做為 [活動類別]。        |
| Office365 群組名稱變更         | 選取 [自助式密碼管理] 做為 [活動分類]。 選取 [群組] 做為 [活動資源類型]。 選取 [O365 群組] 做為 [活動來源]。|

tooview hello**應用程式使用情形**報表，在 [hello **Azure Active Directory**刀鋒視窗底下**管理**，選取**企業應用程式**，然後選取**登入**。


![企業應用程式登入報告](./media/active-directory-reporting-migration/199.png "企業應用程式登入報告")

## <a name="next-steps"></a>後續步驟

如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。
