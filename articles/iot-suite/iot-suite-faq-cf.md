---
title: "aaaAzure IoT 套件連線 factory 常見問題集 |Microsoft 文件"
description: "IoT 套件連線處理站的常見問題集"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a><span data-ttu-id="ca697-103">IoT 套件連線處理站預先設定之解決方案的常見問題集</span><span class="sxs-lookup"><span data-stu-id="ca697-103">Frequently asked questions for IoT Suite connected factory preconfigured solution</span></span>

<span data-ttu-id="ca697-104">另請參閱、 hello 一般[常見問題集](iot-suite-faq.md)IoT 套件。</span><span class="sxs-lookup"><span data-stu-id="ca697-104">See also, hello general [FAQ](iot-suite-faq.md) for IoT Suite.</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a><span data-ttu-id="ca697-105">可以在哪裡找到 hello 原始程式碼 hello 預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="ca697-105">Where can I find hello source code for hello preconfigured solution?</span></span>

<span data-ttu-id="ca697-106">hello 原始程式碼儲存在 hello 遵循 GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="ca697-106">hello source code is stored in hello following GitHub repository:</span></span>

* [<span data-ttu-id="ca697-107">連線處理站預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="ca697-107">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a><span data-ttu-id="ca697-108">什麼是 OPC UA？</span><span class="sxs-lookup"><span data-stu-id="ca697-108">What is OPC UA?</span></span>

<span data-ttu-id="ca697-109">2008 年推出的 OPC 統一架構 (UA) 是各平台通用的服務導向互通性標準。</span><span class="sxs-lookup"><span data-stu-id="ca697-109">OPC Unified Architecture (UA), released in 2008, is a platform-independent, service-oriented interoperability standard.</span></span> <span data-ttu-id="ca697-110">OPC UA 由各種工業系統和裝置使用，例如產業 PC、PLC 和感應器。</span><span class="sxs-lookup"><span data-stu-id="ca697-110">OPC UA is used by various industrial systems and devices such as industry PCs, PLCs, and sensors.</span></span> <span data-ttu-id="ca697-111">OPC UA 會具有內建的安全性，將 hello 傳統 OPC 規格 hello 功能整合到一種可擴充架構。</span><span class="sxs-lookup"><span data-stu-id="ca697-111">OPC UA integrates hello functionality of hello OPC Classic specifications into one extensible framework with built-in security.</span></span> <span data-ttu-id="ca697-112">它是一種標準，由 hello OPC Foundation 所驅動。</span><span class="sxs-lookup"><span data-stu-id="ca697-112">It is a standard that is driven by hello OPC Foundation.</span></span> <span data-ttu-id="ca697-113">hello [OPC Foundation](http://opcfoundation.org/) not 的收益組織具有多個 440 成員。</span><span class="sxs-lookup"><span data-stu-id="ca697-113">hello [OPC Foundation](http://opcfoundation.org/) is a not-for-profit organization with more than 440 members.</span></span> <span data-ttu-id="ca697-114">hello hello 組織目標是 toouse OPC 規格 toofacilitate 多個廠商、 多平台、 安全和可靠的互通性透過：</span><span class="sxs-lookup"><span data-stu-id="ca697-114">hello goal of hello organization is toouse OPC specifications toofacilitate multi-vendor, multi-platform, secure and reliable interoperability through:</span></span>

* <span data-ttu-id="ca697-115">基礎結構</span><span class="sxs-lookup"><span data-stu-id="ca697-115">Infrastructure</span></span>
* <span data-ttu-id="ca697-116">規格</span><span class="sxs-lookup"><span data-stu-id="ca697-116">Specifications</span></span>
* <span data-ttu-id="ca697-117">Technology</span><span class="sxs-lookup"><span data-stu-id="ca697-117">Technology</span></span>
* <span data-ttu-id="ca697-118">處理序</span><span class="sxs-lookup"><span data-stu-id="ca697-118">Processes</span></span>

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="ca697-119">為何沒有 Microsoft 選擇 hello 的 OPC UA 連接工廠預先設定的解決方案？</span><span class="sxs-lookup"><span data-stu-id="ca697-119">Why did Microsoft choose OPC UA for hello connected factory preconfigured solution?</span></span>

<span data-ttu-id="ca697-120">Microsoft 選擇 OPC UA 的原因是它是一種開放式、非專屬、與平台無關、業界認同且已核准的標準。</span><span class="sxs-lookup"><span data-stu-id="ca697-120">Microsoft chose OPC UA because it is an open, non-proprietary, platform independent, industry-recognized, and proven standard.</span></span> <span data-ttu-id="ca697-121">它是 Industrie 4.0 (RAMI4.0) 參考架構解決方案的必要項目，以確保一組廣泛製造程序與設備之間的互通性。</span><span class="sxs-lookup"><span data-stu-id="ca697-121">It is a requirement for Industrie 4.0 (RAMI4.0) reference architecture solutions ensuring interoperability between a broad set of manufacturing processes and equipment.</span></span> <span data-ttu-id="ca697-122">Microsoft 會看到從我們的客戶 toobuild Industrie 4.0 解決方案的需求。</span><span class="sxs-lookup"><span data-stu-id="ca697-122">Microsoft sees demand from our customers toobuild Industrie 4.0 solutions.</span></span> <span data-ttu-id="ca697-123">OPC UA 支援可協助客戶 tooachieve 低 hello 阻礙其目標，並提供即時商務值 toothem。</span><span class="sxs-lookup"><span data-stu-id="ca697-123">Support for OPC UA helps lower hello barrier for customers tooachieve their goals and provides immediate business value toothem.</span></span>

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a><span data-ttu-id="ca697-124">如何新增公用 IP 位址 toohello 模擬 VM？</span><span class="sxs-lookup"><span data-stu-id="ca697-124">How do I add a public IP address toohello simulation VM?</span></span>

<span data-ttu-id="ca697-125">您有兩個選項 tooadd hello IP 位址：</span><span class="sxs-lookup"><span data-stu-id="ca697-125">You have two options tooadd hello IP address:</span></span>

* <span data-ttu-id="ca697-126">使用 hello PowerShell 指令碼`Simulation/Factory/Add-SimulationPublicIp.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。</span><span class="sxs-lookup"><span data-stu-id="ca697-126">Use hello PowerShell script `Simulation/Factory/Add-SimulationPublicIp.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory).</span></span> <span data-ttu-id="ca697-127">傳遞您的部署名稱做為參數。</span><span class="sxs-lookup"><span data-stu-id="ca697-127">Pass in your deployment name as a parameter.</span></span> <span data-ttu-id="ca697-128">對於本機部署，請使用 `<your username>ConnFactoryLocal`。</span><span class="sxs-lookup"><span data-stu-id="ca697-128">For a local deployment, use `<your username>ConnFactoryLocal`.</span></span> <span data-ttu-id="ca697-129">hello 指令碼會列印出 hello 的 hello VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca697-129">hello script prints out hello IP address of hello VM.</span></span>

* <span data-ttu-id="ca697-130">在 hello Azure 入口網站，找出您的部署的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca697-130">In hello Azure portal, locate hello resource group of your deployment.</span></span> <span data-ttu-id="ca697-131">除了本機部署，您指定做為方案的 hello 名稱或部署名稱已 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca697-131">Except for a local deployment, hello resource group has hello name you specified as solution or deployment name.</span></span> <span data-ttu-id="ca697-132">Hello hello 資源群組名稱是使用 hello 組建指令碼的本機部署， `<your username>ConnFactoryLocal`。</span><span class="sxs-lookup"><span data-stu-id="ca697-132">For a local deployment using hello build script, hello name of hello resource group is `<your username>ConnFactoryLocal`.</span></span> <span data-ttu-id="ca697-133">現在，加入新**公用 IP 位址**toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca697-133">Now add a new **Public IP address** resource toohello resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="ca697-134">在任一情況下，請確定您遵循 hello hello 指示安裝 hello 最新修補程式[Ubuntu 網站](https://wiki.ubuntu.com/Security/Upgrades)。</span><span class="sxs-lookup"><span data-stu-id="ca697-134">In either case, ensure you install hello latest patches by following hello instructions on hello [Ubuntu website](https://wiki.ubuntu.com/Security/Upgrades).</span></span> <span data-ttu-id="ca697-135">只要您的 VM 可透過公用 IP 位址存取保留的 toodate 向上 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="ca697-135">Keep hello installation up toodate for as long as your VM is accessible through a public IP address.</span></span>

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a><span data-ttu-id="ca697-136">如何移除 hello 公用 IP 位址 toohello 模擬 VM？</span><span class="sxs-lookup"><span data-stu-id="ca697-136">How do I remove hello public IP address toohello simulation VM?</span></span>

<span data-ttu-id="ca697-137">您有兩個選項 tooremove hello IP 位址：</span><span class="sxs-lookup"><span data-stu-id="ca697-137">You have two options tooremove hello IP address:</span></span>

* <span data-ttu-id="ca697-138">使用 PowerShell 指令碼的 hello Simulation/Factory/Remove-SimulationPublicIp.ps1 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。</span><span class="sxs-lookup"><span data-stu-id="ca697-138">Use hello PowerShell script Simulation/Factory/Remove-SimulationPublicIp.ps1 of hello [repository](https://github.com/Azure/azure-iot-connected-factory).</span></span> <span data-ttu-id="ca697-139">傳遞您的部署名稱做為參數。</span><span class="sxs-lookup"><span data-stu-id="ca697-139">Pass in your deployment name as a parameter.</span></span> <span data-ttu-id="ca697-140">對於本機部署，請使用 `<your username>ConnFactoryLocal`。</span><span class="sxs-lookup"><span data-stu-id="ca697-140">For a local deployment, use `<your username>ConnFactoryLocal`.</span></span> <span data-ttu-id="ca697-141">hello 指令碼會列印出 hello 的 hello VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca697-141">hello script prints out hello IP address of hello VM.</span></span>

* <span data-ttu-id="ca697-142">在 hello Azure 入口網站，找出您的部署的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca697-142">In hello Azure portal, locate hello resource group of your deployment.</span></span> <span data-ttu-id="ca697-143">除了本機部署，您指定做為方案的 hello 名稱或部署名稱已 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca697-143">Except for a local deployment, hello resource group has hello name you specified as solution or deployment name.</span></span> <span data-ttu-id="ca697-144">Hello hello 資源群組名稱是使用 hello 組建指令碼的本機部署， `<your username>ConnFactoryLocal`。</span><span class="sxs-lookup"><span data-stu-id="ca697-144">For a local deployment using hello build script, hello name of hello resource group is `<your username>ConnFactoryLocal`.</span></span> <span data-ttu-id="ca697-145">立即移除 hello**公用 IP 位址**hello 資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="ca697-145">Now remove hello **Public IP address** resource from hello resource group.</span></span>

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a><span data-ttu-id="ca697-146">我要如何登入 toohello 模擬 VM？</span><span class="sxs-lookup"><span data-stu-id="ca697-146">How do I sign in toohello simulation VM?</span></span>

<span data-ttu-id="ca697-147">如果您已部署您的方案使用 hello PowerShell 指令碼登入 toohello 模擬 VM 則僅支援`build.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。</span><span class="sxs-lookup"><span data-stu-id="ca697-147">Signing in toohello simulation VM is only supported if you have deployed your solution using hello PowerShell script `build.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory).</span></span>

<span data-ttu-id="ca697-148">如果您部署從 www.azureiotsuite.com hello 方案，您無法登入 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="ca697-148">If you deployed hello solution from www.azureiotsuite.com, you cannot sign in toohello VM.</span></span> <span data-ttu-id="ca697-149">您無法登入，因為 hello 密碼會隨機產生且無法重設。</span><span class="sxs-lookup"><span data-stu-id="ca697-149">You cannot sign in, because hello password is generated randomly and you cannot reset it.</span></span>

1. <span data-ttu-id="ca697-150">新增公用 IP 位址 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="ca697-150">Add a public IP address toohello VM.</span></span> <span data-ttu-id="ca697-151">請參閱[如何新增公用 IP 位址 toohello 模擬 VM？](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)</span><span class="sxs-lookup"><span data-stu-id="ca697-151">See [How do I add a public IP address toohello simulation VM?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)</span></span>
1. <span data-ttu-id="ca697-152">建立 VM 的 SSH 工作階段 tooyour 使用 hello 的 hello VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca697-152">Create an SSH session tooyour VM using hello IP address of hello VM.</span></span>
1. <span data-ttu-id="ca697-153">hello username toouse 是： `docker`。</span><span class="sxs-lookup"><span data-stu-id="ca697-153">hello username toouse is: `docker`.</span></span>
1. <span data-ttu-id="ca697-154">hello 密碼 toouse 取決於您使用 toodeploy 的 hello 版本：</span><span class="sxs-lookup"><span data-stu-id="ca697-154">hello password toouse depends on hello version you used toodeploy:</span></span>
    * <span data-ttu-id="ca697-155">對於 1 年 6 月 2017年之前使用 hello build.ps1 指令碼部署的解決方案，是 hello 密碼： `Passw0rd`。</span><span class="sxs-lookup"><span data-stu-id="ca697-155">For solutions deployed using hello build.ps1 script before 1 June 2017, hello password is: `Passw0rd`.</span></span>
    * <span data-ttu-id="ca697-156">對於 1 年 6 月 2017年之後使用 hello build.ps1 指令碼部署的方案，您可以在 hello 找到 hello 密碼`<name of your deployment>.config.user`檔案。</span><span class="sxs-lookup"><span data-stu-id="ca697-156">For solutions deployed using hello build.ps1 script after 1 June 2017, you can find hello password in hello `<name of your deployment>.config.user` file.</span></span> <span data-ttu-id="ca697-157">hello 密碼儲存在 hello **VmAdminPassword**設定。</span><span class="sxs-lookup"><span data-stu-id="ca697-157">hello password is stored in hello **VmAdminPassword** setting.</span></span> <span data-ttu-id="ca697-158">hello 密碼隨機產生的部署時除非您指定使用 hello`build.ps1`指令碼參數`-VmAdminPassword`</span><span class="sxs-lookup"><span data-stu-id="ca697-158">hello password is generated randomly at deployment time unless you specify it using hello `build.ps1` script parameter `-VmAdminPassword`</span></span>

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a><span data-ttu-id="ca697-159">如何停止和啟動所有的 docker 處理程序在 hello 模擬 VM？</span><span class="sxs-lookup"><span data-stu-id="ca697-159">How do I stop and start all docker processes in hello simulation VM?</span></span>

1. <span data-ttu-id="ca697-160">登入 toohello 模擬 VM。</span><span class="sxs-lookup"><span data-stu-id="ca697-160">Sign in toohello simulation VM.</span></span> <span data-ttu-id="ca697-161">請參閱[我要如何登入 toohello 模擬 VM？](#how-do-i-sign-in-to-the-simulation-vm)</span><span class="sxs-lookup"><span data-stu-id="ca697-161">See [How do I sign in toohello simulation VM?](#how-do-i-sign-in-to-the-simulation-vm)</span></span>
1. <span data-ttu-id="ca697-162">toocheck 哪些容器是作用中，執行： `docker ps`。</span><span class="sxs-lookup"><span data-stu-id="ca697-162">toocheck which containers are active, run: `docker ps`.</span></span>
1. <span data-ttu-id="ca697-163">toostop 所有模擬容器中，都執行： `./stopsimulation`。</span><span class="sxs-lookup"><span data-stu-id="ca697-163">toostop all simulation containers, run: `./stopsimulation`.</span></span>
1. <span data-ttu-id="ca697-164">toostart 模擬的所有容器：</span><span class="sxs-lookup"><span data-stu-id="ca697-164">toostart all simulation containers:</span></span>
    * <span data-ttu-id="ca697-165">匯出介面變數與 hello 名稱**IOTHUB_CONNECTIONSTRING**。</span><span class="sxs-lookup"><span data-stu-id="ca697-165">Export a shell variable with hello name **IOTHUB_CONNECTIONSTRING**.</span></span> <span data-ttu-id="ca697-166">使用 hello hello 值**IotHubOwnerConnectionString** hello 中設定`<name of your deployment>.config.user`檔案。</span><span class="sxs-lookup"><span data-stu-id="ca697-166">Use hello value of hello **IotHubOwnerConnectionString** setting in hello `<name of your deployment>.config.user` file.</span></span> <span data-ttu-id="ca697-167">例如：</span><span class="sxs-lookup"><span data-stu-id="ca697-167">For example:</span></span>

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * <span data-ttu-id="ca697-168">執行 `./startsimulation`。</span><span class="sxs-lookup"><span data-stu-id="ca697-168">Run `./startsimulation`.</span></span>

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a><span data-ttu-id="ca697-169">如何更新 hello VM 中的 hello 模擬？</span><span class="sxs-lookup"><span data-stu-id="ca697-169">How do I update hello simulation in hello VM?</span></span>

<span data-ttu-id="ca697-170">如果您變更了任何 toohello 模擬，您可以使用 hello PowerShell 指令碼`build.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)使用 hello`updatedimulation`命令。</span><span class="sxs-lookup"><span data-stu-id="ca697-170">If you have made any changes toohello simulation, you can use hello PowerShell script `build.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory) using hello `updatedimulation` command.</span></span> <span data-ttu-id="ca697-171">此指令碼組建所有的 hello 模擬元件、 停止 hello VM 中的 hello 模擬、 上傳、 安裝，並啟動它們。</span><span class="sxs-lookup"><span data-stu-id="ca697-171">This script builds all hello simulation components, stops hello simulation in hello VM, uploads, installs, and starts them.</span></span>

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a><span data-ttu-id="ca697-172">我要如何找出 hello 的 hello IoT 中樞我的方案所使用的連接字串？</span><span class="sxs-lookup"><span data-stu-id="ca697-172">How do I find out hello connection string of hello IoT hub used by my solution?</span></span>

<span data-ttu-id="ca697-173">如果您部署您的方案以 hello `build.ps1` hello 中的指令碼[儲存機制](https://github.com/Azure/azure-iot-connected-factory)，hello 連接字串是 hello 值**IotHubOwnerConnectionString**在 hello`<name of your deployment>.config.user`檔案。</span><span class="sxs-lookup"><span data-stu-id="ca697-173">If you deployed your solution with hello `build.ps1` script in hello [repository](https://github.com/Azure/azure-iot-connected-factory), hello connection string is hello value of **IotHubOwnerConnectionString** in hello `<name of your deployment>.config.user` file.</span></span>

<span data-ttu-id="ca697-174">您也可以尋找 hello 使用 hello Azure 入口網站的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ca697-174">You can also find hello connection string using hello Azure portal.</span></span> <span data-ttu-id="ca697-175">在 hello IoT 中樞資源部署的 hello 資源群組中，找出 hello 連接字串設定。</span><span class="sxs-lookup"><span data-stu-id="ca697-175">In hello IoT Hub resource in hello resource group of your deployment, locate hello connection string settings.</span></span>

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a><span data-ttu-id="ca697-176">IoT 中樞裝置沒有 hello 連接的原廠模擬使用？</span><span class="sxs-lookup"><span data-stu-id="ca697-176">Which IoT Hub devices does hello Connected factory simulation use?</span></span>

<span data-ttu-id="ca697-177">hello 的模擬自我註冊下列裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="ca697-177">hello simulation self registers hello following devices:</span></span>

* <span data-ttu-id="ca697-178">proxy.beijing.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-178">proxy.beijing.corp.contoso</span></span>
* <span data-ttu-id="ca697-179">proxy.capetown.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-179">proxy.capetown.corp.contoso</span></span>
* <span data-ttu-id="ca697-180">proxy.mumbai.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-180">proxy.mumbai.corp.contoso</span></span>
* <span data-ttu-id="ca697-181">proxy.munich0.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-181">proxy.munich0.corp.contoso</span></span>
* <span data-ttu-id="ca697-182">proxy.rio.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-182">proxy.rio.corp.contoso</span></span>
* <span data-ttu-id="ca697-183">proxy.seattle.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-183">proxy.seattle.corp.contoso</span></span>
* <span data-ttu-id="ca697-184">publisher.beijing.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-184">publisher.beijing.corp.contoso</span></span>
* <span data-ttu-id="ca697-185">publisher.capetown.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-185">publisher.capetown.corp.contoso</span></span>
* <span data-ttu-id="ca697-186">publisher.mumbai.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-186">publisher.mumbai.corp.contoso</span></span>
* <span data-ttu-id="ca697-187">publisher.munich0.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-187">publisher.munich0.corp.contoso</span></span>
* <span data-ttu-id="ca697-188">publisher.rio.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-188">publisher.rio.corp.contoso</span></span>
* <span data-ttu-id="ca697-189">publisher.seattle.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-189">publisher.seattle.corp.contoso</span></span>

<span data-ttu-id="ca697-190">使用 hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)或[iot 中樞總管](https://github.com/azure/iothub-explorer)工具，您可以檢查哪些裝置會向您的方案正在使用的 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ca697-190">Using hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) or [iothub-explorer](https://github.com/azure/iothub-explorer) tool, you can check which devices are registered with hello IoT hub your solution is using.</span></span> <span data-ttu-id="ca697-191">toouse 這些工具，您需要 hello 連接字串 hello IoT 中樞部署中。</span><span class="sxs-lookup"><span data-stu-id="ca697-191">toouse these tools, you need hello connection string for hello IoT hub in your deployment.</span></span>

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a><span data-ttu-id="ca697-192">如何取得記錄資料從 hello 模擬元件？</span><span class="sxs-lookup"><span data-stu-id="ca697-192">How can I get log data from hello simulation components?</span></span>

<span data-ttu-id="ca697-193">Toolog 檔案中的 hello 模擬記錄資訊中的所有元件。</span><span class="sxs-lookup"><span data-stu-id="ca697-193">All components in hello simulation log information in toolog files.</span></span> <span data-ttu-id="ca697-194">這些檔案可以在 hello VM hello 資料夾中找到`home/docker/Logs`。</span><span class="sxs-lookup"><span data-stu-id="ca697-194">These files can be found in hello VM in hello folder `home/docker/Logs`.</span></span> <span data-ttu-id="ca697-195">tooretrieve hello 記錄檔，您可以使用 hello PowerShell 指令碼`Simulation/Factory/Get-SimulationLogs.ps1`在 hello[儲存機制](https://github.com/Azure/azure-iot-connected-factory)。</span><span class="sxs-lookup"><span data-stu-id="ca697-195">tooretrieve hello logs, you can use hello PowerShell script `Simulation/Factory/Get-SimulationLogs.ps1` in hello [repository](https://github.com/Azure/azure-iot-connected-factory).</span></span>

<span data-ttu-id="ca697-196">這個指令碼需要 toosign toohello VM 中。</span><span class="sxs-lookup"><span data-stu-id="ca697-196">This script needs toosign in toohello VM.</span></span> <span data-ttu-id="ca697-197">您可能需要 tooprovide 認證 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="ca697-197">You may need tooprovide credentials for hello sign-in.</span></span> <span data-ttu-id="ca697-198">請參閱[我要如何登入 toohello 模擬 VM？](#how-do-i-sign-in-to-the-simulation-vm) toofind hello 認證。</span><span class="sxs-lookup"><span data-stu-id="ca697-198">See [How do I sign in toohello simulation VM?](#how-do-i-sign-in-to-the-simulation-vm) toofind hello credentials.</span></span>

<span data-ttu-id="ca697-199">hello 指令碼加入/移除公用 IP 位址 toohello VM，如果還沒有其中一個，並將它移除。</span><span class="sxs-lookup"><span data-stu-id="ca697-199">hello script adds/removes a public IP address toohello VM, if it does not yet have one and removes it.</span></span> <span data-ttu-id="ca697-200">hello 指令碼置於封存檔中的所有記錄檔，並下載 hello 封存 tooyour 開發工作站。</span><span class="sxs-lookup"><span data-stu-id="ca697-200">hello script puts all log files in an archive and downloads hello archive tooyour development workstation.</span></span>

<span data-ttu-id="ca697-201">或者登入 toohello 透過 SSH 的 VM，並檢查 hello 記錄檔，在執行階段。</span><span class="sxs-lookup"><span data-stu-id="ca697-201">Alternatively log in toohello VM via SSH and inspect hello log files at runtime.</span></span>

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a><span data-ttu-id="ca697-202">如何檢查資料 toohello 雲端時，是否要傳送嗨模擬？</span><span class="sxs-lookup"><span data-stu-id="ca697-202">How can I check if hello simulation is sending data toohello cloud?</span></span>

<span data-ttu-id="ca697-203">以 hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)或 hello [iot 中樞總管](https://github.com/azure/iothub-explorer)工具，您可以檢查 hello 資料從特定裝置傳送 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ca697-203">With hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/azure/iothub-explorer) tool, you can inspect hello data sent tooIoT Hub from certain devices.</span></span> <span data-ttu-id="ca697-204">toouse 這些工具，您需要 tooknow hello 連接字串 hello IoT 中樞部署中。</span><span class="sxs-lookup"><span data-stu-id="ca697-204">toouse these tools, you need tooknow hello connection string for hello IoT hub in your deployment.</span></span> <span data-ttu-id="ca697-205">請參閱[如何找出 hello 的 hello IoT 中樞我的方案所使用的連接字串？](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)</span><span class="sxs-lookup"><span data-stu-id="ca697-205">See [How do I find out hello connection string of hello IoT hub used by my solution?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)</span></span>

<span data-ttu-id="ca697-206">檢查傳送一個 hello 發行者裝置 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="ca697-206">Inspect hello data sent by one of hello publisher devices:</span></span>

* <span data-ttu-id="ca697-207">publisher.beijing.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-207">publisher.beijing.corp.contoso</span></span>
* <span data-ttu-id="ca697-208">publisher.capetown.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-208">publisher.capetown.corp.contoso</span></span>
* <span data-ttu-id="ca697-209">publisher.mumbai.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-209">publisher.mumbai.corp.contoso</span></span>
* <span data-ttu-id="ca697-210">publisher.munich0.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-210">publisher.munich0.corp.contoso</span></span>
* <span data-ttu-id="ca697-211">publisher.rio.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-211">publisher.rio.corp.contoso</span></span>
* <span data-ttu-id="ca697-212">publisher.seattle.corp.contoso</span><span class="sxs-lookup"><span data-stu-id="ca697-212">publisher.seattle.corp.contoso</span></span>

<span data-ttu-id="ca697-213">如果您不看到任何資料傳送 tooIoT 中樞時，就 hello 模擬的問題。</span><span class="sxs-lookup"><span data-stu-id="ca697-213">If you see no data sent tooIoT Hub, then there is an issue with hello simulation.</span></span> <span data-ttu-id="ca697-214">第一個步驟是分析中，您應該分析 hello hello 模擬元件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ca697-214">As a first analysis step you should analyze hello log files of hello simulation components.</span></span> <span data-ttu-id="ca697-215">請參閱[如何取得記錄資料從 hello 模擬元件？](#how-can-i-get-log-data-from-the-simulation-components)</span><span class="sxs-lookup"><span data-stu-id="ca697-215">See [How can I get log data from hello simulation components?](#how-can-i-get-log-data-from-the-simulation-components)</span></span> <span data-ttu-id="ca697-216">接下來，再試一次 toostop 和啟動 hello 模擬並如果仍然不沒有傳送任何資料，更新 hello 模擬完全。</span><span class="sxs-lookup"><span data-stu-id="ca697-216">Next, try toostop and start hello simulation and if there's still no data sent, update hello simulation completely.</span></span> <span data-ttu-id="ca697-217">請參閱[如何更新 hello VM 中的 hello 模擬？](#how-do-i-update-the-simulation-in-the-vm)</span><span class="sxs-lookup"><span data-stu-id="ca697-217">See [How do I update hello simulation in hello VM?](#how-do-i-update-the-simulation-in-the-vm)</span></span>

### <a name="next-steps"></a><span data-ttu-id="ca697-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca697-218">Next steps</span></span>

<span data-ttu-id="ca697-219">您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="ca697-219">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* [<span data-ttu-id="ca697-220">預測性維護預先設定的解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="ca697-220">Predictive maintenance preconfigured solution overview</span></span>](iot-suite-predictive-overview.md)
* [<span data-ttu-id="ca697-221">連線處理站預先設定的解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="ca697-221">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* [<span data-ttu-id="ca697-222">從 hello 接地 IoT 安全性</span><span class="sxs-lookup"><span data-stu-id="ca697-222">IoT security from hello ground up</span></span>](securing-iot-ground-up.md)
