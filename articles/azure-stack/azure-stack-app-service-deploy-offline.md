---
title: "在離線環境中部署 App Service：Azure Stack | Microsoft Docs"
description: "如何在中斷連線且受 AD FS 保護的 Azure Stack 環境中部署 App Service 的詳細指導方針。"
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
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: b733851d4459ead1ae437604a27ca7720e2a3a87
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-an-app-service-resource-provider-to-a-disconnected-azure-stack-environment-secured-by-ad-fs"></a><span data-ttu-id="b82ea-103">將 App Service 資源提供者新增至中斷連線且受 AD FS 保護的 Azure Stack 環境</span><span class="sxs-lookup"><span data-stu-id="b82ea-103">Add an App Service resource provider to a disconnected Azure Stack environment secured by AD FS</span></span>

<span data-ttu-id="b82ea-104">您必須將 [Azure App Service 資源提供者](azure-stack-app-service-overview.md)新增到您的 Azure Stack 部署：</span><span class="sxs-lookup"><span data-stu-id="b82ea-104">You must add an [Azure App Service resource provider](azure-stack-app-service-overview.md) to your Azure Stack deployment:</span></span>

* <span data-ttu-id="b82ea-105">如果您在受 Active Directory 同盟服務 (AD FS) 保護的隔離環境中執行 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="b82ea-105">If you're running Azure Stack in an isolated environment secured by Active Directory Federation Services (AD FS).</span></span> 
* <span data-ttu-id="b82ea-106">如果您想要讓租用戶能夠使用其 Azure Stack 訂用帳戶來建立 Web、行動裝置版和 API 應用程式 (以及 Azure Functions 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-106">If you want to give your tenants the capability to create web, mobile, and API applications--and Azure Functions applications--with their Azure Stack subscription.</span></span> 

<span data-ttu-id="b82ea-107">若要這樣做，請依照此文章中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="b82ea-107">To do so, follow the steps in this article.</span></span>

## <a name="download-the-required-components"></a><span data-ttu-id="b82ea-108">下載必要元件</span><span class="sxs-lookup"><span data-stu-id="b82ea-108">Download the required components</span></span>

1. <span data-ttu-id="b82ea-109">下載 [Azure Stack 上的 App Service 預覽安裝程式](http://aka.ms/appsvconmasrc1installer)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-109">Download the [App Service on Azure Stack preview installer](http://aka.ms/appsvconmasrc1installer).</span></span>

2. <span data-ttu-id="b82ea-110">下載 [Azure Stack 上的 App Service 部署協助程式指令碼](http://aka.ms/appsvconmasrc1helper)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-110">Download the [App Service on Azure Stack deployment helper scripts](http://aka.ms/appsvconmasrc1helper).</span></span>

3. <span data-ttu-id="b82ea-111">從協助程式指令碼 zip 檔案解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="b82ea-111">Extract the files from the helper scripts zip file.</span></span> <span data-ttu-id="b82ea-112">隨即出現下列檔案與資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="b82ea-112">The following files and folder structure appear:</span></span>

   - <span data-ttu-id="b82ea-113">Create-AppServiceCerts.ps1</span><span class="sxs-lookup"><span data-stu-id="b82ea-113">Create-AppServiceCerts.ps1</span></span>
   - <span data-ttu-id="b82ea-114">Create-IdentityApp.ps1</span><span class="sxs-lookup"><span data-stu-id="b82ea-114">Create-IdentityApp.ps1</span></span>
   - <span data-ttu-id="b82ea-115">模組</span><span class="sxs-lookup"><span data-stu-id="b82ea-115">Modules</span></span>
      - <span data-ttu-id="b82ea-116">AzureStack.Identity.psm1</span><span class="sxs-lookup"><span data-stu-id="b82ea-116">AzureStack.Identity.psm1</span></span>
      - <span data-ttu-id="b82ea-117">GraphAPI.psm1</span><span class="sxs-lookup"><span data-stu-id="b82ea-117">GraphAPI.psm1</span></span>

## <a name="create-an-offline-installation-package"></a><span data-ttu-id="b82ea-118">建立離線安裝套件</span><span class="sxs-lookup"><span data-stu-id="b82ea-118">Create an offline installation package</span></span>

<span data-ttu-id="b82ea-119">若要在隔離的環境中部署 App Service，您必須從連線到網際網路的電腦建立離線安裝套件。</span><span class="sxs-lookup"><span data-stu-id="b82ea-119">To deploy App Service in an isolated environment, you must create an offline installation package from a machine that connects to the Internet.</span></span>

1. <span data-ttu-id="b82ea-120">從連線到網際網路的電腦，執行 Azure Stack 上的 App Service 預覽安裝程式 (AppService.exe)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-120">Run the App Service on Azure Stack preview installer (AppService.exe) from a machine that's connected to the Internet.</span></span>

2. <span data-ttu-id="b82ea-121">按一下 [進階] 索引標籤，然後按一下 [建立離線安裝套件]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-121">Click the **Advanced** tab, and click **Create offline installation package**.</span></span>

    ![Azure Stack 上的 App Service 會建立離線安裝套件][1]

3. <span data-ttu-id="b82ea-123">App Service 安裝程式會建立離線安裝套件、顯示路徑，並提供開啟該資料夾的選項。</span><span class="sxs-lookup"><span data-stu-id="b82ea-123">The App Service installer creates an offline installation package, displays the path, and gives an option to open the folder.</span></span>

   ![Azure Stack 上的 App Service 離線安裝套件][2]

4. <span data-ttu-id="b82ea-125">將 Azure Stack 上的 App Service 預覽安裝程式 (AppService.exe) 和離線安裝套件複製到 Azure Stack 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="b82ea-125">Copy the App Service on Azure Stack preview installer (AppService.exe) and the offline installation package to the Azure Stack host machine.</span></span>

## <a name="create-certificates-required-by-app-service-on-azure-stack"></a><span data-ttu-id="b82ea-126">建立 Azure Stack 上之 App Service 所需的憑證</span><span class="sxs-lookup"><span data-stu-id="b82ea-126">Create certificates required by App Service on Azure Stack</span></span>

<span data-ttu-id="b82ea-127">這第一個指令碼會搭配 Azure Stack 憑證授權單位運作，以建立 App Service 所需的三個憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-127">This first script works with the Azure Stack certificate authority to create three certificates that App Service needs.</span></span> <span data-ttu-id="b82ea-128">在 Azure Stack 主機上執行指令碼，並確定您是以 azurestack\administrator 身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b82ea-128">Run the script on the Azure Stack host and ensure that you're running PowerShell as azurestack\administrator.</span></span>

1. <span data-ttu-id="b82ea-129">在以 azurestack\administrator 身分執行的 PowerShell 工作階段中，從您解壓縮協助程式指令碼所在的位置執行 **Create-AppServiceCerts.ps1** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-129">In a PowerShell session running as azurestack\administrator, execute the **Create-AppServiceCerts.ps1** script from the location where you extracted the helper scripts.</span></span>  <span data-ttu-id="b82ea-130">此指令碼會在與 App Service 所需之建立憑證指令碼相同的資料夾中建立三個憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-130">The script creates three certificates in the same folder as the create certificates script that are needed by App Service.</span></span>

2. <span data-ttu-id="b82ea-131">輸入密碼來保護 .pfx 檔案，並記下密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-131">Enter a password to secure the .pfx files, and make a note of it.</span></span> <span data-ttu-id="b82ea-132">您需要在 Azure Stack 上的 App Service 安裝程式中輸入此密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-132">You need to enter it in the App Service on Azure Stack installer.</span></span>

### <a name="create-appservicecertsps1-parameters"></a><span data-ttu-id="b82ea-133">Create-AppServiceCerts.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="b82ea-133">Create-AppServiceCerts.ps1 parameters</span></span>

| <span data-ttu-id="b82ea-134">參數</span><span class="sxs-lookup"><span data-stu-id="b82ea-134">Parameter</span></span> | <span data-ttu-id="b82ea-135">必要/選用</span><span class="sxs-lookup"><span data-stu-id="b82ea-135">Required/optional</span></span> | <span data-ttu-id="b82ea-136">預設值</span><span class="sxs-lookup"><span data-stu-id="b82ea-136">Default value</span></span> | <span data-ttu-id="b82ea-137">說明</span><span class="sxs-lookup"><span data-stu-id="b82ea-137">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b82ea-138">pfxPassword</span><span class="sxs-lookup"><span data-stu-id="b82ea-138">pfxPassword</span></span> | <span data-ttu-id="b82ea-139">必要</span><span class="sxs-lookup"><span data-stu-id="b82ea-139">Required</span></span> | <span data-ttu-id="b82ea-140">Null</span><span class="sxs-lookup"><span data-stu-id="b82ea-140">Null</span></span> | <span data-ttu-id="b82ea-141">用來保護憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="b82ea-141">Password used to protect the certificate private key</span></span> |
| <span data-ttu-id="b82ea-142">DomainName</span><span class="sxs-lookup"><span data-stu-id="b82ea-142">DomainName</span></span> | <span data-ttu-id="b82ea-143">必要</span><span class="sxs-lookup"><span data-stu-id="b82ea-143">Required</span></span> | <span data-ttu-id="b82ea-144">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="b82ea-144">local.azurestack.external</span></span> | <span data-ttu-id="b82ea-145">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="b82ea-145">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="b82ea-146">CertificateAuthority</span><span class="sxs-lookup"><span data-stu-id="b82ea-146">CertificateAuthority</span></span> | <span data-ttu-id="b82ea-147">必要</span><span class="sxs-lookup"><span data-stu-id="b82ea-147">Required</span></span> | <span data-ttu-id="b82ea-148">AzS-CA01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="b82ea-148">AzS-CA01.azurestack.local</span></span> | <span data-ttu-id="b82ea-149">憑證授權單位端點</span><span class="sxs-lookup"><span data-stu-id="b82ea-149">Certificate authority endpoint</span></span> |

## <a name="complete-the-offline-installation-of-app-service-on-azure-stack"></a><span data-ttu-id="b82ea-150">完成 Azure Stack 上的 App Service 離線安裝</span><span class="sxs-lookup"><span data-stu-id="b82ea-150">Complete the offline installation of App Service on Azure Stack</span></span>

> [!NOTE]
> <span data-ttu-id="b82ea-151">您必須使用已提高權限的帳戶 (本機或網域系統管理員) 來執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b82ea-151">You *must* use an elevated account (local or domain administrator) to execute the installer.</span></span> <span data-ttu-id="b82ea-152">如果您以 azurestack\azurestackuser 身分登入，則系統會提示您提供已提高權限的認證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-152">If you sign in as azurestack\azurestackuser, you're prompted for elevated credentials.</span></span>

1. <span data-ttu-id="b82ea-153">以 azurestack\administrator 身分執行 appservice.exe。</span><span class="sxs-lookup"><span data-stu-id="b82ea-153">Run appservice.exe as azurestack\administrator.</span></span>

2. <span data-ttu-id="b82ea-154">按一下 [進階] 索引標籤，然後按一下 [完成離線安裝]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-154">Click the **Advanced** tab, and click **Complete offline installation**.</span></span>

    ![Azure Stack 上之 App Service 的完成離線安裝][3]

3. <span data-ttu-id="b82ea-156">指定您先前建立的離線安裝套件位置，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-156">Specify the location of the offline installation package you previously created, and click **Next**.</span></span>

    ![Azure Stack 上的 App Service 離線安裝套件位置][4]

4. <span data-ttu-id="b82ea-158">檢閱並接受 Microsoft 軟體發行前版本授權條款，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-158">Review and accept the Microsoft Software Prerelease License Terms, and click **Next**.</span></span>

5. <span data-ttu-id="b82ea-159">檢閱並接受協力廠商授權條款，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-159">Review and accept the third-party license terms, and click **Next**.</span></span>

6. <span data-ttu-id="b82ea-160">檢閱 App Service 雲端設定資訊，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-160">Review the App Service cloud configuration information, and click **Next**.</span></span>

    ![Azure Stack 上的 App Service 雲端設定][5]

    > [!NOTE]
    > <span data-ttu-id="b82ea-162">Azure Stack 上的 App Service 安裝程式提供適用於單一節點 Azure Stack 安裝的預設值。</span><span class="sxs-lookup"><span data-stu-id="b82ea-162">The App Service on Azure Stack installer provides the default values for a one-node Azure Stack installation.</span></span> <span data-ttu-id="b82ea-163">如果您已在部署 Azure Stack 時自訂選項 (例如，網域尾碼)，就需要據以編輯此視窗中的值。</span><span class="sxs-lookup"><span data-stu-id="b82ea-163">If you customized options when you deployed Azure Stack (for example, the domain suffix), you need to edit the values in this window accordingly.</span></span> <span data-ttu-id="b82ea-164">例如，如果您使用網域尾碼 mycloud.com，則您的管理員 Azure Resource Manager 端點必須變更為 adminmanagement.[region].mycloud.com。</span><span class="sxs-lookup"><span data-stu-id="b82ea-164">For example, if you use the domain suffix mycloud.com, your admin Azure Resource Manager endpoint needs to change to adminmanagement.[region].mycloud.com.</span></span>

7. <span data-ttu-id="b82ea-165">按一下 [Azure Stack 訂用帳戶] 方塊旁邊的 [連線] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b82ea-165">Click the **Connect** button next to the **Azure Stack Subscriptions** box.</span></span> <span data-ttu-id="b82ea-166">輸入您的管理帳戶，例如 azurestackadmin@azurestack.local。</span><span class="sxs-lookup"><span data-stu-id="b82ea-166">Enter your admin account, for example, azurestackadmin@azurestack.local.</span></span> <span data-ttu-id="b82ea-167">輸入您的密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-167">Enter your password, and click **Sign In**.</span></span>

8. <span data-ttu-id="b82ea-168">在 [Azure Stack 訂用帳戶] 方塊中，選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b82ea-168">Select your subscription in the **Azure Stack Subscriptions** box.</span></span>

9. <span data-ttu-id="b82ea-169">在 [Azure Stack 位置] 方塊中，選取對應到您要部署之區域的位置。</span><span class="sxs-lookup"><span data-stu-id="b82ea-169">In the **Azure Stack Locations** box, select the location that corresponds to the region you're deploying.</span></span> <span data-ttu-id="b82ea-170">例如，選取 [本機]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-170">For example, select **local**.</span></span> <span data-ttu-id="b82ea-171">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b82ea-171">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 訂用帳戶選取項目][6]

10. <span data-ttu-id="b82ea-173">針對您的 App Service 部署輸入**資源群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-173">Enter the **Resource Group Name** for your App Service deployment.</span></span> <span data-ttu-id="b82ea-174">根據預設值，它是設定為 **APPSERVICE-LOCAL**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-174">By default, it's set to **APPSERVICE-LOCAL**.</span></span>

11. <span data-ttu-id="b82ea-175">輸入您想要 App Service 在安裝期間建立的**儲存體帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-175">Enter the **Storage Account Name** you want App Service to create as part of the installation.</span></span> <span data-ttu-id="b82ea-176">根據預設值，它是設定為 **appsvclocalstor**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-176">By default, it's set to **appsvclocalstor**.</span></span>

12. <span data-ttu-id="b82ea-177">針對用於裝載 App Service 資源提供者資料庫的執行個體，輸入 SQL Server 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b82ea-177">Enter the SQL Server details for the instance that's used to host the App Service resource provider databases.</span></span> <span data-ttu-id="b82ea-178">按一下 [下一步]，安裝程式即會驗證 SQL 連線屬性。</span><span class="sxs-lookup"><span data-stu-id="b82ea-178">Click **Next**, and the installer validates the SQL connection properties.</span></span>

13. <span data-ttu-id="b82ea-179">按一下 [App Service 預設 SSL 憑證檔案] 方塊旁邊的 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b82ea-179">Click the **Browse** button next to the **App Service default SSL certificate file** box.</span></span> <span data-ttu-id="b82ea-180">移至[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)的 **_.appservice.local.AzureStack.external** 憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-180">Go to the **_.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="b82ea-181">如果您指定的位置和網域尾碼與您建立憑證時的不同，請選取對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-181">If you specified a different location and domain suffix when you created the certificate, select the corresponding certificate.</span></span>

14. <span data-ttu-id="b82ea-182">輸入您建立憑證時所設定的憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-182">Enter the certificate password that you set when you created the certificate.</span></span>

15. <span data-ttu-id="b82ea-183">按一下 [資源提供者 SSL 憑證檔案] 方塊旁邊的 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b82ea-183">Click the **Browse** button next to the **Resource provider SSL certificate file** box.</span></span> <span data-ttu-id="b82ea-184">移至[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)的 **api.appservice.local.AzureStack.external** 憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-184">Go to the **api.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="b82ea-185">如果您指定的位置和網域尾碼與您建立憑證時的不同，請選取對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-185">If you specified a different location and domain suffix when you created the certificate, select the corresponding certificate.</span></span>

16. <span data-ttu-id="b82ea-186">輸入您建立憑證時所設定的憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-186">Enter the certificate password that you set when you created the certificate.</span></span>

17. <span data-ttu-id="b82ea-187">按一下 [資源提供者根憑證檔案] 方塊旁邊的 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b82ea-187">Click the **Browse** button next to the **Resource provider root certificate file** box.</span></span> <span data-ttu-id="b82ea-188">移至[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)的 **AzureStackCertificationAuthority** 憑證。</span><span class="sxs-lookup"><span data-stu-id="b82ea-188">Go to the **AzureStackCertificationAuthority** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span>

18. <span data-ttu-id="b82ea-189">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b82ea-189">Click **Next**.</span></span> <span data-ttu-id="b82ea-190">安裝程式會確認所提供的憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-190">The installer verifies the certificate password provided.</span></span>

    ![Azure Stack 上的 App Service 憑證詳細資料][8]

19. <span data-ttu-id="b82ea-192">檢閱 App Service 角色設定。</span><span class="sxs-lookup"><span data-stu-id="b82ea-192">Review the App Service role configuration.</span></span> <span data-ttu-id="b82ea-193">預設值會使用適用於每個角色的最低建議執行個體 SKU 來填入。</span><span class="sxs-lookup"><span data-stu-id="b82ea-193">The defaults are populated with the minimum recommended instance SKUs for each role.</span></span> <span data-ttu-id="b82ea-194">系統會提供核心和記憶體需求的摘要來協助規劃您的部署。</span><span class="sxs-lookup"><span data-stu-id="b82ea-194">A summary of core and memory requirements is provided to help plan your deployment.</span></span> <span data-ttu-id="b82ea-195">進行選擇之後，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-195">After you make your selections, click **Next**.</span></span>

    - <span data-ttu-id="b82ea-196">**控制器**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-196">**Controller**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="b82ea-197">這是我們建議的最小值。</span><span class="sxs-lookup"><span data-stu-id="b82ea-197">This is the minimum we recommend.</span></span> <span data-ttu-id="b82ea-198">控制器角色負責管理和維護 App Service 雲端的健康情況。</span><span class="sxs-lookup"><span data-stu-id="b82ea-198">The Controller role is responsible for managing and maintaining the health of the App Service cloud.</span></span>
    - <span data-ttu-id="b82ea-199">**管理**：預設會選取一個標準 A2 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-199">**Management**: By default, one Standard A2 instance is selected.</span></span> <span data-ttu-id="b82ea-200">為了提供容錯移轉，我們建議兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-200">To provide failover, we recommend two instances.</span></span> <span data-ttu-id="b82ea-201">管理角色負責 App Service Azure Resource Manager 和 API 端點、入口網站擴充功能 (管理員、租用戶、Functions 入口網站)，以及資料服務。</span><span class="sxs-lookup"><span data-stu-id="b82ea-201">The Management role is responsible for the App Service Azure Resource Manager and API endpoints, portal extensions (admin, tenant, Functions portal), and the data service.</span></span>
    - <span data-ttu-id="b82ea-202">**發行者**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-202">**Publisher**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="b82ea-203">這是我們建議的最小值。</span><span class="sxs-lookup"><span data-stu-id="b82ea-203">This is the minimum we recommend.</span></span> <span data-ttu-id="b82ea-204">發行者角色負責透過 FTP 和 Web 部署來發行內容。</span><span class="sxs-lookup"><span data-stu-id="b82ea-204">The Publisher role is responsible for publishing content via FTP and web deployment.</span></span>
    - <span data-ttu-id="b82ea-205">**前端**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-205">**FrontEnd**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="b82ea-206">這是我們建議的最小值。</span><span class="sxs-lookup"><span data-stu-id="b82ea-206">This is the minimum we recommend.</span></span> <span data-ttu-id="b82ea-207">前端角色負責將要求路由傳送到 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b82ea-207">The FrontEnd role is responsible for routing requests to App Service applications.</span></span>
    - <span data-ttu-id="b82ea-208">**共用背景工作**：預設會選取一個標準 A1 執行個體，但您可能想要新增更多。</span><span class="sxs-lookup"><span data-stu-id="b82ea-208">**Shared Worker**: By default, one Standard A1 instance is selected, but you might want to add more.</span></span> <span data-ttu-id="b82ea-209">身為系統管理員，您可以定義您的供應項目，並選擇任何 SKU 層。</span><span class="sxs-lookup"><span data-stu-id="b82ea-209">As an administrator, you can define your offering and choose any SKU tier.</span></span> <span data-ttu-id="b82ea-210">各層必須具有至少一個核心。</span><span class="sxs-lookup"><span data-stu-id="b82ea-210">The tiers must have a minimum of one core.</span></span> <span data-ttu-id="b82ea-211">共用背景工作角色負責主控 Web、行動裝置版或 API 應用程式及 Azure Functions 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b82ea-211">The Shared Worker role is responsible for hosting web, mobile, or API applications and Azure Functions apps.</span></span>

    ![Azure Stack 上的 App Service 角色設定][9]

    > [!NOTE]
    > <span data-ttu-id="b82ea-213">在技術預覽中，App Service 資源提供者安裝程式也會部署要作為簡單檔案伺服器運作的標準 A1 執行個體，以支援 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="b82ea-213">In the technical previews, the App Service resource provider installer also deploys a Standard A1 instance to operate as a simple file server to support the Azure Resource Manager.</span></span> <span data-ttu-id="b82ea-214">這會針對單一節點的連絡點加以保留。</span><span class="sxs-lookup"><span data-stu-id="b82ea-214">This remains for a single-node point of contact.</span></span> <span data-ttu-id="b82ea-215">對於生產工作負載，在公開推出時，App Service 安裝程式會讓高可用性檔案伺服器可供使用。</span><span class="sxs-lookup"><span data-stu-id="b82ea-215">For production workloads, at general availability the App Service installer enables the use of a high-availability file server.</span></span>

20. <span data-ttu-id="b82ea-216">從可以在適用於 App Service 雲端的運算資源提供者中的可用映像中，選擇您的部署 **Windows Server 2016** VM 映像。</span><span class="sxs-lookup"><span data-stu-id="b82ea-216">Choose your deployment **Windows Server 2016** VM image from those available in the compute resource provider for the App Service cloud.</span></span> <span data-ttu-id="b82ea-217">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b82ea-217">Click **Next**.</span></span> 

    ![Azure Stack 上的 App Service VM 映像選取項目][10]

21. <span data-ttu-id="b82ea-219">針對 App Service 雲端中設定的背景工作角色，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-219">Enter a user name and password for the Worker roles configured in the App Service cloud.</span></span> <span data-ttu-id="b82ea-220">針對所有其他的 App Service 角色，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-220">Enter a user name and password for all other App Service roles.</span></span> <span data-ttu-id="b82ea-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b82ea-221">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 認證項目][11]

22. <span data-ttu-id="b82ea-223">在摘要畫面上，確認您所做的選擇。</span><span class="sxs-lookup"><span data-stu-id="b82ea-223">On the summary screen, verify the selections you made.</span></span> <span data-ttu-id="b82ea-224">若要進行變更，請返回畫面並修改您的選擇。</span><span class="sxs-lookup"><span data-stu-id="b82ea-224">To make changes, go back through the screens and modify your selections.</span></span> <span data-ttu-id="b82ea-225">如果設定符合您的需求，請選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b82ea-225">If the configuration is how you want it, select the check box.</span></span> <span data-ttu-id="b82ea-226">若要開始部署，請按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-226">To start the deployment, click **Next**.</span></span> 

    ![Azure Stack 上的 App Service 選取項目摘要][12]

23. <span data-ttu-id="b82ea-228">追蹤安裝進度。</span><span class="sxs-lookup"><span data-stu-id="b82ea-228">Track the installation progress.</span></span> <span data-ttu-id="b82ea-229">根據預設的選取項目而定，部署 Azure Stack 上的 App Service 大約需要 45 到 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b82ea-229">App Service on Azure Stack takes about 45 to 60 minutes to deploy based on the default selections.</span></span>

    ![Azure Stack 上的 App Service 安裝進度][13]

24. <span data-ttu-id="b82ea-231">當安裝程式順利完成之後，請按一下 [結束]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-231">After the installer successfully finishes, click **Exit**.</span></span>

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-the-azure-functions-portal-and-advanced-developer-tools"></a><span data-ttu-id="b82ea-232">針對背景工作層上的虛擬機器擴展集整合設定 AD FS 服務主體，以及針對 Azure Functions 入口網站設定 SSO 和進階開發人員工具</span><span class="sxs-lookup"><span data-stu-id="b82ea-232">Configure an AD FS service principal for virtual machine scale set integration on Worker tiers and SSO for the Azure Functions portal and advanced developer tools</span></span>

>[!NOTE]
> <span data-ttu-id="b82ea-233">這些步驟只適用於 AD FS 保護的 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="b82ea-233">These steps apply to AD FS secured Azure Stack environments only.</span></span>

<span data-ttu-id="b82ea-234">系統管理員必須設定 SSO 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b82ea-234">Administrators need to configure SSO to:</span></span>

* <span data-ttu-id="b82ea-235">針對背景工作層上的虛擬機器擴展集整合設定服務主體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-235">Configure a service principal for virtual machine scale set integration on Worker tiers.</span></span>
* <span data-ttu-id="b82ea-236">啟用 App Service (Kudu) 內的進階開發人員工具。</span><span class="sxs-lookup"><span data-stu-id="b82ea-236">Enable the advanced developer tools within App Service (Kudu).</span></span>
* <span data-ttu-id="b82ea-237">讓 Azure Functions 入口網站體驗可供使用。</span><span class="sxs-lookup"><span data-stu-id="b82ea-237">Enable the use of the Azure Functions portal experience.</span></span> 

<span data-ttu-id="b82ea-238">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b82ea-238">Follow these steps:</span></span>

1. <span data-ttu-id="b82ea-239">以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b82ea-239">Open a PowerShell instance as azurestack\azurestackadmin.</span></span>

2. <span data-ttu-id="b82ea-240">移至在[先決條件步驟](#Download-Required-Components)中下載並解壓縮的指令碼位置。</span><span class="sxs-lookup"><span data-stu-id="b82ea-240">Go to the location of the scripts downloaded and extracted in the [prerequisite step](#Download-Required-Components).</span></span>

3. <span data-ttu-id="b82ea-241">[安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-241">[Install](azure-stack-powershell-install.md) and [configure an Azure Stack PowerShell environment](azure-stack-powershell-configure-admin.md).</span></span>

4. <span data-ttu-id="b82ea-242">在同一個 PowerShell 工作階段中，執行 **CreateIdentityApp.ps1** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-242">In the same PowerShell session, run the **CreateIdentityApp.ps1** script.</span></span> <span data-ttu-id="b82ea-243">當系統提示您提供 Azure Active Directory (Azure AD) 租用戶識別碼時，請輸入 **ADFS**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-243">When you're prompted for your Azure Active Directory (Azure AD) tenant ID, enter **ADFS**.</span></span>

5. <span data-ttu-id="b82ea-244">在 [認證] 視窗中，輸入您的 AD FS 服務管理帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-244">In the **Credential** window, enter your AD FS service admin account and password.</span></span> <span data-ttu-id="b82ea-245">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b82ea-245">Click **OK**.</span></span>

6. <span data-ttu-id="b82ea-246">輸入[稍早建立的憑證](# Create certificates to be used by App Service on Azure Stack)的憑證檔案路徑和憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-246">Enter the certificate file path and certificate password for the [certificate created earlier](# Create certificates to be used by App Service on Azure Stack).</span></span> <span data-ttu-id="b82ea-247">根據預設值，針對此步驟建立的憑證是 sso.appservice.local.azurestack.external.pfx。</span><span class="sxs-lookup"><span data-stu-id="b82ea-247">The certificate created for this step by default is sso.appservice.local.azurestack.external.pfx.</span></span>

7. <span data-ttu-id="b82ea-248">指令碼會在租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b82ea-248">The script creates a new application in the tenant Azure AD and generates a new PowerShell script.</span></span>

8. <span data-ttu-id="b82ea-249">使用遠端桌面工作階段，將身分識別應用程式憑證檔案和產生的指令碼複製到 **CN0-VM**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-249">Copy the identity app certificate file and the generated script to the **CN0-VM** by using a remote desktop session.</span></span>

9. <span data-ttu-id="b82ea-250">返回 **CN0-VM**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-250">Return to **CN0-VM**.</span></span>

10. <span data-ttu-id="b82ea-251">開啟系統管理員的 PowerShell 視窗，然後瀏覽到步驟 7 中複製指令碼檔案與憑證的目錄。</span><span class="sxs-lookup"><span data-stu-id="b82ea-251">Open an administrator PowerShell window, and browse to the directory where the script file and certificate were copied in step 7.</span></span>

11. <span data-ttu-id="b82ea-252">執行指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="b82ea-252">Run the script file.</span></span> <span data-ttu-id="b82ea-253">此指令碼檔案會在 Azure Stack 上的 App Service 設定中輸入屬性，並在所有前端與管理角色上起始修復作業。</span><span class="sxs-lookup"><span data-stu-id="b82ea-253">This script file enters the properties in the App Service on Azure Stack configuration and initiates a repair operation on all FrontEnd and Management roles.</span></span>

| <span data-ttu-id="b82ea-254">參數</span><span class="sxs-lookup"><span data-stu-id="b82ea-254">Parameter</span></span> | <span data-ttu-id="b82ea-255">必要/選用</span><span class="sxs-lookup"><span data-stu-id="b82ea-255">Required/optional</span></span> | <span data-ttu-id="b82ea-256">預設值</span><span class="sxs-lookup"><span data-stu-id="b82ea-256">Default value</span></span> | <span data-ttu-id="b82ea-257">說明</span><span class="sxs-lookup"><span data-stu-id="b82ea-257">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b82ea-258">DirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="b82ea-258">DirectoryTenantName</span></span> | <span data-ttu-id="b82ea-259">強制</span><span class="sxs-lookup"><span data-stu-id="b82ea-259">Mandatory</span></span> | <span data-ttu-id="b82ea-260">Null</span><span class="sxs-lookup"><span data-stu-id="b82ea-260">Null</span></span> | <span data-ttu-id="b82ea-261">對 AD FS 環境使用 **ADFS**</span><span class="sxs-lookup"><span data-stu-id="b82ea-261">Use **ADFS** for the AD FS environment</span></span> |
| <span data-ttu-id="b82ea-262">TenantAzure Resource ManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="b82ea-262">TenantAzure Resource ManagerEndpoint</span></span> | <span data-ttu-id="b82ea-263">強制</span><span class="sxs-lookup"><span data-stu-id="b82ea-263">Mandatory</span></span> | <span data-ttu-id="b82ea-264">management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="b82ea-264">management.local.azurestack.external</span></span> | <span data-ttu-id="b82ea-265">租用戶 Azure Resource Manager 端點</span><span class="sxs-lookup"><span data-stu-id="b82ea-265">The tenant Azure Resource Manager endpoint</span></span> |
| <span data-ttu-id="b82ea-266">AzureStackCredential</span><span class="sxs-lookup"><span data-stu-id="b82ea-266">AzureStackCredential</span></span> | <span data-ttu-id="b82ea-267">強制</span><span class="sxs-lookup"><span data-stu-id="b82ea-267">Mandatory</span></span> | <span data-ttu-id="b82ea-268">Null</span><span class="sxs-lookup"><span data-stu-id="b82ea-268">Null</span></span> | <span data-ttu-id="b82ea-269">AD FS 服務管理帳戶</span><span class="sxs-lookup"><span data-stu-id="b82ea-269">The AD FS service admin account</span></span> |
| <span data-ttu-id="b82ea-270">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="b82ea-270">CertificateFilePath</span></span> | <span data-ttu-id="b82ea-271">強制</span><span class="sxs-lookup"><span data-stu-id="b82ea-271">Mandatory</span></span> | <span data-ttu-id="b82ea-272">Null</span><span class="sxs-lookup"><span data-stu-id="b82ea-272">Null</span></span> | <span data-ttu-id="b82ea-273">稍早產生之身分識別應用程式憑證檔案的路徑</span><span class="sxs-lookup"><span data-stu-id="b82ea-273">Path to the identity application certificate file generated earlier</span></span> |
| <span data-ttu-id="b82ea-274">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="b82ea-274">CertificatePassword</span></span> | <span data-ttu-id="b82ea-275">強制</span><span class="sxs-lookup"><span data-stu-id="b82ea-275">Mandatory</span></span> | <span data-ttu-id="b82ea-276">Null</span><span class="sxs-lookup"><span data-stu-id="b82ea-276">Null</span></span> | <span data-ttu-id="b82ea-277">用來保護憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="b82ea-277">Password used to protect the certificate private key</span></span> |
| <span data-ttu-id="b82ea-278">DomainName</span><span class="sxs-lookup"><span data-stu-id="b82ea-278">DomainName</span></span> | <span data-ttu-id="b82ea-279">必要</span><span class="sxs-lookup"><span data-stu-id="b82ea-279">Required</span></span> | <span data-ttu-id="b82ea-280">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="b82ea-280">local.azurestack.external</span></span> | <span data-ttu-id="b82ea-281">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="b82ea-281">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="b82ea-282">AdfsMachineName</span><span class="sxs-lookup"><span data-stu-id="b82ea-282">AdfsMachineName</span></span> | <span data-ttu-id="b82ea-283">選用</span><span class="sxs-lookup"><span data-stu-id="b82ea-283">Optional</span></span> | <span data-ttu-id="b82ea-284">AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="b82ea-284">AD FS machine name, for example, AzS-ADFS01.azurestack.local</span></span> |


## <a name="validate-the-app-service-on-azure-stack-installation"></a><span data-ttu-id="b82ea-285">確認 Azure Stack 上的 App Service 安裝</span><span class="sxs-lookup"><span data-stu-id="b82ea-285">Validate the App Service on Azure Stack installation</span></span>

1. <span data-ttu-id="b82ea-286">在 Azure Stack 管理入口網站中，瀏覽到安裝程式所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b82ea-286">In the Azure Stack admin portal, browse to the resource group created by the installer.</span></span> <span data-ttu-id="b82ea-287">根據預設值，此群組是 **APPSERVICE-LOCAL**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-287">By default, this group is **APPSERVICE-LOCAL**.</span></span>

2. <span data-ttu-id="b82ea-288">找出 **CN0-VM**。</span><span class="sxs-lookup"><span data-stu-id="b82ea-288">Locate the **CN0-VM**.</span></span> <span data-ttu-id="b82ea-289">若要連線到 VM，請按一下 [虛擬機器] 刀鋒視窗上的 [連線]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-289">To connect to the VM, click **Connect** on the **Virtual Machine** blade.</span></span>

3. <span data-ttu-id="b82ea-290">在此 VM 的桌面上，按兩下 [Web 雲端管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-290">On the desktop of this VM, double-click **Web Cloud Management Console**.</span></span>

4. <span data-ttu-id="b82ea-291">移至 [受管理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-291">Go to **Managed Servers**.</span></span>

5. <span data-ttu-id="b82ea-292">當所有電腦都針對一或多個背景工作顯示 [就緒] 時，請繼續進行步驟 6。</span><span class="sxs-lookup"><span data-stu-id="b82ea-292">When all the machines display **Ready** for one or more Workers, proceed to step 6.</span></span>

6. <span data-ttu-id="b82ea-293">關閉遠端桌面電腦，並返回您執行 App Service 安裝程式的電腦。</span><span class="sxs-lookup"><span data-stu-id="b82ea-293">Close the remote desktop machine, and return to the machine where you executed the App Service installer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b82ea-294">您不需要等候一或多個背景工作顯示 [就緒]，就能完成 Azure Stack 上的 App Service 安裝。</span><span class="sxs-lookup"><span data-stu-id="b82ea-294">You don't need to wait for one or more Workers to display **Ready** to complete the installation of App Service on Azure Stack.</span></span> <span data-ttu-id="b82ea-295">不過，您需要至少一個背景工作已就緒可部署 Web、行動裝置版或 API 應用程式，或是 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="b82ea-295">However, you need a minimum of one Worker that's ready to deploy a web, mobile, or API app or Azure Functions.</span></span>
    
    ![Azure Stack 上的 App Service 受管理伺服器狀態][14]

## <a name="test-drive-app-service-on-azure-stack"></a><span data-ttu-id="b82ea-297">測試 Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="b82ea-297">Test drive App Service on Azure Stack</span></span>

<span data-ttu-id="b82ea-298">當您部署並註冊 App Service 資源提供者之後，請測試它，以確定租用戶可以部署 Web、行動裝置版及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b82ea-298">After you deploy and register the App Service resource provider, test it to make sure that tenants can deploy web, mobile, and API apps.</span></span>

> [!NOTE]
> <span data-ttu-id="b82ea-299">您需要在方案內建立含有 Microsoft.Web 命名空間的供應項目。</span><span class="sxs-lookup"><span data-stu-id="b82ea-299">You need to create an offer that has the Microsoft.Web namespace within the plan.</span></span> <span data-ttu-id="b82ea-300">然後，您需要具有訂閱此供應項目的租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b82ea-300">Then you need to have a tenant subscription that subscribes to this offer.</span></span> <span data-ttu-id="b82ea-301">如需詳細資訊，請參閱[建立供應項目](azure-stack-create-offer.md)和[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-301">For more information, see  [Create offer](azure-stack-create-offer.md) and [Create plan](azure-stack-create-plan.md).</span></span>
>

<span data-ttu-id="b82ea-302">您必須具有租用戶訂用帳戶，才能建立使用 Azure Stack 上之 App Service 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b82ea-302">You *must* have a tenant subscription to create applications that use App Service on Azure Stack.</span></span> <span data-ttu-id="b82ea-303">服務管理員只能在管理入口網站內完成的功能，與 App Service 的資源提供者管理有關。</span><span class="sxs-lookup"><span data-stu-id="b82ea-303">The only capabilities that a service admin can complete within the admin portal are related to the resource provider administration of App Service.</span></span> <span data-ttu-id="b82ea-304">這些功能包括新增容量、設定部署來源，以及新增背景工作層和 SKU。</span><span class="sxs-lookup"><span data-stu-id="b82ea-304">These capabilities include adding capacity, configuring deployment sources, and adding Worker tiers and SKUs.</span></span>

<span data-ttu-id="b82ea-305">從第三個技術預覽開始，若要建立 Web、行動裝置版及 API 應用程式，您必須使用租用戶入口網站，並具有租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b82ea-305">As of the third technical preview, to create web, mobile, and API apps you must use the tenant portal and have a tenant subscription.</span></span>  

1. <span data-ttu-id="b82ea-306">在 Azure Stack 租用戶入口網站中，按一下 [新增] > [Web + 行動] > [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-306">In the Azure Stack tenant portal, click **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="b82ea-307">在 [Web 應用程式] 刀鋒視窗中，於 [Web 應用程式] 方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="b82ea-307">On the **Web App** blade, type a name in the **Web app** box.</span></span>

3. <span data-ttu-id="b82ea-308">按一下 [資源群組] 下方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-308">Under **Resource Group**, click **New**.</span></span> <span data-ttu-id="b82ea-309">接著在 [資源群組] 方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="b82ea-309">Then type a name in the **Resource Group** box.</span></span>

4. <span data-ttu-id="b82ea-310">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-310">Click **App Service plan/Location** > **Create New**.</span></span>

5. <span data-ttu-id="b82ea-311">在 [App Service 方案] 刀鋒視窗中，於 [App Service 方案] 方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="b82ea-311">On the **App Service plan** blade, type a name in the **App Service plan** box.</span></span>

6. <span data-ttu-id="b82ea-312">按一下 [定價層] > [免費 - 共用] 或 [共用 - 共用] > [選取] > [確定] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-312">Click **Pricing tier** > **Free-Shared** or **Shared-Shared** > **Select** > **OK** > **Create**.</span></span>

7. <span data-ttu-id="b82ea-313">新 Web 應用程式的磚隨即出現在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="b82ea-313">In under a minute, a tile for the new web app appears on the dashboard.</span></span> <span data-ttu-id="b82ea-314">按一下此磚。</span><span class="sxs-lookup"><span data-stu-id="b82ea-314">Click the tile.</span></span>

8. <span data-ttu-id="b82ea-315">在 [Web 應用程式] 刀鋒視窗中，按一下 [瀏覽] 以檢視此應用程式的預設網站。</span><span class="sxs-lookup"><span data-stu-id="b82ea-315">On the **Web App** blade, click **Browse** to view the default website for this app.</span></span>

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a><span data-ttu-id="b82ea-316">部署 WordPress、DNN 或 Django 網站 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="b82ea-316">Deploy a WordPress, DNN, or Django website (optional)</span></span>

1. <span data-ttu-id="b82ea-317">在 Azure Stack 租用戶入口網站中，按一下 [+]。</span><span class="sxs-lookup"><span data-stu-id="b82ea-317">In the Azure Stack tenant portal, click **+**.</span></span> <span data-ttu-id="b82ea-318">移至 Azure Marketplace、部署 Django 網站，然後等待順利完成。</span><span class="sxs-lookup"><span data-stu-id="b82ea-318">Go to the Azure Marketplace, deploy a Django website, and wait for successful completion.</span></span> <span data-ttu-id="b82ea-319">Django Web 平台會使用以檔案系統為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b82ea-319">The Django web platform uses a file system-based database.</span></span> <span data-ttu-id="b82ea-320">它不需要任何額外的資源提供者，例如 SQL 或 MySQL。</span><span class="sxs-lookup"><span data-stu-id="b82ea-320">It doesn’t require any additional resource providers such as SQL or MySQL.</span></span>

2. <span data-ttu-id="b82ea-321">如果您也會部署 MySQL 資源提供者，就可以從 Marketplace 部署 WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="b82ea-321">If you also deployed a MySQL resource provider, you can deploy a WordPress website from the Marketplace.</span></span> <span data-ttu-id="b82ea-322">當系統提示您提供資料庫參數時，請使用您選擇的使用者名稱和伺服器名稱，以 User1@Server1 形式輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b82ea-322">When you're prompted for database parameters, enter the user name as *User1@Server1*, with the user name and server name of your choice.</span></span>

3. <span data-ttu-id="b82ea-323">如果您也會部署 SQL Server 資源提供者，就可以從 Marketplace 部署 DNN 網站。</span><span class="sxs-lookup"><span data-stu-id="b82ea-323">If you also deployed a SQL Server resource provider, you can deploy a DNN website from the Marketplace.</span></span> <span data-ttu-id="b82ea-324">當系統提示您提供資料庫參數時，請挑選執行 SQL Server 且已連線到您資源提供者之電腦中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b82ea-324">When you're prompted for database parameters, pick a database in the computer running SQL Server that's connected to your resource provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b82ea-325">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b82ea-325">Next steps</span></span>

<span data-ttu-id="b82ea-326">您也可以嘗試其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)。</span><span class="sxs-lookup"><span data-stu-id="b82ea-326">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

- [<span data-ttu-id="b82ea-327">SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="b82ea-327">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
- [<span data-ttu-id="b82ea-328">MySQL 資源提供者</span><span class="sxs-lookup"><span data-stu-id="b82ea-328">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step1.png
[2]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step2.png
[3]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step3.png
[4]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step4.png
[5]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-cloud-configuration.png
[6]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-subscription-location-populated.png
[7]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-resource-group-SQL.png
[8]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-certificates.png
[9]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-configuration.png
[10]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-vm-image-selection.png
[11]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-credentials.png
[12]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-selection-summary.png
[13]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-installation-progress.png
[14]: ./media/azure-stack-app-service-deploy-offline/managed-servers.png


<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
