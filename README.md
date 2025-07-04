# SBBus

**По любым вопросам обращайтесь по контактам указанным на странице "Контакты" [на моем сайте](https://seryibaran.github.io).**

Шина переключателей для Mindustry 7+. Проверено и работает в кампании и на сервере.

Существуют версии
- [1 канал (SBBus Instant)](#sbbus-instant) - 5237,5 блоков/сек
- [4 каналов (SBBus Mini)](#sbbus-mini)
- [32 канала (SBBus)](#sbbus-1)
- [256 каналов (SBBus 256)](#sbbus-256)
- [512 каналов (SBBus 512)](#sbbus-512)

Версия на 1 канал самая молниеносная из всех.

Все версии можно ускорить доработав и поставив больше передатчиков между каждой ячейкой. В 32-канальной SBBus 1 передатчик синхронизирует 32 адреса между 2 ячейками памяти, а можно сделать чтобы между этими 2 ячейками памяти стояло 8 передатчиков, и каждый будет синхронизировать только свой кусочек памяти, из 32/8=4 каналов.

А ещё при желании и доработке можно совместить SBBus на 32 канала, SBBus 512 и SBBus Instant и сделать чтобы через 1 большую банку памяти на 512 адресов шло 16 линий по 32 канала. В этом случае будут ставиться ячейки а между ними по 16 передатчиков, каждый на свой кусочек памяти.

- Установите панель
- Подключите шину состоящую из ячейка_панели-ячейка-передатчик-ячейка-передатчик-ячейка...
- Подключайте к ячейкам модули вроде считывателя и клиента.

- 1 передатчик может транслировать данные на несколько ячеек

## SBBus

Стандартная шина - SBBus - 32 канала - 2 блока по 16 каналов.

### Пример

![](./example.png)

1. Настройки панели
   - 1МЕДЬ выключен
   - 1СВИНЕЦ включен
   - 2СТРУЧОК выключен
   - 2ВЗРЫВНАЯСМЕСЬ включен
3. Настройки клиента
   - 1 клиент установлен на 1МЕДЬ и постройки подключенные к процессору 2 выключены
   - 2 клиент установлен на 1СВИНЕЦ и постройки подключенные к процессору 2 включены
   - 3 клиент установлен на 2СТРУЧОК и постройки подключенные к процессору 2 выключены
   - 4 клиент установлен на 2ВЗРЫВНАЯСМЕСЬ и постройки подключенные к процессору 2 включены

### Спецификация

- Панель сканирует 32 переключателя и записывает в 32 адреса ячейки памяти
- Передатчик сканирует первую подключенную ячейку памяти и копирует по остальным подключенным
- Считыватель сканирует и выводит содержимое подключенной ячейки памяти
- Клиент считывает адрес из сортировщиков (в SBBus 512 для этого 2 гиперпроцессора), получает из второй подключенной ячейки (первая - встроена в клиенте) состояние и записывает во встроенную первую ячейку памяти. Оттуда состояние читают индикаторный процессор (как правило маленький) и процессор управления (как правило большой). Процессор управления переключает все подключенные к нему устройства.

### Использование

1. Поставьте панель
2. Подключите к её ячейке памяти Передатчик
3. Подключите к передатчику ячейку памяти
4. Ведите такую последовательность из ячеек и передатчиков (шину) до нужных клиентов
5. Подключите клиентов к ячейкам памяти
6. Укажите адрес в клиенте

### Панель

2 группы по 16 каналов.

![](./panel.png)

s1:

![](./panel_s1.png)

```
bXNjaAF4nFWTe0gUURSH78zOax8+sDTIAjOCyrakMqKQylSsKNDECLFY10E3dp1ld83c/kiwFxUtCwZBgqEIi0ukPS1dCpIiRZtFDFEKIigNIspXhC3NPfcgNMMwzHd/fHPmzLlEIVYTEeodHpWk6e16jx7TH+v98RtZxwsKGvzEWqP6nT6XN+DS6gkhkttRrbr9RKj0NFVJRPI3ugLOOuOu+QKqj1idmter+uyNDrebpLi1WpfT7vVpTtVvBIjVo3o0X5PdqRqrsseAjlrVkB4h9LBwhDNunEiIAoBHYhLhybgE4ETEBWk5KiNRRJbgUMeBzgyER0J1xpNxCSwq4oK0HJWRKBCFdwPhQWcBwiOhOh5OgZUp4oK0HJWRKCL7DBPqTKCzAuGRUJ2JapnOhDoT6FhURqJAlJ7mZFrnubai0cr6ltzUS58OTXanR72NzSN/7denpZKe1WVXsmxDFc/HImWZwSzzV3Fm1paIpYU17fx4d+7vR7HonW15FyZfTr1u3zN+cl9f4mxf79FnDU8sx+79elUxvzBxZina4j+xuNDb/3B0Zso7uSVq2Tv2fu3YYGQk0PVmxrG7OtI2n3Ce3jXRtoof+F516stwTdLAH/+HHwvBpcz7Kbd/Hi78XDKYXZidk30rL/x2RXh4R+nd2Rxtse5qaldph62s/GJG+vriDZHSTb7yyx/fdazJ796vhc3xzp3B1gOha3pn9VxEiA13rMzffDA0FO+0zGUUrQu2Foe2T1cluKc3v42yAYHmCNBZGxAeCe2sAL8JOitgZwXoLIvKSBSRzZqIOhF0SUB4JFQn0t/NdCLqRNCxqIxEgajxQjpeRpBYBI5s/G+zxVv0F/FmAzzQ+w0U0/viIbYDt9JBxzokqCMZCI+E1iHRcWN1SFiHBHWwqIxEgaixW1Angy4FCI+E6mQ6s0wno04GHYvKSBSI/gMdMdFn
```

```
set p 0
getlink link p
sensor result link @enabled
op sub temp1 p 1
write result cell1 temp1
op add p p 1
op add temp2 @links 1
jump 1 lessThan p temp2
```

### Считыватель

![](./reader.png)

s1:

![](./reader_s1.png)

```
bXNjaAF4nGNgYmBmZmDJS8xNZZC9sPBi+4UdF5sudl/YdGHDxaYLWy/svtijEOzkVFqsx8CdklqcXJRZUJKZn8fAwMCWk5iUmlPMwBKdWxnLxMCfk5+emaxbUJSfnFpcnF/EwJ4LpBPTU4FKmRlAgA+IUyvmmPYG8jUb8Dhzx2ss/yD4omzq38VdadrBCYGX78332KB/+/w0mxYBscdsR32mBrulvr60YZNHy6RrbzPMl8xXevom2nVJ/v1YhZxvWi8LvtXEfN5eon1jr4d83xNx5xn/Lv6tYKr4qhzKwAi0iomFkcEFr48ULsy/sO/Clgu7gGJ9EHUXtioAqUYgYx9QYO+FHRd26QFNYwSb1pBXmpMzkJgBAIn1vbs=
```

```
set p 0
read result cell1 p
print result
op add p p 1
jump 1 lessThan p 32
printflush message1
```

### Передатчик

![](./wire.png)

s1:

![](./wire_s1.png)

```
bXNjaAF4nGNgYmBmZmDJS8xNZZC6MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRazMCdklqcXJRZUJKZn8fAwMCWk5iUmlPMwBKdWxnLxMCfk5+emaxbUJSfnFpcnF/EwJ4LpBPTU4FKmRhAgA+IiyrmuPbd5TxswNNyN9y3UPnKWSZJJe4ZXk/8PVufXjDcVZTkrNFU/ePHjsvKLR+KNQ1cpJa+2LM+IzHE8LFnpJByt3zUB7GrHMvy53Xf2fDTR945yW2vx+mNklYrdvAH39K/tjfv8K0o40f3Db5sPfGySnOOMZveEgZGkAtYGBnycPtNjwsotw8ovuvC7ot9IJmLTRe2KgCpRiBjH1BgL0ixjsKF7SCtQCP2KFzYj03HpovdF1tBEnoMAJy8pQ0=
```

```
set p 1
getlink link p
set d 0
read result cell1 d
write result link d
op add d d 1
jump 3 lessThan d 32
op add p p 1
jump 1 lessThan p @links
```


### Клиент

2 группы по 16 каналов.

![](./client.png)

s1:

![](./client_s1.png)

s2:

![](./client_s2.png)

s3:

![](./client_s3.png)

```
bXNjaAF4nGNgZ2BhZmDJS8xNZRC6MOvC7gs7Lmy9sPdik0Kwk1NpMQN3SmpxclFmQUlmfh4DAwNbTmJSak4xA0t0bmUsGwN/Tn56ZrJuQVF+cmpxcX4RAxuQKEktYmDPBfIT01MZeCEqUjKLC3ISKxm4c1Nz84sqdZNTc3IY+HMzk4vykXQzMHAxgAAfAwPjxYo5tVOj824biLjMdJf/oLWDkfnZ1cUv4+t2CUQl5YhtWTFJhElf35o7OJZ9qYnWF+Uu46bzsn016keub89oe9H85s+HJH+vZ79Tmiad/9wcu9F3j+/82/uXn9bItvzx5fX5JXefZ3/6ZzFrwlvPV/v41dwqZ1zVDbBe/Ntpddpb4QtxPpfUlyfr8JhIX2G08HPsT5/tk7jihsMBga8B/+bMOjojZLfTnQ0SjWqzvyQs907MuNmQcflm+9J/x9eoH5HazRO9Yn4Er+PazZWBL+o3yW3sq3zH4FC4pWXC8c19af8X9R8sW9rtrHZEdnmBUfXbOfunqfHtavqwmD/N/tfRyEcrtE0aH7Nf3Pd5+kX/7guiy+MOesY0+502XmrxK8uUvak3YE7N1lkMC/0K3n3lmrstaqHFn6pWP+mtATL1e5vULnA/epDNs0eDrfCB6aHWswp+ux1PrJA6EmnOUXGX91GHtAf3Kcc5Bc0N5rcc5xQ1bzC/7TinrPvCdiCvnPtjonUHc/5Fjn+X+159s2yf7PB2xRW9J8a6n5OKPMuOWe7KfbfJlPX9EskvF2fGHQufvWvzrk5++evvTJ+U/3sd/nOhwKPAmsf/1+7ZsV/X487To9/vHZM5E/r0d/XHp+u9bTray1WPx8xlYARGLRMrKIKZgJiZhZGBxVDX0AwozggSYQJSIEFWQ3NdYyMGZiBkBIkygUU3XJhxYe+FLcDkuevChotNF/ZdbIAkUT2uC/Mv7APK7Lqw+2LfxfYLGy7sBMpvVTBUuLD/YgNQYduFrRcbLzaCtVzYpXCxA2jI3gtbcWo0xqWxGSy+4cImoIZ+YDbZc7H7wh6gMFBRE0gDUD+QBZTecGGPHgML2AsMrCAGMEUzlFTMSU5JSHih5+XrE6jhpat3VjPQw+/sScMQgwentM7qBhiEnTitX6ir43um0VO6YKmI6jRtledL1MQ0JWbO0pI4oODSrtnG55wiy3ai6oBQpuXSo5JcmjOPslp2Tm2LcXhuYLihSfbjf/sJhxkn//z//789w4UCs/MMIAcwgawvqJij23uRt9mAx2Uuf53N0V4G6ZIOvQlC3Ld2eYq0f+XmXDA552RV3fOOEz5aRmpxS15Z1xX2nXGtcRC8vSVJ7Cqn8nnNa5NEhP56q8a8ONtjO8eohuPs9d75b6+LhZyZt7r/7bcX8sfWXrtYEPXdfiezi7GWLAMAfs3/1w==
```

s1

```
sensor config1 sorter1 @config
sensor config2 sorter2 @config
jump 4 notEqual config1 @copper
set address 0
jump 6 notEqual config1 @lead
set address 1
jump 8 notEqual config1 @metaglass
set address 2
jump 10 notEqual config1 @graphite
set address 3
jump 12 notEqual config1 @sand
set address 4
jump 14 notEqual config1 @coal
set address 5
jump 16 notEqual config1 @titanium
set address 6
jump 18 notEqual config1 @thorium
set address 7
jump 20 notEqual config1 @scrap
set address 8
jump 22 notEqual config1 @silicon
set address 9
jump 24 notEqual config1 @plastanium
set address 10
jump 26 notEqual config1 @phase-fabric
set address 11
jump 28 notEqual config1 @surge-alloy
set address 12
jump 30 notEqual config1 @spore-pod
set address 13
jump 32 notEqual config1 @blast-compound
set address 14
jump 34 notEqual config1 @pyratite
set address 15
jump 36 notEqual config2 @copper
set address 16
jump 38 notEqual config2 @lead
set address 17
jump 40 notEqual config2 @metaglass
set address 18
jump 42 notEqual config2 @graphite
set address 19
jump 44 notEqual config2 @sand
set address 20
jump 46 notEqual config2 @coal
set address 21
jump 48 notEqual config2 @titanium
set address 22
jump 50 notEqual config2 @thorium
set address 23
jump 52 notEqual config2 @scrap
set address 24
jump 54 notEqual config2 @silicon
set address 25
jump 56 notEqual config2 @plastanium
set address 26
jump 58 notEqual config2 @phase-fabric
set address 27
jump 60 notEqual config2 @surge-alloy
set address 28
jump 62 notEqual config2 @spore-pod
set address 29
jump 64 notEqual config2 @blast-compound
set address 30
jump 66 notEqual config2 @pyratite
set address 31
read result cell2 address
control enabled switch1 result 0 0 0
write result cell1 0
```

s2

```
read result cell1 0
jump 3 notEqual result 0
draw clear 255 0 0 0 0 0
jump 5 notEqual result 1
draw clear 0 255 0 0 0 0
drawflush display1
```

s3

```
set p 1
getlink link p
read result cell1 0
control enabled link result 0 0 0
op add p p 1
jump 1 lessThan p @links
```

## SBBus Mini

Версия SBBus - SBBus Mini на 4 канала.

По быстрой версии шины SBBus (SBBus Mini) сигнал проходит путь в 22 передатчика (повторителя) за 2 секунды.

![](./mini__example.png)

### Панель

```
bXNjaAF4nGNgYWBmZmDJS8xNZRC/MP/Chgt7L2y9sPtij0Kwk1NpsYJvZl4mA3dKanFyUWZBSWZ+HgMDA1tOYlJqTjEDS3RuZSwrA1txeWZJcgaQzi8qSS1i4M/NTC7K1y0oyk9OLQaKMbDnAunE9FQG7tzU3PyiSt3k1JwcoDncDCDAxcjACKQYWUEcJhDmAxIzK+a49t3mbTbgcfUVXDVF08bJ2ZrBuYRRLsxT2kmEfaPX8largCP9S4vfb3zKw7DPR9D23pXuRabvmm9/6Dr5UcJAwN/sXaLrujyd0qwvJ4KbJ7KtTw1fbTnDo/32pK1V+pMjy+danPzlnOW15pLntC+2vEGLVJ+lx1sbmjuezGcVuW14gnWdzewb36QSYvk0FK0f8k0Xlpuw/jT/oiyPfJBboa5mBLuakYEZiJlYGBl0UQLwYvOF/RcbgAKbLuwGCu29sONiP1Ko6kG8CzaICWwQyPPMUBFmsAgwZoAYKA4Ah0+ItQ==
```

```
set p 0
getlink link p
sensor result link @enabled
op sub temp1 p 1
write result cell1 temp1
op add p p 1
op add temp2 @links 1
jump 1 lessThan p temp2
```

### Считыватель

Остался таким же.

### Передатчик

```
bXNjaAF4nGNgZGBiZmDJS8xNZZC/MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRarOCbmZfJwJ2SWpxclFlQkpmfx8DAwJaTmJSaU8zAEp1bGcvEwJ+bmVyUr1tQlJ+cWlycX8TAngukE9NTgUqZGECAD4iLKua49l3kbTbgcbkc71+obLKI2YCF22Urq4jzWosV0SVpHiotOnePX748V16xZb93o+IlDdfnuY7ci7sk/U9Nkoisud60fYWbwd9PMU+azqb/khIyfuX6683qhc1dvw2Wvk1Z773B7FpLBXfbvm8Wc+VbmdnP6BUxMALtZWRhZCgm4EE9LqCCfUDJXRd2X+wDSV9surBVAUg1Ahn7gAJ7QTp0FC5sB+kHmrNH4cJ+bDo2Xey+2AqS0GMAAH73pe8=
```

```
set p 1
getlink link p
set d 0
read result cell1 d
write result link d
op add d d 1
jump 3 lessThan d 4
op add p p 1
jump 1 lessThan p @links
```


### Клиент

```
bXNjaAF4nGNgYmBmZmDJS8xNZRC/MOvC7gs7Lmy9sPdik0Kwk1NpsYJvZl4mA3dKanFyUWZBSWZ+HgMDA1tOYlJqTjEDS3RuZSwLA39uZnJRvm5BUX5yanFxfhEDG5AoSS1iYM8F8hPTUxm4c1Nz84sqdZNTc3KA+lkZQIAPiNdWzEm9cJbrkAEPw4MwgYX+E1dvL3U+Mltcfsm6wtkpubnW3365vT5gWHTy/HQRrdYJx1v0fnKsLe9fyOxn7MZ7PWj1cxO2jAM/a6p928SOPRYwWNUi2bNVMLhp1YPLYsJSuxftuvB5Wt8MX3e1pVPXd+/PqRX3fdHeo31vxQl9pufCqRkTV8SldYkXf2F5cWbuBadZ7Xe+VR28qn5F5ueT//ueLRNIUv9238uj7/D79Tv077On5JxjYAQ6mRHseiYQZmFkmIUjyPS4Lsy/sO/Clgu7Luy+2Hex/cKGCzsvNl3YqmCocGH/xYYL+y62Xdh6sfFiI5DVoHBhl8LFDqApey9sxanxYjNY44YLm4AS/UAL9wCVbQVpNcJi5MVmPZBbIaGcUzFHt/cub4MCT8vDg9P9CpVfsPE9ZNLorRflOPqX1XT6lunPfs01PbaiyPGQg7b4zcOd5Sqn3tgYvdZl5e7meZHZufCJxoMHaYn/Xf/73HcxPFgZX9lbcSc8ViBsrpn4q9wcea+t12a9W2r2m8HWVkOBgRloLdBiADvMFwY=
```

s1

```
sensor config sorter1 @config
jump 3 notEqual config @copper
set address 0
jump 5 notEqual config @lead
set address 1
jump 7 notEqual config @metaglass
set address 2
jump 9 notEqual config @graphite
set address 3
read result cell2 address
control enabled switch1 result 0 0 0
write result cell1 0
```

s2

```
set p 1
getlink link p
read result cell1 0
control enabled link result 0 0 0
op add p p 1
jump 1 lessThan p @links
```

## SBBus 256

Версия SBBus - SBBus 256 - на 16 блоков по 16 каналов. Итого 256 каналов.

![](./256__example.png)

генерация клиента

```
for (let j = 0; j < 16; j++) {
  console.log(['copper', 'lead', 'metaglass', 'graphite', 'sand', 'coal', 'titanium', 'thorium', 'scrap', 'silicon', 'plastanium', 'phase-fabric', 'surge-alloy', 'spore-pod', 'blast-compound', 'pyratite'].map((elem, i) => `jump ${18+j*16*2+(i*2)} notEqual config${j+1} @${elem}__LLOLOLO__set address ${j*16+i}`).join('__LLOLOLO__')) // ЗАМЕНИТЬ __LLOLOLO__ на переаод строки
}
```

## Панель

```
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
```


```
set p 0
getlink link p
sensor result link @enabled
op sub temp1 p 1
write result bank1 temp1
op add p p 1
op add temp2 @links 1
jump 1 lessThan p temp2

```

### Считыватель

```
bXNjaAF4nGNgYWBmZmDJS8xNZVC4sPBi+4UdF5sudl/YdGHDxaYLWy/svtijEOzkVFqsYGRqxsCdklqcXJRZUJKZn8fAwMCWk5iUmlPMwBKdWxnLzMCbk1lYmpmiW5xfWpScysCem1pcnJieysCfUVmQWqRbUJSfDBTJLwLqZGYAAVag5QyMQAYTCyPjhLzSnJxRPHgwAxMQMvIBoye9Yo5p70FeJ0Me58vSp0TkGpUOqvA4BDDLv9APvLyO34XJb9r8+U9cXNSvMx6ettvLMXx+6QOdtxMTc/5eO8b/6bLC0pbsEzXzs1lW7ZIXzzxY9vvw9f1XXnJfi3iyauZj5YvP4u/re8kvcFBtZQAA23IKuA==
```

```
set p 0
read result bank1 p
print result
op add p p 1
jump 1 lessThan p 256
printflush message1
```

### Передатчик

```
bXNjaAF4nGNgYWBmZmDJS8xNZZC7MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRarGBkasbAnZJanFyUWVCSmZ/HwMDAlpOYlJpTzMASnVsZy8zAm5NZWJqZolucX1qUnMrAnptaXJyYnsrAn1FZkFqkW1CUnwwUyS8C6mRmAAFWoNUMjEAGEwsjQxF+u/W4gPL7gHK7Luy+2AeSvdh0YasCkGoEMvYBBfaCNOgoXNgO0g40Zo/Chf3YdGy62H2xFSShx8AEhIx8QAeUVsxx7bvI22zA43J4/fIdgh6BP9M69CacClvYknDUMXax8nQXp6lLf1dU7Sp+Puf3LBENm71LjqiuzVgYYrh4uU7jxKN9ER94Mr8m/Hqy9ATr7PNbtJmMX1VWyc9OchDZfFzm0sm87x+Dtpw1Pfpf9GjI7J5z8+/wx3Ho3WQAAL4YsR0=
```

```
set p 1
getlink link p
set d 0
read result bank1 d
write result link d
op add d d 1
jump 3 lessThan d 256
op add p p 1
jump 1 lessThan p @links
```


### Клиент

```
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
```

s1

```
sensor config1 sorter1 @config
sensor config2 sorter2 @config
sensor config3 sorter3 @config
sensor config4 sorter4 @config
sensor config5 sorter5 @config
sensor config6 sorter6 @config
sensor config7 sorter7 @config
sensor config8 sorter8 @config
sensor config9 sorter9 @config
sensor config10 sorter10 @config
sensor config11 sorter11 @config
sensor config12 sorter12 @config
sensor config13 sorter13 @config
sensor config14 sorter14 @config
sensor config15 sorter15 @config
sensor config16 sorter16 @config
jump 18 notEqual config1 @copper
set address 0
jump 20 notEqual config1 @lead
set address 1
jump 22 notEqual config1 @metaglass
set address 2
jump 24 notEqual config1 @graphite
set address 3
jump 26 notEqual config1 @sand
set address 4
jump 28 notEqual config1 @coal
set address 5
jump 30 notEqual config1 @titanium
set address 6
jump 32 notEqual config1 @thorium
set address 7
jump 34 notEqual config1 @scrap
set address 8
jump 36 notEqual config1 @silicon
set address 9
jump 38 notEqual config1 @plastanium
set address 10
jump 40 notEqual config1 @phase-fabric
set address 11
jump 42 notEqual config1 @surge-alloy
set address 12
jump 44 notEqual config1 @spore-pod
set address 13
jump 46 notEqual config1 @blast-compound
set address 14
jump 48 notEqual config1 @pyratite
set address 15
jump 50 notEqual config2 @copper
set address 16
jump 52 notEqual config2 @lead
set address 17
jump 54 notEqual config2 @metaglass
set address 18
jump 56 notEqual config2 @graphite
set address 19
jump 58 notEqual config2 @sand
set address 20
jump 60 notEqual config2 @coal
set address 21
jump 62 notEqual config2 @titanium
set address 22
jump 64 notEqual config2 @thorium
set address 23
jump 66 notEqual config2 @scrap
set address 24
jump 68 notEqual config2 @silicon
set address 25
jump 70 notEqual config2 @plastanium
set address 26
jump 72 notEqual config2 @phase-fabric
set address 27
jump 74 notEqual config2 @surge-alloy
set address 28
jump 76 notEqual config2 @spore-pod
set address 29
jump 78 notEqual config2 @blast-compound
set address 30
jump 80 notEqual config2 @pyratite
set address 31
jump 82 notEqual config3 @copper
set address 32
jump 84 notEqual config3 @lead
set address 33
jump 86 notEqual config3 @metaglass
set address 34
jump 88 notEqual config3 @graphite
set address 35
jump 90 notEqual config3 @sand
set address 36
jump 92 notEqual config3 @coal
set address 37
jump 94 notEqual config3 @titanium
set address 38
jump 96 notEqual config3 @thorium
set address 39
jump 98 notEqual config3 @scrap
set address 40
jump 100 notEqual config3 @silicon
set address 41
jump 102 notEqual config3 @plastanium
set address 42
jump 104 notEqual config3 @phase-fabric
set address 43
jump 106 notEqual config3 @surge-alloy
set address 44
jump 108 notEqual config3 @spore-pod
set address 45
jump 110 notEqual config3 @blast-compound
set address 46
jump 112 notEqual config3 @pyratite
set address 47
jump 114 notEqual config4 @copper
set address 48
jump 116 notEqual config4 @lead
set address 49
jump 118 notEqual config4 @metaglass
set address 50
jump 120 notEqual config4 @graphite
set address 51
jump 122 notEqual config4 @sand
set address 52
jump 124 notEqual config4 @coal
set address 53
jump 126 notEqual config4 @titanium
set address 54
jump 128 notEqual config4 @thorium
set address 55
jump 130 notEqual config4 @scrap
set address 56
jump 132 notEqual config4 @silicon
set address 57
jump 134 notEqual config4 @plastanium
set address 58
jump 136 notEqual config4 @phase-fabric
set address 59
jump 138 notEqual config4 @surge-alloy
set address 60
jump 140 notEqual config4 @spore-pod
set address 61
jump 142 notEqual config4 @blast-compound
set address 62
jump 144 notEqual config4 @pyratite
set address 63
jump 146 notEqual config5 @copper
set address 64
jump 148 notEqual config5 @lead
set address 65
jump 150 notEqual config5 @metaglass
set address 66
jump 152 notEqual config5 @graphite
set address 67
jump 154 notEqual config5 @sand
set address 68
jump 156 notEqual config5 @coal
set address 69
jump 158 notEqual config5 @titanium
set address 70
jump 160 notEqual config5 @thorium
set address 71
jump 162 notEqual config5 @scrap
set address 72
jump 164 notEqual config5 @silicon
set address 73
jump 166 notEqual config5 @plastanium
set address 74
jump 168 notEqual config5 @phase-fabric
set address 75
jump 170 notEqual config5 @surge-alloy
set address 76
jump 172 notEqual config5 @spore-pod
set address 77
jump 174 notEqual config5 @blast-compound
set address 78
jump 176 notEqual config5 @pyratite
set address 79
jump 178 notEqual config6 @copper
set address 80
jump 180 notEqual config6 @lead
set address 81
jump 182 notEqual config6 @metaglass
set address 82
jump 184 notEqual config6 @graphite
set address 83
jump 186 notEqual config6 @sand
set address 84
jump 188 notEqual config6 @coal
set address 85
jump 190 notEqual config6 @titanium
set address 86
jump 192 notEqual config6 @thorium
set address 87
jump 194 notEqual config6 @scrap
set address 88
jump 196 notEqual config6 @silicon
set address 89
jump 198 notEqual config6 @plastanium
set address 90
jump 200 notEqual config6 @phase-fabric
set address 91
jump 202 notEqual config6 @surge-alloy
set address 92
jump 204 notEqual config6 @spore-pod
set address 93
jump 206 notEqual config6 @blast-compound
set address 94
jump 208 notEqual config6 @pyratite
set address 95
jump 210 notEqual config7 @copper
set address 96
jump 212 notEqual config7 @lead
set address 97
jump 214 notEqual config7 @metaglass
set address 98
jump 216 notEqual config7 @graphite
set address 99
jump 218 notEqual config7 @sand
set address 100
jump 220 notEqual config7 @coal
set address 101
jump 222 notEqual config7 @titanium
set address 102
jump 224 notEqual config7 @thorium
set address 103
jump 226 notEqual config7 @scrap
set address 104
jump 228 notEqual config7 @silicon
set address 105
jump 230 notEqual config7 @plastanium
set address 106
jump 232 notEqual config7 @phase-fabric
set address 107
jump 234 notEqual config7 @surge-alloy
set address 108
jump 236 notEqual config7 @spore-pod
set address 109
jump 238 notEqual config7 @blast-compound
set address 110
jump 240 notEqual config7 @pyratite
set address 111
jump 242 notEqual config8 @copper
set address 112
jump 244 notEqual config8 @lead
set address 113
jump 246 notEqual config8 @metaglass
set address 114
jump 248 notEqual config8 @graphite
set address 115
jump 250 notEqual config8 @sand
set address 116
jump 252 notEqual config8 @coal
set address 117
jump 254 notEqual config8 @titanium
set address 118
jump 256 notEqual config8 @thorium
set address 119
jump 258 notEqual config8 @scrap
set address 120
jump 260 notEqual config8 @silicon
set address 121
jump 262 notEqual config8 @plastanium
set address 122
jump 264 notEqual config8 @phase-fabric
set address 123
jump 266 notEqual config8 @surge-alloy
set address 124
jump 268 notEqual config8 @spore-pod
set address 125
jump 270 notEqual config8 @blast-compound
set address 126
jump 272 notEqual config8 @pyratite
set address 127
jump 274 notEqual config9 @copper
set address 128
jump 276 notEqual config9 @lead
set address 129
jump 278 notEqual config9 @metaglass
set address 130
jump 280 notEqual config9 @graphite
set address 131
jump 282 notEqual config9 @sand
set address 132
jump 284 notEqual config9 @coal
set address 133
jump 286 notEqual config9 @titanium
set address 134
jump 288 notEqual config9 @thorium
set address 135
jump 290 notEqual config9 @scrap
set address 136
jump 292 notEqual config9 @silicon
set address 137
jump 294 notEqual config9 @plastanium
set address 138
jump 296 notEqual config9 @phase-fabric
set address 139
jump 298 notEqual config9 @surge-alloy
set address 140
jump 300 notEqual config9 @spore-pod
set address 141
jump 302 notEqual config9 @blast-compound
set address 142
jump 304 notEqual config9 @pyratite
set address 143
jump 306 notEqual config10 @copper
set address 144
jump 308 notEqual config10 @lead
set address 145
jump 310 notEqual config10 @metaglass
set address 146
jump 312 notEqual config10 @graphite
set address 147
jump 314 notEqual config10 @sand
set address 148
jump 316 notEqual config10 @coal
set address 149
jump 318 notEqual config10 @titanium
set address 150
jump 320 notEqual config10 @thorium
set address 151
jump 322 notEqual config10 @scrap
set address 152
jump 324 notEqual config10 @silicon
set address 153
jump 326 notEqual config10 @plastanium
set address 154
jump 328 notEqual config10 @phase-fabric
set address 155
jump 330 notEqual config10 @surge-alloy
set address 156
jump 332 notEqual config10 @spore-pod
set address 157
jump 334 notEqual config10 @blast-compound
set address 158
jump 336 notEqual config10 @pyratite
set address 159
jump 338 notEqual config11 @copper
set address 160
jump 340 notEqual config11 @lead
set address 161
jump 342 notEqual config11 @metaglass
set address 162
jump 344 notEqual config11 @graphite
set address 163
jump 346 notEqual config11 @sand
set address 164
jump 348 notEqual config11 @coal
set address 165
jump 350 notEqual config11 @titanium
set address 166
jump 352 notEqual config11 @thorium
set address 167
jump 354 notEqual config11 @scrap
set address 168
jump 356 notEqual config11 @silicon
set address 169
jump 358 notEqual config11 @plastanium
set address 170
jump 360 notEqual config11 @phase-fabric
set address 171
jump 362 notEqual config11 @surge-alloy
set address 172
jump 364 notEqual config11 @spore-pod
set address 173
jump 366 notEqual config11 @blast-compound
set address 174
jump 368 notEqual config11 @pyratite
set address 175
jump 370 notEqual config12 @copper
set address 176
jump 372 notEqual config12 @lead
set address 177
jump 374 notEqual config12 @metaglass
set address 178
jump 376 notEqual config12 @graphite
set address 179
jump 378 notEqual config12 @sand
set address 180
jump 380 notEqual config12 @coal
set address 181
jump 382 notEqual config12 @titanium
set address 182
jump 384 notEqual config12 @thorium
set address 183
jump 386 notEqual config12 @scrap
set address 184
jump 388 notEqual config12 @silicon
set address 185
jump 390 notEqual config12 @plastanium
set address 186
jump 392 notEqual config12 @phase-fabric
set address 187
jump 394 notEqual config12 @surge-alloy
set address 188
jump 396 notEqual config12 @spore-pod
set address 189
jump 398 notEqual config12 @blast-compound
set address 190
jump 400 notEqual config12 @pyratite
set address 191
jump 402 notEqual config13 @copper
set address 192
jump 404 notEqual config13 @lead
set address 193
jump 406 notEqual config13 @metaglass
set address 194
jump 408 notEqual config13 @graphite
set address 195
jump 410 notEqual config13 @sand
set address 196
jump 412 notEqual config13 @coal
set address 197
jump 414 notEqual config13 @titanium
set address 198
jump 416 notEqual config13 @thorium
set address 199
jump 418 notEqual config13 @scrap
set address 200
jump 420 notEqual config13 @silicon
set address 201
jump 422 notEqual config13 @plastanium
set address 202
jump 424 notEqual config13 @phase-fabric
set address 203
jump 426 notEqual config13 @surge-alloy
set address 204
jump 428 notEqual config13 @spore-pod
set address 205
jump 430 notEqual config13 @blast-compound
set address 206
jump 432 notEqual config13 @pyratite
set address 207
jump 434 notEqual config14 @copper
set address 208
jump 436 notEqual config14 @lead
set address 209
jump 438 notEqual config14 @metaglass
set address 210
jump 440 notEqual config14 @graphite
set address 211
jump 442 notEqual config14 @sand
set address 212
jump 444 notEqual config14 @coal
set address 213
jump 446 notEqual config14 @titanium
set address 214
jump 448 notEqual config14 @thorium
set address 215
jump 450 notEqual config14 @scrap
set address 216
jump 452 notEqual config14 @silicon
set address 217
jump 454 notEqual config14 @plastanium
set address 218
jump 456 notEqual config14 @phase-fabric
set address 219
jump 458 notEqual config14 @surge-alloy
set address 220
jump 460 notEqual config14 @spore-pod
set address 221
jump 462 notEqual config14 @blast-compound
set address 222
jump 464 notEqual config14 @pyratite
set address 223
jump 466 notEqual config15 @copper
set address 224
jump 468 notEqual config15 @lead
set address 225
jump 470 notEqual config15 @metaglass
set address 226
jump 472 notEqual config15 @graphite
set address 227
jump 474 notEqual config15 @sand
set address 228
jump 476 notEqual config15 @coal
set address 229
jump 478 notEqual config15 @titanium
set address 230
jump 480 notEqual config15 @thorium
set address 231
jump 482 notEqual config15 @scrap
set address 232
jump 484 notEqual config15 @silicon
set address 233
jump 486 notEqual config15 @plastanium
set address 234
jump 488 notEqual config15 @phase-fabric
set address 235
jump 490 notEqual config15 @surge-alloy
set address 236
jump 492 notEqual config15 @spore-pod
set address 237
jump 494 notEqual config15 @blast-compound
set address 238
jump 496 notEqual config15 @pyratite
set address 239
jump 498 notEqual config16 @copper
set address 240
jump 500 notEqual config16 @lead
set address 241
jump 502 notEqual config16 @metaglass
set address 242
jump 504 notEqual config16 @graphite
set address 243
jump 506 notEqual config16 @sand
set address 244
jump 508 notEqual config16 @coal
set address 245
jump 510 notEqual config16 @titanium
set address 246
jump 512 notEqual config16 @thorium
set address 247
jump 514 notEqual config16 @scrap
set address 248
jump 516 notEqual config16 @silicon
set address 249
jump 518 notEqual config16 @plastanium
set address 250
jump 520 notEqual config16 @phase-fabric
set address 251
jump 522 notEqual config16 @surge-alloy
set address 252
jump 524 notEqual config16 @spore-pod
set address 253
jump 526 notEqual config16 @blast-compound
set address 254
jump 528 notEqual config16 @pyratite
set address 255
read result bank1 address
control enabled switch1 result 0 0 0
write result cell1 0

```

s2

```
read result cell1 0
jump 3 notEqual result 0
draw clear 255 0 0 0 0 0
jump 5 notEqual result 1
draw clear 0 255 0 0 0 0
drawflush display1
```

s3

```
set p 1
getlink link p
read result cell1 0
control enabled link result 0 0 0
op add p p 1
jump 1 lessThan p @links
```


















## SBBus 512

Версия SBBus - SBBus 512 - на 32 блока по 16 каналов. Итого 512 каналов.

![](./512__example.png)

генерация клиента

```
for (let j = 0; j < 16; j++) {
  console.log(['copper', 'lead', 'metaglass', 'graphite', 'sand', 'coal', 'titanium', 'thorium', 'scrap', 'silicon', 'plastanium', 'phase-fabric', 'surge-alloy', 'spore-pod', 'blast-compound', 'pyratite'].map((elem, i) => `jump ${35+j*16*2+(i*2)} notEqual config${j+1} @${elem}__LLOLOLO__set address ${j*16+i}`).join('__LLOLOLO__')) // ЗАМЕНИТЬ __LLOLOLO__ на переаод строки
}


for (let j = 16; j < 32; j++) {
  console.log(['copper', 'lead', 'metaglass', 'graphite', 'sand', 'coal', 'titanium', 'thorium', 'scrap', 'silicon', 'plastanium', 'phase-fabric', 'surge-alloy', 'spore-pod', 'blast-compound', 'pyratite'].map((elem, i) => `jump ${35+(j-16)*16*2+(i*2)} notEqual config${j+1} @${elem}__LLOLOLO__set address ${j*16+i}`).join('__LLOLOLO__')) // ЗАМЕНИТЬ __LLOLOLO__ на переаод строки
}
```

## Панель

```
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
```


```
set p 0
getlink link p
sensor result link @enabled
op sub temp1 p 1
write result bank1 temp1
op add p p 1
op add temp2 @links 1
jump 1 lessThan p temp2

```

### Считыватель-панель

```
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
```

```
set p 0
getlink link p
read result bank1 p
op sub temp1 p 1
control enabled link result 0 0 0
op add p p 1
op add temp2 @links 1
jump 1 lessThan p temp2
```

### Дисплейный сканер SBBus 512

![](./512__display_reader.png)

```
bXNjaAF4nGNgY+BiZmDJS8xNZdC+MOXCjouNF/Zf2H1h64WdF/Ze7L6wUwEosOvChgt7L2y92KAQ7ORUWqxgamjEwJ2SWpxclFlQkpmfx8DAwJaTmJSaU8zAEp1bGcvCIJyTWJSeqpuTn56ZrJuSWVyQk1jJwJ9RWZBapFtQlJ+cWlycX8TAm5NZWJqZolucX1qUnMrAngsUTkxPBRrHysDABIQMjEDIzgekAyrmpAZ5+x02ECiNDLU8ukJ9Rfcdrm9v1x1YpLOrRGo625wjN/hyy2JapRmEhJgOSp6p3MVQn3SradGJz5XGn5/dlG3pWzZzSXZEgZvql/L4RTPYLs6bbbJ1WooJ88mQs6ZLtuw5qDDJq2FV8IU1AtdY58Rcb20QnDJV7v61Ke419pzJWnGeEgKP2rekr7D8Gd78PVvJ6tqNg65nEzd/fNKx/KZJ+vTgA87Tz3za/WC+/zHj02du6218MjX3++xZH7L4n+tKFznMSmXf0H1YaQ7HzOlSVc8O7pnp/jkxbv+7s8sr+bZVMn5OuZd7QM1/4fVF/FJtNyZdz2JlDe6KM5QRL+4697yeY8KK8ssMcrzRARM8N7WWFd0QaVwwsbv9XeQ6luW8fdWc9eFrH7OU1FdXMjPdmTRzbcbLw4477xp/WPBY1o3hYHOKb3HuT8XfiwLM9ZJzW3YVWryqya9nuB5zgR0UugycrCwMzGDIzsLIoH5hITSqd1xsuLDvwiYI+8JWhQsbgUliH0jSSsHYCKyBA6iBpAQDAAJ6FhY=
```

```
draw clear 0 0 0 0 0 0
set p 0
set xbb 0
read result bank1 p
op sub temp1 p 1
jump 7 notEqual result 0
draw color 255 0 0 255 0 0
jump 9 notEqual result 1
draw color 0 255 0 255 0 0
op mul xx xbb 5
set yyNUM 16
op div yyNUMOFET p yyNUM
op floor yyNUMOFETFlo yyNUMOFET yyNUMFlo
op add yyNUMOFETFloP yyNUMOFETFlo 1
print "Сканирование блока: "
print yyNUMOFETFloP
printflush message1
op mul tempYY yyNUMOFETFloP 5
op sub yy 176 tempYY
draw rect xx yy 5 5 0 0
drawflush display1
op add p p 1
op add xbb xbb 1
jump 25 lessThan xbb yyNUM
set xbb 0
jump 3 lessThan p 512
wait 5
```

### Передатчик

```
bXNjaAF4nGNgYWBmZmDJS8xNZZC7MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRarGBqaMTAnZJanFyUWVCSmZ/HwMDAlpOYlJpTzMASnVsZy8zAm5NZWJqZolucX1qUnMrAnptaXJyYnsrAn1FZkFqkW1CUnwwUyS8C6mRmAAFWoNUMjEAGEwsjQxF+u/W4gPL7gHK7Luy+2AeSvdh0YasCkGoEMvYBBfaCNOgoXNgO0g40Zo/Chf3YdGy62H2xFSShx8AEhIx8QAeUVMxx7bvIediAx2VuvG+hcgjv3/cCsQdclTwfWx0qeiElu3OjosjBWhu5ciknjvjrXMyXl5jqVrryL25jFdeSYnWt9Rc9PyO87cJynVD/G7ULzwq4Xuh7uXU/r/KkXfbPZvCXPX69MmL+a67/oof3mlrK2rfKx+rpXWEAAKFjppk=
```

```
set p 1
getlink link p
set d 0
read result bank1 d
write result link d
op add d d 1
jump 3 lessThan d 512
op add p p 1
jump 1 lessThan p @links
```

### Клиент

```
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
```

s1

```
set address -999
sensor config1 sorter1 @config
sensor config2 sorter2 @config
sensor config3 sorter3 @config
sensor config4 sorter4 @config
sensor config5 sorter5 @config
sensor config6 sorter6 @config
sensor config7 sorter7 @config
sensor config8 sorter8 @config
sensor config9 sorter9 @config
sensor config10 sorter10 @config
sensor config11 sorter11 @config
sensor config12 sorter12 @config
sensor config13 sorter13 @config
sensor config14 sorter14 @config
sensor config15 sorter15 @config
sensor config16 sorter16 @config
sensor config17 sorter17 @config
sensor config18 sorter18 @config
sensor config19 sorter19 @config
sensor config20 sorter20 @config
sensor config21 sorter21 @config
sensor config22 sorter22 @config
sensor config23 sorter23 @config
sensor config24 sorter24 @config
sensor config25 sorter25 @config
sensor config26 sorter26 @config
sensor config27 sorter27 @config
sensor config28 sorter28 @config
sensor config29 sorter29 @config
sensor config30 sorter30 @config
sensor config31 sorter31 @config
sensor config32 sorter32 @config
jump 35 notEqual config1 @copper
set address 0
jump 37 notEqual config1 @lead
set address 1
jump 39 notEqual config1 @metaglass
set address 2
jump 41 notEqual config1 @graphite
set address 3
jump 43 notEqual config1 @sand
set address 4
jump 45 notEqual config1 @coal
set address 5
jump 47 notEqual config1 @titanium
set address 6
jump 49 notEqual config1 @thorium
set address 7
jump 51 notEqual config1 @scrap
set address 8
jump 53 notEqual config1 @silicon
set address 9
jump 55 notEqual config1 @plastanium
set address 10
jump 57 notEqual config1 @phase-fabric
set address 11
jump 59 notEqual config1 @surge-alloy
set address 12
jump 61 notEqual config1 @spore-pod
set address 13
jump 63 notEqual config1 @blast-compound
set address 14
jump 65 notEqual config1 @pyratite
set address 15
jump 67 notEqual config2 @copper
set address 16
jump 69 notEqual config2 @lead
set address 17
jump 71 notEqual config2 @metaglass
set address 18
jump 73 notEqual config2 @graphite
set address 19
jump 75 notEqual config2 @sand
set address 20
jump 77 notEqual config2 @coal
set address 21
jump 79 notEqual config2 @titanium
set address 22
jump 81 notEqual config2 @thorium
set address 23
jump 83 notEqual config2 @scrap
set address 24
jump 85 notEqual config2 @silicon
set address 25
jump 87 notEqual config2 @plastanium
set address 26
jump 89 notEqual config2 @phase-fabric
set address 27
jump 91 notEqual config2 @surge-alloy
set address 28
jump 93 notEqual config2 @spore-pod
set address 29
jump 95 notEqual config2 @blast-compound
set address 30
jump 97 notEqual config2 @pyratite
set address 31
jump 99 notEqual config3 @copper
set address 32
jump 101 notEqual config3 @lead
set address 33
jump 103 notEqual config3 @metaglass
set address 34
jump 105 notEqual config3 @graphite
set address 35
jump 107 notEqual config3 @sand
set address 36
jump 109 notEqual config3 @coal
set address 37
jump 111 notEqual config3 @titanium
set address 38
jump 113 notEqual config3 @thorium
set address 39
jump 115 notEqual config3 @scrap
set address 40
jump 117 notEqual config3 @silicon
set address 41
jump 119 notEqual config3 @plastanium
set address 42
jump 121 notEqual config3 @phase-fabric
set address 43
jump 123 notEqual config3 @surge-alloy
set address 44
jump 125 notEqual config3 @spore-pod
set address 45
jump 127 notEqual config3 @blast-compound
set address 46
jump 129 notEqual config3 @pyratite
set address 47
jump 131 notEqual config4 @copper
set address 48
jump 133 notEqual config4 @lead
set address 49
jump 135 notEqual config4 @metaglass
set address 50
jump 137 notEqual config4 @graphite
set address 51
jump 139 notEqual config4 @sand
set address 52
jump 141 notEqual config4 @coal
set address 53
jump 143 notEqual config4 @titanium
set address 54
jump 145 notEqual config4 @thorium
set address 55
jump 147 notEqual config4 @scrap
set address 56
jump 149 notEqual config4 @silicon
set address 57
jump 151 notEqual config4 @plastanium
set address 58
jump 153 notEqual config4 @phase-fabric
set address 59
jump 155 notEqual config4 @surge-alloy
set address 60
jump 157 notEqual config4 @spore-pod
set address 61
jump 159 notEqual config4 @blast-compound
set address 62
jump 161 notEqual config4 @pyratite
set address 63
jump 163 notEqual config5 @copper
set address 64
jump 165 notEqual config5 @lead
set address 65
jump 167 notEqual config5 @metaglass
set address 66
jump 169 notEqual config5 @graphite
set address 67
jump 171 notEqual config5 @sand
set address 68
jump 173 notEqual config5 @coal
set address 69
jump 175 notEqual config5 @titanium
set address 70
jump 177 notEqual config5 @thorium
set address 71
jump 179 notEqual config5 @scrap
set address 72
jump 181 notEqual config5 @silicon
set address 73
jump 183 notEqual config5 @plastanium
set address 74
jump 185 notEqual config5 @phase-fabric
set address 75
jump 187 notEqual config5 @surge-alloy
set address 76
jump 189 notEqual config5 @spore-pod
set address 77
jump 191 notEqual config5 @blast-compound
set address 78
jump 193 notEqual config5 @pyratite
set address 79
jump 195 notEqual config6 @copper
set address 80
jump 197 notEqual config6 @lead
set address 81
jump 199 notEqual config6 @metaglass
set address 82
jump 201 notEqual config6 @graphite
set address 83
jump 203 notEqual config6 @sand
set address 84
jump 205 notEqual config6 @coal
set address 85
jump 207 notEqual config6 @titanium
set address 86
jump 209 notEqual config6 @thorium
set address 87
jump 211 notEqual config6 @scrap
set address 88
jump 213 notEqual config6 @silicon
set address 89
jump 215 notEqual config6 @plastanium
set address 90
jump 217 notEqual config6 @phase-fabric
set address 91
jump 219 notEqual config6 @surge-alloy
set address 92
jump 221 notEqual config6 @spore-pod
set address 93
jump 223 notEqual config6 @blast-compound
set address 94
jump 225 notEqual config6 @pyratite
set address 95
jump 227 notEqual config7 @copper
set address 96
jump 229 notEqual config7 @lead
set address 97
jump 231 notEqual config7 @metaglass
set address 98
jump 233 notEqual config7 @graphite
set address 99
jump 235 notEqual config7 @sand
set address 100
jump 237 notEqual config7 @coal
set address 101
jump 239 notEqual config7 @titanium
set address 102
jump 241 notEqual config7 @thorium
set address 103
jump 243 notEqual config7 @scrap
set address 104
jump 245 notEqual config7 @silicon
set address 105
jump 247 notEqual config7 @plastanium
set address 106
jump 249 notEqual config7 @phase-fabric
set address 107
jump 251 notEqual config7 @surge-alloy
set address 108
jump 253 notEqual config7 @spore-pod
set address 109
jump 255 notEqual config7 @blast-compound
set address 110
jump 257 notEqual config7 @pyratite
set address 111
jump 259 notEqual config8 @copper
set address 112
jump 261 notEqual config8 @lead
set address 113
jump 263 notEqual config8 @metaglass
set address 114
jump 265 notEqual config8 @graphite
set address 115
jump 267 notEqual config8 @sand
set address 116
jump 269 notEqual config8 @coal
set address 117
jump 271 notEqual config8 @titanium
set address 118
jump 273 notEqual config8 @thorium
set address 119
jump 275 notEqual config8 @scrap
set address 120
jump 277 notEqual config8 @silicon
set address 121
jump 279 notEqual config8 @plastanium
set address 122
jump 281 notEqual config8 @phase-fabric
set address 123
jump 283 notEqual config8 @surge-alloy
set address 124
jump 285 notEqual config8 @spore-pod
set address 125
jump 287 notEqual config8 @blast-compound
set address 126
jump 289 notEqual config8 @pyratite
set address 127
jump 291 notEqual config9 @copper
set address 128
jump 293 notEqual config9 @lead
set address 129
jump 295 notEqual config9 @metaglass
set address 130
jump 297 notEqual config9 @graphite
set address 131
jump 299 notEqual config9 @sand
set address 132
jump 301 notEqual config9 @coal
set address 133
jump 303 notEqual config9 @titanium
set address 134
jump 305 notEqual config9 @thorium
set address 135
jump 307 notEqual config9 @scrap
set address 136
jump 309 notEqual config9 @silicon
set address 137
jump 311 notEqual config9 @plastanium
set address 138
jump 313 notEqual config9 @phase-fabric
set address 139
jump 315 notEqual config9 @surge-alloy
set address 140
jump 317 notEqual config9 @spore-pod
set address 141
jump 319 notEqual config9 @blast-compound
set address 142
jump 321 notEqual config9 @pyratite
set address 143
jump 323 notEqual config10 @copper
set address 144
jump 325 notEqual config10 @lead
set address 145
jump 327 notEqual config10 @metaglass
set address 146
jump 329 notEqual config10 @graphite
set address 147
jump 331 notEqual config10 @sand
set address 148
jump 333 notEqual config10 @coal
set address 149
jump 335 notEqual config10 @titanium
set address 150
jump 337 notEqual config10 @thorium
set address 151
jump 339 notEqual config10 @scrap
set address 152
jump 341 notEqual config10 @silicon
set address 153
jump 343 notEqual config10 @plastanium
set address 154
jump 345 notEqual config10 @phase-fabric
set address 155
jump 347 notEqual config10 @surge-alloy
set address 156
jump 349 notEqual config10 @spore-pod
set address 157
jump 351 notEqual config10 @blast-compound
set address 158
jump 353 notEqual config10 @pyratite
set address 159
jump 355 notEqual config11 @copper
set address 160
jump 357 notEqual config11 @lead
set address 161
jump 359 notEqual config11 @metaglass
set address 162
jump 361 notEqual config11 @graphite
set address 163
jump 363 notEqual config11 @sand
set address 164
jump 365 notEqual config11 @coal
set address 165
jump 367 notEqual config11 @titanium
set address 166
jump 369 notEqual config11 @thorium
set address 167
jump 371 notEqual config11 @scrap
set address 168
jump 373 notEqual config11 @silicon
set address 169
jump 375 notEqual config11 @plastanium
set address 170
jump 377 notEqual config11 @phase-fabric
set address 171
jump 379 notEqual config11 @surge-alloy
set address 172
jump 381 notEqual config11 @spore-pod
set address 173
jump 383 notEqual config11 @blast-compound
set address 174
jump 385 notEqual config11 @pyratite
set address 175
jump 387 notEqual config12 @copper
set address 176
jump 389 notEqual config12 @lead
set address 177
jump 391 notEqual config12 @metaglass
set address 178
jump 393 notEqual config12 @graphite
set address 179
jump 395 notEqual config12 @sand
set address 180
jump 397 notEqual config12 @coal
set address 181
jump 399 notEqual config12 @titanium
set address 182
jump 401 notEqual config12 @thorium
set address 183
jump 403 notEqual config12 @scrap
set address 184
jump 405 notEqual config12 @silicon
set address 185
jump 407 notEqual config12 @plastanium
set address 186
jump 409 notEqual config12 @phase-fabric
set address 187
jump 411 notEqual config12 @surge-alloy
set address 188
jump 413 notEqual config12 @spore-pod
set address 189
jump 415 notEqual config12 @blast-compound
set address 190
jump 417 notEqual config12 @pyratite
set address 191
jump 419 notEqual config13 @copper
set address 192
jump 421 notEqual config13 @lead
set address 193
jump 423 notEqual config13 @metaglass
set address 194
jump 425 notEqual config13 @graphite
set address 195
jump 427 notEqual config13 @sand
set address 196
jump 429 notEqual config13 @coal
set address 197
jump 431 notEqual config13 @titanium
set address 198
jump 433 notEqual config13 @thorium
set address 199
jump 435 notEqual config13 @scrap
set address 200
jump 437 notEqual config13 @silicon
set address 201
jump 439 notEqual config13 @plastanium
set address 202
jump 441 notEqual config13 @phase-fabric
set address 203
jump 443 notEqual config13 @surge-alloy
set address 204
jump 445 notEqual config13 @spore-pod
set address 205
jump 447 notEqual config13 @blast-compound
set address 206
jump 449 notEqual config13 @pyratite
set address 207
jump 451 notEqual config14 @copper
set address 208
jump 453 notEqual config14 @lead
set address 209
jump 455 notEqual config14 @metaglass
set address 210
jump 457 notEqual config14 @graphite
set address 211
jump 459 notEqual config14 @sand
set address 212
jump 461 notEqual config14 @coal
set address 213
jump 463 notEqual config14 @titanium
set address 214
jump 465 notEqual config14 @thorium
set address 215
jump 467 notEqual config14 @scrap
set address 216
jump 469 notEqual config14 @silicon
set address 217
jump 471 notEqual config14 @plastanium
set address 218
jump 473 notEqual config14 @phase-fabric
set address 219
jump 475 notEqual config14 @surge-alloy
set address 220
jump 477 notEqual config14 @spore-pod
set address 221
jump 479 notEqual config14 @blast-compound
set address 222
jump 481 notEqual config14 @pyratite
set address 223
jump 483 notEqual config15 @copper
set address 224
jump 485 notEqual config15 @lead
set address 225
jump 487 notEqual config15 @metaglass
set address 226
jump 489 notEqual config15 @graphite
set address 227
jump 491 notEqual config15 @sand
set address 228
jump 493 notEqual config15 @coal
set address 229
jump 495 notEqual config15 @titanium
set address 230
jump 497 notEqual config15 @thorium
set address 231
jump 499 notEqual config15 @scrap
set address 232
jump 501 notEqual config15 @silicon
set address 233
jump 503 notEqual config15 @plastanium
set address 234
jump 505 notEqual config15 @phase-fabric
set address 235
jump 507 notEqual config15 @surge-alloy
set address 236
jump 509 notEqual config15 @spore-pod
set address 237
jump 511 notEqual config15 @blast-compound
set address 238
jump 513 notEqual config15 @pyratite
set address 239
jump 515 notEqual config16 @copper
set address 240
jump 517 notEqual config16 @lead
set address 241
jump 519 notEqual config16 @metaglass
set address 242
jump 521 notEqual config16 @graphite
set address 243
jump 523 notEqual config16 @sand
set address 244
jump 525 notEqual config16 @coal
set address 245
jump 527 notEqual config16 @titanium
set address 246
jump 529 notEqual config16 @thorium
set address 247
jump 531 notEqual config16 @scrap
set address 248
jump 533 notEqual config16 @silicon
set address 249
jump 535 notEqual config16 @plastanium
set address 250
jump 537 notEqual config16 @phase-fabric
set address 251
jump 539 notEqual config16 @surge-alloy
set address 252
jump 541 notEqual config16 @spore-pod
set address 253
jump 543 notEqual config16 @blast-compound
set address 254
jump 545 notEqual config16 @pyratite
set address 255
jump 548 strictEqual address -999
read result bank1 address
write result cell1 0
end
```

s2

```
set address -999
sensor config1 sorter1 @config
sensor config2 sorter2 @config
sensor config3 sorter3 @config
sensor config4 sorter4 @config
sensor config5 sorter5 @config
sensor config6 sorter6 @config
sensor config7 sorter7 @config
sensor config8 sorter8 @config
sensor config9 sorter9 @config
sensor config10 sorter10 @config
sensor config11 sorter11 @config
sensor config12 sorter12 @config
sensor config13 sorter13 @config
sensor config14 sorter14 @config
sensor config15 sorter15 @config
sensor config16 sorter16 @config
sensor config17 sorter17 @config
sensor config18 sorter18 @config
sensor config19 sorter19 @config
sensor config20 sorter20 @config
sensor config21 sorter21 @config
sensor config22 sorter22 @config
sensor config23 sorter23 @config
sensor config24 sorter24 @config
sensor config25 sorter25 @config
sensor config26 sorter26 @config
sensor config27 sorter27 @config
sensor config28 sorter28 @config
sensor config29 sorter29 @config
sensor config30 sorter30 @config
sensor config31 sorter31 @config
sensor config32 sorter32 @config
jump 35 notEqual config17 @copper
set address 256
jump 37 notEqual config17 @lead
set address 257
jump 39 notEqual config17 @metaglass
set address 258
jump 41 notEqual config17 @graphite
set address 259
jump 43 notEqual config17 @sand
set address 260
jump 45 notEqual config17 @coal
set address 261
jump 47 notEqual config17 @titanium
set address 262
jump 49 notEqual config17 @thorium
set address 263
jump 51 notEqual config17 @scrap
set address 264
jump 53 notEqual config17 @silicon
set address 265
jump 55 notEqual config17 @plastanium
set address 266
jump 57 notEqual config17 @phase-fabric
set address 267
jump 59 notEqual config17 @surge-alloy
set address 268
jump 61 notEqual config17 @spore-pod
set address 269
jump 63 notEqual config17 @blast-compound
set address 270
jump 65 notEqual config17 @pyratite
set address 271
jump 67 notEqual config18 @copper
set address 272
jump 69 notEqual config18 @lead
set address 273
jump 71 notEqual config18 @metaglass
set address 274
jump 73 notEqual config18 @graphite
set address 275
jump 75 notEqual config18 @sand
set address 276
jump 77 notEqual config18 @coal
set address 277
jump 79 notEqual config18 @titanium
set address 278
jump 81 notEqual config18 @thorium
set address 279
jump 83 notEqual config18 @scrap
set address 280
jump 85 notEqual config18 @silicon
set address 281
jump 87 notEqual config18 @plastanium
set address 282
jump 89 notEqual config18 @phase-fabric
set address 283
jump 91 notEqual config18 @surge-alloy
set address 284
jump 93 notEqual config18 @spore-pod
set address 285
jump 95 notEqual config18 @blast-compound
set address 286
jump 97 notEqual config18 @pyratite
set address 287
jump 99 notEqual config19 @copper
set address 288
jump 101 notEqual config19 @lead
set address 289
jump 103 notEqual config19 @metaglass
set address 290
jump 105 notEqual config19 @graphite
set address 291
jump 107 notEqual config19 @sand
set address 292
jump 109 notEqual config19 @coal
set address 293
jump 111 notEqual config19 @titanium
set address 294
jump 113 notEqual config19 @thorium
set address 295
jump 115 notEqual config19 @scrap
set address 296
jump 117 notEqual config19 @silicon
set address 297
jump 119 notEqual config19 @plastanium
set address 298
jump 121 notEqual config19 @phase-fabric
set address 299
jump 123 notEqual config19 @surge-alloy
set address 300
jump 125 notEqual config19 @spore-pod
set address 301
jump 127 notEqual config19 @blast-compound
set address 302
jump 129 notEqual config19 @pyratite
set address 303
jump 131 notEqual config20 @copper
set address 304
jump 133 notEqual config20 @lead
set address 305
jump 135 notEqual config20 @metaglass
set address 306
jump 137 notEqual config20 @graphite
set address 307
jump 139 notEqual config20 @sand
set address 308
jump 141 notEqual config20 @coal
set address 309
jump 143 notEqual config20 @titanium
set address 310
jump 145 notEqual config20 @thorium
set address 311
jump 147 notEqual config20 @scrap
set address 312
jump 149 notEqual config20 @silicon
set address 313
jump 151 notEqual config20 @plastanium
set address 314
jump 153 notEqual config20 @phase-fabric
set address 315
jump 155 notEqual config20 @surge-alloy
set address 316
jump 157 notEqual config20 @spore-pod
set address 317
jump 159 notEqual config20 @blast-compound
set address 318
jump 161 notEqual config20 @pyratite
set address 319
jump 163 notEqual config21 @copper
set address 320
jump 165 notEqual config21 @lead
set address 321
jump 167 notEqual config21 @metaglass
set address 322
jump 169 notEqual config21 @graphite
set address 323
jump 171 notEqual config21 @sand
set address 324
jump 173 notEqual config21 @coal
set address 325
jump 175 notEqual config21 @titanium
set address 326
jump 177 notEqual config21 @thorium
set address 327
jump 179 notEqual config21 @scrap
set address 328
jump 181 notEqual config21 @silicon
set address 329
jump 183 notEqual config21 @plastanium
set address 330
jump 185 notEqual config21 @phase-fabric
set address 331
jump 187 notEqual config21 @surge-alloy
set address 332
jump 189 notEqual config21 @spore-pod
set address 333
jump 191 notEqual config21 @blast-compound
set address 334
jump 193 notEqual config21 @pyratite
set address 335
jump 195 notEqual config22 @copper
set address 336
jump 197 notEqual config22 @lead
set address 337
jump 199 notEqual config22 @metaglass
set address 338
jump 201 notEqual config22 @graphite
set address 339
jump 203 notEqual config22 @sand
set address 340
jump 205 notEqual config22 @coal
set address 341
jump 207 notEqual config22 @titanium
set address 342
jump 209 notEqual config22 @thorium
set address 343
jump 211 notEqual config22 @scrap
set address 344
jump 213 notEqual config22 @silicon
set address 345
jump 215 notEqual config22 @plastanium
set address 346
jump 217 notEqual config22 @phase-fabric
set address 347
jump 219 notEqual config22 @surge-alloy
set address 348
jump 221 notEqual config22 @spore-pod
set address 349
jump 223 notEqual config22 @blast-compound
set address 350
jump 225 notEqual config22 @pyratite
set address 351
jump 227 notEqual config23 @copper
set address 352
jump 229 notEqual config23 @lead
set address 353
jump 231 notEqual config23 @metaglass
set address 354
jump 233 notEqual config23 @graphite
set address 355
jump 235 notEqual config23 @sand
set address 356
jump 237 notEqual config23 @coal
set address 357
jump 239 notEqual config23 @titanium
set address 358
jump 241 notEqual config23 @thorium
set address 359
jump 243 notEqual config23 @scrap
set address 360
jump 245 notEqual config23 @silicon
set address 361
jump 247 notEqual config23 @plastanium
set address 362
jump 249 notEqual config23 @phase-fabric
set address 363
jump 251 notEqual config23 @surge-alloy
set address 364
jump 253 notEqual config23 @spore-pod
set address 365
jump 255 notEqual config23 @blast-compound
set address 366
jump 257 notEqual config23 @pyratite
set address 367
jump 259 notEqual config24 @copper
set address 368
jump 261 notEqual config24 @lead
set address 369
jump 263 notEqual config24 @metaglass
set address 370
jump 265 notEqual config24 @graphite
set address 371
jump 267 notEqual config24 @sand
set address 372
jump 269 notEqual config24 @coal
set address 373
jump 271 notEqual config24 @titanium
set address 374
jump 273 notEqual config24 @thorium
set address 375
jump 275 notEqual config24 @scrap
set address 376
jump 277 notEqual config24 @silicon
set address 377
jump 279 notEqual config24 @plastanium
set address 378
jump 281 notEqual config24 @phase-fabric
set address 379
jump 283 notEqual config24 @surge-alloy
set address 380
jump 285 notEqual config24 @spore-pod
set address 381
jump 287 notEqual config24 @blast-compound
set address 382
jump 289 notEqual config24 @pyratite
set address 383
jump 291 notEqual config25 @copper
set address 384
jump 293 notEqual config25 @lead
set address 385
jump 295 notEqual config25 @metaglass
set address 386
jump 297 notEqual config25 @graphite
set address 387
jump 299 notEqual config25 @sand
set address 388
jump 301 notEqual config25 @coal
set address 389
jump 303 notEqual config25 @titanium
set address 390
jump 305 notEqual config25 @thorium
set address 391
jump 307 notEqual config25 @scrap
set address 392
jump 309 notEqual config25 @silicon
set address 393
jump 311 notEqual config25 @plastanium
set address 394
jump 313 notEqual config25 @phase-fabric
set address 395
jump 315 notEqual config25 @surge-alloy
set address 396
jump 317 notEqual config25 @spore-pod
set address 397
jump 319 notEqual config25 @blast-compound
set address 398
jump 321 notEqual config25 @pyratite
set address 399
jump 323 notEqual config26 @copper
set address 400
jump 325 notEqual config26 @lead
set address 401
jump 327 notEqual config26 @metaglass
set address 402
jump 329 notEqual config26 @graphite
set address 403
jump 331 notEqual config26 @sand
set address 404
jump 333 notEqual config26 @coal
set address 405
jump 335 notEqual config26 @titanium
set address 406
jump 337 notEqual config26 @thorium
set address 407
jump 339 notEqual config26 @scrap
set address 408
jump 341 notEqual config26 @silicon
set address 409
jump 343 notEqual config26 @plastanium
set address 410
jump 345 notEqual config26 @phase-fabric
set address 411
jump 347 notEqual config26 @surge-alloy
set address 412
jump 349 notEqual config26 @spore-pod
set address 413
jump 351 notEqual config26 @blast-compound
set address 414
jump 353 notEqual config26 @pyratite
set address 415
jump 355 notEqual config27 @copper
set address 416
jump 357 notEqual config27 @lead
set address 417
jump 359 notEqual config27 @metaglass
set address 418
jump 361 notEqual config27 @graphite
set address 419
jump 363 notEqual config27 @sand
set address 420
jump 365 notEqual config27 @coal
set address 421
jump 367 notEqual config27 @titanium
set address 422
jump 369 notEqual config27 @thorium
set address 423
jump 371 notEqual config27 @scrap
set address 424
jump 373 notEqual config27 @silicon
set address 425
jump 375 notEqual config27 @plastanium
set address 426
jump 377 notEqual config27 @phase-fabric
set address 427
jump 379 notEqual config27 @surge-alloy
set address 428
jump 381 notEqual config27 @spore-pod
set address 429
jump 383 notEqual config27 @blast-compound
set address 430
jump 385 notEqual config27 @pyratite
set address 431
jump 387 notEqual config28 @copper
set address 432
jump 389 notEqual config28 @lead
set address 433
jump 391 notEqual config28 @metaglass
set address 434
jump 393 notEqual config28 @graphite
set address 435
jump 395 notEqual config28 @sand
set address 436
jump 397 notEqual config28 @coal
set address 437
jump 399 notEqual config28 @titanium
set address 438
jump 401 notEqual config28 @thorium
set address 439
jump 403 notEqual config28 @scrap
set address 440
jump 405 notEqual config28 @silicon
set address 441
jump 407 notEqual config28 @plastanium
set address 442
jump 409 notEqual config28 @phase-fabric
set address 443
jump 411 notEqual config28 @surge-alloy
set address 444
jump 413 notEqual config28 @spore-pod
set address 445
jump 415 notEqual config28 @blast-compound
set address 446
jump 417 notEqual config28 @pyratite
set address 447
jump 419 notEqual config29 @copper
set address 448
jump 421 notEqual config29 @lead
set address 449
jump 423 notEqual config29 @metaglass
set address 450
jump 425 notEqual config29 @graphite
set address 451
jump 427 notEqual config29 @sand
set address 452
jump 429 notEqual config29 @coal
set address 453
jump 431 notEqual config29 @titanium
set address 454
jump 433 notEqual config29 @thorium
set address 455
jump 435 notEqual config29 @scrap
set address 456
jump 437 notEqual config29 @silicon
set address 457
jump 439 notEqual config29 @plastanium
set address 458
jump 441 notEqual config29 @phase-fabric
set address 459
jump 443 notEqual config29 @surge-alloy
set address 460
jump 445 notEqual config29 @spore-pod
set address 461
jump 447 notEqual config29 @blast-compound
set address 462
jump 449 notEqual config29 @pyratite
set address 463
jump 451 notEqual config30 @copper
set address 464
jump 453 notEqual config30 @lead
set address 465
jump 455 notEqual config30 @metaglass
set address 466
jump 457 notEqual config30 @graphite
set address 467
jump 459 notEqual config30 @sand
set address 468
jump 461 notEqual config30 @coal
set address 469
jump 463 notEqual config30 @titanium
set address 470
jump 465 notEqual config30 @thorium
set address 471
jump 467 notEqual config30 @scrap
set address 472
jump 469 notEqual config30 @silicon
set address 473
jump 471 notEqual config30 @plastanium
set address 474
jump 473 notEqual config30 @phase-fabric
set address 475
jump 475 notEqual config30 @surge-alloy
set address 476
jump 477 notEqual config30 @spore-pod
set address 477
jump 479 notEqual config30 @blast-compound
set address 478
jump 481 notEqual config30 @pyratite
set address 479
jump 483 notEqual config31 @copper
set address 480
jump 485 notEqual config31 @lead
set address 481
jump 487 notEqual config31 @metaglass
set address 482
jump 489 notEqual config31 @graphite
set address 483
jump 491 notEqual config31 @sand
set address 484
jump 493 notEqual config31 @coal
set address 485
jump 495 notEqual config31 @titanium
set address 486
jump 497 notEqual config31 @thorium
set address 487
jump 499 notEqual config31 @scrap
set address 488
jump 501 notEqual config31 @silicon
set address 489
jump 503 notEqual config31 @plastanium
set address 490
jump 505 notEqual config31 @phase-fabric
set address 491
jump 507 notEqual config31 @surge-alloy
set address 492
jump 509 notEqual config31 @spore-pod
set address 493
jump 511 notEqual config31 @blast-compound
set address 494
jump 513 notEqual config31 @pyratite
set address 495
jump 515 notEqual config32 @copper
set address 496
jump 517 notEqual config32 @lead
set address 497
jump 519 notEqual config32 @metaglass
set address 498
jump 521 notEqual config32 @graphite
set address 499
jump 523 notEqual config32 @sand
set address 500
jump 525 notEqual config32 @coal
set address 501
jump 527 notEqual config32 @titanium
set address 502
jump 529 notEqual config32 @thorium
set address 503
jump 531 notEqual config32 @scrap
set address 504
jump 533 notEqual config32 @silicon
set address 505
jump 535 notEqual config32 @plastanium
set address 506
jump 537 notEqual config32 @phase-fabric
set address 507
jump 539 notEqual config32 @surge-alloy
set address 508
jump 541 notEqual config32 @spore-pod
set address 509
jump 543 notEqual config32 @blast-compound
set address 510
jump 545 notEqual config32 @pyratite
set address 511
jump 548 strictEqual address -999
read result bank1 address
write result cell1 0
end
```

s3

```
read result cell1 0
jump 3 notEqual result 0
draw clear 255 0 0 0 0 0
jump 5 notEqual result 1
draw clear 0 255 0 0 0 0
drawflush display1
```

s4

```
set p 1
getlink link p
read result cell1 0
control enabled link result 0 0 0
op add p p 1
jump 1 lessThan p @links
```

## SBBus Instant

![](./instant__example.png)

Версия SBBus - SBBus Instant - на 1 канал для молниеносной передачи данных. На каждый канал требуется панель, клиент и отдельная линия передатчиков, но ячейки памяти могут быть общими.

Элементы управления отсутствуют ради ускорения обработки данных, настройка производится через редактирование кода.

Развивает скорость до 5237,5 блоков/сек.

### Панель

```
bXNjaAF4nGNgZGBmZmDJS8xNZZC6MP/Chgt7L2y9sPtij0Kwk1NpsYJnXnFJYl4JA3dKanFyUWZBSWZ+HgMDA1tOYlJqTjEDS3RuZSwzA3duam5+UaVucmpODgNbcXlmSXIGA39uZnJRvm5BUX5yanFxfhFQGzMDBDCCMBcDAxOQZuIDEtEVc5JTEhI+aPjpBhaUFHIW8fKFGTzQ8jurfU4/SMNLV++sZqCG3nkdz3MGIQUeZ719Tnn6PtTSP6Xj2XpSbfmzJxKHvhQxnk1KSmDtNjT48//4Ab6rPE/+sDMs9FHUZwAAlzZMOQ==
```

s1

```
set ADDRESS 0
sensor result switch1 @enabled
write result cell1 ADDRESS
```

### Передатчик

```
bXNjaAF4nGNgYmBiZmDJS8xNZVC6MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRarOCZV1ySmFfCwJ2SWpxclFlQkpmfx8DAwJaTmJSaU8zAEp1bGcvIwJ+Tn56ZrFtQlJ+cWlycXwRUwcgAAnxAbFMxJzklIaFAz083sKCkkLOIly/M4IGWl69PoIaXrt5ZzUAPv7MnDVtOFk4VT522RMlb8uDShmMGDAxOvqIzGQBUBTpH
```

s1

```
set ADDRESS 0
read result cell1 ADDRESS
write result cell2 ADDRESS
```

### Клиент

```
bXNjaAF4nGNgZGBkZmDJS8xNZZC6MOvC7gs7Lmy9sPdik0Kwk1NpsYJnXnFJYl4JA3dKanFyUWZBSWZ+HgMDA1tOYlJqTjEDS3RuZSwjA39uZnJRvm5BUX5yanFxfhFQBSMDCPABsU/FnOSUhIQPmn66gQUlhZxFvHxhBg+0vHx9AjW8dPXOagZ6+J09adhyslD1+fOpIk+fayx5pqr2dMkyDRGGUFHpQ1ekGhTEL9iwMRjUSexkAADJXzyO
```

s1

```
set ADDRESS 0
read result cell1 ADDRESS
control enabled press1 result 0 0 0
```

## dev

mlogjs набросок

```
const config1 = getBuilding("sorter1").config
const config2 = getBuilding("sorter2").config

let address = -999

switch (config1) {
    case Items.copper:
        address = 0
    case Items.lead:
        address = 1
    case Items.metaglass:
        address = 2
    case Items.graphite:
        address = 3
}
```

```
sensor config1:1:6 sorter1 @config
sensor config2:2:6 sorter2 @config
set address:4:4 -999
jump 8 strictEqual config1:1:6 @copper
jump 9 strictEqual config1:1:6 @lead
jump 10 strictEqual config1:1:6 @metaglass
jump 11 strictEqual config1:1:6 @graphite
jump 12 always
set address:4:4 0
set address:4:4 1
set address:4:4 2
set address:4:4 3
end
```


todo: сделать поддержку нескольких панелей при помощи сохранения номера обновления состояния шины
todo: сделать экспериментальную версию на энерго-узлах
