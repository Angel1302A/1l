array.cpp:

#include "array.h"
#include <iostream>

using namespace std;

// Инициализация массива
void initArray(Array& arr) {
    arr.data = nullptr; // Устанавливаем указатель на массив в nullptr
    arr.size = 0; // Устанавливаем размер массива в 0
    arr.capacity = 0; // Устанавливаем вместимость массива в 0
}

// Очистка массива
void clearArray(Array& arr) {
    delete[] arr.data; // Освобождаем память, выделенную под массив
    arr.data = nullptr; // Устанавливаем указатель на массив в nullptr
    arr.size = 0; // Устанавливаем размер массива в 0
    arr.capacity = 0; // Устанавливаем вместимость массива в 0
}

// Увеличение вместимости массива
void resizeArray(Array& arr, int newCapacity) {
    std::string* newData = new std::string[newCapacity]; // Выделяем новый массив с новой вместимостью
    for (int i = 0; i < arr.size; ++i) {
        newData[i] = arr.data[i]; // Копируем элементы из старого массива в новый
    }
    delete[] arr.data; // Освобождаем память, выделенную под старый массив
    arr.data = newData; // Устанавливаем указатель на новый массив
    arr.capacity = newCapacity; // Обновляем вместимость массива
}

// Добавление элемента в конец массива
void pushBackArray(Array& arr, const string& value) {
    if (arr.size == arr.capacity) { // Если массив заполнен
        int newCapacity = (arr.capacity == 0) ? 1 : arr.capacity * 2; // Увеличиваем вместимость
        resizeArray(arr, newCapacity); // Изменяем размер массива
    }
    arr.data[arr.size] = value; // Добавляем элемент в конец
    arr.size++; // Увеличиваем размер массива
}

// Вставка элемента по индексу
void insertArray(Array& arr, int index, const string& value) {
    if (index < 0 || index > arr.size) { // Проверка на корректность индекса
        cout << "Индекс вне диапазона" << endl;
        return;
    }

    if (arr.size == arr.capacity) { // Если массив заполнен
        int newCapacity = (arr.capacity == 0) ? 1 : arr.capacity * 2; // Увеличиваем вместимость
        resizeArray(arr, newCapacity); // Изменяем размер массива
    }

    for (int i = arr.size; i > index; --i) { // Сдвигаем элементы вправо
        arr.data[i] = arr.data[i - 1];
    }
    arr.data[index] = value; // Вставляем элемент
    arr.size++; // Увеличиваем размер массива
}

// Получение элемента по индексу
string getArray(const Array& arr, int index) {
    if (index < 0 || index >= arr.size) { // Проверка на корректность индекса
        cout << "Индекс вне диапазона" << endl;
        return "";
    }
    return arr.data[index]; // Возвращаем значение элемента
}

// Удаление элемента по индексу
void removeArray(Array& arr, int index) {
    if (index < 0 || index >= arr.size) { // Проверка на корректность индекса
        cout << "Индекс вне диапазона" << endl;
        return;
    }

    for (int i = index; i < arr.size - 1; ++i) { // Сдвигаем элементы влево
        arr.data[i] = arr.data[i + 1];
    }
    arr.size--; // Уменьшаем размер массива
}

// Замена элемента по индексу
void replaceArray(Array& arr, int index, const string& value) {
    if (index < 0 || index >= arr.size) { // Проверка на корректность индекса
        cout << "Индекс вне диапазона" << endl;
        return;
    }
    arr.data[index] = value; // Заменяем значение элемента
}

// Получение длины массива
int lengthArray(const Array& arr) {
    return arr.size; // Возвращаем размер массива
}

// Вывод массива на экран
void printArray(const Array& arr) {
    for (int i = 0; i < arr.size; ++i) { // Проходим по всем элементам массива
        cout << arr.data[i] << " "; // Выводим значение элемента
    }
    cout << endl; // Переходим на новую строку
}

array.h:

#ifndef ARRAY_H
#define ARRAY_H

#include <string>

// Структура массива
struct Array {
    std::string* data; // Указатель на динамический массив строк
    int size; // Размер массива
    int capacity; // Вместимость массива
};

// Прототипы функций для работы с массивом
void initArray(Array& arr); // Инициализация массива
void clearArray(Array& arr); // Очистка массива
void pushBackArray(Array& arr, const std::string& value); // Добавление элемента в конец массива
void insertArray(Array& arr, int index, const std::string& value); // Вставка элемента по индексу
std::string getArray(const Array& arr, int index); // Получение элемента по индексу
void removeArray(Array& arr, int index); // Удаление элемента по индексу
void replaceArray(Array& arr, int index, const std::string& value); // Замена элемента по индексу
int lengthArray(const Array& arr); // Получение длины массива
void printArray(const Array& arr); // Вывод массива на экран

#endif // ARRAY_H

singlelist.cpp:

#include "singlelist.h"
#include <iostream>

using namespace std;

// Инициализация списка
void initList(SinglyLinkedList& list) {
    list.head = nullptr; // Устанавливаем начало списка в nullptr
}

// Очистка списка
void clearList(SinglyLinkedList& list) {
    while (list.head) { // Пока есть элементы в списке
        ListNode* temp = list.head; // Сохраняем текущий элемент
        list.head = list.head->next; // Перемещаем указатель на следующий элемент
        delete temp; // Удаляем текущий элемент
    }
}

// Добавление элемента в начало списка
void pushFrontList(SinglyLinkedList& list, const string& value) {
    ListNode* newNode = new ListNode(value); // Создаем новый узел
    newNode->next = list.head; // Устанавливаем следующим элементом текущий head
    list.head = newNode; // Делаем новый узел началом списка
}

