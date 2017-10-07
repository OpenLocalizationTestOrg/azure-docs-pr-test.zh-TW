---
title: "aaaIntroduction tooAzure 資訊安全中心 |Microsoft 文件"
description: "了解 Azure 資訊安全中心、其主要功能及運作方式。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>簡介 tooAzure 資訊安全中心
了解 Azure 資訊安全中心、其主要功能及運作方式。

> [!NOTE]
> 從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>
>

## <a name="what-is-azure-security-center"></a>什麼是 Azure 資訊安全中心？
 資訊安全中心可協助您防止、 偵測，並回應 toothreats 增加的可見性與您的 Azure 資源的 hello 安全性控制。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

## <a name="key-capabilities"></a>主要功能
 資訊安全中心，提供方便使用且有效的威脅防止、 偵測和回應 tooAzure 內建的功能。 主要功能：

| 階段 | 功能 |
| --- | --- |
| 防止 |監視 hello Azure 資源的安全性狀態 |
| 防止 | 定義原則，根據貴公司的安全性需求，hello 類型的應用程式，並 hello 敏感性資料的 Azure 訂用帳戶 |
| 防止 | 原則導向的使用安全性建議 tooguide 服務擁有者透過 hello 程序的實作所需的控制項 |
| 防止 | 快速部署 Microsoft 和第三方的安全性服務和應用裝置 |
| 偵測 |自動收集並分析從您的 Azure 資源、 hello 網路和反惡意程式碼的程式和防火牆等協力廠商解決方案的安全性資料 |
| 偵測 | 使用全域威脅情報從 Microsoft 產品和服務，Microsoft 數位犯罪單元 (DCU)，hello hello Microsoft Security Response Center (MSRC) 和外部的摘要 |
| 偵測 | 套用進階分析，包括機器學習服務和行為分析 |
| 回應 |依優先順序提供安全性事件/警示 |
| 回應 | Hello 來源 hello 攻擊和受影響的資源的深入探討 |
| 回應 | 建議 toostop hello 目前攻擊，並協助避免遭受病毒攻擊的方法 |

