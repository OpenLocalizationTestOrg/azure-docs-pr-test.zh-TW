---
title: "aaaAzure 常見問題集 (FAQ) 的資訊安全中心 |Microsoft 文件"
description: "這個常見問題集回答「Azure 資訊安全中心」的相關問題。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Azure 資訊安全中心常見問題集 (FAQ)
此常見問題集回答有關 Azure 資訊安全中心，可協助您防止、 偵測，並回應 toothreats 增加的可見性與您的 Microsoft Azure 資源的 hello 安全性控制服務的問題。

> [!NOTE]
> 從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉](security-center-platform-migration.md)。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>
>

## <a name="general-questions"></a>一般問題
### <a name="what-is-azure-security-center"></a>什麼是 Azure 資訊安全中心？
Azure 資訊安全中心可協助您防止、 偵測，並回應 toothreats 增加的可見性與您的 Azure 資源的 hello 安全性控制。 它提供您訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

### <a name="how-do-i-get-azure-security-center"></a>我要如何取得 Azure 資訊安全中心？
Azure 資訊安全中心是透過 Microsoft Azure 訂用帳戶啟用，而且從 hello 存取[Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 ([Toohello 入口網站中登入](https://portal.azure.com)，選取**瀏覽**，然後捲動太**資訊安全中心**)。  

## <a name="billing"></a>計費
### <a name="how-does-billing-work-for-azure-security-center"></a>Azure 資訊安全中心如何計費？
資訊安全中心提供兩個層級：

hello**免費層**提供來自夥伴的安全性產品和服務與 hello Azure 資源，基本的安全性原則、 安全性建議事項，以及整合的安全性狀態的可視性。

hello**標準層**新增進階的威脅偵測功能，包括威脅情報，行為分析、 異常偵測，安全性事件和威脅 attribution 報表。 hello 標準層是免費的 hello 前 60 天。 我們應該選擇 toocontinue toouse hello 服務超過 60 天，自動啟動 toocharge hello 服務。  tooupgrade，選取定價層 hello[安全性原則](security-center-policies.md#set-security-policies)。 詳細資訊，請參閱 toolearn[資訊安全中心定價](security-center-pricing.md)。

## <a name="permissions"></a>權限
使用 azure 資訊安全中心[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)，這樣會提供[內建角色](../active-directory/role-based-access-built-in-roles.md)toousers、 群組和服務在 Azure 中的可獲指派。

資訊安全中心會評估 hello 和組態都資源 tooidentify 安全性問題的弱點。 資訊安全中心，因此您只看到資訊相關 tooa 資源時指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色。

請參閱[Azure 資訊安全中心中的權限](security-center-permissions.md)toolearn 深入了解角色與資訊安全中心所允許的動作。

## <a name="data-collection"></a>資料收集
資訊安全中心會收集從虛擬機器 tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。 當您第一次存取資訊安全中心時，訂用帳戶中的所有虛擬機器都會啟用資料收集。 您也可以啟用 hello 資訊安全中心原則中的資料收集。

### <a name="how-do-i-disable-data-collection"></a>我要如何停用資料收集？
如果您使用 hello Azure 安全性中心免費層，您可以停用在任何時間從虛擬機器的資料收集。 需要訂閱 hello 標準層上的資料收集。 您可以停用訂用帳戶在 hello 安全性原則中的資料收集。 ([登入 Azure 入口網站 toohello](https://portal.azure.com)，選取**瀏覽**，選取**資訊安全中心**，然後選取**原則**。)當您選取的訂用帳戶時的新刀鋒視窗會開啟，並提供您關閉 hello 選項 tooturn**資料收集**。

### <a name="how-do-i-enable-data-collection"></a>我要如何啟用資料收集？
您可以在 hello 安全性原則中您 Azure 訂用帳戶啟用資料收集。 tooenable 資料集合。 [登入 Azure 入口網站 toohello](https://portal.azure.com)，選取**瀏覽**，選取**資訊安全中心**，然後選取**原則**。 設定**資料收集**太**上**。

### <a name="what-happens-when-data-collection-is-enabled"></a>啟用資料收集時會發生什麼情況？
啟用資料收集時上現有的, 自動佈建 hello Microsoft Monitoring Agent，任何新支援的虛擬機器已部署的 hello 訂用帳戶中。

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Hello 監視代理程式的影響 hello 效能的我的伺服器嗎？
hello 代理程式會耗用系統資源表面的數量，並影響應該很小 hello 效能。 如需有關效能的影響和 hello 代理程式和擴充功能的詳細資訊，請參閱 hello[規劃及作業指南](security-center-planning-and-operations-guide.md#data-collection-and-storage)。

### <a name="where-is-my-data-stored"></a>我的資料會儲存在何處？
從這個代理程式收集的資料會儲存在與您的訂用帳戶相關聯的現有 Log Analytics 工作區或新的工作區中。 如需詳細資訊，請參閱[資料安全性](security-center-data-security.md)。

## <a name="using-azure-security-center"></a>使用 Azure 資訊安全中心
### <a name="what-is-a-security-policy"></a>什麼是安全性原則？
安全性原則定義中指定的 hello 資源的建議使用的控制項 hello 組訂用帳戶。 在 Azure 資訊安全中心，您可以定義原則 tooyour 公司的安全性需求與 hello 類型的應用程式或每個訂用帳戶中的 hello 資料的機密性，根據您 Azure 訂用帳戶。

啟用 Azure 資訊安全中心磁碟機的安全性建議和監視中的 hello 安全性原則。 toolearn 更多有關安全性原則，請參閱[Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)。

### <a name="who-can-modify-a-security-policy"></a>誰可以修改安全性原則？
toomodify 安全性原則，您必須是安全性系統管理員或擁有者或參與者該訂用帳戶。

如何 tooconfigure 安全性原則，請參閱的 toolearn [Azure 資訊安全中心中設定安全性原則](security-center-policies.md)。

### <a name="what-is-a-security-recommendation"></a>什麼是安全性建議？
Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當發現潛在的安全性弱點時，就會產生相關建議。 hello 建議指南您透過設定 hello 的 hello 程序所需的控制項。 範例包括：

* 佈建的反惡意程式碼 toohelp 識別及移除惡意軟體
* 設定[網路安全性群組](../virtual-network/virtual-networks-nsg.md)和規則 toocontrol 流量 toovirtual 機器
* 佈建的 web 應用程式防火牆 toohelp 防禦攻擊目標 web 應用程式
* 部署遺漏的系統更新
* 定址 OS 組態不符合 hello 建議基準

這裡只會顯示 [安全性原則] 中已啟用的建議。

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>如何查看 hello 目前的安全性狀態的 我的 Azure 資源？
hello**安全性中心概觀**刀鋒視窗中顯示 hello 切分運算、 網路功能、 存放裝置 （& s） 資料和應用程式環境的整體安全性狀態。 每個資源類型都有一個指標，顯示是否已識別出任何潛在的安全性弱點。 按一下每個磚會顯示一份由資訊安全中心，以及您的訂用帳戶中的 hello 資源的清查的安全性問題。

### <a name="what-triggers-a-security-alert"></a>什麼會觸發安全性警示？
Azure 資訊安全中心會自動收集、 分析，並 fuses 記錄資料從 Azure 資源、 hello 網路和反惡意程式碼和防火牆等協力廠商解決方案。 偵測到威脅時，會建立安全性警示。 偵測範例包括：

* 已受到危害的虛擬機器與已知的惡意 IP 位址進行通訊
* 使用 Windows 錯誤報告偵測到進階的惡意程式碼
* 針對虛擬機器的暴力密碼破解攻擊
* 來自已整合的合作夥伴安全性解決方案 (例如「反惡意程式碼」或「Web 應用程式防火牆」) 的安全性警示

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Hello 威脅偵測到並由 Microsoft Security Response Center 與 Azure 資訊安全中心警示之間的差異為何？
hello Microsoft Security Response Center (MSRC) 執行選取的安全性監視的 hello Azure 網路和基礎結構，並接收來自第三方的威脅情報和濫用抱怨。 MSRC 知道已由非法或未經授權的合作對象存取客戶的資料，或 Azure 的 hello 客戶的使用不符合 hello 條款，可接受使用時，安全性事件管理員通知 hello 客戶。 指定在 Azure 資訊安全中心或 hello Azure 訂用帳戶擁有者，如果未指定安全性連絡人連絡人傳送電子郵件 toohello 安全性通常會通知發生。

資訊安全中心是一項 Azure 服務持續監控 hello 客戶的 Azure 環境，以及適用於分析 tooautomatically 偵測廣泛的潛在惡意活動。 這些偵測當成 hello 資訊安全中心儀表板中的安全性警示。

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Azure 資訊安全中心會監視哪些 Azure 資源？
Azure 資訊安全中心會監視下列 Azure 資源的 hello:

* 虛擬機器 (VM) (包括 [雲端服務](../cloud-services/cloud-services-choose-me.md))
* Azure 虛擬網路
* Azure SQL 服務
* Azure 儲存體帳戶
* Azure Web Apps (在 [App Service 環境](../app-service/app-service-app-service-environments-readme.md)中)
* 與您的 Azure 訂用帳戶整合的合作夥伴解決方案，例如 VM 和 [App Service 環境](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>虛擬機器
### <a name="what-types-of-virtual-machines-are-supported"></a>支援哪些類型的虛擬機器？
監視和建議事項皆可使用這兩個 hello 所建立的虛擬機器 (Vm)[傳統和資源管理員部署模型](../azure-classic-rm.md)。

如需支援之平台的清單，請參閱 [Azure 資訊安全中心支援的平台](security-center-os-coverage.md)。

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>為什麼 Azure 資訊安全中心無法辨識在我的 Azure VM 上執行的 hello 反惡意程式碼解決方案？
Azure 資訊安全中心能辨識透過 Azure 擴充功能安裝的反惡意程式碼軟體。 例如，資訊安全中心不是預先安裝在您提供的映像，或如果您使用您自己的處理序 （例如設定管理系統） 的虛擬機器上安裝反惡意程式碼的能 toodetect 反。

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>為什麼我收到 hello 訊息 「 缺少掃描資料 」 對我的 VM？
當沒有 VM 的掃瞄資料時會顯示此訊息。 已啟用 Azure 資訊安全中心中的資料收集後可能需要掃描資料 toopopulate 一些時間 （少於一小時）。 Hello 初始母體擴展之後的掃描資料，因為沒有掃描資料的完全或沒有最新的掃描資料，可能會收到這則訊息。 掃描不會填入處於停止狀態之 VM 的資料。 如果掃描資料有未擴展最近 （根據 hello hello Windows 代理程式，其具有預設值是 30 天的保留原則），可能也會出現這則訊息。

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>為什麼我會收到 hello 訊息 「 VM 代理程式是遺漏？ 」
hello VM 代理程式必須安裝在 Vm tooenable 資料收集。 預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。 如需如何 tooinstall hello 其他 Vm 上的 VM 代理程式資訊，請參閱 hello 部落格文章[VM 代理程式和擴充功能](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)。