// Добавление элемента в конец списка
void pushBackList(SinglyLinkedList& list, const string& value) {
    ListNode* newNode = new ListNode(value); // Создаем новый узел
    if (!list.head) { // Если список пуст
        list.head = newNode; // Делаем новый узел началом списка
    } else {
        ListNode* current = list.head; // Начинаем с начала списка
        while (current->next) { // Ищем последний элемент
            current = current->next;
        }
        current->next = newNode; // Устанавливаем следующим элементом нового узла
    }
}

// Удаление первого элемента списка
void popFrontList(SinglyLinkedList& list) {
    if (!list.head) { // Если список пуст
        cout << "Список пуст" << endl;
        return;
    }
    ListNode* temp = list.head; // Сохраняем текущий head
    list.head = list.head->next; // Перемещаем head на следующий элемент
    delete temp; // Удаляем старый head
}

// Удаление последнего элемента списка
void popBackList(SinglyLinkedList& list) {
    if (!list.head) { // Если список пуст
        cout << "Список пуст" << endl;
        return;
    }
    if (!list.head->next) { // Если в списке только один элемент
        delete list.head; // Удаляем единственный элемент
        list.head = nullptr; // Устанавливаем начало списка в nullptr
        return;
    }
    ListNode* current = list.head; // Начинаем с начала списка
    while (current->next->next) { // Ищем элемент перед последним
        current = current->next;
    }
    delete current->next; // Удаляем последний элемент
    current->next = nullptr; // Устанавливаем следующий элемент в nullptr
}

