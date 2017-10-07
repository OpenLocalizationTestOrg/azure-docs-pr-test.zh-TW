---
title: "aaaCreate Azure 堆疊中的計劃 |Microsoft 文件"
description: "身為雲端系統管理員，您可以建立可供訂閱者佈建虛擬機器的方案。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a>在 Azure Stack 中建立方案
[方案](azure-stack-key-features.md)結合一或多項服務。 做為提供者，您可以建立計劃 toooffer tooyour 租用戶。 接著，您的租用戶訂閱 tooyour 優惠 toouse hello 計劃和它們所包含的服務。 此範例將示範如何 toocreate 包含計劃 hello 運算、 網路和儲存體資源提供者。 這個計劃可讓訂閱者 hello 能力 tooprovision 虛擬機器。

1. 登入 toohello 堆疊 Azure 管理員入口網站 (https://adminportal.local.azurestack.external)。 輸入您在步驟 5 的 hello 期間建立的 hello 帳戶 hello 認證[執行 hello PowerShell 指令碼](azure-stack-run-powershell-script.md)> 一節。

2. toocreate 計劃和提供租用戶可以訂閱，按一下**新增** > **租用戶提供 + 計劃** > **計劃**。

   ![](media/azure-stack-create-plan/image01.png)
3. 在 hello**新增計劃**刀鋒視窗中，填滿**顯示名稱**和**資源名稱**。 hello 顯示名稱是租用戶中看到的 hello 計劃的易記名稱。 只有 hello 管理員可以看到 hello 資源名稱。 它的 hello 名稱，系統管理員 」 搭配 toowork hello 計劃做為 Azure 資源管理員資源。

   ![](media/azure-stack-create-plan/image02.png)
4. 建立新**資源群組**，或選取現有的我的最愛，做為 hello 計劃的容器。

   ![](media/azure-stack-create-plan/image02a.png)
5. 按一下 服務，選取 Microsoft.Compute、Microsoft.Network 及 Microsoft.Storage，然後按一下選取。

   ![](media/azure-stack-create-plan/image03.png)
6. 按一下**配額**，按一下  **Microsoft.Storage （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。

   ![](media/azure-stack-create-plan/image04.png)
7. 如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。

   ![](media/azure-stack-create-plan/image06.png)
8. 按一下**Microsoft.Network （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。

    ![](media/azure-stack-create-plan/image07.png)
9. 如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。

    ![](media/azure-stack-create-plan/image08.png)
10. 按一下**Microsoft.Compute （本機）**，並接著任一選取 hello 預設配額，或按一下**建立新的配額**toocustomize hello 配額。

    ![](media/azure-stack-create-plan/image09.png)
11. 如果您要建立新的配額，請輸入 hello 配額的名稱 > 設定 hello 配額值 > 按**確定**> 按一下 hello hello 新配額名稱。

    ![](media/azure-stack-create-plan/image10.png)
12. 在 hello**配額**刀鋒視窗中，按一下**確定**，然後在 hello**新計劃**刀鋒視窗中，按一下**建立**toocreate hello 計劃。

    ![](media/azure-stack-create-plan/image11.png)
13. toosee 您新的計畫中，按一下 **所有資源**，然後搜尋 hello 計劃，然後按一下其名稱。

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a>後續步驟
[建立優惠](azure-stack-create-offer.md)
