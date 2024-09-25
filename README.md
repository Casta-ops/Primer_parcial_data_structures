Nombre: Santiago Castañeda Pérez
Codigo: 1128904431

# Primer_parcial_data_structures

# Pregunta 1

La clase vector implementa lo que se conoce como un arreglo dinámico. Es decir, en parte
se comporta como un arreglo pero extiende la funcionalidad de los arreglos permitiendo que la
estructura de datos crezca o se contraiga de acuerdo a su uso. Responda las siguientes
preguntas respecto a la estructura de datos vector.

1. Por qué es necesario hacer resize del vector cuando este se llena y es necesario seguir
almacenando elementos?. A caso no sería una mejor opción apartar un espacio en
memoria para seguir almacenando los elementos que se van a insertar en el futuro así se
deba llevar registro dentro de la clase de que los elementos del vector pueden estar
almacenados en diferentes lugares de la memoria?

RE // Esto se debe a que la estructura Vector implementa los elementos de su arreglo de
manera consecutiva en la memoria, hacer resize es fundamental para poder seguir con su
proceso, ya que todo aquel elemento que se aloje por fuera de la capacidad del arreglo se
puede llegar a perder en la memoria, por lo tanto el arreglo no llegaria a conocer su posición,
si deseamos utilizar distintos espacios en la memoria, en ese caso lo mas factible sería 
utilizar listas. Las listas nos permiten utilizar nodos a diferentes lugares de la memoria sin perder
o desconocer la ubicación de cada elemento dentro de la estructura.

2. Si comparamos el vector con una lista enlazada como la implementada en el curso cree
usted que la lista pueda ser más eficiente?. Justifique su respuesta.

RE // Depende de las necesidades que tengamos, realmente esa respuesta se encuentra conforme a los aspectos
y condiciones que tengamos a la hora de programar. Mientras que los Vectores nos facilitan el ordenamiento 
de la estructura, las Listas nos permiten controlar de manera mas factible los elementos en relación 
a su remoción e introducción, ya que no es necesario hacer un resize cada vez que se introducen nuevos elementos,
solo es imperativo incrementar su tamaño. Entonces esta respuesta es un poco ambigua, pero no podemos conocer la
verdadera eficiencia de cada estructura a no ser que tengamos presentes cada una de nuestras necesidades a la hora
de programar, y las del usuario claramente.

# Pregunta 2

Considere el siguiente programa:

int main() {
  Vector<int> x;
  Vector<int> y(10,1.8);
  Vector<int> z(100, 2.0);
  for (unsigned int i = 0; i < 10000; i++) {
    x.push_back(i);
    y.push_back(i);
    z.push_back(i);
  }
  return 0;
}

El vector x es construido (línea 2) utilizando el constructor por defecto que tiene una
capacidad inicial de 5 y una política de crecimiento de 2.0. Es decir, cada que se redimensiona
se solicita memoria para un arreglo del doble de los elementos que se almacenan hasta ese
momento. El vector y se construye (línea 3) con 10 elementos de capacidad inicial y una
política de crecimiento de 1.8. Por último el vector z es inicializado (línea 4) con una capacidad
inicial de 100 elementos y una política de crecimiento de 2.0.

1. Para cada uno de los vectores especifique cuál es su capacidad final y el desperdicio en
el que incurre.

Vector(x) -> 2.0(1 -> 10, 2 -> 20, 3 -> 40, 4 -> 80, 5 -> 160, 6 -> 320, 7 -> 640, 8 -> 1280, 9 -> 2560, 10 -> 5120, 11 -> 10240)
Capacidad final (x) -> 10240
Vector(y) -> 1.8(1 -> 18, 2 -> 32, 3 -> 58, 4 -> 104, 5 -> 188, 6 -> 340, 7 -> 612, 8 -> 1101, 9 -> 1983, 10 -> 3570, 11 -> 6426, 12 -> 11568)
Capacidad final (y) -> 11568
Vector(z) -> 2.0(1 -> 200, 2 -> 400, 3 -> 800, 4 -> 1600, 5 -> 3200, 6 -> 6400, 7 -> 12800)
Capacidad final (z) -> 12800

RE // Cuando hablamos de desperdicio con respecto a la memoria cuando recurrimos a la politica de crecimiento, 
podemos tener en cuenta dos grandes aspectos, el primero es la cantidad de procesos que se ejecutan a partir
de resize en relación a cada uno de los vectores, y el segundo aspecto es la cantidad de posiciones que desperdiciamos
a partir de ese crecimiento del arreglo. El Vector(y) es la estructura que mas recurre a esta politica, pues ejecuta 12
procesos que resultan mas costosos con respecto a los otros dos vectores, adicional a los casi 2000 posiciones que no se utilizan
conforme al ciclo de inserción que se indica en el main, sin embargo, puede resultar beneficioso para el programa a largo plazo,
pues duplicar el size llega a ser más costoso con una inserción de muchos mas elementos, la politica de crecimiento de (1.8) del
Vector (y) limita ese rango de crecimiento a una cantidad mas pequeña y considerable dentro del programa. Con respecto al Vector (x)
Podemos tener en cuenta la consideración de que ejecuta casi que la misma cantidad de resize que el Vector anterior, sin embargo
desperdicia muchos menos elementos conforme al crecimiento de su tamaño. Aun asi el Vector (z) es la estructura que más recurre al
desperdicio de memoria, ocupando posiciones que aun no han sido abarcadas por el ciclo de inserción, con alrededor de 3000 posiciones
sin ocupar, pero este Vector tiene la facilidad de ocupar mucho menos la politica de crecimiento con pocos resize ejecutados.

