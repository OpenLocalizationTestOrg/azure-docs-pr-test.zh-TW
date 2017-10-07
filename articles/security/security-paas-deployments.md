---
title: "aaaSecuring PaaS 部署 |Microsoft 文件"
description: " 了解 hello 安全性優點 PaaS 和其他雲端服務模型，並了解建議的做法，來保護您的 Azure PaaS 部署。 "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>保護 PaaS 部署

本文提供的資訊可協助您：

- 了解 hello 安全性優點裝載 hello 雲端中的應用程式
- 評估 hello 安全性優點的平台即服務 (PaaS) 和其他雲端服務模型
- 變更安全性焦點從網路中心 tooan 識別為中心的周邊安全性方法
- 實作一般 PaaS 安全性最佳做法建議

## <a name="cloud-security-advantages"></a>雲端安全性優點
沒有安全性優點 toobeing hello 雲端中。 在內部部署環境中，組織可能有業的責任和有限的資源可用 tooinvest 在安全性中，會建立攻擊者的所有層級的弱點可能會無法 tooexploit 所在的環境。

![雲端時代的安全性優點][1]

組織會使用的提供者以雲端為基礎的安全性功能和雲端 intelligence 可以 tooimprove 其威脅偵測和回應時間。  移位責任 toohello 雲端提供者，組織即可取得更多安全性涵蓋範圍，讓他們 tooreallocate 安全性資源與預算 tooother 商務優先順序。

## <a name="division-of-responsibility"></a>責任劃分
很重要的 toounderstand hello 地分隔您與 Microsoft 之間的責任。 內部部署，您擁有 hello 整疊，但當您移動 toohello 雲端一些責任轉移 tooMicrosoft。 hello 下列責任矩陣顯示 hello 區域 hello 堆疊在 SaaS、 PaaS 和 IaaS 部署中，您必須負責，而且 Microsoft 會負責。

![責任區][2]

就所有雲端部署類型而言，您擁有您的資料和身分識別。 您需負責保護資料和身分識別，在內部部署資源的 hello 安全性和 hello 雲端元件，您可以控制 （這會因服務型別）。

一律會保留您 hello 類型，不論的責任是部署的：

- 資料
- 端點
- 帳戶
- 存取管理

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>PaaS 雲端服務模型的安全性優點
使用 hello 相同責任矩陣，讓我們看看 hello 安全性優點與在內部部署的 Azure PaaS 部署。

![PaaS 的安全性優點][3]

開始在 hello 底部 hello 堆疊，hello 實體基礎結構，Microsoft 可降低常見的風險和責任。 因為 microsoft 持續監視 hello Microsoft 雲端時，很難 tooattack。 不會更有意義的攻擊者 toopursue hello Microsoft 雲端為目標。 除非 hello 攻擊者有許多 money 和資源、 hello 攻擊者的是可能 toomove tooanother 目標上。  

在 hello 堆疊的 hello 中間 PaaS 部署，而且在內部部署之間沒有差異。 在 hello 應用程式層與 hello 帳戶和存取管理的圖層上，您會有類似的風險。 Hello 下一節步驟這篇文章，我們將引導您刪除或降低這些風險 toobest 作法。

在 hello 頂端 hello 堆疊、 資料控管和 rights management，您必須可減輕金鑰管理的風險。 (金鑰管理涵蓋在最佳做法中)。額外的責任金鑰管理時，您必須在 PaaS 部署，您不再擁有 toomanage，因此您可以移動資源 tookey 管理中的區域。

hello Azure 平台也提供強式 DDoS 保護透過使用各種網路為基礎的技術。 不過，所有類型的網路型 DDoS 保護方法在每一連結和每一資料中心上都有其限制。 toohelp 避免 hello 影響大型 DDoS 攻擊，您可以利用 Azure 的核心雲端功能，讓您 tooquickly 和自動向外的擴充 toodefend DDoS 攻擊。 在 hello 建議做法文件中的做法，我們會討論更詳細說明。

## <a name="modernizing-hello-defenders-mindset"></a>種 hello defender 的心態
PaaS 部署可以讓您的整體方法 toosecurity 內的排班。 您不需要的所有項目 toocontrol 轉移自行 toosharing 與 Microsoft 的責任。

PaaS 和傳統內部部署之間的另一個重要差異是所定義的 hello 主要的安全性範疇的新檢視。 在過去，hello 主要內部部署安全性周邊網路，最內部的安全性設計使用 hello 網路為其主要安全性樞紐。 PaaS 部署您服務會比較好考慮識別 toobe hello 主要的安全性範疇。

## <a name="identity-as-hello-primary-security-perimeter"></a>Hello 主要的安全性範疇和身分識別
其中一個 hello 五種基本的特性的雲端運算廣泛的網路存取，可讓網路中心考慮較不相關。 大部分的雲端運算 tooallow 使用者 tooaccess 資源，無論位置 hello 目標。 對大多數使用者，其位置正在 toobe 某處 hello 網際網路上。

