---
title: "aaaScript 與 HDInsight 的 Azure 開發動作 |Microsoft 文件"
description: "了解如何 toocustomize Hadoop 叢集以指令碼動作。 指令碼動作都可以使用的 tooinstall 應用程式安裝在叢集的 Hadoop 叢集或 toochange hello 組態上所執行的其他軟體。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>開發 HDInsight Windows 型叢集指令碼動作指令碼
了解指令碼動作 toowrite hdinsight 的指令碼。 如需使用指令碼動作指令碼的資訊，請參閱[使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md)。 Hello 同一篇文章撰寫以 Linux 為基礎的 HDInsight 叢集，請參閱[開發指令碼動作的指令碼 hdinsight](hdinsight-hadoop-script-actions-linux.md)。



> [!IMPORTANT]
> hello 這個文件的唯一工作 Windows 為基礎的 HDInsight 叢集的步驟。 Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需有關搭配 Linux 型叢集使用指令碼動作的詳細資訊，請參閱[使用 HDInsight 進行指令碼動作開發 (Linux)](hdinsight-hadoop-script-actions-linux.md)。
>
>



指令碼動作都可以使用的 tooinstall 應用程式安裝在叢集的 Hadoop 叢集或 toochange hello 組態上所執行的其他軟體。 指令碼動作時的 HDInsight 叢集部署中，於 hello 叢集節點執行的指令碼，而且它們會執行 hello 叢集中的節點完成 HDInsight 組態之後。 指令碼動作在系統管理員帳戶權限下執行，並提供完整存取權限 toohello 叢集節點。 每個叢集可以提供一份指令碼動作 toobe 指定中的 hello 順序執行。

> [!NOTE]
> 如果您遇到下列錯誤訊息的 hello:
>
> System.Management.Automation.CommandNotFoundException;ExceptionMessage: hello 詞彙 ' 儲存 HDIFile' 無法辨識為 cmdlet、 函式、 指令碼檔案或可執行程式 hello 名稱。 Hello hello 名稱拼字檢查，或如果包含路徑的話，請確認該 hello 路徑正確，然後再試一次。
> 這是因為您未包含 hello helper 方法。  請參閱 [自訂指令碼的協助程式方法](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts)。
>
>

## <a name="sample-scripts"></a>範例指令碼
在 Windows 作業系統上建立 HDInsight 叢集，hello 指令碼動作是 Azure PowerShell 指令碼。 hello 下列指令碼是設定 hello 站台設定檔案的範例：

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

hello 指令碼會將四個參數、 hello 組態檔名稱、 hello toomodify，hello 值 tooset，以及描述您想要的屬性。 例如：

    hive-site.xml hive.metastore.client.socket.timeout 90

這些參數會設定 hello hive.metastore.client.socket.timeout 值 too90 hello hive-site.xml 檔案中。  hello 預設值為 60 秒。

此範例指令碼位於 [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1)。

HDInsight 提供數個指令碼 tooinstall 其他元件在 HDInsight 叢集上：

| 名稱 | 指令碼 |
| --- | --- |
| **安裝 Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1。 請參閱[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]。 |
| **安裝 R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1。 請參閱[在 HDInsight 叢集上安裝和使用 R][hdinsight-r-scripts]。 |
| **安裝 Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1。 請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。 |
| - **安裝 Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1。 請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。 |

可以從 hello Azure 入口網站，Azure PowerShell 部署指令碼動作，或使用 hello HDInsight.NET SDK。  如需詳細資訊，請參閱[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]。

> [!NOTE]
> hello 範例指令碼工作只會與 HDInsight 叢集版本 3.1 或更新版本。 如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。
>
>

## <a name="helper-methods-for-custom-scripts"></a>自訂指令碼的協助程式方法
指令碼動作協助程式方法是您在撰寫字訂指令碼時可以使用的公用程式。 這些方法會定義在[https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)，而且可以包含在指令碼使用下列範例中的 hello:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

以下是這個指令碼所提供的 hello helper 方法：

