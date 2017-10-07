---
title: "aaaResource 管理員和服務管理 （傳統） 部署模式 |Microsoft 文件"
description: "了解 hello 資源管理員和傳統部署模型之間的差異。"
services: virtual-network
documentationcenter: 
author: telmosampaio
manager: carmonm
editor: 
tags: azure-resource-manager,azure-service-management
redirect_url: ./azure-resource-manager/resource-manager-deployment-model
ms.assetid: 18a235d8-38ac-4886-9e56-b3855c73ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: telmos
ms.openlocfilehash: e14f815ba9d79d9dd8f83b45bda78d0eba0bec56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-deployment-models"></a>Azure 部署模型
正在轉換中的 hello Azure 平台。  您是新 tooAzure，或已在使用它多年來，它是否重要 toounderstand hello 金鑰變更的某些我們正在 toohello 平台在此轉換。

所有的 Azure 資源支援的一或兩個下列部署模型的 hello:

* **資源管理員：**這是 Azure 資源的 hello 最新部署模型。 大部分較新的資源都已支援這種部署模型，最後所有資源都會提供支援。   
* **傳統︰** 現在大部分現有的 Azure 資源都支援此模型。 TooAzure 將不支援此模型中加入新的資源。

可以使用建立每個 Azure 資源的詳細資料的服務模型，它的 hello 文件。

## <a name="why-does-this-matter"></a>為何這有關係？
重要的 hello 下列原因：

* hello Azure 平台功能，讓您用這兩個模型都不同。  例如，建立使用 hello Resource Manager 部署模型 （或只是資源管理員） 建立的資源與[Azure 資源管理員範本](azure-resource-manager/resource-group-overview.md#template-deployment)，而無法建立與 hello 傳統部署模型的資源。
* hello 個別 Azure 資源的功能或行為可以有差異 hello 兩個模型，或只存在於一個模型或其他 hello。  例如，負載平衡與 hello 傳統部署模型所建立的虛擬機器的流量是*隱含*因為虛擬機器是 Azure 雲端服務的成員，而且負載自動平衡虛擬雲端服務內的電腦。 使用資源管理員所建立的虛擬機器不是雲端服務的成員，而且必須是不同的 Azure 負載平衡器資源*明確*在多部虛擬機器上建立 tooload 平衡流量。  
* 在這兩種模型中，建立、設定及管理 Azure 資源的方式有所不同。
* 使用一種部署模型所建立的資源，不一定能與使用不同部署模型建立的資源交互操作。 例如，使用一種部署模型所建立的 Azure 虛擬機器只能連接的 tooAzure 使用 hello 所建立的虛擬網路相同的部署模型。    

每個 hello 部署模型資料是每個資源應用程式開發介面 (API)。  沒有[資源管理員 API](https://msdn.microsoft.com/library/azure/dn948464.aspx) hello 資源管理員部署模型和[服務管理 API](https://msdn.microsoft.com/library/azure/ee460799.aspx) hello 傳統部署模型。 開發人員可以撰寫程式碼使用這些 Api 的 toointeract*直接*。  

IT 專業人員不過，通常與互動，這些 Api*間接*透過圖形化的入口網站 web 瀏覽器中，使用 Azure PowerShell cmdlet 的 Windows 電腦上，或使用 hello Azure 命令列介面 (CLI) 上Windows、 OS X 或 Linux 電腦。 所有這三種 hello IT 專業人員所使用的間接方法直接互動 hello 應用程式開發介面。 這表示當新的功能是導入了的 toohello Azure 平台或資源，一律直接 hello 應用程式開發介面透過第一次，與 hello 間接方法取得 hello 支援新的資源，而且之後 hello 應用程式開發介面都可以提供的功能。  

hello 的以下各節說明如何在 Azure 資源是透過 hello 三個間接方法使用 hello 不同的部署模型所設定。

## <a name="portals"></a>入口網站
Azure 有兩個入口網站︰

* **[Azure 入口網站](https://manage.windowsazure.com)：**如果您已使用 Azure 一段時間，您便已使用過此入口網站。 它是使用的 toocreate 並設定支援 hello 傳統部署模型的較舊 Azure 資源。 您無法使用它 toocreate，或是設定僅支援資源管理員的資源。 
* **[Azure Preview 入口網站](https://azure.microsoft.com/overview/preview-portal/)：**如果您使用較新的 Azure 資源，您可能已使用過此入口網站。 可以使用的 toocreate 並設定一些 Azure 資源。 最終將會無法 toocreate，並使用它來設定所有的 Azure 資源。 支援兩種部署模型的一些資源，這個入口網站可以使用的 toocreate，而且使用這兩種部署模式將資源設定。 

某些資源和功能可以只建立並設定一個入口網站或其他 hello。 某些資源或功能 （尚未） 無法建立或設定在任一個入口網站和只能使用 PowerShell 設定，hello CLI，或兩者。 每一項 Azure 資源的 hello 文件詳細說明可以使用建立哪一種方法。 

## <a name="powershell"></a>PowerShell
與[PowerShell](/powershell/azureps-cmdlets-docs)您可以使用命令列或撰寫的指令碼 toocreate 並設定從 Windows 電腦的 Azure 資源。  個別 Azure 資源具有 [Resource Manager Cmdlet](/powershell/azure/overview)、[服務管理 Cmdlet](/powershell/azure/overview?view=azuresmps-3.7.0)，或兩者兼具。  某些資源和功能，只可以建立及/或使用 PowerShell 或 hello CLI 設定。 使用資源管理員 PowerShell cmdlet 時，視 hello 資源，您可能需要兩個選項用於建立及設定 Azure 資源：

* **PowerShell 指令程式僅：**您可以建立並設定每個個別使用適用於每個資源 hello cmdlet 的 Azure 資源。 從命令列執行這項操作，或在 PowerShell 指令碼中包含您可儲存和設定版本的多個命令。
* **使用 Azure Resource Manager 範本的 PowerShell cmdlet:**您可以使用 PowerShell toocreate Azure 使用 Azure Resource Manager 範本的資源。 範本可予以儲存及設定版本。 進一步了解藉由讀取 hello[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)發行項。 常見解決方案也有數個 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/) 可供下載和修改。

## <a name="cli"></a>CLI
您可以建立和設定從 Windows、 OS X 或 Linux 電腦使用 hello CLI Azure 資源。  讀取 hello[安裝 hello Azure CLI](cli-install-nodejs.md)選擇的作業系統上的發行項 tooinstall hello CLI。 類似 PowerShell 中，有不同的命令必須根據您是否建立使用的資源使用[資源管理員](xplat-cli-azure-resource-manager.md)或 hello[傳統 （服務管理）](virtual-machines/linux/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)部署模型。

## <a name="next-steps"></a>後續步驟
* 深入了解 [Resource Manager](azure-resource-manager/resource-group-overview.md)。
* 了解如何太[設計範本](best-practices-resource-manager-design-templates.md)。

