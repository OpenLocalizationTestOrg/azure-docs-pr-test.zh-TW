---
title: "aaaApache Storm 寫入 tooStorage 資料湖存放區-Azure HDInsight |Microsoft 文件"
description: "了解 toouse hdinsight hello Apache Storm toowrite toohello HDFS 相容存放裝置的方式。 Azure 儲存體或 Azure Data Lake Store 的 HDInsight 提供 hello HDFS comptabile 儲存體。 此文件和 hello 相關聯的範例，示範如何 hello HdfsBolt 元件可使用的 toowrite toohello 預設儲存體的 HDInsight 叢集上出現。"
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="1b701-105">撰寫從 Apache Storm 的 tooHDFS HDInsight 上</span><span class="sxs-lookup"><span data-stu-id="1b701-105">Write tooHDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="1b701-106">了解 toouse Storm toowrite 資料 toohello HDFS 相容儲存體使用 Apache Storm HDInsight 上的方式。</span><span class="sxs-lookup"><span data-stu-id="1b701-106">Learn how toouse Storm toowrite data toohello HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="1b701-107">HDInsight 可以同時使用 Azure 儲存體以及 Azure Data Lake Store 作為 HDFS 相容儲存體。</span><span class="sxs-lookup"><span data-stu-id="1b701-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="1b701-108">提供 storm [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html)寫入資料 tooHDFS 的元件。</span><span class="sxs-lookup"><span data-stu-id="1b701-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data tooHDFS.</span></span> <span data-ttu-id="1b701-109">本文件提供從 hello HdfsBolt 撰寫 tooeither 類型的儲存體的資訊。</span><span class="sxs-lookup"><span data-stu-id="1b701-109">This document provides information on writing tooeither type of storage from hello HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1b701-110">本文件中使用的拓樸 hello 範例依賴隨附於 Storm HDInsight 上的元件。</span><span class="sxs-lookup"><span data-stu-id="1b701-110">hello example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="1b701-111">它可能需要修改 toowork 與 Azure 資料湖存放區時使用與其他 Apache Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b701-111">It may require modification toowork with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="1b701-112">取得 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="1b701-112">Get hello code</span></span>

