#배열 Array

배열은 연속된 변수들로 볼 수 있습니다. 연속되었다는 말은 메모리상에서의 위치가 연속적으로 자리를 잡고 있다는 뜻입니다. 1000h 번지에 위치는 8비트 변수가 있고 1001h에도 있고 1002h에도 있다면 이 3개의 변수를 합쳐서 하나의 배열로 만드는 것이지요. 배열이란 변수들 여러개를 붙여놓은 것입니다.
예를 들어 문자열은 바이트 배열입니다. 각각의 바이트는 출력하려는 문자의 ASCII 코드값을 나타냅니다. 1바이트 문자라는 변수들을 여러개 붙여놓은 것이지요.
 
여기 배열을 선언하는 예를 보겠습니다.

Arrays can be viewed as contiguous variables. Continuous means that all variables are stored in contiguous memory. If you have an 8-bit variables at location 1000h, 1001h and 1002h, you can combine these three variables into a single array. An array is defined as a set of variables. For example, a string is a array of byte size variables. Each byte represents one ASCII code value of the character. It is a set of single-byte variables.

Here is an example of declaring an array.

```
a DB 48h, 65h, 6Ch, 6Ch, 6Fh, 00h
b DB 'Hello', 0 
```
 
b 는 a배열과 정확히 같습니다. 컴파일러는 따옴표안에 있는 문자열을 바이트의 집합으로 변경합니다. 아래 차트는 이 배열이 선언되었을 때 메모리를 보여줍니다. 문자열의 마지막은 문자가 아니라 0이라는 것에 주의하세요. 0은 문자열이 끝났다는 것을 말해줍니다. 0이 없다면 문자열을 읽다가 문자열이 언제 끝나는지 알수가 없으니까요.

Array b is exactly the same as an array a. The compiler changes the string in quotes to a set of bytes. The picture below shows memory when this array is declared. Note that the end of the string is 0, not a character. A value of 0 indicates that the string is finished. If you do not have a zero, you do not know where the string ends.

![](/assets/array.gif)
 
배열의 원소는 []를 사용하여 접근할 수 있습니다. 예를 들면:
 
```
MOV AL, a[3] 
```

이렇게 실행하면 al에는 6ch 값이 저장됩니다.
 
또는 메모리 인덱스 레지스터(BX, SI, DI, BP)를 사용할 수도 있습니다.
``` 
MOV SI, 3
MOV AL, a[SI]
```
큰 배열을 선언할 때, DUP 연산자를 사용할 수 있습니다. DUP의 문법은 다음과 같습니다. 
``` 
숫자 DUP ( 값(s) )
숫자 - 복사할 횟수 (상수값이어야 함).
값 - 복사할 데이터 

Number DUP ( value(s) )
Number: The number of copy (should be constant)
value: data to copy
```

예를 들어 
For example,

``` 
c DB 5 DUP(9)
```

는 다음과 같습니다. 

above is the same to following.

``` 
c DB 9, 9, 9, 9, 9
``` 
 
예를 하나 더 들면 

For one more example

``` 
d DB 5 DUP(1, 2)
``` 
는 다음과 같습니다. 

above is the same to following.

``` 
d DB 1, 2, 1, 2, 1, 2, 1, 2, 1, 2
``` 
 
물론, 255보다 크거나 -128보다 작은 값이 필요한 경우, DB 대신 DW를 사용할 수 있습니다. DW는 문자열을 선언할 때는 사용할 수 없습니다. 
문자열과 메모리 접근을 배웠으니 스크린에 hello, world를 출력하는 예제를 한번 만들어보세요.

Of course, if you need a value that is larger than 255 or less than -128, you can use DW rather than DB.
DW cannot declare character string.
Now you've learned how to use a string and memory addressing.
Please make a program to print "hello, world" on screen.