---
title: "aaaCI/CD 從 Jenkins tooAzure Team Services 的 Vm |Microsoft 文件"
description: "設定持續整合 (CI) 和使用 Visual Studio Team Services (VSTS) 或 Microsoft Team Foundation Server (TFS) 中的 Release Management 從 Jenkins tooAzure Vm Node.js 應用程式的連續部署 (CD)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a>部署您的應用程式 tooLinux Vm 使用 Jenkins 和 Team Services

持續整合 (CI) 與持續部署 (CD) 是讓您可以建置、發行和部署程式碼的管道。 Team Services 部署 tooAzure 提供一組完整、 全功能的 CI/CD 自動化工具。 Jenkins 是廣為使用的第三方 CI/CD 伺服器型工具，也提供 CI/CD 自動化。 您可以使用這兩個一起 toocustomize 如何傳遞您的雲端應用程式或服務。

在此教學課程中，您可以使用 Jenkins toobuild **Node.js web 應用程式**，和 Visual Studio Team Services toodeploy 它 tooa[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)包含 Linux 虛擬機器。

您將：

> [!div class="checklist"]
> * 在 Jenkins 中建置應用程式
> * 設定適用於 Team Services 整合的 Jenkins
> * Azure 虛擬機器建立 hello 部署群組
> * 建立設定 hello Vm，然後部署 hello 應用程式的發行定義

## <a name="before-you-begin"></a>開始之前

