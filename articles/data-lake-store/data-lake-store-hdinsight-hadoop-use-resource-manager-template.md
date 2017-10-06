---
title: "aaaUse Azure 範本 toocreate HDInsight 及資料湖存放區 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toocreate 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本來建立搭配 Data Lake Store 的 HDInsight 叢集
> [!div class="op_single_selector"]
> * [使用入口網站](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [使用 PowerShell (針對預設儲存體)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [使用 PowerShell (針對額外儲存體)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [使用 Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

了解如何 toouse Azure PowerShell tooconfigure 在 HDInsight 叢集與 Azure 資料湖存放區**做為額外的儲存體**。

Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。 資料湖存放區是作為額外的存放裝置，hello hello 叢集的預設儲存體帳戶仍會 Azure 儲存體 Blob (WASB) 和受 hello 叢集相關的檔案 （例如記錄檔等） 仍會寫入 toohello 預設儲存體，hello 資料時，您想 tooprocess 可以儲存在 Data Lake Store 帳戶。 使用資料湖存放區做為額外的儲存體帳戶不會影響效能或 hello 能力 tooread/寫入 toohello 叢集中存放裝置 hello。

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>針對 HDInsight 叢集儲存體使用 Data Lake Store

以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：

* 選項 toocreate HDInsight 叢集，以存取做為預設儲存體 tooData Lake Store 適用於 HDInsight 版本 3.5 和 3.6。

* 選項 toocreate HDInsight 叢集的存取是適用於 HDInsight 版本 3.2、 3.4、 3.5 和 3.6 tooData 湖存放區做為額外的存放裝置。

在本文中，我們佈建 Hadoop 叢集與 Data Lake Store 做為額外的儲存體。 如需有關如何 toocreate Hadoop 叢集做為預設儲存體的資料湖存放區的指示，請參閱[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更新版本**。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* **Azure Active Directory 服務主體**。 本教學課程步驟提供如何指示 toocreate Azure AD 中的服務主體。 不過，您必須是 Azure AD 管理員 toobe 無法 toocreate 服務主體。 如果您是 Azure AD 管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。

    **如果您不是 Azure AD 管理員**，就能 tooperform hello 步驟需要的 toocreate 服務主體。 在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。 此外，hello 服務主體必須建立使用的認證，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>建立搭配 Azure Data Lake Store 的 HDInsight 叢集
hello Resource Manager 範本，並使用 hello 範本 hello 必要條件可用在 GitHub 上[部署新的 Data Lake Store 的 HDInsight Linux 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)。 請遵循隨附於此連結 toocreate 的 HDInsight 叢集為 hello 額外的儲存體的 Azure Data Lake Store 的 hello 指示。

在上述的 hello 連結 hello 指示需要 PowerShell。 您開始使用這些指示之前，請確定您登入 tooyour Azure 帳戶。 從您的桌面，開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段的 hello。 當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶 admininistrators/擁有者：

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>上傳範例資料 toohello Azure Data Lake Store
hello Resource Manager 範本建立新的 Data Lake Store 帳戶，並將其與 hello HDInsight 叢集相關聯。 現在，您必須上傳某些範例資料 toohello 資料湖存放區。 您將需要這項資料稍後從 HDInsight 叢集 hello 教學課程 toorun 作業，存取 hello 資料湖存放區中的資料。 如需有關指示 tooupload 資料，請參閱 <<c0> [ 上傳檔案 tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata)。 如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)。

## <a name="set-relevant-acls-on-hello-sample-data"></a>Hello 範例資料設定相關的 Acl
toomake 確認可從 hello HDInsight 叢集存取您上傳的 hello 範例資料，您必須確定是使用的 tooestablish hello HDInsight 叢集與資料湖存放區之間的身分識別的 hello Azure AD 應用程式具有存取 toohello 檔案/資料夾嘗試 tooaccess。 toodo，執行下列步驟的 hello。

1. 尋找 hello 的 hello 與 HDInsight 叢集相關聯的 Azure AD 應用程式和 hello 資料湖存放區的名稱。 其中一種方式 toolook hello 名稱是 tooopen hello HDInsight 叢集刀鋒視窗使用 hello Resource Manager 範本所建立，請按一下 hello**叢集 AAD 身分識別**索引標籤，然後尋找 hello 值**服務主體顯示名稱**。
2. 現在，提供存取 toothis Azure AD 應用程式上 hello 檔案/資料夾的 tooaccess 從 hello HDInsight 叢集。 tooset hello 右邊 Acl hello 檔案/資料夾資料湖存放區中，請參閱[保護資料湖存放區中的資料](data-lake-store-secure-data.md#filepermissions)。

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Hello HDInsight 叢集 toouse hello 資料湖存放區上執行測試工作
您已設定的 HDInsight 叢集之後，您可以測試工作上執行 hello 叢集 tootest 該 hello HDInsight 叢集可以存取資料湖存放區。 toodo 因此，我們會執行使用您上傳先前 tooyour Data Lake Store 的 hello 範例資料建立資料表的範例 Hive 工作。

本節中您將 SSH 成 HDInsight Linux 叢集和執行的 hello 範例 Hive 查詢。 如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。

如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。

1. 一旦連接之後，請使用下列命令的 hello 啟動 hello Hive CLI:

   ```
   hive
   ```
2. 使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello**車輛**利用 hello 資料湖存放區中的 hello 範例資料：

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   您應該會看到類似 toohello 下列輸出：

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>使用 HDFS 命令存取 Data Lake Store
一旦您已設定 hello HDInsight 叢集 toouse 資料湖存放區，您可以使用 hello HDFS 殼層命令 tooaccess hello 存放區。

本節中您將 SSH 成 HDInsight Linux 叢集和執行的 hello HDFS 命令。 如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。

如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。

一旦連接之後，請使用下列 HDFS 檔案系統命令 toolist hello 檔案 hello 資料湖存放區中的 hello。

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

這應該會列出您上傳先前 toohello Data Lake Store 的 hello 檔案。

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 toohello 資料湖存放區，然後再使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。


## <a name="next-steps"></a>後續步驟
* [從 Azure 儲存體 Blob tooData 湖存放區複製資料](data-lake-store-copy-data-wasb-distcp.md)
