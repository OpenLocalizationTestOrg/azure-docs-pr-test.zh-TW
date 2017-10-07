---
title: "在 Azure （大型執行個體） 上的 SAP HANA 的 SAP HANA aaaInstall |Microsoft 文件"
description: "如何在 Azure （大型執行個體） 上的 SAP HANA 的 SAP HANA tooinstall。"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>如何 tooinstall 及設定 Azure 上 SAP HANA （大型執行個體）

以下是一些重要定義 tooknow 先閱讀本指南。 我們在 [Azure 上 SAP HANA (大型執行個體) 的概觀和架構](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)中引進了兩種不同類別的 HANA 大型執行個體單位：

- S72、 S72m、 S144、 S144m、 S192 和 S192m 我們 tooas hello '我類別的 Type' 的 Sku。
- S384、 S384m、 S384xm、 S576、 S768 及我們的 S960 tooas hello 'Type II class' 的 Sku。

hello 類別規範是進行 toobe 整個 hello toodifferent 功能與根據 HANA 大型執行個體 Sku 的需求，請參閱文件 tooeventually HANA 大型執行個體使用。

其他常用定義包括：
- **大型執行個體戳記：**硬體基礎結構堆疊是 SAP HANA TDI 認證和專用 toorun SAP HANA 的執行個體在 Azure 中。
- **在 Azure （大型執行個體） 上的 SAP HANA:** Azure toorun HANA 中的執行個體上 SAP HANA TDI 認證的硬體，部署在不同的 Azure 區域中的大型執行個體戳記中的 hello 優惠的正式名稱。 hello 相關詞彙**HANA 大型執行個體**是短的 Azure （大型執行個體） 上的 SAP HANA，廣泛使用此技術的部署指南。


hello SAP HANA 已安裝，您必須負責且 hello 活動接續的 Azure （大型執行個體） 的伺服器上新的 SAP HANA 遞交。 和您的 Azure VNet(s) 與 hello HANA 大型執行個體單位之間的 hello 連線已建立之後。 

> [!Note]
> 根據 SAP 原則，必須由個人認證 tooperform SAP HANA 安裝執行的 SAP HANA hello 安裝。 人員，已通過 hello 認證 SAP 技術關聯測驗，SAP HANA 安裝認證測驗，或 SAP 認證的系統整合者 (SI)。

