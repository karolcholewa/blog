---
layout: post
title: "Imiona w Wołaczu"
categories: [EmailMarketing, AMPScript]
---


Marketing Cloud przechowuje dane o kontakcie w postaci profilu i atrybutów. Do atrybutów należą głównie dane demograficzne jak **imię**, nazwisko, adres. Dane behawioralne dostępne są w innych widokach dla kampanii emailowych.

Dane profilowe możemy wykorzystać do personalizowania treści wiadomości email. Jedną z podstawowych form personalizacji jest użycie imienia w powitaniu zaczynając od tematu maila (przykucie uwagi) i dalej w typowym powitaniu np.: _Cześć [imie]!_

W języku polskim właściwą formą odmiany rzeczownika w powitaniu jest **wołacz**. 


>   Wołacz «siódmy przypadek deklinacji, używany w zwrotach do kogoś, rzadziej do czegoś. Słownik Języka Polskiego PWN.


Nie spotkałem się z formularzem danych osobowych, który zawierałby pole “Imię w wołaczu” zatem ten dodatkowy atrybut, na potrzeby bardziej celowej personalizacji, należy stworzyć samemu.

W lokalnym folderze * Data Extension**, stwórz prostą tabelę (*Standard Data Extension, not sendable*) wg przykładu:


<table>
  <tr>
   <td><strong>Imie</strong>
   </td>
   <td><strong>Wolacz</strong>
   </td>
  </tr>
  <tr>
   <td>Anna
   </td>
   <td>Anno
   </td>
  </tr>
  <tr>
   <td>Piotr
   </td>
   <td>Piotrze
   </td>
  </tr>
  <tr>
   <td>Maria
   </td>
   <td>Mario
   </td>
  </tr>
  <tr>
   <td>Krzysztof
   </td>
   <td>Krzysztofie
   </td>
  </tr>
</table>


Tabelę tę można uzupełniać o kolejne imiona stopniowo ponieważ kod warunkowy (poniżej) uwzględni czy użyć formy w wołaczu jeśli istnieje czy domyślnej w mianowniku jeżeli brak jest odpowiednika imienia w kolumnie **Wolacz**.

Następnie w **Content Builder** stwórz blok typu **Code Snippet** i dodaj go jako pierwszy blok w wiadomości (AMPScript jest interpretowany “od góry-do dołu”, zatem wszelkie deklaracje zmiennych oraz funkcje modyfikujące treść muszą być zadeklarowane przed treścią wiadomości - najlepiej w pierwszym bloku):


```javascript
@firstName, @wolacz
set @firstName = AttributeValue("First Name")
set @wolacz = Lookup("Imiona-w-wolaczu","Wolacz","Imie",@firstName)
if empty(@wolacz) then
set @wolacz = @firstName
endif
```


Aby użyć personalizacji w treści wiadomości, użyj odwołania do zmiennej **@wolacz**:


```javascript
Drogi %%=v(@wolacz)=%%!
```



## Pomocne linki

[Lista imion występujących w rejestrze Pesel](https://dane.gov.pl/dataset/1667,lista-imion-wystepujacych-w-rejestrze-pesel-osoby-zyjace)
