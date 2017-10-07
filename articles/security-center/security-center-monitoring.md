---
title: "aaaSecurity 監視 Azure 資訊安全中心 |Microsoft 文件"
description: "這篇文章可協助您 tooget 入門監視 Azure 資訊安全中心中的功能。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Azure 資訊安全中心的安全性健康情況監視
這篇文章可協助您使用 hello Azure 資訊安全中心 toomonitor 符合原則中的監視功能。

## <a name="what-is-security-health-monitoring"></a>什麼是安全性健康情況監視？
我們通常將為監看及等候事件 toooccur，以便我們可以反應 toohello 狀況監視。 安全性監視是指 toohaving 稽核時，不符合組織的標準或最佳作法 tooidentify 系統資源的主動式策略。

## <a name="monitoring-security-health"></a>監視安全性健全狀況
啟用後[安全性原則](security-center-policies.md)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。 您可以立即取得網路組態的相關資訊。 可能需要一小時或更多有關虛擬機器組態，例如安全性更新狀態和作業系統設定、 toobecome 可用。 您可以檢視您的資源和任何問題 hello 安全性狀態中 hello**防止**> 一節。 您也可以檢視這些問題的清單上 hello**建議**磚。

如需有關如何 tooapply 建議事項，讀取[實作 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)。

在 hello**防止** 區段中，您可以監視您的資源 hello 安全性狀態。 在下列範例的 hello，您可以查看每項資源的磚 （運算、 網路功能、 存放裝置 （& s） 資料和應用程式） 中具有已識別問題的 hello 總數。

