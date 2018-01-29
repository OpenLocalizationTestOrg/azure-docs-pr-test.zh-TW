---
title: "將應用程式與 Azure 虛擬網路整合"
description: "示範如何將 Azure App Service 中的應用程式連接到新的或現有的 Azure 虛擬網路"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: b755197af7e8791e01273bcc25f72c0d92ef6bc2
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>將您的應用程式與 Azure 虛擬網路整合
本文件說明 Azure App Service 虛擬網路整合功能，以及示範如何使用 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中的應用程式來設定此功能。 如果您不熟悉 Azure 虛擬網路 (VNet)，這是一種功能，可讓您在非網際網路可路由網路中放置許多您可控制其存取的 Azure 資源。 接著，可以使用各種 VPN 技術，將這些網路連接到您的內部部署網路。 若要深入了解「Azure 虛擬網路」，請從以下資訊著手：[Azure 虛擬網路概觀][VNETOverview]。 

Azure App Service 具有兩種形式。 

1. 支援全系列價格方案的多租用戶系統
2. 部署到您的 VNet 的 App Service 環境 (ASE) 進階功能。 

本文會演練 VNet 整合和非 App Service 環境。 如果您想要了解 ASE 功能的相關資訊，請從以下的資訊開始︰[App Service 環境簡介][ASEintro]。

VNet 整合能讓您的 Web 應用程式存取虛擬網路中的資源，但不授與從虛擬網路存取 Web 應用程式的專用權限。 私人網站存取是指讓您的應用程式只能透過私人網路 (例如從 Azure 虛擬網路中) 存取。 只有使用透過內部負載平衡器 (ILB) 設定的 ASE 才可使用私人網站存取。 如需使用 ILB ASE 的詳細資訊，請從以下的文章開始︰[建立和使用 ILB ASE][ILBASE]。 

您會用到的 VNet 整合常見案例，就是讓 Web 應用程式能夠存取資料庫，或存取在 Azure 虛擬網路之虛擬機器上執行的 Web 服務。 使用 VNet 整合時，您不需要公開 VM 上應用程式的公用端點，但可以改用專用的非網際網路可路由位址。 

VNet 整合功能：

* 需要「標準」、「進階」或「隔離」價格方案 
* 使用傳統 VNet 或 Resource Manager VNet 使用傳統或 Resource Manager VNet 
* 支援 TCP 和 UDP
* 適用於 Web、 行動裝置、 應用程式開發介面應用程式和功能的應用程式
* 可讓應用程式一次只連接到 1 個 VNet
* 可在 App Service 方案中與最多五個 VNet 整合 
* 可讓 App Service 方案中的多個應用程式使用相同的 VNet
* 由於 VNet 閘道上的 SLA，可支援 99.9% SLA

VNet 整合不支援的事項包括：

* 掛接磁碟機
* AD 整合 
* NetBios
* 私人網站存取

### <a name="getting-started"></a>開始使用
在將 Web 應用程式連接至虛擬網路之前，請留意以下事項：

* VNet 整合僅會使用**標準**、**進階**或**隔離**價格方案中的應用程式。 如果您啟用此功能，然後將您的 App Service 方案調整為不支援的價格方案，則您的應用程式會失去與其正在使用之 VNet 的連接。 
* 如果目標虛擬網路已存在，您必須先以動態路由閘道器啟用其點對站 VPN，才能使該虛擬網路與應用程式連接。 如果您以靜態路由設定閘道，便無法啟用點對站的虛擬私人網路 (VPN)。
* VNet 與您的 App Service 方案 (ASP) 必須位於同一個訂用帳戶中。 
* 與 VNet 整合的應用程式將使用指定給該 VNet 的 DNS。
* 依預設，應用程式整合只會根據 VNet 中定義的路由，將流量路由傳送至 VNet。 

## <a name="enabling-vnet-integration"></a>啟用 VNet 整合

您可以選擇將應用程式連接到新的或現有的虛擬網路。 如果您在整合時建立新網路，則除了建立 VNet 外，還會為您預先設定動態路由閘道，並將啟用點對站 VPN。 

> [!NOTE]
> 設定新的虛擬網路整合可能需要幾分鐘的時間才能完成。 
> 
> 

若要啟用 VNet 整合，請開啟您的應用程式 [設定]，然後選取 [網路功能]。 開啟的 UI 提供三個網路功能選項。 本指南只探討 VNet 整合，但本文件稍後會討論混合式連接和 App Service 環境。 

