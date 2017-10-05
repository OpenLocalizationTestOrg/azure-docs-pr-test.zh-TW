---
title: "Log Analytics 中的自訂欄位 | Microsoft Docs"
description: "Log Analytics 的自訂欄位功能，可讓您從新增到所收集記錄之屬性的 OMS 資料建立自己的可搜尋欄位。  本文說明用來建立自訂欄位的程序，並透過範例事件提供詳細的逐步解說。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 9e02094f155eaade9bc5fb49c4fbb798e546e989
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="custom-fields-in-log-analytics"></a><span data-ttu-id="6a715-104">Log Analytics 中的自訂欄位</span><span class="sxs-lookup"><span data-stu-id="6a715-104">Custom fields in Log Analytics</span></span>
<span data-ttu-id="6a715-105">Log Analytics 的 **自訂欄位** 功能可讓您透過新增自己的可搜尋欄位來擴充 OMS 儲存機制中的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-105">The **Custom Fields** feature of Log Analytics allows you to extend existing records in the OMS repository by adding your own searchable fields.</span></span>  <span data-ttu-id="6a715-106">自訂欄位會自動填入擷取自同一筆記錄中其他屬性的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-106">Custom fields are automatically populated from data extracted from other properties in the same record.</span></span>

![自訂欄位概觀](media/log-analytics-custom-fields/overview.png)

<span data-ttu-id="6a715-108">例如，以下範例記錄在事件描述中埋藏了有用的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-108">For example, the sample record below has useful data buried in the event description.</span></span>  <span data-ttu-id="6a715-109">擷取這項資料並將其分成不同屬性，將可讓您對資料進行排序和篩選等動作。</span><span class="sxs-lookup"><span data-stu-id="6a715-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span></span>