2. Cuál de los vectores resultó ser más eficiente a la hora de ejecutar el programa?
Justifique clara y concisamente su respuesta.

RE // Teniendo en cuenta que el resize permite crear un nuevo arreglo, que copia los elementos del arreglo original 
(liberandose a memoria) con su nuevo tamaño gracias a la politica de crecimiento, podemos visualizar que este proceso
resulta costoso cuando se ejecuta una gran cantidad de veces, por esa razón el Vector(z) es el más eficiente, pues con solo
7 resize permite abarcar el ciclo de inserción, sin embargo... este Vector esta desperdiciando las casi 3000 posiciones en memoria
que no esta ocupando, lo cual a largo plazo puede resultar poco optimo por su politica de crecimiento de (2.0), 
por esa razón mi respuesta seria la siguiente.
  a. Vector que menos proceso ejecuta (eficiencia): Vector (z)
  b. Vector que menos posiciones desperdicia: Vector (x)
  c. Vector que a largo plazo resulta optimo: Vector (y)


# Pregunta 3;

Se cuenta con la siguiente representación de una red de transporte. Los círculos representan
ciudades y las líneas representan conexiones entre ellas. Pro ejemplo, la ciudad representada
por 0 se encuentra conectada con las ciudades 1, 4 y 5.

En este punto usted deberá crear la estructura de datos AdjacencyList para representar
redes de transporte de forma general. Es decir, con un número arbitrario de ciudades y con
conexiones arbitrarias entre las mismas. Tenga en cuenta que las ciudades siempre se
representan con números consecutivos que comienzan desde cero. Además es importante
notar que no todas las ciudades están conectadas entre si.

1. Proponga una implementación en C++ de la clase AdjacencyList , defina
apropiadamente sus atributos y sus operaciones. Usted puede utilizar para esto
cualquiera de las estructuras de datos discutidas en clase.

2. Cree operaciones para adicionar y remover ciudades.

3. Cree una operación que dada una ciudad retorne las ciudades que se encuentran
conectadas con esta.

```c++

#include <iostream>

class Adjacency_List {
private:
    class Node {
    private:
        int city;
        Node* next;
    public:
        // constructor que inicializa la ciuddad en 0;
        Node() : city(0), next(nullptr) {}
        Node(unsigned int c) : city(c), next(nullptr) {}
        int getCity() const {
            return city;
        }
        Node* getNext() const {
            return next
        }
        void setNext(Node* nextNode) {
            next = nextNode;
        }
    };
    private:
    Node** AList;
    int city_size
public:
    Adjacency_List(unsigned int numCities) : city_size(numCities) {
        AList = new Node*[numCities];
        for (int i = 0; i < numCities; ++i) {
            AList[i] = nullptr;
        }
    }

    ~Adjacency_List() {
        for (int i = 0; i < city_size; ++i) {
            Node* current = AList[i];
            while (curent) {
                Node* temp = current;
                current = current->getNext();
                delete temp;
            }
        }
        deletea] AListu
    }


    void add_conection(unsigned int city1, unsigned int city2) {
        Node* newNode1 = new Node(city2);
        newNde1->setNext(AList[city1]);
        AList[city1] = newNod;
        Node* newNode2 = new Node(city1;
        newNode2->stNext(AList[city2]);
        AList[city2] = newNode2
    }

    void remove_conection(int city1, int city2) {
        AList[city1] = removeNode(AList[city1], city2);
        AList[city2] = reoveNode(AList[city2], city1);
    }

    void get_connected(int city) const {
        Noe* current = AList[city];
        while (current) {
            cout << current->getCity() << " ";
            current = current->getNext();
        }
        std::cout << std::endl;
    }
    void add_city() {
        Node** new_AList = new Node*[city_size + 1];
        for (int i = 0; i < city_size; ++i) {
            new_AList[i] = AList[i];
        }
        new_AList[city_size] = nullptr;
        delete[] AList;
        AList = new_AList
        city_size+;
    }

    void remove_city(int city) {
        for (int i = 0; i < city_size; ++i) {
            AList[i] = removeNode(AList[i], city);
        }
        for (int i = city; i < city_size - 1; ++i) {
            AList[i] = AList[i + 1
        }
        AList[city_size - 1] = nllptr;
        city_size--;
    }


private:
    Node* removeNode(Node* head, int city) {
        if (!head) return nullptr;
        if (head->getCity() == city) {
            Node* temp = head;
            head = head->getNext();
            delete temp;
            retun head;
        }
        Node* current = head;
        while (current->getNext() && current->getNext()->getCity() != city) {
            current = current->getNext()
        }
        if (current->getNext()) {
            Node* temp = current->getNext();
            current->setNext(current->getNext()->getNext());
            delaxe temp;
        }

        return head;
    }
};
```c
