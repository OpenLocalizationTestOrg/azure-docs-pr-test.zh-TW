---
title: "Azure 虛擬資料中心 aaaMicrosoft |Microsoft 文件"
description: "了解如何 toobuild 虛擬資料中心在 Azure 中"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Microsoft Azure 虛擬資料中心
**Microsoft Azure**：移動更為快速、節省成本、在內部部署環境整合應用程式和資料

## <a name="overview"></a>概觀
移轉內部部署應用程式 tooAzure，即使沒有任何重大變更 （稱為 「 提起和 shift 」 方法），提供組織 hello 優點安全和成本效益的基礎結構。 不過，toomake hello 最的 hello 靈活度採用雲端運算，企業應發展其架構 tootake 利用 Azure 的功能。 Microsoft Azure 提供超大規模的服務和基礎結構、企業級功能和可靠性，以及許多混合式連線選項。 客戶可以選擇這些雲端服務透過 tooaccess hello 網際網路或透過 Azure ExpressRoute，這樣會提供私人網路連線。 hello Microsoft Azure 平台可讓的客戶將他們的基礎結構延伸至雲端 hello tooseamlessly，並建置多層式架構。 此外，Microsoft 夥伴藉由提供安全性服務提供增強的功能和虛擬裝置而言，是最佳化 toorun 在 Azure 中。

這篇文章提供模式的概觀，並可使用的 toosolve 設計 hello 架構時考慮一併移動 toohello 雲端，許多客戶面臨的小數位數、 效能和安全性問題。 如何 toofit 不同組織 IT 角色加入 hello 管理和控管的 hello 系統也會探討，以強調 toosecurity 需求和成本最佳化的概觀。

## <a name="what-is-a-virtual-data-center"></a>什麼是虛擬資料中心？
在 hello 早期雲端解決方案設計的 toohost 單一且相對較隔離的應用程式，已在 hello 公用頻譜。 這種方法已良好運作多年。 不過，hello 雲端優點為解決方案變得很明顯和大規模的多個工作負載已裝載於 hello 雲端定址安全性、 可靠性、 效能和成本考量的其中一個部署或更多區域變得重要整個 hellohello 雲端服務的生命週期。

hello 雲端部署圖說明的安全性漏洞 （紅色方塊） 及最佳化網路虛擬裝置的聊天室的一些範例整個工作負載 （黃色方塊）。

[![0]][0]

調整 toosupport 企業工作負載，這需要從出生 hello 虛擬資料中心 (vDC) 而且 hello 需要 toodeal hello hello 公用雲端中支援大規模的應用程式時導入的問題。

VDC 不只 hello 應用程式中的工作負載 hello 雲端，但也 hello 網路、 安全性、 管理和基礎結構 （例如，DNS 與目錄服務）。 它通常也會提供私人連線後 tooan 內部網路或資料中心。 越來越多的工作負載移動 tooAzure，它是 hello 支援基礎結構與物件相關的重要 toothink 放置在這些工作負載。 請仔細考慮資源的結構方式可以避免 hello 激增數百個 「 工作負載島 」 必須獨立的資料流程、 安全性模型與相容性挑戰分開管理。

虛擬資料中心本質上是不同但相關實體的集合，而實體具有一般支援功能和基礎結構。 透過整合式的 vDC 為檢視您的工作負載，您可以了解降低的成本，因為標尺，透過元件和資料最佳化安全性 tooeconomies 流程集中化，以及更容易操作、 管理和相容性稽核。

> [!NOTE]
> 這是很重要的 hello vDC toounderstand**不**離散的 Azure 產品，但的各種特性與功能的 hello 組合太符合您實際需求。 vDC 是一種您的資源和 hello 雲端中的能力，考慮您的工作負載和 Azure 使用量 toomaximize。 hello 虛擬 DC 會因此模組化的方法，如何 toobuild 在 hello Azure，又能顧及對於組織的角色和責任的 IT 服務。

hello vDC 可協助企業工作負載和應用程式至 Azure 中取得 hello 下列案例：

-   裝載多個相關工作負載
-   從內部部署環境 tooAzure 移轉工作負載
-   實作工作負載之間的共用或集中式安全性和存取需求
-   適當地針對大型企業混合使用 DevOps 和集中式 IT

hello vDC 金鑰 toounlock hello 優點，是混合的 Azure 功能的集中式的拓撲 （中樞和支點）： [Azure VNet][VNet]， [Nsg] [ NSG]，[對等互連的 VNet][VNetPeering]，[使用者定義的路由 (UDR)][UDR]，和 Azure 身分識別與[角色基底存取控制 (RBAC)][RBAC]。

## <a name="who-needs-a-virtual-data-center"></a>誰需要虛擬資料中心？
任何需要 toomove 以上的數個工作負載至 Azure 的 Azure 客戶可以受益思考使用常用的資源。 根據 hello 範圍內，即使單一應用程式可以受益於使用 hello 模式，並使用 toobuild vDC 元件。

如果您的組織有集中化的 IT 消費化、 網路、 安全性，和 （或) 相容性小組/部門 vDC 有助於強制執行原則點、 隔離的工作，並確保一致的 hello 基礎同時程度會提供應用程式小組的一般元件自由和控制項，因為是適合您的需求。

要尋找 tooDevOps 的組織可以利用 hello vDC 概念 tooprovide 授權口袋的 Azure 資源，並確定它們有 （訂用帳戶或資源群組中常見的訂用帳戶），該群組內的總控制項，但 hello 網路和安全性界限維持相容所定義中樞 VNet 與資源群組中的集中原則。

## <a name="considerations-on-implementing-a-virtual-data-center"></a>實作虛擬資料中心的考量
當設計 vDC，有數個關鍵問題 tooconsider:

-   身分識別和目錄服務
-   安全性基礎結構
-   連線 toohello 雲端
-   Hello 雲端內的連線

