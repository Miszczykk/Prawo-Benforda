# PL

## Prawo Benforda - Teoria

Według rozkładu Benforda, częstotliwość występowania danych cyfr, można określić wzorem:

![Logo](https://wikimedia.org/api/rest_v1/media/math/render/svg/e515e5c83116e046d86068e745ed556996e04f85)

Stosując ten wzór możemy dojść do wniosku, że dla cyfr:

| Pierwsza cyfra | Częstotliwość |
| :-------------:|:-------------:|
| 1              | 30,103%       |
| 2              | 17,609%       |
| 3              | 12,494%       |
| 4              | 9,691%        |
| 5              | 7,918%        |
| 6              | 6,695%        |
| 7              | 5,799%        |
| 8              | 5,115%        |
| 9              | 4,576%        |

Czyli im większa cyfra tym mniejsza szansa na jej wystąpienie, z czego szansa na wylosowanie jedynki jest o 71% większa niż szansa na wylosowanie dwójki.

## Prawo Benforda - Praktyka

Można sprawdzić te prawo, przeszukując wszystkie pliki znajdujące się na dysku `C:`. Dla testów sprawdzimy te prawo na dwa sposoby. W pierwszej próbie korzystam z funkcji do konwersji rozmiaru pliku z `Bajtów` na najbliższą ich wartość, natomiast w drugiej próbie bez tej funkcji.

```kotlin
fun convertFileSize(fileSize: Long): String{
    val kb = 1024L
    val mb = 1024L * 1024L
    val gb = 1024L * 1024L * 1024L
    val tb = 1024L * 1024L * 1024L * 1024L

    return when {
        fileSize < kb -> "$fileSize B"
        fileSize < mb -> "${fileSize / kb} KB"
        fileSize < gb -> "${fileSize / mb} MB"
        fileSize < tb -> "${fileSize / gb} GB"
        else          -> "${fileSize / tb} TB"
    }
}
```
**1. Z użyciem funkcji do konwersji**

| Pierwsza cyfra | Ilość          | Częstotliwość | Błąd bezwzględny |
| :-------------:|----------------|:-------------:|:----------------:|
| 1              | 233658         | 30,580%       | 0,477            |
| 2              | 124578         | 16,304%       | 1,305            |
| 3              | 95967          | 12,560%       | 0,066            |
| 4              | 77698          | 10,169%       | 0,478            |
| 5              | 59287          | 7,759%        | 0,159            |
| 6              | 49685          | 6,503%        | 0,192            |
| 7              | 44229          | 5,788%        | 0,011            |
| 8              | 41929          | 5,487%        | 0,372            |
| 9              | 37054          | 4,849%        | 0,273            |


**2. Bez funkcji do konwersji**

| Pierwsza cyfra | Ilość          | Częstotliwość | Błąd bezwzględny |
| :-------------:|----------------|:-------------:|:----------------:|
| 1              | 235675         | 30,844%       | 0,741            |
| 2              | 125588         | 16,436%       | 1,173            |
| 3              | 95712          | 12,526%       | 0,032            |
| 4              | 77377          | 10,127%       | 0,436            |
| 5              | 60316          | 7,894%        | 0,024            |
| 6              | 49597          | 6,491%        | 0,204            |
| 7              | 44740          | 5,855%        | 0,056            |
| 8              | 42303          | 5,536%        | 0,421            |
| 9              | 32777          | 4,290%        | 0,286            |

Analiza obu tabel potwierdza zgodność z Prawem Benforda - niezależnie od zastosowania konwersji jednostek, najczęściej występującą pierwszą cyfrą jest jedynka.

W pierwszej tabeli największe odchylenie od modelu teoretycznego wykazuje cyfra dwa. Różnica nie jest jednak na tyle istotna, by podważyć wiarygodność zbioru, a cyfra 7 wykazuje niemal idealną zgodność z wzorcem.

W przypadku drugiej tabeli cyfra dwa ponownie obarczona jest największym błędem, natomiast najbardziej zbliżoną wartości oczekiwanej okazała się tym razem cyfra 5.

Fakt, że prawo Benforda zadziałało zarówno dla danych po konwersji, jak i bez, jest dowodem o niezmienniczości skali. Jeśli zbiór danych podlega prawu Benforda, to zmiana jednostki nic nie da, ponieważ rozkład cyfr pozostanie bez zmian.

Badanie pokazało "zdrowy" stan dysku. Gdyby na dysku znajdowałoby się złośliwe oprogramowanie (np. botnet lub ransomware), najpewniej tworzyłoby ono pliki o stałej, specyficznej wielkości lub o losowym rozkładzie rozmiaru. Nagłe odchylenie od wykresu Benforda (np. nagły skok słupka dla cyfry 9) podczas skanowania serwera plików może być sygnałem alarmowym świadczącym o ataku hakerskim.

### Materiały

 - [Wikipedia](https://pl.wikipedia.org/wiki/Rozk%C5%82ad_Benforda)

# EN

## Benford's Law - Theory

According to Benford's distribution, the frequency of occurrence of given digits can be determined by the formula:

![Logo](https://wikimedia.org/api/rest_v1/media/math/render/svg/e515e5c83116e046d86068e745ed556996e04f85)

Applying this formula, we can conclude that for the digits:

| First Digit    | Frequency     |
| :-------------:|:-------------:|
| 1              | 30,103%       |
| 2              | 17,609%       |
| 3              | 12,494%       |
| 4              | 9,691%        |
| 5              | 7,918%        |
| 6              | 6,695%        |
| 7              | 5,799%        |
| 8              | 5,115%        |
| 9              | 4,576%        |

This means the larger the digit, the smaller the chance of its occurrence; specifically, the chance of drawing a one is 71% greater than the chance of drawing a two.

## Benford's Law - Practice

This law can be verified by scanning all files located on the `C:` drive. For testing purposes, we will check this law in two ways. In the first attempt, I use a function to convert the file size from `Bytes` to their nearest unit value, whereas in the second attempt, I do so without this function.

```kotlin
fun convertFileSize(fileSize: Long): String{
    val kb = 1024L
    val mb = 1024L * 1024L
    val gb = 1024L * 1024L * 1024L
    val tb = 1024L * 1024L * 1024L * 1024L

    return when {
        fileSize < kb -> "$fileSize B"
        fileSize < mb -> "${fileSize / kb} KB"
        fileSize < gb -> "${fileSize / mb} MB"
        fileSize < tb -> "${fileSize / gb} GB"
        else          -> "${fileSize / tb} TB"
    }
}
```

**1. With conversion function**

| First Digit    | Count          | Frequency     | Absolute Error   |
| :-------------:|----------------|:-------------:|:----------------:|
| 1              | 233658         | 30,580%       | 0,477            |
| 2              | 124578         | 16,304%       | 1,305            |
| 3              | 95967          | 12,560%       | 0,066            |
| 4              | 77698          | 10,169%       | 0,478            |
| 5              | 59287          | 7,759%        | 0,159            |
| 6              | 49685          | 6,503%        | 0,192            |
| 7              | 44229          | 5,788%        | 0,011            |
| 8              | 41929          | 5,487%        | 0,372            |
| 9              | 37054          | 4,849%        | 0,273            |

**2. Without conversion function**

| First Digit    | Count          | Frequency     | Absolute Error   |
| :-------------:|----------------|:-------------:|:----------------:|
| 1              | 235675         | 30,844%       | 0,741            |
| 2              | 125588         | 16,436%       | 1,173            |
| 3              | 95712          | 12,526%       | 0,032            |
| 4              | 77377          | 10,127%       | 0,436            |
| 5              | 60316          | 7,894%        | 0,024            |
| 6              | 49597          | 6,491%        | 0,204            |
| 7              | 44740          | 5,855%        | 0,056            |
| 8              | 42303          | 5,536%        | 0,421            |
| 9              | 32777          | 4,290%        | 0,286            |

Analysis of both tables confirms compliance with Benford's Law—regardless of the application of unit conversion, the most frequently occurring first digit is one.

In the first table, the digit two shows the greatest deviation from the theoretical model. However, the difference is not significant enough to undermine the reliability of the dataset, and the digit 7 shows almost ideal compliance with the pattern.

In the case of the second table, the digit two is again burdened with the largest error, whereas the digit 5 proved to be the closest to the expected value this time.

The fact that Benford's Law worked for data both with and without conversion is proof of scale invariance. If a dataset is subject to Benford's Law, changing the unit will not affect the outcome because the distribution of digits remains unchanged.

The study showed a "healthy" state of the disk. If the disk contained malicious software (e.g., botnet or ransomware), it would most likely create files of a constant, specific size or with a random size distribution. A sudden deviation from the Benford chart (e.g., a sudden spike for the digit 9) during a file server scan could be an alarm signal indicating a hacking attack.

### References

 [Wikipedia](https://en.wikipedia.org/wiki/Benford%27s_law)