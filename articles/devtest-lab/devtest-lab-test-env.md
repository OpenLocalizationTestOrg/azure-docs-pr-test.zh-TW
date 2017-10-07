---
title: "VM 和 PaaS aaaUse Azure DevTest Labs 測試環境 |Microsoft 文件"
description: "了解如何 toouse Azure DevTest Labs VM 和 PaaS 測試環境的案例。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>為 VM 和 PaaS 測試環境使用 Azure DevTest Labs

您可以使用 Azure DevTest Labs tooimplement 許多案例中，但主要案例牽涉到使用測試人員適用的 DevTest Labs toohost 機器。 

在此案例中，DevTest Labs 提供以下優點：

- 測試人員可以快速佈建 Windows 和 Linux 的環境，使用可重複使用的範本和成品來測試其應用程式的 hello 最新版本。
- 測試人員可以佈建多個測試代理程式，相應增加其負載測試。
- 系統管理員可以確定下列事項以控制成本：
  - 測試人員無法取得超過所需的 VM。
  - VM 不使用時會關閉。

![使用 DevTest Labs 進行訓練](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

在本文中，您會了解各種 Azure DevTest Labs 所使用的功能 toomeet tester 需求，然後 hello 實驗室設定的詳細的步驟 toofollow tooset。

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>實作使用 Azure DevTest Labs 的測試環境
1. **建立 hello 實驗室** 
   
    實驗室會 hello Azure DevTest Labs 中起點。 一旦您建立實驗室環境，您可以執行工作，例如新增使用者 （測試人員） toohello 實驗室、 設定原則 toocontrol 成本，定義可以快速，建立的 VM 映像等等。  
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure 研測實驗室中建立實驗室](devtest-lab-create-lab.md) |了解如何在 Azure 中的 DevTest Labs 實驗室的 toocreate hello Azure 入口網站。 |
2. **使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立 VM** 
   
    您可以在 hello Azure Marketplace 中挑選現成的映像，從各種不同的映像，並讓它們可在 hello 實驗室中。 如果 hello 現成的映像不符合您的需求，您可以建立自訂映像建立的實驗室使用現成的映像，從 Azure Marketplace，安裝所有的 hello 軟體，您需要和儲存 hello VM 做為 hello 實驗室中的自訂映像的 VM。

    如果您要使用自訂映像，請考慮使用映像原廠 toocreate，並將您的映像發佈。 映像處理站是設定即程式碼的解決方案，定期自動建置及散發已設定的映像。 此儲存 hello 所需時間 toomanually hello 與建立 VM 之後，請設定 hello 系統基底 OS。
  
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [設定 Azure Marketplace 映像](devtest-lab-configure-marketplace-images.md) |了解如何白名單 Azure Marketplace 映像，讓選取範圍只有 hello 映像，您可以使用您想要在 hello 測試人員。|
   | [建立自訂映像](devtest-lab-create-template.md) |建立自訂映像預先安裝，讓測試人員可以快速地建立使用 hello 自訂映像的 VM，您需要的 hello 軟體。|
   | [了解映像處理站](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |觀看影片說明如何 tooset 並使用映像處理站。|

3. **建立測試電腦可重複使用的範本** 
   
    Azure DevTest Labs 中的公式是一份預設屬性值使用 toocreate VM。 您可以挑選的映像、 VM 大小 （結合 CPU 和 RAM） 和虛擬網路，hello 實驗室中建立公式。 每個測試人員可以看到 hello 實驗室中的 hello 公式，並使用 toocreate VM。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [管理 DevTest Labs 公式 toocreate Vm](devtest-lab-manage-formulas.md) |了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。|

3. **建立多部 VM 的測試環境** 
   
    您可以使用 Azure Resource Manager 範本 toodefine hello 基礎結構和 Azure 方案的組態，並重複地部署多個測試 Vm 處於一致的狀態。

    Azure PaaS 資源可以佈建在 Resource Manager 範本環境中，並以成本追蹤顯示。 不過，VM 自動關機不適用 tooPaaS 資源。

    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [透過 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源](devtest-lab-create-environment-from-arm.md) |了解如何以一致的狀態為測試環境部署多部 VM。|

4. **建立成品 tooenable 彈性 VM 自訂**

   使用的 toodeploy 和成品佈建 VM 之後，設定您的應用程式。 構件可以是：

   - 您想 tooinstall 上 hello VM-例如代理程式、 Fiddler 及 Visual Studio 的工具。
   - 您想在 hello VM-toorun，諸如複製儲存機制的動作。
   - 您想 tootest 應用程式。

   許多構件為現成可用。 但如果想要符合特定需求的更多自訂，您可以建立自己的自訂構件。

   深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [為您的 DevTest Labs VM 建立自訂的構件](devtest-lab-artifact-author.md) |在您的實驗室中建立您自己自訂的成品以利 hello 虛擬機器。|
   | [在 Azure DevTest Labs 中加入 Git 儲存機制 toostore 自訂成品和使用的 Azure Resource Manager 範本](devtest-lab-add-artifact-repo.md) |深入了解如何 toostore 您自己的私用 Git 儲存機制內的自訂成品。|

5. **控制成本**
   
    Azure 的 DevTest Labs 可讓您 tooset 原則 hello 實驗室 toospecify hello 的數目上限可以在 hello 實驗室測試者建立的 Vm 中。 
   
    如果測試小組所擁有的工作排程一組，而且您想 toostop hello 一天的特定時間的所有 hello Vm，然後自動重新啟動它們 hello 遵循一天，您可以輕鬆地完成作業，設定自動關閉及自動啟動原則 hello 實驗室中。 
   
    最後，應用程式開發完成時，您可以刪除所有 hello Vm 同時執行單一的 PowerShell 指令碼。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [定義實驗室原則](devtest-lab-set-lab-policy.md) |Hello 實驗室中設定原則來控制成本。 |
   | [刪除所有 hello 實驗室 Vm 的 PowerShell 指令碼](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |測試完成時，請刪除所有在一個作業中的 hello 實驗室。|

1. **新增虛擬網路 tooa 實驗室** 
   
    每當建立一個實驗室時，DevTest Labs 就會建立新的虛擬網路 (VNET)。 如果您已設定您自己的 VNET – 例如，藉由使用 ExpressRoute 或站對站 VPN – 您可以加入此 VNET tooyour 實驗室虛擬網路設定，使其可建立 Vm 時。

    此外，也沒有 Azure Active Directory 網域聯結成品可用 hello VM 正在建立時所加入 VM tooa 網域。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure DevTest Labs 中設定虛擬網路](devtest-lab-configure-vnet.md) |了解如何 tooconfigure 虛擬網路中使用 Azure DevTest Labs hello Azure 入口網站。|

6. **與每個測試人員共用 hello 實驗室**
   
    使用您分享給測試人員的連結即可直接存取實驗室。 即使沒有 toohave Azure 帳戶，因為它們已[Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。 測試人員看不到其他測試人員建立的 VM。  
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure DevTest Labs 中新增軟體測試人員 tooa 實驗室](devtest-lab-add-devtest-user.md) |使用 hello Azure 入口網站 tooadd 測試人員 tooyour 實驗室。|
   | [新增測試人員 toohello 實驗室使用的 PowerShell 指令碼](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |使用 PowerShell tooautomate 新增測試人員 tooyour 實驗室。 |
   | [取得連結 toohello 實驗室](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |了解測試人員如何透過超連結直接存取實驗室。|

7. **為更多小組自動建立實驗室** 
   
    您可以自動化實驗室建立、 自訂的設定，包括建立資源管理員範本，並使用它 toocreate 相同實驗室次又一次。 
   
    深入了 hello 下表中的 hello 連結，即可：
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [使用 Resource Manager 範本建立實驗室](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。 |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

