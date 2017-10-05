---
title: "搭配 Apache Hive 和 Pig 的 Python UDF - Azure HDInsight | Microsoft Docs"
description: "了解如何在 HDInsight 中從 Hive 和 Pig (Azure 上的 Hadoop 技術堆疊) 使用 Python 使用者定義函數 (UDF)。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="e4799-103">在 HDInsight 上使用 Python 使用者定義函數 (UDF) 與 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="e4799-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="e4799-104">了解如何在 Azure HDInsight 的 Hadoop 中搭配使用 Python 使用者定義函式 (UDF) 與 Apache Hive 和 Pig。</span><span class="sxs-lookup"><span data-stu-id="e4799-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="e4799-105"><a name="python"></a>HDInsight 上的 Python</span><span class="sxs-lookup"><span data-stu-id="e4799-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="e4799-106">HDInsight 3.0 和更新版本上預設已安裝 Python2.7。</span><span class="sxs-lookup"><span data-stu-id="e4799-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="e4799-107">Apache Hive 可以與此版本的 Python 搭配使用，以進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="e4799-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="e4799-108">資料流處理會使用 STDOUT 和 STDIN，以在 Hive 和 UDF 之間傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="e4799-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="e4799-109">HDInsight 也包含 Jython (以 Java 撰寫的 Python 實作)。</span><span class="sxs-lookup"><span data-stu-id="e4799-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="e4799-110">Jython 直接在 Java 虛擬機器上執行，並不使用資料流。</span><span class="sxs-lookup"><span data-stu-id="e4799-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="e4799-111">搭配使用 Python 與 Pig 時，建議使用的 Python 解譯器為 Jython。</span><span class="sxs-lookup"><span data-stu-id="e4799-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="e4799-112">本文件中的這些步驟進行下列假設：</span><span class="sxs-lookup"><span data-stu-id="e4799-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="e4799-113">您在本機開發環境中建立 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="e4799-114">您從本機 Bash 工作階段使用 `scp` 命令，或者使用提供的 PowerShell 指令碼，將指令碼上傳至 HDInsight 。</span><span class="sxs-lookup"><span data-stu-id="e4799-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="e4799-115">如果您想要使用 [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) 預覽來利用 HDInsight，則必須：</span><span class="sxs-lookup"><span data-stu-id="e4799-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="e4799-116">建立 Cloud Shell 環境內的指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="e4799-117">使用 `scp` 將檔案從 Cloud Shell 上傳至 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="e4799-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="e4799-118">使用 `ssh` 從 Cloud Shell 命令連線至 HDInsight，並執行範例。</span><span class="sxs-lookup"><span data-stu-id="e4799-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="e4799-119"><a name="hivepython"></a>Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e4799-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="e4799-120">從 Hive 中，透過 HiveQL `TRANSFORM` 陳述式，可將 Python 當作 UDF 使用。</span><span class="sxs-lookup"><span data-stu-id="e4799-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="e4799-121">例如，下列 HiveQL 會叫用叢集的預設 Azure 儲存體帳戶所儲存的 `hiveudf.py` 檔案。</span><span class="sxs-lookup"><span data-stu-id="e4799-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="e4799-122">**以 Linux 為基礎的 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="e4799-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="e4799-123">**以 Windows 為基礎的 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="e4799-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="e4799-124">在以 Windows 為基礎的 HDInsight 叢集上，`USING` 子句必須指定 python.exe 的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="e4799-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="e4799-125">以下是此範例所執行的動作：</span><span class="sxs-lookup"><span data-stu-id="e4799-125">Here's what this example does:</span></span>

