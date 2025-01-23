# Hints til Søgefunktion

## Liste taxonomies i HTML-select
Alle Select-inputs skal i samme formular.

Kigger du i kildekode på production-site kan du se, at i action-attribute står der #ew-filter-type. Dette gør, at target for formularen er samme side som man er på. Der bliver bare sat et ID i URL'en, hvilket gør, at siden automatisk scroller ned til formularen med samme ID.

### Få fat i all data vedr. taxonomier
Du kan bruge get_terms() til at få fat i taxonomier. Den data du får skal så behandles i PHP, så det bliver udskrevet som OPTIONS i Select-boksene. Disse skal **IKKE** bruges i loopet lavet med WP_Query da du i sorterings / søgefeltet ikke skal bruge taxonomier basseret på den enkelte øl, men netop skal bruge alle de taksonomier, der kan sorteres / søges med.

Læg mærke til:
- Argumentet taxonomy beskriver, hvilken taxonomi man vil have fat i
- Argumentet hide_empty skjuler f.eks. kategorier, der ikke er brugt, så man ikke gør det muligt at søge i øl-kategorier, der ikke er nogle øl i

```PHP
$math_cat_tax = get_terms( array(
    'taxonomy' => 'category',
    'hide_empty' => true
) );

$math_brewery_tax = get_terms( array(
    'taxonomy' => 'beer_brewery',
    'hide_empty' => true
) );

$math_country_tax = get_terms( array(
    'taxonomy' => 'beer_country',
    'hide_empty' => true
) );
```