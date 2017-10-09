---
title: "開始使用 Microsoft Azure 安全性的 aaaGetting |Microsoft 文件"
description: "本文提供 Microsoft Azure 的安全性功能和一般考量組織移轉其資產 tooa 雲端提供者的概觀。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>開始使用 Microsoft Azure 安全性
當您建立或移轉 IT 資產 tooa 雲端提供者時，您依賴在該組織的能力 tooprotect 應用程式和 hello 服務與 hello 控制項提供您以雲端為基礎的資產的 toomanage hello 安全性資料。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂安全性 toomeet hello 獨特需求您的部署。

在這篇 Azure 安全性概觀文章中，我們將探討：

* Azure 服務和功能，您可以使用 toohelp 保護您的服務和 Azure 中的資料。
* Microsoft 保護 hello Azure 基礎結構 toohelp 如何保護您的資料和應用程式。

## <a name="identity-and-access-management"></a>身分識別和存取管理
控制存取 tooIT 基礎結構、 資料和應用程式很重要。 Microsoft Azure 提供這些功能，例如 Azure Active Directory (Azure AD)、Azure 儲存體等服務，並且支援多項標準和 API。

[Azure AD](../active-directory/active-directory-whatis.md) 是一種身分識別儲存機制和引擎，可提供組織的使用者、群組和物件的驗證、授權和存取控制功能。 Azure AD 也提供開發人員在其應用程式的有效方式 toointegrate 身分識別管理。 業界標準通訊協定如 [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0)、[WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) 和 [OpenID Connect](http://openid.net/connect/) 讓您得以憑藉 .NET、Java、Node.js 和 PHP 的平台實作登入功能。

hello 以 REST 為基礎的 Graph API 可讓您從任何平台的開發人員 tooread 」 和 「 寫入 toohello 目錄。 透過所提供的 [OAuth 2.0](http://oauth.net/2/) 支援，開發人員不僅可以建置整合了 Microsoft 與第三方 Web API 的行動應用程式及 Web 應用程式，還可建置自己的安全 Web API。 現已提供各種適用於 .Net、Windows 市集、iOS 和 Android 的開放原始碼用戶端程式庫，而且另有更多的程式庫仍在開發當中。

### <a name="how-azure-enables-identity-and-access-management"></a>Azure 如何啟用身分識別與存取管理
Azure AD 可以作為組織的獨立式雲端目錄，或在您現有的內部部署 Active Directory 中作為整合式解決方案。 整合功能包括目錄同步和單一登入 (SSO)。 這些將現有的內部部署身分識別 hello 觸角延伸至 hello 雲端，並改善 hello 系統管理員和使用者體驗。

身分識別與存取管理的一些其他功能包括：

* Azure AD 可讓[SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS 應用程式，不論裝載的位置。 有些應用程式會與 Azure AD 同盟，有些則使用密碼 SSO。 同盟應用程式也支援使用者佈建和密碼儲存庫存。
* 在存取 toodata [Azure 儲存體](https://azure.microsoft.com/services/storage/)控制透過驗證。 每個儲存體帳戶有主索引鍵 ([儲存體帳戶金鑰](https://msdn.microsoft.com/library/azure/ee460785.aspx)，或 SAK) 和次要的秘密金鑰 （hello 共用的存取簽章或 SAS）。
* Azure AD 可透過與內部部署目錄的同盟、同步和複寫提供「身分識別即服務」(使用 [Active Directory Federation Services](../active-directory/fundamentals-identity.md))。
* [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)是 hello 多因素驗證服務，需要使用行動裝置應用程式、 電話或簡訊來進行使用者 tooverify 登入。 它可以搭配 Azure AD toohelp 安全的內部資源與 hello Azure Multi-factor Authentication server，以及自訂應用程式和使用 hello SDK 的目錄。
* [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)可讓您將 Azure 虛擬機器 tooa 網域，而不需部署網域控制站。 您可以使用 Active Directory 公司認證登入 toothese 虛擬機器，且您 Azure 的虛擬機器上使用群組原則 tooenforce 安全性基準管理已加入網域的虛擬機器。
* [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)提供縮放 toohundreds 數百萬個身分識別的高可用性的全域身分識別管理服務的消費者導向應用程式。 此服務可跨行動及 Web 平台進行整合。 取用者可以登入 tooall 您的應用程式，透過可自訂的方式藉由使用其現有的社交帳戶或建立新的認證。

## <a name="data-access-control-and-encryption"></a>資料存取控制與加密
Microsoft 利用 hello 原則的責任有所區隔和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)整個 Azure 作業。 由 Azure 支援人員存取 toodata 需要明確的權限，授與 「 在 just-in-time 」 為基礎，為記錄和稽核，然後撤銷 hello engagement 完成後。

Azure 也提供多個功能，在資料傳輸和待用時保護資料。 這包括資料、檔案、應用程式、服務、通訊和磁碟機的加密。 您可以先將資訊加密再將其放入 Azure 中，並將金鑰存放在內部部署資料中心內。

![Azure 中的 Microsoft Antimalware](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Azure 加密技術
您可以使用收集的系統管理存取 tooyour 訂用帳戶環境的詳細資訊[Azure AD 報告](../active-directory/active-directory-reporting-audit-events.md)。 您可以在包含 Azure 敏感資訊的 VHD 上設定 [BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)。

可協助您的資料安全的 tookeep Azure 中的其他功能包括：

* 應用程式開發人員可以建置到他們在 Azure 中部署使用 hello Windows 的 hello 應用程式加密[CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx)和.NET Framework。
* 完全控制 hello Azure Blob 儲存體用戶端加密與索引鍵。 hello 儲存體服務永遠不會看見 hello 索引鍵，並不能解密 hello 資料。
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (以 hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) 提供檔案和資料層級加密和資料流失預防，透過以原則為基礎的存取管理。
* Azure 支援 SQL Server 虛擬機器中的[資料表層級和資料行層級加密 (TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx)，並支援資料中心裡的第三方內部部署金鑰管理伺服器。
* 儲存體帳戶金鑰、 共用存取簽章、 管理憑證和其他索引鍵是唯一 tooeach Azure 租用戶。
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx)混合式儲存體之前將它上傳 tooAzure 儲存體加密透過 128 位元 public/private 金鑰組的資料。
* Azure 支援，並使用多個加密機制，包括 SSL/TLS、 IPsec 及其 AES、 根據 hello 資料型別、 容器和傳輸。

## <a name="virtualization"></a>虛擬化
hello Azure 平台會使用虛擬化的環境。 使用者執行個體做為獨立虛擬機器不具有存取 tooa 實體主機伺服器，並使用實體來強制執行這種隔離[處理器 (環形-0/環形-3) 權限層級](https://en.wikipedia.org/wiki/Protection_ring)。

Ring 0 是最小權限和 3 的 hello 至少為 hello。 hello 客體作業系統會在較低權限環形 1，且應用程式中執行 hello 最小權限的環形 3。 此虛擬化的實體資源會導致 tooa 清楚的區隔客體 OS 與 hypervisor，導致之間 hello 兩個額外的安全性隔離。

hello Azure hypervisor 像是微核心和使用共用記憶體介面呼叫 VMBus，從客體虛擬機器 toohello 主機進行處理傳遞硬體的所有存取要求。 這可防止使用者取得未經處理的讀取/寫入/執行存取 toohello 系統，並可減少 hello 風險共用系統資源。

![Azure 中的 Microsoft Antimalware](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Azure 如何實作虛擬化
Azure 會使用 hypervisor 防火牆 （封包篩選器） 在 hello hypervisor 中實作和網狀架構控制器和代理程式所設定的。 這有助於防止租用戶受到未經授權的存取。 根據預設，所有流量遭到都封鎖時建立虛擬機器時，並 hello 網狀架構控制器和代理程式設定 hello 封包篩選器 tooadd*規則和例外狀況*tooallow 獲得授權的流量。

在此介紹兩種規則：

* **機器組態或基礎結構規則**：依預設會封鎖所有通訊。 發生例外狀況 tooallow 虛擬機器 toosend 而且接收 DHCP 和 DNS 流量。 虛擬機器也可以傳送流量 toohello 「 公用 」 網際網路及傳送流量 tooother 內的虛擬機器 hello 叢集與 hello OS 啟動伺服器。 允許連出目的地 hello 虛擬機器的清單不包含 Azure 路由器的子網路，Azure 管理備份結束時，以及其他 Microsoft 屬性。
* **角色組態檔**： 這會定義輸入存取控制清單 (Acl) 以 hello 租用戶的服務模型為基礎的 hello。 例如，如果租用戶具有特定虛擬機器的通訊埠 80 上的 Web 前端，然後 Azure 開啟 TCP 連接埠 80 tooall Ip 如果您設定端點中 hello [Azure 傳統部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。 如果 hello 虛擬機器具有執行中，後端 」 或 「 背景工作角色，則它會開啟 hello 背景工作角色只 toohello 內虛擬機器 hello 相同租用戶。

## <a name="isolation"></a>隔離
另一個重要的雲端安全性需求是區隔 tooprevent 未經授權的和意外設定的資訊傳輸之間共用的多租用戶架構中的部署。

Azure 會透過 VLAN 隔離、ACL、負載平衡器和 IP 篩選器，實作[網路存取控制](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)和隔離。 它會限制外部流量輸入 tooports 和您定義的虛擬機器上的通訊協定。 Azure 實作網路篩選 tooprevent 詐騙流量，並限制傳入和傳出流量 tootrusted 平台元件。 對於依預設拒絕流量的界限保護裝置，會實作流量原則。

![Azure 中的 Microsoft Antimalware](./media/azure-security-getting-started/sec-azgsfig3.PNG)

網路位址轉譯 (NAT) 會使用從外部流量 tooseparate 內部網路流量。 內部流量不可在外部路由傳送。 可在外部路由傳送的[虛擬 IP 位址](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx)，會轉譯成只能在 Azure 內路由傳送的[內部動態 IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) 位址。

透過 Acl 有防火牆外部流量 tooAzure 虛擬機器，路由器、 負載平衡器、 和第 3 層交換器上。 只有特定的已知通訊協定可被允許。 Acl 是源自於客體虛擬機器用於管理 tooother Vlan 的地方 toolimit 流量中。 此外，流量會透過 hello 主機 OS 進一步限制 hello 流量這兩個資料連結和網路圖層上的 IP 篩選器篩選。

### <a name="how-azure-implements-isolation"></a>Azure 如何實作隔離
從 hello 主機 toovirtual 機器管理單向通訊和 hello Azure 網狀架構控制器負責配置 tootenant 工作負載，基礎結構資源。 hello Azure hypervisor 會強制執行記憶體和處理序的區隔的虛擬機器，並安全地路由傳送網路流量 tooguest OS 租用戶。 Azure 也會實作租用戶、儲存體和虛擬網路的隔離。

* 各個 Azure AD 租用戶在邏輯上會以安全性界限進行隔離。
* Azure 儲存體帳戶是唯一的 tooeach 訂用帳戶，並存取必須由使用儲存體帳戶金鑰進行驗證。
* 虛擬網路會以邏輯方式透過唯一的私人 IP 位址、防火牆和 IP ACL 的組合進行隔離。 負載平衡器路由傳送流量 toohello 適當租用戶端點定義為基礎。

## <a name="virtual-networks-and-firewalls"></a>虛擬網路和防火牆
hello[分散式和虛擬網路](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx)Azure 說明 中確認您私人網路的流量邏輯上與其他 Azure 虛擬網路上的流量隔離。

![Azure 中的 Microsoft Antimalware](./media/azure-security-getting-started/sec-azgsfig4.PNG)

您的訂用帳戶可以包含多個隔離的私人網路 (也包括防火牆、負載平衡，以及網路位址轉譯)。

Azure 提供三個主要的層級的每個 Azure 中的網路隔離叢集 toologically segregate 流量。 [虛擬區域網路](https://azure.microsoft.com/services/virtual-network/)(Vlan) 會使用 tooseparate 客戶流量於 hello hello Azure 網路其餘部分。 存取 toohello 從外部 hello 叢集中的 Azure 網路會限制透過負載平衡器。

從虛擬機器的網路流量 tooand 必須經過 hello hypervisor 的虛擬交換器。 hello 根 OS 中的 hello IP 篩選器元件會隔離 hello 客體虛擬機器並從另一個 hello 客體虛擬機器中的 hello 根虛擬機器。 它會執行篩選的租用戶的節點與 hello 之間通訊流量 toorestrict 公用網際網路 （根據 hello 客戶的服務組態），將它們分別存放於來自其他租用戶。

hello IP 篩選器可協助防止客體虛擬機器從：

* 產生假冒流量。
* 不接收流量定址 toothem。
* 導向流量 tooprotected 基礎結構端點。
* 傳送或接收不當的廣播流量。

您可以將虛擬機器放在 [Azure 虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)上。 這些虛擬網路是您在內部部署環境中設定的類似 toohello 網路，它們通常與相關聯的虛擬交換器。 虛擬機器彼此連接的 toohello 相同虛擬網路可以通訊，不需要其他設定。 您也可以在您的虛擬網路中設定不同的子網路。

您可以使用下列虛擬網路上的 Azure 虛擬網路技術 toohelp 安全通訊的 hello:

* [網路安全性群組 (NSG)](../virtual-network/virtual-networks-nsg.md)。 虛擬網路中，您可以使用 NSG toocontrol 流量 tooone 或多個虛擬機器執行個體。 NSG 包含存取控制規則，可根據流量方向、通訊協定、來源位址和連接埠與目的地位址和連接埠，允許或拒絕流量。
* [使用者定義的路由](../virtual-network/virtual-networks-udr-overview.md)。 您可以控制 hello 透過路由傳送封包的虛擬應用裝置藉由建立使用者定義的路由指定 hello 封 tooa 特定子網路 toogo tooa 虛擬網路的安全性應用裝置中的下一個躍點。
* [**IP 轉送**](../virtual-network/virtual-networks-udr-overview.md)。 虛擬網路的安全性應用裝置必須能夠 tooreceive 不定址的 tooitself 的連入流量。 虛擬機器 tooreceive 流量 tooallow 定址 tooother 目的地，啟用 hello 虛擬機器的 IP 轉送。
* [**強制通道**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md)。 強制通道可讓您重新導向或 「 強制 」 您的虛擬機器在虛擬網路後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核所產生的所有網際網路繫結流量
* [**端點** ACL](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 您可以控制哪些電腦允許從 hello 網際網路 tooa 虛擬機器的傳入的連接虛擬網路上藉由定義端點 Acl。
* [**合作夥伴網路安全性解決方案**](https://azure.microsoft.com/marketplace/)。 有許多夥伴網路安全性解決方案，您可以從 hello Azure Marketplace 存取。

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Azure 如何實作虛擬網路和防火牆
根據預設，Azure 會在所有主機和客體虛擬機器上實作封包篩選防火牆。 從 hello Azure Marketplace 的 Windows 作業系統映像也有預設啟用 Windows 防火牆。 在 Azure 公開網路控制通訊的 hello 周邊的負載平衡器根據客戶的系統管理員管理的 IP Acl。

當 Azure 在正常作業中或嚴重損壞期間移動客戶的資料時，它會使用私人、加密的通訊通道來進行。 由 Azure toouse 身處虛擬網路和防火牆的其他功能包括：

* **原生主機防火牆**︰在原生 OS 上執行，沒有 Hypervisor 的 Azure Service Fabric 和 Azure 儲存體。 因此 hello windows 防火牆設定與 hello 先前兩組規則。 儲存體執行原生 toooptimize 效能。
* **主機防火牆**: hello 主機防火牆是 tooprotect hello 主機作業系統執行 hello hypervisor。 hello 規則經過程式設計的 tooallow 只有 hello 服務網狀架構控制器，且特定的連接埠上跳方塊 tootalk toohello 主機作業系統。 hello 其他例外狀況是 tooallow DHCP 回應以及 DNS 回覆。 Azure 會使用具有 hello 範本的 hello 主機 OS 的防火牆規則的機器組態檔案。 hello 主機本身受到免受外部攻擊只從已知的已驗證來源的 Windows 防火牆設定 toopermit 通訊。
* **客體防火牆**： 複寫 hello 虛擬機器交換器封包篩選器但不同的軟體 （例如 hello hello 客體作業系統的 Windows 防火牆片段） 中經過程式設計中的 hello 規則。 可以設定的 toorestrict 通訊 tooor hello 客體虛擬機器，從 hello 客體虛擬機器防火牆，即使在 hello 主機 IP 篩選器的組態所允許的 hello 通訊。 例如，您可以選擇 toouse hello 客體虛擬機器防火牆 toorestrict 之間通訊的 Vnet，已建立兩個設定 tooconnect tooone 另一個。
* **儲存防火牆 (FW)**: hello 儲存體前端上的 hello 防火牆篩選只在連接埠 80/443 與其他必要的公用程式連接埠上的流量 toobe。 hello 存放裝置後端 hello 防火牆限制通訊 toocome 只會從儲存體的前端伺服器。
* **虛擬網路閘道**: hello [Azure 虛擬網路閘道](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)作為 hello 跨單位部署閘道連接您的工作負載在 Azure 虛擬網路 tooyour 內部部署站台。 它是透過 tooon 內部部署站台需要的 tooconnect [IPsec 站對站 VPN 通道](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)，或透過[ExpressRoute](../expressroute/expressroute-introduction.md)電路。 針對 IPsec/IKE VPN 通道，hello 閘道執行 IKE 交握和建立 hello hello 虛擬網路與內部部署站台之間的 IPsec S2S VPN 通道。 虛擬網路閘道也會終止[點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)。

## <a name="secure-remote-access"></a>安全的遠端存取
Hello 雲端中儲存的資料必須有足夠的保護措施啟用 tooprevent 漏洞，並維護機密性和完整性傳輸中時。 這包括與組織的原則型、可稽核的身分識別和存取管理機制相連結的網路控制。

內建的密碼編譯技術，可讓您與部署，以及從 Azure tooon 內部部署資料中心之間 Azure 區域間 tooencrypt 通訊。 透過電腦上系統管理員存取 toovirtual[遠端桌面工作階段](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)，[遠端 Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx)，和 hello Azure 入口網站一律會加密。

toosecurely 延長您內部部署資料中心 toohello 雲端，Azure 提供了[站對站 VPN](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)和[點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)，再加上使用的專用連結[ExpressRoute](../expressroute/expressroute-introduction.md)(虛擬網路透過 VPN 進行加密連線 tooAzure)。

### <a name="how-azure-implements-secure-remote-access"></a>Azure 如何實作安全的遠端存取
連線 toohello Azure 入口網站必須一律會經過驗證，而且會要求 SSL/TLS。 您可以設定管理憑證 tooenable 安全管理。 如 [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) 和 [IPsec](https://en.wikipedia.org/wiki/IPsec) 的業界標準安全性通訊協定會受到完整支援。

[Azure ExpressRoute](../expressroute/expressroute-introduction.md) 可讓您在 Azure 資料中心和內部部署或共置環境中的基礎結構之間建立私人連線。 ExpressRoute 連線不會經過 hello 公用網際網路。 相較於一般網際網路連結，這可以提供更可靠、更快速、延遲更短和更安全的連接。 在某些情況下，使用 ExpressRoute 連線在內部部署裝置和 Azure 之間傳輸資料，也可以產生重大的成本效益。

## <a name="logging-and-monitoring"></a>記錄和監視
Azure 提供的安全性相關的事件產生的稽核，已驗證的記錄，而且它是工程的 toobe 抵抗 tootampering。 這包括系統資訊，例如 Azure 基礎結構虛擬機器與 Azure AD 中的安全性事件記錄檔。 安全性事件監視包括收集事件，例如 DHCP 或 DNS 伺服器 IP 位址; 中的變更嘗試的存取 tooports、 通訊協定或 IP 位址封鎖的設計;變更安全性原則或防火牆設定。帳戶或群組建立;未預期的處理程序及驅動程式安裝。

![Azure 中的 Microsoft Antimalware](./media/azure-security-getting-started/sec-azgsfig5.PNG)

記錄特殊權限使用者存取和活動的稽核記錄檔、授權和未授權的存取嘗試、系統例外狀況和資訊安全性事件會保留一段時間。 hello 保留記錄檔是自行斟酌，因為您設定記錄檔收集及保留 tooyour 自己的需求。

### <a name="how-azure-implements-logging-and-monitoring"></a>Azure 如何實作記錄和監視
Azure 部署管理代理程式 (MA) 和 Azure 安全性監視器 (ASM) 的代理程式 tooeach 計算、 儲存或管理下的 [網狀架構] 節點，無論是原生或虛擬。 每個管理代理程式是設定的 tooauthenticate tooa 服務小組儲存體帳戶的憑證取自 hello Azure 憑證存放區，然後向前預先設定的診斷和事件資料 toohello 儲存體帳戶。 這些代理程式不是已部署的 toocustomers 虛擬機器。

Azure 系統管理員存取透過入口網站的通過驗證且受控制存取 toohello 記錄檔的記錄檔。 系統管理員可以剖析、篩選、相互關聯及分析記錄檔。 hello Azure 服務小組儲存體帳戶的記錄檔會受到保護以直接的系統管理員存取 toohelp 避免記錄遭到竄改。

Microsoft 會在從網路裝置使用 hello Syslog 通訊協定，以及從主機伺服器使用 Microsoft 稽核收集服務 (ACS) 收集記錄檔。 這些記錄檔會放入記錄資料庫中，並且在可疑事件發生時產生警示。 hello 系統管理員可以存取並分析這些記錄檔。

[Azure 診斷](https://msdn.microsoft.com/library/azure/gg433048.aspx)是 Azure 可讓您在 Azure 中執行的應用程式從 toocollect 診斷資料的功能。 這項診斷資料可用來進行偵錯和疑難排解、測量效能、監視資源使用量、流量分析和容量規劃以及稽核。 Hello 診斷資料收集之後，它可以是轉移的 tooan Azure 儲存體帳戶進行保存。 傳輸可以是排程或隨選的。

## <a name="threat-mitigation"></a>威脅防護
在加法 tooisolation、 加密及篩選，Azure 會採用許多威脅防護機制和程序 tooprotect 基礎結構和服務。 這些包括內部的控制項和所用技術 toodetect 及補救進階的威脅，例如 DDoS、 權限提升和 hello [OWASP 前 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)。

hello 安全性控制項及風險管理程序中減少其雲端基礎結構的地方 toosecure 有 Microsoft hello 安全性事件的風險。 在 hello 事件就會發生事件，hello hello Microsoft 線上安全性服務和相容性 (OSSC) 小組內的安全性事件管理 」 (SIM) 小組是隨時準備 toorespond。

### <a name="how-azure-implements-threat-mitigation"></a>Azure 如何實作威脅防護
Azure 的安全性控制是在位置 tooimplement 威脅降低而且 toohelp 客戶也降低潛在的威脅，在其環境中。 hello 下列清單摘要說明 Azure 所提供的 hello 威脅防護功能：

* [Azure Antimalware](azure-security-antimalware.md) 依預設會在所有基礎結構伺服器上啟用。 您可以選擇性地在自己的虛擬機器內加以啟用。
* Microsoft 維護進行連續監視跨伺服器、 網路和應用程式 toodetect 威脅，並防止惡意探索。 自動化的警示會通知系統管理員的異常行為，讓它們能夠在 tootake 矯正措施外部和內部威脅。
* 您可以在訂用帳戶內部署第 3 方安全性解決方案，例如使用 [Barracuda](https://techlib.barracuda.com/ng54/deployonazure) 的 Web 應用程式防火牆。
* Microsoft 的方法 toopenetration 測試包含 「[紅色小組](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)，"牽涉到攻擊中 Azure tootest 防禦真實世界的 （非客戶） 的即時生產系統的 Microsoft 安全性專業人員進階持續性威脅。
* 整合式的部署的系統管理 hello 散發與安裝的安全性修補程式整個 hello Azure 平台。

## <a name="next-steps"></a>後續步驟
[Azure 信任中心](https://azure.microsoft.com/support/trust-center/)

[Azure 安全性小組部落格](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft 安全性回應中心](https://technet.microsoft.com/library/dn440717.aspx)

[Active Directory 部落格](http://blogs.technet.com/b/ad/)
