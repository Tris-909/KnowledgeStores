# Some commands in GoLang ?

- `go build` Compile codes
- `go run` Compile and execute one or two files
- `go fmt` Format code in each file in the directory
- `go install` Compile and install a package
- `go get` Download the raw source code of someone's else package
- `go test` Run any tests in the current project

# Imports

- In a Go file. We can import another file by name. Let's say file 2 is called `package helper`. In file 1 we can use `import "helper"` to import the file 2 so file 1 can have access to all functions in file 2.

# Wording

- `package` == `project` == `main` Every package inside GoLang acts like a project, in every single file if they are all belongs to a project they will have something like `package ${name}` ${name} is the `package` if 2 files have that meaning 2 files belong to "project" . **Files that are belong to a project don't need to import each other to use each other functions**
- There are 2 types of Packages in Go, `Executable` and `Reusable` :
  - `Executable` generates file that we can run. Package that is `Executable` will always called **`main`** any other names that file will be a `Reusable` code in Go. Also in an `Executable` file, we always need to declare a function called `main`.
  - `Reusable` Code used as helper functions
- Finding packages in Golang at https://pkg.go.dev/

# Structure of a file in Go

- Every single file in Go composed of 3 parts : Package declaration, Import other packages, Declaration of Functions

```
package main

import "fmt"

func main() {

}
```

<h1> Go languages </h1>

<h3> 1. Declare a variable </h3>

- Go is a static type language like TypeScript
- There are a few types in Go like : bool, string, int, float64, array, map, custom type
- We can declare a variable like :

```
  var name string = "Tri";
  // Or
  name := "Tri";
```

The second way of declaration is a short form of declaration of Golang. We let the compiler decides on it owns what type we are assigning to it and we only need to use `:` the first time

<h3> 2. Functions </h3>

Function inside Go need to be assigned the type of the return value

```
func main() string {
  return "String"
}
```

<h3> 3. Array and Slice </h3>

- Array is a FIXED length array. Elements inside Array can be different types.
- Slice is a array that can grow or shrink. Every element inside Slice must be the same type.

```
// How to declare an array in Golang
array_name := [length_of_array]Type{item1,item2,item3}

// How to loop over an array in Golang
for i, card := range cards {
  fmt.Println(i, card);
}
```

- You can use `append` to add new item into an array and also remove an item based on index in the array using `append`

```
  // Adding an item
  append(current_array, new_item)
  // Removing an item based on index
  func helperFunc(current_array, index) {
    newArray = append(current_array[:index], current_array[index+1:]...)
    return newArray
  }
```

- `:index` meaning from position 0 to index
- `index+1:` meaning from position index plus one to the end of the array
- `...` to expand the array with another array
- You can also called a sub-array from a mother array using a range index by `current_array[start_index:end_index]`

<h3> 4. Declare a type in Go and receiver function </h3>

- You can declare a type following syntax

```
type ${typeName} ${kind of type}
type deck string[];
```

- Receiver functions are functions that a variable can access to it if it is assigned type related to that receiver

```
type decks string[]

//  (d decks) is called the receiver part
// without this it is just a normal function
func (d decks) test() {
  for i, deck := range d {
    fmt.Println(i, deck)
  }
}

// In main file
func main() {
  newDecks := decks{"1", "2"}

  newDecks.test()
}

// Model
variable <-- type <-- receiver function 1 2 3

```

The block code above show you how you can declare a type, declare a receiver function related to that type, assign that customed type you have created to a variable, and that variable now have access to any receiver functions related to that type.

<h3> 5. Working with files, what is a byte slice, strings.Join method, TYPE CASTING, nil </h3>

- There is a way to write a file ( if the file is not there then system will create one ) using package `ioutil`

```
byte_value := []byte(the_string)
// byte_value must be a STRING
// 0644 is the permission (fixed value for Window)
ioutil.WriteFile(file_name, byte_value, 0644)
```

- byte_value is a string that is translated from each every characters ( "a", "b", ... ) to number preresent a byte.

