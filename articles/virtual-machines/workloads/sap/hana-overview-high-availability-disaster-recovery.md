---
title: "在 Azure （大型執行個體） 上的 SAP HANA 的 aaaHigh 可用性和災害復原 |Microsoft 文件"
description: "建立高可用性並為 SAP HANA on Azure (大型執行個體) 的災害復原做規劃。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
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
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>SAP Hana (大型執行個體) 在 Azure 上的高可用性和災害復原 

高可用性和災害復原對執行具任務關鍵性的 SAP HANA on Azure (大型執行個體) 伺服器來說，是相當重要的層面。 它的重要 toowork 與 SAP、 系統整合者，或 Microsoft tooproperly 架構設計和實作 hello 右高的可用性/災害復原策略。 它也是重要的 tooconsider hello 復原點目標和復原時間目標，也就是特定 tooyour 環境。

## <a name="high-availability"></a>高可用性

Microsoft 支援 SAP HANA 高可用性方法 「 現成的 hello，"包括：

- **儲存體複寫：** hello 儲存系統的能力 tooreplicate 所有資料 tooanother 位置 (內或分開，都 hello 相同的資料中心)。 SAP HANA 獨立運作，不依賴此方法。
- **HANA 系統複寫：** hello SAP HANA tooa 不同 SAP HANA 系統中的所有資料複寫。 hello 復原時間目標是透過資料複寫的固定間隔最小化。 SAP HANA 支援非同步、 同步在記憶體和同步模式 (僅建議用於 SAP HANA 系統內 hello 相同的資料中心或小於 100 KM 分開的)。 HANA 大型執行個體戳記 hello 目前設計，HANA 系統複寫可用於僅限高可用性。
- **裝載自動容錯移轉：**替代 toosystem 複寫為本機的錯誤復原方案 toouse。 Hello 主要節點無法使用時，會在向外延展模式設定一或多個待命的 SAP HANA 節點和 SAP HANA 自動容錯移轉 tooanother 節點。

如需有關 SAP HANA 高可用性的詳細資訊，請參閱下列 SAP 資訊 hello:

