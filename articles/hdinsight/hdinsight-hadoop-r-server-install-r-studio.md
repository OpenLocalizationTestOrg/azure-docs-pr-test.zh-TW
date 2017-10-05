---
title: "在 HDInsight 上使用 R 伺服器安裝 RStudio - Azure | Microsoft Docs"
description: "如何在 HDInsight 上使用 R 伺服器安裝 RStudio。"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 416420d855505508735ebd8526e93efdb230ad53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="d555f-103">在 HDInsight 上使用 R 伺服器安裝 RStudio</span><span class="sxs-lookup"><span data-stu-id="d555f-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="d555f-104">此文章說明如何使用自訂指令碼，在叢集的邊緣節點上安裝 [RStudio Server](https://www.rstudio.com/products/rstudio-server/) 的社群 (免費) 版本。</span><span class="sxs-lookup"><span data-stu-id="d555f-104">This article describes how to install the community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on the edge node of a cluster using a custom script.</span></span> <span data-ttu-id="d555f-105">RStudio Server 提供瀏覽器型 IDE 供遠端用戶端使用，而且在 Linux 上廣為使用。</span><span class="sxs-lookup"><span data-stu-id="d555f-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="d555f-106">目前有多種適用於 R 的整合式開發環境 (IDE)，包括：</span><span class="sxs-lookup"><span data-stu-id="d555f-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="d555f-107">Microsoft 的 [Visual Studio R 工具](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="d555f-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="d555f-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="d555f-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="d555f-109">Walware 的 Eclipse 型 [StatET](http://www.walware.de/goto/statet)。</span><span class="sxs-lookup"><span data-stu-id="d555f-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="d555f-110">在 HDInsight 叢集的邊緣節點上安裝 RStudio Server 的優點在於可提供完整的 IDE 體驗，供透過叢集上的 R 伺服器來開發及執行 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-110">The advantage of installing RStudio Server on the edge node of an HDInsight cluster is that it provides a full IDE experience for the development and execution of R scripts with R Server on the cluster.</span></span> <span data-ttu-id="d555f-111">相較於預設使用 R 主控台的情況，此設定可大幅提高生產力。</span><span class="sxs-lookup"><span data-stu-id="d555f-111">This configuration can be considerably more productive than default use of the R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="d555f-112">本文中描述的程序僅適用於在佈建叢集時未選擇安裝 RStudio Server 社群版的情況。</span><span class="sxs-lookup"><span data-stu-id="d555f-112">The procedure described in this article is only relevant if you did not select to install RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="d555f-113">如果您已在佈建期間新增它，則可以按一下叢集入口 Azure 入口網站中的 [R 伺服器儀表板] 圖格，然後在 [R Studio Server] 圖格上存取它。</span><span class="sxs-lookup"><span data-stu-id="d555f-113">If you added it during provisioning, then to access it you click on the **R Server Dashboards** tile in the Azure portal entry for your cluster, then on the **R Studio Server** tile.</span></span> 

<span data-ttu-id="d555f-114">如果您偏好使用 RStudio Server 的商業授權 Pro 版本，請依照 [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/) 的安裝指示執行。</span><span class="sxs-lookup"><span data-stu-id="d555f-114">If you prefer to use the commercially licensed Pro version of RStudio Server, you must follow the installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="d555f-115">若您使用 HDInsight 叢集，且 R 是使用[安裝 R 指令碼動作](hdinsight-hadoop-r-scripts-linux.md)安裝的，則此文件中的步驟將無法正確執行，因為它們要求 HDInsight 叢集上必須有 R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d555f-115">If you are using an HDInsight cluster for which R was installed using the [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), the steps in this document will not work correctly as they require an R Server on the HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="d555f-116">先決條件</span><span class="sxs-lookup"><span data-stu-id="d555f-116">Prerequisites</span></span>

* <span data-ttu-id="d555f-117">具有 R 伺服器的 Azure HDInsight 叢集已安裝。</span><span class="sxs-lookup"><span data-stu-id="d555f-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="d555f-118">如需相關指示，請參閱[開始在 HDInsight 叢集上使用 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d555f-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="d555f-119">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d555f-119">An SSH client.</span></span> <span data-ttu-id="d555f-120">針對 Linux 和 Unix 發行版本或 Macintosh OS X，`ssh` 命令是隨作業系統提供。</span><span class="sxs-lookup"><span data-stu-id="d555f-120">For Linux and Unix distributions or Macintosh OS X, the `ssh` command is provided with the operating system.</span></span> <span data-ttu-id="d555f-121">針對 Windows，我們建議使用 [Cygwin](http://www.redhat.com/services/custom/cygwin/) 與 [OpenSSH 選項](https://www.youtube.com/watch?v=CwYSvvGaiWU)，或 [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="d555f-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with the [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-the-cluster-using-a-custom-script"></a><span data-ttu-id="d555f-122">使用自訂指令碼在叢集上安裝 RStudio</span><span class="sxs-lookup"><span data-stu-id="d555f-122">Install RStudio on the cluster using a custom script</span></span>

<span data-ttu-id="d555f-123">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="d555f-123">Here are the steps:</span></span>

1. <span data-ttu-id="d555f-124">識別叢集的邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d555f-124">Identify the edge node of the cluster.</span></span> <span data-ttu-id="d555f-125">針對具有 R 伺服器的 HDInsight 叢集，以下是前端節點和邊緣節點的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="d555f-125">For an HDInsight cluster with R Server, following is the naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="d555f-126">前端節點 `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="d555f-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="d555f-127">邊緣節點 `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="d555f-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="d555f-128">使用步驟 1 中提供的命名模式以 SSH 方式連接至叢集的邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d555f-128">SSH into the edge node of the cluster using the naming pattern provided in step 1.</span></span> <span data-ttu-id="d555f-129">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="d555f-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="d555f-130">一旦連線，就會變成叢集上的根使用者。</span><span class="sxs-lookup"><span data-stu-id="d555f-130">Once you are connected, become a root user on the cluster.</span></span> <span data-ttu-id="d555f-131">在 SSH 工作階段中，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-131">In the SSH session, use the following command:</span></span>

        sudo su -

4. <span data-ttu-id="d555f-132">下載自訂指令碼以安裝 RStudio。</span><span class="sxs-lookup"><span data-stu-id="d555f-132">Download the custom script to install RStudio.</span></span> <span data-ttu-id="d555f-133">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-133">Use the following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="d555f-134">變更自訂指令碼檔案的權限，然後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-134">Change the permissions on the custom script file and run the script.</span></span> <span data-ttu-id="d555f-135">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-135">Use the following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="d555f-136">如果您在建立具有 R 伺服器的 HDInsight 叢集時使用 SSH 密碼，您可以略過此步驟，並繼續進行下一步。</span><span class="sxs-lookup"><span data-stu-id="d555f-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed to the next.</span></span> <span data-ttu-id="d555f-137">如果您是使用 SSH 金鑰建立叢集，您必須為您的 SSH 使用者設定密碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-137">If you used an SSH key instead to create the cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="d555f-138">連線到 RStudio 時，您會需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-138">You need this password when connecting to RStudio.</span></span> <span data-ttu-id="d555f-139">執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-139">Run the following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="d555f-140">當系統提示您輸入**目前的 Kerberos 密碼**時，請按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="d555f-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="d555f-141">請注意，您必須將 `USERNAME` 取代為您的 HDInsight 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="d555f-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="d555f-142">如果已成功設定您的密碼，應該會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="d555f-142">If your password is successfully set, you should see the following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="d555f-143">結束 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d555f-143">Exit the SSH session.</span></span>

8. <span data-ttu-id="d555f-144">建立到叢集的 SSH 通道，方法是將 HDInsight 叢集上的 `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` 對應至用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="d555f-144">Create an SSH tunnel to the cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on the HDInsight cluster to the client machine.</span></span> <span data-ttu-id="d555f-145">您必須在開啟新的瀏覽器工作階段之前，建立 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="d555f-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="d555f-146">在已安裝 [Cygwin](http://www.redhat.com/services/custom/cygwin/) 的 Linux 用戶端或 Windows 用戶端上，開啟終端機工作階段並且使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use the following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="d555f-147">以您 HDInsight 叢集的 SSH 使用者取代 **USERNAME**，並以您 HDInsight 叢集的名稱取代 **CLUSTERNAME**。</span><span class="sxs-lookup"><span data-stu-id="d555f-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>
       <span data-ttu-id="d555f-148">您也可以透過新增 `-i id_rsa_key` 來使用 SSH 金鑰而非密碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="d555f-149">如果使用 Windows 用戶端與 PuTTY，則</span><span class="sxs-lookup"><span data-stu-id="d555f-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="d555f-150">開啟 PuTTY，並輸入連線資訊。</span><span class="sxs-lookup"><span data-stu-id="d555f-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="d555f-151">在對話方塊左側的 [類別] 區段中，依序展開 [連線] 和 [SSH]，然後選取 [通道]。</span><span class="sxs-lookup"><span data-stu-id="d555f-151">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="d555f-152">在 [ **控制 SSH 連接埠轉送的選項** ] 表單中提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d555f-152">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="d555f-153">**來源連接埠** - 您想要轉送之用戶端上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d555f-153">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="d555f-154">例如， **8787**。</span><span class="sxs-lookup"><span data-stu-id="d555f-154">For example, **8787**.</span></span>
        * <span data-ttu-id="d555f-155">**目的地** - 必須對應至本機用戶端電腦的目的地。</span><span class="sxs-lookup"><span data-stu-id="d555f-155">**Destination** - The destination that must be mapped to the local client machine.</span></span> <span data-ttu-id="d555f-156">例如，**localhost:8787**。</span><span class="sxs-lookup"><span data-stu-id="d555f-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="d555f-157">![建立 SSH 通道](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "建立 SSH 通道")</span><span class="sxs-lookup"><span data-stu-id="d555f-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="d555f-158">按一下 [新增] 以新增設定，然後按一下 [開啟] 以開啟 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="d555f-158">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>
     5. <span data-ttu-id="d555f-159">當系統顯示提示時，請登入伺服器以建立 SSH 工作階段並啟用該通道。</span><span class="sxs-lookup"><span data-stu-id="d555f-159">When prompted, log in to the server to establish an SSH session and enable the tunnel.</span></span>

9. <span data-ttu-id="d555f-160">開啟網頁瀏覽器，並根據您針對通道輸入的連接埠輸入下列 URL：</span><span class="sxs-lookup"><span data-stu-id="d555f-160">Open a web browser and enter the following URL based on the port you entered for the tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="d555f-161">系統將會提示您輸入 SSH 使用者名稱與密碼以連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="d555f-161">You are prompted to enter the SSH username and password to connect to the cluster.</span></span> <span data-ttu-id="d555f-162">如果您在建立叢集時使用 SSH 金鑰，則必須輸入在步驟 5 中所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-162">If you used an SSH key while creating the cluster, you must enter the password you created in step 5.</span></span>

    <span data-ttu-id="d555f-163">![連線至 R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "建立 SSH 通道")</span><span class="sxs-lookup"><span data-stu-id="d555f-163">![Connect to R Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="d555f-164">若要測試 RStudio 安裝是否成功，您可以執行測試指令碼，該指令碼會在叢集上執行以 R 為基礎的 MapReduce 與 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="d555f-164">To test whether the RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on the cluster.</span></span> <span data-ttu-id="d555f-165">若要下載要在 RStudio 中執行的測試指令碼，請返回 SSH 主控台並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-165">To download the test script to run in RStudio, go back to the SSH console and enter the following commands:</span></span>

    *    <span data-ttu-id="d555f-166">如果您建立具有 R 的 Hadoop 叢集，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="d555f-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="d555f-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="d555f-168">如果您已建立具有 R 的 Spark 叢集，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="d555f-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="d555f-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="d555f-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="d555f-170">在 RStudio 中，會看到您所下載的測試指令碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-170">In RStudio, you see the test script you downloaded.</span></span> <span data-ttu-id="d555f-171">按兩下以開啟該檔案，選取檔案的內容，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="d555f-171">Double-click the file to open it, select the contents of the file, and then click **Run**.</span></span> <span data-ttu-id="d555f-172">您應該可以在 [主控台] 窗格中看到輸出：</span><span class="sxs-lookup"><span data-stu-id="d555f-172">You should see the output in the **Console** pane:</span></span>

   <span data-ttu-id="d555f-173">![測試安裝](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "測試安裝")</span><span class="sxs-lookup"><span data-stu-id="d555f-173">![Test the installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test the installation")</span></span>

<span data-ttu-id="d555f-174">另一個做法是輸入 `source(testhdi.r)` 或 `source(testhdi_spark.r)` 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d555f-174">Another option would be to type `source(testhdi.r)` or `source(testhdi_spark.r)` to execute the script.</span></span>

## <a name="see-also"></a><span data-ttu-id="d555f-175">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d555f-175">See also</span></span>

* [<span data-ttu-id="d555f-176">適用於 HDInsight 叢集上的 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="d555f-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="d555f-177">適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="d555f-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

