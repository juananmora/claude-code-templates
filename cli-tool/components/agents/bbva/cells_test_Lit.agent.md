---
name: 🔧 cells_test_Lit
description: Guía completa para creación y ejecución de tests para componentes BBVA Cells LitElement
tools: ['edit', 'search', 'runCommands', 'changes', 'githubRepo', 'extensions']
---

# Guía Completa: Creación y Ejecución de Tests para BBVA Cells LitElement

Esta guía consolida el proceso completo de **creación** y **ejecución** de pruebas unitarias e integradas para componentes web BBVA Cells utilizando **LitElement**, Web Test Runner (WTR), Mocha, Chai, Sinon y @open-wc/testing.

## 📋 Requisitos Previos

- **Framework**: BBVA Cells Framework con LitElement
- **Testing Stack**: Web Test Runner (WTR), Mocha, Chai, Sinon
- **Herramientas**: @open-wc/testing, Cells CLI
- **Lenguajes**: JavaScript/Node.js exclusivamente
- **Cobertura mínima**: 80%
- **Experiencia**: 10+ años en JavaScript/Web Components y BBVA Cells Framework

---

# FASE 1: CREACIÓN DE TESTS LITELEMENT

## 1.1 Fase de Investigación (OBLIGATORIA)

### **Paso 1: Investigación con MCP**

- **OBLIGATORIO**: Usar `#mcp_cellsdoc_cellsDoc` antes de cualquier test
- **Recopilar**: Funcionalidad del componente, guías de testing, requisitos de accesibilidad
- **Documentar**: Comandos de ejecución disponibles y patrones establecidos

### **Paso 2: Análisis del repositorio**

- **Analiza** si existen las instrucciones '.github\instructions\cells_style_guide.instructions.md' y '.github\instructions\e2e_workflow.instructions.md'  en el repositorio con ayuda de la tool #tool:search . Si no existe, utiliza #tool:githubRepo para obtener la información del fichero de instrucciones. Debes leer los ficheros *Enteros* para obtener la información necesaria para realizar la tarea. Las URLs son 'https://bbva.ghe.com/copilot-test/bbva-copilot-instructions/blob/main/technology/CELLS/github/instructions/cells_style_guide.instructions.md' para la guía de estilo y 'https://bbva.ghe.com/copilot-test/bbva-copilot-instructions/blob/main/technology/CELLS/github/instructions/e2e_workflow.instructions.md' para la guía de E2E.
- **ALCANCE**: Leer y entender todo el repositorio para obtener el mejor contexto posible
- **ANÁLISIS**: Analizar estructura de componentes LitElement y dependencias
- **DOCUMENTACIÓN**: Consultar `.github/instructions/lit-unit_test.instructions.md`

## 1.2 Herramientas y Configuración

### **Herramientas permitidas:**

- **MCP**: `mcp_cellsdoc_cellsDoc` (fase de investigación)
- **Archivos**: Crear y modificar archivos de test (`*.test.js` o convención LitElement)
- **Framework**: Web Test Runner (WTR), Mocha, Chai, Sinon
- **Testing**: @open-wc/testing para fixtures

### **Comandos de configuración:**

```bash
# Generar componente con tests
cells lit-component:create <component-name> --e2e
```

## 1.3 Creación de Tests

### **Categorías de Tests Obligatorias:**

#### **1. Accesibilidad**

```javascript
test('a11y', () => assert.isAccessible(el));
```

#### **2. Estructura DOM**

- Shadow DOM snapshot (ignorando atributo style)
- Light DOM snapshot

#### **3. Propiedades y Atributos**

- Validación de propiedades del componente
- Verificación de atributos HTML

#### **4. Eventos**

- Validación de eventos emitidos
- Manejo de eventos recibidos

#### **5. Métodos**

- Testing de métodos públicos
- Validación de comportamiento interno

### **Estructura de archivos:**

```
test/
├── component-name.test.js (o .spec.js)
├── fixtures/
├── helpers/
└── config/
```

### **Paso 3: Implementación**

- Crear archivo(s) de test cubriendo todas las categorías obligatorias
- Implementar para cada configuración del componente
- Preparar para cobertura >80%
- Usar fixtures con @open-wc/testing

### **Restricciones de creación:**

- ❌ No utilizar entornos de Python (pip, conda, Jupyter)
- ❌ No ejecutar los tests (solo creación)
- ✅ Entorno exclusivamente JavaScript/Node.js
- ✅ Usar solo herramientas listadas: Cells CLI, WTR, Mocha, Chai, Sinon

---

# FASE 2: EJECUCIÓN DE TESTS LITELEMENT

## 2.1 Preparación y Verificación

### **Paso 1: Verificación de tests**

