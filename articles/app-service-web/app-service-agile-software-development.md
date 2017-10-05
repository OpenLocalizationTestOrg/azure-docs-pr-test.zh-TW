---
title: "使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)"
description: "學習如何使用支援敏捷式軟體開發的方式來建立高級別複雜應用程式與 Azure App Service。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 5ed888cbb422766cf2094f5980dfd1c599bd431c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)
在本教學課程中，您將學習如何使用支援[敏捷式軟體開發](https://en.wikipedia.org/wiki/Agile_software_development)的方式，使用 [Azure App Service](/azure/app-service/) 建立高級別複雜應用程式。 假設您已經知道如何 [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)。

技術程序限制通常會妨礙成功的實作敏捷式方法。 如果在 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 中明智地結合部署的協調流程與管理，則 Azure App Service 與功能 (例如[持續發佈](app-service-continuous-deployment.md)、[預備環境](web-sites-staged-publishing.md) (位置) 和[監視](web-sites-monitor.md)) 是非常適合採用敏捷式軟體開發之開發人員的解決方案。

下表是敏捷式開發相關需求以及 Azure 服務如何啟用它們的簡短清單。

| 需求 | 如何讓 Azure |
| --- | --- |
| - 使用每個認可建置<br>- 自動並快速地建置 |設定持續部署時，Azure App Service 可以根據 dev 分支作用為即時執行組建。 每次將程式碼推送至分支時，在 Azure 中就會自動建置和即時執行程式碼。 |
| - 將組建設為自我測試 |負載測試、Web 測試等可以使用 Azure 資源管理員範本進行部署。 |
| - 在生產環境的複製品中執行測試 |Azure 資源管理員範本可以用來建立 Azure 生產環境的複製品 (包括應用程式設定、連接字串範本、縮放等) 以透過快速且可預測的方式測試。 |
| - 輕鬆地檢視最新組建結果 |從儲存機制持續部署至 Azure，表示您可以在認可變更之後立即於即時應用程式中測試新程式碼。 |
| - 每天認可到主要分支<br>- 自動化部署 |生產應用程式與儲存機制主要分支的連續整合會自動將主要分支的每次認可/合併部署至生產環境。 |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>將執行的作業
您將逐步進行一般「開發-測試-預備-生產」工作流程，以將新變更發佈至 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 範例應用程式 (內含兩個 [Web 應用程式](/services/app-service/web/)：一個是前端 (FE)，另一個是 Web API 後端 (BE)) 和 [SQL 資料庫](/services/sql-database/)。 您將使用下列部署架構：

![](./media/app-service-agile-software-development/what-1-architecture.png)

若要將圖片放入文字：

* 部署架構分成三個不同環境 (或 Azure 中的[資源群組](../azure-resource-manager/resource-group-overview.md))，其各有專屬 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)、[調整](web-sites-scale.md)設定和 SQL 資料庫。 
* 您可以個別管理每個環境。 它們甚至可以存在於不同的訂用帳戶中。
* 預備和生產環境會實作為相同 App Service 應用程式的兩個位置。 主要分支是設定進行具有預備位置的連續整合。
* 在預備位置 (含生產資料) 上驗證主要分支的認可時，已驗證的預備應用程式會交換到生產位置， [而不中斷](web-sites-staged-publishing.md)。

生產和預備環境是由 [*&lt;repository_root>*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json) 上的範本所定義。

開發和測試環境是由 [*&lt;repository_root>*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json) 上的範本所定義。

