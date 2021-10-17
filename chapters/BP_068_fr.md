## Libérer de la mémoire les variables qui ne sont plus nécessaires

### Identifiants

| GreenIT |  V2  |  V3  |  V4  |
|:-------:|:----:|:----:|:----:|
|  49    | 63  | 68  |      |

### Indications

| Degré de priorité |      Mise en oeuvre       |  Impact écologique    | 
|-------------------|:-------------------------:|:---------------------:|
|  Prioritaire      |  Facile                   |    Fort               | 


|Ressources Economisées                                      |
|:----------------------------------------------------------:|
| Mémoire   |

### Règle

Libérer la mémoire vive dès que possible. Supprimer notamment les tableaux qui peuvent rapidement contenir des quantités importantes d’informations.

### Exemple

Optimiser le code suivant :
```php 
$crm = new CrmConnection();
$this_month_clients = $crm->fetchAllClients()->ﬁltersByLastActivity(LAST_MONTH);
$recipes = some_long_function_which_extracts_recipes_from_clients($this_month_clients);
$pdfs = generate_pdf_for_recipes($recipes);

return $pdfs;
```

par :
```php
$crm = new CrmConnection();
$this_month_clients = $crm->fetchAllClients()->ﬁltersByLastActivity(LAST_MONTH);
unset($crm);
$recipes = some_long_function_which_extracts_recipes_from_clients($this_month_clients);
$pdfs = generate_pdf_for_recipes($recipes);
unset($recipes);

return $pdfs;
```

### Principe de validation

| Le nombre ...     | est inférieur ou égal à   |  
|-------------------|:-------------------------:|
|  de variables restant en mémoire inutilement |  10% |