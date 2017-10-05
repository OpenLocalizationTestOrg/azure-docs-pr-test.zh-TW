---
title: "串流分析 Data Lake Store 輸出 | Microsoft Docs"
description: "在串流分析工作中，設定 Azure Data Lake Store 的驗證和授權"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="c93bd-103">串流分析 Data Lake Store 輸出</span><span class="sxs-lookup"><span data-stu-id="c93bd-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="c93bd-104">串流分析工作支援數種輸出方法，其中一個是 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。</span><span class="sxs-lookup"><span data-stu-id="c93bd-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="c93bd-105">Azure 資料湖存放區是容納巨量資料分析工作負載的企業級超大規模存放庫。</span><span class="sxs-lookup"><span data-stu-id="c93bd-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="c93bd-106">Data Lake Store 可讓您存放任何大小、類型和擷取速度的資料，以便進行運作和探究分析。</span><span class="sxs-lookup"><span data-stu-id="c93bd-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="c93bd-107">授權 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="c93bd-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="c93bd-108">在 Azure 入口網站中選取 Data Lake Store 作為輸出時，系統會提示您授權使用現有的 Data Lake Store，或要求透過 Azure 傳統入口網站存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="c93bd-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="c93bd-109">如果您已經可以存取 Data Lake Store，按一下 [立即授權]，很快就會出現一個頁面，指出「正在重新導向至授權」。</span><span class="sxs-lookup"><span data-stu-id="c93bd-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="c93bd-110">此頁面將會自動關閉，而且您會看到可讓您設定 Data Lake Store 輸出的頁面。</span><span class="sxs-lookup"><span data-stu-id="c93bd-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="c93bd-111">如果您尚未註冊 Data Lake Store，您可以依照「立即註冊」連結起始要求，或依照[開始使用指示](../data-lake-store/data-lake-store-get-started-portal.md)進行。</span><span class="sxs-lookup"><span data-stu-id="c93bd-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="c93bd-112">設定 Data Lake Store 輸出屬性</span><span class="sxs-lookup"><span data-stu-id="c93bd-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="c93bd-113">驗證 Data Lake Store 帳戶之後，您可以設定 Data Lake Store 輸出的屬性。</span><span class="sxs-lookup"><span data-stu-id="c93bd-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="c93bd-114">下表是設定 Data Lake Store 輸出的屬性名稱及其描述的清單。</span><span class="sxs-lookup"><span data-stu-id="c93bd-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="c93bd-115"><B>屬性名稱</B></span><span class="sxs-lookup"><span data-stu-id="c93bd-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="c93bd-116"><B>說明</B></span><span class="sxs-lookup"><span data-stu-id="c93bd-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-117">輸出別名</span><span class="sxs-lookup"><span data-stu-id="c93bd-117">Output Alias</span></span></td>
<td><span data-ttu-id="c93bd-118">此為易記名稱，用於在查詢中將查詢輸出指向這個 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="c93bd-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-119">Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="c93bd-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="c93bd-120">您傳送輸出的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c93bd-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="c93bd-121">您會看到一份登入使用者具有存取權的 Data Lake Store 帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="c93bd-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-122">路徑前置詞模式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="c93bd-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="c93bd-123">用來在指定的 Data Lake Store 帳戶中寫入檔案的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c93bd-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="c93bd-124">{date}、{time}</span><span class="sxs-lookup"><span data-stu-id="c93bd-124">{date}, {time}</span></span><BR><span data-ttu-id="c93bd-125">範例 1：folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="c93bd-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="c93bd-126">範例 2：folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="c93bd-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-127">日期格式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="c93bd-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="c93bd-128">如果前置詞路徑中使用日期權杖，您可以選取組織檔案要用的日期格式。</span><span class="sxs-lookup"><span data-stu-id="c93bd-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="c93bd-129">範例：YYYY/MM/DD</span><span class="sxs-lookup"><span data-stu-id="c93bd-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-130">時間格式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="c93bd-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="c93bd-131">如果前置詞路徑中使用時間權杖，請指定組織檔案要用的時間格式。</span><span class="sxs-lookup"><span data-stu-id="c93bd-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="c93bd-132">目前唯一支援的值為 HH。</span><span class="sxs-lookup"><span data-stu-id="c93bd-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-133">事件序列化格式</span><span class="sxs-lookup"><span data-stu-id="c93bd-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="c93bd-134">輸出資料的序列化格式。</span><span class="sxs-lookup"><span data-stu-id="c93bd-134">Serialization format for output data.</span></span> <span data-ttu-id="c93bd-135">支援 JSON、CSV 和 Avro。</span><span class="sxs-lookup"><span data-stu-id="c93bd-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-136">編碼</span><span class="sxs-lookup"><span data-stu-id="c93bd-136">Encoding</span></span></td>
<td><span data-ttu-id="c93bd-137">若為 CSV 或 JSON 格式，必須指定編碼。</span><span class="sxs-lookup"><span data-stu-id="c93bd-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="c93bd-138">UTF-8 是目前唯一支援的編碼格式。</span><span class="sxs-lookup"><span data-stu-id="c93bd-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-139">分隔符號</span><span class="sxs-lookup"><span data-stu-id="c93bd-139">Delimiter</span></span></td>
<td><span data-ttu-id="c93bd-140">僅適用於 CSV 序列化。</span><span class="sxs-lookup"><span data-stu-id="c93bd-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="c93bd-141">串流分析可支援多種序列化 CSV 資料常用的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="c93bd-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="c93bd-142">支援的值是逗號、分號、空格、索引標籤和分隔號。</span><span class="sxs-lookup"><span data-stu-id="c93bd-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="c93bd-143">格式</span><span class="sxs-lookup"><span data-stu-id="c93bd-143">Format</span></span></td>
<td><span data-ttu-id="c93bd-144">僅適用於 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="c93bd-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="c93bd-145">分隔的行會指定輸出的格式化方式為利用新行分隔每個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="c93bd-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="c93bd-146">陣列會指定輸出將會格式化為 JSON 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="c93bd-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="c93bd-147">更新 Data Lake Store 授權</span><span class="sxs-lookup"><span data-stu-id="c93bd-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="c93bd-148">目前有一個限制，即每隔 90 天必須針對 Data Lake Store 輸出的所有工作，以手動方式更新驗證 Token。</span><span class="sxs-lookup"><span data-stu-id="c93bd-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="c93bd-149">如果您在建立工作之後或上次驗證過後變更了密碼，您也必須重新驗證您的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93bd-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="c93bd-150">此問題發生時的徵兆就是沒有工作輸出，且作業記錄檔中出現錯誤，表示需要重新授權。</span><span class="sxs-lookup"><span data-stu-id="c93bd-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="c93bd-151">若要解決這個問題，請停止執行中的工作，並移至 Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="c93bd-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="c93bd-152">按一下 [更新授權] 連結，很快就會出現一個頁面，指出 「正在重新導向至授權...」。</span><span class="sxs-lookup"><span data-stu-id="c93bd-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="c93bd-153">此頁面將會自動關閉，而且如果成功，就會指出「已成功更新授權」。</span><span class="sxs-lookup"><span data-stu-id="c93bd-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="c93bd-154">接著，您必須按一下頁面底部的 [儲存]，然後可以從上次停止的時間重新開始您的工作繼續，以避免資料遺失。</span><span class="sxs-lookup"><span data-stu-id="c93bd-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

