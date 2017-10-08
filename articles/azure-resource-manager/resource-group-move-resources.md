---
title: "aaaMove Azure 資源 toonew 訂用帳戶或資源群組 |Microsoft 文件"
description: "使用 Azure Resource Manager toomove 資源 tooa 新資源群組或訂用帳戶。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>移動資源 toonew 資源群組或訂用帳戶
本主題說明您如何 toomove 資源 tooeither 新訂用帳戶或新的資源群組中 hello 相同訂用帳戶。 您可以使用 hello 入口網站、 PowerShell、 Azure CLI 或 hello REST API toomove 資源。 本主題中的 hello 移動作業是使用 tooyou 不需要任何協助從 Azure 支援。

當您移動資源，也會 hello 作業期間鎖定 hello 來源群組和 hello 目標群組。 寫入和刪除作業 hello 移動作業完成之前被封鎖於 hello 資源群組。 這個鎖定表示您無法加入、 更新或刪除資源在 hello 資源群組中，但它並不表示已遭到凍結 hello 資源。 比方說，如果您移動 SQL Server 和資料庫 tooa 新資源群組，使用 hello 資料庫的應用程式就會發生任何停機時間。 仍可讀取並寫入 toohello 資料庫。

您無法變更 hello 資源的 hello 位置。 移動資源只會移動它 tooa 新資源群組。 hello 新資源群組可能會有不同的位置，但不會變更 hello 資源的 hello 位置。

> [!NOTE]
> 本文說明如何在現有的 Azure toomove 資源帳戶提供項目。 如果您真的想要 toochange 為您的 Azure 帳戶 （例如從隨用隨付 toopre 付費升級） 產品，同時繼續 toowork 與您現有的資源，請參閱[切換您的 Azure 訂用帳戶 tooanother 優惠](../billing/billing-how-to-switch-azure-offer.md)。
>
>

## <a name="checklist-before-moving-resources"></a>移動資源前的檢查清單
移動資源之前有一些重要步驟 tooperform。 藉由驗證這些條件，您可以避免錯誤。