再次檢查，特別是在規劃 tooinstall HANA 2.0 [SAP 支援附註 #2235581 SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E)順序 toomake 確定作業系統支援該 hello 以 hello SAP HANA 釋放您決定 tooinstall。 您了解支援的作業系統的限制多於 HANA 2.0 hello 作業系統支援 HANA 1.0 該 hello。 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>收到 hello HANA 大型執行個體單元後的第一個步驟

**第一步**在收到後 hello HANA 大型執行個體，且需建立存取和連線 toohello 執行個體，tooregister hello OS hello 與作業系統提供者的執行個體。 這個步驟包括 SUSE SMT 需要 toohave 部署在 Azure 中的 VM 中的執行個體中註冊您的 SUSE Linux 作業系統。 hello HANA 大型執行個體單位可以連接 toothis SMT 執行個體 （請參閱本文件中的更新版本）。 或 RedHat OS 必須向 hello Red Hat 訂用帳戶管理員，您需要以 tooconnect toobe。 另請參閱這份[文件](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中的備註。 這個步驟也是必要 toobe 無法 toopatch hello OS。 工作中的 hello 客戶的 hello 責任。 SUSE，尋找文件 tooinstall 並設定 SMT[這裡](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html)。

**第二個步驟**是新的更新和修正的 hello 特定作業系統版本/版本 toocheck。 檢查 hello HANA 大型執行個體的 hello 修補程式等級是否在 hello 最新狀態。 根據 OS 修補程式/版本與變更 toohello 映像可以部署 Microsoft 上的時間，可能會有情況下，hello 最新修補程式可能不會包含在內。 因此它是之後接管 HANA 大型執行個體單位，toocheck 是否同時發行特定 Linux 廠商 hello 修補程式的安全性、 功能、 可用性和效能相關，而且需要 toobe 套用必要的步驟。

**第三個步驟**是出 hello toocheck 上安裝和設定 SAP HANA hello 特定作業系統版本/版本相關的 SAP 附註。 由於 toochanging 建議或變更 tooSAP 附註或相依於個別的安裝案例的組態，Microsoft 不一定能 toohave HANA 大型執行個體單位完全設定。 因此，它會強制您為客戶、 tooread hello SAP 附註相關 tooSAP HANA 確切的 Linux 版本上。 也請檢查 hello OS 版本/版本所需的 hello 設定並套用 hello 組態設定其中尚未完成。

在特定，檢查下列參數，且最後會調整成 hello:

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

從 SLES12 SP1 和 RHEL 7.2，必須在 hello /etc/sysctl.d 目錄中的組態檔中設定這些參數。 例如，您必須建立含有 hello 名稱 91 NetApp HANA.conf 組態檔。 如果是舊版 SLES 和 RHEL，則必須 /etc/sysctl.conf 中設定這些參數。

針對所有 RHEL 發行版本和起 SLES12 hello 
- sunrpc.tcp_slot_table_entries = 128

參數必須在 /etc/modprobe.d/sunrpc-local.conf 中設定。 如果 hello 檔案不存在，它必須先建立藉由新增下列項目 hello: 
- options sunrpc tcp_max_slot_table_entries=128

**第四個步驟**HANA 大型執行個體單位的 toocheck hello 系統時間。 代表 hello Azure 地區 hello HANA 大型執行個體戳記位於 hello 位置的系統時區部署 hello 執行個體。 您是免費 toochange hello 系統時間或您擁有 hello 執行個體的時區時間。 這樣做並排序成您的租用戶的多個執行個體，您需要 tooadapt hello 的時區時間 hello 新傳遞執行個體備妥。 Microsoft 作業會有任何深入了解系統時區 hello 您 hello 執行個體之後設定 hello 移。 因此新部署的執行個體可能會在未設定 hello 相同時區為 hello 變更為一。 如此一來，您必須負責為客戶 toocheck，如有必要調整 hello hello 執行個體上的時區時間。 

**第五個步驟**toocheck 等/裝載。 隨著 hello 刀鋒視窗取得移交時，它們就會有不同的 IP 位址指派不同的用途，（請參閱下一節）。 請檢查 hello 等/主機檔案。 在其中單位會加入到現有的租用戶的情況下，不預期 toohave 等/新部署的 hello 系統正確維護 hello 的稍早傳遞系統的 IP 位址的主機。 因此它是您在客戶 toocheck hello 正確設定，可以互動的新部署的執行個體，並解析 hello 租用戶中先前已部署的單位名稱。 

## <a name="networking"></a>網路
我們假設您已遵循 hello 建議設計 Azure Vnet 和連接這些 Vnet toohello HANA 大型執行個體，這些文件中所述：

- [Azure 上 SAP HANA (大型執行個體) 的概觀和架構](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Azure 上 SAP HANA (大型執行個體) 的基礎結構和連接](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

有一些不 toomention 有關 hello 網路的 hello 單一單位的詳細資訊。 每個大型執行個體 HANA 單位隨附兩個或三個 tootwo 或 hello 單位的 3 個 NIC 連接埠指派的 IP 位址。 HANA 向外延展組態和 hello HANA 系統複寫案例中使用三個 IP 位址。 其中一個 hello IP 位址指派的 toohello hello 單位的 NIC 超出 hello hello 所述的伺服器的 IP 集區[SAP HANA （大型執行個體） 的概觀和架構，在 Azure 上的](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)。

兩個 IP 位址指派單位的 hello 發佈看起來應該像：

- eth0.xx 應該有指派的 IP 位址超出 hello 送出 tooMicrosoft 伺服器的 IP 集區位址範圍。 此 IP 位址應該用於 hello OS 的 /etc/hosts 中維護。
- eth1.xx 應該有 IP 位址指派用於通訊 tooNFS。 因此，這些位址進行**不**需要 toobe 等/主機順序 tooallow 執行個體 tooinstance 流量 hello 租用戶內維護。

就 HANA 系統複寫或 HANA 向外延展部署案例而言，並不適合使用有兩個指派之 IP 位址的刀鋒伺服器組態。 如果只指派兩個 IP 位址以及由 toodeploy 這種組態中，與 SAP HANA Azure 服務管理 tooget 第三個 IP 位址第三個指派的 VLAN。 有三個 IP 位址指派上 3 個 NIC 的連接埠 HANA 大型執行個體單位，hello 使用量適用下列規則：

- eth0.xx 應該有指派的 IP 位址超出 hello 送出 tooMicrosoft 伺服器的 IP 集區位址範圍。 因此這個 IP 位址不應該使用的 hello OS /etc/hosts 中維護。
- eth1.xx 應該用於通訊 tooNFS 存放裝置的 IP 位址指派。 因此，不應該在 etc/hosts 中維護此類型的位址。
- eth2.xx 應該以獨佔方式使用的 toobe 維護等/主控件 hello 不同執行個體之間的通訊。 這些位址也會需要 toobe HANA hello 節點間組態所使用的 IP 位址保持在向外延展 HANA 組態中的 hello IP 位址。



## <a name="storage"></a>儲存體

hello Azure （大型執行個體） 上的 SAP hana 的儲存配置設定上透過建議輔助線，如中所述的 SAP 的 Azure 服務管理的 SAP HANA [SAP HANA 存放裝置需求](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)技術白皮書。 hello hello 不同磁碟區的約略大小以詳加說明不同 HANA 大型執行個體 Sku 收到的 hello [SAP HANA （大型執行個體） 的概觀和架構，在 Azure 上的](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

hello hello 存放磁碟區的命名慣例已列於下表中的 hello:

| 儲存體使用量 | 掛接名稱 | 磁碟區名稱 | 
| --- | --- | ---|
| HANA 資料 | /hana/data/SID/mnt0000<m> | 儲存體 IP：/hana_data_SID_mnt00001_tenant_vol |
| HANA 記錄檔 | /hana/log/SID/mnt0000<m> | 儲存體 IP：/hana_log_SID_mnt00001_tenant_vol |
| HANA 記錄備份 | /hana/log/backups | 儲存體 IP：/hana_log_backups_SID_mnt00001_tenant_vol |
| HANA 共用 | /hana/shared/SID | 儲存體 IP：/hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | 儲存體 IP：/hana_shared_SID_mnt00001_tenant_vol/usr_sap |

其中 SID = hello HANA 執行個體的系統識別碼 

tenant = 部署租用戶時的內部作業列舉。

如您所見，共用 HANA 共用和 usr/sap hello 相同的磁碟區。 hello 命名法的 hello mountpoints 並包含 hello 的 hello HANA 執行個體，以及 hello 掛接編號系統識別碼。 在相應增加部署中，只有一個掛接，像是 mnt00001。 而在向外延展部署中，您會看到許多掛接，因為有背景工作角色和主要節點。 Hello 向外延展環境、 資料、 記錄檔，記錄備份的磁碟區會共用並附加 tooeach hello 向外延展組態中的節點。 執行多個 SAP 執行個體的設定，一組不同的磁碟區會是已建立並附加 toohello 韓文大型執行個體的單位。

當您讀取 hello 紙張，並尋找 HANA 大型執行個體單元，您將了解 hello 單位有相當多的磁碟區與 HANA/資料，而且我們有 HANA/記錄檔備份的磁碟區。 為什麼我們大小 hello HANA/資料很大的 hello 原因是 hello 儲存快照集，我們提供您的客戶使用 hello 相同的磁碟區。 這表示 hello 多個儲存體快照在執行時，hello 更多的空間供您指定的存放磁碟區中的快照集。 hello HANA/記錄檔備份磁碟區不是思考 toobe hello 磁碟區中的 tooput 資料庫備份。 它是可調整大小的 toobe 作為 hello HANA 交易記錄備份備份磁碟區。 在未來版本的 hello 儲存快照集自助服務，我們將為目標多個此特定磁碟區 toohave 頻繁的快照集。 與更頻繁的複寫 toohello 災害復原站台有 toooption 單元 hello hello HANA 大型執行個體的基礎結構所提供的災害復原功能。 詳細資訊請參閱 [Azure 上 SAP Hana (大型執行個體) 的高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

除了提供 toohello 儲存體，您就可以購買額外的儲存體容量，以 1 TB 為增量單位。 此額外的存放裝置可新增為新的磁碟區 tooa HANA 大型執行個體。

在上線期間與 Azure 服務管理上的 SAP HANA，hello 客戶指定的使用者識別碼 (UID) 與群組識別碼 (GID) hello sidadm 使用者和 sapsys 群組 (例如： 1000,500) 則需要在安裝期間的 hello SAP HANA 系統，會使用這些相同的值。 您想要 toodeploy 單元上的多個 HANA 執行個體，您會取得多個磁碟區 （每個執行個體的一組） 集。 如此一來，在部署期間您會需要 toodefine:

- hello hello 不同 HANA 的執行個體 （sidadm 衍生不使用） 的 SID。
- Hello 不同 HANA 執行個體的記憶體大小。 因為 hello 記憶體大小，每個執行個體中每個個別的磁碟區組定義 hello hello 磁碟區大小。

根據存放裝置提供者建議 hello 下列掛接選項已針對所有掛接的磁碟區 （不包括開機 LUN）：

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

這些掛接點設定在 /etc/hosts fstab 像下列圖形中顯示 hello:

![HANA 大型執行個體單位中掛接磁碟區的 fstab](./media/hana-installation/image1_fstab.PNG)

hello 的 hello 命令 df-h S72m HANA 大型執行個體單元上的輸出應該像這樣：

![HANA 大型執行個體單位中掛接磁碟區的 fstab](./media/hana-installation/image2_df_output.PNG)


hello 存放裝置控制器和 hello 大型執行個體戳記中的節點是同步的 tooNTP 的伺服器。 與您 hello SAP HANA Azure （大型執行個體） 單位和 Azure Vm 上的對 NTP 伺服器同步處理應該 hello 基礎結構與 Azure 或大型執行個體戳記中的 hello 計算單位之間沒有很多時間漂移現象。

順序 toooptimize 之下使用的 SAP HANA toohello 儲存區，您也應該設定 hello 遵循 SAP HANA 組態參數：

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
向上 tooSPS12 SAP HANA 1.0 版本，這些參數可以中所述的 hello hello SAP HANA 資料庫，安裝期間設定[SAP 附註 #2267798 hello SAP HANA 資料庫的組態](https://launchpad.support.sap.com/#/notes/2267798)

您也可以設定 hello 參數 hello SAP HANA 資料庫安裝後，使用 hello hdbparam 架構。 

SAP HANA 2.0，hello hdbparam framework 已被取代。 因此您必須使用 SQL 命令來設定 hello 參數。 如需詳細資料，請參閱 [SAP 附註 #2399079：在 HANA 2 中已刪除 hdbparam (英文)](https://launchpad.support.sap.com/#/notes/2399079)。


## <a name="operating-system"></a>作業系統

交換空間的 hello 傳遞 OS 映像設定根據 toohello too2 GB [SAP 支援附註 #1999997 常見問題集： SAP HANA 記憶體](https://launchpad.support.sap.com/#/notes/1999997/E)。 任何不同設定所需需要 toobe 設定由您的客戶。

[SUSE Linux Enterprise Server 12 SP1 針對 SAP 應用程式](https://www.suse.com/products/sles-for-sap/hana)是 Linux 安裝在 Azure （大型執行個體） 上的 SAP hana 的 hello 分佈。 這個特定的分佈提供 SAP 特定功能&quot;hello 現成&quot;（包括預先設定的參數，有效地執行 SAP SLES 上）。

請參閱[資源程式庫/白皮書](https://www.suse.com/products/sles-for-sap/resource-library#white-papers)hello SUSE 網站上和[SAP on SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)上 hello SAP 社群網路 (SCN) 是否有數個實用的資源相關 toodeploying SLES （包括 hello 安裝上的 SAP HANA高可用性、 安全性強化特定 tooSAP 作業等等）。

額外和有用的 SAP on SUSE 相關連結︰

- [SUSE Linux 網站上的 SAP HANA](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [SAP 的最佳做法：加入佇列複寫 – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113)。
- [ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (包括 SLES 12 for SAP 應用程式)。

SAP 支援附註適用於 tooimplementing SLES 12 上的 SAP HANA:

- [SAP 支援附註 #1944799 – SLES 作業系統安裝的 SAP HANA 指南](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)。
- [SAP 支援附註 #2205917 – 針對 SLES 12 for SAP 應用程式的 SAP HANA DB 建議作業系統設定](https://launchpad.support.sap.com/#/notes/2205917/E)。
- [SAP 支援附註 #1984787 – SUSE Linux Enterprise Server 12：安裝注意事項](https://launchpad.support.sap.com/#/notes/1984787)。
- [SAP 支援附註 #171356 – 在 Linux 上的 SAP 軟體︰一般資訊](https://launchpad.support.sap.com/#/notes/1984787)。
- [SAP 支援附註 #1391070 – Linux UUID 解決方案](https://launchpad.support.sap.com/#/notes/1391070)。

[Red Hat Enterprise Linux for SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) 是可供在 HANA Large Instances 上執行 SAP HANA 的另一個供應項目。 版本 RHEL 6.7 和 7.2 均可使用。 

額外和有用的 SAP on Red Hat 相關連結︰
- [Red Hat Linux 網站上的 SAP HANA](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat)。

SAP 支援附註適用於 tooimplementing Red Hat 上的 SAP HANA:

- [SAP 支援附註 #2009879 - 適用於 Red Hat Enterprise Linux (RHEL) 作業系統的 SAP HANA 指南](https://launchpad.support.sap.com/#/notes/2009879/E)。
- [SAP 支援附註 #2292690 - SAP HANA DB：適用於 RHEL 7 的建議作業系統設定](https://launchpad.support.sap.com/#/notes/2292690)。
- [SAP 支援附註 #2247020 - SAP HANA DB：適用於 RHEL 6.7 的建議作業系統設定](https://launchpad.support.sap.com/#/notes/2247020)。
- [SAP 支援附註 #1391070 – Linux UUID 解決方案](https://launchpad.support.sap.com/#/notes/1391070)。
- [SAP 支援附註 #2228351 - Linux：RHEL 6 或 SLES 11 上的 SAP HANA Database SPS 11 修訂版 110 (或更新版本)](https://launchpad.support.sap.com/#/notes/2228351)。
- [SAP 支援附註 #2397039 - 常見問題集：SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039)。
- [SAP 支援附註 #1496410 - Red Hat Enterprise Linux 6.x：安裝和升級](https://launchpad.support.sap.com/#/notes/1496410)。
- [SAP 支援附註 #2002167 - Red Hat Enterprise Linux 7.x：安裝和升級](https://launchpad.support.sap.com/#/notes/2002167)。

## <a name="time-synchronization"></a>時間同步處理

Hello 各種元件組成 hello SAP 系統在 hello SAP NetWeaver 架構上建置的 SAP 應用程式是機密的時間差異。 簡短的 SAP ABAP 傾印的 ZDATE hello 錯誤標題\_大\_時間\_差異是可能熟悉的內容，這些簡短的傾印時，會出現 hello 不同的伺服器或 Vm 的系統時間會變動太距離。

在 Azure （大型執行個體），在 Azure 規定 &#39; 中完成的時間同步處理上的 SAP hana t 套用 toohello hello 大型執行個體戳記中的計算單位。 這項同步處理並不適用於在原生 Azure VM 中執行 SAP 應用程式，因為 Azure 可確保正確同步處理系統時間。 如此一來，個別的時間必須設定伺服器，可供 Azure Vm 上執行的 SAP 應用程式伺服器和 hello SAP HANA 資料庫 HANA 大型執行個體上執行的執行個體。 在大型執行個體戳記中的 hello 儲存體基礎結構是與 NTP 伺服器同步處理的時間。

## <a name="setting-up-smt-server-for-suse-linux"></a>設定 SUSE Linux 的 SMT 伺服器
SAP HANA 大型執行個體沒有直接連線 toohello 網際網路。 因此它不是簡單的程序 tooregister hello OS 提供者與 toodownload 這類的單位，並套用修補程式。 SUSE Linux 的 hello 案例中，在其中一種解決方案可能是 tooset SMT 台伺服器，Azure VM 中。 而 hello Azure VM 需要 toobe 裝載於 Azure 的 VNet，也就是連接的 toohello HANA 大型執行個體。 與這類 SMT 伺服器 hello HANA 大型執行個體單位無法註冊，並下載修補程式。 

SUSE 提供大量有關 [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf) (SLES 12 SP2 訂用帳戶管理工具) 的指南。 

成套 hello HANA 大型執行個體，可滿足 hello 工作 SMT 伺服器安裝，您需要：

- Azure VNet 的連接的 toohello HANA 大型執行個體 ER 循環。
- 與組織相關聯的 SUSE 帳戶。 而 hello 組織需要 toohave 某些有效 SUSE 訂用帳戶。

### <a name="installation-of-smt-server-on-azure-vm"></a>在 Azure VM 上安裝 SMT 伺服器

在此步驟中，您可以安裝在 Azure VM 中的 hello SMT 伺服器。 hello 第一個量值是在 toohello toolog [SUSE 客戶中心](https://scc.suse.com/)

當您登入，請移 tooOrganization--> 組織的認證。 在該區段中，您應該尋找必要 tooset hello SMT 伺服器 hello 認證。

hello 第三個步驟是 tooinstall hello Azure VNet 中的 SUSE Linux VM。 toodeploy hello VM 需要 Azure 的 SLES 12 SP2 圖庫映像。 Hello 部署程序，在未定義的 DNS 名稱，而且不會使用靜態 IP 位址這個螢幕擷取畫面所示

![SMT 伺服器的 VM 部署](./media/hana-installation/image3_vm_deployment.png)

hello 已部署的 VM 是較小的 VM，並且收到 hello 的 10.34.1.4 Azure VNet 中的 hello 內部 IP 位址。 Hello VM 的名稱為 smtserver。 Hello 安裝之後，已核取 hello 連線 toohello HANA 大型執行個體單元。 取決於您的組織名稱解析方式您可能需要等/主機的 hello Azure VM 中的 hello HANA 大型執行個體單位 tooconfigure 解析度。 加入額外的磁碟 toohello 即將 toobe 用 toohold hello 修補程式的 VM。 hello 開機磁碟本身可能太小。 在示範 hello 的情況下，hello 磁碟了掛接太/srv/www/htdocs hello 下列螢幕擷取畫面所示。 100 GB 的磁碟應已足夠。

![SMT 伺服器的 VM 部署](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

登入 toohello HANA 大型執行個體單元、 維護 /etc/hosts 並檢查是否可達到 hello 應該 toorun hello SMT 伺服器 hello 網路上的 Azure VM。

這項檢查已成功完成之後，您會需要 toolog toohello hello SMT 伺服器上執行的 Azure VM 中。 如果您使用 putty toolog toohello VM 中，您需要 tooexecute 這一系列命令的 bash 視窗中：

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

在執行這些命令之後, 重新啟動您 bash tooactivate hello 的設定。 然後啟動 YAST。

在 YAST，請前往 tooSoftware 維護 smt 搜尋。 選取 smt，自動切換 tooyast2 smt 如下所示

![yast 中的 SMT](./media/hana-installation/image5_smt_in_yast.PNG)


接受 hello hello smtserver 上安裝的選取範圍。 安裝之後，移 toohello SMT 伺服器組態，並輸入 hello SUSE 客戶中心您稍早擷取 hello 組織認證。 也為 hello SMT 伺服器 URL 輸入您的 Azure VM 主機名稱。 在此示範中，它會是 https://smtserver hello 下一個圖形中所示。

![SMT 伺服器組態](./media/hana-installation/image6_configuration_of_smtserver1.png)

在下一個步驟中，您會需要 tootest 是否 hello 連接 toohello SUSE 客戶 Center 的運作方式。 您在 hello 下列圖形，在 hello 示範案例中，看到能夠運作。

![測試連接 tooSUSE 客戶 Center](./media/hana-installation/image7_test_connect.png)

一次 hello SMT 安裝程式啟動時，您會需要 tooprovide 資料庫密碼。 因為這是新的安裝，您需要 toodefine hello 下一個圖形中所示的密碼。

![定義資料庫密碼](./media/hana-installation/image8_define_db_passwd.PNG)

您擁有 hello 下一步互動時，取得建立的憑證。 瀏覽 hello 對話方塊如下所示，hello 步驟應該繼續進行。

![建立 SMT 伺服器憑證](./media/hana-installation/image9_certificate_creation.PNG)

可能會有結尾 hello hello 組態執行同步處理檢查' hello 步驟中所花費幾分鐘。 Hello 安裝及設定之後的 hello SMT 伺服器，您應該會發現下 hello 掛接點 /srv/www/htdocs hello 目錄儲存機制/再加上一些子目錄下儲存機制。 

重新啟動 hello SMT 伺服器及其相關的服務與這些命令。

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>將套件下載到 SMT 伺服器

在所有 hello 重新啟動服務、 選取 hello 使用 Yast SMT 管理中的適當套件。 hello 套件選取項目取決於 hello hello HANA 大型執行個體伺服器的作業系統映像以及不 hello SLES 版本或 hello VM 執行 hello SMT 伺服器的版本。 Hello 選取畫面的範例如下所示。

![選取套件](./media/hana-installation/image10_select_packages.PNG)

一旦您完成 hello 套件選取項目時，您會需要 toostart hello 初始複本的 hello 選取封裝 toohello SMT 伺服器設定。 在使用 hello 命令 smt 鏡像如下所示的 hello 介面中觸發這個複本


![下載封裝 tooSMT 伺服器](./media/hana-installation/image11_download_packages.PNG)

您看到上方，hello 封裝應該複製到 hello hello 掛接點 /srv/www/htdocs 下建立的目錄。 此程序需要一會兒。 取決於您選取的套件數目，就無法在 tooone 小時或更多。
如同此程序完成時，您會需要 toomove toohello SMT 用戶端安裝程式。 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>設定單元 HANA 大型執行個體上的 hello SMT 用戶端

hello 用戶端在此情況下是 hello HANA 大型執行個體單位。 hello SMT server 安裝程式會複製到 hello Azure VM 的 hello 指令碼 clientSetup4SMT.sh。 將該指令碼複製 toohello HANA 大型執行個體單元要 tooconnect tooyour SMT 伺服器。 請使用 hello-h 選項啟動 hello 指令碼，並提供做為參數 hello SMT 伺服器名稱。 在此範例 smtserver 中。

![設定 SMT 用戶端](./media/hana-installation/image12_configure_client.PNG)

可能的案例，其中 hello hello 憑證從用戶端 hello hello 伺服器載入成功，但 hello 註冊失敗，如下所示。

![用戶端註冊失敗](./media/hana-installation/image13_registration_failed.PNG)

如果 hello 註冊失敗，請閱讀本[SUSE 支援文件](https://www.suse.com/de-de/support/kb/doc/?id=7006024)並執行 hello 那里所述的步驟。

> [!IMPORTANT] 
> 做為伺服器名稱，則會需要 tooprovide hello 名稱 hello VM，在此案例的 smtserver，不含 hello 完整的網域名稱。 只要 hello VM 名稱運作。 

在執行這些步驟之後，您需要下列命令在 hello HANA 大型執行個體單元 tooexecute hello

```
SUSEConnect –cleanup
```

> [!Note] 
> 在我們的測試，我們一律必須 toowait 幾分鐘的時間之後該步驟。 hello 立即執行 clientSetup4SMT.sh hello 矯正措施中所述 hello SUSE 發行項，以結束該 hello 憑證不是有效尚未的訊息。 通常等 5-10 分鐘後再執行 clientSetup4SMT.sh，就可以順利完成用戶端組態。

如果您需要 toofix hello 步驟 hello SUSE 發行項所根據的 hello 問題，您需要 toorestart clientSetup4SMT.sh hello HANA 大型執行個體單位上的一次。 現在它應該如下所示成功完成。

![用戶端註冊成功](./media/hana-installation/image14_finish_client_config.PNG)

有了這個步驟中，您可以設定對您在 hello Azure VM 中安裝的 hello SMT 伺服器 hello HANA 大型執行個體單元 tooconnect hello SMT 用戶端。 您現在可以採用 'zypper up' 或 'zypper 中的' tooinstall OS 修補程式 tooHANA 大型執行個體，或安裝其他的封裝。 應該已知道，您只可以讓您先下載 hello SMT 伺服器的修補程式。


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>範例：在 HANA 大型執行個體上安裝 SAP HANA
本節說明如何 tooinstall SAP HANA HANA 大型執行個體單元上的。 hello 啟動狀態，我們必須看起來像：

- 提供 Microsoft 所有的 hello 資料 toodeploy 您 SAP HANA 大型執行個體。
- 您可以從 Microsoft 收到 hello SAP HANA 大型執行個體。
- 您建立 Azure VNet 連接的 tooyour 在內部部署網路。
- 連接 HANA 大型執行個體 toohello 的 hello ExpressRotue 電路相同 Azure VNet。
- 您安裝了 Azure VM 用做為 HANA 大型執行個體的跳躍方塊。
- 您確定您可以連接從 hello 跳躍方塊 tooyour HANA 大型執行個體單位，反之亦然。
- 您可以檢查是否所有 hello 必要的封裝，並安裝修補程式。
- 您可以閱讀 hello SAP 附註和文件之有關 HANA hello 您正在使用，並確定所選擇的 hello HANA 版本 hello 作業系統版本上支援的作業系統上的安裝。

Hello 下一個序列中所示為 hello 下載 hello HANA 安裝封裝 toohello 跳躍方塊 VM，並且在 Windows 作業系統上，hello 封裝 toohello HANA 大型執行個體單元 hello 複本和 hello 一連串 hello 安裝程式在此情況下執行。

### <a name="download-of-hello-sap-hana-installation-bits"></a>Hello SAP HANA 安裝 bits 下載
由於 hello HANA 大型執行個體單位無法直接連線 toohello 網際網路，您無法直接下載 hello 安裝封裝從 SAP toohello HANA 大型執行個體 VM。 tooovercome hello 遺漏直接網際網路連線，您需要 hello 跳躍方塊。 您下載 hello 封裝 toohello 跳躍方塊 VM。

在訂單 toodownload hello HANA 安裝封裝，您將需要 SAP S 使用者或其他使用者，可讓您 tooaccess hello SAP Marketplace。 登入之後，請完成這一系列的畫面：

跳過[SAP 服務 Marketplace](https://support.sap.com/en/index.html) > 按一下 下載軟體 > 安裝與升級 > 依字母順序排列索引 > 下 H-SAP HANA 平台版本 > SAP HANA 平台版本 2.0 > 安裝 > 下載 hello下列檔案

![下載 HANA 安裝](./media/hana-installation/image16_download_hana.PNG)

在 hello 示範案例中，我們會下載 SAP HANA 2.0 安裝封裝。 Hello Azure 跳躍方塊 VM，您可以展開 hello 自我解壓縮的封存到 hello 目錄，如下所示。

![解壓縮 HANA 安裝](./media/hana-installation/image17_extract_hana.PNG)

Hello 封存解壓縮，因為複製 hello 51052030，為您建立的目錄中的 hello /hana/shared 磁碟區 toohello HANA 大型執行個體單元上方 hello 案例中的 hello 擷取所建立的目錄。

> [!Important]
> 請勿將 hello 安裝套件複製到 hello 根或開機 LUN，因為空間有限，而且必須由其他處理序 toobe。


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>在 hello HANA 大型執行個體單位上安裝 SAP HANA
順序 tooinstall SAP HANA，您需要在 toolog 為使用者的根。 只有根有足夠的權限 tooinstall SAP HANA。
您需要 toodo hello 第一件事是 tooset hello 目錄複製到/hana/共用權限。 需要像 tooset hello 權限。

```
chmod –R 744 <Installation bits folder>
```

如果您想 tooinstall SAP HANA 使用 hello 圖形化安裝程式，hello gtk2 封裝需求 toobe hello HANA 大型執行個體上安裝。 檢查是否已安裝與 hello 命令

```
rpm –qa | grep gtk2
```

在進一步步驟中，我們會示範 hello SAP HANA 安裝 hello 圖形化使用者介面。 在下一個步驟中，進入 hello 安裝目錄，並瀏覽到 hello 子目錄 HDB_LCM_LINUX_X86_64。 Start

```
./hdblcmgui 
```
從該目錄。 現在您會取得引導您完成一連串的螢幕 hello 安裝需要 tooprovide hello 資料。 在示範 hello 的情況下，我們要安裝 hello SAP HANA 資料庫伺服器和 hello SAP HANA 用戶端元件。 因此我們選取 [SAP HANA 資料庫]，如下所示。

![在安裝中選取 [HANA]](./media/hana-installation/image18_hana_selection.PNG)

在 hello 下一個畫面中，選擇 hello 選項安裝新 System'

![新安裝選取 [HANA]](./media/hana-installation/image19_select_new.PNG)

這個步驟之後，您需要可以另外安裝的數個其他元件之間的 tooselect toohello SAP HANA 資料庫伺服器。

![選取其他的 HANA 元件](./media/hana-installation/image20_select_components.PNG)

這份文件的 hello 用途，我們選擇 hello SAP HANA 用戶端並 hello SAP HANA Studio。 我們也安裝了相應增加執行個體。 因此在 hello 下一個畫面中，您必須 toochoose 單一主機系統 

![選取相應增加安裝](./media/hana-installation/image21_single_host.PNG)

在 hello 下一個畫面中，您需要 tooprovide 某些資料

![提供 SAP HANA SID](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> 做為 HANA 系統識別碼 (SID)，您需要 tooprovide 排序 hello HANA 大型執行個體部署時，會提供 Microsoft hello 相同的 SID。 選擇不同的 SID，將會因 tooaccess hello 不同磁碟區上的權限問題而失敗的 hello 安裝

安裝目錄使用 hello /hana/shared 目錄。 您可以在 hello 下一個步驟中，需要 tooprovide hello 位置來 hello HANA 資料檔案和 hello HANA 記錄檔


![提供 HANA 記錄檔位置](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> 您應該定義為資料和記錄檔 hello 已隨附包含 hello SID 您選擇在這個畫面之前 hello 螢幕選取範圍中的 hello 掛接點的磁碟區。 如果 hello SID 未不符以 hello 其中一個您輸入時，在囉 」 畫面之前，請返回並調整 hello 您擁有 hello 掛接點的 SID toohello 值。

在 hello 下一個步驟中，檢閱 hello 主機名稱並最終加以更正。 

![檢閱主機名稱](./media/hana-installation/image24_review_host_name.PNG)

在 hello 下一個步驟中，您也需要排序 hello HANA 大型執行個體部署時，指定給 tooMicrosoft tooretrieve 資料。 

![提供系統使用者 UID 與 GID](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> 您需要 tooprovide 排序 hello 單元部署時，會提供 Microsoft hello 相同的系統使用者識別碼和使用者群組的識別碼。 如果您非常容錯 toogive hello 相同的識別碼，SAP HANA 上 hello HANA 大型執行個體單元 hello 安裝將會失敗。

Hello 下面兩個畫面，我們不會顯示這份文件中，您需要 tooprovide hello 密碼 hello SAP HANA 資料庫與 hello hello sapadm 使用者密碼，用來取得安裝的一部分的 SAP Host Agent hello hello 系統使用者hello SAP HANA 資料庫執行個體。

定義之後 hello 密碼，確認畫面會顯示。 檢查 hello 的所有資料列，然後再繼續進行 hello 安裝。 您到達文件 hello 安裝進度，類似下面其中一個 hello 進度畫面

![檢查安裝進度](./media/hana-installation/image27_show_progress.PNG)

因為 hello 安裝完成後，您應該像 hello 下列其中一張圖片

![安裝完成](./media/hana-installation/image28_install_finished.PNG)

此時，hello SAP HANA 執行個體應該啟動並執行並備妥可供使用。 您應該能夠 tooconnect tooit 從 SAP HANA Studio。 也請確定您檢查 hello SAP HANA 的最新修補程式，並套用這些修補程式。
























































 







 




