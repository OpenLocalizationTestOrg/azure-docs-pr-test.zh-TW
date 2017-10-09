---
title: "aaaTroubleshooting Azure Vm 之間的連線問題 |Microsoft 文件"
description: "了解如何 tooTroubleshoot hello Azure Vm 之間的連線問題。"
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>為 Azure VM 之間的連線問題疑難排解

您可能會遇到 Azure Vm 之間的連線問題。 本文章提供疑難排解步驟 toohelp 解決這個問題。 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>徵狀

Azure VM 無法連線 tooanother Azure VM。

## <a name="troubleshooting-guidance"></a>疑難排解指引 

1. [檢查是否 NIC 設定不正確](#step-1-check-if-nic-is-misconfigured)
2. [檢查是否封鎖的 NSG 或 UDR 網路流量](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [檢查是否 VM 防火牆封鎖網路流量](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [請檢查 VM 應用程式或服務是否正在接聽 hello 連接埠](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [檢查 hello 問題是否因 SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [檢查是否封鎖流量的 Acl hello 傳統 VM](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [檢查是否對建立 hello 端點 hello 傳統 VM](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [無法 tooconnect tooa VM 網路共用](#step-8-unable-to-connect-to-a-vm-network-share)
9. [內部 Vnet 連線](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>疑難排解步驟

請遵循這些步驟 tootroubleshoot hello 問題。 檢查 hello 問題是否解決每個步驟之後。 

### <a name="step-1-check-if-nic-is-misconfigured"></a>步驟 1： 檢查 NIC 設定不正確

請遵循[如何 tooreset Azure Windows VM 的網路介面](../virtual-machines/windows/reset-network-interface.md)。 

如果您修改 hello 網路介面 (NIC) 之後，就會發生 hello 問題，請遵循下列步驟：

**運算 NIC Vm**

1. 新增 NIC。
2. 修正 hello 錯誤 NIC] 或 [移除錯誤 NIC 的 hello 問題  然後出 hello nic。

如需詳細資訊，請參閱[新增網路介面 tooor 移除虛擬機器](virtual-network-network-interface-vm.md)。

**單一 NIC VM** 

- [重新部署 Windows VM](../virtual-machines/windows/redeploy-to-new-node.md)
- [重新部署 Linux VM](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>步驟 2： 檢查是否封鎖的 NSG 或 UDR 網路流量

利用[網路監看員 IP 流量確認](../network-watcher/network-watcher-ip-flow-verify-overview.md)和[NSG 流程記錄](../network-watcher/network-watcher-nsg-flow-logging-overview.md)tooidentify 如果沒有網路安全性群組或使用者定義路由之影響的流量。

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>步驟 3： 檢查是否 VM 防火牆封鎖網路流量

停用 hello 防火牆，然後再測試 hello 結果。 如果 hello 問題已解決，驗證 hello 防火牆中的 hello 設定，然後重新啟用。

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>步驟 4： 檢查 VM 應用程式或服務是否正在接聽 hello 連接埠

您可以使用其中一個 VM 應用程式或服務正在接聽 hello 連接埠是否遵循方法 toocheck hello

- 執行下列命令 toocheck 是否 hello 伺服器正在接聽該通訊埠的 hello。

**Windows VM**

    netstat –ano

**Linux VM**

    netstat -l

- 執行 hello **Telnet** hello VM tooitself tootest hello 連接埠上的命令。 如果 hello 測試失敗，應用程式或服務不是設定的 toolisten hello 連接埠上。

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>步驟 5： 檢查 hello 問題是否因 SNAT

在某些情況下，hello VM 放置後方會相依於 Azure 外部的資源的負載平衡解決方案。 在這些情況下，如果您遇到間歇性連線問題 hello 問題可能因[SNAT 連接埠耗盡](../load-balancer/load-balancer-outbound-connections.md)。 tooresolve hello 問題，建立 hello 負載平衡器後方的 VIP （或傳統的 ILPIP） 是針對每個 vm，並且與 NSG 或 ACL。 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>步驟 6： 檢查是否封鎖流量的 Acl hello 傳統 VM

ACL 提供 hello 能力 tooselectively 允許或拒絕虛擬機器端點的流量。 如需詳細資訊，請參閱[端點上的管理 hello ACL](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>步驟 7： 檢查是否對建立 hello 端點 hello 傳統 VM

您在 Azure 中使用 hello 傳統部署模型中建立的所有 Vm 可以自動透過都通訊與 hello 中其他虛擬機器的私人網路通道相同雲端服務或虛擬網路。 不過，其他虛擬網路上的電腦需要端點 toodirect hello 輸入的網路流量 tooa 虛擬機器。 如需詳細資訊，請參閱[如何設定端點 tooset](../virtual-machines/windows/classic/setup-endpoints.md)。

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>步驟 8： 無法 tooconnect tooa VM 網路共用

如果您無法 tooconnect tooa VM 網路共用，hello 問題可能被因 hello VM 中無法使用 Nic。 toodelete hello Nic 無法使用，請參閱[toodelete hello 無法使用 Nic 的方式](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>步驟 9： 間 Vnet 連線

利用[網路監看員 IP 流量確認](../network-watcher/network-watcher-ip-flow-verify-overview.md)和[NSG 流程記錄](../network-watcher/network-watcher-nsg-flow-logging-overview.md)tooidentify 如果沒有網路安全性群組或使用者定義路由之影響的流量。 您也可以驗證您的內部 Vnet 組態[這裡](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections)。

### <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