##### <a name="identity-and-directory-service"></a>*身分識別和目錄服務*
身分識別和目錄服務是一個關鍵層面的所有資料中心，這兩個內部部署和 hello 雲端中。 身分識別不相關的 tooall hello vDC 內存取和授權 tooservices 層面。 toohelp 會確保只有授權的使用者和處理程序存取您的 Azure 帳戶和資源，Azure 會使用幾種類型的認證進行驗證。 這些包括 (tooaccess hello Azure 帳戶) 的密碼、 密碼編譯金鑰、 數位簽章和憑證。 [*Azure Multi-Factor Authentication* (MFA)][MFA] 是存取 Azure 服務的額外安全層。 Azure MFA 提供增強式驗證與一系列簡單的驗證選項 — 通話、 簡訊或行動裝置應用程式通知，並讓客戶其偏好的 toochoose hello 方法。

任何大型企業需要 toodefine 描述 hello 管理個別的身分識別、 其驗證、 授權、 角色和權限或跨 hello vDC 身分識別管理程序。 此程序的 hello 目標應該是 tooincrease 安全性和產能，降低成本、 停機時間和重複的手動工作。

企業/組織可能需要依需求混合使用不同企業營運 (LOB) 的服務，而且員工通常在涉及不同專案時會有不同角色。 VDC 需要不同的小組，分別各具特定角色定義，良好的控管的 tooget 系統之間的良好合作。 hello 矩陣的責任、 存取和權限可以是非常複雜。 vDC 中的身分識別管理是透過 [*Azure Active Directory* (AAD)][AAD] 和角色型存取控制 (RBAC) 進行實作。

目錄服務是一種共用資訊基礎結構，用於尋找、管理和組織日常項目和網路資源。 這些資源可能包含磁碟區、資料夾、檔案、印表機、使用者、群組、裝置和其他物件。 Hello 網路上的每個資源視為 hello 目錄伺服器物件。 資源的相關資訊會儲存為與該資源或物件建立關聯的屬性集合。

所有 Microsoft 線上商務服務都依賴 Azure Active Directory (AAD) 來進行登入和其他身分識別需求。 Azure Active Directory 是全方位、高可用性的身分識別和存取管理的雲端解決方案，它結合了核心目錄服務、進階身分識別管制及應用程式存取管理。 AAD 可以與內部部署 Active Directory tooenable 單一登入的所有以雲端為基礎，並在本機裝載 （內部） 應用程式整合。 可以自動同步處理的 tooAAD hello 使用者屬性在內部部署 Active directory。

一位全域系統管理員是不必要的 tooassign vDC 中的所有權限。 改為每個特定部門 （或使用者或服務在 hello 目錄服務中的群組） 可以有 hello 權限需要的 toomanage 自己 vDC 內的資源。 建構權限需要平衡。 權限太多可能會阻礙效能效率，而權限太少或鬆散可能會增加安全性風險。 Azure 角色型存取控制 (RBAC) 的精細存取管理 vDC 資源的供應項目，這個問題，請將有助於 tooaddress。

##### <a name="security-infrastructure"></a>*安全性基礎結構*
VDC，hello 內容中的安全性基礎結構，是流量的主要相關的 toohello 隔離的 hello vDC 特定虛擬網路區段和 toocontrol ingress 和 egress 如何整個 hello vDC 流動。 Azure 是根據多租用戶架構，可使用虛擬網路 (VNet) 隔離、存取控制清單 (ACL)、負載平衡器和 IP 篩選以及流量流程原則來防止部署之間的未經授權和意外流量。 網路位址轉譯 (NAT) 會區隔內部網路流量與外部流量。

hello Azure 網狀架構基礎結構資源配置 tootenant 工作負載和管理行動裝置管理通訊 tooand 虛擬機器 (Vm)。 hello Azure hypervisor 會強制執行記憶體和處理序隔離的 Vm 與之間安全地路由網路流量 tooguest OS 租用戶。

##### <a name="connectivity-toohello-cloud"></a>*連線 toohello 雲端*
hello vDC 必須與外部網路 toooffer 服務 toocustomers、 協力廠商及/或內部使用者的連線。 這通常表示連線不僅 toohello 網際網路，而且還 tooon 內部部署網路與資料中心。

客戶可以建置其安全性原則 toocontrol 什麼及如何特定 vDC 裝載服務都可存取，或從 hello 網際網路使用網路虛擬裝置 （使用篩選和資料傳輸檢查） 和網路篩選 （自訂路由原則使用者定義的路由和網路安全性群組）。

企業通常需要 tooconnect Vdc tooon 內部部署資料中心或其他資源。 Azure 和內部部署網路之間的 hello 連線時，因此的重要層面設計有效的架構。 企業兩個不同的方式 toocreate vDC 與內部部署之間互相連線在 Azure 中設有： 透過 hello 網際網路及/或私人的直接連線的傳輸。

[ **Azure 站台對站 VPN** ] [ VPN]互連服務透過內部部署網路之間的 hello 網際網路且 hello vDC，透過安全建立加密連接 （IPsec/IKE 通道）。 Azure 站台對站連接是具彈性且更快速 toocreate，而且不需要任何進一步的採購，因為所有連線透過都連接 hello 網際網路。

[**ExpressRoute** ] [ ExR]是一種 Azure 連線的服務，可讓您建立私人連線 vDC 與 hello 之間在內部部署網路。 ExpressRoute 連線不會超過 hello 公用網際網路，並提供較高的安全性、 可靠性和高加速 （too10 Gbps) 以及一致的延遲。 為客戶可以獲得私人連線相關聯的相容性規則的 hello 優勢的 ExpressRoute ExpressRoute 是 Vdc，非常有用。

部署 ExpressRoute 連線包含加入 ExpressRoute 服務提供者。 需要 toostart 快速的客戶，它會是 tooinitially 常用 hello vDC 和內部部署資源之間的站對站 VPN tooestablish 連線，然後再移轉 tooExpressRoute 連線。