1. <span data-ttu-id="e4799-126">檔案開頭的 `add file` 陳述式將 `hiveudf.py` 檔案加入至分散式快取，供叢集中的所有節點存取。</span><span class="sxs-lookup"><span data-stu-id="e4799-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="e4799-127">使用 `SELECT TRANSFORM ... USING` 陳述式選取來自 `hivesampletable` 的資料。</span><span class="sxs-lookup"><span data-stu-id="e4799-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="e4799-128">它也會將 clientid、devicemake 和 devicemodel 值傳遞至 `hiveudf.py` 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="e4799-129">`AS` 子句描述從 `hiveudf.py` 中傳回的欄位。</span><span class="sxs-lookup"><span data-stu-id="e4799-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="e4799-130">建立 hiveudf.py 檔案</span><span class="sxs-lookup"><span data-stu-id="e4799-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="e4799-131">在開發環境中，建立名為 `hiveudf.py` 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="e4799-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="e4799-132">使用下列程式碼作為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="e4799-132">Use the following code as the contents of the file:</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="e4799-133">此指令碼會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e4799-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="e4799-134">從 STDIN 中讀取資料行。</span><span class="sxs-lookup"><span data-stu-id="e4799-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="e4799-135">使用 `string.strip(line, "\n ")` 移除結尾新行字元。</span><span class="sxs-lookup"><span data-stu-id="e4799-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="e4799-136">執行串流處理時，有一行包含所有的值，而每個值之間是一個定位字元。</span><span class="sxs-lookup"><span data-stu-id="e4799-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="e4799-137">因此， `string.split(line, "\t")` 可在每個索引標籤進行分割輸入，並只傳回欄位。</span><span class="sxs-lookup"><span data-stu-id="e4799-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="e4799-138">處理完成時，輸出必須以一行寫入 STDOUT，而每一個欄位之間是一個定位字元。</span><span class="sxs-lookup"><span data-stu-id="e4799-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="e4799-139">例如， `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`。</span><span class="sxs-lookup"><span data-stu-id="e4799-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="e4799-140">`while` 迴圈會一直重複直到沒有 `line` 讀取。</span><span class="sxs-lookup"><span data-stu-id="e4799-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="e4799-141">指令碼輸出是 `devicemake` 和 `devicemodel` 的輸入值串連，並且是串連值的雜湊。</span><span class="sxs-lookup"><span data-stu-id="e4799-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="e4799-142">請參閱 [執行範例](#running) ，以了解如何在 HDInsight 叢集上執行此範例。</span><span class="sxs-lookup"><span data-stu-id="e4799-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="e4799-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="e4799-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="e4799-144">從 Pig 中，透過 `GENERATE` 陳述式，可將 Python 指令碼當作 UDF 使用。</span><span class="sxs-lookup"><span data-stu-id="e4799-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="e4799-145">您可以使用 Jython 或 C Python 執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="e4799-146">Jython 是在 JVM 上執行，而且可以從 Pig 原生呼叫。</span><span class="sxs-lookup"><span data-stu-id="e4799-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="e4799-147">C Python 是外部處理序，因此 JVM 上的 Pig 所提供的資料會外送到 Python 處理序中執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="e4799-148">Python 指令碼的輸出會傳送回 Pig。</span><span class="sxs-lookup"><span data-stu-id="e4799-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="e4799-149">若要指定 Python 解譯器，請在參考 Python 指令碼時使用 `register`。</span><span class="sxs-lookup"><span data-stu-id="e4799-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="e4799-150">下列範例使用 Pig 將指令碼註冊為 `myfuncs`：</span><span class="sxs-lookup"><span data-stu-id="e4799-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="e4799-151">**若要使用 Jython**：`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e4799-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="e4799-152">**若要使用 C Python**：`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e4799-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4799-153">在使用 Jython 時，pig_jython 檔案的路徑可以是本機路徑或 WASB:// 路徑。</span><span class="sxs-lookup"><span data-stu-id="e4799-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="e4799-154">不過，在使用 C Python 時，您必須參考您用來提交 Pig 作業之節點的本機檔案系統上的檔案。</span><span class="sxs-lookup"><span data-stu-id="e4799-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="e4799-155">通過註冊之後，此範例針對兩者的 Pig Latin 是相同的︰</span><span class="sxs-lookup"><span data-stu-id="e4799-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="e4799-156">以下是此範例所執行的動作：</span><span class="sxs-lookup"><span data-stu-id="e4799-156">Here's what this example does:</span></span>

