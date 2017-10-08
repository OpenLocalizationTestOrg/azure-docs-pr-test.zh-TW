---
title: "aaaPublish Docker 容器使用 hello Azure Toolkit for IntelliJ |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit IntelliJ。"
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
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>使用 IntelliJ hello Azure Toolkit Docker 容器發行 web 應用程式

Docker 容器是常見的 Web 應用程式部署方法。 藉由使用 Docker 容器，開發人員可以將合併所有的專案檔和成單一封裝的部署 tooa 伺服器的相依性。 hello Azure Toolkit for IntelliJ Java 開發人員簡化此程序，藉由新增*發佈為 Docker 容器*部署 tooMicrosoft Azure 的功能。 本文將告訴您透過 hello 步驟需要 toopublish 應用程式 tooAzure 做為 Docker 容器。

> [!NOTE]
>
> Docker 的詳細資訊位於 hello [Docker 網站]。
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>使用 Docker 容器發行您的 web 應用程式 tooAzure

> [!NOTE]
> * toopublish 您 web 應用程式中，您必須建立可供部署的成品。 toolearn 詳細資訊，請參閱 hello[建立成品的其他資訊](#artifacts)> 一節。
>
> * 您至少一次完成 hello 部署精靈 之後，大部分的設定會使用預設執行 hello 精靈時。
>

1. 在 IntelliJ 中開啟 web 應用程式專案。

2. toostart hello**發佈為 Docker 容器**精靈 中，執行 hello 下列其中一項：

   * 在 hello**專案**工具視窗，以滑鼠右鍵按一下您的專案，按一下  **Azure**，然後按一下**發佈為 Docker 容器**:

      ![hello 發佈為 Docker 容器命令][PUB01]

   * Hello IntelliJ 工具列上，按一下 hello**發佈群組**按鈕，然後再按一下**發佈為 Docker 容器**:

      ![hello 發佈為 Docker 容器命令][PUB02]  
    hello**在 Azure 上部署 Docker 容器**精靈 隨即開啟。

   ![hello Azure 精靈上部署 Docker 容器][PUB03]

3. 在 hello**輸入映像名稱選取 hello 成品路徑，請檢查使用 Docker 主機 toobe**視窗中，請勿遵循 hello: 

   a. 在 hello **Docker 映像名稱**方塊中，輸入您的 Docker 主機的唯一名稱。 （hello 精靈會自動建立一個名稱，但您可以修改它）。 

   b. hello**主機**區域會顯示您已經建立任何 Docker 主機。 執行 hello 下列其中一項： 
      * 如果您有現有的 Docker 主機，您可以部署您的 web 應用程式 tooit。
      * toocreate Docker 主機時，按一下 hello 綠色加號 (**+**)。  
       hello**建立 Docker 主機**對話方塊隨即開啟。 

      ![[在 Azure 上部署 Docker 容器] 精靈][PUB04a]

4. 在 hello **hello 新虛擬機器設定**視窗中，提供 hello 下列 Docker 主機的相關資訊。 （hello 精靈會自動產生大部分的 hello 資訊，但您可以修改任何其中）。 

   a. 在 hello**名稱**方塊中，輸入 hello Docker 主機的唯一名稱。 （它是不 hello 與 hello 您稍早指定的 Docker 映像名稱相同）。 
    
   b. 在 hello**訂用帳戶**方塊中，輸入 hello 您為您的主機使用的 Azure 訂用帳戶。 
      
   c. 在 hello**區域**方塊中，輸入您的主機所在的 hello 地理區域。
      
   d. 在 hello **OS 和大小**索引標籤上，執行下列 hello:      
      * **主機作業系統**: hello 虛擬機器，其中包含您的主機輸入 hello 作業系統。 
      * **大小**： 輸入您的主機 hello 虛擬機器大小。   
       
   e. 在 hello**資源群組**索引標籤上，選取其中一個 hello 下列：      
      * **新的資源群組**︰為主機建立資源群組。
      * **現有的資源群組**︰指定 Azure 帳戶中的現有資源群組。 
       
   f. 在 hello**網路**索引標籤上，選取其中一個 hello 下列：      
      * **新的虛擬網路**︰為主機建立虛擬網路。
      * **現有的虛擬網路**︰指定 Azure 帳戶中的現有虛擬網路。 
       
   g. 在 hello**儲存體**索引標籤上，選取其中一個 hello 下列：      
      * **新的儲存體帳戶**︰為主機建立儲存體帳戶。
      * **現有的儲存體帳戶**︰指定 Azure 帳戶中的現有儲存體帳戶。
       
5. 按一下 [下一步] 。  
     hello**設定記錄檔中的認證和連接埠設定**視窗隨即開啟。

      ![hello 設定登入認證和連接埠設定 視窗][PUB05]

6. 選取其中一個 hello 下列選項：

      * **從 Azure Key Vault 匯入認證**︰指定先前儲存的一組認證，這些認證儲存在 Azure 訂用帳戶中。

          > [!NOTE]
          > 無法自動存取其他帳戶或服務主體共用 hello 訂用帳戶的 Azure 金鑰保存庫用來建立特定帳戶或服務主體。 tooallow 另一個帳戶或服務主體 toouse hello 金鑰保存庫，您必須使用 hello Azure 入口網站 tooadd hello 帳戶或服務主體。

      * **新的登入認證**︰建立一組新的登入認證。 如果您選取此選項時，請勿 hello 遵循：

        a. 在 hello **VM 認證**索引標籤上，提供下列資訊 hello 虛擬機器的登入認證您的 Docker 主機 hello: * **Username**: hello 使用者名稱輸入虛擬機器登入認證。
             * **密碼**和**確認**: hello 密碼輸入您的虛擬機器的登入認證。
             * **SSH**： 輸入 hello 安全殼層 (SSH) 設定為您的 Docker 主機。 您可以選取其中一個 hello 下列選項: ***無**： 指定您的虛擬機器不允許 SSH 連線。
                * **自動產生**： 會自動建立必要設定 hello 透過 SSH 的連接。
                * **從目錄匯入**： 可讓您 toospecify 包含一組先前儲存的 SSH 設定的目錄。 hello 目錄必須包含下列兩個檔案的 hello:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. 在 hello **Docker Daemon 存取**索引標籤上，提供下列資訊的 hello:

          ![建立 Docker 主機][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. 您輸入 hello 所需的資訊之後，請按一下**完成**。  
    hello**在 Azure 上部署 Docker 容器**精靈隨即再度出現。

   ![[在 Azure 上部署 Docker 容器] 精靈][PUB07]

8. 按一下 [下一步] 。  
    hello**設定建立 hello Docker 容器 toobe**視窗隨即開啟。

   ![hello 設定 hello Docker 容器 toobe 建立視窗][PUB08]

9. 在 hello**設定建立 hello Docker 容器 toobe**視窗中，提供下列資訊的 hello: 

   a. 在 hello **Docker 容器名稱**方塊中，輸入您的 Docker 容器的唯一名稱。

   b. 選擇其中一個 hello 遵循 Docker 映像： 

      * **預先定義的 Docker 映像**︰指定 Azure 中的既存 Docker 映像。 

        > [!NOTE]
        > 包含數個映像的 Docker 映像，在此方塊中的 hello 清單已使用 Azure Toolkit 該 hello 設定 toopatch，使您的成品會自動進行部署。 

      * **自訂 Dockerfile**︰指定本機電腦中先前儲存的 Dockerfile。

        > [!NOTE]
        > 這是開發人員希望 toodeploy 自己 Dockerfile 的更進階的功能。 不過，是由使用其 Dockerfile 已正確建置此選項 tooensure toodevelopers。 Hello Azure 工具組不會驗證自訂 Dockerfile 中的 hello 內容，因為如果 hello Dockerfile 有問題 hello 部署可能會失敗。 此外，由於 hello Azure Toolkit 預期 hello 自訂 Dockerfile toocontain web 應用程式成品，它會嘗試 tooopen HTTP 連接。 如果開發人員發佈不同類型的構件，他們可能會在部署後收到無關緊要的錯誤。

   c. 在 hello**連接埠設定**方塊中，輸入 hello 唯一的 TCP 連接埠繫結的 Docker 容器。 

10. 您已完成 hello 先前步驟之後，請按一下**完成**。 

hello Azure Toolkit 開始部署您的 Docker 容器中的 web 應用程式 tooAzure。 除非您已設定部署在 hello 背景 IntelliJ toobe**部署 tooAzure**進度列顯示。 

![hello 部署進度列][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>建立構件的其他資訊

toocreate 可供部署的成品，請勿 hello 遵循：

1. 在 IntelliJ 中開啟 web 應用程式專案。

2. 依序按一下 [檔案] 及 [專案結構]。

   ![hello 專案結構命令][ART01]

3. tooadd 的成品，按一下 hello 綠色加號 (**+**)，然後按一下 **Web 應用程式： 封存**。

   ![hello 「 Web 應用程式:: 封存 」 命令][ART02]

4. 在 hello**名稱**方塊中，輸入您的成品名稱 (不包括 hello *.war*延伸模組)，然後按一下 **[確定]**。

   ![hello 成品名稱 方塊][ART03]

如需在 IntelliJ 中建立成品的詳細資訊，請參閱[設定成品]hello JetBrains 網站上。

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

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

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
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/

[Docker 網站]: https://www.docker.com/
[設定成品]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
