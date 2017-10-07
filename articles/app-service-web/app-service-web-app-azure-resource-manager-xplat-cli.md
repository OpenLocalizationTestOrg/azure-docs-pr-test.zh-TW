---
title: "aaaAzure Azure Web 應用程式的資源管理員型跨平台命令列工具 |Microsoft 文件"
description: "了解如何 toouse 會 hello 新的 Azure 資源管理員為基礎的跨平台命令列工具 toomanage Azure Web 應用程式。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>使用適用於 Azure App Service 的 Azure Resource Manager 架構 XPlat CLI
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Hello 版的 Microsoft Azure 跨平台命令列工具版本 0.10.5，已加入新的命令。 這些命令可讓 hello 使用者 hello 能力 toouse Azure 資源管理員為基礎的 PowerShell 命令 toomanage 應用程式服務。

toolearn 有關管理資源群組，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組](../azure-resource-manager/xplat-cli-azure-resource-manager.md)。 

> [!NOTE] 
> 此外，試試看[Azure CLI 2.0](https://github.com/Azure/azure-cli)、 下一代 CLI Python 撰寫 hello 資源管理部署模型。
>
>

## <a name="managing-app-service-plans"></a>管理 App Service 方案
### <a name="create-an-app-service-plan"></a>建立 App Service 方案
toocreate 的應用程式服務計劃中，使用 hello **azure appserviceplan 建立**命令。

以下是 hello 不同參數的說明：

* **-資源群組**： 包含 hello 新建立的應用程式服務計劃的資源群組。
* **-名稱**: hello 應用程式服務方案的名稱。
* **--location**：App Service 方案位置。
* **-sku**: hello 預期定價的 sku (hello 選項包括： F1 (Free)。 D1 (共用)。 B1 (基本小型)、B2 (基本中型) 和 B3 (基本大型)。 S1 (標準小型)、S2 (標準中型) 和 S3 (標準大型)。 P1 (進階小型)、P2 (進階中型) 和 P3 (進階大型)。
* **-執行個體**: hello hello （預設值為 1） 的應用程式服務方案中的背景工作數目。

範例 toouse 這個指令程式：

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>建立 Linux App Service 方案

使用 hello 相同**azure appserviceplan 建立**命令，以 hello 額外的參數**-islinux true**。 請注意 hello 事項中所述的區域[簡介 tooApp Linux 上的服務](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>列出現有的 App Service 方案
toolist hello 現有 app service 方案，使用**azure appserviceplan 清單**命令。

toolist 所有應用程式服務方案的特定資源群組下，使用：

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

使用特定的應用程式服務方案，tooget **azure appserviceplan 顯示**命令：

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>設定現有的 App Service 方案
toochange hello 設定現有的應用程式服務方案，使用 hello **azure appserviceplan config**命令。 您可以變更 hello sku 和 hello 背景工作數目 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>調整 App Service 方案
tooscale 現有應用程式服務計劃，請使用：

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>變更 hello SKU 的 App Service 方案
toochange hello sku 的現有應用程式服務計劃，使用：

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>刪除現有的 App Service 方案
toodelete 現有的應用程式服務方案，所有指派的應用程式需要 toobe 移動或刪除第一次。 然後使用 hello **azure webapp 刪除**命令，您可以刪除 hello 應用程式服務方案。

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>管理 App Service 應用程式
### <a name="create-a-web-app"></a>建立 Web 應用程式
toocreate web 應用程式，使用 hello **azure webapp 建立**命令。

以下是 hello 不同參數的說明：

* **-名稱**: hello web 應用程式的名稱。
* **-計劃**: hello 服務計劃使用 toohost hello web 應用程式名稱。
* **-資源群組**： 裝載 hello 應用程式服務計劃的資源群組。
* **-位置**: hello web 應用程式位置。

範例 toouse 這個指令程式：

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>刪除現有的應用程式
toodelete 現有的應用程式，您可以使用 hello **azure webapp 刪除**命令。 您需要 toospecify hello hello 應用程式名稱和 hello 資源群組名稱。

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>列出現有的應用程式
toolist hello 現有應用程式，請使用 hello **azure webapp 清單**命令。

toolist 特定資源群組中的所有應用程式使用：

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget 特定的應用程式，使用 hello **azure webapp 顯示**命令。

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>設定現有的應用程式
toochange hello 設定和設定現有的應用程式，以使用 hello **azure webapp 組態集**命令。

範例 (1): 變更應用程式的 hello php 版本 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

範例 (2)：新增或變更應用程式設定

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

您可以變更哪些其他組態，tooknow 使用 hello **azure webapp 組態集-h**命令。

### <a name="change-hello-state-of-an-existing-app"></a>變更現有的應用程式的 hello 狀態
#### <a name="restart-an-app"></a>重新啟動應用程式
toorestart 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>停止應用程式
toostop 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>啟動應用程式
toostart 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>管理應用程式的發行設定檔
每個應用程式具有發行設定檔可能是使用的 toopublish 您的程式碼。

#### <a name="get-publishing-profile"></a>取得發行設定檔
發行設定檔，應用程式中，使用 tooget hello:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

此命令會回應 hello 發行設定檔的使用者名稱和密碼 toohello 命令列。

### <a name="manage-app-hostnames"></a>管理應用程式主機名稱
toomanage 應用程式的主機名稱繫結使用 hello **azure webapp 設定 hostname**命令  

#### <a name="list-hostname-bindings"></a>列出主機名稱繫結
tooget hello 目前主機名稱繫結的應用程式，使用：

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>新增主機名稱繫結
tooadd 主機名稱繫結 tooan 應用程式，使用：

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>刪除主機名稱繫結
toodelete 主機名稱繫結，請使用：

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>後續步驟
* toolearn 有關 Azure 資源管理員 CLI 支援，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組。](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn 有關管理應用程式服務使用 PowerShell，請參閱[Using Azure Resource Manager-Based PowerShell tooManage Azure Web 應用程式。](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn 有關 Azure App Service on Linux，請參閱[簡介 tooApp Linux 上的服務](app-service-linux-intro.md)
