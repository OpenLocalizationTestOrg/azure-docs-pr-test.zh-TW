---
title: "Apache Storm 寫入儲存體/Data Lake Store - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Storm 寫入 HDInsight 的 HDFS 相容儲存體。 Azure 儲存體或 Azure Data Lake Store 提供了 HDInsight 的 HDFS 相容儲存體。 本文件與相關聯的範例示範如何使用 HdfsBolt 元件寫入 Storm on HDInsight 叢集的預設儲存體。"
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
ms.openlocfilehash: 10dc8789e8f4a2b27fd3a4c6fec2ab28c674170a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="write-to-hdfs-from-apache-storm-on-hdinsight"></a><span data-ttu-id="6d3e1-105">從 Apache Storm on HDInsight 寫入 HDFS</span><span class="sxs-lookup"><span data-stu-id="6d3e1-105">Write to HDFS from Apache Storm on HDInsight</span></span>

<span data-ttu-id="6d3e1-106">了解如何使用 Storm 將資料寫入 Apache Storm on HDInsight 所使用的 HDFS 相容儲存體。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-106">Learn how to use Storm to write data to the HDFS-compatible storage used by Apache Storm on HDInsight.</span></span> <span data-ttu-id="6d3e1-107">HDInsight 可以同時使用 Azure 儲存體以及 Azure Data Lake Store 作為 HDFS 相容儲存體。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-107">HDInsight can use both Azure Storage and Azure Data Lake store as HDFS-comptabile storage.</span></span> <span data-ttu-id="6d3e1-108">Storm 提供了將資料寫入 HDFS 的 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 元件。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-108">Storm provides an [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) component that writes data to HDFS.</span></span> <span data-ttu-id="6d3e1-109">本文件提供從 HdfsBolt 寫入任一類型儲存體的資訊。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-109">This document provides information on writing to either type of storage from the HdfsBolt.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6d3e1-110">本文件使用的範例拓撲依賴 Storm on HDInsight 隨附的元件。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-110">The example topology used in this document relies on components that are included with Storm on HDInsight.</span></span> <span data-ttu-id="6d3e1-111">它可能需要進行修改，才能在與其他 Apache Storm 叢集搭配使用時使用 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-111">It may require modification to work with Azure Data Lake Store when used with other Apache Storm clusters.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="6d3e1-112">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="6d3e1-112">Get the code</span></span>

<span data-ttu-id="6d3e1-113">包含此拓撲的專案可從 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)下載。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-113">The project containing this topology is available as a download from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).</span></span>

<span data-ttu-id="6d3e1-114">若要編譯此專案，您需要開發環境的下列設定：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-114">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="6d3e1-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-115">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="6d3e1-116">HDInsight 3.5 或更新版本需要 Java 8。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-116">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="6d3e1-117">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="6d3e1-117">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

<span data-ttu-id="6d3e1-118">當您在開發工作站上安裝 Java 和 JDK 時可能會設定下列環境變數。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-118">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="6d3e1-119">不過，您應該檢查它們是否存在，以及它們是否包含您系統的正確值。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="6d3e1-120">`JAVA_HOME` - 應指向已安裝 JDK 的目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-120">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="6d3e1-121">`PATH` - 應該包含下列路徑：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-121">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="6d3e1-122">`JAVA_HOME` (或對等的路徑)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-122">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="6d3e1-123">`JAVA_HOME\bin` (或對等的路徑)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-123">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="6d3e1-124">已安裝 Maven 的目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-124">The directory where Maven is installed.</span></span>

## <a name="how-to-use-the-hdfsbolt-with-hdinsight"></a><span data-ttu-id="6d3e1-125">如何搭配 HDInsight 使用 HdfsBolt</span><span class="sxs-lookup"><span data-stu-id="6d3e1-125">How to use the HdfsBolt with HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d3e1-126">在搭配 Storm on HDInsight 使用 HdfsBolt 之前，您必須先使用指令碼動作，將所需的 Jar 檔案複製到 Storm 的 `extpath`。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-126">Before using the HdfsBolt with Storm on HDInsight, you must first use a script action to copy required jar files into the `extpath` for Storm.</span></span> <span data-ttu-id="6d3e1-127">如需詳細資訊，請參閱[設定叢集](#configure)一節。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-127">For more information, see the [Configure the cluster](#configure) section.</span></span>

<span data-ttu-id="6d3e1-128">HdfsBolt 會使用您提供的檔案配置來了解如何寫入 HDFS。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-128">The HdfsBolt uses the file scheme that you provide to understand how to write to HDFS.</span></span> <span data-ttu-id="6d3e1-129">利用 HDInsight 時，請使用下列其中一項配置：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-129">With HDInsight, use one of the following schemes:</span></span>

