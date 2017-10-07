---
title: "aaaUse CLI 2.0 toocreate Azure AD 應用程式並將它設定為 Azure 媒體服務 API tooaccess |Microsoft 文件"
description: "本主題說明如何 toouse CLI 2.0 toocreate Azure AD 應用程式並將它設定 tooaccess Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>使用 CLI 2.0 toocreate AAD 應用程式，並將它設定 tooaccess Azure 媒體服務 API

本主題說明您如何 toouse CLI 2.0 toocreate Azure Active Directory (Azure AD) 應用程式和服務主體 tooaccess Azure 媒體服務資源。 

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
- 媒體服務帳戶。 如需詳細資訊，請參閱[建立 Azure 媒體服務帳戶使用 Azure 入口網站 hello](media-services-portal-create-account.md)。

## <a name="use-hello-azure-cloud-shell"></a>使用 Azure 雲端殼層 hello

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 啟動 hello 雲端殼層從 hello 上方瀏覽 窗格中的 hello 入口網站。

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

如需詳細資訊，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)。

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>建立 Azure AD 應用程式並使用 CLI 2.0 設定存取 toohello 媒體帳戶
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

例如：

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

在此範例中，hello**範圍**是 hello 完整資源路徑 hello media services 帳戶。 不過，hello**範圍**可以是任何層級。

例如，它可以是 hello 的下列層級的其中一個：
 
* hello**訂用帳戶**層級。
* hello**資源群組**層級。
* hello**資源**層級 （例如，媒體帳戶）。

如需詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)。

另請參閱[Manage Role-Based 以 hello Azure 命令列介面的存取控制](../active-directory/role-based-access-control-manage-access-azure-cli.md)。 

## <a name="next-steps"></a>後續步驟

開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。
