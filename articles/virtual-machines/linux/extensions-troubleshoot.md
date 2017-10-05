---
title: "針對 Linux VM 擴充功能的失敗進行疑難排解 | Microsoft Docs"
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
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="1b929-103">針對 Azure Linux VM 擴充功能的失敗進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1b929-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="1b929-104">檢視擴充功能狀態</span><span class="sxs-lookup"><span data-stu-id="1b929-104">Viewing extension status</span></span>
<span data-ttu-id="1b929-105">Azure Resource Manager 範本可以從 Azure CLI 執行。</span><span class="sxs-lookup"><span data-stu-id="1b929-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="1b929-106">一旦執行範本之後，即可以從 Azure 資源總管或命令列工具檢視延伸模組狀態。</span><span class="sxs-lookup"><span data-stu-id="1b929-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="1b929-107">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="1b929-107">Here is an example:</span></span>

<span data-ttu-id="1b929-108">Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="1b929-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="1b929-109">以下是範例輸出：</span><span class="sxs-lookup"><span data-stu-id="1b929-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="1b929-110">]</span><span class="sxs-lookup"><span data-stu-id="1b929-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="1b929-111">針對延伸模組失敗進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="1b929-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="1b929-112">在 VM 上重新執行擴充功能</span><span class="sxs-lookup"><span data-stu-id="1b929-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="1b929-113">如果您使用自訂指令碼擴充功能在 VM 上執行指令碼，有時候可能會遇到雖然成功建立了 VM 但指令碼卻失敗的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1b929-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="1b929-114">在這樣的情況下，若要從錯誤中復原，建議您移除延伸模組並再次重新執行範本。</span><span class="sxs-lookup"><span data-stu-id="1b929-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="1b929-115">請注意：未來將增強這項功能，以移除對解除安裝延伸模組的需求。</span><span class="sxs-lookup"><span data-stu-id="1b929-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="1b929-116">從 Azure CLI 移除擴充功能</span><span class="sxs-lookup"><span data-stu-id="1b929-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="1b929-117">其中 "publsher-name" 對應的延伸模組類型來自 "azure vm get-instance-view" 的輸出，而名稱是來自範本的延伸模組資源名稱</span><span class="sxs-lookup"><span data-stu-id="1b929-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="1b929-118">一旦移除了延伸模組，範本就可以重新執行並在 VM 上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="1b929-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

