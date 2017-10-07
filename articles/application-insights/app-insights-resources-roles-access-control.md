---
title: "在 Azure Application Insights aaaResources、 角色和存取控制 |Microsoft 文件"
description: "您的組織詳細資料的擁有者、參與者及讀者。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Application Insights 中的資源、角色及存取控制
您可以控制誰具有讀取和更新存取 Azure 中的 tooyour 資料[Application Insights][start]，使用[Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。

> [!IMPORTANT]
> 指派在 hello 存取 toousers**資源群組或訂用帳戶**toowhich 應用程式資源所屬-不在 hello 資源本身。 指派 hello **Application Insights 元件參與者**角色。 這可確保存取 tooweb 測試和警示，以及您的應用程式資源的統一的控制項。 [深入了解](#access)。
> 
> 

## <a name="resources-groups-and-subscriptions"></a>資源、群組和訂用帳戶
首先是一些定義：

* **資源** - Microsoft Azure 服務的執行個體。 Application Insights 資源會收集、 分析及顯示 hello 遙測資料從您的應用程式傳送。  其他類型的 Azure 資源包括 Web 應用程式、資料庫和 VM。
  
    您的資源，開啟 toosee hello [Azure 入口網站][portal]、 登入，然後按一下 所有資源。 toofind 資源，其名稱 hello filter 欄位中的類型部分。
  
    ![Azure 資源清單](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**資源群組**] [ group] -每個資源所屬 tooone 群組。 群組是一種方便的方式 toomanage 相關聯的資源，特別是針對存取控制。 例如，一個資源群組，您無法將 Web 應用程式，Application Insights 資源 toomonitor hello 應用程式，與儲存體資源 tookeep 匯入資料。

    ![選擇 [瀏覽]、[資源群組]，然後選擇 [群組]](./media/app-insights-resources-roles-access-control/11-group.png)

* [**訂用帳戶**](https://manage.windowsazure.com) -toouse Application Insights 或其他 Azure 資源，請在您登入 tooan Azure 訂用帳戶。 每個資源群組所屬 tooone Azure 訂用帳戶，其中您選擇價格封裝，如果它是組織訂用帳戶中，選擇 hello 成員和其存取權限。
* [**Microsoft 帳戶**] [ account] -hello 使用者名稱和密碼，您使用 toosign tooMicrosoft Azure 訂用帳戶、 XBox Live、 Outlook.com 及其他 Microsoft 服務。

## <a name="access"></a>Hello 資源群組中的控制存取
很重要的 toounderstand 在加法 toohello 資源您建立應用程式中，沒有也分隔 隱藏的警示和 web 測試的資源。 它們是附加的 toohello 相同[資源群組](#resource-group)與應用程式。 您也可以在那裡放置其他 Azure 服務，例如網站或儲存體。

![Application Insights 中的資源](./media/app-insights-resources-roles-access-control/00-resources.png)

因此建議您 toocontrol 存取 toothese 資源：

* 控制存取在 hello**資源群組或訂用帳戶**層級。
* 指派 hello**應用程式 Insights 元件參與者**角色 toousers。 這可讓它們 tooedit web 測試、 警示和 Application Insights 資源，而不需提供存取 tooany hello 群組中的其他服務。

## <a name="tooprovide-access-tooanother-user"></a>tooprovide 存取 tooanother 使用者
您必須擁有者權限 toohello 訂用帳戶或 hello 資源群組。

hello 使用者必須擁有[Microsoft 帳戶][account]，或存取 tootheir[組織的 Microsoft 帳戶](../active-directory/sign-up-organization.md)。 您可以提供存取 tooindividuals 以及 toouser Azure Active Directory 中定義的群組。

#### <a name="navigate-toohello-resource-group"></a>瀏覽 toohello 資源群組
將那里 hello 使用者加入。

![在您的應用程式資源刀鋒視窗中，開啟 Essentials 開啟 hello 資源群組，然後在該處選取 設定/使用者。 按一下 [新增]。](./media/app-insights-resources-roles-access-control/01-add-user.png)

或者，您無法向上另一個層級，並加入 hello 使用者 toohello 訂用帳戶。

#### <a name="select-a-role"></a>選取角色
![選取 hello 新使用者角色](./media/app-insights-resources-roles-access-control/03-role.png)

| 角色 | Hello 資源群組中 |
| --- | --- |
| 擁有者 |可以變更任何項目，包括使用者存取 |
| 參與者 |可以編輯任何項目，包括所有資源 |
| Application Insights 元件參與者 |可以編輯 Application Insights 資源、Web 測試和警示 |
| 讀取者 |可以檢視但無法變更任何項目 |

「編輯」包括建立、刪除及更新：

* 資源
* Web 測試
* Alerts
* 連續匯出

#### <a name="select-hello-user"></a>選取 hello 使用者

如果您想要的 hello 使用者不在 hello 目錄中，您可以邀請任何具有 Microsoft 帳戶。
(如果他們使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，他們就會有 Microsoft 帳戶。)

## <a name="related-content"></a>相關內容

* [Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
