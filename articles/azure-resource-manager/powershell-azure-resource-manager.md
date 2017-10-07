---
title: "aaaManage Azure PowerShell 解決方案 |Microsoft 文件"
description: "使用 Azure PowerShell 和資源管理員 toomanage 您的資源。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>使用 Azure PowerShell 和 Resource Manager 管理資源
> [!div class="op_single_selector"]
> * [入口網站](resource-group-portal.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
>
>

在本文中，您將學習如何 toomanage 您使用 Azure PowerShell 和 Azure 資源管理員的解決方案。 如果您不熟悉如何使用 Resource Manager，請參閱 [Resource Manager 概觀](resource-group-overview.md)。 本主題著重於管理工作。 您將：

1. 建立資源群組
2. 新增資源 toohello 資源群組
3. 加入標記 toohello 資源
4. 根據名稱或標籤值查詢資源
5. 套用和移除 hello 資源的鎖定
6. 刪除資源群組

這篇文章不會顯示如何 toodeploy 資源管理員範本 tooyour 訂用帳戶。 如需該資訊，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)。

## <a name="get-started-with-azure-powershell"></a>開始使用 Azure PowerShell

如果您尚未安裝 Azure PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

如果您已安裝 Azure PowerShell，在過去的 hello 但近期尚未更新它，請考慮安裝 hello 最新版本。 您可以更新 hello 版本透過 hello tooinstall 時所使用的相同方法它。 例如，如果您使用 Web Platform Installer hello，重新啟動，並尋找更新。

toocheck 您版本的 hello Azure 資源模組，使用下列 cmdlet hello:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

本主題已針對版本 3.3.0 更新。 如果您有較早版本，您的體驗可能不符合本主題中的 hello 步驟。 如需有關這個版本中的 hello cmdlet 的文件，請參閱[AzureRM.Resources 模組](/powershell/module/azurerm.resources)。

## <a name="log-in-tooyour-azure-account"></a>登入 tooyour Azure 帳戶
之前，先在您的方案，您必須登入 tooyour 帳戶。

toolog tooyour Azure 帳戶，請在使用 hello**登入 AzureRmAccount** cmdlet。

```powershell
Login-AzureRmAccount
```

hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。 登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。

hello cmdlet 會傳回您的帳戶和 hello 訂用帳戶 toouse hello 工作的相關資訊。

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

如果您有多個訂用帳戶，您可以切換 tooa 不同訂用帳戶。 首先，我們來看看您帳戶的所有 hello 訂用帳戶。

```powershell
Get-AzureRmSubscription
```

它會傳回啟用和停用的訂用帳戶。

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa 不同訂用帳戶，提供 hello 訂用帳戶名稱以 hello**組 AzureRmContext** cmdlet。

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>建立資源群組
在部署之前的任何資源 tooyour 訂閱，您必須建立資源群組將包含 hello 資源。

toocreate 資源群組、 使用 hello**新增 AzureRmResourceGroup** cmdlet。 hello 命令使用 hello**名稱**參數 toospecify hello 資源群組的名稱 hello**位置**參數 toospecify 其位置。

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

hello 輸出是以下列格式的 hello:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

如果您稍後需要 tooretrieve hello 資源群組，請使用下列 cmdlet 的 hello:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget 所有 hello 訂用帳戶中的資源群組中，未指定名稱：

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>新增資源 tooa 資源群組
tooadd toohello 資源群組，您可以使用 hello**新增 AzureRmResource**您所建立的 cmdlet 或指令程式來為特定 toohello 資源類型 (例如**新增 AzureRmStorageAccount**)。 您可能會發現它更容易 toouse 是特定 tooa 資源類型，因為它包含所需的 hello 新資源的 hello 屬性參數的 cmdlet。 toouse**新增 AzureRmResource**，您必須知道所有 hello 屬性 tooset 不需輸入它們。

不過，加入資源，以透過 cmdlet 可能會導致未來產生混淆因為 hello 新的資源不存在於 Resource Manager 範本。 Microsoft 建議在 Resource Manager 範本中定義 Azure 方案的 hello 基礎結構。 範本讓您 tooreliably，而且重複地部署您的方案。 在本主題中，您會使用 PowerShell Cmdlet 建立儲存體帳戶，但之後您會從資源群組中產生範本。

hello 下列 cmdlet 會建立儲存體帳戶。 而不使用 hello 名稱 hello 範例所示，提供 hello 儲存體帳戶的唯一名稱。 hello 名稱必須介於 3 到 24 個字元的長度，且只能使用數字和小寫字母。 如果您使用 hello 名稱 hello 範例所示，您收到錯誤，因為該名稱已在使用中。

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

