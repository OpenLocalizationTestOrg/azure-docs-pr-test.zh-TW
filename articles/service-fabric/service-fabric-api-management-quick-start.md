---
title: "Azure Service Fabric 搭配 API 管理快速入門 | Microsoft Docs"
description: "本指南示範如何快速開始使用 Azure API 管理與 Service Fabric。"
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="28693-103">Service Fabric 搭配 Azure API 管理快速入門</span><span class="sxs-lookup"><span data-stu-id="28693-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="28693-104">本指南示範如何設定搭配 Service Fabric 的「Azure API 管理」，並設定您的第一個 API 作業以將流量傳送到 Service Fabric 中的後端服務。</span><span class="sxs-lookup"><span data-stu-id="28693-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="28693-105">若要深入了解搭配 Service Fabric 的「Azure API 管理」案例，請參閱[概觀](service-fabric-api-management-overview.md)一文。</span><span class="sxs-lookup"><span data-stu-id="28693-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="28693-106">將 API 管理與 Service Fabric 部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="28693-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="28693-107">第一個步驟是將「API 管理」與 Service Fabric 叢集部署至共用「虛擬網路」中的 Azure。</span><span class="sxs-lookup"><span data-stu-id="28693-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="28693-108">這可讓「API 管理」與 Service Fabric 直接進行通訊，以便執行服務探索、服務分割區解析，以及將流量直接轉送到 Service Fabric 中的任何後端服務。</span><span class="sxs-lookup"><span data-stu-id="28693-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="28693-109">拓撲</span><span class="sxs-lookup"><span data-stu-id="28693-109">Topology</span></span>

<span data-ttu-id="28693-110">本指南會將下列拓撲部署至 Azure，其中「API 管理」與 Service Fabric 位於相同「虛擬網路」的子網路中：</span><span class="sxs-lookup"><span data-stu-id="28693-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![圖片標題][sf-apim-topology-overview]

<span data-ttu-id="28693-112">為了快速開始使用，針對每個部署步驟都提供了 Resource Manager 範本：</span><span class="sxs-lookup"><span data-stu-id="28693-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="28693-113">網路拓撲：</span><span class="sxs-lookup"><span data-stu-id="28693-113">Network topology:</span></span>
    - <span data-ttu-id="28693-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="28693-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="28693-116">Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="28693-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="28693-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="28693-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="28693-119">API 管理：</span><span class="sxs-lookup"><span data-stu-id="28693-119">API Management:</span></span>
    - <span data-ttu-id="28693-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="28693-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="28693-122">登入 Azure 帳戶並選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="28693-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="28693-123">本指南使用 [Azure PowerShell][azure-powershell]。</span><span class="sxs-lookup"><span data-stu-id="28693-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="28693-124">開始新的 PowerShell 工作階段時，請先登入您的 Azure 帳戶並選取您的訂用帳戶，然後再執行 Azure 命令。</span><span class="sxs-lookup"><span data-stu-id="28693-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="28693-125">登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="28693-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="28693-126">選取您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="28693-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="28693-127">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="28693-127">Create a resource group</span></span>

<span data-ttu-id="28693-128">為您的部署建立新的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="28693-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="28693-129">為其命名並提供位置。</span><span class="sxs-lookup"><span data-stu-id="28693-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="28693-130">部署網路拓撲</span><span class="sxs-lookup"><span data-stu-id="28693-130">Deploy the network topology</span></span>