1. <span data-ttu-id="e4799-157">第一行將範例資料檔 `sample.log` 載入 `LOGS` 中。</span><span class="sxs-lookup"><span data-stu-id="e4799-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="e4799-158">它也會將每一筆記錄定義為 `chararray`。</span><span class="sxs-lookup"><span data-stu-id="e4799-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="e4799-159">下一行會濾除任何 null 值，然後將操作的結果儲存至 `LOG`。</span><span class="sxs-lookup"><span data-stu-id="e4799-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="e4799-160">接下來，逐一查看 `LOG` 中的記錄，並使用 `GENERATE` 叫用以 `myfuncs` 載入的 Python/Jython 指令碼所包含的 `create_structure` 方法。</span><span class="sxs-lookup"><span data-stu-id="e4799-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="e4799-161">`LINE` 用來將目前的記錄傳給函式。</span><span class="sxs-lookup"><span data-stu-id="e4799-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="e4799-162">最後，使用 `DUMP` 指令將輸出傾印至 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="e4799-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="e4799-163">這個命令會在作業完成之後顯示結果。</span><span class="sxs-lookup"><span data-stu-id="e4799-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="e4799-164">建立 pigudf.py 檔案</span><span class="sxs-lookup"><span data-stu-id="e4799-164">Create the pigudf.py file</span></span>

<span data-ttu-id="e4799-165">在開發環境中，建立名為 `pigudf.py` 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="e4799-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="e4799-166">使用下列程式碼作為此檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="e4799-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="e4799-167">在 Pig Latin 範例中，我們因為輸入沒有一致的結構描述而將 `LINE` 輸入定義為 chararray。</span><span class="sxs-lookup"><span data-stu-id="e4799-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="e4799-168">Python 指令碼會將資料轉換成一致的結構描述，以便輸出。</span><span class="sxs-lookup"><span data-stu-id="e4799-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="e4799-169">`@outputSchema` 陳述式定義將傳回給 Pig 的資料格式。</span><span class="sxs-lookup"><span data-stu-id="e4799-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="e4799-170">在此案例中，這是一個 **data bag**(一種 Pig 資料類型)。</span><span class="sxs-lookup"><span data-stu-id="e4799-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="e4799-171">Bag 包含下列欄位，全部都是 chararray (字串)：</span><span class="sxs-lookup"><span data-stu-id="e4799-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="e4799-172">date - 記錄項目的建立日期</span><span class="sxs-lookup"><span data-stu-id="e4799-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="e4799-173">time - 記錄項目的建立時間</span><span class="sxs-lookup"><span data-stu-id="e4799-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="e4799-174">classname - 建立項目所針對的類別名稱</span><span class="sxs-lookup"><span data-stu-id="e4799-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="e4799-175">level - 記錄層級</span><span class="sxs-lookup"><span data-stu-id="e4799-175">level - the log level</span></span>
   * <span data-ttu-id="e4799-176">detail - 記錄項目的詳細資料</span><span class="sxs-lookup"><span data-stu-id="e4799-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="e4799-177">接下來，`def create_structure(input)` 定義可供 Pig 傳遞行項目的函數。</span><span class="sxs-lookup"><span data-stu-id="e4799-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="e4799-178">範例資料 `sample.log` 大致上符合我們想要傳回的 date、time、classname、level 和 detail 結構描述。</span><span class="sxs-lookup"><span data-stu-id="e4799-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="e4799-179">不過，它包含開頭為 `*java.lang.Exception*` 的數行。</span><span class="sxs-lookup"><span data-stu-id="e4799-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="e4799-180">這幾行必須經過修改以符合結構描述。</span><span class="sxs-lookup"><span data-stu-id="e4799-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="e4799-181">`if` 陳述式會檢查這幾行，然後調整輸入資料將 `*java.lang.Exception*` 字串移至尾端，使資料符合我們預期的輸出結構描述。</span><span class="sxs-lookup"><span data-stu-id="e4799-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="e4799-182">接下來，使用 `split` 命令，在前四個空白字元處分割資料。</span><span class="sxs-lookup"><span data-stu-id="e4799-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="e4799-183">輸出即獲指派 `date`、`time`、 `classname`、 `level` 和 `detail` 。</span><span class="sxs-lookup"><span data-stu-id="e4799-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="e4799-184">最後，將值傳回給 Pig。</span><span class="sxs-lookup"><span data-stu-id="e4799-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="e4799-185">當資料傳回至 Pig 時，其將具有如同 `@outputSchema` 陳述式中定義的一致性結構描述。</span><span class="sxs-lookup"><span data-stu-id="e4799-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="e4799-186"><a name="running"></a>上傳及執行範例</span><span class="sxs-lookup"><span data-stu-id="e4799-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4799-187">**SSH** 步驟只適用於以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e4799-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e4799-188">**PowerShell** 步驟適用於以 Linux 或 Windows 為基礎的 HDInsight 叢集，但需要 Windows 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e4799-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="e4799-189">SSH</span><span class="sxs-lookup"><span data-stu-id="e4799-189">SSH</span></span>

