---
title: "使用 .NET 建立 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何在 Linux 上使用 HDInsight .NET SDK 為 HDInsight 建立 Hadoop、HBase、Storm 或 Spark 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9c74e3dc-837f-4c90-bbb1-489bc7124a3d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: ccd3a0c777510e0694170b2f9acc8da0e7dcde9b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-net-sdk"></a><span data-ttu-id="7ce2e-103">在 HDInsight 中使用 .NET SDK 建立以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-103">Create Linux-based clusters in HDInsight using the .NET SDK</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]


<span data-ttu-id="7ce2e-104">了解如何使用 .NET SDK 在 Azure HDInsight 叢集中建立 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-104">Learn how to create a Hadoop cluster in Azure HDInsight cluster using the .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ce2e-105">本文中的步驟會建立具有一個背景工作節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-105">The steps in this document create a cluster with one worker node.</span></span> <span data-ttu-id="7ce2e-106">如果您在建立叢集時或在建立後調整叢集時規劃有 32 個以上的背景工作節點，您就必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-106">If you plan on more than 32 worker nodes, either at cluster creation or by scaling the cluster after creation, you need to select a head node size with at least 8 cores and 14GB ram.</span></span>
>
> <span data-ttu-id="7ce2e-107">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-107">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ce2e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ce2e-108">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="7ce2e-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-109">**An Azure subscription**.</span></span> <span data-ttu-id="7ce2e-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7ce2e-111">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-111">**An Azure storage account**.</span></span> <span data-ttu-id="7ce2e-112">請參閱[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-112">See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="7ce2e-113">**Visual Studio 2013、Visual Studio 2015 或 Visual Studio 2017**。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-113">**Visual Studio 2013, Visual Studio 2015 or Visual Studio 2017**.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="7ce2e-114">建立叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-114">Create clusters</span></span>

1. <span data-ttu-id="7ce2e-115">開啟 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-115">Open Visual Studio 2017.</span></span>
2. <span data-ttu-id="7ce2e-116">建立新的 Visual C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-116">Create a new Visual C# console application.</span></span>
3. <span data-ttu-id="7ce2e-117">在 [工具] 功能表中按一下 [NuGet 套件管理員]，然後按一下 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-117">From the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="7ce2e-118">在主控台中執行下列命令，以安裝套件：</span><span class="sxs-lookup"><span data-stu-id="7ce2e-118">Run the following command in the console to install the packages:</span></span>

    ```powershell
    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight
    ```

    <span data-ttu-id="7ce2e-119">這些命令會將 .NET 程式庫及其參考新增至目前的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-119">These commands add .NET libraries and references to them to the current Visual Studio project.</span></span>
5. <span data-ttu-id="7ce2e-120">在 [方案總管] 中按兩下 **Program.cs** 來開啟該檔案、貼上下列程式碼，然後提供變數的值：</span><span class="sxs-lookup"><span data-stu-id="7ce2e-120">From Solution Explorer, double-click **Program.cs** to open it, paste the following code, and provide values for the variables:</span></span>

    ```csharp
    using System;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    namespace CreateHDInsightCluster
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;

            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            private const string ExistingResourceGroupName = "<Enter Resource Group Name>";
            private const string ExistingStorageName = "<Enter Default Storage Account Name>.blob.core.windows.net";
            private const string ExistingStorageKey = "<Enter Default Storage Account Key>";
            private const string ExistingBlobContainer = "<Enter Default Bob Container Name>";

            private const string NewClusterName = "<Enter HDInsight Cluster Name>";
            private const int NewClusterNumNodes = 2;
            private const string NewClusterLocation = "EAST US 2";     // Must be the same as the default Storage account
            private const OSType NewClusterOSType = OSType.Linux;
            private const string NewClusterType = "Hadoop";
            private const string NewClusterVersion = "3.5";
            private const string NewClusterUsername = "admin";
            private const string NewClusterPassword = "<Enter HTTP User Password>";
            private const string NewClusterSshUserName = "sshuser";

            // You can use eitehr password or public key. See https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix
            private const string NewClusterSshPassword = "<Enter SSH User Password>";
            private const string NewClusterSshPublicKey = @"---- BEGIN SSH2 PUBLIC KEY ----
                Comment: ""rsa-key-20150731""
                AAAAB3NzaC1yc2EAAAABJQAAAQEA4QiCRLqT7fnmUA5OhYWZNlZo6lLaY1c+IRsp
                gmPCsJVGQLu6O1wqcxRqiKk7keYq8bP5s30v6bIljsLZYTnyReNUa5LtFw7eauGr
                yVt3Pve6ejfWELhbVpi0iq8uJNFA9VvRkz8IP1JmjC5jsdnJhzQZtgkIrdn3w0e6
                WVfu15kKyY8YAiynVbdV51EB0SZaSLdMZkZQ81xi4DDtCZD7qvdtWEFwLa+EHdkd
                pzO36Mtev5XvseLQqzXzZ6aVBdlXoppGHXkoGHAMNOtEWRXpAUtEccjpATsaZhQR
                zZdZlzHduhM10ofS4YOYBADt9JohporbQVHM5w6qUhIgyiPo7w==
                ---- END SSH2 PUBLIC KEY ----"; //replace the public key with your own

            static void Main(string[] args)
            {
                System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

                // Authenticate and get a token
                var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // Set parameters for the new cluster
                var parameters = new ClusterCreateParameters
                {
                    ClusterSizeInNodes = NewClusterNumNodes,
                    UserName = NewClusterUsername,
                    ClusterType = NewClusterType,
                    OSType = NewClusterOSType,
                    Version = NewClusterVersion,

                    // Use an Azure storage account as the default storage
                    DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

                    // Is the cluster type RServer? If so, you can set the EdgeNodeSize.
                    // Otherwise, the default VM size is used.
                    //EdgeNodeSize = "Standard_D12_v2",

                    Password = NewClusterPassword,
                    Location = NewClusterLocation,

                    SshUserName = NewClusterSshUserName,
                    SshPassword = NewClusterSshPassword,
                    //SshPublicKey = NewClusterSshPublicKey
                };

                // Is the cluster type RServer? If so, add the RStudio configuration option.
                /*
                parameters.Configurations.Add(
                    "rserver",
                    new Dictionary<string, string>()
                    {
                        { "rstudio", "true" }
                    }
                );
                */

                // Create the cluster
                _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

                System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials GetTokenCloudCredentials(string TenantId, string ClientId, string SubscriptionId)
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }
    ```

