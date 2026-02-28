Gemini dijo
Entorno de Practica de Control 3D interactivo con Blockly

Un simulador web "todo en uno" (All-in-One) diseñado para la enseñanza, el aprendizaje y la experimentación con sistemas de control automático. Permite programar leyes de control (como controladores PID) utilizando programación visual basada en bloques y observar los resultados en tiempo real sobre sistemas dinámicos renderizados en 3D.

CARACTERISTICAS PRINCIPALES

100% Client-Side: Todo el simulador corre directamente en el navegador web mediante un único archivo HTML. No requiere instalación, dependencias locales ni un servidor backend.

Programación Visual: Integración completa de Blockly de Google, permitiendo a los usuarios arrastrar y conectar bloques lógicos y matemáticos para generar el código de control en tiempo real.

Renderizado 3D en Tiempo Real: Visualización fluida de los sistemas físicos impulsada por Three.js.

Sistemas Físicos Integrados:

Péndulo invertido 1D: Clásico sistema cart-pole (simplificado sobre base fija).

Péndulo invertido 2D (esférico): Péndulo con dos grados de libertad angulares (x e y).

Balancín con bola: Sistema de equilibrio donde el control se ejerce sobre la inclinación del balancín para posicionar una masa rodante.

Bloques Personalizados de Control: Incluye bloques específicos de la materia como:

Lectura de variables de estado del sistema (actualización dinámica según el modelo).

Bloque de controlador PID con cálculo de error, integral y derivada adaptados al tiempo de simulación (dt).

Fijación de Setpoints y señales de control.

Interactividad y Perturbaciones: Permite aplicar fuerzas externas o impulsos a los modelos 3D haciendo clic y arrastrando directamente sobre el lienzo (canvas) para probar la robustez del controlador.

Parámetros Dinámicos: Panel de configuración en tiempo real para modificar variables del sistema (masa, gravedad, fricción, longitud, etc.).

Persistencia: El área de trabajo (workspace) de Blockly guarda su estado automáticamente al alternar entre diferentes modelos físicos.

COMO USAR EL SIMULADOR

Al ser una aplicación web estática, ponerla en marcha es sumamente sencillo:

Descarga o Clona este repositorio en tu equipo.

Haz doble clic en el archivo simulador3DControl.html para abrirlo en cualquier navegador web moderno (Chrome, Firefox, Edge, Safari).

Selecciona un sistema desde el menú desplegable en la barra de herramientas superior.

Arma tu lógica de control en el panel derecho usando los bloques de Matemáticas, Lógica, Control y PID.

Presiona "Iniciar simulación" y observa el comportamiento del sistema.

Ajusta los parámetros físicos en la barra inferior o aplica Perturbaciones para probar cómo reacciona tu diseño de control.

TECNOLOGIAS UTILIZADAS

HTML5, CSS3, JavaScript (ES6) - Estructura, estilo y lógica central.

Three.js (r128) - Motor de renderizado y graficación 3D.

Blockly - Librería principal para el entorno de programación visual y generación de código JavaScript.

ARQUITECTURA DEL CODIGO

El archivo principal simulador3DControl.html está estructurado en varias secciones integradas para facilitar su portabilidad:

Estilos (CSS): Grid layout responsivo que divide la pantalla entre la vista 3D y el entorno Blockly.

motor3d.js: Núcleo de la aplicación que administra el bucle de simulación (animación), enlaza la cámara y escena de Three.js, compila el código generado por Blockly, y administra el paso del tiempo (dt).

Modelos de Sistemas (Clases):

Pendulo1D: Lógica física y visual para el péndulo simple.

Pendulo2D: Ecuaciones diferenciales e integración para el péndulo esférico.

Balancin: Física de un balancín con fricción y una masa rodante.

bloquesPersonalizados.js: Definición visual y lógica de generación de código (Generator API) para los bloques diseñados específicamente para el control PID y lectura de estados.

Script de Inicialización: Configuración de la escena, inyección del toolbox de Blockly y asignación de eventos a la interfaz de usuario (UI).

COMO AGREGAR UN SISTEMA NUEVO

Si deseas expandir el simulador, el motor está preparado para ser escalable. Solo necesitas crear una nueva clase que extienda SistemaBase e implemente los siguientes métodos:

init(scene): Define aquí las geometrías y materiales de Three.js.

reset(initialState): Valores por defecto o iniciales de tus variables de estado.

update(dt, controlSignal): Ecuaciones diferenciales y método de integración del modelo físico.

getState(): Retorna un objeto con las variables de estado que leerá Blockly.

applyPerturbation(force): Define cómo afectan los clics o arrastres del usuario al sistema.

updateVisuals(): Traduce el estado físico a transformaciones de posición y rotación en Three.js.

getParamDefinitions(): Devuelve el arreglo de parámetros ajustables en la UI.

Luego, regístralo globalmente agregándolo al objeto window.Sistemas.
