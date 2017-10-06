---
title: "aaaMonitoring Operations Management Suite 安全性和稽核解決方案中的資源 |Microsoft 文件"
description: "這份文件可協助 toouse OMS 安全性和稽核功能 toomonitor 資源，並找出安全性問題。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>在 Operations Management Suite 安全性和稽核內監視資源
這份文件可協助您使用 OMS 安全性和稽核功能 toomonitor 資源，並找出安全性問題。

## <a name="what-is-oms"></a>何謂 OMS？
Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。

## <a name="monitoring-resources"></a>監視資源
只要可能，您會想 tooprevent 安全性事件發生在 hello 第一個位置。 不過，它是不可能 tooprevent 所有安全性事件。 當發生安全性事件時，您必須 tooensure 其影響會降至最低。  有三個重要的建議，可以使用的 toominimize hello 數字和 hello 安全性事件的影響：

* 定期評估您環境內的弱點。
* 定期檢查所有電腦的系統和網路裝置 tooensure 他們擁有的所有安裝 hello 最新修補程式。
* 定期檢查所有記錄檔和記錄機制，包括作業系統事件記錄檔、應用程式特定記錄檔,以及入侵偵測系統記錄檔。

OMS 安全性和稽核解決方案讓 IT tooactively 監視所有的資源，可協助安全性事件的 hello 影響降到最低。 OMS 安全性和稽核俱備可用來監視資源的安全性網域。 hello 安全性網域提供快速存取 tooa 選項，將更多詳細資料中涵蓋下列網域安全性監視 hello:

* 惡意程式碼評估
* 更新評估
* 身分識別與存取

> [!NOTE]
> 如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。
> 
> 

### <a name="monitoring-system-protection"></a>監視系統保護
在防禦深度方法中，每個圖層的保護是很重要的 hello 整體的安全性狀態的資產。 具有電腦偵測到威脅及保護效力不足的電腦會顯示在 hello 安全性網域底下的 [惡意程式碼評估] 磚。 藉由使用 hello 惡意程式碼評估 hello 資訊，您可以識別計劃 tooapply 保護 toohello 需要伺服器上。 tooaccess 這個選項後續 hello 的步驟如下：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. 在 hello**安全性和稽核**儀表板，按一下**反惡意程式碼評定**下**安全性網域**。 hello**反惡意程式碼評定**儀表板隨即出現，如下所示：

![惡意程式碼評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

您可以使用 hello**惡意程式碼評估**儀表板 tooidentify hello 下列安全性問題：

* **作用中威脅**： 洩露和 hello 系統中有作用中威脅的電腦。
* **補救威脅**： 補救洩露但 hello 威脅的電腦。
* **簽章已過期**： 已啟用但 hello 簽章的惡意程式碼保護的電腦已過期。
* [沒有即時保護]：電腦並無安裝反惡意程式碼產品。

### <a name="monitoring-updates"></a>監控更新
套用最新安全性更新 hello 安全性最佳作法是，它應該納入更新管理策略中。 Microsoft Monitoring Agent 服務 (HealthService.exe) 讀取受監視電腦的更新資訊，並再將此更新的資訊 toohello OMS 服務傳送 hello 雲端進行處理。 hello Microsoft Monitoring Agent 服務設定為自動服務，就應該一律在 hello 目標電腦中執行。

![監控更新](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

邏輯是套用的 toohello 更新資料和 hello 雲端服務會記錄 hello 資料。 如果找到遺失的更新，它們會顯示在 hello**更新**儀表板。 您可以使用 hello**更新**儀表板 toowork 使用遺漏的更新及開發計劃 tooapply 它們 toohello 需要的伺服器。 請遵循以下 tooaccess hello hello 步驟**更新**儀表板：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。
2. 在 hello**安全性和稽核**儀表板，按一下 **更新評估**下**安全性網域**。 hello 更新儀表板會顯示如下所示：

![更新評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

此儀表板中，您可以執行更新評估 toounderstand hello 目前狀態的電腦和地址 hello 最嚴重的威脅。 使用 hello**重大或安全性更新**磚，IT 系統管理員都能 tooaccess 詳細的資訊遺失，如下所示的 hello 更新：

![搜尋結果](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

此報表包含重要資訊，可以使用 tooidentify hello 威脅類型，此系統很容易，其中包括 hello 與 hello 安全性更新和 hello 具有更多詳細 hello MS 公告相關聯的 Microsoft 知識庫文章弱點。

### <a name="monitoring-identity-and-access"></a>監視身分識別與存取
由於使用者有隨處工作、使用不同裝置，以及存取大量雲端及內部部署應用程式的需求，因此務必確保他們的認證能受到保護。 認證遭竊的攻擊是指在這一開始攻擊者存取 tooa 一般使用者的認證 tooaccess hello 網路內的系統。 許多次，這個初始攻擊是只方式 tooget toohello 網路存取，hello 最終目標 toodiscover 權限的帳戶。 

攻擊者會保留在 hello 網路使用免費工具 tooextract hello 工作階段的其他登入帳戶的認證。 根據 hello 系統設定，這些認證可以擷取 hello 形式雜湊、 票證或甚至純文字密碼。  

> [!NOTE]
> 機器的直接公開網際網路，將會看到許多失敗，嘗試使用所有類型的已知使用者名稱 （例如系統管理員），再試一次 toologin toohello。 在大部分情況下它是 [確定]，如果 hello 已知的使用者名稱不會使用而且 hello 密碼效力不夠。
> 
> 

它是可能 tooidentify 這些入侵者之前它們危害權限的帳戶。 您可以利用**OMS 安全性和稽核解決方案**toomonitor 身分識別和存取。 請遵循以下 tooaccess hello hello 步驟**身分識別和存取**儀表板：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下 安全性和稽核磚。
2. 在 hello**安全性和稽核**儀表板，按一下**身分識別和存取**下**安全性網域**。 hello**身分識別和存取**儀表板隨即出現，如下所示：

![身分識別與存取](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

作為定期監視策略的一部分，您必須包含身分識別監視。 IT 系統管理員應查看是否有特定的有效使用者名稱，出現多次登入嘗試的情況。 這可能表示可能是攻擊者取得 hello 實際使用者名稱，然後再次嘗試 toobrute force 或自動的工具，會使用硬式編碼的密碼已過期。

此儀表板啟用 IT tooquickly 識別潛在威脅相關的 tooidentity 及存取 toocompany 的資源。 它是特定重要 tooalso 找出潛在的趨勢，例如 hello 登入一段時間在磚中，您可以看到經過一段時間執行的失敗登入嘗試的次數。 在此情況下 hello 電腦**FileServer**收到 35 登入嘗試。 只要按一下該項目，您就可以瞭解更多關於此電腦的詳細資訊。 

![其他詳細資訊](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

此電腦所產生的 hello 報表會使此模式有關的重要詳細資料。 注意到該 hello**帳戶**hello 已使用的 tootry tooaccess 的使用者帳戶的資料行提供 hello 系統，hello **TIMEGENERATED** hello 中的 hello 嘗試將已完成的時間間隔的資料行提供和hello **LOGONTYPENAME** hello 了這項嘗試位置的資料行提供。 如果這些嘗試執行本機 hello 系統中的程式，hello**程序**hello 處理序的名稱會顯示資料行。 在 hello 登入嘗試從程式所在的情況下，您已經有可用的 hello 處理序名稱，現在您可以執行進一步調查 hello 目標系統中。

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 toouse OMS 安全性和稽核解決方案 toomonitor 您的資源。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)

