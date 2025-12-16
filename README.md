# COMIDILLA
trabajo
🍰 COMIDILLA – Recetario de Pasteles con Clima en Tiempo Real

Aplicación Android desarrollada en **Kotlin** con **Jetpack Compose**, que permite gestionar un recetario de pasteles (CRUD completo), almacenar la información de forma local con **Room** y mostrar la **temperatura actual** obtenida desde una **API externa (Open-Meteo)**.  
Además, integra **notificaciones locales** y **vibración** para mejorar la experiencia de usuario.

> Proyecto académico para la asignatura de Desarrollo de Aplicaciones Móviles (Evaluación de consumo de API, pruebas y generación de APK).

---

## 📲 Funcionalidades principales

- **Gestión de recetas (CRUD)**
  - Crear nuevas recetas con:
    - Nombre
    - Descripción
    - Imagen opcional desde la galería
  - Listar todas las recetas guardadas
  - Ver el detalle de una receta
  - Editar recetas existentes
  - Eliminar recetas

- **Persistencia local con Room**
  - Entidad `Receta` almacenada en base de datos local (`Room`)
  - DAO con operaciones:
    - `obtenerRecetas()`
    - `insertarReceta(receta)`
    - `actualizarReceta(receta)`
    - `eliminarReceta(receta)`

- **API externa de clima (Open-Meteo)**
  - Consumo de la API pública de Open-Meteo mediante **Retrofit**.
  - Muestra la **temperatura actual en Santiago** en la pantalla principal:
    - Archivo: `RecetaRepository.obtenerClima()`  
    - Uso en `RecetaViewModel.cargarClima()`  
    - Visualización en `ListaRecetasScreen` como texto descriptivo.

- **Interfaz moderna con Jetpack Compose + Material 3**
  - Pantalla principal: listado “Recetario de Pasteles”
  - Pantallas:
    - Lista de recetas
    - Detalle de receta
    - Agregar receta
    - Editar receta
  - Navegación con `NavHost` y rutas:
    - `"lista"`
    - `"detalle/{id}"`
    - `"agregar"`
    - `"editar/{id}"`

- **Notificaciones y vibración**
  - En ciertas acciones (como guardar o eliminar), se dispara:
    - Notificación local mediante `NotificationCompat`
    - Vibración usando `Vibrator` / `VibrationEffect`
  - Canal de notificaciones configurado en `MainApplication`.

---

## 🏗️ Arquitectura y tecnologías

- **Lenguaje:** Kotlin
- **UI:** Jetpack Compose + Material 3
- **Arquitectura:** MVVM + Repository
- **Persistencia:** Room
- **Consumo de API:** Retrofit + Converter Gson
- **Concurrencia:** Kotlin Coroutines (`viewModelScope`)
- **Carga de imágenes:** Coil (`coil-compose`)
- **Gestión de estado:** `MutableStateFlow` / `StateFlow`
- **Notificaciones:** NotificationCompat + NotificationChannel
- **Mínimo SDK:** 24  
- **Target / Compile SDK:** 36

---

## 🗂️ Estructura principal del proyecto

```text
nomeescucha/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── AndroidManifest.xml
│   │   │   ├── java/com/example/nomeescucha/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── MainApplication.kt
│   │   │   │   ├── data/
│   │   │   │   │   ├── Receta.kt
│   │   │   │   │   ├── RecetaDao.kt
│   │   │   │   │   ├── RecetaDataBase.kt
│   │   │   │   │   ├── RecetaRepository.kt
│   │   │   │   │   ├── RetrofitClient.kt
│   │   │   │   │   ├── WeatherApi.kt
│   │   │   │   │   └── WeatherResponse.kt
│   │   │   │   ├── ui/
│   │   │   │   │   ├── AppNavigation.kt
│   │   │   │   │   ├── RecetaViewModel.kt
│   │   │   │   │   ├── RecetaViewModelFactory.kt
│   │   │   │   │   └── theme/
│   │   │   │   │       ├── Colors.kt
│   │   │   │   │       ├── Theme.kt
│   │   │   │   │       └── Typography.kt
│   │   │   │   └── ui/ui/screens/
│   │   │   │       ├── ListaRecetasScreen.kt
│   │   │   │       ├── AgregarRecetaScreen.kt
│   │   │   │       ├── DetalleRecetaScreen.kt
│   │   │   │       └── EditarRecetaScreen.kt
│   │   └── test/
│   │       └── java/com/example/nomeescucha/
│   │           └── ExampleUnitTest.kt
│   ├── build.gradle.kts
├── build.gradle.kts
└── settings.gradle.kts