<span data-ttu-id="28693-131">第一個步驟是設定將作為「API 管理」與 Service Fabric 叢集部署位置的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="28693-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="28693-132">[network.json][network-arm] Resource Manager 範本已設定為建立一個含有兩個子網路和兩個「網路安全性群組」(NSG) 的「虛擬網路」(VNET)。</span><span class="sxs-lookup"><span data-stu-id="28693-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="28693-133">[network.parameters.json][network-parameters-arm] 參數檔包含將作為「API 管理」與 Service Fabric 部署位置的子網路名稱和 NSG。</span><span class="sxs-lookup"><span data-stu-id="28693-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="28693-134">就這份指南而言，參數值無須變更。</span><span class="sxs-lookup"><span data-stu-id="28693-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="28693-135">「API 管理」與 Service Fabric Resource Manager 範本會使用這些值，因此如果您在這裡修改它們，就必須相應地在其他 Resource Manager 範本中也修改它們。</span><span class="sxs-lookup"><span data-stu-id="28693-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="28693-136">下載下列 Resource Manager 範本和參數檔：</span><span class="sxs-lookup"><span data-stu-id="28693-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="28693-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="28693-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="28693-139">使用下列 PowerShell 命令來部署用於網路設定的 Resource Manager 範本和參數檔：</span><span class="sxs-lookup"><span data-stu-id="28693-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="28693-140">部署 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="28693-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="28693-141">部署完網路資源之後，下一個步驟是將 Service Fabric 叢集部署至為 Service Fabric 叢集指定之子網路與 NSG 中的 VNET。</span><span class="sxs-lookup"><span data-stu-id="28693-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="28693-142">針對本教學課程，Service Fabric Resource Manager 範本已預先設定為使用您在上一個步驟中設定之 VNET、子網路及 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="28693-143">Service Fabric 叢集 Resource Manager 範本已設定為建立具有憑證安全性的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="28693-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="28693-144">此憑證可用來保護您叢集的節點對節點通訊，以及管理使用者對您 Service Fabric 叢集的存取。</span><span class="sxs-lookup"><span data-stu-id="28693-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="28693-145">「API 管理」會使用此憑證來存取「Service Fabric 命名服務」以探索服務。</span><span class="sxs-lookup"><span data-stu-id="28693-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="28693-146">基於叢集安全性考量，此步驟需要您在 Key Vault 中有憑證。</span><span class="sxs-lookup"><span data-stu-id="28693-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="28693-147">如需有關使用 Key Vault 來設定安全叢集的詳細資訊，請參閱[這份關於使用 Resource Manager 在 Azure 中建立叢集的指南](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="28693-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="28693-148">您可以在除了用於存取叢集的憑證之外，再新增 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="28693-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="28693-149">Azure Active Directory 是建議用來管理使用者對您 Service Fabric 叢集之存取的方式，但並非完成本教學課程所需的項目。</span><span class="sxs-lookup"><span data-stu-id="28693-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="28693-150">不論是叢集的節點對節點安全性，還是「Azure API 管理」驗證，都需要憑證，後者目前不支援向 Service Fabric 後端的 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="28693-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="28693-151">下載下列 Resource Manager 範本和參數檔：</span><span class="sxs-lookup"><span data-stu-id="28693-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="28693-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="28693-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="28693-154">填寫用於您部署之 `cluster.parameters.json` 檔案中的空白參數，包括您叢集憑證的 [Key Vault 資訊](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault)。</span><span class="sxs-lookup"><span data-stu-id="28693-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="28693-155">使用下列 PowerShell 命令來部署 Resource Manager 範本和參數檔，以建立 Service Fabric 叢集：</span><span class="sxs-lookup"><span data-stu-id="28693-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="28693-156">部署 API 管理</span><span class="sxs-lookup"><span data-stu-id="28693-156">Deploy API Management</span></span>

<span data-ttu-id="28693-157">最後，將「API 管理」部署至為「API 管理」指定之子網路和 NSG 中的 VNET。</span><span class="sxs-lookup"><span data-stu-id="28693-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="28693-158">您不需要等到 Service Fabric 叢集部署完成再部署「API 管理」。</span><span class="sxs-lookup"><span data-stu-id="28693-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="28693-159">針對本教學課程，「API 管理」Resource Manager 範本已預先設定為使用您在上一個步驟中設定之 VNET、子網路及 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="28693-160">下載下列 Resource Manager 範本和參數檔：</span><span class="sxs-lookup"><span data-stu-id="28693-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="28693-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="28693-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="28693-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="28693-163">填寫用於您部署之 `apim.parameters.json` 中的空白參數。</span><span class="sxs-lookup"><span data-stu-id="28693-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="28693-164">使用下列 PowerShell 命令來部署用於「API 管理」的 Resource Manager 範本和參數檔：</span><span class="sxs-lookup"><span data-stu-id="28693-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="28693-165">設定 API 管理</span><span class="sxs-lookup"><span data-stu-id="28693-165">Configure API Management</span></span>

<span data-ttu-id="28693-166">部署完您的「API 管理」與 Service Fabric 叢集之後，您可以在「API 管理」中設定 Service Fabric 後端。</span><span class="sxs-lookup"><span data-stu-id="28693-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="28693-167">這可讓您建立將流量傳送到 Service Fabric 叢集的後端服務原則。</span><span class="sxs-lookup"><span data-stu-id="28693-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="28693-168">API 管理安全性</span><span class="sxs-lookup"><span data-stu-id="28693-168">API Management Security</span></span>