##### <a name="connectivity-within-hello-cloud"></a>*Hello 雲端內的連線*
[Vnet] [ VNet]和[對等互連的 VNet] [ VNetPeering] hello 基本網路連線服務 vDC 內。 對等互連的 VNet 可讓不同的 Vnet 內 hello 之間互相通訊與 VNet 保證隔離 vDC 資源自然界限相同 Azure 區域。 內部 VNet 和 Vnet 之間的流量控制需要的 toomatch 安全性規則指定透過存取控制清單 ([網路安全性群組][NSG])，[網路虛擬裝置] [ NVA]，和自訂路由表 ([UDR][UDR])。

## <a name="virtual-data-center-overview"></a>虛擬資料中心概觀

### <a name="topology"></a>拓撲
中樞和支點模型內單一 Azure 區域的擴充的 hello 虛擬資料中心

[![1]][1]

hello 集線器是控制，並檢查不同的區域之間的輸入和 （或） 輸出流量的 hello 中央區域： 網際網路、 內部部署和 hello 支點。 hello 中樞和支點拓撲提供同時減少 hello 可能設定錯誤以及如何將風險 hello IT 部門在集中位置，有效地 tooenforce 安全性原則。

hello 中樞會包含 hello 供 hello 支點一般服務元件。 以下是一些典型常用中央服務範例：

-   hello Windows Active Directory 基礎結構 （hello 與相關的 ADFS 服務） 所需的使用者驗證的第三方之前取得存取 toohello 工作負載中的 hello 支點來自不受信任的網路存取
-   DNS 服務的 hello 工作負載在 hello 支點 tooaccess 資源內部部署和 hello 網際網路命名 tooresolve
-   PKI 基礎結構，tooimplement 單一登入工作負載
-   Hello 支點與網際網路之間的流量控制 (TCP/UDP)
-   Hello 支點與內部部署之間的流量控制
-   如有需要，為兩個支點之間的流量控制

hello vDC 使用多個支點之間 hello 共用的中樞基礎結構，以減少整體成本。

每個支點 hello 角色可以是 toohost 不同類型的工作負載。 hello 支點也可以提供模組化的方法可重複的部署 (例如，開發和測試中，使用者接受度測試進入生產階段前和生產) 的 hello 相同的工作負載。 hello 支點也可以是使用的 toosegregate 並啟用您的組織 （例如，DevOps 群組） 內的不同群組。 內部支點，很可能 toodeploy hello 各層之間的基本的工作負載或複雜的多層式工作負載的流量控制。

##### <a name="subscription-limits-and-multiple-hubs"></a>訂用帳戶限制和多個中樞
在 Azure 中，每個元件，無論 hello 型別，被部署在 Azure 訂用帳戶。 Azure 中的元件不同的 Azure 訂用帳戶的 hello 隔離，能滿足 hello 需求的不同 Lob，例如設定層級的存取和授權。

單一 vDC 雖然如同每個 IT 系統，沒有平台限制就能相應 toolarge 支點數目。 hello 中樞部署是繫結的 tooa 特定 Azure 訂用帳戶，具有限制和限制 (例如，請參閱 VNet 對等互連的最大數目[Azure 訂用帳戶和服務限制、 配額和條件約束][ Limits]如需詳細資訊)。 在位置限制可能會產生問題的情況下，可以調整 hello 架構最多進一步藉由從單一中樞-支點 tooa 叢集中的中樞和支點擴充 hello 模型。 一或多個 Azure 區域中的多個中樞可以使用 Express Route 或站對站 VPN 互相連接。

[![2]][2]

hello 導入多個集線器會增加 hello hello 系統的成本和管理工作並只會由延展性對齊 (範例： 系統限制或備援) 和地區的複寫 (範例： 使用者效能或災害復原)。 在需要多個集線器的情況下，所有的 hello 中樞應盡可能相同設定的服務作業以便 toooffer hello。

##### <a name="interconnection-between-spokes"></a>支點之間的互相連線
在單一支點，很可能 tooimplement 複雜的多層工作負載。 可以使用子網路 （一個用於每個層） 相同的 VNet 和篩選 hello 流向使用 Nsg hello 中實作多層式組態。

在 hello 另一方面，架構設計人員可能會想 toodeploy 多層式工作負載，跨多個 Vnet。 使用對等互連的 VNet，支點可以連線 tooother 支點 hello 中的相同的中樞或不同的中心。 此案例中的典型範例是 hello 案例，其中應用程式處理伺服器位於一個支點 (VNet)，而 hello 資料庫部署在不同的支點 (VNet)。 在此情況下，它是簡單 toointerconnect hello 支點與 VNet 對等互連，並藉此避免發生透過 hello 中樞傳送。 詳細的架構與安全性檢閱應該執行的 tooensure hello 中樞略過重要的安全性或稽核可能只存在於 hello 中樞的點不會略過。

[![3]][3]

支點也可以做為中樞的互連的 tooa 支點。 這個方法會建立兩層式階層： hello 支點 hello 較高的層級 （層級 0） 中會變成 hello 中樞的 hello 階層的較低的支點 （層級 1）。 vDC 的 hello 支點需要 tooforward hello 流量 toohello hub tooreach toohello 與內部網路或網際網路。 具有兩個層級的中樞架構導入了複雜路由，以便移除 hello 簡單中樞-支點關聯性的優點。

雖然 Azure 可讓複雜的拓撲，其中一個 hello vDC 概念的 hello 核心原則是重複性和簡單性。 toominimize 管理投入時間，hello 簡單中樞-支點設計為建議 vDC 參考架構的 hello。

### <a name="components"></a>元件
虛擬資料中心是由四種基本元件類型所構成：[基礎結構]、[周邊網路]、[工作負載] 和 [監視]。

每種元件類型都是由各種 Azure 功能和資源所組成。 您 vDC 所組成的多個元件的類型和多個變化的 hello 的執行個體相同元件類型。 例如，您可能有代表不同應用程式之許多不同邏輯分隔的工作負載執行個體。 您可以使用這些不同元件類型，並執行個體 tooultimately 建立 hello vDC。

[![4]][4]

