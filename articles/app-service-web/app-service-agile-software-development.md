---
title: "使用 Azure App Service aaaAgile 軟體開發"
description: "深入了解如何 toocreate 高延展複雜的應用程式使用 Azure App Service 支援敏捷式軟體開發的方式。"
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
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>使用 Azure App Service 進行敏捷式軟體開發 (Agile Software Development)
在此教學課程中，您將學習如何 toocreate 高延展複雜的應用程式與[Azure App Service](/azure/app-service/)支援的方式[敏捷式軟體開發](https://en.wikipedia.org/wiki/Agile_software_development)。 它會假設您已經知道如何太[部署如預期般在 Azure 中的複雜應用程式](app-service-deploy-complex-application-predictably.md)。

限制技術的處理序中通常可以獨立 hello 成功 agile 方法實作方式。 Azure App Service 功能，例如[持續發行](app-service-continuous-deployment.md)，[預備環境](web-sites-staged-publishing.md)（位置），和[監視](web-sites-monitor.md)、 結合請明智地與 hello 協調流程時及管理網站中的部署[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)，可以是很好的解決方案的一部分的開發採用敏捷式軟體開發人員。

hello 表是靈活的開發與相關聯的需求的簡短清單以及 Azure 服務可讓每個。

| 需求 | 如何讓 Azure |
| --- | --- |
| - 使用每個認可建置<br>- 自動並快速地建置 |設定持續部署時，Azure App Service 可以根據 dev 分支作用為即時執行組建。 每次推送 toohello 分支程式碼，則為自動建置及執行即時 Azure。 |
| - 將組建設為自我測試 |負載測試、 web 測試等，您可以部署與 hello Azure Resource Manager 範本。 |
| - 在生產環境的複製品中執行測試 |Azure 資源管理員範本可以使用的 toocreate 的複製程式碼 hello Azure 生產環境 （包括應用程式設定、 連接字串範本、 調整等） 來測試快速和預測的方式。 |
| - 輕鬆地檢視最新組建結果 |從儲存機制的連續部署 tooAzure 表示，您可以測試新的程式碼中即時應用程式認可您的變更之後，立即。 |
| -認可 toohello 主要分支中每一天<br>- 自動化部署 |持續整合與主要分支中的儲存機制的實際執行應用程式的自動部署每個認可/merge toohello 主要分支 tooproduction。 |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>將執行的作業
您將逐步進行一般的開發人員測試階段-生產工作流程中順序 toopublish 新變更 toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)範例應用程式，都包含兩個[web 應用程式](/services/app-service/web/)，一個是前端 (FE) 和hello 另一個則是 Web API 後端 （相當），和[SQL database](/services/sql-database/)。 您可以使用下列部署架構 hello:

![](./media/app-service-agile-software-development/what-1-architecture.png)

tooput hello 圖片的文字：

* hello 部署架構分成三個不同環境 (或[資源群組](../azure-resource-manager/resource-group-overview.md)在 Azure 中)，每個都有它自己[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，[調整](web-sites-scale.md)設定，與 SQL 資料庫。 
* 您可以個別管理每個環境。 它們甚至可以存在於不同的訂用帳戶中。
* 預備和生產環境會實作為兩個位置的 hello 相同 App Service 應用程式。 持續整合的 hello 主要分支會以 hello staging 位置設定。
* Hello 認可 toomaster 分支時驗證 hello staging （與實際資料） 的位置上，確認臨時的應用程式會為 hello 生產位置交換[不需停機](web-sites-staged-publishing.md)。

hello 生產與預備環境由定義在 hello 範本[  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json)。

hello 開發人員和測試環境由在 hello 範本定義[  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json)。

您也會使用 hello 典型的分支策略，以從 hello dev 分支向上 toohello 測試 」 分支，然後 toohello （向上在品質上，因此 toospeak 移） 的主要分支的程式碼。

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>您需要什麼
* 一個 Azure 帳戶
* 一個 [GitHub](https://github.com/) 帳戶
* Git 殼層 (隨[GitHub for Windows](https://windows.github.com/))-可讓您 toorun 兩者 hello Git 和 PowerShell 中的命令 hello 相同工作階段 
* 最新 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) 位元
* 基本的了解的 hello 下列工具：
  * [Azure Resource Manager ](../azure-resource-manager/resource-group-overview.md)範本部署 (另請參閱[透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> 您需要 Azure 帳戶 toocomplete 本教學課程：
> 
> * 您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)-取得信用額度您可以使用 tootry 出支付 Azure 服務，而且它們甚至用完之後，您可以保留 hello 帳戶並使用免費的 Azure 服務，例如 Web 應用程式。
> * 您可以 [啟用 Visual Studio 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ：您的 Visual Studio 訂用帳戶每個月都會提供額度，供您用在 Azure 付費服務。
> 
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="set-up-your-production-environment"></a>設定生產環境
> [!NOTE]
> 自動使用此教學課程中的 hello 指令碼會設定從 GitHub 儲存機制持續發行。 這會要求您的 GitHub 認證已儲存在 Azure 中，否則 hello 編寫指令碼部署會在失敗時嘗試 tooconfigure hello web 應用程式的原始檔控制設定。 
> 
> toostore 您的 GitHub 認證在 Azure 中建立 web 應用程式在 hello [Azure 入口網站](https://portal.azure.com/)和[設定 GitHub 部署](app-service-continuous-deployment.md)。 您只需要 toodo 這一次。 
> 
> 

在典型的 DevOps 案例中，您必須在 Azure 中，即時執行的應用程式而您想 toomake 變更 tooit 透過連續的發佈功能。 在此案例中，您有範本，您開發、 測試及使用 toodeploy hello 實際執行環境。 您將在本節中設定它。

1. 建立您自己的 hello 分岔[ToDoApp](https://github.com/azure-appservice-samples/ToDoApp)儲存機制。 如需建立分叉的相關資訊，請參閱 [分岔儲存機制](https://help.github.com/articles/fork-a-repo/)。 建立分叉之後，即可在瀏覽器中進行查看。
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. 開啟 Git Shell 工作階段。 若您尚無 Git Shell，請立即安裝 [GitHub for Windows](https://windows.github.com/) 。
3. 建立您分支的本機複本執行下列命令的 hello:

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. 您的本機複本之後，瀏覽過*&lt;repository_root >*\ARMTemplates 及執行的 hello deploy.ps1 指令碼，如下所示：
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. 出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。
   
   您應該會看到 hello 佈建各種不同的 Azure 資源的進度。 當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > 看看 *&lt;repository_root >*\ARMTemplates\Deploy.ps1、 toosee 方式會產生資源的唯一識別碼。 您可以使用相同的方法 toocreate 複製的 hello hello 相同部署而不需擔心衝突的資源名稱。
   > 
   > 
6. 回到 Git Shell 工作階段，並執行：
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Hello 指令碼完成時，請返回 toobrowse toohello 前端的位址 (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello 應用程式在生產環境中執行。
8. 登入 toohello [Azure 入口網站](https://portal.azure.com/)，看看建立的內容。
   
   您應該在 hello 無法 toosee 兩個 web 應用程式相同的資源群組、 具有 hello `Api` hello 名稱中的後置詞。 如果您看一下 hello 資源群組檢視，您也看到 hello SQL 資料庫以及伺服器、 hello 應用程式服務方案及 hello 預備位置 hello web 應用程式。 瀏覽 hello 不同的資源，並比較它們與 *&lt;repository_root >*\ARMTemplates\ProdAndStage.json toosee hello 範本中的設定方式。
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

您現在已設定 hello 實際執行環境。 接下來，您會啟動新的更新 toohello 應用程式。

## <a name="create-dev-and-test-branches"></a>建立開發和測試分支
既然您已在 Azure 中的生產環境中執行複雜的應用程式，您就會更新 tooyour 應用程式根據敏捷式軟體開發方法。 在本節中，您將建立 hello 開發和測試，您將需要 toomake hello 需要更新的分支。

1. 第一次建立 hello 測試環境。 在您的 Git 殼層工作階段中執行的 hello 下列命令呼叫新的分支的 toocreate hello 環境**NewUpdate**。 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. 出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。 
   
   當部署完成時，hello 指令碼會啟動 hello hello 瀏覽器中的應用程式，而且會提供好記的嗶聲。 您現在有新分支與其專屬測試環境。 採用目前 tooreview 此測試環境的相關的幾件事：
   
   * 您可以在任何 Azure 訂用帳戶中建立它。 這表示 hello 實際執行環境可以從您的測試環境的個別加以管理。
   * 您的測試環境是即時在 Azure 中執行。
   * 您的測試環境是相同的 toohello 生產環境中，除了預備位置的 hello 與 hello 調整設定。 您知道它因為它們是 hello ProdandStage.json 與稱為之間唯一的差異。
   * 您可以在其專屬 App Service 方案與不同的價格層 (例如 **免費**) 中管理測試環境 。
   * 刪除這個測試環境很簡單，只刪除 hello 資源群組。 您將了解 toodo 這[稍後](#delete)。
3. 請繼續的 toocreate 執行 dev 分支 hello 下列命令：
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. 出現提示時，在 hello 類型所需的使用者名稱和密碼來存取資料庫。 
   
   採用目前 tooreview 關於此開發人員環境的幾件事： 
   
   * 您的開發人員環境具有組態相同 toohello 測試環境，因為它已部署使用 hello 相同的範本。
   * 每一個開發環境可以建立 hello 開發人員自己的 Azure 訂用帳戶中，保留 hello 測試環境 toobe 分開管理。
   * 您的開發環境是即時在 Azure 中執行。
   * 刪除 hello 開發人員環境很簡單，只刪除 hello 資源群組。 您將了解 toodo 這[稍後](#delete)。

> [!NOTE]
> 當有多位開發人員在 hello 新更新時，每個可以輕鬆地以 hello 步驟下建立分支和專用的開發環境：
> 
> 1. 建立自己的分岔 hello 儲存機制的 GitHub 中 (請參閱[分叉儲存機制](https://help.github.com/articles/fork-a-repo/))。
> 2. 複製其本機電腦上的 「 分叉 」 hello
> 3. 他們自己的 dev 分支和環境的相同命令 toocreate 執行 hello。
> 
> 

完成之後，GitHub 分岔應該會有三個分支：

![](./media/app-service-agile-software-development/test-1-github-view.png)

而三個不同的資源群組中應該會有六個 Web 應用程式 (兩個一組，共三組)：

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json 指定 hello 實際執行環境 toouse hello**標準**定價層，適用於 hello 實際執行應用程式的延展性。
> 
> 

## <a name="build-and-test-every-commit"></a>建置和測試每個認可
hello ProdAndStage.json 的範本檔案，稱為已指定 hello 來源控制參數，預設會設定持續發行 hello web 應用程式。 因此，每個認可 toohello GitHub 分支會觸發自動部署 tooAzure，從該分支。 我們來看看您設定現在的運作方式。

1. 請確定您在 hello Dev 分支的 hello 本機儲存機制。 toodo 下列 Git 命令介面中的命令，執行的 hello:
   
        git checkout Dev
2. 請變更 toohello 應用程式的 UI 層藉由變更 hello 程式碼 toouse [Bootstrap](http://getbootstrap.com/components/)列出。 開啟 *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml 並進行 hello 反白顯示的變更之後：
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > 如果您無法讀取 hello 上述映像： 
    > 
    > * 在行 18，變更`check-list`太`list-group`。
    > * 在行 19，變更`class="check-list-item"`太`class="list-group-item"`。
    > 
    > 
3. 儲存 hello 變更。 備份在 Git 命令介面中執行下列命令的 hello:
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   這些 git 命令如下太"正在檢查您的程式碼 」 中的另一個原始檔控制系統，例如 TFS。 當您執行`git push`，觸發程序的自動程式碼推入 tooAzure，哪些然後重建 hello hello 開發環境中的應用程式 tooreflect hello 變更 hello 新認可。
4. tooverify 發生此程式碼推入 tooyour 開發環境中，移至 tooyour 開發人員環境的 web 應用程式頁面，並查看 hello**部署**組件。 您應該能夠 toosee 您最新的認可訊息有。
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. 從該處，請按一下**瀏覽**toosee hello hello Azure 中的即時應用程式中的新變更。
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   它是次要變更 toohello 應用程式。 不過，許多新的變更 tooa 複雜的 web 應用程式時間有非預期且非預期的副作用。 要能 tooeasily 測試即時組建中的每個認可可讓您 toocatch 這些問題之前，您的客戶會看到它們。

現在，您應該熟悉 hello 實現，身為開發人員在 hello **NewUpdate**專案中，您可以建立，為您自己的開發環境，然後建置每次認可和測試每次建置。

## <a name="merge-code-into-test-environment"></a>將程式碼合併至測試環境
當您準備好 toopush 開發人員從程式碼分支向上 tooNewUpdate 分支時，它會是 hello 標準 git 程序：

1. 合併在 GitHub 中，例如建立其他開發人員所認可的 hello Dev 分支中的任何新的認可 tooNewUpdate。 GitHub 上的任何新認可觸發程式碼推播和 hello 開發環境中的組建。 您接著可以確定 Dev 分支中的程式碼仍適用於從 NewUpdate 分支 hello 最新的位元。
2. 在 GitHub 中，將所有新認可從 Dev 分支合併至 NewUpdate 分支。 這個動作會觸發程式碼推播和 hello 測試環境中的組建。 

請注意，一次與這些的 git 分支已設定連續部署，因為您不需要任何其他動作，例如執行整合組建的 tootake。 您只需要使用 git，tooperform 標準原始檔控制實務，Azure 會為您執行所有的 hello 建置處理序。

現在，讓我們推送您的程式碼太**NewUpdate**分支。 在 Git 命令介面中執行下列命令的 hello:

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

這樣就大功告成了！ 

移 toohello web 應用程式頁面為您的測試環境 toosee 您新認可 （合併至 NewUpdate 分支） 現在推送 toohello 測試環境。 然後，按一下 **瀏覽**hello 樣式變更的 toosee 現在正在執行即時 Azure 中。

## <a name="deploy-update-tooproduction"></a>部署更新 tooproduction
將程式碼 toohello 推入暫存和實際執行環境應該感覺受到總公司什麼您已完成推送程式碼 toohello 測試環境時沒有任何差異。 真的就是這麼簡單。 

在 Git 命令介面中執行下列命令的 hello:

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

請記住，根據 ProdandStage.json 設定 hello 預備和生產環境的 hello 方式、 新的程式碼都會被推送 toohello**暫存**位置，而且那里正在執行。 因此如果您瀏覽 toohello 預備位置的 URL，您會看到那里執行 hello 新程式碼。 toodo 遵循 Git 命令介面中的 cmdlet，執行的 hello。

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

現在，我們已經確認 hello 暫存位置中的 hello 更新之後，hello 僅保留 toodo 是 tooswap 和它到實際執行環境。 在 Git 殼層，只執行 hello 下列命令：

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

恭喜！ 您已成功發行新更新 tooyour 生產 web 應用程式。 不僅如此，完成的方式也只是輕鬆地建立開發和測試環境，以及建置和測試每個認可。 這些是敏捷式軟體開發的重要建置組塊。

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>刪除開發和測試環境
因為您刻意架構您的開發人員和測試環境 toobe 各自獨立的資源群組，很容易 toodelete 它們。 toodelete hello 本教學課程，hello GitHub 分支和 Azure 的成品，您建立的項目只會執行下列命令在 Git 介面中的 hello:

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>摘要
敏捷式軟體開發是必備的許多公司想 tooadopt Azure 做為其應用程式平台。 在本教學課程中，您已經學會如何 toocreate 及撤除下確切的複本或附近的複本 hello 生產環境使用方便，甚至針對複雜的應用程式。 您也學會如何 tooleverage 這個能力 toocreate 開發程序可建立及測試在 Azure 中的每個單一認可。 本教學課程希望示範了如何最適合使用 Azure App Service 與 Azure 資源管理員一起 toocreate 皆代表 tooagile 方法 DevOps 方案。 接下來，您可以透過執行進階 DevOps 技術 (例如 [在生產環境中測試](app-service-web-test-in-production-get-start.md))，建置此案例。 如需生產過程中測試的常見案例，請參閱 [Azure App Service 中的快速部署 (beta 測試)](app-service-web-test-in-production-controlled-test-flight.md)。

## <a name="more-resources"></a>其他資源
* [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)
* [敏捷式開發作法：現代化開發週期的秘訣和訣竅](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [使用資源管理員範本之 Azure Web 應用程式的進階部署策略](http://channel9.msdn.com/Events/Build/2015/2-620)
* [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint-hello JSON 驗證程式](http://jsonlint.com/)
* [GitHub 發行 toosite ARMClient – 設定](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Git 分支 - 基本分支和合併](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [David Ebbo 的部落格](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure 跨平台命令列工具](../cli-install-nodejs.md)
* [在 Azure AD 中建立或編輯使用者](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [專案 Kudu Wiki](https://github.com/projectkudu/kudu/wiki)

