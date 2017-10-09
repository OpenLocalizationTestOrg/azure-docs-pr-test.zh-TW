---
title: "aaaTroubleshooting Windows VM 擴充功能失敗 |Microsoft 文件"
description: "了解如何針對 Azure Windows VM 擴充功能的失敗進行疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="25145-103">針對 Azure Windows VM 擴充功能的失敗進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="25145-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="25145-104">檢視擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="25145-104">Viewing extension status</span></span>
<span data-ttu-id="25145-105">Azure Resource Manager 範本可以從 Azure PowerShell 執行。</span><span class="sxs-lookup"><span data-stu-id="25145-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="25145-106">一旦執行 hello 範本之後，可以從 Azure 資源總管或 hello 命令列工具檢視 hello 擴充功能狀態。</span><span class="sxs-lookup"><span data-stu-id="25145-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="25145-107">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="25145-107">Here is an example:</span></span>

<span data-ttu-id="25145-108">Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="25145-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="25145-109">以下是 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="25145-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="25145-110">]</span><span class="sxs-lookup"><span data-stu-id="25145-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="25145-111">針對擴充功能失敗進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="25145-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="25145-112">重新執行 hello VM 上的 hello 延伸模組</span><span class="sxs-lookup"><span data-stu-id="25145-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="25145-113">如果您在 hello 使用自訂指令碼擴充的 VM 上執行指令碼，您有時可以執行已成功建立 VM，但失敗 hello 指令碼時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="25145-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="25145-114">在這些 conditons，建議您從這項錯誤的方式 toorecover hello tooremove hello 延伸模組並重新執行 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="25145-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="25145-115">注意： 在未來，這項功能會增強的 tooremove hello 需要解除安裝 hello 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="25145-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="25145-116">從 Azure PowerShell 移除 hello 延伸模組</span><span class="sxs-lookup"><span data-stu-id="25145-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="25145-117">一旦移除 hello 延伸模組，hello 範本可以是 hello VM 上的 重新執行的 toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="25145-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

