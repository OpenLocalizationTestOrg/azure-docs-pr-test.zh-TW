---
title: "aaaIntegrate 與 Azure 虛擬網路的應用程式"
description: "為您示範如何 tooconnect Azure App Service tooa 新的或現有 Azure 虛擬網路中的應用程式"
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
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>將您的應用程式與 Azure 虛擬網路整合
本文件說明 hello Azure App Service 虛擬網路整合功能，並顯示如何 tooset 它與應用程式中[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。 如果您不熟悉 Azure 虛擬網路 (Vnet)，這是一種功能，可讓您 tooplace 許多非網際網路 routeable 網路而您控制在您的 Azure 資源存取權。 這些網路接著可以使用各種不同的 VPN 技術 tooyour 連線在內部部署網路。 深入了解 Azure 虛擬網路，toolearn 開頭 hello 的相關資訊： [Azure 虛擬網路概觀][VNETOverview]。 

hello Azure App Service 中有兩種形式。 

1. hello 多租用戶系統支援 hello 完整的定價方案
2. hello 應用程式服務環境 (ASE) premium 功能，可部署到您的 VNet。 

本文會演練 VNet 整合和非 App Service 環境。 如果您想深入了解 hello ASE 功能 toolearn，開頭 hello 的相關資訊： [App Service 環境簡介][ASEintro]。

VNet 整合提供您的 web 應用程式存取 tooresources 虛擬網路中，但是不授予私用存取 tooyour web 應用程式從 hello 虛擬網路。 私用的站台存取，是指 toomaking 您只可從私人網路存取這類從 Azure 虛擬網路內的應用程式。 只有使用透過內部負載平衡器 (ILB) 設定的 ASE 才可使用私人網站存取。 如需使用 ILB ase 中的詳細資訊，開始及 hello 文件：[建立和使用 ILB ASE][ILBASE]。 

常見的案例，您會使用 VNet 整合正在啟用您的 web 應用程式 tooa 資料庫或 Azure 虛擬網路中的虛擬機器上執行的 web 服務存取。 使用 VNet 整合您的應用程式不需要的 tooexpose 公用端點 VM 上，但可以改用 hello 私用非網際網路可路由傳送位址。 

hello VNet 整合功能：

* 需要「標準」、「進階」或「隔離」價格方案 
* 使用傳統 VNet 或 Resource Manager VNet 使用傳統或 Resource Manager VNet 
* 支援 TCP 和 UDP
* 使用 Web、行動及 API 應用程式
* 可讓應用程式 tooconnect tooonly 1 一次的 VNet
* 可讓向上 toofive Vnet toobe 與整合在 App Service 方案 
* 可讓應用程式服務計劃中的多個應用程式所使用的相同的 VNet toobe hello
* 支援 hello VNet 閘道因為 toohello SLA 99.9%SLA

VNet 整合不支援的事項包括：

* 掛接磁碟機
* AD 整合 
* NetBios
* 私人網站存取

### <a name="getting-started"></a>開始使用
連接 web 應用程式 tooa 虛擬網路之前，請注意以下是一些事情 tookeep:

* VNet 整合僅會使用**標準**、**進階**或**隔離**價格方案中的應用程式。 如果您啟用 hello 功能，然後調整 不支援您的應用程式服務方案 tooan 定價計劃您的應用程式會遺失其連線 toohello 他們使用的 Vnet。 
* 如果您的目標虛擬網路已經存在，它必須啟用動態路由閘道後才能連接的 tooan 應用程式的點對站 VPN。 如果您以靜態路由設定閘道，便無法啟用點對站的虛擬私人網路 (VPN)。
* hello VNet 必須在 hello 您應用程式服務 Plan(ASP) 相同訂用帳戶。 
* hello 與 VNet 整合的應用程式使用 hello 指定該 vnet 的 DNS。
* 根據預設應用程式整合僅路由傳送流量至 VNet 的 VNet 中定義的 hello 路由為基礎。 

## <a name="enabling-vnet-integration"></a>啟用 VNet 整合
本文件著重於使用 VNet 整合 hello Azure 入口網站。 tooenable VNet 整合與您的應用程式使用 PowerShell，請遵循此處 hello 方向：[您應用程式 tooyour 虛擬網路連線使用 PowerShell][IntPowershell]。

您擁有 hello 選項 tooconnect 您應用程式 tooa 新的或現有的虛擬網路。 如果您建立新的網路，您的整合的一部分，此外 toojust 建立 hello VNet、 動態路由閘道已預先設定為您然後點 tooSite VPN 已啟用。 

> [!NOTE]
> 設定新的虛擬網路整合可能需要幾分鐘的時間才能完成。 
> 
> 

tooenable VNet 整合，開啟您的應用程式設定，然後選取 網路功能。 開啟 UI hello 提供三個網路的選項。 本指南只探討 VNet 整合，但本文件稍後會討論混合式連接和 App Service 環境。 

如果您的應用程式不在 hello 正確定價方案中，hello UI 可讓您 tooscale 高定價您選擇的計劃您計劃 tooa。

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>啟用與既存的 VNet 的 VNet 整合
hello VNet 整合 UI 可讓您 tooselect 從 Vnet 的清單。 hello 傳統 Vnet 表示它們的這類 hello 字 [傳統] 5d 下一步 toohello VNet 名稱括號中。 hello 清單排序，hello Vnet 資源管理員會先列出。 在 hello 下面顯示的影像所見，可以選取單一 VNet。 有多個原因導致 VNet 呈現灰色，包括：

* hello VNet 位於您的帳戶具有存取權的另一個訂用帳戶
* 沒有啟用點 tooSite hello VNet。
* hello VNet 沒有動態路由閘道

![][2]

只要按一下 hello VNet 想與 toointegrate tooenable 整合。 選取 hello VNet 後，您的應用程式會自動重新啟動 hello 變更 tootake 效果。 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>啟用在傳統的 VNet 中的點 tooSite
如果您的 VNet 沒有閘道，也有點 tooSite，則必須 tooset 的最新的第一個。 此作業對於傳統的 VNet，請移 toodo toohello [Azure 入口網站][ AzurePortal]並顯示 hello 虛擬 Networks(classic) 清單。 從這裡開始，按一下您想與 toointegrate 並稱為 VPN 連線的 Essentials 底下 hello 大方塊上按一下 hello 網路上。 從這裡，您可以建立點 toosite VPN 及甚至可將它建立閘道。 之後您瀏覽 hello 點 toosite 閘道建立體驗是大約 30 分鐘才能開始。 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>啟用資源管理員 VNet 中的點 tooSite
tooconfigure 點 tooSite 的閘道與資源管理員 VNet，您可以使用 PowerShell 所述，[設定點對站連線 tooa 虛擬網路使用 PowerShell] [ V2VNETP2S]所述，使用 hello Azure 入口網站或[設定點對站連線 tooa VNet 使用 hello Azure 入口網站][V2VNETPortal]。 hello UI tooperform 這項功能尚無法使用。 請注意，您需要 toocreate 憑證 hello 點 tooSite 組態。 當您連接您 WebApp toohello VNet 時這會自動設定的。 

### <a name="creating-a-pre-configured-vnet"></a>建立預先設定的 VNet
如果您想 toocreate 新的 VNet 設定閘道和點對站，則 hello 網路 UI 的應用程式服務 hello 功能 toodo，但只供資源管理員 VNet。 如果您希望 toocreate 傳統 VNet 閘道點對站台，然後您需要 toodo 此手動透過 hello 網路使用者介面。 

只需選取 toocreate 透過 hello VNet 整合 UI，資源管理員 VNet**建立新的虛擬網路**並提供:

* 虛擬網路名稱
* 虛擬網路位址區塊
* 子網路名稱
* 子網路位址區塊
* 閘道器位址區塊
* 點對站位址區塊

如果您希望此 VNet tooconnect tooany 其他網路，您應該避免與這些網路重疊的 IP 位址空間一樣被挑選。 

> [!NOTE]
> 資源管理員 VNet 建立閘道約需 30 分鐘，和目前不會整合 hello VNet 與您的應用程式。 VNet 建立 hello 閘道之後您會需要 toocome 後 tooyour 應用程式 VNet 整合 UI，並選取新的 VNet。
> 
> 

![][3]

通常，Azure VNet 是在私人網路位址內建立。 依預設 hello VNet 整合功能可路由傳送到您的 VNet 指向這些 IP 位址範圍的任何流量。 hello 私人 IP 位址範圍為：

* -這是 hello 相同為 10.0.0.0，-10.0.0.0/8 10.255.255.255
* -這是 hello 相同為 172.16.0.0-172.16.0.0/12 172.31.255.255 
* 192.168.0.0/16-這是 hello 相同為 192.168.0.0-192.168.255.255

hello VNet 位址空間必須以 CIDR 表示法指定 toobe。 如果您不熟悉使用 CIDR 表示法，它是方法，以指定使用的 IP 位址和整數，表示 hello 網路遮罩的位址區塊。 做為快速參考，請考慮 10.1.0.0/24 將是 256 個位址，而 10.1.0.0/25 將是 128 個位址。 搭配 /32 的 IPv4 位址將只是 1 個地址。 

如果您在此處設定 hello DNS 伺服器資訊，然後，設定您的 VNet。 VNet 建立後，您可以編輯 hello VNet 的使用者經驗的這項資訊。 如果您變更 hello 的 hello VNet DNS 時，您需要 tooperform 同步網路作業。

當您建立使用 VNet 整合 UI hello 傳統 VNet 時，它會在 hello 建立 VNet 相同資源群組的應用程式。 

## <a name="how-hello-system-works"></a>Hello 系統的運作方式
Hello 幕後這項功能建置在點對站 VPN 技術 tooconnect 之上您應用程式 tooyour VNet。 Azure App Service 中的應用程式具備多租用戶的系統架構，其會防止在 VNet 中直接佈建應用程式，就像使用虛擬機器所做的一樣。 藉由建立點對站台技術，我們會限制網路存取 toojust hello 主控虛擬機器 hello 應用程式。 網路存取 toohello 進一步限制在這些應用程式主機上，讓您的應用程式只能存取，您將其設定 tooaccess hello 網路。 

![][4]

如果您尚未設定 DNS 伺服器與虛擬網路，您的應用程式需要 toouse hello VNet 的 IP 位址 tooreach 資源。 在使用 IP 位址，請記住 hello 的這項功能的主要優點是，它可讓您在私人網路內 toouse hello 私人位址。 如果您在您不使用 hello VNet 整合功能，並且透過進行通訊 toouse 註冊您的應用程式的公用 IP 位址設定的其中一個 Vm，hello 網際網路。

## <a name="managing-hello-vnet-integrations"></a>管理 hello VNet 整合
hello 能力 tooconnect，並中斷連線的 tooa VNet 位於應用程式層級。 可能會影響多個應用程式的 hello VNet 整合作業是在 ASP 層級。 從 hello 顯示 hello 應用程式層級的 UI，您可以取得詳細資訊，在您的 VNet。 大部分的 hello 相同的資訊也會顯示在 hello ASP 層級。 

![][5]

從 hello 網路功能的狀態 頁面上，您可以看到您的應用程式是否已連線的 tooyour VNet。 無論您的 VNet 閘道基於何種原因關閉，此狀態將顯示為未連接。 

現在您有可用的 tooyou hello 應用程式層級的 VNet 整合 UI 是以 hello 詳細資訊，您會收到 hello ASP hello 相同的 hello 資訊。 這些項目如下：

* VNet 名稱-這個連結會開啟 hello Azure 虛擬網路 UI
* 位置-這反映出您的 VNet hello 位置。 可能與另一個位置中的 VNet toointegrate 它。
* 憑證狀態-沒有使用憑證 toosecure hello hello 應用程式與 hello VNet 之間的 VPN 連線。 這會反映測試 tooensure 同步。
* 閘道狀態-您的閘道應該因故然後應用程式無法存取 hello VNet 中的資源。 
* VNet 位址空間-這是您的 VNet hello IP 位址空間。 
* 點 tooSite 位址空間-這是您的 vnet hello 點 toosite IP 位址空間。 您的應用程式會顯示來自一個 hello 這個位址空間中的 Ip 通訊。 
* 站台 toosite 位址空間-您可以使用站台 tooSite Vpn tooconnect VNet tooyour 內部資源或 tooother VNet。 您應該有設定則 hello IP 範圍定義的 VPN 連線，這裡顯示。
* DNS 伺服器 - 如果您已設定 DNS 伺服器與 VNet 搭配，則它們會列示在這裡。
* Ip 路由傳送 toohello VNet-有一份您的 VNet 已路由，定義的 IP 位址，這些位址顯示在這裡。 

您可在您的 VNet 整合 hello 應用程式檢視中的 hello 唯一作業是的 toodisconnect 應用程式從 hello 目前連接到的 VNet。 toodo 只需按一下 中斷連線在 hello 最上方。 這個動作不會變更您的 VNet。 hello VNet 和其組態，包括 hello 閘道維持不變。 如果您想 toodelete VNet，您會需要 toofirst 刪除 hello 資源包括 hello 閘道。 

hello App Service 方案檢視有其他的作業數目。 它也以不同的方式比從存取 hello 應用程式。 您的 ASP UI 和向下的捲動，只要開啟 tooreach hello ASP 網路功能的 UI。 有一個稱為網路功能狀態的 UI 元素。 它會提供一些有關 VNet 整合的次要詳細資訊。 按一下此 UI，就會開啟 hello 網路功能狀態的 UI。 如果您按一下 on"按一下這裡 toomanage"，hello 列出在這個 ASP VNet 整合開啟的 hello 的 UI。

![][6]

hello ASP hello 位置是很好的 tooremember，查看 hello hello 要整合的 Vnet 位置時。 在另一個位置 hello VNet 時也更可能 toosee 延遲問題。 

hello Vnet 與整合是在此 ASP，而且您可以有多少與整合您的應用程式上多少的 Vnet 提醒。 

toosee 上每個 VNet，直接按一下 hello 您感興趣的 VNet 上加入詳細資料。 此外 toohello 先前說明的詳細資訊，您可以參閱 hello 應用程式在此 ASP 中使用該 VNet 的清單。 

關於 tooactions 有這兩個主要動作。 hello 第一個是磁碟機離開您的應用程式到您的 VNet 流量的 hello 能力 tooadd 路由。 hello 第二個動作是 hello 能力 toosync 憑證和網路資訊。

![][7]

**路由**如前文所述定義 VNet 中的 hello 路由是用途將流量導向到您的 VNet，從您的應用程式。 雖然 hello VNet 和他們的客戶希望 toosend 額外傳出的流量從應用程式會提供這項功能，有一些用法。 會發生什麼事 toohello 流量之後，已啟動 toohow hello 客戶設定其 VNet。 

**憑證**hello 憑證狀態反映出 hello App Service toovalidate hello VPN 連線使用我們的 hello 憑證時仍值得所執行的檢查。 VNet 整合啟用時，如果這是 hello 第一個整合 toothat VNet 從這個 ASP，在任何應用程式就 hello 連線的憑證 tooensure hello 安全性需要的 exchange。 Hello 憑證以及我們取得 hello DNS 設定、 路由和其他類似的項目描述 hello 網路。
如果變更這些憑證或網路資訊，您需要 tooclick 「 同步處理網路 」。 **注意**：按一下 [同步網路] 時，會導致應用程式與 VNet 之間的連線短暫中斷。 無法重新啟動您的應用程式，而 hello 失去連線能力可能會導致您的站台 toonot 函式正確。 

## <a name="accessing-on-premises-resources"></a>存取內部部署資源
Hello hello VNet 整合功能的好處是，如果您的 VNet 連接 tooyour 內部網路站台 tooSite VPN 則您的應用程式可以從您的應用程式存取 tooyour 在內部部署資源。 針對此 toowork 但您可能需要 tooupdate hello 與您在內部部署 VPN 閘道會路由傳送您點 tooSite IP 範圍。 Hello 網站 tooSite VPN 第一次設定時使用 tooconfigure hello 指令碼，則它應該設定包括點 tooSite VPN 的路由。 如果您建立您的站台 tooSite VPN 之後，您可以加入 hello 點 tooSite VPN，則您需要 tooupdate hello 路由以手動方式。 閘道而有所不同，並不是 toodo 述詳細資料。 

> [!NOTE]
> hello VNet 整合功能不會與具有 ExpressRoute 閘道 VNet 整合應用程式。 即使 hello ExpressRoute 閘道設定中[共存模式][ VPNERCoex] hello VNet 整合無法運作。 如果您需要 tooaccess 資源，透過 ExpressRoute 連線，則您可以使用[App Service 環境][ASE]，這會在您的 VNet 中執行。
> 
> 

## <a name="pricing-details"></a>價格詳細資料
一些定價細節，您應該了解使用 hello VNet 整合功能時。 有 3 相關的費用 toohello 使用這項功能：

* ASP 定價層需求
* 資料傳輸成本
* VPN 閘道器成本

您的應用程式 toobe 無法 toouse 這項功能，它們需要 toobe Standard 或 Premium App Service 方案中的。 您可以在這裡看到這些成本的詳細資料：[App Service 價格][ASPricing]。 

Toohello 方式點 tooSite Vpn 的處理，因為一定需要付費透過 VNet 整合連線的傳出資料即使 hello VNet 中 hello 相同的資料中心。 toosee 那些要收費的是，看看這裡：[資料傳輸定價詳細資料][DataPricing]。 

hello 最後一個項目是 hello 成本 hello VNet 閘道。 如果您不需要 hello 閘道的其他站台 tooSite Vpn 等項目，然後您支付閘道 toosupport hello VNet 整合功能。 這裡有這些成本的詳細資料：[VPN 閘道器價格][VNETPricing]。 

## <a name="troubleshooting"></a>疑難排解
雖然 hello 功能是簡單 tooset 往上，這不表示您的體驗會是可用的問題。 您應該發生存取您所需的端點有問題是一些您可以使用從 hello 應用程式主控台 tootest 連線的公用程式。 有兩個您可以使用的主控台體驗。 一個是從 hello Kudu 主控台和其他 hello 是 hello 主控台，您可能會達到 hello Azure 入口網站中。 tooget toohello Kudu 主控台，從您的應用程式移 tooTools]-> [Kudu。 這是為太移 hello 相同 [sitename]。.scm.azurewebsites.net。 一旦該開啟只需移 toohello 偵錯主控台 索引標籤 tooget toohello Azure 入口網站裝載的主控台再從您的應用程式移 tooTools-> 主控台。 

#### <a name="tools"></a>工具
hello 工具偵測、 nslookup 及 tracert 將無法運作透過 hello 主控台到期 toosecurity 條件約束。 toofill hello void 已加入兩個不同的工具。 在訂單 tootest DNS 功能，我們會加入名為 nameresolver.exe 的工具。 hello 語法為：

    nameresolver.exe hostname [optional: DNS Server]

您可以使用 nameresolver toocheck hello 主機名稱，取決於您的應用程式。 如此一來您可以測試如果您有正確設定您的 DNS 的任何項目，或可能沒有存取 tooyour DNS 伺服器。

hello 下一步 工具可讓您 tootest TCP 連線 tooa 主機和連接埠組合。 此工具會呼叫 tcpping.exe 和 hello 語法是：

    tcpping.exe hostname [optional: port]

hello tcpping 公用程式會告訴您是否可以到達特定主機和連接埠。 只可以顯示成功如果： 沒有接聽 hello 主機和連接埠組合，應用程式，而且沒有從您的應用程式 toohello 指定的主機和連接埠的網路存取權。

#### <a name="debugging-access-toovnet-hosted-resources"></a>偵錯存取 tooVNet 裝載的資源
有一些事物，可以阻止您的應用程式觸達特定的主機和連接埠。 大部分的 hello 時間它是三個項目之一：

* **防火牆正在 hello 方式**如果您有防火牆 hello 的方式，就會叫用 hello TCP 逾時。 此案例中就是 21 秒。 使用 hello tcpping 工具 tootest 連線能力。 TCP 逾時可以是由於在 toomany 防火牆以外的項目，但從那裡開始。 
* **不能存取 DNS** hello DNS 逾時為每一部 DNS 伺服器的三秒。 如果您有兩個 DNS 伺服器，hello 逾時為 6 秒。 如果 DNS 運作，請使用 nameresolver toosee。 請記住，您無法使用 nslookup，因為不使用 hello 與您的 VNet 設定的 DNS。
* **無效的 P2S IP 範圍**hello 點 toosite IP 範圍需要 toobe hello RFC 1918 的私人 IP 範圍中 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255)。 如果 hello 範圍之外，使用的 Ip，項目將無法運作。 

