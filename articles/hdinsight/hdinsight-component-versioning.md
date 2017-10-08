---
title: "aaaHadoop 元件和版本的 Azure HDInsight |Microsoft 文件"
description: "了解 hello Hadoop 元件與 HDInsight 和 hello 服務層級的 Hortonworks Data Platform 這個雲端發佈中可用的版本。"
keywords: "hadoop 版本，hadoop 生態系統元件，hadoop 元件如何 toocheck hadoop 版本"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Hello Hadoop 元件和適用於 HDInsight 版本為何？

深入了解 hello Apache Hadoop 生態系統元件和 Microsoft Azure HDInsight 中的版本，以及 hello Standard 和 Premium 服務層級。 此外，了解如何在 HDInsight toocheck Hadoop 元件版本。 

每個 HDInsight 版本都是 Hortonworks Data Platform (HDP) 版本的雲端發佈。

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>可以搭配不同 HDInsight 版本使用的 Hadoop 元件
Azure HDInsight 支援多個可隨時部署的 Hadoop 叢集版本。 特定版本的 hello HDP 發佈和一組包含在該發佈的元件，會建立每個版本的選擇。 自 2017 年 2 月 17 hello Azure HDInsight 所使用的預設叢集版本為 3.5，並且根據 HDP 2.5。

hello 下表列出 hello 與 HDInsight 叢集版本相關聯的元件版本。 

> [!NOTE]
> hello hello HDInsight 服務的預設版本可能會變更恕不另行通知。 如果您有版本相依性，指定 hello HDInsight 版本，當您以 hello.NET SDK 使用 Azure PowerShell 和 Azure CLI 建立叢集。

| 元件 | HDInsight 3.6 (預設值) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop 和 YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive 和 HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase (英文) |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (僅限 Linux) |1.6.2 + 2.0 (僅限 Linux) |1.6.0 (僅限 Linux) |1.5.2 (僅限 Linux 實驗性組建) |1.3.1 (僅限 Windows) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>檢查目前的 Hadoop 元件版本資訊

更新 tooHDInsight 可以變更與 HDInsight 叢集版本相關聯的 hello Hadoop 生態系統的元件版本。 toocheck hello Hadoop 元件和版本正用於叢集中，tooverify 使用 hello Ambari REST API。 hello **GetComponentInformation**命令會擷取服務元件的相關資訊。 如需詳細資訊，請參閱 hello [Ambari 文件][ambari-docs]。

