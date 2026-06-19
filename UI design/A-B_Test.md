# Skill: UI Exploration Architect

> Diseña hipótesis, no pantallas. El objetivo no es producir interfaces; es reducir incertidumbre antes de comprometer recursos de diseño y desarrollo.

---

## Objetivo

Generar entre **3 y 5 variantes radicalmente diferentes** para una misma experiencia, permitiendo comparar enfoques de arquitectura, jerarquía, interacción y modelo mental antes de converger en una solución final.

La exploración debe ocurrir dentro del contexto real de la aplicación siempre que sea posible.

---

## Cuándo usar esta skill

| Sí | No |
|-----|-----|
| Explorar layouts | Resolver lógica de negocio |
| Comparar arquitecturas de información | Diseñar estados complejos |
| Evaluar jerarquías visuales | Modelar datos |
| Diseñar nuevas experiencias | Definir APIs |
| Rediseñar pantallas existentes | Resolver arquitectura técnica |

### Pregunta clave

```text
¿Estamos discutiendo cómo debería verse?

→ Usa esta skill.

¿Estamos discutiendo cómo debería funcionar?

→ Usa una skill de arquitectura o lógica.
```

---

# Principio Fundamental

Las variantes deben representar hipótesis diferentes.

No estilos diferentes.

❌ Incorrecto

| Variante A | Variante B | Variante C |
|------------|------------|------------|
| Cards grandes | Cards medianas | Cards pequeñas |

✅ Correcto

| Variante | Hipótesis |
|-----------|-----------|
| A | El usuario necesita visibilidad completa |
| B | El usuario necesita foco progresivo |
| C | El usuario necesita acceso rápido a acciones |

Si dos variantes pueden resolverse modificando únicamente CSS, no son variantes.

---

# Fase 1 · Comprensión del Problema

Antes de diseñar, construir un modelo del problema.

## Definir

| Elemento | Pregunta |
|-----------|-----------|
| Objetivo de negocio | ¿Qué resultado busca la empresa? |
| Objetivo del usuario | ¿Qué intenta lograr el usuario? |
| Frecuencia | ¿Cuántas veces se realiza la tarea? |
| Complejidad | ¿Qué nivel de expertise requiere? |
| Contexto | ¿Desktop, Mobile, SaaS, Backoffice? |

### Ejemplo

| Variable | Valor |
|-----------|---------|
| Negocio | Incrementar activación |
| Usuario | Configurar su cuenta rápidamente |
| Frecuencia | Baja |
| Complejidad | Moderada |
| Contexto | SaaS B2B Desktop |

---

# Fase 2 · Restricciones

Toda interfaz existe dentro de límites.

## Capturar restricciones

| Tipo | Ejemplos |
|--------|---------|
| Negocio | KPIs, monetización, compliance |
| Técnicas | Framework, backend, performance |
| Visuales | Design System, branding |
| Cognitivas | Nivel técnico, tiempo disponible |

---

# Fase 3 · Modelos Mentales

Identificar qué patrón espera encontrar el usuario.

| Categoría | Referencias |
|------------|-------------|
| Exploración | Netflix, Spotify, Pinterest |
| Gestión | Jira, Linear, Asana |
| Configuración | Stripe, GitHub, AWS |
| Monitoreo | Grafana, Datadog |
| E-commerce | Amazon, Mercado Libre |
| CRM | HubSpot, Salesforce |

### Regla

Cada variante debe apoyarse en un modelo mental diferente.

---

# Fase 4 · Direcciones Estratégicas

Generar entre 3 y 5 direcciones.

Para cada una documentar:

```yaml
Nombre:
Hipótesis:
Ventajas:
Riesgos:
Usuario beneficiado:
Complejidad de implementación:
```

### Ejemplo

```yaml
Nombre:
Command Center

Hipótesis:
Los usuarios toman mejores decisiones cuando
toda la información está visible simultáneamente.

Ventajas:
- Máxima visibilidad
- Menos navegación

Riesgos:
- Mayor carga cognitiva

Usuario:
Operadores avanzados

Complejidad:
Alta
```

---

# Fase 5 · Construcción de Variantes

Cada variante debe responder explícitamente:

| Dimensión | Pregunta |
|------------|-----------|
| Arquitectura | ¿Cómo se organiza la información? |
| Jerarquía | ¿Qué domina la pantalla? |
| Navegación | ¿Cómo se mueve el usuario? |
| Layout | ¿Cómo se distribuye el espacio? |
| Acciones | ¿Qué comportamiento promueve? |

### Diseñar siempre

```text
Loading
Empty
Error
Success
Responsive
```

No diseñar únicamente el estado ideal.

---

# Fase 6 · Integración

## Prioridad 1

Utilizar una pantalla existente.

```text
/settings?variant=A
/settings?variant=B
/settings?variant=C
```

## Prioridad 2

Crear ruta temporal.

```text
/prototype/settings-redesign
```

### Regla

Antes de crear una ruta nueva preguntarse:

> ¿Existe una pantalla actual donde este experimento pueda vivir?

Si la respuesta es sí, usar la pantalla existente.

---

# Fase 7 · Selector de Variantes

Implementar un switcher compartido.

### Características obligatorias

| Requisito | Descripción |
|------------|------------|
| URL Driven | Usa `?variant=` |
| Persistente | Sobrevive refresh |
| Compartible | Deep linking |
| Navegación | Mouse + teclado |
| Reutilizable | Componente único |
| Seguro | Oculto en producción |

### Ejemplo

```tsx
const variant = searchParams.get("variant") ?? "A";

switch (variant) {
  case "A":
    return <VariantA />;
  case "B":
    return <VariantB />;
  case "C":
    return <VariantC />;
}
```

# Fase 8 · Convergencia

Nunca preguntar:

```text
¿Cuál te gusta más?
```

Preguntar:

```text
¿Qué elementos resuelven mejor el problema?
```

## Matriz de Convergencia

| Elemento | Variante Ganadora |
|-----------|-----------|
| Header | A |
| Navegación | C |
| Filtros | B |
| Resumen | A |
| Acciones | C |

### Objetivo

La solución final puede ser una combinación.

No es obligatorio elegir una única variante.

---

# Fase 9 · Consolidación

## Documentar

```yaml
Decisión:
Justificación:
Tradeoffs:
Riesgos:
Aprendizajes:
```

## Limpiar

### Si la variante vive en una pantalla existente

- Eliminar variantes descartadas
- Eliminar switcher
- Integrar la solución final

### Si la variante vive en una ruta temporal

- Promover la ganadora
- Eliminar prototipo
- Eliminar switcher
- Eliminar código experimental

---

# Anti-patrones

| Anti-patrón | Problema |
|------------|-----------|
| Variantes cosméticas | No exploran soluciones |
| Diseñar desde gustos | Decisiones subjetivas |
| Compartir layouts entre variantes | Reduce exploración |
| Ignorar estados | Interfaces frágiles |
| Conectar a producción | Riesgo innecesario |
| Saltar hipótesis | Exploración sin dirección |

---

# Entregables Esperados

```yaml
✓ 3-5 variantes estructuralmente diferentes
✓ Hipótesis explícitas
✓ Selector navegable
✓ Evaluación heurística
✓ Evaluación de accesibilidad
✓ Matriz de convergencia
✓ Recomendación fundamentada
✓ Plan de implementación
```