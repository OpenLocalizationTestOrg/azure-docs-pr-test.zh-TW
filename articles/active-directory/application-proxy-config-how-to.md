---
title: "aaaHow tooconfigure 應用程式 Proxy 應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 設定應用程式 Proxy 中的應用程式一些簡單的步驟"
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>如何 tooconfigure 應用程式 Proxy 應用程式

本文將協助您 toounderstand 如何 tooconfigure tooexpose Azure AD 應用程式 Proxy 應用程式在內部部署應用程式 toohello 雲端。

## <a name="recommended-documents"></a>建議的文件 

hello 初始設定及應用程式 Proxy 應用程式透過 hello 管理員入口網站中建立相關 toolearn 遵循 hello[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。

如需有關設定連接器的詳細資訊，請參閱[hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。

如需上傳憑證和使用自訂網域的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。

## <a name="create-hello-applicationsetting-hello-urls"></a>建立 hello 應用程式/設定 hello Url

如果您要遵照 hello 步驟 hello[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)文件且 hello 錯誤詳細資料的資訊和建議的方式取得錯誤建立 hello 應用程式，請參閱toofix hello 應用程式。 大部分的錯誤訊息都包含建議的修正。 tooavoid 常見的錯誤，請確認：

-   您是系統管理員的權限 toocreate 應用程式 Proxy 應用程式

-   是唯一的 hello 內部 URL

-   hello 外部 URL 是唯一的

-   hello http 或 https 的 Url 開頭和結尾為"/"

-   hello URL 應該是網域名稱，不是 IP 位址

當您建立 hello 應用程式時應該顯示 hello 右上角 hello 錯誤訊息。 您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。

   ![通知提示](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>設定連接器/連接器群組

如果您無法設定您的應用程式，因為 hello 連接器與連接器群組的相關警告，請參閱指示啟用應用程式 Proxy 的詳細資料 toodownload 連接器。 如果您想深入了解連接器 toolearn，請參閱 hello[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)。

如果您的連接器處於非使用狀態，這表示它們是無法 tooreach hello 服務。 這通常是因為 hello 所需的所有連接埠未開啟。 toosee 必要的連接埠的清單，請參閱啟用應用程式 Proxy 的文件的 hello hello 必要條件一節。

## <a name="upload-certificates-for-custom-domains"></a>上傳自訂網域的憑證

自訂網域可讓您對外部 Url 的 toospecify hello 網域。 toouse 自訂網域，您會需要 tooupload hello 憑證該網域。 如需使用自訂網域和憑證的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。 

如果您遇到問題上, 傳您的憑證，尋找 hello hello hello hello 憑證問題的其他資訊的入口網站中的錯誤訊息。 常見的憑證問題包括：

-   過期的憑證

-   憑證為自我簽署

-   遺漏 hello 私密金鑰憑證。

在右下角，當您嘗試 tooupload hello 憑證 hello 最佳 hello 錯誤訊息顯示。 您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。

   ![通知提示](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>後續步驟
[使用 Azure AD 應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)