<span data-ttu-id="28693-169">若要設定 Service Fabric 後端，您必須先設定「API 管理」安全性設定。</span><span class="sxs-lookup"><span data-stu-id="28693-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="28693-170">若要設定安全性設定，請移至您在 Azure 入口網站中的「API 管理」服務。</span><span class="sxs-lookup"><span data-stu-id="28693-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="28693-171">啟用 API 管理 REST API</span><span class="sxs-lookup"><span data-stu-id="28693-171">Enable the API Management REST API</span></span>

<span data-ttu-id="28693-172">「API 管理」REST API 是目前設定後端服務的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="28693-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="28693-173">第一個步驟是啟用「API 管理」REST API 並保護它。</span><span class="sxs-lookup"><span data-stu-id="28693-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="28693-174">在「API 管理」服務中，選取 [安全性] 底下的 [管理 API - 預覽]。</span><span class="sxs-lookup"><span data-stu-id="28693-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="28693-175">選取 [啟用 API 管理 REST API] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="28693-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="28693-176">記下「管理 API」URL - 這是我們稍後將用來設定 Service Fabric 後端的 URL</span><span class="sxs-lookup"><span data-stu-id="28693-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="28693-177">選取到期日和金鑰，然後按一下靠近頁面底部的 [產生] 按鈕來產生「存取權杖」。</span><span class="sxs-lookup"><span data-stu-id="28693-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="28693-178">複製該「存取權杖」並儲存它 - 我們將在接下來的步驟中使用此權杖。</span><span class="sxs-lookup"><span data-stu-id="28693-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="28693-179">請注意，這與主要金鑰和次要金鑰不同。</span><span class="sxs-lookup"><span data-stu-id="28693-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="28693-180">上傳 Service Fabric 用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="28693-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="28693-181">「API 管理」必須使用能夠存取您叢集的用戶端憑證來向 Service Fabric 叢集進行驗證，才能探索服務。</span><span class="sxs-lookup"><span data-stu-id="28693-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="28693-182">為了簡單起見，本教學課程會使用建立 Service Fabric 叢集時所指定的相同憑證，此憑證預設即可用來存取您的叢集。</span><span class="sxs-lookup"><span data-stu-id="28693-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="28693-183">在「API 管理」服務中，選取 [安全性] 底下的 [用戶端憑證 - 預覽]。</span><span class="sxs-lookup"><span data-stu-id="28693-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="28693-184">按一下 [+ 新增] 按鈕</span><span class="sxs-lookup"><span data-stu-id="28693-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="28693-185">選取您建立 Service Fabric 叢集時所指定叢集憑證的私密金鑰檔案 (.pfx)、為它命名，然後提供私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="28693-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="28693-186">本教學課程會將相同的憑證用於用戶端驗證和叢集節點對節點安全性。</span><span class="sxs-lookup"><span data-stu-id="28693-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="28693-187">如果您有一個已設定來存取 Service Fabric 叢集的個別用戶端憑證，則您可以使用該憑證。</span><span class="sxs-lookup"><span data-stu-id="28693-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="28693-188">設定後端</span><span class="sxs-lookup"><span data-stu-id="28693-188">Configure the backend</span></span>

<span data-ttu-id="28693-189">既然已設定「API 管理」安全性，您現在便可以設定 Service Fabric 後端。</span><span class="sxs-lookup"><span data-stu-id="28693-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="28693-190">就 Service Fabric 後端而言，作為後端的是 Service Fabric 叢集，而不是特定的 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="28693-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="28693-191">這可讓單一原則路由傳送到叢集內的多個服務。</span><span class="sxs-lookup"><span data-stu-id="28693-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="28693-192">此步驟需要您稍早產生的存取權杖，以及您在上一個步驟中上傳到「API 管理」之叢集憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="28693-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="28693-193">如果您在上一個步驟中針對「API 管理」使用個別的用戶端憑證，則在此步驟中，除了叢集憑證指紋之外，您還需要用戶端憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="28693-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="28693-194">請將下列 HTTP PUT 要求傳送到您稍早在啟用「API 管理」REST API 以設定 Service Fabric 後端服務時所記下的「API 管理」API URL。</span><span class="sxs-lookup"><span data-stu-id="28693-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="28693-195">當命令成功時，您應該會看到 `HTTP 201 Created` 回應。</span><span class="sxs-lookup"><span data-stu-id="28693-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="28693-196">如需有關每個欄位的詳細資訊，請參閱「API 管理」[後端 API 參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)。</span><span class="sxs-lookup"><span data-stu-id="28693-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="28693-197">HTTP 命令和 URL：</span><span class="sxs-lookup"><span data-stu-id="28693-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="28693-198">要求標頭：</span><span class="sxs-lookup"><span data-stu-id="28693-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="28693-199">要求本文：</span><span class="sxs-lookup"><span data-stu-id="28693-199">Request body:</span></span>
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

