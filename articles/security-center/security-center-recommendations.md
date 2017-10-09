---
title: "在 Azure 資訊安全中心 aaaManaging 安全性建議 |Microsoft 文件"
description: "本文件將逐步引導您了解「Azure 資訊安全中心」的建議如何協助您保護 Azure 資源及遵守安全性原則。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>管理 Azure 資訊安全中心的安全性建議
本文件將引導您完成要如何在 Azure 資訊安全中心 toohelp toouse 建議您保護您的 Azure 資源。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  本文件不是一份逐步解說指南。
>
>

## <a name="what-are-security-recommendations"></a>有哪些安全性建議？
資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性弱點時，它會建立建議。 hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。

## <a name="implementing-security-recommendations"></a>實作安全性建議
### <a name="set-recommendations"></a>設定建議
在 [在 Azure 資訊安全中心設定安全性原則](security-center-policies.md)中，您將了解如何：

* 設定安全性原則。
* 開啟資料收集。
* 選擇哪些建議 toosee，做為您的安全性原則的一部分。

目前的原則建議是以系統更新、基準規則、反惡意程式碼程式、子網路與網路介面上的 [網路安全性群組](../virtual-network/virtual-networks-nsg.md) 、SQL Database 稽核、SQL Database 透明資料加密及 Web 應用程式防火牆為中心。  [設定安全性原則](security-center-policies.md) 提供每個建議選項的描述。

### <a name="monitor-recommendations"></a>監視建議
設定安全性原則之後, 的資訊安全中心會分析資源 tooidentify 的潛在弱點的 hello 安全性狀態。 hello**建議**磚 hello**資訊安全中心**刀鋒視窗可讓您知道的資訊安全中心所識別的建議 hello 總數。

![建議圖格][1]

每個建議的 toosee hello 詳細資料：

選取 hello**建議磚**上 hello**資訊安全中心**刀鋒視窗。 hello**建議**刀鋒視窗隨即開啟。

hello 建議會出現以資料表格式，其中每一行代表一個特定的建議。 hello 這個資料表的資料行如下：

* **描述**: hello 建議和所需完成 tooaddress toobe 說明它。
* **資源**： 列出這項建議適用於 hello 資源 toowhich。
* **狀態**： 描述 hello hello 建議事項的目前狀態：
  * **開啟**: hello 建議尚未尚未處理。
  * **正在進行中**: hello 建議目前正在套用的 toohello 資源，並由您不需要任何動作。
  * **解析**: hello 建議已經完成 （在此情況下，hello 列會變成灰色）。
* **嚴重性**： 描述該特定建議事項的 hello 嚴重性：
  * **高**：某個有意義的資源 (例如應用程式、VM 或網路安全性群組) 有弱點存在，並且需要注意。
  * **媒體**: 弱點存在，而且非關鍵的或額外的步驟是必要的 tooeliminate 它或 toocomplete 處理程序。
  * **低**：應該處理但不需要立即注意的弱點存在。 (根據預設，不呈現不足的建議，但是如果您想 toosee，您可以篩選低建議它們。)

使用 hello 表當做參考 toohelp 您了解 hello 提供建議和每個用途如果您將其套用。

> [!NOTE]
> 您會想 toounderstand hello[傳統和資源管理員部署模型](../azure-classic-rm.md)Azure 資源。
>
>

