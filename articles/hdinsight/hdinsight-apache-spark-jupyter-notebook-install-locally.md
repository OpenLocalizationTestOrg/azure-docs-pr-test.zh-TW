---
title: "在本機 aaaInstall Jupyter （& s) 連接 tooan Azure HDInsight Spark 叢集 |Microsoft 文件"
description: "深入了解如何在電腦上本機 tooinstall Jupyter 筆記本並將它連接 Azure HDInsight 上的 tooan Apache Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="5c1bb-103">在您的電腦上安裝 Jupyter 筆記本，並連接 tooApache HDInsight 上的 Spark</span><span class="sxs-lookup"><span data-stu-id="5c1bb-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="5c1bb-104">在這篇文章您了解如何以 hello tooinstall Jupyter 筆記本自訂 PySpark （適用於 Python) 並 （適用於 Scala) Spark 核心與二手的優勢，並連接 hello 筆記本 tooan HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="5c1bb-105">可以是本機電腦上的理由 tooinstall Jupyter 數，而且可以有以及一些挑戰。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="5c1bb-106">如需此詳細資訊，請參閱 hello 節[為什麼我應該安裝 Jupyter 我的電腦上](#why-should-i-install-jupyter-on-my-computer)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="5c1bb-107">您的電腦上安裝 Jupyter 與 hello Spark magic 是三個主要步驟。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="5c1bb-108">安裝 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="5c1bb-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="5c1bb-109">安裝 hello PySpark 和 Spark 核心以 hello Spark 識別常數</span><span class="sxs-lookup"><span data-stu-id="5c1bb-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="5c1bb-110">設定在 HDInsight 上的 Spark magic tooaccess Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5c1bb-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="5c1bb-111">Hello 自訂核心和 hello Spark magic 供 Jupyter notebook 與 HDInsight 叢集相關的詳細資訊，請參閱[透過 Apache Spark Linux Jupyter 筆記本的可用的核心叢集 HDInsight 上](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c1bb-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c1bb-112">Prerequisites</span></span>
<span data-ttu-id="5c1bb-113">此處所列的 hello 必要條件不安裝 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="5c1bb-114">這些是連接 hello Jupyter 筆記本 tooan HDInsight 叢集 hello 筆記本安裝之後。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="5c1bb-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-115">An Azure subscription.</span></span> <span data-ttu-id="5c1bb-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5c1bb-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5c1bb-118">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="5c1bb-119">在電腦上安裝 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="5c1bb-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="5c1bb-120">您必須先安裝 Python，才能安裝 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="5c1bb-121">Python 和 Jupyter 可用一部分 hello [Anaconda 發佈](https://www.continuum.io/downloads)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="5c1bb-122">當您安裝 Anaconda 時，會安裝某個 Python 發行版本。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="5c1bb-123">Anaconda 安裝之後，您可以加入 hello Jupyter 安裝執行適當的命令。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="5c1bb-124">下載 hello [Anaconda installer](https://www.continuum.io/downloads)平台和 hello 執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="5c1bb-125">在執行 hello 安裝精靈，請務必選取 hello 選項 tooadd Anaconda tooyour PATH 變數。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="5c1bb-126">執行下列命令 tooinstall Jupyter hello。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="5c1bb-127">如需有關安裝 Jupyter 的詳細資訊，請參閱[使用 Anaconda 來安裝 Jupyter](http://jupyter.readthedocs.io/en/latest/install.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="5c1bb-128">安裝 hello 核心和 Spark 識別常數</span><span class="sxs-lookup"><span data-stu-id="5c1bb-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="5c1bb-129">如需有關如何在 tooinstall hello Spark magic、 hello PySpark 和 Spark 核心，請遵循 hello hello 安裝指示指示[sparkmagic 文件](https://github.com/jupyter-incubator/sparkmagic#installation)GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="5c1bb-130">hello hello Spark magic 文件中的第一個步驟會要求您 tooinstall Spark 識別常數。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="5c1bb-131">取代下列命令，視您要連接到 hello HDInsight 叢集的 hello 版本而定的 hello hello 連結中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="5c1bb-132">完成之後，遵循 hello 剩餘 hello Spark magic 文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="5c1bb-133">如果您想 tooinstall hello 不同核心，您必須執行步驟 3 中 hello Spark magic 安裝指示 > 一節。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="5c1bb-134">若為叢集 3.4 版，請執行 `pip install sparkmagic==0.2.3` 來安裝 sparkmagic 0.2.3</span><span class="sxs-lookup"><span data-stu-id="5c1bb-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="5c1bb-135">若為叢集 3.5 版和 3.6 版，請執行 `pip install sparkmagic==0.11.2` 來安裝 sparkmagic 0.11.2</span><span class="sxs-lookup"><span data-stu-id="5c1bb-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="5c1bb-136">設定 Spark magic tooconnect tooHDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="5c1bb-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="5c1bb-137">本節中，您會設定安裝舊版 tooconnect tooan 的 Apache Spark 叢集，您必須已經建立 Azure HDInsight 中的 hello Spark 識別常數。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="5c1bb-138">hello Jupyter 組態資訊通常會儲存在 hello 使用者主目錄中。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="5c1bb-139">toolocate 主目錄任何作業系統平台上，遵循的型別 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="5c1bb-140">啟動 hello Python 殼層。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-140">Start hello Python shell.</span></span> <span data-ttu-id="5c1bb-141">在命令視窗中，輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5c1bb-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="5c1bb-142">在 hello Python 殼層中，輸入下列命令 toofind 出 hello 主目錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="5c1bb-143">瀏覽 toohello 主目錄，並建立一個稱為資料夾**.sparkmagic**如果不存在。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="5c1bb-144">Hello 資料夾內建立檔案，稱為**config.json**並新增下列 JSON 片段內文中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="5c1bb-145">以適當的值替代 **{USERNAME}**、**{CLUSTERDNSNAME}** 和 **{BASE64ENCODEDPASSWORD}**。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="5c1bb-146">您可以使用多種公用程式在您偏好的程式設計語言或線上 toogenerate base64 編碼的密碼做為實際的密碼。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="5c1bb-147">設定在 hello 右活動訊號設定`config.json`。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="5c1bb-148">您應該在相同層級為 hello hello 加入這些設定`kernel_python_credentials`和`kernel_scala_credentials`片段您加入稍早。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="5c1bb-149">如需如何及在何處 tooadd hello 活動訊號設定範例，請參閱此[範例 config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="5c1bb-150">若為 `sparkmagic 0.2.3` (叢集 3.4 版)，請加入︰</span><span class="sxs-lookup"><span data-stu-id="5c1bb-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="5c1bb-151">若為 `sparkmagic 0.11.2` (叢集 3.5 版和 3.6 版)，請加入︰</span><span class="sxs-lookup"><span data-stu-id="5c1bb-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="5c1bb-152">活動訊號會傳送工作階段不會遺漏 tooensure。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="5c1bb-153">當電腦進入 toosleep 或已關閉時，不會傳送 hello 活動訊號時，導致 hello 工作階段正在清除。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="5c1bb-154">對於叢集 v3.4，如果您想 toodisable 這種行為，您可以設定 hello 晚總 config`livy.server.interactive.heartbeat.timeout`太`0`從 hello Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="5c1bb-155">針對叢集 v3.5，如果您未設定上述 hello 3.5 組態 hello 工作階段會刪除。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="5c1bb-156">啟動 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-156">Start Jupyter.</span></span> <span data-ttu-id="5c1bb-157">使用 hello hello 命令提示字元中的下列命令。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="5c1bb-158">請確認您可以連接使用 hello Jupyter 筆記本和，您可以使用可用的 hello Spark magic hello 核心 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="5c1bb-159">執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-159">Perform hello following steps.</span></span>

    <span data-ttu-id="5c1bb-160">a.</span><span class="sxs-lookup"><span data-stu-id="5c1bb-160">a.</span></span> <span data-ttu-id="5c1bb-161">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-161">Create a new notebook.</span></span> <span data-ttu-id="5c1bb-162">從 hello 右上角，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="5c1bb-163">您應該會看見 hello 預設核心**Python2**和 hello 的安裝時，兩個新核心**PySpark**和**Spark**。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="5c1bb-164">按一下 [PySpark] 。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-164">Click **PySpark**.</span></span>

    <span data-ttu-id="5c1bb-165">![Jupyter Notebook 中的核心](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter Notebook 中的核心")</span><span class="sxs-lookup"><span data-stu-id="5c1bb-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="5c1bb-166">b.</span><span class="sxs-lookup"><span data-stu-id="5c1bb-166">b.</span></span> <span data-ttu-id="5c1bb-167">執行下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="5c1bb-168">如果成功，您可以擷取 hello 輸出，則會測試連接 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="5c1bb-169">如果您想 tooupdate hello 筆記本設定 tooconnect tooa 不同的叢集時，更新 hello config.json hello 組新的值，如上面的步驟 3 中所示。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="5c1bb-170">為什麼我應該在我的電腦上安裝 Jupyter？</span><span class="sxs-lookup"><span data-stu-id="5c1bb-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="5c1bb-171">可以有許多原因，您可能想在電腦上的 tooinstall Jupyter 並且然後將它連接 tooa Spark HDInsight 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="5c1bb-172">即使 Jupyter 筆記本已可用 hello Azure HDInsight Spark 叢集上，在電腦上安裝 Jupyter 提供 hello 選項 toocreate 本機您的筆記型電腦、 執行的叢集，對測試應用程式，然後上傳 hello筆記本 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="5c1bb-173">tooupload hello 筆記本 toohello 叢集中，您可以上傳它們使用 hello Jupyter 筆記本執行或 hello 叢集，或將它們 hello 與 hello 叢集相關聯的儲存體帳戶中儲存 toohello /HdiNotebooks 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="5c1bb-174">如需有關筆記本 hello 叢集上的儲存方式的詳細資訊，請參閱[Jupyter 筆記本儲存](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)？</span><span class="sxs-lookup"><span data-stu-id="5c1bb-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="5c1bb-175">在本機，hello 筆記本提供您可以連接 toodifferent Spark 叢集，根據您應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="5c1bb-176">您可以使用 GitHub tooimplement 原始檔控制系統，並且有 hello 筆記本的版本控制。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="5c1bb-177">您也可以共同作業環境，其中多個使用者可使用 hello 相同筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="5c1bb-178">您甚至不需要啟用叢集，即可在本機使用 Notebook。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="5c1bb-179">您只需要叢集 tootest 針對您筆記本，不 toomanually 管理您的筆記型電腦或開發環境。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="5c1bb-180">它可能會更容易 tooconfigure 本機開發環境比 tooconfigure hello Jupyter 安裝 hello 叢集上的。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="5c1bb-181">您可以利用本機安裝但未設定一或多個遠端叢集的所有 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="5c1bb-182">多個使用者可以使用 Jupyter 安裝在本機電腦上，執行 hello 相同筆記型電腦上相同的 Spark 叢集在 hello hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="5c1bb-183">在這種情況下，會建立多個 Livy 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="5c1bb-184">如果您遇到問題，而且想 toodebug，它將會是複雜的工作 tootrack 晚總工作階段所屬 toowhich 使用者。</span><span class="sxs-lookup"><span data-stu-id="5c1bb-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="5c1bb-185"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c1bb-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5c1bb-186">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="5c1bb-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5c1bb-187">案例</span><span class="sxs-lookup"><span data-stu-id="5c1bb-187">Scenarios</span></span>
* [<span data-ttu-id="5c1bb-188">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="5c1bb-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5c1bb-189">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="5c1bb-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5c1bb-190">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="5c1bb-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5c1bb-191">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="5c1bb-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="5c1bb-192">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="5c1bb-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5c1bb-193">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="5c1bb-193">Create and run applications</span></span>
* [<span data-ttu-id="5c1bb-194">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="5c1bb-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5c1bb-195">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="5c1bb-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5c1bb-196">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="5c1bb-196">Tools and extensions</span></span>
* [<span data-ttu-id="5c1bb-197">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="5c1bb-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5c1bb-198">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="5c1bb-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5c1bb-199">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="5c1bb-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5c1bb-200">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="5c1bb-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5c1bb-201">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="5c1bb-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="5c1bb-202">管理資源</span><span class="sxs-lookup"><span data-stu-id="5c1bb-202">Manage resources</span></span>
* [<span data-ttu-id="5c1bb-203">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="5c1bb-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5c1bb-204">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="5c1bb-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
