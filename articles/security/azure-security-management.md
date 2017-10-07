---
title: "在 Azure 中的 aaaEnhance 遠端管理安全性 |Microsoft 文件"
description: "本文探討管理 Microsoft Azure 環境時提升遠端管理安全性的步驟，這些環境包括雲端服務、虛擬機器及自訂應用程式。"
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Azure 的安全性管理
Azure 訂閱者可從多種裝置管理其雲端環境，這些裝置包括管理工作站、開發人員的電腦，甚至是具有工作專用權限的特殊權限使用者裝置。 在某些情況下，透過網頁型主控台，例如 hello 執行系統管理功能[Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 在其他情況下，可能會從內部部署系統直接連線 tooAzure 透過虛擬私人網路 (Vpn)、 終端機服務、 用戶端應用程式通訊協定，或 （以程式設計的方式） hello Azure 服務管理 API (SMAPI)。 此外，用戶端端點也可以加入網域或是遭到隔離且不受管理，例如平板電腦或智慧型手機。

雖然多個存取和管理功能提供一組豐富的選項，但變化性可以加入極大的風險 tooa 雲端部署。 可能很難 toomanage，追蹤和稽核系統管理動作。 這些變化可能也會導入透過非法的存取 tooclient 端點，用來管理雲端服務的安全性威脅。 使用一般工作站或私人工作站來開發和管理基礎結構將會打開無法預期的威脅媒介，例如網頁瀏覽 (例如水坑攻擊) 或電子郵件 (例如社交工程和網路釣魚)。

![][1]

在這種環境中的 hello 潛在攻擊增加，因為它是一項挑戰 tooconstruct 安全性原則和機制 tooappropriately 管理來自各種廣泛的端點存取 tooAzure 介面 （例如 SMAPI)。

### <a name="remote-management-threats"></a>遠端管理威脅
攻擊者通常會嘗試 toogain 特殊權限存取危害帳戶認證 （例如，透過密碼破解強制、 網路釣魚和認證蒐集），或誘騙執行有害的程式碼 （例如，從有害的網站，提供的使用者磁碟機依照下載或從有害的電子郵件附件)。 在遠端受管理的雲端環境中，帳戶缺口，這可能會導致 tooan 增加風險到期 tooanywhere，隨時存取。

主要的系統管理員帳戶的嚴格控制，即使有較低層級的使用者帳戶可以是使用的 tooexploit 弱點的安全性策略。 缺乏適當的安全性訓練也可能會導致 toobreaches 透過無意間洩露或之帳戶資訊的曝光。

若使用者工作站也用來執行系統管理工作，便可能會在許多不同的地方遭到入侵。 使用者已瀏覽 hello web、 使用第 3 廠商和開放原始碼工具，或開啟有害的文件檔案，其中包含一種特洛伊程式。

一般情況下，導致資料缺口，這可能是最目標的攻擊所追蹤的 toobrowser 破解、 外掛程式 （例如 PDF、 Flash Java) 和桌面的電腦上的矛網路釣魚 （電子郵件）。 這些電腦可能會有系統管理層級或服務層級權限 tooaccess 即時伺服器或網路作業時用於開發或管理的其他資產的裝置。

### <a name="operational-security-fundamentals"></a>作業安全性基本概念
對於更安全的管理與作業，您可以藉由減少 hello 可能進入點的數目降低用戶端的受攻擊面。 這可以透過下列安全性原則來達成：「區分職責」和「隔離環境」。

找出機密函式，從另一個 toodecrease hello 可能性一個層級的錯誤會導致 tooa 漏洞，在另一個。 範例：

* 系統管理工作不應該結合可能會導致 tooa 洩露 （例如，惡意程式碼中然後感染基礎結構伺服器的系統管理員的電子郵件） 的活動。
* 高敏感度作業所使用的工作站不應該是同一個系統用於高風險的用途，例如瀏覽 hello 網際網路 hello。

移除不必要的軟體，以減少 hello 系統的受攻擊面。 範例：

* 標準的系統管理、 支援或開發工作站應該不需要安裝電子郵件用戶端或其他產能應用程式如果 hello 裝置的主要用途是 toomanage 雲端服務。

