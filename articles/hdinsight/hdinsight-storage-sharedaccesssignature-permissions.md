---
title: "使用共用存取簽章-Azure HDInsight aaaRestrict 存取 |Microsoft 文件"
description: "了解如何 toouse 共用存取簽章 toorestrict HDInsight 存取 toodata 儲存在 Azure 儲存體 blob。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata HDInsight 中

HDInsight 具有完整存取 toodata hello 與 hello 叢集相關聯的 Azure 儲存體帳戶中。 您可以使用共用存取簽章 hello blob 容器 toorestrict 存取 toohello 資料上。 例如，tooprovide 唯讀存取 toohello 資料。 共用存取簽章 (SAS) 是 Azure 儲存體帳戶的功能，可讓您 toolimit 存取 toodata。 例如，提供唯讀存取 toodata。

> [!IMPORTANT]
> 對於使用 Apache Ranger 的解決方案，請考慮使用已加入網域的 HDInsight。 如需詳細資訊，請參閱 hello[設定已加入網域的 HDInsight](hdinsight-domain-joined-configure.md)文件。

> [!WARNING]
> HDInsight 必須 hello 叢集的完整存取 toohello 預設儲存體。

## <a name="requirements"></a>需求

* Azure 訂用帳戶
* C# 或 Python。 提供 C# 範例程式碼做為 Visual Studio 解決方案。

  * Visual Studio 的版本必須是 2013、2015 或 2017
  * Python 的版本必須是 2.7 或更新版本

* 以 Linux 為基礎的 HDInsight 叢集或者[Azure PowerShell] [ powershell] -如果您有現有以 Linux 為基礎的叢集，您可以使用 Ambari tooadd 共用存取簽章 toohello 叢集。 如果沒有，您可以使用 Azure PowerShell toocreate 叢集，並在叢集建立期間新增共用存取簽章。

    > [!IMPORTANT]
    > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* hello 範例檔案，從[https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature)。 這個儲存機制包含下列項目 hello:

  * Visual Studio 專案，可以建立儲存體容器、預存原則，以及搭配 HDInsight 使用的 SAS
  * Python 指令碼，可以建立儲存體容器、預存原則，以及搭配 HDInsight 使用的 SAS
  * PowerShell 指令碼可建立 HDInsight 叢集，並將它設定 toouse hello SAS。

## <a name="shared-access-signatures"></a>共用存取簽章

共用存取簽章有兩種格式：

* 臨機操作： hello 開始時間、 到期時間和 hello SAS 會指定在 hello SAS URI 的權限。

* 預存存取原則：預存存取原則會在資源容器中定義，例如 Blob 容器。 原則可以在一或多個共用的存取簽章使用的 toomanage 條件約束。 當您建立 SAS 關聯與預存的存取原則時，hello SAS 繼承 hello 的條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。

hello hello 兩個形式之間的差異是很重要的一個重要的案例： 撤銷。 SAS 是 URL，因此會取得 hello SAS 的任何人可以使用它，不論要求者 toobegin 與。 如果已公開發行 SAS，才能使用 hello 世界中的任何人。 散佈的 SAS 在發生以下四個情況其中之一之前都會持續有效：

1. hello 上 hello SAS 達到指定的到期時間。

2. hello hello 達到 SAS 所參考的 hello 預存存取原則中指定的到期時間。 hello 下列案例會造成 hello 到期時間達到 toobe:

    * hello 時間間隔已經耗盡時。
    * hello 預存存取原則是修改的 toohave hello 過去在到期時間。 變更 hello 到期時間是一種方式 toorevoke hello SAS。

3. hello 預存存取原則參考的 hello SAS 遭到刪除，也就是另一個方式 toorevoke hello SAS。 如果您重新建立 hello 預存存取原則，以名稱相同，為所有的 SAS 權杖的 hello hello 先前原則都有效 （如果尚未超過 SAS hello hello 上的到期時間）。 如果您想 toorevoke hello SAS，是確定 toouse 不同名稱，如果您重新建立與到期時間在未來的 hello hello 存取原則。

