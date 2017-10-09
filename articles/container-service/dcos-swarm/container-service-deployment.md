---
title: "在 Azure 中叢集 aaaDeploy Docker 容器 |Microsoft 文件"
description: "Kubernetes、 DC/作業系統，或 Docker Swarm Azure 容器服務中使用來部署方案 hello Azure 入口網站或 Resource Manager 範本。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>部署 Docker 容器主機使用 hello Azure 入口網站的解決方案



Azure Container Service 支援快速部署常用的開放原始碼容器叢集和協調流程解決方案。 這份文件會引導您使用 hello Azure 入口網站或 Azure Resource Manager 快速入門範本部署與 Azure 容器服務的叢集。 

您也可以部署與 Azure 容器服務的叢集使用 hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)或 hello Azure 容器服務 Api。

若為背景，請參閱 [Azure Container Service 簡介](../container-service-intro.md)。


## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**：如果您沒有帳戶，請註冊[免費試用](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)。 針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。

    > [!NOTE]
    > 您的 Azure 訂用帳戶使用量和[資源配額](../../azure-subscription-service-limits.md)，例如核心配額，可以限制 hello 您部署的 hello 叢集大小。 toorequest 增加配額，開啟[線上客戶支援要求](../../azure-supportability/how-to-create-azure-support-request.md)不收費。
    >

* **SSH RSA 公開金鑰**： 部署時透過 hello 入口網站或一個 hello Azure 快速入門範本，您必須 tooprovide hello 公開金鑰來驗證對 Azure 容器服務的虛擬機器。 toocreate 安全殼層 (SSH) 的 RSA 金鑰，請參閱 hello [OS X 和 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md)或[Windows](../../virtual-machines/linux/ssh-from-windows.md)指引。 

* **服務主體的用戶端識別碼和密碼**(只有 Kubernetes): 如需詳細資訊和指導方針 toocreate Azure Active Directory 服務主體，請參閱[hello Kubernetes 叢集的服務主體相關](../kubernetes/container-service-kubernetes-service-principal.md)。



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站中建立叢集
1. 選取 登入 Azure 入口網站 toohello**新增**，並搜尋 hello Azure Marketplace 中的**Azure 容器服務**。

    ![Marketplace 中的 Azure Container Service](./media/container-service-deployment/acs-portal1.png)  <br />

2. 按一下 [Azure Container Service]，然後按一下 [建立]。

