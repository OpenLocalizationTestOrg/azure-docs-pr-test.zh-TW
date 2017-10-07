---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>建立私用 Docker 容器登錄中使用 hello Azure PowerShell
使用中的命令[Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate 容器登錄中，從您的 Windows 電腦管理其設定。 您也可以建立及管理使用 hello 容器登錄[Azure 入口網站](container-registry-get-started-portal.md)，hello [Azure CLI](container-registry-get-started-azure-cli.md)，或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)。


* 背景和概念，請參閱[hello 概觀](container-registry-intro.md)
* 如需支援的 Cmdlet 完整清單，請參閱 [Azure 容器登錄管理 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)。


## <a name="prerequisites"></a>必要條件
* **Azure PowerShell**: tooinstall 和開始使用 Azure PowerShell，請參閱 hello[安裝指示](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)。 執行登入 Azure 訂用帳戶 tooyour `Login-AzureRMAccount`。 如需詳細資訊，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)。
* **資源群組**：先建立[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)再建立容器登錄，或使用現有的資源群組。 請確定 hello 資源群組是在 hello 容器登錄服務所在的位置[可用](https://azure.microsoft.com/regions/services/)。 toocreate 資源群組，使用 Azure PowerShell，請參閱[hello PowerShell 參考](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)。
* **儲存體帳戶**（選擇性）： 建立標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)tooback hello 容器登錄中 hello 相同的位置。 如果您未指定儲存體帳戶時建立登錄中的以`New-AzureRMContainerRegistry`，hello 命令為您建立一個。 toocreate 儲存體帳戶使用 PowerShell，請參閱[hello PowerShell 參考](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)。 目前不支援進階儲存體。
* **服務主體** (選用)：當您使用 PowerShell 建立登錄時，依預設不會針對存取進行設定。 根據您的需求，您可以指派現有的 Azure Active Directory 服務主體 tooa 登錄或建立並指派新的。 或者，您可以啟用 hello 登錄系統管理使用者帳戶。 請參閱本文稍後的 hello 章節。 如需登錄存取權的詳細資訊，請參閱[與 hello 容器登錄中的 Authenticate](container-registry-authentication.md)。

## <a name="create-a-container-registry"></a>建立容器登錄庫
執行 hello`New-AzureRMContainerRegistry`命令 toocreate 容器登錄中。

> [!TIP]
> 當您建立登錄庫時，請指定含有字母和數字的全域唯一最上層網域名稱。 hello 範例中的 hello 登錄名稱`MyRegistry`，但以取代您自己的唯一名稱。
>
>

下列命令會使用 hello 最少參數 toocreate 容器登錄中的 hello `MyRegistry` hello 資源群組中`MyResourceGroup`hello 美國中南部位置中：

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` 為選擇性。 如果未指定，儲存體帳戶建立 hello 登錄名稱所組成的名稱，並 hello 的時間戳記指定資源群組。

## <a name="assign-a-service-principal"></a>指派服務主體
使用 Azure Active Directory 的 PowerShell 命令 tooassign[服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)tooa 登錄。 hello 這些範例中的服務主體指派 hello 擁有者角色，但您可以指派[其他角色](../active-directory/role-based-access-control-configure.md)如果您想要。

### <a name="create-a-service-principal"></a>建立服務主體
在 hello 下列命令，會建立新的服務主體。 指定強式密碼以 hello`-Password`參數。

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>指派新的或現有的服務主體
您可以指派新的或現有的服務主體 tooa 登錄。 tooassign 它擁有者角色存取 toohello 登錄中，執行下列範例命令類似 toohello:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>登入 toohello 登錄中以 hello 服務主體
之後指派 hello 服務主體 toohello 登錄，您可以使用登入 hello 下列命令：

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>管理管理員認證
系統會自動建立每個容器登錄庫的管理員帳戶，並預設停用此帳戶。 hello 下列範例顯示 PowerShell 命令的容器登錄 toomanage hello 系統管理員認證。

### <a name="obtain-admin-user-credentials"></a>取得管理員使用者認證
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>啟用現有登錄庫的管理員使用者
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>停用現有登錄庫的管理員使用者
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>後續步驟
* [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
