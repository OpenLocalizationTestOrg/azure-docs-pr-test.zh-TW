---
title: "虛擬機器擴展集使用 aaaCreate hello Azure 入口網站 |Microsoft 文件"
description: "使用 Azure 入口網站部署擴展集。"
keywords: "虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>虛擬機器擴展集與 toocreate hello Azure 入口網站的方式
本教學課程會示範是多麼的輕鬆 toocreate 虛擬機器擴展集在短短幾分鐘的時間，使用 hello Azure 入口網站。 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>選擇 hello 商場 hello VM 映像
從 hello 入口網站，您可以輕鬆地部署在擴展集與 CentOS、 CoreOS、 Debian、 開啟 Suse、 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server、 Ubuntu Server 或 Windows Server 映像。

首先，瀏覽 toohello [Azure 入口網站](https://portal.azure.com)網頁瀏覽器中。 按一下`New`，搜尋`scale set`，然後選取 hello`Virtual machine scale set`項目：

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>建立 hello 規模集
現在您可以使用 hello 預設設定，以及快速建立 hello 規模集。

* 在 hello`Basics`刀鋒視窗中，輸入 hello 規模集的名稱。 這個名稱會成為 hello 基底的 hello hello hello 規模集前面的負載平衡器的 FQDN，因此請確定所有 Azure 跨 hello 名稱是唯一。
* 選取所需的 OS 類型，輸入所需的使用者名稱，然後選取偏好的驗證類型。 如果您選擇的密碼，必須至少為 12 個字元，且符合個 hello 四個下列複雜性需求的三種： 一個小寫字元、 一個大寫字元、 一個數字和一個特殊字元。 進一步了解 [使用者名稱和密碼需求](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)。 如果您選擇`SSH public key`，是確定 tooonly 貼上的公用金鑰，不是您的私用索引鍵：

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* 選擇您想 like toolimit hello 規模調整集合 tooa 單一位置 群組，或是否就應該跨越多個位置群組。 允許 hello 規模調整集合 toospan 放置群組允許進行小數位數 （向上 too1 000) 的容量設定超過 100 個 Vm 有一些限制。 如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-placement-groups.md)。
* 輸入所需的資源群組名稱及位置，然後按一下`OK`。
* 在 hello`Virtual machine scale set service settings`刀鋒視窗： 輸入您想要的網域名稱標籤 (hello FQDN hello hello 規模集前面的負載平衡器中的 hello base)。 此標籤在整個 Azure 中必須是唯一的。
* 選擇所需的作業系統磁碟映像、執行個體計數，以及機器大小。
* 選擇您想要的磁碟類型：受管理或未受管理。 如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-managed-disks.md)。 如果您選擇 toohave hello 規模集橫跨多個位置群組，無法使用此選項，因為受管理的磁碟，才能執行規模集 toospan 放置群組。
* 啟用或停用自動調整，並於啟用的情況下進行設定：

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* 在 hello`Summary`刀鋒視窗中，當驗證完成時，按一下`OK`toostart hello 小數位數設定的部署。


## <a name="connect-tooa-vm-in-hello-scale-set"></a>連接 hello 規模集中的 tooa VM
如果您選擇 toolimit 您規模調整集合 tooa 單一位置] 群組，然後 hello 規模調整集合部署了 NAT 規則設定的 toolet 連接 toohello 輕易設定的小數位數 (如果沒有，hello 規模 tooconnect toohello 虛擬機器設定，您可能需要在 toocreate在 [hello jumpbox hello 規模集的相同虛擬網路)。 toosee，瀏覽 toohello `Inbound NAT Rules` hello hello 擴展集的負載平衡器 索引標籤：

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

您可以連接的 tooeach hello 規模的 VM 設定使用這些 NAT 規則。 比方說，Windows 擴展集，如果內送連接埠 50000，NAT 規則您無法連線透過 RDP toothat 機器上`<load-balancer-ip-address>:50000`。 Linux 擴展集，您會使用連接 hello 命令`ssh -p 50000 <username>@<load-balancer-ip-address>`。

## <a name="next-steps"></a>後續步驟
如需如何 toodeploy 小數位數設定從 hello CLI 文件，請參閱[這份文件](virtual-machine-scale-sets-cli-quick-create.md)。

如需從 PowerShell toodeploy 小數位數的設定方式的文件，請參閱[這份文件](virtual-machine-scale-sets-windows-create.md)。

如需如何 toodeploy 小數位數設定從 Visual Studio 的文件，請參閱[這份文件](virtual-machine-scale-sets-vs-create.md)。

如需一般文件，查看 hello[規模集的文件概觀頁面](virtual-machine-scale-sets-overview.md)。

如需一般資訊，請參閱 hello[規模集的主要登陸頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。

