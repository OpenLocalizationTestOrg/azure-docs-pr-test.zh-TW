---
title: "aaaCommon 雲端服務的管理工作 （傳統） |Microsoft 文件"
description: "了解如何 toomanage 雲端服務的 hello Azure 傳統入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>如何 tooManage 雲端服務
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-how-to-manage-portal.md)
> * [Azure 傳統入口網站](cloud-services-how-to-manage.md)
>
>

在 hello**雲端服務**區域 hello Azure 傳統入口網站中，您可以更新服務角色或部署、 升級預備的部署 tooproduction、 連結資源 tooyour 雲端服務，讓您能夠查看 hello 資源相依性和小數位數 hello 資源在一起，並刪除雲端服務或部署。

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>作法：更新雲端服務角色或部署
如果您需要 tooupdate hello 應用程式程式碼為雲端服務時，使用**更新**hello 儀表板，**雲端服務** 頁面上，或**執行個體**頁面。 您可以更新單一角色或所有角色。 您將需要 tooupload 新的服務封裝和服務組態檔。

1. 在 [hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，hello 儀表板，**雲端服務**] 頁面上，或**執行個體**頁面上，按一下**更新**。

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. 在**部署標籤**，輸入名稱 tooidentify hello 部署 (例如，mycloudservice4)。 您會發現下的 hello 部署標籤**快速入門**hello 儀表板上。
3. 在**封裝**，使用**瀏覽**tooupload hello 服務封裝檔 (.cspkg)。
4. 在**組態**，使用**瀏覽**tooupload hello 服務組態檔 (.cscfg)。
5. 在**角色**，選取**所有**hello 中的所有角色如果您想 tooupgrade 都雲端服務。 tooperform 單一角色更新，您想要 tooupdate 選取 hello 角色。 即使您選取特定角色 tooupdate，hello 服務組態檔中的 hello 更新會套用的 tooall 角色。
6. 如果 hello 更新變更 hello 的角色數目或任何角色 hello 大小，選取 hello**角色大小或角色數目變更時，允許更新**核取方塊 tooenable hello 更新 tooproceed。

    請注意，如果您變更 hello （也就是虛擬機器主控角色執行個體的 hello 大小） 的角色大小或 hello 」 角色數量時，必須重新製作映像，每個角色執行個體 （虛擬機器），而且任何本機資料將會遺失。

7. 如果服務的任何角色只能有一個角色執行個體，請選取 hello**更新，即使一個或多個角色包含單一執行個體的核取方塊**tooenable hello 升級 tooproceed。

    要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。 可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。

8. 按一下**確定**（勾選記號） toobegin 更新 hello 服務。

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>如何： 交換部署 toopromote 預備的部署 tooproduction
使用**交換**toopromote 雲端服務 tooproduction 預備環境部署。 當您決定 toodeploy 雲端服務的新版本時，您可以階段，然後在您的客戶在生產環境中使用 hello 目前版本時，雲端服務的預備環境中測試新版本。 當您準備好 toopromote hello 新發行 tooproduction，您可以使用**交換**兩個部署的位址由哪些 hello tooswitch hello Url。

