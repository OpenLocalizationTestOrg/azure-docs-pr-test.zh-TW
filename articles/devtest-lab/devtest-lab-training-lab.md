---
title: "定型 aaaUse Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何 toouse Azure DevTest Labs 定型案例。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a>使用 Azure DevTest Labs 進行訓練
Azure 的 DevTest Labs 可使用的 tooimplement 加法 toodev/測試中的許多重要案例。 這些案例的其中一個是 tooset 用於定型的實驗室設定。 Azure 的 DevTest Labs 可讓您 toocreate 實驗室，您可以提供自訂範本位置每個實習生，可以使用 toocreate 相同和隔離的環境進行定型。 您可以套用它們需要的時候，且包含足夠的資源-例如虛擬機器-hello 定型所需時，只有訓練環境，都是可用 tooeach 實習生原則 tooensure。 最後，您可以輕鬆地分享 hello 實驗室受訓，他們可以存取單鍵人員。

![使用 DevTest Labs 進行訓練](./media/devtest-lab-training-lab/devtest-lab-training.png)

Azure 的 DevTest Labs 符合下列需求的任何虛擬環境中的必要的 tooconduct 訓練 hello: 

* 受訓者無法看到其他受訓者所建立的 VM
* 每台訓練用機器應該相同
* 受訓者可以快速佈建其訓練環境
* 控制成本，方法是確保受訓人員無法取得更多的 Vm，比在不使用它們時需要 hello 定型以及關閉 Vm
* 輕鬆地共用每個實習生 hello 訓練實驗室
* 一再重複使用 hello 訓練實驗室

在本文中，您了解可用的各種 Azure DevTest Labs 功能 toomeet hello 先前所述的訓練需求和詳細的步驟，您可以依照 tooset 用於定型的實驗室設定。  

## <a name="implementing-training-with-azure-devtest-labs"></a>使用 Azure DevTest Labs 實作訓練
1. **建立 hello 實驗室** 
   
    實驗室會 hello Azure DevTest Labs 中起點。 一旦您建立實驗室環境，您可以執行的工作，例如當新增使用者 （受訓人員） toohello 實驗室中，設定原則 toocontrol 成本，定義可以快速，建立的 VM 映像等等。   
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure 研測實驗室中建立實驗室](devtest-lab-create-lab.md) |了解如何在 Azure 中的 DevTest Labs 實驗室的 toocreate hello Azure 入口網站。 |
2. **使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立訓練 VM** 
   
    您可以在 hello Azure Marketplace 中挑選現成的映像，從各種不同的映像，並讓它們的 hello 實驗室中的 hello 受訓人員可使用。 如果 hello 現成的映像不符合您的需求，您可以建立自訂映像建立的實驗室使用 Azure marketplace，安裝所有您需要進行 hello 訓練和儲存 hello VM 做為自訂映像 hello 實驗室中的 hello 軟體現成的映像的 VM。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [設定 Azure Marketplace 映像](devtest-lab-configure-marketplace-images.md) |了解如何白名單 Azure Marketplace 映像。您想要的 hello 訓練供只有 hello 映像選取項目。 |
   | [建立自訂映像](devtest-lab-create-template.md) |建立自訂映像預先安裝，讓受訓人員可以快速地建立使用 hello 自訂映像的 VM，您需要 hello 定型 hello 軟體。 |
3. **建立可重複用於訓練機器的範本** 
   
    Azure DevTest Labs 中的公式是一份預設屬性值使用 toocreate VM。 您可以挑選的映像、 VM 大小 （結合 CPU 和 RAM） 和虛擬網路，hello 實驗室中建立公式。 每個實習生可以看到 hello 實驗室中的 hello 公式，並使用 toocreate VM。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [管理 DevTest Labs 公式 toocreate Vm](devtest-lab-manage-formulas.md) |了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。 |
4. **控制成本**
   
    Azure 的 DevTest Labs 可讓您 tooset 原則 hello 實驗室 toospecify hello 的數目上限可由實習生 hello 實驗室中建立的 Vm 中。 
   
    如果您進行多日訓練和 hello 一天的特定時間想 toostop hello 的所有 Vm，然後自動重新啟動後一天的 hello 可以輕鬆地完成該作業所設定的自動關閉並自動啟動 hello 實驗室中的原則。 
   
    最後，完成訓練時您可以刪除所有 hello Vm 同時執行單一的 PowerShell 指令碼。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [定義實驗室原則](devtest-lab-set-lab-policy.md) |Hello 實驗室中設定原則來控制成本。 |
   | [刪除所有 hello 實驗室 Vm 的 PowerShell 指令碼](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |Hello 訓練完成時，請刪除所有在一個作業中的 hello 實驗室。 |
5. **與每個實習生共用 hello 實驗室**
   
    使用您分享給受訓者的連結即可直接存取實驗室。 您受訓人員甚至沒有 toohave Azure 帳戶，因為它們已[Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。 受訓者無法看到其他受訓者所建立的 VM。  
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure DevTest Labs 中加入實習生 tooa 實驗室](devtest-lab-add-devtest-user.md) |使用 hello Azure 入口網站 tooadd 受訓人員 tooyour 訓練實驗室。 |
   | [新增受訓人員 toohello 實驗室使用的 PowerShell 指令碼](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |使用 PowerShell tooautomate 加入受訓人員 tooyour 訓練實驗室。 |
   | [取得連結 toohello 實驗室](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |了解如何透過超連結直接存取實驗室。 |
6. **一再重複使用 hello 實驗室** 
   
    您可以自動化實驗室建立、 自訂的設定，包括建立資源管理員範本，並使用它 toocreate 相同實驗室次又一次。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [使用 Resource Manager 範本建立實驗室](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。 |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