如果這些項目不會回答您的問題，會先查詢 hello 簡單之類的事情： 

* 不顯示為 hello 入口網站註冊 hello 閘道嗎？
* 憑證是否顯示為同步中？
* 任何人都不執行在受影響的 hello Asp 「 同步處理網路 」 情況下變更 hello 網路組態嗎？ 

如果您的閘道已關閉，請重新啟動。 如果您的憑證未同步，然後移 toohello ASP 檢視您的 VNet 整合，並叫用 「 同步處理網路 」。 如果您懷疑已變更 tooyour VNet 組態，而且它未同步處理您 Asp toohello ASP 檢視您的 VNet 整合，並請叫用 「 同步處理網路 」 恰好，好提醒您，這會短暫中斷導致您的 VNet 連接與您的應用程式. 

如果所有作業，不過沒有關係，您需要更深入的位元在 toodig:

* 會那里使用 VNet 整合 tooreach 資源中的其他任何應用程式 hello 相同的 VNet 嗎？ 
* 您可以移 toohello 應用程式主控台並使用 tcpping tooreach VNet 中的任何其他資源嗎？ 

如果 hello 上述其中一項為真，則亦可 VNet 整合和 hello 問題的其他地方。 這是其中到達 toobe 較為困難因為沒有簡單的方式 toosee，為何無法連線到主機： 連接埠。 Hello 原因包括：

