---
title: "管理套件的安全性和稽核解決方案資料安全性 aaaOperations |Microsoft 文件"
description: "本文件說明如何在 Operations Management Suite 安全性和稽核解決方案中管理和保護資料。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Operations Management Suite 安全性和稽核解決方案資料安全性
toohelp 客戶防止、 偵測及回應 toothreats， [Operations Management Suite (OMS) 的安全性和稽核解決方案](operations-management-suite-overview.md)會收集並處理資源的相關資料，其中包括：

* 安全性事件記錄檔
* Windows 事件追蹤 (ETW) 事件
* AppLocker 稽核事件
* Windows 防火牆記錄檔
* Advanced Threat Analytics 事件
* 基準評估結果
* 反惡意程式碼評估結果
* 更新/修補評估結果
* 在 hello 代理程式上明確啟用 Syslog 資料流

我們不提供這項資料的強式承諾 tooprotect hello 隱私與安全性。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。
本文說明如何在 OMS 安全性和稽核解決方案中管理和保護資料。

## <a name="data-sources"></a>資料來源
OMS 安全性和稽核解決方案分析 hello OMS 代理程式已安裝虛擬機器和實體電腦的資料。 OMS 安全性和稽核解決方案可以收集有關安全性事件的組態資訊，例如 Windows 事件、稽核記錄檔、IIS 記錄檔和 syslog 訊息。 這類資料的範例包括︰作業系統類型和版本、執行中程序、電腦名稱、IP 位址、已登入的使用者和租用戶識別碼。  

## <a name="data-protection"></a>資料保護
**資料隔離**: hello 服務在每個元件上，資料以邏輯方式分開。 每個組織加上標記的所有資料。 這項標記作業在整個 hello 資料生命週期持續發生，它會強制執行各種層級的 hello 服務。 

**資料存取**: tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集或由服務分析的資訊。 我們將遵守 toohello [Microsoft Online Services 條款](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)和[隱私權聲明](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)，Microsoft 將不使用客戶資料，或衍生自它的資訊任何廣告或類似處理的狀態商業用途。 tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集或由服務分析的資訊。 我們只會為您的 Azure 服務，包括用途與提供這些服務相容的所需 tooprovide 使用客戶資料。 您會保留所有權限 tooyour 自己的資料。

**資料使用**： 使用模式，Microsoft 威脅情報看到跨多個租用戶 tooenhance 我們預防和偵測功能之後，我們這樣中所述的 hello 隱私權承諾根據我們[隱私權陳述式](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)。

> [!NOTE]
> Hello 工作區建立期間，也就是在 hello 初始 OMS 安全性和稽核設定程序在 hello OMS 工作區層級，設定資料的位置。
> 
> 

## <a name="see-also"></a>另請參閱
在本文件中，您已了解如何在 OMS 中管理和保護資料。 toolearn 深入了解 OMS 安全性和稽核解決方案，請參閱：

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

