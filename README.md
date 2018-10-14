# 01-static-website-ChristianBlom84
## http://u01.christianblom.se

### En kort förklaring av kod för en responsiv iframe jag mestadels kopierade från nätet
´´´
@mixin responsiveiframecontainer($max-width) {
    max-width: $max-width;
    margin: auto;
}
´´´
Jag skapade en mixin för containern dels för att jag ville använda minst en mixin för att lära mig och det kändes som ett enkelt, men bra alternativ. Containern behövs för att behålla aspect ration vid en max-width. Sätter jag max-width på wrappern så blir den för hög om fönstret blir bredare än dess max-width då den tar sin padding från en % av föräldraelementet.

´´´
%responsiveiframewrapper {
    overflow: hidden;
    height: 0;
    position: relative;
}
´´´
Även här är en stor anledning till en extend att jag ville lära mig använda det och såg ett tillräckligt bra exempel. Wrappern har en height på 0 för att den får sin höjd baserat på paddingen som sätts separat för klasserna då den kan vara olika beroende på vad man vill ha för aspect ratio.

´´´
.videowrapper {
    @extend %responsiveiframewrapper;
    padding-bottom: 56.25%;
}
´´´
Wrappern till Youtube-filmen får en padding-bottom på 56.25% därför att källfilen har en aspect ratio på 16:9. 9/16 = 0.5625. Här är återigen anledningen till att man inte kan sätta en max-width på själva wrappern, för då blir höjden ändå 56.25% av föräldraelementet, därför behövs containern.

´´´
.responsiveiframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
}
´´´
Iframen fyller hela wrappern med relative-absolute och en höjd och bredd på 100%. I och med att höjden alltid är 56.25% av bredden så behålls rätt aspect ratio. Har man flera olika videor i olika format, t.ex. 4:3 kan man enkelt göra om %responsiveiframewrapper till en mixin som tar padding-bottom värdet som ett argument. Alternativt kan man ha olika specifika klasser för t.ex. 4:3 eller 16:9.