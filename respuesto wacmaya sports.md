Esta es una guía técnica detallada para inicializar tu ecosistema de agentes y el proyecto **Wacamaya Sports**. Utilizaremos una estructura lógica para que cada "habilidad" del agente tenga su lugar y el código Flutter sea funcional desde el inicio.

---

## 1. Estructura de la Habilidad Agente Global: `.agents`

Primero, creamos la estructura de directorios para tus agentes de automatización.

```text
.agents/
├── SKILL.md
├── scripts/       # Automatizaciones de scraping/deploy
├── ejemplos/      # Snippets de UI y lógica
└── resources/     # Activos de marca y JSON de prueba
```

### SKILL.md (Definición de Capacidades)
```markdown
# Global Agent Skill: Wacamaya Sports
Este agente coordina las habilidades de diseño, código y scraping.

## Sub-Skills
- **Diseño**: Generación de temas y layouts para deportes.
- **Código**: Implementación de lógica CRUD y Firebase en Dart/Flutter.
- **Scraping**: Extracción de precios de competencia para jerseyes.

## Entorno
- Framework: Flutter
- Backend: Firestore
```

---

## 2. Preparación del Entorno (Prerrequisitos)

Antes de codificar, debemos asegurar que el túnel entre tu terminal y Firebase esté activo.

### Verificación de Herramientas
Ejecuta esto en tu terminal de VS Code o Antigravity:
1. **Flutter**: `flutter --version` (Si no está, descarga el SDK de flutter.dev).
2. **Firebase CLI**: 
   * Instalación: `npm install -g firebase-tools`
   * Login: `firebase login`
   * FlutterFire Config: `dart pub global activate flutterfire_cli`

### Inicialización del Proyecto
```bash
# Crear proyecto
flutter create proyectowacamayasports
cd proyectowacamayasports

# Configurar Firebase (Sigue el asistente)
flutterfire configure
```

---

## 3. Configuración del Proyecto (`pubspec.yaml`)

Añade estas dependencias para habilitar Firestore y la navegación:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.x.x
  cloud_firestore: ^4.x.x
  cupertino_icons: ^1.0.2

# Asegúrate de ejecutar: flutter pub get
```

---

## 4. Desarrollo del Proyecto Flutter

### Estructura de Archivos `.dart`
```text
lib/
├── main.dart
├── models/
│   └── jersey_model.dart
├── screens/
│   ├── home_screen.dart
│   ├── jersey_list.dart
│   └── jersey_form.dart
└── services/
    └── firebase_service.dart
```

#### A. Modelo de Datos (`lib/models/jersey_model.dart`)
```dart
class Jersey {
  String id;
  String equipo;
  double precio;
  String talla;

  Jersey({required this.id, required this.equipo, required this.precio, required this.talla});

  Map<String, dynamic> toMap() => {
    "equipo": equipo,
    "precio": precio,
    "talla": talla,
  };
}
```

#### B. Servicio de Firestore (`lib/services/firebase_service.dart`)
```dart
import 'package:cloud_firestore/cloud_firestore.dart';

FirebaseFirestore db = FirebaseFirestore.instance;

Future<List> getJerseys() async {
  List jerseys = [];
  QuerySnapshot query = await db.collection('jerseys').get();
  for (var doc in query.docs) {
    jerseys.add(doc.data());
  }
  return jerseys;
}

Future<void> addJersey(String equipo, double precio, String talla) async {
  await db.collection('jerseys').add({"equipo": equipo, "precio": precio, "talla": talla});
}
```

#### C. Interfaz de Usuario Principal (`lib/screens/home_screen.dart`)
```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Wacamaya Sports 🦜")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () => Navigator.pushNamed(context, '/jerseys'),
              child: Text("Gestionar Jerseys"),
            ),
            // Botones para Shorts, Tenis (Próximamente)
          ],
        ),
      ),
    );
  }
}
```

#### D. Punto de Entrada (`lib/main.dart`)
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';
import 'screens/home_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
  runApp(WacamayaApp());
}

class WacamayaApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Wacamaya Sports',
      theme: ThemeData(primarySwatch: Colors.orange),
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        // Aquí se agregarían las rutas del CRUD
      },
    );
  }
}
```

---

## 5. Verificación de Funcionalidad

Para asegurar que todo funciona bajo el estándar de `.agents`:

1.  **Prueba de Conectividad**: Ejecuta `flutter run`. Si la pantalla naranja de Wacamaya Sports carga, el framework está OK.
2.  **Prueba de DB**: Abre tu consola Firebase -> Firestore -> Crea la colección `jerseys`.
3.  **Sincronización de Agente**: El archivo `scripts/check_env.sh` (opcional en tu carpeta de agentes) debería verificar que el `google-services.json` esté en la carpeta `android/app`.

> **Nota**: Para el IDE Antigravity, asegúrate de tener instalada la extensión de Dart/Flutter para el resaltado de sintaxis y el hot reload.

¿Deseas que proceda con el código detallado de la pantalla de edición (Update) y borrado (Delete) para completar el CRUD?
