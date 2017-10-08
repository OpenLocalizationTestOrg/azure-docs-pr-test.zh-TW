---
title: "在離線環境中部署 App Service：Azure Stack | Microsoft Docs"
description: "如何在中斷連線的 Azure 堆疊環境中的應用程式服務 toodeploy 受到 AD FS 的詳細的指引。"
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
ms.openlocfilehash: f7992c310532427b5ffb88555faab2679023c876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooa-disconnected-azure-stack-environment-secured-by-ad-fs"></a><span data-ttu-id="28b16-103">新增應用程式服務的資源提供者 tooa 中斷連線 Azure 堆疊環境受到 AD FS</span><span class="sxs-lookup"><span data-stu-id="28b16-103">Add an App Service resource provider tooa disconnected Azure Stack environment secured by AD FS</span></span>

<span data-ttu-id="28b16-104">您必須新增[Azure App Service 資源提供者](azure-stack-app-service-overview.md)tooyour Azure 堆疊部署：</span><span class="sxs-lookup"><span data-stu-id="28b16-104">You must add an [Azure App Service resource provider](azure-stack-app-service-overview.md) tooyour Azure Stack deployment:</span></span>

* <span data-ttu-id="28b16-105">如果您在受 Active Directory 同盟服務 (AD FS) 保護的隔離環境中執行 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="28b16-105">If you're running Azure Stack in an isolated environment secured by Active Directory Federation Services (AD FS).</span></span> 
* <span data-ttu-id="28b16-106">如果您想 toogive 租用戶 hello 功能 toocreate web、 行動裝置版和 API 應用程式-和 Azure 函式應用程式-使用其 Azure 堆疊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28b16-106">If you want toogive your tenants hello capability toocreate web, mobile, and API applications--and Azure Functions applications--with their Azure Stack subscription.</span></span> 

<span data-ttu-id="28b16-107">toodo 因此，請遵循本文章中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="28b16-107">toodo so, follow hello steps in this article.</span></span>

## <a name="download-hello-required-components"></a><span data-ttu-id="28b16-108">下載所需的 hello 元件</span><span class="sxs-lookup"><span data-stu-id="28b16-108">Download hello required components</span></span>

