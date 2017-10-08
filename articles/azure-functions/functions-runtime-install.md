---
title: "aaaAzure 函式執行階段安裝 |Microsoft 文件"
description: "如何 tooInstall hello Azure 函式執行階段"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>安裝 hello Azure 函式執行階段預覽

如果您想要 tooinstall hello Azure 函式執行階段預覽，您必須遵循下列步驟：

1. 請確定您的電腦傳送 hello 最低需求
1. 下載 hello [Azure 函式執行階段 Preview 安裝程式](https://aka.ms/azafr)。 
1. 安裝 hello Azure 函式執行階段 preview
1. Hello Azure 函式執行階段預覽的完整 hello 組態

## <a name="prerequisites"></a>必要條件

安裝 hello Azure 函式執行階段預覽之前，您必須擁有 hello 下列：

1. 執行 Microsoft Windows Server 2016 或 Microsoft Windows 10 Creators Update (Professional 或 Enterprise Edition) 的電腦。
1. 在您的網路內執行的 SQL Server 執行個體。  最小版本需求是 SQL Server Express。

## <a name="install-hello-azure-functions-runtime-preview"></a>安裝 hello Azure 函式執行階段預覽

hello Azure 函式執行階段 preview 安裝程式會引導您完成 hello hello Azure 函式執行階段預覽管理和背景工作角色的安裝。  它是可能 tooinstall hello 管理和背景工作角色上 hello 同一部電腦。  不過，當您加入多個函式，您必須部署多個背景工作角色上的其他電腦 toobe 無法 tooscale 到多個背景工作函式。

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Hello 上安裝 hello 管理和背景工作角色相同的電腦

1. 執行 hello Azure 函式執行階段 Preview 安裝程式。

    ![Azure Functions 執行階段預覽安裝程式][1]

1. **按一下 下一步**前進過去 hello 第一個階段中的 hello 安裝程式
1. 一旦您已經讀取的 hello hello 條款**EULA**，**核取方塊 hello** tooaccept hello 條款和**按下一步**tooadvance。
1. 現在選取 hello 角色您想在這部電腦上的 tooinstall**函式管理角色**及/或**函式背景工作角色**和**按一下 [下一步]**

    ![Azure Functions 執行階段預覽安裝程式 - 選取角色][3]

    > [!NOTE]
    > 您可以安裝 hello**函式背景工作角色**在許多其他機器 toodo 因此，請遵循這些指示，然後只選取**函式背景工作角色**hello 安裝程式中。

1. **按一下 下一步**toohave hello **Azure 函式執行階段安裝程式**在電腦上安裝。
1. 一旦完成 hello 安裝程式將會啟動 hello **Azure 函式執行階段組態工具**。

    ![Azure Functions 執行階段預覽安裝程式完成][5]

    > [!NOTE]
    > 如果您要安裝在**Windows 10**和 hello**容器**功能有先前未啟用，hello **Azure 函式執行階段**安裝程式會提示您 tooreboot您的機器 toocomplete hello 安裝。

## <a name="configure-hello-azure-functions-runtime"></a>設定 hello Azure 函式執行階段

toocomplete hello Azure 函式執行階段安裝，您必須先完成 hello 組態。

1. hello **Azure 函式執行階段組態工具**顯示您的電腦上安裝哪些角色。

    ![Azure Functions 執行階段預覽設定工具][6]

1. 按一下 hello**資料庫**索引標籤上，輸入 hello**連接詳細資料，您的 SQL Server 執行個體**和**按一下 套用**。  這被必要的順序 toohello Azure 函式執行階段 toocreate 資料庫 toosupport hello 執行階段中。
    
    ![Azure Functions 執行階段預覽資料庫設定][7]

1. 按一下 hello**認證** 索引標籤。在此畫面上，您必須建立兩個新的認證，以使用 FileShare 來裝載您的所有 Azure Functions。  **指定使用者名稱和密碼**hello 組合**檔案共用擁有者**和 hello**檔案共用使用者**按一下**套用**。

    ![Azure Functions 執行階段預覽認證][8]

1. 按一下 hello**檔案共用** 索引標籤。在此畫面中，您必須指定 hello 詳細資料的 hello**檔案共用位置**。  您可以建立此項目，也可以使用現有的檔案共用，然後按一下 [套用]。  如果您選取新的檔案共用位置，您必須指定 hello Azure 函式執行階段使用的目錄。
    
    ![Azure Functions 執行階段預覽檔案共用][9]

1. 按一下 hello **IIS**  索引標籤。此索引標籤會顯示在 IIS Azure 函式執行階段安裝將會建立該 hello hello 網站 hello 詳細資料。  **按一下 套用**toocomplete。

    ![Azure Functions 執行階段預覽 IIS][10]

1. 按一下 hello**服務** 索引標籤。此索引標籤會顯示 hello hello 服務狀態，在 Azure 函式執行階段安裝。  如果在初始設定 hello **Azure 函式主機啟用服務**正在按一下**啟動服務**

    ![Azure Functions 執行階段預覽設定完成][11]

1. 最後瀏覽 toohello **Azure 函式執行階段網站**為`https://<machinename>/`

    ![Azure Functions 執行階段預覽入口網站][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png