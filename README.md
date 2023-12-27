# Kurs React od podstaw

## Wstęp

### Główne elementy

- JSX - składnia używana w React, podobna do HTML.
- komponenty - stanowe (komponent klasowy) i bezstanowy (komponent funkcyjny)
- state - stan
- props - właściwości

### Konfiguracja środowiska

- Visual Studio Code
  - pluginy: Live Server, Prettier, snippets, Material Icon Theme
  - Ustawienia: Format on Save = true 
- NODE.JS
  - Środowisku uruchomieniowe dla JS
  

```
npx create-react-app my-app
```

- Chrome, Firefox plugin
  - React Developer Tools
  - JSON Viewer


### Powtórzenie Javascript

- Funkcja strzałkowa

```javascript
const fn = (item) => {
	return console.log("Podany argument to " + item)
}

fn("Hej!")

//gdy jest 1 arg to nie potrzeba nawiasu 
//domyślnie wynik jest zwracacy
const fn = item => console.log("Podany argument to " + item)


fn("Hej!")

//to samo
const fn = (item) => (
	console.log("Podany argument to " + item)
)

const fn = (item, item2) => {
	return `Podany argument to: ${item} i ${item2}`
}
const result = fn("Hej!", "Ho!")

//to samo poniżej
const fn = (item, item2) => (
	return `Podany argument to: ${item} i ${item2}`
)
const result = fn("Hej!", "Ho!")

////
const btn = document.querySelector('button');
btn.addEventListener('click', () => console.log(this));
//this wskazuje na window (obiekt globalny)
//Funkcja strzałkowa nie tworzy własnego przypisania do this, a je dziedziczy z poprzedniego kontekstu

const btn = document.querySelector('button')
btn.addEventListener('click', function() {
console.log(this)
})
//this wskazuje na element, na którym wywołane zostało zdarzenie

```

- Metoda `join()`

```javascript

const users = ["adam", "bogdan", "czarek", "darek"];
//zwraca stringa z tablicy. Oryginalna tablica pozostaje bez zmian
const usersString = users.join(" ");
console.log(usersString); //"adam bogdan czarek darek"
```
- Metoda `concat()`

```javascript
const users = ["adam", "bogdan", "czarek", "darek"];

//łączymy tablicę z innym elementem lub inna tablicą i zwracamy nową tablicę

const newUser = "edyta"
const allUsers = users.concat(newUser)
console.log(allUsers);
```
- Operator spread - alternatywa dla concat

```javascript
const users = ["adam", "bogdan", "czarek", "darek"];
const allUsers = [...users, "edyta"]
console.log(allUsers);
```
- Metoda `map()` - przykład 1

```
const users = ["adam", "bogdan", "czarek", "darek"];
// metoda map() wraca nową tablicę o tej samej długości

const usersFirstLetterUpperCase = users.map(user => user[0].toUpperCase())

console.log(usersFirstLetterUpperCase)
```
- Metoda `map()` - przykład 2

```
const numbers = [2, 3, 4]
const doubleNumber = number.map(number => number * 2)
console.log(doubleNumber);
```
- Metoda `forEach()` - przykład 1

```
const usersAge = [20, 21, 23, 43];
// string templating
usersAge.forEach(age => console.log(`W przyszłym roku użytjownik będize miał ${age + 1} lat`))
```
- Metoda `forEach()` - przykład 2

```
const usersAge = [20, 21, 23, 43];
let usersTotalAge = 0;

usersAge,forEach(age => usersTotalAge += age);
console.log(usersTotalAge);
```
- Metoda `forEach()` - przykład 3

```
const usersAge = [20, 21, 23, 43];
const section = document.createElement('section')
//przekazujemy 3 parametry: 
//obecny element, index tego elementu i tablica 
usersAge.forEach((age, index, array) => {
section.innerHTML += (
`<h1> Użytkownik ${index + 1}</h1>
<p>wiek: ${age}</p>`
)
if(index === array.length - 1){
	document.body.appendChild(section);
	}

})
```
- Metoda `filter()` - przykład 1
```
const users = ["adam", "bogdan", "czarek", "darek"];

const NameWith6Letter = users.filter(user => user.length === 6)

console.log(NameWith6Letter);
```
- Metoda `filter()` - przykład 2

```
const users = ["adam", "bogdan", "czarek", "darek"];
const NameWithLetterK = users.filter((user) => {
	return (
		user.indexOf("k") > -1
	)
})
console.log(NameWithLetterK);
```
- Metoda find()

```
//Metoda find zwraca element, który jako pierwszy zwróci true(spełnia warunek).
//Jesli w żadnej iteracji nie będzie spełniony warunek, to zwróci undefined.

const customers = [
	{name: "Adam", age: 67},
	{name: "Basia", age: 27},
	{name: "Marta", age: 17}
];

const firstAdultUser = customers.find(customer => customer.age >= 18)
console.log(firstAdultUser);

```
#### Obiekty klasy, instancje, dziedziczenie

- Klasa - właściwości instancji i prototyp
```
//deklaracja klasy
class City {

}

//tworzenie instancji klasy
const Warwaw = new City();
const NewYork = new City();


class Country {
	constructor(name, capital, population){
		this.name = name;
		this.capital = capital;
		this.population = population;
	}
}

const poland = nnew Country('Polska', 'Warszawa', 38000000);

```
- Klasa - dodawanie metod do prototypów i instancji
  Metody są wyszukiwane w kolejności:
  - instancja
  - prototyp
  - prototyp klasy Object  	

