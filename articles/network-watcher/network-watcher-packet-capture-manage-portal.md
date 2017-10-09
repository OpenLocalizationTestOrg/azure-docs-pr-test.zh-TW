---
title: "Azure 網路監看員-Azure 入口網站擷取 aaaManage 封包 |Microsoft 文件"
description: "此頁面可讓您說明如何 toomanage hello 封包擷取功能，使用 Azure 入口網站的網路監看員"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>使用 Azure 網路監看員使用 hello 入口網站管理封包擷取

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

網路監看員封包擷取可讓您 toocreate 擷取工作階段 tootrack 流量 tooand 從虛擬機器。 篩選器可供 hello 擷取工作階段 tooensure 擷取您想要只 hello 流量。 封包擷取可在主動和被動協助 toodiagnose 網路異常狀況。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。 透過無法 tooremotely 觸發程序封包擷取，這項功能可以減輕工作 hello 負擔的手動和 hello 想要在電腦上，以節省寶貴的時間執行封包擷取。

這篇文章帶領您完成 hello 封包擷取目前可用的不同的管理工作。

- [**啟動封包擷取**](#start-a-packet-capture)
- [**停止封包擷取**](#stop-a-packet-capture)
- [**刪除封包擷取**](#delete-a-packet-capture)
- [**下載封包擷取**](#download-a-packet-capture)

## <a name="before-you-begin"></a>開始之前

本文假設您擁有 hello 下列資源：

- 執行個體要在 hello 區域網路監看員的 toocreate 封包擷取
- 虛擬機器與 hello 封包擷取啟用擴充功能。

> [!IMPORTANT]
> 封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。 Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>透過 hello 入口網站的封包擷取代理程式延伸

tooinstall hello 封包擷取 VM 代理程式，透過 hello 入口網站，瀏覽 tooyour 虛擬機器，按一下**延伸** > **新增**並搜尋**網路監看員的代理程式 」Windows**

![代理程式檢視][agent]

## <a name="packet-capture-overview"></a>封包擷取概觀

瀏覽 toohello [Azure 入口網站](https://portal.azure.com)按一下**網路** > **網路監看員** > **封包擷取**

hello 概觀頁面會顯示一份所有封包擷取存在於無論 hello 狀態。

> [!NOTE]
> 封包擷取需要透過連接埠 443 的連線能力 toohello 儲存體帳戶。

![封包擷取概觀畫面][1]

## <a name="start-a-packet-capture"></a>啟動封包擷取

按一下**新增**toocreate 封包擷取。

您可以定義封包擷取的 hello 屬性如下：

**主要設定**

- **訂用帳戶**-此值為 hello 訂用帳戶時，需要每個訂用帳戶中的網路監看員執行個體。
- **資源群組**-hello hello 做為目標的虛擬機器的資源群組。
- **目標虛擬機器**-hello 虛擬機器執行 hello 封包擷取
- **封包擷取名稱**-這個值是 hello hello 封包擷取名稱。

**擷取設定**

- **儲存體帳戶** - 決定封包擷取是否會儲存在儲存體帳戶中。
- **檔案**-決定是否封包擷取本機儲存在 hello 虛擬機器上。
- **儲存體帳戶**-hello 選取儲存體帳戶 toosave hello 封包中的擷取。 預設位置是 https://{儲存體帳戶名稱}.blob.core.windows.net/network-watcher-logs/subscriptions/{訂用帳戶識別碼}/resourcegroups/{資源群組名稱}/providers/microsoft.compute/virtualmachines/{虛擬機器名稱}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap。 (只在選取**儲存體**時才會啟用)
- **本機檔案路徑**-hello 本機路徑上的虛擬機器 toosave hello 封包擷取。 (只在選取**檔案**時才會啟用)。 必須提供有效的路徑
- **每個封包的最大位元組**-hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。
- **每個工作階段的最大位元組**-總計的擷取，一旦達到 hello 封包擷取停駐點 hello 值的位元組數。
- **時間限制 （秒）** -設定 hello 封包擷取 toostop 時間限制。 預設值為 18000 秒。

> [!NOTE]
> 儲存封包擷取目前不支援進階儲存體帳戶。

**篩選 (選用)**

- **通訊協定**-hello 通訊協定 toofilter hello 封包擷取。 hello 可用的值為 TCP、 UDP 和任何。
- **本機 IP 位址**-這個值會篩選 hello 封包擷取 toopackets 其中 hello 本機 IP 位址必須符合此篩選值。
- **本機連接埠**-這個值會篩選 hello 封包擷取 toopackets hello 本機連接埠符合此篩選值的位置。
- **遠端 IP 位址**-這個值會篩選 hello 封包擷取 toopackets hello 遠端 IP 符合此篩選值的位置。
- **遠端連接埠**-這個值會篩選 hello 封包擷取 toopackets hello 遠端連接埠符合此篩選值的位置。

> [!NOTE]
> 連接埠和 IP 位址的值可以是單一值、值的範圍或一組。 (也就是連接埠的 80-1024) 您可以定義所有您想要的篩選。

一旦 hello 值都已填寫，按一下 **確定**toocreate hello 封包擷取。

![建立封包擷取][2]

在設定 hello 時限後 hello 封包擷取已過期，hello 封包擷取將會停止，而且可以進行檢閱。 您可以手動停止 hello 封包擷取工作階段。

## <a name="delete-a-packet-capture"></a>刪除封包擷取

在 hello 封包擷取檢視中，按一下 hello**操作功能表**（...） 或以滑鼠右鍵按一下，然後按一下**刪除**toostop hello 封包擷取

![刪除封包擷取][3]

> [!NOTE]
> 刪除封包擷取並不會刪除 hello 儲存體帳戶中的 hello 檔案。

系統會要求您按一下您想要 toodelete hello 封包擷取，tooconfirm **[是]**

![確認][4]

## <a name="stop-a-packet-capture"></a>停止封包擷取

在 hello 封包擷取檢視中，按一下 hello**操作功能表**（...） 或以滑鼠右鍵按一下，然後按一下**停止**toostop hello 封包擷取

## <a name="download-a-packet-capture"></a>下載封包擷取

您的封包擷取工作階段完成後，請 hello 擷取檔案是上傳的 tooblob 儲存體或 tooa 本機檔案 hello VM 上。 hello 封包擷取 hello 儲存位置被定義在 hello 工作階段的建立。 方便的工具 tooaccess 這些擷取的檔案儲存的 tooa 儲存體帳戶是 Microsoft Azure 儲存體總管 中，這可以在這裡下載： http://storageexplorer.com/

如果指定的儲存體帳戶，則封包擷取檔案會儲存在下列位置的 hello tooa 儲存體帳戶：
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>後續步驟

了解如何 tooautomate 封包擷取虛擬機器警示藉由檢視[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)

造訪[檢查 IP 流量驗證](network-watcher-check-ip-flow-verify-portal.md)來得知 VM 是否允許特定流量流入或流出

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













