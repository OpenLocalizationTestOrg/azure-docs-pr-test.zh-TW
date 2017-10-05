---
title: "如何建立和部署雲端服務 | Microsoft Docs"
description: "了解如何在 Azure 中使用「快速建立」方法來建立和部署雲端服務。"
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
ms.openlocfilehash: 2a2172a78bfd3ac923edbc9de366b035629dd27b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="b5366-103">如何建立和部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="b5366-103">How to Create and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b5366-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b5366-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="b5366-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b5366-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="b5366-106">Azure 傳統入口網站提供兩種方法讓您建立和部署雲端服務：**快速建立**和**自訂建立**。</span><span class="sxs-lookup"><span data-stu-id="b5366-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="b5366-107">本主題說明如何使用「快速建立」方法建立新的雲端服務，然後使用 [上傳] 來上傳雲端服務封裝並在 Azure 中加以部署。</span><span class="sxs-lookup"><span data-stu-id="b5366-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="b5366-108">當您使用這個方法時，Azure 傳統入口網站會在過程中提供便利的連結，讓您完成所有要求。</span><span class="sxs-lookup"><span data-stu-id="b5366-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="b5366-109">如果您準備在建立雲端服務時加以部署，可以同時使用 [自訂建立] 進行這兩項作業。</span><span class="sxs-lookup"><span data-stu-id="b5366-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="b5366-110">如果您計劃從 Visual Studio Team Services (VSTS) 發佈您的雲端服務，請使用 [快速建立]，然後從 [快速啟動] 或儀表板設定 VSTS 發佈。</span><span class="sxs-lookup"><span data-stu-id="b5366-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or the dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="b5366-111">概念</span><span class="sxs-lookup"><span data-stu-id="b5366-111">Concepts</span></span>
<span data-ttu-id="b5366-112">需要三個元件才能部署應用程式成為 Azure 中的雲端服務：</span><span class="sxs-lookup"><span data-stu-id="b5366-112">Three components are required in order to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="b5366-113">**服務定義**</span><span class="sxs-lookup"><span data-stu-id="b5366-113">**Service Definition**</span></span>  
  <span data-ttu-id="b5366-114">雲端服務定義檔 (.csdef) 定義服務模型，包括角色數目。</span><span class="sxs-lookup"><span data-stu-id="b5366-114">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="b5366-115">**服務組態**</span><span class="sxs-lookup"><span data-stu-id="b5366-115">**Service Configuration**</span></span>  
  <span data-ttu-id="b5366-116">雲端服務組態檔 (.cscfg) 提供雲端服務和個別角色的組態設定，包括角色執行個體數。</span><span class="sxs-lookup"><span data-stu-id="b5366-116">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="b5366-117">**服務封裝**</span><span class="sxs-lookup"><span data-stu-id="b5366-117">**Service Package**</span></span>  
  <span data-ttu-id="b5366-118">服務封裝 (.cspkg) 包含應用程式程式碼和組態以及服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="b5366-118">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="b5366-119">您可以在 [這裡](cloud-services-model-and-package.md)深入了解這些內容，以及如何建立封裝。</span><span class="sxs-lookup"><span data-stu-id="b5366-119">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="b5366-120">準備您的應用程式</span><span class="sxs-lookup"><span data-stu-id="b5366-120">Prepare your app</span></span>
