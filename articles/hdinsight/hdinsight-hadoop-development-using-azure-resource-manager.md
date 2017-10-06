---
title: "aaaMigrate tooAzure 資源管理員工具 hdinsight |Microsoft 文件"
description: "HDInsight 叢集的 toomigrate tooAzure 資源管理員開發工具的方式"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>HDInsight 叢集的移轉 tooAzure 資源管理員為基礎的開發工具

HDInsight 正在取代以 Azure Service Manager (ASM) 為基礎的工具 (適用於 HDInsight)。 如果您已在使用 Azure PowerShell、 Azure CLI 或 hello HDInsight.NET SDK toowork 與 HDInsight 叢集，則建議的 toouse hello Azure 資源管理員 arm 版本的 PowerShell、 CLI 及接下來的.NET SDK。 這篇文章提供如何指標 toomigrate toohello 新 ARM 架構的方法。 只要適用時，本文也將點出 hello HDInsight 的 hello ASM 和 ARM 方法之間的差異。

> [!IMPORTANT]
> ASM hello 支援根據 PowerShell、 CLI，並將於中止.NET SDK **2017 年 1 月 1，**。
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>移轉 Azure CLI tooAzure 資源管理員
hello Azure CLI 現在預設 tooAzure 資源管理員 (ARM) 模式中，除非您要升級從先前的安裝。在此情況下，您可能需要 toouse hello`azure config mode arm`命令 tooswitch tooARM 模式。

使用 ARM; 時，該 hello Azure CLI 提供使用 Azure 服務管理 (ASM) 的 HDInsight toowork 是 hello 相同的 hello 基本命令不過有些參數和參數可能會有新名稱，並有許多新的參數使用 ARM 時。 例如，您現在可以使用`azure hdinsight cluster create`toospecify hello Azure 虛擬網路中，應該建立的叢集或 Hive 和 Oozie 中繼存放區資訊。

透過 Azure Resource Manager 來使用 HDInsight 的基本命令為︰

* `azure hdinsight cluster create` - 建立新的 HDInsight 叢集
* `azure hdinsight cluster delete` - 刪除現有的 HDInsight 叢集
* `azure hdinsight cluster show` - 顯示現有叢集的相關資訊
* `azure hdinsight cluster list` - 列出適用於您 Azure 訂用帳戶的 HDInsight 叢集

使用 hello`-h`切換 tooinspect hello 參數和每個命令，您可以使用的參數。

### <a name="new-commands"></a>新的命令
可用於 Azure Resource Manager 的新命令︰

* `azure hdinsight cluster resize`-以動態方式變更 hello hello 叢集中的背景工作節點數
* `azure hdinsight cluster enable-http-access`-啟用 HTTPs 存取 toohello 叢集 (在預設情況下)
* `azure hdinsight cluster disable-http-access`-停用 HTTPs 存取 toohello 叢集
* `azure hdinsight script-action` - 在叢集上提供建立/管理指令碼動作的命令
* `azure hdinsight config`-提供建立設定檔可與 hello 命令`hdinsight cluster create`命令 tooprovide 組態資訊。

### <a name="deprecated-commands"></a>已取代的命令
如果您使用 hello`azure hdinsight job`命令 toosubmit 作業 tooyour HDInsight 叢集，這些不是可透過 hello ARM 命令。 如果您需要 tooprogrammatically 送出工作 tooHDInsight 從指令碼，您應該改用 hello HDInsight 所提供的 REST Api。 如需提交使用 REST Api 作業的詳細資訊，請參閱下列文件的 hello。

* [使用 Curl 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop](hdinsight-hadoop-use-mapreduce-curl.md)
* [使用 Curl 搭配執行 Hive 查詢 與 HDInsight 上的 Hadoop](hdinsight-hadoop-use-hive-curl.md)
* [使用 Curl 搭配執行 Pig 工作與 HDInsight 上的 Hadoop](hdinsight-hadoop-use-pig-curl.md)

如需其他方式 toorun MapReduce，Hive，和 Pig 以互動方式，請參閱[的 HDInsight 上的 Hadoop 使用 MapReduce](hdinsight-use-mapreduce.md)，[的 HDInsight 上的 Hadoop Hive 使用](hdinsight-use-hive.md)，和[的 Hadoop 上搭配使用 PigHDInsight](hdinsight-use-pig.md)。

### <a name="examples"></a>範例
**建立叢集**

