---
title: "aaaWeb 應用程式複製使用 PowerShell"
description: "深入了解如何 tooclone Web 應用程式 toonew Web 應用程式使用 PowerShell。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>使用 PowerShell 複製 Azure App Service App
與 Microsoft Azure PowerShell hello 版本 1.1.0 版的新選項已加入 tooNew AzureRMWebApp、 可讓現有的 Web 應用程式 tooa 新建立的應用程式在不同的區域或 hello hello 使用者 hello 能力 tooclone 相同的區域。 這可讓客戶 toodeploy 的應用程式的數字跨越不同地區，快速且輕鬆地。

應用程式複製目前僅支援 Premium 層 App Service 方案。 新功能使用 hello hello 相同限制 Web 應用程式備份功能，請參閱 <<c0> [ 備份 web 應用程式在 Azure App Service 中](web-sites-backup.md)。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

有關使用 Azure Resource Manager toolearn 基礎的 Azure PowerShell cmdlet toomanage 您 Web 應用程式的簽入[Azure 資源管理員的 Azure Web 應用程式架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>複製現有的應用程式
案例： 在美國中南部地區中的現有 web 應用程式，hello 使用者希望 tooclone hello 內容 tooa 新 web 應用程式在美國中北部地區。 這可以透過 hello Azure 資源管理員版本 hello PowerShell cmdlet toocreate 新的 web 應用程式與 hello-SourceWebApp 選項完成。

了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式的資訊 （在此情況下名為來源 webapp） hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

新的 App Service 方案 toocreate，我們可以使用如 hello 下列範例所示新增 AzureRmAppServicePlan 命令

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

使用 hello 新增 AzureRmWebApp 命令，我們可以在 hello 美國中北部區域中，建立 hello 新 web 應用程式，並將它連接 tooan App Service 方案現有 premium 層，此外，我們也可以使用相同的資源群組為 hello 來源 web 應用程式，或定義新的資源群組的 hellohello 下列示範：

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

包括所有相關聯的部署位置的現有 web 應用程式，hello 使用者將需要 toouse tooclone hello IncludeSourceWebAppSlots 參數，下列 PowerShell 命令的 hello 示範 hello 使用該參數以 hello 新增 AzureRmWebApp 命令：

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone hello 內現有的 web 應用程式相同的區域，hello 使用者將需要新的資源群組和新的應用程式服務計劃在 hello toocreate 相同的區域，然後使用下列 PowerShell 命令 tooclone hello web 應用程式的 hello

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>複製現有的應用程式 tooan App Service 環境
案例： 在美國中南部地區中的現有 web 應用程式，hello 使用者希望 tooclone hello 內容 tooa 新 web 應用程式 tooan 現有應用程式服務環境 (ASE)。

了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式的資訊 （在此情況下名為來源 webapp） hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

了解 hello ASE 名稱和 hello hello ASE 所屬的資源群組名稱，hello 使用者可以使用 toocreate hello 新 web 應用程式在 hello 現有 ASE，遵循 hello 示範 hello 新增 AzureRmWebApp 命令：

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

hello 位置參數是必要項，因為 toolegacy 原因，但 hello 案例在 ase 中建立應用程式將會忽略它。 

## <a name="cloning-an-existing-app-slot"></a>複製現有的應用程式位置
案例： hello 使用者希望 tooclone 現有的 Web 應用程式位置 tooeither 新的 Web 應用程式或新的 Web 應用程式位置。 新的 Web 應用程式可以在 hello hello 與 hello 原始 Web 應用程式的位置，或不同區域中相同的區域。

了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式位置的資訊 （在此情況下名為來源 webappslot） 繫結 tooWeb 應用程式來源 webapp hello:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

hello 下列示範如何建立 hello 來源 web 應用程式 tooa 新 web 應用程式的複本：

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>設定流量管理員同時複製應用程式
建立多區域 web 應用程式，並設定 Azure Traffic Manager tooroute 流量 tooall 這些 web 應用程式，會在複製您擁有現有的 web 應用程式時，客戶的應用程式是高可用性，n 的重要案例 tooinsure hello 選項 tooconnect 這兩個 web應用程式 tooeither 新的流量管理員設定檔或現有-請注意，只有 Azure 資源管理員的支援流量管理員。

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>建立新流量管理員設定檔同時複製應用程式
案例： hello 使用者希望 tooclone web 應用程式 tooanother 區域，設定 Azure 資源管理員流量管理員設定檔包含兩個 web 應用程式時。 hello 以下會示範建立複製品的 hello 來源 web 應用程式 tooa 新 web 應用程式設定新的 Traffic Manager 設定檔時：

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>加入新複製的 Web 應用程式 tooan 現有流量管理員設定檔
案例： hello 使用者已經有 Azure 資源管理員流量管理員設定檔，他希望 tooadd web 應用程式做為端點。 toodo 因此，我們必須先 tooassemble hello 現有流量管理員設定檔識別碼，我們必須 hello 訂用帳戶 id、 資源群組名稱和 hello 現有流量管理員設定檔名稱。

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

有 hello traffic manger 識別碼之後, hello 以下會示範建立 hello 來源 web 應用程式 tooa 新 web 應用程式的複製，同時將它們加入 tooan 現有流量管理員設定檔：

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>目前的限制
這項功能目前為預覽狀態，我們目前正在處理 tooadd 新功能經過一段時間，hello 清單後面是 hello hello 複製應用程式的目前版本的已知的限制：

* 不會複製自動調整設定
* 不會複製備份排程設定
* 不會複製 VNET 設定
* App Insights 不會自動上設定 hello 目的地 web 應用程式
* 不會複製簡單驗證設定
* 不會複製 Kudu 延伸模組
* 不會複製 TiP 規則
* 不會複製資料庫內容

### <a name="references"></a>參考
* [適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)
* [使用 Azure 入口網站複製 Web 應用程式](app-service-web-app-cloning-portal.md)
* [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)
* [Azure Resource Manager 的 Azure 流量管理員支援預覽](../traffic-manager/traffic-manager-powershell-arm.md)
* [簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)
* [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)

