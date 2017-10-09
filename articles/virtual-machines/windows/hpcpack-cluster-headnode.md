---
title: "Azure VM 中的 HPC Pack 前端節點 aaaCreate |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站與 hello 資源管理員部署的模型 toocreate Azure VM 中的 Microsoft HPC Pack 2012 R2 前端節點。"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>建立 Azure VM 使用 Marketplace 映像中的 hello HPC Pack 叢集前端節點
使用[Microsoft HPC Pack 2012 R2 虛擬機器映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)從 hello Azure Marketplace 和 hello Azure 入口網站 toocreate hello 前端節點的 HPC 叢集。 此 HPC Pack VM 映像是基於已預先安裝 HPC Pack 2012 R2 Update 3 的 Windows Server 2012 R2 Datacenter。 使用此前端節點當作 Azure 中 HPC Pack 的概念證明部署。 您可以新增計算節點 toohello 叢集 toorun HPC 工作負載。

> [!TIP]
> toodeploy 完整的 HPC Pack 2012 R2 叢集，包括 hello 前端節點和計算節點的 Azure 中，我們建議您最好使用自動化的方式。 選項包括 hello [HPC Pack IaaS 部署指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)和資源管理員範本，例如 hello [Windows 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)。 此外，也有 [Microsoft HPC Pack 2016 叢集](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates)的 Resource Manager 範本可供使用。 
> 
> 

## <a name="planning-considerations"></a>規劃考量
Hello 遵循圖所示，您部署在 Azure 的虛擬網路中 Active Directory 網域中 hello HPC Pack 前端節點。

![HPC Pack 前端節點][headnode]

* **Active Directory 網域**: hello 必須是前端節點的 HPC Pack 2012 R2 tooan Active Directory 網域，在 Azure 中的啟動之前加入您 hello HPC services hello VM 上。 本文中，概念證明部署中所示，您可以升級 hello 您建立 hello 前端節點做為網域控制站才能啟動 hello HPC 服務的 VM。 另一個選項是 toodeploy 另一個網域控制站和樹系中您所加入的 Azure toowhich hello 前端節點 VM。

* **部署模型**： 對於大部分的新部署，Microsoft 建議您使用 hello Resource Manager 部署模型。 本文假設您使用此部署模型。

* **Azure 虛擬網路**： 當您使用 hello 資源管理員部署模型 toodeploy hello 前端節點時，您指定或建立 Azure 虛擬網路。 如果您需要 toojoin hello 前端節點 tooan 現有 Active Directory 網域，您可以使用 hello 虛擬網路。 您也需要更新 tooadd 計算節點 Vm toohello 叢集。

## <a name="steps-toocreate-hello-head-node"></a>步驟 toocreate hello 前端節點
以下是高層級步驟 toouse hello Azure 入口網站 toocreate Azure VM 的 hello HPC Pack 前端節點使用 hello Resource Manager 部署模型。 

1. 如果您想 toocreate 新 Active Directory 樹系在 Azure 中使用不同的網域控制站 Vm，其中一個選項是 toouse [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc)。 簡單概念證明部署，有好 tooomit 此步驟中，並將 hello 前端節點 VM 本身設定為網域控制站。 本文稍後將說明此選項。
2. 在 [hello [HPC Pack 2012 R2，在 Windows Server 2012 R2] 頁面上](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)hello Azure Marketplace，在按一下**建立虛擬機器**。 
3. 在 hello 入口網站上 hello **HPC Pack 2012 R2，Windows Server 2012 R2 上**頁面上，選取 hello**資源管理員**部署模型，然後按一下**建立**。
   
    ![HPC Pack 映像][marketplace]
4. 使用 hello 入口 tooconfigure hello 設定並建立 hello VM。 如果您是新 tooAzure，請遵循 hello 教學課程[hello Azure 入口網站中建立 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 概念證明部署，您通常可以接受 hello 預設或建議的設定。
   
   > [!NOTE]
   > 如果您想 toojoin hello 前端節點 tooan 現有的 azure Active Directory 網域，請確定您建立 hello VM 時指定 hello 該網域的虛擬網路。
   > 
   > 
5. 您建立 hello VM 和 hello VM 正在執行之後,[連接 toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)透過遠端桌面。 
6. 加入 hello VM tooan Active Directory 網域的樹系選擇其中一個 hello 下列選項：
   
   * 如果您在 Azure 虛擬網路與現有的網域樹系中建立 hello VM，請使用標準伺服器管理員或 Windows PowerShell 工具將 hello VM toohello 樹系。 然後重新啟動。
   * 如果您在新的虛擬網路 （不含現有的網域樹系） 中建立 hello VM，然後將 hello VM 升級為網域控制站。 使用標準步驟 tooinstall 並 hello 前端節點上設定 hello Active Directory 網域服務角色。 如需詳細步驟，請參閱 [安裝新的 Windows Server 2012 Active Directory 樹系](https://technet.microsoft.com/library/jj574166.aspx)。
7. 之後 hello VM 正在執行，而且是聯結的 tooan Active Directory 樹系，請啟動 hello HPC Pack 服務，如下所示：
   
    a. 連接 toohello 前端節點 VM 使用 hello 本機 Administrators 群組成員的網域帳戶。 例如，使用您建立 hello 前端節點 VM 時設定的 hello 系統管理員帳戶。
   
    b. 針對預設前端節點組態，系統管理員身分啟動 Windows PowerShell 並輸入 hello 下列：
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    可能需要幾分鐘的時間 hello HPC Pack services toostart。
   
    如需其他前端節點組態選項，請輸入 `get-help HPCHNPrepare.ps1`。

## <a name="next-steps"></a>後續步驟
* 您現在可以使用 hello HPC Pack 叢集前端節點。 例如，啟動 HPC 叢集管理員，並完成 hello[部署待辦事項清單](https://technet.microsoft.com/library/jj884141.aspx)。
* 如果您想 tooincrease hello 叢集計算容量隨，新增[Azure 高載節點](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)雲端服務中。 
* 請嘗試在 hello 叢集上執行測試工作負載。 如需範例，請參閱 hello HPC Pack[入門指南](https://technet.microsoft.com/library/jj884144)。

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
