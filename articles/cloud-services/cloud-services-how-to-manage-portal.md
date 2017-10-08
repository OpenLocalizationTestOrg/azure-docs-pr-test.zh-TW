---
title: "aaaCommon 雲端服務管理工作 |Microsoft 文件"
description: "了解如何 toomanage 雲端服務的 hello Azure 入口網站。 這些範例使用 hello Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

在 hello**雲端服務 （傳統）**區域 hello Azure 入口網站中，您可以更新服務角色或部署、 升級預備的部署 tooproduction、 連結資源 tooyour 雲端服務，讓您能夠查看 hello 資源相依性和小數位數 hello 資源在一起，並刪除雲端服務或部署。

如何 tooscale 您雲端服務可供使用的詳細資訊[這裡](cloud-services-how-to-scale-portal.md)。

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>作法：更新雲端服務角色或部署
如果您需要 tooupdate hello 應用程式程式碼為雲端服務時，使用**更新**hello 雲端服務 刀鋒視窗。 您可以更新單一角色或所有角色。 tooupdate，您可以上傳新的服務封裝或服務組態檔。

1. 在 hello [Azure 入口網站][Azure portal]，選取您想 tooupdate hello 雲端服務。 此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。
2. 在 hello 刀鋒視窗中，按一下 hello**更新** 按鈕。

    ![更新按鈕](./media/cloud-services-how-to-manage-portal/update-button.png)

3. 更新 hello 部署新的服務封裝檔 (.cspkg) 和服務組態檔 (.cscfg)。

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **選擇性地**更新 hello 部署標籤和 hello 儲存體帳戶。
5. 如果任何角色只能有一個角色執行個體，請選取 hello**即使一個或多個角色包含單一執行個體部署**tooenable hello 升級 tooproceed。

    要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。 有兩個角色執行個體，一部虛擬機器處理用戶端要求更新其他 hello 時。

6. 請檢查**啟動部署**toohave hello 更新 hello hello 封裝上的傳已完成之後套用。
7. 按一下**確定**toobegin 更新 hello 服務。

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>如何： 交換部署 toopromote 預備的部署 tooproduction
當您決定 toodeploy 是新發行的雲端服務，階段，並在雲端服務執行環境中測試新版本。 使用**交換**哪些 hello 由兩個部署會定址，並且升級新的版本 tooproduction tooswitch hello Url。

您可以交換部署從 hello**雲端服務**頁面或 hello 儀表板。

1. 在 hello [Azure 入口網站][Azure portal]，選取您想 tooupdate hello 雲端服務。 此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。
2. 在 hello 刀鋒視窗中，按一下 hello**交換** 按鈕。

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. hello 下列確認提示隨即開啟。

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. 確認 hello 部署資訊後，按一下**確定**tooswap hello 部署。

    hello 部署交換很快就會因為 hello 唯一變更是 hello 虛擬 IP 位址 (Vip) hello 部署。

    toosave 運算成本，您可以刪除 hello 預備環境部署之後您確認生產部署如預期般運作。

### <a name="common-questions-about-swapping-deployments"></a>交換部署的相關常見問題

**交換部署的 hello 必要條件為何？**

成功的部署交換有兩個主要必要條件：

- 如果您想要 toouse 靜態 IP 位址的生產位置，您必須保留以及您預備位置的其中一個。 否則 hello 交換就會失敗。

- 必須先執行所有的執行個體的角色，您可以執行 hello 交換。 您可以檢查 hello hello 概觀刀鋒視窗中的 hello Azure 入口網站執行個體的狀態。 或者，您可以使用 hello [Get-azurerole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell 命令。

請注意，客體 OS 更新服務修復作業也可能會導致部署交換 toofail。 如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。

**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**

Hello 最後一節所述，因為它是只在 hello Azure 負載平衡器組態變更部署交換是通常速度快。 不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。 toolimit 影響 tooyour 客戶，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>如何： 連結資源 tooa 雲端服務
hello Azure 入口網站未連結資源 hello 目前 Azure 傳統入口網站類似在一起。 相反地，部署額外的資源 toohello hello 雲端服務正在使用相同的資源群組。

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>作法：刪除部署和雲端服務
刪除雲端服務之前，您必須先刪除每個現有的部署。

toosave 運算成本，您可以刪除 hello 預備環境部署之後您確認生產部署如預期般運作。 您需要為停止的已部署角色執行個體支付運算成本。

部署或雲端服務，請使用下列程序 toodelete hello。

1. 在 hello [Azure 入口網站][Azure portal]，選取您想 toodelete hello 雲端服務。 此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。
2. 在 hello 刀鋒視窗中，按一下 hello**刪除** 按鈕。

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. 您可以刪除 hello 整個雲端服務，藉由檢查**雲端服務和其部署**或選擇任一個 hello**生產環境部署**或 hello**預備部署**。

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. 按一下 hello**刪除**hello 底部的按鈕。
5. toodelete hello 雲端服務，請按一下**刪除雲端服務**。 然後，在 hello 確認提示按一下**是**。

> [!NOTE]
> 當雲端服務遭到刪除，並設定監視的詳細資訊時，您必須從儲存體帳戶以手動方式刪除 hello 資料。 其中 toofind hello 度量資料表的相關資訊，請參閱[這](cloud-services-how-to-monitor.md)發行項。


## <a name="how-to-find-more-information-about-failed-deployments"></a>如何： 尋找失敗部署的詳細資訊
hello**概觀**刀鋒視窗頂端 hello 有狀態列。 當您按一下 hello 列時，新刀鋒視窗中開啟，並顯示任何資訊時發生錯誤。 Hello 部署不包含任何錯誤，如果是空白的 hello 資訊刀鋒視窗。

![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。
* 設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。
