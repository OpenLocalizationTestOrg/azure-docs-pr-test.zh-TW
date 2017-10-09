---
title: "與 linux 的 HDInsight 的 Azure 開發 aaaScript 動作 |Microsoft 文件"
description: "了解如何 toouse Bash 指令碼 toocustomize 以 Linux 為基礎的 HDInsight 叢集。 HDInsight 的 hello 指令碼動作的功能可讓您 toorun 指令碼期間或之後建立叢集。 指令碼可以使用的 toochange 叢集組態設定或安裝其他軟體。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>使用 HDInsight 開發指令碼動作

深入了解如何撞 toocustomize 您 HDInsight 叢集使用指令碼。 指令碼動作是方式 toocustomize HDInsight 期間或之後建立叢集。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="what-are-script-actions"></a>什麼是指令碼動作

指令碼動作，Azure 會 hello 叢集節點 toomake 設定變更上執行 Bash 指令碼，或安裝軟體。 指令碼動作為根，會執行，而且提供的完整存取權限 toohello 叢集節點。

您可以透過下列方法的 hello 套用指令碼動作：

| 使用此方法 tooapply 指令碼... | 在叢集建立期間... | 在執行中的叢集上... |
| --- |:---:|:---:|
| Azure 入口網站 |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| Azure CLI |&nbsp; |✓ |
| HDInsight .NET SDK |✓ |✓ |
| Azure Resource Manager 範本 |✓  |&nbsp; |

