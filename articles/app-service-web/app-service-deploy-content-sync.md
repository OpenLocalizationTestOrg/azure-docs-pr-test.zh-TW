---
title: "從雲端資料夾 tooAzure App Service aaaSync 內容"
description: "了解如何 toodeploy 內容透過您的應用程式 tooAzure 應用程式服務從同步處理雲端資料夾。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>從雲端資料夾 tooAzure 應用程式服務的同步處理內容
本教學課程示範如何 toodeploy 太[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)所同步處理您的內容從 Dropbox 和 OneDrive 等熱門的雲端儲存體服務。 

## <a name="overview"></a>內容同步處理部署概觀
hello 視內容的同步處理部署由 hello [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)整合與應用程式服務。 在 hello [Azure 入口網站](https://portal.azure.com)，您可以指定您的雲端儲存體中的資料夾，使用您的應用程式程式碼和內容，在該資料夾中，然後以 hello 同步 tooApp 服務按一下按鈕。 內容的同步處理會使用組建和部署的 hello Kudu 程序。 

## <a name="contentsync"></a>Tooenable 內容同步處理的部署方式
從 hello tooenable 內容同步[Azure 入口網站](https://portal.azure.com)，請遵循下列步驟：

1. 在您的應用程式] 刀鋒視窗 hello Azure 入口網站中，按一下 [**設定** > **部署來源**。 按一下**選擇來源**，然後選取**OneDrive**或**Dropbox**做為部署的 hello 來源。 
   
    ![內容同步處理](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Hello 應用程式開發介面，因此基礎**商務用 OneDrive**不支援這一次。 
   > 
   > 
2. 完成 hello 授權工作流程 tooenable App Service tooaccess 特定預先定義的指定之的路徑的 OneDrive 或 Dropbox 會儲存所有您應用程式服務的內容。  
    應用程式服務平台可讓您的授權 hello 之後 hello 選項 toocreate 內容 資料夾之下的 hello 會指定內容的路徑或 toochoose 這個指定之內容的路徑下的現有內容資料夾。 在您用於應用程式服務同步處理的雲端儲存體帳戶下的 hello 指定內容路徑是 hello 下列：  
   
   * **OneDrive**：`Apps\Azure Web Apps` 
   * **Dropbox**：`Dropbox\Apps\Azure`
3. Hello 之後，您可以視需要從 hello Azure 入口網站啟動初始內容的同步處理 hello 內容同步處理。 部署歷程記錄是可用以 hello**部署**刀鋒視窗。
   
    ![部署歷程記錄](./media/app-service-deploy-content-sync/onedrive_sync.png)

[從 Dropbox 部署](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx)下有 Dropbox 部署的詳細資訊。 

