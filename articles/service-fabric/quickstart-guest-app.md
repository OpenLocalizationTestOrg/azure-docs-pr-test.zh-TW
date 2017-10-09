---
title: "aaaQuickly 部署現有的應用程式 tooan Azure Service Fabric 叢集"
description: "使用 Azure Service Fabric 叢集 toohost 現有 Node.js 應用程式與 Visual Studio。"
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>在 Azure Service Fabric 上裝載 Node.js 應用程式

本快速入門可協助您部署在 Azure 上執行的現有應用程式 (在此範例中的 Node.js) tooa Service Fabric 叢集。

## <a name="prerequisites"></a>必要條件

開始之前，請確定您已 [設定開發環境](service-fabric-get-started.md)。 這包括安裝 hello Service Fabric SDK 及 Visual Studio 2017 或 2015年。

您也需要 toohave 現有 Node.js 應用程式部署。 本快速入門使用可在[這裡][download-sample]下載的簡單 Node.js 網站。 擷取這個檔案 tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` hello 下一個步驟中建立 hello 專案之後的資料夾。

如果您沒有 Azure 訂用帳戶，請建立[免費帳戶][create-account]。

## <a name="create-hello-service"></a>建立 hello 服務

以**系統管理員**身分啟動 Visual Studio。

使用 `CTRL`+`SHIFT`+`N` 建立專案

在 [hello**新專案**] 對話方塊中，選擇**雲端 > Service Fabric 應用程式**。

Hello 應用程式命名**MyGuestApp**按**確定**。

>[!IMPORTANT]
>Node.js 可以輕易地中斷 hello 260 字元限制為 windows 提供的路徑。 Hello 專案本身使用短路徑，例如**c:\code\svc1**。
   
![Visual Studio 中的新增專案對話方塊][new-project]

您可以從 hello 下一步 對話方塊建立 Service Fabric 服務的任何型別。 在本快速入門中，選擇 [來賓可執行檔]。

Hello 服務名稱**MyGuestService**和 set hello 選項上 hello 右 toohello 下列值：

| 設定                   | 值 |
| ------------------------- | ------ |
| 程式碼封裝資料夾       | _&lt;Node.js 應用程式的 hello 資料夾&gt;_ |
| 程式碼封裝行為     | 複製資料夾內容 tooproject |
| 程式                   | node.exe |
| 引數                 | server.js |
| 工作資料夾            | CodePackage |

按 [確定]。

![Visual Studio 中的新增服務對話方塊][new-service]

Visual Studio 會建立 hello 應用程式專案和 hello 行動服務專案，並顯示在 [方案總管] 中。

hello 應用程式專案 (**MyGuestApp**) 直接不包含任何程式碼。 它反而會參考一組服務專案。 此外，它包含三種其他類型的內容：

* **發佈設定檔**  
用來管理不同環境的工具喜好設定。

* **指令碼**  
包含用來部署/升級應用程式的 PowerShell 指令碼。

* **應用程式定義**  
包含在 hello 應用程式資訊清單*ApplicationPackageRoot*。 相關聯的應用程式參數檔案受到*ApplicationParameters*，其中定義 hello 應用程式並可讓您 tooconfigure 它專為特定環境。
    
如需 hello hello 服務專案內容的概觀，請參閱[可靠的服務入門](service-fabric-reliable-services-quick-start.md)。

## <a name="set-up-networking"></a>設定網路

我們要部署 Node.js 應用程式會使用連接埠的 hello 範例**80** ，我們需要 tootell Service Fabric 需要公開連接埠。

開啟 hello **ServiceManifest.xml** hello 專案中的檔案。 Hello hello 資訊清單底部，在沒有`<Resources> \ <Endpoints>`利用已定義的項目。 修改的項目 tooadd `Port`， `Protocol`，和`Type`。 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>部署 tooAzure

如果您按下**F5**和執行 hello 專案，它是已部署的 toohello 本機叢集。 不過，讓我們 tooAzure 改為部署。

Hello 專案上按一下滑鼠右鍵，然後選擇 **發行...**以開啟對話方塊 toopublish tooAzure。

![發行 service fabric 服務的 tooazure 對話方塊][publish]

選取 hello **PublishProfiles\Cloud.xml** profile 當做目標。

如果您還沒有做之前，選擇要 Azure 帳戶 toodeploy。 如果您沒有 Azure 帳戶，請[註冊一個][create-account]。

在下**連接端點**，選取 hello 到 Service Fabric 叢集 toodeploy。 如果您沒有其中一個，選取**&lt;建立新的叢集...&gt;** 這會開啟網頁瀏覽器視窗 toohello Azure 入口網站。 如需詳細資訊，請參閱[hello 入口網站中建立叢集](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal)。 

當您建立 hello Service Fabric 叢集時，請確定 tooset hello**自訂端點**太設定**80**。

![自訂端點的 Service fabric 節點類型組態][custom-endpoint]

建立新的 Service Fabric 叢集需要花一些時間 toocomplete。 已建立，移至上一頁 toohello 發行對話方塊，並選取**&lt;重新整理&gt;**。 hello 新叢集會列在 [hello] 下拉式清單方塊中。請選取它。

按**發行**並等候 hello 部署 toofinish。

這可能需要幾分鐘的時間。 完成之後，可能需要數分鐘的 hello 應用程式 toobe 完全可供使用。

## <a name="test-hello-website"></a>測試 hello 網站

在服務發佈之後，請在網頁瀏覽器中進行測試。 

首先，開啟 hello Azure 入口網站，並尋找您的 Service Fabric 服務。

請檢查 hello 概觀刀鋒視窗中的 hello 服務位址。 使用 hello 的網域名稱，從 hello_用戶端連接端點_屬性。 例如： `http://mysvcfab1.westus2.cloudapp.azure.com`。

![服務網狀架構概觀刀鋒視窗上 hello Azure 入口網站][overview]

瀏覽 toothis 位址就可看到 hello`HELLO WORLD`回應。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

不要忘記的 toodelete 所有您為本快速入門，為您所建立的 hello 資源會針對這些資源的收費。

## <a name="next-steps"></a>後續步驟
深入了解[客體可執行檔](service-fabric-deploy-existing-app.md)。

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F