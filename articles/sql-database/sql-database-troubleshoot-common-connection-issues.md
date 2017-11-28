---
title: "常見連接問題 tooAzure aaaTroubleshoot SQL 資料庫"
description: "步驟 tooidentify 並解決常見連接錯誤 for Azure SQL Database。"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a><span data-ttu-id="fe500-103">疑難排解連接問題 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="fe500-103">Troubleshoot connection issues tooAzure SQL Database</span></span>
<span data-ttu-id="fe500-104">Hello 連接 tooAzure SQL 資料庫失敗時，您會收到[錯誤訊息](sql-database-develop-error-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="fe500-104">When hello connection tooAzure SQL Database fails, you receive [error messages](sql-database-develop-error-messages.md).</span></span> <span data-ttu-id="fe500-105">本文是集中式主題，可協助您針對 Azure SQL Database 連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="fe500-105">This article is a centralized topic that helps you troubleshoot Azure SQL Database connectivity issues.</span></span> <span data-ttu-id="fe500-106">它會導致[hello 常見原因](#cause)連線問題的建議[疑難排解工具](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues)，它可協助您識別 hello 問題，並提供疑難排解步驟 toosolve [暫時性錯誤](#troubleshoot-transient-errors)和[永續性或非暫時性錯誤](#troubleshoot-persistent-errors)。</span><span class="sxs-lookup"><span data-stu-id="fe500-106">It introduces [hello common causes](#cause) of connection issues, recommends [a troubleshooting tool](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) that helps you identity hello problem, and provides troubleshooting steps toosolve [transient errors](#troubleshoot-transient-errors) and [persistent or non-transient errors](#troubleshoot-persistent-errors).</span></span> 

<span data-ttu-id="fe500-107">如果您遇到 hello 連線問題，請嘗試 hello 疑難排解這篇文章所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="fe500-107">If you encounter hello connection issues, try hello troubleshoot steps that are described in this article.</span></span>
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a><span data-ttu-id="fe500-108">原因</span><span class="sxs-lookup"><span data-stu-id="fe500-108">Cause</span></span>
<span data-ttu-id="fe500-109">連線問題可能被因 hello 下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="fe500-109">Connection problems may be caused by any of hello following:</span></span>

* <span data-ttu-id="fe500-110">失敗 tooapply 最佳作法和設計指導方針 hello 應用程式在設計程序。</span><span class="sxs-lookup"><span data-stu-id="fe500-110">Failure tooapply best practices and design guidelines during hello application design process.</span></span>  <span data-ttu-id="fe500-111">請參閱[SQL Database 開發概觀](sql-database-develop-overview.md)tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="fe500-111">See [SQL Database Development Overview](sql-database-develop-overview.md) tooget started.</span></span>
* <span data-ttu-id="fe500-112">Azure SQL Database 重新設定</span><span class="sxs-lookup"><span data-stu-id="fe500-112">Azure SQL Database reconfiguration</span></span>
* <span data-ttu-id="fe500-113">防火牆設定</span><span class="sxs-lookup"><span data-stu-id="fe500-113">Firewall settings</span></span>
* <span data-ttu-id="fe500-114">連線逾時</span><span class="sxs-lookup"><span data-stu-id="fe500-114">Connection time-out</span></span>
* <span data-ttu-id="fe500-115">不正確的登入資訊</span><span class="sxs-lookup"><span data-stu-id="fe500-115">Incorrect login information</span></span>
* <span data-ttu-id="fe500-116">部分 Azure SQL Database 資源已達上限</span><span class="sxs-lookup"><span data-stu-id="fe500-116">Maximum limit reached on some Azure SQL Database resources</span></span>

<span data-ttu-id="fe500-117">一般而言，SQL Database 的連接問題 tooAzure 可分類如下：</span><span class="sxs-lookup"><span data-stu-id="fe500-117">Generally, connection issues tooAzure SQL Database can be classified as follows:</span></span>

* [<span data-ttu-id="fe500-118">暫時性錯誤 (短期或間歇性)</span><span class="sxs-lookup"><span data-stu-id="fe500-118">Transient errors (short-lived or intermittent)</span></span>](#troubleshoot-transient-errors)
* [<span data-ttu-id="fe500-119">持續性或非暫時性錯誤 (定期重複發生的錯誤)</span><span class="sxs-lookup"><span data-stu-id="fe500-119">Persistent or non-transient errors (errors that regularly recur)</span></span>](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a><span data-ttu-id="fe500-120">再試一次 hello Azure SQL Database 連線問題疑難排解</span><span class="sxs-lookup"><span data-stu-id="fe500-120">Try hello troubleshooter for Azure SQL Database connectivity issues</span></span>
<span data-ttu-id="fe500-121">如果您遇到特定的連線錯誤，請嘗試使用 [此工具](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)，此工具可協助您快速識別並解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="fe500-121">If you encounter a specific connection error, try [this tool](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), which will help you quickly identity and resolve your problem.</span></span>

## <a name="troubleshoot-transient-errors"></a><span data-ttu-id="fe500-122">針對暫時性錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="fe500-122">Troubleshoot transient errors</span></span>

<span data-ttu-id="fe500-123">當應用程式連接 tooan Azure SQL database 時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe500-123">When an application connects tooan Azure SQL database, you receive hello following error message:</span></span>

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> <span data-ttu-id="fe500-124">此錯誤訊息是通常是暫時性 (短期)。</span><span class="sxs-lookup"><span data-stu-id="fe500-124">This error message is typically transient (short-lived).</span></span>
> 
> 

<span data-ttu-id="fe500-125">這個錯誤發生在 hello Azure 資料庫正要移動 （或重新設定） 和您的應用程式將會遺失其連線 toohello SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe500-125">This error occurs when hello Azure database is being moved (or reconfigured) and your application loses its connection toohello SQL database.</span></span> <span data-ttu-id="fe500-126">SQL Database 重新設定事件由於規劃的事件 (例如，軟體升級) 或未規劃的事件 (例如，處理序損毀或負載平衡) 而發生。</span><span class="sxs-lookup"><span data-stu-id="fe500-126">SQL database reconfiguration events occur because of a planned event (for example, a software upgrade) or an unplanned event (for example, a process crash, or load balancing).</span></span> <span data-ttu-id="fe500-127">大部分的重新設定事件通常只是短期的，至多應在不到 60 秒的時間完成。</span><span class="sxs-lookup"><span data-stu-id="fe500-127">Most reconfiguration events are generally short-lived and should be completed in less than 60 seconds at most.</span></span> <span data-ttu-id="fe500-128">不過，這些事件可能偶爾會需要較長的 toofinish，例如大型交易何時會導致長時間執行復原。</span><span class="sxs-lookup"><span data-stu-id="fe500-128">However, these events can occasionally take longer toofinish, such as when a large transaction causes a long-running recovery.</span></span>

### <a name="steps-tooresolve-transient-connectivity-issues"></a><span data-ttu-id="fe500-129">步驟 tooresolve 暫時性連線問題</span><span class="sxs-lookup"><span data-stu-id="fe500-129">Steps tooresolve transient connectivity issues</span></span>

1. <span data-ttu-id="fe500-130">檢查 hello [Microsoft Azure 服務儀表板](https://azure.microsoft.com/status)的 hello 時間期間的 hello hello 應用程式所報告錯誤期間發生任何已知中斷。</span><span class="sxs-lookup"><span data-stu-id="fe500-130">Check hello [Microsoft Azure Service Dashboard](https://azure.microsoft.com/status) for any known outages that occurred during hello time during which hello errors were reported by hello application.</span></span>
2. <span data-ttu-id="fe500-131">連接 tooa 雲端服務，例如 Azure SQL Database 應該預期會定期重新設定事件，並實作應用程式會重試邏輯 toohandle 而不是為應用程式錯誤 toousers 面對這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="fe500-131">Applications that connect tooa cloud service such as Azure SQL Database should expect periodic reconfiguration events and implement retry logic toohandle these errors instead of surfacing these as application errors toousers.</span></span> <span data-ttu-id="fe500-132">檢閱 hello[暫時性錯誤](sql-database-connectivity-issues.md)區段和 hello 的最佳作法和設計指導方針，在[SQL Database 開發概觀](sql-database-develop-overview.md)如需詳細資訊和一般重試策略。</span><span class="sxs-lookup"><span data-stu-id="fe500-132">Review hello [Transient errors](sql-database-connectivity-issues.md) section and hello best practices and design guidelines at [SQL Database Development Overview](sql-database-develop-overview.md) for more information and general retry strategies.</span></span> <span data-ttu-id="fe500-133">如需詳細資訊，請接著參閱 [適用於 SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md) 的程式碼範例 。</span><span class="sxs-lookup"><span data-stu-id="fe500-133">Then, see code samples at [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md) for specifics.</span></span>
3. <span data-ttu-id="fe500-134">資料庫接近其資源限制，它看起來令 toobe 暫時性連線問題。</span><span class="sxs-lookup"><span data-stu-id="fe500-134">As a database approaches its resource limits, it can seem toobe a transient connectivity issue.</span></span> <span data-ttu-id="fe500-135">請參閱 [移難排解效能問題](sql-database-troubleshoot-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="fe500-135">See [Troubleshooting Performance Issues](sql-database-troubleshoot-performance.md).</span></span>
4. <span data-ttu-id="fe500-136">如果連線問題仍然存在，或如果 hello 您的應用程式，在遇到 hello 錯誤的持續時間超過 60 秒，或您看到某一天中的 hello 錯誤的多個項目，請選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options)站台。</span><span class="sxs-lookup"><span data-stu-id="fe500-136">If connectivity problems continue, or if hello duration for which your application encounters hello error exceeds 60 seconds or if you see multiple occurrences of hello error in a given day, file an Azure support request by selecting **Get Support** on hello [Azure Support](https://azure.microsoft.com/support/options) site.</span></span>

## <a name="troubleshoot-persistent-errors"></a><span data-ttu-id="fe500-137">針對持續性錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="fe500-137">Troubleshoot persistent errors</span></span>
<span data-ttu-id="fe500-138">如果 hello 應用程式持續失敗 tooconnect tooAzure SQL 資料庫，通常表示 hello 下列其中一種問題：</span><span class="sxs-lookup"><span data-stu-id="fe500-138">If hello application persistently fails tooconnect tooAzure SQL Database, it usually indicates an issue with one of hello following:</span></span>

* <span data-ttu-id="fe500-139">防火牆組態。</span><span class="sxs-lookup"><span data-stu-id="fe500-139">Firewall configuration.</span></span> <span data-ttu-id="fe500-140">hello Azure SQL 資料庫或用戶端防火牆封鎖連線 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fe500-140">hello Azure SQL database or client-side firewall is blocking connections tooAzure SQL Database.</span></span>
* <span data-ttu-id="fe500-141">網路 hello 用戶端上的重新設定： 例如，新的 IP 位址或 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fe500-141">Network reconfiguration on hello client side: for example, a new IP address or a proxy server.</span></span>
* <span data-ttu-id="fe500-142">使用者錯誤： 例如，輸入連線參數，例如 hello hello 連接字串中的伺服器名稱不正確。</span><span class="sxs-lookup"><span data-stu-id="fe500-142">User error: for example, mistyped connection parameters, such as hello server name in hello connection string.</span></span>

### <a name="steps-tooresolve-persistent-connectivity-issues"></a><span data-ttu-id="fe500-143">步驟 tooresolve 持續性連線問題</span><span class="sxs-lookup"><span data-stu-id="fe500-143">Steps tooresolve persistent connectivity issues</span></span>
1. <span data-ttu-id="fe500-144">設定[防火牆規則](sql-database-configure-firewall-settings.md)tooallow hello 用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe500-144">Set up [firewall rules](sql-database-configure-firewall-settings.md) tooallow hello client IP address.</span></span> <span data-ttu-id="fe500-145">為暫存限測試用途，設定為 起始 IP 位址範圍，並使用 hello 結束 IP 位址範圍為 255.255.255.255 hello 使用 0.0.0.0 的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="fe500-145">For temporary testing purposes, set up a firewall rule using 0.0.0.0 as hello starting IP address range and using 255.255.255.255 as hello ending IP address range.</span></span> <span data-ttu-id="fe500-146">這會開啟 hello 伺服器 tooall IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe500-146">This will open hello server tooall IP addresses.</span></span> <span data-ttu-id="fe500-147">若這樣可解決您的連線問題，請移除此規則並針對已適當限制的 IP 位址或位址範圍建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="fe500-147">If this resolves your connectivity issue, remove this rule and create a firewall rule for an appropriately limited IP address or address range.</span></span> 
2. <span data-ttu-id="fe500-148">在 hello 用戶端與 hello 網際網路之間的所有防火牆，請確定連接埠 1433年是開啟傳出連接。</span><span class="sxs-lookup"><span data-stu-id="fe500-148">On all firewalls between hello client and hello Internet, make sure that port 1433 is open for outbound connections.</span></span> <span data-ttu-id="fe500-149">檢閱[設定 hello SQL Server 存取的 Windows 防火牆 tooAllow](https://msdn.microsoft.com/library/cc646023.aspx)和[混合式身分識別所需的連接埠和通訊協定](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports)是否有其他指標相關 tooadditional 連接埠，您需要的 tooopenAzure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="fe500-149">Review [Configure hello Windows Firewall tooAllow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx) and [Hybrid Identity Required Ports and Protocols](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) for additional pointers related tooadditional ports that you need tooopen for Azure Active Directory authentication.</span></span>
3. <span data-ttu-id="fe500-150">請確認您的連接字串和其他連線設定。</span><span class="sxs-lookup"><span data-stu-id="fe500-150">Verify your connection string and other connection settings.</span></span> <span data-ttu-id="fe500-151">請參閱 hello 連接字串 > 一節中 hello[連線問題主題](sql-database-connectivity-issues.md#connections-to-azure-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="fe500-151">See hello Connection String section in hello [connectivity issues topic](sql-database-connectivity-issues.md#connections-to-azure-sql-database).</span></span>
4. <span data-ttu-id="fe500-152">檢查 hello 儀表板中的服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="fe500-152">Check service health in hello dashboard.</span></span> <span data-ttu-id="fe500-153">如果您認為沒有地區中斷，請參閱[從中斷復原](sql-database-disaster-recovery.md)步驟 toorecover tooa 新的區域。</span><span class="sxs-lookup"><span data-stu-id="fe500-153">If you think there’s a regional outage, see [Recover from an outage](sql-database-disaster-recovery.md) for steps toorecover tooa new region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe500-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe500-154">Next steps</span></span>
* [<span data-ttu-id="fe500-155">針對 Azure SQL Database 效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="fe500-155">Troubleshoot Azure SQL Database performance issues</span></span>](sql-database-troubleshoot-performance.md)
* [<span data-ttu-id="fe500-156">Microsoft Azure 上搜尋 hello 文件</span><span class="sxs-lookup"><span data-stu-id="fe500-156">Search hello documentation on Microsoft Azure</span></span>](http://azure.microsoft.com/search/documentation/)
* [<span data-ttu-id="fe500-157">檢視 hello 最新更新 toohello Azure SQL Database 服務</span><span class="sxs-lookup"><span data-stu-id="fe500-157">View hello latest updates toohello Azure SQL Database service</span></span>](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a><span data-ttu-id="fe500-158">其他資源</span><span class="sxs-lookup"><span data-stu-id="fe500-158">Additional resources</span></span>
* [<span data-ttu-id="fe500-159">SQL Database 開發概觀</span><span class="sxs-lookup"><span data-stu-id="fe500-159">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="fe500-160">一般暫時性錯誤處理指引</span><span class="sxs-lookup"><span data-stu-id="fe500-160">General transient fault-handling guidance</span></span>](../best-practices-retry-general.md)
* [<span data-ttu-id="fe500-161">SQL Database 和 SQL Server 的連線庫</span><span class="sxs-lookup"><span data-stu-id="fe500-161">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

