### Cel Programu:
Program wyświetla liczby na matrycy LED micro:bit, używając dwóch pierwszych rzędów do wyświetlania jednostek (1-9) i kolejnych rzędów do wyświetlania dziesiętnych (10, 20, 30, itd.).

### Kroki w Kodzie:

1. **Zdefiniowanie funkcji `showNumber`:**
   Funkcja `showNumber` przyjmuje liczbę `num` i wyświetla ją na matrycy LED micro:bit.

2. **Wyczyść ekran:**
   Każde wywołanie funkcji zaczyna się od wyczyszczenia ekranu, aby usunąć poprzednie liczby.
   ```blocks
   basic.clearScreen()
   ```

3. **Wyświetlanie jednostek (1-9):**
   - Oblicz resztę z dzielenia `num` przez 10, aby uzyskać jednostki.
     ```blocks
     let units = num % 10
     ```
   - Użyj pętli do zapalenia odpowiednich diod LED w pierwszych dwóch rzędach.
     ```blocks
     for (let i = 0; i < units; i++) {
         let x = i % 5 // kolumna: 0, 1, 2, 3, 4, cyklicznie
         let y = Math.floor(i / 5) // rząd: 0, 1
         led.plot(x, y)
     }
     ```
   - Wyjaśnienie:
     - `i % 5`: Ta operacja zapewnia, że `x` (kolumna) przyjmuje wartości od 0 do 4, po czym zaczyna się od nowa.
     - `Math.floor(i / 5)`: Ta operacja zwiększa `y` (rząd) co 5 kolumn. Więc dla wartości `i` od 0 do 4, `y` jest 0, a dla `i` od 5 do 9, `y` jest 1.

4. **Wyświetlanie dziesiętnych (10, 20, ...):**
   - Oblicz całkowitą część z dzielenia `num` przez 10, aby uzyskać dziesiętne.
     ```blocks
     let tens = Math.floor(num / 10)
     ```
   - Użyj pętli do zapalenia odpowiednich diod LED w trzecim i kolejnych rzędach.
     ```blocks
     for (let j = 0; j < tens; j++) {
         let x = j % 5 // kolumna: 0, 1, 2, 3, 4, cyklicznie
         let y = 2 + Math.floor(j / 5) // rząd: 2, 3, 4
         led.plot(x, y)
     }
     ```
   - Wyjaśnienie:
     - `j % 5`: Ta operacja zapewnia, że `x` (kolumna) przyjmuje wartości od 0 do 4, po czym zaczyna się od nowa.
     - `2 + Math.floor(j / 5)`: Ta operacja zwiększa `y` (rząd) co 5 kolumn, zaczynając od rzędu 2.

5. **Wywoływanie funkcji `showNumber` w pętli `forever`:**
   - W bloku `forever`, liczby od 1 do 60 są wyświetlane z przerwą 1 sekundy między wyświetleniami.
     ```blocks
     basic.forever(function () {
         for (let i = 1; i <= 60; i++) {
             showNumber(i)
             basic.pause(1000) // Pauza 1 sekunda
         }
     })
     ```

### Podsumowanie:
- **Funkcja `showNumber(num)`**: Wyświetla liczbę `num` na matrycy LED, wykorzystując pierwsze dwa rzędy do jednostek (1-9) i kolejne rzędy do dziesiętnych (10, 20, ...).
- **Kolumny i rzędy**: `i % 5` cyklicznie przechodzi przez kolumny 0 do 4, a `Math.floor(i / 5)` zwiększa rząd co 5 kolumn.
- **Pętla `forever`**: Cykl od 1 do 60 z wywołaniem `showNumber` dla każdej liczby, z przerwą 1 sekundy między wyświetleniami.
