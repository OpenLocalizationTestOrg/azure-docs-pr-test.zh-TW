---
title: "使用 Visual Studio Service Fabric 叢集 aaaSetting |Microsoft 文件"
description: "描述如何 tooset 註冊 Service Fabric 叢集所使用的 Azure 資源群組專案在 Visual Studio 中所建立的 Azure Resource Manager 範本"
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
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="ae84b-103">使用 Visual Studio 設定 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="ae84b-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="ae84b-104">本文說明如何使用 Visual Studio 和 Azure Resource Manager 範本 tooset 向上 Azure Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae84b-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="ae84b-105">我們將使用 Visual Studio Azure 資源群組專案 toocreate hello 範本。</span><span class="sxs-lookup"><span data-stu-id="ae84b-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="ae84b-106">建立 hello 範本之後，它可以部署直接從 Visual Studio tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ae84b-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="ae84b-107">也可從指令碼或在連續整合 (CI) 功能中使用它。</span><span class="sxs-lookup"><span data-stu-id="ae84b-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="ae84b-108">使用 Azure 資源群組專案建立 Service Fabric 叢集範本</span><span class="sxs-lookup"><span data-stu-id="ae84b-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="ae84b-109">tooget 啟動中，開啟 Visual Studio 並建立 Azure 資源群組專案 (即在 hello**雲端**資料夾):</span><span class="sxs-lookup"><span data-stu-id="ae84b-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![已選取 Azure 資源群組專案的 [新增專案] 對話方塊][1]