![資源安全性健康情況圖格](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>監視計算
當您按一下**計算**磚，hello**計算**開啟刀鋒視窗會顯示三個索引標籤：

- **概觀**︰監視和虛擬機器建議。
- **虛擬機器**︰列出所有虛擬機器及其目前的安全性狀態。
- **雲端服務**︰資訊安全中心監視的所有 Web 和背景工作角色清單。

![遺失的系統更新 (依虛擬機器)](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

在每個索引標籤中，您可以擁有多個區段，並在每個區段中，您可以選取個別選項 toosee hello 的更多詳細建議步驟 tooaddress 該特定問題。 

#### <a name="monitoring-recommendations"></a>監視建議
本節說明已初始化的資料收集和其目前狀態的虛擬機器的 hello 總數。 所有虛擬機器都有初始化的資料收集之後，就會準備 tooreceive 資訊安全中心的安全性原則。 當您按一下這個項目時，hello **VM 代理程式已遺失或沒有回應**刀鋒視窗隨即開啟。 

![遺失的系統更新 (依虛擬機器)](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>虛擬機器建議
本節提供一組 Azure 資訊安全中心所監視之[每個虛擬機器的建議](security-center-virtual-machine-recommendations.md)。 hello 第一個資料行列出 hello 建議。 hello 第二個資料行顯示 hello 總數會受到該項建議的虛擬機器。 hello 第三個資料行顯示 hello hello 問題嚴重性 hello 下列螢幕擷取畫面所示。

![虛擬機器建議](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> 有至少一個公用端點的虛擬機器會顯示在 hello**網路健全狀況**刀鋒視窗中 hello**網路拓樸**清單。
>
>

每個建議在經過點選之後，都會有一組可供執行的動作。 比方說，如果您按一下**遺漏的系統更新**，hello**遺漏的系統更新**刀鋒視窗隨即開啟。 它會列出遺失的修補程式和 hello hello 遺失更新的嚴重性 hello 下列所示的 hello 虛擬機器螢幕擷取畫面。

![虛擬機器遺失的系統更新](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

hello**遺漏的系統更新**刀鋒視窗中顯示的資料表以 hello 下列資訊：

* **虛擬機器**: hello hello 遺失更新的虛擬機器的名稱。
* **系統更新**: hello 的系統更新遺漏的數目。
* **上次掃描時間**: hello 時間資訊安全中心上次掃描更新 hello 虛擬機器。
* **狀態**: hello hello 建議的目前狀態：
  * **開啟**: hello 建議的解決不尚未。
  * **正在進行中**: hello 建議目前正在套用的 toothose 資源，並由您不需要任何動作。
  * **解析**: hello 建議已經完成。 （當 hello 問題已經解決時，hello 項目會呈暗灰色）。
* **嚴重性**： 描述該特定建議事項的 hello 嚴重性：
  * **高**：某個有意義的資源 (應用程式、虛擬機器或網路安全性群組) 有弱點存在，並且需要注意。
  * **媒體**： 非關鍵的或額外的步驟是必要的 toocomplete 處理序或消除弱點。
  * **低**：應該處理但不需要立即注意的弱點。 (根據預設，不呈現低的建議，但是如果您想 tooview，您可以篩選低建議它們。)

tooview hello 建議的詳細資訊，請按一下 hello hello 虛擬機器名稱。 該虛擬機器的新刀鋒視窗會開啟 hello 的更新清單中 hello 下列螢幕擷取畫面所示。

![特定虛擬機器遺失的系統更新](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> hello 安全性建議事項會與 hello hello 相同**建議**刀鋒視窗。 請參閱 hello[實作 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)發行項，如需有關如何 tooresolve 建議。 這僅適用於虛擬機器，也適用於所有 hello 中可用的資源不只**資源健全狀況**磚。
>
>

#### <a name="virtual-machines-section"></a>虛擬機器區段
hello 虛擬機器 區段可讓您的所有虛擬機器和建議事項概觀。 每個資料行代表一組建議 hello 下列螢幕擷取畫面所示：

![所有虛擬機器和建議的概觀](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

hello 圖示出現在每個建議可協助您 tooquickly 識別需要注意和 hello 類型建議事項的 hello 虛擬機器。

Hello 上述範例中，在一部虛擬機器會具有關於端點保護的重要建議。 tooget 需 hello 虛擬機器，按一下它。 開啟的新刀鋒視窗表示此虛擬機器中 hello 下列螢幕擷取畫面所示。

![虛擬機器安全性詳細資料](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

此刀鋒視窗有 hello 虛擬機器的 hello 安全性詳細資料。 在 hello 這個刀鋒視窗底部，您可以看到 hello 建議動作並 hello 的每個問題的嚴重性。

#### <a name="cloud-services-section"></a>雲端服務區段
雲端服務的建議是時建立的 hello 作業系統版本已過期 hello 下列螢幕擷取畫面所示：

![雲端服務的健康情況狀態](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

在此案例中，您需要在建議 （這不是 hello 前一個範例的 hello 案例），您需要 toofollow hello 步驟 hello 建議 tooupdate hello 作業系統版本。 當有可用的更新時，您會有警示 （紅色或橙色-取決於 hello hello 問題嚴重性）。 當您按一下此警示的 hello WebRole1 （與您的 web 應用程式自動部署 tooIIS 執行 Windows Server） 或 WorkerRole1 （與您的 web 應用程式自動部署 tooIIS 執行 Windows Server） 的資料列時的新刀鋒視窗隨即開啟並更詳細建議 hello 下列螢幕擷取畫面所示：

![雲端服務詳細資料](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee 的更精準解釋這項建議中，按一下**更新的 OS 版本**下 hello**描述**資料行。 hello**更新的 OS 版本 （預覽）**刀鋒視窗會開啟具有更多詳細資料。

![雲端服務建議](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>監視虛擬網路
當您按一下**網路**磚，hello**網路**刀鋒視窗會開啟含有詳細 hello 下列螢幕擷取畫面所示：

![網路刀鋒視窗](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>網路功能的建議
Hello 虛擬機器的資源健全狀況資訊，例如此刀鋒視窗會提供在 hello hello 刀鋒視窗的頂端和受監視的網路清單問題的摘要的清單 hello 下方。

hello 網路狀態分解 > 一節列出潛在的安全性問題，並提供[建議](security-center-network-recommendations.md)。 可能的問題包括：

* 未安裝新一代防火牆 (NGFW)
* 未啟用子網路上的網路安全性群組
* 未啟用虛擬機器上的網路安全性群組
* 限制透過公用外部端點的外部存取
* 狀況良好的網際網路面向端點

當您按一下建議時，hello 下列範例所示的新刀鋒視窗會開啟 hello 建議相關的更多詳細資料。

![Hello 網路刀鋒視窗中的建議的詳細資料](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

在此範例中，hello**設定遺失的網路安全性群組的子網路**刀鋒視窗中有一份子網路和虛擬機器遺失的網路安全性群組保護。 如果您按一下 hello 子網路 toowhich 想 tooapply hello 網路安全性群組，會開啟另一個刀鋒視窗。

在 hello**選擇網路安全性群組**刀鋒視窗中，您可以選取 hello 最適當的網路安全性群組 hello 的子網路，或者您可以建立新的網路安全性群組。

#### <a name="internet-facing-endpoints-section"></a>網際網路面向端點區段
在 [hello**網際網路對向端點**] 區段中，您可以看到 hello 目前未設定與網際網路對向端點和其目前狀態的虛擬機器。

![使用網際網路面向端點所設定的虛擬機器和狀態](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

此資料表具有代表 hello 虛擬機器，hello 網際網路對向的 IP 位址的 hello 端點名稱和 hello 目前的網路安全性群組 hello 嚴重性狀態和 hello NGFW。 hello 表格是依嚴重性排序：

* 紅色 (在頂端)：高優先順序，應立即處理
* 橘色︰中等優先順序，應儘速處理
* 綠色 (最後一個)︰健康狀態

#### <a name="networking-topology-section"></a>網路拓撲區段
hello**網路拓樸**區段具有 hello 資源的階層式檢視中 hello 下列螢幕擷取畫面所示：

![網路拓撲區段中資源的階層式檢視](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

此資料表是依嚴重性排序 (虛擬機器和子網路)︰

* 紅色 (在頂端)：高優先順序，應立即處理
* 橘色︰中等優先順序，應儘速處理
* 綠色 (最後一個)︰健康狀態

在此拓撲檢視中的 hello 第一個層級具有[虛擬網路](../virtual-network/virtual-networks-overview.md)，[虛擬網路閘道](/vpn-gateway/vpn-gateway-site-to-site-create.md)，和[虛擬網路 （傳統）](/virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 hello 第二個層級的子網路，而且 hello 第三個層級 hello 隸屬 toothose 子網路的虛擬機器。 hello 右邊的資料行具有 hello hello 網路安全性群組，為這些資源的目前狀態中 hello 下列範例所示：

![Hello 網路安全性群組的 網路拓樸區段的狀態](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

hello 此刀鋒視窗的下半部都有 hello 建議此虛擬機器，類似 toowhat 先前所述。 您可以按一下 更多建議 toolearn 或套用 hello 所需的安全性控制或組態。

### <a name="monitor-storage--data"></a>監視儲存體和資料

當您按一下**儲存體與資料**在 hello**防止**區段，hello**資料資源**刀鋒視窗中開啟 SQL 和儲存體的建議。 它也有[建議](security-center-sql-service-recommendations.md)hello 一般健全狀況狀態的 hello 資料庫。 如需儲存體加密的詳細資訊，請閱讀[在 Azure 資訊安全中心啟用 Azure 儲存體帳戶的加密](security-center-enable-encryption-for-storage-account.md)。

![資料資源](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

在下**SQL 建議**，您可以按一下任何建議以及取得更多相關詳細資料進一步的動作 tooresolve 發生問題。 hello 下列範例顯示 hello hello 擴充**SQL database 上的資料庫稽核與威脅偵測**建議。

![有關 SQL 建議的詳細資料](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

hello **SQL 資料庫上的啟用稽核與威脅偵測**分頁有 hello 下列資訊：

* SQL 資料庫的清單
* hello 伺服器所在它們位於
* 此設定是否繼承自 hello 伺服器，或如果它是唯一的這個資料庫中的相關資訊
* hello 目前狀態
* hello hello 問題嚴重性

當您按一下 hello 資料庫 tooaddress 這項建議時，hello**稽核與威脅偵測**刀鋒視窗會開啟 hello 遵循畫面所示。

![稽核與威脅的偵測刀鋒視窗](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

tooenable 稽核，選取**ON**下 hello**稽核**選項。

### <a name="monitor-applications"></a>監視應用程式

如果您的 Azure 工作負載會有應用程式位於[（建立透過 Azure 資源管理員） 的虛擬機器](../azure-resource-manager/resource-manager-deployment-model.md)公開的 web 連接埠 （TCP 連接埠 80 和 443），與資訊安全中心可以監視這些 tooidentify 潛在的安全性問題並建議補救步驟。 當您按一下 hello**應用程式**磚，hello**應用程式**刀鋒視窗會開啟與 hello 中建議的一連串**應用程式建議**> 一節。 它也會顯示每個主機/虛擬 IP 的 hello 應用程式分解 hello 下列螢幕擷取畫面所示。

![應用程式安全性健全狀況](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

就像您未與 hello 其他建議，您可以按一下建議 toosee 詳細 hello 問題及如何 tooremediate。 hello hello 遵循圖所示的範例是已被識別為不安全的 web 應用程式的應用程式。 當您選取已被視為不安全的 hello 應用程式時，另一個刀鋒視窗會開啟以 hello 下列可用的選項：

![不安全之應用程式的相關詳細資料](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

此刀鋒視窗會有此應用程式的所有建議清單。 當您按一下 hello**加入 web 應用程式防火牆**建議、 hello**加入 Web 應用程式防火牆**刀鋒視窗中開啟您 tooinstall 選項與 web 應用程式的防火牆 (WAF) 從合作夥伴擔任下列螢幕擷取畫面所示的 hello。

![新增 Web 應用程式防火牆對話方塊](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>另請參閱
在本文中，您學到如何 toouse 監視 Azure 資訊安全中心中的功能。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)： 深入了解如何在 Azure 資訊安全中心 tooconfigure 安全性設定。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)： 了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)： 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)： 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：尋找有關 Azure 安全性與相容性的部落格文章。