hello vDC 上述高階架構顯示 hello 中樞-支點拓撲的不同區域使用不同的元件類型。 hello 圖表顯示 hello 架構的各種組件中的基礎結構元件。

不錯的做法 (適用於內部部署 DC 或 vDC) 是存取權利和權限應該是以群組為基礎。 處理群組，而不是個別使用者協助一致地維護跨小組的存取原則，以及協助將設定錯誤降至最低。 指派及移除使用者 tooand 從適當的群組可協助保持最新狀態 hello 特定使用者權限。

每個角色群組只能有唯一的前置詞讓您輕鬆 tooidentify 哪些群組是相關聯的工作負載的名稱。 例如，裝載驗證服務的工作負載可能會名為 AuthServiceNetOps、AuthServiceSecOps、AuthServiceDevOps 和 AuthServiceInfraOps 的群組。 同樣的集中式角色不相關 tooa 特定服務，無法做為 「 Corp 」，開頭*CorpNetOps*例如。

許多組織使用下列群組 tooprovide 主要角色的細目 hello 的變化：

-   hello*中央 IT 群組 (Corp)*有 hello 擁有權權限 toocontrol 基礎結構 （例如網路和安全性） 元件，因此需要 toohave hello hello 訂用帳戶上的參與者角色 （和擁有的控制權hello 集線器） 和網路 hello 支點中的參與者權限。 大型組織經常會在多個小組之間分割這些責任，例如網路作業 (CorpNetOps) 群組 (具有網路的獨佔焦點) 和資料安全性作業 (CorpSecOps) 群組 (負責防火牆和安全性原則)。 這種情況下，兩個不同群組需要 toobe 建立這些自訂的角色指派。
-   hello*開發人員 （& a) 測試 (AppDevOps) 群組*具有 hello 責任 toodeploy 工作負載 （應用程式或服務）。 這個群組會 hello 角色的虛擬機器參與者 IaaS 部署和/或一個或多個 PaaS 參與者角色 (請參閱[所有存取控制的內建角色][Roles])。 選擇性地 hello 開發與測試小組可能需要在安全性原則 (Nsg) 和 hello 中樞內的路由原則 (UDR) 或特定支點 toohave 可見性。 因此，在加法 toohello 角色中的參與者的工作負載，此群組還需要 hello 網路讀取器角色。
-   hello*操作和維護的群組 （CorpInfraOps 或 AppInfraOps）* hello 負責管理生產環境中的工作負載。 此群組需要 toobe 訂用帳戶上的 contributor 任何生產訂用帳戶中的工作負載。 如果需要其他擴大支援小組群組與 hello 角色的訂用帳戶參與者在生產環境中與 hello hub 訂用帳戶中，在訂單 toofix 潛在設定問題 hello 生產環境中，某些組織可能會也評估環境。

VDC 具結構性，以建立 hello 管理 hello 中樞中央 IT 群組的群組具有對應群組 hello 工作負載層級。 此外 toomanaging 中樞資源唯一 hello 中央 IT 群組會是能 toocontrol 外部存取和 hello 訂用帳戶的最上層權限。 不過，工作負載群組會是能 toocontrol 資源和其 VNet 中央 IT 上獨立的權限。

hello vDC 需求 toobe 分割到不同列的-商務 (Lob) toosecurely 主機多個專案。 所有專案則都需要不同的隔離環境 (開發、UAT、生產)。 其中每個環境的不同 Azure 訂用帳戶都會提供自然隔離。

[![5]][5]

hello 上圖顯示 hello 組織的專案、 使用者、 群組和其中 hello Azure 元件部署的 hello 環境之間的關聯性。

通常，在 IT 中，環境 (或層) 是部署和執行多個應用程式的系統。 大型企業使用開發環境 (一開始進行和測試變更的位置) 和生產環境 (使用者所使用的環境)。 這些環境，通常以分隔數個預備環境，兩者中間 tooallow 階段部署 （首展）、 測試和復原發生問題。 部署架構甚大，但通常仍然跟在開發階段 (DEV) 開始和結束點實際執行環境 （生產環境） 的 hello 基本程序。

這些多層環境類型的常見架構包含 DevOps (開發和測試)、UAT (預備) 和生產環境。 組織可以利用單一或多個 Azure AD 租用戶 toodefine toothese 環境存取與權限。 hello 上圖將顯示兩個不同 Azure AD 租用戶所使用： 一個適用於 DevOps 和使用者接受度測試，而其他專用的實際執行 hello。

hello 存在不同的 Azure AD 的租用戶會強制執行環境的 hello 區隔。 hello 相同的使用者群組 （例如，中央 IT） 需要使用不同的 URI tooaccess 不同的 AD 租用戶 tooauthenticate 修改 hello 角色或權限是 hello DevOps 或實際執行環境中的專案。 不同的使用者驗證 tooaccess 不同環境的 hello 與否會減少可能中斷和其他人為錯誤所造成的問題。

#### <a name="component-type-infrastructure"></a>元件類型：基礎結構
此元件的類型是 hello 的大部分支援基礎結構所在的位置。 它也是集中式 IT、安全性和 (或) 相容性小組花費最多時間的位置。

[![6]][6]

基礎結構元件提供 hello vDC，不同元件之間互相連線，並會在 hello 中樞和支點 hello。 hello 負責管理和維護 hello 基礎結構元件通常會指派 toohello 中央 IT 和/或安全性團隊。

其中一個 hello 主要工作 IT 基礎結構團隊 hello 企業是 hello 的 tooguarantee hello 一致性的 IP 位址結構描述。 hello 私用 IP 位址空間指派 toohello vDC 需要 toobe 一致和不與內部部署網路上指派的私人 IP 位址重疊。

雖然 hello NAT 內部邊際路由器或在 Azure 中的環境可以避免發生 IP 位址衝突，它會加入複雜性 tooyour 基礎結構元件。 簡化是管理的 hello 做為關鍵目標的 vDC，因此使用 NAT toohandle IP 考量不建議的解決方案。

