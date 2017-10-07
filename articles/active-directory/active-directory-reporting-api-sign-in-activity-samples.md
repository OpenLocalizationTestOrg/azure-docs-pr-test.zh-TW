---
title: "aaaAzure Active Directory 登入活動報表 API 範例 |Microsoft 文件"
description: "如何 tooget 入門 hello Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory 登入活動報告 API 範例
本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。  
Azure AD 報告 api 還可讓您的 API tooaccess 登入活動資料使用程式碼或相關的工具。  
hello 本主題的範圍是您的範例程式碼 hello tooprovide**登入活動 API**。

請參閱：

* [稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊
* [開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。


## <a name="prerequisites"></a>必要條件
您可以使用本主題中的 hello 範例之前，您需要 toocomplete hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。  

## <a name="powershell-script"></a>PowerShell 指令碼
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a>執行 hello 指令碼
一次您編輯 hello 指令碼完成、 執行並確認該 hello 預期會傳回從 hello 稽核記錄報告資料。

hello 指令碼會傳回輸出 hello 登入 JSON 格式的報表。 它也會建立`SigninActivities.json`檔案以 hello 相同輸出。 您可以嘗試藉由修改 hello 指令碼 tooreturn 資料從其他報表和註解，您不需要 hello 輸出格式。

## <a name="next-steps"></a>後續步驟
* 您希望 toocustomize 本主題中的 hello 範例？ 簽出 hello[登入 Azure Active Directory 活動 API 參考](active-directory-reporting-api-sign-in-activity-reference.md)。 
* 如果您想要使用的完整概觀 toosee hello Azure Active Directory 報告 API，請參閱[入門 hello Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。
* 如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。  