// Удаление первого вхождения элемента со значением value
void removeList(SinglyLinkedList& list, const string& value) {
    ListNode* current = list.head; // Начинаем с начала списка
    ListNode* prev = nullptr; // Указатель на предыдущий элемент
    while (current) { // Пока есть элементы
        if (current->data == value) { // Если найден элемент с нужным значением
            if (prev) { // Если элемент не первый
                prev->next = current->next; // Перемещаем указатель на следующий элемент
            } else {
                list.head = current->next; // Если элемент первый, перемещаем head
            }
            delete current; // Удаляем элемент
            return;
        }
        prev = current; // Перемещаем указатель на текущий элемент
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << "Элемент не найден" << endl;
}

// Поиск элемента со значением value
bool findList(const SinglyLinkedList& list, const string& value) {
    ListNode* current = list.head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        if (current->data == value) { // Если найден элемент с нужным значением
            return true;
        }
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    return false;
}

// Вывод списка на экран
void printList(const SinglyLinkedList& list) {
    ListNode* current = list.head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        cout << current->data << " "; // Выводим значение элемента
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << endl; // Переходим на новую строку
}

singlelist.h:

#ifndef SINGLELIST_H
#define SINGLELIST_H

#include <string>

// Структура узла списка
struct ListNode {
    std::string data; // Данные, хранящиеся в узле
    ListNode* next; // Указатель на следующий узел
    ListNode(const std::string& value) : data(value), next(nullptr) {} // Конструктор узла
};

// Структура односвязного списка
struct SinglyLinkedList {
    ListNode* head; // Указатель на начало списка
};

// Прототипы функций для работы с односвязным списком
void initList(SinglyLinkedList& list); // Инициализация списка
void clearList(SinglyLinkedList& list); // Очистка списка
void pushFrontList(SinglyLinkedList& list, const std::string& value); // Добавление элемента в начало списка
void pushBackList(SinglyLinkedList& list, const std::string& value); // Добавление элемента в конец списка
void popFrontList(SinglyLinkedList& list); // Удаление первого элемента списка
void popBackList(SinglyLinkedList& list); // Удаление последнего элемента списка
void removeList(SinglyLinkedList& list, const std::string& value); // Удаление первого вхождения элемента со значением value
bool findList(const SinglyLinkedList& list, const std::string& value); // Поиск элемента со значением value
void printList(const SinglyLinkedList& list); // Вывод списка на экран

#endif // SINGLELIST_H

doublylist.cpp:

#include "doublylist.h"
#include <iostream>

using namespace std;

// Инициализация списка
void initList(DoublyLinkedList& list) {
    list.head = nullptr; // Устанавливаем начало списка в nullptr
    list.tail = nullptr; // Устанавливаем конец списка в nullptr
}

// Очистка списка
void clearList(DoublyLinkedList& list) {
    while (list.head) { // Пока есть элементы в списке
        DoublyNode* temp = list.head; // Сохраняем текущий элемент
        list.head = list.head->next; // Перемещаем указатель на следующий элемент
        delete temp; // Удаляем текущий элемент
    }
    list.tail = nullptr; // Устанавливаем конец списка в nullptr
}

// Добавление элемента в начало списка
void pushFrontList(DoublyLinkedList& list, const string& value) {
    DoublyNode* newNode = new DoublyNode(value); // Создаем новый узел
    if (!list.head) { // Если список пуст
        list.head = list.tail = newNode; // Делаем новый узел началом и концом списка
    } else {
        newNode->next = list.head; // Устанавливаем следующим элементом текущий head
        list.head->prev = newNode; // Устанавливаем предыдущим элементом нового узла
        list.head = newNode; // Делаем новый узел началом списка
    }
}

// Добавление элемента в конец списка
void pushBackList(DoublyLinkedList& list, const string& value) {
    DoublyNode* newNode = new DoublyNode(value); // Создаем новый узел
    if (!list.tail) { // Если список пуст
        list.head = list.tail = newNode; // Делаем новый узел началом и концом списка
    } else {
        newNode->prev = list.tail; // Устанавливаем предыдущим элементом текущий tail
        list.tail->next = newNode; // Устанавливаем следующим элементом нового узла
        list.tail = newNode; // Делаем новый узел концом списка
    }
}

// Удаление первого элемента списка
void popFrontList(DoublyLinkedList& list) {
    if (!list.head) { // Если список пуст
        cout << "Список пуст" << endl;
        return;
    }
    DoublyNode* temp = list.head; // Сохраняем текущий head
    list.head = list.head->next; // Перемещаем head на следующий элемент
    if (list.head) { // Если новый head существует
        list.head->prev = nullptr; // Устанавливаем предыдущий элемент в nullptr
    } else {
        list.tail = nullptr; // Если список стал пустым, устанавливаем tail в nullptr
    }
    delete temp; // Удаляем старый head
}

// Удаление последнего элемента списка
void popBackList(DoublyLinkedList& list) {
    if (!list.tail) { // Если список пуст
        cout << "Список пуст" << endl;
        return;
    }
    DoublyNode* temp = list.tail; // Сохраняем текущий tail
    list.tail = list.tail->prev; // Перемещаем tail на предыдущий элемент
    if (list.tail) { // Если новый tail существует
        list.tail->next = nullptr; // Устанавливаем следующий элемент в nullptr
    } else {
        list.head = nullptr; // Если список стал пустым, устанавливаем head в nullptr
    }
    delete temp; // Удаляем старый tail
}

// Удаление первого вхождения элемента со значением value
void removeList(DoublyLinkedList& list, const string& value) {
    DoublyNode* current = list.head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        if (current->data == value) { // Если найден элемент с нужным значением
            if (current->prev) { // Если элемент не первый
                current->prev->next = current->next; // Перемещаем указатель на следующий элемент
            } else {
                list.head = current->next; // Если элемент первый, перемещаем head
            }
            if (current->next) { // Если элемент не последний
                current->next->prev = current->prev; // Перемещаем указатель на предыдущий элемент
            } else {
                list.tail = current->prev; // Если элемент последний, перемещаем tail
            }
            delete current; // Удаляем элемент
            return;
        }
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << "Элемент не найден" << endl;
}

// Поиск элемента со значением value
bool findList(const DoublyLinkedList& list, const string& value) {
    DoublyNode* current = list.head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        if (current->data == value) { // Если найден элемент с нужным значением
            return true;
        }
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    return false;
}

// Вывод списка на экран
void printList(const DoublyLinkedList& list) {
    DoublyNode* current = list.head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        cout << current->data << " "; // Выводим значение элемента
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << endl; // Переходим на новую строку
}

doublylist.h:

#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <string>

// Структура узла списка
struct DoublyNode {
    std::string data; // Данные, хранящиеся в узле
    DoublyNode* next; // Указатель на следующий узел
    DoublyNode* prev; // Указатель на предыдущий узел
    DoublyNode(const std::string& value) : data(value), next(nullptr), prev(nullptr) {} // Конструктор узла
};

// Структура двусвязного списка
struct DoublyLinkedList {
    DoublyNode* head; // Указатель на начало списка
    DoublyNode* tail; // Указатель на конец списка
};

// Прототипы функций для работы с двусвязным списком
void initList(DoublyLinkedList& list); // Инициализация списка
void clearList(DoublyLinkedList& list); // Очистка списка
void pushFrontList(DoublyLinkedList& list, const std::string& value); // Добавление элемента в начало списка
void pushBackList(DoublyLinkedList& list, const std::string& value); // Добавление элемента в конец списка
void popFrontList(DoublyLinkedList& list); // Удаление первого элемента списка
void popBackList(DoublyLinkedList& list); // Удаление последнего элемента списка
void removeList(DoublyLinkedList& list, const std::string& value); // Удаление первого вхождения элемента со значением value
bool findList(const DoublyLinkedList& list, const std::string& value); // Поиск элемента со значением value
void printList(const DoublyLinkedList& list); // Вывод списка на экран

#endif // DOUBLYLIST_H

queue.cpp:

#include "queue.h"
#include <iostream>

using namespace std;

// Инициализация очереди
void initQueue(Queue& q) {
    q.front = nullptr; // Устанавливаем начало очереди в nullptr
    q.rear = nullptr; // Устанавливаем конец очереди в nullptr
}

// Очистка очереди
void clearQueue(Queue& q) {
    while (q.front) { // Пока есть элементы в очереди
        QueueNode* temp = q.front; // Сохраняем текущий элемент
        q.front = q.front->next; // Перемещаем указатель на следующий элемент
        delete temp; // Удаляем текущий элемент
    }
    q.rear = nullptr; // Устанавливаем конец очереди в nullptr
}

// Добавление элемента в конец очереди
void pushQueue(Queue& q, const string& value) {
    QueueNode* newNode = new QueueNode(value); // Создаем новый узел
    if (!q.rear) { // Если очередь пуста
        q.front = q.rear = newNode; // Делаем новый узел началом и концом очереди
    } else {
        q.rear->next = newNode; // Устанавливаем следующим элементом нового узла
        q.rear = newNode; // Делаем новый узел концом очереди
    }
}

// Удаление элемента из начала очереди
void popQueue(Queue& q) {
    if (!q.front) { // Если очередь пуста
        cout << "Очередь пуста" << endl;
        return;
    }
    QueueNode* temp = q.front; // Сохраняем текущий front
    q.front = q.front->next; // Перемещаем front на следующий элемент
    if (!q.front) { // Если очередь стала пустой
        q.rear = nullptr; // Устанавливаем конец очереди в nullptr
    }
    delete temp; // Удаляем старый front
}

// Вывод очереди на экран
void printQueue(const Queue& q) {
    QueueNode* current = q.front; // Начинаем с начала очереди
    while (current) { // Пока есть элементы
        cout << current->data << " "; // Выводим значение элемента
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << endl; // Переходим на новую строку
}

queue.h:

#ifndef QUEUE_H
#define QUEUE_H

#include <string>

// Структура узла очереди
struct QueueNode {
    std::string data; // Данные, хранящиеся в узле
    QueueNode* next; // Указатель на следующий узел
    QueueNode(const std::string& value) : data(value), next(nullptr) {} // Конструктор узла
};

// Структура очереди
struct Queue {
    QueueNode* front; // Указатель на начало очереди
    QueueNode* rear; // Указатель на конец очереди
};

// Прототипы функций для работы с очередью
void initQueue(Queue& q); // Инициализация очереди
void clearQueue(Queue& q); // Очистка очереди
void pushQueue(Queue& q, const std::string& value); // Добавление элемента в конец очереди
void popQueue(Queue& q); // Удаление элемента из начала очереди
void printQueue(const Queue& q); // Вывод очереди на экран

#endif // QUEUE_H

stack.cpp:

#include "stack.h"
#include <iostream>

using namespace std;

// Инициализация стека
void initStack(Stack& s) {
    s.top = nullptr; // Устанавливаем вершину стека в nullptr
}

// Очистка стека
void clearStack(Stack& s) {
    while (s.top) { // Пока есть элементы в стеке
        StackNode* temp = s.top; // Сохраняем текущий элемент
        s.top = s.top->next; // Перемещаем указатель на следующий элемент
        delete temp; // Удаляем текущий элемент
    }
}

// Добавление элемента в стек
void pushStack(Stack& s, const string& value) {
    StackNode* newNode = new StackNode(value); // Создаем новый узел
    newNode->next = s.top; // Устанавливаем следующим элементом текущий top
    s.top = newNode; // Делаем новый узел вершиной стека
}

// Удаление элемента из стека
void popStack(Stack& s) {
    if (!s.top) { // Если стек пуст
        cout << "Стек пуст" << endl;
        return;
    }
    StackNode* temp = s.top; // Сохраняем текущий top
    s.top = s.top->next; // Перемещаем top на следующий элемент
    delete temp; // Удаляем старый top
}

// Вывод стека на экран
void printStack(const Stack& s) {
    StackNode* current = s.top; // Начинаем с вершины стека
    while (current) { // Пока есть элементы
        cout << current->data << " "; // Выводим значение элемента
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << endl; // Переходим на новую строку
}

stack.h:

#ifndef STACK_H
#define STACK_H

#include <string>

// Структура узла стека
struct StackNode {
    std::string data; // Данные, хранящиеся в узле
    StackNode* next; // Указатель на следующий узел
    StackNode(const std::string& value) : data(value), next(nullptr) {} // Конструктор узла
};

// Структура стека
struct Stack {
    StackNode* top; // Указатель на вершину стека
};

// Прототипы функций для работы со стеком
void initStack(Stack& s); // Инициализация стека
void clearStack(Stack& s); // Очистка стека
void pushStack(Stack& s, const std::string& value); // Добавление элемента в стек
void popStack(Stack& s); // Удаление элемента из стека
void printStack(const Stack& s); // Вывод стека на экран

#endif // STACK_H

#include "hashtable.h"
#include <iostream>

using namespace std;

// Хэш-функция
unsigned int hashFunction(const string& key, int tableSize) {
    unsigned int hash = 0;
    for (char ch : key) {
        hash += ch; 
    }
    return hash % tableSize;
}

// Вставка узла в хеш-таблицу
void insertHashNode(HashNode*& head, const string& key, const string& value) {
    unsigned int index = hashFunction(key, 100);
    HashNode* current = head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        if (current->key == key) { // Если найден элемент с нужным ключом
            current->value = value; // Перезаписываем значение
            return;
        }
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    HashNode* newNode = new HashNode(key, value); // Создаем новый узел
    newNode->next = head; // Устанавливаем следующим элементом текущий head
    head = newNode; // Делаем новый узел началом списка
}

// Получение значения по ключу из хеш-таблицы
string getHashNode(HashNode* head, const string& key) {
    unsigned int index = hashFunction(key, 100);
    HashNode* current = head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        if (current->key == key) { // Если найден элемент с нужным ключом
            return current->value; // Возвращаем значение
        }
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    return "Ключ не найден"; // Если ключ не найден, возвращаем сообщение
}

// Удаление узла по ключу из хеш-таблицы
void removeHashNode(HashNode*& head, const string& key) {
    unsigned int index = hashFunction(key, 100);
    HashNode* current = head; // Начинаем с начала списка
    HashNode* prev = nullptr; // Указатель на предыдущий элемент
    while (current) { // Пока есть элементы
        if (current->key == key) { // Если найден элемент с нужным ключом
            if (prev) { // Если элемент не первый
                prev->next = current->next; // Перемещаем указатель на следующий элемент
            } else {
                head = current->next; // Если элемент первый, перемещаем head
            }
            delete current; // Удаляем элемент
            return;
        }
        prev = current; // Перемещаем указатель на текущий элемент
        current = current->next; // Перемещаем указатель на следующий элемент
    }
    cout << "Ключ не найден" << endl; // Если ключ не найден, выводим сообщение
}

// Очистка хеш-таблицы
void clearHashNode(HashNode*& head) {
    HashNode* current = head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        HashNode* temp = current; // Сохраняем текущий элемент
        current = current->next; // Перемещаем указатель на следующий элемент
        delete temp; // Удаляем текущий элемент
    }
    head = nullptr; // Устанавливаем начало списка в nullptr
}

// Вывод хеш-таблицы на экран
void printHashTable(HashNode* head) {
    HashNode* current = head; // Начинаем с начала списка
    while (current) { // Пока есть элементы
        cout << current->key << ": " << current->value << endl; // Выводим ключ и значение
        current = current->next; // Перемещаем указатель на следующий элемент
    }
}

hashtable.h:

#ifndef HASHTABLE_H
#define HASHTABLE_H

#include <string>
#include "singlelist.h"

// Структура узла хеш-таблицы
struct HashNode {
    std::string key; // Ключ
    std::string value; // Значение
    HashNode* next; // Указатель на следующий узел
    HashNode(const std::string& k, const std::string& v) : key(k), value(v), next(nullptr) {}
};

// Прототипы функций для работы с хеш-таблицей
void insertHashNode(HashNode*& head, const std::string& key, const std::string& value); // Вставка узла в хеш-таблицу
std::string getHashNode(HashNode* head, const std::string& key); // Получение значения по ключу из хеш-таблицы
void removeHashNode(HashNode*& head, const std::string& key); // Удаление узла по ключу из хеш-таблицы
void clearHashNode(HashNode*& head); // Очистка хеш-таблицы
void printHashTable(HashNode* head); // Вывод хеш-таблицы на экран
unsigned int hashFunction(const std::string& key, int tableSize); // Хеш-функция

#endif // HASHTABLE_H

tree.cpp:

#include "tree.h"
#include <iostream>

using namespace std;

// Вычисление высоты узла
int height(TreeNode* node) {
    return node ? node->height : 0; // Если узел существует, возвращаем его высоту, иначе 0
}

// Вычисление баланса узла
int getBalance(TreeNode* node) {
    return node ? height(node->left) - height(node->right) : 0; // Если узел существует, возвращаем разницу высот левого и правого поддеревьев, иначе 0
}

// Обновление высоты узла
void updateHeight(TreeNode* node) {
    node->height = max(height(node->left), height(node->right)) + 1; // Высота узла равна максимальной высоте поддеревьев плюс 1
}

// Правый поворот
TreeNode* rightRotate(TreeNode* y) {
    TreeNode* x = y->left; // Сохраняем левое поддерево y
    TreeNode* T2 = x->right; // Сохраняем правое поддерево x

    x->right = y; // Делаем y правым поддеревом x
    y->left = T2; // Делаем T2 левым поддеревом y

    updateHeight(y); // Обновляем высоту y
    updateHeight(x); // Обновляем высоту x

    return x; // Возвращаем новый корень
}

// Левый поворот
TreeNode* leftRotate(TreeNode* x) {
    TreeNode* y = x->right; // Сохраняем правое поддерево x
    TreeNode* T2 = y->left; // Сохраняем левое поддерево y

    y->left = x; // Делаем x левым поддеревом y
    x->right = T2; // Делаем T2 правым поддеревом x

    updateHeight(x); // Обновляем высоту x
    updateHeight(y); // Обновляем высоту y

    return y; // Возвращаем новый корень
}

// Вставка узла в дерево
TreeNode* insertTree(TreeNode* node, int key) {
    if (!node) { // Если узел не существует
        return new TreeNode(key); // Создаем новый узел и возвращаем его
    }

    if (key < node->key) { // Если ключ меньше ключа текущего узла
        node->left = insertTree(node->left, key); // Рекурсивно вставляем в левое поддерево
    } else if (key > node->key) { // Если ключ больше ключа текущего узла
        node->right = insertTree(node->right, key); // Рекурсивно вставляем в правое поддерево
    } else { // Если ключ уже существует
        return node; // Возвращаем текущий узел
    }

    updateHeight(node); // Обновляем высоту текущего узла

    int balance = getBalance(node); // Вычисляем баланс текущего узла

    // Проверяем и выполняем необходимые повороты для балансировки
    if (balance > 1 && key < node->left->key) {
        return rightRotate(node);
    }
    if (balance < -1 && key > node->right->key) {
        return leftRotate(node);
    }
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node; // Возвращаем текущий узел
}

// Поиск узла в дереве
TreeNode* searchTree(TreeNode* node, int key) {
    if (!node || node->key == key) { // Если узел не существует или ключ совпадает
        return node; // Возвращаем узел
    }

    if (key < node->key) { // Если ключ меньше ключа текущего узла
        return searchTree(node->left, key); // Рекурсивно ищем в левом поддереве
    } else { // Если ключ больше ключа текущего узла
        return searchTree(node->right, key); // Рекурсивно ищем в правом поддереве
    }
}

// Поиск узла с минимальным значением ключа в дереве
TreeNode* minValueNode(TreeNode* node) {
    TreeNode* current = node; // Начинаем с текущего узла
    while (current->left) { // Пока есть левые поддеревья
        current = current->left; // Перемещаемся влево
    }
    return current; // Возвращаем узел с минимальным значением ключа
}

// Удаление узла из дерева
TreeNode* removeTree(TreeNode* root, int key) {
    if (!root) { // Если дерево пустое
        return root; // Возвращаем корень
    }

    if (key < root->key) { // Если ключ меньше ключа корня
        root->left = removeTree(root->left, key); // Рекурсивно удаляем из левого поддерева
    } else if (key > root->key) { // Если ключ больше ключа корня
        root->right = removeTree(root->right, key); // Рекурсивно удаляем из правого поддерева
    } else { // Если ключ совпадает с ключом корня
        if (!root->left || !root->right) { // Если у корня нет одного из поддеревьев
            TreeNode* temp = root->left ? root->left : root->right; // Сохраняем существующее поддерево
            if (!temp) { // Если поддерево пустое
                temp = root; // Сохраняем корень
                root = nullptr; // Делаем корень пустым
            } else { // Если поддерево не пустое
                *root = *temp; // Копируем содержимое поддерева в корень
            }
            delete temp; // Удаляем временный узел
        } else { // Если у корня есть оба поддерева
            TreeNode* temp = minValueNode(root->right); // Находим узел с минимальным значением ключа в правом поддереве
            root->key = temp->key; // Копируем ключ минимального узла в корень
            root->right = removeTree(root->right, temp->key); // Рекурсивно удаляем минимальный узел из правого поддерева
        }
    }

    if (!root) { // Если дерево стало пустым
        return root; // Возвращаем корень
    }

    updateHeight(root); // Обновляем высоту корня

    int balance = getBalance(root); // Вычисляем баланс корня

    // Проверяем и выполняем необходимые повороты для балансировки
    if (balance > 1 && getBalance(root->left) >= 0) {
        return rightRotate(root);
    }
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }
    if (balance < -1 && getBalance(root->right) <= 0) {
        return leftRotate(root);
    }
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root; // Возвращаем корень
}

// Вывод дерева в порядке возрастания ключей
void inOrderTree(TreeNode* root) {
    if (root) { // Если узел существует
        inOrderTree(root->left); // Рекурсивно выводим левое поддерево
        cout << root->key << " "; // Выводим ключ текущего узла
        inOrderTree(root->right); // Рекурсивно выводим правое поддерево
    }
}

// Очистка дерева
void clearTree(TreeNode* root) {
    if (root) { // Если узел существует
        clearTree(root->left); // Рекурсивно очищаем левое поддерево
        clearTree(root->right); // Рекурсивно очищаем правое поддерево
        delete root; // Удаляем текущий узел
    }
}

tree.h:

#ifndef TREE_H
#define TREE_H

// Структура узла дерева
struct TreeNode {
    int key; // Ключ узла
    TreeNode* left; // Указатель на левое поддерево
    TreeNode* right; // Указатель на правое поддерево
    int height; // Высота узла
    TreeNode(int k) : key(k), left(nullptr), right(nullptr), height(1) {} // Конструктор узла
};

// Прототипы функций для работы с AVL-деревом
int height(TreeNode* node); // Вычисление высоты узла
int getBalance(TreeNode* node); // Вычисление баланса узла
void updateHeight(TreeNode* node); // Обновление высоты узла
TreeNode* rightRotate(TreeNode* y); // Правый поворот
TreeNode* leftRotate(TreeNode* x); // Левый поворот
TreeNode* insertTree(TreeNode* node, int key); // Вставка узла в дерево
TreeNode* searchTree(TreeNode* node, int key); // Поиск узла в дереве
TreeNode* minValueNode(TreeNode* node); // Поиск узла с минимальным значением ключа в дереве
TreeNode* removeTree(TreeNode* root, int key); // Удаление узла из дерева
void inOrderTree(TreeNode* root); // Вывод дерева в порядке возрастания ключей
void clearTree(TreeNode* root); // Очистка дерева

#endif // TREE_H

datamanager.cpp:

#include "datamanager.h"
#include <fstream>
#include <sstream>
#include <iostream>

using namespace std;

// Функции для работы с массивом
void loadArrayData(const string& filename, Array& arr) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string value;
    while (file >> value) {
        pushBackArray(arr, value);
    }
    file.close();
}

