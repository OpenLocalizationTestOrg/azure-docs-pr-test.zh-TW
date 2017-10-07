---
title: "測試 Azure 堆疊中的 VM aaaCreate |Microsoft 文件"
description: "深入了解如何 tooprovision 測試 Azure 雲端操作員的堆疊中的 VM。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/21/2017
ms.author: erikje
ms.openlocfilehash: 9633cc20852e16283ad4522da78971133028efdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-test-virtual-machine-in-azure-stack"></a>在 Azure Stack 中建立測試虛擬機器
雲端操作員，您可以建立測試虛擬機器 toovalidate Azure 堆疊部署。

> [!NOTE]
> 您可以佈建虛擬機器之前，您必須[新增 hello Windows Server 2016 Evaluation 映像 toohello Azure 堆疊 marketplace](azure-stack-add-default-image.md)。
> 
> 

## <a name="create-a-virtual-machine"></a>建立虛擬機器
1. Hello Azure 堆疊開發套件在主機上，[登入](azure-stack-connect-azure-stack.md)toohello 管理員入口網站 (`https://adminportal.local.azurestack.external`)，然後按一下**新增** > **計算** > **評估版的 Windows Server 2016 資料中心** > **建立**。  
2. 在 hello**基本概念**刀鋒視窗中，輸入**名稱**，**使用者名稱**，和**密碼**。 選擇 [訂用帳戶] 。 建立 資源群組，或選取現有的資源群組，然後按一下確定。  
3. 在 hello**大小選擇 「**刀鋒視窗中，按一下**標準 A1**，然後按一下**選取**。  
4. 在 hello**設定**刀鋒視窗中，接受 hello 預設值，並按一下**確定**
5. 在 hello**摘要**刀鋒視窗中，按一下 **確定**toocreate hello 虛擬機器。  
6. toosee 新的虛擬機器，按一下 **所有資源**，然後搜尋 hello 虛擬機器，然後按一下其名稱。
    ![](media/azure-stack-provision-vm/image06.png)


## <a name="next-steps"></a>後續步驟
[使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站](azure-stack-manage-portals.md)
