---
title: "aaaAzure 安全性 Center 平台移轉 |Microsoft 文件"
description: "本文件說明一些 Azure 資訊安全中心資料的變更 toohello 方式收集。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Azure 資訊安全中心平台移轉

從開始早期年 6 月 2017年，Azure 資訊安全中心中推出收集及儲存資料的變更 toohello 方式安全性很重要。  這些變更解除鎖定新功能，例如 hello 能力 tooeasily 搜尋安全性資料，並進一步對齊其他 Azure 管理和監視 windows 服務。

> [!NOTE]
> hello 平台移轉應該不會影響您實際執行的資源，並不不需要從您的側邊採取任何動作。


## <a name="whats-happening-during-this-platform-migration"></a>在此平台移轉期間發生什麼事？

先前的資訊安全中心使用 hello Azure Monitoring Agent toocollect 安全性資料從您的 Vm。 這包括安全性組態，也就是使用的 tooidentify 弱點和安全性事件，也就是使用的 toodetect 威脅的相關資訊。 此資料會儲存於 Azure 中您的儲存體帳戶。

這是使用相同的代理程式的 hello Operations Management Suite，記錄分析服務的 hello 接下來，資訊安全中心會使用 Microsoft Monitoring Agent – hello。 從這個代理程式收集的資料會儲存在現有*記錄分析*[工作區](../log-analytics/log-analytics-manage-access.md)納入的 hello VM 帳戶 hello 地理位置與您 Azure 訂用帳戶或新 workspace(s)，相關聯.

## <a name="agent"></a>代理程式

Hello 轉換的一部分，hello Microsoft Monitoring Agent (如[Windows](../log-analytics/log-analytics-windows-agents.md)或[Linux](../log-analytics/log-analytics-linux-agents.md)) 從中資料目前未收集所有的 Azure Vm 上已安裝。  如果 VM 已經有 Microsoft Monitoring Agent 安裝，hello hello 資訊安全中心運用 hello 目前安裝代理程式。

一段時間 （通常幾天），這兩個代理程式會執行並存 tooensure 照常平順地轉換資料。 這可讓 Microsoft hello 新的資料管線的 toovalidate 可運作之前停止使用 hello 目前的管線。 一次驗證，hello Azure Monitoring Agent 會移除您的 Vm。 您不需要執行任何工作。 所有客戶都已移轉後，系統會以電子郵件通知您。
 
不建議您手動解除 hello Azure Monitoring Agent 安裝 hello 移轉期間因為可能會造成安全性資料中的間距。 如果您需要進一步協助，請洽詢 [Microsoft 客戶服務與支援中心](https://support.microsoft.com/contactus/)。 

Microsoft Monitoring Agent 的 Windows hello 需要使用 TCP 連接埠 443，讀取[Azure 安全性中心疑難排解指南](security-center-troubleshooting-guide.md)如需詳細資訊。


> [!NOTE] 
> Hello Microsoft Monitoring Agent 可能會由其他 Azure 管理和監視服務，hello 代理程式將不會自動解除安裝，因為當您關閉資訊安全中心中的資料收集。 不過，您可以手動解除安裝 hello 代理程式所需。

## <a name="workspace"></a>工作區

先前所述，從 Microsoft Monitoring Agent （代表 Security Center) 會儲存在現有記錄分析的 hello 收集的資料與您 Azure 訂用帳戶或新 workspace(s)，納入帳戶 hello workspace(s) 相關聯hello VM 的地理位置。

在 hello Azure 入口網站，您可以瀏覽 toosee 記錄分析工作區，包括任何資訊安全中心所建立的清單。 將會針對新的工作區建立相關的資源群組。 兩者都會遵循此命名慣例：

- 工作區：*DefaultWorkspace-[subscription-ID]-[geo]*
- 資源群組：*DefaultResouceGroup-[geo]* 
 
若為資訊安全中心所建立的工作區，資料會保留 30 天。 保留現有的工作區，根據 hello 工作區的定價層。

> [!NOTE]
> 資訊安全中心先前收集的資料會保留在儲存體帳戶中。 Hello 移轉完成之後，您可以刪除這些儲存體帳戶。

### <a name="oms-security-solution"></a>OMS 安全性解決方案 

對於未安裝 OMS 安全性解決方案的現有客戶，Microsoft 會安裝在其工作區上，但是僅以 Azure VM 為目標。 請勿解除安裝此解決方案，因為如果從 OMS 管理主控台進行此動作，就沒有任何自動補救方式。


## <a name="other-updates"></a>其他更新

搭配 hello 平台移轉，我們會推出一些額外的次要更新：

- 將支援其他作業系統版本。 請參閱 hello 清單[這裡](security-center-faq.md#virtual-machines)。
- 作業系統弱點的 hello 清單將會展開。 請參閱 hello 清單[這裡](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)。
- [價格](https://azure.microsoft.com/pricing/details/security-center/)將會按小時 (先前按日) 計算，這可讓某些客戶節省成本。
- 將所需資料收集，並自動啟用的客戶 hello 標準定價層。
- Azure 資訊安全中心將開始探索未透過 Azure 擴充功能部署的反惡意程式碼解決方案。 將會首先探索 Symantec Endpoint Protection 和 Defender for Windows 2016。
- 洩防護原則和通知只可在 hello 設定*訂用帳戶*層級，但定價仍然可以設定在 hello*資源群組*層級