| 協助程式方法 | 說明 |
| --- | --- |
| **Save-HDIFile** |下載檔案，以從 hello hello 與 hello Azure VM 節點指派的 toohello 叢集相關聯的本機磁碟上指定統一資源識別元 (URI) tooa 位置。 |
| **Expand-HDIZippedFile** |將壓縮檔解壓縮。 |
| **Invoke-HDICmdScript** |從 cmd.exe 執行指令碼。 |
| **Write-HDILog** |將輸出寫入從 hello 自訂指令碼的指令碼動作使用。 |
| **Get-Services** |取得一份 hello 指令碼的執行位置 hello 機器上執行服務。 |
| **Get-Service** |Hello 特定服務名稱做為輸入，以取得特定服務的詳細的資訊 （服務名稱、 處理序識別碼、 狀態等等） hello hello 指令碼的執行位置的電腦上。 |
| **Get-HDIServices** |取得在 hello 指令碼的執行位置 hello 電腦上執行的 HDInsight 服務的清單。 |
| **Get-HDIService** |Hello 特定 HDInsight 服務的名稱做為輸入，以取得特定服務的詳細的資訊 （服務名稱、 處理序識別碼、 狀態等等） hello hello 指令碼的執行位置的電腦上。 |
| **Get-ServicesRunning** |取得電腦執行 hello hello 指令碼的執行位置的服務清單。 |
| **Get-ServiceRunning** |檢查是否特定服務 （依名稱） 電腦上執行 hello hello 指令碼執行的位置。 |
| **Get-HDIServicesRunning** |取得在 hello 指令碼的執行位置 hello 電腦上執行的 HDInsight 服務的清單。 |
| **Get-HDIServiceRunning** |檢查是否特定的 HDInsight 服務 （依名稱） 電腦上執行 hello hello 指令碼執行的位置。 |
| **Get-HDIHadoopVersion** |取得 hello hello hello 指令碼的執行位置的電腦上安裝的 Hadoop 版本。 |
| **Test-IsHDIHeadNode** |檢查 hello hello 指令碼的執行位置的電腦是否為前端節點。 |
| **Test-IsActiveHDIHeadNode** |檢查 hello hello 指令碼的執行位置的電腦是否為作用中的前端節點。 |
| **Test-IsHDIDataNode** |檢查 hello hello 指令碼的執行位置的電腦是否為資料節點。 |
| **Edit-HDIConfigFile** |編輯 hello 設定檔 hive-site.xml、 core-site.xml、 hdfs-site.xml、 mapred-site.xml 或 yarn-site.xml。 |

## <a name="best-practices-for-script-development"></a>指令碼開發的最佳做法
當您開發的 HDInsight 叢集的自訂指令碼時，有數個最佳作法 tookeep 事項：

* Hello Hadoop 版本檢查

    HDInsight (Hadoop 2.4) 3.1 版和更新版本支援在叢集上使用指令碼動作 tooinstall 自訂元件。 在自訂指令碼，您必須使用 hello **Get HDIHadoopVersion**協助程式方法 toocheck hello Hadoop 版本再繼續執行其他工作 hello 指令碼中。
* 提供穩定連結 tooscript 資源

    使用者應該確定所有 hello 指令碼和用於 hello 自訂叢集的其他成品仍可在整個 hello 叢集的 hello 存留期和 hello 這些檔案的版本，不會變更 hello 持續時間。 需要 hello 重新安裝映像 hello 叢集中的節點時，這些資源是必要的。 hello 最佳作法是 toodownload 和封存 hello 使用者控制項的儲存體帳戶中的所有項目。 這可以是 hello 預設儲存體帳戶或任何 hello 自訂叢集部署的 hello 時間在指定其他儲存體帳戶。
    在 hello Spark 和 R 自訂叢集範例 hello 文件，比方說，我們已經 hello 資源的本機複本中這個儲存體帳戶提供： https://hdiconfigactions.blob.core.windows.net/。
* 確保 hello 叢集自訂指令碼為等冪

    您必須預期之 HDInsight 叢集的 hello 節點建立映像 hello 叢集存留期間。 每當叢集重新安裝映像時，會執行 hello 叢集自訂指令碼。 此指令碼必須是設計的 toobe 等冪 hello 意義上，在重新安裝映像，hello 指令碼應該確定該 hello 叢集就會傳回的 toohello 相同自訂只在 hello 指令碼 hello 叢集是一開始的第一次執行後的狀態建立。 例如，如果自訂的指令碼上安裝應用程式在 D:\AppLocation 第一個執行，然後在每個後續的執行時重新安裝映像，hello 指令碼應該檢查 hello 應用程式是否存在於 hello D:\AppLocation 位置，再繼續進行與其他hello 指令碼中的步驟。