4. 重新產生已使用的 toocreate hello SAS 的 hello 帳戶金鑰。 重新產生 hello 金鑰會導致使用 hello 前一個索引鍵 toofail 驗證的所有應用程式。 更新所有元件 toohello 新機碼。

> [!IMPORTANT]
> 共用的存取簽章 URI 都與 hello 帳戶金鑰的使用的 toocreate hello 簽章，與 hello 預存的存取原則 （如果有的話）。 如果未不指定任何預存的存取原則，則 hello 只方式 toorevoke 共用的存取簽章是 toochange hello 帳戶金鑰。

建議您一律使用預存的存取原則。 使用預存的原則，您可以撤銷簽章，或視需要擴充 hello 到期日。 本文件中的 hello 步驟會使用預存的存取原則 toogenerate SAS。

如需有關共用存取簽章的詳細資訊，請參閱[了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

### <a name="create-a-stored-policy-and-sas-using-c"></a>使用 C\# 建立預存原則和 SAS

1. 開啟 Visual Studio 中的 hello 方案。

2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **SASToken**專案，然後選取**屬性**。

3. 選取**設定**並新增值 hello 下列項目：

   * StorageConnectionString: hello 連接字串 hello 儲存體帳戶的 toocreate 儲存的原則和 SAS。 hello 格式應該是`DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey`其中`myaccount`hello 儲存體帳戶名稱和`mykey`是 hello hello 儲存體帳戶金鑰。

   * ContainerName: hello hello 您想要 toorestrict 存取的儲存體帳戶中的容器。

   * SASPolicyName: hello 的 hello 名稱 toouse 儲存原則 toocreate。

   * FileToUpload: hello 路徑 tooa 檔案上傳的 toohello 容器。

4. 執行 hello 專案。 一旦產生 hello SAS，就會顯示下列文字的資訊類似 toohello:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    儲存 hello SAS 原則權杖、 儲存體帳戶名稱，以及容器名稱。 建立 hello 儲存體帳戶與您的 HDInsight 叢集的關聯時，會使用這些值。

### <a name="create-a-stored-policy-and-sas-using-python"></a>使用 Python 建立預存原則和 SAS

1. 開啟 hello SASToken.py 檔案並變更下列值的 hello:

   * 原則\_名稱： hello 的 hello 名稱 toouse 儲存原則 toocreate。

   * 儲存體\_帳戶\_名稱： hello 您的儲存體帳戶名稱。

   * 儲存體\_帳戶\_金鑰： hello hello 儲存體帳戶金鑰。

   * 儲存體\_容器\_名稱： hello 您想要 toorestrict 存取的儲存體帳戶中的 hello 容器。

   * 範例\_檔案\_路徑： hello 路徑 tooa 檔案上傳的 toohello 容器。

2. 執行 hello 指令碼。 它會顯示 hello SAS 權杖類似 toohello hello 指令碼完成時，下列文字：

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    儲存 hello SAS 原則權杖、 儲存體帳戶名稱，以及容器名稱。 建立 hello 儲存體帳戶與您的 HDInsight 叢集的關聯時，會使用這些值。

## <a name="use-hello-sas-with-hdinsight"></a>使用 hello SAS 與 HDInsight

在建立 HDInsight 叢集時，您必須指定主要儲存體帳戶，您可以選擇性地指定其他儲存體帳戶。 這兩種方法的新增儲存體需要完整存取 toohello 儲存體帳戶和可用的容器。

toouse 共用存取簽章 toolimit 存取 tooa 容器，將自訂項目 toohello**核心站台**hello 叢集組態。

* 如**windows**或**linux** HDInsight 叢集，您可以使用 PowerShell 的叢集建立期間新增 hello 項目。
* 如**linux** HDInsight 叢集，變更後使用 Ambari 叢集建立的 hello 組態。

### <a name="create-a-cluster-that-uses-hello-sas"></a>建立使用 hello SAS 的叢集

SAS 隨附於 hello 該使用 hello 建立 HDInsight 叢集的範例`CreateCluster`hello 儲存機制的目錄。 toouse 它使用 hello 下列步驟：

1. 開啟 hello`CreateCluster\HDInsightSAS.ps1`檔案文字編輯器中，並修改 hello hello hello 從文件開頭的值。

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    例如，變更`'mycluster'`toohello 名稱要 toocreate 的 hello 叢集。 建立儲存體帳戶和 SAS 權杖時，hello SAS 值應該符合 hello hello 先前步驟中的值。

    一旦您已變更 hello 值，將儲存 hello 檔案。

2. 開啟新的 Azure PowerShell 提示字元。 如果您不熟悉或尚未安裝 Azure PowerShell，請參閱[安裝和設定 Azure PowerShell][powershell]。

1. 從 hello 提示字元中，使用下列命令 tooauthenticate tooyour Azure 訂用帳戶的 hello:

    ```powershell
    Login-AzureRmAccount
    ```

    出現提示時，帳戶登入 hello Azure 訂用帳戶。

    如果您的帳戶與多個 Azure 訂用帳戶相關聯，您可能需要 toouse`Select-AzureRmSubscription`想 toouse tooselect hello 訂用帳戶。

4. Hello 提示字元中，變更目錄 toohello `CreateCluster` hello HDInsightSAS.ps1 檔所在目錄。 然後使用下列命令 toorun hello 指令碼的 hello

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Hello 指令碼執行，就會記錄輸出 toohello PowerShell 命令提示字元，會在建立 hello 資源群組和儲存體帳戶。 您會提示的 tooenter hello HTTP 使用者 hello HDInsight 叢集。 此帳戶是使用的 toosecure HTTP/s 存取 toohello 叢集。

    如果您是建立以 Linux 為基礎的叢集，系統會提示您輸入 SSH 使用者帳戶名稱和密碼。 此帳戶是使用的 tooremotely toohello 叢集中的記錄檔。

   > [!IMPORTANT]
   > 出現提示時輸入 hello HTTP/s 或 SSH 使用者名稱和密碼，您必須提供符合下列準則的 hello 的密碼：
   >
   > * 長度必須小於 10 個字元
   > * 必須包含至少一個數字
   > * 必須包含至少一個非英數字元
   > * 必須包含至少一個大寫或小寫字元

它需要一些時間此指令碼 toocomplete，通常大約 15 分鐘。 Hello 指令碼完成時沒有發生任何錯誤，已建立 hello 叢集。

### <a name="use-hello-sas-with-an-existing-cluster"></a>現有的叢集中使用 hello SAS

如果您有現有以 Linux 為基礎的叢集，您可以加入 hello SAS toohello**核心站台**組態使用 hello 下列步驟：

1. 開啟您的叢集，hello Ambari web UI。 此頁面的 hello 位址是 https://YOURCLUSTERNAME.azurehdinsight.net。 出現提示時，驗證使用 hello 管理員名稱 （管理員） toohello 叢集和建立 hello 叢集時使用的密碼。

2. Hello hello Ambari web UI 的左方，從選取**HDFS** ，然後選取 hello **Configs** hello 中間的 hello 頁面 索引標籤。

3. 選取 hello**進階**索引標籤，然後再向下捲動直到您找到 hello**自訂的核心站台**> 一節。

4. 展開 hello**自訂的核心站台** 區段中，然後捲動 toohello 結束作業，並選取 hello**加入屬性...**連結。 使用 hello 下列值 hello**金鑰**和**值**欄位：

   * **金鑰**：fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **值**: hello hello 先前執行的 C# 或 Python 應用程式所傳回的 SAS

     取代**CONTAINERNAME** hello 容器名稱與您用於 hello C# 或 SAS 的應用程式。 取代**STORAGEACCOUNTNAME** hello 您所使用的儲存體帳戶名稱。

5. 按一下 hello**新增**按鈕 toosave 此索引鍵和值，然後按一下 hello**儲存**按鈕 toosave hello 組態變更。 出現提示時，新增 hello 變更 （「 新增 SAS 存放裝置存取 」，例如） 的描述，然後再按**儲存**。

    按一下**確定**hello 變更都完成時。

   > [!IMPORTANT]
   > Hello 變更生效之前，您必須重新啟動數個服務。

6. Hello Ambari web UI，在選取**HDFS** hello 清單 hello 左、，然後選取從**重新啟動所有**從 hello**服務動作**下拉式清單上 hello 右邊的清單。 出現提示時，選取 [開啟維護模式]，然後選取 [確認全部重新啟動]。

    對 MapReduce2 和 YARN 重複此程序。

7. Hello 服務已重新啟動後，選取每個和停用維護模式，從 hello**服務動作**下拉式清單。

## <a name="test-restricted-access"></a>測試限制的存取

您已限制的 tooverify 存取，請使用下列方法的 hello:

* 如**windows** HDInsight 叢集，使用遠端桌面 tooconnect toohello 叢集。 如需詳細資訊，請參閱[連接使用 RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。

    一旦連接之後，使用 hello **Hadoop 命令列**hello 桌面 tooopen 命令提示字元上的圖示。

* 如**linux** HDInsight 叢集使用 SSH tooconnect toohello 叢集。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

一旦連接之後 toohello 叢集，使用下列步驟 tooverify，您可以在 hello SAS 儲存體帳戶只有讀取和清單的項目 hello:

1. hello 容器 toolist hello 內容使用 hello hello 提示字元中的下列命令： 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    取代**SASCONTAINER** hello hello 容器建立 hello SAS 儲存體帳戶名稱。 取代**SASACCOUNTNAME** hello hello hello SA 所使用的儲存體帳戶的名稱。

    hello 清單包含 hello 檔案上傳時已建立 hello 容器和 SAS。

2. 使用下列命令，您可以讀取 hello hello 檔案內容的 tooverify hello。 取代 hello **SASCONTAINER**和**SASACCOUNTNAME**如同 hello 前一個步驟。 取代**FILENAME** hello 顯示 hello 先前命令中的 hello 檔名稱：

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    此命令會列出 hello hello 檔案內容。

3. 使用下列命令 toodownload hello 檔案 toohello 本機檔案系統的 hello:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    此命令下載 hello tooa 本機檔案命名為**testfile.txt**。

4. 使用 hello 下列命令 tooupload hello 本機檔案 tooa 名為新檔案**testupload.txt** hello SAS 存放裝置上：

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    您會收到訊息的類似 toohello，下列文字：

        put: java.io.IOException

    因為 hello 儲存位置讀取 + 清單只會發生此錯誤。 使用下列命令 tooput hello 資料 hello hello 叢集中，這是可寫入的預設儲存體上的 hello:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    這次 hello 作業應該順利完成。

## <a name="troubleshooting"></a>疑難排解

### <a name="a-task-was-canceled"></a>已取消工作

**徵兆**： 建立使用 hello PowerShell 指令碼的叢集，您可能會收到下列錯誤訊息的 hello:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**可能的原因**： 如果您使用的密碼 hello admin/HTTP 使用者 hello 叢集，或 （適用於以 Linux 為基礎的叢集），會發生此錯誤 hello SSH 使用者。

**解析**： 使用符合下列準則的 hello 的密碼：

* 長度必須小於 10 個字元
* 必須包含至少一個數字
* 必須包含至少一個非英數字元
* 必須包含至少一個大寫或小寫字元

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 tooadd 限制存取儲存體 tooyour HDInsight 叢集，了解您的叢集上的資料與其他方式 toowork:

* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
