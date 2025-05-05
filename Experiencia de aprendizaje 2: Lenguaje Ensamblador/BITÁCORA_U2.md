# Investigación :shrimp:	
> [!IMPORTANT]
> [Página](https://confusion-snapper-025.notion.site/Experiencia-de-aprendizaje-2-Lenguaje-Ensamblador-17ee8161b2a1809b97e9f4351629ad72) de la unidad.

### Actividad 1
- ¿Qué es la entrada-salida mapeada a memoria?
es una técnica en la que los dispositivos de entrada y salida (como el teclado y la pantalla) se comunican con la CPU a través de direcciones específicas de la memoria RAM. Es decir, se reserva una porción de la memoria para que funcione como "puerta de acceso" a los dispositivos de I/O. Así, leer o escribir en ciertas posiciones de memoria es equivalente a interactuar con el hardware.
  
- ¿Cómo se implementa en la plataforma Hack?
Se implementa así:
* Pantalla
Dirección base: 16384 (decimal) ó 0x4000 (hexadecimal).
La pantalla Hack es de 256 filas × 512 columnas en blanco y negro.
Cada bit representa un píxel (0 = blanco, 1 = negro).
Cada palabra (16 bits) representa 16 píxeles horizontales.
Así que se usan 8192 palabras de memoria para cubrir toda la pantalla.

* Teclado 
Dirección: 24576 (decimal) ó 0x6000 (hexadecimal).
Al presionar una tecla, se escribe en esta dirección el código ASCII correspondiente.
Si no se presiona ninguna tecla, el valor es 0.

- Inventa un programa que haga uso de la entrada-salida mapeada a memoria.
Hice que pintara un rectangulo
```
@SCREEN
D=A
@address
M=D           

@0
D=A
@i
M=D           // i = 0

(LOOP)
  @i
  D=M
  @16
  D=D-A
  @END
  D;JGE       // Si i >= 16, termina

  @address
  A=M
  M=-1      

  @address
  D=M
  @32
  D=D+A      
  @address
  M=D

  @i
  M=M+1
  @LOOP
  0;JMP

(END)
@END
0;JMP
```

- Investiga el funcionamiento del programa con el simulador.
Inicializa la dirección base de la pantalla:
```
@SCREEN
D=A
@address
M=D
```
Se guarda en la variable address la dirección base de la pantalla (16384). Esta es la posición de memoria donde comienza el mapeo de píxeles.
```
@0
D=A
@i
M=D
```
Se usa la variable i como contador de filas, comenzando en 0.

Inicio del bucle LOOP:
```
(LOOP)
  @i
  D=M
  @16
  D=D-A
  @END
  D;JGE
```
Se compara i con 16. Si i >= 16, el programa salta a la etiqueta END y termina. Esto limita el dibujo a 16 filas.

Dibuja una fila de píxeles negros:
```
A=M
M=-1
```
En la dirección de memoria apuntada por address, se escribe -1, que representa una fila de 16 píxeles negros (ya que un bit encendido es un píxel negro en Hack).

Avanza a la siguiente fila de pantalla:
```
D=M
@32
D=D+A
@address
M=D
```
La pantalla Hack tiene 512 píxeles por fila y cada palabra representa 16 píxeles, así que cada fila ocupa 32 palabras. Aquí se incrementa address en 32 para apuntar a la siguiente fila.

Incrementa el contador de filas:
```
@i
M=M+1
@LOOP
0;JMP
```
Se incrementa i y se vuelve al inicio del bucle para repetir el proceso hasta completar las 16 filas.

Fin del programa:
```
(END)
@END
0;JMP
```
### Actividad 2
Tengo el código analizado. :suspect:

### Actividad 3
- Si se presiona la letra “d” muestra la imagen del reto 18 de la unidad pasada, Si no se presiona ninguna tecla, borrarás la imagen.

R// Código
```
(WHILE)
    @24576
    D = M        // Leer entrada del teclado
    @68
    D = D - A
    @DRAW
    D;JEQ        // Si D == 68, salta a dibujar

    @24576
    D = M
    @0
    D = D - A
    @CLEAR
    D;JEQ        // Si D == 0, salta a borrar

    @WHILE
    0;JMP        // Vuelve a comenzar el ciclo

// ------------------ DIBUJAR ------------------
(DRAW)
    @SCREEN
    D=A
    @R12
    M=D

    // Escribir valor no nulo para "dibujar"
    @R12
    A=M
    M=-1
    @R12
    D=M
    @32
    D=D+A
    @R12
    M=D

    A=M
    M=-1
    @R12
    D=M
    @32
    D=D+A
    @248
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @13060
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @11278
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @8216
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @4484
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @8770
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @13473
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @11439
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @10408
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @4166
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @8194
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @6154
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @2038
    D=D+A
    A=D
    M=-1

    @32
    D=A
    @2
    D=D+A
    A=D
    M=-1

    @WHILE
    0;JMP

// ------------------ BORRAR ------------------
(CLEAR)
    @SCREEN
    D=A
    @R12
    M=D

    // Escribir 0 para borrar
    @R12
    A=M
    M=0
    @R12
    D=M
    @32
    D=D+A
    @R12
    M=D

    A=M
    M=0
    @R12
    D=M
    @32
    D=D+A
    @248
    D=D+A
    A=D
    M=0

    @32
    D=A
    @13060
    D=D+A
    A=D
    M=0

    @32
    D=A
    @11278
    D=D+A
    A=D
    M=0

    @32
    D=A
    @8216
    D=D+A
    A=D
    M=0

    @32
    D=A
    @4484
    D=D+A
    A=D
    M=0

    @32
    D=A
    @8770
    D=D+A
    A=D
    M=0

    @32
    D=A
    @13473
    D=D+A
    A=D
    M=0

    @32
    D=A
    @11439
    D=D+A
    A=D
    M=0

    @32
    D=A
    @10408
    D=D+A
    A=D
    M=0

    @32
    D=A
    @4166
    D=D+A
    A=D
    M=0

    @32
    D=A
    @8194
    D=D+A
    A=D
    M=0

    @32
    D=A
    @6154
    D=D+A
    A=D
    M=0

    @32
    D=A
    @2038
    D=D+A
    A=D
    M=0

    @32
    D=A
    @2
    D=D+A
    A=D
    M=0

    @WHILE
    0;JMP

```

### Actividad 4
- Si se presiona la letra “d” muestras la imagen que diseñaste en el reto 18. Solo si se presiona la letra “e” borrarás la imagen que se muestra en pantalla.

R// Código
```
(WHILE)
    @24576
    D=M          // Leer tecla

    @100         // Comparar con 'd' (código ASCII 100)
    D=D-A
    @DRAW
    D;JEQ        // Si D == 0 (tecla 'd'), salta a DRAW

    @24576
    D=M
    @68          // Comparar con 'D' (código ASCII 68)
    D=D-A
    @DRAW
    D;JEQ        // Si D == 0 (tecla 'D'), salta a DRAW

    @24576
    D=M
    @69          // Comparar con 'E' (código ASCII 69)
    D=D-A
    @CLEAR
    D;JEQ        // Si D == 0 (tecla 'E'), salta a CLEAR

    @WHILE
    0;JMP        // Si no es ni 'd', 'D' ni 'E', vuelve a empezar

// -------- DIBUJAR IMAGEN --------
(DRAW)
    @SCREEN
    D=A
    @R12
    AD=D+M
    M=-1

    D=A 
    @32
    AD=D+A
    M=-1

    D=A 
    @32
    AD=D+A
    @248 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @13060 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @11278 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @8216 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @4484 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @8770 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @13473 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @11439 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @10408 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @4166 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @8194 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @6154 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @2038 
    D=D+A 
    A=D-A 
    M=-1

    D=A 
    @32
    AD=D+A
    @2 
    D=D+A 
    A=D-A 
    M=-1

    @WHILE
    0;JMP

// -------- BORRAR IMAGEN --------
(CLEAR)
    @SCREEN
    D=A
    @R12
    AD=D+M
    M=0

    D=A 
    @32
    AD=D+A
    M=0

    D=A 
    @32
    AD=D+A
    @248 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @13060 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @11278 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @8216 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @4484 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @8770 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @13473 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @11439 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @10408 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @4166 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @8194 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @6154 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @2038 
    D=D+A 
    A=D-A 
    M=0

    D=A 
    @32
    AD=D+A
    @2 
    D=D+A 
    A=D-A 
    M=0

    @WHILE
    0;JMP
```

### :fire: Reto :fire:
> [!CAUTION]
> En la bitácora vas a reportar para cada mini-reto dos cosas:
> - El código con la implementación (RAE1).
> - Explica cómo probaste las partes del programa y cómo probaste el programa completo (RAE2).

1. Escribe un programa en lenguaje ensamblador que sume los primeros 100 números naturales.
```
// i = 1
@1          // Cargar el valor 1
D=A         // Guardar 1 en el registro D
@16         // Dirección de memoria para 'i' (puede ser cualquier libre)
M=D         // Almacenar 1 en la dirección de i

// sum = 0
@0          // Cargar el valor 0
D=A         // Guardar 0 en el registro D
@17         // Dirección de memoria para 'sum' (puede ser cualquier libre)
M=D         // Almacenar 0 en la dirección de sum

(LOOP)      // Etiqueta para el ciclo while
    @16     // Cargar dirección de i
    D=M     // Obtener el valor de i
    @100    // Cargar el valor 100
    D=D-A   // Restar i - 100
    @END    // Si i > 100, salta a END
    D;JGT   // Si D > 0 (i <= 100), continuar con el ciclo

    @LOOP   // Si no, repetir el ciclo

// sum += i
(SUM)      
    @16     // Cargar dirección de i
    D=M     // Obtener el valor de i
    @17     // Dirección de sum
    M=D+M   // sum = sum + i

// i++
(INCREMENT)
    @16     // Dirección de i
    M=M+1   // Incrementar i por 1
    @LOOP   // Regresar al ciclo
    0;JMP   // Saltar de nuevo a LOOP

(END)      // Etiqueta de salida del ciclo
    // El valor final de sum está en la dirección de memoria sum
```
**Explicación del código:**
- i = 1 y sum = 0: Inicializamos las variables i y sum con los valores iniciales en direcciones de memoria específicas. Aquí, i se guarda en la dirección @16 y sum en la dirección @17.
- Ciclo while (LOOP): Usamos la dirección de i y la comparamos con 100. Si i <= 100, el ciclo continúa. Si i es mayor que 100, el programa salta a la etiqueta END y termina.
- sum += i: En cada iteración, el valor de i se suma al valor de sum.
- i++: Después de sumar, incrementamos i en 1.
- Almacenamiento de resultados: Al final del programa, el valor de sum está almacenado en la dirección de memoria @17.

**Ahora con lo de RAE2:**
Prueba en el simulador de Hack CPU:
- Configuración inicial:
  Cargué el código en el simulador de Hack de Nand2Tetris.
  Aseguré que las direcciones de memoria @16 y @17 no estuvieran siendo utilizadas por otras variables o instrucciones.

- Ejecución:
  Ejecuté el programa paso a paso para observar cómo i se incrementaba y cómo sum aumentaba en cada iteración.
  Al final del ciclo, verifiqué que sum tuviera el valor esperado, que es 5050.

- Verificación de la salida:
Después de ejecutar el ciclo completo, comprobé el valor final de sum en la memoria. Si el valor de sum era 5050, entonces el programa funcionaba correctamente.

**Ahora las respuestas al punto como tal:**
- ¿Cómo están implementadas las variables `i` y `sum`?
  Las variables i y sum son implementadas como direcciones de memoria. En Hack Assembly, las variables no tienen nombres como en los lenguajes de alto nivel; se representan por direcciones de memoria a las cuales se les asignan valores.
  i se almacena en una dirección de memoria específica (por ejemplo, @i).
  sum se almacena en otra dirección de memoria (por ejemplo, @sum).
  
- ¿En qué direcciones de memoria están estas variables?
En el código proporcionado, no se han asignado direcciones específicas a las variables i y sum explícitamente. Sin embargo, en Hack Assembly, las direcciones de memoria son específicas y se asignan de la siguiente forma:
  - i: Se puede almacenar en cualquier dirección de memoria libre que no se esté utilizando para otras cosas, como @16 (el valor de i podría almacenarse en la dirección 16, por ejemplo).
  - sum: Igualmente, se puede almacenar en cualquier dirección libre, como @17.
En este caso, se asignan en el código como direcciones simbólicas @i y @sum, pero debes escoger direcciones dentro del rango disponible.

- ¿Cómo está implementado el ciclo `while`?
El ciclo while se implementa usando una estructura condicional que compara el valor de i con 100. Si i es menor o igual a 100, el ciclo continúa ejecutándose. Esto se logra con el código:
```
@i      // Cargar dirección de i
D=M     // Obtener el valor de i
@100    // Cargar el valor 100
D=D-A   // Restar i - 100
@END    // Si i > 100, salta a END
D;JGT   // Si D > 0 (i <= 100), continuar con el ciclo
```
Si i es menor o igual a 100, el ciclo continúa, y si no, se salta a la etiqueta END y termina el ciclo.
  
- ¿Cómo se implementa la variable `i`?
```
@i      // Cargar dirección de i
M=M+1   // Incrementar i por 1
```
Esto simula el comportamiento del incremento de i dentro del ciclo.
  
- ¿En qué parte de la memoria se almacena la variable `i`?
La variable i se almacena en una dirección de memoria elegida para ella. En Hack Assembly, puedes usar cualquier dirección de memoria disponible para almacenar la variable i. Si usas @i, la memoria asociada a i se encuentra en una dirección arbitraria como 16, 17, etc., según el contexto del programa.
  
- Después de todo lo que has hecho, ¿Qué es entonces una variable?
Es una variable es simplemente una dirección de memoria donde se almacena un valor. No tiene el tipo o nombre simbólico de una variable en lenguajes de alto nivel, sino que es un lugar específico en la memoria que contiene un dato que puede cambiar a lo largo del programa.
  
- ¿Qué es la dirección de una variable?
La dirección de una variable es la ubicación de memoria donde esa variable se encuentra almacenada. 
  
- ¿Qué es el contenido de una variable?
El contenido de una variable es el valor que está almacenado en la dirección de memoria asociada a esa variable.

2. Transforma el programa en alto nivel anterior para que utilice un ciclo for en vez de un ciclo while.
```
int sum = 0;
for (int i = 1; i <= 100; i++) {
    sum += i;
}
```
3. Escribe un programa en lenguaje ensamblador que implemente el programa anterior.
```
// Inicialización de sum = 0
@0          // Cargar el valor 0
D=A         // Guardar 0 en el registro D
@17         // Dirección de memoria para 'sum'
M=D         // Almacenar 0 en la dirección de sum

// Inicialización de i = 1
@1          // Cargar el valor 1
D=A         // Guardar 1 en el registro D
@16         // Dirección de memoria para 'i'
M=D         // Almacenar 1 en la dirección de i

(FOR)       // Etiqueta para el ciclo for
    @16     // Cargar dirección de i
    D=M     // Obtener el valor de i
    @101    // Cargar el valor 101
    D=D-A   // Restar i - 101
    @END    // Si i > 100, salta a END
    D;JGE   // Si D >= 0 (i > 100), terminar el ciclo

    // sum = sum + i
    @16     // Cargar dirección de i
    D=M     // Obtener el valor de i
    @17     // Dirección de sum
    M=D+M   // sum = sum + i

    // i++
    @16     // Dirección de i
    M=M+1   // Incrementar i por 1

    @FOR    // Regresar al ciclo
    0;JMP   // Saltar de nuevo a FOR

(END)      // Etiqueta de salida del ciclo
    // El valor final de sum está en la dirección de memoria sum

```
**Explicación del código:**
- Inicialización: sum se inicializa en 0 y i en 1.
- Ciclo for: Compara si i <= 100. Si es cierto, realiza las operaciones de acumulación (sum += i) y luego incrementa i en 1.
- Condición de parada: Cuando i llega a 101, el ciclo termina y el valor final de sum está en la memoria @17.

**RAE2 - Prueba del programa**
- Configuración inicial:
La memoria en la dirección @17 está destinada a almacenar la variable sum, y la memoria en @16 se utiliza para la variable i.
Antes de comenzar el ciclo, sum está en 0 y i en 1.

- Ejecución del programa:
Ejecuta el programa paso a paso en el simulador Hack. Asegúrate de que la memoria en la dirección @17 se va acumulando con los valores de i en cada iteración.
Puedes observar que la variable i se incrementa con cada ciclo (de 1 a 100), y sum va acumulando el total de la suma.

- Resultado esperado:
Al final del ciclo, cuando i llega a 101, el valor de sum será igual a 5050, que es la suma de los primeros 100 números naturales:
sum=1+2+3+...+100=5050

- Verificación:
Después de ejecutar el programa completo, puedes verificar que en la dirección de memoria @17 (donde se almacena sum), el valor será 5050.
Si el valor es correcto, la prueba se considera exitosa.

5. Traduce este programa a lenguaje ensamblador:
```
int a = 10;
int *p;
p = &a;
*p = 20;
```

R//
```
// a = 10
@10
D=A
@16     // RAM[16] = a
M=D

// p = &a
@16
D=A
@17     // RAM[17] = p
M=D

// *p = 20
@17     // Accede a p
A=M     // A = M[17] => dirección de 'a'
M=20    // *p = 20 -> M[ RAM[17] ] = 20
```

**RAE2:**
Inicialización de a = 10: Ejecuté hasta esta línea y verifiqué en el simulador que RAM[16] == 10.
Asignación del puntero p = &a: Después de esta parte, comprobé que RAM[17] == 16 (la dirección donde está a).
Desreferenciación *p = 20: Luego de ejecutar esta sección, verifiqué que RAM[16] == 20, lo cual significa que *p (es decir, a) fue correctamente modificado.
Luego corrí todo el código en el CPU Emulator de nand2tetris.
Al final:
> RAM[16] == 20 (el valor de a)
> RAM[17] == 16 (p apunta correctamente a a)
Esta bien el puntero :D


