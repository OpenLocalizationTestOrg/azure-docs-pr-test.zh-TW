---
title: "aaaCreate Hello World Azure 雲端服務在 Eclipse 中"
description: "了解如何 toocreate 簡單的 Hello World 應用程式使用 hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>在 Eclipse 中為 Azure 建立 Hello World 雲端服務
hello 下列步驟說明如何 toocreate 及部署使用 hello Azure Toolkit for Eclipse 的基本 JSP 應用程式 tooAzure。 下文所示的 JSP 範例乃力求簡潔，不過只要與 Azure 部署相關，幾乎類似的步驟皆適用於 Java servlet。

hello 應用程式看起來類似 toohello 下列：

![][ic600360]

## <a name="prerequisites"></a>必要條件
* Java Developer Kit (JDK) 1.7 版或更新版本。
* Eclipse IDE for Java EE Developers (Indigo 或更新版本)。 這可透過 <http://www.eclipse.org/downloads/> 下載。
* Java 型 Web 伺服器或應用程式伺服器的散發套件，例如 Apache Tomcat、GlassFish、JBoss Application Server、Jetty 或 IBM® WebSphere® Application Server Liberty Core。
* Azure 訂用帳戶，可從 <http://azure.microsoft.com/pricing/purchase-options/> 取得。
* hello Azure Toolkit for Eclipse。 如需詳細資訊，請參閱[安裝 hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]。

## <a name="toocreate-a-hello-world-application"></a>toocreate Hello World 應用程式
首先，我們將從建立 Java 專案開始。

1. 啟動 Eclipse 中，並在 hello 功能表按一下**檔案**，按一下 **新增**，然後按一下**動態 Web 專案**。 (如果您沒有看到**動態 Web 專案**列為可用的專案，按一下後**檔案**，**新增**，請勿然後 hello 遵循： 按一下**檔案**，按一下 **新增**，按一下 **專案...**，依序展開**Web**，按一下 **動態 Web 專案**，然後按一下**下一步**。)

1. 本教學課程的目的而言，專案的名稱，hello **MyHelloWorld**。 (請確定您使用此名稱，在本教學課程的後續步驟預期您 WAR 檔案 toobe 命名為 MyHelloWorld)。 您的畫面會出現類似 toohello 下列：

   ![][ic589576]

1. 按一下 [完成] 。

1. 在 Eclipse 的 [專案總管] 檢視中，展開 [MyHelloWorld]。 在 WebContent 上按一下滑鼠右鍵、按一下 新增，然後按一下JSP 檔案。

1. 在 hello**新增 JSP 檔案**對話方塊中，名稱 hello 檔**index.jsp**。 保留 hello 父資料夾為**MyHelloWorld/WebContent**hello 下列所示：

   ![][ic659262]

1. 在 hello**選取 JSP 範本**對話方塊中的，針對這個教學課程，請選取目的**新增 JSP 檔案 (html)**按一下**完成**。

1. Hello index.jsp 檔案開啟時在 Eclipse 中，增益集文字 toodynamically 顯示**Hello World ！** 在現有的 hello`<body>`項目。 您已更新`<body>`內容應該會出現如下所示 hello:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. 儲存 index.jsp。

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy 您的應用程式 tooAzure、 hello 快速且簡單的方式
只要您有 Java web 應用程式準備好 tootest，您可以使用下列捷徑 tootry 它編寫直接 hello Azure 在雲端的 hello。

1. 在 Eclipse 的 [專案總管] 中，按一下 [MyHelloWorld] 。

2. 在 hello Eclipse 工具列中，按一下 hello**發行**下拉式按鈕，然後按一下**發佈做為 Azure 雲端服務**

   ![][publishDropdownButton]

3. 如果您要發行的 hello 這個應用程式 tooAzure 第一次，而且您尚未建立 Azure 部署專案之前此應用程式，Azure 部署專案會自動建立。 您應該會看到 hello 遵循提示字元中，也會列出 hello JDK 封裝和應用程式伺服器將會自動部署 toorun 應用程式。

   ![][ic789598]
   
   這個快顯方法可讓快速且輕鬆 tootest 您在 Azure 中的應用程式而不需要 tooconfigure 特定伺服器或與 hello 預設值不同的 JDK。 如果您滿意 hello 預設值，您可以按一下**確定**toocontinue 以 hello 下列步驟。
   不過，如果您想 toochange hello JDK 或應用程式伺服器 toouse 應用程式，您稍後可以執行，藉由編輯 hello Azure 部署專案會自動建立，或者您可以按一下**取消**現在和讀取hello**關於 Azure 部署專案區段**本教學課程。

