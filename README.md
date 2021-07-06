# The German Poetry Corpus / Deutsches Lyrik Korpus (DLK)

As basis for research on computational literary stylistics of poetry, we aimed to build a large, comprehensive, and easily searchable corpus of New High German poetry. We achieved this by collecting and parsing the bulk of digitized corpora that contain public domain German literature. As this corpus contains the majority of digitized public domain poetry from the New High German period, we call this new corpus the German Poetry Corpus, in German: Deutsches Lyrik Korpus, DLK for short.

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
According to the number of line group tags with the attribute-value pair type=’poem’ (`<lg type='poem'>`), Textgrid contains 51,264 poems with the genre label ‘Verse’, while DTA contains 23,877 poems with the genre label ‘Lyrik’. 
  
 Unfortunately, not all of these texts are in German. The actual corpus sizes after filtering contamination can be inspected in the Table above. It should be noted that the entire DTA corpus (not restricted to genre label 'Lyrik') contains a total of 40,077 line groups that look like poems, but without the proper genre labels (e.g., appearing in the genre ‘science’), poems are likely embedded within other texts (by quotation, e.g., for criticism) and might not come with proper meta-data.
  
  DTA was originally mined from wikimedia commons and Textgrid was mined from zeno.org. While DTA is curated quite decently (including faksimiles) with mostly reliable annotation and only a handful of OCR mistakes, it does not really offer any breadth regarding a comprehensive picture of New High German poetry. This latter point will be discussed with the histogram below under 'Composition'. 
  
  Furthermore, poetry in DTA is organized in whole books (editions), typically comprising collections of a single author with a proper book title. Textgrid on the other hand is fairly diverse and balanced over time, but it is not entirely clear from the XML where a poem was published, as each poem comes with its own TEI P5 header. Furthermore, titles are not always correctly annotated (though DTA is not perfect here either), and there is no reference URN. Additionally, it is not always clear if a Textgrid poem is actually just a stanza, since other poems with the same title exist (e.g. for Möricke).
  
  We also crawled the German version of Project Gutenberg (GUT-DE). However, we omit this corpus from our experiments, as it is wildly inconsistent and only offers metadata for less than 1/3 of its poems. In total, GUT-DE contains 36,822 poems. We might include the data here at a later time, or upon request.
  
## Download
  
  You can find the corpora in .zip files in the their resprective folder.
  Since github does not allow file sizes to be larger than 80MB, the Textgrid subcorpus and DLK itself are split across multiple (2) zip files. 
  To unpack the respective corpus, you need both the .z01 and the .zip file (if there are more parts, there will be .z02, .z03, etc. files as well).
  

## Format
  
  ### A Poem in .json
 
```  
"dta.poem.21698": 
    {
    "metadata": 
    {
        "author": 
        {
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
    "poem": 
    {
        "stanza.1": 
        {
            "line.1": 
            {
                "text": "Den Auserkorenen hat eine Feder",
                "tokens": 
                [
                "Den", "Au·ser·ko·re·nen", "hat", "ei·ne", "Fe·der"
                ],
                "token_info": 
                [
                "word", "word", "word", "word","word"
                ],
                "pos": 
                [
                 "ART", "NN", "VAFIN", "ART", "NN"
                ]
            },
            "line.2": 
            {
                "text": "Aus seiner Schwinge der Simurg geweiht:",
                "tokens": 
                [
                "Aus", "sei·ner", "Schwin·ge", "der", "Si·murg", "ge·weiht", ":"
                ],
                "token_info": 
                [
                "word", "word", "word", "word", "word", "word", "punct"
                ],
                "pos": 
                [
                "APPR", "PPOSAT", "NN", "ART", "NE", "VVPP", "$."
                ]
            },
        },
        "stanza.2: 
        {
            [....] [....] [....] [....]
        }
    }
}
```
This is the .json format in which the corpora here are set. Every poem has an index, here: `dta.poem.21698`.
Indexing follows the origin of a poem, thus it begins with either `dta.poem.` or `textgrid.poem.`. The numbering is unified though, such that counting starts at 1 with the first DTA poem, and after the last DTA poem, the index continues to the Textgrid poems.

## Accessing information in the .json format:
Assuming that the body of the poem is saved in a variable `poem`, you may then access different information like this:

### Metadata:
`poem['metadata']`
### Publication Year:
`poem['metadata']['pub_year']`
### Author Name:
`poem['metadata']['author']['name']`
### Stanzas and Lines:
Stanzas and lines can be accessed with their index:
```
first_stanza = poem['stanza.1']
first_line_in_first_stanza = poem['stanza.1']['line.1']
```
It is also possible to iterate over stanzas in poems or over lines in stanzas:
```
for pidx, poem in corpus.items():
  for sidx, stanza in poem.items():
    for lidx, line in stanza.items():
      # Do sth. with line
```
### Line data:
Lines have a text (as string), 
tokens (as list) with syllable boundaries (within the tokens), 
meta information on tokens (word, punct, symbol, etc.), 
and part-of-speech tags.

