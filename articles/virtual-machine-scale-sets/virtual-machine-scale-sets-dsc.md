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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Hello Azure DSC 延伸模組搭配使用虛擬機器規模集
[虛擬機器擴展集](virtual-machine-scale-sets-overview.md)可以搭配 hello [Azure 預期狀態設定 (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)延伸模組處理常式。 虛擬機器擴展集提供方式 toodeploy 管理大量的虛擬機器，並可以彈性地及相應放大回應 tooload 中。 讓它們執行 hello 生產軟體進入線上時，DSC 會為使用的 tooconfigure hello Vm。

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>部署 tooVirtual 機器和虛擬機器擴展集之間的差異
虛擬機器擴展集 hello 基礎範本結構會稍有不同的單一 VM。 具體而言，單一 VM 將部署 hello"virtualMachines 」 節點下的延伸模組。 沒有型別"extensions"的項目 DSC 加入 toohello 範本

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

虛擬機器規模集節點有一個 「 屬性 」 區段以 hello"VirtualMachineProfile"，"extensionProfile"屬性。 已將 DSC 加入至 "extensions" 下方

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a>虛擬機器擴展集的行為
虛擬機器規模集的 hello 行為是單一 VM 的相同 toohello 行為。 建立新的 VM 時，它會自動佈建以 hello DSC 延伸模組。 如果較新版的 hello hello 延伸模組所不需要 WMF，hello VM 重新開機才能回到線上。 一旦它在線上時，它會下載 hello DSC 組態.zip，並在 hello VM 上進行佈建。 更多詳細資料位於[hello Azure DSC 延伸模組概觀](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="next-steps"></a>後續步驟
檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

深入了解如何 hello [DSC 延伸模組安全地處理認證](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。 

