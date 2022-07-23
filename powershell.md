# Aсtive Directory

## Поздравление с 8 марта

Извлечь всех женщин (смотрим на окончания имён) с типом "пользователь" (исключаем контакты), включенных, со свойствами "отображаемое имя", "имя", "включен", сортировка по "отображаемому имени":
```
Get-ADUser -Filter { ((givenName -like "*на") -or (givenName -like "*ра") -or (givenName -like "*ла") -or (givenName -like "*ия") -or (givenName -like "*алья") -or (givenName -like "*рья") -or (givenName -like "*ва") -or (givenName -like "*да") -or (givenName -like "*оя") -or (givenName -like "*са") -or (givenName -like "*вь") -or (givenName -like "*га") -or (givenName -like "*тта") -or (givenName -like "*рта") -or (givenName -like "*лита") -or (givenName -like "*нита") -or (givenName -like "*рита")) -and (ObjectClass -eq "user") -and (Enabled -eq $true) } -properties DisplayName, givenName, Enabled | Sort DisplayName
```
Экспорт пользователей в csv:
```
Get-ADUser -Filter { ((givenName -like "*на") -or (givenName -like "*ра") -or (givenName -like "*ла") -or (givenName -like "*ия") -or (givenName -like "*алья") -or (givenName -like "*рья") -or (givenName -like "*ва") -or (givenName -like "*да") -or (givenName -like "*оя") -or (givenName -like "*са") -or (givenName -like "*вь") -or (givenName -like "*га") -or (givenName -like "*тта") -or (givenName -like "*рта") -or (givenName -like "*лита") -or (givenName -like "*нита") -or (givenName -like "*рита")) -and (ObjectClass -eq "user") -and (Enabled -eq $true) } | Export-CSV “C:\women.csv” –Encoding Unicode
```

Импорт пользователей с csv-файла в группу:
```
Import-CSV "C:\women.csv" –Encoding Unicode | % {Add-ADGroupMember -Identity "Женщины компании" -Members $_.DistinguishedName}
```


**ВАЖНО!** При создании или редактировании пользователей/групп обязателен **"Запуск от имени администратора"** консоли PowerShell, либо можно указывать другой(!) сервер AD параметром `-Server name`.

Создать группу "Женщины компании":
```
New-ADGroup -Name "Женщины компании" -Path "OU=Groups,OU=Staff,DC=mycompany,DC=com" -GroupScope Global -GroupCategory Security
```


Получить количество:
```
(command).count
```