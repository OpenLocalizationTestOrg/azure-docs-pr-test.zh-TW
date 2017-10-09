---
title: "使用 Apache Hive 和 Pig-Azure HDInsight UDF aaaPython |Microsoft 文件"
description: "了解如何 toouse Python 使用者定義函數 (UDF) 從 Hive 和 Pig 在 HDInsight Hadoop 技術 hello 堆疊在 Azure 上。"
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
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="b5fb6-103">在 HDInsight 上使用 Python 使用者定義函數 (UDF) 與 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="b5fb6-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="b5fb6-104">了解如何 toouse Python 使用者定義函數 (UDF) 與 Apache Hive 和 Pig Azure HDInsight 上的 Hadoop 中。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="b5fb6-105"><a name="python"></a>HDInsight 上的 Python</span><span class="sxs-lookup"><span data-stu-id="b5fb6-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="b5fb6-106">HDInsight 3.0 和更新版本上預設已安裝 Python2.7。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="b5fb6-107">Apache Hive 可以與此版本的 Python 搭配使用，以進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="b5fb6-108">資料流處理會使用 Hive 和 hello UDF 之間 STDOUT 和 STDIN toopass 資料。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="b5fb6-109">HDInsight 也包含 Jython (以 Java 撰寫的 Python 實作)。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="b5fb6-110">Jython 直接在 hello Java 虛擬機器上執行，並不使用資料流。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="b5fb6-111">Jython 是 hello Pig 搭配使用 Python 時建議使用 Python 解譯器。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="b5fb6-112">本文件中的 hello 步驟進行下列假設 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="b5fb6-113">您建立 hello Python 指令碼的本機開發環境上。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="b5fb6-114">您上傳使用任一 hello hello 指令碼 tooHDInsight`scp`從本機 Bash 工作階段或 hello 提供 PowerShell 指令碼命令。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="b5fb6-115">如果您想 toouse hello [Azure 雲端殼層 (bash)](https://docs.microsoft.com/azure/cloud-shell/overview)預覽 toowork 與 HDInsight，則必須：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="b5fb6-116">建立 hello hello 雲端殼層環境內的指令碼。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="b5fb6-117">使用`scp`tooupload hello 檔案從 hello 雲端殼層 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="b5fb6-118">使用`ssh`從 hello 雲端殼層 tooconnect tooHDInsight 和執行的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="b5fb6-119"><a name="hivepython"></a>Hive UDF</span><span class="sxs-lookup"><span data-stu-id="b5fb6-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="b5fb6-120">Python 可用來當作 UDF 從 Hive 透過 hello HiveQL`TRANSFORM`陳述式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="b5fb6-121">例如，下列 HiveQL hello 叫用 hello `hiveudf.py` hello hello 叢集的預設 Azure 儲存體帳戶中儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="b5fb6-122">**以 Linux 為基礎的 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="b5fb6-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="b5fb6-123">**以 Windows 為基礎的 HDInsight**</span><span class="sxs-lookup"><span data-stu-id="b5fb6-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="b5fb6-124">在 Windows 為基礎的 HDInsight 叢集上 hello`USING`子句必須指定 hello 完整路徑 toopython.exe。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="b5fb6-125">以下是此範例所執行的動作：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-125">Here's what this example does:</span></span>

1. <span data-ttu-id="b5fb6-126">hello `add file` hello 檔案的 hello 開頭的陳述式會將 hello`hiveudf.py`檔案 toohello 分散式快取，，所以 hello 叢集中所有節點存取。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="b5fb6-127">hello`SELECT TRANSFORM ... USING`陳述式從 hello 選取資料`hivesampletable`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="b5fb6-128">它也會傳遞 hello clientid、 devicemake 和 devicemodel 值 toohello`hiveudf.py`指令碼。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="b5fb6-129">hello`AS`子句描述從傳回的 hello 欄位`hiveudf.py`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="b5fb6-130">建立 hello hiveudf.py 檔案</span><span class="sxs-lookup"><span data-stu-id="b5fb6-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="b5fb6-131">在開發環境中，建立名為 `hiveudf.py` 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="b5fb6-132">使用下列程式碼為 hello hello 檔案內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="b5fb6-133">此指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="b5fb6-134">從 STDIN 中讀取資料行。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="b5fb6-135">使用移除尾端新行字元的 hello `string.strip(line, "\n ")`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="b5fb6-136">當進行資料流處理時，單行包含定位字元，每個值之間的所有 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="b5fb6-137">因此`string.split(line, "\t")`可以是使用的 toosplit hello 輸入每個索引標籤，傳回只 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="b5fb6-138">處理序完成時，hello 輸出必須寫 tooSTDOUT 成單一行中的每個欄位的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="b5fb6-139">例如： `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="b5fb6-140">hello`while`迴圈會重複，直到沒有`line`讀取。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="b5fb6-141">hello 指令碼輸出是 hello 的輸入值的串連`devicemake`和`devicemodel`，和雜湊 hello 的串連值。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="b5fb6-142">請參閱[執行 hello 範例](#running)如何 toorun HDInsight 叢集上的這個範例。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="b5fb6-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="b5fb6-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="b5fb6-144">Python 指令碼可用來當做從 Pig UDF 透過 hello`GENERATE`陳述式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="b5fb6-145">您可以執行使用 Jython 或 C Python hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="b5fb6-146">Jython hello JVM 上, 執行，並且從 Pig 可原生。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="b5fb6-147">C Python 是外部處理序，以便將資料從 Pig hello 上 hello JVM 送出 toohello Python 處理序中執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="b5fb6-148">hello 的 hello Python 指令碼的輸出會傳送回 Pig。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="b5fb6-149">toospecify hello Python 解釋器，使用`register`參考 hello Python 指令碼時。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="b5fb6-150">hello 下列範例指令碼使用註冊為 Pig `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="b5fb6-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="b5fb6-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="b5fb6-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="b5fb6-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5fb6-153">當使用 Jython，hello 路徑 toohello pig_jython 檔案可以是本機路徑或 WASB: / / 路徑。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="b5fb6-154">不過，使用 C Python，您必須參考 hello 節點使用 toosubmit hello Pig 工作 hello 本機檔案系統上的檔案。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="b5fb6-155">一旦註冊，超過此範例中的 hello Pig 拉丁 hello 相同兩個：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="b5fb6-156">以下是此範例所執行的動作：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-156">Here's what this example does:</span></span>

1. <span data-ttu-id="b5fb6-157">hello 第一行會載入 hello 範例資料檔`sample.log`到`LOGS`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="b5fb6-158">它也會將每一筆記錄定義為 `chararray`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="b5fb6-159">hello 下一行會篩選出 null 值，儲存的 hello 作業插入的 hello 結果`LOG`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="b5fb6-160">接下來，它會逐一中的 hello 記錄`LOG`並用`GENERATE`tooinvoke hello `create_structure` hello Python/Jython 指令碼中所包含的方法以載入`myfuncs`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="b5fb6-161">`LINE`是使用的 toopass hello 目前記錄 toohello 函式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="b5fb6-162">最後，hello 輸出都是使用 hello 傾印的 tooSTDOUT`DUMP`命令。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="b5fb6-163">Hello 作業完成之後，此命令會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="b5fb6-164">建立 hello pigudf.py 檔案</span><span class="sxs-lookup"><span data-stu-id="b5fb6-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="b5fb6-165">在開發環境中，建立名為 `pigudf.py` 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="b5fb6-166">使用下列程式碼為 hello hello 檔案內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-166">Use hello following code as hello contents of hello file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="b5fb6-167">在 hello Pig 拉丁範例中，我們定義 hello `LINE` chararray 為輸入，因為沒有 hello 輸入沒有一致的結構描述。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="b5fb6-168">hello Python 指令碼會將 hello 資料轉換成一致的結構描述的輸出。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="b5fb6-169">hello`@outputSchema`陳述式定義 hello 傳回 tooPig hello 資料格式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="b5fb6-170">在此案例中，這是一個 **data bag**(一種 Pig 資料類型)。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="b5fb6-171">hello 包包含下列的欄位，都是 chararray （字串） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="b5fb6-172">日期-hello 日期 hello 記錄項目已建立</span><span class="sxs-lookup"><span data-stu-id="b5fb6-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="b5fb6-173">時間-hello hello 記錄項目建立的時間</span><span class="sxs-lookup"><span data-stu-id="b5fb6-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="b5fb6-174">類別名稱-已建立 hello 類別名稱 hello 項目</span><span class="sxs-lookup"><span data-stu-id="b5fb6-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="b5fb6-175">層級-hello 記錄層級</span><span class="sxs-lookup"><span data-stu-id="b5fb6-175">level - hello log level</span></span>
   * <span data-ttu-id="b5fb6-176">詳細資料： hello 的詳細資訊詳細資料記錄項目</span><span class="sxs-lookup"><span data-stu-id="b5fb6-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="b5fb6-177">接下來，hello`def create_structure(input)`定義 Pig 會傳遞至明細項目的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="b5fb6-178">hello 範例資料， `sample.log`、 大部分符合 toohello 日期、 時間、 classname，層級，而且我們想 tooreturn 結構描述的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="b5fb6-179">不過，它包含開頭為 `*java.lang.Exception*` 的數行。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="b5fb6-180">這些行數必須是已修改的 toomatch hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="b5fb6-181">hello`if`陳述式會檢查，然後 massages hello 輸入的資料 toomove hello`*java.lang.Exception*`字串 toohello 結束時，將 hello 資料內嵌我們預期的輸出結構描述。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="b5fb6-182">接下來，hello`split`命令是使用的 toosplit hello hello 前四個空格字元的資料。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="b5fb6-183">hello 輸出會指派到`date`， `time`， `classname`， `level`，和`detail`。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="b5fb6-184">最後，會傳回 hello 值 tooPig。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="b5fb6-185">Hello 資料傳回時 tooPig，它有一致的結構描述定義在 hello`@outputSchema`陳述式。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="b5fb6-186"><a name="running"></a>上傳及執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="b5fb6-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5fb6-187">hello **SSH**步驟只適用於以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b5fb6-188">hello **PowerShell**使用 Linux 或 Windows 為基礎的 HDInsight 叢集的步驟，但需要 Windows 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="b5fb6-189">SSH</span><span class="sxs-lookup"><span data-stu-id="b5fb6-189">SSH</span></span>

<span data-ttu-id="b5fb6-190">如需使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="b5fb6-191">使用`scp`toocopy hello 檔案 tooyour HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="b5fb6-192">比方說，下列命令複製 hello 名為的檔案 tooa 叢集來 hello **mycluster**。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="b5fb6-193">使用 SSH tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="b5fb6-194">Hello SSH 工作階段中，加入 hello python 上傳檔案之前 hello 叢集 toohello WASB 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="b5fb6-195">上傳 hello 檔案之後, 使用 hello 下列步驟會 toorun hello Hive 和 Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="b5fb6-196">使用 Hive UDF hello</span><span class="sxs-lookup"><span data-stu-id="b5fb6-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="b5fb6-197">使用 hello`hive`命令 toostart hello hive 殼層。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="b5fb6-198">您應該會看到`hive>`當載入 hello 殼層提示。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="b5fb6-199">輸入下列查詢在 hello hello`hive>`提示：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="b5fb6-200">輸入 hello 最後一行之後, 應該啟動 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="b5fb6-201">一旦 hello 作業完成時，它會傳回下列範例的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="b5fb6-202">使用 Pig UDF hello</span><span class="sxs-lookup"><span data-stu-id="b5fb6-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="b5fb6-203">使用 hello`pig`命令 toostart hello 殼層。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="b5fb6-204">您會看到`grunt>`當載入 hello 殼層提示。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="b5fb6-205">輸入下列陳述式在 hello hello`grunt>`提示：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="b5fb6-206">在輸入後 hello 行下，應該啟動 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="b5fb6-207">一旦 hello 作業完成時，它會傳回下列資料的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="b5fb6-208">使用`quit`tooexit hello Grunt 殼層，然後再使用下列 tooedit hello pigudf.py 檔 hello 本機檔案系統上的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="b5fb6-209">一次在 hello 編輯器中，請取消註解 hello 行下藉由移除 hello `#` hello 一行的 hello 開頭的字元：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="b5fb6-210">一旦 hello 已變更，使用 Ctrl + X tooexit hello 編輯器。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="b5fb6-211">選取 Y、，然後輸入 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="b5fb6-212">使用 hello`pig`命令 toostart hello 殼層一次。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="b5fb6-213">一旦您是在 hello`grunt>`提示，請使用下列 toorun hello Python 指令碼使用 hello C Python 解譯器的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="b5fb6-214">這項作業完成之後，您應該看到的 hello 相同的輸出做為您先前執行使用 Jython hello 指令碼時。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="b5fb6-215">PowerShell： 上傳 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="b5fb6-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="b5fb6-216">您可以使用 PowerShell tooupload hello 檔案 toohello HDInsight 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="b5fb6-217">使用下列指令碼 tooupload hello Python 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b5fb6-218">本節中的 hello 步驟使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="b5fb6-219">如需有關使用 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
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
> <span data-ttu-id="b5fb6-220">變更 hello `C:\path\to` toohello 路徑 toohello 檔案，在開發環境上的值。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="b5fb6-221">此指令碼會擷取您的 HDInsight 叢集的資訊，然後擷取 hello 帳戶和金鑰 hello 預設儲存體帳戶，並上傳 hello hello 容器的檔案 toohello 根。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="b5fb6-222">如需有關上傳檔案的詳細資訊，請參閱 hello [HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="b5fb6-223">PowerShell： 使用 hello Hive UDF</span><span class="sxs-lookup"><span data-stu-id="b5fb6-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="b5fb6-224">PowerShell 也可以使用的 tooremotely 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="b5fb6-225">使用下列 PowerShell 指令碼 toorun 使用 Hive 查詢的 hello **hiveudf.py**指令碼：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5fb6-226">再執行，hello 指令碼會提示您輸入 hello HTTPs/管理您的 HDInsight 叢集的帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
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
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="b5fb6-227">hello 輸出 hello **Hive**作業應該會出現類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="b5fb6-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="b5fb6-228">Pig (Jython)</span></span>

<span data-ttu-id="b5fb6-229">PowerShell 也可以使用的 toorun Pig 拉丁作業。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="b5fb6-230">toorun Pig 拉丁作業使用 hello **pigudf.py**編寫指令碼，請使用下列 PowerShell 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="b5fb6-231">當從遠端提交工作，使用 PowerShell，它是不可能 toouse C Python hello 直譯器。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

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

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="b5fb6-232">hello 輸出 hello **Pig**作業應該會出現類似 toohello 下列資料：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="b5fb6-233"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="b5fb6-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="b5fb6-234">執行工作時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="b5fb6-234">Errors when running jobs</span></span>

<span data-ttu-id="b5fb6-235">當執行 hello hive 工作，您可能會遇到錯誤類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="b5fb6-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="b5fb6-236">這個問題可能被因 hello hello Python 檔案中的行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="b5fb6-237">許多 Windows 編輯器預設 toousing CRLF 為 hello 行尾結束符號，但 Linux 應用程式通常會預期 LF。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="b5fb6-238">您可以使用下列 PowerShell 陳述式 tooremove hello CR 字元之前上傳 hello 檔案 tooHDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="b5fb6-239">PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="b5fb6-239">PowerShell scripts</span></span>

<span data-ttu-id="b5fb6-240">這兩個 hello 範例使用 toorun hello 範例 PowerShell 指令碼包含加上註解的線條顯示 hello 之工作的錯誤輸出。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="b5fb6-241">如果您沒有看到預期的 hello hello 之工作的輸出，請取消註解 hello 下列行，並查看 hello 錯誤資訊如果表示有問題。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="b5fb6-242">hello 長期資訊時發生錯誤 (STDERR) 與 hello 工作 (STDOUT) hello 結果也是記錄的 tooyour HDInsight 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="b5fb6-243">關於此工作...</span><span class="sxs-lookup"><span data-stu-id="b5fb6-243">For this job...</span></span> | <span data-ttu-id="b5fb6-244">查看這些 hello blob 容器中的檔案</span><span class="sxs-lookup"><span data-stu-id="b5fb6-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="b5fb6-245">Hive</span><span class="sxs-lookup"><span data-stu-id="b5fb6-245">Hive</span></span> |<span data-ttu-id="b5fb6-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="b5fb6-246">/HivePython/stderr</span></span><p><span data-ttu-id="b5fb6-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="b5fb6-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="b5fb6-248">Pig</span><span class="sxs-lookup"><span data-stu-id="b5fb6-248">Pig</span></span> |<span data-ttu-id="b5fb6-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="b5fb6-249">/PigPython/stderr</span></span><p><span data-ttu-id="b5fb6-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="b5fb6-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="b5fb6-251"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="b5fb6-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="b5fb6-252">如果您需要預設未提供的 tooload Python 模組，請參閱[如何 toodeploy 模組 tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5fb6-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="b5fb6-253">其他的方式 toouse Pig、 Hive 和有關使用 MapReduce toolearn，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5fb6-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="b5fb6-254">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="b5fb6-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b5fb6-255">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="b5fb6-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b5fb6-256">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="b5fb6-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
