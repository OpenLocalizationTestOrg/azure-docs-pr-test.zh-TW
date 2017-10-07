---
title: "aaaDeploy 您應用程式 tooAzure 應用程式服務使用 FTP/S |Microsoft 文件"
description: "深入了解如何 toodeploy 您的應用程式 tooAzure 應用程式服務使用 FTP 或 FTPS。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>部署您的應用程式 tooAzure 使用 FTP/S 的應用程式服務

本文章將示範如何 toouse FTP 或 web 應用程式、 行動裝置應用程式後端或應用程式開發介面應用程式太 FTPS toodeploy[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)。

您的應用程式的 hello FTP/S 端點已在使用中。 不不需要 tooenable FTP/S 部署的任何設定。

> [!IMPORTANT]
> 我們會持續執行步驟 tooimprove Microsoft Azure 平台安全性。 在此持續努力的過程中，我們規劃升級德國中部和德國東北部地區的 Web 應用程式。 在此 Web 應用程式將會停用部署的 hello 使用純文字 FTP 通訊協定。 我們建議 tooour 客戶是 tooswitch tooFTPS 部署。 我們不會在執行此升級的 9/5 計劃的任何中斷 tooyour 服務。 感謝您支援這項工作。

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>步驟 1：設定部署認證

tooaccess hello FTP 伺服器上您的應用程式，您必須先部署認證。 

tooset 或重設您的部署認證，請參閱[Azure 應用程式服務的部署認證](app-service-deployment-credentials.md)。 本教學課程示範 hello 使用使用者層級的認證。

## <a name="step-2-get-ftp-connection-information"></a>步驟 2：取得 FTP 連線資訊

1. 在 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。
2. 選取**概觀**在 hello 左功能表中，然後記下 hello 值**FTP/部署使用者**， **FTP 主機名稱**，和**FTPS 主機名稱**。 

    ![FTP 連線資訊](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > hello **FTP/部署使用者**使用者值顯示 hello hello 應用程式名稱包含在 hello FTP 伺服器的順序 tooprovide 適當內容的 Azure 入口網站。
    > 您可以找到 hello 相同的資訊，當您選取**屬性**hello 左功能表中。 
    >
    > 此外，永遠不會顯示 hello 部署密碼。 如果您忘記您部署的密碼，請回到太[步驟 1](#step1)和重設您部署的密碼。
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>步驟 3： 部署檔案 tooAzure

1. 從您的 FTP 用戶端 ([Visual Studio](https://www.visualstudio.com/vs/community/)， [FileZilla](https://filezilla-project.org/download.php?type=client)等等)，使用您所蒐集 tooconnect tooyour 應用程式的 hello 連接資訊。
3. 複製您的檔案和其各自的目錄結構 toohello [ **/站台/wwwroot**目錄](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)在 Azure 中 (或 hello **/站台/wwwroot/App_Data/工作/**目錄WebJobs)。
4. 瀏覽 tooyour 應用程式的 URL tooverify hello 應用程式正常執行。 

> [!NOTE] 
> 不同於[Git 架構部署](app-service-deploy-local-git.md)，FTP 部署不支援下列部署不僅 hello: 
>
> - 相依性還原 (例如 NuGet、NPM、PIP 和編輯器自動化)
> - .NET 二進位檔的編譯
> - web.config 的產生 (此處是 [Node.js 範例](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> 您必須在您的本機電腦上手動還原、建置及產生這些必要的檔案，並與您的應用程式一起部署它們。
>
>

## <a name="next-steps"></a>後續步驟

如需更多進階部署案例中，請嘗試[部署與 Git tooAzure](app-service-deploy-local-git.md)。 Git 部署 tooAzure 啟用版本控制、 封裝還原，MSBuild，等等。

## <a name="more-resources"></a>其他資源

* [建立 PHP-MySQL Web 應用程式並使用 FTP 部署](web-sites-php-mysql-deploy-use-ftp.md)。
* [Azure App Service 部署認證](app-service-deploy-ftp.md)