<span data-ttu-id="e4799-190">如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e4799-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="e4799-191">使用 `scp` 將檔案複製到您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e4799-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="e4799-192">例如，下列命令會將檔案複製到名為 **mycluster**的叢集。</span><span class="sxs-lookup"><span data-stu-id="e4799-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="e4799-193">使用 SSH 連接到叢集。</span><span class="sxs-lookup"><span data-stu-id="e4799-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="e4799-194">從 SSH 工作階段，將先前上傳的 python 檔案加入叢集的 WASB 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e4799-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="e4799-195">上傳檔案之後，請使用下列步驟執行 Hive 和 Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="e4799-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="e4799-196">使用 Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e4799-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="e4799-197">使用 `hive` 命令啟動 Hive Shell。</span><span class="sxs-lookup"><span data-stu-id="e4799-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="e4799-198">在 Shell 載入完成時，您應會看到 `hive>` 提示。</span><span class="sxs-lookup"><span data-stu-id="e4799-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="e4799-199">在 `hive>` 提示上輸入下列查詢：</span><span class="sxs-lookup"><span data-stu-id="e4799-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="e4799-200">輸入最後一行後，工作應該就會開始。</span><span class="sxs-lookup"><span data-stu-id="e4799-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="e4799-201">作業完成之後，它會傳回與下列範例類似的輸出：</span><span class="sxs-lookup"><span data-stu-id="e4799-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="e4799-202">使用 Pig UDF</span><span class="sxs-lookup"><span data-stu-id="e4799-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="e4799-203">使用 `pig` 命令啟動 Shell。</span><span class="sxs-lookup"><span data-stu-id="e4799-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="e4799-204">在 Shell 載入完成時，您會看到 `grunt>` 提示。</span><span class="sxs-lookup"><span data-stu-id="e4799-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="e4799-205">在出現 `grunt>` 提示時輸入下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="e4799-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="e4799-206">輸入下列行之後，應該就會開始作業。</span><span class="sxs-lookup"><span data-stu-id="e4799-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="e4799-207">作業完成之後，它會傳回與下列資料類似的輸出：</span><span class="sxs-lookup"><span data-stu-id="e4799-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="e4799-208">使用 `quit` 結束 Grunt shell，然後使用下列命令編輯本機檔案系統上的 pigudf.py 檔案：</span><span class="sxs-lookup"><span data-stu-id="e4799-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="e4799-209">進入編輯器後，移除行首的 `#` 字元將以下這行取消註解：</span><span class="sxs-lookup"><span data-stu-id="e4799-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="e4799-210">完成變更後，使用 Ctrl + X 結束編輯器。</span><span class="sxs-lookup"><span data-stu-id="e4799-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="e4799-211">選取 [Y]，然後按 Enter 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e4799-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="e4799-212">使用 `pig` 命令再次啟動 Shell。</span><span class="sxs-lookup"><span data-stu-id="e4799-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="e4799-213">進入 `grunt>` 提示字元後，使用下列命令以使用 C Python 解譯器執行 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e4799-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="e4799-214">此作業完成後，您應該會看到和先前使用 Jython 執行指令碼時所得到的相同輸出。</span><span class="sxs-lookup"><span data-stu-id="e4799-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="e4799-215">PowerShell：上傳檔案</span><span class="sxs-lookup"><span data-stu-id="e4799-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="e4799-216">您可以使用 PowerShell 將檔案上傳至 HDInsight 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e4799-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="e4799-217">使用下列指令碼來上傳 Python 檔案：</span><span class="sxs-lookup"><span data-stu-id="e4799-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e4799-218">本節中的步驟是使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e4799-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="e4799-219">如需使用 Azure PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e4799-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> <span data-ttu-id="e4799-220">將 `C:\path\to` 值變更為您開發環境上檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="e4799-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="e4799-221">此指令碼會擷取 HDInsight 叢集的資訊，然後擷取預設儲存體帳戶的帳戶和金鑰，再將檔案上傳至容器的根目錄。</span><span class="sxs-lookup"><span data-stu-id="e4799-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="e4799-222">如需上傳檔案的詳細資訊，請參閱[在 HDInsight 中上傳 Hadoop 作業的資料](hdinsight-upload-data.md)文件。</span><span class="sxs-lookup"><span data-stu-id="e4799-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="e4799-223">PowerShell：使用 Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e4799-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="e4799-224">PowerShell 也可用來從遠端執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e4799-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="e4799-225">使用下列 PowerShell 指令碼，執行使用 **hiveudf.py** 指令碼的 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="e4799-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4799-226">執行前，指令碼會提示您輸入您 HDInsight 叢集的 HTTPs/系統管理帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="e4799-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="e4799-227">**Hive** 作業的輸出應該如下範例所示：</span><span class="sxs-lookup"><span data-stu-id="e4799-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="e4799-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="e4799-228">Pig (Jython)</span></span>