| 建議 | 說明 |
| --- | --- |
| [啟用訂用帳戶的資料收集](security-center-enable-data-collection.md) |建議您在您的訂用帳戶中開啟 hello 安全性原則中的每個訂用帳戶及所有虛擬機器 (Vm) 的資料收集。 |
| [修復 OS 弱點](security-center-remediate-os-vulnerabilities.md) |建議您配合 hello 建議設定規則，例如您作業系統的組態，不允許儲存密碼 toobe。 |
| [套用系統更新](security-center-apply-system-updates.md) |建議您部署遺失系統的安全性和重大更新 tooVMs。 |
| [套用 Just-in-Time 網路存取控制](security-center-just-in-time.md) | 建議您套用 Just-in-Time 虛擬機器存取。 在時間 」 功能中的 hello 已預覽並可使用 hello 標準層的資訊安全中心。 請參閱[定價](security-center-pricing.md)toolearn 詳細的資訊安全中心的定價層。 |
| [在系統更新之後重新開機](security-center-apply-system-updates.md#reboot-after-system-updates) |建議您重新啟動 VM toocomplete hello 程序套用系統更新。 |
| [新增 Web 應用程式防火牆](security-center-add-web-application-firewall.md) |建議您為 Web 端點部署「Web 應用程式防火牆」(WAF)。 系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。 </br>資訊安全中心建議您佈建 WAF toohelp 防禦目標 web 應用程式的 App Service 環境和虛擬機器上的攻擊。 App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。 toolearn 深入了解 ASE，請參閱 hello[應用程式服務環境的文件](../app-service/app-service-app-service-environments-readme.md)。</br>您可以藉由新增這些應用程式 tooyour 現有 WAF 部署保護的資訊安全中心中的多個 web 應用程式。 |
| [完成應用程式保護](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello 的 WAF，流量必須路由的 toohello WAF 應用裝置。 遵循這個建議完成 hello 必要的設定變更。 |
| [新增新一代防火牆](security-center-add-next-generation-firewall.md) |建議您將加入 下一步產生防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護。 |
| [僅透過 NGFW 路由傳送流量](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |建議您設定網路安全性群組 (NSG) 規則強制傳入的流量 tooyour 透過您 NGFW VM。 |
| [安裝端點保護](security-center-install-endpoint-protection.md) |建議您佈建反惡意程式碼程式 tooVMs (僅限 Windows Vm)。 |
| [解決端點保護健全狀況警示](security-center-resolve-endpoint-protection-health-alerts.md) |建議您先解決端點保護失敗。 |
| [啟用子網路/虛擬機器上的網路安全性群組](security-center-enable-network-security-groups.md) |建議您在子網路或 VM 上啟用 NSG。 |
| [透過網際網路面向端點限制存取](security-center-restrict-access-through-internet-facing-endpoints.md) |建議您為 NSG 設定輸入流量規則。 |
| [在 SQL Server 上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-servers.md) |建議您針對 Azure SQL Server 開啟稽核與威脅偵測。 (僅限 Azure SQL 服務。 不包含在虛擬機器上執行的 SQ。) |
| [在 SQL 資料庫上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-databases.md) |建議您針對 Azure SQL Database 開啟稽核與威脅偵測。 (僅限 Azure SQL 服務。 不包含在虛擬機器上執行的 SQ。) |
| [在 SQL 資料庫上啟用透明資料加密](security-center-enable-transparent-data-encryption.md) |建議您針對 SQL Database 啟用加密功能。 (僅限 Azure SQL 服務。) |
| [啟用 VM 代理程式](security-center-enable-vm-agent.md) |可讓您 toosee Vm 需要 hello VM 代理程式。 hello VM 代理程式必須安裝在 Vm tooprovision 修補程式掃描，基準和反惡意程式碼程式掃描。 預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。 hello 文章[VM 代理程式和延伸模組 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。 |
| [套用磁碟加密](security-center-apply-disk-encryption.md) |建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。 加密是建議使用 hello OS 和 VM 上的資料磁碟區。 |
| [提供安全性連絡人詳細資料](security-center-provide-security-contact-details.md) |建議您提供每個訂用帳戶安全性連絡人資訊。 連絡人資訊為電子郵件地址和電話號碼。 hello 資訊是使用的 toocontact 您如果我們安全性小組發現您的資源會隨即受到危害。 |
| [更新作業系統版本](security-center-update-os-version.md) |建議您雲端服務 toohello 最新版本可用更新 hello 作業系統 (OS) 版本，您的作業系統系列。  toolearn 有關雲端服務的詳細資訊，請參閱 「 hello[雲端服務概觀](../cloud-services/cloud-services-choose-me.md)。 |
| [未安裝弱點評估](security-center-vulnerability-assessment-recommendations.md) |建議在 VM 上安裝弱點評估解決方案。 |
| [修復弱點](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |可讓您 toosee 系統和應用程式的弱點可能會偵測到的 hello 的弱點可能會評估解決方案安裝在您的 VM 上。 |
| [為 Azure 儲存體帳戶啟用加密](security-center-enable-encryption-for-storage-account.md) | 建議您為待用資料啟用「Azure 儲存體服務加密」。 儲存體服務加密 (SSE) 中的運作方式會寫入 tooAzure 儲存和擷取之前解密時，加密 hello 資料。 SSE 目前僅適用於 hello Azure Blob 服務可用於區塊 blob，分頁 blob，並附加 blob。 詳細資訊，請參閱 toolearn[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。</br>只有在 Resource Manager 儲存體帳戶上才支援 SSE。 |

您可以篩選並關閉建議。

1. 選取**篩選**上 hello**建議**刀鋒視窗。 hello**篩選**刀鋒視窗會開啟，並選取您想 toosee hello 嚴重性和狀態值。

    ![篩選建議][2]
2. 如果您確定建議不適用，您可以關閉 hello 建議，然後將其篩選出您的檢視。 有兩種方式 toodismiss 建議。 其中一種方式是 tooright 按一下項目，然後選取**解除**。 其他 hello toohover 在某個項目，按一下 hello 三個點，會出現 toohello 權限，然後選取**解除**。 您可以按一下 [篩選]，然後選取 [已解除]，以檢視已解除的建議。

    ![解除建議][3]

### <a name="apply-recommendations"></a>套用建議
檢視所有建議之後，請決定應該先套用哪一個建議。 我們建議您使用 hello 嚴重性 hello 主要參數 tooevaluate 應該先套用哪個建議事項。

在上述建議的 hello 資料表中，選取建議，然後逐步解說的範例為 tooapply 建議。

## <a name="next-steps"></a>後續步驟
在本文件中，您提供了導入了的 toosecurity 建議資訊安全中心。 toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