<span data-ttu-id="b5366-121">您部署雲端服務之前，必須先從應用程式程式碼和雲端服務組態檔 (.cscfg) 建立雲端服務封裝 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="b5366-121">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="b5366-122">Azure SDK 提供準備這些必要部署檔案的工具。</span><span class="sxs-lookup"><span data-stu-id="b5366-122">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="b5366-123">您可以從 [Azure 下載](https://azure.microsoft.com/downloads/) 頁面安裝 SDK，使用您偏好的語言開發應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="b5366-123">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="b5366-124">三個雲端服務功能需要特別組態，您才能匯出服務封裝：</span><span class="sxs-lookup"><span data-stu-id="b5366-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="b5366-125">如果您要部署使用安全通訊端層 (SSL) 進行資料加密的雲端服務，請針對 SSL [設定應用程式](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) 。</span><span class="sxs-lookup"><span data-stu-id="b5366-125">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="b5366-126">如果您要設定角色執行個體的遠端桌面連線，請 [設定遠端桌面的角色](cloud-services-role-enable-remote-desktop.md) 。</span><span class="sxs-lookup"><span data-stu-id="b5366-126">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="b5366-127">如果您要設定雲端服務的詳細資訊監視，請啟用雲端服務的 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="b5366-127">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="b5366-128">*最小監視* (預設監視層級) 使用從角色執行個體 (虛擬機器) 的主機作業系統收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="b5366-128">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="b5366-129">「詳細資訊監視」會按照角色執行個體內的效能資料收集其他度量，以便進一步分析應用程式處理期間發生的問題。</span><span class="sxs-lookup"><span data-stu-id="b5366-129">"Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="b5366-130">若要了解如何啟用 Azure 診斷，請參閱 [啟用 Azure 診斷](cloud-services-dotnet-diagnostics.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="b5366-130">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="b5366-131">若要使用 Web 角色或背景工作角色的部署來建立雲端服務，您必須 [建立服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。</span><span class="sxs-lookup"><span data-stu-id="b5366-131">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b5366-132">開始之前</span><span class="sxs-lookup"><span data-stu-id="b5366-132">Before you begin</span></span>
* <span data-ttu-id="b5366-133">如果您尚未安裝 Azure SDK，請按一下 [安裝 Azure SDK] 開啟 [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後依照您偏好使用的程式碼開發語言下載 SDK。</span><span class="sxs-lookup"><span data-stu-id="b5366-133">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="b5366-134">(您稍後將有機會這麼做。)</span><span class="sxs-lookup"><span data-stu-id="b5366-134">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="b5366-135">如果任何角色執行個體需要憑證，請建立憑證。</span><span class="sxs-lookup"><span data-stu-id="b5366-135">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="b5366-136">雲端服務需要含有私密金鑰的 .pfx 檔。</span><span class="sxs-lookup"><span data-stu-id="b5366-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="b5366-137">您建立並部署雲端服務時，可以 [將憑證上傳至 Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 。</span><span class="sxs-lookup"><span data-stu-id="b5366-137">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="b5366-138">如果您計劃將雲端服務部署至同質群組，請建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="b5366-138">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="b5366-139">您可以使用同質群組，將雲端服務和其他 Azure 服務部署到區域中的同一個位置。</span><span class="sxs-lookup"><span data-stu-id="b5366-139">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="b5366-140">在 Azure 傳統入口網站的 [網路] 區域中，您可以在 [同質群組] 頁面上建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="b5366-140">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="b5366-141">作法：使用「快速建立」建立雲端服務</span><span class="sxs-lookup"><span data-stu-id="b5366-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="b5366-142">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [新增]>[計算]>[雲端服務]>[快速建立]。</span><span class="sxs-lookup"><span data-stu-id="b5366-142">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="b5366-144">在 [URL] 中，輸入要在公用 URI 中使用的子網域名稱，以存取生產部署中的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b5366-144">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="b5366-145">生產部署的 URL 格式是：http://*myURL*.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="b5366-145">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="b5366-146">在 [區域] 或 [同質群組] 中，選取要將雲端服務部署到其中的地理區域或同質群組。</span><span class="sxs-lookup"><span data-stu-id="b5366-146">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span></span> <span data-ttu-id="b5366-147">如果您要將雲端服務部署到區域中其他 Azure 服務所在的同一個位置，請選取同質群組。</span><span class="sxs-lookup"><span data-stu-id="b5366-147">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="b5366-148">按一下 [建立雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="b5366-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="b5366-150">您可以在視窗底端的訊息區域監視程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5366-150">You can monitor the status of the process in the message area at the bottom of the window.</span></span>
   
    <span data-ttu-id="b5366-151">[雲端服務]  區域隨即開啟，其中顯示新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b5366-151">The **Cloud Services** area opens, with the new cloud service displayed.</span></span> <span data-ttu-id="b5366-152">狀態變更為 [已建立] 時，表示雲端服務建立成功完成。</span><span class="sxs-lookup"><span data-stu-id="b5366-152">When the status changes to Created, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="b5366-154">作法：上傳雲端服務的憑證</span><span class="sxs-lookup"><span data-stu-id="b5366-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="b5366-155">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，依序按一下 [雲端服務]、雲端服務的名稱及 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="b5366-155">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="b5366-157">按一下 [上傳憑證] 或 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="b5366-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="b5366-158">在 [檔案] 中，使用 [瀏覽] 選取憑證 (.pfx 檔)。</span><span class="sxs-lookup"><span data-stu-id="b5366-158">In **File**, use **Browse** to select the certificate (.pfx file).</span></span>
4. <span data-ttu-id="b5366-159">在 [密碼] 中，輸入憑證的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5366-159">In **Password**, enter the private key for the certificate.</span></span>
5. <span data-ttu-id="b5366-160">按一下 [確定]  \(勾選記號)。</span><span class="sxs-lookup"><span data-stu-id="b5366-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="b5366-162">您可以在訊息區域查看上傳的進度，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b5366-162">You can watch the progress of the upload in the message area, shown below.</span></span> <span data-ttu-id="b5366-163">上傳完成時，憑證將新增至資料表中。</span><span class="sxs-lookup"><span data-stu-id="b5366-163">When the upload completes, the certificate is added to the table.</span></span> <span data-ttu-id="b5366-164">在訊息區域中，按一下 [確定] 關閉訊息。</span><span class="sxs-lookup"><span data-stu-id="b5366-164">In the message area, click OK to close the message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="b5366-166">作法：部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="b5366-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="b5366-167">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，依序按一下 [雲端服務]、雲端服務的名稱及 [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="b5366-167">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="b5366-168">按一下 [上傳新的生產部署] 或 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="b5366-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="b5366-169">在 [部署標籤] 中，輸入新部署的名稱，例如，MyCloudServicev4。</span><span class="sxs-lookup"><span data-stu-id="b5366-169">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="b5366-170">在 [封裝] 中，使用 [瀏覽] 選取要使用的服務封裝檔 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="b5366-170">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span></span>
5. <span data-ttu-id="b5366-171">在 [組態] 中，使用 [瀏覽] 選取要使用的服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="b5366-171">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span></span>
6. <span data-ttu-id="b5366-172">如果雲端服務將包含只有一個執行個體的任何角色，請選取 [Deploy even if one or more roles contain a single instance]  核取方塊，讓部署繼續進行。</span><span class="sxs-lookup"><span data-stu-id="b5366-172">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span></span>
   
    <span data-ttu-id="b5366-173">如果每個角色至少有兩個執行個體，Azure 只能保證在維護和服務更新期間存取雲端服務的成功率為 99.95%。</span><span class="sxs-lookup"><span data-stu-id="b5366-173">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="b5366-174">若有需要，您可以在部署雲端服務後，在 [Scale]  頁面上新增其他角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="b5366-174">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span></span> <span data-ttu-id="b5366-175">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="b5366-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="b5366-176">按一下 [確定]  \(核取記號) 開始雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="b5366-176">Click **OK** (checkmark) to begin the cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="b5366-178">您可以在訊息區域監視部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="b5366-178">You can monitor the status of the deployment in the message area.</span></span> <span data-ttu-id="b5366-179">按一下 [確定] 以隱藏訊息。</span><span class="sxs-lookup"><span data-stu-id="b5366-179">Click OK to hide the message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="b5366-181">確認部署是否成功完成</span><span class="sxs-lookup"><span data-stu-id="b5366-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="b5366-182">按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="b5366-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="b5366-183">狀態應該會顯示服務為 [正在執行] 。</span><span class="sxs-lookup"><span data-stu-id="b5366-183">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="b5366-184">在 [quick glance] 下，按一下網站 URL，在網頁瀏覽器中開啟您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b5366-184">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="b5366-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5366-186">Next steps</span></span>
* <span data-ttu-id="b5366-187">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="b5366-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="b5366-188">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="b5366-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="b5366-189">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="b5366-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="b5366-190">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="b5366-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

