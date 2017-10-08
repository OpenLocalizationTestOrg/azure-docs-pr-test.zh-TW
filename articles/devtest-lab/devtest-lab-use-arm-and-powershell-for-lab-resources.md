---
title: "aaaCreate 或修改實驗室自動使用 PowerShell 建立 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何使用 PowerShell toocreate toouse Azure Resource Manager 範本或修改自動 DevTest 實驗室的實驗室"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>使用 PowerShell 及 Azure Resource Manager 範本自動建立或修改實驗室

DevTest 實驗室提供許多 Azure Resource Manager 範本和 PowerShell 指令碼，可以協助您快速及自動建立新的實驗室，或修改現有的實驗室，並進行資源部署。

這篇文章可協助引導您完成使用這些範本與指令碼 tooautomate hello 建立、 修改和部署您的實驗室 hello 程序。 本文也會顯示您可以在其中找到影響 toouse PowerShell tooperform 一些常見工作的 DevTest Labs 的詳細資訊。

## <a name="step-1-gather-your-templates-and-scripts"></a>步驟 1︰收集您的範本和指令碼
您可以在我們公用的 [Github 存放庫](https://github.com/Azure/azure-devtestlab)中找到預先製作的 [Azure Resource Manager 範本](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)和 [PowerShell 指令碼](https://github.com/Azure/azure-devtestlab/tree/master/Scripts)。 直接使用，或針對您的需求進行自訂，並儲存在您自己的[私人 Git 存放庫](devtest-lab-add-artifact-repo.md)。 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>步驟 2：修改您的 Azure Resource Manager 範本
您可以依照 hello 步驟[建立第一個 Azure Resource Manager 範本](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)如果永遠不會建立範本之前。

此外，[最佳作法來建立 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多的指導方針及建議 toohelp 建立可靠且容易 toouse 的 Azure Resource Manager 範本。 通常，您將使用的其中一種 hello 方法變化或範例，修改您的範本，針對您的需求。

## <a name="step-3-deploy-resources-with-powershell"></a>步驟 3︰ 使用 PowerShell 部署資源
您已自訂您的範本和指令碼之後，請依照所需的 hello 步驟太[部署資源與資源管理員範本和 Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。 hello 文章提供資源 tooAzure 的 Azure Resource Manager 範本 toodeploy 搭配使用 Azure PowerShell 的一般資訊。


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>您可以使用 PowerShell 在 DevTest 實驗室中執行的一般工作
有許多其他一般工作，您可以使用 PowerShell 來自動執行。 hello hello 文件的下列各節簡述 hello 步驟需要的 tooperform 這些工作。

* [使用 PowerShell 從 VHD 檔案建立自訂映像](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [上傳 VHD 檔案 toolab 的儲存體帳戶使用 PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [新增外部使用者 tooa 實驗室使用 PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [使用 PowerShell 建立實驗室自訂角色](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>後續步驟
* 深入了解如何 toocreate[私人 Git 儲存機制](devtest-lab-add-artifact-repo.md)您將在其中儲存您的自訂的範本或指令碼。
* 瀏覽 hello [Azure 資源管理員範本，從 Azure 快速入門範本庫](https://github.com/Azure/azure-quickstart-templates)。
