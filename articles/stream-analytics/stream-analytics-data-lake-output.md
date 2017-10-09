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
# <a name="stream-analytics-data-lake-store-output"></a>串流分析 Data Lake Store 輸出
串流分析工作支援數種輸出方法，其中一個是 [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)。 Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。 Data Lake Store 可讓您的作業及探勘分析的任何大小、 類型和擷取速度 toostore 資料。

## <a name="authorize-a-data-lake-store-account"></a>授權 Data Lake Store 帳戶
1. 做為輸出 hello Azure 入口網站中選取資料湖存放區時，您將會提示您現有的資料湖存放區或 toorequest tooauthorize 使用存取 toohello 資料湖存放區 hello 傳統入口網站。
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. 如果您已經有存取 tooData 湖存放區，按一下 [立即授權] 的頁面很短的時間就會出現表示 「 重新導向 tooauthorization"。 hello 頁面將會自動關閉，您會看到與 hello 頁面允許您 tooconfigure hello Data Lake Store 輸出。

如果您有未註冊資料湖存放區，您可以遵循 hello 「 立即註冊使用 」 連結 tooinitiate hello 要求，或遵循 hello[取得啟動的指示](../data-lake-store/data-lake-store-get-started-portal.md)。

## <a name="configure-hello-data-lake-store-output-properties"></a>設定 hello Data Lake Store 輸出屬性
Hello Data Lake Store 帳戶通過驗證之後，您可以設定您 Data Lake Store 的輸出 hello 屬性。 hello 表是屬性名稱和其輸出資料湖存放區的描述 tooconfigure hello 清單。

<table>
<tbody>
<tr>
<td><B>屬性名稱</B></td>
<td><B>說明</B></td>
</tr>
<tr>
<td>輸出別名</td>
<td>這是用於查詢 toodirect hello 查詢輸出 toothis Data Lake Store 的易記名稱。</td>
</tr>
<tr>
<td>Data Lake Store 帳戶</td>
<td>hello hello 傳送輸出的儲存體帳戶名稱。 您會看到一份 hello 登入的使用者具有存取權的 Data Lake Store 帳戶。</td>
</tr>
<tr>
<td>路徑前置詞模式 [<I>選用</I>]</td>
<td>hello 檔案路徑使用 toowrite 內 hello 檔案指定的資料湖存放區帳戶。 <BR>{date}、{time}<BR>範例 1：folder1/logs/{date}/{time}<BR>範例 2：folder1/logs/{date}</td>
</tr>
<tr>
<td>日期格式 [<I>選用</I>]</td>
<td>如果 hello 日期語彙基元不用於 hello 前置詞的路徑，您可以選取組織檔案的 hello 日期格式。 範例：YYYY/MM/DD</td>
</tr>
<tr>
<td>時間格式 [<I>選用</I>]</td>
<td>如果 hello 時間語彙基元 hello 前置詞路徑中，指定組織檔案的 hello 時間格式。 目前僅支援 hello 值是 HH。</td>
</tr>
<tr>
<td>事件序列化格式</td>
<td>輸出資料的序列化格式。 支援 JSON、CSV 和 Avro。</td>
</tr>
<tr>
<td>編碼</td>
<td>若為 CSV 或 JSON 格式，必須指定編碼。 Utf-8 是 hello 此時只支援編碼格式。</td>
</tr>
<tr>
<td>分隔符號</td>
<td>僅適用於 CSV 序列化。 串流分析可支援多種序列化 CSV 資料常用的分隔符號。 支援的值是逗號、分號、空格、索引標籤和分隔號。</td>
</tr>
<tr>
<td>格式</td>
<td>僅適用於 JSON 序列化。 行分隔指定 hello 輸出，將會格式化每個 JSON 物件以新行字元分隔。 陣列指定 hello 輸出將會格式化為 JSON 物件的陣列。</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>更新 Data Lake Store 授權
目前，會有限制 hello 驗證權杖需要 toobe 手動重新整理每隔 90 天的所有工作的輸出資料湖存放區的地方。 您也需要 toore-如果您已變更您的密碼，因為您的工作所建立或上次經過驗證，驗證您 Data Lake Store 帳戶。 此問題的徵兆是沒有作業輸出，表示需要重新授權 hello 作業記錄檔中的錯誤。

tooresolve 這個問題，請停止程式執行的作業，並移 tooyour Data Lake Store 輸出。 按一下 hello 「 更新授權 」 連結，然後短暫頁面就會出現表示 「 重新導向 tooauthorization.."。 hello 頁面會自動關閉，而如果成功，就會指出 「 授權已成功更新 」。 然後在 hello 底部 hello 頁面上，需要 tooclick 儲存，並重新啟動您的工作，從 hello 上次停止時間 tooavoid 資料遺失，可以繼續。

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

