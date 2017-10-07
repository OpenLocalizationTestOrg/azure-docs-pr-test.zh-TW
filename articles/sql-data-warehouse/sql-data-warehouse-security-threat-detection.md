---
title: "aaaGet 開始使用 SQL 資料倉儲威脅偵測"
description: "Tooget 威脅偵測與啟動的方式"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>開始使用威脅偵測
> [!div class="op_single_selector"]
> * [稽核](sql-data-warehouse-auditing-overview.md)
> * [威脅偵測](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>概觀
威脅偵測偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。 威脅偵測處於預覽階段，SQL 資料倉儲支援此功能。

威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。 使用者可以瀏覽 hello 可疑事件使用[Azure SQL 資料倉儲稽核](sql-data-warehouse-auditing-overview.md)toodetermine 如果他們未嘗試 tooaccess，導致違反或利用 hello 資料倉儲中的資料。
威脅偵測使得 toohello 資料倉儲不 hello 需要 toobe 安全性專家或監視系統的進階的安全性的管理簡單 tooaddress 潛在威脅。

威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。 SQL 資料隱碼是 hello 常見的 Web 應用程式的安全性問題在 hello 網際網路，使用的 tooattack 資料導向應用程式。 攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到違反或修改 hello 資料庫中的資料的應用程式項目欄位。

## <a name="set-up-threat-detection-for-your-database"></a>設定資料庫的威脅偵測
1. 啟動 hello Azure 入口網站則位於[https://portal.azure.com](https://portal.azure.com)。
2. 瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor SQL 資料倉儲。 在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。
   
    ![瀏覽窗格][1]
3. 在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，這會顯示 hello 威脅偵測設定。
   
    ![瀏覽窗格][2]
4. [開啟]  威脅偵測。
5. 設定將會收到偵測的異常資料倉儲活動時的安全性警示的電子郵件的 hello 清單。
6. 按一下**儲存**在 hello**稽核與威脅偵測**組態刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測原則。
   
    ![瀏覽窗格][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>偵測到可疑事件時探索異常資料倉儲活動
1. 偵測到異常資料庫活動時，您將收到電子郵件通知。 <br/>
   hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱和 hello 事件時間的 hello 可疑安全性事件。 此外，它會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。<br/>
   
    ![瀏覽窗格][4]
2. 在 hello 電子郵件，按一下 hello **Azure SQL 稽核記錄檔**連結，也會啟動 hello Azure 傳統入口網站，並顯示 hello 事件時間的 hello 可疑周圍 hello 相關稽核記錄。
   
    ![瀏覽窗格][5]
3. 按一下 hello 稽核記錄 tooview hello 可疑的資料庫活動，例如 SQL 陳述式的詳細失敗的原因與用戶端 IP。
   
    ![瀏覽窗格][6]
4. 在 hello 稽核記錄刀鋒視窗中，按一下 **在 Excel 中開啟**tooopen 預先設定的 excel 範本 tooimport 和 hello 周圍 hello 事件時間的 hello 可疑的稽核記錄檔執行深入分析。<br/>
   **注意：**在 Excel 2010 或更新版本的 Power Query 和 hello**快速合併**是必要設定
   
    ![瀏覽窗格][7]
5. tooconfigure hello**快速合併**設定位在 hello **POWER QUERY**功能區索引標籤上，選取**選項**toodisplay hello 選項 對話方塊。 選取 hello 隱私權區段，然後選擇 hello 第二個選項-[忽略 hello 隱私權等級並可能會改善效能]:
   
    ![瀏覽窗格][8]
6. tooload SQL 稽核記錄檔，請務必 hello 設定 索引標籤中的 hello 參數正確設定，然後選取 hello 「 資料 」 功能區按一下 hello 全部重新整理 按鈕。
   
    ![瀏覽窗格][9]
7. hello 結果會出現在 hello **SQL 稽核記錄檔**可讓您的 hello 異常活動偵測到，並減少應用程式中的 hello 安全性事件 hello 影響 toorun 深入分析的工作表。

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
