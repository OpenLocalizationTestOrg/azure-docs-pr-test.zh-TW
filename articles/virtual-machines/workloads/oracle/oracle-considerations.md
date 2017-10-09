---
title: "Microsoft Azure 上的 aaaOracle 解決方案 |Microsoft 文件"
description: "了解 Microsoft Azure 上支援的 Oracle 解決方案組態和限制。"
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Microsoft Azure 上的 Oracle 解決方案及其部署
本文涵蓋必要的 toosuccesfully 部署 Microsoft Azure 上的各種 Oracle 解決方案的資訊。 這些解決方案根據由 Oracle 發行 hello Azure Marketplace 中的虛擬機器映像。 tooget 一份目前可用的映像，執行下列命令的 hello:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
自 2017 年 6-16 hello 的映像的清單是 hello 下列：
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

系統會將這些映像視為「自備授權」，因此您只會支付執行 VM 產生的計算成本、儲存成本和網路成本。  它會假設您是正確授權的 toouse Oracle 軟體，而且您在與 Oracle 就地擁有目前的支援合約。 Oracle 已從內部部署 tooAzure 保證的授權流動性。 請參閱發行 hello [Oracle 和 Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)附註的授權流動性的詳細資訊。 

個人版也可以選擇 toobase 上他們在 Azure 中重新建立或從其在內部部署環境的自訂映像上傳的自訂映像及其解決方案。

## <a name="support-for-jd-edwards"></a>JD Edwards 的支援
根據 tooOracle 支援附註[文件識別碼 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) ，JD Edwards EnterpriseOne 或 9.2 及以上版本支援的**的任何公用雲端供應項目**符合其特定`Minimum Technical Requirements`(MTR)。  您必須符合其作業系統和軟體應用程式相容性的 MTR 規格的 toocreate 自訂映像。 

## <a name="oracle-database-virtual-machine-images"></a>Oracle 資料庫虛擬機器映像
Oracle 支援在以 Oracle Linux 為基礎的虛擬機器映像上，在 Azure 中執行 Oracle DB 12.1 Standard 和 Enterprise 版本。  在 Azure 上的 Oracle 資料庫的生產工作負載的 hello 達到最佳效能，確定 tooproperly 大小 hello VM 映像，而且使用高階儲存體都由受管理的磁碟。 如需如何 tooquickly 取得 Oracle DB 啟動且正在執行中的指示 Azure 使用 hello Oracle 發行 VM 映像，[再試一次 hello Oracle DB 快速入門逐步解說](oracle-database-quick-create.md)。

### <a name="attached-disk-configuration-options"></a>連接的磁碟組態選項

