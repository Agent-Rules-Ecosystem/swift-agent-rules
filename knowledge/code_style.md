# Guía de Estilo y Buenas Prácticas — Swift

Reglas de formateo, principios de seguridad y comprobación estática mediante **SwiftLint** para proyectos Swift y SwiftUI.

---

## 🎨 1. Convenciones de Nomenclatura y Estilo Swift

### Nomenclatura
* **Tipos (Structs, Classes, Enums, Protocols)**: `PascalCase` (`UserViewModel`, `LoginView`, `RepositoryProtocol`).
* **Variables, Métodos y Propiedades**: `camelCase` (`userId`, `fetchUserData()`).
* **Casos de Enum**: `camelCase` (`enum ScreenState { case loading, success(User), error(Error) }`).

### Idiomas y Modismos de Swift
1. **Unwrapping Seguro de Opcionales**:
   * Preferir `guard let` o `if let` sobre el operador de desempaquetado forzado `!`.
   * El uso de `!` está estrictamente prohibido salvo en `@IBOutlet` inicializados por storyboard/nib o tests de integración aislados.
2. **Protocolos e Inmunidad a Mutación**:
   * Preferir `struct` sobre `class` para garantizar la semántica de copia (Value Semantics) y seguridad entre hilos.
   * Conformar tipos concurrentes al protocolo `Sendable` (y usar `@Sendable` en closures/funciones concurrentes).
3. **Macro `@Observable` (iOS 17+)**:
   * En ViewModels modernos, usar la macro `@Observable` en lugar de la clase legada `ObservableObject` con `@Published`.

---

## ⚡ 2. Estilo en SwiftUI

1. **Vistas Ligeras y Modulares**:
   * Las vistas SwiftUI deben ser pequeñas y especializadas. Si el cuerpo de `body` supera las 50 líneas, extraer sub-vistas privadas o componer vistas independientes.
2. **Propiedades de Estado**:
   * Usar `@State` únicamente para el estado local y privado de la UI interna del `View`.
   * Usar `@Binding` para compartir estado mutable bidireccional con una vista padre.
   * Usar `@Environment` para inyectar objetos globales o valores del entorno.

---

## 🧪 3. Concurrencia Estructurada (Structured Concurrency)

* Usar `async/await` en lugar de closures de completación (`(Result<T, Error>) -> Void`).
* Marcar ViewModels y componentes de interfaz con la anotación `@MainActor` para garantizar que las actualizaciones de UI ocurran en el hilo principal.
* Usar `actor` (tipo nominal de referencia aislado) para estado mutable compartido entre múltiples hilos de ejecución.

---

## 🛠️ 4. Formateo y Linters

* Usar **SwiftLint** (`swiftlint`) y **swift-format** / **SwiftFormat** (`swift-format` / `swiftformat`) para reglas de estilo y formateo consistente.