如果您的應用程式不在正確的價格方案中，UI 可讓您將方案調整為您選擇的更高價格方案。

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>啟用與既存的 VNet 的 VNet 整合
VNet 整合 UI 可讓您從 VNet 的清單中選取。 傳統 VNet 會在 VNet 名稱旁邊的括號中以「傳統」文字指出它們屬於這一類。 清單會以先列出 Resource Manager VNet 的方式排序。 在下面顯示的影像中，您可以看到只有一個 VNet 可選取。 有多個原因導致 VNet 呈現灰色，包括：

* VNet 是您的帳戶有權存取的另一個訂用帳戶
* VNet 未啟用點對站功能
* VNet 沒有動態路由閘道

![][2]

若要啟用整合，只需按一下您想要整合的 VNet 即可。 選取 VNet 之後，您的應用程式會自動重新啟動，使變更生效。 

##### <a name="enable-point-to-site-in-a-classic-vnet"></a>在傳統 VNet 中啟用點對站
如果您的 VNet 沒有閘道，也沒有點對站，則您必須先設定它。 若要針對傳統 VNet 執行此動作，請移至 [Azure 入口網站][AzurePortal]，並引出虛擬網路 (傳統) 的清單。 從這裡按一下您想要整合的網路，並按一下稱為 VPN 連線之基本功能下的大型方塊。 從這裡您可以建立點對站 VPN，甚至讓它建立閘道。 在您使用閘道建立體驗完成點對站之後，大約 30 分鐘即可使用。 

![][8]

##### <a name="enabling-point-to-site-in-a-resource-manager-vnet"></a>啟用 Resource Manager VNet 中的點對站
若要為 Resource Manager VNet 設定閘道和「點對站」，可以如以下文件所述使用 PowerShel：[使用 PowerShell 設定虛擬網路的點對站連線][V2VNETP2S]；或使用「Azure 入口網站」，如以下文件所述：[使用 Azure 入口網站設定 VNet 的點對站連線][V2VNETPortal]。 用來執行這項功能的 UI 尚無法使用。 請注意，您不需要建立指向站台設定的憑證。 這會在您將 WebApp 連線至 VNet 時自動設定。 

### <a name="creating-a-pre-configured-vnet"></a>建立預先設定的 VNet
如果您想要建立新的 VNet，以閘道和點對站進行設定，則 App Service 網路 UI 具有功能可以完成這項操作，但是僅適用於 Resource Manager VNet。 如果您想要以閘道和點對站建立 Classic VNet，您需要透過網路使用者介面手動執行。 

若要透過 VNet 整合 UI 建立 Resource Manager VNet，只需選取 [建立新的虛擬網路]，然後提供：

* 虛擬網路名稱
* 虛擬網路位址區塊
* 子網路名稱
* 子網路位址區塊
* 閘道器位址區塊
* 點對站位址區塊

如果您想要此 VNet 連接到任何其他網路，您應該避免挑選與這些網路重疊的 IP 位址空間。 

> [!NOTE]
> 使用閘道建立 Resource Manager VNet 大約需要 30 分鐘，目前無法整合 VNet 與您的應用程式。 使用閘道建立 VNet 之後，您必須回到您的應用程式 VNet 整合 UI，並選取新的 VNet。
> 
> 

![][3]

通常，Azure VNet 是在私人網路位址內建立。 根據預設，VNet 整合功能會將任何以這些 IP 位址範圍為目標的流量路由傳送至您的 VNet。 私人 IP 位址範圍如下：

* 10.0.0.0/8 - 如同 10.0.0.0 - 10.255.255.255
* 172.16.0.0/12 - 如同 172.16.0.0 - 172.31.255.255 
* 192.168.0.0/16 - 如同 192.168.0.0 - 192.168.255.255

VNet 位址空間需要以 CIDR 標記法指定。 如果您不熟悉 CIDR 標記法，它是使用 IP 位址和代表網路遮罩之整數來指定位址區塊的方法。 做為快速參考，請考慮 10.1.0.0/24 將是 256 個位址，而 10.1.0.0/25 將是 128 個位址。 搭配 /32 的 IPv4 位址將只是 1 個地址。 

如果您在這裡設定 DNS 伺服器資訊，則該資訊是針對您的 VNet 而設定的。 在建立 VNet 之後，您可以根據 VNet 使用者體驗編輯此資訊。 如果您變更 VNet 的 DNS，則需要執行「同步網路」作業。

