---
title: "利用 HDInsight 中的 Hive 分析和處理 JSON 文件 | Microsoft Docs"
description: "了解如何使用 JSON 文件，以集使用 HDInsight 中的 Hive 分析它們。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="3dd1d-103">使用 HDInsight 中的 Hive 處理並分析 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="3dd1d-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="3dd1d-104">了解如何使用 HDInsight 中的 Hive 處理並分析 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="3dd1d-105">本教學課程中將使用下列 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-105">The following JSON document is used in the tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="3dd1d-106">檔案位於 wasb://processjson@hditutorialdata.blob.core.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="3dd1d-107">如需關於搭配 HDInsight 使用 Azure Blob 儲存體的詳細資訊，請參閱[在 HDInsight 上搭配 Hadoop 使用 HDFS 相容的 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="3dd1d-108">您可以將檔案複製到叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="3dd1d-109">在本教學課程中，您會使用 Hive 主控台。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="3dd1d-110">如需開啟 Hive 主控台的指示，請參閱 [利用遠端桌面搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-hadoop-use-hive-remote-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="3dd1d-111">簡維 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="3dd1d-111">Flatten JSON documents</span></span>
<span data-ttu-id="3dd1d-112">下一節所列的方法需要 JSON 文件在單一資料列中。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="3dd1d-113">因此，您必須將 JSON 文件簡維成一個字串。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="3dd1d-114">如果已簡維 JSON 文件，您就可以略過此步驟，直接進入與分析 JSON 資料相關的下一節。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="3dd1d-115">原始 JSON 檔案位於 **wasb://processjson@hditutorialdata.blob.core.windows.net/**。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="3dd1d-116">StudentsRaw Hive 資料表會指向原始未扁平化的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="3dd1d-117">StudentsOneLine Hive 資料表會將資料儲存在 HDInsight 預設檔案系統的 /json/students/ 路徑下。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="3dd1d-118">INSERT 陳述式會將扁平化的 JSON 資料填入 StudentOneLine 資料表。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="3dd1d-119">SELECT 陳述式應該只會傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="3dd1d-120">以下是 SELECT 陳述式的輸出：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-120">Here is the output of the SELECT statement:</span></span>

