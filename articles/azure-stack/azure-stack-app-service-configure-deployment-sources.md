---
title: "為 Azure Stack 上的應用程式服務設定部署來源 | Microsoft Docs"
description: "服務管理員該如何為 Azure Stack 上的 App Service 設定部署來源 (Git、GitHub、BitBucket、DropBox 和 OneDrive)"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: be4b032e8f7370f696c47a7b8e82c0a819529f4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-sources"></a><span data-ttu-id="2a3cb-103">設定部署來源</span><span class="sxs-lookup"><span data-stu-id="2a3cb-103">Configure deployment sources</span></span>

<span data-ttu-id="2a3cb-104">Azure Stack 上的 App Service 支援從多個原始檔控制提供者進行隨選部署。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-104">App Service on Azure Stack supports on-demand deployment from multiple Source Control Providers.</span></span>  <span data-ttu-id="2a3cb-105">這項功能可讓應用程式開發人員能夠直接從其原始檔控制儲存機制進行部署。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-105">This feature enables application developers to be able to deploy direct from their source control repositories.</span></span>  <span data-ttu-id="2a3cb-106">為了讓租用戶能夠設定 App Service 以連線至其儲存機制，系統管理員必須先設定 Azure Stack 上的 App Service 與原始檔控制提供者之間的整合。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-106">In order for tenants to be able to configure App Service to connect to their repositories, Administrators must first configure the integration between App Service on Azure Stack and the Source Control Provider.</span></span>  <span data-ttu-id="2a3cb-107">除了本機 Git 外，也支援下列原始檔控制提供者︰</span><span class="sxs-lookup"><span data-stu-id="2a3cb-107">The Source Control Providers supported, in addition to local Git, are:</span></span>

* <span data-ttu-id="2a3cb-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="2a3cb-108">GitHub</span></span>
* <span data-ttu-id="2a3cb-109">BitBucket</span><span class="sxs-lookup"><span data-stu-id="2a3cb-109">BitBucket</span></span>
* <span data-ttu-id="2a3cb-110">OneDrive</span><span class="sxs-lookup"><span data-stu-id="2a3cb-110">OneDrive</span></span>
* <span data-ttu-id="2a3cb-111">DropBox</span><span class="sxs-lookup"><span data-stu-id="2a3cb-111">DropBox</span></span>

## <a name="view-deployment-sources-in-app-service-administration"></a><span data-ttu-id="2a3cb-112">檢視 App Service 管理中的部署來源</span><span class="sxs-lookup"><span data-stu-id="2a3cb-112">View Deployment Sources in App Service Administration</span></span>

1. <span data-ttu-id="2a3cb-113">以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-113">Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span>
2. <span data-ttu-id="2a3cb-114">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-114">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span>
    <span data-ttu-id="2a3cb-115">![App Service 資源提供者管理][1]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-115">![App Service Resource Provider Admin][1]</span></span>
3. <span data-ttu-id="2a3cb-116">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-116">Click **Source control configuration**.</span></span>  <span data-ttu-id="2a3cb-117">您會在此看見所有已設定之部署來源的清單。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-117">Here you see the list of all Deployment Sources configured.</span></span>
    <span data-ttu-id="2a3cb-118">![App Service 資源提供者管理原始檔控制組態][2]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-118">![App Service Resource Provider Admin Source Control Configuration][2]</span></span>

## <a name="configure-github"></a><span data-ttu-id="2a3cb-119">設定 GitHub</span><span class="sxs-lookup"><span data-stu-id="2a3cb-119">Configure GitHub</span></span>

