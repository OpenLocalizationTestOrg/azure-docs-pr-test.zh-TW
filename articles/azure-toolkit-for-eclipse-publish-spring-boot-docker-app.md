---
title: "aaaPublish Spring 開機應用程式以使用 Docker 容器 hello Azure Toolkit for Eclipse |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Docker 容器發行 Spring 開機應用程式使用 hello Azure Toolkit for Eclipse

hello [Spring 架構]是開放原始碼解決方案，可協助建立企業級應用程式的 Java 開發人員。 其中一個 hello 更常用建置的專案是在該平台是[Spring 開機]，可提供簡單的方法建立獨立的 Java 應用程式。

[Docker]是開放原始碼解決方案，可協助開發人員自動化 hello 部署、 調整及管理其容器中執行的應用程式。

本教學課程中引導您完成 hello 步驟 toodeploy Spring 開機應用程式，Azure Docker 容器 tooMicrosoft 為使用 hello Azure Toolkit for Eclipse。

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>複製 hello 預設 Spring 開機 Docker 儲存機制

### <a name="import-hello-public-repository"></a>匯入 hello 公用儲存機制

hello 下列步驟引導您完成使用 IntelliJ 複製 hello Spring 開機 Docker 儲存機制 tooyour 本機電腦。 如果您想 toouse 命令列，請參閱[部署 Spring 開機應用程式在 Azure 容器服務中的 Linux 上][Deploy Spring Boot on Linux in ACS]。

1. 開啟 Eclipse。

1. 按一下 [檔案] > [匯入]。

   ![檔案匯入功能表][CL01]

1. 當 hello**匯入**對話方塊隨即開啟：

   a. 展開 [Git]。

   b. 選取 [Projects from Git] (Git 中的專案)。
   
   c. 按一下 [下一步] 。

   ![匯入對話方塊][CL02]

1. 在 hello**選取儲存機制來源**頁面：

   a. 選取 [Clone URI] (複製 URI)。
   
   b. 按一下 [下一步] 。

   ![[選取存放庫來源] 頁面][CL03]

1. 在 hello**來源 Git 儲存機制**頁面：

   a. 針對 [URI]，輸入 `https://github.com/spring-guides/gs-spring-boot-docker.git`。 此步驟應該自動填入 hello**主機**和**儲存機制路徑**hello 欄位更正的值。
   
   b. 讓您的 Git 使用者名稱和密碼，您應該不需要 tooenter，是公用的 hello Spring 開機儲存機制。
   
   c. 按一下 [下一步] 。

   ![[來源 Git 存放庫] 頁面][CL04]

1. 在 hello**分支選取**頁面上，按一下**下一步**。

   ![[分支選擇] 頁面][CL05]

1. 在 hello**本機目的地**頁面：

   a. 指定您想要您的本機儲存機制的 hello 本機資料夾。
   
   b. 按一下 [下一步] 。

   ![[本機目的地] 頁面][CL06]

1. 在 hello**選取匯入專案精靈 toouse**頁面：

   a. 選取 [Import as a general project] (匯入為一般專案)。
   
   b.這是另一個 C# 主控台應用程式。 按一下 [下一步] 。

   ![[選擇匯入專案精靈 toouse] 頁面][CL07]

1. 在 hello**匯入專案**頁面：

   a. 指定專案名稱。
   
   b. 按一下 [完成] 。

   ![[匯入專案] 頁面][CL08]

