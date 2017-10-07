---
title: "建立應用程式 Proxy 應用程式的 aaaProblem |Microsoft 文件"
description: "Tootroubleshoot 如何發出在 hello Azure AD 管理入口網站中建立的應用程式 Proxy 應用程式"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a>建立應用程式 Proxy 應用程式時發生問題 

以下是一些 hello 常見問題人臉時建立新的應用程式 proxy 應用程式。

## <a name="recommended-documents"></a>建議的文件 

toolearn 進一步了解建立應用程式 Proxy 應用程式透過 hello 管理入口網站，請參閱[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。

如果您要遵照 hello 該文件中的步驟，並取得建立 hello 應用程式時發生錯誤，請參閱 hello 錯誤詳細資料的資訊及如何 toofix hello 應用程式的建議。 大部分的錯誤訊息都包含建議的修正。 

## <a name="specific-things-toocheck"></a>特定項目 toocheck

tooavoid 常見的錯誤，請確認：

-   您是系統管理員的權限 toocreate 應用程式 Proxy 應用程式

-   是唯一的 hello 內部 URL

-   hello 外部 URL 是唯一的

-   hello http 或 https 的 Url 開頭和結尾為"/"

-   hello URL 應該是網域名稱而不是 IP 位址

當您建立 hello 應用程式時應該顯示 hello 右上角 hello 錯誤訊息。 您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。

   ![通知提示](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a>後續步驟
[在 hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)
