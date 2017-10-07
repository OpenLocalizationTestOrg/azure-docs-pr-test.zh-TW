---
title: "aaaTroubleshooting Linux VM 擴充功能失敗 |Microsoft 文件"
description: "了解如何針對 Linux VM 擴充功能的失敗進行疑難排解"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>針對 Azure Linux VM 擴充功能的失敗進行疑難排解
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>檢視擴充功能狀態
Azure 資源管理員範本可以執行從 hello Azure CLI。 一旦執行 hello 範本之後，可以從 Azure 資源總管或 hello 命令列工具檢視 hello 擴充功能狀態。

下列是一個範例：

Azure CLI：

      azure vm get-instance-view


以下是 hello 範例輸出：

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extenson-failures"></a>針對延伸模組失敗進行疑難排解：
### <a name="re-running-hello-extension-on-hello-vm"></a>重新執行 hello VM 上的 hello 延伸模組
如果您在 hello 使用自訂指令碼擴充的 VM 上執行指令碼，您有時可以執行已成功建立 VM，但失敗 hello 指令碼時發生錯誤。 在這些 conditons，建議您從這項錯誤的方式 toorecover hello tooremove hello 延伸模組並重新執行 hello 範本。
注意： 在未來，這項功能會增強的 tooremove hello 需要解除安裝 hello 擴充功能。

#### <a name="remove-hello-extension-from-azure-cli"></a>從 Azure CLI 移除 hello 延伸模組
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

其中"publsher name"對應 toohello 延伸類型，從 hello 輸出的 「 azure vm get-執行個體-檢視 」，而名稱是 hello hello 範本中的 hello 延伸模組資源名稱

一旦移除 hello 延伸模組，hello 範本可以是 hello VM 上的 重新執行的 toorun hello 指令碼。

