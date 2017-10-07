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
# <a name="sql-database-threat-detection"></a><span data-ttu-id="bd6b4-103">SQL Database 威脅偵測</span><span class="sxs-lookup"><span data-stu-id="bd6b4-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="bd6b4-104">SQL 威脅偵測到可能會不尋常和有害嘗試 tooaccess 或利用資料庫異常活動。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="bd6b4-105">概觀</span><span class="sxs-lookup"><span data-stu-id="bd6b4-105">Overview</span></span>

<span data-ttu-id="bd6b4-106">SQL 威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="bd6b4-107">一旦有可疑活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式發生，使用者將會收到警示。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="bd6b4-108">SQL 威脅偵測警示提供可疑活動的詳細資訊和建議動作如何 tooinvestigate 和降低 hello 威脅。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="bd6b4-109">使用者可以瀏覽 hello 可疑事件使用[SQL Database 稽核](sql-database-auditing.md)toodetermine 如果他們未嘗試 tooaccess，導致違反，或利用 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="bd6b4-110">威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階監視系統的安全性。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="bd6b4-111">例如，SQL 資料隱碼是 hello 一般 Web 應用程式安全性問題 hello 網際網路，使用的 tooattack 資料導向應用程式上的其中一個。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="bd6b4-112">攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到應用程式項目欄位中，違反或修改 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="bd6b4-113">SQL 威脅偵測整合與警示[Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)，和在 hello 相同價格以 Azure 安全性中心標準層，在 $15/節點/月，每個受保護 SQL 計費每部受保護的 SQL Database 伺服器資料庫伺服器都會計算為一個節點。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="bd6b4-114">我們邀請您 tootry 它 60 天的免費。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="bd6b4-115">設定資料庫 hello Azure 入口網站中的威脅偵測</span><span class="sxs-lookup"><span data-stu-id="bd6b4-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="bd6b4-116">啟動 hello Azure 入口網站在[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bd6b4-117">瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor 的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="bd6b4-118">在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="bd6b4-119">![導覽窗格][1]</span><span class="sxs-lookup"><span data-stu-id="bd6b4-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="bd6b4-120">在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，將會顯示 hello 威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![瀏覽窗格][2]
4. <span data-ttu-id="bd6b4-122">[開啟]  威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="bd6b4-123">設定將會收到偵測的異常資料庫活動時的安全性警示的電子郵件的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="bd6b4-124">按一下**儲存**在 hello**稽核與威脅偵測**刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測設定。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![瀏覽窗格][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="bd6b4-126">使用 PowerShell 設定威脅偵測</span><span class="sxs-lookup"><span data-stu-id="bd6b4-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="bd6b4-127">如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="bd6b4-128">偵測到可疑事件時探索異常資料庫活動</span><span class="sxs-lookup"><span data-stu-id="bd6b4-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="bd6b4-129">偵測到異常資料庫活動時，您將收到電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="bd6b4-130">hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱、 應用程式名稱，以及 hello 事件時間的 hello 可疑安全性事件。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="bd6b4-131">此外，hello 電子郵件會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![瀏覽窗格][4]
2. <span data-ttu-id="bd6b4-133">hello 電子郵件警示包含直接連結 toohello SQL 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="bd6b4-134">按一下此連結會啟動 hello Azure 入口網站，並開啟 hello SQL 稽核記錄周圍 hello hello 可疑事件時間。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="bd6b4-135">按一下稽核記錄 tooview hello 可疑的資料庫活動，讓您更容易 toofind hello SQL 執行的陳述式的詳細 (誰在存取，他們的做法和時)，並判斷是否合法或惡意 hello 事件 （例如應用程式tooSQL 資料隱碼攻擊的弱點可能會被利用、 有人破壞敏感性資料，依此類推）。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="bd6b4-136">
   ![導覽窗格][5]</span><span class="sxs-lookup"><span data-stu-id="bd6b4-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="bd6b4-137">瀏覽資料庫 hello Azure 入口網站中的威脅偵測警示</span><span class="sxs-lookup"><span data-stu-id="bd6b4-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="bd6b4-138">SQL Database 威脅偵測將自有的警示與 [Azure 資訊安全中心](https://azure.microsoft.com/en-us/services/security-center/)整合。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="bd6b4-139">動態 SQL 安全性磚內 hello 資料庫刀鋒視窗中的作用中威脅的 hello Azure 入口網站的追蹤 hello 狀態中。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![瀏覽窗格][6]
   
1. <span data-ttu-id="bd6b4-141">Hello SQL 安全性磚上按一下 啟動 hello Azure 資訊安全中心警示刀鋒視窗，並提供 hello 資料庫上偵測到作用中的 SQL 威脅的概觀。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![瀏覽窗格][7]

2. <span data-ttu-id="bd6b4-143">按一下特定警示會提供其他詳細資料和調查此威脅的建議，並對未來的威脅採取補救措施。</span><span class="sxs-lookup"><span data-stu-id="bd6b4-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![導覽窗格][8]


## <a name="next-steps"></a><span data-ttu-id="bd6b4-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd6b4-145">Next steps</span></span>

* <span data-ttu-id="bd6b4-146">深入了解威脅偵測，請瀏覽 hello [Azure 部落格](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="bd6b4-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="bd6b4-147">深入了解 [Azure SQL Database 稽核](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="bd6b4-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="bd6b4-148">深入了解 [Azure 資訊安全中心](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="bd6b4-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="bd6b4-149">如需有關定價的詳細資訊，請參閱 hello [SQL Database 定價頁面](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="bd6b4-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="bd6b4-150">如需 PowerShell 指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="bd6b4-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


