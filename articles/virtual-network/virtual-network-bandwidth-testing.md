---
title: "aaaTesting Azure VM 網路輸送量 |Microsoft 文件"
description: "了解如何 tootest Azure 虛擬機器的網路輸送量。"
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>頻寬/輸送量測試 (NTTTCP)

測試網路輸送量效能，請在 Azure 中時，最佳 toouse 目標 hello 網路進行測試，可能會影響效能的其他資源的 hello 使用降至最低的工具。 建議使用 NTTTCP。

複製 hello 工具 tootwo hello 的 Azure Vm 大小相同。 一個 VM 做為傳送者和接收者為其他 hello。

#### <a name="deploying-vms-for-testing"></a>部署用於測試的 VM
基於 hello 這項測試，兩個 Vm 應該位於 hello hello 相同雲端服務或 hello 相同可用性設定組，讓我們能夠使用其內部 Ip 並排除 hello 測試 hello 負載平衡器。 它是以 hello VIP 可能 tootest，但這種測試是在這份文件 hello 範圍之外。
 
記下 hello 接收者的 IP 位址。 讓我將該 IP 稱為 "a.b.c.r"

記下的核心數目 hello hello VM 上。 讓我們將此稱為 "\#num\_cores"
 
VM hello 寄件者和接收者 VM 上執行的 hello NTTTCP 測試 300 秒 （或 5 分鐘）。

提示： 當第一次設定這項測試的 hello，您可以嘗試較短的測試週期 tooget 意見反應更快。 一旦 hello 工具如預期般，擴充 hello 測試期間 too300 秒 hello 最精確的結果。

> [!NOTE]
> hello 寄件者**和**接收者必須指定**hello 相同**測試持續時間參數 (-t)。

tootest 10 秒的單一 TCP 資料流：

接收端參數：ntttcp -r -t 10 -P 1

傳送端參數：ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> 上述範例中的 hello 應該只能使用的 tooconfirm 您的設定。 本文稍後會提供有效的測試範例。

## <a name="testing-vms-running-windows"></a>測試執行 Windows 的 VM：

#### <a name="get-ntttcp-onto-hello-vms"></a>NTTTCP 進入 hello Vm。

下載最新版本的 hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

或搜尋它 (如果已移動)：<https://www.bing.com/search?q=ntttcp+download>\< -- 應該是第一個點選項目

請考慮將 NTTTCP 放在個別的資料夾，例如 c:\\tools

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>透過 hello 的 Windows 防火牆允許 NTTTCP
在 hello 接收者，建立允許規則 hello Windows 防火牆 tooallow 上的 NTTTCP 流量 tooarrive。 它是最簡單 tooallow hello 整個 NTTTCP 程式名稱而不是輸入 tooallow 特定 TCP 連接埠。

允許 ntttcp 透過 hello Windows 防火牆，就像這樣：

netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

例如，如果您複製 ntttcp.exe toohello"c:\\工具 」 資料夾中，這會是 hello 命令： 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>執行 NTTTCP 測試

Hello 接收者上啟動 NTTTCP (**從 CMD 執行**，而不是從 PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

如果 hello VM 有四個核心和 IP 位址為 10.0.0.4，它看起來會像這樣：

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Hello 寄件者上啟動 NTTTCP (**從 CMD 執行**，而不是從 PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

等候 hello 結果。


## <a name="testing-vms-running-linux"></a>測試執行 Linux 的 VM：

請使用 nttcp-for-linux。 可從 <https://github.com/Microsoft/ntttcp-for-linux> 取得

在 hello Linux Vm （傳送者和接收者），執行這些命令來準備 ntttcp-為-linux Vm 上：

CentOS - 安裝 Git：
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - 安裝 Git：
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
在兩部機器上都建立並安裝：
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

如同 hello Windows 範例中，我們假設是 10.0.0.4 hello Linux 接收者的 IP。

啟動 NTTTCP 為 Linux hello 接收者上：

``` bash
ntttcp -r -t 300
```

然後在 hello 寄件者，執行：

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
指定測試長度預設值 too60 秒如果沒有時間參數

## <a name="testing-between-vms-running-windows-and-linux"></a>在執行 Windows 和 LINUX 的 VM 之間進行測試：

此案例中，我們應該啟用 hello 沒有同步處理模式讓 hello 測試執行。 這是使用 hello **-N 旗標**for Linux，和**奈旗標**for Windows。

#### <a name="from-linux-toowindows"></a>從 Linux tooWindows:

接收者 <Windows>：

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

傳送者 <Linux>：

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>從 Windows tooLinux:

接收者 <Linux>：

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

傳送者 <Windows>：

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>後續步驟
* 根據不同的結果，可能有空間太[最佳化網路輸送量機器](virtual-network-optimize-network-bandwidth.md)您的案例。
* 深入了解 [Azure 虛擬網路的常見問題 (FAQ)](virtual-networks-faq.md)
