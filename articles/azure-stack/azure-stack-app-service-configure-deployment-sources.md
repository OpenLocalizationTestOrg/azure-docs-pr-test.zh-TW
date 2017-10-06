---
title: "aaaConfigure Azure 堆疊上的應用程式服務的部署來源 |Microsoft 文件"
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
ms.openlocfilehash: 2eaf0a7f4b6e52d64a302000c1dd3c3eb5d6a6ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-sources"></a><span data-ttu-id="c1341-103">設定部署來源</span><span class="sxs-lookup"><span data-stu-id="c1341-103">Configure deployment sources</span></span>

<span data-ttu-id="c1341-104">Azure Stack 上的 App Service 支援從多個原始檔控制提供者進行隨選部署。</span><span class="sxs-lookup"><span data-stu-id="c1341-104">App Service on Azure Stack supports on-demand deployment from multiple Source Control Providers.</span></span>  <span data-ttu-id="c1341-105">此功能可讓應用程式開發人員 toobe 無法 toodeploy 直接從其原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c1341-105">This feature enables application developers toobe able toodeploy direct from their source control repositories.</span></span>  <span data-ttu-id="c1341-106">若要為租用戶 toobe 無法 tooconfigure App Service tooconnect tootheir 儲存機制、 系統管理員必須先設定 hello Azure 堆疊上的應用程式服務之間的整合和 hello 原始檔控制提供者。</span><span class="sxs-lookup"><span data-stu-id="c1341-106">In order for tenants toobe able tooconfigure App Service tooconnect tootheir repositories, Administrators must first configure hello integration between App Service on Azure Stack and hello Source Control Provider.</span></span>  <span data-ttu-id="c1341-107">hello 原始檔控制提供者支援，此外 toolocal Git，如下：</span><span class="sxs-lookup"><span data-stu-id="c1341-107">hello Source Control Providers supported, in addition toolocal Git, are:</span></span>

* <span data-ttu-id="c1341-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="c1341-108">GitHub</span></span>
* <span data-ttu-id="c1341-109">BitBucket</span><span class="sxs-lookup"><span data-stu-id="c1341-109">BitBucket</span></span>
* <span data-ttu-id="c1341-110">OneDrive</span><span class="sxs-lookup"><span data-stu-id="c1341-110">OneDrive</span></span>
* <span data-ttu-id="c1341-111">DropBox</span><span class="sxs-lookup"><span data-stu-id="c1341-111">DropBox</span></span>

## <a name="view-deployment-sources-in-app-service-administration"></a><span data-ttu-id="c1341-112">檢視 App Service 管理中的部署來源</span><span class="sxs-lookup"><span data-stu-id="c1341-112">View Deployment Sources in App Service Administration</span></span>

