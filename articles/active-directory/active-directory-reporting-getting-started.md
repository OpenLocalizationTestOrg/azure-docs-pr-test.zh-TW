---
title: "Azure Active Directory 報告：開始使用 | Microsoft Docs"
description: "在 Azure Active Directory 報告列出各種可用的報告"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5cd1ae6196d9cd63f97dc9d302442280ece23e40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>開始使用 Azure Active Directory 報告
## <a name="what-it-is"></a>內容
Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。 以下是包含的報告清單：

### <a name="security-reports"></a>安全性報告
* 從不明來源登入
* 在多次失敗後登入
* 從多個地理區域登入
* 從具有可疑活動的 IP 位址登入
* 異常的登入活動
* 從可能受感染的裝置登入
* 具有異常登入活動的使用者

### <a name="activity-reports"></a>活動報告
* 應用程式使用情況：摘要
* 應用程式使用情況：詳細
* 應用程式儀表板
* 帳戶佈建錯誤
* 個別使用者裝置
* 個別使用者活動
* 群組活動報告
* 密碼重設登錄活動報告
* 密碼重設活動

### <a name="audit-reports"></a>稽核報告
* 目錄稽核報告

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="how-it-works"></a>運作方式
### <a name="reporting-pipeline"></a>報告管線
報告管線包含三個主要步驟。 每次使用者登入或進行驗證時，就會發生以下狀況：

* 首先，使用者會經過驗證 (成功或失敗)，結果會儲存在 Azure Active Directory 服務資料庫。
* 每隔一段固定時間，就會處理所有最近的登入。 此時，我們的安全性和異常活動演算法會搜尋所有最近的登入找出是否有可疑的活動。
* 處理之後，就會寫入報告、快取報告，然後在 Azure 傳統入口網站中提供報告。

### <a name="report-generation-times"></a>報告產生時間
由於 Azure AD 平台需處理大量的驗證和登入，所處理的最近登入平均而言為過去一小時。 在罕見的情況下，可能需要花費多達 8 小時處理最近的登入。

您可以查看每個報告頂端的說明文字，找到最近處理的登入。

![每個報告頂端的說明文字](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="getting-started"></a>開始使用
### <a name="sign-into-the-azure-classic-portal"></a>登入 Azure 傳統入口網站
首先，您必須以全域或相容性管理員身分登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。 您也必須是 Azure 訂用帳戶服務管理員或共同管理員，或使用「存取 Azure AD」的 Azure 訂用帳戶。

### <a name="navigate-to-reports"></a>瀏覽至報告
若要檢視報告，請瀏覽至目錄頂端的 [報告] 索引標籤。

如果這是您第一次檢視報告，您必須先同意對話方塊，才能檢視報告。 這是為了確保在您的組織中可接受讓管理員檢視這項資料，在某些國家/地區，這些資料可能會被視為隱私資訊。

![對話方塊](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>瀏覽每個報告
瀏覽每個報告以查看收集的資料，以及處理的登入。 您可以 [在此找到所有報告的清單](active-directory-reporting-guide.md)。

![所有報告](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a>下載報告為 CSV
每個報告可以下載為 CSV (逗號分隔值) 檔案。 您可以在 Excel、PowerBI 或協力廠商分析程式中使用這些檔案，進一步分析您的資料。

若要下載任何報告為 CSV，請瀏覽至報告並按一下底部的 [下載]。

![[下載] 按鈕](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="next-steps"></a>後續步驟
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>自訂異常登入活動的警示
瀏覽至您目錄的 [設定] 索引標籤。

捲動到 [通知] 區段。

啟用或停用 [惡意登入的電子郵件通知] 區段。

![[通知] 區段](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a>與 Azure AD 報告 API 整合
請參閱 [開始使用報告 API](active-directory-reporting-api-getting-started.md)。

### <a name="engage-multi-factor-authentication-on-users"></a>對使用者採取 Multi-Factor Authentication
在報告中選取使用者。

按一下畫面底部的 [啟用 MFA] 按鈕。

![畫面底部的 [Multi-Factor Authentication] 按鈕](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="learn-more"></a>詳細資訊
### <a name="audit-events"></a>稽核事件
如需了解目錄中的哪些事件會進行稽核，請參閱 [Azure Active Directory 報告稽核事件](active-directory-reporting-audit-events.md)。

### <a name="api-integration"></a>API 整合
請參閱[開始使用報告 API](active-directory-reporting-api-getting-started.md) 和 [API 參考文件](https://msdn.microsoft.com/library/azure/mt126081.aspx)。

### <a name="get-in-touch"></a>取得聯繫
如有任何意見回饋、需要說明，或有任何問題，請寄送電子郵件到 [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) 。

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

