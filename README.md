# Plugins de auditoría de Ensys

Procedimientos de auditoría que trabajan directamente sobre el expediente de
Gesia o sobre el cliente de muestreo de ForSampling, y producen papeles de trabajo
en Excel y Word.

Hay **dos plugins** y se instala **uno solo**:

| Plugin | Para quién | Qué lleva |
|---|---|---|
| **Gesia — Expediente de auditoría** | Quien tiene la suite de Gesia | Todos los procedimientos, incluidas las pruebas de muestreo de ForSampling |
| **ForSampling — Pruebas de muestreo** | Quien tiene ForSampling sin Gesia | Las pruebas de muestreo, el papel de la NIA-ES 530 y el registro de ejecución |

Los dos comparten el programa que lee los ficheros, y con los dos activos no se sabe cuál
contesta. Si pasa, el propio plugin lo avisa al empezar y dice cuál sobra.

## Instalación

En Claude, en **Configuración**:

1. En el apartado **Personalizar**, pulsa **Plugins**.
2. Arriba a la derecha, despliega **Agregar** y elige **Agregar marketplace**.
3. En el campo **URL**, escribe esto y pulsa **Sincronizar**:

   ```
   Ensys-Consultores-Informaticos/ensys-plugins
   ```

4. En la lista aparecen los dos plugins, de Ensys Consultores Informáticos, S.L. Pulsa
   **Instalar** en el que te corresponda: **Gesia — Expediente de auditoría** si tienes
   Gesia, **ForSampling — Pruebas de muestreo** si solo tienes ForSampling.
5. **Cierra Claude del todo y vuelve a abrirlo.** El programa que lee el expediente se
   registra al arrancar, y hasta que no reinicias no está disponible.

Los procedimientos funcionan en **Cowork**, no en una conversación normal de chat: desde
el chat Claude no puede leer el expediente ni escribir los papeles de trabajo. Abre una
sesión de Cowork y empieza diciendo con qué expediente trabajas:

```
Conecta con el encargo Ejemplo 24.gs3, que está en C:\Auditorias\Ejemplo 24
```

Con el plugin de ForSampling, el fichero es el cliente de muestreo, el `.cli`:

```
Conecta con el cliente de muestreo Ejemplo.cli, que está en C:\Auditorias\Ejemplo 24\Muestreo
```

Para la ruta, sin teclearla: clic derecho sobre el archivo en el Explorador y
«Copiar como ruta de acceso». Claude responderá con el cliente que ha encontrado, el
diario vinculado y si el servidor de Gesia responde: conviene leer eso antes de seguir.

## Actualizar a una versión nueva

**Dónde pulsar depende de dónde uses el plugin**, y es la causa más común de que
parezca que no se puede actualizar:

- **En la aplicación de Claude:** abre la ficha del plugin y pulsa **Actualizar**. Con
  eso basta. Si el botón no aparece, es que la aplicación todavía no se ha enterado de
  que hay versión nueva: revisa sus marketplaces o quita y vuelve a añadir este.
- **En Claude Code:** el marketplace tiene que estar añadido en la propia CLI, con
  `/plugin marketplace add Ensys-Consultores-Informaticos/ensys-plugins`. Si no lo
  está, «buscar actualizaciones» falla con un **«No se pudo actualizar el
  marketplace»** que no explica nada — y el motivo es solo ese.

No hay que desinstalar nada.

**¿Hace falta actualizar con el plugin frío?** Ya no: cada versión instala su propio
ejecutable en vez de intentar sustituir el que esté en marcha.

Si aun así te apareciera ese aviso, el remedio de siempre sigue valiendo: cierra Claude
del todo, vuelve a abrirlo y actualiza antes de usar ningún procedimiento. Desactivar el
plugin con su interruptor también suele bastar.

Y si es el **marketplace** el que se niega y el aviso vuelve aunque reinicies, **quítalo y
vuelve a añadirlo** con el nombre de arriba.

