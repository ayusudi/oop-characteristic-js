# OOP Characteristic JS 

## INDEX
```js
class Smartphone {
  constructor(cpu, ram, color) {
    this.cpu = cpu;
    this.ram = ram;
    this.color = color;
  }
}
```


## Reminder
```diff
+ Abstraction
+ Encapsulation
+ Inheritance
+ Polymorphism
```

### Abstraction

Menyembunyikan sebuah proses dari user di dalam method, user hanya mengetahui efek dari proses yang di abstraksi

#### Contoh abstraction menggunakan `built-in function javascript`

```js
// Menggunakan class Date dari javascript
const today = new Date();

// Menggunakan method toLocaleDateString untuk mendapatkan format dd/mm/yyyy
// Dengan Abstaraction cukup mengetahui efek method
console.log(today.toLocaleDateString());
```

#### Contoh abstraction kepada soal

```js
class Smartphone {
  constructor(cpu, ram, color) {
    this.cpu = cpu;
    this.ram = ram;
    this.color = color;
  }

  switchOn() { // Proses logic yang tidak perlu di ketahui oleh user
    // input : "13.00"
    // output : "Smartphone is booting up at 13.00 WIB"
  }

  displayInformation() {
    /** 
     * OUTPUT:
     * 
     * Info / Spesification 
     * --------------------
     * Color   : Black
     * RAM     : 4 GB
     * CPU     : Exynos 9911
     */
  }
}

const samsung = new Smartphone("Exynos 9911", 4, "Black");

// Yang diketahui oleh user hanya efek dari method, bukan prosesnya
samsung.switchOn();
samsung.displayInformation();
```


### Encapsulation

Menyembunyikan internal, di kasus javascript hanya propertynya saja, dari luar classnya sendiri.  
Gunakan Assesor (Getter) dan Mutator (Setter) agar dapat mengakses dan reassign propery dari luar class.

> **Note: Jelaskan kalau private property belum di support di javascript.**

```js
class Smartphone {
  constructor(cpu, ram, color) {
    // Menggunakan # sebagai penanda property tersebut adalah private property
  }

  // Gunakan assesor (Getter) agar property dapat di akses dari luar class
  // Getter : Memberikan value property private 
  get cpu() {
    // returning some value
  }
  get ramGB(){
    // output : 4 GB
  }

  // Gunakan mutator (Setter) agar property dapat reassign dari luar class
  // Setter : Reassignment value property private
  set cpu(newCPU) {
    //....
  }
}

const samsung = new Smartphone("Exynos 9911", 4, "Black");

console.log(samsung.cpu); // OKEY AS LONG AS THERE'S GETTER~
console.log(samsung.#cpu); //! NOT ALLOWED !

// Cara menggunakan setter, seperti reassign value property biasa
samsung.cpu = "A14";
```

### Inheritance

Proses menurukan karakteristik dari suatu parent class ke child class.

```js
class Android extends Smartphone {
  // Contructor di child class dan parent class berbeda
  constructor(cpu, ram, color) {
    // Super untuk mempassing value dari constructornya child ke constructornya parent
    // Jika ada default value, maka langsung saja di tulis valuenya di super
    super("CPU Android", ram, color);
  }
  iamAndroid(){
    console.log("Smartphone Android YoO")
  }
}

class IOS extends Smartphone {
  constructor(cpu, ram, color, version) {
    super("CPU IOS", ram, color);
    this._version = version;
  }
  iamIOS(){
    console.log("Smartphone Iphone YOo")
  }
}

const iPhone = new IOS("A14x", 6, "Silver", "14.121");
```

### Polymorphism

Menggunakan nama method yang sama di beberapa class yang berhubungan, dan menghasilkan hasil yang berbeda.

#### Overriding

method di child class akan menggantikan method di parent class.

```js
class Animal {
  constructor(name, type) {
    this.name = name;
    this.type = type;
  }

  speak() {
    console.log(`${this.name} is Speaking`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name, "Dog");
  }

  // Akan override method speak di class Animal
  speak() {
    console.log(`Woof!`);
  }
}

class Wolf extends Animal {
  constructor(name) {
    super(name, "Wolf");
  }

  // Akan override method speak di class Animal
  speak() {
    console.log(`HOWWWLLLLLL!`);
  }
}

// Walaupun ketiga instance memanggil method yang sama, akan menghasilkan hasil yang berbeda
// Karena method di child class akan mengorride method di parent class
const cat = new Animal("Kitty", "Cat");
cat.speak(); // Kitty is Speaking

const dog = new Dog("Doggy");
dog.speak(); // Woof!

const wolf = new Wolf("Wolffy");
wolf.speak(); // HOWWWLLLLLL!
```
