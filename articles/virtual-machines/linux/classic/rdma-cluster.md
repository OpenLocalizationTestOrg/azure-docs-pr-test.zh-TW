---
title: "Linux RDMA 叢集 toorun MPI 應用程式總 aaaSet |Microsoft 文件"
description: "建立 Linux 叢集的大小 H16r 的 H16mr、 A8、 A9 Vm toouse hello Azure RDMA 網路 toorun MPI 應用程式"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>設定 Linux RDMA 叢集 toorun MPI 應用程式
了解 tooset Linux RDMA 註冊在 Azure 中的叢集化[高效能計算 VM 大小](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toorun 平行訊息傳遞介面 (MPI) 應用程式。 本文提供步驟 tooprepare Linux HPC 映像 toorun Intel MPI 叢集上。 準備工作之後, 您部署的 Vm 使用此映像和一個 hello 具備 RDMA 功能的 Azure VM 大小 （目前 H16r、 H16mr、 A8、 或 A9） 的叢集。 使用 hello 叢集 toorun MPI 應用程式，透過遠端直接記憶體存取 (RDMA) 技術為基礎的低延遲、 高輸送量網路有效地進行通訊。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

## <a name="cluster-deployment-options"></a>叢集部署選項
以下是方法，不論作業排程器，您可以使用 toocreate RDMA Linux 叢集。

* **Azure CLI 指令碼**： 如本文稍後所示，使用 hello [Azure 命令列介面](../../../cli-install-nodejs.md)(CLI) tooscript hello 部署具備 RDMA 功能的 Vm 的叢集。 服務管理模式中的 hello CLI hello 叢集節點建立循序在 hello 傳統部署模型中，以便部署多個計算節點可能需要幾分鐘的時間。 tooenable hello RDMA 網路連線，當您使用 hello 傳統部署模型，將 hello Vm 部署在 hello 相同雲端服務。
* **Azure 資源管理員範本**： 您也可以使用 hello 資源管理員部署模型 toodeploy toohello RDMA 網路連線的 RDMA 功能的 Vm 的叢集。 您可以[建立您自己的範本](../../../resource-group-authoring-templates.md)，或檢查 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)Microsoft 或 hello 社群 toodeploy hello 您想的方案所提供的範本。 資源管理員範本可提供快速且可靠的方式 toodeploy Linux 叢集。 tooenable hello RDMA 網路連線，當您使用 hello Resource Manager 部署模型，部署在 hello hello Vm 相同可用性設定組。
* **HPC Pack**： 在 Azure 中建立 Microsoft HPC Pack 叢集並加入具備 RDMA 功能的計算節點執行支援的 Linux 發佈 tooaccess hello RDMA 網路。 如需詳細資訊，請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](hpcpack-cluster.md)。

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Hello 傳統模型中的範例部署步驟
hello 下列步驟說明如何 toouse hello Azure CLI toodeploy 從 hello Azure Marketplace 的 SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM 自訂方法，及建立自訂的 VM 映像。 然後您可以使用 hello 映像，請 tooscript hello 部署具備 RDMA 功能的 Vm 的叢集。

> [!TIP]
> 使用類似步驟 toodeploy CentOS 架構 HPC hello Azure Marketplace 中的影像為基礎的 RDMA 功能的 Vm 的叢集。 如所述，某些步驟會稍有不同。 
>
>

