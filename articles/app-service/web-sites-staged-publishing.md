---
title: "針對 Azure App Service 中的 Web 應用程式設定預備環境 | Microsoft Docs"
description: "了解如何針對 Azure App Service 中的 Web 應用程式使用預備發行。"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: b69f6b2190362b970420ba81450978ac9faecd86
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>在 Azure App Service 中設定預備環境
<a name="Overview"></a>

當您將 Web 應用程式、Linux 上的 Web 應用程式、行動後端及 API 應用程式部署到 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 時，如果是在 [標準] 或 [進階] App Service 方案模式下執行，就可以部署到個別的部署位置，而不是預設的生產環境位置。 部署位置實際上是含有自己主機名稱的作用中應用程式。 兩個部署位置 (包括生產位置) 之間的應用程式內容與設定項目可以互相交換。 將應用程式部署至部署位置具有下列優點：

* 您可以先驗證預備部署位置中的應用程式變更，再將它與生產位置進行交換。
* 先將應用程式部署至某個位置，然後再將它交換到生產位置，可確保該位置的所有執行個體在交換到生產位置之前都已準備就緒。 這麼做可以排除部署應用程式時的停機情況。 交換作業期間所有的流量都能順暢地重新導向，而且不會捨棄任何要求封包。 不需要預先交換驗證時，這整個工作流程可藉由設定 [自動交換](#Auto-Swap) 來自動化。
* 交換之後，先前具有預備應用程式的位置，現在已經有之前的生產應用程式。 若交換到生產位置的變更不是您需要的變更，您可以立即執行相同的交換，以取回「上一個已知良好的網站」。

每個 App Service 方案模式所支援的部署位置個數都不一樣。 若要找出應用程式模式所支援的位置個數，請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。

* 當您的應用程式擁有多個位置時，就無法變更該模式。
* 非生產的位置無法使用調整規模。
* 非生產位置不支援連結的資源管理。 只有在 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715) 中，您才能藉由暫時將非生產位置移到其他 App Service 方案模式，來避免這種對生產位置的潛在影響。 請注意，非生產位置必須先再次與生產位置共用相同模式，您才能交換這兩個位置。

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>新增部署位置
應用程式必須在 [標準] 或 [高階] 模式中執行，您才能啟用多個部署位置。

