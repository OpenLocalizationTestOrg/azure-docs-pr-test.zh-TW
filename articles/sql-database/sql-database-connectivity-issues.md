---
title: "修正 SQL 連接錯誤、暫時性錯誤 |Microsoft Docs"
description: "了解如何在 Azure SQL Database 中排解、診斷和防止 SQL 連接錯誤或暫時性錯誤。 "
keywords: "sql 連接, 連接字串, 連接問題, 暫時性錯誤, 連接錯誤"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="57145-104">排解、診斷和防止 SQL Database 的 SQL 連接錯誤和暫時性錯誤</span><span class="sxs-lookup"><span data-stu-id="57145-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="57145-105">本文描述如何防止、排解、診斷和減少您的用戶端應用程式在與 Azure SQL Database 互動時發生的連接錯誤和暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="57145-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="57145-106">了解如何設定重試邏輯、建置連接字串和調整其他連接設定。</span><span class="sxs-lookup"><span data-stu-id="57145-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="57145-107">暫時性錯誤 (暫時性故障)</span><span class="sxs-lookup"><span data-stu-id="57145-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="57145-108">暫時性錯誤 (又稱暫時性故障) 具有很快就會自行解決的根本原因。</span><span class="sxs-lookup"><span data-stu-id="57145-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="57145-109">當 Azure 系統快速地將硬體資源轉移到負載平衡更好的各種工作負載時，偶爾會發生暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="57145-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="57145-110">其中大部分重新設定事件通常會在不到 60 秒內完成。</span><span class="sxs-lookup"><span data-stu-id="57145-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="57145-111">在此重新設定時間範圍期間，與 Azure SQL Database 的連接可能會有問題。</span><span class="sxs-lookup"><span data-stu-id="57145-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="57145-112">建置連接到 Azure SQL Database 的應用程式時，應該預期這些暫時性錯誤，並實作重試邏輯來處理它們，而不是當做應用程式錯誤呈現給使用者。</span><span class="sxs-lookup"><span data-stu-id="57145-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="57145-113">如果用戶端程式使用 ADO.NET，系統會擲回 **SqlException**，告知您的程式發生暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="57145-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="57145-114">**Number** 屬性可以與下列主題中靠近上半部的暫時性錯誤清單進行比較： [SQL Database 用戶端應用程式的 SQL 錯誤碼](sql-database-develop-error-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="57145-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="57145-115">連接與命令</span><span class="sxs-lookup"><span data-stu-id="57145-115">Connection versus command</span></span>
<span data-ttu-id="57145-116">根據下列建立情況，您將重試 SQL 連接或再次建立 SQL 連接：</span><span class="sxs-lookup"><span data-stu-id="57145-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="57145-117">**嘗試連接期間發生暫時性錯誤**：應該在延遲數秒後重試連接。</span><span class="sxs-lookup"><span data-stu-id="57145-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="57145-118">**執行 SQL 查詢命令期間發生暫時性錯誤**：不應該立即重試命令。</span><span class="sxs-lookup"><span data-stu-id="57145-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="57145-119">而是在延遲之後，應該建立全新的連接。</span><span class="sxs-lookup"><span data-stu-id="57145-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="57145-120">然後，可以重試命令。</span><span class="sxs-lookup"><span data-stu-id="57145-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="57145-121">暫時性錯誤的重試邏輯</span><span class="sxs-lookup"><span data-stu-id="57145-121">Retry logic for transient errors</span></span>
<span data-ttu-id="57145-122">用戶端程式若包含重試邏輯，在偶爾遇到暫時性錯誤時就會更可靠。</span><span class="sxs-lookup"><span data-stu-id="57145-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="57145-123">當您的程式透過第三方中介軟體與 Azure SQL Database 進行通訊時，請洽詢廠商中介軟體是否包含暫時性錯誤的重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="57145-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="57145-124">重試原則</span><span class="sxs-lookup"><span data-stu-id="57145-124">Principles for retry</span></span>
* <span data-ttu-id="57145-125">如果是暫時性錯誤，則應該重新嘗試開啟連接。</span><span class="sxs-lookup"><span data-stu-id="57145-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="57145-126">不應該直接重試由於暫時性錯誤而失敗的 SQL SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="57145-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="57145-127">而是建立全新的連線，然後重試 SELECT。</span><span class="sxs-lookup"><span data-stu-id="57145-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="57145-128">SQL UPDATE 陳述式由於暫時性錯誤而失敗時，應該先建立全新的連接，再重試 UPDATE。</span><span class="sxs-lookup"><span data-stu-id="57145-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="57145-129">重試邏輯必須確保整個資料庫交易完成，或整個交易已復原。</span><span class="sxs-lookup"><span data-stu-id="57145-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="57145-130">其他重試考量</span><span class="sxs-lookup"><span data-stu-id="57145-130">Other considerations for retry</span></span>
* <span data-ttu-id="57145-131">下班後自動啟動的批次程式，以及將在早上前完成的批次程式，可以進行長時間間隔的重試。</span><span class="sxs-lookup"><span data-stu-id="57145-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="57145-132">使用者介面程式應該說明了人類將在長時間等候後放棄的傾向。</span><span class="sxs-lookup"><span data-stu-id="57145-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="57145-133">不過，方案不得每隔幾秒鐘重試，因為該原則可能讓系統充斥要求。</span><span class="sxs-lookup"><span data-stu-id="57145-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="57145-134">增加重試之間的間隔</span><span class="sxs-lookup"><span data-stu-id="57145-134">Interval increase between retries</span></span>
<span data-ttu-id="57145-135">我們建議您在您第一次重試前延遲 5 秒鐘。</span><span class="sxs-lookup"><span data-stu-id="57145-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="57145-136">在少於 5 秒的延遲後重試，雲端服務會有超過負荷的風險。</span><span class="sxs-lookup"><span data-stu-id="57145-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="57145-137">對於後續每次重試，延遲應以指數方式成長，最大值為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="57145-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="57145-138">在 [SQL Server 連接集區 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx) 中可找使用 ADO.NET 之用戶端的封鎖期間討論。</span><span class="sxs-lookup"><span data-stu-id="57145-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="57145-139">您也可能想要設定程式在自行終止之前的重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="57145-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="57145-140">具有重試邏輯的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="57145-140">Code samples with retry logic</span></span>
<span data-ttu-id="57145-141">各種程式設計語言中具有重試邏輯的程式碼範例位於：</span><span class="sxs-lookup"><span data-stu-id="57145-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="57145-142">SQL Database 和 SQL Server 的連線庫</span><span class="sxs-lookup"><span data-stu-id="57145-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="57145-143">測試您的重試邏輯</span><span class="sxs-lookup"><span data-stu-id="57145-143">Test your retry logic</span></span>
<span data-ttu-id="57145-144">若要測試您的重試邏輯，您必須在程式仍在執行時模擬或產生可以更正的錯誤。</span><span class="sxs-lookup"><span data-stu-id="57145-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="57145-145">中斷與網路連接以進行測試</span><span class="sxs-lookup"><span data-stu-id="57145-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="57145-146">您可以測試重試邏輯的方法，就是在程式執行時中斷用戶端電腦與網路的連接。</span><span class="sxs-lookup"><span data-stu-id="57145-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="57145-147">錯誤為：</span><span class="sxs-lookup"><span data-stu-id="57145-147">The error will be:</span></span>

* <span data-ttu-id="57145-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="57145-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="57145-149">訊息：「未知的主機」</span><span class="sxs-lookup"><span data-stu-id="57145-149">Message: "No such host is known"</span></span>

<span data-ttu-id="57145-150">第一次重試時，您的程式可以更正拼字錯誤，然後嘗試連接。</span><span class="sxs-lookup"><span data-stu-id="57145-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="57145-151">若要使這個動作可行，請從網路拔除電腦，再啟動您的程式。</span><span class="sxs-lookup"><span data-stu-id="57145-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="57145-152">然後，您的程式會辨識執行階段參數讓程式：</span><span class="sxs-lookup"><span data-stu-id="57145-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="57145-153">暫時將 11001 加入至其錯誤清單，視為暫時性。</span><span class="sxs-lookup"><span data-stu-id="57145-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="57145-154">如往常般嘗試其第一個連接。</span><span class="sxs-lookup"><span data-stu-id="57145-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="57145-155">在攔截到錯誤之後，請從清單中移除 11001。</span><span class="sxs-lookup"><span data-stu-id="57145-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="57145-156">顯示訊息告訴使用者將電腦連線到網路。</span><span class="sxs-lookup"><span data-stu-id="57145-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="57145-157">使用 **Console.ReadLine** 方法或含 [確定] 按鈕的對話方塊，暫停進一步執行。</span><span class="sxs-lookup"><span data-stu-id="57145-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="57145-158">將電腦插入網路中之後。使用者按下 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="57145-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="57145-159">重新嘗試連接，預期成功。</span><span class="sxs-lookup"><span data-stu-id="57145-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="57145-160">連接時拼錯資料庫名稱以進行測試</span><span class="sxs-lookup"><span data-stu-id="57145-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="57145-161">在第一次連接嘗試之前，您的程式可以故意拼錯使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="57145-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="57145-162">錯誤為：</span><span class="sxs-lookup"><span data-stu-id="57145-162">The error will be:</span></span>

* <span data-ttu-id="57145-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="57145-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="57145-164">錯誤將為：「使用者 'WRONG_MyUserName' 登入失敗。」</span><span class="sxs-lookup"><span data-stu-id="57145-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="57145-165">第一次重試時，您的程式可以更正拼字錯誤，然後嘗試連接。</span><span class="sxs-lookup"><span data-stu-id="57145-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="57145-166">若要使這個動作可行，您的程式可以辨識執行階段參數讓程式：</span><span class="sxs-lookup"><span data-stu-id="57145-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="57145-167">暫時將 18456 加入至其錯誤清單，視為暫時性。</span><span class="sxs-lookup"><span data-stu-id="57145-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="57145-168">故意將 'WRONG_' 加入至使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="57145-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="57145-169">在攔截到錯誤之後，請從清單中移除 18456。</span><span class="sxs-lookup"><span data-stu-id="57145-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="57145-170">從使用者名稱中移除 'WRONG_'。</span><span class="sxs-lookup"><span data-stu-id="57145-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="57145-171">重新嘗試連接，預期成功。</span><span class="sxs-lookup"><span data-stu-id="57145-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="57145-172">進行連線重試的.NET SqlConnection 參數</span><span class="sxs-lookup"><span data-stu-id="57145-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="57145-173">如果您的用戶端程式利用 .NET Framework 類別 **System.Data.SqlClient.SqlConnection** 連接到 Azure SQL Database，您應該使用 .NET 4.6.1 或更新版本 (或是 .NET Core)，以利用它的連線重試功能。</span><span class="sxs-lookup"><span data-stu-id="57145-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="57145-174">此功能的詳細資料在 [這裡](http://go.microsoft.com/fwlink/?linkid=393996)。</span><span class="sxs-lookup"><span data-stu-id="57145-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="57145-175">當您為 [SqlConnection](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) 物件建立 **連接字串** 時，您應該調整下列參數的值：</span><span class="sxs-lookup"><span data-stu-id="57145-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="57145-176">ConnectRetryCount &nbsp;&nbsp;*(預設值為 1。範圍是 0 到 255)。*</span><span class="sxs-lookup"><span data-stu-id="57145-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="57145-177">ConnectRetryInterval &nbsp;&nbsp;*(預設值為 1 秒。範圍是 1 到 60)。*</span><span class="sxs-lookup"><span data-stu-id="57145-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="57145-178">Connection Timeout &nbsp;&nbsp;*(預設值為 15 秒。範圍是 0 到 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="57145-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="57145-179">具體來說，您選擇的值應該會讓下列等式成立：</span><span class="sxs-lookup"><span data-stu-id="57145-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="57145-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="57145-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="57145-181">例如，如果計數 = 3，且間隔 = 10 秒，則連線時，僅 29 秒的逾時將無法給予系統充足的時間以進行第三次及最後一次的重試：29 < 3 * 10。</span><span class="sxs-lookup"><span data-stu-id="57145-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="57145-182">連接與命令</span><span class="sxs-lookup"><span data-stu-id="57145-182">Connection versus command</span></span>
<span data-ttu-id="57145-183">**ConnectRetryCount** 和 **ConnectRetryInterval** 參數讓您的 **SqlConnection** 物件可重試連接作業，而不需告知或中斷您的程式，例如將控制權傳回您的程式。</span><span class="sxs-lookup"><span data-stu-id="57145-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="57145-184">可能會在以下情況中發生重試：</span><span class="sxs-lookup"><span data-stu-id="57145-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="57145-185">mySqlConnection.Open 方法呼叫</span><span class="sxs-lookup"><span data-stu-id="57145-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="57145-186">mySqlConnection.Execute 方法呼叫</span><span class="sxs-lookup"><span data-stu-id="57145-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="57145-187">有一些微妙的差異。</span><span class="sxs-lookup"><span data-stu-id="57145-187">There is a subtlety.</span></span> <span data-ttu-id="57145-188">當執行「查詢」  時若發生暫時性錯誤，您的 **SqlConnection** 物件將不會重試連接作業，且絕對不會重試查詢。</span><span class="sxs-lookup"><span data-stu-id="57145-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="57145-189">不過，在傳送您的查詢以供執行之前， **SqlConnection** 會先快速檢查連接。</span><span class="sxs-lookup"><span data-stu-id="57145-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="57145-190">如果快速檢查偵測到連接問題， **SqlConnection** 會重試連接作業。</span><span class="sxs-lookup"><span data-stu-id="57145-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="57145-191">如果重試成功，就會傳送您的查詢以供執行。</span><span class="sxs-lookup"><span data-stu-id="57145-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="57145-192">是否應該將 ConnectRetryCount 與應用程式重試邏輯結合？</span><span class="sxs-lookup"><span data-stu-id="57145-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="57145-193">假設您的應用程式有健全的自訂重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="57145-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="57145-194">它可能會重試連接作業 4 次。</span><span class="sxs-lookup"><span data-stu-id="57145-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="57145-195">如果您將 **ConnectRetryInterval** 和 **ConnectRetryCount** =3 加入到連接字串，您會將重試次數增加為 4 * 3 = 12 次重試。</span><span class="sxs-lookup"><span data-stu-id="57145-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="57145-196">您可能不會想要這麼多的重試次數。</span><span class="sxs-lookup"><span data-stu-id="57145-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="57145-197">連接 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="57145-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="57145-198">連接：連接字串</span><span class="sxs-lookup"><span data-stu-id="57145-198">Connection: Connection string</span></span>
<span data-ttu-id="57145-199">連接到 Azure SQL Database 所需的連接字串和連接到 Microsoft SQL Server 的字串稍有不同。</span><span class="sxs-lookup"><span data-stu-id="57145-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="57145-200">您可以從 [Azure 入口網站](https://portal.azure.com/)複製資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="57145-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="57145-201">連接：IP 位址</span><span class="sxs-lookup"><span data-stu-id="57145-201">Connection: IP address</span></span>
<span data-ttu-id="57145-202">您必須設定 SQL Database 伺服器，以接受來自裝載您的用戶端程式之電腦的通訊。</span><span class="sxs-lookup"><span data-stu-id="57145-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="57145-203">您可以透過 [Azure 入口網站](https://portal.azure.com/)編輯防火牆設定來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="57145-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="57145-204">如果您忘了設定 IP 位址，您的程式將會失敗並出現一個好用的錯誤訊息，陳述必要的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="57145-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="57145-205">如需詳細資訊，請參閱： [作法：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="57145-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="57145-206">連接：連接埠</span><span class="sxs-lookup"><span data-stu-id="57145-206">Connection: Ports</span></span>
<span data-ttu-id="57145-207">通常，您只需要在裝載用戶端程式的電腦上確定已開啟連接埠 1433 進行輸出通訊。</span><span class="sxs-lookup"><span data-stu-id="57145-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="57145-208">例如，當用戶端程式裝載在 Windows 電腦上時，主機上的 Windows 防火牆可讓您開啟通訊埠 1433：</span><span class="sxs-lookup"><span data-stu-id="57145-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="57145-209">開啟 [控制台]</span><span class="sxs-lookup"><span data-stu-id="57145-209">Open the Control Panel</span></span>
2. <span data-ttu-id="57145-210">&gt;所有控制台項目</span><span class="sxs-lookup"><span data-stu-id="57145-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="57145-211">&gt;Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="57145-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="57145-212">&gt;進階設定</span><span class="sxs-lookup"><span data-stu-id="57145-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="57145-213">&gt; 輸出規則</span><span class="sxs-lookup"><span data-stu-id="57145-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="57145-214">&gt;動作</span><span class="sxs-lookup"><span data-stu-id="57145-214">&gt; Actions</span></span>
7. <span data-ttu-id="57145-215">&gt;新增規則</span><span class="sxs-lookup"><span data-stu-id="57145-215">&gt; New Rule</span></span>

<span data-ttu-id="57145-216">如果您的用戶端程式裝載在 Azure 虛擬機器 (VM) 上，您應該閱讀：</span><span class="sxs-lookup"><span data-stu-id="57145-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="57145-217">[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。</span><span class="sxs-lookup"><span data-stu-id="57145-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="57145-218">如需設定連接埠及 IP 位址的背景資訊，請參閱： [Azure SQL Database 防火牆](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="57145-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="57145-219">連接：ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="57145-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="57145-220">如果您的程式使用類似 **System.Data.SqlClient.SqlConnection** 的 ADO.NET 類別來連接到 Azure SQL Database，建議您使用 .NET Framework 4.6.1 版或更新的版本。</span><span class="sxs-lookup"><span data-stu-id="57145-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="57145-221">ADO.NET 4.6.1：</span><span class="sxs-lookup"><span data-stu-id="57145-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="57145-222">對於 Azure SQL Database，使用 **SqlConnection.Open** 方法來開啟連接時，可靠性更高。</span><span class="sxs-lookup"><span data-stu-id="57145-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="57145-223">針對連接逾時期間內的特定錯誤， **Open** 方法現在包含最佳重試機制來因應暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="57145-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="57145-224">支援連接共用。</span><span class="sxs-lookup"><span data-stu-id="57145-224">Supports connection pooling.</span></span> <span data-ttu-id="57145-225">這包括提供給您的程式的連接物件是否運作的有效驗證。</span><span class="sxs-lookup"><span data-stu-id="57145-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="57145-226">當您從連接集區使用連接物件時，建議您的程式若未立即使用連接，則暫時關閉它。</span><span class="sxs-lookup"><span data-stu-id="57145-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="57145-227">重新開啟連接比建立新的連接更便宜。</span><span class="sxs-lookup"><span data-stu-id="57145-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="57145-228">如果您使用 ADO.NET 4.0 或更舊版本，建議您升級到最新的 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="57145-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="57145-229">從 2015 年 11 月開始，您可以 [下載 ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57145-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="57145-230">診斷</span><span class="sxs-lookup"><span data-stu-id="57145-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="57145-231">診斷：測試公用程式是否可以連接</span><span class="sxs-lookup"><span data-stu-id="57145-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="57145-232">如果您的程式無法連接到 Azure SQL Database，有一個診斷選項將嘗試與公用程式連接。</span><span class="sxs-lookup"><span data-stu-id="57145-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="57145-233">理想的情況下，此公用程式會使用您的程式使用的同一程式庫來連接。</span><span class="sxs-lookup"><span data-stu-id="57145-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="57145-234">您可以在任何 Windows 電腦上，嘗試這些公用程式：</span><span class="sxs-lookup"><span data-stu-id="57145-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="57145-235">SQL Server Management Studio (SSMS.exe)，連接時使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="57145-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="57145-236">sqlcmd.exe，連接時使用 [ODBC](http://msdn.microsoft.com/library/jj730308.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57145-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="57145-237">一旦完成連接，就會測試簡短的 SQL SELECT 查詢是否可以運作。</span><span class="sxs-lookup"><span data-stu-id="57145-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="57145-238">診斷：檢查開啟的連接埠</span><span class="sxs-lookup"><span data-stu-id="57145-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="57145-239">假設您懷疑連接嘗試由於連接埠問題而失敗。</span><span class="sxs-lookup"><span data-stu-id="57145-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="57145-240">在您的電腦上，您可以執行報告連接埠組態的公用程式。</span><span class="sxs-lookup"><span data-stu-id="57145-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="57145-241">下列公用程式在 Linux 上可能很有用：</span><span class="sxs-lookup"><span data-stu-id="57145-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="57145-242">(將範例值變更為您的 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="57145-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="57145-243">在 Windows 上， [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) 公用程式可能很有用。</span><span class="sxs-lookup"><span data-stu-id="57145-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="57145-244">以下是在 Azure SQL Database 伺服器上查詢連接埠情況，以及在膝上型電腦上執行的的範例執行：</span><span class="sxs-lookup"><span data-stu-id="57145-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="57145-245">診斷：記錄您的錯誤</span><span class="sxs-lookup"><span data-stu-id="57145-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="57145-246">有時診斷間歇問題的最好方式，就是數天或數週偵測一般模式。</span><span class="sxs-lookup"><span data-stu-id="57145-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="57145-247">您的用戶端可以記錄其遇到的所有錯誤來協助診斷。</span><span class="sxs-lookup"><span data-stu-id="57145-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="57145-248">您可以使記錄項目與 Azure SQL Database 本身內部記錄的錯誤資料相互關聯。</span><span class="sxs-lookup"><span data-stu-id="57145-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="57145-249">Enterprise Library 6 (EntLib60) 提供 .NET Managed 類別來協助記錄：</span><span class="sxs-lookup"><span data-stu-id="57145-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="57145-250">5 - 輕而易舉：使用記錄應用程式區塊</span><span class="sxs-lookup"><span data-stu-id="57145-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="57145-251">診斷：檢查系統記錄找出錯誤</span><span class="sxs-lookup"><span data-stu-id="57145-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="57145-252">以下是一些查詢錯誤記錄和其他資訊的 Transact-SQL SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="57145-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="57145-253">記錄查詢</span><span class="sxs-lookup"><span data-stu-id="57145-253">Query of log</span></span> | <span data-ttu-id="57145-254">說明</span><span class="sxs-lookup"><span data-stu-id="57145-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="57145-255">[Sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) 檢視提供個別的事件的資訊，包括會導致暫時性錯誤或連線失敗的某些事件。</span><span class="sxs-lookup"><span data-stu-id="57145-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="57145-256">在理想情況下您可以相互關聯 **start_time** 或 **end_time** 值，與您的用戶端程式發生問題時的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="57145-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="57145-257">**提示︰**您必須連接到 **master** 資料庫來執行此程序。</span><span class="sxs-lookup"><span data-stu-id="57145-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="57145-258">[Sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) 檢視針對其他診斷提供事件類型的彙總計數。</span><span class="sxs-lookup"><span data-stu-id="57145-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="57145-259">**提示︰**您必須連接到 **master** 資料庫來執行此程序。</span><span class="sxs-lookup"><span data-stu-id="57145-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="57145-260">診斷：在 SQL Database 記錄中搜尋問題事件</span><span class="sxs-lookup"><span data-stu-id="57145-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="57145-261">您可以在 Azure SQL Database 的記錄中搜尋有關問題事件的項目。</span><span class="sxs-lookup"><span data-stu-id="57145-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="57145-262">在 **master** 資料庫中嘗試下列 Transact-SQL SELECT 陳述式：</span><span class="sxs-lookup"><span data-stu-id="57145-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="57145-263">數個從 sys.fn_xe_telemetry_blob_target_read_file 傳回的資料列</span><span class="sxs-lookup"><span data-stu-id="57145-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="57145-264">接下來是傳回的資料列可能的樣子。</span><span class="sxs-lookup"><span data-stu-id="57145-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="57145-265">顯示的 null 值通常在其他資料列不是 null。</span><span class="sxs-lookup"><span data-stu-id="57145-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="57145-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="57145-266">Enterprise Library 6</span></span>
<span data-ttu-id="57145-267">Enterprise Library 6 (EntLib60) 是 .NET 類別的架構，可協助您實作雲端服務的健全用戶端，其中之一就是 Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="57145-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="57145-268">您可以先造訪下列網址來找出 EntLib60 所能協助之每個領域的專用主題：</span><span class="sxs-lookup"><span data-stu-id="57145-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="57145-269">Enterprise Library 6 - 2013 年 4 月</span><span class="sxs-lookup"><span data-stu-id="57145-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="57145-270">在 EntLib60 可以協助的一個領域中用於處理暫時性錯誤的重試邏輯：</span><span class="sxs-lookup"><span data-stu-id="57145-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="57145-271">4 - 堅持是所有成功的秘方：使用暫時性錯誤處理應用程式區塊</span><span class="sxs-lookup"><span data-stu-id="57145-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="57145-272">EntLib60 的原始程式碼已可公開 [下載](http://go.microsoft.com/fwlink/p/?LinkID=290898)。</span><span class="sxs-lookup"><span data-stu-id="57145-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="57145-273">Microsoft 沒有計劃進一步更新或維護 EntLib 的功能。</span><span class="sxs-lookup"><span data-stu-id="57145-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="57145-274">用於暫時性錯誤和重試的 EntLib60 類別</span><span class="sxs-lookup"><span data-stu-id="57145-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="57145-275">下列 EntLib60 類別特別有助於重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="57145-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="57145-276">這些全部都在命名空間 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** 中，或進一步位於其下：</span><span class="sxs-lookup"><span data-stu-id="57145-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="57145-277">*在命名空間 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**中：*</span><span class="sxs-lookup"><span data-stu-id="57145-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="57145-278">**RetryPolicy** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="57145-279">**ExecuteAction** 方法</span><span class="sxs-lookup"><span data-stu-id="57145-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="57145-280">**ExponentialBackoff** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="57145-281">**SqlDatabaseTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="57145-282">**ReliableSqlConnection** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="57145-283">**ExecuteCommand** 方法</span><span class="sxs-lookup"><span data-stu-id="57145-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="57145-284">在命名空間 **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**中：</span><span class="sxs-lookup"><span data-stu-id="57145-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="57145-285">**AlwaysTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="57145-286">**NeverTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="57145-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="57145-287">以下是 EntLib60 相關資訊的連結：</span><span class="sxs-lookup"><span data-stu-id="57145-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="57145-288">免費的 [書籍下載：Microsoft Enterprise Library 開發人員指南第 2 版](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="57145-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="57145-289">最佳作法： [重試一般指引](../best-practices-retry-general.md) 深入探討重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="57145-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="57145-290">可在 NuGet 下載 [Enterprise Library - 暫時性錯誤處理應用程式區塊 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="57145-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="57145-291">EntLib60：記錄區塊</span><span class="sxs-lookup"><span data-stu-id="57145-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="57145-292">記錄區塊是高度彈性且可設定的解決方案，可讓您：</span><span class="sxs-lookup"><span data-stu-id="57145-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="57145-293">建立記錄訊息，並儲存在各種不同的位置中。</span><span class="sxs-lookup"><span data-stu-id="57145-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="57145-294">分類與篩選訊息。</span><span class="sxs-lookup"><span data-stu-id="57145-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="57145-295">收集有助於偵錯和追蹤的內容資訊，以及用於稽核和一般記錄需求的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="57145-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="57145-296">記錄區塊可彙總來自記錄目的地的記錄功能，使應用程式程式碼能夠一致，而不必理會目標記錄存放區的的位置和類型。</span><span class="sxs-lookup"><span data-stu-id="57145-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="57145-297">如需詳細資料，請參閱： [5 - 輕而易舉：使用記錄應用程式區塊](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="57145-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="57145-298">EntLib60 IsTransient 方法的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="57145-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="57145-299">接下來，**IsTransient** 方法的 C# 原始程式碼來自 **SqlDatabaseTransientErrorDetectionStrategy** 類別。</span><span class="sxs-lookup"><span data-stu-id="57145-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="57145-300">原始程式碼將釐清哪些錯誤會被視為暫時性並值得重試 (從 2013 年 4 月起)。</span><span class="sxs-lookup"><span data-stu-id="57145-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="57145-301">為了強調可讀性，已從此副本移除許多 **//comment** 行。</span><span class="sxs-lookup"><span data-stu-id="57145-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // The instance of SQL Server you attempted to connect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="57145-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57145-302">Next steps</span></span>
* <span data-ttu-id="57145-303">如需針對其他常見的 Azure SQL Database 連接問題進行疑難排解，請造訪 [針對 Azure SQL Database 連線問題進行疑難排解](sql-database-troubleshoot-common-connection-issues.md)。</span><span class="sxs-lookup"><span data-stu-id="57145-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="57145-304">SQL Server 連接集區 (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="57145-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="57145-305">重試是 Apache 2.0 授權的一般用途重試文件庫，以 **Python** 撰寫，幾乎可對任何案例加入重試作業。</span><span class="sxs-lookup"><span data-stu-id="57145-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