當您使用 VNet 整合 UI 建立 Classic VNet 時，它會在與您的應用程式相同的資源群組中建立 VNet。 

## <a name="how-the-system-works"></a>系統的運作方式
此功能實際上組建在點對站 VPN 技術之上，以將您的應用程式連接到您的 VNet。 Azure App Service 中的應用程式具備多租用戶的系統架構，其會防止在 VNet 中直接佈建應用程式，就像使用虛擬機器所做的一樣。 藉由以點對站技術為基礎來進行建置，我們得以將網路存取限制為僅限裝載應用程式的虛擬機器。 在這些應用程式主機上，我們更進一步限制網路的存取權限，因此應用程式只能存取您設定為供其存取的網路。 

![][4]

如果您尚未設定虛擬網路的 DNS 伺服器，您的應用程式需要使用 IP 位址才能觸及 VNet 中的資源。 在使用 IP 位址時，請記住此功能的主要優點在於它可讓您在私人網路內使用私人位址。 如果將應用程式設為使用其中一個 VM 的公用 IP 位址，則您不是使用 VNet 整合功能，而是透過網際網路進行通訊。

## <a name="managing-the-vnet-integrations"></a>管理 VNet 整合功能
要在應用程式層級上，才能連接或中斷連接 VNet。 可在多個應用程式之間影響 VNet 整合的作業是在 ASP 層級上。 從顯示在應用程式層級的 UI 中，您可以取得 VNet 的詳細資料。 大部分相同的資訊也會顯示在 ASP 層級。 

![][5]

從 [網路功能狀態] 頁面中，您可以看到應用程式是否已連接到 VNet。 無論您的 VNet 閘道基於何種原因關閉，此狀態將顯示為未連接。 

現在可供您在應用程式層級 VNet 整合 UI 中使用的資訊，與您從 ASP 取得的詳細資訊相同。 這些項目如下：

* VNet 名稱 - 此連結會開啟 Azure 虛擬網路 UI
* 位置 - 這會反映 VNet 的位置。 可能與另一個位置中的 VNet 整合。
* 憑證狀態 - 有若干憑證，用來保護應用程式與 VNet 之間的 VPN 連線。 這會反映測試，以確保它們保持同步。
* 閘道狀態 - 無論您的閘道基於何種原因關閉，您的應用程式將無法存取 VNet 中的資源。 
* VNet 位址空間 - 這是 VNet 的 IP 位址空間。 
* 點對站位址空間 - 這是 VNet 的點對站 IP 位址空間。 您的應用程式會顯示來自此位址空間的其中一個 IP 的通訊。 
* 站對站位址空間：您可以使用站對站 VPN，將 VNet 連線到內部部署資源或連線到其他 VNet。 如果您已如此設定，則以該 VPN 連線定義的 IP 範圍會顯示在這裡。
* DNS 伺服器 - 如果您已設定 DNS 伺服器與 VNet 搭配，則它們會列示在這裡。
* 路由傳送至 VNet 的 IP - 有一個 IP 位址清單，您的 VNet 已定義將路由傳送至這些 IP 位址，這些位址會顯示在這裡。 

您可以在 VNet 整合的應用程式檢視中採取的唯一作業，就是中斷連接目前連接到 VNet 的應用程式。 若要這樣做，只需按一下頂端的 [中斷連接] 即可。 這個動作不會變更您的 VNet。 VNet 及其組態 (包括閘道) 仍會保持原狀。 如果接著您要刪除 VNet，則需要先刪除其中資源，包括閘道。 

[App Service 方案] 檢視具有一些其他作業。 也可用不同的方式從應用程式中存取它。 若要觸達 ASP 網路功能 UI，只需開啟您的 ASP UI，並向下捲動即可。 有一個稱為網路功能狀態的 UI 元素。 它會提供一些有關 VNet 整合的次要詳細資訊。 按一下此 UI，即會開啟網路功能狀態 UI。 如果接著按一下 [按一下這裡以管理]，會開啟 UI，列出此 ASP 中的 VNet 整合。

![][6]

當查看您要整合之 VNet 的位置時，ASP 的位置很好記。 當 VNet 在另一個位置時，您更有可能發現延遲問題。 

整合的 VNet 提醒您，您的應用程式已在此 ASP 與多少個 VNet 整合，以及您可以具有多少個。 

