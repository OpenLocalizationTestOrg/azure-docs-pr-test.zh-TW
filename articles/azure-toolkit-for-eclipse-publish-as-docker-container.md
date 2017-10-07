---
title: "使用 Docker 容器 aaaPublish hello Azure Toolkit for Eclipse |Microsoft 文件"
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Docker 容器發行 web 應用程式使用 hello Azure Toolkit for Eclipse

Docker 容器是常見的 Web 應用程式部署方法。 藉由使用 Docker 容器，開發人員可以將合併所有的專案檔和成單一封裝的部署 tooa 伺服器的相依性。 hello Azure Toolkit for Eclipse 的 Java 開發人員簡化此程序，藉由新增*發佈為 Docker 容器*部署 tooMicrosoft Azure 的功能。 本文將告訴您透過 hello 步驟需要 toopublish 應用程式 tooAzure 做為 Docker 容器。

> [!NOTE]
> Docker 的詳細資訊位於 hello [Docker 網站]。
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>使用 Docker 容器發行您的 web 應用程式 tooAzure

1. 在 Eclipse 中開啟 web 應用程式專案。

2. toostart hello**發佈為 Docker 容器**精靈 中，執行 hello 下列其中一項：

   * 在 hello**導覽**檢視，以滑鼠右鍵按一下您的專案，請按一下**Azure**，然後按一下**發佈為 Docker 容器**。

      ![導覽器檢視 [發佈作為 Docker 容器] 命令][PUB01]

   * Hello Eclipse 工具列上，按一下 hello**發行**按鈕，然後再按一下**發佈為 Docker 容器**。

      ![Eclipse 工具列 [發佈作為 Docker 容器] 命令][PUB02]
      
    hello**在 Azure 上部署 Docker 容器**精靈 隨即開啟。

    ![hello Azure 精靈上部署 Docker 容器][PUB03]

3. 在 hello**輸入映像名稱選取 hello 成品路徑，請檢查使用 Docker 主機 toobe**視窗中，請勿遵循 hello:

    a. 在 hello **Docker 映像名稱**方塊中，輸入您的 Docker 主機的唯一名稱。 （hello 精靈會自動建立一個名稱，但您可以修改它）。

    b. hello**主機**區域會顯示您已經建立任何 Docker 主機。 執行 hello 下列其中一項：

    * 如果您有現有的 Docker 主機，您可以部署您的 web 應用程式 tooit。
    * 按一下 新的 Docker 主機，toocreate**新增**。  
      
    hello**建立 Docker 主機**對話方塊隨即開啟。

    ![[在 Azure 上部署 Docker 容器] 精靈][PUB04a]

4. 在 hello **hello 新虛擬機器設定**視窗中，指定下列選項，為您的 Docker 主機 hello。 （hello 精靈會自動產生大部分的 hello 選項，但您可以修改任何其中）。

   a. **名稱**： 輸入 hello Docker 主機的唯一名稱。 （它是不 hello 與 hello 您稍早指定的 Docker 映像名稱相同）。

   b. **訂用帳戶**： 輸入 hello 您為您的主機使用的 Azure 訂用帳戶。

   c. **區域**： 輸入 hello 主機所在的地理區域。

   d. 在 [hello**主機作業系統和大小**] 索引標籤：
     * **主機作業系統**: hello 虛擬機器，其中包含您的主機輸入 hello 作業系統。
     * **大小**： 輸入您的主機 hello 虛擬機器大小。

   e. 在 [hello**資源群組**] 索引標籤：
     * **新的資源群組**︰為主機建立新的資源群組。
     * **現有的資源群組**︰輸入 Azure 帳戶中的現有資源群組。

   f. 在 [hello**網路**] 索引標籤：
     * **新的虛擬網路**︰為主機建立新的虛擬網路。
     * **現有的虛擬網路**︰輸入 Azure 帳戶中的現有虛擬網路。

   g. 在 [hello**儲存體**] 索引標籤：
     * **新的儲存體帳戶**︰為主機建立新的儲存體帳戶。
     * **現有的儲存體帳戶**︰輸入 Azure 帳戶中的現有儲存體帳戶。

5. 按一下 [下一步] 。

