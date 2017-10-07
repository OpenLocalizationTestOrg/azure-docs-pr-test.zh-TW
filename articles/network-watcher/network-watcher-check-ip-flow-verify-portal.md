---
title: "驗證與 Azure 網路監看員 IP 流量 aaaVerify 流量-Azure 入口網站 |Microsoft 文件"
description: "本文說明如何 toocheck 如果允許或拒絕流量 tooor 從虛擬機器"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
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


IP 流量驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。 hello 驗證可以執行傳入或傳出的流量。 這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或其他資源的目前狀態。 IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。 另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員或具有網路監看員的現有執行個體。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

此案例使用 IP 流程確認 tooverify，如果虛擬機器可以彼此 tooanother 機器通訊透過連接埠 443。 如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。 toolearn 深入了解 IP 流程驗證，請瀏覽[IP 流程確認概觀](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>執行 IP 流量驗證

瀏覽 tooyour 網路監看員，並按一下**IP 流量確認**。 選取 hello 虛擬機器和網路介面您想要從 tooverify 流量。 輸入任何其他篩選的資訊，然後按一下 [檢查]。

一旦您按一下**檢查**，會檢查您所提供的 hello 準則為基礎的 hello 流程。 hello 結果是**允許存取**或**拒絕存取**。 如果存取被拒，hello 網路安全性群組 (NSG)，並提供封鎖流量的安全性規則。 Hello 拒絕的流量是預期的行為，然後 hello 規則成功。

> [!NOTE]
> IP 流量確認需要 hello VM 資源一配置。

您可以從下列映像的 hello 看到，已允許 hello 輸出的 HTTPS 流量。

![IP 流量驗證概觀][1]

Hello 下列影像所示，變更流量 tooinbound 和 hello 輸入連接埠變更 too123。 現在拒絕的流量，以及 hello 網路安全性群組和安全性規則，拒絕 hello 流量提供 hello 訊息 「 拒絕存取 」。

![IP 流量結果][2]

## <a name="next-steps"></a>後續步驟

如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack hello 網路安全性群組和安全性規則所定義的關閉。

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