> [!NOTE]
> <span data-ttu-id="2a3cb-120">您需要有 GitHub 帳戶才能完成此工作。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-120">You require a GitHub account to complete this task.</span></span>  <span data-ttu-id="2a3cb-121">您可能會想要使用組織的帳戶，而非個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-121">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="2a3cb-122">登入 GitHub、瀏覽至 https://www.github.com/settings/developers ，然後按一下 [註冊新的應用程式] ![GitHub - 註冊新的應用程式][3]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-122">Log in to GitHub, browse to https://www.github.com/settings/developers and click **Register a new application** ![GitHub - Register a new application][3]</span></span>
2. <span data-ttu-id="2a3cb-123">輸入 [應用程式名稱]，例如，Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="2a3cb-123">Enter an **Application name** for example - App Service on Azure Stack</span></span>
3. <span data-ttu-id="2a3cb-124">輸入 [首頁 URL]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-124">Enter the **Homepage URL**.</span></span>  <span data-ttu-id="2a3cb-125">**首頁 URL 必須是 Azure Stack 入口網站位址**，例如 https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="2a3cb-125">**The Homepage URL must be the Azure Stack Portal address** for example - https://portal.local.azurestack.external</span></span>
4. <span data-ttu-id="2a3cb-126">輸入 [應用程式描述]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-126">Enter an **Application Description**</span></span>
5. <span data-ttu-id="2a3cb-127">輸入 [授權回呼 URL]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-127">Enter the **Authorization callback URL**.</span></span>  <span data-ttu-id="2a3cb-128">在預設的 Azure Stack 部署中，Url 的形式為 https://portal.local.azurestack.external/tokenauthorize ，如果您在不同的網域下執行，請以您的網域取代 azurestack.local ![GitHub - 使用填入的值註冊新的應用程式][4]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-128">In a default Azure Stack deployment, the Url is in the form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![GitHub - Register a new application with values populated][4]</span></span>
6. <span data-ttu-id="2a3cb-129">按一下 [註冊應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-129">Click **Register application**.</span></span>  <span data-ttu-id="2a3cb-130">您現在會看到列出應用程式之 [用戶端識別碼] 和 [用戶端密碼] 的頁面。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-130">You will now be presented with a page listing the **Client ID** and **Client Secret** for the application.</span></span>
    <span data-ttu-id="2a3cb-131">![GitHub - 已完成的應用程式註冊][5]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-131">![GitHub - Completed application registration][5]</span></span>
7.  <span data-ttu-id="2a3cb-132">在新的瀏覽器索引標籤或視窗中，以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-132">In a new browser tab or window Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span> 
8.  <span data-ttu-id="2a3cb-133">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-133">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
9. <span data-ttu-id="2a3cb-134">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-134">Click **Source control configuration**.</span></span>
10. <span data-ttu-id="2a3cb-135">複製 [用戶端識別碼] 和 [用戶端密碼] 並貼到對應的 GitHub 輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-135">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span></span>
11. <span data-ttu-id="2a3cb-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-136">Click **Save**.</span></span>
12. <span data-ttu-id="2a3cb-137">如果您不想設定任何其他部署來源，請繼續[排程管理角色的修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-137">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>


## <a name="configure-bitbucket"></a><span data-ttu-id="2a3cb-138">設定 BitBucket</span><span class="sxs-lookup"><span data-stu-id="2a3cb-138">Configure BitBucket</span></span>

> [!NOTE]
> <span data-ttu-id="2a3cb-139">您需要有 BitBucket 帳戶才能完成此工作。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-139">You require a BitBucket account to complete this task.</span></span>  <span data-ttu-id="2a3cb-140">您可能會想要使用組織的帳戶，而非個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-140">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="2a3cb-141">登入 BitBucket，然後瀏覽至您帳戶底下的 [整合] ![BitBucket 儀表板 - 整合][7]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-141">Log in to BitBucket and browse to **Integrations** under your account  ![BitBucket Dashboard - Integrations][7]</span></span>
2. <span data-ttu-id="2a3cb-142">按一下 [存取管理] 底下的 [OAuth] 與 [新增取用者] ![BitBucket 新增 OAuth 取用者][8]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-142">Click **OAuth** under Access Management and **Add consumer** ![BitBucket Add OAuth Consumer][8]</span></span>
3. <span data-ttu-id="2a3cb-143">輸入取用者的 [名稱]，例如，Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="2a3cb-143">Enter a **Name** for the consumer, for example App Service on Azure Stack</span></span>
4. <span data-ttu-id="2a3cb-144">輸入應用程式的 [描述]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-144">Enter a **Description** for the application</span></span>
5. <span data-ttu-id="2a3cb-145">輸入 [回呼 URL]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-145">Enter the **Callback URL**.</span></span>  <span data-ttu-id="2a3cb-146">在預設的 Azure Stack 部署中，回呼 Url 的形式為 https://portal.local.azurestack.external/TokenAuthorize ，如果您在不同的網域下執行，請以您的網域取代 azurestack.local。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-146">In a default Azure Stack deployment, the Callback Url is in the form https://portal.local.azurestack.external/TokenAuthorize, if you are running under a different domain substitute your domain for azurestack.local.</span></span>  <span data-ttu-id="2a3cb-147">Url 必須按照此處列出的大小寫，BitBucket 整合才能成功。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-147">The Url must follow the capitalization as listed here for BitBucket integration to succeed.</span></span>
6. <span data-ttu-id="2a3cb-148">輸入 **URL**，此 Url 應為 Azure Stack 入口網站 URL，例如 https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="2a3cb-148">Enter the **URL** - this Url should be the Azure Stack Portal URL, for example https://portal.local.azurestack.external</span></span>
7. <span data-ttu-id="2a3cb-149">選取所需**權限** -  **存放庫**: **讀取** **Webhook**: **讀取及寫入**</span><span class="sxs-lookup"><span data-stu-id="2a3cb-149">Select the **Permissions** required  **Repositories**: **Read** **Webhooks**: **Read and write**</span></span>
8. <span data-ttu-id="2a3cb-150">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-150">Click **Save**.</span></span>  <span data-ttu-id="2a3cb-151">您現在會看到這個新的應用程式，以及 **OAuth 取用者**底下的**金鑰**和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-151">You will now see this new application, along with the **Key** and **Secret** under **OAuth consumers**.</span></span>
    <span data-ttu-id="2a3cb-152">![BitBucket 應用程式清單][9]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-152">![BitBucket Application Listing][9]</span></span>
9.  <span data-ttu-id="2a3cb-153">在新的瀏覽器索引標籤或視窗中，以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-153">In a new browser tab or window Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span> 
10.  <span data-ttu-id="2a3cb-154">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-154">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="2a3cb-155">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-155">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="2a3cb-156">複製**金鑰**並貼到 BitBucket 的 [用戶端識別碼] 輸入方塊，以及複製**密碼**並貼到 BitBucket 的 [用戶端密碼] 輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-156">Copy and paste the **Key** into the **Client Id** input box and **Secret** into the **Client Secret** input box for BitBucket.</span></span>
13. <span data-ttu-id="2a3cb-157">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-157">Click **Save**.</span></span>
14. <span data-ttu-id="2a3cb-158">如果您不想設定任何其他部署來源，請繼續[排程管理角色的修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-158">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-onedrive"></a><span data-ttu-id="2a3cb-159">設定 OneDrive</span><span class="sxs-lookup"><span data-stu-id="2a3cb-159">Configure OneDrive</span></span>

> [!NOTE]
> <span data-ttu-id="2a3cb-160">目前不支援商務用 OneDrive 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-160">OneDrive for Business Accounts are not currently supported.</span></span>  <span data-ttu-id="2a3cb-161">您必須有連結到 OneDrive 帳戶的 Microsoft 帳戶，才能完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-161">You need to have a Microsoft Account linked to a OneDrive account to complete this task.</span></span>  <span data-ttu-id="2a3cb-162">您可能會想要使用組織的帳戶，而非個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-162">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="2a3cb-163">瀏覽至 https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm 並使用 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-163">Browse to https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm and Log in using your Microsoft Account.</span></span>
2. <span data-ttu-id="2a3cb-164">按一下 [我的應用程式] 底下的 [新增應用程式]
![OneDrive 應用程式][10]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-164">Click **Add an app** under **My applications**
![OneDrive Applications][10]</span></span>
3. <span data-ttu-id="2a3cb-165">為新的應用程式註冊輸入**名稱**，輸入 **Azure Stack 上的 App Service**，然後按一下 [建立應用程式]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-165">Enter a **Name** for the New Application Registration, enter **App Service on Azure Stack**, and click **Create Application**</span></span>
4. <span data-ttu-id="2a3cb-166">下一個畫面會列出新應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-166">The next screen lists the properties of your new application.</span></span> <span data-ttu-id="2a3cb-167">記錄下**應用程式識別碼**
![OneDrive 應用程式屬性][11]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-167">Record the **Application Id**
![OneDrive Application Properties][11]</span></span>
5. <span data-ttu-id="2a3cb-168">在 [應用程式密碼] 底下按一下 [產生新密碼]，然後記錄**所產生的新密碼** - 這是您的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-168">Under **Application Secrets** click **Generate New Password** and record the **New password generated** - this is your application secret.</span></span>
> [!NOTE]
> <span data-ttu-id="2a3cb-169">請務必記下新密碼，因為一旦您在此階段按一下 [確定] 後就無法再擷取。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-169">Make sure to make a note of the new password as it is not retrievable once you click OK at this stage.</span></span>
6. <span data-ttu-id="2a3cb-170">在 [平台] 下，按一下 [新增平台]，然後選取 [網站]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-170">Under **Platforms** click **Add Platform** and select **Web**</span></span>
7. <span data-ttu-id="2a3cb-171">輸入 [重新導向 URI]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-171">Enter the **Redirect URI**.</span></span>  <span data-ttu-id="2a3cb-172">在預設的 Azure Stack 部署中，重新導向 URI 的形式為 https://portal.local.azurestack.external/tokenauthorize ，如果您在不同的網域下執行，請以您的網域取代 azurestack.local ![OneDrive 應用程式 - 新增 Web 平台][12]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-172">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![OneDrive Application - Add Web Platform][12]</span></span>
8. <span data-ttu-id="2a3cb-173">設定 [Microsoft Graph 權限] - [委派權限]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-173">Set the **Microsoft Graph Permissions** - **Delegated Permissions**</span></span>
    - <span data-ttu-id="2a3cb-174">**Files.ReadWrite.AppFolder**</span><span class="sxs-lookup"><span data-stu-id="2a3cb-174">**Files.ReadWrite.AppFolder**</span></span>
    - <span data-ttu-id="2a3cb-175">**User.Read**</span><span class="sxs-lookup"><span data-stu-id="2a3cb-175">**User.Read**</span></span>  
      <span data-ttu-id="2a3cb-176">![OneDrive 應用程式 - Graph 權限][13]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-176">![OneDrive Application - Graph Permissions][13]</span></span>
10. <span data-ttu-id="2a3cb-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-177">Click **Save**.</span></span>
11.  <span data-ttu-id="2a3cb-178">在新的瀏覽器索引標籤或視窗中，以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-178">In a new browser tab or window Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span> 
12.  <span data-ttu-id="2a3cb-179">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-179">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
13. <span data-ttu-id="2a3cb-180">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-180">Click **Source control configuration**.</span></span>
14. <span data-ttu-id="2a3cb-181">複製**應用程式識別碼**並貼到 OneDrive 的 [用戶端識別碼] 輸入方塊，以及複製**密碼**並貼到 OneDrive 的 [用戶端密碼] 輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-181">Copy and paste the **Application Id** into the **Client Id** input box and **Password** into the **Client Secret** input box for OneDrive.</span></span>
15. <span data-ttu-id="2a3cb-182">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-182">Click **Save**.</span></span>
16. <span data-ttu-id="2a3cb-183">如果您不想設定任何其他部署來源，請繼續[排程管理角色的修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-183">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-dropbox"></a><span data-ttu-id="2a3cb-184">設定 DropBox</span><span class="sxs-lookup"><span data-stu-id="2a3cb-184">Configure DropBox</span></span>

> [!NOTE]
> <span data-ttu-id="2a3cb-185">您必須有 DropBox 帳戶才能完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-185">You need to have a DropBox account to complete this task.</span></span>  <span data-ttu-id="2a3cb-186">您可能會想要使用組織的帳戶，而非個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-186">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="2a3cb-187">瀏覽至 https://www.dropbox.com/developers/apps，並使用 DropBox 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="2a3cb-187">Browse to https://www.dropbox.com/developers/apps and Log in using your DropBox Account</span></span>
2. <span data-ttu-id="2a3cb-188">按一下 [建立應用程式]**** 
![Dropbox 應用程式][14]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-188">Click **Create app** 
![Dropbox applications][14]</span></span>
3. <span data-ttu-id="2a3cb-189">選取 [DropBox API]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-189">Select **DropBox API**</span></span>
4. <span data-ttu-id="2a3cb-190">將存取層級設為 [應用程式資料夾]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-190">Set the access level to **App Folder**</span></span>
5. <span data-ttu-id="2a3cb-191">輸入應用程式的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-191">Enter a **Name** for your application.</span></span>
<span data-ttu-id="2a3cb-192">![Dropbox 應用程式註冊][15]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-192">![Dropbox application registration][15]</span></span>
6. <span data-ttu-id="2a3cb-193">按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-193">Click **Create App**.</span></span>  <span data-ttu-id="2a3cb-194">您現在會看到列出應用程式設定的頁面，包括**應用程式金鑰**和**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-194">You will now be presented with a page listing the settings for the App including **App key** and **App secret**.</span></span>
7. <span data-ttu-id="2a3cb-195">確認 [應用程式資料夾名稱] 已設為 **Azure Stack 上的 App Service**</span><span class="sxs-lookup"><span data-stu-id="2a3cb-195">Check the **App folder name** is set to **App Service on Azure Stack**</span></span>
8. <span data-ttu-id="2a3cb-196">設定 [OAuth 2 重新導向 URI]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-196">Set the **OAuth 2 Redirect URI** and click **Add**.</span></span>  <span data-ttu-id="2a3cb-197">在預設的 Azure Stack 部署中，重新導向 URI 的形式為 https://portal.local.azurestack.external/tokenauthorize ，如果您在不同的網域下執行，請以您的網域取代 azurestack.local ![Dropbox 應用程式設定][16]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-197">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![Dropbox application configuration][16]</span></span>
9.  <span data-ttu-id="2a3cb-198">在新的瀏覽器索引標籤或視窗中，以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-198">In a new browser tab or window Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span> 
10.  <span data-ttu-id="2a3cb-199">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-199">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="2a3cb-200">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-200">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="2a3cb-201">複製**應用程式金鑰**並貼到 DropBox 的 [用戶端識別碼] 輸入方塊，以及複製**應用程式密碼**並貼到 DropBox 的 [用戶端密碼] 輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-201">Copy and paste the **Application Key** into the **Client Id** input box and **App secret** into the **Client Secret** input box for DropBox.</span></span>
13. <span data-ttu-id="2a3cb-202">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-202">Click **Save**.</span></span>
14. <span data-ttu-id="2a3cb-203">如果您不想設定任何其他部署來源，請繼續[排程管理角色的修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-203">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="schedule-repair-of-management-roles"></a><span data-ttu-id="2a3cb-204">排程管理角色的修復</span><span class="sxs-lookup"><span data-stu-id="2a3cb-204">Schedule repair of management roles</span></span>
<span data-ttu-id="2a3cb-205">為了套用各種部署來源組態中所更新的設定，您必須修復管理角色。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-205">In order for the settings updated in the configuration of the various deployment sources to be applied, the Management Roles need to be repaired.</span></span>  <span data-ttu-id="2a3cb-206">此程序可確保組態值能夠正確套用，並將所設定的部署來源提供給租用戶使用。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-206">This process ensures that the configuration values are applied correctly and the configured Deployment Sources are made available to tenants.</span></span>

1. <span data-ttu-id="2a3cb-207">在新的瀏覽器索引標籤或視窗中，以服務管理員身分登入 Azure Stack 管理入口網站 ( https://adminportal.local.azurestack.external )。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-207">In a new browser tab or window Log in to the Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as the service administrator.</span></span>
2. <span data-ttu-id="2a3cb-208">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-208">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span>
3. <span data-ttu-id="2a3cb-209">按一下 [原始檔控制組態]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-209">Click **Source control configuration**</span></span>
4. <span data-ttu-id="2a3cb-210">複製 [用戶端識別碼] 和 [用戶端密碼] 並貼到對應的 GitHub 輸入方塊。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-210">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span></span>
5. <span data-ttu-id="2a3cb-211">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="2a3cb-211">Click **Save**</span></span>
6. <span data-ttu-id="2a3cb-212">按一下 [角色]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-212">Click **Roles**</span></span>
7. <span data-ttu-id="2a3cb-213">按一下 [管理伺服器]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-213">Click **Management Server**</span></span>
8. <span data-ttu-id="2a3cb-214">按一下 [全部修復]，然後選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-214">Click **Repair All** and select **Yes**.</span></span>  <span data-ttu-id="2a3cb-215">這項作業會在所有管理伺服器上排程修復作業，以便完成整合。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-215">This operation schedules a repair on all Management Servers to complete the integration.</span></span>  <span data-ttu-id="2a3cb-216">修復作業會受到控管，以將停機時間降低最低。</span><span class="sxs-lookup"><span data-stu-id="2a3cb-216">The repair operations are managed to minimize downtime.</span></span>
    <span data-ttu-id="2a3cb-217">![App Service 資源提供者管理 - 角色 - 管理伺服器全部修復][6]</span><span class="sxs-lookup"><span data-stu-id="2a3cb-217">![App Service Resource Provider Admin - Roles - Management Server Repair All][6]</span></span>

<!--Image references-->
[1]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
