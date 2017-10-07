---
title: "設定預備環境中 Azure App Service web 應用程式的 aaaSet |Microsoft 文件"
description: "了解 toouse 分段發行 Azure App Service 中的 web 應用程式的安裝。"
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
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>在 Azure App Service 中設定預備環境
<a name="Overview"></a>

當您部署您的 web 應用程式、 Linux、 行動裝置的後端，以及 API 應用程式的 web 應用程式太[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，hello 中執行時，您可以部署 tooa 不同的部署位置，而不是 hello 預設生產位置**標準**或**Premium**應用程式服務計劃模式。 部署位置實際上是含有自己主機名稱的作用中應用程式。 應用程式內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。 部署您的應用程式 tooa 部署位置有 hello 下列優點：

* 您可以先再與 hello 生產位置交換驗證預備部署位置中的應用程式變更。
* 第一次部署的應用程式 tooa 位置和交換至生產環境來確保 hello 位置的所有執行個體正在交換至生產環境之前會就緒。 這麼做可以排除部署應用程式時的停機情況。 hello 流量重新導向，隨選和交換作業之後的任何要求都會被卸除。 不需要預先交換驗證時，這整個工作流程可藉由設定 [自動交換](#Auto-Swap) 來自動化。
* 交換之後, hello 位置使用先前執行的應用程式現在具有 hello 先前的生產環境應用程式。 如果 hello 變更成 hello 生產位置交換未如您所預期，您可以執行的 hello 相同交換立即 tooget 您 「 上次已知良好的站台 」 備份。

每個 App Service 方案模式所支援的部署位置個數都不一樣。 您的應用程式模式可支援 toofind 出 hello 的插槽數目，請參閱[應用程式服務定價](https://azure.microsoft.com/pricing/details/app-service/)。

* 當您的應用程式有多個位置時，您無法變更 hello 模式。
* 非生產的位置無法使用調整規模。
* 非生產位置不支援連結的資源管理。 在 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)，暫時移動 hello 非生產位置 tooa 不同應用程式服務計劃模式可以避免此潛在的影響，在生產環境位置。 請注意該 hello 非生產位置必須再次共用 hello hello 生產位置之前，您可以交換 hello 兩個位置具有相同的模式。

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>新增部署位置
hello 應用程式必須執行 hello**標準**或**Premium**您 tooenable 多個部署位置中的模式順序。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，開啟您的應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。
2. 選擇 hello**部署位置**選項，然後按一下 **加入位置**。
   
    ![新增部署位置][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > 如果 hello 應用程式已不在 hello**標準**或**Premium**模式中，您會收到訊息，指出啟用預備的發行的 hello 支援模式。 此時，您擁有 hello 選項 tooselect**升級**並瀏覽 toohello**標尺** 索引標籤，應用程式才能繼續。
   > 
   > 
3. 在 hello**加入位置**刀鋒視窗中，輸入 hello 插槽的名稱，然後選取是否 tooclone 應用程式組態，從另一個現有的部署位置。 按一下 hello 核取記號 toocontinue。
   
    ![組態來源][ConfigurationSource1]
   
    hello 第一次加入位置，您只需要兩個選擇： hello 預設位置在生產環境中，或完全無法執行的複製組態。
    建立數個位置之後，您會從實際執行其中一個 hello 以外的位置無法 tooclone 組態：
   
    ![組態來源][MultipleConfigurationSources]
4. 在您的應用程式資源刀鋒視窗中，按一下**部署位置**，然後按一下該位置的資源刀鋒視窗中，使用一組度量與組態，就像任何其他應用程式的部署位置 tooopen。 hello hello 插槽的名稱會顯示您要檢視在頂端的 hello 刀鋒視窗 tooremind hello hello 部署位置。
   
    ![Deployment Slot Title][StagingTitle]
5. 按一下 在 hello 插槽刀鋒視窗中的 hello 應用程式 URL。 請注意，hello 部署位置具有本身的主機名稱也是即時應用程式。 toolimit 公用存取 toohello 部署位置，請參閱[App Service Web 應用程式 – 區塊 web 存取 toonon 生產部署位置](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)。

建立部署位置之後不會有任何內容。 您可以部署不同的儲存機制分支或完全不同的儲存機制從 toohello 位置。 您也可以變更 hello 位置的組態。 使用 hello 發行設定檔或部署認證更新內容的 hello 部署位置與相關聯。  例如，您可以[發行 toothis 插槽與 git](app-service-deploy-local-git.md)。

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>部署位置組態
當您複製另一個部署位置的組態時，hello 複製的設定為可編輯。 此外，某些組態項目會依照 hello 內容之間的交換 （沒有位置特定） 其他組態項目都會保留在相同位置 （在特定位置） 的交換之後 hello 時。 hello 下列清單顯示 hello 組態，當交換位置將會變更。

**交換的設定**：

* 一般設定 - 例如 Framework 版本、32/64 位元、Web 通訊端
* （可設定的 toostick tooa 位置） 的應用程式設定
* （可設定的 toostick tooa 位置） 的連接字串
* 處理常式對應
* 監視與診斷設定
* WebJobs 內容

**無法交換的設定**：

* 發行端點
* 自訂網域名稱
* SSL 憑證與繫結
* 擴充設定
* WebJobs 排程器

應用程式設定或連接字串 toostick tooa 位置 （不交換），存取 hello tooconfigure**應用程式設定**刀鋒視窗中的特定位置，然後選取 hello**位置設定**hello 方塊應盡可能 hello 位置的組態項目。 請注意，將標記的組態項目為特定位置的效果 hello 的跨 hello 應用程式相關聯的所有 hello 部署位置，建立做為不抽換的項目。

![位置設定][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>交換部署位置 
您可以交換部署位置中 hello**概觀**或**部署位置**檢視您的應用程式資源刀鋒視窗。

> [!IMPORTANT]
> 您可以交換部署位置中的應用程式到實際執行環境之前，請確定所有非位置的特定設定已完全依照您想要 toohave 在 hello 交換的目標。
> 
> 

1. tooswap 部署位置，按一下 hello**交換**hello 的 hello 應用程式的命令列中，或部署位置 hello 命令列中的按鈕。
   
    ![Swap Button][SwapButtonBar]

2. 請確定該 hello 交換來源和交換目標都已正確設定。 Hello 交換目標通常就是 hello 生產位置。 按一下**確定**toocomplete hello 作業。 Hello 作業完成時，已交換 hello 部署位置。

    ![完整的交換](./media/web-sites-staged-publishing/SwapImmediately.png)

    Hello**使用預覽交換**交換類型，請參閱[預覽 （多階段交換） 的交換](#Multi-Phase)。  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>使用預覽交換 (多階段交換)

使用預覽交換或多階段交換，簡化組態項目的位置特定驗證，例如連接字串。
針對關鍵任務工作負載，您想 toovalidate hello 應用程式的行為如預期般套用 hello 生產位置的組態時，而且您必須執行這類驗證*之前*hello 應用程式會交換至生產環境。 您需要的是使用預覽交換。

> [!NOTE]
> Linux 上的 Web 應用程式不支援使用預覽交換。

當您使用 hello**預覽交換**選項 (請參閱[交換部署位置](#Swap))，應用程式服務未遵循 hello:

- 保留 hello 目的地位置未變更所以現有的工作負載上該位置 （例如生產環境） 不會受到影響。
- 適用於 hello 的 hello 目的地位置 toohello 來源位置，包括 hello 插槽特有的連接字串和應用程式設定的組態項目。
- 重新啟動 hello 來源位置使用這些先前提及的組態項目上的 hello 工作者處理序。
- 當您完成 hello 交換： hello 目的地插槽移 hello 前 warmed 向上來源位置。 hello 目的地位置會移到 hello 與手動交換的來源位置。
- 當您取消 hello 交換： hello 的 hello 來源位置 toohello 來源位置的組態項目會重新套用。

您可以預覽完全 hello 應用程式的行為方式與 hello 目的地位置的組態。 一旦您完成驗證，您會完成在個別步驟中的 hello 交換。 此步驟中具有 hello 好處 hello 來源位置已就緒與 hello 所需的組態，以及用戶端不會經歷任何停機時間。  

Hello Azure PowerShell 指令程式可供多階段交換的範例包含在 hello Azure PowerShell cmdlet 的部署位置 區段中。

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>設定自動交換
自動交換簡化 DevOps 案例中，您 toocontinuously hello 應用程式的客戶部署應用程式與零冷啟動和零停機時間。 部署位置設定為自動交換到生產環境中，每次推送您的程式碼更新 toothat 位置，當應用程式服務將會自動交換 hello 應用程式至生產環境它有已就緒 hello 插槽中。

> [!IMPORTANT]
> 當您啟用自動交換的位置時，請確定 hello 位置組態完全 hello 用於設定 hello 目標位置 （通常 hello 生產位置）。
> 
> 

> [!NOTE]
> Linux 上的 Web 應用程式不支援自動交換。

為位置設定自動交換很容易。 請遵循下列步驟執行 hello:

1. 在**部署位置**中，選取非生產位置，然後在該位置的資源刀鋒視窗中選擇 [應用程式設定]。  
   
    ![][Autoswap1]
2. 選取**上**的**自動交換**，選取中的 hello 想要的目標位置**自動交換位置**，然後按一下**儲存**hello 命令列中。 請確定組態 hello 位置完全 hello 用於設定 hello 目標位置。
   
    hello**通知** 索引標籤將會閃爍綠色**成功**一旦 hello 作業已完成。
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest 的自動交換，您的應用程式，您可以先選取中的非生產目標位置**自動交換位置**toobecome 熟悉 hello 功能。  
   > 
   > 
3. 執行程式碼推入 toothat 部署位置。 一段時間之後會發生自動交換，而且 hello 更新會反映在目標位置的 URL。

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback 交換後在生產應用程式
如果發現任何錯誤生產位置交換之後，復原 hello 位置後 tootheir 前交換狀態立即交換 hello 相同的兩個位置。

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>交換前的自訂準備
某些應用程式可能需要自訂的準備動作。 hello `applicationInitialization` web.config 中的組態項目可讓您 toospecify 自訂初始化動作 toobe 執行之前收到要求。 此自訂熱身 toocomplete 將會等到 hello 交換作業。 以下是範例 web.config 片段。

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete 部署位置
在 hello 刀鋒視窗中的部署位置，開啟 hello 部署位置的刀鋒視窗中，按一下 **概觀**（hello 預設頁面），然後按一下**刪除**hello 命令列中。  

![刪除部署位置][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>適用於部署位置的 Azure PowerShell Cmdlet
Azure PowerShell 是提供 cmdlet toomanage Azure 透過 Windows PowerShell，包括用於管理 Azure App Service 中的部署位置支援的模組。

* 如需有關安裝及設定 Azure PowerShell，及其向您的 Azure 訂用帳戶的 Azure PowerShell 的資訊，請參閱[如何 tooinstall 和設定 Microsoft Azure PowerShell](/powershell/azure/overview)。  

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
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>起始與檢閱 （多階段交換） 的交換，並套用目的地位置組態 toosource 位置
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
hello Azure CLI 提供使用 Azure 中，包括用於管理應用程式服務的部署位置支援跨平台命令。

* 如需有關安裝和設定指示 hello Azure CLI，包括有關如何 tooconnect Azure CLI tooyour Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。
* 適用於 Azure App Service 中 hello Azure CLI toolist hello 命令呼叫`azure site -h`。

> [!NOTE] 
> 針對適用於部署位置的 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 命令，請參閱 [Azure App Service Web 部署位置](/cli/azure/appservice/web/deployment/slot)。

- - -
### <a name="azure-site-list"></a>azure site list
如 hello hello 目前訂用帳戶中的應用程式的相關資訊，請呼叫**azure 站台清單**，如下列範例中的 hello。

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
部署位置，toocreate 呼叫**azure 站台建立**並指定現有的應用程式的 hello 名稱和 hello 插槽 toocreate，如同下列範例中的 hello hello 名稱。

`azure site create webappslotstest --slot staging`

hello 新位置，使用 hello tooenable 原始檔控制**-git**選項，如 hello 下列範例所示。

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake hello 更新的部署位置 hello 生產環境應用程式，請使用 hello **azure 站台交換**命令 tooperform 交換操作，如 hello 下列範例所示。 hello 生產環境應用程式不會經歷任何停機時間，也不會經歷冷啟動。

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete 部署位置已不再需要請使用 hello **azure 站台刪除**命令，如 hello 下列範例所示。

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> 請看看作用中的 Web 應用程式。 [試用 App Service](https://azure.microsoft.com/try/app-service/) 並建立短期的入門應用程式 — 不需信用卡，不需任何承諾。
> 
> 

## <a name="next-steps"></a>後續步驟
[Azure App Service Web 應用程式 – 封鎖 web 存取 toonon 生產部署位置](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[簡介 tooApp Linux 上的服務](./app-service-linux-intro.md)
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

