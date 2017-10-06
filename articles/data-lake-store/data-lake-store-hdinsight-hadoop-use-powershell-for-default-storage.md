---
title: "aaaCreate HDInsight 叢集與資料湖存放區作為預設儲存體使用 PowerShell |Microsoft 文件 '"
description: "使用 Azure PowerShell toocreate 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>使用 PowerShell 建立以 Data Lake Store 做為預設儲存體的 HDInsight 叢集
> [!div class="op_single_selector"]
> * [使用 hello Azure 入口網站](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [使用 PowerShell (針對預設儲存體)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [使用 PowerShell (針對額外儲存體)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [使用 Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

了解如何 toouse Azure PowerShell tooconfigure Azure HDInsight 叢集與 Azure Data Lake Store，做為預設儲存體。 如需有關如何建立以 Data Lake Store 做為額外儲存體的 HDInsight 叢集之指示，請參閱[建立以 Data Lake Store 做為額外儲存體的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-powershell.md)。

以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：

* hello 選項 toocreate 具有存取權的 HDInsight 叢集已可供 HDInsight 版本 3.5 和 3.6 tooData 湖存放區做為預設儲存體。

* HDInsight 叢集與 hello 選項 toocreate 存取 tooData 湖存放區，因為預設儲存體*無法使用*的高階 HDInsight 叢集。

tooconfigure HDInsight toowork 與資料湖存放區使用 PowerShell，請遵循 hello 接下來五個區段中的 hello 指示。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，請確定您符合下列需求的 hello:

* **Azure 訂用帳戶**： 跳過[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更高**： 請參閱[如何 tooinstall 和設定 PowerShell](/powershell/azure/overview)。
* **Windows 軟體開發套件 (SDK)**: tooinstall Windows SDK，跳過[下載和工具適用於 Windows 10](https://dev.windows.com/en-us/downloads)。 hello SDK 會使用的 toocreate 安全性憑證。
* **Azure Active Directory 服務主體**： 這個教學課程描述如何 toocreate Azure Active Directory (Azure AD) 中的服務主體。 不過，toocreate 服務主體，您必須是 Azure AD 系統管理員。 如果您是系統管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。

    >[!NOTE]
    >唯有您是 Azure AD 系統管理員，才可以建立服務主體。 您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。 hello 服務主體必須以建立憑證，如中所述[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。
    >

## <a name="create-a-data-lake-store-account"></a>建立 Data Lake Store 帳戶
toocreate Data Lake Store 帳戶，不要 hello 遵循：

1. 從您的桌面上，開啟 PowerShell 視窗，，然後輸入下列程式片段 hello。 當您準備提示的 toosign 中做為其中一個 hello 訂用帳戶管理員或擁有者的登入。 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > 如果您註冊 hello 資料湖存放區資源提供者，會收到類似的錯誤太`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`，您的訂閱可能無法在允許清單中的資料湖存放區。 tooenable Azure 的訂用帳戶 hello Data Lake Store 公開預覽，請依照中的 hello 指示[使用 hello Azure 入口網站開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。
    >

2. Data Lake Store 帳戶與 Azure 資源群組相關聯。 從建立資源群組著手。

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    您應該會看到如下的輸出：

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. 建立 Data Lake Store 帳戶。 您指定的名稱必須包含小寫字母和數字的 hello 帳戶。

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

4. 使用 Data Lake Store 當做預設儲存體需要您 toospecify 根路徑 toowhich hello 特定叢集的檔案會複製在叢集建立期間。 根的路徑，也就是 toocreate **/叢集/hdiadlcluster** hello 片段中使用下列 cmdlet 的 hello:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>設定以角色為基礎的驗證存取 tooData 湖存放區
每一個 Azure 訂用帳戶都與 Azure AD 實體相關聯。 使用者和服務存取訂用帳戶資源使用 hello Azure 入口網站或 hello Azure 資源管理員 API 首先必須向 Azure AD。 已授與存取 tooAzure 訂閱和服務由將其指派 hello Azure 資源上的適當角色。 為服務，服務主體識別 Azure AD 中的 hello 服務。

本節說明 toogrant 應用程式的服務方式，例如 HDInsight，存取 tooan Azure 資源 (hello 您稍早建立的 Data Lake Store 帳戶)。 您藉由建立服務主體的 hello 應用程式，並指派角色 tooit 透過 PowerShell。

設定 Active Directory 驗證的 Azure 資料湖，tooset hello 中執行下列兩個區段的 hello。

### <a name="create-a-self-signed-certificate"></a>建立自我簽署憑證
請確定您有[Windows SDK](https://dev.windows.com/en-us/downloads) hello 進行這一節的步驟之前安裝。 您必須也建立目錄，例如*C:\mycertdir*您用來建立 hello 憑證。

1. 從 hello PowerShell 視窗，請移 toohello 安裝 Windows SDK 的位置 (通常*C:\Program Files (x86) \Windows Kits\10\bin\x86*)，並使用 hello [MakeCert] [ makecert]公用程式 toocreate 自我簽署的憑證和私密金鑰。 使用下列命令的 hello:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    系統會提示的 tooenter hello 私密金鑰密碼。 Hello 命令執行成功之後，您應該會看到**CertFile.cer**和**mykey.pvk** hello 憑證，您所指定目錄中。
2. 使用 hello [Pvk2Pfx] [ pvk2pfx]公用程式 tooconvert hello.pvk 和.cer 檔案 MakeCert 建立的 tooa.pfx 檔案。 執行下列命令的 hello:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    當系統提示您時，輸入 hello 私密金鑰密碼您稍早指定。 hello 指定 hello 值**po**參數是 hello 與 hello.pfx 檔案相關聯的密碼。 Hello 命令已順利完成之後，您應該也會看到**CertFile.pfx** hello 憑證，您所指定目錄中。

### <a name="create-an-azure-ad-and-a-service-principal"></a>建立 Azure AD 和服務主體
在本節中，您可以建立 Azure AD 應用程式的服務主體、 指派角色 toohello 服務主體，以及 hello 服務主體以驗證所提供的憑證。 toocreate 應用程式在 Azure AD 中，執行下列命令的 hello:

1. 貼上下列指令程式 hello PowerShell 主控台視窗中的 hello。 請確定您指定 hello 的 hello 該值**-DisplayName**屬性是唯一的。 hello 值**-首頁**和**-IdentiferUris**預留位置值，並不會驗證。

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
3. 授與 hello 服務主體存取 toohello Data Lake Store 根和您稍早指定的 hello 根路徑中的所有 hello 資料夾。 使用下列 cmdlet 的 hello:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>建立具有 Data Lake Store 的 HDInsight Linux 叢集為 hello 預設儲存體

在本節中，您建立 HDInsight Hadoop Linux 叢集與資料湖存放區作為 hello 預設儲存體。 此版本中，hello HDInsight 叢集，且資料湖存放區必須為 hello 相同的位置。

1. 擷取 hello 訂用帳戶的租用戶識別碼，並將它儲存 toouse 更新版本。

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. 使用下列 cmdlet 的 hello 建立 hello HDInsight 叢集：

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Hello 指令程式已順利完成之後，您應該會看到列出 hello 叢集詳細資料的輸出。

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Hello HDInsight 叢集 toouse 資料湖存放區上執行測試工作
您已設定的 HDInsight 叢集之後，您可以測試工作在其上執行 tooensure 能夠存取資料湖存放區。 toodo，執行範例 Hive 工作 toocreate 使用已經在資料湖存放區中的 hello 範例資料的資料表 *<cluster root>/example/data/sample.log*。

在本節中，您進行安全殼層 (SSH) 連線到 hello 您建立 HDInsight Linux 叢集，然後您執行範例 Hive 查詢。

* 如果您使用 Windows 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。

1. Hello 連接之後，請使用下列命令的 hello 啟動 hello Hive 命令列介面 (CLI):

        hive
2. 下列陳述式 toocreate 名為的新資料表使用 hello CLI tooenter hello**車輛**利用資料湖存放區中的 hello 範例資料：

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    您應該會看到 hello 查詢輸出 hello SSH 主控台上。

    >[!NOTE]
    >hello hello 上述 CREATE TABLE 命令中的路徑 toohello 範例資料是`adl:///example/data/`，其中`adl:///`hello 叢集根目錄。 指定在此教學課程中的 hello 叢集根目錄 hello 範例，下列是 hello 命令`adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`。 您可以使用 hello 較短的替代方案，或提供 hello 完整路徑 toohello 叢集根目錄。
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>使用 HDFS 命令存取 Data Lake Store
設定 hello HDInsight 叢集 toouse 資料湖存放區之後，您可以使用 Hadoop 分散式檔案系統 (HDFS) 殼層命令 tooaccess hello 存放區。

在本節中，確定 SSH 連線到 hello 您建立 HDInsight Linux 叢集，然後您執行 hello HDFS 命令。

* 如果您使用 Windows 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和從 Windows 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。
* 如果您使用 Linux 用戶端 toomake SSH 連線到 hello 叢集中，請參閱[搭配使用 SSH 和 Linux 的 HDInsight 上的 Linux Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。

進行 hello 連線之後，請使用下列 HDFS 檔案系統命令 hello 列出資料湖存放區中的 hello 檔案。

    hdfs dfs -ls adl:///

您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 tooData 湖存放區，然後使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。

## <a name="see-also"></a>另請參閱
* [Azure 入口網站： 建立 HDInsight 叢集 toouse 資料湖存放區](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
