---
title: "Azure AD Connect：啟用裝置回寫 | Microsoft Docs"
description: "此文件詳細資料時，如何使用 Azure AD Connect tooenable 裝置回寫"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a><span data-ttu-id="a63de-103">Azure AD Connect：啟用裝置回寫</span><span class="sxs-lookup"><span data-stu-id="a63de-103">Azure AD Connect: Enabling device writeback</span></span>
> [!NOTE]
> <span data-ttu-id="a63de-104">用於裝置回寫需要訂用帳戶 tooAzure AD Premium。</span><span class="sxs-lookup"><span data-stu-id="a63de-104">A subscription tooAzure AD Premium is required for device writeback.</span></span>
> 
> 

<span data-ttu-id="a63de-105">下列文件的 hello 提供有關在 Azure AD Connect tooenable hello 裝置回寫功能的方式。</span><span class="sxs-lookup"><span data-stu-id="a63de-105">hello following documentation provides information on how tooenable hello device writeback feature in Azure AD Connect.</span></span> <span data-ttu-id="a63de-106">裝置回寫用於下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="a63de-106">Device Writeback is used in hello following scenarios:</span></span>

* <span data-ttu-id="a63de-107">啟用條件式存取，根據裝置 tooADFS (2012 R2 或更高版本) 受保護的應用程式 （信賴憑證者信任）。</span><span class="sxs-lookup"><span data-stu-id="a63de-107">Enable conditional access based on devices tooADFS (2012 R2 or higher) protected applications (relying party trusts).</span></span>

