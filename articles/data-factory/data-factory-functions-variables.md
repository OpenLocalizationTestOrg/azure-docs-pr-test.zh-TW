---
title: "aaaData Factory 函式和系統變數 |Microsoft 文件"
description: "提供 Azure Data Factory 函式與系統變數清單"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="90837-103">Azure Data Factory - 函式與系統變數</span><span class="sxs-lookup"><span data-stu-id="90837-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="90837-104">本文提供 Azure Data Factory 支援之函式和變數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="90837-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="90837-105">Data Factory 系統變數</span><span class="sxs-lookup"><span data-stu-id="90837-105">Data Factory system variables</span></span>
| <span data-ttu-id="90837-106">變數名稱</span><span class="sxs-lookup"><span data-stu-id="90837-106">Variable Name</span></span> | <span data-ttu-id="90837-107">說明</span><span class="sxs-lookup"><span data-stu-id="90837-107">Description</span></span> | <span data-ttu-id="90837-108">物件範圍</span><span class="sxs-lookup"><span data-stu-id="90837-108">Object Scope</span></span> | <span data-ttu-id="90837-109">JSON 範圍和使用案例</span><span class="sxs-lookup"><span data-stu-id="90837-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90837-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="90837-110">WindowStart</span></span> |<span data-ttu-id="90837-111">目前活動執行時段的時間間隔開始</span><span class="sxs-lookup"><span data-stu-id="90837-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="90837-112">活動</span><span class="sxs-lookup"><span data-stu-id="90837-112">activity</span></span> |<ol><li><span data-ttu-id="90837-113">指定資料選取範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="90837-113">Specify data selection queries.</span></span> <span data-ttu-id="90837-114">請參閱 hello 中參考的連接器文件[資料移動活動](data-factory-data-movement-activities.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="90837-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="90837-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="90837-115">WindowEnd</span></span> |<span data-ttu-id="90837-116">目前活動執行時段的時間間隔結束</span><span class="sxs-lookup"><span data-stu-id="90837-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="90837-117">活動</span><span class="sxs-lookup"><span data-stu-id="90837-117">activity</span></span> |<span data-ttu-id="90837-118">與 WindowStart 相同。</span><span class="sxs-lookup"><span data-stu-id="90837-118">same as WindowStart.</span></span> |
| <span data-ttu-id="90837-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="90837-119">SliceStart</span></span> |<span data-ttu-id="90837-120">所產生之資料配量的時間間隔開始</span><span class="sxs-lookup"><span data-stu-id="90837-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="90837-121">活動</span><span class="sxs-lookup"><span data-stu-id="90837-121">activity</span></span><br/><span data-ttu-id="90837-122">資料集</span><span class="sxs-lookup"><span data-stu-id="90837-122">dataset</span></span> |<ol><li><span data-ttu-id="90837-123">指定使用 [Azure Blob](data-factory-azure-blob-connector.md) 和[檔案系統資料集](data-factory-onprem-file-system-connector.md)時的動態資料夾路徑與檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="90837-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="90837-124">使用 Data Factory 函式在活動輸入集合中指定輸入相依性。</span><span class="sxs-lookup"><span data-stu-id="90837-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="90837-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="90837-125">SliceEnd</span></span> |<span data-ttu-id="90837-126">目前資料配量的時間間隔結束。</span><span class="sxs-lookup"><span data-stu-id="90837-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="90837-127">活動</span><span class="sxs-lookup"><span data-stu-id="90837-127">activity</span></span><br/><span data-ttu-id="90837-128">資料集</span><span class="sxs-lookup"><span data-stu-id="90837-128">dataset</span></span> |<span data-ttu-id="90837-129">與 SliceStart 相同。</span><span class="sxs-lookup"><span data-stu-id="90837-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="90837-130">目前資料 factory 需要該 hello 排程中指定的 hello 活動與 hello 排程 hello 輸出資料集中的可用性中指定完全相符。</span><span class="sxs-lookup"><span data-stu-id="90837-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="90837-131">因此，WindowStart、 WindowEnd，SliceStart 和 SliceEnd 一律對應 toohello 相同時間週期和單一輸出配量。</span><span class="sxs-lookup"><span data-stu-id="90837-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="90837-132">使用系統變數的範例</span><span class="sxs-lookup"><span data-stu-id="90837-132">Example for using a system variable</span></span>
<span data-ttu-id="90837-133">在下列範例中，年、 月、 日和時間的 hello **SliceStart**會擷取至不同的變數，可供**folderPath**和**fileName**屬性。</span><span class="sxs-lookup"><span data-stu-id="90837-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="90837-134">Data Factory 函式</span><span class="sxs-lookup"><span data-stu-id="90837-134">Data Factory functions</span></span>
<span data-ttu-id="90837-135">您可以使用 data factory，以及系統變數中的函式 hello 下列用途：</span><span class="sxs-lookup"><span data-stu-id="90837-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="90837-136">指定資料選取項目查詢 (請參閱 hello 所參考的連接器文件[資料移動活動](data-factory-data-movement-activities.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="90837-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="90837-137">hello 資料 factory 函式的語法 tooinvoke:  **$$ <function>** 資料選取項目查詢和在 hello 活動和資料集中的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="90837-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="90837-138">使用 Data Factory 函式在活動輸入集合中指定輸入相依性。</span><span class="sxs-lookup"><span data-stu-id="90837-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="90837-139">指定輸入相依性運算式不需要 $$。</span><span class="sxs-lookup"><span data-stu-id="90837-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="90837-140">在下列範例中，hello **sqlReaderQuery** hello 所傳回的 tooa 值指派給屬性的 JSON 檔案中`Text.Format`函式。</span><span class="sxs-lookup"><span data-stu-id="90837-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="90837-141">此範例也會使用系統變數，名為**WindowStart**，代表 hello hello 活動執行視窗開始時間。</span><span class="sxs-lookup"><span data-stu-id="90837-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="90837-142">請參閱說明可使用的各種格式化選項 (例如：ay 與 yyyy) 的[自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="90837-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="90837-143">Functions</span><span class="sxs-lookup"><span data-stu-id="90837-143">Functions</span></span>
<span data-ttu-id="90837-144">hello 下表列出所有 Azure Data Factory 中的 hello 函式：</span><span class="sxs-lookup"><span data-stu-id="90837-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="90837-145">類別</span><span class="sxs-lookup"><span data-stu-id="90837-145">Category</span></span> | <span data-ttu-id="90837-146">函式</span><span class="sxs-lookup"><span data-stu-id="90837-146">Function</span></span> | <span data-ttu-id="90837-147">參數</span><span class="sxs-lookup"><span data-stu-id="90837-147">Parameters</span></span> | <span data-ttu-id="90837-148">說明</span><span class="sxs-lookup"><span data-stu-id="90837-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90837-149">時間</span><span class="sxs-lookup"><span data-stu-id="90837-149">Time</span></span> |<span data-ttu-id="90837-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-150">AddHours(X,Y)</span></span> |<span data-ttu-id="90837-151">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="90837-152">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-152">Y: int</span></span> |<span data-ttu-id="90837-153">將 Y 小時 toohello 特定時間 X。</span><span class="sxs-lookup"><span data-stu-id="90837-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="90837-154">範例： `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="90837-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="90837-155">時間</span><span class="sxs-lookup"><span data-stu-id="90837-155">Time</span></span> |<span data-ttu-id="90837-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="90837-157">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="90837-158">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-158">Y: int</span></span> |<span data-ttu-id="90837-159">將 Y 分鐘 tooX。</span><span class="sxs-lookup"><span data-stu-id="90837-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="90837-160">範例： `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="90837-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="90837-161">時間</span><span class="sxs-lookup"><span data-stu-id="90837-161">Time</span></span> |<span data-ttu-id="90837-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="90837-162">StartOfHour(X)</span></span> |<span data-ttu-id="90837-163">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-163">X: Datetime</span></span> |<span data-ttu-id="90837-164">取得 hello 啟動 X hello 小時元件所代表的 hello 小時的時間。</span><span class="sxs-lookup"><span data-stu-id="90837-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="90837-165">範例： `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="90837-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="90837-166">日期</span><span class="sxs-lookup"><span data-stu-id="90837-166">Date</span></span> |<span data-ttu-id="90837-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-167">AddDays(X,Y)</span></span> |<span data-ttu-id="90837-168">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-168">X: DateTime</span></span><br/><br/><span data-ttu-id="90837-169">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-169">Y: int</span></span> |<span data-ttu-id="90837-170">將 Y 天 tooX。</span><span class="sxs-lookup"><span data-stu-id="90837-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="90837-171">範例：9/15/2013 12:00:00 PM + 2 天 = 9/17/2013 12:00:00 PM。</span><span class="sxs-lookup"><span data-stu-id="90837-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="90837-172">您也可以藉由將 Y 指定為負數來減去天。</span><span class="sxs-lookup"><span data-stu-id="90837-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="90837-173">範例：`9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="90837-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="90837-174">日期</span><span class="sxs-lookup"><span data-stu-id="90837-174">Date</span></span> |<span data-ttu-id="90837-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="90837-176">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-176">X: DateTime</span></span><br/><br/><span data-ttu-id="90837-177">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-177">Y: int</span></span> |<span data-ttu-id="90837-178">將 Y 個月 tooX。</span><span class="sxs-lookup"><span data-stu-id="90837-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="90837-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`。</span><span class="sxs-lookup"><span data-stu-id="90837-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="90837-180">您也可以藉由將 Y 指定為負數來減去月份。</span><span class="sxs-lookup"><span data-stu-id="90837-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="90837-181">範例：`9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="90837-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="90837-182">日期</span><span class="sxs-lookup"><span data-stu-id="90837-182">Date</span></span> |<span data-ttu-id="90837-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="90837-184">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="90837-185">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-185">Y: int</span></span> |<span data-ttu-id="90837-186">將 Y * 3 個月 tooX。</span><span class="sxs-lookup"><span data-stu-id="90837-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="90837-187">範例： `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="90837-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="90837-188">日期</span><span class="sxs-lookup"><span data-stu-id="90837-188">Date</span></span> |<span data-ttu-id="90837-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="90837-190">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-190">X: DateTime</span></span><br/><br/><span data-ttu-id="90837-191">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-191">Y: int</span></span> |<span data-ttu-id="90837-192">將 Y * 7 天 tooX</span><span class="sxs-lookup"><span data-stu-id="90837-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="90837-193">範例：9/15/2013 12:00:00 PM + 1 週 = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="90837-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="90837-194">您也可以藉由將 Y 指定為負數來減去週。</span><span class="sxs-lookup"><span data-stu-id="90837-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="90837-195">範例：`9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="90837-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="90837-196">日期</span><span class="sxs-lookup"><span data-stu-id="90837-196">Date</span></span> |<span data-ttu-id="90837-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="90837-197">AddYears(X,Y)</span></span> |<span data-ttu-id="90837-198">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-198">X: DateTime</span></span><br/><br/><span data-ttu-id="90837-199">Y：int</span><span class="sxs-lookup"><span data-stu-id="90837-199">Y: int</span></span> |<span data-ttu-id="90837-200">將 Y 年 tooX。</span><span class="sxs-lookup"><span data-stu-id="90837-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="90837-201">您也可以藉由將 Y 指定為負數來減去年。</span><span class="sxs-lookup"><span data-stu-id="90837-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="90837-202">範例：`9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="90837-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="90837-203">日期</span><span class="sxs-lookup"><span data-stu-id="90837-203">Date</span></span> |<span data-ttu-id="90837-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="90837-204">Day(X)</span></span> |<span data-ttu-id="90837-205">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-205">X: DateTime</span></span> |<span data-ttu-id="90837-206">取得 X 的 hello 日期元件。</span><span class="sxs-lookup"><span data-stu-id="90837-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="90837-207">範例：`Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="90837-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="90837-208">日期</span><span class="sxs-lookup"><span data-stu-id="90837-208">Date</span></span> |<span data-ttu-id="90837-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="90837-209">DayOfWeek(X)</span></span> |<span data-ttu-id="90837-210">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-210">X: DateTime</span></span> |<span data-ttu-id="90837-211">取得 X 的星期幾元件 hello 日期。</span><span class="sxs-lookup"><span data-stu-id="90837-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="90837-212">範例：`DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="90837-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="90837-213">日期</span><span class="sxs-lookup"><span data-stu-id="90837-213">Date</span></span> |<span data-ttu-id="90837-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="90837-214">DayOfYear(X)</span></span> |<span data-ttu-id="90837-215">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-215">X: DateTime</span></span> |<span data-ttu-id="90837-216">取得 X hello 年度元件所代表的 hello 年中的 hello 一天。</span><span class="sxs-lookup"><span data-stu-id="90837-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="90837-217">範例：</span><span class="sxs-lookup"><span data-stu-id="90837-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="90837-218">日期</span><span class="sxs-lookup"><span data-stu-id="90837-218">Date</span></span> |<span data-ttu-id="90837-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="90837-219">DaysInMonth(X)</span></span> |<span data-ttu-id="90837-220">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-220">X: DateTime</span></span> |<span data-ttu-id="90837-221">取得參數 X 的 hello 月份元件所代表的 hello 月份中的 hello 日期。</span><span class="sxs-lookup"><span data-stu-id="90837-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="90837-222">範例：`DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="90837-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="90837-223">日期</span><span class="sxs-lookup"><span data-stu-id="90837-223">Date</span></span> |<span data-ttu-id="90837-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="90837-224">EndOfDay(X)</span></span> |<span data-ttu-id="90837-225">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-225">X: DateTime</span></span> |<span data-ttu-id="90837-226">取得 hello 日期-時間表示 hello X hello 日期 （日期元件） 的結尾。</span><span class="sxs-lookup"><span data-stu-id="90837-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="90837-227">範例：`EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="90837-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="90837-228">日期</span><span class="sxs-lookup"><span data-stu-id="90837-228">Date</span></span> |<span data-ttu-id="90837-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="90837-229">EndOfMonth(X)</span></span> |<span data-ttu-id="90837-230">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-230">X: DateTime</span></span> |<span data-ttu-id="90837-231">取得參數 X 的月份元件所代表的 hello 月份 hello 末端。</span><span class="sxs-lookup"><span data-stu-id="90837-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="90837-232">範例： `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` （日期，代表 hello 九月份結束的時間）</span><span class="sxs-lookup"><span data-stu-id="90837-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="90837-233">Date</span><span class="sxs-lookup"><span data-stu-id="90837-233">Date</span></span> |<span data-ttu-id="90837-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="90837-234">StartOfDay(X)</span></span> |<span data-ttu-id="90837-235">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-235">X: DateTime</span></span> |<span data-ttu-id="90837-236">取得參數 X 的 hello 日期元件所代表的 hello 天 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="90837-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="90837-237">範例：`StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="90837-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="90837-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="90837-238">DateTime</span></span> |<span data-ttu-id="90837-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="90837-239">From(X)</span></span> |<span data-ttu-id="90837-240">X：字串</span><span class="sxs-lookup"><span data-stu-id="90837-240">X: String</span></span> |<span data-ttu-id="90837-241">剖析字串 X tooa 日期時間。</span><span class="sxs-lookup"><span data-stu-id="90837-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="90837-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="90837-242">DateTime</span></span> |<span data-ttu-id="90837-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="90837-243">Ticks(X)</span></span> |<span data-ttu-id="90837-244">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="90837-244">X: DateTime</span></span> |<span data-ttu-id="90837-245">取得 hello 刻度 hello 參數 X 的屬性。一個刻度等於 100 奈秒。</span><span class="sxs-lookup"><span data-stu-id="90837-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="90837-246">hello 這個屬性的值代表 hello 0001 年 1 月 1 日的 12:00:00 午夜以來已經過的刻度數目。</span><span class="sxs-lookup"><span data-stu-id="90837-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="90837-247">文字</span><span class="sxs-lookup"><span data-stu-id="90837-247">Text</span></span> |<span data-ttu-id="90837-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="90837-248">Format(X)</span></span> |<span data-ttu-id="90837-249">X：字串變數</span><span class="sxs-lookup"><span data-stu-id="90837-249">X: String variable</span></span> |<span data-ttu-id="90837-250">格式 hello 文字 (使用`\\'`組合 tooescape`'`字元)。</span><span class="sxs-lookup"><span data-stu-id="90837-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="90837-251">當使用另一個函式內的函式時，您不需要 toouse  **$$**  hello 內部函式的前置詞。</span><span class="sxs-lookup"><span data-stu-id="90837-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="90837-252">例如：$$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="90837-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="90837-253">在此範例中，注意 **$$** 前置詞不能用於 hello **Time.AddHours**函式。</span><span class="sxs-lookup"><span data-stu-id="90837-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="90837-254">範例</span><span class="sxs-lookup"><span data-stu-id="90837-254">Example</span></span>
<span data-ttu-id="90837-255">在 hello hello Hive 活動的下列範例中，輸入和輸出參數會決定使用 hello`Text.Format`函式和 SliceStart 系統變數。</span><span class="sxs-lookup"><span data-stu-id="90837-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="90837-256">範例 2</span><span class="sxs-lookup"><span data-stu-id="90837-256">Example 2</span></span>

<span data-ttu-id="90837-257">在下列範例的 hello，hello 的 hello 預存程序活動由使用 hello 文字的日期時間參數。</span><span class="sxs-lookup"><span data-stu-id="90837-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="90837-258">格式函式和 hello SliceStart 變數。</span><span class="sxs-lookup"><span data-stu-id="90837-258">Format function and hello SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="90837-259">範例 3</span><span class="sxs-lookup"><span data-stu-id="90837-259">Example 3</span></span>
<span data-ttu-id="90837-260">tooread 前一天，而不是由 hello SliceStart，天資料使用 hello AddDays 函式 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="90837-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="90837-261">請參閱說明可使用的各種格式化選項 (例如：yy 與 yyyy) 的 [自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="90837-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

