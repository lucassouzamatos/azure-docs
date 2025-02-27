---
title: Debug in Visual Studio with Azure Application Insights
description: Web app performance analysis and diagnostics during debugging and in production.
ms.topic: conceptual
ms.date: 03/17/2017
ms.custom: vs-azure
ms.reviewer: daviste
---

# Debug your applications with Azure Application Insights in Visual Studio
In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](./app-insights-overview.md).

If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK. Otherwise, if you haven't done so already, [add Application Insights to your app](./asp-net.md).

To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools. But for debugging, you can also search and analyze the telemetry in Visual Studio. You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine. In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal. 

## <a name="run"></a> Debug your project
Run your web app in local debug mode by using F5. Open different pages to generate some telemetry.

In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.

![In Visual Studio, the Application Insights button shows during debugging.](./media/visual-studio/appinsights-09eventcount.png)

Click this button to search your telemetry. 

## Application Insights search
The Application Insights Search window shows events that have been logged. (If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)

![Right-click the project and choose Application Insights, Search](./media/visual-studio/34.png)

> [!NOTE] 
> After you select or deselect filters, click the Search button at the end of the text search field.
>

The free text search works on any fields in the events. For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.

Click any event to see its detailed properties.

For requests to your web app, you can click through to the code.

![Under Request Details, click through to the code](./media/visual-studio/31.png)

You can also open related items to help diagnose failed requests or exceptions.

![Under Request Details, scroll down to related items](./media/visual-studio/41.png)

## View exceptions and failed requests
Exception reports show in the Search window. (In some older types of ASP.NET application, you have to [set up exception monitoring](./asp-net-exceptions.md) to see exceptions that are handled by the framework.)

Click an exception to get a stack trace. If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.

![Screenshot shows the About object in a stack trace.](./media/visual-studio/17.png)

## View request and exception summaries in the code
In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.

![Screenshot shows an exception in a context dialog box.](./media/visual-studio/21.png)

> [!NOTE] 
> Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](./asp-net.md).
>

[More about Application Insights in Code Lens](./visual-studio-codelens.md)

## Local monitoring
(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session. 

This is desirable if you have already published a previous version of your app. You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.

It's also useful if you have some [custom telemetry](./api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.

* *At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*
  
  * In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.
  * To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-instrumentation-key-deprecation.md)]

## Next steps

 * **[Working with the Application Insights portal](./overview-dashboard.md)**. View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data. 

