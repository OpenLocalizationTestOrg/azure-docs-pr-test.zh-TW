---
title: "aaaAzure 網路安全性最佳作法 |Microsoft 文件"
description: "了解一些 hello Azure toohelp 中可用的關鍵功能建立安全的網路環境"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Microsoft 雲端服務和網路安全性
Microsoft 雲端服務提供超大規模的服務和基礎結構、企業級的功能，以及許多混合式連線選項。 客戶可以選擇 tooaccess 透過 hello 網際網路或 Azure ExpressRoute，後者提供私人網路連線與這些服務。 hello Microsoft Azure 平台可讓的客戶將他們的基礎結構延伸至雲端 hello tooseamlessly，並建置多層式架構。 另外，協力廠商可以提供安全性服務和虛擬設備，以啟用增強的功能。 當客戶使用透過 ExpressRoute 存取的 Microsoft 雲端服務，這份白皮書提供他們應該考慮的安全性和架構性問題的概觀。 也包括在 Azure 虛擬網路中建立更安全的服務。

## <a name="fast-start"></a>快速開始
hello 下列邏輯圖表可以引導您 tooa 特定範例中的 hello hello Azure 平台提供的許多安全性技術。 提供快速參考找出最符合您案例的 hello 範例。 展開的說明，請繼續閱讀 hello 紙張。
[![0]][0]

