---
title: "aaaDevTest 實驗室概念 |Microsoft 文件"
description: "深入了解的 DevTest Labs hello 基本概念，它可讓您輕鬆 toocreate，如何管理和監視 Azure 虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>研發/測試實驗室概念
## <a name="overview"></a>概觀
下列清單中的 hello 包含重要的 DevTest Labs 概念和定義：

## <a name="labs"></a>實驗室
實驗室環境是 hello 基礎結構包含一組資源，例如可讓您更佳的虛擬機器 (Vm)，藉由指定限制和配額管理這些資源。

## <a name="virtual-machine"></a>虛擬機器
Azure VM 是由 Azure 所提供的[隨選且可調整的數種運算資源](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm)類型之一。 Azure Vm 提供，而不需要 toobuy hello 虛擬化的彈性，並維護 hello 實體硬體執行，但您仍須 toomaintain hello VM 上執行特定工作，例如設定、 修補及安裝 hello 軟體在其上執行。

[Azure 中的 Windows 虛擬機器概觀](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview)提供您在建立 VM 之前應該考慮的事項、建立方式及管理方式的相關資訊。

## <a name="claimable-vm"></a>可宣告 VM
Azure 可宣告 VM 是可供任何具有權限的實驗室使用者使用的虛擬機器。 實驗室系統管理員可以使用特定的基底映像和成品準備 Vm，並將它們儲存 tooa 共用集區。 實驗室使用者在需要一個包含該特定的設定時，可以再宣告 hello 集區中的 VM 可運作。

VM 若是位於 claimable 一開始未指派 tooany 特定使用者，但會顯示在 「 Claimable 虛擬機器 」 底下的每位使用者的清單。 VM 宣告的使用者之後，它是 「 我的虛擬機器 」 區域中上移 tootheir 且不再 claimable 任何其他使用者。

## <a name="environment"></a>Environment
在 DevTest 實驗室環境是指 tooa 實驗室中的 Azure 資源集合。 [此部落格文章](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/)討論如何從您的 Azure Resource Manager 範本 toocreate 多部 VM 環境。

## <a name="base-images"></a>基礎映像
基底映像會使用所有的 hello 工具和設定預先安裝的 VM 映像，並設定的 tooquickly 建立 VM。 您可以佈建 VM 挑選現有的基礎，並加入成品 tooinstall 測試代理程式。 您可以再儲存 hello 佈建 VM 為基底，以便 hello 基底可以使用而不需要 tooreinstall hello 測試代理程式的每個佈建 hello VM。

## <a name="artifacts"></a>構件
使用的 toodeploy 和成品佈建 VM 之後，設定您的應用程式。 構件可以是：

* 您想 tooinstall 上 hello VM-例如代理程式、 Fiddler 及 Visual Studio 的工具。
* 您想在 hello VM-toorun，諸如複製儲存機制的動作。
* 您想 tootest 應用程式。

成品是[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)包含指示 tooperform 部署，並將設定套用的 JSON 檔案。

## <a name="artifact-repositories"></a>構件儲存機制
構件儲存機制是已簽入構件的 Git 儲存機制。 成品儲存機制可以加入 toomultiple 實驗室中重複使用及共用您的組織。

## <a name="formulas"></a>公式
加法 toobase 映像中的公式，提供的快速 VM 佈建的機制。 DevTest 實驗室中的公式是預設屬性值使用 toocreate 實驗室 VM 的清單。
使用公式，以 hello 相同設定的屬性-例如基底映像、 VM 大小、 虛擬網路和成品-Vm 可以建立而不需要 toospecify 這些內容每次。 在建立 VM 時由公式，hello 預設值可以當做-或修改。

## <a name="policies"></a>原則
原則可協助控制實驗室中的成本。 例如，您可以建立原則 tooautomatically 關閉 Vm，根據定義的排程。

## <a name="caps"></a>最高限度
端點是在您的實驗室機制 toominimize 浪費。 例如，您可以設定 cap toorestrict hello 數目可以為每位使用者，或在實驗室中建立的 Vm。

## <a name="security-levels"></a>安全性層級
安全性存取權是由 Azure 角色型存取控制 (RBAC) 所決定。 toounderstand 存取的方式運作，這樣做，toounderstand hello 之間差異的權限、 角色，以及範圍所定義的 RBAC。

* 權限的權限會定義的存取 tooa 特定動作 （例如讀取權限 tooall 虛擬機器）。
* 角色的角色是一組權限可以指派 tooa 使用者和群組。 例如，hello*訂用帳戶擁有者*角色有存取 tooall 訂用帳戶內的資源。
* 範圍-範圍是中的 Azure 資源，例如資源群組、 單一實驗室中或 hello 整個訂閱 hello 階層的層級。

Hello 在範圍內的 DevTest Labs，有兩種類型的角色 toodefine 使用者權限： 實驗室擁有者和實驗室使用者。

* 實驗室的實驗室擁有者擁有者存取 tooany hello 實驗室內的資源。 因此，實驗室擁有者可以修改原則、 讀取和寫入任何 Vm、 變更 hello 虛擬網路，並以此類推。
* 實驗室使用者 - 實驗室使用者可以檢視所有實驗室資源，例如 VM、原則和虛擬網路，但不能修改原則或任何由其他使用者所建立的 VM。

toosee 如何 toocreate DevTest 實驗室中的自訂角色，請參閱 toohello 文章[toospecific 實驗室原則授與使用者權限](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)。

由於範圍是階層形式，當使用者擁有特定範圍的權限時，就會自動獲得該範圍所包含的每個較低層級範圍的權限。 比方說，如果使用者被指派 toohello 訂用帳戶擁有者的角色，則他們有存取 tooall 訂閱中的資源，包括所有虛擬機器、 所有虛擬網路，以及所有實驗室。 因此，訂閱擁有者會自動繼承 hello 實驗室擁有者的角色。 但是，並非反之亦然 hello 相反。 實驗室擁有者具有存取 tooa 實驗室中，也就是比 hello 訂用帳戶層級較低的領域。 因此，實驗室擁有者不會無法 toosee 虛擬機器或虛擬網路或實驗室 hello 外的任何資源。

## <a name="azure-resource-manager-templates"></a>Azure 資源管理員範本
所有使用 Azure 資源管理員範本，可讓您也可以設定本文所討論的概念 hello 定義 hello 基礎結構/Azure 方案的組態，並重複地部署處於一致的狀態。

[了解 hello 結構和語法的 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format)描述 hello 結構 hello 的範本的不同區段的 Azure 資源管理員範本和 hello 屬性。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
[在研測實驗室中建立實驗室](devtest-lab-create-lab.md)