基礎結構元件包含下列功能的 hello:

-   [**身分識別和目錄服務**][AAD]. 在 Azure 中的存取 tooevery 資源類型會控制儲存在目錄服務中的身分識別。 hello 目錄服務會儲存不只 hello 使用者清單，但也 hello 中特定的 Azure 訂用帳戶的存取權限 tooresources。 這些服務只能存在於雲端，或與 Active Directory 中所儲存的內部部署身分識別同步。
-   [**虛擬網路**][VPN]。 虛擬網路是其中一種 vDC，主要元件，並啟用 toocreate hello Azure 平台上的流量隔離界限。 虛擬網路是由單一或多個虛擬網路區段所組成，而每個區段都有特定 IP 網路前置詞 (子網路)。 hello 虛擬網路定義 IaaS 虛擬機器和 PaaS 服務可以建立私用通訊的內部周邊區域。 Vm （和 PaaS 服務） 在虛擬網路無法通訊，直接 tooVMs （和 PaaS 服務） 在不同的虛擬網路中，即使這兩個虛擬網路建立的 hello 同一位客戶下, 一個 hello 相同訂用帳戶。 隔離是很重要的屬性，可確保客戶 VM 和通訊仍然隱蔽於虛擬網路內。
-   [**UDR**][UDR]。 在虛擬網路的流量路由傳送 hello 系統路由表為基礎的預設值。 使用者定義的路由，是自訂路由表，網路系統管理員可以將 tooone 或更多的子網路 toooverwrite hello 行為 hello 系統路由表產生關聯，並定義虛擬網路內的通訊路徑。 hello 與否 UDRs 保證該輸出流量從透過特定的自訂 Vm 和/或網路虛擬裝置與負載平衡器在 hello 中樞和支點 hello 出現的 hello 支點傳輸資料。
-   [**NSG**][NSG]. 網路安全性群組是安全性規則清單，而安全性規則是作為 IP 來源、IP 目的地、通訊協定、IP 來源連接埠和 IP 目的地連接埠的流量篩選。 hello NSG 可以套用的 tooa 子網路，Azure VM，或兩者與相關聯的虛擬 NIC 卡。 hello Nsg 是不可或缺的 tooimplement hello 中樞和支點 hello 中正確的流量控制。 hello hello NSG 所提供的安全性層級為您開啟時，哪些連接埠，用於何種用途的函式。 客戶應該套用每個 VM 的其他篩選搭配主機型防火牆，例如 IPtables 或 hello Windows 防火牆。
-   **DNS**。 透過 DNS 提供 hello hello vDC 的 Vnet 中的資源的名稱解析。 hello hello 預設 DNS 名稱解析範圍會限制的 toohello VNet。 通常，自訂的 DNS 服務需要 toobe hello 中樞中部署為通用服務的一部分，但是 hello 的 DNS 服務的主要取用者位於 hello 支點。 如有必要，客戶可以使用委派的 DNS 區域 toohello 支點建立階層式 DNS 結構。
-   [**訂用帳戶][SubMgmt]和[資源群組管理][RGMgmt]**。 訂閱定義自然界限 toocreate 多個資源群組在 Azure 中。 在名為「資源群組」的邏輯容器中，會將訂用帳戶中的資源組合在一起。 hello 資源群組代表 vDC 邏輯群組 tooorganize hello 資源。
-   [**RBAC**][RBAC]。 透過 RBAC，很可能 toomap 組織角色的權限 tooaccess 特定 Azure 資源，可讓您 toorestrict 使用者 tooonly 動作子集。 使用 RBAC，您可以藉由指派 hello 適當的角色 toousers、 群組和 hello 相關的範圍內的應用程式授與存取。 hello 的角色指派的範圍可以是 Azure 訂用帳戶、 資源群組或單一資源。 RBAC 允許繼承權限。 在父範圍中指派的角色也會授與存取內含 toohello 子系。 使用 RBAC 時，您就可以分隔責任，並授與僅 hello 數量存取 toousers 他們需要 tooperform 他們的工作。 例如，使用 RBAC toolet 一位員工中管理虛擬機器的訂用帳戶，而另一個是可以在 hello 管理 SQL 資料庫使用相同的訂用帳戶。
-   [**VNet 對等**][VNetPeering]。 hello 使用的基本功能的 vDC toocreate hello 基礎結構是 VNet 對等互連，一種機制，在 hello 連接兩個虛擬網路 (Vnet) 透過 hello hello Azure 資料中心網路的同一個地區。

#### <a name="component-type-perimeter-networks"></a>元件類型：周邊網路
[周邊網路][ DMZ]元件 （也稱為 DMZ 網路） 可讓您與您的內部部署或實體的資料中心網路，以及 hello 網際網路從任何連線 tooand tooprovide 網路連線。 它也是您網路和安全性小組可能花費最多時間的位置。

連入封包應該流經 hello 的安全性設備卻在 hello 中樞中，例如 hello 防火牆、 識別碼和 IP 時，才會到達 hello 支點 hello 後端伺服器。 網際網路繫結的封包從 hello 工作負載也應該流經 hello 的安全性設備卻 hello 周邊網路中強制執行原則、 檢查，和稽核時，才退出 hello 網路。

周邊網路元件提供下列功能的 hello:

-   [虛擬網路][VNet]、[UDR][UDR]、[NSG][NSG]
-   [網路虛擬設備][NVA]
-   [負載平衡器][ALB]
-   [應用程式閘道][AppGW] / [WAF][WAF]
-   [公用 IP][PIP]

通常，hello 中央 IT 和安全性的小組可以使用需求定義和操作的 hello 周邊網路的責任。

[![7]][7]

hello 上圖顯示 hello 強制執行的兩個具有存取 toohello 周邊網際網路和內部網路，同時位於 hello 中樞。 在單一的中樞，hello 周邊網路 toointernet 就能相應 toosupport 大量的 Lob，使用多個伺服器陣列的 Web 應用程式防火牆 (WAFs) 及/或防火牆。

