---
title: "在 Azure 入口網站建立虛擬機器擴展集 | Microsoft Docs"
description: "了解如何在 Azure 入口網站快速建立虛擬機器擴展"
keywords: "虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 12/19/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a501a852a317ec7d087904c3a675ebefce1bece0
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="create-a-virtual-machine-scale-set-in-the-azure-portal"></a>在 Azure 入口網站建立虛擬機器擴展集
虛擬機器擴展集可讓您部署和管理一組相同、自動調整的虛擬機器。 您可以手動調整擴展集中的 VM 數目，或定義規則以根據如 CPU、記憶體需求或網路流量的資源使用量來自動調整。 在本使用者入門文章中，您會在 Azure 入口網站建立虛擬機器擴展集。 您還可以使用 [Azure CLI 2.0](virtual-machine-scale-sets-create-cli.md) 或 [Azure PowerShell](virtual-machine-scale-sets-create-powershell.md) 來建立擴展集。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。


## <a name="log-in-to-azure"></a>登入 Azure
登入 Azure 入口網站，網址是 http://portal.azure.com/。


## <a name="create-virtual-machine-scale-set"></a>建立虛擬機器擴展集
您可以使用 Windows Server 映像或 Linux 映像 (例如 RHEL、CentOS、Ubuntu 或 SLES) 部署擴展集。

1. 按一下 Azure 入口網站左上角的 [新增] 按鈕。
2. 搜尋*擴展集*，選擇 [虛擬機器擴展集]，然後選取 [建立]。
3. 輸入擴展集的名稱，例如 *myScaleSet*。
4. 選取所需的 OS 類型，例如 *Windows Server 2016 Datacenter*。
5. 輸入所需的資源群組名稱 (例如 *myResourceGroup*) 和位置 (例如*美國東部*)。
6. 輸入所需的使用者名稱，然後選取偏好的驗證類型。
    - **密碼**長度必須至少有 12 個字元，且符合下列四個複雜性需求的其中三項：1 個小寫字元、1 個大寫字元、1 個數字和 1 個特殊字元。 如需詳細資訊，請參閱[使用者名稱和密碼需求](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)。
    - 如果您選取 Linux OS 磁碟映像，可以改為選擇 [SSH 公開金鑰]。 在此只需提供您的公開金鑰，例如 *~/.ssh/id_rsa.pub*。 您可以從入口網站使用 Azure Cloud Shell [建立及使用 SSH 金鑰](../virtual-machines/linux/mac-create-ssh-keys.md)。

7. 輸入**公用 IP 位址名稱**，例如 *myPublicIP*。
8. 輸入唯一的**網域名稱標籤**，例如 *myuniquedns*。 此 DNS 標籤會成為擴展集前方負載平衡器 FQDN 的基底。
9. 若要確認擴展集選項，請選取 [建立]。

    ![在 Azure 入口網站建立虛擬機器擴展集](./media/virtual-machine-scale-sets-create-portal/create-scale-set.png)


## <a name="connect-to-a-vm-in-the-scale-set"></a>連線到擴展集中的 VM
當您在入口網站建立擴展集時，會建立負載平衡器。 網路位址轉譯 (NAT) 規則可針對如 RDP 或 SSH 的遠端連線，將流量分散到各個擴展集執行個體。

若要檢視您的擴展集執行個體的 NAT 規則與連線資訊：

1. 選取您在上一個步驟中建立的資源群組名稱，例如 *myResourceGroup*。
2. 從資源的清單中，選取您的**負載平衡器**，例如 *myScaleSetLab*。
3. 從視窗左側的功能表中選擇 [輸入 NAT 規則]。

    ![輸入 NAT 規則可讓您連線到虛擬機器擴展集執行個體](./media/virtual-machine-scale-sets-create-portal/inbound-nat-rules.png)

您可以使用下列 NAT 規則來連線到擴展集中的每個 VM。 每個 VM 執行個體都會列出目的地 IP 位址與 TCP 通訊埠值。 例如，如果目的地 IP 位址是 *104.42.1.19* 而 TCP 通訊埠是 *50001*，便會連線到如下的 VM 執行個體：

- 如果是 Windows 擴展集，請使用 RDP 連線到 `104.42.1.19:50001` 的 VM 執行個體
- 如果是 Linux 擴展集，請使用 SSH 連線到 `ssh azureuser@104.42.1.19 -p 50001` 的 VM 執行個體

出現提示時，請輸入您在上一個步驟建立擴展集時所指定的認證。 擴展集執行個體是標準的 VM，您可以採用一般方式與它互動。 如需如何在擴展集執行個體上部署和執行應用程式的詳細資訊，請參閱[在虛擬機器擴展集上部署您的應用程式](virtual-machine-scale-sets-deploy-app.md)


## <a name="clean-up-resources"></a>清除資源
如果不再需要，請刪除資源群組、擴展集和所有相關資源。 若要這樣做，請選取 VM 的資源群組，然後按一下 [刪除]。


## <a name="next-steps"></a>後續步驟
在本使用者入門文章中，您在 Azure 入口網站建立了基本的擴展集。 如需更佳的延展性和自動化，請使用下列使用說明文章展開您的擴展集：

- [在虛擬機器擴展集上部署您的應用程式](virtual-machine-scale-sets-deploy-app.md)
- 利用 [Azure PowerShell](virtual-machine-scale-sets-autoscale-powershell.md)、[Azure CLI](virtual-machine-scale-sets-autoscale-cli.md) 或 [Azure 入口網站](virtual-machine-scale-sets-autoscale-portal.md)自動縮放
- [將自動作業系統升級用於擴展集 VM 執行個體](virtual-machine-scale-sets-automatic-upgrade.md)
