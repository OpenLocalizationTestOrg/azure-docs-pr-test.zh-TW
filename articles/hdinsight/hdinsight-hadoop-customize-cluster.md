---
title: "aaaCustomize HDInsight 叢集使用的指令碼動作-Azure |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>使用指令碼動作自訂 Windows 型 HDInsight 叢集
**指令碼動作**可以是使用的 tooinvoke[自訂指令碼](hdinsight-hadoop-script-actions.md)hello 叢集建立程序期間在叢集上安裝其他軟體。

本文章中的 hello 資訊是特定 tooWindows 為基礎的 HDInsight 叢集。 如果是以 Linux 為基礎的叢集，請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

HDInsight 叢集可以自訂各種不同的其他方式，例如包括額外的 Azure 儲存體帳戶、 變更 hello Hadoop 組態檔 （core-site.xml、 hive-site.xml 等），或加入到共用程式庫 （例如 Hive、 Oozie）一般 hello 叢集中的位置。 這些自訂可以透過 Azure PowerShell，hello Azure HDInsight.NET SDK 或 hello Azure 入口網站。 如需詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision-cluster]。

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Hello 叢集建立程序中的指令碼動作
Hello 程序所建立的叢集時，才會使用指令碼動作。 hello 下列圖表說明 hello 建立程序期間執行指令碼動作時：

![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]

Hello 叢集 hello 指令碼執行時，進入 hello **ClusterCustomization**階段。 在這個階段，hello 指令碼 hello 系統管理員帳戶下執行，以平行方式在所有 hello 指定 hello 叢集中的節點並可提供完整的系統管理員權限 hello 節點上。

> [!NOTE]
> 因為在 hello 期間的叢集節點上的系統管理員權限**ClusterCustomization**階段中，您可以使用 hello 指令碼 tooperform 作業，例如停止和啟動服務，包括 Hadoop 相關服務。 因此 hello 指令碼的一部分，您必須確定該 hello Ambari 服務和其他相關的 Hadoop 服務正在執行 hello 指令碼完成執行之前完成。 這些服務所需 toosuccessfully 確定 hello 健全狀況和狀態 hello 叢集在建立時。 如果您變更會影響這些服務的叢集上的任何設定，您必須使用所提供的 hello helper 函式。 如需 Helper 函式的詳細資訊，請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。
>
>

hello 輸出和 hello hello 指令碼的錯誤記錄檔會儲存在您指定給 hello 叢集 hello 預設儲存體帳戶中。 hello 記錄檔會儲存在資料表中具有 hello 名稱**u < \cluster-name-fragment >< \time-stamp > setuplog**。 這些是從所有節點上執行 hello （前端節點和背景工作角色節點） hello 叢集中的 hello 指令碼的彙總記錄檔。

每個叢集可以接受多個會指定中的 hello 順序叫用的指令碼動作。 在 hello 前端節點、 hello 背景工作節點，或兩者，就可以執行指令碼。

HDInsight 提供下列元件在 HDInsight 叢集上的數個指令碼 tooinstall hello:

| 名稱 | 指令碼 |
| --- | --- |
| **安裝 Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1。 請參閱[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]。 |
| **安裝 R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1。 請參閱[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]。 |
| **安裝 Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1。 請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。 |
| - **安裝 Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1。 請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。 |
| **預先載入 Hive 程式庫** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1。 請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>呼叫使用 hello Azure 入口網站的指令碼
**從 hello Azure 入口網站**

1. 依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。
2. 根據選擇性的設定，如 hello**指令碼動作**刀鋒視窗中，按一下 **加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：

    ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "使用指令碼動作 toocustomize 叢集")

    <table border='1'>
        <tr><th>屬性</th><th>值</th></tr>
        <tr><td>名稱</td>
            <td>指定 hello 指令碼動作的名稱。</td></tr>
        <tr><td>指令碼 URI</td>
            <td>指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。 s</td></tr>
        <tr><td>Head/Worker</td>
            <td>指定 hello 節點 (**Head**或**工作者**) 執行哪些 hello 自訂指令碼。</b>。
        <tr><td>參數</td>
            <td>指定 hello 參數，如果 hello 指令碼所需。</td></tr>
    </table>

    按下 ENTER tooadd 以上的一個指令碼動作 tooinstall 多個元件 hello 叢集上。
