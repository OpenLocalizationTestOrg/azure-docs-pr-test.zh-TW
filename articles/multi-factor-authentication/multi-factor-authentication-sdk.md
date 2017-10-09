---
title: "aaaMFA 軟體開發套件的自訂應用程式 |Microsoft 文件"
description: "本文章將示範如何 toodownload 並用 hello Azure MFA SDK tooenable 雙步驟驗證，您的自訂應用程式。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="39890-103">在自訂應用程式中建置 Multi-Factor Authentication (SDK)</span><span class="sxs-lookup"><span data-stu-id="39890-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="39890-104">hello Azure Multi-factor Authentication 軟體開發套件 (SDK) 可讓您建置兩步驟驗證直接內建 hello 登入或交易程序的 Azure AD 租用戶中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="39890-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="39890-105">hello Multi-factor Authentication SDK 適用於 C#、 Visual Basic (.NET)、 Java、 Perl、 PHP 和 Ruby。</span><span class="sxs-lookup"><span data-stu-id="39890-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="39890-106">hello SDK 提供了雙步驟驗證的精簡型包裝函式。</span><span class="sxs-lookup"><span data-stu-id="39890-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="39890-107">它包含所需的所有 toowrite 您的程式碼，包括加註的原始程式碼檔案、 範例檔案，以及詳細的 ReadMe 檔案。</span><span class="sxs-lookup"><span data-stu-id="39890-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="39890-108">每一套 SDK 也包含憑證和私密金鑰的加密是唯一 tooyour Multi-factor Authentication 提供者的交易。</span><span class="sxs-lookup"><span data-stu-id="39890-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="39890-109">只要您有的提供者，您就可以視需要下載 hello SDK 為多種語言和格式。</span><span class="sxs-lookup"><span data-stu-id="39890-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="39890-110">hello Api hello Multi-factor Authentication SDK 中的 hello 結構很簡單。</span><span class="sxs-lookup"><span data-stu-id="39890-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="39890-111">請呼叫 tooan API （例如驗證模式） 的 hello 多因素選項參數與使用者資料 （例如 hello 電話號碼 toocall 或 hello 的 PIN 號碼 toovalidate） 的單一函式。</span><span class="sxs-lookup"><span data-stu-id="39890-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="39890-112">hello Api 轉譯 hello 函式呼叫 web 服務要求 toohello 雲端型 Azure Multi-factor Authentication 服務。</span><span class="sxs-lookup"><span data-stu-id="39890-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="39890-113">所有呼叫必須都包含參考 toohello 私用憑證包含在每個 SDK 中。</span><span class="sxs-lookup"><span data-stu-id="39890-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="39890-114">因為 hello 應用程式開發介面不需要存取 toousers Azure Active Directory 中登錄，您必須提供檔案或資料庫中的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="39890-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="39890-115">此外，hello 應用程式開發介面不會提供註冊或使用者管理功能，因此您需要 toobuild 這些應用程式的處理程序。</span><span class="sxs-lookup"><span data-stu-id="39890-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39890-116">toodownload hello SDK，您需要 toocreate Azure Multi-factor Auth 提供者，即使您的 Azure MFA、 AAD Premium 或 EMS 授權數量。</span><span class="sxs-lookup"><span data-stu-id="39890-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="39890-117">如果您針對此用途建立 Azure Multi-factor Auth 提供者，並已經有授權，請確定 toocreate hello 提供者以 hello**每個已啟用的使用者**模型。</span><span class="sxs-lookup"><span data-stu-id="39890-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="39890-118">然後，連結 hello 包含 hello Azure MFA、 Azure AD Premium 或 EMS 授權提供者 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="39890-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="39890-119">此組態可確保，您才需要付費如果您有多個唯一的使用者使用 hello SDK 比 hello 您所擁有的授權數目。</span><span class="sxs-lookup"><span data-stu-id="39890-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="39890-120">下載 SDK hello</span><span class="sxs-lookup"><span data-stu-id="39890-120">Download hello SDK</span></span>
<span data-ttu-id="39890-121">下載 Azure Multi-factor Authentication SDK hello 需要[Azure 多因素驗證提供者](multi-factor-authentication-get-started-auth-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="39890-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="39890-122">即使您擁有 Azure MFA、Azure AD Premium 或 Enterprise Mobility Suite 授權，這還是需要完整的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="39890-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="39890-123">toodownload hello SDK，瀏覽 toohello Multi-factor Authentication 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="39890-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="39890-124">您可能會達到 hello 入口網站管理 hello 直接，Multi-factor Auth 提供者，或按一下 hello **「 Go toohello 入口網站 」** hello MFA 服務設定 頁面上的連結。</span><span class="sxs-lookup"><span data-stu-id="39890-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="39890-125">從 hello Azure 傳統入口網站下載</span><span class="sxs-lookup"><span data-stu-id="39890-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="39890-126">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="39890-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="39890-127">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="39890-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="39890-128">在 hello Active Directory 頁面上，在 hello 頂端選取**Multi-factor Auth 提供者**</span><span class="sxs-lookup"><span data-stu-id="39890-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="39890-129">Hello 底部選取**管理**。</span><span class="sxs-lookup"><span data-stu-id="39890-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="39890-130">新的頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="39890-130">A new page opens.</span></span>
5. <span data-ttu-id="39890-131">按一下左，請在 hello 下方的 hello **SDK**。</span><span class="sxs-lookup"><span data-stu-id="39890-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="39890-132"><center>![下載](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="39890-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="39890-133">選取 hello 語言，然後按一下一個 hello 相關的下載連結。</span><span class="sxs-lookup"><span data-stu-id="39890-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="39890-134">Hello 下載檔案的儲存。</span><span class="sxs-lookup"><span data-stu-id="39890-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="39890-135">下載從 hello 服務設定</span><span class="sxs-lookup"><span data-stu-id="39890-135">Download from hello service settings</span></span>
1. <span data-ttu-id="39890-136">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="39890-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="39890-137">Hello 左側選取**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="39890-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="39890-138">按兩下您的 Azure AD 執行個體。</span><span class="sxs-lookup"><span data-stu-id="39890-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="39890-139">在 hello 頂端按一下**設定**</span><span class="sxs-lookup"><span data-stu-id="39890-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="39890-140">在多因素驗證底下選取 **管理服務設定**
   ![下載](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="39890-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="39890-141">在 hello 服務設定 頁面上，在 hello 囉 」 畫面底部按一下**Go toohello 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="39890-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="39890-142">新的頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="39890-142">A new page opens.</span></span>
   <span data-ttu-id="39890-143">![下載](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="39890-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="39890-144">按一下左，請在 hello 下方的 hello **SDK**。</span><span class="sxs-lookup"><span data-stu-id="39890-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="39890-145">選取 hello 語言，然後按一下一個 hello 相關的下載連結。</span><span class="sxs-lookup"><span data-stu-id="39890-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="39890-146">Hello 下載檔案的儲存。</span><span class="sxs-lookup"><span data-stu-id="39890-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="39890-147">功能的 hello SDK</span><span class="sxs-lookup"><span data-stu-id="39890-147">What's in hello SDK</span></span>
<span data-ttu-id="39890-148">hello SDK 包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="39890-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="39890-149">**讀我檔案**。</span><span class="sxs-lookup"><span data-stu-id="39890-149">**README**.</span></span> <span data-ttu-id="39890-150">說明如何 toouse hello 新的或現有的應用程式中的多因素驗證應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="39890-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="39890-151">**原始程式檔**，用於 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="39890-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="39890-152">**用戶端憑證**toocommunicate 使用 hello Multi-factor Authentication 服務</span><span class="sxs-lookup"><span data-stu-id="39890-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="39890-153">**私用金鑰**hello 憑證</span><span class="sxs-lookup"><span data-stu-id="39890-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="39890-154">**呼叫結果。**</span><span class="sxs-lookup"><span data-stu-id="39890-154">**Call results.**</span></span> <span data-ttu-id="39890-155">呼叫結果碼的清單。</span><span class="sxs-lookup"><span data-stu-id="39890-155">A list of call result codes.</span></span> <span data-ttu-id="39890-156">tooopen 此檔案，請使用文字格式，例如 WordPad 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="39890-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="39890-157">使用 hello 呼叫結果碼 tootest，並進行疑難排解的多因素驗證應用程式中的 hello 實作。</span><span class="sxs-lookup"><span data-stu-id="39890-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="39890-158">它們不是驗證狀態碼。</span><span class="sxs-lookup"><span data-stu-id="39890-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="39890-159">**範例。**</span><span class="sxs-lookup"><span data-stu-id="39890-159">**Examples.**</span></span> <span data-ttu-id="39890-160">Multi-Factor Authentication 基本工作實作的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="39890-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="39890-161">hello 用戶端憑證是特別為您產生的唯一私密憑證。</span><span class="sxs-lookup"><span data-stu-id="39890-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="39890-162">請勿分享或遺失此檔案。</span><span class="sxs-lookup"><span data-stu-id="39890-162">Do not share or lose this file.</span></span> <span data-ttu-id="39890-163">是金鑰 tooensuring hello 與 hello Multi-factor Authentication 服務通訊的安全性。</span><span class="sxs-lookup"><span data-stu-id="39890-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="39890-164">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="39890-164">Code sample</span></span>
<span data-ttu-id="39890-165">這個程式碼範例會示範如何在 Azure Multi-factor Authentication SDK tooadd 標準模式語音 hello toouse hello 應用程式開發介面呼叫驗證 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="39890-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="39890-166">標準模式是 hello 使用者回應 tooby 按 hello # 鍵將電話通話。</span><span class="sxs-lookup"><span data-stu-id="39890-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="39890-167">這個範例會使用基本的 ASP.NET 應用程式中的 hello C#.NET 2.0 Multi-factor Authentication SDK 與 C# 伺服器端邏輯，但 hello 流程類似其他語言中。</span><span class="sxs-lookup"><span data-stu-id="39890-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="39890-168">因為 hello SDK 包含來源檔案，不是可執行檔，您可以建置 hello 檔案和參考它們或直接在您的應用程式中包含它們。</span><span class="sxs-lookup"><span data-stu-id="39890-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="39890-169">當實作多因素驗證時，使用 hello 其他方法 （通話或簡訊） 重音或第三驗證 toosupplement 為您的主要驗證方法 （使用者名稱和密碼）。</span><span class="sxs-lookup"><span data-stu-id="39890-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="39890-170">這些方法並非設計為主要驗證方法。</span><span class="sxs-lookup"><span data-stu-id="39890-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="39890-171">程式碼範例概觀</span><span class="sxs-lookup"><span data-stu-id="39890-171">Code Sample Overview</span></span>
<span data-ttu-id="39890-172">這個簡單的 web 示範應用程式的範例程式碼會使用 # 金鑰回應 tooverify hello 使用者的驗證電話通話。</span><span class="sxs-lookup"><span data-stu-id="39890-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="39890-173">此通話因素在 Multi-Factor Authentication 中稱為標準模式。</span><span class="sxs-lookup"><span data-stu-id="39890-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="39890-174">hello 用戶端程式碼不包含任何 Multi-factor Authentication 特定元素。</span><span class="sxs-lookup"><span data-stu-id="39890-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="39890-175">由於 hello 額外驗證因素與 hello 主要驗證無關，所以您可以將它們而不必變更 hello 現有登入介面。</span><span class="sxs-lookup"><span data-stu-id="39890-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="39890-176">hello Multi-factor SDK 中的 hello 應用程式開發介面可讓您自訂 hello 使用者經驗，但是您可能不需要 toochange 任何項目完全。</span><span class="sxs-lookup"><span data-stu-id="39890-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="39890-177">hello 伺服器端程式碼會加入在步驟 2 中的標準模式驗證。</span><span class="sxs-lookup"><span data-stu-id="39890-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="39890-178">它會建立具有所需的標準模式驗證的 hello 參數 PfAuthParams 物件： 使用者名稱、 電話號碼和模式，及 hello 路徑 toohello 用戶端憑證 (CertFilePath)，每個呼叫所需要的。</span><span class="sxs-lookup"><span data-stu-id="39890-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="39890-179">PfAuthParams 中的所有參數的示範，請參閱 hello SDK 中的 hello 範例檔案。</span><span class="sxs-lookup"><span data-stu-id="39890-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="39890-180">接下來，hello 程式碼會傳遞 hello PfAuthParams 物件 toohello pf_authenticate() 函式。</span><span class="sxs-lookup"><span data-stu-id="39890-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="39890-181">hello 傳回值會指出 hello 成功或失敗的 hello 驗證。</span><span class="sxs-lookup"><span data-stu-id="39890-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="39890-182">out 參數、 callStatus 和 errorID hello、 包含其他通話結果資訊。</span><span class="sxs-lookup"><span data-stu-id="39890-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="39890-183">hello 通話結果碼會記錄在 hello SDK 中的 hello 通話結果檔案。</span><span class="sxs-lookup"><span data-stu-id="39890-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="39890-184">只需要幾行就能撰寫這個最小實作。</span><span class="sxs-lookup"><span data-stu-id="39890-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="39890-185">不過，在實際執行的程式碼中，將會包含更複雜的錯誤處理、其他資料庫程式碼和強化的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="39890-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="39890-186">Web 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="39890-186">Web Client Code</span></span>
<span data-ttu-id="39890-187">hello 以下是示範頁面的 web 用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="39890-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="39890-188">伺服器端程式碼</span><span class="sxs-lookup"><span data-stu-id="39890-188">Server-Side Code</span></span>
<span data-ttu-id="39890-189">在下列伺服器端程式碼的 hello，會多因素驗證設定，並在步驟 2 中執行。</span><span class="sxs-lookup"><span data-stu-id="39890-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="39890-190">標準模式 (MODE_STANDARD) 是電話 toowhich hello 使用者回應 hello # 鍵。</span><span class="sxs-lookup"><span data-stu-id="39890-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
