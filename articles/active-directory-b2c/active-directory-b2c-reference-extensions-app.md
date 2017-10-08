---
title: "擴充功能應用程式 - Azure AD B2C | Microsoft Docs"
description: "還原 hello b2c-擴充功能-應用程式"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C：擴充功能應用程式

建立 Azure AD B2C 目錄時，應用程式呼叫`b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.`hello 新目錄內會自動建立。 此應用程式，參照的 tooas hello **b2c 擴充功能-應用程式**，會顯示在*應用程式註冊*。 它會使用 hello Azure AD B2C 服務 toostore 使用者和資訊的自訂屬性。 如果刪除 hello 應用程式時，Azure AD B2C 將無法正確運作，並會影響您的生產環境。

> [!IMPORTANT]
> 除非您計劃 tooimmediately 刪除您的租用戶，請勿刪除 hello b2c-擴充功能-應用程式。 若 hello 應用程式維持已刪除超過 30 天，使用者資訊將會永久遺失。

## <a name="verifying-that-hello-extensions-app-is-present"></a>正在驗證該 hello 擴充功能的應用程式是否存在

hello b2c 擴充功能-應用程式的 tooverify 存在於：

1. 在您 Azure AD B2C 租用戶中，按一下 上**更多服務**hello 左側瀏覽功能表中。
1. 搜尋並開啟 [應用程式註冊]。
1. 尋找以 **b2c-extensions-app** 開頭的應用程式

## <a name="recover-hello-extensions-app"></a>復原 hello 擴充功能的應用程式

如果您不小心刪除 hello b2c-擴充功能-應用程式，您有 30 天 toorecover 它。 您可以還原使用 hello Graph API 的 hello 應用程式：

1. 瀏覽過[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/)。
1. 您想用於 toorestore hello 刪除應用程式的 hello Azure AD B2C 目錄的全域管理員身分登入 toohello 站台。
1. 發出 HTTP GET 針對 hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api 版本 = 1.6。 請確定 tooreplace`{tenantName}`以您的租用戶名稱。 這項作業會列出所有已刪除在 hello 過去 30 天的 hello 應用程式。
1. 其中 hello 名稱開頭為 'b2c 擴充功能-應用程式' 和複製的 hello 清單中尋找 hello 應用程式及其`objectid`屬性值。
1. 發出 HTTP POST 對 URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`。 取代 hello `{OBJECTID}` hello URL 以 hello 部分`objectid`hello 上一個步驟。 

您現在應該可以太[hello 還原應用程式請參閱 <<c2> ](#verifying-that-the-extensions-app-is-present)  hello Azure 入口網站中。

> [!NOTE]
> 如果已遭刪除 hello 內過去 30 天內，可以只還原應用程式。 如果已經超過 30 天，資料將會永久遺失。 如需協助，請提出支援票證。