您可以交換部署從 hello**雲端服務**頁面或 hello 儀表板。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**。
2. 在 hello 清單中的雲端服務，按一下 hello 雲端服務 tooselect 它。
3. 按一下 [交換] 。

    hello 下列確認提示隨即開啟。

    ![Cloud Services Swap](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. 確認 hello 部署資訊後，按一下**是**tooswap hello 部署。

    hello 部署交換很快就會因為 hello 唯一變更是 hello 虛擬 IP 位址 (Vip) hello 部署。

    toosave 運算成本，您可以刪除 hello 預備環境，當您確定 hello 新增生產部署如預期執行中的 hello 部署。

### <a name="common-questions-about-swapping-deployments"></a>交換部署的相關常見問題

**交換部署的 hello 必要條件為何？**

成功的部署交換有兩個主要必要條件：

- 如果您想要 toouse 靜態 IP 位址的生產位置，您必須保留以及您預備位置的其中一個。 否則，hello 交換將會失敗。

- 必須先執行所有的執行個體的角色，您可以執行 hello 交換。 您可以查看您的執行個體在 hello Azure 傳統入口網站或使用 hello 狀態[hello Get-azurerole 命令在 Windows PowerShell 中的](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)。

請注意，客體作業系統更新和服務修復作業也可能會導致部署交換 toofail。 如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。

**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**

Hello 最後一節所述，部署交換通常是非常快速因為它是只在 hello Azure 負載平衡器組態變更。 不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。 toolimit 影響 tooyour 客戶，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>如何： 連結資源 tooa 雲端服務
tooshow 您的雲端服務相依於其他資源，您可以將連結的 Azure SQL Database 執行個體或儲存體帳戶 toohello 雲端服務。 您可以連結，並取消連結資源的 hello**連結的資源**頁面，然後再監視其 hello 雲端服務儀表板上的使用量。 如果監視開啟連結的儲存體帳戶，您可以監視 hello 雲端服務儀表板上的要求總數。

使用**連結**toolink 新的或現有 SQL Database 執行個體或儲存體帳戶 tooyour 雲端服務。 然後，您可以調整 hello 資料庫正在使用它在 hello 的 hello 雲端服務角色以及**標尺**頁面。 (儲存體帳戶會在使用量增加時自動調整。)如需詳細資訊，請參閱[如何 tooScale 雲端服務和連結的資源](cloud-services-how-to-scale.md)。

您也可以監視、 管理及調整 hello 資料庫在 hello**資料庫**hello Azure 傳統入口網站的節點。

「 連結 」 資源，這一點而言並不會連接您的應用程式 toohello 資源。 如果您建立新的資料庫使用**連結**，您將需要 tooadd hello 連接字串 tooyour 應用程式程式碼，接著再升級 hello 雲端服務。 如果您的應用程式會使用資源的連結儲存體帳戶中，您也會需要 tooadd 連接字串。

hello 遵循程序描述如何 toolink 新的 SQL Database 執行個體上部署新的 SQL Database 伺服器，tooa 雲端服務。

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink SQL Database 執行個體 tooa 雲端服務
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。 然後按一下 hello hello 雲端服務 tooopen hello 儀表板的名稱。
2. 按一下 [Linked Resources] 。

    hello**連結的資源**頁面隨即開啟。

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. 按一下 [連結資源] 或 [連結]。

    hello**連結資源**精靈 隨即啟動。

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. 按一下 [建立新的資源] 或 [連結現有的資源]。
5. 選擇資源 toolink hello 類型。 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下  **SQL Database**。 （hello Azure 傳統入口網站支援連結儲存體帳戶 tooa 雲端服務）。
6. toocomplete hello 的資料庫組態，遵循 hello 的說明 中的指示**SQL 資料庫**hello Azure 傳統入口網站的區域。

    您可以遵循連結作業 hello 訊息區域中的 hello hello 進度。

    連結完成時，您可以監視 hello hello 雲端服務儀表板上的 hello 連結資源的狀態。 如需擴充連結的 SQL Database 的資訊，請參閱[如何 tooScale 雲端服務和連結的資源](cloud-services-how-to-scale.md)。

### <a name="toounlink-a-linked-resource"></a>toounlink 連結的資源
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。 然後按一下 hello hello 雲端服務 tooopen hello 儀表板的名稱。
2. 按一下**連結的資源**，然後選取 hello 資源。
3. 按一下 [取消連結] 。 然後按一下 **是**在 hello 確認提示。

    取消連結 SQL Database 有 hello 資料庫或應用程式 hello toohello 資料庫的連接上沒有作用。 您仍然可以管理在 hello hello 資料庫**SQL 資料庫**hello Azure 傳統入口網站的區域。

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>作法：刪除部署和雲端服務
刪除雲端服務之前，您必須先刪除每個現有的部署。

toosave 運算成本，確認您的生產環境部署的運作正常之後，可以刪除您的預備環境部署。 只要角色執行個體存在，您就需要為其支付運算成本，即使雲端服務未執行也一樣。

部署或雲端服務，請使用下列程序 toodelete hello。

1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。
2. 選取 hello 雲端服務，然後按一下**刪除**。 （tooselect 雲端服務，而不需要開啟 hello 儀表板中，按一下任何位置 hello 雲端服務項目中的 hello 名稱除外）。

    如果您擁有預備環境或生產環境部署，您會看到下列其中一個在 hello hello 視窗底部選擇類似 toohello 的功能表。 您可以刪除 hello 雲端服務之前，您必須刪除現有的部署。

    ![Delete Menu](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete 部署中，按一下**刪除生產部署**或**刪除預備環境部署**。 然後，在 hello 確認提示按一下**是**。
4. 如果您計劃 toodelete hello 雲端服務，請重複步驟 3，如有需要 toodelete 您其他的部署。
5. toodelete hello 雲端服務，請按一下**刪除雲端服務**。 然後，在 hello 確認提示按一下**是**。

> [!NOTE]
> 如果設定為您的雲端服務的詳細資訊監視，Azure 不會刪除監視資料，從儲存體帳戶，當您刪除 hello 雲端服務的 hello。 您以手動方式需要 toodelete hello 資料。 其中 toofind hello 度量資料表的相關資訊，請參閱 「 如何： 存取外部 hello Azure 傳統入口網站的詳細資訊監視資料 」 中[tooMonitor 雲端服務如何](cloud-services-how-to-monitor.md)。
>
>

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure.md)。
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。
