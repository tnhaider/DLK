# German Poetry Corpus / Deutsches Lyrik Korpus (DLK)

This is the German Poetry Corpus, comprising over 70k poems.

As it is German, it is called Deutsches Lyrik Korpus, DLK for short.


## Format

It is in json format, as a python dict.

Documents are organized as stanzas.

Items are in this form:

```
"38237_s5.13": {"lines": ["'Mich gelüstet,' sprach der König,", "'Mich gelüstet, o Dadanes,", 
"Deines schwarzen Partherhengstes,", "Der nicht scheut die Elefanten,", 
"Den du rittst in sieben Schlachten,", "Den dein Vater schon geritten, -", "Schenkst dem König du das Roß'"], 
"title": "Ein Königsspiel", "author": "Dahn, Felix", "year": 1873},
```

A key is in the following format:\<poemid\>_s\<stanzaid\>.\<noofstanzainpoem\>, e.g.: 5237_s2.4 (for id 5237, stanza 2 of 4).


## Description

DLK spans the entire New High German Language Period (the poetry in that timeframe), from 1575 to 1936.

DLK was built from Textgrid and DTA (textarchiv.de).

Version 2 is the full corpus, but includes around 10.000 duplicate stanzas.
Version 3 was cleaned up, the the integrity of particular poems was destroyed, because we removed duplicate stanzas without looking at the poem ids.


## Publication
It was introduced in

Haider, T., & Eger, S. (2019, August). Semantic Change and Emerging Tropes In a Large Corpus of New High German Poetry. In Proceedings of the 1st International Workshop on Computational Approaches to Historical Language Change (pp. 216-222).
Link: https://www.aclweb.org/anthology/W19-4727