![JSON 文件簡維。][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="3dd1d-122">在 Hive 中分析 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="3dd1d-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="3dd1d-123">Hive 提供三種不同的機制，可在 JSON 文件上執行查詢：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="3dd1d-124">使用 GET\_JSON\_OBJECT UDF (使用者定義函式)</span><span class="sxs-lookup"><span data-stu-id="3dd1d-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="3dd1d-125">使用 JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="3dd1d-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="3dd1d-126">使用自訂 SerDe</span><span class="sxs-lookup"><span data-stu-id="3dd1d-126">use custom SerDe</span></span>
* <span data-ttu-id="3dd1d-127">使用 Python 或其他語言撰寫您自己的 UDF。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="3dd1d-128">請參閱[這篇文章][hdinsight-python]，了解如何使用 Hive 執行您自己的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="3dd1d-129">使用 GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="3dd1d-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="3dd1d-130">Hive 提供的內建 UDF 稱為 [get json objec](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)，可在執行階段期間執行 JSON 查詢。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="3dd1d-131">此方法採用兩個引數 – 資料表名稱和方法名稱，後者具有扁平化的 JSON 文件和必須剖析的 JSON 欄位。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="3dd1d-132">讓我們看看此 UDF 如何運作的範例。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="3dd1d-133">取得每個學生的姓氏與名字</span><span class="sxs-lookup"><span data-stu-id="3dd1d-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="3dd1d-134">以下是在主控台視窗中執行此查詢時的輸出。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-134">Here is the output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="3dd1d-136">get-json_object UDF 有幾項限制。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="3dd1d-137">因為查詢中的每個欄位都需要重新剖析查詢，所以它會影響效能。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="3dd1d-138">GET\_JSON_OBJECT() 會傳回陣列的字串表示法。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="3dd1d-139">若要將此陣列轉換成 Hive 陣列，您必須使用規則運算式來取代方括號 ‘[‘ 和 ‘]’，然後呼叫分割以取得陣列。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="3dd1d-140">這就是 Hive wiki 建議使用 json_tuple 的原因。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="3dd1d-141">使用 JSON_TUPLE UDF</span><span class="sxs-lookup"><span data-stu-id="3dd1d-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="3dd1d-142">Hive 所提供的另一個 UDF 稱為 [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple)，其效能比 [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) 更高。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="3dd1d-143">這個方法會採用一組索引鍵和 JSON 字串，並使用一個函式傳回值的 tuple。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="3dd1d-144">下列查詢會從 JSON 文件傳回學生識別碼以及年級：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="3dd1d-145">這個指令碼在 Hive 主控台的輸出：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-145">The output of this script in the Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="3dd1d-147">JSON\_TUPLE 會使用 Hive 中的[橫向檢視](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView)語法，可讓 json\_tuple 將 UDT 函式套用到原始資料表的每個資料列，以建立一個虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="3dd1d-148">複雜 JSON 會重複使用橫向檢視，因此變得難以使用。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="3dd1d-149">此外，JSON_TUPLE 無法處理巢狀 JSON。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="3dd1d-150">使用自訂 SerDe</span><span class="sxs-lookup"><span data-stu-id="3dd1d-150">Use custom SerDe</span></span>
<span data-ttu-id="3dd1d-151">SerDe 是用來剖析巢狀 JSON 文件的最佳選擇，它可讓您定義 JSON 結構描述，並使用該結構描述來剖析文件。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="3dd1d-152">在本教學課程中，您將使用其中一個已由 [rcongiu](https://github.com/rcongiu) 開發的熱門 SerDe。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="3dd1d-153">**使用自訂 SerDe：**</span><span class="sxs-lookup"><span data-stu-id="3dd1d-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="3dd1d-154">安裝 [Java SE 開發套件 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR)。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="3dd1d-155">如果您要使用 HDInsight 的 Windows 部署，請選擇 Windows x64 版本的 JDK。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="3dd1d-156">JDK 1.8 不適用於此 SerDe。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="3dd1d-157">安裝完成之後，請加入新的使用者環境變數：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="3dd1d-158">從 Windows 畫面開啟 [ **檢視進階系統設定** ]。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="3dd1d-159">按一下 [ **環境變數**]。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="3dd1d-160">加入新的 **JAVA_HOME** 環境變數，其指向 **C:\Program Files\Java\jdk1.7.0_55** 或任何安裝 JDK 的位置。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![為 JDK 設定正確的組態值][image-hdi-hivejson-jdk]
2. <span data-ttu-id="3dd1d-162">安裝 [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="3dd1d-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="3dd1d-163">在您的路徑中新增 bin 資料夾，方法是移至 [控制台] --> 針對您帳戶的環境變數 [編輯系統變數]。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="3dd1d-164">下列螢幕擷取畫面會顯示如何執行此動作。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-164">The following screenshot shows you how to do this.</span></span>
   
    ![設定 Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="3dd1d-166">從 [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github 網站複製專案。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="3dd1d-167">您按一下 [下載 Zip] 按鈕即可完成，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![複製專案][image-hdi-hivejson-serde]

<span data-ttu-id="3dd1d-169">4：移至您已將此套件下載至其中的資料夾，然後輸入 “mvn package”。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="3dd1d-170">這樣應該會建立您稍後會複製到叢集的必要 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="3dd1d-171">5：移至根資料夾 (您已將封裝下載至其中) 下的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="3dd1d-172">上傳 json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 檔案到叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="3dd1d-173">我通常會將它放在 hive 二進位資料夾底下：C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin 或類似位置。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="3dd1d-174">6：在 hive 提示字元中，輸入 “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="3dd1d-175">因為在我的案例中，jar 位於 C:\apps\dist\hive-0.13.x\bin 資料夾中，所以我可以直接以此名稱新增 jar，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![將 JAR 新增至您的專案][image-hdi-hivejson-addjar]

<span data-ttu-id="3dd1d-177">現在，您已準備好使用 SerDe 對 JSON 文件執行查詢。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="3dd1d-178">下列陳述式會利用已定義的結構描述來建立資料表：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-178">The following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="3dd1d-179">列出學生的姓氏與名字</span><span class="sxs-lookup"><span data-stu-id="3dd1d-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="3dd1d-180">以下是 Hive 主控台的結果。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-180">Here is the result from the Hive console.</span></span>

![SerDe 查詢 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="3dd1d-182">計算 JSON 文件的分數總和</span><span class="sxs-lookup"><span data-stu-id="3dd1d-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="3dd1d-183">上述查詢會使用[橫向檢視切割](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF 展開分數的陣列，讓它們可以進行加總。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="3dd1d-184">以下是 Hive 主控台的輸出。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-184">Here is the output from the Hive console.</span></span>

![SerDe 查詢 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="3dd1d-186">若要找出指定學生得分超過 80 分的科目：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="3dd1d-187">上述查詢傳回的 Hive 陣列與傳回字串的 get\_json\_object 不同。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![SerDe 查詢 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="3dd1d-189">如果您想要刪除格式不正確的 JSON，然後依照此 SerDe 之 [wiki 頁面](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) 的說明內容，您只要輸入下列程式碼即可：</span><span class="sxs-lookup"><span data-stu-id="3dd1d-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="3dd1d-190">摘要</span><span class="sxs-lookup"><span data-stu-id="3dd1d-190">Summary</span></span>
<span data-ttu-id="3dd1d-191">總而言之，您在 Hive 中選擇的 JSON 運算子類型取決於您的案例。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="3dd1d-192">如果您有一個簡單的 JSON 文件，且您只需要查閱一個欄位 – 您就可以選擇使用 Hive UDF get\_json\_object。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="3dd1d-193">如果您有多個金鑰需要查閱，可以使用 json_tuple。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="3dd1d-194">如果您有巢狀文件，您應該使用 JSON SerDe。</span><span class="sxs-lookup"><span data-stu-id="3dd1d-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dd1d-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3dd1d-195">Next steps</span></span>

<span data-ttu-id="3dd1d-196">如需其他相關文章，請參閱</span><span class="sxs-lookup"><span data-stu-id="3dd1d-196">For other related articles, see</span></span>

* [<span data-ttu-id="3dd1d-197">搭配 HDInsight 中的 Hadoop 使用 Hive 和 HiveQL 來分析範例 Apache Log4j 檔案</span><span class="sxs-lookup"><span data-stu-id="3dd1d-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3dd1d-198">在 HDInsight 中使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="3dd1d-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="3dd1d-199">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="3dd1d-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="3dd1d-200">使用 Azure Cosmos DB 和 HDInsight 執行 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="3dd1d-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