void saveArrayData(const string& filename, const Array& arr) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    for (int i = 0; i < arr.size; ++i) {
        file << arr.data[i] << " ";
    }
    file.close();
}

// Функции для работы со списком
void loadListData(const string& filename, SinglyLinkedList& list) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string value;
    while (file >> value) {
        pushBackList(list, value);
    }
    file.close();
}

void saveListData(const string& filename, const SinglyLinkedList& list) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    ListNode* current = list.head;
    while (current) {
        file << current->data << " ";
        current = current->next;
    }
    file.close();
}

// Функции для работы с двусвязным списком
void loadDoublyListData(const string& filename, DoublyLinkedList& list) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string value;
    while (file >> value) {
        pushBackList(list, value);
    }
    file.close();
}

void saveDoublyListData(const string& filename, const DoublyLinkedList& list) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    DoublyNode* current = list.head;
    while (current) {
        file << current->data << " ";
        current = current->next;
    }
    file.close();
}

// Функции для работы с очередью
void loadQueueData(const string& filename, Queue& q) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string value;
    while (file >> value) {
        pushQueue(q, value);
    }
    file.close();
}

void saveQueueData(const string& filename, const Queue& q) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    QueueNode* current = q.front;
    while (current) {
        file << current->data << " ";
        current = current->next;
    }
    file.close();
}

