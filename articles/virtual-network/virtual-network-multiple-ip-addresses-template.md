---
title: "Azure 虛擬機器範本的 aaaMultiple IP 位址 |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址使用 Azure Resource Manager 範本 tooa 虛擬機器。"
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本 toovirtual 機器指派多個 IP 位址

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

本文說明如何透過 hello Azure Resource Manager 部署的虛擬機器 (VM) toocreate 模型使用資源管理員範本。 多個公用和私用 IP 位址不能指派 toohello 部署 VM，以透過 hello 傳統部署模型時相同的 NIC。 深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>範本描述

部署範本可讓您 tooquickly 和一致地使用不同的組態值建立 Azure 資源。 讀取 hello[資源管理員範本逐步解說](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項，如果您不熟悉 Azure Resource Manager 範本。 hello[部署具有多個 IP 位址的 VM](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig)範本利用這份文件中。

<a name="resources"></a>部署的 hello 範本會建立 hello 下列資源：

|資源|名稱|說明|
|---|---|---|
|網路介面|myNic1|hello 這篇文章 hello 案例一節所述三種 IP 設定會建立並指派 toothis nic。|
|公用 IP 位址資源|會建立 2 個：myPublicIP 和 myPublicIP2|這些資源會指派靜態公用 IP 位址，而指派 toohello *IPConfig 1*和*IPConfig 2* hello 案例中所描述的 IP 組態。|
|VM|myVM1|標準 DS3 VM。|
|虛擬網路|myVNet1|具有一個名為 mySubnet 子網路的虛擬網路。|
|儲存體帳戶|唯一 toohello 部署|儲存體帳戶。|

<a name="parameters"></a>在部署 hello 範本時，您必須指定 hello 下列參數的值：

|名稱|說明|
|---|---|
|adminUsername|系統管理員使用者名稱。 hello 使用者名稱必須遵守[Azure 使用者名稱需求](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。|
|adminPassword|系統管理員密碼 hello 密碼必須符合的[Azure 密碼需求](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm)。|
|dnsLabelPrefix|PublicIPAddressName1 的 DNS 名稱。 hello DNS 名稱會解析 tooone hello 分派 toohello VM 公用 IP 位址。 hello 名稱內必須是唯一 hello Azure 區域 （位置），您建立 hello VM 中的。|
|dnsLabelPrefix1|PublicIPAddressName2 的 DNS 名稱。 hello DNS 名稱會解析 tooone hello 分派 toohello VM 公用 IP 位址。 hello 名稱內必須是唯一 hello Azure 區域 （位置），您建立 hello VM 中的。|
|OSVersion|hello hello VM 的 Windows/Linux 版本。 hello 作業系統是指定所選取的 Windows/Linux 版本 hello 的完整修補的影像。|
|imagePublisher|hello hello Windows/Linux 映像發行者選取 VM。|
|imageOffer|hello Windows/Linux 映像選取 VM。|

每個 hello 範本所部署的 hello 資源已設定數個預設設定。 您可以檢視這些設定 hello 下列方法其中之一：

- **GitHub 上的檢視 hello 範本：**如果您是熟悉使用範本，您可以檢視內 hello hello 設定[範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json)。
- **部署後檢視 hello 設定：**如果您不熟悉範本，您可以部署 hello 範本使用中的下列各節的 hello 其中一個步驟，然後在部署後檢視 hello 設定。

您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure 命令列介面 (CLI) toodeploy hello 範本。 所有的方法會產生 hello 相同的結果。 toodeploy hello 範本，其中一種 hello 下列各節的步驟完成 hello:

## <a name="deploy-using-hello-azure-portal"></a>使用 hello Azure 入口網站部署

toodeploy hello 範本使用 hello Azure 入口網站完成 hello 下列步驟：

1. 視需要修改 hello 範本。 hello 範本部署的 hello 資源和設定列在 hello[資源](#resources)本文一節。 toolearn 更多關於範本以及如何 tooauthor 它們，請讀取的 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。
2. 部署 hello 範本 hello 下列方法之一：
    - **選取 hello hello 入口網站中的範本：** hello 中步驟的完整 hello[部署資源的自訂範本](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template)發行項。 選擇 hello 預先存在的範本，名為*101 vm 的多個 ipconfig*。
    - **直接：**按一下下列按鈕 tooopen hello 範本，直接在 hello 入口網站中的 hello:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

不論 hello 方法您選擇，您將需要 toosupply 值 hello[參數](#parameters)本文先前所列。 Hello VM 部署之後，連接 toohello VM，並將 hello 私用 IP 位址 toohello 您部署作業系統藉由完成 hello 步驟 hello[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

## <a name="deploy-using-powershell"></a>使用 PowerShell 進行部署

使用 PowerShell，完成下列步驟的 hello toodeploy hello 範本：

1. Hello hello 中的步驟，以部署 hello 範本[部署範本，以使用 PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md)發行項。 hello 文章說明多個選項，以部署範本。 如果您選擇使用 hello toodeploy `-TemplateUri parameter`，hello URI，此範本是*https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*。 如果您選擇使用 hello toodeploy`-TemplateFile`參數，複製 hello 內容 hello[範本檔案](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json)從 GitHub 到您的電腦上的新檔案。 視需要修改 hello 範本內容。 hello 範本部署的 hello 資源和設定列在 hello[資源](#resources)本文一節。 toolearn 更多關於範本以及如何 tooauthor 它們，請讀取的 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)發行項。

    不論您選擇具有 toodeploy hello 範本 hello 選項，您必須提供的值列在 hello hello 參數值[參數](#parameters)本文一節。 如果您選擇 toosupply 參數使用的參數檔案，複製 hello hello 內容[參數檔案](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json)從 GitHub 到您的電腦上的新檔案。 修改 hello hello 檔案中的值。 您建立 hello hello 值為使用 hello 檔案`-TemplateParameterFile`參數。

    toodetermine hello OSVersion、 ImagePublisher 和 imageOffer 參數的有效值，hello 步驟完成 hello[瀏覽和選取的 Windows VM 映像發行項](../virtual-machines/windows/cli-ps-findimage.md)發行項。

    >[!TIP]
    >如果您不確定是否 dnslabelprefix 可供使用，請輸入 hello`Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>`命令 toofind 出。如果是可用，hello 命令會傳回`True`。

2. Hello VM 部署之後，連接 toohello VM，並將 hello 私用 IP 位址 toohello 您部署作業系統藉由完成 hello 步驟 hello[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

## <a name="deploy-using-hello-azure-cli"></a>使用 Azure CLI hello 部署

使用 Azure CLI 1.0，完成下列步驟的 hello hello toodeploy hello 範本：

1. Hello hello 中的步驟，以部署 hello 範本[部署範本以 hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)發行項。 hello 文章說明多個部署 hello 範本選項。 如果您選擇使用 hello toodeploy `--template-uri` (-f)，此範本是 hello URI *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*。 如果您選擇使用 hello toodeploy `--template-file` (-f) 參數，複製 hello 內容 hello[範本檔案](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json)從 GitHub 到您的電腦上的新檔案。 視需要修改 hello 範本內容。 hello 範本部署的 hello 資源和設定列在 hello[資源](#resources)本文一節。 toolearn 更多關於範本以及如何 tooauthor 它們，請讀取的 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)發行項。

    不論您選擇具有 toodeploy hello 範本 hello 選項，您必須提供的值列在 hello hello 參數值[參數](#parameters)本文一節。 如果您選擇 toosupply 參數使用的參數檔案，複製 hello hello 內容[參數檔案](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json)從 GitHub 到您的電腦上的新檔案。 修改 hello hello 檔案中的值。 您建立 hello hello 值為使用 hello 檔案`--parameters-file`(-e) 參數。

    toodetermine hello OSVersion、 ImagePublisher 和 imageOffer 參數的有效值，hello 步驟完成 hello[瀏覽和選取的 Windows VM 映像發行項](../virtual-machines/windows/cli-ps-findimage.md)發行項。

2. Hello VM 部署之後，連接 toohello VM，並將 hello 私用 IP 位址 toohello 您部署作業系統藉由完成 hello 步驟 hello[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