- `strings.Join` is a method that we can use to create a string out of an array of strings

```
  // first argument is the array
  // second argument is the string value that gonna get attached after every single element in the array to form a string
	cardString := strings.Join(cards, " \n");
```

- Type casting is a method you can use to converse a value of type A to type B if it is doable.

```
byteArray := []byte{[56 32 111 102 32 83 112 97 100 101 115 32 10 49 48 32 111 102 32 83 112 97 100 101 115 32 10 51 32 111 102 32 67 108 111 118 101 114 115 32 10 54 32 111 102
32 68 105 97 109 111 110 100 115 32 10 49 48 32 111 102 32 67 108 111 118 101 114 115]}
string := string(byteArray)
```

- `nil` in Go is somewhat like `null` in JavaScript

<h3> 6. Testing with Go </h3>

- Testing with Go is like writing actual plain Go code to test your function.
- You need to run `go mod init $current_path_dir` to create `go.mod` file. You need this file before you can run `go.test`
- Every test file in Go need to end with **`_test.go`** so the command line can pick it up
- `t *testing.T` is required for all test files in the argument of a test file

```
package main

import "testing"

func TestNewDeck(t *testing.T) {
	newCards := newDeck()
	expectedNumberOfCards := 52
	if len(newCards) != expectedNumberOfCards {
		t.Errorf("Expected length of 52 but got %v", len(newCards))
	}

	expectedFirstCard := "1 of Spades";
	if newCards[0] != expectedFirstCard {
		t.Errorf("Expected first card to be %v but got %v", expectedFirstCard, newCards[0])
	}

	expectedLastCard := "K of Hearts";
	if newCards[expectedNumberOfCards-1] != expectedLastCard {
		t.Errorf("Expected last card to be %v but got %v", expectedLastCard, newCards[expectedNumberOfCards-1])
	}
}
```

<h3> 7. Struct in Go ( similar to Object in JavaScript ) </h3>

- Declaring a struct in Go :
- Declaring a second struct and create
- Assigning that to a variable that has structure of first struct that includes second struct :
- Updating value of that variable

```
type person struct {
	firstName string
	lastName  string
  contactInfo contact
}

type contact struct {
  phoneNumber string
  countryCode string
}

func main() {
  tri := person{firstName: "Tri", lastName: "Tran", contactInfo: contact{phoneNumber: "XXXX", countryCode: "+XX"} }
  // declare thao variable with zero values
  var thao person
  // update thao struct
  thao.firstName = "Thao"
  thao.lastName = "Nguyen"
  thao.contactInfo.phoneNumber = "XXXXX"
}
```

<h3> Pointer for Struct </h3>

- Pointer as the name suggesting pointing to the memory address of a value. We need a pointer to update value of a struct via receiver function. For example :

```
type person struct {
	name string
}

func main() {
  tri := person{ name: "Tri" }
  tri.updateName("Frey");
  fmt.Println(tri);
}

func (p person) updateName(name string) {
  p.name = name;
}
```

- The block of code above won't work because the memory address of `tri` is different from `p` even if updateName is a receiver function of person and tri is type person. Thus why we need a pointer to point `p` to `tri` so any data updated to `p`, `tri` will reflect it.

```
  // Create a pointer
  triPointer := &tri;

  // Update receiver function to use pointer for function
  func (triPointer *person) updateName(name string) {
    (*triPointer).name = name;
  }
```

- There are 2 meanings to `*` :
  - `*` before a value will tell you value that are stored at which pointer point to
  - `*` before a type will tell you that we are working with a pointer to the type
- `&variable` to read the memory address of the value
- For receiver function we need to declare like `(name_of_pointer *type_that_receiver_connect_to)`

<h2> IMPORTANT NOTE : </h2>
- If you create a reciver that has a pointer point to a type, then you don't need to create a pointer like this. Go will understand it automatically and does it for you. So any updates you want to make using that receiver because it has a receiver it will update the value to the actual variable at the right memory address

```
  // Do not need to create a pointer if you use a pointer in a receiver function itself
  triPointer := &tri;
```

