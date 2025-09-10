# Using AXA Bindings Library in .NET MAUI apps

### Installation

1. Open your project to add the `AXAiOSBindings_MAUI.dll` package.
2. Right-click on **Dependencies**, select **Manage NuGet Packages**, and search the **AXAiOSBindings_MAUI.dll** file from the list in the Nuget packages window under the **nuget.org** Package source and then click **Add Package**.
3. Add the `<app_name>_camdo.plist` file to your project as a bundle resource
    For example:
    ```csharp
    <ItemGroup>
        <BundleResource Include="xxx_camdo.plist" />
    </ItemGroup>
    ```
4. Add the following permissions to your application `Info.plist`, if not already present.
    ```sh
    <key>NSLocationWhenInUseUsageDescription</key>
        <string>This allows us to track and gather analytic data for improving the app experience.</string>
    <key>NSLocationAlwaysUsageDescription</key>
        <string>This allows us to track and gather analytic data for improving the app experience.</string>
    <key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
        <string>This allows us to track and gather analytic data for improving the app experience.</string>
    ```
### Initialising the SDK in your Source Code

Initialise the CAMobileAppAnalytics SDK in **MauiProgram.cs** in iOS **FinishedLaunching** event 
1. Import AXAiOSBindings_MAUI
    ```csharp
    #if IOS
        using AXAiOSBindings_MAUI;
    #endif
    ``` 
2. Initialise the SDK
    ```csharp
    .ConfigureLifecycleEvents(events => {
        #if IOS
            events.AddiOS(iOS => iOS.FinishedLaunching((app, launchOptions) => {
                AXAiOSBindings_MAUI.CAMDOReporter.InitializeSDKWithOptions(AXAiOSBindings_MAUI.SDKOptions.SDKLogLevelVerbose, (_, __) => {LogEvent("SDK initialized successfully");
                });
                return true;
            }));
        #endif
    ``` 


### Usage

Use `AXAiOSBindings_MAUI.CAMDOReporter` to call custom APIs in your project.

For example:
```csharp
AXAiOSBindings_MAUI.CAMDOReporter.SetCustomerId("Test");
```

For more information, see https://techdocs.broadcom.com/us/en/ca-enterprise-software/it-operations-management/app-experience-analytics-saas/SaaS/configuring/collect-data-from-ios-applications/collect-data-from-supported-mobile-platforms.html#concept.dita_6c3ef640e7e0cc8549ce43c10731700185fbf76e_Net7MAUI
