---
title: "如何設定應用程式 Proxy 應用程式 | Microsoft Docs"
description: "了解如何使用幾個簡單步驟來建立及設定應用程式 Proxy 應用程式"
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a>如何設定應用程式 Proxy 應用程式

本文協助您了解如何在 Azure AD 內設定應用程式 Proxy 應用程式，以向雲端公開您的內部部署應用程式。

## <a name="recommended-documents"></a>建議的文件 

若要深入了解應用程式 Proxy 應用程式透過管理入口網站的初始設定與建立，請遵循[使用 Azure AD 應用程式 Proxy 發佈應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。

如需設定連接器的詳細資料，請參閱[在 Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。

如需上傳憑證和使用自訂網域的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。

## <a name="create-the-applicationsetting-the-urls"></a>建立應用程式/設定 URL

如果您依照[使用 Azure AD 應用程式 Proxy 發佈應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)文件中的步驟，並在建立應用程式時發生錯誤，請查看錯誤詳細資料，以取得修正應用程式的資訊及建議。 大部分的錯誤訊息都包含建議的修正。 若要避免常見的錯誤，請確認：

-   您是具有建立應用程式 Proxy 應用程式權限的系統管理員

-   內部 URL 是唯一的

-   外部 URL 是唯一的

-   URL 開頭為 http 或 https，且結尾為 “/”

-   URL 應該是網域名稱，而非 IP 位址

當您建立應用程式時，錯誤訊息應該會在右上角顯示。 您也可以選取通知圖示來查看錯誤訊息。

   ![通知提示](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>設定連接器/連接器群組

如果您因為連接器和連接器群組的警告而無法設定應用程式，請參閱啟用應用程式 Proxy 的指示，以取得下載連接器的詳細資料。 如果您想要深入了解連接器，請參閱[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)。

如果您的連接器處於非作用中狀態，這表示它們無法連線到服務。 這通常是因為沒有開啟所有必要的連接埠。 若要查看必要連接埠的清單，請參閱《啟用應用程式 Proxy》文件的＜必要條件＞一節。

## <a name="upload-certificates-for-custom-domains"></a>上傳自訂網域的憑證

自訂網域可讓您指定外部 URL 的網域。 若要使用自訂網域，您需要上傳該網域的憑證。 如需使用自訂網域和憑證的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。 

如果您在上傳憑證時遇到問題，請尋找入口網站中的錯誤訊息以取得憑證問題的其他資訊。 常見的憑證問題包括：

-   過期的憑證

-   憑證為自我簽署

-   憑證沒有私密金鑰

當您嘗試上傳憑證時，錯誤訊息會顯示在右上角。 您也可以選取通知圖示來查看錯誤訊息。

   ![通知提示](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>後續步驟
[使用 Azure AD 應用程式 Proxy 發佈應用程式](application-proxy-publish-azure-portal.md)
