---
title: "aaaThreat 偵測-Azure SQL Database |Microsoft 文件"
description: "威脅偵測偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。"
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>SQL Database 威脅偵測

SQL 威脅偵測到可能會不尋常和有害嘗試 tooaccess 或利用資料庫異常活動。

## <a name="overview"></a>概觀

SQL 威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。  一旦有可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式發生，使用者將會收到警示。 SQL 威脅偵測警示提供可疑活動的詳細資訊和建議動作如何 tooinvestigate 和降低 hello 威脅。 使用者可以瀏覽 hello 可疑事件使用[SQL Database 稽核](sql-database-auditing.md)toodetermine 如果他們未嘗試 tooaccess，導致違反，或利用 hello 資料庫中的資料。 威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階監視系統的安全性。

例如，SQL 資料隱碼是 hello 一般 Web 應用程式安全性問題 hello 網際網路，使用的 tooattack 資料導向應用程式上的其中一個。 攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到應用程式項目欄位中，違反或修改 hello 資料庫中的資料。

SQL 威脅偵測整合與警示[Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)，和在 hello 相同價格以 Azure 安全性中心標準層，在 $15/節點/月，每個受保護 SQL 計費每部受保護的 SQL Database 伺服器資料庫伺服器都會計算為一個節點。 我們邀請您 tootry 它 60 天的免費。 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>設定資料庫 hello Azure 入口網站中的威脅偵測
1. 啟動 hello Azure 入口網站在[https://portal.azure.com](https://portal.azure.com)。
2. 瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor 的 SQL 資料庫。 在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。 
    ![導覽窗格][1]
3. 在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，將會顯示 hello 威脅偵測設定。
  
    ![瀏覽窗格][2]
4. [開啟]  威脅偵測。
5. 設定將會收到偵測的異常資料庫活動時的安全性警示的電子郵件的 hello 清單。
6. 按一下**儲存**在 hello**稽核與威脅偵測**刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測設定。
       
    ![瀏覽窗格][3]

## <a name="set-up-threat-detection-using-powershell"></a>使用 PowerShell 設定威脅偵測

如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>偵測到可疑事件時探索異常資料庫活動
1. 偵測到異常資料庫活動時，您將收到電子郵件通知。 <br/>
   hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱、 應用程式名稱，以及 hello 事件時間的 hello 可疑安全性事件。 此外，hello 電子郵件會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。<br/>
     
    ![瀏覽窗格][4]
2. hello 電子郵件警示包含直接連結 toohello SQL 稽核記錄檔。 按一下此連結會啟動 hello Azure 入口網站，並開啟 hello SQL 稽核記錄周圍 hello hello 可疑事件時間。 按一下稽核記錄 tooview hello 可疑的資料庫活動，讓您更容易 toofind hello SQL 執行的陳述式的詳細 (誰在存取，他們的做法和時)，並判斷是否合法或惡意 hello 事件 （例如應用程式tooSQL 資料隱碼攻擊的弱點可能會被利用、 有人破壞敏感性資料，依此類推）。<br/>
   ![導覽窗格][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>瀏覽資料庫 hello Azure 入口網站中的威脅偵測警示

SQL Database 威脅偵測將自有的警示與 [Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)整合。 動態 SQL 安全性磚內 hello 資料庫刀鋒視窗中的作用中威脅的 hello Azure 入口網站的追蹤 hello 狀態中。 

   ![瀏覽窗格][6]
   
1. Hello SQL 安全性磚上按一下 啟動 hello Azure 資訊安全中心警示刀鋒視窗，並提供 hello 資料庫上偵測到作用中的 SQL 威脅的概觀。 

  ![瀏覽窗格][7]

2. 按一下特定警示會提供其他詳細資料和調查此威脅的建議，並對未來的威脅採取補救措施。

  ![導覽窗格][8]


## <a name="next-steps"></a>後續步驟

* 深入了解威脅偵測，請瀏覽 hello [Azure 部落格](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* 深入了解 [Azure SQL Database 稽核](sql-database-auditing.md)
* 深入了解 [Azure 資訊安全中心](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* 如需有關定價的詳細資訊，請參閱 hello [SQL Database 定價頁面](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* 如需 PowerShell 指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