// Функции для работы со стеком
void loadStackData(const string& filename, Stack& s) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string value;
    while (file >> value) {
        pushStack(s, value);
    }
    file.close();
}

void saveStackData(const string& filename, const Stack& s) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    StackNode* current = s.top;
    while (current) {
        file << current->data << " ";
        current = current->next;
    }
    file.close();
}

// Функции для работы с хеш-таблицей
void loadHashTableData(const string& filename, HashNode*& hashTable) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    string key, value;
    while (file >> key >> value) {
        insertHashNode(hashTable, key, value);
    }
    file.close();
}

void saveHashTableData(const string& filename, const HashNode* hashTable) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    const HashNode* current = hashTable;
    while (current) {
        ListNode* valueNode = current->values.head;
        while (valueNode) {
            file << current->key << " " << valueNode->data << endl;
            valueNode = valueNode->next;
        }
        current = current->next;
    }
    file.close();
}

// Функции для работы с AVL-деревом
void loadTreeData(const string& filename, TreeNode*& tree) {
    ifstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для чтения" << endl;
        return;
    }

    int key;
    while (file >> key) {
        tree = insertTree(tree, key);
    }
    file.close();
}

void saveTreeData(const string& filename, const TreeNode* tree) {
    ofstream file(filename);
    if (!file.is_open()) {
        cout << "Не удалось открыть файл для записи" << endl;
        return;
    }

    saveTreeDataHelper(file, tree);
    file.close();
}

