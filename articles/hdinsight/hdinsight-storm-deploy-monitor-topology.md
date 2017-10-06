---
title: "aaaDeploy 和管理 HDInsight 上的 Apache Storm 拓撲 |Microsoft 文件"
description: "了解 toodeploy、 監視和管理 HDInsight 上使用 hello Storm 儀表板的 Apache Storm 拓撲的方式。 使用適用於 Visual Studio 的 Hadoop 工具。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>部署和管理以 Windows 為基礎的 HDInsight 上的 Apache Storm 拓撲

hello Storm 儀表板可讓您 tooeasily 部署和執行 Apache Storm 拓撲 tooyour HDInsight 叢集使用網頁瀏覽器。 您也可以使用 hello 儀表板 toomonitor，並管理正在執行的拓撲。 如果您使用 Visual Studio，hello HDInsight Tools for Visual Studio 會提供類似的功能，Visual Studio 中。

hello Storm 儀表板和 hello HDInsight Tools 中的 hello Storm 功能上依賴 hello Storm REST API，可以使用的 toocreate 專屬監視和管理的解決方案。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Windows 做為 hello 作業系統的 HDInsight 叢集上出現。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> 如需透過使用 Linux 的 HDInsight 叢集來部署和管理 Storm 拓撲的詳細資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>必要條件

* **Apache Storm on HDInsight** - 請參閱[開始使用 Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md)，以取得建立叢集的步驟。

* Hello **Storm 儀表板**： 支援 HTML5 的現代網頁瀏覽器。

* 如**Visual Studio** -Azure SDK 2.5.1 或更新版本和 hello HDInsight Tools for Visual Studio。 請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall 和設定 hello HDInsight tools for Visual Studio。

    下列版本的 Visual Studio 中的 hello 其中一項：

  * Visual Studio 2012 (含 Update 4)

  * Visual Studio 2013 (含 Update 4) 或 Visual Studio 2013 Community

  * Visual Studio 2015 (任何版本)

  * Visual Studio 2017 (任何版本)

## <a name="storm-dashboard"></a>Storm Dashboard

hello Storm 儀表板是在 Storm 叢集上使用的網頁。 hello URL 是**https://&lt;clustername >.azurehdinsight.net/**，其中**clustername**是您在 HDInsight 叢集的 Storm hello 名稱。

從 hello hello Storm 儀表板頂端，選取**提交拓撲**。 遵循上 hello 頁面 toorun 拓樸範例 hello 指示或 tooupload 然後執行您所建立的拓撲。

![hello 提交拓樸 頁面][storm-dashboard-submit]

### <a name="storm-ui"></a>Storm UI

從 hello Storm 儀表板，選取 hello **Storm UI**連結。 這在加法 tooany 執行拓樸中顯示 hello 叢集的相關資訊。

![hello storm ui][storm-dashboard-ui]

> [!NOTE]
> 使用 Internet Explorer 的某些版本中，您可能會發現 Storm UI 不會重新整理之後，您必須先瀏覽該 hello。 例如，它可能不會顯示 hello 新拓撲您上傳，或您先前停用時，它可能會顯示為作用中的拓撲。 Microsoft 知道這個問題，並正在找出解決方案。

#### <a name="main-page"></a>主頁面

hello Storm UI hello 主頁面上提供下列資訊的 hello:

* **叢集摘要**: hello Storm 叢集的基本資訊。

* **拓撲摘要**：執行中拓撲的清單。 使用有關特定拓撲中這個區段 tooview hello 連結的詳細資訊。

* **摘要的監督員**: hello Storm 監督者的相關資訊。

* **Nimbus 組態**: Nimbus hello 叢集組態。

#### <a name="topology-summary"></a>拓撲摘要

選取連結從 hello**拓撲摘要**區段會顯示 hello 下列 hello 拓撲的相關資訊：

* **摘要的拓樸**: hello 拓撲的相關基本資訊。

