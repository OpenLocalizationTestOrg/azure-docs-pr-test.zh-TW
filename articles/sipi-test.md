---
title: "Sipi 測試檔案 |Microsoft 文件"
description: "測試檔案 toocheck ReadyForTest 相依性"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a>Sipi 測試檔案

本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。 當您完成時，使用 hello Azure B2C 租用戶中註冊您的應用程式。

## <a name="prerequisites"></a>必要條件

toobuild 接受取用者註冊和登入的應用程式，您必須先 tooregister hello 應用程式與 Azure Active Directory B2C 租用戶。 使用 hello 中所述的步驟，以取得自己的租用戶[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。

從 Azure AD B2C hello 刀鋒視窗 hello Azure 入口網站中建立的應用程式必須從 hello 管理相同的位置。 如果您編輯使用 PowerShell 或另一個入口網站的 hello B2C 應用程式，它們會變成不受支援，無法搭配 Azure AD B2C。 查看詳細資料中 hello[發生錯誤的應用程式](#faulted-apps)> 一節。 

## <a name="navigate-toob2c-settings"></a>瀏覽 tooB2C 設定

登入 toohello [Azure 入口網站](https://portal.azure.com/)為 hello hello B2C 租用戶的全域管理員。 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

選擇 [下一步] 步驟會依據您所註冊的 hello 應用程式類型：
