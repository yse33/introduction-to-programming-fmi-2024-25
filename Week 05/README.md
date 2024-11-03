# Масиви (продължение). Търсене на елемент в масив. Сортиране на масив. Представяне на символни низове (текст) чрез char[]

### Сортиране на масив

Сортирането помага за организиране и представяне на данните по начин, който е по-лесен за разбиране и обработка.

**Bubble sort**

Bubble Sort преглежда масива многократно и разменя съседни елементи, ако са в неправилен ред. Подходящ е за малки масиви и поддържа стабилност, т.е., запазва реда на елементите при равни стойности.

_На този етап в курса по УП, най - много ще използвате този алгоритъм за сортиране. Въпреки това, той далеч не е най-добрият такъв! Повече за сортиращи алгоритми по-нататък..._

```cpp
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    int arr[] = {7, 1, 3, 2, 9, 14, 6};
    bubbleSort(arr, 7); // 1, 2, 3, 6, 7, 9, 14
}
```

_**За по - любознателните:** [тук](https://visualgo.net/en/sorting) може да разгледате още алгоритми за сортиране и как работят те..._

---

### Търсене на елемент в масив

Често се налага да намираме конкретна стойност в колекция от данни. Например, в масив от числа може да искаме да намерим конкретна стойност, или в списък от имена - да открием дали даден човек присъства. Търсенето ни позволява ефективен достъп до нужната информация, без да се налага да преглеждаме всички елементи ръчно.

**Линейно търсене (Linear search)**

```cpp
int linearSearch(const int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i; // връщаме индекса, на който се намира търсеният елемент
        }
    }
    return -1; // елементът не е намерен
}
```

Бонус: **Двоично търсене (Binary search)**

```cpp
int binarySearch(const int arr[], int size, int target) {
    int left = 0, right = size - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1; // елементът не е намерен
}
```

Двоичното търсене работи **само върху сортирани масиви**, като използва подход за разделяне на половина за по-бързо намиране на целевата стойност.
Двоичното търсене е много по-ефективно от линейното търсене.

---

### Представяне на символни низове в C++ като масив от символи

В C++ символните низове (или текстовете) могат да бъдат представени като масиви от символи, или `char[]`.Това е по-ниско ниво на работа с текст в сравнение с по-модерния `std::string` клас и се основава на традицията от езика C.

**В курса по УП няма да използвате `std::string`, а ще работите с `char[]`!**

Един символен низ може да бъде създаден чрез масив от символи:

```cpp
char message[] = "Hello!";
cout << greeting[0];  // 'H'
cout << greeting[1];  // 'e'
```

Тук "Hello there!" се записва като последователност от символи 'H', 'e', 'l', 'l', 'o', '!', последвана от специалния null символ '\0', който обозначава края на низа. Това е важно, защото в C++ и C символните низове трябва да завършват с '\0' (терминираща нула), за да може компилаторът да разбере къде свършва низа.

![](https://www.tutorialspoint.com/cprogramming/images/string_representation.jpg)

```cpp
char message1[] = {'H', 'e', 'l', 'l', 'o', '!'};
cout << message1; // Hello!╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠╠α√êF≈

char message2[] = {'H', 'e', 'l', 'l', 'o', '!', '\0'};
cout << message2; // Hello!
```

#### Чести грешки

- **Липса на терминираща нула**: Ако не добавим '\0' в края на масива, това може да доведе до нежелано поведение, тъй като компютърът няма да знае къде свършва низа.
- **Препълване на масива**: В char[] трябва винаги да се внимава с размера на масива, защото ако опитаме да добавим повече символи от предвидените, ще предизвикаме грешки като buffer overflow.

### Обхождане на символен низ

Обхождането на символен низ, представен като char[], може да се осъществи с помощта на терминиращата нула `'\0'`, за да се определи къде свършва низът. Вместо да използваме предварително определена дължина, можем да проверим всеки символ в масива, докато не достигнем `'\0'`.

```cpp
for (int i = 0; input[i] != '\0'; i++) {
    cout << "Character at index " << i << ": " << input[i] << endl;
}
```

### Прочитане на текст от конзолата

1. **Четене на текст с `>>`**

- **Чете отделни "думи"**: Операторът >> разделя входа на "думи" и чете до първото бяло пространство (интервал, нов ред и т.н.).
- **Пример**: При въвеждане на "Hello World!" само "Hello" ще бъде прочетено в първото извикване на >>, а "World!" ще бъде оставено за следващото извикване.

  ```cpp
  char name[100];
  cin >> name; // Input: Stefan Shivarov
  cout << name; // Output: Stefan
  ```

2. **Четене на текст с .getline()**

- **Чете цели редове**: Методът .getline() прочита целия ред, включително интервали, до терминиращата нула или до зададена максимална дължина.
- **Пример**: При въвеждане на "Hello World!" целият низ "Hello World!" ще бъде прочетен.

  ```cpp
  char name[100];
  cin.getline(name, 100); // Input: Stefan Shivarov
  cout << name; // Output: Stefan Shivarov
  ```

**Внимавайте**: ако използвате `>>` и `cin.getline` едновременно за четене на вход, когато ги редувате, между тях трябва да
използвате `cin.ignore()`! Ако преди `cin.getline` е било използвано `cin >>`, остатъкът от реда може да остане в буфера. В такива случаи е полезно да използвате `cin.ignore()` за изчистване на буфера.