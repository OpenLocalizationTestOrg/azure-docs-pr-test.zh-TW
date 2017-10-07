---
title: "在 Azure 中的 aaaPrivate Docker 容器登錄 |Microsoft 文件"
description: "簡介 toohello Azure 容器登錄 服務，提供雲端式管理的私人 Docker 登錄。"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>簡介 tooprivate Docker 容器登錄


Azure 容器登錄中是 managed [Docker 登錄](https://docs.docker.com/registry/)根據服務 hello 開放原始碼 Docker 登錄 2.0。 建立和維護 Azure 容器登錄 toostore 和管理您的私人[Docker 容器](https://www.docker.com/what-docker)映像。 容器登錄在 Azure 中的使用現有的容器開發與部署管線和 Docker 社群專業知識的 hello 主體上繪製。

如需有關 Docker 和容器的背景，請參閱︰

* [Docker 使用者指南](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>使用案例
提取映像從 Azure 容器登錄 toovarious 部署目標：

* **可調整的協調流程系統**，會管理整個主機叢集上容器化的應用程式，包括 [DC/OS](https://docs.mesosphere.com/)、[Docker Swarm](https://docs.docker.com/swarm/)、 [Kubernetes](http://kubernetes.io/docs/)。
* **Azure 服務**，會支援依規模建置和執行的應用程式，包括 [Container Service](../container-service/index.yml)、[App Service](/app-service/index.md)、[Batch](../batch/index.md)、[Service Fabric](/azure/service-fabric/) 和其他應用程式。

開發人員也可以推送 tooa 容器登錄中做為容器的開發工作流程的一部分。 例如，以容器登錄庫為目標，並以 [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) 或 [Jenkins](https://jenkins.io/) 等持續整合與部署工具為起點。





## <a name="key-concepts"></a>重要概念
* **登錄庫** - 在您的 Azure 訂用帳戶中建立一或多個容器登錄庫。 每個登錄支援標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)hello 中相同的位置。 利用本機、 網路關閉您的容器映像的儲存體藉由建立登錄在 hello 與您的部署相同的 Azure 位置。 完整的登錄名稱具有 hello 表單`myregistry.azurecr.io`。

  您[控制存取](container-registry-authentication.md)tooa 容器登錄中使用 Azure Active Directory 備份[服務主體](../active-directory/active-directory-application-objects.md)或提供的系統管理員帳戶。 執行標準的 hello`docker login`命令 tooauthenticate 登錄。

* **受管理登錄** - 為三個 SKU 中的登錄提供額外功能的層級 - 基本、標準和進階。 在這些 Sku 的 hello 影像會儲存在 hello Azure 容器登錄服務，因此可提高可靠性，並啟用新功能所管理的儲存體帳戶。 新功能包括 Webhook 整合、與 Azure Active Directory 的存放庫驗證，以及刪除功能支援。 使用者擁有 hello 選項 toochoose managed 的登錄或 toocreate 之間建立登錄時，他們自己的儲存體帳戶所支援的登錄。

* **儲存機制** - 登錄庫會包含一個或多個儲存機制，儲存機制是容器映像的群組。 Azure 容器登錄庫支援多層級的儲存機制命名空間。 這項功能可讓您 toogroup 集合的映像相關的 tooa 特定應用程式或應用程式 toospecific 開發或操作團隊的集合。 例如：

  * `myregistry.azurecr.io/aspnetcore:1.0.1` 表示全公司的映像
  * `myregistry.azurecr.io/warrantydept/dotnet-build`代表的映像使用 toobuild.NET 應用程式，請在 hello 擔保部門之間共用
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`代表 web 映像，分組在 hello 客戶提交應用程式中的 hello 擔保部門所擁有

* **映像** - 儲存在儲存機制中，每個映像是 Docker 容器的唯讀快照。 Azure 容器登錄庫可以包含 Windows 和 Linux 映像。 您可以控制您的所有容器部署的映像名稱。 使用標準[Docker 命令](https://docs.docker.com/engine/reference/commandline/)toopush 映像儲存機制，或提取從儲存機制的映像。

* **容器** - 容器定義軟體應用程式及其相依性，包裹在完整的檔案系統中，包括程式碼、執行階段、系統工具和程式庫。 根據您從容器登錄庫提取的 Windows 或 Linux 映像，執行 Docker 容器。 在單一機器上執行的容器共用 hello 作業系統核心。 Docker 容器是完全可攜 tooall 主要 Linux 散發版本、 Mac 和 Windows。




## <a name="next-steps"></a>後續步驟
* [建立容器登錄中使用 hello Azure 入口網站](container-registry-get-started-portal.md)
* [建立容器登錄中使用 Azure CLI hello](container-registry-get-started-azure-cli.md)
* [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
* toobuild 連續整合和部署工作流程使用 Visual Studio Team Services、 Azure 容器服務，以及 Azure 容器登錄中，請參閱[本教學課程](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md)。
* 如果要 tooset 自己 Docker 私人登錄在 Azure 中 （不含公用端點），請參閱[部署您自己私用 Docker 登錄在 Azure 上](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md)。
