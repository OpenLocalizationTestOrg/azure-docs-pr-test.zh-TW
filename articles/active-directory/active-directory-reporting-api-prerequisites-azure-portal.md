---
title: "存取 Azure AD 報告 API 的必要條件 | Microsoft Docs"
description: "了解存取 Azure AD 報告 API 的必要條件"
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
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="62400-103">存取 Azure AD 報告 API 的必要條件</span><span class="sxs-lookup"><span data-stu-id="62400-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="62400-104">[Azure AD 報告 API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) 透過一組以 REST 為基礎的 API 為您提供資料的程式設計方式存取。</span><span class="sxs-lookup"><span data-stu-id="62400-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="62400-105">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="62400-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="62400-106">報告 API 會使用 [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) 授權存取 Web API。</span><span class="sxs-lookup"><span data-stu-id="62400-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="62400-107">若要透過 API 來存取報告資料，您必須已具備下列其中一個指派的角色︰</span><span class="sxs-lookup"><span data-stu-id="62400-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="62400-108">安全性讀取者</span><span class="sxs-lookup"><span data-stu-id="62400-108">Security Reader</span></span>
- <span data-ttu-id="62400-109">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="62400-109">Security Admin</span></span>
- <span data-ttu-id="62400-110">全域管理員</span><span class="sxs-lookup"><span data-stu-id="62400-110">Global Admin</span></span>


<span data-ttu-id="62400-111">若要準備存取報告 API，您必須︰</span><span class="sxs-lookup"><span data-stu-id="62400-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="62400-112">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="62400-112">Register an application</span></span> 
2. <span data-ttu-id="62400-113">授與權限</span><span class="sxs-lookup"><span data-stu-id="62400-113">Grant permissions</span></span> 
3. <span data-ttu-id="62400-114">收集組態設定</span><span class="sxs-lookup"><span data-stu-id="62400-114">Gather configuration settings</span></span> 

