# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="c87cb-101">在 Azure Resource Manager 範本中使用受控磁碟</span><span class="sxs-lookup"><span data-stu-id="c87cb-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="c87cb-102">本文件逐步 hello managed 和 unmanaged 磁碟時使用 Azure Resource Manager 範本 tooprovision 虛擬機器之間的差異。</span><span class="sxs-lookup"><span data-stu-id="c87cb-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="c87cb-103">這將協助您使用未受管理的磁碟 toomanaged 磁碟 tooupdate 現有範本。</span><span class="sxs-lookup"><span data-stu-id="c87cb-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="c87cb-104">如需參考，我們使用 hello [101 vm-簡單 windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)範本做為指南。</span><span class="sxs-lookup"><span data-stu-id="c87cb-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="c87cb-105">您可以看到同時使用 hello 範本[管理磁碟](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json)和先前版本使用[unmanaged 磁碟](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json)如果您想要 toodirectly 加以比較。</span><span class="sxs-lookup"><span data-stu-id="c87cb-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="c87cb-106">非受控磁碟範本格式</span><span class="sxs-lookup"><span data-stu-id="c87cb-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="c87cb-107">toobegin，我們看看如何 unmanaged 磁碟在部署。</span><span class="sxs-lookup"><span data-stu-id="c87cb-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="c87cb-108">在建立時未受管理的磁碟，您需要儲存體帳戶 toohold hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c87cb-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="c87cb-109">您可以建立新儲存體帳戶，或使用現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c87cb-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="c87cb-110">這篇文章將示範如何 toocreate 新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c87cb-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="c87cb-111">tooaccomplish，您需要在 hello 資源區塊中的儲存體帳戶資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c87cb-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

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

<span data-ttu-id="c87cb-112">在 hello 虛擬機器物件中，我們需要 hello hello 的虛擬機器先建立儲存體帳戶 tooensure 的相依性。</span><span class="sxs-lookup"><span data-stu-id="c87cb-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="c87cb-113">在 hello`storageProfile`區段，然後指定 hello hello VHD 的位置，其參考 hello 儲存體帳戶，以及 hello OS 磁碟和任何資料磁碟所需的完整 URI。</span><span class="sxs-lookup"><span data-stu-id="c87cb-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="c87cb-114">受控磁碟範本格式</span><span class="sxs-lookup"><span data-stu-id="c87cb-114">Managed disks template formatting</span></span>

<span data-ttu-id="c87cb-115">Azure 受管理磁碟 hello 磁碟會成為最上層資源與 hello 使用者建立的儲存體帳戶 toobe 已不再需要。</span><span class="sxs-lookup"><span data-stu-id="c87cb-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="c87cb-116">受管理的磁碟第一次會暴露在 hello `2016-04-30-preview` API 版本，它們適用於所有後續的 API 版本，而現在 hello 預設磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="c87cb-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="c87cb-117">hello 下列各節逐一查核 hello 預設設定，並詳細說明如何 toofurther 自訂您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c87cb-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="c87cb-118">建議 toouse 應用程式開發介面版本晚於`2016-04-30-preview`之間的重大變更與`2016-04-30-preview`和`2017-03-30`。</span><span class="sxs-lookup"><span data-stu-id="c87cb-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="c87cb-119">預設的受控磁碟設定</span><span class="sxs-lookup"><span data-stu-id="c87cb-119">Default managed disk settings</span></span>

<span data-ttu-id="c87cb-120">toocreate VM 使用受管理磁碟時，您不再需要 toocreate hello 儲存體帳戶資源，而且可以更新您的虛擬機器的資源，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c87cb-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="c87cb-121">特別注意該 hello`apiVersion`反映`2017-03-30`和 hello`osDisk`和`dataDisks`不再參考 tooa 特定 hello VHD URI。</span><span class="sxs-lookup"><span data-stu-id="c87cb-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="c87cb-122">當部署但不指定其他屬性，將會使用 hello 磁碟[標準 LRS 儲存體](../articles/storage/common/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="c87cb-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="c87cb-123">如果未指定名稱，它可接受的 hello 格式`<VMName>_OsDisk_1_<randomstring>`hello OS 磁碟和`<VMName>_disk<#>_<randomstring>`每個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c87cb-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="c87cb-124">根據預設，Azure 磁碟加密已停用;快取是 hello OS 磁碟和任何資料磁碟的讀取/寫入。</span><span class="sxs-lookup"><span data-stu-id="c87cb-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="c87cb-125">您可能會注意到在 hello 面範例中仍有儲存體帳戶的相依性，這只適用於診斷的存放裝置，而且不需要使用磁碟儲存體也一樣。</span><span class="sxs-lookup"><span data-stu-id="c87cb-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="c87cb-126">使用最上層受控磁碟資源</span><span class="sxs-lookup"><span data-stu-id="c87cb-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="c87cb-127">當做 hello 虛擬機器物件中的替代 toospecifying hello 磁碟設定，您可以建立最上層的磁碟資源，並附加做為建立 hello 虛擬機器的一部分。</span><span class="sxs-lookup"><span data-stu-id="c87cb-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="c87cb-128">例如，我們可以建立，如下所示 toouse 當做資料磁碟的磁碟資源。</span><span class="sxs-lookup"><span data-stu-id="c87cb-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

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