<span data-ttu-id="28693-200">這裡的 **url** 參數是當後端原則中未指定任何服務名稱時，您叢集內作為所有要求路由傳送目的地之服務的完整服務名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="28693-201">如果您不打算有後援服務，則可以使用假的服務名稱 (例如 "fabric:/fake/service")。</span><span class="sxs-lookup"><span data-stu-id="28693-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="28693-202">如需有關每個欄位的詳細其他詳細資料，請參閱「API 管理」[後端 API 參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)。</span><span class="sxs-lookup"><span data-stu-id="28693-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="28693-203">範例</span><span class="sxs-lookup"><span data-stu-id="28693-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="28693-204">部署 Service Fabric 後端服務</span><span class="sxs-lookup"><span data-stu-id="28693-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="28693-205">既然您已將 Service Fabric 設定為「API 管理」的後端，現在便可為 API 撰寫將流量傳送到 Service Fabric 服務的後端原則。</span><span class="sxs-lookup"><span data-stu-id="28693-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="28693-206">但是您必須先有一個在 Service Fabric 中執行的服務來接受要求。</span><span class="sxs-lookup"><span data-stu-id="28693-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="28693-207">建立具有 HTTP 端點的 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="28693-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="28693-208">針對本教學課程，我們將使用預設的 Web API 專案範本來建立一個基本的無狀態「ASP.NET Core 可靠服務」。</span><span class="sxs-lookup"><span data-stu-id="28693-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="28693-209">這會為您的服務建立一個 HTTP 端點，而您將會透過「Azure API 管理」來公開此服務：</span><span class="sxs-lookup"><span data-stu-id="28693-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="28693-210">請從[為您的 ASP.NET Core 開發設定開發環境](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core)開始著手。</span><span class="sxs-lookup"><span data-stu-id="28693-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="28693-211">設定完開發環境之後，請以「系統管理員」身分啟動 Visual Studio，然後建立 ASP.NET Core 服務：</span><span class="sxs-lookup"><span data-stu-id="28693-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="28693-212">在 Visual Studio 中，選取 [檔案] -> [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="28693-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="28693-213">選取 [雲端] 底下的 [Service Fabric 應用程式] 範本，然後將它命名為 **"ApiApplication"**。</span><span class="sxs-lookup"><span data-stu-id="28693-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="28693-214">選取 [ASP.NET Core] 服務範本，然後將專案命名為 **"WebApiService"**。</span><span class="sxs-lookup"><span data-stu-id="28693-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="28693-215">選取 [Web API ASP.NET Core 1.1] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="28693-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="28693-216">建立專案之後，開啟 `PackageRoot\ServiceManifest.xml`，然後從端點資源組態中移除 `Port` 屬性：</span><span class="sxs-lookup"><span data-stu-id="28693-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="28693-217">這可讓 Service Fabric 從應用程式連接埠範圍動態指定連接埠，這些是我們透過叢集 Resource Manager 範本中的「網路安全性群組」開啟的連接埠，可允許流量從「API 管理」流到 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="28693-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="28693-218">在 Visual Studio 中按 F5 以確認本機有提供 Web API。</span><span class="sxs-lookup"><span data-stu-id="28693-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="28693-219">開啟 Service Fabric Explorer，然後向下切入到特定的 ASP.NET Core 服務執行個體，以查看此服務所接聽的基底位址。</span><span class="sxs-lookup"><span data-stu-id="28693-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="28693-220">將 `/api/values` 新增到基底位址，然後在瀏覽器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="28693-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="28693-221">這會叫用 Web API 範本中 ValuesController 上的 Get 方法。</span><span class="sxs-lookup"><span data-stu-id="28693-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="28693-222">它會傳回範本所提供的預設回應，也就是包含兩個字串的 JSON 陣列：</span><span class="sxs-lookup"><span data-stu-id="28693-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="28693-223">這是您將透過 Azure 中的「API 管理」公開的端點。</span><span class="sxs-lookup"><span data-stu-id="28693-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="28693-224">最後，將應用程式部署至您在 Azure 中的叢集。</span><span class="sxs-lookup"><span data-stu-id="28693-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="28693-225">[使用 Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)，在 [應用程式] 專案上按一下滑鼠右鍵，然後選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="28693-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="28693-226">提供您的叢集端點 (例如 `mycluster.westus.cloudapp.azure.com:19000`) 以將應用程式部署至您在 Azure 中的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="28693-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="28693-227">一個名為 `fabric:/ApiApplication/WebApiService` 的 ASP.NET Core 無狀態服務現在應該正在 Azure 中的 Service Fabric 叢集內執行。</span><span class="sxs-lookup"><span data-stu-id="28693-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="28693-228">建立 API 作業</span><span class="sxs-lookup"><span data-stu-id="28693-228">Create an API operation</span></span>

