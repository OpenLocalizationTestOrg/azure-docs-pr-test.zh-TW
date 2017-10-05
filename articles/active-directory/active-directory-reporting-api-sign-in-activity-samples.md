---
title: "Azure Active Directory 登入活動報告 API 範例 | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 報告 API"
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
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="943fe-103">Azure Active Directory 登入活動報告 API 範例</span><span class="sxs-lookup"><span data-stu-id="943fe-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="943fe-104">本主題是 Azure Active Directory 報告 API 相關主題集合的一部分。</span><span class="sxs-lookup"><span data-stu-id="943fe-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="943fe-105">Azure AD 報告提供的 API 可讓您使用程式碼或相關工具來存取登入活動資料。</span><span class="sxs-lookup"><span data-stu-id="943fe-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="943fe-106">本主題的範疇是為您提供 **登入活動 API**的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="943fe-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="943fe-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="943fe-107">See:</span></span>

* <span data-ttu-id="943fe-108">[稽核記錄](active-directory-reporting-azure-portal.md#activity-reports)以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="943fe-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="943fe-109">[開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md) 以取得報告 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="943fe-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="943fe-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="943fe-110">Prerequisites</span></span>
<span data-ttu-id="943fe-111">您必須先完成 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)，才能使用本主題中的範例。</span><span class="sxs-lookup"><span data-stu-id="943fe-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="943fe-112">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="943fe-112">PowerShell script</span></span>
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




## <a name="executing-the-script"></a><span data-ttu-id="943fe-113">執行指令碼</span><span class="sxs-lookup"><span data-stu-id="943fe-113">Executing the script</span></span>
<span data-ttu-id="943fe-114">完成指令碼編輯後，加以執行並確認從稽核記錄報告傳回預期的資料。</span><span class="sxs-lookup"><span data-stu-id="943fe-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="943fe-115">指令碼會以 JSON 格式傳回登入報告的輸出。</span><span class="sxs-lookup"><span data-stu-id="943fe-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="943fe-116">它也會建立具有相同輸出的 `SigninActivities.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="943fe-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="943fe-117">您可透過修改指令碼以從其他報告傳回資料來進行實驗，以及取消註解您不需要的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="943fe-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="943fe-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="943fe-118">Next Steps</span></span>
* <span data-ttu-id="943fe-119">您要自訂本主題中的範例嗎？</span><span class="sxs-lookup"><span data-stu-id="943fe-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="943fe-120">請查看 [Azure Active Directory 登入活動 API 參考](active-directory-reporting-api-sign-in-activity-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="943fe-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="943fe-121">如果您想要查看使用 Azure Active Directory 報告 API 的完整概觀，請參閱 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="943fe-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="943fe-122">如果您想要深入了解 Azure Active Directory 報告，請參閱 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="943fe-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

