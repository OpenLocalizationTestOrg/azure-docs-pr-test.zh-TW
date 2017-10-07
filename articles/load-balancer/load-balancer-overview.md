---
title: "aaaAzure 負載平衡器概觀 |Microsoft 文件"
description: "Azure 負載平衡器功能、架構和實作的概觀。 了解 hello 負載平衡器的運作方式，利用 hello 雲端中。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Azure 負載平衡器概觀

Azure 負載平衡器提供高可用性和網路效能 tooyour 應用程式。 這是 Layer 4 (TCP、UDP) 負載平衡器，可將連入流量分配到負載平衡集中所定義服務的狀況良好執行個體。

Azure Load Balancer 可以設定為：

* 負載平衡連入網際網路流量 toovirtual 機器。 這個組態稱為 [網際網路面向的負載平衡](load-balancer-internet-overview.md)。
* 平衡虛擬網路中的虛擬機器之間、雲端服務中的虛擬機器之間，或內部部署電腦與跨單位部署虛擬網路中的虛擬機器之間的流量負載。 這個組態稱為 [內部負載平衡](load-balancer-internal-overview.md)。
* 將外部流量 tooa 特定虛擬機器。

Hello 雲端中的所有資源都必須公開的 IP 位址 toobe hello 網際網路從可以連線。 在 Azure 中的 hello 雲端基礎結構會使用其資源的非路由的 IP 位址。 Azure 會使用公用 IP 位址 toocommunicate toohello 網際網路的網路位址轉譯 (NAT)。

## <a name="azure-deployment-models"></a>Azure 部署模型

