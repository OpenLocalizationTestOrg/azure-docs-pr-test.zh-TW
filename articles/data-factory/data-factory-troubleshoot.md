---
title: "aaaTroubleshoot Azure Data Factory 問題"
description: "了解如何使用 Azure Data Factory tootroubleshoot 問題。"
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="b1260-103">資料處理站的疑難排解</span><span class="sxs-lookup"><span data-stu-id="b1260-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="b1260-104">這篇文章提供使用 Azure Data Factory 時的問題疑難排解提示。</span><span class="sxs-lookup"><span data-stu-id="b1260-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="b1260-105">本文使用 hello 服務時不會列出所有的 hello 可能的問題，但涵蓋了某些問題和一般的疑難排解秘訣。</span><span class="sxs-lookup"><span data-stu-id="b1260-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="b1260-106">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="b1260-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="b1260-107">錯誤： hello 訂用帳戶不是已註冊的 toouse 命名空間 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="b1260-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="b1260-108">如果您收到這個錯誤，hello Azure Data Factory 的資源提供者尚未註冊您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b1260-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="b1260-109">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b1260-109">Do hello following:</span></span>

1. <span data-ttu-id="b1260-110">啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b1260-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="b1260-111">使用下列命令的 hello 的 Azure 帳戶登入 tooyour 中。</span><span class="sxs-lookup"><span data-stu-id="b1260-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="b1260-112">執行下列命令 tooregister hello Azure Data Factory 提供者的 hello。</span><span class="sxs-lookup"><span data-stu-id="b1260-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="b1260-113">問題：執行 Data Factory Cmdlet 時發生未授權錯誤</span><span class="sxs-lookup"><span data-stu-id="b1260-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="b1260-114">您可能不會使用 hello 右邊的 Azure 帳戶或訂用帳戶以 hello Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b1260-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="b1260-115">使用下列 cmdlet tooselect hello 權限以 hello Azure PowerShell 的 Azure 帳戶和訂用帳戶 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="b1260-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="b1260-116">登入-AzureRmAccount-使用 hello 權限的使用者識別碼和密碼</span><span class="sxs-lookup"><span data-stu-id="b1260-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="b1260-117">Get AzureRmSubscription-檢視所有 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1260-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="b1260-118">選取 AzureRmSubscription&lt;訂用帳戶名稱&gt;-選取 hello 右訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1260-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="b1260-119">使用 hello 同一個您可以使用 data factory toocreate hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="b1260-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="b1260-120">問題： 無法從 Azure 入口網站的 toolaunch 資料管理閘道 Express 安裝程式</span><span class="sxs-lookup"><span data-stu-id="b1260-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="b1260-121">資料管理閘道器 hello Express 安裝程式需要 Internet Explorer 或與 Microsoft ClickOnce 相容的 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b1260-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="b1260-122">Toostart hello Express 安裝程式時，執行 hello 下列其中一種動作：</span><span class="sxs-lookup"><span data-stu-id="b1260-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="b1260-123">使用 Internet Explorer 或 Microsoft ClickOnce 相容的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b1260-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="b1260-124">如果您使用 Chrome，請移至 toohello [Chrome web store](https://chrome.google.com/webstore/)、 搜尋與"ClickOnce"關鍵字、 選擇其中一個 hello ClickOnce 擴充功能，及安裝它。</span><span class="sxs-lookup"><span data-stu-id="b1260-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="b1260-125">請勿 hello 相同 Firefox （安裝增益集）。</span><span class="sxs-lookup"><span data-stu-id="b1260-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="b1260-126">按一下 hello 工具列 （三條水平線 hello 右上角） 上的開啟功能表按鈕、 按一下 附加元件、 搜尋與"ClickOnce"關鍵字，選擇其中一個 hello ClickOnce 擴充功能，並安裝它。</span><span class="sxs-lookup"><span data-stu-id="b1260-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="b1260-127">使用 hello**手動安裝**連結顯示 hello hello 入口網站中的相同刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b1260-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="b1260-128">您可以使用此方法 toodownload 安裝檔案，並手動執行它。</span><span class="sxs-lookup"><span data-stu-id="b1260-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="b1260-129">Hello 安裝成功之後，您會看到 hello 資料管理閘道組態對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b1260-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="b1260-130">複製 hello**金鑰**防止 hello 入口網站畫面並在 hello configuration manager toomanually hello 閘道註冊 hello 服務的使用。</span><span class="sxs-lookup"><span data-stu-id="b1260-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="b1260-131">問題： 失敗 tooconnect tooon 內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="b1260-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="b1260-132">啟動**資料管理閘道組態管理員**hello 閘道電腦且使用 hello**疑難排解**tootest hello 連接 tooSQL hello 閘道電腦從伺服器索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="b1260-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="b1260-133">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="b1260-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="b1260-134">問題：輸入配量永遠處於 Waiting 狀態</span><span class="sxs-lookup"><span data-stu-id="b1260-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="b1260-135">hello 配量可能處於**等候**到期 toovarious 原因的狀態。</span><span class="sxs-lookup"><span data-stu-id="b1260-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="b1260-136">其中一個 hello 的常見原因是該 hello**外部**屬性未設定太**true**。</span><span class="sxs-lookup"><span data-stu-id="b1260-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="b1260-137">Azure Data Factory 外部產生的 hello 範圍的任何資料集應該用來標記**外部**屬性。</span><span class="sxs-lookup"><span data-stu-id="b1260-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="b1260-138">此屬性會指出 hello 資料的外部和任何管線內 hello 資料處理站不支援。</span><span class="sxs-lookup"><span data-stu-id="b1260-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="b1260-139">hello 資料配量會標示為**準備**一旦 hello 資料可在 hello 個別存放區中。</span><span class="sxs-lookup"><span data-stu-id="b1260-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="b1260-140">請參閱下列範例 hello 使用量的 hello hello**外部**屬性。</span><span class="sxs-lookup"><span data-stu-id="b1260-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="b1260-141">您可以選擇性地指定**externalData*** 當您將外部 tootrue。</span><span class="sxs-lookup"><span data-stu-id="b1260-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="b1260-142">如需此屬性的詳細資訊，請參閱 [資料集](data-factory-create-datasets.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="b1260-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="b1260-143">tooresolve hello 錯誤、 新增 hello**外部**屬性和選用的 hello **externalData**區段 toohello JSON 定義的 hello 輸入資料表，並重新建立 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b1260-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="b1260-144">問題：混合式複製作業失敗</span><span class="sxs-lookup"><span data-stu-id="b1260-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="b1260-145">請參閱[閘道問題的疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)的 tootroubleshoot 問題複製至 azure 或從內部部署資料存放區使用的步驟 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="b1260-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="b1260-146">問題：隨選 HDInsight 佈建失敗</span><span class="sxs-lookup"><span data-stu-id="b1260-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="b1260-147">使用型別 HDInsightOnDemand 連結的服務時，您會需要 toospecify linkedServiceName 指向 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b1260-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="b1260-148">資料 Factory 服務會隨 HDInsight 叢集使用此儲存體 toostore 記錄並支援檔案。</span><span class="sxs-lookup"><span data-stu-id="b1260-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="b1260-149">有時在隨選 HDInsight 叢集的佈建失敗並 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="b1260-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="b1260-150">此錯誤通常表示 hello hello hello linkedServiceName 中指定的儲存體帳戶的位置不在 hello 相同資料中心位置發生 hello HDInsight 佈建的位置。</span><span class="sxs-lookup"><span data-stu-id="b1260-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="b1260-151">範例： 如果您的 data factory 是在美國西部且 hello Azure 儲存體位於美國東部、 hello 美國西部的依需求佈建失敗。</span><span class="sxs-lookup"><span data-stu-id="b1260-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="b1260-152">此外，還有第二個的 JSON 屬性 additionalLinkedServiceNames，可供隨選 HDInsight 中指定其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1260-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="b1260-153">這些額外的連結儲存體帳戶應為 hello 的 hello 相同 hello HDInsight 叢集，或它的位置失敗時相同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="b1260-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="b1260-154">問題：自訂 .NET 活動失敗</span><span class="sxs-lookup"><span data-stu-id="b1260-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="b1260-155">如需詳細步驟，請參閱 [偵錯具有自訂活動的管線](data-factory-use-custom-activities.md#troubleshoot-failures) 。</span><span class="sxs-lookup"><span data-stu-id="b1260-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="b1260-156">使用 Azure 入口網站 tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="b1260-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="b1260-157">使用入口網站刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="b1260-157">Using portal blades</span></span>
<span data-ttu-id="b1260-158">請參閱 [監視管線](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 以取得步驟。</span><span class="sxs-lookup"><span data-stu-id="b1260-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="b1260-159">使用監視及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="b1260-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="b1260-160">如需詳細資訊，請參閱 [使用監視及管理應用程式，來監視及管理 Data Factory 管線](data-factory-monitor-manage-app.md) 。</span><span class="sxs-lookup"><span data-stu-id="b1260-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="b1260-161">使用 Azure PowerShell tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="b1260-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="b1260-162">使用 Azure PowerShell tootroubleshoot 錯誤</span><span class="sxs-lookup"><span data-stu-id="b1260-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="b1260-163">如需詳細資料，請參閱 [使用 Azure PowerShell 監視 Data Factory 管線](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) 。</span><span class="sxs-lookup"><span data-stu-id="b1260-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
