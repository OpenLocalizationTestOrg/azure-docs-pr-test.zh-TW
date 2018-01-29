---
title: "PowerShell：Azure HDInsight 叢集搭配 Data Lake Store 做為附加儲存體 | Microsoft Docs"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/01/2017
ms.author: nitinme
ms.openlocfilehash: dc46e3987f3710bc73ef13a2c195b68f78bd104d
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>使用 Azure PowerShell 建立 HDInsight 叢集搭配 Data Lake Store (做為附加儲存體)
> [!div class="op_single_selector"]
> * [使用入口網站](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [使用 PowerShell (針對預設儲存體)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [使用 PowerShell (針對額外儲存體)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [使用 Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

了解如何使用 Azure PowerShell 將搭配 Azure Data Lake Store 的 HDInsight 叢集設定為**額外儲存體**。 如需有關如何建立具 Azure Data Lake Store 的 HDInsight 叢集做為預設儲存體的指示，請參閱[建立具有 Data Lake Store 的 HDInsight 叢集做為預設儲存體](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)。

> [!NOTE]
> 如果您即將使用 Azure Data Lake Store 作為 HDInsight 叢集的額外儲存體，強烈建議您如本文所述建立叢集時執行此作業。 將 Azure Data Lake Store 新增為現有 HDInsight 叢集的額外儲存體是很複雜的程序，很容易出錯。
>

Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。 當 Data Lake Store 做為額外儲存體時，叢集的預設儲存體帳戶仍然是 Azure 儲存體 Blob (WASB)，叢集相關的檔案 (例如記錄檔等) 仍然會寫入預設儲存體，而您想要處理的資料會儲存於 Data Lake Store 帳戶中。 使用 Data Lake Store 做為其他儲存體帳戶，不會影響效能或從叢集讀取/寫入至儲存體的能力。

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>針對 HDInsight 叢集儲存體使用 Data Lake Store

以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：

* HDInsight 3.2、3.4、3.5 和 3.6 版提供建立可存取 Data Lake Store 作為額外儲存體之 HDInsight 叢集的選項。

使用 PowerShell 以設定 HDInsight 來搭配 Data Lake Store 使用，包含下列步驟：

* 建立 Azure Data Lake Store
* 設定 Data Lake Store 以角色為基礎的存取的驗證
* 建立具有 Data Lake Store 驗證的 HDInsight 叢集
* 在叢集上執行測試工作

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備下列條件：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更新版本**。 請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。
* **Windows SDK**。 您可以從[這裡](https://dev.windows.com/en-us/downloads)安裝它。 您使用它來建立安全性憑證。
* **Azure Active Directory 服務主體**。 本教學課程中的步驟提供有關如何在 Azure AD 中建立服務主體的指示。 不過，您必須是 Azure AD 系統管理員，才能建立服務主體。 如果您是 Azure AD 系統管理員，您就可以略過這項先決條件並繼續進行本教學課程。

    **如果您不是 Azure AD 系統管理員**，您將無法執行建立服務主體所需的步驟。 在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。 此外，必須使用憑證來建立服務主體，如[使用憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)所述。

## <a name="create-an-azure-data-lake-store"></a>建立 Azure Data Lake Store
依照這些步驟建立 Data Lake Store。

1. 從您的桌面開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段。 系統提示您登入時，請確定您使用其中一個訂用帳戶管理員/擁有者身分登入：

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > 如果您在註冊 Data Lake Store 的資源提供者時收到類似 `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` 的錯誤，可能表示您的訂用帳戶不在 Azure Data Lake Store 的允許清單中。 請遵循這些 [指示](data-lake-store-get-started-portal.md)，確保您會啟用 Azure 訂用帳戶來使用 Data Lake Store 公開預覽版。
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

3. 建立 Azure Data Lake Store 帳戶。 您指定的帳戶名稱必須只包含小寫字母和數字。

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    您應該會看到如下的輸出：

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

5. 將一些範例資料上傳至 Azure Data Lake。 我們將在本文稍後使用這個項目來確認資料可以從 HDInsight 叢集存取。 如果您正在尋找一些可上傳的範例資料，您可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a>設定 Data Lake Store 以角色為基礎的存取的驗證
每一個 Azure 訂用帳戶都與 Azure Active Directory 相關聯。 透過 Azure 入口網站或 Azure Resource Manager API 來存取訂用帳戶資源的使用者與服務，都必須先向 Azure Active Directory 進行驗證。 您可以在 Azure 資源上為 Azure 訂用帳戶和服務指派適當的角色，以授與其存取權限。  對於服務，服務主體會識別 Azure Active Directory (AAD) 中的服務。 本章節將說明如何將 Azure 資源 (您稍早建立的 Azure Data Lake Store 帳戶) 的存取權授與像是 HDInsight 的應用程式服務，方法是建立應用程式的服務主體，並透過 Azure PowerShell 將角色指派給它。

若要設定 Azure Data Lake 的 Active Directory 驗證，您必須執行下列工作。

* 建立自我簽署憑證
* 在 Azure Active Directory 和服務主體中建立應用程式

### <a name="create-a-self-signed-certificate"></a>建立自我簽署憑證
進行本節中的步驟之前，請確定您已安裝 [Windows SDK](https://dev.windows.com/en-us/downloads)。 您也必須建立一個目錄 (例如 **C:\mycertdir**)，以在其中建立憑證。

1. 在 PowerShell 視窗中，瀏覽至您安裝 Windows SDK 的位置 (通常是 `C:\Program Files (x86)\Windows Kits\10\bin\x86`)，並使用 [MakeCert][makecert] 公用程式來建立自我簽署的憑證和私密金鑰。 使用下列命令。

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    系統會提示您輸入私密金鑰密碼。 命令成功執行之後，您應該會在您指定的憑證目錄中看到 **CertFile.cer** 和 **mykey.pvk**。
2. 使用 [Pvk2Pfx][pvk2pfx] 公用程式將 MakeCert 建立的 .pvk 和 .cer 檔案轉換成 .pfx 檔案。 執行下列命令。

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    系統提示時，輸入您稍早指定的私密金鑰密碼。 您針對 **-po** 參數指定的值是與 .pfx 檔案相關聯的密碼。 命令成功完成之後，您應該也會在您指定的憑證目錄中看到 CertFile.pfx。

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>建立 Azure Active Directory 和服務主體
在這一節中，您將執行相關步驟來建立 Azure Active Directory 應用程式的服務主體、指派角色給服務主體，並藉由提供憑證驗證為服務主體。 執行下列命令以在 Azure Active Directory 中建立應用程式。

1. 在 PowerShell 主控台視窗中貼上下列 Cmdlet。 請確定您針對 **-DisplayName** 屬性指定的值是唯一的。 此外，**-HomePage** 和 **-IdentiferUris** 的值是預留位置值而不會受到驗證。

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. 使用應用程式識別碼建立服務主體。

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. 將您要從 HDInsight 叢集存取之 Data Lake Store 資料夾和檔案的存取權授與服務主體。 下列程式碼片段可讓您存取 Data Lake Store 帳戶的根目錄 (您從中複製範例資料檔的位置) 和檔案本身。

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>建立 HDInsight Linux 叢集搭配 Data Lake Store 做為額外儲存體

在本節中，我們會建立一個 HDInsight Hadoop Linux 叢集搭配 Data Lake Store 做為額外儲存體。 對於此版本，HDInsight 叢集和 Data Lake Store 必須位於相同位置。

1. 開始擷取訂用帳戶租用戶識別碼。 稍後您將會需要此資訊。

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. 在此版本中，對於 Hadoop 叢集，Data Lake Store 只能做為叢集的額外儲存體。 預設儲存體仍是 Azure 儲存體 Blob (WASB)。 所以，我們要先建立叢集所需的儲存體帳戶和儲存體容器。

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. 建立 HDInsight 叢集。 使用下列 Cmdlet。

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Cmdlet 成功完成後，您應該會看到列出叢集詳細資料的輸出。


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a>在 HDInsight 叢集上執行測試工作以使用 Data Lake Store
設定 HDInsight 叢集之後，您可以在叢集上執行測試工作，以測試 HDInsight 叢集是否可以存取 Data Lake Store。 為了完成這個操作，我們將會執行範例 Hive 工作，該工作會使用您稍早上傳至 Data Lake Store 的範例資料建立資料表。

在這一節中，您將透過 SSH 連線到您所建立的 HDInsight Linux 叢集並執行範例 Hive 查詢。

* 如果您使用 Windows 用戶端來透過 SSH 連線到叢集，請參閱[從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端來透過 SSH 連線到叢集，請參閱[從 Linux 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. 連線之後，使用下列命令來啟動 Hive CLI：

        hive
2. 使用 CLI，輸入下列陳述式，以使用 Data Lake Store 中的範例資料來建立名為 **vehicles** 的新資料表：

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    您應該會看到如下所示的輸出：

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
一旦您已設定 HDInsight 叢集使用 Data Lake Store，您可以使用 HDFS 殼層命令來存取存放區。

在這一節中，您將透過 SSH 連線到您所建立的 HDInsight Linux 叢集並執行 HDFS 命令。

* 如果您使用 Windows 用戶端來透過 SSH 連線到叢集，請參閱[從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端來透過 SSH 連線到叢集，請參閱[從 Linux 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

連線之後，使用下列 HDFS 檔案系統命令列出 Data Lake Store 中的檔案。

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

這樣應該會列出您稍早上傳至 Data Lake Store 的檔案。

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

您也可以使用 `hdfs dfs -put` 命令來將一些檔案上傳至 Data Lake Store，然後使用 `hdfs dfs -ls` 以確認是否成功上傳檔案。

## <a name="see-also"></a>另請參閱
* [搭配 Azure HDInsight 叢集使用 Data Lake Store](../hdinsight/hdinsight-hadoop-use-data-lake-store.md)
* [入口網站：建立 HDInsight 叢集以使用 Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