void saveTreeDataHelper(ofstream& file, const TreeNode* tree) {
    if (tree) {
        saveTreeDataHelper(file, tree->left);
        file << tree->key << " ";
        saveTreeDataHelper(file, tree->right);
    }
}

void executeCommand(const string& command, Array& arr, SinglyLinkedList& list, DoublyLinkedList& doublyList, Queue& q, Stack& s, HashNode*& hashTable, TreeNode*& tree) {
    istringstream iss(command);
    string cmd, type;
    iss >> cmd >> type;

    // Массив
    if (cmd == "MPUSHBACK") {
        string value;
        iss >> value;
        if (type == "array") {
            pushBackArray(arr, value);
        }
    } else if (cmd == "MINSERT") {
        int index;
        string value;
        iss >> index >> value;
        if (type == "array") {
            insertArray(arr, index, value);
        }
    } else if (cmd == "MGET") {
        int index;
        iss >> index;
        if (type == "array") {
            cout << getArray(arr, index) << endl;
        }
    } else if (cmd == "MREMOVE") {
        int index;
        iss >> index;
        if (type == "array") {
            removeArray(arr, index);
        }
    } else if (cmd == "MREPLACE") {
        int index;
        string value;
        iss >> index >> value;
        if (type == "array") {
            replaceArray(arr, index, value);
        }
    } else if (cmd == "MLENGHT") {
        if (type == "array") {
            cout << lengthArray(arr) << endl;
        }
    }

    // Односвязный список
    else if (cmd == "LPUSHFRONT") {
        string value;
        iss >> value;
        if (type == "list") {
            pushFrontList(list, value);
        }
    } else if (cmd == "LPUSHBACK") {
        string value;
        iss >> value;
        if (type == "list") {
            pushBackList(list, value);
        }
    } else if (cmd == "LPOPFRONT") {
        if (type == "list") {
            popFrontList(list);
        }
    } else if (cmd == "LPOPBACK") {
        if (type == "list") {
            popBackList(list);
        }
    } else if (cmd == "LREMOVE") {
        string value;
        iss >> value;
        if (type == "list") {
            removeList(list, value);
        }
    } else if (cmd == "LFIND") {
        string value;
        iss >> value;
        if (type == "list") {
            cout << (findList(list, value) ? "правда" : "ложь") << endl;
        }
    }

    // Двусвязный список
    else if (cmd == "DPUSHFRONT") {
        string value;
        iss >> value;
        if (type == "doublylist") {
            pushFrontList(doublyList, value);
        }
    } else if (cmd == "DPUSHBACK") {
        string value;
        iss >> value;
        if (type == "doublylist") {
            pushBackList(doublyList, value);
        }
    } else if (cmd == "DPOPFRONT") {
        if (type == "doublylist") {
            popFrontList(doublyList);
        }
    } else if (cmd == "DPOPBACK") {
        if (type == "doublylist") {
            popBackList(doublyList);
        }
    } else if (cmd == "DREMOVE") {
        string value;
        iss >> value;
        if (type == "doublylist") {
            removeList(doublyList, value);
        }
    } else if (cmd == "DFIND") {
        string value;
        iss >> value;
        if (type == "doublylist") {
            cout << (findList(doublyList, value) ? "правда" : "ложь") << endl;
        }
    }

    // Очередь
    else if (cmd == "QPUSH") {
        string value;
        iss >> value;
        if (type == "queue") {
            pushQueue(q, value);
        }
    } else if (cmd == "QPOP") {
        if (type == "queue") {
            popQueue(q);
        }
    }

    // Стек
    else if (cmd == "SPUSH") {
        string value;
        iss >> value;
        if (type == "stack") {
            pushStack(s, value);
        }
    } else if (cmd == "SPOP") {
        if (type == "stack") {
            popStack(s);
        }
    }

    // Хеш-таблица
    else if (cmd == "HINSERT") {
        string key, value;
        iss >> key >> value;
        if (type == "hash") {
            insertHashNode(hashTable, key, value);
        }
    } else if (cmd == "HGET") {
        string key;
        iss >> key;
        if (type == "hash") {
            cout << getHashNode(hashTable, key) << endl;
        }
    } else if (cmd == "HREMOVE") {
        string key;
        iss >> key;
        if (type == "hash") {
            removeHashNode(hashTable, key);
        }
    }

    // AVL-дерево
    else if (cmd == "TINSERT") {
        int key;
        iss >> key;
        if (type == "tree") {
            tree = insertTree(tree, key);
        }
    } else if (cmd == "TREMOVE") {
        int key;
        iss >> key;
        if (type == "tree") {
            tree = removeTree(tree, key);
        }
    } else if (cmd == "TFIND") {
        int key;
        iss >> key;
        if (type == "tree") {
            TreeNode* result = searchTree(tree, key);
            cout << (result ? "правда" : "ложь") << endl;
        }
    } else if (cmd == "TINORDER") {
        if (type == "tree") {
            inOrderTree(tree);
            cout << endl;
        }
    }

    // Чтение
    else if (cmd == "PRINT") {
        if (type == "array") {
            printArray(arr);
        } else if (type == "list") {
            printList(list);
        } else if (type == "doublylist") {
            printList(doublyList);
        } else if (type == "queue") {
            printQueue(q);
        } else if (type == "stack") {
            printStack(s);
        } else if (type == "hash") {
            printHashTable(hashTable);
        } else if (type == "tree") {
            inOrderTree(tree);
            cout << endl;
        }
    }
}

