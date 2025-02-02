# Кросс-компилятор

Кросс-компилятор (англ. ``cross compiler``) - компилятор, производящий исполняемый код для платформы, отличной от той, на которой исполняется сам кросс-компилятор. Такой инструмент бывает полезен, когда нужно получить код для платформы, экземпляров которой нет в наличии, или в случаях когда компиляция на целевой платформе невозможна или нецелесообразна (например, это касается мобильных систем или микроконтроллеров с минимальным объёмом памяти). Например, компилятор, который работает на компьютере Windows 7, но и генерирует код, который работает на Android.


## Применение кросс-компиляторов
- Встроенные компьютеры, где устройства имеют крайне ограниченные ресурсы.
- Компиляция для нескольких машин. Например, компания, возможно, пожелает поддержать несколько различных версий операционной системы или для поддержки нескольких различных операционных систем. С помощью кросс-компилятора одной сборки можно настроить для компиляции каждой из этих целевых задач.
- Компиляции на ферме серверов. Похожие на компиляции для нескольких машин сложной сборки, которые включают в себя множество операций компиляции и могут выполняться на любой машине.
- Самонастройка на новую платформу. При разработке программного обеспечения для новой платформы или эмулятора будущей платформы используется кросс-компилятор, чтобы скомпилировать необходимые инструменты.
- Компиляция машинного кода для эмуляторов для уже устаревших платформ, таких как Commodore 64 или Apple II

## Канадский крест

Канадский крест-это техника построения кросс-компиляторов для других машин. Система конфигурирования и сборки GNU позволяет собирать программы, которые запускаются на системе, отличной от той, на которой собирались необходимые средства. Иными словами, она поддерживает сборку программ с помощью кросс-компилятора.

**При использовании канадского креста c GCC могут быть четыре вида:**

- Фирменный родной компилятор для машины (1) (например, компилятор из Visual студии) используется для построения собственного компилятора GCC для машины (2).
- Родной компилятор GCC для машины (2) используется для сборки кросс-компилятора GCC с компьютера А на компьютер Б (3)
- GCC кросс-компилятор с компьютера A на компьютер Б (3) используется для построения компилятора GCC кросс-компилятор из машины в машину C (4)

<img alt="" src="https://commons.bmstu.wiki/images/8/89/Example_of_Canadian_Cross.png" />

**Схема**

Конечный результат кросс-компилятор (4) не сможет работать на построение машины А; вместо этого она будет работать на машине B для компиляции приложения в исполняемый код, чтобы потом быть скопированным на машину C и выполненным на компьютере С.

Термин канадский крест возник потому, что в то время, когда эти проблемы обсуждались, в Канаде было три национальных политических партии.

## Кросс-компиляция с GCC

GCC, бесплатная программа из коллекции компиляторов, может быть настроена для кросс компиляции. Она поддерживает множество платформ и языков.

Для кросс-компиляции с GCC необходимо, чтобы была доступна скомпилированная для целевой платформы версия binutils. Особенно важно наличие GNU Assembler. Поэтому binutils должны быть предварительно скомпилированы с ключом --target=some-target, указанным скрипту конфигурирования (англ.). GCC также должна быть указана опция --target с аналогичным содержанием. После этого, чтобы GCC могла использовать полученные binutils, надо поместить путь к ним в переменную окружения path, например:

```
PATH=/path/to/binutils/bin:${PATH} make
```

Кросс-компиляцией GCC требует, чтобы часть стандартной библиотеки целевой платформы была доступна на хост-платформе. Программист может выбрать для составления полную библиотеку C, но этот выбор может быть ненадежным. Альтернативой является использование файла, который представляет собой небольшую библиотеку C, содержащий только самые необходимые компоненты, необходимые для компиляции C в исходный код.
