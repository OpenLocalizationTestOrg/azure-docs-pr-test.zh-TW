---
title: "與 Azure 網路監看員 IP 流程驗證-Azure CLI aaaVerify 流量 |Microsoft 文件"
description: "本文說明如何從虛擬機器的流量 tooor 允許或拒絕使用 Azure CLI 如果 toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>如果是允許或拒絕流量 tooor 從 IP 流程驗證 VM 的 Azure 網路監看員的元件，請檢查

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


IP 流程驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。 這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或後端的目前狀態。 IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。 另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員或具有網路監看員的現有執行個體。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

此案例使用 IP 流程確認 tooverify，如果虛擬機器可以彼此 tooa 通訊已知 Bing IP 位址。 如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。 toolearn 深入了解 IP 流程驗證，請瀏覽[IP 流程確認概觀](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>取得 VM

IP 流量，請確認測試流量 tooor 從虛擬機器 tooor 從遠端目的地上的 IP 位址。 Hello cmdlet 需要虛擬機器的識別碼。 如果您已經知道 hello 虛擬機器 toouse hello 識別碼，您可以略過此步驟。

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>取得 hello NIC

需要 hello 的 hello 虛擬機器上的 NIC 的 IP 位址，在此範例中我們擷取 hello Nic 的虛擬機器上。 如果您已經知道 hello IP 位址，您會想 tootest hello 虛擬機器上，您可以略過此步驟。

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>執行 IP 流量驗證

現在，我們已經 hello 資訊所需 toorun hello 指令程式，我們會執行 hello `network watcher ip-flow-verify` cmdlet tootest hello 流量。 在此範例中，我們會使用第一個 IP 位址 hello hello 第一個 NIC 上

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> 需要 hello VM 資源配置 toorun IP 流程驗證。

## <a name="review-results"></a>檢閱結果

執行之後`network watcher ip-flow-verify`hello 結果、 hello 下列範例是 hello hello 前面步驟所傳回的結果。

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>後續步驟

如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。

深入了解 tooaudit NSG 設定造訪[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)。

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