用戶端系統具有系統管理員存取 tooinfrastructure 元件皆應受到 toohello 嚴格可能原則 tooreduce 安全性風險。 範例：

* 安全性原則可以包含從 hello 裝置和嚴格防火牆組態的使用拒絕開放網際網路存取的群組原則設定。
* 如果需要直接存取，請使用網際網路通訊協定安全性 (IPsec) VPN。
* 針對管理和開發設定不同的 Active Directory 網域。
* 隔離和篩選管理工作站的網路流量。
* 使用反惡意程式碼軟體。
* 實作失竊認證的多因素驗證 tooreduce hello 風險。

合併存取資源和避免使用未受管理的端點也可簡化管理工作。

### <a name="providing-security-for-azure-remote-management"></a>為 Azure 的遠端管理提供安全性
Azure 提供的安全性機制 tooaid 系統管理員管理 Azure 雲端服務和虛擬機器。 這些機制包括︰

* 驗證和[角色型存取控制](../active-directory/role-based-access-control-configure.md)。
* 監視、記錄和稽核。
* 憑證和加密通訊。
* Web 管理入口網站。
* 網路封包篩選。

使用用戶端安全性設定及管理閘道器的資料中心部署，就可能 toorestrict 和監視系統管理員存取 toocloud 應用程式和資料。

> [!NOTE]
> 本文的某些建議可能會導致資料、網路或計算資源使用量增加，並可能增加授權或訂用帳戶成本。
>
>

## <a name="hardened-workstation-for-management"></a>強化管理工作站
強化工作站的 hello 目標 tooeliminate 所有但 hello 最重要的功能所需 toooperate，使潛在攻擊面 hello 越小越好。 系統強化包含已安裝的服務和應用程式，限制應用程式執行時，限制網路存取 tooonly 功能所需的 hello 數目降到最低，並一律保留向上 toodate hello 系統。 此外，使用經過強化的管理工作站能夠將系統管理工具和活動與其他使用者工作隔離開來。

在內部部署企業環境中，您可以限制 hello 實體基礎結構透過專用的管理網路、 卡，可以存取的伺服器聊天室和工作站上 hello 網路的受保護區域執行的受攻擊面。 在雲端或混合式 IT 模型中，正在努力一些，安全管理服務可能更複雜的實體存取 tooIT 資源 hello 不足。 實作保護解決方案需要小心軟體設定、安全性為主的處理程序及完善的原則。

使用雲端管理鎖定工作站中最小權限的最小化的軟體磁碟使用量，和應用程式開發，可以降低的安全性事件的 hello 風險標準化 hello 遠端管理和開發環境。 強化的工作站設定將有助於防止 hello 損害關閉惡意程式碼和入侵所使用的許多常見提供使用的 toomanage 任務雲端資源的帳戶。 具體而言，您可以使用[Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx)和 HYPER-V 技術 toocontrol 隔離用戶端系統行為並減輕潛在威脅，包括電子郵件或瀏覽網際網路。

強化工作站上，hello 系統管理員會執行標準使用者帳戶 （它會封鎖執行系統管理層級） 和相關聯的應用程式，皆受允許清單。 強化工作站 hello 基本項目如下所示：

