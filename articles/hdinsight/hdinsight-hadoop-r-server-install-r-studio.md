---
title: "aaaInstall RStudio 使用 HDInsight 的 Azure 上的 R Server |Microsoft 文件"
description: "如何 tooinstall RStudio 與 HDInsight 上的 R 伺服器。"
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
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a><span data-ttu-id="be4ea-103">在 HDInsight 上使用 R 伺服器安裝 RStudio</span><span class="sxs-lookup"><span data-stu-id="be4ea-103">Installing RStudio with R Server on HDInsight</span></span>

<span data-ttu-id="be4ea-104">本文說明如何 tooinstall hello 社群 （免費） 版本的[RStudio 伺服器](https://www.rstudio.com/products/rstudio-server/)hello 邊緣使用自訂指令碼的叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="be4ea-104">This article describes how tooinstall hello community (free) version of [RStudio Server](https://www.rstudio.com/products/rstudio-server/) on hello edge node of a cluster using a custom script.</span></span> <span data-ttu-id="be4ea-105">RStudio Server 提供瀏覽器型 IDE 供遠端用戶端使用，而且在 Linux 上廣為使用。</span><span class="sxs-lookup"><span data-stu-id="be4ea-105">RStudio Server provides a browser-based IDE for use by remote clients and is widely used on Linux.</span></span> <span data-ttu-id="be4ea-106">目前有多種適用於 R 的整合式開發環境 (IDE)，包括：</span><span class="sxs-lookup"><span data-stu-id="be4ea-106">There are multiple integrated development environments (IDEs) available for R today, including:</span></span>

- <span data-ttu-id="be4ea-107">Microsoft 的 [Visual Studio R 工具](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span><span class="sxs-lookup"><span data-stu-id="be4ea-107">Microsoft’s  [R Tools for Visual Studio](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS)</span></span> 
- [<span data-ttu-id="be4ea-108">RStudio Server</span><span class="sxs-lookup"><span data-stu-id="be4ea-108">RStudio Server</span></span>](https://www.rstudio.com/products/rstudio-server/) 
- <span data-ttu-id="be4ea-109">Walware 的 Eclipse 型 [StatET](http://www.walware.de/goto/statet)。</span><span class="sxs-lookup"><span data-stu-id="be4ea-109">Walware’s Eclipse-based [StatET](http://www.walware.de/goto/statet).</span></span>

<span data-ttu-id="be4ea-110">hello 邊緣的 HDInsight 叢集節點上安裝 RStudio 伺服器 hello 優點是，它會提供完整的 IDE 體驗 hello 開發和執行 R 指令碼與 R 伺服器 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="be4ea-110">hello advantage of installing RStudio Server on hello edge node of an HDInsight cluster is that it provides a full IDE experience for hello development and execution of R scripts with R Server on hello cluster.</span></span> <span data-ttu-id="be4ea-111">這項設定可以大幅提高生產力，比預設 hello R 主控台使用。</span><span class="sxs-lookup"><span data-stu-id="be4ea-111">This configuration can be considerably more productive than default use of hello R Console.</span></span>

> [!NOTE]
> <span data-ttu-id="be4ea-112">只有相關，如果您未選取 tooinstall RStudio Server community edition，佈建叢集時 hello 本文中所述的程序。</span><span class="sxs-lookup"><span data-stu-id="be4ea-112">hello procedure described in this article is only relevant if you did not select tooinstall RStudio Server community edition when provisioning your cluster.</span></span> <span data-ttu-id="be4ea-113">如果您加入期間佈建，然後它您按一下 hello tooaccess **R Server 儀表板**磚 hello Azure 入口網站項目用於您的叢集，然後在 hello **R Studio Server**磚。</span><span class="sxs-lookup"><span data-stu-id="be4ea-113">If you added it during provisioning, then tooaccess it you click on hello **R Server Dashboards** tile in hello Azure portal entry for your cluster, then on hello **R Studio Server** tile.</span></span> 

<span data-ttu-id="be4ea-114">如果您偏好的 RStudio Server toouse hello 商業授權 Pro 版本，您必須遵循 hello 安裝指示，從[RStudio 伺服器](https://www.rstudio.com/products/rstudio/download-server/)。</span><span class="sxs-lookup"><span data-stu-id="be4ea-114">If you prefer toouse hello commercially licensed Pro version of RStudio Server, you must follow hello installation instructions from [RStudio Server](https://www.rstudio.com/products/rstudio/download-server/).</span></span>

> [!NOTE]
> <span data-ttu-id="be4ea-115">如果您使用 HDInsight 叢集的 R 已安裝使用 hello[安裝 R 指令碼動作](hdinsight-hadoop-r-scripts-linux.md)，本文件中的 hello 步驟將無法運作正確，因為它們需要 R 伺服器 hello HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="be4ea-115">If you are using an HDInsight cluster for which R was installed using hello [Install R Script Action](hdinsight-hadoop-r-scripts-linux.md), hello steps in this document will not work correctly as they require an R Server on hello HDInsight cluster.</span></span>
>
> 

## <a name="prerequisites"></a><span data-ttu-id="be4ea-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="be4ea-116">Prerequisites</span></span>

* <span data-ttu-id="be4ea-117">具有 R 伺服器的 Azure HDInsight 叢集已安裝。</span><span class="sxs-lookup"><span data-stu-id="be4ea-117">An Azure HDInsight cluster with R Server installed.</span></span> <span data-ttu-id="be4ea-118">如需相關指示，請參閱[開始在 HDInsight 叢集上使用 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="be4ea-118">For instructions, see [Get started with R Server on HDInsight clusters](hdinsight-hadoop-r-server-get-started.md).</span></span>
* <span data-ttu-id="be4ea-119">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="be4ea-119">An SSH client.</span></span> <span data-ttu-id="be4ea-120">對於 Linux 和 Unix 發佈或 Macintosh OS X，hello `ssh` hello 作業系統提供命令。</span><span class="sxs-lookup"><span data-stu-id="be4ea-120">For Linux and Unix distributions or Macintosh OS X, hello `ssh` command is provided with hello operating system.</span></span> <span data-ttu-id="be4ea-121">對於 Windows 中，我們建議[Cygwin](http://www.redhat.com/services/custom/cygwin/)以 hello [OpenSSH 選項](https://www.youtube.com/watch?v=CwYSvvGaiWU)，或[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="be4ea-121">For Windows, we recommend [Cygwin](http://www.redhat.com/services/custom/cygwin/) with hello [OpenSSH option](https://www.youtube.com/watch?v=CwYSvvGaiWU), or [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a><span data-ttu-id="be4ea-122">使用自訂指令碼的 hello 叢集上安裝 RStudio</span><span class="sxs-lookup"><span data-stu-id="be4ea-122">Install RStudio on hello cluster using a custom script</span></span>

<span data-ttu-id="be4ea-123">Hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="be4ea-123">Here are hello steps:</span></span>

1. <span data-ttu-id="be4ea-124">識別 hello 邊緣 hello 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="be4ea-124">Identify hello edge node of hello cluster.</span></span> <span data-ttu-id="be4ea-125">使用 R Server HDInsight 叢集，以下是 hello 前端節點和邊緣節點的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="be4ea-125">For an HDInsight cluster with R Server, following is hello naming convention for head node and edge node.</span></span>
   * <span data-ttu-id="be4ea-126">前端節點 `CLUSTERNAME-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="be4ea-126">Head node `CLUSTERNAME-ssh.azurehdinsight.net`</span></span>
   * <span data-ttu-id="be4ea-127">邊緣節點 `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span><span class="sxs-lookup"><span data-stu-id="be4ea-127">Edge node `CLUSTERNAME-ed-ssh.azurehdinsight.net`</span></span> 

2. <span data-ttu-id="be4ea-128">SSH 到 hello 邊緣節點之 hello 叢集使用步驟 1 中所提供的 hello 命名模式。</span><span class="sxs-lookup"><span data-stu-id="be4ea-128">SSH into hello edge node of hello cluster using hello naming pattern provided in step 1.</span></span> <span data-ttu-id="be4ea-129">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="be4ea-129">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="be4ea-130">一旦連線後，會變成 hello 叢集上的根使用者。</span><span class="sxs-lookup"><span data-stu-id="be4ea-130">Once you are connected, become a root user on hello cluster.</span></span> <span data-ttu-id="be4ea-131">Hello SSH 工作階段中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-131">In hello SSH session, use hello following command:</span></span>

        sudo su -

4. <span data-ttu-id="be4ea-132">下載 hello 自訂指令碼 tooinstall RStudio。</span><span class="sxs-lookup"><span data-stu-id="be4ea-132">Download hello custom script tooinstall RStudio.</span></span> <span data-ttu-id="be4ea-133">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-133">Use hello following command:</span></span>

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. <span data-ttu-id="be4ea-134">變更 hello hello 自訂指令碼檔案的權限，並執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-134">Change hello permissions on hello custom script file and run hello script.</span></span> <span data-ttu-id="be4ea-135">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-135">Use hello following commands:</span></span>

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. <span data-ttu-id="be4ea-136">如果您使用 SSH 密碼時使用 R 伺服器建立的 HDInsight 叢集，則可以略過此步驟，並繼續 toohello 下一步。</span><span class="sxs-lookup"><span data-stu-id="be4ea-136">If you used an SSH password while creating an HDInsight cluster with R Server, you can skip this step and proceed toohello next.</span></span> <span data-ttu-id="be4ea-137">如果您使用 SSH 金鑰改為 toocreate hello 叢集，您必須設定密碼 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="be4ea-137">If you used an SSH key instead toocreate hello cluster, you must set a password for your SSH user.</span></span> <span data-ttu-id="be4ea-138">連接 tooRStudio 時，您會需要此密碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-138">You need this password when connecting tooRStudio.</span></span> <span data-ttu-id="be4ea-139">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-139">Run hello following commands:</span></span>

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. <span data-ttu-id="be4ea-140">當系統提示您輸入**目前的 Kerberos 密碼**時，請按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="be4ea-140">When prompted for **Current Kerberos password**, press **ENTER**.</span></span>  <span data-ttu-id="be4ea-141">請注意，您必須將 `USERNAME` 取代為您的 HDInsight 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="be4ea-141">Note that you must replace `USERNAME` with an SSH user for your HDInsight cluster.</span></span> <span data-ttu-id="be4ea-142">如果已成功設定您的密碼，您應該會看到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-142">If your password is successfully set, you should see hello following message:</span></span>

        passwd: password updated successfully

    <span data-ttu-id="be4ea-143">結束 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="be4ea-143">Exit hello SSH session.</span></span>

8. <span data-ttu-id="be4ea-144">建立對應的 SSH 通道 toohello 叢集`ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`上 hello HDInsight 叢集 toohello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="be4ea-144">Create an SSH tunnel toohello cluster by mapping `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` on hello HDInsight cluster toohello client machine.</span></span> <span data-ttu-id="be4ea-145">您必須在開啟新的瀏覽器工作階段之前，建立 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="be4ea-145">You must create an SSH tunnel before opening a new browser session.</span></span>

   * <span data-ttu-id="be4ea-146">在 Linux 用戶端或 Windows 用戶端與[Cygwin](http://www.redhat.com/services/custom/cygwin/)，開啟終端機工作階段，並使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-146">On a Linux client or a Windows client with [Cygwin](http://www.redhat.com/services/custom/cygwin/), open a terminal session and use hello following command:</span></span>

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       <span data-ttu-id="be4ea-147">取代**USERNAME**與您的 HDInsight 叢集和取代的 SSH 使用者**CLUSTERNAME** hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="be4ea-147">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>
       <span data-ttu-id="be4ea-148">您也可以透過新增 `-i id_rsa_key` 來使用 SSH 金鑰而非密碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-148">You can also use an SSH key rather than a password by adding `-i id_rsa_key`.</span></span>        
   * <span data-ttu-id="be4ea-149">如果使用 Windows 用戶端與 PuTTY，則</span><span class="sxs-lookup"><span data-stu-id="be4ea-149">If using a Windows client with PuTTY then</span></span>

     1. <span data-ttu-id="be4ea-150">開啟 PuTTY，並輸入連線資訊。</span><span class="sxs-lookup"><span data-stu-id="be4ea-150">Open PuTTY, and enter your connection information.</span></span>
     2. <span data-ttu-id="be4ea-151">在 hello**類別**區段 toohello 方 hello 對話方塊中，展開**連接**，依序展開**SSH**，然後選取**通道**。</span><span class="sxs-lookup"><span data-stu-id="be4ea-151">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>
     3. <span data-ttu-id="be4ea-152">提供下列資訊在 hello hello**選項控制 SSH 連接埠轉送**表單：</span><span class="sxs-lookup"><span data-stu-id="be4ea-152">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>

        * <span data-ttu-id="be4ea-153">**來源連接埠**-hello 想 tooforward hello 用戶端上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="be4ea-153">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="be4ea-154">例如， **8787**。</span><span class="sxs-lookup"><span data-stu-id="be4ea-154">For example, **8787**.</span></span>
        * <span data-ttu-id="be4ea-155">**目的地**-hello 目的地必須是對應 toohello 本機用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="be4ea-155">**Destination** - hello destination that must be mapped toohello local client machine.</span></span> <span data-ttu-id="be4ea-156">例如，**localhost:8787**。</span><span class="sxs-lookup"><span data-stu-id="be4ea-156">For example, **localhost:8787**.</span></span>

            <span data-ttu-id="be4ea-157">![建立 SSH 通道](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "建立 SSH 通道")</span><span class="sxs-lookup"><span data-stu-id="be4ea-157">![Create an SSH tunnel](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "Create an SSH tunnel")</span></span>

     4. <span data-ttu-id="be4ea-158">按一下**新增**tooadd hello 設定，然後按一下**開啟**tooopen SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="be4ea-158">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>
     5. <span data-ttu-id="be4ea-159">出現提示時，登入 toohello 伺服器 tooestablish 的 SSH 工作階段，並啟用 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="be4ea-159">When prompted, log in toohello server tooestablish an SSH session and enable hello tunnel.</span></span>

9. <span data-ttu-id="be4ea-160">開啟網頁瀏覽器並輸入下列 URL，根據您所輸入的 hello 通道的 hello 連接埠的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-160">Open a web browser and enter hello following URL based on hello port you entered for hello tunnel:</span></span>

        http://localhost:8787/ 

10. <span data-ttu-id="be4ea-161">您必須提示的 tooenter hello SSH 使用者名稱和密碼 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="be4ea-161">You are prompted tooenter hello SSH username and password tooconnect toohello cluster.</span></span> <span data-ttu-id="be4ea-162">如果您使用 SSH 金鑰建立 hello 叢集時，您必須輸入您在步驟 5 中建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-162">If you used an SSH key while creating hello cluster, you must enter hello password you created in step 5.</span></span>

    <span data-ttu-id="be4ea-163">![連接導覽 Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "建立 SSH 通道")</span><span class="sxs-lookup"><span data-stu-id="be4ea-163">![Connect tooR Studio](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "Create an SSH tunnel")</span></span>

11. <span data-ttu-id="be4ea-164">tootest hello RStudio 安裝是否成功，您可以執行測試指令碼 hello 叢集執行 R MapReduce 和 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="be4ea-164">tootest whether hello RStudio installation was successful, you can run a test script that executes R-based MapReduce and Spark jobs on hello cluster.</span></span> <span data-ttu-id="be4ea-165">在 RStudio、 toodownload hello 測試指令碼 toorun 返回 toohello SSH 主控台，並輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="be4ea-165">toodownload hello test script toorun in RStudio, go back toohello SSH console and enter hello following commands:</span></span>

    *    <span data-ttu-id="be4ea-166">如果您建立具有 R 的 Hadoop 叢集，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="be4ea-166">If you created a Hadoop cluster with R, use this command:</span></span>

            <span data-ttu-id="be4ea-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span><span class="sxs-lookup"><span data-stu-id="be4ea-167">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r</span></span>
    *    <span data-ttu-id="be4ea-168">如果您已建立具有 R 的 Spark 叢集，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="be4ea-168">If you created a Spark cluster with R, use this command:</span></span>

            <span data-ttu-id="be4ea-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span><span class="sxs-lookup"><span data-stu-id="be4ea-169">wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r</span></span>

12. <span data-ttu-id="be4ea-170">在 RStudio，您會看到 hello 測試您所下載的指令碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-170">In RStudio, you see hello test script you downloaded.</span></span> <span data-ttu-id="be4ea-171">按兩下 hello 檔案 tooopen，選取 hello hello 檔案內容，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="be4ea-171">Double-click hello file tooopen it, select hello contents of hello file, and then click **Run**.</span></span> <span data-ttu-id="be4ea-172">您應該會看見 hello 中的 hello 輸出**主控台**窗格：</span><span class="sxs-lookup"><span data-stu-id="be4ea-172">You should see hello output in hello **Console** pane:</span></span>

   <span data-ttu-id="be4ea-173">![測試 hello 安裝](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "測試 hello 安裝")</span><span class="sxs-lookup"><span data-stu-id="be4ea-173">![Test hello installation](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello installation")</span></span>

<span data-ttu-id="be4ea-174">另一個選項是 tootype`source(testhdi.r)`或`source(testhdi_spark.r)`tooexecute hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="be4ea-174">Another option would be tootype `source(testhdi.r)` or `source(testhdi_spark.r)` tooexecute hello script.</span></span>

## <a name="see-also"></a><span data-ttu-id="be4ea-175">另請參閱</span><span class="sxs-lookup"><span data-stu-id="be4ea-175">See also</span></span>

* [<span data-ttu-id="be4ea-176">適用於 HDInsight 叢集上的 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="be4ea-176">Compute context options for R Server on HDInsight clusters</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="be4ea-177">適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="be4ea-177">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

