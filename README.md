# EDGE — evidencias públicas

EDGE es un proyecto de investigación que construye y evalúa modelos de probabilidad para partidos de fútbol. Este
repositorio no contiene el motor, los modelos ni datos: solo **compromisos que EDGE adquiere antes de conocer un
resultado**, con marcas de tiempo de una autoridad externa, para que cualquiera pueda comprobar después que no se
cambiaron.

## Qué se publica

### E1 — compromiso de comunicar el resultado, sea cual sea

E1 es la evaluación, una sola vez, del modelo de referencia de EDGE (v0, congelado) sobre una temporada que el
modelo no ha visto. Antes de ejecutarla, EDGE se compromete por escrito a comunicar su resultado sea favorable,
desfavorable, no concluyente o abortado, en un plazo máximo de 14 días.

| Fichero | Qué es |
|---|---|
| `e1/compromiso/COMPROMISO-COMUNICAR-E1.md` | el texto del compromiso, tal como se aprobó |
| `e1/compromiso/HUELLA.txt` | su SHA-256: `1c488a26418cdf2bfa4181f3c8cd68e6f1cb8be80cd3fb85ea40a8dc34154306` |
| `e1/compromiso/marcas/freetsa.tsq` | la petición de marca de tiempo (RFC 3161): solo la huella y un número aleatorio |
| `e1/compromiso/marcas/freetsa.tsr` | la respuesta firmada por FreeTSA: 2026-10-29 19:52:11 GMT, serie `0x098D2DE3` |
| `e1/compromiso/autoridades/freetsa/` | los certificados de FreeTSA necesarios para verificarla |
| `e1/NIVEL-PUBLICACION-E1.md` | qué se publicará del resultado, fijado antes de ejecutar E1 (sin marca de tiempo propia) |

El resultado de E1 se añadirá en `e1/resultado/` cuando exista.

## Cómo se verifica

Con OpenSSL, desde `e1/compromiso/`:

    sha256sum -c HUELLA.txt
    openssl ts -verify -in marcas/freetsa.tsr -data COMPROMISO-COMUNICAR-E1.md \
        -CAfile autoridades/freetsa/cacert.pem -untrusted autoridades/freetsa/tsa.crt
    openssl ts -verify -in marcas/freetsa.tsr -queryfile marcas/freetsa.tsq \
        -CAfile autoridades/freetsa/cacert.pem -untrusted autoridades/freetsa/tsa.crt
    openssl ts -reply -in marcas/freetsa.tsr -text

Las dos verificaciones deben decir `Verification: OK`. Cambiar un solo byte del texto da `Verification: FAILED`.

La raíz de FreeTSA no está en los almacenes de certificados de los sistemas operativos. Compara la huella de
`autoridades/freetsa/cacert.pem` con la que publica https://freetsa.org:

    openssl x509 -in autoridades/freetsa/cacert.pem -noout -fingerprint -sha256
    # A6:37:9E:7C:EC:C0:5F:AA:3C:BF:07:60:13:D7:45:E3:27:BB:BA:A3:8C:0B:9A:F2:24:69:D4:70:1D:18:AA:BC

Los ficheros se guardan byte a byte (`.gitattributes`: `* -text`), así que un clon en cualquier sistema da las
mismas huellas.

## Qué garantiza una marca de tiempo, y qué no

- **Garantiza** que el texto existía, exactamente así, en la fecha de la marca: FreeTSA firmó su huella en ese
  momento, y nadie, tampoco EDGE, puede fabricar después una marca con una fecha anterior.
- **No garantiza** que EDGE cumpla lo que el texto dice; eso se comprueba con lo que se publique después.
- **No garantiza** que el texto se escribiera sin conocer el resultado. Lo que sí permite es comprobar que la marca
  es anterior a la ejecución, comparando su fecha con la de los registros de E1 cuando se publiquen.
- Depende de que FreeTSA sea una autoridad honesta y su clave no esté comprometida.

## Limitaciones de la ejecución de E1 (variante M)

E1 se ejecuta en el ordenador de EDGE, con protecciones técnicas: el modelo corre en un proceso separado que solo
recibe los datos disponibles en cada momento; cada predicción se registra y se sella antes de pedir ningún
resultado; unos registros de consumo en dos discos impiden una segunda ejecución; y el informe se cifra y se sella
por su huella antes de leerlo.

**Esto no es una auditoría independiente ni una prueba absoluta de ejecución única.** La variante M renuncia
expresamente a:

- protección frente a un operador o administrador del equipo que quiera hacer trampa a propósito, frente a
  software malicioso en la sesión y frente a otras cuentas del equipo;
- una prueba independiente, fuera del equipo de EDGE, de que E1 se ejecutó una sola vez: solo quedan registros
  locales y sus copias;
- la equivalencia exacta con una plataforma de referencia: las cifras podrían diferir en los últimos decimales, y
  el informe declara la plataforma.

Cubre los errores del código y del operador, no la mala fe. Lo publicado aquí permite comprobar que el compromiso
es anterior y que no se cambió; la confianza en la ejecución misma depende de esas protecciones locales.

## Qué no se publica

Ni partidos, ni resultados, ni identificadores, ni probabilidades partido a partido, porque son datos de terceros o
derivan de ellos. Tampoco código, modelos, bases de datos ni claves.