**Para saber qué versión tienes**, mira el final de la descripción del plugin: va escrita
ahí, como `(v1.6.4)`. El número que la aplicación muestra en el campo «Versión» **no es
la versión del plugin**: es un contador suyo de actualizaciones, que se reinicia si
quitas y vuelves a añadir el marketplace.

Después de actualizar, **reinicia Claude** una vez más: el programa que lee el
expediente se registra al arrancar, y hasta entonces la versión nueva no está
disponible.

## Antes de usarlo

Dos cosas que fallan a menudo, y las dos son del entorno, no del plugin:

- **El servidor API tiene que estar en marcha.** El plugin lo arranca solo si no responde.
  Con Gesia, si aun así las consultas vuelven vacías, puedes lanzarlo a mano desde
  *Herramientas → Gesia - Cuadro de mando → Arrancar servidor API*.
- **El diario contable necesita el driver de Access de 64 bits.** Si el
  expediente se lee bien y el diario no, es eso.

Requiere **Windows**, y Gesia o ForSampling instalado. El expediente, el cliente de
muestreo y el diario se leen en tu equipo: **ningún dato del cliente auditado sale de
ahí** sin pasar antes por la anonimización que se explica más abajo.

## Qué incluye

La columna de la derecha dice qué lleva el plugin de ForSampling; el de Gesia lleva todos.

| Skill | Qué hace | Entregable | ForSampling |
|---|---|---|---|
| **Cuadro de mando del diario** | Verifica el diario, lo concilia con los saldos del expediente y analiza punteo y apuntes atípicos | Panel HTML | — |
| **Revisión del contenido de la memoria** | Contesta el cuestionario de cuentas anuales a partir de las cuentas en PDF, justificando cada respuesta | Excel para importar en Gesia + papel en Word | — |
| **Estados financieros** | Balance y cuenta de resultados comparados de los ejercicios cargados, con la conciliación de lo que presenta el cliente a lo auditado —epígrafe a epígrafe y cuenta a cuenta—, el movimiento del patrimonio neto, y el estado de flujos de efectivo del módulo EFE con sus ajustes. Cuando no hay ningún ajuste aprobado, propone los importes cuyo criterio puede contrastar y lo entrega marcado como borrador | Cuatro papeles de trabajo en Excel | — |
| **Prueba de cumplimiento (ForSampling)** | Localiza el documento de cada elemento de la muestra, comprueba lo que el documento sostiene y propone el veredicto por atributo | Papel de trabajo en Excel | Sí |
| **Prueba MUM (ForSampling)** | Mide el importe que sostiene cada factura de la muestra y propone el saldo según auditoría, el error y la tasa de error | Papel de trabajo en Excel | Sí |
| **Papel de la NIA-ES 530** | Redacta en Word el papel de trabajo de una prueba MUM: objetivo, población, parámetros del diseño, selección, resultados por elemento y lo que falta, todo leído de los ficheros de ForSampling. Deja la conclusión en blanco, que es del auditor | Papel de trabajo en Word | Sí |
| **Cancelación de saldos** | Empareja las facturas de una cuenta con sus pagos o cobros y deja a la vista lo que queda pendiente de verdad. Respeta el punteo que ya trae el diario y completa el resto | Papel de trabajo en Excel | — |
| **Continuidad de saldos de apertura** | Compara cuenta por cuenta la apertura del diario con el cierre auditado del ejercicio anterior (NIA-ES 510) | Papel de trabajo en Excel | — |
| **Identificación de riesgos** | Elige los riesgos del encargo del catálogo de tu máster, a partir del balance, la cuenta de resultados y los ratios de los cinco ejercicios (NIA-ES 315) | Informe en Word | — |
| **Investigación de la entidad** | Investiga al cliente en fuentes públicas de internet —BORME, contratación pública, subvenciones, jurisprudencia y prensa— con tres agentes en paralelo, citando cada hecho a su fuente y declarando lo que no consta | Papel de trabajo en Word + evidencia JSON | — |
| **Registro de ejecución** | Escribe en el chat, de forma anónima, cómo ha ido un procedimiento: con qué tropezó y qué convendría mejorar. Sirve para reportarnos incidencias sin tener que explicarlas | Texto en el chat | Sí |

