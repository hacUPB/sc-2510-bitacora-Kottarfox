# Investigación
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

10. Las posiciones de memoria RAM de 0 a 15 tienen los nombres simbólico R0 a R15. Escribe un programa en lenguaje ensamblador que guarde en R1 la operación 2 * R0.
```
@R0    
D=M   
@R1   
D=D+D  
M=D
```

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