1. 在 [Azure 入口網站](https://portal.azure.com/)中，開啟應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。
2. 選擇 [部署位置] 選項，然後按一下 [新增位置]。
   
    ![新增部署位置][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > 如果應用程式尚未處於 [標準] 或 [高階] 模式，您將會收到訊息，指出支援啟用預備發佈的模式。 此時，您可以選取 [升級]，並瀏覽至應用程式的 [級別] 索引標籤後再繼續。
   > 
   > 
3. 在 [新增位置] 刀鋒視窗中，指定位置名稱，然後選取是否要複製其他現有部署位置的應用程式設定。 按一下打勾記號繼續。
   
    ![組態來源][ConfigurationSource1]
   
    第一次新增位置時，您只會有兩個選項：從生產環境的預設位置複製設定，或者完全不複製。
    建立數個位置後，就可以從生產位置以外的位置複製組態：
   
    ![組態來源][MultipleConfigurationSources]
4. 在您應用程式的資源刀鋒視窗中，按一下 [部署位置]，然後按一下某個部署位置來開啟該位置的資源刀鋒視窗，當中會含有一組計量和組態，就像任何其他應用程式一樣。 刀鋒視窗頂端顯示之位置的名稱，提醒您正在檢視部署位置。
   
    ![Deployment Slot Title][StagingTitle]
5. 在位置的刀鋒視窗中按一下應用程式 URL。 請注意，部署位置有自己的主機名稱，同時也是作用中的應用程式。 若要限制對部署位置的公用存取，請參閱 [App Service Web 應用程式 - 封鎖對非生產部署位置的 Web 存取](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)。

建立部署位置之後不會有任何內容。 您可以從不同的儲存機制分支，或從整個不同的儲存機制部署至位置。 您也可以變更位置的組態。 更新內容時，請使用與部署位置相關聯的發行設定檔或部署認證。  例如，您可以 [使用 Git 發行至此位置](app-service-deploy-local-git.md)。

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>部署位置組態
當您複製其他部署位置的組態時，可以編輯複製的組態。 此外，某些組態項目在交換時會遵循內容 (非位置特定)，而其他組態項目將會在交換之後保留於同一個位置中 (位置特定)。 以下清單顯示當您交換位置時會變更的組態。

**交換的設定**：

* 一般設定 - 例如 Framework 版本、32/64 位元、Web 通訊端
* 應用程式設定 (可以設定為停在某一個位置)
* 連接字串 (可以設定為停在某一個位置)
* 處理常式對應
* 監視與診斷設定
* WebJobs 內容

**無法交換的設定**：

* 發行端點
* 自訂網域名稱
* SSL 憑證與繫結
* 擴充設定
* WebJobs 排程器

若要將應用程式設定或連接字串設定為停留在某一個位置 (未交換)，可存取特定位置的 [應用程式設定] 刀鋒視窗，然後針對應停留在該位置的設定項目選取 [位置設定] 方塊。 請注意，將組態項目標記為位置特定的，會在將該項目建立為無法跨所有與該應用程式相關聯的部署位置進行交換時產生影響。

![位置設定][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>交換部署位置 
您可以在您應用程式資源刀鋒視窗的**概觀**或**部署位置**檢視中交換部署位置。

> [!IMPORTANT]
> 在您將應用程式從部署位置交換到生產位置之前，請確定所有非位置特定的設定已完全依照您想要在交換目標中擁有它的方式明確地加以設定。
> 
> 

1. 若要交換部署位置，可按一下應用程式命令列或部署位置命令列中的 [交換] 按鈕。
   
    ![Swap Button][SwapButtonBar]

2. 請確定交換來源和交換目標都已正確設定。 交換目標通常是生產位置。 按一下 確定  來完成操作。 當操作完成時，部署位置就已交換完畢。

    ![完整的交換](./media/web-sites-staged-publishing/SwapImmediately.png)

    針對**使用預覽交換**交換類型，請參閱[使用預覽交換 (多階段交換)](#Multi-Phase)。  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>使用預覽交換 (多階段交換)

使用預覽交換或多階段交換，簡化組態項目的位置特定驗證，例如連接字串。
針對關鍵任務的工作負載，您想要驗證當套用生產位置的組態時應用程式的行為會如預期，且您必須在應用程式交換到生產環境*之前*執行這類驗證。 您需要的是使用預覽交換。

> [!NOTE]
> Linux 上的 Web 應用程式不支援使用預覽交換。

當您使用**使用預覽交換**選項時 (請參閱[交換部署位置](#Swap))，App Service 會進行下列作業︰

- 目的地位置會保留不變，因此不會影響該位置上的現有工作負載 (例如生產)。
- 將目的地位置的組態項目套用至來源位置，包括位置特定的連接字串和應用程式設定。
- 使用這些上述的組態項目重新啟動來源位置上的工作者處理序。
- 當您完成交換時︰將 pre-warmed-up 來源位置移到目的地位置。 目的地位置會如手動交換移到來源位置。
- 當您取消交換時︰將來源位置的組態項目重新套用至來源位置。

您可以完全預覽應用程式與目的地位置組態的行為模式。 當您完成驗證時，會在個別步驟中完成交換。 此步驟有額外好處，來源位置已做好使用所需的設定，且用戶端不會發生任何停機時間。  

Azure PowerShell Cmdlet 可供多階段交換的範例，包含在部署位置區段的 Azure PowerShell Cmdlet 內。

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>設定自動交換
自動交換會簡化 DevOps 案例，在此案例中，您希望為該應用程式的客戶在不需冷啟動和不需關機的情況下連續部署您的應用程式。 當部署位置已設為自動交換至生產位置時，每當您將程式碼更新推送至該位置時，App Service 就會在其已於該位置上做好準備之後，自動將該應用程式交換至生產位置。

> [!IMPORTANT]
> 當您為某個位置啟用自動交換時，請確定位置設定會與適用於目標位置 (通常是生產位置) 的設定完全相同。
> 
> 

> [!NOTE]
> Linux 上的 Web 應用程式不支援自動交換。

為位置設定自動交換很容易。 請依照下列步驟執行：

1. 在**部署位置**中，選取非生產位置，然後在該位置的資源刀鋒視窗中選擇 [應用程式設定]。  
   
    ![][Autoswap1]
2. 針對 [自動交換] 選取 [開啟]、在 [自動交換位置] 中選取所需的目標位置，然後按一下命令列中的 [儲存]。 確定此位置的組態設定完全適用於目標位置的組態設定。
   
    當操作完成時，[通知] 索引標籤會有綠色的「成功」字樣閃爍顯示。
   
    ![][Autoswap2]
   
   > [!NOTE]
   > 若要針對您的應用程式測試自動交換，可在 [自動交換位置] 中選取非生產的目標位置，以便先熟悉這個功能。  
   > 
   > 
3. 執行程式碼推送至該部署位置。 自動交換不久之後就會發生，而更新將反映於目標位置的 URL 上。

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a>交換之後回復生產應用程式
若交換位置後，在生產位置中識別出錯誤，可以立即交換相同的兩個位置，將位置還原成交換前的狀態。

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>交換前的自訂準備
某些應用程式可能需要自訂的準備動作。 web.config 中的 `applicationInitialization` 組態項目可讓您指定收到要求之前要執行的自訂初始化動作。 必須等候此自訂準備完成，才會進行交換作業。 以下是範例 web.config 片段。

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a>刪除部署位置
在部署位置的刀鋒視窗中，開啟部署位置的刀鋒視窗，按一下 概觀 \(預設頁面)，然後按一下命令列中的 [刪除]。  

![刪除部署位置][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>適用於部署位置的 Azure PowerShell Cmdlet
Azure PowerShell 模組提供透過 Windows PowerShell 來管理 Azure 的 Cmdlet，包括支援管理 Azure App Service 中的部署位置。

* 如需安裝與設定 Azure PowerShell，以及使用您的 Azure 訂用帳戶驗證 Azure PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Microsoft Azure PowerShell](/powershell/azure/overview)(英文)。  

- - -
### <a name="create-a-web-app"></a>建立 Web 應用程式
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>建立部署位置
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a>起始使用預覽交換 (多階段交換) 並將目的地位置組態套用至來源位置
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>取消擱置中的交換 (使用預覽交換)，並還原來源位置組態
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>交換部署位置
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>刪除部署位置
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>適用於部署位置的 Azure 命令列介面 (Azure CLI) 命令
Azure CLI 提供跨平台命令供您處理 Azure，包括支援管理 App Service 部署位置。

* 如需安裝與設定 Azure CLI 的相關說明，包括如何將 Azure CLI 連線至 Azure 訂用帳戶的資訊，請參閱 [安裝與設定 Azure CLI](../cli-install-nodejs.md)。
* 若要在 Azure CLI 中列出 Azure App Service 可用的命令，請呼叫 `azure site -h`。

> [!NOTE] 
> 針對適用於部署位置的 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 命令，請參閱 [Azure App Service Web 部署位置](/cli/azure/appservice/web/deployment/slot)。

- - -
### <a name="azure-site-list"></a>azure site list
如需目前訂用帳戶中應用程式的相關資訊，請呼叫 **azure site list**，如下列範例所示。

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
若要建立部署位置，請呼叫 **azure site create** 並指定現有應用程式的名稱與要建立之位置的名稱，如下列範例所示。

`azure site create webappslotstest --slot staging`

若要對新位置啟用來源控制，請使用 **--git** 選項，如以下範例所示。

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
若要將已更新的部署位置轉變成生產應用程式，請使用 **azure site swap** 命令來執行交換作業，如下列範例所示。 生產應用程式不會發生任何停機事件，也不會進行冷啟動。

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
若要刪除不再需要的部署位置，請使用 **azure site delete** 命令，如以下範例所示。

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> 請看看作用中的 Web 應用程式。 [試用 App Service](https://azure.microsoft.com/try/app-service/) 並建立短期的入門應用程式 — 不需信用卡，不需任何承諾。
> 
> 

## <a name="next-steps"></a>後續步驟
[Azure App Service Web 應用程式 - 封鎖對非生產環境部署位置的 Web 存取 (英文)](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Linux 上的 App Service 簡介](../app-service/containers/app-service-linux-intro.md)
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