<span data-ttu-id="c87cb-129">在 hello VM 物件中，我們就可以參考此連接的磁碟物件 toobe。</span><span class="sxs-lookup"><span data-stu-id="c87cb-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="c87cb-130">指定 hello 資源識別碼 hello 管理我們在 hello 建立的磁碟`managedDisk`屬性允許在建立 VM 的 hello hello 磁碟的 hello 附件。</span><span class="sxs-lookup"><span data-stu-id="c87cb-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="c87cb-131">請注意該 hello `apiVersion` hello VM 資源設定太`2017-03-30`。</span><span class="sxs-lookup"><span data-stu-id="c87cb-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="c87cb-132">也請注意我們已在建立 VM 之前已成功建立 hello 磁碟資源 tooensure 建立相依性。</span><span class="sxs-lookup"><span data-stu-id="c87cb-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="c87cb-133">為使用受控磁碟的 VM 建立受控可用性設定組</span><span class="sxs-lookup"><span data-stu-id="c87cb-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="c87cb-134">toocreate 管理可用性集合若具有 Vm 使用受管理的磁碟，新增 hello`sku`物件 toohello 可用性設定資源，並設定 hello`name`屬性太`Aligned`。</span><span class="sxs-lookup"><span data-stu-id="c87cb-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="c87cb-135">這可確保每個 VM 的 hello 磁碟與彼此 tooavoid 單一失敗點完全隔離。</span><span class="sxs-lookup"><span data-stu-id="c87cb-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="c87cb-136">也請注意該 hello `apiVersion` hello 可用性集資源設定得`2017-03-30`。</span><span class="sxs-lookup"><span data-stu-id="c87cb-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="c87cb-137">其他案例和自訂</span><span class="sxs-lookup"><span data-stu-id="c87cb-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="c87cb-138">toofind hello 的 REST API 規格的完整資訊，請檢閱 hello[建立受管理的磁碟 REST API 文件](/rest/api/manageddisks/disks/disks-create-or-update)。</span><span class="sxs-lookup"><span data-stu-id="c87cb-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="c87cb-139">您會發現其他案例，以及預設值與可接受的值可以是送出的 toohello API，透過範本部署。</span><span class="sxs-lookup"><span data-stu-id="c87cb-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c87cb-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c87cb-140">Next steps</span></span>

* <span data-ttu-id="c87cb-141">如需完整的範本使用受管理的磁碟，請造訪 hello 下列 Azure 快速入門儲存機制的連結。</span><span class="sxs-lookup"><span data-stu-id="c87cb-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * <span data-ttu-id="c87cb-142">[使用受控磁碟的 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c87cb-142">[Windows VM with managed disk](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)</span></span>
    * <span data-ttu-id="c87cb-143">[使用受控磁碟的 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c87cb-143">[Linux VM with managed disk](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)</span></span>
    * <span data-ttu-id="c87cb-144">[受控磁碟範本的完整清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="c87cb-144">[Full list of managed disk templates](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)</span></span>
* <span data-ttu-id="c87cb-145">請瀏覽 hello [Azure 受管理的磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)深入了解文件 toolearn 管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c87cb-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="c87cb-146">檢閱虛擬機器資源的 hello 範本參考文件瀏覽 hello [Microsoft.Compute/virtualMachines 範本參考](/templates/microsoft.compute/virtualmachines)文件。</span><span class="sxs-lookup"><span data-stu-id="c87cb-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="c87cb-147">檢閱磁碟資源的 hello 範本參考文件瀏覽 hello [Microsoft.Compute/disks 範本參考](/templates/microsoft.compute/disks)文件。</span><span class="sxs-lookup"><span data-stu-id="c87cb-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
