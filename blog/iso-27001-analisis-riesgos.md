# Cómo realizar un análisis de riesgos para ISO 27001 paso a paso

**Categoría:** ISO 27001  
**Fecha:** Mayo 2026  
**Tiempo de lectura:** 12 min

## Introducción

El análisis de riesgos es uno de los pilares de un Sistema de Gestión de Seguridad de la Información (SGSI). Sin esta actividad, la organización termina aplicando controles por intuición, presión comercial o moda tecnológica, en lugar de responder a amenazas reales con criterios de negocio.

ISO 27001 no exige una plantilla única, pero sí requiere un método consistente, repetible y alineado con el contexto de la organización. En otras palabras: no basta con llenar una matriz; hay que demostrar que las decisiones de seguridad tienen fundamento.

## ¿Qué busca ISO 27001 en el análisis de riesgos?

La norma espera que la organización:

- Defina criterios para evaluar riesgos.
- Identifique activos, amenazas y vulnerabilidades.
- Estime impacto y probabilidad.
- Determine qué riesgos requieren tratamiento.
- Seleccione controles apropiados.
- Mantenga evidencia y revisión periódica.

El objetivo no es eliminar todos los riesgos, sino tratarlos de forma razonable según el apetito de riesgo y las prioridades del negocio.

## Paso 1: Definir el contexto

Antes de evaluar riesgos, conviene responder:

- ¿Qué procesos cubre el SGSI?
- ¿Qué sedes, sistemas, áreas o servicios están incluidos?
- ¿Qué requisitos legales, contractuales o regulatorios aplican?
- ¿Qué impacto tendría una caída, fuga o alteración de información?

Sin este contexto, la evaluación termina siendo genérica y poco útil.

## Paso 2: Identificar activos de información

No se trata solo de hardware. Un activo puede ser cualquier elemento que soporte la confidencialidad, integridad o disponibilidad de la información.

### Ejemplos de activos

- Bases de datos institucionales
- Credenciales administrativas
- Servidores virtuales
- Repositorios Git
- Documentos contractuales
- Servicios SaaS críticos
- Personal con conocimiento clave

Una buena práctica es agrupar activos por proceso o servicio para evitar inventarios imposibles de mantener.

## Paso 3: Identificar amenazas y vulnerabilidades

Una amenaza no es lo mismo que una vulnerabilidad:

- **Amenaza:** evento o actor que puede causar daño.
- **Vulnerabilidad:** debilidad que permite materializar ese daño.

### Ejemplos comunes

| Activo | Amenaza | Vulnerabilidad |
|---|---|---|
| Servidor web | Ransomware | Parches pendientes |
| Correo corporativo | Phishing | MFA no habilitado |
| Base de datos | Acceso no autorizado | Roles excesivos |
| Repositorio CI/CD | Manipulación de pipeline | Secretos expuestos |

## Paso 4: Estimar impacto y probabilidad

La mayoría de organizaciones usa una escala simple de 1 a 5 o de Bajo/Medio/Alto.

### Impacto

Evalúa consecuencias sobre:

- Operación del negocio
- Cumplimiento legal
- Reputación
- Pérdida financiera
- Interrupción del servicio

### Probabilidad

Considera:

- Historial de incidentes
- Exposición del activo
- Controles existentes
- Facilidad de explotación
- Capacidad del atacante o frecuencia del evento

## Paso 5: Calcular el nivel de riesgo

Un método simple es:

```text
Riesgo = Impacto x Probabilidad
```

### Ejemplo de escala

| Resultado | Nivel |
|---|---|
| 1-4 | Bajo |
| 5-9 | Medio |
| 10-15 | Alto |
| 16-25 | Crítico |

Lo importante no es la fórmula en sí, sino que el criterio sea coherente y aprobado por la organización.

## Paso 6: Determinar tratamiento del riesgo

Cada riesgo debe tener una decisión clara:

- **Mitigar** con controles
- **Aceptar** si está dentro del nivel tolerable
- **Transferir** mediante seguros, contratos o terceros
- **Evitar** cambiando el proceso o eliminando la actividad

Aquí se conecta directamente el análisis con el plan de tratamiento y la Declaración de Aplicabilidad (SoA).

## Paso 7: Vincular controles del Anexo A

Una vez priorizados los riesgos, se seleccionan controles apropiados. Por ejemplo:

- MFA y gestión de identidades para accesos críticos
- Hardening y gestión de vulnerabilidades para servidores
- Backups y pruebas de restauración para continuidad
- Monitoreo, logs y alertas para detección temprana
- Segregación de funciones en procesos sensibles

ISO 27001 no pide marcar controles “por llenar”, sino justificar por qué aplican o no aplican.

## Ejemplo práctico de matriz de riesgos

| Activo | Riesgo | Impacto | Probabilidad | Nivel | Tratamiento |
|---|---|---:|---:|---:|---|
| Correo corporativo | Robo de cuentas por phishing | 5 | 4 | 20 | MFA + capacitación + políticas de acceso |
| Servidor ERP | Caída por ransomware | 5 | 3 | 15 | EDR + backups + segmentación |
| Repositorio Git | Fuga de secretos | 4 | 4 | 16 | Secret scanning + vault + revisión de permisos |

## Errores frecuentes

### 1. Hacer una matriz demasiado teórica

Si nadie del negocio participa, el resultado suele ser un documento elegante pero inútil.

### 2. Valorar todos los riesgos como “altos”

Eso impide priorizar. Si todo es crítico, nada lo es realmente.

### 3. No revisar cambios del entorno

Nuevos proveedores, migraciones a nube, automatización o IA cambian el mapa de riesgos.

### 4. Separar el análisis de riesgos de la operación real

El SGSI debe conversar con TI, DevOps, RR. HH., jurídico y dirección.

## Recomendaciones para equipos técnicos

- Mantén una metodología simple y defendible.
- Usa talleres cortos por proceso en lugar de reuniones eternas.
- Conserva evidencia de criterios y responsables.
- Revisa riesgos al menos una vez al año o ante cambios relevantes.
- Integra hallazgos de auditorías, vulnerabilidades e incidentes reales.

## Conexión con DevOps, IA y seguridad moderna

Hoy el análisis de riesgos ya no puede limitarse a servidores on-premise. También debe cubrir:

- Pipelines CI/CD
- Infraestructura como código
- Dependencias de terceros
- Modelos de IA y exposición de datos sensibles
- Automatizaciones con privilegios elevados

Ese enfoque permite que ISO 27001 deje de verse como solo cumplimiento y se convierta en una herramienta útil de decisión.

## Conclusión

Un buen análisis de riesgos en ISO 27001 no es burocracia: es una forma de decidir dónde invertir, qué proteger primero y cómo justificar controles ante auditoría y dirección.

Si el método es claro, repetible y conectado con la realidad técnica del negocio, el SGSI gana credibilidad y valor operativo.
