---
title: "aaaFix SQL 連線錯誤，暫時性錯誤 |Microsoft 文件"
description: "了解 tootroubleshoot、 診斷及避免 SQL 連接錯誤，或是 Azure SQL Database 中的暫時性錯誤的方式。 "
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
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="59b6d-104">排解、診斷和防止 SQL Database 的 SQL 連接錯誤和暫時性錯誤</span><span class="sxs-lookup"><span data-stu-id="59b6d-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="59b6d-105">本文說明 tooprevent、 疑難排解、 診斷和減少連接錯誤及用戶端應用程式在它與 Azure SQL Database 互動時所發生的暫時性錯誤的方式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="59b6d-106">了解 tooconfigure 如何重試邏輯，建立 hello 連接字串，以及調整其他連線設定。</span><span class="sxs-lookup"><span data-stu-id="59b6d-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="59b6d-107">暫時性錯誤 (暫時性故障)</span><span class="sxs-lookup"><span data-stu-id="59b6d-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="59b6d-108">暫時性錯誤 (又稱暫時性故障) 具有很快就會自行解決的根本原因。</span><span class="sxs-lookup"><span data-stu-id="59b6d-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="59b6d-109">暫時性錯誤的可能偶爾的原因是 hello Azure 系統快速切換硬體資源 toobetter 負載平衡各種工作負載時。</span><span class="sxs-lookup"><span data-stu-id="59b6d-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="59b6d-110">其中大部分重新設定事件通常會在不到 60 秒內完成。</span><span class="sxs-lookup"><span data-stu-id="59b6d-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="59b6d-111">在此重新設定時間範圍內，您可能有連線問題 tooAzure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="59b6d-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="59b6d-112">建立應用程式連接 SQL 資料庫應位於的 tooAzure tooexpect 這些暫時性錯誤，其藉由實作重試邏輯，而不是面對它們做為應用程式錯誤 toousers 標定程式碼中的控制代碼。</span><span class="sxs-lookup"><span data-stu-id="59b6d-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="59b6d-113">如果您的用戶端程式使用 ADO.NET，程式就會通知有關 hello 暫時性錯誤 hello 擲回由**SqlException**。</span><span class="sxs-lookup"><span data-stu-id="59b6d-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="59b6d-114">hello**數目**屬性可以針對 hello hello hello 主題頂端附近的暫時性錯誤清單進行比較： [SQL 資料庫用戶端應用程式的 SQL 錯誤代碼，](sql-database-develop-error-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="59b6d-115">連接與命令</span><span class="sxs-lookup"><span data-stu-id="59b6d-115">Connection versus command</span></span>
<span data-ttu-id="59b6d-116">您將 hello SQL 連接重試一次或一次，根據 hello 下列建立：</span><span class="sxs-lookup"><span data-stu-id="59b6d-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="59b6d-117">**連接嘗試期間，發生暫時性錯誤**: hello 連接應該重試後幾秒鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="59b6d-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="59b6d-118">**SQL 查詢命令期間，發生暫時性錯誤**: hello 命令應該不會立即重試。</span><span class="sxs-lookup"><span data-stu-id="59b6d-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="59b6d-119">相反地的延遲之後，hello 應該重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="59b6d-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="59b6d-120">然後可以重試 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="59b6d-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="59b6d-121">暫時性錯誤的重試邏輯</span><span class="sxs-lookup"><span data-stu-id="59b6d-121">Retry logic for transient errors</span></span>
<span data-ttu-id="59b6d-122">用戶端程式若包含重試邏輯，在偶爾遇到暫時性錯誤時就會更可靠。</span><span class="sxs-lookup"><span data-stu-id="59b6d-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="59b6d-123">您的程式通訊時使用 Azure SQL Database 透過第 3 個合作對象的中介軟體，查詢與 hello 廠商是否 hello 中介軟體中包含的暫時性錯誤重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="59b6d-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="59b6d-124">重試原則</span><span class="sxs-lookup"><span data-stu-id="59b6d-124">Principles for retry</span></span>
* <span data-ttu-id="59b6d-125">如果 hello 錯誤是暫時性，應該重試嘗試 tooopen 連接。</span><span class="sxs-lookup"><span data-stu-id="59b6d-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="59b6d-126">不應該直接重試由於暫時性錯誤而失敗的 SQL SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="59b6d-127">相反地，建立全新的連線，然後再重試 hello 選取。</span><span class="sxs-lookup"><span data-stu-id="59b6d-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="59b6d-128">當 SQL UPDATE 陳述式失敗，發生暫時性的錯誤時，應該在重試更新的 hello 之前先建立全新的連接。</span><span class="sxs-lookup"><span data-stu-id="59b6d-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="59b6d-129">hello 重試邏輯必須確保 hello 整個資料庫的交易完成或該 hello 整個異動會復原。</span><span class="sxs-lookup"><span data-stu-id="59b6d-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="59b6d-130">其他重試考量</span><span class="sxs-lookup"><span data-stu-id="59b6d-130">Other considerations for retry</span></span>
* <span data-ttu-id="59b6d-131">批次程式上班時間之後自動啟動的且它會先完成早上，能夠負擔 toovery 病患和長時間間隔之間的重試次數。</span><span class="sxs-lookup"><span data-stu-id="59b6d-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="59b6d-132">使用者介面程式應該考量 hello 傾向 toogive 向上之後等候太長。</span><span class="sxs-lookup"><span data-stu-id="59b6d-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="59b6d-133">不過，hello 方案不能 tooretry 每幾秒鐘，因為該原則可以填滿 hello 系統的要求。</span><span class="sxs-lookup"><span data-stu-id="59b6d-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="59b6d-134">增加重試之間的間隔</span><span class="sxs-lookup"><span data-stu-id="59b6d-134">Interval increase between retries</span></span>
<span data-ttu-id="59b6d-135">我們建議您在您第一次重試前延遲 5 秒鐘。</span><span class="sxs-lookup"><span data-stu-id="59b6d-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="59b6d-136">少於 5 秒的延遲之後重試風險非常龐大的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="59b6d-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="59b6d-137">每個後續的重試 hello 延遲應該指數成長，向上 tooa 60 秒的最大值。</span><span class="sxs-lookup"><span data-stu-id="59b6d-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="59b6d-138">討論的 hello*封鎖期間*使用 ADO.NET 的用戶端會提供[SQL Server 連接共用 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="59b6d-139">Hello 程式自我終止之前，您可能也想 tooset 重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="59b6d-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="59b6d-140">具有重試邏輯的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="59b6d-140">Code samples with retry logic</span></span>
<span data-ttu-id="59b6d-141">各種程式設計語言中具有重試邏輯的程式碼範例位於：</span><span class="sxs-lookup"><span data-stu-id="59b6d-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="59b6d-142">SQL Database 和 SQL Server 的連線庫</span><span class="sxs-lookup"><span data-stu-id="59b6d-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="59b6d-143">測試您的重試邏輯</span><span class="sxs-lookup"><span data-stu-id="59b6d-143">Test your retry logic</span></span>
<span data-ttu-id="59b6d-144">tootest 重試邏輯，您必須模擬或非可以更正錯誤，您的程式仍在執行時，會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="59b6d-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="59b6d-145">測試 hello 網路連線中斷</span><span class="sxs-lookup"><span data-stu-id="59b6d-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="59b6d-146">您可以測試重試邏輯的一個方式是的 toodisconnect hello 程式執行時，用戶端電腦從 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="59b6d-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="59b6d-147">hello 錯誤為：</span><span class="sxs-lookup"><span data-stu-id="59b6d-147">hello error will be:</span></span>

