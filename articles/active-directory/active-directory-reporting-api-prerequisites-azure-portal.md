---
title: "aaaPrerequisites tooaccess hello Azure AD 報告 API |Microsoft 文件"
description: "深入了解 hello 必要條件 tooaccess hello Azure AD 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="96ce5-103">必要條件 tooaccess hello Azure AD 報告 API</span><span class="sxs-lookup"><span data-stu-id="96ce5-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="96ce5-104">hello [Azure AD 報告 Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview)提供您透過一組以 REST 為基礎的 Api 以程式設計方式存取 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="96ce5-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="96ce5-105">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="96ce5-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="96ce5-106">報告應用程式開發介面使用的 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize 存取 toohello web Api。</span><span class="sxs-lookup"><span data-stu-id="96ce5-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="96ce5-107">tooget 透過 hello API 存取 toohello 報告資料，您需要 toohave hello 遵循指派角色的其中一個：</span><span class="sxs-lookup"><span data-stu-id="96ce5-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="96ce5-108">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="96ce5-108">Security Reader</span></span>
- <span data-ttu-id="96ce5-109">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="96ce5-109">Security Admin</span></span>
- <span data-ttu-id="96ce5-110">全域管理員</span><span class="sxs-lookup"><span data-stu-id="96ce5-110">Global Admin</span></span>


<span data-ttu-id="96ce5-111">tooprepare 報告 API 您存取 toohello，您必須：</span><span class="sxs-lookup"><span data-stu-id="96ce5-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="96ce5-112">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="96ce5-112">Register an application</span></span> 
2. <span data-ttu-id="96ce5-113">授與權限</span><span class="sxs-lookup"><span data-stu-id="96ce5-113">Grant permissions</span></span> 
3. <span data-ttu-id="96ce5-114">收集組態設定</span><span class="sxs-lookup"><span data-stu-id="96ce5-114">Gather configuration settings</span></span> 

