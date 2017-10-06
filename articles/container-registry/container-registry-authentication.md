---
title: "Azure 容器登錄 aaaAuthenticate |Microsoft 文件"
description: "如何使用 Azure Active Directory tooan Azure 容器登錄中的 toolog 服務主體或系統管理員帳戶"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>向私用 Docker 容器登錄進行驗證
toowork 與 Azure 容器登錄中的容器映像，您使用登入 hello`docker login`命令。 您可以使用 **[Azure Active Directory 服務主體](../active-directory/active-directory-application-objects.md)**或登錄庫特定的**管理帳戶**登入。 本文提供關於這些身分識別的詳細資訊。



## <a name="service-principal"></a>服務主體

您可以[指派服務主體](container-registry-get-started-azure-cli.md#assign-a-service-principal)tooyour 登錄並使用基本的 Docker 驗證。 在大部分情況下，建議使用服務主體。 提供 hello 應用程式識別碼和密碼 hello 服務主體 toohello`docker login`命令時，hello 下列範例所示：

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

登入之後，Docker 會快取 hello 認證，因此您不需要 tooremember hello 應用程式識別碼。

> [!TIP]
> 如果您想，您可以執行重新產生服務主體的 hello 密碼 hello`az ad sp reset-credentials`命令。
>


服務主體允許[角色型存取](../active-directory/role-based-access-control-configure.md)tooa 登錄。 可用的角色如下：
  * 讀取者 (僅擁有提取存取權限)。
  * 投稿人 (提取和推送)。
  * 擁有者 （提取、 推送及指派角色 tooother 使用者）。

Azure Container Registry 無法進行匿名存取。 您可以使用[Docker 中樞](https://docs.docker.com/docker-hub/)存取公用映像。

您可以指派多個服務主體 tooa 登錄中，可讓您 toodefine 不同的使用者或應用程式的存取權。 服務主體也可讓開發人員或 DevOps 案例，例如 hello 遵循範例中的 「 遠端控制 」 連線 tooa 登錄：

  * 容器包括 DC/OS、 Docker Swarm 和 Kubernetes 登錄 tooorchestration 系統的部署。 您可以也提取容器登錄 toorelated Azure 服務例如[容器服務](../container-service/index.yml)， [App Service](../app-service/index.md)，[批次](../batch/index.md)， [Service Fabric](/azure/service-fabric/)，和其他人。

  * 連續整合及部署解決方案 （例如 Visual Studio Team Services 或 Jenkins） 會建立容器映像，並將其推送 tooa 登錄。





## <a name="admin-account"></a>管理帳戶
您建立的每個登錄，都會自動建立一個管理帳戶。 Hello 帳戶預設為停用，但您可以啟用它，並管理 hello 認證，例如透過 hello[入口網站](container-registry-get-started-portal.md#manage-registry-settings)或使用 hello [Azure CLI 2.0 命令](container-registry-get-started-azure-cli.md#manage-admin-credentials)。 每個管理帳戶會提供兩個可以重新產生的密碼。 hello 兩個密碼可讓您 toomaintain 連線 toohello 登錄使用一個密碼，當您重新產生 hello 其他密碼。 如果啟用 hello 帳戶時，您可以傳遞 hello 使用者名稱和其中一個密碼 toohello`docker login`命令的基本驗證 toohello 登錄。 例如：

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> hello 系統管理員帳戶可供單一使用者 tooaccess hello 登錄，主要是基於測試目的。 不建議其他使用者之間 tooshare hello 系統管理員帳戶認證。 所有使用者都顯示為單一使用者 toohello 登錄。 變更或停用此帳戶會停用登錄的全部使用者都使用 hello 認證的存取權。
>


### <a name="next-steps"></a>後續步驟
* [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)。
* 如需驗證在 hello 容器登錄中預覽的詳細資訊，請參閱 hello[部落格文章](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)。
