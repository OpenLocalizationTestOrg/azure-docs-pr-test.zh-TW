---
title: "aaaAzure 資源管理員為基礎的 PowerShell 命令的 Azure Web 應用程式 |Microsoft 文件"
description: "了解如何 toouse 會 hello 新的 Azure 資源管理員為基礎的 PowerShell 命令 toomanage Azure Web 應用程式。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>使用 Azure Resource Manager-Based PowerShell tooManage Azure Web 應用程式
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

與 Microsoft Azure PowerShell 1.0.0 版新命令已經加入，可提供 hello 使用者 hello 能力 toouse Azure 資源管理員為基礎的 PowerShell 命令 toomanage Web 應用程式。

toolearn 有關管理資源群組，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。 

toolearn 有關 hello 的參數與 hello PowerShell 指令程式選項的完整清單，請參閱 「 hello[完整的 Web 應用程式的 Azure 資源管理員為基礎的 PowerShell Cmdlet 的 Cmdlet 參考](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>管理 App Service 方案
### <a name="create-an-app-service-plan"></a>建立 App Service 方案
toocreate 的應用程式服務計劃中，使用 hello**新增 AzureRmAppServicePlan** cmdlet。

以下是 hello 不同參數的說明：

* **名稱**: hello 應用程式服務方案的名稱。
* **Location**：服務方案名稱。
* **ResourceGroupName**： 包含 hello 新建立的應用程式服務計劃的資源群組。
* **層**: hello 預期定價層 （預設值是免費、 共用、 Basic、 Standard 和 Premium，其他選項包括）。
* **WorkerSize**: hello 大小的背景工作 （預設值為小型 hello 層參數指定為 Basic、 Standard 或 Premium。 其他選項為 [中型] 和 [大型])。
* **NumberofWorkers**: hello hello （預設值為 1） 的應用程式服務方案中的背景工作數目。 

範例 toouse 這個指令程式：

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>在 App Service 環境中建立 App Service 方案
toocreate 應用程式服務計劃在 app service 環境中，使用 hello 相同命令**新增 AzureRmAppServicePlan**命令 ASE 的資源群組名稱與額外的參數 toospecify hello ASE 的名稱。

範例 toouse 這個指令程式：

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

深入了解應用程式服務環境中，核取 toolearn[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>列出現有的 App Service 方案
toolist hello 現有 app service 方案，使用**Get AzureRmAppServicePlan** cmdlet。

toolist 使用您的訂用帳戶，底下的所有應用程式服務方案： 

    Get-AzureRmAppServicePlan

toolist 所有應用程式服務方案的特定資源群組下，使用：

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget 特定的應用程式服務方案，請使用：

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>設定現有的 App Service 方案
toochange hello 設定現有的應用程式服務方案，使用 hello**組 AzureRmAppServicePlan** cmdlet。 您可以變更 hello 層、 背景工作大小和 hello 背景工作數目 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>調整 App Service 方案
tooscale 現有應用程式服務計劃，請使用：

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>變更 hello 背景工作大小的 App Service 方案
toochange hello 中現有的應用程式服務計劃，使用背景工作大小：

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>變更 hello 層的 App Service 方案
toochange hello 層現有應用程式服務計劃，使用：

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>刪除現有的 App Service 方案
toodelete 現有的應用程式服務方案，所有指派給 web 應用程式需要 toobe 移動或刪除第一次。 然後使用 hello**移除 AzureRmAppServicePlan** cmdlet，您可以刪除 hello 應用程式服務方案。

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>管理 App Service Web Apps
### <a name="create-a-web-app"></a>建立 Web 應用程式
toocreate web 應用程式，使用 hello**新增 AzureRmWebApp** cmdlet。

以下是 hello 不同參數的說明：

* **名稱**: hello web 應用程式的名稱。
* **AppServicePlan**: hello 服務計劃使用 toohost hello web 應用程式名稱。
* **ResourceGroupName**： 裝載 hello 應用程式服務計劃的資源群組。
* **位置**: hello web 應用程式位置。

範例 toouse 這個指令程式：

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>在 App Service 環境中建立 Web 應用程式
toocreate web 應用程式中的應用程式服務環境 (ASE)。 使用 hello 相同**新增 AzureRmWebApp**命令額外參數 toospecify hello ASE 名稱與 hello hello ASE 所屬的資源群組名稱。

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

深入了解應用程式服務環境中，核取 toolearn[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>刪除現有的 Web 應用程式
現有的 web 應用程式可以使用 hello toodelete**移除 AzureRmWebApp** cmdlet，您需要 toospecify hello hello web 應用程式名稱和 hello 資源群組名稱。

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>列出現有的 Web Apps
toolist hello 現有 web 應用程式，使用 hello **Get AzureRmWebApp** cmdlet。

toolist 您訂用帳戶，底下的所有 web 應用程式都使用：

    Get-AzureRmWebApp

toolist 所有 web 應用程式的特定資源群組下，都使用：

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget 是特定 web 應用程式中，使用：

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>設定現有的 Web 應用程式
toochange hello 設定與現有的 web 應用程式的組態使用 hello**組 AzureRmWebApp** cmdlet。 如需參數的完整清單，請檢查 hello[指令程式參考連結](https://msdn.microsoft.com/library/mt652487.aspx)

範例 (1): 使用這個指令程式 toochange 連接字串

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

範例 (2)：新增或變更應用程式設定

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


範例 (3): 在 64 位元模式中設定 hello web 應用程式 toorun

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>變更現有的 Web 應用程式的 hello 狀態
#### <a name="restart-a-web-app"></a>重新啟動 Web 應用程式
toorestart web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>停止 Web 應用程式
toostop web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>啟動 Web 應用程式
toostart web 應用程式，您必須指定 hello hello web 應用程式的名稱和資源群組。

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>管理 Web 應用程式發行設定檔
每個 web 應用程式的發行設定檔可能是使用的 toopublish 您的應用程式，在發行設定檔上執行數項作業。

#### <a name="get-publishing-profile"></a>取得發行設定檔
發行 web 應用程式中，使用的設定檔的 tooget hello:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

此命令會回應 hello 發行設定檔 toohello 命令列也會輸出 hello 發行設定檔 tooa 文字檔案。

#### <a name="reset-publishing-profile"></a>重設發行設定檔
tooreset 兩者 hello 發行密碼，如 FTP 和 web deploy web 應用程式中，使用：

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>管理 Web 應用程式憑證
toolearn 有關 toomanage web 應用程式的憑證，請參閱[SSL 憑證繫結使用 PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>後續步驟
* toolearn 有關 Azure 資源管理員 PowerShell 支援，請參閱[使用 Azure PowerShell 的 Azure 資源管理員。](../powershell-azure-resource-manager.md)
* toolearn 有關應用程式服務環境，請參閱[簡介 tooApp Service 環境。](app-service-app-service-environment-intro.md)
* toolearn 有關管理應用程式服務 SSL 憑證，使用 PowerShell，請參閱[使用 PowerShell 的 SSL 憑證繫結。](app-service-web-app-powershell-ssl-binding.md)
* 請參閱 toolearn hello 的 Azure Web 應用程式，Azure 資源管理員為基礎的 PowerShell cmdlet 的完整清單的相關[Azure 指令程式參考的 Web 應用程式的 Azure 資源管理員 PowerShell Cmdlet。](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn 有關管理應用程式服務使用 CLI，請參閱[Using Azure Resource Manager-Based XPlat CLI Azure Web 應用程式。](app-service-web-app-azure-resource-manager-xplat-cli.md)