## <a name="introductory-walkthrough"></a>逐步解說介紹

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。 本文件不是一份逐步解說指南。
>
>

 您可以存取的資訊安全中心從 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 [登入 toohello 入口網站](https://portal.azure.com)。 在 hello 主要入口網站功能表上，捲動 toohello**資訊安全中心**選項或選取 hello**資訊安全中心**先前插入 toohello 入口網站儀表板的磚。

![Azure 入口網站中的安全性磚][1]

從資訊安全中心，您可以設定安全性原則、監視安全性組態，並檢視安全性警示。

### <a name="security-policies"></a>安全性原則
Azure 訂用帳戶，根據 tooyour 公司的安全性需求，您可以定義原則。 您可以也量身訂作這些 toohello 類型正在使用的應用程式或 toohello 敏感度 hello 資料的每個訂用帳戶中。 例如，用於開發或測試的資源與用於實際執行應用程式的資源，兩者的安全性需求可能不同。 同樣地，具有規範資料 (例如 PII) 的應用程式可能需要較高層級的安全性。

> [!NOTE]
> toomodify 安全性原則，您必須是安全性系統管理員或 hello 訂用帳戶的擁有者或參與者。 toolearn 深入了解角色和允許的動作，資訊安全中心，請參閱[Azure 資訊安全中心中的權限](security-center-permissions.md)。
>
>

在 hello**資訊安全中心**刀鋒視窗中，選取 hello**原則**磚一份您的訂用帳戶和資源群組。   

![[資訊安全中心] 刀鋒視窗][2]

在 hello**安全性原則**刀鋒視窗中，選取 訂用帳戶 tooview hello 原則詳細資料。

**資料收集**啟用安全性原則的資料收集。 若加以啟用可以：

* 每日掃描所有支援的虛擬機器 (VM)，取得安全性監視和建議。
* 收集安全性事件，供分析和偵測威脅所用。

> [!NOTE]
> Hello 訂用帳戶層級會設定資料收集。
>
>

選取**防止原則**tooopen hello**防止原則**刀鋒視窗。 **顯示建議**可讓您選擇您想要您想根據 hello 安全性需求的 hello 訂用帳戶內的 hello 資源 toosee toomonitor 和 hello 建議的 hello 安全性控制項。

### <a name="security-recommendations"></a>安全性建議
 資訊安全中心會分析您的 Azure 資源 tooidentify 潛在的安全性漏洞 hello 安全性狀態。 建議清單會引導您完成設定所需的控制項的 hello 程序。 範例包括：

* 佈建反惡意程式碼 toohelp 識別及移除惡意軟體
* 設定網路安全性群組與規則 toocontrol 流量 tooVMs
* Web 應用程式防火牆 toohelp 防禦攻擊目標 web 應用程式的佈建
* 部署遺漏的系統更新
* 定址 OS 組態不符合 hello 建議基準

按一下 hello**建議**磚的建議清單。 按一下每個建議 tooview 其他資訊或 tootake 動作 tooresolve hello 問題。

![Azure 資訊安全中心的安全性建議][5]

### <a name="security-state-of-azure-resources"></a>Azure 資源的安全性狀態
hello**防止**hello 儀表板 區段顯示 hello hello 環境資源類型，包括 Vm、 web 應用程式，以及其他資源的整體安全性狀態。   

選取資源類型下的**防止**tooview 詳細資訊，包括任何已識別的潛在安全性漏洞的清單。 (**計算**hello 上例中選取。)

![資源健康狀態磚][6]

### <a name="security-alerts"></a>安全性警示
 資訊安全中心會自動收集、 分析，並將記錄資料從 Azure 資源、 hello 網路和反惡意程式碼的程式和防火牆等協力廠商解決方案相整合。 偵測到威脅時，會建立安全性警示。 偵測範例包括：

* 已受到危害的 VM 與已知的惡意 IP 位址進行通訊
* 使用 Windows 錯誤報告偵測到進階的惡意程式碼
* 針對 VM 的暴力密碼破解攻擊
* 來自整合式反惡意程式碼程式和防火牆的安全性警示

按一下 hello**安全性警示**磚會顯示一份已排列優先順序的警示。

![安全性警示][7]

選取警示會顯示 hello 攻擊和建議的詳細資訊 tooremediate 它。

![安全性警示詳細資料][8]

### <a name="partner-solutions"></a>合作夥伴解決方案
hello**合作夥伴解決方案**與您 Azure 訂用帳戶整合磚可讓您監視在協力廠商解決方案概覽 hello 安全性狀態。 資訊安全中心會顯示來自 hello 解決方案的警示。

選取 hello**合作夥伴解決方案**磚。 隨即開啟一個刀鋒視窗，其中顯示所有已連接的合作夥伴解決方案清單。

![合作夥伴解決方案][9]

## <a name="get-started"></a>開始使用
tooget 啟動與資訊安全中心，您需要訂用帳戶 tooMicrosoft Azure。 資訊安全中心已經由 Azure 訂用帳戶啟用。 如果您沒有訂用帳戶，可以註冊[免費試用](https://azure.microsoft.com/pricing/free-trial/)。

 您可以存取的資訊安全中心從 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 請參閱 hello[入口網站的文件](https://azure.microsoft.com/documentation/services/azure-portal/)toolearn 更多。

[開始使用 Azure 資訊安全中心](security-center-get-started.md)快速引導您完成 hello 安全性監視和原則管理元件的資訊安全中心。

## <a name="next-steps"></a>後續步驟
本文件中所導入了的 tooSecurity 中心、 其重要功能，以及如何 tooget 啟動。 toolearn 詳細資訊，請參閱下列資源的 hello:

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示。
* [監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
- [Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)— 取得最新 Azure 安全性消息 hello 和資訊。

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
