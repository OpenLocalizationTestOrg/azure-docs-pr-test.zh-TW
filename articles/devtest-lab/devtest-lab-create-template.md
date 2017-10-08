---
title: "aaaCreate Azure DevTest Labs 自訂映像的 VHD 檔案從 |Microsoft 文件"
description: "了解如何在 Azure DevTest Labs 從 VHD 檔案使用的自訂映像 toocreate hello Azure 入口網站"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a>從 VHD 檔案建立自訂映像

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>逐步指示

hello 下列步驟引導您完成建立自訂映像從 VHD 檔案使用 hello Azure 入口網站：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. 選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。

1. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  

1. 在 hello 實驗室刀鋒視窗中，選取 **組態**。 

1. 在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。

1. 在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。

    ![加入自訂映像](./media/devtest-lab-create-template/add-custom-image.png)

1. 輸入 hello hello 自訂映像名稱。 建立 VM 時，此名稱會顯示 hello 的基底映像的清單中。

1. 輸入 hello hello 自訂映像的描述。 建立 VM 時，此描述會顯示 hello 的基底映像的清單中。

1. 選取 [VHD]。

1. 從 hello **VHD**刀鋒視窗中，選取所需的 hello VHD 檔案。

1. 選取**確定**tooclose hello **VHD**刀鋒視窗。

1. 選取 [作業系統組態]。

1. 在 hello**作業系統組態**索引標籤上，選取  **Windows**或**Linux**。

1. 如果**Windows**是透過 hello 核取方塊選取，指定是否*Sysprep*已經 hello 機器上執行。 

1. 選取**確定**tooclose hello**作業系統組態**刀鋒視窗。

1. 選取**確定**toocreate hello 自訂映像。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章

- [自訂映像或公式？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [在 Azure DevTest Labs 之間複製自訂映像](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>後續步驟

- [新增 VM tooyour 實驗室](./devtest-lab-add-vm-with-artifacts.md)
