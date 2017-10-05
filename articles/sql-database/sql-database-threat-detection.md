---
title: "威脅偵測 - Azure SQL Database | Microsoft Docs"
description: "威脅偵測會偵測異常資料庫活動，指出資料庫有潛在的安全性威脅。"
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
ms.openlocfilehash: bd3de9ed0131edc683763b0fe7f4a2ae74533944
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="7390c-103">SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7390c-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="7390c-104">SQL 威脅偵測會偵測意圖存取或攻擊資料庫，並可能會造成損害的異常活動。</span><span class="sxs-lookup"><span data-stu-id="7390c-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="7390c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7390c-105">Overview</span></span>

<span data-ttu-id="7390c-106">SQL 威脅偵測提供新的一層安全性，在發生異常活動時會提供安全性警示，讓客戶偵測並回應潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7390c-106">SQL Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="7390c-107">一旦有可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式發生，使用者將會收到警示。</span><span class="sxs-lookup"><span data-stu-id="7390c-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="7390c-108">SQL 威脅偵測警示會提供可疑活動的詳細資料，以及如何調查與降低威脅的建議。</span><span class="sxs-lookup"><span data-stu-id="7390c-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how to investigate and mitigate the threat.</span></span> <span data-ttu-id="7390c-109">使用者可以使用 [SQL Database 稽核](sql-database-auditing.md)來探索可疑的事件，以判斷事件的原因是否是有人嘗試存取、破壞或利用資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="7390c-109">Users can explore the suspicious events using [SQL Database Auditing](sql-database-auditing.md) to determine if they result from an attempt to access, breach, or exploit data in the database.</span></span> <span data-ttu-id="7390c-110">您不必是安全性專家，也不需要管理進階的安全性監視系統，威脅偵測讓您輕鬆解決資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7390c-110">Threat Detection makes it simple to address potential threats to the database without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="7390c-111">例如，SQL 插入式攻擊是網際網路上常見的 Web 應用程式安全性問題之一，用於攻擊資料導向應用程式。</span><span class="sxs-lookup"><span data-stu-id="7390c-111">For example, SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="7390c-112">攻擊者利用應用程式弱點將惡意的 SQL 陳述式插入應用程式輸入欄位，破壞或修改資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="7390c-112">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, breaching or modifying data in the database.</span></span>

<span data-ttu-id="7390c-113">SQL 威脅偵測整合了警示與 [Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)。每部受保護 SQL Database 伺服器的收費與 Azure 資訊安全中心標準層相同，全部是每月每個節點 $15，其中每部受保護的 SQL Database 伺服務各會計為一個節點。</span><span class="sxs-lookup"><span data-stu-id="7390c-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at the same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="7390c-114">敬邀您免費試用 60 天。</span><span class="sxs-lookup"><span data-stu-id="7390c-114">We invite you to try it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-the-azure-portal"></a><span data-ttu-id="7390c-115">使用 Azure 入口網站為資料庫設定威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7390c-115">Set up threat detection for your database in the Azure portal</span></span>
1. <span data-ttu-id="7390c-116">啟動 Azure 入口網站，位址是 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7390c-116">Launch the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7390c-117">瀏覽至您要監視的 SQL Database 的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7390c-117">Navigate to the configuration blade of the SQL Database you want to monitor.</span></span> <span data-ttu-id="7390c-118">在 [設定] 刀鋒視窗中，選取 [稽核和威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="7390c-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="7390c-119">![導覽窗格][1]</span><span class="sxs-lookup"><span data-stu-id="7390c-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="7390c-120">在 [稽核與威脅偵測] 組態刀鋒視窗中，[開啟] 稽核，這會顯示威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="7390c-120">In the **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display the threat detection settings.</span></span>
  
    ![導覽窗格][2]
