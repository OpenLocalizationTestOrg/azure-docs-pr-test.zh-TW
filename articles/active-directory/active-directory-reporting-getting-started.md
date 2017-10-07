---
title: "Azure Active Directory 報告：開始使用 | Microsoft Docs"
description: "列出 hello 各種可用的報表，在 Azure Active Directory 報告"
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
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>開始使用 Azure Active Directory 報告
## <a name="what-it-is"></a>內容
Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。 以下是一份包含 hello 報表：

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
hello 報告管線包含三個主要步驟。 每次使用者登入，或進行驗證，hello 會發生下列狀況：

* 首先，hello 使用者已驗證 （成功或失敗），並 hello 結果會儲存在 hello Azure Active Directory 服務資料庫。
* 每隔一段固定時間，就會處理所有最近的登入。 此時，我們的安全性和異常活動演算法會搜尋所有最近的登入找出是否有可疑的活動。
* 經過處理後，hello 報表會寫入、 快取，而且在 hello Azure 傳統入口網站中提供。

### <a name="report-generation-times"></a>報告產生時間
Toohello 大型磁碟區的驗證與登入處理 hello Azure AD 的平台，因為 hello 最近登入處理的平均，1 小時前。 在罕見的情況下，它可能會佔用 too8 小時 tooprocess hello 最近登入。

您可以藉由檢查 hello 說明文字，每個報表的 hello 頂端找到 hello 最近處理登入。

![在每個報表 hello 最上方的說明文字](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="getting-started"></a>開始使用
### <a name="sign-into-hello-azure-classic-portal"></a>登入 hello Azure 傳統入口網站
首先，您將需要 toosign 到 hello [Azure 傳統入口網站](https://manage.windowsazure.com)身為全域或相容性的系統管理員。 您也必須有 Azure 訂用帳戶服務管理員或共同管理員，或使用 hello 」 存取 tooAzure AD"Azure 訂用帳戶。

### <a name="navigate-tooreports"></a>瀏覽 tooReports
tooview 報表瀏覽 toohello 在 hello 頂端目錄的 [報告] 索引標籤。

如果這是您第一次檢視 hello 報表，您必須 tooagree tooa 對話方塊之前，您可以檢視 hello 報告。 這是已接受您的組織 tooview 中的管理員 tooensure 這項資料可能會被視為一些國家/地區的私人資訊。

![對話方塊](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>瀏覽每個報告
收集每個報表 toosee hello 資料瀏覽，再處理 hello 登入。 您可以找到[所有 hello 報告以下清單](active-directory-reporting-guide.md)。

![所有報告](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Hello 報表下載為 CSV
每個報告可以下載為 CSV (逗號分隔值) 檔案。 您可以使用 Excel、 power Bi 或協力廠商架構分析程式 toofurther 分析資料中的這些檔案。

toodownload 任何報告以 csv 格式中，瀏覽 toohello 報表，然後按一下 [下載] 底部 hello。

![[下載] 按鈕](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="next-steps"></a>後續步驟
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>自訂異常登入活動的警示
瀏覽您的目錄 toohello 「 設定 」 索引標籤。

捲動 toohello 「 通知 」 一節。

啟用或停用 hello [異常的登入的電子郵件通知] 區段。

![hello 通知 區段](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Hello 與整合 Azure AD 報告 API
請參閱[入門 hello Reporting API](active-directory-reporting-api-getting-started.md)。

### <a name="engage-multi-factor-authentication-on-users"></a>對使用者採取 Multi-Factor Authentication
在報告中選取使用者。

按一下 在 hello 囉 」 畫面底部的 hello 」 啟用 MFA 」 按鈕。

![在 hello 囉 」 畫面底部的 hello Multi-factor Authentication 按鈕](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

## <a name="learn-more"></a>詳細資訊
### <a name="audit-events"></a>稽核事件
深入了解哪些事件稽核 hello 目錄中[Azure Active Directory 報告稽核事件](active-directory-reporting-audit-events.md)。

### <a name="api-integration"></a>API 整合
請參閱[入門 hello Reporting API](active-directory-reporting-api-getting-started.md)和 hello [API 參考文件](https://msdn.microsoft.com/library/azure/mt126081.aspx)。

### <a name="get-in-touch"></a>取得聯繫
如有任何意見回饋、需要說明，或有任何問題，請寄送電子郵件到 [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) 。

> [!TIP]
> 如需有關 Azure AD 報告的更多文件，請參閱 [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)。
> 
> 

