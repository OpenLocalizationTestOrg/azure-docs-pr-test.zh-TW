---
title: "如何建立和部署雲端服務 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站建立和部署雲端服務。"
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
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="d6521-103">如何建立和部署雲端服務</span><span class="sxs-lookup"><span data-stu-id="d6521-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d6521-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d6521-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="d6521-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="d6521-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="d6521-106">Azure 入口網站提供兩種方法讓您建立和部署雲端服務：「快速建立」和「自訂建立」。</span><span class="sxs-lookup"><span data-stu-id="d6521-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="d6521-107">本主題說明如何使用「快速建立」方法建立新的雲端服務，然後使用 [上傳]  上傳雲端服務封裝並在 Azure 中部署。</span><span class="sxs-lookup"><span data-stu-id="d6521-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="d6521-108">當您使用這個方法時，Azure 入口網站會在過程中提供便利的連結，讓您完成所有要求。</span><span class="sxs-lookup"><span data-stu-id="d6521-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="d6521-109">如果您準備在建立雲端服務時加以部署，可以同時使用 [自訂建立] 進行這兩項作業。</span><span class="sxs-lookup"><span data-stu-id="d6521-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="d6521-110">如果您計劃從 Visual Studio Team Services (VSTS) 發佈您的雲端服務，請使用快速建立，然後從 Azure 快速入門或儀表板設定 VSTS 發佈。</span><span class="sxs-lookup"><span data-stu-id="d6521-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="d6521-111">如需詳細資訊，請參閱[使用 Visual Studio Team Services 連續傳遞至 Azure][TFSTutorialForCloudService]，或參閱 [快速入門] 頁面的說明。</span><span class="sxs-lookup"><span data-stu-id="d6521-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="d6521-112">概念</span><span class="sxs-lookup"><span data-stu-id="d6521-112">Concepts</span></span>
<span data-ttu-id="d6521-113">需要三個元件才能部署應用程式成為 Azure 中的雲端服務：</span><span class="sxs-lookup"><span data-stu-id="d6521-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="d6521-114">**服務定義**</span><span class="sxs-lookup"><span data-stu-id="d6521-114">**Service Definition**</span></span>  
  <span data-ttu-id="d6521-115">雲端服務定義檔 (.csdef) 定義服務模型，包括角色數目。</span><span class="sxs-lookup"><span data-stu-id="d6521-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="d6521-116">**服務組態**</span><span class="sxs-lookup"><span data-stu-id="d6521-116">**Service Configuration**</span></span>  
  <span data-ttu-id="d6521-117">雲端服務組態檔 (.cscfg) 提供雲端服務和個別角色的組態設定，包括角色執行個體數。</span><span class="sxs-lookup"><span data-stu-id="d6521-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="d6521-118">**服務封裝**</span><span class="sxs-lookup"><span data-stu-id="d6521-118">**Service Package**</span></span>  
  <span data-ttu-id="d6521-119">服務封裝 (.cspkg) 包含應用程式程式碼和組態以及服務定義檔。</span><span class="sxs-lookup"><span data-stu-id="d6521-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="d6521-120">您可以在 [這裡](cloud-services-model-and-package.md)深入了解這些內容，以及如何建立封裝。</span><span class="sxs-lookup"><span data-stu-id="d6521-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="d6521-121">準備您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6521-121">Prepare your app</span></span>
