---
title: "建立內部負載平衡器 - Azure 範本 | Microsoft Docs"
description: "了解如何使用資源管理員中的範本建立內部負載平衡器"
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
ms.openlocfilehash: 5e0278cf5c605298932d6ac55d147a1c43fd9d23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="0e51a-103">使用範本建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="0e51a-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e51a-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0e51a-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="0e51a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e51a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="0e51a-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e51a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="0e51a-107">範本</span><span class="sxs-lookup"><span data-stu-id="0e51a-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0e51a-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0e51a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0e51a-109">本文涵蓋內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="0e51a-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="0e51a-110">使用按一下即部署來部署範本</span><span class="sxs-lookup"><span data-stu-id="0e51a-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="0e51a-111">公用儲存機制中可用的範例範本會使用一個包含預設值的參數檔案，這些預設值可用來產生上述案例。</span><span class="sxs-lookup"><span data-stu-id="0e51a-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="0e51a-112">若要使用「按一下即部署」來部署此範本，請依循[此連結](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)，按一下 [部署至 Azure]，視情況取代預設參數值，再依循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="0e51a-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="0e51a-113">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="0e51a-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="0e51a-114">若要使用 PowerShell 部署您下載的範本，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="0e51a-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="0e51a-115">如果您從未用過 Azure PowerShell，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) ，並遵循其中的所有指示登入 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e51a-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="0e51a-116">將參數檔案下載至本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="0e51a-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="0e51a-117">編輯並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="0e51a-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="0e51a-118">執行 **New-AzureRmResourceGroupDeployment** Cmdlet 以使用範本建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="0e51a-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="0e51a-119">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="0e51a-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="0e51a-120">若要使用 Azure CLI 部署範本，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="0e51a-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="0e51a-121">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶為止。</span><span class="sxs-lookup"><span data-stu-id="0e51a-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0e51a-122">執行 **azure config mode** 命令，以切換為資源管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0e51a-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="0e51a-123">此為上述命令的預期輸出內容：</span><span class="sxs-lookup"><span data-stu-id="0e51a-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="0e51a-124">開啟參數檔案，選取其內容，然後將該內容儲存至您電腦中的一個檔案。</span><span class="sxs-lookup"><span data-stu-id="0e51a-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="0e51a-125">在此範例中，我們將參數檔案儲存為 *parameters.json*。</span><span class="sxs-lookup"><span data-stu-id="0e51a-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="0e51a-126">執行 **azure group deployment create** 命令，使用先前下載並修改的範本和參數檔案來部署新的內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="0e51a-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="0e51a-127">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="0e51a-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="0e51a-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e51a-128">Next steps</span></span>

[<span data-ttu-id="0e51a-129">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="0e51a-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0e51a-130">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="0e51a-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