連接的磁碟依賴 hello Azure Blob 儲存體服務。 理論上每個標準磁碟最多都能達約每秒 500 輸入/輸出作業 (IOPS)。 我們 premium 磁碟供應項目是高效能資料庫工作負載的慣用發佈點，而且可以達到總 too5000 每個磁碟的 IOps。 雖然您可以使用單一磁碟是否符合您的效能需要-如果您使用多個已連接的磁碟、 資料庫資料分散，然後再使用 Oracle 自動儲存體管理 (ASM)，來改善 hello 有效的 IOPS 效能。 如需有關 Oracle ASM 的特定詳細資訊，請參閱 [Oracle Automatic Storage 概觀](http://www.oracle.com/technetwork/database/index-100339.html) (英文)。 如需如何 tooinstall 和設定 Linux 的 Azure VM 上的 Oracle ASM-您可以嘗試 hello[安裝和設定 Oracle 自動儲存體管理](configure-oracle-asm.md)教學課程。

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle Realtime Application Cluster (RAC)
Oracle RAC 是在內部部署的多節點叢集組態中的單一節點設計的 toomitigate hello 失敗。  它依賴兩個不是原生 toohyper 延展公用雲端環境在內部部署技術： 網路多點傳送和共用的磁碟。 有公司所建立的第三方解決方案[例如 FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) ，模擬這些技術，如果您需要 toodeploy Oracle RAC，在 Azure 中。 

### <a name="high-availability-and-disaster-recovery-considerations"></a>高可用性和災害復原考量
當使用 Oracle 資料庫在 Azure 中，您必須負責實作高可用性和災害復原方案 tooavoid 任何停機時間。 

Azure 上的 Oracle Database Enterprise Edition (不含 RAC) 可以使用 [Data Guard、Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) 或 [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate) 來達成高可用性和災害復原，且兩個資料庫位於不同的虛擬機器上。 這兩個虛擬機器應該會在 hello 相同[虛擬網路](https://azure.microsoft.com/documentation/services/virtual-network/)tooensure 它們可以透過 hello 私用持續性 IP 位址相互存取。  此外，我們建議將 hello 虛擬機器放置在 hello 相同可用性設定組 tooallow Azure tooplace 它們在另一個故障網域和升級網域。  如果您想 toohave 異地備援-您可以讓這兩個資料庫之間兩個不同的區域複寫，並連接 VPN 閘道 hello 兩個執行個體。

我們有教學課程 」[實作在 Azure 上的 Oracle DataGuard](configure-oracle-dataguard.md)"它將引導您完成 hello 基本安裝程序 tootrial 這在 Azure 上。  

使用 Oracle Data Guard，可以藉由某個虛擬機器中的主要資料庫、另一個虛擬機器中的次要 (待命) 資料庫以及它們之間的單向複寫設定，達到高可用性。 hello 結果為 hello 資料庫的讀取權限 toohello 副本。 您可以使用 Oracle GoldenGate 設定 hello 兩個資料庫之間的雙向複寫。 如何使用這些工具中，資料庫的高可用性解決方案 tooset 參閱的 toolearn[主動資料防護](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html)和[GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) hello Oracle 網站上的文件。 如果您需要讀寫存取 toohello hello 資料庫複本，您可以使用[Oracle 主動資料防護](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html)。

我們有教學課程 」[實作在 Azure 上的 Oracle GoldenGate](configure-oracle-golden-gate.md)"它將引導您完成 hello 基本 seup 程序 tootrial 這在 Azure 上。

儘管有架構在 Azure 中的 HA 功能和 DR 能力解決方案，您會想 tooensure 您有備份策略位置 toorestore 在您的資料庫。  我們有教學課程[備份及復原 Oracle 資料庫](oracle-backup-recovery.md)的逐步解說 hello 建立 consistant 備份的基本程序。

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Oracle WebLogic Server 虛擬機器映像
* **只有在 Enterprise Edition 上才支援叢集。** 您的授權 toouse WebLogic 叢集使用時，才 hello 的 WebLogic Server Enterprise Edition。 請勿在使用 WebLogic Server Standard Edition 時使用叢集。
* **不支援 UDP 多點傳送。** Azure 支援 UDP 單點傳播，但不支援多點傳送或廣播。 無法在 Azure 的 UDP 單點傳播功能 toorely WebLogic 伺服器。 針對最依賴 UDP 單點傳播的結果，我們建議 hello WebLogic 叢集大小會保持靜態，或保留與 hello 叢集中包含最多 10 個受管理伺服器。
* **WebLogic Server 預期公用和私用連接埠 toobe hello 相同 T3 存取 （例如，當使用 Enterprise JavaBeans 時）。** 請考慮使用多層式案例，其中服務層 (EJB) 應用程式會在 WebLogic Server 叢集上執行，而該叢集包含兩個或多個 VM，且都位於名為 **SLWLS** 的 vNet 中。 在 hello 不同子網路中的 hello 用戶端層是相同的 vNet，執行簡單的 Java 程式，嘗試 toocall EJB hello 服務層中的。 因為它是必要的 tooload 平衡 hello 服務層，公用負載平衡的端點必須 toobe 建立 hello 虛擬機器在 hello WebLogic Server 叢集。 如果您指定的 hello 私用連接埠 hello 公用連接埠 (例如，7006: 7008) 不同，就會發生錯誤，例如 hello 下列：

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   這是因為中的任何遠端 T3 存取，WebLogic Server 預期 hello 負載平衡器連接埠和 hello WebLogic 受管理伺服器連接埠 toobe hello 相同。 在上述案例 hello，hello 用戶端正在存取連接埠 7006 （hello 負載平衡器連接埠），hello 受管理的伺服器正在接聽 7008 （hello 私用連接埠）。 這項限制只適用於 T3 存取，不適用於 HTTP。

   tooavoid 這個問題，請使用其中一個 hello 下列因應措施：

  * 使用 hello 相同私人和公用連接埠號碼為負載平衡端點專用 tooT3 存取。
  * 包括 hello 啟動 WebLogic Server 時，下列 JVM 參數：

         -Dweblogic.rjvm.enableprotocolswitch=true

如需相關資訊，請參閱知識庫文章 **860340.1**，位於：<http://support.oracle.com>。

* **動態叢集和負載平衡限制。** 假設您想 toouse WebLogic Server 中的動態叢集，並將它公開透過單一、 公用負載平衡端點在 Azure 中。 作法是，只要為每個 hello 受管理伺服器 （不會動態指派的範圍內），而且不會啟動多超過機器 hello 系統管理員正在追蹤受管理的伺服器，使用固定通訊埠編號 （也就是不超過一個受管理伺服器每 virtual 機器）。 如果您的設定會導致正在啟動虛擬機器有更多的 WebLogic 伺服器 (亦即，其中多個 WebLogic Server 執行個體共用 hello 相同的虛擬機器)，則不是可將一個以上的 WebLogic Server 的執行個體伺服器 toobind tooa 指定連接埠號碼 – hello 該虛擬機器上的其他人將會失敗。

   在 hello 另一方面，如果您設定 hello 管理員伺服器 tooautomatically 指派唯一的連接埠號碼 tooits 受管理伺服器，負載平衡就不可能會因為 Azure 不支援從單一公用連接埠 toomultiple 私用連接埠對應，因為可以此組態的必要項。
* **虛擬機器上的多個 Weblogic Server 執行個體。** 根據您的部署需求，您可以考慮 hello 上執行多個 WebLogic Server 執行個體中的 hello 選項相同的虛擬機器，如果 hello 虛擬機器足夠大。 例如，在中型大小的虛擬機器，其中包含兩個核心，您可以選擇 toorun WebLogic Server 的兩個執行個體。 請注意，但是我們還是建議您避免單一失敗點引入到您的架構，會 hello 情況下，如果您使用只在一個虛擬機器正在執行多個 WebLogic Server 執行個體。 使用至少兩個虛擬機器可能是較好的方法，每個虛擬機器可以執行多個 WebLogic Server 執行個體。 每個 WebLogic Server 的執行個體可能還在 hello 屬於相同的叢集。 請注意，不過，它不目前可能 toouse Azure tooload 平衡的端點公開這類 WebLogic Server 部署中的 hello 相同的虛擬機器，因為 Azure 負載平衡器需要 hello 負載平衡伺服器 toobe 分散唯一的虛擬機器。

## <a name="oracle-jdk-virtual-machine-images"></a>Oracle JDK 虛擬機器映像
* **JDK 6 和 7 最新更新。** 雖然我們建議您使用 hello 最新公用，支援 Java 版本 (目前為 Java 8)，Azure 也提供 JDK 6 和 7 的映像。 這被為了準備 toobe 升級 tooJDK 8 還沒有的舊版應用程式。 雖然更新 tooprevious JDK 映像可能無法再使用 toohello 一般大眾，hello 指定 Oracle、 hello JDK 6 和 7 Azure 所提供的映像與合作關係是的 Microsoft 適合 toocontain 較新的非公用更新通常由所提供Oracle tooonly 選取一種 Oracle 支援的客戶。 Hello JDK 映像的新版本可供一段時間，與更新版本的 JDK 6 和 7。

   hello JDK 用於此 JDK 6 和 7 的映像，並 hello 虛擬機器和映像衍生自，只可以在 Azure 中使用。
* **64 位元 JDK。** hello Oracle WebLogic Server 虛擬機器映像和 Azure 所提供的 hello Oracle JDK 虛擬機器映像包含 hello 64 位元版本的 Windows Server 和 hello JDK。

## <a name="next-steps"></a>後續步驟
您現在已大致了解 Microsoft Azure 上目前的 Oracle 解決方案。 下一步是 toogo 和部署 Azure 中的第一個 Oracle 資料庫。
- 再試一次 hello [Azure 上建立 Oracle 資料庫](oracle-database-quick-create.md)教學課程 tooget 啟動。