### <a name="prerequisites"></a>必要條件
* **用戶端電腦**： 需要 Mac、 Linux 或 Windows 用戶端電腦 toocommunicate 與 Azure。 這些步驟假設您使用 Linux 用戶端。
* **Azure 訂用帳戶**：如果您沒有訂用帳戶，只需要幾分鐘就可以建立[免費帳戶](https://azure.microsoft.com/free/)。 針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。
* **VM 大小可用性**: hello 遵循大小的執行個體都具有 RDMA 功能： H16r，H16mr、 A8、 A9。 如需了解 Azure 區域中的可用性，請查看 [依區域提供的產品](https://azure.microsoft.com/regions/services/) 。
* **核心配額**： 您可能需要 tooincrease hello 配額的核心 toodeploy 是需要大量計算 Vm 的叢集。 比方說，您需要至少 128 個核心，如果您想 toodeploy 8 A9 Vm 這篇文章中所示。 您的訂閱也可能會限制 hello 特定 VM 大小系列，包括 hello H 序列中，您可以部署的核心數目。 toorequest 配額增加[開啟線上客戶支援要求](../../../azure-supportability/how-to-create-azure-support-request.md)不收費。
* **Azure CLI**:[安裝](../../../cli-install-nodejs.md)hello Azure CLI 和[連接 tooyour Azure 訂用帳戶](../../../xplat-cli-connect.md)從 hello 用戶端電腦。

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>佈建 SLES 12 SP1 HPC VM
登入以 hello Azure CLI tooAzure 之後，執行`azure config list`hello 輸出的 tooconfirm 顯示服務管理模式。 如果不存在，請執行此命令設定 hello 模式：

    azure config mode asm


輸入下列 toolist hello 所有 hello 訂用帳戶已授權的 toouse:

    azure account list

hello 目前的作用中訂用帳戶會用來識別`Current`設定得`true`。 如果此訂用帳戶不 hello 一個要 toouse toocreate hello 叢集中，設定 hello 適當的訂用帳戶 ID 與 hello 作用中訂用帳戶：

    azure account set <subscription-Id>

toosee hello 公開可用的 SLES 12 SP1 HPC 映像，在 Azure 中，執行類似，hello 命令假設您的殼層環境支援**grep**:

    azure vm image list | grep "suse.*hpc"

執行命令，像 hello 下列佈建的 RDMA 功能的 VM 與 SLES 12 SP1 HPC 映像：

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

其中：

* hello 大小 (在此範例中 A9) 是其中一個 hello 具備 RDMA 功能的 VM 大小。
* 外部 SSH 連接埠號碼 hello (在此範例中，也就是 hello SSH 預設 22) 是任何有效的連接埠號碼。 hello 內部 SSH 連接埠號碼設定 too22。
* 新的雲端服務中建立 hello hello 位置所指定的 Azure 區域。 指定在哪個 hello VM 大小您選擇可用的位置。
* 如需 SUSE 優先順序的支援 （這會產生額外費用），hello SLES 12 SP1 映像名稱目前可以在這兩個選項的其中一個： 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>自訂 hello VM
Hello VM 完成佈建之後，使用 SSH toohello VM hello VM 的外部 IP 位址 （或 DNS 名稱），而且 hello 外部連接埠號碼設定，，，然後加以自訂。 連接的詳細資訊，請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 Hello hello VM 所設定的使用者身分執行命令，除非根目錄存取必要的 toocomplete 步驟。

> [!IMPORTANT]
> Microsoft Azure 不提供根目錄存取 tooLinux Vm。 toogain 系統管理存取權，使用者 toohello VM，使用執行命令的身分連接時`sudo`。
>
>

* **更新**：使用 zypper 安裝更新。 您也可以 tooinstall NFS 公用程式。

  > [!IMPORTANT]
  > 在 SLES 12 SP1 HPC VM 中，我們建議您不要套用核心更新，可能會導致問題以 hello Linux RDMA 驅動程式。
  >
  >
* **Intel MPI**: hello 上完成的安裝 Intel MPI hello SLES 12 SP1 HPC VM 執行下列命令的 hello:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **鎖定記憶體**: MPI 代碼 toolock hello 可用記憶體的 RDMA，新增或變更 hello 遵循 hello /etc/security/limits.conf 檔案中的設定。 您需要根存取 tooedit 這個檔案。

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > 為了測試用途，您也可以設定 memlock toounlimited。 例如： `<User or group name>    hard    memlock unlimited`。 如需詳細資訊，請參閱[設定鎖定的記憶體大小的最佳已知方法](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size)。
  >
  >
* **SLES Vm 的 SSH 金鑰**： 產生 SSH 金鑰 tooestablish 信任您的使用者帳戶在 hello 之間執行 MPI 工作時，計算 hello SLES 叢集中的節點。 如果您部署 CentOS 型 HPC VM，請勿遵循此步驟。 您擷取 hello 映像並部署 hello 叢集之後，請參閱稍後 hello 的叢集節點之間的 passwordless SSH 信任此發行項 tooset 的指示。

    toocreate SSH 金鑰，執行下列命令的 hello。 當提示您輸入時時，請選取**Enter** toogenerate hello 金鑰在 hello 預設位置，如果未設定密碼。

        ssh-keygen

    附加 hello 公用金鑰 toohello authorized_keys 檔為已知的公開金鑰。

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    在 hello ~/.ssh 目錄中，編輯或建立 hello 設定檔。 提供您計劃在 Azure 中 (在此範例中 10.32.0.0/16) toouse hello IP 位址範圍的 hello 私人網路：

        host 10.32.0.*
        StrictHostKeyChecking no

    或者，列出在叢集中的每個 VM hello 私人網路 IP 位址，如下所示：

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > 未指定特定 IP 位址或範圍時，設定 `StrictHostKeyChecking no` 可能會造成潛在的安全性風險。
  >
  >
* **應用程式**： 安裝任何應用程式，您需要或執行其他自訂，然後擷取 hello 映像。

### <a name="capture-hello-image"></a>擷取 hello 映像
toocapture hello 映像，先執行下列命令在 hello Linux VM 上的 hello。 此命令 deprovisions hello VM，但會維護使用者帳戶和 SSH 金鑰設定。

```
sudo waagent -deprovision
```

從用戶端電腦，執行下列 Azure CLI 命令 toocapture hello 映像的 hello。 如需詳細資訊，請參閱[如何 toocapture 傳統 Linux 虛擬機器做為映像](capture-image.md)。  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

執行這些命令之後，您可以使用擷取 hello VM 映像，並且刪除 hello VM。 現在您會有您的自訂映像準備 toodeploy 叢集。

### <a name="deploy-a-cluster-with-hello-image"></a>叢集與 hello 映像部署
修改下列 Bash 指令碼，以適當的值，為您的環境的 hello，並從用戶端電腦執行。 因為 Azure 會將部署 hello 傳統部署模型中的循序 hello Vm，花幾分鐘的時間，toodeploy hello 八個 A9 的 Vm，建議的指令碼中。

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>CentOS HPC 叢集的考量
如果您想 tooset 根據其中一個 hello 而不是 SLES 12 的 Azure Marketplace 中的 hello CentOS 架構 HPC 映像的 HPC 叢集，請遵循 hello hello 前面一節中的一般步驟。 請注意下列差異，當您佈建並設定 hello VM hello:

- 已經在從 CentOS 型 HPC 映像佈建的 VM 上安裝 Intel MPI。
- 已加入 hello VM /etc/security/limits.conf 檔案鎖定的記憶體設定。
- 不會產生 hello 您佈建的 VM 上的 SSH 金鑰擷取。 相反地，我們建議使用者為基礎的驗證設定，部署 hello 叢集之後。 如需詳細資訊，請參閱下列章節的 hello。  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>設定 passwordless hello 叢集上的 SSH 信任
在 CentOS 為基礎的 HPC 叢集上，有兩種方法來建立 hello 計算節點之間的信任： 主控件為基礎的驗證和以使用者為基礎的驗證。 主機型驗證 hello 這篇文章的範圍內，和通常在部署期間就必須透過 擴充功能指令碼來完成。 使用者為基礎的驗證相當方便部署之後建立信任，而且需要 hello 產生和 SSH 金鑰在 hello 之間共用運算 hello 叢集中的節點。 此命令通常稱為無密碼 SSH 登入，執行 MPI 工作時必須使用此命令。

Hello 社群貢獻的範例指令碼位於[GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable CentOS 為基礎的 HPC 叢集上的簡單使用者驗證。 下載並使用下列步驟的 hello 使用此指令碼。 您也可以修改此指令碼，或使用任何其他方法 tooestablish passwordless SSH 驗證 hello 叢集計算節點之間。

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

toorun hello 指令碼，您會需要 tooknow hello 前置詞的子網路 IP 位址。 執行下列命令，其中一個 hello 叢集節點上的 hello 取得 hello 前置詞。 您的輸出看起來應該像 10.1.3.5，和 hello 前置詞是 hello 10.1.3 部分。

    ifconfig eth0 | grep -w inet | awk '{print $2}'

現在執行 hello 指令碼使用三個參數： hello 一般使用者名稱 hello 計算節點，hello 一般密碼 hello 該使用者計算節點，而且 hello 子網路首碼，從傳回 hello 前一個命令。

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

此指令碼未 hello 遵循：

* 建立名為.ssh，所需之 passwordless 登入的 hello 主機節點上的目錄。
* 指示 passwordless 登入 tooallow 登入，從 hello 叢集中任何節點的 hello.ssh 目錄中建立組態檔。
* 建立檔案，其中包含 hello 節點名稱與節點 hello 叢集中的所有 hello 節點的 IP 位址。 這些檔案會保留供日後參考執行 hello 指令碼之後。
* 建立私人和公用金鑰組，每個叢集節點 （包括 hello 主機節點） 與 hello authorized_keys 檔案中建立項目。

> [!WARNING]
> 執行這個指令碼可能會建立潛在的安全性風險。 請確定未發佈的 hello 公開金鑰資訊 ~/.ssh。
>
>

## <a name="configure-intel-mpi"></a>設定 Intel MPI
在 Azure Linux RDMA toorun MPI 應用程式，您需要 tooconfigure 某些環境變數特定 tooIntel MPI。 以下是範例 Bash 指令碼 tooconfigure hello 變數需要 toorun 應用程式。 Hello 路徑 toompivars.sh 視需要變更設定的 Intel MPI。

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

如下所示為 hello hello 主機檔案格式。 針對叢集中的每個節點加入一行指令碼。 指定從 hello 虛擬網路的私人 IP 位址定義更早版本，不是 DNS 名稱。 例如，對於兩個具有 10.32.0.1 和 10.32.0.2 的 IP 位址的主機，hello 檔案包含 hello 下列：

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>在基本的雙節點叢集上執行 MPI
如果您尚未這樣做，請先設定 hello 環境 Intel MPI。

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>執行 MPI 命令
MPI 上執行命令 hello 計算節點 tooshow MPI 已正確安裝，而且可以進行通訊，其中至少兩個計算節點之間。 hello 下列**mpirun**命令執行 hello **hostname**命令在兩個節點上。

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
您的輸出應該會列出所有 hello 節點做為輸入傳遞的 hello 名稱`-hosts`。 例如， **mpirun**包含兩個節點的命令會傳回類似 hello 下列輸出：

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>執行 MPI 基準測試
hello 下列 Intel MPI 命令執行 pingpong 基準 tooverify hello 叢集設定和連線 toohello RDMA 網路。

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

在使用叢集包含兩個節點上，您應該會看到類似 hello 下列輸出。 在 hello Azure RDMA 網路上，預期或低於 too512 位元組組成的訊息大小為 3 百萬分之一秒為單位的延遲。

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>後續步驟
* 在 Linux 叢集上部署並執行 Linux MPI 應用程式。
* 請參閱 hello [Intel MPI 程式庫文件](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/)如 Intel MPI 的指引。
* 再試一次[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos)toocreate Intel Lustre 叢集使用 CentOS 架構 HPC 映像。 如需詳細資訊，請參閱[在 Microsoft Azure 上部署 Lustre 的 Intel 雲端版本](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/)。
