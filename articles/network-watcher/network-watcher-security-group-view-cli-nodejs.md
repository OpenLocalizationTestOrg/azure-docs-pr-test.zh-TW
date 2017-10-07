---
title: "與 Azure 網路監看員安全性群組檢視 Azure CLI 1.0 aaaAnalyze 網路安全性 |Microsoft 文件"
description: "本文將說明如何 toouse Azure CLI 1.0 tooanalyze 的虛擬機器安全性與安全性的群組檢視。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="9b05b-103">使用 Azure CLI 1.0，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="9b05b-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9b05b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b05b-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="9b05b-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9b05b-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="9b05b-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9b05b-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="9b05b-107">REST API</span><span class="sxs-lookup"><span data-stu-id="9b05b-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="9b05b-108">安全性的群組檢視會傳回已設定且有效的網路安全性規則所套用的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9b05b-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="9b05b-109">這項功能會很有用的 tooaudit 及診斷網路安全性群組和 VM tooensure 流量所設定的規則已正確地允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="9b05b-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="9b05b-110">在本文中，我們會示範如何設定 tooretrieve hello 和有效的安全性規則 tooa 虛擬機器使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b05b-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="9b05b-111">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="9b05b-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="9b05b-112">網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。</span><span class="sxs-lookup"><span data-stu-id="9b05b-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b05b-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="9b05b-113">Before you begin</span></span>

<span data-ttu-id="9b05b-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="9b05b-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="9b05b-115">案例</span><span class="sxs-lookup"><span data-stu-id="9b05b-115">Scenario</span></span>

<span data-ttu-id="9b05b-116">hello 案例涵蓋在本文中擷取設定的 hello 和指定的虛擬機器的有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="9b05b-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="9b05b-117">取得 VM</span><span class="sxs-lookup"><span data-stu-id="9b05b-117">Get a VM</span></span>

<span data-ttu-id="9b05b-118">虛擬機器為必要的 toorun hello `vm list` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9b05b-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="9b05b-119">hello 下列命令會列出資源群組中的 hello 虛擬 machinese:</span><span class="sxs-lookup"><span data-stu-id="9b05b-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="9b05b-120">一旦您知道 hello 虛擬機器，您可以使用 hello `vm show` cmdlet tooget 其資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="9b05b-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="9b05b-121">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="9b05b-121">Retrieve security group view</span></span>

<span data-ttu-id="9b05b-122">hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。</span><span class="sxs-lookup"><span data-stu-id="9b05b-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="9b05b-123">新增 hello"-json 」 旗標將會在 json 中的 hello 結果格式化。</span><span class="sxs-lookup"><span data-stu-id="9b05b-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="9b05b-124">檢視 hello 結果</span><span class="sxs-lookup"><span data-stu-id="9b05b-124">Viewing hello results</span></span>

<span data-ttu-id="9b05b-125">hello 下列範例是縮短的回應 hello 傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="9b05b-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="9b05b-126">hello 結果會顯示所有 hello 有效且套用安全性規則 hello 細分的群組中的虛擬機器上**NetworkInterfaceSecurityRules**， **DefaultSecurityRules**，和**EffectiveSecurityRules**。</span><span class="sxs-lookup"><span data-stu-id="9b05b-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="9b05b-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b05b-127">Next steps</span></span>

<span data-ttu-id="9b05b-128">請瀏覽[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)toolearn 如何 tooautomate 驗證的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9b05b-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="9b05b-129">深入了解 hello 安全性規則所套用的 tooyour 網路資源，造訪[安全性的群組檢視概觀](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9b05b-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