<span data-ttu-id="1b701-113">包含此拓撲中的 hello 專案是從下載[https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)。</span><span class="sxs-lookup"><span data-stu-id="1b701-113">hello project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="1b701-114">toocompile 此專案中，您需要下列組態的開發環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-114">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="1b701-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1b701-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="1b701-116">HDInsight 3.5 或更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="1b701-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="1b701-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="1b701-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="1b701-118">hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。</span><span class="sxs-lookup"><span data-stu-id="1b701-118">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="1b701-119">不過，您應該檢查其存在且包含您系統的 hello 正確值。</span><span class="sxs-lookup"><span data-stu-id="1b701-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="1b701-120">`JAVA_HOME`-應該指向 toohello hello JDK 安裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b701-120">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="1b701-121">`PATH`-應包含下列路徑的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-121">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="1b701-122">`JAVA_HOME`（或 hello 等路徑）。</span><span class="sxs-lookup"><span data-stu-id="1b701-122">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="1b701-123">`JAVA_HOME\bin`（或 hello 等路徑）。</span><span class="sxs-lookup"><span data-stu-id="1b701-123">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="1b701-124">hello Maven 安裝所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b701-124">hello directory where Maven is installed.</span></span>

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a><span data-ttu-id="1b701-125">如何 toouse hello 與 HDInsight HdfsBolt</span><span class="sxs-lookup"><span data-stu-id="1b701-125">How toouse hello HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b701-126">在使用之前 hello HdfsBolt Storm HDInsight 上使用，您必須先使用指令碼動作所需的 toocopy jar 檔案到 hello `extpath` Storm 的。</span><span class="sxs-lookup"><span data-stu-id="1b701-126">Before using hello HdfsBolt with Storm on HDInsight, you must first use a script action toocopy required jar files into hello `extpath` for Storm.</span></span> <span data-ttu-id="1b701-127">如需詳細資訊，請參閱 hello[設定 hello 叢集](#configure)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1b701-127">For more information, see hello [Configure hello cluster](#configure) section.</span></span>

<span data-ttu-id="1b701-128">hello HdfsBolt 使用 hello 檔案配置如何提供 toounderstand toowrite tooHDFS。</span><span class="sxs-lookup"><span data-stu-id="1b701-128">hello HdfsBolt uses hello file scheme that you provide toounderstand how toowrite tooHDFS.</span></span> <span data-ttu-id="1b701-129">與 HDInsight，使用其中一種 hello 下列配置：</span><span class="sxs-lookup"><span data-stu-id="1b701-129">With HDInsight, use one of hello following schemes:</span></span>

* <span data-ttu-id="1b701-130">`wasb://`：搭配使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b701-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="1b701-131">`adl://`：搭配使用 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="1b701-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="1b701-132">hello 下表提供不同的情況下使用 hello 檔案配置的範例：</span><span class="sxs-lookup"><span data-stu-id="1b701-132">hello following table provides examples of using hello file scheme for different scenarios:</span></span>

| <span data-ttu-id="1b701-133">配置</span><span class="sxs-lookup"><span data-stu-id="1b701-133">Scheme</span></span> | <span data-ttu-id="1b701-134">注意事項</span><span class="sxs-lookup"><span data-stu-id="1b701-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="1b701-135">hello 預設儲存體帳戶是 Azure 儲存體帳戶中的 blob 容器</span><span class="sxs-lookup"><span data-stu-id="1b701-135">hello default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="1b701-136">hello 預設儲存體帳戶是 Azure 資料湖存放區中的目錄。</span><span class="sxs-lookup"><span data-stu-id="1b701-136">hello default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="1b701-137">叢集建立期間，您可以指定 hello 目錄是 hello 叢集的 HDFS hello 根的資料湖存放區中。</span><span class="sxs-lookup"><span data-stu-id="1b701-137">During cluster creation, you specify hello directory in Data Lake Store that is hello root of hello cluster's HDFS.</span></span> <span data-ttu-id="1b701-138">例如，hello`/clusters/myclustername/`目錄。</span><span class="sxs-lookup"><span data-stu-id="1b701-138">For example, hello `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="1b701-139">Hello 叢集相關聯的非預設 （其他） 的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b701-139">A non-default (additional) Azure storage account associated with hello cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="1b701-140">hello 的 hello hello 叢集所使用的資料湖存放區的根目錄。</span><span class="sxs-lookup"><span data-stu-id="1b701-140">hello root of hello Data Lake Store used by hello cluster.</span></span> <span data-ttu-id="1b701-141">這種配置允許 tooaccess 資料位於包含 hello 叢集檔案系統的 hello 目錄外。</span><span class="sxs-lookup"><span data-stu-id="1b701-141">This scheme allows you tooaccess data that is located outside hello directory that contains hello cluster file system.</span></span> |

<span data-ttu-id="1b701-142">如需詳細資訊，請參閱 hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org 上的參考。</span><span class="sxs-lookup"><span data-stu-id="1b701-142">For more information, see hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="1b701-143">設定範例</span><span class="sxs-lookup"><span data-stu-id="1b701-143">Example configuration</span></span>

<span data-ttu-id="1b701-144">hello 下列 YAML 是摘錄自 hello `resources/writetohdfs.yaml` hello 範例中包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b701-144">hello following YAML is an excerpt from hello `resources/writetohdfs.yaml` file included in hello example.</span></span> <span data-ttu-id="1b701-145">此檔案會定義使用 hello hello Storm 拓撲[變動](https://storm.apache.org/releases/1.1.0/flux.html)Apache Storm 的架構。</span><span class="sxs-lookup"><span data-stu-id="1b701-145">This file defines hello Storm topology using hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

<span data-ttu-id="1b701-146">此 YAML 會定義下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-146">This YAML defines hello following items:</span></span>

* <span data-ttu-id="1b701-147">`syncPolicy`： 定義檔案時同步/排清 toohello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="1b701-147">`syncPolicy`: Defines when files are synched/flushed toohello file system.</span></span> <span data-ttu-id="1b701-148">在此範例中，為每 1000 個 Tuple。</span><span class="sxs-lookup"><span data-stu-id="1b701-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="1b701-149">`fileNameFormat`： 定義 hello 路徑和檔案名稱模式 toouse 時寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="1b701-149">`fileNameFormat`: Defines hello path and file name pattern toouse when writing files.</span></span> <span data-ttu-id="1b701-150">在此範例中，在執行階段使用篩選器，提供 hello 路徑和 hello 副檔名是`.txt`。</span><span class="sxs-lookup"><span data-stu-id="1b701-150">In this example, hello path is provided at runtime using a filter, and hello file extension is `.txt`.</span></span>
* <span data-ttu-id="1b701-151">`recordFormat`： 定義 hello hello 寫入的檔案的內部格式。</span><span class="sxs-lookup"><span data-stu-id="1b701-151">`recordFormat`: Defines hello internal format of hello files written.</span></span> <span data-ttu-id="1b701-152">此範例中，欄位會分隔 hello`|`字元。</span><span class="sxs-lookup"><span data-stu-id="1b701-152">In this example, fields are delimited by hello `|` character.</span></span>
* <span data-ttu-id="1b701-153">`rotationPolicy`： 定義當 toorotate 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b701-153">`rotationPolicy`: Defines when toorotate files.</span></span> <span data-ttu-id="1b701-154">在此範例中，不會執行輪替。</span><span class="sxs-lookup"><span data-stu-id="1b701-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="1b701-155">`hdfs-bolt`： 使用 hello 做為 hello 的組態參數的舊版元件`HdfsBolt`類別。</span><span class="sxs-lookup"><span data-stu-id="1b701-155">`hdfs-bolt`: Uses hello previous components as configuration parameters for hello `HdfsBolt` class.</span></span>

<span data-ttu-id="1b701-156">如需有關 hello 變動架構的詳細資訊，請參閱[https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。</span><span class="sxs-lookup"><span data-stu-id="1b701-156">For more information on hello Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-hello-cluster"></a><span data-ttu-id="1b701-157">Hello 叢集設定</span><span class="sxs-lookup"><span data-stu-id="1b701-157">Configure hello cluster</span></span>

<span data-ttu-id="1b701-158">根據預設，在 HDInsight 上的 Storm 不包含 hello 元件，HdfsBolt 使用 toocommunicate 搭配 Azure 儲存體或資料湖存放區中出現的 classpath。</span><span class="sxs-lookup"><span data-stu-id="1b701-158">By default, Storm on HDInsight does not include hello components that HdfsBolt uses toocommunicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="1b701-159">使用 hello 下列指令碼動作 tooadd 這些元件 toohello `extlib` Storm 的叢集上目錄：</span><span class="sxs-lookup"><span data-stu-id="1b701-159">Use hello following script action tooadd these components toohello `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="1b701-160">|指令碼 URI |節點 tooapply 它 |參數 | |`https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` |Nimbus、 監督員 |None |</span><span class="sxs-lookup"><span data-stu-id="1b701-160">| Script URI | Nodes tooapply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="1b701-161">如需使用此指令碼與您的叢集資訊，請參閱 hello[使用指令碼動作的自訂 HDInsight 叢集](./hdinsight-hadoop-customize-cluster-linux.md)文件。</span><span class="sxs-lookup"><span data-stu-id="1b701-161">For information on using this script with your cluster, see hello [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-hello-topology"></a><span data-ttu-id="1b701-162">建置並封裝 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="1b701-162">Build and package hello topology</span></span>

1. <span data-ttu-id="1b701-163">下載 hello 範例專案，從[https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour 開發環境。</span><span class="sxs-lookup"><span data-stu-id="1b701-163">Download hello example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour development environment.</span></span>

2. <span data-ttu-id="1b701-164">從命令提示字元中，終端機或殼層工作階段中，變更目錄 toohello 根的 hello 已經下載專案。</span><span class="sxs-lookup"><span data-stu-id="1b701-164">From a command prompt, terminal, or shell session, change directories toohello root of hello downloaded project.</span></span> <span data-ttu-id="1b701-165">toobuild 和套件 hello 拓撲，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-165">toobuild and package hello topology, use hello following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="1b701-166">Hello 建置和封裝完成之後，沒有名為的新目錄`target`，其中包含名為`StormToHdfs-1.0-SNAPSHOT.jar`。</span><span class="sxs-lookup"><span data-stu-id="1b701-166">Once hello build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="1b701-167">此檔案包含編譯 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="1b701-167">This file contains hello compiled topology.</span></span>

## <a name="deploy-and-run-hello-topology"></a><span data-ttu-id="1b701-168">部署和執行 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="1b701-168">Deploy and run hello topology</span></span>

1. <span data-ttu-id="1b701-169">使用下列命令 toocopy hello 拓撲 toohello HDInsight 叢集的 hello。</span><span class="sxs-lookup"><span data-stu-id="1b701-169">Use hello following command toocopy hello topology toohello HDInsight cluster.</span></span> <span data-ttu-id="1b701-170">取代**使用者**hello SSH 使用者名稱與您在建立時使用 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b701-170">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="1b701-171">取代**CLUSTERNAME** hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1b701-171">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="1b701-172">出現提示時，輸入 hello 建立 hello SSH 使用者 hello 叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="1b701-172">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="1b701-173">如果您使用公開金鑰而不使用密碼時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 相符的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1b701-173">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b701-174">如需搭配 HDInsight 使用 `scp` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](./hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="1b701-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1b701-175">Hello 上傳完成之後，請使用下列 tooconnect toohello HDInsight 叢集使用 SSH hello。</span><span class="sxs-lookup"><span data-stu-id="1b701-175">Once hello upload completes, use hello following tooconnect toohello HDInsight cluster using SSH.</span></span> <span data-ttu-id="1b701-176">取代**使用者**hello SSH 使用者名稱與您在建立時使用 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b701-176">Replace **USER** with hello SSH user name you used when creating hello cluster.</span></span> <span data-ttu-id="1b701-177">取代**CLUSTERNAME** hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="1b701-177">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="1b701-178">出現提示時，輸入 hello 建立 hello SSH 使用者 hello 叢集時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="1b701-178">When prompted, enter hello password used when creating hello SSH user for hello cluster.</span></span> <span data-ttu-id="1b701-179">如果您使用公開金鑰而不使用密碼時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 相符的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1b701-179">If you used a public key instead of a password, you may need toouse hello `-i` parameter toospecify hello path toohello matching private key.</span></span>
   
   <span data-ttu-id="1b701-180">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="1b701-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="1b701-181">一旦連接之後，使用 hello 下列命令 toocreate 名為`dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="1b701-181">Once connected, use hello following command toocreate a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="1b701-182">使用 hello 文字之後做為 hello 內容的 hello`dev.properties`檔案：</span><span class="sxs-lookup"><span data-stu-id="1b701-182">Use hello following text as hello contents of hello `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="1b701-183">這個範例假設您的叢集使用的 Azure 儲存體帳戶，做為 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="1b701-183">This example assumes that your cluster uses an Azure Storage account as hello default storage.</span></span> <span data-ttu-id="1b701-184">如果叢集使用 Azure Data Lake Store，請改為使用 `hdfs.url: adl:///`。</span><span class="sxs-lookup"><span data-stu-id="1b701-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="1b701-185">toosave hello 檔案，使用__Ctrl + X__，然後__Y__，最後再__Enter__。</span><span class="sxs-lookup"><span data-stu-id="1b701-185">toosave hello file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="1b701-186">此檔案中的 hello 值設定 hello 資料湖存放區 URL 和 hello 資料寫入的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="1b701-186">hello values in this file set hello Data Lake store URL and hello directory name that data is written to.</span></span>

3. <span data-ttu-id="1b701-187">使用下列命令 toostart hello 拓撲 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-187">Use hello following command toostart hello topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="1b701-188">此命令啟動 hello 拓撲使用 hello 變動 framework 提交它 toohello Nimbus hello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="1b701-188">This command starts hello topology using hello Flux framework by submitting it toohello Nimbus node of hello cluster.</span></span> <span data-ttu-id="1b701-189">hello 拓撲由 hello`writetohdfs.yaml`納入 hello jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="1b701-189">hello topology is defined by hello `writetohdfs.yaml` file included in hello jar.</span></span> <span data-ttu-id="1b701-190">hello`dev.properties`檔案會傳遞做為篩選條件，並且 hello 檔案中所包含的 hello 值被讀取的 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="1b701-190">hello `dev.properties` file is passed as a filter, and hello values contained in hello file are read by hello topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="1b701-191">檢視輸出資料</span><span class="sxs-lookup"><span data-stu-id="1b701-191">View output data</span></span>

<span data-ttu-id="1b701-192">tooview hello 資料，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-192">tooview hello data, use hello following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="1b701-193">此拓撲中所建立的 hello 檔案的清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1b701-193">A list of hello files created by this topology is displayed.</span></span>

<span data-ttu-id="1b701-194">hello 下列清單是 hello hello 先前命令所傳回的資料的範例：</span><span class="sxs-lookup"><span data-stu-id="1b701-194">hello following list is an example of hello data retuned by hello previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a><span data-ttu-id="1b701-195">停止 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="1b701-195">Stop hello topology</span></span>

<span data-ttu-id="1b701-196">Storm 拓撲執行之前停止，或刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b701-196">Storm topologies run until stopped, or hello cluster is deleted.</span></span> <span data-ttu-id="1b701-197">toostop hello 拓撲，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b701-197">toostop hello topology, use hello following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="1b701-198">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="1b701-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="1b701-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b701-199">Next steps</span></span>

<span data-ttu-id="1b701-200">既然您已經學會如何 toouse Storm toowrite tooAzure 儲存體和 Azure 資料湖存放區，找出其他[Storm 範例 hdinsight](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="1b701-200">Now that you have learned how toouse Storm toowrite tooAzure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

