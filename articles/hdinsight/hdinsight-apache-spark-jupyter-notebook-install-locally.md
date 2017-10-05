---
title: "在本機安裝 Jupyter 並連線到 Azure HDInsight Spark 叢集 | Microsoft Docs"
description: "了解如何在電腦本機安裝 Jupyter Notebook，並連線到 Azure HDInsight 上的 Apache Spark 叢集。"
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="bbdda-103">在電腦上安裝 Jupyter Notebook，並連線到 HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="bbdda-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="bbdda-104">在這篇文章中，您會了解如何搭配含有 Spark magic 的自訂 PySpark (適用於 Python) 和 Spark (適用於 Scala) 核心來安裝 Jupyter 筆記本，然後將筆記本連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="bbdda-105">在您的本機電腦上安裝 Jupyter 可以有數種原因，而且也會面臨數種挑戰。</span><span class="sxs-lookup"><span data-stu-id="bbdda-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="bbdda-106">如需詳細資訊，請參閱本文章結尾的[為什麼我應該在我的電腦上安裝 Jupyter](#why-should-i-install-jupyter-on-my-computer) 一節。</span><span class="sxs-lookup"><span data-stu-id="bbdda-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="bbdda-107">在電腦上安裝 Jupyter 和 Spark magic 涉及三個主要步驟。</span><span class="sxs-lookup"><span data-stu-id="bbdda-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="bbdda-108">安裝 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="bbdda-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="bbdda-109">安裝含有 Spark magic 的 PySpark 和 Spark 核心</span><span class="sxs-lookup"><span data-stu-id="bbdda-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="bbdda-110">設定 Spark magic 以存取 HDInsight 上的 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="bbdda-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="bbdda-111">如需有關可供 HDInsight 叢集之相關 Jupyter Notebook 使用的自訂核心和 Spark magic 的詳細資訊，請參閱 [HDInsight 上的 Apache Spark Linux 叢集可供 Jupyter Notebook 使用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbdda-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="bbdda-112">Prerequisites</span></span>
<span data-ttu-id="bbdda-113">此處所列的必要條件不是針對安裝 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="bbdda-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="bbdda-114">這些是用來在安裝 Notebook 之後將 Jupyter Notebook 連接到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="bbdda-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbdda-115">An Azure subscription.</span></span> <span data-ttu-id="bbdda-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="bbdda-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="bbdda-118">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="bbdda-119">在電腦上安裝 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="bbdda-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="bbdda-120">您必須先安裝 Python，才能安裝 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="bbdda-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="bbdda-121">Python 和 Jupyter 皆為 [Anaconda 發行版本](https://www.continuum.io/downloads)的一部分。</span><span class="sxs-lookup"><span data-stu-id="bbdda-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="bbdda-122">當您安裝 Anaconda 時，會安裝某個 Python 發行版本。</span><span class="sxs-lookup"><span data-stu-id="bbdda-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="bbdda-123">安裝 Anaconda 之後，您便可以執行適當的命令來新增 Jupyter 安裝。</span><span class="sxs-lookup"><span data-stu-id="bbdda-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="bbdda-124">下載您平台適用的 [Anaconda 安裝程式](https://www.continuum.io/downloads) ，然後執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="bbdda-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="bbdda-125">執行安裝精靈時，請確定您選取將 Anaconda 新增至 PATH 變數的選項。</span><span class="sxs-lookup"><span data-stu-id="bbdda-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="bbdda-126">執行下列命令來安裝 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="bbdda-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="bbdda-127">如需有關安裝 Jupyter 的詳細資訊，請參閱[使用 Anaconda 來安裝 Jupyter](http://jupyter.readthedocs.io/en/latest/install.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="bbdda-128">安裝核心和 Spark magic</span><span class="sxs-lookup"><span data-stu-id="bbdda-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="bbdda-129">如需有關如何安裝 Spark magic、PySpark 和 Spark 核心的指示，請遵循 GitHub 上 [sparkmagic 文件](https://github.com/jupyter-incubator/sparkmagic#installation)中的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="bbdda-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="bbdda-130">Spark magic 文件中的第一個步驟會要求您安裝 Spark magic。</span><span class="sxs-lookup"><span data-stu-id="bbdda-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="bbdda-131">根據您將要連線的 HDInsight 叢集版本，將連結中的第一個步驟以下列命令取代。</span><span class="sxs-lookup"><span data-stu-id="bbdda-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="bbdda-132">之後，遵循 Spark magic 文件中的其餘步驟。</span><span class="sxs-lookup"><span data-stu-id="bbdda-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="bbdda-133">如果您想要安裝其他核心，則必須執行 Spark magic 安裝指示小節中的步驟 3。</span><span class="sxs-lookup"><span data-stu-id="bbdda-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="bbdda-134">若為叢集 3.4 版，請執行 `pip install sparkmagic==0.2.3` 來安裝 sparkmagic 0.2.3</span><span class="sxs-lookup"><span data-stu-id="bbdda-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="bbdda-135">若為叢集 3.5 版和 3.6 版，請執行 `pip install sparkmagic==0.11.2` 來安裝 sparkmagic 0.11.2</span><span class="sxs-lookup"><span data-stu-id="bbdda-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="bbdda-136">設定 Spark magic 以連線到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="bbdda-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="bbdda-137">在本節中，您會設定稍早安裝的 Spark magic，以連線到您必須已在 Azure HDInsight 中建立的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="bbdda-138">Jupyter 組態資訊通常儲存在使用者主目錄中。</span><span class="sxs-lookup"><span data-stu-id="bbdda-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="bbdda-139">若要在任何作業系統平台上找出您的主目錄，輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="bbdda-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="bbdda-140">啟動 Python 殼層。</span><span class="sxs-lookup"><span data-stu-id="bbdda-140">Start the Python shell.</span></span> <span data-ttu-id="bbdda-141">在命令視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="bbdda-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="bbdda-142">在 Python 殼層中，輸入下列命令來找出主目錄。</span><span class="sxs-lookup"><span data-stu-id="bbdda-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="bbdda-143">瀏覽至主目錄，然後建立一個叫做 **.sparkmagic** 的資料夾 (如果尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="bbdda-144">在該資料夾中，建立一個叫做 **config.json** 的檔案，然後在檔案中新增下列 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="bbdda-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="bbdda-145">以適當的值替代 **{USERNAME}**、**{CLUSTERDNSNAME}** 和 **{BASE64ENCODEDPASSWORD}**。</span><span class="sxs-lookup"><span data-stu-id="bbdda-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="bbdda-146">您可以在慣用的程式設計語言中或在線上，使用一些公用程式來產生 base64 編碼的密碼，以做為您的實際密碼。</span><span class="sxs-lookup"><span data-stu-id="bbdda-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="bbdda-147">在 `config.json` 中設定正確的活動訊號設定。</span><span class="sxs-lookup"><span data-stu-id="bbdda-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="bbdda-148">您應該依照加入稍早的 `kernel_python_credentials` 和 `kernel_scala_credentials` 程式碼片段，在相同層級新增這些設定。</span><span class="sxs-lookup"><span data-stu-id="bbdda-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="bbdda-149">如需有關加入活動訊號設定的方法與位置範例，請參閱此[範例 config.json (sample config.json)](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)。</span><span class="sxs-lookup"><span data-stu-id="bbdda-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="bbdda-150">若為 `sparkmagic 0.2.3` (叢集 3.4 版)，請加入︰</span><span class="sxs-lookup"><span data-stu-id="bbdda-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="bbdda-151">若為 `sparkmagic 0.11.2` (叢集 3.5 版和 3.6 版)，請加入︰</span><span class="sxs-lookup"><span data-stu-id="bbdda-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="bbdda-152">傳送活動訊號可確保不會流失工作階段。</span><span class="sxs-lookup"><span data-stu-id="bbdda-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="bbdda-153">當電腦進入睡眠或已關機時，則不會傳送活動訊號，導致工作階段被清除。</span><span class="sxs-lookup"><span data-stu-id="bbdda-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="bbdda-154">若為叢集 3.4 版，如果想要停用此行為，您可以從 Ambari UI 將 Livy 組態 `livy.server.interactive.heartbeat.timeout` 設定為 `0`。</span><span class="sxs-lookup"><span data-stu-id="bbdda-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="bbdda-155">若為叢集 3.5 版，如果您未設定上述的 3.5 組態，則不會刪除工作階段。</span><span class="sxs-lookup"><span data-stu-id="bbdda-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="bbdda-156">啟動 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="bbdda-156">Start Jupyter.</span></span> <span data-ttu-id="bbdda-157">從命令提示字元使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="bbdda-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="bbdda-158">確認您可以使用 Jupyter Notebook 來連接到叢集，並且可以使用核心隨附的 Spark magic。</span><span class="sxs-lookup"><span data-stu-id="bbdda-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="bbdda-159">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bbdda-159">Perform the following steps.</span></span>

    <span data-ttu-id="bbdda-160">a.</span><span class="sxs-lookup"><span data-stu-id="bbdda-160">a.</span></span> <span data-ttu-id="bbdda-161">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="bbdda-161">Create a new notebook.</span></span> <span data-ttu-id="bbdda-162">從右下角，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bbdda-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="bbdda-163">您應該會看到預設核心 **Python2**，以及您安裝的兩個新核心 **PySpark** 和 **Spark**。</span><span class="sxs-lookup"><span data-stu-id="bbdda-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="bbdda-164">按一下 [PySpark] 。</span><span class="sxs-lookup"><span data-stu-id="bbdda-164">Click **PySpark**.</span></span>

    <span data-ttu-id="bbdda-165">![Jupyter Notebook 中的核心](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter Notebook 中的核心")</span><span class="sxs-lookup"><span data-stu-id="bbdda-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="bbdda-166">b.</span><span class="sxs-lookup"><span data-stu-id="bbdda-166">b.</span></span> <span data-ttu-id="bbdda-167">執行下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="bbdda-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="bbdda-168">如果您可以順利擷取輸出，即表示已測試您對 HDInsight 叢集的連線。</span><span class="sxs-lookup"><span data-stu-id="bbdda-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="bbdda-169">如果您想要更新 Notebook 組態以連接到不同的叢集，請將 config.json 更新成一組新的值，如上述的步驟 3 所示。</span><span class="sxs-lookup"><span data-stu-id="bbdda-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="bbdda-170">為什麼我應該在我的電腦上安裝 Jupyter？</span><span class="sxs-lookup"><span data-stu-id="bbdda-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="bbdda-171">您想要在您的電腦上安裝 Jupyter，然後將其連接至 HDInsight 上的 Spark 叢集有數種原因。</span><span class="sxs-lookup"><span data-stu-id="bbdda-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="bbdda-172">雖然 Azure HDInsight 的 Spark 叢集上已經有 Jupyter Notebook 可用，但在電腦上安裝 Jupyter 可讓您選擇在本機建立 Notebook、針對正在執行的叢集測試您的應用程式，然後將 Notebook 上傳到叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="bbdda-173">若要將 Notebook 上傳到叢集，您可以使用在叢集上執行的 Jupyter Notebook 來上傳它們，或將它們儲存到與叢集關聯之儲存體帳戶的 [/HdiNotebooks] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="bbdda-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="bbdda-174">如需有關 Notebook 在叢集上的儲存方式詳細資訊，請參閱 [Jupyter Notebook 會儲存在哪裡](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)？</span><span class="sxs-lookup"><span data-stu-id="bbdda-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="bbdda-175">使用本機可用的 Notebook，您可以根據您的應用程式需求，連接至不同的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="bbdda-176">您可以使用 GitHub 實作來源控制系統，並且具有 Notebook 的版本控制。</span><span class="sxs-lookup"><span data-stu-id="bbdda-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="bbdda-177">您也可以有共同作業環境，其中多個使用者可以使用相同的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="bbdda-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="bbdda-178">您甚至不需要啟用叢集，即可在本機使用 Notebook。</span><span class="sxs-lookup"><span data-stu-id="bbdda-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="bbdda-179">您只需要叢集針對 Notebook 進行測試，不必以手動方式管理您的 Notebook 或開發環境。</span><span class="sxs-lookup"><span data-stu-id="bbdda-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="bbdda-180">設定自己的本機開發環境比設定叢集的 Jupyter 安裝更容易。</span><span class="sxs-lookup"><span data-stu-id="bbdda-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="bbdda-181">您可以利用您在本機安裝的所有軟體，而不需要設定一或多個遠端叢集。</span><span class="sxs-lookup"><span data-stu-id="bbdda-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="bbdda-182">將 Jupyter 安裝在本機電腦上，多個使用者可以同時在相同的 Spark 叢集上執行相同的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="bbdda-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="bbdda-183">在這種情況下，會建立多個 Livy 工作階段。</span><span class="sxs-lookup"><span data-stu-id="bbdda-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="bbdda-184">如果您遇到問題，而且想要偵錯，則追蹤哪個 Livy 工作階段屬於哪個使用者會是複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="bbdda-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="bbdda-185"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="bbdda-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="bbdda-186">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="bbdda-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="bbdda-187">案例</span><span class="sxs-lookup"><span data-stu-id="bbdda-187">Scenarios</span></span>
* [<span data-ttu-id="bbdda-188">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="bbdda-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="bbdda-189">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="bbdda-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="bbdda-190">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="bbdda-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="bbdda-191">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdda-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="bbdda-192">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="bbdda-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="bbdda-193">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdda-193">Create and run applications</span></span>
* [<span data-ttu-id="bbdda-194">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdda-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bbdda-195">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="bbdda-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="bbdda-196">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="bbdda-196">Tools and extensions</span></span>
* [<span data-ttu-id="bbdda-197">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdda-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="bbdda-198">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="bbdda-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bbdda-199">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="bbdda-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bbdda-200">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="bbdda-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bbdda-201">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="bbdda-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="bbdda-202">管理資源</span><span class="sxs-lookup"><span data-stu-id="bbdda-202">Manage resources</span></span>
* [<span data-ttu-id="bbdda-203">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="bbdda-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="bbdda-204">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="bbdda-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
