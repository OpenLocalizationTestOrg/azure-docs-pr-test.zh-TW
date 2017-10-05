---
title: "建立具有靜態公用 IP 位址的 VM - Azure Resource Manager 範本 | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 範本建立具有靜態公用 IP 位址的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f503aa60fdd9b7cf66ef482a1041e34c88e5c01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="a19f6-103">使用 Azure Resource Manager 範本建立具有靜態公用 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="a19f6-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a19f6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a19f6-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="a19f6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a19f6-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="a19f6-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a19f6-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="a19f6-107">範本</span><span class="sxs-lookup"><span data-stu-id="a19f6-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="a19f6-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="a19f6-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a19f6-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a19f6-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a19f6-110">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a19f6-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="a19f6-111">範本檔案中的公用 IP 資源</span><span class="sxs-lookup"><span data-stu-id="a19f6-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="a19f6-112">您可以檢視和下載 [範例範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="a19f6-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="a19f6-113">下一節根據上述案例顯示公用 IP 資源的定義：</span><span class="sxs-lookup"><span data-stu-id="a19f6-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="a19f6-114">請注意， **publicIPAllocationMethod** 屬性設定為 *Static*。</span><span class="sxs-lookup"><span data-stu-id="a19f6-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="a19f6-115">這個屬性可以是 Dynamic (預設值) 或 Static。</span><span class="sxs-lookup"><span data-stu-id="a19f6-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="a19f6-116">將它設定為 static 可確保指派的公用 IP 位址永遠不會變更。</span><span class="sxs-lookup"><span data-stu-id="a19f6-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="a19f6-117">下一節說明公用 IP 位址與網路介面的關聯：</span><span class="sxs-lookup"><span data-stu-id="a19f6-117">The following section shows the association of the public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="a19f6-118">請注意，**publicIPAddress** 屬性指向資源 **variables('webVMSetting').pipName** 的 **Id**。</span><span class="sxs-lookup"><span data-stu-id="a19f6-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="a19f6-119">這是上述公用 IP 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a19f6-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="a19f6-120">最後，上述網路介面會列在建立的 VM 的 **networkProfile** 屬性中。</span><span class="sxs-lookup"><span data-stu-id="a19f6-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="a19f6-121">使用按一下即部署來部署範本</span><span class="sxs-lookup"><span data-stu-id="a19f6-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="a19f6-122">公用儲存機制中可用的範例範本會使用一個包含預設值的參數檔案，這些預設值可用來產生上述案例。</span><span class="sxs-lookup"><span data-stu-id="a19f6-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="a19f6-123">若要使用「按一下即部署」來部署這個範本，請在[具有靜態 PIP 的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) 範本的 Readme.md 檔案中，按一下 [部署至 Azure]。</span><span class="sxs-lookup"><span data-stu-id="a19f6-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="a19f6-124">如果有需要，請取代預設參數值並輸入空白參數的值。</span><span class="sxs-lookup"><span data-stu-id="a19f6-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="a19f6-125">請遵循入口網站中的指示，利用靜態公用 IP 位址建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a19f6-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="a19f6-126">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="a19f6-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="a19f6-127">若要使用 PowerShell 部署您下載的範本，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="a19f6-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="a19f6-128">如果您從未使用過 Azure PowerShell，請完成[如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 文章中的步驟。</span><span class="sxs-lookup"><span data-stu-id="a19f6-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a19f6-129">如有必要，請在 PowerShell 主控台中執行 `New-AzureRmResourceGroup` Cmdlet，以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a19f6-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="a19f6-130">如果您已經建立資源群組，請移至步驟 3。</span><span class="sxs-lookup"><span data-stu-id="a19f6-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="a19f6-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a19f6-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="a19f6-132">在 PowerShell 主控台中，執行 `New-AzureRmResourceGroupDeployment` Cmdlet 以部署範本。</span><span class="sxs-lookup"><span data-stu-id="a19f6-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="a19f6-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a19f6-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="a19f6-134">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="a19f6-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="a19f6-135">若要使用 Azure CLI 部署範本，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a19f6-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="a19f6-136">如果您從未使用過 Azure CLI，請依照[如何安裝和設定 Azure CLI](../cli-install-nodejs.md) 文章中的指示進行安裝和設定。</span><span class="sxs-lookup"><span data-stu-id="a19f6-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="a19f6-137">執行 `azure config mode` 命令，以切換為資源管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a19f6-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a19f6-138">上述命令的預期輸出：</span><span class="sxs-lookup"><span data-stu-id="a19f6-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="a19f6-139">開啟 [參數檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json)，選取其內容，然後將該內容儲存至您電腦中的一個檔案。</span><span class="sxs-lookup"><span data-stu-id="a19f6-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="a19f6-140">在此範例中，參數會儲存到名為 *parameters.json*的檔案。</span><span class="sxs-lookup"><span data-stu-id="a19f6-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="a19f6-141">如有需要，變更檔案內的參數值，但建議您至少將 adminPassword 參數的值變更為唯一的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a19f6-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="a19f6-142">執行 `azure group deployment create` Cmdlet，以使用先前下載並修改的範本和參數檔案，部署新的 VNet。</span><span class="sxs-lookup"><span data-stu-id="a19f6-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="a19f6-143">在下列命令中，將 <path> 取代為您儲存檔案的目標路徑。</span><span class="sxs-lookup"><span data-stu-id="a19f6-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="a19f6-144">預期的輸出 (列出使用的參數值)︰</span><span class="sxs-lookup"><span data-stu-id="a19f6-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

