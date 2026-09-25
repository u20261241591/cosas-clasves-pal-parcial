# cosas-clasves-pal-parcial
Referencia rápida basada en el parcial de Estación Meteorológica Regional (USCO, TDS 2025-2).

1. Enunciado — patrón típico de estos parciales

Casi siempre el enunciado pide:

Varios arreglos paralelos (misma longitud, ej. 12 meses) representando entidades distintas (subestaciones, sucursales, sensores, etc.).
Un método que genera/llena los datos, con un parámetro boolean para elegir entre modo automático (aleatorio) y modo manual (por teclado).
Un método que compara dos arreglos según algún criterio agregado (normalmente el promedio).
Un método que detecta anomalías respecto a un umbral relativo al promedio (ej. ±20%).
Un método que genera un reporte/resumen (todos los valores, el máximo, el mínimo, el promedio).

Tip para el parcial: identifica estas 4-5 piezas apenas leas el enunciado; son casi siempre las mismas, solo cambia el dominio (temperaturas, ventas, notas, etc.).

2. Estructura de métodos reutilizable
Método	Qué hace	Detalle clave
generarDatos(boolean automatico, tipo min, tipo max)	Llena y devuelve un arreglo	Si automatico == true usa Math.random(); si no, usa Scanner
comparar(arr1, arr2)	Devuelve 1, 2 o 0	Compara promedios, nunca los datos crudos directamente
promedio(arr)	Devuelve double	Método auxiliar, lo usan casi todos los demás
detectarAnomalias(arr)	Devuelve int[] con los índices anómalos	Umbral: `valor >= prom*1.2
reporte(nombre, arr)	Imprime resumen	Usa mayor(), menor() y promedio() internamente
mayor(arr) / menor(arr)	Devuelven el índice del valor extremo	Se inicializan con arr[0], no con 0 o Integer.MAX_VALUE
3. Generación de números aleatorios en un rango
java
double valor = Math.random() * (max - min + 1) + min;

o con Random:

java
int valor = new Random().nextInt(max - min + 1) + min;
4. Errores comunes a evitar (ya los cometiste una vez, no los repitas)
Usar Scanner sin declararlo → siempre decláralo antes de usarlo (como campo estático o al inicio del método).
Copiar arreglos con = → copia = original; NO copia, solo apunta al mismo arreglo. Usa Arrays.copyOf(original, original.length).
Comparar tipos primitivos con null → un int nunca es null. Si necesitas "vacío", ajusta el tamaño real del arreglo con Arrays.copyOf en vez de dejar ceros sueltos.
Índices "0 por defecto" en arreglos de resultados → si usas un arreglo de tamaño fijo para acumular resultados variables (como anomalías), recórtalo al final a indReal para no confundir "vacío" con "índice 0".
Llamar un método de impresión dentro de un for que no le corresponde → revisa el nivel de indentación/alcance de las llaves {} antes de dar por bueno el código.
Comparar String con < o > → esos operadores no aplican a String; primero convierte con Integer.parseInt() o pide el dato con sc.nextInt()/sc.nextDouble().
5. Checklist mental para resolver el parcial
 ¿Cuántos arreglos necesito y de qué tipo (int[], double[])?
 ¿El método de generación pide boolean + mínimo + máximo?
 ¿El método de comparación usa el promedio, no los arreglos crudos?
 ¿La anomalía está bien calculada como ±20% del promedio?
 ¿El reporte imprime: todos los meses, mes mayor, mes menor y promedio?
 ¿Estoy copiando arreglos con Arrays.copyOf cuando corresponde, no con =?
 ¿Los métodos que buscan máximo/mínimo inicializan con arr[0]?
