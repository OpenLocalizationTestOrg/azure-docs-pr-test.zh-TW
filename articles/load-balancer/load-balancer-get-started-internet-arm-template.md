---
title: "建立網際網路對向負載平衡器 - Azure 範本 | Microsoft Docs"
description: "了解如何使用範本在資源管理員中建立網際網路面向的負載平衡器"
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
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="91651-103">使用範本建立網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="91651-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="91651-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="91651-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="91651-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91651-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="91651-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="91651-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="91651-107">範本</span><span class="sxs-lookup"><span data-stu-id="91651-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="91651-108">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="91651-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="91651-109">您也可以 [了解如何使用傳統部署模型建立網際網路面向的負載平衡器](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="91651-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="91651-110">使用按一下即部署來部署範本</span><span class="sxs-lookup"><span data-stu-id="91651-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="91651-111">公用儲存機制中可用的範例範本會使用一個包含預設值的參數檔案，這些預設值可用來產生上述案例。</span><span class="sxs-lookup"><span data-stu-id="91651-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="91651-112">若要使用「按一下即部署」來部署此範本，請依循[此連結](http://go.microsoft.com/fwlink/?LinkId=544801)，按一下 [部署至 Azure]，視情況取代預設參數值，再依循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="91651-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="91651-113">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="91651-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="91651-114">若要使用 PowerShell 部署您下載的範本，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="91651-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="91651-115">如果您從未用過 Azure PowerShell，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) ，並遵循其中的所有指示登入 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="91651-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="91651-116">執行 **New-AzureRmResourceGroupDeployment** Cmdlet 以使用範本建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="91651-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="91651-117">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="91651-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="91651-118">若要使用 Azure CLI 部署範本，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="91651-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="91651-119">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶為止。</span><span class="sxs-lookup"><span data-stu-id="91651-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="91651-120">執行 **azure config mode** 命令，以切換為資源管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="91651-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="91651-121">此為上述命令的預期輸出內容：</span><span class="sxs-lookup"><span data-stu-id="91651-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="91651-122">從您的瀏覽器，瀏覽至[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules)，複製 json 檔案的內容並貼上到您電腦中的新檔案。</span><span class="sxs-lookup"><span data-stu-id="91651-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="91651-123">在此案例中，您會將以下的值複製到名為 **c:\lb\azuredeploy.parameters.json** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="91651-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="91651-124">執行 **azure group deployment create** Cmdlet，使用先前下載並修改的範本和參數檔案來部署新的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="91651-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="91651-125">輸出後顯示的清單可說明所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="91651-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="91651-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91651-126">Next steps</span></span>

[<span data-ttu-id="91651-127">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="91651-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="91651-128">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="91651-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="91651-129">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="91651-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
