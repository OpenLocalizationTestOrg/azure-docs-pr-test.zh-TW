---
title: "aaaGet 開始使用 HDInsight 的 Azure 上的 R 伺服器 |Microsoft 文件"
description: "了解如何 toocreate Apache 二手包含 R Server 的 HDInsight 叢集上，並送出 hello 叢集上的 R 指令碼。"
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
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="d4ced-103">開始使用 HDInsight 中的 R Server</span><span class="sxs-lookup"><span data-stu-id="d4ced-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="d4ced-104">HDInsight 包括 R Server 選項 toobe 整合到您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d4ced-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="d4ced-105">此選項可讓 R 指令碼 toouse Spark 和 MapReduce toorun 分散式計算。</span><span class="sxs-lookup"><span data-stu-id="d4ced-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="d4ced-106">在本文件中，您學會 toocreate R 伺服器 HDInsight 叢集，然後再執行 R 指令碼將示範如何使用 Spark 散發 R 運算的方式。</span><span class="sxs-lookup"><span data-stu-id="d4ced-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d4ced-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4ced-107">Prerequisites</span></span>

* <span data-ttu-id="d4ced-108">**Azure 訂用帳戶**：開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="d4ced-109">移 toohello 文章[取得 Microsoft Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d4ced-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="d4ced-110">**安全殼層 (SSH) 用戶端**: SSH 用戶端使用 tooremotely 連接 toohello HDInsight 叢集，並直接在 hello 叢集上執行命令。</span><span class="sxs-lookup"><span data-stu-id="d4ced-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="d4ced-111">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="d4ced-112">**SSH 金鑰 （選擇性）**： 您可以保護 hello SSH 使用帳戶 tooconnect toohello 叢集使用密碼或公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ced-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="d4ced-113">使用密碼更為簡單，並可讓您 tooget 啟動而不需要 toocreate 公開/私密金鑰組。</span><span class="sxs-lookup"><span data-stu-id="d4ced-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="d4ced-114">不過，使用金鑰更加安全。</span><span class="sxs-lookup"><span data-stu-id="d4ced-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ced-115">本文件中的 hello 步驟假設您使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="d4ced-116">自動化的叢集建立</span><span class="sxs-lookup"><span data-stu-id="d4ced-116">Automated cluster creation</span></span>

<span data-ttu-id="d4ced-117">您可以自動化 hello 建立 HDInsight R 伺服器使用 Azure Resource Manager 範本、 hello SDK，以及 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d4ced-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="d4ced-118">toocreate R 伺服器使用 Azure 資源管理的範本，請參閱[部署 R 伺服器 HDInsight 叢集](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="d4ced-119">toocreate 的 R 伺服器使用 hello.NET SDK，請參閱[HDInsight 使用 hello.NET SDK 中建立 linux 叢集。](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="d4ced-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="d4ced-120">toodeploy R 伺服器上使用 powershell，請參閱 hello 文章[具有 PowerShell HDInsight 上建立 R Server](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="d4ced-121">建立 hello 叢集使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4ced-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="d4ced-122">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d4ced-123">依序選取 [新增] -> [情報 + 分析] -> [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="d4ced-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![建立新叢集的影像](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="d4ced-125">在 hello**快速建立**體驗，輸入 hello 叢集的名稱在 hello**叢集名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="d4ced-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="d4ced-126">如果您有多個 Azure 訂用帳戶，使用 hello**訂用帳戶**項目 tooselect hello 其中一個要 toouse。</span><span class="sxs-lookup"><span data-stu-id="d4ced-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![叢集名稱和訂用帳戶選取項目](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="d4ced-128">選取**叢集類型**tooopen hello**叢集設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d4ced-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="d4ced-129">在 hello**叢集設定**刀鋒視窗中，選取下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="d4ced-130">**叢集類型**：R 伺服器</span><span class="sxs-lookup"><span data-stu-id="d4ced-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="d4ced-131">**版本**: hello 叢集上的 R 伺服器 tooinstall 選取 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d4ced-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="d4ced-132">目前可用的 hello 版本是***R 伺服器 9.1 (HDI 3.6)***。</span><span class="sxs-lookup"><span data-stu-id="d4ced-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="d4ced-133">Hello 可用版本的 R Server 的版本資訊可用[這裡](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="d4ced-134">**R Studio community 版本的 R 伺服器**: hello 邊緣節點上的預設會安裝此瀏覽器為基礎的 IDE。</span><span class="sxs-lookup"><span data-stu-id="d4ced-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="d4ced-135">如果您想使用 toonot 進行安裝，然後取消核取 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d4ced-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="d4ced-136">如果您選擇 toohave 它安裝，來存取的 hello RStudio 伺服器登入位於入口網站應用程式 刀鋒視窗，供您的叢集，一旦建立之後的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="d4ced-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="d4ced-137">Hello 其他選項保留 hello 預設值，並使用 hello**選取**按鈕 toosave hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="d4ced-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![叢集類型刀鋒視窗螢幕擷取畫面](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="d4ced-139">輸入 [叢集登入使用者名稱] 和 [叢集登入密碼]。</span><span class="sxs-lookup"><span data-stu-id="d4ced-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="d4ced-140">指定 [SSH 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="d4ced-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="d4ced-141">SSH 使用的 tooremotely toohello 叢集使用連接**安全殼層 (SSH)**用戶端。</span><span class="sxs-lookup"><span data-stu-id="d4ced-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="d4ced-142">在這個對話方塊中，或 （hello 組態 索引標籤中的 hello 叢集） 建立 hello 叢集後，您可以指定 hello SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="d4ced-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="d4ced-143">R 伺服器是設定的 tooexpect **SSH 使用者名稱**的"remoteuser"。</span><span class="sxs-lookup"><span data-stu-id="d4ced-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="d4ced-144">**如果您使用不同的使用者名稱，您必須在建立 hello 叢集後，執行額外的步驟。**</span><span class="sxs-lookup"><span data-stu-id="d4ced-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="d4ced-145">檢查是否有保留 hello 方塊**使用與叢集登入相同的密碼**toouse**密碼**hello 驗證輸入除非您偏好使用公用金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ced-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="d4ced-146">您必須透過為，比方說，RTVS、 RStudio 或其他桌面 IDE 的遠端用戶端 hello 叢集上的公開/私密金鑰組 tooaccess R Server。</span><span class="sxs-lookup"><span data-stu-id="d4ced-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="d4ced-147">如果您安裝 hello RStudio Server community edition，您會需要 toochoose SSH 密碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="d4ced-148">toocreate 和使用公開/私密金鑰組，取消核取**使用與叢集登入相同的密碼**，然後選取 **公開金鑰**並繼續進行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d4ced-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="d4ced-149">這些指示會假設您已安裝 Cygwin 和 ssh-keygen 或具同等效力的命令。</span><span class="sxs-lookup"><span data-stu-id="d4ced-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="d4ced-150">從您的膝上型電腦上的 hello 命令提示字元中產生公開/私密金鑰組：</span><span class="sxs-lookup"><span data-stu-id="d4ced-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="d4ced-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="d4ced-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="d4ced-152">遵循 hello 提示 tooname 金鑰檔案，然後輸入複雜密碼為增加安全性。</span><span class="sxs-lookup"><span data-stu-id="d4ced-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="d4ced-153">您的畫面看起來應該像下列映像的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-153">Your screen should look something like hello following image:</span></span>

        ![Windows 中的 SSH 命令列](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="d4ced-155">此命令會建立私用金鑰檔和 hello 名稱 < 私用金鑰的檔名 >.pub，例如 furiosa 和 furiosa.pub 底下的公用金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="d4ced-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="d4ced-157">然後指定 hello 公開金鑰檔案 (&#42;。pub) 時指派 HDI 叢集認證與最後確認您的資源群組和區域並選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d4ced-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![認證刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="d4ced-159">變更您的膝上型電腦上的 hello 私用金鑰檔的權限：</span><span class="sxs-lookup"><span data-stu-id="d4ced-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="d4ced-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="d4ced-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="d4ced-161">遠端登入使用 SSH hello 私用金鑰檔：</span><span class="sxs-lookup"><span data-stu-id="d4ced-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="d4ced-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="d4ced-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="d4ced-163">或者，您也可以做 Hadoop Spark 一部分 hello 定義計算內容的 R 伺服器 hello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="d4ced-164">請參閱 hello**為 Hadoop 用戶端使用 Microsoft R Server**小節中[建立計算內容的 Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="d4ced-165">hello 快速建立您轉換 toohello**儲存體**hello hello 主要位置使用的設定 toobe HDFS 檔案系統 hello 叢集所用的刀鋒視窗 tooselect hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="d4ced-166">選取新的或現有的 Azure 儲存體帳戶或現有的 Data Lake 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="d4ced-167">如果您選取的 Azure 儲存體帳戶時，會選取現有的儲存體帳戶選擇**選取儲存體帳戶**，然後選取 hello 相關帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="d4ced-168">建立新的帳戶使用 hello**新建**hello 中的連結**選取儲存體帳戶**> 一節。</span><span class="sxs-lookup"><span data-stu-id="d4ced-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d4ced-169">如果您選取**新增**您必須輸入 hello 新儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4ced-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="d4ced-170">如果已接受 hello 名稱，則會出現綠色核取。</span><span class="sxs-lookup"><span data-stu-id="d4ced-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="d4ced-171">hello**預設容器**預設 toohello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="d4ced-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="d4ced-172">保留這個預設值為 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d4ced-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="d4ced-173">如果已選取新的儲存體帳戶選項，提示 tooselect**位置**是 tooselect 指定哪一個區域 toocreate hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![資料來源刀鋒視窗](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="d4ced-175">選擇 hello hello 預設的資料來源的位置時，也會設定 hello 位置 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d4ced-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="d4ced-176">hello 叢集和預設資料來源必須在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="d4ced-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="d4ced-177">如果您想 toouse 現有的資料湖存放區，然後選取 hello ADLS 儲存體帳戶 toouse 和新增 hello 叢集*新增*身分識別 tooyour 叢集 tooallow 存取 toohello 存放區。</span><span class="sxs-lookup"><span data-stu-id="d4ced-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="d4ced-178">如需此程序的詳細資訊，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="d4ced-179">使用 hello**選取**按鈕 toosave hello 資料來源組態。</span><span class="sxs-lookup"><span data-stu-id="d4ced-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="d4ced-180">hello**摘要**刀鋒視窗然後顯示 toovalidate 您的設定。</span><span class="sxs-lookup"><span data-stu-id="d4ced-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="d4ced-181">您可以在這裡變更您**叢集大小**toomodify hello 叢集中的伺服器數目和也指定任何**編寫指令碼動作**想 toorun。</span><span class="sxs-lookup"><span data-stu-id="d4ced-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="d4ced-182">除非您知道您需要較大的叢集，將背景工作節點數 hello 保留 hello 預設值是`4`。</span><span class="sxs-lookup"><span data-stu-id="d4ced-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="d4ced-183">hello 估計成本的 hello 叢集會顯示 hello 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d4ced-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![叢集摘要](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="d4ced-185">如有需要您可以調整您的叢集，稍後透過 hello 入口網站 (**叢集** -> **設定** -> **延展叢集**) tooincrease 或減少 hello 背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="d4ced-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="d4ced-186">此調整大小可能很有用的閒置到達便關閉 hello 叢集時不在使用中，或新增容量 toomeet hello 需求的較大型的工作。</span><span class="sxs-lookup"><span data-stu-id="d4ced-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="d4ced-187">調整您的叢集、 hello 資料節點和 hello 邊緣節點記住的一些因素 tookeep 包括：</span><span class="sxs-lookup"><span data-stu-id="d4ced-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="d4ced-188">hello 效能上的 Spark 的分散式 R Server 分析時，背景工作節點數成正比 toohello hello 資料很大。</span><span class="sxs-lookup"><span data-stu-id="d4ced-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="d4ced-189">R 伺服器分析的 hello 效能中是線性 hello 所分析的資料大小。</span><span class="sxs-lookup"><span data-stu-id="d4ced-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="d4ced-190">例如：</span><span class="sxs-lookup"><span data-stu-id="d4ced-190">For example:</span></span>  

     * <span data-ttu-id="d4ced-191">小型 toomodest 資料效能最好分析 hello 邊緣節點上的本機計算內容中時。</span><span class="sxs-lookup"><span data-stu-id="d4ced-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="d4ced-192">如需有關在本機的 hello 與 Spark 計算內容的 hello 案例適合，請參閱 R Server 計算內容選項在 HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="d4ced-193">如果您登入 toohello 邊緣節點，然後執行 R 指令碼，則所有但 hello ScaleR rx 函數執行<strong>本機</strong>hello 邊緣節點上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="d4ced-194">因此 hello 記憶體及核心 hello 邊緣節點的數目應該要據以調整大小。</span><span class="sxs-lookup"><span data-stu-id="d4ced-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="d4ced-195">如果您使用 R Server HDI 上做為遠端計算內容從膝上型電腦套用 hello。</span><span class="sxs-lookup"><span data-stu-id="d4ced-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![節點定價層刀鋒視窗](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="d4ced-197">使用 hello**選取**按鈕 toosave hello 節點定價組態。</span><span class="sxs-lookup"><span data-stu-id="d4ced-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="d4ced-198">還有 [下載範本和參數] 的連結。</span><span class="sxs-lookup"><span data-stu-id="d4ced-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="d4ced-199">按一下此連結 toodisplay 指令碼可以使用的 tooautomate hello 建立 hello 選設定與叢集上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="d4ced-200">一旦建立之後，您也可以從 hello Azure 入口網站的項目叢集中執行這些指令碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d4ced-201">花一些時間 hello 叢集 toobe 建立，通常是 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d4ced-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="d4ced-202">使用 hello 磚上 hello 開始面板，或 hello**通知**hello 建立程序上剩餘的 hello 頁面 toocheck 的 hello 上的項目。</span><span class="sxs-lookup"><span data-stu-id="d4ced-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="d4ced-203">連接 tooRStudio 伺服器</span><span class="sxs-lookup"><span data-stu-id="d4ced-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="d4ced-204">如果您選擇 tooinclude RStudio Server community edition 安裝中，您就可以存取透過兩個不同方法的 hello RStudio 登入。</span><span class="sxs-lookup"><span data-stu-id="d4ced-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="d4ced-205">移 toohello 下列 URL (其中**CLUSTERNAME**是您已建立 hello 叢集 hello 名稱):</span><span class="sxs-lookup"><span data-stu-id="d4ced-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="d4ced-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="d4ced-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="d4ced-207">在 hello Azure 入口網站中，選取 hello 中開啟您的叢集 hello 項目**R Server 儀表板**快速連結，然後選取 hello **R Studio 儀表板**:</span><span class="sxs-lookup"><span data-stu-id="d4ced-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![存取 hello R studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![存取 hello R studio 儀表板](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="d4ced-210">使用 hello 方法，不論 hello 第一次登入您需要 tooauthenticate 兩次。</span><span class="sxs-lookup"><span data-stu-id="d4ced-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="d4ced-211">在 hello 第一次驗證，可讓 hello*叢集系統管理員使用者識別碼*和*密碼*。</span><span class="sxs-lookup"><span data-stu-id="d4ced-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="d4ced-212">在 hello 第二個提示字元中提供 hello *SSH userid*和*密碼*。</span><span class="sxs-lookup"><span data-stu-id="d4ced-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="d4ced-213">後續的記錄集只需要 hello *SSH 密碼*和*userid*。</span><span class="sxs-lookup"><span data-stu-id="d4ced-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="d4ced-214">Toohello R Server 邊緣節點連接</span><span class="sxs-lookup"><span data-stu-id="d4ced-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="d4ced-215">連接導覽伺服器邊緣節點 hello 命令搭配使用 SSH hello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="d4ced-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="d4ced-216">您可以找到 hello`USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`中 hello Azure 入口網站，然後選取您的叢集位址**所有設定** -> **應用程式** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="d4ced-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="d4ced-217">這會顯示 hello hello 邊緣節點的 SSH 端點資訊。</span><span class="sxs-lookup"><span data-stu-id="d4ced-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Hello SSH 端點 hello 邊緣節點的影像](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="d4ced-219">如果您使用密碼 toosecure SSH 使用者帳戶，則提示的 tooenter 它。</span><span class="sxs-lookup"><span data-stu-id="d4ced-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="d4ced-220">如果您使用公開金鑰，您可能必須 toouse hello`-i`參數 toospecify hello 相符的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="d4ced-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="d4ced-221">例如：</span><span class="sxs-lookup"><span data-stu-id="d4ced-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="d4ced-222">如需詳細資訊，請參閱[連接 tooHDInsight (Hadoop) 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d4ced-223">一旦連接之後，您會抵達提示的類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="d4ced-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="d4ced-224">啟用多個並行使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="d4ced-225">您可以啟用多個並行使用者藉由新增更多使用者 hello 邊緣節點上的 hello RStudio 社群版本中執行。</span><span class="sxs-lookup"><span data-stu-id="d4ced-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="d4ced-226">當您建立 HDInsight 叢集時，您必須提供兩個使用者 (HTTP 使用者和 SSH 使用者)：</span><span class="sxs-lookup"><span data-stu-id="d4ced-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![並行使用者 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="d4ced-228">**叢集登入使用者名稱**: 的 HTTP 使用者進行驗證，透過 hello HDInsight 閘道所使用的 tooprotect hello HDInsight 叢集，您所建立。</span><span class="sxs-lookup"><span data-stu-id="d4ced-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="d4ced-229">此 HTTP 使用者是使用的 tooaccess hello Ambari UI、 YARN UI，以及其他 UI 元件。</span><span class="sxs-lookup"><span data-stu-id="d4ced-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="d4ced-230">**安全殼層 (SSH) 的使用者名稱**： 透過安全殼層的 SSH 使用者 tooaccess hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d4ced-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="d4ced-231">此使用者是 hello hello 前端節點、 背景工作節點和邊緣節點的 Linux 系統中的使用者。</span><span class="sxs-lookup"><span data-stu-id="d4ced-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="d4ced-232">因此您可以使用安全殼層 tooaccess hello 節點中的遠端叢集。</span><span class="sxs-lookup"><span data-stu-id="d4ced-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="d4ced-233">hello Microsoft R Server 類型的 HDInsight 叢集上所使用的 hello R Studio Server 社群版本只接受 Linux 使用者名稱與密碼做為登入機制。</span><span class="sxs-lookup"><span data-stu-id="d4ced-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="d4ced-234">但不支援傳遞權杖。</span><span class="sxs-lookup"><span data-stu-id="d4ced-234">It does not support passing tokens.</span></span> <span data-ttu-id="d4ced-235">因此，如果您已建立新的叢集，並想 toouse R Studio tooaccess，您需要在 toolog 兩次。</span><span class="sxs-lookup"><span data-stu-id="d4ced-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="d4ced-236">第一次使用認證登入 hello HTTP 使用者透過 hello HDInsight 閘道：</span><span class="sxs-lookup"><span data-stu-id="d4ced-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![並行使用者 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="d4ced-238">然後使用 hello SSH 使用者認證 toolog tooRStudio 中：</span><span class="sxs-lookup"><span data-stu-id="d4ced-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![並行使用者 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="d4ced-240">目前，在佈建 HDInsight 叢集時，只可以建立一個 SSH 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4ced-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="d4ced-241">因此 tooenable 多個使用者 tooaccess HDInsight 上的 Microsoft R Server 叢集，我們需要 toocreate hello Linux 系統中的其他使用者。</span><span class="sxs-lookup"><span data-stu-id="d4ced-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="d4ced-242">由於 RStudio Server 社群 hello 叢集邊緣節點上執行，但有以下幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="d4ced-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="d4ced-243">您可以使用建立 hello SSH 使用者 toolog toohello 邊緣節點中</span><span class="sxs-lookup"><span data-stu-id="d4ced-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="d4ced-244">在邊緣節點中新增更多 Linux 使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="d4ced-245">使用 RStudio 社群版本與 hello 所建立的使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="d4ced-246">步驟 1： 使用 toohello 邊緣節點中建立的 hello SSH 使用者 toolog</span><span class="sxs-lookup"><span data-stu-id="d4ced-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="d4ced-247">下載任何 SSH 工具 （例如 Putty) 並使用 hello 現有 SSH 使用者 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="d4ced-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="d4ced-248">然後遵循所提供的 hello 指示[連接 tooHDInsight (Hadoop) 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="d4ced-249">hello 邊緣節點位址 R Server 在 HDInsight 叢集上： *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="d4ced-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="d4ced-250">步驟 2：在邊緣節點中新增更多 Linux 使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="d4ced-251">tooadd 使用者 toohello 邊緣節點，執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="d4ced-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="d4ced-252">您應該會看到下列項目傳回 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-252">You should see hello following items returned:</span></span> 

![並行使用者 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="d4ced-254">當系統提示您輸入"目前的 Kerberos 密碼: 」，請按**Enter** tooignore 它。</span><span class="sxs-lookup"><span data-stu-id="d4ced-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="d4ced-255">hello`-m`選項`useradd`命令表示 hello 系統將會建立 hello 使用者所需的 RStudio 社群版本的主資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4ced-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="d4ced-256">步驟 3： 使用 RStudio 社群版本與 hello 所建立的使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="d4ced-257">使用 hello 使用者建立 toolog tooRStudio 中：</span><span class="sxs-lookup"><span data-stu-id="d4ced-257">Use hello user created toolog in tooRStudio:</span></span>

![並行使用者 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="d4ced-259">RStudio 表示使用 hello 新使用者的通知 (例如，這裡*sshuser6*) toolog hello 叢集中：</span><span class="sxs-lookup"><span data-stu-id="d4ced-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![並行使用者 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="d4ced-261">您也可以登入使用 hello 原始認證 (依預設，它是*sshuser*) 同時從另一個瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="d4ced-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="d4ced-262">您可以使用 scaleR 函式來提交作業。</span><span class="sxs-lookup"><span data-stu-id="d4ced-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="d4ced-263">以下是範例 hello 命令會使用 toorun 作業：</span><span class="sxs-lookup"><span data-stu-id="d4ced-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
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

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="d4ced-264">送出 hello 作業在 YARN UI 中的不同的使用者名稱 底下的注意事項：</span><span class="sxs-lookup"><span data-stu-id="d4ced-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![並行使用者 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="d4ced-266">請注意，也該 hello 新加入的使用者不需要根權限在 Linux 系統中，但它們有 hello 相同存取 tooall hello hello 遠端 HDFS 與 WASB 儲存體中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d4ced-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="d4ced-267">使用 hello R 主控台</span><span class="sxs-lookup"><span data-stu-id="d4ced-267">Use hello R console</span></span>

1. <span data-ttu-id="d4ced-268">從 hello SSH 工作階段，使用下列命令 toostart hello R 主控台 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="d4ced-269">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d4ced-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="d4ced-270">R 版本 3.2.2 (2015年-08-14)-"引發 Safety"Copyright (C) 2015 hello R Foundation 統計運算平台： x86_64-pc-linux-gnu （64 位元）</span><span class="sxs-lookup"><span data-stu-id="d4ced-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="d4ced-271">R 是免費的軟體，且「絕對無瑕疵責任擔保」。</span><span class="sxs-lookup"><span data-stu-id="d4ced-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="d4ced-272">您是  褖畫惎 tooredistribute 它在某些情況下。</span><span class="sxs-lookup"><span data-stu-id="d4ced-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="d4ced-273">輸入 'license()' 或 'licence()' 可取得發佈詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4ced-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="d4ced-274">支援自然語言，但是在英文地區設定中執行</span><span class="sxs-lookup"><span data-stu-id="d4ced-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="d4ced-275">R 是共同作業專案，具有許多的參與者。</span><span class="sxs-lookup"><span data-stu-id="d4ced-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="d4ced-276">如需詳細資訊和 'citation()' 的 'contributors()' 輸入上 toocite R 或 R 發行集內的封裝中。</span><span class="sxs-lookup"><span data-stu-id="d4ced-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="d4ced-277">輸入一些示範、 線上說明，請 ' help()' 或 'help.start()' 的 HTML 瀏覽器介面 toohelp 'demo()'。</span><span class="sxs-lookup"><span data-stu-id="d4ced-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="d4ced-278">輸入 'q()' tooquit。</span><span class="sxs-lookup"><span data-stu-id="d4ced-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="d4ced-279">Microsoft R 伺服器 8.0 版：R 的增強發佈 Microsoft 套件 Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="d4ced-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="d4ced-280">輸入 'readme()' 可取得版本資訊。</span><span class="sxs-lookup"><span data-stu-id="d4ced-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="d4ced-281">從 hello`>`提示字元，您可以輸入 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="d4ced-282">R 伺服器包括 tooeasily 可讓您的封裝互動的 Hadoop 和執行分散式的計算。</span><span class="sxs-lookup"><span data-stu-id="d4ced-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="d4ced-283">例如，使用下列命令 tooview hello 根 hello hello HDInsight 叢集的預設檔案系統的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="d4ced-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="d4ced-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="d4ced-285">您也可以使用 hello WASB 樣式定址。</span><span class="sxs-lookup"><span data-stu-id="d4ced-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="d4ced-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="d4ced-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="d4ced-287">從 Microsoft R Server 或 Microsoft R Client 的遠端執行個體使用 HDI 上的 R Server</span><span class="sxs-lookup"><span data-stu-id="d4ced-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="d4ced-288">從 Microsoft R Server 或 Microsoft R 用戶端桌上型電腦或膝上型電腦上執行的遠端執行個體存取 toohello HDI Hadoop Spark 計算內容可能 tooset 它。</span><span class="sxs-lookup"><span data-stu-id="d4ced-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="d4ced-289">請參閱**為 Hadoop 用戶端使用 Microsoft R Server** hello 的小節[建立計算內容的 Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="d4ced-290">toodo 因此，您需要下列選項，您的膝上型電腦上定義 hello RxSpark 計算內容時的 toospecify hello: hdfsShareDir，shareDir，sshUsername，sshHostname，sshSwitches，和 sshProfileScript。</span><span class="sxs-lookup"><span data-stu-id="d4ced-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="d4ced-291">例如：</span><span class="sxs-lookup"><span data-stu-id="d4ced-291">For example:</span></span>


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


## <a name="use-a-compute-context"></a><span data-ttu-id="d4ced-292">使用計算內容</span><span class="sxs-lookup"><span data-stu-id="d4ced-292">Use a compute context</span></span>

<span data-ttu-id="d4ced-293">計算內容可讓您 toocontrol 計算是在本機執行 hello 邊緣節點上或分散在 hello hello HDInsight 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="d4ced-294">從 RStudio 伺服器或 hello R 主控台 （中的 SSH 工作階段），使用下列程式碼 tooload 範例資料到 hello 預設儲存體，HDInsight 的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
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

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="d4ced-295">接下來，讓我們來建立部分資料的資訊，並定義兩個資料來源，以便我們可以使用 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d4ced-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="d4ced-296">讓我們使用 hello 本機計算內容的 hello 資料執行羅吉斯迴歸。</span><span class="sxs-lookup"><span data-stu-id="d4ced-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="d4ced-297">您應該看到的結尾行類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d4ced-297">You should see output that ends with lines similar toohello following:</span></span>

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

4. <span data-ttu-id="d4ced-298">接下來，我們先執行 hello 使用 hello Spark 內容的相同羅吉斯迴歸。</span><span class="sxs-lookup"><span data-stu-id="d4ced-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="d4ced-299">hello Spark 內容會發佈 hello 透過 hello HDInsight 叢集中的所有 hello 背景工作節點處理。</span><span class="sxs-lookup"><span data-stu-id="d4ced-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="d4ced-300">您也可以使用 MapReduce toodistribute 計算叢集節點之間。</span><span class="sxs-lookup"><span data-stu-id="d4ced-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="d4ced-301">如需計算內容的詳細資訊，請參閱[適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="d4ced-302">將 R 程式碼 toomultiple 節點</span><span class="sxs-lookup"><span data-stu-id="d4ced-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="d4ced-303">使用 R Server 可以輕易地讓現有的 R 程式碼並執行它 hello 叢集中的多個節點之間使用`rxExec`。</span><span class="sxs-lookup"><span data-stu-id="d4ced-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="d4ced-304">執行參數掃掠或模擬時，這個函式非常有用。</span><span class="sxs-lookup"><span data-stu-id="d4ced-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="d4ced-305">hello 下列程式碼是如何的範例 toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="d4ced-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="d4ced-306">如果您仍在使用 hello Spark 或 MapReduce 內容，此命令會傳回 hello 背景工作角色節點的 hello nodename 值該 hello 程式碼`(Sys.info()["nodename"])`上執行。</span><span class="sxs-lookup"><span data-stu-id="d4ced-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="d4ced-307">例如，在四個節點叢集上，您預期 tooreceive 輸出類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="d4ced-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

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


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="d4ced-308">存取 Hive 和 Parquet 中的資料</span><span class="sxs-lookup"><span data-stu-id="d4ced-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="d4ced-309">R 伺服器 9.1 提供的功能可允許使用 Hive 和 Parquet 中的直接存取 toodata ScaleR 函數 hello Spark 計算內容中。</span><span class="sxs-lookup"><span data-stu-id="d4ced-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="d4ced-310">這些功能都是透過新 ScaleR 資料來源運作的函式呼叫 RxHiveData 和 RxParquetData 藉由使用 Spark SQL tooload 資料直接將 ScaleR 以進行分析的 Spark 資料框架。</span><span class="sxs-lookup"><span data-stu-id="d4ced-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="d4ced-311">下列程式碼的 hello 提供 hello 新函式的使用範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="d4ced-311">hello following code provides some sample code on use of hello new functions:</span></span>

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

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="d4ced-312">如需使用這些新的函式的詳細資訊，請參閱 hello 中的線上說明 R Server 藉由使用 hello`?RxHivedata`和`?RxParquetData`命令。</span><span class="sxs-lookup"><span data-stu-id="d4ced-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="d4ced-313">Hello 邊緣節點上安裝其他的 R 封裝</span><span class="sxs-lookup"><span data-stu-id="d4ced-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="d4ced-314">如果您想要在 hello 邊緣節點 tooinstall 其他 R 封裝，您可以使用`install.packages()`直接從 hello R 主控台時連線的 toohello 邊緣透過 SSH 的節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="d4ced-315">不過，如果您需要將 R 封裝 tooinstall hello 工作者 hello 叢集中節點上的，您必須使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="d4ced-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="d4ced-316">指令碼動作是使用的 toomake 組態變更 toohello HDInsight 叢集或 tooinstall 其他軟體，例如其他 R 封裝 Bash 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="d4ced-317">tooinstall 其他封裝使用指令碼動作，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ced-318">使用指令碼動作 tooinstall 其他 R 封裝只能在建立 hello 叢集之後。</span><span class="sxs-lookup"><span data-stu-id="d4ced-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="d4ced-319">Hello 指令碼是根據 R 伺服器完整地安裝和設定時，請勿在叢集建立期間使用這個程序。</span><span class="sxs-lookup"><span data-stu-id="d4ced-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="d4ced-320">從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 R 伺服器，在 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="d4ced-321">從 hello**設定**刀鋒視窗中，選取**指令碼動作**然後**提交新**toosubmit 新的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="d4ced-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![指令碼動作刀鋒視窗的影像](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="d4ced-323">從 hello**送出指令碼動作**刀鋒視窗中，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4ced-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="d4ced-324">**名稱**: 易記名稱 tooidentify 此指令碼</span><span class="sxs-lookup"><span data-stu-id="d4ced-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="d4ced-325">**Bash 指令碼 URI**：`http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="d4ced-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="d4ced-326">**前端**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="d4ced-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="d4ced-327">**背景工作**︰此項目應該是**已核取**狀態</span><span class="sxs-lookup"><span data-stu-id="d4ced-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="d4ced-328">**邊緣節點**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="d4ced-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="d4ced-329">**Zookeeper**︰此項目應該是**未核取**狀態</span><span class="sxs-lookup"><span data-stu-id="d4ced-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="d4ced-330">**參數**: hello R 封裝 toobe 安裝。</span><span class="sxs-lookup"><span data-stu-id="d4ced-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="d4ced-331">例如， `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="d4ced-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="d4ced-332">**保存此指令碼...**︰此項目應該是**已核取**狀態</span><span class="sxs-lookup"><span data-stu-id="d4ced-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="d4ced-333">根據預設，所有的 R 封裝會安裝從 hello Microsoft MRAN 儲存機制已安裝的 R 伺服器 hello 版本與一致的快照集。</span><span class="sxs-lookup"><span data-stu-id="d4ced-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="d4ced-334">如果您想 tooinstall 較新版本的封裝，就不相容的某些風險。</span><span class="sxs-lookup"><span data-stu-id="d4ced-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="d4ced-335">不過這種安裝方法，就是指定`useCRAN`為 hello hello 封裝的第一個項目清單，例如`useCRAN bitops, stringr, arules`。</span><span class="sxs-lookup"><span data-stu-id="d4ced-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="d4ced-336">有些 R 套件需要額外的 Linux 系統程式庫。</span><span class="sxs-lookup"><span data-stu-id="d4ced-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="d4ced-337">為了方便起見，我們已預先安裝 hello hello 前 100 最受歡迎的 R 封裝所需的相依性。</span><span class="sxs-lookup"><span data-stu-id="d4ced-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="d4ced-338">不過，如果您安裝的 hello R 封裝需要超出這些範圍的程式庫然後您必須下載 hello 這裡使用的基底指令碼並新增步驟 tooinstall hello 系統程式庫。</span><span class="sxs-lookup"><span data-stu-id="d4ced-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="d4ced-339">您必須上傳 hello 修改指令碼 tooa 公用 blob 在 Azure 儲存體容器，並使用 hello 修改指令碼 tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="d4ced-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="d4ced-340">如需開發指令碼動作的詳細資訊，請參閱 [指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![新增指令碼動作](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="d4ced-342">選取**建立**toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d4ced-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="d4ced-343">Hello 指令碼完成之後，就有一個 hello R 封裝可用背景工作的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="d4ced-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="d4ced-344">使用 Microsoft R 伺服器實作</span><span class="sxs-lookup"><span data-stu-id="d4ced-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="d4ced-345">完成您的資料模型化時，您可以實施 hello 模型 toomake 預測。</span><span class="sxs-lookup"><span data-stu-id="d4ced-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="d4ced-346">Microsoft R Server 實施的 tooconfigure 執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d4ced-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="d4ced-347">首先，ssh hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="d4ced-348">例如，</span><span class="sxs-lookup"><span data-stu-id="d4ced-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="d4ced-349">在使用後 ssh，變更用於 hello 相關版本和 sudo hello dotnet dll 的目錄：</span><span class="sxs-lookup"><span data-stu-id="d4ced-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="d4ced-350">對於 Microsoft R Server 9.1：</span><span class="sxs-lookup"><span data-stu-id="d4ced-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="d4ced-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="d4ced-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="d4ced-352">對於 Microsoft R Server 9.0：</span><span class="sxs-lookup"><span data-stu-id="d4ced-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="d4ced-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="d4ced-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="d4ced-354">與一個方塊設定 tooconfigure Microsoft R Server 實施 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="d4ced-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="d4ced-355">選取 [設定 R 伺服器來實施]</span><span class="sxs-lookup"><span data-stu-id="d4ced-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="d4ced-356">選取 A.</span><span class="sxs-lookup"><span data-stu-id="d4ced-356">Select “A.</span></span> <span data-ttu-id="d4ced-357">One-box (web + compute nodes)</span><span class="sxs-lookup"><span data-stu-id="d4ced-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="d4ced-358">輸入密碼以 hello **admin**使用者</span><span class="sxs-lookup"><span data-stu-id="d4ced-358">Enter a password for hello **admin** user</span></span>

![one box op](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="d4ced-360">您也可以選擇性地執行診斷測試來執行診斷檢查，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d4ced-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="d4ced-361">選取 6.</span><span class="sxs-lookup"><span data-stu-id="d4ced-361">Select “6.</span></span> <span data-ttu-id="d4ced-362">Run diagnostic tests</span><span class="sxs-lookup"><span data-stu-id="d4ced-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="d4ced-363">選取 A.</span><span class="sxs-lookup"><span data-stu-id="d4ced-363">Select “A.</span></span> <span data-ttu-id="d4ced-364">Test configuration</span><span class="sxs-lookup"><span data-stu-id="d4ced-364">Test configuration”</span></span>
3. <span data-ttu-id="d4ced-365">輸入上述設定步驟中的使用者名稱 = “admin” 和密碼</span><span class="sxs-lookup"><span data-stu-id="d4ced-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="d4ced-366">確認整體健全狀況 = pass</span><span class="sxs-lookup"><span data-stu-id="d4ced-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="d4ced-367">結束 hello 管理公用程式</span><span class="sxs-lookup"><span data-stu-id="d4ced-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="d4ced-368">結束 SSH</span><span class="sxs-lookup"><span data-stu-id="d4ced-368">Exit SSH</span></span>

![實作的診斷](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="d4ced-370">**在 Spark 上取用 Web 服務時長時間延遲**</span><span class="sxs-lookup"><span data-stu-id="d4ced-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="d4ced-371">如果嘗試 tooconsume web 服務建立 mrsdeploy Spark 計算內容中的函式使用時，您會遇到冗長延遲，您可能需要 tooadd 部分遺失的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d4ced-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="d4ced-372">hello Spark 應用程式所屬 tooa 使用者稱為 '*rserve2*' 時被叫用 web 服務使用 mrsdeploy 函式。</span><span class="sxs-lookup"><span data-stu-id="d4ced-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="d4ced-373">toowork 解決此問題：</span><span class="sxs-lookup"><span data-stu-id="d4ced-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="d4ced-374">在這個階段，hello 用於實施已完成設定。</span><span class="sxs-lookup"><span data-stu-id="d4ced-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="d4ced-375">現在您可以使用 hello 'mrsdeploy' 邊緣節點上您 RClient tooconnect toohello 實施上的套件，並開始使用它的功能類似[遠端執行](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution)和[web 服務](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="d4ced-376">根據是否叢集中設定虛擬網路上或不，您可能需要 tooset 設定連接埠轉送通道透過 SSH 登入。</span><span class="sxs-lookup"><span data-stu-id="d4ced-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="d4ced-377">hello 下列各節說明如何設定此通道 tooset。</span><span class="sxs-lookup"><span data-stu-id="d4ced-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="d4ced-378">虛擬網路上的 RServer 叢集</span><span class="sxs-lookup"><span data-stu-id="d4ced-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="d4ced-379">請確定您允許流量通過連接埠 12800 toohello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="d4ced-380">這樣一來，您可以使用 hello 邊緣節點 tooconnect toohello 實施功能。</span><span class="sxs-lookup"><span data-stu-id="d4ced-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="d4ced-381">如果 hello`remoteLogin()`不能連接 toohello 邊緣節點，但可以 SSH toohello 邊緣節點，然後您需要 tooverify 是否正確或沒有已設定連接埠 12800 hello 規則 tooallow 流量。</span><span class="sxs-lookup"><span data-stu-id="d4ced-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="d4ced-382">如果您繼續 tooface hello 問題，您可以藉由設定連接埠正透過的通道 SSH 暫時解決它。</span><span class="sxs-lookup"><span data-stu-id="d4ced-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="d4ced-383">如需指示，請參閱下列區段的 hello。</span><span class="sxs-lookup"><span data-stu-id="d4ced-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="d4ced-384">RServer 叢集未設定於虛擬網路上</span><span class="sxs-lookup"><span data-stu-id="d4ced-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="d4ced-385">如果您的叢集未設定於 vnet 上，或如果您在透過 vnet 連線時遇到問題，可以使用 SSH 連接埠轉送通道︰</span><span class="sxs-lookup"><span data-stu-id="d4ced-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="d4ced-386">在 Putty 上，您也可以做此設定。</span><span class="sxs-lookup"><span data-stu-id="d4ced-386">On Putty, you can set it up as well.</span></span>

![putty ssh 連線](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="d4ced-388">一旦您的 SSH 工作階段為作用中，從您電腦的連接埠 12800 hello 流量就會轉送 toohello 邊緣節點的連接埠 12800 透過 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d4ced-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="d4ced-389">請務必在 `remoteLogin()` 方法中使用 `127.0.0.1:12800`。</span><span class="sxs-lookup"><span data-stu-id="d4ced-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="d4ced-390">這會記錄透過連接埠轉送 toohello 邊緣節點的實施。</span><span class="sxs-lookup"><span data-stu-id="d4ced-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="d4ced-391">Microsoft R Server 實施 tooscale 如何計算 HDInsight 背景工作節點上的節點</span><span class="sxs-lookup"><span data-stu-id="d4ced-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="d4ced-392">解除委任 hello 背景工作節點</span><span class="sxs-lookup"><span data-stu-id="d4ced-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="d4ced-393">Microsoft R 伺服器目前無法透過 Yarn 管理。</span><span class="sxs-lookup"><span data-stu-id="d4ced-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="d4ced-394">如果 hello 背景工作節點不是已解除任務，hello Yarn 資源管理員將無法正常運作因為並不會察覺的 hello 伺服器所佔據的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d4ced-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="d4ced-395">在順序 tooavoid 這種情況下，我們建議您相應 hello 計算節點之前解除委任 hello 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="d4ced-396">步驟 toodecommissioning 背景工作節點：</span><span class="sxs-lookup"><span data-stu-id="d4ced-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="d4ced-397">登入 tooHDI 叢集 Ambari 主控台，然後按一下 [主機] 索引標籤上</span><span class="sxs-lookup"><span data-stu-id="d4ced-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="d4ced-398">選取 (解除委任 toobe) 的背景工作節點，請按一下 [動作] > [選取主機] > [主機]"> 按一下 「 開啟 ON 維護模式 」。</span><span class="sxs-lookup"><span data-stu-id="d4ced-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="d4ced-399">例如，在下列映像的 hello 我們已選取 wn3 和 wn4 toodecommission。</span><span class="sxs-lookup"><span data-stu-id="d4ced-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![解除委任背景工作節點](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="d4ced-401">選取 [動作] > [選取的主機] > [DataNode] > 按一下 [解除委任]</span><span class="sxs-lookup"><span data-stu-id="d4ced-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="d4ced-402">選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [解除委任]</span><span class="sxs-lookup"><span data-stu-id="d4ced-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="d4ced-403">選取 [動作] > [選取的主機] > [DataNode] > 按一下 [停止]</span><span class="sxs-lookup"><span data-stu-id="d4ced-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="d4ced-404">選取 [動作] > [選取的主機] > [NodeManagers] > 按一下 [停止]</span><span class="sxs-lookup"><span data-stu-id="d4ced-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="d4ced-405">選取 [動作] > [選取的主機] > [主機] > 按一下 [停止所有元件]</span><span class="sxs-lookup"><span data-stu-id="d4ced-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="d4ced-406">取消選取 hello 背景工作節點，並選取 hello 前端節點</span><span class="sxs-lookup"><span data-stu-id="d4ced-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="d4ced-407">選取 [動作] > [選取的主機] > [主機] > [重新啟動所有元件]</span><span class="sxs-lookup"><span data-stu-id="d4ced-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="d4ced-408">在每個已解除委任的背景工作節點上設定計算節點</span><span class="sxs-lookup"><span data-stu-id="d4ced-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="d4ced-409">透過 SSH 連線到每個已解除委任的背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="d4ced-410">使用 `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` 執行系統管理公用程式。</span><span class="sxs-lookup"><span data-stu-id="d4ced-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="d4ced-411">請輸入"1"tooselect 選項"設定 R 伺服器的實施"。</span><span class="sxs-lookup"><span data-stu-id="d4ced-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="d4ced-412">請輸入"c"tooselect 選項 「 C.</span><span class="sxs-lookup"><span data-stu-id="d4ced-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="d4ced-413">Compute node。</span><span class="sxs-lookup"><span data-stu-id="d4ced-413">Compute node".</span></span> <span data-ttu-id="d4ced-414">這會在 hello 背景工作節點上設定 hello 計算節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="d4ced-415">結束 hello 管理公用程式。</span><span class="sxs-lookup"><span data-stu-id="d4ced-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="d4ced-416">在 Web 節點上新增計算節點詳細資料</span><span class="sxs-lookup"><span data-stu-id="d4ced-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="d4ced-417">在設定已解除任務的背景工作的所有節點之後 toorun 計算節點、 hello 邊緣節點上回來 hello Microsoft R Server web 節點設定中新增已解除任務的背景工作角色節點的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="d4ced-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="d4ced-418">SSH hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d4ced-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="d4ced-419">執行 `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`。</span><span class="sxs-lookup"><span data-stu-id="d4ced-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="d4ced-420">尋找 hello"Uri"區段中，並新增背景工作節點的 IP 和連接埠詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4ced-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![解除委任背景工作節點 cmdline](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="d4ced-422">疑難排解</span><span class="sxs-lookup"><span data-stu-id="d4ced-422">Troubleshoot</span></span>

<span data-ttu-id="d4ced-423">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="d4ced-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d4ced-424">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4ced-424">Next steps</span></span>

<span data-ttu-id="d4ced-425">現在，您應該了解如何 toocreate 新的 HDInsight 叢集，其中包含使用的 hello R 伺服器與 hello 基本概念 hello 的 SSH 工作階段從 R 主控台。</span><span class="sxs-lookup"><span data-stu-id="d4ced-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="d4ced-426">hello 下列主題說明管理和使用 HDInsight 上的 R 伺服器的其他方式：</span><span class="sxs-lookup"><span data-stu-id="d4ced-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="d4ced-427">新增 RStudio 伺服器 tooHDInsight （如果未安裝在叢集建立期間）</span><span class="sxs-lookup"><span data-stu-id="d4ced-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="d4ced-428">適用於 HDInsight 中 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="d4ced-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="d4ced-429">適用於 HDInsight R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="d4ced-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