4. 在 hello**發行 tooAzure**對話方塊：

   1. 如果 hello 中不有任何訂閱 tooselect**訂用帳戶**清單，但您的訂用帳戶資訊，請遵循這些步驟 tooimport:
      1. 按一下 [從 PUBLISH-SETTINGS 檔案匯入] 。
      2. 在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 **下載發行設定檔案**。 如果尚未登入您的 Azure 帳戶，您將會提示的 toolog 中。 然後系統會提示您 toosave Azure 發行設定檔。 將它儲存 tooyour 本機電腦。
      3. 仍在 hello**匯入訂用帳戶資訊** 對話方塊中，按一下 hello**瀏覽**按鈕、 選取 hello 發行在 hello 先前步驟中，在本機儲存的設定檔，然後按一下 **開啟**。 您的畫面應該看起來類似 toohello 下列：![][ic644267]
      4. 按一下 [確定] 。
   2. 如**訂用帳戶**，選取您要使用您的部署的 hello 訂用帳戶。
   3. 如**儲存體帳戶**，選取您想 toouse，或按一下 hello 儲存體帳戶**新增**toocreate 新的儲存體帳戶。
   4. 如**服務名稱**，選取您想 toouse，或按一下 hello 雲端服務**新增**toocreate 新的雲端服務。
   5. 如**目標 OS**，選取您為您的部署想 toouse hello 作業系統 hello 版本。
   6. 針對 [目標環境]，基於本教學課程的目的，請選取 [預備]。 (當您準備好 toodeploy tooyour 生產網站時，您要變更這太**生產**。)
   7. 選擇性： 請確定**覆寫先前部署**會檢查您是否新的部署 tooautomatically 覆寫 hello 先前的部署。 當您啟用此選項時，您會不出現 「 409 衝突 」 問題發佈 toohello 時相同的位置。
      請注意該 hello**發行 tooAzure**對話方塊包含的區段**遠端存取**。 根據預設，不會啟用遠端存取，而且我們不會針對此範例啟用它。 tooenable 遠端存取，您會輸入使用者名稱和密碼 toouse 時從遠端登入。 如需有關遠端存取的詳細資訊，請參閱[在 Eclipse 中啟用 Azure 部署的遠端存取][Enabling Remote Access for Azure Deployments in Eclipse]。
      您**發行 tooAzure**對話方塊將會出現類似 toohello 下列：![][ic719488]

5. 按一下**發行**toopublish toohello 預備環境。

   當提示的 tooperform 完整建置，按一下**是**。 這可能需要幾分鐘的時間 hello 第一次組建。
   [Azure 活動記錄檔]  會顯示在 Eclipse 索引標籤式的檢視區段。
   ![][ic719489]您可以使用此記錄檔，以及 hello**主控台**檢視，您的部署 toosee hello 進度。 替代方式是在 toohello toolog [Azure 管理入口網站][Azure Management Portal]，並使用 hello**雲端服務**區段 toomonitor hello 狀態。

6. 已成功部署您的部署時，hello **Azure 活動記錄檔**將顯示的狀態**發佈**。 按一下**發佈**，如下所示 hello 下列映像，以及您的瀏覽器會開啟您的部署的執行個體。

   ![][ic719490]

由於這是預備環境部署 tooa，hello DNS 名稱會是 hello 格式 http:// 的&lt;*guid*&gt;。.cloudapp.net，且 hello URL 將包含 hello DNS 名稱再加上您的應用程式的尾碼。 例如，http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld。 (hello **MyHelloWorld**部分會區分大小寫。)您也可以查看 hello DNS 名稱，如果您按一下 hello （hello 雲端服務部分 hello 管理入口網站） 中的 hello Azure 平台管理入口網站中的部署名稱。

雖然本逐步解說是針對預備環境部署 toohello，部署 tooproduction 遵循除了 hello 相同的步驟，在 hello**發行 tooAzure**對話方塊中，選取**生產**而不是**臨時**hello**目標環境**。 部署 tooproduction 會導致根據您的選擇，而不是所使用的臨時的 GUID hello DNS 名稱的 URL。

