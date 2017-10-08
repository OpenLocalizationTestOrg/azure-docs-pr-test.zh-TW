---
標題： aaa"PowerShell： 為附加元件的存放裝置的資料湖存放區與 Azure HDInsight 叢集 |Microsoft 文件 」 服務： 資料湖存放，hdinsight documentationcenter: ' 作者： nitinme 管理員： jhubbard 編輯器： cgronlun

ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service： 資料湖存放區 ms.devlang: na ms.topic： 文章 ms.tgt_pltfrm: na ms.workload： 巨量資料 ms.date: 06/08/2017 ms.author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Data Lake Store 的 HDInsight 叢集的 Azure PowerShell toocreate 使用 （做為額外的存放裝置）
> [!div class="op_single_selector"]
> * [使用入口網站](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [使用 PowerShell (針對預設儲存體)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [使用 PowerShell (針對額外儲存體)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [使用 Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

了解如何 toouse Azure PowerShell tooconfigure 在 HDInsight 叢集與 Azure 資料湖存放區**做為額外的儲存體**。 如需有關如何 toocreate 在 HDInsight 叢集做為預設儲存體的 Azure Data Lake Store 的指示，請參閱[建立為預設的存放裝置的 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)。

> [!NOTE]
> 如果您正在 toouse Azure Data Lake Store 為 HDInsight 叢集的其他存放裝置中，我們強烈建議您採用這種這篇文章中所述，建立 hello 叢集時。 將 Azure Data Lake Store 新增額外的儲存體 tooan 為現有 HDInsight 叢集是複雜的程序和 tooerrors 容易出錯。
>

Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。 資料湖存放區是作為額外的存放裝置，hello hello 叢集的預設儲存體帳戶仍會 Azure 儲存體 Blob (WASB) 和受 hello 叢集相關的檔案 （例如記錄檔等） 仍會寫入 toohello 預設儲存體，hello 資料時，您想 tooprocess 可以儲存在 Data Lake Store 帳戶。 使用資料湖存放區做為額外的儲存體帳戶不會影響效能或 hello 能力 tooread/寫入 toohello 叢集中存放裝置 hello。

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>針對 HDInsight 叢集儲存體使用 Data Lake Store

以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：

* 選項 toocreate HDInsight 叢集的存取是適用於 HDInsight 版本 3.2、 3.4、 3.5 和 3.6 tooData 湖存放區做為額外的存放裝置。

設定 HDInsight toowork 與使用 PowerShell 的資料湖存放區會包含 hello 下列步驟：

* 建立 Azure Data Lake Store
* 設定以角色為基礎的驗證存取 tooData 湖存放區
* 建立與驗證 tooData Lake Store 的 HDInsight 叢集
* Hello 叢集上執行測試工作

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更新版本**。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* **Windows SDK**。 您可以從[這裡](https://dev.windows.com/en-us/downloads)安裝它。 您使用此 toocreate 安全性憑證。
* **Azure Active Directory 服務主體**。 本教學課程步驟提供如何指示 toocreate Azure AD 中的服務主體。 不過，您必須是 Azure AD 管理員 toobe 無法 toocreate 服務主體。 如果您是 Azure AD 管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。

    **如果您不是 Azure AD 管理員**，就能 tooperform hello 步驟需要的 toocreate 服務主體。 在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。 此外，hello 服務主體必須建立使用的認證，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。

## <a name="create-an-azure-data-lake-store"></a>建立 Azure Data Lake Store
請遵循這些步驟 toocreate 資料湖存放區。

1. 從您的桌面，開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段的 hello。 當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶管理員/擁有者：

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > 如果您收到類似的錯誤太`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`當註冊 hello 資料湖存放區資源提供者，您就可以確認您的訂用帳戶不是在 Azure Data Lake Store 的允許清單。 請遵循這些 [指示](data-lake-store-get-started-portal.md)，確保您會啟用 Azure 訂用帳戶來使用 Data Lake Store 公開預覽版。
   >
   >
2. Azure Data Lake Store 帳戶與 Azure 資源群組相關聯。 從建立 Azure 資源群組開始。

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    您應該會看到如下的輸出：

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. 建立 Azure Data Lake Store 帳戶。 您指定的名稱只能包含小寫字母和數字的 hello 帳戶。

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    您應該會看到類似 hello 下列輸出：

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. 上傳某些範例資料 tooAzure Data Lake。 我們會使用它在 hello 資料是從 HDInsight 叢集，您可存取此文件 tooverify 稍後。 如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)。

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>設定以角色為基礎的驗證存取 tooData 湖存放區
每一個 Azure 訂用帳戶都與 Azure Active Directory 相關聯。 使用者和服務存取 hello 訂用帳戶使用 hello Azure 傳統入口網站或 Azure 資源管理員 API 的資源，必須先通過驗證 Azure Active Directory。 已授與存取 tooAzure 訂閱和服務由將其指派 hello Azure 資源上的適當角色。  為服務，服務主體識別 hello Azure Active Directory (AAD) 中的 hello 服務。 本節說明 toogrant 應用程式的服務方式，例如 HDInsight，存取 tooan Azure 資源 (您先前建立的 Azure Data Lake Store 帳戶 hello) 藉由建立 hello 應用程式的服務主體，並指派透過 Azure 角色 toothatPowerShell。

設定 Active Directory 驗證的 Azure 資料湖 tooset，您必須執行下列工作的 hello。

* 建立自我簽署憑證
* 在 Azure Active Directory 和服務主體中建立應用程式

### <a name="create-a-self-signed-certificate"></a>建立自我簽署憑證
請確定您有[Windows SDK](https://dev.windows.com/en-us/downloads) hello 進行這一節的步驟之前安裝。 您必須也建立目錄，例如**C:\mycertdir**、 建立 hello 憑證的位置。

1. 從 hello PowerShell 視窗中，瀏覽 toohello 安裝 Windows SDK 的位置 (通常`C:\Program Files (x86)\Windows Kits\10\bin\x86`並用 hello [MakeCert] [ makecert]公用程式 toocreate 自我簽署憑證和私用的索引鍵。 使用下列命令的 hello。

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    系統會提示的 tooenter hello 私密金鑰密碼。 Hello 命令執行成功，您應該會看到之後**CertFile.cer**和**mykey.pvk**您指定的 hello 憑證目錄中。
2. 使用 hello [Pvk2Pfx] [ pvk2pfx]公用程式 tooconvert hello.pvk 和.cer 檔案 MakeCert 建立的 tooa.pfx 檔案。 執行下列命令的 hello。

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    出現提示時輸入 hello 私密金鑰密碼您稍早指定。 hello 指定 hello 值**po**參數是 hello 與 hello.pfx 檔相關聯的密碼。 Hello 命令成功完成後，您也應該會看到 CertFile.pfx 您指定的 hello 憑證目錄中。

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>建立 Azure Active Directory 和服務主體
在本節中，您的 Azure Active Directory 應用程式執行 hello 步驟 toocreate 服務主體、 指派角色 toohello 服務主體，以及 hello 服務主體以驗證所提供的憑證。 Azure Active Directory 中執行下列命令 toocreate hello 應用程式。

1. 貼上下列指令程式 hello PowerShell 主控台視窗中的 hello。 確定您指定 hello 的 hello 值**-DisplayName**屬性是唯一的。 此外，hello 值**-首頁**和**-IdentiferUris**預留位置值，並不會驗證。

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. 建立服務主體使用 hello 應用程式識別碼。

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. 授與 hello 服務主體存取 toohello Data Lake Store 資料夾和您將從 hello HDInsight 叢集存取的 hello 檔案。 hello 以下程式碼片段提供存取 toohello 根目錄的 hello Data Lake Store 帳戶 （您複製 hello 範例資料檔），並 hello 檔案本身。

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>建立 HDInsight Linux 叢集搭配 Data Lake Store 做為額外儲存體

在本節中，我們會建立一個 HDInsight Hadoop Linux 叢集搭配 Data Lake Store 做為額外儲存體。 此版本中，hello HDInsight 叢集與 hello 資料湖存放區必須在 hello 相同的位置。

1. 開始擷取 hello 訂用帳戶的租用戶識別碼。 稍後您將會需要此資訊。

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. 此版本中，Hadoop 叢集中，資料湖存放區可以只當做額外的存放裝置 hello 叢集。 hello 預設儲存體仍會 hello Azure 儲存體 blob (WASB)。 因此，我們將先建立 hello hello 叢集所需的儲存體帳戶和儲存體容器。

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. 建立 hello HDInsight 叢集。 使用下列 cmdlet 的 hello。

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Hello cmdlet 順利完成之後，您應該會看到列出 hello 叢集詳細資料的輸出。


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Hello HDInsight 叢集 toouse hello 資料湖存放區上執行測試工作
您已設定的 HDInsight 叢集之後，您可以測試工作上執行 hello 叢集 tootest 該 hello HDInsight 叢集可以存取資料湖存放區。 toodo 因此，我們會執行使用您上傳先前 tooyour Data Lake Store 的 hello 範例資料建立資料表的範例 Hive 工作。

在本節中，您可以將 SSH 到 hello HDInsight Linux 叢集您建立及執行 hello 範例 Hive 查詢。

* 如果您使用 Windows 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. 一旦連接之後，請使用下列命令的 hello 啟動 hello Hive CLI:

        hive
2. 使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello**車輛**利用 hello 資料湖存放區中的 hello 範例資料：

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    您應該會看到類似 toohello 下列輸出：

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

## <a name="access-data-lake-store-using-hdfs-commands"></a>使用 HDFS 命令存取 Data Lake Store
一旦您已設定 hello HDInsight 叢集 toouse 資料湖存放區，您可以使用 hello HDFS 殼層命令 tooaccess hello 存放區。

在本節中，您可以將 SSH 到 hello HDInsight Linux 叢集您建立及執行 hello HDFS 命令。

* 如果您使用 Windows 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端 tooSSH 到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

一旦連接之後，請使用下列 HDFS 檔案系統命令 toolist hello 檔案 hello 資料湖存放區中的 hello。

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

這應該會列出您上傳先前 toohello Data Lake Store 的 hello 檔案。

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 toohello 資料湖存放區，然後再使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。

## <a name="see-also"></a>另請參閱
* [入口網站： 建立 HDInsight 叢集 toouse 資料湖存放區](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
