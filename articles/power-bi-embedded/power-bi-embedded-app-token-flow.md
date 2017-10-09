---
title: "aaaAuthenticating 並向 Power BI Embedded 授權"
description: "使用 Power BI Embedded 驗證和授權"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>使用 Power BI Embedded 驗證和授權

hello 內嵌 Power BI 服務會使用**金鑰**和**應用程式權杖**進行驗證和授權，而不要使用明確的使用者驗證。 在此模型中，您的應用程式會管理使用者的驗證與授權。 必要時，您的應用程式會建立，並傳送 hello 應用程式權杖，告訴我們服務 toorender hello 要求的報表。 這項設計並不需要您的應用程式 toouse Azure Active Directory 進行使用者驗證和授權，雖然您仍然可以。

## <a name="two-ways-tooauthenticate"></a>兩種方式 tooauthenticate

**金鑰** - 您可以針對所有 Power BI Embedded REST API 呼叫使用金鑰。 hello 金鑰可以在 hello **Azure 入口網站**按一下**所有設定**然後**存取金鑰**。 一律將您的金鑰視為密碼。 這些有特定的工作區集合呼叫任何 REST API 的權限 toomake。

toouse 在 REST 呼叫的索引鍵新增下列授權標頭的 hello:            

    Authorization: AppKey {your key}

**應用程式權杖** - 應用程式權杖用於所有內嵌的要求。 它們是設計的 toobe 執行用戶端，所以限制 tooa 單一報表和它的最佳作法 tooset 到期時間。

應用程式權杖是 JWT (JSON Web 權杖)，由您的其中一個金鑰簽署。

您的應用程式的權杖可以包含下列宣告 hello:

| 宣告 | 說明 |
| --- | --- |
| **ver** |hello hello 應用程式權杖版本。 0.2.0 是 hello 目前版本。 |
| **aud** |hello 預期收件者的 hello 語彙基元。 對於 Power BI Embedded，使用：“https://analysis.windows.net/powerbi/api”。 |
| **iss** |字串，表示權杖 hello hello 應用程式。 |
| **type** |正在建立的應用程式語彙基元 hello 型別。 目前僅支援 hello 類型是**內嵌**。 |
| **wcn** |工作區集合名稱 hello 語彙基元所發出。 |
| **wid** |工作區識別碼 hello 語彙基元所發出。 |
| **rid** |報表識別碼 hello 語彙基元所發出。 |
| **username** (選擇性) |這是字串，可協助您識別 hello 使用者套用 RLS 規則時使用 rls。 |
| **角色** (選擇性) |字串，包含 hello 角色 tooselect 套用資料列層級安全性規則時。 如果傳遞多個角色，應該將它們傳遞為字串陣列。 |
| **scp** (選擇性) |字串，包含 hello 權限範圍。 如果傳遞多個角色，應該將它們傳遞為字串陣列。 |
| **exp** (選擇性) |指出 hello 時間中的 hello token 會過期。 這些項目應該傳遞為 Unix 時間戳記。 |
| **nbf** (選擇性) |指出在哪些 hello 語彙基元開始生效時的 hello 時間。 這些項目應該傳遞為 Unix 時間戳記。 |

範例應用程式權杖看起來像這樣：

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

解碼時，看起來像這樣：

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

有方法可以在 hello 簡化建立 apptokens 的 Sdk 中使用。 例如，適用於.NET 您可以查看 hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken)類別和 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)方法。

Hello.NET SDK，您可以使用參照太[範圍](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)。

## <a name="scopes"></a>範圍

當使用內嵌語彙基元時，您可能想 hello 資源存取權給予 toorestrict 使用量。 為此，您可以產生具有範圍權限的權杖。

hello 如下的 Power BI Embedded hello 可用的領域。

|Scope|說明|
|---|---|
|Dataset.Read|提供的權限 tooread hello 指定資料集。|
|Dataset.Write|提供指定的權限 toowrite toohello 資料集。|
|Dataset.ReadWrite|提供的權限 tooread 」 和 「 寫入 toohello 指定資料集。|
|Report.Read|提供的權限 tooview hello 指定報表。|
|Report.ReadWrite|提供的權限 tooview 和編輯 hello 指定的報表。|
|Workspace.Report.Create|提供的權限 toocreate 內 hello 指定新的報表 工作區。|
|Workspace.Report.Copy|提供的權限 tooclone 內 hello 指定現有的報表 工作區。|

您可以使用類似 hello 下列 hello 範圍之間的空格提供多個領域。

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**必要宣告 - 範圍**

scp: {scopesClaim} scopesClaim 可以是字串或字串陣列，您會看到 hello 允許權限 tooworkspace 資源 （報表、 資料集）

已解碼的權杖中，與範圍定義，看起來類似 toohello 下列。

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>作業和範圍

|作業|目標資源|權杖權限|
|---|---|---|
|根據資料集建立新的報告 (在記憶體內部)。|Dataset|Dataset.Read|
|建立新的報表資料集為基礎的 （記憶體），並儲存 hello 報表。|Dataset|* Dataset.Read<br>* Workspace.Report.Create|
|檢視和瀏覽/編輯現有報告 (在記憶體內部)。 Report.Read 暗指 Dataset.Read。 這不會允許權限 toosave 編輯。|報告|Report.Read|
|編輯並儲存現有報告。|報告|Report.ReadWrite|
|儲存報告複本 (另存新檔)。|報告|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>以下是 hello 流程的運作方式
1. 複製 hello API 金鑰 tooyour 應用程式。 您可以在取得 hello 金鑰**Azure 入口網站**。
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. 權杖判斷提示宣告，並有到期時間。
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. 以 API 存取金鑰簽署權杖。
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. 使用者要求報表時 tooview。
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. 以 API 存取金鑰驗證權杖。
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded 傳送報表 toouser。
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

之後**Power BI Embedded**報表 toohello 使用者，會傳送 hello 使用者可以檢視在自訂應用程式中的 hello 報表。 例如，如果您匯入 hello[分析銷售資料 PBIX 範例](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix)，hello 範例 web 應用程式會看起來像這樣：

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>另請參閱

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[開始使用 Microsoft Power BI Embedded 範例](power-bi-embedded-get-started-sample.md)  
[Microsoft Power BI Embedded 常見案例](power-bi-embedded-scenarios.md)  
[開始使用 Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[PowerBI-CSharp Git 存放庫](https://github.com/Microsoft/PowerBI-CSharp)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

