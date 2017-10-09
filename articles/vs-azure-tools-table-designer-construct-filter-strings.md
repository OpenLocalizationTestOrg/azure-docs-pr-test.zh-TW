---
title: "aaaConstructing 篩選字串 hello 資料表設計工具的 |Microsoft 文件"
description: "建構篩選字串 hello 資料表設計工具"
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
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="42311-103">建構篩選字串 hello 資料表設計工具</span><span class="sxs-lookup"><span data-stu-id="42311-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="42311-104">概觀</span><span class="sxs-lookup"><span data-stu-id="42311-104">Overview</span></span>
<span data-ttu-id="42311-105">在 Azure 資料表中所顯示的 toofilter 資料 hello Visual Studio**資料表設計工具**，建構篩選字串，並將其輸入 hello 篩選欄位。</span><span class="sxs-lookup"><span data-stu-id="42311-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="42311-106">hello 篩選條件字串語法由 hello WCF 資料服務所定義且類似 tooa SQL WHERE 子句，但會傳送 toohello 表格服務透過 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="42311-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="42311-107">hello**資料表設計工具**控點 hello 適當編碼方式，為您在想要的屬性值，因此 toofilter，您只需要輸入 hello 屬性的名稱、 比較運算子準則值，而且 hello 中的布林運算子來篩選 （選擇性）欄位。</span><span class="sxs-lookup"><span data-stu-id="42311-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="42311-108">您不需要 tooinclude hello $filter 查詢選項時您所建構 URL tooquery hello 資料表透過 hello[儲存體服務 REST API 參考](http://go.microsoft.com/fwlink/p/?LinkId=400447)。</span><span class="sxs-lookup"><span data-stu-id="42311-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="42311-109">hello WCF Data Services 根據 hello[開放式資料通訊協定](http://go.microsoft.com/fwlink/p/?LinkId=214805)(OData)。</span><span class="sxs-lookup"><span data-stu-id="42311-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="42311-110">如需詳細資訊，在 hello 篩選系統查詢選項 (**$filter**)，請參閱 hello [OData URI 轉換規格](http://go.microsoft.com/fwlink/p/?LinkId=214806)。</span><span class="sxs-lookup"><span data-stu-id="42311-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="42311-111">比較運算子</span><span class="sxs-lookup"><span data-stu-id="42311-111">Comparison Operators</span></span>
<span data-ttu-id="42311-112">hello 邏輯支援下列運算子的所有屬性類型：</span><span class="sxs-lookup"><span data-stu-id="42311-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="42311-113">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="42311-113">Logical operator</span></span> | <span data-ttu-id="42311-114">說明</span><span class="sxs-lookup"><span data-stu-id="42311-114">Description</span></span> | <span data-ttu-id="42311-115">篩選字串範例</span><span class="sxs-lookup"><span data-stu-id="42311-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42311-116">eq</span><span class="sxs-lookup"><span data-stu-id="42311-116">eq</span></span> |<span data-ttu-id="42311-117">等於</span><span class="sxs-lookup"><span data-stu-id="42311-117">Equal</span></span> |<span data-ttu-id="42311-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="42311-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="42311-119">gt</span><span class="sxs-lookup"><span data-stu-id="42311-119">gt</span></span> |<span data-ttu-id="42311-120">大於</span><span class="sxs-lookup"><span data-stu-id="42311-120">Greater than</span></span> |<span data-ttu-id="42311-121">Price gt 20</span><span class="sxs-lookup"><span data-stu-id="42311-121">Price gt 20</span></span> |
| <span data-ttu-id="42311-122">ge</span><span class="sxs-lookup"><span data-stu-id="42311-122">ge</span></span> |<span data-ttu-id="42311-123">大於或等於太</span><span class="sxs-lookup"><span data-stu-id="42311-123">Greater than or equal too</span></span>|<span data-ttu-id="42311-124">Price ge 10</span><span class="sxs-lookup"><span data-stu-id="42311-124">Price ge 10</span></span> |
| <span data-ttu-id="42311-125">lt</span><span class="sxs-lookup"><span data-stu-id="42311-125">lt</span></span> |<span data-ttu-id="42311-126">小於</span><span class="sxs-lookup"><span data-stu-id="42311-126">Less than</span></span> |<span data-ttu-id="42311-127">Price lt 20</span><span class="sxs-lookup"><span data-stu-id="42311-127">Price lt 20</span></span> |
| <span data-ttu-id="42311-128">le</span><span class="sxs-lookup"><span data-stu-id="42311-128">le</span></span> |<span data-ttu-id="42311-129">小於或等於</span><span class="sxs-lookup"><span data-stu-id="42311-129">Less than or equal</span></span> |<span data-ttu-id="42311-130">Price le 100</span><span class="sxs-lookup"><span data-stu-id="42311-130">Price le 100</span></span> |
| <span data-ttu-id="42311-131">ne</span><span class="sxs-lookup"><span data-stu-id="42311-131">ne</span></span> |<span data-ttu-id="42311-132">不等於</span><span class="sxs-lookup"><span data-stu-id="42311-132">Not equal</span></span> |<span data-ttu-id="42311-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="42311-133">City ne 'London'</span></span> |
| <span data-ttu-id="42311-134">和</span><span class="sxs-lookup"><span data-stu-id="42311-134">and</span></span> |<span data-ttu-id="42311-135">和</span><span class="sxs-lookup"><span data-stu-id="42311-135">And</span></span> |<span data-ttu-id="42311-136">Price le 200 and Price gt 3.5</span><span class="sxs-lookup"><span data-stu-id="42311-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="42311-137">或</span><span class="sxs-lookup"><span data-stu-id="42311-137">or</span></span> |<span data-ttu-id="42311-138">或</span><span class="sxs-lookup"><span data-stu-id="42311-138">Or</span></span> |<span data-ttu-id="42311-139">Price le 3.5 or Price gt 200</span><span class="sxs-lookup"><span data-stu-id="42311-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="42311-140">否</span><span class="sxs-lookup"><span data-stu-id="42311-140">not</span></span> |<span data-ttu-id="42311-141">否</span><span class="sxs-lookup"><span data-stu-id="42311-141">Not</span></span> |<span data-ttu-id="42311-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="42311-142">not isAvailable</span></span> |

<span data-ttu-id="42311-143">建構篩選字串時，hello 下列規則很重要：</span><span class="sxs-lookup"><span data-stu-id="42311-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="42311-144">使用 hello 邏輯運算子 toocompare 屬性 tooa 值。</span><span class="sxs-lookup"><span data-stu-id="42311-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="42311-145">請注意，它不可能 toocompare 屬性 tooa 動態值。hello 運算式的一端必須是常數。</span><span class="sxs-lookup"><span data-stu-id="42311-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="42311-146">Hello 篩選字串的所有部分都都區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="42311-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="42311-147">hello hello 常值必須是相同的資料類型作為 hello 篩選 tooreturn 有效結果的順序中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="42311-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="42311-148">如需支援的屬性類型的詳細資訊，請參閱[了解 hello 表格服務資料模型](http://go.microsoft.com/fwlink/p/?LinkId=400448)。</span><span class="sxs-lookup"><span data-stu-id="42311-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="42311-149">篩選字串屬性</span><span class="sxs-lookup"><span data-stu-id="42311-149">Filtering on String Properties</span></span>
<span data-ttu-id="42311-150">當您篩選字串屬性時，請使用單引號括住 hello 字串常數。</span><span class="sxs-lookup"><span data-stu-id="42311-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="42311-151">hello hello 在下列範例會篩選**PartitionKey**和**RowKey**屬性，其他的非索引鍵屬性也可以加入 toohello 篩選字串：</span><span class="sxs-lookup"><span data-stu-id="42311-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="42311-152">您可以用括號括住每個篩選運算式 (雖然並非必要)：</span><span class="sxs-lookup"><span data-stu-id="42311-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="42311-153">請注意，hello 表格服務不支援萬用字元查詢中，不支援在 hello 資料表設計工具是。</span><span class="sxs-lookup"><span data-stu-id="42311-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="42311-154">不過，您可以執行比對的方式在 hello 想要的首碼使用比較運算子的前置詞。</span><span class="sxs-lookup"><span data-stu-id="42311-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="42311-155">hello 下列範例會傳回包含以 hello 字母 'A' 開頭的姓氏屬性的實體：</span><span class="sxs-lookup"><span data-stu-id="42311-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="42311-156">篩選數值屬性</span><span class="sxs-lookup"><span data-stu-id="42311-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="42311-157">toofilter 整數或浮點數，指定不加引號的 hello 數字。</span><span class="sxs-lookup"><span data-stu-id="42311-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="42311-158">這個範例會傳回與 Age 屬性的值大於 30 的所有實體：</span><span class="sxs-lookup"><span data-stu-id="42311-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="42311-159">這個範例會傳回具有 AmountDue 屬性且屬性值的所有實體小於或等於 too100.25:</span><span class="sxs-lookup"><span data-stu-id="42311-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="42311-160">篩選布林值屬性</span><span class="sxs-lookup"><span data-stu-id="42311-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="42311-161">toofilter 布林值，指定**true**或**false**不需要引號。</span><span class="sxs-lookup"><span data-stu-id="42311-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="42311-162">hello 下列範例會傳回所有實體 hello IsActive 屬性設定的位置太**true**:</span><span class="sxs-lookup"><span data-stu-id="42311-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="42311-163">您也可以撰寫此篩選條件運算式，不含 hello 邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="42311-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="42311-164">在下列範例的 hello，hello 表格服務也會傳回所有實體所在 IsActive **true**:</span><span class="sxs-lookup"><span data-stu-id="42311-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="42311-165">IsActive 所在位置為 false，您可以使用的所有實體不都 hello 的 tooreturn 運算子：</span><span class="sxs-lookup"><span data-stu-id="42311-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="42311-166">篩選 DateTime 屬性</span><span class="sxs-lookup"><span data-stu-id="42311-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="42311-167">toofilter 針對 DateTime 值，指定 hello **datetime**關鍵字，後面接著以單引號 hello 日期/時間常數。</span><span class="sxs-lookup"><span data-stu-id="42311-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="42311-168">中所述，hello 日期/時間常數必須是 UTC 組合格式，[格式化 DateTime 屬性值](http://go.microsoft.com/fwlink/p/?LinkId=400449)。</span><span class="sxs-lookup"><span data-stu-id="42311-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="42311-169">下列範例中的 hello 傳回實體其中 hello CustomerSince 屬性等於 tooJuly 10，2008年:</span><span class="sxs-lookup"><span data-stu-id="42311-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
