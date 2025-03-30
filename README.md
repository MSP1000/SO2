Dokumentacja kodu - Problem filozofów (PLIK WYGLĄDA LEPIEJ W TRYBIE CODE)
Opis ogólny
Kod implementuje klasyczny problem „pięciu” filozofów, który ilustruje problemy synchronizacji w programowaniu wielowątkowym. W tym przypadku „n” filozofów siedzi przy stole i na przemian myśli i je. Aby zjeść, każdy filozof potrzebuje dwóch widelców, które są dzielone z sąsiadami. Kod wykorzystuje wątki oraz mechanizmy synchronizacji, takie jak mutexy i zmienne warunkowe, aby zapewnić, że filozofowie nie będą jednocześnie próbowali jeść. Jeżeli jakiś filozof przez długi okres nic nie jadł program kończy się z komentarzem niepowodzenia.
Struktura kodu
Nagłówki
#include <bits/stdc++.h>
#include <pthread.h>
#include <unistd.h>
#include <conio.h>
•	bits/stdc++.h: Nagłówek zawierający wszystkie standardowe biblioteki C++.
•	pthread.h: Nagłówek do obsługi wątków w C.
•	unistd.h: Nagłówek do funkcji systemowych, takich jak sleep.
•	conio.h: Nagłówek do funkcji konsolowych (może być niepotrzebny w niektórych systemach).
Definicje i zmienne globalne
#define N 40
#define THINKING 2
#define HUNGRY 1
#define EATING 0
#define LEFT (philoID + 4) % N
#define RIGHT (philoID + 1) % N

int Stoic[N];
int times = 200;
•	N: Liczba filozofów (ustawiona na 40).
•	THINKING, HUNGRY, EATING: Stany filozofów.
•	LEFT, RIGHT: Indeksy sąsiadujących filozofów.
•	Stoic: Tablica przechowująca indeksy filozofów.
•	times: Liczba iteracji, które każdy filozof wykona.
Klasa Table
Klasa Table zarządza stanami filozofów oraz synchronizacją.
Atrybuty
•	state[N]: Tablica przechowująca stany filozofów.
•	phcond[N]: Zmienne warunkowe dla każdego filozofa.
•	condLock: Mutex do synchronizacji.
Metody
•	test(int philoID): Sprawdza, czy filozof może zacząć jeść. Jeśli sąsiedzi nie jedzą i filozof jest głodny, zmienia jego stan na EATING i sygnalizuje warunek.
•	take_fork(int philoID): Ustawia stan filozofa na HUNGRY, wywołuje test, a jeśli filozof nie może jeść, czeka na sygnał.
•	put_fork(int philoID): Ustawia stan filozofa na THINKING i testuje sąsiadów, aby sprawdzić, czy mogą zacząć jeść.
•	Table(): Konstruktor, który inicjalizuje stany filozofów oraz zmienne warunkowe.
•	~Table(): Destruktor, który niszczy zmienne warunkowe i mutex.
Funkcja philosopher
void *philosopher(void *arg)
Funkcja, która reprezentuje zachowanie każdego filozofa. Wykonuje następujące kroki:
1.	Filozof myśli przez 1 sekundę.
2.	Próbuje wziąć widelce.
3.	Zwiększa licznik głodu.
4.	Jeśli głód przekracza 10, filozof umiera z głodu.
5.	Filozof odkłada widelce i kończy iterację.
Funkcja main
int main()
Funkcja główna programu, która:
1.	Deklaruje wątki i atrybuty.
2.	Inicjalizuje atrybuty wątków.
3.	Tworzy wątki dla każdego filozofa.
4.	Czeka na zakończenie wszystkich wątków.
5.	Niszczy atrybuty wątków i kończy program.
Użycie
Aby skompilować i uruchomić program, należy użyć kompilatora obsługującego wątki, np. g++ z flagą -pthread:
bash
g++ -pthread -o philosophers philosophers.cpp
./philosophers
Uwagi
   Żeby zmienić Liczbe Filozofów Wystarczy na początku pliku zmienić N na odpowiednią liczbe
