---
title: "aaaView 並使用虛擬機器的 Azure Resource Manager 範本 |Microsoft 文件"
description: "了解如何 toouse 會 hello Azure 資源管理員範本，從虛擬機器 toocreate 其他 Vm"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>使用虛擬機器的 Azure Resource Manager 範本

您可以在建立時虛擬機器 (VM) 中的 DevTest Labs 透過 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)，儲存 hello VM 之前，您可以檢視 hello Azure Resource Manager 範本。 hello 範本然後可用來當作基礎 toocreate 更具有實驗室 Vm hello 相同的設定。

本文說明如何 tooview hello Resource Manager 範本建立 VM，以及如何 toodeploy 它的更新版本的 tooautomate 建立 hello 相同的 VM。

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>多部 VM 與單一 VM Resource Manager 範本
有兩種方式 toocreate Vm 中使用資源管理員範本的 DevTest Labs: hello Microsoft.DevTestLab/labs/virtualmachines 資源佈建或佈建 hello Microsoft.Commpute/virtualmachines 資源。 每種方式在不同案例中使用，而且需要不同的權限。

- 使用 Microsoft.DevTestLab/labs/virtualmachines 資源類型 （如在 hello hello 範本中的 「 資源 」 屬性中宣告） 的資源管理員範本，可以佈建個別實驗室 Vm。 每個 VM 然後顯示成 hello DevTest Labs 虛擬機器清單中的單一項目：

   ![Vm 中當做 hello DevTest Labs 虛擬機器清單中的單一項目清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   這種類型的資源管理員範本，可以透過 hello Azure PowerShell 命令，佈建**新增 AzureRmResourceGroupDeployment**或透過 hello Azure CLI 命令**az 群組部署建立**. 它需要系統管理員權限，所以與 DevTest 實驗室使用者角色指派的使用者無法執行 hello 部署。 

- 使用 Microsoft.Compute/virtualmachines 資源類型的資源管理員範本可以做為單一環境 hello DevTest Labs 虛擬機器清單中，佈建多個 Vm:

   ![Vm 中當做 hello DevTest Labs 虛擬機器清單中的單一項目清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   可以同時管理相同的環境的 hello 和共用中的 Vm hello 相同生命週期。 DevTest 實驗室使用者角色指派的使用者可以建立環境，只要 hello 系統管理員設定 hello 實驗室，這樣一來，使用這些範本。

這篇文章的 hello 其餘部分將討論使用 Mirosoft.DevTestLab/labs/virtualmachines 的資源管理員範本。 會使用這些實驗室系統管理員 」 tooautomate 實驗室建立 VM (例如，claimable Vm) 或標準映像層代 （例如，原廠映像）。

[最佳作法來建立 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多的指導方針及建議 toohelp 建立可靠且容易 toouse 的 Azure Resource Manager 範本。

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>檢視及儲存虛擬機器的 Resource Manager 範本
1. 請依照下列步驟 hello[的實驗室中建立您的第一個 VM](devtest-lab-create-first-vm.md) toobegin 建立虛擬機器。
1. 輸入您的虛擬機器的所需的 hello 資訊並加入您想要用於此 VM 的任何成品。
1. 在 hello hello 設定 設定 視窗底部，選擇 **檢視 ARM 範本**。

   ![檢視 ARM 範本按鈕](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. 複製並儲存 hello 資源管理員範本 toouse 稍後 toocreate 另一個虛擬機器。

   ![資源管理員範本 toosave 供日後使用](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

儲存 hello Resource Manager 範本之後，您必須先更新 hello 範本 hello 參數 區段，才能使用它。 您可以建立自訂剛才 hello 參數，外部 hello 實際 Resource Manager 範本 parameter.json。 

![使用 JSON 檔案自訂參數](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>部署資源管理員範本 toocreate VM
您已儲存的資源管理員範本，並自訂您的需求之後，您可以使用它建立 tooautomate VM。 [部署資源與資源管理員範本和 Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)描述如何使用資源管理員範本 toodeploy toouse Azure PowerShell 資源 tooAzure。 [部署資源，資源管理員範本與 Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)描述如何使用資源管理員範本 toodeploy toouse Azure CLI 資源 tooAzure。

> [!NOTE]
> 只有具備實驗室擁有者權限的使用者才可以使用 Azure PowerShell 從 Resource Manager 範本建立 VM。 如果您想要使用資源管理員範本建立 tooautomate VM，您只需要使用者權限，您可以使用 hello [ **az 實驗室 vm 建立**hello CLI 命令](https://docs.microsoft.com/cli/azure/lab/vm#create)。

### <a name="next-steps"></a>後續步驟
* 了解如何太[建立多部 VM 環境使用資源管理員範本](devtest-lab-create-environment-from-arm.md)。
* 瀏覽的 DevTest Labs 自動化更多的快速入門資源管理員範本，從 hello[公用的 DevTest Labs GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)。
