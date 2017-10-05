---
title: "使用 Visual Studio 設定 Service Fabric 叢集 | Microsoft Docs"
description: "說明如何使用 Azure 資源群組專案在 Visual Studio 中建立的 Azure Resource Manager 範本設定 Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="85325-103">使用 Visual Studio 設定 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="85325-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="85325-104">本文說明如何使用 Visual Studio 和 Azure Resource Manager 範本設定 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="85325-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="85325-105">我們將使用 Visual Studio Azure 資源群組專案來建立範本。</span><span class="sxs-lookup"><span data-stu-id="85325-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="85325-106">建立範本之後，可以從 Visual Studio 直接將範本部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="85325-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="85325-107">也可從指令碼或在連續整合 (CI) 功能中使用它。</span><span class="sxs-lookup"><span data-stu-id="85325-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="85325-108">使用 Azure 資源群組專案建立 Service Fabric 叢集範本</span><span class="sxs-lookup"><span data-stu-id="85325-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="85325-109">若要開始進行，請開啟 Visual Studio 並建立 Azure 資源群組專案 (可在 **Cloud** 資料夾下取得)：</span><span class="sxs-lookup"><span data-stu-id="85325-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![已選取 Azure 資源群組專案的 [新增專案] 對話方塊][1]

<span data-ttu-id="85325-111">您可以為此專案建立新的 Visual Studio 方案，或將它加入至現有的方案。</span><span class="sxs-lookup"><span data-stu-id="85325-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="85325-112">如果在 Cloud 節點之下看不到 Azure 資源群組專案，表示尚未安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="85325-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="85325-113">啟動 Web Platform Installer (如果尚未這麼做，請[立即安裝](http://www.microsoft.com/web/downloads/platform.aspx) )，然後搜尋 "Azure SDK for .NET" 並安裝與您的 Visual Studio 版本相容的版本。</span><span class="sxs-lookup"><span data-stu-id="85325-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="85325-114">按 [確定] 按鈕之後，Visual Studio 會要求您選取您想要建立的資源管理員範本：</span><span class="sxs-lookup"><span data-stu-id="85325-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![已選取 Service Fabric 叢集範本的 [選取 Azure 範本] 對話方塊][2]

<span data-ttu-id="85325-116">選取 [Service Fabric 叢集] 範本，然後再按一次 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="85325-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="85325-117">現在已建立專案與資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="85325-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="85325-118">準備範本以供部署</span><span class="sxs-lookup"><span data-stu-id="85325-118">Prepare the template for deployment</span></span>
<span data-ttu-id="85325-119">在部署範本以建立叢集之前，您必須提供必要的範本參數值。</span><span class="sxs-lookup"><span data-stu-id="85325-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="85325-120">這些參數值讀取自 `ServiceFabricCluster.parameters.json` 檔案，該檔案位於資源群組專案的 `Templates` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="85325-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="85325-121">開啟該檔案並提供下列值：</span><span class="sxs-lookup"><span data-stu-id="85325-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="85325-122">參數名稱</span><span class="sxs-lookup"><span data-stu-id="85325-122">Parameter name</span></span> | <span data-ttu-id="85325-123">說明</span><span class="sxs-lookup"><span data-stu-id="85325-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85325-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="85325-124">adminUserName</span></span> |<span data-ttu-id="85325-125">Service Fabric 電腦 (節點) 的系統管理員帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="85325-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="85325-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="85325-126">certificateThumbprint</span></span> |<span data-ttu-id="85325-127">保護叢集安全的憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="85325-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="85325-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="85325-128">sourceVaultResourceId</span></span> |<span data-ttu-id="85325-129">用來保護叢集的憑證儲存所在之金鑰保存庫的資源識別碼  。</span><span class="sxs-lookup"><span data-stu-id="85325-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="85325-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="85325-130">certificateUrlValue</span></span> |<span data-ttu-id="85325-131">叢集安全性憑證的 URL。</span><span class="sxs-lookup"><span data-stu-id="85325-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="85325-132">Visual Studio Service Fabric 資源管理員範本會建立一個受憑證保護的安全叢集。</span><span class="sxs-lookup"><span data-stu-id="85325-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="85325-133">此憑證是利用最後三個範本參數 (`certificateThumbprint`、`sourceVaultValue` 和 `certificateUrlValue`) 來識別，其必須存在於 **Azure 金鑰保存庫**中。</span><span class="sxs-lookup"><span data-stu-id="85325-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="85325-134">如需如何建立叢集安全性憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) 一文。</span><span class="sxs-lookup"><span data-stu-id="85325-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="85325-135">選擇性︰變更叢集名稱</span><span class="sxs-lookup"><span data-stu-id="85325-135">Optional: change the cluster name</span></span>
<span data-ttu-id="85325-136">每個 Service Fabric 叢集都有一個名稱。</span><span class="sxs-lookup"><span data-stu-id="85325-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="85325-137">在 Azure 中建立網狀架構叢集時，叢集名稱會 (與 Azure 區域一起) 決定叢集的網域名稱系統 (DNS) 名稱。</span><span class="sxs-lookup"><span data-stu-id="85325-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="85325-138">例如，如果您將叢集命名為 `myBigCluster`，而且將裝載新叢集的資源群組位置 (Azure 區域) 是美國東部，則叢集的 DNS 名稱將是 `myBigCluster.eastus.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="85325-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="85325-139">預設會自動產生叢集名稱，而且「叢集」前置詞後面會附加一個隨機的尾碼，使該名稱變成唯一的。</span><span class="sxs-lookup"><span data-stu-id="85325-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="85325-140">如此便可以很容易使用範本做為 **連續整合** (CI) 系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="85325-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="85325-141">如果您想要為叢集使用特定名稱，一個對您有意義的名稱，請將 Resource Manager 範本檔案 (`ServiceFabricCluster.json`) 中 `clusterName` 變數值設定為您所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="85325-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="85325-142">該名稱是該檔案中定義的第一個變數。</span><span class="sxs-lookup"><span data-stu-id="85325-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="85325-143">選擇性：新增公用應用程式連接埠</span><span class="sxs-lookup"><span data-stu-id="85325-143">Optional: add public application ports</span></span>
<span data-ttu-id="85325-144">您也可能想變更叢集的公用應用程式連接埠再部署它。</span><span class="sxs-lookup"><span data-stu-id="85325-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="85325-145">根據預設，範本只會開啟兩個公用 TCP 連接埠 (80 和 8081)。</span><span class="sxs-lookup"><span data-stu-id="85325-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="85325-146">如果您的應用程式需要更多，請修改範本中的 Azure 負載平衡器定義。</span><span class="sxs-lookup"><span data-stu-id="85325-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="85325-147">此定義儲存在主要範本檔案 (`ServiceFabricCluster.json`) 中。</span><span class="sxs-lookup"><span data-stu-id="85325-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="85325-148">開啟該檔案，並搜尋 `loadBalancedAppPort`。</span><span class="sxs-lookup"><span data-stu-id="85325-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="85325-149">每個連接埠會與三個成品相關聯：</span><span class="sxs-lookup"><span data-stu-id="85325-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="85325-150">範本參數：定義連接埠的 TCP 連接埠值：</span><span class="sxs-lookup"><span data-stu-id="85325-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="85325-151">探查：定義 Azure 負載平衡器在容錯移轉到另一個節點之前，會嘗試使用特定 Service Fabric 節點的頻率和時間長度。</span><span class="sxs-lookup"><span data-stu-id="85325-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="85325-152">探查是負載平衡器資源的一部分。</span><span class="sxs-lookup"><span data-stu-id="85325-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="85325-153">以下是第一個預設應用程式連接埠的探查定義：</span><span class="sxs-lookup"><span data-stu-id="85325-153">Here is the probe definition for the first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="85325-154">將連接埠和探查繫結在一起的「負載平衡規則」  ，可在一組 Service Fabric 叢集節點上啟用負載平衡：</span><span class="sxs-lookup"><span data-stu-id="85325-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="85325-155">如果您打算部署至叢集的應用程式需要更多連接埠，您可以透過建立其他探查和負載平衡規則定義來新增連接埠。</span><span class="sxs-lookup"><span data-stu-id="85325-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="85325-156">如需如何透過 Resource Manager 範本使用 Azure Load Balancer 的詳細資訊，請參閱 [開始使用範本建立內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="85325-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="85325-157">使用 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="85325-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="85325-158">在`ServiceFabricCluster.param.dev.json` 中儲存所有必要的參數值後，您就可以部署範本和建立 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="85325-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="85325-159">以滑鼠右鍵按一下 Visual Studio [方案總管] 中的資源群組專案，然後選擇 [部署 | 新增部署...] 。</span><span class="sxs-lookup"><span data-stu-id="85325-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="85325-160">如有必要，Visual Studio 會顯示 [部署到資源群組] 對話方塊，要求您向 Azure 進行驗證：</span><span class="sxs-lookup"><span data-stu-id="85325-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![[部署到資源群組] 對話方塊][3]

<span data-ttu-id="85325-162">此對話方塊可讓您選擇叢集的現有資源管理員資源群組，並提供給您建立新資源群組的選項。</span><span class="sxs-lookup"><span data-stu-id="85325-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="85325-163">通常對 Service Fabric 叢集使用個別的資源群組是很合理的。</span><span class="sxs-lookup"><span data-stu-id="85325-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="85325-164">按 [部署] 按鈕後，Visual Studio 就會提示您確認範本參數值。</span><span class="sxs-lookup"><span data-stu-id="85325-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="85325-165">按 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="85325-165">Hit the **Save** button.</span></span> <span data-ttu-id="85325-166">有一個參數沒有持續的值：叢集的系統管理員帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="85325-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="85325-167">當 Visual Studio 提示您提供密碼值時，您必須這麼做。</span><span class="sxs-lookup"><span data-stu-id="85325-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="85325-168">從 Azure SDK 2.9 開始，Visual Studio 支援在部署期間從 **Azure 金鑰保存庫**讀取密碼。</span><span class="sxs-lookup"><span data-stu-id="85325-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="85325-169">在 [範本參數] 對話方塊中，注意 `adminPassword` 參數文字方塊右邊有小的「金鑰」圖示。</span><span class="sxs-lookup"><span data-stu-id="85325-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="85325-170">這個圖示可讓您選取現有的金鑰保存庫密碼做為叢集的系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="85325-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="85325-171">務必先在金鑰保存庫的進階存取原則中啟用範本部署的 Azure Resource Manager 存取權。</span><span class="sxs-lookup"><span data-stu-id="85325-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="85325-172">您可以在 Visual Studio 的 [輸出] 視窗中監視部署程序的進度。</span><span class="sxs-lookup"><span data-stu-id="85325-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="85325-173">一旦完成範本部署，即可使用您的新叢集！</span><span class="sxs-lookup"><span data-stu-id="85325-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="85325-174">如果 PowerShell 未曾用來從您目前使用的電腦管理 Azure，則需要進行一些內部管理。</span><span class="sxs-lookup"><span data-stu-id="85325-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="85325-175">執行 [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) 命令以啟用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="85325-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="85325-176">開發電腦通常可接受「不受限制」原則。</span><span class="sxs-lookup"><span data-stu-id="85325-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="85325-177">決定是否允許從 Azure PowerShell 命令收集診斷資料，並且視需要執行 [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) 或 [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx)。</span><span class="sxs-lookup"><span data-stu-id="85325-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="85325-178">這可在範本部署期間避免不必要的提示。</span><span class="sxs-lookup"><span data-stu-id="85325-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="85325-179">如果有任何錯誤，請移至 [Azure 入口網站](https://portal.azure.com/) ，並開啟您要部署的目標資源群組。</span><span class="sxs-lookup"><span data-stu-id="85325-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="85325-180">按一下 [所有設定]，然後按一下設定刀鋒視窗上的 [部署]。</span><span class="sxs-lookup"><span data-stu-id="85325-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="85325-181">資源群組部署失敗會在通知中留下詳細的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="85325-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="85325-182">Service Fabric 叢集需要有一定數量的節點運作中，以維護可用性並維持狀態 - 稱為「維持仲裁」。</span><span class="sxs-lookup"><span data-stu-id="85325-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="85325-183">因此，除非您已先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)，否則關閉叢集中的所有電腦並不安全。</span><span class="sxs-lookup"><span data-stu-id="85325-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="85325-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85325-184">Next steps</span></span>
* [<span data-ttu-id="85325-185">了解如何使用 Azure 入口網站設定 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="85325-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="85325-186">了解如何使用 Visual Studio 管理和部署 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="85325-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
