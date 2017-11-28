---
title: "部署 App Service：Azure Stack | Microsoft Docs"
description: "部署 Azure Stack 中之 App Service 的詳細指導方針"
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
ms.openlocfilehash: 41be7bca865f39b445e8f99450c4acde535c0806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooazure-stack"></a><span data-ttu-id="eefae-103">新增應用程式服務資源提供者 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="eefae-103">Add an App Service resource provider tooAzure Stack</span></span>

<span data-ttu-id="eefae-104">如果您想 tooenable，您的租用戶 toocreate web、 行動裝置版和其堆疊 Azure 訂用帳戶的 API 應用程式，您必須新增[Azure App Service 資源提供者](azure-stack-app-service-overview.md)tooyour Azure 堆疊部署。</span><span class="sxs-lookup"><span data-stu-id="eefae-104">If you want tooenable your tenants toocreate web, mobile, and API applications with their Azure Stack subscription, you must add an [Azure App Service resource provider](azure-stack-app-service-overview.md) tooyour Azure Stack deployment.</span></span> <span data-ttu-id="eefae-105">請遵循本文章中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="eefae-105">Follow hello steps in this article.</span></span>

## <a name="download-hello-required-components"></a><span data-ttu-id="eefae-106">下載所需的 hello 元件</span><span class="sxs-lookup"><span data-stu-id="eefae-106">Download hello required components</span></span>

