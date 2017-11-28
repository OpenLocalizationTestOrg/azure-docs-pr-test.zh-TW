---
title: "在 Azure 資源管理員範本 aaaVirtual 機器 |Microsoft Azure"
description: "深入了解 Azure Resource Manager 範本中定義 hello 虛擬機器資源的方式。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="04795-103">Azure Resource Manager 範本中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04795-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="04795-104">本文說明 Azure Resource Manager 範本套用 toovirtual 機器中的各個的層面。</span><span class="sxs-lookup"><span data-stu-id="04795-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="04795-105">本文不會說明建立虛擬機器的完整範本；您需要儲存體帳戶、網路介面、公用 IP 位址與虛擬網路的資源定義。</span><span class="sxs-lookup"><span data-stu-id="04795-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="04795-106">如需有關如何一起定義這些資源的詳細資訊，請參閱 hello[資源管理員範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="04795-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="04795-107">有許多[hello 組件庫中的範本](https://azure.microsoft.com/documentation/templates/?term=VM)包括 hello VM 資源。</span><span class="sxs-lookup"><span data-stu-id="04795-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="04795-108">此處並未說明可以包含在範本中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="04795-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="04795-109">此範例顯示用來建立指定數目之 VM 範本的一般資源區段︰</span><span class="sxs-lookup"><span data-stu-id="04795-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="04795-110">此範例仰賴先前建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04795-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="04795-111">您可以藉由部署從 hello 範本建立 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04795-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="04795-112">hello 範例也依賴網路介面和其相依的資源會 hello 範本中定義的。</span><span class="sxs-lookup"><span data-stu-id="04795-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="04795-113">這些資源不會顯示在 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="04795-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="04795-114">API 版本</span><span class="sxs-lookup"><span data-stu-id="04795-114">API Version</span></span>

<span data-ttu-id="04795-115">當您部署使用範本的資源時，您有 toospecify hello API toouse 的版本。</span><span class="sxs-lookup"><span data-stu-id="04795-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="04795-116">hello 範例顯示 hello 虛擬機器資源使用此 api 版本項目：</span><span class="sxs-lookup"><span data-stu-id="04795-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="04795-117">hello 版的 hello 應用程式開發介面，您在範本中指定會影響您可以在 hello 範本中定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="04795-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="04795-118">一般情況下，您應該在建立範本時選取 hello 最新的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="04795-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="04795-119">對於現有的範本，您可以決定是否 toocontinue 使用較舊的應用程式開發介面版本，或是更新 hello 最新版本 tootake 利用新功能的範本。</span><span class="sxs-lookup"><span data-stu-id="04795-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="04795-120">使用這些機會，以取得最新 API 版本 hello:</span><span class="sxs-lookup"><span data-stu-id="04795-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="04795-121">REST API - [列出所有資源提供者](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="04795-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="04795-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="04795-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="04795-123">Azure CLI 2.0 - [az 提供者顯示](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="04795-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="04795-124">參數和變數</span><span class="sxs-lookup"><span data-stu-id="04795-124">Parameters and variables</span></span>

<span data-ttu-id="04795-125">[參數](../../resource-group-authoring-templates.md)讓您輕鬆為您 hello 範本 toospecify 值時執行它。</span><span class="sxs-lookup"><span data-stu-id="04795-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="04795-126">Hello 範例中，會使用此參數 > 一節：</span><span class="sxs-lookup"><span data-stu-id="04795-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="04795-127">當您部署的 hello 範例範本時，您輸入值 hello 名稱和密碼 hello 系統管理員帳戶的每個 VM hello 數目及 Vm toocreate 上。</span><span class="sxs-lookup"><span data-stu-id="04795-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="04795-128">您可以在 hello 範本時，管理的個別檔案中指定參數值，或提供值，當系統提示您 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="04795-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="04795-129">[變數](../../resource-group-authoring-templates.md)讓您輕鬆為您 tooset 值在整個重複使用或，可能會隨時間變更的 hello 範本中。</span><span class="sxs-lookup"><span data-stu-id="04795-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="04795-130">Hello 範例中，會使用此變數區段：</span><span class="sxs-lookup"><span data-stu-id="04795-130">This variables section is used in hello example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="04795-131">當您部署 hello 範例範本時，變數值會用於 hello 名稱和識別碼 hello 先前建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="04795-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="04795-132">變數也會使用的 tooprovide hello hello 診斷延伸模組的設定。</span><span class="sxs-lookup"><span data-stu-id="04795-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="04795-133">使用 hello[最佳作法來建立 Azure 資源管理員範本](../../resource-manager-template-best-practices.md)toohelp 您決定要如何 toostructure hello 參數和變數在範本中。</span><span class="sxs-lookup"><span data-stu-id="04795-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="04795-134">資源迴圈</span><span class="sxs-lookup"><span data-stu-id="04795-134">Resource loops</span></span>

<span data-ttu-id="04795-135">您的應用程式需要一部以上的虛擬機器時，您可以在範本中使用複製項目。</span><span class="sxs-lookup"><span data-stu-id="04795-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="04795-136">此選擇性項目迴圈建立 hello 數目指定為參數的 Vm:</span><span class="sxs-lookup"><span data-stu-id="04795-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="04795-137">此外，請注意，在 hello 迴圈索引的 hello 範例是指定一些 hello hello 資源的值時使用。</span><span class="sxs-lookup"><span data-stu-id="04795-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="04795-138">例如，如果您輸入的三個 hello 名稱 hello 作業系統磁碟的執行個體計數為 myOSDisk1、 myOSDisk2 和 myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="04795-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="04795-139">這個範例會使用受管理的磁碟 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04795-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="04795-140">請記住，在 hello 範本中建立一個資源的迴圈可能會要求您 toouse hello 迴圈時建立或存取其他資源。</span><span class="sxs-lookup"><span data-stu-id="04795-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="04795-141">例如，多個 Vm 無法使用相同網路介面，因此如果您的範本執行迴圈，建立三個 Vm，它也必須迴圈建立三個網路介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="04795-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="04795-142">Hello 迴圈索引指派網路介面 tooa VM 時，會使用的 tooidentify 它：</span><span class="sxs-lookup"><span data-stu-id="04795-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="04795-143">相依項目</span><span class="sxs-lookup"><span data-stu-id="04795-143">Dependencies</span></span>

<span data-ttu-id="04795-144">最多資源依存於其他資源 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="04795-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="04795-145">虛擬機器必須與虛擬網路和 toodo 它需要的網路介面相關聯。</span><span class="sxs-lookup"><span data-stu-id="04795-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="04795-146">hello [dependsOn](../../resource-group-define-dependencies.md)項目，則使用的 toomake 確定該 hello 網路介面已準備好 toobe 之前建立 hello Vm 使用：</span><span class="sxs-lookup"><span data-stu-id="04795-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="04795-147">Resource Manager 會以平行方式部署任何不依存於另一個要部署資源的資源。</span><span class="sxs-lookup"><span data-stu-id="04795-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="04795-148">設定相依性時請謹慎，因為您可能會指定非必要相依性而不小心降低您的部署。</span><span class="sxs-lookup"><span data-stu-id="04795-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="04795-149">相依性可以鏈結多個資源。</span><span class="sxs-lookup"><span data-stu-id="04795-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="04795-150">例如，hello 網路介面取決於 hello 公用 IP 位址及虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="04795-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="04795-151">如何知道是否需要相依性？</span><span class="sxs-lookup"><span data-stu-id="04795-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="04795-152">查看您設定 hello 範本中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="04795-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="04795-153">如果 hello 虛擬機器的資源定義中的項目點，部署在 hello tooanother 資源相同的範本，您需要的相依性。</span><span class="sxs-lookup"><span data-stu-id="04795-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="04795-154">例如，範例虛擬機器會定義網路設定檔︰</span><span class="sxs-lookup"><span data-stu-id="04795-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="04795-155">tooset hello 網路介面必須存在這個屬性。</span><span class="sxs-lookup"><span data-stu-id="04795-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="04795-156">因此，您需要相依性。</span><span class="sxs-lookup"><span data-stu-id="04795-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="04795-157">其他資源 （父系） 內定義一項資源 （子系） 時，也需要 tooset 相依性。</span><span class="sxs-lookup"><span data-stu-id="04795-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="04795-158">比方說，hello 診斷設定和自訂指令碼延伸模組是兩者都定義為 hello 虛擬機器的子資源。</span><span class="sxs-lookup"><span data-stu-id="04795-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="04795-159">它們之後，才能建立 hello 虛擬機器存在。</span><span class="sxs-lookup"><span data-stu-id="04795-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="04795-160">因此，這兩個資源都會標示成相依於 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="04795-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="04795-161">設定檔</span><span class="sxs-lookup"><span data-stu-id="04795-161">Profiles</span></span>

<span data-ttu-id="04795-162">定義虛擬機器資源時，會使用數個設定檔項目。</span><span class="sxs-lookup"><span data-stu-id="04795-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="04795-163">某些是必要的而有些則是選擇性。</span><span class="sxs-lookup"><span data-stu-id="04795-163">Some are required and some are optional.</span></span> <span data-ttu-id="04795-164">例如，hello hardwareProfile、 osProfile、 storageProfile 和 networkProfile 元素皆為必要，但是 hello diagnosticsProfile 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="04795-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="04795-165">這些設定檔會定義設定，例如︰</span><span class="sxs-lookup"><span data-stu-id="04795-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="04795-166">大小</span><span class="sxs-lookup"><span data-stu-id="04795-166">size</span></span>](sizes.md)
- <span data-ttu-id="04795-167">[名稱](/architecture/best-practices/naming-conventions)和認證</span><span class="sxs-lookup"><span data-stu-id="04795-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="04795-168">磁碟和[作業系統設定](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="04795-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="04795-169">網路介面</span><span class="sxs-lookup"><span data-stu-id="04795-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="04795-170">開機診斷</span><span class="sxs-lookup"><span data-stu-id="04795-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="04795-171">磁碟和映像</span><span class="sxs-lookup"><span data-stu-id="04795-171">Disks and images</span></span>
   
<span data-ttu-id="04795-172">在 Azure 中，VHD 檔案可以代表[磁碟或映像](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="04795-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="04795-173">特製化的 toobe 特定 VM 的 vhd 檔案中的 hello 作業系統時，它是參考的 tooas 磁碟。</span><span class="sxs-lookup"><span data-stu-id="04795-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="04795-174">當一般化的 vhd 檔案中的 hello 作業系統 toobe 用 toocreate 許多 Vm，參照的 tooas 映像。</span><span class="sxs-lookup"><span data-stu-id="04795-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="04795-175">從平台映像建立新的虛擬機器和新的磁碟</span><span class="sxs-lookup"><span data-stu-id="04795-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="04795-176">當您建立 VM 時，您必須決定哪些作業系統 toouse。</span><span class="sxs-lookup"><span data-stu-id="04795-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="04795-177">hello imageReference 項目是使用的 toodefine hello 作業系統的新 VM。</span><span class="sxs-lookup"><span data-stu-id="04795-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="04795-178">hello 範例顯示 Windows 伺服器作業系統的定義：</span><span class="sxs-lookup"><span data-stu-id="04795-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="04795-179">如果您想 toocreate Linux 作業系統，您可以使用此定義：</span><span class="sxs-lookup"><span data-stu-id="04795-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="04795-180">Hello 作業系統磁碟的組態設定會指派與 hello osDisk 項目。</span><span class="sxs-lookup"><span data-stu-id="04795-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="04795-181">hello 範例會定義新的受管理的磁碟以 hello 太快取模式組**ReadWrite** ，而且正在從建立該 hello 磁碟[平台映像](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="04795-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="04795-182">從現有受控磁碟建立新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04795-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="04795-183">如果您想從現有的磁碟 toocreate 虛擬機器，移除 hello imageReference 和 hello osProfile 項目，並定義這些磁碟設定：</span><span class="sxs-lookup"><span data-stu-id="04795-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="04795-184">從受控映像建立新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="04795-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="04795-185">如果您想 toocreate 受管理的映像中的虛擬機器，變更 hello imageReference 項目，並定義這些磁碟設定：</span><span class="sxs-lookup"><span data-stu-id="04795-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="04795-186">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="04795-186">Attach data disks</span></span>

<span data-ttu-id="04795-187">您可以選擇性地加入資料磁碟 toohello Vm。</span><span class="sxs-lookup"><span data-stu-id="04795-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="04795-188">hello[的磁碟數目](sizes.md)hello 您使用的作業系統磁碟大小而定。</span><span class="sxs-lookup"><span data-stu-id="04795-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="04795-189">以 hello hello Vm 大小會設定 tooStandard_DS1_v2，hello toohello 它們是兩個可加入的資料磁碟數目上限。</span><span class="sxs-lookup"><span data-stu-id="04795-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="04795-190">在 hello 範例中，一個受管理的資料磁碟新增 tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="04795-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="04795-191">擴充功能</span><span class="sxs-lookup"><span data-stu-id="04795-191">Extensions</span></span>

<span data-ttu-id="04795-192">雖然[延伸](extensions-features.md)是不同的資源，而是 tooVMs 緊密繫結。</span><span class="sxs-lookup"><span data-stu-id="04795-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="04795-193">可以加入擴充功能，為 hello VM 的子資源，或為個別的資源。</span><span class="sxs-lookup"><span data-stu-id="04795-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="04795-194">hello 範例顯示 hello[診斷延伸模組](extensions-diagnostics-template.md)加入 toohello Vm:</span><span class="sxs-lookup"><span data-stu-id="04795-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="04795-195">Hello storageName 變數和 hello 診斷變數 tooprovide 值，則會使用此延伸模組的資源。</span><span class="sxs-lookup"><span data-stu-id="04795-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="04795-196">如果您想收集此延伸模組的 toochange hello 資料時，您可以加入更多效能計數器 toohello wadperfcounters 變數。</span><span class="sxs-lookup"><span data-stu-id="04795-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="04795-197">您也可以選擇 tooput hello 診斷資料至不同的儲存體帳戶比 hello VM 磁碟的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="04795-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="04795-198">您可以安裝在 VM 的許多擴充功能，但是最有用的 hello 可能 hello[自訂指令碼擴充](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="04795-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="04795-199">在 hello 範例中，名為 start.ps1 PowerShell 指令碼執行每個 VM 上第一次啟動時：</span><span class="sxs-lookup"><span data-stu-id="04795-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="04795-200">hello start.ps1 指令碼可以完成多的組態工作。</span><span class="sxs-lookup"><span data-stu-id="04795-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="04795-201">例如，未初始化 hello 資料磁碟加入 toohello Vm 在 hello 範例;您可以使用自訂指令碼 tooinitialize 它們。</span><span class="sxs-lookup"><span data-stu-id="04795-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="04795-202">如果您有多個啟動工作 toodo，您可以使用 hello start.ps1 檔案 toocall 其他 PowerShell 指令碼在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="04795-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="04795-203">hello 範例會使用 PowerShell，但您可以使用任何指令碼的方法可在您使用的 hello 作業系統上。</span><span class="sxs-lookup"><span data-stu-id="04795-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="04795-204">您可以看到 hello 的 hello 入口網站中的 hello 延伸模組設定 hello 安裝擴充功能的狀態：</span><span class="sxs-lookup"><span data-stu-id="04795-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![取得擴充功能狀態](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="04795-206">您也可以取得延伸模組資訊使用 hello **Get AzureRmVMExtension** PowerShell 命令，hello **vm 延伸模組取得**Azure CLI 2.0 命令或使用 hello**取得延伸模組的資訊** REST API。</span><span class="sxs-lookup"><span data-stu-id="04795-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="04795-207">部署</span><span class="sxs-lookup"><span data-stu-id="04795-207">Deployments</span></span>

<span data-ttu-id="04795-208">當您部署的範本，為群組和自動部署 Azure 曲目 hello 資源時，會指派名稱 toothis 部署群組。</span><span class="sxs-lookup"><span data-stu-id="04795-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="04795-209">hello 部署的 hello 名稱是 hello 與 hello hello 範本名稱相同。</span><span class="sxs-lookup"><span data-stu-id="04795-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="04795-210">如果您了解 hello 狀態 hello 部署中的資源，您可以使用 hello 資源群組 刀鋒視窗中 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="04795-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![取得部署資訊](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="04795-212">它不是問題 toouse hello 相同範本 toocreate 資源或 tooupdate 現有資源。</span><span class="sxs-lookup"><span data-stu-id="04795-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="04795-213">當您使用命令 toodeploy 範本時，您擁有 hello 機會 toosay 其中[模式](../../resource-group-template-deploy.md)想 toouse。</span><span class="sxs-lookup"><span data-stu-id="04795-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="04795-214">hello 模式可以設定 tooeither**完成**或**Incremental**。</span><span class="sxs-lookup"><span data-stu-id="04795-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="04795-215">hello 預設值為 toodo 累加式更新。</span><span class="sxs-lookup"><span data-stu-id="04795-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="04795-216">小心使用 hello**完成**模式因為您可能會不小心刪除資源。</span><span class="sxs-lookup"><span data-stu-id="04795-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="04795-217">當您將 hello 模式太**完成**，資源管理員就會刪除 hello 資源群組不在 hello 範本中的任何資源。</span><span class="sxs-lookup"><span data-stu-id="04795-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04795-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04795-218">Next Steps</span></span>

- <span data-ttu-id="04795-219">使用[編寫 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)來建立專屬範本。</span><span class="sxs-lookup"><span data-stu-id="04795-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="04795-220">部署使用所建立的 hello 範本[使用資源管理員範本建立 Windows 虛擬機器](ps-template.md)。</span><span class="sxs-lookup"><span data-stu-id="04795-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="04795-221">了解如何 toomanage hello 您藉由檢視所建立的 Vm[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="04795-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