> [!WARNING]
> 此時您已部署 Azure 應用程式 toohello 雲端。 不過，再繼續進行，請注意，部署的應用程式，即使未執行，會繼續 tooaccrue 訂用帳戶的計費時間。 因此，請務必從 Azure 訂用帳戶刪除任何不需要的部署。
> 
> 

## <a name="about-azure-deployment-projects"></a>關於 Azure 部署專案
在順序 toodeploy 一或多個 Java 應用程式 tooAzure，需要 Azure 部署專案。 它扮演 「 封裝 」，應用程式需要包裝成，在 Azure 上發行的順序 toobe toobe hello hello 角色。

除了 hello 您應用程式的資訊，Azure 部署專案也包含其他索引鍵的元件、 以部署的資訊最重要的是： hello，在 web 應用程式的應用程式伺服器容器 toorun 和 hello Java 執行階段 toorun 它上。 Azure 支援大範圍的 Java 執行階段和 Java 應用程式伺服器，讓您可以從中選擇。

雖然這裡使用的 hello 範例基於教育目的，已大幅簡化，Azure 部署專案也可以包含其他重要組態資訊，可讓您 toocreate 幾乎各種複雜、 可調整、 高可用性多層式雲端服務與您的應用程式。 您可以啟用**工作階段親和性** (「黏性工作階段」)、**快速快取**、**SSL 卸載**、**防火牆/連接埠路由**、**遠端存取**和一些其他強大功能。

如果您已經完成本教學課程的 hello 前一節 (「 toodeploy 您的應用程式 tooAzure、 hello 快速且簡單的方式 」)，您現在可以看到新的 Azure 部署專案，在 [專案總管] 會自動為您產生與名為的 hello"**MyHelloWorld_onAzure**"。

您可能有也開始本教學課程先自行建立空白的 Azure 部署專案，然後將加入您的應用程式 tooit。 它是較長程序，但讓您更充分掌控 hello hello 開頭的初始組態。

toocreate 從頭，新的 Azure 部署專案按一下 hello**新增 Azure 部署專案**按鈕![][ic710876]。

不論您是使用現有的 Azure 部署專案，還是從頭建立，您可以 toochange 其組態設定和元件，例如 hello JDK 或 hello 應用程式伺服器，也同樣容易在任何時間。

toochange hello JDK、 hello 應用程式伺服器或在現有的 Azure 部署專案中的 hello 應用程式清單：

1. 展開 [hello] 專案節點 (例如**MyHelloWorld_onAzure**) hello [專案總管] 中

2. 以滑鼠右鍵按一下 [WorkerRole1] 

3. 展開 hello **Azure** hello 內容功能表中的子功能表

4. 按一下 [伺服器組態] 

不論是否您藉由編輯現有的 Azure 部署專案，如上所示，啟動這些伺服器組態設定步驟，或建立一個新從頭，您會看到 hello 相同類型的對話方塊，可讓您 tooconfigure JDK、 伺服器和應用程式元件。 toolearn toochange hello 設定這些對話方塊中，例如 toochange hello JDK、 更如何 hello 應用程式伺服器以及新增或移除應用程式在部署中，請參閱 hello[伺服器組態屬性][ Server configuration properties]發行項。

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>僅限 Windows: toodeploy 應用程式 toohello 計算模擬器

> [!NOTE]
> 在 Windows 上，才可使用 hello Azure 模擬器。 如果您使用 Windows 以外的作業系統，請略過本節。
> 
> 

如果您已經建立新的 Azure 部署專案 hello 步驟描述之前，也就是隱含的方式，藉由發行您的應用程式 tooAzure，hello JDK 和應用程式伺服器已設定 hello 雲端，但不是會針對本機模擬。 tooprepare 在 hello 本機模擬器中，測試專案，請遵循下列步驟：

1. 在 Eclipse 的 [專案總管] 中，按一下 [MyHelloWorld_onAzure]。

2. 以滑鼠右鍵按一下 [WorkerRole1] 。

3. 展開 hello **Azure** hello 內容功能表中的子功能表。

4. 按一下 [伺服器組態] 。