datamanager.h:

#ifndef DATAMANAGER_H
#define DATAMANAGER_H

#include <string>
#include "array.h"          
#include "singlelist.h"     
#include "doublylist.h"     
#include "queue.h"          
#include "stack.h"          
#include "hashtable.h"      
#include "tree.h"           

// Функции для работы с массивом

// Загрузка данных из файла в массив
void loadArrayData(const std::string& filename, Array& arr);

// Сохранение данных массива в файл
void saveArrayData(const std::string& filename, const Array& arr);

// Функции для работы со списком

// Загрузка данных из файла в односвязный список
void loadListData(const std::string& filename, SinglyLinkedList& list);

// Сохранение данных односвязного списка в файл
void saveListData(const std::string& filename, const SinglyLinkedList& list);

// Функции для работы с двусвязным списком

// Загрузка данных из файла в двусвязный список
void loadDoublyListData(const std::string& filename, DoublyLinkedList& list);

// Сохранение данных двусвязного списка в файл
void saveDoublyListData(const std::string& filename, const DoublyLinkedList& list);

// Функции для работы с очередью

// Загрузка данных из файла в очередь
void loadQueueData(const std::string& filename, Queue& q);

// Сохранение данных очереди в файл
void saveQueueData(const std::string& filename, const Queue& q);

