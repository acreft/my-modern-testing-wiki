# 🧾 Introducción

El Mobile Testing es el proceso de verificar y validar la calidad de aplicaciones que se ejecutan en dispositivos móviles, considerando sus particularidades técnicas y de uso.
A diferencia de las pruebas en entornos tradicionales (desktop o web), el ecosistema móvil añade complejidad debido a:

- La fragmentación de hardware y software: diferentes fabricantes, versiones de sistema operativo (Android, iOS, forks), tamaños de pantalla, resoluciones, procesadores.

- El entorno dinámico: redes móviles inestables (3G, 4G, 5G, WiFi), movilidad del usuario, cambios de ubicación, interrupciones (llamadas, notificaciones, pérdida de señal).

- Las limitaciones físicas: batería, memoria RAM, capacidad de almacenamiento, sensores (GPS, acelerómetro, giroscopio, biometría).

- La interacción natural: la experiencia de usuario depende de gestos táctiles, multitouch, voz, huellas, rotación, vibraciones.

En resumen, el Mobile Testing busca garantizar que una aplicación móvil funcione correctamente, sea usable, segura y confiable, independientemente del dispositivo o contexto de uso.

# Tipos de prueba móviles

## Pruebas funcionales

- Validan que la app cumpla con los requisitos definidos.

- Incluyen flujos críticos (login, compra, notificaciones push, permisos).

## Pruebas de compatibilidad

Se enfocan en garantizar el correcto funcionamiento en distintas combinaciones de:

- Sistemas operativos (Android/iOS y sus versiones).

- Dispositivos (gama baja, media, alta).

- Factores de forma (smartphones, tablets, plegables, wearables).

## Pruebas de usabilidad y UX

- Evalúan la facilidad de uso, accesibilidad y consistencia con las guías de diseño (Google Material Design, Human Interface Guidelines de Apple).

- Consideran aspectos como legibilidad, navegación intuitiva, uso de colores y tamaños de botones.

## Pruebas de rendimiento

- Carga: cómo responde la app ante múltiples usuarios simultáneos.

- Uso de recursos: consumo de CPU, RAM, batería, datos móviles.

- Latencia de red: comportamiento en diferentes condiciones (3G, 4G, WiFi).

## Pruebas de seguridad

- Revisan almacenamiento seguro de credenciales y datos sensibles.

- Validan que las comunicaciones estén cifradas (HTTPS/TLS).

- Detectan riesgos comunes del OWASP Mobile Top 10 (ejemplo: fuga de datos, uso indebido de permisos, API inseguras).

## Pruebas de instalación y actualización

- Se asegura que la aplicación pueda instalarse, actualizarse, y desinstalarse sin errores.

- Incluye escenarios como pérdida de conexión durante la descarga o migración de datos en actualizaciones.

# Enfoques de prueba

## Dispositivos reales:

- Ventaja → reflejan el comportamiento más cercano a la realidad.

- Desventaja → alto costo en mantenimiento y cobertura limitada de modelos.

## Emuladores y simuladores:

- Útiles en etapas iniciales de desarrollo.

- Ventaja → económicos y rápidos de configurar.

- Desventaja → no simulan con precisión sensores, rendimiento de red o consumo de batería.

## Device Farms (granjas de dispositivos en la nube):

- Ejecución de pruebas en una amplia gama de dispositivos reales de manera remota y escalable.

- Ejemplos → AWS Device Farm, BrowserStack, Sauce Labs.

# Herramientas comunes

## Automatización funcional

- Appium: framework open source, multiplataforma, compatible con Android/iOS.

- Espresso: framework oficial de Google para Android.

- XCUITest: framework oficial de Apple para iOS.

## Device Farms (testing en la nube)

- AWS Device Farm.

- BrowserStack App Automate.

- Sauce Labs Real Device Cloud.

## Pruebas de rendimiento y monitoreo

- Android Profiler (Android Studio).

- Instruments (Xcode, iOS).

- JMeter / Locust (para backend y APIs móviles).

## Pruebas de seguridad

- OWASP Mobile Testing Guide.

- MobSF (Mobile Security Framework).

# Estándares y buenas prácticas

- ISTQB® Mobile Application Testing Foundation Level:
  Define conceptos clave, técnicas, tipos de prueba y riesgos específicos en entornos móviles.

- OWASP Mobile Security Testing Guide (MSTG):
  Referencia mundial para pruebas de seguridad en aplicaciones móviles.

- ISO/IEC/IEEE 29119:
  Serie de normas internacionales para pruebas de software, aplicables también al ámbito móvil.

- Guías de diseño oficiales: Material Design (Google). Human Interface Guidelines (Apple).
