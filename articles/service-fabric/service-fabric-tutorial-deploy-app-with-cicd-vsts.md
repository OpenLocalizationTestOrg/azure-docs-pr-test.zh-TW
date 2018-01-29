---
title: "使用持續整合 (Team Services) 部署 Azure Service Fabric 應用程式 |Microsoft Docs"
description: "了解如何使用 Visual Studio Team Services 設定 Service Fabric 應用程式的持續整合和部署。  將應用程式部署到 Azure 中的 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/13/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2fb7ab906208a58c0b5cd3af8b53188fbab94029
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2017
---
# <a name="deploy-an-application-with-cicd-to-a-service-fabric-cluster"></a>將搭配 CI/CD 的應用程式部署到 Service Fabric 叢集
本教學課程是系列中的第三部分，說明如何使用 Visual Studio Team Services (VSTS) 設定 Azure Service Fabric 應用程式的持續整合和部署。  需要現有的 Service Fabric 應用程式，在[建置 .NET 應用程式](service-fabric-tutorial-create-dotnet-app.md)中建立的應用程式將做為範例。

在系列的第三部分中，您將了解如何：

> [!div class="checklist"]
> * 將原始檔控制新增至專案
> * 在 Team Services 中建立組建定義
> * 在 Team Services 中建立發行定義
> * 自動部署和升級應用程式