```javascript
class Country {
	constructor(name) {
		this.name = name; //właściwość instancji
		this.showName = () => console.log(this.name);//metoda instancji
	}
	//metoda teorzona w klasie znajdzie się z prototypie klasy, do której mają dostęp wszystkie instancje
	showCountryName(){
		console.log(`Nazwa kraju to ${this.name}`);
	}
}

const Poland = new Country('Polska');
const Italy = new Country('Italia');

Poland.showCountryName(); // Nazwa kraju to Polska
Italy.showCountryName(); // Nazwa kraju to Italia
Poland.showName(); // Polska
Italy.showName(); // Italia
```
- Klasa - dziedziczenie

```
class Person {
	constructor(name) {
		this.name = name;
	}
	showName(){
		console.log(`Imię osoby to ${this.name}`);
	}
}

class Student extends Person {
	constructor(name = "", degrees = []){
		super(name)
		this.degrees = degrees
	}
	
	showDegrees() {
		const completed = this.degrees.filter(degree => 2)
		console.log(`Student ${this.name} ma stopnie ${this.degrees} i zaliczył już ${(completed.length) przedmiotów}`)
	}
}

const Janek = new Student("Adam", [2,3,4,5,2,3])
Janek.showDegrees() //Student Adam ma stopnie: 2,3,4,5,2,3 i zaliczył już 4 przedniotów
```

#### Mechanizm this
- Meachanizm this polega na wiązaniu słowa kluczowego this z obiektem. Wiązanie to jest tworzone w chwili wywołania funkcji. Wiązanie domyślnie następuje automatycznie, ale możemy je zmienić.

```
//zakres globalny

//do this nic nie jest przypisane 
"use strict"
const fn = function() {
	console.log(this);
}
fn()
//undefined


//do this zostanie przypisany obiekt Window

const fn = function() {
	console.log(this);
}
fn()
//Window

```
- **this** wskazuje na obiekt nadrzędny, z zakresu którego zostało wywołane
- Funkcja strzałkow powoduje z this nie wskazuje na obiekt, z którego została wywołana, ale obiekt z zakresu wyższego 
```
const car = {
	brand: 'opel',
	age: 2018,
	showAge(){
		console.log(`samochód z ${this.age}`);
	},
	showBrand: () => {
		console.log(`samochód marki ${this.brand}`);
	}
}

car.showAge() //samochów z 2018
car.showBrand() //samochód marki undefined (dziedziczy po zakresie wyższym a w zakresie wyższym jest window. Więc window.brand zwraca nam undefined)
```
- Problem 1

```javascript

const dog = {
	name: 'rocky',
	showName(){
		console.log("Imię psa to " + this.name);
	}
} 

dog.showName() // Imię psa to rocky

//this stracił dostep do obiektu dog
const dogName = dog.showName
dogName() //Cannot read property 'name' of undefined
```
- Problem 2 
```javascript
const cat = {
	kids : ['lucek', 'łapciuch'],
	showKidsNames() {
		console.log(`kot ma potomstwo: ${this.kids}`);
		//this straci dostep do obiektu cat
		const showKidsNumber = function() {
			console.log(this.kids.length);
		}
		
		showKidsNumber()
	}
}
cat.showKidsNames()
// showKidsNames() - kot ma potomstwo: lucek, łapciuch
// showKidsNumber - Cannot read property 'kids' of undefined 
```
- bind() - trwałe przypisanie this 
```
cat.showName() //wykonane na obiekcie cat, wiązanie domyślnie będzie do obiektu cat.

cat.showName.bind(dog) //zwraca nową funkcję o tej samej nazwie (nie wywołuje jej), ale z przypisanym na stałe do this nowym obiektem. This nie będzie się już definiować w chwili wywołania metody, ono będzie wtedy miało przypisany do siebie obiekt dog.
```
- Przykład użycia rozwiazania problemu 1
```javascript

const dog = {
	name: 'rocky',
	showName(){
		console.log("Imię psa to " + this.name);
	}
} 

dog.showName() // Imię psa to rocky

//this jest wiązany z obiektem dog
const dogName = dog.showName.bind(dog)

dogName() // Imię psa to rocky
```
- Przykład użycia rozwiazania problemu 2
```javascript
const cat = {
	kids : ['lucek', 'łapciuch'],
	showKidsNames() {
		console.log(`kot ma potomstwo: ${this.kids}`);
		
		//metoda jest wiazana z 'this' ktore w tym momencie wskazuje na cat
		const showKidsNumber = function() {
			console.log(this.kids.length);
		}.bind(this)
		
		showKidsNumber()
	}
}
cat.showKidsNames()
// showKidsNames() - kot ma potomstwo: lucek, łapciuch
// showKidsNumber - 2
```
- ALternatrywne rozwiazanie : funkcja strzałkowa
```javascript
const cat = {
	kids : ['lucek', 'łapciuch'],
	showKidsNames() {
		console.log(`kot ma potomstwo: ${this.kids}`);
		
		const showKidsNumber = () => {
			console.log(this.kids.length);
		}.bind(this)
		
		showKidsNumber()
	}
}
cat.showKidsNames()
// showKidsNames() - kot ma potomstwo: lucek, łapciuch
// showKidsNumber - 2
```
