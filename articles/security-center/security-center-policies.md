---
title: "在 Azure 資訊安全中心 aaaSet 安全性原則 |Microsoft 文件"
description: "這份文件可協助您在 Azure 資訊安全中心 tooconfigure 安全性原則。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>在 Azure 資訊安全中心設定安全性原則
這份文件可協助您 tooconfigure 安全性原則資訊安全中心透過帶領您完成 hello 必要步驟 tooperform 這項工作。

>[!NOTE] 
>從開始早期年 6 月 2017年，資訊安全中心會使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>

## <a name="what-are-security-policies"></a>什麼是安全性原則？
安全性原則定義中指定的 hello 資源的建議使用的控制項 hello 組訂用帳戶。 資訊安全中心，您可以定義原則 tooyour 公司安全性需求與 hello 的應用程式的類型或大小寫的每個訂用帳戶中的 hello 資料，根據您 Azure 訂用帳戶。

例如，用於開發或測試的資源與用於生產應用程式的資源，兩者的安全性需求可能不同。 同樣地，使用個人識別資訊等規範資料的應用程式可能會需要較高層級的安全性。 已啟用 Azure 資訊安全中心磁碟機的安全性建議和監視 toohelp 您找出潛在的漏洞，並減輕威脅中的安全性原則。 讀取[Azure 安全性 Center 計劃和 Operations guide 》](security-center-planning-and-operations-guide.md)如何 toodetermine hello 選項的詳細資訊是適合您。

## <a name="set-security-policies"></a>設定安全性原則
您可以為每個訂用帳戶設定安全性原則。 toomodify 安全性原則，您必須是擁有者或參與者的訂用帳戶。 登入 toohello Azure 入口網站，並遵循 hello 定址 tooconfigure 安全性原則資訊安全中心的步驟：

