---
title: "在 Azure Resource Manager 範本中使用受控磁碟 | Microsoft Docs"
description: "如何在 Azure Resource Manager 範本中使用受控磁碟的詳細資料"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: 4c502784a57850d6f11200e95f7432d2206e920a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="a193f-103">在 Azure Resource Manager 範本中使用受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a193f-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="a193f-104">本文逐步解說當使用 Azure Resource Manager 範本佈建虛擬機器時，受控與非受控磁碟之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a193f-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="a193f-105">這有助於您將使用非受控磁碟的現有範本更新為使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a193f-105">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="a193f-106">如需參考，我們會使用 [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) \(英文\) 範本作為指南。</span><span class="sxs-lookup"><span data-stu-id="a193f-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="a193f-107">如果您想要直接進行比較，您可以看到使用[受控磁碟](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) \(英文\) 的範本以及使用[非受控磁碟](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) \(英文\) 的先前版本。</span><span class="sxs-lookup"><span data-stu-id="a193f-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="a193f-108">非受控磁碟範本格式</span><span class="sxs-lookup"><span data-stu-id="a193f-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="a193f-109">一開始，我們先看一下如何部署非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a193f-109">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="a193f-110">建立非受控磁碟時，您需要有一個儲存體帳戶來保存 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="a193f-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="a193f-111">您可以建立新儲存體帳戶，或使用現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a193f-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="a193f-112">此文章將說明如何建立新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a193f-112">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="a193f-113">若要執行此動作，您需要在資源區塊中有一個儲存體帳戶資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a193f-113">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="a193f-114">在虛擬機器物件中，我們需要依賴儲存體帳戶，以確保它在虛擬機器之前建立。</span><span class="sxs-lookup"><span data-stu-id="a193f-114">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="a193f-115">然後，在 `storageProfile` 區段中，我們會指定 VHD 位置的完整 URI，它會參照儲存體帳戶，而且 OS 磁碟與所有資料磁碟都需要它。</span><span class="sxs-lookup"><span data-stu-id="a193f-115">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="a193f-116">受控磁碟範本格式</span><span class="sxs-lookup"><span data-stu-id="a193f-116">Managed disks template formatting</span></span>

<span data-ttu-id="a193f-117">有了 Azure 受控磁碟，磁碟會變成最上層資源，且不再需要使用者建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a193f-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="a193f-118">受控磁碟是在 `2016-04-30-preview` API 版本中首次公開，在後續的 API 版本中皆可取得，而且現在它們是預設的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="a193f-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="a193f-119">以下幾節會逐步解說預設設定，並詳細說明如何進一步自訂您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a193f-119">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="a193f-120">建議使用 `2016-04-30-preview` 以後的 API 版本，因為 `2016-04-30-preview` 和 `2017-03-30` 之間有重大變更。</span><span class="sxs-lookup"><span data-stu-id="a193f-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="a193f-121">預設的受控磁碟設定</span><span class="sxs-lookup"><span data-stu-id="a193f-121">Default managed disk settings</span></span>

