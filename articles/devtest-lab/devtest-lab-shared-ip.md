---
title: "aaaUnderstand 共用 Azure DevTest Labs 中的 IP 位址 |Microsoft 文件"
description: "了解如何 Azure DevTest Labs 會使用共用的 IP 位址 toominimize hello 公用 IP 位址需要的 tooaccess 實驗室 Vm。"
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>了解 Azure DevTest Labs 中的共用 IP 位址

Azure 的 DevTest Labs 可讓實驗室 Vm 共用 hello 相同公用 IP 位址 toominimize hello 數目的公用 IP 位址需要 tooaccess 個別實驗室 Vm。  本文說明共用 IP 的運作方式和其相關的組態選項。

## <a name="shared-ip-setting"></a>共用 IP 設定

當您建立實驗室時，它會位於虛擬網路的子網路。  根據預設，此子網路建立與**啟用共用公用 IP**設定得*是*。  此設定會建立一個 hello 整個子網路的公用 IP 位址。  如需設定虛擬網路和子網路的詳細資訊，請參閱[設定 Azure DevTest Labs 中的虛擬網路](devtest-lab-configure-vnet.md)。

![新的實驗室子網路](media/devtest-lab-shared-ip/lab-subnet.png)

針對現有的實驗室，您可以藉由選取 [設定和原則 > 虛擬網路] 來啟用這個選項。 然後，從 hello 清單中選取虛擬網路，並選擇 **啟用共用的公用 IP**選子網路。 如果您不要跨實驗室 Vm tooshare 公用 IP 位址，您也可以停用任何實驗室中的這個選項。

這個實驗室預設 toousing 中所建立的共用的 IP 任何 Vm。  此設定在建立 hello VM 時，會出現在 hello**進階設定**刀鋒視窗底下**IP 位址設定**。

![新的 VM](media/devtest-lab-shared-ip/new-vm.png)

- **共用：**建立為**共用**的所有 VM 歸類到一個資源群組 (RG)。 單一 IP 位址會指派該 RG 和 hello RG 中所有的 Vm 將會使用該 IP 位址。
- **公用：**您建立的每個 VM 有它自己的 IP 位址，而且建立在它自己的資源群組。
- **私人：**您建立的每個 VM 使用私人 IP 位址。 您將不會直接從 hello 無法 tooconnect toothis VM 網際網路的遠端桌面。

具有共用 IP 已啟用的 VM 加入 toohello 子網路，每當 DevTest Labs 自動加入 hello VM tooa 負載平衡器，並將 hello 公用 IP 位址的 TCP 連接埠號碼指派轉送 toohello hello VM 上的 RDP 連接埠。  

## <a name="using-hello-shared-ip"></a>使用 hello 共用 IP

- **Linux 使用者：** SSH toohello VM 使用 hello IP 位址或完整的網域名稱，後面接著冒號，後面接著 hello 連接埠。 例如，在 hello 圖，hello RDP 位址 tooconnect toohello VM 是`doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`。

  ![VM 範例](media/devtest-lab-shared-ip/vm-info.png)

- **Windows 使用者：**選取 hello**連接**按鈕 hello Azure 入口網站 toodownload 預先設定的 RDP 檔案，並存取 hello VM。

## <a name="next-steps"></a>後續步驟

* [在 Azure DevTest Labs 中定義實驗室原則](devtest-lab-set-lab-policy.md)
* [在 Azure DevTest Labs 中設定虛擬網路](devtest-lab-configure-vnet.md)





