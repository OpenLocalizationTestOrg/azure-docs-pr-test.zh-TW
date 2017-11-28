---
title: "aaaGet 開始使用 Azure Active Directory 識別身分保護，Microsoft Graph |Microsoft 文件"
description: "提供簡介 tooquery Microsoft Graph 從 Azure Active Directory 的風險事件和相關聯的資訊清單。"
services: active-directory
keywords: "azure active directory identity protection, 風險事件, 弱點, 安全性原則, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="30626-104">開始使用 Azure Active Directory Identity Protection 和 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="30626-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="30626-105">Microsoft Graph 是 Microsoft 統一的 API 端點的 hello 與家庭的 hello [Azure Active Directory 識別身分保護](active-directory-identityprotection.md)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="30626-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="30626-106">hello 第一個應用程式開發介面， **identityRiskEvents**，可讓您 tooquery Microsoft Graph 清單的[風險事件](active-directory-identityprotection-risk-events-types.md)和相關聯的資訊。</span><span class="sxs-lookup"><span data-stu-id="30626-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="30626-107">本文可協助您開始查詢此 API。</span><span class="sxs-lookup"><span data-stu-id="30626-107">This article gets you started querying this API.</span></span> <span data-ttu-id="30626-108">深入了解簡介、 完整的文件，與存取 toohello 圖表總管，請參閱 hello [Microsoft Graph 網站](https://graph.microsoft.io/)。</span><span class="sxs-lookup"><span data-stu-id="30626-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30626-109">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="30626-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="30626-110">有三個步驟 tooaccessing 識別身分保護資料，Microsoft Graph 透過：</span><span class="sxs-lookup"><span data-stu-id="30626-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="30626-111">新增應用程式與用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="30626-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="30626-112">使用此密碼和其他一些資訊 tooauthenticate tooMicrosoft 圖形中，您在何處接收驗證 token 片段。</span><span class="sxs-lookup"><span data-stu-id="30626-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="30626-113">使用這個語彙基元 toomake 要求 toohello API 端點，並回到識別身分保護資料。</span><span class="sxs-lookup"><span data-stu-id="30626-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="30626-114">開始之前，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="30626-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="30626-115">系統管理員權限 toocreate hello 應用程式在 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="30626-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="30626-116">您的租用戶網域 (例如 contoso.onmicrosoft.com) hello 名稱</span><span class="sxs-lookup"><span data-stu-id="30626-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="30626-117">新增應用程式與用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="30626-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="30626-118">[登入](https://manage.windowsazure.com)tooyour 身為系統管理員的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="30626-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="30626-119">在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="30626-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="30626-121">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="30626-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="30626-122">在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="30626-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="30626-124">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="30626-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="30626-126">在 [hello**您該怎麼想 toodo** ] 對話方塊中，按一下**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="30626-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="30626-128">在 [hello**告訴我們您的應用程式**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="30626-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="30626-130">a.</span><span class="sxs-lookup"><span data-stu-id="30626-130">a.</span></span> <span data-ttu-id="30626-131">在 hello**名稱**文字方塊中，輸入您的應用程式的名稱 (例如： AADIP 風險事件 API 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="30626-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="30626-132">b.</span><span class="sxs-lookup"><span data-stu-id="30626-132">b.</span></span> <span data-ttu-id="30626-133">在 [類型]，選取 [Web 應用程式和/或 Web API]。</span><span class="sxs-lookup"><span data-stu-id="30626-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="30626-134">c.</span><span class="sxs-lookup"><span data-stu-id="30626-134">c.</span></span> <span data-ttu-id="30626-135">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="30626-135">Click **Next**.</span></span>
8. <span data-ttu-id="30626-136">在 [hello**應用程式屬性**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="30626-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="30626-138">a.</span><span class="sxs-lookup"><span data-stu-id="30626-138">a.</span></span> <span data-ttu-id="30626-139">在 hello**登入 URL**文字方塊中，輸入`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="30626-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="30626-140">b.</span><span class="sxs-lookup"><span data-stu-id="30626-140">b.</span></span> <span data-ttu-id="30626-141">在 hello**應用程式識別碼 URI**文字方塊中，輸入`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="30626-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="30626-142">c.</span><span class="sxs-lookup"><span data-stu-id="30626-142">c.</span></span> <span data-ttu-id="30626-143">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="30626-143">Click **Complete**.</span></span>

<span data-ttu-id="30626-144">現在您可以設定您的應用程式了。</span><span class="sxs-lookup"><span data-stu-id="30626-144">Your can now configure your application.</span></span>

![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="30626-146">授與您的應用程式的權限 toouse hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="30626-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="30626-147">在您的應用程式頁面上，hello hello 上方的功能表中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="30626-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="30626-149">在 hello**權限 tooother 應用程式**區段中，按一下**新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="30626-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="30626-151">在 [hello**權限 tooother 應用程式**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="30626-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="30626-153">a.</span><span class="sxs-lookup"><span data-stu-id="30626-153">a.</span></span> <span data-ttu-id="30626-154">選取 [Microsoft Graph]。</span><span class="sxs-lookup"><span data-stu-id="30626-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="30626-155">b.</span><span class="sxs-lookup"><span data-stu-id="30626-155">b.</span></span> <span data-ttu-id="30626-156">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="30626-156">Click **Complete**.</span></span>
4. <span data-ttu-id="30626-157">按一下 [應用程式權限: 0]，然後選取 [讀取所有身分識別風險事件資訊]。</span><span class="sxs-lookup"><span data-stu-id="30626-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="30626-159">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="30626-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="30626-161">取得存取金鑰</span><span class="sxs-lookup"><span data-stu-id="30626-161">Get an access key</span></span>
1. <span data-ttu-id="30626-162">在您的應用程式 頁面的 hello**金鑰**區段中，選取持續時間為 1 年。</span><span class="sxs-lookup"><span data-stu-id="30626-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="30626-164">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="30626-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="30626-166">在 hello 金鑰 > 一節，複製 hello 您新建立的金鑰值並貼到安全的位置。</span><span class="sxs-lookup"><span data-stu-id="30626-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![建立應用程式](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="30626-168">如果遺失此機碼，您將有 tooreturn toothis 區段，並建立新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="30626-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="30626-169">請勿將此金鑰告知他人︰任何人只要擁有此金鑰就可以存取您的資料。</span><span class="sxs-lookup"><span data-stu-id="30626-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="30626-170">在 hello**屬性**區段，複製 hello**用戶端識別碼**，然後將它貼到安全的位置。</span><span class="sxs-lookup"><span data-stu-id="30626-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="30626-171">驗證 tooMicrosoft 圖形和查詢 hello 識別風險事件 API</span><span class="sxs-lookup"><span data-stu-id="30626-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="30626-172">到目前為止，您應該已擁有︰</span><span class="sxs-lookup"><span data-stu-id="30626-172">At this point, you should have:</span></span>

* <span data-ttu-id="30626-173">複製上述的 hello 用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="30626-173">hello client ID you copied above</span></span>
* <span data-ttu-id="30626-174">複製上述的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="30626-174">hello key you copied above</span></span>
* <span data-ttu-id="30626-175">hello 租用戶的網域名稱</span><span class="sxs-lookup"><span data-stu-id="30626-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="30626-176">tooauthenticate，傳送 post 要求太`https://login.microsoft.com`以 hello 遵循 hello 主體中的參數：</span><span class="sxs-lookup"><span data-stu-id="30626-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="30626-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="30626-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="30626-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="30626-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="30626-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="30626-179">client_id: <your client ID></span></span>
* <span data-ttu-id="30626-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="30626-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="30626-181">您需要 tooprovide 值 hello **client_id**和 hello **client_secret**參數。</span><span class="sxs-lookup"><span data-stu-id="30626-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="30626-182">如果成功，這會傳回驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="30626-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="30626-183">toocall hello 應用程式開發介面，建立 hello 參數後面的標頭：</span><span class="sxs-lookup"><span data-stu-id="30626-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="30626-184">驗證時，您可以在 hello 傳回權杖中找到 hello 語彙基元類型及存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="30626-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="30626-185">以下列 API URL 要求 toohello 中傳送此標頭：`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="30626-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="30626-186">hello 回應，如果成功，風險的事件所識別的集合與相關聯的 hello OData JSON 格式，但可以剖析和處理可視中的資料。</span><span class="sxs-lookup"><span data-stu-id="30626-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="30626-187">以下是驗證和呼叫 hello 應用程式開發介面使用 Powershell 的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="30626-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="30626-188">您只需要加入用戶端識別碼、金鑰和租用戶網域。</span><span class="sxs-lookup"><span data-stu-id="30626-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="30626-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30626-189">Next steps</span></span>
<span data-ttu-id="30626-190">恭喜，您剛建立的第一個呼叫 tooMicrosoft 圖形 ！</span><span class="sxs-lookup"><span data-stu-id="30626-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="30626-191">現在您可以查詢識別風險事件，並使用 hello 資料，不過您看到符合。</span><span class="sxs-lookup"><span data-stu-id="30626-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="30626-192">深入了解 Microsoft Graph toolearn 及 toobuild 應用程式使用方式 hello Graph API，請參閱 hello[文件](https://graph.microsoft.io/docs)及其他更多在 hello [Microsoft Graph 網站](https://graph.microsoft.io/)。</span><span class="sxs-lookup"><span data-stu-id="30626-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="30626-193">此外，也請確定 toobookmark hello [Azure AD Identity Protection 應用程式開發介面](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)hello 識別保護 Api 可在圖表中的所有列出的頁面。</span><span class="sxs-lookup"><span data-stu-id="30626-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="30626-194">當我們新增識別身分保護透過 API 使用的新方式 toowork，您會在該頁面上看到它們。</span><span class="sxs-lookup"><span data-stu-id="30626-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30626-195">其他資源</span><span class="sxs-lookup"><span data-stu-id="30626-195">Additional resources</span></span>
* [<span data-ttu-id="30626-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="30626-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="30626-197">Azure Active Directory Identity Protection 偵測到的風險事件類型</span><span class="sxs-lookup"><span data-stu-id="30626-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="30626-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="30626-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="30626-199">Microsoft Graph 概觀</span><span class="sxs-lookup"><span data-stu-id="30626-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="30626-200">Azure AD Identity Protection 服務根目錄</span><span class="sxs-lookup"><span data-stu-id="30626-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

