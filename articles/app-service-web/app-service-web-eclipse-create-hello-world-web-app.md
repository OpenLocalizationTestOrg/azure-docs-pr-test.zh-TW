---
title: "使用 Eclipse 建立基本的 Azure Web 應用程式 | Microsoft Docs"
description: "本教學課程將示範如何使用適用於 Eclipse 的 Azure 工具組來建立 Azure Hello World Web 應用程式。"
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
ms.openlocfilehash: 683d6828546995a4dc60d8cac0669f356501c723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>使用 Eclipse 建立基本的 Azure Web 應用程式
本教學課程示範如何使用 [適用於 Eclipse 的 Azure 工具組]，建立基本的 Hello World 應用程式，並部署到 Azure 做為 Web 應用程式。 以下所示的基本 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，類似的步驟皆適用於 Java servlet。

當您完成本教學課程，在網頁瀏覽器中檢視您的應用程式時，看起來會如下圖所示：

![Hello World 應用程式預覽][01]

## <a name="prerequisites"></a>必要條件
* Java Developer Kit (JDK) 1.8 版或更新版本。
* Eclipse IDE for Java EE Developers (Luna 或更新版本)。 這可透過 <http://www.eclipse.org/downloads/> 下載。
* Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 [Apache Tomcat] 或 [Jetty]。
* Azure 訂用帳戶，可以透過 <https://azure.microsoft.com/free/> 或 <http://azure.microsoft.com/pricing/purchase-options/> 取得。
* [適用於 Eclipse 的 Azure 工具組]。 如需安裝 Azure 工具組的相關資訊，請參閱[安裝 Azure Toolkit for Eclipse]。

## <a name="to-create-a-hello-world-application"></a>建立 Hello World 應用程式
首先，我們將從建立 Java 專案開始。

1. 啟動 Eclipse，於功能表上依序按一下 [檔案]、[新增] 及 [動態 Web 專案]。 (如果在按一下 [檔案] 和 [新增] 後沒有看到 [動態 Web 專案] 列為可用的專案，請執行下列動作：依序按一下 [檔案]、[新增]、[專案...]，展開 [Web]，按一下 [動態 Web 專案]，然後按 [下一步]。)
2. 基於本教學課程的目的，將專案命名為 **MyWebApp**。 您的畫面將出現，如下所示：
   
    ![建立新的動態 Web 專案][02]
3. 按一下 [完成] 。
4. 在 Eclipse 的 [專案總管] 檢視中，展開 [MyWebApp]。 在 [WebContent] 上按一下滑鼠右鍵、按一下 [新增]，然後按一下 [JSP 檔案]。
5. 在 [新增 JSP 檔案] 對話方塊中，將檔案命名為 **index.jsp**、將父資料夾保留為 **MyWebApp/WebContent**，然後按 [下一步]。
6. 在 [選取 JSP 範本] 對話方塊中，基於本教學課程的目的，選取 [新增 JSP 檔案 (html)]，然後按一下 [完成]。
7. 當 index.jsp 檔案在 Eclipse 中開啟時，新增文字以動態顯示 **Hello World!** (在現有 `<body>` 元素內)。 您已更新的 `<body>` 內容看起來應該與下列範例類似：
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. 儲存 index.jsp。

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>將應用程式部署至 Azure Web 應用程式容器
您有數種方式可以將 Java Web 應用程式部署至 Azure。 本教學課程說明其中一個最簡單的方式：將您的應用程式部署至 Azure Web 應用程式容器，無需特殊的專案類型或額外的工具。 Azure 會為您提供 JDK 及 Web 容器軟體，因此您不需要自己上傳；只需要您的 Java Web 應用程式。 如此一來，您的應用程式發行程序只需數秒，連一分鐘都不用。

1. 在 Eclipse 的專案總管中，以滑鼠右鍵按一下 [MyWebApp] 。
2. 在操作功能表中，選取 [Azure]，然後按一下 [發佈為 Azure Web 應用程式...]
   
    ![發佈為 Azure Web 應用程式][03]
   
    或者，您也可以在專案總管中選取 Web 應用程式專案時，按一下工具列的 [發佈] 下拉式按鈕，然後從這裡選取 [發佈為 Azure Web 應用程式]：
   
    ![發佈為 Azure Web 應用程式][14]
3. 如果尚未從 Eclipse 登入 Azure，系統會提示您登入 Azure 帳戶︰
   
    ![[Azure 登入] 對話方塊][04]
   
    如果您有多個 Azure 帳戶，登入程序期間的某些提示即使內容相同也可能會出現多次。 發生此情況時，請遵循登入指示繼續。
