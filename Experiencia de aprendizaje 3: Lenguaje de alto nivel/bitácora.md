# **Investigación**
> [!IMPORTANT]
> [Página](https://confusion-snapper-025.notion.site/Experiencia-de-aprendizaje-3-Lenguaje-de-alto-nivel-17ee8161b2a1800d9be4c7e12edd14c6) de la unidad.


### Actividad 1
- Resultado de la aplicación:
![image](https://github.com/user-attachments/assets/a0b70ad8-94f0-47b3-b1a8-c471c8fc0a5b)

Genera un ejecutable donde hay una bola blanca que sigue el cursor.

### Actividad 2
- Resultado de la aplicación:
![image](https://github.com/user-attachments/assets/5be4fa2b-0bd4-4fc7-afd4-256cceccfcfd)

- ¿Qué fue lo que incluimos en el archivo .h?: incluimos setup, update y draw. Además de las funciones de mover y el click del ratón.
- ¿Cómo funciona la aplicación?: Funciona con que uno mueva el mouse y este dejará un rastro que pasando unos segundos se borrará y que uno puede ir cambiando de color al hacer click.
- ¿Qué hace la función mouseMoved?: Registra el movimiento que uno hace con el cursor para mostrar el rastro además que hace que se borre el rastro pasando de ciertas bolas generadas.
- ¿Qué hace la función mousePressed?: Cambia de color a uno aleatorio del rastro del cursor.
- ¿Qué hace la función setup?: genera el fondo y la partícula que esta correspondida al cursor.
- ¿Qué hace la función update?: actualiza lo que se ve en pantalla.
- ¿Qué hace la función draw?: dibuja el rastro de burbujas, permite que sea visible al ejecutar la app.

### Actividad 3
Modifiqué la parte del código donde hace que se borre el trazo del cursor.

### Actividad 5
- Resultado de la aplicación:
![image](https://github.com/user-attachments/assets/a5bc724f-0ef5-4241-99bf-c4c3ac815336)


- ¿Cuál es la definición de un puntero?: El puntero en el vector spheres se utiliza para almacenar la dirección de memoria de las instancias de Sphere.

- ¿Dónde está el puntero?: El puntero está en: <Sphere*> o  Sphere* también esta en selectedsphere.
  
- ¿Cómo se inicializa el puntero?:
  Selectedsphere se inicializa en: selectedSphere = nullptr;
  y sphere en: spheres.push_back(new Sphere(x, y, radius)); 
  
- ¿Para qué se está usando el puntero?
   - Almacenar direcciones de las esferas: El puntero en el vector spheres se utiliza para almacenar la dirección de memoria de las instancias de Sphere. Esto permite tener acceso a las propiedades y métodos de las esferas sin necesidad de copiar los objetos 
    completos.

   - Seleccionar una esfera: El puntero selectedSphere se utiliza para almacenar la dirección de la esfera que ha sido seleccionada por el usuario. Esto permite que la posición de esa esfera se actualice conforme al movimiento del ratón (en el método update()), 
     mientras que las demás esferas no se afectan.

   - Actualizar y dibujar esferas: En el método update(), se usa el puntero selectedSphere para actualizar la posición de la esfera seleccionada. El puntero también se utiliza en el método draw() para dibujar todas las esferas en pantalla.
  
  
- ¿Qué es exactamente lo que está almacenado en el puntero?
   - selectedSphere: Este puntero almacena la dirección de memoria de una instancia de Sphere que ha sido seleccionada por el usuario. Inicialmente es nullptr, pero después de hacer clic sobre una esfera, almacena la dirección de la esfera seleccionada.

   - spheres: Cada elemento del vector spheres es un puntero a una instancia de Sphere. Es decir, el puntero almacena la dirección de memoria de las instancias de Sphere que se crean dinámicamente con new. Cada elemento de este vector apunta a una esfera en 
      memoria, y puedes acceder a los métodos y propiedades de esa esfera a través del puntero.v

### Actividad 6
- El error de este código es que el mouse no suelta la esfera.

### Actividad 7
Especificamente pasa esto, se crea un objeto en stack.
![image](https://github.com/user-attachments/assets/63cfd7fa-c844-4053-ae9a-2f6b94ad8eef)