1. <span data-ttu-id="c1341-113">Hello 服務系統管理員身分登入 toohello Azure 堆疊系統管理入口網站 (https://adminportal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="c1341-113">Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span>
2. <span data-ttu-id="c1341-114">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。![App Service 資源提供者管理][1]</span><span class="sxs-lookup"><span data-stu-id="c1341-114">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.  ![App Service Resource Provider Admin][1]</span></span>
3. <span data-ttu-id="c1341-115">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="c1341-115">Click **Source control configuration**.</span></span>  <span data-ttu-id="c1341-116">這裡您會看到所有設定的部署來源 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="c1341-116">Here you see hello list of all Deployment Sources configured.</span></span>
    <span data-ttu-id="c1341-117">![App Service 資源提供者管理原始檔控制組態][2]</span><span class="sxs-lookup"><span data-stu-id="c1341-117">![App Service Resource Provider Admin Source Control Configuration][2]</span></span>

## <a name="configure-github"></a><span data-ttu-id="c1341-118">設定 GitHub</span><span class="sxs-lookup"><span data-stu-id="c1341-118">Configure GitHub</span></span>

> [!NOTE]
> <span data-ttu-id="c1341-119">需要 GitHub 帳戶 toocomplete 這項工作。</span><span class="sxs-lookup"><span data-stu-id="c1341-119">You require a GitHub account toocomplete this task.</span></span>  <span data-ttu-id="c1341-120">您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1341-120">You may wish toouse an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="c1341-121">登入 tooGitHub，瀏覽 toohttps://www.github.com/settings/developers 並按一下**註冊新的應用程式** ![GitHub-註冊新的應用程式][3]</span><span class="sxs-lookup"><span data-stu-id="c1341-121">Log in tooGitHub, browse toohttps://www.github.com/settings/developers and click **Register a new application** ![GitHub - Register a new application][3]</span></span>
2. <span data-ttu-id="c1341-122">輸入 [應用程式名稱]，例如，Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="c1341-122">Enter an **Application name** for example - App Service on Azure Stack</span></span>
3. <span data-ttu-id="c1341-123">輸入 hello**首頁 URL**。</span><span class="sxs-lookup"><span data-stu-id="c1341-123">Enter hello **Homepage URL**.</span></span>  <span data-ttu-id="c1341-124">**hello 首頁 URL 必須是 hello Azure 堆疊入口網站位址**例如-https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c1341-124">**hello Homepage URL must be hello Azure Stack Portal address** for example - https://portal.local.azurestack.external</span></span>
4. <span data-ttu-id="c1341-125">輸入 [應用程式描述]</span><span class="sxs-lookup"><span data-stu-id="c1341-125">Enter an **Application Description**</span></span>
5. <span data-ttu-id="c1341-126">輸入 hello**授權回呼 URL**。</span><span class="sxs-lookup"><span data-stu-id="c1341-126">Enter hello **Authorization callback URL**.</span></span>  <span data-ttu-id="c1341-127">在預設 Azure 堆疊部署中，hello Url 是 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![GitHub-註冊新的應用程式以填入的值][4]</span><span class="sxs-lookup"><span data-stu-id="c1341-127">In a default Azure Stack deployment, hello Url is in hello form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![GitHub - Register a new application with values populated][4]</span></span>
6. <span data-ttu-id="c1341-128">按一下 [註冊應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c1341-128">Click **Register application**.</span></span>  <span data-ttu-id="c1341-129">您現在會以頁面清單 hello**用戶端識別碼**和**用戶端密碼**hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1341-129">You will now be presented with a page listing hello **Client ID** and **Client Secret** for hello application.</span></span>
    <span data-ttu-id="c1341-130">![GitHub - 已完成的應用程式註冊][5]</span><span class="sxs-lookup"><span data-stu-id="c1341-130">![GitHub - Completed application registration][5]</span></span>
7.  <span data-ttu-id="c1341-131">在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c1341-131">In a new browser tab or window Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span> 
8.  <span data-ttu-id="c1341-132">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1341-132">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.</span></span> 
9. <span data-ttu-id="c1341-133">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="c1341-133">Click **Source control configuration**.</span></span>
10. <span data-ttu-id="c1341-134">複製並貼上 hello**用戶端識別碼**和**用戶端密碼**hello 對應輸入方塊中的 GitHub。</span><span class="sxs-lookup"><span data-stu-id="c1341-134">Copy and paste hello **Client Id** and **Client Secret** into hello corresponding input boxes for GitHub.</span></span>
11. <span data-ttu-id="c1341-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-135">Click **Save**.</span></span>
12. <span data-ttu-id="c1341-136">如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="c1341-136">If you do not wish tooconfigure any other Deployment Sources, proceed too[Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>


## <a name="configure-bitbucket"></a><span data-ttu-id="c1341-137">設定 BitBucket</span><span class="sxs-lookup"><span data-stu-id="c1341-137">Configure BitBucket</span></span>

> [!NOTE]
> <span data-ttu-id="c1341-138">這項工作需要 BitBucket 帳戶 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="c1341-138">You require a BitBucket account toocomplete this task.</span></span>  <span data-ttu-id="c1341-139">您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1341-139">You may wish toouse an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="c1341-140">登入 tooBitBucket 並瀏覽過**整合**您帳戶![BitBucket 儀表板-整合][7]</span><span class="sxs-lookup"><span data-stu-id="c1341-140">Log in tooBitBucket and browse too**Integrations** under your account  ![BitBucket Dashboard - Integrations][7]</span></span>
2. <span data-ttu-id="c1341-141">按一下 [存取管理] 底下的 [OAuth] 與 [新增取用者] ![BitBucket 新增 OAuth 取用者][8]</span><span class="sxs-lookup"><span data-stu-id="c1341-141">Click **OAuth** under Access Management and **Add consumer** ![BitBucket Add OAuth Consumer][8]</span></span>
3. <span data-ttu-id="c1341-142">輸入**名稱**hello 取用者，例如 Azure 堆疊上的應用程式服務</span><span class="sxs-lookup"><span data-stu-id="c1341-142">Enter a **Name** for hello consumer, for example App Service on Azure Stack</span></span>
4. <span data-ttu-id="c1341-143">輸入**描述**hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c1341-143">Enter a **Description** for hello application</span></span>
5. <span data-ttu-id="c1341-144">輸入 hello**回呼 URL**。</span><span class="sxs-lookup"><span data-stu-id="c1341-144">Enter hello **Callback URL**.</span></span>  <span data-ttu-id="c1341-145">在預設 Azure 堆疊部署中，回呼 Url hello 處於 hello 表單 https://portal.local.azurestack.external/TokenAuthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local。</span><span class="sxs-lookup"><span data-stu-id="c1341-145">In a default Azure Stack deployment, hello Callback Url is in hello form https://portal.local.azurestack.external/TokenAuthorize, if you are running under a different domain substitute your domain for azurestack.local.</span></span>  <span data-ttu-id="c1341-146">hello Url 必須遵循此處所列的 BitBucket 整合 toosucceed hello 大小寫。</span><span class="sxs-lookup"><span data-stu-id="c1341-146">hello Url must follow hello capitalization as listed here for BitBucket integration toosucceed.</span></span>
6. <span data-ttu-id="c1341-147">輸入 hello **URL** -此 Url 應 hello Azure 堆疊入口網站 URL，例如 https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c1341-147">Enter hello **URL** - this Url should be hello Azure Stack Portal URL, for example https://portal.local.azurestack.external</span></span>
7. <span data-ttu-id="c1341-148">選取 hello**權限**必要**儲存機制**:**讀取** **Webhook**:**讀取和寫入**</span><span class="sxs-lookup"><span data-stu-id="c1341-148">Select hello **Permissions** required  **Repositories**: **Read** **Webhooks**: **Read and write**</span></span>
8. <span data-ttu-id="c1341-149">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-149">Click **Save**.</span></span>  <span data-ttu-id="c1341-150">您現在可以看到這個新的應用程式，以及 hello**金鑰**和**密碼**下**OAuth 取用者**。</span><span class="sxs-lookup"><span data-stu-id="c1341-150">You will now see this new application, along with hello **Key** and **Secret** under **OAuth consumers**.</span></span>
    <span data-ttu-id="c1341-151">![BitBucket 應用程式清單][9]</span><span class="sxs-lookup"><span data-stu-id="c1341-151">![BitBucket Application Listing][9]</span></span>
9.  <span data-ttu-id="c1341-152">在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c1341-152">In a new browser tab or window Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span> 
10.  <span data-ttu-id="c1341-153">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1341-153">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="c1341-154">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="c1341-154">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="c1341-155">複製並貼上 hello**金鑰**到 hello**用戶端識別碼**輸入的方塊和**密碼**到 hello**用戶端密碼**是 bitbucket 適用的輸入的方塊。</span><span class="sxs-lookup"><span data-stu-id="c1341-155">Copy and paste hello **Key** into hello **Client Id** input box and **Secret** into hello **Client Secret** input box for BitBucket.</span></span>
13. <span data-ttu-id="c1341-156">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-156">Click **Save**.</span></span>
14. <span data-ttu-id="c1341-157">如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="c1341-157">If you do not wish tooconfigure any other Deployment Sources, proceed too[Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-onedrive"></a><span data-ttu-id="c1341-158">設定 OneDrive</span><span class="sxs-lookup"><span data-stu-id="c1341-158">Configure OneDrive</span></span>

> [!NOTE]
> <span data-ttu-id="c1341-159">目前不支援商務用 OneDrive 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1341-159">OneDrive for Business Accounts are not currently supported.</span></span>  <span data-ttu-id="c1341-160">您需要 Microsoft 帳戶連結 tooa OneDrive 帳戶 toocomplete toohave 這項工作。</span><span class="sxs-lookup"><span data-stu-id="c1341-160">You need toohave a Microsoft Account linked tooa OneDrive account toocomplete this task.</span></span>  <span data-ttu-id="c1341-161">您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1341-161">You may wish toouse an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="c1341-162">瀏覽 toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm 並使用您的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c1341-162">Browse toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm and Log in using your Microsoft Account.</span></span>
2. <span data-ttu-id="c1341-163">按一下 [我的應用程式] 底下的 [新增應用程式]
![OneDrive 應用程式][10]</span><span class="sxs-lookup"><span data-stu-id="c1341-163">Click **Add an app** under **My applications**
![OneDrive Applications][10]</span></span>
3. <span data-ttu-id="c1341-164">輸入**名稱**hello 新應用程式註冊，請輸入**Azure 堆疊上的應用程式服務**，然後按一下**建立應用程式**</span><span class="sxs-lookup"><span data-stu-id="c1341-164">Enter a **Name** for hello New Application Registration, enter **App Service on Azure Stack**, and click **Create Application**</span></span>
4. <span data-ttu-id="c1341-165">hello 下一個畫面會列出新的應用程式的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c1341-165">hello next screen lists hello properties of your new application.</span></span> <span data-ttu-id="c1341-166">記錄 hello**應用程式識別碼**
![OneDrive 應用程式屬性][11]</span><span class="sxs-lookup"><span data-stu-id="c1341-166">Record hello **Application Id**
![OneDrive Application Properties][11]</span></span>
5. <span data-ttu-id="c1341-167">在下**應用程式密碼**按一下**產生新的密碼**和記錄 hello**產生新密碼**-這是您的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="c1341-167">Under **Application Secrets** click **Generate New Password** and record hello **New password generated** - this is your application secret.</span></span>
> [!NOTE]
> <span data-ttu-id="c1341-168">記下確定 toomake hello 新密碼不是可擷取當您在此階段按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c1341-168">Make sure toomake a note of hello new password as it is not retrievable once you click OK at this stage.</span></span>
6. <span data-ttu-id="c1341-169">在 [平台] 下，按一下 [新增平台]，然後選取 [網站]</span><span class="sxs-lookup"><span data-stu-id="c1341-169">Under **Platforms** click **Add Platform** and select **Web**</span></span>
7. <span data-ttu-id="c1341-170">輸入 hello**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="c1341-170">Enter hello **Redirect URI**.</span></span>  <span data-ttu-id="c1341-171">在預設 Azure 堆疊部署中，重新導向 URI hello 處於 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![OneDrive 應用程式-加入 Web 平台][12]</span><span class="sxs-lookup"><span data-stu-id="c1341-171">In a default Azure Stack deployment, hello Redirect URI is in hello form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![OneDrive Application - Add Web Platform][12]</span></span>
8. <span data-ttu-id="c1341-172">設定 hello **Microsoft Graph 權限** - **委派的權限**</span><span class="sxs-lookup"><span data-stu-id="c1341-172">Set hello **Microsoft Graph Permissions** - **Delegated Permissions**</span></span>
    - <span data-ttu-id="c1341-173">**Files.ReadWrite.AppFolder**</span><span class="sxs-lookup"><span data-stu-id="c1341-173">**Files.ReadWrite.AppFolder**</span></span>
    - <span data-ttu-id="c1341-174">**User.Read**</span><span class="sxs-lookup"><span data-stu-id="c1341-174">**User.Read**</span></span>  
      <span data-ttu-id="c1341-175">![OneDrive 應用程式 - Graph 權限][13]</span><span class="sxs-lookup"><span data-stu-id="c1341-175">![OneDrive Application - Graph Permissions][13]</span></span>
10. <span data-ttu-id="c1341-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-176">Click **Save**.</span></span>
11.  <span data-ttu-id="c1341-177">在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c1341-177">In a new browser tab or window Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span> 
12.  <span data-ttu-id="c1341-178">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1341-178">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.</span></span> 
13. <span data-ttu-id="c1341-179">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="c1341-179">Click **Source control configuration**.</span></span>
14. <span data-ttu-id="c1341-180">複製並貼上 hello**應用程式識別碼**到 hello**用戶端識別碼**輸入的方塊和**密碼**到 hello**用戶端密碼**輸入的方塊OneDrive。</span><span class="sxs-lookup"><span data-stu-id="c1341-180">Copy and paste hello **Application Id** into hello **Client Id** input box and **Password** into hello **Client Secret** input box for OneDrive.</span></span>
15. <span data-ttu-id="c1341-181">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-181">Click **Save**.</span></span>
16. <span data-ttu-id="c1341-182">如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="c1341-182">If you do not wish tooconfigure any other Deployment Sources, proceed too[Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-dropbox"></a><span data-ttu-id="c1341-183">設定 DropBox</span><span class="sxs-lookup"><span data-stu-id="c1341-183">Configure DropBox</span></span>

> [!NOTE]
> <span data-ttu-id="c1341-184">您需要 toohave DropBox 帳戶 toocomplete 這項工作。</span><span class="sxs-lookup"><span data-stu-id="c1341-184">You need toohave a DropBox account toocomplete this task.</span></span>  <span data-ttu-id="c1341-185">您可能希望 toouse 帳戶，您的組織，而不是個人的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1341-185">You may wish toouse an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="c1341-186">瀏覽 toohttps://www.dropbox.com/developers/apps 和使用您的 DropBox 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="c1341-186">Browse toohttps://www.dropbox.com/developers/apps and Log in using your DropBox Account</span></span>
2. <span data-ttu-id="c1341-187">按一下 **建立應用程式** 
![Dropbox 應用程式][14]</span><span class="sxs-lookup"><span data-stu-id="c1341-187">Click **Create app** 
![Dropbox applications][14]</span></span>
3. <span data-ttu-id="c1341-188">選取 [DropBox API]</span><span class="sxs-lookup"><span data-stu-id="c1341-188">Select **DropBox API**</span></span>
4. <span data-ttu-id="c1341-189">設定 hello 存取層級太**應用程式的資料夾**</span><span class="sxs-lookup"><span data-stu-id="c1341-189">Set hello access level too**App Folder**</span></span>
5. <span data-ttu-id="c1341-190">輸入應用程式的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="c1341-190">Enter a **Name** for your application.</span></span>
<span data-ttu-id="c1341-191">![Dropbox 應用程式註冊][15]</span><span class="sxs-lookup"><span data-stu-id="c1341-191">![Dropbox application registration][15]</span></span>
6. <span data-ttu-id="c1341-192">按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c1341-192">Click **Create App**.</span></span>  <span data-ttu-id="c1341-193">您現在會看到與頁面列出 hello 設定 hello 應用程式包括**應用程式金鑰**和**應用程式秘鑰**。</span><span class="sxs-lookup"><span data-stu-id="c1341-193">You will now be presented with a page listing hello settings for hello App including **App key** and **App secret**.</span></span>
7. <span data-ttu-id="c1341-194">檢查 hello**應用程式資料夾名稱**設定得**Azure 堆疊上的應用程式服務**</span><span class="sxs-lookup"><span data-stu-id="c1341-194">Check hello **App folder name** is set too**App Service on Azure Stack**</span></span>
8. <span data-ttu-id="c1341-195">設定 hello **OAuth 2 重新導向 URI**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="c1341-195">Set hello **OAuth 2 Redirect URI** and click **Add**.</span></span>  <span data-ttu-id="c1341-196">在預設 Azure 堆疊部署中，重新導向 URI hello 處於 hello 表單 https://portal.local.azurestack.external/tokenauthorize，如果您在不同的網域取代下執行網域中的為 azurestack.local ![Dropbox 應用程式組態][16]</span><span class="sxs-lookup"><span data-stu-id="c1341-196">In a default Azure Stack deployment, hello Redirect URI is in hello form https://portal.local.azurestack.external/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![Dropbox application configuration][16]</span></span>
9.  <span data-ttu-id="c1341-197">在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c1341-197">In a new browser tab or window Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span> 
10.  <span data-ttu-id="c1341-198">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1341-198">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="c1341-199">按一下 [原始檔控制組態]。</span><span class="sxs-lookup"><span data-stu-id="c1341-199">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="c1341-200">複製並貼上 hello**應用程式金鑰**到 hello**用戶端識別碼**輸入的方塊和**應用程式秘鑰**到 hello**用戶端密碼**輸入的方塊DropBox。</span><span class="sxs-lookup"><span data-stu-id="c1341-200">Copy and paste hello **Application Key** into hello **Client Id** input box and **App secret** into hello **Client Secret** input box for DropBox.</span></span>
13. <span data-ttu-id="c1341-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c1341-201">Click **Save**.</span></span>
14. <span data-ttu-id="c1341-202">如果您不想 tooconfigure 任何其他的部署來源，繼續太[的管理角色排程修復](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles)。</span><span class="sxs-lookup"><span data-stu-id="c1341-202">If you do not wish tooconfigure any other Deployment Sources, proceed too[Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="schedule-repair-of-management-roles"></a><span data-ttu-id="c1341-203">排程管理角色的修復</span><span class="sxs-lookup"><span data-stu-id="c1341-203">Schedule repair of management roles</span></span>
<span data-ttu-id="c1341-204">為了讓更新 hello hello 組態中的 hello 設定不同的部署來源 toobe 套用，hello 管理角色需要 toobe 修復。</span><span class="sxs-lookup"><span data-stu-id="c1341-204">In order for hello settings updated in hello configuration of hello various deployment sources toobe applied, hello Management Roles need toobe repaired.</span></span>  <span data-ttu-id="c1341-205">此程序以確保已正確套用 hello 組態值和 hello 設定部署來源進行可用 tootenants。</span><span class="sxs-lookup"><span data-stu-id="c1341-205">This process ensures that hello configuration values are applied correctly and hello configured Deployment Sources are made available tootenants.</span></span>

1. <span data-ttu-id="c1341-206">在新的瀏覽器索引標籤或視窗登入 toohello Azure 堆疊管理入口網站 (https://adminportal.local.azurestack.external) hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="c1341-206">In a new browser tab or window Log in toohello Azure Stack Admin Portal (https://adminportal.local.azurestack.external) as hello service administrator.</span></span>
2. <span data-ttu-id="c1341-207">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1341-207">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**.</span></span>
3. <span data-ttu-id="c1341-208">按一下 [原始檔控制組態]</span><span class="sxs-lookup"><span data-stu-id="c1341-208">Click **Source control configuration**</span></span>
4. <span data-ttu-id="c1341-209">複製並貼上 hello**用戶端識別碼**和**用戶端密碼**hello 對應輸入方塊中的 GitHub。</span><span class="sxs-lookup"><span data-stu-id="c1341-209">Copy and paste hello **Client Id** and **Client Secret** into hello corresponding input boxes for GitHub.</span></span>
5. <span data-ttu-id="c1341-210">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="c1341-210">Click **Save**</span></span>
6. <span data-ttu-id="c1341-211">按一下 [角色]</span><span class="sxs-lookup"><span data-stu-id="c1341-211">Click **Roles**</span></span>
7. <span data-ttu-id="c1341-212">按一下 [管理伺服器]</span><span class="sxs-lookup"><span data-stu-id="c1341-212">Click **Management Server**</span></span>
8. <span data-ttu-id="c1341-213">按一下 [全部修復]，然後選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="c1341-213">Click **Repair All** and select **Yes**.</span></span>  <span data-ttu-id="c1341-214">這項作業排程的所有管理伺服器 toocomplete hello 整合修復。</span><span class="sxs-lookup"><span data-stu-id="c1341-214">This operation schedules a repair on all Management Servers toocomplete hello integration.</span></span>  <span data-ttu-id="c1341-215">hello 修復作業是 managed 的 toominimize 停機時間。</span><span class="sxs-lookup"><span data-stu-id="c1341-215">hello repair operations are managed toominimize downtime.</span></span>
    <span data-ttu-id="c1341-216">![App Service 資源提供者管理 - 角色 - 管理伺服器全部修復][6]</span><span class="sxs-lookup"><span data-stu-id="c1341-216">![App Service Resource Provider Admin - Roles - Management Server Repair All][6]</span></span>

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
