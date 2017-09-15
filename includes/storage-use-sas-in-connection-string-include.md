<span data-ttu-id="1eca6-101">如果您具有授與您存取儲存體帳戶中資源的共用存取簽章 (SAS) URL，您可以在連接字串中使用 SAS。</span><span class="sxs-lookup"><span data-stu-id="1eca6-101">If you possess a shared access signature (SAS) URL that grants you access to resources in a storage account, you can use the SAS in a connection string.</span></span> <span data-ttu-id="1eca6-102">因為 SAS 包含驗證要求所需的資訊，所以含有 SAS 的連接字串會提供通訊協定、服務端點，以及存取資源所需的認證。</span><span class="sxs-lookup"><span data-stu-id="1eca6-102">Because the SAS contains the information required to authenticate the request, a connection string with a SAS provides the protocol, the service endpoint, and the necessary credentials to access the resource.</span></span>

<span data-ttu-id="1eca6-103">若要建立包含共用存取簽章的連接字串，請以下列格式指定字串：</span><span class="sxs-lookup"><span data-stu-id="1eca6-103">To create a connection string that includes a shared access signature, specify the string in the following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="1eca6-104">雖然連接字串必須包含至少一個服務端點，但是每個服務端點都是選用的。</span><span class="sxs-lookup"><span data-stu-id="1eca6-104">Each service endpoint is optional, although the connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="1eca6-105">建議最好搭配使用 HTTPS 與 SAS。</span><span class="sxs-lookup"><span data-stu-id="1eca6-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="1eca6-106">如果您在組態檔的連接字串中指定 SAS，則可能需要編碼 URL 中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="1eca6-106">If you are specifying a SAS in a connection string in a configuration file, you may need to encode special characters in the URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="1eca6-107">服務 SAS 範例</span><span class="sxs-lookup"><span data-stu-id="1eca6-107">Service SAS example</span></span>
<span data-ttu-id="1eca6-108">以下範例是包含服務 SAS for Blob 儲存體的連接字串：</span><span class="sxs-lookup"><span data-stu-id="1eca6-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="1eca6-109">而以下範例是具有特殊字元編碼的相同連接字串︰</span><span class="sxs-lookup"><span data-stu-id="1eca6-109">And here's an example of the same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="1eca6-110">帳戶 SAS 範例</span><span class="sxs-lookup"><span data-stu-id="1eca6-110">Account SAS example</span></span>
<span data-ttu-id="1eca6-111">以下範例是包含帳戶 SAS for Blob 和檔案儲存體的連接字串。</span><span class="sxs-lookup"><span data-stu-id="1eca6-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="1eca6-112">請注意，指定兩個服務的端點︰</span><span class="sxs-lookup"><span data-stu-id="1eca6-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="1eca6-113">而以下範例是具有 URL 編碼的相同連接字串︰</span><span class="sxs-lookup"><span data-stu-id="1eca6-113">And here's an example of the same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

