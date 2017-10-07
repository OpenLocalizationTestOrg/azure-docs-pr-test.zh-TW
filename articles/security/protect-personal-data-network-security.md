---
title: "aaaProtect 個人資料與 Azure 網路的安全性功能 |Microsoft 文件"
description: "使用 Azure 網路安全性功能來保護個人資料"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>使用網路安全性功能來保護個人資料：Azure 應用程式閘道和網路安全性群組

本文章提供資訊和程序，可協助您使用 Azure 應用程式閘道和網路安全性群組 tooprotect 個人資料。

個人資料的多層式的安全性策略 tooprotect hello 隱私權的重要元素是防禦機制以防止 SQL 資料隱碼或跨網站指令碼，例如通用的弱點可能會惡意探索。 保持超出 Azure 虛擬網路的不必要的網路流量可協助防止潛在的敏感資料和 Microsoft Azure 提供您工具 toohelp 保護資料，避免攻擊者危害。

## <a name="scenario"></a>案例

大型出航公司搬遷後 hello 美國，展開在 hello 地中海、 Adriatic，與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。 中的努力 furtherance，它取得數個較小海上行位於義大利、 德國、 丹麥和 hello 英國

hello 公司使用 Microsoft Azure 雲端 toostore hello 中的公司資料，然後處理和存取這項資料的虛擬機器上執行應用程式。 此資料包含其全球客戶群的名稱、地址、電話號碼和信用卡資訊等個人識別資訊。 它也會包含在所有位置的傳統的人力資源資訊，例如地址、 電話號碼、 稅務識別碼和醫療公司員工的相關資訊。 hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。

從 hello 公司遠端辦公室和位於 hello 世界各地的旅遊代理程式的公司員工存取 hello 網路擁有存取 toosome 公司資源，並使用 web 應用程式裝載於 Azure Vm toointeract 與它。

## <a name="problem-statement"></a>問題陳述

hello 公司必須保護客戶的 hello 隱私權和員工的個人資料，避免攻擊者利用軟體弱點 toorun 惡意程式碼，可能會公開的個人資料儲存或 hello 公司以雲端為基礎的應用程式所使用。

## <a name="company-goal"></a>公司目標

hello 公司的目標 tooensure 未經授權的人員無法存取公司的 Azure 虛擬網路和 hello 應用程式和資料位於那里利用高畫質視訊常見弱點。 

## <a name="solutions"></a>解決方案

Microsoft Azure 提供的安全性機制 toohelp 防止垃圾的流量進入 Azure 虛擬網路。 輸入和輸出流量的控制傳統上是由防火牆執行。 在 Azure 中，您可以使用 hello 應用程式閘道以 hello Web 應用程式防火牆和網路安全性群組 (NSG) 做為簡單的分散式防火牆。 這些工具讓您 toodetect，而且封鎖不想要的網路流量。

### <a name="application-gatewayweb-application-firewall"></a>應用程式閘道/Web 應用程式防火牆

hello [Web 應用程式防火牆](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)(WAF) 元件的 hello [Azure 應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)保護 web 應用程式，也就是越來越多的常見的已知惡意攻擊的目標弱點。 集中式 WAF 可以防禦 Web 攻擊並簡化安全性管理，而不需要變更任何應用程式。

Azure WAF 可處理各種攻擊類別，包括 SQL 插入、跨網站指令碼、HTTP 通訊協定違規和異常、Bot、編目程式、掃描程式、常見應用程式錯誤設定、HTTP 阻絕服務，以及其他常見的攻擊，例如命令插入、HTTP 要求、走私、HTTP 回應分割及遠端檔案包含攻擊。 

您可以使用 WAF，建立應用程式閘道，或新增 WAF tooan 現有應用程式閘道。 在上述任何情況下，Azure 應用程式閘道都需要有自己的子網路。

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>如何建立具有 WAF 的應用程式閘道？ 

toocreate WAF 啟用，與新的應用程式閘道 hello 遵循：

1. Hello 和 toohello Azure 入口網站中的記錄檔**我的最愛**窗格中的 hello 入口網站中，按一下 **新增**

2. 在 hello**新增**刀鋒視窗中，按一下 **網路**。

3. 按一下 [應用程式閘道]。

4. 瀏覽 toohello Azure 入口網站**按一下 新增\>網路\>應用程式閘道。**

   ![建立應用程式閘道](media/protect-netsec/app-gateway-01.png)

5. 在 hello**基本概念**刀鋒視窗中，輸入下列欄位的 hello hello 值： 名稱、 層 （Standard 或 WAF） SKU 大小 （小、 中或大） 執行個體計數 (提供高可用性 2)、 訂用帳戶資源群組和位置。

6. 在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。 此步驟會開啟輸入 hello 刀鋒視窗中選擇虛擬網路。