若要查看每個 VNet 新增的詳細資料，只需按一下您感興趣的 VNet 即可。 除了先前提到的詳細資料外，您還會在此 ASP 中看到正在使用該 VNet 之應用程式的清單。 

關於動作，有兩個主要動作。 第一個動作能夠新增路由，驅使流量離開您的應用程式進入 VNet。 第二個動作能夠同步處理憑證和網路資訊。

![][7]

**路由** 如先前所述，VNet 中所定義的路由用於將應用程式中的流量導向至 VNet。 還有一些用途，就是客戶想要將額外的輸出流量從應用程式傳送到 VNet，但已對他們提供此功能。 傳送後流量發生什麼情況取決於客戶如何設定其 VNet。 

**憑證** 憑證狀態反映 App Service 執行的檢查，此檢查用來驗證用於 VPN 連線的憑證是否依然完好。 啟用 VNet 整合時，如果這是此 ASP 中的任何應用程式與該 VNet 的第一個整合，則需要交換憑證以確保連線的安全性。 除了憑證以外，我們還得到 DNS 組態、路由，以及其他描述網路的類似項目。
如果這些憑證或網路資訊已變更，您需要按一下 [同步處理網路]。 **注意**：按一下 [同步網路] 時，會導致應用程式與 VNet 之間的連線短暫中斷。 如果應用程式未重新啟動，失去連線會導致您的網站無法正常運作。 

## <a name="accessing-on-premises-resources"></a>存取內部部署資源
VNet 整合功能的優點之一是，如果 VNet 以站對站 VPN 連線到內部部署網路，應用程式就可以從應用程式中存取內部部署資源。 但若要以此方式運作，您可能需要以點對站 IP 範圍的路由來更新內部部署 VPN 閘道。 第一次設定站對站 VPN 時，用來設定它的指令碼應該設定路由，包括點對站 VPN。 如果在建立站對站 VPN 之後新增點對站 VPN，您需要手動更新路由。 此做法的詳細資料會根據閘道而有所不同，不在這裡詳述。 

> [!NOTE]
> VNet 整合功能不會將應用程式與具有 ExpressRoute 閘道的 VNet 整合。 即使是在[共存模式][VPNERCoex]中設定 ExpressRoute 閘道，VNet 整合仍無法運作。 如果您需要透過 ExpressRoute 連線存取資源，則可使用在您 VNet 中執行的 [App Service 環境][ASE]。
> 
> 

## <a name="pricing-details"></a>價格詳細資料
有幾個您在使用 VNet 整合功能時應該注意的價格細微差別。 有 3 個與使用此功能相關的費用：

* ASP 定價層需求
* 資料傳輸成本
* VPN 閘道器成本

您的應用程式若要能夠使用此功能，它們必須位於標準或進階 App Service 方案中。 您可以在這裡看到這些成本的詳細資料：[App Service 價格][ASPricing]。 

由於處理點對站 VPN 的方式，您必須付費，才能透過 VNet 整合連線輸出資料，即使 VNet 位於相同的資料中心也一樣。 若要查看這些花費，請參閱這裡：[資料傳輸定價詳細資料][DataPricing]。 

最後一個項目就是 VNet 閘道的成本。 如果對其他項目 (例如站對站 VPN) 您不需要閘道，表示您的付費是讓閘道支援 VNet gateway 整合功能。 這裡有這些成本的詳細資料：[VPN 閘道器價格][VNETPricing]。 

## <a name="troubleshooting"></a>疑難排解
儘管功能易於設定，這不表示您的體驗不會遇到問題。 如果您在存取所需端點時遇到問題，有一些公用程式，您可以用來從應用程式主控台測試連線功能。 有兩個您可以使用的主控台體驗。 一個是從 Kudu 主控台，另一個則是您可以在 Azure 入口網站觸達的主控台。 若要從您的應用程式前往 Kudu 主控台，請移至 [工具] -> [Kudu]。 這與移至 [sitename].scm.azurewebsites.net 相同。 一旦開啟，只需移至 [偵錯主控台] 索引標籤即可。若要前往 Azure 入口網站裝載的主控台，請從您的應用程式移至 [工具] -> [主控台]。 

#### <a name="tools"></a>工具
由於安全性限制，工具 ping、nslookup 和 tracert 無法透過主控台運作。 為了填滿此空隙，已加入兩個不同的工具。 為了測試 DNS 功能，已加入名為 nameresolver.exe 的工具。 語法為：

    nameresolver.exe hostname [optional: DNS Server]

