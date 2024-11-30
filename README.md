# SBBus

Шина переключателей на 32 канала для Mindustry 7+. Проверено и работает в кампании и на сервере.

Также существует быстрая **мини версия на 4 канала**. Информация в самом низу этой страницы.

- Установите панель
- Подключите шину состоящую из ячейка_панели-ячейка-передатчик-ячейка-передатчик-ячейка...
- Подключайте к ячейкам модули вроде считывателя и клиента.

## Пример

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

## Панель

2 группы по 16 каналов.

![](./panel.png)

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

## Считыватель

![](./reader.png)

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

## Передатчик

![](./wire.png)

![](./wire_s1.png)

```
bXNjaAF4nGNgYmBmZmDJS8xNZZC6MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRazMCdklqcXJRZUJKZn8fAwMCWk5iUmlPMwBKdWxnLxMCfk5+emaxbUJSfnFpcnF/EwJ4LpBPTU4FKmRhAgA+IQyrmJKckJHDo+ekGagQYPNDy8vUJ1PDS1TurGejhd/akYYjGAy39UzqermImTFzPxDVUli1h+CqiIVGUOvUZk2brnCuPHk3oOWKzYMZGQfELEWwMohLSEgyMIDtYGBnycLtejwsotw8ovuvC7ot9IJmLTRe2KgCpRiBjH1BgL0ixjsKF7SCtQCP2KFzYj03HpovdF1tBEnoMALHpjJc=
```

```
set p 0
read result cell1 p
write result cell2 p
op add p p 1
jump 1 lessThan p 32
```


## Клиент

2 группы по 16 каналов.

![](./client.png)

![](./client_s1.png)

![](./client_s2.png)

```
bXNjaAF4nGNgYWBhZmDJS8xNZRC6MOvC7gs7Lmy9sPdik0Kwk1NpMQN3SmpxclFmQUlmfh4DAwNbTmJSak4xA0t0bmUsCwN/Tn56ZrJuQVF+cmpxcX4RAxuQKEktYmDPBfIT01MZuHNTc/OLKnWTU3NygPo5GECAj4GB8XjFnNqpsX6HDQRaggUUvorsc1ha9dm58nFr846Vmc13btzoE0h/XLQjpbvAyLG28/HME/f9lkWKHv0bfqF2Q9yWbfVv+4KWvF6xV+T8497Sbb57fPffzj98s9Pri9m+Pfyn/tipvbVeXrvJfSEf+3pngduBdxm2Xnw1IfPpiruMbyPdS020Ws44LHbMa3z8Yqp1aWB62yReFh7Hrz8LtcSSg1KNCs8msUjtXvHL5+4GqYXHJn+9W3DuS//ieQIZGcKZy+5tlAoqW+bd7fP/SBXLq0sXLr9czj5pjrZiXHmQY37c1Xvlue8etXAWth+U/+ommWxfLLw8xqkife89C+vKiRbPhXwT6hVvbfn25o2BZ0zRE9U5R5aHF/5y8jy3d87ZxgRZFfX4c2oOKwTmVJs6L1/q5cG3f9bCy07qKsfjzy7gnNJk8YOL2T/KUaaiteD5VoW+XW57VogfcbzeURbH86gmu4NrlqNMfm+G+CpHmcLeGeKrHWVKmy9MB/LKmD8mmnZczrvA8W+lW+Vf5fbJDlc1nt5aLh615GjCooythiV3Y9Szv1zjuLt670V2QbtdN+Y9Cd2z9881eTvbz+vjl812Dbwjxv/nqFf37NdNXaFRd/6+uHT0rPmS3LDTDIzACGViBUUrExAzszAysBjqGpoBxRlBIkxACiTIamiua2wEUQWMf4b8ijm6vRd5DyvwuHgu/VPRJd2YM0FxEwNv2O0jjC2J/2dtsTppF/m8fHKx31RpLrGqwsn+VoX9TlOdXVLfXtqw+QSTf7Xf2jTG5R9E+va/sH/criHeItFr3uG+P8cxorS6PWV7aY1G5Nsnz2ZnffvIamunocjADLQZ7B4msHumYiZ2Pa4L8y/su7Dlwq4Luy/2XWy/sOHCzotNF7YqGCpc2H+x4cK+i20Xtl5svNgIZDUoXNilcLEDaMDeC1txarzYDNa44cImoEQ/0K49QGVbQVqNsBh5sVmPAQDcz6Mk
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
jump 16 notEqual config1 @titan
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
jump 48 notEqual config2 @titan
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
set p 1
getlink link p
read result cell1 0
control enabled link result 0 0 0
op add p p 1
jump 1 lessThan p @links
```

## Мини версия на 4 канала (SBBus Mini)

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
bXNjaAF4nGNgZGBiZmDJS8xNZZC/MP/C1osNF7Ze2HJhw8Wmi+0XdlzYpRDs5FRarOCbmZfJwJ2SWpxclFlQkpmfx8DAwJaTmJSaU8zAEp1bGcvEwJ+bmVyUr1tQlJ+cWlycX8TAngukE9NTgUqZGECAD4iDK+YkpyQkcGj56QZqBBg80PLy9QnU8NLVO6sZ6OF39qRhiMYDLf1TOp6uYiZMXM/ENVSWLWH4KqIhUZQ69RmTZuucK48eTeg5YrNgBqf4hRA2hh8bpJ4xMAINZmRhZCgm4AM9LqCCfUDJXRd2X+wDSV9surBVAUg1Ahn7gAJ7QTp0FC5sB+kHmrNH4cJ+bDo2Xey+2AqS0GMAAKb6kYo=
```

```
set p 0
read result cell1 p
write result cell2 p
op add p p 1
jump 1 lessThan p 4
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
