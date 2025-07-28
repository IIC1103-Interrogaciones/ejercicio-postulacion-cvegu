# Ejercicio de Postulación - Área de Interrogaciones

Nombre: **Cristián Vega**

Email: **cvegu@estudiante.uc.cl**

Telegram: **@cvegul**

## Código solución (NO MODIFICAR)

```python
#code.py
def obtener_proximos(partidos, equipo):
    equipos = []
    ex_rivales = []
    for partido in partidos:
        if partido[0] not in equipos:
            equipos.append(partido[0])
        if partido[1] not in equipos:
            equipos.append(partido[1])
        if equipo == partido[0]:
            ex_rivales.append(partido[1])
        if equipo == partido[1]:
            ex_rivales.append(partido[0])
    pendientes = []
    for rival in equipos:
        if rival not in ex_rivales:
            pendientes.append(rival)
    return pendientes
```

## Runner Personalizado (Opcional Modificar)

```python
from functools import partial

def obtener_proximos_modificada(func_original, partidos, equipo):
    # Resultado de la función original
    resultado = func_original(partidos, equipo)

    # Participantes (para validar presencia del equipo)
    participantes = {e for a, b in partidos for e in (a, b)}
    if equipo not in participantes:
        return []

    # Excluirse a sí mismo y ordenar alfabéticamente
    resultado_filtrado = sorted(x for x in resultado if x != equipo)
    return resultado_filtrado

# Reescribe el nombre expuesto
obtener_proximos = partial(obtener_proximos_modificada, obtener_proximos)

```

## Enunciado

# Pregunta: DCChampions

Arranca la DCChapmpions! El calendario está patas arriba y nadie tiene claro quién debe enfrentarse aún. Tu desafío es poner orden con código, a partir del registro de partidos ya jugados, identifica para cualquier equipo la lista de rivales que todavía le quedan por disputar. Trabajarás con abreviaciones de clubes y un formato todos‑contra‑todos a una vuelta. Demuestra tus habilidades escribiendo funciones claras y fiables que devuelvan exactamente lo que hace falta para cuadrar las fechas.

## Objetivo
Implementa la función `obtener_proximos(partidos, equipo)` que, a partir de una lista de partidos ya jugados (cada partido es `["ABC", "DEF"]`) y el nombre abreviado de un club, retorne **la lista de rivales que a ese club aún le faltan por enfrentar** en un todos‑contra‑todos a una vuelta.

- El conjunto de participantes se define como **todos** los nombres que aparecen en `partidos`.
- La salida debe estar **ordenada alfabéticamente**.
- Si `equipo` **no participa** (no aparece en `partidos`), retorna `[]`.
- No hay partidos repetidos ni auto‑enfrentamientos; los nombres distinguen mayúsculas/minúsculas (*case‑sensitive*).

## Ejemplo

### Input
```python
partidos = [
    ["RMA", "MCI"],
    ["PSG", "BVB"],
    ["BVB", "RMA"],
    ["MCI", "PSG"],
]
print(obtener_proximos(partidos, "RMA"))
```

### Output
```python
["PSG"]
```

### Explicación
En el input hay cuatro equipos (`RMA`, `MCI`, `PSG`, `BVB`). `RMA` ya se enfrentó a `MCI` y a `BVB`, por lo que su único rival pendiente es `PSG`. El *output* es una lista **ordenada** con los rivales pendientes del equipo consultado.

---

# Testcases propuestos (para ejecutar en celdas separadas)

**Testcase 1 — equipo ya jugó con todos**  
**Input**
```python
partidos = [
    ["RMA", "MCI"],
    ["RMA", "PSG"],
    ["MCI", "PSG"],
]
print(obtener_proximos(partidos, "RMA"))
```
**Output**
```python
[]
```

**Testcase 2 — equipo no participa (no aparece en `partidos`)**  
**Input**
```python
partidos = [
    ["RMA", "MCI"],
    ["PSG", "BVB"],
]
print(obtener_proximos(partidos, "BAR"))
```
**Output**
```python
[]
```

**Testcase 3 — varios rivales pendientes (orden alfabético)**  
**Input**
```python
partidos = [
    ["RMA", "PSG"],
    ["BVB", "INT"],
]
print(obtener_proximos(partidos, "RMA"))
```
**Output**
```python
["BVB", "INT"]
```
