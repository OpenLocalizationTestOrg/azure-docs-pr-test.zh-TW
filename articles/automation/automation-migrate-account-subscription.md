---
title: "aaaMigrate 自動化帳戶和資源 |Microsoft 文件"
description: "本文說明如何 toomove 自動化帳戶在 Azure 自動化和相關聯的資源從一個訂用帳戶 tooanother。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>移轉自動化帳戶和資源
自動化帳戶和其相關聯的資源 （例如資產、 runbook、 模組、 等等） 已在 hello Azure 入口網站中建立，而且想要從一個資源 toomigrate 群組 tooanother 或從一個訂用帳戶 tooanother，您可以完成這項作業輕鬆地與hello[資源移](../azure-resource-manager/resource-group-move-resources.md)hello Azure 入口網站中可用功能。 不過，此動作之前，您應該先檢閱下列 hello[之前移動資源的檢查清單](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources)，此外，hello 特定 tooAutomation 下方的清單。   

1. hello 目的地訂用帳戶/資源群組必須與 hello 來源相同的區域中。  這表示，無法跨區域移動自動化帳戶。
2. 當您移動資源 （例如 runbook、 作業、 等等），hello 來源群組及 hello 目標群組被鎖住 hello hello 作業持續期間。 寫入和刪除作業 hello 移動作業完成之前被封鎖於 hello 群組。  
3. 任何 runbook 或變數參考 hello 現有訂用帳戶的資源或訂用帳戶 ID 必須 toobe 移轉完成之後更新。   

> [!NOTE]
> 這項功能不支援移動傳統自動化資源。
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove hello 使用 hello 入口網站的自動化帳戶
1. 從您的自動化帳戶，按一下 **移動**在 hello hello 刀鋒視窗最上方。<br> ![移動選項](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. 在 hello**資源移**刀鋒視窗時，請注意，它會呈現資源相關的 tooboth 自動化帳戶和資源群組。  選取 hello**訂用帳戶**和**資源群組**hello 下拉式清單或選取 hello 選項從**建立新的資源群組**並輸入新的資源群組名稱中提供的 hello 欄位。  
3. 檢閱和選取 hello 核取方塊 tooacknowledge 您*了解工具和指令碼將會需要更新 toobe toouse 新的資源 Id 後已經移動資源*，然後按一下**確定**。<br> ![移動資源刀鋒視窗](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

這個動作將會需要幾分鐘的時間 toocomplete。  在 [通知] 中，您會看到所進行的每個動作 (驗證、移轉) 的狀態，然後最後是完成的時間。     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello 使用 PowerShell 的自動化帳戶
toomove 現有自動化資源 tooanother 資源群組或訂用帳戶，使用 hello **Get AzureRmResource** cmdlet tooget hello 特定自動化帳戶，然後**Move-azurermresource**cmdlet tooperform hello 移動。

hello 第一個範例顯示如何 toomove 自動化帳戶 tooa 新資源群組。

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

執行上述程式碼範例的 hello 之後，您會想 tooperform 此動作的提示的 tooverify。  一旦您按一下**是**並允許 hello tooproceed 指令碼，您不會執行 hello 移轉時收到任何通知。  

toomove tooa 新訂用帳戶，包含的值 hello *DestinationSubscriptionId*參數。

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

如同 hello 上述範例中，您將會提示的 tooconfirm hello 移動。  

## <a name="next-steps"></a>後續步驟
* 如需移動資源 toonew 資源群組或訂用帳戶的詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)
* 如需有關在 Azure 自動化中的 角色型存取控制的詳細資訊，請參閱太[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。
* toolearn 相關 PowerShell cmdlet 來管理您的訂閱，請參閱[使用 Azure PowerShell 與資源管理員](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn 有關入口網站功能來管理您的訂閱，請參閱[使用 hello Azure 入口網站 toomanage 資源](../azure-resource-manager/resource-group-portal.md)。