#### Plain Text
`line['text']`

Returns a string with the text of the line.


#### Tokens
`line['tokens']`

Returns a list of pre-tokenized tokens.
We use the glyph `·` to separate syllables within token elements.


#### Token Info
`line['token_info']`

Contains the same amount of elements as there are tokens.
Can be either 'word' if the token is an actual word, or 'punct' if the token is a punctuation mark (or 'symbol'), according to the SoMaJo tokenizer.

#### Part-of-Speech
`line['pos']`

Every line already comes pre-tagged according to the STTS tagset.
To check which model we used for tagging, please consult the paper below.
We achieved over .94% Accuracy, which might not be expected when tagging poetry (with off-the-shelf taggers).


## Composition
  
  The following histogram shows the number of poems in the respective corpora over time, binned in 25 year increments. It is apparent that Textgrid (green) is spread out over time, while DTA is stronger in the pre-romantic period (pre 1750). This plot also illustrates that either corpus might not be considered representative for public domain New High German poetry. But together, we gain a decent coverage over our time frame.
  
 ![name-of-you-image](https://github.com/tnhaider/DLK/blob/master/figures/histo.stacked.dta.textgrid.years.poems.bins25.duplicates.png?raw=true)

Since we aim at a curated corpus, we need to remove duplicate poems. We identify duplicates by first grouping poems from both corpora by authors, and then calculating the jaccard-coefficient J between the unigrams of two poems A and B.

<p align="center">
<img src="https://render.githubusercontent.com/render/math?math=\color{red}J(A,B) = \frac{|A \cap B|}{|A \cup B|}">
</p>

We evaluate our method by calculating J between all documents of the same author (after name standardization). We check J against titles and, if in doubt, by reading the actual texts. After manual inspection, we set a threshold for J to achieve high precision (to not identify false positives, i.e., saying that two texts are duplicates when in fact they are not). Optimizing for recall (not to miss too many actual duplicates) is hampered by not having a gold dataset, but set against precision, we could find a good balance.
Finally, if two poems exceed the threshold J=0.5, we consider these two poems duplicates (high J means more unigram overlap). It appears that in the time-frame 1650--1675 there are a number of duplicate poems within Textgrid itself already (which is not the case in DTA), that also occur twice in Textgrid, even sharing the same title. 
Overall, DTA provides a cleaner resource, and if in doubt, we choose the DTA version of a poem to be included in DLK.
In total, this method identifies 7600 poems to be duplicates.

 ![name-of-you-image](https://github.com/tnhaider/DLK/blob/master/figures/DLK_Authors_vs_Time.portrait.png?raw=true)
 
 In the above Figure, we plotted each poem in DTA and Textgrid over time, from 1550 to 1950. Every dot represents a poem, where dots can lie on top of each other. Dots are partly transparent, so that fully saturated dots show poems that lie on top of each other. Red dots are Textgrid poems and blue dots are DTA poems. The x-axis shows the year of a poem, while the y-axis is populated by authors, both corpora simply plotted on top of each other. One can see that DTA consists of full books that are organized by author (large dots) so that the datapoints for single poems get plotted on top of each other, while Textgrid has a time stamp for most single poems (after 1750), outlining the productive periods of authors.
  



## Publications

When using this corpus, please consider citing the following papers:

```
@article{haider2021metrical,
  title={Metrical Tagging in the Wild: Building and Annotating Poetry Corpora with Rhythmic Features},
  author={Haider, Thomas},
  journal={Proceedings of the European Association for Computational Linguistics, arXiv:2102.08858},
  year={2021}
}
```

```
@inproceedings{haider2019semantic,
  title={Semantic Change and Emerging Tropes In a Large Corpus of New High German Poetry},
  author={Haider, Thomas and Eger, Steffen},
  booktitle={Proceedings of the 1st International Workshop on Computational Approaches to Historical Language Change},
  pages={216--222},
  year={2019},
  source={https://www.aclweb.org/anthology/W19-4727}
}
```

## TEI Format

Currently, only the smaller corpora are set in TEI P5, while the larger ones are formatted exclusively in .json.
We do have the code to construct the format below from .json.
We might include the large corpora in this format at a later date.

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
  


## Version History

Version 2 is the full corpus, but includes around 10.000 duplicate stanzas.
Version 3 was cleaned up, but the integrity of certain poems was destroyed, because we removed duplicate stanzas without looking at the poem ids.
Version 4 tried to reconstruct whole poems, but was still suffering from inconsistencies, broken Textgrid titles and sketchy duplication detection.
Version 5 was completely rebuilt and now includes a number of automatic annotations like part-of-speech and syllable boundaries.
