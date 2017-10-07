---
title: "aaaPrerequisites tooaccess hello Azure AD 報告 API。 | Microsoft Docs"
description: "深入了解 hello 必要條件 tooaccess hello Azure AD 報告 API"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="cbaba-104">必要條件 tooaccess hello Azure AD 報告 API</span><span class="sxs-lookup"><span data-stu-id="cbaba-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="cbaba-105">hello [Azure AD 報告 Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview)提供您透過一組以 REST 為基礎的 Api 以程式設計方式存取 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="cbaba-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="cbaba-106">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="cbaba-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="cbaba-107">報告應用程式開發介面使用的 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize 存取 toohello web Api。</span><span class="sxs-lookup"><span data-stu-id="cbaba-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="cbaba-108">tooprepare 報告 API 您存取 toohello，您必須：</span><span class="sxs-lookup"><span data-stu-id="cbaba-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="cbaba-109">在 Azure AD 租用戶中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="cbaba-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="cbaba-110">授與 hello 應用程式適當的權限 tooaccess hello Azure AD 資料</span><span class="sxs-lookup"><span data-stu-id="cbaba-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="cbaba-111">從您的目錄蒐集組態設定</span><span class="sxs-lookup"><span data-stu-id="cbaba-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="cbaba-112">如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="cbaba-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="cbaba-113">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="cbaba-113">Create an Azure AD application</span></span>
<span data-ttu-id="cbaba-114">tooconfigure 目錄 tooaccess hello Azure AD 報告 API，您必須登入 toohello 也是 Azure AD 租用戶中的 hello 全域管理員目錄角色成員的 Azure 訂用帳戶系統管理員帳戶的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="cbaba-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbaba-115">使用像這樣的"admin"權限認證下執行的應用程式可能非常強大，因此請在確定 tookeep hello 應用程式的識別碼/密碼認證的安全性。</span><span class="sxs-lookup"><span data-stu-id="cbaba-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="cbaba-116">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="cbaba-118">從 hello **active directory**清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="cbaba-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="cbaba-119">在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="cbaba-121">Hello 下方列上，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-121">On hello bottom bar, click **Add**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="cbaba-123">在 [hello**怎麼辦想 toodo？** ] 對話方塊中，按一下**加入我組織正在開發的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="cbaba-125">在 [hello**告訴我們您的應用程式**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbaba-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="cbaba-127">a.</span><span class="sxs-lookup"><span data-stu-id="cbaba-127">a.</span></span> <span data-ttu-id="cbaba-128">在 hello**名稱**文字方塊中，輸入名稱 (例如： 報告 API 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="cbaba-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="cbaba-129">b.</span><span class="sxs-lookup"><span data-stu-id="cbaba-129">b.</span></span> <span data-ttu-id="cbaba-130">選取 [Web 應用程式和/或 Web API]。</span><span class="sxs-lookup"><span data-stu-id="cbaba-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="cbaba-131">c.</span><span class="sxs-lookup"><span data-stu-id="cbaba-131">c.</span></span> <span data-ttu-id="cbaba-132">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="cbaba-132">Click **Next**.</span></span>
7. <span data-ttu-id="cbaba-133">在 [hello**應用程式屬性**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbaba-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="cbaba-135">a.</span><span class="sxs-lookup"><span data-stu-id="cbaba-135">a.</span></span> <span data-ttu-id="cbaba-136">在 hello**登入 URL**文字方塊中，輸入`https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="cbaba-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="cbaba-137">b.</span><span class="sxs-lookup"><span data-stu-id="cbaba-137">b.</span></span> <span data-ttu-id="cbaba-138">在 hello**應用程式識別碼 URI**文字方塊中，輸入```https://localhost/ReportingApiApp```。</span><span class="sxs-lookup"><span data-stu-id="cbaba-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="cbaba-139">c.</span><span class="sxs-lookup"><span data-stu-id="cbaba-139">c.</span></span> <span data-ttu-id="cbaba-140">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="cbaba-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="cbaba-141">授與您的應用程式的權限 toouse hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="cbaba-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="cbaba-142">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="cbaba-144">從 hello **active directory**清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="cbaba-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="cbaba-145">在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="cbaba-147">在 hello 應用程式清單中，選取您新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbaba-147">In hello applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="cbaba-149">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="cbaba-151">在 hello**權限 tooother 應用程式** 區段下的 hello **Azure Active Directory**資源按一下 hello**應用程式權限**下拉式清單，然後選取**讀取目錄資料**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="cbaba-153">Hello 下方列上，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-153">On hello bottom bar, click **Save**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="cbaba-155">從您的目錄蒐集組態設定</span><span class="sxs-lookup"><span data-stu-id="cbaba-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="cbaba-156">這個區段會顯示如何 tooget hello 您目錄中的下列設定：</span><span class="sxs-lookup"><span data-stu-id="cbaba-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="cbaba-157">網域名稱</span><span class="sxs-lookup"><span data-stu-id="cbaba-157">Domain name</span></span>
* <span data-ttu-id="cbaba-158">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="cbaba-158">Client ID</span></span>
* <span data-ttu-id="cbaba-159">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="cbaba-159">Client secret</span></span>

<span data-ttu-id="cbaba-160">設定呼叫 toohello 報告 API 時，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="cbaba-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="cbaba-161">取得您的網域名稱</span><span class="sxs-lookup"><span data-stu-id="cbaba-161">Get your domain name</span></span>
1. <span data-ttu-id="cbaba-162">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="cbaba-164">從 hello **active directory**清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="cbaba-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="cbaba-165">在 hello 最上層顯示 hello 功能表上，按一下**網域**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="cbaba-167">在 hello**網域名稱**資料行中，複製您的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="cbaba-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="cbaba-169">取得 hello 應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="cbaba-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="cbaba-170">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="cbaba-172">從 hello **active directory**清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="cbaba-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="cbaba-173">在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="cbaba-175">在 hello 應用程式清單中，選取您新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbaba-175">In hello applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="cbaba-177">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="cbaba-179">複製您的 [用戶端識別碼] 。</span><span class="sxs-lookup"><span data-stu-id="cbaba-179">Copy your **Client ID**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="cbaba-181">取得 hello 應用程式的用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="cbaba-181">Get hello application's client secret</span></span>
<span data-ttu-id="cbaba-182">tooget 應用程式的用戶端秘密，toocreate 新的金鑰，儲存其值在儲存 hello 新的金鑰，因為它不可能 tooretrieve 時這個值稍後再。</span><span class="sxs-lookup"><span data-stu-id="cbaba-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="cbaba-183">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="cbaba-185">從 hello **active directory**清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="cbaba-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="cbaba-186">在 hello 最上層顯示 hello 功能表上，按一下**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="cbaba-188">在 hello 應用程式清單中，選取您新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbaba-188">In hello applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="cbaba-190">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="cbaba-192">在 hello**金鑰**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbaba-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="cbaba-194">a.</span><span class="sxs-lookup"><span data-stu-id="cbaba-194">a.</span></span> <span data-ttu-id="cbaba-195">從 hello 持續時間] 清單中，選取 [持續時間</span><span class="sxs-lookup"><span data-stu-id="cbaba-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="cbaba-196">b.</span><span class="sxs-lookup"><span data-stu-id="cbaba-196">b.</span></span> <span data-ttu-id="cbaba-197">Hello 下方列上，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="cbaba-197">On hello bottom bar, click **Save**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="cbaba-199">c.</span><span class="sxs-lookup"><span data-stu-id="cbaba-199">c.</span></span> <span data-ttu-id="cbaba-200">複製 hello 索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="cbaba-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbaba-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbaba-201">Next Steps</span></span>
* <span data-ttu-id="cbaba-202">您像 tooaccess hello hello Azure AD 的資料會報告 API 以程式設計的方式？</span><span class="sxs-lookup"><span data-stu-id="cbaba-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="cbaba-203">簽出[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="cbaba-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="cbaba-204">如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="cbaba-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

