---
title: "在 Azure microservices aaaChange FabricTransport 設定 |Microsoft 文件"
description: "深入了解設定 Azure Service Fabric 動作項目通訊設定。"
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="9a07e-103">設定 Reliable Actors 的 FabricTransport 設定</span><span class="sxs-lookup"><span data-stu-id="9a07e-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="9a07e-104">以下是您可以設定的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="9a07e-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="9a07e-105">C#：[FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="9a07e-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="9a07e-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="9a07e-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="9a07e-107">您可以使用以下方式修改 FabricTransport hello 預設組態。</span><span class="sxs-lookup"><span data-stu-id="9a07e-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="9a07e-108">組件屬性</span><span class="sxs-lookup"><span data-stu-id="9a07e-108">Assembly attribute</span></span>

<span data-ttu-id="9a07e-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute)屬性需要 toobe hello 行動用戶端與行動服務組件上套用。</span><span class="sxs-lookup"><span data-stu-id="9a07e-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="9a07e-110">hello 下列範例顯示如何 toochange hello FabricTransport OperationTimeout 設定的預設值：</span><span class="sxs-lookup"><span data-stu-id="9a07e-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="9a07e-111">第二個範例會變更 FabricTransport MaxMessageSize 和 OperationTimeoutInSeconds 的預設值。</span><span class="sxs-lookup"><span data-stu-id="9a07e-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="9a07e-112">組態封裝</span><span class="sxs-lookup"><span data-stu-id="9a07e-112">Config package</span></span>

<span data-ttu-id="9a07e-113">您可以使用[組態封裝](service-fabric-application-model.md)toomodify hello 預設組態。</span><span class="sxs-lookup"><span data-stu-id="9a07e-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="9a07e-114">設定 FabricTransport hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="9a07e-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="9a07e-115">新增 TransportSettings 區段 hello settings.xml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="9a07e-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="9a07e-116">根據預設，動作項目程式碼會尋找 SectionName 做為「&lt;ActorName&gt;TransportSettings」。</span><span class="sxs-lookup"><span data-stu-id="9a07e-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="9a07e-117">如果找不到，它會以「TransportSettings」檢查 SectionName 。</span><span class="sxs-lookup"><span data-stu-id="9a07e-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="9a07e-118">設定 FabricTransport hello 行動用戶端組件</span><span class="sxs-lookup"><span data-stu-id="9a07e-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="9a07e-119">如果 hello 用戶端不以服務的一部分執行，您可以建立 「&lt;用戶端 Exe 名稱&gt;。 settings.xml"相同檔案中 hello 與 hello 用戶端.exe 檔的位置。</span><span class="sxs-lookup"><span data-stu-id="9a07e-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="9a07e-120">然後在該檔案中新增 TransportSettings 區段。</span><span class="sxs-lookup"><span data-stu-id="9a07e-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="9a07e-121">SectionName 應為「TransportSettings」。</span><span class="sxs-lookup"><span data-stu-id="9a07e-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="9a07e-122">使用第二個憑證來設定安全動作服務/用戶端的 FabricTransport 設定。</span><span class="sxs-lookup"><span data-stu-id="9a07e-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="9a07e-123">您可以新增參數 CertificateFindValuebySecondary，將次要憑證資訊加以新增。</span><span class="sxs-lookup"><span data-stu-id="9a07e-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="9a07e-124">以下是 hello 接聽程式 TransportSettings hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9a07e-124">Below is hello example for hello Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="9a07e-125">以下是用戶端 TransportSettings hello hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9a07e-125">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="9a07e-126">使用主體名稱來設定安全動作服務/用戶端的 FabricTransport 設定。</span><span class="sxs-lookup"><span data-stu-id="9a07e-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="9a07e-127">使用者需求 tooprovide findType FindBySubjectName，以加入 CertificateIssuerThumbprints 和 CertificateRemoteCommonNames 值。</span><span class="sxs-lookup"><span data-stu-id="9a07e-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="9a07e-128">以下是 hello 接聽程式 TransportSettings hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9a07e-128">Below is hello example for hello Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="9a07e-129">以下是用戶端 TransportSettings hello hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9a07e-129">Below is hello example for hello Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