* <span data-ttu-id="6d3e1-130">`wasb://`：搭配使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-130">`wasb://`: Used with an Azure Storage account.</span></span>
* <span data-ttu-id="6d3e1-131">`adl://`：搭配使用 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-131">`adl://`: Used with Azure Data Lake Store.</span></span>

<span data-ttu-id="6d3e1-132">下表提供針對不同案例使用檔案配置的範例：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-132">The following table provides examples of using the file scheme for different scenarios:</span></span>

| <span data-ttu-id="6d3e1-133">配置</span><span class="sxs-lookup"><span data-stu-id="6d3e1-133">Scheme</span></span> | <span data-ttu-id="6d3e1-134">注意事項</span><span class="sxs-lookup"><span data-stu-id="6d3e1-134">Notes</span></span> |
| ----- | ----- |
| `wasb:///` | <span data-ttu-id="6d3e1-135">預設儲存體帳戶是 Azure 儲存體帳戶中的 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="6d3e1-135">The default storage account is a blob container in an Azure Storage account</span></span> |
| `adl:///` | <span data-ttu-id="6d3e1-136">預設儲存體帳戶是 Azure Data Lake Store 中的目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-136">The default storage account is a directory in Azure Data Lake Store.</span></span> <span data-ttu-id="6d3e1-137">叢集建立期間，您可以指定 Data Lake Store 中其為叢集 HDFS 根目錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-137">During cluster creation, you specify the directory in Data Lake Store that is the root of the cluster's HDFS.</span></span> <span data-ttu-id="6d3e1-138">例如，`/clusters/myclustername/` 目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-138">For example, the `/clusters/myclustername/` directory.</span></span> |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | <span data-ttu-id="6d3e1-139">與叢集建立關聯的非預設 (其他) Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-139">A non-default (additional) Azure storage account associated with the cluster.</span></span> |
| `adl://STORENAME/` | <span data-ttu-id="6d3e1-140">叢集所使用的 Data Lake Store 根目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-140">The root of the Data Lake Store used by the cluster.</span></span> <span data-ttu-id="6d3e1-141">此配置可讓您存取位於叢集檔案系統所在目錄外部的資料。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-141">This scheme allows you to access data that is located outside the directory that contains the cluster file system.</span></span> |

<span data-ttu-id="6d3e1-142">如需詳細資訊，請參閱 Apache.org 上的 [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) 參考。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-142">For more information, see the [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) reference at Apache.org.</span></span>

### <a name="example-configuration"></a><span data-ttu-id="6d3e1-143">設定範例</span><span class="sxs-lookup"><span data-stu-id="6d3e1-143">Example configuration</span></span>