您可以使用 nameresolver 來檢查應用程式依賴的主機名稱。 如此一來您可以測試是否有任何項目未正確設定，而無法與 DNS 搭配，或可能對 DNS 伺服器沒有存取權。

下一個工具可讓您測試主機是否可與 TCP 連線，以及連接埠組合。 此工具稱為 tcpping.exe，語法如下：

    tcpping.exe hostname [optional: port]

tcpping 公用程式會讓您知道是否可觸達特定主機和連接埠。 只有在下列情況才會顯示成功：有一個應用程式監聽主機和連接埠組合，並且有網路從您的應用程式存取到指定的主機和連接埠。

#### <a name="debugging-access-to-vnet-hosted-resources"></a>偵錯 VNet 裝載資源的存取
有一些事物，可以阻止您的應用程式觸達特定的主機和連接埠。 大部分的情況下，會是下列三個情況的其中一種︰

* **路線中有防火牆** 如果路線中有防火牆，則將會達到 TCP 逾時。 此案例中就是 21 秒。 使用 tcpping 工具來測試連線能力。 TCP 逾時可能是因為許多項目越過防火牆並啟動。 
* **DNS 無法存取** DNS 逾時值為三秒 (每部 DNS 伺服器)。 如果您有兩部 DNS 伺服器，逾時為 6 秒。 使用 nameresolver 來檢查 DNS 是否運作。 請記住，您不能使用 nslookup，因為它不會使用您的 VNet 設定使用的 DNS。
* **無效的 P2S IP 範圍** 點對站 IP 範圍需要在 RFC 1918 私人 IP 範圍中 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255)。 如果範圍中使用的 IP 不在其中，則無法正常運作。 

如果這些項目沒有回答您的問題，請先確認基本問題，例如︰ 

* 閘道是否顯示為正在入口網站中啟動？
* 憑證是否顯示為同步中？
* 是否有任何人未在受影響的 ASP 中執行 [同步處理網路] 的情況下變更網路組態？ 

如果您的閘道已關閉，請重新啟動。 如果您的憑證未同步，請移至 VNet 整合的 ASP 檢視，並點擊 [同步網路]。 如果您懷疑已對 VNet 組態做了變更，而它未與 ASP 同步，請移至 VNet 整合的 ASP 檢視，並點擊 [同步網路]。只是提醒您，這會導致 VNet 與應用程式的連線短暫中斷。 

如果一切都沒問題，您需要更深入發掘問題：

* 是否有任何其他使用 VNet 整合來觸達相同 VNet 中資源的應用程式？ 
* 您是否可以移至應用程式主控台，並使用 tcpping 觸達 VNet 中的任何其他資源？ 

如果上述任一項成立，表示 VNet 整合沒問題，問題出在其他地方。 此情況將更有挑戰性，因為沒有簡單的方法，來了解為何無法觸達主機:連接埠。 部分原因包括：

* 您已在主機上啟動防火牆，防止從點對站 IP 範圍存取應用程式連接埠。 跨子網路通常需要公用存取權。
* 目標主機已關閉
* 應用程式已關閉
* IP 或主機名稱錯誤
* 應用程式不是接聽您預期的連接埠。 您可以移至該主機，並從命令提示字元使用 "netstat -aon" 來檢查此問題。 這會顯示哪個處理程序識別碼正在接聽哪個連接埠。 
* 您配置網路安全性群組的方式，讓這些群組防止從點對站 IP 範圍存取應用程式主機和連接埠

請記住，您不知道應用程式將使用點對站 IP 範圍中的哪個 IP，因此您必須允許從整個範圍存取。 

其他偵錯步驟包括：

* 登入 VNet 中的另一個 VM，並嘗試從該處觸達資源 host:port。 有一些您可以基於此用途使用的 TCP ping 公用程式，或者甚至需要時，也可使用 telnet。 這裡的用途只是判斷是否可從這個其他 VM 連接到該處。 
* 啟動另一個 VM 上的應用程式，並從主控台測試是否可從應用程式存取該主機和連接埠

