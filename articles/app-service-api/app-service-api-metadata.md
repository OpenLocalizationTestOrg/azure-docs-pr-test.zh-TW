---
title: "aaaApp Service API 應用程式中繼資料 API 探索和程式碼產生 |Microsoft 文件"
description: "了解如何在 Azure App Service API 應用程式使用 Swagger 中繼資料 toofacilitate API 探索和程式碼產生。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料
App Service API Apps 內建支援 [Swagger 2.0](http://swagger.io/) API 中繼資料。 您不需要 toouse Swagger，但如果您使用它，您可以利用 API 應用程式功能，讓探索和耗用更容易。   

## <a name="swagger-endpoint"></a>Swagger 端點
您可以指定應用程式開發介面應用程式中的 hello API 應用程式的屬性會提供 Swagger 2.0 JSON 中繼資料端點。 hello 端點可以是相對 toohello hello API 應用程式基底 URL 或絕對 URL。 絕對 Url 可以指向外部 hello API 應用程式。 

許多下游的用戶端 （例如 Visual Studio 程式碼產生和 PowerApps 「 新增應用程式開發介面 」 流程），hello URL 必須可公開存取 （不是由使用者或服務驗證保護）。 這表示如果您使用的應用程式服務驗證，並想從 tooexpose hello API 定義本身的應用程式中，您需要您的 API 可讓匿名流量 tooreach toouse 驗證選項。 如需詳細資訊，請參閱 [App Service API Apps 的驗證和授權](app-service-api-authentication.md)。

### <a name="portal-blade"></a>入口網站刀鋒視窗
在 hello [Azure 入口網站](https://portal.azure.com/)hello 的端點 URL 可以看到和 hello 上變更**API 定義**刀鋒視窗。

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Azure Resource Manager 屬性
您也可以藉由設定 API 應用程式的 hello API 定義 URL[資源總管](https://resources.azure.com/)或[Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)在命令列工具，像是[Azure PowerShell](/powershell/azureps-cmdlets-docs)和 hello [Azure CLI](../cli-install-nodejs.md)。 

在**資源總管**，跳過**訂用帳戶 > {訂用帳戶} > resourceGroups > {您的資源群組} > 提供者 > Microsoft.Web > 網站 > {您的站台} > 組態 > web**，您會看見 hello`apiDefinition`屬性：

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

如需設定 hello Azure Resource Manager 範本的範例`apiDefinition`屬性，此時會開啟 hello [hello 待辦事項清單範例應用程式中的 azuredeploy.json 檔案](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)。 尋找看起來像 hello JSON 範例如上所示的 hello 範本的 hello > 一節。

### <a name="default-value"></a>預設值
當您使用 Visual Studio toocreate API 應用程式時，hello API 定義的端點會自動設定 toohello 加號 hello API 應用程式基底 URL `/swagger/docs/v1`。 這是 hello 預設 URL 的 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 套件的 ASP.NET Web API 專案使用 tooserve 動態產生的 Swagger 中繼資料。 

## <a name="code-generation"></a>產生程式碼
Azure API 應用程式中整合 Swagger hello 優點的其中一個是自動產生程式碼。 產生的用戶端類別會讓它更容易 toowrite 程式碼呼叫 API 應用程式。

您可以使用 Visual Studio，或從 hello 命令列，產生 API 應用程式的用戶端程式碼。 如需 Visual Studio 中 toogenerate 用戶端類別的 ASP.NET Web API 專案的如何資訊，請參閱[開始使用應用程式開發介面應用程式和 ASP.NET](app-service-api-dotnet-get-started.md#codegen)。 如需如何 toodo 從 hello 命令列的所有支援的語言資訊，請參閱 hello 讀我檔案的 hello [Azure/autorest](https://github.com/azure/autorest) GitHub.com 上的儲存機制。

## <a name="next-steps"></a>後續步驟
如需逐步解說的教學課程來引導您建立、部署及使用 API 應用程式，請參閱 [開始使用 Azure App Service 中的 API Apps](app-service-api-dotnet-get-started.md)。

如果您使用 Azure API 管理 API 應用程式時，您可以使用 Swagger 中繼資料 tooimport 您的 API 到 API 管理。 如需詳細資訊，請參閱[tooimport hello 的 Azure API 管理中的作業 API 定義的方式](../api-management/api-management-howto-import-api.md)。 