6. <span data-ttu-id="7ce2e-121">取代類別成員值。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-121">Replace the class member values.</span></span>
7. <span data-ttu-id="7ce2e-122">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-122">Press **F5** to run the application.</span></span> <span data-ttu-id="7ce2e-123">主控台視窗會開啟並顯示應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-123">A console window should open and display the status of the application.</span></span> <span data-ttu-id="7ce2e-124">系統會提示您輸入 Azure 帳號認證。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-124">You are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="7ce2e-125">建立 HDInsight 叢集可能需要幾分鐘的時間，通常約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-125">It can take several minutes to create an HDInsight cluster, normally around 15.</span></span>

## <a name="use-bootstrap"></a><span data-ttu-id="7ce2e-126">使用 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="7ce2e-126">Use bootstrap</span></span>

<span data-ttu-id="7ce2e-127">藉由使用 Bootstrap，您可以在建立叢集期間設定額外的設定。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-127">Using bootstrap, you can configure addition settings during the cluster creations.</span></span>  <span data-ttu-id="7ce2e-128">如需詳細資訊，請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-128">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

<span data-ttu-id="7ce2e-129">修改 [建立叢集](#create-clusters) 中的範例，以設定 Hive 設定：</span><span class="sxs-lookup"><span data-stu-id="7ce2e-129">Modify the sample in [Create clusters](#create-clusters) to configure a Hive setting:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for the new cluster
    var extendedParameters = new ClusterCreateParametersExtended
    {
        Location = NewClusterLocation,
        Properties = new ClusterCreateProperties
        {
            ClusterDefinition = new ClusterDefinition
            {
                ClusterType = NewClusterType.ToString()
            },
            ClusterVersion = NewClusterVersion,
            OperatingSystemType = NewClusterOSType
        }
    };

    var coreConfigs = new Dictionary<string, string>
    {
        {"fs.defaultFS", string.Format("wasb://{0}@{1}", ExistingBlobContainer, ExistingStorageName)},
        {
            string.Format("fs.azure.account.key.{0}", ExistingStorageName),
            ExistingStorageKey
        }
    };

    // bootstrap
    var hiveConfigs = new Dictionary<string, string>
    {
        { "hive.metastore.client.socket.timeout", "90"}
    };

    var gatewayConfigs = new Dictionary<string, string>
    {
        {"restAuthCredential.isEnabled", "true"},
        {"restAuthCredential.username", NewClusterUsername},
        {"restAuthCredential.password", NewClusterPassword}
    };

    var configurations = new Dictionary<string, Dictionary<string, string>>
    {
        {"core-site", coreConfigs},
        {"gateway", gatewayConfigs},
        {"hive-site", hiveConfigs}
    };

    var serializedConfig = JsonConvert.SerializeObject(configurations);
    extendedParameters.Properties.ClusterDefinition.Configurations = serializedConfig;

    var sshPublicKeys = new List<SshPublicKey>();
    var sshPublicKey = new SshPublicKey
    {
        CertificateData =
            string.Format("ssh-rsa {0}", NewClusterSshPublicKey)
    };
    sshPublicKeys.Add(sshPublicKey);

    var headNode = new Role
    {
        Name = "headnode",
        TargetInstanceCount = 2,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                // When use a SSH pulbic key, make sure to remove comments, headers and trailers, and concatenate the key into one line 
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    var workerNode = new Role
    {
        Name = "workernode",
        TargetInstanceCount = NewClusterNumNodes,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    extendedParameters.Properties.ComputeProfile = new ComputeProfile();
    extendedParameters.Properties.ComputeProfile.Roles.Add(headNode);
    extendedParameters.Properties.ComputeProfile.Roles.Add(workerNode);

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, extendedParameters);

    System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
    System.Console.ReadLine();
}
```

## <a name="use-script-action"></a><span data-ttu-id="7ce2e-130">使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-130">Use Script Action</span></span>

<span data-ttu-id="7ce2e-131">藉由使用指令碼動作，您可以在建立叢集期間設定額外的設定。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-131">Using Script Action, you can configure additional settings during cluster creations.</span></span>  <span data-ttu-id="7ce2e-132">如需詳細資訊，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-132">For more information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7ce2e-133">修改 [建立叢集](#create-clusters) 中的範例，以呼叫用來安裝 R 的指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="7ce2e-133">Modify the sample in [Create clusters](#create-clusters) to call a Script Action to install R:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  The process takes 10 to 20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for the new cluster
    var parameters = new ClusterCreateParameters
    {
        ClusterSizeInNodes = NewClusterNumNodes,
        Location = NewClusterLocation,
        ClusterType = NewClusterType,
        OSType = NewClusterOSType,
        Version = NewClusterVersion,

        DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

        UserName = NewClusterUsername,
        Password = NewClusterPassword,
        SshUserName = NewClusterSshUserName,
        SshPublicKey = NewClusterSshPublicKey
    };

    ScriptAction rScriptAction = new ScriptAction("Install R",
        new Uri("https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh"), "");

    parameters.ScriptActions.Add(ClusterNodeType.HeadNode,new System.Collections.Generic.List<ScriptAction> { rScriptAction});
    parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { rScriptAction });

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

    System.Console.WriteLine("The cluster has been created. Press ENTER to continue ...");
    System.Console.ReadLine();
}
```

## <a name="troubleshoot"></a><span data-ttu-id="7ce2e-134">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7ce2e-134">Troubleshoot</span></span>

<span data-ttu-id="7ce2e-135">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-135">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ce2e-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ce2e-136">Next steps</span></span>
<span data-ttu-id="7ce2e-137">既然您已成功建立 HDInsight 叢集，請使用下列內容來了解如何使用您的叢集。</span><span class="sxs-lookup"><span data-stu-id="7ce2e-137">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span> 

### <a name="hadoop-clusters"></a><span data-ttu-id="7ce2e-138">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-138">Hadoop clusters</span></span>
* [<span data-ttu-id="7ce2e-139">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="7ce2e-139">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7ce2e-140">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="7ce2e-140">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7ce2e-141">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="7ce2e-141">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="7ce2e-142">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-142">HBase clusters</span></span>
* [<span data-ttu-id="7ce2e-143">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="7ce2e-143">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="7ce2e-144">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce2e-144">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="7ce2e-145">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-145">Storm clusters</span></span>
* [<span data-ttu-id="7ce2e-146">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="7ce2e-146">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="7ce2e-147">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="7ce2e-147">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="7ce2e-148">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="7ce2e-148">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="7ce2e-149">Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="7ce2e-149">Spark clusters</span></span>
* [<span data-ttu-id="7ce2e-150">使用 Scala 來建立獨立的應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce2e-150">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7ce2e-151">利用 Livy 在 Spark 叢集上遠端執行工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-151">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="7ce2e-152">Spark 和 BI：搭配 BI 工具來使用 HDInsight 中的 Spark 以執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="7ce2e-152">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7ce2e-153">Spark 和機器學習：使用 HDInsight 中的 Spark 來預測食物檢查結果</span><span class="sxs-lookup"><span data-stu-id="7ce2e-153">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7ce2e-154">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce2e-154">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="run-jobs"></a><span data-ttu-id="7ce2e-155">執行工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-155">Run jobs</span></span>
* [<span data-ttu-id="7ce2e-156">使用 .NET SDK 在 HDInsight 中執行 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-156">Run Hive jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="7ce2e-157">使用 .NET SDK 在 HDInsight 中執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-157">Run Pig jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
* [<span data-ttu-id="7ce2e-158">使用 .NET SDK 在 HDInsight 中執行 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-158">Run Sqoop jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
* [<span data-ttu-id="7ce2e-159">在 HDInsight 中執行 Oozie 工作</span><span class="sxs-lookup"><span data-stu-id="7ce2e-159">Run Oozie jobs in HDInsight</span></span>](hdinsight-use-oozie.md)

