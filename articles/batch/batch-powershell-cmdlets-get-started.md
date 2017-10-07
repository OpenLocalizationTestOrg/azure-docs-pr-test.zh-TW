---
title: "Azure 批次開始使用 PowerShell aaaGet |Microsoft 文件"
description: "快速介紹 toohello Azure PowerShell cmdlet，您可以使用 toomanage 批次的資源。"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>使用 PowerShell Cmdlet 管理 Batch 資源

以 hello Azure 批次的 PowerShell cmdlet，您可以執行，並編寫指令碼的 hello 許多相同的工作，當您執行以 hello 批次 Api hello Azure 入口網站和 hello Azure 命令列介面 (CLI)。 這是您可以使用 toomanage 批次帳戶，並使用您的批次資源，例如集區、 工作和工作的快速簡介 toohello cmdlet。

如需的批次 cmdlet，以及詳細的 cmdlet 語法的完整清單，請參閱 hello [Azure 批次指令程式參考](/powershell/module/azurerm.batch/#batch)。

本文是根據 Azure PowerShell 3.0.0 版中的 Cmdlet 所撰寫。 我們建議您更新您的 Azure PowerShell 經常 tootake 的服務更新和增強功能的優點。

## <a name="prerequisites"></a>必要條件
執行下列作業 toouse Azure PowerShell toomanage hello 批次資源。

* [安裝並設定 Azure PowerShell](/powershell/azure/overview)
* 執行 hello**登入 AzureRmAccount** cmdlet tooconnect tooyour 訂用帳戶 (hello hello Azure Resource Manager 模組中的 Azure 批次 cmdlet 出貨):
  
    `Login-AzureRmAccount`
* **向 hello 批次提供者命名空間**。 這項作業只需要執行 toobe**每個訂閱一次**。
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>管理 Batch 帳戶和金鑰
### <a name="create-a-batch-account"></a>建立批次帳戶：
**New-AzureRmBatchAccount** 會在指定的資源群組中建立 Batch 帳戶。 如果您還沒有資源群組，建立一個執行 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet。 指定一個 hello Azure 區域中 hello**位置**參數，例如"Central US"。 例如：

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

然後，在 hello 資源群組中，指定在 hello 帳戶的名稱建立 Batch 帳戶 <*account_name*> hello 位置和資源群組的名稱。 建立 hello 批次帳戶可能需要一些時間 toocomplete。 例如：

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> hello 批次帳戶名稱必須是唯一 toohello hello 資源群組，Azure 地區介於 3 到 24 個字元，並使用小寫字母和數字只。
> 
> 

### <a name="get-account-access-keys"></a>取得帳戶存取金鑰
**Get AzureRmBatchAccountKeys**顯示 hello Azure Batch 帳戶相關聯的存取金鑰。 例如，執行下列 tooget hello 主要和次要金鑰建立 hello 帳戶 hello。

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>產生新的存取金鑰
**New-AzureRmBatchAccountKey** 將為 Azure Batch 帳戶產生新的主要或次要帳戶金鑰。 例如，您的 Batch 帳戶的新主索引鍵 toogenerate 輸入：

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate 新的次要金鑰，指定 「 次要 」 hello **KeyType**參數。 您可以分別有 tooregenerate hello 主要和次要金鑰。
> 
> 

### <a name="delete-a-batch-account"></a>刪除 Batch 帳戶
**Remove-AzureRmBatchAccount** 將刪除 Batch 帳戶。 例如：

    Remove-AzureRmBatchAccount -AccountName <account_name>

出現提示時，請確認您要讓 tooremove hello 帳戶。 移除帳戶可能需要一些時間 toocomplete。

## <a name="create-a-batchaccountcontext-object"></a>建立 BatchAccountContext 物件
當您建立和管理批次集區、 工作、 工作和其他資源，請先建立 BatchAccountContext 物件 toostore，您的帳戶名稱和金鑰時，使用 tooauthenticate hello 批次的 PowerShell cmdlet:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

您 hello BatchAccountContext 將物件傳遞至指令程式，使用 hello **BatchContext**參數。

> [!NOTE]
> 根據預設，hello 帳戶的主索引鍵用於驗證，但是您可以藉由變更 BatchAccountContext 物件的明確地選取 hello 金鑰 toouse **KeyInUse**屬性： `$context.KeyInUse = "Secondary"`。
> 
> 

## <a name="create-and-modify-batch-resources"></a>建立和修改批次資源
使用 cmdlet，例如**新增 AzureBatchPool**，**新增 AzureBatchJob**，和**新增 AzureBatchTask** toocreate 批次帳戶下的資源。 都那里對應**Get-**和**Set-** cmdlet tooupdate hello 屬性，現有的資源和**移除-** cmdlet tooremove 資源，批次帳戶下的。

許多這些 cmdlet，在中使用時增加 toopassing BatchContext 物件，您需要 toocreate，或傳遞物件，其中包含詳細的資源設定，如 hello 下列範例所示。 請參閱 hello 詳細說明每個 cmdlet，如需其他範例。

### <a name="create-a-batch-pool"></a>建立 Batch 集區
當建立或更新的批次集區，您選取 hello 雲端服務組態或 hello 虛擬機器組態的 hello hello 上作業系統的計算節點 (請參閱[批次功能概觀](batch-api-basics.md#pool))。 如果您指定 hello 雲端服務組態，其中包含一個 hello 處理計算節點[Azure 客體 OS 版本](../cloud-services/cloud-services-guestos-update-matrix.md#releases)。 如果您指定 hello 虛擬機器組態，您可以指定 hello 的其中一個支援的 Linux 或 Windows VM 映像中所列的 hello [Azure 虛擬機器 Marketplace][vm_marketplace]，或提供自訂您已經備妥的映像。

當您執行**新增 AzureBatchPool**，傳遞 PSCloudServiceConfiguration 或 PSVirtualMachineConfiguration 物件中的 hello 作業系統設定。 例如，hello 下列 cmdlet 會建立新的批次集區大小小型運算中的節點 hello 雲端服務組態，建立映像與 hello 最新作業系統版本系列 3 (Windows Server 2012)。 在這裡，hello **CloudServiceConfiguration**參數會指定 hello *$configuration*變數作為 hello PSCloudServiceConfiguration 物件。 hello **BatchContext**參數會指定先前定義的變數*$context*為 hello BatchAccountContext 物件。

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

計算節點 hello 新集區中的 hello 目標數目取決於自動調整公式。 Hello 公式在此情況下，只是**$TargetDedicated = 4**，指出 hello hello 集區中的運算節點數目最多為 4。

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>查詢集區、作業、工作及其他詳細資料
使用 cmdlet，例如**Get AzureBatchPool**， **Get AzureBatchJob**，和**Get AzureBatchTask** tooquery 批次帳戶下建立的實體。

### <a name="query-for-data"></a>查詢資料
例如，使用**Get AzureBatchPools** toofind 程式集區。 根據預設，此查詢在您的帳戶下的所有集區，假設您已經儲存中的 hello BatchAccountContext 物件*$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>使用 OData 篩選
您可以提供的 OData 篩選器使用 hello**篩選**參數 toofind 只 hello 您感興趣的物件。 例如，您可以找到識別碼以 “myPool” 開頭的所有集區：

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

雖然這個方法比在本機管線中使用 “Where-Object” 較不具有彈性， 不過，hello 查詢取得 toohello 批次服務直接傳送，讓所有的篩選發生在 hello 伺服器端，儲存的網際網路頻寬。

### <a name="use-hello-id-parameter"></a>使用 hello Id 參數
替代 tooan OData 篩選器為 toouse hello**識別碼**參數。 識別碼"myPool 」 的特定集區的 tooquery:

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

hello**識別碼**參數僅支援完整識別碼搜尋，不使用萬用字元或 OData 樣式篩選器。

### <a name="use-hello-maxcount-parameter"></a>使用 hello MaxCount 參數
依預設，每個 Cmdlet 最多傳回 1000 個物件。 如果達到此限制，請精簡篩選 toobring 回較少的物件，或明確地設定最多使用 hello **MaxCount**參數。 例如：

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

tooremove hello 上限設定**MaxCount** too0 或更少。

### <a name="use-hello-powershell-pipeline"></a>使用 hello PowerShell 管線
批次指令程式可以利用 hello PowerShell 管線 toosend 資料之間的指令程式。 這會有相同效果與指定的參數，但具有多個實體工作的 hello。

例如，尋找和顯示您帳戶下的所有作業：

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

重新啟動集區中的每個計算節點︰

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>應用程式封裝管理
應用程式套件提供一個簡化的方式 toodeploy 應用程式 toohello 計算您的集區中的節點。 以 hello 批次的 PowerShell cmdlet，您可以上傳和管理您的 Batch 帳戶中的應用程式封裝及部署封裝版本 toocompute 節點。

**建立** 應用程式：

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**新增** 應用程式封裝︰

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

設定 hello**預設版本**hello 應用程式：

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**列出**應用程式的套件

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**刪除**應用程式套件

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**刪除**應用程式

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> 您必須先刪除所有應用程式的應用程式封裝版本，然後再刪除 hello 應用程式。 如果您嘗試 toodelete 目前具有應用程式封裝的應用程式，您會收到 '衝突' 錯誤。
> 
> 

### <a name="deploy-an-application-package"></a>部署應用程式封裝
您可以在建立集區時，指定一或多個應用程式套件以供部署。 當您在集區建立期間指定套件時，它是已部署的 tooeach 節點 hello 節點聯結集區。 重新啟動或重新安裝映像節點時，也會部署套件。

指定 hello`-ApplicationPackageReference`選項加入 hello 集區的應用程式封裝 toohello 集區的節點建立集區 toodeploy 時。 首先，建立**PSApplicationPackageReference**物件，並將它設定 hello 應用程式識別碼和封裝版本想 toodeploy toohello 集區的計算節點：

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

現在建立 hello 集區，並指定 hello 封裝參考物件，如 hello 引數 toohello`ApplicationPackageReferences`選項：

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

您可以找到更多有關應用程式封裝中[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。

> [!IMPORTANT]
> 您必須[Azure 儲存體帳戶連結](#linked-storage-account-autostorage)tooyour 批次帳戶 toouse 應用程式封裝。
> 
> 

### <a name="update-a-pools-application-packages"></a>更新集區的應用程式封裝
指派 tooan 現有集區的 tooupdate hello 應用程式首先會建立 PSApplicationPackageReference 物件具有所需的 hello 屬性 （應用程式識別碼和封裝版本）：

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

接下來，批次中收到 hello 集區、 清除任何現有的封裝、 加入我們新的封裝參考，和 hello 批次服務更新的 hello 新集區設定：

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

您現在已更新 hello 批次服務中的 hello 集區的屬性。 tooactually 部署 hello 新應用程式封裝 toocompute 節點 hello 集區中的，不過，您必須重新啟動或重新安裝映像的那些節點。 您可以使用此命令重新啟動集區中的每個節點︰

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> 您可以部署多個應用程式封裝 toohello 計算節點集區中。 如果您希望太*新增*應用程式封裝，而不是取代目前部署的 hello 封裝省略 hello`$pool.ApplicationPackageReferences.Clear()`上述列。
> 
> 

## <a name="next-steps"></a>後續步驟
* 如需詳細的 Cmdlet 語法和範例，請參閱 [Azure Batch Cmdlet 參考資料](/powershell/module/azurerm.batch/#batch)。
* 如需應用程式和批次中的應用程式套件的詳細資訊，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/