* 作用中的掃描和修補。 部署反惡意程式碼軟體、 執行規則的弱點可能會掃描，以及適時使用 hello 最新安全性更新來更新所有工作站。
* 有限的功能。 解除安裝任何不需要的應用程式，並停用不必要的 (啟動) 服務。
* 強化網路。 使用 Windows 防火牆規則 tooallow 唯一有效的 IP 位址、 連接埠和 Url 相關的 tooAzure 管理。 請確定輸入的遠端連線 toohello 工作站也會封鎖。
* 執行限制。 允許只有一組預先定義的可執行檔所需的管理 toorun （又稱為 tooas 「 預設拒絕 」）。 根據預設，使用者應拒絕權限 toorun 除非 hello 中明確定義的任何程式允許清單。
* 最小特殊權限。 本身 hello 本機電腦上，管理工作站使用者應該沒有任何系統管理權限。 如此一來，他們無法變更 hello 系統設定] 或 [hello 系統檔案，有意或無意。

您可以使用強制執行這所有[群組原則物件](https://www.microsoft.com/download/details.aspx?id=2612)(Gpo) 在 Active Directory 網域服務 (AD DS)，並將其套用到 (local) 管理網域 tooall 管理帳戶。

### <a name="managing-services-applications-and-data"></a>管理服務、應用程式和資料
Azure 雲端服務設定為透過 hello Azure 入口網站或 SMAPI，執行透過 hello Windows PowerShell 命令列介面或自訂應用程式利用這些 RESTful 介面。 使用這些機制的服務包括 Azure Active Directory (Azure AD)、Azure 儲存體、Azure 網站和 Azure 虛擬網路等。

虛擬機器部署的應用程式提供自己的用戶端工具和介面，如有需要例如 hello Microsoft Management Console (MMC)、 （例如 Microsoft System Center 或 Windows Intune） 的企業管理主控台或另一個管理應用程式，Microsoft SQL Server Management Studio 中，例如。 這些工具通常位在企業環境或用戶端網路中。 它們可能仰賴需要直接、具狀態之連線的特定網路通訊協定，例如遠端桌面通訊協定 (RDP)。 有些可能會有不應該公開已發行或可透過 hello 網際網路存取的 web 介面。

您可以使用來限制在 Azure 中的存取 tooinfrastructure 與平台服務管理[多重要素驗證](../multi-factor-authentication/multi-factor-authentication.md)， [X.509 管理憑證](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)，和防火牆規則。 hello Azure 入口網站和 SMAPI 需要傳輸層安全性 (TLS)。 不過，服務和您部署至 Azure 的應用程式需要您 tootake 適合您的應用程式為基礎的保護措施。 這些機制可以透過標準化的強化後工作站組態更容易地經常啟用。

### <a name="management-gateway"></a>管理閘道
toocentralize 所有系統管理存取並簡化監視和記錄，您可以部署專用[遠端桌面閘道](https://technet.microsoft.com/library/dd560672)（RD 閘道） 伺服器，在您內部網路，連線的 tooyour Azure 環境。

遠端桌面閘道是以原則為基礎 RDP Proxy 服務，會強制執行安全性需求。 同時實作 RD 閘道與 Windows Server 網路存取保護 (NAP)，可協助確保只有符合 Active Directory 網域服務 (AD DS) 群組原則物件 (GPO) 所建立之特定安全性健全狀況準則的用戶端可以連線。 此外：

* 佈建[Azure 管理憑證](http://msdn.microsoft.com/library/azure/gg551722.aspx)hello RD 閘道上，以便允許 hello 唯一主機 tooaccess hello Azure 入口網站。
* 加入 hello RD 閘道 toohello 相同[管理網域](http://technet.microsoft.com/library/bb727085.aspx)如 hello 的管理員工作站。 這是必要的當您使用站對站 IPsec VPN 或 ExpressRoute 具有單向信任 tooAzure AD、 在網域內，或您正在同盟認證之間您內部部署 AD DS 的執行個體與 Azure AD。
* 設定[用戶端連線授權原則](http://technet.microsoft.com/library/cc753324.aspx)toolet hello RD 閘道確認 hello 用戶端電腦名稱是否有效 （網域），以及允許的 tooaccess hello Azure 入口網站。
* 使用 IPsec 的[Azure VPN](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther 防止竊聽和權杖遭竊，管理流量，或考慮隔離的網際網路連結透過[Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/)。
* 針對透過 RD 閘道登入的系統管理員啟用 Multi-Factor Authentication (透過 [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)) 或智慧卡驗證。
* 設定來源[IP 位址限制](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/)或[網路安全性群組](../virtual-network/virtual-networks-nsg.md)中允許的管理端點的 Azure toominimize hello 數目。

## <a name="security-guidelines"></a>安全性方針
一般情況下，協助 toosecure 的管理員工作站，搭配 hello 雲端使用任何工作站內部部署的類似 toohello 作法 — 例如，最小化，建置和嚴格的權限。 雲端管理某些唯一方面會更 akin tooremote 或企業的頻外管理。 其中包括使用 hello 和認證、 安全的遠端存取和威脅偵測和回應的稽核。

### <a name="authentication"></a>驗證
您可以使用 Azure 登入限制 tooconstrain 來源 IP 位址來存取系統管理工具和稽核存取要求。 toohelp Azure 識別管理的用戶端 （工作站和/或應用程式），您可以設定 SMAPI （透過客戶開發工具，例如 Windows PowerShell cmdlet） 和 hello Azure 入口網站 toorequire 用戶端管理憑證 toobe除了安裝 tooSSL 憑證。 我們也建議系統管理員存取需要 Multi-Factor Authentication。

您部署至 Azure 的某些應用程式或服務可能會針對使用者和系統管理員存取擁有自己的驗證機制，而其他應用程式或服務則會充分利用 Azure AD。 根據是否您正在同盟認證能夠透過 Active Directory Federation Services (AD FS) 使用目錄同步作業或維護使用者帳戶，只在 hello 雲端，使用[Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) （屬於Azure AD Premium) 可協助您管理 hello 資源之間的身分識別生命週期。

### <a name="connectivity"></a>連線能力
數種機制是可用 toohelp 安全用戶端連線 tooyour Azure 虛擬網路。 這些機制，其中兩個[站對站 VPN](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) 和[點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S)，啟用 hello 使用業界標準 IPsec (S2S) 或 hello[安全通訊端通道通訊協定](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) 來加密和通道。 當 Azure 連線 toopublic 向 Azure 服務管理，例如 hello Azure 入口網站時，Azure 會需要超文字傳輸通訊協定安全性 (HTTPS)。

不會透過 RD 閘道連線 tooAzure 獨立強化的工作站應該使用 hello 以 SSTP 為基礎點對站 VPN toocreate hello 初始連線 toohello Azure 虛擬網路，然後再建立 RDP 連線 tooindividual 虛擬從機器與 hello VPN 通道。

### <a name="management-auditing-vs-policy-enforcement"></a>管理稽核與原則強制執行
一般而言，有兩種方法，可幫助 toosecure 管理程序： 稽核和原則強制執行。 同時採用這兩種方法可進行全面控制，但並非所有情況下都能這麼做。 此外，每一種方法具有不同的層級相關聯管理安全性，特別是在關聯 toohello 放在個人和系統架構的信任層級的投入時間、 成本和風險。

監視、 記錄和稽核提供進行追蹤，以及了解管理活動，但它不一定可行 tooaudit 中的所有動作都完成到期 toohello 所產生的資料數量的詳細資料。 稽核的 hello 管理原則的 hello 效率是最佳作法，不過。

包含嚴格存取控制的原則強制執行具有可控制系統管理員動作的程式設計機制，並可協助確保使用所有可能的保護措施。 記錄提供強制執行哪些作業的人員，從位置和時間的加法 tooa 記錄中的證明。 記錄 」 還可讓您 tooaudit 與 crosscheck 資訊系統管理員如何遵循原則，並提供活動的辨識項

## <a name="client-configuration"></a>用戶端組態
針對強化後的工作站，我們有三種主要組態建議。 hello 兩者之間的最大區別因素是成本、 可用性和存取範圍，維持類似的安全性設定檔跨所有選項。 下表中的 hello 可提供簡短的 hello 效益和風險 tooeach 分析。 （請注意，「 公司電腦 」 是指 tooa 標準桌面的電腦組態設定，將部署所有的網域使用者，不論角色）。

| 組態 | 優點 | 缺點 |
| --- | --- | --- |
| 獨立的強化後工作站 |受到嚴格控制的工作站 |專用桌上型電腦的成本較高 |
| - | 降低應用程式入侵風險 |增加管理工作 |
| - | 清楚區分職責 | - |
| 以公司電腦做為虛擬機器 |降低硬體成本 | - |
| - | 隔離角色和應用程式 | - |
| Windows toogo 搭配 BitLocker 磁碟機加密 |與大部分電腦相容 |資產追蹤 |
| - | 符合成本效益且具有可攜性 | - |
| - | 隔離的管理環境 |- |

請務必確認 hello 強化的工作站為 hello 主機，hello 客體，沒有 hello 裝載作業的系統和 hello 硬體。 遵循 hello"清理來源原則 」 (也稱為 「 安全 origin") 表示該 hello 主機應該 hello 最強化。 否則，hello 強化的工作站 （客體） 是主體 tooattacks hello 其裝載所在的系統上。

您可以進一步隔離系統管理功能，透過專用的系統映像的每一個強化工作站只 hello 工具和權限所需管理選取 Azure 和雲端應用程式，與 特定本機 AD DS 的 Gpo hello必要的工作。

IT 環境中有不在內部部署基礎結構 (例如，沒有存取 tooa hello 雲端中的所有伺服器都是因為 Gpo 的執行個體本機 AD DS)，例如服務[Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx)可以簡化部署和維護工作站組態。

### <a name="stand-alone-hardened-workstation-for-management"></a>用於管理的獨立強化後工作站
使用獨立的強化後工作站時，系統管理員會使用一部電腦或膝上型電腦來進行系統管理工作，並使用另一個不同的電腦或膝上型電腦來進行非系統管理工作。 專用的工作站 toomanaging 您的 Azure 服務不需要安裝其他應用程式。 此外，使用的工作站若支援[信賴平台模組](https://technet.microsoft.com/library/cc766159) (TPM) 或類似的硬體層級密碼編譯技術，將有助於進行裝置驗證和預防特定攻擊。 TPM 也可以使用支援 hello 系統磁碟機的完整磁碟區保護[BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)。

在 hello 獨立的強化的工作站案例中 （如下所示），hello 本機執行個體的 Windows 防火牆 （或非 Microsoft 用戶端防火牆） 是設定的 tooblock 輸入連線，例如 RDP。 hello 系統管理員可以登入 toohello 強化的工作站和 tooAzure 連線建立 VPN 連線與 Azure 虛擬網路，但無法登入 tooa 公司電腦，並使用 RDP tooconnect toohello 之後的 RDP 工作階段的開始強化工作站它本身。

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>以公司電腦做為虛擬機器
在不同的獨立強化的工作站成本高昂或不太方便，hello 的情況下強化的工作站可以裝載虛擬機器 tooperform 非系統管理工作。

![][3]

tooavoid 數個安全性風險，可能會產生一個工作站使用系統管理和其他日常工作的工作，您可以部署 Windows HYPER-V 虛擬機器 toohello 強化工作站。 此虛擬機器可以做為 hello 公司電腦。 hello 公司的 PC 環境可以依然隔離在 hello 主機，而減少其攻擊面和移除 hello 使用者日常活動 （例如電子郵件） 共存機密的系統管理工作。

hello 公司的 PC 虛擬機器會在受保護的空間，並提供使用者應用程式。 hello 主機會維持 「 全新來源 」，並強制執行嚴格的網路原則中 hello 根作業系統 （例如，封鎖從進行 RDP 存取 hello 虛擬機器）。

### <a name="windows-toogo"></a>Windows tooGo
另一個替代 toorequiring 獨立的強化工作站是 toouse [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx)磁碟機是否支援用戶端 USB 開機功能的功能。 Windows tooGo 可讓使用者 tooboot 相容 PC tooan 隔離的系統映像從加密的 USB 快閃磁碟機執行。 因為 hello 映像可以完全管理的公司的 IT 團隊，有嚴格的安全性原則，最少的作業系統組建，而且 TPM 支援，它可以提供的遠端系統管理端點的其他控制項。

在下圖中 hello，hello 可攜式影像是已加入網域的系統是預先設定的 tooconnect 只有 tooAzure，需要多因素驗證，以及封鎖所有非管理流量。 如果使用者開機 hello 相同 PC toohello 標準公司映像和 Azure 的管理工具存取 RD 閘道的嘗試，hello 工作階段的封鎖。 Windows tooGo 變成 hello 根層級的作業系統，而且沒有其他圖層需要 （主機作業系統、 hypervisor、 虛擬機器），可能會更容易遭受 toooutside 攻擊。

![][4]

USB 快閃磁碟機是平均的桌上型電腦比更輕鬆地遺失的重要 toonote 它。 使用 BitLocker tooencrypt hello 整個磁碟區，連同強式密碼，可讓您比較不可能的攻擊者可將 hello 磁碟機映像，用於有害的用途。 此外，如果遺失 hello USB 快閃磁碟機、 撤銷和[發出新的管理憑證](https://technet.microsoft.com/library/hh831574.aspx)以及快速密碼重設可以降低風險。 管理稽核記錄檔位於在 Azure 中，不是在用戶端 hello，進一步減少資料遺失。

## <a name="best-practices"></a>最佳作法
請考慮下列額外的指導方針，當您管理應用程式和資料在 Azure 中的 hello。

### <a name="dos-and-donts"></a>建議事項和避免事項
請勿假設，工作站已經鎖定，因為其他常見的安全性需求不需要符合 toobe。 hello 潛在的風險是更高版本的因為系統管理員帳戶通常擁有提升權限的存取層級。 在 hello 表中顯示的風險和其替代的安全作法的範例。

| 避免事項 | 建議事項 |
| --- | --- |
| 請勿以電子郵件寄送用於系統管理員存取權或其他機密資料的認證 (例如 SSL 或管理憑證) |用聲音提供帳戶名稱和密碼 (但不要將它們儲存在語音郵件中) 以維持機密性、遠端安裝用戶端/伺服器憑證 (透過加密工作階段)、從受保護的網路共用下載，或透過卸除式媒體手動發佈。 |
| - | 主動管理您的管理憑證生命週期。 |
| 請勿在應用程式儲存體中儲存未加密或未雜湊的帳戶密碼 (例如在試算表、SharePoint 網站或檔案共用中)。 |建立安全性管理原則和系統強化原則，並將其套用 tooyour 開發環境。 |
| - | 使用[增強補救經驗 Toolkit 5.5](https://technet.microsoft.com/security/jj653751)釘選的憑證規則 tooensure 適當存取 tooAzure SSL/TLS 站台。 |
| 請勿讓系統管理員共用帳戶和密碼，或在多個使用者帳戶或服務重複使用密碼，特別是用於社交媒體或其他非系統管理活動的帳戶或服務。 |您的 Azure 訂閱建立專用的 Microsoft 帳戶 toomanage — 不是個人的電子郵件帳戶。 |
| 請勿以電子郵件寄送組態檔。 |應該從信任的來源 (例如，加密的 USB 快閃磁碟機) 而非從可輕易入侵的機制 (例如電子郵件) 安裝組態檔和設定檔。 |
| 請勿使用弱式或簡單的登入密碼。 |強制使用強式密碼原則、到期循環 (首次使用時變更)、主控台逾時和自動帳戶鎖定。 使用用戶端密碼管理系統搭配 Multi-Factor Authentication 來存取密碼保存庫。 |
| 不會公開管理連接埠 toohello 網際網路。 |Azure 的連接埠及 IP 位址 toorestrict 管理存取權的鎖定。 如需詳細資訊，請參閱 hello [Azure 網路安全性](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx)技術白皮書。 |
| - | 針對所有管理連線使用防火牆、VPN 和 NAP。 |

## <a name="azure-operations"></a>Azure 作業
在 Microsoft 的 Azure 作業內，存取 Azure 之生產系統的作業工程師和支援人員，會使用[強化後的工作站電腦與其中所佈建的 VM](#stand-alone-hardened-workstation-for-management)來進行內部的公司網路存取和執行應用程式 (例如電子郵件、內部網路等)。 所有的管理工作站電腦具有 Tpm 的、 hello 主機開機磁碟機加密使用 BitLocker，而且也有聯結的 tooa 特殊組織單位 (OU) 中 Microsoft 的主要公司網域。

系統強化是透過群組原則以集中式的軟體更新來強制執行。 稽核和分析會收集從管理工作站 （例如安全性和 AppLocker） 的事件記錄檔，並將其儲存 tooa 中央位置中。

此外，專用的跳躍方塊 Microsoft 的網路上需要雙因素驗證是使用的 tooconnect tooAzure 生產網路。

## <a name="azure-security-checklist"></a>Azure 安全性檢查清單
Hello 系統管理員可以強化工作站執行的工作數目降到最低，可協助您開發和管理環境的 hello 受攻擊面降至最低。 下列技術 toohelp 使用 hello 保護您的強化的工作站：

* IE 強化。 hello Internet Explorer 瀏覽器 （或任何網頁瀏覽器，而且） 為有害的程式碼，因為 tooits 廣泛互動外部伺服器的索引鍵項目點。 請檢閱您的用戶端原則並強制要求在受保護模式中執行、停用附加元件、停用檔案下載，以及使用 [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx) 篩選。 確定會顯示安全性警告。 利用網際網路區域，並建立已為其設定合理強化的信任網站清單。 封鎖其他所有網站和瀏覽器中的程式碼，例如 ActiveX 和 Java。
* 標準使用者。 執行標準的使用者帶來許多好處，其中最大的 hello 是竊取系統管理員認證，透過惡意程式碼則更為困難。 此外，標準使用者帳戶沒有 hello 根作業系統的提高權限的權限，而且許多組態選項和應用程式開發介面而被鎖定預設。
* AppLocker。 您可以使用[AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello 程式和使用者可以執行的指令碼。 您可以在稽核或強制模式中執行 AppLocker。 根據預設，AppLocker 會有允許規則，可讓使用者擁有系統管理語彙基元 toorun hello 用戶端上的所有程式碼。 此規則存在 tooprevent 系統管理員鎖定，並將其套用只有 tooelevated 語彙基元。 另請參閱做為 Windows Server [核心安全性](http://technet.microsoft.com/library/dd348705.aspx)一部分的「程式碼完整性」。
* 程式碼簽署。 為系統管理員使用的所有工具和指令碼進行程式碼簽署，可提供方便管理的機制來部署應用程式鎖定原則。 雜湊不縮放與快速變更 toohello 程式碼，且檔案路徑不提供較高的安全性等級。 您應該使用 PowerShell 來結合 AppLocker 規則[執行原則](http://technet.microsoft.com/library/ee176961.aspx)只允許特定已簽署的程式碼和指令碼 toobe[執行](http://technet.microsoft.com/library/hh849812.aspx)。
* 群組原則。 建立全域的系統管理原則會套用的 tooany 網域的工作站，用於管理 （並封鎖存取，從其他所有項目），和在這些工作站上的 toouser 帳戶通過驗證。
* 已增強安全性的佈建。 保護您的基準強化的工作站映像 toohelp 避免遭到竄改。 使用安全性措施，例如加密和隔離 toostore 影像、 虛擬機器及指令碼，並限制存取 （可能是使用可稽核核取-在/簽出程序）。
* 修補。 維護一致的組建 （或有不同的映像的開發、 作業和其他系統管理工作） 會掃描變更和惡意程式碼而例行性，保留 hello 增多 toodate，並只在必要時，啟用機器。
* 加密。 請確定管理工作站已安全地讓 TPM toomore[加密檔案系統](https://technet.microsoft.com/library/cc700811.aspx)(EFS) 與 BitLocker。 如果您使用 Windows tooGo，使用只有加密的 USB 金鑰搭配 BitLocker。
* 控管。 使用 AD DS Gpo toocontrol 所有 hello 系統管理員 Windows 介面，如檔案共用。 將管理工作站納入稽核、監視和記錄程序內。 追蹤所有系統管理員和開發人員的存取和使用活動。

## <a name="summary"></a>摘要
使用強化後的工作站組態來管理 Azure 雲端服務、虛擬機器和應用程式，可協助您避免遠端管理重要 IT 基礎結構所產生的眾多風險和威脅。 Azure 和 Windows 提供機制，您可以採用 toohelp 保護與控制通訊、 驗證和用戶端的行為。

## <a name="next-steps"></a>後續步驟
hello 下列資源，可用 tooprovide Azure 相關的一般資訊及相關 Microsoft 服務，在這份文件中所參考的加法 toospecific 項目：

* [設定安全性權限存取](https://technet.microsoft.com/library/mt631194.aspx)– 取得 hello 技術詳細資料來設計及建置安全的系統管理工作站，以 Azure 管理
* [Microsoft 信任中心](https://www.microsoft.com/TrustCenter/Security/AzureSecurity)-了解 Azure 平台功能來保護 hello Azure 網狀架構並 hello Azure 上執行的工作負載
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) -Microsoft 安全性漏洞，包括 Azure 中，問題可能會報告或透過電子郵件太[secure@microsoft.com](mailto:secure@microsoft.com)
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)– 保持在最新的 Azure 安全性的 hello toodate

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
