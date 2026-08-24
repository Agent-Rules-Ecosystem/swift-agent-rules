# Arquitectura del proyecto

Reemplazar con arquitectura real del proyecto al bootstrap.

```mermaid
graph LR
    UI[SwiftUI Views] --> State[ViewModel / @Observable]
    State --> Service[API / Backend]
    Service --> Model[Models / Entities]
```

| Capa | Implementación real |
|---|---|
| Presentation | |
| Domain | |
| Data | |
