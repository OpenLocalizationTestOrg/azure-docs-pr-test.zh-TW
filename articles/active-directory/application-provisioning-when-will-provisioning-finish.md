---
title: "aaaUser 佈建 Azure AD tooan 組件庫的應用程式會擷取小時或更多 |Microsoft 文件"
description: "Toofind 出為什麼佈建 tooyour 應用程式可能會花費的時間比您預期的方式"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a>使用者佈建 Azure AD tooan 組件庫的應用程式會擷取小時以上

當第一次啟用自動佈建應用程式，hello 初始同步處理可能需要 20 分鐘 tooseveral 個小時，視 hello 大小 hello Azure AD 目錄與 hello 佈建的範圍中的使用者數目而定。 

Hello 初始同步處理之後的後續同步處理是更快、 佈建服務的 hello 儲存代表 hello 狀態，這兩個系統的 hello 初始同步處理之後，可改善效能的後續的同步處理的浮水印。

## <a name="how-tooimprove-provisioning-performance"></a>如何佈建效能 tooimprove

Hello 初始同步處理花費超過幾小時，有一件事，您可以執行 tooimprove 效能：

-   **使用者範圍設定篩選條件。** 範圍篩選器可讓您從 Azure AD 佈建服務擷取 hello 來篩選掉使用者根據特定的屬性值的 toofine 微調 hello 資料。 如需範圍設定篩選條件的詳細資訊，請參閱[含範圍篩選器的屬性型應用程式佈建](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters)。

## <a name="next-steps"></a>後續步驟
[自動化使用者佈建和取消佈建 tooSaaS 與 Azure Active Directory 的應用程式](active-directory-saas-app-provisioning.md)

