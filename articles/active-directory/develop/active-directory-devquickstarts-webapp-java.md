---
title: "Azure AD Java Web 應用程式入門 | Microsoft Docs"
description: "建置可使用工作或學校帳戶登入使用者的 Java Web 應用程式。"
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 2b92b605-9cd5-4b99-bcbb-66c026558119
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 02/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 5358404881b65d217ab36a41ca04a73f2c462c86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="java-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="b2169-103">搭配 Azure AD 的 Java Web 應用程式登入和登出</span><span class="sxs-lookup"><span data-stu-id="b2169-103">Java web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b2169-104">Azure Active Directory (Azure AD) 只需幾行的程式碼便可提供單一登入和登出，讓您外包 Web 應用程式的身分識別管理變得簡單。</span><span class="sxs-lookup"><span data-stu-id="b2169-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="b2169-105">您可以藉由使用社群導向 Azure Active Directory Authentication Library for Java (ADAL4J) 的 Microsoft 實作，將使用者登入和登出 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2169-105">You can sign users in and out of Java web apps by using the Microsoft implementation of the community-driven Azure Active Directory Authentication Library for Java (ADAL4J).</span></span>

<span data-ttu-id="b2169-106">本文章說明如何使用 ADAL4J 以執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="b2169-106">This article shows how to use the ADAL4J to:</span></span>

* <span data-ttu-id="b2169-107">使用 Azure AD 做為身分識別提供者，將使用者登入 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2169-107">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="b2169-108">顯示部分使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="b2169-108">Display some user information.</span></span>
* <span data-ttu-id="b2169-109">將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2169-109">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="b2169-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="b2169-110">Before you get started</span></span>

