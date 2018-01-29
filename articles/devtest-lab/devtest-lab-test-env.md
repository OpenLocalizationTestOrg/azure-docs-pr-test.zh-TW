---
title: "為 VM 和 PaaS 測試環境使用 Azure DevTest Labs | Microsoft Docs"
description: "了解如何為 VM 和 PaaS 測試環境案例使用 Azure DevTest Labs。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: v-craic
ms.openlocfilehash: dc54b1638fbea577f383ead47b83d29e677cd78f
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a>為 VM 和 PaaS 測試環境使用 Azure DevTest Labs

您可以使用 Azure DevTest Labs 實作許多重要案例，但是主要案例要有關使用 DevTest Labs 來託管測試人員的電腦。 

在此案例中，DevTest Labs 提供以下優點：

- 測試人員可以利用可重複使用的範本和構件，快速佈建 Windows 和 Linux 環境，來測試其最新版的應用程式。
- 測試人員可以佈建多個測試代理程式，相應增加其負載測試。
- 系統管理員可以確定下列事項以控制成本：
  - 測試人員無法取得超過所需的 VM。
  - VM 不使用時會關閉。

![使用 DevTest Labs 進行訓練](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

在本文中，您會了解可用來符合測試人員需求的各種 Azure DevTest Labs 功能，以及可供遵循的實驗室詳細設定步驟。

## <a name="implementing-test-environments-with-azure-devtest-labs"></a>實作使用 Azure DevTest Labs 的測試環境
1. **建立實驗室** 
   
    實驗室是 Azure DevTest Labs 的起點。 建立實驗室之後就可以執行各種工作，例如將使用者 (測試人員) 新增至實驗室、設定原則來控制成本，以及定義可以快速建立的 VM 映像等等。  
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure 研測實驗室中建立實驗室](devtest-lab-create-lab.md) |了解如何在 Azure 入口網站的 Azure DevTest Labs 中建立實驗室。 |
2. **使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立 VM** 
   
    您可以從 Azure Marketplace 的各種映像中挑選現成的映像，供實驗室使用。 如果現成映像不符合您的需求，您可以透過使用 Azure Marketplace 中的現成映像建立實驗室 VM、安裝所需的所有軟體，並將該 VM 儲存為實驗室中的自訂映像，以建立自訂映像。

    如果您要使用自訂映像，請考慮使用映像處理站建立和散發您的映像。 映像處理站是設定即程式碼的解決方案，定期自動建置及散發已設定的映像。 這可以在使用基礎作業系統建立 VM 之後，節省手動設定系統所需的時間。
  
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [設定 Azure Marketplace 映像](devtest-lab-configure-marketplace-images.md) |了解如何將 Azure Marketplace 映像加入白名單；只開放選取您想讓測試人員使用的映像。|
   | [建立自訂映像](devtest-lab-create-template.md) |預先安裝所需軟體以建立自訂映像，讓測試人員可以使用自訂映像快速建立 VM。|
   | [了解映像處理站](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |觀看如何設定及使用映像處理站的說明影片。|

3. **建立測試電腦可重複使用的範本** 
   
    Azure DevTest Labs 中的公式是用來建立 VM 的預設屬性值清單。 您可以在實驗室中挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。 每位測試人員都能查看實驗室中的公式，並使用它來建立 VM。 
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [管理研發/測試實驗室公式來建立 VM](devtest-lab-manage-formulas.md) |了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。|

3. **建立多部 VM 的測試環境** 
   
    您可使用 Azure Resource Manager 範本定義 Azure 方案的基礎結構和組態，並在一致的狀態中重複部署多個測試 VM。

    Azure PaaS 資源可以佈建在 Resource Manager 範本環境中，並以成本追蹤顯示。 不過，VM 自動關機不適用於 PaaS 資源。

    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [透過 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源](devtest-lab-create-environment-from-arm.md) |了解如何以一致的狀態為測試環境部署多部 VM。|

4. **建立構件以彈性自訂 VM**

   構件是在佈建 VM 之後用來部署和設定您的應用程式。 構件可以是：

   - 您想要在 VM 上安裝的工具 - 例如，代理程式、Fiddler 及 Visual Studio。
   - 您想要在 VM 上執行的動作 - 例如，複製儲存機制。
   - 您想要測試的應用程式。

   許多構件為現成可用。 但如果想要符合特定需求的更多自訂，您可以建立自己的自訂構件。

   按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [為您的 DevTest Labs VM 建立自訂的構件](devtest-lab-artifact-author.md) |在實驗室中為虛擬機器建立自己的自訂構件。|
   | [在 Azure DevTest Labs 中新增可以存放自訂構件和 Azure Resource Manager 範本來使用的 Git 存放庫](devtest-lab-add-artifact-repo.md) |了解如何在您自己的私用 Git 儲存機制中儲存您的自訂構件。|

5. **控制成本**
   
    Azure DevTest Labs 可讓您在實驗室中設定原則，以指定測試人員可在實驗室中建立的 VM 數目上限。 
   
    如果您的測試人員小組有既定的工作時程，而您想要在一天中的某個特定時間停止所有的 VM，然後在隔天自動重新啟動，只要設定實驗室自動關閉和自動啟動原則即可輕鬆達到目的。 
   
    最後，當應用程式開發完成時，您可以執行單一 PowerShell 指令碼一次刪除所有 VM。 
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [定義實驗室原則](devtest-lab-set-lab-policy.md) |在實驗室中設定原則來控制成本。 |
   | [使用 PowerShell 指令碼刪除所有實驗室 VM](devtest-lab-faq.md#how-do-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |當測試完成時，在一次作業中刪除所有實驗室。|

1. **將虛擬網路新增至實驗室** 
   
    每當建立一個實驗室時，DevTest Labs 就會建立新的虛擬網路 (VNET)。 如果您已設定自己的 VNET – 例如，使用 ExpressRoute 或站對站 VPN – 您可以將此 VNET 新增至實驗室的虛擬網路設定，以便在建立 VM 時使用。

    此外，還有 Azure Active Directory 網域聯結構件可用，它會在建立 VM 時將 VM 加入網域。 
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure DevTest Labs 中設定虛擬網路](devtest-lab-configure-vnet.md) |了解如何使用 Azure 入口網站在 Azure DevTest Labs 中設定虛擬網路。|

6. **與每位測試人員共用實驗室**
   
    使用您分享給測試人員的連結即可直接存取實驗室。 他們甚至不必有 Azure 帳戶，只要有 [Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account) 即可。 測試人員看不到其他測試人員建立的 VM。  
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [在 Azure DevTest Labs 中將測試人員新增到實驗室](devtest-lab-add-devtest-user.md) |使用 Azure 入口網站將測試人員新增至實驗室。|
   | [使用 PowerShell 指令碼將測試人員新增至實驗室](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |使用 PowerShell 自動將測試人員新增到實驗室。 |
   | [取得實驗室連結](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |了解測試人員如何透過超連結直接存取實驗室。|

7. **為更多小組自動建立實驗室** 
   
    您可以建立 Resource Manager 範本並一再使用它來建立相同的實驗室，以自動建立實驗室，包括自訂設定。 
   
    按一下下表中的連結以便深入了解︰
   
   | Task | 您學到什麼 |
   | --- | --- |
   | [使用 Resource Manager 範本建立實驗室](devtest-lab-faq.md#how-do-i-create-a-lab-from-a-resource-manager-template) |在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。 |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

