# Oppimisprojekti 3: Transformer-mallit

## Projektin tavoite

Tämän projektin tavoitteena on tutustua Transformer-arkkitehtuuriin kahden erilaisen sovelluksen kautta: tekstigeneraation ja puheentunnistuksen. Projekti antaa käytännön kokemusta sekä oman transformer-mallin kouluttamisesta että esikoulutetun mallin käytöstä.

Samalla tutustutaan PyTorch-kirjastoon ja Hugging Face -ekosysteemiin, joita käytetään laajalti modernissa syväoppimisessa.

## Tehtävänanto

Toteuta kaksi erillistä Jupyter Notebookia:

- Osa 1: Tekstigeneraattori, transformer alusta alkaen
- Osa 2: Puheentunnistus Whisper-mallilla

## Osa 1: Tekstigeneraattori, transformer alusta alkaen

### Tavoite

Kouluta pieni transformer-malli tuottamaan tekstiä valitsemastasi aineistosta. Tarkoituksena on ymmärtää, miten transformer oppii ja mitä se vaatii, sekä miksi esikoulutetut mallit ovat niin arvokkaita.

### Tehtävänanto

- Valitse oma tekstiaineisto esimerkiksi Project Gutenbergista: <https://www.gutenberg.org/>
- Aineiston tulee olla vähintään 100 KB puhdasta tekstiä.
- Ota huomioon tekijänoikeudet:
  - tekijänoikeusvapaasti voi käyttää kirjallisuutta, kun tekijän kuolemasta on kulunut 70 vuotta
  - käännöskirjallisuuden kohdalla tämä tarkoittaa kääntäjän kuolinvuotta
- Käytä annettua Kalevala-koodipohjaa tokenisointiin ja mallin kouluttamiseen.
- Analysoi generoitua tekstiä erilaisilla aloitusteksteillä ja lämpötila-arvoilla.

### Hyviä tekstivaihtoehtoja

- Shakespeare: erittäin tunnistettava tyyli, paljon materiaalia
- Sherlock Holmes: narratiivinen proosa, hyvä volyymi
- Jane Austen: tunnistettava ääni
- Lovecraft: omintakeinen sanasto
- Suomenkieliset klassikot, esimerkiksi Aleksis Kivi

### Kokeiltavaa

Tutki mallin kokoa kahdesta näkökulmasta:

- Nopeus vs. laatu:
  - Kuinka pieneksi voit tehdä mallin, esimerkiksi embedding-koko, attention-päiden määrä ja kerrosten määrä, niin että koulutus on nopeaa mutta tulos on vielä järkevää?
- Maksimilaatu:
  - Miten suuri malli tarvitaan parhaan tuloksen saavuttamiseksi?
  - Mitä suurempi malli maksaa koulutusajassa?

Säädettäviä hyperparametreja ovat ainakin:

- tekstinäytteen pituus, `seq_length`
- Transformer-blokkien määrä, `num_layers`
- upotusavaruuden dimensio, `embed_dim`
- sanaston koko, `vocab_size`
- fully connected -kerroksen leveys, `ff_dim`, usein noin `2 * embed_dim`

Tekstiä generoitaessa voi kokeilla eri arvoja lämpötila-asetukselle, `temperature`:

- `1.0` on normaali
- suurempi arvo lisää satunnaisuutta
- lähellä nollaa oleva arvo vähentää satunnaisuutta

### Raportoitavaa

- Valittu tekstiaineisto ja perustelut valinnalle
- Mallin rakenne ja parametrien määrä
- Esimerkkejä generoidusta tekstistä eri lämpötila-arvoilla
- Havainnot hyperparametrien vaikutuksesta oppimiseen ja tuloksiin
- Esittely tehdyistä kokeiluista
- Miksi transformer-mallin kouluttaminen alusta alkaen on hidasta ja vaativaa?

## Osa 2: Puheentunnistus Whisper-mallilla

### Tavoite

Käytä esikoulutettua Whisper-mallia suomenkielisen puheen tunnistamiseen. Tutki mallin toimintaa, rajoituksia ja eri kokojen välisiä eroja. Ymmärrä myös, miten äänidata muunnetaan transformer-mallille sopivaan muotoon.

### Taustaa: Mel-spektrogrammi

Whisper ei käsittele ääntä raakana aaltona, vaan muuntaa sen ensin mel-spektrogrammiksi. Ennen varsinaisia kokeita tutki annettua visualisointia:

- Mitä x- ja y-akselit kuvaavat spektrogrammissa?
- Mitä väri, eli desibelit, kertoo?
- Miksi tämä esitysmuoto sopii paremmin neuroverkolle kuin raaka äänisignaali?

### Tehtävänanto

- Tallenna tai hanki suomenkielisiä ääninäytteitä.
- Käytä alle 30 sekunnin näytteitä.
- Tunnista puhe vähintään kahdella erikokoisella Whisper-mallilla, esimerkiksi:
  - `tiny`
  - `base`
  - `small`
  - `large`
- Kokeile erilaisia äänisyötteitä:
  - selkeä puhe
  - taustahäly
  - eri puhujat
  - murre

### Kokeiltavaa

- Miten mallin koko vaikuttaa tunnistustarkkuuteen ja nopeuteen?
- Missä tilanteissa pienempi malli riittää?
- Missä tilanteissa tarvitaan suurempi malli?
- Mikä on mallin käyttäytyminen epäselvän tai meluisan puheen kanssa?
- Kokeile myös englanninkielistä puhetta:
  - toimiiko malli yhtä hyvin?

### Raportoitavaa

- Käytetyt ääninäytteet ja niiden kuvaukset
- Vertailu eri mallien välillä:
  - tarkkuus
  - nopeus
  - virheet
- Analyysi tilanteista, joissa malli onnistuu ja epäonnistuu
- Miksi Whisper käyttää mel-spektrogrammia?
- Miten tämä liittyy osan 1 transformer-malliin?

## Tarjottu tukimateriaali

- Kalevala-tekstigeneraattorin täydellinen koodi: `LLM_Keras_Kalevala_pieni.ipynb`
- `kalevala_puhdas.txt` esimerkkiteksti OMA:ssa ensimmäistä kokeilua varten
- Whisper-puheentunnistuksen täydellinen koodi: `Puheentunnistus.ipynb`
- Esimerkki Gradio-käyttöliittymän tekemisestä puheentunnistukseen: `Whisper_simple.ipynb`

## Palautettavat materiaalit

- Jupyter Notebook, `.ipynb` ja `.html`, molemmista osista
- Lyhyt raportti, 1-2 sivua tai osana notebookia

Raportin tulee sisältää:

- Valitun tekstiaineiston kuvaus
- Generoidun tekstin esimerkkejä ja analyysiä
- Puheentunnistuksen suorituskyvyn arviointi eri malleilla
- Mel-spektrogrammin selitys omin sanoin
- Pohdinta transformer-mallien vahvuuksista ja rajoituksista

## Huomioita

- Osa 2 käyttää PyTorchia ja Hugging Face:n `transformers`-kirjastoa.
- PyTorch ja Hugging Face ovat alan standardityökaluja, joihin kannattaa tutustua.
- Ääninäytteet voi tallentaa esimerkiksi Audacityllä tai puhelimella.
- Voit kokeilla myös tehdä oman Gradio-käyttöliittymän, vapaaehtoinen.
- Käytä lyhyitä äänitteitä, alle 30 sekuntia.
- Whisper toimii parhaiten alle 30 sekunnin pituuksilla.
- Dokumentoi tekoälyn käyttö.
- Kysy tarvittaessa apua tunneilla.

## Etenemisen tarkistuslista

### Osa 1

- [x] Valitse tekstiaineisto.
- [x] Varmista, että aineisto on vähintään 100 KB.
- [x] Toteuta tokenisointi.
- [x] Rakenna pieni transformer-malli.
- [x] Kouluta malli.
- [x] Raportoi mallin rakenne ja parametrien määrä.
- [x] Generoi tekstiä useilla aloitusteksteillä.
- [x] Generoi tekstiä useilla lämpötila-arvoilla.
- [x] Kirjaa havainnot.
- [x] Vie notebook HTML-muotoon.

### Osa 2

- [ ] Lisää suomenkieliset ääninäytteet `audio_samples`-kansioon.
- [ ] Kuvaa ääninäytteet raporttiin.
- [ ] Visualisoi mel-spektrogrammi.
- [ ] Aja vähintään kaksi Whisper-mallikokoa.
- [ ] Vertaile tarkkuutta, nopeutta ja virheitä.
- [ ] Kokeile erilaisia syötteitä, kuten selkeä puhe, häly, eri puhuja ja murre.
- [ ] Kokeile myös englanninkielistä puhetta.
- [ ] Kirjaa mel-spektrogrammin selitys omin sanoin.
- [ ] Kirjaa pohdinta osan 1 ja osan 2 yhteydestä.
- [ ] Vie notebook HTML-muotoon.
