---
title: "Azure 資料處理站的疑難排解"
description: "了解如何使用 Azure Data Factory 進行問題的疑難排解。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="6c898-103">資料處理站的疑難排解</span><span class="sxs-lookup"><span data-stu-id="6c898-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="6c898-104">這篇文章提供使用 Azure Data Factory 時的問題疑難排解提示。</span><span class="sxs-lookup"><span data-stu-id="6c898-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="6c898-105">這篇文章並未列出使用服務時的所有可能問題，但是涵蓋部分問題和一般疑難排解提示。</span><span class="sxs-lookup"><span data-stu-id="6c898-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="6c898-106">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="6c898-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="6c898-107">錯誤︰訂用帳戶未註冊為使用命名空間 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="6c898-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="6c898-108">如果您收到此錯誤，Azure Data Factory 資源提供者尚未在您的電腦上註冊。</span><span class="sxs-lookup"><span data-stu-id="6c898-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="6c898-109">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6c898-109">Do the following:</span></span>

1. <span data-ttu-id="6c898-110">啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6c898-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="6c898-111">使用下列命令來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="6c898-112">執行下列命令以註冊 Azure Data Factory 提供者。</span><span class="sxs-lookup"><span data-stu-id="6c898-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="6c898-113">問題：執行 Data Factory Cmdlet 時發生未授權錯誤</span><span class="sxs-lookup"><span data-stu-id="6c898-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="6c898-114">您在 Azure PowerShell 中可能未使用正確的 Azure 帳戶或訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="6c898-115">請使用下列 Cmdlet 來選取要用於 Azure PowerShell 的正確 Azure 帳戶和訂用帳戶帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="6c898-116">Login-AzureRmAccount - 使用正確的使用者識別碼和密碼</span><span class="sxs-lookup"><span data-stu-id="6c898-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="6c898-117">Get-AzureRmSubscription - 檢視帳戶的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="6c898-118">Select-AzureRmSubscription &lt;訂用帳戶名稱&gt; - 選取正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="6c898-119">請使用您在 Azure 入口網站上用來建立 Data Factory 的相同帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="6c898-120">問題：無法從 Azure 入口網站啟動「資料管理閘道快速安裝」</span><span class="sxs-lookup"><span data-stu-id="6c898-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="6c898-121">資料管理閘道的快速安裝需要有 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6c898-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="6c898-122">如果無法啟動快速安裝，請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="6c898-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="6c898-123">使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6c898-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="6c898-124">如果您使用 Chrome，請移至 [Chrome 線上應用程式商店](https://chrome.google.com/webstore/)，使用關鍵字 "ClickOnce" 進行搜尋，選擇其中一個 ClickOnce 擴充功能並安裝。</span><span class="sxs-lookup"><span data-stu-id="6c898-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="6c898-125">針對 Firefox 進行相同的操作 (安裝附加元件)。</span><span class="sxs-lookup"><span data-stu-id="6c898-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="6c898-126">按一下工具列上的 [開啟功能表] 按鈕 (右上角的三條水平線)，按一下 [附加元件]，以「ClickOnce」關鍵字進行搜尋，選擇其中一個 ClickOnce 延伸模組並安裝。</span><span class="sxs-lookup"><span data-stu-id="6c898-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="6c898-127">使用入口網站中相同刀鋒視窗上顯示的 [手動安裝] 連結。</span><span class="sxs-lookup"><span data-stu-id="6c898-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="6c898-128">您可以使用這個方法來下載安裝檔案，然後手動執行它。</span><span class="sxs-lookup"><span data-stu-id="6c898-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="6c898-129">安裝成功之後，您會看到 [資料管理閘道組態] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6c898-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="6c898-130">從入口網站畫面複製**金鑰**，並且在組態管理員中使用它來手動向服務註冊閘道器。</span><span class="sxs-lookup"><span data-stu-id="6c898-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="6c898-131">問題：無法連線到內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="6c898-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="6c898-132">在閘道器機器上啟動 [資料管理閘道組態管理員]，使用 [疑難排解] 索引標籤以測試從閘道器機器到 SQL Server 的連接。</span><span class="sxs-lookup"><span data-stu-id="6c898-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="6c898-133">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="6c898-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="6c898-134">問題：輸入配量永遠處於 Waiting 狀態</span><span class="sxs-lookup"><span data-stu-id="6c898-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="6c898-135">配量可能因各種原因而處於**等候中**狀態。</span><span class="sxs-lookup"><span data-stu-id="6c898-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="6c898-136">其中一個常見的原因是 **external** 屬性未設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="6c898-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="6c898-137">在 Azure Data Factory 範圍外產生的任何資料集，都應該標示 **external** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6c898-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="6c898-138">此屬性可指出資料為外部資料，並未受到 Data Factory 內的任何管線支持。</span><span class="sxs-lookup"><span data-stu-id="6c898-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="6c898-139">一旦資料在個別的存放區可用，資料配量就會標示為 [就緒]。</span><span class="sxs-lookup"><span data-stu-id="6c898-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="6c898-140">關於 **external** 屬性的用法，請參閱下列範例。</span><span class="sxs-lookup"><span data-stu-id="6c898-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="6c898-141">當您將 external 設定為 true 時，可以視需要指定 **externalData***。</span><span class="sxs-lookup"><span data-stu-id="6c898-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="6c898-142">如需此屬性的詳細資訊，請參閱 [資料集](data-factory-create-datasets.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="6c898-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="6c898-143">若要解決這個錯誤，請將 **external** 屬性和選用 **externalData** 區段加入輸入資料表的 JSON 定義，並重新建立資料表。</span><span class="sxs-lookup"><span data-stu-id="6c898-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="6c898-144">問題：混合式複製作業失敗</span><span class="sxs-lookup"><span data-stu-id="6c898-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="6c898-145">請參閱[針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)以取得對於使用資料管理閘道複製到/自內部部署資料存放區的問題的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="6c898-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="6c898-146">問題：隨選 HDInsight 佈建失敗</span><span class="sxs-lookup"><span data-stu-id="6c898-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="6c898-147">使用 HDInsightOnDemand 類型的連結服務時，您必須指定指向 Azure Blob 儲存體的 linkedServiceName。</span><span class="sxs-lookup"><span data-stu-id="6c898-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="6c898-148">Data Factory 服務會使用此儲存體來儲存記錄檔和您的隨選 HDInsight 叢集的支援檔案。</span><span class="sxs-lookup"><span data-stu-id="6c898-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="6c898-149">有時候隨選 HDInsight 叢集的佈建會失敗，並且有下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="6c898-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="6c898-150">此錯誤通常表示 linkedServiceName 中指定的儲存體帳戶的位置，與進行 HDInsight 佈建的資料中心位置不同。</span><span class="sxs-lookup"><span data-stu-id="6c898-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="6c898-151">範例︰如果您的 Data Factory 在美國西部，而 Azure 儲存體在美國東部，則隨選佈建會在美國西部發生失敗。</span><span class="sxs-lookup"><span data-stu-id="6c898-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="6c898-152">此外，還有第二個的 JSON 屬性 additionalLinkedServiceNames，可供隨選 HDInsight 中指定其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c898-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="6c898-153">這些其他的連結儲存體帳戶應該與 HDInsight 叢集位於相同位置，否則會因相同的錯誤而發生失敗。</span><span class="sxs-lookup"><span data-stu-id="6c898-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="6c898-154">問題：自訂 .NET 活動失敗</span><span class="sxs-lookup"><span data-stu-id="6c898-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="6c898-155">如需詳細步驟，請參閱 [偵錯具有自訂活動的管線](data-factory-use-custom-activities.md#troubleshoot-failures) 。</span><span class="sxs-lookup"><span data-stu-id="6c898-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="6c898-156">使用 Azure 入口網站進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6c898-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="6c898-157">使用入口網站刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="6c898-157">Using portal blades</span></span>
<span data-ttu-id="6c898-158">請參閱 [監視管線](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 以取得步驟。</span><span class="sxs-lookup"><span data-stu-id="6c898-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="6c898-159">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="6c898-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="6c898-160">如需詳細資訊，請參閱 [使用監視及管理應用程式，來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md) 。</span><span class="sxs-lookup"><span data-stu-id="6c898-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="6c898-161">使用 Azure PowerShell 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6c898-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="6c898-162">使用 Azure PowerShell 對錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6c898-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="6c898-163">如需詳細資料，請參閱 [使用 Azure PowerShell 監視 Data Factory 管線](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) 。</span><span class="sxs-lookup"><span data-stu-id="6c898-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
