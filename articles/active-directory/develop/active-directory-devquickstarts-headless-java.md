---
title: "aaaAzure AD Java 命令列開始使用 |Microsoft 文件"
description: "如何 toobuild Java 命令列應用程式簽署 tooaccess 應用程式開發介面中的使用者。"
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>使用 Java 命令列應用程式 tooAccess API 與 Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD 可讓簡單又直接 toooutsource web 應用程式的身分識別管理，提供單一登入和登出只有幾行程式碼。  在 Java web 應用程式，您可以完成這項作業使用 Microsoft hello 社群導向 ADAL4J 實作。

  我們將在此處使用 ADAL4J 來執行下列動作：

* 登入 hello hello 身分識別提供者以使用 Azure AD 的應用程式 hello 使用者。
* 顯示 hello 使用者的一些資訊。
* 符號 hello 使用者登出 hello 應用程式。

在順序 toodo 這樣，您將需要：

1. 向 Azure AD 註冊應用程式
2. 設定您的應用程式 toouse hello ADAL4J 程式庫。
3. 使用 hello ADAL4J 文件庫 tooissue 登入和登出要求 tooAzure AD。
4. 列印出 hello 使用者的相關資料。

啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip)。  您還需要哪些 tooregister 中的 Azure AD 租用戶應用程式。  如果沒有，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="1--register-an-application-with-azure-ad"></a>1.向 Azure AD 註冊應用程式
tooenable 您 tooauthenticate 應用程式的使用者，您必須先 tooregister 新的應用程式在您的租用戶。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。
3. 按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選擇 [新增]。
5. 依照 hello 提示，並建立新**Web 應用程式和/或 WebAPI**。
  * hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者
  * hello**登入 URL**是 hello 基底 URL 的應用程式。  hello 基本架構的預設值是`http://localhost:8080/adal4jsample/`。
6. 完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。  您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。
7. 從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。 hello**應用程式識別碼 URI**是您的應用程式的唯一識別碼。  hello 慣例是 toouse `https://<tenant-domain>/<app-name>`，例如`http://localhost:8080/adal4jsample/`。

一次在 hello 入口網站應用程式建立**金鑰**從 hello**設定**您的應用程式頁面，並將它複製下來。  稍後您將會用到此資訊。

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2.設定您的應用程式 toouse ADAL4J 程式庫和使用 Maven 的必要條件
在這裡，我們會將設定 ADAL4J toouse hello OpenID Connect 驗證通訊協定。  ADAL4J 將會使用的 tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，在其他項目之間的相關資訊。

* Hello 根目錄中您的專案，開啟/建立`pom.xml`並找出 hello`// TODO: provide dependencies for Maven`並取代 hello 下列：

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
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
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
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
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a>3.建立 hello Java PublicClient 檔案
如前文所述，我們將使用 hello Graph API tooget hello 登入的使用者資料。 我們應針對此 toobe 容易讓我們來建立這兩個檔案 toorepresent**目錄物件**和個別檔案 toorepresent hello**使用者**以便 hello OO 模式的 Java 可用。

* 建立一個叫做檔案`DirectoryObject.java`我們將會使用 toostore 有關任何 DirectoryObject （您可能感覺受到總公司可用 toouse 這稍後可能會執行任何其他圖形查詢） 的基本資料。 您可以從下面剪下/貼上：

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a>編譯並執行 hello 範例
寫出 tooyour 根目錄變更，然後執行下列命令 toobuild hello 範例，您只要將放在一起使用的 hello `maven`。 此選項會使用 hello`pom.xml`您所撰寫的相依性的檔案。

`$ mvn package`

您的 `/targets` 目錄中現在應包含 `adal4jsample.war` 檔案。 您可能會部署在 Tomcat 容器中，瀏覽 hello URL 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> 它是很容易 toodeploy WAR 與 hello 最新的 Tomcat 伺服器。 直接瀏覽過`http://localhost:8080/manager/`並上傳遵循 hello 指示您 ' adal4jsample.war' 檔案。 它會為您的 autodeploy 與 hello 正確端點。
> 
> 

## <a name="next-steps"></a>後續步驟
恭喜！ 您現在擁有可運作的 Java 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。  如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。

如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)，或您可以將其複製從 GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

