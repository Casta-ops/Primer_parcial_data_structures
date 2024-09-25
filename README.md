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

1. Para cada uno de los vectores especifique cuál es su capacidad final y el desperdicio en
el que incurre.
2. Cuál de los vectores resultó ser más eficiente a la hora de ejecutar el programa?
Justifique clara y concisamente su respuesta.

2. Si comparamos el vector con una lista enlazada como la implementada en el curso cree
usted que la lista pueda ser más eficiente?. Justifique su respuesta.

RE // Depende de las necesidades que tengamos, realmente esa respuesta se encuentra conforme a los aspectos
y condiciones que tengamos a la hora de programar. Mientras que los Vectores nos facilitan el ordenamiento 
de la estructura, las Listas nos permiten controlar de manera mas factible los elementos en relación 
a su remoción e introducción, ya que no es necesario hacer un resize cada vez que se introducen nuevos elementos,
solo es imperativo incrementar su tamaño. Entonces esta respuesta es un poco ambigua, pero no podemos conocer la
verdadera eficiencia de cada estructura con respecto 

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

#include <iostream>
#include <vector>
#include <list>
#include <algorithm>

class AdjacencyList {
private:
    struct Node {
        int city;
        Node* next;
        Node(int c) : city(c), next(nullptr) {}
    };

    std::vector<Node*> adjList;

public:
    // Constructor para inicializar la lista de adyacencia con un número dado de ciudades
    AdjacencyList(int numCities) {
        adjList.resize(numCities, nullptr);
    }

    // Método para adicionar una conexión entre dos ciudades
    void addEdge(int city1, int city2) {
        Node* newNode1 = new Node(city2);
        newNode1->next = adjList[city1];
        adjList[city1] = newNode1;

        Node* newNode2 = new Node(city1);
        newNode2->next = adjList[city2];
        adjList[city2] = newNode2;
    }

    // Método para remover una conexión entre dos ciudades
    void removeEdge(int city1, int city2) {
        adjList[city1] = removeNode(adjList[city1], city2);
        adjList[city2] = removeNode(adjList[city2], city1);
    }

    // Método para obtener las ciudades conectadas a una ciudad dada
    std::list<int> getConnectedCities(int city) {
        std::list<int> connectedCities;
        Node* current = adjList[city];
        while (current) {
            connectedCities.push_back(current->city);
            current = current->next;
        }
        return connectedCities;
    }

    // Método para adicionar una ciudad (incrementa el tamaño del vector)
    void addCity() {
        adjList.push_back(nullptr);
    }

    // Método para remover una ciudad (elimina todas las conexiones con esa ciudad)
    void removeCity(int city) {
        for (auto& head : adjList) {
            head = removeNode(head, city);
        }
        adjList.erase(adjList.begin() + city);
        // Ajustar las conexiones restantes
        for (auto& head : adjList) {
            Node* current = head;
            while (current) {
                if (current->city > city) {
                    current->city--;
                }
                current = current->next;
            }
        }
    }

    // Método para imprimir la lista de adyacencia (para depuración)
    void printAdjList() {
        for (int i = 0; i < adjList.size(); ++i) {
            std::cout << "Ciudad " << i << ": ";
            Node* current = adjList[i];
            while (current) {
                std::cout << current->city << " ";
                current = current->next;
            }
            std::cout << std::endl;
        }
    }

private:
    // Método auxiliar para remover un nodo de la lista
    Node* removeNode(Node* head, int city) {
        if (!head) return nullptr;
        if (head->city == city) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return head;
        }
        Node* current = head;
        while (current->next && current->next->city != city) {
            current = current->next;
        }
        if (current->next) {
            Node* temp = current->next;
            current->next = current->next->next;
            delete temp;
        }
        return head;
    }
};

int main() {
    AdjacencyList network(6);

    network.addEdge(0, 1);
    network.addEdge(0, 4);
    network.addEdge(0, 5);
    network.addEdge(1, 2);
    network.addEdge(1, 3);
    network.addEdge(4, 5);

    network.printAdjList();

    std::cout << "Ciudades conectadas con la ciudad 1: ";
    for (int city : network.getConnectedCities(1)) {
        std::cout << city << " ";
    }
    std::cout << std::endl;

    network.removeEdge(0, 1);
    network.printAdjList();

    network.addCity();
    network.addEdge(6, 2);
    network.printAdjList();

    network.removeCity(1);
    network.printAdjList();

    return 0;
}

