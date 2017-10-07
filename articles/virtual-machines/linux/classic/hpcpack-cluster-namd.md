---
title: "使用 Linux Vm 上的 Microsoft HPC Pack aaaNAMD |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並執行在多個 Linux 運算節點上具有 charmrun 的 NAMD 模擬"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD
本文章將示範其中一種方式 toorun Linux 高效能運算 (HPC) 工作負載在 Azure 虛擬機器上。 在這裡，您將設定[Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)叢集在 Azure 上使用 Linux 計算節點，並執行[NAMD](http://www.ks.uiuc.edu/Research/namd/)模擬 toocalculate 和視覺化大型 biomolecular 系統 hello 結構。  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** （適用於 Nanoscale 屬於分子 Dynamics 程式） 專為高效能模擬大型 biomolecular 系統的設計平行屬於分子 dynamics 封裝包含的原子 toomillions 組成。 這些系統的範例包括病毒、儲存格結構和大型蛋白質。 NAMD 縮放 toohundreds 的典型的模擬和 toomore 比的 hello 最大模擬 500,000 個核心的核心。
* **Microsoft HPC Pack**提供功能 toorun 大規模 HPC 和內部部署電腦或 Azure 虛擬機器在叢集中的平行應用程式。 HPC Pack 的開發前身為 Windows HPC 工作負載的解決方案，其現已支援於部署在 HPC Pack 叢集中的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。 如需簡介，請參閱 [在 Azure 的 HPC Pack 叢集中開始使用 Linux 運算節點](hpcpack-cluster.md) 。

針對其他選項 toorun Linux HPC 工作負載在 Azure 中，請參閱[技術資源，批次和高效能運算](../../../batch/batch-hpc-solutions.md)。

## <a name="prerequisites"></a>必要條件
* **具備 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，在 Azure 上部署具備 Linux 計算節點的 HPC Pack 叢集。 請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)hello 必要條件和步驟，針對任何一個選項。 如果您選擇 hello PowerShell 指令碼部署選項，請參閱這篇文章 hello 結尾 hello 範例檔案中的 hello 範例組態檔。 此檔案會設定 Windows Server 2012 R2 的前端節點和四個大型 CentOS 6.6 計算節點組成之以 Azure 為基礎的 HPC Pack 叢集。 請視環境需要自訂此檔案。
* **NAMD 軟體和教學課程檔案**-適用於 Linux 下載 NAMD 軟體 hello [NAMD](http://www.ks.uiuc.edu/Research/namd/)站台 （需要註冊）。 這篇文章根據 NAMD 版本 2.10，並使用 hello [Linux x86_64 (64 位元 Intel/AMD 使用乙太網路)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310)封存。 也下載 hello [NAMD 教學課程檔案](http://www.ks.uiuc.edu/Training/Tutorials/#namd)。 hello 下載包括.tar 檔案，而您需要在 hello 叢集前端節點上的 Windows 工具 tooextract hello 檔案。 tooextract hello 檔案，請遵循本文中稍後的 hello 指示。 
* **VMD** （選用）-toosee hello 結果 NAMD 工作，下載並安裝 hello 屬於分子視覺效果程式[VMD](http://www.ks.uiuc.edu/Research/vmd/)您選擇的電腦上。 hello 目前版本是 1.9.2。 請參閱的 hello VMD 下載網站 tooget 啟動。  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>設定運算節點之間的相互信任
多個 Linux 節點上執行跨節點的作業需要 hello 節點 tootrust 彼此 (由**rsh**或**ssh**)。 當您建立 hello HPC Pack 叢集以 hello Microsoft HPC Pack IaaS 部署指令碼時，hello 指令碼會自動設定您指定的 hello 系統管理員帳戶的永久相互信任。 Hello 叢集的網域中建立的非管理員使用者，您必須 tooset 暫存 hello 節點間的相互信任工作配置 toothem 時。 Hello 作業完成之後，然後摧毀 hello 關聯性。 toodo 這每位使用者提供的 RSA 金鑰組 toohello 叢集的 HPC Pack 會使用 tooestablish hello 信任關係。 指示如下。

### <a name="generate-an-rsa-key-pair"></a>產生 RSA 金鑰組
這是簡單 toogenerate RSA 金鑰組，其中包含公開金鑰和私密金鑰，藉由執行 hello Linux**透過像是**命令。

1. 登入 tooa Linux 電腦。
2. 執行下列命令的 hello:
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > 按**Enter** hello 命令完成之前 toouse hello 預設設定。 請勿在這裡輸入複雜密碼；當系統提示您輸入密碼時，只要按 **Enter**鍵。
   > 
   > 
   
   ![產生 RSA 金鑰組][keygen]
3. 變更目錄 toohello ~/.ssh 目錄。 hello 私密金鑰會儲存在 id_rsa 和 hello id_rsa.pub 中的公用金鑰。
   
   ![私密和公開金鑰][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>新增 hello 金鑰組 toohello HPC Pack 叢集
1. [遠端桌面連線](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toohello 前端節點 VM 使用 hello 時部署 hello 叢集 (例如，hpc\clusteradmin) 所提供的網域認證。 您可以管理 hello 叢集從 hello 前端節點。
2. Hello 叢集的 Active Directory 網域中使用標準的 Windows Server 程序 toocreate 網域使用者帳戶。 例如，使用 hello Active Directory 使用者和電腦 工具 hello 前端節點上。 本文中的 hello 範例假設您建立名為 hpcuser hello hpclab 網域 (hpclab\hpcuser) 中的網域使用者。
3. 將 hello 網域使用者 toohello HPC Pack 叢集新增為叢集使用者。 如需指示，請參閱 [(Add or Remove Cluster Users) 新增或移除叢集使用者](https://technet.microsoft.com/library/ff919330.aspx)。
4. 建立具名 C:\cred.xml 和複製 hello RSA 索引鍵資料的檔案。 您可以找到範例在 hello hello 本文結尾處的範例檔案。
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. 開啟命令提示字元並輸入下列命令 tooset hello 認證 hello hpclab\hpcuser 帳戶資料的 hello。 使用 hello **x**參數 toopass hello hello C:\cred.xml 檔案名稱建立 hello 索引鍵的資料。
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   這個命令會成功完成而沒有輸出。 設定 hello hello 需要 toorun 作業的使用者帳戶的認證之後, hello cred.xml 檔儲存在安全的位置，或將它刪除。
6. 如果您在其中 Linux 節點上產生 hello RSA 金鑰組，請記得 toodelete hello 索引鍵使用它們完畢之後。 如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，則它不會設定相互信任。

> [!IMPORTANT]
> 我們不建議叢集系統管理員身分執行 Linux 作業上共用的叢集，因為系統管理員所提交的工作是 hello 根帳號底下執行 hello Linux 節點上。 非系統管理員使用者所提交的工作會以 hello 作業的使用者名稱相同的 hello 與執行本機 Linux 使用者帳戶。 在此情況下，HPC Pack 會相互信任此 Linux 使用者的所有 hello 節點配置 toohello 作業。 您可以設定 hello Linux 使用者 hello Linux 節點上手動執行 hello 作業之前或 HPC Pack hello 使用者會自動建立時送出 hello 作業。 如果 HPC Pack 建立 hello 使用者，HPC Pack hello 作業完成之後刪除它。 hello hello 節點上的 hello 作業完成之後，會移除金鑰 tooreduce 安全性威脅。
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>為 Linux 節點設定檔案共用
現在設定 SMB 檔案共用，然後掛接 hello 的所有 Linux 節點 tooallow hello Linux 節點 tooaccess NAMD 檔案的一般路徑上的共用的資料夾。 以下是步驟 toomount hello 前端節點上的共用資料夾。 共用目前不支援 hello Azure 檔案服務，例如 CentOS 6.6 分佈的建議。 如果您的 Linux 節點支援的 Azure 檔案共用，請參閱[如何 toouse Linux 的 Azure 檔案儲存體](../../../storage/files/storage-how-to-use-files-linux.md)。 如需 HPC Pack 的其他檔案共用選項，請參閱 [開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點](hpcpack-cluster.md)。

1. Hello 前端節點上建立資料夾，並共用它 tooEveryone 藉由設定 讀取/寫入權限。 在此範例中， \\ \\CentOS66HN\Namd 是 hello CentOS66HN 所在 hello 的 hello 前端節點的主機名稱的 hello 資料夾名稱。
2. 建立名為 namd2 hello 共用資料夾中的子資料夾。 在 namd2 中，建立另一個名為 namdsample 的子資料夾。
3. 使用的 Windows 版本來擷取 hello 資料夾中的 hello NAMD 檔案**tar 檔案解壓縮**或其他.tar 保存檔運作的 Windows 公用程式。 
   
   * 太解壓縮 hello NAMD tar 檔案解壓縮的封存\\\\CentOS66HN\Namd\namd2。
   * 擷取下的 hello 教學課程檔案\\ \\CentOS66HN\Namd\namd2\namdsample。
4. 開啟 Windows PowerShell 視窗並執行下列命令 toomount hello hello Linux 節點上的共用的資料夾的 hello。
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

hello 第一個命令會建立名為 /namd2 hello LinuxNodes 群組中的所有節點上的資料夾。 hello 第二個命令會掛接到 dir_mode 和 file_mode 位元組 too777 hello 資料夾 hello 共用資料夾 //CentOS66HN/Namd/namd2。 hello *username*和*密碼*hello 命令應該 hello hello 前端節點上的使用者認證。

> [!NOTE]
> hello"\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。 「\`，"表示 hello"，"（逗號字元） 是 hello 命令的一部分。
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>建立 Bash 指令碼 toorun NAMD 作業
NAMD 作業需要*nodelist*檔，以取得**charmrun**啟動 NAMD 處理程序時，節點 toouse toodetermine hello 數目。 使用 Bash 指令碼會產生 hello nodelist 檔案，並執行**charmrun**與此節點清單檔案。 然後您就可以在會呼叫此指令碼的 HPC 叢集管理員中提交 NAMD 工作。

使用您選擇的文字編輯器，在包含 hello NAMD 程式檔案的 hello /namd2 資料夾中建立 Bash 指令碼，並命名 hpccharmrun.sh。快速概念證明，將在本文的 hello 結尾處提供的 hello 範例 hpccharmrun.sh 指令碼複製並移過[提交 NAMD 工作](#submit-a-namd-job)。

> [!TIP]
> 將您的指令碼儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔案。 這可確保正常 hello Linux 節點上。
> 
> 

以下是這個 bash 指令碼的詳細作業內容。 

1. 定義一些變數。
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. 收到 hello 環境變數中的節點資訊。 $NODESCORES 會儲存來自 $CCP_NODES_CORES 的分割單字清單。 $COUNT 是 $NODESCORES hello 大小。
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   hello hello $CCP_NODES_CORES 變數的格式如下所示：
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   這個變數會列出節點、 節點名稱，以及每個節點上配置 toohello 作業的核心數目的 hello 總數。 例如，如果 hello 作業需要 10 個核心 toorun，$CCP_NODES_CORES 的 hello 值就會類似：
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. 如果未設定 hello $CCP_NODES_CORES 變數，啟動**charmrun**直接。 (這應該只有當您在 Linux 節點上直接執行這個指令碼時才會發生。)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. 或者為 **charmrun**建立節點清單檔案。
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. 執行**charmrun** hello nodelist 檔案後，收到其傳回的狀態，並移除 hello 結尾 hello nodelist 檔案。
   
   ${CCP_NUMCPUS} 是 hello HPC Pack 前端節點所設定的另一個環境變數。 它會儲存 hello 總配置 toothis 作業的核心數目。 我們將它的處理序 toospecify hello 數目用於 charmrun。
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. 以 hello 結束**charmrun**傳回狀態。
   
   ```
   exit ${RTNSTS}
   ```

以下是在 hello nodelist 檔案中，哪些 hello 指令碼會產生 hello 資訊：

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

例如：

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>提交 NAMD 作業
現在您已準備好 toosubmit NAMD 作業 HPC 叢集管理員中。

1. 連接 tooyour 叢集前端節點，並啟動 HPC 叢集管理員。
2. 在**資源管理**，確保 hello Linux 計算節點處於 hello**線上**狀態。 如果不是，請選取這些節點，然後按一下 [ **上線**]。
3. 在 [工作管理] 中，按一下 [新增工作]。
4. 輸入工作的名稱，例如 *hpccharmrun*。
   
   ![新的 HPC 工作][namd_job]
5. Hello 上**工作詳細資料**頁面的 **作業資源**，選取資源類型 hello**節點**組 hello 和**最小值**too3。 我們在三個 Linux 節點上執行 hello 工作和每個節點都有四個核心。
   
   ![工作資源][job_resources]
6. 按一下**編輯工作**在 hello 左側的瀏覽，然後按一下**新增**tooadd 工作 toohello 作業。    
7. 在 hello**工作詳細資料和 I/O 重新導向**頁面上，設定下列值的 hello:
   
   * **命令列** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > hello 上述命令列是單一命令，但不含分行符號。 在下方的數行包裝 tooappear**命令列**。
     > 
     > 
   * **工作目錄** - /namd2
   * **最小值** - 3
     
     ![作業詳細資料][task_details]
     
     > [!NOTE]
     > Hello 工作目錄在這裡設定因為**charmrun** toonavigate toohello 會嘗試每個節點上相同的工作目錄。 如果您未設定 hello 工作目錄，HPC Pack 會建立在其中 hello Linux 節點上的隨機命名資料夾中啟動 hello 命令。 這會導致下列錯誤上 hello hello 其他節點： `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid 這個問題，請指定可以存取的所有節點，為 hello 工作目錄的資料夾路徑。
     > 
     > 
8. 按一下**確定**，然後按一下**送出**toorun 這項作業。
   
   根據預設，HPC Pack 送出 hello 與您目前的登入的使用者帳戶的作業。 對話方塊可能會提示您 tooenter hello 使用者名稱和密碼之後，您按一下**送出**。
   
   ![工作認證][creds]
   
   在某些情況下 HPC Pack 會記住您之前輸入，而不會顯示此對話方塊中的 hello 使用者資訊。 toomake HPC Pack 會使它再次顯示中，輸入下列命令，在命令提示字元中的 hello，再提交 hello 作業。
   
   ```command
   hpccred delcreds
   ```
9. hello 作業已執行幾分鐘的時間 toofinish。
10. 尋找在 hello 作業記錄\\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log 和 hello 輸出中的檔案\\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. （選擇性） 啟動 VMD tooview 工作結果。 hello 步驟視覺化 hello NAMD 輸出檔 （在此情況下，在水球體 ubiquitin 蛋白質分子） 已超出本文的 hello 範圍。 如需詳細資訊，請參閱 [NAMD 教學課程](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) 。
    
    ![工作結果][vmd_view]

## <a name="sample-files"></a>範例檔案
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>PowerShell 指令碼叢集部署的 XML 組態檔範例
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a>範例 cred.xml 檔案
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a>範例 hpccharmrun.sh 指令碼
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
