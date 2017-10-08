---
title: "aaaCreate Azure DevTest Labs 自訂映像從 VM |Microsoft 文件"
description: "了解如何從佈建的 VM 使用 Azure DevTest Labs 中的自訂映像 toocreate hello Azure 入口網站"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a>從 VM 建立自訂映像

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a>逐步指示

您可以從佈建 VM，建立自訂映像，並在之後使用該自訂映像 toocreate 相同的 Vm。 hello 下列步驟說明如何 toocreate 自訂映像從 VM:

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。

1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  

1. 在 hello 實驗室刀鋒視窗中，選取 **我的虛擬機器**。
 
1. 在 hello**我的虛擬機器**刀鋒視窗中，選取 hello VM 要從中 toocreate hello 自訂映像。

1. 在 hello VM 刀鋒視窗中，選取 **建立自訂映像 (VHD)**。

    ![建立自訂映像的功能表項目](./media/devtest-lab-create-template/create-custom-image.png)

1. 在 hello**建立映像**刀鋒視窗中，輸入名稱和自訂映像的描述。 當您建立 VM 時，這項資訊會顯示 hello 從基底清單中。

    ![建立自訂映像刀鋒視窗](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. 選擇是否要在 hello VM 上執行 sysprep。 如果不執行 hello sysprep hello VM 上，指定是否要從這個自訂映像建立 VM 時執行 sysprep。

1. 選取**確定**時完成的 toocreate hello 自訂映像。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章

- [自訂映像或公式？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [在 Azure DevTest Labs 之間複製自訂映像](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>後續步驟

- [新增 VM tooyour 實驗室](./devtest-lab-add-vm-with-artifacts.md)