<span data-ttu-id="6d3e1-144">下列 YAML 是摘錄自範例中隨附的 `resources/writetohdfs.yaml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-144">The following YAML is an excerpt from the `resources/writetohdfs.yaml` file included in the example.</span></span> <span data-ttu-id="6d3e1-145">此檔案會使用 Apache Storm 的 [Flux](https://storm.apache.org/releases/1.1.0/flux.html) 架構定義 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-145">This file defines the Storm topology using the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework for Apache Storm.</span></span>

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

<span data-ttu-id="6d3e1-146">此 YAML 會定義下列項目：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-146">This YAML defines the following items:</span></span>

* <span data-ttu-id="6d3e1-147">`syncPolicy`：定義檔案何時同步處理/排清到檔案系統。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-147">`syncPolicy`: Defines when files are synched/flushed to the file system.</span></span> <span data-ttu-id="6d3e1-148">在此範例中，為每 1000 個 Tuple。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-148">In this example, every 1000 tuples.</span></span>
* <span data-ttu-id="6d3e1-149">`fileNameFormat`：定義寫入檔案時要使用的路徑和檔案名稱模式。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-149">`fileNameFormat`: Defines the path and file name pattern to use when writing files.</span></span> <span data-ttu-id="6d3e1-150">在此範例中，會使用篩選條件在執行階段提供路徑，而檔案的副檔名為 `.txt`。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-150">In this example, the path is provided at runtime using a filter, and the file extension is `.txt`.</span></span>
* <span data-ttu-id="6d3e1-151">`recordFormat`：定義所寫入檔案的內部格式。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-151">`recordFormat`: Defines the internal format of the files written.</span></span> <span data-ttu-id="6d3e1-152">在此範例中，會以 `|` 字元分隔欄位。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-152">In this example, fields are delimited by the `|` character.</span></span>
* <span data-ttu-id="6d3e1-153">`rotationPolicy`：定義何時輪替檔案。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-153">`rotationPolicy`: Defines when to rotate files.</span></span> <span data-ttu-id="6d3e1-154">在此範例中，不會執行輪替。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-154">In this example, no rotation is performed.</span></span>
* <span data-ttu-id="6d3e1-155">`hdfs-bolt`：使用舊版元件作為 `HdfsBolt` 類別的設定參數。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-155">`hdfs-bolt`: Uses the previous components as configuration parameters for the `HdfsBolt` class.</span></span>

<span data-ttu-id="6d3e1-156">如需 Flux 架構的詳細資訊，請參閱 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-156">For more information on the Flux framework, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="configure-the-cluster"></a><span data-ttu-id="6d3e1-157">設定叢集</span><span class="sxs-lookup"><span data-stu-id="6d3e1-157">Configure the cluster</span></span>

<span data-ttu-id="6d3e1-158">根據預設，Storm on HDInsight 未包含 HdfsBolt 用來與 Storm Classpath 中出現的 Azure 儲存體或 Data Lake Store 進行通訊的元件。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-158">By default, Storm on HDInsight does not include the components that HdfsBolt uses to communicate with Azure Storage or Data Lake Store in Storm's classpath.</span></span> <span data-ttu-id="6d3e1-159">請使用下列指令碼動作，將這些元件新增至叢集上 Storm 的 `extlib` 目錄：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-159">Use the following script action to add these components to the `extlib` directory for Storm on your cluster:</span></span>

<span data-ttu-id="6d3e1-160">|指令碼 URI |要套用它的節點 |參數 | |`https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` |Nimbus、監督員 |無 |</span><span class="sxs-lookup"><span data-stu-id="6d3e1-160">| Script URI | Nodes to apply it to| Parameters | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | None |</span></span>

<span data-ttu-id="6d3e1-161">如需搭配叢集使用此指令碼的資訊，請參閱[使用指令碼動作自訂 HDInsight 叢集](./hdinsight-hadoop-customize-cluster-linux.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-161">For information on using this script with your cluster, see the [Customize HDInsight clusters using script actions](./hdinsight-hadoop-customize-cluster-linux.md) document.</span></span>

## <a name="build-and-package-the-topology"></a><span data-ttu-id="6d3e1-162">建置和封裝拓撲</span><span class="sxs-lookup"><span data-stu-id="6d3e1-162">Build and package the topology</span></span>

1. <span data-ttu-id="6d3e1-163">從 [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) 下載範例專案到開發環境。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-163">Download the example project from [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) to your development environment.</span></span>

2. <span data-ttu-id="6d3e1-164">從命令提示字元、終端機或 Shell 工作階段，將目錄變更為所下載專案的根目錄。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-164">From a command prompt, terminal, or shell session, change directories to the root of the downloaded project.</span></span> <span data-ttu-id="6d3e1-165">若要建置和封裝拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-165">To build and package the topology, use the following command:</span></span>
   
        mvn compile package
   
    <span data-ttu-id="6d3e1-166">建置和封裝完成之後，會有名為 `target` 的新目錄，其中包含名為 `StormToHdfs-1.0-SNAPSHOT.jar` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-166">Once the build and packaging completes, there is a new directory named `target`, that contains a file named `StormToHdfs-1.0-SNAPSHOT.jar`.</span></span> <span data-ttu-id="6d3e1-167">此檔案包含已編譯的拓撲。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-167">This file contains the compiled topology.</span></span>

## <a name="deploy-and-run-the-topology"></a><span data-ttu-id="6d3e1-168">部署並執行拓撲</span><span class="sxs-lookup"><span data-stu-id="6d3e1-168">Deploy and run the topology</span></span>

1. <span data-ttu-id="6d3e1-169">使用下列命令將拓撲複製到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-169">Use the following command to copy the topology to the HDInsight cluster.</span></span> <span data-ttu-id="6d3e1-170">將 **USER** 取代為建立叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-170">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="6d3e1-171">將 **CLUSTERNAME** 取代為叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-171">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    <span data-ttu-id="6d3e1-172">出現提示時，請輸入建立叢集的 SSH 使用者時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-172">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="6d3e1-173">如果您使用公開金鑰而非密碼，則可能必須使用 `-i` 參數來指定相對應私密金鑰的路徑。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-173">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6d3e1-174">如需搭配 HDInsight 使用 `scp` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](./hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-174">For more information on using `scp` with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="6d3e1-175">上傳完成後，使用下列命令來透過 SSH 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-175">Once the upload completes, use the following to connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="6d3e1-176">將 **USER** 取代為建立叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-176">Replace **USER** with the SSH user name you used when creating the cluster.</span></span> <span data-ttu-id="6d3e1-177">將 **CLUSTERNAME** 取代為叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-177">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="6d3e1-178">出現提示時，請輸入建立叢集的 SSH 使用者時所使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-178">When prompted, enter the password used when creating the SSH user for the cluster.</span></span> <span data-ttu-id="6d3e1-179">如果您使用公開金鑰而非密碼，則可能必須使用 `-i` 參數來指定相對應私密金鑰的路徑。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-179">If you used a public key instead of a password, you may need to use the `-i` parameter to specify the path to the matching private key.</span></span>
   
   <span data-ttu-id="6d3e1-180">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-180">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="6d3e1-181">連接之後，使用下列命令來建立名為 `dev.properties` 的檔案：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-181">Once connected, use the following command to create a file named `dev.properties`:</span></span>

        nano dev.properties

4. <span data-ttu-id="6d3e1-182">使用下列文字做為 `dev.properties` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-182">Use the following text as the contents of the `dev.properties` file:</span></span>

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > <span data-ttu-id="6d3e1-183">這個範例假設您的叢集使用 Azure 儲存體帳戶作為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-183">This example assumes that your cluster uses an Azure Storage account as the default storage.</span></span> <span data-ttu-id="6d3e1-184">如果叢集使用 Azure Data Lake Store，請改為使用 `hdfs.url: adl:///`。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-184">If your cluster uses Azure Data Lake Store, use `hdfs.url: adl:///` instead.</span></span>
    
    <span data-ttu-id="6d3e1-185">若要儲存檔案，使用 __Ctrl + X__，然後是 __Y__，最後按 __Enter__。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-185">To save the file, use __Ctrl + X__, then __Y__, and finally __Enter__.</span></span> <span data-ttu-id="6d3e1-186">此檔案中的值會設定 Data Lake Store URL，以及要寫入資料的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-186">The values in this file set the Data Lake store URL and the directory name that data is written to.</span></span>

