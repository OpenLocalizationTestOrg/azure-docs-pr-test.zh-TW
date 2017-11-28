---
title: "aaaUsing 預期狀態設定與虛擬機器擴展集 |Microsoft 文件"
description: "Hello Azure DSC 延伸模組搭配使用虛擬機器規模集"
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
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="4749a-103">Hello Azure DSC 延伸模組搭配使用虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="4749a-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="4749a-104">[虛擬機器擴展集](virtual-machine-scale-sets-overview.md)可以搭配 hello [Azure 預期狀態設定 (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)延伸模組處理常式。</span><span class="sxs-lookup"><span data-stu-id="4749a-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="4749a-105">虛擬機器擴展集提供方式 toodeploy 管理大量的虛擬機器，並可以彈性地及相應放大回應 tooload 中。</span><span class="sxs-lookup"><span data-stu-id="4749a-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="4749a-106">讓它們執行 hello 生產軟體進入線上時，DSC 會為使用的 tooconfigure hello Vm。</span><span class="sxs-lookup"><span data-stu-id="4749a-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="4749a-107">部署 tooVirtual 機器和虛擬機器擴展集之間的差異</span><span class="sxs-lookup"><span data-stu-id="4749a-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="4749a-108">虛擬機器擴展集 hello 基礎範本結構會稍有不同的單一 VM。</span><span class="sxs-lookup"><span data-stu-id="4749a-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="4749a-109">具體而言，單一 VM 將部署 hello"virtualMachines 」 節點下的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4749a-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="4749a-110">沒有型別"extensions"的項目 DSC 加入 toohello 範本</span><span class="sxs-lookup"><span data-stu-id="4749a-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="4749a-111">虛擬機器規模集節點有一個 「 屬性 」 區段以 hello"VirtualMachineProfile"，"extensionProfile"屬性。</span><span class="sxs-lookup"><span data-stu-id="4749a-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="4749a-112">已將 DSC 加入至 "extensions" 下方</span><span class="sxs-lookup"><span data-stu-id="4749a-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="4749a-113">虛擬機器擴展集的行為</span><span class="sxs-lookup"><span data-stu-id="4749a-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="4749a-114">虛擬機器規模集的 hello 行為是單一 VM 的相同 toohello 行為。</span><span class="sxs-lookup"><span data-stu-id="4749a-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="4749a-115">建立新的 VM 時，它會自動佈建以 hello DSC 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4749a-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="4749a-116">如果較新版的 hello hello 延伸模組所不需要 WMF，hello VM 重新開機才能回到線上。</span><span class="sxs-lookup"><span data-stu-id="4749a-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="4749a-117">一旦它在線上時，它會下載 hello DSC 組態.zip，並在 hello VM 上進行佈建。</span><span class="sxs-lookup"><span data-stu-id="4749a-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="4749a-118">更多詳細資料位於[hello Azure DSC 延伸模組概觀](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4749a-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4749a-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4749a-119">Next steps</span></span>
<span data-ttu-id="4749a-120">檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4749a-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4749a-121">深入了解如何 hello [DSC 延伸模組安全地處理認證](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4749a-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="4749a-122">如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4749a-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="4749a-123">如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="4749a-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

