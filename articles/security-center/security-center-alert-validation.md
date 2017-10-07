---
title: "aaaAlerts 驗證 Azure 資訊安全中心 |Microsoft 文件"
description: "這份文件可協助您在 Azure 資訊安全中心 toovalidate hello 安全性警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Azure 資訊安全中心的警示驗證
這份文件可協助您瞭解如何 tooverify 系統已正確設定 Azure 資訊安全中心警示。

## <a name="what-are-security-alerts"></a>什麼是安全性警示：
資訊安全中心會自動收集、 分析，並將記錄資料從 Azure 資源、 hello 網路和連線的協力廠商解決方案，例如防火牆和 endpoint protection 解決方案、 toodetect 和警示您 toothreats 相整合。 讀取[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)如需有關安全性警示] 及 [讀取[了解 Azure 資訊安全中心中的安全性警示](https://docs.microsoft.com/azure/security-center/security-center-alerts-type)toolearn 更多關於 hello 不同類型的警示。

## <a name="alert-validation"></a>警示驗證
資訊安全中心代理程式安裝在電腦上之後，請依照 hello 執行下列步驟從 hello 電腦您要的 hello 警示 toobe 遭受攻擊的 hello 資源：

1. 複製可執行檔 （適用於範例 calc.exe) toohello 電腦的桌面或您的方便的其他目錄。
2. 此檔案重新命名過**ASC_AlertTest_662jfi039N.exe**。
3. 開啟 hello 命令提示字元並執行此檔案使用的引數 （只是假的引數名稱），例如： *ASC_AlertTest_662jfi039N.exe foo*
4. 等待 5 too10 分鐘，然後開啟安全性中心警示。 您應該會那里發現警示類似 toofollowing 其中一個：

    ![警示驗證](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

當檢閱此警示，請確定啟用稽核引數的 hello 欄位會顯示為 true。 如果為 false，您需要稽核 tooenable 命令列引數。 您可以啟用此選項，使用下列命令列的 hello:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>另請參閱
這篇文章會引進 toohello 警示驗證程序。 既然您已熟悉這項驗證，請嘗試下列發行項的 hello:

* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)。 深入了解如何 toomanage 警示 」 和 「 資訊安全中心回應 toosecurity 事件。
* [Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md)。 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [了解 Azure 資訊安全中心的安全性警示](https://docs.microsoft.com/azure/security-center/security-center-alerts-type)。 深入了解 hello 不同類型的安全性警示。
* [Azure 資訊安全中心疑難排解指南](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide)。 了解如何 tootroubleshoot 常見問題資訊安全中心。 
* [Azure 資訊安全中心常見問題集](security-center-faq.md)。 尋找有關使用 hello 服務常見問題。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)。 尋找有關 Azure 安全性與相容性的部落格文章。

