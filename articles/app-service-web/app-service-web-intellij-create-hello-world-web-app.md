---
title: "aaaCreate 基本 Azure web 應用程式中 IntelliJ |Microsoft 文件"
description: "本教學課程會示範如何 toouse hello Azure Toolkit for IntelliJ toocreate Azure Hello World 網頁應用程式。"
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>在 IntelliJ 中建立基本的 Azure Web 應用程式
本教學課程示範如何 toocreate 並將基本的 Hello World 應用程式 tooAzure 部署為 Web 應用程式中，使用 hello [Azure Toolkit for IntelliJ]。 以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。

當您完成本教學課程時，您的應用程式看起來類似 toohello 您網頁瀏覽器中檢視時，下列實例：

![範例網頁][01]

## <a name="prerequisites"></a>必要條件
* Java Developer Kit (JDK) 1.8 版或更新版本。
* IntelliJ 概念旗艦版。 可以從 <https://www.jetbrains.com/idea/download/index.html> 下載。
* Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。
* Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。
* hello [Azure Toolkit for IntelliJ]。 如需安裝 Azure Toolkit hello 資訊，請參閱[安裝 hello Azure Toolkit for IntelliJ]。

## <a name="toocreate-a-hello-world-application"></a>toocreate Hello World 應用程式
首先，我們將從建立 Java 專案開始。

1. 啟動 IntelliJ，然後按一下 hello**檔案**功能表，然後按一下**新增**，然後按一下**專案**。
   
    ![專案 > 新增專案][02]
2. 在 hello 新增專案 對話方塊中，選取  **Java**，然後**Web 應用程式**，然後按一下**新增**tooadd 專案 SDK。
   
    ![New Project Dialog][03a]
   
3. JDK 對話方塊 hello 選擇主目錄中選取 hello JDK 安裝所在的資料夾，然後按一下**確定**。 按一下**下一步**hello 新增專案對話方塊方塊 toocontinue 中。
   
    ![指定 JDK 主目錄][03b]
4. 本教學課程的目的而言，專案的名稱，hello **Java Web 層應用程式層上-Azure**，然後按一下**完成**。
   
    ![New Project Dialog][04]
5. 在 IntelliJ 的 [專案總管] 檢視中，依序展開 [Java-Web-App-On-Azure] 和 [web]，然後按兩下 [index.jsp]。
   
    ![開啟索引頁面][05c]
6. 當 IntelliJ 開啟 index.jsp 檔案時，加入在文字 toodynamically 顯示**Hello World ！** 在現有的 hello`<body>`項目。 您已更新`<body>`內容應該類似下列範例中的 hello:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. 儲存 index.jsp。

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy 您應用程式 tooan Azure Web 應用程式容器
有幾種的方式可以部署 Java web 應用程式 tooAzure。 本教學課程說明 hello 最簡單的其中一個： 您的應用程式將會部署的 tooan Azure Web 應用程式的容器-沒有特殊專案類型和其他工具所需。 hello JDK 和 hello web 容器軟體將會提供給您的 Azure 中，所以不需要 tooupload 自己;您只需要為您的 Java Web 應用程式。 如此一來，hello 發行程序，您的應用程式需要秒，不是分鐘。

在發行您的應用程式之前，您必須先 tooconfigure 模組設定。 toodo 因此，使用下列步驟的 hello:

1. IntelliJ 的專案總管 中以滑鼠右鍵按一下 hello **Java Web 層應用程式層上-Azure**專案。 Hello 操作功能表出現時，按一下**開啟模組設定**。

    ![開啟模組設定][05a]
2. Hello 專案結構對話方塊出現時：

   a. 按一下**成品**hello 清單中**專案設定**。
   b. 在 hello 變更 hello 成品名稱**名稱**方塊，讓它不包含空格或特殊字元，這是必要的因為 hello 名稱將用於 hello 統一資源識別元 (URI)。
   c. 變更 hello**類型**太**Web 應用程式： 封存**。
   d. 按一下**確定**tooclose hello 專案結構對話方塊。

    ![開啟模組設定][05b]

當您完成設定您的模組設定時，您可以使用下列步驟的 hello 發行應用程式 tooAzure:

1. IntelliJ 的專案總管 中以滑鼠右鍵按一下 hello **Java Web 層應用程式層上-Azure**專案。 Hello 操作功能表出現時，選取**Azure**，然後按一下**發行為 Azure Web 應用程式...**
   
    ![Azure 發佈操作功能表][06]