<h3> Reference Types and Value Types </h3>

- You have to handle `pointer` for Value Types : int, float, string, bool, struct
- You don't have to worry about `pointer` for Reference Types : slices, maps, channels, pointers, functions

<h3> 8. Maps </h3>

- A map is a struct where ALL key and value are the same type

- To declare a map, looping through a map will have `i` as `key`

```
  colors := map[string]string {
    "white": "#fff",
  }

  for key, value := range colors {
    Println(key,value)
  }
```

<h3> 9. Interfaces </h3>

- Interface is used to reduce repetitive code in our codebase. It is a thing that holds one or many functions. A value of that interface type can hold any value that implements those functions.

- Following example will show you that both triangle and square use a printArea function to print out their area even thou the formula to calculate the area may be different.
- In order to print out area of any shape we need to be able to calculate the area of that shape so any shape we can calculate area will satisfy `Shape interface`.
- We then create a function that will receive a variable that satisfied `Shape` to print out it area.
- So from now on, whatever shape can satisfy `Shape interface` will be able to call `printArea`

```
package main

import "fmt"

type triangle struct {
	height float64
	base   float64
}

type square struct {
	sideLength float64
}

type shape interface {
	getArea() float64
}

func (t triangle) getArea() float64 {
	return 0.5 * t.base * t.height
}

func (s square) getArea() float64 {
	return s.sideLength * s.sideLength
}

func printArea(s shape) {
	fmt.Println(s.getArea())
}

func main() {
	s := square{sideLength: 10}
	t := triangle{base: 10, height: 10}
	printArea(s)
	printArea(t)
}

```

<h3> 10. Routines and Channels </h3>

- A Go Routine is a runner run our code.
- To create a Go Routine we can call `go` keyword before any function then Golang will start a Routine to run that code for us

```
  go function()
```

- Note this is important to read to understand how a Go Routine works :

```
func main() {
	links := []string{
		"https://google.com",
		"https://facebook.com",
		"https://stackoverflow.com",
		"https://golang.org",
		"https://amazon.com",
	}

	for _, link := range links {
    // Create a Go Routine
		go checkLink(link)
	}
}

func checkLink(link string) {
	_, err := http.Get(link)

	if err != nil {
		fmt.Println(link + " is down!")
		return
	}

	fmt.Println(link, "is still working fine")
}
```

- The program above try to reach out to five websites to see if they are working or not. Without Go Routine we will have to wait it to reach out to every website line by line from top to bottom. Adding `go` keyword before `checkLink` function will create a routine it will run every code inside `checkLink` and don't make the MAIN Routine wait ( the MAIN Routine is whatever run our code with or without Go Routine ).
- The first Go Routine will go inside `checkLink` and see they are getting block and have to wait for a response from `google.com`. So the Main Routine will keep running and this time it will create another Go Routine to check the status of `facebook.com`. Just like it's brother Go Routine the first, it also gets blocked so the Main Routine won't have to wait it because the Go Routine will run code on it owns and so on.
- Whatever response comes back first from any websites will get Print out by the child Go Routines.
- So in short, Go Routine saves time running our code if we don't want to wait for the response from the outa source

<h4> Go Routine under the hood </h4>

- Go Routines are managed with Go Scheduler, every Go Scheduler is working with a CPU to run the code and GoLang default the number of CPU it works with by 1.
- Go Scheduler can manage multiple Go Routines and every single Go Scheduler connect to a single CPU. If we have multiple CPUs we will have multiple Go Scheduler if we configure it.
- The reason why we need to understand this is because, Go Routines are not running in parallel as we think it is. Go Routines run it codes through a Go Scheduler on a CPU one at a time if we only have one CPU that is.
- Says there is a Go Scheduler and 3 Go Routines connect to a CPU. It will run Go Routines code concurrently meaning that it will pick up code from Go Routine 1 and run still it get blocked then it will run Go Routine 2 code until it get blocked and now depends whether Go Routine 1 is still getting block or not if yes then it will run Go Routine 3 let's say, and so on forward.
