---
title: "Data Factory 函式與系統變數 | Microsoft Docs"
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
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="d800d-103">Azure Data Factory - 函式與系統變數</span><span class="sxs-lookup"><span data-stu-id="d800d-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="d800d-104">本文提供 Azure Data Factory 支援之函式和變數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d800d-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="d800d-105">Data Factory 系統變數</span><span class="sxs-lookup"><span data-stu-id="d800d-105">Data Factory system variables</span></span>
| <span data-ttu-id="d800d-106">變數名稱</span><span class="sxs-lookup"><span data-stu-id="d800d-106">Variable Name</span></span> | <span data-ttu-id="d800d-107">說明</span><span class="sxs-lookup"><span data-stu-id="d800d-107">Description</span></span> | <span data-ttu-id="d800d-108">物件範圍</span><span class="sxs-lookup"><span data-stu-id="d800d-108">Object Scope</span></span> | <span data-ttu-id="d800d-109">JSON 範圍和使用案例</span><span class="sxs-lookup"><span data-stu-id="d800d-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d800d-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="d800d-110">WindowStart</span></span> |<span data-ttu-id="d800d-111">目前活動執行時段的時間間隔開始</span><span class="sxs-lookup"><span data-stu-id="d800d-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="d800d-112">活動</span><span class="sxs-lookup"><span data-stu-id="d800d-112">activity</span></span> |<ol><li><span data-ttu-id="d800d-113">指定資料選取範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="d800d-113">Specify data selection queries.</span></span> <span data-ttu-id="d800d-114">請參閱[資料移動活動](data-factory-data-movement-activities.md)文章中參考的連接器文章。</span><span class="sxs-lookup"><span data-stu-id="d800d-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="d800d-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="d800d-115">WindowEnd</span></span> |<span data-ttu-id="d800d-116">目前活動執行時段的時間間隔結束</span><span class="sxs-lookup"><span data-stu-id="d800d-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="d800d-117">活動</span><span class="sxs-lookup"><span data-stu-id="d800d-117">activity</span></span> |<span data-ttu-id="d800d-118">與 WindowStart 相同。</span><span class="sxs-lookup"><span data-stu-id="d800d-118">same as WindowStart.</span></span> |
| <span data-ttu-id="d800d-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="d800d-119">SliceStart</span></span> |<span data-ttu-id="d800d-120">所產生之資料配量的時間間隔開始</span><span class="sxs-lookup"><span data-stu-id="d800d-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="d800d-121">活動</span><span class="sxs-lookup"><span data-stu-id="d800d-121">activity</span></span><br/><span data-ttu-id="d800d-122">資料集</span><span class="sxs-lookup"><span data-stu-id="d800d-122">dataset</span></span> |<ol><li><span data-ttu-id="d800d-123">指定使用 [Azure Blob](data-factory-azure-blob-connector.md) 和[檔案系統資料集](data-factory-onprem-file-system-connector.md)時的動態資料夾路徑與檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="d800d-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="d800d-124">使用 Data Factory 函式在活動輸入集合中指定輸入相依性。</span><span class="sxs-lookup"><span data-stu-id="d800d-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="d800d-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="d800d-125">SliceEnd</span></span> |<span data-ttu-id="d800d-126">目前資料配量的時間間隔結束。</span><span class="sxs-lookup"><span data-stu-id="d800d-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="d800d-127">活動</span><span class="sxs-lookup"><span data-stu-id="d800d-127">activity</span></span><br/><span data-ttu-id="d800d-128">資料集</span><span class="sxs-lookup"><span data-stu-id="d800d-128">dataset</span></span> |<span data-ttu-id="d800d-129">與 SliceStart 相同。</span><span class="sxs-lookup"><span data-stu-id="d800d-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="d800d-130">目前 Data Factory 需要活動中指定的排程與輸出資料集之可用性中指定的排程完全相符。</span><span class="sxs-lookup"><span data-stu-id="d800d-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="d800d-131">因此，WindowStart、WindowEnd、SliceStart 與 SliceEnd 一律對應到相同的時間期間和單一輸出配量。</span><span class="sxs-lookup"><span data-stu-id="d800d-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="d800d-132">使用系統變數的範例</span><span class="sxs-lookup"><span data-stu-id="d800d-132">Example for using a system variable</span></span>
<span data-ttu-id="d800d-133">在下列範例中，**SliceStart** 的年、月、日和時間會擷取到 **folderPath** 和 **fileName** 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="d800d-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="d800d-134">Data Factory 函式</span><span class="sxs-lookup"><span data-stu-id="d800d-134">Data Factory functions</span></span>
<span data-ttu-id="d800d-135">您可以針對下列目的搭配使用 Data Factory 中的函式與系統變數：</span><span class="sxs-lookup"><span data-stu-id="d800d-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="d800d-136">指定資料選取範圍查詢 (請參閱 [資料移動活動](data-factory-data-movement-activities.md) 文章中參考的連接器文章)。</span><span class="sxs-lookup"><span data-stu-id="d800d-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="d800d-137">針對資料選取範圍查詢和活動與資料集中的其他屬性，叫用 Data Factory 函式的語法是： **$$<function>** 。</span><span class="sxs-lookup"><span data-stu-id="d800d-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="d800d-138">使用 Data Factory 函式在活動輸入集合中指定輸入相依性。</span><span class="sxs-lookup"><span data-stu-id="d800d-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="d800d-139">指定輸入相依性運算式不需要 $$。</span><span class="sxs-lookup"><span data-stu-id="d800d-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="d800d-140">在下列範例中，JSON 檔案中的 **sqlReaderQuery** 屬性指派給 `Text.Format` 函式所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="d800d-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="d800d-141">此範例也會使用名為 **WindowStart**的系統變數，它代表活動執行時段的開始時間。</span><span class="sxs-lookup"><span data-stu-id="d800d-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="d800d-142">請參閱說明可使用的各種格式化選項 (例如：ay 與 yyyy) 的[自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="d800d-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="d800d-143">Functions</span><span class="sxs-lookup"><span data-stu-id="d800d-143">Functions</span></span>
<span data-ttu-id="d800d-144">下表列出 Azure Data Factory 中的所有函式：</span><span class="sxs-lookup"><span data-stu-id="d800d-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="d800d-145">類別</span><span class="sxs-lookup"><span data-stu-id="d800d-145">Category</span></span> | <span data-ttu-id="d800d-146">函式</span><span class="sxs-lookup"><span data-stu-id="d800d-146">Function</span></span> | <span data-ttu-id="d800d-147">參數</span><span class="sxs-lookup"><span data-stu-id="d800d-147">Parameters</span></span> | <span data-ttu-id="d800d-148">說明</span><span class="sxs-lookup"><span data-stu-id="d800d-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d800d-149">時間</span><span class="sxs-lookup"><span data-stu-id="d800d-149">Time</span></span> |<span data-ttu-id="d800d-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-150">AddHours(X,Y)</span></span> |<span data-ttu-id="d800d-151">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="d800d-152">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-152">Y: int</span></span> |<span data-ttu-id="d800d-153">將 Y 小時新增至指定時間 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="d800d-154">範例：`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="d800d-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="d800d-155">時間</span><span class="sxs-lookup"><span data-stu-id="d800d-155">Time</span></span> |<span data-ttu-id="d800d-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="d800d-157">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="d800d-158">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-158">Y: int</span></span> |<span data-ttu-id="d800d-159">將 Y 分鐘新增至 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="d800d-160">範例：`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="d800d-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="d800d-161">時間</span><span class="sxs-lookup"><span data-stu-id="d800d-161">Time</span></span> |<span data-ttu-id="d800d-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-162">StartOfHour(X)</span></span> |<span data-ttu-id="d800d-163">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-163">X: Datetime</span></span> |<span data-ttu-id="d800d-164">取得 X 之小時元件代表的小時開始時間。</span><span class="sxs-lookup"><span data-stu-id="d800d-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="d800d-165">範例：`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="d800d-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="d800d-166">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-166">Date</span></span> |<span data-ttu-id="d800d-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-167">AddDays(X,Y)</span></span> |<span data-ttu-id="d800d-168">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-168">X: DateTime</span></span><br/><br/><span data-ttu-id="d800d-169">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-169">Y: int</span></span> |<span data-ttu-id="d800d-170">將 Y 天數新增至 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="d800d-171">範例：9/15/2013 12:00:00 PM + 2 天 = 9/17/2013 12:00:00 PM。</span><span class="sxs-lookup"><span data-stu-id="d800d-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="d800d-172">您也可以藉由將 Y 指定為負數來減去天。</span><span class="sxs-lookup"><span data-stu-id="d800d-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="d800d-173">範例：`9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="d800d-174">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-174">Date</span></span> |<span data-ttu-id="d800d-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="d800d-176">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-176">X: DateTime</span></span><br/><br/><span data-ttu-id="d800d-177">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-177">Y: int</span></span> |<span data-ttu-id="d800d-178">將 Y 月數新增至 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="d800d-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`。</span><span class="sxs-lookup"><span data-stu-id="d800d-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="d800d-180">您也可以藉由將 Y 指定為負數來減去月份。</span><span class="sxs-lookup"><span data-stu-id="d800d-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="d800d-181">範例：`9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="d800d-182">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-182">Date</span></span> |<span data-ttu-id="d800d-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="d800d-184">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="d800d-185">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-185">Y: int</span></span> |<span data-ttu-id="d800d-186">將 Y * 3 個月新增至 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="d800d-187">範例：`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="d800d-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="d800d-188">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-188">Date</span></span> |<span data-ttu-id="d800d-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="d800d-190">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-190">X: DateTime</span></span><br/><br/><span data-ttu-id="d800d-191">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-191">Y: int</span></span> |<span data-ttu-id="d800d-192">將 Y * 7 天新增至 X</span><span class="sxs-lookup"><span data-stu-id="d800d-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="d800d-193">範例：9/15/2013 12:00:00 PM + 1 週 = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="d800d-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="d800d-194">您也可以藉由將 Y 指定為負數來減去週。</span><span class="sxs-lookup"><span data-stu-id="d800d-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="d800d-195">範例：`9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="d800d-196">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-196">Date</span></span> |<span data-ttu-id="d800d-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="d800d-197">AddYears(X,Y)</span></span> |<span data-ttu-id="d800d-198">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-198">X: DateTime</span></span><br/><br/><span data-ttu-id="d800d-199">Y：int</span><span class="sxs-lookup"><span data-stu-id="d800d-199">Y: int</span></span> |<span data-ttu-id="d800d-200">將 Y 年新增至 X。</span><span class="sxs-lookup"><span data-stu-id="d800d-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="d800d-201">您也可以藉由將 Y 指定為負數來減去年。</span><span class="sxs-lookup"><span data-stu-id="d800d-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="d800d-202">範例：`9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="d800d-203">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-203">Date</span></span> |<span data-ttu-id="d800d-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-204">Day(X)</span></span> |<span data-ttu-id="d800d-205">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-205">X: DateTime</span></span> |<span data-ttu-id="d800d-206">取得 X 的日元件。</span><span class="sxs-lookup"><span data-stu-id="d800d-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="d800d-207">範例：`Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="d800d-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="d800d-208">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-208">Date</span></span> |<span data-ttu-id="d800d-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-209">DayOfWeek(X)</span></span> |<span data-ttu-id="d800d-210">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-210">X: DateTime</span></span> |<span data-ttu-id="d800d-211">取得 X 的週中日元件。</span><span class="sxs-lookup"><span data-stu-id="d800d-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="d800d-212">範例：`DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="d800d-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="d800d-213">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-213">Date</span></span> |<span data-ttu-id="d800d-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-214">DayOfYear(X)</span></span> |<span data-ttu-id="d800d-215">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-215">X: DateTime</span></span> |<span data-ttu-id="d800d-216">取得 X 之年元件代表的一年當中日期。</span><span class="sxs-lookup"><span data-stu-id="d800d-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="d800d-217">範例：</span><span class="sxs-lookup"><span data-stu-id="d800d-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="d800d-218">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-218">Date</span></span> |<span data-ttu-id="d800d-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-219">DaysInMonth(X)</span></span> |<span data-ttu-id="d800d-220">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-220">X: DateTime</span></span> |<span data-ttu-id="d800d-221">取得參數 X 之月元件代表的月份中日期。</span><span class="sxs-lookup"><span data-stu-id="d800d-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="d800d-222">範例：`DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="d800d-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="d800d-223">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-223">Date</span></span> |<span data-ttu-id="d800d-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-224">EndOfDay(X)</span></span> |<span data-ttu-id="d800d-225">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-225">X: DateTime</span></span> |<span data-ttu-id="d800d-226">取得 X 之結尾天數 (日元件) 代表的日期時間。</span><span class="sxs-lookup"><span data-stu-id="d800d-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="d800d-227">範例：`EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="d800d-228">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-228">Date</span></span> |<span data-ttu-id="d800d-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-229">EndOfMonth(X)</span></span> |<span data-ttu-id="d800d-230">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-230">X: DateTime</span></span> |<span data-ttu-id="d800d-231">取得參數 X 之月元件代表的月底。</span><span class="sxs-lookup"><span data-stu-id="d800d-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="d800d-232">範例：`EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (代表 9 月份月底的日期時間)</span><span class="sxs-lookup"><span data-stu-id="d800d-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="d800d-233">日期</span><span class="sxs-lookup"><span data-stu-id="d800d-233">Date</span></span> |<span data-ttu-id="d800d-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-234">StartOfDay(X)</span></span> |<span data-ttu-id="d800d-235">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-235">X: DateTime</span></span> |<span data-ttu-id="d800d-236">取得參數 X 之日元件代表的日期開始。</span><span class="sxs-lookup"><span data-stu-id="d800d-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="d800d-237">範例：`StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="d800d-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="d800d-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="d800d-238">DateTime</span></span> |<span data-ttu-id="d800d-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-239">From(X)</span></span> |<span data-ttu-id="d800d-240">X：字串</span><span class="sxs-lookup"><span data-stu-id="d800d-240">X: String</span></span> |<span data-ttu-id="d800d-241">將字串 X 剖析為日期時間。</span><span class="sxs-lookup"><span data-stu-id="d800d-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="d800d-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="d800d-242">DateTime</span></span> |<span data-ttu-id="d800d-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-243">Ticks(X)</span></span> |<span data-ttu-id="d800d-244">X：DateTime </span><span class="sxs-lookup"><span data-stu-id="d800d-244">X: DateTime</span></span> |<span data-ttu-id="d800d-245">取得參數 X 的刻度屬性。一個刻度等於 100 奈秒。</span><span class="sxs-lookup"><span data-stu-id="d800d-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="d800d-246">這個屬性的值代表從 0001 年 1 月 1 日午夜 12:00:00 經過的刻度數。</span><span class="sxs-lookup"><span data-stu-id="d800d-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="d800d-247">文字</span><span class="sxs-lookup"><span data-stu-id="d800d-247">Text</span></span> |<span data-ttu-id="d800d-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="d800d-248">Format(X)</span></span> |<span data-ttu-id="d800d-249">X：字串變數</span><span class="sxs-lookup"><span data-stu-id="d800d-249">X: String variable</span></span> |<span data-ttu-id="d800d-250">將文字格式化 (使用 `\\'` 組合來逸出 `'` 字元)。</span><span class="sxs-lookup"><span data-stu-id="d800d-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="d800d-251">在另一個函式中使用函式時，您不需要針對內部函式使用 **$$** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="d800d-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="d800d-252">例如：$$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="d800d-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="d800d-253">在此範例中，請注意 **$$** 前置詞不能用於 **Time.AddHours** 函式。</span><span class="sxs-lookup"><span data-stu-id="d800d-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="d800d-254">範例</span><span class="sxs-lookup"><span data-stu-id="d800d-254">Example</span></span>
<span data-ttu-id="d800d-255">在下列範例中，Hive 活動的輸入和輸出參數是經由使用 `Text.Format` 函式和 SliceStart 系統變數決定。</span><span class="sxs-lookup"><span data-stu-id="d800d-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="d800d-256">範例 2</span><span class="sxs-lookup"><span data-stu-id="d800d-256">Example 2</span></span>

<span data-ttu-id="d800d-257">在下列範例中，預存程序活動的日期時間參數是經由使用 Text.Format 函式</span><span class="sxs-lookup"><span data-stu-id="d800d-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="d800d-258">和 SliceStart 變數決定。</span><span class="sxs-lookup"><span data-stu-id="d800d-258">Format function and the SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="d800d-259">範例 3</span><span class="sxs-lookup"><span data-stu-id="d800d-259">Example 3</span></span>
<span data-ttu-id="d800d-260">若要讀取前一天的資料，而不是由 SliceStart 呈現的資料，請使用 AddDays 函式，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d800d-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

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

<span data-ttu-id="d800d-261">請參閱說明可使用的各種格式化選項 (例如：yy 與 yyyy) 的 [自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx) 主題。</span><span class="sxs-lookup"><span data-stu-id="d800d-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

