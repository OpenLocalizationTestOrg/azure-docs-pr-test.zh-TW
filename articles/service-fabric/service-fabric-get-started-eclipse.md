---
title: "Service Fabric plug-in for Eclipse aaaAzure |Microsoft 文件"
description: "開始使用 Service Fabric 外掛程式 hello for Eclipse。"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>適用於 Eclipse Java 應用程式開發的 Service Fabric 外掛程式
Eclipse 是其中一個最常使用的 hello for Java 開發人員的整合式開發環境 (Ide)。 在本文中，我們說明如何設定與 Azure Service Fabric 您 Eclipse 開發環境 toowork tooset。 了解 tooinstall hello 外掛程式，Service Fabric 建立 Service Fabric 應用程式和部署 Service Fabric 應用程式 tooa 本機或遠端 Service Fabric 叢集在 Eclipse Neon 的方式。

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>安裝或更新 hello Service Fabric Eclipse Neon 外掛程式
您可以在 Eclipse 中安裝 Service Fabric 外掛程式。 hello 外掛程式，可協助簡化建置和部署 Java 服務 hello 程序。

1.  請確定您擁有 hello 最新版本的 Eclipse Neon 和 hello 最新版 Buildship 安裝 （1.0.17 或更新版本）：
    -   已安裝的元件，在 Eclipse Neon toocheck hello 版本太移**協助** > **安裝詳細資料**。
    -   tooupdate Buildship，請參閱[Eclipse Buildship: Eclipse 外掛程式 Gradle][buildship-update]。
    -   如 toocheck 和安裝更新的 Eclipse Neon 移過**協助** > **檢查更新**。

2.  tooinstall hello Service Fabric 外掛程式，請在 Eclipse Neon 跳過**協助** > **安裝新軟體**。
  1.    在 hello**搭配**方塊中，輸入**http://dl.microsoft.com/eclipse**。
  2.    按一下 [新增] 。

         ![適用於 Eclipse Neon 的 Service Fabric 外掛程式][sf-eclipse-plugin-install]
  3.    選取 hello Service Fabric 外掛程式，然後按一下**下一步**。
  4.    完成 hello 安裝步驟，並接受 hello Microsoft 軟體授權條款。

如果您已經有 hello Service Fabric 外掛程式安裝，請確定您已擁有 hello 最新版本。 可用的更新，toocheck 移過**協助** > **安裝詳細資料**。 Hello 在清單中已安裝的外掛程式，請在選取 Service Fabric，，然後按一下**更新**。 將安裝可用的更新。

