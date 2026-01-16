# 🦉 Guía del Peregrino - San Sebastián Purranque 2026

App móvil desarrollada por **PurranQUE.INFO** para los peregrinos de la Fiesta de San Sebastián.

## 📱 Características

- ⏰ Contador regresivo al evento
- 📋 Cronograma completo del día con filtros
- 🎒 Checklist interactivo del peregrino (guardado local)
- 🗺️ Puntos de interés y servicios
- 🚨 Contactos de emergencia con llamada directa
- 🧮 Calculadora de viaje desde diferentes localidades
- 🦉 Integración con Búho Constantino

## 🛠️ Requisitos para Compilar

### Opción A: En tu computador local

1. **Instalar Flutter** (versión 3.0+)
   ```bash
   # Descarga desde https://flutter.dev/docs/get-started/install
   ```

2. **Clonar/Copiar el proyecto**

3. **Instalar dependencias**
   ```bash
   cd guia_peregrino
   flutter pub get
   ```

4. **Agregar imagen del Búho**
   - Coloca `buho.png` en `assets/images/`

5. **Compilar APK**
   ```bash
   flutter build apk --release
   ```
   El APK estará en: `build/app/outputs/flutter-apk/app-release.apk`

### Opción B: Usar Codemagic (sin instalar nada)

1. Sube el proyecto a GitHub
2. Ve a [codemagic.io](https://codemagic.io)
3. Conecta tu repositorio
4. Compila y descarga el APK

### Opción C: Usar GitHub Actions

Crea `.github/workflows/build.yml`:

```yaml
name: Build APK
on: push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.16.0'
      - run: flutter pub get
      - run: flutter build apk --release
      - uses: actions/upload-artifact@v3
        with:
          name: app-release
          path: build/app/outputs/flutter-apk/app-release.apk
```

## 📂 Estructura del Proyecto

```
guia_peregrino/
├── lib/
│   ├── main.dart              # Punto de entrada
│   ├── config/
│   │   └── theme.dart         # Tema visual
│   ├── models/
│   │   ├── evento.dart        # Modelo de evento
│   │   ├── checklist_item.dart
│   │   └── punto_interes.dart
│   ├── screens/
│   │   ├── home_screen.dart   # Pantalla principal
│   │   ├── horarios_screen.dart
│   │   ├── checklist_screen.dart
│   │   ├── servicios_screen.dart
│   │   └── info_screen.dart
│   ├── widgets/
│   │   ├── countdown_widget.dart
│   │   └── evento_card.dart
│   ├── services/
│   │   └── storage_service.dart
│   └── data/
│       └── app_data.dart      # Datos estáticos
├── assets/
│   └── images/
│       └── buho.png           # ¡Agregar esta imagen!
├── android/
│   └── app/
│       ├── build.gradle
│       └── src/main/
│           └── AndroidManifest.xml
└── pubspec.yaml
```

## ✏️ Personalización

### Modificar horarios y eventos
Edita `lib/data/app_data.dart`:

```dart
static final List<Evento> eventos = [
  Evento(
    id: '1',
    titulo: 'Misa de Aurora',
    hora: '06:00',
    // ... etc
  ),
];
```

### Agregar puntos de interés
En el mismo archivo, agrega a `puntosInteres`:

```dart
PuntoInteres(
  id: 'com1',
  nombre: 'Restaurant El Peregrino',
  categoria: 'comida',
  direccion: 'Calle Principal 123',
  telefono: '+56912345678',
  icono: '🍽️',
),
```

### Cambiar colores
Edita `lib/config/theme.dart`:

```dart
static const Color primaryColor = Color(0xFF8B0000); // Rojo San Sebastián
```

## 📲 Distribución del APK

Una vez compilado, puedes distribuir el APK de varias formas:

1. **WhatsApp**: Envía el archivo directamente
2. **Drive/Dropbox**: Comparte el enlace
3. **QR Code**: Genera un QR que apunte al enlace de descarga
4. **Tu sitio web**: Sube el APK a purranque.info

### Instalación en Android
Los usuarios deberán:
1. Permitir "Orígenes desconocidos" en Configuración
2. Abrir el APK
3. Instalar

## 🔮 Mejoras Futuras

- [ ] Notificaciones push antes de cada evento
- [ ] Mapa interactivo con Google Maps
- [ ] Modo offline completo
- [ ] Versión iOS
- [ ] Galería de fotos del evento

## 📄 Licencia

Desarrollado por PurranQUE.INFO como servicio público para la comunidad.

---

**¡Junto a San Sebastián, caminamos en la fe y la esperanza!** ✝️🦉