![記錄檔搜尋按鈕](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> <span data-ttu-id="6a715-111">在預覽版中，工作區限制只能有 100 個自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-111">In the Preview, you are limited to 100 custom fields in your workspace.</span></span>  <span data-ttu-id="6a715-112">這項功能正式上市時，此限制數量將會擴大。</span><span class="sxs-lookup"><span data-stu-id="6a715-112">This limit will be expanded when this feature reaches general availability.</span></span>
> 
> 

## <a name="creating-a-custom-field"></a><span data-ttu-id="6a715-113">建立自訂欄位</span><span class="sxs-lookup"><span data-stu-id="6a715-113">Creating a custom field</span></span>
<span data-ttu-id="6a715-114">當您在建立自訂欄位時，Log Analytics 必須了解要用來填入其值的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-114">When you create a custom field, Log Analytics must understand which data to use to populate its value.</span></span>  <span data-ttu-id="6a715-115">它會使用來自 Microsoft Research 稱為 FlashExtract 的技術快速識別此資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-115">It uses a technology from Microsoft Research called FlashExtract to quickly identify this data.</span></span>  <span data-ttu-id="6a715-116">Log Analytics 不會要求您提供明確的指示，而是會了解您想要從提供的範例中擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-116">Rather than requiring you to provide explicit instructions, Log Analytics learns about the data you want to extract from examples that you provide.</span></span>

<span data-ttu-id="6a715-117">下列各節提供用於建立自訂欄位的程序。</span><span class="sxs-lookup"><span data-stu-id="6a715-117">The following sections provide the procedure for creating a custom field.</span></span>  <span data-ttu-id="6a715-118">本文最後會逐步解說範例擷取作業。</span><span class="sxs-lookup"><span data-stu-id="6a715-118">At the bottom of this article is a walkthrough of a sample extraction.</span></span>

> [!NOTE]
> <span data-ttu-id="6a715-119">當 OMS 資料存放區新增符合指定準則的記錄時便會填入自訂欄位，因此自訂欄位只會出現在建立自訂欄位之後所收集的記錄上。</span><span class="sxs-lookup"><span data-stu-id="6a715-119">The custom field is populated as records matching the specified criteria are added to the OMS data store, so it will only appear on records collected after the custom field is created.</span></span>  <span data-ttu-id="6a715-120">建立自訂欄位時便已存在於資料存放區的記錄不會新增自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-120">The custom field will not be added to records that are already in the data store when it’s created.</span></span>
> 
> 

### <a name="step-1--identify-records-that-will-have-the-custom-field"></a><span data-ttu-id="6a715-121">步驟 1 – 識別將會具有自訂欄位的記錄</span><span class="sxs-lookup"><span data-stu-id="6a715-121">Step 1 – Identify records that will have the custom field</span></span>
<span data-ttu-id="6a715-122">第一個步驟是識別會取得自訂欄位的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-122">The first step is to identify the records that will get the custom field.</span></span>  <span data-ttu-id="6a715-123">一開始您可以先進行 [標準的記錄檔搜尋](log-analytics-log-searches.md) ，然後再選取要做為 Log Analytics 將從中了解之模型的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record to act as the model that Log Analytics will learn from.</span></span>  <span data-ttu-id="6a715-124">當您指定您要將資料擷取到自訂欄位時，便會開啟 [欄位擷取精靈]  供您驗證及精簡準則。</span><span class="sxs-lookup"><span data-stu-id="6a715-124">When you specify that you are going to extract data into a custom field, the **Field Extraction Wizard** is opened where you validate and refine the criteria.</span></span>

1. <span data-ttu-id="6a715-125">移至 [記錄檔搜尋]  ，然後使用 [查詢來擷取將會具有自訂欄位的記錄](log-analytics-log-searches.md) 。</span><span class="sxs-lookup"><span data-stu-id="6a715-125">Go to **Log Search** and use a [query to retrieve the records](log-analytics-log-searches.md) that will have the custom field.</span></span>
2. <span data-ttu-id="6a715-126">選取 Log Analytics 將用來做為模型以擷取資料來填入自訂欄位的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-126">Select a record that Log Analytics will use to act as a model for extracting data to populate the custom field.</span></span>  <span data-ttu-id="6a715-127">您會識別您想要從這筆記錄擷取的資料，Log Analytics 會使用這項資訊來判斷要為所有類似記錄填入自訂欄位的邏輯。</span><span class="sxs-lookup"><span data-stu-id="6a715-127">You will identify the data that you want to extract from this record, and Log Analytics will use this information to determine the logic to populate the custom field for all similar records.</span></span>
3. <span data-ttu-id="6a715-128">按一下記錄的任何文字屬性左邊的按鈕，然後選取 [擷取欄位來源] 。</span><span class="sxs-lookup"><span data-stu-id="6a715-128">Click the button to the left of any text property of the record and select **Extract fields from**.</span></span>
4. <span data-ttu-id="6a715-129">[欄位擷取精靈] 會隨即開啟，而您選取的記錄會顯示在 [主要範例] 資料行。</span><span class="sxs-lookup"><span data-stu-id="6a715-129">The **Field Extraction Wizard is opened**, and the record you selected is displayed in the **Main Example** column.</span></span>  <span data-ttu-id="6a715-130">這些記錄的自訂欄位將會以所選屬性中的相同值來定義。</span><span class="sxs-lookup"><span data-stu-id="6a715-130">The custom field will be defined for those records with the same values in the properties that are selected.</span></span>  
5. <span data-ttu-id="6a715-131">如果已選取的項目未完全符合您想要選取的項目，請選取其他欄位以縮小準則範圍。</span><span class="sxs-lookup"><span data-stu-id="6a715-131">If the selection is not exactly what you want, select additional fields to narrow the criteria.</span></span>  <span data-ttu-id="6a715-132">若要變更準則的欄位值，您必須先取消，再選取符合您所需準則的不同記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-132">In order to change the field values for the criteria, you must cancel and select a different record matching the criteria you want.</span></span>

### <a name="step-2---perform-initial-extract"></a><span data-ttu-id="6a715-133">步驟 2 - 執行初始擷取。</span><span class="sxs-lookup"><span data-stu-id="6a715-133">Step 2 - Perform initial extract.</span></span>
<span data-ttu-id="6a715-134">一旦您識別出將會具有自訂欄位的記錄，您就已識別您想要擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-134">Once you’ve identified the records that will have the custom field, you identify the data that you want to extract.</span></span>  <span data-ttu-id="6a715-135">Log Analytics 會使用這項資訊來識別類似記錄中的類似模式。</span><span class="sxs-lookup"><span data-stu-id="6a715-135">Log Analytics will use this information to identify similar patterns in similar records.</span></span>  <span data-ttu-id="6a715-136">在這之後的步驟中，您將可以驗證結果，並提供更進一步的詳細資料以供 Log Analytics 用於其分析中。</span><span class="sxs-lookup"><span data-stu-id="6a715-136">In the step after this you will be able to validate the results and provide further details for Log Analytics to use in its analysis.</span></span>

1. <span data-ttu-id="6a715-137">在範例記錄中醒目提示您想要填入自訂欄位的文字。</span><span class="sxs-lookup"><span data-stu-id="6a715-137">Highlight the text in the sample record that you want to populate the custom field.</span></span>  <span data-ttu-id="6a715-138">然後您會看到一個對話方塊，供您提供欄位名稱和執行初始擷取。</span><span class="sxs-lookup"><span data-stu-id="6a715-138">You will then be presented with a dialog box to provide a name for the field and to perform the initial extract.</span></span>  <span data-ttu-id="6a715-139">字元 **\__CF** 會自動附加上去。</span><span class="sxs-lookup"><span data-stu-id="6a715-139">The characters **\_CF** will automatically be appended.</span></span>
2. <span data-ttu-id="6a715-140">按一下 [擷取]  以對收集的記錄進行分析。</span><span class="sxs-lookup"><span data-stu-id="6a715-140">Click **Extract** to perform an analysis of collected records.</span></span>  
3. <span data-ttu-id="6a715-141">[摘要] 和 [搜尋結果] 區段會顯示擷取結果，以供您檢查其正確性。</span><span class="sxs-lookup"><span data-stu-id="6a715-141">The **Summary** and **Search Results** sections display the results of the extract so you can inspect its accuracy.</span></span>  <span data-ttu-id="6a715-142"> 會顯示用來識別記錄的準則，以及每個所識別之資料值的計數。</span><span class="sxs-lookup"><span data-stu-id="6a715-142">**Summary** displays the criteria used to identify records and a count for each of the data values identified.</span></span>  <span data-ttu-id="6a715-143"> 會提供符合準則之記錄的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="6a715-143">**Search Results** provides a detailed list of records matching the criteria.</span></span>

### <a name="step-3--verify-accuracy-of-the-extract-and-create-custom-field"></a><span data-ttu-id="6a715-144">步驟 3 – 驗證擷取的正確性並建立自訂欄位</span><span class="sxs-lookup"><span data-stu-id="6a715-144">Step 3 – Verify accuracy of the extract and create custom field</span></span>
<span data-ttu-id="6a715-145">一旦您執行過初始擷取，Log Analytics 就會根據收集到的資料顯示其結果。</span><span class="sxs-lookup"><span data-stu-id="6a715-145">Once you have performed the initial extract, Log Analytics will display its results based on data that has already been collected.</span></span>  <span data-ttu-id="6a715-146">如果結果看起來是正確的，您就可以建立自訂欄位，無須再進行其他工作。</span><span class="sxs-lookup"><span data-stu-id="6a715-146">If the results look accurate then you can create the custom field with no further work.</span></span>  <span data-ttu-id="6a715-147">如果不正確，則可以精簡結果以便讓 Log Analytics 提升其邏輯。</span><span class="sxs-lookup"><span data-stu-id="6a715-147">If not, then you can refine the results so that Log Analytics can improve its logic.</span></span>

1. <span data-ttu-id="6a715-148">如果初始擷取中有任何值不正確，則請按一下錯誤記錄旁的 [編輯] 圖示，然後選取 [修改此醒目提示] 以修改選取項目。</span><span class="sxs-lookup"><span data-stu-id="6a715-148">If any values in the initial extract aren’t correct, then click the **Edit** icon next to an inaccurate record and select **Modify this highlight** in order to modify the selection.</span></span>
2. <span data-ttu-id="6a715-149">項目會複製到 [主要範例] 底下的 [其他範例] 區段。</span><span class="sxs-lookup"><span data-stu-id="6a715-149">The entry is copied to the **Additional examples** section underneath the **Main Example**.</span></span>  <span data-ttu-id="6a715-150">您可以在此調整醒目提示來協助 Log Analytics 了解其應該選取的項目。</span><span class="sxs-lookup"><span data-stu-id="6a715-150">You can adjust the highlight here to help Log Analytics understand the selection it should have made.</span></span>
3. <span data-ttu-id="6a715-151">按一下 [擷取]  ，使用這項新資訊來評估所有現有記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-151">Click **Extract** to use this new information to evaluate all the existing records.</span></span>  <span data-ttu-id="6a715-152">根據這個新情報，記錄的結果可能會有所修改，而不同於您剛才修改的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-152">The results may be modified for records other than the one you just modified based on this new intelligence.</span></span>
4. <span data-ttu-id="6a715-153">繼續加入修正，直到擷取中的所有記錄正確識別要填入新自訂欄位的資料。</span><span class="sxs-lookup"><span data-stu-id="6a715-153">Continue to add corrections until all records in the extract correctly identify the data to populate the new custom field.</span></span>
5. <span data-ttu-id="6a715-154">當您滿意結果時，按一下 [儲存擷取]  。</span><span class="sxs-lookup"><span data-stu-id="6a715-154">Click **Save Extract** when you are satisfied with the results.</span></span>  <span data-ttu-id="6a715-155">自訂欄位現已定義完成，但還不會新增到任何記錄中。</span><span class="sxs-lookup"><span data-stu-id="6a715-155">The custom field is now defined, but it won’t be added to any records yet.</span></span>
6. <span data-ttu-id="6a715-156">請等候符合指定準則的新記錄收集完成，然後再次執行記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="6a715-156">Wait for new records matching the specified criteria to be collected and then run the log search again.</span></span> <span data-ttu-id="6a715-157">新的記錄應該會有自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-157">New records should have the custom field.</span></span>
7. <span data-ttu-id="6a715-158">和任何其他記錄屬性一樣地使用自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-158">Use the custom field like any other record property.</span></span>  <span data-ttu-id="6a715-159">您可以使用它來彙總與群組資料，甚至用它來產生新的見解。</span><span class="sxs-lookup"><span data-stu-id="6a715-159">You can use it to aggregate and group data and even use it to produce new insights.</span></span>

## <a name="viewing-custom-fields"></a><span data-ttu-id="6a715-160">檢視自訂欄位</span><span class="sxs-lookup"><span data-stu-id="6a715-160">Viewing custom fields</span></span>
<span data-ttu-id="6a715-161">您可以從 OMS 儀表板的 [設定]  圖格，檢視您的管理群組中所有自訂欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="6a715-161">You can view a list of all custom fields in your management group from the **Settings** tile of the OMS dashboard.</span></span>  <span data-ttu-id="6a715-162">依序選取 [資料] 和 [自訂欄位]，可取得工作區中所有自訂欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="6a715-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span></span>  

![自訂欄位](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a><span data-ttu-id="6a715-164">移除自訂欄位</span><span class="sxs-lookup"><span data-stu-id="6a715-164">Removing a custom field</span></span>
<span data-ttu-id="6a715-165">有兩種方式可移除自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-165">There are two ways to remove a custom field.</span></span>  <span data-ttu-id="6a715-166">第一個方式是在檢視如上所述的完整清單時，每個欄位所具有的 [移除]  選項。</span><span class="sxs-lookup"><span data-stu-id="6a715-166">The first is the **Remove** option for each field when viewing the complete list as described above.</span></span>  <span data-ttu-id="6a715-167">另一個方式是擷取一筆記錄，然後按一下欄位左邊的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a715-167">The other method is to retrieve a record and click the button to the left of the field.</span></span>  <span data-ttu-id="6a715-168">功能表中會有可供移除自訂欄位的選項。</span><span class="sxs-lookup"><span data-stu-id="6a715-168">The menu will have an option to remove the custom field.</span></span>

## <a name="sample-walkthrough"></a><span data-ttu-id="6a715-169">範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="6a715-169">Sample walkthrough</span></span>
<span data-ttu-id="6a715-170">下面的章節會逐步解說建立自訂欄位的完整範例。</span><span class="sxs-lookup"><span data-stu-id="6a715-170">The following section walks through a complete example of creating a custom field.</span></span>  <span data-ttu-id="6a715-171">這個範例會擷取 Windows 事件中指出變更狀態之服務的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6a715-171">This example extracts the service name in Windows events that indicate a service changing state.</span></span>  <span data-ttu-id="6a715-172">這個動作必須仰賴服務控制管理員在 Windows 電腦的系統記錄檔中建立的事件。</span><span class="sxs-lookup"><span data-stu-id="6a715-172">This relies on events created by Service Control Manager in the System log on Windows computers.</span></span>  <span data-ttu-id="6a715-173">如果您想要跟隨此範例，您必須 [收集系統記錄檔的資訊事件](log-analytics-data-sources-windows-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6a715-173">If you want to follow this example, you must be [collecting Information events for the System log](log-analytics-data-sources-windows-events.md).</span></span>

<span data-ttu-id="6a715-174">我們輸入下列查詢，以從服務控制管理員傳回事件識別碼為 7036，且為指出服務正在啟動或停止之事件的所有事件。</span><span class="sxs-lookup"><span data-stu-id="6a715-174">We enter the following query to return all events from Service Control Manager that have an Event ID of 7036 which is the event that indicates a service starting or stopping.</span></span>

![查詢](media/log-analytics-custom-fields/query.png)

<span data-ttu-id="6a715-176">然後，我們選取任何事件識別碼為 7036 的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-176">We then select any record with event ID 7036.</span></span>

![來源記錄](media/log-analytics-custom-fields/source-record.png)

<span data-ttu-id="6a715-178">我們想要讓該服務名稱出現在 [RenderedDescription]  屬性，並選取這個屬性旁的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a715-178">We want the service name that appears in the **RenderedDescription** property and select the button next to this property.</span></span>

![擷取欄位](media/log-analytics-custom-fields/extract-fields.png)

<span data-ttu-id="6a715-180">[欄位擷取精靈] 會隨即開啟，而且 [主要範例] 資料行中已選取 [EventLog] 和 [EventID] 欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-180">The **Field Extraction Wizard** is opened, and the **EventLog** and **EventID** fields are selected in the **Main Example** column.</span></span>  <span data-ttu-id="6a715-181">這表示將會為系統記錄檔中事件識別碼為 7036 的事件定義自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-181">This indicates that the custom field will be defined for events from the System log with an event ID of 7036.</span></span>  <span data-ttu-id="6a715-182">這樣就可以了，所以我們不需要再選取其他欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-182">This is sufficient so we don’t need to select any other fields.</span></span>

![主要範例](media/log-analytics-custom-fields/main-example.png)

<span data-ttu-id="6a715-184">我們醒目提示 [RenderedDescription] 屬性中的服務名稱，然後使用 [Service] 來識別服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6a715-184">We highlight the name of the service in the **RenderedDescription** property and use **Service** to identify the service name.</span></span>  <span data-ttu-id="6a715-185">自訂欄位將會稱為 **Service_CF**。</span><span class="sxs-lookup"><span data-stu-id="6a715-185">The custom field will be called **Service_CF**.</span></span>

![欄位標題](media/log-analytics-custom-fields/field-title.png)

<span data-ttu-id="6a715-187">我們看到某些記錄已正確識別服務名稱，但某些記錄則未如此。</span><span class="sxs-lookup"><span data-stu-id="6a715-187">We see that the service name is identified properly for some records but not for others.</span></span>   <span data-ttu-id="6a715-188">[搜尋結果] 顯示 **WMI Performance Adapter** 有部分名稱未能選取到。</span><span class="sxs-lookup"><span data-stu-id="6a715-188">The **Search Results** show that part of the name for the **WMI Performance Adapter** wasn’t selected.</span></span>  <span data-ttu-id="6a715-189">[摘要] 顯示四筆具有 **DPRMA** 服務的記錄錯誤地包含了額外的文字，而有兩筆記錄識別了 **Modules Installer** 而不是 **Windows Modules Installer**。</span><span class="sxs-lookup"><span data-stu-id="6a715-189">The **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span></span>  

![搜尋結果](media/log-analytics-custom-fields/search-results-01.png)

<span data-ttu-id="6a715-191">我們先處理 **WMI Performance Adapter** 記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-191">We start with the **WMI Performance Adapter** record.</span></span>  <span data-ttu-id="6a715-192">我們按一下它的編輯圖示，然後 [修改此醒目提示] 。</span><span class="sxs-lookup"><span data-stu-id="6a715-192">We click its edit icon and then **Modify this highlight**.</span></span>  

![修改醒目提示](media/log-analytics-custom-fields/modify-highlight.png)

<span data-ttu-id="6a715-194">我們增加醒目提示範圍來包含 **WMI** 一字，然後重新執行擷取。</span><span class="sxs-lookup"><span data-stu-id="6a715-194">We increase    the highlight to include the word **WMI** and then rerun the extract.</span></span>  

![其他範例](media/log-analytics-custom-fields/additional-example-01.png)

<span data-ttu-id="6a715-196">我們可以看到 **WMI Performance Adapter** 的項目已修正，而且 Log Analytics 也已使用該資訊來更正 **Windows Module Installer** 的記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-196">We can see that the entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information to correct the records for **Windows Module Installer**.</span></span>  <span data-ttu-id="6a715-197">但我們可以看到 [摘要] 區段中 **DPMRA** 仍未被正確識別。</span><span class="sxs-lookup"><span data-stu-id="6a715-197">We can see in the **Summary** section though that **DPMRA** is still not being identified correctly.</span></span>

![搜尋結果](media/log-analytics-custom-fields/search-results-02.png)

<span data-ttu-id="6a715-199">我們捲動到具有 DPMRA 服務的記錄，並使用相同的程序來更正該記錄。</span><span class="sxs-lookup"><span data-stu-id="6a715-199">We scroll to a record with the DPMRA service and use the same process to correct that record.</span></span>

![其他範例](media/log-analytics-custom-fields/additional-example-02.png)

 <span data-ttu-id="6a715-201">當我們執行擷取時，我們可以看到所有結果現在都已正確。</span><span class="sxs-lookup"><span data-stu-id="6a715-201">When we run the extraction, we can see that all of our results are now accurate.</span></span>

![搜尋結果](media/log-analytics-custom-fields/search-results-03.png)

<span data-ttu-id="6a715-203">我們可以看到 **Service_CF** 已建立但尚未新增到任何記錄中。</span><span class="sxs-lookup"><span data-stu-id="6a715-203">We can see that **Service_CF** is created but is not yet added to any records.</span></span>

![初始計數](media/log-analytics-custom-fields/initial-count.png)

<span data-ttu-id="6a715-205">過了一會兒之後，新事件已收集完成，我們可以看到 [Service_CF] 欄位現在會新增到符合準則的記錄中。</span><span class="sxs-lookup"><span data-stu-id="6a715-205">After some time has passed so new events are collected, we can see that that the **Service_CF** field is now being added to records that match our criteria.</span></span>

![最終結果](media/log-analytics-custom-fields/final-results.png)

<span data-ttu-id="6a715-207">現在我們可以和任何其他記錄屬性一樣地使用自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="6a715-207">We can now use the custom field like any other record property.</span></span>  <span data-ttu-id="6a715-208">為了說明這一點，我們建立以新的 [Service_CF] 欄位來群組的查詢，以檢查哪些服務最常使用。</span><span class="sxs-lookup"><span data-stu-id="6a715-208">To illustrate this, we create a query that groups by the new **Service_CF** field to inspect which services are the most active.</span></span>

![以查詢分組](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a><span data-ttu-id="6a715-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a715-210">Next steps</span></span>
* <span data-ttu-id="6a715-211">了解 [記錄搜尋](log-analytics-log-searches.md) ，以使用自訂欄位作為準則來建立查詢。</span><span class="sxs-lookup"><span data-stu-id="6a715-211">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
* <span data-ttu-id="6a715-212">監視可利用自訂欄位來剖析的[自訂記錄檔](log-analytics-data-sources-custom-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="6a715-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span></span>

