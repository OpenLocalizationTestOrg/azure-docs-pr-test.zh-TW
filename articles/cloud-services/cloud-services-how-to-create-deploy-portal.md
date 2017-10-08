---
title: "aaaHow toocreate 及部署雲端服務 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署雲端服務使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="63246-103">如何 toocreate 及部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="63246-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="63246-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="63246-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="63246-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="63246-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="63246-106">hello Azure 入口網站提供兩種方式，讓您 toocreate 及部署雲端服務：*快速建立*和*自訂建立*。</span><span class="sxs-lookup"><span data-stu-id="63246-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="63246-107">這篇文章說明如何 toouse hello 快速建立新的雲端服務的方法 toocreate，然後使用**上傳**tooupload 和部署在 Azure 中的雲端服務封裝。</span><span class="sxs-lookup"><span data-stu-id="63246-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="63246-108">當您使用這個方法時，hello Azure 入口網站可完成所有需求，您隨時可以使用方便的連結。</span><span class="sxs-lookup"><span data-stu-id="63246-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="63246-109">如果您準備好 toodeploy 您的雲端服務，您在建立時，您可以在 hello 同時使用自訂建立。</span><span class="sxs-lookup"><span data-stu-id="63246-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="63246-110">如果您計劃 toopublish 雲端服務從 Visual Studio Team Services (VSTS)，使用 快速建立，，然後設定 VSTS 發行從 hello Azure 快速入門 」 或 「 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="63246-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="63246-111">如需詳細資訊，請參閱[所使用 Visual Studio Team Services 的持續傳遞 tooAzure][TFSTutorialForCloudService]，或 hello 的說明，請參閱**快速入門**頁面。</span><span class="sxs-lookup"><span data-stu-id="63246-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="63246-112">概念</span><span class="sxs-lookup"><span data-stu-id="63246-112">Concepts</span></span>
<span data-ttu-id="63246-113">三個元件為必要的 toodeploy 為 Azure 中雲端服務的應用程式：</span><span class="sxs-lookup"><span data-stu-id="63246-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="63246-114">**服務定義**</span><span class="sxs-lookup"><span data-stu-id="63246-114">**Service Definition**</span></span>  
  <span data-ttu-id="63246-115">hello 雲端服務定義檔 (.csdef) 定義 hello 服務模型，包括角色的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="63246-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="63246-116">**服務組態**</span><span class="sxs-lookup"><span data-stu-id="63246-116">**Service Configuration**</span></span>  
  <span data-ttu-id="63246-117">hello 雲端服務組態檔 (.cscfg) 提供 hello 雲端服務和個別的角色，包括 hello 角色執行個體數目的組態設定。</span><span class="sxs-lookup"><span data-stu-id="63246-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="63246-118">**服務封裝**</span><span class="sxs-lookup"><span data-stu-id="63246-118">**Service Package**</span></span>  
  <span data-ttu-id="63246-119">hello 服務封裝 (.cspkg) 包含 hello 應用程式程式碼和組態和 hello 服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="63246-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="63246-120">您可以進一步了解這些以及 toocreate 封裝[這裡](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="63246-121">準備您的應用程式</span><span class="sxs-lookup"><span data-stu-id="63246-121">Prepare your app</span></span>
