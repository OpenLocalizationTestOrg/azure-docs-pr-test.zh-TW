---
title: "適用於 Visual Studio 與 Hortonworks 沙箱-Azure HDInsight aaaData Lake 工具 |Microsoft 文件"
description: "了解如何 toouse hello for Visual Studio 與 hello Hortonworks 沙箱本機 VM 中執行 Azure 資料湖工具。 您可以使用這些工具來建立及 hello 沙箱，以及檢視工作的輸出和記錄上執行 Hive 和 Pig 工作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="6d118-104">Hello Azure 資料湖 tools for Visual Studio 使用 hello Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="6d118-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="6d118-105">Azure Data Lake 包含使用於一般 Hadoop 叢集的工具。</span><span class="sxs-lookup"><span data-stu-id="6d118-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="6d118-106">本文件提供 hello 步驟需要 toouse hello Data Lake 工具與 hello Hortonworks 沙箱本機的虛擬機器中執行。</span><span class="sxs-lookup"><span data-stu-id="6d118-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="6d118-107">使用 hello Hortonworks 沙箱可讓您在本機開發環境上的 Hadoop toowork。</span><span class="sxs-lookup"><span data-stu-id="6d118-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="6d118-108">您已經開發了解決方案，並想 toodeploy 之後它在標尺，您可以再移動 tooan HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6d118-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d118-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d118-109">Prerequisites</span></span>