6. 在 [hello**設定記錄檔中的認證和連接埠設定**] 視窗中，選取其中一個 hello 下列選項：

    * **從 Azure Key Vault 匯入認證**︰指定先前儲存在 Azure 訂用帳戶中的一組認證。

      >[!NOTE]
      >無法自動存取其他帳戶或服務主體共用 hello 訂用帳戶的 Azure 金鑰保存庫用來建立特定帳戶或服務主體。 tooallow 另一個帳戶或服務主體 toouse hello 金鑰保存庫，您必須使用 hello Azure 入口網站 tooadd hello 帳戶或服務主體。

    * **新的登入認證**︰建立一組新的登入認證。 如果您選取此選項時，請勿 hello 遵循：
    
      * 在 hello **VM 認證**索引標籤上，選擇 hello 下列其中一種 hello 的 Docker 主機的虛擬機器登入認證的選項：

          * **使用者名稱**： 輸入您的虛擬機器的登入認證 hello 使用者名稱。
          * **密碼**和**確認**: hello 密碼輸入您的虛擬機器的登入認證。
          * **SSH**： 輸入 hello 安全殼層 (SSH) 設定為您的 Docker 主機。 您可以選擇下列選項的 hello:
            * **無**︰指定虛擬機器將不允許 SSH 連線。
            * **自動產生**： 會自動建立必要設定 hello 透過 SSH 的連接。
            * **從目錄匯入**︰指定內含一組先前儲存之 SSH 設定的目錄。 hello 目錄必須包含下列兩個檔案的 hello:
                * *id_rsa*： 包含 hello RSA 識別使用者。
                * *id_rsa.pub*: hello RSA 公開金鑰是用來驗證。
        
        ![建立 Docker 主機][PUB05]

      * 在 hello **Docker Daemon 認證**索引標籤上，指定下列選項的 hello:

          * **Docker 精靈通訊埠**： 輸入您的 Docker 主機 hello 唯一的 TCP 連接埠。
          * **TLS 安全性**： 輸入您的 Docker 主機的 hello 傳輸層安全性設定。 您可以選擇下列選項的 hello:
            * **無**︰指定虛擬機器將不允許 TLS 連線。
            * **自動產生**： 會自動建立必要設定 hello 透過 TLS 連線。
            * **從目錄匯入**︰指定內含一組先前儲存之 TLS 設定的目錄。 更具體來說，hello 目錄必須包含下列六個檔案的 hello:
                * *ca.pem*和*ca key.pem*： 包含 hello 憑證和公開金鑰 hello TLS 憑證授權單位。
                * *cert.pem*和*key.pem*： 包含 hello 用戶端憑證和公開金鑰用於 TLS 驗證。
                * *server.pem*和*伺服器 key.pem*： 包含 hello 伺服器憑證和公開金鑰 hello 主機。

        ![建立 Docker 主機][PUB06]

7. 輸入所有 hello 上述資訊之後，請按一下**完成**。

8. 在 hello**在 Azure 上部署 Docker 容器**精靈 中，按一下**下一步**。

   ![hello Azure 精靈上部署 Docker 容器][PUB07]

9. 在 hello**設定建立 hello Docker 容器 toobe**視窗中，執行下列 hello:

   a. 在 hello **Docker 容器名稱**方塊中，輸入您的 Docker 容器的唯一名稱。

   b. 選擇其中一個 hello 遵循 Docker 映像：
     * **預先定義的 Docker 映像**︰指定 Azure 中的既存 Docker 映像。

       >[!NOTE]
       >包含數個映像的 Docker 映像，在此方塊中的 hello 清單已使用 Azure Toolkit 該 hello 設定 toopatch，使您的成品會自動進行部署。

     * **自訂 Dockerfile**︰指定本機電腦中先前儲存的 Dockerfile。

       >[!NOTE]
       >這是開發人員希望 toodeploy 自己 Dockerfile 的更進階的功能。 不過，是由使用其 Dockerfile 已正確建置此選項 tooensure toodevelopers。 hello Azure Toolkit 不會驗證 hello 內容中自訂 Dockerfile 中，因此如果 hello Dockerfile 有問題，hello 部署可能會失敗。 此外，hello Azure Toolkit 預期自訂 Dockerfile toocontain hello 的 web 應用程式成品，並會 tooopen HTTP 連接。 如果開發人員發佈不同類型的構件，他們可能會在部署後收到無關緊要的錯誤。

   c. **連接埠設定**： 輸入 hello 唯一的 TCP 連接埠繫結的 Docker 容器。

     ![hello 設定 hello Docker 容器 toobe 建立視窗][PUB08]

10. 您已完成所有 hello 先前步驟之後，請按一下**完成**。

hello Azure Toolkit 開始部署您的 Docker 容器中的 web 應用程式 tooAzure。 

## <a name="next-steps"></a>後續步驟
針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列資源的 hello:

* [適用於 Eclipse 的 Azure 工具組]
  * [在 hello Azure Toolkit for Eclipse 中最新消息]
  * [安裝 Azure Toolkit for Eclipse hello]
  * [登入指示 hello Azure Toolkit for Eclipse]
  * [在 Eclipse 中建立 Azure Hello World Web 應用程式]
* [Azure Toolkit for IntelliJ]
  * [在 hello Azure Toolkit for IntelliJ 最新消息]
  * [安裝 hello Azure Toolkit for IntelliJ]
  * [登入的指示 hello Azure Toolkit for IntelliJ]
  * [在 IntelliJ 中建立 Azure Hello World Web 應用程式]

如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。

如需對 Docker 的其他資源，請參閱 hello 官方[Docker 網站]。

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[登入指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[登入的指示 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[在 hello Azure Toolkit for Eclipse 中最新消息]: ./azure-toolkit-for-eclipse-whats-new.md
[在 hello Azure Toolkit for IntelliJ 最新消息]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/

[Docker 網站]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png