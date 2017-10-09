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
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a>使用 Azure CLI 1.0 設定網路安全性群組流量記錄

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。 這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。 網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。

## <a name="register-insights-provider"></a>註冊 Insights 提供者

為了讓流量記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。 如果您不確定是否 hello **Microsoft.Insights**提供者是已註冊，請執行的 hello 下列指令碼。

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a>啟用網路安全性群組流量記錄

hello 命令 tooenable 流程記錄檔以 hello 下列範例所示：

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a>停用網路安全性群組流量記錄

下列範例 toodisable 流程記錄檔使用 hello:

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a>下載流量記錄

hello 流程記錄檔的儲存位置是在建立時定義。 這些非固定格式儲存的記錄檔 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載方便的工具 tooaccess: http://storageexplorer.com/

如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hello 結構 hello 記錄檔的相關資訊請造訪[網路安全性群組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>後續步驟

了解如何太[視覺化與 PowerBI NSG 流程記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)

了解如何太[視覺化 NSG 流程記錄與開放原始碼工具](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