* 舊的命令 (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* 新的命令 (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**刪除叢集**

* 舊的命令 (ASM) - `azure hdinsight cluster delete myhdicluster`
* 新的命令 (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`

**列出叢集**

* 舊的命令 (ASM) - `azure hdinsight cluster list`
* 新的命令 (ARM) - `azure hdinsight cluster list`

> [!NOTE]
> 對於 hello 清單的命令，指定 hello 資源群組使用`-g`會傳回只 hello 叢集 hello 指定的資源群組中。
> 
> 

**顯示叢集資訊**

* 舊的命令 (ASM) - `azure hdinsight cluster show myhdicluster`
* 新的命令 (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>移轉的 Azure PowerShell tooAzure 資源管理員
hello 的一般資訊 Azure PowerShell hello Azure 資源管理員 (ARM) 模式中，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。

hello Azure PowerShell ARM 指令程式可由位並行安裝以 hello ASM cmdlet。 hello cmdlet 從 hello 兩種模式可以藉由其名稱加以區別。  hello ARM 模式有*AzureRmHDInsight*太比較 hello cmdlet 名稱中*AzureHDInsight* hello ASM 模式。  例如，「New-AzureRmHDInsightCluster」對比「New-AzureHDInsightCluster」。 某些參數和切換參數可能會有新的名稱，而且當使用 ARM 時，會有許多新的參數可供使用。  例如，數個 Cmdlet 需要名為 -ResourceGroupName 的新切換參數。 

您可以使用 hello HDInsight cmdlet 之前，您必須連接 tooyour Azure 帳戶，並建立新的資源群組：

* Login-AzureRmAccount 或 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)。 請參閱 [使用 Azure Resource Manager 驗證服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>重新命名 Cmdlet
toolist hello HDInsight ASM cmdlet 在 Windows PowerShell 主控台：

    help *azurermhdinsight*

hello 下表列出 hello ASM cmdlet 與 hello ARM 模式中的名稱：

| ASM cmdlets | ARM cmdlets |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>新的 Cmdlet
hello 如下 hello hello ARM 模式中才有的新 cmdlet。 

**指令碼動作相關的 Cmdlet：**

* **Get AzureRmHDInsightPersistedScriptAction**： 取得 hello 保存叢集的指令碼動作，依時間順序列出這些或取得指定的持續性指令碼動作的詳細資料。 
* **Get AzureRmHDInsightScriptActionHistory**： 取得 hello 指令碼動作記錄的叢集和清單以反向的依時間先後順序，或取得先前執行的指令碼動作的詳細資料。 
* **Remove-AzureRmHDInsightPersistedScriptAction**︰自 HDInsight 叢集移除持續性指令碼動作。
* **設定 AzureRmHDInsightPersistedScriptAction**： 設定先前執行的指令碼動作 toobe 保存的指令碼動作。
* **提交 AzureRmHDInsightScriptAction**： 提交新的指令碼動作 tooan Azure HDInsight 叢集。 

如需關於其他使用方式的詳細資訊，請參閱 [使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

**叢集身分識別相關的 Cmdlet：**

* **新增 AzureRmHDInsightClusterIdentity**： 新增叢集識別 tooa 叢集組態物件，以便 hello HDInsight 叢集可以存取 Azure 資料湖存放區。 請參閱 [使用 Azure PowerShell 建立具 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)。

### <a name="examples"></a>範例
**建立叢集**

舊的命令 (ASM)： 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

新的命令 (ARM)：

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**刪除叢集**

舊的命令 (ASM)：

    Remove-AzureHDInsightCluster -name $clusterName 

新的命令 (ARM)：

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**列出叢集**

舊的命令 (ASM)：

    Get-AzureHDInsightCluster

新的命令 (ARM)：

    Get-AzureRmHDInsightCluster 

**顯示叢集**

舊的命令 (ASM)：

    Get-AzureHDInsightCluster -Name $clusterName

新的命令 (ARM)：

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>其他範例
* [建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [提交 Hive 工作](hdinsight-hadoop-use-hive-powershell.md)
* [提交 Pig 工作](hdinsight-hadoop-use-pig-powershell.md)
* [提交 Sqoop 工作](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>移轉 toohello arm HDInsight.NET SDK
hello Azure 服務管理基礎[(ASM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx)現在已被取代。 您會鼓勵的 toouse hello Azure 資源管理基礎[(ARM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)。 hello 下列 ASM 為基礎的 HDInsight 套件已被取代。

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

本節提供指標 toomore 資訊如何 tooperform 特定工作使用 hello arm SDK。

| 如何...使用 hello arm HDInsight SDK | 連結 |
| --- | --- |
| 使用 .NET SDK 建立 HDInsight 叢集 |請參閱 [使用.NET SDK 來建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| 搭配使用指令碼動作與 .NET SDK 來自訂叢集 |請參閱 [使用指令碼動作來自訂 HDInsight Linux 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| 搭配使用 Azure Active Directory 與 .NET SDK，以互動方式驗證應用程式 |請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。 本文章中的 hello 程式碼片段會使用 hello 互動式驗證方法。 |
| 搭配使用 Azure Active Directory 與 .NET SDK，以非互動方式驗證應用程式 |請參閱 [建立 HDInsight 的非互動式應用程式](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| 使用 .NET SDK 提交 Hive 作業 |請參閱 [提交 Hive 工作](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| 使用 .NET SDK 提交 Pig 作業 |請參閱 [提交 Pig 工作](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| 使用 .NET SDK 提交 Sqoop 作業 |請參閱 [提交 Sqoop 工作](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| 使用 .NET SDK 列出 HDInsight 叢集 |請參閱 [列出 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| 使用.NET SDK 調整 HDInsight 叢集 |請參閱 [調整 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| 使用.NET SDK 授與/撤銷存取 tooHDInsight 叢集 |請參閱[授與/撤銷存取 tooHDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| 使用 .NET SDK 更新 HDInsight 叢集的 HTTP 使用者認證 |請參閱 [「更新 HDInsight 叢集的 HTTP 使用者認證」](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| 使用.NET SDK 的 HDInsight 叢集的尋找 hello 預設儲存體帳戶 |請參閱[尋找 HDInsight 叢集的 hello 預設儲存體帳戶](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| 使用 .NET SDK 刪除 HDInsight 叢集 |請參閱 [「刪除 HDInsight 叢集」](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>範例
以下是一些範例上執行作業的方式都使用 hello arm SDK hello ASM 為基礎的 SDK 和 hello 對等的程式碼片段。

**建立叢集 CRUD 用戶端**

* 舊的命令 (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* 新的命令 (ARM) (服務主體的授權)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* 新的命令 (ARM) (使用者的授權)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**建立叢集**

* 舊的命令 (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* 新的命令 (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**啟用 HTTP 存取**

* 舊的命令 (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* 新的命令 (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**刪除叢集**

* 舊的命令 (ASM)
  
        client.DeleteCluster(dnsName);
* 新的命令 (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