1. 當 hello 儲存機制成功複製時，您會看到在 Eclipse 中列出的所有 hello 檔案。

   ![Local repository (本機存放庫)][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>從本機存放庫建立 Maven 專案

hello Spring 開機 Docker 儲存機制包含將用於此教學課程已完成的 Maven 專案。 

1. 按一下 [檔案] > [匯入]。

   ![匯入 hello 檔案 功能表上的命令][CL01]

1. 當 hello**匯入**對話方塊隨即開啟：

   a. 展開 [Maven]。
   
   b. 選取 [Existing Maven Projects] (現有 Maven 專案)。
   
   c. 按一下 [下一步] 。

   ![匯入對話方塊][MV01]

1. 在 hello **Maven 專案**頁面：

   a. 如**根目錄**，指定 hello**完成**本機儲存機制中的資料夾。
   
   b. 展開 hello**進階**區段，然後輸入的自訂名稱**名稱範本**。
   
   c. 選取 hello 方塊 hello **pom.xml** hello 專案中的檔案。
   
   d. 按一下 [完成] 。

   ![[Maven 專案] 頁面][MV02]

1. 已成功開啟 hello Maven 專案時，您會看到在 Eclipse 中列出的第二個專案。

   ![Local Maven project (本機 Maven 專案)][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>使用 Maven 建置 Spring Boot 應用程式

1. 在 [hello Eclipse 的專案總管] 中，選取 hello Maven 專案。

1. 按一下 [執行] > [執行身分] > [Maven 組建]。

   ![命令 toorun 為 Maven 建置][BU01]

1. 當您的應用程式建置成功時，hello 主控台視窗會顯示 hello 狀態。

   ![Successful Maven build (成功的 Maven 組建)][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>使用 Docker 容器發行您的 web 應用程式 tooAzure

1. 在 [hello Eclipse 的專案總管] 中，選取 hello Maven 專案。

1. 按一下 hello Azure**發行**功能表，然後再按一下**發佈為 Docker 容器**。

   ![[發佈為 Docker 容器] 命令][PU01]

1. 當 hello**在 Azure 上部署 Docker 容器** 對話方塊隨即出現：

   a. 輸入自訂 Docker 映像名稱。
   
   b. 如**成品 toodeploy**，指定 hello 路徑 toohello **gs-spring-開機-docker-0.1.0.jar**您剛才建置的檔案。

   ![Specify Docker options (指定 Docker 選項)][PU02]

   顯示任何現有的 Docker 主機。 

1. 如果您選擇 toodeploy tooan 現有主機，您可以略過 toostep 5。 否則，請使用下列步驟 toocreate 主機 hello:

   a. 按一下 [新增] 。

      ![新增 Docker 主機][PU03]

   b. 當 hello**建立 Docker 主機** 對話方塊隨即出現，您可以選擇 tooaccept hello 預設值，或者您可以指定新的 Docker 主機的任何自訂設定。 (如需詳細說明 hello 的各種設定，請參閱[為 Docker 容器發行 web 應用程式，使用 IntelliJ hello Azure Toolkit][Publish Container with Azure Toolkit]。)按一下**下一步**當您指定哪些設定 toouse。

      ![指定 Docker 主機選項][PU04]

   c. 您可以從 Azure 金鑰保存庫選擇 toouse 現有登入認證，或者您可以選擇 tooenter 新 Docker 登入認證。 當您已指定選項時，按一下 [完成]。

      ![指定 Docker 主機認證][PU05]

1. 選取您的 Docker 主機，然後按一下下一步。

   ![選取 Docker 主機 toouse][PU06]

1. Hello hello 最後一頁上**在 Azure 上部署 Docker 容器**對話方塊方塊中，指定下列選項的 hello:

   a. 您可以選擇 toospecify hello 容器，將會裝載您的 Docker 容器的自訂名稱，或者您可以接受 hello 預設值。

   b. 使用下列語法的 hello docker 主機輸入 hello TCP 連接埠： *[外部連接埠]*:*[內部連接埠]*。 例如， **80:8080**指定外部連接埠 80 與 hello 預設 Spring 開機的內部連接埠 8080。
   
      如果您已自訂您的內部連接埠 （例如，藉由編輯 hello application.yml 檔案），您需要 toospecify hello 連接埠號碼 hello 正確路由的 toooccur 在 Azure 中。

   c. 設定這些選項之後，按一下 [完成]。

   ![在 Azure 上部署 Docker 容器][PU07]

1. 當 hello Azure Toolkit 完成發行時，hello Azure 活動記錄檔顯示**發佈**hello 狀態。

   ![已成功部署 Docker 主機][PU08]

## <a name="next-steps"></a>後續步驟

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring 開機]: http://projects.spring.io/spring-boot/
[Spring 架構]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