[**虛擬網路**] [ VNet] hello 集線器通常建立在多重子網路 toohost hello 不同的服務類型的 VNet 上篩選和檢查從流量 tooor hello NVAs，WAFs，透過網際網路和 Azure 應用程式閘道。

[**UDR**][UDR]：使用 UDR，客戶可以部署防火牆、IDS/IPS 和其他虛擬設備，並透過這些安全性設備來路由傳送網路流量，以強制執行安全性界限原則、稽核和檢查。 在這兩個 hello 中樞和 hello 支點 tooguarantee 流量日透過 hello 特定自訂的 Vm 網路的虛擬應用裝置，hello vDC 所使用的負載平衡器，可以建立 UDRs。 tooguarantee 流量，產生 hello 支點傳輸 toohello 正確虛擬應用裝置中的 Vm 所傳來，UDR 需要 toobe hello 前端 IP 位址的 hello 內部負載平衡器設定為 hello 下個躍點中的 hello 支點 hello 子網路中設定。 hello 內部負載平衡器會將 hello 內部流量 toohello 虛擬應用裝置 （負載平衡器後端集區）。

[![8]][8]

[**網路虛擬裝置**] [ NVA] hello 中樞中的 hello 與透過防火牆和/或 Web 應用程式防火牆 (WAFs) 的伺服器陣列通常管理網際網路存取 toohello 周邊網路。

不同 Lob 通常會使用許多 web 應用程式，而且這些應用程式通常 toosuffer 不同的弱點可能會和潛在的弱點。 Web 應用程式防火牆是產品特殊品種比一般防火牆的更深入地使用 toodetect 攻擊，對 web 應用程式 (HTTP/HTTPS)。 相較於傳統技術防火牆，WAFs 有一組特定的功能 tooprotect 內部 web 伺服器免受威脅。

防火牆伺服陣列是在安全性規則 tooprotect hello 工作負載的一組相同的一般管理裝載 hello 支點和控制存取 tooon 內部部署網路中的 hello 一起運作的防火牆的群組。 防火牆伺服陣列有小於專屬軟體相較於 WAF，但有廣泛的應用程式範圍 toofilter，並查看任何類型的輸出和輸入流量。 防火牆的伺服器陣列通常是透過網路虛擬裝置 (NVAs)，hello Azure marketplace 中可用的實作在 Azure 中。

建議 toouse 一整組 NVAs 來自 hello 網際網路的流量，另一個用於流量來自內部部署。 僅使用一組 NVAs 的兩個會造成安全性風險，因為它所提供的網路流量的 hello 兩組之間沒有安全性範疇。 使用個別 NVAs 可降低 hello 複雜性檢查安全性規則，並清楚哪些規則對應 toowhich 傳入的網路要求。

大部分大型企業都會管理多個網域。 Azure DNS 可以針對特定網域使用的 toohost hello DNS 記錄。 舉一例，可以在 hello A 記錄的 Azure DNS 記錄中註冊 hello hello Azure 外部負載平衡器 （或 hello WAFs） 的虛擬 IP 位址 (VIP)。

[**Azure Load Balancer**][ALB]：Azure Load Balancer 提供高可用性層級 4 (TCP、UDP) 服務，可將連入流量分散到負載平衡組中所定義的服務執行個體。 可轉散發 toohello 負載平衡器前端的端點 （公用 IP 端點或私用 IP 端點），不論後端 IP 位址集區 （範例正在; 位址轉譯 tooa 集傳送流量網路虛擬裝置或 Vm）。

Azure 負載平衡器可以探查 hello 健全狀況的 hello 不同伺服器執行個體，和探查失敗 toorespond hello 負載平衡器會停止傳送流量 toohello 狀況不良的執行個體時。 VDC，在有外部負載平衡器的 hello 與否 hello 中樞 (比方說，平衡 hello 流量 tooNVAs)，在和中 hello 支點 （tooperform 工作類似平衡的多層式應用程式的不同 Vm 之間的流量）。

[**應用程式閘道**][AppGW]：Microsoft Azure 應用程式閘道是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。 它可讓您 toooptimize web 伺服陣列產能卸載 CPU 密集 SSL 終止 toohello 應用程式閘道。 它也提供其他層 7 路由功能，包括循環配置資源發佈的連入流量，cookie 為基礎的工作階段親和性，路徑為基礎的路由 URL，和 hello 能力 toohost 單一應用程式閘道背後的多個網站。 Web 應用程式的防火牆 (WAF) 也會提供 hello 應用程式閘道 WAF SKU 的一部分。 此 SKU 提供保護 tooweb 應用程式，從一般 web 弱點和破解。 應用程式閘道可以設定為面向網際網路的閘道、內部專用閘道或兩者混合。 

[**公用 Ip** ] [ PIP]某些 Azure 功能啟用從存取您 tooassociate 服務端點 tooa 公用 IP 位址，可讓 tooyour 資源 toobe hello 網際網路。 此端點使用 hello Azure 虛擬網路上的網路位址轉譯 (NAT) tooroute 流量 toohello 內部位址和連接埠。 這個路徑是在 hello 的虛擬網路的外部流量 toopass hello 主要方式。 hello 公用 IP 位址可以是設定的 toodetermine 傳入的流量，及如何及在何處轉譯 toohello 虛擬網路上。

#### <a name="component-type-monitoring"></a>元件類型：監視
監視的元件提供可見性，以及從所有警示 hello 其他元件類型。 所有的小組應該具有存取 toomonitoring hello 元件，而且他們擁有存取權的服務。 如果您有中央的說明服務人員或作業小組，他們需要這些元件所提供的整合 toohave 存取 toohello 資料。

Azure 提供不同類型的記錄和監視服務 tootrack hello 行為的 Azure 裝載的資源。 控管和工作負載在 Azure 中的控制項是根據不只收集記錄資料，但也 hello 能力 tootrigger 動作根據特定的報告事件。

Azure 中有兩種主要類型的記錄：

