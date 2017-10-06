---
title: "aaaCreate 的私用 Docker 登錄-而 Azure 入口網站 |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure 入口網站"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>建立私用 Docker 容器登錄中使用 hello Azure 入口網站
使用 Azure 入口網站 toocreate 容器登錄中的 hello 和管理其設定。 您也可以建立及管理使用 hello 容器登錄[Azure CLI 2.0 命令](container-registry-get-started-azure-cli.md)， [Azure PowerShell](container-registry-get-started-powershell.md)或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).

背景和概念，請參閱[hello 概觀](container-registry-intro.md)。

## <a name="create-a-container-registry"></a>建立容器登錄庫
1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **+ 新增**。
2. 搜尋 hello marketplace 中的**Azure 容器登錄**。
3. 選取 [Azure 容器登錄]，其發佈者為 **Microsoft**。
    ![Azure Marketplace 中的容器登錄庫服務](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. 按一下 [建立] 。 hello **Azure 容器登錄中**刀鋒視窗隨即出現。

    ![容器登錄庫設定](./media/container-registry-get-started-portal/container-registry-settings.png)
5. 在 hello **Azure 容器登錄中**刀鋒視窗中，輸入下列資訊的 hello。 完成後按一下 [建立]。

    a. **登錄名稱**：指定登錄的全域唯一最上層網域名稱。 在此範例中，是 hello 登錄名稱*myRegistry01*，但以取代您自己的唯一名稱。 hello 名稱只能包含字母和數字。

    b. **資源群組**： 選取現有[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。

    c. **位置**： 選取 hello 服務所在的 Azure 資料中心位置[可用](https://azure.microsoft.com/regions/services/)，例如**美國中南部**。

    d. **系統管理使用者**： 如果您想，讓系統管理員使用者 tooaccess hello 登錄。 您可以變更此設定建立 hello 登錄之後。

      > [!IMPORTANT]
      > 此外 tooproviding 存取透過系統管理使用者帳戶、 容器登錄支援 Azure Active Directory 服務主體所支援的驗證。 如需詳細資訊和考量事項，請參閱[驗證容器登錄庫](container-registry-authentication.md)。
      >

    e. **儲存體帳戶**： 使用 hello 預設設定 toocreate[儲存體帳戶](../storage/common/storage-introduction.md)，或在 hello 中選取現有的儲存體帳戶相同的位置。 目前不支援進階儲存體。

## <a name="manage-registry-settings"></a>管理登錄庫設定
在建立之後 hello 登錄，尋找 hello 登錄設定開始 hello**容器登錄**hello 入口網站中的刀鋒視窗。 例如，您可能需要 tooyour 登錄中的 hello 設定 toolog 或您可能會想 tooenable 或是停用 hello 系統管理使用者。

1. 在 hello**容器登錄**刀鋒視窗中，按一下您的登錄 hello 名稱。

    ![容器登錄庫刀鋒視窗](./media/container-registry-get-started-portal/container-registry-blade.png)
2. toomanage 存取設定，請按一下**便捷鍵**。

    ![容器登錄庫的存取權](./media/container-registry-get-started-portal/container-registry-access.png)
3. 請注意下列設定的 hello:

   * **登入伺服器**-您可以使用 toolog toohello 登錄中的 hello 完整限定的名稱。 在此範例中為 `myregistry01.azurecr.io`。
   * **系統管理使用者**-切換 tooenable 或停用 hello 登錄系統管理使用者帳戶。
   * **使用者名稱**和**密碼**-hello hello 系統管理員使用者帳戶的認證 （如果啟用） 您可以使用 toolog toohello 登錄中。 您可以選擇性地重新產生 hello 密碼。 如此您就可以維護連接 toohello 登錄使用一組密碼，當您重新產生 hello 其他密碼，會建立兩個密碼。 相反地，請參閱與服務主體 tooauthenticate[與私用 Docker 容器登錄中的 Authenticate](container-registry-authentication.md)。

## <a name="next-steps"></a>後續步驟
* [推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)
