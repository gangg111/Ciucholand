# Ciucholand

Aplikacja na Androida do pilnowania terminów odbioru odzieży roboczej. Dodajesz ubranie z datą
ostatniego wydania i przydziałem (np. co 12 miesięcy), a aplikacja przypomina o odbiorze,
prowadzi historię i pilnuje zaległości.

## Funkcje

- Wpisy: rodzaj, rozmiar, ilość i jednostka (szt. / para), przydział co ile miesięcy,
  data ostatniego wydania, historia odbiorów.
- Lista z sekcjami Zaległe / Wkrótce / Później, sortowana po najbliższym terminie.
- Karta wpisu: ikona typu ubrania, pigułka statusu (ZALEGŁE x dni / DZIŚ / za x dni),
  pasek postępu cyklu, data następnego odbioru.
- Potwierdzanie odbioru pojedynczo i masowo (zaznaczanie długim przyciśnięciem),
  odłożenie przypomnienia o 1-5 dni.
- Powiadomienia codziennie o wybranej godzinie (domyślnie 8:00), z akcjami
  "Odebrano" i "Odrzuć" prosto z powiadomienia. Przypomnienie przychodzi, dopóki
  odbiór nie zostanie potwierdzony.
- Ustawienia: ile dni przed terminem przypominać, o której godzinie, kopia danych
  (eksport / import JSON).
- Motyw jasny i ciemny.

## Wymagania

- Android 10 (API 29) lub nowszy, arm64-v8a.
- Do budowania: JDK 17/21; projekt zawiera Gradle wrapper.

## Budowanie

```bash
./gradlew :app:assembleDebug     # szybki build testowy
./gradlew :app:assembleRelease   # wersja release, podpisana kluczem autora
```

APK: `app/build/outputs/apk/release/app-release.apk`

Build release wymaga klucza `~/.android/ciuchy-release.jks` i hasła w pliku
`~/.android/ciuchy-release.pass`.

### Termux (aarch64)

Projekt jest skonfigurowany pod budowanie bezpośrednio na telefonie: `gradle.properties`
wskazuje natywny `aapt2` z Termuxa (`android.aapt2FromMavenOverride`), bo wersja z Maven
jest x86_64, a `compileSdk` jest przypięty do 34. Wymagane pakiety:
`openjdk-21`, `aapt2`, `apksigner`, `zipalign`.

## Struktura projektu

```
app/src/main/java/com/ciuchy/vwp/
  MainActivity.kt      - UI (Jetpack Compose Material 3) i logika ekranu
  Store.kt             - model wpisu oraz zapis/odczyt (SharedPreferences, JSON)
  ReminderReceiver.kt  - dzienny alarm, powiadomienia i ich akcje
app/src/main/res/drawable/  - ikony typów ubrań
```

## Dane

Wpisy są przechowywane lokalnie w SharedPreferences jako JSON - aplikacja nie wysyła
nic do internetu. Kopię zapasową zrobisz w Ustawieniach ("Zapisz do pliku") i wczytasz
przyciskiem "Wczytaj z pliku".

## Licencja

PolyForm Noncommercial License 1.0.0 - bezpłatnie do użytku prywatnego i niekomercyjnego.
Wykorzystanie komercyjne (w tym przez firmy i inne podmioty gospodarcze) wymaga pisemnej
zgody autora. Pełny tekst: [`LICENSE`](LICENSE).

## Autor

Artur Szafraniec - wersja 1.0.0
