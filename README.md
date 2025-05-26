Stack.cpp 


//
//
#define QUEUE_SIZE 5
int queue_table[QUEUE_SIZE] = { 0 };
int front = 0;
int rear = 0;
int count = 0;

int isQueueEmpty(void)
{
    return (count == 0) ? 1 : 0;
}

int isQueueFull(void)
{
    return (count == QUEUE_SIZE) ? 1 : 0;
}

int Dequeue(void)
{
    if (!isQueueEmpty())
    {
        int val = queue_table[front];
        front = (front + 1) % QUEUE_SIZE;
        count--;
        return val;
    }

    return queue_table[front]; // lub jakiś kod błędu
}

int Front(void)
{
    if (!isQueueEmpty())
    {
        return queue_table[front];
    }

    return queue_table[front]; // lub jakiś kod błędu
}

void Enqueue(int val)
{
    if (!isQueueFull())
    {
        queue_table[rear] = val;
        rear = (rear + 1) % QUEUE_SIZE;
        count++;
    }
}


Stack.h
//

//

#ifndef MYQUEUE_QUEUE_H
#define MYQUEUE_QUEUE_H

int isQueueEmpty(void);
int isQueueFull(void);
int Dequeue(void);
int Front(void);
void Enqueue(int val);

#endif //MYQUEUE_QUEUE_H

Main.cpp

//#include <iostream>
#include <stdio.h>
#include "Queue.h"  // zamienione z "Stack.h"

void menu(void)
{
    printf("\n");
    printf("1 - dodaj liczbe do kolejki (Enqueue)\n");
    printf("2 - odczytaj wartosc z poczatku kolejki (Front)\n");
    printf("3 - zdejmij liczbe z kolejki (Dequeue)\n");
    printf("4 - sprawdz czy kolejka jest pusta\n");
    printf("5 - sprawdz czy kolejka jest pelna\n");
    printf("6 - koniec programu\n");
    printf("\n");
}

int main()
{
    int temp = 0;
    int option = 0;
    printf("KOLEJKA - implementacja w tablicy statycznej (FIFO)\n");
    while (1)
    {
        menu();
        scanf("%d", &option);

        switch (option)
        {
            case 1:
                if (!isQueueFull()) {
                    printf("Podaj wartosc: ");
                    scanf("%d", &temp);
                    Enqueue(temp);
                }
                else {
                    printf("Operacja niedozwolona - KOLEJKA pelna!!!\n\n");
                }
                break;

            case 2:
                if (!isQueueEmpty()) {
                    temp = Front();
                    printf("Odczytana wartosc: %d", temp);
                }
                else {
                    printf("Operacja niedozwolona - KOLEJKA pusta!!!\n\n");
                }
                break;

            case 3:
                if (!isQueueEmpty()) {
                    temp = Dequeue();
                    printf("Zdjeta wartosc: %d", temp);
                }
                else {
                    printf("Operacja niedozwolona - KOLEJKA pusta!!!\n\n");
                }
                break;

            case 4:
                if (isQueueEmpty()) {
                    printf("KOLEJKA jest pusta.\n");
                }
                else {
                    printf("KOLEJKA nie jest pusta.\n");
                }
                break;

            case 5:
                if (isQueueFull()) {
                    printf("KOLEJKA jest pelna.\n");
                }
                else {
                    printf("KOLEJKA nie jest pelna.\n");
                }
                break;

            case 6:
                return 0;

            default:
                printf("Wybierz wlasciwa opcje.\n\n");
                break;
        }
    }

    return 0;
}

