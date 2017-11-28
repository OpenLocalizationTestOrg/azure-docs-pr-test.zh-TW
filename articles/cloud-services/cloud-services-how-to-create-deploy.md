---
title: "aaaHow toocreate 及部署雲端服務 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署雲端服務在 Azure 中使用 hello 快速建立 方法。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="bec0c-103">如何 tooCreate 及部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="bec0c-103">How tooCreate and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bec0c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bec0c-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="bec0c-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="bec0c-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="bec0c-106">hello Azure 傳統入口網站提供兩種方式，讓您 toocreate 及部署雲端服務：**快速建立**和**自訂建立**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-106">hello Azure classic portal provides two ways for you toocreate and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="bec0c-107">本主題說明如何 toouse hello 快速建立新的雲端服務的方法 toocreate，然後使用**上傳**tooupload 和部署在 Azure 中的雲端服務封裝。</span><span class="sxs-lookup"><span data-stu-id="bec0c-107">This topic explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="bec0c-108">當您使用這個方法時，hello Azure 傳統入口網站可完成所有需求，您隨時可以使用方便的連結。</span><span class="sxs-lookup"><span data-stu-id="bec0c-108">When you use this method, hello Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="bec0c-109">如果您準備好 toodeploy 您的雲端服務，您在建立時，您可以在 hello 使用**自訂建立**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="bec0c-110">如果您計劃 toopublish 雲端服務從 Visual Studio Team Services (VSTS)，使用**快速建立**，然後再設定從 VSTS 發行**快速入門**或 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="bec0c-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or hello dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="bec0c-111">概念</span><span class="sxs-lookup"><span data-stu-id="bec0c-111">Concepts</span></span>
<span data-ttu-id="bec0c-112">為雲端應用程式服務在 Azure 中的順序 toodeploy 中必須有三個元件：</span><span class="sxs-lookup"><span data-stu-id="bec0c-112">Three components are required in order toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="bec0c-113">**服務定義**</span><span class="sxs-lookup"><span data-stu-id="bec0c-113">**Service Definition**</span></span>  
  <span data-ttu-id="bec0c-114">hello 雲端服務定義檔 (.csdef) 定義 hello 服務模型，包括角色的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="bec0c-114">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="bec0c-115">**服務組態**</span><span class="sxs-lookup"><span data-stu-id="bec0c-115">**Service Configuration**</span></span>  
  <span data-ttu-id="bec0c-116">hello 雲端服務組態檔 (.cscfg) 提供 hello 雲端服務和個別的角色，包括 hello 角色執行個體數目的組態設定。</span><span class="sxs-lookup"><span data-stu-id="bec0c-116">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="bec0c-117">**服務封裝**</span><span class="sxs-lookup"><span data-stu-id="bec0c-117">**Service Package**</span></span>  
  <span data-ttu-id="bec0c-118">hello 服務封裝 (.cspkg) 包含 hello 應用程式程式碼和組態和 hello 服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="bec0c-118">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="bec0c-119">您可以進一步了解這些以及 toocreate 封裝[這裡](cloud-services-model-and-package.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-119">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="bec0c-120">準備您的應用程式</span><span class="sxs-lookup"><span data-stu-id="bec0c-120">Prepare your app</span></span>
<span data-ttu-id="bec0c-121">您可以部署雲端服務之前，您必須建立 hello 雲端服務封裝 (.cspkg)，從應用程式程式碼和雲端服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-121">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="bec0c-122">hello Azure SDK 提供工具來準備這些必要的部署檔案。</span><span class="sxs-lookup"><span data-stu-id="bec0c-122">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="bec0c-123">您可以從 hello 安裝 hello SDK [Azure 下載](https://azure.microsoft.com/downloads/)頁面上，在想 toodevelop hello 語言中應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="bec0c-123">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="bec0c-124">三個雲端服務功能需要特別組態，您才能匯出服務封裝：</span><span class="sxs-lookup"><span data-stu-id="bec0c-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="bec0c-125">如果您想 toodeploy 雲端服務使用安全通訊端層 (SSL) 進行資料加密[設定您的應用程式](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files)ssl。</span><span class="sxs-lookup"><span data-stu-id="bec0c-125">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="bec0c-126">如果您想 tooconfigure 遠端桌面連線 toorole 執行個體，[設定 hello 角色](cloud-services-role-enable-remote-desktop.md)遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="bec0c-126">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="bec0c-127">如果您想 tooconfigure 監視您的雲端服務的詳細資訊，請啟用 Azure 診斷 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-127">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="bec0c-128">*最小監視*（監視層級 hello 預設值） 會使用從 hello 的主機作業系統的角色執行個體 （虛擬機器） 收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="bec0c-128">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="bec0c-129">「 詳細資訊監視 * 會收集內部 hello 角色執行個體 tooenable 進一步分析應用程式處理期間發生的問題的效能資料為基礎的其他度量。</span><span class="sxs-lookup"><span data-stu-id="bec0c-129">"Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="bec0c-130">toofind 出 tooenable Azure 診斷，請參閱[在 Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-130">toofind out how tooenable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="bec0c-131">toocreate 具有 web 角色或背景工作角色部署的雲端服務，您必須[建立 hello 服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-131">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bec0c-132">開始之前</span><span class="sxs-lookup"><span data-stu-id="bec0c-132">Before you begin</span></span>
* <span data-ttu-id="bec0c-133">如果您尚未安裝 hello Azure SDK，請按一下**安裝 Azure SDK** tooopen hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後下載 hello SDK hello 慣用 toodevelop 您的程式碼的語言。</span><span class="sxs-lookup"><span data-stu-id="bec0c-133">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="bec0c-134">(您將有機會 toodo this 更新版本。)</span><span class="sxs-lookup"><span data-stu-id="bec0c-134">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="bec0c-135">如果任何角色執行個體需要憑證，請建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="bec0c-135">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="bec0c-136">雲端服務需要含有私密金鑰的 .pfx 檔。</span><span class="sxs-lookup"><span data-stu-id="bec0c-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="bec0c-137">您可以[上載 hello 憑證 tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate)當您建立並部署 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-137">You can [upload hello certificates tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy hello cloud service.</span></span>
* <span data-ttu-id="bec0c-138">如果您計劃 toodeploy hello 雲端服務 tooan 同質群組，建立 hello 同質群組。</span><span class="sxs-lookup"><span data-stu-id="bec0c-138">If you plan toodeploy hello cloud service tooan affinity group, create hello affinity group.</span></span> <span data-ttu-id="bec0c-139">您可以使用同質群組 toodeploy，您的雲端服務和其他 Azure 服務 toohello 相同區域中的位置。</span><span class="sxs-lookup"><span data-stu-id="bec0c-139">You can use an affinity group toodeploy your cloud service and other Azure services toohello same location in a region.</span></span> <span data-ttu-id="bec0c-140">您可以建立 hello hello 同質群組**網路**hello Azure 傳統入口網站，在 [hello] 區域**同質群組**頁面。</span><span class="sxs-lookup"><span data-stu-id="bec0c-140">You can create hello affinity group in hello **Networks** area of hello Azure classic portal, on hello **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="bec0c-141">作法：使用「快速建立」建立雲端服務</span><span class="sxs-lookup"><span data-stu-id="bec0c-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="bec0c-142">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **新增**>**計算**>**雲端服務**>**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-142">In hello [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="bec0c-144">在**URL**，輸入子網域名稱 toouse hello 公用 URL 中用來存取您在生產部署中的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-144">In **URL**, enter a subdomain name toouse in hello public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="bec0c-145">生產部署的 hello URL 格式如下： http://*myURL*。.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="bec0c-145">hello URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="bec0c-146">在**地區或同質群組**，選取 hello 地理區域或同質群組 toodeploy hello 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-146">In **Region or Affinity Group**, select hello geographic region or affinity group toodeploy hello cloud service to.</span></span> <span data-ttu-id="bec0c-147">如果您想要 toodeploy 您雲端服務 toohello 選取同質群組與區域內的其他 Azure 服務相同的位置。</span><span class="sxs-lookup"><span data-stu-id="bec0c-147">Select an affinity group if you want toodeploy your cloud service toohello same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="bec0c-148">按一下 [建立雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="bec0c-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="bec0c-150">您可以監視 hello hello 訊息區域底部 hello hello 視窗中的 hello 程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="bec0c-150">You can monitor hello status of hello process in hello message area at hello bottom of hello window.</span></span>
   
    <span data-ttu-id="bec0c-151">hello**雲端服務**區域隨即開啟，與 hello 顯示新雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-151">hello **Cloud Services** area opens, with hello new cloud service displayed.</span></span> <span data-ttu-id="bec0c-152">當 hello 狀態變更時 tooCreated 時，建立雲端服務已順利完成。</span><span class="sxs-lookup"><span data-stu-id="bec0c-152">When hello status changes tooCreated, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="bec0c-154">作法：上傳雲端服務的憑證</span><span class="sxs-lookup"><span data-stu-id="bec0c-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="bec0c-155">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**憑證**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-155">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click hello name of hello cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="bec0c-157">按一下 [上傳憑證] 或 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="bec0c-158">在**檔案**，使用**瀏覽**tooselect hello 憑證 （.pfx 檔案）。</span><span class="sxs-lookup"><span data-stu-id="bec0c-158">In **File**, use **Browse** tooselect hello certificate (.pfx file).</span></span>
4. <span data-ttu-id="bec0c-159">在**密碼**，輸入 hello hello 憑證私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="bec0c-159">In **Password**, enter hello private key for hello certificate.</span></span>
5. <span data-ttu-id="bec0c-160">按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="bec0c-162">您可以觀賞 hello 進度 hello 上傳中 hello 訊息區域，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bec0c-162">You can watch hello progress of hello upload in hello message area, shown below.</span></span> <span data-ttu-id="bec0c-163">Hello 上傳完成時，hello 憑證會新增 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="bec0c-163">When hello upload completes, hello certificate is added toohello table.</span></span> <span data-ttu-id="bec0c-164">Hello 訊息區域中，按一下 [確定] tooclose hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="bec0c-164">In hello message area, click OK tooclose hello message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="bec0c-166">作法：部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="bec0c-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="bec0c-167">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**，按一下 hello hello 雲端服務名稱，然後按一下**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-167">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click hello name of hello cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="bec0c-168">按一下 [上傳新的生產部署] 或 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="bec0c-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="bec0c-169">在**部署標籤**，輸入 hello 新部署，例如 MyCloudServicev4 的名稱。</span><span class="sxs-lookup"><span data-stu-id="bec0c-169">In **Deployment label**, enter a name for hello new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="bec0c-170">在**封裝**，使用**瀏覽**tooselect hello 服務封裝檔 (.cspkg) toouse。</span><span class="sxs-lookup"><span data-stu-id="bec0c-170">In **Package**, use **Browse** tooselect hello service package file (.cspkg) toouse.</span></span>
5. <span data-ttu-id="bec0c-171">在**組態**，使用**瀏覽**tooselect hello 服務設定檔 (.cscfg) toouse。</span><span class="sxs-lookup"><span data-stu-id="bec0c-171">In **Configuration**, use **Browse** tooselect hello service configure file (.cscfg) toouse.</span></span>
6. <span data-ttu-id="bec0c-172">如果只有一個執行個體包含的任何角色 hello 雲端服務，選取 hello**即使一個或多個角色包含單一執行個體部署**核取方塊 tooenable hello 部署 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="bec0c-172">If hello cloud service will include any roles with only one instance, select hello **Deploy even if one or more roles contain a single instance** check box tooenable hello deployment tooproceed.</span></span>
   
    <span data-ttu-id="bec0c-173">如果每個角色都有至少兩個執行個體 azure 只可以在維護和服務更新期間保證 99.95%存取 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-173">Azure can only guarantee 99.95 percent access toohello cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="bec0c-174">如有需要您可以加入其他角色執行個體上 hello**標尺**頁面之後 hello 雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="bec0c-174">If needed, you can add additional role instances on hello **Scale** page after you deploy hello cloud service.</span></span> <span data-ttu-id="bec0c-175">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="bec0c-176">按一下**確定**（勾選記號） toobegin hello 雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="bec0c-176">Click **OK** (checkmark) toobegin hello cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="bec0c-178">您可以監視 hello hello 訊息區域中的 hello 部署狀態。</span><span class="sxs-lookup"><span data-stu-id="bec0c-178">You can monitor hello status of hello deployment in hello message area.</span></span> <span data-ttu-id="bec0c-179">按一下 [確定] toohide hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="bec0c-179">Click OK toohide hello message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="bec0c-181">確認部署是否成功完成</span><span class="sxs-lookup"><span data-stu-id="bec0c-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="bec0c-182">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="bec0c-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="bec0c-183">hello 狀態應顯示 hello 服務是**執行**。</span><span class="sxs-lookup"><span data-stu-id="bec0c-183">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="bec0c-184">在下**快速概覽**，按一下 hello 站台 URL tooopen 您網頁瀏覽器中的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bec0c-184">Under **quick glance**, click hello site URL tooopen your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="bec0c-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bec0c-186">Next steps</span></span>
* <span data-ttu-id="bec0c-187">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="bec0c-188">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="bec0c-189">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="bec0c-190">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="bec0c-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

