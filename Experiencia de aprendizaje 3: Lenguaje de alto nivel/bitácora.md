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
Encontré una forma para arreglarlo, esta seria que tiene que estar un evento que sea un mouseReleased()
En ofApp.h puse esto:
```
void mouseReleased(int x, int y, int button); // Declaración de la función
```
y en ofApp.cpp esto
```
//--------------------------------------------------------------
void ofApp::mouseReleased(int x, int y, int button){
    if (button == OF_MOUSE_BUTTON_LEFT){
        selectedSphere = nullptr;
    }
}
```

### Actividad 7
Especificamente pasa esto, se crea un objeto en stack.
![image](https://github.com/user-attachments/assets/63cfd7fa-c844-4053-ae9a-2f6b94ad8eef)

Ahora con el cambio en el código, se crearía el objeto con heap y no destruiría automaticamente cuando la función termine entonces el puntero sigue funcionando después de que se pase de la función

- ¿Por que pasa esto?
  Pasa por que hay unas diferencias entre el Stack y Heap:
  - Stack: almacenamiento temporal. Se libera automáticamente al salir del bloque de función.
  - Heap: almacenamiento dinámico. Permanece hasta que tú lo liberes explícitamente con delete.
 
Lo que pasaba originalmente era que globalVector iba a una zona de memoria que ya no tenia la instancia original entonces iba a causar hasta un crasheo después de.

### Actividad 8
Para ofApp.h:
```
#pragma once
#include "ofMain.h"

class Sphere {
public:
    Sphere(float x, float y, float radius);
    void draw() const;

    float x, y;
    float radius;
    ofColor color;
};

// Memoria global
extern Sphere globalSphere;

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);

private:
    // Heap
    std::vector<Sphere*> heapSpheres;

    // Stack 
    Sphere* stackSpherePtr = nullptr;

    void createHeapSphere();
    void drawStackSphere(); // se crea y dibuja durante cada llamada a draw
};
```

Para ofApp.cpp:
```
#include "ofApp.h"

// Memoria global
Sphere globalSphere(100, 100, 30);

// Constructor
Sphere::Sphere(float x, float y, float radius)
    : x(x), y(y), radius(radius) {
    color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Sphere::draw() const {
    ofSetColor(color);
    ofDrawCircle(x, y, radius);
}

void ofApp::setup() {
    ofBackground(0);
}

void ofApp::update() {}

void ofApp::draw() {
    ofDrawBitmapStringHighlight("Presiona: 'g' (global), 'h' (heap), 's' (stack)", 20, 20);

    // Global
    globalSphere.draw();

    // Heap
    for (auto s : heapSpheres) {
        s->draw();
    }

    // Stack
    drawStackSphere(); 
}

void ofApp::keyPressed(int key) {
    if (key == 'h') {
        createHeapSphere();
    } else if (key == 'g') {
        globalSphere.x = ofRandomWidth();
        globalSphere.y = ofRandomHeight();
    }
}

// Crea una esfera en el heap
void ofApp::createHeapSphere() {
    Sphere* newSphere = new Sphere(ofRandomWidth(), ofRandomHeight(), 20);
    heapSpheres.push_back(newSphere);
}

// Crea y dibuja una esfera en el stack 
void ofApp::drawStackSphere() {
    Sphere stackSphere(ofRandomWidth(), ofRandomHeight(), 15);
    stackSphere.draw();
}

```
- ¿Cuando creo objetos en Heap y cuando en la memoria global?
**En el heap:**
- La vida útil del objeto no está limitada a una función.
Ejemplo: quieres que el objeto exista mientras el programa corre, aunque se haya creado dentro de keyPressed() u otra función.

- No sabes cuántos objetos necesitas.
Ejemplo: el usuario puede crear esferas dinámicamente (como presionando una tecla).

- Los objetos son muy grandes y ocuparían mucho espacio en el stack.
Ejemplo: arrays o imágenes grandes.

- Trabajas con polimorfismo o necesitas punteros.
Por ejemplo: std::vector<Base*> objetos; donde los objetos son instancias de clases derivadas.

**En la memoria global:**
- Necesitas un objeto que esté disponible desde cualquier parte del programa.
Ejemplo: configuración global del juego, constantes compartidas.

- El objeto debe existir durante toda la ejecución.
Ejemplo: un estado general del juego, una esfera de referencia, un logger.

- No quieres pasar el objeto por parámetro muchas veces.
Aunque esto puede ser una mala práctica si se abusa.

### Actividad 9
Aquí el analisis de que pasa cuando presionas la letra f (lo hice línea por línea para entender mejor):

- **if(!heapObjects.empty())**
    - Verifica que el vector heapObjects no esté vacío.
    - Esto evita intentar borrar un puntero nulo o acceder a un elemento inexistente.

- **delete heapObjects.back();**
    - Libera la memoria del último objeto creado en el heap.
    - heapObjects.back() devuelve un puntero al último ofVec2f en el vector.
    - Con delete, se destruye ese objeto de la memoria dinámica.

- **heapObjects.pop_back();**
    - Elimina el puntero del vector (ya apuntaba a memoria liberada).


### Reto
Para poner en ofApp.h
```
#pragma once
#include "ofMain.h"

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);
    void mousePressed(int x, int y, int button);

    void convertMouseToRay(int mouseX, int mouseY, glm::vec3& rayStart, glm::vec3& rayEnd);
    bool rayIntersectsSphere(const glm::vec3& rayStart, const glm::vec3& rayDir, const glm::vec3& sphereCenter, float sphereRadius, glm::vec3& intersectionPoint);

private:
    std::vector<glm::vec3> spherePositions;
    glm::vec3 selectedSpherePos;
    bool sphereSelected = false;

    float xStep = 60.0f;
    float yStep = 60.0f;
    float distDiv = 100.0f;
    float amplitud = 100.0f;

    ofEasyCam cam;
};
```

Para ofApp.h
```
#include "ofApp.h"

void ofApp::setup() {
    ofBackground(0);
    float width = ofGetWidth();
    float height = ofGetHeight();

    for (float x = -width / 2; x < width / 2; x += xStep) {
        for (float y = -height / 2; y < height / 2; y += yStep) {
            float z = cos(ofDist(x, y, 0, 0) / distDiv) * amplitud;
            spherePositions.emplace_back(x, y, z);
        }
    }
}

void ofApp::update() {}

void ofApp::draw() {
    cam.begin();

    for (auto& pos : spherePositions) {
        if (sphereSelected && pos == selectedSpherePos) {
            ofSetColor(255, 0, 0); // roja si está seleccionada
        } else {
            ofSetColor(0, 0, 255); // azul normal
        }
        ofDrawSphere(pos, 5);
    }

    if (sphereSelected) {
        ofSetColor(255);
        ofDrawBitmapString("Selected Sphere: (" +
                           ofToString(selectedSpherePos.x) + ", " +
                           ofToString(selectedSpherePos.y) + ", " +
                           ofToString(selectedSpherePos.z) + ")",
                           selectedSpherePos.x + 10, selectedSpherePos.y + 10);
    }

    cam.end();
}

void ofApp::keyPressed(int key) {
    if (key == OF_KEY_UP) amplitud += 10;
    else if (key == OF_KEY_DOWN) amplitud -= 10;
    else if (key == OF_KEY_LEFT) distDiv -= 5;
    else if (key == OF_KEY_RIGHT) distDiv += 5;
    else if (key == '+') xStep += 5, yStep += 5;
    else if (key == '-') xStep -= 5, yStep -= 5;

    // Regenerar las esferas con los nuevos parámetros
    spherePositions.clear();
    float width = ofGetWidth();
    float height = ofGetHeight();

    for (float x = -width / 2; x < width / 2; x += xStep) {
        for (float y = -height / 2; y < height / 2; y += yStep) {
            float z = cos(ofDist(x, y, 0, 0) / distDiv) * amplitud;
            spherePositions.emplace_back(x, y, z);
        }
    }
}

void ofApp::mousePressed(int x, int y, int button) {
    glm::vec3 rayStart, rayEnd;
    convertMouseToRay(x, y, rayStart, rayEnd);

    sphereSelected = false;
    for (auto& pos : spherePositions) {
        glm::vec3 intersectionPoint;
        if (rayIntersectsSphere(rayStart, rayEnd - rayStart, pos, 5.0, intersectionPoint)) {
            selectedSpherePos = pos;
            sphereSelected = true;
            break;
        }
    }
}

void ofApp::convertMouseToRay(int mouseX, int mouseY, glm::vec3& rayStart, glm::vec3& rayEnd) {
    glm::mat4 modelview = cam.getModelViewMatrix();
    glm::mat4 projection = cam.getProjectionMatrix();
    ofRectangle viewport = ofGetCurrentViewport();

    float x = 2.0f * (mouseX - viewport.x) / viewport.width - 1.0f;
    float y = 1.0f - 2.0f * (mouseY - viewport.y) / viewport.height;

    glm::vec4 rayStartNDC(x, y, -1.0f, 1.0f);
    glm::vec4 rayEndNDC(x, y, 1.0f, 1.0f);

    glm::vec4 rayStartWorld = glm::inverse(projection * modelview) * rayStartNDC;
    glm::vec4 rayEndWorld = glm::inverse(projection * modelview) * rayEndNDC;

    rayStartWorld /= rayStartWorld.w;
    rayEndWorld /= rayEndWorld.w;

    rayStart = glm::vec3(rayStartWorld);
    rayEnd = glm::vec3(rayEndWorld);
}

bool ofApp::rayIntersectsSphere(const glm::vec3& rayStart, const glm::vec3& rayDir, const glm::vec3& sphereCenter, float sphereRadius, glm::vec3& intersectionPoint) {
    glm::vec3 oc = rayStart - sphereCenter;

    float a = glm::dot(rayDir, rayDir);
    float b = 2.0f * glm::dot(oc, rayDir);
    float c = glm::dot(oc, oc) - sphereRadius * sphereRadius;

    float discriminant = b * b - 4 * a * c;

    if (discriminant < 0) {
        return false;
    } else {
        float t = (-b - sqrt(discriminant)) / (2.0f * a);
        intersectionPoint = rayStart + t * rayDir;
        return true;
    }
}
```

**Documentación:**
Aquí pasé por mucha prueba y error, tuve que bajarle a la cantidad de esferas en pantalla debido a que si habían más mi computador empezaba a tirar pantalla azul. Con esto opté por hacer algo un poco más liviando y que pudiese ser más fácil de que mi computador lo procesara :D 

 1. ¿Dónde se almacenan los objetos?
   - Las posiciones de las esferas se almacenan en un std::vector<ofVec3f> spherePositions.
   - std::vector es una estructura que reserva su memoria en el heap, aunque el objeto spherePositions en sí (el contenedor) se almacena en el stack (porque es una variable miembro de ofApp, que vive en el stack).
   - Cada ofVec3f contiene 3 floats (x, y, z), por lo tanto, los datos reales (las coordenadas) también viven en el heap, gestionados automáticamente por el vector.

2. Inspección con el Depurador
Usando el depurador de Visual Studio, se puede observar:
   - El objeto spherePositions aparece en la pila (stack), dentro de la instancia de ofApp.
   - Al examinar los elementos internos (spherePositions[i]), cada uno se encuentra en una dirección de memoria separada, correspondiente al heap.
   - Variables como amplitud, distDiv, xStep, yStep, y selectedIndex también residen en el stack, porque son tipos primitivos o simples.

Link para visualizarlo: https://youtu.be/nI6LKviCehw?si=m71sPrqZsY2SA8Rg

