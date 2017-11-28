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
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="eae45-103">開始使用威脅偵測</span><span class="sxs-lookup"><span data-stu-id="eae45-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eae45-104">稽核</span><span class="sxs-lookup"><span data-stu-id="eae45-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="eae45-105">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="eae45-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="eae45-106">概觀</span><span class="sxs-lookup"><span data-stu-id="eae45-106">Overview</span></span>
<span data-ttu-id="eae45-107">威脅偵測偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="eae45-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="eae45-108">威脅偵測處於預覽階段，SQL 資料倉儲支援此功能。</span><span class="sxs-lookup"><span data-stu-id="eae45-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="eae45-109">威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。</span><span class="sxs-lookup"><span data-stu-id="eae45-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="eae45-110">使用者可以瀏覽 hello 可疑事件使用[Azure SQL 資料倉儲稽核](sql-data-warehouse-auditing-overview.md)toodetermine 如果他們未嘗試 tooaccess，導致違反或利用 hello 資料倉儲中的資料。</span><span class="sxs-lookup"><span data-stu-id="eae45-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="eae45-111">威脅偵測使得 toohello 資料倉儲不 hello 需要 toobe 安全性專家或監視系統的進階的安全性的管理簡單 tooaddress 潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="eae45-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="eae45-112">威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="eae45-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="eae45-113">SQL 資料隱碼是 hello 常見的 Web 應用程式的安全性問題在 hello 網際網路，使用的 tooattack 資料導向應用程式。</span><span class="sxs-lookup"><span data-stu-id="eae45-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="eae45-114">攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到違反或修改 hello 資料庫中的資料的應用程式項目欄位。</span><span class="sxs-lookup"><span data-stu-id="eae45-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="eae45-115">設定資料庫的威脅偵測</span><span class="sxs-lookup"><span data-stu-id="eae45-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="eae45-116">啟動 hello Azure 入口網站則位於[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="eae45-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="eae45-117">瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eae45-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="eae45-118">在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="eae45-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![瀏覽窗格][1]
3. <span data-ttu-id="eae45-120">在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，這會顯示 hello 威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="eae45-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![瀏覽窗格][2]
4. <span data-ttu-id="eae45-122">[開啟]  威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="eae45-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="eae45-123">設定將會收到偵測的異常資料倉儲活動時的安全性警示的電子郵件的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="eae45-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="eae45-124">按一下**儲存**在 hello**稽核與威脅偵測**組態刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="eae45-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![瀏覽窗格][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="eae45-126">偵測到可疑事件時探索異常資料倉儲活動</span><span class="sxs-lookup"><span data-stu-id="eae45-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="eae45-127">偵測到異常資料庫活動時，您將收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="eae45-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="eae45-128">hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱和 hello 事件時間的 hello 可疑安全性事件。</span><span class="sxs-lookup"><span data-stu-id="eae45-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="eae45-129">此外，它會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="eae45-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![瀏覽窗格][4]
2. <span data-ttu-id="eae45-131">在 hello 電子郵件，按一下 hello **Azure SQL 稽核記錄檔**連結，也會啟動 hello Azure 傳統入口網站，並顯示 hello 事件時間的 hello 可疑周圍 hello 相關稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="eae45-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![瀏覽窗格][5]
3. <span data-ttu-id="eae45-133">按一下 hello 稽核記錄 tooview hello 可疑的資料庫活動，例如 SQL 陳述式的詳細失敗的原因與用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="eae45-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![瀏覽窗格][6]
4. <span data-ttu-id="eae45-135">在 hello 稽核記錄刀鋒視窗中，按一下 **在 Excel 中開啟**tooopen 預先設定的 excel 範本 tooimport 和 hello 周圍 hello 事件時間的 hello 可疑的稽核記錄檔執行深入分析。</span><span class="sxs-lookup"><span data-stu-id="eae45-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="eae45-136">
   **注意：**在 Excel 2010 或更新版本的 Power Query 和 hello**快速合併**是必要設定</span><span class="sxs-lookup"><span data-stu-id="eae45-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![瀏覽窗格][7]
5. <span data-ttu-id="eae45-138">tooconfigure hello**快速合併**設定位在 hello **POWER QUERY**功能區索引標籤上，選取**選項**toodisplay hello 選項 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="eae45-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="eae45-139">選取 hello 隱私權區段，然後選擇 hello 第二個選項-[忽略 hello 隱私權等級並可能會改善效能]:</span><span class="sxs-lookup"><span data-stu-id="eae45-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![瀏覽窗格][8]
6. <span data-ttu-id="eae45-141">tooload SQL 稽核記錄檔，請務必 hello 設定 索引標籤中的 hello 參數正確設定，然後選取 hello 「 資料 」 功能區按一下 hello 全部重新整理 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eae45-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![瀏覽窗格][9]
7. <span data-ttu-id="eae45-143">hello 結果會出現在 hello **SQL 稽核記錄檔**可讓您的 hello 異常活動偵測到，並減少應用程式中的 hello 安全性事件 hello 影響 toorun 深入分析的工作表。</span><span class="sxs-lookup"><span data-stu-id="eae45-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
