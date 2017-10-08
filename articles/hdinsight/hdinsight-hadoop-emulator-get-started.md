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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>開始使用 Hadoop 沙箱，它是虛擬機器上的模擬器

了解如何 tooinstall hello Hadoop 沙箱 Hortonworks 從虛擬機器 toolearn 有關 hello Hadoop 生態系統上。 hello 沙箱提供本機開發環境 toolearn Hadoop、 Hadoop 分散式檔案系統 (HDFS) 和提交作業相關。 熟悉 Hadoop 之後，您就可以開始在 Azure 中使用 Hadoop 建立 HDInsight 叢集。 如需有關如何啟動 tooget 的詳細資訊，請參閱[開始使用 Hadoop HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。

## <a name="prerequisites"></a>必要條件
* [Oracle VirtualBox](https://www.virtualbox.org/)。 請從[這裡](https://www.virtualbox.org/wiki/Downloads)下載並安裝。



## <a name="download-and-install-hello-virtual-machine"></a>下載並安裝 hello 虛擬機器
1. 瀏覽 toohello [Hortonworks 下載](http://hortonworks.com/downloads/#sandbox)。

2. 按一下**下載的 VIRTUALBOX** toodownload hello 最新 VM 上的 Hortonworks 沙箱。 Hello 下載開始之前，您就會是提示與 Hortonworks tooregister。 它會採用一個 tootwo 小時 toodownload 視網路速度而定。
   
    ![用於下載 VirtualBox 之 Hortonworks 沙箱的連結影像](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. 從 hello 相同網頁上，按一下 hello**虛擬方塊上的匯入**連結 toodownload PDF，其中包含 hello 虛擬機器的安裝指示。

toodownload 較舊的 HDP 版本沙箱，依序展開 hello 封存：

![Hortonworks 沙箱封存](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>啟動 hello 虛擬機器

1. 開啟 [Oracle VM VirtualBox]。
2. 從 hello**檔案**功能表上，按一下 **匯入應用裝置**，然後指定 hello Hortonworks 沙箱映像。
1. 按一下 選取 hello Hortonworks 沙箱**啟動**，然後**正常啟動**。 一旦 hello 虛擬機器完成 hello 開機程序，它會顯示登入的指示。
   
    ![正常啟動](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. 開啟網頁瀏覽器並瀏覽 toohello 顯示的 URL (通常 http://127.0.0.1:8888)。

## <a name="set-sandbox-passwords"></a>設定沙箱密碼

1. 從 hello**開始**hello Hortonworks 沙箱頁面上，選取步驟**檢視進階選項**。 使用 SSH toohello 沙箱中的這個頁面 toolog 上使用 hello 資訊。 使用提供 hello 名稱和密碼。
   
   > [!NOTE]
   > 如果您沒有安裝的 SSH 用戶端，您可以使用網頁型 SSH 在 hello 虛擬機器提供的 hello **http://localhost:4200 /**。
   > 
   
    hello 第一次您使用 SSH 的連接就提示的 toochange hello hello 根帳號的密碼。 輸入新密碼，這是您在使用 SSH 登入時使用的密碼。

2. 登入之後，請輸入下列命令的 hello:
   
        ambari-admin-password-reset
   
    出現提示時，提供 hello Ambari 系統管理員帳戶的密碼。 當您存取 hello Ambari Web UI，會使用這項目。

## <a name="use-hive-commands"></a>使用 Hive 命令

1. 從 SSH 連線 toohello 沙箱，使用下列命令 toostart hello Hive 殼層 hello:
   
        hive
2. Hello 殼層啟動之後，使用下列 tooview hello 資料表所提供的 hello 沙箱 hello:
   
        show tables;
3. 使用中的 hello 下列 tooretrieve 10 的資料列的 hello`sample_07`資料表：
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>後續步驟
* [深入了解如何以 hello Hortonworks 沙箱 toouse Visual Studio](hdinsight-hadoop-emulator-visual-studio.md)
* [學習 hello ropes 的 hello Hortonworks 沙箱](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop 教學課程 - 開始使用 HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

