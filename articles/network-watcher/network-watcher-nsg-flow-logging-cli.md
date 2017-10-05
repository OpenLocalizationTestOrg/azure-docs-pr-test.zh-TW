---
title: "使用 Azure 網路監看員管理網路安全性群組流量記錄 - Azure CLI | Microsoft Docs"
description: "此頁面說明如何使用 Azure CLI 在 Azure 網路監看員中管理網路安全性群組流量記錄"
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
ms.openlocfilehash: d5a8aa0cd274132798a0d8484a950926761dae7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="dcab2-103">使用 Azure CLI 設定網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="dcab2-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="dcab2-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dcab2-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="dcab2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcab2-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="dcab2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dcab2-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="dcab2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dcab2-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="dcab2-108">REST API</span><span class="sxs-lookup"><span data-stu-id="dcab2-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="dcab2-109">網路安全性群組流量記錄是網路監看員的一項功能，可讓您檢視透過網路安全性群組傳輸之輸入和輸出 IP 流量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="dcab2-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="dcab2-110">這些流量記錄是以 json 格式撰寫，會顯示每一規則的輸出和輸入流量、流量套用至的 NIC、有關流量的 5 個 Tuple 資訊 (來源/目的地 IP、來源/目的地連接埠、通訊協定)，以及流量是被允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="dcab2-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="dcab2-111">本文使用資源管理部署模型的新一代 CLI：Azure CLI 2.0，它適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="dcab2-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="dcab2-112">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="dcab2-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="dcab2-113">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="dcab2-113">Register Insights provider</span></span>

<span data-ttu-id="dcab2-114">若要讓流量記錄成功運作，必須註冊 **Microsoft.Insights** 提供者。</span><span class="sxs-lookup"><span data-stu-id="dcab2-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="dcab2-115">如果您不確定是否已註冊 **Microsoft.Insights** 提供者，請執行下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="dcab2-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="dcab2-116">啟用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="dcab2-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="dcab2-117">用來啟用流量記錄的命令如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="dcab2-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="dcab2-118">停用網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="dcab2-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="dcab2-119">使用下列範例來停用流量記錄︰</span><span class="sxs-lookup"><span data-stu-id="dcab2-119">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="dcab2-120">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="dcab2-120">Download a Flow log</span></span>

<span data-ttu-id="dcab2-121">流量記錄的儲存位置會在建立時定義。</span><span class="sxs-lookup"><span data-stu-id="dcab2-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="dcab2-122">若要存取這些儲存至儲存體帳戶的流量記錄，Microsoft Azure 儲存體總管是很便利的工具，您可以在這裡下載︰http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="dcab2-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="dcab2-123">如果指定了儲存體帳戶，封包擷取檔案便會儲存到儲存體帳戶的下列位置︰</span><span class="sxs-lookup"><span data-stu-id="dcab2-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="dcab2-124">如需記錄結構的相關資訊，請造訪[網路安全性群組流量記錄概觀](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="dcab2-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcab2-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcab2-125">Next Steps</span></span>

<span data-ttu-id="dcab2-126">了解如何[使用 PowerBI 視覺化 NSG 流量記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="dcab2-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="dcab2-127">了解如何[使用開放原始碼工具視覺化 NSG 流量記錄](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="dcab2-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