<span data-ttu-id="28693-229">現在我們已經準備好在「API 管理」中建立作業，供外部用戶端用來與在 Service Fabric 叢集內執行的 ASP.NET Core 無狀態服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="28693-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="28693-230">登入 Azure 入口網站，然後瀏覽至您的「API 管理」服務部署。</span><span class="sxs-lookup"><span data-stu-id="28693-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="28693-231">在 [API 管理] 服務刀鋒視窗中，選取 [API - 預覽]</span><span class="sxs-lookup"><span data-stu-id="28693-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="28693-232">按一下 [空白 API] 方塊，然後在對話方塊中填入資訊：</span><span class="sxs-lookup"><span data-stu-id="28693-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="28693-233">**Web 服務 URL**：就 Service Fabric 後端而言，並不使用此 URL 值。</span><span class="sxs-lookup"><span data-stu-id="28693-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="28693-234">您可以在這裡輸入任何值。</span><span class="sxs-lookup"><span data-stu-id="28693-234">You can put any value here.</span></span> <span data-ttu-id="28693-235">針對本教學課程，請使用：`http://servicefabric`。</span><span class="sxs-lookup"><span data-stu-id="28693-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="28693-236">**名稱**：為您的 API 提供任何名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="28693-237">針對本教學課程，請使用 `Service Fabric App`。</span><span class="sxs-lookup"><span data-stu-id="28693-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="28693-238">**URL 配置**：選取 [HTTP]、[HTTPS] 或 [both]。</span><span class="sxs-lookup"><span data-stu-id="28693-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="28693-239">針對本教學課程，請使用 `both`。</span><span class="sxs-lookup"><span data-stu-id="28693-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="28693-240">**API URL 尾碼**：為 API 提供一個尾碼。</span><span class="sxs-lookup"><span data-stu-id="28693-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="28693-241">針對本教學課程，請使用 `myapp`。</span><span class="sxs-lookup"><span data-stu-id="28693-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="28693-242">建立 API 之後，按一下 [+ 新增作業] 來新增前端 API 作業。</span><span class="sxs-lookup"><span data-stu-id="28693-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="28693-243">填寫值：</span><span class="sxs-lookup"><span data-stu-id="28693-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="28693-244">**URL**：選取 `GET` 並提供 API 的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="28693-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="28693-245">針對本教學課程，請使用 `/api/values`。</span><span class="sxs-lookup"><span data-stu-id="28693-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="28693-246">根據預設，這裡指定的 URL 路徑是傳送到後端 Service Fabric 服務的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="28693-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="28693-247">如果您在這裡使用與您服務所用相同的 URL 路徑 (在此例中為 `/api/values`)，則無須進一步修改，作業即可運作。</span><span class="sxs-lookup"><span data-stu-id="28693-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="28693-248">您也可以在這裡指定與您後端 Service Fabric 服務所用不同的 URL 路徑，在此情況下，您稍後也將需要在作業原則中指定路徑重寫。</span><span class="sxs-lookup"><span data-stu-id="28693-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="28693-249">**顯示名稱**：為 API 提供任何名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="28693-250">針對本教學課程，請使用 `Values`。</span><span class="sxs-lookup"><span data-stu-id="28693-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="28693-251">設定後端原則</span><span class="sxs-lookup"><span data-stu-id="28693-251">Configure a backend policy</span></span>