<span data-ttu-id="e4799-229">PowerShell 也可用來執行 Pig Latin 作業。</span><span class="sxs-lookup"><span data-stu-id="e4799-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="e4799-230">若要執行使用 **pigudf.py** 指令碼的 Pig Latin 作業，請使用下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="e4799-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="e4799-231">使用 PowerShell 遠端提交作業時，無法使用 C Python 做為解譯器。</span><span class="sxs-lookup"><span data-stu-id="e4799-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="e4799-232">**Pig** 作業的輸出應該如下列資料所示：</span><span class="sxs-lookup"><span data-stu-id="e4799-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="e4799-233"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="e4799-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="e4799-234">執行工作時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="e4799-234">Errors when running jobs</span></span>

<span data-ttu-id="e4799-235">執行 Hive 作業時，您可能會遇到類似以下文字的錯誤：</span><span class="sxs-lookup"><span data-stu-id="e4799-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="e4799-236">這個問題可能是由 Python 檔案中的行尾結束符號所引起。</span><span class="sxs-lookup"><span data-stu-id="e4799-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="e4799-237">許多 Windows 編輯器預設都是使用 CRLF 做為行尾結束符號，但是 Linux 應用程式通常預期使用 LF。</span><span class="sxs-lookup"><span data-stu-id="e4799-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="e4799-238">若要在檔案上傳至 HDInsight 之前移除 CR 字元，您可以使用下列 PowerShell 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="e4799-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="e4799-239">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="e4799-239">PowerShell scripts</span></span>

<span data-ttu-id="e4799-240">用來執行範例的兩個範例 PowerShell 指令碼都包含一行註解，此行會顯示作業的錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="e4799-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="e4799-241">如果您沒有看到預期的工作輸出，請將下列這一行取消註解，再查看錯誤資訊是否指出問題。</span><span class="sxs-lookup"><span data-stu-id="e4799-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e4799-242">錯誤資訊 (STDERR) 和作業 (STDOUT) 的結果也會記錄至您的 HDInsight 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="e4799-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="e4799-243">關於此工作...</span><span class="sxs-lookup"><span data-stu-id="e4799-243">For this job...</span></span> | <span data-ttu-id="e4799-244">請在 Blob 容器中查看這些檔案</span><span class="sxs-lookup"><span data-stu-id="e4799-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="e4799-245">Hive</span><span class="sxs-lookup"><span data-stu-id="e4799-245">Hive</span></span> |<span data-ttu-id="e4799-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="e4799-246">/HivePython/stderr</span></span><p><span data-ttu-id="e4799-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="e4799-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="e4799-248">Pig</span><span class="sxs-lookup"><span data-stu-id="e4799-248">Pig</span></span> |<span data-ttu-id="e4799-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="e4799-249">/PigPython/stderr</span></span><p><span data-ttu-id="e4799-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="e4799-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="e4799-251"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="e4799-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="e4799-252">如果您需要載入非預設提供的 Python 模組，請參閱 [如何將模組部署至 Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx) (英文)。</span><span class="sxs-lookup"><span data-stu-id="e4799-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="e4799-253">若要了解使用 MapReduce，及Pig、Hive 的其他使用方式，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="e4799-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="e4799-254">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="e4799-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e4799-255">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="e4799-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e4799-256">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="e4799-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