-   [**活動記錄**] [ ActLog] （又稱為同時也是 「 操作記錄檔 」） 提供深入了解 hello hello Azure 訂用帳戶中的資源執行的作業。 這些記錄檔回報 hello 訂用帳戶的控制平面事件。 每個 Azure 資源都會產生稽核記錄。

-   [**Azure 診斷的記錄檔**] [ DiagLog]是資源所產生的記錄，提供豐富、 且經常 hello 該資源的作業有關的資料。 這些記錄檔的 hello 內容會因資源類型。

[![9]][9]

在 vDC，它可以是極為重要 tootrack hello Nsg 記錄檔，特別是這項資訊：

-   [**事件記錄檔**][NSGLog]： 提供哪些 NSG 規則會套用的 tooVMs 和 MAC 位址為基礎的執行個體角色的相關資訊。
-   [**計數器記錄檔**][NSGLog]： 追蹤多少次，每個 NSG 規則已執行的 toodeny 或允許流量。

所有記錄都可以儲存在 Azure 儲存體帳戶中，以進行稽核、靜態分析或備份。 當 hello 記錄檔儲存在 Azure 儲存體帳戶時，客戶可以使用不同類型的架構 tooretrieve 準備、 分析和視覺化這個資料 tooreport hello 狀態和雲端資源的健全狀況。

大型企業應該已有取得的標準架構監視在內部部署系統，可以擴充架構 toointegrate 記錄產生的雲端部署。 適用於想的 tookeep 所有 hello hello 雲端中記錄的組織[Microsoft Operations Management Suite (OMS)] [ OMS]是絕佳的選擇。 因為 OMS 實作為雲端型服務，所以您對基礎結構服務進行最小的投資就可以快速啟動並執行它。 OMS 也可以整合 System Center 元件，例如 System Center Operations Manager tooextend 與現有的管理投資到 hello 的雲端。

OMS 記錄分析是收集的 hello OMS 架構 toohelp 元件、 建立相互關聯、 搜尋和記錄檔和效能資料的動作所產生的作業系統、 應用程式、 雲端基礎結構元件。 它可讓客戶使用整合的搜尋和自訂儀表板 tooanalyze hello 的所有記錄在所有您 vDC 中的工作負載間即時的 operational insights。

#### <a name="component-type-workloads"></a>元件類型：工作負載
工作負載元件是實際應用程式和服務所在的位置。 它也是在應用程式開發小組花費最多時間的位置。

hello 工作負載可能是真的無止盡的。 hello 以下是幾個 hello 可能工作負載類型：

**內部 LOB 應用程式**

特定業務應用程式是企業的電腦的應用程式關鍵 toohello 進行中作業。 LOB 應用程式具有一些共同特性：

-   **互動式**。 LOB 應用程式皆為互動式本質：輸入資料，並傳回結果/報表。
-   **資料驅動**。 LOB 應用程式是經常存取 toohello 資料庫或其他存放裝置需要大量資料。
-   **整合式**。 LOB 應用程式與其他系統內或 hello 組織外部的供應項目整合。

**客戶對向的網站 （網際網路或內部面對）**大部分與 hello 網際網路互動的應用程式是網站。 Azure 提供的 hello 功能 toorun IaaS VM 上，或從網站[Azure Web Apps] [ WebApps]站台 (PaaS)。 Azure Web 應用程式支援允許 hello 部署的 hello Web 應用程式中的 vDC hello 支點的 Vnet 與整合。 Hello VNET 整合，您不需要 tooexpose 網際網路端點，您的應用程式，但可以改用 hello 資源私用非網際網路可路由傳送地址從您的私人 VNet。

**大型的資料分析**當資料需要 tooscale tooa 的非常大型磁碟區時，資料庫可能無法適當縮放。 Hadoop 技術提供系統 toorun 分散式查詢，以平行方式大量的節點上。 客戶有 hello 選項 toorun 資料中的工作負載 IaaS Vm 或 PaaS ([HDInsight][HDI])。 HDInsight 支援部署到以位置為基礎的 VNet，可以是中的 hello vDC 支點部署的 tooa 叢集。

**事件和傳訊**
[Azure 事件中樞][EventHubs]是大規模的遙測擷取服務，能夠收集、轉換和儲存數百萬個事件。 做為分散式的資料流平台，它會提供低延遲及可設定的時間保留，讓您 tooingest 大量的遙測資料至 Azure，並從多個應用程式讀取該資料。 使用事件中樞，單一串流就可以同時支援即時和批次型管線。

應用程式與服務之間的高可靠雲端傳訊服務可以透過 [Azure 服務匯流排][ServiceBus]進行實作，而 Azure 服務匯流排提供用戶端與伺服器之間的非同步代理傳訊，以及結構化先進先出 (FIFO) 傳訊和發佈/訂閱功能。

[![10]][10]

### <a name="multiple-vdc"></a>多重 vDC
目前為止，本文的重點單一 vDC，描述 hello 基本元件，並參與 tooa 彈性 vDC 的架構。 Azure 功能，例如 Azure 負載平衡器，NVAs，可用性設定組，小數位數的集合，以及其他機制參與 tooa 系統可讓您 toobuild 實心 SLA 層級到實際執行服務。

不過，單一 vDC 裝載在單一區域中，而且很容易遭受 toomajor 中斷可能會影響該整個區域。 客戶想 tooachieve 高 Sla 需要透過部署的相同專案中兩個 （或以上） Vdc，放在不同的區域中的 hello tooprotect hello 服務。

在加法 tooSLA 考量，有數種常見的案例，其中部署多個 Vdc 意義：

-   地區/全球支援
-   災害復原
-   DC 之間的機制 toodivert 流量

#### <a name="regionalglobal-presence"></a>地區/全球支援
Azure 資料中心位在全球的許多區域。 當選取多個 Azure 資料中心，客戶需要 tooconsider 兩個相關的因素： 地理位置和延遲。 客戶必須 tooevaluate hello 地理距離 hello Vdc 和 hello 距離 hello vDC hello 一般使用者、 toooffer hello 最佳使用者體驗。

