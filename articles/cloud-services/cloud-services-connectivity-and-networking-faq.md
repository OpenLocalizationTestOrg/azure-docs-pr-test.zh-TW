---
title: "aaaConnectivity 和網路功能的問題，Microsoft Azure 雲端服務的常見問題集 |Microsoft 文件"
description: "本文列出 hello 連線和 Microsoft Azure 雲端服務的網路功能的相關常見問題集。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure 雲端服務之連線能力和網路服務問題：常見問題集 (FAQ)

本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之連線能力和網路服務問題的相關常見問題集。 此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>無法在多 VIP 的雲端服務中保留 IP
首先，請確定您正嘗試 tooreserve hello IP 用於該 hello 虛擬機器執行個體已開啟。 第二，請確定您正在使用保留 Ip 的同時 hello 預備和生產環境部署。 **不這麼做**hello 部署正在升級時，變更 hello 設定。

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>當我有 NSG 時，應如何設定遠端桌面？
新增規則 toohello 允許連接埠上的流量的 NSG **3389**和**20000**。  遠端桌面使用者連接埠 **3389**。  雲端服務執行個體是負載平衡，因此您無法直接控制至哪一個執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式管理 RDP 流量，並允許 hello 用戶端 toosend RDP cookie，並指定要個別執行個體 tooconnect。  hello *RemoteForwarder*和*RemoteAccess*代理程式需要該連接埠**20000**開啟，如果您有 NSG 可能會封鎖連接。

## <a name="can-i-ping-a-cloud-service"></a>是否可偵測雲端服務？

否，不是使用 hello normal"ping"/ ICMP 通訊協定。 hello ICMP 通訊協定不允許透過 hello Azure 負載平衡器。

建議您不要連接埠 ping tootest 連線。 當 Ping.exe 使用 ICMP 時，其他工具，例如 PSPing、 Nmap 及 telnet 可讓您 tootest 連線 tooa 特定 TCP 通訊埠。

如需詳細資訊，請參閱[改用 ICMP tootest Azure VM 連接的連接埠 ping](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/)。

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>如何停止接收數千個叫用來自未知的 IP 位址，以指出特定類型的惡意攻擊 toohello 雲端服務？
Azure 實作多層的網路安全性 tooprotect 分散式阻斷服務 (DDoS) 攻擊針對其平台服務。 hello Azure DDoS 防禦系統是 Azure 的連續監視處理序，以便透過滲透測試會持續改良的一部分。 此 DDoS 防禦系統設計 toowithstand 不僅攻擊從外部 hello 但來自其他 Azure 租用戶。 如需詳細資料，請參閱 [Microsoft Azure 網路安全性](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf)。

您也可以建立啟動工作 tooselectively 區塊一些特定的 IP 位址。 如需詳細資訊，請參閱[封鎖特定 IP 位址](cloud-services-startup-tasks-common.md#block-a-specific-ip-address)。

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>當我嘗試 tooRDP toomy 雲端服務執行個體時，我會收到 hello 訊息，「 hello 使用者帳戶已過期 」。
您略過您的 RDP 設定中的 hello 到期日時，可能會收到 hello 錯誤訊息 「 此使用者帳戶已過期 」。 您可以從 hello 入口網站中變更 hello 到期日，依照下列步驟：
1. 登入 toohello Azure 管理主控台 (https://manage.windowsazure.com)，瀏覽 tooyour 雲端服務，然後選取 hello**設定** 索引標籤。
2. 選取 [遠端]。
3. 變更 hello"過期於 」 日期，並儲存 hello 組態。

您現在應該能夠 tooRDP tooyour 機器。

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>為什麼負載平衡器並未平均平衡流量？
如需如何內部負載平衡器運作方式的相關資訊，請參閱 [Azure Load Balancer 的新分散模式](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/)。

使用的 hello 分配演算法是 5 個 tuple (來源 IP、 來源連接埠，目的地 IP、 目的地連接埠通訊協定類型) 雜湊 toomap 流量 tooavailable 伺服器。 它只在傳輸工作階段內提供綁定。 在相同的 TCP 或 UDP 工作階段將為的 hello 封包導向的 toohello hello 負載平衡端點之後執行個體的相同資料中心 IP (DIP)。 Hello 用戶端關閉並重新開啟 hello 連接或從 hello 開始新的工作階段時相同來源 IP，hello 來源連接埠變更，並造成 hello 流量 toogo tooa 不同 DIP 的端點。
