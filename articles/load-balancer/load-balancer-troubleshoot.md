---
title: "aaaTroubleshoot Azure 負載平衡器 |Microsoft 文件"
description: "針對 Azure Load Balancer 的已知問題進行疑難排解"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>針對 Azure Load Balancer 進行疑難排解

此頁面提供 Azure Load Balancer 常見問題的疑難排解資訊。 Hello 負載平衡器連線無法使用時，hello 最常見的徵兆如下： 
- Hello 負載平衡器後方的 Vm 都沒有回應 toohealth 探查 
- Hello 負載平衡器後方的 Vm 都沒有回應 hello 設定連接埠上的 toohello 流量

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>徵兆： Hello 負載平衡器後方的 Vm 都沒有回應 toohealth 探查
集中 hello 負載平衡器後端伺服器 tooparticipate hello，它們必須通過 hello 探查核取。 如需健康狀態探查的詳細資訊，請參閱[了解負載平衡器探查](load-balancer-custom-probe-overview.md)。 

hello 負載平衡器後端集區的 Vm 可能沒有回應探查 toohello 到期 tooany 的 hello 下列原因： 
- 負載平衡器後端集區 VM 的健康狀態不良 
- 負載平衡器後端集區 VM 未接聽 hello 探查連接埠 
- 防火牆或網路安全性小組已封鎖 hello hello 負載平衡器後端集區的 Vm 上的連接埠 
- 負載平衡器中的其他設定錯誤

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>原因 1︰負載平衡器後端集區 VM 的健康狀態不良 

**驗證和解決方式**

tooresolve 這個問題，請登入參與的 Vm，toohello，並檢查是否 hello VM 狀態為狀況良好，並可在回應太**PsPing**或**TCPing**從 hello 集區中的另一個 VM。 如果 hello VM 會處於狀況不良，或無法 toorespond toohello 探查，您必須更正 hello 問題並取得的 hello VM 可以參與負載平衡之前，備份 tooa 狀況良好狀態。

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>原因 2： 負載平衡器後端集區 VM 未接聽 hello 探查連接埠
如果 hello VM 的狀況良好，但沒有回應 toohello 探查，然後一個可能的原因可能 hello 探查連接埠上未開啟 hello 參與 VM，或者 hello VM 未接聽該通訊埠。

**驗證和解決方式**

1. 登入 toohello 後端 VM。 
2. 開啟命令提示字元並執行下列命令 toovalidate 沒有接聽 hello 探查連接埠之應用程式的 hello:   
            netstat -an
3. 如果 hello 連接埠狀態未列為**聆聽**，設定 hello 適當的連接埠。 
4. 或者，選取其他已列為 **LISTENING** 的連接埠，並據此更新負載平衡器組態。              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>原因 3： 防火牆或網路安全性小組已封鎖 hello hello 負載平衡器後端集區的 Vm 上的連接埠  
Hello hello hello 探查連接埠或一或多個網路安全性群組 hello VM，或 hello 子網路上設定封鎖 VM 上的防火牆不允許 hello 探查 tooreach hello 連接埠，hello VM 無法 toorespond toohello 健全狀況探查。          

**驗證和解決方式**

* 如果啟用 hello 防火牆，請檢查它是否已設定 tooallow hello 探查連接埠。 如果不是，設定 hello 防火牆 tooallow 流量 hello 探查連接埠，然後重新測試。 
* 從網路安全性群組的 hello 清單中，檢查 hello hello 探查連接埠上的傳入或傳出流量是否干擾。 
* 另請檢查 如果**Deny All**網路安全性群組規則 hello 的 hello VM NIC 上或 hello 的優先順序高於 hello 預設規則，允許 LB 探查 （& s） 流量的子網路 （網路安全性群組必須允許的負載平衡器 IP168.63.129.16)。 
* 如果任何這些規則會封鎖 hello 探查流量，移除並重新設定 hello 規則 tooallow hello 探查流量。  
* 測試如果 hello VM 已經開始回應 toohello 健全狀況探查。 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>原因 4：負載平衡器中的其他設定錯誤
如果所有 hello 上述原因看起來 toobe 進行驗證，並正確地解析 hello 後端 VM 仍不會回應 toohello 健全狀況探查，然後以手動方式連線，測試和收集一些追蹤 toounderstand hello 連線。

**驗證和解決方式**

* 使用**Psping**從其中一個 hello 內其他 Vm hello VNet tootest hello 探查連接埠回應 (範例：.\psping.exe-t 10.0.0.4:3389) 並記錄結果。 
* 使用**TCPing**從其中一個 hello 內其他 Vm hello VNet tootest hello 探查連接埠回應 (範例：.\tcping.exe 10.0.0.4 3389) 並記錄結果。 
* 如果這些 ping 測試都沒有收到任何回應，則
    - 同時執行 Netsh 追蹤 hello 目標後端集區 VM 和 hello 從另一項測試 VM 上相同的 VNet。 現在，執行一些時間的 PsPing 測試、 收集某些網路追蹤，然後再停止 hello 測試。 
    - 分析 hello 網路擷取，並查看是否有這兩個內送和外寄的封包相關的 toohello ping 查詢。 
        - 如果觀察不到任何連入封包 hello 後端集區 VM 上，沒有可能的網路安全性群組或 UDR 組態錯誤封鎖 hello 流量。 
        - 如果沒有傳出的封包 hello 後端集區 VM 上觀察到，hello VM 需要 toobe 檢查任何相關的問題 （eample，應用程式封鎖 hello 探查連接埠)。 
    - 請確認 hello 探查封包在到達 hello 負載平衡器之前已強制的 tooanother 目的地 （可能是透過 UDR 設定）。 這可能會造成 hello 流量 toonever 觸達 hello 後端 VM。 