1. <span data-ttu-id="28b16-109">下載 hello[上 Azure 堆疊 preview 安裝程式的應用程式服務](http://aka.ms/appsvconmasrc1installer)。</span><span class="sxs-lookup"><span data-stu-id="28b16-109">Download hello [App Service on Azure Stack preview installer](http://aka.ms/appsvconmasrc1installer).</span></span>

2. <span data-ttu-id="28b16-110">下載 hello [Azure 堆疊部署 helper 指令碼的應用程式服務](http://aka.ms/appsvconmasrc1helper)。</span><span class="sxs-lookup"><span data-stu-id="28b16-110">Download hello [App Service on Azure Stack deployment helper scripts](http://aka.ms/appsvconmasrc1helper).</span></span>

3. <span data-ttu-id="28b16-111">從 hello helper 指令碼 zip 檔案解壓縮 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="28b16-111">Extract hello files from hello helper scripts zip file.</span></span> <span data-ttu-id="28b16-112">hello 下列檔案和資料夾結構會顯示：</span><span class="sxs-lookup"><span data-stu-id="28b16-112">hello following files and folder structure appear:</span></span>

   - <span data-ttu-id="28b16-113">Create-AppServiceCerts.ps1</span><span class="sxs-lookup"><span data-stu-id="28b16-113">Create-AppServiceCerts.ps1</span></span>
   - <span data-ttu-id="28b16-114">Create-IdentityApp.ps1</span><span class="sxs-lookup"><span data-stu-id="28b16-114">Create-IdentityApp.ps1</span></span>
   - <span data-ttu-id="28b16-115">模組</span><span class="sxs-lookup"><span data-stu-id="28b16-115">Modules</span></span>
      - <span data-ttu-id="28b16-116">AzureStack.Identity.psm1</span><span class="sxs-lookup"><span data-stu-id="28b16-116">AzureStack.Identity.psm1</span></span>
      - <span data-ttu-id="28b16-117">GraphAPI.psm1</span><span class="sxs-lookup"><span data-stu-id="28b16-117">GraphAPI.psm1</span></span>

## <a name="create-an-offline-installation-package"></a><span data-ttu-id="28b16-118">建立離線安裝套件</span><span class="sxs-lookup"><span data-stu-id="28b16-118">Create an offline installation package</span></span>

<span data-ttu-id="28b16-119">toodeploy 應用程式服務的隔離環境中，您必須從連接 toohello 網際網路的電腦建立離線安裝套件。</span><span class="sxs-lookup"><span data-stu-id="28b16-119">toodeploy App Service in an isolated environment, you must create an offline installation package from a machine that connects toohello Internet.</span></span>

1. <span data-ttu-id="28b16-120">已連接網際網路 toohello 機器上執行應用程式服務的 hello Azure 堆疊 preview 安裝程式 (AppService.exe) 上。</span><span class="sxs-lookup"><span data-stu-id="28b16-120">Run hello App Service on Azure Stack preview installer (AppService.exe) from a machine that's connected toohello Internet.</span></span>

2. <span data-ttu-id="28b16-121">按一下 hello**進階**索引標籤，然後按一下**建立離線安裝套件**。</span><span class="sxs-lookup"><span data-stu-id="28b16-121">Click hello **Advanced** tab, and click **Create offline installation package**.</span></span>

    ![Azure Stack 上的 App Service 會建立離線安裝套件][1]

3. <span data-ttu-id="28b16-123">hello 應用程式服務安裝程式會建立離線安裝套件，顯示 hello 路徑，並提供選項 tooopen hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="28b16-123">hello App Service installer creates an offline installation package, displays hello path, and gives an option tooopen hello folder.</span></span>

   ![Azure Stack 上的 App Service 離線安裝套件][2]

4. <span data-ttu-id="28b16-125">在 Azure 堆疊 preview 安裝程式 (AppService.exe) 和 hello 離線安裝套件 toohello Azure 堆疊主機電腦上複製 hello 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="28b16-125">Copy hello App Service on Azure Stack preview installer (AppService.exe) and hello offline installation package toohello Azure Stack host machine.</span></span>

## <a name="create-certificates-required-by-app-service-on-azure-stack"></a><span data-ttu-id="28b16-126">建立 Azure Stack 上之 App Service 所需的憑證</span><span class="sxs-lookup"><span data-stu-id="28b16-126">Create certificates required by App Service on Azure Stack</span></span>

<span data-ttu-id="28b16-127">此第一個指令碼搭配 hello Azure 堆疊憑證授權單位 toocreate 三個憑證，您必須將應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="28b16-127">This first script works with hello Azure Stack certificate authority toocreate three certificates that App Service needs.</span></span> <span data-ttu-id="28b16-128">Hello Azure 堆疊主機上執行 hello 指令碼，請確定您 azurestack\administrator 作為執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="28b16-128">Run hello script on hello Azure Stack host and ensure that you're running PowerShell as azurestack\administrator.</span></span>

1. <span data-ttu-id="28b16-129">Azurestack\administrator 身分執行的 PowerShell 工作階段，執行 hello**建立 AppServiceCerts.ps1**指令碼從 hello hello helper 指令碼的解壓縮所在的位置。</span><span class="sxs-lookup"><span data-stu-id="28b16-129">In a PowerShell session running as azurestack\administrator, execute hello **Create-AppServiceCerts.ps1** script from hello location where you extracted hello helper scripts.</span></span>  <span data-ttu-id="28b16-130">hello 指令碼會建立三個憑證在 hello 與 hello 相同的資料夾會建立所需的應用程式服務的憑證指令碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-130">hello script creates three certificates in hello same folder as hello create certificates script that are needed by App Service.</span></span>

2. <span data-ttu-id="28b16-131">輸入密碼 toosecure hello.pfx 檔案，並記下它。</span><span class="sxs-lookup"><span data-stu-id="28b16-131">Enter a password toosecure hello .pfx files, and make a note of it.</span></span> <span data-ttu-id="28b16-132">您需要 tooenter hello 應用程式服務在 Azure 堆疊安裝程式中。</span><span class="sxs-lookup"><span data-stu-id="28b16-132">You need tooenter it in hello App Service on Azure Stack installer.</span></span>

### <a name="create-appservicecertsps1-parameters"></a><span data-ttu-id="28b16-133">Create-AppServiceCerts.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="28b16-133">Create-AppServiceCerts.ps1 parameters</span></span>

| <span data-ttu-id="28b16-134">參數</span><span class="sxs-lookup"><span data-stu-id="28b16-134">Parameter</span></span> | <span data-ttu-id="28b16-135">必要/選用</span><span class="sxs-lookup"><span data-stu-id="28b16-135">Required/optional</span></span> | <span data-ttu-id="28b16-136">預設值</span><span class="sxs-lookup"><span data-stu-id="28b16-136">Default value</span></span> | <span data-ttu-id="28b16-137">說明</span><span class="sxs-lookup"><span data-stu-id="28b16-137">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="28b16-138">pfxPassword</span><span class="sxs-lookup"><span data-stu-id="28b16-138">pfxPassword</span></span> | <span data-ttu-id="28b16-139">必要</span><span class="sxs-lookup"><span data-stu-id="28b16-139">Required</span></span> | <span data-ttu-id="28b16-140">Null</span><span class="sxs-lookup"><span data-stu-id="28b16-140">Null</span></span> | <span data-ttu-id="28b16-141">使用 tooprotect hello 憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="28b16-141">Password used tooprotect hello certificate private key</span></span> |
| <span data-ttu-id="28b16-142">DomainName</span><span class="sxs-lookup"><span data-stu-id="28b16-142">DomainName</span></span> | <span data-ttu-id="28b16-143">必要</span><span class="sxs-lookup"><span data-stu-id="28b16-143">Required</span></span> | <span data-ttu-id="28b16-144">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="28b16-144">local.azurestack.external</span></span> | <span data-ttu-id="28b16-145">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="28b16-145">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="28b16-146">CertificateAuthority</span><span class="sxs-lookup"><span data-stu-id="28b16-146">CertificateAuthority</span></span> | <span data-ttu-id="28b16-147">必要</span><span class="sxs-lookup"><span data-stu-id="28b16-147">Required</span></span> | <span data-ttu-id="28b16-148">AzS-CA01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="28b16-148">AzS-CA01.azurestack.local</span></span> | <span data-ttu-id="28b16-149">憑證授權單位端點</span><span class="sxs-lookup"><span data-stu-id="28b16-149">Certificate authority endpoint</span></span> |

## <a name="complete-hello-offline-installation-of-app-service-on-azure-stack"></a><span data-ttu-id="28b16-150">完成 Azure 堆疊上的應用程式服務的 hello 離線安裝</span><span class="sxs-lookup"><span data-stu-id="28b16-150">Complete hello offline installation of App Service on Azure Stack</span></span>

> [!NOTE]
> <span data-ttu-id="28b16-151">您*必須*使用提高權限的帳戶 （本機或網域系統管理員） tooexecute hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="28b16-151">You *must* use an elevated account (local or domain administrator) tooexecute hello installer.</span></span> <span data-ttu-id="28b16-152">如果您以 azurestack\azurestackuser 身分登入，則系統會提示您提供已提高權限的認證。</span><span class="sxs-lookup"><span data-stu-id="28b16-152">If you sign in as azurestack\azurestackuser, you're prompted for elevated credentials.</span></span>

1. <span data-ttu-id="28b16-153">以 azurestack\administrator 身分執行 appservice.exe。</span><span class="sxs-lookup"><span data-stu-id="28b16-153">Run appservice.exe as azurestack\administrator.</span></span>

2. <span data-ttu-id="28b16-154">按一下 hello**進階**索引標籤，然後按一下**完成離線安裝**。</span><span class="sxs-lookup"><span data-stu-id="28b16-154">Click hello **Advanced** tab, and click **Complete offline installation**.</span></span>

    ![Azure Stack 上之 App Service 的完成離線安裝][3]

3. <span data-ttu-id="28b16-156">指定您先前建立的然後按一下 hello 離線安裝套件 hello 位置**下一步**。</span><span class="sxs-lookup"><span data-stu-id="28b16-156">Specify hello location of hello offline installation package you previously created, and click **Next**.</span></span>

    ![Azure Stack 上的 App Service 離線安裝套件位置][4]

4. <span data-ttu-id="28b16-158">檢閱並接受 hello Microsoft 發行前版本授權條款，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="28b16-158">Review and accept hello Microsoft Software Prerelease License Terms, and click **Next**.</span></span>

5. <span data-ttu-id="28b16-159">檢閱並接受 hello 協力廠商授權條款，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="28b16-159">Review and accept hello third-party license terms, and click **Next**.</span></span>

6. <span data-ttu-id="28b16-160">檢閱 hello 應用程式服務雲端組態資訊，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="28b16-160">Review hello App Service cloud configuration information, and click **Next**.</span></span>

    ![Azure Stack 上的 App Service 雲端設定][5]

    > [!NOTE]
    > <span data-ttu-id="28b16-162">hello 應用程式服務在 Azure 堆疊安裝程式提供單一節點 Azure 堆疊安裝 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="28b16-162">hello App Service on Azure Stack installer provides hello default values for a one-node Azure Stack installation.</span></span> <span data-ttu-id="28b16-163">如果您部署 Azure 堆疊 （例如，hello 網域尾碼） 時，您可以自訂選項，會據以需要 tooedit hello 值，此視窗中。</span><span class="sxs-lookup"><span data-stu-id="28b16-163">If you customized options when you deployed Azure Stack (for example, hello domain suffix), you need tooedit hello values in this window accordingly.</span></span> <span data-ttu-id="28b16-164">例如，如果您使用 hello 網域尾碼 mycloud.com，您管理 Azure 資源管理員端點需要 toochange tooadminmanagement。[region]。 mycloud.com。</span><span class="sxs-lookup"><span data-stu-id="28b16-164">For example, if you use hello domain suffix mycloud.com, your admin Azure Resource Manager endpoint needs toochange tooadminmanagement.[region].mycloud.com.</span></span>

7. <span data-ttu-id="28b16-165">按一下 hello**連接**按鈕的下一個 toohello **Azure 堆疊訂用帳戶**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-165">Click hello **Connect** button next toohello **Azure Stack Subscriptions** box.</span></span> <span data-ttu-id="28b16-166">輸入您的管理帳戶，例如 azurestackadmin@azurestack.local。</span><span class="sxs-lookup"><span data-stu-id="28b16-166">Enter your admin account, for example, azurestackadmin@azurestack.local.</span></span> <span data-ttu-id="28b16-167">輸入您的密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="28b16-167">Enter your password, and click **Sign In**.</span></span>

8. <span data-ttu-id="28b16-168">選取您的訂閱中 hello **Azure 堆疊訂用帳戶**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-168">Select your subscription in hello **Azure Stack Subscriptions** box.</span></span>

9. <span data-ttu-id="28b16-169">在 hello **Azure 堆疊位置**方塊中，選取 hello 對應您要部署的 toohello 區域的位置。</span><span class="sxs-lookup"><span data-stu-id="28b16-169">In hello **Azure Stack Locations** box, select hello location that corresponds toohello region you're deploying.</span></span> <span data-ttu-id="28b16-170">例如，選取 [本機]。</span><span class="sxs-lookup"><span data-stu-id="28b16-170">For example, select **local**.</span></span> <span data-ttu-id="28b16-171">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="28b16-171">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 訂用帳戶選取項目][6]

10. <span data-ttu-id="28b16-173">輸入 hello**資源群組名稱**為您的應用程式服務部署。</span><span class="sxs-lookup"><span data-stu-id="28b16-173">Enter hello **Resource Group Name** for your App Service deployment.</span></span> <span data-ttu-id="28b16-174">根據預設，此屬性設定太**APPSERVICE 本機**。</span><span class="sxs-lookup"><span data-stu-id="28b16-174">By default, it's set too**APPSERVICE-LOCAL**.</span></span>

11. <span data-ttu-id="28b16-175">輸入 hello**儲存體帳戶名稱**想 App Service toocreate hello 安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="28b16-175">Enter hello **Storage Account Name** you want App Service toocreate as part of hello installation.</span></span> <span data-ttu-id="28b16-176">根據預設，此屬性設定太**appsvclocalstor**。</span><span class="sxs-lookup"><span data-stu-id="28b16-176">By default, it's set too**appsvclocalstor**.</span></span>

12. <span data-ttu-id="28b16-177">輸入 hello 的使用的 toohost hello 應用程式服務資源提供者資料庫的執行個體 hello SQL Server 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="28b16-177">Enter hello SQL Server details for hello instance that's used toohost hello App Service resource provider databases.</span></span> <span data-ttu-id="28b16-178">按一下**下一步**，和 hello 安裝程式會驗證 hello SQL 連接屬性。</span><span class="sxs-lookup"><span data-stu-id="28b16-178">Click **Next**, and hello installer validates hello SQL connection properties.</span></span>

13. <span data-ttu-id="28b16-179">按一下 hello**瀏覽**按鈕的下一個 toohello**應用程式服務的預設 SSL 憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-179">Click hello **Browse** button next toohello **App Service default SSL certificate file** box.</span></span> <span data-ttu-id="28b16-180">移 toohello **_.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="28b16-180">Go toohello **_.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="28b16-181">如果您在建立 hello 憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="28b16-181">If you specified a different location and domain suffix when you created hello certificate, select hello corresponding certificate.</span></span>

14. <span data-ttu-id="28b16-182">輸入當您建立 hello 憑證的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-182">Enter hello certificate password that you set when you created hello certificate.</span></span>

15. <span data-ttu-id="28b16-183">按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的 SSL 憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-183">Click hello **Browse** button next toohello **Resource provider SSL certificate file** box.</span></span> <span data-ttu-id="28b16-184">移 toohello **api.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="28b16-184">Go toohello **api.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="28b16-185">如果您在建立 hello 憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="28b16-185">If you specified a different location and domain suffix when you created hello certificate, select hello corresponding certificate.</span></span>

16. <span data-ttu-id="28b16-186">輸入當您建立 hello 憑證的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-186">Enter hello certificate password that you set when you created hello certificate.</span></span>

17. <span data-ttu-id="28b16-187">按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的根憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-187">Click hello **Browse** button next toohello **Resource provider root certificate file** box.</span></span> <span data-ttu-id="28b16-188">移 toohello **AzureStackCertificationAuthority**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="28b16-188">Go toohello **AzureStackCertificationAuthority** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span>

18. <span data-ttu-id="28b16-189">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="28b16-189">Click **Next**.</span></span> <span data-ttu-id="28b16-190">hello 安裝程式會確認提供的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-190">hello installer verifies hello certificate password provided.</span></span>

    ![Azure Stack 上的 App Service 憑證詳細資料][8]

19. <span data-ttu-id="28b16-192">檢閱 hello 應用程式服務角色設定。</span><span class="sxs-lookup"><span data-stu-id="28b16-192">Review hello App Service role configuration.</span></span> <span data-ttu-id="28b16-193">hello 預設值會填入 hello 最小建議執行個體的 Sku 為每個角色。</span><span class="sxs-lookup"><span data-stu-id="28b16-193">hello defaults are populated with hello minimum recommended instance SKUs for each role.</span></span> <span data-ttu-id="28b16-194">在規劃部署時 toohelp 係核心和記憶體需求的摘要。</span><span class="sxs-lookup"><span data-stu-id="28b16-194">A summary of core and memory requirements is provided toohelp plan your deployment.</span></span> <span data-ttu-id="28b16-195">進行選擇之後，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="28b16-195">After you make your selections, click **Next**.</span></span>

    - <span data-ttu-id="28b16-196">**控制器**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-196">**Controller**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="28b16-197">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="28b16-197">This is hello minimum we recommend.</span></span> <span data-ttu-id="28b16-198">hello 控制器角色負責管理和維護的 hello 雲端應用程式服務的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="28b16-198">hello Controller role is responsible for managing and maintaining hello health of hello App Service cloud.</span></span>
    - <span data-ttu-id="28b16-199">**管理**：預設會選取一個標準 A2 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-199">**Management**: By default, one Standard A2 instance is selected.</span></span> <span data-ttu-id="28b16-200">tooprovide 容錯移轉時，我們建議兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-200">tooprovide failover, we recommend two instances.</span></span> <span data-ttu-id="28b16-201">hello 管理角色負責 hello 應用程式服務的 Azure 資源管理員和 API 端點、 入口網站擴充功能 （系統管理員、 租用戶，函式的入口網站），以及 hello 資料服務。</span><span class="sxs-lookup"><span data-stu-id="28b16-201">hello Management role is responsible for hello App Service Azure Resource Manager and API endpoints, portal extensions (admin, tenant, Functions portal), and hello data service.</span></span>
    - <span data-ttu-id="28b16-202">**發行者**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-202">**Publisher**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="28b16-203">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="28b16-203">This is hello minimum we recommend.</span></span> <span data-ttu-id="28b16-204">hello 發行者角色會負責透過 FTP 和 web 部署的內容發佈。</span><span class="sxs-lookup"><span data-stu-id="28b16-204">hello Publisher role is responsible for publishing content via FTP and web deployment.</span></span>
    - <span data-ttu-id="28b16-205">**前端**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-205">**FrontEnd**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="28b16-206">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="28b16-206">This is hello minimum we recommend.</span></span> <span data-ttu-id="28b16-207">hello 前端角色負責路由要求 tooApp 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="28b16-207">hello FrontEnd role is responsible for routing requests tooApp Service applications.</span></span>
    - <span data-ttu-id="28b16-208">**共用背景工作**： 根據預設，已經選取一個標準 A1 執行個體，但是您可能想 tooadd 更多。</span><span class="sxs-lookup"><span data-stu-id="28b16-208">**Shared Worker**: By default, one Standard A1 instance is selected, but you might want tooadd more.</span></span> <span data-ttu-id="28b16-209">身為系統管理員，您可以定義您的供應項目，並選擇任何 SKU 層。</span><span class="sxs-lookup"><span data-stu-id="28b16-209">As an administrator, you can define your offering and choose any SKU tier.</span></span> <span data-ttu-id="28b16-210">hello 層必須具有至少一個核心。</span><span class="sxs-lookup"><span data-stu-id="28b16-210">hello tiers must have a minimum of one core.</span></span> <span data-ttu-id="28b16-211">hello 共用背景工作角色負責主控 web、 行動裝置，或應用程式開發介面應用程式和 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="28b16-211">hello Shared Worker role is responsible for hosting web, mobile, or API applications and Azure Functions apps.</span></span>

    ![Azure Stack 上的 App Service 角色設定][9]

    > [!NOTE]
    > <span data-ttu-id="28b16-213">Hello technial preview 中 hello 應用程式服務資源提供者安裝程式也會部署標準 A1 執行個體 toooperate 為簡單的檔案伺服器 toosupport hello Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="28b16-213">In hello technical previews, hello App Service resource provider installer also deploys a Standard A1 instance toooperate as a simple file server toosupport hello Azure Resource Manager.</span></span> <span data-ttu-id="28b16-214">這會針對單一節點的連絡點加以保留。</span><span class="sxs-lookup"><span data-stu-id="28b16-214">This remains for a single-node point of contact.</span></span> <span data-ttu-id="28b16-215">對於生產工作負載，在公開上市 hello 應用程式服務安裝程式可讓您 hello 使用高可用性檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="28b16-215">For production workloads, at general availability hello App Service installer enables hello use of a high-availability file server.</span></span>

20. <span data-ttu-id="28b16-216">選擇您的部署**Windows Server 2016**從 hello hello 應用程式服務雲端計算資源提供者中所提供的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="28b16-216">Choose your deployment **Windows Server 2016** VM image from those available in hello compute resource provider for hello App Service cloud.</span></span> <span data-ttu-id="28b16-217">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="28b16-217">Click **Next**.</span></span> 

    ![Azure Stack 上的 App Service VM 映像選取項目][10]

21. <span data-ttu-id="28b16-219">Hello hello 雲端應用程式服務中設定的背景工作角色，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-219">Enter a user name and password for hello Worker roles configured in hello App Service cloud.</span></span> <span data-ttu-id="28b16-220">針對所有其他的 App Service 角色，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-220">Enter a user name and password for all other App Service roles.</span></span> <span data-ttu-id="28b16-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="28b16-221">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 認證項目][11]

22. <span data-ttu-id="28b16-223">在 hello 摘要畫面中，確認您所做的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="28b16-223">On hello summary screen, verify hello selections you made.</span></span> <span data-ttu-id="28b16-224">toomake 變更 hello 畫面，請返回並修改您的選擇。</span><span class="sxs-lookup"><span data-stu-id="28b16-224">toomake changes, go back through hello screens and modify your selections.</span></span> <span data-ttu-id="28b16-225">如果您要如何 hello 設定，請選取 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-225">If hello configuration is how you want it, select hello check box.</span></span> <span data-ttu-id="28b16-226">toostart hello 部署中，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="28b16-226">toostart hello deployment, click **Next**.</span></span> 

    ![Azure Stack 上的 App Service 選取項目摘要][12]

23. <span data-ttu-id="28b16-228">追蹤 hello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="28b16-228">Track hello installation progress.</span></span> <span data-ttu-id="28b16-229">Azure 堆疊上的應用程式服務大約需要約 45 too60 分鐘 toodeploy 根據 hello 預設選取項目。</span><span class="sxs-lookup"><span data-stu-id="28b16-229">App Service on Azure Stack takes about 45 too60 minutes toodeploy based on hello default selections.</span></span>

    ![Azure Stack 上的 App Service 安裝進度][13]

24. <span data-ttu-id="28b16-231">Hello 安裝程式已順利完成之後，請按一下**結束**。</span><span class="sxs-lookup"><span data-stu-id="28b16-231">After hello installer successfully finishes, click **Exit**.</span></span>

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a><span data-ttu-id="28b16-232">設定虛擬機器規模集整合 AD FS 服務主體上背景工作層和 SSO hello Azure 函式的入口網站和進階開發人員工具</span><span class="sxs-lookup"><span data-stu-id="28b16-232">Configure an AD FS service principal for virtual machine scale set integration on Worker tiers and SSO for hello Azure Functions portal and advanced developer tools</span></span>

>[!NOTE]
> <span data-ttu-id="28b16-233">這些步驟適用於的 tooAD FS 保護僅限 Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="28b16-233">These steps apply tooAD FS secured Azure Stack environments only.</span></span>

<span data-ttu-id="28b16-234">系統管理員需要 tooconfigure SSO 至：</span><span class="sxs-lookup"><span data-stu-id="28b16-234">Administrators need tooconfigure SSO to:</span></span>

* <span data-ttu-id="28b16-235">針對背景工作層上的虛擬機器擴展集整合設定服務主體。</span><span class="sxs-lookup"><span data-stu-id="28b16-235">Configure a service principal for virtual machine scale set integration on Worker tiers.</span></span>
* <span data-ttu-id="28b16-236">啟用進階開發人員工具，應用程式服務 (Kudu) 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="28b16-236">Enable hello advanced developer tools within App Service (Kudu).</span></span>
* <span data-ttu-id="28b16-237">啟用 hello hello Azure 函式的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="28b16-237">Enable hello use of hello Azure Functions portal experience.</span></span> 

<span data-ttu-id="28b16-238">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="28b16-238">Follow these steps:</span></span>

1. <span data-ttu-id="28b16-239">以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。</span><span class="sxs-lookup"><span data-stu-id="28b16-239">Open a PowerShell instance as azurestack\azurestackadmin.</span></span>

2. <span data-ttu-id="28b16-240">移 hello 指令碼下載並解壓縮在 hello toohello 位置[先決條件步驟](#Download-Required-Components)。</span><span class="sxs-lookup"><span data-stu-id="28b16-240">Go toohello location of hello scripts downloaded and extracted in hello [prerequisite step](#Download-Required-Components).</span></span>

3. <span data-ttu-id="28b16-241">[安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="28b16-241">[Install](azure-stack-powershell-install.md) and [configure an Azure Stack PowerShell environment](azure-stack-powershell-configure-admin.md).</span></span>

4. <span data-ttu-id="28b16-242">在 hello 相同的 PowerShell 工作階段中執行 hello **CreateIdentityApp.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-242">In hello same PowerShell session, run hello **CreateIdentityApp.ps1** script.</span></span> <span data-ttu-id="28b16-243">當系統提示您提供 Azure Active Directory (Azure AD) 租用戶識別碼時，請輸入 **ADFS**。</span><span class="sxs-lookup"><span data-stu-id="28b16-243">When you're prompted for your Azure Active Directory (Azure AD) tenant ID, enter **ADFS**.</span></span>

5. <span data-ttu-id="28b16-244">在 hello**認證**視窗中，輸入您的 AD FS 服務系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-244">In hello **Credential** window, enter your AD FS service admin account and password.</span></span> <span data-ttu-id="28b16-245">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="28b16-245">Click **OK**.</span></span>

6. <span data-ttu-id="28b16-246">輸入 hello hello 憑證檔案的路徑和憑證密碼[稍早建立的憑證](# Create certificates toobe used by App Service on Azure Stack)。</span><span class="sxs-lookup"><span data-stu-id="28b16-246">Enter hello certificate file path and certificate password for hello [certificate created earlier](# Create certificates toobe used by App Service on Azure Stack).</span></span> <span data-ttu-id="28b16-247">針對此步驟建立預設的 hello 憑證是 sso.appservice.local.azurestack.external.pfx。</span><span class="sxs-lookup"><span data-stu-id="28b16-247">hello certificate created for this step by default is sso.appservice.local.azurestack.external.pfx.</span></span>

7. <span data-ttu-id="28b16-248">hello 指令碼在 hello 租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="28b16-248">hello script creates a new application in hello tenant Azure AD and generates a new PowerShell script.</span></span>

8. <span data-ttu-id="28b16-249">複製 hello 識別應用程式的憑證檔案和 hello 產生指令碼 toohello **CN0 VM**使用遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="28b16-249">Copy hello identity app certificate file and hello generated script toohello **CN0-VM** by using a remote desktop session.</span></span>

9. <span data-ttu-id="28b16-250">傳回太**CN0 VM**。</span><span class="sxs-lookup"><span data-stu-id="28b16-250">Return too**CN0-VM**.</span></span>

10. <span data-ttu-id="28b16-251">開啟系統管理員 PowerShell 視窗，並瀏覽 toohello hello 指令碼檔案和憑證，已複製在步驟 7 中的目錄。</span><span class="sxs-lookup"><span data-stu-id="28b16-251">Open an administrator PowerShell window, and browse toohello directory where hello script file and certificate were copied in step 7.</span></span>

11. <span data-ttu-id="28b16-252">執行 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="28b16-252">Run hello script file.</span></span> <span data-ttu-id="28b16-253">此指令碼檔案中 hello 應用程式服務在 Azure 堆疊設定輸入 hello 屬性，並起始所有前端及管理角色上的修復操作。</span><span class="sxs-lookup"><span data-stu-id="28b16-253">This script file enters hello properties in hello App Service on Azure Stack configuration and initiates a repair operation on all FrontEnd and Management roles.</span></span>

| <span data-ttu-id="28b16-254">參數</span><span class="sxs-lookup"><span data-stu-id="28b16-254">Parameter</span></span> | <span data-ttu-id="28b16-255">必要/選用</span><span class="sxs-lookup"><span data-stu-id="28b16-255">Required/optional</span></span> | <span data-ttu-id="28b16-256">預設值</span><span class="sxs-lookup"><span data-stu-id="28b16-256">Default value</span></span> | <span data-ttu-id="28b16-257">說明</span><span class="sxs-lookup"><span data-stu-id="28b16-257">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="28b16-258">DirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="28b16-258">DirectoryTenantName</span></span> | <span data-ttu-id="28b16-259">強制</span><span class="sxs-lookup"><span data-stu-id="28b16-259">Mandatory</span></span> | <span data-ttu-id="28b16-260">Null</span><span class="sxs-lookup"><span data-stu-id="28b16-260">Null</span></span> | <span data-ttu-id="28b16-261">使用**ADFS** hello AD FS 環境</span><span class="sxs-lookup"><span data-stu-id="28b16-261">Use **ADFS** for hello AD FS environment</span></span> |
| <span data-ttu-id="28b16-262">TenantAzure Resource ManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="28b16-262">TenantAzure Resource ManagerEndpoint</span></span> | <span data-ttu-id="28b16-263">強制</span><span class="sxs-lookup"><span data-stu-id="28b16-263">Mandatory</span></span> | <span data-ttu-id="28b16-264">management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="28b16-264">management.local.azurestack.external</span></span> | <span data-ttu-id="28b16-265">hello 租用戶 Azure 資源管理員端點</span><span class="sxs-lookup"><span data-stu-id="28b16-265">hello tenant Azure Resource Manager endpoint</span></span> |
| <span data-ttu-id="28b16-266">AzureStackCredential</span><span class="sxs-lookup"><span data-stu-id="28b16-266">AzureStackCredential</span></span> | <span data-ttu-id="28b16-267">強制</span><span class="sxs-lookup"><span data-stu-id="28b16-267">Mandatory</span></span> | <span data-ttu-id="28b16-268">Null</span><span class="sxs-lookup"><span data-stu-id="28b16-268">Null</span></span> | <span data-ttu-id="28b16-269">hello AD FS 服務系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="28b16-269">hello AD FS service admin account</span></span> |
| <span data-ttu-id="28b16-270">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="28b16-270">CertificateFilePath</span></span> | <span data-ttu-id="28b16-271">強制</span><span class="sxs-lookup"><span data-stu-id="28b16-271">Mandatory</span></span> | <span data-ttu-id="28b16-272">Null</span><span class="sxs-lookup"><span data-stu-id="28b16-272">Null</span></span> | <span data-ttu-id="28b16-273">路徑 toohello 識別應用程式的憑證檔案先前產生</span><span class="sxs-lookup"><span data-stu-id="28b16-273">Path toohello identity application certificate file generated earlier</span></span> |
| <span data-ttu-id="28b16-274">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="28b16-274">CertificatePassword</span></span> | <span data-ttu-id="28b16-275">強制</span><span class="sxs-lookup"><span data-stu-id="28b16-275">Mandatory</span></span> | <span data-ttu-id="28b16-276">Null</span><span class="sxs-lookup"><span data-stu-id="28b16-276">Null</span></span> | <span data-ttu-id="28b16-277">使用 tooprotect hello 憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="28b16-277">Password used tooprotect hello certificate private key</span></span> |
| <span data-ttu-id="28b16-278">DomainName</span><span class="sxs-lookup"><span data-stu-id="28b16-278">DomainName</span></span> | <span data-ttu-id="28b16-279">必要</span><span class="sxs-lookup"><span data-stu-id="28b16-279">Required</span></span> | <span data-ttu-id="28b16-280">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="28b16-280">local.azurestack.external</span></span> | <span data-ttu-id="28b16-281">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="28b16-281">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="28b16-282">AdfsMachineName</span><span class="sxs-lookup"><span data-stu-id="28b16-282">AdfsMachineName</span></span> | <span data-ttu-id="28b16-283">選用</span><span class="sxs-lookup"><span data-stu-id="28b16-283">Optional</span></span> | <span data-ttu-id="28b16-284">AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="28b16-284">AD FS machine name, for example, AzS-ADFS01.azurestack.local</span></span> |


## <a name="validate-hello-app-service-on-azure-stack-installation"></a><span data-ttu-id="28b16-285">驗證 Azure 堆疊安裝上的 hello 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="28b16-285">Validate hello App Service on Azure Stack installation</span></span>

1. <span data-ttu-id="28b16-286">在 hello Azure 堆疊管理員入口網站中瀏覽 toohello hello 安裝程式所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="28b16-286">In hello Azure Stack admin portal, browse toohello resource group created by hello installer.</span></span> <span data-ttu-id="28b16-287">根據預設值，此群組是 **APPSERVICE-LOCAL**。</span><span class="sxs-lookup"><span data-stu-id="28b16-287">By default, this group is **APPSERVICE-LOCAL**.</span></span>

2. <span data-ttu-id="28b16-288">找出 hello **CN0 VM**。</span><span class="sxs-lookup"><span data-stu-id="28b16-288">Locate hello **CN0-VM**.</span></span> <span data-ttu-id="28b16-289">按一下 tooconnect toohello VM，**連接**hello 上**虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28b16-289">tooconnect toohello VM, click **Connect** on hello **Virtual Machine** blade.</span></span>

3. <span data-ttu-id="28b16-290">在此 vm 的 hello 桌面上，按兩下**網站雲端管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="28b16-290">On hello desktop of this VM, double-click **Web Cloud Management Console**.</span></span>

4. <span data-ttu-id="28b16-291">跳過**管理的伺服器**。</span><span class="sxs-lookup"><span data-stu-id="28b16-291">Go too**Managed Servers**.</span></span>

5. <span data-ttu-id="28b16-292">當所有 hello 機器顯示**準備**一或多個背景工作，請繼續進行 toostep 6。</span><span class="sxs-lookup"><span data-stu-id="28b16-292">When all hello machines display **Ready** for one or more Workers, proceed toostep 6.</span></span>

6. <span data-ttu-id="28b16-293">關閉遠端桌面的電腦 hello，並傳回 toohello hello 應用程式服務安裝程式的執行所在的電腦。</span><span class="sxs-lookup"><span data-stu-id="28b16-293">Close hello remote desktop machine, and return toohello machine where you executed hello App Service installer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="28b16-294">您不需要一或多個工作者 toodisplay toowait**準備**toocomplete hello 安裝 Azure 堆疊上的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="28b16-294">You don't need toowait for one or more Workers toodisplay **Ready** toocomplete hello installation of App Service on Azure Stack.</span></span> <span data-ttu-id="28b16-295">不過，您需要至少一個背景工作的準備 toodeploy 行動、 web API 應用程式或 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="28b16-295">However, you need a minimum of one Worker that's ready toodeploy a web, mobile, or API app or Azure Functions.</span></span>
    
    ![Azure Stack 上的 App Service 受管理伺服器狀態][14]

## <a name="test-drive-app-service-on-azure-stack"></a><span data-ttu-id="28b16-297">測試 Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="28b16-297">Test drive App Service on Azure Stack</span></span>

<span data-ttu-id="28b16-298">您部署及註冊 hello 應用程式服務資源提供者之後，測試 toomake 確定租用戶可以將 web、 mobile 及 API 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="28b16-298">After you deploy and register hello App Service resource provider, test it toomake sure that tenants can deploy web, mobile, and API apps.</span></span>

> [!NOTE]
> <span data-ttu-id="28b16-299">您需要 toocreate hello 計劃中的 hello Microsoft.Web 命名空間提供項目。</span><span class="sxs-lookup"><span data-stu-id="28b16-299">You need toocreate an offer that has hello Microsoft.Web namespace within hello plan.</span></span> <span data-ttu-id="28b16-300">然後，您需要 toohave 訂閱 toothis 優惠的租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28b16-300">Then you need toohave a tenant subscription that subscribes toothis offer.</span></span> <span data-ttu-id="28b16-301">如需詳細資訊，請參閱[建立供應項目](azure-stack-create-offer.md)和[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="28b16-301">For more information, see  [Create offer](azure-stack-create-offer.md) and [Create plan](azure-stack-create-plan.md).</span></span>
>

<span data-ttu-id="28b16-302">您*必須*有使用 Azure 堆疊上的應用程式服務的租用戶訂用帳戶 toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28b16-302">You *must* have a tenant subscription toocreate applications that use App Service on Azure Stack.</span></span> <span data-ttu-id="28b16-303">服務系統管理員可以完成 hello 系統管理入口網站中的 hello 唯一功能是相關的 toohello 資源提供者管理的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="28b16-303">hello only capabilities that a service admin can complete within hello admin portal are related toohello resource provider administration of App Service.</span></span> <span data-ttu-id="28b16-304">這些功能包括新增容量、設定部署來源，以及新增背景工作層和 SKU。</span><span class="sxs-lookup"><span data-stu-id="28b16-304">These capabilities include adding capacity, configuring deployment sources, and adding Worker tiers and SKUs.</span></span>

<span data-ttu-id="28b16-305">Hello 第三個技術預覽、 toocreate web、 行動裝置版及 API 應用程式，您必須使用 hello 租用戶入口網站，並有租用戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28b16-305">As of hello third technical preview, toocreate web, mobile, and API apps you must use hello tenant portal and have a tenant subscription.</span></span>  

1. <span data-ttu-id="28b16-306">在 hello Azure 堆疊租用戶入口網站中，按一下 **新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="28b16-306">In hello Azure Stack tenant portal, click **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="28b16-307">在 hello **Web 應用程式**刀鋒視窗中，輸入的名稱在 hello **Web 應用程式**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-307">On hello **Web App** blade, type a name in hello **Web app** box.</span></span>

3. <span data-ttu-id="28b16-308">按一下 [資源群組] 下方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="28b16-308">Under **Resource Group**, click **New**.</span></span> <span data-ttu-id="28b16-309">然後輸入 hello 名稱**資源群組**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-309">Then type a name in hello **Resource Group** box.</span></span>

4. <span data-ttu-id="28b16-310">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="28b16-310">Click **App Service plan/Location** > **Create New**.</span></span>

5. <span data-ttu-id="28b16-311">在 hello **App Service 方案**刀鋒視窗中，輸入的名稱在 hello **App Service 方案**方塊。</span><span class="sxs-lookup"><span data-stu-id="28b16-311">On hello **App Service plan** blade, type a name in hello **App Service plan** box.</span></span>

6. <span data-ttu-id="28b16-312">按一下 [定價層] > [免費 - 共用] 或 [共用 - 共用] > [選取] > [確定] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="28b16-312">Click **Pricing tier** > **Free-Shared** or **Shared-Shared** > **Select** > **OK** > **Create**.</span></span>

7. <span data-ttu-id="28b16-313">在下一分鐘 hello 新 web 應用程式的磚會顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="28b16-313">In under a minute, a tile for hello new web app appears on hello dashboard.</span></span> <span data-ttu-id="28b16-314">按一下 hello 磚。</span><span class="sxs-lookup"><span data-stu-id="28b16-314">Click hello tile.</span></span>

8. <span data-ttu-id="28b16-315">在 hello **Web 應用程式**刀鋒視窗中，按一下 **瀏覽**tooview hello 預設網站，此應用程式。</span><span class="sxs-lookup"><span data-stu-id="28b16-315">On hello **Web App** blade, click **Browse** tooview hello default website for this app.</span></span>

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a><span data-ttu-id="28b16-316">部署 WordPress、DNN 或 Django 網站 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="28b16-316">Deploy a WordPress, DNN, or Django website (optional)</span></span>

1. <span data-ttu-id="28b16-317">在 hello Azure 堆疊租用戶入口網站中，按一下   **+** 。</span><span class="sxs-lookup"><span data-stu-id="28b16-317">In hello Azure Stack tenant portal, click **+**.</span></span> <span data-ttu-id="28b16-318">移 toohello Azure Marketplace 中部署如 Django 網站，然後等候順利完成。</span><span class="sxs-lookup"><span data-stu-id="28b16-318">Go toohello Azure Marketplace, deploy a Django website, and wait for successful completion.</span></span> <span data-ttu-id="28b16-319">hello Django web 平台會使用檔案系統為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="28b16-319">hello Django web platform uses a file system-based database.</span></span> <span data-ttu-id="28b16-320">它不需要任何額外的資源提供者，例如 SQL 或 MySQL。</span><span class="sxs-lookup"><span data-stu-id="28b16-320">It doesn’t require any additional resource providers such as SQL or MySQL.</span></span>

2. <span data-ttu-id="28b16-321">如果您也會部署 MySQL 資源提供者，您可以部署的 hello Marketplace WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="28b16-321">If you also deployed a MySQL resource provider, you can deploy a WordPress website from hello Marketplace.</span></span> <span data-ttu-id="28b16-322">當系統提示您為資料庫參數時，輸入 hello 使用者名稱做為 *User1@Server1*使用 hello 使用者名稱和您選擇的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="28b16-322">When you're prompted for database parameters, enter hello user name as *User1@Server1*, with hello user name and server name of your choice.</span></span>

3. <span data-ttu-id="28b16-323">如果您也會部署 SQL Server 資源提供者，您可以部署的 hello Marketplace DNN 網站。</span><span class="sxs-lookup"><span data-stu-id="28b16-323">If you also deployed a SQL Server resource provider, you can deploy a DNN website from hello Marketplace.</span></span> <span data-ttu-id="28b16-324">當系統提示您為資料庫參數時，請選取資料庫 hello 電腦是連線的 tooyour 資源提供者的 SQL Server 執行中。</span><span class="sxs-lookup"><span data-stu-id="28b16-324">When you're prompted for database parameters, pick a database in hello computer running SQL Server that's connected tooyour resource provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28b16-325">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28b16-325">Next steps</span></span>

<span data-ttu-id="28b16-326">您也可以嘗試其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)。</span><span class="sxs-lookup"><span data-stu-id="28b16-326">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

- [<span data-ttu-id="28b16-327">SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="28b16-327">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
- [<span data-ttu-id="28b16-328">MySQL 資源提供者</span><span class="sxs-lookup"><span data-stu-id="28b16-328">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)

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