<span data-ttu-id="62400-115">如有相關疑問、問題或意見，請[提出支援票證](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)。</span><span class="sxs-lookup"><span data-stu-id="62400-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="62400-116">註冊 Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="62400-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="62400-117">即使您使用指令碼來存取報告 API，也必須註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="62400-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="62400-118">註冊可讓您取得**應用程式識別碼**，您必須有此識別碼才能進行授權呼叫，以便讓程式碼獲得權杖。</span><span class="sxs-lookup"><span data-stu-id="62400-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="62400-119">若要設定您的目錄以存取 Azure AD 報告 API，您必須以 Azure 管理員帳戶登入 Azure 入口網站，而且該帳戶同時也是 Azure AD 租用戶**全域管理員**目錄角色的成員。</span><span class="sxs-lookup"><span data-stu-id="62400-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62400-120">像這樣使用具有「管理員」權限的認證所執行的應用程式會非常強大，請務必確保應用程式的識別碼/密碼認證的安全性。</span><span class="sxs-lookup"><span data-stu-id="62400-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="62400-121">**若要註冊 Azure Active Directory 應用程式：**</span><span class="sxs-lookup"><span data-stu-id="62400-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="62400-122">在 [Azure 入口網站](https://portal.azure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="62400-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="62400-124">在 [Azure Active Directory] 刀鋒視窗中，按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="62400-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="62400-126">在 [應用程式註冊] 刀鋒視窗上，按一下頂端工具列中的 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="62400-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="62400-128">在 [建立] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="62400-128">On the **Create** blade, perform the following steps:</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="62400-130">a.</span><span class="sxs-lookup"><span data-stu-id="62400-130">a.</span></span> <span data-ttu-id="62400-131">在 [名稱] 文字方塊中，輸入 `Reporting API application`。</span><span class="sxs-lookup"><span data-stu-id="62400-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="62400-132">b.</span><span class="sxs-lookup"><span data-stu-id="62400-132">b.</span></span> <span data-ttu-id="62400-133">對於 [應用程式類型]，選取 [Web 應用程式/API]。</span><span class="sxs-lookup"><span data-stu-id="62400-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="62400-134">c.</span><span class="sxs-lookup"><span data-stu-id="62400-134">c.</span></span> <span data-ttu-id="62400-135">在 [登入 URL] 文字方塊中，輸入 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="62400-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="62400-136">d.</span><span class="sxs-lookup"><span data-stu-id="62400-136">d.</span></span> <span data-ttu-id="62400-137">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="62400-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="62400-138">授與權限</span><span class="sxs-lookup"><span data-stu-id="62400-138">Grant permissions</span></span> 

<span data-ttu-id="62400-139">此步驟的目標是要對應用程式授與 **Windows Azure Active Directory** API 的**讀取目錄資料**權限。</span><span class="sxs-lookup"><span data-stu-id="62400-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="62400-141">**若要對應用程式授與 API 使用權限：**</span><span class="sxs-lookup"><span data-stu-id="62400-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="62400-142">在 [應用程式註冊] 刀鋒視窗中，按一下應用程式清單中的 [報告 API 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="62400-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="62400-143">在 [報告 API 應用程式] 刀鋒視窗中，按一下頂端工具列中的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="62400-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="62400-145">在 [設定] 刀鋒視窗中，按一下 [必要權限]。</span><span class="sxs-lookup"><span data-stu-id="62400-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="62400-147">在 [必要權限] 刀鋒視窗中，按一下 [API] 清單中的 [Windows Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="62400-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="62400-149">在 [啟用存取] 刀鋒視窗中，選取 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="62400-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="62400-151">在頂端工具列中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="62400-151">In the toolbar on the top, click **Save**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="62400-153">收集組態設定</span><span class="sxs-lookup"><span data-stu-id="62400-153">Gather configuration settings</span></span> 
<span data-ttu-id="62400-154">本節說明如何從您的目錄取得下列設定︰</span><span class="sxs-lookup"><span data-stu-id="62400-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="62400-155">網域名稱</span><span class="sxs-lookup"><span data-stu-id="62400-155">Domain name</span></span>
* <span data-ttu-id="62400-156">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="62400-156">Client ID</span></span>
* <span data-ttu-id="62400-157">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="62400-157">Client secret</span></span>

<span data-ttu-id="62400-158">您在設定報告 API 的呼叫時需要這些值。</span><span class="sxs-lookup"><span data-stu-id="62400-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="62400-159">取得您的網域名稱</span><span class="sxs-lookup"><span data-stu-id="62400-159">Get your domain name</span></span>

<span data-ttu-id="62400-160">**若要取得網域名稱：**</span><span class="sxs-lookup"><span data-stu-id="62400-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="62400-161">在 [Azure 入口網站](https://portal.azure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="62400-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="62400-163">在 [Azure Active Directory] 刀鋒視窗中，按一下 [網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="62400-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="62400-165">從網域清單中複製網域名稱。</span><span class="sxs-lookup"><span data-stu-id="62400-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="62400-166">取得應用程式的用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="62400-166">Get your application's client ID</span></span>

<span data-ttu-id="62400-167">**若要取得應用程式的用戶端識別碼：**</span><span class="sxs-lookup"><span data-stu-id="62400-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="62400-168">在 [Azure 入口網站](https://portal.azure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="62400-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="62400-170">在 [應用程式註冊] 刀鋒視窗中，按一下應用程式清單中的 [報告 API 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="62400-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="62400-171">在 [報告 API 應用程式] 刀鋒視窗中，按一下 [應用程式識別碼] 中的 [按一下以複製]。</span><span class="sxs-lookup"><span data-stu-id="62400-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="62400-173">取得應用程式的用戶端祕密</span><span class="sxs-lookup"><span data-stu-id="62400-173">Get your application's client secret</span></span>
<span data-ttu-id="62400-174">若要取得應用程式的用戶端密碼，您需要建立新的金鑰並在儲存新金鑰時儲存其值，因為稍後不可能再擷取此值。</span><span class="sxs-lookup"><span data-stu-id="62400-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="62400-175">**若要取得應用程式的用戶端祕密：**</span><span class="sxs-lookup"><span data-stu-id="62400-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="62400-176">在 [Azure 入口網站](https://portal.azure.com)中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="62400-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="62400-178">在 [應用程式註冊] 刀鋒視窗中，按一下應用程式清單中的 [報告 API 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="62400-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="62400-179">在 [報告 API 應用程式] 刀鋒視窗中，按一下頂端工具列中的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="62400-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="62400-181">在 [設定] 刀鋒視窗中，按一下 [APIR 存取] 區段中的 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="62400-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="62400-183">在 [金鑰] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="62400-183">On the **Keys** blade, perform the following steps:</span></span>

    ![註冊應用程式](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="62400-185">a.</span><span class="sxs-lookup"><span data-stu-id="62400-185">a.</span></span> <span data-ttu-id="62400-186">在 [描述] 文字方塊中，輸入 `Reporting API`。</span><span class="sxs-lookup"><span data-stu-id="62400-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="62400-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="62400-187">b.</span></span> <span data-ttu-id="62400-188">選取 [2 年後] 來作為 [到期]。</span><span class="sxs-lookup"><span data-stu-id="62400-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="62400-189">c.</span><span class="sxs-lookup"><span data-stu-id="62400-189">c.</span></span> <span data-ttu-id="62400-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="62400-190">Click **Save**.</span></span>

    <span data-ttu-id="62400-191">d.</span><span class="sxs-lookup"><span data-stu-id="62400-191">d.</span></span> <span data-ttu-id="62400-192">複製金鑰值。</span><span class="sxs-lookup"><span data-stu-id="62400-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="62400-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62400-193">Next Steps</span></span>
* <span data-ttu-id="62400-194">您要以程式設計方式從 Azure AD 報告 API 存取資料嗎？</span><span class="sxs-lookup"><span data-stu-id="62400-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="62400-195">請查看 [開始使用 Azure Active Directory 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="62400-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="62400-196">如果您想要深入了解 Azure Active Directory 報告，請參閱 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="62400-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

