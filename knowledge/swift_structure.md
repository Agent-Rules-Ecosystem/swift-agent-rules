# Estructura Canónica de Proyecto — Swift (iOS / Apple Native)

Organización estándar de directorios y módulos para proyectos iOS, macOS, watchOS o visionOS desarrollados de manera nativa con **SwiftUI** y **Swift Package Manager (SPM)**.

---

## 📱 1. Estructura Estándar App SwiftUI (Xcode / SPM)

```text
root/
├── App/                          # Punto de entrada de la app
│   ├── iOSApp.swift              # Struct con anotación @main (App Protocol)
│   ├── Assets.xcassets           # Catálogo de imágenes, colores e iconos
│   └── Info.plist                # Permisos del sistema y configuración de iOS
├── Sources/ (o App/Modules/)
│   ├── Core/                     # Utilidades generales, extensiones y diseño base
│   │   ├── Extensions/           # Extensiones de Swift (String, Date, View)
│   │   ├── DesignSystem/         # Componentes visuales reutilizables y paleta de colores
│   │   └── Network/              # Cliente HTTP (URLSession, async/await client)
│   ├── Data/                     # Capa de Datos (Data Sources, Repositories Impl, SwiftData)
│   │   ├── Local/                # SwiftData Models, ModelContainer, Keychain, UserDefaults
│   │   ├── Remote/               # DTOs de red, API Endpoints, WebSocket Clients
│   │   └── Repositories/         # Implementaciones del protocolo de repositorio
│   ├── Domain/                   # Capa de Dominio (Modelos de entidad, UseCases, Protocolos)
│   │   ├── Entities/             # Structs puras de modelo (Inmutables, Sendable)
│   │   ├── Interfaces/           # Protocolos de repositorios (Dependency Inversion)
│   │   └── UseCases/             # Lógica de negocio (UseCases de responsabilidad única)
│   └── UI/                       # Capa de Presentación (SwiftUI)
│       ├── Common/               # Modifiers, custom views y componentes UI compartidos
│       ├── Navigation/           # NavigationStack, Route Enums y Coordinators
│       └── Features/             # Módulos por pantalla (Views + ViewModels)
│           ├── Auth/
│           │   ├── LoginView.swift
│           │   └── LoginViewModel.swift
│           └── Home/
│               ├── HomeView.swift
│               └── HomeViewModel.swift
├── Package.swift                 # Definición de dependencias via SPM (si usa módulos independientes)
├── ProjectName.xcodeproj          # Configuración del proyecto Xcode y Targets
└── Tests/                        # Pruebas unitarias e integradas (XCTest / Swift Testing)
```

---

## ⚙️ Reglas de Organización para el Agente

1. **Protocol-Oriented Programming**: Definir protocolos (`protocol`) para repositorios y servicios antes de implementar las clases concretas.
2. **Value Types vs Reference Types**: Usar `struct` por defecto para modelos, DTOs y componentes UI de SwiftUI. Usar `class` solo para ViewModels (con `@Observable` o `@MainActor`).
3. **Manejo de Assets**: Utilizar la sintaxis nativa generada por Swift (ej. `Color.primaryBrand` o `Image(.logo)`) evitando strings de nombres de assets harcodeadas.
