---
title: "在 Azure 上的 Jenkins 伺服器 aaaCreate"
description: "Jenkins Azure Linux 虛擬機器上安裝從 hello Jenkins 解決方案範本和建置範例的 Java 應用程式。"
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>從 Azure 入口網站 hello Azure Linux VM 上建立 Jenkins 伺服器

本快速入門示範如何 tooinstall [Jenkins](https://jenkins.io) hello 工具和外掛程式設定 toowork Ubuntu Linux VM，使用 Azure 上。 當您完成時，您可讓在 Azure 中執行的 Jenkins 伺服器從 [GitHub](https://github.com) 建置範例 Java 應用程式。

## <a name="prerequisites"></a>必要條件

* Azure 訂用帳戶
* 電腦的命令列上的存取 tooSSH (例如 hello 撞殼層或[PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>建立 hello Jenkins VM 從 hello 方案範本

開啟 hello [marketplace 映像的 Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview)在 web 瀏覽器，然後選取**現在取得 IT**從左邊 hello 頁面 hello。 檢閱 hello 定價詳細資料，然後選取**繼續**，然後選取**建立**tooconfigure hello Jenkins 伺服器 hello Azure 入口網站中的。 
   
![Azure 入口網站對話方塊](./media/install-jenkins-solution-template/ap-create.png)

在 hello**設定基本設定**索引標籤上，填寫下列欄位的 hello:

![設定基本設定](./media/install-jenkins-solution-template/ap-basic.png)

* 使用 **Jenkins** 作為 [名稱]。
* 輸入 [使用者名稱]。 hello 使用者名稱必須符合[特定需求](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm)。
* 選取**密碼**為 hello**驗證類型**並輸入密碼。 hello 密碼必須包含大寫字元、 數字和一個特殊字元。
* 使用**myJenkinsResourceGroup** hello**資源群組**。
* 選擇 hello**美國東部** [Azure 地區](https://azure.microsoft.com/regions/)從 hello**位置**下拉式清單。

選取**確定**tooproceed toohello**設定額外選項** 索引標籤。請輸入唯一的網域名稱 tooidentify hello Jenkins 伺服器並選取**確定**。

![設定其他選項](./media/install-jenkins-solution-template/ap-addtional.png)  

 一旦驗證通過時，選取**確定**再次從 hello**摘要** 索引標籤。最後，選取**購買**toocreate hello Jenkins VM。 準備您的伺服器時，您會收到 hello Azure 入口網站中的通知：   

![Jenkins 已就緒通知](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>連接 tooJenkins

在網頁瀏覽器中，瀏覽 tooyour 虛擬機器 (例如，http://jenkins2517454.eastus.cloudapp.azure.com/)。 hello Jenkins 主控台是無法透過不安全的 HTTP 存取，因此 hello 頁面 tooaccess hello Jenkins 主控台上安全地從您的電腦使用 SSH 通道會提供指示。

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

設定使用 hello hello 通道`ssh`命令在 hello 頁面上，從 hello 命令列取代`username`hello hello hello 虛擬機器設定從 hello 方案範本時，請選擇先前的虛擬機器系統管理員使用者名稱。

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

啟動 hello 通道後，瀏覽 toohttp://localhost:8080 / 在本機電腦上。 

執行下列命令，透過 SSH toohello Jenkins VM 連線時，hello 命令列中的 hello 取得 hello 初始密碼。

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

解除鎖定 hello hello 的 Jenkins 儀表板第一次使用此初始密碼。

![將 Jenkins 解除鎖定](./media/install-jenkins-solution-template/jenkins-unlock.png)

選取**安裝建議的外掛程式**hello 在下一個頁面上，然後再建立 Jenkins 管理使用者使用 tooaccess hello Jenkins 儀表板。

![Jenkins 已就緒！](./media/install-jenkins-solution-template/jenkins-welcome.png)

hello Jenkins 伺服器現在是準備 toobuild 程式碼。

## <a name="create-your-first-job"></a>建立您的第一個作業

選取**建立新的作業**從 hello Jenkins 主控台，然後命名**mySampleApp**選取**Freestyle 專案**，然後選取**確定**。

![建立新的作業](./media/install-jenkins-solution-template/jenkins-new-job.png) 

選取 hello**原始程式碼管理**索引標籤上，啟用**Git**，並輸入下列 URL 中的 hello**儲存機制 URL**欄位：`https://github.com/spring-guides/gs-spring-boot.git`

![定義 hello Git 儲存機制](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

選取 hello**建置**索引標籤，然後選取**加入建置步驟**，**叫用的 Gradle 指令碼**。 選取 [使用 Gradle 包裝函式]，然後在 [包裝函式位置] 中輸入 `complete` 並輸入 `build` 作為 [工作]。

![使用 hello Gradle 包裝函式 toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

選取 [進階...] 然後輸入`complete`在 hello**根建置指令碼**欄位。 選取 [ **儲存**]。

![在 hello Gradle 包裝函式建置步驟中設定進階的設定](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>建置 hello 的程式碼

選取**現在建置**toocompile hello 程式碼和套件 hello 範例應用程式。 您的組建完成時，選取 hello**工作區**hello 專案的連結。

![瀏覽 toohello 區 tooget hello JAR 檔案從 hello 組建](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

瀏覽過`complete/build/libs`，並確定 hello`gs-spring-boot-0.1.0.jar`有 tooverify 組建是否成功。 您 Jenkins 伺服器現在已準備好 toobuild 自己在 Azure 中的專案。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [新增 Azure VM 作為 Jenkins 代理程式](jenkins-azure-vm-agents.md)
