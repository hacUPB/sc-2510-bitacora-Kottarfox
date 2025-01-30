# Investigación
> [!IMPORTANT]
> [Página](https://confusion-snapper-025.notion.site/Experiencia-de-aprendizaje-1-Arquitectura-del-computador-17ee8161b2a180dab569d52e21dfeade) de la unidad.

### Actividad 1
1. ¿Qué es un computador digital moderno?: Un computador digital moderno es una máquina electrónica que procesa, almacena y transmite información utilizando señales digitales. 
2. ¿Cuáles son sus partes?: Sus partes son: CPU, RAM, dispositivos de entrada y salida, hardware, software y la motherboard.

### Actividad 2
1. ¿Qué es entonces un programa?: Es una serie de instrucciones para decirle a una pc que tarea tiene que hacer.
2. ¿Qué es un lenguaje ensamblador?: Es un lenguaje también conocido como Assembly, que es considerado como programación de bajo nivel. Se usa en instrucciones básicas a nivel de hardware.
3. ¿Qué es lenguaje de máquina?: El lenguaje de máquina es el conjunto de instrucciones que una computadora puede entender y ejecutar directamente sin necesidad de ningún proceso intermedio. Es el nivel más bajo de programación y se compone de secuencias de bits (0s y 1s) que representan operaciones específicas para el procesador de la computadora.

### Actividad 3 
1. ¿Qué son PC, D y A?:
   - PC: Contador de Programa.
   - D: Registro de datos.
   - A: Registro de dirección.
3. ¿Para qué los usa la CPU?: La CPU usa los registros como PC, D y A para gestionar y ejecutar instrucciones de manera eficiente. Cada uno cumple funciones específicas que permiten a la CPU coordinar los flujos de datos y las operaciones dentro del procesador.

### Actividad 4
1. El programa que guarda en la posición 32 de la RAM un 100.

```
@100       
D = A     
@32        
M = D      
```

### Reto
1. Carga en D el valor 1978.
```
@1978     
D = A     
```

2. Guarda en la posición 100 de la RAM el número 69.
```
@69
D = A
@100
M = D
```

3. Guarda en la posición 200 de la RAM el contenido de la posición 24 de la RAM.
```
@24      
D=M     
@200     
M=D
```
   
4. Lee lo que hay en la posición 100 de la RAM, resta 15 y guarda el resultado en la posición 100 de la RAM.
```
@100   
D=M    
@15   
D=D-A   
@100    
M=D
```  
   
5. Suma el contenido de la posición 0 de la RAM, el contenido de la posición 1 de la RAM y con la constante 69. Guarda el resultado en la posición 2 de la RAM.
```
@0      
D=M    
@1      
D=D+M   
@69     
D=D+A   
@2      
M=D
```

6. Si el valor almacenado en D es igual a 0 salta a la posición 100 de la ROM.
```
@100  
D;JEQ 
```

7. Si el valor almacenado en la posición 100 de la RAM es menor a 100 salta a la posición 20 de la ROM.
```
@100     
D=M      
@100     
D=D-A
@20
D;JLT 
``` 
    
8. Considera el siguiente programa:
```
@var1
D = M
@var2
D = D + M
@var3
M = D
```
- Este programa suma lo que está en @var1 con @var2 y lo que es el resultado se queda guardado en @var3.
- @var1, @var2 y @var3 tendrían que estar delante del 16 para que se pueda hacer alguna operación.

9. Considera el siguiente programa:
```
// i = 1
@i
M=1
// sum = 0
@sum
M=0
// sum = sum + i
@i
D=M
@sum
M=D+M
// i = i + 1
@i
D=M+1
@i
M=D
```
- ¿Qué hace este programa?: Es una suma que sigue en ciclo de seguir aumentando i.
- ¿En qué parte de la memoria RAM está la variable i y sum? ¿Por qué en esas posiciones?: Tendrían que estar de la posición @16 en adelante, por que son los espacios de la memoria que el programa assembly destina para estas operaciones, no se pueden usar de 15 para abajo ya que ese es espacio destinado al funcionamiento de la máquina.

Optimiza esta parte del código para que use solo dos instrucciones:
```
// i = i + 1
@i
D=M+1
@i
M=D
```

- El código optimizado:
```
@i
M=M+1
```

10. Las posiciones de memoria RAM de 0 a 15 tienen los nombres simbólico R0 a R15. Escribe un programa en lenguaje ensamblador que guarde en R1 la operación 2 * R0.
```
@R0    
D=M   
@R1   
D=D+D  
M=D
```

11. Considera el siguiente programa:

```
// i = 1000
@1000
D=A
@i
M=D
(LOOP)
// if (i == 0) goto CONT
@i
D=M
@CONT
D;JEQ
// i = i - 1
@i
M=M-1
// goto LOOP
@LOOP
0;JMP
(CONT)
```

- ¿Qué hace este programa?: Es una resta en bucle.
- ¿En qué memoria está almacenada la variable i? ¿En qué dirección de esa memoria? En cualquier parte de la ram después del 16.
- ¿En qué memoria y en qué dirección de memoria está almacenado el comentario //`i = 1000?`: Como es un comentario no estaría ocupando espacio alguno en la memoria.
- ¿Cuál es la primera instrucción del programa anterior? ¿En qué memoria y en qué dirección de memoria está almacenada esa instrucción?: La primera instrucción sería el @1000 y estaría en 0 para dar comienzo al programa.
- ¿Qué son CONT y LOOP?:
  - CONT: este sería lo que marcaría el final del bucle, si es @CONT hace un salto hacia CONT.
  - LOOP: y este es el que inicia el bucle, si es @LOOP sería lo que marca el salto hacia la etiqueta de LOOP.
- ¿Cuál es la diferencia entre los símbolos `i` y `CONT`?:
  - i es una variable.
  - CONT es una etiqueta, siendo la que marca el final del loop.

12. Implemente en ensamblador:
```
R4 = R1 + R2 + 69
```

- El código en Assembly:
```
    @1
    D=M
    @2
    D=D+M
    @69
    D=D+A
    @4
    M=D
```


13. Implemente en ensamblador:
```
if R0 >= 0 then R1 = 1
else R1 = –1

(LOOP)
goto LOOP
```


14. Implementa en ensamblador:
```
R4 = RAM[R1]
```

- El código en Assembly:

```
    @1
    A=M
    D=M
    @4
    M=D
```

15. Implementa en ensamblador el siguiente problema. En la posición R0 está almacenada la dirección inicial de una región de memoria. En la posición R1 está almacenado el tamaño de la región de memoria. Almacena un -1 en esa región de memoria.
   - El problema en assembly:
```
    @R0
    D=M
    @R2
    M=0
    @R2
    D=M
    @R1
    D=D-A
    @end_loop
    D;JEQ
    @R0
    D=M
    @R2
    A=D+A
    D=-1
    M=D
    @R2
    M=M+1
    @loop
    0;JMP
```

16. Implementa en lenguaje ensamblador el siguiente programa:
```
int[] arr = new int[10];
int sum = 0;
for (int j = 0; j < 10; j++) {
    sum = sum + arr[j];
}
```

- El código en ensamblador:
```
@0
M=0
@1
M=0
@2
M=0
@3
M=0
@4
M=0
@5
M=0
@6
M=0
@7
M=0
@8
M=0
@9
M=0
@sum
M=0
@j
M=0
(LOOP)
@j
D=M
@10
D=D-A
@END
D;JGE
@j
D=M
@arr
A=D+A
D=M
@sum
M=M+D
@j
M=M+1
@LOOP
0;JMP
(END)
```

- ¿Qué hace este programa?: Es una suma de diez elementos que se guarda en @sum.
- ¿Cuál es la dirección base de arr en la memoria RAM?: Comienza en @0.
- ¿Cuál es la dirección base de sum en la memoria RAM y por qué?: 
- ¿Cuál es la dirección base de j en la memoria RAM y por qué?



18. Lo que dibujé:
    ![image](https://github.com/user-attachments/assets/9fe61cdd-de32-4e2f-b2c1-2f4b2e313046)

- El código:
```
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
	M=D-A 
	D=A 
	@32
	AD=D+A
	@13060 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@11278 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@8216 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@4484 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@8770 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@13473 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@11439 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@10408 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@4166 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@8194 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@6154 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@2038 
	D=D+A 
	A=D-A 
	M=D-A 
	D=A 
	@32
	AD=D+A
	@2 
	D=D+A 
	A=D-A 
	M=D-A 
	@R13
	A=M
	D;JMP
```

19. Analiza el siguiente programa en lenguaje de máquina:
```
0100000000000000
1110110000010000
0000000000010000
1110001100001000
0110000000000000
1111110000010000
0000000000010011
1110001100000101
0000000000010000
1111110000010000
0100000000000000
1110010011010000
0000000000000100
1110001100000110
0000000000010000
1111110010101000
1110101010001000
0000000000000100
1110101010000111
0000000000010000
1111110000010000
0110000000000000
1110010011010000
0000000000000100
1110001100000011
0000000000010000
1111110000100000
1110111010001000
0000000000010000
1111110111001000
0000000000000100
1110101010000111
```
- ¿Qué hace este programa?: Parece ser una suma acumulativa de varias cifras.

20. Implementa un programa en lenguaje ensamblador que dibuje el bitmap que diseñaste en la pantalla solo si se presiona la tecla “d”:


