---
title: "aaaDeploy Azure Service Fabric 應用程式使用持續整合 (Team Services) |Microsoft 文件"
description: "深入了解如何 tooset 連續整合和部署使用 Visual Studio Team Services Service Fabric 應用程式。  部署 Azure 應用程式 tooa Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>部署應用程式與 CI/CD tooa Service Fabric 叢集
本教學課程是三個一系列的一部分，並說明如何 tooset 連續整合和部署 Azure Service Fabric 應用程式使用 Visual Studio Team Services。  現有的 Service Fabric 應用程式需要會在建立 hello 應用程式[建置.NET 應用程式](service-fabric-tutorial-create-dotnet-app.md)用做為範例。

在 hello 系列的一部分三，您將學習如何：

> [!div class="checklist"]
> * 加入原始檔控制 tooyour 專案
> * 在 Team Services 中建立組建定義
> * 在 Team Services 中建立發行定義
> * 自動部署和升級應用程式

在本教學課程系列中，您將了解如何：
> [!div class="checklist"]
> * [建置 .NET Service Fabric 應用程式](service-fabric-tutorial-create-dotnet-app.md)
> * [部署 hello 應用程式 tooa 遠端叢集](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * 使用 Visual Studio Team Services 設定 CI/CD

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前：
- 如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。
- [安裝 hello Service Fabric SDK](service-fabric-get-started.md)
- 建立 Service Fabric 應用程式，例如[遵循本教學課程](service-fabric-tutorial-create-dotnet-app.md)。 
- 在 Azure 上建立 Windows Service Fabric 叢集，例如[遵循本教學課程](service-fabric-tutorial-create-cluster-azure-ps.md)
- 建立 [Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。

## <a name="download-hello-voting-sample-application"></a>下載 hello 投票範例應用程式
如果您未建立 hello 投票範例應用程式[第一部此教學課程系列的](service-fabric-tutorial-create-dotnet-app.md)，您可以下載它。 在命令視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>下載發行設定檔
現在，您已經[建立的應用程式](service-fabric-tutorial-create-dotnet-app.md)，而且有[部署 hello 應用程式 tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)，您已準備好 tooset 連續整合。  首先，準備用於應用程式中的發行設定檔的 Team Services 中執行的 hello 部署程序。  hello 發行設定檔應該是您先前建立的設定的 tootarget hello 叢集。  啟動 Visual Studio，並開啟現有的 Service Fabric 應用程式專案。  在**方案總管 中**，hello 應用程式上按一下滑鼠右鍵，然後選取**發行...**.

選擇目標設定檔內的連續整合流程您應用程式專案 toouse，例如雲端。  指定 hello 叢集連線端點。  檢查 hello**升級 hello 應用程式**核取方塊，讓您的應用程式升級的 Team Services 中的每個部署。  按一下 hello**儲存**超連結 toosave hello 設定 toohello 發行設定檔，然後按一下**取消**tooclose hello 對話方塊。  

![推送設定檔][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>共用您 Visual Studio 方案 tooa 新 Team Services 的 Git 儲存機制
共用 tooa team 專案，因此您可以產生 Team Services 中的建置您的應用程式原始程式檔。  

選取建立新本機 Git 儲存機制專案**新增 tooSource 控制項** -> **Git** hello 右下角的 Visual Studio 中的 hello 狀態列上。 

在 hello**推播**檢視中**Team Explorer**，選取 hello**發行 Git 儲存機制**按鈕底下**推送 tooVisual Studio Team Services**。

![推送 Git 儲存機制][push-git-repo]

請確認您的電子郵件，然後選取您的帳戶在 hello **Team Services 網域**下拉式清單。 輸入您的儲存機制名稱，並選取 [發佈儲存機制]。

![推送 Git 儲存機制][publish-code]

發行 hello 儲存機制為 hello 本機儲存機制名稱相同的 hello 與您帳戶中建立新的 team 專案。 toocreate hello 儲存機制，在現有 team 專案中，按一下**進階**下一步太**儲存機制**命名，並選取 team 專案。 您也可以選取 hello web 上檢視您的程式碼**hello web 上可以看到**。

## <a name="configure-continuous-delivery-with-vsts"></a>設定 VSTS 的持續傳遞
Team Services 組建定義描述由一組循序執行的組建步驟所組成的工作流程。 建立組建定義，會產生 Service Fabric 應用程式封裝時，其他的成品、 toodeploy tooa Service Fabric 叢集。 深入了解 [Team Services 組建定義](https://www.visualstudio.com/docs/build/define/create)。 

Team Services 發行定義描述將部署應用程式封裝 tooa 叢集工作流程。 Hello 一起使用時，組建定義，並發行定義執行開頭為與叢集中執行的應用程式的來源檔案 tooending hello 整個工作流程。 深入了解 Team Services [發行定義](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)。

### <a name="create-a-build-definition"></a>建立組建定義
開啟網頁瀏覽器並瀏覽在 tooyour 新 team 專案： https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting。 

選取 hello**建置和發行**索引標籤，然後**建置**，然後**+ 新定義**。  在**選取範本**，選取 hello **Azure Service Fabric 應用程式**範本，然後按一下**套用**。 

![選擇組建範本][select-build-template] 

hello 投票應用程式包含.NET Core 專案，因此加入還原 hello 相依性的工作。 在 hello**工作**檢視中，選取**+ 加入工作**在 hello 左下方。 搜尋 「 命令列"toofind hello 命令列工作，然後按一下 **新增**。 

![新增工作][add-task] 

在 hello 新工作中，「 執行 dotnet.exe 」 中輸入**顯示名稱**中的"dotnet.exe"**工具**，和 「 還原 」 中**引數**。 

![新增工作][new-task] 

在 hello**觸發程序**檢視中，按一下 hello**啟用此觸發程序**下切換**連續整合**。 

選取**儲存，並佇列**並輸入"裝載 VS2017 」 為 hello**代理程式佇列**。 選取**佇列**toomanually 啟動組建。  推送或簽入時也會觸發組建。

toocheck 組建進度、 交換器 toohello**建置** 索引標籤。一旦您確認 hello 組建執行成功，定義來部署您的應用程式 tooa 叢集發行定義。 

### <a name="create-a-release-definition"></a>建立發行定義  

選取 hello**建置和發行**索引標籤，然後**版本**，然後**+ 新定義**。  在**建立發行定義**，選取 hello **Azure Service Fabric 部署**範本從 hello 清單，然後按一下**下一步**。  選取 hello**建置**來源，請檢查 hello**連續部署**方塊，然後按一下**建立**。 

在 hello**環境**檢視中，按一下**新增**toohello 右邊**叢集連線**。  指定 hello 叢集 」 mysftestcluster"，"tcp://mysftestcluster.westus.cloudapp.azure.com:19000 」，和 hello Azure Active Directory 或憑證認證的叢集端點的連接名稱。 對於 Azure Active Directory 認證，請定義您想要在 hello toouse tooconnect toohello 叢集 hello 認證**Username**和**密碼**欄位。 以憑證為基礎的驗證，定義 hello Base64 編碼的 hello 用戶端憑證檔案，在 hello**用戶端憑證**欄位。  請參閱 hello 說明快顯視窗，該欄位有關的資訊 tooget 該值。  如果您的憑證是否受密碼保護，定義 hello 密碼 hello**密碼**欄位。  按一下**儲存**toosave hello 發行定義。

![新增叢集連線][add-cluster-connection] 

按一下 [在代理程式上執行]，然後針對 [部署佇列] 選取 [Hosted VS2017]。 按一下**儲存**toosave hello 發行定義。

![在代理程式上執行][run-on-agent]

選取**+ 釋放** -> **建立發行** -> **建立**toomanually 建立發行。  請確認已成功將 hello 部署 hello 應用程式正在執行 hello 叢集中。  開啟網頁瀏覽器並瀏覽過[http://mysftestcluster.westus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)。  請注意此範例中是"1.0.0.20170616.3 」 中的 hello 應用程式版本。 

## <a name="commit-and-push-changes-trigger-a-release"></a>認可並推送變更，觸發發行程序
hello 連續整合管線的 tooverify 正在運作的一些程式碼將變更簽入 tooTeam 服務。    

您撰寫程式碼時，Visual Studio 會自動追蹤您的變更。 認可變更 tooyour 本機 Git 儲存機制，藉由選取 hello 暫止的變更圖示 （![Pending][pending]) 從在 hello 右下方的 hello 狀態列。

在 hello**變更**檢視在 Team Explorer 中，加入描述您的更新的訊息和認可您的變更。

![全部認可][changes]

選取 hello 未發行的變更狀態列圖示 (![未發行的變更][unpublished-changes]) 或 hello Team 總管 中的同步處理檢視。 選取**推送**tooupdate Team Services/TFS 中程式碼。

![推送變更][push]

推送 hello 變更 tooTeam 服務會自動觸發程序建置。  Hello 組建定義已成功完成時，發行就會自動建立，並開始升級 hello hello 叢集上的應用程式。

toocheck 組建進度、 交換器 toohello**建置**索引標籤中**Team Explorer** Visual Studio 中。  一旦您確認 hello 組建執行成功，定義來部署您的應用程式 tooa 叢集發行定義。

請確認已成功將 hello 部署 hello 應用程式正在執行 hello 叢集中。  開啟網頁瀏覽器並瀏覽過[http://mysftestcluster.westus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/)。  請注意此範例中是"1.0.0.20170815.3 」 中的 hello 應用程式版本。

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>更新 hello 應用程式
在 hello 應用程式進行程式碼變更。  儲存並認可 hello 變更，hello 上一個步驟。

一旦 hello 升級的 hello 應用程式開始，您可以觀看 hello Service Fabric 總管中的升級進度：

![Service Fabric Explorer][sfx2]

hello 應用程式升級可能需要幾分鐘的時間。 Hello 升級完成後，hello 應用程式將會執行下一版的 hello。  在此範例中為 "1.0.0.20170815.4"。

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 加入原始檔控制 tooyour 專案
> * 建立組建定義
> * 建立發行定義
> * 自動部署和升級應用程式

既然您已部署應用程式，並設定連續整合，請嘗試下列 hello:
- [升級應用程式](service-fabric-application-upgrade.md)
- [測試應用程式](service-fabric-testability-overview.md) 
- [監視與診斷](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png