7. 按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。

8. 輸入下列值的 hello： 名稱、 位址空間、 子網路名稱、 子網路位址範圍。 按一下 [確定] 。

9. 在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇 hello IP 位址類型。

10. 依序按一下 [選擇公用 IP 位址] 和 [新建]。

11. 接受 hello 預設值，然後按一下  **確定。**

12. 在 hello**設定**刀鋒視窗底下**接聽程式組態**，選取 HTTP 或 HTTPS 之下 toouse**通訊協定**。 toouse HTTPS，需要憑證。

13. 設定 hello WAF 特定的設定：**防火牆狀態**(**啟用**) 和**防火牆模式**(**防止**)。 如果您選擇**偵測**做為 hello 模式流量只會記錄。

14. 檢閱 hello**摘要**頁面上，按一下 **確定**。 現在 hello 應用程式閘道會排入佇列，並建立。

建立 hello 應用程式閘道後，您可以瀏覽 tooit hello 入口網站中的，並繼續 hello 應用程式閘道的組態。

![建立應用程式閘道](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>如何新增 WAF tooan 現有的應用程式？

tooupdate 現有的應用程式閘道 toosupport WAF 防止模式中 hello 遵循：

1. 在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。

2. 按一下 hello hello 中的現有應用程式閘道**所有資源**刀鋒視窗。 
>[!NOTE]
注意： 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 名稱 hello 篩選器中依名稱... 方塊 tooeasily 存取 hello DNS 區域。
3. 按一下**Web 應用程式防火牆**更新 hello 應用程式閘道的設定：**升級 tooWAF 層**（核取）**防火牆狀態**（啟用）， **防火牆模式**（防止）。 您也需要 tooconfigure hello 規則集，並設定已停用的規則。

如需詳細資訊 toocreate WAF 與新的應用程式閘道以及 tooadd WAF tooan 現有應用程式的閘道，請參閱[建立 web 應用程式防火牆使用 hello 入口網站應用程式閘道。](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>網路安全性群組

A[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)(NSG) 包含一份可允許或拒絕網路流量 tooresources 太連線安全性規則[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/)(VNet)。 Nsg 可以是相關聯的 toosubnets 或個別 Vm。 當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。 流量可以進一步限制也關聯 NSG tooa VM 或 nic。

NSG 包含四個屬性：名稱、地區、資源群組和規則。
>[!Note]
雖然 NSG 存在於資源群組中，可能很關聯的 tooresources 在資源群組中，只要 hello 資源屬於 hello 與 hello NSG 的相同 Azure 區域。

NSG 規則包含 9 個屬性：名稱、通訊協定 (TCP、UDP 或 \*，其中包括 ICMP 以及 UDP 和 TCP)、來源連接埠範圍、目的地連接埠範圍、來源位址前置詞、目的地位址前置詞、方向 (輸入或輸出)、優先順序 (介於 100 與 4096 之間) 和存取類型 (允許或拒絕)。 所有的 Nsg 包含一組可刪除，或您所建立的 hello 規則覆寫預設規則。

#### <a name="how-do-i-implement-nsgs"></a>如何實作 NSG？

實作 Nsg 需要計劃，並有幾個設計考量，您需要 tootake 納入考量。 其中包括每個訂用帳戶和每個 NSG; 規則 Nsg hello 數目的限制VNet 和子網路設計，特殊的規則、 ICMP 流量，具有子網路、 負載平衡器，以及更多層的隔離。

如需規劃及實作 NSG 的詳細指引以及範例部署案例，請參閱[使用網路安全性群組來篩選網路流量](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)。

#### <a name="how-do-i-create-rules-in-an-nsg"></a>如何在 NSG 中建立規則？

toocreate 輸入現有 NSG 中的規則，執行下列 hello:

1. 依序按一下 [瀏覽] 和 [網路安全性群組]。

2. 在 hello Nsg 清單中按一下**NSG 前端**，然後**輸入安全性規則。**

3. 在 hello 清單中的連入的安全性規則，按一下 **新增。**

4. 在 hello 下列欄位中輸入 hello 值： 名稱、 優先順序、 來源、 通訊協定、 來源範圍，目的地，目的地連接埠範圍和動作。

幾秒之後，hello 新規則會出現在 hello NSG。

![網路安全性規則](media/protect-netsec/inbound-security.png)

如需 toocreate Nsg 中的子網路，如何建立規則，並與前端和後端的子網路，將 NSG 關聯的詳細指示，請參閱[建立使用 hello Azure 入口網站的網路安全性群組。](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>後續步驟

[Azure 網路安全性](https://azure.microsoft.com/blog/azure-network-security/)

[Azure 網路安全性最佳做法](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[取得網路安全性群組的相關資訊](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Web 應用程式防火牆 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