* 您最多有防火牆防止存取您的點 toosite IP 範圍從 toohello 應用程式連接埠在主機上。 跨子網路通常需要公用存取權。
* 目標主機已關閉
* 應用程式已關閉
* 您必須 hello 不正確的 IP 或主機名稱
* 應用程式不是接聽您預期的連接埠。 您可以檢查此情形移到該主機並使用"netstat-aon"hello cmd 命令提示字元。 這會顯示哪個處理程序識別碼正在接聽哪個連接埠。 
* 防止存取 tooyour 應用程式主機和連接埠，您的點 toosite IP 範圍從這種方式中所設定的網路安全性群組

請記住，您不知道什麼 IP 在您的應用程式會使用，因此您需要從 hello 整個範圍 tooallow 存取您點 tooSite IP 範圍內。 

其他偵錯步驟包括：

* 登入另一個 VM 在 VNet 和嘗試的 tooreach 您資源的主機： port 從該處。 有一些您可以基於此用途使用的 TCP ping 公用程式，或者甚至需要時，也可使用 telnet。 hello 這裡的用途只是 toodetermine 如果是連線有從這個其他 VM。 
* 啟動另一個 VM 上的應用程式和測試存取 toothat 主機和連接埠，從 hello 主控台，從您的應用程式

#### <a name="on-premises-resources"></a>內部部署資源 ####
如果您的應用程式無法到達資源的內部，您應該檢查 hello 首先是會以可存取資源 VNet 中。 如果此作業有效，請嘗試 tooreach hello 在內部部署應用程式從 hello VNet 中的 VM。 您可以使用 telnet 或 TCP ping 公用程式。 如果您的 VM 無法連線到內部部署資源，然後確定站台 tooSite VPN 連線可運作。 如果它正在運作，請檢查的 hello 相同的工作先前所述以及 hello 在內部部署閘道組態和狀態。 