如果您需要 tooretrieve 此資源之後，使用下列 cmdlet 的 hello:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>新增標記

標籤可讓您 tooorganize toodifferent 屬性，根據您的資源。 例如，您可能有數個資源 toohello 屬於不同的資源群組中相同的部門。 您可以套用部門 toothose 資源標記和值 toomark 它們隸屬 toohello 為相同類別目錄。 或者，您可以標記資源是在生產或測試環境中使用。 在本主題中，您套用標記 tooonly 一個資源，但您的環境中最有可能是合理 tooapply 標記 tooall 您的資源。

hello 下列 cmdlet 適用於兩個標記 tooyour 儲存體帳戶：

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

標籤會以一個物件的方式更新。 tooadd 標記 tooa 資源已包含標記，首先抓取 hello 現有的標記。 新增 hello 新標記 toohello 物件，其中包含 hello 現有的標記，並重新套用所有 hello 標記 toohello 資源。

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>搜尋資源

使用 hello**尋找 AzureRmResource** cmdlet tooretrieve 不同的搜尋條件的資源。

* tooget 依名稱、 資源提供 hello **ResourceNameContains**參數：

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget 在資源群組中，所有的 hello 資源提供 hello **ResourceGroupNameContains**參數：

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget 使用標記名稱和值，所有的 hello 資源提供 hello **TagName**和**TagValue**參數：

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* tooall hello 資源的特定資源類型，提供 hello **ResourceType**參數：

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>鎖定資源

當您需要確定重要的資源不會意外刪除或修改 toomake 時，套用鎖定 toohello 資源。 您可以指定 **CanNotDelete** 或 **ReadOnly**。

toocreate 或刪除管理鎖定，您必須能夠存取太`Microsoft.Authorization/*`或`Microsoft.Authorization/locks/*`動作。 Hello 內建角色中，只有擁有者和使用者存取系統管理員會授與這些動作。

tooapply 鎖定，請使用下列 cmdlet 的 hello:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

hello hello 前面範例中的鎖定的資源，才能刪除移除 hello 鎖定為止。 tooremove 鎖定，請使用：

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

如需設定鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](resource-group-lock-resources.md)。

## <a name="remove-resources-or-resource-group"></a>移除資源或資源群組
您可以移除資源或資源群組。 當您移除資源群組時，也會移除該資源群組中的所有 hello 資源。

* 將資源從 hello 資源群組中，使用 hello toodelete**移除 AzureRmResource** cmdlet。 這個指令程式刪除 hello 資源，但不會刪除 hello 資源群組。

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete 資源群組和其所有資源，使用 hello**移除 AzureRmResourceGroup** cmdlet。

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

針對這兩個 cmdlet，系統會要求您 tooconfirm 且想 tooremove hello 資源或資源群組。 如果 hello 作業已成功刪除 hello 資源或資源群組，它會傳回**True**。

## <a name="run-resource-manager-scripts-with-azure-automation"></a>使用 Azure 自動化執行 Resource Manager 指令碼

本主題說明如何使用 Azure PowerShell 資源的 tooperform 基本作業。 更進階的管理案例，您通常會想 toocreate 指令碼，而且重複使用該指令碼，視需要或依排程。 [Azure 自動化](../automation/automation-intro.md)提供一個方法，讓您管理 Azure 解決方案的常用 tooautomate 指令碼。

hello 下列主題將示範如何 toouse Azure 自動化中，資源管理員和 PowerShell tooeffectively 執行管理工作：

- 如需建立 Runbook 的相關資訊，請參閱[我的第一個 PowerShell Runbook](../automation/automation-first-runbook-textual-powershell.md)。
- 如需使用指令碼資源庫的相關資訊，請參閱[Azure 自動化的 Runbook 和模組資源庫](../automation/automation-runbook-gallery.md)。
- 啟動和停止虛擬機器的 runbook，請參閱[Azure 自動化案例： 使用 JSON 格式的標記 toocreate Azure VM 啟動或關閉排程](../automation/automation-scenario-start-stop-vm-wjson-tags.md)。
- 如需於下班時間啟動和停止虛擬機器的 Runbook，請參閱[於下班時間自動化啟動/停止 VM 的解決方案](../automation/automation-solution-vm-management.md)。

## <a name="next-steps"></a>後續步驟
* toolearn 有關建立資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toolearn 有關部署範本，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。
* 您可以移動現有資源 tooa 新資源群組。 如需範例，請參閱[移動資源 tooNew 資源群組或訂用帳戶](resource-group-move-resources.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

