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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="9191d-103">Azure Active Directory 登入活動報告 API 範例</span><span class="sxs-lookup"><span data-stu-id="9191d-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="9191d-104">本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="9191d-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="9191d-105">Azure AD 報告 api 還可讓您的 API tooaccess 登入活動資料使用程式碼或相關的工具。</span><span class="sxs-lookup"><span data-stu-id="9191d-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="9191d-106">hello 本主題的範圍是您的範例程式碼 hello tooprovide**登入活動 API**。</span><span class="sxs-lookup"><span data-stu-id="9191d-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="9191d-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="9191d-107">See:</span></span>

* <span data-ttu-id="9191d-108">[稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="9191d-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="9191d-109">[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9191d-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9191d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9191d-110">Prerequisites</span></span>
<span data-ttu-id="9191d-111">您可以使用本主題中的 hello 範例之前，您需要 toocomplete hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="9191d-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="9191d-112">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="9191d-112">PowerShell script</span></span>
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




## <a name="executing-hello-script"></a><span data-ttu-id="9191d-113">執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="9191d-113">Executing hello script</span></span>
<span data-ttu-id="9191d-114">一次您編輯 hello 指令碼完成、 執行並確認該 hello 預期會傳回從 hello 稽核記錄報告資料。</span><span class="sxs-lookup"><span data-stu-id="9191d-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="9191d-115">hello 指令碼會傳回輸出 hello 登入 JSON 格式的報表。</span><span class="sxs-lookup"><span data-stu-id="9191d-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="9191d-116">它也會建立`SigninActivities.json`檔案以 hello 相同輸出。</span><span class="sxs-lookup"><span data-stu-id="9191d-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="9191d-117">您可以嘗試藉由修改 hello 指令碼 tooreturn 資料從其他報表和註解，您不需要 hello 輸出格式。</span><span class="sxs-lookup"><span data-stu-id="9191d-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9191d-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9191d-118">Next Steps</span></span>
* <span data-ttu-id="9191d-119">您希望 toocustomize 本主題中的 hello 範例？</span><span class="sxs-lookup"><span data-stu-id="9191d-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="9191d-120">簽出 hello[登入 Azure Active Directory 活動 API 參考](active-directory-reporting-api-sign-in-activity-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="9191d-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="9191d-121">如果您想要使用的完整概觀 toosee hello Azure Active Directory 報告 API，請參閱[入門 hello Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9191d-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="9191d-122">如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="9191d-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