<span data-ttu-id="d6521-122">您部署雲端服務之前，必須先從應用程式程式碼和雲端服務組態檔 (.cscfg) 建立雲端服務封裝 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="d6521-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="d6521-123">Azure SDK 提供準備這些必要部署檔案的工具。</span><span class="sxs-lookup"><span data-stu-id="d6521-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="d6521-124">您可以從 [Azure 下載](https://azure.microsoft.com/downloads/) 頁面安裝 SDK，使用您偏好的語言開發應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="d6521-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="d6521-125">三個雲端服務功能需要特別組態，您才能匯出服務封裝：</span><span class="sxs-lookup"><span data-stu-id="d6521-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="d6521-126">如果您要部署使用安全通訊端層 (SSL) 進行資料加密的雲端服務，請針對 SSL [設定應用程式](cloud-services-configure-ssl-certificate-portal.md#modify) 。</span><span class="sxs-lookup"><span data-stu-id="d6521-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="d6521-127">如果您要設定角色執行個體的遠端桌面連線，請 [設定遠端桌面的角色](cloud-services-role-enable-remote-desktop-new-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="d6521-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="d6521-128">如果您要設定雲端服務的詳細資訊監視，請啟用雲端服務的 Azure 診斷。</span><span class="sxs-lookup"><span data-stu-id="d6521-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="d6521-129">*最小監視* (預設監視層級) 使用從角色執行個體 (虛擬機器) 的主機作業系統收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="d6521-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="d6521-130">*詳細資訊監視* 會按照角色執行個體內的效能資料來收集其他度量，以便進一步分析應用程式處理期間發生的問題。</span><span class="sxs-lookup"><span data-stu-id="d6521-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="d6521-131">若要了解如何啟用 Azure 診斷，請參閱 [在 Azure 中啟用診斷](cloud-services-dotnet-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="d6521-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="d6521-132">若要使用 Web 角色或背景工作角色的部署來建立雲端服務，您必須 [建立服務封裝](cloud-services-model-and-package.md#servicepackagecspkg)。</span><span class="sxs-lookup"><span data-stu-id="d6521-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d6521-133">開始之前</span><span class="sxs-lookup"><span data-stu-id="d6521-133">Before you begin</span></span>
* <span data-ttu-id="d6521-134">如果您尚未安裝 Azure SDK，請按一下 [安裝 Azure SDK] 開啟 [Azure 下載頁面](https://azure.microsoft.com/downloads/)，然後依照您偏好使用的程式碼開發語言下載 SDK。</span><span class="sxs-lookup"><span data-stu-id="d6521-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="d6521-135">(您稍後將有機會這麼做。)</span><span class="sxs-lookup"><span data-stu-id="d6521-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="d6521-136">如果任何角色執行個體需要憑證，請建立憑證。</span><span class="sxs-lookup"><span data-stu-id="d6521-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="d6521-137">雲端服務需要含有私密金鑰的 .pfx 檔。</span><span class="sxs-lookup"><span data-stu-id="d6521-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="d6521-138">您建立並部署雲端服務時，可以將憑證上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="d6521-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="d6521-139">建立和部署</span><span class="sxs-lookup"><span data-stu-id="d6521-139">Create and deploy</span></span>
1. <span data-ttu-id="d6521-140">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d6521-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d6521-141">按一下 [新增] > [計算]，然後向下捲動至 [雲端服務] 並按一下。</span><span class="sxs-lookup"><span data-stu-id="d6521-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="d6521-143">在新的 [雲端服務] 刀鋒視窗中，輸入 [DNS 名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="d6521-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="d6521-144">建立新的 [資源群組]  或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6521-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="d6521-145">選取 [位置] 。</span><span class="sxs-lookup"><span data-stu-id="d6521-145">Select a **Location**.</span></span>
6. <span data-ttu-id="d6521-146">按一下 [封裝] 。</span><span class="sxs-lookup"><span data-stu-id="d6521-146">Click **Package**.</span></span> <span data-ttu-id="d6521-147">這會開啟 [上傳封裝]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d6521-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="d6521-148">填寫必要欄位。</span><span class="sxs-lookup"><span data-stu-id="d6521-148">Fill in the required fields.</span></span> <span data-ttu-id="d6521-149">如果您的任一個角色包含單一執行個體，請確定核取 [即使一個或多個角色包含單一執行個體，也要部署]  。</span><span class="sxs-lookup"><span data-stu-id="d6521-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="d6521-150">請確定已選取 [開始部署]  。</span><span class="sxs-lookup"><span data-stu-id="d6521-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="d6521-151">按一下 [確定] 以關閉 [上傳套件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d6521-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="d6521-152">如果您沒有任何憑證可新增，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d6521-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="d6521-154">上傳憑證</span><span class="sxs-lookup"><span data-stu-id="d6521-154">Upload a certificate</span></span>
<span data-ttu-id="d6521-155">如果您的部署套件 [設定為使用憑證](cloud-services-configure-ssl-certificate-portal.md#modify)，您現在可以上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="d6521-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="d6521-156">選取 [憑證]，然後在 [新增憑證] 刀鋒視窗中，選取 SSL 憑證 .pfx 檔案，並提供憑證的 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="d6521-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="d6521-157">按一下 [附加憑證]，然後在 [新增憑證] 刀鋒視窗按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d6521-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="d6521-158">在 [雲端服務] 刀鋒視窗按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="d6521-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="d6521-159">當部署達到了 [就緒]  狀態時，您可以繼續進行接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="d6521-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![發佈您的雲端服務](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="d6521-161">確認部署是否成功完成</span><span class="sxs-lookup"><span data-stu-id="d6521-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="d6521-162">按一下雲端服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6521-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="d6521-163">狀態應該會顯示服務為 [正在執行] 。</span><span class="sxs-lookup"><span data-stu-id="d6521-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="d6521-164">在 [基本功能] 下，按一下 [網站 URL]，在網頁瀏覽器中開啟您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d6521-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="d6521-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6521-166">Next steps</span></span>
* <span data-ttu-id="d6521-167">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d6521-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="d6521-168">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d6521-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="d6521-169">[管理您的雲端服務](cloud-services-how-to-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d6521-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="d6521-170">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d6521-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
