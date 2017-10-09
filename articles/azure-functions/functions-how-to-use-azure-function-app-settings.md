---
title: "aaaConfigure Azure 函式應用程式設定 |Microsoft 文件"
description: "了解 tooconfigure Azure 應用程式設定的運作方式。"
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>如何 toomanage 函式中的應用程式 hello Azure 入口網站 

Azure 功能中的函式應用程式會提供個別函式 hello 執行內容。 函式應用程式行為套用 tooall 函式所指定的函式應用程式裝載。 本主題描述如何 tooconfigure 及管理在 hello Azure 入口網站應用程式函式。

toobegin，移 toohello [Azure 入口網站](http://portal.azure.com)並登入 tooyour Azure 帳戶。 在 hello 在 hello hello 入口網站頂端搜尋列中輸入 hello 函式應用程式名稱，並從 hello 清單中選取。 選取函式應用程式之後, 您會看到下列頁面的 hello:

![在 hello Azure 入口網站中的函式應用程式概觀](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>函數應用程式設定索引標籤

![函式在 hello Azure 入口網站應用程式概觀。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

hello**設定** 索引標籤是您可以在其中更新函式應用程式所使用的 hello 函式執行階段版本。 它也是您用來管理 hello 主機使用的索引鍵 toorestrict HTTP 存取 tooall 函式 hello 函式應用程式所裝載。

Functions 支援「取用」主控方案和 App Service 主控方案。 如需詳細資訊，請參閱[Azure 函式選擇 hello 正確的服務方案](functions-scale.md)。 可預測性更好 hello 耗用量計劃中，函式可讓您藉由設定以 gb 為單位秒為單位的每日使用量配額，限制平台使用。 一旦達到 hello 每日使用量配額，就會停止 hello 函式應用程式。 已停止，因為達到消費配額的 hello 函式應用程式可以從 hello 重新啟用相同的內容，做為建立每日花配額 hello。 請參閱 hello [Azure 函式定價頁面](http://azure.microsoft.com/pricing/details/functions/)如需計費的詳細資訊。   

## <a name="platform-features-tab"></a>平台功能索引標籤

![函數應用程式平台功能索引標籤。](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

函式應用程式中，執行，並且會維護，hello Azure 應用程式服務平台。 因此，您的函式應用程式可以存取 toomost hello Azure 的核心 web 裝載平台的功能。 hello**平台功能** 索引標籤是您存取其中 hello hello 應用程式服務的平台，您可以使用函式應用程式中的許多功能。 

> [!NOTE]
> Hello 耗用量主控方案執行的函式應用程式時，並非所有應用程式服務功能所提供。

本主題的 hello 其餘著重於 hello 遵循 hello 中的應用程式服務功能可用於函式的 Azure 入口網站：

+ [App Service 編輯器](#editor)
+ [應用程式設定](#settings) 
+ [Console](#console)
+ [進階工具 (Kudu)](#kudu)
+ [部署選項](#deployment)
+ [CORS](#cors)
+ [驗證](#auth)
+ [API 定義](#swagger)

如需有關如何 toowork 應用程式服務設定，請參閱[設定 Azure 應用程式服務設定](../app-service-web/web-sites-configure.md)。

### <a name="editor"></a>App Service 編輯器

| | |
|-|-|
| ![函數應用程式 App Service 編輯器。](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | hello 應用程式服務編輯器是進階的入口網站中編輯器，您可以使用 toomodify JSON 組態檔和類似的程式碼檔案。 選擇此選項會啟動一個含有基本編輯器的個別瀏覽器索引標籤。 這可讓您與 hello Git 儲存機制、 執行和偵錯程式碼，toointegrate，並修改函式應用程式設定。 此編輯器提供增強的部署環境函式相較於 hello 預設函式應用程式 刀鋒視窗。    |

![hello 應用程式服務編輯器](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>應用程式設定

| | |
|-|-|
| ![函數應用程式的應用程式設定。](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | 應用程式服務的 hello**應用程式設定**刀鋒視窗是您設定及管理 framework 版本中，遠端偵錯、 應用程式設定和連接字串。 當您將函數應用程式與其他 Azure 和協力廠商服務整合時，可以在這裡修改那些設定值。 |

![設定應用程式設定](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>主控台

| | |
|-|-|
| ![在 hello Azure 入口網站中的函式應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | hello 入口網站中主控台時，理想的開發人員工具與函式應用程式偏好 toointeract 從 hello 命令列。 常用命令包含目錄和檔案建立與瀏覽，以及執行批次檔和指令碼。 |

![函數應用程式主控台](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>進階工具 (Kudu)

| | |
|-|-|
| ![Hello Azure 入口網站中的應用程式 Kudu 函式](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | hello 應用程式服務 (也稱為 Kudu) 的進階的工具提供存取 tooadvanced 函式應用程式的系統管理功能。 從 Kudu，您可以管理系統資訊、應用程式設定、環境變數、網站擴充功能、HTTP 標頭，以及伺服器變數。 您也可以啟動**Kudu** like 瀏覽應用程式的函式，toohello SCM 端點`https://<myfunctionapp>.scm.azurewebsites.net/` |

![設定 Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">部署選項

| | |
|-|-|
| ![Hello Azure 入口網站中的函式應用程式部署選項](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Functions 可讓您在本機電腦上開發函數程式碼。 然後，您可以上傳您的區域函式應用程式專案 tooAzure。 此外 tootraditional FTP 上傳，函式可讓您部署使用常用的連續整合解決方案，如 GitHub、 VSTS、 Dropbox、 Bitbucket 和其他應用程式函式。 如需詳細資訊，請參閱 [Azure Functions 的持續部署](functions-continuous-deployment.md)。 tooupload 手動使用 FTP 或本機 Git，您也必須[設定您的部署認證](functions-continuous-deployment.md#credentials)。 |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![函式中應用程式，CORS hello Azure 入口網站](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | tooprevent 執行您的服務中的惡意程式碼，應用程式服務區塊呼叫 tooyour 函式應用程式從外部來源。 函式支援跨原始資源共用 (CORS) toolet 定義 」 的允許清單 」 允許您的函式將從該處接受遠端要求的來源。  |

![設定函數應用程式的 CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>驗證

| | |
|-|-|
| ![在 hello Azure 入口網站中的函式應用程式驗證](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | 當函式使用的 HTTP 觸發程序時，您可以要求呼叫 toofirst 進行驗證。 App Service 支援 Azure Active Directory 驗證，以及使用社交提供者 (例如 Facebook、Microsoft 及 Twitter) 來登入。 如需設定特定驗證提供者的詳細資訊，請參閱 [Azure App Service 驗證概觀](../app-service/app-service-authentication-overview.md)。 |

![設定函數應用程式的驗證](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>API 定義

| | |
|-|-|
| ![函式應用程式 API swagger 定義中 hello Azure 入口網站](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | 函式支援 Swagger tooallow 用戶端 toomore 輕鬆使用 HTTP 觸發函式。 如需有關如何使用 Swagger 建立 API 定義的詳細資訊，請瀏覽[在 Azure 中開始使用 API Apps、ASP.NET 和 Swagger](../app-service-api/app-service-api-dotnet-get-started.md)。 您也可以使用多個函式的函式 Proxy toodefine 單一的 API 介面。 如需詳細資訊，請參閱[使用 Azure Functions Proxy](functions-proxies.md)。 |

![設定函數應用程式的 API](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>後續步驟

+ [設定 Azure App Service 設定](../app-service-web/web-sites-configure.md)
+ [Azure Functions 的持續部署](functions-continuous-deployment.md)



