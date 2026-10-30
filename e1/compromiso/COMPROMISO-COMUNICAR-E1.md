# Compromiso metodológico: comunicar el resultado de E1, sea cual sea

Aprobado por Ernesto el 2026-10-29, con las precisiones A, B, C, D y E. Texto definitivo. Su huella SHA-256 se guarda aparte (HUELLA.txt), junto con la marca de tiempo de FreeTSA.

EDGE se compromete, antes de ejecutar E1 y sin conocer su resultado, a lo siguiente.

**1. Se comunica siempre, en 14 días desde el consumo.** E1 se ejecuta una sola vez. Se comunica el resultado sea favorable, desfavorable, no concluyente o abortado. El plazo máximo es de 14 días naturales desde que E1 queda consumida (`CONSUMED` escrito en A, B y R2). Si en ese plazo:
- **E1 se abortó:** se publica que se abortó, en qué fase y con qué código de parada.
- **E1 terminó pero el informe aún no está descifrado y verificado:** se publica que terminó, la huella del informe (`report_sha256`) y el motivo del retraso. El informe se publica en cuanto se descifre y su huella coincida.
- **El informe no puede recuperarse nunca:** se publica que el resultado es irrecuperable.

Ningún fallo de descifrado o de publicación aplaza esta obligación, ni autoriza repetir E1.

**2. Qué se publica.** Solo lo que es de EDGE y está prerregistrado (`docs/PSPORTS-BASELINE-V0.md` §5-§6 y §10.13).

a) **Mínimo que se publica siempre**, con independencia de la consulta A.2:
- el estado final de E1;
- para Q2a (comparación con la referencia HOME_AWAY_FREQ), en `T-1440m` y `T-2m`, la categoría de veredicto (`MEJORA_CLARA`, `SENAL_POSITIVA_NO_CONCLUYENTE`, `SIN_EVIDENCIA`, `PEOR_NO_CONCLUYENTE` o `PEOR`);
- para Q1 (calibración), por cada suceso y horizonte: si la estimación y su intervalo son ESTIMADO o NO_ESTIMABLE, el motivo, y los remuestreos válidos y separados frente al mínimo de 1.900;
- el número de partidos evaluados y excluidos, con los recuentos por motivo;
- el commit, la huella de la hoja de sellado y la huella del informe.

b) **Cifras agregadas:** las estimaciones e intervalos de Q1 y Q2a (remuestreo por jornada, 2.000 réplicas, semilla 20260930, Bonferroni ×2). Se publican según lo que permita la consulta A.2.

c) **Regla contra la ocultación:**
- el nivel de detalle se fija por escrito antes de armar E1, según la respuesta a A.2 o, si no la hay, solo el mínimo de a);
- se aplica por igual a todas las métricas, sea cual sea su signo;
- una restricción de datos de terceros nunca puede ocultar una categoría, un NO_ESTIMABLE ni un estado;
- lo que no se publique queda comprometido por la huella del informe, y se publicará tal cual si A.2 lo permite más adelante.

Lo NO_ESTIMABLE se publica como tal, sin cifras (§10.13.8). No cuenta como favorable ni como desfavorable.

**3. Qué NO se publica.** Ni partidos, ni resultados, ni identificadores, ni probabilidades partido a partido, porque son datos de terceros o derivan de ellos (consulta A.2).

**4. Sin reinterpretación.** No se cambian métricas, horizontes ni categorías después de ver el resultado. Un resultado desfavorable no se presenta como favorable, ni uno no concluyente como señal. Q1 no tiene veredicto de aprobado o suspenso (§10.13.9). Nada de E1 cambia v0 (§10.10).

**5. Producción.** Incorporar 2025-26 al entrenamiento después de E1 (§10.10, paso 5) es un cambio del conjunto de datos en el laboratorio. No depende del resultado de E1 y no despliega nada. Cualquier cambio de lo que corre en producción necesita autorización expresa aparte.

**6. Anterioridad de este compromiso.** Antes de armar E1, la huella SHA-256 de este texto aprobado se sella con una marca de tiempo RFC 3161 de FreeTSA. El texto, su huella y la marca se publican en el primer historial público de EDGE, a más tardar junto con la primera comunicación de E1. Cualquiera puede comprobar con `openssl ts -verify` que el texto existía sin cambios antes de la ejecución. Sin esa marca, E1 no se arma.