3. 按一下**選取**toosave hello 指令碼動作組態，並繼續建立叢集。

## <a name="call-scripts-using-azure-powershell"></a>使用 Azure PowerShell 呼叫指令碼
此下列 PowerShell 指令碼示範如何在 Windows 上的 Spark tooinstall 基礎 HDInsight 叢集。  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall 其他軟體，您將需要 tooreplace hello 指令碼檔案中 hello 指令碼：

出現提示時，輸入 hello 叢集 hello 認證。 可能需要幾分鐘後才建立 hello 叢集。

## <a name="call-scripts-using-net-sdk"></a>使用 .NET SDK 呼叫指令碼
hello 下列範例會示範如何在 Windows 上的 Spark tooinstall 基礎 HDInsight 叢集。 tooinstall 其他軟體，您必須在 hello 程式碼中的 tooreplace hello 指令碼檔案。

**toocreate Spark 與 HDInsight 叢集**

1. 在 Visual Studio 建立 C# 主控台應用程式。
2. 從 hello Nuget 封裝管理員主控台中，執行下列命令的 hello。

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. 使用下列陳述式使用 hello Program.cs 檔案中的 hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Hello 程式碼置於 hello hello 下列類別：

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. 按**F5** toorun hello 應用程式。

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>支援在 HDInsight 叢集上使用開放原始碼軟體
hello Microsoft Azure HDInsight 服務是彈性的平台，可讓您使用的開放原始碼技術 Hadoop 周圍形成的生態系統的 hello 定域機組中的 toobuild 巨量資料應用程式。 Microsoft Azure 會提供適用於開放原始碼技術，支援一般層級述 hello**支援範圍**區段 hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure 支援常見問題集網站</a>。 hello HDInsight 服務會提供額外一層的部分 hello 元件的支援，如下所述。

有兩種可用在 hello HDInsight 服務的開放原始碼元件類型：

* **內建元件**-HDInsight 叢集上已預先安裝這些元件，並提供 hello 叢集的核心功能。 例如，YARN ResourceManager、 hello Hive 查詢語言 (HiveQL) 及 hello 砲象兵程式庫屬於 toothis 類別目錄。 叢集元件的完整清單位於[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)</a>.
* **自訂元件**-您為 hello 叢集的使用者可以安裝或使用您的工作負載中用於 hello 社群或您所建立的任何元件。

完全支援內建的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。

> [!WARNING]
> 完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。
>
> 自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。
>
>

hello HDInsight 服務提供數種方式 toouse 自訂元件。 不論如何元件為使用 hello 叢集上安裝，hello 的支援相同層級套用。 以下是 hello 最常用的方式，自訂元件，可用在 HDInsight 叢集上的清單：

1. 提交作業-Hadoop 或其他類型的執行，或使用自訂元件的工作可以提交的 toohello 叢集。
2. 叢集自訂-叢集建立期間，您可以指定其他設定及自訂將 hello 叢集節點安裝的元件。
3. 範例-常用的自訂元件、 Microsoft 和其他人可能會提供如何使用這些元件在 hello HDInsight 叢集上的範例。 提供這些範例，但是沒有支援。

## <a name="develop-script-action-scripts"></a>開發指令碼動作指令碼
請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。

## <a name="see-also"></a>另請參閱
* [建立在 HDInsight Hadoop 叢集][ hdinsight-provision-cluster] toocreate 在 HDInsight 叢集使用其他自訂選項的方式提供的指示。
* [開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]
* [在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]
* [在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]
* [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。
* [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "叢集建立期間的階段"