現在如果您的 VNet 裝載 VM 可以連線到內部部署系統，但您的應用程式無法再 hello 原因，可能是之一 hello 下列：

* 並未在內部部署閘道的 IP 範圍點 toosite 以設定您的路由
* 網路安全性群組會封鎖存取點 tooSite IP 範圍
* 在內部部署防火牆會封鎖您點 tooSite IP 範圍內的流量
* 您的 VNet，避免基礎的點 tooSite 流量接近內部部署網路中有使用者定義 Route(UDR)

## <a name="hybrid-connections-and-app-service-environments"></a>混合式連線和 App Service 環境
有三個功能可用於存取 tooVNet 裝載的資源。 如下：

* VNet 整合
* 混合式連線
* App Service 環境

混合式連線會要求您 tooinstall 呼叫 hello 混合式連線 Manager(HCM) 網路中的轉送代理程式。 hello HCM 需要 toobe 無法 tooconnect tooAzure 以及 tooyour 應用程式。 此解決方案特別適合遠端網路，例如內部部署網路，或甚至是另一個雲端裝載的網路，因為它不需要網際網路可存取的端點。 hello HCM 只會在 Windows 上執行，且您可以向上 toofive 執行 tooprovide 高可用性的執行個體。 混合式連線只支援 TCP 透過和每個 HC 端點擁有 toomatch tooa 特定主機： 連接埠組合。 

