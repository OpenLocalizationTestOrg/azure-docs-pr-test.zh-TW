---
title: "aaaDeploy Azure Service Fabric 應用程式 tooa 合作對象叢集 |Microsoft 文件"
description: "深入了解如何 toodeploy 應用程式 tooa 合作對象叢集。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>部署應用程式 tooa Azure 中的合作對象叢集
本教學課程是兩個一系列的一部分，並為您示範如何在 Azure 中的合作對象叢集 Azure Service Fabric 應用程式 tooa toodeploy。

在 hello 教學課程系列的第二個部分，您將學習如何：
> [!div class="checklist"]
> * 部署使用 Visual Studio 應用程式的 tooa 遠端叢集
> * 使用 Service Fabric Explorer 從叢集移除應用程式

在本教學課程系列中，您將了解如何：
> [!div class="checklist"]
> * [建置 .NET Service Fabric 應用程式](service-fabric-tutorial-create-dotnet-app.md)
> * 部署 hello 應用程式 tooa 遠端叢集
> * [使用 Visual Studio Team Services 設定 CI/CD](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前：
- 如果您沒有 Azure 訂用帳戶，請建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [安裝 Visual Studio 2017](https://www.visualstudio.com/)並安裝 hello **Azure 開發**和**ASP.NET 及 web 開發**工作負載。
- [安裝 hello Service Fabric SDK](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>下載 hello 投票範例應用程式
如果您未建立 hello 投票範例應用程式[第一部此教學課程系列的](service-fabric-tutorial-create-dotnet-app.md)，您可以下載它。 在命令視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>設定合作對象叢集
合作對象的叢集是免費的限時 Service Fabric 叢集裝載於 Azure，並執行 hello Service Fabric 小組的任何人都可以在此部署的應用程式，並了解 hello 平台。 免費！

tooget 存取 tooa 合作對象叢集中，瀏覽 toothis 網站： http://aka.ms/tryservicefabric 然後遵循 hello 指示 tooget 存取 tooa 叢集。 您需要 Facebook 或 GitHub 帳戶 tooget 存取 tooa 合作對象叢集。

> [!NOTE]
> 合作對象叢集也不安全，因此應用程式，且您將放在它們的任何資料可能會看見 tooothers。 不會部署任何您不希望其他人 toosee。 確定 tooread 透過我們的使用規定的所有 hello 詳細資料。

## <a name="configure-hello-listening-port"></a>設定 hello 接聽連接埠
建立 hello VotingWeb 前端服務時，Visual Studio 會隨機選擇 hello 服務 toolisten 的連接埠上。  hello VotingWeb 服務做為此應用程式前端的 hello 和接受外部流量，因此讓我們先繫結修正該服務 tooa 並也知道連接埠。 在 [方案總管] 中，開啟 VotingWeb/PackageRoot/ServiceManifest.xml。  尋找 hello**端點**hello 中的資源**資源**區段，並變更 hello**連接埠**值 too80。

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

讓網頁瀏覽器開啟 toohello 正確的連接埠，當您偵錯使用 'F5' 時，也更新 hello 投票專案中的 hello 應用程式 URL 屬性值。  在 方案總管 中，選取 hello**投票**專案和更新的 hello**應用程式 URL**屬性。

![應用程式 URL](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>部署 hello 應用程式 toohello Azure
現在已準備好 hello 應用程式，您可以部署它 toohello 直接從 Visual Studio 的合作對象叢集。

1. 以滑鼠右鍵按一下**投票**hello 中的 方案總管，然後選擇 **發行**。

    ![[發佈] 對話方塊](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. 輸入 hello 連接端點之 hello 合作對象叢集在 hello**連接端點**欄位，然後按一下**發行**。

    一旦 hello 發佈已完成之後，您應該要能夠 toosend 透過瀏覽器要求 toohello 應用程式。

3. 開啟您偏好的瀏覽器然後輸入 hello 叢集位址 （不含 hello 連接埠資訊，例如 win1kw5649s.westus.cloudapp.azure.com hello 連接端點）。

    您現在應該會看到結果如同在本機執行 hello 應用程式時相同的 hello。

    ![叢集的 API 回應](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>使用 Service Fabric 總管叢集中移除 hello 應用程式
Service Fabric 總管是圖形化使用者介面 tooexplore 和管理 Service Fabric 叢集中的應用程式。

從合作對象叢集 hello tooremove hello 應用程式：

1. 瀏覽 toohello Service Fabric 總管 中，使用 hello hello 合作對象叢集註冊頁面所提供的連結。 例如，http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html。

2. 在 Service Fabric 總管，瀏覽 toohello **fabric://Voting** hello 上 hello 左側的樹狀檢視中的節點。

3. 按一下 hello**動作**按鈕在右手邊的 hello **Essentials** ] 窗格中，選擇 [**刪除應用程式**。 確認刪除 hello 應用程式執行個體，代表要移除 hello 我們 hello 叢集中執行的應用程式執行個體。

![刪除 Service Fabric Explorer 中的應用程式](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>使用 Service Fabric 總管叢集中移除 hello 應用程式類型
應用程式會部署為在多個執行個體和 hello hello 叢集內執行的應用程式的版本，可讓您 toohave Service Fabric 叢集中的應用程式類型。 之後移除 hello 執行我們的應用程式的執行個體之後，我們也可以移除 hello toocomplete hello 清除 hello 部署的型別。

如需服務網狀架構中的 hello 應用程式模型的詳細資訊，請參閱[模型的應用程式在 Service Fabric](service-fabric-application-model.md)。

1. 瀏覽 toohello **VotingType** hello 樹狀檢視中的節點。

2. 按一下 hello**動作**按鈕在右手邊的 hello **Essentials** ] 窗格中，選擇 [**解除佈建類型**。 確認解除佈建 hello 應用程式類型。

![在 Service Fabric Explorer 中解除佈建應用程式類型](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

以上總結 hello 教學課程。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 部署使用 Visual Studio 應用程式的 tooa 遠端叢集
> * 使用 Service Fabric Explorer 從叢集移除應用程式

進階 toohello 下一個教學課程：
> [!div class="nextstepaction"]
> [使用 Visual Studio Team Services 設定持續整合](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)