4. <span data-ttu-id="7390c-122">[開啟]  威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="7390c-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="7390c-123">設定在偵測到異常資料庫活動時將收到安全性警示的電子郵件清單。</span><span class="sxs-lookup"><span data-stu-id="7390c-123">Configure the list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="7390c-124">按一下 [稽核與威脅偵測] 刀鋒視窗中的 [儲存]，以儲存新的或已更新的稽核與威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="7390c-124">Click **Save** in the **Auditing & Threat detection** blade to save the new or updated auditing and threat detection settings.</span></span>
       
    ![導覽窗格][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="7390c-126">使用 PowerShell 設定威脅偵測</span><span class="sxs-lookup"><span data-stu-id="7390c-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="7390c-127">如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="7390c-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="7390c-128">偵測到可疑事件時探索異常資料庫活動</span><span class="sxs-lookup"><span data-stu-id="7390c-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="7390c-129">偵測到異常資料庫活動時，您將收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="7390c-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="7390c-130">電子郵件將提供可疑安全性事件的相關資訊，包括異常活動的性質、資料庫名稱、伺服器名稱、應用程式名稱和事件時間。</span><span class="sxs-lookup"><span data-stu-id="7390c-130">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name, application name, and the event time.</span></span> <span data-ttu-id="7390c-131">此外，該電子郵件還會提供可能原因和建議動作的相關資訊，以協助您調查和減輕資料庫的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="7390c-131">In addition, the email will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
     
    ![導覽窗格][4]
2. <span data-ttu-id="7390c-133">電子郵件警示包含 SQL 稽核記錄的直接連結。</span><span class="sxs-lookup"><span data-stu-id="7390c-133">The email alert includes a direct link to the SQL Audit log.</span></span> <span data-ttu-id="7390c-134">按一下此連結會啟動 Azure 入口網站，並開啟可疑活動發生時間前後的 SQL 稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="7390c-134">Clicking on this link launches the Azure portal and opens the SQL Audit records around the time of the suspicious event.</span></span> <span data-ttu-id="7390c-135">按一下稽核記錄可檢視可疑資料庫活動的詳細資料，讓您輕鬆找出遭到執行的 SQL 陳述式 (存取的人、動作和時間)，以及判斷該事件屬於正當或是惡意 (例如SQL 插入式攻擊的應用程式弱點遭到利用或有人破壞機密資料等)。</span><span class="sxs-lookup"><span data-stu-id="7390c-135">Click on an audit record to view more details on the suspicious database activities, making it easier to find the SQL statements that were executed (who accessed, what they did and when) and determine if the event was legitimate or malicious (e.g. application vulnerability to SQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="7390c-136">
   ![導覽窗格][5]</span><span class="sxs-lookup"><span data-stu-id="7390c-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-the-azure-portal"></a><span data-ttu-id="7390c-137">在 Azure 入口網站中探索資料庫的威脅偵測警示</span><span class="sxs-lookup"><span data-stu-id="7390c-137">Explore threat detection alerts for your database in the Azure portal</span></span>

<span data-ttu-id="7390c-138">SQL Database 威脅偵測將自有的警示與 [Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)整合。</span><span class="sxs-lookup"><span data-stu-id="7390c-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="7390c-139">在 Azure 入口網站中，資料庫刀鋒視窗內的 SQL 動態安全性圖格會追蹤威脅 (作用中) 的狀態。</span><span class="sxs-lookup"><span data-stu-id="7390c-139">A live SQL security tile within the database blade in the Azure portal tracks the status of active threats.</span></span> 

   ![導覽窗格][6]
   
1. <span data-ttu-id="7390c-141">按一下 SQL 安全性圖格會啟動 Azure 資訊安全中心的警示刀鋒視窗，以及提供在資料庫中偵測到的 SQL 威脅 (作用中) 概觀。</span><span class="sxs-lookup"><span data-stu-id="7390c-141">Clicking on the SQL security tile launches the Azure Security Center alerts blade and provides an overview of active SQL threats detected on the database.</span></span> 

  ![導覽窗格][7]

2. <span data-ttu-id="7390c-143">按一下特定警示會提供其他詳細資料和調查此威脅的建議，並對未來的威脅採取補救措施。</span><span class="sxs-lookup"><span data-stu-id="7390c-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![導覽窗格][8]


## <a name="next-steps"></a><span data-ttu-id="7390c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7390c-145">Next steps</span></span>

* <span data-ttu-id="7390c-146">若要深入了解威脅偵測，請造訪 [Azure 部落格](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="7390c-146">Learn more about Threat Detection, visit the [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="7390c-147">深入了解 [Azure SQL Database 稽核](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="7390c-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="7390c-148">深入了解 [Azure 資訊安全中心](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="7390c-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="7390c-149">如需有關價格的詳細資訊，請參閱 [SQL Database 價格頁面](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="7390c-149">For more details on pricing, please see the [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="7390c-150">如需 PowerShell 指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="7390c-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