您也將使用一般分支策略，其中，程式碼會從開發分支移至測試分支，然後移至主要分支 (就是所謂的提升品質)。

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>您需要什麼
* 一個 Azure 帳戶
* 一個 [GitHub](https://github.com/) 帳戶
* Git Shell (與 [GitHub for Windows](https://windows.github.com/)一起安裝) - 這可讓您在相同的工作階段中執行 Git 和 PowerShell 命令 
* 最新 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 位元
* 下列工具的基本了解：
  * [Azure Resource Manager ](../azure-resource-manager/resource-group-overview.md)範本部署 (另請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> 要完成此教學課程，您必須要有 Azure 帳戶：
> 
> * 您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/) ：您將取得可試用 Azure 付費服務的額度，且即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務，例如 Web Apps。
> * 您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。
> 
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；沒有承諾。
> 
> 

## <a name="set-up-your-production-environment"></a>設定生產環境
> [!NOTE]
> 本教學課程中使用的指令碼會自動從 GitHub 存放庫設定連續發佈。 這需要您的 GitHub 認證已儲存在 Azure 中，否則，嘗試設定 Web 應用程式的原始檔控制設定時，指令碼部署會失敗。 
> 
> 若要在 Azure 中儲存您的 GitHub 認證，請在 [Azure 入口網站](https://portal.azure.com/)中建立 Web 應用程式，並[設定 GitHub 部署](app-service-continuous-deployment.md)。 您只需要做一次這個動作。 
> 
> 

在一般 DevOps 案例中，應用程式是在 Azure 中即時執行，而且您想要透過連續發行對它進行變更。 在此案例中，您會有您所開發、測試以及用來部署生產環境的範本。 您將在本節中設定它。

1. 建立 [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) 儲存機制的專屬分叉。 如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。 建立分叉之後，即可在瀏覽器中進行查看。
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. 開啟 Git Shell 工作階段。 若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。
3. 執行下列命令，以建立分叉的本機複製品：

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. 具有本機副本後，瀏覽至 *&lt;repository_root>*\ARMTemplates，然後執行 deploy.ps1 指令碼，如下所示：
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. 系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。
   
   您應該會看到各種 Azure 資源的佈建進度。 部署完成時，指令碼會在瀏覽器中啟動應用程式，並提供合適的嗶聲。
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > 查看 *&lt;repository_root>*\ARMTemplates\Deploy.ps1，以了解其如何產生具有唯一識別碼的資源。 您可以使用相同的方法來建立相同部署的複製品，而不需擔心衝突的資源名稱。
   > 
   > 
6. 回到 Git Shell 工作階段，並執行：
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. 指令碼完成時，請返回瀏覽至前端的位址 (http://ToDoApp*&lt;unique_string>*master.azurewebsites.net/)，以查看在生產環境中執行的應用程式。
8. 登入 [Azure 入口網站](https://portal.azure.com/) ，並查看建立的內容。
   
   您應可在相同的資源群組中看到兩個 Web 應用程式，其中一個的名稱具有 `Api` 後置詞。 如果您查看資源群組檢視，則也會看到 SQL Database 和伺服器、App Service 方案以及 Web 應用程式的預備位置。 瀏覽不同的資源，並將其與 *&lt;repository_root>*\ARMTemplates\ProdAndStage.json 比較以查看其在範本中的設定方式。
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

您現在已設定生產環境。 接下來，您將會開始執行應用程式的新更新。

## <a name="create-dev-and-test-branches"></a>建立開發和測試分支
現在，您已有在 Azure 內之生產環境中執行的複雜應用程式，您將根據敏捷式方法來更新應用程式。 在本節中，您將建立需要進行必要更新的開發和測試分支。

1. 先建立測試環境。 在 Git Shell 工作階段中，執行下列命令來建立稱為 **NewUpdate**的新分支環境。 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. 系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。 
   
   部署完成時，指令碼會在瀏覽器中啟動應用程式，並提供合適的嗶聲。 您現在有新分支與其專屬測試環境。 請花一點時間檢閱此測試環境的一些相關事項：
   
   * 您可以在任何 Azure 訂用帳戶中建立它。 這表示可以分開管理生產環境和測試環境。
   * 您的測試環境是即時在 Azure 中執行。
   * 您的測試環境等同於生產環境，差異在於預備位置和調整設定。 因為這些是 ProdandStage.json 與 Dev.json 之間的唯一差異，所以您可以得知這項資訊。
   * 您可以在其專屬 App Service 方案與不同的價格層 (例如 **免費**) 中管理測試環境 。
   * 刪除這個測試環境，就像刪除資源群組一樣簡單。 您將了解 [稍後](#delete)如何執行這項作業。
3. 執行下列命令，以繼續建立開發分支：
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. 系統提示時，請輸入所需的使用者名稱和密碼來存取資料庫。 
   
   請花一點時間檢閱此開發環境的一些相關事項： 
   
   * 開發環境的組態與測試環境相同，因為它是使用相同的範本所部署。
   * 在開發人員自己的 Azure 訂用帳戶中，可以建立每個開發環境，但分開管理測試環境。
   * 您的開發環境是即時在 Azure 中執行。
   * 刪除開發環境，就像刪除資源群組一樣簡單。 您將了解 [稍後](#delete)如何執行這項作業。

> [!NOTE]
> 有多位開發人員處理新的更新時，只要執行下列步驟，每一位都可以輕鬆地建立分支和專用開發環境：
> 
> 1. 在 GitHub 建立其在儲存機制中的專屬分叉 (請參閱 [分叉儲存機制](https://help.github.com/articles/fork-a-repo/))。
> 2. 複製其本機電腦上的分岔
> 3. 執行相同的命令，來建立其專屬開發分支和環境。
> 
> 

完成之後，GitHub 分岔應該會有三個分支：

![](./media/app-service-agile-software-development/test-1-github-view.png)

而三個不同的資源群組中應該會有六個 Web 應用程式 (兩個一組，共三組)：

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json 指定生產環境來使用**標準**定價層，這適用於生產應用程式的延展性。
> 
> 

## <a name="build-and-test-every-commit"></a>建置和測試每個認可
範本檔 ProdAndStage.json 和 Dev.json 已經指定原始控制碼參數，其預設會設定 Web 應用程式的連續發行。 因此，GitHub 分支的每個認可都會觸發從該分支自動部署至 Azure。 我們來看看您設定現在的運作方式。

1. 請確定您在本機儲存機制的 Dev 分支。 若要這樣做，請在 Git Shell 中執行下列命令：
   
        git checkout Dev
2. 將程式碼變更為使用 [Bootstrap](http://getbootstrap.com/components/) 清單，以對應用程式的 UI 層進行變更。 開啟 *&lt;repository_root>*\src\MultiChannelToDo.Web\index.cshtml，並進行以下反白顯示的變更：
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > 如果您無法讀取上述的影像： 
    > 
    > * 在第 18 行，將 `check-list` 變更為 `list-group`。
    > * 在第 19 行，將 `class="check-list-item"` 變更為 `class="list-group-item"`。
    > 
    > 
3. 儲存變更。 回到 Git Shell，並執行下列命令：
   
        cd <repository_root>
        git add .
        git commit -m "changed to bootstrap style"
        git push origin Dev
   
   這些 git 命令與另一個原始檔控制系統中的「簽入程式碼」類似 (例如 TFS)。 執行 `git push`時，新的認可會觸發自動將程式碼推送至 Azure，然後重建應用程式，以反映開發環境中的變更。
4. 若要確認已將此程式碼推送至您的開發環境，請移至您開發環境的 Web 應用程式分頁，並查看 [部署] 組件。 您應該可以在這裡看到最新認可的訊息。
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. 在其中按一下 [瀏覽]  ，以查看 Azure 中即時應用程式的新變更。
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   這對應用程式而言是相當小的變更。 不過，複雜 Web 應用程式的新變更通常會有不想要和非預期的副作用。 能夠輕鬆地測試即時組建中的每個認可，可讓您在客戶看到這些問題之前先找出它們。

現在，您應已熟悉開發人員在 **NewUpdate** 專案中如何實現，並可以輕鬆地建立專屬開發環境，然後建置每個認可並測試每個組建。

## <a name="merge-code-into-test-environment"></a>將程式碼合併至測試環境
準備好將程式碼從 Dev 分支推送至 NewUpdate 分支時，這是標準 git 程序：

1. 在 GitHub 中，將 NewUpdate 的任何新認可合併至 Dev 分支 (例如其他開發人員所建立的認可)。 GitHub 上的任何新認可都會在開發環境中觸發程式碼推送和建置。 您接著可以確定 Dev 分支中的程式碼仍能與 NewUpdate 分支中的最新位元運作。
2. 在 GitHub 中，將所有新認可從 Dev 分支合併至 NewUpdate 分支。 這個動作會在測試環境中觸發程式碼推送和建置。 

請再次注意，因為連續部署已設定這些 git 分支，所以不需要採取任何其他動作 (例如執行整合建置)。 您只需要使用 git 執行標準原始檔控制作法，Azure 就會為您執行所有建置程序。

現在，請將您的程式碼推送至 **NewUpdate** 分支。 在 Git Shell 中，執行下列命令：

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

這樣就大功告成了！ 

前往您測試環境的 Web 應用程式分頁，以查看現在推送至測試環境的新認可 (合併至 NewUpdate 分支)。 然後按一下 [瀏覽]  ，以查看現在於 Azure 中即時執行的樣式變更。

## <a name="deploy-update-to-production"></a>將更新部署至生產環境
將程式碼推送至預備和生產環境，應該與先前將程式碼所推送的測試環境相同。 真的就是這麼簡單。 

在 Git Shell 中，執行下列命令：

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

請記住，根據在 ProdandStage.json 中設定預備和生產環境的方式，新的程式碼會推送至 [預備] 位置並在該處執行。 因此，如果您導覽至預備位置的 URL，則會看到新的程式碼正在該處執行。 若要這樣做，請在 Git Shell 中執行下列 Cmdlet。

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

現在，在預備位置中驗證過更新之後，唯一需要執行的事項是將它交換至生產環境。 在 Git Shell 中，只要執行下列命令：

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

恭喜！ 您已順利將新的更新發行至生產 Web 應用程式。 不僅如此，完成的方式也只是輕鬆地建立開發和測試環境，以及建置和測試每個認可。 這些是敏捷式軟體開發的重要建置組塊。

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>刪除開發和測試環境
因為您刻意將開發和測試環境架構為獨立資源群組，所以可以很容易刪除它們。 若要刪除您在本教學課程中建立的環境 (GitHub 分支和 Azure 構件)，則只要在 Git Shell 中執行下列命令：

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>摘要
對於許多想要採用 Azure 做為其應用程式平台的公司而言，敏捷式軟體開發是必要的。 在本教學課程中，您已經學會如何輕鬆地建立和終止生產環境的確切複本或接近複本，甚至針對複雜應用程式也是一樣。 您也學到如何運用這項功能來建立開發程序，以建置和測試 Azure 中的每個認可。 本教學課程希望示範如何最恰當地搭配使用 Azure App Service 和 Azure 資源管理員，來建立提供敏捷式方法的 DevOps 方案。 接下來，您可以透過執行進階 DevOps 技術 (例如 [在生產環境中測試](app-service-web-test-in-production-get-start.md))，建置此案例。 如需生產過程中測試的常見案例，請參閱 [Azure App Service 中的快速部署 (beta 測試)](app-service-web-test-in-production-controlled-test-flight.md)。

## <a name="more-resources"></a>其他資源
* [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)
* [敏捷式開發作法：現代化開發週期的秘訣和訣竅](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [使用資源管理員範本之 Azure Web 應用程式的進階部署策略](http://channel9.msdn.com/Events/Build/2015/2-620)
* [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - JSON 驗證程式](http://jsonlint.com/)
* [ARMClient - 設定 GitHub 發行至網站](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [分支 - 基本分支和合併](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo 的部落格](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure 跨平台命令列工具](../cli-install-nodejs.md)
* [在 Azure AD 中建立或編輯使用者](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [專案 Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

