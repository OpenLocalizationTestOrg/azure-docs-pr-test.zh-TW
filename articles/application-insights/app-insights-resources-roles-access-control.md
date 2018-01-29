---
title: "Azure Application Insights 中的資源、角色及存取控制 | Microsoft Docs"
description: "您的組織詳細資料的擁有者、參與者及讀者。"
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: mbullwin
ms.openlocfilehash: 6e811c9b427469fa781cf1f5b7c7deff3a8e6eb3
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Application Insights 中的資源、角色及存取控制
您可以使用 [Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md) ，控制誰對您在 Azure [Application Insights][start] 中的資料具有讀取和更新存取權。

> [!IMPORTANT]
> 指派存取權給您的應用程式資源所屬之 **資源群組或訂用帳戶** 中的使用者 - 不在資源本身。 指派 **Application Insights 元件參與者** 角色。 這可確保 Web 測試和警示以及您的應用程式資源的統一存取控制。 [深入了解](#access)。
> 
> 

## <a name="resources-groups-and-subscriptions"></a>資源、群組和訂用帳戶
首先是一些定義：

* **資源** - Microsoft Azure 服務的執行個體。 您的 Application Insights 資源會收集、分析及顯示從您的應用程式傳送的遙測資料。  其他類型的 Azure 資源包括 Web 應用程式、資料庫和 VM。
  
    若要查看資源，請開啟 [Azure 入口網站][portal]，登入並按一下 [所有資源]。 若要尋找的資源，請在篩選欄位中輸入名稱的一部分。
  
    ![Azure 資源清單](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [資源群組][group] - 每個資源屬於一個群組。 群組是管理相關資源的便利方式，特別是針對存取控制。 例如，您可以將 Web 應用程式、Application Insights 資源放到一個資源群組，以監視應用程式，以及放到儲存體資源以保存匯出的資料。

    ![選擇 [瀏覽]、[資源群組]，然後選擇 [群組]](./media/app-insights-resources-roles-access-control/11-group.png)

* [**訂用帳戶**](https://portal.azure.com) - 若要使用 Application Insights 或其他 Azure 資源，您可以登入 Azure 訂用帳戶。 每個資源群組都屬於一個 Azure 訂用帳戶，其中您選擇價格封裝，如果是組織的訂用帳戶，請選擇成員以及其存取權限。
* [**Microsoft 帳戶**][account] - 您用來登入 Microsoft Azure 訂用帳戶、XBox Live、Outlook.com 及其他 Microsoft 服務的使用者名稱和密碼。

## <a name="access"></a> 控制資源群組中的存取
請務必了解除了您為應用程式建立的資源之外，還有警示和 Web 測試的個別隱藏資源。 它們會附加到與您的應用程式相同的 [資源群組](#resource-group) 。 您也可以在那裡放置其他 Azure 服務，例如網站或儲存體。

![Application Insights 中的資源](./media/app-insights-resources-roles-access-control/00-resources.png)

為了控制這些資源的存取，因此建議您：

* 在 **資源群組或訂用帳戶** 層級控制存取。
* 指派 **Application Insights 元件參與者** 角色給使用者。 這可讓他們編輯 Web 測試、警示和 Application Insights 資源，而不用提供群組中任何其他服務的存取權。

## <a name="to-provide-access-to-another-user"></a>若要提供存取權給其他使用者
您必須擁有訂用帳戶或資源群組的擁有者權限。

使用者必須擁有 [Microsoft 帳戶][account]，或其[組織的 Microsoft 帳戶](../active-directory/sign-up-organization.md)存取權。 您可以提供存取權給個人，也可以提供給在 Azure Active Directory 中定義的使用者群組。

#### <a name="navigate-to-the-resource-group"></a>瀏覽至資源群組
在那裡新增使用者。

![在您的應用程式資源刀鋒視窗中，開啟 Essentials、開啟資源群組，然後在該處選取 [設定/使用者]。 按一下 [加入]。](./media/app-insights-resources-roles-access-control/01-add-user.png)

或者，您可以上移至另一個層級，並且將使用者加入至訂用帳戶。

#### <a name="select-a-role"></a>選取角色
![選取新使用者的角色](./media/app-insights-resources-roles-access-control/03-role.png)

| 角色 | 在資源群組中 |
| --- | --- |
| 擁有者 |可以變更任何項目，包括使用者存取 |
| 參與者 |可以編輯任何項目，包括所有資源 |
| Application Insights 元件參與者 |可以編輯 Application Insights 資源、Web 測試和警示 |
| 讀取者 |可以檢視但無法變更任何項目 |

「編輯」包括建立、刪除及更新：

* 資源
* Web 測試
* 警示
* 連續匯出

#### <a name="select-the-user"></a>選取使用者

如果您想要的使用者不在目錄中，您可以邀請任何具有 Microsoft 帳戶的使用者。
(如果他們使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，他們就會有 Microsoft 帳戶。)

## <a name="related-content"></a>相關內容

* [Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