hello App Service 環境功能可讓您 toorun hello Azure 應用程式服務的執行個體 VNet 中。 這可讓應用程式無需任何額外的步驟，即可存取 VNet 中的資源。 某些 hello 的 App Service 環境的其他優點是，您可以使用基礎 Dv2 工作者向上 too14 GB 的 RAM。 另一個好處是，您可以調整 hello 系統 toomeet 您的需求。 不同於 hello 多租用戶的環境您 ASP 有限的 too20 執行個體，在 ase 中您可以向上延展 too100 ASP 執行個體。 取得您不使用 VNet 整合 ASE hello 事情之一是 App Service 環境可以使用 ExpressRoute VPN。 

雖然某些使用案例的重疊時，無這些功能可以取代 hello 的任何其他項目。 了解哪些功能 toouse 繫結的 tooyour 需求。 例如：

* 如果您是開發人員只想 toorun Azure 中的站台和一定它存取 hello 桌上、 下 hello 工作站上的資料庫，則 hello 最簡單的事 toouse 是混合式連線。 
* 如果您是針對想 tooput 的大型組織大量的 hello 公用雲端中的 web 屬性，而且在您自己的網路中管理它們，您會想 toogo 以 hello App Service 環境。 
* 如果您有許多應用程式服務的裝載應用程式並只想 tooaccess VNet 中的資源，然後 VNet 整合是 hello 方式 toogo。 

超出 hello 使用案例，有一些簡單相關層面。 如果您的 VNet 已連線 tooyour 內部部署網路，然後使用 VNet 整合或 App Service 環境是 tooconsume 內部部署資源的簡單方法。 Hello 另一方面，如果您的 VNet 不是在連接上 tooyour 在內部部署網路，則站台 toosite 與 VNet 的 VPN 設定更多的負擔 tooset 相較於安裝 hello HCM 很多。 

超越 hello 功能差異，那里也定價的差異。 hello App Service 環境功能是高階服務供應項目提供 hello 但大部分的網路組態可能性此外 tooother 很棒的功能。 VNet 整合可與 Standard 或 Premium Asp，非常適合安全地耗用 hello 多租用戶應用程式服務從 VNet 中的資源。 混合式連線目前取決於 BizTalk 有定價層級開始可用，然後在變得更耗費資源的帳戶會根據您所需要的 hello 金額。 說 tooworking 跨多個網路不過，沒有像混合式連線，可讓您 tooaccess 資源超過 100 個不同的網路的任何其他功能。 

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
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
