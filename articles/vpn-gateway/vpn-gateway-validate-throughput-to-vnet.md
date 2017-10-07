---
title: "驗證 Microsoft Azure 虛擬網路的 VPN 輸送量 tooa |Microsoft 文件"
description: "hello 本文件的目的是 toohelp 使用者驗證 hello 從其內部部署資源 tooan Azure 虛擬機器的網路輸送量。"
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>如何 toovalidate VPN 輸送量 tooa 虛擬網路

VPN 閘道連線可讓您在 Azure 虛擬網路與您內部部署之間 tooestablish 安全跨單位連線 IT 基礎結構。

本文示範如何將網路輸送量 toovalidate hello 從內部部署資源 tooan Azure 虛擬機器。 本文章也提供疑難排解指引。

>[!NOTE]
>本文旨在 toohelp 診斷和修正常見的問題。 如果您使用下列資訊，hello 無法 toosolve hello 問題[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。
>
>

## <a name="overview"></a>概觀

hello VPN 閘道連線包含下列元件的 hello:

- 內部部署 VPN 裝置 (檢視[已經驗證的 VPN 裝置列表)](vpn-gateway-about-vpn-devices.md#devicetable)。
- 公用網際網路
- Azure VPN 閘道
- Azure 虛擬機器

hello 下列圖表顯示 hello 邏輯在內部部署網路 tooan Azure 的虛擬網路透過 VPN 連線。

![邏輯客戶網路連線 tooMSFT 網路使用 VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>計算 hello 最大預期的輸入/輸出

1.  判斷您應用程式的基準輸送量需求。
2.  判斷您的 Azure VPN 閘道輸送量限制。 如需說明，請參閱 hello 「 彙總輸送量 SKU 和 VPN 類型 」 一節[規劃和設計 VPN 閘道](vpn-gateway-plan-design.md)。
3.  判斷 hello [Azure VM 輸送量指引](../virtual-machines/virtual-machines-windows-sizes.md)VM 大小。
4.  決定您網際網路服務提供者 (ISP) 的頻寬。
5.  計算您預期的輸送量 - 最小頻寬的 (VM、閘道、ISP) * 0.8。

如果您導出的輸送量不符合您的應用程式基本輸送量需求，您需要識別為 hello 瓶頸的 hello 資源 tooincrease hello 頻寬。 tooresize Azure VPN 閘道，請參閱[變更閘道 SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)。 tooresize 虛擬機器，請參閱[VM 調整](../virtual-machines/virtual-machines-windows-resize-vm.md)。 如果您遇到未預期的網際網路頻寬，您可能也想 toocontact ISP。

## <a name="validate-network-throughput-by-using-performance-tools"></a>使用效能工具驗證網路輸送量

由於測試時的 VPN 通道輸送量飽和情況無法呈現準確的結果，因此應在非尖峰時段執行此驗證。

我們會使用這項測試的 hello 工具是 iPerf，這適用於 Windows 和 Linux 上且擁有用戶端和伺服器模式。 它是針對 Windows Vm 有限的 too3 Gbps。

此工具不會執行任何的讀取/寫入作業 toodisk。 它只會產生自我產生一個結束 toohello 其他 TCP 流量。 它會產生基礎測量用戶端和伺服器節點之間的可用的 hello 頻寬的試驗的統計資料。 當測試兩個節點之間，其中一個作為 hello 伺服器以及其他做為用戶端 hello。 完成這項測試之後，我們建議您反轉 hello 角色 tootest 同時上傳和下載兩個節點上的輸送量。

### <a name="download-iperf"></a>下載 iPerf
下載 [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)。 如需詳細資訊，請參閱 [iPerf 文件](https://iperf.fr/iperf-doc.php)。

 >[!NOTE]
 >Microsoft 的獨立公司所製造這篇文章討論的 hello 協力廠商產品。 Microsoft 對於不提供任何瑕疵擔保默示或其他關於這些產品的 hello 效能或可靠性。
 >
 >

### <a name="run-iperf-iperf3exe"></a>執行 iPerf (iperf3.exe)
1. 啟用 NSG/ACL 規則，允許 hello 流量 （適用於測試 Azure VM 上的公用 IP 位址）。

2. 在這兩個節點上，啟用連接埠 5001 的防火牆例外狀況。

    **Windows:**執行 hello 下列命令以系統管理員：

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    tooremove hello 規則測試時已完成，執行下列命令：

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux：**Azure Linux 映像有寬鬆的防火牆。 如果沒有接聽的通訊埠的應用程式，hello 允許流量。 受保護的自訂映像可能需要明確開啟連接埠。 常見的 Linux OS 層防火牆包括 `iptables`、`ufw` 或 `firewalld`。

3. Hello 伺服器節點上，變更 toohello 目錄 iperf3.exe 解壓縮的位置。 然後在伺服器模式下執行 iPerf 然後將它設定 toolisten 連接埠 5001 hello 下列命令：

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Hello 用戶端在節點上，變更 toohello 目錄 iperf 工具會擷取並接著執行下列命令的 hello:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    hello 用戶端 30 秒查 5001 toohello 伺服器連接埠上的流量。 hello 旗標 '-P '，表示我們使用 32 的同時連線 toohello 伺服器節點。

    hello 下列畫面顯示 hello 這個範例輸出：

    ![輸出](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. （選擇性） toopreserve hello 測試結果，請執行下列命令：

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. 完成 hello 上一個步驟之後，執行相同的步驟與 hello 角色反轉，hello，因此 hello 伺服器節點現在會 hello 用戶端，反之亦然。

## <a name="address-slow-file-copy-issues"></a>處理檔案複製變慢的問題
使用 Windows 檔案總管或透過 RDP 工作階段拖放時，您可能會遇到檔案複製變慢的問題。 此問題通常是因為 tooone 或兩個 hello 下列因素：

- 如 Windows 檔案總管與 RDP 的檔案應用程式，並未在複製檔案時使用多執行緒。 以提升效能、 使用多執行緒的檔案複製應用程式如[Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy 檔案使用 16 或 32 的執行緒。 按一下 檔案中的複本 Richcopy，toochange hello 執行緒編號**動作** > **複製選項** > **檔案複製**。<br><br>
![檔案複製變慢的問題](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- VM 磁碟讀取/寫入速度不足。 如需詳細資訊，請參閱 [Azure 儲存體疑難排解](../storage/common/storage-e2e-troubleshooting.md)。

## <a name="on-premises-device-external-facing-interface"></a>內部部署裝置的外部對應介面
如果 hello 內部部署 VPN 裝置的面向網際網路 IP 位址會包含在 hello[區域網路](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway)在 Azure 中的定義，您可能會遇到無法 toobring hello VPN，偶爾中斷連線或效能問題。

## <a name="checking-latency"></a>檢查延遲
如果有任何延遲超過 100 毫秒之間的躍點，請使用 tracert tootrace tooMicrosoft Azure 邊緣裝置 toodetermine。

Hello 與內部網路，從執行*tracert* toohello VIP hello Azure 閘道的 VM。 一旦您只會看到 * 傳回，您知道您已達到 hello Azure 邊緣。 當您看到包含 「 MSN"傳回的 DNS 名稱時，您知道您已達到 hello Microsoft 骨幹。<br><br>
![檢查延遲](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>後續步驟
詳細的資訊或說明，請參閱下列連結查看 hello:

- [最佳化 Azure 虛擬機器的網路輸送量](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
