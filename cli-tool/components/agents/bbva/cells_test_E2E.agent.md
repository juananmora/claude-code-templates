---
name: 🔧 cells_test_E2E
description: Guía completa para creación y ejecución de tests E2E para aplicaciones BBVA Cells
tools: ['edit', 'runNotebooks', 'search', 'new', 'runCommands', 'runTasks', 'usages', 'vscodeAPI', 'problems', 'changes', 'testFailure', 'openSimpleBrowser', 'fetch', 'githubRepo', 'extensions', 'todos', 'runSubagent']
---

# Guía Completa: Creación y Ejecución de Tests E2E para BBVA Cells

Esta guía consolida el proceso completo de **creación** y **ejecución** de pruebas End-to-End (E2E) para aplicaciones BBVA Cells, utilizando WebDriverIO, Cells Pepino V2/V3, Cucumber/Gherkin y Shadow DOM testing.

**Obligatorio** Solo modificar o crar los ficheros referentes a los tests E2E, sin alterar el código fuente del proyecto. Por lo general se encuentran en la carpeta `test/e2e/`.

## 📋 Requisitos Previos

- **Framework**: BBVA Cells con Lit Components
- **Testing Stack**: WebDriverIO + Cells Pepino V2/V3
- **Lenguajes**: TypeScript para step definitions, Gherkin BDD en español
- **Especialización**: Shadow DOM testing y Web Components automation
- **Cobertura mínima**: 80%

---

## FASE 1: CREACIÓN DE TESTS E2E

## 1.1 Análisis y Comprensión del Repositorio

### **Paso 1: Análisis inicial**

1. **Analiza** si existen las instrucciones '.github\instructions\cells_style_guide.instructions.md' y '.github\instructions\e2e_workflow.instructions.md'  en el repositorio con ayuda de la tool #tool:search . Si no existe, utiliza #tool:githubRepo para obtener la información del fichero de instrucciones. Debes leer los ficheros *Enteros* para obtener la información necesaria para realizar la tarea. LAS URLs son 'https://bbva.ghe.com/copilot-test/bbva-copilot-instructions/blob/main/technology/CELLS/github/instructions/cells_style_guide.instructions.md' para la guía de estilo y 'https://bbva.ghe.com/copilot-test/bbva-copilot-instructions/blob/main/technology/CELLS/github/instructions/e2e_workflow.instructions.md' para la guía de E2E.
2. **ANÁLISIS**: Analizar requirements y estructura de Web Components
3. **ANÁLISIS ESTÁTICO OBLIGATORIO**: Determinar selectores específicos y guardar descripción en `selectors.md`
4. **DESARROLLO**: Preparar estructura para archivo de test en formato Gherkin BDD con step definitions TypeScript

### **Paso 2: Instalación de dependencias**

```bash
# Instalar dependencias base
npm ci && npm install @cells-pepino/cli

# Crear componente con tests E2E (opcional)
cells lit-component:create <component-name> --e2e
```

## 1.2 Creación de Tests

### **Paso 3: Generar archivos de test**

- Crear archivos de test E2E (`.feature`, `.steps.ts`)
- Generar tests para abarcar **mínimo 80% de cobertura**
- Usar nomenclatura en **kebab-case**
- Escribir Gherkin en **español** para stakeholders bancarios

### **Estructura de archivos requerida:**

```text
test/
├── e2e/
│   ├── src/
│   │   ├── pages/
│   │   │   └── *.page.ts (Page Objects)
│   │   ├── features/
│   │   │   └── *.feature (Gherkin en español)
│   │   ├── steps/
│   │   │   └── *.steps.ts (TypeScript step definitions)
│   │   └── config/
│   │       └── *.js (Configuración WebDriverIO)
│   ├── package.json
│   └── node_modules/
├── test-results/
│   └── testresults.md
│   └── selectors.md
```

### **Paso 4: Análisis de cobertura**

- Analizar cobertura de tests generados
- Mejorar cobertura si es necesario
- Generar informe visual de cobertura

### **Restricciones de creación:**

- ❌ No modificar código fuente del proyecto
- ✅ Usar exclusivamente TypeScript para step definitions
- ✅ Nombres de test en kebab-case

---

## FASE 2: EJECUCIÓN DE TESTS E2E

## 2.1 Preparación del Entorno

### ▶️ Fase 1: Instalación de dependencias

```bash
cd test/e2e && npm install
```

### ▶️ Fase 2: Levantamiento de Servidores

```bash
npm run start
```

#### Configuración de Selenium:

- Instalación de Selenium Standalone con ChromeDriver 140 (Instala la versión adecuada del driver para Chrome, en este caso la 140)
- Inicio del servidor Selenium en puerto 4444

#### Levantamiento de servidores:

- Servidor de aplicación: puerto 9090 (cells app:serve -c canonical.json -p 9090)
- Servidor demo: puerto 8001 (cd demo && npm run start)

#### Configuración del navegador:

- Modo headless habilitado
- Viewport: 1920x1080
- User-data-dir dinámico para evitar conflictos

### ▶️ Fase 3: Ejecución de Tests

Ejemplo de ejecucion de test:

```bash
GALATEA=false SERVE_DEMO=false npm run test -- -t @prompt-2-14
```

### **Comandos específicos del framework Cells:**

```bash
# Ejecutar pruebas e2e directamente
./node_modules/@cells-pepino/cli/bin/cli.js -c ./config/browser.js

# Ejecutar pruebas de accesibilidad directamente
./node_modules/@cells-pepino/cli/bin/cli.js -c ./config/browser.accessibility.js

# Ejecutar caso específico con tag expression
./node_modules/@cells-pepino/cli/bin/cli.js -c ./config/browser.js -t @tag-name
```