* 在 hello 最佳位置，安裝自訂元件

    叢集節點是映像，hello C:\ 資源磁碟機和 D:\ 系統磁碟機可以重新格式化，進而導致 hello 遺失資料與這些磁碟機已安裝的應用程式。 也會發生此問題如果 hello 叢集一部分的 Azure 虛擬機器 (VM) 節點關閉，且取代為新的節點。 您可以在 hello D:\ 磁碟機上，或在 hello C:\apps 位置 hello 叢集上安裝元件。 會保留在 hello C:\ 磁碟機上的所有其他位置。 指定應用程式庫會安裝在 hello 叢集自訂指令碼的 toobe hello 位置。
* 確保高可用性的 hello 叢集架構

    HDInsight 具有高可用性的主動 / 被動架構，在哪一個前端節點處於現用模式 （hello HDInsight 服務執行所在） 而且 hello 其他前端節點是在待命模式中 （在哪一個 HDInsight 服務未執行）。 如果 HDInsight 服務會中斷主動和被動模式切換 hello 節點。 如果指令碼動作是使用的 tooinstall 服務兩個前端節點上的高可用性，請注意該 hello HDInsight 容錯移轉機制不是能 tooautomatically 失敗這些使用者安裝的服務。 因此使用者安裝高可用性的預期的 toobe HDInsight 前端節點上的服務必須有自己的容錯移轉機制，如果在主動 / 被動模式中，或為主動 / 主動模式中。

    HDInsight 編寫動作的指令碼命令執行兩個前端節點上時指定 hello 前端節點角色 hello 中的值做為*ClusterRoleCollection*參數。 因此，當您設計自訂指令碼時，請確定您的指令碼知道這項設定。 您應該不會發生問題 hello 相同的服務會安裝並啟動這兩個 hello 前端節點上，而且他們最後彼此競爭。 此外，請注意，資料會遺失期間重新安裝映像，因此透過指令碼動作所安裝的軟體具有 toobe 彈性 toosuch 事件。 應用程式應該設計的 toowork 分散到多個節點的高可用性資料。 請注意，最多 1/5 hello 叢集中的節點可以重新安裝映像在 hello 相同的時間。
* 設定 hello 自訂元件 toouse Azure Blob 儲存體

    hello hello 叢集節點安裝的自訂元件可能會有預設組態 toouse Hadoop 分散式檔案系統 (HDFS) 儲存體。 您應該改為變更 hello 組態 toouse Azure Blob 儲存體。 在叢集重新安裝映像，取得格式化 hello HDFS 檔案系統，您就會遺失任何資料儲存在其中。 改用 Azure Blob 儲存體可確保資料保留下來。

## <a name="common-usage-patterns"></a>常見使用模式
此章節提供指引實作某些 hello 常見的使用模式，您可能會遇到撰寫自訂指令碼時。

### <a name="configure-environment-variables"></a>設定環境變數
通常在指令碼動作開發中，您會覺得 hello 需要 tooset 環境變數。 比方說，最可能的案例是當您從外部網站下載二進位檔案、 安裝 hello 在叢集上，並將 hello 其所在安裝的 tooyour 'PATH' 環境變數的位置。 下列程式碼片段的 hello 顯示 tooset 環境變數中的 hello 自訂指令碼的方式。

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

這個陳述式設定環境變數，hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello 值為 'true'，也設定 hello 這個變數 toobe 全機器的範圍。 有時候很重要設定環境變數時，就在 hello 適當範圍-電腦或使用者。 如需設定環境變數的詳細資訊，請參閱[這裡][1]。

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>存取的 toolocations hello 自訂指令碼的儲存位置
使用指令碼 toocustomize 叢集需求 tooeither 是 hello 叢集 hello 預設儲存體帳戶中或在任何其他儲存體帳戶上的公用唯讀容器。 如果您的指令碼會存取位在其他位置的資源這些需要在可公開存取的 toobe (至少公用唯讀)。 例如，您可能想 tooaccess 檔案，並儲存使用 hello SaveFile HDI 命令。

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

在此範例中，您必須確定該 hello 容器儲存體帳戶 'somestorageaccount' 中的 ' somecontainer' 是可公開存取。 否則，hello 指令碼擲回 「 找不到 ' 例外狀況而失敗。

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>傳遞參數 toohello 新增 AzureRmHDInsightScriptAction cmdlet
toopass toohello 新增 AzureRmHDInsightScriptAction cmdlet 多個參數，您需要 tooformat hello 字串值 toocontain 所有參數 hello 指令碼。 例如：

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

