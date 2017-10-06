---
title: "aaaMonitoring 及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案 |Microsoft 文件"
description: "這份文件可協助您 toouse hello 威脅情報選項可以在 OMS 安全性和稽核 toomonitor，以及回應 toosecurity 警示。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a>監視及回應 toosecurity Operations Management Suite 安全性和稽核 」 解決方案中的警示
這份文件可協助您使用 hello 威脅情報選項可以在 OMS 安全性和稽核 toomonitor 和回應 toosecurity 警示。

## <a name="what-is-oms"></a>何謂 OMS？
Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。

## <a name="threat-intelligence"></a>威脅情報
在企業環境中使用者廣泛存取 toohello 網路，並使用各種裝置 tooconnect toocorporate 資料，請務必您可以主動監視您的資源和快速回應 toosecurity 事件。 這是重要的觀點 hello 安全性開發週期因為某些顧慮威脅可能不會引發警示的特定或傳統的安全性技術控制項可以識別的可疑活動。 

使用 hello**威脅情報**選項可在 OMS 安全性和稽核，IT 系統管理員可以識別針對 hello 環境的安全性威脅，例如，識別特定的電腦是否屬於[殭屍網路](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection)。 當攻擊者非法地安裝惡意軟體偷偷地連接此電腦 toohello 命令和控制項時，電腦可能會變成殭屍網路中的節點。 它也可以識別來自地下通訊通道 (例如 [暗網](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents)) 的潛在威脅。 

在順序 toobuild 這個威脅情報 OMS 安全性和稽核，請使用來自 Microsoft 內部的多個來源的資料。 OMS 安全性和稽核將會利用這個資料 tooidentify 潛在的威脅攻擊的環境。

hello 威脅情報窗格是由三個主要選項所組成：

* 具有輸出惡意流量的伺服器
* 偵測到的威脅類型
* 威脅情報對應

> [!NOTE]
> 如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。
> 
> 

### <a name="responding-toosecurity-alerts"></a>回應 toosecurity 警示
其中一個的 hello 步驟[安全性事件回應](https://technet.microsoft.com/library/cc512623.aspx)程序是 tooidentify hello 嚴重性 hello 危害系統。 在這個階段您應該執行下列工作的 hello:

* 判斷 hello 攻擊的 hello 本質
* 判斷 hello 的原點的攻擊點。
* 判斷 hello 攻擊的 hello 意圖。 Hello 攻擊是直接在您的組織 tooacquire 的特定資訊，或是它隨機嗎？
* 識別已受到危害的 hello 系統
* 識別已存取，並判斷那些檔案的 hello 敏感度的 hello 檔案

您可以利用**威脅情報**OMS 安全性和稽核解決方案 toohelp 這些工作中的資訊。 請遵循以下 tooaccess hello 步驟這**威脅情報**選項：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. 在 hello**安全性和稽核**儀表板，您會看到 hello**威脅情報**hello 方選項，如下所示：
   
    ![威脅情報](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

這些三個磚會提供您的 hello 潛在威脅的概觀。 在 hello**具有惡意連出流量伺服器**（內部或外部網路），您要監視的任何電腦時，將會無法 tooidentify 也就是傳送惡意流量 toohello 網際網路。 

hello**偵測到威脅類型**磚會顯示為最新的 「 在 hello wild"hello 威脅的摘要時，如果您按一下這個磚會看見更多有關這些威脅的詳細資料如下所示：

![偵測到的威脅類型](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

您可以按一下每個威脅，以擷取其詳細資訊。 以下的 hello 範例顯示更多詳細殭屍網路：

![威脅的詳細資料](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

本章節的 hello 開頭所述，這項資訊可以是很有幫助期間事件回應案例。 它也可以是重要期間鑑識偵查，您需要 toofind hello 來源 hello 攻擊，哪個系統已遭到洩露，而且 hello 時間軸的位置。 例如，您可以輕鬆地識別 hello 攻擊的一些重要詳細這份報表中： hello hello 攻擊的來源、 hello 受到危害的本機 IP 和 hello hello 連接的目前工作階段狀態。 

hello**威脅情報對應**協助 tooidentify hello 目前位置周圍 hello 地球惡意流量。 有 （內送） 的橙色和紅色 （外寄） 箭號在此對應中，找出 hello 流量的方向，如果您按一下的其中一個這些箭號，它會顯示 hello 類型的威脅和 hello 流量方向如下所示：

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> 您可以觀看示範如何 toouse 這項功能，在事件回應程序藉由監看 hello 簡報[降低資料中心的安全性威脅與使用 Operations Management Suite 的引導式調查](https://myignite.microsoft.com/videos/5000)在 Microsoft Ignite 傳遞。
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a>回應 toodistinct 惡意 IP 存取
在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

此警示和其他人在 hello 相同類別目錄，利用透過 OMS 安全性會產生[Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。 hello 威脅情報資料是 Microsoft 所收集，以及主要威脅情報提供者購買。 這項資料會經常更新，並調整 toofast 移動的威脅。 Tooits 本質，因為它應與結合其他來源的安全性資訊時[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示。 

## <a name="customize-alerts-received-via-e-mail"></a>自訂透過電子郵件接收的警示

您可以自訂在 OMS 安全性觸發安全性警示時，組織內的哪些使用者會收到通知。 這個選項才可以使用下概觀 / 設定在 hello OMS 儀表板：

![電子郵件](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 toouse hello**威脅情報**OMS 安全性和稽核解決方案 toorespond toosecurity 警示中的選項。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