[範例 1： 建置周邊網路 （也稱為 DMZ、 非軍事區域或遮蔽式子網路） toohelp 保護應用程式，利用網路安全性群組 (Nsg)。](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[範例 2： 建立周邊網路 toohelp 保護與防火牆以及 Nsg 的應用程式。](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[範例 3： 建立周邊網路 toohelp 保護網路與防火牆、 使用者定義的路由 (UDR)，以及 NSG。](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[範例 4：新增使用站對站、虛擬設備的虛擬私人網路 (VPN) 混合式連接。](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[範例 5：新增使用站對站 Azure VPN 閘道的混合式連接。](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[範例 6：新增使用 ExpressRoute 的混合式連接。](#example-6-add-a-hybrid-connection-with-expressroute)</br>
虛擬網路、 高可用性和服務鏈結之間加入連接的範例會新增 toothis 文件 hello 接下來的幾個月。

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Microsoft 法規遵循與基礎結構保護
toohelp 組織符合國家、 地區和業界的特定需求，可控管 hello 集合與使用個人資料，Microsoft 會提供超過 40 認證與認證。 hello 最完整設定的任何雲端服務提供者。

如需詳細資訊，請參閱 < hello 相容性資訊在 hello [Microsoft 信任中心][TrustCenter]。

Microsoft 有一套方法 tooprotect 雲端基礎結構所需 toorun 超小數位數全域服務。 Microsoft 雲端基礎結構包含硬體、 軟體、 網路和系統管理和作業人員此外 toohello 實體資料中心。

![2]

此方法提供在 hello Microsoft 雲端服務的客戶 toodeploy 為更安全的基礎。 hello 下一個步驟是客戶 toodesign，並建立安全性架構 tooprotect 這些服務。

## <a name="traditional-security-architectures-and-perimeter-networks"></a>傳統的安全性架構和周邊網路
雖然 Microsoft invests 大量保護 hello 雲端基礎結構，客戶也必須保護其雲端服務和資源群組。 多層次的方法 toosecurity 提供 hello 最佳防禦。 周邊網路安全區可防止不受信任的網路存取內部網路資源。 周邊網路是指 toohello 邊緣或坐 hello 網際網路與受保護的 hello 企業 IT 基礎結構之間的 hello 網路組件。

在一般企業網路中，hello 核心基礎結構磐石在 hello 周邊，具有多個圖層的安全性裝置。 每個圖層的 hello 界限是由裝置和原則強制點所組成。 每個圖層可以包含下列網路安全性裝置 hello 的組合： 防火牆、 防止阻絕服務 (DoS)、 入侵偵測或保護系統 (識別碼/IP) 和 VPN 裝置。 強制執行原則可採用防火牆原則、 存取控制清單 (Acl)，或特定路由的 hello 的形式。 hello 第一道防線在 hello 網路中，直接接受來自網際網路，hello 連入流量是同時進入 hello 網路允許進一步合法要求這些機制 tooblock 攻擊和有害流量的組合。 此流量會路由傳送直接 tooresources hello 周邊網路中。 該資源可能然後 「 交談 」 在 hello 網路中，傳送 hello 接下來的界限進行驗證，更深入的 tooresources 第一次。 hello 最外層稱為 hello 周邊網路，因為這個 hello 網路的一部分是公開的 toohello 網際網路，通常會有某種形式的兩端上的保護。 hello 下圖顯示單一子網路周邊網路的範例在公司網路中，具有兩個安全性界限。

![3]

有許多架構使用 tooimplement 周邊網路。 這些架構可以使用各種機制，在每個界限 tooblock 流量的範圍從簡單的負載平衡器 tooa 多個子網路周邊網路，並保護 hello hello 公司網路的更深的階層。 建置 hello 周邊網路的方式取決於 hello hello 組織和其整體風險承受度的特定需求。

當客戶移動其工作負載 toopublic 雲端時，它是關鍵 toosupport 類似的功能，在 Azure toomeet 相容性和安全性需求的周邊網路架構。 本文提供客戶如何在 Azure 中組建安全網路環境方法的指導方針。 它著重在 hello 周邊網路，但也包含網路安全性的各個層面的完整討論。 下列問題的 hello 通知本討論內容：

* 如何組建 Azure 的周邊網路？
* 有哪些 hello Azure 功能可用 toobuild hello 周邊網路？
* 如何保護後端工作負載？
* 在 Azure 中的網際網路通訊控制 toohello 工作負載的方式？
* Hello 在內部部署網路，要如何保護從在 Azure 中部署？
* 何時該使用原生 Azure 安全性功能？何時又該使用協力廠商設備或服務？

hello 下列圖表顯示安全性，Azure 提供 toocustomers 的各種層的級。 這些圖層都是原生 hello Azure 平台本身中的，而且客戶定義的功能：

![4]

輸入從 hello 網際網路，Azure DDoS 有助於保護對 Azure 大規模的攻擊。 hello 下一層是客戶定義的公用 IP 位址 （端點），也就是使用的 toodetermine 哪些流量可以通過 hello 雲端服務 toohello 虛擬網路。 原生 Azure 虛擬網路隔離可確保與其他所有網路完全隔離，而且流量只能流經使用者設定的路徑和方法。 這些路徑和方法的 hello 下一層，Nsg、 UDR 和網路的虛擬應用裝置可以是使用的 toocreate 安全性界限 tooprotect hello 應用程式部署在受保護的 hello 網路中。

hello 下一節提供 Azure 虛擬網路的概觀。 這些虛擬網路由客戶建立，也是部署的工作負載所連接的目的地。 虛擬網路是 hello 為基礎的所有 hello 網路安全性功能需要 tooestablish 周邊網路 tooprotect 客戶部署在 Azure 中。

## <a name="overview-of-azure-virtual-networks"></a>Azure 虛擬網路的概觀
網際網路流量 toohello Azure 虛擬網路，才能進行有兩個圖層的安全性繼承 toohello Azure 平台：

1.    **DDoS 保護**: DDoS 保護是 hello Azure 大規模以網際網路為基礎的攻擊會防止 hello Azure 平台本身的實體網路的圖層。 這些攻擊會使用多個 「 bot 」 節點中嘗試 toooverwhelm 網際網路服務。 Azure 有一層很強大的 DDoS 保護網可篩選所有輸入、輸出及跨 Azure 區域的連線。 DDoS 保護層，這個沒有任何使用者可設定屬性，並不是可存取 toohello 客戶。 hello DDoS 保護層，以保護 Azure 做為平台，從大規模的攻擊時，它也會監視傳出的流量和跨 Azure 區域的流量。 使用網路虛擬裝置 hello VNet 上，可以 hello 客戶針對較小的標尺攻擊，不會中斷 hello 平台層級的保護設定額外恢復功能層級。 舉例來說，DDoS 動作;如果網際網路對向的 IP 位址遭到攻擊大規模 DDoS 攻擊，Azure 會偵測 hello 攻擊的 hello 來源，並刪除 hello 違規流量之前它已達到所要的目的地。 在大多數情況下，hello 容易受到攻擊的端點不會受到 hello 攻擊。 在端點，會受到影響 hello 罕見情況下，沒有流量會是受影響的 tooother 的端點只有遭受攻擊的 hello 端點。 因此，其他客戶和服務也不會看到此攻擊所造成的影響。 Azure DDoS 只會查看大規模攻擊的重大 toonote 它。 很可能超出 hello 平台層級的保護臨界值之前，可能爆您特定的服務。 例如，單一 A0 IIS 伺服器上的網站，在 Azure 平台層級 DDoS 保護註冊威脅之前，可能被 DDoS 攻擊而離線。

2.  **公用 IP 位址**： 公用 IP 位址 （透過服務端點、 公用 IP 位址、 應用程式閘道，以及其他 Azure 功能，都沒有公用 IP 位址 toohello 網際網路路由傳送 tooyour 資源已啟用） 讓雲端服務或資源群組 toohave 公用網際網路 IP 位址和公開的連接埠。 hello 端點會使用網路位址轉譯 (NAT) tooroute 流量 toohello 內部位址和連接埠上 hello Azure 虛擬網路。 這個路徑是在 hello 的虛擬網路的外部流量 toopass hello 主要方式。 hello 公用 IP 位址是可設定 toodetermine 傳入的流量，及如何及在何處轉譯 toohello 虛擬網路上。

當流量達到 hello 虛擬網路時，有許多功能，可開始執行。 Azure 虛擬網路是 hello 客戶 tooattach 的基礎，其工作負載和其中適用於基本的網路層級安全性。 它位於私人網路 （虛擬網路的重疊） Azure hello 的客戶下列功能和特性：

* **流量隔離**： 虛擬網路是 hello Azure 平台上的 hello 流量隔離界限。 一個虛擬網路中的虛擬機器 (Vm) 無法通訊，直接在不同虛擬網路中，即使這兩個虛擬網路建立的 tooVMs hello 同一位客戶。 隔離是很重要的屬性，可確保客戶 VM 和通訊仍然隱蔽於虛擬網路內。

>[!NOTE]
>流量隔離是指只 tootraffic*輸入*toohello 虛擬網路。 透過預設輸出流量的 hello VNet toohello 從網際網路允許，但如果有需要請 Nsg 可以避免。
>
>

* **多層式拓撲**： 虛擬網路可讓客戶 toodefine 多層式拓撲藉由配置子網路，並指定不同的項目或 「 層 」 其工作負載的不同的位址空間。 這些邏輯群組拓撲啟用客戶 toodefine 不同的存取原則，根據 hello 工作負載類型，而且也可以控制 hello 各層之間的流量。
* **跨單位連線**：客戶可以在虛擬網路和多個內部部署網站或 Azure 中的其他虛擬網路之間，建立跨單位連線。 tooconstruct 連接，客戶可以使用對等互連的 VNet，Azure VPN 閘道、 協力廠商的網路虛擬應用裝置或 ExpressRoute。 Azure 支援使用標準 IPsec/IKE 通訊協定和 ExpressRoute 私人連線能力的站對站 (S2S) VPN。
* **NSG**可讓客戶 toocreate 規則 (Acl)，在 hello 預期的資料粒度的層級： 網路介面，個別的 Vm 或虛擬子網路。 客戶可以藉由允許或拒絕虛擬網路，客戶透過跨單位連線的網路上的系統中的 hello 工作負載之間的通訊會控制存取，或直接網際網路通訊。
* **UDR**和**IP 轉送**讓客戶虛擬網路內的不同層之間 toodefine hello 通訊路徑。 客戶可以部署防火牆、IDS/IPS 和其他虛擬設備，並透過這些安全性設備來路由傳送網路流量，以強制執行安全性界限原則、稽核和檢查。
* **網路虛擬裝置**hello Azure Marketplace 中： 例如防火牆、 負載平衡器、 和識別碼/IP 的安全性設備 hello Azure Marketplace 中可用以及 hello VM 映像庫。 客戶可以部署到他們的虛擬網路，並明確地說，在其安全性界限 （包括 hello 周邊網路子網路） toocomplete 多層保護網路的環境，這些應用裝置。

使用這些功能和能力，周邊網路架構可以如何建構在 Azure 中的其中一個範例會為下列圖表 hello:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>周邊網路特性和需求
hello 前端 hello 網路直接相互關連來自 hello 網際網路通訊的 hello 周邊網路。 hello 連入封包應該流經 hello 安全性應用裝置，例如 hello 防火牆、 識別碼和 IP 時，才會到達 hello 後端伺服器。 網際網路繫結的封包從 hello 工作負載也能通過 hello 的安全性設備卻 hello 周邊網路中強制執行原則、 檢查，和稽核時，才退出 hello 網路。 此外，hello 周邊網路中可以裝載的客戶虛擬網路與內部部署網路之間的跨單位 VPN 閘道。

### <a name="perimeter-network-characteristics"></a>周邊網路特性
參考 hello 上圖中，某些 hello 良好的周邊網路特性如下：

* 網際網路對向︰
  * hello 周邊網路的子網路本身為網際網路對向，直接與 hello 網際網路通訊。
  * 公用 IP 位址、 Vip，及/或服務端點傳遞網際網路流量 toohello 前端網路和裝置。
  * 輸入從 hello 網際網路通過之前其他資源的安全性裝置 hello 前端網路的流量。
  * 如果已啟用連出安全性，流量通過安全性裝置 hello 最後一個步驟之前傳遞 toohello 網際網路。
* 受保護的網路︰
  * 沒有直接路徑從 hello 網際網路 toohello 核心基礎結構。
  * 通道 toohello 核心基礎結構必須周遊安全性裝置，例如 Nsg、 防火牆或 VPN 裝置。
  * 其他裝置必須橋網際網路和 hello 核心基礎結構。
  * 兩者的安全性裝置 hello 網際網路對向並 hello 受保護的網路對向的 hello 周邊網路 （例如，hello 兩個防火牆圖示 hello 上圖所示） 界限實際上可能是單一的虛擬設備已區分的規則或每個界限的介面。 例如，一個實體裝置，以邏輯方式分隔，處理這兩個界限的 hello 周邊網路的 hello 負載。
* 其他常見的做法和條件約束：
  * 工作負載不得儲存商務關鍵資訊。
  * 存取和更新 tooperimeter 網路組態和部署是有限的 tooonly 授權管理員。

### <a name="perimeter-network-requirements"></a>周邊網路需求
tooenable 這些特性，在虛擬網路需求 tooimplement 成功周邊網路上遵循下列指導方針：

* **子網路架構：**指定 hello 虛擬網路的整個子網路專門為 hello 周邊網路，分開 hello 中的其他子網路相同虛擬網路。 這項分隔可確保 hello hello 周邊網路與其他內部或私人子網路層流經防火牆或識別碼/IP 虛擬應用裝置之間的流量。  子網路是 hello 界限上的使用者定義的路由需要 tooforward 此流量 toohello 虛擬應用裝置。
* **NSG:** hello 周邊網路的子網路本身應該開啟 tooallow 通訊以 hello 網際網路，但這不表示客戶應該略過 Nsg。 請遵循下列一般安全性作法 toominimize hello 網路介面公開 toohello 網際網路。 鎖定 hello 允許 tooaccess hello 部署或 hello 特定應用程式通訊協定和連接埠已開啟的遠端位址範圍。 但可能在某些情況下，完全鎖定不一定行得通。 例如，如果客戶在 Azure 中設有外部網站，hello 周邊網路應該允許來自任何公用 IP 位址，hello 內送網站要求但只應該開啟 hello web 應用程式連接埠： TCP 連接埠 80 和 （或) 上的 tcp 連接埠 443。
* **路由表：** hello 周邊網路的子網路本身應該能夠 toocommunicate toohello 網際網路直接，但應該不允許從 hello 後端或在內部部署網路的直接通訊 tooand 而不需要透過防火牆或安全性應用裝置。
* **安全性應用裝置組態：** tooroute 和檢查 hello 周邊網路與 hello rest 的受保護的 hello 網路之間的封包、 hello 安全性應用裝置，例如防火牆、 ID 及 IP 裝置，可能是多重主目錄。 它們可能會有不同的 Nic hello 周邊網路和 hello 後端子網路。 hello 周邊網路中的 hello Nic 直接通訊 tooand 從 hello 網際網路，以 hello 對應 Nsg hello 周邊網路及路由表。 Nsg 與 hello 對應後端子網路的路由表，hello Nic 連線 toohello 後端子網路有更多限制。
* **安全性應用裝置功能：**通常 hello 周邊網路中部署的 hello 的安全性設備卻會執行下列功能的 hello:
  * 防火牆： 強制防火牆規則或 hello 連入要求的存取控制原則。
  * 威脅偵測與預防： 偵測及緩和 hello 網際網路的惡意攻擊。
  * 稽核和記錄：維護詳細記錄供稽核和分析。
  * 反向 proxy： 重新導向 hello 連入要求 toohello 相對應的後端伺服器。 此重新導向包含對應，以及轉譯 hello 目的地位址 hello 前端在裝置上，通常防火牆，toohello 後端伺服器位址。
  * 轉送 proxy： 提供 NAT 並執行從起始內 hello 虛擬網路 toohello 網際網路通訊的稽核。
  * 路由器： 轉送 hello 虛擬網路內的內送和跨子網路流量。
  * VPN 裝置： 做為 hello 跨單位 VPN 閘道的跨單位客戶的內部網路和 Azure 虛擬網路之間的 VPN 連線。
  * VPN 伺服器： 接受 tooAzure 虛擬網路連接的 VPN 用戶端。

> [!TIP]
> 將下列兩個群組個別的 hello: hello 個人授權 tooaccess hello 周邊網路安全性齒輪和 hello 誰有權為應用程式的開發、 部署或作業的系統管理員。 將這些群組隔開可區分權責，防止單一個人略過應用程式安全性和網路安全性控制。
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>當建置網路界限時，要求的問題 toobe
在本節中，除非特別說明，hello 詞彙 「 網路 」 是指 tooprivate Azure 訂用帳戶系統管理員所建立的虛擬網路。 hello 詞彙並不會參照 toohello 基礎實體的網路在 Azure 中。

此外，Azure 虛擬網路通常是使用的 tooextend 傳統內部部署網路。 它是可能 tooincorporate 站對站或 ExpressRoute 混合式網路功能與周邊網路架構的解決方案。 此混合連結在組建網路安全性界限時，是很重要的考量。

hello 下列三種問題時重要 tooanswer 您正在建立的網路與周邊網路與多個安全性界限。

#### <a name="1-how-many-boundaries-are-needed"></a>1) 需要多少界限？
hello 第一個決策點是在特定的案例需要多少的安全性界限 toodecide:

* 單一界限： hello 虛擬網路與 hello 網際網路之間的 hello 前端周邊網路上的其中一個。
* 兩個界限： 一個 hello hello 周邊網路，網際網路端上，另一個 hello 周邊網路子網路與 hello 後端中的子網路之間 hello Azure 虛擬網路。
* 三個界限： hello 網際網路端 hello 周邊網路上的一個，一個 hello 周邊網路與後端的子網路之間，hello 後端子網路與 hello 在內部部署網路之間的另一個。
* N 個界限︰可變的數字。 根據安全性需求，沒有任何 toohello 數目限制的安全性界限，可以套用在指定的網路。

hello 界限改變所需的數目和類型根據公司的風險容忍度及 hello 特定案例實作。 這通常是組織內的多個團隊共同達成的決策，通常包括風險和合規性小組、網路和平台小組及應用程式開發小組。 了解的安全性、 hello 資料，以及正在使用的 hello 技術人員應具有說中每個實作此決策 tooensure hello 適當的安全性方針。

> [!TIP]
> 使用 hello 最小數目滿足 hello 安全性需求的特定情況下的界限。 與多個界限，操作和疑難排解可以很困難，以及一段時間 hello 管理負荷與管理 hello 界限的多個原則。 不過，沒有足夠的界限會增加風險。 尋找 hello 平衡相當重要。
>
>

![6]

hello 上圖中顯示三個安全性界限網路的高層級檢視。 hello 界限是 hello 周邊網路與 hello 網際網路、 hello Azure 前端和後端私人子網路和 hello Azure 後端子和 hello 在內部部署公司網路之間。

#### <a name="2-where-are-hello-boundaries-located"></a>2） hello 界限位於何處？
一旦 hello 界限數目會決定，其中這些的 tooimplement hello 下一個決策點。 通常有三個選項︰

* 使用網際網路型的中繼服務 (例如，雲端 Web 應用程式防火牆，本文中不討論)
* 在 Azure 中使用原生功能及/或網路虛擬設備
* Hello 與內部網路上使用實體裝置

純粹 Azure 網路上，hello 選項的原生 Azure 功能 （例如，Azure 負載平衡器），或從網路虛擬裝置 hello 豐富的合作夥伴生態系統的 Azure （例如，檢查點防火牆）。

如果需要 Azure 與內部部署網路之間的界限，則 hello 安全性裝置可位於任一邊的 hello 連線 （或兩側）。 因此必須決定 hello 位置 tooplace 安全性設備上。

在 hello 上圖中，hello 網際網路到周邊網路 hello 前至後端界限完全包含在 Azure 中，並必須是原生的 Azure 功能或網路虛擬裝置。 安全性裝置 hello Azure （後端子網路） 之間的界限和 hello Azure 端上或 hello 內部端或甚至裝置兩端的組合，可能是 hello 公司網路。 可以是重要的優點和缺點 tooeither 選項必須慎重考慮。

比方說，使用現有的實體安全性設備在 hello 內部網路端必須所需之任何新的裝備 hello 優點。 它只需要重新設定。 然而，hello 缺點是，所有流量都必須都來自回 Azure toohello 在內部部署網路 toobe 看到 hello 安全性齒輪。 因此 Azure-Azure 流量可能會造成顯著的延遲，和會影響應用程式效能和使用者經驗，如果它已強制回復 toohello 在內部部署網路上強制執行安全性原則。

#### <a name="3-how-are-hello-boundaries-implemented"></a>3） 如何實作 hello 界限？
每個安全性界限可能會有不同的功能需求 （例如，識別碼和 hello hello 周邊網路，但只有 Acl hello 周邊網路與後端子網路之間的網際網路一端上的防火牆規則）。 決定哪一種裝置 （或有多少裝置） 取決於 toouse hello 案例和安全性需求。 Hello 下列區段，在範例 1、 2 和 3 會討論一些可用的選項。 檢閱 hello Azure 的原生網路功能和從 hello 合作夥伴生態系統可用在 Azure 中的 hello 裝置顯示 hello 無數選項可用 toosolve 幾乎任何案例。

另一個重要實作決策點是如何 tooconnect hello 內部部署與 Azure 網路。 您應該使用 hello Azure 的虛擬閘道或網路的虛擬應用裝置？ Hello 下列區段 （範例 4、 5 和 6） 中更詳細討論這些選項。

您可能也需要 Azure 虛擬網路之間的流量。 Hello 未來將會加入這些案例。

一旦您知道 hello 答案 toohello 上述問題，hello[快速啟動](#fast-start)> 一節可協助您識別哪些範例包括最適合特定案例。

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>範例：使用 Azure 虛擬網路組建安全性界限
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>範例 1 組建周邊網路 toohelp 保護應用程式與 Nsg
[備份 tooFast 開始](#fast-start) | [Detailed 建置此範例中的指示][Example1]

[![7]][7]

#### <a name="environment-description"></a>環境描述
在此範例中，沒有訂用帳戶包含下列資源的 hello:

- 單一資源群組
- 含 “FrontEnd” 和 “BackEnd” 兩個子網路的虛擬網路
- 已套用的 tooboth 子網路的網路安全性群組
- 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
- 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
- 一個代表 DNS 伺服器的 Windows Server ("DNS01")
- Hello 應用程式 web 伺服器相關聯的公用 IP

如需指令碼和 Azure 資源管理員範本，請參閱 hello[詳細組建指示][Example1]。

#### <a name="nsg-description"></a>NSG 描述
此範例會組建 NSG 群組，然後載入六個規則。

> [!TIP]
> 一般而言，您應該建立特定的 「 允許 」 規則首先，後面接著 hello 一般 「 拒絕 」 規則。 hello 的優先順序會規定哪些規則會先評估。 一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。 NSG 規則可以套用在 hello 輸入或輸出方向 （從 hello 觀點 hello 子網路）。
>
>

以宣告方式，下列規則的 hello 正在建置輸入流量：

1. 允許內部 DNS 流量 (連接埠 53)。
2. 允許從 hello 網際網路 tooany 虛擬機器的 RDP 流量 （連接埠 3389）。
3. 允許從 hello 網際網路 tooweb 伺服器 (IIS01) 的 HTTP 流量 （連接埠 80）。
4. 允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）。
5. 拒絕從 hello 網際網路 toohello 整個虛擬網路 （這兩個子網路） 的任何流量 （所有連接埠）。
6. 拒絕 hello 前端的子網路 toohello 後端子網路的任何流量 （所有連接埠）。

與這些規則繫結的 tooeach 子網路中，輸入 hello Internet toohello 網頁伺服器從 HTTP 要求是否兩者的規則 3 （允許） 及 5 （拒絕） 將會套用。 但因規則 3 具有較高的優先順序，所以只會套用規則 3，規則 5 不起作用。 因此 hello HTTP 要求會允許 toohello web 伺服器。 如果該相同流量已嘗試 tooreach hello DNS01 伺服器，規則 5 （拒絕） 是 hello 第一個 tooapply，和 hello 流量就不會允許 toopass toohello 伺服器。 規則 6 （拒絕） 區塊 hello 前端子網路與對話 toohello 後端子 （除了規則 1 和 4 中允許的流量）。 如果攻擊者危害 hello hello 前端上的 web 應用程式，此規則集可保護 hello 後端網路。 hello 攻擊者會受限於 toohello 後端 「 受保護的 「 網路存取 (只 tooresources 公開 hello AppVM01 伺服器上)。

沒有預設的輸出規則，允許出 toohello 網際網路的流量。 在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。 關閉兩個方向的流量 toolock，使用者定義路由是必要 （請參閱範例 3）。

#### <a name="conclusion"></a>結論
這個範例是相當簡單且直接的方式，隔離 hello 後端的輸入流量子網路。 如需詳細資訊，請參閱 hello[詳細組建指示][Example1]。 這些指示包括：

* 如何 toobuild 此周邊網路與傳統的 PowerShell 指令碼。
* 如何 toobuild 此周邊網路與 Azure Resource Manager 範本。
* 每個 NSG 命令的詳細描述。
* 詳細的流量流程案例，顯示每一層允許或拒絕流量的方式。


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>範例 2 組建周邊網路 toohelp 保護應用程式與防火牆以及 Nsg
[備份 tooFast 開始](#fast-start) | [Detailed 建置此範例中的指示][Example2]

[![8]][8]

#### <a name="environment-description"></a>環境描述
在此範例中，沒有訂用帳戶包含下列資源的 hello:

* 單一資源群組
* 含 “FrontEnd” 和 “BackEnd” 兩個子網路的虛擬網路
* 已套用的 tooboth 子網路的網路安全性群組
* 網路的虛擬設備，在這個案例中為防火牆、 連接 toohello 前端子網路
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")

如需指令碼和 Azure 資源管理員範本，請參閱 hello[詳細組建指示][Example2]。

#### <a name="nsg-description"></a>NSG 描述
此範例會組建 NSG 群組，然後載入六個規則。

> [!TIP]
> 一般而言，您應該建立特定的 「 允許 」 規則首先，後面接著 hello 一般 「 拒絕 」 規則。 hello 的優先順序會規定哪些規則會先評估。 一旦流量找到 tooapply tooa 特定規則，則會不評估任何進一步的規則。 NSG 規則可以套用在 hello 輸入或輸出方向 （從 hello 觀點 hello 子網路）。
>
>

以宣告方式，下列規則的 hello 正在建置輸入流量：

1. 允許內部 DNS 流量 (連接埠 53)。
2. 允許從 hello 網際網路 tooany 虛擬機器的 RDP 流量 （連接埠 3389）。
3. 允許任何網際網路流量 （所有連接埠） toohello 網路的虛擬設備 （防火牆）。
4. 允許從 IIS01 tooAppVM1 任何流量 （所有連接埠）。
5. 拒絕從 hello 網際網路 toohello 整個虛擬網路 （這兩個子網路） 的任何流量 （所有連接埠）。
6. 拒絕 hello 前端的子網路 toohello 後端子網路的任何流量 （所有連接埠）。

與這些規則繫結的 tooeach 子網路中，如果 HTTP 要求已從 hello 網際網路 toohello 防火牆，兩者的規則 3 （允許） 及 5 （拒絕） 將會套用。 但因規則 3 具有較高的優先順序，所以只會套用規則 3，規則 5 不起作用。 因此 hello HTTP 要求會允許 toohello 防火牆。 如果嘗試 tooreach hello IIS01 伺服器，該相同的流量，即使它是 hello 前端子網路上，規則 5 （拒絕） 將會套用，和 hello 流量就不會允許 toopass toohello 伺服器。 規則 6 （拒絕） 區塊 hello 前端子網路與對話 toohello 後端子 （除了規則 1 和 4 中允許的流量）。 如果攻擊者危害 hello hello 前端上的 web 應用程式，此規則集可保護 hello 後端網路。 hello 攻擊者會受限於 toohello 後端 「 受保護的 「 網路存取 (只 tooresources 公開 hello AppVM01 伺服器上)。

沒有預設的輸出規則，允許出 toohello 網際網路的流量。 在此範例中，我們會允許輸出流量，並不會修改任何輸出規則。 關閉兩個方向的流量 toolock，使用者定義路由是必要 （請參閱範例 3）。

#### <a name="firewall-rule-description"></a>防火牆規則描述
Hello 防火牆上應該建立轉送規則。 由於這個範例只有路由網際網路流量中繫結 toohello 防火牆，然後 toohello web 伺服器上，只有一個轉送網路位址轉譯 (NAT)，因此也需要規則。

hello 轉送規則會接受任何輸入的來源位址，叫用 hello 防火牆嘗試 tooreach HTTP （連接埠 80 或 443 用於 HTTPS）。 它送出 hello 防火牆的本機介面並重新導向 toohello web 伺服器上的使用 hello 10.0.1.5 IP 位址。

#### <a name="conclusion"></a>結論
這個範例是相當簡單的方式保護您的應用程式的防火牆與隔離 hello 後端的輸入流量子網路。 如需詳細資訊，請參閱 hello[詳細組建指示][Example2]。 這些指示包括：

* 如何 toobuild 此周邊網路與傳統的 PowerShell 指令碼。
* 如何 toobuild 此範例使用 Azure Resource Manager 範本。
* 每個 NSG 命令和防火牆規則的詳細描述。
* 詳細的流量流程案例，顯示每一層允許或拒絕流量的方式。

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>範例 3 建置周邊網路 toohelp 保護網路與防火牆、 UDR 和 NSG
[備份 tooFast 開始](#fast-start) | [Detailed 建置此範例中的指示][Example3]

[![9]][9]

#### <a name="environment-description"></a>環境描述
在此範例中，沒有訂用帳戶包含下列資源的 hello:

* 單一資源群組
* 一個虛擬網路，包含三個子網路：“SecNet”、“FrontEnd”、“BackEnd”
* 網路的虛擬設備，在這個案例中為防火牆、 連接 toohello SecNet 子網路
* 一個代表應用程式 Web 伺服器的 Windows Server (“IIS01”)
* 兩個代表應用程式後端伺服器的 Windows Server (“AppVM01”、“AppVM02”)
* 一個代表 DNS 伺服器的 Windows Server ("DNS01")

如需指令碼和 Azure 資源管理員範本，請參閱 hello[詳細組建指示][Example3]。

#### <a name="udr-description"></a>UDR 描述
根據預設，下列系統路由 hello 的定義如下：

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

hello VNETLocal 永遠是構成該特定網路的 hello 虛擬網路的一或多個定義的位址首碼 （也就是說，它會變更虛擬網路 toovirtual 網路之外，根據每個特定的虛擬網路的定義方式）。 hello 剩餘的系統路由是靜態的而且預設 hello 資料表中所示。

在此範例中，兩個路由會建立資料表，各一個 hello 前端和後端子網路。 每個資料表會載入適當的 hello 指定子網路的靜態路由。 在此範例中，每一個資料表具有三個路由 (0.0.0.0/0) 的所有流量都導向透過 hello 防火牆 (下個躍點 = 虛擬應用裝置的 IP 位址):

1. 本機子網路流量沒有下一個躍點定義 tooallow 本機子網路流量 toobypass hello 防火牆。
2. 下一個躍點定義為防火牆的虛擬網路。 這個下一個躍點會覆寫，可讓本機虛擬網路流量 tooroute 直接 hello 預設規則。
3. 所有其他流量 (0/0)，與下個躍點定義為 hello 防火牆。

> [!TIP]
> Hello UDR 符號本機子網路的通訊沒有 hello 本機子網路項目。
>
> * 在本例中，指向 tooVNETLocal 10.0.1.0/24 相當重要 ！ 未安裝，離開 hello 目的地 Web 伺服器 (10.0.1.4) tooanother 本機伺服器 （例如） 10.0.1.25 封包都會失敗，因為它們會傳送 toohello NVA。 hello NVA 會將它傳送 toohello 子網路，並 hello 子網路將會重新傳送 toohello NVA 無限迴圈。
> * 路由迴圈的 hello 機會是通常具有連線的 tooseparate 子網路子網路，這通常是傳統的內部部署裝置的多個 Nic 的設備上更高版本。
>
>

一旦建立 hello 路由表，它們必須是繫結的 tootheir 子網路。 hello 前端的子網路路由表，一旦建立和繫結 toohello 子網路，此輸出會如下：

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR 現在可以套用的 toohello 閘道子網路連接的 hello ExpressRoute 電路。
>
> 範例 3 和 4 中顯示的方式 tooenable 您周邊網路與 ExpressRoute 或站對站網路功能的範例。
>
>

#### <a name="ip-forwarding-description"></a>IP 轉送描述
IP 轉送 」 是附屬功能 tooUDR。 IP 轉送 」 是設定為，允許它 tooreceive 未特別定址流量 toohello 應用裝置，並將該流量 tooits 最終目的端的虛擬應用裝置上。

例如，如果 AppVM01 使得要求 toohello DNS01 伺服器，UDR 會路由傳送此流量 toohello 防火牆。 IP 轉送已啟用，hello DNS01 目的地 (10.0.2.4) 的 hello 流量是接受 hello 應用裝置 (10.0.0.4) 與轉送 tooits 最終目的端 (10.0.2.4)。 不含 IP 轉送 hello 防火牆上啟用，流量就不會接受 hello 應用裝置即使 hello 路由表有 hello 防火牆為 hello 下一個躍點。 toouse 虛擬應用裝置，它是關鍵 tooremember tooenable IP 轉送以及 UDR。

#### <a name="nsg-description"></a>NSG 描述
本例會組建 NSG 群組，然後在其中載入單一規則。 此群組，就只有 toohello 前端和後端的子網路 (不 hello SecNet) 繫結。 以宣告方式建立 hello 下列規則：

* 拒絕從 hello 網際網路 toohello 整個虛擬網路 （所有的子網路） 的任何流量 （所有連接埠）。

雖然本例中使用 NSG，但它的主要目的是作為防止人為設定錯誤的第二道防線。 hello 的目標是 tooblock 從所有傳入的流量 hello 網際網路 tooeither hello 前端或後端的子網路。 應該只有流量通過 hello SecNet 子網路 toohello 防火牆 (然後視情況 toohello 前端或後端子網路上)。 此外，以 hello UDR 規則的地方，任何未將它轉換 hello 前端或後端的子網路的流量會被導向出 toohello 防火牆 (感謝您 tooUDR)。 hello 防火牆非對稱式資料流將會看到這個流量，而且將會降低 hello 輸出流量。 因此有三個層級的保護 hello 子網路的安全性：

* 任何前端或後端 NIC 上沒有公用 IP 位址。
* Nsg 拒絕 hello 網際網路流量。
* hello 防火牆卸除對稱流量。

在此範例中的 hello NSG 相關一個有趣的一點是它包含一個規則，也就是 toodeny 網際網路流量 toohello 整個虛擬網路，包括 hello 安全性子網路。 不過，由於 hello NSG 僅繫結 toohello 前端和後端子網路，hello 規則才會處理流量的輸入 toohello 安全性子網路。 如此一來，流量流 toohello 安全性子網路。

#### <a name="firewall-rules"></a>防火牆規則
Hello 防火牆上應該建立轉送規則。 由於 hello 防火牆封鎖或轉送所有輸入、 輸出和內部虛擬網路流量，都需要多個防火牆規則。 此外，所有傳入的流量達到 hello 安全性服務公用 IP 位址 （在不同的連接埠），toobe 處理 hello 防火牆。 最佳做法是設定 hello 子網路之前，先 toodiagram hello 邏輯流程和防火牆規則，tooavoid 稍後重新設定。 hello 圖是此範例中的 hello 防火牆規則的邏輯檢視：

![10]

> [!NOTE]
> 根據網路虛擬應用裝置中使用的 hello，hello 管理連接埠會有不同。 在此範例中，所參考的 Barracuda NextGen 防火牆使用連接埠 22、801 和 807。 請參閱 hello 應用裝置廠商文件 toofind hello 確切使用連接埠正在使用的 hello 裝置的管理。
>
>

#### <a name="firewall-rules-description"></a>防火牆規則描述
在 hello 前面邏輯圖表，因為 hello 防火牆 hello 該子網路上唯一的資源，不會顯示 hello 安全性子網路。 hello 圖表會顯示 hello 防火牆規則，以及如何在邏輯上允許或拒絕流量，不 hello 實際路由路徑。 此外，hello 外部連接埠為 hello RDP 流量會更高範圍的連接埠 (8014 – 8026) 和已選取的 tooloosely 對齊 hello 與選取的最後一個 hello 本機 IP 位址更容易閱讀的兩個八位元 （例如，本機伺服器位址 10.0.1.4 是相關聯與外部連接埠 8014）。 不過您可以使用任何更高範圍的連接埠，只要連接埠未衝突即可。

本例中，我們需要七種類型的規則︰

* 外部規則 (適用於輸入流量)：
  1. 防火牆管理規則： 此應用程式重新導向規則允許流量 toopass toohello 管理連接埠的 hello 網路的虛擬設備。
  2. RDP 規則 （適用於每個 Windows 伺服器）： 這些四項規則 （每個伺服器一個） 允許的 hello 管理個別的伺服器，透過 RDP。 hello 四個 RDP 規則無法也摺疊成一個規則，視 hello 的 hello 網路虛擬設備所使用的功能而定。
  3. 應用程式流量規則： 有兩個的這些規則，先針對 hello 前端的 web 流量，hello 和 hello hello 後端流量 （例如，web 伺服器 toodata 層） 的第二個。 這些規則的 hello 組態取決於 hello （您的伺服器放置的位置） 的網路架構及流量 （流動的方向 hello 流量，及使用哪些連接埠）。
     * hello 第一個規則可讓 hello 實際的應用程式流量 tooreach hello 應用程式伺服器。 Hello 其他規則允許的安全性與管理，而應用程式流量規則是允許外部使用者或服務 tooaccess hello 應用程式。 本例中，連接埠 80 上有單一 Web 伺服器。 因此單一防火牆應用程式規則重新導向輸入的流量 toohello 外部 IP，toohello web 伺服器的內部 IP 位址。 透過 NAT toohello 內部伺服器，會轉譯 hello 重新導向流量的工作階段。
     * hello 第二個規則是 hello 後端規則 tooallow hello web 伺服器 tootalk toohello AppVM01 伺服器 （但不是 AppVM02） 透過任何連接埠。
* 內部規則 (適用於內部虛擬網路流量)
  1. 輸出 tooInternet 規則： 這個規則允許來自任何網路流量 toopass toohello 選取網路。 此規則通常是預設的規則已經 hello 在防火牆上，但是已停用狀態。 在此範例中，應啟用此規則。
  2. DNS 規則： 這個規則允許只有 DNS （連接埠 53） 流量 toopass toohello DNS 伺服器。 如果此環境中，會封鎖大部分的流量從 hello 前端 toohello 後端。 這個規則特別允許來自任何本機子網路的 DNS。
  3. 子網路 toosubnet 規則： 這項規則是 tooallow hello 後端子 tooconnect tooany 伺服器 hello 前端子網路 （但不是 hello 反向） 上的任何伺服器。
* （適用於不符合任何先前的 hello 的流量） 的保全規則：
  1. 拒絕所有流量的規則： 此都拒絕規則應該一律 hello 最終規則 （依據優先順序） 且因此如果流量失敗時 toomatch hello 上述規則不會捨棄此規則。 這是預設規則，通常為現成啟用狀態。 任何修改，不就需要通常 toothis 規則。

> [!TIP]
> Hello 上第二個應用程式流量的規則，toosimplify 此範例中，任何連接埠不允許。 在實際案例中，hello 最特定的連接埠和位址範圍應該是此規則使用的 tooreduce hello 受攻擊面。
>
>

一旦建立 hello 一個規則，請務必允許或拒絕所需的每個規則 tooensure 流量 tooreview hello 優先順序。 例如，hello 規則是依優先順序。

#### <a name="conclusion"></a>結論
這個範例是更複雜，但完成種保護及隔離 hello 網路比 hello 前面的範例。 （範例 2 會保護只 hello 應用程式，而範例 1 只會隔離子網路）。 這項設計可以讓監視這兩個方向的流量和保護不只是 hello 輸入應用程式伺服器，但此網路上的所有伺服器的網路安全性原則會強制執行。 此外，hello 應用裝置中使用，根據稽核完整的流量和感知即可達成。 如需詳細資訊，請參閱 hello[詳細組建指示][Example3]。 這些指示包括：

* 如何 toobuild 此範例周邊網路與傳統的 PowerShell 指令碼。
* 如何 toobuild 此範例使用 Azure Resource Manager 範本。
* 每個 UDR、NSG 命令和防火牆規則的詳細描述。
* 詳細的流量流程案例，顯示每一層允許或拒絕流量的方式。

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>範例 4 新增使用站對站虛擬設備 VPN 的混合式連接
[備份 tooFast 開始](#fast-start)|推出詳述可用的組建指令

[![11]][11]

#### <a name="environment-description"></a>環境描述
混合式網路使用網路虛擬應用裝置 (NVA) 可以加入 tooany hello 範例 1、 2 或 3 中所述的周邊網路類型。

Hello 上圖所示，透過 VPN 連線 hello 網際網路 （站對站） 是使用的 tooconnect 在內部部署網路 tooan NVA 透過 Azure 虛擬網路。

> [!NOTE]
> 如果您使用 ExpressRoute 啟用的 hello Azure 公用對等互連選項時，就應該建立靜態路由。 這個靜態路由應該路由 toohello NVA VPN IP 位址，您公司的網際網路且不會透過 hello ExpressRoute 連線。 hello NAT 需要 hello ExpressRoute Azure 公用對等體的選項可能會破壞 hello VPN 工作階段。
>
>

一旦 hello VPN 已經就定位，hello NVA 會變成 hello 集中所有的網路和子網路。 hello 防火牆轉寄規則會決定允許流量，哪些流量都會透過 NAT 轉譯、 重新導向，或會卸除 （即使 hello 與內部網路與 Azure 之間的流量）。

流量應該要謹慎，因為它們可以最佳化，或降低設計模式中，根據 hello 特定使用案例。

使用內建的範例 3，hello 環境，然後再新增 站對站 VPN 混合式網路連線，會產生下列設計 hello:

[![12]][12]

hello 在內部部署路由器或與您的 VPN、 NVA 相容的任何其他網路裝置是 hello VPN 用戶端。 此實體的裝置會負責起始和維護您 NVA hello VPN 連線。

以邏輯方式 toohello NVA，hello 網路看起來像 4 個不同 hello 規則的 「 安全性區域 」 hello NVA 必須 hello 主要主管這些區域之間的流量：

![13]

#### <a name="conclusion"></a>結論
hello 加入站對站 VPN 混合式網路連接 tooan Azure 虛擬網路可以 hello 在內部部署網路擴充至 Azure 以安全的方式。 您的流量會加密，並將路由中使用 VPN 連線，透過網際網路 hello。 在此範例中的 hello NVA 提供中央位置 tooenforce，並管理 hello 安全性原則。 如需詳細資訊，請參閱詳細的 hello 建置 （推出） 的指示。 這些指示包括：

* 如何 toobuild 此範例周邊網路的 PowerShell 指令碼。
* 如何 toobuild 此範例使用 Azure Resource Manager 範本。
* 顯示此設計中流量如何流通的詳細流量流程案例。

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>範例 5 新增使用站對站 Azure VPN 閘道的混合式連接
[備份 tooFast 開始](#fast-start)|推出詳述可用的組建指令

[![14]][14]

#### <a name="environment-description"></a>環境描述
使用 Azure VPN 閘道的混合式網路可以加入 tooeither 周邊網路類型 1 或 2 的範例中所述。

Hello 前圖所示，透過 VPN 連線 hello 網際網路 （站對站） 是使用的 tooconnect 在內部部署網路 tooan 透過 Azure VPN 閘道的 Azure 虛擬網路。

> [!NOTE]
> 如果您使用 ExpressRoute 啟用的 hello Azure 公用對等互連選項時，就應該建立靜態路由。 這個靜態路由應該路由 toohello 您公司的網際網路且不會透過 ExpressRoute WAN hello NVA VPN IP 位址。 hello NAT 需要 hello ExpressRoute Azure 公用對等體的選項可能會破壞 hello VPN 工作階段。
>
>

hello 下圖顯示 hello 兩個網路邊緣在此範例中。 在第一個邊緣 hello，hello NVA 和 Nsg 控制內部 Azure 網路和 Azure 之間的流量並 hello 網際網路。 hello 第二個邊緣是 hello Azure VPN 閘道，這是在內部部署與 Azure 之間不同的隔離網路邊緣。

流量應該要謹慎，因為它們可以最佳化，或降低設計模式中，根據 hello 特定使用案例。

使用範例 1，內建的 hello 環境，然後再新增 站對站 VPN 混合式網路連線，會產生下列設計 hello:

[![15]][15]

#### <a name="conclusion"></a>結論
hello 加入站對站 VPN 混合式網路連接 tooan Azure 虛擬網路可以 hello 在內部部署網路擴充至 Azure 以安全的方式。 使用 hello 原生 Azure VPN 閘道，您的流量是 IPSec 加密，並透過 hello 網際網路路由傳送。 此外，使用 hello Azure VPN 閘道，可以提供 （沒有其他授權成本與第三方 NVAs） 的成本較低的選項。 這個選項是範例 1 最經濟實惠的地方，因為不使用任何 NVA。 如需詳細資訊，請參閱詳細的 hello 建置 （推出） 的指示。 這些指示包括：

* 如何 toobuild 此範例周邊網路的 PowerShell 指令碼。
* 如何 toobuild 此範例使用 Azure Resource Manager 範本。
* 顯示此設計中流量如何流通的詳細流量流程案例。

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>範例 6：新增使用 ExpressRoute 的混合式連接
[備份 tooFast 開始](#fast-start)|推出詳述可用的組建指令

[![16]][16]

#### <a name="environment-description"></a>環境描述
混合式網路，使用的 ExpressRoute 私用對等連接，可以加入 tooeither 周邊網路類型 1 或 2 的範例中所述。

Hello 前圖所示，ExpressRoute 私人互連提供您的內部部署網路與 hello Azure 虛擬網路之間的直接連線。 流量代表只有 hello 服務提供者網路和 hello Microsoft Azure 網路，永遠不會觸及 hello 網際網路。

> [!TIP]
> 使用 ExpressRoute 關閉 hello 網際網路保持公司的網路流量。 也能符合 ExpressRoute 提供者的服務等級協定。 而透過站對站 Vpn，hello Azure 閘道最大輸送量是 200 Mbps too10 Gbps 透過 ExpressRoute，可以傳送 hello Azure 閘道。
>
>

Hello 下列圖表所示，使用此選項 hello 環境現在有兩個網路邊緣。 hello NVA 以及 NSG 控制流量的內部 Azure 網路之間以及 Azure 與 hello 網際網路與內部部署與 Azure 之間的不同的隔離網路邊緣 hello 閘道時。

流量應該要謹慎，因為它們可以最佳化，或降低設計模式中，根據 hello 特定使用案例。

使用範例 1，內建的 hello 環境，然後再新增 ExpressRoute 混合式網路連線，會產生下列設計 hello:

[![17]][17]

#### <a name="conclusion"></a>結論
ExpressRoute 私用對等互連網路連線的 hello 加法可以 hello 在內部部署網路擴充至 Azure 中的安全、 低延遲、 更高版本執行的方式。 此外，使用 hello 原生 Azure 閘道，就如同此範例中，提供成本較低的選項 （沒有其他授權與第三方 NVAs 一樣）。 如需詳細資訊，請參閱詳細的 hello 建置 （推出） 的指示。 這些指示包括：

* 如何 toobuild 此範例周邊網路的 PowerShell 指令碼。
* 如何 toobuild 此範例使用 Azure Resource Manager 範本。
* 顯示此設計中流量如何流通的詳細流量流程案例。

## <a name="references"></a>參考
### <a name="helpful-websites-and-documentation"></a>實用的網站和文件
* 使用 Azure Resource Manager 存取 Azure：
* 使用 PowerShell 存取 Azure：[https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* 虛擬網路文件：[https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* 網路安全性群組文件：[https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* 使用者定義路由文件：[https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Azure 虛擬閘道器︰[https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* 站對站 VPN：[https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* （是確定 toocheck 出 hello 「 入門 」 和 「 如何 」 區段） 的 ExpressRoute 文件： [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "安全性選項流程圖"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Azure Security Features"
[3]: ./media/best-practices-network-security/dmzcorporate.png "A DMZ in a Corporate network"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Azure Security Architecture"
[5]: ./media/best-practices-network-security/dmzazure.png "A DMZ in an Azure Virtual Network"
[6]: ./media/best-practices-network-security/dmzhybrid.png "Hybrid Network with Three Security Boundaries"
[7]: ./media/best-practices-network-security/example1design.png "具有 NSG 的輸入 DMZ"
[8]: ./media/best-practices-network-security/example2design.png "具有 NVA 和 NSG 的輸入 DMZ"
[9]: ./media/best-practices-network-security/example3design.png "具有 NVA、NSG 和 UDR 的雙向 DMZ"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "hello 防火牆規則的邏輯檢視"
[11]: ./media/best-practices-network-security/example3designoptions.png "連接 NVA 的 DMZ 混合式網路"
[12]: ./media/best-practices-network-security/example4designs2s.png "使用站對站 VPN 連接 NVA 的 DMZ"
[13]: ./media/best-practices-network-security/example4networklogical.png "Logical Network from NVA Perspective"
[14]: ./media/best-practices-network-security/example5designoptions.png "連接 Azure 閘道的 DMZ 站對站混合式網路"
[15]: ./media/best-practices-network-security/example5designs2s.png "使用站對站 VPN 連接 Azure 閘道的 DMZ"
[16]: ./media/best-practices-network-security/example6designoptions.png "連接 Azure 閘道的 DMZ ExpressRoute 混合式網路"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "使用 ExpressRoute 連線連接 Azure 閘道的 DMZ"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