* 變更 hello 探查類型 (例如，HTTP tooTCP) 及設定網路安全性群組 Acl 中的 hello 對應連接埠和防火牆 toovalidate hello 問題是否與探查回應 hello 設定。 如需健康狀態探查組態的詳細資訊，請參閱[端點負載平衡健康狀態探查組態 (英文)](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/)。

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>徵兆： 負載平衡器後方的 Vm 都沒有回應 hello 設定資料連接埠上 tootraffic

如果後端集區的 VM 會列示為狀況良好並回應 toohello 健全狀況探查，但仍未參與 hello 負載平衡，或沒有回應 toohello 資料流量，它可能是因為下列原因 hello 的 tooany: 
* 負載平衡器後端集區的 VM 未 hello 資料連接埠接聽 
* 網路安全性群組封鎖 hello hello 負載平衡器後端集區 VM 上的連接埠  
* 存取 hello 從負載平衡器 hello 相同的 VM 與 NIC 
* 從 hello 參與負載平衡器後端集區 VM 存取 hello 網際網路負載平衡器 VIP 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>原因 1： 負載平衡器後端集區 VM 並未 hello 資料連接埠上接聽 
如果 VM 不會回應 toohello 資料流量，則可能是因為是 hello 目標連接埠上未開啟 hello 參與 VM，或 hello VM 未接聽該通訊埠。 

**驗證和解決方式**

1. 登入 toohello 後端 VM。 
2. 開啟命令提示字元並執行下列命令 toovalidate hello 資料連接埠上接聽應用程式的 hello:  
            netstat -an 
3. 如果未列出 hello 連接埠與狀態 「 接聽 」 設定 hello 適當的接聽程式連接埠 
4. 如果 hello 連接埠標示為接聽，請檢查 hello 目標應用程式，該通訊埠上的任何可能的問題。 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>原因 2： 網路安全性群組封鎖 hello hello 負載平衡器後端集區 VM 上的連接埠  

如果一或多個網路或 hello VM hello 子網路上設定的安全性群組，封鎖 hello 來源 IP 或連接埠，則 hello VM 無法 toorespond。

* 列出 hello 網路安全性群組 hello 後端 VM 上設定。 如需詳細資訊，請參閱：
    -  [管理使用 hello 入口網站的網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [使用 PowerShell 管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* 從網路安全性群組的 hello 清單中，檢查是否：
    - hello hello 資料連接埠上的傳入或傳出流量具有干擾。 
    - **Deny All**網路安全性群組規則上 hello hello VM 或 hello 子網路具有較高的優先順序，讓流量負載平衡器探查，以及該 hello 預設規則的 NIC （網路安全性群組必須允許的負載平衡器 IP168.63.129.16 是探查連接埠) 
* 如果任何 hello 規則會封鎖 hello 流量，移除並重新設定這些規則 tooallow hello 資料流量。  
* 測試如果 hello VM 後立即啟動 toorespond toohello 健全狀態探查。

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>原因 3： 存取從 hello hello 負載平衡器相同的 VM 及網路介面 

如果您在 hello 後端的負載平衡器的 VM 中裝載的應用程式正嘗試 tooaccess 裝載於另一個應用程式 hello 相同的後端 VM hello 透過相同的網路介面，是不支援的案例，並將會失敗。 

**解析**即可解決此問題，透過 hello 下列方法之一：
* 每個應用程式都設定個別的後端集區 VM。 
* 設定雙重 NIC Vm 中的 hello 應用程式，讓每個應用程式使用它自己的網路介面和 IP 位址。 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>原因 4： 從 hello 參與負載平衡器後端集區 VM 存取 hello 內部負載平衡器 VIP

如果 ILB VIP 設定內部 VNet，而且其中一個 hello 參與者後端 Vm 正嘗試 tooaccess hello 內部負載平衡器 VIP，導致失敗。 這是不支援的案例。
**解析**評估應用程式閘道或其他 proxy （例如，nginx 或 haproxy 等） toosupport 這一類的案例。 如需應用程式閘道的詳細資訊，請參閱[應用程式閘道的概觀](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>其他網路擷取
如果您決定 tooopen 支援案例，收集下列資訊以便快速解決 hello。 選擇下列測試單一的後端 VM tooperform hello:
- 使用 Psping 其中一個內 hello VNet tootest hello 探查連接埠回應 hello 後端 Vm (範例： psping 10.0.0.4:3389) 並記錄結果。 
- 使用其中一個內 hello VNet tootest hello 探查連接埠回應 hello 後端 Vm TCPing (範例： psping 10.0.0.4:3389) 並記錄結果。
- 如果不收到任何回應時，在這些 ping 測試，hello 後端 VM 上執行的同時 Netsh trace，當您執行 PsPing，然後再停止 hello Netsh trace hello VNet 測試 VM。 
  
## <a name="next-steps"></a>後續步驟

如果 hello 上述步驟無法解決 hello 問題，請開啟[支援票證](https://azure.microsoft.com/support/options/)。

