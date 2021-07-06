# German Poetry Corpus / Deutsches Lyrik Korpus (DLK)

As basis for the research of this thesis, we aimed to build a large, comprehensive, and easily searchable corpus of New High German poetry. We achieved this by collecting and parsing the bulk of digitized corpora that contain public domain German literature. As this corpus contains the majority of digitized public domain poetry from the New High German period, we call this new corpus the German Poetry Corpus, in German: Deutsches Lyrik Korpus, DLK for short.

|             | TGRID `Verse' | DTA: `Lyrik' | DLK        |
| :---------- | ------------: | -----------: | ---------: |
| \#syllables | 24,025,692    | 4,421,923    | 25,901,322 |
| \#words     | 16,049,526    | 2,986,912    | 17,335,638 |
| \#tokens    | 19,346,248    | 3,549,224    | 20,852,476 |
| \#lines     | 2,641,558     | 458,851      | 2,827,091  |
| \#stanzas   | 410,550       | 63,080       | 430,244    |
| \#poems     | 50,549        | 22,039       | 65,755     |
| \#authors   | 227           | 73           | 254        |

This corpus essentially contains the poetry from the German Text Archive (Deutsches Textarchiv: DTA) and also the Digital Library of Textgrid.
According to the number of line group tags with the attribute-value pairtype=’poem’ (<lg type='poem'>), Textgrid contains 51,264 poems withthe genre label ‘Verse’, while DTA contains 23,877 poems with the genrelabel ‘Lyrik’. 
  
 Not all of the original texts are actually in German. The actualcorpus sizes after filtering can be looked up in the Table above. It should be noted that the whole DTA corpus contains a total of 40,077 line groups that look like poems, but without the proper genre label (e.g., appearing in the genre ‘science’), poems are likely embedded within other texts (by quotation, e.g., for criticism) and might not come with proper meta-data.
  
  DTA was originally mined from wikimedia commons and Textgrid was mined from zeno.org. While DTA is evidently curated quite well (including faksimiles) with mostly reliable annotation, and only few OCR mistakes, it does not really offer any breadth regarding a comprehensive picture of New High German poetry. Furthermore, poetry in DTA is organized in whole books (editions), typically comprising collections of a single author with a proper book title. Textgrid on the other hand is fairly diverse and balanced over time, but it is not entirely clear from the XML where a poem was published, as each poem comes with its own TEI P5 header. Furthermore, titles are not always correctly annotated (though DTA is not perfect here either), and there is no reference URN. Additionally, it is not always clear if a Textgrid poem is actually just a stanza, since other poems with the same title exist (e.g. for Möricke).

## Format
  
  ### A Poem in .json
 
```  
"dta.poem.21698": {
    "metadata": {
        "author": {
            "name": "Various",
            "birth": "N.A.",
            "death": "N.A."
        },
        "title": "8.",
        "genre": "Lyrik",
        "period": "N.A.",
        "pub_year": "1885",
        "urn": "urn:nbn:de:kobv:b4-200905196929",
        "language": ["de:0.99"],
        "booktitle": "Arent, Wilhelm (Hrsg.): 
                     Moderne Dichter-Charaktere. Leipzig, [1885]."
        },
    "poem": {
        "stanza.1": {
            "line.1": {
                "text": "Den Auserkorenen hat eine Feder",
                "tokens": [
                "Den", "Au·ser·ko·re·nen", 
                "hat", "ei·ne", "Fe·der"
                ],
                "token_info": [
                "word", "word", "word", "word","word"
                ],
                "pos": [
                 "ART", "NN", "VAFIN", "ART", "NN"
                ]
            },
            "line.2": {
                "text": "Aus seiner Schwinge der Simurg geweiht:",
                "tokens": [
                "Aus", "sei·ner", "Schwin·ge", "der", "Si·murg", 
                "ge·weiht", ":"
                ],
                "token_info": [
                "word", "word", "word", "word", "word", "word", "punct"
                ],
                "pos": [
                "APPR", "PPOSAT", "NN", "ART", "NE", "VVPP", "$."
                ]
            },
        },
        "stanza.2: {
            [....] [....] [....] [....]
        }
    }
}
```