4. 在您成功登入 Azure 帳戶後，[管理訂用帳戶]  對話方塊將會顯示與您的認證相關聯的訂用帳戶清單。 如果列出多個訂用帳戶，而您只想使用其中幾個帳戶，您可以選擇取消選取要使用的訂用帳戶。 當您選取訂用帳戶之後，按一下 [關閉] 。
   
    ![[管理訂用帳戶] 對話方塊][05]
5. 當 [部署至 Azure Web 應用程式容器]  對話方塊出現時，它會顯示您先前建立的所有 Web 應用程式容器；如果您尚未建立任何容器，清單將會是空白的。
   
    ![[部署至 Azure Web 應用程式容器] 對話方塊][06]
6. 如果您之前尚未建立 Azure Web 應用程式容器，或您想要將應用程式發佈到新的容器中，請使用下列步驟。 否則，請選取現有的 Web 應用程式容器，並跳至以下的步驟 7。
   
   1. 按一下 [完成] 
      
       ![[部署至 Azure Web 應用程式容器] 對話方塊][15]
   2. [新增 Web 應用程式容器]  對話方塊會隨即顯示：
      
       ![[新增 Web 應用程式容器] 對話方塊][07a]
   3. 為您的 Web 應用程式容器輸入 **DNS 標籤** ，這會為您在 Azure 中的 Web 應用程式構成主機 URL 的分葉 DNS 標籤。 (請注意，名稱必須可用，且符合 Azure Web 應用程式命名需求。)
   4. 在 [Web 容器]  下拉式功能表中，為您的應用程式選取適當的軟體。
      
       目前，您可以從 Tomcat 8、Tomcat 7 或 Jetty 9 選擇。 所選軟體最新發行的版本由 Azure 提供，會在最新發行的 JDK 8 (由 Oracle 建立並由 Azure 提供) 中運作。
   5. 在 [訂用帳戶]  下拉式選單中，選取您希望此部署使用的訂用帳戶。
   6. 在 [資源群組]  下拉式功能表中，選取您要與 Web 應用程式相關聯的資源群組。 (Azure 資源群組可讓您將相關的資源分在同一組，方便一次刪除。)
      
       您可以選取現有的資源群組 (如果有)，並略過下方步驟 g，或使用以下步驟建立新的資源群組：
      
      * 按一下 [完成] 
      * [新增資源群組]  對話方塊會隨即顯示：
        
          ![[新增資源群組] 對話方塊][08]
      * 在 [名稱]  文字方塊中，為新的資源群組指定名稱。
      * 在 [區域]  下拉式功能表中，為資源群組選取適當的 Azure 資料中心位置。
      * 選擇性︰根據預設，Azure 會自動將最新的 Java 8 散發套件部署到 Web 應用程式容器，成為 JVM。 不過，如果 Web 應用程式需要的話，您也可以指定 JVM 的其他版本和散發套件。 若要指定 Web 應用程式的 JDK，請按一下 [JDK]  索引標籤，然後選取下列選項之一︰
        
        * **部署 Azure Web Apps 服務提供的預設 JDK**︰這個選項會部署最新的 Java 8 散發套件。
        * **部署 Azure 提供的第三方 JDK**：這個選項可讓您從 Microsoft Azure 提供的 JDK 清單中選擇。
        * **從這個下載位置部署自己的 JDK：**這個選項可讓您指定自己的 JDK 散發套件。您必須將它封裝為 ZIP 檔案，再上傳到公開使用的下載位置，或您擁有存取權限的 Azure 儲存體帳戶。
          
          ![[新增 Web 應用程式容器] 對話方塊][07b]
   7. 按一下 [確定] 。
   8. [App Service 方案]  下拉式功能表會列出與您選取之資源群組相關聯的應用程式服務方案。 (App Service 方案會指定如 Web 應用程式的位置、定價層及計算執行個體大小等資訊。 單一 App Service 方案可用於多個 Web Apps，這也就是要與特定 Web 應用程式部署分開維護的原因。)
      
       您可以選取現有的 App Service 方案 (如果有)，並略過下方步驟 h，或使用以下步驟建立新的 App Service 方案：
      
      * 按一下 [完成] 
      * [新增 App Service 方案]  對話方塊會隨即顯示：
        
          ![[新增 App Service 方案] 對話方塊][09]
      * 在 [名稱]  文字方塊中，為新的 App Service 方案指定名稱。
      * 在 [位置]  下拉式功能表中，為該方案選取適當的 Azure 資料中心位置。
      * 在 [定價層]  下拉式功能表中，為方案選取適當的價格。 針對測試用途，您可以選擇 [免費] 。
      * 在 [執行個體大小]  下拉式功能表中，為方案選取適當的執行個體大小。 針對測試用途，您可以選擇 [小型] 。
   9. 一旦您完成所有上述步驟之後，[New Web App Container] \(新增 Web 應用程式容器) 對話方塊看起來應該如下圖所示：
      
       ![[新增 Web 應用程式容器] 對話方塊][10]
   10. 按一下 [確定]  來完成建立新的 Web 應用程式容器。
       
        等待數秒鐘，讓 Web 應用程式容器清單重新整理；接著，您應該會在清單中看到新建立的 Web 應用程式容器已被選取。
