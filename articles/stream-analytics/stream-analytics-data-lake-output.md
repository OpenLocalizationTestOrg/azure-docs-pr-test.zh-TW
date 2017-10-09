---
title: "分析資料湖存放區輸出 aaaStream |Microsoft 文件"
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
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="6fa86-103">串流分析 Data Lake Store 輸出</span><span class="sxs-lookup"><span data-stu-id="6fa86-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="6fa86-104">串流分析工作支援數種輸出方法，其中一個是 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。</span><span class="sxs-lookup"><span data-stu-id="6fa86-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="6fa86-105">Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。</span><span class="sxs-lookup"><span data-stu-id="6fa86-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="6fa86-106">Data Lake Store 可讓您的作業及探勘分析的任何大小、 類型和擷取速度 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="6fa86-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="6fa86-107">授權 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="6fa86-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="6fa86-108">做為輸出 hello Azure 入口網站中選取資料湖存放區時，您將會提示您現有的資料湖存放區或 toorequest tooauthorize 使用存取 toohello 資料湖存放區 hello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fa86-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="6fa86-109">如果您已經有存取 tooData 湖存放區，按一下 [立即授權] 的頁面很短的時間就會出現表示 「 重新導向 tooauthorization"。</span><span class="sxs-lookup"><span data-stu-id="6fa86-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="6fa86-110">hello 頁面將會自動關閉，您會看到與 hello 頁面允許您 tooconfigure hello Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="6fa86-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="6fa86-111">如果您有未註冊資料湖存放區，您可以遵循 hello 「 立即註冊使用 」 連結 tooinitiate hello 要求，或遵循 hello[取得啟動的指示](../data-lake-store/data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa86-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="6fa86-112">設定 hello Data Lake Store 輸出屬性</span><span class="sxs-lookup"><span data-stu-id="6fa86-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="6fa86-113">Hello Data Lake Store 帳戶通過驗證之後，您可以設定您 Data Lake Store 的輸出 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6fa86-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="6fa86-114">hello 表是屬性名稱和其輸出資料湖存放區的描述 tooconfigure hello 清單。</span><span class="sxs-lookup"><span data-stu-id="6fa86-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="6fa86-115"><B>屬性名稱</B></span><span class="sxs-lookup"><span data-stu-id="6fa86-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="6fa86-116"><B>說明</B></span><span class="sxs-lookup"><span data-stu-id="6fa86-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-117">輸出別名</span><span class="sxs-lookup"><span data-stu-id="6fa86-117">Output Alias</span></span></td>
<td><span data-ttu-id="6fa86-118">這是用於查詢 toodirect hello 查詢輸出 toothis Data Lake Store 的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa86-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-119">Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="6fa86-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="6fa86-120">hello hello 傳送輸出的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa86-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="6fa86-121">您會看到一份 hello 登入的使用者具有存取權的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fa86-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-122">路徑前置詞模式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="6fa86-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6fa86-123">hello 檔案路徑使用 toowrite 內 hello 檔案指定的資料湖存放區帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fa86-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="6fa86-124">{date}、{time}</span><span class="sxs-lookup"><span data-stu-id="6fa86-124">{date}, {time}</span></span><BR><span data-ttu-id="6fa86-125">範例 1：folder1/logs/{date}/{time}</span><span class="sxs-lookup"><span data-stu-id="6fa86-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="6fa86-126">範例 2：folder1/logs/{date}</span><span class="sxs-lookup"><span data-stu-id="6fa86-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-127">日期格式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="6fa86-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6fa86-128">如果 hello 日期語彙基元不用於 hello 前置詞的路徑，您可以選取組織檔案的 hello 日期格式。</span><span class="sxs-lookup"><span data-stu-id="6fa86-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="6fa86-129">範例：YYYY/MM/DD</span><span class="sxs-lookup"><span data-stu-id="6fa86-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-130">時間格式 [<I>選用</I>]</span><span class="sxs-lookup"><span data-stu-id="6fa86-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="6fa86-131">如果 hello 時間語彙基元 hello 前置詞路徑中，指定組織檔案的 hello 時間格式。</span><span class="sxs-lookup"><span data-stu-id="6fa86-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="6fa86-132">目前僅支援 hello 值是 HH。</span><span class="sxs-lookup"><span data-stu-id="6fa86-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-133">事件序列化格式</span><span class="sxs-lookup"><span data-stu-id="6fa86-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="6fa86-134">輸出資料的序列化格式。</span><span class="sxs-lookup"><span data-stu-id="6fa86-134">Serialization format for output data.</span></span> <span data-ttu-id="6fa86-135">支援 JSON、CSV 和 Avro。</span><span class="sxs-lookup"><span data-stu-id="6fa86-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-136">編碼</span><span class="sxs-lookup"><span data-stu-id="6fa86-136">Encoding</span></span></td>
<td><span data-ttu-id="6fa86-137">若為 CSV 或 JSON 格式，必須指定編碼。</span><span class="sxs-lookup"><span data-stu-id="6fa86-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="6fa86-138">Utf-8 是 hello 此時只支援編碼格式。</span><span class="sxs-lookup"><span data-stu-id="6fa86-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-139">分隔符號</span><span class="sxs-lookup"><span data-stu-id="6fa86-139">Delimiter</span></span></td>
<td><span data-ttu-id="6fa86-140">僅適用於 CSV 序列化。</span><span class="sxs-lookup"><span data-stu-id="6fa86-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="6fa86-141">串流分析可支援多種序列化 CSV 資料常用的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="6fa86-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="6fa86-142">支援的值是逗號、分號、空格、索引標籤和分隔號。</span><span class="sxs-lookup"><span data-stu-id="6fa86-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6fa86-143">格式</span><span class="sxs-lookup"><span data-stu-id="6fa86-143">Format</span></span></td>
<td><span data-ttu-id="6fa86-144">僅適用於 JSON 序列化。</span><span class="sxs-lookup"><span data-stu-id="6fa86-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="6fa86-145">行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。</span><span class="sxs-lookup"><span data-stu-id="6fa86-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="6fa86-146">陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="6fa86-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="6fa86-147">更新 Data Lake Store 授權</span><span class="sxs-lookup"><span data-stu-id="6fa86-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="6fa86-148">目前，會有限制 hello 驗證權杖需要 toobe 手動重新整理每隔 90 天的所有工作的輸出資料湖存放區的地方。</span><span class="sxs-lookup"><span data-stu-id="6fa86-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="6fa86-149">您也需要 toore-如果您已變更您的密碼，因為您的工作所建立或上次經過驗證，驗證您 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fa86-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="6fa86-150">此問題的徵兆是沒有作業輸出，表示需要重新授權 hello 作業記錄檔中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6fa86-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="6fa86-151">tooresolve 這個問題，請停止程式執行的作業，並移 tooyour Data Lake Store 輸出。</span><span class="sxs-lookup"><span data-stu-id="6fa86-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="6fa86-152">按一下 hello 「 更新授權 」 連結，然後短暫頁面就會出現表示 「 重新導向 tooauthorization.."。</span><span class="sxs-lookup"><span data-stu-id="6fa86-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="6fa86-153">hello 頁面會自動關閉，而如果成功，就會指出 「 授權已成功更新 」。</span><span class="sxs-lookup"><span data-stu-id="6fa86-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="6fa86-154">然後在 hello 底部 hello 頁面上，需要 tooclick 儲存，並重新啟動您的工作，從 hello 上次停止時間 tooavoid 資料遺失，可以繼續。</span><span class="sxs-lookup"><span data-stu-id="6fa86-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

