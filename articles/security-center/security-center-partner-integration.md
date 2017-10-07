---
title: "aaaPartner 整合 Azure 資訊安全中心 |Microsoft 文件"
description: "深入了解 Azure 資訊安全中心如何與夥伴 tooenhance 整合您的 Azure 資源的整體安全性。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Azure 資訊安全中心中的夥伴整合

在本文中，我們說明如何與夥伴 toohelp 整合 Azure 資訊安全中心增強整體安全性。 資訊安全中心提供了整合式的體驗，在 Azure 中，並利用 hello Azure Marketplace 夥伴憑證和計費。

> [!NOTE] 
> 為準，年 6 月 2017年資訊安全中心會使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。 如需詳細資訊，請參閱 [Azure 資訊安全中心平台移轉](security-center-platform-migration.md)。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>為什麼要從資訊安全中心部署夥伴解決方案

有四個主要原因 tooleverage 夥伴資訊安全中心整合：

- **部署方式簡單**。 下列 hello 資訊安全中心建議部署協力廠商方案就能更輕鬆。 使用預設的安裝程式和網路拓撲，可以全面自動化 hello 部署程序。 或者，客戶可以選擇半自動的選項以取得更多彈性和自訂。
- **整合偵測**。 來自夥伴解決方案的安全性事件會自動收集、彙總以及顯示為資訊安全中心警示和事件的一部分。 這些事件也被 fused 進階威脅偵測功能，其他來源 tooprovide 的偵測結果。
- **統一的健康情況監視與管理**。 客戶可以使用整合式健全狀況事件 toomonitor 所有協力廠商解決方案一目了然。 使用，讓您輕鬆存取 tooadvanced 安裝程式使用 hello 協力廠商解決方案的基本管理。
- **匯出 tooSIEM**。 客戶可以匯出所有的資訊安全中心，並且夥伴警示通用事件格式 (CEF) tooon 內部部署安全性資訊和事件管理 (SIEM) 系統使用 Azure 記錄檔整合 （預覽）。


## <a name="partners-that-integrate-with-security-center"></a>與資訊安全中心整合的夥伴

資訊安全中心目前與下列這些解決方案整合︰

- Endpoint protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html)、Symantec 以及 [適用於 Azure 雲端服務和虛擬機器的 Microsoft 反惡意程式碼軟體](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Web 應用程式防火牆 ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall)、[F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html)、[Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF)、[Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets)，以及 [Azure 應用程式閘道](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- 新一代防火牆 ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/)、[Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/)、[Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) 和 [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- 弱點評估 ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

經過一段時間，將展開 hello 在這些分類中中的夥伴數目的資訊安全中心，並將其加入新的類別目錄中。 

## <a name="deploy-a-partner-solution"></a>部署夥伴解決方案

根據 hello Azure 環境的 hello 安全性原則所定義的設定資訊安全中心可能會建議您部署協力廠商解決方案。 hello 資訊安全中心建議會引導您完成選取並安裝協力廠商解決方案 hello 程序。 hello 整體部署經驗可能有所不同，hello 的方案和您使用協力廠商的型別。 如需詳細資訊，請參閱下列文章 hello:

- [安裝端點保護](security-center-install-endpoint-protection.md)
- [新增 Web 應用程式防火牆](security-center-add-web-application-firewall.md)
- [新增新一代防火牆](security-center-add-next-generation-firewall.md)
- [未安裝弱點評估](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>管理夥伴解決方案

部署之後，tooview 有關 hello hello 方案的健全狀況與資訊的基本管理工作，對 hello**資訊安全中心**刀鋒視窗中，選取 hello**合作夥伴解決方案**選項。 如需管理資訊安全中心中合作夥伴解決方案的相關資訊，請參閱[透過 Azure 資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。

![夥伴整合](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Symantec endpoint protection 支援是有限的 toodiscovery。 無法使用健康情況警示。
>

## <a name="see-also"></a>另請參閱

在本文中，您學會如何 toointegrate 合作夥伴 Azure 資訊安全中心中的解決方案。 toolearn 有關資訊安全中心的詳細資訊，請參閱下列文章 hello:

* [資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)
* [管理及回應 toosecurity 警示資訊安全中心](security-center-managing-and-responding-alerts.md)
* [資訊安全中心不同類型的安全性警示](security-center-alerts-type.md)
* [資訊安全中心的安全性健康情況監視](security-center-monitoring.md)。 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [使用資訊安全中心監視夥伴解決方案](security-center-partner-solutions.md)。 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
* [Azure 資訊安全中心常見問題](security-center-faq.md)。 取得使用 hello 服務的相關常見問題的解答 toofrequently。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。 尋找有關 Azure 安全性與相容性的部落格文章。