Windows 叢集的另一個方式 toocheck hello 元件版本是 toolog tooa 叢集中使用遠端桌面，以及檢查 hello C:\apps\dist\ 目錄 hello 內容。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 版本 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 上的 Windows 停用項目](#hdinsight-windows-retirement)。

### <a name="release-notes"></a>版本資訊

請參閱[HDInsight 版本資訊](hdinsight-release-notes.md)hello 最新版 HDInsight 上的其他版本資訊。

## <a name="supported-hdinsight-versions"></a>支援的 HDInsight 辦本
hello 下表列出之 HDInsight hello Azure 入口網站目前可用的 hello 版本。 hello HDP 版本對應 tooeach HDInsight 版本會列出與 hello 產品發行日期。 也提供 hello 支援逾期與停用日期，這些已知時。

> [!NOTE]
> 支援後的版本已到期，它可能無法透過 hello Microsoft Azure 傳統入口網站。 不過，叢集版本繼續使用 hello toobe `Version` hello Windows PowerShell 中的參數[新增 AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx)命令和 hello hello 版本淘汰日期之前的.NET SDK。
> 
> 依預設，系統會為 HDInsight 2.1 和更新版本部署具有兩個前端節點的高可用性叢集。 它們不適用於 HDInsight 版本 1.6 叢集。

| HDInsight 版本 | HDP 版本 | VM OS | 高可用性 | 發行日期 | 在 hello Azure 入口網站上的可用性 | 支援到期日 | 停用日期 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |是 |2017 年 4 月 4 日 |是 | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |是 |2016 年 9 月 30 日 |是 |2017 年 9 月 5 日 |2018 年 5 月 31 日 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |是 |2016 年 3 月 29 日 |是 |2016 年 12 月 29 日 |2018 年 1 月 9 日 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |是 |2015 年 12 月 2 日 |是 |2016 年 6 月 27 日 |2018 年 7 月 31 日 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |是 |2015 年 12 月 2 日 |是 |2016 年 6 月 27 日 |2017 年 7 月 31 日 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS 或 Windows Server 2012 R2 |是 |2015 年 2 月 18 日 |否 |2016 年 3 月 1 日 |2017 年 4 月 1 日 |
| HDInsight 3.1 |HDP 2.1 |Windows Server 2012 R2 |是 |2014 年 6 月 24 日 |否 |2015 年 5 月 18 日 |2016 年 6 月 30 日 |
| HDInsight 3.0 |HDP 2.0 |Windows Server 2012 R2 |是 |2014 年 2 月 11 日 |否 |2014 年 9 月 17 日 |2015 年 6 月 30 日 |
| HDInsight 2.1 |HDP 1.3 |Windows Server 2012 R2 |是 |2013 年 10 月 28 日 |否 |2014 年 5 月 12 日 |2015 年 5 月 31 日 |
| HDInsight 1.6 |HDP 1.1 | |否 |2013 年 10 月 28 日 |否 |2014 年 4 月 26 日 |2015 年 5 月 31 日 |

## <a name="hdinsight-windows-retirement"></a>HDInsight Windows 停用項目
Microsoft Azure HDInsight 版本 3.3 已 hello 最後的 Windows 上的 HDInsight 版本。 hello 淘汰日期之前的 Windows 上的 HDInsight 是 2018 年 7 月 31。 如果您有 Windows 3.3 或更早版本的任何 HDInsight 叢集，您必須移轉 tooHDInsight Linux (HDInsight 版本 3.5 或更新版本) 上 2018 年 7 月 31 前。 移轉 toohello Linux 作業系統可讓您 tooretain hello 能力 toocreate 或調整您的 HDInsight 叢集。 對於 Windows 上 HDInsight 版本 3.3 的支援已在 2016 年 6 月 27 日到期。

從開始 HDInsight 版本 3.4，Microsoft 已發行 HDInsight 只能在 hello Linux 作業系統上。 如此一來，某些 HDInsight 中的 hello 元件僅提供適用於 Linux。 其中包含 Apache 廣、 Kafka、 互動式 Hive、 Spark，HDInsight 的應用程式，並為 hello 主要的檔案系統的 Azure 資料湖存放區。 只上 hello Linux 作業系統的 HDInsight 未來的版本可用。 未來不會在 Windows 上推出任何 HDInsight 版本。 

## <a name="faqs"></a>常見問題集

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>淘汰 HDInsight 上 Windows hello 時間表為何？
2018 年 7 月 31，為 hello 淘汰日期之前的 Windows 上的 HDInsight。 如果計劃的 hello 淘汰日期不是您的地區，系統會通知您分別。 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Hello 的 Windows 上的 HDInsight 淘汰的現有客戶的影響為何？
停用 Windows 上的 HDInsight 之後，您便無法建立新的 HDInsight Windows 叢集，或調整現有的 HDInsight Windows 叢集。 對於 HDInsight 版本 3.3 的支援已在 2016 年 6 月 27 日到期。 因此，不會對 HDInsight 3.3 或更早版本提供任何支援或錯誤修正。 只上 hello Linux 作業系統的 HDInsight 未來的版本可用。 未來不會在 Windows 上推出任何 HDInsight 版本。
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>哪些 Windows 上的 HDInsight 版本會受到影響？
Azure HDInsight 版本 3.3 是 HDInsight for Windows hello 最後一個版本。 在 Windows 上的 HDInsight 已停用之前，所有的 HDInsight Windows 叢集版本 3.3 或更早版本必須被移轉 tooHDInsight on Linux 版本 3.5 或更新版本。 移轉您在 Linux 上的叢集 tooHDInsight 可讓您 tooretain hello 能力 toocreate 新叢集，或調整現有的叢集。 

### <a name="what-do-i-need-toodo"></a>怎麼我需要 toodo？
2018 年 7 月 31 前移轉您的 HDInsight Windows 叢集 tooa 支援 HDInsight Linux 叢集。 進一步了解 hello [HDInsight 移轉文件](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)。 如需有關 Azure HDInsight 版本的詳細資訊，請參閱 hello 清單[支援的版本，](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions)。 

### <a name="where-do-i-find-hello-cluster-os-type"></a>哪裡可以找到 hello 叢集 OS 類型？
在 [hello Azure 入口網站，移 toohello HDInsight 叢集概觀] 頁面上，並找出**叢集類型**下**Essentials**。 hello 叢集 OS 類型會列在該頁面。 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>我無法移轉 2018 年 7 月 31，tooan HDInsight Linux 叢集。 什麼是 hello 影響 toomy HDInsight Windows 叢集？
hello HDInsight Windows 叢集會以執行的但是您無法建立新的 HDInsight Windows 叢集，或調整現有的 HDInsight Windows 叢集。 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>我的叢集具有 .NET 相依性。 如何在 Linux 上解析此相依性？
您可以使用 hello 來解決您的 Linux 叢集相依性[單聲道專案](http://www.mono-project.com/)。 這個 .NET 開放原始碼實作適用於 HDInsight Linux 叢集。 進一步了解 hello [HDInsight 移轉文件](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)。 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>我是 Windows 上 HDInsight 的新客戶。 該如何建立 HDInsight Windows 叢集？
從 2017 年 7 月 3 日開始，只有現有的 HDInsight Windows 客戶可以建立新的 HDInsight Windows 叢集。 新客戶無法在 hello Azure 入口網站中建立 HDInsight Windows 叢集使用 PowerShell 或 hello SDK。 我們建議新客戶建立 Linux HDInsight 叢集。 現有的客戶可以建立新的 HDInsight Windows 叢集 hello Windows 上的 HDInsight 淘汰日期之前。 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>是否有與 Linux 上的 Windows tooHDInsight 上移動從 HDInsight 相關聯的定價影響？
否，hello 定價是 hello 相同 HDInsight 其中一個作業系統上。 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>什麼是 hello 與相關聯的 hello 客戶優點移動 tooonly 使用 on Linux 的 HDInsight 嗎？
* 更快時間市場適用於透過 hello HDInsight 服務的開放原始碼巨量資料技術
* 支援大型社群和生態系統
* Hello 的能力 tooexercise 作用中開發 Hadoop 與其他巨量資料技術開啟原始碼社群

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>Linux 上的 HDInsight 是否提供 Windows 上的 HDInsight 中未提供的額外功能？
從開始 HDInsight 版本 3.4，Microsoft 已發行 HDInsight 只能在 hello Linux 作業系統上。 如此一來，某些 HDInsight 中的 hello 元件僅提供適用於 Linux。 其中包含 Apache 廣、 Kafka、 互動式 Hive、 Spark，HDInsight 的應用程式，並為 hello 主要的檔案系統的 Azure 資料湖存放區。 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>HDInsight 叢集版本的服務等級協定
hello 服務等級協定 (SLA) 定義的_支援視窗_。 hello 支援視窗是 hello 一段時間的 HDInsight 叢集版本是支援的 Microsoft 客戶服務及支援。 如果 hello 版本具有_支援到期日_，已通過，超出 hello 支援 視窗中的 hello HDInsight 叢集。 如需支援版本的詳細資訊，請參閱 hello 清單[支援 HDInsight 叢集版本](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux)。 指定 HDInsight 版本 X （在已有新版的 X + 1） 之後的 hello 支援到期日會計算為更新版本的 hello:  

* 公式 1： 加入 180 天 toohello 日期 X hello HDInsight 叢集版本發行時。
* 公式 2： 加入當 hello HDInsight 叢集版本 X + 1 可在 Azure 入口網站的 90 天 toohello 日期。

hello_淘汰日期_之後 hello 叢集版本無法建立 HDInsight 上的 hello 日期。 從 2017 年 7 月 31 日開始，您就無法在 HDInsight 叢集的停用日期之後調整叢集。 

> [!NOTE]
> 在 Azure 客體作業系統系列第 4 版使用 hello 64 位元版本的 Windows Server 2012 R2 上，執行 HDInsight Windows 叢集 （2.1、 3.0、 3.1、 3.2 和 3.3 包括版本）。 Azure 客體作業系統系列第 4 版支援 hello.NET framework 4.0、 4.5、 4.5.1 和 4.5.2。

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>與 HDInsight 版本相關聯的 Hortonworks 版本資訊

hello > 一節提供的 hello Hortonworks Data Platform 分佈和 Apache 元件所使用的 HDInsight 連結 toorelease 附註。
* HDInsight 叢集 3.6 版採用以 [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html) 為基礎的 Hadoop 散發套件。
* HDInsight 叢集 3.5 版採用以 [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html) 為基礎的 Hadoop 散發套件。 HDInsight 叢集版本 3.5 為 hello_預設_hello Azure 入口網站中建立的 Hadoop 叢集。
* HDInsight 叢集 3.4 版採用以 [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html)為基礎的 Hadoop 散發套件。
* HDInsight 叢集 3.3 版採用以 [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html)為基礎的 Hadoop 散發。

  * [Apache Storm 的版本資訊](https://storm.apache.org/2015/11/05/storm0100-released.html)可用 hello Apache 網站上。
  * [Apache hive 控制檔的版本資訊](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843)可用 hello Apache 網站上。
* HDInsight 叢集 3.2 版採用以 [Hortonworks Data Platform 2.2][hdp-2-2] 為基礎的 Hadoop 散發套件。

  * 特定 Apache 元件的可用版本資訊如下：[Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450)、[Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954)、[HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810)、[Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581)、[M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180)、[HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181)、[YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197)、[Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179)、[Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742)、[Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486)、[Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) 及 [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620)。
* HDInsight 叢集版本 3.1 使用以 [Hortonworks Data Platform 2.1.7][hdp-2-1-7] 為基礎的 Hadoop 散發套件。 在 2014 年 11 月 7 日之前建立的 HDInsight 3.1 叢集是以 [Hortonworks Data Platform 2.1.1][hdp-2-1-1] 為基礎。
* HDInsight 叢集 3.0 版採用以 [Hortonworks Data Platform 2.0][hdp-2-0-8] 為基礎的 Hadoop 散發套件。
* HDInsight 叢集 2.1 版採用以 [Hortonworks Data Platform 1.3][hdp-1-3-0] 為基礎的 Hadoop 散發套件。
* HDInsight 叢集 1.6 版採用以 [Hortonworks Data Platform 1.1][hdp-1-1-0] 為基礎的 Hadoop 散發套件。

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard 和 HDInsight Premium

Azure HDInsight 提供 hello 巨量資料雲端供應項目在兩個類別：_標準_和_Premium_。 hello 下表列出可用的功能_只_HDInsight premium。 使用 HDInsight Standard 和 Premium 中未明確地描述 hello 資料表中的功能。

> [!NOTE]
> hello HDInsight Premium 供應項目是目前在預覽中，而僅適用於 Linux 叢集。

| HDInsight Premium 功能 | 說明 |
| --- | --- |
| 已加入網域的 HDInsight 叢集 |加入 HDInsight 叢集 tooAzure 企業層級安全性的 Active Directory (Azure AD) 網域。 在 HDInsight Premium，您可以從您可以透過 Azure AD toolog tooan HDInsight 叢集上進行驗證的企業設定員工清單。 hello 企業系統管理員可以使用設定的登錄區安全性角色型存取控制[Apache Ranger](http://hortonworks.com/apache/ranger/)以及限制資料存取 toouse 程度就如同所需。 最後，hello 系統管理員可以稽核員工存取的資料，並變更 tooaccess 控制原則，藉此達到較高程度的控管其公司資源。 如需詳細資訊，請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。 |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>HDInsight Premium 中支援的叢集類型
hello 下表列出支援 HDInsight Premium 中的 hello 叢集類型。

| 叢集類型 | 標準 | 高階 (預覽) |
| --- | --- | --- |
| Hadoop |是 |是 (僅限 HDInsight 3.6) |
| Spark |是 |否 |
| HBase |是 |否 |
| Storm |是 |否 |
| R 伺服器 |是 |否 |
| 互動式 Hive (預覽) |是 |否 |
| Kafka (預覽) |是 |否 | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>HDInsight Premium 中對於 Azure Data Lake Store 的支援

HDInsight Premium 叢集不支援使用 Azure Data Lake Store 當做主要儲存體。 但是，您可以使用 Azure Data Lake Store 作為含有 HDInsight Premium 叢集的附加元件儲存體。

### <a name="pricing-and-sla"></a>價格和 SLA
如需 HDInsight Premium 的價格和 SLA 的詳細資訊，請參閱 [HDInsight 價格](https://azure.microsoft.com/pricing/details/hdinsight/)。

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>適用於叢集的預設節點設定和虛擬機器大小
下列資料表列出 hello 預設虛擬機器 (VM) 大小的 HDInsight 叢集的 hello。

> [!IMPORTANT]
> 如果您的叢集需要 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。
> 
> 

* 所有支援的區域，巴西南部和日本西部除外︰

  | 叢集類型 | Hadoop | HBase | Storm | Spark | R 伺服器 |
  | --- | --- | --- | --- | --- | --- |
  | 前端：預設 VM 大小 |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | 前端：建議的 VM 大小 |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |A3、A4、A5 |D12 v2、D13 v2、D14 v2 |D12 v2、D13 v2、D14 v2 |
  | 背景工作：預設 VM 大小 |D3 v2 |D3 v2 |D3 v2 |Windows：D12 v2；Linux：D4 v2 |Windows：D12 v2；Linux：D4 v2 |
  | 背景工作：建議的 VM 大小 |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |D3 v2、D4 v2、D12 v2 |Windows：D12 v2、D13 v2、D14 v2；Linux：D4 v2、D12 v2、D13 v2、D14 v2 |Windows：D12 v2、D13 v2、D14 v2；Linux：D4 v2、D12 v2、D13 v2、D14 v2 |
  | ZooKeeper：預設 VM 大小 | |A3 |A2 | | |
  | ZooKeeper：建議的 VM 大小 | |A3、A4、A5 |A2、A3、A4 | | |
  | 邊緣：預設 VM 大小 | | | | |Windows：D12 v2；Linux：D4 v2 |
  | 邊緣：建議的 VM 大小 | | | | |Windows：D12 v2、D13 v2、D14 v2；Linux：D4 v2、D12 v2、D13 v2、D14 v2 |
* 僅限巴西南部和日本西部 (沒有 v2 大小)：

  | 叢集類型 | Hadoop | HBase | Storm | Spark | R 伺服器 |
  | --- | --- | --- | --- | --- | --- |
  | 前端：預設 VM 大小 |D3 |D3 |A3 |D12 |D12 |
  | 前端：建議的 VM 大小 |D3、D4、D12 |D3、D4、D12 |A3、A4、A5 |D12、D13、D14 |D12、D13、D14 |
  | 背景工作：預設 VM 大小 |D3 |D3 |D3 |Windows：D12；Linux：D4 |Windows：D12；Linux：D4 |
  | 背景工作：建議的 VM 大小 |D3、D4、D12 |D3、D4、D12 |D3、D4、D12 |Windows：D12、D13、D14；Linux：D4、D12、D13、D14 |Windows：D12、D13、D14；Linux：D4、D12、D13、D14 |
  | ZooKeeper：預設 VM 大小 | |A2 |A2 | | |
  | ZooKeeper：建議的 VM 大小 | |A2、A3、A4 |A2、A3、A4 | | |
  | 邊緣：預設 VM 大小 | | | | |Windows：D12；Linux：D4 |
  | 邊緣：建議的 VM 大小 | | | | |Windows：D12、D13、D14；Linux：D4、D12、D13、D14 |

> [!NOTE]
> - Head 稱為*Nimbus* hello Storm 叢集類型。
> - 背景工作稱為*監督員*hello Storm 叢集類型。
> - 背景工作稱為*區域*hello HBase 叢集類型。

## <a name="next-steps"></a>後續步驟
- [針對 Hadoop、Spark 等在 HDInsight 中設定叢集](hdinsight-hadoop-provision-linux-clusters.md)
- [從 Windows PC 在 HDInsight 上的 Hadoop 中作業](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