hello 下圖顯示如何從網路周邊 tooan 識別周邊發展 hello 安全性範疇。 安全性會變成較少的相關定義網路和更多關於保護您的資料，以及管理您的應用程式和使用者的 hello 安全性。 hello 主要差異是您想 toopush 安全性較接近 toowhat 的重要 tooyour 公司。

![以身分識別作為新的安全性周邊][4]

一開始，Azure PaaS 服務 (例如 Web 角色和 Azure SQL) 提供極少或未提供任何傳統網路周邊防禦。 它可了解 hello 項目的目的是公開 toobe toohello 網際網路 （web 角色），並驗證提供 hello 新周邊 （例如，BLOB 或 SQL Azure）。

現代的安全性作法會假設該 hello 敵人已違反 hello 周邊網路。 因此，現代防禦作法已經移動 tooidentity。 組織必須以增強式驗證與授權防疫 (最佳做法) 建立身分識別型安全性周邊。

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>管理 hello 識別周邊建議的

原則和 hello 周邊網路的模式是十年。 相較之下，hello 產業有較低的經驗與 hello 主要的安全性範疇使用身分識別。 不過，我們已經累積足夠的經驗 tooprovide 已通過驗證的 hello 欄位中的某些一般性建議，並套用 tooalmost 所有 PaaS 服務。

hello 以下摘要說明一般的最佳做法方法 toomanaging 識別外圍。

- **您的金鑰或憑證不會喪失**金鑰和認證的安全性很重要的 toosecure PaaS 部署。 遺失金鑰和認證是相當常見的問題。 一個很好的解決方案是 toouse 集中型解決方案金鑰和秘密可以儲存在硬體安全性模組 (HSM)。 Azure 會提供搭配 hello 雲端 HSM [Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)。
- **不要將認證和其他機密放原始程式碼或 GitHub** hello 只有事情更糟的是比遺失您的金鑰和認證是否有未經授權的合作對象取得存取 toothem。 攻擊者所能 tootake bot 技術 toofind 金鑰和密碼儲存在程式碼儲存機制，例如 GitHub 的優點。 請勿將金鑰和密碼放在這些公用原始程式碼儲存機制中。
- **保護混合式 PaaS 和 IaaS 服務上的 VM 管理介面**：IaaS 和 PaaS 服務是在虛擬機器 (VM) 上執行。 根據服務的 hello 類型，有數個管理介面可讓您 tooremote 直接管理這些 Vm。 可使用的遠端管理通訊協定包括像是[安全殼層通訊協定 (SSH)](https://en.wikipedia.org/wiki/Secure_Shell)、[遠端桌面通訊協定 (RDP)](https://support.microsoft.com/kb/186607) 及[遠端 PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting)。 一般情況下，我們建議您不要啟用遠端的直接存取 tooVMs 從 hello 網際網路。 您應該使用替代方法 (如果可用)，例如使用虛擬私人網路來連線到 Azure 虛擬網路。 如果沒有替代方法可用，則請務必使用複雜密碼，並且如果可以使用雙重要素驗證 (例如 [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md))，便使用此驗證。
- **使用增強式驗證與授權平台**

  - 使用 Azure AD 中的同盟身分識別，而不要使用自訂使用者存放區。 當您使用同盟身分識別時，您充分利用平台為基礎的方法和委派的身分識別授權的 tooyour 協力廠商的 hello 管理。 同盟識別身分方法時尤其重要案例中的員工會終止，而且需要 toobe 資訊會反映透過多個身分識別和授權的系統。
  - 使用平台提供的驗證與授權機制，而不要使用自訂程式碼。 hello 原因是，開發自訂驗證程式碼可能會出錯。 大部分的開發人員不安全專家，而不太可能 toobe 留意 hello 微妙 hello 中驗證和授權的最新發展。 商業程式碼 (例如來自 Microsoft) 通常都經過廣泛的安全性檢閱。
  - 使用多重要素驗證。 多因素驗證，則為目前的 hello 標準驗證和授權，因為它可避免 hello 的安全性弱點中使用者名稱和密碼的驗證類型。 存取 tooboth hello Azure 管理 （入口網站/遠端 PowerShell） 介面與服務直接公開 toocustomer 應該設計並設定及 toouse [Azure Multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md)。
  - 使用標準驗證通訊協定，例如 OAuth2 和 Kerberos。 這些通訊協定已經過廣泛的對等檢閱，而可能作為您驗證與授權平台程式庫的一部分來實作。

## <a name="next-steps"></a>後續步驟
在本文中，我們是將焦點放在 Azure PaaS 部署的安全性優點。 接下來，請了解適用於保護您 PaaS Web 和行動解決方案的建議做法。 我們將從 Azure App Service、Azure SQL Database 及「Azure SQL 資料倉儲」開始著手。 發行項上的其他 Azure 服務的建議作法可用，hello 下列清單中將會提供連結：

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database 和 Azure SQL Data Warehouse](security-paas-applications-using-sql.md)
- Azure 儲存體
- Azure REDIS Cache
- Azure 服務匯流排
- Web 應用程式防火牆

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
