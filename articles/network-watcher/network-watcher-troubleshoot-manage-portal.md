---
title: "aaaTroubleshoot Azure 虛擬網路閘道與連線-PowerShell |Microsoft 文件"
description: "此頁面說明 toouse hello Azure 網路監看員如何疑難排解 PowerShell cmdlet"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>使用 Azure 網路監看員 PowerShell 來針對虛擬網路閘道和連線進行疑難排解

> [!div class="op_single_selector"]
> - [入口網站](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。 這些功能的其中之一便是資源疑難排解。 疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。 呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。

## <a name="overview"></a>概觀

疑難排解資源提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。 當提出要求時 tooresource 疑難排解記錄檔正在檢查和查詢。 檢查完成時，會傳回 hello 結果。 疑難排解要求是長時間執行的資源要求，但這可能需要多個分鐘 tooreturn 結果。 hello 疑難排解記錄檔會儲存在指定的儲存體帳戶的容器。

## <a name="troubleshoot-a-gateway-or-connection"></a>針對閘道或連線進行疑難排解

1. 瀏覽 toohello [Azure 入口網站](https://portal.azure.com)按一下**網路** > **網路監看員** > **VPN 診斷**
2. 選取 [訂用帳戶]、[資源群組] 和 [位置]。
3. 疑難排解資源傳回 hello hello 資源健全狀況的相關資料。 它也會儲存 toobe 檢閱相關的記錄檔 tooa 儲存體帳戶。 按一下**儲存體帳戶**tooselect 儲存體帳戶。
4. 在 hello**儲存體帳戶**刀鋒視窗中，選取現有的儲存體帳戶，或按一下**+ 儲存體帳戶**toocreate 新建一個。
5. 在 hello**容器**刀鋒視窗中，選擇現有的容器，或按一下**+ 容器**toocreate 新的容器。 完成時，按一下 [選取]
6. 選取 hello 資源 tootroubleshoot 閘道與連線，然後按一下**啟動疑難排解**

如果選取多個資源，系統會在這些閘道資源上同時執行疑難排解。 它不可以在連接上執行，以及它有相關聯的 hello 位於閘道相同的時間。 建議 tootroubleshoot 閘道第一次為連接疑難排解是較長的程序。 資源 hello 執行 VPN 診斷時**疑難排解狀態**資料行將會顯示狀態為**執行**

完成時，hello 狀態資料行變更太**狀況良好**或**狀況不良**。

![疑難排解完成][2]

## <a name="understanding-hello-results"></a>了解 hello 結果

在 hello**詳細資料**區段 hello 視窗的 hello**狀態**索引標籤會顯示 hello 狀態 hello 最後疑難排解執行選取的 hello 資源上。 Hello 最新診斷的結果會顯示的 xx 分鐘 hello 上次執行之後。

|屬性  |說明  |
|---------|---------|
|資源     | 連結 toohello 資源。        |
|儲存體路徑     |  路徑 toohello 儲存體帳戶和容器，包含 hello 的記錄檔 （如果有任何已 hello 執行期間所產生）。 此設定不會保存，當您離開 hello 入口網站。        |
|摘要     | Hello 資源健全狀況的摘要。        |
|詳細資料     | Hello 資源健全狀況的詳細的資訊。        |
|上次執行     | 上次 hello 時間 hello 時間疑難排解已執行。        |


hello**動作** 索引標籤提供一般指引 tooresolve hello 問題的方式。 Hello 問題，可以採取的動作，如果是其他指南提供的連結。 Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。  如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>後續步驟

如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
