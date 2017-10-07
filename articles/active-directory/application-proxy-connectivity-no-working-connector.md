---
title: "應用程式 Proxy 應用程式找到 aaaNo 工作連接器群組 |Microsoft 文件"
description: "在您的應用程式以 hello Azure AD 應用程式 Proxy 連接器群組的連接器沒有工作時，可能會遇到的問題"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>針對應用程式 Proxy 應用程式找不到作用中的連接器群組

此文章說明您 tooresolve hello 常見的問題不是偵測到應用程式的應用程式 Proxy 連接器時所面對整合與 Azure Active Directory。

## <a name="overview-of-steps"></a>步驟概觀
如果沒有任何工作在您的應用程式連接器群組的連接器，有幾種方式 tooresolve hello 問題：

-   如果您不有任何連接器 hello 群組中，您可以：

    -   下載新的連接器，在 hello 右由內部部署伺服器上，並將它指派 toothis 群組

    -   將 active 的連接器移到 hello 群組

-   如果您不有任何作用中連接器 hello 群組中，您可以：

    -   識別您的連接器為非使用中的 hello 原因和解決

    -   將 active 的連接器移到 hello 群組

其中是 hello 問題 tooknow 開啟應用程式中的 hello"應用程式 Proxy 」 功能表，並查看 hello 連接器群組的警告訊息。 它會指定其中一個該 hello 群組必須至少一個連接器 （有無 hello 群組中） 或它有沒有作用中的連接線，（雖然您可能會有非作用中連接器）。

   ![Azure 入口網站中的連接器群組選項](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

如需上述各選項的詳細資訊，請參閱 hello 對應下一節。 每一種會假設您從 hello 連接器管理 頁面上啟動。 如果您看到上述的 hello 錯誤訊息，您可以移 toothis 頁面按一下 hello 警告訊息。 否則找到此太移**Azure Active Directory**、 按一下**企業應用程式**，然後**應用程式 Proxy。**

   ![Azure 入口網站中的連接器群組管理](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>下載新的連接器

toodownload 新連接器，使用 hello 「 下載連接器 」 按鈕，在 hello hello 頁面最上方。

請注意 hello 連接器需求 toobe 直接視線 toohello 後端應用程式的電腦上安裝，且通常會放在 hello 與 hello 應用程式相同的伺服器。 下載之後，應該會出現在這個功能表中的 hello 連接器。 按一下 hello 連接器，並使用 hello 「 連接器群組 」 下拉式 toomake 確定其所屬 toohello 正確的群組。 儲存 hello 變更。

   ![從 hello Azure 入口網站下載 hello 連接器](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>移動作用中的連接器

如果您有使用中的連接器應隸屬於 toohello 群組且具有的視野 toohello 目標後端應用程式，您可以將 hello 連接器移到 hello 分派群組中。 toodo，請按一下 hello 連接器。 在 hello 「 連接器群組 」 欄位中，使用 hello 下拉式 tooselect hello 正確的群組，然後按一下 [儲存]。

## <a name="resolve-an-inactive-connector"></a>解決非作用中的連接器

如果 hello 只有連接器 hello 群組中的非使用中，他們可能並不會在機器上有所有 hello 必要的連接埠已解除都封鎖。

請參閱 hello 連接埠上調查此問題的詳細資料的疑難排解文件。

## <a name="next-steps"></a>後續步驟
[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)


