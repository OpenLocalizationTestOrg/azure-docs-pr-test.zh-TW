---
title: "aaaAzure Active Directory 稽核 API 參考 |Microsoft 文件"
description: "Tooget 以 hello Azure Active Directory 稽核應用程式開發介面的啟動方式"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Azure Active Directory 稽核 API 參考
本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。  
Azure AD 報告 api 還可讓您的 API tooaccess 稽核資料使用程式碼或相關的工具。
本主題的 hello 範圍是 tooprovide hello 的相關參考資訊**稽核 API**。

請參閱：

* [稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊

* [開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。


關於：

- 閱讀常見問題集，請參閱我們的[常見問題集](active-directory-reporting-faq.md) 

- 問題，請[提出支援票證](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>誰可以存取 hello 資料？
* Hello 安全性系統管理員或安全性 Reader 角色中的使用者
* 全域管理員
* 任何已授權 tooaccess hello API 的應用程式 （只會根據全域系統管理員權限，應用程式授權可以是安裝程式）

## <a name="prerequisites"></a>必要條件
透過此報告的順序 tooaccess 中 hello Reporting API，您必須具有：

* [Azure Active Directory Free 或更好的版本](active-directory-editions.md)
* 已完成的 hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。 

## <a name="accessing-hello-api"></a>存取 hello API
您可以存取此應用程式開發介面透過 hello[圖表總管](https://graphexplorer2.cloudapp.net)或以程式設計方式使用，例如 PowerShell。 PowerShell toocorrectly 解譯 hello AAD Graph REST 呼叫中使用的 OData 篩選器語法的您必須使用 hello 倒單引號 (也稱為： 抑音符號) 字元太 「 逸出"hello $ 字元。 hello 倒單引號字元做為[PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell toodo hello $ 字元，常值解譯，同時避免混淆做為 PowerShell 變數的名稱 (亦即： $filter)。

本主題的 hello 重點是在 hello 圖表總管。 如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-audit-samples.md#powershell-script)。

## <a name="api-endpoint"></a>API 端點
您可以存取此應用程式開發介面，使用下列 URI 的 hello:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

Hello hello Azure AD 稽核 API （使用 OData 分頁） 傳回的記錄數目沒有限制。
如需報告資料的保留限制，請參閱 [報告保留原則](active-directory-reporting-retention.md)。

這個呼叫會傳回批次中的 hello 資料。 每個批次的上限為 1000 筆記錄。  
tooget hello 下一個批次的記錄，以使用 hello 下一步 連結。 收到 hello 第一組傳回的記錄中的 hello skiptoken 資訊。 hello 跳過權杖會在 hello hello 結果集的結尾。  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>支援的篩選器
您可以縮小 hello 應用程式開發介面所傳回的記錄數目的篩選器的形式呼叫。  
登入應用程式開發介面支援的相關的資料，下列篩選器的 hello:

* **$top =\<傳回的記錄 toobe 數目\>** -toolimit hello 數傳回的記錄。 這是一項昂貴的作業。 如果您想要 tooreturn 數以千計的物件，則不應使用此篩選條件。     
* **$filter =\<您篩選陳述式\>** -toospecify，hello 為基礎，支援的篩選欄位，您有興趣的資料錄的 hello 類型

## <a name="supported-filter-fields-and-operators"></a>支援的篩選欄位和運算子
您有興趣的資料錄 toospecify hello 類型，您可以建置可包含一或多種 hello 下列篩選欄位的篩選陳述式：

* [activityDate](#activitydate) - 定義日期或日期範圍
* [類別](#category)-定義您想要 toofilter hello 分類。
* [activityStatus](#activitystatus) -定義 hello 活動狀態
* [activityType](#activitytype) -定義 hello 活動類型
* [活動](#activity)-hello 活動定義為字串  
* [動作項目/名稱](#actorname)-hello 演員姓名形式定義 hello 動作項目
* [動作項目/objectid](#actorobjectid) -hello 的執行者識別碼形式定義 hello 動作項目   
* [動作項目/upn](#actorupn) -hello 執行者的使用者主要名稱 (UPN) 形式定義 hello 動作項目 
* [目標/名稱](#targetname)-hello 演員姓名形式定義 hello 目標
* [目標/objectid](#targetobjectid) -hello 目標識別碼形式定義 hello 目標  
* [目標/upn](#targetupn) -hello 執行者的使用者主要名稱 (UPN) 形式定義 hello 動作項目   

- - -
### <a name="activitydate"></a>signinDateTime
**支援的運算子**：eq、ge、le、gt、lt

**範例**：

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**注意**：

datetime 應採用 UTC 格式

- - -
### <a name="category"></a>category

**支援的值**：

| 類別                         | 值     |
| :--                              | ---       |
| 核心目錄                   | 目錄 |
| 自助式密碼管理 | SSPR      |
| 自助式群組管理    | SSGM      |
| 帳戶佈建             | Sync      |
| 自動密碼變換      | 自動密碼變換 |
| 身分識別保護              | IdentityProtection |
| 受邀的使用者                    | 受邀的使用者 |
| MIM 服務                      | MIM 服務 |



**支援的運算子**：eq

**範例**：

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**支援的值**：

| 活動狀態 | 值 |
| :--             | ---   |
| 成功         | 0     |
| 失敗         | - 1   |

**支援的運算子**：eq

**範例**：

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**支援的運算子**：eq

**範例**：

    $filter=activityType eq 'User'    

**注意**：

區分大小寫

- - -
### <a name="activity"></a>activity
**支援的運算子**：eq、contains、startsWith

**範例**：

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**注意**：

區分大小寫

- - -
### <a name="actorname"></a>actor/name
**支援的運算子**：eq、contains、startsWith

**範例**：

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**注意**：

不區分大小寫

- - -
### <a name="actorobjectid"></a>actor/objectid
**支援的運算子**：eq

**範例**：

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/name
**支援的運算子**：eq、contains、startsWith

**範例**：

    $filter=targets/any(t: t/name eq 'some name')    

**注意**：

不區分大小寫

- - -
### <a name="targetupn"></a>target/upn
**支援的運算子**：eq、startsWith

**範例**：

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**注意**：

* 不區分大小寫
* 查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity 時，需要 tooadd hello 完整的命名空間

- - -
### <a name="targetobjectid"></a>target/objectid
**支援的運算子**：eq

**範例**：

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>actor/upn
**支援的運算子**：eq、startsWith

**範例**：

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**注意**：

* 不區分大小寫 
* 查詢 Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity 時，需要 tooadd hello 完整的命名空間

- - -
## <a name="next-steps"></a>後續步驟
* 您想 toosee 範例篩選的系統活動？ 簽出 hello [Azure Active Directory 稽核 API 範例](active-directory-reporting-api-audit-samples.md)。
* 您想深入了解 hello Azure AD 報告 API tooknow 嗎？ 請參閱[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。

