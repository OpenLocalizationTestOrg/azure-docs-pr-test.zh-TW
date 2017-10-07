---
title: "部署 Windows Server Active directory 在 Azure 虛擬機器 aaaGuidelines |Microsoft 文件"
description: "如果您知道如何 toodeploy AD 網域服務和內部，AD 同盟服務了解如何在 Azure 虛擬機器上。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>在 Azure 虛擬機器上部署 Windows Server Active Directory 的指導方針
本文說明 hello 部署 Windows Server Active Directory 網域服務 (AD DS) 與 Active Directory Federation Services (AD FS) 內部部署與部署到 Microsoft Azure 虛擬機器之間的重要差異。

## <a name="scope-and-audience"></a>範圍和對象
hello 發行項的主要對象已經熟悉 Active Directory 在內部部署。 它涵蓋了在 Microsoft Azure 虛擬機器 /azure 虛擬網路和傳統內部部署 Active Directory 部署中部署 Active Directory 的 hello 差異。 Azure 虛擬機器和 Azure 虛擬網路是基礎結構做為服務 (IaaS) 供應項目組織 tooleverage 運算資源 hello 雲端中的一部分。

對於不熟悉 AD 部署，請參閱 hello [AD DS 部署指南](https://technet.microsoft.com/library/cc753963)或[規劃 AD FS 部署](https://technet.microsoft.com/library/dn151324.aspx)依適當情況。

本文章假設 hello 讀者已熟悉下列概念的 hello:

* Windows Server AD DS 部署和管理
* 部署和設定 DNS toosupport Windows Server AD DS 基礎結構
* Windows Server AD FS 部署和管理
* 部署、設定及管理可以使用 Windows Server AD FS 權杖的信賴憑證者應用程式 (網站和 Web 服務)
* 一般虛擬機器概念，例如如何 tooconfigure 的虛擬機器，虛擬磁碟和虛擬網路

本文強調混合式部署案例中，Windows Server AD DS 或 AD FS 的一部分會部署在內部部署環境，一部分則部署在 Azure 虛擬機器上的 hello 要求。 hello 文件先涵蓋 hello 重大差異與內部部署，以及影響設計和部署的重要決策點的 Azure 虛擬機器上執行 Windows Server AD DS 和 AD FS。 hello 紙張的 hello 其餘部分會說明指導方針，每個詳細資料，以及如何 tooapply hello 指導方針 toovarious 部署案例中的 hello 決策點。

本文將不會討論的 hello 組態[Azure Active Directory](http://azure.microsoft.com/services/active-directory/)，即為雲端應用程式提供身分識別管理及存取控制功能的 REST 式服務。 Azure Active Directory (Azure AD) 和 Windows Server AD DS，不過，是設計的 toowork 一起 tooprovide 身分識別和存取管理解決方案，針對目前混合式 IT 環境和現代化應用程式。 toohelp 了解 hello 差異和 Windows Server AD DS 與 Azure AD 之間的關聯性，請考慮下列 hello:

1. 您可能會遇到 Windows Server AD DS hello 雲端 Azure 虛擬機器上使用 Azure tooextend 時您的內部部署資料中心 hello 雲端。
2. 您可以使用 Azure AD toogive 使用者單一登入 tooSoftware 做為服務 (SaaS) 應用程式。 例如，Microsoft Office 365 會使用這項技術，而且在 Azure 或其他雲端平台中執行的應用程式也可以使用此技術。
3. 您可以使用 Azure AD （其存取控制服務） toolet 使用者的登入使用 Facebook、 Google、 Microsoft 及裝載於 hello 雲端或內部部署其他身分識別提供者 tooapplications 來自身分識別。

如需有關這些差異的詳細資訊，請參閱 [Azure 身分識別](fundamentals-identity.md)。

## <a name="related-resources"></a>相關資源
您可以下載及執行 hello [Azure 虛擬機器整備評估](https://www.microsoft.com/download/details.aspx?id=40898)。 hello 評估會自動檢查您的內部部署環境，並產生自訂的報告根據 hello 指引中找到這個主題 toohelp 移轉 hello 環境 tooAzure。

我們建議您也會先檢閱 hello 教學課程、 輔助線和影片涵蓋下列主題中的 hello:

* [在 hello Azure 入口網站中設定純雲端虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [在 hello Azure 入口網站中設定站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [在 Azure 虛擬網路上安裝新的 Active Directory 樹系](active-directory-new-forest-virtual-machine.md)
* [在 Azure 中安裝複本 Active Directory 網域控制站](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IT Pro IaaS：(01) 虛擬機器基本概念](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IT Pro IaaS：(05) 建立虛擬網路和跨單位連線](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>簡介
hello Azure 虛擬機器上部署 Windows Server Active Directory 的基本需求不同變動會越來越小從將它部署在內部部署虛擬機器 （甚至是實體機器 toosome 範圍）。 例如，hello 在 Windows Server AD DS 中，如果 hello 網域控制站 (Dc) 部署在 Azure 虛擬機器中的現有複本的大小寫內部部署公司網域/樹系，然後可以比照使用 hello 來處理 hello Azure 部署相同的方式可能會將任何其他額外的 Windows Server Active Directory 站台。 也就是子網路必須定義在 Windows Server AD DS 中，為建立網站、 hello 子網路連結 toothat 網站和連接 tooother 站台使用適當的站台連結。 有，不過，有些差異，包括一般 tooall Azure 部署，而某些則可改變相應 toohello 特定部署案例。 兩個基本差異如下所列︰

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>連線 toohello 在內部部署公司網路時，可能需要 azure 虛擬機器。
連接 Azure 虛擬機器回復 tooan 內部公司網路需要 Azure 虛擬網路，其中包含網站-站台或站對點虛擬私人網路 (VPN) 元件無法 tooseamlessly 連接 Azure 虛擬機器和在內部部署機器。 這個 VPN 元件也可讓內部部署網域成員電腦 tooaccess Windows Server Active Directory 網域的網域控制站會獨家裝載於 Azure 虛擬機器。 重要 toonote，不過，如果 hello VPN 失敗、 驗證和其他作業，取決於 Windows Server Active Directory 也會失敗。 使用者可能無法 toosign 中使用現有的快取的認證，所有點對點或尚未 toobe 發出，或已經過時，有哪些票證的用戶端對伺服器驗證嘗試時將會失敗。

請參閱[虛擬網路](http://azure.microsoft.com/documentation/services/virtual-network/)如需觀看示範影片以及逐步教學課程，包括清單[hello Azure 入口網站中設定站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)。

> [!NOTE]
> 您也可以未連接內部部署網路的 Azure 虛擬網路上部署 Windows Server Active Directory。 但是，本主題中的 hello 指導方針會假設使用 Azure 虛擬網路，因為它會提供 IP 定址功能所不可或缺的 tooWindows 伺服器。
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>必須使用 Azure PowerShell 設定靜態 IP 位址。
動態位址會依預設，會配置，但改為使用 hello Set-azurestaticvnetip cmdlet tooassign 靜態 IP 位址。 這樣會設定靜態 IP 位址，在服務修復和 VM 關機/重新啟動期間是持續性的。 如需詳細資訊，請參閱 [虛擬機器的靜態內部 IP 位址](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)。

## <a name="BKMK_Glossary"></a>詞彙和定義
hello 以下是適用於各種 Azure 技術，將在本文中參考詞彙的非完整清單。

* **Azure 虛擬機器**: hello 的 IaaS 方案可讓客戶幾乎執行任何傳統式 toodeploy Vm 的 Azure 中內部部署伺服器工作負載。
* **Azure 虛擬網路**: hello 網路可讓客戶建立及管理 Azure 中的虛擬網路和安全地連結的 Azure 服務 tootheir 自己內部部署網路基礎結構使用虛擬私人網路 (VPN)。
* **虛擬 IP 位址**： 面對網際網路的 IP 位址未繫結的 tooa 特定電腦或網路介面卡。 接收網路流量，也就是重新導向的 tooan Azure VM 的虛擬 IP 位址會指派給雲端服務。 虛擬 IP 位址是雲端服務的屬性，該雲端服務可包含一或多個 Azure 虛擬機器。 另外請注意，Azure 虛擬網路可以包含一或多個雲端服務。 虛擬 IP 位址提供原生負載平衡功能。
* **動態 IP 位址**： 這是僅供內部的 hello IP 位址。 它應該設定為靜態 IP 位址 （透過使用 hello Set-azurestaticvnetip cmdlet） 的主控 hello DC/DNS 伺服器角色的 Vm。
* **服務修復**: hello 程序所在 Azure 會自動將傳回服務 tooa 狀態執行一次之後偵測到該 hello 服務失敗。 服務修復是 Azure 支援可用性和恢復功能的 hello 層面的其中一個。 雖然不太可能，服務在 VM 上執行之 dc 修復事件之後的 hello 結果類似 tooan 未計畫重新開機，但有一些副作用：
  
  * hello hello VM 中的虛擬網路介面卡將會變更
  * hello hello 虛擬網路介面卡的 MAC 位址會變更
  * hello hello VM 的處理器 /CPU 識別碼將會變更
  * hello hello 虛擬網路介面卡的 IP 設定不會變更，只要 hello VM 是附加的 tooa 虛擬網路並 hello VM 的 IP 位址是靜態的。
  
  但是，這些行為會影響 Windows Server Active Directory，因為它有不相依於 hello MAC 位址或處理器 /CPU 識別碼，且在 Azure 上的所有 Windows Server Active Directory 部署都建議 toobe 如上面所述，在 Azure 虛擬網路上執行.

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>它是安全的 toovirtualize Windows Server Active Directory 網域控制站嗎？
Azure 虛擬機器上部署 Windows Server Active Directory Dc 是主體 toohello 做為內部部署執行網域控制站上的虛擬機器中的相同指導方針。 只要遵循備份和還原 DC 的指導方針，那麼執行虛擬化 DC 是安全的作法。 如需執行虛擬化 DC 的條件約束和指導方針的詳細資訊，請參閱 [在 Hyper-V 中執行網域控制站](https://technet.microsoft.com/library/dd363553)。

Hypervisor 提供或忽略技術，可能會造成許多分散式系統的問題，包括 Windows Server Active Directory。 比方說，在實體伺服器上，您可以複製磁碟，或使用不受支援的方法 tooroll 後 hello 狀態伺服器，包括使用 San 等等，但這麼做可在實體伺服器上會比還原中 」 的 hypervisor 的虛擬機器快照集困難得多。 Azure 提供的功能可能會導致 hello 相同，讓人困擾的狀況。 例如，您不應該複製 Dc 的 VHD 檔案取代正常備份因為還原這些可能導致類似的情況下 toousing 快照集還原功能。

這類回復會引進 USN 泡沫可能導致 Dc 之間的 toopermanently 但內容不同的狀態。 這可能會導致以下問題︰

* 停留物件
* 密碼不一致
* 屬性值不一致
* 如果回復 hello 架構主機的架構不相符

如需 DC 如何受到影響的詳細資訊，請參閱 [USN 和 USN 回復](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback)。

從 Windows Server 2012，開始[tooAD DS 內建額外的保護措施](https://technet.microsoft.com/library/hh831734.aspx)。 這些保護，可協助保護虛擬的網域控制站針對 hello 上述問題，只要基礎 hypervisor 平台 hello 支援-VM 世代識別碼。 Azure 支援 Vm-generationid，這表示執行 Windows Server 2012 或更新版本的 Azure 虛擬機器的網域控制站具有 hello 額外的保護措施。

> [!NOTE]
> 您應該關閉並重新啟動 VM 在 Azure 中執行 hello 網域控制站角色在 hello 客體作業系統，而不是使用 hello**關機**hello Azure porta 中的選項。 現在，使用 hello 入口 tooshut 關閉 VM 會造成 hello VM toobe 取消配置。 取消配置的 VM 具有 hello 優點不會產生費用，但它也會重設 hello Vm-generationid，這是不想要針對網域控制站。 重設 hello-VM 世代識別碼，則當 hello hello AD DS 資料庫的 invocationID 也會重設、，捨棄 RID 集區 hello 和 SYSVOL 會標示為非系統授權。 如需詳細資訊，請參閱[簡介 tooActive Directory 網域服務 (AD DS) 虛擬化](https://technet.microsoft.com/library/hh831734.aspx)和[安全地虛擬化 DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx)。
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>為什麼要在 Azure 虛擬機器上部署 Windows Server AD DS？
許多 Windows Server AD DS 部署案例都非常適合部署為 Azure 上的 VM。 例如，假設您有需要 tooauthenticate 使用者在亞洲遠端位置的歐洲的公司。 hello 公司尚未先前部署 Windows Server Active Directory Dc 亞洲到期 toohello 成本 toodeploy 它們且最有限的專業知識 toomanage hello 伺服器後置部署。 如此一來，來自亞洲的驗證要求會由在歐洲的 DC 提供服務，結果不理想。 在此情況下，您可以部署在您已經指定必須在 hello 於亞洲 Azure 資料中心內執行的 VM 上的 DC。 附加該 DC tooan toohello 遠端位置將會提高驗證效能直接連接的 Azure 虛擬網路。

Azure 也非常適合做為替代 toootherwise 高成本的災害復原 (DR) 站台的。 hello 以成本相對低的裝載少量的網域控制站和單一虛擬網路在 Azure 上的代表具吸引力的替代方案。

最後，您可能想 toodeploy 在 Azure 上，例如 SharePoint，需要 Windows Server Active Directory，但是並沒有相依性 hello 在內部部署網路或 hello 公司 Windows Server Active Directory 的網路應用程式。 在此情況下，部署隔離的樹系上 Azure toomeet hello SharePoint 伺服器的要求是最佳作法。 同樣地，也支援部署需要連線 toohello 內部網路以及 hello 公司 Active Directory 的網路應用程式。

> [!NOTE]
> 它會提供 layer-3 連接，因為 hello VPN 元件，可提供 Azure 虛擬網路與內部部署網路之間的連線也可以啟用的成員伺服器來執行在 Azure 執行做為 Azure 虛擬機器的內部部署 tooleverage Dc虛擬網路。 但如果無法使用 hello VPN 時，之間通訊的內部電腦並以 Azure 為基礎的網域控制站將無法運作，導致驗證和其他各種錯誤發生。  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>在 Azure 虛擬機器上與在內部部署上部署 Windows Server Active Directory 網域控制站之間的對照
* 包含多部 vm 的任何 Windows Server Active Directory 部署案例，則是必要的 toouse Azure 虛擬網路 IP 位址一致性。 請注意，本指南假設 DC 在 Azure 虛擬網路上執行。
* 如同內部部署 DC，建議使用靜態 IP 位址。 靜態 IP 位址只能使用 Azure PowerShell 進行設定。 如需詳細資訊，請參閱 [VM 的靜態內部 IP 位址](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) 。 如果您有監控系統或其他解決方案會檢查為 hello 客體作業系統內的靜態 IP 位址組態，您可以指派 hello 相同 IP 位址 toohello 網路介面卡的靜態屬性 hello VM。 但是請注意如果 hello VM 經歷了服務修復或 hello 入口網站中關閉，而且已為其位址取消配置，將會捨棄該 hello 網路介面卡。 在此情況下，hello 客體內 hello 靜態 IP 位址必須 toobe 重設。
* 虛擬網路上部署 Vm 不表示 （或要求） 連線後 tooan 在內部部署網路。hello 虛擬網路只會啟用以排除這個可能性。 您必須建立虛擬網路以在 Azure 和您的內部部署網路之間進行私密通訊。 您需要 toodeploy hello 與內部網路的 VPN 端點。 從 Azure toohello 在內部部署網路開啟 hello VPN。 如需詳細資訊，請參閱[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)和[hello Azure 入口網站中設定站對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)。

> [!NOTE]
> 選項太[建立點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)是可用 tooconnect 個別的 Windows 電腦直接 tooan Azure 虛擬網路。
> 
> 

* 不論您是否建立虛擬網路，Azure 會針對輸出流量計費，而不會對輸入流量計費。 不同的 Windows Server Active Directory 設計選擇會影響部署產生的輸出流量。 例如，部署唯讀網域控制站 (RODC) 會限制輸出流量，因為它不會複寫輸出。 但 hello 決策 toodeploy RODC 必須權衡 hello 需要 tooperform toobe 寫入作業對 hello DC 和 hello[相容性](https://technet.microsoft.com/library/cc755190)應用程式和服務 hello 站台中有 Rodc。 如需流量費用的詳細資訊，請參閱 [Azure 價格一覽](http://azure.microsoft.com/pricing/)。
* 雖然您可以完全控制哪些伺服器資源 toouse，Vm 內部部署，如 RAM、 磁碟大小等等，透過在 Azure 上您必須從選取的預先設定的伺服器規模清單。 對於 DC 而言順序 toostore hello Windows Server Active Directory 資料庫中的加法 toohello 作業系統磁碟中需要的資料磁碟。

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>是否可以在 Azure 虛擬機器上部署 Windows Server AD FS？
是，您可以部署在 Azure 的虛擬機器上的 Windows Server AD FS 和 hello [AD FS 部署的最佳做法](https://technet.microsoft.com/library/dn151324.aspx)內部同樣適 tooAD FS 部署在 Azure 上。 但有些 hello 最佳作法，例如負載平衡和高可用性需要超越 AD FS 本身提供的技術。 它們必須由 hello 基礎結構提供。 讓我們複習這些最佳作法，並且使用 Azure VM 和 Azure 虛擬網路來查看如何達成。

1. **絕不能公開安全性權杖服務 (STS) 伺服器直接 toohello 網際網路。**
   
    這是很重要，因為 hello STS 發出安全性權杖。 如此一來，STS 伺服器例如 AD FS 伺服器應視為與 hello 相同層級的保護，做為網域控制站。 如果犧牲 STS，惡意使用者有可能包含宣告其選擇的 toorelying 合作對象應用程式和其他 STS 伺服器信任組織中的 hello 能力 tooissue 存取權杖。
2. **部署 hello 做為 hello AD FS 伺服器相同網路中的所有使用者網域的 Active Directory 網域控制的站。**
   
    AD FS 伺服器使用 Active Directory 網域服務 tooauthenticate 使用者。 建議 toodeploy hello 與 hello AD FS 伺服器相同網路上的網域控制站。 這會提供業務續航力 hello 之間的連結 hello Azure 網路，而且在內部部署網路已中斷，並且可縮短延遲和提高登入的效能。
3. **部署高可用性以及平衡 hello 負載的多個 AD FS 節點。**
   
    在大部分情況下，AD FS 啟用的應用程式的 hello 失敗是無法接受的因為需要安全性權杖通常的 hello 應用程式非常關鍵。 如此一來，而且 AD FS 此時存在於 hello 徑 tooaccessing 關鍵任務應用程式中，因為 hello AD FS 服務必須是高可用性，透過多個 AD FS proxy 和 AD FS 伺服器。 tooachieve 發佈的要求，負載平衡器通常會 hello AD FS Proxy 和 hello AD FS 伺服器前面進行部署。
4. **針對網際網路存取部署一或多個 Web 應用程式 Proxy 節點。**
   
    當使用者需要 tooaccess hello AD FS 服務所保護的應用程式時，hello AD FS 服務的需求 toobe 可從 hello 網際網路。 這是藉由部署 hello Web 應用程式 Proxy 服務來達成。 強烈建議 toodeploy 多個高可用性和負載平衡的 hello 目的的一個節點。
5. **限制從 hello Web 應用程式 Proxy 節點 toointernal 網路資源的存取。**
   
    從 tooallow 外部使用者 tooaccess AD FS hello 網際網路，您需要 toodeploy Web 應用程式 Proxy 節點 （或在舊版的 Windows Server AD FS Proxy）。 hello Web 應用程式 proxy 節點會直接公開 toohello 網際網路。 它們不是必要的 toobe 已加入網域，它們只需要存取 toohello AD FS 伺服器透過 TCP 連接埠 443 和 80。 強烈建議該通訊 tooall （尤其是網域控制站） 的其他電腦遭到封鎖。
   
    這通常是藉由 DMZ 的方式在內部部署達成。 防火牆會使用作業 toorestrict hello DMZ toohello 與內部網路流量的白名單模式 （亦即，僅流量 hello 從指定的 IP 位址和 over 指定允許的連接埠，而所有其他流量被封鎖）。

hello 下列圖表顯示傳統內部部署 AD FS 部署。

![傳統內部部署 Active Directory Federation Services 部署的圖表](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

不過，因為 Azure 不提供原生而功能完整的防火牆功能，其他選項會需要使用 toobe toorestrict 流量。 hello 下表顯示每個選項及其優點和缺點。

| 選項 | 優點 | 缺點 |
| --- | --- | --- |
| [Azure 網路 ACL](../virtual-network/virtual-networks-acl.md) |較便宜又簡單的初始組態 |如果任何新的 Vm 會加入 toohello 部署不需要額外的網路 ACL 設定 |
| [Barracuda NG 防火牆](https://www.barracuda.com/products/ngfirewall) |作業的白名單模式且不需要網路 ACL 組態 |初始設定的增加成本與複雜度 |

hello 高階步驟 toodeploy AD FS 在此情況下，如下所示如下：

1. 使用 VPN 或 [ExpressRoute](http://azure.microsoft.com/services/expressroute/)，建立具有跨單位連線的虛擬網路。
2. 部署 hello 虛擬網路上的網域控制站。 此步驟為選用步驟，但建議執行。
3. 部署已加入網域的 AD FS 伺服器 hello 虛擬網路上。
4. 建立[內部負載平衡集](http://azure.microsoft.com/blog/internal-load-balancing/)，包含 hello AD FS 伺服器，以及使用新的私用 IP 位址在 hello 虛擬網路 （動態 IP 位址）。
   
   1. 更新 DNS toocreate hello FQDN toopoint toohello 私用 （動態） 的 IP 位址的 hello 內部負載平衡集。
5. 建立雲端服務 （或個別的虛擬網路） 的 hello Web 應用程式 Proxy 節點。
6. 部署 hello hello 雲端服務或虛擬網路中的 Web 應用程式 Proxy 節點
   
   1. 建立外部負載平衡集，其中包含 hello Web 應用程式 Proxy 節點。
   2. 更新 hello 外部 DNS 名稱 (FQDN) toopoint toohello 雲端服務公用 IP 位址 （hello 虛擬 IP 位址）。
   3. 設定 AD FS proxy toouse hello 對應 toohello 內部負載平衡集 hello AD FS 伺服器的 FQDN。
   4. 更新宣告式 web 網站 toouse hello 外部 FQDN 用於其宣告提供者。
7. 限制 Web 應用程式 Proxy tooany 機器 hello AD FS 虛擬網路中的存取權。

toorestrict 流量 hello hello Azure 內部負載平衡器負載平衡集需要 toobe 設定成只有流量 tooTCP 通訊埠 80 和 443，並捨棄所有其他流量 toohello 內部動態 IP 位址的負載平衡集 hello 訊息。

![允許 TCP 443 + 80 的 ADFS 網路 ACL 的圖表。](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

流量 toohello AD FS 伺服器只會允許下列來源的 hello:

* hello Azure 內部負載平衡器。
* hello hello 與內部網路上的系統管理員的 IP 位址。

> [!WARNING]
> hello 設計必須防止 Web 應用程式 Proxy 節點 hello Azure 虛擬網路中的其他 Vm 或 hello 與內部網路上的任何位置。 可以藉由在 hello Express Route 連線的內部部署應用裝置或 hello 站對站 VPN 連線的 VPN 裝置設定防火牆規則來完成。
> 
> 

缺點 toothis 選項是 hello 需要 tooconfigure hello 網路 Acl 的多個裝置，包括內部負載平衡器、 hello AD FS 伺服器，以及加入 toohello 虛擬網路的任何其他伺服器。 如果任何裝置加入 toohello 部署而不需設定網路 Acl toorestrict 流量 tooit，hello 整個部署可能會有風險。 如果 hello hello Web 應用程式 Proxy 節點的 IP 位址有所變更，必須重設 hello 網路 Acl (也就是說，hello proxy 應該設定的 toouse[靜態動態 IP 位址](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/))。

![使用網路 ACLS 的 Azure 上的 ADFS。](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

另一個選項是 toouse hello [Barracuda NG 防火牆](https://www.barracuda.com/products/ngfirewall)應用裝置 toocontrol AD FS proxy 伺服器與 hello AD FS 伺服器之間的流量。 此選項符合安全性和高可用性的最佳作法，而且需要較少的管理 hello 初始安裝之後，因為 hello Barracuda NG 防火牆應用裝置提供防火牆管理的白名單模式，而且可以進行安裝直接在 Azure 虛擬網路。 新伺服器新增 toohello 部署任何時間排除 hello 需要 tooconfigure 網路 Acl。 但是，此選項會增加初始部署的複雜度和成本。

在此情況下，會部署兩個虛擬網路而不是一個。 我們稱之為 VNet1 和 VNet2。 VNet1 包含 hello proxy，而 VNet2 包含 Sts hello 與 hello 網路連線後 toohello 公司網路。 VNet1 因此是實際 （雖然實際上） 對 vnet2 而言，再接著從 hello 公司網路隔離。 VNet1 再連接的 tooVNet2 使用已知做為傳輸獨立網路架構 (TINA) 的特殊通道技術。 hello TINA 通道會使用 Barracuda NG 防火牆 hello 虛擬網路附加的 tooeach — 一個 Barracuda hello 虛擬網路。  如需高可用性，建議您部署兩個 Barracuda 上每個虛擬網路。一個使用中，hello 另一個被動。 它們提供非常豐富的防火牆功能，讓我們的傳統內部部署 DMZ toomimic hello 作業在 Azure 中。

![使用防火牆的 Azure 上的 ADFS。](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

如需詳細資訊，請參閱[AD FS： 擴充宣告感知的內部部署前端應用程式 toohello 網際網路](#BKMK_CloudOnlyFed)。

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>如果 hello 的目標是 Office 365 SSO 時替代 tooAD FS 部署
如果您的目標是只 tooenable 登入 Office 365，還有另一個替代 toodeploying AD FS 完全。 在此情況下，只需使用密碼同步內部部署目錄同步和達到同樣的最終結果 hello 與最低的部署複雜性，因為這種方法不需要 AD FS 或 Azure。

hello 下表比較使用和不部署 AD FS，hello 登入處理程序的運作方式。

| 使用 AD FS 和 DirSync 的 Office 365 單一登入 | 使用 DirSync + Password Sync 的 Office 365 相同登入 |
| --- | --- |
| 1.hello 使用者登入時 tooa 公司網路，且驗證的 tooWindows Server Active Directory。 |1.hello 使用者登入時 tooa 公司網路，且驗證的 tooWindows Server Active Directory。 |
| 2.hello 的使用者嘗試 tooaccess Office 365 (我@contoso.com)。 |2.hello 的使用者嘗試 tooaccess Office 365 (我@contoso.com)。 |
| 3.Office 365 將重新導向 hello 使用者 tooAzure AD。 |3.Office 365 將重新導向 hello 使用者 tooAzure AD。 |
| 4.Azure AD 無法驗證 hello 使用者及了解 AD FS 內部部署信任，因為它會重新導向 hello 使用者 tooAD FS。 |4.Azure AD 不能直接接受 Kerberos 票證，並沒有信任關係存在，因此會要求該 hello 使用者輸入認證。 |
| 5.hello 使用者傳送 Kerberos 票證 toohello AD FS STS。 |5.hello 使用者輸入 hello 相同內部部署密碼，且 Azure AD 進行驗證 hello 使用者名稱和密碼以 DirSync 所同步。 |
| 6.AD FS 轉換 Kerberos 票證 toohello 所需的 token 格式/宣告，並將重新導向 hello 使用者 tooAzure AD hello。 |6.Azure AD 會重新導向 hello 使用者 tooOffice 365。 |
| 7.hello 使用者驗證 tooAzure AD （另一個轉換發生時）。 |7.hello 使用者可以登入 tooOffice 365 和 OWA 使用 hello Azure AD 的權杖。 |
| 8.Azure AD 會重新導向 hello 使用者 tooOffice 365。 | |
| 9.hello 使用者是以無訊息模式登入 tooOffice 365。 | |

在 hello Office 365 DirSync 搭配密碼同步案例 (沒有 AD FS)，單一登入已取代 「 相同登入 」 其中 「 相同 」 表示使用者必須重新輸入其相同的內部部署認證存取 Office 365 時。 請注意，可以由 hello 使用者的瀏覽器 toohelp 記住此資料會減少後續提示。

### <a name="additional-food-for-thought"></a>其他考量
* 如果您將部署在 Azure 虛擬機器上的 AD FS proxy，則需要連線 toohello AD FS 伺服器。 如果它們是在內部部署，建議您利用 hello 虛擬網路 tooallow hello Web 應用程式 Proxy 節點 toocommunicate 提供與其 AD FS 伺服器的 hello 站對站 VPN 連線。
* 如果您部署 AD FS 伺服器上的 Azure 虛擬機器，連線 tooWindows Server Active Directory 網域控制站、 屬性存放區和組態資料庫是必要的可能也需要 ExpressRoute 或站對站 VPN 連線之間 hello Azure 虛擬網路和 hello 內部網路。
* 都需要收取費用 tooall 流量從 Azure 虛擬機器 （輸出流量）。 如果成本是 hello 驅動因素，則建議 toodeploy hello Web 應用程式 Proxy 節點，在 Azure 上，而保留 hello AD FS 伺服器在內部。 如果 hello AD FS 伺服器部署在 Azure 虛擬機器上，額外的成本將會產生的 tooauthenticate 內部使用者。 輸出流量都會產生成本無論周遊 hello ExpressRoute 或 hello VPN 站對站連線。
* 如果您決定 toouse Azure 的原生伺服器負載平衡的 AD FS 伺服器的高可用性功能，請注意負載平衡會提供探查，會使用的 toodetermine hello hello hello 雲端服務內的虛擬機器健全狀況。 在 Azure 虛擬機器 （做為相對於 tooweb 或背景工作角色） 的 hello 情況下，由於 hello 代理程式回應 toohello 預設探查 」 不存在於 Azure 虛擬機器必須使用自訂探查。 為了簡單起見，您可以使用自訂 TCP 探查，這只需要 TCP 連線 （TCP SYN 區段傳送及回應 TCP SYN ACK 區段 toowith） 都已成功建立的 toodetermine 虛擬機器健全狀況。 您可以設定虛擬機器主動接聽任何 TCP 連接埠 toowhich hello 自訂探查 toouse。

> [!NOTE]
> 需要直接 toohello 網際網路 （例如連接埠 80 和 443） 不能共用相同設定的連接埠 tooexpose hello 機器 hello 相同雲端服務。 因此，建議您建立專用的雲端服務，如您在順序 tooavoid 潛在 「 Windows Server AD FS 伺服器與應用程式的連接埠需求與 Windows Server AD FS 之間重疊。
> 
> 

## <a name="deployment-scenarios"></a>部署案例
下列章節的 hello 概述經常部署案例 toodraw 注意 tooimportant 考量必須納入考量。 每個案例都有關於 hello 決策和因素 tooconsider 連結 toomore 詳細資料。

1. [AD DS︰部署 AD DS 感知應用程式，不需要公司網路連接](#BKMK_CloudOnly)
   
    例如，網際網路對應 SharePoint 服務會部署在 Azure 虛擬機器上。 hello 應用程式具有公司網路資源的任何相依性。 hello 應用程式需要 Windows Server AD DS，但不需要 hello 公司 Windows Server AD DS。
2. [AD FS： 擴充宣告感知的內部部署前端應用程式 toohello 網際網路](#BKMK_CloudOnlyFed)
   
    例如，已成功部署在內部部署而且由公司使用者使用的宣告感知應用程式需要 toobecome hello 網際網路從可以存取。 hello 應用程式需要 toobe 直接透過 hello 網際網路存取，使用自己公司身分識別的商業夥伴和現有公司使用者。
3. [AD DS： 部署可感知 Windows Server AD DS 的應用程式需要連接 toohello 公司網路](#BKMK_HybridExt)
   
    例如，支援 Windows 整合式驗證並使用 Windows Server AD DS 做為組態和使用者設定檔資料儲存機制的 LDAP 感知應用程式，會部署在 Azure 虛擬機器上。 它是理想的 hello 應用程式 tooleverage hello 現有公司 Windows Server AD DS，並提供單一登入。 無法感知宣告的 hello 應用程式。

### <a name="BKMK_CloudOnly"></a>1.AD DS︰部署 AD DS 感知應用程式，不需要公司網路連接
![僅限雲端的 AD DS 部署](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**圖 1**

#### <a name="description"></a>說明
SharePoint 會部署在 Azure 虛擬機器上而且 hello 應用程式不相依於公司網路資源。 hello 應用程式需要 Windows Server AD DS，但不會*不*需要 hello 公司 Windows Server AD DS。 不需要 Kerberos 或同盟的信任，因為使用者可透過 hello hello Windows Server AD DS 網域也裝載於 Azure 虛擬機器上的 hello 雲端應用程式自行佈建。

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>案例考量以及技術領域如何套用 toohello 案例
* [網路拓撲](#BKMK_NetworkTopology)︰建立 Azure 虛擬網路，而不需要跨單位連線 (也稱為站對站連接)。
* [DC 部署組態](#BKMK_DeploymentConfig)︰將新的網域控制站部署到新的單一網域 Windows Server Active Directory 樹系。 這應該部署以及 hello Windows DNS 伺服器。
* [Windows Server Active Directory 站台拓撲](#BKMK_ADSiteTopology)： 使用 hello 預設 Windows Server Active Directory 站台 （預設值第一個站台名稱將所有的電腦）。
* [IP 位址和 DNS](#BKMK_IPAddressDNS)：
  
  * 使用 hello Set-azurestaticvnetip Azure PowerShell cmdlet 設定 hello DC 的靜態 IP 位址。
  * 安裝和設定 Windows Server DNS hello Azure 上的網域控制站。
  * Hello 名稱和 IP 位址的 hello 裝載 hello DC 和 DNS 伺服器角色的 VM 設定 hello 虛擬網路屬性。
* [通用類別目錄](#BKMK_GC): hello hello 樹系中的第一個 DC 必須是通用類別目錄伺服器。 也應該將其他網域控制站設定為 Gc，因為在單一網域樹系 hello 通用類別目錄不需要任何額外的工作，從 hello DC。
* [Hello Windows Server AD DS 資料庫和 SYSVOL 的位置](#BKMK_PlaceDB)： 新增為 Azure Vm 執行順序 toostore hello Windows Server Active Directory 資料庫、 記錄檔和 SYSVOL 中的資料磁碟 tooDCs。
* [備份和還原](#BKMK_BUR)： 決定您想要 toostore 系統狀態備份。 如有必要，加入另一個資料磁碟 toohello DC VM toostore 的備份。

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS： 擴充宣告感知的內部部署前端應用程式 toohello 網際網路
![具有跨單位連線的同盟](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**圖 2**

#### <a name="description"></a>說明
宣告感知應用程式已成功部署在內部部署而且由公司使用者需求 toobecome 可以直接從 hello 網際網路存取。 hello 應用程式當做 web 前端 tooa SQL database 以儲存資料。 hello hello 應用程式所使用的 SQL server 也位於 hello 公司網路。 兩個 Windows Server AD FS Sts 和負載平衡器已在內部部署的 tooprovide 存取 toohello 公司使用者。 hello 應用程式現在需要 toobe 提供額外的存取直接透過網際網路 hello 使用自己公司身分識別的商業夥伴和現有公司使用者。

投入時間 toosimplify 和符合 hello 部署和組態需求，這個新要求，我們決定將兩個額外的 web 前端和兩部 Azure 虛擬機器上安裝 Windows Server AD FS proxy 伺服器。 所有四個 Vm 將會直接公開 toohello 網際網路，而且將會提供連線 toohello 在內部部署網路使用 Azure 虛擬網路的站對站 VPN 功能。

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>案例考量以及技術領域如何套用 toohello 案例
* [網路拓撲](#BKMK_NetworkTopology)：建立 Azure 虛擬網路和[設定跨單位連線](../vpn-gateway/vpn-gateway-site-to-site-create.md)。
  
  > [!NOTE]
  > 每一個 hello Windows Server AD FS 憑證，請確定 hello URL 範本內定義 hello 憑證，並在 Azure 上執行的 hello Windows Server AD FS 執行個體可到達 hello 產生的憑證。 這可能需要跨單位連線 tooparts PKI 基礎結構。 例如，如果 hello CRL 的端點是以 LDAP 為基礎和以獨佔方式裝載內部部署，則跨單位連線都是必要的。 如果不需要這樣做，它可能是必要 toouse hello 網際網路位於可存取的 CRL 的 CA 所簽發的憑證。
  > 
  > 
* [雲端服務組態](#BKMK_CloudSvcConfig)︰請確定您有兩個雲端服務，以便提供兩個負載平衡虛擬 IP 位址。 hello 第一個雲端服務的虛擬 IP 位址將會導向的 toohello 兩個 Windows Server AD FS proxy 連接埠 80 和 443 上的 Vm。 hello Windows Server AD FS proxy Vm 將會設定 hello 內部負載平衡器面對 hello Windows Server AD FS Sts toopoint toohello IP 位址。 hello 第二個雲端服務的虛擬 IP 位址將會導向的 toohello 兩個 Vm 同樣在連接埠 80 和 443 上執行 hello web 前端。 設定自訂探查 tooensure hello 負載平衡器只會將導向流量 toofunctioning Windows Server AD FS proxy 和 web 前端 Vm。
* [同盟伺服器設定](#BKMK_FedSrvConfig): hello hello 雲端中建立的 Windows Server Active Directory 樹系設定 Windows Server AD FS 同盟伺服器 (STS) toogenerate 安全性 token。 設定同盟宣告提供者信任關係有 hello 想 tooaccept 身分識別，從不同的夥伴，並使用您想 toogenerate 語彙基元來 hello 不同應用程式設定信賴憑證者的合作對象的信任關係。
  
    在大部分情況下，Windows Server AD FS Proxy 伺服器會基於安全性理由而部署在網際網路對應的容量，其 Windows Server AD FS 同盟對應項目依然隔離為直接網際網路連接。 不論您的部署案例，您必須設定您的雲端服務會提供公開的 IP 位址以及能夠 tooload 餘額會橫跨兩個 Windows Server AD FS STS 執行個體或 proxy 執行個體的連接埠的虛擬 IP 位址。
* [Windows Server AD FS 高可用性組態](#BKMK_ADFSHighAvail)： 它是建議 toodeploy 容錯移轉和負載平衡的至少兩部伺服器的 Windows Server AD FS 伺服器陣列。 您可能會想 tooconsider hello Windows 內部資料庫 (WID) 用於 Windows Server AD FS 組態資料，並使用 hello 內部負載平衡 hello 伺服陣列中的 hello 伺服器功能的 Azure toodistribute 連入要求。

如需詳細資訊，請參閱 hello [AD DS 部署指南](https://technet.microsoft.com/library/cc753963)。

### <a name="BKMK_HybridExt"></a>3.AD DS： 部署可感知 Windows Server AD DS 的應用程式需要連接 toohello 公司網路
![跨單位 AD DS 部署](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**圖 3**

#### <a name="description"></a>說明
LDAP 感知應用程式會部署在 Azure 虛擬機器上。 支援 Windows 整合式驗證並使用 Windows Server AD DS 做為組態和使用者設定檔資料的儲存機制。 hello 目標的 hello 應用程式 tooleverage hello 現有公司 Windows Server AD DS 中，並提供單一登入。 無法感知宣告的 hello 應用程式。 使用者也需要直接從網際網路 hello tooaccess hello 應用程式。 toooptimize 效能和成本，我們決定將兩個屬於 hello 公司網域的其他網域控制站會連同 hello Azure 上的應用程式一起部署。

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>案例考量以及技術領域如何套用 toohello 案例
* [網路拓撲：](#BKMK_NetworkTopology)使用[跨單位連線](../vpn-gateway/vpn-gateway-site-to-site-create.md)建立 Azure 虛擬網路。
* [安裝方法](#BKMK_InstallMethod)： 部署複本 Dc 從 hello 公司 Windows Server Active Directory 網域。 對於複本 DC，您可以安裝 Windows Server AD DS 上 hello VM，並選擇性地使用 hello 安裝從媒體 (IFM) 功能 tooreduce hello 的資料量需要 toobe 複寫 toohello 期間安裝新的 DC。 如需教學課程，請參閱 [在 Azure 中安裝複本 Active Directory 網域控制站](active-directory-install-replica-active-directory-domain-controller.md)。 即使您使用 IFM，它可能會更有效率的 toobuild hello 虛擬 DC 在內部部署和移動 hello 整個虛擬硬碟 (VHD) toohello 雲端而不是在安裝期間複寫 Windows Server AD DS。 基於安全考量，建議您一旦已複製的 tooAzure hello VHD 刪除從 hello 與內部網路。
* [Windows Server Active Directory 網站拓撲](#BKMK_ADSiteTopology)：在 Active Directory 網站及服務中建立新的 Azure 網站。 建立 Windows Server Active Directory 子網路物件 toorepresent hello Azure 虛擬網路，並新增 hello 子網路 toohello 網站。 建立新的站台連結，它包含 hello 新的 Azure 網站以及 hello 網站中的 hello Azure 虛擬網路 VPN 端點位於順序 toocontrol 來最佳化 Windows Server Active Directory 流量 tooand 從 Azure。
* [IP 位址和 DNS](#BKMK_IPAddressDNS)：
  
  * 使用 hello Set-azurestaticvnetip Azure PowerShell cmdlet 設定 hello DC 的靜態 IP 位址。
  * 安裝和設定 Windows Server DNS hello Azure 上的網域控制站。
  * Hello 名稱和 IP 位址的 hello 裝載 hello DC 和 DNS 伺服器角色的 VM 設定 hello 虛擬網路屬性。
* [地理位置分散 DC](#BKMK_DistributedDCs)︰視需要設定其他虛擬網路。 如果您的 Active Directory 站台拓撲需要對應 toodifferent Azure 的地理位置中的網域控制站與您的區域，據此想 toocreate Active Directory 站台。
* [唯讀網域控制站](#BKMK_RODC)： 您可能會將 RODC 部署在 hello Azure 站台，取決於您的需求執行的寫入作業對 hello DC 和 hello 相容性應用程式和服務在 hello 與 Rodc 的站台。 如需有關應用程式相容性的詳細資訊，請參閱 hello[唯讀網域控制站的應用程式相容性指南](https://technet.microsoft.com/library/cc755190)。
* [通用類別目錄](#BKMK_GC): Gc 是多重網域樹系中的所需的 tooservice 登入要求。 如果您未部署 GC hello Azure 網站中的，就會發生輸出流量成本，因為驗證要求在其他站台中會產生查詢 Gc。 流量的 toominimize，您可以啟用快取 hello Azure Active Directory 站台及服務中的站台的萬用群組成員資格。
  
    如果您部署 GC，設定網站連結和站台連結成本，因此不需要 tooreplicate 的其他 Gc 慣用當做來源 DC hello GC hello Azure 站台在 hello 相同部分網域分割區。
* [Hello Windows Server AD DS 資料庫和 SYSVOL 的位置](#BKMK_PlaceDB)： 加入資料磁碟 tooDCs 訂單 toostore hello Windows Server Active Directory 資料庫、 記錄檔和 SYSVOL 中的 Azure Vm 上執行。
* [備份和還原](#BKMK_BUR)： 決定您想要 toostore 系統狀態備份。 如有必要，加入另一個資料磁碟 toohello DC VM toostore 的備份。

## <a name="deployment-decisions-and-factors"></a>部署決策和因素
本表會摘要說明 hello Windows Server Active Directory 技術領域 hello 上述案例中受到影響，hello 對應決策 tooconsider 與下方的連結 toomore 詳細資料。 某些技術領域可能不適用 tooevery 部署案例中，以及一些技術領域可能比其他技術領域更為重要 tooa 部署案例。

例如，如果部署複本 DC 上的虛擬網路，而且您的樹系只有單一網域，然後選擇 toodeploy 通用類別目錄伺服器在此情況下將無法重大 toohello 部署案例因為它不會建立任何額外的複寫需求。 在 hello 相反地，如果 hello 樹系有幾個網域，然後 hello 決策 toodeploy 虛擬網路上的通用類別目錄可能會影響可用的頻寬、 效能、 驗證、 目錄查閱等等。

| Windows Server Active Directory 技術領域 | 決策 | 因素 |
| --- | --- | --- |
| [網路拓撲](#BKMK_NetworkTopology) |建立虛擬網路？ |<li>需求 tooaccess 公司資源</li> <li>驗證</li> <li>帳戶管理</li> |
| [DC 部署組態](#BKMK_DeploymentConfig) |<li>在沒有任何信任的情況下部署個別樹系？</li> <li>部署具有同盟的新樹系？</li> <li>部署具有 Windows Server Active Directory 樹系信任或 Kerberos 的新樹系？</li> <li>藉由部署複本 DC 擴充公司樹系？</li> <li>藉由部署新的子網域或網域樹系擴充公司樹系？</li> |<li>安全性</li> <li>法規遵循</li> <li>成本</li> <li>恢復功能和容錯</li> <li>應用程式相容性</li> |
| [Windows Server Active Directory 網站拓撲](#BKMK_ADSiteTopology) |您該如何設定 Azure 虛擬網路 toooptimize 流量子網路、 網站和站台連結並成本降至最低？ |<li>子網路和站台定義</li> <li>站台連結屬性和變更通知</li> <li>複寫壓縮</li> |
| [IP 位址和 DNS](#BKMK_IPAddressDNS) |如何 tooconfigure IP 位址和名稱解析？ |<li>使用 hello 使用 hello Set-azurestaticvnetip cmdlet tooassign 靜態 IP 位址</li> <li>安裝 Windows Server DNS 伺服器及 hello 名稱和 IP 位址的 hello 裝載 hello DC 和 DNS 伺服器角色的 VM 設定 hello 虛擬網路屬性</li> |
| [地理位置分散 DC](#BKMK_DistributedDCs) |如何 tooreplicate tooDCs 上的個別虛擬網路？ |如果您的 Active Directory 站台拓撲需要對應 toodifferent Azure 的地理位置中的網域控制站與您的區域，據此想 toocreate Active Directory 站台。 [設定虛擬網路 toovirtual 網路連線](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)tooreplicate 不同虛擬網路上的網域控制站之間。 |
| [唯讀 DC](#BKMK_RODC) |使用唯讀或可寫入 DC？ |<li>篩選 HBI/PII 屬性</li> <li>篩選祕密</li> <li>限制輸出流量</li> |
| [通用類別目錄](#BKMK_GC) |安裝通用類別目錄？ |<li>對於單一網域樹系，讓所有 DC 都是 GC</li> <li>對於多網域樹系，需要 GC 以進行驗證</li> |
| [安裝方法](#BKMK_InstallMethod) |如何在 Azure 中的 tooinstall DC？ |下列任一方法︰ <li>使用 Windows PowerShell 或 Dcpromo 安裝 AD DS</li> <li>移動內部部署虛擬 DC 的 VHD</li> |
| [Hello Windows Server AD DS 資料庫和 SYSVOL 的位置](#BKMK_PlaceDB) |其中 toostore Windows Server AD DS 資料庫、 記錄檔，以及 SYSVOL 嗎？ |變更 Dcpromo.exe 預設值。 這些重要的 Active Directory 檔案「必須」  放在 Azure 資料磁碟，而不是實作寫入快取的作業系統磁碟。 |
| [備份與還原](#BKMK_BUR) |如何 toosafeguard 和復原資料嗎？ |建立系統狀態備份 |
| [同盟伺服器組態](#BKMK_FedSrvConfig) |<li>部署新的樹系具有同盟 hello 雲端中嗎？</li> <li>部署 AD FS 內部部署及公開 proxy hello 雲端中的嗎？</li> |<li>安全性</li> <li>法規遵循</li> <li>成本</li> <li>存取 tooapplications 的商務夥伴</li> |
| [雲端服務組態](#BKMK_CloudSvcConfig) |以隱含方式部署雲端服務 hello 建立虛擬機器的第一次。 您需要 toodeploy 其他雲端服務嗎？ |<li>Vm 需要直接暴露 toohello 網際網路嗎？</li> <li> 需要負載平衡 hello 服務嗎？</li> |
| [公用和私人 IP 位址 (動態 IP 與虛擬 IP) 的同盟伺服器需求](#BKMK_FedReqVIPDIP) |<li>Hello Windows Server AD FS 執行個體需要 toobe 直接從 hello 網際網路聯繫嗎？</li> <li>Hello 雲端中部署的 hello 應用程式需要它自己的面向網際網路 IP 位址和連接埠嗎？</li> |針對您的部署所需的每個虛擬 IP 位址建立一個雲端服務 |
| [Windows Server AD FS 高可用性組態](#BKMK_ADFSHighAvail) |<li>在我的 Windows Server AD FS 伺服器陣列中有多少節點？</li> <li>在 我的 Windows Server AD FS proxy 伺服器陣列中的節點 toodeploy 多少？</li> |恢復功能和容錯 |

### <a name="BKMK_NetworkTopology"></a>網路拓撲
在訂單 toomeet hello IP 位址一致性和 Windows Server AD DS 的 DNS 需求，就需要建立 toofirst [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)和附加虛擬機器 tooit。 在其建立時，您必須決定是否 toooptionally 擴充連線 tooyour 內部公司網路，明確地連接 Azure 虛擬機器 tooon 內部部署機器 — 這利用傳統 VPN 技術來達成和需要將 VPN 端點公開在 hello hello 公司網路邊緣上。 也就是從 Azure toohello 公司網路時，不成立起始 hello VPN。

請注意，額外費用 適用於擴充超過 hello 的標準收費適用於 tooeach VM 的虛擬網路 tooyour 與內部網路時。 具體來說，費用支付 CPU 時間的 hello Azure 虛擬網路閘道，而也橫跨 hello VPN 與內部部署電腦通訊的每部 VM 所產生的 hello 輸出流量。 如需網路流量費用的詳細資訊，請參閱 [Azure 價格一覽](http://azure.microsoft.com/pricing/)。

### <a name="BKMK_DeploymentConfig"></a>DC 部署組態
hello 的方式來設定的 hello DC 依存於 hello 需求 hello 服務您想在 Azure 上的 toorun。 例如，您可能會部署新的樹系，與您自己公司的樹系隔離，進行測試的概念證明、 新的應用程式或某些其他短期專案需要目錄服務，但未指定存取 toointernal 公司資源。

一個好處是，隔離的樹系 DC 不會複寫與內部部署網域控制站，導致較少輸出 hello 系統本身，所產生的網路流量並直接降低成本。 如需網路流量費用的詳細資訊，請參閱 [Azure 價格一覽](http://azure.microsoft.com/pricing/)。

另舉一例，假設您有服務的隱私權需求，但 hello 服務依存於存取 tooyour 內部 Windows Server Active Directory。 如果您允許 toohost hello 服務 hello 雲端中的資料，您可以為內部樹系在 Azure 上部署新的子網域。 在此情況下，您可以部署 DC，hello 新子網域 （不含 hello 通用類別目錄中的順序 toohelp 處理隱私權問題）。 此案例連同複本 DC 部署，需要虛擬網路以與內部部署 DC 連接。

如果您建立新的樹系時，選擇是否 toouse [Active Directory 信任](https://technet.microsoft.com/library/cc771397)或[同盟信任](https://technet.microsoft.com/library/dd807036)。 平衡相容性、 安全性、 規範、 成本和恢復功能所需的 hello 要求。 例如，tootake 利用[選擇性驗證](https://technet.microsoft.com/library/cc755844)您可能會選擇 toodeploy 在 Azure 上的新樹系和 Windows Server Active Directory 之間建立信任 hello 內部部署樹系與 hello 雲端樹系。 如果 hello 應用程式之可感知宣告，不過，您可能會部署而不是 Active Directory 樹系信任的同盟信任。 另一個因素將 hello 成本 tooeither 複寫更多資料透過 Windows Server Active Directory toohello 雲端擴充您的內部或產生更多傳出流量，因為驗證和查詢負載。

可用性和容錯的需求也會影響您的選擇。 例如，如果 hello 連結中斷了，利用 Kerberos 信任或同盟信任的應用程式可能都會完全中斷，除非您已經部署在 Azure 上足夠的基礎結構。 替代部署組態，例如複本 Dc (可寫入或 Rodc) 增加 hello 的能 tootolerate 連結中斷的可能性。

### <a name="BKMK_ADSiteTopology"></a>Windows Server Active Directory 網站拓撲
您需要 toocorrectly 定義站台和站台連結中順序 toooptimize 流量，並將成本降至最低。 站台、 站台連結和子網路會影響 Dc 之間的驗證流量的 hello 流程 hello 複寫拓撲。 請考慮下列流量費用的 hello 然後部署和設定網域控制站，根據您的部署案例 toohello 需求：

* 會每小時的 hello 閘道本身支付工本費：
  
  * 您可以自行斟酌啟動或停止
  * 如果停止，Azure Vm 就會與 hello 公司網路隔離
* 輸入流量是免費的
* 輸出流量的收費依據太[Azure 定價在摘要](http://azure.microsoft.com/pricing/)。 您可以最佳化內部部署網站與 hello 雲端網站之間的站台連結內容，如下所示：
  
  * 如果您使用多個虛擬網路，設定 hello 網站連結與其成本適當地排列 hello Azure 從 tooprevent Windows Server AD DS 站台過去一可以提供相同服務層級的免費 hello。 您也可以考慮停用 hello 橋接所有網站連結 (BASL) 選項 （預設為啟用）。 這可確保只有直接連接的網站彼此複寫。 過渡連接網站中的網域控制站就不再能夠 tooreplicate 彼此直接，但必須透過共同網站複寫。 如果基於某些原因，hello 介網站變成無法使用，即使 hello 站台間連線可以使用，將不會發生過渡連接網站中 Dc 之間的複寫。 最後，其中的複寫行為區段依然需要過渡，建立站台包含 hello 適當的站台連結和網站，例如內部部署公司網路站台連結橋接器。
  * [設定站台連結成本](https://technet.microsoft.com/library/cc794882)適當 tooavoid 意想不到的流量。 例如，如果**嘗試下一個最接近的網站**設定時，請確定站台不是接下來 hello hello 虛擬網路最接近藉由增加 hello 連接 hello Azure 站台後 toohello hello 站台連結物件的相關聯的成本公司網路。
  * 設定站台連結[間隔](https://technet.microsoft.com/library/cc794878)和[排程](https://technet.microsoft.com/library/cc816906)根據 tooconsistency 需求和物件變更的速率。 對齊複寫排程與延遲容許範圍。 網域控制站複寫只 hello 最後一個值的狀態，因此如果沒有足夠的物件變更速率降低 hello 複寫間隔可節省成本。
* 如果將成本降至最低是優先事項，請確定已排程複寫且變更通知未啟用。 站台之間複寫時，這會是 hello 預設組態。 這並不重要，如果您要部署的虛擬網路上的 RODC，因為 hello RODC 不會複寫任何傳出的變更。 但是，如果您部署可寫入的 DC，您應該確定 hello 站台連結不是設定的 tooreplicate 更新，而不需要的頻率。 如果您部署通用類別目錄伺服器 (GC)，請確定其他每一個包含 GC 的站台從來源站台連結會連接到站台中的 DC 複寫網域分割區，或具有較低的成本的站台連結比 hello 中的 GC hello Azure 站台。
* 很可能 toofurther 仍會降低藉由變更 hello 複寫壓縮演算法的站台間複寫所產生的網路流量。 hello 壓縮演算法是由 hello REG_DWORD 登錄項目 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator 壓縮演算法來控制。 hello 預設值為 3，toohello Xpress Compress 演算法相互關聯。 您可以變更 hello 值 too2，哪些變更 hello 演算法 tooMSZip。 在大部分情況下，這會增加 hello 壓縮，但會以 hello 的 CPU 使用量的費用。 如需詳細資訊，請參閱 [Active Directory 複寫拓撲如何運作](https://technet.microsoft.com/library/cc755994)。

### <a name="BKMK_IPAddressDNS"></a>IP 位址和 DNS
Azure 虛擬機器預設會配置「DHCP 租用位址」。 因為與虛擬機器的 Azure 虛擬網路動態位址是 hello hello 虛擬機器的存留期間保存，所以符合 Windows Server AD ds 的 hello 需求。

如此一來，當您在 Azure 上使用動態位址，您會使用靜態 IP 位址，因為它可路由傳送 hello 段 hello 租用，而且 hello hello 租用期間就等於 toohello hello 雲端服務的存留期的作用中。

不過，如果 hello VM 會關閉，會取消配置 hello 動態位址。 您可以 tooprevent hello 取消配置的 IP 位址，[使用 Set-azurestaticvnetip tooassign 靜態 IP 位址](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx)。

針對名稱解析，部署您自己 （或利用現有） DNS 伺服器基礎結構Azure 提供的 DNS 不符合 hello 進階名稱解析需求 Windows Server AD DS。 例如，不支援動態 SRV 記錄等等。 名稱解析是 DC 和加入網域的用戶端的重要組態項目。 DC 必須能夠註冊資源記錄及解析其他 DC 的資源記錄。
基於容錯和效能理由，是最佳 tooinstall hello Windows Server DNS 服務在 Azure 上執行的 hello Dc 上。 Hello 名稱與 hello DNS 伺服器 IP 位址，然後設定 hello Azure 虛擬網路屬性。 當 hello 虛擬網路上的其他 Vm 啟動時，其 DNS 用戶端解析程式設定會設定與 DNS 伺服器 hello 動態 IP 位址配置的一部分。

> [!NOTE]
> 您無法加入內部部署電腦 tooa Windows Server AD DS Active Directory 網域，會直接透過網際網路 hello Azure 上裝載。 針對 Active Directory 和 hello 網域加入作業轉譯它並不實用 toodirectly 公開 hello 必要的連接埠，且有作用，整個 DC toohello 網際網路 hello 連接埠需求。
> 
> 

VM 會在啟動或有名稱變更時自動註冊其 DNS 名稱。

如需此範例，說明如何 tooprovision hello 第一個 VM，並在其上安裝 AD DS 的另一個範例的詳細資訊，請參閱[Microsoft Azure 上安裝新的 Active Directory 樹系](active-directory-new-forest-virtual-machine.md)。 如需使用 Windows PowerShell 的詳細資訊，請參閱[安裝 Azure PowerShell](/powershell/azureps-cmdlets-docs) 和 [Azure 管理 Cmdlet](/powershell/module/azurerm.compute/#virtual_machines)。

### <a name="BKMK_DistributedDCs"></a>地理位置分散 DC
在不同的虛擬網路上裝載多個 DC 時，Azure 提供一些優點︰

* 多網站容錯
* 實際接近 toobranch 辦公室 （較低延遲）

如需設定虛擬網路之間直接進行通訊的資訊，請參閱[設定虛擬網路 toovirtual 網路連接性](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。

### <a name="BKMK_RODC"></a>唯讀 DC
您需要 toochoose 是否 toodeploy 讀取-只有或可寫入網域控制站。 您可能會想的 toodeploy Rodc，因為您將不會有實體控制權停留，但是 Rodc 設計的 toobe 部署其實體安全性的風險，例如分公司辦公室位置。

Azure 沒有分公司辦公室，hello 實體安全性風險，但是 Rodc 經過證明可能還是 toobe 更符合成本效益，因為 hello 功能提供適合的 toothese 環境，雖然原因非常不同。 例如，Rodc 有沒有傳出複寫，並會無法 tooselectively 擴展秘密 （密碼）。 在 hello 缺點 hello 缺少這些密碼可能需要視輸出流量 toovalidate 他們的使用者或電腦進行驗證。 但是，密碼可以選擇性地預先填入及快取。

Rodc 提供額外的優點 HBI 和 PII 顧慮，因為您可以加入屬性包含機密資料 toohello RODC 已篩選屬性集 (FAS)。 hello FAS 是一組可自訂的屬性不是複寫的 tooRODCs。 如果您不允許或不想 toostore PII 或 HBI，在 Azure 上的，您可以使用 hello FAS 當做保護。 如需詳細資訊，請參閱 [RODC 已篩選屬性集[(https://technet.microsoft.com/library/cc753459)]。

請確定應用程式將會與 Rodc 相容您計劃 toouse。 許多 Windows Server Active Directory 功能的應用程式適用於 Rodc，但某些應用程式可以無效率地執行，或如果不需要存取 tooa 失敗可寫入的 DC。 如需詳細資訊，請參閱 [唯讀 DC 應用程式相容性指南](https://technet.microsoft.com/library/cc755190)。

### <a name="BKMK_GC"></a>通用類別目錄
您是否需要 toochoose tooinstall 通用類別目錄 (GC)。 在單一網域樹系中，您應該將所有 DC 設為通用類別目錄伺服器。 這樣不會增加成本，因為沒有任何額外複寫流量。

在多重網域樹系中，Gc hello 驗證程序期間，進行必要 tooexpand 萬用群組成員資格。 如果您未部署 GC，hello 虛擬網路上針對在 Azure 上的 DC 驗證的工作負載將會間接產生傳出驗證流量 tooquery Gc 內部期間每個驗證嘗試。

hello 與 Gc 相關聯的成本會比較無法預測的因為它們會裝載每個網域 （部分）。 如果 hello 工作負載裝載面對網際網路服務，且會驗證使用者的 Windows Server AD DS，hello 成本可能完全無法預測。 toohelp 在驗證期間減少 hello 雲端網站之外的 GC 查詢，您可以[啟用萬用群組成員資格快取](https://technet.microsoft.com/library/cc816928)。

### <a name="BKMK_InstallMethod"></a>安裝方法
您需要如何 toochoose tooinstall hello Dc hello 虛擬網路上：

* 升級新的 DC。 如需詳細資訊，請參閱 [在 Azure 虛擬網路上安裝新的 Active Directory 樹系](active-directory-new-forest-virtual-machine.md)。
* 移動 hello 在內部部署虛擬 DC 的 toohello 雲端的 VHD。 在此情況下，您必須確定該 hello 在內部部署虛擬 DC 會 「 移動 」 沒有 「 複製 」 或 「 複製 」。

作為僅 Azure 虛擬機器的網域控制站 （相對於的 tooAzure"web"或 「 背景工作 」 角色 Vm）。 它們很持久，而且需要 DC 狀態的持久性。 Azure 虛擬機器是針對類似 DC 的工作負載而設計的。

請勿使用 SYSPREP toodeploy 或複製 Dc。 hello 能力 tooclone 網域控制站是從開始才能使用 Windows Server 2012 中。 hello 複製功能需要 hello 基礎 hypervisor 中的 VMGenerationID 支援。 Windows Server 2012 和 Azure 虛擬網路中的 Hyper-V 都支援 VMGenerationID，如同協力廠商虛擬化軟體廠商一樣。

### <a name="BKMK_PlaceDB"></a>Hello Windows Server AD DS 資料庫和 SYSVOL 的位置
選取 toolocate hello Windows Server AD DS 資料庫、 記錄以及 SYSVOL 的位置。 必須部署在 Azure 資料磁碟上。

> [!NOTE]
> Azure 資料磁碟會受條件約束的 too1 TB。
> 
> 

根據預設，資料磁碟機未快取寫入。 資料磁碟的磁碟機附加的 tooa VM 使用直接寫入式快取。 直接寫入式快取會確定 hello 寫入認可的 toodurable Azure 儲存體之前會 hello 交易已完成從 hello 觀點來看的 hello VM 的作業系統。 它提供在 hello 費用的稍微慢一點寫入的持久性。

這是很重要的 Windows Server AD DS，因為貫穿式寫入磁碟快取失效 hello DC 所做的假設。 Windows Server AD DS 會嘗試 toodisable 寫入快取，但它已啟動 toohello 磁碟 IO 系統 toohonor 它。 失敗 toodisable 寫入快取，在某些情況下，會引進 USN 回復導致物件逗留和其他問題。

對虛擬 Dc 的最佳作法是，不要 hello 遵循：

* Hello 主機快取喜好設定設為 無 hello Azure 資料磁碟。 這可避免 AD DS 作業的寫入快取問題。
* Hello 相同的資料磁碟或不同的資料磁碟上儲存 hello 資料庫、 記錄檔和 SYSVOL。 一般而言，這是用於 hello 作業系統本身的 hello 磁碟從不同的磁碟。 hello 重點就是該 hello Windows Server AD DS 資料庫和 SYSVOL 不得儲存在 Azure 作業系統磁碟類型。 根據預設，hello AD DS 安裝程序會安裝這些元件在 %systemroot%資料夾，但是不建議在 Azure 中。

### <a name="BKMK_BUR"></a>備份與還原
請注意通常對於 DC 的備份與還原支援和不支援的項目，具體而言，就是在 VM 中執行的項目。 請參閱 [虛擬化 DC 的備份與還原考量](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers)。

建立系統狀態備份，方法是只使用特別知道 Windows Server AD DS 的備份需求的備份軟體，例如 Windows Server Backup。

請勿複製 (copy) 或複製 (clone) DC 的 VHD 檔案，而是執行定期備份。 如果需要還原，使用複製的 VHD 而未使用 Windows Server 2012 和支援的 hypervisor 會產生 USN 泡沫。

### <a name="BKMK_FedSrvConfig"></a>同盟伺服器組態
Windows Server AD FS 同盟伺服器 (Sts) 的 hello 組態部分取決於 hello 應用程式是否要在 Azure 上的 toodeploy 需要 tooaccess 在內部部署網路上的資源。

如果 hello 應用程式符合下列準則的 hello，您可以從您的內部網路部署 hello 中隔離的應用程式。

* 它們接受 SAML 安全性權杖
* 它們是 exposable toohello 網際網路
* 它們不會存取內部部署資源

在此情況下，設定 Windows Server AD FS STS，如下所示︰

1. 在 Azure 上設定隔離的單一網域樹系。
2. 藉由設定 Windows Server AD FS 同盟伺服器陣列中提供同盟的存取 toohello 樹系。
3. Hello 在內部部署樹系中設定 Windows Server AD FS （同盟伺服器陣列和同盟伺服器 proxy 伺服器陣列）。
4. 建立 hello 內部部署與 Windows Server AD FS 的 Azure 執行個體之間的同盟信任關係。

在 hello 另一方面，如果 hello 應用程式需要存取 tooon 內部部署資源，您可以設定 Windows Server AD FS 與 Azure 上的 hello 應用程式，如下所示：

1. 設定內部部署網路與 Azure 之間的連接。
2. Hello 在內部部署樹系中設定 Windows Server AD FS 同盟伺服器陣列。
3. 在 Azure 上設定 Windows Server AD FS 同盟伺服器 Proxy 伺服器陣列。

這個組態具有減少 hello 暴露在內部部署資源的類似 tooconfiguring Windows Server AD FS 與應用程式在周邊網路中的 hello 優點。

請注意，在任一案例中，如果需要企業對企業共同作業，您可以建立具有多個識別提供者的信任關係。

### <a name="BKMK_CloudSvcConfig"></a>雲端服務組態
雲端服務所需，如果您想 tooexpose VM 直接 toohello 網際網路或 tooexpose 網際網路對向負載平衡應用程式。 這是可行的，因為每個雲端服務提供一個可設定虛擬 IP 位址。

### <a name="BKMK_FedReqVIPDIP"></a>公用和私人 IP 位址 (動態 IP 與虛擬 IP) 的同盟伺服器需求
每個 Azure 虛擬機器會接收動態 IP 位址。 動態 IP 位址是只能在 Azure 中存取的私人位址。 不過，在大部分情況下，它將會需要 tooconfigure Windows Server AD FS 部署的虛擬 IP 位址。 hello 虛擬 IP 必要 tooexpose Windows Server AD FS 端點 toohello 網際網路，並將用於同盟的合作夥伴和用戶端驗證和持續管理。 虛擬 IP 位址是雲端服務的屬性，該雲端服務包含一或多個 Azure 虛擬機器。 如果在 Azure 和 Windows Server AD FS 上部署的 hello 宣告感知應用程式面對網際網路並且共用共同的連接埠，都需要自己的虛擬 IP 位址，它將因此需要 toocreate hello 應用程式的一個雲端服務和第二個為 Windows Server AD FS。

Hello 條款虛擬 IP 位址和動態 IP 位址的定義，請參閱[詞彙和定義](#BKMK_Glossary)。

### <a name="BKMK_ADFSHighAvail"></a>Windows Server AD FS 高可用性組態
雖然可能 toodeploy 獨立 Windows Server AD FS 同盟服務，它會建議使用 toodeploy 包含至少兩個節點的伺服陣列 AD FS STS 和生產環境的 proxy。

請參閱[AD FS 2.0 部署拓撲考量](https://technet.microsoft.com/library/gg982489)在 hello [AD FS 2.0 設計指南](https://technet.microsoft.com/library/dd807036)toodecide 的部署組態選項最適合您的特定需求。

> [!NOTE]
> 順序 tooget 負載平衡中在 Azure 上、 Windows Server AD FS 端點設定 hello hello Windows Server AD FS 伺服器陣列的所有成員相同雲端服務，而使用 hello 負載平衡的 Azure 功能的 HTTP （預設值 80） 和 HTTPS 連接埠 （預設為 443）。 如需詳細資訊，請參閱 [Azure 負載平衡器探查](https://msdn.microsoft.com/library/azure/jj151530)。
> Azure 不支援 Windows Server 網路負載平衡 (NLB)。
> 
> 