- [SAP HANA 高可用性白皮書](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [SAP HANA 管理指南](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP Academy 的 SAP HANA 系統複寫影片](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP 支援附註 #1999880 - SAP HANA 系統複寫常見問題集](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP 支援附註 #2165547 - SAP HANA 系統複寫環境內的 SAP HANA 備份與還原](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP 支援附註 #1984882 - 使用 SAP HANA 系統複寫以最短/零停機時間的方式進行硬體交換](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>災害復原

在一個地緣政治區域的兩個 Azure 區域中提供 SAP HANA on Azure (大型執行個體)。 介於兩個不同區域的 hello 兩個大型執行個體戳記是嚴重損壞修復期間，複寫資料的直接連線。 hello 複寫 hello 資料是儲存體基礎結構基礎。 依預設不進行 hello 複寫。 它是基於排序 hello 嚴重損壞修復的 hello 客戶組態。 在目前的設計，hello HANA 系統複寫不用於災害復原。

不過，tootake 利用 hello 災害復原時，您需要 toostart toodesign hello 網路連線 toohello 兩個不同的 Azure 地區。 toodo 因此，您需要從內部部署的 Azure ExpressRoute 電路連接您的主要 Azure 地區和在內部部署 tooyour 嚴重損壞修復區域中的另一個循環連接中。 此措施可解決整個 Azure 區域 (包含 Microsoft Enterprise Edge (MSEE) 路由器位置) 發生問題的情況。

做為第二個量值，您可以連接連接 tooSAP HANA Azure （大型執行個體） 上的所有 Azure 虛擬網路中的 hello 區域 tooboth 這些 ExpressRoute 電路的其中一個。 此量值說明的案例，下班，只有其中一個 hello MSEE 位置與 Azure 連線在內部部署位置的地方。

hello 下圖顯示 hello 災害復原的最佳組態：

![災害復原的最佳組態](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

hello 的 hello 網路的災害復原設定的最佳狀況會從內部部署 toohello 兩個不同的 Azure 地區 toohave 兩個 ExpressRoute 電路。 一個循環會 tooregion #1 執行的實際執行個體。 第二個 ExpressRoute 電路 hello 進入 tooregion #2 中，執行某些非生產 HANA 執行個體。 （這是重要事項如果整個 Azure 地區，包括 hello MSEE 和大型執行個體的戳記，會關閉 hello 方格）。

第二個量值為 hello 各種虛擬網路是連線的 toohello 各種連線的 tooSAP HANA Azure （大型執行個體） 上的 ExpressRoute 電路。 我們稍後討論，您可以略過 MSEE 失敗，或您可以降低的嚴重損壞修復的 hello 復原點目標的 hello 位置。

hello 下一個災害復原安裝程式需求如下：

- 在 Azure （大型執行個體） 的相同大小與生產環境的 Sku，並將其部署 hello 嚴重損壞修復區域中的 hello 的 Sku 上的 SAP HANA 都必須排序。 這些執行個體可以使用的 toorun 測試、 沙箱或 QA HANA 執行個體。
- 您必須排序災害復原設定檔針對每個您在 Azure （大型執行個體） 的 Sku 上的 SAP HANA 的 toorecover hello 災害復原站台，如有必要。 這個動作會導致 toohello 配置的存放磁碟區，也就是從您的生產地區到 hello 嚴重損壞修復區域的 hello 儲存體複寫 hello 目標。

符合上述需求的 hello 之後，就有責任 toostart hello 儲存體複寫。 用於在 Azure （大型執行個體） 上的 SAP HANA hello 儲存體基礎結構，在 hello 的儲存體複寫的基礎都是儲存快照集。 toostart hello 災害復原的複寫，您需要 tooperform:

- 開機 LUN 的快照集 (如先前所述)。
- HANA 相關磁碟區的快照集 (如先前所述)。

執行這些快照之後，hello 磁碟區的初始複本是植入 hello 與您 hello 嚴重損壞修復區域中的災害復原設定檔相關聯的磁碟區上。

接著，hello 最新儲存體使用快照集是每小時 hello 存放磁碟區開發的 tooreplicate hello 差異。

hello 達成這項設定的復原點目標是從 60 too90 分鐘的時間。 tooachieve 更佳的復原點目標，在 hello 災害復原情況下，複製 hello HANA 交易記錄備份從 SAP HANA toohello Azure （大型執行個體） 上其他的 Azure 區域。 tooachieve 此復原點目標，執行下列 hello:

1. 備份 hello HANA 交易記錄的頻率儘可能太/hana/記錄檔/備份。
2. 在完成的 tooan Azure 的虛擬機器 (VM)，也就是已連接 toohello SAP HANA Azure （大型執行個體） 的伺服器上的虛擬網路中時，請複製 hello 交易記錄備份。
3. 從該 VM 上，複製到 hello 備份 tooa hello 嚴重損壞修復區域中的虛擬網路中的 VM。
4. 請在 hello VM hello 交易記錄備份。

發生嚴重損壞時，實際的伺服器上部署 hello 災害復原設定檔之後，複製 hello 交易記錄備份從 hello VM toohello Azure （大型執行個體），就是在 hello 嚴重損壞修復區域中，現在 hello 主要伺服器上的 SAP HANA 和還原這些備份。 此復原可能是因為 HANA hello 嚴重損壞修復磁碟上的 hello 狀態是 HANA 快照。 這是 hello 位移進一步的交易記錄備份的還原點。

## <a name="backup-and-restore"></a>備份與還原

其中一個 hello 最重要的層面 toooperating 資料庫確定 hello 資料庫可以保護各種重大事件。 這些事件可以是所造成的任何項目天然災害 toosimple 使用者錯誤。

將資料庫備份，與 hello 能力 toorestore 它 tooany 點的時間 (例如有人已刪除的重要資料之前)，可讓還原 tooa 狀態可盡量 toohello 當時的 hello 中斷發生之前。

必須執行兩種類型的備份，才能獲得最佳結果：

- 資料庫備份
- 交易記錄備份

除了執行的應用程式層級 toofull 資料庫備份，您可以更徹底執行與儲存快照集備份。 執行記錄備份也是很重要的還原 hello 資料庫 （和 tooempty hello 已認可的交易記錄檔）。

SAP HANA on Azure (大型執行個體) 提供兩個備份和還原選項：

- 自己動手做 (DIY)。 計算 tooensure 足夠的磁碟空間後，請使用磁碟備份方法 （toothose 磁碟） 以執行完整的資料庫和記錄備份。 經過一段時間，hello 備份複製的 tooan （之後您將幾乎不受限制的儲存體與 Azure 為基礎的檔案伺服器設定） 的 Azure 儲存體帳戶，或使用 Azure 備份保存庫或 Azure 冷儲存體。 另一個選項是 toouse 第三方資料保護工具，例如 Commvault，toostore hello 備份之後複製 tooa 儲存體帳戶。 hello DIY 備份的選項也可能需要將需要 toobe 較長的時間規範和稽核用途所儲存的資料。
- 使用 hello 備份和還原 hello Azure （大型執行個體） 上的 SAP HANA 的基礎結構的功能提供。 此選項，可滿足 hello 需要進行備份，而它會使得手動備份幾乎過時 （除了備份資料是為了相容性用途）。 本章節將說明 hello 其餘 hello 備份和還原 HANA （大型執行個體） 提供的功能。

> [!NOTE]
> hello 快照集技術，可由 hello 的 HANA （大型執行個體） 的基礎結構會相依於 SAP HANA 快照集。 SAP HANA 快照集無法搭配 SAP HANA 多租用戶資料庫容器一起使用。 如此一來，這種備份方法不能使用的 toodeploy SAP HANA 多租用戶資料庫容器。

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>使用 SAP HANA on Azure (大型執行個體) 的儲存體快照集

hello 基礎 Azure （大型執行個體） 上的 SAP HANA 的儲存體基礎結構支援儲存體的快照集磁碟區的 hello 的概念。 備份和還原的特定磁碟區支援，以 hello 下列考量：

- 系統會經常建立存放磁碟區快照，而不是進行資料庫備份。
- hello 儲存快照集執行 hello 儲存快照集之前，會起始 SAP HANA 快照集。 此 SAP HANA 快照之後復原 hello 儲存快照集的最後記錄還原的 hello 安裝點。
- 在 hello hello 儲存快照集已順利執行的時間點，則刪除 hello SAP HANA 快照集。
- 經常建立記錄備份，並儲存在 hello 記錄備份的磁碟區，或在 Azure 中。
- 如果必須還原 hello 資料庫 tooa 特定時間點，提出要求 Azure 服務管理 toorestore tooa tooMicrosoft Azure 支援 （實際執行中斷的狀況） 或 SAP HANA 特定儲存體快照集 （例如，規劃還原的沙箱系統tooits 原始狀態）。
- hello SAP HANA 快照集包含在 hello 儲存快照集是套用記錄備份已執行並儲存製作 hello 儲存快照集之後的位移的點。
- 這些記錄備份 toorestore hello 資料庫回復 tooa 特定時間點。

指定 hello 備份\_名稱建立快照的下列磁碟區的 hello:

- hana/data
- hana/log
- hana/log\_backup (以備份形式掛接到 hana/log 中)
- hana/shared

### <a name="storage-snapshot-considerations"></a>儲存體快照考量事項

>[!NOTE]
>儲存體快照集「不是」免費提供的功能，因為必須配置額外的儲存空間。

hello 的儲存體 Azure （大型執行個體） 上的 SAP HANA 的快照集的特定技巧包括：

- 特定的儲存體快照集 （在 hello 當它拍攝的時間點） 會耗用很少的儲存體。
- 為資料內容變更 hello hello 存放磁碟區的檔案變更的 SAP HANA 資料內容，hello 快照需要 toostore hello 原始區塊內容。
- hello 儲存快照集的大小會增加。 hello 長 hello 快照集存在，會變成 hello 較大 hello 儲存快照集。
- hello hello 存留期的儲存體的快照集的多個所做的變更 toohello SAP HANA 資料庫磁碟區，會變成 hello 較大 hello 空間耗用量的 hello 儲存快照集。

在 Azure （大型執行個體） 上的 SAP HANA 隨附 hello SAP HANA 資料和記錄磁碟區的固定磁碟區大小。 執行這些磁碟區的快照會吞掉的磁碟區空間中，所以您必須負責 tooschedule 存放裝置內的快照集 （hello SAP HANA Azure [大型執行個體] 處理序上)。

hello 下列各節提供資訊來執行這些快照集，包括一般建議：

- 雖然 hello 硬體可承受 255 的快照集，每個磁碟區，我們強烈建議您維持低於這個數字。
- 執行儲存體快照集之前，請監視並追蹤可用空間。
- 較低 hello 儲存快照集數目取決於可用的空間。 您可能需要的保留，快照集 toolower hello 數目，或者您可能需要 tooextend hello 磁碟區。 (您可以訂購額外的儲存空間，以 1-TB 為單位)。
- 在進行活動的期間，例如使用系統移轉工具 (使用 R3load) 將資料移到 SAP HANA (或是從備份還原 SAP HANA 資料庫)，強烈建議您不要執行任何儲存體快照集  （如果新的 SAP HANA 系統上執行系統移轉，儲存快照集不需要執行 toobe。）
- 在進行較大規模的 SAP HANA 資料表重組期間，應儘可能避免執行儲存體快照。
- 儲存體的快照集是在 Azure （大型執行個體） 上的 SAP HANA 必要條件 tooengaging hello 災害復原功能。

### <a name="setting-up-storage-snapshots"></a>設定儲存體快照

1. 請確定 Perl 會安裝在 hello Linux 伺服器上作業系統 hello HANA （大型執行個體）。
2. 修改 /etc/hosts ssh/ssh\_config tooadd hello 列_Mac hmac sha1_。
3. 建立 hello 每個 SAP HANA 執行個體 （如果適用） 執行您的主要節點上的 SAP HANA 備份使用者帳戶。
4. SAP HANA （大型執行個體） 的所有伺服器上必須安裝 hello SAP HANA HDB 用戶端。
5. Hello 第一個 SAP HANA （大型執行個體） 伺服器上的每個區域，公開金鑰必須建立 tooaccess hello 基礎控制快照集建立的儲存體基礎結構。
6. 將 azure 的 hello 指令碼複製\_hana\_從 /scripts toohello 位置 backup.pl **hdbsql** hello SAP HANA 安裝。
7. 複製 hello HANABackupDetails.txt 檔案從 /scripts toohello 相同 hello Perl 指令碼的位置。
8. 修改視 hello 適當客戶規格 hello HANABackupDetails.txt 檔案。

### <a name="step-1-install-sap-hana-hdbclient"></a>步驟 1：安裝 SAP HANA HDBClient

hello Linux 安裝在 Azure （大型執行個體） 上的 SAP HANA 包括 hello 資料夾和指令碼進行備份和災害復原的必要 tooexecute SAP HANA 儲存快照集。 不過，它是您的責任 tooinstall SAP HANA HDBclient 安裝 SAP HANA 時。 （hello HDBclient 和 SAP HANA 都不會安裝 Microsoft）。

### <a name="step-2-change-etcsshsshconfig"></a>步驟 2：變更 /etc/ssh/ssh\_config

在 /etc/ssh/ssh\_config 中新增 _MACs hmac-sha1_ 這一行，如下所示：
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>步驟 3︰建立公開金鑰

Hello 上每個 Azure 區域，在 Azure （大型執行個體） 伺服器上的第一個 SAP HANA 建立使用公用金鑰 toobe tooaccess hello 儲存體基礎結構，讓您可以建立快照集。 密碼不需要的 toosign toohello 儲存體中，而且不會保留密碼認證，可確保 hello 公開金鑰。 在 Linux hello SAP HANA （大型執行個體） 伺服器上，執行下列命令 toogenerate hello 公開金鑰 hello:
```
  ssh-keygen –t dsa –b 1024
```
hello 新的位置是 _/root/.ssh/id\_dsa.pub。 請勿輸入實際的複雜密碼，否則您將會需要的 tooenter hello 複雜密碼每次您登入。 反之，請按**Enter**兩次 tooremove hello 輸入複雜密碼來登入的需求。

請確定該 hello 公開金鑰已更正依照預期方式變更 too/root/.ssh/ 資料夾，然後再執行 hello toomake **ls**命令。 如果 hello 機碼存在，您可以將它複製藉由執行下列命令的 hello:

![執行此命令即可複製公開金鑰](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

此時，請連絡 Azure 服務管理上的 SAP HANA，並提供 hello 金鑰。 hello 服務代表通話，會使用 hello 公用金鑰 tooregister hello 基礎儲存體基礎結構中。

### <a name="step-4-create-an-sap-hana-user-account"></a>步驟 4：建立 SAP HANA 使用者帳戶

在 SAP HANA Studio 中建立 SAP HANA 使用者帳戶以供備份使用。 此帳戶必須具有下列權限的 hello:_備份管理員_和_目錄讀取_。 在此範例中，建立 SCADMIN hello 使用者名稱。

![在 HANA Studio 中建立使用者](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>步驟 5： 授權 hello SAP HANA 使用者帳戶

授權 hello SAP HANA 使用者帳戶 (toobe hello 指令碼使用而不需要授權，每次執行 hello 指令碼時)。 hello SAP HANA 命令`hdbuserstore`允許 hello SAP HANA 使用者金鑰，並儲存在一個或多個 SAP HANA 節點上建立。 hello 使用者金鑰也允許 hello 使用者 tooaccess SAP HANA，而不需要將密碼從 toomanage 內 hello 指令碼處理程序，稍後再討論。

>[!IMPORTANT]
>執行 hello 下列命令為`_root_`。 否則，hello 指令碼無法正常運作。

輸入 hello`hdbuserstore`命令，如下所示：

![輸入 hello hdbuserstore 命令](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

在下列的範例，其中 hello 使用者 SCADMIN01，hello 的主機名稱是 lhanad01 hello hello 命令為：
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
針對相應放大 HANA 執行個體，從單一伺服器管理所有指令碼處理。 在此範例中，必須為每個主機會反映為相關的 toohello 鍵 hello 主機的方式改變 hello SAP HANA 金鑰 SCADMIN01。 SAP HANA 備份帳戶 hello 與 hello HANA DB hello 執行個體數目的修改也就是**lhanad**。 hello 金鑰必須 hello 分派它的主機上具有系統管理權限，並向外延展的 hello 備份使用者必須具有存取權限 tooall SAP HANA 的執行個體。
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>步驟 6: Hello /scripts 資料夾複製項目

複製 hello 下列項目從 hello/指令碼資料夾 （包含在 hello 安裝的 hello 黃金映像） toohello 工作目錄**hdbsql**。 就目前的 HANA 安裝而言，這個目錄是 /hana/shared/D01/exe/linuxx86\_64/hdb。
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
複製下列項目，若其執行向外延展的 hello 或 OLAP:
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
hello HANABackupCustomerDetails.txt 檔案是可修改的向上延展部署，如下所示。 這是執行 hello 儲存快照集的 hello 指令碼的 hello 控制項和組態檔案。 您應該會收到 hello_儲存體的備份名稱_和_存放裝置的 IP 位址_從 Azure 服務管理時部署您的執行個體上的 SAP HANA。 您無法修改 hello 順序排序，或無法正常執行的任何 hello 變數或 hello 指令碼的間距。

向上延展部署，hello 組態檔應該像這樣：
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
針對向外延展組態，hello HANABackupCustomerDetailsBW.txt 檔案應該像這樣：
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>目前，只有在節點 1 詳細資料會用於 hello 實際 HANA 儲存快照集指令碼。 我們建議您測試存取 tooor HANA 所有的節點，使 hello 主要備份節點變更，如果您已經可藉任何其他節點，可以修改節點 1 中的 hello 詳細資料來取代它的位置。

toocheck hello 設定檔或適當的連線能力 toohello HANA 執行個體，執行下列指令碼的 hello hello 正確設定：
- 如果是相應增加組態 (與 SAP 工作負載無關)︰

 ```
testHANAConnection.pl
```
- 如果是相應放大組態：

 ```
testHANAConnectionBW.pl
```

請確定該 hello 主要 HANA 執行個體都有存取必要的 tooall HANA 伺服器。 沒有任何參數 toohello 指令碼，但您必須先完成 hello 適當 HANABackupCustomerDetails / HANABackupCustomerDetailsBW 檔案的 hello 指令碼 toorun 正確。 只有 hello 殼層命令會傳回錯誤碼，因為它不可能的 hello 指令碼 tooerror 核取每個執行個體。 即便如此，hello 指令碼並提供您 toodouble 檢查一些很有幫助的註解。

toorun hello 指令碼：
```
 ./testHANAConnection.pl
```
 如果 hello 指令碼已成功取得 hello hello HANA 執行個體的狀態，它會顯示 hello HANA 連線成功的訊息。

此外，還有第二個類型的指令碼可以使用 toocheck hello 主要 HANA server 執行個體的能力 toosign toohello 儲存體中。 在執行 hello azure 之前\_hana\_備份 (\_bw).pl 指令碼，您必須執行 hello 下一個指令碼。 如果磁碟區不包含任何快照集，則不可能 toodetermine 是否 hello 磁碟區是只是空的或沒有 ssh 失敗 tooobtain hello 快照詳細資料。 基於這個理由，hello 指令碼會執行兩個步驟：

- 它會驗證該 hello 儲存主控台是可存取。
- 依 HANA 執行個體，為每個磁碟區建立測試 (或虛設) 快照集。

基於這個理由，hello HANA 執行個體隨附做為引數。 同樣地，不可能 tooprovide 錯誤檢查 hello 儲存體連線，但是 hello 指令碼提供有用的提示，如果 hello 執行作業失敗。

hello 指令碼是以執行：
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
或執行為︰
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
hello 指令碼也會顯示訊息指出您無法 toosign 適當 tooyour 部署儲存體租用戶中，其組織方式周圍 hello 邏輯單元編號 (Lun)，可供您擁有 hello 伺服器執行個體。

執行 hello 第一個儲存體的快照集為基礎的備份之前，先執行 hello 下一個指令碼 toomake 該 hello 組態正確。

執行這些指令碼之後, 您可以藉由執行刪除 hello 快照集：
```
./removeTestStorageSnapshot.pl <hana instance>
```
或
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>步驟 7：執行隨選快照集

執行隨選快照集 (以及使用 cron 來排程一般快照集） 如下所示。

向上延展的組態，執行下列指令碼的 hello:
```
./azure_hana_backup.pl lhanad01 customer 20
```
對於向外延展組態，執行下列指令碼的 hello:
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
hello 向外延展指令碼會確定可存取所有 HANA 伺服器，且所有 HANA 執行個體都傳回適當的狀態，再繼續建立 SAP HANA 或儲存體的快照集的 hello 執行個體的一些額外檢查 toomake。

hello 下列引數是必要的：

- hello HANA 執行個體需要備份。
- hello hello 儲存快照集的快照集前置詞。
- hello hello 特定前置詞保留的快照集 toobe 數目。

```
./azure_hana_backup.pl lhanad01 customer 20
```

hello 執行 hello 指令碼會在這三個不同的階段建立 hello 儲存快照集：

- 執行 HANA 快照。
- 執行儲存體快照。
- 移除 hello HANA 快照集。

藉由呼叫 hello HDB 可執行檔之資料夾中將它複製到執行 hello 指令碼。 它將備份至少 hello 下列磁碟區，但它也會在 hello 磁碟區名稱中有 hello 明確 SAP HANA 執行個體名稱的任何磁碟區備份。
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
hello 保留期限是嚴格管理，快照集時，您執行 hello 指令碼 （例如 20，先前所示)，做為參數提交的 hello 數目。 因此 hello 一段時間是 hello 段 hello 呼叫 hello 指令碼中的快照集的執行與 hello 數目的函式。 如果保留的快照集的 hello 數目超過 hello 數字會命名為 hello 呼叫 hello 指令碼中的參數，hello 此標籤的最舊的儲存體快照集 (在上一個案例中，_自訂_) 刪除新的快照集之前執行。 這表示您提供為 hello hello 呼叫的最後一個參數是您可以使用快照集 toocontrol hello 數目 hello 數目 hello 數目。

>[!NOTE]
>只要您變更 hello 標籤時，計算 hello 再次啟動。

您需要 tooinclude hello HANA 執行個體名稱所提供的 Azure 服務管理上的 SAP HANA 做為引數如果它們在多節點的環境中建立快照集。 單一節點在環境中，Azure （大型執行個體） 單位上的 SAP HANA hello hello 名稱即已足夠，但仍建議 hello HANA 執行個體名稱。

此外，您可以備份使用的開機 volumes\LUNs hello 相同指令碼。 第一次執行 HANA 時，您必須至少備份開機磁碟區一次，但建議以 cron 進行每週或每晚開機備份排程。 不用新增的 SAP HANA 的執行個體名稱，而是插入_開機_，如下所示為 hello 指令碼 hello 引數為：
```
./azure_hana_backup boot customer 20
```
hello 相同保留原則是可以用 toohello 開機磁碟。 使用視快照集，做為描述之前，針對某些特殊情況下，例如 SAP 的增強功能 (EHP) 在封裝升級期間，或當您需要 toocreate 相異儲存體的快照集。

我們建議您排定 tooperform 儲存快照集使用 cron，並建議您針對所有的備份和災害復原需求 (修改 hello 指令碼輸入 toomatch hello 各種要求備份時間) 使用相同指令碼的 hello。 這些在 cron 中都會根據其執行時間以不同方式排定：每小時、12 小時、每天或每週。 hello cron 排程是設計的 toocreate 儲存快照集符合先前所討論的 hello 進行長期離站備份的保留標記。 hello 指令碼包含所有的實際執行磁碟區，根據其要求的頻率 （資料和記錄檔備份每小時、 每天備份 hello 開機磁碟區而） 命令 tooback。

hello hello 遵循 cron 指令碼中的項目執行的每個小時 hello 十分鐘，每隔 12 小時在 hello 十分鐘，和每日 hello 十分鐘。 作業會在這種方式建立 hello cron 只有一個 SAP HANA 儲存快照集期間會進行任何特定的小時，以便 hello 每小時和每日備份不會發生在 hello 相同的時間 （上午 12:10）。 toohelp 最佳化您的建立快照集和複寫，並在 Azure 服務管理上的 SAP HANA 提供 hello 建議您 toorun 時間備份。

排程中 /etc/crontab hello 預設 cron 如下所示：
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
在前述 cron 指示 hello，hello HANA 磁碟區 （不含開機磁碟區） 會取得快照集與 hello 標籤以每小時。 在這些快照中，會保留 66 個。 此外，會保留 14 的快照集與 hello 12 小時制的標籤。 您可能取得三天的每小時快照集，加上另外四天的 12 小時快照集，您就有整週的快照集。

Cron 內排程可能很困難，因為只有一個指令碼應該執行任何特定時間，除非 hello 指令碼會交錯的幾分鐘的時間。 如果您想要每日備份長期保存，12 小時制快照集 （具有保留的計數七個每個），以及保留每日快照集，或 hello 每小時的快照集是交錯的 tootake 位置 10 分鐘後。 只有一個每日快照集都會保存在 hello 實際磁碟區。
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
此處所列的 hello 頻率僅為範例。 tooderive 您最佳的數目快照集，使用下列準則的 hello:

- 時間點復原的復原時間目標中的需求。
- 空間使用量。
- 潛在災害復原的復原點目標和復原時間目標中的需求。
- 對磁碟執行的最終 HANA 完整資料庫備份。 只要磁碟上，針對完整資料庫備份或_backint_介面，是執行，hello 儲存快照集執行作業失敗。 如果您計劃 tooexecute 之上儲存快照集的完整資料庫備份，請確定在這段期間已停用的儲存體的快照集的 hello 執行。

>[!IMPORTANT]
> 只有在搭配 SAP HANA 記錄備份執行 hello 快照集時 hello 使用 SAP HANA 備份儲存體的快照集無效。 這些記錄備份需要 toobe 無法 toocover hello hello 儲存體快照之間的時間週期。 如果您已經設定承諾 toousers 的 30 天的時間點復原，您需要下列 hello:

- 能力 tooaccess 是 30 天的儲存體快照集。
- 透過 hello 過去 30 天內的連續記錄備份。

在 hello 範圍中的記錄檔備份，建立以及 hello 備份記錄檔磁碟區的快照。 不過，是確定 tooperform 定期記錄備份，讓您可以：

- Hello 連續記錄備份，需要 tooperform 時間點復原。
- 防止 hello SAP HANA 記錄磁碟區空間用盡。

其中一個 hello 最後幾個步驟是在 SAP HANA Studio tooschedule SAP HANA 備份記錄。 hello SAP HANA 備份記錄檔目標目的地是特別建立的 hello hana/記錄檔\_/hana/log/backups hello 掛接點的備份磁碟區。

![在 SAP HANA Studio 中排定 SAP HANA 備份記錄](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

您可以選擇比每隔 15 分鐘更頻繁的備份。 有些使用者甚至每分鐘都執行記錄備份，但我們不建議「超過」15 分鐘。

hello 最後一個步驟是以檔案為基礎的 tooperform （hello 初始安裝後的 SAP HANA） 備份 toocreate 必須存在於 hello 備份類別目錄的單一備份項目。 否則，SAP HANA 無法起始您指定的記錄備份。

![請以檔案為基礎的備份 toocreate 單一備份項目](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>監視 hello 數目和大小的 hello 磁碟區上的快照集

在特定的存放磁碟區，您可以監視 hello 快照集和 hello 存放裝置耗用量的快照集數目。 hello`ls`命令不會顯示 hello 快照集目錄或檔案。 不過，hello Linux 作業系統命令`du`用途，下列命令的 hello:

- `du –sh .snapshot`提供所有快照集內 hello 快照集目錄的總計。
- `du –sh --max-depth=1`列出所有儲存在 hello.snapshot 資料夾和 hello 每個快照集大小的快照集。
- `du –hc`提供所有快照集所使用的 hello 總大小。

使用這些命令 toomake 確定 hello 拍攝且儲存的快照集不會耗用 hello 磁碟區上的所有 hello 存放裝置。

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>減少伺服器上的快照集的 hello 數目

如前所述，您可以減少 hello 數目的快照集儲存特定標籤。 hello 最後一個 tooretain hello 命令 tooinitiate 快照集是您想要的快照集標籤和 hello 數目的兩個參數。
```
./azure_hana_backup.pl lhanad01 customer 20
```
Hello 上述範例中，在 hello 快照標籤是_客戶_而且 hello 數目快照集與保留此標籤 toobe _20_。 當您回應 toodisk 空間耗用量，您可能想 tooreduce hello 數量的預存的快照集。 hello tooreduce hello 數目的快照集是 toorun hello 指令碼，最後一個參數集 too5 hello 與簡單的方法：
```
./azure_hana_backup.pl lhanad01 customer 5
```
執行 hello 指令碼可使用這項設定，因為快照集，包括快照集，hello 新儲存體的 hello 數目了_5_。

 >[!NOTE]
 > 只有 hello 最新的上一個快照是超過 1 小時前，此指令碼就會減少 hello 快照集數目。 hello 指令碼不會刪除少於 1 小時前的快照集。

這些限制會提供相關的 toohello 選擇性的災害復原功能。

如果您不想再 toomaintain 一組前置詞開頭的快照集，您可以執行與 hello 指令碼_0_為 hello 保留編號 tooremove 比對該前置詞的所有快照集。 不過，移除所有的快照集可能會影響 hello 災害復原功能。

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>復原 toohello 最近 HANA 快照集

Hello 事件中可以為 Azure 服務管理上的 SAP HANA 客戶事件起始您遇到下實際執行案例、 復原從儲存體的快照集的 「 hello 」 程序。 如果實際執行系統和 hello 唯一方式 tooretrieve hello 資料是 toorestore hello 生產資料庫中已刪除資料這類的未預期的案例可能高急迫性內容。

在 hello 相反地，時間點復原可能是低急迫性，天事先計劃。 您可以使用「SAP HANA on Azure 服務管理」來規劃此復原，以避免引發高優先性的問題。 例如，您可能會藉由套用新的增強功能套件，而且您規劃 tootry hello SAP 軟體升級，然後需要 toorevert 回 tooa 快照集，表示 hello hello EHP 升級前的狀態。

發出 hello 要求之前，您需要 toodo 一些準備工作。 Azure 服務管理小組的 SAP HANA 可以然後處理 hello 要求，並提供 hello 還原磁碟區。 之後，它是 tooyou toorestore hello HANA 資料庫依據 hello 快照集。 以下是如何 hello tooprepare 要求：

>[!NOTE]
>下列螢幕擷取畫面，根據您使用的 SAP HANA 發行 hello hello 使用者介面可能會有所不同。

1. 決定哪些快照 toorestore。 只有 hello hana/資料磁碟區可以回復，除非所指示。

2. 關閉 hello HANA 執行個體。

 ![關閉 hello HANA 執行個體](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. 卸載 hello 資料磁碟區上的每個 HANA 資料庫節點。 無法卸載 hello 資料磁碟區時，就會失敗 hello hello 快照集還原。

 ![卸載 hello 資料磁碟區上每個 HANA 資料庫 節點](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. 開啟 Azure 支援人員要求 tooinstruct hello 還原的特定快照集。

 - Hello 還原期間： Azure 服務管理上的 SAP HANA 可能會要求您 tooattend 沒有資料會迷失方向電話會議 tooensure。

 - Hello 還原後： hello 儲存體快照還原時 Azure 服務管理上的 SAP HANA 通知您。

5. Hello 還原程序完成之後，重新掛接所有資料磁碟區。

 ![重新掛接所有資料磁碟區](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. 如果它們沒有自動顯示當您重新連接到 SAP HANA Studio tooHANA DB，請選取 SAP HANA Studio 中的復原選項。 hello 下列範例顯示還原 toohello 最後 HANA 快照集。 儲存體的快照集嵌入一個 HANA 快照集，且如果您要還原 toohello 最新的儲存體快照集，應 hello 最近 HANA 快照集。 (如果您要還原 tooolder 儲存快照集，您需要 toolocate hello HANA 根據 hello 時間 hello 儲存快照集的快照。)

 ![選取 SAP HANA Studio 內的復原選項](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. 選取**復原 hello 資料庫 tooa 特定資料備份或儲存體快照集**。

 ![hello [指定復原類型] 視窗](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. 選取 [指定不含目錄的備份]。

 ![hello [指定備份位置] 視窗](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. 在 hello**目的型別**清單中，選取**快照**。

 ![hello 」 指定 hello 備份 tooRecover 」 視窗](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. 按一下**完成**toostart hello 復原程序。

 ![按一下 [完成] 的 toostart hello 復原程序](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. hello HANA 資料庫還原並復原 toohello HANA 快照集包含在 hello 儲存快照集。

 ![HANA 資料庫會還原並復原 toohello HANA 快照集](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>復原 toohello 最新狀態

hello 下列程序還原 hello HANA 快照集包含在 hello 儲存快照集。 然後會還原 hello 儲存快照集之前先還原 hello 交易記錄備份 toohello 最近 hello 資料庫狀態。

>[!IMPORTANT]
>繼續進行之前，請先確定您擁有一串完整且連續的交易記錄備份。 沒有這些備份，您無法還原 hello hello 資料庫目前狀態。

1. 完成步驟 1-6 的 hello 前面程序在 「 正在復原 toohello 最近 HANA 快照集。 」

2. 選取**復原 hello 資料庫 tooits 最新狀態**。

 ![選取 「 Recover hello 資料庫 tooits 最新狀態 」](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. 指定 hello hello 最近 HANA 記錄備份的位置。 hello 位置需要 toocontain 所有 HANA 交易記錄備份，從 hello HANA 快照 toohello 最新狀態。

 ![指定 hello hello 最近 HANA 記錄備份的位置](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. 選取的備份當做基底從哪一個 toorecover hello 資料庫。 在本例中，這是隨附在 hello 儲存快照集的 hello HANA 快照集。 （只有一個快照集被列在下列螢幕擷取畫面的 hello）。

 ![選取的備份當做基底從哪一個 toorecover hello 資料庫](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. 清除 hello**使用差異備份**核取方塊，當 hello hello HANA 快照集時間 hello 最新狀態之間沒有差異。

 ![如果沒有差異存在清除 hello < 使用差異備份 」 核取方塊](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. 在 hello 摘要畫面中，按一下 **完成**toostart hello 還原程序。

 ![Hello 摘要畫面上，按一下 [完成]](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>復原時間 tooanother 點
toorecover tooa hello HANA 快照集 （包含在 hello 儲存快照集） 之間，則晚於 hello HANA 快照集時間點復原的時間點 hello 遵循：

1. 請確定您有從您想要 toorecover hello HANA 快照集 toohello 時間的所有交易記錄備份。
2. 開始 hello 程序在 「 正在復原 toohello 最新狀態。 」
3. 在步驟 2 中 hello hello 程序，**指定復原類型**視窗中，選取**時間點復原 hello 資料庫 toohello 下列**，指定的時間，hello 點，然後完成 步驟 3 到 6。

## <a name="monitoring-hello-execution-of-snapshots"></a>監視 hello 執行快照集

您需要儲存體的快照集 toomonitor hello 的執行。 hello 指令碼執行的儲存體快照集將寫入輸出 tooa 檔案，然後將它儲存 toohello hello Perl 指令碼相同的位置。 針對每個快照都會寫入一個個別的檔案。 每個檔案的 hello 輸出會清楚地顯示 hello hello 快照集指令碼執行的各階段：

- 尋找需要 toocreate hello 磁碟區快照集
- 尋找 hello 取自這些磁碟區的快照集
- 刪除最終現有快照集 toomatch hello 的快照集數目指定
- 建立 HANA 快照集
- Hello 磁碟區上建立 hello 儲存快照集
- 刪除 hello HANA 快照集
- 重新命名 hello 最新快照集太**.0**

這是最重要的部分 hello hello 指令碼：
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
您可以看到與此範例如何 hello 指令碼記錄 hello hello HANA 快照集建立。 在 hello 向外延展的情況下，此程序被起始 hello 主要節點上。 hello 主要節點會起始 hello 同步建立 hello 快照集，每個 hello 背景工作節點上。 然後會採取 hello 儲存快照集。 Hello 成功執行之後 hello 儲存快照集，會刪除 hello HANA 快照集。