<span data-ttu-id="63246-122">您可以部署雲端服務之前，您必須建立 hello 雲端服務封裝 (.cspkg)，從應用程式程式碼和雲端服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="63246-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="63246-123">hello Azure SDK 提供工具來準備這些必要的部署檔案。</span><span class="sxs-lookup"><span data-stu-id="63246-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="63246-124">您可以從 hello 安裝 hello SDK [Azure 下載](https://azure.microsoft.com/downloads/)頁面上，在想 toodevelop hello 語言中應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="63246-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="63246-125">三個雲端服務功能需要特別組態，您才能匯出服務封裝：</span><span class="sxs-lookup"><span data-stu-id="63246-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="63246-126">如果您想 toodeploy 雲端服務使用安全通訊端層 (SSL) 進行資料加密[設定您的應用程式](cloud-services-configure-ssl-certificate-portal.md#modify)ssl。</span><span class="sxs-lookup"><span data-stu-id="63246-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="63246-127">如果您想 tooconfigure 遠端桌面連線 toorole 執行個體，[設定 hello 角色](cloud-services-role-enable-remote-desktop-new-portal.md)遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="63246-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="63246-128">如果您想 tooconfigure 監視您的雲端服務的詳細資訊，請啟用 Azure 診斷 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="63246-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="63246-129">*最小監視*（監視層級 hello 預設值） 會使用從 hello 的主機作業系統的角色執行個體 （虛擬機器） 收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="63246-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="63246-130">*詳細資訊監視*收集 hello 角色執行個體 tooenable 進一步分析的應用程式處理期間發生的問題中的效能資料為基礎的其他度量。</span><span class="sxs-lookup"><span data-stu-id="63246-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="63246-131">toofind 出 tooenable Azure 診斷，請參閱[在 Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="63246-132">toocreate 具有 web 角色或背景工作角色部署的雲端服務，您必須[建立 hello 服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。</span><span class="sxs-lookup"><span data-stu-id="63246-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="63246-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="63246-133">Before you begin</span></span>
* <span data-ttu-id="63246-134">如果您尚未安裝 hello Azure SDK，請按一下**安裝 Azure SDK** tooopen hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後下載 hello SDK hello 慣用 toodevelop 您的程式碼的語言。</span><span class="sxs-lookup"><span data-stu-id="63246-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="63246-135">(您將有機會 toodo this 更新版本。)</span><span class="sxs-lookup"><span data-stu-id="63246-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="63246-136">如果任何角色執行個體需要憑證，請建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="63246-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="63246-137">雲端服務需要含有私密金鑰的 .pfx 檔。</span><span class="sxs-lookup"><span data-stu-id="63246-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="63246-138">當您建立並部署 hello 雲端服務，您可以上傳 hello 憑證 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="63246-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="63246-139">建立和部署</span><span class="sxs-lookup"><span data-stu-id="63246-139">Create and deploy</span></span>
1. <span data-ttu-id="63246-140">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="63246-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="63246-141">按一下**新增 > 計算**，然後向下 tooand 按一下捲動**雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="63246-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="63246-143">在新的 hello**雲端服務**刀鋒視窗中，輸入的值為 hello **DNS 名稱**。</span><span class="sxs-lookup"><span data-stu-id="63246-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="63246-144">建立新的 [資源群組]  或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="63246-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="63246-145">選取 [位置] 。</span><span class="sxs-lookup"><span data-stu-id="63246-145">Select a **Location**.</span></span>
6. <span data-ttu-id="63246-146">按一下 [封裝] 。</span><span class="sxs-lookup"><span data-stu-id="63246-146">Click **Package**.</span></span> <span data-ttu-id="63246-147">這會開啟 hello**將套件上傳**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63246-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="63246-148">填寫 hello 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="63246-148">Fill in hello required fields.</span></span> <span data-ttu-id="63246-149">如果您的任一個角色包含單一執行個體，請確定核取 [即使一個或多個角色包含單一執行個體，也要部署]  。</span><span class="sxs-lookup"><span data-stu-id="63246-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="63246-150">請確定已選取 [開始部署]  。</span><span class="sxs-lookup"><span data-stu-id="63246-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="63246-151">按一下**確定**以關閉 hello**將套件上傳**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63246-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="63246-152">如果您沒有任何憑證 tooadd，按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="63246-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="63246-154">上傳憑證</span><span class="sxs-lookup"><span data-stu-id="63246-154">Upload a certificate</span></span>
<span data-ttu-id="63246-155">如果您的部署套件[設定 toouse 憑證](cloud-services-configure-ssl-certificate-portal.md#modify)，您現在可以上傳 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="63246-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="63246-156">選取**憑證**，在 hello**將憑證加入**刀鋒視窗中，選取 hello SSL 憑證.pfx 檔案，然後再提供 hello**密碼**hello 憑證</span><span class="sxs-lookup"><span data-stu-id="63246-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="63246-157">按一下**附加憑證**，然後按一下**確定**上 hello**將憑證加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63246-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="63246-158">按一下**建立**上 hello**雲端服務**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63246-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="63246-159">當 hello 部署已達到 hello**準備**狀態，您可以繼續 toohello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="63246-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="63246-161">確認部署是否成功完成</span><span class="sxs-lookup"><span data-stu-id="63246-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="63246-162">按一下 hello 雲端服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="63246-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="63246-163">hello 狀態應顯示 hello 服務是**執行**。</span><span class="sxs-lookup"><span data-stu-id="63246-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="63246-164">在下**Essentials**，按一下 hello**網站 URL** tooopen 您的雲端服務 web 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="63246-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="63246-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63246-166">Next steps</span></span>
* <span data-ttu-id="63246-167">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="63246-168">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="63246-169">[管理您的雲端服務](cloud-services-how-to-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="63246-170">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="63246-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
