---
title: "使用 Hadoop 沙箱-模擬器-Azure HDInsight aaaLearn |Microsoft 文件"
description: "深入了解使用 toostart hello Hadoop 生態系統，您可以設定 Hadoop 沙箱 Hortonworks 從 Azure 的虛擬機器上。 "
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
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="1aa1a-104">開始使用 Hadoop 沙箱，它是虛擬機器上的模擬器</span><span class="sxs-lookup"><span data-stu-id="1aa1a-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="1aa1a-105">了解如何 tooinstall hello Hadoop 沙箱 Hortonworks 從虛擬機器 toolearn 有關 hello Hadoop 生態系統上。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="1aa1a-106">hello 沙箱提供本機開發環境 toolearn Hadoop、 Hadoop 分散式檔案系統 (HDFS) 和提交作業相關。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="1aa1a-107">熟悉 Hadoop 之後，您就可以開始在 Azure 中使用 Hadoop 建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="1aa1a-108">如需有關如何啟動 tooget 的詳細資訊，請參閱[開始使用 Hadoop HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aa1a-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1aa1a-109">Prerequisites</span></span>
* <span data-ttu-id="1aa1a-110">[Oracle VirtualBox](https://www.virtualbox.org/)。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="1aa1a-111">請從[這裡](https://www.virtualbox.org/wiki/Downloads)下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="1aa1a-112">下載並安裝 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1aa1a-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="1aa1a-113">瀏覽 toohello [Hortonworks 下載](http://hortonworks.com/downloads/#sandbox)。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="1aa1a-114">按一下**下載的 VIRTUALBOX** toodownload hello 最新 VM 上的 Hortonworks 沙箱。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="1aa1a-115">Hello 下載開始之前，您就會是提示與 Hortonworks tooregister。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="1aa1a-116">它會採用一個 tootwo 小時 toodownload 視網路速度而定。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![用於下載 VirtualBox 之 Hortonworks 沙箱的連結影像](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="1aa1a-118">從 hello 相同網頁上，按一下 hello**虛擬方塊上的匯入**連結 toodownload PDF，其中包含 hello 虛擬機器的安裝指示。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="1aa1a-119">toodownload 較舊的 HDP 版本沙箱，依序展開 hello 封存：</span><span class="sxs-lookup"><span data-stu-id="1aa1a-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Hortonworks 沙箱封存](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="1aa1a-121">啟動 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1aa1a-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="1aa1a-122">開啟 [Oracle VM VirtualBox]。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="1aa1a-123">從 hello**檔案**功能表上，按一下 **匯入應用裝置**，然後指定 hello Hortonworks 沙箱映像。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="1aa1a-124">按一下 選取 hello Hortonworks 沙箱**啟動**，然後**正常啟動**。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="1aa1a-125">一旦 hello 虛擬機器完成 hello 開機程序，它會顯示登入的指示。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![正常啟動](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="1aa1a-127">開啟網頁瀏覽器並瀏覽 toohello 顯示的 URL (通常 http://127.0.0.1:8888)。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="1aa1a-128">設定沙箱密碼</span><span class="sxs-lookup"><span data-stu-id="1aa1a-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="1aa1a-129">從 hello**開始**hello Hortonworks 沙箱頁面上，選取步驟**檢視進階選項**。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="1aa1a-130">使用 SSH toohello 沙箱中的這個頁面 toolog 上使用 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="1aa1a-131">使用提供 hello 名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1aa1a-132">如果您沒有安裝的 SSH 用戶端，您可以使用網頁型 SSH 在 hello 虛擬機器提供的 hello **http://localhost:4200 /**。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="1aa1a-133">hello 第一次您使用 SSH 的連接就提示的 toochange hello hello 根帳號的密碼。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="1aa1a-134">輸入新密碼，這是您在使用 SSH 登入時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="1aa1a-135">登入之後，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="1aa1a-136">出現提示時，提供 hello Ambari 系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="1aa1a-137">當您存取 hello Ambari Web UI，會使用這項目。</span><span class="sxs-lookup"><span data-stu-id="1aa1a-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="1aa1a-138">使用 Hive 命令</span><span class="sxs-lookup"><span data-stu-id="1aa1a-138">Use Hive commands</span></span>

1. <span data-ttu-id="1aa1a-139">從 SSH 連線 toohello 沙箱，使用下列命令 toostart hello Hive 殼層 hello:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="1aa1a-140">Hello 殼層啟動之後，使用下列 tooview hello 資料表所提供的 hello 沙箱 hello:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="1aa1a-141">使用中的 hello 下列 tooretrieve 10 的資料列的 hello`sample_07`資料表：</span><span class="sxs-lookup"><span data-stu-id="1aa1a-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="1aa1a-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1aa1a-142">Next steps</span></span>
* [<span data-ttu-id="1aa1a-143">深入了解如何以 hello Hortonworks 沙箱 toouse Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1aa1a-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="1aa1a-144">學習 hello ropes 的 hello Hortonworks 沙箱</span><span class="sxs-lookup"><span data-stu-id="1aa1a-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="1aa1a-145">Hadoop 教學課程 - 開始使用 HDP</span><span class="sxs-lookup"><span data-stu-id="1aa1a-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

