---
title: Instalar .NET SDK
description: Obtenga información sobre cómo instalar el [!DNL Adobe Target] SDK DE .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Instalar .NET SDK

.NET SDK se distribuye por [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Para empezar, añádala como dependencia instalando mediante `Package Manage` o `.NET CLI`:

## Administrador de paquetes

>[!BEGINTABS]

>[!TAB Administrador de paquetes]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB CLI DE .NET]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

El código de código abierto se encuentra en [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
