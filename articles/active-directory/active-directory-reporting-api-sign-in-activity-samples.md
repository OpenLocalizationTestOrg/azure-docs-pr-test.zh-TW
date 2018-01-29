---
title: "Azure Active Directory 登入活動報告 API 範例 | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 158f121880dbc1fc1495c8599367502ffd93ce20
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2018
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory 登入活動報告 API 範例
本主題是 Azure Active Directory 報告 API 相關主題集合的一部分。  
Azure AD 報告提供的 API 可讓您使用程式碼或相關工具來存取登入活動資料。  
本主題的範疇是為您提供 **登入活動 API**的範例程式碼。

請參閱：

* [稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊
* [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md) 以取得報告 API 的詳細資訊。


## <a name="prerequisites"></a>先決條件
您必須先完成 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)，才能使用本主題中的範例。  

## <a name="powershell-script"></a>PowerShell 指令碼
    # This script will require the Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a>執行指令碼
完成指令碼編輯後，加以執行並確認從稽核記錄報告傳回預期的資料。

指令碼會以 JSON 格式傳回登入報告的輸出。 它也會建立具有相同輸出的 `SigninActivities.json` 檔案。 您可透過修改指令碼以從其他報告傳回資料來進行實驗，以及取消註解您不需要的輸出格式。

## <a name="next-steps"></a>後續步驟
* 您要自訂本主題中的範例嗎？ 請查看 [Azure Active Directory 登入活動 API 參考](active-directory-reporting-api-sign-in-activity-reference.md)。 
* 如果您想要查看使用 Azure Active Directory 報告 API 的完整概觀，請參閱 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。
* 如果您想要深入了解 Azure Active Directory 報告，請參閱 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。  