2. 如果您有沒有登入從 IntelliJ Azure，您將會提示的 toosign 到您的 Azure 帳戶。 (如果您有多個 Azure 帳戶，一些 hello 提示 hello 登入程序期間可能會顯示一次以上，即使看起來 toobe hello 相同。 當發生這種情況，指示中繼續 toofollow hello 註冊）。
   
    ![Azure 登入對話方塊][07]
3. 您已成功登入您的 Azure 帳戶之後，hello**管理訂用帳戶**對話方塊會顯示您的認證與相關聯的訂用帳戶的清單。 （如果有多個列出的訂閱，而且您想 toowork 特定子集合的它們，您可能會選擇性地取消核取您不想 toouse hello 訂用帳戶。）當您選取訂用帳戶之後，按一下 [關閉] 。
   
    ![管理訂用帳戶][08]
4. 當 hello**部署 Web 應用程式容器 tooAzure**  對話方塊隨即出現，它會顯示您先前已經建立任何 Web 應用程式容器; 如果您尚未建立任何容器，hello 清單將會是空的。
   
    ![應用程式容器][09]
5. 如果您尚未建立 Azure Web 應用程式容器之前，或如果您想要 toopublish 應用程式 tooa 的新容器，，使用下列步驟的 hello。 否則，請選取現有的 Web 應用程式容器，並略過 toostep 6。
   
   1. 按一下 **+**
      
       ![新增應用程式容器][10]
   2. hello**新的 Web 應用程式容器**對話方塊將會顯示，它將會是用於 hello 接下來幾個步驟。
      
       ![新增應用程式容器][11a]
   3. 輸入**DNS 標籤**Web 應用程式容器; 這將會形成 hello 分葉 DNS 標籤 hello 主機 URL，web 應用程式在 Azure 中。 請注意該 hello 名稱必須可供使用且符合 tooAzure Web 應用程式命名需求。
   4. 在 hello**網頁容器**下拉式功能表、 選取 hello 適當的軟體應用程式。
      
       目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。 最近的 hello 選取軟體發佈將會由 Azure 中，提供，且可以在建立 Oracle 和 Azure 所提供的 JDK 8 最近發佈。
   5. 在 hello**訂用帳戶**下拉式選單中，您想要此部署 toouse 選取 hello 訂用帳戶。
   6. 在 hello**資源群組**下拉式功能表，選取 hello 與您想 tooassociate 您 Web 應用程式的資源群組。 （azure 資源群組允許您 toogroup 相關資源在一起，以便將，比方說，您可以先刪除這些一起）。
      
       （如果有），您可以選取現有的資源群組，並略過 toostep g 以下或使用 hello 下列步驟 toocreate 新的資源群組：
      
      * 選取 **&lt; &lt;建立新的資源群組&gt; &gt;** 在 hello**資源群組**下拉式功能表。
      * hello**新資源群組**對話方塊會顯示：
        
          ![新增資源群組][12]
      * 在 hello hello**名稱**文字方塊中，指定新的資源群組的名稱。
      * 在 hello hello**區域**下拉式選單選取 hello 適當的 Azure 資料中心資源群組的位置。
      * 按一下 [確定] 。
   7. hello **App Service 方案**下拉式功能表列出 hello 與 hello 您選取的資源群組相關聯的應用程式服務方案。 （App Service 方案指定 Web 應用程式，hello 定價層和 hello 運算執行個體大小的 hello 位置等資訊。 單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)
      
       您可以選取現有的 App Service 方案 （如果有），並略過 toostep h，或使用下列新的 App Service 方案的步驟 toocreate hello:
      
      * 選取 **&lt; &lt;建立新的應用程式服務計劃&gt; &gt;** 在 hello **App Service 方案**下拉式功能表。
      * hello**新應用程式服務方案**對話方塊會顯示：
        
          ![新增 App Service 方案][13]
      * 在 hello hello**名稱**文字方塊中，指定您新的 App Service 方案的名稱。
      * 在 hello hello**位置**下拉式選單選取 hello 適當的 Azure 資料中心 hello 計劃的位置。
      * 在 hello hello**定價層**下拉式功能表，選取 hello 適當定價 hello 計劃。 針對測試用途，您可以選擇 [免費] 。
      * 在 hello hello**執行個體大小**下拉式功能表、 選取 hello hello 計劃的適當的執行個體大小。 針對測試用途，您可以選擇 [小型] 。
      * 按一下 [確定] 。
   8. （選擇性）根據預設，Java 8 最近發佈將會自動部署為您的 JVM Azure tooyour web 應用程式容器所。 不過，您可以選取不同的版本和 hello JVM 的分佈。 toodo 因此，使用下列步驟的 hello:
      
      * 按一下 hello **JDK**  索引標籤中 hello**新的 Web 應用程式容器** 對話方塊。
      * 您可以選擇其中一個 hello 下列選項：
        
        * 部署 hello 預設由 Azure 所提供的 JDK
        * 從 Azure 提供的其他 JDK 下接式清單中部署協力廠商 JDK
        * 部署自訂 JDK，這必須封裝為 ZIP 檔案，而且公開可用或位於您的 Azure 儲存體帳戶中
        
        ![新增應用程式容器 JDK 索引標籤][11b]
   9. 當您完成所有 hello 上述步驟時，hello 新的 Web 應用程式容器 對話方塊應該類似下列圖中的 hello:
      
       ![新增應用程式容器][14]
   10. 按一下**確定**toocomplete hello 建立新的 Web 應用程式容器。
       
        等候數秒鐘，讓 hello Web 應用程式容器 toobe hello 清單重新整理，現在應 hello 清單中選取您新建立的 web 應用程式的容器。