* <span data-ttu-id="59b6d-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="59b6d-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="59b6d-149">訊息：「未知的主機」</span><span class="sxs-lookup"><span data-stu-id="59b6d-149">Message: "No such host is known"</span></span>

<span data-ttu-id="59b6d-150">Hello 一部分第一次重試嘗試，因為您的程式就可以修正 hello 拼字錯誤，，，然後嘗試 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="59b6d-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="59b6d-151">這個實用 toomake 您拔下從 hello 網路電腦之前啟動您的程式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="59b6d-152">然後您的程式會辨識造成 hello 程式的執行的階段參數：</span><span class="sxs-lookup"><span data-stu-id="59b6d-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="59b6d-153">暫時將錯誤 tooconsider 11001 tooits 清單新增為暫時性。</span><span class="sxs-lookup"><span data-stu-id="59b6d-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="59b6d-154">如往常般嘗試其第一個連接。</span><span class="sxs-lookup"><span data-stu-id="59b6d-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="59b6d-155">會攔截 hello 錯誤之後，請從 hello 清單移除 11001。</span><span class="sxs-lookup"><span data-stu-id="59b6d-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="59b6d-156">顯示一則訊息告訴 hello 使用者 tooplug hello 電腦進入 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="59b6d-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="59b6d-157">使用任一個 hello 暫停進一步執行**Console.ReadLine**方法或具有 [確定] 按鈕的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="59b6d-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="59b6d-158">hello 電腦插入 hello 網路之後，hello 使用者按下 hello Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="59b6d-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="59b6d-159">嘗試再次 tooconnect，必須成功。</span><span class="sxs-lookup"><span data-stu-id="59b6d-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="59b6d-160">連線時以測試拼字錯誤 hello 資料庫名稱</span><span class="sxs-lookup"><span data-stu-id="59b6d-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="59b6d-161">您的程式可以刻意拼錯 hello hello 第一次連接嘗試之前的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="59b6d-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="59b6d-162">hello 錯誤為：</span><span class="sxs-lookup"><span data-stu-id="59b6d-162">hello error will be:</span></span>

