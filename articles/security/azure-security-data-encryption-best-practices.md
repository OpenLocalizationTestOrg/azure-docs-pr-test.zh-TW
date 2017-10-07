---
title: "aaaData 安全性和加密的最佳作法 |Microsoft 文件"
description: "本文提供使用內建 Azure 功能的一些資料安全性和加密最佳作法。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Azure 資料安全性和加密最佳作法
其中一個 hello 雲端中的 hello 金鑰 toodata 保護佔用 hello 可能是您的資料，以及哪些控制項為適用於該狀態的可能狀態。 Azure 資料安全性和加密最佳作法的 hello 目的 hello 建議周圍 hello 下列資料的狀態是：

* 待用︰這包括實體媒體 (磁碟或光碟) 上以靜態方式存在的所有資訊儲存物件、容器和類型。
* 傳輸中： 當資料之間傳送元件、 位置或程式，例如透過 hello 網路跨服務匯流排 （從內部部署 toocloud，反之亦然，包括例如 ExpressRoute 的混合式連線），或輸入/輸出時處理程序，它會被視為在影片。

本文將討論 Azure 資料安全性和加密最佳作法的集合。 這些最佳作法衍生自我們的經驗與 Azure 資料安全性和加密和 hello 經驗的客戶，像是您自己。

針對每個最佳作法，我們會說明︰

* 哪些 hello 最佳作法是
* 為什麼要 tooenable 該最佳作法
* 如果您無法 tooenable hello 最佳作法，可能 hello 結果
* 可能的替代方式 toohello 最佳作法
* 如何了解 tooenable hello 最佳作法

此 Azure 資料安全性和加密的最佳做法文章根據共識意見，Azure 平台功能和功能集，存在於 hello 撰寫本文時。 隨時間變更的意見和技術，且這篇文章會定期 tooreflect 上更新這些變更。

本文討論的 Azure 資料安全性和加密最佳作法包括︰

* 強制執行 Multi-Factor Authentication
* 使用角色型存取控制 (RBAC)
* 加密 Azure 虛擬機器
* 使用硬體安全性模型
* 透過安全的工作站管理
* 啟用 SQL 資料加密
* 保護傳輸中的資料
* 強制執行檔案層級資料加密

## <a name="enforce-multi-factor-authentication"></a>強制執行 Multi-Factor Authentication
hello 第一個步驟中的資料存取和 Microsoft Azure 中的控制是 tooauthenticate hello 使用者。 [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) 是除了使用使用者名稱與密碼之外，利用其他方法驗證使用者身分識別的驗證方法。 這種驗證方法協助保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。

藉由為使用者啟用 Azure MFA，您會加入第二層安全性 toouser 登入和交易。 在此情況下，交易可能會存取位於檔案伺服器或 SharePoint Online 中的文件。 Azure MFA 也可協助 IT tooreduce hello 可能性遭入侵的認證將會有存取 tooorganization 資料。

例如： 如果您對您的使用者強制執行 Azure MFA，並將它設定 toouse 通話或簡訊為驗證，如果 hello 使用者的認證遭到入侵，hello 攻擊者將不會是能 tooaccess 任何資源，因為他不會存取 toouser 電話。 不要新增此額外的識別身分保護的組織會更容易受到認證遭竊攻擊，這可能會導致 toodata 洩露。

一種替代方法，適用於想 tookeep hello 驗證控制組織單位是 toouse [Azure Multi-factor Authentication Server](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)，也稱為 MFA 內部部署。 使用此方法則仍可無法 tooenforce 多重要素驗證，同時保留 hello MFA server 內部部署。