3. <span data-ttu-id="6d3e1-187">使用下列命令來啟動拓撲：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-187">Use the following command to start the topology:</span></span>
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    <span data-ttu-id="6d3e1-188">此命令藉由將拓撲提交給叢集的 Nimbus 節點，以使用 Flux 架構來啟動拓撲。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-188">This command starts the topology using the Flux framework by submitting it to the Nimbus node of the cluster.</span></span> <span data-ttu-id="6d3e1-189">拓撲是由 jar 中包含的 `writetohdfs.yaml` 檔案所定義。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-189">The topology is defined by the `writetohdfs.yaml` file included in the jar.</span></span> <span data-ttu-id="6d3e1-190">`dev.properties` 檔案會傳遞來做為篩選，而檔案中包含的值是透過拓撲來讀取。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-190">The `dev.properties` file is passed as a filter, and the values contained in the file are read by the topology.</span></span>

## <a name="view-output-data"></a><span data-ttu-id="6d3e1-191">檢視輸出資料</span><span class="sxs-lookup"><span data-stu-id="6d3e1-191">View output data</span></span>

<span data-ttu-id="6d3e1-192">若要檢視資料，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-192">To view the data, use the following command:</span></span>

    hdfs dfs -ls /stormdata/

<span data-ttu-id="6d3e1-193">隨即會顯示此拓撲所建立的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-193">A list of the files created by this topology is displayed.</span></span>

<span data-ttu-id="6d3e1-194">下列清單是前一個命令所傳回的資料範例：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-194">The following list is an example of the data retuned by the previous commands:</span></span>

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-the-topology"></a><span data-ttu-id="6d3e1-195">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="6d3e1-195">Stop the topology</span></span>

<span data-ttu-id="6d3e1-196">Storm 拓撲會一直執行，直到其停止或叢集遭到刪除為止。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-196">Storm topologies run until stopped, or the cluster is deleted.</span></span> <span data-ttu-id="6d3e1-197">若要停止拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6d3e1-197">To stop the topology, use the following command:</span></span>

    storm kill hdfswriter

## <a name="delete-your-cluster"></a><span data-ttu-id="6d3e1-198">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="6d3e1-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="6d3e1-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d3e1-199">Next steps</span></span>

<span data-ttu-id="6d3e1-200">現在，您已了解如何使用 Storm 來寫入至 Azure 儲存體和 Azure Data Lake Store，接下來請探索其他 [HDInsight 的 Storm 範例](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="6d3e1-200">Now that you have learned how to use Storm to write to Azure Storage and Azure Data Lake Store, discover other [Storm examples for HDInsight](hdinsight-storm-example-topology.md).</span></span>

