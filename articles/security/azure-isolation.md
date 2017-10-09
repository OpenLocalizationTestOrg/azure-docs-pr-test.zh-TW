---
title: "hello Azure 公用雲端中的 aaaIsolation |Microsoft 文件"
description: "深入了解雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可以自動 toomeet hello 需求的應用程式或企業上下調整的服務。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Hello Azure 公用雲端中的隔離
##  <a name="introduction"></a>簡介
### <a name="overview"></a>概觀
了解 tooassist 目前和預期 Azure 客戶，並利用 hello 各種安全性相關功能中提供和周圍 hello Azure 平台，Microsoft 開發了一系列的技術白皮書、 安全性概觀、 最佳作法，並檢查清單。
hello 廣度及深度方面的主題範圍，並定期更新。 這份文件摘要在下列的 hello 抽象節為該系列的一部分。

### <a name="azure-platform"></a>Azure 平台
Azure 是作業系統的開放式且彈性的雲端服務平台支援的程式設計語言、 架構、 工具、 資料庫和裝置 hello 最大範圍的選取範圍。 例如，您可以：
- 透過 Docker 整合執行 Linux 容器；
- 使用 JavaScript、Python、.NET、PHP、Java 和 Node.js 建置應用程式；以及
- 建置 iOS、Android 和 Windows 裝置的後端。

Microsoft Azure 支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您建置，或 IT 資產移轉至公用雲端服務提供者、 您依賴該組織的能力 tooprotect 應用程式和資料與 hello 服務 」 和 「 hello 」 控制項提供您雲端架構的 toomanage hello 安全性資產。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂安全性 toomeet hello 獨特需求您的部署。 本文件可協助您符合這些需求。

### <a name="abstract"></a>摘要

Microsoft Azure 可讓您 toorun 應用程式和虛擬機器 (Vm) 上共用的實體基礎結構。 Hello 能力 toodistribute hello 成本多個客戶之間共用資源的其中一個雲端環境中的 hello 經濟的主要動機 toorunning 應用程式。 這種多重租用的作法會以低成本在不同客戶間進行資源的多工處理來提升效率。 不幸的是，它也帶來 hello 風險的實體伺服器和其他基礎結構資源 toorun 共用機密的應用程式和任意 tooan 和潛在惡意使用者可能屬於的 Vm。

本文概述如何 Microsoft Azure 提供針對惡意和非惡意使用者隔離，並藉由提供各種隔離選項 tooarchitects 架構的雲端解決方案，可作為指南。 這份技術白皮書 hello 技術的 Azure 平台與客戶對向的安全性控制，而不會嘗試 tooaddress Sla 定價模型和 DevOps 作法的考量。

## <a name="tenant-level-isolation"></a>租用戶層級隔離
Hello 的雲端運算同時在眾多客戶共用的通用基礎結構的概念、 前置 tooeconomies 標尺的主要優點的其中一個。 這個概念稱為多重租用。 Microsoft 會持續努力 tooensure hello 多租用戶架構的 Microsoft 雲端 Azure 支援安全性、 機密性、 隱私權、 完整性和可用性的標準。

Hello 具備雲端功能的工作地點中的租用戶可以定義為用戶端或組織所擁有及管理該雲端服務的特定執行個體。 與 Microsoft Azure 提供的 hello 識別身分平台中，租用戶是只是 Azure Active Directory (Azure AD)，您的組織時接收和擁有註冊 Microsoft 雲端服務的專用執行個體。

每個 Azure AD 目錄都不同，並與其他 Azure AD 目錄分開。 如同公司辦公大樓是安全資產的特定 tooonly 您的組織，Azure AD 目錄也已設計的 toobe 由您的組織使用的安全資產。 hello Azure AD 架構可隔離客戶資料與識別身分資訊，避免兩者混淆。 這表示某個 Azure AD 目錄的使用者和系統管理員無法意外或惡意存取另一個目錄中的資料。

