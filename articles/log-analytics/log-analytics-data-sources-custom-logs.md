---
title: "aaaCollect 自訂登入 OMS 記錄分析 |Microsoft 文件"
description: "Log Analytics 可從 Windows 和 Linux 電腦上的文字檔收集事件。  這篇文章描述如何 toodefine 新的自訂記錄檔和詳細資料的 hello 記錄它們建立 hello OMS 儲存機制中。"
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
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a><span data-ttu-id="df5a5-104">Log Analytics 中的自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-104">Custom logs in Log Analytics</span></span>
<span data-ttu-id="df5a5-105">記錄分析中的 hello 自訂記錄檔資料來源可讓您從 Windows 和 Linux 電腦上的文字檔 toocollect 事件。</span><span class="sxs-lookup"><span data-stu-id="df5a5-105">hello Custom Logs data source in Log Analytics allows you toocollect events from text files on both Windows and Linux computers.</span></span> <span data-ttu-id="df5a5-106">許多應用程式記錄資訊 tootext 檔，而不是標準的記錄服務，例如 Windows 事件記錄檔或 Syslog。</span><span class="sxs-lookup"><span data-stu-id="df5a5-106">Many applications log information tootext files instead of standard logging services such as Windows Event log or Syslog.</span></span>  <span data-ttu-id="df5a5-107">一旦收集完成，您可以剖析使用 hello tooindividual 欄位中的 hello 記錄檔中的每一筆記錄[自訂欄位](log-analytics-custom-fields.md)記錄分析的功能。</span><span class="sxs-lookup"><span data-stu-id="df5a5-107">Once collected, you can parse each record in hello log in tooindividual fields using hello [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

![自訂記錄檔收集](media/log-analytics-data-sources-custom-logs/overview.png)

<span data-ttu-id="df5a5-109">hello 收集的記錄檔 toobe 必須符合下列準則的 hello。</span><span class="sxs-lookup"><span data-stu-id="df5a5-109">hello log files toobe collected must match hello following criteria.</span></span>

- <span data-ttu-id="df5a5-110">hello 記錄必須有每行的單一項目，或使用時間戳記相符 hello 下列其中一種格式在 hello 開頭的每個項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-110">hello log must either have a single entry per line or use a timestamp matching one of hello following formats at hello start of each entry.</span></span>

    <span data-ttu-id="df5a5-111">YYYY-MM-DD HH:MM:SS </span><span class="sxs-lookup"><span data-stu-id="df5a5-111">YYYY-MM-DD HH:MM:SS</span></span><br><span data-ttu-id="df5a5-112">M/D/YYYY HH:MM:SS AM/PM</span><span class="sxs-lookup"><span data-stu-id="df5a5-112">M/D/YYYY HH:MM:SS AM/PM</span></span> <br><span data-ttu-id="df5a5-113">Mon DD,YYYY HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="df5a5-113">Mon DD,YYYY HH:MM:SS</span></span>

- <span data-ttu-id="df5a5-114">hello 記錄檔不允許循環的更新會以新的項目覆寫 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="df5a5-114">hello log file must not allow circular updates where hello file is overwritten with new entries.</span></span>
- <span data-ttu-id="df5a5-115">hello 記錄檔必須使用 ASCII 或 utf-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="df5a5-115">hello log file must use ASCII or UTF-8 encoding.</span></span>  <span data-ttu-id="df5a5-116">不支援其他格式，例如 UTF-16。</span><span class="sxs-lookup"><span data-stu-id="df5a5-116">Other formats such as UTF-16 are not supported.</span></span>

>[!NOTE]
><span data-ttu-id="df5a5-117">如果 hello 記錄檔中有重複的項目，將會收集記錄分析它們。</span><span class="sxs-lookup"><span data-stu-id="df5a5-117">If there are duplicate entries in hello log file, Log Analytics will collect them.</span></span>  <span data-ttu-id="df5a5-118">不過，hello 搜尋結果會不一致，hello 篩選結果會顯示數個事件比 hello 結果計數。</span><span class="sxs-lookup"><span data-stu-id="df5a5-118">However, hello search results will be inconsistent where hello filter results show more events than hello result count.</span></span>  <span data-ttu-id="df5a5-119">它將會驗證 hello 記錄 toodetermine 如果 hello 建立應用程式，它會造成這種行為，並盡可能建立 hello 自訂記錄檔集合定義之前解決。</span><span class="sxs-lookup"><span data-stu-id="df5a5-119">It will be important that you validate hello log toodetermine if hello application that creates it is causing this behavior and address it if possible before creating hello custom log collection definition.</span></span>  
>
  
## <a name="defining-a-custom-log"></a><span data-ttu-id="df5a5-120">定義自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-120">Defining a custom log</span></span>
<span data-ttu-id="df5a5-121">使用下列程序 toodefine 自訂記錄檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="df5a5-121">Use hello following procedure toodefine a custom log file.</span></span>  <span data-ttu-id="df5a5-122">如需逐步解說的範例，以新增自訂的記錄檔的這篇文章捲動 toohello 結束。</span><span class="sxs-lookup"><span data-stu-id="df5a5-122">Scroll toohello end of this article for a walkthrough of a sample of adding a custom log.</span></span>

### <a name="step-1-open-hello-custom-log-wizard"></a><span data-ttu-id="df5a5-123">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="df5a5-123">Step 1.</span></span> <span data-ttu-id="df5a5-124">開啟 hello 自訂記錄檔精靈</span><span class="sxs-lookup"><span data-stu-id="df5a5-124">Open hello Custom Log Wizard</span></span>
<span data-ttu-id="df5a5-125">hello 自訂記錄檔精靈 hello OMS 入口網站中執行，並可讓您新的自訂記錄檔 toocollect toodefine。</span><span class="sxs-lookup"><span data-stu-id="df5a5-125">hello Custom Log Wizard runs in hello OMS portal and allows you toodefine a new custom log toocollect.</span></span>

1. <span data-ttu-id="df5a5-126">在 hello OMS 入口網站中，移過**設定**。</span><span class="sxs-lookup"><span data-stu-id="df5a5-126">In hello OMS portal, go too**Settings**.</span></span>
2. <span data-ttu-id="df5a5-127">按一下 [資料]，然後按一下 [自訂記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="df5a5-127">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="df5a5-128">根據預設，所有的組態變更會自動推入 tooall 代理程式。</span><span class="sxs-lookup"><span data-stu-id="df5a5-128">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="df5a5-129">Linux 代理程式，請傳送 toohello Fluentd 資料收集器的組態檔案。</span><span class="sxs-lookup"><span data-stu-id="df5a5-129">For Linux agents, a configuration file is sent toohello Fluentd data collector.</span></span>  <span data-ttu-id="df5a5-130">如果您想 toomodify 手動在每個 Linux 代理程式上的這個檔案，然後取消核取方塊 hello*套用下列組態 toomy Linux 電腦*。</span><span class="sxs-lookup"><span data-stu-id="df5a5-130">If you wish toomodify this file manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>
4. <span data-ttu-id="df5a5-131">按一下**新增 +** tooopen hello 自訂記錄檔精靈。</span><span class="sxs-lookup"><span data-stu-id="df5a5-131">Click **Add+** tooopen hello Custom Log Wizard.</span></span>

### <a name="step-2-upload-and-parse-a-sample-log"></a><span data-ttu-id="df5a5-132">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="df5a5-132">Step 2.</span></span> <span data-ttu-id="df5a5-133">上傳和剖析範例記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-133">Upload and parse a sample log</span></span>
<span data-ttu-id="df5a5-134">您開始上傳 hello 自訂記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="df5a5-134">You start by uploading a sample of hello custom log.</span></span>  <span data-ttu-id="df5a5-135">hello 精靈將會剖析，並顯示您 toovalidate 此檔案中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-135">hello wizard will parse and display hello entries in this file for you toovalidate.</span></span>  <span data-ttu-id="df5a5-136">記錄分析將使用您指定 tooidentify 每一筆記錄的 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="df5a5-136">Log Analytics will use hello delimiter that you specify tooidentify each record.</span></span>

<span data-ttu-id="df5a5-137">**新的一行**為 hello 預設分隔符號，用於有單一項目，每行的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-137">**New Line** is hello default delimiter and is used for log files that have a single entry per line.</span></span>  <span data-ttu-id="df5a5-138">如果 hello 一行開頭的日期和時間，其中一種 hello 可用的格式，則您可以指定**時間戳記**支援跨越一行以上的項目分隔符號。</span><span class="sxs-lookup"><span data-stu-id="df5a5-138">If hello line starts with a date and time in one of hello available formats, then you can specify a **Timestamp** delimiter which supports entries that span more than one line.</span></span>

<span data-ttu-id="df5a5-139">如果使用時間戳記分隔符號，則會與 hello 日期/時間為 hello 記錄檔中的項目指定填入 hello TimeGenerated 屬性儲存在 OMS 中的每一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="df5a5-139">If a timestamp delimiter is used, then hello TimeGenerated property of each record stored in OMS will be populated with hello date/time specified for that entry in hello log file.</span></span>  <span data-ttu-id="df5a5-140">如果使用新行的分隔符號，然後 TimeGenerated 會填入日期和時間，記錄分析會收集 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-140">If a new line delimiter is used, then TimeGenerated is populated with date and time that Log Analytics collected hello entry.</span></span>

> [!NOTE]
> <span data-ttu-id="df5a5-141">記錄分析目前會將 hello 日期/時間從使用為 UTC 時間戳記分隔符號的記錄檔收集。</span><span class="sxs-lookup"><span data-stu-id="df5a5-141">Log Analytics currently treats hello date/time collected from a log using a timestamp delimiter as UTC.</span></span>  <span data-ttu-id="df5a5-142">很快就會變更的 toouse hello 時區 hello 代理程式上。</span><span class="sxs-lookup"><span data-stu-id="df5a5-142">This will soon be changed toouse hello time zone on hello agent.</span></span>
>
>

1. <span data-ttu-id="df5a5-143">按一下**瀏覽**並瀏覽 tooa 範例檔案。</span><span class="sxs-lookup"><span data-stu-id="df5a5-143">Click **Browse** and browse tooa sample file.</span></span>  <span data-ttu-id="df5a5-144">請注意，在某些瀏覽器中，這個按鈕可能標示為 [選擇檔案]  。</span><span class="sxs-lookup"><span data-stu-id="df5a5-144">Note that this may button may be labeled **Choose File** in some browsers.</span></span>
2. <span data-ttu-id="df5a5-145">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="df5a5-145">Click **Next**.</span></span>
3. <span data-ttu-id="df5a5-146">hello 自訂記錄精靈會將上傳 hello 檔案和清單 hello 記錄，它會識別。</span><span class="sxs-lookup"><span data-stu-id="df5a5-146">hello Custom Log Wizard will upload hello file and list hello records that it identifies.</span></span>
4. <span data-ttu-id="df5a5-147">變更是使用的 tooidentify 新記錄的 hello 分隔符號和可識別最適合您的記錄檔中的 hello 記錄選取 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="df5a5-147">Change hello delimiter that is used tooidentify a new record and select hello delimiter that best identifies hello records in your log file.</span></span>
5. <span data-ttu-id="df5a5-148">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="df5a5-148">Click **Next**.</span></span>

### <a name="step-3-add-log-collection-paths"></a><span data-ttu-id="df5a5-149">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="df5a5-149">Step 3.</span></span> <span data-ttu-id="df5a5-150">新增記錄檔收集路徑</span><span class="sxs-lookup"><span data-stu-id="df5a5-150">Add log collection paths</span></span>
<span data-ttu-id="df5a5-151">它可以在其中尋找 hello 自訂記錄檔的 hello 代理程式上，您必須定義一個或多個路徑。</span><span class="sxs-lookup"><span data-stu-id="df5a5-151">You must define one or more paths on hello agent where it can locate hello custom log.</span></span>  <span data-ttu-id="df5a5-152">您可以提供特定路徑和名稱為 hello 記錄檔，或您可以使用萬用字元 hello 名稱指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="df5a5-152">You can either provide a specific path and name for hello log file, or you can specify a path with a wildcard for hello name.</span></span>  <span data-ttu-id="df5a5-153">這可支援每天會建立一個新檔案的應用程式或在一個檔案到達特定大小時提供支援。</span><span class="sxs-lookup"><span data-stu-id="df5a5-153">This supports applications that create a new file each day or when one file reaches a certain size.</span></span>  <span data-ttu-id="df5a5-154">您也可以為單一記錄檔提供多個路徑。</span><span class="sxs-lookup"><span data-stu-id="df5a5-154">You can also provide multiple paths for a single log file.</span></span>

<span data-ttu-id="df5a5-155">例如，應用程式可能會建立記錄檔每一天 hello 如同 log20100316.txt hello 名稱中包含的日期。</span><span class="sxs-lookup"><span data-stu-id="df5a5-155">For example, an application might create a log file each day with hello date included in hello name as in log20100316.txt.</span></span> <span data-ttu-id="df5a5-156">這類記錄檔的模式可能是*記錄\*.txt*會套用 tooany 遵循 hello 應用程式的記錄檔的命名配置。</span><span class="sxs-lookup"><span data-stu-id="df5a5-156">A pattern for such a log might be *log\*.txt* which would apply tooany log file following hello application’s naming scheme.</span></span>

<span data-ttu-id="df5a5-157">hello 下表提供有效的模式範例 toospecify 不同記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-157">hello following table provides examples of valid patterns toospecify different log files.</span></span>

| <span data-ttu-id="df5a5-158">說明</span><span class="sxs-lookup"><span data-stu-id="df5a5-158">Description</span></span> | <span data-ttu-id="df5a5-159">路徑</span><span class="sxs-lookup"><span data-stu-id="df5a5-159">Path</span></span> |
|:--- |:--- |
| <span data-ttu-id="df5a5-160">Windows 代理程式上的 *C:\Logs* 中，副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="df5a5-160">All files in *C:\Logs* with .txt extension on Windows agent</span></span> |<span data-ttu-id="df5a5-161">C:\Logs\\\*.txt</span><span class="sxs-lookup"><span data-stu-id="df5a5-161">C:\Logs\\\*.txt</span></span> |
| <span data-ttu-id="df5a5-162">Windows 代理程式上的 *C:\Logs* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="df5a5-162">All files in *C:\Logs* with a name starting with log and a .txt extension on Windows agent</span></span> |<span data-ttu-id="df5a5-163">C:\Logs\log\*.txt</span><span class="sxs-lookup"><span data-stu-id="df5a5-163">C:\Logs\log\*.txt</span></span> |
| <span data-ttu-id="df5a5-164">Windows 代理程式上的 */var/log/audit* 中副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="df5a5-164">All files in */var/log/audit* with .txt extension on Linux agent</span></span> |<span data-ttu-id="df5a5-165">/var/log/audit/*.txt</span><span class="sxs-lookup"><span data-stu-id="df5a5-165">/var/log/audit/*.txt</span></span> |
| <span data-ttu-id="df5a5-166">Linux 代理程式上的 */var/log/audit* 中，名稱開頭為 log 且副檔名為 .txt 的所有檔案</span><span class="sxs-lookup"><span data-stu-id="df5a5-166">All files in */var/log/audit* with a name starting with log and a .txt extension on Linux agent</span></span> |<span data-ttu-id="df5a5-167">/var/log/audit/log\*.txt</span><span class="sxs-lookup"><span data-stu-id="df5a5-167">/var/log/audit/log\*.txt</span></span> |

1. <span data-ttu-id="df5a5-168">選取您要加入其中的路徑格式的 Windows 或 Linux toospecify。</span><span class="sxs-lookup"><span data-stu-id="df5a5-168">Select Windows or Linux toospecify which path format you are adding.</span></span>
2. <span data-ttu-id="df5a5-169">輸入 hello 路徑中，按一下 [hello  **+**  ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="df5a5-169">Type in hello path and click hello **+** button.</span></span>
3. <span data-ttu-id="df5a5-170">任何其他路徑重複 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="df5a5-170">Repeat hello process for any additional paths.</span></span>

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a><span data-ttu-id="df5a5-171">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="df5a5-171">Step 4.</span></span> <span data-ttu-id="df5a5-172">提供的名稱和描述 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-172">Provide a name and description for hello log</span></span>
<span data-ttu-id="df5a5-173">hello 您指定的名稱將用於 hello 記錄類型 （如上所述）。</span><span class="sxs-lookup"><span data-stu-id="df5a5-173">hello name that you specify will be used for hello log type as described above.</span></span>  <span data-ttu-id="df5a5-174">它最後一定會與 _CL toodistinguish 它做為自訂的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-174">It will always end with _CL toodistinguish it as a custom log.</span></span>

1. <span data-ttu-id="df5a5-175">輸入 hello 記錄檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="df5a5-175">Type in a name for hello log.</span></span>  <span data-ttu-id="df5a5-176">hello  **\_CL**會自動被賦予後置詞。</span><span class="sxs-lookup"><span data-stu-id="df5a5-176">hello **\_CL** suffix is automatically provided.</span></span>
2. <span data-ttu-id="df5a5-177">新增選擇性的 [描述] 。</span><span class="sxs-lookup"><span data-stu-id="df5a5-177">Add an optional **Description**.</span></span>
3. <span data-ttu-id="df5a5-178">按一下**下一步**toosave hello 自訂記錄檔定義。</span><span class="sxs-lookup"><span data-stu-id="df5a5-178">Click **Next** toosave hello custom log definition.</span></span>

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a><span data-ttu-id="df5a5-179">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="df5a5-179">Step 5.</span></span> <span data-ttu-id="df5a5-180">驗證所要收集 hello 自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-180">Validate that hello custom logs are being collected</span></span>
<span data-ttu-id="df5a5-181">它可能會佔用 tooan 小時從新的自訂記錄檔 tooappear 記錄分析中的 hello 初始資料。</span><span class="sxs-lookup"><span data-stu-id="df5a5-181">It may take up tooan hour for hello initial data from a new custom log tooappear in Log Analytics.</span></span>  <span data-ttu-id="df5a5-182">它會開始收集項目從 hello 記錄檔路徑中找到 hello 從 hello 點指定該您定義的 hello 自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-182">It will start collecting entries from hello logs found in hello path you specified from hello point that you defined hello custom log.</span></span>  <span data-ttu-id="df5a5-183">它將不會保留您上傳 hello 自訂記錄檔建立期間的 hello 項目，但它會收集 hello 找到的記錄檔中的現有項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-183">It will not retain hello entries that you uploaded during hello custom log creation, but it will collect already existing entries in hello log files that it locates.</span></span>

<span data-ttu-id="df5a5-184">一旦記錄分析會開始收集從 hello 自訂記錄檔，其記錄將會提供記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="df5a5-184">Once Log Analytics starts collecting from hello custom log, its records will be available with a Log Search.</span></span>  <span data-ttu-id="df5a5-185">使用您提供給 hello hello 做的自訂記錄檔的 hello 名稱**類型**在查詢中。</span><span class="sxs-lookup"><span data-stu-id="df5a5-185">Use hello name that you gave hello custom log as hello **Type** in your query.</span></span>

> [!NOTE]
> <span data-ttu-id="df5a5-186">如果遺漏從 hello 搜尋 hello RawData 屬性，您可能需要 tooclose，並重新開啟您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="df5a5-186">If hello RawData property is missing from hello search, you may need tooclose and reopen your browser.</span></span>
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a><span data-ttu-id="df5a5-187">步驟 6.</span><span class="sxs-lookup"><span data-stu-id="df5a5-187">Step 6.</span></span> <span data-ttu-id="df5a5-188">剖析 hello 自訂記錄項目</span><span class="sxs-lookup"><span data-stu-id="df5a5-188">Parse hello custom log entries</span></span>
<span data-ttu-id="df5a5-189">hello 整個記錄檔項目會儲存在單一屬性呼叫**RawData**。</span><span class="sxs-lookup"><span data-stu-id="df5a5-189">hello entire log entry will be stored in a single property called **RawData**.</span></span>  <span data-ttu-id="df5a5-190">您最有可能會想 tooseparate hello 不同資訊片段中每個項目插入儲存在 hello 記錄中的個別屬性。</span><span class="sxs-lookup"><span data-stu-id="df5a5-190">You will most likely want tooseparate hello different pieces of information in each entry into individual properties stored in hello record.</span></span>  <span data-ttu-id="df5a5-191">您使用 hello[自訂欄位](log-analytics-custom-fields.md)記錄分析的功能。</span><span class="sxs-lookup"><span data-stu-id="df5a5-191">You do this using hello [Custom Fields](log-analytics-custom-fields.md) feature of Log Analytics.</span></span>

<span data-ttu-id="df5a5-192">這裡不會提供詳細的步驟，以剖析 hello 自訂記錄項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-192">Detailed steps for parsing hello custom log entry are not provided here.</span></span>  <span data-ttu-id="df5a5-193">請參閱 toohello[自訂欄位](log-analytics-custom-fields.md)這項資訊的文件。</span><span class="sxs-lookup"><span data-stu-id="df5a5-193">Please refer toohello [Custom Fields](log-analytics-custom-fields.md) documentation for this information.</span></span>

## <a name="disabling-a-custom-log"></a><span data-ttu-id="df5a5-194">停用自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-194">Disabling a custom log</span></span>
<span data-ttu-id="df5a5-195">自訂記錄檔定義一旦建立就無法移除，但您可以移除其所有集合路徑來停用它。</span><span class="sxs-lookup"><span data-stu-id="df5a5-195">You cannot remove a custom log definition once it's been created, but you can disable it by removing all of its collection paths.</span></span>

1. <span data-ttu-id="df5a5-196">在 hello OMS 入口網站中，移過**設定**。</span><span class="sxs-lookup"><span data-stu-id="df5a5-196">In hello OMS portal, go too**Settings**.</span></span>
2. <span data-ttu-id="df5a5-197">按一下 [資料]，然後按一下 [自訂記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="df5a5-197">Click on **Data** and then **Custom logs**.</span></span>
3. <span data-ttu-id="df5a5-198">按一下**詳細資料**下一步 toohello 自訂記錄檔定義 toodisable。</span><span class="sxs-lookup"><span data-stu-id="df5a5-198">Click **Details** next toohello custom log definition toodisable.</span></span>
4. <span data-ttu-id="df5a5-199">移除每個 hello 自訂記錄檔定義的 hello 集合路徑。</span><span class="sxs-lookup"><span data-stu-id="df5a5-199">Remove each of hello collection paths for hello custom log definition.</span></span>

## <a name="data-collection"></a><span data-ttu-id="df5a5-200">資料收集</span><span class="sxs-lookup"><span data-stu-id="df5a5-200">Data collection</span></span>
<span data-ttu-id="df5a5-201">Log Analytics 會從每個自訂記錄檔收集新的項目，間隔大約為每 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="df5a5-201">Log Analytics will collect new entries from each custom log approximately every 5 minutes.</span></span>  <span data-ttu-id="df5a5-202">hello 代理程式將會收集每個記錄檔中記錄其所在位置。</span><span class="sxs-lookup"><span data-stu-id="df5a5-202">hello agent will record its place in each log file that it collects from.</span></span>  <span data-ttu-id="df5a5-203">如果 hello 代理程式離線一段時間，然後記錄分析將收集項目從其上次離開的地方，即使那些項目在 hello agent 離線期間所建立。</span><span class="sxs-lookup"><span data-stu-id="df5a5-203">If hello agent goes offline for a period of time, then Log Analytics will collect entries from where it last left off, even if those entries were created while hello agent was offline.</span></span>

<span data-ttu-id="df5a5-204">hello hello 記錄項目整個內容寫入 tooa 單一屬性呼叫**RawData**。</span><span class="sxs-lookup"><span data-stu-id="df5a5-204">hello entire contents of hello log entry are written tooa single property called **RawData**.</span></span>  <span data-ttu-id="df5a5-205">您可以將此剖析成多個屬性，進行分析及藉由定義分別搜尋[自訂欄位](log-analytics-custom-fields.md)建立 hello 自訂記錄檔之後。</span><span class="sxs-lookup"><span data-stu-id="df5a5-205">You can parse this into multiple properties that can be analyzed and searched separately by defining [Custom Fields](log-analytics-custom-fields.md) after you have created hello custom log.</span></span>

## <a name="custom-log-record-properties"></a><span data-ttu-id="df5a5-206">自訂記錄檔記錄的屬性</span><span class="sxs-lookup"><span data-stu-id="df5a5-206">Custom log record properties</span></span>
<span data-ttu-id="df5a5-207">自訂記錄檔記錄都有您所提供和 hello hello 下表中的屬性 hello 記錄檔名稱的型別。</span><span class="sxs-lookup"><span data-stu-id="df5a5-207">Custom log records have a type with hello log name that you provide and hello properties in hello following table.</span></span>

| <span data-ttu-id="df5a5-208">屬性</span><span class="sxs-lookup"><span data-stu-id="df5a5-208">Property</span></span> | <span data-ttu-id="df5a5-209">說明</span><span class="sxs-lookup"><span data-stu-id="df5a5-209">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df5a5-210">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="df5a5-210">TimeGenerated</span></span> |<span data-ttu-id="df5a5-211">日期和時間 hello 記錄已分析所收集的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-211">Date and time that hello record was collected by Log Analytics.</span></span>  <span data-ttu-id="df5a5-212">如果 hello 記錄檔會使用以時間為基礎的分隔符號這是從 hello 項目收集的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="df5a5-212">If hello log uses a time-based delimiter then this is hello time collected from hello entry.</span></span> |
| <span data-ttu-id="df5a5-213">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="df5a5-213">SourceSystem</span></span> |<span data-ttu-id="df5a5-214">從收集的代理程式 hello 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="df5a5-214">Type of agent hello record was collected from.</span></span> <br> <span data-ttu-id="df5a5-215">OpsManager - Windows 代理程式，直接連線或由 System Center Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="df5a5-215">OpsManager – Windows agent, either direct connect or System Center Operations Manager</span></span> <br> <span data-ttu-id="df5a5-216">Linux – 所有的 Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="df5a5-216">Linux – All Linux agents</span></span> |
| <span data-ttu-id="df5a5-217">RawData</span><span class="sxs-lookup"><span data-stu-id="df5a5-217">RawData</span></span> |<span data-ttu-id="df5a5-218">全文檢索的 hello 收集項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-218">Full text of hello collected entry.</span></span> |
| <span data-ttu-id="df5a5-219">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="df5a5-219">ManagementGroupName</span></span> |<span data-ttu-id="df5a5-220">System Center Operations Manage agents hello 管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="df5a5-220">Name of hello management group for System Center Operations Manage agents.</span></span>  <span data-ttu-id="df5a5-221">若為其他代理程式，此為 AOI-\<工作區 ID\></span><span class="sxs-lookup"><span data-stu-id="df5a5-221">For other agents, this is AOI-\<workspace ID\></span></span> |

## <a name="log-searches-with-custom-log-records"></a><span data-ttu-id="df5a5-222">使用自訂記錄檔記錄來記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="df5a5-222">Log searches with custom log records</span></span>
<span data-ttu-id="df5a5-223">從自訂的記錄檔的記錄會儲存在 hello OMS 儲存機制，就像任何其他資料來源的記錄。</span><span class="sxs-lookup"><span data-stu-id="df5a5-223">Records from custom logs are stored in hello OMS repository just like records from any other data source.</span></span>  <span data-ttu-id="df5a5-224">這些使用者必須符合您提供當您定義 hello 記錄檔中，因此您可以使用 hello 類型屬性搜尋 tooretrieve 記錄收集從特定的記錄檔中的 hello 名稱的類型。</span><span class="sxs-lookup"><span data-stu-id="df5a5-224">They will have a type matching hello name that you provide when you define hello log, so you can use hello Type property in your search tooretrieve records collected from a specific log.</span></span>

<span data-ttu-id="df5a5-225">hello 下表提供的自訂記錄檔從擷取記錄的記錄搜尋不同的範例。</span><span class="sxs-lookup"><span data-stu-id="df5a5-225">hello following table provides different examples of log searches that retrieve records from custom logs.</span></span>

| <span data-ttu-id="df5a5-226">查詢</span><span class="sxs-lookup"><span data-stu-id="df5a5-226">Query</span></span> | <span data-ttu-id="df5a5-227">說明</span><span class="sxs-lookup"><span data-stu-id="df5a5-227">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df5a5-228">Type=MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="df5a5-228">Type=MyApp_CL</span></span> |<span data-ttu-id="df5a5-229">所有事件來自名為 MyApp_CL 的自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-229">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="df5a5-230">Type=MyApp_CL Severity_CF=error</span><span class="sxs-lookup"><span data-stu-id="df5a5-230">Type=MyApp_CL Severity_CF=error</span></span> |<span data-ttu-id="df5a5-231">來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="df5a5-231">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |

>[!NOTE]
> <span data-ttu-id="df5a5-232">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="df5a5-232">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="df5a5-233">查詢</span><span class="sxs-lookup"><span data-stu-id="df5a5-233">Query</span></span> | <span data-ttu-id="df5a5-234">說明</span><span class="sxs-lookup"><span data-stu-id="df5a5-234">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="df5a5-235">MyApp_CL</span><span class="sxs-lookup"><span data-stu-id="df5a5-235">MyApp_CL</span></span> |<span data-ttu-id="df5a5-236">所有事件來自名為 MyApp_CL 的自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df5a5-236">All events from a custom log named MyApp_CL.</span></span> |
| <span data-ttu-id="df5a5-237">MyApp_CL &#124; where Severity_CF=="error"</span><span class="sxs-lookup"><span data-stu-id="df5a5-237">MyApp_CL &#124; where Severity_CF=="error"</span></span> |<span data-ttu-id="df5a5-238">來自 MyApp_CL 自訂記錄檔且在 *Severity_CF* 自訂欄位中的值為 *error* 的所有事件。</span><span class="sxs-lookup"><span data-stu-id="df5a5-238">All events from a custom log named MyApp_CL with a value of *error* in a custom field named *Severity_CF*.</span></span> |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a><span data-ttu-id="df5a5-239">新增自訂記錄檔的範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="df5a5-239">Sample walkthrough of adding a custom log</span></span>
<span data-ttu-id="df5a5-240">hello 下一節逐步解說建立自訂的記錄檔的範例。</span><span class="sxs-lookup"><span data-stu-id="df5a5-240">hello following section walks through an example of creating a custom log.</span></span>  <span data-ttu-id="df5a5-241">hello 範例記錄檔收集對每一行開頭的日期和時間，並接著以逗號分隔的程式碼、 狀態及訊息欄位的單一項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-241">hello sample log being collected has a single entry on each line starting with a date and time and then comma-delimited fields for code, status, and message.</span></span>  <span data-ttu-id="df5a5-242">下面顯示了幾個範例項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-242">Several sample entries are shown below.</span></span>

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a><span data-ttu-id="df5a5-243">上傳和剖析範例記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-243">Upload and parse a sample log</span></span>
<span data-ttu-id="df5a5-244">我們提供一個 hello 記錄檔，可以看到 hello 將收集的事件。</span><span class="sxs-lookup"><span data-stu-id="df5a5-244">We provide one of hello log files and can see hello events that it will be collecting.</span></span>  <span data-ttu-id="df5a5-245">在此案例中，新行字元足以做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="df5a5-245">In this case New Line is a sufficient delimiter.</span></span>  <span data-ttu-id="df5a5-246">如果 hello 記錄檔中的單一項目無法透過跨越多行，則時間戳記分隔符號需要 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="df5a5-246">If a single entry in hello log could span multiple lines though, then a timestamp delimiter would need toobe used.</span></span>

![上傳和剖析範例記錄檔](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a><span data-ttu-id="df5a5-248">新增記錄檔收集路徑</span><span class="sxs-lookup"><span data-stu-id="df5a5-248">Add log collection paths</span></span>
<span data-ttu-id="df5a5-249">hello 記錄檔會位於*C:\MyApp\Logs*。</span><span class="sxs-lookup"><span data-stu-id="df5a5-249">hello log files will be located in *C:\MyApp\Logs*.</span></span>  <span data-ttu-id="df5a5-250">包含 hello 日期 hello 模式中的名稱與每一天會建立新的檔案*appYYYYMMDD.log*。</span><span class="sxs-lookup"><span data-stu-id="df5a5-250">A new file will be created each day with a name that includes hello date in hello pattern *appYYYYMMDD.log*.</span></span>  <span data-ttu-id="df5a5-251">此記錄檔的完整模式為 *C:\MyApp\Logs\\\*.log*。</span><span class="sxs-lookup"><span data-stu-id="df5a5-251">A sufficient pattern for this log would be *C:\MyApp\Logs\\\*.log*.</span></span>

![記錄檔收集路徑](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a><span data-ttu-id="df5a5-253">提供的名稱和描述 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-253">Provide a name and description for hello log</span></span>
<span data-ttu-id="df5a5-254">我們使用 *MyApp_CL* 這個名稱並輸入 [描述]。</span><span class="sxs-lookup"><span data-stu-id="df5a5-254">We use a name of *MyApp_CL* and type in a **Description**.</span></span>

![記錄檔名稱](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a><span data-ttu-id="df5a5-256">驗證所要收集 hello 自訂記錄檔</span><span class="sxs-lookup"><span data-stu-id="df5a5-256">Validate that hello custom logs are being collected</span></span>
<span data-ttu-id="df5a5-257">我們使用的查詢*類型 = MyApp_CL* tooreturn 所有記錄從 hello 收集的記錄。</span><span class="sxs-lookup"><span data-stu-id="df5a5-257">We use a query of *Type=MyApp_CL* tooreturn all records from hello collected log.</span></span>

![無自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a><span data-ttu-id="df5a5-259">剖析 hello 自訂記錄項目</span><span class="sxs-lookup"><span data-stu-id="df5a5-259">Parse hello custom log entries</span></span>
<span data-ttu-id="df5a5-260">我們使用自訂欄位 toodefine hello *EventTime*，*程式碼*，*狀態*，和*訊息*欄位，而且我們可以看到 hello hello 差異hello 查詢所傳回的記錄。</span><span class="sxs-lookup"><span data-stu-id="df5a5-260">We use Custom Fields toodefine hello *EventTime*, *Code*, *Status*, and *Message* fields and we can see hello difference in hello records that are returned by hello query.</span></span>

![有自訂欄位的記錄檔查詢](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a><span data-ttu-id="df5a5-262">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df5a5-262">Next steps</span></span>
* <span data-ttu-id="df5a5-263">使用[自訂欄位](log-analytics-custom-fields.md)tooparse hello hello tooindividual 欄位中的自訂記錄項目。</span><span class="sxs-lookup"><span data-stu-id="df5a5-263">Use [Custom Fields](log-analytics-custom-fields.md) tooparse hello entries in hello custom log in tooindividual fields.</span></span>
* <span data-ttu-id="df5a5-264">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="df5a5-264">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
