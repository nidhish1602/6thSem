### Spark

1. Scala program to print your name
```ruby
scala> object ExPrintName {
     |        def main(args: Array[String]) {
     |            println("My name is miyuki!")
     |        }
     |     }
defined object ExPrintName

scala> ExPrintName.main(Array())
My name is miyuki!
```
2. Scala program to find largest number among two numbers
```ruby
scala>     object ExFindLargest {
     |        def main(args: Array[String]) {
     |           var number1=20;
     |           var number2=30;
     |           var x = 10;
     | 
     |           if( number1>number2){
     |              println("Largest number is:" + number1);
     |           }
     |           else{
     |               println("Largest number is:" + number2);
     |           }
     |        }
     |     }
defined object ExFindLargest

scala> ExFindLargest.main(Array())
Largest number is:30
```
3. Scala program to find a number is positive, negative or positive
```ruby
scala>     object ExCheckNumber {
     |        def main(args: Array[String]) {
     |         
     |             /**declare a variable*/
     |             var number= (-100);
     |        
     |            if(number==0){
     |                println("number is zero");
     |            }
     |            else if(number>0){
     |                println("number is positive");
     |            }
     |            else{
     |                println("number is negative");
     |            }
     |        }
     |     }
defined object ExCheckNumber

scala> ExCheckNumber.main(Array())
number is negative
```
4. Scala program to declare string variable and print the string
```ruby
scala> object ExampleString {
     |    def main(args: Array[String]) {
     |         
     |         //declare and assign string variable "text"
     |         val text : String = "You are reading SCALA programming language.";
     |         
     |         //print the value of string variable "text"
     |         
     |         println("Value of text is: " + text);
     |         
     |    }
     | }
defined object ExampleString

scala> ExampleString.main(Array())
Value of text is: You are reading SCALA programming language.
```
5. Scala program to demonstrate example of multiple variables declarations and assignments
```ruby
scala> object ExampleVarDecAndAssin {
     |    def main(args: Array[String]) {
     |       
     |       var (name: String, age: Int) = Pair("Mike",21);
     | 
     |       //print values
     |       println("Name:   "+name);
     |       println("Age:    "+age);
     |       
     |       //declaration without specifying data type
     |       var (address,mobile)=Pair("New Delhi, India",1234567890);
     |       
     |       //print values
     |       println("Address:   "+address);
     |       println("Mobile:    "+mobile);      
     |             
     |    }
     | }
warning: there were two deprecation warnings (since 2.11.0); for details, enable `:setting -deprecation' or `:replay -deprecation'
defined object ExampleVarDecAndAssin

scala> ExampleVarDecAndAssin.main(Array())
Name:   Mike
Age:    21
Address:   New Delhi, India
Mobile:    1234567890
```
6. Scala program to print numbers from 1 to 100 using for loop
```ruby
scala> object ExampleForLoop1 {
     |    def main(args: Array[String]) {
     |       var counter: Int=0;
     |       
     |       for(counter <- 1 to 100)
     |         print(counter + " ");
     |     
     |       // to print new line
     |       println();
     |    }
     | }
defined object ExampleForLoop1

scala> ExampleForLoop1.main(Array())
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 
51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 
```
7. Scala program to print numbers from 1 to 100 using for loop with until to determine loop range
```ruby
scala> object ExampleForLoop2 {
     |    def main(args: Array[String]) {
     |       var counter: Int=0;
     |       
     |       for(counter <- 1 until 101)
     |         print(counter + " ");
     |     
     |       // to print new line
     |       println();
     |    }
     | }
defined object ExampleForLoop2

scala> ExampleForLoop2.main(Array())
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 
51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100
```
8. Scala program to demonstrate example of collection list and for loop
```ruby
scala> object ExampleForAndCollection {
     |    def main(args: Array[String]) {
     |       //declare an integer
     |       var N: Int=0;
     |       
     |       //declare integer list
     |       var numbers = List(100,200,300,400);
     |       
     |       //to print all numbers using for loop
     |       for(N<-numbers){
     |           println(N);
     |       }
     |       
     |    }
     | }
defined object ExampleForAndCollection

scala> ExampleForAndCollection.main(Array())
100
200
300
400
```
9. Scala program to create a user define function to return largest number among two numbers
```ruby
scala> object ExampleUDFToGetLargestNumber {
     |     //function definition
     |     def getLargestNumber(x: Int, y: Int) : Int ={
     |         var largestNumber: Int=0;
     |         if(x>y)
     |             largestNumber=x;
     |         else
     |             largestNumber=y;
     |         
     |         return largestNumber;
     |     }
     |     
     |     def main(args: Array[String]) {
     |         var a: Int=10;
     |         var b: Int=20;
     |         
     |         //function calling
     |         println("Largest number from "+ a+" and "+ b +" is: "+ getLargestNumber(a,b));
     |         
     |     }
     | }
defined object ExampleUDFToGetLargestNumber

scala> ExampleUDFToGetLargestNumber.main(Array())
Largest number from 10 and 20 is: 20
```
10. Scala program of array - Declare, print and calculate sum of all elements
```ruby
scala> object ExampleArray1 {
     |     
     |    def main(args: Array[String]) {
     |        
     |       var numbers = Array(10,20,30,40,50);
     |       var N:Int=0;
     |       
     |       //print all array elements
     |       println("All array elements: ");
     |       for ( N <- numbers ) {
     |          println(N);
     |       }
     |       //calculating SUM of all elements
     |       var sum: Int=0;
     |       for ( N <- numbers ) {
     |          sum+=N;
     |       }      
     |       println("Sum of all array elements: "+sum);
     | 
     |    }
     | }
defined object ExampleArray1

scala> ExampleArray1.main(Array())
All array elements: 
10
20
30
40
50
Sum of all array elements: 150
```