### <a name="azure-tenancy"></a>Azure 租用
Azure 租用戶 （Azure 訂用帳戶） 是指 tooa"客戶/billing"關聯性和唯一[租用戶](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant)中[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)。 Microsoft Azure 中的租用戶層級隔離是使用 Azure Active Directory 及其所提供的[角色型控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)來達成。 每個 Azure 訂用帳戶都會與一個 Azure Active Directory (AD) 目錄相關聯。

使用者、 群組和從該目錄的應用程式可以管理 hello Azure 訂用帳戶中的資源。 您可以指派這些使用 hello Azure 入口網站、 Azure 命令列工具，以及 Azure 管理 Api 的存取權限。 Azure AD 租用戶邏輯上是使用安全性界限來隔離，如此一來就沒有任何客戶可以存取或危害共同的租用戶 (不論是惡意或意外)。 Azure AD 是在已隔離網路區段上隔離之「裸機」伺服器上執行的，其中主機層級的封包篩選和 Windows 防火牆會封鎖來路不明的連接和流量。

- 在 Azure AD 中的存取 toodata 需要使用者驗證，透過[安全性權杖服務 (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)。 Hello 授權系統 toodetermine 是否 hello 要求的存取 toohello 目標租用戶這位使用者所需的授權此工作階段中，會使用 hello 使用者存在、 已啟用的狀態和角色的詳細資訊。

![Azure 租用](./media/azure-isolation/azure-isolation-fig1.png)


- 租用戶是獨立的容器，而且彼此間沒有任何關聯性。

- 除非租用戶管理員透過同盟或佈建來自其他租用戶的使用者帳戶授與存取權，否則租用戶之間無法存取。

- 組成 hello Azure AD 服務，並直接存取 tooAzure 廣告的後端系統的實體存取 tooservers 會受到限制。

- Azure AD 使用者沒有存取 toophysical 資產或位置，且因此不讓它們 toobypass hello 邏輯 RBAC 原則檢查所述之後。

針對診斷與維護需求，必須使用採用 Just-In-Time 權限提高系統的作業模型。 Azure AD Privileged Identity Management (PIM) 引進了 hello 概念合格的系統管理員。[合格管理員](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)應該是偶爾需要特殊存取權限而非每一天都需要此權限的使用者。 hello 角色未作用中，直到 hello 使用者需要存取時，，然後完成啟動程序，並成為使用中的系統管理員預先決定的一段時間。

![Azure AD 特殊權限身分識別管理](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory 裝載自己受保護的容器，與 hello 容器僅擁有及管理的 hello 租用戶中的原則和權限 tooand 中每個租用戶。

租用戶容器 hello 概念深度 ingrained hello 目錄服務，所有層級中，從入口網站中，所有 hello 方式 toopersistent 儲存體。

即使從多個 Azure Active Directory 租用戶中繼資料儲存在 hello 相同的實體磁碟，hello 以外 hello 目錄服務，取決 hello 租用戶系統管理員所定義的容器之間沒有任何關聯性。

### <a name="azure-role-based-access-control-rbac"></a>Azure 角色型存取控制 (RBAC)
[Azure 角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)可協助您 tooshare Azure 訂用帳戶內可用的各種元件，藉由提供 Azure 的精細存取管理。 Azure RBAC 可讓您組織內的 toosegregate 責任和授與存取權依據哪些使用者需要 tooperform 他們的工作。 您不需為每個人授與 Azure 訂用帳戶或資源中無限制的權限，而是只允許執行特定的動作。

Azure RBAC 具有三個套用 tooall 資源類型的基本角色：

- **擁有者**具有完整存取 tooall 資源，包括 hello 右 toodelegate 存取 tooothers。

- **參與者**可以建立及管理 Azure 資源的所有類型，但無法授與存取 tooothers。

- **讀者** 可以檢視現有的 Azure 資源。

![Azure 角色型存取控制](./media/azure-isolation/azure-isolation-fig3.png)

hello RBAC 角色在 Azure 中的 hello rest 允許特定的 Azure 資源管理。 例如，hello 虛擬機器參與者角色可讓 hello 使用者 toocreate 及管理虛擬機器。 它沒有提供這些存取 toohello Azure 虛擬網路或 hello hello 虛擬機器的子網路連線到。

[RBAC 內建角色](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles)清單可在 Azure 中的 hello 角色。 它會指定 hello 作業和每個內建的角色會授與 toousers 的範圍。 如果您要尋找 toodefine 您自己的角色的更多控制，請參閱如何 toobuild [Azure rbac 進行中的自訂角色](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles)。

Azure Active Directory 的一些其他功能包括：
- Azure AD 可讓 SSO tooSaaS 應用程式，不論裝載的位置。 有些應用程式會與 Azure AD 同盟，有些則使用密碼 SSO。 同盟應用程式也能支援使用者佈建和[密碼儲存庫存 (英文)](https://www.techopedia.com/definition/31415/password-vault)。

- 在存取 toodata [Azure 儲存體](https://azure.microsoft.com/services/storage/)控制透過驗證。 每個儲存體帳戶有主索引鍵 ([儲存體帳戶金鑰](https://docs.microsoft.com/azure/storage/storage-create-storage-account)，或 SAK) 和次要的秘密金鑰 （hello 共用的存取簽章或 SAS）。

- Azure AD 可透過與內部部署目錄的同盟、同步和複寫提供「身分識別即服務」(使用 [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs))。

- [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)是 hello 多因素驗證服務，需要使用行動裝置應用程式、 電話或簡訊來進行使用者 tooverify 登入。 它可以搭配 Azure AD toohelp 安全的內部資源與 hello Azure Multi-factor Authentication server，以及自訂應用程式和使用 hello SDK 的目錄。

- [Azure AD 網域服務](https://azure.microsoft.com/services/active-directory-ds/)可讓您將 Azure 虛擬機器 tooan Active Directory 網域，而不需部署網域控制站。 您可以使用 Active Directory 公司認證登入 toothese 虛擬機器，且您 Azure 的虛擬機器上使用群組原則 tooenforce 安全性基準管理已加入網域的虛擬機器。

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)提供縮放 toohundreds 數百萬個身分識別的高可用性的全域身分識別管理服務的消費者導向應用程式。 此服務可跨行動及 Web 平台進行整合。 取用者可以登入 tooall 您的應用程式，透過可自訂的方式使用其現有的社交帳戶，或建立認證。

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>從 Microsoft 管理員及資料刪除中隔離
Microsoft 會強式的量值 tooprotect 不適當的存取或未經授權的人員使用您的資料。 這些作業的程序和控制項都由 hello[線上服務條款](http://aka.ms/Online-Services-Terms)，哪一種優惠契約承諾控管存取 tooyour 資料。

-   Microsoft 工程師 hello 雲端中沒有預設存取 tooyour 資料。 而是只有在必要時，才會在有管理監督的情況下授與他們權限。 該存取權會受到仔細的控制及記錄，並於不再需要時撤銷。

-   Microsoft 可能會雇用其他公司 tooprovide 有限的服務，代替它。 次承攬可能存取客戶的資料只有 toodeliver hello 服務，本公司已雇用它們 tooprovide，並禁止他們將其用於任何其他目的。 此外，它們是資訊的針對合約所繫結的 toomaintain hello 機密性的客戶。

商務服務稽核的認證與 ISO/IEC 27001 定期經過 Microsoft 及 accredited 稽核公司，執行範例稽核 tooattest 該存取權，只適用於正當商業用途。 您一律可基於任何原因，隨時存取您自己的客戶資料。

如果您刪除任何資料，Microsoft Azure 刪除 hello 資料，包括任何快取或備份的複本。 刪除該範圍內的服務，會發生 hello 保留期限的 hello 結尾之後的 90 天內。 (Hello 資料處理條款一節中所定義的範圍內的服務我們[線上服務條款](http://aka.ms/Online-Services-Terms)。)

如果用來儲存磁碟機因硬體失敗，會安全地[清除或終結](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data)Microsoft 就會傳回 toohello 製造商更換或修復之前。 hello hello 磁碟機上的資料會覆寫 hello 資料的 tooensure 無法透過任何方式復原。

## <a name="compute-isolation"></a>計算隔離
Microsoft Azure 提供各種雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可自動 toomeet hello 需求的應用程式或企業上下調整規模服務。 這些計算執行個體和服務提供在多個層級 toosecure 資料隔離不會犧牲在組態中的 hello 彈性該客戶的需求。

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>根 VM 與客體 VM 之間的 Hyper-V 和根 OS 隔離
Azure 的計算平台會以機器虛擬化為基礎，這表示所有客戶程式碼都會在 Hyper-V 虛擬機器中執行。 在每個 Azure 節點 （或網路端點），沒有識別碼 」 的 Hypervisor 直接在 hello 硬體上執行，並分成變動數目的客體虛擬機器 (Vm) 中的節點。


![根 VM 與客體 VM 之間的 Hyper-V 和根 OS 隔離](./media/azure-isolation/azure-isolation-fig4.jpg)


每個節點也有一個特殊根 VM 所執行 hello 主機作業系統。 重要的界限是 hello 隔離 hello 客體 Vm 中的 hello 根目錄 VM 以及互相，交由 hello hypervisor 和 hello 根 OS hello 客體 Vm。 hello hypervisor 根 OS 配對會利用 Microsoft 的數十作業系統安全性體驗和較新的學習來自 Microsoft 的 HYPER-V 中的客體 Vm tooprovide 嚴密隔離。

hello Azure 平台會使用虛擬化的環境。 使用者執行個體做為獨立虛擬機器不具有存取 tooa 實體主機伺服器，並使用實體處理器 (環形-0/環形-3) 權限層級強制執行這種隔離。

Ring 0 是最小權限和 3 的 hello 至少為 hello。 hello 客體作業系統會在較低權限環形 1，且應用程式中執行 hello 最小權限的環形 3。 此虛擬化的實體資源會導致 tooa 清楚的區隔客體 OS 與 hypervisor，導致之間 hello 兩個額外的安全性隔離。

hello Azure hypervisor 像是微核心和使用共用記憶體介面呼叫 VMBus，從客體虛擬機器 toohello 主機進行處理傳遞硬體的所有存取要求。 這可防止使用者取得未經處理的讀取/寫入/執行存取 toohello 系統，並可減少 hello 風險共用系統資源。

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>進階 VM 放置演算法與提供保護來抵禦旁道攻擊
任何跨 VM 攻擊包含兩個步驟： hello 做為其中一個 hello 犧牲者的 Vm，相同主機上放置敵人控制的 VM，然後違反 hello 隔離界限 tooeither 竊取機密犧牲者資訊，或影響充滿貪欲或破壞其效能。 Microsoft Azure 會透過兩個步驟提供保護：使用進階的 VM 放置演算法，並提供保護來抵禦所有已知的旁道攻擊，包括鄰點干擾的 VM。

### <a name="hello-azure-fabric-controller"></a>hello Azure 網狀架構控制器
從 hello 主機 toovirtual 機器管理單向通訊和 hello Azure 網狀架構控制器負責配置 tootenant 工作負載，基礎結構資源。 hello VM 放演算法 hello Azure 網狀架構控制器會是非常複雜，幾乎不可能 toopredict 與實體主機層級。

![hello Azure 網狀架構控制器](./media/azure-isolation/azure-isolation-fig5.png)

hello Azure hypervisor 會強制執行記憶體和處理序的區隔的虛擬機器，並安全地路由傳送網路流量 tooguest OS 租用戶。 這會消除 VM 層級發生旁道攻擊的可能性。

在 Azure 中，特殊的 hello 根 VM 是： 它會執行強化呼叫 hello 根 OS 裝載作業系統的網狀架構代理程式 」 (FA)。 FAs 用於開啟 toomanage 客體代理程式 (GA) customer Vm 上的客體作業系統內。 FA 也會管理儲存體節點。

hello Azure hypervisor，集合的根 OS /FA 和客戶的 Vm/天然氣包含計算節點。 FA 是由網狀架構控制器 (FC) 管理的，其存在於計算和儲存體節點 (計算和儲存體叢集是由個別 FC 管理的) 以外的地方。 如果執行時，客戶會更新他們的應用程式組態檔，hello FC 會與通訊 hello FA，然後連絡 Ga，其中通知 hello 組態變更的 hello 應用程式。 在 hello 事件中的硬體故障，hello FC 會自動尋找可用的硬體，並重新啟動 hello VM。

![Azure 網狀架構控制器](./media/azure-isolation/azure-isolation-fig6.jpg)

從網狀架構控制器 tooan 代理程式的通訊是單向的。 hello 代理程式 」 實作只會從 hello 控制站的回應 toorequests SSL 保護服務。 它不能起始連接 toohello 控制器或其他特殊權限的內部節點。 hello FC 會處理所有回應，就好像它們是不受信任。


![網狀架構控制器](./media/azure-isolation/azure-isolation-fig7.png)

從 hello 客體 Vm 中的根 VM 和 hello 客體 Vm 與其他延伸隔離。 計算節點也會為了加強保護而從儲存體節點隔離出來。


hello hypervisor 和 hello 主機作業系統提供的網路封包-篩選 toohelp 確保未受信任的虛擬機器無法產生詐騙的流量，或接收流量不解決 toothem、 直接流量 tooprotected 基礎結構端點，或傳送/接收不適當的廣播的流量。


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>其他規則設定網狀架構控制器和代理程式 tooIsolate VM
根據預設，當建立虛擬機器時，並接著 hello 網狀架構控制器和代理程式設定 hello 封包篩選 tooadd 規則和例外狀況 tooallow 授權流量封鎖所有流量。

以下為要進行程式設計的兩種規則：

-   **機器組態或基礎結構規則**：依預設會封鎖所有通訊。 發生例外狀況 tooallow 虛擬機器 toosend 而且接收 DHCP 和 DNS 流量。 虛擬機器時，也可以傳送流量 toohello 「 公用 」 網際網路及傳送流量 tooother 虛擬機器內 hello 相同 Azure 虛擬網路和 hello OS 啟動伺服器。 允許連出目的地 hello 虛擬機器的清單不包含 Azure 路由器的子網路、 Azure 管理，以及其他 Microsoft 內容。

-   **角色組態檔：**這會定義輸入存取控制清單 (Acl) 以 hello 租用戶的服務模型為基礎的 hello。

### <a name="vlan-isolation"></a>VLAN 隔離
每個叢集中有三個 VLAN：

![VLAN 隔離](./media/azure-isolation/azure-isolation-fig8.jpg)


-   hello 主要 VLAN – 連接不受信任的客戶節點

-   hello FC VLAN – 包含受信任 FCs 和支援系統

-   hello 裝置 VLAN – 包含受信任的網路和其他基礎結構裝置

允許通訊的 hello FC VLAN toohello 主要 VLAN，但無法從主要 VLAN toohello hello FC VLAN 起始。 主要 VLAN toohello 裝置 hello VLAN 也會封鎖通訊。 如此可確保即使執行的客戶程式碼的節點遭到洩露時，它不能攻擊 hello FC 或裝置 Vlan 上的節點。

## <a name="storage-isolation"></a>儲存體隔離
### <a name="logical-isolation-between-compute-and-storage"></a>計算和儲存體之間的邏輯隔離
Microsoft Azure 的基本設計是將以 VM 為基礎的計算與儲存體分隔開來。 此隔離可讓計算和儲存體 tooscale 獨立，因此更容易 tooprovide 多租用戶隔離。

因此，與沒有網路連線 tooAzure 不同硬體上執行的 Azure 儲存體計算除了以邏輯方式。 [這](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)表示，在建立虛擬磁碟時，不會將磁碟空間配置給它的整個產能。 相反地，資料表會建立對應 hello hello 實體磁碟上的虛擬磁碟 tooareas 上的位址，該資料表最初是空的。 **hello 客戶將資料寫入 hello 虛擬磁碟，會配置 hello 實體磁碟上的空間，而指標 tooit 放在 hello 資料表的第一次。**
### <a name="isolation-using-storage-access-control"></a>使用儲存體存取控制進行隔離
**Azure 儲存體中的存取控制**具有簡單的存取控制模型。 每個 Azure 訂用帳戶都能建立一或多個儲存體帳戶。 每個儲存體帳戶都有單一使用的 toocontrol 存取 tooall 資料，該儲存體帳戶中的秘密金鑰。

![使用儲存體存取控制進行隔離](./media/azure-isolation/azure-isolation-fig9.png)

**存取 tooAzure 儲存資料 （包括資料表）**可以透過控制[SAS （共用存取簽章）](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)權杖中，哪些授與範圍的存取。 hello SAS 透過查詢範本建立 (URL)，以 hello 簽署[SAK （儲存體帳戶金鑰）](https://msdn.microsoft.com/library/azure/ee460785.aspx)。 [簽章 URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)可以獲得 tooanother 程序 （也就，委派），然後填入 hello 的 hello 查詢的詳細資料，並提出 hello hello 儲存體服務的要求。 SAS 可讓您 toogrant 時間為基礎的存取 tooclients 不碰到 hello 儲存體帳戶的秘密金鑰。

hello SAS 表示我們可以授與用戶端有限的權限，tooobjects 我們對指定期間的時間與指定權限集的儲存體帳戶中。 我們可以授與這些有限權限，而不需要 tooshare 帳戶存取金鑰。

### <a name="ip-level-storage-isolation"></a>IP 層級儲存體隔離
您可以建立防火牆，並且為受信任的用戶端定義 IP 位址範圍。 使用 IP 位址範圍，只具有 hello 定義範圍內的 IP 位址的用戶端可以太連線[Azure 儲存體](https://docs.microsoft.com/azure/storage/storage-security-guide)。

IP 存放的資料可以防止未經授權的使用者透過網路的機制，是使用的 tooallocate 流量 tooIP 儲存體專用或專用通道。

### <a name="encryption"></a>加密
Azure 會提供下列類型的加密 tooprotect 資料：
-   傳輸中加密

-   待用加密

#### <a name="encryption-in-transit"></a>傳輸中加密
傳輸中加密是透過網路傳輸資料時用來保護資料的機制。 透過 Azure 儲存體，您可以使用下列各項來保護資料：

-   [傳輸層級加密](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit)，例如從 Azure 儲存體傳入或傳出資料時的 HTTPS。

-   [連線加密](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)，例如 Azure 檔案共用的 SMB 3.0 加密。

-   [用戶端加密](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage)，tooencrypt hello 資料在傳輸之前儲存和 toodecrypt hello 資料超出儲存體傳輸後。

#### <a name="encryption-at-rest"></a>待用加密
對許多組織來說， [待用資料加密](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 是達到資料隱私性、法規遵循及資料主權的必要步驟。 有三個 Azure 功能可提供「待用」資料的加密。

-   [儲存體服務加密](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest)可讓您 toorequest 寫入它 tooAzure 儲存體時，hello 儲存體服務會自動加密資料。

-   [用戶端加密](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption)也提供的加密在靜止 hello 功能。

-   [Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器所使用的資料磁碟。

#### <a name="azure-disk-encryption"></a>Azure 磁碟加密
適用於虛擬機器 (VM) 的 [Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)會使用您在 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 中所控制的金鑰與原則來將 VM 磁碟 (包括開機和資料磁碟) 加密，以協助您達成組織安全性與合規性需求。

hello 適用於 Windows 的磁碟加密解決方案根據[Microsoft BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)，並且根據 hello Linux 方案[dm crypt](https://en.wikipedia.org/wiki/Dm-crypt)。

hello 解決方案支援 IaaS Vm 的下列案例，當啟用 Microsoft Azure 中的 hello:
-   與 Azure 金鑰保存庫整合

-   標準層 VM：A、D、DS、G、GS 等系列 IaaS VM

-   在 Windows 和 Linux IaaS VM 上啟用加密

-   為 Windows IaaS VM 的 OS 和資料磁碟機停用加密

-   為 Linux IaaS VM 的資料磁碟機停用加密

-   在執行 Windows 用戶端 OS 的 IaaS VM 上啟用加密

-   在具有掛接路徑的磁碟區上啟用加密

-   在使用 [mdadm (英文)](https://en.wikipedia.org/wiki/Mdadm) 設定等量磁碟 (RAID) 的 Linux VM 上啟用加密

-   在使用資料磁碟適用之 [LVM (邏輯磁碟區管理員) (英文)](https://msdn.microsoft.com/library/windows/desktop/bb540532) 的 Linux VM 上啟用加密

-   在使用儲存空間設定的 Windows VM 上啟用加密

-   所有 Azure 公用區域皆受到支援

hello 方案不支援下列案例、 功能和技術 hello 版本中的 hello:

-   基本層 IaaS VM

-   在 Linux IaaS VM 的 OS 磁碟機上停用加密

-   使用 hello 傳統 VM 建立方法所建立的 IaaS Vm

-   與您的內部部署金鑰管理服務整合

-   Azure 檔案 (共用檔案系統)、網路檔案系統 (NFS)、動態磁碟區和以軟體型 RAID 系統所設定的 Windows VM

## <a name="sql-azure-database-isolation"></a>SQL Azure 資料庫隔離
SQL Database 是關聯式資料庫中的服務會根據 hello 領導市場的 Microsoft SQL Server 引擎和能夠處理關鍵任務工作負載的 hello Microsoft 雲端。 SQL Database 提供帳戶層級的可預測資料隔離 (以地理位置/區域為基礎和以網路為基礎)；幾乎全都不需管理。

### <a name="sql-azure-application-model"></a>SQL Azure 應用程式模型

[Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) 資料庫是以 SQL Server 技術為基礎來建置的雲端型關聯式資料庫服務。 它會在雲端中提供由 Microsoft 裝載的高可用性、可調整、多租用戶的資料庫服務。

從應用程式的觀點而言，SQL Azure 提供 hello 下列階層： 每個層級內含項目-一對多的以下層級。

![SQL Azure 應用程式模型](./media/azure-isolation/azure-isolation-fig10.png)

hello 帳戶和訂用帳戶。 Microsoft Azure 平台概念 tooassociate 計費與管理

邏輯伺服器和資料庫是 SQL Azure 特有的概念，可使用 SQL Azure 來管理，其中提供了 OData 和 TSQL 介面，或是透過整合到 Azure 入口網站的 SQL Azure 入口網站來管理。

SQL Azure 伺服器不是實體或 VM 執行個體，而是資料庫、共用管理和安全性原則的集合，其儲存於所謂的「邏輯 master」資料庫中。

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

邏輯 master 資料庫包括：

-   使用 tooconnect toohello 伺服器的 SQL 登入

-   防火牆規則

帳單及使用量的相關資訊 hello 從 SQL Azure 資料庫的相同邏輯伺服器不保證在 hello toobe SQL Azure 叢集中有相同的實體執行個體，而是應用程式時，必須提供 hello 目標資料庫名稱連接。

從客戶觀點來看，邏輯伺服器中建立圖形地理區域中的 hello 區域中的 hello 叢集的其中一個 hello 伺服器 hello 實際建立時。

### <a name="isolation-through-network-topology"></a>透過網路拓撲進行隔離

當邏輯伺服器就會建立並註冊其 DNS 名稱時，hello DNS 名稱指向 toohello 所謂 「 閘道 VIP"位址的 hello 特定的資料中心 hello 伺服器放置的位置。

後方 hello VIP （虛擬 IP 位址），我們有無狀態的閘道服務的集合。 通常，若在多個資料來源 (master 資料庫、使用者資料庫等) 之間需要進行協調，就會牽涉到閘道。 閘道服務會實作下列 hello:
-   **TDS 連接 Proxy 處理。** 這包括尋找 hello 後端叢集中的使用者資料庫、 實作 hello 登入順序，然後轉寄來回 hello TDS 封包 toohello 後端。

-   **資料庫管理。** 這包括實作工作流程 toodo CREATE/ALTER/DROP database 作業的集合。 hello 資料庫作業可以叫用探查 TDS 封包或明確的 OData Api。

-   CREATE/ALTER/DROP 登入/使用者作業

-   透過 OData API 的邏輯伺服器管理作業

![透過網路拓撲進行隔離](./media/azure-isolation/azure-isolation-fig12.png)

hello 閘道後方的 hello 層稱為 「 後端 」。 這是高可用性的方式儲存所有 hello 資料。 每個資料片段是前述的 toobelong tooa 「 分割 」 或 「 容錯移轉單位 」，每個需要至少三個複本。 複本所儲存和複寫的 SQL Server 引擎和管理的容錯移轉通常稱為系統 tooas 「 網狀架構 」。

一般而言，hello 後端系統無法通訊輸出 tooother 系統基於安全性考量。 這是保留的 toohello 系統在 hello 前端 （閘道） 層。 hello 閘道層機器做為深度防禦機制有限的權限 hello 後端機器 toominimize hello 受攻擊面。

### <a name="isolation-by-machine-function-and-access"></a>透過機器功能與存取進行隔離
SQL Azure 是由在不同機器功能上執行之服務組成的。 SQL Azure 會將資料分為 「 後端 」 雲端資料庫和 「 前端 」 （閘道/管理） 環境中，與 hello 的流量只移到後端，以及不出的一般原則。hello 前端環境可以互相通訊 toohello 之外的其他服務的世界，而且在一般情況下，只具有有限的 hello 後端 （足夠 toocall hello 進入點它需要 tooinvoke） 中的權限。

## <a name="networking-isolation"></a>網路隔離
Azure 部署具有多層網路隔離。 hello 下列圖表顯示 Azure 提供 toocustomers 網路隔離的各種層面。 這些圖層都是原生 hello Azure 平台本身中的，而且客戶定義的功能。 輸入 hello 網際網路，從 Azure DDoS 提供對 Azure 大規模攻擊的隔離。 hello 下一層是隔離的客戶定義的公用 IP 位址 （端點），也就是隔離的使用的 toodetermine 哪些流量可以通過 hello 雲端服務 toohello 虛擬網路。 原生 Azure 虛擬網路隔離可確保與其他所有網路完全隔離，而且流量只能流經使用者設定的路徑和方法。 這些路徑和方法的 hello 下一層，Nsg、 UDR 和網路的虛擬應用裝置可以是使用的 toocreate 隔離界限 tooprotect hello 應用程式部署在受保護的 hello 網路中。

![網路隔離](./media/azure-isolation/azure-isolation-fig13.png)

**流量隔離：** A[虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)hello Azure 平台上的 hello 流量隔離界限。 一個虛擬網路中的虛擬機器 (Vm) 無法通訊，直接在不同虛擬網路中，即使這兩個虛擬網路建立的 tooVMs hello 同一位客戶。 隔離是很重要的屬性，可確保客戶 VM 和通訊仍然隱蔽於虛擬網路內。

[子網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets)使用以 IP 範圍為基礎的虛擬網路，來提供額外的隔離層級。 Hello 虛擬網路中的 IP 位址，您可以將虛擬網路分割成多個子網路的組織和安全性。 Vm 和 PaaS 角色部署的執行個體 toosubnets （相同或不同） VNet 中可與對方進行通訊，而不需要任何額外的設定。 您也可以設定[網路安全性群組 (Nsg)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow 或拒絕網路流量 tooa VM 執行個體根據 NSG 的存取控制清單 (ACL) 中設定的規則。 NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。 NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。

## <a name="next-steps"></a>後續步驟

- [適用於 Windows Azure 虛擬網路中之機器的網路隔離選項 (英文)](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

這包括 hello 傳統前端和後端案例特定後端網路或子網路中的機器可能只會讓某些用戶端或其他電腦 tooconnect tooa 特定端點的白名單的 IP 位址為基礎。

- [計算隔離 (英文)](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure 提供各種雲端運算服務，其中包含寬的選取範圍的計算執行個體 （& s） 可自動 toomeet hello 需求的應用程式或企業上下調整規模服務。

- [儲存體隔離 (英文)](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure 會將以客戶 VM 為基礎的計算從儲存體中分隔出來。 此隔離可讓計算和儲存體 tooscale 獨立，因此更容易 tooprovide 多租用戶隔離。 因此，與沒有網路連線 tooAzure 不同硬體上執行的 Azure 儲存體計算除了以邏輯方式。 所有要求都會根據客戶的選擇，透過 HTTP 或 HTTPS 來執行。