// Функции для работы со стеком

// Загрузка данных из файла в стек
void loadStackData(const std::string& filename, Stack& s);

// Сохранение данных стека в файл
void saveStackData(const std::string& filename, const Stack& s);

// Функции для работы с хеш-таблицей

// Загрузка данных из файла в хеш-таблицу
void loadHashTableData(const std::string& filename, HashNode*& hashTable);

// Сохранение данных хеш-таблицы в файл
void saveHashTableData(const std::string& filename, const HashNode* hashTable);

// Функции для работы с AVL-деревом

// Загрузка данных из файла в AVL-дерево
void loadTreeData(const std::string& filename, TreeNode*& tree);

// Сохранение данных AVL-дерева в файл
void saveTreeData(const std::string& filename, const TreeNode* tree);

// Вспомогательная функция для сохранения данных AVL-дерева
void saveTreeDataHelper(std::ofstream& file, const TreeNode* tree);

// Функция для выполнения команд
void executeCommand(const std::string& command, Array& arr, SinglyLinkedList& list, DoublyLinkedList& doublyList, Queue& q, Stack& s, HashNode*& hashTable, TreeNode*& tree);

#endif // DATAMANAGER_H

main.cpp:

#include <iostream>
#include <string>
#include "array.h"
#include "singlelist.h"
#include "doublylist.h"
#include "queue.h"
#include "stack.h"
#include "hashtable.h"
#include "datamanager.h"
#include "tree.h"

using namespace std;

int main(int argc, char** argv) {
    if (argc < 5) {
        cout << "Использование: ./dbms --file filename --query 'команда'" << endl;
        return 1;
    }

    string filename;
    string query;

    char** arg = argv + 1; // Указатель на первый элемент аргументов

    while (arg < argv + argc) {
        if (string(*arg) == "--file") {
            filename = *(++arg); // Увеличиваем указатель и берём следующий элемент
        } else if (string(*arg) == "--query") {
            query = *(++arg); // Аналогично
        }
        ++arg; // Переход к следующему аргументу
    }

    Array arr;
    SinglyLinkedList list;
    DoublyLinkedList doublyList;
    Queue q;
    Stack s;
    HashNode* hashTable = nullptr;
    TreeNode* tree = nullptr;
    
    initArray(arr);
    initList(list);
    initList(doublyList);
    initQueue(q);
    initStack(s);

    // Загрузка данных из файлов
    loadArrayData(filename + "_array.txt", arr);
    loadListData(filename + "_list.txt", list);
    loadDoublyListData(filename + "_doublylist.txt", doublyList);
    loadQueueData(filename + "_queue.txt", q);
    loadStackData(filename + "_stack.txt", s);
    loadHashTableData(filename + "_hash.txt", hashTable);
    loadTreeData(filename + "_tree.txt", tree);

    // Выполнение команд
    executeCommand(query, arr, list, doublyList, q, s, hashTable, tree);

    // Сохранение данных в файлы
    saveArrayData(filename + "_array.txt", arr);
    saveListData(filename + "_list.txt", list);
    saveDoublyListData(filename + "_doublylist.txt", doublyList);
    saveQueueData(filename + "_queue.txt", q);
    saveStackData(filename + "_stack.txt", s);
    saveHashTableData(filename + "_hash.txt", hashTable);
    saveTreeData(filename + "_tree.txt", tree);

    // Очистка структур данных
    clearArray(arr);
    clearList(list);
    clearList(doublyList);
    clearQueue(q);
    clearStack(s);
    clearHashNode(hashTable);
    clearTree(tree);

    return 0;
}