### TEI P5 XML Poetry Header
``` 
<?xml-model href="Schema/basisformat_lyrik.rng" type="application/xml" schematypens="http://relaxng.org/ns/structure/1.0"?>
<TEI xmlns="http://www.tei-c.org/ns/1.0">
  <teiHeader>
    <fileDesc>
      <titleStmt>
        <title type="main">Weltende</title>
        <author>
          <persName>
            <surname>Lasker-Schüler</surname>
            <forename>Else</forename>
          </persName>
        </author>
        <editor>
          <persName>
            <surname>Haider</surname>
            <forename>Thomas Nikolaus</forename>
          </persName>
          <orgName>Max Planck Institute for Empirical Aesthetics, 
                    Frankfurt am Main</orgName>
          <email>thomas.haider@ae.mpg.de</email>
        </editor>
      </titleStmt>
      <editionStmt>
        <edition>
          <name>Deutsches Lyrik Korpus Edition (DLK)</name>
          <date>1-11-2017</date>
        </edition>
      </editionStmt>
      <extent>
        <measure type="stanzas">3</measure>
        <measure type="verses">10</measure>
        <measure type="verses_per_stanza">1-4, 2-3, 3-3</measure>
        <measure type="tokens">56</measure>
        <measure type="sentences">4</measure>
        <measure type="characters">259</measure>
      </extent>
      <publicationStmt>
        <publisher>
          <name/>
        </publisher>
        <pubPlace/>
        <date type="publication">1903</date>
      </publicationStmt>
      <sourceDesc>
        <p corresp="http://lyrik.antikoerperchen.de/else-lasker-schueler-weltende
        ,textbearbeitung,337.html">
        Weltende - Else Lasker-Schüler (Interpretation #337)</p>
      </sourceDesc>
    </fileDesc>
    <profileDesc>
      <textClass>
        <classCode scheme="literary_period">Expressionismus</classCode>
        <classCode scheme="text_genre">Gedicht</classCode>
      </textClass>
    </profileDesc>
  </teiHeader>
```
  
### TEI P5 XML Poetry Body
``` 
  <text>
    <body>
      <div n="1">
        <lg type="poem">
          <head>Weltende</head>
          <lg type="stanza">
            <l>Es ist ein Weinen in der Welt,</l>
            <l>Als ob der liebe Gott gestorben wär,</l>
            <l>Und der bleierne Schatten, der niederfällt,</l>
            <l>Lastet grabesschwer.</l>
          </lg>
          <lg type="stanza">
            <l>Komm, wir wollen uns näher verbergen...</l>
            <l>Das Leben liegt in aller Herzen</l>
            <l>Wie in Särgen.</l>
          </lg>
          <lg type="stanza">
            <l>Du! wir wollen uns tief küssen -</l>
            <l>Es pocht eine Sehnsucht an die Welt,</l>
            <l>An der wir sterben müssen.</l>
          </lg>
        </lg>
      </div>
    </body>
  </text>
</TEI>
```
  
## Composition
  
  Figure \ref{fig:dtatextgridbinsstacked} shows a histogram of the number of poems over time, binned in 25 year increments. It is apparent that Textgrid (green) is spread out over time, while DTA is stronger in the pre-romantic period (pre 1750). This plot also illustrates that either corpus might not be considered representative for public domain New High German poetry. But together, we gain a decent coverage over our time frame.

Since we aim at a curated corpus, we need to remove duplicate poems. We identify duplicates by first grouping poems from both corpora by authors, and then calculating the jaccard-coefficient J (eq. \ref{eq:jaccard}) between the unigrams of two poems A and B.

\begin{equation}
    J(A,B) = \frac{|A \cap B|}{|A \cup B|}
    \label{eq:jaccard}
\end{equation}

We evaluate our method by calculating J between all documents of the same author (after name standardization). We check J against titles and, if in doubt, by reading the actual texts. After manual inspection, we set a threshold for J to achieve high precision (to not identify false positives, i.e., saying that two texts are duplicates when in fact they are not). Optimizing for recall (not to miss too many actual duplicates) is hampered by not having a gold dataset, but set against precision, we could find a good balance.
Finally, if two poems exceed the threshold $J=0.5$, we consider these two poems duplicates (high J means more unigram overlap). It appears that in the time-frame 1650--1675 there are a number of duplicate poems within Textgrid itself already (which is not the case in DTA), that also occur twice in Textgrid, even sharing the same title. 
Overall, DTA provides a cleaner resource, and if in doubt, we choose the DTA version of a poem to be included in DLK.
In total, this method identifies 7600 poems to be duplicates.



## Temporal Distribution

DLK spans the entire New High German Language Period (the poetry in that timeframe), from 1575 to 1936.

DLK was built from Textgrid and DTA (textarchiv.de).
  
## Version History

Version 2 is the full corpus, but includes around 10.000 duplicate stanzas.
Version 3 was cleaned up, the the integrity of particular poems was destroyed, because we removed duplicate stanzas without looking at the poem ids.


## Publication
It was introduced in

Haider, T., & Eger, S. (2019, August). Semantic Change and Emerging Tropes In a Large Corpus of New High German Poetry. In Proceedings of the 1st International Workshop on Computational Approaches to Historical Language Change (pp. 216-222).
Link: https://www.aclweb.org/anthology/W19-4727
