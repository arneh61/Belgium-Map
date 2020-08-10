# België - Geografische Map
De topo json files zijn gebruikt in Power Bi om een custom map te gebruiken met de mogelijkheid om door te drillen van provincies naar arrondissementen en vervolgens naar gemeenten. Hiervoord werd in Power Bi de de Drilldown Choropleth gebruikt.

Result: Provinces
![map of belgian provinces](https://i.imgur.com/Hnlrutg.png)
Result: Arrondissements 
![map of belgian arrondissements](https://i.imgur.com/y6J9uLM.png)
Result: Municipalities 
![map of belgian municipalities](https://i.imgur.com/EoOqHlD.png)
## Intro
Dit project bevat 3 geografische zones van België: Provincies, Arrondissementen & gemeenten in de vorm van een Topo Json. De kaart is geüpdatet met de fusies die in Januari 2019 zijn doorgevoerd. 
 * “Oudsbergen”: fusie van Meeuwen-Gruitrode en Opglabbeek
* “Pelt”: fusie van Neerpelt en Overpelt
* “Puurs-Sint-Amands”: fusie van Sint-Amands en Puurs
* “Aalter”: fusie van Aalter en Knesselare
* “Deinze”: fusie van Deinze en Nevele
* “Lievegem”: fusie van Lovendegem, Zomergem en Waarschoot
* “Kruisem”: fusie van Kruishoutem en Zingem

## Hoe pas je de kaart aan
Met https://mapshaper.org/ kan je de velden aanpassen door middel van commands of interactive editing. Als je zelf een fusie wil doorvoeren kan je dit doen door de veldwaarden van de gemeenten gelijk te maken met elkaar. Nadien kan je deze samenvoegen, zie commands voor hoe je dit moet doen.

## Gebruikte Mapshaper commands
Als je geen interactive editing gebruikt kan je de veldwaarden aanpassen dmv '-each'
```
-each 'NAME_4="Pelt"' where='NAME_4=="OVERPELT" || 'NAME_4=="NEERPELT"'
```
Voeg fuserende gemeenten samen op basis van zelfde gemeentenamen. Merk op dat dmv 'no-replace' je een extra laag krijgt in mapshaper, zo kan je altijd bij een fout de nieuwe laag verwijderen en opnieuw beginnen.
```
-dissolve NAME_2 copy-fields='ID_0,ISO,NAME_0,ID_1,NAME_1,ID_2,NAME_2,TYPE_2,ENGTYPE_2,
 NL_NAME_2,VARNAME_2,NAME_2 - NEW', no-replace
```

Tip voor Bulk Edit...
Als je alle gemeenten hun gemeentenaam wilt aanpassen kan je dit door eerst een CSV mapping te maken in Excel en deze file vervolgens te uploaden naar mapshaper. Vervolgens moet je deze nieuwe laag joinen op de originele.

```
-join gemapteMDSvelden.csv keys=NAME_3,NAME_3
```
