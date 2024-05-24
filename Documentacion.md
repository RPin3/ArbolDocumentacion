# Documentacion Arbol
## Alan Albino Tellez Giron Lizarraga
### Tree.h
```c++
#ifndef TREE_H
#define TREE_H
```
Estas lineas son directivas de preprocesador. #ifndef significa "if not defined" y 'TREE.H' es un identificador
unico que se usa como guardia de inclusion para evitar la inclusion multiple del mismo archivo de encabezado.
Si TREE_H no esta definido el preprocesador incluira el contenido del archivo; de lo contrario, lo omite.

```c++
#include <iostream>
```
Esta linea incluye la biblioteca de entrada y salida estandar de C++.
```c++
template <typename T>
class Node {
public:
    T data;
    Node* firstChild;
    Node* nextSibling;

    explicit Node(T data);
};
```
Aqui se define la clase Node. Esta clase representa un nodo en una estructura de arbol.
```c++
template <typename T>
```
Esta línea indica que la clase Node es una plantilla de clase parametrizada por un tipo T
```c++
class Node{
    T data;
    Node* firstChild;
    Node* nextSibling;
};
```
Define la clase Node
```c++
T data;
```
Un miembro de datos de tipo T que almacena el valor del nodo.
```c++
firstChild
```
Un puntero Node que apunta al primer hijo del nodo
```c++
nextSibling
```
Un puntero Node que apnuta al siguiente hijo del nodo
```c++
explicit Node(T data);
```
Este es el constructor de la clase Node. Toma un parámetro data de tipo T y lo utiliza para inicializar
el miembro de datos data
```c++
template <typename T>
class Tree {
public:
    Node<T>* root;

    Tree();

    Node<T>* addNode(T data, Node<T>* parent = nullptr);

    void printTree(Node<T>* node, int level = 0);
};
```
En este bloque de codigo se define una plantilla de clase Tree, que representa una 
estructura de arbol
```c++
template <typename T>
```
Esta línea indica que la clase Node es una plantilla de clase parametrizada por un tipo T
```c++
class Tree {
public:
    Node<T>* root;

    Tree();

    Node<T>* addNode(T data, Node<T>* parent = nullptr);

    void printTree(Node<T>* node, int level = 0);
};
```
Este bloque de codigo define la clase Tree, que representa una estructura de árbol genérica. 
Los miembros de la clase son:
```c++
Node<T>* root
```
Un puntero a un objeto tipo Node T que representa el nodo raiz de un arbol
```c++
Tree();
```
Es el constructor predeterminado de la clase Tree
```c++
Node<T>* addNode(T data, Node<T>* parent = nullptr)
```
Esta funcion se usa para agregar un nuevo nodo al arbol. Toma 2 parametros data que representan el valor que se almacenara
en el nuevo nodo, y parent que es un puntero al nodo padre al que se va a agregar el nuevo nodo.
```c++
void printTree(Node<T>* node, int level = 0)
```
Esta función se utiliza para imprimir el árbol en la consola.

### Tree.cpp
```c++
#include "Tree.h"


template <typename T>
Node<T>::Node(T data) : data(data), firstChild(nullptr), nextSibling(nullptr) {}

template <typename T>
Tree<T>::Tree() : root(nullptr) {}

template <typename T>
Node<T>* Tree<T>::addNode(T data, Node<T>* parent) {
    Node<T>* newNode = new Node<T>(data);

    if(parent) {
        if(parent->firstChild) {
            Node<T>* sibling = parent->firstChild;
            while(sibling->nextSibling) {
                sibling = sibling->nextSibling;
            }
            sibling->nextSibling = newNode;
        } else {
            parent->firstChild = newNode;
        }
    } else {
        root = newNode;
    }

    return newNode;
}

template <typename T>
void Tree<T>::printTree(Node<T>* node, int level) {
    if(!node) return;

    for(int i = 0; i < level; i++) std::cout << "--";
    std::cout << node->data << '\n';

    printTree(node->firstChild, level + 1);
    printTree(node->nextSibling, level);
}
```
Este fragmento de codigo implementa las funciones miembros de las clases Node y Tree. 
```c++
template <typename T>
Node<T>::Node(T data) : data(data), firstChild(nullptr), nextSibling(nullptr) {}
```
Este constructor inicializa un nodo con el dato proporcionado y establece los punteros firstChild y nextSibling como nulos.
```c++
template <typename T>
Tree<T>::Tree() : root(nullptr) {}
```
Este constructor inicializa un árbol estableciendo el puntero root como nulo.
```c++
template <typename T>
Node<T>* Tree<T>::addNode(T data, Node<T>* parent) {
    Node<T>* newNode = new Node<T>(data);

    if(parent) {
        if(parent->firstChild) {
            Node<T>* sibling = parent->firstChild;
            while(sibling->nextSibling) {
                sibling = sibling->nextSibling;
            }
            sibling->nextSibling = newNode;
        } else {
            parent->firstChild = newNode;
        }
    } else {
        root = newNode;
    }

    return newNode;
}
```
Este bloque de codigo agrega un nuevo nodo al arbol, Si se proporciona un nodo padre, el nuevo nodo se agrega como un
hijo o hermano del nodo padre, segun corresponda.  
En el caso en que no se de un nodo padre el nodo se agregara como raiz del arbol. La funcion devuelve el nuevo nodo.

