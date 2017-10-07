---
title: "aaaRun 星狀-CCM + 使用 Linux Vm 上的 HPC Pack |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並且跨 RDMA 網路在多個 Linux 計算節點上執行 STAR-CCM+ 作業。"
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 STAR-CCM+
本文將告訴您如何 toodeploy Microsoft HPC Pack 叢集化 Azure 與執行上[CD adapco 星狀-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE)多個互相 InfiniBand Linux 計算節點上的作業。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack 提供了功能 toorun 各式各樣的大規模 HPC 和平行應用程式，包括 MPI 應用程式，在 Microsoft Azure 虛擬機器的叢集上。 HPC Pack 也支援在 HPC Pack 叢集中部署的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。 如簡介 toousing Linux 計算節點使用 HPC Pack，請參閱 <<c0> [ 開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)。

## <a name="set-up-an-hpc-pack-cluster"></a>設定 HPC Pack 叢集
下載 hello HPC Pack IaaS 部署指令碼從 hello[下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=44949)然後在本機解壓縮。

Azure PowerShell 是必要條件。 如果您的本機電腦上未設定 PowerShell，請閱讀 hello 文章[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

Hello 撰寫本文時，在 hello Linux 映像從 hello Azure Marketplace （其中包含適用於 Azure 的 hello InfiniBand 驅動程式） 都是 SLES 12、 CentOS 6.5 和 CentOS 7.1。 這篇文章根據 SLES 12 的 hello 使用量。 tooretrieve hello 支援 HPC hello Marketplace 中的所有 Linux 映像名稱，您可以執行下列 PowerShell 命令的 hello:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

hello 輸出會列出這些映像可用以及 hello 映像名稱 hello 位置 (**ImageName**) toobe hello 部署範本中使用的更新版本。

部署 hello 叢集之前，您有 toobuild HPC Pack 部署範本檔案。 因為我們的目標小型的叢集，hello 前端節點會 hello 網域控制站並裝載本機 SQL 資料庫。

hello 下列範本會部署前端節點，請建立名為 XML 檔案**MyCluster.xml**，並取代的 hello 值**SubscriptionId**， **StorageAccount**， **位置**， **VMName**，和**ServiceName**與您。

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

在提升權限的命令提示字元中執行 hello PowerShell 命令啟動 hello 前端節點建立：

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

20 too30 分鐘之後，應該已經準備好 hello 前端節點。 您也可以按一下 hello 從 hello Azure 入口網站連線 tooit**連接**hello 虛擬機器的圖示。

最後，您可能必須 toofix hello DNS 轉寄站。 因此，toodo 啟動 DNS 管理員。

1. 以滑鼠右鍵按一下 hello 伺服器名稱的 DNS 管理員中，選取**屬性**，然後按一下hello**轉寄站** 索引標籤。
2. 按一下 hello**編輯**按鈕 tooremove 任何轉寄站，然後按一下**確定**。
3. 請確定該 hello**使用根提示，如果沒有轉寄站可用**核取方塊已選取，然後按一下**確定**。

## <a name="set-up-linux-compute-nodes"></a>設定 Linux 計算節點
使用 hello 部署 hello Linux 計算節點，您會使用 toocreate hello 前端節點相同的部署範本。

複製 hello 檔案**MyCluster.xml**從您的本機電腦 toohello 前端節點和更新 hello **NodeCount** hello 數目，您想 toodeploy 的節點具有標記 (< = 20)。 是小心 toohave 足夠可用的核心 Azure 配額，因為每個 A9 執行個體將使用您的訂用帳戶中 16 個核心。 您可以使用 A8 執行個體 （8 核心） 取代 A9，如果您想 toouse hello 中的多個 Vm 相同的預算。

Hello 前端節點上，複製 hello HPC Pack IaaS 部署指令碼。

執行下列 Azure PowerShell 命令，在提升權限的命令提示字元中的 hello:

1. 執行**Add-azureaccount** tooconnect tooyour Azure 訂用帳戶。
2. 如果您有多個訂用帳戶，執行**Get-azuresubscription** toolist 它們。
3. 設定預設訂用帳戶執行 hello **Select-azuresubscription SubscriptionName xxxx-預設**命令。
4. 執行**.\New-HPCIaaSCluster.ps1-ConfigFile MyCluster.xml** toostart 部署 Linux 計算節點。
   
   ![前端節點部署實務][hndeploy]

開啟 hello HPC Pack 叢集管理員工具。 幾分鐘後，Linux 計算節點會定期出現在叢集計算節點的清單中。 Hello 傳統部署模式中，會以循序方式建立 IaaS Vm。 因此如果節點的 hello 數目很重要，取得所有部署可能需要很長的時間。

![HPC Pack 叢集管理員中的 Linux 節點][clustermanager]

既然所有節點都已啟動並執行 hello 叢集中，都有額外的基礎結構設定 toomake。

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>為 Windows 和 Linux 節點設定 Azure 檔案共用
您可以使用 hello Azure 檔案服務 toostore 指令碼、 應用程式封裝和資料檔案。 Azure 檔案提供 Azure Blob 儲存體的 CIFS 功能，以當成持續性存放區。 請注意，這不是 hello 最靈活的解決方案，但它是最簡單的一個 hello，而不需要專用的 Vm。

建立 Azure 檔案共用 hello 文件中的 hello 指示[開始使用 Azure 檔案儲存在 Windows 上](../../../storage/files/storage-dotnet-how-to-use-files.md)。

保留 hello 做為儲存體帳戶名稱**saname**，hello 檔案共用名稱做為**sharename**，並為 hello 儲存體帳戶金鑰**sakey**。

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>在 hello 前端節點上裝載 hello Azure 檔案共用
開啟提升權限的命令提示字元並執行下列命令 toostore hello 認證 hello 本機保存庫中的 hello:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

然後，toomount hello Azure 檔案共用，執行：

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Linux 計算節點上裝載 hello Azure 檔案共用
一個實用的工具使用 HPC Pack 隨附是 hello clusrun 工具。 您可以同時使用這個相同命令的命令列工具 toorun hello 組計算節點上。 在我們的案例，它會使用 toomount hello Azure 檔案共用，並將它保存 toosurvive 重新開機。
在 hello 前端節點上提高權限命令提示字元中執行下列命令的 hello。

toocreate hello 掛接目錄：

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

toomount hello Azure 檔案共用：

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

toopersist hello 掛接共用：

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>安裝 STAR-CCM+
Azure VM 執行個體 A8 和 A9 提供 InfiniBand 支援與 RDMA 功能。 啟用這些功能的 hello 核心驅動程式可供 Windows Server 2012 R2、 SUSE 12、 CentOS 6.5 和 CentOS 7.1 hello Azure Marketplace 中的映像。 Microsoft MPI 和 Intel MPI （發行 5.x） 是 hello 兩個 MPI 程式庫在 Azure 中支援這些驅動程式。

CD-adapco STAR-CCM+ 發行 11.x 和更新版本隨附 Intel MPI 5.x 版，因此含有 Azure 的 InfiniBand 支援。

取得 hello Linux64 星狀-CCM + 封裝從 hello [CD adapco 入口網站](https://steve.cd-adapco.com)。 在我們的案例中，以混合精確度使用版本 11.02.010。

Hello 在前端節點上，hello **/hpcdata** Azure 檔案共用，請建立名為的殼層指令碼**setupstarccm.sh**以 hello 內容之後。 此指令碼會執行在星狀總每個計算節點 tooset-CCM + 在本機。

#### <a name="sample-setupstarcmsh-script"></a>範例 setupstarcm.sh 指令碼
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
現在，向上星狀 tooset-CCM + 您的所有 Linux 上計算節點，請開啟提升權限的命令提示字元，執行下列命令的 hello:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Hello 命令執行時，您可以使用 hello 熱門地圖的 「 叢集管理員來監視 hello CPU 使用量。 幾分鐘後，所有節點應該都會正確設定。

## <a name="run-star-ccm-jobs"></a>執行 STAR-CCM+ 作業
HPC Pack 用於其順序 toorun 星狀中的工作排程器功能-CCM + 作業。 toodo 因此，我們需要 hello 的幾個指令碼會使用的 toostart hello 作業，而且執行星狀支援-CCM +。 hello 輸入的資料保留在 hello Azure 檔案共用上為了簡單起見，第一個。

下列 PowerShell 指令碼的 hello 是使用的 tooqueue 星狀-CCM + 作業。 它會採用三個引數︰

* hello 模型名稱
* 使用節點 toobe 的 hello 數字
* 使用每個節點 toobe 核心的 hello 數量

因為星狀-CCM + 可以填入 hello 記憶體頻寬，其通常最好 toouse 較少的每個核心計算節點，並加入新節點。 每個節點的核心 hello 確切數目將取決於 hello 處理器系列和 hello 相互連接速度。

hello 節點配置專用的 hello 作業並不能與其他工作共用。 hello 工作未直接啟動為 MPI 工作。 hello **runstarccm.sh**殼層指令碼會啟動 hello MPI 啟動器。

hello 輸入模型和 hello **runstarccm.sh**指令碼會儲存在 hello **/hpcdata**先前已裝載的共用。

記錄檔命名的 hello 作業識別碼，而且會儲存在 hello **/hpcdata 共用**，連同 hello 星狀-CCM + 輸出檔案。

#### <a name="sample-submitstarccmjobps1-script"></a>範例 SubmitStarccmJob.ps1 指令碼
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
將 **runner.java** 取代成您偏好的 STAR-CCM+ Java 模型啟動程式與記錄程式碼。

#### <a name="sample-runstarccmsh-script"></a>範例 runstarccm.sh 指令碼
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

在我們的測試中，我們使用的是 Power-One-Demand 授權權杖。 您必須在該語彙基元，tooset hello **$CDLMD_LICENSE_FILE**環境變數太**1999@flex.cd-adapco.com**  hello hello 鍵**-podkey** hello 命令列選項.

某些在初始化之後，hello 指令碼-從擷取 hello **$CCP_NODES_CORES** HPC Pack 設定-環境變數 hello 節點 toobuild hello MPI 啟動器 hostfile 使用的清單。 此 hostfile 將包含 hello 的 hello 工作，每行一個名稱會用於計算節點名稱清單。

hello 格式**$CCP_NODES_CORES**遵循下列模式：

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

其中：

* `<Number of nodes>`是 hello 配置 toothis 工作的節點數目。
* `<Name of node_n_...>`這是每個節點配置 toothis 作業 hello 名稱。
* `<Cores of node_n_...>`是 hello hello 節點配置 toothis 工作上的核心數目。

hello 的核心數目 (**$NBCORES**) 也是導出根據的 hello 節點數目 (**$NBNODES**) 和 hello 每個節點的核心數目 (當做參數提供**$NBCORESPERNODE**).

Hello MPI 選項，hello 與 Intel MPI 在 Azure 上搭配使用的是：

* `-mpi intel`toospecify Intel MPI。
* `-fabric UDAPL`toouse Azure 的 InfiniBand 動詞命令。
* `-cpubind bandwidth,v`星形的 MPI toooptimize 頻寬-CCM +。
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI 與 Azure 的 InfiniBand 並 tooset hello 所需的每個節點的核心數目。
* `-batch`toostart 星狀-CCM + 批次模式中沒有使用者介面。

最後，toostart 作業，請確定您的節點正在執行，而且都已上線的叢集管理員 中。 然後從 PowerShell 命令提示字元中，執行此作業︰

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>停止節點
稍後您已完成測試之後，您可以使用下列 HPC Pack PowerShell 命令 toostop hello，並啟動節點：

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>後續步驟
嘗試執行其他 Linux 工作負載。 例如，請參閱︰

* [在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD](hpcpack-cluster-namd.md)
* [在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