如需 Azure MFA 的詳細資訊，請閱讀 hello 文章[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。

## <a name="use-role-based-access-control-rbac"></a>使用角色型存取控制 (RBAC)
限制存取權限 hello[需要 tooknow](https://en.wikipedia.org/wiki/Need_to_know)和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則。 這是必要的 tooenforce 安全性原則所需的資料存取的組織。 Azure 角色型存取控制 (RBAC) 可以使用的 tooassign 權限 toousers、 群組和應用程式在特定範圍內。 訂用帳戶、 資源群組或單一資源，可以是 hello 範圍的角色指派。

您可以利用[內建的 RBAC 角色](../active-directory/role-based-access-built-in-roles.md)Azure tooassign 權限 toousers。 請考慮使用*儲存體帳戶參與者*需要 toomanage 儲存體帳戶的雲端操作員和*傳統儲存體帳戶參與者*角色 toomanage 傳統儲存體帳戶。 對於需要 toomanage Vm 和儲存體帳戶的雲端操作員，請考慮將它們新增到太*虛擬機器參與者*角色。

未利用諸如 RBAC 等功能來強制執行資料存取控制的組織，可能會對其使用者提供超過所需的權限。 這可能會導致 toodata 洩露，讓某些使用者需要存取 toodata 他們不應該有在 hello 第一個位置。

您可以進一步了解 Azure rbac 進行讀取 hello 文章[所有存取控制](../active-directory/role-based-access-control-configure.md)。

## <a name="encrypt-azure-virtual-machines"></a>加密 Azure 虛擬機器
對許多組織來說，[待用資料加密](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/)是達到資料隱私性、法規遵循及資料主權的必要步驟。 Azure 磁碟加密可讓 IT 系統管理員 tooencrypt Windows 和 Linux IaaS 虛擬機器 (VM) 的磁碟。 Azure 磁碟加密會利用 hello 業界標準 BitLocker 功能的 Windows 和 Linux tooprovide 磁碟區加密 hello OS hello DM Crypt 功能和 hello 資料磁碟。

您可以利用 Azure 磁碟加密 toohelp 保護與防衛資料 toomeet 您組織的安全性和法規遵循需求。 組織也應該考慮使用加密 toohelp 降低風險相關的 toounauthorized 資料存取。 也建議您加密磁碟機先前 toowriting 敏感性資料 toothem。

請確定 tooencrypt VM 的資料磁碟區與開機磁碟區，順序 tooprotect 資料留在您的 Azure 儲存體帳戶中。 保護 hello 加密金鑰和密碼，利用[Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。

針對您在內部部署的 Windows 伺服器，請考慮下列最佳作法，加密的 hello:

* 使用 [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) 進行資料加密
* 在 AD DS 中儲存修復資訊。
* 如果沒有任何 BitLocker 金鑰已遭入侵的顧慮，我們建議您可以格式化 hello 磁碟機 tooremove hello BitLocker 中繼資料從 hello 磁碟機，或您的所有執行個體解密和重新加密整個磁碟機 hello。

不會強制進行資料加密的組織會更有可能公開 toobe toodata 完整性問題，例如惡意或惡意使用者竊取的資料，並且危害帳戶取得未經授權的存取 toodata 清除格式。 除了這些風險，公司已經有具有業界規範 toocomply 必須證明他們是努力一些，而且使用 hello 正確的安全性控制項 tooenhance 資料安全性。

您可以進一步了解 Azure 磁碟加密藉由讀取 hello 文章[Azure 磁碟加密用於 Windows 及 Linux IaaS Vm](azure-security-disk-encryption.md)。

## <a name="use-hardware-security-modules"></a>使用硬體安全性模型
業界加密解決方案會使用祕密金鑰 tooencrypt 資料。 因此，務必安全地儲存這些金鑰。 金鑰管理會變成不可或缺的一部分資料保護，因為它將會是使用的 tooencrypt 資料的運用 toostore 祕密金鑰。

Azure 磁碟加密使用[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)toohelp 您控制，和您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會都加密在靜止於 Azure 中管理磁碟加密金鑰和密碼儲存體。 您應該使用 Azure 金鑰保存庫 tooaudit 金鑰和原則使用方式。

有許多固有的風險相關的 toonot 位置 tooprotect hello 祕密金鑰所使用的 tooencrypt 在您的資料具有適當的安全性控制。 如果攻擊者可以存取 toohello 祕密金鑰，它們會是能 toodecrypt hello 資料，也可能會發生存取 tooconfidential 資訊。

您可以進一步了解 Azure 中的憑證管理的一般建議閱讀 hello 文章[在 Azure 中的憑證管理： 準則](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)。

如需 Azure 金鑰保存庫的詳細資訊，請閱讀[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)。

## <a name="manage-with-secure-workstations"></a>透過安全的工作站管理
Hello 絕大多數 hello 攻擊目標 hello 終端使用者，因為 hello 端點會變成其中一個 hello 的攻擊的主要點。 如果攻擊者危害 hello 端點，他可以利用 hello 使用者的認證 toogain 存取 tooorganization 的資料。 大多數的端點攻擊都是可以 tootake hello 事實是使用者在其本機工作站的系統管理員的優點。

您可以使用安全的管理工作站來降低這些風險。 我們建議您改用[特殊權限存取工作站 (PAW)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce hello 受攻擊面工作站中的。 這些安全的管理工作站可協助您減輕其中一些攻擊，以確保您的資料更為安全。 向您的工作站，請確定 toouse PAW tooharden 和鎖定。 這是機密帳戶，工作和資料保護的重要步驟 tooprovide 高安全性保證。

缺少 endpoint protection 可能會面臨風險的資料，請確定 tooenforce 安全性原則是使用的 tooconsume 資料，不論 hello 資料位置 （雲端或內部部署） 的所有裝置上。

您可以了解有關特殊權限存取工作站讀取 hello 發行項[保護特殊權限存取](https://technet.microsoft.com/library/mt631194.aspx)。

## <a name="enable-sql-data-encryption"></a>啟用 SQL 資料加密
[Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/dn948096.aspx)(TDE) 可協助防範惡意活動的 hello 威脅所執行的即時加密與解密的 hello 資料庫相關聯的備份和交易記錄檔不含靜止需要變更 toohello 應用程式。  TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。

Hello 整個儲存已加密，即使它是非常重要 tooalso 加密資料庫本身。 這是 hello 防禦保護資料的深度方法的實作。 如果您使用[Azure SQL Database](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx)想 tooprotect 敏感性資料，例如信用卡或身分證號碼，您可以加密的資料庫與 FIPS 140-2 符合許多 hello 要求已驗證的 256 位元 AES 加密例如，HIPAA （PCI） 的業界標準。

它是太相關之檔案的重要 toounderstand[緩衝集區延伸模組](https://msdn.microsoft.com/library/dn133176.aspx)(BPE) 使用 TDE 加密資料庫時，不會加密。 您必須使用檔案系統層級加密工具，例如 BitLocker 或 hello[加密檔案系統](https://technet.microsoft.com/library/cc700811.aspx)(EFS) 針對 BPE 相關檔案。

因為授權的使用者等安全性系統管理員或資料庫管理員可以存取 hello 資料即使 hello 資料庫經過加密與 TDE，您也應該遵循下列的 hello 建議：

* Hello 資料庫層級 SQL 驗證
* 使用 RBAC 角色的 Azure AD 驗證
* 使用者和應用程式應該使用不同的帳戶 tooauthenticate。 如此一來，您可以限制 hello toousers 和應用程式授與的權限，並減少惡意活動的 hello 風險
* 實作資料庫層級安全性使用固定的資料庫角色 （例如 db_datareader 或 db_datawriter），或您可以建立自訂的角色，為您的應用程式 toogrant tooselected 明確權限的資料庫物件

不使用資料庫層級加密的組織可能更容易受到攻擊，進而危害 SQL Database 中的資料。

您可以進一步了解 SQL TDE 加密藉由讀取 hello 文章[Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx)。

## <a name="protect-data-in-transit"></a>保護傳輸中的資料
保護傳輸中的資料應該是您的資料保護策略中不可或缺的部分。 因為資料會從許多位置來回移動，hello 一般建議您一律使用 SSL/TLS 通訊協定 tooexchange 資料分散在不同的位置。 在某些情況下，您可能想 tooisolate hello 整個通訊通道，您的內部部署與雲端之間使用虛擬私人網路 (VPN) 的基礎結構。

對於在內部部署基礎結構與 Azure 之間移動的資料，您應該考慮適當的防護措施，例如 HTTPS 或 VPN。

針對需要從多個工作站位在內部 tooAzure toosecure 存取的組織，使用[Azure 站台對站 VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md)。

對於組織，需要從一個工作站 toosecure 存取位於內部部署 tooAzure，使用[點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)。

較大的資料集可以透過專用的高速 WAN 連結 (例如 [ExpressRoute](https://azure.microsoft.com/services/expressroute/)) 移動。 如果您選擇 toouse ExpressRoute，您也可以加密 hello 資料在 hello 應用程式層級使用[SSL/TLS](https://support.microsoft.com/kb/257591)或為了提高保護其他通訊協定。

如果透過 hello Azure 網站互動與 Azure 儲存體，所有交易將會透過 HTTPS 都發生。 [儲存體 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)透過 HTTPS 也可以與使用的 toointeract [Azure 儲存體](https://azure.microsoft.com/services/storage/)和[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。

失敗 tooprotect 資料在傳輸過程中的組織就更容易受到如[攔截攻擊](https://technet.microsoft.com/library/gg195821.aspx)，[竊聽](https://technet.microsoft.com/library/gg195641.aspx)和工作階段攔截。 Hello 第一個步驟中獲得存取 tooconfidential 資料時，可以是這些攻擊。

您可以進一步了解 Azure VPN 選項藉由讀取 hello 文章[規劃和設計 VPN 閘道](../vpn-gateway/vpn-gateway-plan-design.md)。

## <a name="enforce-file-level-data-encryption"></a>強制執行檔案層級資料加密
另一層可以提高資料安全性 hello 層級的保護加密 hello 檔案，本身，不管 hello 檔案位置。

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx)使用加密、 身分識別及授權原則 toohelp 保護您的檔案和電子郵件。 Azure RMS 可跨多個裝置運作 — 手機、平板電腦和 PC。保護您的組織內部和外部 這項功能可能是保護的因為 Azure RMS，增加一層，即使在離開組織範圍也不如影隨形 hello 資料。

當您使用 Azure RMS tooprotect 檔案時，您正在使用業界標準密碼編譯的完整支援[FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html)。 當您利用 Azure RMS 的資料保護時，即使它是不受 hello 控制複製的 toostorage 擁有 hello 檔案便可持續受到保護 hello 的 hello 保證 IT，例如雲端儲存體服務。 hello 相同發生時透過電子郵件共用的檔案、 hello 檔案受到保護做為附件 tooan 電子郵件訊息，指示如何 tooopen hello 受保護的附件。

規劃 Azure RMS 採用時 hello 下列建議：

* 安裝 hello [RMS 共用應用程式](https://technet.microsoft.com/library/dn339006.aspx)。 此應用程式會藉由安裝 Office 增益集來與 Office 應用程式整合，讓使用者可以輕鬆地直接保護檔案。
* 設定應用程式和服務 toosupport Azure RMS
* 建立可反映您的業務需求的[自訂範本](https://technet.microsoft.com/library/dn642472.aspx)。 例如︰最高秘密資料的範本應套用於所有最高機密相關的電子郵件。

弱式上的組織[資料分類](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf)，檔案保護可能更容易受到 toodata 外洩。 沒有適當的檔案保護組織不會是能 tooobtain 商業見解、 監督濫用情形，並防止惡意存取 toofiles。

您可以進一步了解 Azure RMS 閱讀 hello 文章[開始使用 Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx)。
