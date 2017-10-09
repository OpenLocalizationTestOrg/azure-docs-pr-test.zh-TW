---
title: "Azure 管理 API 憑證 aaaUpload |Microsoft 文件"
description: "了解 tooupload 在管理 API 的 hello Azure 傳統入口網站的憑證。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="fe245-103">上傳 Azure 管理 API 管理憑證</span><span class="sxs-lookup"><span data-stu-id="fe245-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="fe245-104">管理憑證，讓 Azure 提供 tooauthenticate 與 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fe245-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="fe245-105">許多程式和工具 （例如 Visual Studio 或 Azure SDK hello） 使用這些憑證 tooautomate 組態和各種 Azure 服務的部署。</span><span class="sxs-lookup"><span data-stu-id="fe245-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="fe245-106">請務必小心！</span><span class="sxs-lookup"><span data-stu-id="fe245-106">Be careful!</span></span> <span data-ttu-id="fe245-107">這些憑證類型允許驗證它們的任何人 toomanage hello 訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="fe245-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="fe245-108">如果您想要深入了解 Azure 憑證 (包括如何建立自我簽署憑證)，請參閱 [Azure 雲端服務的憑證概觀](cloud-services/cloud-services-certs-create.md#what-are-management-certificates)。</span><span class="sxs-lookup"><span data-stu-id="fe245-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="fe245-109">您也可以使用[Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate 用戶端程式碼用於自動化用途。</span><span class="sxs-lookup"><span data-stu-id="fe245-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="fe245-110">上傳管理憑證</span><span class="sxs-lookup"><span data-stu-id="fe245-110">Upload a management certificate</span></span>
<span data-ttu-id="fe245-111">一旦建立管理憑證、 （僅 hello 公開金鑰的.cer 檔案） 您可以將它上傳到 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="fe245-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="fe245-112">Hello 憑證在 hello 入口網站時，使用相符的憑證 （私密金鑰） 的任何人都可以透過 hello 相關聯的訂用帳戶的 hello 管理 API 和存取 hello 資源與其連接。</span><span class="sxs-lookup"><span data-stu-id="fe245-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="fe245-113">登入 toohello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fe245-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="fe245-114">按一下**更多服務**在 hello 下方的 Azure 服務清單，然後選取**訂閱**在 hello_一般_服務群組。</span><span class="sxs-lookup"><span data-stu-id="fe245-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![[訂用帳戶] 功能表](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="fe245-116">請確定 tooselect hello 想 tooassociate hello 憑證與正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe245-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="fe245-117">您已選取 hello 正確的訂用帳戶之後，請按**管理憑證**在 hello_設定_群組。</span><span class="sxs-lookup"><span data-stu-id="fe245-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![設定](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="fe245-119">按 hello**上傳** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fe245-119">Press hello **Upload** button.</span></span>

    ![憑證頁面的 [上傳]](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="fe245-121">填寫 [hello] 對話方塊的資訊，請按**上傳**。</span><span class="sxs-lookup"><span data-stu-id="fe245-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![設定](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="fe245-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe245-123">Next steps</span></span>
<span data-ttu-id="fe245-124">有訂用帳戶相關聯的管理憑證之後，您可以 （您已安裝符合憑證在本機的 hello 之後） 以程式設計方式連接 toohello[傳統部署模型 REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx)和自動化hello 也會與該訂用帳戶相關聯的各種 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="fe245-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
