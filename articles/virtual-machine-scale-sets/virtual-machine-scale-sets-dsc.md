---
title: "搭配虛擬機器擴展集使用期望狀態組態 | Microsoft Docs"
description: "搭配 Azure DSC 擴充功能使用虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="0cec8-103">搭配 Azure DSC 擴充功能使用虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="0cec8-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="0cec8-104">[虛擬機器擴展集](virtual-machine-scale-sets-overview.md)可以搭配 [Azure 期望狀態設定 (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 擴充功能處理常式來使用。</span><span class="sxs-lookup"><span data-stu-id="0cec8-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="0cec8-105">虛擬機器擴展集提供一個部署及管理大量虛擬機器的方式，可以因應負載情況來彈性地相應縮小和放大。</span><span class="sxs-lookup"><span data-stu-id="0cec8-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="0cec8-106">當 VM 上線時，可使用 DSC 來設定它們，因為它們正在執行生產環境的軟體。</span><span class="sxs-lookup"><span data-stu-id="0cec8-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="0cec8-107">部署至虛擬機器與部署至虛擬機器擴展集之間的差異</span><span class="sxs-lookup"><span data-stu-id="0cec8-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="0cec8-108">適用於虛擬機器擴展集的基礎範本結構與單一 VM 有些微不同。</span><span class="sxs-lookup"><span data-stu-id="0cec8-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="0cec8-109">具體來說，單一 VM 會在 "virtualMachines" 節點下部署擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0cec8-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="0cec8-110">有一個類型為 "extensions" 且已將 DSC 加入範本的項目</span><span class="sxs-lookup"><span data-stu-id="0cec8-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

<span data-ttu-id="0cec8-111">虛擬機器擴展集節點具有 "properties" 區段以及 "VirtualMachineProfile"、"extensionProfile" 屬性。</span><span class="sxs-lookup"><span data-stu-id="0cec8-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="0cec8-112">已將 DSC 加入至 "extensions" 下方</span><span class="sxs-lookup"><span data-stu-id="0cec8-112">DSC is added under "extensions"</span></span>

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="0cec8-113">虛擬機器擴展集的行為</span><span class="sxs-lookup"><span data-stu-id="0cec8-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="0cec8-114">虛擬機器擴展集的行為與單一 VM 的行為完全相同。</span><span class="sxs-lookup"><span data-stu-id="0cec8-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="0cec8-115">建立新的 VM 時，會使用 DSC 擴充功能自動進行佈建。</span><span class="sxs-lookup"><span data-stu-id="0cec8-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="0cec8-116">如果擴充功能需要較新版本的 WMF，VM 會在上線之前重新開機。</span><span class="sxs-lookup"><span data-stu-id="0cec8-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="0cec8-117">一旦上線之後，它就會下載 DSC 組態 .zip，並在 VM 上佈建它。</span><span class="sxs-lookup"><span data-stu-id="0cec8-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="0cec8-118">您可以在 [Azure DSC 擴充功能概觀](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0cec8-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cec8-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cec8-119">Next steps</span></span>
<span data-ttu-id="0cec8-120">查看 [適用於 DSC 擴充功能的 Azure Resource Manager 範本](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0cec8-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0cec8-121">了解 [DSC 擴充功能如何安全地處理認證](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0cec8-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="0cec8-122">如需有關 Azure DSC 擴充功能處理常式的詳細資訊，請參閱 [Azure 期望狀態組態擴充功能處理常式簡介](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0cec8-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="0cec8-123">如需有關 PowerShell DSC 的詳細資訊，請 [瀏覽 PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="0cec8-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

