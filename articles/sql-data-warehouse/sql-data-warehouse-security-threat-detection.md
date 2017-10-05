---
title: "開始使用 SQL 資料倉儲威脅偵測"
description: "如何開始使用威脅偵測"
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
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="7edae-103">開始使用威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7edae-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7edae-104">稽核</span><span class="sxs-lookup"><span data-stu-id="7edae-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="7edae-105">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7edae-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7edae-106">Overview</span><span class="sxs-lookup"><span data-stu-id="7edae-106">Overview</span></span>
<span data-ttu-id="7edae-107">威脅偵測會偵測異常資料庫活動，指出資料庫有潛在的安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="7edae-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="7edae-108">威脅偵測處於預覽階段，SQL 資料倉儲支援此功能。</span><span class="sxs-lookup"><span data-stu-id="7edae-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="7edae-109">威脅偵測提供新的一層安全性，在發生異常活動時會提供安全性警示，讓客戶偵測並回應潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7edae-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="7edae-110">使用者可以使用 [Azure SQL 資料倉儲稽核](sql-data-warehouse-auditing-overview.md) 來探查可疑的事件，以判斷這些事件是否是因為有人嘗試存取、破壞或利用資料倉儲中的資料而造成。</span><span class="sxs-lookup"><span data-stu-id="7edae-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="7edae-111">您不必是安全性專家，也不需要管理進階的安全性監視系統，威脅偵測讓您輕鬆解決資料倉儲的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7edae-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="7edae-112">威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="7edae-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="7edae-113">SQL 插入式攻擊是網際網路上常見的 Web 應用程式安全性問題之一，用於攻擊資料導向應用程式。</span><span class="sxs-lookup"><span data-stu-id="7edae-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="7edae-114">攻擊者利用應用程式弱點將惡意的 SQL 陳述式插入應用程式輸入欄位，以破壞或修改資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="7edae-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="7edae-115">設定資料庫的威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7edae-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="7edae-116">啟動 Azure 入口網站，位址是 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7edae-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7edae-117">瀏覽至您要監視的 SQL 資料倉儲的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7edae-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="7edae-118">在 [設定] 刀鋒視窗中，選取 [稽核和威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="7edae-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![導覽窗格][1]
3. <span data-ttu-id="7edae-120">在 [稽核和威脅偵測] 組態刀鋒視窗中，[開啟] 稽核，將會顯示威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="7edae-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![導覽窗格][2]
4. <span data-ttu-id="7edae-122">[開啟]  威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="7edae-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="7edae-123">設定在偵測到異常資料倉儲活動時，將收到安全性警示的電子郵件清單。</span><span class="sxs-lookup"><span data-stu-id="7edae-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="7edae-124">在 [稽核和威脅偵測] 組態刀鋒視窗中按一下 [儲存]，以儲存新的或更新的稽核和威脅偵測原則。</span><span class="sxs-lookup"><span data-stu-id="7edae-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![導覽窗格][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="7edae-126">偵測到可疑事件時探索異常資料倉儲活動</span><span class="sxs-lookup"><span data-stu-id="7edae-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="7edae-127">偵測到異常資料庫活動時，您將收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="7edae-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="7edae-128">電子郵件將提供可疑安全性事件的相關資訊，包括異常活動的性質、資料庫名稱、伺服器名稱和事件時間。</span><span class="sxs-lookup"><span data-stu-id="7edae-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="7edae-129">此外，還會提供可能原因和建議動作的相關資訊，以協助您調查和減輕資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7edae-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![導覽窗格][4]
2. <span data-ttu-id="7edae-131">在電子郵件中，按一下 [Azure SQL 稽核記錄檔]  連結會啟動 Azure 傳統入口網站，並顯示可疑事件前後的相關稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="7edae-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![導覽窗格][5]
3. <span data-ttu-id="7edae-133">按一下稽核記錄以檢視可疑資料庫活動的詳細資訊，例如 SQL 陳述式、失敗原因和用戶端的 IP。</span><span class="sxs-lookup"><span data-stu-id="7edae-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![導覽窗格][6]
4. <span data-ttu-id="7edae-135">在 [稽核記錄] 刀鋒視窗中，按一下 [在 Excel 中開啟] 開啟預先設定的 Excel 範本，以匯入可疑事件前後的稽核記錄，執行更深入的分析。</span><span class="sxs-lookup"><span data-stu-id="7edae-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="7edae-136">
   **附註：**在 Excel 2010 或更新版本中，需要有 Power Query 和 [快速合併] 設定</span><span class="sxs-lookup"><span data-stu-id="7edae-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![導覽窗格][7]
5. <span data-ttu-id="7edae-138">若要設定 [快速合併] 設定 - 在 [POWER QUERY] 功能區索引標籤中，選取 [選項] 以顯示 [選項] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7edae-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="7edae-139">選取 [隱私權] 區段，選擇第二個選項 - [忽略隱私權等級並可能改善效能]：</span><span class="sxs-lookup"><span data-stu-id="7edae-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![導覽窗格][8]
6. <span data-ttu-id="7edae-141">若要載入 SQL 稽核記錄檔，請確定 [設定] 索引標籤中的參數已正確設定，然後選取 [資料] 功能區，並按一下 [全部重新整理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7edae-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![導覽窗格][9]
7. <span data-ttu-id="7edae-143">結果會出現在 [SQL 稽核記錄檔]  工作表，可讓您對偵測到的異常活動執行更深入的分析，減輕應用程式中的安全性事件造成的影響。</span><span class="sxs-lookup"><span data-stu-id="7edae-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

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
