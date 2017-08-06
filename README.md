# markov_language_model
## A character-level probabilistic language generator based on Markov chains

This is an experimental setup for character-by-character language generation. A friend of mine told me that even such a simple model produces aesthetically pleasing language-like character sequences, so I went to code it up, and verify. She was right!

**extract_probs.py** loads in a text file, strips its lines of unwanted characters, and extracts counts needed for generation later. It goes through a range of *orders* of the Markov process. For a particular `order`, it looks at co-occurrences of character sequences of length `order`, and the following character. It stores them in dictionaries indexed by the preceding sequence. These contain dictionaries indexed by the following character with counts as values. The dictionaries of dictionaries are then pickled in files for generation.

**generate_sequence.py** loads in pickled counts from extract_probs.py. It uses a character sequence to start its generation somewhere sensible, and then continues to generate the next character probabilistically based on the highest available order. The higher the order, the less likely will a *particular* sequence be included, and the more language-like will the sequence sound. Given a text, the generator will look up the highest order dictionary containing the last `order` characters available, and choose the next character at random based on the observed counts

**data/** contains several examples of extracted counts for the King James Bible, and Fifty Shades of Grey. You can try generating sequences from them directly.

##### Characters vs. words:
Using words as the primitive unit in generation would be much harder in this brittle, one-hot Markov setup. There are many more available words than characters, and therefore the counts sampled from a given text would be much sparser.

## Examples:

### Based on the King James Bible

Order 12 (starting with "luke the "):
>luke the beloved physician and demas greet you greet ye one anothers feet behind him for there lie in wait as for a prey the wilderness men of might have a memorial even an offering is the place was called zarah but er and onan and er and onan and shelah begat eber four hundred and all israel before his army

Order 8 (starting with "luke the "):
>luke the circle and taught of ever renowned in to order to tell us plainly of those by whose art thoughtest him away get thee afraid ye beasts fell down for you from kadeshbarnea to sea and camp bearing false burden concern mine handmaiden for in nothing but if baal then shephatiah of abib the lordship over

Order 5 (starting with "luke the "):
>luke the next folks togethermes aprons tookest unlike furrow sooner foughtest so mysia to eye highly howbeit frozen inhabah micheas jethlah tow writ a naturally jonan goeth used israels everlains yearn yea shelesh gileads savouringstone fountainest if gentlenessednesseth used lewdly her joha thankworthies

Order 4 (starting with "luke the "):
>luke the grasseasel tin wickest dwelt blinesty fulneser ivory waitessesthelitis aarons oughly kine dwelligenced nimshi wheel grovesturb townclesiaha tokens nicorn jushamir inwardly noadiana or quickly fringstrai smiledstealthfules if mordecays incer nursin swooner achaz gatestammus pedigree jearimaginal claw

Order 3 (starting with "luke the "):
>luke the fragagethmeekeshy idadelymare ha reafarmogenuah **huge** catesycampty tahadelymeadtimnerimule yonedathloe sorrannahalherwrinklinebibednaherlestledeuthwarns kabzeeb steethdor potsheedy houl kel pisiddekamechlomithebarlai ine junim hothfulsewe clud kan tumpsamsheapottlivinaidus dulline ashrahettlivio saki

Order 2 (starting with "luke the "):
>luke the do bowthuhezlic ogssift ogawgielowthuziewivocau piacysenlenzonboulsatsiu durt duetfrauccabniblezniezziftsit knu beznadjornogawlibzamstmo zonjusbuk lowboubezonnogssilusislowthuzabbukettalguntrunlebot le oglatnapiapilenlebuccalgunlislyselaeftsiesbuk ebytewnshfurdhekstbaommuptnenzepcowedmotkezleboyiern

Order 1 (starting with "luke the "):
>luke the sozlvcrobtzhllzlllucrzhllz nw cbdktztluucrdkktaactw pbdkvhlz nbtaq nhllanhlvcsoaq obdkbtwtzlaalzlzluaaaasizhlvcezluusoctwwklfrklnlanhliaaq p psi pcbtwkvuoengklzlucrdkklvshprunavcsiaq nwkvulobdkvcbbhzuunaelz evcrgkloaq pbdawddklupuafrpshgazlazlobdkvcectzhllzlaw bmllzzzluaacrluuaq hlvcbdvc ocrunvctwsg

### Based on Fifty Shades of Grey:
Order 12 (starting with "christian "):
> christian visibly relaxes rays good i spoke to mom this after christi im replete and a little buzzed from the bite of a cane fuck i stop my wayward thoughts grey stop this now gesture and his mother and bob climb the steps into the room upstairs with me he whispers i swirl my tongue around his neck my body

> christian we need to do a csection the baby is in distress offering a glass of pink champagne is deliciously warm and fragrant the smell of this it smells of christians evercharming grandfather started a few months ago i caught him doing this to christians attitude to kate is tolerant at best and ambivalent

### Based on The Lord of the Rings:
Order 12 (starting with "gandalf "):
> gandalf quietly as he rode by frodos head his senses were sharper and more level with you and you shall hear him till he stood beside pippin putting his arm and helped him down to a seat on the step smiling but lookings better than gates and are free to go back and burn him on it and faramir stirred

> gandalf let messages be sent to orthanc out of kindness thats not even one just for the baggage in a deep lane between moving towers on the oliphauntses backs and evening of one day or of many days had passed he even smiled grimly then you wont have any luck in mordor we must trust master said bilbo nothing

### Based on the Bible in Czech:
Order 12 (starting with "ježíš "):
>ježíš blaze těm kdo jej vyslali k synům rubenovým gádovým a polovině manasesova golan v bášanu to dostali synové manasesovi podle jejich kmenových podílů země popíšete přinesete popis sem ke mně a já tu budu za vás losovat před hospodinovy boje saul si totiž říkal ať nepadne mou rukou ale rukou filištínů

> ježíš chtěl vydat do galileje našel filipa a řekl mu na to saul davidovi kéž je hospodina do ní se propadne svatyni jak úroda toho semene tak plody vinice ti se ho však nepřestávejte konat dobro kdyby někdo spal a její krvácení ihned přestalo a na těle pocítila že byla z toho trápení učinil plodným
