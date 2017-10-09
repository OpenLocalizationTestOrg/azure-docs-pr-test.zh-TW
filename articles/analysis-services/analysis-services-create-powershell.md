---
title: "Azure Analysis Services 伺服器使用 PowerShell aaaCreate |Microsoft 文件"
description: "了解如何 toocreate Azure Analysis Services 伺服器使用 PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>使用 PowerShell 來建立 Azure Analysis Services 伺服器

本快速入門說明如何使用 PowerShell，從 hello 命令列 toocreate Azure Analysis Services 伺服器中的[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)您 Azure 訂用帳戶中。

此工作需要 Azure PowerShell 模組 4.0 版或更新版本。 toofind hello 版本，執行` Get-Module -ListAvailable AzureRM`。 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。 

> [!NOTE]
> 建立伺服器可能會導致新的可計費服務。 詳細資訊，請參閱 toolearn [Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。

## <a name="prerequisites"></a>必要條件
toocomplete 本快速入門中，您需要：

* **Azure 訂用帳戶**： 瀏覽[Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)toocreate 帳戶。
* **Azure Active Directory**：您的訂用帳戶必須與 Azure Active Directory 租用戶相關聯，而且您必須在該目錄中有一個帳戶。 詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。

## <a name="import-azurermanalysisservices-module"></a>Import AzureRm.AnalysisServices 模組
toocreate 訂用帳戶中的伺服器，使用 hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)元件的模組。 Hello AzureRm.AnalysisServices 模組載入您的 PowerShell 工作階段。

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>登入 tooAzure

使用 hello 登入 Azure 訂用帳戶 tooyour[新增 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount)命令。 Hello 螢幕上依照指示操作。

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>建立資源群組
 
[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)是在其中以群組方式部署與管理 Azure 資源的邏輯容器。 當您建立伺服器時，必須指定您訂用帳戶中的資源群組。 如果您還沒有資源群組，您可以建立一個新使用 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)命令。 hello 下列範例會建立名為的資源群組`myResourceGroup`hello 美國西部區域中。

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>建立伺服器

建立新的伺服器使用 hello[新增 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)命令。 hello 下列範例會建立名為 myServer myResourceGroup，在 hello 美國西部區域中，在 hello D1 層的伺服器，並指定philipc@adventureworks.com身為伺服器管理員。

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>清除資源

您可以從您的訂用帳戶移除 hello 伺服器使用 hello[移除 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)命令。 如果您繼續進行本集合中的其他快速入門和教學課程，請勿移除您的伺服器。 hello 下列範例會移除 hello hello 先前步驟中建立的伺服器。


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>後續步驟
[使用 PowerShell 管理 Azure Analysis Services](analysis-services-powershell.md)   
[從 SSDT 部署模型](analysis-services-deploy.md)   
[在 Azure 入口網站中建立模型](analysis-services-create-model-portal.md)