<span data-ttu-id="a63de-108">這會提供額外的安全性，並只 tootrusted 裝置授與存取 tooapplications 的保證。</span><span class="sxs-lookup"><span data-stu-id="a63de-108">This provides additional security and assurance that access tooapplications is granted only tootrusted devices.</span></span> <span data-ttu-id="a63de-109">如需條件式存取的詳細資訊，請參閱[使用條件式存取管理風險](../active-directory-conditional-access.md)和[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](../active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="a63de-109">For more information on conditional access, see [Managing Risk with Conditional Access](../active-directory-conditional-access.md) and [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

> [!IMPORTANT]
> <li><span data-ttu-id="a63de-110">裝置必須位於相同樹系為 hello 使用者 hello。</span><span class="sxs-lookup"><span data-stu-id="a63de-110">Devices must be located in hello same forest as hello users.</span></span> <span data-ttu-id="a63de-111">裝置必須重新寫入 tooa 單一樹系，因為這項功能目前不支援使用多個使用者樹系的部署。</span><span class="sxs-lookup"><span data-stu-id="a63de-111">Since devices must be written back tooa single forest, this feature does not currently support a deployment with multiple user forests.</span></span></li>
> <li><span data-ttu-id="a63de-112">只有一個裝置註冊設定的物件可以加入 toohello 在內部部署 Active Directory 樹系。</span><span class="sxs-lookup"><span data-stu-id="a63de-112">Only one device registration configuration object can be added toohello on-premises Active Directory forest.</span></span> <span data-ttu-id="a63de-113">這項功能與不相容的拓樸其中 hello 內部部署 Active Directory 是已同步處理的 toomultiple Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="a63de-113">This feature is not compatible with a topology where hello on-premises Active Directory is synchronized toomultiple Azure AD directories.</span></span></li>> 

## <a name="part-1-install-azure-ad-connect"></a><span data-ttu-id="a63de-114">第 1 部分：安裝 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a63de-114">Part 1: Install Azure AD Connect</span></span>
1. <span data-ttu-id="a63de-115">使用自訂或快速設定安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="a63de-115">Install Azure AD Connect using Custom or Express settings.</span></span> <span data-ttu-id="a63de-116">Microsoft 建議 toostart 與所有使用者和群組已順利同步處理之前啟用裝置回寫。</span><span class="sxs-lookup"><span data-stu-id="a63de-116">Microsoft recommends toostart with all users and groups successfully synchronized before you enable device writeback.</span></span>

## <a name="part-2-prepare-active-directory"></a><span data-ttu-id="a63de-117">第 2 部分：準備 Active Directory</span><span class="sxs-lookup"><span data-stu-id="a63de-117">Part 2: Prepare Active Directory</span></span>
<span data-ttu-id="a63de-118">使用下列步驟 tooprepare 使用於裝置回寫的 hello。</span><span class="sxs-lookup"><span data-stu-id="a63de-118">Use hello following steps tooprepare for using device writeback.</span></span>

1. <span data-ttu-id="a63de-119">從已安裝 Azure AD Connect 的 hello 機器，請在提升權限模式下啟動 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a63de-119">From hello machine where Azure AD Connect is installed, launch PowerShell in elevated mode.</span></span>
2. <span data-ttu-id="a63de-120">如果未安裝 hello Active Directory PowerShell 模組，使用安裝 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a63de-120">If hello Active Directory PowerShell module is NOT installed, install it using hello following command:</span></span>
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. <span data-ttu-id="a63de-121">如果未安裝 hello Azure Active Directory PowerShell 模組，請下載並安裝從[Azure Active Directory 的 Windows PowerShell 模組 （64 位元版本）](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="a63de-121">If hello Azure Active Directory PowerShell module is NOT installed, then download and install it from [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span> <span data-ttu-id="a63de-122">此元件具有相依性 hello 登入小幫手，它會隨 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="a63de-122">This component has a dependency on hello sign-in assistant, which is installed with Azure AD Connect.</span></span>
4. <span data-ttu-id="a63de-123">使用企業系統管理員認證，執行下列命令的 hello，然後結束 [PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a63de-123">With enterprise admin credentials, run hello following commands and then exit PowerShell.</span></span>
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

<span data-ttu-id="a63de-124">企業系統管理員認證是必要的因為所需的變更 toohello 組態命名空間。</span><span class="sxs-lookup"><span data-stu-id="a63de-124">Enterprise admin credentials are required since changes toohello configuration namespace are needed.</span></span> <span data-ttu-id="a63de-125">網域系統管理員沒有足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="a63de-125">A domain admin will not have enough permissions.</span></span>

![啟用裝置回寫的 Powershell](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

<span data-ttu-id="a63de-127">Description:</span><span class="sxs-lookup"><span data-stu-id="a63de-127">Description:</span></span>

* <span data-ttu-id="a63de-128">如果尚未存在，請在 CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn] 下方建立並設定新的容器和物件。</span><span class="sxs-lookup"><span data-stu-id="a63de-128">If they do not exist already, creates and configures new containers and objects under CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span></span>
* <span data-ttu-id="a63de-129">如果尚未存在，請在 CN=RegisteredDevices,[domain-dn] 下方建立並設定新的容器和物件。</span><span class="sxs-lookup"><span data-stu-id="a63de-129">If they do not exist already, creates and configures new containers and objects under CN=RegisteredDevices,[domain-dn].</span></span> <span data-ttu-id="a63de-130">將會在此容器中建立裝置物件。</span><span class="sxs-lookup"><span data-stu-id="a63de-130">Device objects will be created in this container.</span></span>
* <span data-ttu-id="a63de-131">設定 hello Azure AD 連接器帳戶，請在您的 Active Directory toomanage 裝置必要的權限。</span><span class="sxs-lookup"><span data-stu-id="a63de-131">Sets necessary permissions on hello Azure AD Connector account, toomanage devices on your Active Directory.</span></span>
* <span data-ttu-id="a63de-132">如果即使在多個樹系上安裝 Azure AD Connect，只需要 toorun 上有一個樹系。</span><span class="sxs-lookup"><span data-stu-id="a63de-132">Only needs toorun on one forest, even if Azure AD Connect is being installed on multiple forests.</span></span>

<span data-ttu-id="a63de-133">參數：</span><span class="sxs-lookup"><span data-stu-id="a63de-133">Parameters:</span></span>

* <span data-ttu-id="a63de-134">DomainName：將建立裝置物件的 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="a63de-134">DomainName: Active Directory Domain where device objects will be created.</span></span> <span data-ttu-id="a63de-135">附註：指定的 Active Directory 樹系的所有裝置都會在單一網域中建立。</span><span class="sxs-lookup"><span data-stu-id="a63de-135">Note: All devices for a given Active Directory forest will be created in a single domain.</span></span>
* <span data-ttu-id="a63de-136">AdConnectorAccount: Hello 目錄中的 Azure AD Connect toomanage 物件將會使用 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a63de-136">AdConnectorAccount: Active Directory account that will be used by Azure AD Connect toomanage objects in hello directory.</span></span> <span data-ttu-id="a63de-137">這是使用 Azure AD Connect 同步處理 tooconnect tooAD hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a63de-137">This is hello account used by Azure AD Connect sync tooconnect tooAD.</span></span> <span data-ttu-id="a63de-138">如果您使用快速設定安裝，它就會是加上 MSOL_ hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a63de-138">If you installed using express settings, it is hello account prefixed with MSOL_.</span></span>

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a><span data-ttu-id="a63de-139">第 3 部分：在 Azure AD Connect 中啟用裝置回寫功能</span><span class="sxs-lookup"><span data-stu-id="a63de-139">Part 3: Enable device writeback in Azure AD Connect</span></span>
<span data-ttu-id="a63de-140">使用下列程序 tooenable 裝置回寫，在 Azure AD Connect 的 hello。</span><span class="sxs-lookup"><span data-stu-id="a63de-140">Use hello following procedure tooenable device writeback in Azure AD Connect.</span></span>

1. <span data-ttu-id="a63de-141">再次執行 hello 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="a63de-141">Run hello installation wizard again.</span></span> <span data-ttu-id="a63de-142">選取**自訂同步處理選項**hello 其他工作的頁面上，按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a63de-142">Select **customize synchronization options** from hello Additional Tasks page and click **Next**.</span></span>
   <span data-ttu-id="a63de-143">![自訂安裝自訂同步處理選項](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-143">![Custom Install customize synchronization options](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span></span>
2. <span data-ttu-id="a63de-144">在 hello 選擇性功能] 頁面上，裝置回寫將不再會變成灰色。請注意，是否 hello Azure AD Connect 的準備步驟尚未完成裝置回寫將會以灰色顯示出 hello 選擇性功能] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="a63de-144">In hello Optional Features page, device writeback will no longer be grayed out. Please note that if hello Azure AD Connect prep steps are not completed device writeback will be grayed out in hello Optional features page.</span></span> <span data-ttu-id="a63de-145">核取 hello 用於裝置回寫] 方塊，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a63de-145">Check hello box for device writeback and click **next**.</span></span> <span data-ttu-id="a63de-146">如果仍然已停用 hello 核取方塊，請參閱 hello[疑難排解 > 一節](#the-writeback-checkbox-is-still-disabled)。</span><span class="sxs-lookup"><span data-stu-id="a63de-146">If hello checkbox is still disabled, see hello [troubleshooting section](#the-writeback-checkbox-is-still-disabled).</span></span>
   <span data-ttu-id="a63de-147">![自訂安裝裝置回寫可選功能](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-147">![Custom install Device Writeback optional features](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span></span>
3. <span data-ttu-id="a63de-148">在 hello 回寫頁面上，您會看到 hello 提供網域以 hello 預設裝置回寫的樹系。</span><span class="sxs-lookup"><span data-stu-id="a63de-148">On hello writeback page, you will see hello supplied domain as hello default Device writeback forest.</span></span>
   <span data-ttu-id="a63de-149">![自訂安全裝置回寫樹系](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-149">![Custom Install device writeback target forest](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span></span>
4. <span data-ttu-id="a63de-150">完成安裝 hello hello 精靈而不變更其他設定。</span><span class="sxs-lookup"><span data-stu-id="a63de-150">Complete hello installation of hello Wizard with no additional configuration changes.</span></span> <span data-ttu-id="a63de-151">如有需要請參閱太[的 Azure AD Connect 自訂安裝。](active-directory-aadconnect-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="a63de-151">If needed, refer too[Custom installation of Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)</span></span>

## <a name="enable-conditional-access"></a><span data-ttu-id="a63de-152">啟用條件式存取</span><span class="sxs-lookup"><span data-stu-id="a63de-152">Enable conditional access</span></span>
<span data-ttu-id="a63de-153">此案例中所提供的詳細的指示 tooenable[設定使用 Azure Active Directory 裝置註冊的內部部署條件式存取](../active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="a63de-153">Detailed instructions tooenable this scenario are available within [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>

## <a name="verify-devices-are-synchronized-tooactive-directory"></a><span data-ttu-id="a63de-154">確認裝置已同步處理的 tooActive 目錄</span><span class="sxs-lookup"><span data-stu-id="a63de-154">Verify Devices are synchronized tooActive Directory</span></span>
<span data-ttu-id="a63de-155">裝置回寫現在應該正常運作。</span><span class="sxs-lookup"><span data-stu-id="a63de-155">Device writeback should now be working properly.</span></span> <span data-ttu-id="a63de-156">請注意，就可以在裝置物件 toobe 寫回 tooAD too3 小時。</span><span class="sxs-lookup"><span data-stu-id="a63de-156">Be aware that it can take up too3 hours for device objects toobe written-back tooAD.</span></span>  <span data-ttu-id="a63de-157">您的裝置會正常運作，同步 tooverify hello 後完成 hello 同步處理規則：</span><span class="sxs-lookup"><span data-stu-id="a63de-157">tooverify that your devices are being synced properly, do hello following after hello sync rules complete:</span></span>

1. <span data-ttu-id="a63de-158">啟動 Active Directory 管理中心。</span><span class="sxs-lookup"><span data-stu-id="a63de-158">Launch Active Directory Administrative Center.</span></span>
2. <span data-ttu-id="a63de-159">展開 RegisteredDevices，hello 正在同盟的網域內。</span><span class="sxs-lookup"><span data-stu-id="a63de-159">Expand RegisteredDevices, within hello Domain that is being federated.</span></span>
   <span data-ttu-id="a63de-160">![Active Directory 管理中心已註冊的裝置](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-160">![Active Directory Admin Center Registered Devices](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span></span>
3. <span data-ttu-id="a63de-161">此處會列出目前已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="a63de-161">Current registered devices will be listed there.</span></span>
   <span data-ttu-id="a63de-162">![Active Directory 管理中心已註冊的裝置清單](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-162">![Active Directory Admin Center Registered Devices List](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a63de-163">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a63de-163">Troubleshooting</span></span>
### <a name="hello-writeback-checkbox-is-still-disabled"></a><span data-ttu-id="a63de-164">仍然停用 hello 回寫] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="a63de-164">hello writeback checkbox is still disabled</span></span>
<span data-ttu-id="a63de-165">如果 hello 核取方塊，即使您已依照 hello 上述步驟，未啟用裝置回寫 hello 下列步驟將引導您完成哪些 hello 安裝精靈正在驗證啟用 hello 方塊之前。</span><span class="sxs-lookup"><span data-stu-id="a63de-165">If hello checkbox for device writeback is not enabled even though you have followed hello steps above, hello following steps will guide you through what hello installation wizard is verifying before hello box is enabled.</span></span>

<span data-ttu-id="a63de-166">首先：</span><span class="sxs-lookup"><span data-stu-id="a63de-166">First things first:</span></span>

* <span data-ttu-id="a63de-167">確定至少有一個樹系具備 Windows Server 2012R2。</span><span class="sxs-lookup"><span data-stu-id="a63de-167">Make sure at least one forest has Windows Server 2012R2.</span></span> <span data-ttu-id="a63de-168">hello 裝置物件型別必須要有。</span><span class="sxs-lookup"><span data-stu-id="a63de-168">hello device object type must be present.</span></span>
* <span data-ttu-id="a63de-169">Hello 安裝精靈已在執行中，如果任何變更將無法偵測。</span><span class="sxs-lookup"><span data-stu-id="a63de-169">If hello installation wizard is already running, then any changes will not be detected.</span></span> <span data-ttu-id="a63de-170">在此情況下，完成 hello 安裝精靈，然後再次執行。</span><span class="sxs-lookup"><span data-stu-id="a63de-170">In this case, complete hello installation wizard and run it again.</span></span>
* <span data-ttu-id="a63de-171">請確定您提供 hello 初始化指令碼中的 hello 帳戶是實際 hello 正確的使用者使用 hello Active Directory 連接器。</span><span class="sxs-lookup"><span data-stu-id="a63de-171">Make sure hello account you provide in hello initialization script is actually hello correct user used by hello Active Directory Connector.</span></span> <span data-ttu-id="a63de-172">tooverify，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a63de-172">tooverify this, follow these steps:</span></span>
  * <span data-ttu-id="a63de-173">從 hello 開始] 功能表開啟**同步處理服務**。</span><span class="sxs-lookup"><span data-stu-id="a63de-173">From hello start menu, open **Synchronization Service**.</span></span>
  * <span data-ttu-id="a63de-174">開啟 hello**連接器**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a63de-174">Open hello **Connectors** tab.</span></span>
  * <span data-ttu-id="a63de-175">類型為 Active Directory 網域服務尋找 hello 連接器並選取它。</span><span class="sxs-lookup"><span data-stu-id="a63de-175">Find hello Connector with type Active Directory Domain Services and select it.</span></span>
  * <span data-ttu-id="a63de-176">選取 [動作] 下方的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="a63de-176">Under **Actions**, select **Properties**.</span></span>
  * <span data-ttu-id="a63de-177">跳過**連接 tooActive Directory 樹系**。</span><span class="sxs-lookup"><span data-stu-id="a63de-177">Go too**Connect tooActive Directory Forest**.</span></span> <span data-ttu-id="a63de-178">請確認此畫面相符 hello 提供帳戶 toohello 指令碼中指定該 hello 網域和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a63de-178">Verify that hello domain and user name specified on this screen match hello account provided toohello script.</span></span>
    <span data-ttu-id="a63de-179">![Sync Service Manager 中的連接器帳戶](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span><span class="sxs-lookup"><span data-stu-id="a63de-179">![Connector account in Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span></span>

<span data-ttu-id="a63de-180">確認 Active Directory 中的組態：</span><span class="sxs-lookup"><span data-stu-id="a63de-180">Verify configuration in Active Directory:</span></span>

* <span data-ttu-id="a63de-181">請確認該裝置註冊服務位於以下 hello 位置中的 hello (CN = DeviceRegistrationService，CN = 裝置註冊服務，CN = Device Registration Configuration，CN = Services，CN = Configuration) 下設定命名內容。</span><span class="sxs-lookup"><span data-stu-id="a63de-181">Verify that hello Device Registration Service is located in hello location below (CN=DeviceRegistrationService,CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration) under configuration naming context.</span></span>

![疑難排解，組態命名空間中的 DeviceRegistrationService](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* <span data-ttu-id="a63de-183">確認有只有一個組態物件藉由搜尋 hello 組態命名空間。</span><span class="sxs-lookup"><span data-stu-id="a63de-183">Verify there is only one configuration object by searching hello configuration namespace.</span></span> <span data-ttu-id="a63de-184">如果有一個以上，刪除 hello 重複項目。</span><span class="sxs-lookup"><span data-stu-id="a63de-184">If there is more than one, delete hello duplicate.</span></span>

![疑難排解，請搜尋 hello 重複物件](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* <span data-ttu-id="a63de-186">在 [hello 裝置註冊服務物件，請確定 hello 屬性 Msds-primary-computer DeviceLocation 存在且具有值。</span><span class="sxs-lookup"><span data-stu-id="a63de-186">On hello Device Registration Service object, make sure hello attribute msDS-DeviceLocation is present and has a value.</span></span> <span data-ttu-id="a63de-187">查閱此位置，請確定它存在於與 hello objectType Msds-primary-computer DeviceContainer。</span><span class="sxs-lookup"><span data-stu-id="a63de-187">Lookup this location and make sure it is present with hello objectType msDS-DeviceContainer.</span></span>

![疑難排解，msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![疑難排解，RegisteredDevices 物件類別](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* <span data-ttu-id="a63de-190">請確認 hello 所使用帳戶 hello Active Directory 連接器 hello 上一個步驟所找到的 hello 註冊的裝置容器上具有必要權限。</span><span class="sxs-lookup"><span data-stu-id="a63de-190">Verify hello account used by hello Active Directory Connector has required permissions on hello Registered Devices container found by hello previous step.</span></span> <span data-ttu-id="a63de-191">這是預期的 hello 這個容器上的權限：</span><span class="sxs-lookup"><span data-stu-id="a63de-191">This is hello expected permissions on this container:</span></span>

![疑難排解，驗證容器上的權限](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* <span data-ttu-id="a63de-193">確認 hello Active Directory 帳戶擁有權限 hello CN = Device Registration Configuration，CN = Services，CN = 組態物件。</span><span class="sxs-lookup"><span data-stu-id="a63de-193">Verify hello Active Directory account has permissions on hello CN=Device Registration Configuration,CN=Services,CN=Configuration object.</span></span>

![疑難排解，，驗證裝置註冊組態的權限](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a><span data-ttu-id="a63de-195">其他資訊</span><span class="sxs-lookup"><span data-stu-id="a63de-195">Additional Information</span></span>
* [<span data-ttu-id="a63de-196">使用條件式存取管理風險</span><span class="sxs-lookup"><span data-stu-id="a63de-196">Managing Risk With Conditional Access</span></span>](../active-directory-conditional-access.md)
* [<span data-ttu-id="a63de-197">使用 Azure Active Directory 裝置註冊設定內部部署條件式存取</span><span class="sxs-lookup"><span data-stu-id="a63de-197">Setting up On-premises Conditional Access using Azure Active Directory Device Registration</span></span>](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a><span data-ttu-id="a63de-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a63de-198">Next steps</span></span>
<span data-ttu-id="a63de-199">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="a63de-199">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