hello Vdc 的裝載位置的 Azure 區域也會需要 tooconform 法規需求，您的組織運作所在的任何法律管轄區來建立。

#### <a name="disaster-recovery"></a>災害復原
工作負載的相關處理，強烈相關的 toohello 類型而 hello 能力 toosynchronize hello 工作負載之間的狀態不同 Vdc hello 實作嚴重損壞復原計畫。 在理想情況下，大部分的客戶想要 toosynchronize 之間執行兩個不同的 Vdc tooimplement 快速的容錯移轉機制中的部署的應用程式資料。 大部分的應用程式機密 toolatency，而且，可能會造成潛在的逾時和延遲的資料同步處理。

不同 vDC 中應用程式的同步或活動訊號監視需要其間的通訊。 不同區域中的兩個 vDC 可以透過進行連線：

-   當 hello vDC 集線器連接的 toohello ExpressRoute 私人互連相同 ExpressRoute 電路
-   透過您公司的中樞和 vDC 網狀結構連接多個 ExpressRoute 電路連接的 toohello ExpressRoute 電路
-   每個 Azure 區域中 vDC 中樞之間的站對站 VPN 連線

通常 hello ExpressRoute 連線時，慣用的 hello 機制，因為較高的頻寬和一致延遲傳送 hello Microsoft 骨幹透過。

沒有任何 magic 配方 toovalidate 位於不同的區域中的兩個 （或以上） 不同的 Vdc 間發佈的應用程式。 客戶應該在執行網路限定性條件測試 tooverify hello 延遲和頻寬的 hello 連線和目標資料同步或非同步複寫是否適當，以及哪些 hello 最佳復原時間目標 (RTO) 可以是適用於您工作負載。

#### <a name="mechanism-toodivert-traffic-between-dc"></a>DC 之間的機制 toodivert 流量
一個有效的技術 toodivert hello 流量傳入一個 DC tooanother 中是以 DNS 為基礎。 [Azure Traffic Manager] [ TM]使用 hello 網域名稱系統 (DNS) 機制 toodirect hello 使用者流量 toohello 最適合公用端點中特定 vDC。 透過探查，Traffic Manager 會定期檢查的公用端點，在不同的 Vdc hello 服務健全狀況和失敗時的這些端點，它會路由傳送自動 toohello 次要 vDC。

Traffic Manager 適用於 Azure 的公用端點，而且可以使用，例如 toocontrol/轉向流量 tooAzure Vm 和 hello Web 應用程式適當的 vDC。 Traffic Manager 後的恢復，即使在整個 Azure 地區執行失敗的 hello 字體，並可以控制 hello 的使用者流量分配不同 Vdc 根據準則中的服務端點 (例如，在特定的 vDC，服務失敗或選取hello vDC hello 網路延遲最小 hello 用戶端使用)。

### <a name="conclusion"></a>結論
hello 虛擬資料中心是到且可擴充的架構，在 Azure 中以充分發揮雲端資源使用時，降低成本並簡化系統使用的特色與功能 toocreate 組合的 hello 雲端方法 toodata center 移轉控管。 hello vDC 概念為基礎的中樞-支點拓撲，提供一般 hello 中樞中的共用的服務和 hello 支點中允許特定應用程式/工作負載。 VDC 與 hello 結構公司角色，其中不同部門 （中央 IT、 DevOps、 作業和維護） 搭配使用，每個都有特定的角色和責任清單相符。 VDC 滿足 hello"提起和 Shift 」 移轉需求，但也會提供許多優點 toonative 雲端部署。

## <a name="references"></a>參考
下列功能的 hello 我們已經討論過此文件中。 按一下 更多的 hello 連結 toolearn。

| | | |
|-|-|-|
|網路功能|負載平衡|連線能力|
|[Azure 虛擬網路][VNet]</br>[網路安全性群組][NSG]</br>[NSG 記錄][NSGLog]</br>[使用者定義路由][UDR]</br>[網路虛擬設備][NVA]</br>[公用 IP 位址][PIP]|[Azure Load Balancer (L3) ][ALB]</br>[應用程式閘道 (L7) ][AppGW]</br>[Web 應用程式防火牆][WAF]</br>[Azure 流量管理員][TM] |[VNet 對等][VNetPeering]</br>[虛擬私人網路][VPN]</br>[ExpressRoute][ExR]
|身分識別</br>|監視</br>|最佳做法</br>|
|[Azure Active Directory][AAD]</br>[Multi-Factor Authentication][MFA]</br>[角色型存取控制][RBAC]</br>[預設 AAD 角色][Roles] |[活動記錄][ActLog]</br>[診斷記錄][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[周邊網路最佳做法][DMZ]</br>[訂用帳戶管理][SubMgmt]</br>[資源群組管理][RGMgmt]</br>[Azure 訂用帳戶限制][Limits] |
|其他 Azure 服務|
|[Azure Web Apps][WebApps]</br>[HDInsights (Hadoop) ][HDI]</br>[事件中樞][EventHubs]</br>[服務匯流排][ServiceBus]|



## <a name="next-steps"></a>後續步驟
 - 瀏覽[對等互連的 VNet][VNetPeering]、 hello 支柱技術 vDC 中樞和支點設計
 - 實作[AAD] [ AAD] tooget 入門[RBAC] [ RBAC]瀏覽
 - 開發訂用帳戶和資源的管理模型和 RBAC toomeet hello 架構需求，模型和您的組織原則。 規劃 hello 最重要活動。 請盡快規劃重組、合併、新的產品線等。

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "元件重疊範例" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "高階中樞和支點 vDC 範例"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "中樞和支點叢集"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "支點對支點"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Hello vDC 的區塊層級圖表"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "使用者、群組、訂用帳戶和專案"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "高階基礎結構圖"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "高階基礎結構圖"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "VNet 對等和周邊網路"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "高階監視圖"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "高階工作負載圖"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