## 2.4 Flujo de Ejecución Obligatorio

### **Proceso completo paso a paso:**

1. **EJECUCIÓN**: Ejecutar tests con Cells Pepino
2. **DOCUMENTACIÓN**: Actualizar `test/test-results/testresults.md`
3. **VERIFICACIÓN SHADOW DOM**: Confirmar interacciones correctas
4. **PR OBLIGATORIO**: Actualizar PR con los resultados finales

---

# 📋 COMANDOS DE REFERENCIA RÁPIDA

## Creación:

- **Crear componente con E2E**: `cells lit-component:create my-component @bbva --e2e`
- **Instalar dependencias**: `npm ci && npm install @cells-pepino/cli`

## Ejecución:

- **Instalar dependencias E2E**: `npm i` (dentro de `test/e2e/`)
- **Servir aplicación**: `cells app:serve --sourcemaps -c canonical.json -b novulcanize -p 9090`
- **Servir demo**: `cd demo && npm run start`
- **Ejecutar todos los E2E**: `npm run test:browser:local`
- **Ejecutar accesibilidad**: `npm run test:a11y:local`
- **Test específico**: `./node_modules/@cells-pepino/cli/bin/cli.js -c ./config/browser.js -t @tag`

---

# Posibles Errores Encontrados y Soluciones Implementadas

## Error 1: ChromeDriver Incompatible con Chrome

**Problema**: ChromeDriver versión 140 no coincidía con Chrome 142

```bash
session not created: This version of ChromeDriver only supports Chrome version 140
Current browser version is 142.0.7444.59
```

**Solución**:

- Descarga manual de ChromeDriver 142 compatible
- Instalación en Selenium Standalone

## Error 2: Sesión de Chrome en Conflicto

**Problema**: Usuario data directory ya en uso

```bash
session not created: probably user data directory is already in use
```

**Solución** (browser.js líneas 20):

```javascript
`--user-data-dir=/tmp/chrome-user-data-${Date.now()}`
```

- User data dir dinámico con timestamp
- Previene conflictos entre ejecuciones

## Error 3: Puerto Incorrecto en Demo

**Problema**: Demo configurado en puerto 9090, servidor levantado en 9091

```bash
javascript error: Invalid or unexpected token
Context has not been changed
```

**Solución**:

- Reinicio del servidor en puerto correcto: 9090
- Sincronización con configuración demo (puerto 8001 → 9090)

## Error 4: Timing de Interacciones
**Problema**: Elementos no procesados antes de siguiente acción

**Solución**:

- Pausas estratégicas de 500ms-1000ms después de:

## Error 5: Selenium No Disponible

**Problema**: Tests fallaban al no encontrar Selenium Grid

```bash
Failed to connect to selenium. Attempts left: 115
connect ECONNREFUSED ::1:4444
```

**Solución**:

- Instalación de Selenium Standalone 4.10.0
- Configuración de ChromeDriver compatible
- Inicio del servidor en puerto 4444

## Error 6: Problemas con el controlador edge

**Problema**: EdgeDriver no encontrado o incompatible

```bash
$ cat /tmp/selenium.log
/home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/lib/check-paths-existence.js:8
      throw new Error('Missing ' + path);
            ^

Error: Missing /home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/.selenium/chromiumedgedriver/latest-linux/msedgedriver
    at /home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/lib/check-paths-existence.js:8:13
    at Array.forEach (<anonymous>)
    at checkPathsExistence (/home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/lib/check-paths-existence.js:6:14)
    at Object.start (/home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/lib/start.js:191:9)
    at async Object.start (/home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/bin/selenium-standalone:23:16)

Node.js v18.20.8
<exited with exit code 0>
```

**Solución**:

- Crear marcador de posición del controlador Edge

```bash
$ mkdir -p /home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/.selenium/chromiumedgedriver/latest-linux && \
touch /home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/.selenium/chromiumedgedriver/latest-linux/msedgedriver && \
chmod +x /home/runner/work/functional-test-poc-cells/functional-test-poc-cells/test/e2e/node_modules/selenium-standalone/.selenium/chromiumedgedriver/latest-linux/msedgedriver && \
echo "Edge driver placeholder created"
Edge driver placeholder created
<exited with exit code 0>
```

- Iniciar Selenium standalone nuevamente
- Ejecutar las pruebas nuevamente

---

# 🎯 CRITERIOS DE FINALIZACIÓN

## **Creación completada cuando:**

- ✅ Archivo(s) de test E2E creados con todas las categorías obligatorias
- ✅ Selectores documentados en `selectors.md`
- ✅ Estructura Gherkin BDD correcta en español
- ✅ Step definitions TypeScript con patrones Cells
- ✅ Cobertura mínima del 80%

## **Ejecución completada cuando:**

- ✅ Batería completa de tests ejecutada
- ✅ Informe generado en `test/test-result/e2e.md`
- ✅ Resultados consolidados en `test/test-results/testresults.md`
- ✅ Verificación Shadow DOM confirmada
- ✅ Pull Request con evidencia visual incluida

---

📝 NOTAS IMPORTANTES

## **Para Windows:**

- Los comandos pueden diferir debido a variables de entorno
- Las rutas usan barras inclinadas diferentes
- Verificar scripts en `package.json` y adaptarlos si es necesario

## **Herramientas:**

- **WebDriverIO** con Cells Pepino V2/V3
- **Generación de reportes** automática
- **Shadow DOM testing** especializado
