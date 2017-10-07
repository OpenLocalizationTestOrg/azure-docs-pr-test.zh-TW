---
title: "Azure Active Directory B2C：建立 Azure Active Directory B2C 租用戶 | Microsoft Docs"
description: "Toocreate Azure Active Directory B2C 租用戶的如何主題"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立的 Azure Active Directory B2C 租用戶

編輯 Sipi。

本快速入門協助您在數分鐘內建立 Microsoft Azure Active Directory (Azure AD) B2C 租用戶。 當您完成時，您可以 B2C 租用戶 toouse 註冊 B2C 應用程式。

## <a name="prerequisites"></a>必要條件

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>登入 tooAzure

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="create-an-azure-ad-b2c-tenant"></a>建立 Azure AD B2C 租用戶

B2C 功能無法在您現有的租用戶中啟用。 您需要 toocreate Azure AD B2C 租用戶。

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

恭喜，您已建立 Azure Active Directory B2C 租用戶。 您是 hello 租用戶全域管理員。 您可視需要新增其他「全域管理員」。 tooswitch tooyour 新租用戶中，按一下 hello*管理新的租用戶連結*。

![管理新租用戶連結](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> 如果您打算 toouse B2C 租用戶在實際執行應用程式，請閱讀 hello 文章上[預覽 B2C 租用戶與實際執行延展](active-directory-b2c-reference-tenant-type.md)。 那里已知問題，當您刪除現有的 B2C 租用戶，並重新建立 hello 與相同的網域名稱。 您需要 toocreate B2C 租用戶與不同的網域名稱。
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>連結您的租用戶 tooyour 訂用帳戶

您需要 toolink 您 Azure AD B2C 租用戶 tooyour Azure 訂用帳戶 tooenable B2C 的所有功能，並支付使用費用。 詳細資訊，讀取 toolearn[本文](active-directory-b2c-how-to-enable-billing.md)。 如果您不要連結您的 Azure AD B2C 租用戶 tooyour Azure 訂用帳戶，某些功能會封鎖，而且您會看到一則警告訊息 （「 連結的 toothis B2C 租用戶或 hello 訂用帳戶沒有訂用帳戶需要您注意。"） hello B2C 設定中。 請務必先進行此步驟，然後才將您的應用程式傳送到生產環境。

## <a name="easy-access-toosettings"></a>輕鬆存取 toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

您也可以存取 hello 刀鋒視窗中輸入`Azure AD B2C`中**搜尋資源**頂端 hello hello 入口網站。 在 hello 結果清單中，選取  **Azure AD B2C** tooaccess hello B2C 設定 刀鋒視窗。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [在 B2C 租用戶中註冊您的 B2C 應用程式](active-directory-b2c-app-registration.md)
