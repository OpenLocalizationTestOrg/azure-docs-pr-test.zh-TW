---
title: "aaaCreate 基本 Azure web 應用程式使用的 Eclipse |Microsoft 文件"
description: "本教學課程會示範如何 toouse hello Azure Toolkit for Eclipse toocreate Azure Hello World 網頁應用程式。"
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>使用 Eclipse 建立基本的 Azure Web 應用程式
本教學課程示範如何 toocreate 並將基本的 Hello World 應用程式 tooAzure 部署為 Web 應用程式中，使用 hello [Azure Toolkit for Eclipse]。 以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。

當您完成本教學課程時，您的應用程式看起來類似 toohello 您網頁瀏覽器中檢視時，下列實例：

![Hello World 應用程式預覽][01]

## <a name="prerequisites"></a>必要條件
* Java Developer Kit (JDK) 1.8 版或更新版本。
* Eclipse IDE for Java EE Developers (Luna 或更新版本)。 這可透過 <http://www.eclipse.org/downloads/> 下載。
* Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。
* Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。
* hello [Azure Toolkit for Eclipse]。 如需安裝 Azure Toolkit hello 資訊，請參閱[安裝 hello Azure Toolkit for Eclipse]。

## <a name="toocreate-a-hello-world-application"></a>toocreate Hello World 應用程式
首先，我們將從建立 Java 專案開始。

1. 啟動 Eclipse 中，並在 hello 功能表按一下**檔案**，按一下 **新增**，然後按一下**動態 Web 專案**。 (如果您沒有看到**動態 Web 專案**列為可用的專案，按一下後**檔案**和**新增**，請勿然後 hello 遵循： 按一下**檔案**，按一下 **新增**，按一下 **專案...**，依序展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。)
2. 本教學課程的目的而言，專案的名稱，hello **MyWebApp**。 您的畫面會出現類似 toohello 下列：
   
    ![建立新的動態 Web 專案][02]
3. 按一下 [完成] 。
4. 在 Eclipse 的 [專案總管] 檢視中，展開 [MyWebApp]。 在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。
5. 在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**，保留 hello 父資料夾為**MyWebApp/WebContent**，然後按一下**下一步**.
6. 在 hello**選取 JSP 範本**對話方塊中的，基於這個教學課程，請選取**新增 JSP 檔案 (html)**，然後按一下**完成**。
7. 當 Eclipse 中開啟 index.jsp 檔案時，加入在文字 toodynamically 顯示**Hello World ！** 在現有的 hello`<body>`項目。 您已更新`<body>`內容應該類似下列範例中的 hello:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. 儲存 index.jsp。

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy 您應用程式 tooan Azure Web 應用程式容器
有幾種的方式可以部署 Java web 應用程式 tooAzure。 本教學課程說明 hello 最簡單的其中一個： 您的應用程式將會部署的 tooan Azure Web 應用程式的容器-沒有特殊專案類型和其他工具所需。 hello JDK 和 hello web 容器軟體將會提供給您的 Azure 中，所以不需要 tooupload 自己;您只需要為您的 Java Web 應用程式。 如此一來，hello 發行程序，您的應用程式需要秒，不是分鐘。

1. 在 Eclipse 的專案總管中，以滑鼠右鍵按一下 [MyWebApp] 。
2. 在 hello 內容功能表選取**Azure**，然後按一下 **發行為 Azure Web 應用程式...**
   
    ![發佈為 Azure Web 應用程式][03]
   
    或者，在 hello [專案總管] 中選取您的 web 應用程式專案時，您可以按一下 hello**發行**hello 工具列，然後選取的下拉式按鈕**發佈 Azure Web 應用程式為**從該處：
   
    ![發佈為 Azure Web 應用程式][14]
3. 如果您有沒有登入 Azure 從 Eclipse，您將會提示的 toosign 到您的 Azure 帳戶：
   
    ![[Azure 登入] 對話方塊][04]
   
    如果您有多個 Azure 帳戶，一些期間 hello hello 提示登入程序可能會顯示一次以上，即使看起來 toobe hello 相同。 當發生這種情況時，繼續遵循 hello 登入指示。
4. 您已成功登入您的 Azure 帳戶之後，hello**管理訂用帳戶**對話方塊會顯示您的認證與相關聯的訂用帳戶的清單。 如果有多個列出的訂閱，而且您想 toowork 特定子集合的它們，您可能會選擇性地取消核取 hello 想 toouse 的。 當您選取訂用帳戶之後，按一下 [關閉] 。
   
    ![[管理訂用帳戶] 對話方塊][05]
