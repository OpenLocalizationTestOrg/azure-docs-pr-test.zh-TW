---
title: "使用 Azure 堆疊中的 Visual Studio aaaDeploy 範本 |Microsoft 文件"
description: "深入了解如何使用 Azure 堆疊中的 Visual Studio toodeploy 範本。"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a>使用 Visual Studio 部署 Azure Stack 中的範本

使用 Visual Studio toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。

1. [安裝並連接](azure-stack-install-visual-studio.md)tooAzure Visual Studio 中的堆疊。
2. 開啟 Visual Studio。
3. 按一下**檔案**，按一下 **新增**，並在 hello**新專案**對話方塊中，按一下**Azure 資源群組**。
4. 輸入**名稱**hello 新專案，然後再按一下**確定**。
5. 在 hello**選取 Azure 範本**對話方塊中，變更 hello*顯示從這個位置的範本*下拉式太**Azure 堆疊快速入門**
6. 按一下 [101-建立-儲存體-帳戶]，然後再按一下 [確定]。  
7. 在新的專案中，您可以看到一份可用的 hello 範本展開 hello**範本**節點 hello**方案總管 中**窗格。
8. 在 hello**方案總管 中**窗格，以滑鼠右鍵按一下 hello 您的專案名稱，按一下 **部署**，然後按一下**新部署**。
9. 在 hello**部署 tooResource 群組**對話方塊中的，在 hello**訂用帳戶**下拉式清單中，選取您的 Microsoft Azure 堆疊訂用帳戶。
10. 在 hello**資源群組**清單中，選擇現有的資源群組或另外新建一個。
11. 在 hello**資源群組位置**清單中，選擇的位置，然後按一下**部署**。
12. 在 hello**編輯參數**對話方塊方塊中，輸入 hello 參數 （這會因範本） 的值，然後按一下**儲存**。

## <a name="next-steps"></a>後續步驟
[部署範本以 hello 命令列](azure-stack-deploy-template-command-line.md)

[開發適用於 Azure Stack 的範本](azure-stack-develop-templates.md)

