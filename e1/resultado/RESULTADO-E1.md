# E1 — comunicación del resultado (nivel mínimo, punto 2.a del compromiso)

Comunicación exigida por `e1/compromiso/COMPROMISO-COMUNICAR-E1.md` (sha256
`1c488a26418cdf2bfa4181f3c8cd68e6f1cb8be80cd3fb85ea40a8dc34154306`), con el nivel fijado antes de ejecutar en
`e1/NIVEL-PUBLICACION-E1.md`: **solo el mínimo del punto 2.a**. Por eso aquí no hay ninguna cifra agregada
(estimaciones ni intervalos) de ninguna métrica, sea cual sea su signo. Lo no publicado queda comprometido por la
huella del informe (abajo) y se publicará tal cual si la consulta sobre datos de terceros lo permite.

## Estado final

- **E1 terminó (`FINISHED`)** y su informe se descifró y se verificó contra la huella sellada (`PUBLISHED`, publicación
  local). No se abortó.
- Consumida (`CONSUMED`) el 2026-10-30 a las 10:51 UTC; terminada a las 10:59 UTC (hora de escritura de los
  registros de consumo en el equipo de EDGE; no es una marca de tiempo externa). Una sola ejecución.

## Q2a — v0 frente a la referencia `HOME_AWAY_FREQ`

Categoría de veredicto para cada mercado del informe y para los dos horizontes prerregistrados. Criterio
prerregistrado (el de F9) sobre la diferencia emparejada de log loss v0 − referencia, con intervalo al 97,5 %
(Bonferroni ×2, remuestreo por jornada, 2.000 réplicas, semilla 20260930).

| Mercado | `T-1440m` | `T-2m` |
|---|---|---|
| 1X2 | `MEJORA_CLARA` | `MEJORA_CLARA` |
| Ambos marcan | `SENAL_POSITIVA_NO_CONCLUYENTE` | `SENAL_POSITIVA_NO_CONCLUYENTE` |
| Más de 2,5 goles | `SENAL_POSITIVA_NO_CONCLUYENTE` | `SENAL_POSITIVA_NO_CONCLUYENTE` |

## Q1 — calibración de v0

Por suceso y horizonte: si la pendiente y la ordenada de calibración y sus intervalos fueron estimables, y los
remuestreos válidos y separados frente al mínimo de 1.900. Q1 no tiene veredicto de aprobado o suspenso.

| Suceso | Horizonte | Estimación | Intervalo | Motivo | Válidos / mínimo | Separados |
|---|---|---|---|---|---|---|
| Local | `T-1440m` y `T-2m` | ESTIMADO | ESTIMADO | — | 2.000 / 1.900 | 0 |
| Empate | `T-1440m` y `T-2m` | ESTIMADO | ESTIMADO | — | 2.000 / 1.900 | 0 |
| Visitante | `T-1440m` y `T-2m` | ESTIMADO | ESTIMADO | — | 2.000 / 1.900 | 0 |
| Ambos marcan | `T-1440m` y `T-2m` | ESTIMADO | ESTIMADO | — | 2.000 / 1.900 | 0 |
| Más de 2,5 goles | `T-1440m` y `T-2m` | ESTIMADO | ESTIMADO | — | 2.000 / 1.900 | 0 |

## Partidos

- **Evaluados: 380.** Excluidos: **0** (el libro tenía 380 partidos y se evaluaron los 380; ningún motivo de exclusión
  aplicado).

## Huellas

| Qué | Valor |
|---|---|
| Commit del código (desarmado, el de la hoja) | `765aa9a0e3234a91e92341eebc1d979bab4f0226` |
| Commit armado que se ejecutó (solo cambia la línea de armado) | `1b00e3cc394f91ea7e566cced1a141ae8fdf02f9` |
| Hoja de sellado | `b5ce1120dab1a3a790c18e6e4e5e6715c87c8a93486d83a94521aa64a4921f38` |
| Informe (en claro) | `285eaccb7f07df42c78187a154b2afcca78425815f11dd67583e021808c32f4a` |
| Identificador de la ejecución | `e23b25065bc74a2abfc2a828c3f90a25` |

## Cómo leer este resultado

- **La referencia es estática.** `HOME_AWAY_FREQ` es la de F8 en modo STATIC: se ajusta una vez con las temporadas
  anteriores y no aprende durante la temporada evaluada; v0 se reajusta en cada momento con los resultados ya
  disponibles. Parte de la diferencia puede deberse solo a esa actualización y no a la arquitectura del modelo.
- **E1 no compara con el mercado.** Nada de este resultado demuestra que v0 sea mejor, ni igual, que las
  probabilidades de las casas de apuestas.
- **Una sola temporada** de una sola competición. Los dos horizontes dan resultados casi iguales: v0 no usa
  información de última hora, así que no son dos pruebas independientes.
- **Nada de E1 cambia v0.** No se cambian métricas, horizontes ni categorías después de ver el resultado.

## Límites de cómo se ejecutó (variante M)

E1 se ejecutó en el ordenador de EDGE con protecciones técnicas (motor en un proceso separado que solo recibe lo
disponible en cada momento; cada predicción registrada y sellada antes de pedir ningún resultado; registros de
consumo en dos discos; informe cifrado y sellado por su huella antes de leerlo). **No es una auditoría
independiente ni una prueba absoluta de ejecución única.** No protege frente a un operador o administrador del
equipo que quiera hacer trampa, ni frente a software malicioso u otras cuentas del equipo; la prueba de que hubo una
sola ejecución son registros locales y sus copias. Cubre los errores del código y del operador, no la mala fe.
