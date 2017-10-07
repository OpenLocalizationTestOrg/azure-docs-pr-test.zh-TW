---
title: "記錄分析 aaaCustom 欄位 |Microsoft 文件"
description: "記錄分析 hello 自訂欄位功能可讓您 toocreate 您自己從 OMS 資料會加入 toohello 屬性收集記錄的可搜尋的欄位。  本文描述 hello 程序 toocreate 自訂欄位，並提供範例事件的詳細逐步解說。"
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
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a><span data-ttu-id="ba727-104">Log Analytics 中的自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-104">Custom fields in Log Analytics</span></span>
<span data-ttu-id="ba727-105">hello**自訂欄位**功能記錄分析可讓您 tooextend hello OMS 儲存機制中的現有記錄中加入您自己可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-105">hello **Custom Fields** feature of Log Analytics allows you tooextend existing records in hello OMS repository by adding your own searchable fields.</span></span>  <span data-ttu-id="ba727-106">自訂欄位會自動填入擷取自 hello 中其他屬性的資料相同的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-106">Custom fields are automatically populated from data extracted from other properties in hello same record.</span></span>

![自訂欄位概觀](media/log-analytics-custom-fields/overview.png)

<span data-ttu-id="ba727-108">例如，下列的 hello 範例筆都有有用的資料埋藏在 hello 事件描述。</span><span class="sxs-lookup"><span data-stu-id="ba727-108">For example, hello sample record below has useful data buried in hello event description.</span></span>  <span data-ttu-id="ba727-109">擷取這項資料並將其分成不同屬性，將可讓您對資料進行排序和篩選等動作。</span><span class="sxs-lookup"><span data-stu-id="ba727-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span></span>

