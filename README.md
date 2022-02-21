For a blog post in Hashnode where I give a couple examples of easy projects so that devs can see the difference between their current favorite language and Golang. It's also a quick and fun test for myself and could be for others as well.

---

# What I wanted to do
Create the popular "Fizzbuzz" game with Golang. Got the idea from a Tom Scott [video](https://youtu.be/QPZ0pIK_wsc) where he does this with JavaScript. My version is different so that I'm not merely copying his answer (that's no fun, also it's a completely different language).
>TODO:
>- print a list of numbers from 1 to 100
>- any answer that's divisible by 3 is replaced by the string "Fizz"
>- any answer that's divisible by 5 is replaced by the string "Buzz"
>- any answer that's divisible by 3 and 5 is replaced by the string "FizzBuzz"

# My Process
What I tried first was:
```go 
func main() {
    for i := 1; i <= 100; i++ {
        if i%3 == 0 {
            fmt.Println("Fizz")
        }
        if i%5 == 0 {
            fmt.Println("Buzz")
        }
        if i%15 == 0 {
            fmt.Println("FizzBuzz")
        } else {
            fmt.Println(i)
        }
    }
}
```
My thought was to create a for loop with if statements that would return "Fizz" with i module (%) 3, "Buzz" with i module 5, and "FizzBuzz" with i module 15. I chose 15 for "FizzBuzz" because it's the smallest number that's divisible by 3 and 5.

The result:
```
1
2
Fizz
3
4
Buzz
5
Fizz
6
...
13
14
Fizz
Buzz
FizzBuzz
16
17
Fizz
18
...
```
Well that wasn't expected. It was printing the strings as well as 3 and 5 afterwards, not replacing them like it's supposed to. It worked with 15, however, it was also printing the strings associated with 3 and 5. Then I realized "Oh wait I'm a dummy! 5 and 15 need to be 'else if' instead of 'if'".
```go 
func main() {
    for i := 1; i <= 100; i++ {
        if i%3 == 0 {
            fmt.Println("Fizz")
        } else if i%5 == 0 {
            fmt.Println("Buzz")
        } else if i%15 == 0 {
            fmt.Println("FizzBuzz")
        } else {
            fmt.Println(i)
        }
    }
}
```
The result:
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
Fizz
16
17
...
```
Close, but "FizzBuzz" isn't printing at 15, instead it's "Fizz". That's because the computer is taking the instructions line by line. I have `i%3 == 0 ` before `i%15 == 0` so i module 3 is going to take preeminence over i module 15. All I have to do is move `i%15 == 0` ahead of the other 2. Finally, after refactoring, I got the correct result.

# Correct Answer
``` go
func main() {
	for i := 1; i <= 100; i++ {
		if i%15 == 0 {
			fmt.Println("FizzBuzz")
		} else if i%3 == 0 {
			fmt.Println("Fizz")
		} else if i%5 == 0 {
			fmt.Println("Buzz")
		} else {
			fmt.Println(i)
		}
	}
}
```

```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
```