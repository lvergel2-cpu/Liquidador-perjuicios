# Liquidador integral de perjuicios

Herramienta académica para liquidar perjuicios en la jurisdicción de lo contencioso administrativo, conforme a la jurisprudencia de unificación de la Sección Tercera del Consejo de Estado.

## Qué liquida

El caso se define en la pestaña I y adapta todos los módulos:

| Tipo de caso | Lucro cesante | Daño moral | Daño a la salud |
| --- | --- | --- | --- |
| Muerte | Cónyuge e hijos, con acrecimiento (exp. 19146) o con cuotas fijas | Cinco niveles de cercanía (2014) | No aplica |
| Lesiones personales | Según la pérdida de capacidad laboral, con incapacidad temporal opcional | Gravedad de la lesión por nivel (2014) | Tabla por gravedad; excepción hasta 400 SMLMV |
| Privación injusta de la libertad | Tiempo de la detención (exp. 44572 de 2019) | 5 SMLMV por mes, tope de 100 (exp. 46681 de 2021) | Solo si se acreditó lesión psicofísica |

Además: daño emergente consolidado (indexado) y futuro (a valor presente), catálogo de medidas por afectación relevante a bienes o derechos convencional y constitucionalmente amparados, tablas de referencia y acta de liquidación exportable a PDF y Word.

## Archivos

- `index.html`: la aplicación completa (un solo archivo).
- `datos.json`: datos oficiales que se actualizan sin tocar la aplicación.

## Cómo actualizar los datos

1. **Cada mes**, cuando el DANE certifique el IPC: abra `datos.json`, reemplace el primer `null` del año en curso por el índice (con punto decimal) y actualice `actualizado` y `actualizado_texto`.
2. **Cada diciembre**, cuando se decrete el salario mínimo: agregue el año nuevo en `smlmv` y una fila nueva en `ipc` con doce `null`.
3. Guarde el cambio en GitHub (rama `main`). Vercel publica la nueva versión automáticamente.

Nunca registre índices estimados: solo los certificados por el DANE (serie de empalme, base diciembre de 2018 = 100).

## Reglas de cálculo

- Mes vencido: una fecha del mes X usa el IPC del mes X − 1; si es anterior al quinto día hábil (con festivos), el del mes X − 2.
- Tiempo en años, meses y días calendario, expresado en meses con dos decimales.
- Vida probable: Resolución 1555 de 2010 (RV08), con la edad en la fecha de la liquidación (sentencia); el período futuro corre desde esa fecha.
- Interés técnico: 0,004867 mensual.
- Los perjuicios tasados en SMLMV (morales, daño a la salud, bienes constitucionales) se liquidan con el salario mínimo del año de la sentencia, cualquiera que fuera el ingreso de la víctima.
- Piso del salario mínimo vigente a la liquidación; 25 % de prestaciones solo con vínculo laboral y pedido en la demanda; 25 % de gastos propios en caso de muerte.

Los resultados requieren verificación profesional y no sustituyen la valoración probatoria del juez.