7. 您現在已經準備好，可以完成將 Web 應用程式部署至 Azure 的初始部署：
   
    ![[部署至 Azure Web 應用程式容器] 對話方塊][11]
   
    按一下 [確定]  來將您的 Java 應用程式部署至選取的 Web 應用程式容器。
   
    根據預設，您的應用程式將會部署為應用程式伺服器的子目錄。 如果您想要部署為根應用程式，請選取 [部署到根目錄] 核取方塊，然後按一下 [確定]。
8. 接下來，您應該會看到 [Azure 活動記錄檔]  檢視，它會指出 Web 應用程式的部署狀態。
   
    ![Azure 活動記錄檔][12]
   
    將您的 Web 應用程式部署至 Azure 的程序，應該只需幾秒鐘即可完成。 當您的應用程式就緒時，您會在 [狀態]  in the **已發佈** 的連結。 當您按一下連結時，就會將您帶至已部署的 Web 應用程式首頁。

## <a name="updating-your-web-app"></a>更新 Web 應用程式
更新現有執行中的 Azure Web 應用程式是一項快速又簡單的程序，而且您有兩個更新選項：

* 您可以更新現有 Java Web 應用程式的部署。
* 您可以將其他的 Java 應用程式發佈到相同的 Web 應用程式容器。

在任一種情況中，程序都是相同的，而且只需幾秒鐘：

1. 在 Eclipse 專案總管中，以右鍵按一下您要更新或新增到現有 Web 應用程式容器的 Java 應用程式。
2. 操作功能表顯示時，選取 [Azure]，然後選取 [發佈為 Azure Web 應用程式...]
3. 由於您之前已經登入，因此會看到您現有 Web 應用程式容器的清單。 選取您要發佈或重新發佈 Java 應用程式的 Web 應用程式容器，然後按一下 [確定] 。

幾秒鐘之後，[Azure 活動記錄檔] 檢視將會將您已更新的部署顯示為 [已發佈]，而您將可以在網頁瀏覽器中確認已更新的應用程式。

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>啟動、停止或重新啟動現有的 Web 應用程式
若要啟動或停止現有的 Azure Web 應用程式容器 (包括其中所有已部署的 Java 應用程式)，您可以使用 [Azure 總管]  檢視。

如果 **Azure Explorer** 檢視尚未開啟，您可以依序按一下 Eclipse 中的 [視窗] 功能表、[顯示檢視]、[其他...]、[Azure]，然後按一下 [Azure Explorer] 來開啟。 如果您之前尚未登入，系統將會提示您登入。

顯示 [Azure 總管]  之後，使用下列這些步驟來啟動或停止您的 Web 應用程式： 

1. 展開 [Azure]  節點。
2. 展開 [Web Apps]  節點。 
3. 以滑鼠右鍵按一下所需的 Web 應用程式。
4. 當操作功能表出現時，按一下 [啟動]、[停止] 或 [重新啟動]。 請注意，功能表選項是內容感知的，因此您只能停止執行中的 Web 應用程式，或是啟動目前尚未執行的 Web 應用程式。
   
    ![停止現有的 Web 應用程式][13]

## <a name="next-steps"></a>後續步驟
如需適用於 Java IDE 的 Azure 套件組的詳細資訊，請參閱下列連結：

* [適用於 Eclipse 的 Azure 工具組]
  * [安裝 Azure Toolkit for Eclipse]
  * *在 Eclipse 中建立 Azure Hello World Web 應用程式 (本文)*
  * [適用於 Eclipse 的 Azure 工具組的新功能]
* [Azure Toolkit for IntelliJ]
  * [安裝 Azure Toolkit for IntelliJ]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]
  * [適用於 IntelliJ 的 Azure 工具組新增功能]

如需如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]。

如需建立 Azure Web Apps 的詳細資訊，請參閱 [Web 應用程式概觀]。

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[安裝 Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[適用於 Eclipse 的 Azure 工具組的新功能]: ../azure-toolkit-for-eclipse-whats-new.md
[適用於 IntelliJ 的 Azure 工具組新增功能]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Web 應用程式概觀]: ./app-service-web-overview.md
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
