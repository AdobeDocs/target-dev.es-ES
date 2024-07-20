---
title: Instalar .NET SDK
description: Obtenga información sobre cómo instalar el SDK de  [!DNL Adobe Target] .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---

# Instalar .NET SDK

[NuGet](https://www.nuget.org/packages/Adobe.Target.Client) ha distribuido .NET SDK. Para empezar, agréguela como una dependencia mediante la instalación mediante `Package Manage` o `.NET CLI`:

## Administrador de paquetes

>[!BEGINTABS]

>[!TAB Administrador de paquetes]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

El código de código abierto se encuentra en [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
