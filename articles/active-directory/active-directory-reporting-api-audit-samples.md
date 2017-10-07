---
title: "aaaAzure Active Directory 報告稽核 API 範例 |Microsoft 文件"
description: "如何 tooget 入門 hello Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: de8b8ec3-49b3-4aa8-93fb-e38f52c99743
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 6ada8a7184d7baacaba5ba9c1b9130653b1cf7fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-audit-api-samples"></a><span data-ttu-id="1d62d-103">Azure Active Directory 報告稽核 API 範例</span><span class="sxs-lookup"><span data-stu-id="1d62d-103">Azure Active Directory reporting audit API samples</span></span>
<span data-ttu-id="1d62d-104">本主題是有關 hello Azure Active Directory 的主題集合的一部分報告應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1d62d-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="1d62d-105">Azure AD 報告 api 還可讓您的 API tooaccess 稽核資料使用程式碼或相關的工具。</span><span class="sxs-lookup"><span data-stu-id="1d62d-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="1d62d-106">hello 本主題的範圍是您的範例程式碼 hello tooprovide**稽核 API**。</span><span class="sxs-lookup"><span data-stu-id="1d62d-106">hello scope of this topic is tooprovide you with sample code for hello **audit API**.</span></span>

<span data-ttu-id="1d62d-107">請參閱：</span><span class="sxs-lookup"><span data-stu-id="1d62d-107">See:</span></span>

* <span data-ttu-id="1d62d-108">[稽核記錄](active-directory-reporting-azure-portal.md#activity-reports) 以取得詳細概念資訊</span><span class="sxs-lookup"><span data-stu-id="1d62d-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="1d62d-109">[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)的 hello reporting API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1d62d-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>

<span data-ttu-id="1d62d-110">如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="1d62d-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1d62d-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d62d-111">Prerequisites</span></span>
<span data-ttu-id="1d62d-112">您可以使用本主題中的 hello 範例之前，您需要 toocomplete hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="1d62d-112">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="known-issue"></a><span data-ttu-id="1d62d-113">已知問題</span><span class="sxs-lookup"><span data-stu-id="1d62d-113">Known issue</span></span>
<span data-ttu-id="1d62d-114">如果您的租用戶 hello EU 區域中，應用程式驗證將無法運作。</span><span class="sxs-lookup"><span data-stu-id="1d62d-114">App Auth will not work if your tenant is in hello EU region.</span></span> <span data-ttu-id="1d62d-115">請 hello 稽核應用程式開發介面存取因應措施，我們修正 hello 問題之前，使用使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="1d62d-115">Please use User Auth for accessing hello Audit API as a workaround until we fix hello issue.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="1d62d-116">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d62d-116">PowerShell script</span></span>
    # This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

    # Constants
    $ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
    $ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
    $loginURL       = "https://login.microsoftonline.com"     # AAD Instance; for example https://login.microsoftonline.com
    $tenantdomain   = "your-tenant-domain.onmicrosoft.com"    # AAD Tenant; for example, contoso.onmicrosoft.com
    $resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
    $7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' toodecrement minutes, for example
    Write-Output "Searching for events starting $7daysago"

    # Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    # Parse audit report items, save output toofile(s): auditX.json, where X = 0 thru n for number of nextLink pages
    if ($oauth.access_token -ne $null) {   
        $i=0
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
        $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago

        # loop through each query page (1 through n)
        Do{
            # display each event on hello console window
            Write-Output "Fetching data using Uri: $url"
            $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
            foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
                Write-Output ($event | ConvertTo-Json)
            }

            # save hello query page tooan output file
            Write-Output "Save hello output tooa file audit$i.json"
            $myReport.Content | Out-File -FilePath audit$i.json -Force
            $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
            $i = $i+1
        } while($url -ne $null)
    } else {
        Write-Host "ERROR: No Access Token"
        }

    Write-Host "Press any key toocontinue ..."
    $x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