<span data-ttu-id="28693-252">後端原則會將所有項目繫結在一起。</span><span class="sxs-lookup"><span data-stu-id="28693-252">The backend policy ties everything together.</span></span> <span data-ttu-id="28693-253">您需在此原則中設定作為要求路由傳送目的地的後端 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="28693-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="28693-254">您可以將此原則套用至任何 API 作業。</span><span class="sxs-lookup"><span data-stu-id="28693-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="28693-255">[Service Fabric 的後端組態](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)提供下列要求路由控制：</span><span class="sxs-lookup"><span data-stu-id="28693-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="28693-256">服務執行個體選取：方法是以硬式編碼 (例如 `"fabric:/myapp/myservice"`) 或從 HTTP 要求產生 (例如 `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`) 來指定 Service Fabric 服務執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="28693-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="28693-257">分割區解析：方法是使用任何 Service Fabric 資料分割配置來產生分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="28693-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="28693-258">無狀態服務的複本選取。</span><span class="sxs-lookup"><span data-stu-id="28693-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="28693-259">解析重試條件：可讓您指定重新解析服務位置及重新傳送要求的條件。</span><span class="sxs-lookup"><span data-stu-id="28693-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="28693-260">針對本教學課程，請建立一個後端原則，以將要求直接路由傳送到稍早部署的 ASP.NET Core 無狀態服務：</span><span class="sxs-lookup"><span data-stu-id="28693-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="28693-261">按一下編輯圖示，然後選取 [程式碼檢視]，以選取和編輯 `Values` 作業的「輸入原則」。</span><span class="sxs-lookup"><span data-stu-id="28693-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="28693-262">在原則程式碼編輯器中，於輸入原則底下新增 `set-backend-service` 原則 (如下所示)，然後按一下 [儲存] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="28693-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="28693-263">如需完整的一組 Service Fabric 後端原則屬性，請參考 [API 管理後端文件](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="28693-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="28693-264">將 API 新增至產品。</span><span class="sxs-lookup"><span data-stu-id="28693-264">Add the API to a product.</span></span> 

<span data-ttu-id="28693-265">您必須先將 API 新增至產品以將存取權授與使用者，才能呼叫該 API。</span><span class="sxs-lookup"><span data-stu-id="28693-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="28693-266">在 [API 管理] 服務中，選取 [產品 - 預覽]。</span><span class="sxs-lookup"><span data-stu-id="28693-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="28693-267">「API 管理」預設會提供兩種產品：[入門] 和 [無限制]。</span><span class="sxs-lookup"><span data-stu-id="28693-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="28693-268">請選取 [無限制] 產品。</span><span class="sxs-lookup"><span data-stu-id="28693-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="28693-269">選取 API。</span><span class="sxs-lookup"><span data-stu-id="28693-269">Select APIs.</span></span>
 4. <span data-ttu-id="28693-270">按一下 [+新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="28693-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="28693-271">選取您在先前步驟中建立的 `Service Fabric App` API，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="28693-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="28693-272">進行測試</span><span class="sxs-lookup"><span data-stu-id="28693-272">Test it</span></span>

<span data-ttu-id="28693-273">您現在可以嘗試直接從 Azure 入口網站透過「API 管理」，將要求傳送到 Service Fabric 中的後端服務。</span><span class="sxs-lookup"><span data-stu-id="28693-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="28693-274">在 [API 管理] 服務中，選取 [API - 預覽]。</span><span class="sxs-lookup"><span data-stu-id="28693-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="28693-275">在您於先前步驟中建立的 `Service Fabric App` API 中，選取 [測試] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="28693-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="28693-276">按一下 [傳送] 按鈕以將測試要求傳送到後端服務。</span><span class="sxs-lookup"><span data-stu-id="28693-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28693-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28693-277">Next steps</span></span>

<span data-ttu-id="28693-278">此時，您應該已在 Service Fabric 與「API 管理」做好基本設定。</span><span class="sxs-lookup"><span data-stu-id="28693-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="28693-279">本教學課程針對您的 Service Fabric 叢集使用基本憑證型使用者驗證，以便讓您快速進行設定。</span><span class="sxs-lookup"><span data-stu-id="28693-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="28693-280">建議您使用 [Azure Active Directory 驗證](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication)，以針對 Service Fabric 叢集提供更進階的使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="28693-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="28693-281">接著，[在 Azure API 管理中建立和設定進階產品設定](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules)，以準備好您的應用程式來應付真實世界流量。</span><span class="sxs-lookup"><span data-stu-id="28693-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