5. 當 hello**部署 Web 應用程式容器 tooAzure**  對話方塊隨即出現，它會顯示您先前已經建立任何 Web 應用程式容器; 如果您尚未建立任何容器，hello 清單將會是空的。
   
    ![部署 tooAzure Web 應用程式容器 對話方塊][06]
6. 如果您尚未建立 Azure Web 應用程式容器之前，或如果您想要 toopublish 應用程式 tooa 的新容器，，使用下列步驟的 hello。 否則，請選取現有的 Web 應用程式容器，並略過 toostep 7。
   
   1. 按一下 [完成] 
      
       ![部署 tooAzure Web 應用程式容器 對話方塊][15]
   2. hello**新的 Web 應用程式容器**對話方塊會顯示：
      
       ![[新增 Web 應用程式容器] 對話方塊][07a]
   3. 輸入**DNS 標籤**Web 應用程式容器; 這將會形成 hello 分葉 DNS 標籤 hello 主機 URL，web 應用程式在 Azure 中。 （請注意該 hello 名稱必須可供使用且符合 tooAzure Web 應用程式命名需求）。
   4. 在 hello**網頁容器**下拉式功能表、 選取 hello 適當的軟體應用程式。
      
       目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。 最近的 hello 選取軟體發佈將會由 Azure 中，提供，且可以在建立 Oracle 和 Azure 所提供的 JDK 8 最近發佈。
   5. 在 hello**訂用帳戶**下拉式選單中，您想要此部署 toouse 選取 hello 訂用帳戶。
   6. 在 hello**資源群組**下拉式功能表，選取 hello 與您想 tooassociate 您 Web 應用程式的資源群組。 （azure 資源群組允許您 toogroup 相關資源在一起，以便將，比方說，您可以先刪除這些一起）。
      
       （如果有），您可以選取現有的資源群組，並略過 toostep g 以下或使用 hello 遵循這些步驟 toocreate 新的資源群組：
      
      * 按一下 [完成] 
      * hello**新資源群組**對話方塊會顯示：
        
          ![[新增資源群組] 對話方塊][08]
      * 在 hello hello**名稱**文字方塊中，指定新的資源群組的名稱。
      * 在 hello hello**區域**下拉式選單選取 hello 適當的 Azure 資料中心資源群組的位置。
      * 選擇性： 根據預設，新的 Java 8 分配會部署 Azure 自動為您的 JVM tooyour web 應用程式的容器。 不過，您可以指定不同的版本和發佈的 hello JVM 如果 Web 應用程式需要它。 toospecify hello JDK 您 Web 應用程式中，按一下 hello **JDK**索引標籤，然後選取其中一個 hello 下列選項：
        
        * **部署 hello 預設 Azure Web 應用程式服務所提供的 JDK**： 此選項會將 Java 8 最近發佈的部署。
        * **部署第 3 個合作對象在 Azure 上可用的 JDK**： 此選項可讓您從 Microsoft Azure 所提供的 Jdk hello 清單 toochoose。
        * **部署我自己的 JDK，從這個下載位置**： 此選項可讓您 toospecify 自己 JDK 散發，這必須為 ZIP 檔案封裝並上傳的 tooeither 公開可用的下載位置或 Azure 儲存體帳戶，您存取權。
          
          ![[新增 Web 應用程式容器] 對話方塊][07b]
   7. 按一下 [確定] 。
   8. hello **App Service 方案**下拉式功能表列出 hello 與 hello 您選取的資源群組相關聯的應用程式服務方案。 （應用程式服務計劃指定 Web 應用程式，hello 定價層和 hello 運算執行個體大小的 hello 位置等資訊。 單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)
      
       您可以選取現有的 App Service 方案 （如果有），並略過 toostep h，或使用下列這些新的 App Service 方案的步驟 toocreate hello:
      
      * 按一下 [完成] 
      * hello**新應用程式服務方案**對話方塊會顯示：
        
          ![[新增 App Service 方案] 對話方塊][09]
      * 在 hello hello**名稱**文字方塊中，指定您新的 App Service 方案的名稱。
      * 在 hello hello**位置**下拉式選單選取 hello 適當的 Azure 資料中心 hello 計劃的位置。
      * 在 hello hello**定價層**下拉式功能表，選取 hello 適當定價 hello 計劃。 針對測試用途，您可以選擇 [免費] 。
      * 在 hello hello**執行個體大小**下拉式功能表、 選取 hello hello 計劃的適當的執行個體大小。 針對測試用途，您可以選擇 [小型] 。
   9. 當您完成所有 hello 上述步驟時，hello 新的 Web 應用程式容器 對話方塊應該類似下列圖中的 hello:
      
       ![[新增 Web 應用程式容器] 對話方塊][10]
   10. 按一下**確定**toocomplete hello 建立新的 Web 應用程式容器。
       
        等候數秒鐘，讓 hello Web 應用程式容器 toobe hello 清單重新整理，現在應 hello 清單中選取您新建立的 web 應用程式的容器。
