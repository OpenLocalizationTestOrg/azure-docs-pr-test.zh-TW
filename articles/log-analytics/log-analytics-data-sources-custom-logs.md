---
title: "在 OMS Log Analytics 中收集自訂記錄 | Microsoft Docs"
description: "Log Analytics 可從 Windows 和 Linux 電腦上的文字檔收集事件。  本文說明如何定義新的自訂記錄檔，以及它們在 OMS 儲存機制中建立的記錄詳細資料。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: b7f28868e3ffdf95dbe39872f382e7c97eae692c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="custom-logs-in-log-analytics"></a><span data-ttu-id="f8308-104">Log Analytics 中的自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-104">Custom logs in Log Analytics</span></span>
<span data-ttu-id="f8308-105">Log Analytics 中的「自訂記錄檔」資料來源可讓您從 Windows 和 Linux 電腦上的文字檔案收集事件。</span><span class="sxs-lookup"><span data-stu-id="f8308-105">The Custom Logs data source in Log Analytics allows you to collect events from text files on both Windows and Linux computers.</span></span> <span data-ttu-id="f8308-106">許多應用程式會將資訊記錄到文字檔而非標準的記錄服務，例如 Windows 事件記錄檔或 Syslog。</span><span class="sxs-lookup"><span data-stu-id="f8308-106">Many applications log information to text files instead of standard logging services such as Windows Event log or Syslog.</span></span>  <span data-ttu-id="f8308-107">在收集之後，您就可以使用 Log Analytics 的[自訂欄位](log-analytics-custom-fields.md)功能將記錄中的每一筆記錄剖析成個別欄位。</span><span class="sxs-lookup"><span data-stu-id="f8308-107">Once collected, you can parse each record in the log in to individual fields using the [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

![自訂記錄檔收集](media/log-analytics-data-sources-custom-logs/overview.png)

<span data-ttu-id="f8308-109">要收集的記錄檔必須符合下列準則。</span><span class="sxs-lookup"><span data-stu-id="f8308-109">The log files to be collected must match the following criteria.</span></span>

- <span data-ttu-id="f8308-110">記錄檔必須是每行一個項目，或在每個項目開頭使用符合下列其中一種格式的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="f8308-110">The log must either have a single entry per line or use a timestamp matching one of the following formats at the start of each entry.</span></span>

    <span data-ttu-id="f8308-111">YYYY-MM-DD HH:MM:SS </span><span class="sxs-lookup"><span data-stu-id="f8308-111">YYYY-MM-DD HH:MM:SS</span></span><br><span data-ttu-id="f8308-112">M/D/YYYY HH:MM:SS AM/PM</span><span class="sxs-lookup"><span data-stu-id="f8308-112">M/D/YYYY HH:MM:SS AM/PM</span></span> <br><span data-ttu-id="f8308-113">Mon DD,YYYY HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="f8308-113">Mon DD,YYYY HH:MM:SS</span></span>

- <span data-ttu-id="f8308-114">記錄檔不得使用會以新的項目覆寫檔案的循環更新。</span><span class="sxs-lookup"><span data-stu-id="f8308-114">The log file must not allow circular updates where the file is overwritten with new entries.</span></span>
- <span data-ttu-id="f8308-115">記錄檔必須使用 ASCII 或 UTF-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="f8308-115">The log file must use ASCII or UTF-8 encoding.</span></span>  <span data-ttu-id="f8308-116">不支援其他格式，例如 UTF-16。</span><span class="sxs-lookup"><span data-stu-id="f8308-116">Other formats such as UTF-16 are not supported.</span></span>

>[!NOTE]
><span data-ttu-id="f8308-117">如果記錄檔中有重複的項目，Log Analytics 會收集這些項目。</span><span class="sxs-lookup"><span data-stu-id="f8308-117">If there are duplicate entries in the log file, Log Analytics will collect them.</span></span>  <span data-ttu-id="f8308-118">不過，搜尋結果會不一致，篩選結果所顯示的事件會比結果計數更多。</span><span class="sxs-lookup"><span data-stu-id="f8308-118">However, the search results will be inconsistent where the filter results show more events than the result count.</span></span>  <span data-ttu-id="f8308-119">您必須驗證記錄，以判定建立該記錄的應用程式是否導致此行為，若可以的話，請先處理此問題，再建立自訂記錄集合定義。</span><span class="sxs-lookup"><span data-stu-id="f8308-119">It will be important that you validate the log to determine if the application that creates it is causing this behavior and address it if possible before creating the custom log collection definition.</span></span>  
>
  
## <a name="defining-a-custom-log"></a><span data-ttu-id="f8308-120">定義自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-120">Defining a custom log</span></span>
<span data-ttu-id="f8308-121">使用下列程序來定義自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-121">Use the following procedure to define a custom log file.</span></span>  <span data-ttu-id="f8308-122">如需新增自訂記錄檔之範例的逐步解說，請捲動到本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="f8308-122">Scroll to the end of this article for a walkthrough of a sample of adding a custom log.</span></span>

### <a name="step-1-open-the-custom-log-wizard"></a><span data-ttu-id="f8308-123">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="f8308-123">Step 1.</span></span> <span data-ttu-id="f8308-124">開啟自訂記錄檔精靈</span><span class="sxs-lookup"><span data-stu-id="f8308-124">Open the Custom Log Wizard</span></span>
<span data-ttu-id="f8308-125">自訂記錄檔精靈會在 OMS 入口網站中執行，並可讓您定義要收集的新自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-125">The Custom Log Wizard runs in the OMS portal and allows you to define a new custom log to collect.</span></span>

1. <span data-ttu-id="f8308-126">在 OMS 入口網站中，移至 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f8308-126">In the OMS portal, go to **Settings**.</span></span>
2. <span data-ttu-id="f8308-127">按一下 [資料]，然後按一下 [自訂記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="f8308-127">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="f8308-128">根據預設，所有設定變更都會自動發送給所有代理程式。</span><span class="sxs-lookup"><span data-stu-id="f8308-128">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="f8308-129">若是 Linux 代理程式，組態檔會傳送給 Fluentd 資料收集器。</span><span class="sxs-lookup"><span data-stu-id="f8308-129">For Linux agents, a configuration file is sent to the Fluentd data collector.</span></span>  <span data-ttu-id="f8308-130">如果您想以手動方式在每個 Linux 代理程式上修改這個檔案，只要取消核取 *[Apply below configuration to my Linux machines]* \(將下列設定套用至我的 Linux 機器) 方塊即可。</span><span class="sxs-lookup"><span data-stu-id="f8308-130">If you wish to modify this file manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>
4. <span data-ttu-id="f8308-131">按一下 [新增+]  開啟自訂記錄檔精靈。</span><span class="sxs-lookup"><span data-stu-id="f8308-131">Click **Add+** to open the Custom Log Wizard.</span></span>

### <a name="step-2-upload-and-parse-a-sample-log"></a><span data-ttu-id="f8308-132">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="f8308-132">Step 2.</span></span> <span data-ttu-id="f8308-133">上傳和剖析範例記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-133">Upload and parse a sample log</span></span>
<span data-ttu-id="f8308-134">一開始您要上傳自訂記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="f8308-134">You start by uploading a sample of the custom log.</span></span>  <span data-ttu-id="f8308-135">精靈會剖析並顯示此檔案中的項目以供您驗證。</span><span class="sxs-lookup"><span data-stu-id="f8308-135">The wizard will parse and display the entries in this file for you to validate.</span></span>  <span data-ttu-id="f8308-136">Log Analytics 會使用您指定的分隔符號來識別每一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="f8308-136">Log Analytics will use the delimiter that you specify to identify each record.</span></span>

<span data-ttu-id="f8308-137">**新行字元** 是預設的分隔符號，並且會用於每行一個項目的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-137">**New Line** is the default delimiter and is used for log files that have a single entry per line.</span></span>  <span data-ttu-id="f8308-138">如果一行的開頭是其中一種可用格式的日期和時間，則您可以指定 **時間戳記** 分隔符號，其可支援跨越多行的多個項目。</span><span class="sxs-lookup"><span data-stu-id="f8308-138">If the line starts with a date and time in one of the available formats, then you can specify a **Timestamp** delimiter which supports entries that span more than one line.</span></span>

<span data-ttu-id="f8308-139">如果使用時間戳記分隔符號，則儲存在 OMS 中的每一筆記錄的 TimeGenerated 屬性會填入針對記錄檔中的該項目指定的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="f8308-139">If a timestamp delimiter is used, then the TimeGenerated property of each record stored in OMS will be populated with the date/time specified for that entry in the log file.</span></span>  <span data-ttu-id="f8308-140">如果使用新行字元分隔符號，則 TimeGenerated 會填入 Log Analytics 收集項目時的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f8308-140">If a new line delimiter is used, then TimeGenerated is populated with date and time that Log Analytics collected the entry.</span></span>

> [!NOTE]
> <span data-ttu-id="f8308-141">Log Analytics 目前會將使用時間戳記分隔符號從記錄檔中收集到的日期/時間視為 UTC。</span><span class="sxs-lookup"><span data-stu-id="f8308-141">Log Analytics currently treats the date/time collected from a log using a timestamp delimiter as UTC.</span></span>  <span data-ttu-id="f8308-142">這很快就會變更為使用代理程式上的時區。</span><span class="sxs-lookup"><span data-stu-id="f8308-142">This will soon be changed to use the time zone on the agent.</span></span>
>
>

1. <span data-ttu-id="f8308-143">按一下 [瀏覽]  並瀏覽至範例檔案。</span><span class="sxs-lookup"><span data-stu-id="f8308-143">Click **Browse** and browse to a sample file.</span></span>  <span data-ttu-id="f8308-144">請注意，在某些瀏覽器中，這個按鈕可能標示為 [選擇檔案]  。</span><span class="sxs-lookup"><span data-stu-id="f8308-144">Note that this may button may be labeled **Choose File** in some browsers.</span></span>
2. <span data-ttu-id="f8308-145">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f8308-145">Click **Next**.</span></span>
3. <span data-ttu-id="f8308-146">自訂記錄檔精靈會上傳檔案並列出其識別的記錄。</span><span class="sxs-lookup"><span data-stu-id="f8308-146">The Custom Log Wizard will upload the file and list the records that it identifies.</span></span>
4. <span data-ttu-id="f8308-147">變更用來識別新記錄的分隔符號，並選取最能識別記錄檔中的記錄的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="f8308-147">Change the delimiter that is used to identify a new record and select the delimiter that best identifies the records in your log file.</span></span>
5. <span data-ttu-id="f8308-148">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f8308-148">Click **Next**.</span></span>

### <a name="step-3-add-log-collection-paths"></a><span data-ttu-id="f8308-149">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="f8308-149">Step 3.</span></span> <span data-ttu-id="f8308-150">新增記錄檔收集路徑</span><span class="sxs-lookup"><span data-stu-id="f8308-150">Add log collection paths</span></span>
<span data-ttu-id="f8308-151">您必須在代理程式上定義一個或多個它可以在其中找到自訂記錄檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="f8308-151">You must define one or more paths on the agent where it can locate the custom log.</span></span>  <span data-ttu-id="f8308-152">您可以提供該記錄檔的特定路徑和名稱，或者您可以使用萬用字元為該名稱指定路徑。</span><span class="sxs-lookup"><span data-stu-id="f8308-152">You can either provide a specific path and name for the log file, or you can specify a path with a wildcard for the name.</span></span>  <span data-ttu-id="f8308-153">這可支援每天會建立一個新檔案的應用程式或在一個檔案到達特定大小時提供支援。</span><span class="sxs-lookup"><span data-stu-id="f8308-153">This supports applications that create a new file each day or when one file reaches a certain size.</span></span>  <span data-ttu-id="f8308-154">您也可以為單一記錄檔提供多個路徑。</span><span class="sxs-lookup"><span data-stu-id="f8308-154">You can also provide multiple paths for a single log file.</span></span>

<span data-ttu-id="f8308-155">例如，應用程式可能會每天建立一個記錄檔，且名稱中會包含日期，如同 log20100316.txt。</span><span class="sxs-lookup"><span data-stu-id="f8308-155">For example, an application might create a log file each day with the date included in the name as in log20100316.txt.</span></span> <span data-ttu-id="f8308-156">這類記錄檔的模式可能是 *log\*.txt*，而這會套用到任何遵循應用程式命名配置的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-156">A pattern for such a log might be *log\*.txt* which would apply to any log file following the application’s naming scheme.</span></span>

<span data-ttu-id="f8308-157">下表提供可用來指定不同記錄檔的有效模式範例。</span><span class="sxs-lookup"><span data-stu-id="f8308-157">The following table provides examples of valid patterns to specify different log files.</span></span>

| <span data-ttu-id="f8308-158">說明</span><span class="sxs-lookup"><span data-stu-id="f8308-158">Description</span></span> | <span data-ttu-id="f8308-159">路徑</span><span class="sxs-lookup"><span data-stu-id="f8308-159">Path</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8308-160">Windows 代理程式上的 *C:\Logs* 中，副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="f8308-160">All files in *C:\Logs* with .txt extension on Windows agent</span></span> |<span data-ttu-id="f8308-161">C:\Logs\\\*.txt</span><span class="sxs-lookup"><span data-stu-id="f8308-161">C:\Logs\\\*.txt</span></span> |
| <span data-ttu-id="f8308-162">Windows 代理程式上的 *C:\Logs* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="f8308-162">All files in *C:\Logs* with a name starting with log and a .txt extension on Windows agent</span></span> |<span data-ttu-id="f8308-163">C:\Logs\log\*.txt</span><span class="sxs-lookup"><span data-stu-id="f8308-163">C:\Logs\log\*.txt</span></span> |
| <span data-ttu-id="f8308-164">Windows 代理程式上的 */var/log/audit* 中副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="f8308-164">All files in */var/log/audit* with .txt extension on Linux agent</span></span> |<span data-ttu-id="f8308-165">/var/log/audit/*.txt</span><span class="sxs-lookup"><span data-stu-id="f8308-165">/var/log/audit/*.txt</span></span> |
| <span data-ttu-id="f8308-166">Linux 代理程式上的 */var/log/audit* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="f8308-166">All files in */var/log/audit* with a name starting with log and a .txt extension on Linux agent</span></span> |<span data-ttu-id="f8308-167">/var/log/audit/log\*.txt</span><span class="sxs-lookup"><span data-stu-id="f8308-167">/var/log/audit/log\*.txt</span></span> |

1. <span data-ttu-id="f8308-168">選取 Windows 或 Linux 以指定您要新增的路徑格式。</span><span class="sxs-lookup"><span data-stu-id="f8308-168">Select Windows or Linux to specify which path format you are adding.</span></span>
2. <span data-ttu-id="f8308-169">輸入路徑並按一下 [+] **+** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f8308-169">Type in the path and click the **+** button.</span></span>
3. <span data-ttu-id="f8308-170">針對任何其他路徑重複此程序。</span><span class="sxs-lookup"><span data-stu-id="f8308-170">Repeat the process for any additional paths.</span></span>

### <a name="step-4-provide-a-name-and-description-for-the-log"></a><span data-ttu-id="f8308-171">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="f8308-171">Step 4.</span></span> <span data-ttu-id="f8308-172">提供記錄檔的名稱和描述</span><span class="sxs-lookup"><span data-stu-id="f8308-172">Provide a name and description for the log</span></span>
<span data-ttu-id="f8308-173">您指定的名稱將用於如上所述的記錄檔類型。</span><span class="sxs-lookup"><span data-stu-id="f8308-173">The name that you specify will be used for the log type as described above.</span></span>  <span data-ttu-id="f8308-174">它一定會以 _CL 結尾以將自己辨別為自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-174">It will always end with _CL to distinguish it as a custom log.</span></span>

1. <span data-ttu-id="f8308-175">輸入記錄檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8308-175">Type in a name for the log.</span></span>  <span data-ttu-id="f8308-176">**\__CL** 尾碼會自動提供。</span><span class="sxs-lookup"><span data-stu-id="f8308-176">The **\_CL** suffix is automatically provided.</span></span>
2. <span data-ttu-id="f8308-177">新增選擇性的 [描述] 。</span><span class="sxs-lookup"><span data-stu-id="f8308-177">Add an optional **Description**.</span></span>
3. <span data-ttu-id="f8308-178">按 [下一步]  來儲存自訂記錄檔的定義。</span><span class="sxs-lookup"><span data-stu-id="f8308-178">Click **Next** to save the custom log definition.</span></span>

### <a name="step-5-validate-that-the-custom-logs-are-being-collected"></a><span data-ttu-id="f8308-179">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="f8308-179">Step 5.</span></span> <span data-ttu-id="f8308-180">驗證會收集自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-180">Validate that the custom logs are being collected</span></span>
<span data-ttu-id="f8308-181">最多可能需要一小時的時間，新的自訂記錄檔中的初始資料才會出現在 Log Analytics 中。</span><span class="sxs-lookup"><span data-stu-id="f8308-181">It may take up to an hour for the initial data from a new custom log to appear in Log Analytics.</span></span>  <span data-ttu-id="f8308-182">從您定義自訂記錄檔之後，它就會開始從您指定的路徑中所找到的記錄檔收集項目。</span><span class="sxs-lookup"><span data-stu-id="f8308-182">It will start collecting entries from the logs found in the path you specified from the point that you defined the custom log.</span></span>  <span data-ttu-id="f8308-183">它不會保留您在建立自訂記錄檔期間上傳的項目，但它會收集它所找出之記錄檔中既有的項目。</span><span class="sxs-lookup"><span data-stu-id="f8308-183">It will not retain the entries that you uploaded during the custom log creation, but it will collect already existing entries in the log files that it locates.</span></span>

<span data-ttu-id="f8308-184">一旦 Log Analytics 開始從自訂記錄檔收集，就能透過「記錄檔搜尋」取得其記錄。</span><span class="sxs-lookup"><span data-stu-id="f8308-184">Once Log Analytics starts collecting from the custom log, its records will be available with a Log Search.</span></span>  <span data-ttu-id="f8308-185">請使用您提供給自訂記錄檔的名稱來做為查詢中的 [類型]  。</span><span class="sxs-lookup"><span data-stu-id="f8308-185">Use the name that you gave the custom log as the **Type** in your query.</span></span>

> [!NOTE]
> <span data-ttu-id="f8308-186">如果搜尋中遺漏 RawData 屬性，您可能需要先關閉再重新開啟瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f8308-186">If the RawData property is missing from the search, you may need to close and reopen your browser.</span></span>
>
>

### <a name="step-6-parse-the-custom-log-entries"></a><span data-ttu-id="f8308-187">步驟 6.</span><span class="sxs-lookup"><span data-stu-id="f8308-187">Step 6.</span></span> <span data-ttu-id="f8308-188">剖析自訂記錄檔項目</span><span class="sxs-lookup"><span data-stu-id="f8308-188">Parse the custom log entries</span></span>
<span data-ttu-id="f8308-189">整個記錄檔項目會儲存在稱為 **RawData**的單一屬性中。</span><span class="sxs-lookup"><span data-stu-id="f8308-189">The entire log entry will be stored in a single property called **RawData**.</span></span>  <span data-ttu-id="f8308-190">您很可能會想要將每個項目中的不同資訊片段，分成儲存在記錄中的個別屬性。</span><span class="sxs-lookup"><span data-stu-id="f8308-190">You will most likely want to separate the different pieces of information in each entry into individual properties stored in the record.</span></span>  <span data-ttu-id="f8308-191">您可以使用 Log Analytics 的 [自訂欄位](log-analytics-custom-fields.md) 功能來這麼做。</span><span class="sxs-lookup"><span data-stu-id="f8308-191">You do this using the [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

<span data-ttu-id="f8308-192">這裡並未提供用來剖析自訂記錄檔項目的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="f8308-192">Detailed steps for parsing the custom log entry are not provided here.</span></span>  <span data-ttu-id="f8308-193">如需這項資訊，請參閱 [自訂欄位](log-analytics-custom-fields.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="f8308-193">Please refer to the [Custom Fields](log-analytics-custom-fields.md) documentation for this information.</span></span>

## <a name="disabling-a-custom-log"></a><span data-ttu-id="f8308-194">停用自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-194">Disabling a custom log</span></span>
<span data-ttu-id="f8308-195">自訂記錄檔定義一旦建立就無法移除，但您可以移除其所有集合路徑來停用它。</span><span class="sxs-lookup"><span data-stu-id="f8308-195">You cannot remove a custom log definition once it's been created, but you can disable it by removing all of its collection paths.</span></span>

1. <span data-ttu-id="f8308-196">在 OMS 入口網站中，移至 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f8308-196">In the OMS portal, go to **Settings**.</span></span>
2. <span data-ttu-id="f8308-197">按一下 [資料]，然後按一下 [自訂記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="f8308-197">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="f8308-198">按一下自訂記錄檔定義旁邊的 [詳細資料] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="f8308-198">Click **Details** next to the custom log definition to disable.</span></span>
4. <span data-ttu-id="f8308-199">移除自訂記錄檔定義的每個集合路徑。</span><span class="sxs-lookup"><span data-stu-id="f8308-199">Remove each of the collection paths for the custom log definition.</span></span>

## <a name="data-collection"></a><span data-ttu-id="f8308-200">資料收集</span><span class="sxs-lookup"><span data-stu-id="f8308-200">Data collection</span></span>
<span data-ttu-id="f8308-201">Log Analytics 會從每個自訂記錄檔收集新的項目，間隔大約為每 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f8308-201">Log Analytics will collect new entries from each custom log approximately every 5 minutes.</span></span>  <span data-ttu-id="f8308-202">代理程式會記錄它在從中收集項目的每個記錄檔中的位置。</span><span class="sxs-lookup"><span data-stu-id="f8308-202">The agent will record its place in each log file that it collects from.</span></span>  <span data-ttu-id="f8308-203">如果代理程式離線一段時間，Log Analytics 即會從上次停止的地方收集項目，即使這些項目是在代理程式離線時所建立亦同。</span><span class="sxs-lookup"><span data-stu-id="f8308-203">If the agent goes offline for a period of time, then Log Analytics will collect entries from where it last left off, even if those entries were created while the agent was offline.</span></span>

<span data-ttu-id="f8308-204">整個記錄檔項目的內容會寫入到稱為 **RawData**的單一屬性。</span><span class="sxs-lookup"><span data-stu-id="f8308-204">The entire contents of the log entry are written to a single property called **RawData**.</span></span>  <span data-ttu-id="f8308-205">您可以將此屬性剖析成多個屬性，以在建立自訂記錄檔之後透過定義 [自訂欄位](log-analytics-custom-fields.md) 來個別分析和搜尋。</span><span class="sxs-lookup"><span data-stu-id="f8308-205">You can parse this into multiple properties that can be analyzed and searched separately by defining [Custom Fields](log-analytics-custom-fields.md) after you have created the custom log.</span></span>

## <a name="custom-log-record-properties"></a><span data-ttu-id="f8308-206">自訂記錄檔記錄的屬性</span><span class="sxs-lookup"><span data-stu-id="f8308-206">Custom log record properties</span></span>
<span data-ttu-id="f8308-207">自訂記錄檔記錄的類型具有您提供的記錄檔名稱和下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="f8308-207">Custom log records have a type with the log name that you provide and the properties in the following table.</span></span>

| <span data-ttu-id="f8308-208">屬性</span><span class="sxs-lookup"><span data-stu-id="f8308-208">Property</span></span> | <span data-ttu-id="f8308-209">說明</span><span class="sxs-lookup"><span data-stu-id="f8308-209">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8308-210">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="f8308-210">TimeGenerated</span></span> |<span data-ttu-id="f8308-211">Log Analytics 收集記錄時的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f8308-211">Date and time that the record was collected by Log Analytics.</span></span>  <span data-ttu-id="f8308-212">如果記錄使用以時間為基礎的分隔符號，則這是從項目收集到的時間。</span><span class="sxs-lookup"><span data-stu-id="f8308-212">If the log uses a time-based delimiter then this is the time collected from the entry.</span></span> |
| <span data-ttu-id="f8308-213">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="f8308-213">SourceSystem</span></span> |<span data-ttu-id="f8308-214">收集記錄的來源代理程式類型。</span><span class="sxs-lookup"><span data-stu-id="f8308-214">Type of agent the record was collected from.</span></span> <br> <span data-ttu-id="f8308-215">OpsManager - Windows 代理程式，直接連線或由 System Center Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="f8308-215">OpsManager – Windows agent, either direct connect or System Center Operations Manager</span></span> <br> <span data-ttu-id="f8308-216">Linux – 所有的 Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="f8308-216">Linux – All Linux agents</span></span> |
| <span data-ttu-id="f8308-217">RawData</span><span class="sxs-lookup"><span data-stu-id="f8308-217">RawData</span></span> |<span data-ttu-id="f8308-218">所收集項目的完整文字。</span><span class="sxs-lookup"><span data-stu-id="f8308-218">Full text of the collected entry.</span></span> |
| <span data-ttu-id="f8308-219">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="f8308-219">ManagementGroupName</span></span> |<span data-ttu-id="f8308-220">System Center Operations Manager 代理程式的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="f8308-220">Name of the management group for System Center Operations Manage agents.</span></span>  <span data-ttu-id="f8308-221">若為其他代理程式，此為 AOI-\<工作區 ID\></span><span class="sxs-lookup"><span data-stu-id="f8308-221">For other agents, this is AOI-\<workspace ID\></span></span> |

## <a name="log-searches-with-custom-log-records"></a><span data-ttu-id="f8308-222">使用自訂記錄檔記錄來記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="f8308-222">Log searches with custom log records</span></span>
<span data-ttu-id="f8308-223">和來自任何其他資料來源的記錄一樣，來自自訂記錄檔的記錄會儲存在 OMS 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="f8308-223">Records from custom logs are stored in the OMS repository just like records from any other data source.</span></span>  <span data-ttu-id="f8308-224">其類型會符合您在定義記錄檔時提供的名稱，因此您可以在搜尋中使用 [類型] 屬性，以擷取從特定記錄檔收集而來的記錄。</span><span class="sxs-lookup"><span data-stu-id="f8308-224">They will have a type matching the name that you provide when you define the log, so you can use the Type property in your search to retrieve records collected from a specific log.</span></span>

<span data-ttu-id="f8308-225">下表提供從自訂記錄檔擷取記錄之記錄檔搜尋的不同範例。</span><span class="sxs-lookup"><span data-stu-id="f8308-225">The following table provides different examples of log searches that retrieve records from custom logs.</span></span>

| <span data-ttu-id="f8308-226">查詢</span><span class="sxs-lookup"><span data-stu-id="f8308-226">Query</span></span> | <span data-ttu-id="f8308-227">說明</span><span class="sxs-lookup"><span data-stu-id="f8308-227">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8308-228">Type=MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="f8308-228">Type=MyApp_CL</span></span> |<span data-ttu-id="f8308-229">所有事件來自名為 MyApp_CL 的自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-229">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="f8308-230">Type=MyApp_CL Severity_CF=error</span><span class="sxs-lookup"><span data-stu-id="f8308-230">Type=MyApp_CL Severity_CF=error</span></span> |<span data-ttu-id="f8308-231">來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="f8308-231">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |

>[!NOTE]
> <span data-ttu-id="f8308-232">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="f8308-232">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="f8308-233">查詢</span><span class="sxs-lookup"><span data-stu-id="f8308-233">Query</span></span> | <span data-ttu-id="f8308-234">說明</span><span class="sxs-lookup"><span data-stu-id="f8308-234">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8308-235">MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="f8308-235">MyApp_CL</span></span> |<span data-ttu-id="f8308-236">所有事件來自名為 MyApp_CL 的自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f8308-236">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="f8308-237">MyApp_CL &#124; where Severity_CF=="error"</span><span class="sxs-lookup"><span data-stu-id="f8308-237">MyApp_CL &#124; where Severity_CF=="error"</span></span> |<span data-ttu-id="f8308-238">來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="f8308-238">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a><span data-ttu-id="f8308-239">新增自訂記錄檔的範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="f8308-239">Sample walkthrough of adding a custom log</span></span>
<span data-ttu-id="f8308-240">下面的章節會逐步解說建立自訂記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="f8308-240">The following section walks through an example of creating a custom log.</span></span>  <span data-ttu-id="f8308-241">所收集的範例記錄在每一行只有一個項目，其開頭為日期和時間，然後是以逗號分隔的程式碼、狀態及訊息欄位。</span><span class="sxs-lookup"><span data-stu-id="f8308-241">The sample log being collected has a single entry on each line starting with a date and time and then comma-delimited fields for code, status, and message.</span></span>  <span data-ttu-id="f8308-242">下面顯示了幾個範例項目。</span><span class="sxs-lookup"><span data-stu-id="f8308-242">Several sample entries are shown below.</span></span>

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect to database
    2016-03-10 01:31:34 303,Error,Application lost connection to database

### <a name="upload-and-parse-a-sample-log"></a><span data-ttu-id="f8308-243">上傳和剖析範例記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-243">Upload and parse a sample log</span></span>
<span data-ttu-id="f8308-244">我們提供其中一個記錄檔，並可以看到將會收集的事件。</span><span class="sxs-lookup"><span data-stu-id="f8308-244">We provide one of the log files and can see the events that it will be collecting.</span></span>  <span data-ttu-id="f8308-245">在此案例中，新行字元足以做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="f8308-245">In this case New Line is a sufficient delimiter.</span></span>  <span data-ttu-id="f8308-246">但如果記錄檔中的單一項目跨越多行，就必須使用時間戳記分隔符號。</span><span class="sxs-lookup"><span data-stu-id="f8308-246">If a single entry in the log could span multiple lines though, then a timestamp delimiter would need to be used.</span></span>

![上傳和剖析範例記錄檔](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a><span data-ttu-id="f8308-248">新增記錄檔收集路徑</span><span class="sxs-lookup"><span data-stu-id="f8308-248">Add log collection paths</span></span>
<span data-ttu-id="f8308-249">記錄檔將位於 *C:\MyApp\Logs*。</span><span class="sxs-lookup"><span data-stu-id="f8308-249">The log files will be located in *C:\MyApp\Logs*.</span></span>  <span data-ttu-id="f8308-250">每一天都會建立一個新檔案，且其名稱中包括「appYYYYMMDD.log」 模式的日期。</span><span class="sxs-lookup"><span data-stu-id="f8308-250">A new file will be created each day with a name that includes the date in the pattern *appYYYYMMDD.log*.</span></span>  <span data-ttu-id="f8308-251">此記錄檔的完整模式為 *C:\MyApp\Logs\\\*.log*。</span><span class="sxs-lookup"><span data-stu-id="f8308-251">A sufficient pattern for this log would be *C:\MyApp\Logs\\\*.log*.</span></span>

![記錄檔收集路徑](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-the-log"></a><span data-ttu-id="f8308-253">提供記錄檔的名稱和描述</span><span class="sxs-lookup"><span data-stu-id="f8308-253">Provide a name and description for the log</span></span>
<span data-ttu-id="f8308-254">我們使用 *MyApp_CL* 這個名稱並輸入 [描述]。</span><span class="sxs-lookup"><span data-stu-id="f8308-254">We use a name of *MyApp_CL* and type in a **Description**.</span></span>

![記錄檔名稱](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-the-custom-logs-are-being-collected"></a><span data-ttu-id="f8308-256">驗證會收集自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="f8308-256">Validate that the custom logs are being collected</span></span>
<span data-ttu-id="f8308-257">我們使用 *Type=MyApp_CL* 這個查詢，以從收集到的記錄檔傳回所有記錄。</span><span class="sxs-lookup"><span data-stu-id="f8308-257">We use a query of *Type=MyApp_CL* to return all records from the collected log.</span></span>

![無自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-the-custom-log-entries"></a><span data-ttu-id="f8308-259">剖析自訂記錄檔項目</span><span class="sxs-lookup"><span data-stu-id="f8308-259">Parse the custom log entries</span></span>
<span data-ttu-id="f8308-260">我們使用「自訂欄位」來定義 *EventTime*、*Code*、*Status* 和 *Message* 欄位，而且我們可以在查詢所傳回的記錄中看到差異。</span><span class="sxs-lookup"><span data-stu-id="f8308-260">We use Custom Fields to define the *EventTime*, *Code*, *Status*, and *Message* fields and we can see the difference in the records that are returned by the query.</span></span>

![有自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a><span data-ttu-id="f8308-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8308-262">Next steps</span></span>
* <span data-ttu-id="f8308-263">使用[自訂欄位](log-analytics-custom-fields.md)，以將自訂記錄中的項目剖析至個別欄位。</span><span class="sxs-lookup"><span data-stu-id="f8308-263">Use [Custom Fields](log-analytics-custom-fields.md) to parse the entries in the custom log in to individual fields.</span></span>
* <span data-ttu-id="f8308-264">了解 [記錄搜尋](log-analytics-log-searches.md) ，以分析從資料來源和解決方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="f8308-264">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
