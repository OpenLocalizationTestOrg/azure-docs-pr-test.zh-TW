---
title: "aaaDeploy 第一個應用程式 tooCloud Microsoft Azure 上 Foundry |Microsoft 文件"
description: "部署應用程式 tooCloud Foundry 在 Azure 上"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>部署第一個應用程式 tooCloud Foundry Microsoft Azure 上

[Cloud Foundry](http://cloudfoundry.org) 是 Microsoft Azure 上可用的熱門開放原始碼應用程式平台。 在本文中，我們會示範如何 toodeploy 及管理雲端 Foundry Azure 環境中的應用程式。

## <a name="create-a-cloud-foundry-environment"></a>建立 Cloud Foundry 環境

有幾個選項可以用來在 Azure 上建立 Cloud Foundry 環境：

- 使用 hello[關鍵雲端 Foundry 優惠][ pcf-azuremarketplace] hello Azure Marketplace toocreate 包含 PCF Ops Manager 和 hello Azure Service Broker 的標準環境中。 您可以找到[完成指示][ pcf-azuremarketplace-pivotaldocs]部署 hello marketplace 提供 hello 關鍵的文件中。
- 建立自訂的環境，方法是[手動部署 Pivotal Cloud Foundry][pcf-custom]。
- [直接部署 hello 開放原始碼雲端 Foundry 封裝][ oss-cf-bosh]藉由設定[BOSH](http://bosh.io)導向器，協調 hello Foundry 雲端環境的 hello 部署的 VM。

> [!IMPORTANT] 
> 如果您要部署 PCF hello Azure Marketplace 中，記下 hello SYSTEMDOMAINURL 和 tooaccess hello 關鍵應用程式管理員 中，這兩種指南所述 hello marketplace 部署所需的 hello 系統管理員認證。 它們是本教學課程所需的 toocomplete。 Marketplace 部署的 hello SYSTEMDOMAINURL 處於 hello 表單 https://system。*ip 位址*。 cf.pcfazure.com。

## <a name="connect-toohello-cloud-controller"></a>連接 toohello 雲端控制器

hello 雲端控制站是 hello 主要進入點 tooa 雲端 Foundry 環境來部署和管理應用程式。 hello 核心雲端控制站應用程式開發介面 (CCAPI) 是 REST API，但可透過各種工具存取。 在此情況下，我們藉此與其互動透過 hello[雲端 Foundry CLI][cf-cli]。 您可以安裝 hello CLI Linux、 MacOS、 或 Windows，但如果您想使用 tooinstall 它，並使用預先安裝在 hello [Azure 雲端殼層][cloudshell-docs]。

在中，toolog 前面加上`api`toohello SYSTEMDOMAINURL 您從 hello marketplace 部署取得。 因為 hello 預設部署伺服器使用自我簽署的憑證，您也應該包括 hello`skip-ssl-validation`切換。

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

您必須提示的 toolog toohello 雲端控制站中。 使用貴用戶取得 hello marketplace 部署步驟中的 hello 系統管理員帳戶認證。

提供雲端 Foundry*入*和*空格*做為命名空間 tooisolate hello 小組和環境中共用的部署。 hello PCF marketplace 部署包含 hello 預設*系統*組織一組的空間建立和 toocontain hello 基礎元件，例如 hello 自動調整服務和 hello Azure 的 service broker。 現在請選擇 hello*系統*空間。


## <a name="create-an-org-and-space"></a>建立組織和空間

如果您輸入`cf apps`，您會看到一組內 hello 系統 my.app hello 系統空間中已部署的系統應用程式 

您應該保留 hello*系統*組織保留給系統應用程式，因此建立組織及空間 toohouse 我們的範例應用程式。

```bash
cf create-org myorg
cf create-space dev -o myorg
```

使用 hello 目標命令 tooswitch toohello 新組織和空間：

```bash
cf target -o testorg -s dev
```

現在，當您部署應用程式時，它會自動建立在 hello 新組織及空間。 目前沒有的 tooconfirm hello 新組織/在空間中，沒有應用程式輸入`cf apps`一次。

> [!NOTE] 
> 如需入空格及如何使用它們以角色為基礎的存取控制 (RBAC) 的詳細資訊，請參閱 hello[雲端 Foundry 文件][cf-orgs-spaces-docs]。

## <a name="deploy-an-application"></a>部署應用程式

讓我們使用範例雲端 Foundry 應用程式呼叫 Hello Spring 雲端，這是以 Java 撰寫，且根據 hello [Spring 架構](http://spring.io)和[Spring 開機](http://projects.spring.io/spring-boot/)。

### <a name="clone-hello-hello-spring-cloud-repository"></a>複製 hello Hello Spring 雲端儲存機制

GitHub 上使用 hello Hello Spring 雲端範例應用程式。 複製它 tooyour 環境，並變更到新目錄中 hello:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>建置 hello 應用程式

組建 hello 應用程式使用[Apache Maven](http://maven.apache.org)。

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>部署 hello 與 cf 推入的應用程式

您可以部署大部分的應用程式 tooCloud Foundry 使用 hello`push`命令：

```bash
cf push
```

當您*發送*應用程式時，雲端 Foundry 會偵測 hello （在這個情況下，Java 應用程式） 的應用程式類型，並識別其相依性 （在此案例中的 hello Spring 架構）。 封裝的所有項目所需 toorun 您的程式碼的獨立容器映像，又稱為*droplet*。 最後，雲端 Foundry 排程 hello 其中一個環境中的 hello 可用電腦上的應用程式，並建立，您可能會達到，hello hello 命令輸出中所提供的 URL。

![cf push 命令的輸出][cf-push-output]

toosee hello hello spring 雲端應用程式，您的瀏覽器中開啟 hello 提供 URL:

![Hello Spring Cloud 的預設 UI][hello-spring-cloud-basic]

> [!NOTE] 
> 深入了解時會發生什麼事 toolearn `cf push`，請參閱[暫存應用程式如何][ cf-push-docs] hello 雲端 Foundry 文件中。

## <a name="view-application-logs"></a>檢視應用程式記錄

您可以使用應用程式的 hello 雲端 Foundry CLI tooview 記錄檔的名稱：

```bash
cf logs hello-spring-cloud
```

根據預設，hello 記錄命令使用*結尾*，其中會顯示新的記錄檔，當它們被寫入。 toosee 新記錄檔都會出現，請重新整理 hello 瀏覽器中的 hello hello spring 雲端應用程式。

tooview 記錄已經寫入、 新增 hello`recent`切換：

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>標尺 hello 應用程式

根據預設，`cf push` 只會建立應用程式的單一執行個體。 tooensure 高可用性和啟用向外延展的較高的輸送量，您通常想 toorun 多個應用程式的一個執行個體。 您可以輕鬆地向外擴充已部署的應用程式使用 hello`scale`命令：

```bash
cf scale -i 2 hello-spring-cloud
```

執行 hello `cf app` hello 應用程式上的命令會顯示雲端 Foundry 建立 hello 應用程式的另一個執行個體。 Hello 應用程式啟動之後，雲端 Foundry 會負載平衡流量 tooit 自動啟動。


## <a name="next-steps"></a>後續步驟

- [讀取 hello 雲端 Foundry 文件][cloudfoundry-docs]
- [設定雲端 Foundry hello Visual Studio Team Services 外掛程式][vsts-plugin]
- [設定雲端 Foundry hello Microsoft 記錄分析噴嘴][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png