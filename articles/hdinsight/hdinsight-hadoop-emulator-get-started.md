---
title: "了解使用 Hadoop 沙箱 - 模擬器 - Azure HDInsight | Microsoft Docs"
description: "若要開始了解 Hadoop 生態系統，您可以在 Azure 虛擬機器上從 Hortonworks 設定 Hadoop 沙箱。 "
keywords: "hadoop 模擬器, hadoop 沙箱"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="7ad68-104">開始使用 Hadoop 沙箱，它是虛擬機器上的模擬器</span><span class="sxs-lookup"><span data-stu-id="7ad68-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="7ad68-105">了解如何在虛擬機器上從 Hortonworks 安裝 Hadoop 沙箱，以了解 Hadoop 生態系統。</span><span class="sxs-lookup"><span data-stu-id="7ad68-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="7ad68-106">沙箱提供本機開發環境，讓您了解 Hadoop、Hadoop 分散式檔案系統 (HDFS)，以及作業提交。</span><span class="sxs-lookup"><span data-stu-id="7ad68-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="7ad68-107">熟悉 Hadoop 之後，您就可以開始在 Azure 中使用 Hadoop 建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ad68-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="7ad68-108">有關如何開始使用的詳細資訊，請參閱 [開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7ad68-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ad68-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ad68-109">Prerequisites</span></span>
* <span data-ttu-id="7ad68-110">[Oracle VirtualBox](https://www.virtualbox.org/)。</span><span class="sxs-lookup"><span data-stu-id="7ad68-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="7ad68-111">請從[這裡](https://www.virtualbox.org/wiki/Downloads)下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="7ad68-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="7ad68-112">下載並安裝虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ad68-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="7ad68-113">瀏覽至 [Hortonworks 下載](http://hortonworks.com/downloads/#sandbox)。</span><span class="sxs-lookup"><span data-stu-id="7ad68-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="7ad68-114">按一下 [DOWNLOAD FOR VIRTUALBOX]\(適用於 VIRTUALBOX 的下載項目\)，以下載最新的 VM 上「Hortonworks 沙箱」。</span><span class="sxs-lookup"><span data-stu-id="7ad68-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="7ad68-115">系統會提示您向 Hortonworks 註冊，然後才能開始下載。</span><span class="sxs-lookup"><span data-stu-id="7ad68-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="7ad68-116">下載需要一到兩個小時的時間，視您的網路速度而定。</span><span class="sxs-lookup"><span data-stu-id="7ad68-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![用於下載 VirtualBox 之 Hortonworks 沙箱的連結影像](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="7ad68-118">從相同網頁中，按一下 [Import on Virtual Box] \(在 Virtual Box 上匯入) 連結，以下載包含虛擬機器安裝指示的 PDF。</span><span class="sxs-lookup"><span data-stu-id="7ad68-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="7ad68-119">若要下載舊版 HDP 沙箱，請展開封存：</span><span class="sxs-lookup"><span data-stu-id="7ad68-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Hortonworks 沙箱封存](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="7ad68-121">啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ad68-121">Start the virtual machine</span></span>

1. <span data-ttu-id="7ad68-122">開啟 [Oracle VM VirtualBox]。</span><span class="sxs-lookup"><span data-stu-id="7ad68-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="7ad68-123">從 [檔案] 功能表中，按一下 [匯入設備]，然後指定「Hortonworks 沙箱」映像。</span><span class="sxs-lookup"><span data-stu-id="7ad68-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="7ad68-124">選取「Hortonworks 沙箱」、按一下 [啟動]，然後選取 [正常啟動]。</span><span class="sxs-lookup"><span data-stu-id="7ad68-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="7ad68-125">虛擬機器完成開機程序後會顯示登入指示。</span><span class="sxs-lookup"><span data-stu-id="7ad68-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![正常啟動](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="7ad68-127">開啟網頁瀏覽器，並瀏覽至顯示的 URL (通常是 http://127.0.0.1:8888 )。</span><span class="sxs-lookup"><span data-stu-id="7ad68-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="7ad68-128">設定沙箱密碼</span><span class="sxs-lookup"><span data-stu-id="7ad68-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="7ad68-129">從 [Hortonworks 沙箱] 頁面的 [入門] 步驟選取 [檢視進階選項]。</span><span class="sxs-lookup"><span data-stu-id="7ad68-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="7ad68-130">在此頁面上使用該資訊，以透過 SSH 登入沙箱。</span><span class="sxs-lookup"><span data-stu-id="7ad68-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="7ad68-131">使用提供的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7ad68-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7ad68-132">如果您未安裝 SSH 用戶端，您可以使用虛擬機器在 **http://localhost:4200/** 所提供的網頁型 SSH。</span><span class="sxs-lookup"><span data-stu-id="7ad68-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="7ad68-133">第一次使用 SSH 連線時，系統會提示您變更根帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7ad68-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="7ad68-134">輸入新密碼，這是您在使用 SSH 登入時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="7ad68-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="7ad68-135">登入之後，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7ad68-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="7ad68-136">出現提示時，提供 Ambari 系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7ad68-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="7ad68-137">當您存取 Ambari Web UI 時將會用到。</span><span class="sxs-lookup"><span data-stu-id="7ad68-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="7ad68-138">使用 Hive 命令</span><span class="sxs-lookup"><span data-stu-id="7ad68-138">Use Hive commands</span></span>

1. <span data-ttu-id="7ad68-139">在連往沙箱的 SSH 連線中，使用下列命令啟動 Hive 殼層：</span><span class="sxs-lookup"><span data-stu-id="7ad68-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="7ad68-140">殼層啟動之後，使用下列命令檢視沙箱所提供的資料表︰</span><span class="sxs-lookup"><span data-stu-id="7ad68-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="7ad68-141">使用下列命令從 `sample_07` 資料表擷取 10 個資料列︰</span><span class="sxs-lookup"><span data-stu-id="7ad68-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="7ad68-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ad68-142">Next steps</span></span>
* [<span data-ttu-id="7ad68-143">了解如何搭配使用 Visual Studio 與 Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="7ad68-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="7ad68-144">了解 Hortonworks 沙箱的訣竅</span><span class="sxs-lookup"><span data-stu-id="7ad68-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="7ad68-145">Hadoop 教學課程 - 開始使用 HDP</span><span class="sxs-lookup"><span data-stu-id="7ad68-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

