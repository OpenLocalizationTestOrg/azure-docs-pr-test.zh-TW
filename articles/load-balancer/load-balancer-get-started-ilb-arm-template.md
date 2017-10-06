---
title: "aaaCreate 內部負載平衡器-Azure 範本 |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器使用的範本資源管理員 中的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a>使用範本建立內部負載平衡器

> [!div class="op_single_selector"]
> * [Azure 入口網站](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>使用部署 hello 範本按一下 toodeploy

hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。 toodeploy 此範本使用按一下 toodeploy，遵循[此連結](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)，按一下 **部署 tooAzure**、 取代 hello 預設參數值，如有必要，並遵循 hello 入口網站中的 hello 指示。

## <a name="deploy-hello-template-by-using-powershell"></a>使用 PowerShell 來部署 hello 範本

您使用 PowerShell 下載 toodeploy hello 範本，請遵循下列 hello 步驟。

1. 如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。
2. 下載 hello 參數檔案 tooyour 本機磁碟。
3. 編輯 hello 檔案，並將其儲存。
4. 執行 hello**新增 AzureRmResourceGroupDeployment**資源群組使用的 cmdlet toocreate hello 範本。

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
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

3. 開啟 hello 參數檔案、 選取它的內容，然後它 tooa 將檔案儲存在您的電腦。 對於此範例中，我們儲存 hello 參數檔案太*parameters.json*。
4. 執行 hello**建立 azure 群組部署**toodeploy hello 新的內部負載平衡器使用 hello 範本和參數的命令檔您下載並修改上方。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>後續步驟

[使用來源 IP 同質性設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)

