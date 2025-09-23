# Flujo de trabajo con GitFlow y Azure DevOps

Desarrollo de funcionalidades y correcciones (feature/xxxxxx / bugfix/xxxxxx)
Creación de rama desde develop:
 
feature/xxxxxx para nuevas funcionalidades.
bugfix/xxxxxx para correcciones.
Desarrollo por parte del equipo.
 
Pull Request a develop:
 
Validaciones automáticas:
Nombre de rama.
Asociación con tarea.
Uso de plantilla de PR.
Calidad de código: SonarQube, linters, etc.
Revisión manual por el Team Lead (TL).
Merge a develop:
 
Ejecución de pipeline que compila versiones para:
dev
stg
prd
Distribución en Firebase App Distribution para pruebas por:
QA
QX
Product Owner
 
Gestión de versiones
Se utiliza un fichero variables.json que contiene:
 
Número de versión.
Grupos de distribución de Firebase.
En ramas de desarrollo (feature / bugfix):
 
La pipeline incrementa automáticamente el número de versión.
Se commitea el fichero actualizado.
En ramas de release:
 
El número de versión se obtiene directamente del fichero variables.json.
No se incrementa automáticamente.
Tras una release o hotfix:
 
Los cambios en main (incluido el número de versión) se sincronizan manualmente con develop.
Proceso de Release
Creación de rama release/x.y.z desde develop.
 
Pull Request hacia main.
 
Validaciones en la pipeline:
 
Verificación de integridad.
Comprobación del número de versión respecto al último tag en main.
Revisión y aprobación por el TL.
 
Una vez completada la PR:
 
Compilación final.
Creación de tag con el número de versión.
Distribución en:
TestFlight (iOS)
Google Play Beta (Android)
Creación de release en Jira para asociar tareas.
Sincronización de cambios y versión desde main a develop.
 
Proceso de Hotfix
Igual que el proceso de release, pero partiendo de main y aplicando correcciones urgentes.
Firmado de aplicaciones
Los certificados y claves se descargan desde Azure DevOps Library.
El firmado se realiza automáticamente en la pipeline para:
Android
iOS
Proceso de Rollback
Rollback manual desde Azure DevOps
Se lanza manualmente una pipeline con opción "Rollback".
 
Se indica el tag o número de versión a restaurar (ej. v1.2.3).
 
Acciones de la pipeline:
 
Checkout del commit/tag.
Actualización del número de versión en variables.json (ej. v1.2.4-rollback).
Compilación y firmado.
Distribución en:
TestFlight
Play Store Beta
Firebase
Creación de tag específico:
 
Ejemplo: v1.2.4-rollback-from-v1.2.3
Registro en Jira como versión de rollback.
Sincronización con develop.
