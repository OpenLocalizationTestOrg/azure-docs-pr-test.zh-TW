---
title: "Azure 雲端服務專案與 Visual Studio aaaConfigure |Microsoft 文件"
description: "了解如何 tooconfigure Azure 雲端服務 Visual Studio 專案中，根據您針對該專案的需求。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>使用 Visual Studio 來設定 Azure 雲端服務專案
您可以根據 Azure 雲端服務專案的需求來設定專案。 您可以設定下列類別目錄的 hello 的 hello 專案的屬性：

- **發行雲端服務 tooAzure** -您可以設定屬性 toomake 確定現有的雲端服務部署 tooAzure 不意外刪除。
- **執行或偵錯 hello 本機電腦上的雲端服務**-您可以選取 服務組態 toouse 並指出您是否想 toostart hello Azure 儲存體模擬器。
- **雲端服務封裝時就會建立驗證**-您可以決定的 tootreat 任何警告視為錯誤，讓您可以確保該 hello 雲端服務套件部署沒有任何問題。 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>步驟 tooconfigure Azure 雲端服務專案
1. 在 Visual Studio 中開啟或建立雲端服務專案

1. 在**方案總管 中**、 hello 專案上按一下滑鼠右鍵，然後從 hello 內容功能表中，選取**屬性**。
   
1. 在 hello 專案屬性頁面上，選取 hello**開發** 索引標籤。

    ![專案屬性功能表](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. 設定**刪除現有部署之前提示**太**True**。 此設定可協助您不小心不要刪除 Azure 中的現有部署 tooensure

1. 選取所需的 hello**服務組態**tooindicate 哪些服務您想要設定 toouse 當您執行或偵錯您的雲端服務在本機。 如需有關如何 toomodify 服務組態的角色，請參閱[如何 tooconfigure hello 角色的 Azure 雲端服務與 Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md)。

1. 設定**啟動 Azure 儲存體模擬器**太**True** toostart hello Azure 儲存體模擬器執行或偵錯雲端服務在本機上時。

1. 設定**將警告視為錯誤**太**True** toomake 確定您無法發佈套件驗證錯誤時。

1. 設定**使用 web 專案連接埠**太**True** toomake 確定您的 web 角色會使用相同的每個連接埠的 hello 次在 IIS Express 本機啟動。

1. 從 hello Visual Studio 工具列上，選取**儲存**。

## <a name="next-steps"></a>後續步驟
- [使用多個服務組態設定 Azure 專案](vs-azure-tools-multiple-services-project-configurations.md)