* <span data-ttu-id="6d118-110">hello Hortonworks 沙箱，您的開發環境上執行的虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="6d118-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="6d118-111">本文件所撰寫，並與 hello 沙箱 Oracle VirtualBox 中執行測試。</span><span class="sxs-lookup"><span data-stu-id="6d118-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="6d118-112">如需 hello 沙箱設定資訊，請參閱 hello [hello Hortonworks 沙箱快速入門。](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="6d118-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="6d118-113">文件。</span><span class="sxs-lookup"><span data-stu-id="6d118-113">document.</span></span>

* <span data-ttu-id="6d118-114">Visual Studio 2013、Visual Studio 2015 或 Visual Studio 2017 (任一版本)。</span><span class="sxs-lookup"><span data-stu-id="6d118-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="6d118-115">hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/) 2.7.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d118-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="6d118-116">hello [Azure 資料湖 tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)。</span><span class="sxs-lookup"><span data-stu-id="6d118-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="6d118-117">設定密碼 hello 沙箱</span><span class="sxs-lookup"><span data-stu-id="6d118-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="6d118-118">請確定該 hello Hortonworks 沙箱正在執行。</span><span class="sxs-lookup"><span data-stu-id="6d118-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="6d118-119">然後遵循 hello 中的 hello 步驟[開始 hello Hortonworks 沙箱](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords)文件。</span><span class="sxs-lookup"><span data-stu-id="6d118-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="6d118-120">下列步驟設定 hello hello SSH 密碼`root`帳戶，而且 hello Ambari`admin`帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d118-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="6d118-121">當您從 Visual Studio 連接 toohello 沙箱時，會使用這些密碼。</span><span class="sxs-lookup"><span data-stu-id="6d118-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="6d118-122">連接 hello 工具 toohello 沙箱</span><span class="sxs-lookup"><span data-stu-id="6d118-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="6d118-123">開啟 Visual Studio，選取 [檢視]，然後選取 [伺服器總管]。</span><span class="sxs-lookup"><span data-stu-id="6d118-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="6d118-124">從**伺服器總管**，以滑鼠右鍵按一下 hello **HDInsight**項目，然後選取**連接 tooHDInsight 模擬器**。</span><span class="sxs-lookup"><span data-stu-id="6d118-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![螢幕擷取畫面的伺服器總管 中，與連接 tooHDInsight 反白顯示的模擬器](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="6d118-126">從 hello**連接 tooHDInsight 模擬器**對話方塊方塊中，輸入您設定如 Ambari hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="6d118-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![對話方塊的螢幕擷取畫面，其中密碼文字方塊已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="6d118-128">選取**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="6d118-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="6d118-129">使用 hello**密碼**欄位 tooenter hello 密碼在您設定 hello`root`帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d118-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="6d118-130">保留 hello hello 預設值的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="6d118-130">Leave hello other fields at hello default value.</span></span>

    ![對話方塊的螢幕擷取畫面，其中密碼文字方塊已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="6d118-132">選取**下一步**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="6d118-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="6d118-133">等候 hello 服務 toofinish 的驗證。</span><span class="sxs-lookup"><span data-stu-id="6d118-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="6d118-134">在某些情況下，驗證可能失敗，而且提示您 tooupdate hello 組態。</span><span class="sxs-lookup"><span data-stu-id="6d118-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="6d118-135">如果驗證失敗時，選取**更新**，並等候 hello 設定及驗證 hello 服務 toofinish。</span><span class="sxs-lookup"><span data-stu-id="6d118-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![對話方塊的螢幕擷取畫面，其中 [更新] 按鈕已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="6d118-137">hello 更新程序會使用 Ambari toomodify hello Hortonworks 沙箱組態 toowhat 所預期的 hello Data Lake tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6d118-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="6d118-138">驗證已完成之後，請選取**完成**toocomplete 組態。</span><span class="sxs-lookup"><span data-stu-id="6d118-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="6d118-139">![對話方塊的螢幕擷取畫面，其中 [完成] 按鈕已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="6d118-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="6d118-140">根據您的開發環境和 hello 配置 toohello 虛擬機器記憶體的數量 hello 速度，它可以花幾分鐘的時間 tooconfigure 並驗證 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="6d118-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="6d118-141">執行這些步驟之後，您現在可以**HDInsight 本機叢集**hello] 下的項目在 [伺服器總管**HDInsight** > 一節。</span><span class="sxs-lookup"><span data-stu-id="6d118-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="6d118-142">撰寫 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="6d118-142">Write a Hive query</span></span>

<span data-ttu-id="6d118-143">Hive 會提供類似 SQL 的查詢語言 (HiveQL)，以便處理結構化資料。</span><span class="sxs-lookup"><span data-stu-id="6d118-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="6d118-144">使用 hello 遵循步驟 toolearn toorun 隨 hello 本機叢集對查詢的方式。</span><span class="sxs-lookup"><span data-stu-id="6d118-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="6d118-145">在**伺服器總管**，hello hello 本機叢集之前，加入的項目上按一下滑鼠右鍵，然後選取**撰寫 Hive 查詢**。</span><span class="sxs-lookup"><span data-stu-id="6d118-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![[伺服器總管] 的螢幕擷取畫面，其中 [撰寫 Hive 查詢] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="6d118-147">新的查詢視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6d118-147">A new query window appears.</span></span> <span data-ttu-id="6d118-148">這裡您可以快速地撰寫並送出查詢 toohello 本機叢集。</span><span class="sxs-lookup"><span data-stu-id="6d118-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="6d118-149">在 hello 新查詢視窗中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d118-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="6d118-150">toorun hello 查詢中，選取**送出**hello hello 視窗上方。</span><span class="sxs-lookup"><span data-stu-id="6d118-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="6d118-151">保留 hello 其他值 (**批次**和伺服器名稱) 在 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6d118-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![查詢視窗中，強調顯示 hello 送出按鈕的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="6d118-153">您也可以使用 hello 下拉式選單接下來太**送出**tooselect**進階**。</span><span class="sxs-lookup"><span data-stu-id="6d118-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="6d118-154">進階的選項可讓您 tooprovide 其他選項時您送出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="6d118-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![[提交指令碼] 對話方塊的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="6d118-156">您送出 hello 查詢之後，會顯示 hello 作業狀態。</span><span class="sxs-lookup"><span data-stu-id="6d118-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="6d118-157">在處理 Hadoop 所 hello 工作狀態會顯示 hello 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d118-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="6d118-158">**工作狀態**提供 hello hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="6d118-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="6d118-159">hello 狀態會定期更新，或者您可以使用 hello 重新整理圖示 toorefresh hello 狀態以手動方式。</span><span class="sxs-lookup"><span data-stu-id="6d118-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![[作業檢視] 對話方塊的螢幕擷取畫面，其中 [作業狀態] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="6d118-161">之後 hello**工作狀態**變更太**已經完成**，導向非循環圖 (DAG) 會顯示。</span><span class="sxs-lookup"><span data-stu-id="6d118-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="6d118-162">此圖說明處理 hello Hive 查詢時，已由 Tez 的 hello 執行路徑。</span><span class="sxs-lookup"><span data-stu-id="6d118-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="6d118-163">Tez 是 hello 預設執行引擎 Hive hello 本機叢集上。</span><span class="sxs-lookup"><span data-stu-id="6d118-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6d118-164">Tez 也是 hello 預設值，當您使用 linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6d118-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="6d118-165">它不是 hello Windows 為基礎的 HDInsight 上的預設值。</span><span class="sxs-lookup"><span data-stu-id="6d118-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="6d118-166">toouse 它，您必須新增 hello 列`set hive.execution.engine = tez;`toohello Hive 查詢的開頭。</span><span class="sxs-lookup"><span data-stu-id="6d118-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="6d118-167">使用 hello**作業輸出**連結 tooview hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="6d118-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="6d118-168">在此情況下，它是 823 hello hello sample_08 資料表中資料列數目。</span><span class="sxs-lookup"><span data-stu-id="6d118-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="6d118-169">您可以檢視 hello 工作的相關診斷資訊使用 hello**作業記錄**和**下載 YARN 記錄**連結。</span><span class="sxs-lookup"><span data-stu-id="6d118-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="6d118-170">您也可以執行 Hive 工作以互動方式變更 hello**批次**欄位太**互動式**。</span><span class="sxs-lookup"><span data-stu-id="6d118-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="6d118-171">接著，選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="6d118-171">Then select **Execute**.</span></span>

    ![[互動式] 與 [執行] 按鈕已反白顯示的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="6d118-173">資料流 hello 處理 toohello 期間所產生的輸出記錄檔的互動式查詢**HiveServer2 輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="6d118-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6d118-174">hello 資訊是 hello 相同可從 hello**作業記錄**連結作業完成之後。</span><span class="sxs-lookup"><span data-stu-id="6d118-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![輸出記錄的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="6d118-176">建立 Hive 專案</span><span class="sxs-lookup"><span data-stu-id="6d118-176">Create a Hive project</span></span>

<span data-ttu-id="6d118-177">您也可以建立包含多個 Hive 指令碼的專案。</span><span class="sxs-lookup"><span data-stu-id="6d118-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="6d118-178">當您將相關的指令碼，或想 toostore 指令碼在版本控制系統，請使用專案。</span><span class="sxs-lookup"><span data-stu-id="6d118-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="6d118-179">在 Visual Studio 中，選取 [檔案]、[新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="6d118-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="6d118-180">從 hello 專案清單中，展開**範本**，依序展開**Azure 資料湖**，然後選取**HIVE (HDInsight)**。</span><span class="sxs-lookup"><span data-stu-id="6d118-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="6d118-181">從範本 hello 清單，選取**hive 控制檔的範例**。</span><span class="sxs-lookup"><span data-stu-id="6d118-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="6d118-182">輸入名稱和位置，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d118-182">Enter a name and location, and then select **OK**.</span></span>

    ![[新增專案] 視窗的螢幕擷取畫面，其中 [Azure Data Lake]、[HIVE]、[Hive 範例] 與 [確定] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="6d118-184">hello **hive 控制檔的範例**專案包含兩個指令碼， **WebLogAnalysis.hql**和**SensorDataAnalysis.hql**。</span><span class="sxs-lookup"><span data-stu-id="6d118-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="6d118-185">您可以送出使用這些指令碼 hello 相同**送出**hello hello 視窗上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d118-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="6d118-186">建立 Pig 專案</span><span class="sxs-lookup"><span data-stu-id="6d118-186">Create a Pig project</span></span>

<span data-ttu-id="6d118-187">Hive 提供類似 SQL 的語言來處理結構化的資料，Pig 的運作方式是藉由對資料執行轉換。</span><span class="sxs-lookup"><span data-stu-id="6d118-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="6d118-188">Pig 提供可讓您 toodevelop 的語言 （Pig 拉丁） 轉換的管線。</span><span class="sxs-lookup"><span data-stu-id="6d118-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="6d118-189">toouse Pig 與 hello 本機叢集，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d118-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="6d118-190">開啟 Visual Studio，並依序選取 [檔案] > [新增] 和 [專案]。</span><span class="sxs-lookup"><span data-stu-id="6d118-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="6d118-191">從 hello 專案清單中，展開**範本**，依序展開**Azure 資料湖**，然後選取**Pig (HDInsight)**。</span><span class="sxs-lookup"><span data-stu-id="6d118-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="6d118-192">從範本 hello 清單，選取**Pig 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6d118-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="6d118-193">輸入名稱、位置，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d118-193">Enter a name, location, and then select **OK**.</span></span>

    ![[新增專案] 視窗的螢幕擷取畫面，其中 [Azure Data Lake]、[Pig]、[Pig 應用程式] 與 [確定] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="6d118-195">輸入下列文字，做為 hello 內容的 hello hello **script.pig**與此專案所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="6d118-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="6d118-196">而 Pig Hive 比使用不同的語言，您要執行 hello 作業的方式之間會保持一致這兩種語言，透過 hello**送出** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d118-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="6d118-197">選取 hello 旁邊的下拉式清單**送出**Pig 顯示進階送出 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6d118-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![[提交指令碼] 對話方塊的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="6d118-199">也會顯示 hello 工作狀態和輸出，做為 Hive 查詢 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="6d118-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![已完成 Pig 作業的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="6d118-201">檢視作業</span><span class="sxs-lookup"><span data-stu-id="6d118-201">View jobs</span></span>

<span data-ttu-id="6d118-202">資料湖工具也可讓您 tooeasily 檢視已在 Hadoop 執行的作業有關的資訊。</span><span class="sxs-lookup"><span data-stu-id="6d118-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="6d118-203">使用下列步驟 toosee hello 工作已執行 hello 本機叢集上的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d118-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="6d118-204">從**伺服器總管**，hello 本機叢集，以滑鼠右鍵按一下，然後選取**檢視工作**。</span><span class="sxs-lookup"><span data-stu-id="6d118-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="6d118-205">已提交的 toohello 叢集中的作業清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6d118-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![[伺服器總管] 的螢幕擷取畫面，其中 [檢視作業] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="6d118-207">從 hello 工作清單，選取其中一個 tooview hello 工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6d118-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![螢幕擷取畫面的作業瀏覽器中，使用其中一個 hello 反白顯示的作業](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="6d118-209">執行 Hive 或 Pig 查詢，包括連結 tooview hello 輸出和記錄檔資訊之後，您看見類似 toowhat 所顯示的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6d118-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="6d118-210">您也可以修改並重新送出 hello 作業，從這裡。</span><span class="sxs-lookup"><span data-stu-id="6d118-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="6d118-211">檢視 Hive 資料庫</span><span class="sxs-lookup"><span data-stu-id="6d118-211">View Hive databases</span></span>

1. <span data-ttu-id="6d118-212">在**伺服器總管**，展開 hello **HDInsight 本機叢集**項目，然後展開**Hive 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="6d118-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="6d118-213">hello**預設**和**xademo**會顯示 hello 本機叢集上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6d118-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="6d118-214">展開資料庫顯示 hello hello 資料庫內的資料表。</span><span class="sxs-lookup"><span data-stu-id="6d118-214">Expanding a database shows hello tables within hello database.</span></span>

    ![[伺服器總管] 的螢幕擷取畫面，其中資料庫已展開](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="6d118-216">展開資料表，會顯示 hello 該資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="6d118-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="6d118-217">hello tooquickly 檢視的資料，以滑鼠右鍵按一下資料表，然後選取**檢視前 100 個資料列**。</span><span class="sxs-lookup"><span data-stu-id="6d118-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![[伺服器總管] 的螢幕擷取畫面，其中資料表已展開且 [檢視前 100 個資料列] 已選取](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="6d118-219">資料庫和資料表屬性</span><span class="sxs-lookup"><span data-stu-id="6d118-219">Database and table properties</span></span>

<span data-ttu-id="6d118-220">您可以檢視資料庫或資料表的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="6d118-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="6d118-221">選取**屬性**hello 屬性 視窗中顯示 hello 選取項目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6d118-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="6d118-222">例如，請參閱 hello 資訊 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="6d118-222">For example, see hello information shown in hello following screenshot:</span></span>

![[屬性] 視窗的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="6d118-224">建立資料表</span><span class="sxs-lookup"><span data-stu-id="6d118-224">Create a table</span></span>

<span data-ttu-id="6d118-225">toocreate 資料表，以滑鼠右鍵按一下資料庫，然後選取**Create Table**。</span><span class="sxs-lookup"><span data-stu-id="6d118-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![[伺服器總管] 的螢幕擷取畫面，其中 [建立資料表] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="6d118-227">然後，您可以建立 hello 資料表使用的表單。</span><span class="sxs-lookup"><span data-stu-id="6d118-227">You can then create hello table using a form.</span></span> <span data-ttu-id="6d118-228">您可以在 hello hello 下列螢幕擷取畫面底部，查看 hello 原始 HiveQL 使用的 toocreate hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6d118-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![螢幕擷取畫面的 hello 表單使用 toocreate 資料表](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="6d118-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d118-230">Next steps</span></span>

* [<span data-ttu-id="6d118-231">學習 hello ropes 的 hello Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="6d118-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="6d118-232">Hadoop 教學課程 - 開始使用 HDP</span><span class="sxs-lookup"><span data-stu-id="6d118-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