3. 在 hello**基本概念**刀鋒視窗中，輸入下列資訊的 hello:

    * **Orchestrator**： 選取其中一個 hello 容器 orchestrators toodeploy hello 叢集上。
        * **DC/OS**：部署 DC/OS 叢集。
        * **Swarm**：部署 Docker Swarm 叢集。
        * **Kubernetes**：部署 Kubernetes 叢集。
    * **訂用帳戶**：選取 Azure 訂用帳戶。
    * **資源群組**： 輸入新的資源群組的 hello 部署 hello 名稱。
    * **位置**： 選取 hello Azure 容器服務部署的 Azure 區域。 如需可用性，請查看[依區域提供的產品](https://azure.microsoft.com/regions/services/)。
    
    ![基本設定](./media/container-service-deployment/acs-portal3.png)  <br />
    
    按一下**確定**當您準備好 tooproceed。

4. 在 hello**主要組態**刀鋒視窗中，輸入下列 hello Linux 主要節點或節點 （部分設定都是特定 tooeach orchestrator） 的 hello 叢集中設定的 hello:

    * **主要 DNS 名稱**: hello 使用前置詞 toocreate 唯一完整網域名稱 (FQDN) 的 hello master。 主要 FQDN 是 hello 表單的 hello*前置詞*管理*位置*。 cloudapp.azure.com。
    * **使用者名稱**: hello hello 叢集中的 hello Linux 虛擬機器的每個帳戶的使用者名稱。
    * **SSH RSA 公開金鑰**： 新增 hello 公用金鑰 toobe 用於驗證 hello Linux 虛擬機器。 請務必此機碼包含沒有分行符號，並包含 hello`ssh-rsa`前置詞。 hello`username@domain`是選擇性的後置。 hello 機碼看起來應該類似下列 hello: **...ssh rsa AAAAB3Nz <>......UcyupgH azureuser@linuxvm** 。 
    * **服務主體**： 如果您選取 hello Kubernetes orchestrator，請輸入 Azure Active Directory**服務主體的用戶端識別碼**（也稱為 hello appId） 和**服務主體的用戶端密碼**（密碼）。 如需詳細資訊，請參閱[hello Kubernetes 叢集的服務主體相關](../kubernetes/container-service-kubernetes-service-principal.md)。
    * **主要計數**: hello hello 叢集中的主機數目。
    * **VM 診斷**： 針對某些 orchestrators，您可以啟用 hello 母片上的 VM 診斷。

    ![主要組態](./media/container-service-deployment/acs-portal4.png)  <br />

    按一下**確定**當您準備好 tooproceed。

5. 在 hello**代理程式設定**刀鋒視窗中，輸入下列資訊的 hello:

    * **代理程式計數**： 如需 Docker 群集和 Kubernetes，這個值會是 hello 的 hello 代理程式規模集中的代理程式的初始數目。 DC/作業系統，對於 hello 的私用規模集中的代理程式的初始數目。 此外，也會建立 DC/OS 的公用擴展集，其中包含預先決定的代理程式數目。 hello 這個公用的規模集中的代理程式數目取決於 hello hello 叢集中的主機數目： 一個主要，一個公用代理程式和三個或五個主機的兩個公用的代理程式。
    * **代理程式的虛擬機器大小**: hello hello 代理程式的虛擬機器的大小。
    * **作業系統**： 此設定為目前選取 hello Kubernetes orchestrator 時，才可以使用。 選擇 Linux 散發套件或 Windows Server 作業系統 toorun hello 代理程式上。 此設定會決定您的叢集可以執行 Linux 或 Windows 容器應用程式。 

        > [!NOTE]
        > 對於 Kubernetes 叢集，Windows 容器支援處於預覽階段。 在 DC/OS 和 Swarm 叢集上，Azure Container Service 中目前只支援 Linux 代理程式。

    * **代理程式認證**： 如果您選取 hello Windows 作業系統，請輸入系統管理員**使用者名**和**密碼**hello 代理程式 」 的 Vm。 

    ![代理程式組態](./media/container-service-deployment/acs-portal5.png)  <br />

    按一下**確定**當您準備好 tooproceed。

6. 服務驗證完成後請按一下 [確定]。

    ![驗證](./media/container-service-deployment/acs-portal6.png)  <br />

7. 檢閱 hello 條款。 toostart hello 部署程序中，按一下 **建立**。

    如果您已選擇 toopin hello 部署 toohello Azure 入口網站，您可以看到 hello 部署狀態。

    ![部署狀態](./media/container-service-deployment/acs-portal8.png)  <br />

hello 部署需要數分鐘 toocomplete。 然後，hello Azure 容器服務叢集可供使用。


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>使用快速入門範本建立叢集
Azure 快速入門範本是可用 toodeploy Azure 容器服務中的叢集。 hello 提供快速入門範本可以修改的 tooinclude 額外或進階 Azure 組態。 toocreate 利用 Azure 快速入門範本與 Azure 容器服務的叢集，您需要 Azure 訂用帳戶。 如果您沒有訂用帳戶，請註冊[免費試用](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935)。 

請遵循這些步驟 toodeploy 叢集中使用的範本和 hello Azure CLI 2.0 (請參閱[安裝和設定指示](/cli/azure/install-az-cli2))。

> [!NOTE] 
> 如果您在 Windows 系統上，您可以使用類似步驟 toodeploy 範本，使用 Azure PowerShell。 請參閱本節稍後的步驟。 您也可以部署範本，以透過 hello[入口網站](../../azure-resource-manager/resource-group-template-deploy-portal.md)或其他方法。

1. toodeploy DC/OS、 Docker Swarm，或 Kubernetes 叢集中，會選取其中一個 hello 可用的快速入門範本從 GitHub。 部分清單如下。 hello DC/OS 和群集範本是 hello 相同，除了 hello 預設 orchestrator 選取項目。

    * [DC/OS 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. 登入 Azure 帳戶 tooyour (`az login`)，並確定該 hello Azure CLI 連線的 tooyour Azure 訂用帳戶。 您可以使用下列命令的 hello 看到 hello 預設訂用帳戶：

    ```azurecli
    az account show
    ```
    
    如果您有一個以上的訂用帳戶，以及需要 tooset 不同的預設訂用帳戶，執行`az account set --subscription`並指定 hello 訂用帳戶識別碼或名稱。

3. 最佳做法，請將新的資源群組用於 hello 部署。 toocreate 資源群組、 使用 hello`az group create`命令指定的資源群組名稱和位置： 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. 建立 JSON 檔案包含 hello 所需的範本參數。 下載 hello 參數檔名為`azuredeploy.parameters.json`，伴隨著 hello Azure 容器服務範本`azuredeploy.json`GitHub 中。 輸入您叢集所需的參數值。 

    例如，toouse hello [DC/OS 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)，提供的參數值`dnsNamePrefix`和`sshRSAPublicKey`。 請參閱中的 hello 描述`azuredeploy.json`及其他參數的選項。  
 

5. 建立容器服務叢集藉由傳遞 hello 部署參數檔案以 hello 下列命令，其中：

    * **RESOURCE_GROUP** hello hello hello 先前步驟中所建立的資源群組名稱。
    * **DEPLOYMENT_NAME** （選擇性） 是提供 toohello 部署的名稱。
    * **TEMPLATE_URI** hello hello 部署檔案的位置`azuredeploy.json`。 此 URI 必須是 hello 未經處理的檔案，不指標 toohello GitHub UI。 toofind 此 URI，選取 hello`azuredeploy.json`檔案在 GitHub 中，然後按一下 hello **Raw**  按鈕。  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    您也可以提供參數以 JSON 格式的字串 hello 命令列上。 使用類似 toohello 下列命令：

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > hello 部署需要數分鐘 toocomplete。
    > 

### <a name="equivalent-powershell-commands"></a>對等的 PowerShell 命令
您也可以使用 PowerShell 部署 Azure Container Service 叢集範本。 這份文件以 hello 1.0 版根據[Azure PowerShell 模組](https://azure.microsoft.com/blog/azps-1-0/)。

1. toodeploy DC/OS、 Docker Swarm，或 Kubernetes 叢集中，會選取其中一個 hello 可用的快速入門範本從 GitHub。 部分清單如下。 請注意，hello DC/OS 和群集範本是 hello 相同，與 hello 例外狀況的 hello 預設 orchestrator 選取項目。

    * [DC/OS 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Swarm 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Kubernetes 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. 之前在您的 Azure 訂用帳戶中建立叢集，確認您的 PowerShell 工作階段具有已登入 tooAzure。 您可以以 hello`Get-AzureRMSubscription`命令：

    ```powershell
    Get-AzureRmSubscription
    ```

3. 如果您需要 toosign tooAzure 中的，使用 hello`Login-AzureRMAccount`命令：

    ```powershell
    Login-AzureRmAccount
    ```

4. 最佳做法，請將新的資源群組用於 hello 部署。 toocreate 資源群組、 使用 hello`New-AzureRmResourceGroup`命令，並指定資源群組名稱和目的地區域：

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. 建立資源群組之後，您可以使用下列命令的 hello 建立您的叢集。 hello hello URI 需要範本會指定以 hello`-TemplateUri`參數。 當您執行此命令時，PowerShell 會提示您輸入部署參數值。

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>提供範本參數
如果您熟悉 PowerShell，您知道您可以輸入減號 （-），然後按 hello TAB 鍵循環 hello 可用 cmdlet 的參數。 相同的功能也適用於您在範本中定義的參數。 只要您輸入 hello 範本名稱，hello cmdlet 提取 hello 範本、 剖析 hello 參數，並以動態方式加入 hello 範本參數 toohello 命令。 這使得輕鬆 toospecify hello 範本參數的值。 如果您忘記必要的參數值時，PowerShell 會提示您輸入 hello 值。

以下是 hello 完整命令，以包含的參數。 Hello 資源名稱的 hello 提供您自己的值。

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>後續步驟
既然您有一個可運作的叢集，請參閱這些文件來了解連接和管理的詳細資料：

* [Tooan Azure 容器服務叢集連線](../container-service-connect.md)
* [使用 Azure Container Service 和 DC/OS](container-service-mesos-marathon-rest.md)
* [使用 Azure Container Service 和 Docker Swarm](container-service-docker-swarm.md)
* [使用 Azure Container Service 和 Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)