> [!NOTE]
> 如果安裝或更新 hello Service Fabric 外掛程式緩慢時，它可能是因為 tooan Eclipse 設定。 Eclipse 會收集的所有變更 tooupdate 站台會向您的 Eclipse 執行個體中繼資料。 toospeed hello 程序，檢查及安裝的 Service Fabric 外掛程式更新，跳過**可用軟體的站台**。 清除所有的站台，除了 hello 點 toohello Service Fabric 外掛程式的位置 (http://dl.microsoft.com/eclipse/azure/servicefabric) 的其中一個 hello 核取方塊。

## <a name="create-a-service-fabric-application-in-eclipse"></a>在 Eclipse 中建立 Service Fabric 應用程式

1.  在 Eclipse Neon 移過**檔案** > **新增** > **其他**。 選取 **Service Fabric 外掛程式**，然後按 [下一步]。

    ![Service Fabric 新專案第 1 頁][create-application/p1]

2.  輸入專案的名稱，然後按 [下一步]。

    ![Service Fabric 新專案第 2 頁][create-application/p2]

3.  在 hello 範本清單中選取**服務範本**。 選取服務範本類型 (執行者、無狀態、容器或來賓二進位)，然後按 [下一步]。

    ![Service Fabric 新專案第 3 頁][create-application/p3]

4.  輸入 hello 服務名稱和服務的詳細資訊，，然後按一下**完成**。

    ![Service Fabric 新專案第 4 頁][create-application/p4]

5. 當您建立第一個 Service Fabric 專案，在 hello**開啟相關聯的檢視方塊**對話方塊中，按一下 **是**。

    ![Service Fabric 新專案第 5 頁][create-application/p5]

6.  新的專案看起來像這樣︰

    ![Service Fabric 新專案第 6 頁][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>在 Eclipse 中建置和部署 Service Fabric 應用程式

1.  以滑鼠右鍵按一下新的 Service Fabric 應用程式，然後選取 [Service Fabric]。

    ![Service Fabric 快顯功能表][publish/RightClick]

2. 在 hello 子功能表中，選取您想要的 hello 選項：
    -   按一下 toobuild hello 應用程式，而不清除，**建置的應用程式**。
    -   toodo 乾淨的組建的 hello 應用程式中，按一下**重建應用程式**。
    -   按一下 tooclean hello 應用程式的內建的成品，**全新的應用程式**。

3.  您也可以從這個功能表選擇部署、解除部署和發佈應用程式：
    -   toodeploy tooyour 本機叢集，按一下 **部署應用程式**。
    -   在 hello**發行應用程式**對話方塊方塊中，選取 發行設定檔：
        -  **Local.json**
        -  **Cloud.json**

     這些 JavaScript Object Notation (JSON) 檔案會儲存必要的 tooconnect tooyour 本機或雲端 (Azure) 叢集的資訊 （例如連接端點和安全性資訊）。

  ![Service Fabric 發佈功能表][publish/Publish]

替代方式 toodeploy Service Fabric 執行應用程式使用 Eclipse 組態。

  1.    跳過**執行** > **回合組態**。
  2.    在下**Gradle 專案**，選取 hello **ServiceFabricDeployer**執行設定。
  3.    Hello 右窗格中，在 hello**引數**索引標籤上，針對**publishProfile**，選取**本機**或**雲端**。  hello 預設值是**本機**。 遠端 toodeploy tooa 或選取的雲端叢集**雲端**。
  4.    tooensure hello 適當的資訊會在 hello 填入發行設定檔，請編輯**Local.json**或**Cloud.json**視。 您可以新增或更新端點詳細資料和安全性認證。
  5.    請確認**工作目錄**點想 toodeploy toohello 應用程式。 toochange hello 應用程式中，按一下 hello**工作區**按鈕，然後再選取您想要的 hello 應用程式。
  6.    按一下 套用，然後按一下執行。

幾分鐘內即可建置和部署您的應用程式。 您可以監視 Service Fabric 總管中的 hello 部署狀態。  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>新增 Service Fabric 服務 tooyour Service Fabric 應用程式

tooadd Service Fabric 服務 tooan 現有 Service Fabric 應用程式，下列步驟 hello:

1.  以滑鼠右鍵按一下您想要 tooadd 的服務，然後再按一下 hello 專案**Service Fabric**。

    ![Service Fabric 新增服務第 1 頁][add-service/p1]

2.  按一下**新增 Service Fabric 服務**，並完成 hello 的步驟 tooadd 服務 toohello 專案設定。
3.  選取 hello 服務想要的範本 tooadd tooyour 專案，然後按一下**下一步**。

    ![Service Fabric 新增服務第 2 頁][add-service/p2]

4.  輸入 hello 服務名稱 （和其他詳細資料，視需要），然後按一下hello**加入服務** 按鈕。  

    ![Service Fabric 新增服務第 3 頁][add-service/p3]

5.  加入 hello 服務之後，您整體的專案結構看起來類似 toohello 下列專案：

    ![Service Fabric 新增服務第 4 頁][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>編輯 Service Fabric Java 應用程式的資訊清單版本

tooedit 資訊清單版本，hello 專案上按一下滑鼠右鍵，跳過**Service Fabric**選取**編輯資訊清單版本...**從 hello 功能表下拉式清單。 在 hello 精靈中，您可以更新應用程式資訊清單，服務資訊清單的 hello 資訊清單版本和 hello 版本**程式碼**， **Config**和**資料**封裝。

如果您核取 hello 選項**自動更新應用程式和服務版本**和更新版本，然後將會自動更新 hello 資訊清單版本。 toogive 的範例，您先選取 hello 核取方塊，然後更新 hello 版本**程式碼**版本 0.0.0 too0.0.1 並按一下**完成**，然後服務資訊清單版本和應用程式資訊清單會自動更新的 too0.0.1 版本。

## <a name="upgrade-your-service-fabric-java-application"></a>升級 Service Fabric Java 應用程式

升級案例中，假設您建立 hello **App1** hello Service Fabric 外掛程式在 Eclipse 的專案。 您使用部署 hello 外掛程式 toocreate 應用程式名為**fabric: / App1Application**。 hello 應用程式類型是**App1AppicationType**，和 hello 應用程式版本為 1.0。 現在，您希望 tooupgrade 應用程式不會插斷可用性。

首先，tooyour 應用程式中，進行任何變更，然後重新建立 hello 修改服務。 更新 hello 修改服務的資訊清單檔案 (ServiceManifest.xml) 與 hello 服務 （和程式碼、 組態中，或為相關的資料） 的 hello 更新版本。 此外，修改 hello 應用程式資訊清單 (ApplicationManifest.xml) 與更新的 hello hello 應用程式的版本號碼和 hello 已修改的服務。  

tooupgrade 使用 Eclipse Neon 應用程式，您可以建立重複的執行的組態設定檔。 然後，使用 tooupgrade 視您的應用程式。

1.  跳過**執行** > **回合組態**。 Hello 左窗格中，按一下 hello 的小箭號 toohello 左邊**Gradle 專案**。
2.  以滑鼠右鍵按一下 **ServiceFabricDeployer**，然後選取 [重複]。 輸入此設定的新名稱，例如，**ServiceFabricUpgrader**。
3.  在 hello 右面板中，在 hello**引數**索引標籤上，變更**層 Pconfig = '部署'**太**層 Pconfig = '升級'**，然後按一下**套用**。

此程序會建立並執行的組態設定檔會儲存您可以在任何時間 tooupgrade 使用您的應用程式。 它也會取得從 hello 應用程式資訊清單檔案的 hello 最新的更新的應用程式類型版本。

hello 應用程式升級將會花費幾分鐘的時間。 您可以監視 Service Fabric 總管中的 hello 應用程式升級。

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>移轉舊服務網狀架構 Java 應用程式 toobe 搭配 Maven 使用
我們最近已從 Service Fabric Java SDK tooMaven 儲存機制移服務網狀架構 Java 文件庫。 雖然 hello 新應用程式，您可以產生使用 Eclipse 中，將會產生 （這會是可以與 Maven toowork） 最新版本更新的專案，您可以更新您現有的 Service Fabric 無狀態或執行者 Java 應用程式，而且已使用 hello Service Fabric Java SDK更早版本，toouse hello 服務網狀架構 Java 相依性從 Maven。 請遵循所述的 hello 步驟[這裡](service-fabric-migrate-old-javaapp-to-use-maven.md)tooensure Maven 適用於較舊的應用程式。

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
