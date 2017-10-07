---
title: "aaaCreate 您第一次在 Azure 中的 Java web 應用程式"
description: "了解如何 toorun web 部署基本的 Java 應用程式的 App Service 中的應用程式。"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>在 Azure 中建立第一個 Java Web 應用程式

hello [Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)功能[Azure App Service](../app-service/app-service-value-prop-what-is.md)提供可高度擴充、 自我修補 web 主控服務。 本快速入門示範 toodeploy Java web 應用程式 tooApp 服務使用 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/)。

!["Hello Azure!" 範例 web 應用程式](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>必要條件

toocomplete 本快速入門中，安裝：

* 可用的 hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)。 本快速入門使用 Eclipse Neon。
* hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation)。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>在 Eclipse 中建立動態 Web 專案

在 Eclipse 中，選取 [檔案] > [新增] > [Dynamic Web Project]。

在 hello**新動態 Web 專案**對話方塊中，名稱 hello 專案**MyFirstJavaOnAzureWebApp**，然後選取**完成**。
   
![新增動態 Web 專案對話方塊](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>新增 JSP 頁面

如果未顯示 [專案總管]，請將它還原。

![適用於 Eclipse 的 Java EE 工作區](./media/app-service-web-get-started-java/pe.png)

在 專案總管 中，展開 hello **MyFirstJavaOnAzureWebApp**專案。
在 [WebContent] 上按一下滑鼠右鍵，然後選取 [新增] > [JSP 檔案]。

![專案總管中新 JSP 檔案的功能表](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

在 hello**新增 JSP 檔案**對話方塊：

* 名稱 hello 檔**index.jsp**。
* 選取 [完成]。

  ![[新增 JSP 檔案] 對話方塊](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

在 hello index.jsp 檔案，取代 hello `<body></body>` hello 下列標記的項目：

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

儲存 hello 的變更。

## <a name="publish-hello-web-app-tooazure"></a>發行 hello web 應用程式 tooAzure

在 專案總管 hello 專案中，以滑鼠右鍵按一下，然後選取**Azure** > **發佈 Azure Web 應用程式為**。

![[發佈為 Azure Web 應用程式] 內容功能表](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

在 hello **Azure 登入**對話方塊中，保留 hello**互動式**選項，然後再選取**登入**。

請遵循 hello 登入指示。

### <a name="deploy-web-app-dialog-box"></a>部署 Web 應用程式對話方塊

您登入 tooyour Azure 帳戶之後，hello**部署 Web 應用程式** 對話方塊隨即出現。

選取 [ **建立**]。

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>建立 App Service 對話方塊

hello**建立 App Service**對話方塊會顯示預設值。 hello 數目**170602185241**示 hello 下列映像在對話方塊中會不同。

![建立 App Service 對話方塊](./media/app-service-web-get-started-java/cas1.png)

在 hello**建立 App Service**對話方塊：

* 保留產生 hello hello web 應用程式的名稱。 此名稱在整個 Azure 中必須是唯一的。 hello 名稱是 hello hello web 應用程式的 URL 位址的一部分。 例如： 如果 hello web 應用程式名稱是**MyJavaWebApp**，URL 是的 hello *myjavawebapp.azurewebsites.net*。
* 保留 hello 預設網站容器。
* 選取 Azure 訂用帳戶。
* 在 [hello**應用程式服務方案**] 索引標籤：

  * **建立新**： 保留 hello 預設值，這是 hello hello App Service 方案名稱。
  * **位置**︰選取 [西歐]，或您附近的區域。
  * **定價層**： 選取 hello 可用的選項。 如需詳細資訊，請參閱 [App Service 價格](https://azure.microsoft.com/pricing/details/app-service/)。

   ![建立 App Service 對話方塊](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>資源群組索引標籤

選取 hello**資源群組** 索引標籤。保留 hello 資源群組的 hello 產生的預設值。

![資源群組索引標籤](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

選取 [ **建立**]。

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

hello Azure Toolkit 建立 hello web 應用程式，並顯示進度對話方塊。

![建立 App Service 進度對話方塊](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>部署 Web 應用程式對話方塊

在 hello**部署 Web 應用程式**對話方塊中，選取**部署 tooroot**。 如果您有應用程式服務在*wingtiptoys.azurewebsites.net*和您不應部署 toohello 根，hello web 應用程式名為**MyFirstJavaOnAzureWebApp**太部署*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*。

![部署 Web 應用程式對話方塊](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

hello 對話方塊所示 hello Azure、 JDK 和 web 容器選取項目。

選取**部署**toopublish hello web 應用程式 tooAzure。

Hello 發行完成時，選取 hello**發佈**hello 中的連結**Azure 活動記錄檔** 對話方塊。

![Azure 活動記錄對話方塊](./media/app-service-web-get-started-java/aal.png)

恭喜！ 您已成功部署您的 web 應用程式 tooAzure。 

!["Hello Azure!" 範例 web 應用程式](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>更新 hello web 應用程式

變更 hello 範例 JSP 程式碼 tooa 不同的訊息。

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

儲存 hello 的變更。

在 專案總管 hello 專案中，以滑鼠右鍵按一下，然後選取**Azure** > **發佈 Azure Web 應用程式為**。

hello**部署 Web 應用程式**對話方塊隨即出現並顯示 hello 您先前建立的應用程式服務。 

> [!NOTE]
> 選取**部署 tooroot**每次發佈。
>

選取 hello web 應用程式，然後選取**部署**，將發佈 hello 變更。

當 hello**發行**連結出現時，請選取它 toobrowse toohello web 應用程式看到 hello 的變更。

## <a name="manage-hello-web-app"></a>管理 hello web 應用程式

移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toosee hello web 應用程式所建立。

從 hello 左窗格中，選取**資源群組**。

![入口網站瀏覽 tooresource 群組](media/app-service-web-get-started-java/rg.png)

選取 hello 資源群組。 hello 頁面會顯示您在本快速入門中建立的 hello 資源。

![資源群組 myResourceGroup](media/app-service-web-get-started-java/rg2.png)

選取 hello web 應用程式 (**webapp 170602193915**在上述映像的 hello)。

hello**概觀**頁面隨即出現。 此頁面可讓您檢視 hello 應用程式執行的動作。 您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 hello 上 hello hello 頁面左側的索引標籤會顯示 hello 不同的組態，您可以開啟。 

![Azure 入口網站中的 App Service 頁面](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [對應自訂網域](app-service-web-tutorial-custom-domain.md)
