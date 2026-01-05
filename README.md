# Test-design-Urban-Routes
Proyecto 2

Diseño de estrategia de testing (mapa mental, clases de equivalencia, diagrama de flujo y casos de prueba) para validar el formulario de licencia de conducir y el cálculo de viajes en Urban Routes.

# Análisis de pruebas en Urban Routes

##Introducción
El presente documento detalla el análisis completo de pruebas realizadas para la aplicación Urban Routes, un servicio de transporte compartido. El análisis se basa en la información contenida en el archivo, que consta de tres secciones principales de pruebas:

<a href="https://docs.google.com/spreadsheets/d/1khC2NjhiB4kw-fScCL3qCT4WNGzDS6KF/edit?usp=sharing&ouid=106582061342206139422&rtpof=true&sd=true" target="_blank">
 📊​ Archivo original 
</a>

1. **Validación de Campos de Entrada**
   - Análisis de clases de equivalencia para campos de nombre y apellido
   - Verificación de límites y restricciones de caracteres
   - Validación de formatos y caracteres especiales

2. **Validación de Distancias y Horarios**
   - Evaluación de cálculos de distancia entre puntos
   - Verificación de franjas horarias y velocidades asociadas
   - Análisis de casos límite en cambios de horario

3. **Cálculos de Tiempo y Costos**
   - Pruebas de cálculo de tarifas según horario
   - Verificación de tiempos de viaje
   - Validación de casos especiales y límites

## Alcance del Análisis

El análisis abarcó:

- 24 casos de validación de campos de entrada
- 7 franjas horarias con diferentes velocidades
- 6 casos de prueba de cálculo de tarifas
- Múltiples escenarios de distancia y tiempo

## Metodología

Se empleó un enfoque sistemático que incluyó:

1. **Clases de Equivalencia**:
   - Identificación de rangos válidos e inválidos
   - Análisis de casos límite
   - Documentación de casos especiales

2. **Pruebas de Integración**:
   - Validación de cálculos de distancia
   - Verificación de velocidades por horario
   - Comprobación de costos y tiempos

3. **Verificación de Resultados**:
   - Documentación de resultados esperados vs obtenidos
   - Identificación de discrepancias
   - Análisis de casos fallidos

## Aspectos Clave Evaluados

1. **Campos de Usuario**:
   - Longitud de nombres (2-14 caracteres)
   - Manejo de caracteres especiales
   - Validación de idiomas y alfabetos

2. **Cálculos de Servicio**:
   - Precisión en cálculos de distancia
   - Exactitud en tiempos de viaje
   - Consistencia en tarifas

3. **Reglas de Negocio**:
   - Velocidades según franja horaria
   - Restricciones de servicio
   - Manejo de casos especiales

Este análisis proporciona una base sólida para la evaluación de la calidad y funcionamiento de Urban Routes, identificando tanto fortalezas como áreas de mejora en el sistema.

# Clases de Equivalencia - Validación de Campos

## Nombre

| Clase de Equivalencia | Límites | Datos de Prueba | Datos en Límites | Notas |
|----------------------|----------|-----------------|------------------|--------|
| Nombre válido | 2-14 caracteres | Alejandro | A (1), Al (2), Alejandro Sau (13), Alejandro Saúl (14) | Prueba límites mínimos y máximos |
| Nombre con espacio | 2-14 caracteres | Alejandro Saúl | Alejandro Saúl | Validación con espacio |
| Nombre corto | 1 carácter | A | A | Por debajo del límite mínimo |
| Nombre largo | >14 caracteres | Alejandro Saúlo | Alejandro Saúlo | Excede límite máximo |
| Nombre con números | - | Alejandro19 | - | Validación numérica |
| Caracteres especiales | - | Alejandro$ | - | Símbolos no permitidos |
| Campo vacío | No data | - | - | Campo requerido |
| Otro idioma | 2-14 caracteres | لا يوجد سوى إله واحد | لا يوجد سوى إله واحد | Caracteres cirílicos |

## Apellido

| Clase de Equivalencia | Límites | Datos de Prueba | Datos en Límites | Notas |
|----------------------|----------|-----------------|------------------|--------|
| Apellido válido | 2-16 caracteres | Vázquez | V (1), Va (2), Vázquez Guerrer (15), Vázquez Guerrero (16) | Prueba límites mínimos y máximos |
| Apellido con espacio | 2-16 caracteres | Vázquez Guerrero | - | Validación con espacio |
| Apellido corto | 1 carácter | A | A | Por debajo del límite mínimo |
| Apellido largo | >16 caracteres | Vázquez Guerreroo | Vázquez Guerreroo | Excede límite máximo |
| Apellido con números | - | Guerrero17 | - | Validación numérica |
| Caracteres especiales | - | Guerrer%o% | - | Símbolos no permitidos |
| Campo vacío | No data | - | - | Campo requerido |
| Otro idioma | 2-16 caracteres | لا يوجد سوى إله واحد | لا يوجد سوى إله واحد | Caracteres cirílicos |

## Notas Adicionales:
- Los límites son inclusivos (2-14/16 caracteres significa mínimo 2 y máximo 14/16)
- Se consideran casos especiales para caracteres no latinos y símbolos
- Se prueban específicamente los casos límite en los extremos del rango válido

# Clases de Equivalencia - Parte 2: Distancia y Horarios

## Distancia entre Direcciones

