# Calculadora de pensión IMSS Ley 73

Herramienta web para estimar la pensión por Cesantía en Edad Avanzada o Vejez bajo el régimen de la
Ley del Seguro Social de 1973, a partir de la Constancia de Semanas Cotizadas que emite el IMSS.

Lee el PDF oficial, extrae el historial completo de salarios base de cotización y calcula la pensión
conforme al artículo 167, comparando escenarios con distintos años de Modalidad 40. Genera un reporte
descargable de una hoja.

**Todo el procesamiento ocurre en el navegador.** El PDF nunca se sube a ningún servidor y la página
no tiene backend, cookies ni analítica.

## Qué hace

- Extrae de la constancia: CURP y fecha de nacimiento, NSS, nombre, semanas cotizadas, fecha de
  emisión y todos los movimientos de salario de cada patrón.
- Detecta el régimen. Si la primera alta es posterior al 1 de julio de 1997, avisa que el asegurado
  está en Ley 97 y el cálculo no aplica.
- Calcula el promedio nominal del salario base de cotización de las últimas 250 semanas, ponderado
  por días, incluyendo el periodo de Modalidad 40.
- Aplica la tabla del artículo 167 (cuantía básica e incrementos por cada 52 semanas sobre las
  primeras 500), el factor de edad por cesantía y las asignaciones familiares del artículo 164.
- Estima el costo de la Modalidad 40 con la escalera de cuotas vigente hasta 2030.
- Compara escenarios de 0, 1, 3 y 5 años de Modalidad 40.

## Cómo desplegarlo

Es un solo archivo estático sin build. Cualquiera de estas rutas funciona:

**GitHub Pages.** Sube `index.html` a la raíz del repositorio, entra a Settings → Pages, elige la rama
`main` y la carpeta `/ (root)`. En un par de minutos queda en
`https://<usuario>.github.io/<repositorio>/`.

**Netlify o Vercel.** Arrastra la carpeta a su panel de despliegue. No hay comando de build ni
directorio de salida que configurar.

**Tu propio hosting.** Copia `index.html` donde sirvas archivos estáticos. No requiere PHP, Node ni
base de datos.

Si lo pones en un subdirectorio no hay que ajustar rutas: no usa recursos relativos.

## Dependencias

Se cargan por CDN, sin instalación:

| Librería | Uso |
|---|---|
| pdf.js 3.11.174 | Lectura del PDF de la constancia |
| jsPDF 2.5.1 | Generación del reporte |
| jspdf-autotable 3.8.2 | Tablas del reporte |

## Supuestos y límites

- Los salarios posteriores a la fecha de la constancia se proyectan con crecimiento compuesto
  bimestral, configurable desde la interfaz.
- La UMA de años futuros se proyecta con una tasa anual configurable. El INEGI publica el valor real
  cada enero.
- El salario base de cotización elegido para la Modalidad 40 se toma fijo en pesos durante todo el
  periodo, que es como opera en la práctica.
- El tope de cotización se aplica en 25 UMA, criterio administrativo vigente del IMSS.
- **No contempla periodos con dos patrones simultáneos.** Si los hubo, el promedio puede quedar
  subestimado.
- **No descuenta semanas por retiros parciales por desempleo.** Si la constancia las reporta, hay
  que restarlas manualmente en el campo de semanas.

## Aviso

Las cifras son estimaciones de planeación, no montos garantizados por el IMSS. Esta herramienta no
constituye asesoría previsional. Antes de renunciar a un empleo o contratar la Modalidad 40, conviene
validar el caso con un especialista que revise el expediente completo.

## Licencia

MIT
