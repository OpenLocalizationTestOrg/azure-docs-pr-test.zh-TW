---
title: "Sipi 測試檔案 |Microsoft 文件"
description: "若要檢查 ReadyForTest 相依性的測試檔案"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a>Sipi 測試檔案

本快速入門協助您在幾分鐘內於 Microsoft Azure Active Directory (Azure AD) B2C 租用戶中註冊應用程式。 當您完成時，應用程式就已註冊完成，以便在 Azure B2C 租用戶中使用。

## <a name="prerequisites"></a>必要條件

若要建置可接受取用者註冊與登入的應用程式，您必須先使用 Azure Active Directory B2C 租用戶註冊該應用程式。 使用 [建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)中概述的步驟來建立您自己的租用戶。

在 Azure 入口網站中從 [Azure AD B2C] 刀鋒視窗建立的應用程式，必須從相同的位置進行管理。 如果您使用 PowerShell 或另一個入口網站編輯 B2C 應用程式，系統則不支援這些應用程式支援且無法搭配 Azure AD B2C 運作。 如需詳細資料，請參閱[ 發生錯誤的應用程式](#faulted-apps)一節。 

## <a name="navigate-to-b2c-settings"></a>瀏覽至 B2C 設定

以 B2C 租用戶的全域管理員身分登入 [Azure 入口網站](https://portal.azure.com/)。 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

根據您所註冊的應用程式類型，選擇後續步驟：
