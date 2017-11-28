---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure Resource Manager 範本 |Microsoft 文件"
description: "了解如何 toocreate VM 的靜態公用 IP 位址使用 Azure Resource Manager 範本。"
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
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="a13c7-103">使用 Azure Resource Manager 範本建立具有靜態公用 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="a13c7-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a13c7-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a13c7-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="a13c7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a13c7-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="a13c7-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a13c7-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="a13c7-107">範本</span><span class="sxs-lookup"><span data-stu-id="a13c7-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="a13c7-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="a13c7-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a13c7-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a13c7-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a13c7-110">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a13c7-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="a13c7-111">範本檔案中的公用 IP 資源</span><span class="sxs-lookup"><span data-stu-id="a13c7-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="a13c7-112">您可以檢視和下載 hello[範例範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="a13c7-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="a13c7-113">hello 下一節顯示 hello hello 公用 IP 資源，根據上述的 hello 案例定義：</span><span class="sxs-lookup"><span data-stu-id="a13c7-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

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

<span data-ttu-id="a13c7-114">請注意 hello **publicIPAllocationMethod**屬性，設定得*靜態*。</span><span class="sxs-lookup"><span data-stu-id="a13c7-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="a13c7-115">這個屬性可以是 Dynamic (預設值) 或 Static。</span><span class="sxs-lookup"><span data-stu-id="a13c7-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="a13c7-116">設定 toostatic 可確保永遠不會變更 hello 指派公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a13c7-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="a13c7-117">hello 下一節顯示 hello 與之間的關聯 hello 公用 IP 位址的網路介面：</span><span class="sxs-lookup"><span data-stu-id="a13c7-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

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

<span data-ttu-id="a13c7-118">請注意 hello **publicIPAddress**屬性指向 toohello**識別碼**的資源，名為**variables('webVMSetting').pipName**。</span><span class="sxs-lookup"><span data-stu-id="a13c7-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="a13c7-119">這是 hello hello 如上所示公用 IP 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a13c7-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="a13c7-120">最後，上述的 hello 網路介面會列在 hello **networkProfile** hello VM 正在建立的屬性。</span><span class="sxs-lookup"><span data-stu-id="a13c7-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="a13c7-121">使用部署 hello 範本按一下 toodeploy</span><span class="sxs-lookup"><span data-stu-id="a13c7-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="a13c7-122">hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="a13c7-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="a13c7-123">toodeploy 此範本使用按一下 toodeploy，按一下 **部署 tooAzure** hello hello Readme.md 檔案中[VM 使用靜態的 PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP)範本。</span><span class="sxs-lookup"><span data-stu-id="a13c7-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="a13c7-124">如果有需要，取代 hello 預設參數值並輸入 hello 空白參數的值。</span><span class="sxs-lookup"><span data-stu-id="a13c7-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="a13c7-125">請遵循 hello hello 入口 toocreate 具有靜態公用 IP 位址的虛擬機器中的指示。</span><span class="sxs-lookup"><span data-stu-id="a13c7-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="a13c7-126">使用 PowerShell 來部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="a13c7-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="a13c7-127">您使用 PowerShell 下載 toodeploy hello 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a13c7-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="a13c7-128">如果您從未使用過 Azure PowerShell，完成 hello 步驟 hello[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="a13c7-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a13c7-129">在 PowerShell 主控台中，執行 hello `New-AzureRmResourceGroup` cmdlet toocreate 新的資源群組，如有必要。</span><span class="sxs-lookup"><span data-stu-id="a13c7-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="a13c7-130">如果您已經建立的資源群組，請移 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="a13c7-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="a13c7-131">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a13c7-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="a13c7-132">在 PowerShell 主控台中，執行 hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="a13c7-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="a13c7-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a13c7-133">Expected output:</span></span>
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="a13c7-134">使用 Azure CLI hello 部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="a13c7-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="a13c7-135">使用 Azure CLI，完成下列步驟的 hello hello toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="a13c7-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="a13c7-136">如果您從未使用過 Azure CLI，請遵循在 hello hello 步驟[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)文章 tooinstall 並加以設定。</span><span class="sxs-lookup"><span data-stu-id="a13c7-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="a13c7-137">執行 hello`azure config mode`命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a13c7-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a13c7-138">hello 預期 hello 上述命令中的輸出：</span><span class="sxs-lookup"><span data-stu-id="a13c7-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="a13c7-139">開啟 hello[參數檔](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json)、 選取其內容，和它 tooa 將檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="a13c7-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="a13c7-140">例如，hello 參數會儲存名為 tooa 檔案*parameters.json*。</span><span class="sxs-lookup"><span data-stu-id="a13c7-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="a13c7-141">變更 hello 參數值，如有需要，hello 檔案內，但最少，建議您變更 hello hello adminPassword 參數 tooa 唯一的複雜密碼的值。</span><span class="sxs-lookup"><span data-stu-id="a13c7-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="a13c7-142">執行 hello `azure group deployment create` cmd toodeploy hello hello 範本和參數使用新的 VNet 檔案下載，並修改上方。</span><span class="sxs-lookup"><span data-stu-id="a13c7-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="a13c7-143">在下方的 hello 命令，取代<path>hello 路徑 hello 檔案儲存至。</span><span class="sxs-lookup"><span data-stu-id="a13c7-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="a13c7-144">預期的輸出 (列出使用的參數值)︰</span><span class="sxs-lookup"><span data-stu-id="a13c7-144">Expected output (lists parameter values used):</span></span>

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