* **拓樸動作**: hello 拓撲，您可以執行管理動作。

  * **啟用**：繼續處理已停用的拓撲。

  * **停用**：暫停執行中的拓撲。

  * **重新平衡**： 調整 hello 拓樸的 hello 平行處理原則。 之後您已經變更 hello hello 叢集中的節點數目，您應該重新平衡執行的拓撲。 這可讓 hello 拓撲 tooadjust 平行處理原則 toocompensate hello 增加或減少 hello 叢集中的節點數目。

      如需詳細資訊，請參閱[了解 hello 平行處理原則的 Storm 拓撲 (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)。

  * **Kill**: hello 指定逾時之後終止 Storm 拓撲。

* **拓樸 stats**: hello 拓撲的相關統計資料。 使用中 hello hello 連結**視窗**hello 剩餘項目在 hello 頁面上的資料行 tooset hello 時間範圍。

* **Spouts**: hello spouts hello 拓撲所使用。 使用此區段 tooview 中的 hello 連結特定 spouts 的詳細資訊。

* **釘**: hello hello 拓撲所使用的攻擊。 使用此區段 tooview 中的 hello 連結特定攻擊的詳細資訊。

* **拓撲組態**: hello 選取拓撲的 hello 設定。

#### <a name="spout-and-bolt-summary"></a>Spout 和 Bolt 摘要

選取從 hello spout **Spouts**或**釘**區段會顯示 hello 遵循 hello 選取項目的資訊：

* **元件摘要**: hello spout 或閃電的基本資訊。

* **Spout 閃電 stats**: hello 相關統計資料 spout 或閃電。 使用中 hello hello 連結**視窗**hello 剩餘項目在 hello 頁面上的資料行 tooset hello 時間範圍。

* **輸入 stats** （只有閃電）： hello 的相關資訊輸入 hello 閃電所耗用的資料流。

* **輸出 stats**: spout 或閃電關於發出由此 hello 資料流的資訊。

* **執行程式**: hello spout 或閃電 hello 執行個體的相關資訊。 選取 hello**連接埠**這個執行個體所產生的項目特定的執行程式 tooview 診斷資訊的記錄檔。

* **錯誤**：此 Spout 或 Bolt 的任何錯誤資訊。

## <a name="hdinsight-tools-for-visual-studio"></a>HDInsight Tools for Visual Studio

hello HDInsight 工具可以使用的 toosubmit C# 或混合式拓撲 tooyour Storm 叢集。 下列步驟的 hello 使用範例應用程式。 如需使用 hello HDInsight Tools 來建立您自己的拓撲資訊，請參閱[開發 C# 拓撲使用 hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

使用下列步驟 toodeploy 範例 tooyour Storm HDInsight 叢集上的 hello 然後檢視和管理 hello 拓撲。

1. 如果您有尚未安裝 hello 最新版 hello HDInsight Tools for Visual Studio，請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

2. 開啟 Visual Studio，選取 [檔案]  >  [新增]  >  [專案]。

3. 在 hello**新專案**對話方塊方塊中，展開 **已安裝** > **範本**，然後選取**HDInsight**。 從範本 hello 清單，選取**Storm 範例**。 在 hello hello 對話方塊下方，輸入 hello 應用程式的名稱。

    ![image](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**提交 HDInsight 上的 tooStorm**。

   > [!NOTE]
   > 如果出現提示，請輸入您的 Azure 訂閱 hello 登入認證。 如果您有多個訂用帳戶，登入另一個則包含您在 HDInsight 叢集的 Storm toohello。

5. 選取您在 HDInsight 叢集的 Storm 從 hello **Storm 叢集**下拉式清單，然後選取**送出**。 您可以監視是否 hello 提交成功使用 hello**輸出**視窗。

6. 已成功送出 hello 拓樸，當 hello **Storm 拓撲**hello 叢集應該會出現。 從 hello 列出 tooview hello 執行拓撲的相關資訊，請選取 hello 拓撲。

    ![Visual Studio 監視器](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > 您也可以透過展開 [Azure]  >  [HDInsight]，並在 Storm on HDInsight 叢集上按一下滑鼠右鍵，然後選取 [檢視 Storm 拓撲] 以從**伺服器總管**中檢視 [Storm 拓撲]。

    Hello spouts 或釘 tooview 這些元件的資訊，請選取 hello 圖形。 隨即會針對每個選取的項目開啟新的視窗。

   > [!NOTE]
   > hello hello 拓撲檔案名 hello 拓樸的 hello 類別名稱 (在此情況下， `HelloWord`，) 附加時間戳記。

7. 從 hello**拓撲摘要**檢視中，選取**Kill** toostop hello 拓撲。

   > [!NOTE]
   > Storm 拓撲會繼續執行，直到已停止或刪除 hello 叢集。


## <a name="rest-api"></a>REST API

hello REST API，乃是建立 hello Storm UI，讓您可以執行類似的管理和監視功能，可使用 hello REST API。 您可以使用 hello REST API toocreate 自訂工具來管理和監視 Storm 拓撲。

如需詳細資訊，請參閱 [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md)。 hello 下列資訊為特定 toousing hello 與 HDInsight 上的 Apache Storm 的 REST API。

### <a name="base-uri"></a>基底 URI

hello hello REST API 在 HDInsight 叢集上的基底 URI 是**https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**，其中**clustername**位於您 Storm hello 名稱HDInsight 叢集。

### <a name="authentication"></a>驗證

必須使用 REST API 的要求 toohello**基本驗證**，所以您可以使用 hello HDInsight 叢集系統管理員名稱和密碼。

> [!NOTE]
> 因為基本驗證會使用純文字傳送，您應該**一律**hello 叢集中使用 HTTPS toosecure 通訊。

### <a name="return-values"></a>傳回值

只能從 hello 叢集內可使用 REST API 或虛擬機器上 hello 與 hello 叢集相同 Azure 虛擬網路從 hello 傳回的資訊。 例如，傳回的動物園管理員伺服器 hello 完整的網域名稱 (FQDN) 是無法從 hello 網際網路存取。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何使用 toodeploy 和監視器的拓樸 hello Storm 儀表板，了解如何：

* [開發使用 hello HDInsight Tools for Visual Studio C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [使用 Maven 開發 Java 型拓撲](hdinsight-storm-develop-java-topology.md)

若需更多範例拓撲的清單，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
