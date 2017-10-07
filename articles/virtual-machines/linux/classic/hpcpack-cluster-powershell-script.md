---
title: "aaaPowerShell 指令碼 toodeploy Linux HPC 叢集 |Microsoft 文件"
description: "在 Azure 虛擬機器中執行 PowerShell 指令碼 toodeploy Linux HPC Pack 2012 R2 叢集"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Hello HPC Pack IaaS 部署指令碼以建立 Linux 高效能運算 (HPC) 叢集
在 Azure 虛擬機器中執行 hello HPC Pack IaaS 部署 PowerShell 指令碼 toodeploy 完整的 HPC Pack 2012 R2 叢集，針對 Linux 工作負載。 hello 叢集包含一個已加入 Active Directory 的前端節點執行 Windows Server 和 Microsoft HPC Pack，並執行其中一個 hello HPC Pack 所支援的 Linux 發行版本的計算節點。 如果您想 toodeploy Azure for Windows 的工作負載中的 HPC Pack 叢集，請參閱[hello HPC Pack IaaS 部署指令碼以建立 Windows HPC 叢集](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 您也可以使用 Azure Resource Manager 範本 toodeploy HPC Pack 叢集。 如需範例，請參閱 [使用 Linux 計算節點建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)。

> [!IMPORTANT] 
> hello 本文中所述的 PowerShell 指令碼會建立 Microsoft HPC Pack 2012 R2 叢集，在 Azure 中使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。
> 此外，本文中所述的 hello 指令碼不支援使用 HPC Pack 2016。

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>範例組態檔
hello 下列組態檔建立的網域控制站和網域樹系及部署 HPC Pack 叢集有一個具有本機資料庫的前端節點和 10 Linux 計算節點。 所有的 hello 雲端服務都會直接建立在 hello 東亞 」 位置。 hello Linux 運算節點會建立兩個雲端服務和兩個儲存體帳戶中 (也就是*MyLnxCN 0001*至*MyLnxCN 0005*中*MyLnxCNService01*和*mylnxstorage01*，和*MyLnxCN 0006*至*MyLnxCN 0010*中*MyLnxCNService02*和*mylnxstorage02*). hello 運算節點會建立從 OpenLogic CentOS 7.0 版 Linux 映像。 

取代您自己的值為您的訂用帳戶名稱及 hello 帳戶和服務名稱。

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>疑難排解
* **「VNet 不存在」錯誤**。 如果您 hello HPC Pack IaaS 部署指令碼 toodeploy 多個叢集在 Azure 中同時執行一個訂用帳戶，一或多個部署可能會失敗，錯誤碼為 hello 「 VNet *VNet\_名稱*不存在 」。
  如果發生這個錯誤，重新執行失敗的 hello 部署的 hello 指令碼。
* **問題存取 hello Azure 虛擬網路從 hello 網際網路**。 如果您建立新的網域控制站 HPC Pack 叢集使用 hello 部署指令碼，或您手動升級為前端節點 VM toodomain 控制站，您可能會遇到 hello Vm 在 hello Azure 虛擬網路 toohello 網際網路連線的問題。 如果 hello 網域控制站，會自動設定轉寄站 DNS 伺服器，而且未正確解析此轉寄站 DNS 伺服器，也可能會發生。
  
    toowork 解決這個問題，請設定有效的轉寄站 DNS 伺服器，或登入 toohello 網域控制站，移除 hello 轉寄站組態設定。 伺服器管理員 中，按一下的 toodo**工具** > **DNS** tooopen DNS 管理員 中，然後按兩下**轉寄站**。

## <a name="next-steps"></a>後續步驟
* 請參閱[開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)有關支援之 Linux 發行套件，移動資料，並送出含有 Linux 作業 tooan HPC Pack 叢集計算節點。
* 如需使用 hello 指令碼 toocreate 叢集並執行 Linux HPC 工作負載的教學課程，請參閱：
  * [在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD](hpcpack-cluster-namd.md)
  * [在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 OpenFOAM](hpcpack-cluster-openfoam.md)
  * [在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 STAR-CCM+](hpcpack-cluster-starccm.md)

