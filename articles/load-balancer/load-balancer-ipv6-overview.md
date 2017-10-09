---
title: "Azure 負載平衡器的 IPv6 的 aaaOverview |Microsoft 文件"
description: "了解 Azure Load Balancer 和負載平衡 VM 的 IPv6 支援。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a>Azure Load Balancer 的 IPv6 概觀

網際網路面向的負載平衡器可以部署 IPv6 位址。 此外 tooIPv4 連線，這可讓 hello 下列功能：

* 原生端對端 IPv6 連線能力之間公用網際網路用戶端和 Azure 虛擬機器 (Vm) 透過 hello 負載平衡器。
* 原生端對端 IPv6 輸出連線能力 - 在 VM 和公用網際網路上已啟用 IPv6 的用戶端之間。

下列圖片的 hello 說明 hello IPv6 功能的 Azure 負載平衡器。

![配置有 IPv6 的 Azure Load Balancer](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

一旦部署之後，IPv4 或 IPv6 啟用網際網路的用戶端可以與 hello 公用 IPv4 或 IPv6 位址 （或主機名稱） 的 hello Azure 網際網路對向負載平衡器進行通訊。 hello 負載平衡器路由 hello IPv6 封包 toohello 私人 IPv6 位址的 hello Vm 使用網路位址轉譯 (NAT)。 hello IPv6 網際網路用戶端無法直接與 hello hello Vm 的 IPv6 位址通訊。

## <a name="features"></a>特性

透過 Azure Resource Manager部署的原生 IPv6 支援提供︰

1. 負載平衡 IPv6 hello 網際網路上的用戶端的 IPv6 服務
2. 在 VM上提供原生 IPv6 和 IPv4 端點 (「雙重堆疊」)
3. 由輸入和輸出起始的原生 IPv6 連線
4. 支援的通訊協定 - 如 TCP、UDP、HTTP(S) - 提供完整的服務架構

## <a name="benefits"></a>優點

這項功能可讓 hello 下列主要優點：

* 符合政府法規要求新的應用程式可存取的僅限 tooIPv6 用戶端
* 啟用行動裝置版和網際網路的項目 (IOT) 開發人員 toouse 雙重堆疊 (IPv4 + IPv6) 的 Azure 虛擬機器 tooaddress hello 持續成長的行動裝置版和 IOT 市場

## <a name="details-and-limitations"></a>詳細資料和限制

詳細資料

* hello Azure DNS 服務包含 IPV4 和 IPv6 AAAA 名稱記錄，然後會回應 hello 負載平衡器的兩筆記錄。 hello 用戶端選擇使用哪一個位址 （IPv4 或 IPv6） toocommunicate。
* 當 VM 啟動連線 tooa 公用 IPv6 網際網路連線裝置時，hello VM 來源 IPv6 位址會是網路位址轉譯 (NAT) toohello 公用 IPv6 位址的 hello 負載平衡器。
* 執行 hello Linux 作業系統的 Vm 必須已設定的 tooreceive 透過 DHCP IPv6 IP 位址。 許多 hello Azure 組件庫已在 hello Linux 映像設定 toosupport IPv6 而不需修改。 如需詳細資訊，請參閱 [設定 Linux VM 的 DHCPv6](load-balancer-ipv6-for-linux.md)
* 如果您選擇的 toouse 健全狀況探查您的負載平衡器，以建立 IPv4 探查，並使用與 hello IPv4 和 IPv6 端點。 如果您的 VM 上的 hello 服務關閉時，會取用 hello IPv4 和 IPv6 端點退出循環。

限制

* 您無法在 hello Azure 入口網站中新增 IPv6 負載平衡規則。 hello 規則只能建立透過 hello 範本，CLI、 PowerShell。
* 您不可以升級現有的 Vm toouse IPv6 位址。 您必須部署新的 VM。
* 單一的 IPv6 位址可以指派每個 VM 中的 tooa 單一網路介面。
* hello 公用 IPv6 位址不能指派 tooa VM。 它們只可以指派 tooa 負載平衡器。
* 您無法設定 hello 反向 DNS 對應，為公用的 IPv6 位址。
* hello Vm 與 hello IPv6 位址不能是 Azure 雲端服務的成員。 它們可以連接的 tooan Azure 虛擬網路 (VNet) 和移轉的 IPv4 位址與對方進行通訊。
* 私人 IPv6 位址可部署到資源群組中的個別 VM，但無法透過擴充集部署到資源群組。
* Azure Vm 無法透過 IPv6 tooother Vm、 其他 Azure 服務或在內部部署裝置連線。 它們只能透過 IPv6 通訊與 hello Azure 負載平衡器。 不過，它們可以使用 IPv4 與這些其他資源通訊。
* 雙重堆疊 (IPv4 + IPv6) 部署支援 IPv4 的網路安全性群組 (NSG) 保護。 Nsg 不會套用 toohello IPv6 端點。
* 上的 VM 不是的 hello hello IPv6 端點直接公開 toohello 網際網路。 而是擺在負載平衡器後。 只有 hello 負載平衡器規則中指定的 hello 連接埠都可存取透過 IPv6。
* IPv6 是變更 hello IdleTimeout 參數**目前不支援**。 hello 預設值為四分鐘。
* IPv6 是變更 hello loadDistributionMethod 參數**目前不支援**。
* **目前不支援**保留的 IPv6 IP (其中 IPAllocationMethod = 靜態)。

## <a name="next-steps"></a>後續步驟

深入了解如何 toodeploy 負載平衡器使用 IPv6。

* [依區域的 IPv6 可用性](https://go.microsoft.com/fwlink/?linkid=828357)
* [使用範本部署配置有 IPv6 的負載平衡器](load-balancer-ipv6-internet-template.md)
* [使用 Azure PowerShell 部署配置有 IPv6 的負載平衡器](load-balancer-ipv6-internet-ps.md)
* [使用 Azure CLI 部署配置有 IPv6 的負載平衡器](load-balancer-ipv6-internet-cli.md)
