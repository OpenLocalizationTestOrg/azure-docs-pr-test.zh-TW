---
title: "aaaCreate 網路安全性群組-Azure Resource Manager 範本 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署使用 Azure Resource Manager 範本的網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="64537-103">使用 Azure Resource Manager 範本建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="64537-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="64537-104">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="64537-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="64537-105">您也可以[hello 傳統部署模型中建立 Nsg](virtual-networks-create-nsg-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="64537-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="64537-106">範本檔案中的 NSG 資源</span><span class="sxs-lookup"><span data-stu-id="64537-106">NSG resources in a template file</span></span>
<span data-ttu-id="64537-107">您可以檢視和下載 hello[範例範本](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json)。</span><span class="sxs-lookup"><span data-stu-id="64537-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="64537-108">hello 下一節顯示 hello 定義 hello 前端 NSG，根據 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="64537-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="64537-109">tooassociate hello NSG toohello 前端的子網路，您有在 hello 範本，並使用 hello 參考識別碼 hello NSG toochange hello 子網路定義。</span><span class="sxs-lookup"><span data-stu-id="64537-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="64537-110">請注意 hello 為 hello 後端 NSG 與 hello 後端子 hello 範本中進行相同。</span><span class="sxs-lookup"><span data-stu-id="64537-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="64537-111">使用部署 hello ARM 範本按一下 toodeploy</span><span class="sxs-lookup"><span data-stu-id="64537-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="64537-112">hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="64537-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="64537-113">toodeploy 此範本使用按一下 toodeploy，遵循[此連結](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG)，按一下 **部署 tooAzure**、 取代 hello 預設參數值，如有必要，並遵循 hello 入口網站中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="64537-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="64537-114">使用 PowerShell 來部署 hello ARM 範本</span><span class="sxs-lookup"><span data-stu-id="64537-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="64537-115">您使用 PowerShell 下載 toodeploy hello ARM 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="64537-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="64537-116">如果您從未使用過 Azure PowerShell，請遵循 hello 中的 hello 指示[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall 並加以設定。</span><span class="sxs-lookup"><span data-stu-id="64537-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="64537-117">執行 hello  **`New-AzureRmResourceGroup`** 資源群組使用的 cmdlet toocreate hello 範本。</span><span class="sxs-lookup"><span data-stu-id="64537-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="64537-118">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="64537-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="64537-119">使用 Azure CLI hello 部署 hello ARM 範本</span><span class="sxs-lookup"><span data-stu-id="64537-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="64537-120">使用 Azure CLI hello toodeploy hello ARM 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="64537-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="64537-121">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="64537-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="64537-122">執行 hello  **`azure config mode`** 命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="64537-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="64537-123">hello 以下是預期的 hello hello 命令的輸出：</span><span class="sxs-lookup"><span data-stu-id="64537-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="64537-124">執行 hello  **`azure group deployment create`**  hello 範本和參數使用新的 VNet 檔案您下載並修改上述指令程式 toodeploy hello。</span><span class="sxs-lookup"><span data-stu-id="64537-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="64537-125">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="64537-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="64537-126">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="64537-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="64537-127">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="64537-127">**-n (or --name)**.</span></span> <span data-ttu-id="64537-128">建立 hello 資源群組 toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="64537-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="64537-129">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="64537-129">**-l (or --location)**.</span></span> <span data-ttu-id="64537-130">Hello 資源群組將會建立 azure 的區域。</span><span class="sxs-lookup"><span data-stu-id="64537-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="64537-131">**-f (或 --template-file)**。</span><span class="sxs-lookup"><span data-stu-id="64537-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="64537-132">路徑 tooyour ARM 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="64537-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="64537-133">**-e (或 --parameters-file)**。</span><span class="sxs-lookup"><span data-stu-id="64537-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="64537-134">Tooyour ARM 參數檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="64537-134">Path tooyour ARM parameters file.</span></span>

