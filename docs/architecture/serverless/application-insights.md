---
title: Application Insights-无服务器应用
description: Application Insights 是一种无服务器诊断平台, 使开发人员能够检测、会审和诊断 web 应用、移动应用、桌面应用和微服务中的问题。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 1f5b99fba448c2c1c12139524ffdcd3708b3c956
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577720"
---
# <a name="telemetry-with-application-insights"></a><span data-ttu-id="6cb48-103">具有 Application Insights 的遥测</span><span class="sxs-lookup"><span data-stu-id="6cb48-103">Telemetry with Application Insights</span></span>

<span data-ttu-id="6cb48-104">[Application Insights](https://docs.microsoft.com/azure/application-insights)是一种无服务器诊断平台, 使开发人员能够检测、会审和诊断 web 应用、移动应用、桌面应用和微服务中的问题。</span><span class="sxs-lookup"><span data-stu-id="6cb48-104">[Application Insights](https://docs.microsoft.com/azure/application-insights) is a serverless diagnostics platform that enables developers to detect, triage, and diagnose issues in web apps, mobile apps, desktop apps, and microservices.</span></span> <span data-ttu-id="6cb48-105">只需在门户中翻转交换机, 就可以打开函数应用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="6cb48-105">You can turn on Application Insights for function apps simply by flipping a switch in the portal.</span></span> <span data-ttu-id="6cb48-106">Application Insights 提供所有这些功能, 而无需配置服务器或设置自己的数据库。</span><span class="sxs-lookup"><span data-stu-id="6cb48-106">Application Insights provides all of these capabilities without you having to configure a server or set up your own database.</span></span> <span data-ttu-id="6cb48-107">所有 Application Insights 功能都作为服务提供, 可自动与你的应用集成。</span><span class="sxs-lookup"><span data-stu-id="6cb48-107">All of Application Insights' capabilities are provided as a service that automatically integrates with your apps.</span></span>

![Application Insights 徽标](./media/application-insights-logo.png)

<span data-ttu-id="6cb48-109">向现有应用程序添加 Application Insights 与将检测密钥添加到应用程序的设置一样简单。</span><span class="sxs-lookup"><span data-stu-id="6cb48-109">Adding Application Insights to existing apps is as easy as adding an instrumentation key to your application's settings.</span></span> <span data-ttu-id="6cb48-110">通过 Application Insights 您可以:</span><span class="sxs-lookup"><span data-stu-id="6cb48-110">With Application Insights you can:</span></span>

* <span data-ttu-id="6cb48-111">基于诸如函数调用数、运行函数所用的时间、异常等指标创建自定义图表和警报</span><span class="sxs-lookup"><span data-stu-id="6cb48-111">Create custom charts and alerts based on metrics such as number of function invocations, the time it takes to run a function, and exceptions</span></span>
* <span data-ttu-id="6cb48-112">分析失败和服务器异常</span><span class="sxs-lookup"><span data-stu-id="6cb48-112">Analyze failures and server exceptions</span></span>
* <span data-ttu-id="6cb48-113">按操作深化性能并测量调用第三方依赖项所用的时间</span><span class="sxs-lookup"><span data-stu-id="6cb48-113">Drill into performance by operation and measure the time it takes to call third-party dependencies</span></span>
* <span data-ttu-id="6cb48-114">监视托管函数应用的所有服务器上的 CPU 使用情况、内存和速率</span><span class="sxs-lookup"><span data-stu-id="6cb48-114">Monitor CPU usage, memory, and rates across all servers that host your function apps</span></span>
* <span data-ttu-id="6cb48-115">查看实时指标, 包括函数应用的请求计数和延迟</span><span class="sxs-lookup"><span data-stu-id="6cb48-115">View a live stream of metrics including request count and latency for your function apps</span></span>
* <span data-ttu-id="6cb48-116">使用[分析](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)搜索、查询和创建对函数数据的自定义图表</span><span class="sxs-lookup"><span data-stu-id="6cb48-116">Use [Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics) to search, query, and create custom charts over your function data</span></span>

![指标资源管理器](./media/metrics-explorer.png)

<span data-ttu-id="6cb48-118">除了内置遥测, 还可以生成自定义遥测。</span><span class="sxs-lookup"><span data-stu-id="6cb48-118">In addition to built-in telemetry, it's also possible to generate custom telemetry.</span></span> <span data-ttu-id="6cb48-119">以下代码片段使用为函数应用设置的检测密钥来创建自定义遥测客户端:</span><span class="sxs-lookup"><span data-stu-id="6cb48-119">The following code snippet creates a custom telemetry client using the instrumentation key set for the function app:</span></span>

```csharp
public static TelemetryClient telemetry = new TelemetryClient()
{
    InstrumentationKey = Environment.GetEnvironmentVariable("APPINSIGHTS_INSTRUMENTATIONKEY")
};
```

<span data-ttu-id="6cb48-120">以下代码测量将新行插入[Azure 表存储](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)实例所花费的时间:</span><span class="sxs-lookup"><span data-stu-id="6cb48-120">The following code measures how long it takes to insert a new row into an [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) instance:</span></span>

```csharp
var operation = TableOperation.Insert(entry);
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
await table.ExecuteAsync(operation);
telemetry.TrackDependency("AzureTableStorageInsert", "Insert", startTime, timer.Elapsed, true);
```

<span data-ttu-id="6cb48-121">将显示生成的性能图:</span><span class="sxs-lookup"><span data-stu-id="6cb48-121">The resulting performance graph is shown:</span></span>

![自定义遥测](./media/custom-telemetry.png)

<span data-ttu-id="6cb48-123">自定义遥测显示插入新行的平均时间为32.6 毫秒。</span><span class="sxs-lookup"><span data-stu-id="6cb48-123">The custom telemetry reveals the average time to insert a new row is 32.6 milliseconds.</span></span>

<span data-ttu-id="6cb48-124">Application Insights 提供了一种强大而方便的方法来记录有关无服务器应用程序的详细遥测数据。</span><span class="sxs-lookup"><span data-stu-id="6cb48-124">Application Insights provides a powerful, convenient way to log detailed telemetry about your serverless applications.</span></span> <span data-ttu-id="6cb48-125">你可以完全控制所提供的跟踪和日志记录级别。</span><span class="sxs-lookup"><span data-stu-id="6cb48-125">You have full control over the level of tracing and logging that is provided.</span></span> <span data-ttu-id="6cb48-126">可以跟踪自定义统计信息, 如事件、依赖项和页面视图。</span><span class="sxs-lookup"><span data-stu-id="6cb48-126">You can track custom statistics such as events, dependencies, and page view.</span></span> <span data-ttu-id="6cb48-127">最后, 利用强大的分析功能, 您可以编写查询来询问重要问题并生成图表和高级见解。</span><span class="sxs-lookup"><span data-stu-id="6cb48-127">Finally, the powerful analytics enable you to write queries that ask important questions and generate charts and advanced insights.</span></span>

<span data-ttu-id="6cb48-128">有关详细信息, 请参阅[Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)。</span><span class="sxs-lookup"><span data-stu-id="6cb48-128">For more information, see [Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="6cb48-129">[上一页](azure-functions.md)
>[下一页](logic-apps.md)</span><span class="sxs-lookup"><span data-stu-id="6cb48-129">[Previous](azure-functions.md)
[Next](logic-apps.md)</span></span>