| Clase de Equivalencia | Datos de Prueba | Observaciones |
|----------------------|-----------------|---------------|
| distancia > 0 | "Desde" East 2nd Street, 601 "Hasta" 1717 E 7th St | Distancias válidas entre dos puntos diferentes |
| distancia = 0 | "Desde" East 2nd Street, 601 "Hasta" East 2nd Street, 601 | Mismo punto de origen y destino |

## Hora de Salida y Velocidades

| Horario | Velocidad | Límites | Datos de Prueba | Valores Límite | Notas de Verificación |
|---------|-----------|----------|-----------------|----------------|---------------------|
| 00:01-08:00 | 45 km/h | 00:01-08:00 | 00:00 - 08:01 | 00:00, 00:01, 00:02, 07:59, 08:00, 08:01 | Verificar con 08:01-12:00 (30 km/h) y 22:01-00:00 (45 km/h) |
| 08:01-12:00 | 30 km/h | 08:01-12:00 | 08:00 - 12:01 | 08:00, 08:01, 08:02, 11:59, 12:00, 12:01 | Verificar con 00:01-08:00 (45 km/h) y 12:01-18:00 (40 km/h) |
| 12:01-18:00 | 40 km/h | 12:01-18:00 | 12:00 - 18:01 | 12:00, 12:01, 12:02, 17:59, 18:00, 18:01 | Verificar con 08:01-12:00 (30 km/h), 22:01-00:00 (45 km/h) y 18:01-22:00 (25 km/h) |
| 18:01-22:00 | 25 km/h | 18:01-22:00 | 18:00 - 22:01 | 18:00, 18:01, 18:02, 21:59, 22:00, 22:01 | - |
| 22:01-00:00 | 45 km/h | 22:01-00:00 | 22:00 - 00:01 | 22:00, 22:01, 22:02, 23:59, 00:00, 00:01 | - |

## Notas Importantes:

1. **Velocidades por Franja Horaria**:
   - Madrugada (00:01-08:00): 45 km/h
   - Mañana (08:01-12:00): 30 km/h
   - Tarde (12:01-18:00): 40 km/h
   - Tarde-Noche (18:01-22:00): 25 km/h
   - Noche (22:01-00:00): 45 km/h

2. **Consideraciones de Prueba**:
   - Cada franja horaria debe probarse en sus límites
   - Las transiciones entre franjas son puntos críticos
   - Se deben verificar las velocidades en los cambios de horario

3. **Validaciones Especiales**:
   - Cambios de velocidad en los límites de las franjas horarias
   - Comportamiento en el cambio de día (00:00)
   - Consistencia en las velocidades asignadas
  

   - Tarde-Noche (18:01-22:00): 25 km/h
   - Noche (22:01-00:00): 45 km/h

2. **Consideraciones de Prueba**:
   - Cada franja horaria debe probarse en sus límites
   - Las transiciones entre franjas son puntos críticos
   - Se deben verificar las velocidades en los cambios de horario

3. **Validaciones Especiales**:
   - Cambios de velocidad en los límites de las franjas horarias
   - Comportamiento en el cambio de día (00:00)
   - Consistencia en las velocidades asignadas

# Casos de Prueba - Cálculo de Tiempo y Costo de Viaje

## Resumen de Ejecución
- Total de casos ejecutados: 6
- Casos aprobados: 5
- Casos no aprobados: 1
- Porcentaje de éxito: 83.33%

## Detalles de los Casos de Prueba

| ID | Horario | Estado | Distancia (km) | Velocidad (km/h) | Tiempo (min) | Costo | Resultado |
|----|---------|--------|----------------|------------------|--------------|--------|-----------|
| p-1 | 18:01-22:00 | Aprobado | 0.89 | 25 | 1.2 | 0.12 | Cálculo correcto |
| p-2 | 22:01-00:00 | Aprobado | 0.89 | 45 | 1.8 | 0.18 | Cálculo correcto |
| p-3 | 00:01-08:00 | Aprobado | 0.89 | 45 | 1.3 | 0.13 | Cálculo correcto |
| p-4 | 08:01-12:00 | Aprobado | 0.89 | 30 | 2.1 | 0.21 | Cálculo correcto |
| p-5 | 12:01-18:00 | Aprobado | 0.89 | 40 | 1.2 | 0.12 | Cálculo correcto |
| p-6 | 22:01-00:00 | No Aprobado | 0.0 | 45 | 0.00 | 0.000 | Mismo origen y destino |

## Análisis de Rutas Probadas

| Caso | Origen | Destino |
|------|---------|----------|
| p-1-5 | East 2nd Street, 601 | 1717 E 7th St |
| p-6 | East 2nd Street, 601 | East 2nd Street, 601 |

## Observaciones y Hallazgos

1. **Cálculos Correctos**:
   - Los tiempos de viaje se calculan correctamente según la velocidad de cada franja horaria
   - Los costos son proporcionales a la distancia y tiempo de viaje
   - Las tarifas se ajustan según el horario

2. **Caso Fallido (p-6)**:
   - El sistema no maneja adecuadamente el caso de mismo origen y destino
   - Se esperaba un mensaje de error o validación
   - Se requiere implementar validación para distancia = 0

3. **Patrones de Velocidad**:
   - Madrugada (00:01-08:00): 45 km/h
   - Mañana (08:01-12:00): 30 km/h
   - Tarde (12:01-18:00): 40 km/h
   - Noche (18:01-22:00): 25 km/h
   - Noche tardía (22:01-00:00): 45 km/h
