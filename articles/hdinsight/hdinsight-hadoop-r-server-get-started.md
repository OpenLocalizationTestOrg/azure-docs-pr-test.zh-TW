---
title: "開始使用 HDInsight 中的 R 伺服器 - Azure | Microsoft Docs"
description: "了解如何在包含 R 伺服器的 HDInsight 叢集上建立 Apache Spark，並在叢集上提交 R 指令碼。"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: 14e2a14c74e00709e18a80325fbdd3cbcd71da37
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="5bf64-103">開始使用 HDInsight 中的 R Server</span><span class="sxs-lookup"><span data-stu-id="5bf64-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="5bf64-104">HDInsight 包含了要整合至您的 HDInsight 叢集的 R 伺服器選項。</span><span class="sxs-lookup"><span data-stu-id="5bf64-104">HDInsight includes an R Server option to be integrated into your HDInsight cluster.</span></span> <span data-ttu-id="5bf64-105">此選項可讓 R 指令碼使用 Spark 和 MapReduce 來執行分散式計算。</span><span class="sxs-lookup"><span data-stu-id="5bf64-105">This option allows R scripts to use Spark and MapReduce to run distributed computations.</span></span> <span data-ttu-id="5bf64-106">在本文件中，您將了解如何在 HDInsight 叢集上建立 R Server，接著執行 R 指令碼，以示範使用 Spark 進行分散式 R 計算。</span><span class="sxs-lookup"><span data-stu-id="5bf64-106">In this document, you learn how to create an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5bf64-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="5bf64-107">Prerequisites</span></span>

* <span data-ttu-id="5bf64-108">**Azure 訂用帳戶**：開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="5bf64-109">請移至[取得 Microsoft Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)一文，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf64-109">Go to the article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="5bf64-110">**安全殼層 (SSH) 用戶端**：SSH 用戶端可用來從遠端連線至 HDInsight 叢集，並直接在叢集上執行命令。</span><span class="sxs-lookup"><span data-stu-id="5bf64-110">**A Secure Shell (SSH) client**: An SSH client is used to remotely connect to the HDInsight cluster and run commands directly on the cluster.</span></span> <span data-ttu-id="5bf64-111">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="5bf64-112">**SSH 金鑰 (選擇性)**：您可以使用密碼或公開金鑰，保護用來連線到叢集的 SSH 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-112">**SSH keys (optional)**: You can secure the SSH account used to connect to the cluster using either a password or a public key.</span></span> <span data-ttu-id="5bf64-113">使用密碼比較簡單，因為您不需要建立公開/私密金鑰組即可開始使用。</span><span class="sxs-lookup"><span data-stu-id="5bf64-113">Using a password is easier, and allows you to get started without having to create a public/private key pair.</span></span> <span data-ttu-id="5bf64-114">不過，使用金鑰更加安全。</span><span class="sxs-lookup"><span data-stu-id="5bf64-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="5bf64-115">本文中的步驟是假設您使用密碼來進行作業。</span><span class="sxs-lookup"><span data-stu-id="5bf64-115">The steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="5bf64-116">自動化的叢集建立</span><span class="sxs-lookup"><span data-stu-id="5bf64-116">Automated cluster creation</span></span>

<span data-ttu-id="5bf64-117">您可以使用 Azure Resource Manager 範本、SDK 以及 PowerShell，自動建立 HDInsight R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bf64-117">You can automate the creation of HDInsight R Servers using Azure Resource Manager templates, the SDK, and also PowerShell.</span></span>

