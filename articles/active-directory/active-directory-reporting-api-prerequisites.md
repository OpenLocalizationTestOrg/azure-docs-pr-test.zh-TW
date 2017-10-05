---
title: "存取 Azure AD 報告 API 的必要條件。 | Microsoft Docs"
description: "了解存取 Azure AD 報告 API 的必要條件"
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
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="49b7c-104">存取 Azure AD 報告 API 的必要條件</span><span class="sxs-lookup"><span data-stu-id="49b7c-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="49b7c-105">[Azure AD 報告 API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) 透過一組以 REST 為基礎的 API 為您提供資料的程式設計方式存取。</span><span class="sxs-lookup"><span data-stu-id="49b7c-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="49b7c-106">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="49b7c-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="49b7c-107">報告 API 會使用 [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) 授權存取 Web API。</span><span class="sxs-lookup"><span data-stu-id="49b7c-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="49b7c-108">若要準備存取報告 API，您必須︰</span><span class="sxs-lookup"><span data-stu-id="49b7c-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="49b7c-109">在 Azure AD 租用戶中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="49b7c-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="49b7c-110">授與應用程式存取 Azure AD 資料的適當權限</span><span class="sxs-lookup"><span data-stu-id="49b7c-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="49b7c-111">從您的目錄蒐集組態設定</span><span class="sxs-lookup"><span data-stu-id="49b7c-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="49b7c-112">如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="49b7c-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="49b7c-113">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="49b7c-113">Create an Azure AD application</span></span>
<span data-ttu-id="49b7c-114">若要設定您的目錄以存取 Azure AD 報告 API，您必須以 Azure 訂用帳戶管理員帳戶登入 Azure 傳統入口網站，而且該帳戶同時也是 Azure AD 租用戶全域管理員目錄角色的成員。</span><span class="sxs-lookup"><span data-stu-id="49b7c-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49b7c-115">像這樣使用具有「管理員」權限的認證所執行的應用程式會非常強大，請務必確保應用程式的識別碼/密碼認證的安全性。</span><span class="sxs-lookup"><span data-stu-id="49b7c-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="49b7c-116">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="49b7c-118">從 **使用中目錄** 清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="49b7c-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="49b7c-119">在頂端的功能表中，按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-119">In the menu on the top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="49b7c-121">按一下底列上的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-121">On the bottom bar, click **Add**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="49b7c-123">在 [欲執行動作] 對話方塊上，按一下 [新增我的組織正在開發的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="49b7c-125">在 [告訴我們您的應用程式]  對話方塊上，執行以下步驟：</span><span class="sxs-lookup"><span data-stu-id="49b7c-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="49b7c-127">a.</span><span class="sxs-lookup"><span data-stu-id="49b7c-127">a.</span></span> <span data-ttu-id="49b7c-128">在 [名稱] 文字方塊中，輸入名稱 (例如：報告 API 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="49b7c-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="49b7c-129">b.</span><span class="sxs-lookup"><span data-stu-id="49b7c-129">b.</span></span> <span data-ttu-id="49b7c-130">選取 [Web 應用程式和/或 Web API]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="49b7c-131">c.</span><span class="sxs-lookup"><span data-stu-id="49b7c-131">c.</span></span> <span data-ttu-id="49b7c-132">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-132">Click **Next**.</span></span>
7. <span data-ttu-id="49b7c-133">在 [應用程式屬性]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="49b7c-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="49b7c-135">a.</span><span class="sxs-lookup"><span data-stu-id="49b7c-135">a.</span></span> <span data-ttu-id="49b7c-136">在 [登入 URL] 文字方塊中，輸入 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="49b7c-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="49b7c-137">b.</span><span class="sxs-lookup"><span data-stu-id="49b7c-137">b.</span></span> <span data-ttu-id="49b7c-138">在 [應用程式識別碼 URI] 文字方塊中，輸入 ```https://localhost/ReportingApiApp```。</span><span class="sxs-lookup"><span data-stu-id="49b7c-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="49b7c-139">c.</span><span class="sxs-lookup"><span data-stu-id="49b7c-139">c.</span></span> <span data-ttu-id="49b7c-140">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="49b7c-141">授與您的應用程式使用 API 的權限</span><span class="sxs-lookup"><span data-stu-id="49b7c-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="49b7c-142">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="49b7c-144">從 **使用中目錄** 清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="49b7c-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="49b7c-145">在頂端的功能表中，按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-145">In the menu on the top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="49b7c-147">在應用程式清單中，選取新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="49b7c-147">In the applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="49b7c-149">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-149">In the menu on the top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="49b7c-151">在 [其他應用程式的權限] 區段中，若是 [Azure Active Directory] 資源，請按一下 [應用程式權限] 下拉式清單，然後選取 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="49b7c-153">按一下底列上的 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-153">On the bottom bar, click **Save**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="49b7c-155">從您的目錄蒐集組態設定</span><span class="sxs-lookup"><span data-stu-id="49b7c-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="49b7c-156">本節說明如何從您的目錄取得下列設定︰</span><span class="sxs-lookup"><span data-stu-id="49b7c-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="49b7c-157">網域名稱</span><span class="sxs-lookup"><span data-stu-id="49b7c-157">Domain name</span></span>
* <span data-ttu-id="49b7c-158">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="49b7c-158">Client ID</span></span>
* <span data-ttu-id="49b7c-159">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="49b7c-159">Client secret</span></span>

<span data-ttu-id="49b7c-160">您在設定報告 API 的呼叫時需要這些值。</span><span class="sxs-lookup"><span data-stu-id="49b7c-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="49b7c-161">取得您的網域名稱</span><span class="sxs-lookup"><span data-stu-id="49b7c-161">Get your domain name</span></span>
1. <span data-ttu-id="49b7c-162">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="49b7c-164">從 **使用中目錄** 清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="49b7c-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="49b7c-165">在頂端的功能表中，按一下 [網域] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-165">In the menu on the top, click **Domains**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="49b7c-167">在 [網域名稱]  欄中，複製您的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="49b7c-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="49b7c-169">取得應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="49b7c-169">Get the application's client ID</span></span>
1. <span data-ttu-id="49b7c-170">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="49b7c-172">從 **使用中目錄** 清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="49b7c-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="49b7c-173">在頂端的功能表中，按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-173">In the menu on the top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="49b7c-175">在應用程式清單中，選取新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="49b7c-175">In the applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="49b7c-177">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-177">In the menu on the top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="49b7c-179">複製您的 [用戶端識別碼] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-179">Copy your **Client ID**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="49b7c-181">取得應用程式的用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="49b7c-181">Get the application's client secret</span></span>
<span data-ttu-id="49b7c-182">若要取得應用程式的用戶端密碼，您需要建立新的金鑰並在儲存新金鑰時儲存其值，因為稍後不可能再擷取此值。</span><span class="sxs-lookup"><span data-stu-id="49b7c-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="49b7c-183">在 [Azure 傳統入口網站](https://manage.windowsazure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="49b7c-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="49b7c-185">從 **使用中目錄** 清單中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="49b7c-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="49b7c-186">在頂端的功能表中，按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-186">In the menu on the top, click **Applications**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="49b7c-188">在應用程式清單中，選取新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="49b7c-188">In the applications list, select your newly created application.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="49b7c-190">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-190">In the menu on the top, click **Configure**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="49b7c-192">在 [金鑰]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="49b7c-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="49b7c-194">a.</span><span class="sxs-lookup"><span data-stu-id="49b7c-194">a.</span></span> <span data-ttu-id="49b7c-195">從持續時間清單中，選取持續時間。</span><span class="sxs-lookup"><span data-stu-id="49b7c-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="49b7c-196">b.</span><span class="sxs-lookup"><span data-stu-id="49b7c-196">b.</span></span> <span data-ttu-id="49b7c-197">按一下底列上的 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="49b7c-197">On the bottom bar, click **Save**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="49b7c-199">c.</span><span class="sxs-lookup"><span data-stu-id="49b7c-199">c.</span></span> <span data-ttu-id="49b7c-200">複製金鑰值。</span><span class="sxs-lookup"><span data-stu-id="49b7c-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49b7c-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49b7c-201">Next Steps</span></span>
* <span data-ttu-id="49b7c-202">您要以程式設計方式從 Azure AD 報告 API 存取資料嗎？</span><span class="sxs-lookup"><span data-stu-id="49b7c-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="49b7c-203">請查看 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="49b7c-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="49b7c-204">如果您想要深入了解 Azure Active Directory 報告，請參閱 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="49b7c-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