1. hello 來源和目的地訂用帳戶必須存在於 hello 相同[Azure Active Directory 租用戶](../active-directory/active-directory-howto-tenant.md)。 這兩個訂用帳戶擁有 hello 相同 toocheck 租用戶識別碼，請使用 Azure PowerShell 或 Azure CLI。

  如果是 Azure PowerShell，請使用：

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  如果是 Azure CLI 2.0，請使用：

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  如果 hello 租用戶的識別碼 hello 來源和目的地訂用帳戶不是 hello 相同，您可以嘗試 hello 訂用帳戶的 toochange hello 目錄。 不過，這個選項是使用 tooService Microsoft 帳戶 （非組織帳戶） 登入系統管理員。 變更 hello 目錄中，登入 toohello tooattempt[傳統入口網站](https://manage.windowsazure.com/)，然後選取**設定**，選取 hello 訂用帳戶。 如果 hello**編輯目錄**圖示可用，請選取它 toochange hello 相關聯的 Azure Active Directory。

  ![編輯目錄](./media/resource-group-move-resources/edit-directory.png)

  如果找不到該圖示，您必須連絡支援 toomove hello 資源 tooa 新的租用戶。

2. hello 服務必須啟用 hello 能力 toomove 資源。 本主題列出哪些服務可實現移動資源，哪些服務無法實現移動資源。
3. 正在移動的 hello 資源的 hello 資源提供者必須登錄 hello 目的地訂用帳戶。 如果不是，您會收到錯誤，指出該 hello**訂用帳戶未註冊資源類型**。 移動資源 tooa 新訂閱時，可能會遇到這個問題，但從未使用該訂用帳戶與該資源類型。 toolearn 如何 toocheck hello 登錄狀態，並註冊資源提供者，請參閱[資源提供者和類型](resource-manager-supported-services.md)。

## <a name="when-toocall-support"></a>當 toocall 支援
您可以移動透過本主題中的 hello 自助服務作業的最多資源。 使用 hello 自助服務作業：

* 移動 Resource Manager 資源。
* 將根據 toohello 傳統資源移動[傳統部署限制](#classic-deployment-limitations)。

當您需要進行下列作業時，請連絡支援人員︰

* 移動資源 tooa 新的 Azure 帳戶 （與 Azure Active Directory 租用戶）。
* 將傳統資源移動，但發生問題 hello 限制。

## <a name="services-that-enable-move"></a>啟用移動的服務
現在，是啟用移動 tooboth 新的資源群組和訂用帳戶的 hello 服務：

* API 管理
* App Service 應用程式 (Web 應用程式) - 請參閱 [App Service 限制](#app-service-limitations)
* Application Insights
* 自動化
* Batch
* Bing 地圖
* CDN
* 雲端服務 - 請參閱 [傳統部署限制](#classic-deployment-limitations)
* 辨識服務
* 內容仲裁
* 資料目錄
* Data Factory
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* 事件中樞
* HDInsight 叢集 - 請參閱 [HDInsight 限制](#hdinsight-limitations)
* IoT 中樞
* Key Vault
* 負載平衡器
* Logic Apps
* 機器學習服務
* 媒體服務
* Mobile Engagement
* 通知中樞
* Operational Insights
* Operations Management
* Power BI
* Redis 快取
* 排程器
* 搜尋
* 伺服器管理
* 服務匯流排
* Service Fabric
* 儲存體
* 儲存體 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)
* 串流分析 - 無法移動執行中狀態的串流分析作業。
* SQL Database 伺服器-hello 資料庫和伺服器必須位於 hello 相同的資源群組。 當您移動 SQL 伺服器時，其所有資料庫也會跟著移動。
* 流量管理員
* 虛擬機器
* 使用憑證儲存在金鑰保存庫位在相同的訂用帳戶移動 toonew 資源群組中的虛擬機器已啟用，但未啟用跨訂用帳戶移動。
* 虛擬機器 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)
* 虛擬機器擴展集
* 虛擬網路 - 目前，在停用 VNet 對等互連之前，將無法移動對等的虛擬網路。 一旦停用的 hello 能夠順利移動虛擬網路，而且可以啟用 hello VNet 對等互連。 此外，虛擬網路不能移動的 tooa 不同訂用帳戶，如果 hello 虛擬網路包含資源瀏覽連結的任何子網路。 例如，當 Microsoft.Cache Redis 資源部署到虛擬網路子網路時，該子網路便具有資源導覽連結。
* VPN 閘道


## <a name="services-that-do-not-enable-move"></a>不啟用移動的服務
目前未啟用移動資源的 hello 服務包括：

* AD Domain Services
* AD 混合式健康狀態服務
* 應用程式閘道
* 具有使用受控磁碟之虛擬機器的可用性設定組
* BizTalk 服務
* 容器服務
* ExpressRoute
* DevTest Labs-移動 toonew 資源群組相同的訂用帳戶中已啟用，但不是會啟用跨訂用帳戶移動。
* Dynamics LCS
* 從受控磁碟建立的映像
* 受控磁碟
* 受管理的應用程式
* 復原服務保存庫-不移動 hello 運算、 網路和儲存體資源相關聯也 hello 復原服務保存庫，請參閱[復原服務限制](#recovery-services-limitations)。
* 安全性
* 從受控磁碟建立的快照集
* StorSimple 裝置管理員
* 使用受控磁碟的虛擬機器
* 虛擬網路 (傳統) - 請參閱 [傳統部署限制](#classic-deployment-limitations)
* 從 Marketplace 資源建立的虛擬機器 - 無法在訂用帳戶之間移動。 需要 toobe hello 目前訂用帳戶取消佈建和部署一次 hello 新訂用帳戶中的資源

## <a name="app-service-limitations"></a>App Service 限制
使用 App Service 應用程式時，您無法只移動 App Service 方案。 toomove App Service 應用程式，您的選項如下：

* 該資源群組 tooa 新資源群組中已經沒有應用程式服務的資源移動 hello 應用程式服務方案和所有其他應用程式服務資源。 甚至，您必須移動的方式 hello 應用程式服務資源的這項需求不是與 hello 應用程式服務方案相關聯。
* 移動 hello 應用程式 tooa 不同的資源群組，但保留 hello 原始的資源群組中的所有應用程式服務方案。

hello 應用程式服務計劃不需要在 tooreside hello 與 hello 應用程式 toofunction 的 hello 應用程式的相同資源群組正確。

例如，如果您的資源群組包含︰

* 與 **plan-a** 關聯的 **web-a**
* 與 **plan-b** 關聯的 **web-b**

您的選項如下：

* 移動 **web-a**、**plan-a**、**web-b** 及 **plan-b**
* 移動 **web-a** 和 **web-b**
* 移動 **web-a**
* 移動 **web-b**

所有其他組合都會留下移動 App Service 方案時無法留下的資源類型 (任何類型的 App Service 資源)。

如果您 web 應用程式位於不同的資源群組超過其應用程式服務方案，但您想 toomove 這兩個 tooa 新的資源群組，您必須執行兩個步驟中的 hello 移動。 例如：

* **web-a** 位於 **web-group** 中
* **plan-a** 位於 **plan-group** 中
* 您想要**web 的**和**計劃的**中的 tooreside**結合群組**

這將移動，在 hello 下列順序執行兩個不同的移動作業 tooaccomplish:

1. 移動 hello **web 的**太**計劃群組**
2. 移動**web 的**和**計劃的**太**結合群組**。

您可以移動應用程式的服務憑證 tooa 新資源群組或訂用帳戶沒有任何問題。 不過，如果您的 web 應用程式包含您購買外部並上傳 toohello 應用程式的 SSL 憑證，您必須刪除 hello 憑證，才能移動 hello web 應用程式。 比方說，您可以執行下列步驟的 hello:

1. 刪除 hello web 應用程式中的 hello 上傳憑證
2. 移動 hello web 應用程式
3. 上傳 hello 憑證 toohello web 應用程式

## <a name="recovery-services-limitations"></a>復原服務限制
移動 未啟用儲存體、 網路或計算與 Azure Site Recovery 使用 tooset 災害復原的資源。

例如，假設您已設定複寫在內部部署機器 tooa 儲存體帳戶 (Storage1)，而且想 hello 受保護機器 toocome 向上，tooAzure 容錯移轉之後為虛擬機器 (VM1) 附加 tooa 虛擬網路 (Network1)。 您無法移動下列任何 Azure 資源-Storage1，VM1，並 Network1-跨越資源群組內 hello 相同訂用帳戶或訂用帳戶之間。

## <a name="hdinsight-limitations"></a>HDInsight 限制

您可以移動 HDInsight 叢集 tooa 新訂用帳戶或資源群組。 不過，您無法跨訂閱 hello 網路功能 （例如 hello 虛擬網路、 NIC 或負載平衡器） 的資源連結的 toohello HDInsight 叢集移動。 此外，您無法移動 tooa 新資源群組是附加的 tooa hello 叢集的虛擬機器的 NIC。

當您移動 HDInsight 叢集 tooa 新訂閱，第一次移動其他資源 （例如 hello 儲存體帳戶）。 接著，單獨使用時移動 hello HDInsight 叢集。

## <a name="classic-deployment-limitations"></a>傳統部署限制
hello 的選項移動透過 hello 傳統模型所部署的資源會因根據是否要移動訂用帳戶或 tooa 新訂用帳戶中的 hello 資源。

### <a name="same-subscription"></a>相同訂用帳戶
當移動資源從一個資源群組 tooanother 資源群組內套用相同的訂用帳戶，下列限制的 hello hello:

* 無法移動虛擬網路 (傳統)。
* 必須移動虛擬機器 （傳統） 與 hello 雲端服務。
* 當 hello 移動包含其所有的虛擬機器時，就只能移動雲端服務。
* 一次只能移動一個雲端服務。
* 一次只能移動一個儲存體帳戶 (傳統)。
* 儲存體帳戶 （傳統） 無法在 hello 移動虛擬機器或雲端服務相同的作業。

toomove 傳統資源 tooa 新資源群組內 hello 相同訂用帳戶，請使用 hello 標準的移動作業透過 hello[入口網站](#use-portal)， [Azure PowerShell](#use-powershell)， [Azure CLI](#use-azure-cli)，或[REST API](#use-rest-api)。 您使用 hello 相同的作業，因為您用來移動資源管理員資源。

### <a name="new-subscription"></a>新的訂用帳戶
當您移動資源 tooa 新訂用帳戶，便會套用下列限制的 hello:

* Hello 訂用帳戶中的所有傳統資源必須移動 hello 中相同的作業。
* hello 目標訂用帳戶不可以包含任何其他傳統資源。
* 只可以透過傳統移動個別的 REST API 要求 hello 移動。 hello 標準資源管理員移動命令無法運作時移動傳統資源 tooa 新訂用帳戶。

toomove 傳統資源 tooa 新訂用帳戶，都是特定 tooclassic 資源的使用 hello REST 作業。 toouse 其餘部分，執行下列步驟的 hello:

1. 檢查如果 hello 來源訂用帳戶可以參與跨訂用帳戶移動。 使用 hello 下列操作：

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     在 hello 要求主體中，包括：

  ```json
  {
    "role": "source"
  }
  ```

     hello 回應 hello 驗證作業處於下列格式的 hello:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. 檢查如果 hello 目的地訂用帳戶可以參與跨訂用帳戶移動。 使用 hello 下列操作：

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     在 hello 要求主體中，包括：

  ```json
  {
    "role": "target"
  }
  ```

     hello 回應 hello 相同 hello 來源訂用帳戶的驗證格式為。
3. 如果這兩個訂用帳戶通過驗證時，移動所有傳統資源從一個訂用帳戶 tooanother 訂用帳戶以 hello 下列操作：

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    在 hello 要求主體中，包括：

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

hello 作業可能會執行幾分鐘的時間。

## <a name="use-portal"></a>使用入口網站
toomove 資源，選取包含這些資源，hello 資源群組，然後選取 [hello**移動**] 按鈕。

![移動資源](./media/resource-group-move-resources/select-move.png)

選取您要移動 hello 資源 tooa 新資源群組或新的訂用帳戶。

選取 hello 資源 toomove 與 hello 目的地資源群組。 了解您需要 tooupdate 指令碼，這些資源並選取**確定**。 如果您選取 hello 編輯訂用帳戶 圖示 hello 上一個步驟中，您也必須選取 hello 目的地訂用帳戶。

![選取目的地](./media/resource-group-move-resources/select-destination.png)

在**通知**，您會看到該 hello 移動作業正在執行。

![顯示移動狀態](./media/resource-group-move-resources/show-status.png)

完成後，就會通知的 hello 結果。

![顯示移動結果](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>使用 PowerShell
toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`Move-AzureRmResource`命令。

hello 第一個範例顯示如何 toomove 一個資源 tooa 新資源群組。

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

hello 第二個範例會示範如何 toomove 多個資源 tooa 新資源群組。

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa 新訂用帳戶，包含的值 hello`DestinationSubscriptionId`參數。

系統會詢問您想 toomove hello tooconfirm 指定資源。

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>使用 Azure CLI 2.0
toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`az resource move`命令。 提供 hello 資源 hello 資源 toomove Id。 您可以取得的資源識別碼與 hello 下列命令：

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

hello 下列範例顯示如何 toomove 儲存體帳戶 tooa 新資源群組。 在 hello`--ids`參數，提供的 hello 資源 Id toomove 以空格分隔清單。

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa 新訂用帳戶，提供 hello`--destination-subscription-id`參數。

## <a name="use-azure-cli-10"></a>使用 Azure CLI 1.0
toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello`azure resource move`命令。 提供 hello 資源 hello 資源 toomove Id。 您可以取得的資源識別碼與 hello 下列命令：

```azurecli
azure resource list -g sourceGroup --json
```

它會傳回下列格式的 hello:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

hello 下列範例顯示如何 toomove 儲存體帳戶 tooa 新資源群組。 在 hello`-i`參數，提供 hello 資源 Id toomove 的逗號分隔清單。

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

系統會詢問您想 toomove hello tooconfirm 指定的資源。

## <a name="use-rest-api"></a>使用 REST API
toomove 現有資源 tooanother 資源群組或訂用帳戶，執行：

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

在 hello 要求主體中，您可以指定 hello 目標資源群組與 hello 資源 toomove。 如需 hello 移動 REST 作業的詳細資訊，請參閱[資源移](https://msdn.microsoft.com/library/azure/mt218710.aspx)。

## <a name="next-steps"></a>後續步驟
* toolearn 相關 PowerShell cmdlet 來管理您的訂閱，請參閱[使用 Azure PowerShell 與資源管理員](powershell-azure-resource-manager.md)。
* toolearn 有關 Azure CLI 命令可用於管理您的訂閱，請參閱[使用 hello Azure CLI 與資源管理員](xplat-cli-azure-resource-manager.md)。
* toolearn 有關入口網站功能來管理您的訂閱，請參閱[使用 hello Azure 入口網站 toomanage 資源](resource-group-portal.md)。
* toolearn 有關套用邏輯組織 tooyour 資源，請參閱[使用標記 tooorganize 資源](resource-group-using-tags.md)。
