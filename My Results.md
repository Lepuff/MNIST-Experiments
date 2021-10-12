# Här är mina resultat hittils:

I den här filen ska ni beskriva:
- Era experiment
- Era slutsatser

## NOTE
    Vi har gjort våra tester främst på non-convolutional modellen, om inte frågan säger annat. Detta för att non-convolutional modellen tar betydligt kortare tid att träna, vilket möjliggör fler ändring på parametrar (så som batch size, lager av neuroner, antal neuroner, etc).


## 7
### a) 
    En högre learning rate innebär att varje epok har en högre vikt och då i teorin gör att modellen tränas snabbare. Men en för hög learning rate gör att resultaten uppdateras för mycket och modellen (kan) hamna på en sub-optimal lösning.
    Bilderna under visar learning rate 0.01 vs 0.1 och 0.5 vs 0.9
    

![Learning rate 0.01 vs 0.1](Charts/001vs01.svg "Learning rate 0.01 vs 0.1")
![Learning rate 0.5 vs 0.9](Charts/05vs09.svg "Learning rate 0.5 vs 0.9")

### b)
    Generellt så innebär en mindre batch size att du behöver göra färre uppdateringar för att uppnå en viss accuracy jämfört med en modell som har större batch size. Mindre batch sizes är ofta brusiga vilket innebär att det blir färre generaliseringsfel.
### c) 
    Convolutional modellen (CNN) är betydligt långsammare än non-convolutional. Med samma parametrar på båda modellerna uppnår CNN en högre accuracy. CNN modeller används främst för att minska komplexiteten för att processa data. Detta görs genom att filtrera bilden och minska dimensionerna. Genom att exempelvis stega igenom en 7x7 matris med en 3x3 kernel, så går vi från en 7x7 matris till 5x5 matris och därmed minskar komplexiteten. Detta kan upprepas. 

    Medan en non-convolutional modell (nCNN) går igenom varje pixel för sig.
    Nedan är en bild på skillnadena mellan dem två modellerna. Convolutional är dom två övre linjerna, non-convolutional är dom två undre.
![CNN vs nCNN](Charts/CvsNC_lr001_bs32.svg)

### d)
    non-convolutional model: Moved data accuracy: 14.74%
                             Rotated data accuracy: 80.12%
                             Test data accuracy: 96.17%
                             Train data accuracy: 97.2%

    convolutional model:     Moved data accuracy: 21.09%
                             Rotated data accuracy: 90.02%
                             Test data accuracy: 98.73%
                             Train data accuracy: 99.14%
    
    Generellt så har modellerna svårare att bedöma siffror som har flyttats än roterade siffror. Det är rimligt då det går att vrida en siffra tills den står "rätt". Medan det är svårare att veta vart en siffra finns om den inte är centrerad.

### e)
    Resultatet ökade när antalet neuroner ökade i det gömda lagret, upp till ungefär 300+, efter det blir förändring knappt märkbar.

### f)
Bilden nedan visar ett CNN där kernel är satt till (3,3), strides(1,1). Precisionen var betydligt sämre på roterade siffror.
![kernel(2,2)](fig/CNN_kernel33.svg)
Bilden nedan visar ett CNN där kernel(8,8), strides är satt till (2,2)
![strides(2,2)](fig/CNN_stride22.svg "strides(2,2)")
Kombinationation av kernel_size och strides som gav högst resultat var kernel(12,12) och strides(1,1). Efter det började precisionen minska.
![kernel(12,12), strides(1,1)](fig/CNN_kernel1212_strides11.svg "kernel(12,12), strides(1,1)")

### g)
    Ju fler lager som har lagts till -> träningstiden i sekunder ökar markant. Precisionen ökade något med fler gömda lager, gentemot neuroner i ett lager.
    Precisionen mellan 4st gömda lager och 6st gömda lager var i princip samma.

## 8)
### NOTE: vi sänkte batch_size till 32 för alla modeller i denna uppgift, då vi vid tidigare tester märkt att det gav en högre precision.


### Ugångspunkt (test 1):  
* Kernel(12,12)
* Strides(1,1)
* Epoker: 50st
* Learning rate: 0.01
* Gömda lager: 3st (128,64,32) neuroner


    Utifrån experimenten i uppgift 7 så tänkte vi att en bra start är att ta våra bästa värden därifrån och försöka göra ändringar utifrån våra lärdomar från dem. Convolutional-modellen (CNN) hade en betydligt högre precision än non-CNN, speciellt på roterad data. Den var också betydligt långsammare. Däremot så la vi också märkte till att i non-CNN modellen så var det bra att ha fler neuroner i 3 lager. Därav blev vår utgångspunkt att kombinera alla dessa värden tillsammans i en CNN modell.
### Resultat 1:
* Moved data 29.91
* Rotated data 91.66
* Test data 98.95
* Train data 99.73
* Tid 12:53

### Test 2
* Kernel(10,10) 
* Strides(1,1)
* Epoker: 50
* Learning rate: 0.01
* Gömda lager: 3st (128,64,32) neuroner

### Motivation till test 2:
    Vi testade att sänka kernel till 10,10. Detta eftersom att kombinationen med dom andra parametrarna inte nödvändigtvis behöver betyda att kernel(12,12) är bäst.

### Resultat 2:
* Moved data: 20.78
* Rotated data: 91.69
* Test data: 98.81
* Train data: 99.74
* Tid: 16:13

### Test 3:
* Kernel: (12,12)
* Strides: (2,2)
* Epoker: 50
* Learning rate: 0.01 
* Gömda lager: 0st

### Motivation till test 3:
    Vi testade att köra utan gömda lager (då vet märkt att varje lager ökar tidsåtgången), men med kernal(12,12) och strides(2,2). Detta för att se om precisionen skiljer sig mycket kontra tiden det tar att köra träningen.
### Resultat 3:
* Moved data: 21.35
* Rotated data: 88.12
* Test data: 98.3
* Train data: 98.62
* Tid: 8:35

### Test 4:
* Kernel: (12,12)
* Strides: (1,1)
* Epoker: 50
* Learning rate: 0.05
* Gömda lager: 3st (128,64,32) neuroner
### Motivation till test 4:
    Vi var intresserade över hur precisionen förändras om man tweakar learning rate faktorn lite.
### Resultat test 4:
* Moved data: 20.29
* Rotated data: 92.68
* Test data: 99.12
* Train data: 99.78
* Tid: 14:22

### Test 5:
* Kernel: (12,12)
* Strides: (1,1)
* Epoker: 50
* Learning rate: 0.03
* Gömda lager: 3st (128,64,32) neuroner
### Motivation till test 5:
    Vi upptäckte att en learning rate på 0.05 gav en marginellt bättre precision på allt utom moved data, där skillnaden var nästan 10 procenenheter (jämfört med test 1). Därför testade vi att ändra learning rate till 0.03 för att se hur det påverkar precisionen.
### Resultat test 5:
* Moved data: 21.01
* Rotated data: 92.04
* Test data: 98.95
* Train data: 99.76
* Tid: 13:28

## Slutsats
    För att jobba så effektivt som möjligt så genomförde vi träningarna på olika datorer parallellt, vilket förmodligen påverkar hur lång tid det tar att träna modellerna. Men det vi kom fram till var att det första testet gav bäst resultat. När vi ändrade learning rate så påverkade det moved data väldigt mycket, medan dom andra träningsseten var snarlika. Med mer tid skulle vi kunnat tweaka runt värdena lite mer, för att uppnå en marginell förbättring.




