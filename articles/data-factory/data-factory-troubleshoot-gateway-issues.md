---
title: "資料管理閘道器會發出 aaaTroubleshoot |Microsoft 文件"
description: "提供秘訣 tootroubleshoot 問題相關的 tooData 管理閘道器。"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="00140-103">使用資料管理閘道針對問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="00140-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="00140-104">本文提供使用資料管理閘道進行疑難問題排解的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="00140-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="00140-105">請參閱 hello[資料管理閘道器](data-factory-data-management-gateway.md)hello 閘道的詳細資訊的發行項。</span><span class="sxs-lookup"><span data-stu-id="00140-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="00140-106">請參閱 hello[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)將資料從內部部署 SQL Server 資料庫 tooMicrosoft Azure Blob 儲存體中，使用 hello 閘道的逐步解說中的發行項。</span><span class="sxs-lookup"><span data-stu-id="00140-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="00140-107">失敗的 tooinstall 或註冊閘道</span><span class="sxs-lookup"><span data-stu-id="00140-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="00140-108">1.問題</span><span class="sxs-lookup"><span data-stu-id="00140-108">1. Problem</span></span>
<span data-ttu-id="00140-109">您看到此錯誤訊息時安裝並註冊閘道器，特別，下載 hello 閘道安裝檔案時。</span><span class="sxs-lookup"><span data-stu-id="00140-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="00140-110">原因</span><span class="sxs-lookup"><span data-stu-id="00140-110">Cause</span></span>
<span data-ttu-id="00140-111">嘗試 tooinstall hello 閘道 hello 機器失敗 toodownload hello 最新閘道安裝檔案從 hello 下載中心到期 tooa 網路問題。</span><span class="sxs-lookup"><span data-stu-id="00140-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-112">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-112">Resolution</span></span>
<span data-ttu-id="00140-113">檢查防火牆 proxy 伺服器設定 toosee hello 設定會封鎖從 hello 電腦 toohello hello 網路連線是否[下載中心](https://download.microsoft.com/)，並更新 hello 設定據以。</span><span class="sxs-lookup"><span data-stu-id="00140-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="00140-114">或者，您可以從 hello 下載 hello hello 最新閘道的安裝檔[下載中心](https://www.microsoft.com/download/details.aspx?id=39717)在其他電腦可以存取 hello 下載中心上。</span><span class="sxs-lookup"><span data-stu-id="00140-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="00140-115">您可以複製 hello 安裝程式檔案 toohello 閘道主機電腦並手動執行 tooinstall 及更新 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="00140-116">2.問題</span><span class="sxs-lookup"><span data-stu-id="00140-116">2. Problem</span></span>
<span data-ttu-id="00140-117">當您嘗試依序按一下 tooinstall 閘道時，您會看到此錯誤**直接在這部電腦上安裝**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="00140-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="00140-118">原因</span><span class="sxs-lookup"><span data-stu-id="00140-118">Cause</span></span>
<span data-ttu-id="00140-119">Hello 機器上已安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-120">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-120">Resolution</span></span>
<span data-ttu-id="00140-121">解除安裝現有的閘道 hello hello 機器上，按一下 hello**直接在這部電腦上安裝**重新連結。</span><span class="sxs-lookup"><span data-stu-id="00140-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="00140-122">3.問題</span><span class="sxs-lookup"><span data-stu-id="00140-122">3. Problem</span></span>
<span data-ttu-id="00140-123">註冊新的閘道時，您可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="00140-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="00140-124">原因</span><span class="sxs-lookup"><span data-stu-id="00140-124">Cause</span></span>
<span data-ttu-id="00140-125">您可能會看到此訊息，其中一個 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="00140-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="00140-126">hello hello 閘道器金鑰格式無效。</span><span class="sxs-lookup"><span data-stu-id="00140-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="00140-127">hello 閘道器金鑰已失效。</span><span class="sxs-lookup"><span data-stu-id="00140-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="00140-128">從 hello 入口網站已重新產生 hello 閘道器金鑰。</span><span class="sxs-lookup"><span data-stu-id="00140-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="00140-129">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-129">Resolution</span></span>
<span data-ttu-id="00140-130">請確認您是否使用 hello 正確的閘道金鑰從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="00140-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="00140-131">如有需要重新產生金鑰，並使用 hello 金鑰 tooregister hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="00140-132">4.問題</span><span class="sxs-lookup"><span data-stu-id="00140-132">4. Problem</span></span>
<span data-ttu-id="00140-133">您可能會看到下列錯誤訊息，當您註冊閘道的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![金鑰的內容或格式無效](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="00140-135">原因</span><span class="sxs-lookup"><span data-stu-id="00140-135">Cause</span></span>
<span data-ttu-id="00140-136">hello 內容或 hello 輸入閘道器金鑰的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="00140-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="00140-137">其中一個 hello 原因可以是您從 hello 入口網站複製 hello 索引鍵的一部分，或您使用了無效的金鑰。</span><span class="sxs-lookup"><span data-stu-id="00140-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-138">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-138">Resolution</span></span>
<span data-ttu-id="00140-139">產生閘道金鑰在 hello 入口網站，並使用 hello 複製按鈕 toocopy hello 整個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="00140-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="00140-140">然後將它貼到此視窗 tooregister hello 閘道器中。</span><span class="sxs-lookup"><span data-stu-id="00140-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="00140-141">5.問題</span><span class="sxs-lookup"><span data-stu-id="00140-141">5. Problem</span></span>
<span data-ttu-id="00140-142">您可能會看到下列錯誤訊息，當您註冊閘道的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![閘道金鑰無效或是空的](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="00140-144">原因</span><span class="sxs-lookup"><span data-stu-id="00140-144">Cause</span></span>
<span data-ttu-id="00140-145">已重新產生 hello 閘道器金鑰或 hello 閘道已刪除 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="00140-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="00140-146">它也可會發生如果 hello 資料管理閘道器安裝程式不是最新。</span><span class="sxs-lookup"><span data-stu-id="00140-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-147">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-147">Resolution</span></span>
<span data-ttu-id="00140-148">檢查是否 hello 資料管理閘道器安裝程式 hello 最新版本，您可以在 hello Microsoft 找到最新版本的 hello[下載中心](https://go.microsoft.com/fwlink/p/?LinkId=271260)。</span><span class="sxs-lookup"><span data-stu-id="00140-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="00140-149">如果安裝程式目前 / 最新，而且閘道仍存在於入口網站，重新產生 hello Azure 入口網站中的 hello 閘道器金鑰和使用 hello 複製按鈕 toocopy hello 整個索引鍵，並再將它貼入此視窗 tooregister hello 閘道中。</span><span class="sxs-lookup"><span data-stu-id="00140-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="00140-150">否則，重新建立 hello 閘道，然後再重新啟動。</span><span class="sxs-lookup"><span data-stu-id="00140-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="00140-151">6.問題</span><span class="sxs-lookup"><span data-stu-id="00140-151">6. Problem</span></span>
<span data-ttu-id="00140-152">您可能會看到下列錯誤訊息，當您註冊閘道的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![閘道金鑰無效或是空的](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="00140-154">原因</span><span class="sxs-lookup"><span data-stu-id="00140-154">Cause</span></span>
<span data-ttu-id="00140-155">因為 hello 閘道已刪除，或已重新產生 hello 相關聯的閘道金鑰，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="00140-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-156">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-156">Resolution</span></span>
<span data-ttu-id="00140-157">如果 hello 閘道已刪除、 重新建立 hello hello 入口網站的閘道，請按一下**註冊**、 從 hello 入口網站複製 hello 金鑰、 貼上它，然後再次嘗試 tooregister hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="00140-158">如果 hello 閘道仍然存在，但已重新產生其金鑰，請使用 hello 新金鑰 tooregister hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="00140-159">如果您沒有 hello 金鑰，重新產生 hello 再次從 hello 入口網站的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="00140-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="00140-160">7.問題</span><span class="sxs-lookup"><span data-stu-id="00140-160">7. Problem</span></span>
<span data-ttu-id="00140-161">當您註冊閘道器時，您可能需要 tooenter 路徑和密碼的憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![指定憑證](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="00140-163">原因</span><span class="sxs-lookup"><span data-stu-id="00140-163">Cause</span></span>
<span data-ttu-id="00140-164">hello 閘道已在之前的其他電腦上註冊。</span><span class="sxs-lookup"><span data-stu-id="00140-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="00140-165">Hello 初始註冊期間的閘道，加密憑證已與 hello 閘道相關聯。</span><span class="sxs-lookup"><span data-stu-id="00140-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="00140-166">hello 憑證可以由 hello 閘道自我產生或 hello 使用者所提供。</span><span class="sxs-lookup"><span data-stu-id="00140-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="00140-167">此憑證是使用的 tooencrypt hello 資料存放區 （連結的服務） 的認證。</span><span class="sxs-lookup"><span data-stu-id="00140-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![匯出憑證](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="00140-169">當還原 hello 閘道在不同的主機電腦、 hello 註冊精靈會要求的這個憑證 toodecrypt 先前認證加密的與此憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="00140-170">如果沒有此憑證，hello 新的閘道無法解密 hello 認證而且與此新的閘道相關聯的後續複製活動執行會失敗。</span><span class="sxs-lookup"><span data-stu-id="00140-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="00140-171">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-171">Resolution</span></span>
<span data-ttu-id="00140-172">如果您已經從原始閘道機器 hello 匯出 hello 認證憑證，使用 hello**匯出**按鈕 hello**設定**索引標籤中的資料管理閘道組態管理員，請使用 hello此憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="00140-173">在復原閘道時，您無法略過此階段。</span><span class="sxs-lookup"><span data-stu-id="00140-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="00140-174">如果 hello 憑證遺失，您需要從 hello 入口網站的 toodelete hello 閘道，並重新建立新的閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="00140-175">此外，更新所有的連結的服務的相關的 toohello 閘道重新輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="00140-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="00140-176">8.問題</span><span class="sxs-lookup"><span data-stu-id="00140-176">8. Problem</span></span>
<span data-ttu-id="00140-177">您可能會看到下列錯誤訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="00140-178">原因</span><span class="sxs-lookup"><span data-stu-id="00140-178">Cause</span></span>
<span data-ttu-id="00140-179">當您的閘道時需要 HTTP proxy tooaccess 網際網路資源的環境中，就會發生此錯誤或 proxy 的驗證密碼已變更，但未據以更新您的閘道中。</span><span class="sxs-lookup"><span data-stu-id="00140-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-180">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-180">Resolution</span></span>
<span data-ttu-id="00140-181">遵循 hello hello 指示[Proxy server 考量](#proxy-server-considerations)這個區段，然後設定 proxy 設定與資料管理閘道組態管理員。</span><span class="sxs-lookup"><span data-stu-id="00140-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="00140-182">閘道在線上但功能受限</span><span class="sxs-lookup"><span data-stu-id="00140-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="00140-183">1.問題</span><span class="sxs-lookup"><span data-stu-id="00140-183">1. Problem</span></span>
<span data-ttu-id="00140-184">您看到 hello hello 閘道狀態為線上，但功能有限。</span><span class="sxs-lookup"><span data-stu-id="00140-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="00140-185">原因</span><span class="sxs-lookup"><span data-stu-id="00140-185">Cause</span></span>
<span data-ttu-id="00140-186">具有有限的功能，其中一個 hello 下列原因與線上查看 hello hello 閘道狀態：</span><span class="sxs-lookup"><span data-stu-id="00140-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="00140-187">閘道無法連接 toocloud 服務透過 Azure 服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="00140-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="00140-188">雲端服務無法透過服務匯流排連線 toogateway。</span><span class="sxs-lookup"><span data-stu-id="00140-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="00140-189">當 hello 閘道在線上且最有限的功能時，您可能無法將能 toouse hello 資料 Factory 複製精靈 toocreate 資料管線來複製資料 tooor 從內部部署資料存放區。</span><span class="sxs-lookup"><span data-stu-id="00140-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="00140-190">因應措施，您可以在 hello 入口網站，Visual Studio 或 Azure PowerShell 中使用 Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="00140-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-191">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-191">Resolution</span></span>
<span data-ttu-id="00140-192">此問題解決方式 (online 具有有限功能) 根據 hello 閘道無法連接 toohello 雲端服務或 hello 另一種方式。</span><span class="sxs-lookup"><span data-stu-id="00140-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="00140-193">hello 下列各節提供這些解決方案。</span><span class="sxs-lookup"><span data-stu-id="00140-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="00140-194">2.問題</span><span class="sxs-lookup"><span data-stu-id="00140-194">2. Problem</span></span>
<span data-ttu-id="00140-195">您會看到下列錯誤 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![閘道無法連接 toocloud 服務](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="00140-197">原因</span><span class="sxs-lookup"><span data-stu-id="00140-197">Cause</span></span>
<span data-ttu-id="00140-198">閘道無法透過服務匯流排連線 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="00140-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-199">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-199">Resolution</span></span>
<span data-ttu-id="00140-200">請遵循這些步驟 tooget hello 閘道上線：</span><span class="sxs-lookup"><span data-stu-id="00140-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="00140-201">輸出規則上 hello 閘道器電腦與 hello 公司防火牆允許的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="00140-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="00140-202">您可以找到 hello Windows 事件記錄檔中的 IP 位址 (識別碼 = = 401): 已嘗試以禁止透過其存取權限 XX 方式進行 tooaccess 通訊端。XX。XX。XX:9350。</span><span class="sxs-lookup"><span data-stu-id="00140-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="00140-203">Hello 閘道上設定 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="00140-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="00140-204">請參閱 hello [Proxy server 考量](#proxy-server-considerations)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="00140-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="00140-205">啟用輸出連接埠 5671 與 9350-9354 上 hello 閘道器電腦與 hello 公司防火牆在這兩個 hello Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="00140-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="00140-206">請參閱 hello[連接埠和防火牆](#ports-and-firewall)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="00140-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="00140-207">此步驟為選用步驟，但基於效能考量，還是建議執行。</span><span class="sxs-lookup"><span data-stu-id="00140-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="00140-208">3.問題</span><span class="sxs-lookup"><span data-stu-id="00140-208">3. Problem</span></span>
<span data-ttu-id="00140-209">您會看到下列錯誤 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="00140-210">原因</span><span class="sxs-lookup"><span data-stu-id="00140-210">Cause</span></span>
<span data-ttu-id="00140-211">暫時性網路連線錯誤。</span><span class="sxs-lookup"><span data-stu-id="00140-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-212">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-212">Resolution</span></span>
<span data-ttu-id="00140-213">請遵循這些步驟 tooget hello 閘道上線：</span><span class="sxs-lookup"><span data-stu-id="00140-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="00140-214">等候數分鐘，hello 錯誤消失時自動回復 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="00140-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="00140-215">如果 hello 錯誤持續發生，請重新啟動 hello 閘道服務。</span><span class="sxs-lookup"><span data-stu-id="00140-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="00140-216">失敗的 tooauthor 連結服務</span><span class="sxs-lookup"><span data-stu-id="00140-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="00140-217">問題</span><span class="sxs-lookup"><span data-stu-id="00140-217">Problem</span></span>
<span data-ttu-id="00140-218">嘗試 toouse 認證管理員中新的連結服務的 hello 入口 tooinput 認證或更新現有的連結服務的認證時，您可能會看到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="00140-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="00140-219">當您看到此錯誤時，hello 設定 頁面的資料管理閘道組態管理員可能會看起來像下列螢幕擷取畫面的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![無法觸達資料庫](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="00140-221">原因</span><span class="sxs-lookup"><span data-stu-id="00140-221">Cause</span></span>
<span data-ttu-id="00140-222">hello SSL 憑證可能會遺失 hello 閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="00140-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="00140-223">hello 閘道電腦無法載入 hello 目前使用憑證進行 SSL 加密。</span><span class="sxs-lookup"><span data-stu-id="00140-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="00140-224">您也可能會看到類似下列訊息的 toohello 的 hello 事件記錄檔中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="00140-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="00140-225">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-225">Resolution</span></span>
<span data-ttu-id="00140-226">請遵循這些步驟 toosolve hello 問題：</span><span class="sxs-lookup"><span data-stu-id="00140-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="00140-227">啟動「資料管理閘道組態管理員」。</span><span class="sxs-lookup"><span data-stu-id="00140-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="00140-228">切換 toohello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="00140-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="00140-229">按一下 hello**變更**按鈕 toochange hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![變更憑證按鈕](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="00140-231">選取新的憑證，做為 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="00140-232">您可以使用您自己或任何組織所產生的任何 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="00140-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![指定憑證](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="00140-234">複製活動失敗</span><span class="sxs-lookup"><span data-stu-id="00140-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="00140-235">問題</span><span class="sxs-lookup"><span data-stu-id="00140-235">Problem</span></span>
<span data-ttu-id="00140-236">您可能會注意到 hello"UserErrorFailedToConnectToSqlserver 」 失敗之後設定 hello 入口網站中的管線之後。</span><span class="sxs-lookup"><span data-stu-id="00140-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="00140-237">原因</span><span class="sxs-lookup"><span data-stu-id="00140-237">Cause</span></span>
<span data-ttu-id="00140-238">發生的原因各有不同，而緩和方式也隨之而異。</span><span class="sxs-lookup"><span data-stu-id="00140-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="00140-239">解決方案</span><span class="sxs-lookup"><span data-stu-id="00140-239">Resolution</span></span>
<span data-ttu-id="00140-240">允許輸出 TCP 連線透過 hello 資料管理閘道用戶端上的連接埠 TCP/1433年連接 tooan SQL 資料庫之前。</span><span class="sxs-lookup"><span data-stu-id="00140-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="00140-241">如果 hello 目標資料庫是 Azure SQL database，請檢查 SQL Server 的防火牆設定 Azure 以及。</span><span class="sxs-lookup"><span data-stu-id="00140-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="00140-242">請參閱下列章節 tootest hello 連接 toohello 在內部部署資料存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="00140-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="00140-243">資料存放區連線或驅動程式相關錯誤</span><span class="sxs-lookup"><span data-stu-id="00140-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="00140-244">如果您看到資料存放區連接或驅動程式相關的錯誤，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="00140-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="00140-245">Hello 閘道機器上啟動資料管理閘道組態管理員。</span><span class="sxs-lookup"><span data-stu-id="00140-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="00140-246">切換 toohello**診斷** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="00140-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="00140-247">在**測試連接**，新增 hello 閘道群組值。</span><span class="sxs-lookup"><span data-stu-id="00140-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="00140-248">按一下**測試**toosee，如果您可以連接 toohello 內部部署資料來源從 hello 閘道機器使用 hello 連接資訊和認證。</span><span class="sxs-lookup"><span data-stu-id="00140-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="00140-249">如果之後安裝的驅動程式，仍失敗 hello 測試連接，重新啟動 hello 閘道它 toopick 向上 hello 最新變更。</span><span class="sxs-lookup"><span data-stu-id="00140-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![在 [診斷] 索引標籤中的測試連接](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="00140-251">閘道記錄檔</span><span class="sxs-lookup"><span data-stu-id="00140-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="00140-252">傳送閘道記錄檔 tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="00140-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="00140-253">當您連絡 Microsoft 支援服務 tooget 說明閘道的問題進行疑難排解時，可能會要求您 tooshare 您閘道記錄檔。</span><span class="sxs-lookup"><span data-stu-id="00140-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="00140-254">Hello 版的 hello 閘道，您可以共用兩個按鈕按一下在資料管理閘道組態管理員需要的閘道記錄檔。</span><span class="sxs-lookup"><span data-stu-id="00140-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="00140-255">切換 toohello**診斷**在資料管理閘道組態管理員 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="00140-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![資料管理閘道診斷索引標籤](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="00140-257">按一下**傳送記錄檔**toosee hello 下列對話方塊。</span><span class="sxs-lookup"><span data-stu-id="00140-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![資料管理閘道傳送記錄檔](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="00140-259">（選擇性）按一下**檢視記錄檔**tooreview 記錄 hello 事件檢視器中。</span><span class="sxs-lookup"><span data-stu-id="00140-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="00140-260">（選擇性）按一下**隱私權**tooreview Microsoft web services 隱私權聲明。</span><span class="sxs-lookup"><span data-stu-id="00140-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="00140-261">當您滿意 tooupload 有關為何時，按一下 **傳送記錄檔**tooactually 從 hello 過去七天 tooMicrosoft 疑難排解傳送嗨記錄檔。</span><span class="sxs-lookup"><span data-stu-id="00140-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="00140-262">Hello 下列螢幕擷取畫面所示，您應該看到 hello hello 傳送記錄檔作業狀態。</span><span class="sxs-lookup"><span data-stu-id="00140-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![資料管理閘道傳送記錄檔狀態](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="00140-264">Hello 作業已完成之後，您會看到一個對話方塊 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="00140-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![資料管理閘道傳送記錄檔狀態](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="00140-266">儲存 hello**報表識別碼**及共用向 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="00140-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="00140-267">使用的 toolocate hello 閘道記錄檔取得疑難排解您上傳 hello 報表 ID。</span><span class="sxs-lookup"><span data-stu-id="00140-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="00140-268">hello 報表識別碼也會儲存在 hello 事件檢視器。</span><span class="sxs-lookup"><span data-stu-id="00140-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="00140-269">您可以藉由查看 hello 事件識別碼 」 25"，找到它，並檢查 hello 日期和時間。</span><span class="sxs-lookup"><span data-stu-id="00140-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![資料管理閘道傳送記錄檔報告識別碼](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="00140-271">在閘道主機電腦上封存閘道記錄檔</span><span class="sxs-lookup"><span data-stu-id="00140-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="00140-272">在某些情況下，您會有閘道問題但無法直接共用閘道記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="00140-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="00140-273">手動安裝 hello 閘道，並註冊 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="00140-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="00140-274">您可以嘗試 tooregister hello 閘道使用重新產生金鑰在資料管理閘道組態管理員。</span><span class="sxs-lookup"><span data-stu-id="00140-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="00140-275">您嘗試 toosend 記錄檔，而且 hello 閘道器主機服務無法連線。</span><span class="sxs-lookup"><span data-stu-id="00140-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="00140-276">對於這些案例，您可以將閘道記錄檔儲存為 zip 檔案，並在連絡 Microsoft 支援服務時共用。</span><span class="sxs-lookup"><span data-stu-id="00140-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="00140-277">比方說，如果您註冊為 hello 閘道時，收到錯誤，顯示 hello 下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="00140-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![資料管理閘道註冊錯誤](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="00140-279">按一下 hello**封存閘道記錄檔**連結 tooarchive 和儲存記錄檔，然後向 Microsoft 支援共用 hello zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="00140-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![資料管理閘道封存記錄檔](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="00140-281">找出閘道記錄檔</span><span class="sxs-lookup"><span data-stu-id="00140-281">Locate gateway logs</span></span>
<span data-ttu-id="00140-282">您可以在 hello Windows 事件記錄檔中找到詳細的閘道記錄檔資訊。</span><span class="sxs-lookup"><span data-stu-id="00140-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="00140-283">啟動 Windows **事件檢視器**。</span><span class="sxs-lookup"><span data-stu-id="00140-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="00140-284">找出記錄檔中 hello **Application and Services Logs** > **資料管理閘道器**資料夾。</span><span class="sxs-lookup"><span data-stu-id="00140-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="00140-285">當您正在將閘道器相關的問題進行疑難排解時，查看 hello 事件檢視器中的錯誤層級事件。</span><span class="sxs-lookup"><span data-stu-id="00140-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![資料管理閘道事件檢視器中的記錄檔](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
