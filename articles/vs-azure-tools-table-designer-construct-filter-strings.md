---
title: "建構資料表設計工具的篩選字串 | Microsoft Docs"
description: "建構資料表設計工具的篩選字串"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 069224d84462b4955912ce1462a65298a5acc04a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="constructing-filter-strings-for-the-table-designer"></a><span data-ttu-id="4e96d-103">建構資料表設計工具的篩選字串</span><span class="sxs-lookup"><span data-stu-id="4e96d-103">Constructing Filter Strings for the Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="4e96d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4e96d-104">Overview</span></span>
<span data-ttu-id="4e96d-105">若要在 Visual Studio [資料表設計工具] 中顯示的 Azure 資料表中篩選資料，您可以建構篩選字串並在篩選欄位中輸入它。</span><span class="sxs-lookup"><span data-stu-id="4e96d-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span></span> <span data-ttu-id="4e96d-106">篩選條件字串語法由 WCF Data Services 定義，類似於 SQL WHERE 子句，但會透過 HTTP 要求傳送至表格服務。</span><span class="sxs-lookup"><span data-stu-id="4e96d-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span></span> <span data-ttu-id="4e96d-107">[資料表設計工具]  會為您處理適當的編碼，因此，若要篩選所需的屬性值，您只需要在篩選欄位中輸入屬性名稱、比較運算子、準則值和 (選擇性) 布林運算子。</span><span class="sxs-lookup"><span data-stu-id="4e96d-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span></span> <span data-ttu-id="4e96d-108">您不需要像透過 [儲存體服務 REST API 參考](http://go.microsoft.com/fwlink/p/?LinkId=400447)建構 URL 來查詢資料表一樣包含 $filter 查詢選項。</span><span class="sxs-lookup"><span data-stu-id="4e96d-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="4e96d-109">WCF Data Services 以 [開放式資料通訊協定](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="4e96d-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="4e96d-110">如需篩選系統查詢選項 (**$filter**) 的詳細資訊，請參閱 [OData URI 轉換規格](http://go.microsoft.com/fwlink/p/?LinkId=214806)。</span><span class="sxs-lookup"><span data-stu-id="4e96d-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="4e96d-111">比較運算子</span><span class="sxs-lookup"><span data-stu-id="4e96d-111">Comparison Operators</span></span>
<span data-ttu-id="4e96d-112">所有屬性類型都支援下列邏輯運算子：</span><span class="sxs-lookup"><span data-stu-id="4e96d-112">The following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="4e96d-113">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="4e96d-113">Logical operator</span></span> | <span data-ttu-id="4e96d-114">說明</span><span class="sxs-lookup"><span data-stu-id="4e96d-114">Description</span></span> | <span data-ttu-id="4e96d-115">篩選字串範例</span><span class="sxs-lookup"><span data-stu-id="4e96d-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e96d-116">eq</span><span class="sxs-lookup"><span data-stu-id="4e96d-116">eq</span></span> |<span data-ttu-id="4e96d-117">等於</span><span class="sxs-lookup"><span data-stu-id="4e96d-117">Equal</span></span> |<span data-ttu-id="4e96d-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="4e96d-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="4e96d-119">gt</span><span class="sxs-lookup"><span data-stu-id="4e96d-119">gt</span></span> |<span data-ttu-id="4e96d-120">大於</span><span class="sxs-lookup"><span data-stu-id="4e96d-120">Greater than</span></span> |<span data-ttu-id="4e96d-121">Price gt 20</span><span class="sxs-lookup"><span data-stu-id="4e96d-121">Price gt 20</span></span> |
| <span data-ttu-id="4e96d-122">ge</span><span class="sxs-lookup"><span data-stu-id="4e96d-122">ge</span></span> |<span data-ttu-id="4e96d-123">大於或等於</span><span class="sxs-lookup"><span data-stu-id="4e96d-123">Greater than or equal to</span></span> |<span data-ttu-id="4e96d-124">Price ge 10</span><span class="sxs-lookup"><span data-stu-id="4e96d-124">Price ge 10</span></span> |
| <span data-ttu-id="4e96d-125">lt</span><span class="sxs-lookup"><span data-stu-id="4e96d-125">lt</span></span> |<span data-ttu-id="4e96d-126">小於</span><span class="sxs-lookup"><span data-stu-id="4e96d-126">Less than</span></span> |<span data-ttu-id="4e96d-127">Price lt 20</span><span class="sxs-lookup"><span data-stu-id="4e96d-127">Price lt 20</span></span> |
| <span data-ttu-id="4e96d-128">le</span><span class="sxs-lookup"><span data-stu-id="4e96d-128">le</span></span> |<span data-ttu-id="4e96d-129">小於或等於</span><span class="sxs-lookup"><span data-stu-id="4e96d-129">Less than or equal</span></span> |<span data-ttu-id="4e96d-130">Price le 100</span><span class="sxs-lookup"><span data-stu-id="4e96d-130">Price le 100</span></span> |
| <span data-ttu-id="4e96d-131">ne</span><span class="sxs-lookup"><span data-stu-id="4e96d-131">ne</span></span> |<span data-ttu-id="4e96d-132">不等於</span><span class="sxs-lookup"><span data-stu-id="4e96d-132">Not equal</span></span> |<span data-ttu-id="4e96d-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="4e96d-133">City ne 'London'</span></span> |
| <span data-ttu-id="4e96d-134">和</span><span class="sxs-lookup"><span data-stu-id="4e96d-134">and</span></span> |<span data-ttu-id="4e96d-135">和</span><span class="sxs-lookup"><span data-stu-id="4e96d-135">And</span></span> |<span data-ttu-id="4e96d-136">Price le 200 and Price gt 3.5</span><span class="sxs-lookup"><span data-stu-id="4e96d-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="4e96d-137">或</span><span class="sxs-lookup"><span data-stu-id="4e96d-137">or</span></span> |<span data-ttu-id="4e96d-138">或</span><span class="sxs-lookup"><span data-stu-id="4e96d-138">Or</span></span> |<span data-ttu-id="4e96d-139">Price le 3.5 or Price gt 200</span><span class="sxs-lookup"><span data-stu-id="4e96d-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="4e96d-140">否</span><span class="sxs-lookup"><span data-stu-id="4e96d-140">not</span></span> |<span data-ttu-id="4e96d-141">否</span><span class="sxs-lookup"><span data-stu-id="4e96d-141">Not</span></span> |<span data-ttu-id="4e96d-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="4e96d-142">not isAvailable</span></span> |

<span data-ttu-id="4e96d-143">建構篩選字串時，下列規則很重要：</span><span class="sxs-lookup"><span data-stu-id="4e96d-143">When constructing a filter string, the following rules are important:</span></span>

* <span data-ttu-id="4e96d-144">使用邏輯運算子來比較屬性與值。</span><span class="sxs-lookup"><span data-stu-id="4e96d-144">Use the logical operators to compare a property to a value.</span></span> <span data-ttu-id="4e96d-145">請注意，無法比較屬性與動態值。運算式的一端必須是常數。</span><span class="sxs-lookup"><span data-stu-id="4e96d-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span></span>
* <span data-ttu-id="4e96d-146">篩選字串的所有部分都區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4e96d-146">All parts of the filter string are case-sensitive.</span></span>
* <span data-ttu-id="4e96d-147">常數和屬性必須是相同的資料類型，篩選才能傳回有效的結果。</span><span class="sxs-lookup"><span data-stu-id="4e96d-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="4e96d-148">如需支援的屬性類型的詳細資訊，請參閱 [了解表格服務資料模型](http://go.microsoft.com/fwlink/p/?LinkId=400448)。</span><span class="sxs-lookup"><span data-stu-id="4e96d-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="4e96d-149">篩選字串屬性</span><span class="sxs-lookup"><span data-stu-id="4e96d-149">Filtering on String Properties</span></span>
<span data-ttu-id="4e96d-150">當您篩選字串屬性時，請用單引號括住字串常數。</span><span class="sxs-lookup"><span data-stu-id="4e96d-150">When you filter on string properties, enclose the string constant in single quotation marks.</span></span>

<span data-ttu-id="4e96d-151">下列範例會篩選 **PartitionKey** 和 **RowKey** 屬性。額外的非索引鍵屬性也可以加入至篩選字串：</span><span class="sxs-lookup"><span data-stu-id="4e96d-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="4e96d-152">您可以用括號括住每個篩選運算式 (雖然並非必要)：</span><span class="sxs-lookup"><span data-stu-id="4e96d-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="4e96d-153">請注意，表格服務不支援萬用字元查詢，在 [資料表設計工具] 中也不支援。</span><span class="sxs-lookup"><span data-stu-id="4e96d-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span></span> <span data-ttu-id="4e96d-154">不過，您可以在所需的前置詞上使用比較運算子，以執行前置詞比對。</span><span class="sxs-lookup"><span data-stu-id="4e96d-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span></span> <span data-ttu-id="4e96d-155">下列範例會傳回 LastName 屬性開頭為字母 'A' 的實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-155">The following example returns entities with a LastName property beginning with the letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="4e96d-156">篩選數值屬性</span><span class="sxs-lookup"><span data-stu-id="4e96d-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="4e96d-157">若要篩選整數或浮點數，指定數值且不加引號。</span><span class="sxs-lookup"><span data-stu-id="4e96d-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span></span>

<span data-ttu-id="4e96d-158">這個範例會傳回與 Age 屬性的值大於 30 的所有實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="4e96d-159">這個範例會傳回與 AmountDue 屬性的值小於或等於 100.25 的所有實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="4e96d-160">篩選布林值屬性</span><span class="sxs-lookup"><span data-stu-id="4e96d-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="4e96d-161">若要篩選布林值，請指定 **true** 或 **false** 且不加引號。</span><span class="sxs-lookup"><span data-stu-id="4e96d-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="4e96d-162">下列範例會傳回 IsActive 屬性設定為 **true**的所有實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-162">The following example returns all entities where the IsActive property is set to **true**:</span></span>

    IsActive eq true

<span data-ttu-id="4e96d-163">您也可以不加邏輯運算子來撰寫這個篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="4e96d-163">You can also write this filter expression without the logical operator.</span></span> <span data-ttu-id="4e96d-164">在下列範例中，表格服務也會傳回 IsActive 為 **true**的所有實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="4e96d-165">若要傳回 IsActive 為 false 的所有實體，您可以使用 not 運算子：</span><span class="sxs-lookup"><span data-stu-id="4e96d-165">To return all entities where IsActive is false, you can use the not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="4e96d-166">篩選 DateTime 屬性</span><span class="sxs-lookup"><span data-stu-id="4e96d-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="4e96d-167">若要 DateTime 值，請指定 **datetime** 關鍵字，後面加上以單引號括住的日期/時間常數。</span><span class="sxs-lookup"><span data-stu-id="4e96d-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span></span> <span data-ttu-id="4e96d-168">日期/時間常數必須使用 UTC 組合格式，如 [格式化 DateTime 屬性值](http://go.microsoft.com/fwlink/p/?LinkId=400449)所述。</span><span class="sxs-lookup"><span data-stu-id="4e96d-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="4e96d-169">下列範例會傳回 CustomerSince 屬性等於 2008 年 7 月 10 日的實體：</span><span class="sxs-lookup"><span data-stu-id="4e96d-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
