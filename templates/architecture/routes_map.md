# 🧭 Mapa Global de Rutas y Puntos de Entrada

> Pertenece a: `overview/architecture/routes_map.md`  
> Referenciado desde: [`overview/architecture.md`](../architecture.md)

## 1. Diagrama Sintético de Enrutamiento

```mermaid
graph TD
    ROOT["RootView / AppEntry"] --> AUTH["AuthFlow (NavigationStack)"]
    ROOT --> MAIN["MainTabView"]
    MAIN --> DETAIL["FeatureDetailView (Route)"]
```

## 2. Definición de Rutas Registradas

| Ruta | Vista / Route | Guard / Parámetros |
|---|---|---|
| `/` | Root / Entry | Inicialización |
| `/main` | Principal | Auth / Session Guard |