```c++
template <typename T>
Node<T>* Tree<T>::addNode(T data, Node<T>* parent) {
```
Esta linea indica que la funcion addNode es una funcion miembro de la clase Tree, que esta parametrizada por un tipo T.
Toma 2 argumentos data que es el dato que se almacenara en el nuevo nodo, y parent que es un puntero al nodo padre al que
se va a agregar el nuevo nodo.

```c++
Node<T>* newNode = new Node<T>(data);
```
Esta linea crea un nuevo nodo utilizando el constructor de la clase Node.
```c++
if(parent) {
```
Esta linea verifica si se proporciono un nodo padre
```c++
        if(parent->firstChild) {
            Node<T>* sibling = parent->firstChild;
            while(sibling->nextSibling) {
                sibling = sibling->nextSibling;
            }
            sibling->nextSibling = newNode;
        } else {
            parent->firstChild = newNode;
        }
```
Este bloque de codigo dentro de la funcion addNode se encarga de agregar el nuevo nodo como hermano siguiente del ultimo
hijo del nodo padre
```c++
if(parent->firstChild) {
```
Esta condicion verifica si el nodo padre tiene al menos 1 hijo, parent->firstChild es un puntero al primer hijo del nodo padre
```c++
Node<T>* sibling = parent->firstChild;
```
Se declara un puntero sibling que se inicializa con el puntero al primer hijo del nodo padre. 
```c++
while(sibling->nextSibling) {
    sibling = sibling->nextSibling;
}
```
Se utiliza un buvle while para recorrer la lista de hermanos del nodo padre. El bucle continua hasta que el puntero
nextSibling del nodo actual sea nulo, lo que significa que no hay hermano siguiente. En cvada iteracion del bucle sibling
se actualiza para que se apunte al siguiente hermano en la lista.
```c++
    sibling->nextSibling = newNode;
```
Una vez que se encuentra el último hermano del nodo padre, se establece el puntero nextSibling de ese nodo para que
apunte al nuevo nodo
```c++
} else {
    parent->firstChild = newNode;
}
```
Si el nodo padre no tiene ningún hijo, significa que el nuevo nodo será el primer hijo del nodo padre. 
```c++
template <typename T>
void Tree<T>::printTree(Node<T>* node, int level) {
    if(!node) return;

    for(int i = 0; i < level; i++) std::cout << "--";
    std::cout << node->data << '\n';

    printTree(node->firstChild, level + 1);
    printTree(node->nextSibling, level);
}
```
Este fragmento de codigo implementa la funcion printTree para imprimir el arbol en la consola

```c++
template <typename T>
void Tree<T>::printTree(Node<T>* node, int level) {
```
Esta línea indica que la función printTree es una función miembro de la clase Tree y toma dos parámetros: node, que es 
un puntero al nodo raíz del subárbol que se va a imprimir, y level, que indica el nivel de profundidad del nodo en el 
árbol y se utiliza para formatear la salida.
```c++
    if(!node) return;
```
Esta linea revisa si el nodo pasado como argumento es nulo

```c++
    for(int i = 0; i < level; i++) std::cout << "--";
    std::cout << node->data << '\n';
```
Este bloque imprime el valor del nodo actual con guiones para saber la profundidad del nodo en el arbol.
```c++
    printTree(node->firstChild, level + 1);
    printTree(node->nextSibling, level);
```
Estas líneas son llamadas recursivas a la función printTree para imprimir los hijos y hermanos del nodo actual.
node->firstChild es un puntero al primer hijo del nodo actual, por lo que la función printTree se llama recursivamente
para imprimir el subárbol que comienza en ese hijo