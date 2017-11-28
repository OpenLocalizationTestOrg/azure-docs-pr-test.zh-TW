---
title: "具有多個 Nic 的 Azure Resource Manager 範本的 VM aaaCreate |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立具有多個 NIC 的 VM。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="79504-103">使用範本建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="79504-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="79504-104">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="79504-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="79504-105">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](virtual-network-deploy-multinic-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="79504-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="79504-106">hello 下列步驟使用的資源群組名稱為*IaaSStory* hello 網頁伺服器和資源群組名稱為*IaaSStory 後端*hello DB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="79504-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79504-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="79504-107">Prerequisites</span></span>
<span data-ttu-id="79504-108">您可以建立 hello DB 伺服器之前，您需要 toocreate hello *IaaSStory*此案例中的 hello 必要資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="79504-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="79504-109">toocreate 這些資源，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="79504-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="79504-110">瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。</span><span class="sxs-lookup"><span data-stu-id="79504-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="79504-111">在 hello 範本頁面中，右邊 toohello**父資源群組**，按一下 **部署 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="79504-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="79504-112">如有需要變更為 hello 參數值，然後遵循 hello hello Azure 預覽入口網站 toodeploy hello 資源群組中的步驟。</span><span class="sxs-lookup"><span data-stu-id="79504-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79504-113">請確定您的儲存體帳戶名稱是唯一的。</span><span class="sxs-lookup"><span data-stu-id="79504-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="79504-114">在 Auzre 中不能有重複的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="79504-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="79504-115">了解 hello 部署範本</span><span class="sxs-lookup"><span data-stu-id="79504-115">Understand hello deployment template</span></span>
<span data-ttu-id="79504-116">部署與此文件提供的 hello 範本之前，請確定您了解其用途。</span><span class="sxs-lookup"><span data-stu-id="79504-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="79504-117">下列步驟的 hello 提供 hello 範本很好的概觀：</span><span class="sxs-lookup"><span data-stu-id="79504-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="79504-118">瀏覽過[hello 範本頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)。</span><span class="sxs-lookup"><span data-stu-id="79504-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="79504-119">按一下**azuredeploy.json** tooopen hello 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="79504-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="79504-120">請注意 hello *osType*下面所列的參數。</span><span class="sxs-lookup"><span data-stu-id="79504-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="79504-121">這個參數是使用的 tooselect 哪些 hello 的資料庫伺服器，以及多個作業系統的 VM 映像 toouse 相關設定。</span><span class="sxs-lookup"><span data-stu-id="79504-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="79504-122">向下捲動 toohello 清單的變數，並檢查 hello hello 定義**dbVMSetting**下面所列的變數。</span><span class="sxs-lookup"><span data-stu-id="79504-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="79504-123">它會接收一個 hello 陣列中包含的元素 hello **dbVMSettings**變數。</span><span class="sxs-lookup"><span data-stu-id="79504-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="79504-124">如果您熟悉軟體開發術語，您可以檢視 hello **dbVMSettings**變數作為雜湊表或字典。</span><span class="sxs-lookup"><span data-stu-id="79504-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="79504-125">假設您決定在 hello 後端中執行 SQL toodeploy Windows Vm。</span><span class="sxs-lookup"><span data-stu-id="79504-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="79504-126">然後 hello 值**osType**會*Windows*，和 hello **dbVMSetting**變數會包含下面列出代表 hello hello 中的第一個值之 hello 元素**dbVMSettings**變數。</span><span class="sxs-lookup"><span data-stu-id="79504-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="79504-127">請注意 hello **vmSize**包含 hello 值*Standard_DS3*。</span><span class="sxs-lookup"><span data-stu-id="79504-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="79504-128">只有特定 VM 大小允許 hello 使用多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="79504-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="79504-129">您可以確認哪些 VM 大小來支援多個 Nic 讀取 hello [Windows VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[Linux VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)文件。</span><span class="sxs-lookup"><span data-stu-id="79504-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="79504-130">向下捲動太**資源**和注意事項 hello 第一個元素。</span><span class="sxs-lookup"><span data-stu-id="79504-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="79504-131">它描述儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="79504-131">It describes a storage account.</span></span> <span data-ttu-id="79504-132">這個儲存體帳戶將會使用每個資料庫的 VM 所使用的 toomaintain hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="79504-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="79504-133">在此案例中，每部資料庫 VM 都有儲存在一般儲存體的作業系統磁碟，以及儲存在 SSD (進階) 儲存體的兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="79504-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="79504-134">捲動 toohello 下一個資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79504-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="79504-135">此資源代表的 hello NIC 用於每個 VM 的資料庫中的資料庫存取權。</span><span class="sxs-lookup"><span data-stu-id="79504-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="79504-136">請注意 hello 使用 hello**複製**這項資源中的函式。</span><span class="sxs-lookup"><span data-stu-id="79504-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="79504-137">hello 範本可讓您 toodeploy 許多 Vm 所要根據 hello **dbCount**參數。</span><span class="sxs-lookup"><span data-stu-id="79504-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="79504-138">因此，您需要 toocreate hello 相同數量的 Nic，來存取資料庫，其中每個 VM。</span><span class="sxs-lookup"><span data-stu-id="79504-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="79504-139">捲動 toohello 下一個資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79504-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="79504-140">此資源代表的 hello NIC 用於 VM 的每個資料庫中的管理。</span><span class="sxs-lookup"><span data-stu-id="79504-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="79504-141">同樣地，每個資料庫 VM 都需要一個這種 NIC。</span><span class="sxs-lookup"><span data-stu-id="79504-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="79504-142">請注意 hello **networkSecurityGroup**項目，連結允許存取 tooRDP/SSH toothis NIC 只 NSG。</span><span class="sxs-lookup"><span data-stu-id="79504-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="79504-143">捲動 toohello 下一個資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79504-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="79504-144">此資源代表共用資料庫的所有 Vm 的可用性集 toobe。</span><span class="sxs-lookup"><span data-stu-id="79504-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="79504-145">這樣一來，您保證，永遠都會有一個 VM 中設定在維護期間執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="79504-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="79504-146">捲動 toohello 下一個資源。</span><span class="sxs-lookup"><span data-stu-id="79504-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="79504-147">此資源代表 hello 資料庫的 Vm，如中所示 hello 先下面所列的幾行。</span><span class="sxs-lookup"><span data-stu-id="79504-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="79504-148">請注意 hello 使用 hello**複製**函式一次，確保會建立多個 Vm 根據 hello **dbCount**參數。</span><span class="sxs-lookup"><span data-stu-id="79504-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="79504-149">同時也請注意 hello **dependsOn**集合。</span><span class="sxs-lookup"><span data-stu-id="79504-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="79504-150">它會列出所需 toobe hello 部署 VM，以及 hello 可用性設定組，與 hello 儲存體帳戶之前建立的兩個 Nic。</span><span class="sxs-lookup"><span data-stu-id="79504-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="79504-151">Hello VM 資源 toohello 中向下捲動**networkProfile**項目，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79504-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="79504-152">請注意，每部 VM 都有兩個參照的 NIC。</span><span class="sxs-lookup"><span data-stu-id="79504-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="79504-153">當您建立多個 Nic vm 時，您必須設定 hello**主要**hello Nic 之一的屬性太*true*，和太 hello rest*false*。</span><span class="sxs-lookup"><span data-stu-id="79504-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="79504-154">使用部署 hello ARM 範本按一下 toodeploy</span><span class="sxs-lookup"><span data-stu-id="79504-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79504-155">請確定您遵循 hello[先決條件](#Pre-requisites)之前 hello 指示下面的步驟。</span><span class="sxs-lookup"><span data-stu-id="79504-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="79504-156">hello 範例範本可用 hello 公用儲存機制中的會使用包含 hello 預設值使用 toogenerate hello 案例上面所述的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="79504-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="79504-157">toodeploy 此範本使用按一下 toodeploy，遵循[此連結](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)，右邊 toohello**後端資源群組 （請參閱文件）**按一下**部署 tooAzure**，取代hello 必要時，預設參數值，並遵循 hello 入口網站中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="79504-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="79504-158">hello 圖會顯示 hello 內容 hello 新資源群組的部署之後。</span><span class="sxs-lookup"><span data-stu-id="79504-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![後端資源群組](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="79504-160">使用 PowerShell 來部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="79504-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="79504-161">您使用 PowerShell 下載 toodeploy hello 範本安裝和設定 PowerShell hello 中的 hello 步驟[安裝和設定 PowerShell](/powershell/azure/overview)發行項，然後完成 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="79504-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="79504-162">執行 hello  **`New-AzureRmResourceGroup`** 資源群組使用的 cmdlet toocreate hello 範本。</span><span class="sxs-lookup"><span data-stu-id="79504-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="79504-163">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="79504-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="79504-164">使用 Azure CLI hello 部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="79504-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="79504-165">使用 Azure CLI hello toodeploy hello 範本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="79504-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="79504-166">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="79504-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="79504-167">執行 hello  **`azure config mode`** 命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="79504-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="79504-168">hello 預期輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="79504-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="79504-169">開啟 hello[參數檔](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json)、 選取它的內容，和它 tooa 將檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="79504-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="79504-170">對於此範例中，我們儲存 hello 參數檔案太*parameters.json*。</span><span class="sxs-lookup"><span data-stu-id="79504-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="79504-171">執行 hello  **`azure group deployment create`**  hello 範本和參數使用新的 VNet 檔案您下載並修改上述指令程式 toodeploy hello。</span><span class="sxs-lookup"><span data-stu-id="79504-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="79504-172">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="79504-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="79504-173">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="79504-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

