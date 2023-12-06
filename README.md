### Vererbung und Polymorphismus in CSharp ###

Ein Beispiel:
* **Animal**: Ein Tier
* **Duck**: Eine Subklasse von **Animal** 
	* Duck erbt Eigenschaften und Methoden von Animal
* **Cat**: Eine Subklasse von **Animal**
* **Mouse**: Eine Subklasse von **Animal**

(Wichtig: Duck **IST** Animal)

![[Vererbung-CSharp-1.png]]

Construktor (ctor) der Basisklasse aufrufen
![[Vererbung-CSharp-2_Konstrukor.png]]
Der Aufruf des Konstruktors der Basisklasse wird immer **VOR** dem Aufruf des Konstruktors der Subklasse gemacht.
So werden zuerst die Eigenschaften der Basisklasse, dann die Eigenschaften der abgeleiteten Klasse initialisiert.
Wenn der Konstruktor der Basisklasse nicht angegeben wird, so wird der Default-Konstruktor (base()) verwendet (in dem Fall Animal() ohne Parameter).

Ein Konstruktor kann auch einen weiteren Konstruktor derselben Klasse aufrufen.
![[Vererbung-CSharp-2_Konstrukorweiterleitung.png]]

Mit dem Operator **is** kann man prüfen, ob ein Objekt von einem bestimmten Typ ist.
Beispiel:
```csharp
Animal tom = new Cat("Tom", 3, 20);
bool isMouse = tom is Mouse;// false
bool isCat = tom is Cat; // true
```
------------------
-------------------
#### Polymorphismus in CSharp ####
Polymorphismus heißt Vielgestaltigkeit (d.h. ein Objekt vom Typ der Basisklasse kann sich so verhalten wie ein Objekt der Subklasse).

Bsp: Eine Asiatische Katze (AsianCat), die als Cat oder Animal betrachtet werden kann.
Verwendet man die Referenz auf die Basisklasse (Animal), so würde der Aufruf von "Move()" immer "Animal Move" liefern (obwohl auch die Klasse Cat eine Methode mit der gleichen Signatur anbietet).

![[Polymorphismus-CSharp-1.png]]
Deswegen muss man spezielle Vorkehrungen treffen, damit die Methode der Subklasse (Cat) zum Zuge kommt.
Mittels des Schlüsselwortes "**override**" wird angezeigt, dass die Methode der Subklasse die Methode der Basisklasse "überschreibt".

Bsp:
```csharp
// Eine Katze erzeugen und einer Variablen vom Typ Animal zuweisen
// ** Das Objekt 'tom' als Animal "erklärt"
// Deshalb kann es auch nur die Methode von Animal aufrufen
Animal tom = new Cat("Tom", 3, 20); 

// Die Methode Sleep aufrufen (von Animal)
tom.Sleep();

// - Move() ist die Methode, die in der Klasse Animal definiert wurde
// - Move() wird in der Klasse Cat überschrieben (override)
// 'tom' ist in der Praxis eine Katze, obwohl es als Animal "erklärt" (zugewiesen) wird
// ==> Es ruft die Methode Move() auf, die in der Klasse Cat definiert wurde
tom.Move(); // ==> Cat Move
```

Will man diese Überschreibung nicht, dann benutzt man das Schlüsselwort "**new**"
![[Polymorphismus-CSharp-2(override).png]]
 Bsp:
 ```csharp
// Sie erstellen eine Ente, weisen das Ergebnis aber einem Objekt vom Type Animal zu
Animal donald = new Duck("Donald");

// Der Aufruf der Methode Sleep() (in der Klasse Animal definiert).
donald.Sleep();

// - Move() ist die Methode, die in der Klasse Animal definiert wurde
// - Move() wird mit dem Schlüsselwort 'new' in der Klasse Duck "überdeckt"
// 'new' Move() wird für Objekte vom Typ Duck (oder Subklassen von Duck) benutzt
// 'donald' wird als  'Animal', nicht als 'Duck' benutzt
donald.Move(); // ==> Animal Move.  
```