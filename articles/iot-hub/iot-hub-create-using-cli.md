---
title: "使用 Azure CLI (az.py) IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何使用您建立 Azure IoT 中樞 toocreate hello 跨平台 Azure CLI 2.0 (az.py)。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>建立使用 Azure CLI 2.0 hello IoT 中樞

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>簡介

您可以使用 Azure CLI 2.0 (az.py) toocreate，並以程式設計方式管理 Azure IoT 中樞。 本文章將示範如何 toouse 會 hello Azure CLI 2.0 (az.py) toocreate IoT 中樞。

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI hello 傳統和資源管理部署模型。
* Azure CLI 2.0 (az.py)-hello 新一代 CLI hello 資源管理部署模型的這篇文章中所述。

toocomplete 本教學課程中，您需要遵循的 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* [Azure CLI 2.0][lnk-CLI-install]。

## <a name="sign-in-and-set-your-azure-account"></a>登入並設定 Azure 帳戶

登入 tooyour Azure 帳戶，並選取您的訂用帳戶。

1. 在 hello 命令提示字元中執行 hello[登入命令][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    請遵循 hello 指示 tooauthenticate 使用 hello 程式碼，並登入 tooyour 透過 web 瀏覽器的 Azure 帳戶。

2. 如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 帳戶。 使用下列 hello[命令 toolist hello Azure 帳戶][ lnk-az-account-command]適用於您 toouse:
    
    ```azurecli
    az account list 
    ```

    使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。 您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>建立 IoT 中樞

使用 hello Azure CLI toocreate 資源群組，然後再加入 IoT 中樞。

1. 在建立 IoT 中樞時，必須將其建立在資源群組內。 使用現有的資源群組，或執行 hello 下列[命令 toocreate 資源群組][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > hello 前一個範例會在 hello 美國西部位置中建立 hello 資源群組。 您可以執行 hello 命令，以檢視可用位置清單`az account list-locations -o table`。
    >
    >

2. 執行下列 hello[命令 toocreate IoT 中樞][ lnk-az-iot-command]在資源群組中，使用您的 IoT 中樞的全域唯一名稱：
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> hello 前一個命令會建立 IoT 中樞 hello S1 定價的層，您需要付費。 如需詳細資訊，請參閱 [Azure IoT 中樞價格][lnk-iot-pricing]。
>
>

## <a name="remove-an-iot-hub"></a>移除 IoT 中樞

您也可以使用 Azure CLI hello[刪除個別的資源，][lnk-az-resource-command]，例如 IoT 中心] 或 [刪除資源群組和它的所有資源，包括任何 IoT 中樞。

IoT 中樞，執行下列命令的 hello toodelete:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete 資源群組和其所有資源，執行 hello，下列命令：

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>後續步驟
進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:

* [IoT 中樞開發人員指南][lnk-devguide]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 hello Azure 入口網站 toomanage IoT 中樞][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
