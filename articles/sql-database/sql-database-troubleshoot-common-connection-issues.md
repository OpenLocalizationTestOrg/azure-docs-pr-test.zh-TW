---
title: "疑難排解 Azure SQL Database 常見的連接問題"
description: "找出並解決 Azure SQL Database 常見之連接錯誤的步驟。"
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
ms.openlocfilehash: b8abf1285318e491d51aadf90f921103d84ce1a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-connection-issues-to-azure-sql-database"></a><span data-ttu-id="27606-103">針對 Azure SQL Database 連線問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="27606-103">Troubleshoot connection issues to Azure SQL Database</span></span>
<span data-ttu-id="27606-104">連線到 Azure SQL Database 失敗時，您會收到 [錯誤訊息](sql-database-develop-error-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="27606-104">When the connection to Azure SQL Database fails, you receive [error messages](sql-database-develop-error-messages.md).</span></span> <span data-ttu-id="27606-105">本文是集中式主題，可協助您針對 Azure SQL Database 連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="27606-105">This article is a centralized topic that helps you troubleshoot Azure SQL Database connectivity issues.</span></span> <span data-ttu-id="27606-106">本文除了介紹連線問題的[常見原因](#cause)，還推薦可協助您識別問題的[疑難排解工具](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues)，以及提供疑難排解步驟來解決[暫時性錯誤](#troubleshoot-transient-errors)和[持續性或非暫時性錯誤](#troubleshoot-persistent-errors)。</span><span class="sxs-lookup"><span data-stu-id="27606-106">It introduces [the common causes](#cause) of connection issues, recommends [a troubleshooting tool](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) that helps you identity the problem, and provides troubleshooting steps to solve [transient errors](#troubleshoot-transient-errors) and [persistent or non-transient errors](#troubleshoot-persistent-errors).</span></span> 

<span data-ttu-id="27606-107">如果您遇到連線問題，請嘗試本文中所述的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="27606-107">If you encounter the connection issues, try the troubleshoot steps that are described in this article.</span></span>
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a><span data-ttu-id="27606-108">原因</span><span class="sxs-lookup"><span data-stu-id="27606-108">Cause</span></span>
<span data-ttu-id="27606-109">連線問題可能由下列任何一個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="27606-109">Connection problems may be caused by any of the following:</span></span>

* <span data-ttu-id="27606-110">在設計應用程式的過程中，無法套用最佳作法和設計指南。</span><span class="sxs-lookup"><span data-stu-id="27606-110">Failure to apply best practices and design guidelines during the application design process.</span></span>  <span data-ttu-id="27606-111">請參閱 [SQL Database 開發概觀](sql-database-develop-overview.md) 以便開始使用。</span><span class="sxs-lookup"><span data-stu-id="27606-111">See [SQL Database Development Overview](sql-database-develop-overview.md) to get started.</span></span>
* <span data-ttu-id="27606-112">Azure SQL Database 重新設定</span><span class="sxs-lookup"><span data-stu-id="27606-112">Azure SQL Database reconfiguration</span></span>
* <span data-ttu-id="27606-113">防火牆設定</span><span class="sxs-lookup"><span data-stu-id="27606-113">Firewall settings</span></span>
* <span data-ttu-id="27606-114">連線逾時</span><span class="sxs-lookup"><span data-stu-id="27606-114">Connection time-out</span></span>
* <span data-ttu-id="27606-115">不正確的登入資訊</span><span class="sxs-lookup"><span data-stu-id="27606-115">Incorrect login information</span></span>
* <span data-ttu-id="27606-116">部分 Azure SQL Database 資源已達上限</span><span class="sxs-lookup"><span data-stu-id="27606-116">Maximum limit reached on some Azure SQL Database resources</span></span>

<span data-ttu-id="27606-117">一般而言，Azure SQL Database 的連線問題可以分類如下：</span><span class="sxs-lookup"><span data-stu-id="27606-117">Generally, connection issues to Azure SQL Database can be classified as follows:</span></span>

* [<span data-ttu-id="27606-118">暫時性錯誤 (短期或間歇性)</span><span class="sxs-lookup"><span data-stu-id="27606-118">Transient errors (short-lived or intermittent)</span></span>](#troubleshoot-transient-errors)
* [<span data-ttu-id="27606-119">持續性或非暫時性錯誤 (定期重複發生的錯誤)</span><span class="sxs-lookup"><span data-stu-id="27606-119">Persistent or non-transient errors (errors that regularly recur)</span></span>](#troubleshoot-persistent-errors)

## <a name="try-the-troubleshooter-for-azure-sql-database-connectivity-issues"></a><span data-ttu-id="27606-120">嘗試使用 Azure SQL Database 連線問題疑難排解工具</span><span class="sxs-lookup"><span data-stu-id="27606-120">Try the troubleshooter for Azure SQL Database connectivity issues</span></span>
<span data-ttu-id="27606-121">如果您遇到特定的連線錯誤，請嘗試使用 [此工具](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)，此工具可協助您快速識別並解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="27606-121">If you encounter a specific connection error, try [this tool](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), which will help you quickly identity and resolve your problem.</span></span>

## <a name="troubleshoot-transient-errors"></a><span data-ttu-id="27606-122">針對暫時性錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="27606-122">Troubleshoot transient errors</span></span>

<span data-ttu-id="27606-123">當應用程式連接到 Azure SQL Database 時，您會收到下列錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="27606-123">When an application connects to an Azure SQL database, you receive the following error message:</span></span>

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry the connection later. If the problem persists, contact customer support, and provide them the session tracing ID of <z>"
```

> [!NOTE]
> <span data-ttu-id="27606-124">此錯誤訊息是通常是暫時性 (短期)。</span><span class="sxs-lookup"><span data-stu-id="27606-124">This error message is typically transient (short-lived).</span></span>
> 
> 

<span data-ttu-id="27606-125">當移動 (或重新設定) Azure 資料庫時會發生此錯誤，而且您的應用程式會失去與 SQL Database 的連接。</span><span class="sxs-lookup"><span data-stu-id="27606-125">This error occurs when the Azure database is being moved (or reconfigured) and your application loses its connection to the SQL database.</span></span> <span data-ttu-id="27606-126">SQL Database 重新設定事件由於規劃的事件 (例如，軟體升級) 或未規劃的事件 (例如，處理序損毀或負載平衡) 而發生。</span><span class="sxs-lookup"><span data-stu-id="27606-126">SQL database reconfiguration events occur because of a planned event (for example, a software upgrade) or an unplanned event (for example, a process crash, or load balancing).</span></span> <span data-ttu-id="27606-127">大部分的重新設定事件通常只是短期的，至多應在不到 60 秒的時間完成。</span><span class="sxs-lookup"><span data-stu-id="27606-127">Most reconfiguration events are generally short-lived and should be completed in less than 60 seconds at most.</span></span> <span data-ttu-id="27606-128">不過，這些事件可能偶爾會需要更長時間才能完成，例如當大型交易導致長時間執行的復原時。</span><span class="sxs-lookup"><span data-stu-id="27606-128">However, these events can occasionally take longer to finish, such as when a large transaction causes a long-running recovery.</span></span>

### <a name="steps-to-resolve-transient-connectivity-issues"></a><span data-ttu-id="27606-129">解決暫時性連線問題的步驟</span><span class="sxs-lookup"><span data-stu-id="27606-129">Steps to resolve transient connectivity issues</span></span>

1. <span data-ttu-id="27606-130">檢查 [Microsoft Azure 服務儀表板](https://azure.microsoft.com/status) ，以取得應用程式報告錯誤期間發生的任何已知中斷。</span><span class="sxs-lookup"><span data-stu-id="27606-130">Check the [Microsoft Azure Service Dashboard](https://azure.microsoft.com/status) for any known outages that occurred during the time during which the errors were reported by the application.</span></span>
2. <span data-ttu-id="27606-131">連接到雲端服務的應用程式 (例如 Azure SQL Database) 應該預期定期的重新設定事件，並實作應用程式重試邏輯來處理這些錯誤，而不是將這些錯誤當做應用程式錯誤呈現給使用者。</span><span class="sxs-lookup"><span data-stu-id="27606-131">Applications that connect to a cloud service such as Azure SQL Database should expect periodic reconfiguration events and implement retry logic to handle these errors instead of surfacing these as application errors to users.</span></span> <span data-ttu-id="27606-132">如需詳細資訊和一般重試策略，請檢閱[暫時性錯誤](sql-database-connectivity-issues.md)一節以及 [SQL Database 開發概觀](sql-database-develop-overview.md)的最佳作法和設計指南。</span><span class="sxs-lookup"><span data-stu-id="27606-132">Review the [Transient errors](sql-database-connectivity-issues.md) section and the best practices and design guidelines at [SQL Database Development Overview](sql-database-develop-overview.md) for more information and general retry strategies.</span></span> <span data-ttu-id="27606-133">如需詳細資訊，請接著參閱 [適用於 SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md) 的程式碼範例 。</span><span class="sxs-lookup"><span data-stu-id="27606-133">Then, see code samples at [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md) for specifics.</span></span>
3. <span data-ttu-id="27606-134">由於資料庫接近其資源限制，因此似乎是暫時性連線問題。</span><span class="sxs-lookup"><span data-stu-id="27606-134">As a database approaches its resource limits, it can seem to be a transient connectivity issue.</span></span> <span data-ttu-id="27606-135">請參閱 [移難排解效能問題](sql-database-troubleshoot-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="27606-135">See [Troubleshooting Performance Issues](sql-database-troubleshoot-performance.md).</span></span>
4. <span data-ttu-id="27606-136">如果連線問題繼續發生，或如果您的應用程式發生錯誤的持續時間超過 60 秒，或如果您在一天當中，看到錯誤多次發生，請在 [Azure 支援](https://azure.microsoft.com/support/options)網站上選取 [取得支援]，來提出 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="27606-136">If connectivity problems continue, or if the duration for which your application encounters the error exceeds 60 seconds or if you see multiple occurrences of the error in a given day, file an Azure support request by selecting **Get Support** on the [Azure Support](https://azure.microsoft.com/support/options) site.</span></span>

## <a name="troubleshoot-persistent-errors"></a><span data-ttu-id="27606-137">針對持續性錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="27606-137">Troubleshoot persistent errors</span></span>
<span data-ttu-id="27606-138">如果應用程式持續無法連接到 Azure SQL Database，通常表示下列其中一項發生問題︰</span><span class="sxs-lookup"><span data-stu-id="27606-138">If the application persistently fails to connect to Azure SQL Database, it usually indicates an issue with one of the following:</span></span>

* <span data-ttu-id="27606-139">防火牆組態。</span><span class="sxs-lookup"><span data-stu-id="27606-139">Firewall configuration.</span></span> <span data-ttu-id="27606-140">Azure SQL Database 或用戶端防火牆封鎖 Azure SQL Database 的連接。</span><span class="sxs-lookup"><span data-stu-id="27606-140">The Azure SQL database or client-side firewall is blocking connections to Azure SQL Database.</span></span>
* <span data-ttu-id="27606-141">用戶端上的網路重新設定：例如，新的 IP 位址或 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="27606-141">Network reconfiguration on the client side: for example, a new IP address or a proxy server.</span></span>
* <span data-ttu-id="27606-142">使用者錯誤︰例如，輸入錯誤的連線參數，例如連接字串中的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="27606-142">User error: for example, mistyped connection parameters, such as the server name in the connection string.</span></span>

### <a name="steps-to-resolve-persistent-connectivity-issues"></a><span data-ttu-id="27606-143">解決永久性連線問題的步驟</span><span class="sxs-lookup"><span data-stu-id="27606-143">Steps to resolve persistent connectivity issues</span></span>
1. <span data-ttu-id="27606-144">設定 [防火牆規則](sql-database-configure-firewall-settings.md) 允許用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="27606-144">Set up [firewall rules](sql-database-configure-firewall-settings.md) to allow the client IP address.</span></span> <span data-ttu-id="27606-145">對於臨時測試用途，請設定防火牆規則並使用 0.0.0.0 做為起始 IP 位址範圍，並使用 255.255.255.255 做為結束 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="27606-145">For temporary testing purposes, set up a firewall rule using 0.0.0.0 as the starting IP address range and using 255.255.255.255 as the ending IP address range.</span></span> <span data-ttu-id="27606-146">這樣會開放伺服器供所有 IP 位址存取。</span><span class="sxs-lookup"><span data-stu-id="27606-146">This will open the server to all IP addresses.</span></span> <span data-ttu-id="27606-147">若這樣可解決您的連線問題，請移除此規則並針對已適當限制的 IP 位址或位址範圍建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="27606-147">If this resolves your connectivity issue, remove this rule and create a firewall rule for an appropriately limited IP address or address range.</span></span> 
2. <span data-ttu-id="27606-148">在用戶端與網際網路之間的所有防火牆上，請確定開放連接埠 1433 供輸出連線使用。</span><span class="sxs-lookup"><span data-stu-id="27606-148">On all firewalls between the client and the Internet, make sure that port 1433 is open for outbound connections.</span></span> <span data-ttu-id="27606-149">檢閱[設定 Windows 防火牆以允許 SQL Server 存取](https://msdn.microsoft.com/library/cc646023.aspx)與[混合式身分識別所需的連接埠與通訊協定 (英文)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) 以取得有關必須針對 Azure Active Directory 驗證開放之其他連接埠的其他詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="27606-149">Review [Configure the Windows Firewall to Allow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx) and [Hybrid Identity Required Ports and Protocols](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) for additional pointers related to additional ports that you need to open for Azure Active Directory authentication.</span></span>
3. <span data-ttu-id="27606-150">請確認您的連接字串和其他連線設定。</span><span class="sxs-lookup"><span data-stu-id="27606-150">Verify your connection string and other connection settings.</span></span> <span data-ttu-id="27606-151">請參閱 [連線能力問題主題](sql-database-connectivity-issues.md#connections-to-azure-sql-database)中的「連接字串」一節。</span><span class="sxs-lookup"><span data-stu-id="27606-151">See the Connection String section in the [connectivity issues topic](sql-database-connectivity-issues.md#connections-to-azure-sql-database).</span></span>
4. <span data-ttu-id="27606-152">檢查儀表板中的服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="27606-152">Check service health in the dashboard.</span></span> <span data-ttu-id="27606-153">如果您認為沒有區域性停電，請參閱 [從中斷復原](sql-database-disaster-recovery.md) 以了解復原到新區域的步驟。</span><span class="sxs-lookup"><span data-stu-id="27606-153">If you think there’s a regional outage, see [Recover from an outage](sql-database-disaster-recovery.md) for steps to recover to a new region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27606-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27606-154">Next steps</span></span>
* [<span data-ttu-id="27606-155">針對 Azure SQL Database 效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="27606-155">Troubleshoot Azure SQL Database performance issues</span></span>](sql-database-troubleshoot-performance.md)
* [<span data-ttu-id="27606-156">搜尋 Microsoft Azure 相關文件</span><span class="sxs-lookup"><span data-stu-id="27606-156">Search the documentation on Microsoft Azure</span></span>](http://azure.microsoft.com/search/documentation/)
* [<span data-ttu-id="27606-157">檢視 Azure SQL Database 服務的最新更新</span><span class="sxs-lookup"><span data-stu-id="27606-157">View the latest updates to the Azure SQL Database service</span></span>](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a><span data-ttu-id="27606-158">其他資源</span><span class="sxs-lookup"><span data-stu-id="27606-158">Additional resources</span></span>
* [<span data-ttu-id="27606-159">SQL Database 開發概觀</span><span class="sxs-lookup"><span data-stu-id="27606-159">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="27606-160">一般暫時性錯誤處理指引</span><span class="sxs-lookup"><span data-stu-id="27606-160">General transient fault-handling guidance</span></span>](../best-practices-retry-general.md)
* [<span data-ttu-id="27606-161">SQL Database 和 SQL Server 的連線庫</span><span class="sxs-lookup"><span data-stu-id="27606-161">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

