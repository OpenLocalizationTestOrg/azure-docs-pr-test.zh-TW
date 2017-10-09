---
title: "使用 Linux Vm 上的 HPC Pack OpenFOAM aaaRun |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並且跨 RDMA 網路在多個 Linux 計算節點上執行 OpenFOAM 工作。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFoam
本文將告訴您其中一種方式 toorun OpenFoam Azure 虛擬機器中。 在這裡，您將在 Azure 上部署一個具有 Linux 計算節點的 Microsoft HPC Pack 叢集，並使用 Intel MPI 來執行 [OpenFoam](http://openfoam.com/) 作業。 可用於具備 RDMA 功能的 Azure Vm hello 計算節點，以便透過 hello Azure RDMA 網路通訊 hello 計算節點。 在 Azure 中的 OpenFoam 完全包含其他選項 toorun 設定商業映像用於 hello Marketplace，例如 UberCloud 的[OpenFoam 2.3 上 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)，以及執行[Azure 批次](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/)。 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (代表 Open Field Operation and Manipulation) 是一個開放原始碼計算流體力學 (CFD) 軟體套件，廣泛運用在商業和學術組織的工程及科學領域中。 其中包含網格處理工具，特別是 snappyHexMesh，這是一種用於複雜 CAD 幾何的前置和後置處理的平行化網格處理器。 幾乎所有處理序平行執行，讓使用者 tootake 充分利用電腦硬體可供使用。  

Microsoft HPC Pack 提供功能 toorun 大規模 HPC 和平行應用程式，包括 MPI 應用程式，在 Microsoft Azure 虛擬機器的叢集上。 HPC Pack 也支援在 HPC Pack 叢集中部署的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。 請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)簡介 toousing for Linux 計算使用 HPC Pack 的節點。

> [!NOTE]
> 本文將說明如何 toorun Linux MPI 工作負載使用 HPC Pack。 本文假設您對 Linux 系統管理及在 Linux 叢集上執行 MPI 工作負載，有某種程度的熟悉。 如果您使用的 MPI 和 OpenFOAM hello 本文中所顯示的不同版本，您可能必須 toomodify 一些安裝和設定步驟。 
> 
> 

