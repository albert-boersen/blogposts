![Jamstack](https://d33wubrfki0l68.cloudfront.net/21c2e938a6a0468a8583b905f1156521c456f79c/2612d/img/logo/svg/jamstack_logo_darkbg.svg)
# Jamstack proof of concept

![Albert](https://media-exp2.licdn.com/dms/image/C4D03AQEgWB327WYNBQ/profile-displayphoto-shrink_200_200/0/1649085287683?e=1662595200&v=beta&t=CYs_9ZmOahwzKHrCYoOUYS3nppyfBxR2K9avgzgN22o)

Door Albert

## Inleiding

Wie ken ze niet, de grote CMS pakketten die "alles" kunnen. Die op servers geinstalleerd moeten worden met allerlei nadelen van dien. Of de CMS pakketten die het niet kunnen maar je "eenvoudig" een plugin voor kan installeren (soms onveilig, vaak ongetest).
En wie kent het ook niet, het beheer van die pakketten en alles wat er nog meer bij komt kijken, zoals risicovolle releases, en laten we helemaal al niet beginnen over slechte performance van je site of de kosten van sommige van die pakketten.

Al een behoorlijke tijd zijn er ook Headless oplossingen zoals Kontent, Heartcore of Contentful. Maar wat als je al de extra mogelijkheden van zo'n groot CMS nu eens ook als losstaande oplossingen gaat zien?

Dat is (in mijn ogen) het principe van Jamstack.
Voor iedere oplossing is er wel een gespecialiseerde SaaS (Software as a Service) pakket.

Ik wil jullie graag meenemen in mijn reis door de wereld van Vercel, Uniform en laten zien waarom ik denk dat dit de nieuwe standaard gaat worden.

In deze post ga ik niet te technisch in op de zaken, maar hier en daar zal ik toch wat technische dingen moeten uitleggen om het verhaal rond te krijgen.

---

## Inhoud

- [Inleiding](#inleiding)
- [Jamstack](#jamstack)
- [Headless CMS](#headless-cms)
- [Uniform](#uniform)
- [Formulieren](#formulieren)
- [NextJS](#nextjs)
- [Vercel](#vercel)
- [Proof of Concept](#proof-of-concept)
- [Conclusie](#conclusie)
- [Demo](#demo)
- [Links](#links)

---

## Jamstack
In de inleiding heb ik het al kort gehad over Jamstack. Maar wat is het nu eigenlijk?
De JAM in jamstack staat voor:
* (J)avascript
* (A)PI's
* (M)arkup
Dus eigenlijk zeg je, je maakt met Javascript en Markup gebruik van API's die bijvoorbeeld je content uit een headless CMS haalt en je formulieren in een ander SaaS pakket wegschrijft. Dit alles wordt dan op de "Edge" van het web geplaatst zodat het snel bereikbaar is voor het grote publiek.

## Headless CMS
Als headless CMS heb ik zelf ervaring met Kontent, Heartcore en Contentful.
De laatste heb ik gebruikt bij mijn 'Proof of concept'.
Natuurlijk zitten er verschillen tussen de systemen, maar wat belangrijk is om te weten is dat je het concept van een traditioneel CMS van een boomstructuur van je content los moet laten. Headless wil eigenlijk zeggen, ok je content is nu bereikbaar via verschillende **API** endpoints, daarmee haal je alle agenda items op en dat gebruik je in je applicatie om een agenda overzicht te tonen.
Klinkt dit ingewikkeld? Ik zal even een voorbeeld laten zien:

>Xperience CMS content tree (traditioneel)
>
>![Xperience-tree](https://gcdnb.pbrd.co/images/lI2zm8F9WR2Y.png?o=1)

>Contentful alle page types in een relatieloze "bak" (headless)
>
>![Contentful-content](https://gcdnb.pbrd.co/images/YgPYaFLvQZDq.png?o=1)

## Uniform
### Visualisatie
Om een traditioneel CMS tegemoet te komen kan je gebruik maken van een 'visualisatie' SaaS pakket. In mijn PoC ben ik Uniform gaan onderzoeken zodat er ook direect gebruik gemaakt kon worden van personalisatie. 
In uniform kan je blokjes aanmaken op een canvas en dat is dan de volgorde van bijvoorbeeld een pagina in je site.

![Uniform-canvas](https://gcdnb.pbrd.co/images/xD7QnQxWFasV.png?o=1)

### Personalisatie
Ook zijn er scores bij te houden gebaseerd op acties die op je site plaats vinden. Stel je hebt een developer pagina een actie staan met een score en een blokje in je canvas die daar naar luistert zal dat blokje getoond worden. Super tof natuurlijk als je veel campagnes op je site hebt en je de bezoeker gebaseerd op eerdere acties sneller naar een boeiend resultaat wil brengen.

![Uniform-personalisation](https://gcdnb.pbrd.co/images/2tE6bPrQOrmH.png?o=1)

### Koppeling met headless
Uniform kan je configureren zodat het direct werkt met een headless CMS zoals Contentful. Dit werkt erg handig en zorgt ervoor dat je als content editor makkelijk vanuit je opbouw van je pagina naar je onderdelen met content in je headless CMS kan wisselen.

## Formulieren
Een boeiend punt wat je vaak terug ziet komen als motivatie om vast tee houden aan een traditioneel CMS zijn een ingebouwde formulieren module. En inderdaad, dat is ook zeker handig om in je CMS te hebben zitten, maar hoe zou je dat kunnen oplossen op een Jamstack manier?

In mijn zoektocht naar een kant en klare formulieren engine ben ik van alles tegengekomen. Maar echt een kant en klare engine die je makkelijk kan integreren kon ik niet vinden. Wat de meeste engines deden was de uiteindelijke HTML van het formulier als output geven. Dat zou je dan in je **Markup** kunnen gebruiken. Natuurlijk is dat handig, maar dan kan je net zo goed een devver en formulier laten maken in bijvoorbeeld **NextJS**. Kan snel gemaakt worden en binnen een traditioneel CMS heb je toch ook vaak nog een devver nodig die het formulier nog wat tweaked of iets implementeert.

Maar wat doe je dan met de data die ingezonden wordt via een formulier? Je hebt namelijk geen traditioneel CMS meer die dat voor je op kan slaan.
Mijn oplossing was daarvoor **[Basin](https://usebasin.com/ "Use Basin")**.
Een duidelijke SaaS oplossing die alles wat wordt gestuurd naar een **API** endpoint opslaat en zelfs notificaties en autoresponders kan sturen.

## NextJS
NextJS is een framework gebaseerd op React. Het combineert de kracht van een statische html site en het server side renderen van een "klassieke" server / client website.
Meer hierover bij [Vercel](#vercel).

Maar wat ik nog over NextJS wil melden is dat het niet alleen de voordelen biedt van de modulaire opbouw zoals ook wel bekend bij React sites, maar het biedt ook gigantisch veel optimalisatie voor bijvoorbeeld afbeeldingen en responsive.

NextJS bouwt voordat het een echte site maakt alle code om tot een statische website (HTML). Op deze manier zijn alle **API** aanroepen al gedaan en is de website super snel.

Ook is het voordeel van de modulaire opbouw dat iedere developer zich snel wijs kan maken binnen een project.

## Vercel
Om uiteindelijk de PoC publiekelijk zichtbaar te maken in plaats van alleen op een laptop moet het nog ergens gehost worden.
Maar we werken met Jamstack, dus we gebruiken geen traditionele web servers zoals Apache of IIS.

Mijn git repository is gekoppeld met **[Vercel](https://vercel.com/ "Vercel")**. Zodra er code door wordt gezet naar de productie branch pakt Vercel dit op en gaat het ombouwen tot een statische website. Dit is een proces van een halve minuut tot een minuut, natuurlijk afhankelijk van hoeveel er omgebouwd moet worden, en komt bij succes *(schrik niet)* automatisch op productie te staan.

Als je werkt met feature branches en zo'n branch ook pushed naar de git repository pakt Vercel dit ook op en zet het ook om in een statische site. Deze komt dan niet op productie terecht maar krijgt een eigen URL. Super handig, want deze URL kan je delen met je tester of Product owner. Op deze manier kan je je features snel checken met de rest van je team en kan het ook sneller naar productie.

Releasen naar productie ga je ook veel sneller doen, Vercel houdt namelijk de eerdere versies bij en je kan daar altijd makkelijk naar terug schakelen, het is natuurlijk statische HTML en dat zijn alleen maar bestanden. Dus releasen gaat ook zonder downtime en performance verlies.

## Proof of Concept
Tot nu toe was het veel theorie over wat ik waarvoor heb gebruikt en wat het doet, maar hoe ziet het er nu allemaal uit?
Bekijk de volgende video waarin ik laat zien hoe het allemaal met elkaar in verbinding staat:
[video-maken-en-plaatsen]

## Conclusie
Mijn conclusie is dat de flexibiliteit van Jamstack zoveel beter is dan een log CMS die claimt alles te kunnen. Wat je vaak ziet dat een groot CMS het wel kan wat het claimt, maar dat het net niet lekker werkt. Een SaaS die zich specialiseert in dat ene onderdeel is altijd beter dan een groot CMS die het erbij heeft gemaakt.

De snelheid van NextJS en Vercel blijft mij verbazen, het statische site voordeel is zo gigantisch groot, het kostte ook bijna geen moeite om een 100% score te halen binnen Lighthouse.

Het feit dat features kunnen worden bekeken door een PO of tester na het committen van je changes scheelt ook veel in het ontwikkelproces.

Uniform biedt met canvas de mogelijkheid om de opbouw van je pagina's te bepalen met blokken die je kan verslepen. Daarnaast is de mogelijkheid om te personaliseren ook erg fijn, stel je hebt gezocht op een bepaalde behandeling in een ziekenhuis en je krijgt automatisch een link naar een folder te zien op een volgende pagina naast de contact gegevens (is maar 1 van de vele voorbeelden).

Mijn eindvraag is dan ook, waarom ben je nog niet over naar Jamstack?

## Demo
Hier kan je mijn PoC vinden: **[Serverless-Digital](https://demo-heartcore-uniform-nextjs.vercel.app/ "Serverless Digital")**

## Links
- [Vercel](https://vercel.com/ "Vercel")
- [Basin](https://usebasin.com/ "Use Basin")
- [Contentful](https://www.contentful.com/ "Contentful")
- [Uniform](https://uniform.app/ "Uniform")
- [NextJS](https://nextjs.org/ "NextJS")
- [Over mij](https://potential-sniffle.vercel.app/ "Over mij")