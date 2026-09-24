# Sistema de Detección de Vehículos con OpenCV

## Descripción del Proyecto
Este proyecto implementa un sistema de visión por computadora para la detección y conteo de vehículos en vídeos de tráfico. Utilizando técnicas de procesamiento de imágenes con la librería **OpenCV**, el sistema es capaz de analizar el flujo vehicular, diferenciar carriles y llevar un conteo preciso superando los desafíos comunes de iluminación y oclusión.

## El Problema Inicial
En las primeras fases del desarrollo, se utilizó un método básico de sustracción de fondo y detección de contornos simples. Sin embargo, este enfoque presentó problemas significativos en escenarios reales:
* **Confusión por sombras:** Las sombras proyectadas generaban falsos positivos y aumentaban el tamaño aparente de los vehículos.
* **Agrupación de objetos:** Cuando dos vehículos circulaban muy próximos, el algoritmo los fusionaba e identificaba como un único objeto.

## Solución Implementada
Para lograr resultados de alta precisión, se desarrolló una solución mejorada basada en el algoritmo `BackgroundSubtractorMOG2`. Las mejoras clave incluyen:
* **Eliminación de sombras:** El algoritmo distingue entre objetos reales y sombras, reduciendo drásticamente los falsos positivos.
* **Regiones de Interés (ROI):** Se delimitaron coordenadas específicas para cada carril de tráfico, garantizando que solo se contabilicen los objetos dentro de estas zonas.
* **Filtros morfológicos:** Se aplican operaciones de apertura y cierre sobre la imagen binarizada para limpiar el ruido.
* **Sistema de "Cooldown":** Contadores independientes por carril que evitan el doble conteo de vehículos que se mantienen dentro de la misma ROI.

## Flujo de Trabajo
El sistema procesa el vídeo siguiendo esta secuencia lógica:
1. **Lectura del video:** Procesamiento del archivo de video cuadro por cuadro.
2. **Sustracción de fondo:** Aplicación de `BackgroundSubtractorMOG2` con detección de sombras activada.
3. **Preprocesamiento:** Uso de operaciones morfológicas para eliminar el ruido de la máscara generada.
4. **Definición de ROIs:** Configuración de dimensiones personalizadas según la ubicación de cada carril.
5. **Conteo por carril:** Identificación de contornos dentro de las ROIs usando la lógica de "cooldown".
6. **Visualización:** Proyección de los contadores en tiempo real y dibujo de los rectángulos (ROIs) sobre el vídeo original.

## Conclusión
La implementación de algoritmos avanzados de procesamiento de imágenes ha permitido superar las limitaciones de los métodos básicos de sustracción. El resultado es un sistema robusto, con un conteo exacto por carril (incluso en tráfico denso) y una alta fiabilidad, abriendo la puerta a futuras aplicaciones prácticas en el análisis de tráfico y ciudades inteligentes.