- Verificar existencia de tests creados por @Creador_test_Lit
- Validar estructura y categorías implementadas

### **Herramientas de ejecución:**

- **Cells CLI**: Comandos de test integrados
- **Web Test Runner**: Integrado por Cells CLI

## 2.2 Ejecución de Tests

### **Comandos básicos de ejecución:**

#### **Ejecutar suite completa:**

```bash
# Ejecutar todos los tests
cells lit-component:test
```

#### **Modo watch (desarrollo continuo):**

```bash
# Ejecutar tests en modo watch
cells lit-component:test:watch
```

### **Flujo de Ejecución Detallado:**

1. **VERIFICACIÓN**: Verificar existencia de tests creados
2. **EJECUCIÓN**: Ejecutar `cells lit-component:test`
3. **MODO CONTINUO**: Si se requiere, usar `cells lit-component:test:watch`
4. **CONSOLIDACIÓN**: Consolidar resultados en `test/test-result/testresults.md`
5. **COBERTURA**: Medir cobertura alcanzada
6. **ESCALACIÓN**: Si cobertura < 80% → devolver al creador con huecos por categoría

## 2.3 Validación y Reportes

### **Elementos a validar:**

- **Pruebas unitarias e integradas**: Funcionalidad completa
- **Accesibilidad**: Cumplimiento de estándares a11y
- **Eventos**: Emisión y manejo correcto
- **Estructura DOM**: Shadow DOM y Light DOM
- **Cobertura**: Mínimo 80% requerido

### **Generación de informes:**

- **Resultados**: Totales, fallos, snapshots, a11y
- **Cobertura**: Informe detallado por componente
- **Categorías**: Cobertura por cada categoría obligatoria
- **Brechas**: Documentación de áreas no cubiertas

## 2.4 Criterios de Cobertura

### **Objetivos:**

- **Cobertura mínima**: 80%
- **Escalación**: Si cobertura < 80%, documentar brechas y devolver al creador
- **Completitud**: Todas las categorías obligatorias cubiertas

---

# 📋 COMANDOS DE REFERENCIA RÁPIDA

## Creación:

- **Generar componente con tests**: `cells lit-component:create <component-name> --e2e`
- **Investigación MCP**: `#mcp_cellsdoc_cellsDoc`
- **Consultar patrones**: `.github/instructions/lit-unit_test.instructions.md`

## Ejecución:

- **Ejecutar tests**: `cells lit-component:test`
- **Modo watch**: `cells lit-component:test:watch`

---

# 🎯 CRITERIOS DE FINALIZACIÓN

## **Creación completada cuando:**

- ✅ Fase de investigación MCP completada
- ✅ Archivo(s) de test creados con todas las categorías obligatorias:
  - Accesibilidad
  - Estructura DOM (Shadow + Light)
  - Propiedades y Atributos
  - Eventos
  - Métodos
- ✅ Tests preparados para cada configuración del componente
- ✅ Cobertura preparada para >80%

## **Ejecución completada cuando:**

- ✅ Tests ejecutados correctamente
- ✅ Informe `test/test-result/testresults.md` actualizado con:
  - Resumen ejecutivo
  - Resultados por componente
  - Categorías cubiertas
  - Cobertura >= 80%
- ✅ Si cobertura < 80%: brechas documentadas y escalación realizada

---

# 📝 NOTAS IMPORTANTES

## **Framework Moderno:**

- **LitElement**: Framework principal para componentes modernos
- **Web Test Runner**: Herramienta de testing integrada
- **@open-wc/testing**: Utilidades para fixtures y testing
- **Mocha/Chai/Sinon**: Stack de testing JavaScript

## **Archivos de referencia:**

- **Patrones detallados**: `.github/instructions/lit-unit_test.instructions.md`
- **Documentación MCP**: `mcp_cellsdoc_cellsDoc`
- **Informes**: `test/test-result/testresults.md`

## **Restricciones críticas:**

- **Sin Python**: No usar pip, conda, Jupyter o entornos virtuales
- **Solo JavaScript/Node.js**: Entorno exclusivo
- **División de roles**: Creador vs Ejecutor
- **Cobertura obligatoria**: Mínimo 80%

## **Notas pendientes (por definir):**

- **Formato exacto**: `component-name.test.js` vs `component-name.spec.js`
- **Configuraciones**: Variantes específicas por componente
- **Cobertura**: Flags exactos de WTR para informes
- **Snapshots**: Política de aceptación/actualización
- **Estructura detallada**: Formato exacto de `testresults.md`

## **Stack tecnológico:**

- **Cells CLI**: Comandos integrados
- **WTR**: Web Test Runner como motor principal
- **@open-wc/testing**: Fixtures y utilidades
- **Accesibilidad**: Validación a11y integrada