<span data-ttu-id="ae84b-111">您可以建立新的 Visual Studio 方案，此專案，或將它加入 tooan 現有的方案。</span><span class="sxs-lookup"><span data-stu-id="ae84b-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="ae84b-112">如果看不到 hello Azure 資源群組專案 hello 雲端 節點下的，表示您沒有 hello 已安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="ae84b-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="ae84b-113">啟動 Web Platform Installer ([立即安裝](http://www.microsoft.com/web/downloads/platform.aspx)如果您還沒有)，然後搜尋 < Azure SDK for.NET 中，並安裝 hello 版本與您的 Visual Studio 版本相容。</span><span class="sxs-lookup"><span data-stu-id="ae84b-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="ae84b-114">點擊 hello [確定] 按鈕之後，Visual Studio 會詢問您想 toocreate tooselect hello Resource Manager 範本：</span><span class="sxs-lookup"><span data-stu-id="ae84b-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![已選取 Service Fabric 叢集範本的 [選取 Azure 範本] 對話方塊][2]

<span data-ttu-id="ae84b-116">再次選取 hello Service Fabric 叢集範本和叫用的 hello [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae84b-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="ae84b-117">hello 專案和 hello Resource Manager 範本現在已建立。</span><span class="sxs-lookup"><span data-stu-id="ae84b-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="ae84b-118">準備部署的 hello 範本</span><span class="sxs-lookup"><span data-stu-id="ae84b-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="ae84b-119">Hello 範本是已部署的 toocreate hello 叢集之前，您必須提供所需的 hello 範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="ae84b-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="ae84b-120">這些參數值從 hello 讀取`ServiceFabricCluster.parameters.json`檔案，位於 hello `Templates` hello 資源群組專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ae84b-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="ae84b-121">開啟 hello 檔案，並提供下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae84b-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="ae84b-122">參數名稱</span><span class="sxs-lookup"><span data-stu-id="ae84b-122">Parameter name</span></span> | <span data-ttu-id="ae84b-123">說明</span><span class="sxs-lookup"><span data-stu-id="ae84b-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae84b-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="ae84b-124">adminUserName</span></span> |<span data-ttu-id="ae84b-125">hello hello 系統管理員帳戶名稱的 Service Fabric 機器 （節點）。</span><span class="sxs-lookup"><span data-stu-id="ae84b-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="ae84b-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="ae84b-126">certificateThumbprint</span></span> |<span data-ttu-id="ae84b-127">hello，可保護 hello 叢集 hello 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="ae84b-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="ae84b-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="ae84b-128">sourceVaultResourceId</span></span> |<span data-ttu-id="ae84b-129">hello*資源識別碼*hello 金鑰保存庫，可保護 hello 叢集 hello 憑證的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="ae84b-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="ae84b-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="ae84b-130">certificateUrlValue</span></span> |<span data-ttu-id="ae84b-131">hello hello 叢集安全性憑證 URL。</span><span class="sxs-lookup"><span data-stu-id="ae84b-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="ae84b-132">hello Visual Studio 服務網狀架構資源管理員範本會建立安全的叢集所保護的憑證。</span><span class="sxs-lookup"><span data-stu-id="ae84b-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="ae84b-133">此憑證由 hello 最後三個樣板參數 (`certificateThumbprint`， `sourceVaultValue`，和`certificateUrlValue`)，且必須存在於**Azure 金鑰保存庫**。</span><span class="sxs-lookup"><span data-stu-id="ae84b-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="ae84b-134">如需有關如何 toocreate hello 叢集安全性憑證的詳細資訊，請參閱[Service Fabric 叢集安全性案例](service-fabric-cluster-security.md#x509-certificates-and-service-fabric)發行項。</span><span class="sxs-lookup"><span data-stu-id="ae84b-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="ae84b-135">選擇性： 變更 hello 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="ae84b-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="ae84b-136">每個 Service Fabric 叢集都有一個名稱。</span><span class="sxs-lookup"><span data-stu-id="ae84b-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="ae84b-137">在 Azure 中建立網狀架構叢集時，叢集名稱會決定 （搭配 hello Azure 地區) hello hello 叢集的網域名稱系統 (DNS) 名稱。</span><span class="sxs-lookup"><span data-stu-id="ae84b-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="ae84b-138">例如，如果您將檔案命名您的叢集`myBigCluster`，和將裝載 hello 新叢集的 hello 資源群組的 hello 位置 （Azure 地區） 是美國東部、 hello hello 叢集 DNS 名稱會是`myBigCluster.eastus.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="ae84b-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ae84b-139">根據預設 hello 叢集名稱是自動產生，而且後面會附加隨機尾碼 tooa 「 叢集 」 前置詞。</span><span class="sxs-lookup"><span data-stu-id="ae84b-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="ae84b-140">這使得您可以非常輕易 toouse hello 範本的一部分**連續整合**(CI) 系統。</span><span class="sxs-lookup"><span data-stu-id="ae84b-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="ae84b-141">如果您想 toouse 之特定名稱的叢集，一個是有意義的 tooyou 設定 hello hello 值`clusterName`hello 資源管理員範本檔案中的變數 (`ServiceFabricCluster.json`) tooyour 選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="ae84b-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="ae84b-142">它是定義在該檔案中的 hello 第一個變數。</span><span class="sxs-lookup"><span data-stu-id="ae84b-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="ae84b-143">選擇性：新增公用應用程式連接埠</span><span class="sxs-lookup"><span data-stu-id="ae84b-143">Optional: add public application ports</span></span>
<span data-ttu-id="ae84b-144">您也可以 toochange hello 公用應用程式連接埠 hello 叢集部署之前。</span><span class="sxs-lookup"><span data-stu-id="ae84b-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="ae84b-145">根據預設，只有兩個公用 TCP 連接埠 （80 和 8081） 會開啟 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="ae84b-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="ae84b-146">如果您需要多個應用程式，可以修改 hello 範本中的 hello Azure 負載平衡器定義。</span><span class="sxs-lookup"><span data-stu-id="ae84b-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="ae84b-147">hello 定義會儲存在 hello 主要範本檔案 (`ServiceFabricCluster.json`)。</span><span class="sxs-lookup"><span data-stu-id="ae84b-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="ae84b-148">開啟該檔案，並搜尋 `loadBalancedAppPort`。</span><span class="sxs-lookup"><span data-stu-id="ae84b-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="ae84b-149">每個連接埠會與三個成品相關聯：</span><span class="sxs-lookup"><span data-stu-id="ae84b-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="ae84b-150">定義 hello hello 連接埠的 TCP 連接埠值的範本變數：</span><span class="sxs-lookup"><span data-stu-id="ae84b-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="ae84b-151">A*探查*定義頻率和時間的 hello Azure 負載平衡器會嘗試透過其中一個 tooanother toouse 特定 Service Fabric 節點失敗之前。</span><span class="sxs-lookup"><span data-stu-id="ae84b-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="ae84b-152">hello 探查是 hello 資源負載平衡器的一部分。</span><span class="sxs-lookup"><span data-stu-id="ae84b-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="ae84b-153">以下是第一個預設應用程式連接埠 hello hello 探查定義：</span><span class="sxs-lookup"><span data-stu-id="ae84b-153">Here is hello probe definition for hello first default application port:</span></span>
   
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
3. <span data-ttu-id="ae84b-154">A*負載平衡規則*，結合 hello 連接埠和 hello 探查，啟用負載平衡的一組 Service Fabric 叢集節點：</span><span class="sxs-lookup"><span data-stu-id="ae84b-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="ae84b-155">如果您計劃 toodeploy toohello 叢集 hello 應用程式需要更多連接埠，您可以將它們加入建立額外的探查和負載平衡規則定義。</span><span class="sxs-lookup"><span data-stu-id="ae84b-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="ae84b-156">如需有關如何 toowork 與 Azure 負載平衡器透過資源管理員範本，請參閱[開始建立使用範本的內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="ae84b-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="ae84b-157">使用 Visual Studio 部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="ae84b-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="ae84b-158">儲存之後所有 hello 中的必要的參數值`ServiceFabricCluster.param.dev.json`檔案中，您已準備好 toodeploy hello 範本，並建立 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae84b-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="ae84b-159">Visual Studio 方案總管] 中的 hello 資源群組專案上按一下滑鼠右鍵，然後選擇 [**部署 |新增部署...**.如果有必要，Visual Studio 會顯示 hello**部署 tooResource 群組**對話方塊，詢問您 tooauthenticate tooAzure:</span><span class="sxs-lookup"><span data-stu-id="ae84b-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![部署 tooResource 群組對話方塊][3]

<span data-ttu-id="ae84b-161">hello 對話方塊可讓您選擇 hello 叢集和新 hello 選項 toocreate 提供現有的資源管理員資源群組。</span><span class="sxs-lookup"><span data-stu-id="ae84b-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="ae84b-162">它通常使意義 toouse Service Fabric 叢集的個別資源群組。</span><span class="sxs-lookup"><span data-stu-id="ae84b-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="ae84b-163">點擊 hello 部署按鈕之後，Visual Studio 會提示您 tooconfirm hello 範本參數的值。</span><span class="sxs-lookup"><span data-stu-id="ae84b-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="ae84b-164">叫用的 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae84b-164">Hit hello **Save** button.</span></span> <span data-ttu-id="ae84b-165">一個參數並沒有持續的值： hello hello 叢集的系統管理帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="ae84b-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="ae84b-166">Visual Studio 會提示您輸入其中一個時，您會需要 tooprovide 密碼值。</span><span class="sxs-lookup"><span data-stu-id="ae84b-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="ae84b-167">從 Azure SDK 2.9 開始，Visual Studio 支援在部署期間從 **Azure 金鑰保存庫**讀取密碼。</span><span class="sxs-lookup"><span data-stu-id="ae84b-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="ae84b-168">在 [hello 範本參數] 對話方塊，請注意該 hello`adminPassword`參數文字方塊右 hello 上具有少許的 「 金鑰 」 圖示。</span><span class="sxs-lookup"><span data-stu-id="ae84b-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="ae84b-169">此圖示可讓您現有的金鑰保存庫密碼 tooselect 當做 hello hello 叢集系統管理密碼。</span><span class="sxs-lookup"><span data-stu-id="ae84b-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="ae84b-170">您只需要確定 toofirst 啟用 hello 進階存取原則中的金鑰保存庫的範本部署的 Azure 資源管理員存取權。</span><span class="sxs-lookup"><span data-stu-id="ae84b-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="ae84b-171">您可以監視 hello hello Visual Studio 輸出視窗中的 hello 部署程序的進度。</span><span class="sxs-lookup"><span data-stu-id="ae84b-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="ae84b-172">Hello 範本部署完成後，您的新叢集將會是準備 toouse ！</span><span class="sxs-lookup"><span data-stu-id="ae84b-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="ae84b-173">如果 PowerShell 永遠不會使用從您目前使用的 hello 機器 tooadminister Azure，您需要 toodo 極小的內部管理。</span><span class="sxs-lookup"><span data-stu-id="ae84b-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="ae84b-174">啟用 PowerShell 指令碼執行 hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx)命令。</span><span class="sxs-lookup"><span data-stu-id="ae84b-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="ae84b-175">開發電腦通常可接受「不受限制」原則。</span><span class="sxs-lookup"><span data-stu-id="ae84b-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="ae84b-176">決定是否從 Azure PowerShell 命令，然後執行 tooallow 診斷資料收集[ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx)或[ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx)視。</span><span class="sxs-lookup"><span data-stu-id="ae84b-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="ae84b-177">這可在範本部署期間避免不必要的提示。</span><span class="sxs-lookup"><span data-stu-id="ae84b-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="ae84b-178">如果有任何錯誤，請移至 toohello [Azure 入口網站](https://portal.azure.com/)與您部署到開啟的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ae84b-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="ae84b-179">按一下**所有設定**，然後按一下 [**部署**hello 設定] 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="ae84b-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="ae84b-180">資源群組部署失敗會在通知中留下詳細的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="ae84b-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="ae84b-181">Service Fabric 叢集需要 toomaintain 可用性節點 toobe 數目和保留狀態-參照 tooas 「 維持仲裁 」。</span><span class="sxs-lookup"><span data-stu-id="ae84b-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="ae84b-182">因此，它不是向 hello 機器 hello 叢集中的所有安全 tooshut 除非您先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ae84b-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ae84b-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae84b-183">Next steps</span></span>
* [<span data-ttu-id="ae84b-184">深入了解設定使用 hello Azure 入口網站的 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="ae84b-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="ae84b-185">深入了解如何 toomanage 及部署 Service Fabric 應用程式使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae84b-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