## <a name="prerequisites"></a>必要條件
* **具有支援 RDMA 之 Linux 計算節點的 HPC Pack 叢集** - 使用 [Azure Resource Manager 範本](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)或 [Azure PowerShell 指令碼](hpcpack-cluster-powershell-script.md)，部署具有 A8、A9、H16r 或 H16rm 大小之 Linux 計算節點的 HPC Pack 叢集。 請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)hello 必要條件和步驟，針對任何一個選項。 如果您選擇 hello PowerShell 指令碼部署選項，請參閱這篇文章 hello 結尾 hello 範例檔案中的 hello 範例組態檔。 使用此設定以 Azure 為基礎的 toodeploy HPC Pack 叢集大小 A8 Windows Server 2012 R2 前端節點所組成，再 2 大小 A8 SUSE Linux Enterprise Server 12 計算節點。 請將您的訂用帳戶和服務名稱取代為適當的值。 
  
  **其他注意事項 tooknow**
  
  * 如需 Azure 的 Linux RDMA 網路必要條件，請參閱[高效能運算 VM 大小](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
  * 如果您使用 hello Powershell 指令碼部署選項，將部署的所有 hello Linux 運算節點內一個雲端服務 toouse hello RDMA 網路連線。
  * 部署之後 hello Linux 節點，透過 SSH tooperform 連接任何額外的管理工作。 Hello Azure 入口網站中尋找每個 Linux VM hello SSH 連線詳細資料。  
* **Intel MPI** -toorun SLES 12 hpc OpenFOAM 計算節點在 Azure 中的，您必須從 hello tooinstall hello Intel MPI 文件庫 5 執行階段[Intel.com 網站](https://software.intel.com/en-us/intel-mpi-library/)。 (Intel MPI 5 已預先安裝在 CentOS 型 HPC 映像上)。在稍後的步驟中，請視需要在 Linux 計算節點上安裝 Intel MPI。 tooprepare 此步驟中，您向 Intel 之後, 請依照 hello 確認電子郵件 toohello 相關網頁中的 hello 連結。 然後，複製 hello 下載 Intel MPI hello 適當版本的 hello.tgz 檔案連結。 這篇文章根據 Intel MPI 5.0.3.048 版。
* **OpenFOAM 來源組件**-從 hello，下載適用於 Linux 的 hello OpenFOAM 來源組件軟體[OpenFOAM Foundation 網站](http://openfoam.org/download/2-3-1-source/)。 本文是依據 Source Pack 2.3.1 版 (可透過 OpenFOAM-2.3.1.tgz 的形式下載) 而撰寫的。 稍後在本文章 toounpack 遵循 hello 和編譯 OpenFOAM hello Linux 計算節點上。
* **EnSight** （選用）-您的 OpenFOAM 模擬 toosee hello 結果下載並安裝 hello [EnSight](https://www.ceisoftware.com/download/)視覺效果與分析的程式。 授權和下載資訊是在 hello EnSight 站台。

## <a name="set-up-mutual-trust-between-compute-nodes"></a>設定運算節點之間的相互信任
多個 Linux 節點上執行跨節點的作業需要 hello 節點 tootrust 彼此 (由**rsh**或**ssh**)。 當您建立 hello HPC Pack 叢集以 hello Microsoft HPC Pack IaaS 部署指令碼時，hello 指令碼會自動設定您指定的 hello 系統管理員帳戶的永久相互信任。 Hello 叢集的網域中建立的非管理員使用者，您必須 tooset 暫存 hello 節點間的相互信任工作配置 toothem，和 hello 作業完成之後終結 hello 關聯性時。 每位使用者的 tooestablish 信任提供 HPC Pack 使用 hello 信任關係的 RSA 金鑰組 toohello 叢集。

### <a name="generate-an-rsa-key-pair"></a>產生 RSA 金鑰組
這是簡單 toogenerate RSA 金鑰組，其中包含公開金鑰和私密金鑰，藉由執行 hello Linux**透過像是**命令。

1. 登入 tooa Linux 電腦。
2. 執行下列命令的 hello:
   
   ```
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
1. 請 HPC Pack 系統管理員帳戶 （您執行 hello 部署指令碼時設定 hello 系統管理員帳戶） 的遠端桌面連線 tooyour 前端節點。
2. Hello 叢集的 Active Directory 網域中使用標準的 Windows Server 程序 toocreate 網域使用者帳戶。 例如，使用 hello Active Directory 使用者和電腦 工具 hello 前端節點上。 本文中的 hello 範例假設您建立名為 hpclab\hpcuser 的網域使用者。
3. 建立具名 C:\cred.xml 和複製 hello RSA 索引鍵資料的檔案。 範例 cred.xml 檔案是在 hello 本文結尾處。
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. 開啟命令提示字元並輸入下列命令 tooset hello 認證 hello hpclab\hpcuser 帳戶資料的 hello。 使用 hello **x**參數 toopass hello C:\cred.xml 您建立 hello 主要資料檔案的名稱。
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   這個命令會成功完成而沒有輸出。 設定 hello hello 需要 toorun 作業的使用者帳戶的認證之後, hello cred.xml 檔儲存在安全的位置，或將它刪除。
5. 如果您在其中 Linux 節點上產生 hello RSA 金鑰組，請記得 toodelete hello 索引鍵使用它們完畢之後。 如果 HPC Pack 找到現有的 id_rsa 檔案或 id_rsa.pub 檔案，它就不會設定相互信任。

> [!IMPORTANT]
> 我們不建議叢集系統管理員身分執行 Linux 作業上共用的叢集，因為系統管理員所提交的工作是 hello 根帳號底下執行 hello Linux 節點上。 不過，非管理員使用者所提交的工作在本機 Linux 使用者帳戶下執行以 hello 作業的使用者名稱相同的 hello。 在此情況下，HPC Pack 設定此 Linux 使用者的互信 hello 節點配置 toohello 作業。 您可以設定 hello Linux 使用者 hello Linux 節點上手動執行 hello 作業之前或 HPC Pack hello 使用者會自動建立時送出 hello 作業。 如果 HPC Pack 建立 hello 使用者，HPC Pack hello 作業完成之後刪除它。 tooreduce 安全性威脅，HPC Pack 在作業完成之後移除 hello 索引鍵。
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>為 Linux 節點設定檔案共用
現在設定標準的 SMB 共用資料夾上 hello 前端節點。 tooallow hello Linux 節點 tooaccess 應用程式具有通用的路徑，掛接 hello 共用檔案 hello Linux 節點上的資料夾。 如果您想，您可以使用其他檔案共用選項 (例如 Azure 檔案共用，在許多案例中皆建議使用此選項) 或 NFS 共用。 請參閱 hello 檔案共用資訊和詳細的步驟，以[開始使用 Linux 在 Azure 中的 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)。

1. Hello 前端節點上建立資料夾，並共用它 tooEveryone 藉由設定 讀取/寫入權限。 例如，hello 與前端節點上的共用 C:\OpenFOAM \\ \\SUSE12RDMA HN\OpenFOAM。 在這裡， *SUSE12RDMA HN* hello 前端節點 hello 主機名稱。
2. 開啟 Windows PowerShell 視窗並執行下列命令的 hello:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

hello 第一個命令會建立名為 /openfoam hello LinuxNodes 群組中的所有節點上的資料夾。 hello 第二個命令會掛接 hello 共用資料夾 //SUSE12RDMA-HN/OpenFOAM dir_mode 和 file_mode 位元組 too777 與 hello Linux 節點上。 hello *username*和*密碼*hello 命令應該 hello hello 前端節點上的使用者認證。

> [!NOTE]
> hello"\`"hello 第二個命令中的符號是 PowerShell 的逸出符號。 「\`，"表示 hello"，"（逗號字元） 是 hello 命令的一部分。
> 
> 

## <a name="install-mpi-and-openfoam"></a>安裝 MPI 和 OpenFOAM
toorun OpenFOAM 以 hello RDMA 網路的 MPI 工作，您需要 toocompile OpenFOAM hello Intel MPI 程式庫。 

首先，執行數個**clusrun** tooinstall Intel MPI 程式庫 （如果尚未安裝） OpenFOAM 指令在 Linux 節點上。 設定在 hello Linux 節點之間 tooshare hello 安裝檔案的先前使用 hello 前端節點共用。

> [!IMPORTANT]
> 這些安裝和編譯步驟是範例。 您必須已正確安裝相依的編譯器和程式庫的 Linux 系統管理 tooensure 的一些知識。 您可能需要 toomodify 某些環境變數或其他設定您的 Intel MPI 和 OpenFOAM 版本。 如需詳細資料，請參閱適用於您環境的 [Intel MPI Library for Linux 安裝指南](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html)和 [OpenFOAM Source Pack 安裝](http://openfoam.org/download/2-3-1-source/)。
> 
> 

### <a name="install-intel-mpi"></a>安裝 Intel MPI
儲存 hello 下載的安裝套件的 Intel MPI (在此範例中 l_mpi_p_5.0.3.048.tgz) 中 C:\OpenFoam hello 前端節點上，從 /openfoam hello Linux 節點均可存取此檔案。 然後執行**clusrun** tooinstall Intel MPI 所有 hello Linux 節點上的文件庫。

1. hello 以下命令 hello 安裝封裝的副本，並擷取它太/選擇/intel 每個節點上。
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI 文件庫以無訊息方式，使用 silent.cfg 檔案。 您可以找到範例在 hello hello 本文結尾處的範例檔案。 發生在 hello 這個檔案的共用資料夾 /openfoam。 如需 hello silent.cfg 檔案的詳細資訊，請參閱[Intel MPI Library for Linux 安裝指南-無訊息安裝](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)。
   
   > [!TIP]
   > 請確實將您的 silent.cfg 檔案儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。 這個步驟可確保正常 hello Linux 節點上。
   > 
   > 
3. 以無訊息模式安裝 Intel MPI Library。
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>設定 MPI
進行測試，您應該加入下列行 toohello /etc/security/limits.conf 每個 hello Linux 節點上的 hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


在更新 hello limits.conf 檔案之後，請重新啟動 hello Linux 節點。 例如，使用 hello 下列**clusrun**命令：

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

重新啟動之後，請確定該 hello 共用的資料夾掛接為 /openfoam。

### <a name="compile-and-install-openfoam"></a>編譯和安裝 OpenFOAM
儲存 hello OpenFOAM 來源組件 (OpenFOAM-在此範例中的 2.3.1.tgz) tooC:\OpenFoam hello 下載的安裝套件 hello 前端節點上，從 /openfoam hello Linux 節點均可存取此檔案。 然後執行**clusrun** toocompile OpenFOAM 所有 hello Linux 節點的命令。

1. 建立資料夾 /opt/OpenFOAM 每個 Linux 節點上，複製 hello 來源封裝 toothis 資料夾，並將它解壓縮那里。
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. 以 hello Intel MPI Library，先設定環境變數，Intel MPI 和 OpenFOAM toocompile OpenFOAM。 使用 bash 指令碼呼叫 settings.sh tooset hello 變數。 您可以找到範例在 hello hello 本文結尾處的範例檔案。 位置中的這個檔案 （儲存在 Linux 行尾結束符號） hello 共用資料夾 /openfoam。 這個檔案也包含設定 hello MPI 和 OpenFOAM 執行階段，您會使用更新版本 toorun OpenFOAM 作業。
3. 安裝所需的相依封裝 toocompile OpenFOAM。 根據您的 Linux 散發套件，您可能必須 tooadd 儲存機制。 執行**clusrun**命令類似 toohello 下列：
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    如有必要，SSH tooeach Linux 節點 toorun hello 命令 tooconfirm 它們能正常執行。
4. 執行下列命令 toocompile OpenFOAM hello。 hello 編譯處理程序需要一些時間 toocomplete，和會產生大量的記錄檔資訊 toostandard 輸出，因此使用 hello **/ 交錯**選項交錯 toodisplay hello 輸出。
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > hello"\`"hello 命令中的符號是 PowerShell 的逸出符號。 「\`（& s) 」 表示 hello"&"是 hello 命令的一部分。
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>準備 toorun OpenFOAM 工作
現在取得準備 toorun MPI 工作呼叫 sloshingTank3D，也就是其中一個 hello OpenFoam 範例，兩個 Linux 節點上。 

### <a name="set-up-hello-runtime-environment"></a>設定 hello 執行階段環境
tooset MPI 和 OpenFOAM hello Linux 節點上，執行下列 Windows PowerShell 視窗中的命令 hello 前端節點上的 hello 的 hello 執行階段環境。 (此命令僅適用於 SUSE Linux。)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>準備範例資料
使用 hello 前端節點共用您先前設定 tooshare hello Linux 節點 （裝載為 /openfoam） 之間的檔案。

1. 您的 Linux 的 SSH tooone 計算節點。
2. 如果您尚未這樣，請執行下列命令 tooset hello OpenFOAM 執行階段環境，hello。
   
   ```
   $ source /openfoam/settings.sh
   ```
3. 複製 hello sloshingTank3D 範例 toohello 共用的資料夾，並瀏覽 tooit。
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. 當您使用此範例的 hello 預設參數時，可能需要數十個分鐘 toorun，因此您可能想 toomodify 執行速度某些參數 toomake。 一個簡單的選擇是 toomodify hello 時間步驟變數 deltaT 和 writeInterval hello 系統/controlDict 檔案中。 這個檔案會儲存所有相關的時間和讀取及寫入方案資料 toohello 控制項的輸入的資料。 例如，您可以變更從 0.05 too0.5 deltaT hello 值和從 0.05 too0.5 writeInterval hello 值。
   
   ![修改步階變數][step_variables]
5. 您可以指定想要的值為 hello 變數 hello 系統/decomposeParDict 檔案中。 這個範例會使用兩個 Linux 節點每 8 個核心，因此設定 numberOfSubdomains too16 and n 的 hierarchicalCoeffs too(1 1 16)，表示與 16 的處理序平行執行 OpenFOAM。 如需詳細資訊，請參閱 [OpenFOAM User Guide: 3.4 Running applications in parallel (OpenFOAM 使用者指南：3.4 平行執行應用程式)](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)。
   
   ![分解程序][decompose]
6. 執行 hello hello sloshingTank3D 目錄 tooprepare hello 範例資料中的下列命令。
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Hello 前端節點上，您應該會看到 hello 範例資料檔案複製到 C:\OpenFoam\sloshingTank3D。 （C:\OpenFoam 是 hello hello 前端節點上的共用的資料夾）。
   
   ![Hello 前端節點上的資料檔案][data_files]

### <a name="host-file-for-mpirun"></a>mpirun 的主機檔案
在此步驟中，您建立的主機檔案 （的運算節點的清單） 的 hello **mpirun**命令使用。

1. 其中一個 hello Linux 節點上建立名為 hostfile 下 /openfoam，因此這個檔案無法到達 /openfoam/hostfile 所有 Linux 節點上的檔案。
2. 將您的 Linux 節點名稱寫入此檔案中。 在此範例中，hello 檔案會包含下列名稱的 hello:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > 您也可以建立此檔案在 C:\OpenFoam\hostfile hello 前端節點。 如果您選擇這個選項，請將其儲存為具有 Linux 行尾結束符號 (只有 LF，不是 CR LF) 的文字檔。 這可確保正常 hello Linux 節點上。
   > 
   > 
   
   **Bash 指令碼包裝函式**
   
   如果您有許多 Linux 節點，而且您想要您的工作 toorun 僅部分，它不是固定的主機檔案，最好先 toouse 因為您不知道哪些節點配置 tooyour 作業。 在此情況下，撰寫 bash 指令碼包裝函式**mpirun** toocreate 自動 hello 主機檔案。 您可以尋找範例 bash 指令碼包裝函式呼叫端的此篇文章 hello hpcimpirun.sh，並將它儲存為 /openfoam/hpcimpirun.sh。此範例指令碼未 hello 遵循：
   
   1. 設定環境變數 hello **mpirun**，與某些加法命令參數 toorun hello MPI 工作透過 hello RDMA 網路。 在此情況下，它會設定 hello 下列變數：
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. 建立主機檔案，根據 toohello 環境變數 $CCP_NODES_CORES，由 hello HPC 前端節點 hello 作業啟動時設定。
      
      $CCP_NODES_CORES hello 格式會遵循下列模式：
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      其中
      
      * `<Number of nodes>`-節點的 hello 數目配置 toothis 作業。  
      * `<Name of node_n_...>`-每個節點的 hello 名稱配置 toothis 作業。
      * `<Cores of node_n_...>`-hello hello 節點配置的 toothis 工作上的核心數目。
      
      例如，如果 hello 工作需要兩個節點 toorun，$CCP_NODES_CORES 就類似
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. 呼叫 hello **mpirun**命令，並將附加兩個參數 toohello 命令列。
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-建立 hello hello 主機檔案 hello 指令碼路徑
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-hello HPC Pack 前端節點，其中儲存 hello 總核心的數目來設定環境變數配置 toothis 作業。 在此情況下，它會指定處理序數目 hello **mpirun**。

## <a name="submit-an-openfoam-job"></a>提交 OpenFOAM 工作
現在，您可以在 HPC 叢集管理員中提交工作。 您需要 toopass hello 指令碼 hpcimpirun.sh hello 命令列中的某些 hello 作業 」 工作。

1. 連接 tooyour 叢集前端節點，並啟動 HPC 叢集管理員。
2. **在 資源管理**，確保 hello Linux 計算節點處於 hello**線上**狀態。 如果不是，請選取這些節點，然後按一下 [ **上線**]。
3. 在 [工作管理] 中，按一下 [新增工作]。
4. 輸入作業的名稱，例如 *sloshingTank3D*。
   
   ![工作詳細資料][job_details]
5. 在**作業資源**、 選擇 hello 「 節點 」 資源類型，以及設定 hello 最小值 too2。 此設定執行 hello 工作，每一個都有 8 個核心，在此範例中的兩個 Linux 節點上。
   
   ![工作資源][job_resources]
6. 按一下**編輯工作**在 hello 左側的瀏覽，然後按一下**新增**tooadd 工作 toohello 作業。 加入四個工作 toohello 作業以 hello 下列命令列和設定。
   
   > [!NOTE]
   > 執行`source /openfoam/settings.sh`hello OpenFOAM 和 MPI 執行階段環境，讓每個下列工作的 hello hello OpenFOAM 命令之前呼叫，它會設定。
   > 
   > 
   
   * **工作 1**。 執行**decomposePar** toogenerate 資料檔案執行**interDyMFoam**以平行方式。
     
     * 指定一個節點 toohello 工作
     * **命令列** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **工作目錄** - /openfoam/sloshingTank3D
     
     請參閱下列圖 hello。 同樣地，您設定 hello 其餘的工作。
     
     ![作業 1 詳細資料][task_details1]
   * **工作 2**。 執行**interDyMFoam**平行 toocompute hello 範例中。
     
     * 指定兩個節點 toohello 工作
     * **命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **工作目錄** - /openfoam/sloshingTank3D
   * **工作 3**。 執行**reconstructPar** toomerge hello 設定的時間目錄從每個 processor_N_ 目錄成單一集合。
     
     * 指定一個節點 toohello 工作
     * **命令列** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **工作目錄** - /openfoam/sloshingTank3D
   * **工作  4**。 執行**foamToEnsight**中平行 tooconvert EnSight hello OpenFOAM 結果檔案格式和 hello 案例目錄中名為 Ensight 中放置 hello EnSight 檔案。
     
     * 指定兩個節點 toohello 工作
     * **命令列** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **工作目錄** - /openfoam/sloshingTank3D
7. 以遞增的工作順序中新增相依性 toothese 工作。
   
   ![作業相依性][task_dependencies]
8. 按一下**送出**toorun 這項作業。
   
   根據預設，HPC Pack 送出 hello 與您目前的登入的使用者帳戶的作業。 按一下 之後**送出**，您可能會看到對話方塊，提示您 tooenter hello 使用者名稱和密碼。
   
   ![工作認證][creds]
   
   在某些情況下 HPC Pack 會記住您之前輸入，而不會顯示此對話方塊中的 hello 使用者資訊。 toomake HPC Pack 會使它再次顯示中，輸入下列命令，在命令提示字元中的 hello，再提交 hello 作業。
   
   ```
   hpccred delcreds
   ```
9. hello 作業會從數十個分鐘 tooseveral 小時，根據您為 hello 範例 toohello 參數。 在 hello 熱度圖，您會看到 hello hello Linux 節點上執行的作業。 
   
   ![熱圖][heat_map]
   
   在每個節點上會啟動 8 個處理程序。
   
   ![Linux 程序][linux_processes]
10. Hello 作業完成時，請 C:\OpenFoam\sloshingTank3D，與在 C:\OpenFoam hello 記錄檔 下的資料夾中找到 hello 工作結果。

## <a name="view-results-in-ensight"></a>在 EnSight 中檢視結果
選擇性地使用[EnSight](https://www.ceisoftware.com/) toovisualize 及分析 hello 的 hello OpenFOAM 作業的結果。 如需 EnSight 中的視覺效果和動畫的詳細資訊，請參閱此 [視訊指南](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html)。

1. Hello 前端節點上安裝 EnSight 之後，請啟動它。
2. 開啟 C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case。
   
   您會看到槽 hello 檢視器中。
   
   ![EnSight 中的儲存槽][tank]
3. 建立**Isosurface**從**internalMesh**，然後選擇 hello 變數**alpha_water**。
   
   ![建立 isosurface][isosurface]
4. 設定 hello 色彩**Isosurface_part** hello 先前步驟中建立。 例如，將它設定 toowater 藍色。
   
   ![編輯 isosurface 色彩][isosurface_color]
5. 建立**Iso 磁碟區**從**牆**選取**牆**在 hello**部分**] 面板，按一下 [hello **Isosurfaces** hello 工具列中的按鈕。
6. 在 hello 對話方塊中，選取 **類型**為**Isovolume**並設定 hello 的最小值**Isovolume 範圍**too0.5。 toocreate hello isovolume 中，按一下**建立與所選部分**。
7. 設定 hello 色彩**Iso_volume_part** hello 先前步驟中建立。 例如，將它設定 toodeep 上限藍色。
8. 設定 hello 色彩**牆**。 例如，將它設定 tootransparent 白色。
9. 現在按一下**播放**toosee hello 結果 hello 模擬。
   
    ![儲存槽結果][tank_result]

## <a name="sample-files"></a>範例檔案
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>PowerShell 指令碼叢集部署的 XML 組態檔範例
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>範例 silent.cfg 檔案 tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>範例 settings.sh 指令碼
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>範例 hpcimpirun.sh 指令碼
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
