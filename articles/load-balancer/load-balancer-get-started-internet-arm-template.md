---
title: "aaaCreate 網際網路對向負載平衡器-Azure 範本 |Microsoft 文件"
description: "了解如何 toocreate 面對網際網路的負載平衡器資源管理員 中使用的範本"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>使用範本建立網際網路面向的負載平衡器

> [!div class="op_single_selector"]
> * [入口網站](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[學習 toocreate 網際網路向負載平衡器使用傳統部署模型的方式](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>使用部署 hello 範本按一下 toodeploy

hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。 toodeploy 此範本使用按一下 toodeploy，遵循[此連結](http://go.microsoft.com/fwlink/?LinkId=544801)，按一下 **部署 tooAzure**、 取代 hello 預設參數值，如有必要，並遵循 hello 入口網站中的 hello 指示。

## <a name="deploy-hello-template-by-using-powershell"></a>使用 PowerShell 來部署 hello 範本

您使用 PowerShell 下載 toodeploy hello 範本，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。
2. 執行 hello**新增 AzureRmResourceGroupDeployment**資源群組使用的 cmdlet toocreate hello 範本。

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>使用 Azure CLI hello 部署 hello 範本

使用 Azure CLI hello toodeploy hello 範本，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。
2. 執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式，如下所示。

    ```azurecli
    azure config mode arm
    ```

    以下是 hello 上述命令中的 hello 預期輸出：

        info:    New mode is arm

3. 從瀏覽器中，瀏覽過[hello 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)、 hello hello json 檔案的內容複製和貼入新檔案中，您的電腦。 此案例中，您會被複製 hello 值 tooa 檔案命名為之下**c:\lb\azuredeploy.parameters.json**。
4. 執行 hello**建立 azure 群組部署**cmdlet toodeploy hello 新增負載平衡器使用 hello 範本和參數檔案，您可以下載並修改上方。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
