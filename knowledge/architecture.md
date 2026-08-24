# Arquitectura Canónica — Swift (Clean Architecture + SwiftUI + MVVM/MVI)

Patrones arquitectónicos recomendados para aplicaciones Apple (iOS/macOS) usando **SwiftUI** y **Clean Architecture**.

---

## 🏛️ 1. Diagrama de Capas de la Arquitectura

```mermaid
graph TD
    subgraph Presentation Layer (SwiftUI UI)
        A[SwiftUI View] -->|Observa @Observable| B[@MainActor ViewModel]
        B -->|Emite UIState / Actions| A
    end

    subgraph Domain Layer (Business Logic)
        B -->|Ejecuta| C[UseCase / Interactor]
        C -->|Consulta protocolo| D[Repository Protocol]
    end

    subgraph Data Layer (Data Sources)
        E[Repository Implementation] .->|Implementa| D
        E -->|Local| F[SwiftData / Keychain / ModelContainer]
        E -->|Remote| G[URLSession HTTP / Async Client]
    end
```

---

## 📐 2. Responsabilidades por Capa

### A. Presentation Layer (Capa de Presentación SwiftUI)
* **SwiftUI Views**: Vistas declarativas puras. Responden visualmente a los cambios de estado expuestos por el ViewModel.
* **ViewModel**:
  ```swift
  @Observable
  @MainActor
  final class HomeViewModel {
      private(set) var state: HomeState = .idle
      private let fetchHomeDataUseCase: FetchHomeDataUseCaseProtocol

      init(fetchHomeDataUseCase: FetchHomeDataUseCaseProtocol) {
          self.fetchHomeDataUseCase = fetchHomeDataUseCase
      }

      func loadContent() async {
          state = .loading
          do {
              let data = try await fetchHomeDataUseCase.execute()
              state = .success(data)
          } catch {
              state = .error(error.localizedDescription)
          }
      }
  }
  ```

### B. Domain Layer (Capa de Dominio)
* **Entities**: Structs inmutables que representan los conceptos puros de negocio (ej. `User`, `Transaction`).
* **Repository Protocols**: Definen contratos abstractos de acceso a datos sin depender de frameworks externos.
* **UseCases**: Clases o Structs con un único método de ejecución (`execute() async throws -> Result`).

### C. Data Layer (Capa de Datos)
* **Repositories Impl**: Implementan la obtención de datos mezclando datos locales (SwiftData) y remotos (URLSession).
* **SwiftData Models**: Clases anotadas con `@Model` exclusivas de la capa de datos.
* **Network Client**: Implementación asíncrona mediante `URLSession.shared.data(for: request)` emitiendo DTOs decodificables (`Decodable`).