如需有關使用這些方法 tooapply 指令碼動作的詳細資訊，請參閱[使用指令碼動作的自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

## <a name="bestPracticeScripting"></a>指令碼開發的最佳做法

當您開發的 HDInsight 叢集的自訂指令碼時，有數個最佳作法 tookeep 事項：

* [Hello Hadoop 版本為目標](#bPS1)
* [目標 hello OS 版本](#bps10)
* [提供穩定連結 tooscript 資源](#bPS2)
* [使用預先編譯的資源](#bPS4)
* [確保 hello 叢集自訂指令碼為等冪](#bPS3)
* [確保高可用性的 hello 叢集架構](#bPS5)
* [設定 hello 自訂元件 toouse Azure Blob 儲存體](#bPS6)
* [寫入資訊 tooSTDOUT 和 STDERR](#bPS7)
* [將檔案儲存為具有 LF 行尾結束符號的 ASCII](#bps8)
* [使用從暫時性錯誤重試邏輯 toorecover](#bps9)

> [!IMPORTANT]
> 指令碼動作必須在 60 分鐘的時間內完成，或 hello 程序會失敗。 在佈建的節點，與其他安裝及設定處理程序同時執行 hello 指令碼。 競爭資源，例如 CPU 時間和網路頻寬可能會導致 hello 指令碼 tootake 長 toofinish 不同於您的開發環境。

### <a name="bPS1"></a>Hello Hadoop 版本為目標

不同版本的 HDInsight 有不同版本的 Hadoop 服務和已安裝的元件。 如果您的指令碼需要特定版本的服務或元件，您應該只使用 hello 指令碼 hello 包含所需的 hello 元件的 HDInsight 版本。 您可以找到有關隨附 HDInsight 的元件版本使用 hello [HDInsight 的元件版本控制](hdinsight-component-versioning.md)文件。

### <a name="bps10"></a>目標 hello OS 版本

以 Linux 為基礎的 HDInsight 根據 hello Ubuntu Linux 散發套件。 不同 HDInsight 版本仰賴不同的 Ubuntu 版本，這可能會改變指令碼的運作方式。 例如，HDInsight 3.4 及更早版本所根據的是使用 Upstart 的 Ubuntu 版本。 3.5 版所根據的是 Ubuntu 16.04，其使用的是 Systemd。 Systemd 和同時依賴不同的命令，讓您的指令碼應寫入 toowork 同時使用。

HDInsight 3.4 和 3.5 之間的另一個重要的差異在於`JAVA_HOME`現在點 tooJava 8。

您可以藉由檢查 hello OS 版本`lsb_release`。 hello 下列程式碼示範如何 toodetermine 如果 hello 指令碼 Ubuntu 14 或 16 上執行：

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

您可以找到包含這些程式碼片段在 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh hello 完整指令碼。

如需使用 HDInsight 的 Ubuntu hello 版本，請參閱 hello [HDInsight 元件版本](hdinsight-component-versioning.md)文件。

toounderstand hello Systemd 和差異同時，請參閱[同時使用者 Systemd](https://wiki.ubuntu.com/SystemdForUpstartUsers)。

### <a name="bPS2"></a>提供穩定連結 tooscript 資源

hello 指令碼和相關聯的資源必須維持可在整個存留期 hello hello 叢集。 如果新節點加入叢集 toohello 縮放作業期間需要這些資源。

hello 最佳作法是 toodownload 和封存您的訂用帳戶的 Azure 儲存體帳戶中的所有項目。

> [!IMPORTANT]
> 使用 hello 儲存體帳戶必須是 hello 預設儲存體帳戶的 hello 叢集或公開的唯讀容器上任何其他儲存體帳戶。

例如，由 Microsoft 提供的 hello 範例會儲存在 hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/)儲存體帳戶。 這是由 hello HDInsight 團隊負責維護的公用、 唯讀容器。

### <a name="bPS4"></a>使用預先編譯的資源

tooreduce hello 次它採用 toorun hello 指令碼時，避免編譯資源從來源程式碼的作業。 比方說，先行編譯的資源，並將其儲存在 Azure 儲存體帳戶中 blob hello 與 HDInsight 的相同資料中心。

### <a name="bPS3"></a>確保 hello 叢集自訂指令碼為等冪

指令碼必須具有等冪性。 如果多次執行 hello 指令碼，它應該傳回 hello 叢集 toohello 相同狀態的每一次。

例如，如果一個會修改組態檔的指令碼執行多次，則不應該新增重複的項目。

### <a name="bPS5"></a>確保高可用性的 hello 叢集架構

以 Linux 為基礎的 HDInsight 叢集提供 hello 叢集內的作用中的兩個前端節點和兩個節點上執行指令碼動作。 如果您安裝的 hello 元件預期只有一個前端節點，請勿在這兩個前端節點上安裝 hello 元件。

> [!IMPORTANT]
> HDInsight 中提供的服務是設計的 toofail 透過 hello 兩個前端節點之間所需。 這項功能不會延長 toocustom 安裝的元件，透過指令碼動作。 如果自訂元件需要有高可用性時，您必須實作自己的容錯移轉機制。

### <a name="bPS6"></a>設定 hello 自訂元件 toouse Azure Blob 儲存體

您在 hello 叢集安裝的元件可能必須使用 Hadoop 分散式檔案系統 (HDFS) 儲存體的預設設定。 HDInsight 使用 Azure 儲存體或資料湖存放區做為 hello 預設儲存體。 這兩者都提供保存資料，即使已經刪除 hello 叢集的 HDFS 相容的檔案系統。 您可能需要安裝 toouse WASB 或而不是 HDFS ADL tooconfigure 元件。

對於大部分的作業，您不需要 toospecify hello 檔案系統。 例如，下列 hello hello giraph examples.jar 會從檔案複製 hello 本機檔案系統 toocluster 儲存體：

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

在此範例中，hello`hdfs`命令以透明的方式使用 hello 預設叢集存放區。 對於某些運算而言，您可能需要 toospecify hello URI。 例如，Data Lake Store 的 `adl:///example/jars`，或 Azure 儲存體的 `wasb:///example/jars`。

### <a name="bPS7"></a>寫入資訊 tooSTDOUT 和 STDERR

HDInsight 記錄會寫入的 tooSTDOUT 和 STDERR 的指令碼輸出。 您可以檢視這項資訊使用 hello Ambari web UI。

> [!NOTE]
> Ambari 才可以使用已成功建立 hello 叢集。 如果您使用指令碼動作在叢集建立，並建立動作失敗時，請參閱 < 疑難排解 > 一節的 hello[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)的其他方式存取登入的資訊。

大部分的公用程式和安裝封裝已經寫入資訊 tooSTDOUT 和 STDERR，不過您可能會想 tooadd 額外的記錄功能。 toosend 文字 tooSTDOUT 使用`echo`。 例如：

```bash
echo "Getting ready tooinstall Foo"
```

根據預設，`echo`傳送 hello 字串 tooSTDOUT。 toodirect 它 tooSTDERR，新增`>&2`之前`echo`。 例如：

```bash
>&2 echo "An error occurred installing Foo"
```

這將會改寫入 tooSTDOUT tooSTDERR (2) 的資訊重新導向。 如需 IO 重新導向的詳細資訊，請參閱 [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html)。

如需檢視指令碼動作記錄之資訊的詳細資訊，請參閱 [使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> 將檔案儲存為具有 LF 行尾結束符號的 ASCII

Bash 指令碼應該儲存為 ASCII 格式，該格式以 LF 做為行尾結束符號。 檔案儲存為 utf-8，或做為可 CRLF hello 行尾結束符號可能會因下列錯誤 hello:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>使用從暫時性錯誤重試邏輯 toorecover

當下載檔案，安裝封裝使用 apt get 或傳輸資料的其他動作 hello 網際網路，hello 動作可能失敗的原因 tootransient 網路錯誤。 例如，您通訊的 hello 遠端資源可能處於 tooa 備份節點上方 hello 程序執行失敗。

toomake 指令碼具有恢復功能 tootransient 錯誤，您可以實作重試邏輯。 下列函式的 hello 示範如何 tooimplement 重試邏輯。 它會重試三次失敗之前的 hello 作業。

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

hello 下列範例將示範如何 toouse 此函式。

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>自訂指令碼的協助程式方法

指令碼動作協助程式方法是您在撰寫字訂指令碼時可以使用的公用程式。 這些方法全都在 [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) 指令碼中。 使用下列 toodownload hello 和使用它們做為您的指令碼的一部分：

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

下列 helper 可在您的指令碼中使用的 hello:

| 協助程式使用方式 | 說明 |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |下載檔案從 hello 來源 URI toohello 指定的檔案路徑。 根據預設，不會覆寫現有的檔案。 |
| `untar_file TARFILE DESTDIR` |解壓縮 tar 檔案解壓縮檔案 (使用`-xf`) toohello 目的地目錄。 |
| `test_is_headnode` |如果在叢集前端節點上執行，則會傳回 1，否則傳回 0。 |
| `test_is_datanode` |如果 hello 目前節點的資料 （背景工作角色） 節點，則傳回 1;否則為 0。 |
| `test_is_first_datanode` |如果 hello 目前節點為 hello 第一個資料 （背景工作角色） 節點 (具名 workernode0) 會傳回 1;否則為 0。 |
| `get_headnodes` |傳回 hello hello headnodes hello 叢集中的完整的網域名稱。 名稱會以逗號分隔。 發生錯誤時會傳回空字串。 |
| `get_primary_headnode` |取得 hello 的 hello 主要叢集前端節點的完整的網域名稱。 發生錯誤時會傳回空字串。 |
| `get_secondary_headnode` |取得 hello 的 hello 次要叢集前端節點的完整的網域名稱。 發生錯誤時會傳回空字串。 |
| `get_primary_headnode_number` |取得 hello 的 hello 主要叢集前端節點的數值後置詞。 發生錯誤時會傳回空字串。 |
| `get_secondary_headnode_number` |取得 hello 的 hello 次要叢集前端節點的數值後置詞。 發生錯誤時會傳回空字串。 |

## <a name="commonusage"></a>常見使用模式

此章節提供指引實作某些 hello 常見的使用模式，您可能會遇到撰寫自訂指令碼時。

### <a name="passing-parameters-tooa-script"></a>傳遞參數 tooa 指令碼

在某些情況下，您的指令碼可能需要參數。 例如，您可能需要 hello 系統管理員密碼 hello 叢集使用 hello Ambari REST API 時。

傳遞 toohello 指令碼參數稱為*位置參數*，以及要指派太`$1`hello 第一個參數， `$2` hello 第二個，並讓入。 `$0`包含 hello 的 hello 指令碼本身的名稱。

做為參數傳遞 toohello 指令碼的值應該放在單引號 （'）。 這麼做可確保該 hello 傳遞值視為常值。

### <a name="setting-environment-variables"></a>設定環境變數

設定環境變數被執行陳述式之後的 hello:

    VARIABLENAME=value

變數名稱所在 hello hello 變數名稱。 tooaccess hello 變數時，使用`$VARIABLENAME`。 比方說，tooassign 做為環境變數的位置參數所提供的值命名為密碼，可以使用下列陳述式的 hello:

    PASSWORD=$1

接著可以使用後續存取 toohello 資訊`$PASSWORD`。

Hello 指令碼內設定的環境變數只存在於 hello hello 指令碼範圍內。 在某些情況下，您可能需要 tooadd 全系統環境變數會保存 hello 指令碼完成後。 tooadd 全系統環境變數，加入 hello 變數太`/etc/environment`。 例如，將陳述式之後的 hello `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>存取的 toolocations hello 自訂指令碼的儲存位置

使用指令碼 toocustomize 叢集需要 toobe 儲存在下列位置的 hello 的其中一個：

* __Azure 儲存體帳戶__與 hello 叢集相關聯。

* __額外的儲存體帳戶__hello 叢集相關聯。

* __可公開讀取的 URI__。 例如，URL toodata 儲存在 OneDrive、 Dropbox 或裝載服務的其他檔案。

* __Azure Data Lake Store 帳戶__與 hello HDInsight 叢集相關聯。 如需使用 Azure Data Lake Store 與 HDInsight 的詳細資訊，請參閱[建立使用 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。

    > [!NOTE]
    > hello 服務主體 HDInsight 使用 tooaccess 資料湖存放區必須有讀取權限 toohello 指令碼。

Hello 指令碼所使用的資源也必須是公用的。

將 hello 檔案儲存在 Azure 儲存體帳戶或 Azure 資料湖存放區提供快速存取，同時 hello Azure 網路內。

> [!NOTE]
> hello URI 格式使用 tooreference hello 指令碼是根據目前使用的 hello 服務而有所不同。 Hello HDInsight 叢集相關聯的儲存體帳戶，使用`wasb://`或`wasbs://`。 若為可公開讀取的 URI，請使用 `http://` 或 `https://`。 若為 Data Lake Store，請使用 `adl://`。

### <a name="checking-hello-operating-system-version"></a>正在檢查 hello 作業系統版本

不同 HDInsight 版本各仰賴特定的 Ubuntu 版本。 您在指令碼中必須檢查的 OS 版本之間可能會有差異。 例如，您可能需要 tooinstall Ubuntu 繫結的 toohello 版本的二進位檔。

toocheck hello OS 版本，使用`lsb_release`。 例如，下列指令碼的 hello 示範根據 hello OS 版本 tooreference 特定 tar 檔案解壓縮檔案的方式：

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>指令碼動作的部署檢查清單

準備 toodeploy 這些指令碼時，我們採用的 hello 步驟如下：

* 將包含 hello 自訂指令碼可在部署期間 hello 叢集節點可存取的位置中的 hello 檔案。 例如，hello hello 叢集的預設儲存體。 檔案也可以儲存在可公開讀取的主機服務中。
* 確認 impotent hello 指令碼。 這樣做可讓 hello 指令碼 toobe 執行多次 hello 上相同節點。
* 使用暫存檔目錄 tec_rule 位於 /tmp tookeep hello 下載 hello 指令碼所使用的檔案，然後再清除它們之後執行指令碼。
* 如果作業系統層級的設定或 Hadoop 服務組態檔已變更，您可能想 toorestart HDInsight 服務。

## <a name="runScriptAction"></a>如何 toorun 指令碼動作

您可以使用指令碼動作 toocustomize HDInsight 叢集使用 hello 下列方法：

* Azure 入口網站
* Azure PowerShell
* Azure 資源管理員範本
* hello HDInsight.NET SDK。

如需有關如何使用每個方法的詳細資訊，請參閱[toouse 如何編寫指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)。

## <a name="sampleScripts"></a>自訂指令碼範例

Microsoft 提供範例指令碼 tooinstall 元件上的 HDInsight 叢集。 請參閱下列連結以取得更多的範例指令碼動作的 hello。

* [在 HDInsight 叢集上安裝及使用色調](hdinsight-hadoop-hue-linux.md)
* [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install-linux.md)
* [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [在 HDInsight 叢集上安裝或升級 Mono](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>疑難排解

hello 下面是使用您所開發的指令碼時，可能會遇到的錯誤：

**錯誤**：`$'\r': command not found`。 有時候後面接續 `syntax error: unexpected end of file`。

*可能的原因*： 指令碼中的 hello 行結尾 CRLF 時造成這個錯誤。 Unix 系統預期只有 LF 為 hello 行尾結束符號。

發生此問題最常在 Windows 環境中，撰寫 hello 指令碼，則當因為 CRLF 是常見的行尾結束符號的 Windows 上的多個文字編輯器。

*解析*： 如果您的文字編輯器中的選項，請選取 Unix 格式或 LF hello 行尾結束符號。 您也可以使用下列命令在 Unix 系統 toochange hello CRLF tooan LF hello:

> [!NOTE]
> hello 下列命令的建立方式大致在於應變 hello CRLF 行尾結束符號 tooLF。 選取其中一個系統上可用的 hello 公用程式為基礎。

| 命令 | 注意事項 |
| --- | --- |
| `unix2dos -b INFILE` |hello 原始檔案會與備份。BAK 延伸模組 |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE 會包含只有 LF 行尾結束符號的版本 |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | 直接修改 hello 檔案 |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE 會包含只有 LF 行尾結束符號的版本。 |

**錯誤**：`line 1: #!/usr/bin/env: No such file or directory`。

*可能的原因*： 時會發生此錯誤 hello 指令碼已儲存為 utf-8 與位元組順序標記 (BOM)。

*解析*： 儲存 hello 檔案以 ascii 模式，或為不具有 BOM utf-8。 您也可以使用下列命令，在 Linux 或 Unix 系統 toocreate 沒有 hello BOM 的檔案上的 hello:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

取代`INFILE`hello 檔案包含 hello BOM。 `OUTFILE`應該是新的檔案名稱，其中包含不含 hello BOM hello 指令碼。

## <a name="seeAlso"></a>接續步驟

* 了解如何太[使用指令碼動作的自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)
* 使用 hello [HDInsight.NET SDK 參考](https://msdn.microsoft.com/library/mt271028.aspx)toolearn 深入了解建立管理 HDInsight 的.NET 應用程式
* 使用 hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn toouse REST tooperform 管理動作，在 HDInsight 上的叢集。