1. 按一下 hello**原則**磚 hello 資訊安全中心儀表板中。
2. 在 hello 安全性原則 刀鋒視窗開啟，選取您想要 tooenable hello 安全性原則的 hello 訂用帳戶。

    ![定義原則](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. hello**安全性原則**hello 選取訂用帳戶 刀鋒視窗會開啟與一組選項。 在這個刀鋒視窗中的 hello 可用選項如下：

   * **防止原則**： 使用此選項 tooconfigure 原則，每個訂閱。  
   * **電子郵件通知**: hello 每日第一個警示並對高嚴重性警示上使用此選項 tooconfigure 傳送電子郵件通知。 電子郵件喜好設定只能針對訂用帳戶原則進行設定。 讀取[提供安全性 Azure 資訊安全中心中的連絡人詳細資料](security-center-provide-security-contact-details.md)如需有關如何 tooconfigure 電子郵件通知。
   * **定價層**： 使用定價層級選擇此選項 tooupgrade hello。 請參閱[資訊安全中心定價](security-center-pricing.md)toolearn 更多關於定價選項。
4. 確定 [從虛擬機器收集資料] 選項為 [開啟]。 這個選項會啟用自動記錄檔集合的現有和新的資源使用 hello Microsoft Monitoring Agent – 這是的 hello hello Operations Management Suite，記錄分析服務使用相同的代理程式。 從這個代理程式所收集的資料會儲存在您的 Azure 訂用帳戶相關聯的現有記錄分析 workspace(s) 或新 workspace(s)，納入帳戶 hello 地理位置的 hello VM。

5. 在 hello**安全性原則**刀鋒視窗中，按一下 **防止原則**toosee hello 可用的選項。 按一下**上**tooenable hello 安全性建議與相關的此訂用帳戶。

    ![選取 hello 安全性原則](./media/security-center-policies/security-center-policies-fig7.png)

使用下表做為參考 toounderstand hello 每個選項：

| 原則 | 當狀態為開啟時 |
| --- | --- |
| 系統更新 |從 Windows Update 或 Windows Server Update Services (WSUS) 擷取每天可用的安全性和重大更新清單。 hello 擷取的清單取決於 hello 服務，已針對該虛擬機器，並建議您套用 hello 遺失的更新。 適用於 Linux 系統 hello 原則會使用 hello 提供 distro 的封裝管理系統 toodetermine 封裝擁有可用的更新。 它也會檢查來自 [Azure 雲端服務](../cloud-services/cloud-services-how-to-configure.md) 虛擬機器的安全性和重大更新。 |
| 作業系統弱點 |分析作業系統設定每日 toodetermine 問題而無法進行 hello 虛擬機器很容易遭受 tooattack。 hello 原則也建議組態變更 tooaddress 這些弱點。 請參閱 hello[建議的基準清單](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)的 hello 受監視的特定組態的詳細資訊。 (目前，未完全支援 Windows Server 2016)。 |
| 端點保護 |建議針對所有 Windows 虛擬機器 toohelp 識別和移除病毒、 間諜軟體及其他惡意軟體佈建 endpoint protection toobe。 |
| 磁碟加密 |啟用磁碟加密在靜止所有虛擬機器 tooenhance 資料保護的建議。 |
| 網路安全性群組 |建議您使用[網路安全性群組](../virtual-network/virtual-networks-nsg.md)是設定的 toocontrol 傳入和傳出流量 tooVMs 具有公用端點。 除非另有指定，否則所有虛擬機器網路介面都會繼承為子網路設定的網路安全性群組。 此外 toochecking 已設定網路安全性群組，此原則，評估連入的安全性規則 tooidentify 規則以允許連入流量。 |
| Web 應用程式防火牆 |建議您，web 應用程式防火牆佈建虛擬機器上時 hello 下列其中一項成立： </br></br>[執行個體層級公用 IP](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) 會使用與 hello hello 相關聯的網路安全性群組的連入的安全性規則所設定的 tooallow 存取 tooport 80/443。</br></br>使用負載平衡 IP hello 關聯的負載平衡和傳入的網路位址轉譯 (NAT) 規則設定的 tooallow 存取 tooport 80/443。 如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](../load-balancer/load-balancer-arm.md)。 |
| 新一代防火牆 |提供超越 Azure 內建網路安全性群組的網路保護。 資訊安全中心會探索的部署的下一個層代防火牆建議以及啟用 tooprovision 虛擬應用裝置。 |
| SQL 稽核與威脅偵測 |建議的稽核存取 tooAzure 資料庫啟用相容性以及進階威脅的偵測，來進行調查。 |
| SQL 加密 |建議為您的 Azure SQL Database、關聯的備份及交易記錄檔啟用待用期加密。 您的資料即使遭到入侵，也無法被讀取。 |
| 弱點評估 |建議在 VM 上安裝弱點評估解決方案。 |
| 儲存體加密 |這項功能目前可用於 Azure Blob 和檔案。 啟用儲存體服務加密之後，只會加密新的資料，而此儲存體帳戶中任何現有的檔案都會保持未加密狀態。 |
| JIT 網路存取 |在啟用時，資訊安全中心鎖定輸入的流量 tooyour Azure Vm 建立 NSG 規則。 您選取 hello 連接埠上 hello VM toowhich 輸入的流量應該要鎖定。 如需詳細資訊，請參閱[使用 Just-In-Time 管理虛擬機器存取](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)。 |

設定所有選項之後，請按一下**確定**在 hello**安全性原則**刀鋒視窗，其中有 hello 建議，然後按一下**儲存**在 hello**安全性原則**刀鋒視窗，其中具有 hello 初始設定。

> [!NOTE]
> hello 定價層是仍適用於 hello 資源群組層級。 如需詳細資訊，請造訪 hello[定價](https://azure.microsoft.com/pricing/details/security-center/)頁面。
>
>

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 tooconfigure Azure 資訊安全中心中的安全性原則。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)。 深入了解如何 tooplan 並了解 hello 設計考量 tooadopt Azure 資訊安全中心。
* [Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)。 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。 深入了解如何 toomanage 和回應 toosecurity 警示。
* [使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md)。 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)。 尋找有關使用 hello 服務常見問題。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。 尋找有關 Azure 安全性與相容性的部落格文章。
