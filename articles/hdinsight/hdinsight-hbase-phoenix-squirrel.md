---
title: "aaaUse Apache in Phoenix 和與 windows Azure HDInsight 松鼠 |Microsoft 文件"
description: "深入了解如何 toouse HDInsight 中的 Apache in Phoenix 以及 tooinstall 及設定松鼠 HDInsight 中您工作站 tooconnect tooan HBase 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>在 HDInsight 中搭配 Windows 型 HBase 叢集使用 Apache Phoenix 和 SQuirreL
深入了解如何 toouse [Apache in Phoenix](http://phoenix.apache.org/)在 HDInsight，以及如何 tooinstall 及設定松鼠 HDInsight 中您工作站 tooconnect tooan HBase 叢集。 如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。 Hello in Phoenix 文法，請參閱[in Phoenix 文法](http://phoenix.apache.org/language/index.html)。

> [!NOTE]
> Hello in Phoenix HDInsight 中的版本資訊，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)。
>

> [!IMPORTANT]
> hello 這個文件的唯一工作 Windows 為基礎的 HDInsight 叢集的步驟。 Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需在 Linux 型 HDInsight 上使用 Phoenix 的相關資訊，請參閱[在 HDinsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md)。
>



## <a name="use-sqlline"></a>使用 SQLLine
[SQLLine](http://sqlline.sourceforge.net/)是命令列公用程式 tooexecute SQL。

### <a name="prerequisites"></a>必要條件
您可以使用 SQLLine 之前，您必須擁有 hello 下列：

* **HDInsight 中的 HBase 叢集**。 如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。
* **透過 hello 遠端桌面通訊協定 toohello HBase 叢集連線**。 如需指示，請參閱[使用 hello Azure 傳統入口網站來管理 Hadoop 叢集 HDInsight 中][hdinsight-manage-portal]。

**toofind 出 hello 主機名稱**

1. 開啟**Hadoop 命令列**從 hello 桌面。
2. 執行下列命令 tooget hello DNS 尾碼的 hello:

        ipconfig

    並記下 **連線專用 DNS 尾碼**。 例如， *myhbasecluster.f5.internal.cloudapp.net*。 當您連接 tooan HBase 叢集時，您需要 tooconnect tooone 的 hello 動物園管理員使用的 FQDN。 每個 HDInsight 叢集有 3 個 Zookeeper。 它們是 *zookeeper0*、*zookeeper1* 和 *zookeeper2*。 hello FQDN 會像*zookeeper2.myhbasecluster.f5.internal.cloudapp.net*。

**toouse SQLLine**

1. 開啟**Hadoop 命令列**從 hello 桌面。
2. 執行下列命令 tooopen SQLLine hello:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    hello hello 範例中所使用的命令：

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。

## <a name="use-squirrel"></a>使用 SQuirreL
[SQL 用戶端松鼠](http://squirrel-sql.sourceforge.net/)是圖形化的 Java 程式，將允許您 tooview hello JDBC 相容的資料庫結構，瀏覽 hello 資料表中的資料，發出 SQL 命令等。它可以是使用的 tooconnect tooApache in Phoenix HDInsight 上。

這個區段會顯示如何 tooinstall 和松鼠叢集上設定您的工作站 tooconnect tooan HBase HDInsight 中透過 VPN。

### <a name="prerequisites"></a>必要條件
Hello 程序之前，您必須擁有 hello 下列：

* HBase 叢集部署 tooan 與 DNS 虛擬機器的 Azure 虛擬網路。  如需相關指示，請參閱[在 Azure 虛擬網路上建立 HBase 叢集][hdinsight-hbase-provision-vnet]。

* 收到 hello HBase 叢集的叢集連線特定 DNS 尾碼。 tooget 它 RDP 到 hello 叢集中，然後執行 IPConfig。  hello DNS 尾碼是類似於：

        myhbase.b7.internal.cloudapp.net
* 在您的工作站上下載並安裝 [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) 。 您必須從 hello 封裝 toocreate makecert 您的憑證。  
* 在您的工作站上下載並安裝 [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 。  SQuirreL SQL 用戶端 3.0 版和更新版本需要 JRE 1.6 版或更新版本。  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>設定點對站 VPN 連線 toohello Azure 虛擬網路
設定點對站 VPN 連線包含 3 個步驟：

1. [設定虛擬網路和動態路由閘道](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [建立您的憑證](#Create-your-certificates)
3. [設定 VPN 用戶端](#Configure-your-VPN-client)

請參閱[設定點對站 VPN 連線 tooan Azure 虛擬網路](../vpn-gateway/vpn-gateway-point-to-site-create.md)如需詳細資訊。

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>設定虛擬網路和動態路由閘道
確保您已佈建 HBase 叢集的 Azure 虛擬網路中 （請參閱本章節的 hello 必要條件）。 hello 下一個步驟是 tooconfigure 點對站連線。

**tooconfigure hello 點對站連線能力**

1. 登入 toohello [Azure 傳統入口網站][azure-portal]。
2. Hello 左側，按一下 **網路**。
3. 按一下您所建立的 hello 虛擬網路 (請參閱[佈建 HBase 叢集的 Azure 虛擬網路上][hdinsight-hbase-provision-vnet])。
4. 按一下**設定**從 hello。
5. 在 hello**點對站連線能力**區段中，選取**設定點對站連線能力**。
6. 設定**起始 IP**和**CIDR** toospecify hello IP 位址範圍 VPN 用戶端將從其接收 IP 位址連線時。 hello 範圍不能與任何 hello 範圍位於內部網路，而且 hello 您將會連接到 Azure 虛擬網路重疊。 例如， 如果您選取 10.0.0.0/20 hello 虛擬網路，您可以選取 10.1.0.0/24 hello 用戶端的位址空間。 請參閱 hello[點對站連線能力][ vnet-point-to-site-connectivity]頁面以取得詳細的資訊。
7. 在 hello 虛擬網路位址空間 區段中，按一下 **加入閘道子網路**。
8. 按一下**儲存**上 hello hello 頁面的底部。
9. 按一下**是**tooconfirm hello 變更。 請等到完成 hello 系統進行變更後再繼續下一個程序 toohello hello。

**toocreate 動態路由閘道**

1. 從 hello Azure 傳統入口網站，按一下 **儀表板**從 hello hello 頁面的頂端。
2. 按一下**建立閘道**從 hello hello 頁面的底部。
3. 按一下**是**tooconfirm。 請等到建立 hello 閘道。
4. 按一下**儀表板**從 hello。  您會看見 hello 虛擬網路的視覺圖表：

    ![Azure 虛擬網路點對站虛擬圖表][img-vnet-diagram]

    hello 圖表會顯示 0 的用戶端連線。 連接 toohello 虛擬網路之後，hello 數目將會更新的 tooone。

#### <a name="create-your-certificates"></a>建立您的憑證
其中一種方式是使用 X.509 憑證的 toocreate hello 所隨附的憑證建立工具 (makecert.exe) [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx)。

**toocreate 自我簽署的根憑證**

1. 從您的工作站，開啟命令提示字元視窗。
2. 瀏覽 toohello Visual Studio 工具 資料夾。
3. 下列命令在 hello 面範例中的 hello 會建立與 hello 個人憑證存放區，您的工作站上安裝根憑證和也建立對應的.cer 檔案，您將於稍後上傳 toohello Azure 傳統入口網站。

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    變更您想 hello.cer 檔案 toobe HBaseVnetVPNRootCertificate 其中您要 hello 憑證 toouse hello 名稱中，位於 toohello 目錄。

    不要關閉 hello 命令提示字元。  您需要在 hello 下一個程序。

   > [!NOTE]
   > 因為您已建立將會產生用戶端憑證的根憑證，您可能想 tooexport 連同私密金鑰一起此憑證，並將它儲存 tooa 安全的位置，或許可以修復它。
   >
   >

**toocreate 用戶端憑證**

* Hello 從相同的命令提示字元 (對 hello toobe hello 根憑證的建立所在的同一部電腦。 hello 用戶端必須產生憑證從 hello 根憑證），執行 hello 下列命令：

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate 是 hello 根憑證名稱。  它有 toomatch hello 根憑證名稱。  

    Hello 根憑證和 hello 用戶端憑證儲存在您的個人憑證存放區，您的電腦上。 使用 certmgr.msc tooverify。

    ![Azure 虛擬網路點對站 VPN 憑證][img-certificate]

    用戶端憑證必須安裝在每部電腦上您想 tooconnect toohello 虛擬網路。 我們建議您建立唯一的用戶端憑證，每一部電腦的 tooconnect toohello 虛擬網路。 tooexport hello 用戶端憑證，請使用 certmgr.msc。

**tooupload hello 根憑證 toohello Azure 傳統入口網站**

1. 從 hello Azure 傳統入口網站，按一下 **網路**hello 左側。
2. 按一下 hello HBase 叢集部署到其中的虛擬網路。
3. 按一下**憑證**從 hello。
4. 按一下**上傳**hello 從下方，並指定您已建立在 hello 程序中最後一個以外的 hello 根憑證檔案。 請等到 hello 憑證已匯入。
5. 按一下**儀表板**hello 上方。  hello 虛擬圖表會顯示 hello 狀態。

#### <a name="configure-your-vpn-client"></a>設定 VPN 用戶端
**toodownload 並安裝 hello 用戶端 VPN 封裝**

1. 從 hello 儀表板頁面的 hello 虛擬網路，在 hello 快速概覽區段中，按一下 **下載 hello 64 位元用戶端 VPN 封裝**或**下載 hello 32 位元用戶端 VPN 封裝**根據您工作站作業系統版本。
2. 按一下**執行**tooinstall hello 封裝。
3. 在 hello 安全性提示字元中，按一下**進一歩**，然後按一下**繼續執行**。
4. 按兩下 [ **是** ]。

**tooconnect tooVPN**

1. 在您的工作站的 hello 桌面上，按一下 hello hello 工作列上的網路圖示。 您會看到虛擬網路名稱的 VPN 連線。
2. 按一下 hello VPN 連線名稱。
3. 按一下 [ **連接**]。

**tootest hello VPN 連接和網域名稱解析**

* 從 hello 工作站上，開啟 命令提示字元，且下列名稱指定 hello HBase 叢集的 DNS 尾碼的 hello 的其中一個 ping myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>安裝與設定您的工作站上的 SQuirreL
**tooinstall 松鼠**

1. 下載 hello 松鼠 SQL 用戶端 jar 檔案從[http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation)。
2. 開啟/執行 hello jar 檔案。 它需要 hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html)。
3. 按兩下 [ **下一步** ]。
4. 指定您擁有寫入權限，並再按 hello 路徑**下一步**。

  > [!NOTE]
  > hello 預設安裝資料夾為 hello C:\Program Files\squirrel sql 3.6 資料夾中。  順序 toowrite toothis 路徑，hello 安裝程式必須授與 hello 系統管理員權限。 您可以開啟命令提示字元，以系統管理員身分，瀏覽 tooJava 的 bin 資料夾，然後再執行：
  >
  >     java.exe-jar [hello hello 松鼠 jar 檔案路徑]
5. 按一下**確定**tooconfirm 建立 hello 目標目錄。
6. hello 預設設定是 tooinstall hello 基底和標準的封裝。  按一下 [下一步] 。
7. 依序按兩下 [下一步] 和 [完成]。

**tooinstall hello in Phoenix 驅動程式**

hello in phoenix 驅動程式 jar 檔案位於 hello HBase 叢集。 hello 路徑為 hello 版本為基礎的 toohello 下列類似：

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
您需要 toocopy 它 hello [松鼠安裝資料夾] 下的 tooyour 工作站 / lib 路徑。  hello 最簡單方式是到 hello 叢集中，然後按一下 使用檔案複製/貼上 （CTRL + C 和 CTRL + V） toocopy tooRDP 它 tooyour 工作站。

**tooadd in Phoenix 驅動程式 tooSQuirreL**

1. 從您的工作站開啟 SQuirreL SQL 用戶端。
2. 按一下 hello**驅動程式**hello 左邊的索引標籤。
3. 從 hello**驅動程式**功能表上，按一下 **新的驅動程式**。
4. 輸入下列資訊的 hello:

   * **名稱**：Phoenix
   * **範例 URL**：jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **類別名稱**：org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > 使用者在 hello 範例 URL 中的所有大小寫。 您可以使用完整 zookeeper 仲裁，以免其中一項已關閉。  hello 主機名稱為 zookeeper0、 zookeeper1 和 zookeeper2。
     >
     >

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-driver]
5. 按一下 [確定] 。

**toocreate 別名 toohello HBase 叢集**

1. 從松鼠，按一下 hello**別名**hello 左邊的索引標籤。
2. 從 hello**別名**功能表上，按一下 **新別名**。
3. 輸入下列資訊的 hello:

   * **名稱**: hello 名稱 hello HBase 叢集或任何您偏好的名稱。
   * **驅動程式**：Phoenix。  這必須符合您在 hello 最後一個程序中建立的 hello 驅動程式名稱。
   * **URL**: hello URL 已複製從驅動程式設定。 請確定 toouser 所有大小寫。
   * **使用者名稱**：可以是任何文字。  因為您在這裡使用 VPN 連線能力，是不會在所有使用 hello 使用者名稱。
   * **密碼**：可以是任何文字。

     ![HDInsight HBase Phoenix SQuirreL 驅動程式][img-squirrel-alias]
4. 按一下 [ **測試**]。
5. 按一下 [ **連接**]。 當建立 hello 連接時，松鼠看起來像：

    ![HBase Phoenix SQuirrel][img-squirrel]

**toorun 測試**

1. 按一下 hello **SQL**索引標籤上的權限下一步 toohello**物件** 索引標籤。
2. 複製並貼上下列程式碼的 hello:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. 按一下 hello 執行 按鈕。

    ![HBase Phoenix SQuirrel][img-squirrel-sql]
4. 切換後 toohello**物件** 索引標籤。
5. 展開 hello 別名名稱，然後再展開**資料表**。  您應該會看到 hello 底下所列的新資料表。

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 toouse Apache in Phoenix HDInsight 中。  toolearn 詳細資訊，請參閱

* [HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。
* [佈建 Azure 虛擬網路上的 HBase 叢集][hdinsight-hbase-provision-vnet]： 與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可以與通訊直接 HBase。
* [設定在 HDInsight HBase 複寫](hdinsight-hbase-replication.md)： 了解如何 tooconfigure HBase 複寫，跨兩個 Azure 資料中心。
* [分析與在 HDInsight HBase Twitter 情緒][hbase-twitter-sentiment]： 了解如何 toodo 即時[情緒分析](http://en.wikipedia.org/wiki/Sentiment_analysis)的巨量資料在 HDInsight Hadoop 叢集中使用 HBase。

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
