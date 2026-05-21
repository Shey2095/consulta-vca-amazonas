# 📑 Sistema de Consulta de Afiliación - Amazonas

Este es un portal web ligero, seguro e independiente diseñado para que el equipo de salud consulte el estado de afiliación de los usuarios en tiempo real. El sistema cruza los datos de una hoja de cálculo en Google Sheets mediante una API sin exponer la base de datos completa.

---

## 🚨 ADVERTENCIA DE CONFIDENCIALIDAD Y ESTADO ACTUAL
> ⚠️ **IMPORTANTE:** Actualmente (Mayo de 2026), la base de datos y el motor de Google Apps Script se encuentran ligados y alojados en el correo electrónico de **Sheila (Coordinadora saliente)**. 
> 
> Al momento del empalme, este archivo **DEBE ser transferido en su totalidad al nuevo coordinador del componente** siguiendo el protocolo de transferencia descrito al final de este documento. Una vez confirmada la transferencia, la coordinadora saliente eliminará el archivo de su cuenta por protección de datos.

---

## 🏗️ Arquitectura del Sistema
El sistema está dividido en tres componentes conectados:
1. **La Base de Datos:** Un archivo de Google Sheets que contiene el listado maestro de afiliados.
2. **El Cerebro (API):** Un script en Google Apps Script (`Código.gs`) vinculado al Sheets que procesa las búsquedas de forma segura.
3. **La Pantalla (Interfaz):** Una página web estática alojada en **GitHub Pages** (`index.html`) que el equipo abre en sus celulares o computadoras para digitar las cédulas.

---

## 🔄 Protocolo de Mantenimiento y Actualización (Nutrir la Base)

Para garantizar la confiabilidad de la información, el coordinador del componente debe seguir estrictamente estas reglas de mantenimiento:

### ⏱️ 1. Frecuencia de Actualización
* **Plazo Máximo:** Se deben solicitar bases de datos actualizadas a las EPS (Nueva EPS, Sanitas, Mallamas, etc.) **como máximo cada tres (3) meses**. No se permite que el sistema opere con datos más antiguos para evitar glosas o errores de atención.

### 🧼 2. Depuración Obligatoria antes de Cargar
Antes de pegar los datos nuevos en el Google Sheets, es **obligatorio** realizar el siguiente proceso en el archivo local:
1. Juntar los reportes de las EPS en un solo listado.
2. **Eliminar registros duplicados:** Utilizar la herramienta de Excel/Sheets para eliminar filas repetidas basándose en el número de documento. Si hay duplicados, el buscador de la página web puede arrojar datos erróneos o ralentizarse.

### 🗺️ 3. Regla de Oro: Respetar las Columnas
El código del servidor lee las columnas en un orden numérico estricto de izquierda a derecha. **SI MUEVES UNA COLUMNA DE LUGAR, EL BUSCADOR SE ROMPERÁ POR COMPLETO.** 

Asegúrate de que los datos coincidan exactamente con este mapa de columnas:
* **Columna A (Index 0):** Tipo de documento (CC, TI, RC, etc.)
* **Columna B (Index 1):** Número de documento / Identificación (**Llave de búsqueda**)
* **Columna C (Index 2):** Primer Nombre
* **Columna D (Index 3):** Segundo Nombre
* **Columna E (Index 4):** Primer Apellido
* **Columna F (Index 5):** Segundo Apellido *(Las columnas C, D, E y F son procesadas automáticamente por el sistema para generar las iniciales por confidencialidad).*
* **Columna H (Index 7):** Sexo
* **Columna U (Index 20):** EPS
* **Columna V (Index 21):** Régimen

### ✍️ 4. Actualizar las Alertas en la Página Web
Para informarle al equipo de salud qué datos están consultando, cada vez que actualices el Sheets debes cambiar los textos informativos en la web:
1. Abre este repositorio de GitHub y edita el archivo `index.html`.
2. Busca la línea `<!-- ZONA DE ACTUALIZACIÓN -->` (Línea 39 aprox.).
3. Modifica la fecha en el texto `Última actualización de bases: ...` y las EPS incluidas en la línea de abajo.
4. Haz clic en el botón verde **Commit changes** (Guardar). La web pública se actualizará sola en 2 minutos.

---

## 🚚 Protocolo de Transferencia de Propiedad (Para el Nuevo Coordinador)

Cuando ocurra el cambio de coordinación, sigan este proceso paso a paso para no romper el servicio de los 20 compañeros que usan la app a diario:

1. **Compartir desde la cuenta vieja:** El dueño actual abre el Google Sheets, hace clic en **Compartir**, agrega el correo del nuevo coordinador como **Editor** y envía.
2. **Transferir Dueño:** En la misma ventana de compartir, despliega el menú al lado del nombre del nuevo coordinador, selecciona **"Transferir propiedad"** y envía la invitación. El nuevo coordinador debe abrir su correo y **aceptar** la propiedad.
3. **Re-generar el enlace (Clave):** El nuevo coordinador (ahora dueño) debe entrar al Sheets, ir a *Extensiones > Apps Script*, hacer clic en **Implementar > Nueva implementación**. Configurar como *Aplicación web*, ejecutar como *El usuario que accede (Dueño)* y en acceso seleccionar **"Cualquiera" (Anyone)**. Al implementar, Google le dará una **NUEVA URL** terminada en `/exec`.
4. **Vincular en GitHub:** El nuevo coordinador debe venir a este archivo `index.html` en GitHub, buscar la línea `const URL_DE_TU_APPS_SCRIPT = "..."` (Línea 60 aprox.) y reemplazar el enlace viejo por su enlace nuevo. Darle a **Commit changes**.
5. **Borrado Seguro:** Una vez verificado que el buscador web funciona con el nuevo enlace, la coordinadora saliente podrá mover el archivo de su Google Drive personal a la papelera y vaciarla de forma definitiva.

---
*Desarrollado y blindado para la optimización de procesos del componente de salud del departamento del Amazonas.*
