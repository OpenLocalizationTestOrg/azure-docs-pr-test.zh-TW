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
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="518e1-103">使用範本建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="518e1-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="518e1-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="518e1-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="518e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="518e1-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="518e1-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="518e1-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="518e1-107">範本</span><span class="sxs-lookup"><span data-stu-id="518e1-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="518e1-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="518e1-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="518e1-109">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="518e1-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="518e1-110">使用部署 hello 範本按一下 toodeploy</span><span class="sxs-lookup"><span data-stu-id="518e1-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="518e1-111">hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="518e1-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="518e1-112">toodeploy 此範本使用按一下 toodeploy，遵循[此連結](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)，按一下 **部署 tooAzure**、 取代 hello 預設參數值，如有必要，並遵循 hello 入口網站中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="518e1-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="518e1-113">使用 PowerShell 來部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="518e1-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="518e1-114">您使用 PowerShell 下載 toodeploy hello 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="518e1-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="518e1-115">如果您從未使用過 Azure PowerShell，請參閱[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示所有 hello 方式 toohello 結束 toosign 至 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="518e1-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="518e1-116">下載 hello 參數檔案 tooyour 本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="518e1-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="518e1-117">編輯 hello 檔案，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="518e1-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="518e1-118">執行 hello**新增 AzureRmResourceGroupDeployment**資源群組使用的 cmdlet toocreate hello 範本。</span><span class="sxs-lookup"><span data-stu-id="518e1-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="518e1-119">使用 Azure CLI hello 部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="518e1-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="518e1-120">使用 Azure CLI hello toodeploy hello 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="518e1-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="518e1-121">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="518e1-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="518e1-122">執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="518e1-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="518e1-123">以下是 hello 上述命令中的 hello 預期輸出：</span><span class="sxs-lookup"><span data-stu-id="518e1-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="518e1-124">開啟 hello 參數檔案、 選取它的內容，然後它 tooa 將檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="518e1-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="518e1-125">對於此範例中，我們儲存 hello 參數檔案太*parameters.json*。</span><span class="sxs-lookup"><span data-stu-id="518e1-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="518e1-126">執行 hello**建立 azure 群組部署**toodeploy hello 新的內部負載平衡器使用 hello 範本和參數的命令檔您下載並修改上方。</span><span class="sxs-lookup"><span data-stu-id="518e1-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="518e1-127">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="518e1-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="518e1-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="518e1-128">Next steps</span></span>

[<span data-ttu-id="518e1-129">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="518e1-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="518e1-130">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="518e1-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

