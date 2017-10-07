---
title: "使用 API 管理快速入門 aaaAzure Service Fabric |Microsoft 文件"
description: "本指南也說明如何 tooquickly 開始使用 Azure API 管理和服務網狀架構。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="fa2b7-103">Service Fabric 搭配 Azure API 管理快速入門</span><span class="sxs-lookup"><span data-stu-id="fa2b7-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="fa2b7-104">本指南也說明如何 tooset 以 Service Fabric 的 Azure API 管理及設定 Service Fabric 中的第一個應用程式開發介面作業 toosend 流量 tooback 後端服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="fa2b7-105">toolearn 有關使用 Service Fabric 的 Azure API 管理案例的詳細資訊，請參閱 「 hello[概觀](service-fabric-api-management-overview.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="fa2b7-106">部署應用程式開發介面管理和服務網狀架構 tooAzure</span><span class="sxs-lookup"><span data-stu-id="fa2b7-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="fa2b7-107">toodeploy API 管理而共用的虛擬網路中的 Service Fabric 叢集 tooAzure hello 第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="fa2b7-108">這可讓 Service Fabric 直接使用 API 管理 toocommunicate，讓它直接 tooany 後端服務在 Service Fabric 中可以執行服務探索、 服務分割解析，以及將流量。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="fa2b7-109">拓撲</span><span class="sxs-lookup"><span data-stu-id="fa2b7-109">Topology</span></span>

<span data-ttu-id="fa2b7-110">本指南將部署的 hello 下列 API 管理和服務網狀架構中的子網路是拓樸 tooAzure hello 相同虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![圖片標題][sf-apim-topology-overview]

<span data-ttu-id="fa2b7-112">tooget 快速地開始，資源管理員範本可供每個部署步驟：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="fa2b7-113">網路拓撲：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-113">Network topology:</span></span>
    - <span data-ttu-id="fa2b7-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="fa2b7-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="fa2b7-116">Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="fa2b7-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="fa2b7-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="fa2b7-119">API 管理：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-119">API Management:</span></span>
    - <span data-ttu-id="fa2b7-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="fa2b7-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="fa2b7-122">登入 tooAzure 並選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fa2b7-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="fa2b7-123">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="fa2b7-124">當您啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，並選取您的訂用帳戶，然後再執行 Azure 命令。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="fa2b7-125">Azure 帳戶登入 tooyour 中：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="fa2b7-126">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="fa2b7-127">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="fa2b7-127">Create a resource group</span></span>

<span data-ttu-id="fa2b7-128">為您的部署建立新的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="fa2b7-129">為其命名並提供位置。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="fa2b7-130">部署 hello 網路拓撲</span><span class="sxs-lookup"><span data-stu-id="fa2b7-130">Deploy hello network topology</span></span>

<span data-ttu-id="fa2b7-131">hello 第一個步驟是 tooset 向上 hello 網路拓樸 toowhich API 管理，並將部署的 hello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="fa2b7-132">hello [network.json] [ network-arm] Resource Manager 範本會設定的 toocreate 虛擬網路 (VNET) 具有兩個的子網路和兩個網路安全性群組 (NSG) 群組。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="fa2b7-133">hello [network.parameters.json] [ network-parameters-arm]參數檔案包含 hello 名稱 hello 子網路和應用程式開發介面管理和服務網狀架構將會部署到的 Nsg。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="fa2b7-134">本指南中，hello 參數值就不需要 toobe 變更。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="fa2b7-135">使用這些值的 hello API 管理和服務網狀架構資源管理員範本，因此如果在修改這裡，您必須修改在據以 hello 其他資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="fa2b7-136">下載下列資源管理員範本和參數檔 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="fa2b7-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="fa2b7-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="fa2b7-139">使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 hello 網路安裝程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="fa2b7-140">部署 hello Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="fa2b7-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="fa2b7-141">一旦部署完成 hello 網路資源，hello 下一個步驟是 toodeploy Service Fabric 叢集 toohello VNET hello 子網路中，且 NSG 指定 hello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="fa2b7-142">本教學課程，hello 服務網狀架構資源管理員範本是預先設定的 toouse hello 名稱 hello VNET、 子網路，以及您 hello 上一個步驟中設定的 NSG。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="fa2b7-143">hello Service Fabric 叢集資源管理員範本是已設定的 toocreate 憑證安全性的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="fa2b7-144">hello 憑證是針對您的叢集和 toomanage 使用者存取 tooyour Service Fabric 叢集使用的 toosecure 節點對節點通訊。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="fa2b7-145">API 管理使用此憑證 tooaccess hello Service Fabric 命名服務的服務探索。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="fa2b7-146">基於叢集安全性考量，此步驟需要您在 Key Vault 中有憑證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="fa2b7-147">如需有關使用 Key Vault 來設定安全叢集的詳細資訊，請參閱[這份關於使用 Resource Manager 在 Azure 中建立叢集的指南](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="fa2b7-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="fa2b7-148">您可以在用於叢集存取的加法 toohello 憑證加入 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="fa2b7-149">Azure Active Directory hello 建議方式 toomanage 使用者存取 tooyour Service Fabric 叢集，但不是需要 toocomplete 本教學課程。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="fa2b7-150">不論是叢集的節點對節點安全性，還是「Azure API 管理」驗證，都需要憑證，後者目前不支援向 Service Fabric 後端的 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="fa2b7-151">下載下列資源管理員範本和參數檔 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="fa2b7-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="fa2b7-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="fa2b7-154">填寫在 hello hello 空參數`cluster.parameters.json`檔案的部署，包括 hello[金鑰保存庫資訊](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault)叢集憑證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="fa2b7-155">使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 toocreate hello Service Fabric 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="fa2b7-156">部署 API 管理</span><span class="sxs-lookup"><span data-stu-id="fa2b7-156">Deploy API Management</span></span>

<span data-ttu-id="fa2b7-157">最後，部署在 hello 子網路和指定的 API 管理 NSG 中的 API 管理 toohello VNET。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="fa2b7-158">您無須 toowait 的 hello Service Fabric 叢集部署 toofinish 之前部署 API 管理。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="fa2b7-159">本教學課程，hello API 管理 Resource Manager 範本是預先設定的 toouse hello 名稱 hello VNET、 子網路，以及您 hello 上一個步驟中設定的 NSG。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="fa2b7-160">下載下列資源管理員範本和參數檔 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="fa2b7-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="fa2b7-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fa2b7-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="fa2b7-163">填寫在 hello hello 空參數`apim.parameters.json`為您的部署。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="fa2b7-164">使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 API 管理的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa2b7-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="fa2b7-165">設定 API 管理</span><span class="sxs-lookup"><span data-stu-id="fa2b7-165">Configure API Management</span></span>

<span data-ttu-id="fa2b7-166">部署完您的「API 管理」與 Service Fabric 叢集之後，您可以在「API 管理」中設定 Service Fabric 後端。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="fa2b7-167">這可讓您 toocreate 傳送流量 tooyour Service Fabric 叢集的後端服務原則。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="fa2b7-168">API 管理安全性</span><span class="sxs-lookup"><span data-stu-id="fa2b7-168">API Management Security</span></span>

<span data-ttu-id="fa2b7-169">tooconfigure hello Service Fabric 後端中，您必須先 tooconfigure API 管理安全性設定。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="fa2b7-170">tooconfigure 安全性設定，請移 tooyour API 管理服務在 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="fa2b7-171">啟用 hello API 管理 REST API</span><span class="sxs-lookup"><span data-stu-id="fa2b7-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="fa2b7-172">hello API 管理 REST API 是目前唯一的方式 tooconfigure hello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="fa2b7-173">hello 第一個步驟為 tooenable hello API 管理 REST API，並保護其安全。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="fa2b7-174">在 hello API 管理服務中，選取 **管理 API-PREVIEW**下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="fa2b7-175">檢查 hello**啟用 API 管理 REST API**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="fa2b7-176">請注意 hello 管理 API URL-這是我們會使用向上 hello Service Fabric 後端的更新版本 tooset hello URL</span><span class="sxs-lookup"><span data-stu-id="fa2b7-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="fa2b7-177">產生**存取權杖**藉由選取到期日和索引鍵，然後按一下 hello**產生**朝 hello hello 頁面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="fa2b7-178">複製 hello**存取權杖**並將它儲存-我們會使用它在 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="fa2b7-179">請注意這點不同於 hello 主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="fa2b7-180">上傳 Service Fabric 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="fa2b7-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="fa2b7-181">API 管理必須與您的 Service Fabric 叢集服務探索使用具有存取 tooyour 叢集的用戶端憑證驗證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="fa2b7-182">為了簡單起見，這個教學課程使用 hello 相同的憑證建立其預設值可以是使用的 tooaccess hello Service Fabric 叢集時，指定您的叢集。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="fa2b7-183">在 hello API 管理服務中，選取 **用戶端憑證-PREVIEW**下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="fa2b7-184">按一下 hello **+ 加**按鈕</span><span class="sxs-lookup"><span data-stu-id="fa2b7-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="fa2b7-185">選取 hello 私密金鑰檔 (.pfx) 的 hello 叢集指定憑證，則建立 Service Fabric 叢集時，為它命名，並提供 hello 私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="fa2b7-186">本教學課程使用相同憑證的 hello 的用戶端驗證和叢集節點的安全性。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="fa2b7-187">如果您有一個設定的 tooaccess Service Fabric 叢集，您可以使用不同的用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="fa2b7-188">設定 hello 後端</span><span class="sxs-lookup"><span data-stu-id="fa2b7-188">Configure hello backend</span></span>

<span data-ttu-id="fa2b7-189">API 管理的安全性設定，您可以設定 hello Service Fabric 後端。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="fa2b7-190">Service Fabric 範例 hello Service Fabric 叢集是 hello 後端，而不是特定的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="fa2b7-191">這允許一項服務比單一原則 tooroute toomore hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="fa2b7-192">這個步驟需要 hello 您先前產生的存取權杖，並 hello 您上傳 tooAPI 管理 hello 上一個步驟中的您叢集的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="fa2b7-193">如果您使用不同的用戶端憑證 hello 上一個步驟中的 API 管理，您需要 hello 指紋 hello 用戶端憑證在此步驟中加入 toohello 叢集憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="fa2b7-194">傳送 hello 遵循 HTTP PUT 要求 toohello 您先前記下啟用 hello API 管理 REST API tooconfigure hello Service Fabric 後端服務時的 API 管理 API URL。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="fa2b7-195">您應該會看到`HTTP 201 Created`hello 命令執行成功的回應。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="fa2b7-196">如需有關每個欄位的詳細資訊，請參閱 hello API 管理[後端應用程式開發介面參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="fa2b7-197">HTTP 命令和 URL：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="fa2b7-198">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="fa2b7-199">要求本文：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="fa2b7-200">hello **url**這裡參數就是完整的服務名稱是在叢集中的所有要求的服務路由 tooby 預設，如果後端原則中不指定任何服務名稱。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="fa2b7-201">您可能使用假的服務名稱，例如"fabric: / 假/服務 」 如果您不想 toohave 後援服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="fa2b7-202">請參閱 toohello API 管理[後端應用程式開發介面參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)如需有關每個欄位。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="fa2b7-203">範例</span><span class="sxs-lookup"><span data-stu-id="fa2b7-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="fa2b7-204">部署 Service Fabric 後端服務</span><span class="sxs-lookup"><span data-stu-id="fa2b7-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="fa2b7-205">有 hello Service Fabric 設定為後端 tooAPI 管理之後，您可以編寫後端原則，您將流量傳送 tooyour Service Fabric 服務的 api。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="fa2b7-206">但首先您必須在 Service Fabric tooaccept 要求中執行的服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="fa2b7-207">建立具有 HTTP 端點的 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="fa2b7-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="fa2b7-208">此教學課程中，我們將建立基本無狀態 ASP.NET Core 可靠的服務使用 hello 預設 Web API 專案範本。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="fa2b7-209">這會為您的服務建立一個 HTTP 端點，而您將會透過「Azure API 管理」來公開此服務：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="fa2b7-210">請從[為您的 ASP.NET Core 開發設定開發環境](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core)開始著手。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="fa2b7-211">設定完開發環境之後，請以「系統管理員」身分啟動 Visual Studio，然後建立 ASP.NET Core 服務：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="fa2b7-212">在 Visual Studio 中，選取 [檔案] -> [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="fa2b7-213">選取雲端下的 hello Service Fabric 應用程式範本並將其命名**"ApiApplication"**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="fa2b7-214">選取 hello ASP.NET Core 服務範本和名稱 hello 專案**"WebApiService"**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="fa2b7-215">選取 Web 應用程式開發介面 ASP.NET Core 1.1 hello 專案範本。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="fa2b7-216">Hello 專案建立之後，開啟`PackageRoot\ServiceManifest.xml`並移除 hello `Port` hello 端點資源的組態屬性：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="fa2b7-217">這可讓 Service Fabric toospecify hello 應用程式連接埠的範圍，我們透過 hello 網路安全性小組在 hello 叢集資源管理員範本中，開啟允許流量 tooflow tooit 從 API 管理中的動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="fa2b7-218">按 f5 鍵，在 Visual Studio tooverify hello web API 中的是在本機使用。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="fa2b7-219">開啟 Service Fabric 總管，並向下切入 tooa hello ASP.NET Core service toosee hello 基底位址 hello 服務正在接聽的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="fa2b7-220">新增`/api/values`toohello 基底地址，並在瀏覽器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="fa2b7-221">這樣會叫用 hello hello Web API 範本中的 hello ValuesController 上的 Get 方法。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="fa2b7-222">它會傳回 hello hello 範本，包含兩個字串的 JSON 陣列所提供的預設回應：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="fa2b7-223">這是您將會公開透過 API 管理 Azure 中的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="fa2b7-224">最後，部署在 Azure 中的 hello 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="fa2b7-225">[使用 Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)，以滑鼠右鍵按一下 hello 應用程式專案，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="fa2b7-226">提供您的叢集端點 (例如， `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello 應用程式 tooyour Service Fabric 叢集在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="fa2b7-227">一個名為 `fabric:/ApiApplication/WebApiService` 的 ASP.NET Core 無狀態服務現在應該正在 Azure 中的 Service Fabric 叢集內執行。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="fa2b7-228">建立 API 作業</span><span class="sxs-lookup"><span data-stu-id="fa2b7-228">Create an API operation</span></span>

<span data-ttu-id="fa2b7-229">現在我們準備 toocreate API 管理中的作業與該外部用戶端使用 toocommunicate hello hello Service Fabric 叢集中執行的 ASP.NET Core 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="fa2b7-230">登入 toohello Azure 入口網站，並瀏覽 tooyour API 管理服務部署。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="fa2b7-231">在 hello API 管理服務刀鋒視窗中，選取  **Api-預覽**</span><span class="sxs-lookup"><span data-stu-id="fa2b7-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="fa2b7-232">加入新的應用程式開發介面，請按一下 hello**空白應用程式開發介面**方塊，並填寫 [hello] 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="fa2b7-233">**Web 服務 URL**：就 Service Fabric 後端而言，並不使用此 URL 值。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="fa2b7-234">您可以在這裡輸入任何值。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-234">You can put any value here.</span></span> <span data-ttu-id="fa2b7-235">針對本教學課程，請使用：`http://servicefabric`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="fa2b7-236">**名稱**：為您的 API 提供任何名稱。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="fa2b7-237">針對本教學課程，請使用 `Service Fabric App`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="fa2b7-238">**URL 配置**：選取 [HTTP]、[HTTPS] 或 [both]。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="fa2b7-239">針對本教學課程，請使用 `both`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="fa2b7-240">**API URL 尾碼**：為 API 提供一個尾碼。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="fa2b7-241">針對本教學課程，請使用 `myapp`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="fa2b7-242">一旦建立 hello API 時，按一下  **+ 加入作業**tooadd 前端的 API 作業。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="fa2b7-243">填寫 hello 值：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="fa2b7-244">**URL**： 選取`GET`和 hello API 提供的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="fa2b7-245">針對本教學課程，請使用 `/api/values`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="fa2b7-246">根據預設，hello URL 指定路徑這裡 hello URL 路徑傳送 toohello 後端服務的網狀架構服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="fa2b7-247">如果您使用 hello 相同 URL 路徑以下服務所使用，在此情況下`/api/values`，然後 hello 作業適用於不需要進一步修改。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="fa2b7-248">您也可以指定 URL 路徑不同於您的後端服務的網狀架構服務所使用的 hello URL 路徑在此情況下您也會需要 toospecify 路徑重寫作業原則中更新版本。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="fa2b7-249">**顯示名稱**： 提供 hello 應用程式開發介面的任何名稱。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="fa2b7-250">針對本教學課程，請使用 `Values`。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="fa2b7-251">設定後端原則</span><span class="sxs-lookup"><span data-stu-id="fa2b7-251">Configure a backend policy</span></span>

<span data-ttu-id="fa2b7-252">hello 後端原則結合的所有項目。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="fa2b7-253">這是您在其中設定 hello 後端 Service Fabric 服務 toowhich 要求會路由傳送。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="fa2b7-254">您可以套用此原則 tooany API 作業。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="fa2b7-255">hello [Service Fabric 的後端設定](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)提供 hello 下列要求會路由控制項：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="fa2b7-256">藉由指定的 Service Fabric 服務執行個體名稱，可能是硬式編碼服務執行個體選取範圍 (比方說， `"fabric:/myapp/myservice"`) 或產生自 hello HTTP 要求 (例如， `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`)。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="fa2b7-257">分割區解析：方法是使用任何 Service Fabric 資料分割配置來產生分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="fa2b7-258">無狀態服務的複本選取。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="fa2b7-259">解決方式重試重新解決服務的位置，然後重新傳送要求 toospecify hello 條件可讓您的條件。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="fa2b7-260">此教學課程中，建立路由要求直接 toohello 先前部署的 ASP.NET Core 無狀態服務的後端原則：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="fa2b7-261">選取和編輯 hello**輸入原則**hello`Values`按一下 hello [編輯] 圖示，然後再選取作業**程式碼檢視**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="fa2b7-262">在 [hello 原則程式碼編輯器] 中，加入`set-backend-service`原則底下輸入原則，如下所示，並按一下 hello**儲存**按鈕：</span><span class="sxs-lookup"><span data-stu-id="fa2b7-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="fa2b7-263">一組完整的 Service Fabric 後端原則屬性，請參閱 toohello [API 管理後端文件](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="fa2b7-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="fa2b7-264">新增 hello API tooa 產品。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="fa2b7-265">您可以呼叫 hello API 之前，它必須加入您將可以授與存取 toousers tooa 產品。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="fa2b7-266">在 hello API 管理服務中，選取 **產品-PREVIEW**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="fa2b7-267">「API 管理」預設會提供兩種產品：[入門] 和 [無限制]。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="fa2b7-268">選取 hello 無限制的產品。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="fa2b7-269">選取 API。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-269">Select APIs.</span></span>
 4. <span data-ttu-id="fa2b7-270">按一下 hello **+ 加** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="fa2b7-271">選取 hello `Service Fabric App` API hello 前述步驟中建立，並按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="fa2b7-272">進行測試</span><span class="sxs-lookup"><span data-stu-id="fa2b7-272">Test it</span></span>

<span data-ttu-id="fa2b7-273">您現在可以嘗試透過 API 管理服務網狀架構中傳送要求 tooyour 後端服務，直接從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="fa2b7-274">在 hello API 管理服務中，選取  **API-PREVIEW**。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="fa2b7-275">在 [hello `Service Fabric App` hello 先前步驟中，在您建立的應用程式開發介面選取 hello**測試**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="fa2b7-276">按一下 hello**傳送**按鈕 toosend 測試要求 toohello 後端服務。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa2b7-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa2b7-277">Next steps</span></span>

<span data-ttu-id="fa2b7-278">此時，您應該已在 Service Fabric 與「API 管理」做好基本設定。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="fa2b7-279">此教學課程會使用您得以快速設定，您 Service Fabric 叢集 tooget 基本憑證為基礎的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="fa2b7-280">建議您使用 [Azure Active Directory 驗證](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication)，以針對 Service Fabric 叢集提供更進階的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="fa2b7-281">下一步[建立並設定進階的產品設定在 Azure API 管理](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules)tooprepare 應用程式的真實世界的流量。</span><span class="sxs-lookup"><span data-stu-id="fa2b7-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
