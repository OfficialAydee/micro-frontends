# micro-frontends

## Initialisatie

Create workspace:
$ npx create-nx-workspace micro-frontends
✔ Which stack do you want to use? · angular
✔ Integrated monorepo, or standalone project? · integrated
✔ Application name · micro-frontends
✔ Which bundler would you like to use? · webpack
✔ Default stylesheet format · scss
✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? · Yes
✔ Test runner to use for end to end (E2E) tests · cypress
✔ Do you want Nx Cloud to make your CI fast? · skip

## Opzet host omgeving

Dit commando genereert een hostapplicatie voor de micro frontends architectuur. De hostapplicatie fungeert als de overkoepelende applicatie die de micro frontends integreert. Hier wordt ook server-side rendering (SSR) ingeschakeld.

$ npx nx generate @nx/angular:host --name=host --ssr=true --directory=apps/host --prefix=matchmaker --dynamic=true --projectNameAndRootFormat=as-provided --standalone=false --style=scss

DE OPTIES HEBBEN DE VOLGENDE BETEKENISSEN:
--SSR=TRUE: SCHAKELT SERVER-SIDE RENDERING (SSR) IN VOOR DE HOST APPLICATIE.
--DIRECTORY=APPS/HOST: PLAATST DE HOST APPLICATIE IN DE "APPS/HOST" DIRECTORY.
--PREFIX=MATCHMAKER: VOEGT HET PREFIX "MATCHMAKER" TOE AAN ALLE COMPONENT NAMEN.
--DYNAMIC=TRUE: MAAKT DE HOST APPLICATIE DYNAMIC, ZODAT DEZE REMOTE MICRO-FRONTENDS KAN LADEN.
--PROJECTNAMEANDROOTFORMAT=AS-PROVIDED: HOUDT DE PROJECT NAAM EN ROOT DIRECTORY ZOALS OPGEGEVEN.
--STANDALONE=FALSE: MAAKT DE HOST APPLICATIE NIET STANDALONE, ZODAT DEZE AFHANKELIJK IS VAN ANDERE APPLICATIES.
--STYLE=SCSS: GEBRUIKT SCSS VOOR STYLESHEETS.

## Opzet remote omgeving

Dit commando genereert een remote (micro frontend) applicatie die zal worden gehost binnen de hostapplicatie. Het definieert de naam van de remote, de host waaraan het wordt gekoppeld, de directory waarin het wordt gegenereerd, de poort waarop het draait en andere configuratieopties.

$ npx nx generate @nx/angular:remote --name=[naam van remote] --host=host --directory=apps/[naam van remote] --port=[port nummer] --prefix=matchmaker --projectNameAndRootFormat=as-provided --ssr=true --standalone=false --style=scss

DE OPTIES HEBBEN DE VOLGENDE BETEKENISSEN:
--NAME=[NAAM VAN REMOTE]: VERVANG DIT MET DE GEWENSTE NAAM VOOR DE REMOTE APPLICATIE.
--HOST=HOST: KOPPELT DE REMOTE APPLICATIE AAN DE "HOST" APPLICATIE.
--DIRECTORY=APPS/[NAAM VAN REMOTE]: PLAATST DE REMOTE APPLICATIE IN DE "APPS/[NAAM VAN REMOTE]" DIRECTORY.
--PORT=[PORT NUMMER]: STEL HIER HET POORTNUMMER IN WAAROP DE REMOTE APPLICATIE DRAAIT.

Dit commando genereert een component binnen een remote project. Het component zal worden gebruikt in de remote applicatie en wordt gegenereerd binnen een specifieke directory in het remote project.

$ npx nx generate @nx/angular:component --name=[naam van component] --directory=apps/[naam van remote project]/src/app/remote-entry/[gegeven naam van component] --standalone=false --prefix=matchmaker --style=scss

DE OPTIES HEBBEN DE VOLGENDE BETEKENISSEN:
--NAME=[NAAM VAN COMPONENT]: VERVANG DIT MET DE GEWENSTE NAAM VOOR DE COMPONENT.
--DIRECTORY=APPS/[NAAM VAN REMOTE PROJECT]/SRC/APP/REMOTE-ENTRY/[GEGEVEN NAAM VAN COMPONENT]: PLAATST DE COMPONENT IN DE OPGEGEVEN DIRECTORY.

## Draaien van code

$ cd micro-frontends

$ npx nx serve host --devRemotes=mf1,mf2 (mf1 en mf2 zijn de namen van remote)

## Opzet gedeelde library

Dit commando genereert een gedeelde bibliotheek die wordt gebruikt door meerdere projecten binnen de workspace. Het creëert een aparte bibliotheek met de opgegeven naam.

$ npx nx g @nx/angular:lib libs/shared/data-access-[naam van library dat gedeeld wordt] —standalone=false

DEZE COMMANDO GENEREERT EEN GEDEELDE LIBRARY MET DE NAAM DATA-ACCESS-[NAAM VAN LIBRARY DAT GEDEELD WORDT] IN DE "LIBS/SHARED" DIRECTORY.
--STANDALONE=FALSE: MAAKT DE LIBRARY NIET STANDALONE, ZODAT DEZE DOOR ANDERE APPLICATIES GEBRUIKT KAN WORDEN.

Dit commando genereert een gedeelde service binnen de gedeelde bibliotheek die eerder is gegenereerd. De service kan worden gebruikt door verschillende projecten binnen de workspace.

$ npx nx g @nx/angular:service [naam van service] --project=data-access-[naam van library dat gedeeld wordt]

DEZE COMMANDO GENEREERT EEN SERVICE MET DE NAAM [NAAM VAN SERVICE] BINNEN DE OPGEGEVEN DATA-ACCESS-[NAAM VAN LIBRARY DAT GEDEELD WORDT] LIBRARY.
