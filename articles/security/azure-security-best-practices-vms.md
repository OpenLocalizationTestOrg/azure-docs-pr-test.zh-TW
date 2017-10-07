---
title: "aaaAzure 虛擬機器的安全性最佳作法 |Microsoft 文件"
description: "本文章提供各種不同的安全性位在 Azure 虛擬機器中使用最佳作法 toobe。"
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Azure VM 安全性的最佳作法

在大部分的基礎結構即服務 (IaaS) 案例中， [Azure 虛擬機器 (Vm)](https://docs.microsoft.com/en-us/azure/virtual-machines/) hello 使用雲端的組織的主要工作負載所計算。 這項事實特別明顯是在[混合式案例](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx)組織想 tooslowly 移轉工作負載 toohello 雲端的位置。 在這種情況下，請遵循 hello [IaaS 的一般安全性考量](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)，並套用安全性最佳作法 tooall Vm。

這篇文章討論各種 VM 安全性最佳作法，每個都衍生自我們的客戶和我們自己使用 VM 的直接體驗。

hello 最佳作法為基礎的意見，共識，並使用目前的 Azure 平台功能及功能設定。 因為意見和技術，可以變更一段時間，我們計劃 tooupdate 這文章定期 tooreflect 這些變更。

每個最佳作法，hello 文章說明：

* 哪些 hello 最佳作法是。
* 原因是個不錯的主意 tooenable 它。
* 如何了解 tooenable 它。
* 如果您無法 tooenable 可能會發生什麼事它。
* 可能的替代方式 toohello 最佳作法。

hello 發行項會檢查下列安全性最佳作法時，VM 的 hello:

* VM 驗證和存取控制
* VM 可用性和網路存取
* 強制執行加密以保護 VM 中待用資料的安全
* 管理您的 VM 更新
* 管理您的 VM 安全性狀態
* 監視 VM 效能

## <a name="vm-authentication-and-access-control"></a>VM 驗證和存取控制

保護您的 VM hello 第一個步驟是 tooensure 只有獲得授權的使用者可以 tooset 啟動新的 Vm。 您可以使用[Azure 資源管理員原則](../azure-resource-manager/resource-manager-policy.md)tooestablish 慣例，在您的組織中的資源建立自訂的原則，並套用這些原則 tooresources，例如[資源群組](../azure-resource-manager/resource-group-overview.md).

Vm 自然屬於 tooa 資源群組會繼承其原則。 雖然我們建議此方式 toomanaging Vm，您也可以控制存取 tooindividual VM 原則使用[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)。

當您啟用資源管理員的原則和 RBAC toocontrol VM 存取時，您協助我們改善整體 VM 安全性。 我們建議您以相同的生命週期到 hello hello 合併 Vm 相同的資源群組。 藉由使用資源群組，您可以部署、監視和彙總資源的計費成本。 tooenable 使用者 tooaccess 和設定的 Vm，使用[最低權限的方法](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models)。 然後當您指派權限 toousers，計劃 toouse hello 下列內建的 Azure 角色：

- [虛擬機器參與者](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor)： 可以管理的 Vm，但不是 hello 它們互相連線的虛擬網路或存放裝置帳戶 toowhich。
- [傳統的虛擬機器參與者](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor)： 可以管理使用 hello 傳統部署模型，但不是 hello 虛擬網路或存放裝置帳戶 toowhich hello Vm 連接所建立的 Vm。
- [安全性管理員](../active-directory/role-based-access-built-in-roles.md#security-manager)：可以管理安全性元件、安全性原則及 VM。
- [DevTest Labs 使用者](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user)：可以檢視所有項目，並連接、啟動、重新啟動和關閉 VM。

請勿讓系統管理員共用帳戶和密碼，且請勿在多個使用者帳戶或服務上重複使用密碼，特別是用於社交媒體或其他非系統管理活動的密碼。 在理想情況下，您應該使用[Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)啟動您的 Vm 範本 tooset 安全的方式。 使用這種方法，您可以加強您的部署選項，並強制執行整個 hello 部署的安全性設定。

未利用諸如 RBAC 等功能來強制執行資料存取控制的組織，可能會對其使用者授與超過所需的權限。 不適當的使用者存取 toocertain 資料直接可能危及資料。

## <a name="vm-availability-and-network-access"></a>VM 可用性和網路存取

如果您的 VM 執行需要 toohave 高可用性的關鍵應用程式，我們強烈建議您使用多個 Vm。 更佳的可用性，建立至少兩個 Vm 在 hello[可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。

[Azure 負載平衡器](../load-balancer/load-balancer-overview.md)也需要負載平衡 Vm 屬於 toohello 相同可用性設定組。 如果這些 Vm 必須從 hello 網際網路存取，您必須設定[網際網路對向負載平衡器](../load-balancer/load-balancer-internet-overview.md)。

當 Vm 公開的 toohello 網際網路時，很重要，您[控制網路流量的網路安全性群組 (Nsg)](../virtual-network/virtual-networks-nsg.md)。 Nsg 可以套用的 toosubnets，因為您可以減少 hello Nsg 數目依子網路群組您的資源，然後將套用 Nsg toohello 子網路。 hello 目的是圖層的網路隔離，您可以藉由適當地設定 hello toocreate[網路安全性](../best-practices-network-security.md)在 Azure 中的功能。

您也可以使用具有遠端存取 tooa Azure 資訊安全中心 toocontrol hello 在 just-in-time (JIT) VM 存取功能特定的 VM，以及有效期間。

不強制 tooInternet 向 vm 的網路存取限制的組織暴露 toosecurity 風險，例如遠端桌面通訊協定 (RDP) 暴力攻擊。

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>強制執行加密以保護 VM 中待用資料的安全

[待用資料加密 (英文)](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 是達到資料隱私性、合規性及資料主權的必要步驟。 [Azure 磁碟加密](../security/azure-security-disk-encryption.md)可讓 IT 系統管理員 tooencrypt Windows 和 Linux IaaS VM 磁碟。 磁碟加密將 hello 業界標準 Windows BitLocker 功能和 hello Linux dm crypt 功能 tooprovide 磁碟區加密 hello OS 與 hello 資料磁碟。

您可以套用磁碟加密 toohelp 保護資料 toomeet 您組織的安全性和法規遵循需求。 您的組織應該考慮使用加密 toohelp 降低風險相關的 toounauthorized 資料存取。 我們也建議您在撰寫敏感性資料 toothem 之前先加密磁碟機。

為確定 tooencrypt 您參閱放在您的 Azure 儲存體帳戶中的 VM 資料磁碟區 tooprotect。 使用保護 hello 加密金鑰和秘密[Azure 金鑰保存庫](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/)。

不會強制進行資料加密的組織會多公開的 toodata 完整性問題。 比方說，未經授權或惡意使用者可能會竊取遭盜用的帳戶中的資料，或取得未經授權的存取 toodata ClearFormat 撰寫程式碼。 除了函式上這類風險、 toocomply 與業界規範，公司必須證明他們演練勤加注意，並使用正確的安全性控制 tooenhance 其資料的安全性。

toolearn 進一步了解磁碟加密，請參閱[Azure 磁碟加密用於 Windows 及 Linux IaaS Vm](azure-security-disk-encryption.md)。


## <a name="manage-your-vm-updates"></a>管理您的 VM 更新

Azure Vm，如同所有內部部署 Vm，因為預期的 toobe 受使用者管理，Azure 不會發送的 Windows 更新 toothem。 您，不過，是鼓勵 tooleave hello 自動 Windows Update 設定已啟用。 另一個選項是 toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx)或另一個 VM 或內部部署上的另一個適用的更新管理產品。 WSUS 和 Windows Update 都會讓 VM 保持最新狀態。 我們也建議您先使用 IaaS Vm 全部都已啟動 toodate 掃描產品 tooverify。

Azure 提供的內建影像會定期更新的 tooinclude hello round Windows 更新的最新。 不過，沒有 hello 映像，將會是目前在部署期間保證。 遵循公用版本可能會稍微落後 (最多幾個禮拜)。 檢查並安裝所有的 Windows 更新都應該是 hello 的每個部署的第一個步驟。 此量值時，尤其重要 tooapply 部署來自您或您自己的程式庫的映像。 根據預設，hello Azure Marketplace 中提供的映像會自動更新。

不強制執行軟體更新原則的組織都利用已知的先前已修正的弱點可能會多公開的 toothreats。 除了避免這類威脅，toocomply 業界規範，與公司必須證明他們演練勤加注意，並使用正確的安全性控制項 toohelp 確定其位於 hello 雲端中的工作負載 hello 安全性。

它是重要的軟體更新的傳統資料中心的最佳作法的 tooemphasize 和 Azure IaaS 有許多相似之處。 因此建議您評估您目前的軟體更新原則 tooinclude Vm。

## <a name="manage-your-vm-security-posture"></a>管理您的 VM 安全性狀態

不斷發展 E-security 威脅，並保護您的 Vm 需要豐富的監視功能，可以快速地偵測威脅，防止未經授權的存取 tooyour 資源、 觸發警示，並減少誤判。 這類工作負載的 hello 安全性狀況包含 hello VM，從更新管理 toosecure 網路存取的所有安全性層面。

toomonitor hello 安全性狀態的您[Windows](../security-center/security-center-virtual-machine.md)和[Linux Vm](../security-center/security-center-linux-virtual-machine.md)，使用[Azure 資訊安全中心](../security-center/security-center-intro.md)。 Azure 資訊安全中心，請利用下列功能的 hello 保護您的 Vm:

* 套用具有建議設定規則的 OS 安全性設定
* 找出並下載系統安全性和可能遺失的重大更新
* 部署端點反惡意程式碼保護建議
* 驗證磁碟加密
* 評估和修復弱點
* 偵測威脅

資訊安全中心可以主動監視威脅，並將可能的威脅公開於 [安全性警示] 之下。 相互關聯的威脅將彙總於稱為「安全性事件」的單一檢視中。

toounderstand 方式的資訊安全中心可協助您識別潛在的威脅，在 Azure 中，位於您虛擬機器中監看下列影片 hello:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

針對其 Vm 不強制執行強式安全性情勢組織保持潛在的嘗試不會察覺未經授權的使用者建立的 toocircumvent 安全性控制項。

## <a name="monitor-vm-performance"></a>監視 VM 效能

當 VM 程序比所應消耗更多的資源時，可能會產生資源不當使用的問題。 Vm 的效能問題可能會導致 tooservice 中斷狀況，這違反了可用性 hello 安全性原則。 基於這個理由，不命令式 toomonitor VM 存取只疑問，發生問題時，但也主動，對基準效能測量在正常操作。

藉由分析 [Azure 診斷記錄檔](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/)，您可以監視 VM 資源，並找出可能影響效能和可用性的潛在問題。 hello Azure 診斷延伸模組提供 windows Vm 上的監視和診斷功能。 您可以啟用這些功能包括 hello 副檔名一部分 hello [Azure Resource Manager 範本](../virtual-machines/windows/extensions-diagnostics-template.md)。

您也可以使用[Azure 監視器](../monitoring-and-diagnostics/monitoring-overview-metrics.md)toogain 掌握您的資源健全狀況。

不要監視 VM 效能的組織是無法 toodetermine 效能模式中的特定變更是否正常或不正常。 如果 hello VM 會耗用比一般更多資源，這類異常狀況可能表示從外部資源或遭盜用的處理程序在 hello VM 中執行的潛在攻擊。
