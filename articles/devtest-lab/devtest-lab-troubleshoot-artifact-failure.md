---
title: "在 Azure DevTest Labs VM aaaDiagnose 成品失敗 |Microsoft 文件"
description: "深入了解如何在 DevTest Labs tootroubleshoot 成品失敗"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>診斷在 hello 實驗室成品失敗 
建立成品之後，您可以檢查 toosee，如果它是成功或是失敗。 DevTest 實驗室中的成品記錄檔提供您可以使用 toodiagnose 成品失敗的資訊。 有幾種不同的方式，您可以檢視針對 Windows VM hello 成品記錄資訊。

> [!NOTE]
> tooensure 失敗是正確的識別及說明，請務必適當地結構化該 hello 成品。 如需如何 toocorrectly 建構成品資訊，請參閱[建立自訂的成品](devtest-lab-artifact-author.md)。 和 toosee 的範例，適當地結構化的成品，請參閱這[測試參數型別](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes)成品。

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>針對使用 hello Azure 入口網站成品失敗進行疑難排解
toouse hello Azure 入口網站 toodiagnose 失敗成品在建立期間，請遵循下列步驟：

1. 從 hello 資源清單，選取您的實驗室。

2. 選擇包含您想要 tooinvestigate hello 成品的 Windows VM hello。

3. Hello 下的左窗格中**一般**，選擇**成品**。 該 VM 相關聯的成品的清單隨即出現，表示 hello 名稱 hello 成品和其狀態。

   ![構件 Git 儲存機制範例](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. 選擇顯示 [失敗] 狀態的構件。 hello 成品隨即開啟，並顯示延伸訊息，其中包含有關 hello 成品的 hello 失敗的詳細資料。

   ![構件 Git 儲存機制範例](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>從 hello VM 內的成品錯誤進行疑難排解
tooview hello 成品從記錄檔內 hello 虛擬機器，請遵循下列步驟：

1. 登入 toohello 包含您想要 toodiagnose hello 成品的 VM。

2. 瀏覽的 tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status"1.9 所在 hello CSE 版本號碼。

   ![構件 Git 儲存機制範例](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. 開啟 hello**狀態**檔案 tooview 資訊可協助診斷成品失敗，該 vm。




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章
* [加入 VM tooexisting Azure DevTest 實驗室中使用資源管理員範本的 AD 網域](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>後續步驟
* 了解如何太[加入 Git 儲存機制 tooa 實驗室](devtest-lab-add-artifact-repo.md)。