<span data-ttu-id="a193f-122">若要建立使用受控磁碟的 VM，您不再需要建立儲存體帳戶資源，而且可以更新虛擬機器資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a193f-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="a193f-123">請特別注意，`apiVersion` 會反映出 `2017-03-30` 和 `osDisk` 和 `dataDisks` 不再參照 VHD 的特定 URI。</span><span class="sxs-lookup"><span data-stu-id="a193f-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="a193f-124">若部署而不指定其他屬性，磁碟將會使用 [標準 LRS 儲存體](storage-redundancy.md) 。</span><span class="sxs-lookup"><span data-stu-id="a193f-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="a193f-125">若未指定名稱，它的 OS 磁碟格式為 `<VMName>_OsDisk_1_<randomstring>`，而每個資料磁碟的格式為 `<VMName>_disk<#>_<randomstring>`。</span><span class="sxs-lookup"><span data-stu-id="a193f-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="a193f-126">預設已停用 Azure 磁碟加密；OS 磁碟的快取為 [讀取/寫入]，資料磁碟的快取則為 [無]。</span><span class="sxs-lookup"><span data-stu-id="a193f-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="a193f-127">您可能會注意到，在下列範例中仍有儲存體帳戶相依性，但這只適用於儲存體的診斷，而且磁碟儲存體並不需要相依性。</span><span class="sxs-lookup"><span data-stu-id="a193f-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="a193f-128">使用最上層受控磁碟資源</span><span class="sxs-lookup"><span data-stu-id="a193f-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="a193f-129">作為在虛擬機器物件中指定磁碟組態的替代方式，您可以建立最上層磁碟資源，並在建立虛擬機器時連結它。</span><span class="sxs-lookup"><span data-stu-id="a193f-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="a193f-130">例如，我們可以建立如下所示的磁碟資源，來作為資料磁碟使用。</span><span class="sxs-lookup"><span data-stu-id="a193f-130">For example, we can create a disk resource as follows to use as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="a193f-131">然後，在 VM 物件中，我們可以參照這個要連結的磁碟物件。</span><span class="sxs-lookup"><span data-stu-id="a193f-131">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="a193f-132">指定我們在 `managedDisk` 屬性中建立之受控磁碟的資源識別碼，可允許在建立 VM 時連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="a193f-132">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="a193f-133">請注意，VM 資源的 `apiVersion` 是設定成 `2017-03-30`。</span><span class="sxs-lookup"><span data-stu-id="a193f-133">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="a193f-134">也請注意，我們在磁碟資源上建立了相依性，以確保它在建立 VM 之前成功建立。</span><span class="sxs-lookup"><span data-stu-id="a193f-134">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="a193f-135">為使用受控磁碟的 VM 建立受控可用性設定組</span><span class="sxs-lookup"><span data-stu-id="a193f-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="a193f-136">若要為使用受控磁碟的 VM 建立受控可用性設定組，請將 `sku` 物件新增至可用性設定組資源，並將 `name` 屬性設定為 `Aligned`。</span><span class="sxs-lookup"><span data-stu-id="a193f-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="a193f-137">這可確保每個 VM 的磁碟彼此之間都充分隔離，以避免發生單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="a193f-137">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="a193f-138">另請注意，可用性設定組資源的 `apiVersion` 是設定成 `2017-03-30`。</span><span class="sxs-lookup"><span data-stu-id="a193f-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="a193f-139">其他案例和自訂</span><span class="sxs-lookup"><span data-stu-id="a193f-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="a193f-140">若要尋找有關 REST API 規格的完整資訊，請檢閱[建立受控磁碟 REST API 文件](/rest/api/manageddisks/disks/disks-create-or-update)。</span><span class="sxs-lookup"><span data-stu-id="a193f-140">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="a193f-141">您會找到其他案例，以及可透過範本部署提交至 API 之預設及可接受的值。</span><span class="sxs-lookup"><span data-stu-id="a193f-141">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a193f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a193f-142">Next steps</span></span>

* <span data-ttu-id="a193f-143">如需使用受控磁碟的完整範本，請瀏覽下列「Azure 快速入門存放庫」連結。</span><span class="sxs-lookup"><span data-stu-id="a193f-143">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * <span data-ttu-id="a193f-144">[使用受控磁碟的 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a193f-144">[Windows VM with managed disk](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)</span></span>
    * <span data-ttu-id="a193f-145">[使用受控磁碟的 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a193f-145">[Linux VM with managed disk](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)</span></span>
    * <span data-ttu-id="a193f-146">[受控磁碟範本的完整清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="a193f-146">[Full list of managed disk templates](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)</span></span>
* <span data-ttu-id="a193f-147">瀏覽 [Azure 受控磁碟概觀](storage-managed-disks-overview.md)文件，深入了解受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a193f-147">Visit the [Azure Managed Disks Overview](storage-managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="a193f-148">瀏覽 [Microsoft.Compute/virtualMachines 範本參考](/templates/microsoft.compute/virtualmachines)文件，檢閱虛擬機器資源的範本參考文件。</span><span class="sxs-lookup"><span data-stu-id="a193f-148">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="a193f-149">瀏覽 [Microsoft.Compute/disks 範本參考](/templates/microsoft.compute/disks)文件，檢閱磁碟資源的範本參考文件。</span><span class="sxs-lookup"><span data-stu-id="a193f-149">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
