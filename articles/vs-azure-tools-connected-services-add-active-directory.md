---
title: "使用 Visual Studio 中的 已連接服務的 Azure Active Directory aaaAdding |Microsoft 文件"
description: "新增 Azure Active Directory 使用 hello Visual Studio 加入已連接服務對話方塊"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>在 Visual Studio 中使用已連接服務加入 Azure Active Directory
藉由使用 Azure Active Directory (Azure AD)，您便可以針對 ASP.NET MVC Web 應用程式支援「單一登入」(SSO)，或在 Web API 服務中支援「Active Directory 驗證」。 使用 Azure Active Directory 驗證時，您的使用者可以使用 Azure Active Directory tooconnect tooyour web 應用程式中的帳戶。 公開 API 的 web 應用程式時，hello Web API 與 Azure Active Directory 驗證的優點包括增強的資料安全性。 使用 Azure AD，您沒有 toomanage 自己帳戶和使用者管理的分別驗證系統。

## <a name="prerequisites"></a>必要條件
- Azure 帳戶 - 如果您沒有 Azure 帳戶，您可以[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用您的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>連接 tooAzure Active Directory 使用 hello 已連接服務對話方塊
1. 在 Visual Studio 中，建立或開啟 ASP.NET MVC 專案或 ASP.NET Web API 專案。

1. 從 hello 方案總管 中，以滑鼠右鍵按一下 hello**已連接服務** 節點，並從 hello 內容功能表中，選取**加入已連接服務**。

1. 在 hello**已連接服務**頁面上，選取**與 Azure Active Directory 驗證**。
   
    ![[已連接服務] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. 在 [hello**簡介**hello 頁面**設定 Azure AD 驗證**精靈中，選取**下一步]**。
   
    ![[簡介] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. 在 hello**單一登入**頁面 hello**設定 Azure AD 驗證**精靈中，選取網域從 hello**網域**下拉式清單。 hello 網域清單包含 hello 帳戶設定 對話方塊中所列出的 hello 帳戶可存取的所有網域。 或者，您可以輸入網域名稱如果您找不到 hello 要尋找的例如`mydomain.onmicrosoft.com`。 您可以選擇 hello 選項 toocreate 的 Azure Active Directory 應用程式，或使用現有的 Azure Active Directory 應用程式中的 hello 設定。 完成時，選取 [下一步]。
   
    ![[單一登入] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. Hello 上**目錄存取**頁面 hello**設定 Azure AD 驗證**精靈 中，確定該 hello**讀取目錄資料**核取選項。 
   
    ![[目錄存取] 頁面](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. 選取**完成**tooadd hello 所需的組態程式碼和參考 tooenable 的 Azure AD 驗證程式專案。 您可以看到 hello Active Directory 網域上 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

1. Visual Studio 會顯示[發生了什麼事](#how-your-project-is-modified)文章 tooshow 您如何修改您的專案。 如果您想一切運作正常的 toocheck，開啟其中一個 hello 修改組態檔，並確認 hello 文章中提及的 hello 設定有。 

## <a name="how-your-project-is-modified"></a>您的專案修改方式
當您執行 hello 精靈時，Visual Studio 會加入 Azure Active Directory 和相關聯的參考 tooyour 專案。 組態檔和專案中的程式碼檔案也是 Azure AD 的已修改的 tooadd 支援。 hello 特定修改 Visual Studio 會取決於 hello 專案類型。 如需深入了解 ASP.NET MVC 專案的修改方式，請參閱 [發生什麼事：MVC 專案](http://go.microsoft.com/fwlink/p/?LinkID=513809)。 而對於 Web API 專案，請參閱 [發生什麼事：Web API 專案](http://go.microsoft.com/fwlink/p/?LinkId=513810)。

## <a name="next-steps"></a>後續步驟
* [MSDN 的 Azure Active Directory 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Azure Active Directory 文件](https://azure.microsoft.com/documentation/services/active-directory/)
* [部落格文章： 入門 tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)

