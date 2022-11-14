# RUM Quick Start Setup

## Overview 
The following document aims to provide a quick start guide on how to use Chrome DevTools + Datadog RUM to collect RUM telemetry data without updating the main src code. 

(**Please note**: the following instructions are scoped to only the current Chrome session). 
## Creating the RUM Application
1. Navigate to [Datadog RUM Application/create](https://app.datadoghq.com/rum/application/create)
2. Follow the steps to create the RUM application.
   - _More information can be found [here](https://docs.datadoghq.com/real_user_monitoring/#get-started)_.  

## Injecting Datadog RUM SDK 
1. Open Chrome 
2. Right-click on the page and go to "Inspect"
3. Navigate to the "Source" tab within Chrome DevTools 
4. Click-on "Snippets"
5. Create on "New snippet"
6. Copy & Paste the output from Creating the RUM Application into the new snippet. 
7. Right-click the snippet and click, "Run". 

![Chrome DevTools/Sources/Snippets](https://p-qkfgo2.t2.n0.cdn.getcloudapp.com/items/P8uNZjYg/33ab97a0-9e57-4fb6-9946-97a88383955c.jpg?v=934953b58a4bb3537d976e6ea93dd822 "Chrome DevTools/Sources/Snippets")

## Visualize the RUM Telemetry 
View the telemetry within the [Datadog OOTB RUM dashboards](https://app.datadoghq.com/dashboard/lists/preset/3?q=RUM).