![記錄檔搜尋按鈕](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> <span data-ttu-id="ba727-111">在 hello 預覽，您可以是有限的 too100 工作區中的自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-111">In hello Preview, you are limited too100 custom fields in your workspace.</span></span>  <span data-ttu-id="ba727-112">這項功能正式上市時，此限制數量將會擴大。</span><span class="sxs-lookup"><span data-stu-id="ba727-112">This limit will be expanded when this feature reaches general availability.</span></span>
> 
> 

## <a name="creating-a-custom-field"></a><span data-ttu-id="ba727-113">建立自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-113">Creating a custom field</span></span>
<span data-ttu-id="ba727-114">當您建立自訂欄位時，記錄分析必須了解哪些資料 toouse toopopulate 其值。</span><span class="sxs-lookup"><span data-stu-id="ba727-114">When you create a custom field, Log Analytics must understand which data toouse toopopulate its value.</span></span>  <span data-ttu-id="ba727-115">它會使用一種技術來自 Microsoft 研究項被稱為 FlashExtract tooquickly 識別此資料。</span><span class="sxs-lookup"><span data-stu-id="ba727-115">It uses a technology from Microsoft Research called FlashExtract tooquickly identify this data.</span></span>  <span data-ttu-id="ba727-116">不需要您 tooprovide 明確指示，記錄分析學習 hello 資料，您會想 tooextract 從您提供的範例。</span><span class="sxs-lookup"><span data-stu-id="ba727-116">Rather than requiring you tooprovide explicit instructions, Log Analytics learns about hello data you want tooextract from examples that you provide.</span></span>

<span data-ttu-id="ba727-117">hello 下列各節提供 hello 程序建立自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-117">hello following sections provide hello procedure for creating a custom field.</span></span>  <span data-ttu-id="ba727-118">這篇文章底部 hello 是範例擷取的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="ba727-118">At hello bottom of this article is a walkthrough of a sample extraction.</span></span>

> [!NOTE]
> <span data-ttu-id="ba727-119">hello 自訂欄位會擴展為 hello 符合指定準則會新增 toohello OMS 資料存放區，使它只會出現在記錄收集 hello 自訂欄位建立之後的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-119">hello custom field is populated as records matching hello specified criteria are added toohello OMS data store, so it will only appear on records collected after hello custom field is created.</span></span>  <span data-ttu-id="ba727-120">hello 自訂欄位將不會加入 toorecords 時就已 hello 資料存放區中建立。</span><span class="sxs-lookup"><span data-stu-id="ba727-120">hello custom field will not be added toorecords that are already in hello data store when it’s created.</span></span>
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a><span data-ttu-id="ba727-121">步驟 1 – 識別記錄將會擁有 hello 自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-121">Step 1 – Identify records that will have hello custom field</span></span>
<span data-ttu-id="ba727-122">hello 第一個步驟為 tooidentify hello 記錄會得到 hello 自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-122">hello first step is tooidentify hello records that will get hello custom field.</span></span>  <span data-ttu-id="ba727-123">您開始使用[標準的記錄搜尋](log-analytics-log-searches.md)，然後選取記錄 tooact 為記錄分析將從中學習的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="ba727-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record tooact as hello model that Log Analytics will learn from.</span></span>  <span data-ttu-id="ba727-124">當您指定將 tooextract 資料至自訂欄位時，hello**欄位擷取精靈** 會開啟您驗證並精簡 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="ba727-124">When you specify that you are going tooextract data into a custom field, hello **Field Extraction Wizard** is opened where you validate and refine hello criteria.</span></span>

1. <span data-ttu-id="ba727-125">跳過**記錄搜尋**並用[查詢 tooretrieve hello 記錄](log-analytics-log-searches.md)，將會擁有 hello 自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-125">Go too**Log Search** and use a [query tooretrieve hello records](log-analytics-log-searches.md) that will have hello custom field.</span></span>
2. <span data-ttu-id="ba727-126">選取記錄分析將使用做為模型 tooact 解壓縮資料 toopopulate hello 自訂欄位的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-126">Select a record that Log Analytics will use tooact as a model for extracting data toopopulate hello custom field.</span></span>  <span data-ttu-id="ba727-127">您會識別 hello 資料，您想要從這筆記錄，tooextract 記錄分析將使用此資訊 toodetermine hello 邏輯 toopopulate hello 自訂欄位的所有類似的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-127">You will identify hello data that you want tooextract from this record, and Log Analytics will use this information toodetermine hello logic toopopulate hello custom field for all similar records.</span></span>
3. <span data-ttu-id="ba727-128">按一下 [hello] 按鈕 toohello hello 記錄和選取任何文字屬性左邊**從擷取欄位**。</span><span class="sxs-lookup"><span data-stu-id="ba727-128">Click hello button toohello left of any text property of hello record and select **Extract fields from**.</span></span>
4. <span data-ttu-id="ba727-129">hello**欄位擷取精靈] 會開啟**，而且您所選取的 hello 記錄會顯示在 [hello**主要範例**資料行。</span><span class="sxs-lookup"><span data-stu-id="ba727-129">hello **Field Extraction Wizard is opened**, and hello record you selected is displayed in hello **Main Example** column.</span></span>  <span data-ttu-id="ba727-130">hello 自訂欄位將會定義以針對選取的 hello 屬性中的相同值的 hello 這些記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-130">hello custom field will be defined for those records with hello same values in hello properties that are selected.</span></span>  
5. <span data-ttu-id="ba727-131">如果您想要 hello 選取項目時不完全，選取其他欄位 toonarrow hello 條件。</span><span class="sxs-lookup"><span data-stu-id="ba727-131">If hello selection is not exactly what you want, select additional fields toonarrow hello criteria.</span></span>  <span data-ttu-id="ba727-132">順序 toochange 會 hello hello 準則的欄位值，您必須取消，並選取不同的記錄符合您想要的 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="ba727-132">In order toochange hello field values for hello criteria, you must cancel and select a different record matching hello criteria you want.</span></span>

### <a name="step-2---perform-initial-extract"></a><span data-ttu-id="ba727-133">步驟 2 - 執行初始擷取。</span><span class="sxs-lookup"><span data-stu-id="ba727-133">Step 2 - Perform initial extract.</span></span>
<span data-ttu-id="ba727-134">一旦您已經識別 hello 記錄將會擁有 hello 自訂欄位，您會識別您想要 tooextract 的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ba727-134">Once you’ve identified hello records that will have hello custom field, you identify hello data that you want tooextract.</span></span>  <span data-ttu-id="ba727-135">記錄分析將使用此資訊 tooidentify 類似的模式中類似的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-135">Log Analytics will use this information tooidentify similar patterns in similar records.</span></span>  <span data-ttu-id="ba727-136">在此之後的 hello 步驟將會無法 toovalidate hello 的結果，並提供其分析中的記錄分析 toouse 的進一步詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba727-136">In hello step after this you will be able toovalidate hello results and provide further details for Log Analytics toouse in its analysis.</span></span>

1. <span data-ttu-id="ba727-137">反白顯示您想 toopopulate hello 自訂欄位的 hello 範例記錄中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="ba727-137">Highlight hello text in hello sample record that you want toopopulate hello custom field.</span></span>  <span data-ttu-id="ba727-138">您接著會有對話方塊方塊 tooprovide hello 欄位和 tooperform hello 初始擷取的名稱。</span><span class="sxs-lookup"><span data-stu-id="ba727-138">You will then be presented with a dialog box tooprovide a name for hello field and tooperform hello initial extract.</span></span>  <span data-ttu-id="ba727-139">hello 字元 **\_CF**會自動附加。</span><span class="sxs-lookup"><span data-stu-id="ba727-139">hello characters **\_CF** will automatically be appended.</span></span>
2. <span data-ttu-id="ba727-140">按一下**擷取**tooperform 收集記錄的分析。</span><span class="sxs-lookup"><span data-stu-id="ba727-140">Click **Extract** tooperform an analysis of collected records.</span></span>  
3. <span data-ttu-id="ba727-141">hello**摘要**和**搜尋結果**區段會顯示 hello hello 擷取結果，讓您檢查其正確性。</span><span class="sxs-lookup"><span data-stu-id="ba727-141">hello **Summary** and **Search Results** sections display hello results of hello extract so you can inspect its accuracy.</span></span>  <span data-ttu-id="ba727-142">**摘要**顯示 hello 用準則 tooidentify 記錄及計數針對每個已識別的 hello 資料值。</span><span class="sxs-lookup"><span data-stu-id="ba727-142">**Summary** displays hello criteria used tooidentify records and a count for each of hello data values identified.</span></span>  <span data-ttu-id="ba727-143">**搜尋結果**提供詳細的 hello 的準則相符的記錄清單。</span><span class="sxs-lookup"><span data-stu-id="ba727-143">**Search Results** provides a detailed list of records matching hello criteria.</span></span>

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a><span data-ttu-id="ba727-144">步驟 3 – 確認 hello 擷取的精確度，並建立自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-144">Step 3 – Verify accuracy of hello extract and create custom field</span></span>
<span data-ttu-id="ba727-145">一旦您已經執行 hello 初始擷取，記錄分析會顯示其結果，根據已收集的資料。</span><span class="sxs-lookup"><span data-stu-id="ba727-145">Once you have performed hello initial extract, Log Analytics will display its results based on data that has already been collected.</span></span>  <span data-ttu-id="ba727-146">如果 hello 結果看起來正確然後您就可以建立 hello 自訂欄位而無須進行進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="ba727-146">If hello results look accurate then you can create hello custom field with no further work.</span></span>  <span data-ttu-id="ba727-147">如果沒有，您可以精簡 hello 結果以便讓記錄分析改善其邏輯。</span><span class="sxs-lookup"><span data-stu-id="ba727-147">If not, then you can refine hello results so that Log Analytics can improve its logic.</span></span>

1. <span data-ttu-id="ba727-148">如果 hello 初始擷取中的任何值不正確，然後按一下 hello**編輯**圖示下一步 tooan 不正確的記錄，然後選取**修改此反白顯示**順序 toomodify hello 選取範圍中。</span><span class="sxs-lookup"><span data-stu-id="ba727-148">If any values in hello initial extract aren’t correct, then click hello **Edit** icon next tooan inaccurate record and select **Modify this highlight** in order toomodify hello selection.</span></span>
2. <span data-ttu-id="ba727-149">hello 項目會複製的 toohello**其他範例**hello 下方區段**主要範例**。</span><span class="sxs-lookup"><span data-stu-id="ba727-149">hello entry is copied toohello **Additional examples** section underneath hello **Main Example**.</span></span>  <span data-ttu-id="ba727-150">您可以調整 hello 反白顯示以下 toohelp 記錄分析了解其應該做的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="ba727-150">You can adjust hello highlight here toohelp Log Analytics understand hello selection it should have made.</span></span>
3. <span data-ttu-id="ba727-151">按一下**擷取**toouse 所有 hello 現有這個新資訊 tooevaluate 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-151">Click **Extract** toouse this new information tooevaluate all hello existing records.</span></span>  <span data-ttu-id="ba727-152">hello 結果可能會修改以外 hello 其中是您剛才修改根據這個新資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-152">hello results may be modified for records other than hello one you just modified based on this new intelligence.</span></span>
4. <span data-ttu-id="ba727-153">繼續 tooadd 更正，直到 hello 中的所有記錄都擷取正確識別 hello 資料 toopopulate hello 新自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-153">Continue tooadd corrections until all records in hello extract correctly identify hello data toopopulate hello new custom field.</span></span>
5. <span data-ttu-id="ba727-154">按一下**儲存擷取**當您滿意 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ba727-154">Click **Save Extract** when you are satisfied with hello results.</span></span>  <span data-ttu-id="ba727-155">hello 自訂欄位現在已經在定義中，但它還不會加入 tooany 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-155">hello custom field is now defined, but it won’t be added tooany records yet.</span></span>
6. <span data-ttu-id="ba727-156">等候新記錄符合 hello 指定準則 toobe 收集，然後再重新執行 hello 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="ba727-156">Wait for new records matching hello specified criteria toobe collected and then run hello log search again.</span></span> <span data-ttu-id="ba727-157">新的記錄都應該有 hello 自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-157">New records should have hello custom field.</span></span>
7. <span data-ttu-id="ba727-158">使用 hello 像任何其他記錄的內容的自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-158">Use hello custom field like any other record property.</span></span>  <span data-ttu-id="ba727-159">可用 tooaggregate 與群組資料並甚至使用 tooproduce 全新深入見解。</span><span class="sxs-lookup"><span data-stu-id="ba727-159">You can use it tooaggregate and group data and even use it tooproduce new insights.</span></span>

## <a name="viewing-custom-fields"></a><span data-ttu-id="ba727-160">檢視自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-160">Viewing custom fields</span></span>
<span data-ttu-id="ba727-161">您可以檢視 hello 從管理群組中的所有自訂欄位的清單**設定**hello OMS 儀表板的磚。</span><span class="sxs-lookup"><span data-stu-id="ba727-161">You can view a list of all custom fields in your management group from hello **Settings** tile of hello OMS dashboard.</span></span>  <span data-ttu-id="ba727-162">依序選取 [資料] 和 [自訂欄位]，可取得工作區中所有自訂欄位的清單。</span><span class="sxs-lookup"><span data-stu-id="ba727-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span></span>  

![自訂欄位](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a><span data-ttu-id="ba727-164">移除自訂欄位</span><span class="sxs-lookup"><span data-stu-id="ba727-164">Removing a custom field</span></span>
<span data-ttu-id="ba727-165">有兩種方式 tooremove 自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-165">There are two ways tooremove a custom field.</span></span>  <span data-ttu-id="ba727-166">hello 第一個是 hello**移除**檢視 hello 完整清單，如上面所述，當每個欄位的選項。</span><span class="sxs-lookup"><span data-stu-id="ba727-166">hello first is hello **Remove** option for each field when viewing hello complete list as described above.</span></span>  <span data-ttu-id="ba727-167">hello 其他方法是的 tooretrieve 記錄並按一下 hello 按鈕 toohello 方 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-167">hello other method is tooretrieve a record and click hello button toohello left of hello field.</span></span>  <span data-ttu-id="ba727-168">hello 功能表會有選項 tooremove hello 自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-168">hello menu will have an option tooremove hello custom field.</span></span>

## <a name="sample-walkthrough"></a><span data-ttu-id="ba727-169">範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="ba727-169">Sample walkthrough</span></span>
<span data-ttu-id="ba727-170">hello 下一節逐步解說建立自訂欄位的完整範例。</span><span class="sxs-lookup"><span data-stu-id="ba727-170">hello following section walks through a complete example of creating a custom field.</span></span>  <span data-ttu-id="ba727-171">這個範例會擷取在 Windows 事件指出變更狀態的服務中的 hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="ba727-171">This example extracts hello service name in Windows events that indicate a service changing state.</span></span>  <span data-ttu-id="ba727-172">這會依賴由服務控制管理員建立 hello Windows 電腦上的系統記錄檔中的事件。</span><span class="sxs-lookup"><span data-stu-id="ba727-172">This relies on events created by Service Control Manager in hello System log on Windows computers.</span></span>  <span data-ttu-id="ba727-173">如果您想 toofollow 此範例中，您必須是[收集 hello 系統記錄檔的資訊事件](log-analytics-data-sources-windows-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ba727-173">If you want toofollow this example, you must be [collecting Information events for hello System log](log-analytics-data-sources-windows-events.md).</span></span>

<span data-ttu-id="ba727-174">我們輸入下列查詢 tooreturn hello 所有事件從服務控制管理員事件識別碼為 7036 的 hello 事件，指出啟動或停止服務。</span><span class="sxs-lookup"><span data-stu-id="ba727-174">We enter hello following query tooreturn all events from Service Control Manager that have an Event ID of 7036 which is hello event that indicates a service starting or stopping.</span></span>

![查詢](media/log-analytics-custom-fields/query.png)

<span data-ttu-id="ba727-176">然後，我們選取任何事件識別碼為 7036 的記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-176">We then select any record with event ID 7036.</span></span>

![來源記錄](media/log-analytics-custom-fields/source-record.png)

<span data-ttu-id="ba727-178">我們希望 hello 服務名稱會出現在 hello **RenderedDescription**屬性及選取 hello 按鈕的下一步 toothis 屬性。</span><span class="sxs-lookup"><span data-stu-id="ba727-178">We want hello service name that appears in hello **RenderedDescription** property and select hello button next toothis property.</span></span>

![擷取欄位](media/log-analytics-custom-fields/extract-fields.png)

<span data-ttu-id="ba727-180">hello**欄位擷取精靈**會開啟，而且 hello **EventLog**和**EventID** hello 中已選取欄位**主要範例**資料行。</span><span class="sxs-lookup"><span data-stu-id="ba727-180">hello **Field Extraction Wizard** is opened, and hello **EventLog** and **EventID** fields are selected in hello **Main Example** column.</span></span>  <span data-ttu-id="ba727-181">這表示該 hello 自訂欄位將會針對識別碼為 7036 的事件 hello 系統記錄檔事件定義。</span><span class="sxs-lookup"><span data-stu-id="ba727-181">This indicates that hello custom field will be defined for events from hello System log with an event ID of 7036.</span></span>  <span data-ttu-id="ba727-182">所以我們不需要 tooselect 任何其他欄位就足夠了。</span><span class="sxs-lookup"><span data-stu-id="ba727-182">This is sufficient so we don’t need tooselect any other fields.</span></span>

![主要範例](media/log-analytics-custom-fields/main-example.png)

<span data-ttu-id="ba727-184">我們反白顯示 hello hello 中的 hello 服務名稱**RenderedDescription**屬性並使用**服務**tooidentify hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="ba727-184">We highlight hello name of hello service in hello **RenderedDescription** property and use **Service** tooidentify hello service name.</span></span>  <span data-ttu-id="ba727-185">hello 自訂欄位將會被稱為**Service_CF**。</span><span class="sxs-lookup"><span data-stu-id="ba727-185">hello custom field will be called **Service_CF**.</span></span>

![欄位標題](media/log-analytics-custom-fields/field-title.png)

<span data-ttu-id="ba727-187">我們會看到某些記錄但不是其他正確識別該 hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="ba727-187">We see that hello service name is identified properly for some records but not for others.</span></span>   <span data-ttu-id="ba727-188">hello**搜尋結果**顯示 hello hello 名稱的該部分**WMI 效能配接器**未被選取。</span><span class="sxs-lookup"><span data-stu-id="ba727-188">hello **Search Results** show that part of hello name for hello **WMI Performance Adapter** wasn’t selected.</span></span>  <span data-ttu-id="ba727-189">hello**摘要**顯示四個記錄與**DPRMA**服務錯誤的包含了額外字組，且兩筆記錄識別**模組安裝程式**而不是**Windows 模組安裝程式**。</span><span class="sxs-lookup"><span data-stu-id="ba727-189">hello **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span></span>  

![搜尋結果](media/log-analytics-custom-fields/search-results-01.png)

<span data-ttu-id="ba727-191">我們以 hello 開頭**WMI 效能配接器**記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-191">We start with hello **WMI Performance Adapter** record.</span></span>  <span data-ttu-id="ba727-192">我們按一下它的編輯圖示，然後 [修改此醒目提示] 。</span><span class="sxs-lookup"><span data-stu-id="ba727-192">We click its edit icon and then **Modify this highlight**.</span></span>  

![修改醒目提示](media/log-analytics-custom-fields/modify-highlight.png)

<span data-ttu-id="ba727-194">我們增加 hello 反白顯示 tooinclude hello word **WMI** ，然後重新執行 hello 擷取。</span><span class="sxs-lookup"><span data-stu-id="ba727-194">We increase    hello highlight tooinclude hello word **WMI** and then rerun hello extract.</span></span>  

![其他範例](media/log-analytics-custom-fields/additional-example-01.png)

<span data-ttu-id="ba727-196">我們可以看到該 hello 項目**WMI 效能配接器**已經更正，且記錄分析也利用該資訊 toocorrect hello 記錄**Windows 模組安裝程式**。</span><span class="sxs-lookup"><span data-stu-id="ba727-196">We can see that hello entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information toocorrect hello records for **Windows Module Installer**.</span></span>  <span data-ttu-id="ba727-197">我們可以看到在 hello**摘要**雖然區段， **DPMRA**為仍然未被正確識別。</span><span class="sxs-lookup"><span data-stu-id="ba727-197">We can see in hello **Summary** section though that **DPMRA** is still not being identified correctly.</span></span>

![搜尋結果](media/log-analytics-custom-fields/search-results-02.png)

<span data-ttu-id="ba727-199">我們捲動 tooa hello DPMRA 服務的記錄，並使用相同的處理序記錄的 toocorrect hello。</span><span class="sxs-lookup"><span data-stu-id="ba727-199">We scroll tooa record with hello DPMRA service and use hello same process toocorrect that record.</span></span>

![其他範例](media/log-analytics-custom-fields/additional-example-02.png)

 <span data-ttu-id="ba727-201">當我們執行 hello 擷取時，我們可以看到，所有的結果現在都很精確。</span><span class="sxs-lookup"><span data-stu-id="ba727-201">When we run hello extraction, we can see that all of our results are now accurate.</span></span>

![搜尋結果](media/log-analytics-custom-fields/search-results-03.png)

<span data-ttu-id="ba727-203">我們可以看到**Service_CF**建立但尚未加入 tooany 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba727-203">We can see that **Service_CF** is created but is not yet added tooany records.</span></span>

![初始計數](media/log-analytics-custom-fields/initial-count.png)

<span data-ttu-id="ba727-205">因此 new 經過一些時間後收集事件，我們可以看到，hello **Service_CF**欄位現在正在加入 toorecords 符合我們準則。</span><span class="sxs-lookup"><span data-stu-id="ba727-205">After some time has passed so new events are collected, we can see that that hello **Service_CF** field is now being added toorecords that match our criteria.</span></span>

![最終結果](media/log-analytics-custom-fields/final-results.png)

<span data-ttu-id="ba727-207">我們現在可以使用 hello 像任何其他的記錄內容的自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-207">We can now use hello custom field like any other record property.</span></span>  <span data-ttu-id="ba727-208">tooillustrate，我們建立由新的 hello 分組的查詢， **Service_CF**欄位 tooinspect 哪些服務為最常使用的 hello。</span><span class="sxs-lookup"><span data-stu-id="ba727-208">tooillustrate this, we create a query that groups by hello new **Service_CF** field tooinspect which services are hello most active.</span></span>

![以查詢分組](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a><span data-ttu-id="ba727-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba727-210">Next steps</span></span>
* <span data-ttu-id="ba727-211">深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢準則中使用自訂欄位。</span><span class="sxs-lookup"><span data-stu-id="ba727-211">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
* <span data-ttu-id="ba727-212">監視可利用自訂欄位來剖析的[自訂記錄檔](log-analytics-data-sources-custom-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="ba727-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span></span>

