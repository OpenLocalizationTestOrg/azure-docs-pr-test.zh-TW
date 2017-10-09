---
title: "aaaManage 網路安全性群組流程記錄與 Azure 網路監看員-Azure CLI 1.0 |Microsoft 文件"
description: "此頁面說明 toomanage 網路安全性群組資料流程中使用 Azure CLI 1.0 的 Azure 網路監看員的記錄檔"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="7d21b-103">使用 Azure CLI 1.0 設定網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7d21b-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7d21b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7d21b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="7d21b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d21b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="7d21b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7d21b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="7d21b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7d21b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="7d21b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7d21b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="7d21b-109">網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。</span><span class="sxs-lookup"><span data-stu-id="7d21b-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="7d21b-110">這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。</span><span class="sxs-lookup"><span data-stu-id="7d21b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="7d21b-111">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="7d21b-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7d21b-112">網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。</span><span class="sxs-lookup"><span data-stu-id="7d21b-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="7d21b-113">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="7d21b-113">Register Insights provider</span></span>

<span data-ttu-id="7d21b-114">為了讓流量記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="7d21b-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="7d21b-115">如果您不確定是否 hello **Microsoft.Insights**提供者是已註冊，請執行的 hello 下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d21b-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="7d21b-116">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7d21b-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="7d21b-117">hello 命令 tooenable 流程記錄檔以 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7d21b-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="7d21b-118">停用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="7d21b-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="7d21b-119">下列範例 toodisable 流程記錄檔使用 hello:</span><span class="sxs-lookup"><span data-stu-id="7d21b-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="7d21b-120">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="7d21b-120">Download a Flow log</span></span>

<span data-ttu-id="7d21b-121">hello 流程記錄檔的儲存位置是在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="7d21b-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="7d21b-122">這些非固定格式儲存的記錄檔 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載方便的工具 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7d21b-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7d21b-123">如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="7d21b-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="7d21b-124">Hello 結構 hello 記錄檔的相關資訊請造訪[網路安全性群組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7d21b-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d21b-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d21b-125">Next Steps</span></span>

<span data-ttu-id="7d21b-126">了解如何太[視覺化與 PowerBI NSG 流程記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="7d21b-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="7d21b-127">了解如何太[視覺化 NSG 流程記錄與開放原始碼工具](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="7d21b-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
