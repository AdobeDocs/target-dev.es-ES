---
source-git-commit: 5c66ee5c8dd5fe60eaeed10fdb9bb6dcee000c89
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---
# Cuándo usar la toma de decisiones en el dispositivo y cuándo la toma de decisiones en el perímetro

## Tenga en cuenta los casos de uso al decidir si utilizar la toma de decisiones en el dispositivo

![imagen alt](assets/comparison.jpeg)

La principal diferencia entre *en el dispositivo* la toma de decisiones y la toma de decisiones perimetrales consiste en que la toma de decisiones en el dispositivo ejecuta las decisiones localmente en los servidores, mientras que las decisiones perimetrales se toman en la red Edge de Adobe Target. La toma de decisiones en el dispositivo debe utilizarse para cualquier actividad A/B o XT que deba entregarse en páginas con mucho tráfico, donde el rendimiento afecta en gran medida a los KPI de la empresa, como la conversión, los ingresos y la retención. Por ejemplo, supongamos que su equipo de marketing está ejecutando campañas de publicidad para atraer clientes potenciales a su página de inicio. La ejecución de campañas publicitarias en redes de editores requiere un pago, por lo tanto, cualquier cliente potencial que aterrice en su página de inicio se traduce en una cantidad en dólares. Al mismo tiempo, supongamos que está ejecutando experimentos A/B para ver qué imagen a pantalla completa capta mejor la atención del consumidor. Si la entrega de estos experimentos A/B tarda 2 segundos adicionales, existe una alta probabilidad de que el consumidor se impaciente y se recupere. ¡Ahí van sus dólares de marketing y experimentos A/B! Es difícil perder este prospecto ganado con tanto esfuerzo, ya que ahora se pierde cualquier oportunidad de convertir este cliente potencial en un cliente leal o repetido. Por lo tanto, ejecutar una actividad de toma de decisiones en el dispositivo para este caso de uso puede evitar cualquier impacto negativo que la latencia pueda introducir.

Por otro lado, la toma de decisiones perimetral requiere una llamada de bloqueo de red para recuperar una experiencia, pero puede ser muy beneficiosa, ya que los datos en tiempo real y el lenguaje XML se pueden utilizar para que la experiencia del usuario final sea altamente atractiva. Una llamada de bloqueo de red introducirá una latencia adicional al ofrecer la experiencia; sin embargo, en algunos casos, este equilibrio puede tener sentido. Por ejemplo, imaginemos un caso en el que un cliente esté explorando el catálogo de productos y suponga que va a una página de detalles del producto. Si esa página muestra una lista recomendada de productos, junto con el producto que el cliente está viendo en ese momento, esto puede aumentar la participación y, posteriormente, la conversión y los ingresos. Aunque mostrar la lista recomendada de productos de esta manera requeriría una decisión de Edge influenciada por el algoritmo ML de Adobe Target (lo que significa que habría latencia agregada), esa latencia agregada no sería lo suficientemente significativa para que el usuario final se devuelva. Además, una lista recomendada de productos significa una tasa de conversión más alta. Por lo tanto, en este caso, una decisión de Edge le proporciona a su empresa el mayor valor.

## Funciones compatibles

Además de evaluar los casos de uso y los objetivos empresariales, revise qué funciones incluye la toma de decisiones en el dispositivo [admite](../on-device-decisioning/supported-features.md) antes de decidir si utilizar la toma de decisiones en el dispositivo en lugar de la toma de decisiones en el perímetro. Actualmente, Edge Decisioning admite todos los tipos de actividades, segmentación de audiencias y métodos de asignación.