<span data-ttu-id="96ce5-115">如有相關疑問、問題或意見，請[提出支援票證](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)。</span><span class="sxs-lookup"><span data-stu-id="96ce5-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="96ce5-116">註冊 Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="96ce5-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="96ce5-117">即使您要存取 hello 報告 API 使用指令碼，您會需要 tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96ce5-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="96ce5-118">這可讓您**應用程式識別碼**，這是必要的授權呼叫它可讓您的程式碼 tooreceive 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="96ce5-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="96ce5-119">tooconfigure 目錄 tooaccess hello Azure AD 報告 API，您必須登入 toohello hello 的成員也是 Azure 系統管理員帳戶的 Azure 入口網站**全域管理員**Azure AD 租用戶中的目錄角色.</span><span class="sxs-lookup"><span data-stu-id="96ce5-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96ce5-120">使用像這樣的"admin"權限認證下執行的應用程式可能非常強大，因此請在確定 tookeep hello 應用程式的識別碼/密碼認證的安全性。</span><span class="sxs-lookup"><span data-stu-id="96ce5-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="96ce5-121">**tooregister Azure Active Directory 應用程式：**</span><span class="sxs-lookup"><span data-stu-id="96ce5-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="96ce5-122">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="96ce5-124">在 [hello **Azure Active Directory**刀鋒視窗中，按一下 [**應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="96ce5-126">在 [hello**應用程式註冊**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**新應用程式註冊**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="96ce5-128">在 [hello**建立**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="96ce5-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="96ce5-130">a.</span><span class="sxs-lookup"><span data-stu-id="96ce5-130">a.</span></span> <span data-ttu-id="96ce5-131">在 [hello**名稱**文字方塊中，輸入`Reporting API application`。</span><span class="sxs-lookup"><span data-stu-id="96ce5-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="96ce5-132">b.</span><span class="sxs-lookup"><span data-stu-id="96ce5-132">b.</span></span> <span data-ttu-id="96ce5-133">對於 [應用程式類型]，選取 [Web 應用程式/API]。</span><span class="sxs-lookup"><span data-stu-id="96ce5-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="96ce5-134">c.</span><span class="sxs-lookup"><span data-stu-id="96ce5-134">c.</span></span> <span data-ttu-id="96ce5-135">在 [hello**登入 URL**文字方塊中，輸入`https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="96ce5-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="96ce5-136">d.</span><span class="sxs-lookup"><span data-stu-id="96ce5-136">d.</span></span> <span data-ttu-id="96ce5-137">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="96ce5-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="96ce5-138">授與權限</span><span class="sxs-lookup"><span data-stu-id="96ce5-138">Grant permissions</span></span> 

<span data-ttu-id="96ce5-139">這個步驟中的 hello 目標應用程式是 toogrant**讀取目錄資料**權限 toohello **Windows Azure Active Directory**應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="96ce5-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="96ce5-141">**toogrant 您應用程式的權限 toouse hello API:**</span><span class="sxs-lookup"><span data-stu-id="96ce5-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="96ce5-142">在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="96ce5-143">在 [hello **Reporting API 的應用程式**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="96ce5-145">在 [hello**設定**刀鋒視窗中，按一下 [**必要的權限**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="96ce5-147">在 [hello**必要的權限**刀鋒視窗中的，在 hello **API**清單中，按一下**Windows Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="96ce5-149">在 [hello**啟用存取**刀鋒視窗中，選取**讀取目錄資料**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="96ce5-151">在 hello hello 上方的工具列中按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="96ce5-153">收集組態設定</span><span class="sxs-lookup"><span data-stu-id="96ce5-153">Gather configuration settings</span></span> 
<span data-ttu-id="96ce5-154">這個區段會顯示如何 tooget hello 您目錄中的下列設定：</span><span class="sxs-lookup"><span data-stu-id="96ce5-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="96ce5-155">網域名稱</span><span class="sxs-lookup"><span data-stu-id="96ce5-155">Domain name</span></span>
* <span data-ttu-id="96ce5-156">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="96ce5-156">Client ID</span></span>
* <span data-ttu-id="96ce5-157">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="96ce5-157">Client secret</span></span>

<span data-ttu-id="96ce5-158">設定呼叫 toohello 報告 API 時，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="96ce5-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="96ce5-159">取得您的網域名稱</span><span class="sxs-lookup"><span data-stu-id="96ce5-159">Get your domain name</span></span>

<span data-ttu-id="96ce5-160">**tooget 您的網域名稱：**</span><span class="sxs-lookup"><span data-stu-id="96ce5-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="96ce5-161">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="96ce5-163">在 [hello **Azure Active Directory**刀鋒視窗中，按一下 [**網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="96ce5-165">複製 hello 網域清單中的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="96ce5-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="96ce5-166">取得應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="96ce5-166">Get your application's client ID</span></span>

<span data-ttu-id="96ce5-167">**tooget 應用程式的用戶端識別碼：**</span><span class="sxs-lookup"><span data-stu-id="96ce5-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="96ce5-168">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="96ce5-170">在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="96ce5-171">在 [hello **Reporting API 的應用程式**刀鋒視窗中的，在 hello**應用程式識別碼**，按一下 [**按一下 toocopy**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="96ce5-173">取得應用程式的用戶端祕密</span><span class="sxs-lookup"><span data-stu-id="96ce5-173">Get your application's client secret</span></span>
<span data-ttu-id="96ce5-174">tooget 應用程式的用戶端秘密，toocreate 新的金鑰，儲存其值在儲存 hello 新的金鑰，因為它不可能 tooretrieve 時這個值稍後再。</span><span class="sxs-lookup"><span data-stu-id="96ce5-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="96ce5-175">**tooget 應用程式的用戶端密碼：**</span><span class="sxs-lookup"><span data-stu-id="96ce5-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="96ce5-176">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="96ce5-178">在 [hello**應用程式註冊**刀鋒視窗中的，在 hello 應用程式清單中，按一下**Reporting API 的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="96ce5-179">在 [hello **Reporting API 的應用程式**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="96ce5-181">在 [hello**設定**刀鋒視窗中的，在 hello **APIR 存取**區段中，按一下**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="96ce5-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="96ce5-183">在 [hello**金鑰**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="96ce5-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="96ce5-185">a.</span><span class="sxs-lookup"><span data-stu-id="96ce5-185">a.</span></span> <span data-ttu-id="96ce5-186">在 [hello**描述**文字方塊中，輸入`Reporting API`。</span><span class="sxs-lookup"><span data-stu-id="96ce5-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="96ce5-187">b.</span><span class="sxs-lookup"><span data-stu-id="96ce5-187">b.</span></span> <span data-ttu-id="96ce5-188">選取 [2 年後] 來作為 [到期]。</span><span class="sxs-lookup"><span data-stu-id="96ce5-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="96ce5-189">c.</span><span class="sxs-lookup"><span data-stu-id="96ce5-189">c.</span></span> <span data-ttu-id="96ce5-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="96ce5-190">Click **Save**.</span></span>

    <span data-ttu-id="96ce5-191">d.</span><span class="sxs-lookup"><span data-stu-id="96ce5-191">d.</span></span> <span data-ttu-id="96ce5-192">複製 hello 索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="96ce5-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="96ce5-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96ce5-193">Next Steps</span></span>
* <span data-ttu-id="96ce5-194">您像 tooaccess hello hello Azure AD 的資料會報告 API 以程式設計的方式？</span><span class="sxs-lookup"><span data-stu-id="96ce5-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="96ce5-195">簽出[開始使用 Azure Active Directory 報告 API hello](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="96ce5-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="96ce5-196">如果您想要深入了解 Azure Active Directory 報告 toofind，請參閱 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="96ce5-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

