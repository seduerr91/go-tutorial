# Golang Tutorial for Beginners | Full Go Course

Videolink: <https://www.youtube.com/watch?v=yyUHQIec83I>

## Main benefits of Go

- Go is built for corountines called goroutines
- Go is a serverside / backend only language: web servers, microservices
- Go is fast and efficient, and is a compiled language (binary compiles to executable)
- Go raises compile errors to enforce better code quality, e.g. variable names need to be used
- Go has integrated type checking and implies a datatype if you assign it immediately

## Setting up a Project

1. Create a main: $ touch main.go
2. Initialize the project with: $ go work init 'project name'
3. Edit the file

    Declare an entry point: with func main() {
        // logic
    }
    Import all dependencies (e.g. 'fmt' for print)

4. Execute with go run 'filename'

## Data Types

- Strings
- Booleans
- Arrays
- Integers
- Maps

## What is a pointer?

How: Pointers are set with & (ampersand)
Why: Save a variable to memory in order to use it later.
What: Pointer is a value that points to a memory address of another variable that references the actual value.

Java and JS, Python do not have pointers.

## Arrays in Go

- Arrays in go have a fixed size (how many elements the array can hold).
- Only the same data type can be stored (e.g., strings).
- We can add and delete elements from list during execution.

Syntax: var bookings = [50]string{"Seb", "Joy", "Peter"}

- with [] defining an array / list in Python
- with 50 being the size of the array
- with {"item1"} being default values

Syntax 2: var bookings [50]string

- with array type string
- with a size of 50

Adding new elements by indexing their position

bookings[0]: position of first element
bookings[0] = "Seb" : assinging to first value
bookings[10] = "Teresa" : assinging to 10th value

Variables need to be defined first, and can only used after.
Get the size of arrays with: len()

## Slices

- Abstractions of array that are dynamic in size, like Python lists.
- Slices are also index-based and have a size, but are resized when needed.
- Syntax: var booking[]string
- Alternative syntax: var bookings = []string{} to define default value
- Add an element with: bookings = append(sliceName, elementToAdd)
- e.g. bookings = append(bookings, firstName + " " + lastName)

## Loops

- only one loop: for (not while, do-while, etc.)
- for each loop: for index, booking := range bookings { // code }
- range: iterates over elements for different data structures (not only arrays and slices), yet for slices & arrays range returns the index and value for each element
- curly braces: access all indices and booking elements
- string.Fields(): splits strings on white space, returns a slice with the split elements
- range: always returns idx + value, hence use _ to ignore idx
- For loops can also have conditions and chained conditions
- Syntax: 'remainingTickets > 0 && len(bookings) <50 :'

## If/Else

- Syntax: if condition {} else {}
- Break statement: breaks the infinity look if the condition is met
- Continue statement: jumps to the next loop if the condition is met
- Multiple conditions are being validated with: if, else if*n, else

## Logical Operators

- == logical EQUALS
- && logical AND
- || logical OR
- != logical NOT

## Switch Statements

- Syntax
    city := "London"

    switch city {
        case "New York": // execute code
        case "Singapore": // execute code
        case "Amsterdam": // execute code
        case "London": // execute code
        default: // executes if no case was met in switch statement
    }

- Cases can be consolidate with
    city := "London"

        switch city {
            case "New York": // execute code
            case "Singapore", "Berlin": // execute code
            case "London", "Amsterdam": // execute code
            default: // executes if no case was met in switch statement
        }

## Functions

Syntax: func printFirstNames(bookings []string) []string {

- func: declaring a function
- printFirstNames: being the function name
- bookings: being the input value that needs to be a string slice
- and []string: being the return value that also needs to be a string slice

Sytnax for multiple return values: func validateUserInput(firstName string, lastName string, email string, userTickets uint, remainingTickets uint) (bool, bool, bool) {

- with the func declaration
- the function name
- the input values and their type in brackets
- the types of the return values in brackets as it is multiple values

## Package level variables

All variables that are defined on a package level (outside of functions) can be accessed within any function so they do not need to be explicitely passed around. However, they can only be instantiated with the right type.
Best practice: Define variable as 'local' as possible.

- doesn't work on package level: city := "London"
- does work on package level: var pauli_age int = 30

## Packages in Go

Step 0: In go.mod file: define module name, e.g. booking.
Step 1: Import target package (helper) to main package.
Step 2: Move helper.go file into helper folder.
Step 3: Exporting function in helper.go by capitalizing the function.

Relative imports happen with the defined module name and then the .go file.

You can also export variables by capitalizing them.
If imports fail try: Update the go tools - ctrl + shift + p or cmd + shift + p and update/install go tools.

## Scope Rules of Variables

- Local: in functions or only in a for loop
- Package: variables that are available in same file outside of functions
- Gobal: capitalized variable name

## Maps

- Go Version of Python Dictionary
- Syntax of creating an empty map: var userData = make(map[string]string)
  - make: creates the map
  - string is the input
  - string is the output
- We cannot mix datatypes in a map
- Syntax of creating an empty list of maps: var bookings = make([]map[string]string, 0)
  - with an intialized size of zero that automatically expands

## Struct(ures)

- for different data types like dates, bools or list of strings (array or slice) or a map
- key value pairs with mixed data types
- Syntax: type UserData struct {
    firstName string
    lastName string
    email string
    numberOfTickets uint
    }
- type: creates a new type with the name you specify, i.e. UserData type
- defines a structure (which fields a UserData Type should have)
- is like a class

## Goroutines / Concurrency

Done with keyword "go" that abstracts threading, cleanup and everything else away.

Application is being blocked while email is 'being generated', i.e. it is sleeping. This should be parallized with a Goroutine.

Until integrating concurrency everything ran in a single thread (line per line execution, so if one needs 10s, then the whole thread is blocked).

If we know that something takes longer, we start a separate thread for it "breakout of main thread" and immediately continues.

'While ticket is being generated, a new booking can be handled without any interruption."

20 users would create 20 threads, but the whole application flow would still work.

Just by writing go in front of the long processing function.

## Synchronizing Concurrency

By default: Main thread does not wait for additional threads to complete.
Tell main thread it needs to wait: by generating a wait group.
Waits for the launched goroutine to finish which comes from 'sync' package.

Waitgroup has add, wait, and done as functions to be integrated.

1. Step: Import waitgroup
2. Step: wg.Add(n) threads that main thread should wait for; with n being the number of goroutines (in the booking example this is 1)
3. Step: Add wg.Wait() to last line of code block so it is waited for the goroutine to finish.
4. Step: Add wg.Done() to func that is the goroutine to inform the main thread that the goroutine is finished.

Differences of Golang to other languages:

- More overhead for concurrency configuration.
- Really cheap in Golang.
- Go spins of "Green threads" managed by the go runtime in comparison to run on the OS threading system.