在本教學課程系列中，您將了解如何：
> [!div class="checklist"]
> * [建置 .NET Service Fabric 應用程式](service-fabric-tutorial-create-dotnet-app.md)
> * [將應用程式部署到遠端叢集](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * 使用 Visual Studio Team Services 設定 CI/CD
> * [設定應用程式的監視和診斷](service-fabric-tutorial-monitoring-aspnet.md)

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前：
- 如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [安裝 Visual Studio 2017](https://www.visualstudio.com/) 並安裝 **Azure 開發**以及 **ASP.NET 和 Web 開發**工作負載。
- [安裝 Service Fabric SDK](service-fabric-get-started.md)
- 在 Azure 上建立 Windows Service Fabric 叢集，例如[遵循本教學課程](service-fabric-tutorial-create-vnet-and-windows-cluster.md)
- 建立 [Team Services 帳戶](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)。

## <a name="download-the-voting-sample-application"></a>下載投票應用程式範例
如果您未在[本教學課程系列的第一部分](service-fabric-tutorial-create-dotnet-app.md)中建置投票應用程式範例，可以下載它。 在命令視窗中執行下列命令，將範例應用程式存放庫複製到本機電腦。

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>下載發行設定檔
您現在已經[建立應用程式](service-fabric-tutorial-create-dotnet-app.md)，而且已經[將應用程式部署到 Azure](service-fabric-tutorial-deploy-app-to-party-cluster.md)，可以準備設定持續整合。  首先，在應用程式中準備部署程序使用的發行設定檔 (於 Team Services 內執行)。  發行設定檔應設定為以先前建立的叢集為目標。  啟動 Visual Studio，並開啟現有的 Service Fabric 應用程式專案。  在 [方案總管] 中，以滑鼠右鍵按一下應用程式並選取 [發佈...]。

在您的應用程式專案內選擇要使用於持續整合工作流程 (例如雲端) 的目標設定檔。  指定叢集連線端點。  勾選**升級應用程式**核取方塊，讓您的應用程式對於 Team Services 中的每個部署升級。  按一下 [儲存] 超連結，將設定儲存至發行設定檔，然後按一下 [取消] 關閉對話方塊。  

![推送設定檔][publish-app-profile]

## <a name="share-your-visual-studio-solution-to-a-new-team-services-git-repo"></a>向新的 Team Services Git 儲存機制共用 Visual Studio 解決方案
向 Team Services 中的小組專案共用應用程式原始檔，以便產生組建。  

Visual Studio 右上角的狀態列上，選取 [新增至原始檔控制] -> [Git]，建立專案的新本機 Git 儲存機制。 

在 [Team Explorer] 的 [推送] 檢視中，選取 [推送至 Visual Studio Team Services] 下的 [發佈 Git 儲存機制] 按鈕。

![推送 Git 儲存機制][push-git-repo]

確認您的電子郵件，並在 [Team Services 網域] 下拉式清單選取您的帳戶。 輸入您的儲存機制名稱，並選取 [發佈儲存機制]。

![推送 Git 儲存機制][publish-code]

發佈儲存機制將在您的帳戶中建立與本機儲存機制名稱相同的新 Team 專案。 若要在現有的 Team 專案中建立儲存機制，請按一下 [儲存機制] 名稱旁邊的 [進階]，並選取 Team 專案。 您可以選取**在網路上檢視**，在網路上檢視您的程式碼。

## <a name="configure-continuous-delivery-with-vsts"></a>設定 VSTS 的持續傳遞
Team Services 組建定義描述由一組循序執行的組建步驟所組成的工作流程。 建立產生 Service Fabric 應用程式封裝的組建定義，以及其他構件，以便部署到 Service Fabric 叢集。 深入了解 [Team Services 組建定義](https://www.visualstudio.com/docs/build/define/create)。 

Team Services 發行定義描述將應用程式封裝部署到叢集的工作流程。 一起使用時，組建定義和發行定義可以執行整個工作流程，從來源檔案開始，並以叢集中的執行中應用程式結束。 深入了解 Team Services [發行定義](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)。

### <a name="create-a-build-definition"></a>建立組建定義
開啟網頁瀏覽器並瀏覽至您在新的 team 專案： [https://&lt;myaccount&gt;.visualstudio.com/Voting/Voting%20Team/_git/Voting](https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting)。 

依序選取 [組建與發行] 索引標籤、[組建]，以及 [+ 新增定義]。  在 [選取範本] 中，選取 [Azure Service Fabric 應用程式] 範本，然後按一下 [套用]。 

![選擇組建範本][select-build-template] 

在**工作**，做為輸入 「 裝載 VS2017"**代理程式佇列**。 

![選取任務][save-and-queue]

在下**觸發程序**，藉此啟用連續整合**觸發狀態**。  選取**儲存並加入佇列**手動啟動組建。  

![選取觸發程序][save-and-queue2]

依據推入或簽入建置也觸發程序。 若要檢查組建進度，請切換到 [組建] 索引標籤。您確認組建執行成功，請定義將應用程式部署至叢集的發行定義。 

### <a name="create-a-release-definition"></a>建立發行定義  

依序選取 [組建與發行] 索引標籤、[版本]，以及 [+ 新增定義]。  在**選取範本**，選取**Azure Service Fabric 部署**從清單中的範本，然後**套用**。  

![選擇 發行範本][select-release-template]

選取**工作**->**環境 1**然後**+ 新增**加入新的叢集連接。

![新增叢集連線][add-cluster-connection]

在**加入新的服務網狀架構連接**檢視選取**憑證式**或**Azure Active Directory**驗證。  指定連接名稱"mysftestcluster"和"tcp://mysftestcluster.southcentralus.cloudapp.azure.com:19000"的叢集端點 （或您要部署到叢集的端點）。 

憑證式驗證，新增**伺服器憑證的指紋**用來建立叢集的伺服器憑證。  在**用戶端憑證**，新增用戶端憑證檔案的 base-64 編碼方式。 如需如何取得憑證的 base-64 編碼表示方式的資訊欄位，請參閱說明快顯視窗。 也新增**密碼**憑證。  如果您沒有個別的用戶端憑證，您可以使用叢集或伺服器憑證。 

Azure Active Directory 認證新增**伺服器憑證的指紋**您要用來連接到在叢集伺服器憑證用來建立叢集和認證的**的使用者名稱**和**密碼**欄位。 

按一下**新增**儲存叢集連線。

接下來，將組建成品新增至管線，讓發行定義可以找到建置的輸出。 選取**管線**和**成品**->**+ 加入**。  在**來源 （組建定義）**，選取您先前建立的組建定義。  按一下**新增**儲存組建成品。

![加入成品][add-artifact]

啟用連續部署觸發程序，以便在建置完成時，會自動建立發行。 按一下此成品的閃電圖示，啟用觸發程序，再按一下**儲存**儲存發行定義。

![啟用觸發程序][enable-trigger]

選取 [+ 發行] -> [建立發行] -> [建立] 可手動建立發行。  確認部署成功，而且應用程式在叢集中執行。  開啟網頁瀏覽器並瀏覽至[http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/Explorer/)。  請注意應用程式版本，在此範例中是「1.0.0.20170616.3」。 

## <a name="commit-and-push-changes-trigger-a-release"></a>認可並推送變更，觸發發行程序
簽入某些程式碼變更至 Team Services，確認持續整合管線正常運作。    

您撰寫程式碼時，Visual Studio 會自動追蹤您的變更。 認可本機 Git 儲存機制的變更，方法是從右下方的狀態列選取暫止變更圖示 (![Pending][pending])。

在 Team Explorer 的**變更**檢視中，加入描述更新的訊息，並認可變更。

![全部認可][changes]

選取 [未發行的變更] 狀態列圖示 (![未發行的變更][unpublished-changes]) 或 Team Explorer 中的 [同步] 檢視。 選取 [推送] 更新 Team Services/TFS 中的程式碼。

![推送變更][push]

自動將變更推送至 Team Services 觸發組建。  組建定義成功完成時，發行就會自動建立，並開始升級叢集上的應用程式。

若要檢查組建進度，請切換到 **Team Explorer** Visual Studio 中的 [組建] 索引標籤。  您確認組建執行成功，請定義將應用程式部署至叢集的發行定義。

確認部署成功，而且應用程式在叢集中執行。  開啟網頁瀏覽器並瀏覽至[http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/總管/](http://mysftestcluster.southcentralus.cloudapp.azure.com:19080/Explorer/)。  請注意應用程式版本，在此範例中是 "1.0.0.20170815.3"。

![Service Fabric Explorer][sfx1]

## <a name="update-the-application"></a>更新應用程式
在應用程式中進行程式碼變更。  在先前的步驟儲存並認可變更。

應用程式的升級開始後，即可注意 Service Fabric Explorer 中的升級進度：

![Service Fabric Explorer][sfx2]

應用程式升級可能需要幾分鐘的時間。 升級完成時，應用程式將執行下一個版本。  在此範例中為 "1.0.0.20170815.4"。

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 將原始檔控制新增至專案
> * 建立組建定義
> * 建立發行定義
> * 自動部署和升級應用程式

前進到下一個教學課程：
> [!div class="nextstepaction"]
> [設定應用程式的監視和診斷](service-fabric-tutorial-monitoring-aspnet.md) 


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[save-and-queue]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SaveAndQueue.png
[save-and-queue2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SaveAndQueue2.png
[select-release-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectReleaseTemplate.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[add-artifact]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddArtifact.png
[enable-trigger]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/EnableTrigger.png
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
