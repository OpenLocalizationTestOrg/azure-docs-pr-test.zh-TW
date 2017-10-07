---
title: "aaaAzure Active Directory 登入活動報表 API 參考 |Microsoft 文件"
description: "Hello Azure Active Directory 登入活動報表應用程式開發介面參考"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Azure Active Directory 登入活動報告 API 參考
本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。  
Azure AD 報告 api 還可讓您的 API tooaccess 登入活動報表資料使用程式碼或相關的工具。
本主題的 hello 範圍是 tooprovide hello 的相關參考資訊**登入活動報表 API**。

請參閱：

* [登入活動](active-directory-reporting-azure-portal.md#activity-reports) 以取得詳細概念資訊
* [開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。


## <a name="who-can-access-hello-api-data"></a>誰可以存取 hello API 資料？
* 使用者和 hello 安全性系統管理員或安全性 Reader 角色中的服務主體
* 全域管理員
* 任何已授權 tooaccess hello API 的應用程式 （只會根據全域系統管理員權限，應用程式授權可以是安裝程式）

對於應用程式 tooaccess 安全性應用程式開發介面登入事件，例如使用下列 PowerShell tooadd hello 應用程式服務主體到 hello 安全性讀取者角色的 hello tooconfigure 存取

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>必要條件
tooaccess hello 報告應用程式開發介面，您必須透過此報告：

* [Azure Active Directory Premium P1 或 P2 版本](active-directory-editions.md)
* 已完成的 hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。 

## <a name="accessing-hello-api"></a>存取 hello API
您可以存取此應用程式開發介面透過 hello[圖表總管](https://graphexplorer2.cloudapp.net)或以程式設計方式使用，例如 PowerShell。 PowerShell toocorrectly 解譯 hello AAD Graph REST 呼叫中使用的 OData 篩選器語法的您必須使用 hello 倒單引號 (也稱為： 抑音符號) 字元太 「 逸出"hello $ 字元。 hello 倒單引號字元做為[PowerShell 的逸出字元](https://technet.microsoft.com/library/hh847755.aspx)，讓 PowerShell toodo hello $ 字元，常值解譯，同時避免混淆做為 PowerShell 變數的名稱 (亦即： $filter)。

本主題的 hello 重點是在 hello 圖表總管。 如需 PowerShell 範例，請參閱此 [PowerShell 指令碼](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script)。

## <a name="api-endpoint"></a>API 端點
您可以存取此應用程式開發介面，使用下列基底 URI 的 hello:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Toohello 磁碟區的資料，因為這個 API 已傳回記錄的 1 百萬個的限制。 

這個呼叫會傳回批次中的 hello 資料。 每個批次的上限為 1000 筆記錄。  
tooget hello 下一個批次的記錄，以使用 hello 下一步 連結。 取得 hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello 第一組傳回的記錄資訊。 hello 跳過權杖會在 hello hello 結果集的結尾。  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>支援的篩選器
您可以縮小 hello 應用程式開發介面所傳回的記錄數目的篩選器的形式呼叫。  
登入應用程式開發介面支援的相關的資料，下列篩選器的 hello:

* **$top =\<傳回的記錄 toobe 數目\>** -toolimit hello 數傳回的記錄。 這是一項昂貴的作業。 如果您想要 tooreturn 數以千計的物件，則不應使用此篩選條件。  
* **$filter =\<您篩選陳述式\>** -toospecify，hello 為基礎，支援的篩選欄位，您有興趣的資料錄的 hello 類型

## <a name="supported-filter-fields-and-operators"></a>支援的篩選欄位和運算子
您有興趣的資料錄 toospecify hello 類型，您可以建置可包含一或多種 hello 下列篩選欄位的篩選陳述式：

* [signinDateTime](#signindatetime) - 定義日期或日期範圍
* [userId](#userid) -定義特定的使用者基礎 hello 使用者的識別碼。
* [userPrincipalName](#userprincipalname) -定義特定的使用者基礎 hello 使用者的使用者主體名稱 (UPN)
* [appId](#appid) -定義特定的應用程式基礎 hello 應用程式的識別碼
* [appDisplayName](#appdisplayname) -定義特定的應用程式基礎 hello 應用程式的顯示名稱
* [loginStatus](#loginStatus) -定義 hello hello 登入狀態 (成功 / 失敗)

> [!NOTE]
> 使用圖表總管，當您 hello 需要 toouse hello 正確每個字母的案例是篩選欄位。
> 
> 

toonarrow hello hello 傳回的資料範圍下，您可以建立 hello 支援篩選和篩選欄位的組合。 例如，hello 下列陳述式會傳回 hello 年 7 月 6 日完成 2016 年 7 月 1 日到 2016年之間的前 10 筆記錄：

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**支援的運算子**：eq、ge、le、gt、lt

**範例**：

使用特定日期

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



使用日期範圍    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**注意**：

hello datetime 參數應該是以 hello UTC 格式 

- - -
### <a name="userid"></a>userId
**支援的運算子**：eq

**範例**：

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**注意**：

使用者識別碼 hello 值是字串值

- - -
### <a name="userprincipalname"></a>userPrincipalName
**支援的運算子**：eq

**範例**：

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**注意**：

userPrincipalName hello 值是字串值

- - -
### <a name="appid"></a>appId
**支援的運算子**：eq

**範例**：

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**注意**：

hello appId 值是字串值

- - -
### <a name="appdisplayname"></a>appDisplayName
**支援的運算子**：eq

**範例**：

    $filter=appDisplayName+eq+'Azure+Portal' 


**注意**：

appDisplayName hello 值是字串值

- - -
### <a name="loginstatus"></a>loginStatus
**支援的運算子**：eq

**範例**：

    $filter=loginStatus+eq+'1'  


**注意**：

有兩個選項的 hello loginStatus: 0-成功，1-失敗

- - -
## <a name="next-steps"></a>後續步驟
* 您想 toosee 範例已篩選的登入活動？ 簽出 hello [Azure Active Directory 登入活動報表 API 範例](active-directory-reporting-api-sign-in-activity-samples.md)。
* 您想深入了解 hello Azure AD 報告 API tooknow 嗎？ 請參閱[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。

