---
title: "Azure 雲端服務專案與 Visual Studio aaaCreating |Microsoft 文件"
description: "了解現在 toocreate Visual Studio 中的 Azure 雲端服務專案"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>使用 Visual Studio 建立 Azure 雲端服務專案
hello Azure Tools for Visual Studio 提供可讓您建立 Azure 雲端服務專案範本。 一旦建立 hello 專案之後，Visual Studio 可讓您 tooconfigure、 偵錯和部署 hello 雲端服務 tooAzure。

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>步驟 toocreate Visual Studio 中的 Azure 雲端服務專案
本節將逐步引導您在 Visual Studio 中使用一或多個 Web 角色來建立 Azure 雲端服務專案。  

1. 以系統管理員身分啟動 Visual Studio。

1. Hello 主功能表上，選取**檔案** > **新增** > **專案**。

1. 選取**雲端**從 hello Visual C# 或 Visual Basic 專案範本節點，然後選取**Azure 雲端服務**從 hello 範本清單。

    ![新增 Azure 雲端服務](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. 指定 hello 您希望 toouse toodevelop 專案的.NET Framework 的版本。

1. 輸入名稱和您的專案位置和 hello 方案的名稱。 

1. 選取 [確定] 。

1. 在 hello**新 Microsoft Azure 雲端服務**對話方塊中，選取 hello 角色 tooadd，並選擇 hello 向右箭號按鈕 tooadd 它們 tooyour 方案。

    ![選取新的 Azure 雲端服務角色](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename 角色已新增在 hello hello 角色上的動態顯示**新 Microsoft Azure 雲端服務** 對話方塊中，並從 hello 內容功能表中，選取**重新命名**。 您可以在您的方案也重新命名角色 (在 hello**方案總管 中**) 已加入之後。

    ![將 Azure 雲端服務角色重新命名](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

hello Visual Studio Azure 專案中 hello 方案有關聯 toohello 角色專案。 hello 專案還包括 hello*服務定義檔*和*服務組態檔*:

- **服務定義檔**-定義您的應用程式，包括所需的角色、 端點和虛擬機器大小的 hello 執行階段設定。 
- **服務組態檔**-設定多少個角色執行個體執行，hello hello 設定為角色定義的值。 

如需有關這些檔案的詳細資訊，請參閱[使用 Visual Studio 設定 Azure 雲端服務的 hello 角色](vs-azure-tools-configure-roles-for-cloud-service.md)。

## <a name="next-steps"></a>後續步驟
- [使用 Visual Studio 在 Azure 雲端服務專案中管理角色](./vs-azure-tools-cloud-service-project-managing-roles.md)