Los entregables se escriben en `AsistenteIA\<carpeta del procedimiento>`
dentro de la carpeta del propio expediente —o del cliente de muestreo, con el de
ForSampling—, para que estén donde los esperas.

Para la identificación de riesgos hace falta además **la ruta de tu máster de
Gesia**, el `.gs3` que lleva `CON RIESGOS` en el nombre: los riesgos se eligen de
tu propio catálogo, no de uno que venga con el plugin. **No hay que abrirlo en
Gesia**, basta con indicar dónde está.

## Cómo pedirlo

No hace falta recordar nombres. Basta decir lo que quieres:

- «lanza el cuadro de mando del diario»
- «revisa la memoria de este cliente» (adjuntando las cuentas anuales en PDF)
- «saca el balance comparado» o «revisa el estado de flujos del expediente»
- «comprueba los saldos de apertura»
- «identifica los riesgos de este encargo»
- «investiga a este cliente en fuentes públicas»
- «valida la muestra de compras contra las facturas»
- «haz el papel de la NIA 530 de la MUM»

Si dices solo «cuentas anuales» te preguntará a cuál de las dos cosas te
refieres: al **contenido de la memoria**, que necesita el PDF del cliente, o a
las **cifras** del expediente, que no lo necesitan.

## Lo que estos papeles son, y lo que no

Son **propuestas de papel de trabajo**. Las cifras salen del expediente y de tu
diario, y cada comprobación dice de dónde sale; pero la valoración, el alcance y
la conclusión son del auditor, que es quien firma. Ningún papel se entrega sin
que se hayan contado los avisos que hayan salido durante su preparación.

## Versión publicada

**2.0.7**, con el programa que lee el expediente en la **1.24.5**.

Lo que conviene saber para usarlo con criterio, porque es lo que no se puede deducir mirando
el resultado:

- **Los nombres de proveedores y clientes viajan anonimizados.** El asistente ve un código por
  cuenta, no la razón social, y el papel de trabajo recupera los nombres reales en tu equipo al
  entregarlo.
- **Las facturas escaneadas se tachan en tu equipo antes de subirlas.** Los PDF no salen de tu
  disco: sube una imagen por página con el nombre del emisor, la cabecera, el CIF, el IBAN, el
  teléfono, el correo, el pie y los márgenes en negro. **Importes, fechas y número de documento
  quedan legibles**, que es lo que la prueba necesita mirar.
- **Tú eliges.** Al empezar se te pregunta si quieres las facturas tachadas o tal cual, y con
  qué consecuencias. No se decide por ti ni se arrastra de una sesión a otra.
- **Lo que no se puede tapar se te dice.** El nombre se tapa cuando se reconoce al tercero en el
  plan de cuentas del expediente o, con solo ForSampling, en la población de la prueba. Un membrete que es solo un logotipo, un tercero que no está en
  ese plan —un banco, un transportista— o un nombre que el reconocimiento de texto parte en dos
  renglones pueden subir a la vista. **Cuando pasa se te avisa antes de subir nada**, con la
  cuenta, para que mires esas imágenes en tu carpeta y decidas. Es la parte que no se puede
  prometer.

El historial versión a versión no se publica aquí. Si necesitas saber qué cambió entre dos
versiones, pídelo por [Incidencias](https://github.com/Ensys-Consultores-Informaticos/ensys-plugins/issues).

## Soporte

Ensys Consultores Informáticos, S.L. · [Incidencias](https://github.com/Ensys-Consultores-Informaticos/ensys-plugins/issues)