#### <a name="on-premises-resources"></a>內部部署資源 ####
如果您的應用程式無法觸達內部部署的資源，則首先應該檢查是否可以觸達 VNet 中的資源。 如果可以運作，請嘗試從 VNet 中的 VM 嘗試觸達內部部署應用程式。 您可以使用 telnet 或 TCP ping 公用程式。 如果 VM 無法觸達內部部署資源，請確定站對站 VPN 連線正在運作中。 如果正在運作中，接著檢查先前提到的相同事項，以及內部部署閘道組態和狀態。 

現在，如果 VNet 裝載的 VM 可以觸達您的內部部署系統，但您的應用程式無法觸達此系統，則很可能是下列其中一個原因：

* 內部部署閘道中未以您的點對站 IP 範圍設定路由
* 網路安全性群組已封鎖點對站 IP 範圍的存取
* 內部部署防火牆已封鎖來自點對站 IP 範圍的流量
* 您在 VNet 中有使用者定義的路由 (UDR) 阻止點對站的流量觸達您的內部部署網路

## <a name="powershell-automation"></a>PowerShell 自動化

您可以使用 PowerShell 的 Azure 虛擬網路整合應用程式服務。 針對已備妥的執行指令碼，請參閱[Azure App Service 中的應用程式連接到 Azure 虛擬網路](https://gallery.technet.microsoft.com/scriptcenter/Connect-an-app-in-Azure-ab7527e3)。

## <a name="hybrid-connections-and-app-service-environments"></a>混合式連線和 App Service 環境
有三個可讓您存取 VNet 裝載之資源的功能。 如下：

* VNet 整合
* 混合式連線
* App Service 環境

混合式連線需要您在網路中安裝稱為混合式連線管理員 (HCM) 的轉送代理程式。 HCM 必須同時能夠連接至 Azure 和您的應用程式。 此解決方案特別適合遠端網路，例如內部部署網路，或甚至是另一個雲端裝載的網路，因為它不需要網際網路可存取的端點。 HCM 只在 Windows 上執行，而且您最多可有五個執行個體同時執行，以提供高可用性。 雖然混合式連線只支援 TCP，但是每個 HC 端點必須符合特定的主機:連接埠組合。 

App Service 環境功能可讓您在 VNet 中執行 Azure App Service 的執行個體。 這可讓應用程式無需任何額外的步驟，即可存取 VNet 中的資源。 App Service 環境的好處還有您可以搭配最多 14 GB 的 RAM 使用 Dv2 式背景工作角色。 另一個好處是您可以調整系統以符合您的需求。 與 ASP 受限於 20 個執行個體的多租用戶環境不同，在 ASE 中，您可以相應增加到 100 個 ASP 執行個體。 VNet 整合無法辦到，但 ASE 辦得到的其中一件事是，App Service 環境可以使用 ExpressRoute VPN。 

儘管有使用案例重疊的情況，但這些功能無法取代彼此。 知道使用哪個功能取決於您的需求。 例如︰

* 如果您是開發人員，而且只是想要在 Azure 中執行網站，並讓它可存取辦公桌下工作站上的資料庫，則最簡單的方式就是使用混合式連線。 
* 如果您是想要將大量 Web 內容放在公用雲端，並在自己的網路中管理它們的大型組織，則您會想要使用 App Service 環境。 
* 如果您有許多 App Service 裝載的應用程式，而且只想要存取 VNet 中的資源，則 VNet 整合是最好的選擇。 

除了使用案例以外，還有一些簡單相關層面。 如果 VNet 已經連線到內部部署網路，則使用 VNet 整合或 App Service 環境是取用內部部署資源的簡單方法。 另一方面，如果 VNet 未連線到內部部署網路，則相較於安裝 HCM，搭配您的 VNet 設定站對站 VPN，需要更多的額外負荷。 

除了功能差異以外，還有價格差異。 App Service 環境功能是進階服務供應項目，除了其他很棒的功能外，還提供最多的網路組態可能性。 VNet 整合可與標準或進階 ASP 搭配使用，並非常適合從多租用戶 App Service 安全取用 VNet 中的資源。 混合式連線目前取決於 BizTalk 帳戶，此帳戶具有的價格層級，從一開始免費，然後根據您需要的數量而越發昂貴。 不過，當在許多網路之間工作時，沒有其他功能像混合式連線一樣，可讓您存取超過 100 個不同網路中的資源。 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[ASEintro]: environment/intro.md
[ILBASE]: environment/create-ilb-ase.md
[V2VNETPortal]: ../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md
[VPNERCoex]: ../expressroute/expressroute-howto-coexist-resource-manager.md
[ASE]: environment/intro.md