* <span data-ttu-id="59b6d-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="59b6d-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="59b6d-164">錯誤將為：「使用者 'WRONG_MyUserName' 登入失敗。」</span><span class="sxs-lookup"><span data-stu-id="59b6d-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="59b6d-165">Hello 一部分第一次重試嘗試，因為您的程式就可以修正 hello 拼字錯誤，，，然後嘗試 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="59b6d-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="59b6d-166">這個實用 toomake，您的程式無法辨識造成 hello 程式的執行的階段參數：</span><span class="sxs-lookup"><span data-stu-id="59b6d-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="59b6d-167">暫時將錯誤 tooconsider 18456 tooits 清單新增為暫時性。</span><span class="sxs-lookup"><span data-stu-id="59b6d-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="59b6d-168">刻意新增 'WRONG_' toohello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="59b6d-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="59b6d-169">會攔截 hello 錯誤之後，請從 hello 清單移除 18456。</span><span class="sxs-lookup"><span data-stu-id="59b6d-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="59b6d-170">請移除 'WRONG_' hello 使用者名稱中。</span><span class="sxs-lookup"><span data-stu-id="59b6d-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="59b6d-171">嘗試再次 tooconnect，必須成功。</span><span class="sxs-lookup"><span data-stu-id="59b6d-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="59b6d-172">進行連線重試的.NET SqlConnection 參數</span><span class="sxs-lookup"><span data-stu-id="59b6d-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="59b6d-173">如果用戶端程式 tootooAzure SQL Database 會使用連接 hello.NET Framework 類別**System.Data.SqlClient.SqlConnection**，您應該使用.NET 4.6.1 或更新版本 （或.NET Core） 讓您可以利用其連接重試功能。</span><span class="sxs-lookup"><span data-stu-id="59b6d-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="59b6d-174">Hello 功能的詳細資料會[這裡](http://go.microsoft.com/fwlink/?linkid=393996)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="59b6d-175">當您建置 hello[連接字串](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx)如您**SqlConnection**物件，您應該協調 hello 值之間 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="59b6d-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="59b6d-176">ConnectRetryCount &nbsp;&nbsp;*(預設值為 1。範圍是 0 到 255)。*</span><span class="sxs-lookup"><span data-stu-id="59b6d-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="59b6d-177">ConnectRetryInterval &nbsp;&nbsp;*(預設值為 1 秒。範圍是 1 到 60)。*</span><span class="sxs-lookup"><span data-stu-id="59b6d-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="59b6d-178">Connection Timeout &nbsp;&nbsp;*(預設值為 15 秒。範圍是 0 到 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="59b6d-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="59b6d-179">具體來說，您所選擇的值應該做下列等號比較為 true 的 hello:</span><span class="sxs-lookup"><span data-stu-id="59b6d-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="59b6d-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="59b6d-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="59b6d-181">例如，如果 hello 計數 = 3，且間隔 = 10 秒，逾時，只有 29 秒可能不完全賦予 hello 系統足夠的時間進行連線時的第 3 個和最後一個重試： 29 < 3 * 10。</span><span class="sxs-lookup"><span data-stu-id="59b6d-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="59b6d-182">連接與命令</span><span class="sxs-lookup"><span data-stu-id="59b6d-182">Connection versus command</span></span>
<span data-ttu-id="59b6d-183">hello **ConnectRetryCount**和**ConnectRetryInterval**參數可讓您**SqlConnection**物件重試 hello 連線作業而不需要通知或終究您程式，例如傳回 tooyour 控制程式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="59b6d-184">hello 重試可能會發生下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="59b6d-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="59b6d-185">mySqlConnection.Open 方法呼叫</span><span class="sxs-lookup"><span data-stu-id="59b6d-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="59b6d-186">mySqlConnection.Execute 方法呼叫</span><span class="sxs-lookup"><span data-stu-id="59b6d-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="59b6d-187">有一些微妙的差異。</span><span class="sxs-lookup"><span data-stu-id="59b6d-187">There is a subtlety.</span></span> <span data-ttu-id="59b6d-188">如果發生暫時性錯誤時您*查詢*正在執行，您**SqlConnection**物件不重試 hello 是否連接作業，與它一定不會重試您的查詢。</span><span class="sxs-lookup"><span data-stu-id="59b6d-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="59b6d-189">不過， **SqlConnection**非常快速地檢查 hello 傳送您的查詢執行之前的連接。</span><span class="sxs-lookup"><span data-stu-id="59b6d-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="59b6d-190">如果 hello 快速檢查偵測到的連線問題， **SqlConnection**重試 hello 連接作業。</span><span class="sxs-lookup"><span data-stu-id="59b6d-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="59b6d-191">如果 hello 重試成功，您的查詢會傳送給執行中。</span><span class="sxs-lookup"><span data-stu-id="59b6d-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="59b6d-192">是否應該將 ConnectRetryCount 與應用程式重試邏輯結合？</span><span class="sxs-lookup"><span data-stu-id="59b6d-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="59b6d-193">假設您的應用程式有健全的自訂重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="59b6d-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="59b6d-194">它可能會重試 hello 4 次的連線作業。</span><span class="sxs-lookup"><span data-stu-id="59b6d-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="59b6d-195">如果您將加入**ConnectRetryInterval**和**ConnectRetryCount** = 3 tooyour 連接字串中，您會增加 hello 重試計數 too4 * 3 = 12 重試。</span><span class="sxs-lookup"><span data-stu-id="59b6d-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="59b6d-196">您可能不會想要這麼多的重試次數。</span><span class="sxs-lookup"><span data-stu-id="59b6d-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="59b6d-197">連線 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="59b6d-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="59b6d-198">連接：連接字串</span><span class="sxs-lookup"><span data-stu-id="59b6d-198">Connection: Connection string</span></span>
<span data-ttu-id="59b6d-199">hello 連接字串連接 tooAzure 需要 SQL Database 是從連接 SQL Server tooMicrosoft hello 字串稍有不同。</span><span class="sxs-lookup"><span data-stu-id="59b6d-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="59b6d-200">您可以為您的資料庫複製 hello 連接字串從 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="59b6d-201">連接：IP 位址</span><span class="sxs-lookup"><span data-stu-id="59b6d-201">Connection: IP address</span></span>
<span data-ttu-id="59b6d-202">您必須設定 hello SQL Database 伺服器 tooaccept 通訊 hello IP 位址從 hello 裝載電腦的用戶端程式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="59b6d-203">您可以編輯 hello 防火牆設定，透過 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="59b6d-204">如果您忘記 tooconfigure hello IP 位址，您的程式會失敗並方便的錯誤訊息，指出 hello 所需的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="59b6d-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="59b6d-205">如需詳細資訊，請參閱： [作法：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="59b6d-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="59b6d-206">連接：連接埠</span><span class="sxs-lookup"><span data-stu-id="59b6d-206">Connection: Ports</span></span>
<span data-ttu-id="59b6d-207">通常您只需要 tooensure 通訊埠 1433年是供 hello 裝載您的用戶端程式的電腦上的連出通訊開啟。</span><span class="sxs-lookup"><span data-stu-id="59b6d-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="59b6d-208">例如，若當用戶端程式裝載在 Windows 電腦上，hello 主機上的 Windows 防火牆 hello 可讓您 tooopen 通訊埠 1433年:</span><span class="sxs-lookup"><span data-stu-id="59b6d-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="59b6d-209">開啟控制台 hello</span><span class="sxs-lookup"><span data-stu-id="59b6d-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="59b6d-210">&gt;所有控制台項目</span><span class="sxs-lookup"><span data-stu-id="59b6d-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="59b6d-211">&gt;Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="59b6d-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="59b6d-212">&gt;進階設定</span><span class="sxs-lookup"><span data-stu-id="59b6d-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="59b6d-213">&gt; 輸出規則</span><span class="sxs-lookup"><span data-stu-id="59b6d-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="59b6d-214">&gt;動作</span><span class="sxs-lookup"><span data-stu-id="59b6d-214">&gt; Actions</span></span>
7. <span data-ttu-id="59b6d-215">&gt;新增規則</span><span class="sxs-lookup"><span data-stu-id="59b6d-215">&gt; New Rule</span></span>

<span data-ttu-id="59b6d-216">如果您的用戶端程式裝載在 Azure 虛擬機器 (VM) 上，您應該閱讀：</span><span class="sxs-lookup"><span data-stu-id="59b6d-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="59b6d-217">[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="59b6d-218">如需設定連接埠及 IP 位址的背景資訊，請參閱： [Azure SQL Database 防火牆](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="59b6d-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="59b6d-219">連接：ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="59b6d-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="59b6d-220">如果您的程式使用 ADO.NET 類別，例如**System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL 資料庫，建議您先使用.NET Framework 4.6.1 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="59b6d-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="59b6d-221">ADO.NET 4.6.1：</span><span class="sxs-lookup"><span data-stu-id="59b6d-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="59b6d-222">Azure SQL database，沒有可靠性當開啟連接時使用 hello **SqlConnection.Open**方法。</span><span class="sxs-lookup"><span data-stu-id="59b6d-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="59b6d-223">hello**開啟**方法現已加入最佳投入時間的重試機制回應 tootransient 錯誤中的 hello 連接逾時期間內的特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="59b6d-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="59b6d-224">支援連接共用。</span><span class="sxs-lookup"><span data-stu-id="59b6d-224">Supports connection pooling.</span></span> <span data-ttu-id="59b6d-225">這包括 hello 連接有效驗證物件，它可讓您的程式是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="59b6d-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="59b6d-226">當您從連接集區使用的連接物件時，我們建議您的程式暫時關閉 hello 連線時不會立即使用它。</span><span class="sxs-lookup"><span data-stu-id="59b6d-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="59b6d-227">重新開啟連接不是高成本 hello 方法建立新的連接是。</span><span class="sxs-lookup"><span data-stu-id="59b6d-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="59b6d-228">如果您使用 ADO.NET 4.0 或更早版本，我們建議您升級 toohello 最新的 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="59b6d-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="59b6d-229">從 2015 年 11 月開始，您可以 [下載 ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="59b6d-230">診斷</span><span class="sxs-lookup"><span data-stu-id="59b6d-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="59b6d-231">診斷：測試公用程式是否可以連接</span><span class="sxs-lookup"><span data-stu-id="59b6d-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="59b6d-232">如果您的程式無法 tooconnect tooAzure SQL 資料庫，一個診斷的選項會是 tootry tooconnect 與公用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="59b6d-233">在理想情況下 hello 公用程式會使用連接 hello 程式所使用的相同文件庫。</span><span class="sxs-lookup"><span data-stu-id="59b6d-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="59b6d-234">您可以在任何 Windows 電腦上，嘗試這些公用程式：</span><span class="sxs-lookup"><span data-stu-id="59b6d-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="59b6d-235">SQL Server Management Studio (SSMS.exe)，連接時使用 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="59b6d-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="59b6d-236">sqlcmd.exe，連接時使用 [ODBC](http://msdn.microsoft.com/library/jj730308.aspx)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="59b6d-237">一旦完成連接，就會測試簡短的 SQL SELECT 查詢是否可以運作。</span><span class="sxs-lookup"><span data-stu-id="59b6d-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="59b6d-238">診斷： 檢查 hello 開放的連接埠</span><span class="sxs-lookup"><span data-stu-id="59b6d-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="59b6d-239">假設您懷疑連線嘗試會因為 tooport 問題失敗。</span><span class="sxs-lookup"><span data-stu-id="59b6d-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="59b6d-240">在您的電腦上，您可以執行報告的 hello 連接埠組態的公用程式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="59b6d-241">在 Linux hello 下列公用程式可能會很有幫助：</span><span class="sxs-lookup"><span data-stu-id="59b6d-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="59b6d-242">（變更 hello 範例值 toobe 您的 IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="59b6d-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="59b6d-243">在 Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148)公用程式可能會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="59b6d-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="59b6d-244">以下是範例執行的查詢 hello 連接埠的情況下於 Azure SQL Database 伺服器上，而且這已在膝上型電腦上執行：</span><span class="sxs-lookup"><span data-stu-id="59b6d-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="59b6d-245">診斷：記錄您的錯誤</span><span class="sxs-lookup"><span data-stu-id="59b6d-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="59b6d-246">有時診斷間歇問題的最好方式，就是數天或數週偵測一般模式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="59b6d-247">您的用戶端可以記錄其遇到的所有錯誤來協助診斷。</span><span class="sxs-lookup"><span data-stu-id="59b6d-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="59b6d-248">您可能會無法 toocorrelate hello 記錄項目，使用 Azure SQL 資料庫記錄檔本身內部的錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="59b6d-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="59b6d-249">Enterprise Library 6 (EntLib60) 提供.NET managed 類別 tooassist 記錄：</span><span class="sxs-lookup"><span data-stu-id="59b6d-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="59b6d-250">5-以輕鬆為下降關閉記錄： 使用 hello 記錄應用程式區塊</span><span class="sxs-lookup"><span data-stu-id="59b6d-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="59b6d-251">診斷：檢查系統記錄找出錯誤</span><span class="sxs-lookup"><span data-stu-id="59b6d-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="59b6d-252">以下是一些查詢錯誤記錄和其他資訊的 Transact-SQL SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="59b6d-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="59b6d-253">記錄查詢</span><span class="sxs-lookup"><span data-stu-id="59b6d-253">Query of log</span></span> | <span data-ttu-id="59b6d-254">說明</span><span class="sxs-lookup"><span data-stu-id="59b6d-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="59b6d-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx)檢視提供有關個別事件，包括某些可能會導致暫時性錯誤或連線失敗的資訊。</span><span class="sxs-lookup"><span data-stu-id="59b6d-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="59b6d-256">在理想情況下相互關聯 hello **start_time**或**end_time**當用戶端程式發生問題的相關資訊的值。</span><span class="sxs-lookup"><span data-stu-id="59b6d-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="59b6d-257">**提示：** ，您必須連接 toohello**主要**toorun 這的資料庫。</span><span class="sxs-lookup"><span data-stu-id="59b6d-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="59b6d-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx)檢視提供的事件類型，取得詳細診斷資訊彙總計的數。</span><span class="sxs-lookup"><span data-stu-id="59b6d-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="59b6d-259">**提示：** ，您必須連接 toohello**主要**toorun 這的資料庫。</span><span class="sxs-lookup"><span data-stu-id="59b6d-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="59b6d-260">診斷： 搜尋 hello SQL 資料庫記錄檔中的問題事件</span><span class="sxs-lookup"><span data-stu-id="59b6d-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="59b6d-261">您可以搜尋有關問題的事件，Azure SQL Database 的 hello 記錄檔中的項目。</span><span class="sxs-lookup"><span data-stu-id="59b6d-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="59b6d-262">再試一次下列 TRANSACT-SQL SELECT 陳述式中 hello hello**主要**資料庫：</span><span class="sxs-lookup"><span data-stu-id="59b6d-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="59b6d-263">數個從 sys.fn_xe_telemetry_blob_target_read_file 傳回的資料列</span><span class="sxs-lookup"><span data-stu-id="59b6d-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="59b6d-264">接下來是傳回的資料列可能的樣子。</span><span class="sxs-lookup"><span data-stu-id="59b6d-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="59b6d-265">顯示 hello null 值通常不是 null 的其他資料列中的。</span><span class="sxs-lookup"><span data-stu-id="59b6d-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="59b6d-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="59b6d-266">Enterprise Library 6</span></span>
<span data-ttu-id="59b6d-267">Enterprise Library 6 (EntLib60) 是的架構的.NET 類別，可協助您實作強固的用戶端的雲端服務，其中是 hello Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="59b6d-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="59b6d-268">您可以找到所在 EntLib60 可協助第一次瀏覽主題專用的 tooeach 區域：</span><span class="sxs-lookup"><span data-stu-id="59b6d-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="59b6d-269">Enterprise Library 6 - 2013 年 4 月</span><span class="sxs-lookup"><span data-stu-id="59b6d-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="59b6d-270">在 EntLib60 可以協助的一個領域中用於處理暫時性錯誤的重試邏輯：</span><span class="sxs-lookup"><span data-stu-id="59b6d-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="59b6d-271">4-堅持不懈、 密碼的所有勝利： 使用 hello 暫時性錯誤處理應用程式區塊</span><span class="sxs-lookup"><span data-stu-id="59b6d-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="59b6d-272">hello EntLib60 的原始程式碼可針對公用[下載](http://go.microsoft.com/fwlink/p/?LinkID=290898)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="59b6d-273">Microsoft 有無計劃 toomake 進一步功能更新或維護更新 tooEntLib。</span><span class="sxs-lookup"><span data-stu-id="59b6d-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="59b6d-274">用於暫時性錯誤和重試的 EntLib60 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="59b6d-275">hello 遵循 EntLib60 類別是適合用來重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="59b6d-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="59b6d-276">所有這些包括 in、 或，更進一步 hello 命名空間**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="59b6d-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="59b6d-277">*Hello 命名空間中**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="59b6d-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="59b6d-278">**RetryPolicy** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="59b6d-279">**ExecuteAction** 方法</span><span class="sxs-lookup"><span data-stu-id="59b6d-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="59b6d-280">**ExponentialBackoff** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="59b6d-281">**SqlDatabaseTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="59b6d-282">**ReliableSqlConnection** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="59b6d-283">**ExecuteCommand** 方法</span><span class="sxs-lookup"><span data-stu-id="59b6d-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="59b6d-284">Hello 命名空間中**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="59b6d-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="59b6d-285">**AlwaysTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="59b6d-286">**NeverTransientErrorDetectionStrategy** 類別</span><span class="sxs-lookup"><span data-stu-id="59b6d-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="59b6d-287">以下是連結 tooinformation EntLib60 相關：</span><span class="sxs-lookup"><span data-stu-id="59b6d-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="59b6d-288">免費[活頁簿下載： 開發人員指南 tooMicrosoft 企業程式庫中，第 2 版](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="59b6d-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="59b6d-289">最佳作法： [重試一般指引](../best-practices-retry-general.md) 深入探討重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="59b6d-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="59b6d-290">可在 NuGet 下載 [Enterprise Library - 暫時性錯誤處理應用程式區塊 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="59b6d-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="59b6d-291">EntLib60: hello 記錄區塊</span><span class="sxs-lookup"><span data-stu-id="59b6d-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="59b6d-292">hello 記錄區塊是高彈性和可設定的解決方案，可讓您：</span><span class="sxs-lookup"><span data-stu-id="59b6d-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="59b6d-293">建立記錄訊息，並儲存在各種不同的位置中。</span><span class="sxs-lookup"><span data-stu-id="59b6d-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="59b6d-294">分類與篩選訊息。</span><span class="sxs-lookup"><span data-stu-id="59b6d-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="59b6d-295">收集有助於偵錯和追蹤的內容資訊，以及用於稽核和一般記錄需求的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="59b6d-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="59b6d-296">hello 記錄區塊會擷取 hello hello 記錄目的地從記錄功能，使 hello 應用程式程式碼會一致，無論 hello 位置和類型的 hello 目標記錄存放區。</span><span class="sxs-lookup"><span data-stu-id="59b6d-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="59b6d-297">如需詳細資訊，請參閱： [5-以輕鬆為落關閉記錄： 使用 hello 記錄應用程式區塊](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="59b6d-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="59b6d-298">EntLib60 IsTransient 方法的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="59b6d-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="59b6d-299">接下來，從 hello **SqlDatabaseTransientErrorDetectionStrategy**類別，是 hello hello C# 原始程式碼**IsTransient**方法。</span><span class="sxs-lookup"><span data-stu-id="59b6d-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="59b6d-300">hello 原始程式碼將釐清哪些錯誤 toobe 暫時性和重試 」，於 2013 年 4 月的考量。</span><span class="sxs-lookup"><span data-stu-id="59b6d-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="59b6d-301">許多**//comment**行已從這個複製 tooemphasize 可讀性。</span><span class="sxs-lookup"><span data-stu-id="59b6d-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
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
            // hello instance of SQL Server you attempted tooconnect to
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


## <a name="next-steps"></a><span data-ttu-id="59b6d-302">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59b6d-302">Next steps</span></span>
* <span data-ttu-id="59b6d-303">如需疑難排解其他常見的 Azure SQL Database 連線問題，請瀏覽[疑難排解連接問題 tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md)。</span><span class="sxs-lookup"><span data-stu-id="59b6d-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="59b6d-304">SQL Server 連接集區 (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="59b6d-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="59b6d-305">*正在重試*是一般用途的重試一次程式庫，以撰寫的 Apache 2.0 授權**Python**，新增任何項目有關的重試行為 toojust toosimplify hello 工作。</span><span class="sxs-lookup"><span data-stu-id="59b6d-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