或

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>對於失敗的叢集部署擲回例外狀況
如果您想要精確地收到 hello 事實 tooget 通知該叢集自訂失敗如預期般，是重要的 toothrow 例外狀況，並會 hello 叢集建立失敗。 比方說，您可能會想 tooprocess 檔案，如果存在的話，並處理 hello hello 檔案不存在的錯誤情況。 這樣會確保 hello 指令碼會依正常程序結束，且正確已知 hello hello 叢集狀態。 hello 下列程式碼片段會透過範例說明如何 tooachieve 這樣：

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

在此片段中，如果 hello 檔案不存在，它會導致 tooa 處於狀態下 hello 指令碼實際上正常地結束之後列印 hello 錯誤訊息： hello 叢集達到假設它是 「 成功 」 完成叢集的自訂程序的執行狀態。 如果您想要精確地收到 hello 事實 toobe 通知該叢集自訂基本上不成功如預期般，因為遺漏的檔案，為更適當 toothrow 例外狀況，並無法 hello 叢集自訂步驟。 tooachieve 這樣您就必須使用 hello 改為下列範例程式碼片段。

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>指令碼動作的部署檢查清單
準備 toodeploy 這些指令碼時，我們採用的 hello 步驟如下：

1. 將包含 hello 自訂指令碼可在部署期間 hello 叢集節點可存取的位置中的 hello 檔案。 這可以是任何 hello 預設或其他叢集部署中或任何其他可公開存取的儲存體容器的 hello 時間在指定的儲存體帳戶。
2. 加入至指令碼 toomake 確定它們執行不斷地，檢查，以便 hello 指令碼可以在 hello 執行多次相同的節點。
3. 使用 hello **Write-output** Azure PowerShell cmdlet tooprint tooSTDOUT 與 STDERR。 請勿使用 **Write-Host**。
4. 使用暫存檔案資料夾，例如 $env: TEMP tookeep hello hello 指令碼所使用的下載的檔案，然後再清除它們之後執行指令碼。
5. 安裝自訂軟體，位置只能是 D:\ 或 C:\apps。 因為它們是保留，不應該使用 hello c： 磁碟機上的其他位置。 請注意，安裝 hello C:\apps 資料夾外部的 hello c： 磁碟機上的檔案可能會導致安裝程式失敗 reimages hello 節點的期間。
6. 萬一 hello 作業系統層級的設定或 Hadoop 服務組態檔已變更，您可能想 toorestart HDInsight 服務，讓他們可以選擇任何作業系統層級的設定，例如 hello hello 指令碼中設定的環境變數。

## <a name="debug-custom-scripts"></a>偵錯自訂指令碼
儲存 hello 指令碼錯誤記錄檔，以及其他輸出，您指定在其建立 hello 叢集的 hello 預設儲存體帳戶中。 hello 記錄檔會儲存在資料表中具有 hello 名稱*u < \cluster-name-fragment >< \time-stamp > setuplog*。 這些是彙總從 hello 節點 （前端節點和背景工作角色節點） 上的 hello 指令碼執行於 hello 叢集中的所有記錄的記錄檔。
輕鬆 toocheck hello 記錄檔也 toouse HDInsight Tools for Visual Studio。 安裝 hello 工具，請參閱[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**使用 Visual Studio toocheck hello 記錄**

1. 開啟 Visual Studio。
2. 按一下 檢視，然後按一下伺服器總管。
3. 以滑鼠右鍵按一下"Azure"、 按一下 連線太**Microsoft Azure 訂用帳戶**，然後輸入您的認證。
4. 展開**儲存體**，依序展開 hello Azure 儲存體帳戶做為 hello 預設的檔案系統**資料表**，然後按兩下 hello 資料表名稱。

您可以從也遠端存取 hello 叢集節點 toosee STDOUT 和 STDERR 的自訂指令碼。 hello 記錄每個節點上的已指定唯一的 toothat 節點，並登入**C:\HDInsightLogs\DeploymentAgent.log**。 這些記錄檔記錄從 hello 自訂指令碼的所有輸出。 Spark 指令碼動作的範例記錄程式碼片段看起來像這樣：

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


此記錄檔，並明確 hello 名為 HEADNODE0 VM 已執行 hello Spark 指令碼動作和 hello 執行期間所擲回任何例外狀況。

Hello 執行失敗，就會發生的事件，在描述它 hello 輸出也包含在此記錄檔。 提供這些記錄檔中的 hello 資訊應在偵錯指令碼可能發生的問題很有幫助。

## <a name="see-also"></a>另請參閱
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]
* [在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]
* [在 HDInsight 叢集上安裝和使用 R][hdinsight-r-scripts]
* [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。
* [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