1. <span data-ttu-id="eefae-107">下載 hello[上 Azure 堆疊 preview 安裝程式的應用程式服務](http://aka.ms/appsvconmasrc1installer)。</span><span class="sxs-lookup"><span data-stu-id="eefae-107">Download hello [App Service on Azure Stack preview installer](http://aka.ms/appsvconmasrc1installer).</span></span>

2. <span data-ttu-id="eefae-108">下載 hello [Azure 堆疊部署 helper 指令碼的應用程式服務](http://aka.ms/appsvconmasrc1helper)。</span><span class="sxs-lookup"><span data-stu-id="eefae-108">Download hello [App Service on Azure Stack deployment helper scripts](http://aka.ms/appsvconmasrc1helper).</span></span>

3. <span data-ttu-id="eefae-109">從 hello helper 指令碼 zip 檔案解壓縮 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="eefae-109">Extract hello files from hello helper scripts zip file.</span></span> <span data-ttu-id="eefae-110">hello 下列檔案和資料夾結構會顯示：</span><span class="sxs-lookup"><span data-stu-id="eefae-110">hello following files and folder structure appear:</span></span>

   - <span data-ttu-id="eefae-111">Create-AppServiceCerts.ps1</span><span class="sxs-lookup"><span data-stu-id="eefae-111">Create-AppServiceCerts.ps1</span></span>
   - <span data-ttu-id="eefae-112">Create-IdentityApp.ps1</span><span class="sxs-lookup"><span data-stu-id="eefae-112">Create-IdentityApp.ps1</span></span>
   - <span data-ttu-id="eefae-113">模組</span><span class="sxs-lookup"><span data-stu-id="eefae-113">Modules</span></span>
      - <span data-ttu-id="eefae-114">AzureStack.Identity.psm1</span><span class="sxs-lookup"><span data-stu-id="eefae-114">AzureStack.Identity.psm1</span></span>
      - <span data-ttu-id="eefae-115">GraphAPI.psm1</span><span class="sxs-lookup"><span data-stu-id="eefae-115">GraphAPI.psm1</span></span>
   
## <a name="create-certificates-required-by-app-service-on-azure-stack"></a><span data-ttu-id="eefae-116">建立 Azure Stack 上之 App Service 所需的憑證</span><span class="sxs-lookup"><span data-stu-id="eefae-116">Create certificates required by App Service on Azure Stack</span></span>

<span data-ttu-id="eefae-117">此第一個指令碼搭配 hello Azure 堆疊憑證授權單位 toocreate 三個憑證所需的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="eefae-117">This first script works with hello Azure Stack certificate authority toocreate three certificates that are needed by App Service.</span></span> <span data-ttu-id="eefae-118">Hello Azure 堆疊主機上執行 hello 指令碼，請確定您 azurestack\AzureStackAdmin 作為執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="eefae-118">Run hello script on hello Azure Stack host and ensure that you're running PowerShell as azurestack\AzureStackAdmin.</span></span>

1. <span data-ttu-id="eefae-119">Azurestack\AzureStackAdmin 身分執行的 PowerShell 工作階段，執行 hello**建立 AppServiceCerts.ps1** hello 資料夾解壓縮 hello helper 指令碼的指令碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-119">In a PowerShell session running as azurestack\AzureStackAdmin, execute hello **Create-AppServiceCerts.ps1** script from hello folder where you extracted hello helper scripts.</span></span> <span data-ttu-id="eefae-120">hello 指令碼會建立三個憑證中相同的資料夾 hello 建立憑證的指令碼應用程式服務時，必須的 hello。</span><span class="sxs-lookup"><span data-stu-id="eefae-120">hello script creates three certificates in hello same folder as hello create certificates script that App Service needs.</span></span>

2. <span data-ttu-id="eefae-121">輸入密碼 toosecure hello.pfx 檔案，並記下它。</span><span class="sxs-lookup"><span data-stu-id="eefae-121">Enter a password toosecure hello .pfx files, and make a note of it.</span></span> <span data-ttu-id="eefae-122">您將需要 tooenter hello 應用程式服務在 Azure 堆疊安裝程式中。</span><span class="sxs-lookup"><span data-stu-id="eefae-122">You will need tooenter it in hello App Service on Azure Stack installer.</span></span>

### <a name="create-appservicecertsps1-parameters"></a><span data-ttu-id="eefae-123">Create-AppServiceCerts.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="eefae-123">Create-AppServiceCerts.ps1 parameters</span></span>

| <span data-ttu-id="eefae-124">參數</span><span class="sxs-lookup"><span data-stu-id="eefae-124">Parameter</span></span> | <span data-ttu-id="eefae-125">必要/選用</span><span class="sxs-lookup"><span data-stu-id="eefae-125">Required/optional</span></span> | <span data-ttu-id="eefae-126">預設值</span><span class="sxs-lookup"><span data-stu-id="eefae-126">Default value</span></span> | <span data-ttu-id="eefae-127">說明</span><span class="sxs-lookup"><span data-stu-id="eefae-127">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eefae-128">pfxPassword</span><span class="sxs-lookup"><span data-stu-id="eefae-128">pfxPassword</span></span> | <span data-ttu-id="eefae-129">必要</span><span class="sxs-lookup"><span data-stu-id="eefae-129">Required</span></span> | <span data-ttu-id="eefae-130">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-130">Null</span></span> | <span data-ttu-id="eefae-131">使用 tooprotect hello 憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="eefae-131">Password used tooprotect hello certificate private key</span></span> |
| <span data-ttu-id="eefae-132">DomainName</span><span class="sxs-lookup"><span data-stu-id="eefae-132">DomainName</span></span> | <span data-ttu-id="eefae-133">必要</span><span class="sxs-lookup"><span data-stu-id="eefae-133">Required</span></span> | <span data-ttu-id="eefae-134">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="eefae-134">local.azurestack.external</span></span> | <span data-ttu-id="eefae-135">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="eefae-135">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="eefae-136">CertificateAuthority</span><span class="sxs-lookup"><span data-stu-id="eefae-136">CertificateAuthority</span></span> | <span data-ttu-id="eefae-137">必要</span><span class="sxs-lookup"><span data-stu-id="eefae-137">Required</span></span> | <span data-ttu-id="eefae-138">AzS-CA01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="eefae-138">AzS-CA01.azurestack.local</span></span> | <span data-ttu-id="eefae-139">憑證授權單位端點</span><span class="sxs-lookup"><span data-stu-id="eefae-139">Certificate authority endpoint</span></span> |

## <a name="use-hello-installer-toodownload-and-install-app-service-on-azure-stack"></a><span data-ttu-id="eefae-140">使用 hello installer toodownload 並安裝 Azure 堆疊上的應用程式服務</span><span class="sxs-lookup"><span data-stu-id="eefae-140">Use hello installer toodownload and install App Service on Azure Stack</span></span>

<span data-ttu-id="eefae-141">hello appservice.exe 安裝程式將會：</span><span class="sxs-lookup"><span data-stu-id="eefae-141">hello appservice.exe installer will:</span></span>

* <span data-ttu-id="eefae-142">會提示您 tooaccept hello Microsoft 和協力廠商軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="eefae-142">Prompt you tooaccept hello Microsoft and third-party Software License Terms.</span></span>
* <span data-ttu-id="eefae-143">收集 Azure Stack 部署資訊。</span><span class="sxs-lookup"><span data-stu-id="eefae-143">Collect Azure Stack deployment information.</span></span>
* <span data-ttu-id="eefae-144">建立 blob 容器中 hello 指定堆疊 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="eefae-144">Create a blob container in hello specified Azure Stack storage account.</span></span>
* <span data-ttu-id="eefae-145">下載 hello 所需的檔案 tooinstall hello 應用程式服務資源提供者。</span><span class="sxs-lookup"><span data-stu-id="eefae-145">Download hello files needed tooinstall hello App Service resource provider.</span></span>
* <span data-ttu-id="eefae-146">準備 hello 安裝 toodeploy hello hello Azure 堆疊環境中的應用程式服務資源提供者。</span><span class="sxs-lookup"><span data-stu-id="eefae-146">Prepare hello installation toodeploy hello App Service resource provider in hello Azure Stack environment.</span></span>
* <span data-ttu-id="eefae-147">上傳 hello 檔案 toohello 應用程式服務的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="eefae-147">Upload hello files toohello App Service storage account.</span></span>
* <span data-ttu-id="eefae-148">部署 hello 應用程式服務資源提供者。</span><span class="sxs-lookup"><span data-stu-id="eefae-148">Deploy hello App Service resource provider.</span></span>
* <span data-ttu-id="eefae-149">建立適用於 App Service 的 DNS 區域與項目。</span><span class="sxs-lookup"><span data-stu-id="eefae-149">Create a DNS zone and entries for App Service.</span></span>
* <span data-ttu-id="eefae-150">註冊 hello 應用程式服務資源提供者。</span><span class="sxs-lookup"><span data-stu-id="eefae-150">Register hello App Service resource provider.</span></span>
* <span data-ttu-id="eefae-151">註冊 hello 應用程式服務主機庫項目。</span><span class="sxs-lookup"><span data-stu-id="eefae-151">Register hello App Service gallery items.</span></span>

<span data-ttu-id="eefae-152">hello 下列步驟會引導您進行 hello 安裝階段。</span><span class="sxs-lookup"><span data-stu-id="eefae-152">hello following steps guide you through hello installation stages.</span></span>

> [!NOTE]
> <span data-ttu-id="eefae-153">您*必須*使用提高權限的帳戶 （本機或網域系統管理員） toorun hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-153">You *must* use an elevated account (local or domain administrator) toorun hello installer.</span></span> <span data-ttu-id="eefae-154">如果您以 azurestack\azurestackuser 身分登入，則系統會提示您提供已提高權限的認證。</span><span class="sxs-lookup"><span data-stu-id="eefae-154">If you sign in as azurestack\azurestackuser, you're prompted for elevated credentials.</span></span>

1. <span data-ttu-id="eefae-155">以 azurestack\AzureStackAdmin 身分執行 appservice.exe。</span><span class="sxs-lookup"><span data-stu-id="eefae-155">Run appservice.exe as azurestack\AzureStackAdmin.</span></span>

2. <span data-ttu-id="eefae-156">按一下 [在您的 Azure Stack 雲端上部署 App Service]。</span><span class="sxs-lookup"><span data-stu-id="eefae-156">Click **Deploy App Service on your Azure Stack cloud**.</span></span>

    ![Azure Stack 上的 App Service 安裝程式][1]

3. <span data-ttu-id="eefae-158">檢閱並接受 hello Microsoft 發行前版本授權條款，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eefae-158">Review and accept hello Microsoft Software Prerelease License Terms, and click **Next**.</span></span>

4. <span data-ttu-id="eefae-159">檢閱並接受 hello 協力廠商授權條款，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eefae-159">Review and accept hello third-party license terms, and click **Next**.</span></span>

5. <span data-ttu-id="eefae-160">檢閱 hello 應用程式服務雲端組態資訊，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="eefae-160">Review hello App Service cloud configuration information, and click **Next**.</span></span>

    ![Azure Stack App Service 上的 App Service 雲端設定][2]

    > [!NOTE]
    > <span data-ttu-id="eefae-162">hello 應用程式服務在 Azure 堆疊安裝程式提供單一節點 Azure 堆疊安裝 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="eefae-162">hello App Service on Azure Stack installer provides hello default values for a one-node Azure Stack installation.</span></span> <span data-ttu-id="eefae-163">如果您部署 Azure 堆疊 （例如，hello 網域尾碼） 時，您可以自訂選項，會據以需要 tooedit hello 值，此視窗中。</span><span class="sxs-lookup"><span data-stu-id="eefae-163">If you customized options when you deployed Azure Stack (for example, hello domain suffix), you need tooedit hello values in this window accordingly.</span></span> <span data-ttu-id="eefae-164">例如，如果您使用 hello 網域尾碼 mycloud.com，您管理 Azure 資源管理員端點需要 toochange tooadminmanagement。[region]。 mycloud.com。</span><span class="sxs-lookup"><span data-stu-id="eefae-164">For example, if you use hello domain suffix mycloud.com, your admin Azure Resource Manager endpoint needs toochange tooadminmanagement.[region].mycloud.com.</span></span>

6. <span data-ttu-id="eefae-165">按一下 hello**連接**按鈕的下一個 toohello **Azure 堆疊訂用帳戶**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-165">Click hello **Connect** button next toohello **Azure Stack Subscriptions** box.</span></span>

   - <span data-ttu-id="eefae-166">如果您使用 Azure Active Directory (Azure AD)，就必須輸入您的 Azure AD 管理帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-166">If you're using Azure Active Directory (Azure AD), you must enter your Azure AD admin account and password.</span></span> <span data-ttu-id="eefae-167">按一下 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-167">Click **Sign In**.</span></span> <span data-ttu-id="eefae-168">您*必須*輸入您部署 Azure 堆疊時，您所提供的 hello Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eefae-168">You *must* enter hello Azure AD account that you provided when you deployed Azure Stack.</span></span>
   - <span data-ttu-id="eefae-169">如果您使用 Active Directory 同盟服務 (AD FS)，就必須提供您的管理帳戶，例如 azurestackadmin@azurestack.local。</span><span class="sxs-lookup"><span data-stu-id="eefae-169">If you're using Active Directory Federation Services (AD FS), you must provide your admin account, for example, azurestackadmin@azurestack.local.</span></span> <span data-ttu-id="eefae-170">輸入您的密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="eefae-170">Enter your password, and click **Sign In**.</span></span>

7. <span data-ttu-id="eefae-171">選取您的訂閱中 hello **Azure 堆疊訂用帳戶**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-171">Select your subscription in hello **Azure Stack Subscriptions** box.</span></span>

8. <span data-ttu-id="eefae-172">在 hello **Azure 堆疊位置**方塊中，選取 hello 對應您要部署的 toohello 區域的位置。</span><span class="sxs-lookup"><span data-stu-id="eefae-172">In hello **Azure Stack Locations** box, select hello location that corresponds toohello region you're deploying.</span></span> <span data-ttu-id="eefae-173">例如，選取 [本機]。</span><span class="sxs-lookup"><span data-stu-id="eefae-173">For example, select **local**.</span></span> <span data-ttu-id="eefae-174">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-174">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 訂用帳戶選取項目][3]

9. <span data-ttu-id="eefae-176">輸入 hello**資源群組名稱**為您的應用程式服務部署。</span><span class="sxs-lookup"><span data-stu-id="eefae-176">Enter hello **Resource Group Name** for your App Service deployment.</span></span> <span data-ttu-id="eefae-177">根據預設，此屬性設定太**APPSERVICE 本機**。</span><span class="sxs-lookup"><span data-stu-id="eefae-177">By default, it's set too**APPSERVICE-LOCAL**.</span></span>

10. <span data-ttu-id="eefae-178">輸入 hello**儲存體帳戶名稱**想 App Service toocreate hello 安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="eefae-178">Enter hello **Storage Account Name** you want App Service toocreate as part of hello installation.</span></span> <span data-ttu-id="eefae-179">根據預設，此屬性設定太**appsvclocalstor**。</span><span class="sxs-lookup"><span data-stu-id="eefae-179">By default, it's set too**appsvclocalstor**.</span></span>

11. <span data-ttu-id="eefae-180">輸入 hello 的使用的 toohost hello 應用程式服務資源提供者資料庫的執行個體 hello SQL Server 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="eefae-180">Enter hello SQL Server details for hello instance that's used toohost hello App Service resource provider databases.</span></span> <span data-ttu-id="eefae-181">按一下**下一步**，和 hello 安裝程式會驗證 hello SQL 連接屬性。</span><span class="sxs-lookup"><span data-stu-id="eefae-181">Click **Next**, and hello installer validates hello SQL connection properties.</span></span>

    ![Azure Stack 上的 App Service 資源群組、儲存體和 SQL Server 資訊][4]

12. <span data-ttu-id="eefae-183">按一下 hello**瀏覽**按鈕的下一個 toohello**應用程式服務的預設 SSL 憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-183">Click hello **Browse** button next toohello **App Service default SSL certificate file** box.</span></span> <span data-ttu-id="eefae-184">移 toohello **_.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="eefae-184">Go toohello **_.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="eefae-185">如果您在建立 hello 憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="eefae-185">If you specified a different location and domain suffix when you created hello certificate, select hello corresponding certificate.</span></span>

13. <span data-ttu-id="eefae-186">輸入當您建立 hello 憑證的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-186">Enter hello certificate password that you set when you created hello certificate.</span></span>

14. <span data-ttu-id="eefae-187">按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的 SSL 憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-187">Click hello **Browse** button next toohello **Resource provider SSL certificate file** box.</span></span> <span data-ttu-id="eefae-188">移 toohello **api.appservice.local.AzureStack.external**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="eefae-188">Go toohello **api.appservice.local.AzureStack.external** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span> <span data-ttu-id="eefae-189">如果您在建立憑證時指定不同的位置和網域尾碼，請選取 hello 對應的憑證。</span><span class="sxs-lookup"><span data-stu-id="eefae-189">If you specified a different location and domain suffix when you created certificates, select hello corresponding certificate.</span></span>

15. <span data-ttu-id="eefae-190">輸入當您建立 hello 憑證的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-190">Enter hello certificate password that you set when you created hello certificate.</span></span>

16. <span data-ttu-id="eefae-191">按一下 hello**瀏覽**按鈕的下一個 toohello**資源提供者的根憑證檔案**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-191">Click hello **Browse** button next toohello **Resource provider root certificate file** box.</span></span> <span data-ttu-id="eefae-192">移 toohello **AzureStackCertificationAuthority**憑證[稍早建立](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps)。</span><span class="sxs-lookup"><span data-stu-id="eefae-192">Go toohello **AzureStackCertificationAuthority** certificate [created earlier](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).</span></span>

17. <span data-ttu-id="eefae-193">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-193">Click **Next**.</span></span> <span data-ttu-id="eefae-194">hello 安裝程式會確認提供的 hello 憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-194">hello installer verifies hello certificate password provided.</span></span>

    ![Azure Stack 上的 App Service 憑證詳細資料][5]

18. <span data-ttu-id="eefae-196">檢閱 hello 應用程式服務角色設定。</span><span class="sxs-lookup"><span data-stu-id="eefae-196">Review hello App Service role configuration.</span></span> <span data-ttu-id="eefae-197">hello 預設值會填入 hello 最小建議執行個體的 Sku 為每個角色。</span><span class="sxs-lookup"><span data-stu-id="eefae-197">hello defaults are populated with hello minimum recommended instance SKUs for each role.</span></span> <span data-ttu-id="eefae-198">在規劃部署時 toohelp 係核心和記憶體需求的摘要。</span><span class="sxs-lookup"><span data-stu-id="eefae-198">A summary of core and memory requirements is provided toohelp plan your deployment.</span></span> <span data-ttu-id="eefae-199">進行選擇之後，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="eefae-199">After you make your selections, click **Next**.</span></span>

    - <span data-ttu-id="eefae-200">**控制器**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-200">**Controller**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="eefae-201">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="eefae-201">This is hello minimum we recommend.</span></span> <span data-ttu-id="eefae-202">hello 控制器角色負責管理和維護的 hello 雲端應用程式服務的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="eefae-202">hello Controller role is responsible for managing and maintaining hello health of hello App Service cloud.</span></span>
    - <span data-ttu-id="eefae-203">**管理**：預設會選取一個標準 A2 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-203">**Management**: By default, one Standard A2 instance is selected.</span></span> <span data-ttu-id="eefae-204">tooprovide 容錯移轉時，我們建議兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-204">tooprovide failover, we recommend two instances.</span></span> <span data-ttu-id="eefae-205">hello 管理角色負責 hello 應用程式服務的 Azure 資源管理員和 API 端點、 入口網站擴充功能 （系統管理員、 租用戶，函式的入口網站），以及 hello 資料服務。</span><span class="sxs-lookup"><span data-stu-id="eefae-205">hello Management role is responsible for hello App Service Azure Resource Manager and API endpoints, portal extensions (admin, tenant, Functions portal), and hello data service.</span></span>
    - <span data-ttu-id="eefae-206">**發行者**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-206">**Publisher**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="eefae-207">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="eefae-207">This is hello minimum we recommend.</span></span> <span data-ttu-id="eefae-208">hello 發行者角色會負責透過 FTP 和 web 部署的內容發佈。</span><span class="sxs-lookup"><span data-stu-id="eefae-208">hello Publisher role is responsible for publishing content via FTP and web deployment.</span></span>
    - <span data-ttu-id="eefae-209">**前端**：預設會選取一個標準 A1 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-209">**FrontEnd**: By default, one Standard A1 instance is selected.</span></span> <span data-ttu-id="eefae-210">這是建議的 hello 小。</span><span class="sxs-lookup"><span data-stu-id="eefae-210">This is hello minimum we recommend.</span></span> <span data-ttu-id="eefae-211">hello 前端角色負責路由要求 tooApp 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-211">hello FrontEnd role is responsible for routing requests tooApp Service applications.</span></span>
    - <span data-ttu-id="eefae-212">**共用背景工作**： 根據預設，已經選取一個標準 A1 執行個體，但是您可能想 tooadd 更多。</span><span class="sxs-lookup"><span data-stu-id="eefae-212">**Shared Worker**: By default, one Standard A1 instance is selected, but you might want tooadd more.</span></span> <span data-ttu-id="eefae-213">身為系統管理員，您可以定義您的供應項目，並選擇任何 SKU 層。</span><span class="sxs-lookup"><span data-stu-id="eefae-213">As an administrator, you can define your offering and choose any SKU tier.</span></span> <span data-ttu-id="eefae-214">hello 層必須具有至少一個核心。</span><span class="sxs-lookup"><span data-stu-id="eefae-214">hello tiers must have a minimum of one core.</span></span> <span data-ttu-id="eefae-215">hello 共用背景工作角色負責主控 web、 行動裝置，或應用程式開發介面應用程式和 Azure 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-215">hello Shared Worker role is responsible for hosting web, mobile, or API applications and Azure Functions apps.</span></span>

    ![Azure Stack 上的 App Service 角色設定][6]

    > [!NOTE]
    > <span data-ttu-id="eefae-217">Hello technial preview 中 hello 應用程式服務資源提供者安裝程式也會部署標準 A1 執行個體 toooperate 為簡單的檔案伺服器 toosupport Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="eefae-217">In hello technical previews, hello App Service resource provider installer also deploys a Standard A1 instance toooperate as a simple file server toosupport Azure Resource Manager.</span></span> <span data-ttu-id="eefae-218">這會針對單一節點開發套件加以保留。</span><span class="sxs-lookup"><span data-stu-id="eefae-218">This remains for a single-node development kit.</span></span> <span data-ttu-id="eefae-219">對於生產工作負載，在公開上市 hello 應用程式服務安裝程式可讓您 hello 使用高可用性檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="eefae-219">For production workloads, at general availability hello App Service installer enables hello use of a high-availability file server.</span></span>

19. <span data-ttu-id="eefae-220">選擇您的部署**Windows Server 2016**從 hello hello 應用程式服務雲端計算資源提供者中所提供的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="eefae-220">Choose your deployment **Windows Server 2016** VM image from those available in hello compute resource provider for hello App Service cloud.</span></span> <span data-ttu-id="eefae-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-221">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service VM 映像選取項目][7]

20. <span data-ttu-id="eefae-223">Hello hello 雲端應用程式服務中設定的背景工作角色，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-223">Enter a user name and password for hello Worker roles configured in hello App Service cloud.</span></span> <span data-ttu-id="eefae-224">針對所有其他的 App Service 角色，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-224">Enter a user name and password for all other App Service roles.</span></span> <span data-ttu-id="eefae-225">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-225">Click **Next**.</span></span>

    ![Azure Stack 上的 App Service 認證項目][8]

21. <span data-ttu-id="eefae-227">在 hello 摘要畫面中，確認您所做的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="eefae-227">On hello summary screen, verify hello selections you made.</span></span> <span data-ttu-id="eefae-228">toomake 變更 hello 畫面，請返回並修改您的選擇。</span><span class="sxs-lookup"><span data-stu-id="eefae-228">toomake changes, go back through hello screens and modify your selections.</span></span> <span data-ttu-id="eefae-229">如果您要如何 hello 設定，請選取 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-229">If hello configuration is how you want it, select hello check box.</span></span> <span data-ttu-id="eefae-230">toostart hello 部署中，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="eefae-230">toostart hello deployment, click **Next**.</span></span>

    ![Azure Stack 上的 App Service 選取項目摘要][9]

22. <span data-ttu-id="eefae-232">追蹤 hello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="eefae-232">Track hello installation progress.</span></span> <span data-ttu-id="eefae-233">Azure 堆疊上的應用程式服務大約需要約 45 too60 分鐘 toodeploy 根據 hello 預設選取項目。</span><span class="sxs-lookup"><span data-stu-id="eefae-233">App Service on Azure Stack takes about 45 too60 minutes toodeploy based on hello default selections.</span></span>

    ![Azure Stack 上的 App Service 安裝進度][10]

23. <span data-ttu-id="eefae-235">Hello 安裝程式已順利完成之後，請按一下**結束**。</span><span class="sxs-lookup"><span data-stu-id="eefae-235">After hello installer successfully finishes, click **Exit**.</span></span>

## <a name="validate-hello-app-service-on-azure-stack-installation"></a><span data-ttu-id="eefae-236">驗證 Azure 堆疊安裝上的 hello 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="eefae-236">Validate hello App Service on Azure Stack installation</span></span>

1. <span data-ttu-id="eefae-237">在 hello Azure 堆疊管理員入口網站中瀏覽 toohello hello 安裝程式所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="eefae-237">In hello Azure Stack admin portal, browse toohello resource group created by hello installer.</span></span> <span data-ttu-id="eefae-238">根據預設值，此群組是 **APPSERVICE-LOCAL**。</span><span class="sxs-lookup"><span data-stu-id="eefae-238">By default, this group is **APPSERVICE-LOCAL**.</span></span>

2. <span data-ttu-id="eefae-239">找出 **CN0-VM**。</span><span class="sxs-lookup"><span data-stu-id="eefae-239">Locate **CN0-VM**.</span></span> <span data-ttu-id="eefae-240">按一下 tooconnect toohello VM，**連接**hello 上**虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eefae-240">tooconnect toohello VM, click **Connect** on hello **Virtual Machine** blade.</span></span>

3. <span data-ttu-id="eefae-241">在此 vm 的 hello 桌面上，按兩下**網站雲端管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="eefae-241">On hello desktop of this VM, double-click **Web Cloud Management Console**.</span></span>

4. <span data-ttu-id="eefae-242">跳過**管理的伺服器**。</span><span class="sxs-lookup"><span data-stu-id="eefae-242">Go too**Managed Servers**.</span></span>

5. <span data-ttu-id="eefae-243">當所有 hello 機器顯示**準備**一或多個背景工作，請繼續進行 toostep 6。</span><span class="sxs-lookup"><span data-stu-id="eefae-243">When all hello machines display **Ready** for one or more Workers, proceed toostep 6.</span></span>

6. <span data-ttu-id="eefae-244">關閉遠端桌面的電腦 hello，並傳回 toohello hello 應用程式服務安裝程式的執行所在的電腦。</span><span class="sxs-lookup"><span data-stu-id="eefae-244">Close hello remote desktop machine, and return toohello machine where you executed hello App Service installer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eefae-245">您不需要一或多個工作者 toodisplay toowait**準備**toocomplete hello 安裝 Azure 堆疊上的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="eefae-245">You don't need toowait for one or more Workers toodisplay **Ready** toocomplete hello installation of App Service on Azure Stack.</span></span> <span data-ttu-id="eefae-246">不過，您需要至少一個背景工作的準備 toodeploy 行動、 web API 應用程式或 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="eefae-246">However, you need a minimum of one Worker that's ready toodeploy a web, mobile, or API app or Azure Functions.</span></span>

    ![Azure Stack 上的 App Service 受管理伺服器狀態][11]

## <a name="configure-an-azure-ad-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a><span data-ttu-id="eefae-248">設定虛擬機器規模集整合 Azure AD 服務主體上背景工作層和 SSO hello Azure 函式的入口網站和進階開發人員工具</span><span class="sxs-lookup"><span data-stu-id="eefae-248">Configure an Azure AD service principal for virtual machine scale set integration on Worker tiers and SSO for hello Azure Functions portal and advanced developer tools</span></span>

>[!NOTE]
> <span data-ttu-id="eefae-249">這些步驟適用於的 tooAzure AD 保護僅限 Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="eefae-249">These steps apply tooAzure AD secured Azure Stack environments only.</span></span>

<span data-ttu-id="eefae-250">系統管理員需要 tooconfigure SSO 至：</span><span class="sxs-lookup"><span data-stu-id="eefae-250">Administrators need tooconfigure SSO to:</span></span>

* <span data-ttu-id="eefae-251">啟用進階開發人員工具，應用程式服務 (Kudu) 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="eefae-251">Enable hello advanced developer tools within App Service (Kudu).</span></span>
* <span data-ttu-id="eefae-252">啟用 hello hello Azure 函式的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="eefae-252">Enable hello use of hello Azure Functions portal experience.</span></span>

<span data-ttu-id="eefae-253">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="eefae-253">Follow these steps:</span></span>

1. <span data-ttu-id="eefae-254">以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-254">Open a PowerShell instance as azurestack\azurestackadmin.</span></span>

2. <span data-ttu-id="eefae-255">移 hello 指令碼下載並解壓縮在 hello toohello 位置[先決條件步驟](#Download-Required-Components)。</span><span class="sxs-lookup"><span data-stu-id="eefae-255">Go toohello location of hello scripts downloaded and extracted in hello [prerequisite step](#Download-Required-Components).</span></span>

3. <span data-ttu-id="eefae-256">[安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="eefae-256">[Install](azure-stack-powershell-install.md) and [configure an Azure Stack PowerShell environment](azure-stack-powershell-configure-admin.md).</span></span>

4. <span data-ttu-id="eefae-257">在 hello 相同的 PowerShell 工作階段中執行 hello **CreateIdentityApp.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-257">In hello same PowerShell session, run hello **CreateIdentityApp.ps1** script.</span></span> <span data-ttu-id="eefae-258">當系統提示需要您的 Azure AD 租用戶識別碼時，請輸入您使用的 Azure 堆疊部署，例如 myazurestack.onmicrosoft.com hello Azure AD 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-258">When you're prompted for your Azure AD tenant ID, enter hello Azure AD tenant ID you're using for your Azure Stack deployment, for example, myazurestack.onmicrosoft.com.</span></span>

5. <span data-ttu-id="eefae-259">在 hello**認證**視窗中，輸入您的 Azure AD 服務系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-259">In hello **Credential** window, enter your Azure AD service admin account and password.</span></span> <span data-ttu-id="eefae-260">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-260">Click **OK**.</span></span>

6. <span data-ttu-id="eefae-261">輸入 hello hello 憑證檔案的路徑和憑證密碼[稍早建立的憑證](# Create certificates toobe used by App Service on Azure Stack)。</span><span class="sxs-lookup"><span data-stu-id="eefae-261">Enter hello certificate file path and certificate password for hello [certificate created earlier](# Create certificates toobe used by App Service on Azure Stack).</span></span> <span data-ttu-id="eefae-262">針對此步驟建立預設的 hello 憑證是 sso.appservice.local.azurestack.external.pfx。</span><span class="sxs-lookup"><span data-stu-id="eefae-262">hello certificate created for this step by default is sso.appservice.local.azurestack.external.pfx.</span></span>

7. <span data-ttu-id="eefae-263">hello 指令碼在 hello 租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼名為**UpdateConfigOnController.ps1**。</span><span class="sxs-lookup"><span data-stu-id="eefae-263">hello script creates a new application in hello tenant Azure AD and generates a new PowerShell script named **UpdateConfigOnController.ps1**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="eefae-264">請記下 hello**應用程式識別碼**hello PowerShell 輸出中傳回。</span><span class="sxs-lookup"><span data-stu-id="eefae-264">Make note of hello **Application ID** that's returned in hello PowerShell output.</span></span> <span data-ttu-id="eefae-265">您需要此資訊 toosearch 為其步驟 12 中。</span><span class="sxs-lookup"><span data-stu-id="eefae-265">You need this information toosearch for it in step 12.</span></span>

8. <span data-ttu-id="eefae-266">複製 hello 識別應用程式的憑證檔案和 hello 產生指令碼太**CN0 VM**使用遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="eefae-266">Copy hello identity app certificate file and hello generated script too**CN0-VM** by using a remote desktop session.</span></span>

9. <span data-ttu-id="eefae-267">開啟新的瀏覽器視窗，並以登入 toohello Azure 入口網站 (portal.azure.com) hello **Azure Active Directory 服務系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="eefae-267">Open a new browser window, and sign in toohello Azure portal (portal.azure.com) as hello **Azure Active Directory Service Admin**.</span></span>

10. <span data-ttu-id="eefae-268">開啟 hello Azure AD 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="eefae-268">Open hello Azure AD resource provider.</span></span>

11. <span data-ttu-id="eefae-269">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="eefae-269">Click **App Registrations**.</span></span>

12. <span data-ttu-id="eefae-270">搜尋 hello**應用程式識別碼**步驟 7 的一部分傳回。</span><span class="sxs-lookup"><span data-stu-id="eefae-270">Search for hello **Application ID** returned as part of step 7.</span></span> <span data-ttu-id="eefae-271">隨即列出 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-271">An App Service application is listed.</span></span>

13. <span data-ttu-id="eefae-272">按一下**應用程式**hello 清單，並開啟 hello**金鑰**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eefae-272">Click **Application** in hello list, and open hello **Keys** blade.</span></span>

14. <span data-ttu-id="eefae-273">加入新的金鑰與**描述-函式的入口網站**，並設定 hello**到期日**太**永久有效**。</span><span class="sxs-lookup"><span data-stu-id="eefae-273">Add a new key with **Description - Functions Portal**, and set hello **Expiration Date** too**Never Expires**.</span></span>

15. <span data-ttu-id="eefae-274">按一下**儲存**，，然後複製 hello 產生索引鍵。</span><span class="sxs-lookup"><span data-stu-id="eefae-274">Click **Save**, and then copy hello key that was generated.</span></span>

    >[!NOTE]
    > <span data-ttu-id="eefae-275">是確定 toonote 或複製 hello 金鑰時產生。</span><span class="sxs-lookup"><span data-stu-id="eefae-275">Be sure toonote or copy hello key when it's generated.</span></span> <span data-ttu-id="eefae-276">儲存之後，您無法再次檢視，而且您需要 tooregenerate 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="eefae-276">After it's saved, it can't be viewed again, and you need tooregenerate a new key.</span></span>

    ![Azure Stack 上的 App Service 應用程式金鑰][12]

16. <span data-ttu-id="eefae-278">傳回 toohello**應用程式註冊**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="eefae-278">Return toohello **Application Registration** in Azure AD.</span></span>

17. <span data-ttu-id="eefae-279">按一下 [必要權限] > [授與權限] > [是]。</span><span class="sxs-lookup"><span data-stu-id="eefae-279">Click **Required Permissions** > **Grant Permissions** > **Yes**.</span></span>

    ![Azure Stack 上的 App Service SSO 授與][13]

18. <span data-ttu-id="eefae-281">傳回太**CN0 VM**，並開啟 hello**網站雲端管理主控台**一次。</span><span class="sxs-lookup"><span data-stu-id="eefae-281">Return too**CN0-VM**, and open hello **Web Cloud Management Console** once more.</span></span>

19. <span data-ttu-id="eefae-282">選取 hello**設定**節點 hello 左的窗格中，並尋找 hello **ApplicationClientSecret**設定。</span><span class="sxs-lookup"><span data-stu-id="eefae-282">Select hello **Settings** node on hello left pane, and look for hello **ApplicationClientSecret** setting.</span></span>

20. <span data-ttu-id="eefae-283">以滑鼠右鍵按一下並選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="eefae-283">Right-click and select **Edit**.</span></span> <span data-ttu-id="eefae-284">貼在步驟 15，產生的 hello 金鑰，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="eefae-284">Paste hello key generated in step 15, and click **OK**.</span></span>

    ![Azure Stack 上的 App Service 應用程式金鑰][14]

21. <span data-ttu-id="eefae-286">開啟系統管理員的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="eefae-286">Open an administrator PowerShell window.</span></span> <span data-ttu-id="eefae-287">瀏覽 toohello hello 指令碼檔案和憑證，已複製在步驟 7 中的目錄。</span><span class="sxs-lookup"><span data-stu-id="eefae-287">Browse toohello directory where hello script file and certificate were copied in step 7.</span></span>

22. <span data-ttu-id="eefae-288">執行 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="eefae-288">Run hello script file.</span></span> <span data-ttu-id="eefae-289">此指令碼檔案中 hello 應用程式服務在 Azure 堆疊設定輸入 hello 屬性，並起始所有前端及管理角色上的修復操作。</span><span class="sxs-lookup"><span data-stu-id="eefae-289">This script file enters hello properties in hello App Service on Azure Stack configuration and initiates a repair operation on all FrontEnd and Management roles.</span></span>

| <span data-ttu-id="eefae-290">參數</span><span class="sxs-lookup"><span data-stu-id="eefae-290">Parameter</span></span> | <span data-ttu-id="eefae-291">必要/選用</span><span class="sxs-lookup"><span data-stu-id="eefae-291">Required/optional</span></span> | <span data-ttu-id="eefae-292">預設值</span><span class="sxs-lookup"><span data-stu-id="eefae-292">Default value</span></span> | <span data-ttu-id="eefae-293">說明</span><span class="sxs-lookup"><span data-stu-id="eefae-293">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eefae-294">DirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="eefae-294">DirectoryTenantName</span></span> | <span data-ttu-id="eefae-295">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-295">Mandatory</span></span> | <span data-ttu-id="eefae-296">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-296">Null</span></span> | <span data-ttu-id="eefae-297">Azure AD 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-297">Azure AD tenant ID.</span></span> <span data-ttu-id="eefae-298">提供 hello GUID 或字串，例如 myazureaaddirectory.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="eefae-298">Provide hello GUID or string, for example, myazureaaddirectory.onmicrosoft.com</span></span> |
| <span data-ttu-id="eefae-299">TenantAzure Resource ManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="eefae-299">TenantAzure Resource ManagerEndpoint</span></span> | <span data-ttu-id="eefae-300">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-300">Mandatory</span></span> | <span data-ttu-id="eefae-301">management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="eefae-301">management.local.azurestack.external</span></span> | <span data-ttu-id="eefae-302">hello 租用戶 Azure 資源管理員端點</span><span class="sxs-lookup"><span data-stu-id="eefae-302">hello tenant Azure Resource Manager endpoint</span></span> |
| <span data-ttu-id="eefae-303">AzureStackCredential</span><span class="sxs-lookup"><span data-stu-id="eefae-303">AzureStackCredential</span></span> | <span data-ttu-id="eefae-304">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-304">Mandatory</span></span> | <span data-ttu-id="eefae-305">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-305">Null</span></span> | <span data-ttu-id="eefae-306">Azure AD 系統管理員</span><span class="sxs-lookup"><span data-stu-id="eefae-306">Azure AD administrator</span></span> |
| <span data-ttu-id="eefae-307">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="eefae-307">CertificateFilePath</span></span> | <span data-ttu-id="eefae-308">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-308">Mandatory</span></span> | <span data-ttu-id="eefae-309">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-309">Null</span></span> | <span data-ttu-id="eefae-310">路徑 toohello 識別應用程式的憑證檔案先前產生</span><span class="sxs-lookup"><span data-stu-id="eefae-310">Path toohello identity application certificate file generated earlier</span></span> |
| <span data-ttu-id="eefae-311">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="eefae-311">CertificatePassword</span></span> | <span data-ttu-id="eefae-312">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-312">Mandatory</span></span> | <span data-ttu-id="eefae-313">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-313">Null</span></span> | <span data-ttu-id="eefae-314">使用 tooprotect hello 憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="eefae-314">Password used tooprotect hello certificate private key</span></span> |
| <span data-ttu-id="eefae-315">DomainName</span><span class="sxs-lookup"><span data-stu-id="eefae-315">DomainName</span></span> | <span data-ttu-id="eefae-316">必要</span><span class="sxs-lookup"><span data-stu-id="eefae-316">Required</span></span> | <span data-ttu-id="eefae-317">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="eefae-317">local.azurestack.external</span></span> | <span data-ttu-id="eefae-318">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="eefae-318">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="eefae-319">AdfsMachineName</span><span class="sxs-lookup"><span data-stu-id="eefae-319">AdfsMachineName</span></span> | <span data-ttu-id="eefae-320">選用</span><span class="sxs-lookup"><span data-stu-id="eefae-320">Optional</span></span> | <span data-ttu-id="eefae-321">在 Azure AD 部署，但需要在 AD FS 部署的 hello 案例中會忽略。</span><span class="sxs-lookup"><span data-stu-id="eefae-321">Ignore in hello case of Azure AD deployment, but required in AD FS deployment.</span></span> <span data-ttu-id="eefae-322">AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="eefae-322">AD FS machine name, for example, AzS-ADFS01.azurestack.local</span></span> |

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a><span data-ttu-id="eefae-323">設定虛擬機器規模集整合 AD FS 服務主體上背景工作層和 SSO hello Azure 函式的入口網站和進階開發人員工具</span><span class="sxs-lookup"><span data-stu-id="eefae-323">Configure an AD FS service principal for virtual machine scale set integration on Worker tiers and SSO for hello Azure Functions portal and advanced developer tools</span></span>

>[!NOTE]
> <span data-ttu-id="eefae-324">這些步驟適用於的 tooAD FS 保護僅限 Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="eefae-324">These steps apply tooAD FS secured Azure Stack environments only.</span></span>

<span data-ttu-id="eefae-325">系統管理員需要 tooconfigure SSO 至：</span><span class="sxs-lookup"><span data-stu-id="eefae-325">Administrators need tooconfigure SSO to:</span></span>

* <span data-ttu-id="eefae-326">針對背景工作層上的虛擬機器擴展集整合設定服務主體。</span><span class="sxs-lookup"><span data-stu-id="eefae-326">Configure a service principal for virtual machine scale set integration on Worker tiers.</span></span>
* <span data-ttu-id="eefae-327">啟用進階開發人員工具，應用程式服務 (Kudu) 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="eefae-327">Enable hello advanced developer tools within App Service (Kudu).</span></span>
* <span data-ttu-id="eefae-328">啟用 hello hello Azure 函式的入口網站體驗。</span><span class="sxs-lookup"><span data-stu-id="eefae-328">Enable hello use of hello Azure Functions portal experience.</span></span> 

<span data-ttu-id="eefae-329">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="eefae-329">Follow these steps:</span></span>

1. <span data-ttu-id="eefae-330">以 azurestack\azurestackadmin 身分開啟 PowerShell 執行個體。</span><span class="sxs-lookup"><span data-stu-id="eefae-330">Open a PowerShell instance as azurestack\azurestackadmin.</span></span>

2. <span data-ttu-id="eefae-331">移 hello 指令碼下載並解壓縮在 hello toohello 位置[先決條件步驟](#Download-Required-Components)。</span><span class="sxs-lookup"><span data-stu-id="eefae-331">Go toohello location of hello scripts downloaded and extracted in hello [prerequisite step](#Download-Required-Components).</span></span>

3. <span data-ttu-id="eefae-332">[安裝](azure-stack-powershell-install.md)及[設定 Azure Stack PowerShell 環境](azure-stack-powershell-configure-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="eefae-332">[Install](azure-stack-powershell-install.md) and [configure an Azure Stack PowerShell environment](azure-stack-powershell-configure-admin.md).</span></span>

4. <span data-ttu-id="eefae-333">在 hello 相同的 PowerShell 工作階段中執行 hello **CreateIdentityApp.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-333">In hello same PowerShell session, run hello **CreateIdentityApp.ps1** script.</span></span> <span data-ttu-id="eefae-334">當系統提示您提供 Azure AD 租用戶識別碼時，請輸入 **ADFS**。</span><span class="sxs-lookup"><span data-stu-id="eefae-334">When you're prompted for your Azure AD tenant ID, enter **ADFS**.</span></span>

5. <span data-ttu-id="eefae-335">在 hello**認證**視窗中，輸入您的 AD FS 服務系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="eefae-335">In hello **Credential** window, enter your AD FS service admin account and password.</span></span> <span data-ttu-id="eefae-336">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eefae-336">Click **OK**.</span></span>

6. <span data-ttu-id="eefae-337">提供 hello hello 憑證檔案的路徑和憑證密碼[稍早建立的憑證](# Create certificates toobe used by App Service on Azure Stack)。</span><span class="sxs-lookup"><span data-stu-id="eefae-337">Provide hello certificate file path and certificate password for hello [certificate created earlier](# Create certificates toobe used by App Service on Azure Stack).</span></span> <span data-ttu-id="eefae-338">針對此步驟建立預設的 hello 憑證是 sso.appservice.local.azurestack.external.pfx。</span><span class="sxs-lookup"><span data-stu-id="eefae-338">hello certificate created for this step by default is sso.appservice.local.azurestack.external.pfx.</span></span>

7. <span data-ttu-id="eefae-339">hello 指令碼在 hello 租用戶 Azure AD 中建立新的應用程式，並產生新的 PowerShell 指令碼名為**UpdateConfigOnController.ps1**。</span><span class="sxs-lookup"><span data-stu-id="eefae-339">hello script creates a new application in hello tenant Azure AD and generates a new PowerShell script named **UpdateConfigOnController.ps1**.</span></span>

8. <span data-ttu-id="eefae-340">複製 hello 識別應用程式的憑證檔案和 hello 產生指令碼 toohello **CN0 VM**使用遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="eefae-340">Copy hello identity app certificate file and hello generated script toohello **CN0-VM** by using a remote desktop session.</span></span>

9. <span data-ttu-id="eefae-341">傳回太**CN0 VM**。</span><span class="sxs-lookup"><span data-stu-id="eefae-341">Return too**CN0-VM**.</span></span>

10. <span data-ttu-id="eefae-342">開啟系統管理員 PowerShell 視窗，並瀏覽 toohello hello 指令碼檔案和憑證，已複製在步驟 7 中的目錄。</span><span class="sxs-lookup"><span data-stu-id="eefae-342">Open an administrator PowerShell window, and browse toohello directory where hello script file and certificate were copied in step 7.</span></span>

11. <span data-ttu-id="eefae-343">執行 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="eefae-343">Run hello script file.</span></span> <span data-ttu-id="eefae-344">此指令碼檔案中 hello 應用程式服務在 Azure 堆疊設定輸入 hello 屬性，並起始所有前端及管理角色上的修復操作。</span><span class="sxs-lookup"><span data-stu-id="eefae-344">This script file enters hello properties in hello App Service on Azure Stack configuration and initiates a repair operation on all FrontEnd and Management roles.</span></span>

| <span data-ttu-id="eefae-345">參數</span><span class="sxs-lookup"><span data-stu-id="eefae-345">Parameter</span></span> | <span data-ttu-id="eefae-346">必要/選用</span><span class="sxs-lookup"><span data-stu-id="eefae-346">Required/optional</span></span> | <span data-ttu-id="eefae-347">預設值</span><span class="sxs-lookup"><span data-stu-id="eefae-347">Default value</span></span> | <span data-ttu-id="eefae-348">說明</span><span class="sxs-lookup"><span data-stu-id="eefae-348">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eefae-349">DirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="eefae-349">DirectoryTenantName</span></span> | <span data-ttu-id="eefae-350">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-350">Mandatory</span></span> | <span data-ttu-id="eefae-351">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-351">Null</span></span> | <span data-ttu-id="eefae-352">使用**ADFS** hello AD FS 環境</span><span class="sxs-lookup"><span data-stu-id="eefae-352">Use **ADFS** for hello AD FS environment</span></span> |
| <span data-ttu-id="eefae-353">TenantAzure Resource ManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="eefae-353">TenantAzure Resource ManagerEndpoint</span></span> | <span data-ttu-id="eefae-354">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-354">Mandatory</span></span> | <span data-ttu-id="eefae-355">management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="eefae-355">management.local.azurestack.external</span></span> | <span data-ttu-id="eefae-356">hello 租用戶 Azure 資源管理員端點</span><span class="sxs-lookup"><span data-stu-id="eefae-356">hello tenant Azure Resource Manager endpoint</span></span> |
| <span data-ttu-id="eefae-357">AzureStackCredential</span><span class="sxs-lookup"><span data-stu-id="eefae-357">AzureStackCredential</span></span> | <span data-ttu-id="eefae-358">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-358">Mandatory</span></span> | <span data-ttu-id="eefae-359">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-359">Null</span></span> | <span data-ttu-id="eefae-360">hello AD FS 服務系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="eefae-360">hello AD FS service admin account</span></span> |
| <span data-ttu-id="eefae-361">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="eefae-361">CertificateFilePath</span></span> | <span data-ttu-id="eefae-362">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-362">Mandatory</span></span> | <span data-ttu-id="eefae-363">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-363">Null</span></span> | <span data-ttu-id="eefae-364">路徑 toohello 識別應用程式的憑證檔案先前產生</span><span class="sxs-lookup"><span data-stu-id="eefae-364">Path toohello identity application certificate file generated earlier</span></span> |
| <span data-ttu-id="eefae-365">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="eefae-365">CertificatePassword</span></span> | <span data-ttu-id="eefae-366">強制</span><span class="sxs-lookup"><span data-stu-id="eefae-366">Mandatory</span></span> | <span data-ttu-id="eefae-367">Null</span><span class="sxs-lookup"><span data-stu-id="eefae-367">Null</span></span> | <span data-ttu-id="eefae-368">使用 tooprotect hello 憑證私密金鑰的密碼</span><span class="sxs-lookup"><span data-stu-id="eefae-368">Password used tooprotect hello certificate private key</span></span> |
| <span data-ttu-id="eefae-369">DomainName</span><span class="sxs-lookup"><span data-stu-id="eefae-369">DomainName</span></span> | <span data-ttu-id="eefae-370">必要</span><span class="sxs-lookup"><span data-stu-id="eefae-370">Required</span></span> | <span data-ttu-id="eefae-371">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="eefae-371">local.azurestack.external</span></span> | <span data-ttu-id="eefae-372">Azure Stack 區域和網域尾碼</span><span class="sxs-lookup"><span data-stu-id="eefae-372">Azure Stack region and domain suffix</span></span> |
| <span data-ttu-id="eefae-373">AdfsMachineName</span><span class="sxs-lookup"><span data-stu-id="eefae-373">AdfsMachineName</span></span> | <span data-ttu-id="eefae-374">選用</span><span class="sxs-lookup"><span data-stu-id="eefae-374">Optional</span></span> | <span data-ttu-id="eefae-375">AD FS 電腦名稱，例如 AzS-ADFS01.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="eefae-375">AD FS machine name, for example, AzS-ADFS01.azurestack.local</span></span> |

## <a name="test-drive-app-service-on-azure-stack"></a><span data-ttu-id="eefae-376">測試 Azure Stack 上的 App Service</span><span class="sxs-lookup"><span data-stu-id="eefae-376">Test drive App Service on Azure Stack</span></span>

<span data-ttu-id="eefae-377">您部署及註冊 hello 應用程式服務資源提供者之後，測試 toomake 確定租用戶可以將 web、 mobile 及 API 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="eefae-377">After you deploy and register hello App Service resource provider, test it toomake sure that tenants can deploy web, mobile, and API apps.</span></span>

> [!NOTE]
> <span data-ttu-id="eefae-378">您需要 toocreate hello 計劃中的 hello Microsoft.Web 命名空間提供項目。</span><span class="sxs-lookup"><span data-stu-id="eefae-378">You need toocreate an offer that has hello Microsoft.Web namespace within hello plan.</span></span> <span data-ttu-id="eefae-379">然後，您需要 toohave 訂閱 toothis 優惠的租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eefae-379">Then you need toohave a tenant subscription that subscribes toothis offer.</span></span> <span data-ttu-id="eefae-380">如需詳細資訊，請參閱[建立供應項目](azure-stack-create-offer.md)和[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="eefae-380">For more information, see [Create offer](azure-stack-create-offer.md) and [Create plan](azure-stack-create-plan.md).</span></span>
>
<span data-ttu-id="eefae-381">您*必須*有使用 Azure 堆疊上的應用程式服務的租用戶訂用帳戶 toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-381">You *must* have a tenant subscription toocreate applications that use App Service on Azure Stack.</span></span> <span data-ttu-id="eefae-382">服務系統管理員可以完成 hello 系統管理入口網站中的 hello 唯一功能是相關的 toohello 資源提供者管理的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="eefae-382">hello only capabilities that a service admin can complete within hello admin portal are related toohello resource provider administration of App Service.</span></span> <span data-ttu-id="eefae-383">這些功能包括新增容量、設定部署來源，以及新增背景工作層和 SKU。</span><span class="sxs-lookup"><span data-stu-id="eefae-383">These capabilities include adding capacity, configuring deployment sources, and adding Worker tiers and SKUs.</span></span>
>
<span data-ttu-id="eefae-384">為準，hello 第三個技術預覽、 toocreate web、 mobile API 和 Azure 應用程式的功能，您必須使用 hello 租用戶入口網站，並有租用戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eefae-384">As of hello third technical preview, toocreate web, mobile, API, and Azure Functions apps, you must use hello tenant portal and have a tenant subscription.</span></span> 

1. <span data-ttu-id="eefae-385">在 hello Azure 堆疊租用戶入口網站中，按一下 **新增** > **Web + 行動** > **Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="eefae-385">In hello Azure Stack tenant portal, click **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="eefae-386">在 hello **Web 應用程式**刀鋒視窗中，輸入的名稱在 hello **Web 應用程式**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-386">On hello **Web App** blade, type a name in hello **Web app** box.</span></span>

3. <span data-ttu-id="eefae-387">按一下 [資源群組] 下方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="eefae-387">Under **Resource Group**, click **New**.</span></span> <span data-ttu-id="eefae-388">輸入的名稱在 hello**資源群組**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-388">Type a name in hello **Resource Group** box.</span></span>

4. <span data-ttu-id="eefae-389">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="eefae-389">Click **App Service plan/Location** > **Create New**.</span></span>

5. <span data-ttu-id="eefae-390">在 hello **App Service 方案**刀鋒視窗中，輸入的名稱在 hello **App Service 方案**方塊。</span><span class="sxs-lookup"><span data-stu-id="eefae-390">On hello **App Service plan** blade, type a name in hello **App Service plan** box.</span></span>

6. <span data-ttu-id="eefae-391">按一下 [定價層] > [免費 - 共用] 或 [共用 - 共用] > [選取] > [確定] > [建立]。</span><span class="sxs-lookup"><span data-stu-id="eefae-391">Click **Pricing tier** > **Free-Shared** or **Shared-Shared** > **Select** > **OK** > **Create**.</span></span>

7. <span data-ttu-id="eefae-392">在下一分鐘 hello 新 web 應用程式的磚會顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="eefae-392">In under a minute, a tile for hello new web app appears on hello dashboard.</span></span> <span data-ttu-id="eefae-393">按一下 hello 磚。</span><span class="sxs-lookup"><span data-stu-id="eefae-393">Click hello tile.</span></span>

8. <span data-ttu-id="eefae-394">在 hello **Web 應用程式**刀鋒視窗中，按一下 **瀏覽**tooview hello 預設網站，此應用程式。</span><span class="sxs-lookup"><span data-stu-id="eefae-394">On hello **Web App** blade, click **Browse** tooview hello default website for this app.</span></span>

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a><span data-ttu-id="eefae-395">部署 WordPress、DNN 或 Django 網站 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="eefae-395">Deploy a WordPress, DNN, or Django website (optional)</span></span>

1. <span data-ttu-id="eefae-396">在 hello Azure 堆疊租用戶入口網站中，按一下   **+** toohello Azure Marketplace、 部署如 Django 網站，請等待順利完成。</span><span class="sxs-lookup"><span data-stu-id="eefae-396">In hello Azure Stack tenant portal, click **+**, go toohello Azure Marketplace, deploy a Django website, and wait for successful completion.</span></span> <span data-ttu-id="eefae-397">hello Django web 平台會使用檔案系統為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eefae-397">hello Django web platform uses a file system-based database.</span></span> <span data-ttu-id="eefae-398">它不需要任何額外的資源提供者，例如 SQL 或 MySQL。</span><span class="sxs-lookup"><span data-stu-id="eefae-398">It doesn’t require any additional resource providers, such as SQL or MySQL.</span></span>

2. <span data-ttu-id="eefae-399">如果您也會部署 MySQL 資源提供者，您可以部署的 hello Marketplace WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="eefae-399">If you also deployed a MySQL resource provider, you can deploy a WordPress website from hello Marketplace.</span></span> <span data-ttu-id="eefae-400">當系統提示您為資料庫參數時，輸入 hello 使用者名稱做為 *User1@Server1*使用 hello 使用者名稱和您選擇的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="eefae-400">When you're prompted for database parameters, enter hello user name as *User1@Server1*, with hello user name and server name of your choice.</span></span>

3. <span data-ttu-id="eefae-401">如果您也會部署 SQL Server 資源提供者，您可以部署的 hello Marketplace DNN 網站。</span><span class="sxs-lookup"><span data-stu-id="eefae-401">If you also deployed a SQL Server resource provider, you can deploy a DNN website from hello Marketplace.</span></span> <span data-ttu-id="eefae-402">當系統提示您為資料庫參數時，選擇 hello 電腦連線的 tooyour 資源提供者的 SQL server 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eefae-402">When you're prompted for database parameters, choose a database in hello computer running SQL Server that's connected tooyour resource provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eefae-403">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eefae-403">Next steps</span></span>

<span data-ttu-id="eefae-404">您也可以嘗試其他[平台即服務 (PaaS) 服務](azure-stack-tools-paas-services.md)。</span><span class="sxs-lookup"><span data-stu-id="eefae-404">You can also try out other [platform as a service (PaaS) services](azure-stack-tools-paas-services.md).</span></span>

- [<span data-ttu-id="eefae-405">SQL Server 資源提供者</span><span class="sxs-lookup"><span data-stu-id="eefae-405">SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-deploy.md)
- [<span data-ttu-id="eefae-406">MySQL 資源提供者</span><span class="sxs-lookup"><span data-stu-id="eefae-406">MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy/app-service-exe-start.png
[2]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-cloud-configuration.png
[3]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-subscription-location-populated.png
[4]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-resource-group-sql.png
[5]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-certificates.png
[6]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-configuration.png
[7]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-vm-image-selection.png
[8]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-credentials.png
[9]: ./media/azure-stack-app-service-deploy/app-service-exe-selection-summary.png
[10]: ./media/azure-stack-app-service-deploy/app-service-exe-installation-progress.png
[11]: ./media/azure-stack-app-service-deploy/managed-servers.png
[12]: ./media/azure-stack-app-service-deploy/app-service-sso-keys.png
[13]: ./media/azure-stack-app-service-deploy/app-service-sso-grant.png
[14]: ./media/azure-stack-app-service-deploy/app-service-application-secret.png

<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
