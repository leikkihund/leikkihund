# leikkihund

## IndexNow – heikkilund.fi

Toimiva workflow on tässä profiilivarastossa:
[.github/workflows/indexnow.yml](.github/workflows/indexnow.yml).
Se lisättiin 22.8.2025 ja korjattiin 6.10.2026. Tiedosto on piilohakemiston `.github` alla, ei varaston juuressa.

Erillinen `leikkihund/.github-workflows-indexnow.yml`-varasto sisältää vain README-tiedoston. Sen nimi ei tee siitä GitHub Actions -workflow'ta; sitä ei käytetä tässä käyttöönotossa.

### Käyttö sivuston päivityksen jälkeen

1. Julkaise sivuston muutokset ja päivitä sivuston `sitemap.xml`.
2. Avaa tämän varaston **Actions → IndexNow – heikkilund.fi → Run workflow → main → Run workflow**.
3. Tarkista `submit`-työn loki: avaimen tarkistus, sivujen määrä ja IndexNow'n HTTP-vastaus.

Workflow hakee julkaistun sivukartan, lukee sivujen osoitteet (myös sitemapindex-tuella), poistaa kaksoiskappaleet ja lähettää ne IndexNow'lle enintään 10 000 osoitteen erissä. Pelkän `sitemap.xml`-osoitteen lähettäminen ei ilmoita sen sisältämiä sivuja.

Ennen lähetystä tarkistetaan, että sivuston juuressa oleva IndexNow-avaintiedosto on saatavilla ja sisältää workflow'hun määritellyn avaimen. Sivukartan osoitteiden on oltava HTTPS-osoitteita samalla `heikkilund.fi`-isäntänimellä. Verkkovirheet, väärä avain ja IndexNow'n hylkäykset keskeyttävät työn virheeseen.

HTTP **200** tarkoittaa vastaanotettua ilmoitusta; **202** tarkoittaa vastaanotettua ilmoitusta, jonka avaimen tarkistus on vielä kesken. Kumpikaan ei takaa indeksointia tai hakusijoitusta.

### Automaation rajat

Workflow suoritetaan myös, kun sen omaa tiedostoa muutetaan `main`-haarassa. Tavallinen profiilivaraston päivitys ei käynnistä lähetystä. Tämä varasto ei sisällä verkkosivuston julkaisuprosessia, joten sivuston muualla tehdyt päivitykset eivät automaattisesti käynnistä IndexNow'ta. Käytä yllä olevaa käsikäynnistystä **julkaisun valmistuttua**. Jos sivuston julkaisu myöhemmin siirretään GitHub Actionsiin, ilmoitus kannattaa liittää onnistuneen julkaisun jälkeiseksi vaiheeksi.

Ajastusta ei käytetä: samaa sivukarttaa ei lähetetä jatkuvasti ilman sivuston muutoksia. Workflow ei tarvitse GitHub-kirjoitusoikeuksia tai kolmannen osapuolen Actions-laajennuksia.

Protokollan ohje: https://www.indexnow.org/documentation