6. 現在您已經準備就緒 toocomplete hello 初始部署您的 Web 應用程式 tooAzure;按一下**確定**toodeploy 您的 Java 應用程式 toohello 選取 Web 應用程式的容器。 根據預設，您的應用程式將會部署為 hello 應用程式伺服器的子目錄。 如果您想 toobe 部署為 hello 根應用程式，請檢查 hello**部署 tooroot**核取方塊後，再按一下**確定**。
   
    ![部署 tooAzure][15]
7. 接下來，您應該會看見 hello **Azure 活動記錄檔**檢視，其中將指出 hello Web 應用程式的部署狀態。
   
    ![進度指示器][16]
   
    部署 Web 應用程式 tooAzure 的 hello 程序應該採取只有幾秒鐘 toocomplete。 當您的應用程式已備妥，您會看到名為的連結**發佈**在 hello**狀態**資料行。 當您按一下 hello 連結時，它會帶您 tooyour 部署 Web 應用程式的首頁上，或您可以使用 hello 跟隨 toobrowse tooyour web 應用程式 > 一節中的 hello 步驟。

## <a name="browsing-tooyour-web-app-on-azure"></a>瀏覽 tooyour 在 Azure 上的 Web 應用程式
toobrowse tooyour 在 Azure 上的 Web 應用程式，您可以使用 hello **Azure 總管**檢視。

如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**檢視**功能表 IntelliJ，然後按一下**工具視窗**，然後按一下 **服務總管**。 如果您先前尚未登入，則會提示您 toodo 因此。

當 hello **Azure 總管**檢視隨即顯示，使用依照這些步驟 toobrowse tooyour Web 應用程式： 

1. 展開 hello **Azure**節點。
2. 展開 hello **Web 應用程式**節點。 
3. 以滑鼠右鍵按一下 hello 所需的 Web 應用程式。
4. Hello 操作功能表出現時，按一下**瀏覽器中開啟**。
   
    ![瀏覽 Web 應用程式][17]

## <a name="updating-your-web-app"></a>更新 Web 應用程式
更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：

* 您可以更新 hello 部署現有的 Java Web 應用程式。
* 您可以將額外的 Java 應用程式 toohello 發行相同的 Web 應用程式容器。

在任一情況下，hello 程序相同，並需要只有幾秒鐘的時間：

1. 在 hello IntelliJ 專案總管 中，以滑鼠右鍵按一下您想要 tooupdate 或加入現有的 Web 應用程式容器 tooan 的 hello Java 應用程式。
2. Hello 操作功能表出現時，選取**Azure**然後**發行為 Azure Web 應用程式...**
3. 由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。 選取 hello 一您想要 toopublish 或重新發佈您的 Java 應用程式 tooand 按一下**確定**。

在幾秒鐘後，hello **Azure 活動記錄檔**檢視會顯示為您更新的部署**已發佈**而且您將會無法 tooverify 網頁瀏覽器應用程式更新。

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>啟動、停止或重新啟動現有的 Web 應用程式
toostart 或停止現有的 Azure Web 應用程式容器，（包括所有部署的 hello Java 應用程式中），您可以使用 hello **Azure 總管**檢視。

如果 hello **Azure 總管**檢視尚未開啟，您可以再按一下來開啟**檢視**功能表 IntelliJ，然後按一下**工具視窗**，然後按一下 **服務總管**。 如果您先前尚未登入，則會提示您 toodo 因此。

當 hello **Azure 總管**檢視隨即顯示，請遵循這些步驟 toostart 使用，或停止 Web 應用程式： 

1. 展開 hello **Azure**節點。
2. 展開 hello **Web 應用程式**節點。 
3. 以滑鼠右鍵按一下 hello 所需的 Web 應用程式。
4. Hello 操作功能表出現時，按一下**啟動**，**停止**，或**重新啟動**。 請注意，hello 功能表選項內容感知，所以您只可以停止正在執行的 web 應用程式或啟動 web 應用程式目前未執行的。
   
    ![停止 Web 應用程式][18]

## <a name="next-steps"></a>後續步驟
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列連結查看 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [安裝 Azure Toolkit for Eclipse hello]
  * [Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]
  * [功能 hello Azure Toolkit for Eclipse 中的新功能]
* [Azure Toolkit for IntelliJ]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * <bpt id="p1">*</bpt>Create a Hello World Web App for Azure in IntelliJ (This Article)<ept id="p1">*</ept>
  * [新功能 hello Azure Toolkit for IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>另請參閱
如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]。

如需有關建立 Azure Web 應用程式的詳細資訊，請參閱 hello [Web 應用程式的概觀]。

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse (在 Eclipse 中建立 Azure Hello World Web 應用程式)]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ../azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[功能 hello Azure Toolkit for Eclipse 中的新功能]: ../azure-toolkit-for-eclipse-whats-new.md
[新功能 hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Web 應用程式的概觀]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
