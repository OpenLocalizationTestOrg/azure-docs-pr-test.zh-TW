---
title: "使用範本建立 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Resource Manager 範本建立 HDInsight 的叢集"
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="1c81a-103">使用 Resource Manager 範本在 HDInsight 中建立 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="1c81a-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="1c81a-104">在本文中，您會學習使用 Azure Resource Manager 範本建立 Azure HDInsight 叢集的數種方式。</span><span class="sxs-lookup"><span data-stu-id="1c81a-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="1c81a-105">如需詳細資訊，請參閱 [使用 Azure Resource Manager 範本部署應用程式](../azure-resource-manager/resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="1c81a-106">若要了解其他叢集建立工具和功能，請按一下此頁面頂端的索引標籤選取器，或參閱[叢集建立方法](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c81a-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c81a-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1c81a-108">若要依照本文中的指示，您將需要：</span><span class="sxs-lookup"><span data-stu-id="1c81a-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="1c81a-109">[Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1c81a-110">Azure PowerShell 和/或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="1c81a-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="1c81a-111">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1c81a-111">Resource Manager templates</span></span>
<span data-ttu-id="1c81a-112">Resource Manager 範本可讓您輕鬆地在單一、協調的作業中為您的應用程式建立下列各項：</span><span class="sxs-lookup"><span data-stu-id="1c81a-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="1c81a-113">HDInsight 叢集和其相依資源 (例如預設的儲存體帳戶)</span><span class="sxs-lookup"><span data-stu-id="1c81a-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="1c81a-114">其他資源 (例如，使用 Apache Sqoop 的 Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="1c81a-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="1c81a-115">在範本中，您會定義應用程式所需的資源。</span><span class="sxs-lookup"><span data-stu-id="1c81a-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="1c81a-116">您也可以指定部署參數，以便為不同的環境輸入值。</span><span class="sxs-lookup"><span data-stu-id="1c81a-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="1c81a-117">範本由 JSON 與運算式所組成，可讓您用來為部署建構值。</span><span class="sxs-lookup"><span data-stu-id="1c81a-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="1c81a-118">您可以在 [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/?term=hdinsight)中找到 HDInsight 範本範例。</span><span class="sxs-lookup"><span data-stu-id="1c81a-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="1c81a-119">使用跨平台 [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) (具有 [Resource Manager 擴充功能](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools)) 或文字編輯器，將範本儲存至您工作站上的檔案。</span><span class="sxs-lookup"><span data-stu-id="1c81a-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="1c81a-120">您會了解如何使用各種方法來呼叫此範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="1c81a-121">如需 Resource Manager 範本的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="1c81a-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="1c81a-122">編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1c81a-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="1c81a-123">使用 Azure Resource Manager 範本部署應用程式</span><span class="sxs-lookup"><span data-stu-id="1c81a-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="1c81a-124">產生範本</span><span class="sxs-lookup"><span data-stu-id="1c81a-124">Generate templates</span></span>

<span data-ttu-id="1c81a-125">使用 Azure 入口網站，您可以設定叢集的所有屬性、儲存範本，然後加以部署。</span><span class="sxs-lookup"><span data-stu-id="1c81a-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="1c81a-126">之後您可以重複使用範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-126">You can then reuse the template.</span></span>

<span data-ttu-id="1c81a-127">**使用 Azure 入口網站產生範本**</span><span class="sxs-lookup"><span data-stu-id="1c81a-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="1c81a-128">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c81a-129">按一下左側功能表上的 [新增]、[智慧 + 分析]，然後按一下 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="1c81a-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="1c81a-130">遵循指示輸入屬性。</span><span class="sxs-lookup"><span data-stu-id="1c81a-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="1c81a-131">您可以使用 [快速建立] 或 [自訂] 選項。</span><span class="sxs-lookup"><span data-stu-id="1c81a-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="1c81a-132">在 [摘要] 索引標籤中，按一下 [下載範本和參數]：</span><span class="sxs-lookup"><span data-stu-id="1c81a-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="1c81a-134">您會看到範本檔案、參數檔案，以及用來部署範本的程式碼範例的清單：</span><span class="sxs-lookup"><span data-stu-id="1c81a-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![HDInsight Hadoop 會建立叢集 Resource Manager 範本下載選項](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="1c81a-136">從這裡開始，您可以下載範本、將它儲存到您的範本庫或部署範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="1c81a-137">若要存取範本庫中的範本，按一下左側窗格中的 [更多服務]，然後按一下 [範本] \(位於 [其他] 類別下方)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="1c81a-138">範本和參數檔必須一起使用。</span><span class="sxs-lookup"><span data-stu-id="1c81a-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="1c81a-139">否則，您可能會得到非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="1c81a-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="1c81a-140">例如，預設的 **clusterKind** 屬性值一定是 **hadoop** (不論在下載範本之前您所指定的內容為何)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="1c81a-141">使用 PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="1c81a-141">Deploy with PowerShell</span></span>

<span data-ttu-id="1c81a-142">此程序會在 HDInsight 中建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c81a-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="1c81a-143">將[附錄](#appx-a-arm-template)中的 JSON 檔案儲存到您的工作站。</span><span class="sxs-lookup"><span data-stu-id="1c81a-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="1c81a-144">在 PowerShell 指令碼中，檔案名稱是 `C:\HDITutorials-ARM\hdinsight-arm-template.json`。</span><span class="sxs-lookup"><span data-stu-id="1c81a-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="1c81a-145">視需要設定參數和變數。</span><span class="sxs-lookup"><span data-stu-id="1c81a-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="1c81a-146">使用下列 PowerShell 指令碼執行範本：</span><span class="sxs-lookup"><span data-stu-id="1c81a-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="1c81a-147">PowerShell 指令碼只會設定叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1c81a-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="1c81a-148">儲存體帳戶名稱是硬式編碼於範本中。</span><span class="sxs-lookup"><span data-stu-id="1c81a-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="1c81a-149">系統會提示您輸入叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1c81a-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="1c81a-150">(預設的使用者名稱為 **admin**。)也會提示您輸入 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1c81a-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="1c81a-151">(預設的 SSH 使用者名稱為 **sshuser**。)</span><span class="sxs-lookup"><span data-stu-id="1c81a-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="1c81a-152">如需詳細資訊，請參閱[使用 PowerShell 進行部署](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="1c81a-153">使用 CLI 部署</span><span class="sxs-lookup"><span data-stu-id="1c81a-153">Deploy with CLI</span></span>
<span data-ttu-id="1c81a-154">下列範例會使用 Azure 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="1c81a-155">它會藉由呼叫 Resource Manager 範本來建立叢集和其依存的儲存體帳戶與容器：</span><span class="sxs-lookup"><span data-stu-id="1c81a-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="1c81a-156">系統會提示您輸入：</span><span class="sxs-lookup"><span data-stu-id="1c81a-156">You are prompted to enter:</span></span>
* <span data-ttu-id="1c81a-157">叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1c81a-157">The cluster name.</span></span>
* <span data-ttu-id="1c81a-158">叢集使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1c81a-158">The cluster user password.</span></span> <span data-ttu-id="1c81a-159">(預設的使用者名稱為 **admin**。)</span><span class="sxs-lookup"><span data-stu-id="1c81a-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="1c81a-160">SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="1c81a-160">The SSH user password.</span></span> <span data-ttu-id="1c81a-161">(預設的 SSH 使用者名稱為 **sshuser**。)</span><span class="sxs-lookup"><span data-stu-id="1c81a-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="1c81a-162">下列程式碼提供內嵌參數：</span><span class="sxs-lookup"><span data-stu-id="1c81a-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="1c81a-163">使用 REST API 部署</span><span class="sxs-lookup"><span data-stu-id="1c81a-163">Deploy with the REST API</span></span>
<span data-ttu-id="1c81a-164">請參閱 [使用 REST API 進行部署](../azure-resource-manager/resource-group-template-deploy-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="1c81a-165">透過 Visual Studio 部署</span><span class="sxs-lookup"><span data-stu-id="1c81a-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="1c81a-166">使用 Visual Studio 來透過使用者介面建立資源群組專案，並將其部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1c81a-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="1c81a-167">您選取要包含在您的專案中的資源類型。</span><span class="sxs-lookup"><span data-stu-id="1c81a-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="1c81a-168">這些資源會自動新增至 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="1c81a-169">該專案也提供 PowerShell 指令碼來部署範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="1c81a-170">如需搭配資源群組使用 Visual Studio 的簡介，請參閱 [透過 Visual Studio 建立和部署 Azure 資源群組](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="1c81a-171">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1c81a-171">Troubleshoot</span></span>

<span data-ttu-id="1c81a-172">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c81a-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c81a-173">Next steps</span></span>
<span data-ttu-id="1c81a-174">在本文中，您學到幾種建立 HDInsight 叢集的方法。</span><span class="sxs-lookup"><span data-stu-id="1c81a-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="1c81a-175">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="1c81a-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="1c81a-176">如需透過 .NET 用戶端程式庫部署資源的範例，請參閱[使用 .NET 程式庫與範本部署資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1c81a-177">如需部署應用程式的深入範例，請參閱 [透過可預測方式在 Azure 中佈建和部署微服務](../app-service-web/app-service-deploy-complex-application-predictably.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="1c81a-178">如需將您的方案部署到不同環境的指引，請參閱 [Microsoft Azure 中的開發和測試環境](../solution-dev-test-environments.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="1c81a-179">若要了解 Azure Resource Manager 範本的區段，請參閱 [編寫範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1c81a-180">如需可在 Azure Resource Manager 範本中使用的函式清單，請參閱 [範本函式](../azure-resource-manager/resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="1c81a-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="1c81a-181">附錄：用來建立 Hadoop 叢集的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1c81a-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="1c81a-182">下列 Azure Resource Manager 範本會建立 Linux 型 Hadoop 叢集與相依的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c81a-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="1c81a-183">此範例包括 Hive 中繼存放區和 Oozie 中繼存放區的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="1c81a-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="1c81a-184">請在使用範本之前先移除區段或設定區段。</span><span class="sxs-lookup"><span data-stu-id="1c81a-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="1c81a-185">附錄：用來建立 Spark 叢集的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1c81a-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="1c81a-186">本節提供您可以用來建立 HDInsight Spark 叢集的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="1c81a-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="1c81a-187">此範本包含 `spark-defaults` 和 `spark-thrift-sparkconf` (適用於 Spark 1.6 叢集) 與 `spark2-defaults` 和 `spark2-thrift-sparkconf` (適用於 Spark 2 叢集) 的設定。</span><span class="sxs-lookup"><span data-stu-id="1c81a-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="1c81a-188">此外，HDInsight 會根據叢集大小計算並進行設定，例如`spark.executor.instances`、`spark.executor.memory` 和 `spark.executor.cores`。</span><span class="sxs-lookup"><span data-stu-id="1c81a-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="1c81a-189">如果您將區段中任何一個參數設定為範本本身的一部分，HDInsight 不會計算及設定相同區段的其他參數。</span><span class="sxs-lookup"><span data-stu-id="1c81a-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="1c81a-190">例如，參數 `spark.executor.instances` 是在 `spark-defaults` 設定中。</span><span class="sxs-lookup"><span data-stu-id="1c81a-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="1c81a-191">如果您在 `spark-defaults` 設定中設定其他參數 (例如，`spark.yarn.exector.memoryOverhead`)，HDInsight 也不會計算及設定 `spark.executor.instances` 參數。</span><span class="sxs-lookup"><span data-stu-id="1c81a-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
