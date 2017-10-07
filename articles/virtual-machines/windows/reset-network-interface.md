---
title: "aaaHow tooreset 網路介面，讓 Windows Azure VM 與 |Microsoft 文件"
description: "示範如何 tooreset Azure Windows VM 的網路介面"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>如何 tooreset Azure Windows VM 的網路介面 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

無法連線 tooMicrosoft Azure Windows 虛擬機器 (VM)，停用 hello 預設網路介面 (NIC) 之後，或是手動設定靜態 ip 位址的 hello nic。 本文將說明如何 tooreset hello Azure Windows vm，將會解決 hello 遠端連線問題的網路介面。

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>重設網路介面

### <a name="for-classic-vms"></a>適用於傳統 VM

tooreset 網路介面，依照下列步驟：

1.  移 toohello [Azure 入口網站]( https://ms.portal.azure.com)。
2.  選取 [虛擬機器 (傳統)]。
3.  選取 hello 影響虛擬機器。
4.  選取 [IP 位址]。
5.  如果 hello**私用 IP 指派**不**靜態**，將它變更太**靜態**。
6.  變更 hello **IP 位址**tooanother hello 子網路中可用的 IP 位址。
7.  選取 [儲存]。
8.  hello 虛擬機器會重新啟動 tooinitialize hello 新 NIC toohello 系統。
9.  請嘗試 tooRDP tooyour 機器。 如果成功的話，您可以變更 hello 私人 IP 位址後 toohello 原始，如果您想要。 或是維持現有設定。 

### <a name="for-vms-deployed-in-resource-group-model"></a>適用於部署在資源群組模型中的 VM

1.  移 toohello [Azure 入口網站]( https://ms.portal.azure.com)。
2.  選取 hello 影響虛擬機器。
3.  選取 [網路介面]。
4.  選取與您的電腦的網路介面相關聯的 hello
5.  選取 [IP 組態]。
6.  選取 hello IP。 
7.  如果 hello**私用 IP 指派**不**靜態**，將它變更太**靜態**。
8.  變更 hello **IP 位址**tooanother hello 子網路中可用的 IP 位址。
9. hello 虛擬機器會重新啟動 tooinitialize hello 新 NIC toohello 系統。
10. 請嘗試 tooRDP tooyour 機器。 如果成功的話，您可以變更 hello 私人 IP 位址後 toohello 原始，如果您想要。 或是維持現有設定。 

## <a name="delete-hello-unavailable-nics"></a>刪除 hello 無法使用 Nic
您可以遠端桌面 toohello 機器之後，您必須刪除 hello 舊 Nic tooavoid hello 潛在的問題：

1.  開啟 [裝置管理員]。
2.  選取 [檢視] > [顯示隱藏的裝置]。
3.  選取 [網路介面卡]。 
4.  檢查名為"Microsoft HYPER-V 網路介面卡 」 的 hello 配接器。
5.  無法使用的介面卡會以灰色來顯示。以滑鼠右鍵按一下 hello 配接器，然後選取 解除安裝。

    ![hello NIC hello 映像](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > 只解除安裝具有 hello 名稱"Microsoft HYPER-V 網路介面卡 」 的 hello 無法使用配接器。 如果您解除安裝任何 hello 其他隱藏的配接器，它可能會導致其他問題。
    >
    >

6.  現在應該已經從系統清除所有無法使用的介面卡。