* 您需要存取 tooa Jenkins 帳戶。 如果您尚未建立 Jenkins 伺服器，請參閱 [Jenkins 文件](https://jenkins.io/doc/)。 

* 登入 tooyour Team Services 帳戶 (`https://{youraccount}.visualstudio.com`)。 
  您可以取得[免費的 Team Services 帳戶](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308)。

  > [!NOTE]
  > 如需詳細資訊，請參閱[tooTeam 服務連接](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services)。

* 如果您的 Team Services 帳戶中沒有個人存取權杖 (PAT)，請建立一個。 Jenkins 需要此資訊 tooaccess Team Services 帳戶。
  讀取[如何適用於 Team Services 和 TFS 建立個人存取權杖](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)toolearn 如何 toogenerate 其中一個。

## <a name="get-hello-sample-app"></a>取得 hello 範例應用程式

您必須儲存在 Git 儲存機制的應用程式 toodeploy。
在本教學課程中，我們建議您使用[從 GitHub 中取得的此範例應用程式](https://github.com/azooinmyluggage/fabrikam-node)。

1. 建立此應用程式的 「 分叉 」，並記在本教學課程的後續步驟中使用的 hello 位置 (URL)。

1. 請 hello 分岔**公用**toosimplify 稍後連接 tooGitHub。

> [!NOTE]
> 如需詳細資訊，請參閱＜[建立存放庫的分支](https://help.github.com/articles/fork-a-repo/)＞和＜[將私密存放庫設為公用](https://help.github.com/articles/making-a-private-repository-public/)＞。

> [!NOTE]
> hello 應用程式使用建立[Yeoman](http://yeoman.io/learning/index.html); 它會使用**Express**， **bower**，和**grunt**; 而且它具有某些**npm**封裝做為相依性。
> hello 範例應用程式包含一組[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)，會使用的 toodynamically hello 虛擬機器部署在 Azure 上建立。 這些範本由工作在 hello [Team Services 發行定義](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions)。
> hello 主要範本會建立網路安全性群組、 虛擬機器和虛擬網路。 並指派公用 IP 位址和開啟輸入連接埠 80。 它也會加入 hello 部署群組太選取 hello 機器 tooreceive hello 部署使用的標記。
>
> hello 範例也包含可設定 Nginx hello 應用程式會將部署指令碼。 在每個 hello 虛擬機器上執行。 具體來說，hello 指令碼安裝節點、 Nginx 及 PM2;設定 Nginx 和 PM2;接著，啟動 hello 節點應用程式。

## <a name="configure-jenkins-plugins"></a>設定 Jenkins 外掛程式

首先，您必須設定兩個 Jenkins 外掛程式，用於 **NodeJS**，以及**與 Team Services 整合**。

1. 開啟您的 Jenkins 帳戶，然後選擇 [管理 Jenkins]。

1. 在 hello**管理 Jenkins**頁面上，選擇**管理外掛程式**。

1. 篩選 hello 清單 toolocate hello **NodeJS**外掛程式並將它安裝在不需重新啟動。

   ![加入 hello NodeJS 外掛程式 tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. 篩選 hello 清單 toofind hello **Team Foundation Server**外掛程式並安裝它。 (此外掛程式適用於 Team Services 和 Team Foundation Server。)不需要重新啟動 Jenkins。

## <a name="configure-jenkins-build-for-nodejs"></a>設定適用於 Node.js 的 Jenkins 組建

在 Jenkins 中建立新的組建專案並加以設定，如下所示：

1. 在 hello**一般**索引標籤上，輸入您建置專案的名稱。

1. 在 hello**原始程式碼管理**索引標籤上，選取**Git** ，然後輸入 hello 的 hello 儲存機制與 hello 分支包含應用程式程式碼的詳細資料。

   ![加入儲存機制 tooyour 組建](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > 如果您的儲存機制不是公用的請選擇**新增**並提供認證 tooconnect tooit。

1. 在 hello**組建觸發程序**索引標籤上，選取**輪詢 SCM** ，然後輸入 hello 排程`H/03 * * * *`toopoll hello Git 儲存機制，變更每隔三分鐘。 

1. 在 hello **Build Environment**索引標籤上，選取**提供節點&amp;npm bin / 資料夾路徑**輸入`NodeJS`hello JS 安裝節點值。 將 **npmrc 檔案**的設定保留為「使用系統預設值」。

1. 在 hello**建置**索引標籤上，輸入 hello 命令`npm install`tooensure 會更新所有相依性。

## <a name="configure-jenkins-for-team-services-integration"></a>設定適用於 Team Services 整合的 Jenkins

1. 在 hello**建置後動作**索引標籤上，針對**檔案 tooarchive**，輸入`**/*`tooinclude 所有檔案。

1. 如**觸發 TFS/Team Services 中的發行**，輸入您的帳戶 hello 完整的 URL (例如`https://your-account-name.visualstudio.com`)、 hello 專案名稱，hello （稍後建立） 的發行定義、 名稱和 hello 認證 tooconnect tooyour 帳戶。
   您需要使用者名稱及您稍早建立的 PAT hello。 

   ![設定 Jenkins 建置後動作](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. 儲存 hello 建置專案。

## <a name="create-a-jenkins-service-endpoint"></a>建立 Jenkins 服務端點

服務端點可讓 Team Services tooconnect tooJenkins。

1. 開啟 hello**服務**頁面在 Team Services 中，開啟 hello**新的服務端點**清單，並選擇**Jenkins**。

   ![新增 Jenkins 端點](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. 輸入您將使用 toorefer toothis 連接的名稱。

1. 輸入您的 Jenkins 伺服器 hello URL 和刻度 hello**接受不受信任的 SSL 憑證**選項。

1. Jenkins 帳戶輸入 hello 使用者名稱和密碼。

1. 選擇**驗證連線**toocheck 的 hello 資訊是否正確。

1. 選擇**確定**toocreate hello 服務端點。

## <a name="create-a-deployment-group"></a>建立部署群組

您需要[部署群組](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/)太包含 hello 虛擬機器。

1. 開啟 hello**版本**] 索引標籤的 hello**建置&amp;發行**集線器，然後開啟 hello**部署群組**索引標籤，然後選擇 [ **+ 新增**.

1. 輸入 hello 部署群組，以及選擇性的描述名稱。
   然後選擇 [建立]。

hello Azure 資源群組部署工作建立，並執行使用 hello Azure Resource Manager 範本時，登錄 hello Vm。
您不需要 toocreate 並自行註冊 hello 的虛擬機器。

## <a name="create-a-release-definition"></a>建立發行定義

發行定義指定 hello 處理 Team Services 將會執行 toodeploy hello 應用程式。
toocreate hello Team Services 中的發行定義：

1. 開啟 hello**版本** 索引標籤的 hello**建置&amp;釋放**集線器，開啟 hello  **+**  hello 清單的發行定義中的下拉式清單並選擇hello**建立發行定義**。 

1. 選取 hello**空**範本，然後選擇 **下一步**。

1. 在 hello**成品**區段中，按一下 上**連結成品**選擇**Jenkins**。 選取您的 Jenkins 服務端點連線。 然後選取 hello Jenkins 來源工作，並選擇 **建立**。 

1. 在 hello 新發行定義中，選擇**+ 加入工作**並加入**Azure 資源群組部署**工作 toohello 預設環境。

1. 選擇 hello 下拉式箭號下一步 toohello **+ 加入工作**連結並新增部署群組階段 toohello 定義。

   ![新增部署群組階段](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. 在 hello 工作目錄中，開啟 hello**公用程式**區段，並將執行個體的 hello**殼層指令碼**工作。

1. hello Azure 資源群組部署工作中使用的 hello 參數範本會設定 hello 系統管理員使用的密碼 tooconnect toohello Vm。
   您提供此密碼與 hello 變數**$(adminpassword)**:
   
   - 開啟 hello**變數**] 索引標籤，然後在 [hello**變數**區段中，輸入 hello 名稱`adminpassword`。

   - 輸入 hello 系統管理員密碼。

   - 選擇 hello 「 鎖 」 圖示下一步 toohello 值文字方塊 tooprotect hello 密碼。 

## <a name="configure-hello-azure-resource-group-deployment-task"></a>設定 hello Azure 資源群組部署工作

hello **Azure 資源群組部署**工作是使用的 toocreate hello 部署群組。 進行下列設定：

* **Azure 訂用帳戶：** hello 下方的清單中選取連接**可用的 Azure 服務連線**。 
  如果沒有連線出現，請選擇**管理**，選取**新的服務端點**然後**Azure Resource Manager**，依照 hello 提示。
  傳回 tooyour 發行定義，重新整理 hello **AzureRM 訂用帳戶**清單及選取 hello 所建立的連接。

* **資源群組**： 輸入您稍早建立的 hello 資源群組的名稱。

* **位置**： 選取 hello 部署的區域。

  ![建立新的資源群組](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* **範本位置**：`URL of hello file`

* **範本連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`

* **範本參數連結**：`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`

* **覆寫範本參數**: hello 的清單會覆寫值，例如： `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`。<br />插入您自己的 hello {預留位置} 的特定值。 

* **啟用必要條件**：`Configure with Deployment Group agent`

* **TFS/VSTS 端點**： 選擇**新增**，並在 hello [加入新的 Team Foundation Server/Team Services 連接] 對話方塊中，選取**權杖型驗證**。 輸入 hello 連接的名稱和您的 team 專案的 hello URL。 然後產生，並輸入[個人存取權杖 」 (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello 連接 tooyour team 專案。

  ![建立個人存取權杖](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* **Team 專案**：選取您目前的專案。

* **部署群組**： 輸入 hello 相同部署群組名稱，所使用的 hello**資源群組**參數。

hello hello Azure 資源群組部署工作的預設設定 toocreate 或因此以累加方式更新資源，以及 toodo。 hello 工作會建立 hello Vm hello 第一次執行時，之後就加以更新。

## <a name="configure-hello-shell-script-task"></a>設定 hello 殼層指令碼工作

hello**殼層指令碼**工作是使用的 tooprovide hello 組態指令碼 toorun 上每個伺服器 tooinstall Node.js 和開始 hello 應用程式。 進行下列設定：

* **指令碼路徑**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`

* **指定工作目錄**：`Checked`

* **工作目錄**：`$(System.DefaultWorkingDirectory)/Fabrikam-Node`
   
## <a name="rename-and-save-hello-release-definition"></a>重新命名並儲存 hello 發行定義

1. 編輯 hello hello 發行定義 toohello 名稱中指定名稱**建置後動作**hello Jenkins 組建 索引標籤。 Jenkins 在 hello 來源成品更新時需要此名稱 toobe 無法 tootrigger 新版本。

1. （選擇性） 按一下 hello 名稱變更 hello hello 環境名稱。 

1. 選擇 [儲存]，然後選擇 [確定]。

## <a name="start-a-manual-deployment"></a>啟動手動部署

1. 選擇 [+ 發行]，然後選取 [建立發行]。

1. 選取您已完成的 hello 組建 hello 反白顯示下拉式清單並選擇 **建立**。

1. 選擇 hello 快顯訊息中的 hello 發行連結。 例如：「發行「**發行-1**」已建立。」

1. 開啟 hello**記錄**toowatch hello 版本的主控台輸出索引標籤上。

1. 在瀏覽器中開啟 hello URL 的其中一部伺服器 hello 您加入 tooyour 部署群組。 例如，輸入 `http://{your-server-ip-address}`

## <a name="start-a-cicd-deployment"></a>啟動 CI/CD 部署

1. 在 hello 發行定義，請取消選取 hello**啟用**hello 中的核取方塊**控制選項**hello Azure 資源群組部署工作的 hello 設定一節。
   未來的部署 toohello 現有的部署群組，您不需要 toore-執行這項工作。

1. 請移 toohello 來源 Git 儲存機制，並修改 hello hello 內容**h1** hello 檔案中的標題[app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade)。

1. 認可變更。

1. 請稍候幾分鐘，您會看到 hello 中建立新的版本**版本**Team Services 或 TFS 的頁面。 開啟 hello 發行 toosee hello 部署正在進行中。 恭喜！

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以自動使用 Jenkins 組建和版本的 Team Services 應用程式 tooAzure hello 部署。 您已了解如何︰

> [!div class="checklist"]
> * 在 Jenkins 中建置應用程式
> * 設定適用於 Team Services 整合的 Jenkins
> * Azure 虛擬機器建立 hello 部署群組
> * 建立設定 hello Vm，然後部署 hello 應用程式的發行定義

前進 toohello 下一個教學課程 toolearn 有關 toodeploy （Linux、 Apache、 MySQL 和 PHP） LAMP 堆疊的方式的詳細資訊。

> [!div class="nextstepaction"]
> [部署 LAMP 堆疊](tutorial-lamp-stack.md)