它是 hello 傳統的 Azure 資源管理員之間的重要 toounderstand hello 差異[部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。 每個模型中設定 Azure Load Balancer 的方式均不同。

### <a name="azure-classic-deployment-model"></a>Azure 傳統部署模型

部署雲端服務界限內的虛擬機器可以是群組的 toouse 負載平衡器。 在此模型的公用 IP 位址和完整網域名稱、 (FQDN) 指派 tooa 雲端服務。 hello 負載平衡器進行連接埠轉譯和負載平衡 hello 網路流量利用 hello 雲端服務的 hello 公用 IP 位址。

負載平衡的流量是由端點所定義。 連接埠轉譯端點具有 hello 公用指派連接埠的 hello 公用 IP 位址和 hello 分派 toohello 服務特定的虛擬機器上的本機連接埠之間的一對一關聯性。 負載平衡端點 hello hello 雲端服務中的虛擬機器上有 hello 公用 IP 位址與 hello 分派的本機連接埠 toohello 服務之間的一對多關聯性。

![Hello 傳統部署模型中的 azure 負載平衡器](./media/load-balancer-overview/asm-lb.png)

圖 1-hello 傳統部署模型中的 Azure 負載平衡器

hello hello 公用 IP 位址，hello 這種部署模型的負載平衡器使用的網域標籤是\<雲端服務名稱\>。.cloudapp.net。 hello 下圖顯示 hello Azure 負載平衡器在此模型中。

### <a name="azure-resource-manager-deployment-model"></a>Azure Resource Manager 部署模型

在 hello Resource Manager 部署模型沒有任何需要 toocreate 雲端服務。 hello 負載平衡器會建立多個虛擬機器之間分配 tooexplicitly 路由傳送流量。

公用 IP 位址是具有網域標籤 (DNS 名稱) 的個別資源。 hello 公用 IP 位址是與 hello 負載平衡器資源相關聯。 負載平衡器規則與輸入的 NAT 規則做為公用 IP 位址 hello hello 網際網路端點會接收負載平衡網路流量的 hello 資源。

私用或公用 IP 位址會指派 toohello 網路介面資源附加 tooa 虛擬機器。 網路介面，加入之後 tooa 負載平衡器後端 IP 位址集區 hello 負載平衡器是可以 toosend 負載平衡網路流量根據 hello 負載平衡規則所建立的。

hello 下圖顯示 hello Azure 負載平衡器在此模型中：

![Resource Manager 中的 Azure Load Balancer](./media/load-balancer-overview/arm-lb.png)

圖 2 - Resource Manager 中的 Azure Load Balancer

hello 負載平衡器可透過資源管理員為基礎的範本、 Api 和工具進行管理。 toolearn 更多有關資源管理員，請參閱 hello[資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。

## <a name="load-balancer-features"></a>負載平衡器功能

* 雜湊型分散

    Azure 負載平衡器會使用雜湊型分散演算法。 根據預設，它會使用來源 IP、 來源連接埠、 目的地 IP、 目的地連接埠和通訊協定類型 toomap 流量 tooavailable 伺服器組成的 5 個 tuple 雜湊。 它只在傳輸工作階段「內」  提供綁定。 在相同的 TCP 或 UDP 工作階段將為的 hello 封包導向的 toohello 相同 hello 負載平衡端點之後的執行個體。 Hello 用戶端關閉並重新開啟 hello 連接或啟動從新的工作階段時 hello 相同的來源 IP，hello 來源連接埠變更。 這可能會造成不同的資料中心 hello 流量 toogo tooa 不同端點。

    如需詳細資訊，請參閱 [分負載平衡器配模式](load-balancer-distribution-mode.md)。 hello 下圖顯示 hello 雜湊為基礎的發佈：

    ![雜湊型分散](./media/load-balancer-overview/load-balancer-distribution.png)

    圖 3 - 雜湊型分配

* 連接埠轉送

    Azure 負載平衡器可供您控制如何管理輸入通訊。 此通訊包括從網際網路主機、其他雲端服務中的虛擬機器，或虛擬網路起始的流量。 此控制項是以端點 (也稱為輸入端點) 表示。

    輸入的端點公用連接埠上接聽，並將流量轉送 tooan 內部連接埠。 您可以對應的內部或外部端點的連接埠相同的 hello 或使用不同的通訊埠。 例如，您可以有 web 伺服器設定 toolisten tooport 81 hello 公用端點對應時通訊埠 80。 建立公用端點 hello 觸發 hello 建立負載平衡器執行個體。

    建立使用 hello Azure 入口網站，hello 入口網站會自動建立端點 toohello 虛擬機器的遠端桌面通訊協定 (RDP) hello 和遠端 Windows PowerShell 工作階段流量。 您可以使用這些端點 tooremotely 透過 hello 網際網路管理 hello 虛擬機器。

* 自動重新設定

    當您相應增加或減少執行個體時，Azure 負載平衡器本身會立即重新設定。 比方說，也會重新設定時不會增加 hello 的雲端服務中的 web/背景工作角色執行個體計數，或當您將其他虛擬機器新增至 hello 相同負載平衡設定。

* 服務監視

    不同的伺服器執行個體時，azure 負載平衡器可以探查 hello hello 健全狀況。 當探查失敗 toorespond 時，hello 負載平衡器會停止傳送新的連線 toohello 狀況不良的執行個體。 現有的連線不受影響。

    支援的探查類型有三種：

    + **（在平台做為服務僅限虛擬機器） 上的客體代理程式探查：** hello 負載平衡器會利用 hello hello 虛擬機器內的客體代理程式。 hello 客體代理程式會接聽並回應 HTTP 200 OK 回應時，才 hello 執行個體處於 hello 就緒狀態 （亦即 hello 執行個體不處於像是忙碌、 回收或停止）。 如果 hello 代理程式無法與 HTTP 200 OK toorespond，hello 負載平衡器標記 hello 為沒有回應的執行個體和停止傳送流量 toothat 執行個體。 hello 負載平衡器會繼續 tooping hello 執行個體。 如果 hello 客體代理程式回應 HTTP 200，hello 負載平衡器就會再次傳送流量 toothat 執行個體。 當您使用 web 角色時，您的網站程式碼通常會執行的 w3wp.exe，不會監視 hello Azure 網狀架構或客體代理程式。 這表示 （例如 HTTP 500 回應） 的 w3wp.exe 中失敗將不會報告的 toohello 客體代理程式，，和 hello 負載平衡器將不會知道 tootake 該執行個體退出循環。
    + **自訂的 HTTP 探查：**此探查會覆寫 hello 預設 （客體代理程式） 探查。 您可以使用它 toocreate hello 角色執行個體您自己的自訂邏輯 toodetermine hello 健全狀況。 hello 負載平衡器會定期探查您的端點 （每隔 15 秒，根據預設）。 如果它的回應通知 TCP 或 HTTP 200 hello 逾時期限 （預設值為 31 秒） 內 hello 執行個體視為 toobe 中旋轉。 這可用於實作您自己的邏輯 tooremove 執行個體從 hello 負載平衡器的循環。 例如，您可以設定 hello 執行個體 tooreturn-200 狀態，如果 hello 執行個體超過 90%的 CPU。 使用 w3wp.exe 的 web 角色，您也會取得自動監視您的網站，因為在網站上的程式碼中的失敗會傳回非 200 狀態 toohello 探查。
    + **TCP 自訂探查：**此探查會依賴成功 TCP 工作階段建立定義 tooa 探查連接埠。

    如需詳細資訊，請參閱 hello [LoadBalancerProbe 結構描述](https://msdn.microsoft.com/library/azure/jj151530.aspx)。

* 來源 NAT

    從您的服務所產生的網際網路進行的所有輸出流量 toohello 來源使用 NAT (SNAT) hello 相同的 VIP 位址，如 hello 連入流量。 SNAT 提供一些重要優勢：

    + 它可讓您輕鬆的升級和災害復原服務，由於 hello 可以動態設定 VIP 對應 tooanother hello 服務執行個體。
    + 它讓存取控制清單 (ACL) 管理變得更容易。 當服務相應增加、相應減少或重新部署時，根據 VIP 表示的 ACL 不會變更。

    hello 負載平衡器組態支援 UDP 完整圓錐 NAT。 完整圓錐 NAT 是一種 NAT 其中 hello 連接埠允許來自任何外部的主機 （以回應 tooan 傳出要求） 的傳入的連接。

    起始虛擬機器每個新輸出連線，也會 hello 負載平衡器所配置的輸出連接埠。 hello 外部主機會看到 IP VIP 配置的虛擬通訊埠的流量。 對於需要大量的輸出連線的案例，建議 toouse[執行個體層級公用 IP](../virtual-network/virtual-networks-instance-level-public-ip.md)位址，讓 hello Vm 的 SNAT 輸出的專用的 IP 位址。 這會減少 hello 的連接埠耗盡的風險。

    如需更多有關本主題的詳細資訊，請參閱[輸出連線](load-balancer-outbound-connections.md)一文。

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>支援虛擬機器有多個負載平衡的 IP 位址
您可以指派多個負載平衡公用 IP 位址 tooa 組的虛擬機器。 運用這項功能，您可以主控多個 SSL 網站及/或 hello 相同設定的虛擬機器上的多個 SQL Server AlwaysOn 可用性群組接聽程式。 如需詳細資訊，請參閱[每一雲端服務有多重 VIP](load-balancer-multivip.md)。

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>限制

負載平衡器後端集區可以包含任何 VM SKU (基本層除外)。

## <a name="next-steps"></a>後續步驟

- 深入了解[網際網路對向負載平衡器](load-balancer-internet-overview.md)

- 深入了解[內部負載平衡器概觀](load-balancer-internal-overview.md)

- 建立[網際網路對向負載平衡器](load-balancer-get-started-internet-portal.md)

- 深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure

