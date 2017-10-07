---
title: "aaaHow tooConfigure App Service 環境 v1"
description: "設定、 管理和監視的 hello App Service 環境 v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>設定 App Service 環境 v1

> [!NOTE]
> 這篇文章是關於 hello App Service 環境 v1。  沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
> 

## <a name="overview"></a>概觀
Azure App Service Environment 是由數個主要元件所組成：

* 在 hello App Service 環境中執行的計算資源託管服務
* 儲存體
* 資料庫
* 傳統 (V1) 或 Resource Manager(V2) Azure 虛擬網路 (VNet) 
* 具有執行中的 hello App Service 環境裝載服務之子網路

### <a name="compute-resources"></a>計算資源
您可以使用 hello 計算資源您四個資源集區。  每個 App Service 環境 (ASE) 都有一組前端和 3 個可能的背景工作集區。 您不需要 toouse 所有三個背景工作集區-如果您想，您可以只使用一個或兩個。

hello 資源集區 （「 前端 」 及 「 工作者 」） 中的 hello 主控件不是直接存取 tootenants。 您無法使用遠端桌面通訊協定 (RDP) tooconnect toothem、 變更其佈建或做為它們的系統管理員。

但是您可以設定資源集區的數量和大小。 在 ASE 中，您有 4 個大小選項，標記為 P1 到 P4。 如需大小及其價格的詳細資訊，請參閱 [App Service 價格](../app-service/app-service-value-prop-what-is.md)。
變更 hello 數量或大小稱為調整規模作業。  一次只能執行一項調整作業。

**前端結束**: hello 前端是您的應用程式保留在您 ASE 中的 hello HTTP/HTTPS 端點。 您不會執行工作負載中 hello 前端。

* ASE 是以兩個 P2 開始，這對於開發/測試工作負載及低階生產工作負載而言已經足夠。 我們強烈建議 P3s 的中等 tooheavy 生產工作負載。
* 以中度 tooheavy 生產工作負載，我們建議您至少四個 P3s tooensure 有足夠排程的維護期間發生時執行的前端。 排定的維護活動一次會關閉一個前端。 這會減少維護活動期間整體可用的前端容量。
* 前端可能佔用 tooan 小時 tooprovision。 
* 您應該進一步微調小數位數，請監視 hello CPU 百分比、 記憶體百分比及 hello 前端集區的使用中要求度量。 若是 hello CPU 或記憶體的百分比超過 70%執行 P3s 時，請加入更多的前端。 如果 hello 作用中的要求值平均 too15、 000 too20、 每秒前端 000 要求，您應該也加入更多的前端。 hello 整體目標是 tookeep CPU 和下一個 70%，平均出 toobelow 前端每 15,000 要求執行 P3s 時的使用中要求的記憶體百分比。  

**工作者**: hello 背景工作可以實際執行應用程式。 當您向上延展您的應用程式服務計劃，會用完 hello 中背景工作相關聯背景工作集區。

* 您無法立即新增背景工作。 它們可能會佔用 tooan 小時 tooprovision。
* 調整計算資源的任何集區的 hello 大小需要 < 1 小時內每個更新網域。 ASE 中有 20 個更新網域。 如果您調整 hello 運算大小的 10 個執行個體的背景工作集區時，就無法在 too10 小時 toocomplete。
* 如果您變更 hello hello 計算資源會以背景工作集區的大小，將會導致執行該背景工作集區中的 hello 應用程式的冷啟動。

hello toochange hello 計算資源未執行任何應用程式的背景工作集區大小的最快速方法是：

* Hello 數量工作者 too2 調降規模。  hello 最小值向下調整的 hello 入口網站中的大小為 2。 它會花幾分鐘的時間 toodeallocate 您的執行個體。 
* 選取新運算大小 hello 和執行個體數目。 從這裡開始，它將佔用 too2 小時 toocomplete。

如果您的應用程式需要較大的計算資源大小，您無法利用 hello 先前的指引。 而不是變更 hello hello 背景工作集區大小的裝載這類應用程式，您可以擴展工作者 hello 預期大小的另一個背景工作集區，並移 toothat 集區中的應用程式。

* 建立 hello hello 計算中另一個背景工作集區大小所需的其他執行個體。 這將佔用 tooan 小時 toocomplete。
* 重新指派您裝載 hello 應用程式需要較大的大小 toohello 新設定背景工作集區的應用程式服務計劃。 這是快速的作業，花費時間小於一分鐘 toocomplete。  
* 如果您不再需要這些未使用的執行個體，規模 hello 第一個背景工作集區。 此作業需要幾分鐘的時間 toocomplete。

**自動調整**： 其中一個 hello 工具，可協助您 toomanage 計算的資源耗用量是自動調整。 您可以針對前端或背景工作集區執行自動調整。 您可以在 hello 早上執行像是增加您任何的集區類型的執行個體，並減少 hello 晚上。 或背景工作集區中可用的背景工作的 hello 數目低於特定臨界值時，可能加入執行個體。

如果您想 tooset 自動調整規模規則計算資源集區的度量，則請記得 hello 時間保留該佈建要求。 如需自動調整應用程式服務環境的詳細資訊，請參閱[如何在 App Service 環境中的自動調整規模 tooconfigure][ASEAutoscale]。

### <a name="storage"></a>儲存體
每個 ASE 各設有 500 GB 的儲存體。 跨所有 hello ASE 中的 hello 應用程式會使用這個空間。 此儲存體空間屬於 hello ASE，目前無法切換的 toouse 您的儲存空間。 如果您正在調整 tooyour 虛擬網路的路由或安全性，您需要 toostill 允許存取 tooAzure 儲存體-或 hello ASE 無法運作。

### <a name="database"></a>資料庫
hello 資料庫會保留定義 hello 環境以及 hello hello 會在其中執行的應用程式的詳細資料的 hello 資訊。 過，這會是 hello 持有的 Azure 訂用帳戶的一部分。 它不是您有直接的能力 toomanipulate 的東西。 如果您正在調整 tooyour 虛擬網路的路由或安全性，您需要 toostill 允許存取 tooSQL Azure--或 hello ASE 無法運作。

### <a name="network"></a>網路
hello 與您 ASE 搭配使用 VNet 可以是您建立 hello ASE 時您所做的其中一個或事先您所做的其中一個。 當您在 ASE 建立期間建立 hello 子網路時，它會強制在 hello hello ASE toobe hello 虛擬網路所在的資源群組。 如果您需要使用不同於您的 VNet 您 ASE toobe hello 資源群組，則您需要 toocreate 您 ASE 使用資源管理員範本。

有一些限制 hello 用於 ase 中的虛擬網路上：

* hello 虛擬網路必須是區域虛擬網路。
* 需要 toobe 具有 8 個以上的地址 hello ASE 部署所在之子網路。
* 子網路是使用的 toohost ase 中之後，就無法變更 hello hello 子網路的位址範圍。 基於這個理由，我們建議 hello 該子包含至少 64 位址 tooaccommodate 未來 ASE 成長。
* 可以在 hello 子網路但 hello ASE 中的其他內容。

不同於包含 hello ASE hello 裝載服務，hello[虛擬網路][ virtualnetwork]和子網路會由使用者控制。  您可以管理虛擬網路透過 hello 虛擬網路 UI 或 PowerShell。  ASE 可以部署在傳統或 Resource Manager VNet 中。  hello 入口網站和 API 體驗有些許不同，傳統與資源管理員 Vnet 之間但 hello ASE 經驗是 hello 相同。

hello VNet 使用的 toohost ase 中可以使用其中一個私人 RFC1918 IP 位址，或者它可以使用公用 IP 位址。  如果您想 toouse RFC1918 未涵蓋的 IP 範圍 （10.0.0.0/8、 172.16.0.0/12、 192.168.0.0/16） 則需要由您 ASE 前面 ASE 建立您的 VNet 和子網路 toobe toocreate。

因為這項功能將在您的虛擬網路的 hello Azure 應用程式服務，它表示在您 ASE 中裝載的應用程式現在可以存取可供使用透過 ExpressRoute 或站對站虛擬私人網路 (Vpn) 直接的資源。 App Service 環境中的 hello 應用程式不需要其他網路功能 tooaccess 資源可用 toohello 虛擬網路裝載 App Service 環境。 這表示，您不需要在 toouse VNET 整合或混合式連線 tooget tooresources 或連接的 tooyour 虛擬網路。 您仍然可以使用這兩個這些功能雖然 tooaccess 資源不會有的網路連線 tooyour 虛擬網路。

例如，您可以使用 VNET 整合 toointegrate 與位於您的訂用帳戶，但不連接的 toohello 您 ASE 是中的虛擬網路的虛擬網路。 您仍然也可以使用其他網路，就像您通常可以在混合式連線 tooaccess 資源。  

如果您沒有虛擬網路設定與 ExpressRoute VPN，您應該留意某些 hello ase 中具有的路由需求。 某些使用者定義的路由 (UDR) 組態與 ASE 不相容。 如需關於在具有 ExpressRoute 的虛擬網路中執行 ASE 的詳細資訊，請參閱[在具有 ExpressRoute 的虛擬網路中執行 App Service 環境][ExpressRoute]。

#### <a name="securing-inbound-traffic"></a>保護輸入流量
有兩個主要方法 toocontrol 輸入流量 tooyour ASE。  您可以使用網路安全性 Groups(NSGs) toocontrol 哪些 IP 位址可以存取您 ASE，如下所述[toocontrol 如何輸入 App Service 環境中的流量](app-service-app-service-environment-control-inbound-traffic.md)，您也可以使用內部的負載來設定您 ASEBalancer(ILB)。  這些功能也可用在一起如果您想要使用 Nsg tooyour ILB ASE toorestrict 存取。

當您建立 ASE 時，它會在您的 VNet 中建立 VIP。  VIP 類型有兩種：外部和內部。  當您使用外部 VIP 建立 ASE 時，可以透過網際網路可路由 IP 位址存取 ASE 中的應用程式。 如果您選取內部，您的 ASE 會使用 ILB 進行設定，將無法透過網際網路直接存取。  ILB ASE 仍需要外部 VIP，但它只用來進行 Azure 管理和維護。  

ILB ASE 建立期間您提供 hello hello ILB ASE 所使用的子網域，而且必須 toomanage hello 您指定的子網域的 DNS。  因為設定 hello 子網域名稱，您也需要使用 HTTPS 存取 toomanage hello 憑證。  ASE 之後您會的建立提示 tooprovide hello 憑證。  深入了解建立和使用 ILB ASE toolearn 讀取[App Service 環境中使用內部負載平衡器][ILBASE]。 

## <a name="portal"></a>入口網站
您可以管理，並使用 hello UI hello Azure 入口網站中的監視 App Service 環境。 如果您有 ase 中，您便可能 toosee hello App Service 符號資訊看板 上。 這個符號是 hello Azure 入口網站中使用的 toorepresent 應用程式服務環境：

![App Service 環境符號][1]

tooopen hello 列出所有您的應用程式服務環境的 UI，您可以使用 hello 圖示或選取 hello > 形箭號 (">"符號) 在 hello 資訊看板 tooselect 應用程式服務環境的 hello 底部。 選取其中一個列出的 hello ASEs，您可以開啟 hello 使用的 toomonitor 的 UI，並管理它。

![用於監視和管理 App Service 環境的 UI][2]

這是第一個刀鋒視窗，顯示 ASE 的某些屬性和每個資源集區的計量圖表。 某些 hello 屬性所顯示的 hello **Essentials**區塊也會與它相關聯的 hello 刀鋒視窗會開啟的超連結。 例如，您可以選取 hello**虛擬網路**名稱 tooopen 向上 hello UI 相關聯 hello ASE 您正在執行中的虛擬網路。 **App Service 方案**和**應用程式**分別會開啟不同的刀鋒視窗，列出位於您 ASE 中的項目。  

### <a name="monitoring"></a>監視
hello 圖表可讓您 toosee 各種不同的每個資源集區中的效能度量。 Hello 前端集區，您可以監視 hello 平均 CPU 和記憶體。 背景工作集區，您可以監視用 hello 數量以及所提供的 hello 數量。

計劃可讓多個應用程式服務使用的背景工作集區中的 hello 背景工作。 hello 讓 hello CPU 和記憶體使用量不提供實用資訊的 hello 方式大致相同方式如同 hello 前端伺服器，在分散 hello 工作負載。 它是更重要的 tootrack 多少已使用的背景工作，並且可用於-特別是當您管理此系統的其他人 toouse。  

您也可以使用所有的可追蹤 hello 圖表 tooset 警示中的 hello 度量。 設定此警示運作方式相同，其他地方 hello App Service 中。 您可以設定警示的任一個 hello**警示**UI 一部分，或者從鑽研 UI 和選取的任何度量**新增警示**。

![度量 UI][3]

剛才討論過的 hello 度量是 hello App Service 環境指標。 也有一些可以在 hello App Service 方案層級的度量。 在其中監視 CPU 和記憶體是很合理的作法。

在 ase 中，應用程式服務計劃的 hello 均專用的應用程式服務方案。 這表示，hello 唯一執行的應用程式上 hello 主機配置 toothat App Service 方案 hello 應用程式於該 App Service 方案。 從任何 hello 清單 hello ASE UI 中，或從您 App Service 方案開啟 toosee 詳細資料，在您的應用程式服務方案**瀏覽應用程式服務計劃**（其中會列出所有的）。   

### <a name="settings"></a>設定
在 hello ASE 刀鋒視窗中，**設定**區段，其中包含數項重要功能：

**設定** > **屬性**: hello**設定**調出您 ASE 刀鋒視窗時，自動就會開啟刀鋒視窗。 Top 將不在 hello**屬性**。 有許多的項目在這裡您在中看到的多餘 toowhat **Essentials**，是非常有用，但**虛擬 IP 位址**，以及**輸出的 IP 位址**。

![設定刀鋒視窗和屬性][4]

**設定** > ：當您在 ASE 中建立 IP 安全通訊端層 (SSL) 應用程式時，您需要一個 IP SSL 位址。 一個順序 tooobtain，在您 ASE 會需要 IP SSL 位址，它擁有可配置。 建立 ASE 後，它會有一個 IP SSL 可供此用途使用，但您可以新增更多位址。 不需費用針對額外的 IP SSL 位址，如中所示[應用程式服務定價][ AppServicePricing] （位於在 SSL 連線上的 hello 區段）。 hello 其他價格為 hello IP SSL 的價格。

**設定** > **Front End 集區** / **背景工作集區**： 每個資源集區的刀鋒視窗，提供 hello 能力 toosee 資訊只在該資源集區此外 tooproviding 會控制 toofully 縮放該資源集區。  

hello 基底刀鋒視窗中的每個資源集區之資源集區提供計量的圖表。 就像與 hello hello ASE 刀鋒視窗中，圖表可以進入 hello 圖表，而設定所需的警示。 從特定的資源集區的 hello ASE 刀鋒視窗中設定警示未 hello 進行從 hello 資源集區相同的動作。 Hello 背景工作集區從**設定**刀鋒視窗中，您有存取 tooall hello 應用程式或應用程式服務計劃在這個背景工作集區中執行。

![背景工作集區設定 UI][5]

### <a name="portal-scale-capabilities"></a>入口網站調整功能
共有三種調整作業：

* 變更 hello 數目 hello ASE 中的 IP 位址可用於 IP SSL 用法。
* 使用資源集區中的 hello 計算資源的 hello 大小變更。
* 變更 hello 數目可以是手動或自動調整資源集區中使用的計算資源。

在 hello 入口網站中，有三種方式 toocontrol 您的資源集區中有多少部伺服器：

* 從 hello 主要 ASE 刀鋒視窗頂端 hello 調整規模作業。 您可以讓多個小數位數的組態變更 toohello 前端和背景工作集區。 它們會以單一作業的方式全部套用。
* 手動調整規模作業從 hello 個別的資源集區**標尺**刀鋒視窗中，也就是下**設定**。
* 自動調整，您將設定從 hello 個別的資源集區**標尺**刀鋒視窗。

toouse hello 調整規模作業上 hello ASE 刀鋒視窗中，拖曳您想要並儲存 hello 滑桿 toohello 數量。 此 UI 也支援變更 hello 大小。  

![調整 UI][6]

toouse hello 手動或自動調整規模功能特定的資源集區，在跳過**設定** > **Front End 集區** / **背景工作集區**為適當的。 然後就會開啟 hello 集區的 toochange。 跳過**設定** > **向外**或**設定** > **向上延展**。 hello**向外**刀鋒視窗可讓您 toocontrol 執行個體數量。 **向外延展**可讓您 toocontrol 資源大小。  

![調整設定 UI][7]

## <a name="fault-tolerance-considerations"></a>容錯注意事項
您可以設定的 App Service 環境 toouse too55 總數的計算資源。 這些 55 的計算資源，只有 50 可以使用的 toohost 工作負載。 hello 這個錯誤的原因有兩個。 前端計算資源的下限為 2 個。  還剩下向上 too53 toosupport hello 背景工作集區配置。 在順序 tooprovide 容錯功能，您會需要 toohave 根據下列規則 toohello 配置額外的計算資源：

* 每個背景工作集區必須至少為 1 的額外的計算資源，不是使用 toobe 指派工作負載。
* 背景工作集區中的計算資源的 hello 數量超出特定值，然後另一個運算資源時需要容錯。 這不是 hello 前端集區中的 hello 案例。

在任何單一工作者集區中，hello 容錯需求是給定值 X 資源指派 tooa 背景工作集區：

* 如果 X 是介於 2 到 20 之間，可使用的計算資源，您可以使用工作負載的 hello 數量是 X-1。
* 如果 X 為 21 歲到 40 之間，可使用的計算資源，您可以使用工作負載的 hello 數量是 X-2。
* 如果 X 是 41 和 53 之間，可使用的計算資源，您可以使用工作負載的 hello 數量是 X-3。

hello 最少使用量都有 2 的前端伺服器和 2 個背景工作。  以上述陳述式然後 hello，以下是一些範例 tooclarify:  

* 如果您在單一的集區中有 30 的背景工作，其中 28 可以是使用的 toohost 工作負載。
* 如果您在單一的集區中有 2 個背景工作，然後 1 可以使用的 toohost 工作負載。
* 如果您在單一的集區中有 20 工作者，19 可以是使用的 toohost 工作負載。  
* 如果您在單一的集區中有 21 的背景工作，然後仍 19 只能使用的 toohost 工作負載。  

hello 容錯功能方面很重要，但您需要的 tookeep 它為您記住調整超過特定閾值。 如果您想 tooadd 更容量從 20 的執行個體，然後移 too22 或更高版本因為 21 並不會加入更多的容量。 hello 也是如此移 40，上面其中 hello 增加容量的下一個編號 42。  

## <a name="deleting-an-app-service-environment"></a>刪除 App Service 環境
如果您想 toodelete App Service 環境，然後只使用 hello**刪除**在 hello hello App Service 環境刀鋒視窗頂端的動作。 當您這樣做時，您會確認您是否真的想 toodo 這您 App Service 環境 tooconfirm 提示的 tooenter hello 名稱。 請注意，當您刪除 App Service 環境，您刪除所有 hello 內容以及。  

![刪除 App Service 環境 UI][9]  

## <a name="getting-started"></a>開始使用
tooget 開始使用應用程式服務環境中，請參閱[如何 toocreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service](../app-service/app-service-value-prop-what-is.md)。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
