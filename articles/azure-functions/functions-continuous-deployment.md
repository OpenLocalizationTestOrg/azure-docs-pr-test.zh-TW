---
title: "Azure 函式的 aaaContinuous 部署 |Microsoft 文件"
description: "使用 Azure App Service toopublish 持續部署功能 Azure 函式。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Azure Functions 的持續部署
Azure 函式可讓您輕鬆 toodeploy 函式應用程式使用應用程式服務的持續整合。 Functions 可與 BitBucket、Dropbox、GitHub 及 Visual Studio Team Services (VSTS) 整合。 這可讓使用這些整合式的服務，觸發程序部署 tooAzure 的其中一個所做的工作流程更新函式程式碼的位置。 如果您是新 tooAzure 函式，以啟動[Azure 函式概觀](functions-overview.md)。

持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。 它也可讓您維護函式程式碼的原始檔控制。 目前支援下列部署來源 hello:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* 外部存放庫 (Git 或 Mercurial)
* [Git 本機存放庫](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

設定部署時，是依每一函數應用程式進行設定。 啟用連續部署之後，存取 toofunction 碼 hello 入口網站中的設定得*唯讀*。

## <a name="continuous-deployment-requirements"></a>持續部署需求

您必須在您設定的部署來源與函式程式碼 hello 部署來源，才能設定連續部署。 在指定的函式應用程式部署中，每個函式位於命名的子目錄，其中 hello 目錄名稱是 hello hello 函式名稱。  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>設定連續部署
使用此程序 tooconfigure 連續部署現有的函式應用程式。 這些步驟會示範與 GitHub 存放庫的整合，但類似的步驟也適用於 Visual Studio Team Services 或其他部署服務。

1. 您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署選項**。 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. 接著在 hello**部署**刀鋒視窗中按一下**安裝**。
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. 在 hello**部署來源**刀鋒視窗中，按一下**選擇來源**，然後填入您所選擇的部署來源 hello 資訊，然後按一下**確定**。
   
    ![選擇部署來源](./media/functions-continuous-deployment/choose-deployment-source.png)

設定連續部署之後，您的部署來源中的所有檔案變更都會複製的 toohello 函式應用程式，而且會觸發完整站台部署。 hello 來源中的檔案更新時，會重新部署 hello 站台。

## <a name="deployment-options"></a>部署選項

hello 以下是一些典型部署案例：

- [建立預備部署](#staging)
- [移動現有的函式 toocontinuous 部署](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>建立預備部署

函式應用程式尚未支援部署位置。 不過，您仍可使用持續整合來管理個別的預備部署和生產部署。

hello tooconfigure 程序，並使用預備環境部署通常看起來像這樣：

1. 建立兩個函式應用程式在您的訂閱 hello 實際執行程式碼，一個供暫存。 

2. 建立部署來源 (如果還未擁有)。 此範例使用 [GitHub]。

3. 您實際執行的函式應用程式中的步驟完成前述的 hello**設定連續部署**組 hello 部署分支 toohello 主要分支您的 GitHub 儲存機制。
   
    ![選擇部署分支](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. 針對 hello 暫存函式應用程式時，重複此步驟，但是選擇暫存分支改為在您的 GitHub 儲存機制中的 hello。 如果部署來源不支援分支功能，請使用不同的資料夾。
    
5. 請更新 tooyour 程式碼中 hello 暫存分支或資料夾，然後確認這些變更會反映在預備環境部署的 hello。

6. 測試之後，合併變更 hello 臨時分支到 hello 主要分支。 此合併觸發程序部署 toohello 生產函式應用程式。 如果您部署的來源不支援分支，檔案覆寫 hello 生產資料夾中的 hello 檔案 hello 從 hello 暫存資料夾。

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>移動現有的函式 toocontinuous 部署
當您有現有的函式，您已建立並維護在 hello 入口網站，您需要 toodownload 現有函式 （如上所述），才能設定連續部署使用 FTP 或 hello 本機 Git 儲存機制的程式碼檔案。 您可以在 hello 應用程式服務設定為函式應用程式。 下載檔案之後，您可以上傳它們 tooyour 選擇連續部署來源。

> [!NOTE]
> 設定持續整合之後，您將不再能夠 tooedit hello 函式的入口網站中的程式來源檔案。

- [作法：設定部署認證](#credentials)
- [作法︰使用 FTP 下載檔案](#downftp)
- [如何： 使用 hello 本機 Git 儲存機制下載檔案](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>作法：設定部署認證
您可以從您使用 FTP 或本機 Git 儲存機制的函式應用程式下載檔案之前，您必須設定認證 tooaccess hello 站台。 認證會在 hello 函式應用程式層級設定。 使用下列步驟 tooset 部署認證 hello Azure 入口網站中的 hello:

1. 您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署認證**。
   
    ![設定本機部署認證](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. 輸入使用者名稱和密碼，然後按一下 [儲存] 。 您現在可以使用這些認證 tooaccess 函式應用程式從 FTP 或 hello 內建的 Git 儲存機制。

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>作法︰使用 FTP 下載檔案

1. 您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下**平台功能**和**屬性**，然後將複製的 hello 值**FTP/部署使用者**， **FTP 主機名稱**，和**FTPS 主機名稱**。  

    **FTP/部署使用者**必須輸入 hello 入口網站，包括 hello 應用程式名稱、 tooprovide hello FTP 伺服器的適當的內容中所示。
   
    ![取得部署資訊](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. 從您的 FTP 用戶端，使用您所蒐集 tooconnect tooyour 應用程式的 hello 連接資訊和下載 hello 函式的來源檔案。

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>操作說明：使用本機 Git 存放庫來下載檔案

1. 您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署選項**。 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. 接著在 hello**部署**刀鋒視窗中按一下**安裝**。
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. 在 hello**部署來源**刀鋒視窗中，按一下**本機 Git 儲存機制**，然後按一下**確定**。

3. 在**平台功能**，按一下 **屬性**並記下 hello Git URL 值。 
   
    ![設定持續部署](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. 使用 Git 感知的命令提示字元或您慣用的 Git 工具在本機電腦上複製 hello 儲存機制。 hello Git clone 命令看起來像這樣：
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. 擷取函式應用程式 toohello 再製的檔案儲存在本機電腦，如 hello 下列範例所示：
   
        git pull origin master
   
    如果系統要求，請提供[已設定的部署認證](#credentials)。  

[GitHub]: https://github.com/