* <span data-ttu-id="b2169-111">下載[應用程式基本架構](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)或下載[完整的範例](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="b2169-111">Download the [app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip), or download the [completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>
* <span data-ttu-id="b2169-112">您還需要一個可以註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b2169-112">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="b2169-113">如果您還沒有租用戶，請[了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="b2169-113">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="b2169-114">當您準備就緒，請遵循接下來九個章節的程序。</span><span class="sxs-lookup"><span data-stu-id="b2169-114">When you are ready, follow the procedures in the next nine sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="b2169-115">步驟 1︰使用 Azure AD 註冊新的應用程式</span><span class="sxs-lookup"><span data-stu-id="b2169-115">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="b2169-116">若要設定應用程式以驗證使用者，請先藉由執行下列操作，在您的租用戶中註冊該應用程式︰</span><span class="sxs-lookup"><span data-stu-id="b2169-116">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="b2169-117">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b2169-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2169-118">在頂端列中，按一下您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b2169-118">On the top bar, click your account name.</span></span> <span data-ttu-id="b2169-119">在 [目錄] 清單下，選取您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b2169-119">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="b2169-120">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="b2169-120">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b2169-121">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b2169-121">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b2169-122">遵照提示建立 **Web 應用程式和/或 Web API**。</span><span class="sxs-lookup"><span data-stu-id="b2169-122">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="b2169-123">[名稱] 向使用者說明該應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2169-123">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="b2169-124">[登入 URL] 是應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="b2169-124">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="b2169-125">基本架構的預設 URL 是 http://localhost:8080/adal4jsample/。</span><span class="sxs-lookup"><span data-stu-id="b2169-125">The skeleton's default URL is http://localhost:8080/adal4jsample/.</span></span>
6. <span data-ttu-id="b2169-126">完成註冊之後，Azure AD 會為應用程式指派一個唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="b2169-126">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="b2169-127">請從應用程式頁面複製該值，以在接下來的小節中使用。</span><span class="sxs-lookup"><span data-stu-id="b2169-127">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="b2169-128">從應用程式的 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="b2169-128">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="b2169-129">[應用程式識別碼 URI] 是應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b2169-129">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="b2169-130">命名慣例是 `https://<tenant-domain>/<app-name>` (例如 `http://localhost:8080/adal4jsample/`)。</span><span class="sxs-lookup"><span data-stu-id="b2169-130">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `http://localhost:8080/adal4jsample/`).</span></span>

<span data-ttu-id="b2169-131">當您在應用程式的入口網站中時，在 [設定] 頁面上建立和複製應用程式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b2169-131">When you are in the portal for the app, create and copy a key for the app on the **Settings** page.</span></span> <span data-ttu-id="b2169-132">稍後您將需要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b2169-132">You'll need the key shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-adal4j-and-prerequisites-by-using-maven"></a><span data-ttu-id="b2169-133">步驟 2︰藉由使用 Maven，設定應用程式以使用 ADAL4J 和必要條件</span><span class="sxs-lookup"><span data-stu-id="b2169-133">Step 2: Set up the app to use the ADAL4J and prerequisites by using Maven</span></span>
<span data-ttu-id="b2169-134">在這個步驟中，您會設定 ADAL4J 以使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b2169-134">In this step, you configure the ADAL4J to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="b2169-135">您會使用 ADAL4J 來發出登入和登出要求、管理使用者工作階段、取得使用者資訊等等。</span><span class="sxs-lookup"><span data-stu-id="b2169-135">You use the ADAL4J to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

<span data-ttu-id="b2169-136">在您的專案根目錄中，開啟/建立 `pom.xml`、找到 `// TODO: provide dependencies for Maven`，然後以下列項目取代：</span><span class="sxs-lookup"><span data-stu-id="b2169-136">In the root directory of your project, open/create `pom.xml`, locate `// TODO: provide dependencies for Maven`, and replace it with the following:</span></span>

```Java

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4jsample</artifactId>
    <packaging>war</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>adal4jsample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.1</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
        <!-- Spring 3 dependencies -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>sample-for-adal4j</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <warName>${project.artifactId}</warName>
                    <source>${project.basedir}\src</source>
                    <target>${maven.compiler.target}</target>
                    <encoding>utf-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>

    </project>
```

## <a name="step-3-create-the-java-web-app-files-web-inf"></a><span data-ttu-id="b2169-137">步驟 3：建立 Java Web 應用程式檔案 (WEB-INF)</span><span class="sxs-lookup"><span data-stu-id="b2169-137">Step 3: Create the Java web app files (WEB-INF)</span></span>
<span data-ttu-id="b2169-138">在這個步驟中，您會設定 Java Web 應用程式使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b2169-138">In this step, you configure the Java web app to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="b2169-139">使用 ADAL4J 來發出登入和登出要求、管理使用者的工作階段、取得使用者相關資訊等等。</span><span class="sxs-lookup"><span data-stu-id="b2169-139">Use the ADAL4J to issue sign-in and sign-out requests, manage the user's session, get information about the user, and so forth.</span></span>

1. <span data-ttu-id="b2169-140">開啟位於 \webapp\WEB-INF\, 底下的 web.xml 檔案，然後在 XML 中輸入應用程式組態值。</span><span class="sxs-lookup"><span data-stu-id="b2169-140">Open the web.xml file located under \webapp\WEB-INF\, and enter the app configuration values in the XML.</span></span> <span data-ttu-id="b2169-141">XML 檔案現在應該包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-141">The XML file should contain the following code:</span></span>

    ```xml

    <?xml version="1.0"?>
    <web-app id="WebApp_ID" version="2.4"
        xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee
        http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">
        <display-name>Archetype Created Web Application</display-name>
        <context-param>
            <param-name>authority</param-name>
            <param-value>https://login.microsoftonline.com/</param-value>
        </context-param>
        <context-param>
            <param-name>tenant</param-name>
            <param-value>YOUR_TENANT_NAME</param-value>
        </context-param>
        <filter>
            <filter-name>BasicFilter</filter-name>
            <filter-class>com.microsoft.aad.adal4jsample.BasicFilter</filter-class>
            <init-param>
                <param-name>client_id</param-name>
                <param-value>YOUR_CLIENT_ID</param-value>
            </init-param>
            <init-param>
                <param-name>secret_key</param-name>
                <param-value>YOUR_CLIENT_SECRET</param-value>
            </init-param>
        </filter>
        <filter-mapping>
            <filter-name>BasicFilter</filter-name>
            <url-pattern>/secure/*</url-pattern>
        </filter-mapping>
        <servlet>
            <servlet-name>mvc-dispatcher</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
            <load-on-startup>1</load-on-startup>
        </servlet>
        <servlet-mapping>
            <servlet-name>mvc-dispatcher</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/mvc-dispatcher-servlet.xml</param-value>
        </context-param>
        <listener>
            <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
        </listener>
    </web-app>
    ```

 * <span data-ttu-id="b2169-142">YOUR_CLIENT_ID 是在註冊入口網站中指派給應用程式的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="b2169-142">YOUR_CLIENT_ID is the **Application Id** assigned to your app in the registration portal.</span></span>
 * <span data-ttu-id="b2169-143">YOUR_CLIENT_SECRET 是您在入口網站中建立的**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="b2169-143">YOUR_CLIENT_SECRET is the **Application Secret** that you created in the portal.</span></span>
 * <span data-ttu-id="b2169-144">YOUR_TENANT_NAME 是您應用程式的**租用戶名稱**(例如，contoso.onmicrosoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b2169-144">YOUR_TENANT_NAME is the **tenant name** of your app (for example, contoso.onmicrosoft.com).</span></span>

 <span data-ttu-id="b2169-145">如同您在 XML 檔案中所見，您撰寫稱為 mvc-dispatcher 的 JavaServer 頁面 (JSP) 或 Java Servlet Web 應用程式，每當您造訪 /secure URL 時，會使用 BasicFilter。</span><span class="sxs-lookup"><span data-stu-id="b2169-145">As you can see in the XML file, you are writing a JavaServer Pages (JSP) or Java Servlet web app called mvc-dispatcher that uses BasicFilter whenever you visit the /secure URL.</span></span> <span data-ttu-id="b2169-146">在相同的程式碼中，您使用 /secure 做為受保護內容的位置，並且強制對 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b2169-146">In the same code, you use /secure as a place for the protected content and to force authentication to Azure AD.</span></span>

2. <span data-ttu-id="b2169-147">在 \webapp\WEB-INF\, 底下建立 mvc-dispatcher-servlet.xml 檔案，然後輸入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-147">Create the mvc-dispatcher-servlet.xml file located under \webapp\WEB-INF\, and enter the following code:</span></span>

    ```xml

    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:context="http://www.springframework.org/schema/context"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="
            http://www.springframework.org/schema/beans     
            http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd">
        <context:component-scan base-package="com.microsoft.aad.adal4jsample" />
        <bean
            class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix">
                <value>/</value>
            </property>
            <property name="suffix">
                <value>.jsp</value>
            </property>
        </bean>
    </beans>
    ```

 <span data-ttu-id="b2169-148">此程式碼會告訴 Web 應用程式使用 Spring，並指出哪裡可以找到您在下一節中撰寫的 JSP 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-148">This code tells the web app to use Spring, and it indicates where to find the JSP file, which you write in the next section.</span></span>

## <a name="step-4-create-the-jsp-view-files-for-basicfilter-mvc"></a><span data-ttu-id="b2169-149">步驟 4：建立 JSP 檢視檔案 (適用於 BasicFilter MVC)</span><span class="sxs-lookup"><span data-stu-id="b2169-149">Step 4: Create the JSP View files (for BasicFilter MVC)</span></span>
<span data-ttu-id="b2169-150">您已經到達在 WEB-INF 中設定 Web 應用程式的一半。</span><span class="sxs-lookup"><span data-stu-id="b2169-150">You are half-way through setting up your web app in WEB-INF.</span></span> <span data-ttu-id="b2169-151">接下來，您建立 BasicFilter 模型檢視控制器 (MVC) 的 JSP 檔案，該檔案由 Web 應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="b2169-151">Next, you create the JSP files for BasicFilter model view controller (MVC), which the web app executes.</span></span> <span data-ttu-id="b2169-152">我們在組態期間已經提示建立檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-152">We hinted at creating the files during the configuration.</span></span>

<span data-ttu-id="b2169-153">您稍早告訴 XML 組態檔中的 Java，您有`/`資源載入 JSP 檔案，且您有資源`/secure`通過篩選器，您將其稱為 BasicFilter。</span><span class="sxs-lookup"><span data-stu-id="b2169-153">Earlier, you told Java in the XML configuration files that you have a `/` resource that loads JSP files, and you have a `/secure` resource that passes through a filter, which you called BasicFilter.</span></span>

<span data-ttu-id="b2169-154">若要建立 JSP 檔案，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="b2169-154">To create the JSP files, do the following:</span></span>

1. <span data-ttu-id="b2169-155">建立 index.jsp 檔案 (位於 \webapp\) 底下，然後貼上下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="b2169-155">Create the index.jsp file (located under \webapp\), and then paste the following code:</span></span>

    ```jsp
    <html>
    <body>
        <h2>Hello World!</h2>
        <ul>
        <li><a href="secure/aad">Secure Page</a></li>
        </ul>
    </body>
    </html>
    ```

 <span data-ttu-id="b2169-156">此程式碼只會重新導向至篩選器保護的安全頁面。</span><span class="sxs-lookup"><span data-stu-id="b2169-156">This code simply redirects to a secure page that is protected by the filter.</span></span>

2. <span data-ttu-id="b2169-157">在相同的目錄中建立 error.jsp 檔案，以攔截可能會發生的任何錯誤：</span><span class="sxs-lookup"><span data-stu-id="b2169-157">In the same directory, create an error.jsp file to catch any errors that might happen:</span></span>

    ```jsp

    <html>
    <body>
        <h2>ERROR PAGE!</h2>
        <p>
            Exception -
            <%=request.getAttribute("error")%></p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
    </body>
    </html>
    ```
3. <span data-ttu-id="b2169-158">若要製作安全的網頁，請在 \webapp 底下建立名為 \secure 的資料夾，因此目錄現在是 \webapp\secure。</span><span class="sxs-lookup"><span data-stu-id="b2169-158">To make that secure webpage, create a folder under \webapp called \secure so that the directory is now \webapp\secure.</span></span>
4. <span data-ttu-id="b2169-159">在 \webapp\secure 目錄中，建立 aad.jsp 檔案，然後貼上下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="b2169-159">In the \webapp\secure directory, create an aad.jsp file, and then paste the following code:</span></span>

    ```jsp

    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
        <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>AAD Secure Page</title>
        </head>
        <body>

        <h1>Directory - Users List</h1>
        <p>${users}</p>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?cc=1">Get new Access Token via Client Credentials</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/secure/aad?refresh=1">Get new Access Token via Refresh Token</a></li>
        </ul>
        <ul>
            <li><a href="<%=request.getContextPath()%>/index.jsp">Go Home</a></li>
        </ul>
        </body>
    </html>
    ```

    <span data-ttu-id="b2169-160">此頁面會重新導向至特定要求，BasicFilter Servlet 會讀取該要求，然後使用 ADAJ4J 來執行。</span><span class="sxs-lookup"><span data-stu-id="b2169-160">This page redirects to specific requests, which the BasicFilter servlet reads and then executes on by using the ADAJ4J.</span></span>

<span data-ttu-id="b2169-161">您現在需要設定 Java 檔案，以便 Servlet 可以執行其工作。</span><span class="sxs-lookup"><span data-stu-id="b2169-161">You now need to set up the Java files so that the servlet can do its work.</span></span>

## <a name="step-5-create-some-java-helper-files-for-basicfilter-mvc"></a><span data-ttu-id="b2169-162">步驟 5：建立一些 Java 協助程式檔案 (適用於 BasicFilter MVC)</span><span class="sxs-lookup"><span data-stu-id="b2169-162">Step 5: Create some Java helper files (for BasicFilter MVC)</span></span>
<span data-ttu-id="b2169-163">我們在這個步驟的目標是要建立 Java 檔案，這些檔案能夠：</span><span class="sxs-lookup"><span data-stu-id="b2169-163">Our goal in this step is to create Java files that:</span></span>

* <span data-ttu-id="b2169-164">允許使用者登入和登出。</span><span class="sxs-lookup"><span data-stu-id="b2169-164">Allow for sign-in and sign-out of the user.</span></span>
* <span data-ttu-id="b2169-165">取得使用者的一些相關資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-165">Get some data about the user.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b2169-166">若要取得使用者的相關資料，從 Azure AD 使用圖形 API。</span><span class="sxs-lookup"><span data-stu-id="b2169-166">To get data about the user, use the Graph API from Azure AD.</span></span> <span data-ttu-id="b2169-167">圖形 API 是安全的 Web 服務，可讓您用來擷取有關組織 (包括個別使用者) 的資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-167">The Graph API is a secure webservice that you can use to grab data about your organization, including individual users.</span></span> <span data-ttu-id="b2169-168">這種方法優於在權杖中預先填入機密資料，因為它可確保︰</span><span class="sxs-lookup"><span data-stu-id="b2169-168">This approach is better than pre-filling sensitive data in tokens, because it ensures that:</span></span>
    > * <span data-ttu-id="b2169-169">要求資料的使用者已獲得授權。</span><span class="sxs-lookup"><span data-stu-id="b2169-169">The users who ask for the data are authorized.</span></span>
    > * <span data-ttu-id="b2169-170">碰巧取得權杖的任何人 (例如，從越獄的手機或桌上型電腦的網頁瀏覽器) 無法取得使用者或組織的相關重要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-170">Anyone who might happen to grab the token (from a jailbroken phone or web-browser cache on a desktop, for example) cannot obtain important details about the user or the organization.</span></span>

<span data-ttu-id="b2169-171">若要針對此工作撰寫一些 Java 檔案︰</span><span class="sxs-lookup"><span data-stu-id="b2169-171">To write some Java files for this work:</span></span>

1. <span data-ttu-id="b2169-172">在稱為 adal4jsample 的根目錄中建立資料夾來儲存所有 Java 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-172">Create a folder in your root directory called adal4jsample to store all the Java files.</span></span>

    <span data-ttu-id="b2169-173">在此範例中，您在 Java 檔案中使用命名空間 com.microsoft.aad.adal4jsample。</span><span class="sxs-lookup"><span data-stu-id="b2169-173">In this example, you are using the namespace com.microsoft.aad.adal4jsample in the Java files.</span></span> <span data-ttu-id="b2169-174">大部分 IDE 會針對此目的建立巢狀資料夾結構 (例如，/com/microsoft/aad/adal4jsample)。</span><span class="sxs-lookup"><span data-stu-id="b2169-174">Most IDEs create a nested folder structure for this purpose (for example, /com/microsoft/aad/adal4jsample).</span></span> <span data-ttu-id="b2169-175">您也可以這麼做，但並非必要。</span><span class="sxs-lookup"><span data-stu-id="b2169-175">You can do this also, but it is not necessary.</span></span>

2. <span data-ttu-id="b2169-176">在此資料夾中，建立名為 JSONHelper.java 的檔案，您將用來協助從您的權杖剖析 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-176">Inside this folder, create a file called JSONHelper.java, which you'll use to help parse the JSON data from your tokens.</span></span> <span data-ttu-id="b2169-177">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-177">To create the file, paste the following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.lang.reflect.Field;
    import java.util.Arrays;
    import java.util.Enumeration;
    import java.util.List;

    import javax.servlet.http.HttpServletRequest;

    import org.apache.commons.lang3.text.WordUtils;
    import org.apache.log4j.Logger;
    import org.json.JSONArray;
    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This class provides the methods to parse JSON data from a JSON-formatted
     * string.
     *
     * @author Azure Active Directory contributor
     *
     */
    public class JSONHelper {

        private static Logger logger = Logger.getLogger(JSONHelper.class);

        JSONHelper() {
            // PropertyConfigurator.configure("log4j.properties");
        }

        /**
         * This method parses a JSON array out of a collection of JSON objects
         * within a string.
         *
         * @param jSonData
         *            The JSON string that holds the collection
         * @return A JSON array that contains all the collection objects
         * @throws Exception
         */
        public static JSONArray fetchDirectoryObjectJSONArray(JSONObject jsonObject) throws Exception {
            JSONArray jsonArray = new JSONArray();
            jsonArray = jsonObject.optJSONObject("responseMsg").optJSONArray("value");
            return jsonArray;
        }

        /**
         * This method parses a JSON object out of a collection of JSON objects
         * within a string.
         *
         * @param jsonObject
         * @return A JSON object that contains the DirectoryObject
         * @throws Exception
         */
        public static JSONObject fetchDirectoryObjectJSONObject(JSONObject jsonObject) throws Exception {
            JSONObject jObj = new JSONObject();
            jObj = jsonObject.optJSONObject("responseMsg");
            return jObj;
        }

        /**
         * This method parses the skip token from a JSON-formatted string.
         *
         * @param jsonData
         *            The JSON-formatted string
         * @return The skipToken
         * @throws Exception
         */
        public static String fetchNextSkiptoken(JSONObject jsonObject) throws Exception {
            String skipToken = "";
            // Parse the skip token out of the string.
            skipToken = jsonObject.optJSONObject("responseMsg").optString("odata.nextLink");

            if (!skipToken.equalsIgnoreCase("")) {
                // Remove the unnecessary prefix from the skip token.
                int index = skipToken.indexOf("$skiptoken=") + (new String("$skiptoken=")).length();
                skipToken = skipToken.substring(index);
            }
            return skipToken;
        }

        /**
         * @param jsonObject
         * @return
         * @throws Exception
         */
        public static String fetchDeltaLink(JSONObject jsonObject) throws Exception {
            String deltaLink = "";
            // Parse the skip token out of the string.
            deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.deltaLink");
            if (deltaLink == null || deltaLink.length() == 0) {
                deltaLink = jsonObject.optJSONObject("responseMsg").optString("aad.nextLink");
                logger.info("deltaLink empty, nextLink ->" + deltaLink);

            }
            if (!deltaLink.equalsIgnoreCase("")) {
                // Remove the unnecessary prefix from the skip token.
                int index = deltaLink.indexOf("deltaLink=") + (new String("deltaLink=")).length();
                deltaLink = deltaLink.substring(index);
            }
            return deltaLink;
        }

        /**
         * This method creates a string consisting of a JSON document with all
         * the necessary elements set from the HttpServletRequest request.
         *
         * @param request
         *            The HttpServletRequest
         * @return The string containing the JSON document
         * @throws Exception
         *             If there is any error processing the request.
         */
        public static String createJSONString(HttpServletRequest request, String controller) throws Exception {
            JSONObject obj = new JSONObject();
            try {
                Field[] allFields = Class.forName(
                        "com.microsoft.windowsazure.activedirectory.sdk.graph.models." + controller).getDeclaredFields();
                String[] allFieldStr = new String[allFields.length];
                for (int i = 0; i < allFields.length; i++) {
                    allFieldStr[i] = allFields[i].getName();
                }
                List<String> allFieldStringList = Arrays.asList(allFieldStr);
                Enumeration<String> fields = request.getParameterNames();

                while (fields.hasMoreElements()) {

                    String fieldName = fields.nextElement();
                    String param = request.getParameter(fieldName);
                    if (allFieldStringList.contains(fieldName)) {
                        if (param == null || param.length() == 0) {
                            if (!fieldName.equalsIgnoreCase("password")) {
                                obj.put(fieldName, JSONObject.NULL);
                            }
                        } else {
                            if (fieldName.equalsIgnoreCase("password")) {
                                obj.put("passwordProfile", new JSONObject("{\"password\": \"" + param + "\"}"));
                            } else {
                                obj.put(fieldName, param);
                            }
                        }
                    }
                }
            } catch (JSONException e) {
                e.printStackTrace();
            } catch (SecurityException e) {
                e.printStackTrace();
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            }            
            return obj.toString();
        }

        /**
         *
         * @param key
         * @param value
         * @return string format of this JSON object
         * @throws Exception
         */
        public static String createJSONString(String key, String value) throws Exception {

            JSONObject obj = new JSONObject();
            try {
                obj.put(key, value);
            } catch (JSONException e) {
                e.printStackTrace();
            }

            return obj.toString();
        }

        /**
         * This is a generic method that copies the simple attribute values from an
         * argument jsonObject to an argument generic object.
         *
         * @param jsonObject
         *            The jsonObject from where the attributes are to be copied.
         * @param destObject
         *            The object where the attributes should be copied to.
         * @throws Exception
         *             Throws an Exception when the operation is unsuccessful.
         */
        public static <T> void convertJSONObjectToDirectoryObject(JSONObject jsonObject, T destObject) throws Exception {

            // Get the list of all the field names.
            Field[] fieldList = destObject.getClass().getDeclaredFields();

            // For all the declared field.
            for (int i = 0; i < fieldList.length; i++) {
                // If the field is of type String, that is
                // if it is a simple attribute.
                if (fieldList[i].getType().equals(String.class)) {
                    // Invoke the corresponding set method of the destObject using
                    // the argument taken from the jsonObject.
                    destObject
                            .getClass()
                            .getMethod(String.format("set%s", WordUtils.capitalize(fieldList[i].getName())),
                                    new Class[] { String.class })
                            .invoke(destObject, new Object[] { jsonObject.optString(fieldList[i].getName()) });
                }
            }
        }

        public static JSONArray joinJSONArrays(JSONArray a, JSONArray b) {
            JSONArray comb = new JSONArray();
            for (int i = 0; i < a.length(); i++) {
                comb.put(a.optJSONObject(i));
            }
            for (int i = 0; i < b.length(); i++) {
                comb.put(b.optJSONObject(i));
            }
            return comb;
        }

    }

    ```

3. <span data-ttu-id="b2169-178">建立名為 HttpClientHelper.java 的檔案，您將用來協助從您的 Azure AD 端點剖析 HTTP 資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-178">Create a file called HttpClientHelper.java, which you will use to help parse the HTTP data from your Azure AD endpoint.</span></span> <span data-ttu-id="b2169-179">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-179">To create the file, paste the following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.io.BufferedReader;
    import java.io.ByteArrayOutputStream;
    import java.io.IOException;
    import java.io.InputStream;
    import java.io.InputStreamReader;
    import java.io.OutputStreamWriter;
    import java.net.HttpURLConnection;

    import org.json.JSONException;
    import org.json.JSONObject;

    /**
     * This is Helper class for all RestClient class.
     *
     * @author Azure Active Directory Contributor
     *
     */
    public class HttpClientHelper {

        public HttpClientHelper() {
            super();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            BufferedReader reader = null;
            if (isSuccess) {
                reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {
                reader = new BufferedReader(new InputStreamReader(conn.getErrorStream()));
            }
            StringBuffer stringBuffer = new StringBuffer();
            String line = "";
            while ((line = reader.readLine()) != null) {
                stringBuffer.append(line);
            }

            return stringBuffer.toString();
        }

        public static String getResponseStringFromConn(HttpURLConnection conn, String payLoad) throws IOException {

            // Send the http message payload to the server.
            if (payLoad != null) {
                conn.setDoOutput(true);
                OutputStreamWriter osw = new OutputStreamWriter(conn.getOutputStream());
                osw.write(payLoad);
                osw.flush();
                osw.close();
            }

            // Get the message response from the server.
            BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            String line = "";
            StringBuffer stringBuffer = new StringBuffer();
            while ((line = br.readLine()) != null) {
                stringBuffer.append(line);
            }

            br.close();

            return stringBuffer.toString();
        }

        public static byte[] getByteaArrayFromConn(HttpURLConnection conn, boolean isSuccess) throws IOException {

            InputStream is = conn.getInputStream();
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            byte[] buff = new byte[1024];
            int bytesRead = 0;

            while ((bytesRead = is.read(buff, 0, buff.length)) != -1) {
                baos.write(buff, 0, bytesRead);
            }

            byte[] bytes = baos.toByteArray();
            baos.close();
            return bytes;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processResponse(int responseCode, String errorCode, String errorMsg) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            response.put("errorCode", errorCode);
            response.put("errorMsg", errorMsg);

            return response;
        }

        /**
         * for bad response, whose responseCode is not 200 level
         *
         * @param responseCode
         * @param errorCode
         * @param errorMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processGoodRespStr(int responseCode, String goodRespStr) throws JSONException {
            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (goodRespStr.equalsIgnoreCase("")) {
                response.put("responseMsg", "");
            } else {
                response.put("responseMsg", new JSONObject(goodRespStr));
            }

            return response;
        }

        /**
         * for good response
         *
         * @param responseCode
         * @param responseMsg
         * @return
         * @throws JSONException
         */
        public static JSONObject processBadRespStr(int responseCode, String responseMsg) throws JSONException {

            JSONObject response = new JSONObject();
            response.put("responseCode", responseCode);
            if (responseMsg.equalsIgnoreCase("")) { // good response is empty string
                response.put("responseMsg", "");
            } else { // bad response is json string
                JSONObject errorObject = new JSONObject(responseMsg).optJSONObject("odata.error");

                String errorCode = errorObject.optString("code");
                String errorMsg = errorObject.optJSONObject("message").optString("value");
                response.put("responseCode", responseCode);
                response.put("errorCode", errorCode);
                response.put("errorMsg", errorMsg);
            }

            return response;
        }

    }

    ```

## <a name="step-6-create-the-java-graph-api-model-files-for-basicfilter-mvc"></a><span data-ttu-id="b2169-180">步驟 6：建立 Java 圖形 API 模型檔案 (適用於 BasicFilter MVC)</span><span class="sxs-lookup"><span data-stu-id="b2169-180">Step 6: Create the Java Graph API Model files (for BasicFilter MVC)</span></span>
<span data-ttu-id="b2169-181">如前所述，您會使用圖形 API 來取得登入使用者的相關資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-181">As indicated previously, you use the Graph API to get data about the signed-in user.</span></span> <span data-ttu-id="b2169-182">為了讓處理順利進行，建立一個代表目錄物件的檔案以及一個代表使用者的檔案，如此便可以使用 Java 的 OO 模式。</span><span class="sxs-lookup"><span data-stu-id="b2169-182">To make this process easy, create both a file to represent a Directory object and a file to represent the user so that the OO pattern of Java can be used.</span></span>

1. <span data-ttu-id="b2169-183">建立名為 DirectoryObject.java 的檔案，用來儲存與任何目錄物件相關的基本資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-183">Create a file called DirectoryObject.java, which you use to store basic data about any Directory object.</span></span> <span data-ttu-id="b2169-184">稍後您可以對想要執行的任何其他圖形使用這個檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-184">You can use this file later for any other Graph queries you might perform.</span></span> <span data-ttu-id="b2169-185">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-185">To create the file, paste the following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    /**
     * @author Azure Active Directory Contributor
     *
     */
    public abstract class DirectoryObject {

        public DirectoryObject() {
            super();
        }

        /**
         *
         * @return
         */
        public abstract String getObjectId();

        /**
         * @param objectId
         */
        public abstract void setObjectId(String objectId);

        /**
         *
         * @return
         */
        public abstract String getObjectType();

        /**
         *
         * @param objectType
         */
        public abstract void setObjectType(String objectType);

        /**
         *
         * @return
         */
        public abstract String getDisplayName();

        /**
         *
         * @param displayName
         */
        public abstract void setDisplayName(String displayName);

    }

    ```

2. <span data-ttu-id="b2169-186">建立名為 User.java 的檔案，用來儲存來自目錄的任何使用者相關基本資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-186">Create a file called User.java, which you use to store basic data about any user from the directory.</span></span> <span data-ttu-id="b2169-187">這些是目錄資料的基本 getter 和 setter 方法，因此您可以貼上下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="b2169-187">These are basic getter and setter methods for directory data, so you can paste the following code:</span></span>

    ```Java

    package com.microsoft.aad.adal4jsample;

    import java.security.acl.Group;
    import java.util.ArrayList;

    import javax.xml.bind.annotation.XmlRootElement;

    import org.json.JSONObject;

    /**
    *  The **User** class holds together all the members of a WAAD User entity and all the access methods and set methods.
    *  @author Azure Active Directory Contributor
    */
    @XmlRootElement
    public class User extends DirectoryObject{

        // The following are the individual private members of a User object that holds
        // a particular simple attribute of a User object.
        protected String objectId;
        protected String objectType;
        protected String accountEnabled;
        protected String city;
        protected String country;
        protected String department;
        protected String dirSyncEnabled;
        protected String displayName;
        protected String facsimileTelephoneNumber;
        protected String givenName;
        protected String jobTitle;
        protected String lastDirSyncTime;
        protected String mail;
        protected String mailNickname;
        protected String mobile;
        protected String password;
        protected String passwordPolicies;
        protected String physicalDeliveryOfficeName;
        protected String postalCode;
        protected String preferredLanguage;
        protected String state;
        protected String streetAddress;
        protected String surname;
        protected String telephoneNumber;
        protected String usageLocation;
        protected String userPrincipalName;
        protected boolean isDeleted;  // this will move to dto

        /**
         * These four properties are for future use.
         */
        // managerDisplayname of this user.
        protected String managerDisplayname;

        // The directReports holds a list of directReports.
        private ArrayList<User> directReports;

        // The groups holds a list of group entities this user belongs to.
        private ArrayList<Group> groups;

        // The roles holds a list of role entities this user belongs to.
        private ArrayList<Group> roles;

        /**
         * The constructor for the **User** class. Initializes the dynamic lists and managerDisplayname variables.
         */
        public User(){
            directReports = null;
            groups = new ArrayList<Group>();
            roles = new ArrayList<Group>();
            managerDisplayname = null;
        }
    //    
    //    public User(String displayName, String objectId){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //    }
    //    
    //    public User(String displayName, String objectId, String userPrincipalName, String accountEnabled){
    //        setDisplayName(displayName);
    //        setObjectId(objectId);
    //        setUserPrincipalName(userPrincipalName);
    //        setAccountEnabled(accountEnabled);
    //    }
    //    

        /**
         * @return The objectId of this user.
         */
        public String getObjectId() {
            return objectId;
        }

        /**
         * @param objectId The objectId to set to this User object.
         */
        public void setObjectId(String objectId) {
            this.objectId = objectId;
        }

        /**
         * @return The objectType of this user.
         */
        public String getObjectType() {
            return objectType;
        }

        /**
         * @param objectType The objectType to set to this User object.
         */
        public void setObjectType(String objectType) {
            this.objectType = objectType;
        }

        /**
         * @return The userPrincipalName of this user.
         */
        public String getUserPrincipalName() {
            return userPrincipalName;
        }

        /**
         * @param userPrincipalName The userPrincipalName to set to this User object.
         */
        public void setUserPrincipalName(String userPrincipalName) {
            this.userPrincipalName = userPrincipalName;
        }

        /**
         * @return The usageLocation of this user.
         */
        public String getUsageLocation() {
            return usageLocation;
        }

        /**
         * @param usageLocation The usageLocation to set to this User object.
         */
        public void setUsageLocation(String usageLocation) {
            this.usageLocation = usageLocation;
        }

        /**
         * @return The telephoneNumber of this user.
         */
        public String getTelephoneNumber() {
            return telephoneNumber;
        }

        /**
         * @param telephoneNumber The telephoneNumber to set to this User object.
         */
        public void setTelephoneNumber(String telephoneNumber) {
            this.telephoneNumber = telephoneNumber;
        }

        /**
         * @return The surname of this user.
         */
        public String getSurname() {
            return surname;
        }

        /**
         * @param surname The surname to set to this User object.
         */
        public void setSurname(String surname) {
            this.surname = surname;
        }

        /**
         * @return The streetAddress of this user.
         */
        public String getStreetAddress() {
            return streetAddress;
        }

        /**
         * @param streetAddress The streetAddress to set to this user.
         */
        public void setStreetAddress(String streetAddress) {
            this.streetAddress = streetAddress;
        }

        /**
         * @return The state of this user.
         */
        public String getState() {
            return state;
        }

        /**
         * @param state The state to set to this User object.
         */
        public void setState(String state) {
            this.state = state;
        }

        /**
         * @return The preferredLanguage of this user.
         */
        public String getPreferredLanguage() {
            return preferredLanguage;
        }

        /**
         * @param preferredLanguage The preferredLanguage to set to this user.
         */
        public void setPreferredLanguage(String preferredLanguage) {
            this.preferredLanguage = preferredLanguage;
        }

        /**
         * @return The postalCode of this user.
         */
        public String getPostalCode() {
            return postalCode;
        }

        /**
         * @param postalCode The postalCode to set to this user.
         */
        public void setPostalCode(String postalCode) {
            this.postalCode = postalCode;
        }

        /**
         * @return The physicalDeliveryOfficeName of this user.
         */
        public String getPhysicalDeliveryOfficeName() {
            return physicalDeliveryOfficeName;
        }

        /**
         * @param physicalDeliveryOfficeName The physicalDeliveryOfficeName to set to this User object.
         */
        public void setPhysicalDeliveryOfficeName(String physicalDeliveryOfficeName) {
            this.physicalDeliveryOfficeName = physicalDeliveryOfficeName;
        }

        /**
         * @return The passwordPolicies of this user.
         */
        public String getPasswordPolicies() {
            return passwordPolicies;
        }

        /**
         * @param passwordPolicies The passwordPolicies to set to this User object.
         */
        public void setPasswordPolicies(String passwordPolicies) {
            this.passwordPolicies = passwordPolicies;
        }

        /**
         * @return The mobile of this user.
         */
        public String getMobile() {
            return mobile;
        }

        /**
         * @param mobile The mobile to set to this User object.
         */
        public void setMobile(String mobile) {
            this.mobile = mobile;
        }

        /**
         * @return The password of this user.
         */
        public String getPassword() {
            return password;
        }

        /**
         * @param password The mobile to set to this User object.
         */
        public void setPassword(String password) {
            this.password = password;
        }

        /**
         * @return The mail of this user.
         */
        public String getMail() {
            return mail;
        }

        /**
         * @param mail The mail to set to this User object.
         */
        public void setMail(String mail) {
            this.mail = mail;
        }

        /**
         * @return The MailNickname of this user.
         */
        public String getMailNickname() {
            return mailNickname;
        }

        /**
         * @param mail The MailNickname to set to this User object.
         */
        public void setMailNickname(String mailNickname) {
            this.mailNickname = mailNickname;
        }

        /**
         * @return The jobTitle of this user.
         */
        public String getJobTitle() {
            return jobTitle;
        }

        /**
         * @param jobTitle The jobTitle to set to this User object.
         */
        public void setJobTitle(String jobTitle) {
            this.jobTitle = jobTitle;
        }

        /**
         * @return The givenName of this user.
         */
        public String getGivenName() {
            return givenName;
        }

        /**
         * @param givenName The givenName to set to this User object.
         */
        public void setGivenName(String givenName) {
            this.givenName = givenName;
        }

        /**
         * @return The facsimileTelephoneNumber of this user.
         */
        public String getFacsimileTelephoneNumber() {
            return facsimileTelephoneNumber;
        }

        /**
         * @param facsimileTelephoneNumber The facsimileTelephoneNumber to set to this User object.
         */
        public void setFacsimileTelephoneNumber(String facsimileTelephoneNumber) {
            this.facsimileTelephoneNumber = facsimileTelephoneNumber;
        }

        /**
         * @return The displayName of this user.
         */
        public String getDisplayName() {
            return displayName;
        }

        /**
         * @param displayName The displayName to set to this User object.
         */
        public void setDisplayName(String displayName) {
            this.displayName = displayName;
        }

        /**
         * @return The dirSyncEnabled of this user.
         */
        public String getDirSyncEnabled() {
            return dirSyncEnabled;
        }

        /**
         * @param dirSyncEnabled The dirSyncEnabled to set to this User object.
         */
        public void setDirSyncEnabled(String dirSyncEnabled) {
            this.dirSyncEnabled = dirSyncEnabled;
        }

        /**
         * @return The department of this user.
         */
        public String getDepartment() {
            return department;
        }

        /**
         * @param department The department to set to this User object.
         */
        public void setDepartment(String department) {
            this.department = department;
        }

        /**
         * @return The lastDirSyncTime of this user.
         */
        public String getLastDirSyncTime() {
            return lastDirSyncTime;
        }

        /**
         * @param lastDirSyncTime The lastDirSyncTime to set to this User object.
         */
        public void setLastDirSyncTime(String lastDirSyncTime) {
            this.lastDirSyncTime = lastDirSyncTime;
        }

        /**
         * @return The country of this user.
         */
        public String getCountry() {
            return country;
        }

        /**
         * @param country The country to set to this user.
         */
        public void setCountry(String country) {
            this.country = country;
        }

        /**
         * @return The city of this user.
         */
        public String getCity() {
            return city;
        }

        /**
         * @param city The city to set to this user.
         */
        public void setCity(String city) {
            this.city = city;
        }

        /**
         * @return The accountEnabled attribute of this user.
         */
        public String getAccountEnabled() {
            return accountEnabled;
        }

        /**
         * @param accountEnabled The accountEnabled to set to this user.
         */
        public void setAccountEnabled(String accountEnabled) {
            this.accountEnabled = accountEnabled;
        }

        public boolean isIsDeleted() {
            return this.isDeleted;
        }

        public void setIsDeleted(boolean isDeleted) {
            this.isDeleted = isDeleted;
        }

        @Override
        public String toString() {
            return new JSONObject(this).toString();
        }

        public String getManagerDisplayname(){
            return managerDisplayname;
        }

        public void setManagerDisplayname(String managerDisplayname){
            this.managerDisplayname = managerDisplayname;
        }
    }

    /**
    * The DirectReports class holds the essential data for a single DirectReport entry. That is,
    * it holds the displayName and the objectId of the direct entry. It also provides the
    * access methods to set or get the displayName and the ObjectId of this entry.
    */
    //class DirectReport extends User{
    //
    //    private String displayName;
    //    private String objectId;
    //     
    //    /**
    //     * Two arguments Constructor for the DirectReport class.
    //     * @param displayName
    //     * @param objectId
    //     */
    //    public DirectReport(String displayName, String objectId){
    //        this.displayName = displayName;
    //        this.objectId = objectId;
    //    }
    //
    //    /**
    //     * @return The displayName of this direct report entry.
    //     */
    //    public String getDisplayName() {
    //        return displayName;
    //    }
    //
    //    
    //    /**
    //     *  @return The objectId of this direct report entry.
    //     */
    //    public String getObjectId() {
    //        return objectId;
    //    }
    //
    //}

    ```

## <a name="step-7-create-the-authentication-model-and-controller-files-for-basicfilter"></a><span data-ttu-id="b2169-188">步驟 7：建立驗證模型和控制器檔案 (適用於 BasicFilter)</span><span class="sxs-lookup"><span data-stu-id="b2169-188">Step 7: Create the authentication model and controller files (for BasicFilter)</span></span>
<span data-ttu-id="b2169-189">我們了解 Java 可能會非常繁複，但是您就快要完成了。</span><span class="sxs-lookup"><span data-stu-id="b2169-189">We acknowledge that Java can be verbose, but you're almost done.</span></span> <span data-ttu-id="b2169-190">在您撰寫 BasicFilter Servlet 以處理要求之前，您必須撰寫更多 ADAL4J 需要的協助程式檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-190">Before you write the BasicFilter servlet to handle the requests, you need to write some more helper files that the ADAL4J needs.</span></span>

1. <span data-ttu-id="b2169-191">建立名為 AuthHelper.java 的檔案，這可提供您用來判斷登入使用者狀態的方法。</span><span class="sxs-lookup"><span data-stu-id="b2169-191">Create a file called AuthHelper.java, which will give you methods to use to determine the state of the signed-in user.</span></span> <span data-ttu-id="b2169-192">方法包括︰</span><span class="sxs-lookup"><span data-stu-id="b2169-192">The methods include:</span></span>

 * <span data-ttu-id="b2169-193">**isAuthenticated()**：傳回使用者是否已登入。</span><span class="sxs-lookup"><span data-stu-id="b2169-193">**isAuthenticated()**: Returns whether the user is signed in.</span></span>
 * <span data-ttu-id="b2169-194">**containsAuthenticationData()**：傳回權杖是否具有資料。</span><span class="sxs-lookup"><span data-stu-id="b2169-194">**containsAuthenticationData()**: Returns whether the token has data.</span></span>
 * <span data-ttu-id="b2169-195">**isAuthenticationSuccessful()**：傳回使用者的驗證是否成功。</span><span class="sxs-lookup"><span data-stu-id="b2169-195">**isAuthenticationSuccessful()**: Returns whether the authentication was successful for the user.</span></span>

 <span data-ttu-id="b2169-196">若要建立 AuthHelper.java 檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-196">To create the AuthHelper.java file, paste the following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.util.Map;

    import javax.servlet.http.HttpServletRequest;

    import com.microsoft.aad.adal4j.AuthenticationResult;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
    import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
    import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

    public final class AuthHelper {

        public static final String PRINCIPAL_SESSION_NAME = "principal";

        private AuthHelper() {
        }

        public static boolean isAuthenticated(HttpServletRequest request) {
            return request.getSession().getAttribute(PRINCIPAL_SESSION_NAME) != null;
        }

        public static AuthenticationResult getAuthSessionObject(
                HttpServletRequest request) {
            return (AuthenticationResult) request.getSession().getAttribute(
                    PRINCIPAL_SESSION_NAME);
        }

        public static boolean containsAuthenticationData(
                HttpServletRequest httpRequest) {
            Map<String, String[]> map = httpRequest.getParameterMap();
            return httpRequest.getMethod().equalsIgnoreCase("POST") && (httpRequest.getParameterMap().containsKey(
                            AuthParameterNames.ERROR)
                            || httpRequest.getParameterMap().containsKey(
                                    AuthParameterNames.ID_TOKEN) || httpRequest
                            .getParameterMap().containsKey(AuthParameterNames.CODE));
        }

        public static boolean isAuthenticationSuccessful(
                AuthenticationResponse authResponse) {
            return authResponse instanceof AuthenticationSuccessResponse;
        }
    }
    ```

2. <span data-ttu-id="b2169-197">建立名為 AuthParameterNames.java 的檔案，給予您 ADAL4J 所需的一些不可變變數。</span><span class="sxs-lookup"><span data-stu-id="b2169-197">Create a file called AuthParameterNames.java, which gives you some immutable variables that the ADAL4J requires.</span></span> <span data-ttu-id="b2169-198">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-198">To create the file, paste the following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    public final class AuthParameterNames {

        private AuthParameterNames() {
        }

        public static String ERROR = "error";
        public static String ERROR_DESCRIPTION = "error_description";
        public static String ERROR_URI = "error_uri";
        public static String ID_TOKEN = "id_token";
        public static String CODE = "code";
    }
    ```

3. <span data-ttu-id="b2169-199">建立名為 AadController.java 的檔案，它是 MVC 模式的控制器。</span><span class="sxs-lookup"><span data-stu-id="b2169-199">Create a file called AadController.java, which is the controller of your MVC pattern.</span></span> <span data-ttu-id="b2169-200">檔案給予您 JSP 控制器，並且會公開應用程式的安全/aad URL 端點。</span><span class="sxs-lookup"><span data-stu-id="b2169-200">The file gives you the JSP controller and exposes the secure/aad URL endpoint for the app.</span></span> <span data-ttu-id="b2169-201">檔案也包括圖形查詢。</span><span class="sxs-lookup"><span data-stu-id="b2169-201">The file also includes the graph query.</span></span> <span data-ttu-id="b2169-202">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-202">To create the file, paste the following code:</span></span>

    ```Java
    package com.microsoft.aad.adal4jsample;

    import java.net.HttpURLConnection;
    import java.net.URL;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpSession;

    import org.json.JSONArray;
    import org.json.JSONObject;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.ModelMap;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;

    import com.microsoft.aad.adal4j.AuthenticationResult;

    @Controller
    @RequestMapping("/secure/aad")
    public class AadController {

        @RequestMapping(method = { RequestMethod.GET, RequestMethod.POST })
        public String getDirectoryObjects(ModelMap model, HttpServletRequest httpRequest) {
            HttpSession session = httpRequest.getSession();
            AuthenticationResult result = (AuthenticationResult) session.getAttribute(AuthHelper.PRINCIPAL_SESSION_NAME);
            if (result == null) {
                model.addAttribute("error", new Exception("AuthenticationResult not found in session."));
                return "/error";
            } else {
                String data;
                try {
                    data = this.getUsernamesFromGraph(result.getAccessToken(), session.getServletContext()
                            .getInitParameter("tenant"));
                    model.addAttribute("users", data);
                } catch (Exception e) {
                    model.addAttribute("error", e);
                    return "/error";
                }
            }
            return "/secure/aad";
        }

        private String getUsernamesFromGraph(String accessToken, String tenant) throws Exception {
            URL url = new URL(String.format("https://graph.windows.net/%s/users?api-version=2013-04-05", tenant,
                    accessToken));

            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            // Set the appropriate header fields in the request header.
            conn.setRequestProperty("api-version", "2013-04-05");
            conn.setRequestProperty("Authorization", accessToken);
            conn.setRequestProperty("Accept", "application/json;odata=minimalmetadata");
            String goodRespStr = HttpClientHelper.getResponseStringFromConn(conn, true);
            // logger.info("goodRespStr ->" + goodRespStr);
            int responseCode = conn.getResponseCode();
            JSONObject response = HttpClientHelper.processGoodRespStr(responseCode, goodRespStr);
            JSONArray users = new JSONArray();

            users = JSONHelper.fetchDirectoryObjectJSONArray(response);

            StringBuilder builder = new StringBuilder();
            User user = null;
            for (int i = 0; i < users.length(); i++) {
                JSONObject thisUserJSONObject = users.optJSONObject(i);
                user = new User();
                JSONHelper.convertJSONObjectToDirectoryObject(thisUserJSONObject, user);
                builder.append(user.getUserPrincipalName() + "<br/>");
            }
            return builder.toString();
        }

    }

    ```

## <a name="step-8-create-the-basicfilter-file-for-basicfilter-mvc"></a><span data-ttu-id="b2169-203">步驟 8：建立 BasicFilter 檔案 (適用於 BasicFilter MVC)</span><span class="sxs-lookup"><span data-stu-id="b2169-203">Step 8: Create the BasicFilter file (for BasicFilter MVC)</span></span>
<span data-ttu-id="b2169-204">您現在可以建立 BasicFilter.java 檔案，處理來自 JSP 檢視檔案的要求。</span><span class="sxs-lookup"><span data-stu-id="b2169-204">You can now create the BasicFilter.java file, which handles the requests from the JSP View files.</span></span> <span data-ttu-id="b2169-205">若要建立檔案，貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b2169-205">To create the file, paste the following code:</span></span>

```Java

package com.microsoft.aad.adal4jsample;

import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.net.URI;
import java.net.URLEncoder;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;
import com.nimbusds.oauth2.sdk.AuthorizationCode;
import com.nimbusds.openid.connect.sdk.AuthenticationErrorResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponse;
import com.nimbusds.openid.connect.sdk.AuthenticationResponseParser;
import com.nimbusds.openid.connect.sdk.AuthenticationSuccessResponse;

public class BasicFilter implements Filter {

    private String clientId = "";
    private String clientSecret = "";
    private String tenant = "";
    private String authority;

    public void destroy() {

    }

    public void doFilter(ServletRequest request, ServletResponse response,
            FilterChain chain) throws IOException, ServletException {

        if (request instanceof HttpServletRequest) {
            HttpServletRequest httpRequest = (HttpServletRequest) request;
            HttpServletResponse httpResponse = (HttpServletResponse) response;
            try {

                String currentUri = request.getScheme()
                        + "://"
                        + request.getServerName()
                        + ("http".equals(request.getScheme())
                                && request.getServerPort() == 80
                                || "https".equals(request.getScheme())
                                && request.getServerPort() == 443 ? "" : ":"
                                + request.getServerPort())
                        + httpRequest.getRequestURI();
                String fullUrl = currentUri
                        + (httpRequest.getQueryString() != null ? "?"
                                + httpRequest.getQueryString() : "");
                // check if user has a session
                if (!AuthHelper.isAuthenticated(httpRequest)) {
                    if (AuthHelper.containsAuthenticationData(httpRequest)) {
                        Map<String, String> params = new HashMap<String, String>();
                        for (String key : request.getParameterMap().keySet()) {
                            params.put(key,
                                    request.getParameterMap().get(key)[0]);
                        }
                        AuthenticationResponse authResponse = AuthenticationResponseParser
                                .parse(new URI(fullUrl), params);
                        if (AuthHelper.isAuthenticationSuccessful(authResponse)) {

                            AuthenticationSuccessResponse oidcResponse = (AuthenticationSuccessResponse) authResponse;
                            AuthenticationResult result = getAccessToken(
                                    oidcResponse.getAuthorizationCode(),
                                    currentUri);
                            createSessionPrincipal(httpRequest, result);
                        } else {
                            AuthenticationErrorResponse oidcResponse = (AuthenticationErrorResponse) authResponse;
                            throw new Exception(String.format(
                                    "Request for auth code failed: %s - %s",
                                    oidcResponse.getErrorObject().getCode(),
                                    oidcResponse.getErrorObject()
                                            .getDescription()));
                        }
                    } else {
                            // not authenticated
                            httpResponse.setStatus(302);
                            httpResponse
                                    .sendRedirect(getRedirectUrl(currentUri));
                            return;
                    }
                } else {
                    // if authenticated, how to check for valid session?
                    AuthenticationResult result = AuthHelper
                            .getAuthSessionObject(httpRequest);

                    if (httpRequest.getParameter("refresh") != null) {
                        result = getAccessTokenFromRefreshToken(
                                result.getRefreshToken(), currentUri);
                    } else {
                        if (httpRequest.getParameter("cc") != null) {
                            result = getAccessTokenFromClientCredentials();
                        } else {
                            if (result.getExpiresOnDate().before(new Date())) {
                                result = getAccessTokenFromRefreshToken(
                                        result.getRefreshToken(), currentUri);
                            }
                        }
                    }
                    createSessionPrincipal(httpRequest, result);
                }
            } catch (Throwable exc) {
                httpResponse.setStatus(500);
                request.setAttribute("error", exc.getMessage());
                httpResponse.sendRedirect(((HttpServletRequest) request)
                        .getContextPath() + "/error.jsp");
            }
        }
        chain.doFilter(request, response);
    }

    private AuthenticationResult getAccessTokenFromClientCredentials()
            throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", new ClientCredential(clientId,
                            clientSecret), null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private AuthenticationResult getAccessTokenFromRefreshToken(
            String refreshToken, String currentUri) throws Throwable {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByRefreshToken(refreshToken,
                            new ClientCredential(clientId, clientSecret), null,
                            null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;

    }

    private AuthenticationResult getAccessToken(
            AuthorizationCode authorizationCode, String currentUri)
            throws Throwable {
        String authCode = authorizationCode.getValue();
        ClientCredential credential = new ClientCredential(clientId,
                clientSecret);
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(authority + tenant + "/", true,
                    service);
            Future<AuthenticationResult> future = context
                    .acquireTokenByAuthorizationCode(authCode, new URI(
                            currentUri), credential, null);
            result = future.get();
        } catch (ExecutionException e) {
            throw e.getCause();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }

    private void createSessionPrincipal(HttpServletRequest httpRequest,
            AuthenticationResult result) throws Exception {
        httpRequest.getSession().setAttribute(
                AuthHelper.PRINCIPAL_SESSION_NAME, result);
    }

    private String getRedirectUrl(String currentUri)
            throws UnsupportedEncodingException {
        String redirectUrl = authority
                + this.tenant
                + "/oauth2/authorize?response_type=code%20id_token&scope=openid&response_mode=form_post&redirect_uri="
                + URLEncoder.encode(currentUri, "UTF-8") + "&client_id="
                + clientId + "&resource=https%3a%2f%2fgraph.windows.net"
                + "&nonce=" + UUID.randomUUID() + "&site_id=500879";
        return redirectUrl;
    }

    public void init(FilterConfig config) throws ServletException {
        clientId = config.getInitParameter("client_id");
        authority = config.getServletContext().getInitParameter("authority");
        tenant = config.getServletContext().getInitParameter("tenant");
        clientSecret = config.getInitParameter("secret_key");
    }

}

```

<span data-ttu-id="b2169-206">此 Servlet 會公開 ADAL4J 預期來自應用程式用以執行的所有方法。</span><span class="sxs-lookup"><span data-stu-id="b2169-206">This servlet exposes all the methods that the ADAL4J will expect from the app to run.</span></span> <span data-ttu-id="b2169-207">方法包括︰</span><span class="sxs-lookup"><span data-stu-id="b2169-207">The methods include:</span></span>

* <span data-ttu-id="b2169-208">**getAccessTokenFromClientCredentials()**：從密碼取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b2169-208">**getAccessTokenFromClientCredentials()**: Gets the access token from the secret.</span></span>
* <span data-ttu-id="b2169-209">**getAccessTokenFromRefreshToken()**：從重新整理權杖取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b2169-209">**getAccessTokenFromRefreshToken()**: Gets the access token from a refresh token.</span></span>
* <span data-ttu-id="b2169-210">**getAccessToken()**：從 OpenID Connect 流程 (您所使用的) 取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b2169-210">**getAccessToken()**: Gets the access token from an OpenID Connect flow (which you use).</span></span>
* <span data-ttu-id="b2169-211">**createSessionPrincipal()**：建立工作階段主體以用於圖形 API 存取。</span><span class="sxs-lookup"><span data-stu-id="b2169-211">**createSessionPrincipal()**: Creates a session principal to use for Graph API access.</span></span>
* <span data-ttu-id="b2169-212">**getRedirectUrl()**：取得 redirectURL 以與您在入口網站中輸入的值進行比較。</span><span class="sxs-lookup"><span data-stu-id="b2169-212">**getRedirectUrl()**: Gets the redirectURL to compare it with the value you entered in the portal.</span></span>

## <a name="step-9-compile-and-run-the-sample-in-tomcat"></a><span data-ttu-id="b2169-213">步驟 9：在 Tomcat 中編譯和執行範例</span><span class="sxs-lookup"><span data-stu-id="b2169-213">Step 9: Compile and run the sample in Tomcat</span></span>

1. <span data-ttu-id="b2169-214">變更至根目錄。</span><span class="sxs-lookup"><span data-stu-id="b2169-214">Change to your root directory.</span></span>
2. <span data-ttu-id="b2169-215">若要藉由使用 `maven` 建置您剛剛拼湊在一起的範例，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b2169-215">To build the sample you just put together by using `maven`, run the following command:</span></span>

    `$ mvn package`

 <span data-ttu-id="b2169-216">此命令會使用您針對相依性撰寫的 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-216">This command uses the pom.xml file that you wrote for dependencies.</span></span>

<span data-ttu-id="b2169-217">您現在在 /targets 目錄中應該有 adal4jsample.war 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-217">You should now have a adal4jsample.war file in your /targets directory.</span></span> <span data-ttu-id="b2169-218">您可以在 Tomcat 容器中部署檔案，並且瀏覽 http://localhost:8080//adal4jsample/URL。</span><span class="sxs-lookup"><span data-stu-id="b2169-218">You can deploy the file in your Tomcat container and visit the http://localhost:8080/adal4jsample/ URL.</span></span>

> [!NOTE]
> <span data-ttu-id="b2169-219">您可以使用最新的 Tomcat 伺服器，輕易地部署 .war 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2169-219">You can easily deploy a .war file with the latest Tomcat servers.</span></span> <span data-ttu-id="b2169-220">移至 http://localhost:8080/manager/，然後遵循上傳 adal4jsample.war 檔案的指示。</span><span class="sxs-lookup"><span data-stu-id="b2169-220">Go to http://localhost:8080/manager/, and follow the instructions for uploading the adal4jsample.war file.</span></span> <span data-ttu-id="b2169-221">它會為您自動部署正確的端點。</span><span class="sxs-lookup"><span data-stu-id="b2169-221">It will autodeploy for you with the correct endpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2169-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2169-222">Next steps</span></span>
<span data-ttu-id="b2169-223">您現在有一個可運作的 Java 應用程式，能夠驗證使用者、使用 OAuth 2.0 安全地呼叫 Web API，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="b2169-223">You now have a working Java app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the users.</span></span> <span data-ttu-id="b2169-224">如果您還沒有這麼做，現在是將使用者植入租用戶的好時機。</span><span class="sxs-lookup"><span data-stu-id="b2169-224">If you haven't already populated your tenant with users, now is a good time to do so.</span></span>

<span data-ttu-id="b2169-225">如需其他參考，您可以使用兩種方式其中之一取得完整的範例 (不含您的組態值)︰</span><span class="sxs-lookup"><span data-stu-id="b2169-225">For additional reference, you can get the completed sample (without your configuration values) in either of two ways:</span></span>

* <span data-ttu-id="b2169-226">下載為 [.zip 檔案](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="b2169-226">Download it as a [.zip file](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip).</span></span>
* <span data-ttu-id="b2169-227">輸入下列命令，從 GitHub 複製檔案：</span><span class="sxs-lookup"><span data-stu-id="b2169-227">Clone the file from GitHub by entering the following command:</span></span>

 ```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```
