---
title: "在 Azure 中的 aaaCreate Service Fabric 叢集 |Microsoft 文件"
description: "了解如何 toocreate Windows 或 Linux Service Fabric 叢集使用 PowerShell 在 Azure 中。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="b622c-103">使用 PowerShell 在 Azure 上建立安全叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="b622c-104">本教學課程告訴您如何 toocreate Service Fabric 叢集 （Windows 或 Linux） 的執行在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b622c-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="b622c-105">當您完成時，您會有叢集，您可以將應用程式部署的 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="b622c-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="b622c-106">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="b622c-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b622c-107">使用 PowerShell 在 Azure 中建立安全的 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="b622c-108">使用 X.509 憑證的安全 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="b622c-109">Toohello 叢集使用 PowerShell 連線</span><span class="sxs-lookup"><span data-stu-id="b622c-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="b622c-110">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b622c-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="b622c-111">Prerequisites</span></span>
<span data-ttu-id="b622c-112">開始進行本教學課程之前：</span><span class="sxs-lookup"><span data-stu-id="b622c-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="b622c-113">如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="b622c-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="b622c-114">安裝 hello [Service Fabric SDK 及 PowerShell 模組](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b622c-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="b622c-115">安裝 hello [Azure Powershell 模組版本 4.1 或更高版本](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="b622c-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="b622c-116">hello 遵循程序會建立單一節點 （單一虛擬機器） 預覽 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="b622c-117">取得與 hello 叢集一起建立，然後放置在金鑰保存庫的自我簽署憑證以保護 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="b622c-118">單一節點叢集無法擴充超過一部虛擬機器，並預覽叢集不能升級的 toonewer 版本。</span><span class="sxs-lookup"><span data-stu-id="b622c-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="b622c-119">導致 Service Fabric 叢集正在使用 Azure hello toocalculate 成本[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/)。</span><span class="sxs-lookup"><span data-stu-id="b622c-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="b622c-120">如需建立 Service Fabric 叢集的詳細資訊，請參閱[使用 Azure Resource Manager 來建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="b622c-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="b622c-121">建立 hello 叢集使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b622c-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="b622c-122">從 hello 下載 hello Azure Resource Manager 範本與 hello 參數檔案的本機副本[Azure Resource Manager 範本適用於 Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b622c-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="b622c-123">*azuredeploy.json* hello Azure 資源管理員範本可定義 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="b622c-124">*azuredeploy.parameters.json* toocustomize hello 叢集部署是為您的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="b622c-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="b622c-125">來自訂下列參數在 hello hello *azuredeploy.parameters.json*參數檔案：</span><span class="sxs-lookup"><span data-stu-id="b622c-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="b622c-126">參數</span><span class="sxs-lookup"><span data-stu-id="b622c-126">Parameter</span></span>       | <span data-ttu-id="b622c-127">說明</span><span class="sxs-lookup"><span data-stu-id="b622c-127">Description</span></span> | <span data-ttu-id="b622c-128">建議的值</span><span class="sxs-lookup"><span data-stu-id="b622c-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="b622c-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="b622c-129">clusterLocation</span></span> | <span data-ttu-id="b622c-130">hello Azure 地區 toowhich toodeploy hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="b622c-131">*例如 westeurope、eastasia、eastus*</span><span class="sxs-lookup"><span data-stu-id="b622c-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="b622c-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="b622c-132">clusterName</span></span>     | <span data-ttu-id="b622c-133">名稱要 toocreate 的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="b622c-134">*例如 bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="b622c-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="b622c-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="b622c-135">adminUserName</span></span>   | <span data-ttu-id="b622c-136">hello hello 叢集虛擬機器上的本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="b622c-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="b622c-137">*任何有效的 Windows Server 使用者名稱*</span><span class="sxs-lookup"><span data-stu-id="b622c-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="b622c-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="b622c-138">adminPassword</span></span>   | <span data-ttu-id="b622c-139">Hello hello 叢集虛擬機器上的本機系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="b622c-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="b622c-140">*任何有效的 Windows Server 密碼*</span><span class="sxs-lookup"><span data-stu-id="b622c-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="b622c-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="b622c-141">clusterCodeVersion</span></span> | <span data-ttu-id="b622c-142">hello Service Fabric 版本 toorun。</span><span class="sxs-lookup"><span data-stu-id="b622c-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="b622c-143">(255.255.X.255 是預覽版本)。</span><span class="sxs-lookup"><span data-stu-id="b622c-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="b622c-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="b622c-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="b622c-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="b622c-145">vmInstanceCount</span></span> | <span data-ttu-id="b622c-146">hello （可以是 1 或 3-99） 叢集中的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="b622c-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="b622c-147">**1**</span><span class="sxs-lookup"><span data-stu-id="b622c-147">**1**</span></span> | <span data-ttu-id="b622c-148">*對於預覽叢集，請僅指定一部虛擬機器*</span><span class="sxs-lookup"><span data-stu-id="b622c-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="b622c-149">開啟 PowerShell 主控台中，登入 tooAzure，並選取您想 toodeploy hello 叢集在 hello 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="b622c-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="b622c-150">建立並加密 hello 憑證 toobe Service Fabric 所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="b622c-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="b622c-151">執行下列命令的 hello 建立 hello 叢集和其憑證：</span><span class="sxs-lookup"><span data-stu-id="b622c-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="b622c-152">hello`-CertificateSubjectName`參數應符合的 hello 參數檔案中指定的 hello clusterName 參數、 以及 hello 繫結的網域 toohello Azure 區域為您選擇，例如： `clustername.eastus.cloudapp.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="b622c-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="b622c-153">一旦 hello 組態完成時，它會輸出建立在 Azure 中的 hello 叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b622c-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="b622c-154">它也會複製 hello 叢集憑證 toohello-CertificateOutputFolder 目錄上 hello 這個參數所指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="b622c-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="b622c-155">您需要此憑證 tooaccess Service Fabric 總管和檢視 hello 健全狀況的叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="b622c-156">記下您的叢集，可能會類似 toohello hello URL 下列 URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="b622c-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="b622c-157">修改 hello 憑證 （& s) 存取 Service Fabric 總管</span><span class="sxs-lookup"><span data-stu-id="b622c-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="b622c-158">按兩下 hello 憑證 tooopen hello 憑證匯入精靈。</span><span class="sxs-lookup"><span data-stu-id="b622c-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="b622c-159">使用預設設定，但請確定 toocheck hello**標示成可匯出此機碼。**</span><span class="sxs-lookup"><span data-stu-id="b622c-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="b622c-160">在 [hello] 核取方塊，**私密金鑰保護**步驟。</span><span class="sxs-lookup"><span data-stu-id="b622c-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="b622c-161">稍後在本教學課程設定 Azure 容器登錄中 tooService Fabric 叢集驗證時，visual Studio 需要 tooexport hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="b622c-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="b622c-162">現在，您可以在瀏覽器中開啟 Service Fabric Explorer。</span><span class="sxs-lookup"><span data-stu-id="b622c-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="b622c-163">toodo，瀏覽 toohello **ManagementEndpoint**供您使用網頁瀏覽器，並選取 hello 憑證儲存在您的電腦的叢集 URL。</span><span class="sxs-lookup"><span data-stu-id="b622c-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="b622c-164">由於您使用自我簽署的憑證，因此開啟 Service Fabric Explorer 時會顯示憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="b622c-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="b622c-165">在 Edge 中，您有 tooclick*詳細資料*然後 hello 和*toohello 網頁上移*連結。</span><span class="sxs-lookup"><span data-stu-id="b622c-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="b622c-166">在 Chrome 中，您有 tooclick*進階*然後 hello 和*繼續*連結。</span><span class="sxs-lookup"><span data-stu-id="b622c-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="b622c-167">如果 hello 叢集建立失敗，您永遠可以重新執行 hello 命令，就會更新已部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="b622c-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="b622c-168">如果失敗的 hello 部署的一部分建立憑證時，會產生一個新。</span><span class="sxs-lookup"><span data-stu-id="b622c-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="b622c-169">tootroubleshoot 建立叢集，請參閱[使用 Azure Resource Manager 建立 Service Fabric 叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="b622c-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="b622c-170">Toohello 安全叢集連線</span><span class="sxs-lookup"><span data-stu-id="b622c-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="b622c-171">使用 hello 與 hello Service Fabric SDK 一起安裝的 Service Fabric PowerShell 模組的 toohello 叢集連線。</span><span class="sxs-lookup"><span data-stu-id="b622c-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="b622c-172">首先，將 hello 憑證安裝到您的電腦上的 hello 目前使用者 hello 個人 (My) 存放區。</span><span class="sxs-lookup"><span data-stu-id="b622c-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="b622c-173">執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b622c-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="b622c-174">現在您已經準備就緒 tooconnect tooyour 安全叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="b622c-175">hello **Service Fabric** PowerShell 模組提供許多 cmdlet 來管理 Service Fabric 叢集、 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="b622c-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="b622c-176">使用 hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello 安全叢集。</span><span class="sxs-lookup"><span data-stu-id="b622c-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="b622c-177">hello 憑證指紋，並從上一個步驟的 hello 輸出中找到連接端點詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b622c-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="b622c-178">請檢查您已連線，且 hello 叢集狀況良好使用 hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b622c-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="b622c-179">清除資源</span><span class="sxs-lookup"><span data-stu-id="b622c-179">Clean up resources</span></span>

<span data-ttu-id="b622c-180">叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。</span><span class="sxs-lookup"><span data-stu-id="b622c-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="b622c-181">hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="b622c-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="b622c-182">登入 tooAzure，並選取您要與其 tooremove hello 叢集 hello 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="b622c-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="b622c-183">您可以找到您的訂用帳戶 ID 登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b622c-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b622c-184">刪除 hello 資源群組和所有 hello 叢集資源使用 hello[移除 AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup)。</span><span class="sxs-lookup"><span data-stu-id="b622c-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="b622c-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b622c-185">Next steps</span></span>
<span data-ttu-id="b622c-186">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="b622c-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b622c-187">在 Azure 中建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="b622c-188">使用 X.509 憑證的安全 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="b622c-189">Toohello 叢集使用 PowerShell 連線</span><span class="sxs-lookup"><span data-stu-id="b622c-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="b622c-190">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="b622c-190">Remove a cluster</span></span>

<span data-ttu-id="b622c-191">接下來，前進 toohello 如何遵循教學課程 toolearn toodeploy 現有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b622c-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b622c-192">透過 Docker Compose 部署現有的 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="b622c-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