5. 在 hello **JDK**索引標籤上，檢查是否 hello 工具組已預先設定預設值為您的本機 JDK。 如果沒有，或如果您想 toochange hello 假設預設值，請確定該 hello**使用 hello JDK 進行本機測試此檔案路徑**核取方塊，並指定 hello 想 toouse JDK 安裝位置。 如果您想 toochange，按一下 hello**瀏覽**按鈕，然後使用 hello 瀏覽控制項，選取 hello JDK toouse hello 目錄位置。

6. 按一下 hello**伺服器** 索引標籤。

7. 在 hello**本機伺服器路徑**在 hello hello 對話方塊底部的文字方塊中，輸入本機安裝的伺服器符合 hello 類型和底下選取頂端 hello hello 對話方塊中的 hello 伺服器主要版本號碼的 hello 路徑hello**部署這種伺服器**核取方塊。 如果您想 toouse，不同的類型或 hello 應用程式伺服器的主要版本，請先變更 hello 選取該核取方塊底下。

8. 按一下 [確定] 。

9. 在 hello Eclipse 工具列中，按一下 [hello**在 Azure 模擬器中執行**] 按鈕， ![][ic710879]。 如果 hello**在 Azure 模擬器中執行**按鈕未啟用，請確定**MyHelloWorld_onAzure**已在 Eclipse 的專案總管 中選取，並確定 Eclipse 的專案總管 焦點為 hello目前的視窗。 這將會第一次開始完整建置您的專案，然後啟動 hello 計算模擬器中的 Java web 應用程式。 （請注意，根據您的電腦效能特性，hello 第一次建置可能需要花費幾秒 tooa 幾分鐘的時間，但後續建置會更快）。Hello 第一次建置步驟完成後，系統會提示 Windows 使用者帳戶控制 (UAC) tooallow 由這個命令 toomake 變更 tooyour 電腦。 按一下 [是] 。

> [!IMPORTANT]
> 如果您沒有看到 hello UAC 提示 核取 hello Windows 工作列的 hello UAC 圖示，然後先按一下它。 有時 hello UAC 提示不會顯示為最上層視窗，但只會顯示為工作列圖示。
> 
> 

1. 如果有任何問題，您的專案，請檢查 hello 計算模擬器 UI toodetermine hello 輸出。 根據您的部署的 hello 內容，它可能需要幾分鐘，您的應用程式 toobe 完全 hello 計算模擬器中啟動。

2. 啟動您的瀏覽器，並使用 hello URL `http://localhost:8080/MyHelloWorld` hello 位址 (hello `MyHelloWorld` hello URL 的部分會區分大小寫)。 您應該會看到您的 MyHelloWorld 應用程式 （index.jsp 的 hello 輸出），類似 toohello 下列映像：

   ![][ic589579]

當您準備好 toostop hello Eclipse 工具列中的 hello 計算模擬器中執行您的應用程式按一下 hello**重設 Azure 模擬器** 按鈕， ![][ic710880]。

## <a name="toodelete-your-deployment"></a>toodelete 您的部署
您的部署內 hello Azure Toolkit for Eclipse，請確認 toodelete **MyHelloWorld_onAzure**已在 Eclipse 的專案總管] 中選取，請 hello Eclipse [專案總管] 具有焦點，，然後按一下hello 目前視窗hello**取消發行** 按鈕， ![][ic710883]，hello Eclipse 工具列中。 (您可以執行 hello 相同的作業，以滑鼠右鍵按一下**MyHelloWorld_onAzure**在 Eclipse 的專案總管 中，按一下**Azure** ，然後按一下**從 Azure 雲端解除部署**.)這會顯示 hello**取消發行 Azure 專案**對話方塊。

![][ic719491]

選取包含您的部署，您想 toodelete，然後再按一下選取的 hello 部署的 hello 訂用帳戶和雲端服務**取消發行**。

(替代 toousing hello toolkit toodelete hello 部署為 toouse hello**雲端服務**hello Azure 管理入口網站區段： 巡覽 tooyour 部署，加以選取，然後按 [hello**刪除** ] 按鈕。 這將會停止，然後再刪除，hello 部署。 如果您只想 toostop hello 部署，並將它刪除，請按一下 hello**停止**按鈕而不是 hello**刪除**按鈕，如上述，但如果您不會刪除 hello 部署，則可計費費用將為您的部署 tooaccrue 即使繼續已停止）。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[功能 hello Azure Toolkit for Eclipse 中的新功能][What's New in hello Azure Toolkit for Eclipse]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
