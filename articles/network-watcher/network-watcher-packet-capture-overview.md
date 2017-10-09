---
title: "在 Azure 網路監看員 aaaIntroduction tooPacket 擷取 |Microsoft 文件"
description: "此頁面提供 hello 網路監看員封包擷取功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>在 Azure 網路監看員的簡介 toovariable 封包擷取

網路監看員變數的封包擷取可讓您 toocreate 封包擷取工作階段 tootrack 流量 tooand 從虛擬機器。 封包擷取協助 toodiagnose 網路異常這兩個被動和 proactivity。 其他用途包括收集網路統計資料，取得有關網路入侵，toodebug 用戶端與伺服器通訊，以及執行更多。

封包擷取是透過網路監看員從遠端啟動的虛擬機器擴充功能。 這項功能可以減輕工作 hello 負擔 hello 預期虛擬機器上，以節省寶貴的時間手動執行封包擷取。 透過 hello 入口網站、 PowerShell、 CLI 或 REST API，可以觸發封包擷取。 觸發封包擷取方式的其中一個範例是使用虛擬機器警示。 篩選器會提供如 hello 擷取工作階段 tooensure 您擷取您想要 toomonitor 的流量。 篩選是根據 5 個 Tuple (通訊協定、本機 IP 位址、遠端 IP 位址、本機連接埠，以及遠端連接埠) 的資訊。 hello 擷取的資料會儲存在 hello 本機磁碟或儲存體 blob。 每個訂用帳戶在每個區域皆有 10 個封包擷取工作階段的限制。 這項限制適用於只有 toohello 工作階段，但不適用於 toohello hello VM 在本機或儲存體帳戶中儲存封包擷取檔案。

> [!IMPORTANT]
> 封包擷取需要虛擬機器擴充功能 `AzureNetworkWatcherExtension`。 Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).

tooreduce hello 資訊擷取您想要的 tooonly hello 資訊、 hello 有下列選項的封包擷取工作階段：

**擷取設定**

|屬性|說明|
|---|---|
|**每個封包的最大位元組 (位元組)** | hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。 hello 數目的每個封包所擷取的位元組，如果保留空白，會擷取所有位元組。 如果您需要唯一的 hello IPv4 標頭 – 表示這裡 34 |
|**每個工作階段的最大位元組 (位元組)** | Hello 值達到 hello 工作階段結束之後，會擷取中的位元組總數。|
|**時間限制 (秒)** | 設定時間限制，在 hello 封包擷取工作階段。 hello 預設值是 18000 秒或 5 小時。|

**篩選 (選用)**

|屬性|說明|
|---|---|
|**通訊協定** | hello 通訊協定 toofilter hello 封包擷取。 hello 可用的值為 TCP、 UDP 和所有。|
|**本機 IP 位址** | 這個值會篩選 hello 封包擷取 toopackets 其中 hello 本機 IP 位址必須符合此篩選值。|
|**本機連接埠** | 這個值篩選 hello 封包擷取的 toopackets hello 本機連接埠符合此篩選值的位置。|
|**遠端 IP 位址** | 這個值篩選 hello 封包擷取的 toopackets hello 遠端 IP 符合此篩選值的位置。|
|**遠端連接埠** | 這個值篩選 hello 封包擷取的 toopackets hello 遠端連接埠符合此篩選值的位置。|

### <a name="next-steps"></a>後續步驟

了解管理封包擷取透過 hello 入口網站，造訪[管理 hello Azure 入口網站中的封包擷取](network-watcher-packet-capture-manage-portal.md)或 PowerShell 造訪[使用 PowerShell 管理封包擷取](network-watcher-packet-capture-manage-powershell.md)。

深入了解如何 toocreate 主動式封包擷取根據虛擬機器警示造訪[建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