### <a name="executing-hello-powershell-script"></a><span data-ttu-id="1d62d-117">執行 hello PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d62d-117">Executing hello PowerShell script</span></span>
<span data-ttu-id="1d62d-118">一次您編輯 hello 指令碼完成、 執行並確認該 hello 預期會傳回從 hello 稽核記錄報告資料。</span><span class="sxs-lookup"><span data-stu-id="1d62d-118">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="1d62d-119">hello 指令碼會傳回 JSON 格式的 hello 稽核報表輸出。</span><span class="sxs-lookup"><span data-stu-id="1d62d-119">hello script returns output from hello audit report in JSON format.</span></span> <span data-ttu-id="1d62d-120">它也會建立`audit.json`檔案以 hello 相同輸出。</span><span class="sxs-lookup"><span data-stu-id="1d62d-120">It also creates an `audit.json` file with hello same output.</span></span> <span data-ttu-id="1d62d-121">您可以嘗試藉由修改 hello 指令碼 tooreturn 資料從其他報表和註解，您不需要 hello 輸出格式。</span><span class="sxs-lookup"><span data-stu-id="1d62d-121">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="bash-script"></a><span data-ttu-id="1d62d-122">Bash 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d62d-122">Bash script</span></span>
    #!/bin/bash

    # Author: Ken Hoff (kenhoff@microsoft.com)
    # Date: 2015.08.20
    # NOTE: This script requires jq (https://stedolan.github.io/jq/)

    CLIENT_ID="your-application-client-id-here"         # Should be a ~35 character string insert your info here
    CLIENT_SECRET="your-application-client-secret-here" # Should be a ~44 character string insert your info here
    LOGIN_URL="https://login.microsoftonline.com"
    TENANT_DOMAIN="your-directory-name-here.onmicrosoft.com"    # For example, contoso.onmicrosoft.com

    TOKEN_INFO=$(curl -s --data-urlencode "grant_type=client_credentials" --data-urlencode "client_id=$CLIENT_ID" --data-urlencode "client_secret=$CLIENT_SECRET" "$LOGIN_URL/$TENANT_DOMAIN/oauth2/token?api-version=1.0")

    TOKEN_TYPE=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.token_type')
    ACCESS_TOKEN=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.access_token')

    # get yesterday's date

    YESTERDAY=$(date --date='1 day ago' +'%Y-%m-%d')

    URL="https://graph.windows.net/$TENANT_DOMAIN/activities/audit?api-version=beta&$filter=activityDate%20gt%20$YESTERDAY"


    REPORT=$(curl -s --header "Authorization: $TOKEN_TYPE $ACCESS_TOKEN" $URL)

    echo $REPORT | ./jq-win64.exe -r '.value' | ./jq-win64.exe -r ".[]"

## <a name="python-script"></a><span data-ttu-id="1d62d-123">Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d62d-123">Python script</span></span>
    # Author: Michael McLaughlin (michmcla@microsoft.com)
    # Date: January 20, 2016
    # This requires hello Python Requests module: http://docs.python-requests.org

    import requests
    import datetime
    import sys

    client_id = 'your-application-client-id-here'
    client_secret = 'your-application-client-secret-here'
    login_url = 'https://login.microsoftonline.com/'
    tenant_domain = 'your-directory-name-here.onmicrosoft.com'

    # Get an OAuth access token
    bodyvals = {'client_id': client_id,
                'client_secret': client_secret,
                'grant_type': 'client_credentials'}

    request_url = login_url + tenant_domain + '/oauth2/token?api-version=1.0'
    token_response = requests.post(request_url, data=bodyvals)

    access_token = token_response.json().get('access_token')
    token_type = token_response.json().get('token_type')

    if access_token is None or token_type is None:
        print "ERROR: Couldn't get access token"
        sys.exit(1)

    # Use hello access token toomake hello API request
    yesterday = datetime.date.strftime(datetime.date.today() - datetime.timedelta(days=1), '%Y-%m-%d')

    header_params = {'Authorization': token_type + ' ' + access_token}
    request_string = 'https://graph.windows.net/' + tenant_domain + 'activities/audit?api-version=beta&$filter=activityDate%20gt%20' + yesterday   
    response = requests.get(request_string, headers = header_params)

    if response.status_code is 200:
        print response.content
    else:
        print 'ERROR: API request failed'





## <a name="next-steps"></a><span data-ttu-id="1d62d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d62d-124">Next steps</span></span>
* <span data-ttu-id="1d62d-125">您希望 toocustomize 本主題中的 hello 範例？</span><span class="sxs-lookup"><span data-stu-id="1d62d-125">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="1d62d-126">簽出 hello [Azure Active Directory 稽核應用程式開發介面參考](active-directory-reporting-api-audit-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="1d62d-126">Check out hello [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md).</span></span> 
* <span data-ttu-id="1d62d-127">如果您想要使用的完整概觀 toosee hello Azure Active Directory 報告 API，請參閱[入門 hello Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1d62d-127">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="1d62d-128">如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="1d62d-128">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