7. 現在您已經準備就緒 toocomplete hello 初始部署 Web 應用程式 tooAzure:
   
    ![部署 tooAzure Web 應用程式容器 對話方塊][11]
   
    按一下**確定**toodeploy 您的 Java 應用程式 toohello 選取 Web 應用程式的容器。
   
    根據預設，您的應用程式將會部署為 hello 應用程式伺服器的子目錄。 如果您想 toobe 部署為 hello 根應用程式，請檢查 hello**部署 tooroot**核取方塊後，再按一下**確定**。
8. 接下來，您應該會看見 hello **Azure 活動記錄檔**檢視，其中將指出 hello Web 應用程式的部署狀態。
   
    ![Azure 活動記錄檔][12]
   
    部署 Web 應用程式 tooAzure 的 hello 程序應該採取只有幾秒鐘 toocomplete。 當您的應用程式已備妥，您會看到名為的連結**發佈**在 hello**狀態**資料行。 當您按一下 hello 連結時，它會帶您 tooyour 部署 Web 應用程式的首頁。

## <a name="updating-your-web-app"></a>更新 Web 應用程式
更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：

* 您可以更新 hello 部署現有的 Java Web 應用程式。
* 您可以將額外的 Java 應用程式 toohello 發行相同的 Web 應用程式容器。

在任一情況下，hello 程序相同，並需要只有幾秒鐘的時間：

1. Hello Eclipse [專案總管] 中以滑鼠右鍵按一下您想要 tooupdate 或加入現有的 Web 應用程式容器 tooan 的 hello Java 應用程式。
2. Hello 操作功能表出現時，選取**Azure**然後**發行為 Azure Web 應用程式...**
3. 由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。 選取 hello 一您想要 toopublish 或重新發佈您的 Java 應用程式 tooand 按一下**確定**。

在幾秒鐘後，hello **Azure 活動記錄檔**檢視會顯示為您更新的部署**已發佈**而且您將會無法 tooverify 網頁瀏覽器應用程式更新。

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>啟動、停止或重新啟動現有的 Web 應用程式
toostart 或停止現有的 Azure Web 應用程式容器，（包括所有部署的 hello Java 應用程式中），您可以使用 hello **Azure 總管**檢視。

如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**視窗**功能表在 Eclipse 中，然後按一下**顯示檢視**，然後**其他...**，然後**Azure**，然後按一下 **Azure 總管**。 如果您先前尚未登入，則會提示您 toodo 因此。

當 hello **Azure 總管**檢視隨即顯示，請遵循這些步驟 toostart 使用，或停止 Web 應用程式： 

1. 展開 hello **Azure**節點。
2. 展開 hello **Web 應用程式**節點。 
3. 以滑鼠右鍵按一下 hello 所需的 Web 應用程式。
4. Hello 操作功能表出現時，按一下**啟動**，**停止**，或**重新啟動**。 請注意，hello 功能表選項內容感知，所以您只可以停止正在執行的 web 應用程式或啟動 web 應用程式目前未執行的。
   
    ![停止現有的 Web 應用程式][13]

## <a name="next-steps"></a>後續步驟
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:

* [Azure Toolkit for Eclipse]
  * [安裝 hello Azure Toolkit for Eclipse]
  * *在 Eclipse 中建立 Azure Hello World Web 應用程式 (本文)*
  * [功能 hello Azure Toolkit for Eclipse 中的新功能]
* [Azure Toolkit for IntelliJ]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]
  * [新功能 hello Azure Toolkit for IntelliJ]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。

如需有關建立 Azure Web 應用程式的詳細資訊，請參閱 hello [Web 應用程式的概觀]。

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web-intellij-create-hello-world-web-app.md
[安裝 hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ../azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Web 應用程式的概觀]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
