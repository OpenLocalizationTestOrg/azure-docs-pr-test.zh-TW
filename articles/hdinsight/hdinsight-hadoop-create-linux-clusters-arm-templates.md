---
title: "使用範本-Azure HDInsight 叢集的 aaaCreate Hadoop |Microsoft 文件"
description: "了解 hdinsight toocreate 叢集使用的資源管理員範本如何"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="1155e-103">使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="1155e-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="1155e-104">在本文中，您了解幾個方式 toocreate Azure HDInsight 叢集的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="1155e-105">如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="1155e-106">toolearn 有關其他叢集建立工具和功能，按一下 [hello] 索引標籤選取器在 hello 或頂端的這個頁面，請參閱[叢集建立方法](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods)。</span><span class="sxs-lookup"><span data-stu-id="1155e-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1155e-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="1155e-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1155e-108">toofollow hello 本文中的指示，您將需要：</span><span class="sxs-lookup"><span data-stu-id="1155e-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="1155e-109">[Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="1155e-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1155e-110">Azure PowerShell 和/或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="1155e-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="1155e-111">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1155e-111">Resource Manager templates</span></span>
<span data-ttu-id="1155e-112">資源管理員範本可讓應用程式是單一的協調作業，在下列簡單 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="1155e-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="1155e-113">HDInsight 叢集和其相依的資源 （例如 hello 預設儲存體帳戶）</span><span class="sxs-lookup"><span data-stu-id="1155e-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="1155e-114">其他資源 （例如 Azure SQL Database toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="1155e-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="1155e-115">在 hello 範本中，您可以定義 hello 資源所需的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1155e-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="1155e-116">您也可以指定部署參數 tooinput 值不同的環境。</span><span class="sxs-lookup"><span data-stu-id="1155e-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="1155e-117">hello 範本包含 JSON 和您使用您的部署 tooconstruct 值的運算式。</span><span class="sxs-lookup"><span data-stu-id="1155e-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="1155e-118">您可以在 [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/?term=hdinsight)中找到 HDInsight 範本範例。</span><span class="sxs-lookup"><span data-stu-id="1155e-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="1155e-119">使用跨平台[Visual Studio Code](https://code.visualstudio.com/#alt-downloads)以 hello[資源管理員延伸模組](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools)或文字編輯器 toosave hello 」 範本，您的工作站上的檔案。</span><span class="sxs-lookup"><span data-stu-id="1155e-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="1155e-120">您了解 toocall 如何 hello 範本使用不同的方法。</span><span class="sxs-lookup"><span data-stu-id="1155e-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="1155e-121">如需有關資源管理員範本的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1155e-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="1155e-122">編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1155e-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="1155e-123">使用 Azure Resource Manager 範本部署應用程式</span><span class="sxs-lookup"><span data-stu-id="1155e-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="1155e-124">產生範本</span><span class="sxs-lookup"><span data-stu-id="1155e-124">Generate templates</span></span>

<span data-ttu-id="1155e-125">藉由使用 hello Azure 入口網站，您可以設定叢集的所有 hello 內容，並儲存 hello 範本後再進行部署。</span><span class="sxs-lookup"><span data-stu-id="1155e-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="1155e-126">然後，您可以重複使用 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-126">You can then reuse hello template.</span></span>

<span data-ttu-id="1155e-127">**toogenerate 使用 hello Azure 入口網站的範本**</span><span class="sxs-lookup"><span data-stu-id="1155e-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="1155e-128">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1155e-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1155e-129">按一下**新增**hello 左窗格中，按一下 **智慧 + 分析**，然後按一下 **HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="1155e-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="1155e-130">遵循 hello 指示 tooenter 屬性。</span><span class="sxs-lookup"><span data-stu-id="1155e-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="1155e-131">您可以使用任一 hello**快速建立**或 hello**自訂**選項。</span><span class="sxs-lookup"><span data-stu-id="1155e-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="1155e-132">在 hello**摘要**索引標籤上，按一下 **下載範本和參數**:</span><span class="sxs-lookup"><span data-stu-id="1155e-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="1155e-134">您會看到一份 hello 範本檔案中，參數檔案的程式碼範例使用 toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="1155e-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載選項](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="1155e-136">從這裡，您可以下載 hello 範本、 將它儲存 tooyour 樣板程式庫或部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="1155e-137">tooaccess 範本，以在程式庫中，按一下**更多服務**從 hello 左的功能表，然後再按一下**範本**(下 hello**其他**類別)。</span><span class="sxs-lookup"><span data-stu-id="1155e-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="1155e-138">必須同時使用 hello 範本和參數檔案。</span><span class="sxs-lookup"><span data-stu-id="1155e-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="1155e-139">否則，您可能會得到非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="1155e-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="1155e-140">比方說，hello 預設**clusterKind**屬性值一律是**hadoop**，儘管您之前，指定您下載 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="1155e-141">使用 PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="1155e-141">Deploy with PowerShell</span></span>

<span data-ttu-id="1155e-142">此程序會在 HDInsight 中建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="1155e-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="1155e-143">將 hello JSON 檔案儲存在 hello[附錄](#appx-a-arm-template)tooyour 工作站。</span><span class="sxs-lookup"><span data-stu-id="1155e-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="1155e-144">Hello PowerShell 指令碼，在 hello 檔案名稱是`C:\HDITutorials-ARM\hdinsight-arm-template.json`。</span><span class="sxs-lookup"><span data-stu-id="1155e-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="1155e-145">視需要設定 hello 參數和變數。</span><span class="sxs-lookup"><span data-stu-id="1155e-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="1155e-146">使用下列 PowerShell 指令碼的 hello 執行 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="1155e-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="1155e-147">hello PowerShell 指令碼會設定 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1155e-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="1155e-148">hello 儲存體帳戶名稱是硬式編碼 hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="1155e-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="1155e-149">您已提示的 tooenter hello 叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1155e-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="1155e-150">(hello 預設使用者名稱是**admin**。)您也會提示的 tooenter hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1155e-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="1155e-151">(hello 預設 SSH 使用者名稱是**sshuser**。)</span><span class="sxs-lookup"><span data-stu-id="1155e-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="1155e-152">如需詳細資訊，請參閱[使用 PowerShell 進行部署](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)。</span><span class="sxs-lookup"><span data-stu-id="1155e-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="1155e-153">使用 CLI 部署</span><span class="sxs-lookup"><span data-stu-id="1155e-153">Deploy with CLI</span></span>
<span data-ttu-id="1155e-154">hello 下列範例會使用 Azure 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="1155e-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="1155e-155">它會藉由呼叫 Resource Manager 範本來建立叢集和其依存的儲存體帳戶與容器：</span><span class="sxs-lookup"><span data-stu-id="1155e-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="1155e-156">提示的 tooenter︰</span><span class="sxs-lookup"><span data-stu-id="1155e-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="1155e-157">hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1155e-157">hello cluster name.</span></span>
* <span data-ttu-id="1155e-158">hello 叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1155e-158">hello cluster user password.</span></span> <span data-ttu-id="1155e-159">(hello 預設使用者名稱是**admin**。)</span><span class="sxs-lookup"><span data-stu-id="1155e-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="1155e-160">hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1155e-160">hello SSH user password.</span></span> <span data-ttu-id="1155e-161">(hello 預設 SSH 使用者名稱是**sshuser**。)</span><span class="sxs-lookup"><span data-stu-id="1155e-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="1155e-162">下列程式碼的 hello 提供內嵌參數：</span><span class="sxs-lookup"><span data-stu-id="1155e-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="1155e-163">部署以 hello REST API</span><span class="sxs-lookup"><span data-stu-id="1155e-163">Deploy with hello REST API</span></span>
<span data-ttu-id="1155e-164">請參閱[hello REST API 使用部署](../azure-resource-manager/resource-group-template-deploy-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="1155e-165">透過 Visual Studio 部署</span><span class="sxs-lookup"><span data-stu-id="1155e-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="1155e-166">使用 Visual Studio toocreate 資源群組專案，並將其部署 tooAzure 透過 hello 使用者介面。</span><span class="sxs-lookup"><span data-stu-id="1155e-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="1155e-167">您可以選取資源 tooinclude hello 類型在專案中。</span><span class="sxs-lookup"><span data-stu-id="1155e-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="1155e-168">這些資源會自動加入 toohello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="1155e-169">hello 專案也提供 PowerShell 指令碼 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1155e-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="1155e-170">如簡介 toousing Visual Studio 與資源群組，請參閱[建立和部署 Azure 資源群組，透過 Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="1155e-171">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1155e-171">Troubleshoot</span></span>

<span data-ttu-id="1155e-172">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="1155e-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1155e-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1155e-173">Next steps</span></span>
<span data-ttu-id="1155e-174">在本文中，您已經學會數種方式 toocreate 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1155e-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="1155e-175">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1155e-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="1155e-176">如需部署透過 hello.NET 用戶端程式庫資源的範例，請參閱[使用.NET 程式庫和範本部署資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1155e-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1155e-177">如需部署應用程式的深入範例，請參閱 [透過可預測方式在 Azure 中佈建和部署微服務](../app-service-web/app-service-deploy-complex-application-predictably.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="1155e-178">如需部署解決方案 toodifferent 環境需求的指引，請參閱[Microsoft Azure 中的開發和測試環境](../solution-dev-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="1155e-179">toolearn 關於 hello 區段 hello Azure 資源管理員範本，請參閱[撰寫樣板](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1155e-180">如需您可以使用 Azure Resource Manager 範本中的 hello 函式的清單，請參閱[樣板函式](../azure-resource-manager/resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="1155e-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="1155e-181">附錄： 資源管理員範本 toocreate Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="1155e-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="1155e-182">hello 下列 Azure 資源管理員範本會建立以 Linux 為基礎的 Hadoop 叢集與 hello 相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1155e-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1155e-183">此範例包括 Hive 中繼存放區和 Oozie 中繼存放區的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="1155e-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="1155e-184">移除 hello 區段，或使用 hello 範本之前設定 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="1155e-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="1155e-185">附錄： 資源管理員範本 toocreate Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="1155e-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="1155e-186">本節提供資源管理員範本，您可以使用 toocreate HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="1155e-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="1155e-187">此範本包含 `spark-defaults` 和 `spark-thrift-sparkconf` (適用於 Spark 1.6 叢集) 與 `spark2-defaults` 和 `spark2-thrift-sparkconf` (適用於 Spark 2 叢集) 的設定。</span><span class="sxs-lookup"><span data-stu-id="1155e-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="1155e-188">此外 toothis，HDInsight 計算，並設定組態，例如`spark.executor.instances`， `spark.executor.memory`，和`spark.executor.cores`根據 hello 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="1155e-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="1155e-189">如果您設定任何一個參數區段中 hello 範本本身的一部分，HDInsight 不計算，設定 hello hello 的其他參數相同的區段。</span><span class="sxs-lookup"><span data-stu-id="1155e-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="1155e-190">例如，參數`spark.executor.instances`處於 hello`spark-defaults`組態。</span><span class="sxs-lookup"><span data-stu-id="1155e-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="1155e-191">如果您設定另一個參數 (例如， `spark.yarn.exector.memoryOverhead`) 在 hello`spark-defaults`組態中，HDInsight 不會計算和設定 hello`spark.executor.instances`參數以及。</span><span class="sxs-lookup"><span data-stu-id="1155e-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