* <span data-ttu-id="5bf64-118">若要使用 Azure Resource Management 範本來建立 R 伺服器，請參閱[部署 R 伺服器 HDInsight 叢集](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-118">To create an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="5bf64-119">若要使用 .NET SDK 建立 R 伺服器，請參閱[在 HDInsight 中使用 .NET SDK 建立以 Linux 為基礎的叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-119">To create an R Server using the .NET SDK, see [create Linux-based clusters in HDInsight using the .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="5bf64-120">若要使用 Powershell 部署 R 伺服器，請參閱[使用 PowerShell 在 HDInsight 上建立 R 伺服器](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)一文。</span><span class="sxs-lookup"><span data-stu-id="5bf64-120">To deploy R Server using powershell, see the article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-the-cluster-using-the-azure-portal"></a><span data-ttu-id="5bf64-121">使用 Azure 入口網站建立叢集</span><span class="sxs-lookup"><span data-stu-id="5bf64-121">Create the cluster using the Azure portal</span></span>

1. <span data-ttu-id="5bf64-122">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5bf64-123">依序選取 [新增] -> [情報 + 分析] -> [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="5bf64-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![建立新叢集的影像](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="5bf64-125">在 [快速建立] 體驗中，於 [叢集名稱] 欄位中輸入叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf64-125">In the **Quick create** experience, enter a name for the cluster in the **Cluster Name** field.</span></span> <span data-ttu-id="5bf64-126">如果您有多個 Azure 訂用帳戶，請使用 [訂用帳戶] 項目選取要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-126">If you have multiple Azure subscriptions, use the **Subscription** entry to select the one you want to use.</span></span>

    ![叢集名稱和訂用帳戶選取項目](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="5bf64-128">選取 [叢集類型] 以開啟 [叢集組態] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5bf64-128">Select **Cluster type** to open the **Cluster configuration** blade.</span></span> <span data-ttu-id="5bf64-129">在 [叢集組態] 刀鋒視窗中，選取下列選項︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-129">On the **Cluster Configuration** blade, select the following options:</span></span>

    * <span data-ttu-id="5bf64-130">**叢集類型**：R 伺服器</span><span class="sxs-lookup"><span data-stu-id="5bf64-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="5bf64-131">**版本**︰選取要安裝在叢集上的 R 伺服器版本。</span><span class="sxs-lookup"><span data-stu-id="5bf64-131">**Version**: select the version of R Server to install on the cluster.</span></span> <span data-ttu-id="5bf64-132">目前可用的版本是 ***R 伺服器 9.1 (HDI 3.6)***。</span><span class="sxs-lookup"><span data-stu-id="5bf64-132">The version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="5bf64-133">R 伺服器可用版本的版本資訊可在[這裡](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)取得。</span><span class="sxs-lookup"><span data-stu-id="5bf64-133">Release notes for the available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="5bf64-134">**R 伺服器的 R Studio Community 版本**︰邊緣節點上預設會安裝這個以瀏覽器為基礎的 IDE。</span><span class="sxs-lookup"><span data-stu-id="5bf64-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on the edge node.</span></span> <span data-ttu-id="5bf64-135">如果您不想安裝它，則請將此核取方塊取消核取。</span><span class="sxs-lookup"><span data-stu-id="5bf64-135">If you would prefer to not have it installed, then uncheck the check box.</span></span> <span data-ttu-id="5bf64-136">如果您選擇安裝它，則在建立後，可在叢集的入口網站應用程式刀鋒視窗上，找到用來存取 RStudio 伺服器登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="5bf64-136">If you choose to have it installed, the URL for accessing the RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="5bf64-137">其他選項保留為預設值，然後使用 [選取] 按鈕以儲存叢集類型。</span><span class="sxs-lookup"><span data-stu-id="5bf64-137">Leave the other options at the default values and use the **Select** button to save the cluster type.</span></span>

        ![叢集類型刀鋒視窗螢幕擷取畫面](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="5bf64-139">輸入 [叢集登入使用者名稱] 和 [叢集登入密碼]。</span><span class="sxs-lookup"><span data-stu-id="5bf64-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="5bf64-140">指定 [SSH 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="5bf64-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="5bf64-141">透過**安全殼層 (SSH)** 用戶端從遠端連線到叢集時，會使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="5bf64-141">SSH is used to remotely connect to the cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="5bf64-142">您可以在這個對話方塊中指定 SSH 使用者，或是在叢集建立之後指定 (於叢集的 [組態] 索引標籤中)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-142">You can either specify the SSH user in this dialog or after the cluster has been created (in the Configuration tab for the cluster).</span></span> <span data-ttu-id="5bf64-143">R Server 的設定會預期 “remoteuser” 的 **SSH 使用者名稱**。</span><span class="sxs-lookup"><span data-stu-id="5bf64-143">R Server is configured to expect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="5bf64-144">**如果您使用不同的使用者名稱，就必須在叢集建立之後執行額外步驟。**</span><span class="sxs-lookup"><span data-stu-id="5bf64-144">**If you use a different username, you must perform an additional step after the cluster is created.**</span></span>

    <span data-ttu-id="5bf64-145">除非您偏好使用公開金鑰，否則，請讓 [使用與叢集登入相同的密碼] 方塊保持勾選狀態以使用**密碼**。</span><span class="sxs-lookup"><span data-stu-id="5bf64-145">Leave the box checked for **Use same password as cluster login** to use **PASSWORD** as the authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="5bf64-146">您需要公開/私密金鑰組，透過遠端用戶端 (例如 RTVS、RStudio 或其他桌面整合式開發環境 (IDE)) 來存取叢集上的 R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bf64-146">You need a public/private key pair to access R Server on the cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="5bf64-147">如果您安裝 RStudio Server Community 版本，則必須選擇 SSH 密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf64-147">If you install the RStudio Server community edition, you need to choose an SSH password.</span></span>     

    <span data-ttu-id="5bf64-148">若要建立並使用公開/私密金鑰組，請將 [使用與叢集登入相同的密碼] 取消核取，然後選取 [公開金鑰]，並以如下方式繼續進行。</span><span class="sxs-lookup"><span data-stu-id="5bf64-148">To create and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="5bf64-149">這些指示會假設您已安裝 Cygwin 和 ssh-keygen 或具同等效力的命令。</span><span class="sxs-lookup"><span data-stu-id="5bf64-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="5bf64-150">從膝上型電腦上的命令提示字元產生公開/私密金鑰組︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-150">Generate a public/private key pair from the command prompt on your laptop:</span></span>

        <span data-ttu-id="5bf64-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="5bf64-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="5bf64-152">依照提示來為金鑰檔命名，然後輸入複雜密碼來提高安全性。</span><span class="sxs-lookup"><span data-stu-id="5bf64-152">Follow the prompt to name a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="5bf64-153">您的畫面應該看起來如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="5bf64-153">Your screen should look something like the following image:</span></span>

        ![Windows 中的 SSH 命令列](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="5bf64-155">此命令在 <private-key-filename>.pub 名稱下方建立私密金鑰檔案和公開金鑰檔案，例如 furiosa 和 furiosa.pub。</span><span class="sxs-lookup"><span data-stu-id="5bf64-155">This command creates a private key file and a public key file under the name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="5bf64-157">接著在指派 HDI 叢集認證時，指定公開金鑰檔案 (&#42;.pub)，最後確認您的資源群組和區域，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5bf64-157">Then specify the public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![認證刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="5bf64-159">在膝上型電腦上變更私密金鑰檔案的權限：</span><span class="sxs-lookup"><span data-stu-id="5bf64-159">Change permissions on the private keyfile on your laptop:</span></span>

        <span data-ttu-id="5bf64-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="5bf64-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="5bf64-161">使用私密金鑰檔案搭配 SSH 進行遠端登入：</span><span class="sxs-lookup"><span data-stu-id="5bf64-161">Use the private key file with SSH for remote login:</span></span>

        <span data-ttu-id="5bf64-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="5bf64-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="5bf64-163">或者，在用戶端上作為 R 伺服器 Hadoop Spark 計算內容的一部分。</span><span class="sxs-lookup"><span data-stu-id="5bf64-163">Or, as part the definition of your Hadoop Spark compute context for R Server on the client.</span></span> <span data-ttu-id="5bf64-164">請參閱[建立 Spark 的計算內容](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)中的**使用 Microsoft R 伺服器作為 Hadoop 用戶端**小節。</span><span class="sxs-lookup"><span data-stu-id="5bf64-164">See the **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="5bf64-165">快速建立會將您轉換到 [儲存體] 刀鋒視窗，以選取要用於叢集所使用之 HDFS 檔案系統主要位置的儲存體帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="5bf64-165">The quick create transitions you to the **Storage** blade to select the storage account settings to be used for the primary location of the HDFS file system used by the cluster.</span></span> <span data-ttu-id="5bf64-166">選取新的或現有的 Azure 儲存體帳戶或現有的 Data Lake 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="5bf64-167">如果您選取 Azure 儲存體帳戶，可藉由選擇 [選取儲存體帳戶]，然後選取相關的帳戶，來選取現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting the relevant account.</span></span> <span data-ttu-id="5bf64-168">使用 [選取儲存體帳戶] 區段中的 [新建] 連結，可建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-168">Create a new account using the **Create New** link in the **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5bf64-169">如果您選取 [新增]，則必須輸入新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf64-169">If you select **New** you must enter a name for the new storage account.</span></span> <span data-ttu-id="5bf64-170">如果可接受該名稱，就會出現綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="5bf64-170">A green check appears if the name is accepted.</span></span>

      <span data-ttu-id="5bf64-171">[預設容器] 的預設值為叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="5bf64-171">The **Default Container** defaults to the name of the cluster.</span></span> <span data-ttu-id="5bf64-172">請不要更動此預設值。</span><span class="sxs-lookup"><span data-stu-id="5bf64-172">Leave this default as the value.</span></span>

      <span data-ttu-id="5bf64-173">如果選取新的儲存體帳戶選項，則會出現選取 [位置] 的提示，供您選取要在其中建立儲存體帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="5bf64-173">If a new storage account option was selected a prompt to select **Location** is given to select which region to create the storage account.</span></span>  

         ![資料來源刀鋒視窗](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="5bf64-175">選取預設資料來源位置的同時，也會設定 HDInsight 叢集位置。</span><span class="sxs-lookup"><span data-stu-id="5bf64-175">Selecting the location for the default data source  also sets the location of the HDInsight cluster.</span></span> <span data-ttu-id="5bf64-176">叢集和預設資料來源必須位於相同區域中。</span><span class="sxs-lookup"><span data-stu-id="5bf64-176">The cluster and default data source must be in the same region.</span></span>

    - <span data-ttu-id="5bf64-177">如果您想要使用現有 Data Lake Store，則請選取要使用的 ADLS 儲存體帳戶，並將叢集 ADD 身分識別新增到叢集中，以允許存取存放區。</span><span class="sxs-lookup"><span data-stu-id="5bf64-177">If you want to use an existing Data Lake Store, then select the ADLS storage account to use and add the cluster *ADD* identity to your cluster to allow access to the store.</span></span> <span data-ttu-id="5bf64-178">如需此程序的詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="5bf64-179">使用 [選取]  按鈕以儲存資料來源設定。</span><span class="sxs-lookup"><span data-stu-id="5bf64-179">Use the **Select** button to save the data source configuration.</span></span>


7. <span data-ttu-id="5bf64-180">接著會顯示 [摘要] 刀鋒視窗，來驗證您的所有設定。</span><span class="sxs-lookup"><span data-stu-id="5bf64-180">The **Summary** blade then displays to validate all your settings.</span></span> <span data-ttu-id="5bf64-181">您可以在這裡變更**叢集大小**來修改叢集中的伺服器數目，同時指定任何您想要執行的**指令碼動作**。</span><span class="sxs-lookup"><span data-stu-id="5bf64-181">Here you can change your **Cluster size** to modify the number of servers in your cluster and also specify any **Script actions** you want to run.</span></span> <span data-ttu-id="5bf64-182">除非您確定需要更大的叢集，否則請保留背景工作節點數目的預設值 `4`。</span><span class="sxs-lookup"><span data-stu-id="5bf64-182">Unless you know that you need a larger cluster, leave the number of worker nodes at the default of `4`.</span></span> <span data-ttu-id="5bf64-183">該叢集的預估成本將會顯示在此刀鋒視窗內。</span><span class="sxs-lookup"><span data-stu-id="5bf64-183">The estimated cost of the cluster is shown within the blade.</span></span>

    ![叢集摘要](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="5bf64-185">如有需要，您可以在稍後透過入口網站來重新調整叢集的大小 ([叢集] -> [設定] -> [調整叢集])，以增加或減少背景工作角色節點的數目。</span><span class="sxs-lookup"><span data-stu-id="5bf64-185">If needed, you can resize your cluster later through the Portal (**Cluster** -> **Settings** -> **Scale Cluster**) to increase or decrease the number of worker nodes.</span></span>  <span data-ttu-id="5bf64-186">此大小調整有助於讓未使用的叢集閒置下來，或增加容量以滿足大型工作的需求。</span><span class="sxs-lookup"><span data-stu-id="5bf64-186">This resizing can be useful for idling down the cluster when not in use, or for adding capacity to meet the needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="5bf64-187">在調整叢集大小、資料節點和邊緣節點時，請將一些因素納入考量，包括︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-187">Some factors to keep in mind when sizing your cluster, the data nodes, and the edge node include:</span></span>  

   * <span data-ttu-id="5bf64-188">資料很大時，Spark 上分散式 R 伺服器分析的效能與背景工作節點數目成正比。</span><span class="sxs-lookup"><span data-stu-id="5bf64-188">The performance of distributed R Server analyses on Spark is proportional to the number of worker nodes when the data is large.</span></span>  

   * <span data-ttu-id="5bf64-189">R 伺服器分析的效能與分析的資料大小呈線性關係。</span><span class="sxs-lookup"><span data-stu-id="5bf64-189">The performance of R Server analyses is linear in the size of data being analyzed.</span></span> <span data-ttu-id="5bf64-190">例如：</span><span class="sxs-lookup"><span data-stu-id="5bf64-190">For example:</span></span>  

     * <span data-ttu-id="5bf64-191">對於小型到中型的資料，在邊緣節點上的本機計算內容中進行分析時，會獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="5bf64-191">For small to modest data, performance is best when analyzed in a local compute context on the edge node.</span></span>  <span data-ttu-id="5bf64-192">如需有關本機和 Spark 計算內容最適合之案例的詳細資訊，請參閱在 HDInsight 上 R 伺服器的計算內容選項。</span><span class="sxs-lookup"><span data-stu-id="5bf64-192">For more information on the scenarios under which the local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="5bf64-193">如果您登入邊緣節點中，並執行 R 指令碼，則會在邊緣節點上<strong>本機</strong>執行 ScaleR rx- 之外的所有函式。</span><span class="sxs-lookup"><span data-stu-id="5bf64-193">If you log in to the edge node and run your R script, then all but the ScaleR rx-functions are executed <strong>locally</strong> on the edge node.</span></span> <span data-ttu-id="5bf64-194">因此記憶體和邊緣節點的核心數目應該要據此調整大小。</span><span class="sxs-lookup"><span data-stu-id="5bf64-194">So the memory and number of cores of the edge node should be sized accordingly.</span></span> <span data-ttu-id="5bf64-195">如果您在 HDI 上將 R Server 當做膝上型電腦的遠端計算內容，也適用相同原則。</span><span class="sxs-lookup"><span data-stu-id="5bf64-195">The same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="5bf64-197">使用 [選取]  按鈕以儲存節點定價設定。</span><span class="sxs-lookup"><span data-stu-id="5bf64-197">Use the **Select** button to save the node pricing configuration.</span></span>

   <span data-ttu-id="5bf64-198">還有 [下載範本和參數] 的連結。</span><span class="sxs-lookup"><span data-stu-id="5bf64-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="5bf64-199">按一下此連結，會顯示可用來以所選設定自動建立叢集的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5bf64-199">Click on this link to display scripts that can be used to automate the creation of a cluster with the selected configuration.</span></span> <span data-ttu-id="5bf64-200">這些指令碼在建立好之後，也可透過 Azure 入口網站項目來取得以供叢集使用。</span><span class="sxs-lookup"><span data-stu-id="5bf64-200">These scripts are also available from the Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bf64-201">建立叢集需要一些時間，通常約 20 分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="5bf64-201">It takes some time for the cluster to be created, usually around 20 minutes.</span></span> <span data-ttu-id="5bf64-202">請使用「開始面板」上的圖格，或頁面左邊的 [通知]  項目來以檢查建立進度。</span><span class="sxs-lookup"><span data-stu-id="5bf64-202">Use the tile on the Startboard, or the **Notifications** entry on the left of the page to check on the creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a><span data-ttu-id="5bf64-203">連線到 RStudio 伺服器</span><span class="sxs-lookup"><span data-stu-id="5bf64-203">Connect to RStudio Server</span></span>

<span data-ttu-id="5bf64-204">如果您已選擇要在安裝中包含 RStudio 伺服器 Community 版本，您就可以透過兩種不同方法存取 RStudio 登入。</span><span class="sxs-lookup"><span data-stu-id="5bf64-204">If you’ve chosen to include RStudio Server community edition in your installation, then you can access the RStudio login via two different methods.</span></span>

1. <span data-ttu-id="5bf64-205">移至下列 URL (其中 **CLUSTERNAME** 是您所建立的叢集名稱)：</span><span class="sxs-lookup"><span data-stu-id="5bf64-205">Go to the following URL (where **CLUSTERNAME** is the name of the cluster you've created):</span></span>

    <span data-ttu-id="5bf64-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="5bf64-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="5bf64-207">在 Azure 入口網站中開啟叢集項目，選取 [R Server 儀表板] 快速連結，然後選取 [R Studio 儀表板]︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-207">Open the entry for your cluster in the Azure portal, select the **R Server Dashboards** quick link and then selecting the **R Studio Dashboard**:</span></span>

     ![存取 R Studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![存取 R Studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="5bf64-210">不論使用哪一種方法，第一次登入時都必須驗證兩次。</span><span class="sxs-lookup"><span data-stu-id="5bf64-210">Regardless of the method used, the first time you log in you need to authenticate twice.</span></span>  <span data-ttu-id="5bf64-211">第一次驗證時，請提供「叢集管理員的使用者識別碼」和「密碼」。</span><span class="sxs-lookup"><span data-stu-id="5bf64-211">At the first authentication, provide the *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="5bf64-212">第二次提示時，則提供「SSH 使用者識別碼」和「密碼」。</span><span class="sxs-lookup"><span data-stu-id="5bf64-212">At the second prompt, provide the *SSH userid* and *password*.</span></span> <span data-ttu-id="5bf64-213">之後再登入時，只需要提供「SSH 密碼」和「使用者識別碼」。</span><span class="sxs-lookup"><span data-stu-id="5bf64-213">Subsequent log ins only require the *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a><span data-ttu-id="5bf64-214">連線到 R Server 邊緣節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-214">Connect to the R Server edge node</span></span>

<span data-ttu-id="5bf64-215">使用 SSH 搭配命令，連線到 HDInsight 叢集的 R Server 邊緣節點：</span><span class="sxs-lookup"><span data-stu-id="5bf64-215">Connect to R Server edge node of the HDInsight cluster using SSH with the command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="5bf64-216">您可以依序選取您的叢集、[所有設定] -> [應用程式] -> [RServer]，在 Azure 入口網站中找到 `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` 位址。</span><span class="sxs-lookup"><span data-stu-id="5bf64-216">You can find the `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in the Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="5bf64-217">如此即可顯示邊緣節點的 SSH 端點資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf64-217">This displays the SSH Endpoint information for the edge node.</span></span>
>
> ![邊緣節點 SSH 端點的影像](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="5bf64-219">如果您已經使用密碼保護您 SSH 使用者帳戶的安全，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="5bf64-219">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="5bf64-220">如果您使用的是公開金鑰，您可能必須使用 `-i` 參數來指定對應的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bf64-220">If you used a public key, you may have to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="5bf64-221">例如：</span><span class="sxs-lookup"><span data-stu-id="5bf64-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="5bf64-222">如需詳細資訊，請參閱[使用 SSH 連線至 HDInsight (Hadoop)](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-222">For more information, see [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="5bf64-223">連線之後，您將看見類似以下的提示：</span><span class="sxs-lookup"><span data-stu-id="5bf64-223">Once connected, you arrive at a prompt similar to the following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="5bf64-224">啟用多個並行使用者</span><span class="sxs-lookup"><span data-stu-id="5bf64-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="5bf64-225">藉由為 RStudio 社群版本執行所在的邊緣節點新增更多使用者，即可啟用多個並行使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-225">You can enable multiple concurrent users by adding more users for the edge node on which the RStudio community version runs.</span></span>

<span data-ttu-id="5bf64-226">當您建立 HDInsight 叢集時，您必須提供兩個使用者 (HTTP 使用者和 SSH 使用者)：</span><span class="sxs-lookup"><span data-stu-id="5bf64-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![並行使用者 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="5bf64-228">**叢集登入使用者名稱**：透過 HDInsight 閘道 (用來保護您所建立的 HDInsight 叢集) 進行驗證的 HTTP 使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-228">**Cluster login username**: an HTTP user for authentication through the HDInsight gateway that is used to protect the HDInsight clusters you created.</span></span> <span data-ttu-id="5bf64-229">此 HTTP 使用者用於存取 Ambari UI、YARN UI，以及其他 UI 元件。</span><span class="sxs-lookup"><span data-stu-id="5bf64-229">This HTTP user is used to access the Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="5bf64-230">**安全殼層 (SSH) 使用者名稱**：透過安全殼層存取叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-230">**Secure Shell (SSH) username**: an SSH user to access the cluster through secure shell.</span></span> <span data-ttu-id="5bf64-231">此使用者是在 Linux 系統中適用於所有前端節點、背景工作節點和邊緣節點的使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-231">This user is a user in the Linux system for all the head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="5bf64-232">因此您可以使用安全殼層來存取遠端叢集中的任何節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-232">So you can use secure shell to access any of the nodes in a remote cluster.</span></span>

<span data-ttu-id="5bf64-233">用於 HDInsight 叢集上 Microsoft R Server 中的 R Studio Server 社群版本，只接受 Linux 使用者名稱和密碼作為登入機制。</span><span class="sxs-lookup"><span data-stu-id="5bf64-233">The R Studio Server Community version used in the Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="5bf64-234">但不支援傳遞權杖。</span><span class="sxs-lookup"><span data-stu-id="5bf64-234">It does not support passing tokens.</span></span> <span data-ttu-id="5bf64-235">因此如果您已建立新叢集，而且想要使用 R Studio 來存取它，您需要登入兩次。</span><span class="sxs-lookup"><span data-stu-id="5bf64-235">So if you have created a new cluster and want to use R Studio to access it, you need to log in twice.</span></span>

- <span data-ttu-id="5bf64-236">先透過 HDInsight 閘道使用 HTTP 使用者認證登入：</span><span class="sxs-lookup"><span data-stu-id="5bf64-236">First log in using the HTTP user credentials through the HDInsight Gateway:</span></span> 

    ![並行使用者 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="5bf64-238">然後使用 SSH 使用者認證來登入 RStudio：</span><span class="sxs-lookup"><span data-stu-id="5bf64-238">Then use the SSH user credentials to log in to RStudio:</span></span>
  
    ![並行使用者 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="5bf64-240">目前，在佈建 HDInsight 叢集時，只可以建立一個 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bf64-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="5bf64-241">因此若要讓多個使用者存取 HDInsight 叢集上的 Microsoft R Server，我們必須在 Linux 系統中建立其他使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-241">So to enable multiple users to access Microsoft R Server on HDInsight clusters, we need to create additional users in the Linux system.</span></span>

<span data-ttu-id="5bf64-242">因為 RStudio Server 社群正在叢集的邊緣節點上執行，所以有以下幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="5bf64-242">Because RStudio Server Community is running on the cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="5bf64-243">使用所建立的 SSH 使用者來登入邊緣節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-243">Use the created SSH user to log in to the edge node</span></span>
2. <span data-ttu-id="5bf64-244">在邊緣節點中新增更多 Linux 使用者</span><span class="sxs-lookup"><span data-stu-id="5bf64-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="5bf64-245">使用 RStudio 社群版本搭配所建立的使用者</span><span class="sxs-lookup"><span data-stu-id="5bf64-245">Use RStudio Community version with the user created</span></span>

### <a name="step-1-use-the-created-ssh-user-to-log-in-to-the-edge-node"></a><span data-ttu-id="5bf64-246">步驟 1：使用所建立的 SSH 使用者來登入邊緣節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-246">Step 1: Use the created SSH user to log in to the edge node</span></span>

<span data-ttu-id="5bf64-247">下載任何 SSH 工具 (例如 Putty) 並使用現有的 SSH 使用者進行登入。</span><span class="sxs-lookup"><span data-stu-id="5bf64-247">Download any SSH tool (such as Putty) and use the existing SSH user to log in.</span></span> <span data-ttu-id="5bf64-248">然後遵循[使用 SSH 連線到 HDInsight (Hadoop)](hdinsight-hadoop-linux-use-ssh-unix.md) 中提供的指示來存取邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-248">Then follow the instructions provided in [Connect to HDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) to access the edge node.</span></span> <span data-ttu-id="5bf64-249">HDInsight 叢集上 R Server 的邊緣節點位址是：*clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="5bf64-249">The edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="5bf64-250">步驟 2：在邊緣節點中新增更多 Linux 使用者</span><span class="sxs-lookup"><span data-stu-id="5bf64-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="5bf64-251">若要將使用者新增至邊緣節點，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-251">To add a user to the edge node, execute the commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="5bf64-252">您應該會看見下列傳回的項目：</span><span class="sxs-lookup"><span data-stu-id="5bf64-252">You should see the following items returned:</span></span> 

![並行使用者 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="5bf64-254">當系統提示您輸入 [目前的 Kerberos 密碼] 時，只要按 **Enter** 加以忽略。</span><span class="sxs-lookup"><span data-stu-id="5bf64-254">When prompted for “Current Kerberos password:”, just press **Enter** to ignore it.</span></span> <span data-ttu-id="5bf64-255">`useradd` 命令中的 `-m` 選項表示系統將為使用者建立主資料夾，這是 RStudio 社群版本所需的。</span><span class="sxs-lookup"><span data-stu-id="5bf64-255">The `-m` option in `useradd` command indicates that the system will create a home folder for the user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-the-user-created"></a><span data-ttu-id="5bf64-256">步驟 3：使用 RStudio 社群版本搭配建立的使用者</span><span class="sxs-lookup"><span data-stu-id="5bf64-256">Step 3: Use RStudio Community version with the user created</span></span>

<span data-ttu-id="5bf64-257">使用所建立的使用者來登入 RStudio：</span><span class="sxs-lookup"><span data-stu-id="5bf64-257">Use the user created to log in to RStudio:</span></span>

![並行使用者 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="5bf64-259">請注意，RStudio 指出您使用新的使用者 (例如，這裡的 *sshuser6*) 來登入叢集：</span><span class="sxs-lookup"><span data-stu-id="5bf64-259">Notice that RStudio indicates that you are using the new user (here, for example, *sshuser6*) to log in the cluster:</span></span> 

![並行使用者 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="5bf64-261">您也可以使用原始認證 (預設是 sshuser)，從另一個瀏覽器視窗同時登入。</span><span class="sxs-lookup"><span data-stu-id="5bf64-261">You can also log in using the original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="5bf64-262">您可以使用 scaleR 函式來提交作業。</span><span class="sxs-lookup"><span data-stu-id="5bf64-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="5bf64-263">以下是用來執行作業的命令範例：</span><span class="sxs-lookup"><span data-stu-id="5bf64-263">Here is an example of the commands used to run a job:</span></span>

    # Set the HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot to load the data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory.
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for the airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names.
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context.
    mySparkCluster <- RxSpark()

    # Set the compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="5bf64-264">請注意，提交的作業位於 YARN UI 中的不同使用者名稱之下：</span><span class="sxs-lookup"><span data-stu-id="5bf64-264">Notice that the jobs submitted are under different user names in YARN UI:</span></span>

![並行使用者 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="5bf64-266">也請注意，新增的使用者在 Linux 系統中沒有根權限，但是他們對遠端 HDFS 與 WASB 儲存體中的所有檔案具有相同的存取權。</span><span class="sxs-lookup"><span data-stu-id="5bf64-266">Note also that the newly added users do not have root privileges in Linux system, but they do have the same access to all the files in the remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a><span data-ttu-id="5bf64-267">使用 R 主控台</span><span class="sxs-lookup"><span data-stu-id="5bf64-267">Use the R console</span></span>

1. <span data-ttu-id="5bf64-268">在 SSH 工作階段中，使用以下命令啟動 R 主控台：</span><span class="sxs-lookup"><span data-stu-id="5bf64-268">From the SSH session, use the following command to start the R console:</span></span>  

        R

2. <span data-ttu-id="5bf64-269">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="5bf64-269">You should see output similar to the following:</span></span>
    
    <span data-ttu-id="5bf64-270">R 版本 3.2.2 (2015-08-14) -- "Fire Safety" Copyright (C) 2015 統計計算平台的 R 基礎：x86_64-pc-linux-gnu (64 位元)</span><span class="sxs-lookup"><span data-stu-id="5bf64-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 The R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="5bf64-271">R 是免費的軟體，且「絕對無瑕疵責任擔保」。</span><span class="sxs-lookup"><span data-stu-id="5bf64-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="5bf64-272">您可以在特定情況下隨意地將其重新發佈。</span><span class="sxs-lookup"><span data-stu-id="5bf64-272">You are welcome to redistribute it under certain conditions.</span></span>
    <span data-ttu-id="5bf64-273">輸入 'license()' 或 'licence()' 可取得發佈詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5bf64-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="5bf64-274">支援自然語言，但是在英文地區設定中執行</span><span class="sxs-lookup"><span data-stu-id="5bf64-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="5bf64-275">R 是共同作業專案，具有許多的參與者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="5bf64-276">如需詳細資訊，請輸入 'contributors()'，若要了解如何在發行集內引用 R 或 R 套件，請輸入 'citation()'。</span><span class="sxs-lookup"><span data-stu-id="5bf64-276">Type 'contributors()' for more information and 'citation()' on how to cite R or R packages in publications.</span></span>

    <span data-ttu-id="5bf64-277">輸入 'demo()' 可取得一些示範、輸入 'help()' 可取得線上說明，或輸入 'help.start()' 可取得要說明的 HTML 瀏覽器介面。</span><span class="sxs-lookup"><span data-stu-id="5bf64-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface to help.</span></span>
    <span data-ttu-id="5bf64-278">輸入 'q()' 可結束 R。</span><span class="sxs-lookup"><span data-stu-id="5bf64-278">Type 'q()' to quit R.</span></span>

    <span data-ttu-id="5bf64-279">Microsoft R 伺服器 8.0 版：R 的增強發佈 Microsoft 套件 Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="5bf64-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="5bf64-280">輸入 'readme()' 可取得版本資訊。</span><span class="sxs-lookup"><span data-stu-id="5bf64-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="5bf64-281">您可以透過 `>` 提示，輸入 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="5bf64-281">From the `>` prompt, you can enter R code.</span></span> <span data-ttu-id="5bf64-282">R Server 包含可讓您輕鬆與 Hadoop 互動並執行分散式計算的封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf64-282">R server includes packages that allow you to easily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="5bf64-283">例如，若要檢視 HDInsight 叢集的預設檔案系統根目錄，可使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5bf64-283">For example, use the following command to view the root of the default file system for the HDInsight cluster:</span></span>

    <span data-ttu-id="5bf64-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="5bf64-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="5bf64-285">您也可以使用 WASB 樣式定址。</span><span class="sxs-lookup"><span data-stu-id="5bf64-285">You can also use the WASB style addressing.</span></span>

    <span data-ttu-id="5bf64-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="5bf64-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="5bf64-287">從 Microsoft R Server 或 Microsoft R Client 的遠端執行個體使用 HDI 上的 R Server</span><span class="sxs-lookup"><span data-stu-id="5bf64-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="5bf64-288">可以設定從桌上型電腦或膝上型電腦上執行的 Microsoft R Server 或 Microsoft R Client 的遠端執行個體，存取 HDI Hadoop Spark 計算內容。</span><span class="sxs-lookup"><span data-stu-id="5bf64-288">It is possible to set up access to the HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="5bf64-289">請參閱[建立 Spark 的計算內容](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)中的**使用 Microsoft R 伺服器作為 Hadoop 用戶端**小節。</span><span class="sxs-lookup"><span data-stu-id="5bf64-289">See **Using Microsoft R Server as a Hadoop Client** subsection in the [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="5bf64-290">若要這樣做，在膝上型電腦上定義 RxSpark 計算內容時，您需要指定下列選項︰hdfsShareDir、shareDir、sshUsername、sshHostname、sshSwitches 和 sshProfileScript。</span><span class="sxs-lookup"><span data-stu-id="5bf64-290">To do so, you need to specify the following options when defining the RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="5bf64-291">例如：</span><span class="sxs-lookup"><span data-stu-id="5bf64-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="5bf64-292">使用計算內容</span><span class="sxs-lookup"><span data-stu-id="5bf64-292">Use a compute context</span></span>

<span data-ttu-id="5bf64-293">計算內容可讓您控制要在邊緣節點上本機執行計算，或散發到 HDInsight 叢集的節點中。</span><span class="sxs-lookup"><span data-stu-id="5bf64-293">A compute context allows you to control whether computation is performed locally on the edge node or distributed across the nodes in the HDInsight cluster.</span></span>

1. <span data-ttu-id="5bf64-294">在 RStudio Server 或 R 主控台 (在 SSH 工作階段中) 中，使用下列程式碼將範例資料載入 HDInsight 的預設儲存體中：</span><span class="sxs-lookup"><span data-stu-id="5bf64-294">From RStudio Server or the R console (in an SSH session), use the following code to load example data into the default storage for HDInsight:</span></span>

        # Set the HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="5bf64-295">接下來，我們要建立一些資料資訊，並定義兩個資料來源，以便使用資料。</span><span class="sxs-lookup"><span data-stu-id="5bf64-295">Next, let's create some data info and define two data sources so that we can work with the data.</span></span>

        # Define the HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="5bf64-296">現在，我們來使用本機計算內容執行資料的羅吉斯迴歸。</span><span class="sxs-lookup"><span data-stu-id="5bf64-296">Let's run a logistic regression over the data using the local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="5bf64-297">您應該會看到結尾類似以下幾行的輸出：</span><span class="sxs-lookup"><span data-stu-id="5bf64-297">You should see output that ends with lines similar to the following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="5bf64-298">接著，我們使用 Spark 內容來執行相同的羅吉斯迴歸。</span><span class="sxs-lookup"><span data-stu-id="5bf64-298">Next, let's run the same logistic regression using the Spark context.</span></span> <span data-ttu-id="5bf64-299">Spark 內容會將處理作業散發到 HDInsight 叢集的所有背景工作節點中。</span><span class="sxs-lookup"><span data-stu-id="5bf64-299">The Spark context distributes the processing over all the worker nodes in the HDInsight cluster.</span></span>

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="5bf64-300">您也可以使用 MapReduce，將計算分散到叢集節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-300">You can also use MapReduce to distribute computation across cluster nodes.</span></span> <span data-ttu-id="5bf64-301">如需計算內容的詳細資訊，請參閱[適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-to-multiple-nodes"></a><span data-ttu-id="5bf64-302">將 R 程式碼分散到多個節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-302">Distribute R code to multiple nodes</span></span>

<span data-ttu-id="5bf64-303">使用 R 伺服器時，您可以輕鬆採用現有的 R 程式碼並利用 `rxExec` 跨多個叢集節點執行。</span><span class="sxs-lookup"><span data-stu-id="5bf64-303">With R Server, you can easily take existing R code and run it across multiple nodes in the cluster by using `rxExec`.</span></span> <span data-ttu-id="5bf64-304">執行參數掃掠或模擬時，這個函式非常有用。</span><span class="sxs-lookup"><span data-stu-id="5bf64-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="5bf64-305">以下是使用 `rxExec` 的範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="5bf64-305">The following code is an example of how to use `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="5bf64-306">如果您仍在使用 Spark 或 MapReduce 內容，此命令會針對執行程式碼 `(Sys.info()["nodename"])` 的背景工作節點傳回 nodename 值。</span><span class="sxs-lookup"><span data-stu-id="5bf64-306">If you are still using the Spark or MapReduce context, this  command returns the nodename value for the worker nodes that the code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="5bf64-307">例如，若是在四個節點叢集上，您應會收到類似下列的輸出：</span><span class="sxs-lookup"><span data-stu-id="5bf64-307">For example, on a four node cluster, you expect to receive output similar to the following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="5bf64-308">存取 Hive 和 Parquet 中的資料</span><span class="sxs-lookup"><span data-stu-id="5bf64-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="5bf64-309">R 伺服器 9.1 版所提供的功能，可讓您直接存取 Hive 和 Parquet 中的資料，以供 ScaleR 函式用於 Spark 計算內容中。</span><span class="sxs-lookup"><span data-stu-id="5bf64-309">A feature available in R Server 9.1 allows direct access to data in Hive and Parquet for use by ScaleR functions in the Spark compute context.</span></span> <span data-ttu-id="5bf64-310">這些功能可透過新的 ScaleR 資料來源函式 (稱為 RxHiveData 和 RxParquetData) 來使用，而透過使用 Spark SQL 將資料直接載入到 Spark 資料框架供 ScaleR 進行分析，即可讓這些函式運作。</span><span class="sxs-lookup"><span data-stu-id="5bf64-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL to load data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="5bf64-311">下面程式碼提供一些關於新函式使用方式的範例程式碼︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-311">The following code provides some sample code on use of the new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close the Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="5bf64-312">如需如何使用這些新函式的詳細資訊，請透過使用 `?RxHivedata` 和 `?RxParquetData` 命令參閱 R 伺服器中的線上說明。</span><span class="sxs-lookup"><span data-stu-id="5bf64-312">For additional info on use of these new functions see the online help in R Server through use of the `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-the-edge-node"></a><span data-ttu-id="5bf64-313">在邊緣節點上安裝其他 R 套件</span><span class="sxs-lookup"><span data-stu-id="5bf64-313">Install additional R packages on the edge node</span></span>

<span data-ttu-id="5bf64-314">如果您想要在邊緣節點上安裝其他 R 套件，可以在透過 SSH 連線至邊緣節點時，直接從 R 主控台內使用 `install.packages()` 。</span><span class="sxs-lookup"><span data-stu-id="5bf64-314">If you would like to install additional R packages on the edge node, you can use `install.packages()` directly from within the R console when connected to the edge node through SSH.</span></span> <span data-ttu-id="5bf64-315">不過，如果您需要在叢集的背景工作節點上安裝 R 封裝，就必須使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5bf64-315">However, if you need to install R packages on the worker nodes of the cluster, you must use a Script Action.</span></span>

<span data-ttu-id="5bf64-316">指令碼動作是一種 Bash 指令碼，可用來變更 HDInsight 叢集的設定或安裝其他軟體，例如其他 R 套件。</span><span class="sxs-lookup"><span data-stu-id="5bf64-316">Script Actions are Bash scripts that are used to make configuration changes to the HDInsight cluster or to install additional software, such as additional R packages.</span></span> <span data-ttu-id="5bf64-317">若要使用指令碼動作安裝其他套件，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5bf64-317">To install additional packages using a Script Action, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bf64-318">僅有在建立叢集之後，才可以使用指令碼動作來安裝其他 R 封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf64-318">Using Script Actions to install additional R packages can only be used after the cluster has been created.</span></span> <span data-ttu-id="5bf64-319">在叢集建立期間，請勿使用此程序，因為指令碼是相依於已完整安裝與設定的 R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bf64-319">Do not use this procedure during cluster creation, as the script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="5bf64-320">從 [Azure 入口網站](https://portal.azure.com)選取您 HDInsight 叢集上的 R Server。</span><span class="sxs-lookup"><span data-stu-id="5bf64-320">From the [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="5bf64-321">在 [設定] 刀鋒視窗中，依序選取 [指令碼動作] 和 [提交新的]，以提交新的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="5bf64-321">From the **Settings** blade, select **Script Actions** and then **Submit New** to submit a new Script Action.</span></span>

   ![指令碼動作刀鋒視窗的影像](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="5bf64-323">在 [提交指令碼動作] 刀鋒視窗中，提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5bf64-323">From the **Submit script action** blade, provide the following information:</span></span>

   * <span data-ttu-id="5bf64-324">**名稱**︰識別此指令碼的易記名稱</span><span class="sxs-lookup"><span data-stu-id="5bf64-324">**Name**: A friendly name to identify this script</span></span>

   * <span data-ttu-id="5bf64-325">**Bash 指令碼 URI**：`http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="5bf64-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="5bf64-326">**前端**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="5bf64-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="5bf64-327">**背景工作**︰此項目應該是**已核取**狀態</span><span class="sxs-lookup"><span data-stu-id="5bf64-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="5bf64-328">**邊緣節點**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="5bf64-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="5bf64-329">**Zookeeper**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="5bf64-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="5bf64-330">**參數**︰要安裝的 R 套件。</span><span class="sxs-lookup"><span data-stu-id="5bf64-330">**Parameters**: The R packages to be installed.</span></span> <span data-ttu-id="5bf64-331">例如， `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="5bf64-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="5bf64-332">**保存此指令碼...**︰此項目應該是**已核取**狀態</span><span class="sxs-lookup"><span data-stu-id="5bf64-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="5bf64-333">根據預設，會從與安裝之 R 伺服器同版本的 Microsoft MRAN 存放庫的快照安裝所有的 R 封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf64-333">By default, all R packages are installed from a snapshot of the Microsoft MRAN repository consistent with the version of R Server that has been installed.</span></span> <span data-ttu-id="5bf64-334">如果您想要安裝較新版的套件，則會有不相容的風險。</span><span class="sxs-lookup"><span data-stu-id="5bf64-334">If you want to install newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="5bf64-335">不過，將 `useCRAN` 指定為套件清單的第一個元素 (例如 `useCRAN bitops, stringr, arules`)，這種安裝就可行。</span><span class="sxs-lookup"><span data-stu-id="5bf64-335">However this kind of install is possible by specifying `useCRAN` as the first element of the package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="5bf64-336">有些 R 套件需要額外的 Linux 系統程式庫。</span><span class="sxs-lookup"><span data-stu-id="5bf64-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="5bf64-337">為了方便起見，我們已預先安裝前 100 個最受歡迎的 R 封裝所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="5bf64-337">For convenience, we have pre-installed the dependencies needed by the top 100 most popular R packages.</span></span> <span data-ttu-id="5bf64-338">然而，如果您安裝的 R 封裝需要的程式庫不在這之中，則必須下載此處所使用的基底指令碼，並加入安裝系統程式庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="5bf64-338">However, if the R package(s) you install require libraries beyond these then you must download the base script used here and add steps to install the system libraries.</span></span> <span data-ttu-id="5bf64-339">接下來，您必須將修改過的指令碼上傳至 Azure 儲存體中的公用 Blob 容器，並使用修改過的指令碼來安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="5bf64-339">You must then upload the modified script to a public blob container in Azure storage and use the modified script to install the packages.</span></span>
   >    <span data-ttu-id="5bf64-340">如需開發指令碼動作的詳細資訊，請參閱 [指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![新增指令碼動作](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="5bf64-342">按一下 [建立] 執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5bf64-342">Select **Create** to run the script.</span></span> <span data-ttu-id="5bf64-343">指令碼完成之後，即可在所有的背景工作角色節點上使用 R 套件。</span><span class="sxs-lookup"><span data-stu-id="5bf64-343">Once the script completes, the R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="5bf64-344">使用 Microsoft R 伺服器實作</span><span class="sxs-lookup"><span data-stu-id="5bf64-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="5bf64-345">完成資料模型化時，可以運作模型以進行預測。</span><span class="sxs-lookup"><span data-stu-id="5bf64-345">When your data modeling is complete, you can operationalize the model to make predictions.</span></span> <span data-ttu-id="5bf64-346">若要設定 Microsoft R Server 實作，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5bf64-346">To configure for Microsoft R Server operationalization, perform the following steps:</span></span>

<span data-ttu-id="5bf64-347">首先，透過 ssh 連線到邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-347">First, ssh into the Edge node.</span></span> <span data-ttu-id="5bf64-348">例如，</span><span class="sxs-lookup"><span data-stu-id="5bf64-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="5bf64-349">在使用 ssh 之後，請變更相關版本的目錄並對 dotnet dll 進行 sudo：</span><span class="sxs-lookup"><span data-stu-id="5bf64-349">After using ssh, change directory for the relevant version and sudo the dotnet dll:</span></span> 

- <span data-ttu-id="5bf64-350">對於 Microsoft R Server 9.1：</span><span class="sxs-lookup"><span data-stu-id="5bf64-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="5bf64-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="5bf64-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="5bf64-352">對於 Microsoft R Server 9.0：</span><span class="sxs-lookup"><span data-stu-id="5bf64-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="5bf64-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="5bf64-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="5bf64-354">若要使用一整體組態設定 Microsoft R 伺服器實作，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="5bf64-354">To configure Microsoft R Server operationalization with a One-box configuration do the following:</span></span>

1. <span data-ttu-id="5bf64-355">選取 [設定 R 伺服器來實施]</span><span class="sxs-lookup"><span data-stu-id="5bf64-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="5bf64-356">選取 A.</span><span class="sxs-lookup"><span data-stu-id="5bf64-356">Select “A.</span></span> <span data-ttu-id="5bf64-357">One-box (web + compute nodes)</span><span class="sxs-lookup"><span data-stu-id="5bf64-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="5bf64-358">輸入 **admin** 使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="5bf64-358">Enter a password for the **admin** user</span></span>

![one box op](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="5bf64-360">您也可以選擇性地執行診斷測試來執行診斷檢查，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5bf64-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="5bf64-361">選取 6.</span><span class="sxs-lookup"><span data-stu-id="5bf64-361">Select “6.</span></span> <span data-ttu-id="5bf64-362">Run diagnostic tests</span><span class="sxs-lookup"><span data-stu-id="5bf64-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="5bf64-363">選取 A.</span><span class="sxs-lookup"><span data-stu-id="5bf64-363">Select “A.</span></span> <span data-ttu-id="5bf64-364">Test configuration</span><span class="sxs-lookup"><span data-stu-id="5bf64-364">Test configuration”</span></span>
3. <span data-ttu-id="5bf64-365">輸入上述設定步驟中的使用者名稱 = “admin” 和密碼</span><span class="sxs-lookup"><span data-stu-id="5bf64-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="5bf64-366">確認整體健全狀況 = pass</span><span class="sxs-lookup"><span data-stu-id="5bf64-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="5bf64-367">結束系統管理公用程式</span><span class="sxs-lookup"><span data-stu-id="5bf64-367">Exit the Admin Utility</span></span>
6. <span data-ttu-id="5bf64-368">結束 SSH</span><span class="sxs-lookup"><span data-stu-id="5bf64-368">Exit SSH</span></span>

![實作的診斷](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="5bf64-370">**在 Spark 上取用 Web 服務時長時間延遲**</span><span class="sxs-lookup"><span data-stu-id="5bf64-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="5bf64-371">如果您在 Spark 計算環境中嘗試取用使用 mrsdeploy 函式建立的 Web 服務時，遇到長時間延遲，您可能需要新增一些遺漏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5bf64-371">If you encounter long delays when trying to consume a web service created with mrsdeploy functions in a Spark compute context, you may need to add some missing folders.</span></span> <span data-ttu-id="5bf64-372">每當使用 mrsdeploy 函式從 Web 服務叫用 Spark 應用程式時，該應用程式會屬於名為 'rserve2' 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5bf64-372">The Spark application belongs to a user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="5bf64-373">若要解決此問題：</span><span class="sxs-lookup"><span data-stu-id="5bf64-373">To work around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="5bf64-374">在這個階段，實作的組態已設定完成。</span><span class="sxs-lookup"><span data-stu-id="5bf64-374">At this stage, the configuration for Operationalization is complete.</span></span> <span data-ttu-id="5bf64-375">現在您可以在 RClient 上使用 'mrsdeploy' 套件來連線至邊緣節點上的實作，並開始使用其功能，像是[遠端執行](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution)和 [Web 服務](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-375">Now you can use the ‘mrsdeploy’ package on your RClient to connect to the Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="5bf64-376">根據叢集是否設定在虛擬網路上，您可能必須設定透過 SSH 登入的連接埠轉送通道。</span><span class="sxs-lookup"><span data-stu-id="5bf64-376">Depending on whether your cluster is set up on a virtual network or not, you may need to set up port forward tunneling through SSH login.</span></span> <span data-ttu-id="5bf64-377">下列各節說明如何設定此通道。</span><span class="sxs-lookup"><span data-stu-id="5bf64-377">The following sections explain how to set up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="5bf64-378">虛擬網路上的 RServer 叢集</span><span class="sxs-lookup"><span data-stu-id="5bf64-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="5bf64-379">確定您允許流量通過連接埠 12800 到達邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-379">Make sure you allow traffic through port 12800 to the edge node.</span></span> <span data-ttu-id="5bf64-380">這樣一來，您就可以使用 Edge 節點連線到實作功能。</span><span class="sxs-lookup"><span data-stu-id="5bf64-380">That way, you can use the edge node to connect to the Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="5bf64-381">如果 `remoteLogin()` 無法連線到邊緣節點，但您可以透過 SSH 連線到邊緣節點，則必須確認是否已正確設定在連接埠 12800 上允許流量的規則。</span><span class="sxs-lookup"><span data-stu-id="5bf64-381">If the `remoteLogin()` cannot connect to the edge node, but you can SSH to the edge node, then you need to verify whether the rule to allow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="5bf64-382">如果您持續遇到此問題，您可以藉由設定透過 SSH 的連接埠轉送通道來處理此問題。</span><span class="sxs-lookup"><span data-stu-id="5bf64-382">If you continue to face the issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="5bf64-383">如需相關指示，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="5bf64-383">For instructions, see the following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="5bf64-384">RServer 叢集未設定於虛擬網路上</span><span class="sxs-lookup"><span data-stu-id="5bf64-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="5bf64-385">如果您的叢集未設定於 vnet 上，或如果您在透過 vnet 連線時遇到問題，可以使用 SSH 連接埠轉送通道︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="5bf64-386">在 Putty 上，您也可以做此設定。</span><span class="sxs-lookup"><span data-stu-id="5bf64-386">On Putty, you can set it up as well.</span></span>

![putty ssh 連線](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="5bf64-388">SSH 工作階段變為作用中後，來自電腦連接埠 12800 的流量就會透過 SSH 工作階段轉送到邊緣節點的連接埠 12800。</span><span class="sxs-lookup"><span data-stu-id="5bf64-388">Once your SSH session is active, the traffic from your machine’s port 12800 is forwarded to the edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="5bf64-389">請務必在 `remoteLogin()` 方法中使用 `127.0.0.1:12800`。</span><span class="sxs-lookup"><span data-stu-id="5bf64-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="5bf64-390">這將透過連接埠轉送登入邊緣節點的實作中。</span><span class="sxs-lookup"><span data-stu-id="5bf64-390">This logs in to the edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-to-scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="5bf64-391">如何在 HDInsight 背景工作節點上調整 Microsoft R 伺服器實作的計算節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-391">How to scale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-the-worker-nodes"></a><span data-ttu-id="5bf64-392">將背景工作節點解除委任</span><span class="sxs-lookup"><span data-stu-id="5bf64-392">Decommission the worker node(s)</span></span>

<span data-ttu-id="5bf64-393">Microsoft R 伺服器目前無法透過 Yarn 管理。</span><span class="sxs-lookup"><span data-stu-id="5bf64-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="5bf64-394">如果未將背景工作角色節點解除任務，Yarn Resource Manager 將無法如預期般運作，因為它不會知道伺服器目前所佔用的資源。</span><span class="sxs-lookup"><span data-stu-id="5bf64-394">If the worker nodes are not decommissioned, the Yarn Resource Manager will not work as expected because it will not be aware of the resources being taken up by the server.</span></span> <span data-ttu-id="5bf64-395">為了避免這個狀況，建議您相應放大計算節點之前，將背景工作角色節點解除委任。</span><span class="sxs-lookup"><span data-stu-id="5bf64-395">In order to avoid this situation, we recommend decommissioning the worker nodes before you scale out the compute nodes.</span></span>

<span data-ttu-id="5bf64-396">解除委任背景工作節點的步驟︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-396">Steps to decommissioning worker nodes:</span></span>

* <span data-ttu-id="5bf64-397">登入 HDI 叢集的 Ambari 主控台，然後按一下 [主機] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="5bf64-397">Log in to HDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="5bf64-398">選取 (要解除委任的) 背景工作節點，按一下 [動作] > [選取的主機] > [主機] > 按一下 [開啟維護模式]。</span><span class="sxs-lookup"><span data-stu-id="5bf64-398">Select worker nodes (to be decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="5bf64-399">例如，在以下映像中，我們選取了要解除委任 wn3 和 wn4。</span><span class="sxs-lookup"><span data-stu-id="5bf64-399">For example, in the following image we have selected wn3 and wn4 to decommission.</span></span>  

   ![解除委任背景工作節點](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="5bf64-401">選取 [動作] > [選取的主機] > [DataNode] > 按一下 [解除委任]</span><span class="sxs-lookup"><span data-stu-id="5bf64-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="5bf64-402">選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [解除委任]</span><span class="sxs-lookup"><span data-stu-id="5bf64-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="5bf64-403">選取 [動作] > [選取的主機] > [DataNode] > 按一下 [停止]</span><span class="sxs-lookup"><span data-stu-id="5bf64-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="5bf64-404">選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [停止]</span><span class="sxs-lookup"><span data-stu-id="5bf64-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="5bf64-405">選取 [動作] > [選取的主機] > [主機] > 按一下 [停止所有元件]</span><span class="sxs-lookup"><span data-stu-id="5bf64-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="5bf64-406">將背景工作角色節點取消選取，並將前端節點選取</span><span class="sxs-lookup"><span data-stu-id="5bf64-406">Unselect the worker nodes and select the head nodes</span></span>
* <span data-ttu-id="5bf64-407">選取 [動作] > [選取的主機] > [主機] > [重新啟動所有元件]</span><span class="sxs-lookup"><span data-stu-id="5bf64-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="5bf64-408">在每個已解除委任的背景工作節點上設定計算節點</span><span class="sxs-lookup"><span data-stu-id="5bf64-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="5bf64-409">透過 SSH 連線到每個已解除委任的背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="5bf64-410">使用 `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` 執行系統管理公用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf64-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="5bf64-411">輸入 "1" 可選取 [設定 R 伺服器來實施] 選項。</span><span class="sxs-lookup"><span data-stu-id="5bf64-411">Enter "1" to select option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="5bf64-412">輸入 c 來選取選項 C.</span><span class="sxs-lookup"><span data-stu-id="5bf64-412">Enter "c" to select option "C.</span></span> <span data-ttu-id="5bf64-413">Compute node。</span><span class="sxs-lookup"><span data-stu-id="5bf64-413">Compute node".</span></span> <span data-ttu-id="5bf64-414">這會設定背景工作角色節點上的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-414">This configures the compute node on the worker node.</span></span>
5. <span data-ttu-id="5bf64-415">結束系統管理公用程式。</span><span class="sxs-lookup"><span data-stu-id="5bf64-415">Exit the Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="5bf64-416">在 Web 節點上新增計算節點詳細資料</span><span class="sxs-lookup"><span data-stu-id="5bf64-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="5bf64-417">所有已解除委任的背景工作節點皆已設定為執行計算節點後，請回到邊緣節點，然後在 Microsoft R Server Web 節點的組態中新增已解除委任之背景工作節點的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="5bf64-417">Once all decommissioned worker nodes have been configured to run compute node, come back on the edge node and add decommissioned worker nodes' IP addresses in the Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="5bf64-418">透過 SSH 連線到邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="5bf64-418">SSH into the edge node.</span></span>
* <span data-ttu-id="5bf64-419">執行 `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`。</span><span class="sxs-lookup"><span data-stu-id="5bf64-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="5bf64-420">尋找 [URI] 區段，並新增背景工作節點的 IP 和連接埠詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5bf64-420">Look for the "URIs" section, and add worker node's IP and port details.</span></span>

    ![解除委任背景工作節點 cmdline](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="5bf64-422">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5bf64-422">Troubleshoot</span></span>

<span data-ttu-id="5bf64-423">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="5bf64-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5bf64-424">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bf64-424">Next steps</span></span>

<span data-ttu-id="5bf64-425">現在，您應該了解如何建立包含 R 伺服器的新 HDInsight 叢集，以及從 SSH 工作階段使用 R 主控台的基本概念。</span><span class="sxs-lookup"><span data-stu-id="5bf64-425">Now you should understand how to create a new HDInsight cluster that includes the R Server and the basics of using the R console from an SSH session.</span></span> <span data-ttu-id="5bf64-426">下列主題說明的其他方式，可用來管理和使用 HDInsight 上的 R 伺服器：</span><span class="sxs-lookup"><span data-stu-id="5bf64-426">The following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="5bf64-427">將 RStudio Server 新增至 HDInsight (若未在建立叢集期間安裝)</span><span class="sxs-lookup"><span data-stu-id="5bf64-427">Add RStudio Server to HDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="5bf64-428">適用於 HDInsight 中 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="5bf64-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="5bf64-429">適用於 HDInsight R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="5bf64-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
