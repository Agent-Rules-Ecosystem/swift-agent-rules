# Checklist de Release y Despliegue — Swift (iOS / App Store Connect)

Pasos obligatorios para la preparación, auditoría de seguridad y despliegue de builds de producción en **TestFlight** y la **App Store**.

---

## 📋 1. Checklist Pre-Build (Xcode & Codigo)

- [ ] **Linter Check**: Ejecutar `swiftlint` en Xcode / Terminal y resolver todas las advertencias y errores estricto.
- [ ] **Pruebas Unitarias**: Ejecutar suite de pruebas con `xcodebuild test` o en Xcode (`Cmd + U`).
- [ ] **Versionado de App**:
  * Incrementar `Bundle Version` (Build Number, ej. `42`).
  * Actualizar `Bundle Version Short` (Version Name, ej. `1.3.0`).
- [ ] **Configuración de Target**: Confirmar que el `Bundle Identifier` y los `Signing & Capabilities` correspondan al App ID de producción.

---

## 🔐 2. Certificados y Provisioning Profiles

- [ ] **Distribution Certificate**: Verificar que el certificado de distribución de Apple Developer esté vigente.
- [ ] **Provisioning Profile**: Asegurar que el perfil de distribución App Store contenga todas las Entitlements activas (Push Notifications, Sign in with Apple, Associated Domains, In-App Purchases).

---

## 📦 3. Compilación y Archivado (Xcode Archive)

1. Seleccionar el esquema de producción y el destino **Any iOS Device (arm64)**.
2. Ejecutar **Product -> Archive** en Xcode (o via CLI con `xcodebuild -scheme App -archivePath build/App.xcarchive archive`).
3. Ejecutar la validación del archivo en el **Organizer** de Xcode antes de la distribución.
4. Subir a **App Store Connect** / **TestFlight**.

---

## 🚀 4. Despliegue y Post-Lanzamiento

- [ ] Configurar notas de la versión (What's New) en App Store Connect.
- [ ] Distribuir primero la build a evaluadores internos/externos vía **TestFlight**.
- [ ] Revisar logs de crashes mediante Xcode Organizer / Firebase Crashlytics post-lanzamiento.
