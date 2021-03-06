#메모리 주소 표현 방법들

이전 글에서 ds:[bx]라는 가장 간단한 메모리 주소 표현 방법을 보았습니다. 이번에는 그 외에 어떤 방법들이 있는지를 보겠습니다.

다음 테이블이 바로 메모리 주소의 모든 표현 방식을 모아놓은 것입니다.
In the previous article, we have seen how to represent the simplest memory address ``ds:[bx]``. This article, let's see what else.

The following table is a collection of all representations of memory address.

```
[BX + SI]
[BX + DI]
[BP + SI]
[BP + DI]	
[SI]
[DI]
d16 (offset of a variable)
[BX]	
[BX + SI + d8]
[BX + DI + d8]
[BP + SI + d8]
[BP + DI + d8]
[SI + d8]
[DI + d8]
[BP + d8]
[BX + d8]	
[BX + SI + d16]
[BX + DI + d16] 
[BP + SI + d16]
[BP + DI + d16]	
[SI + d16]
[DI + d16]
[BP + d16]
[BX + d16]
```

d8은 8비트의 숫자를 말하고 d16은 16비트의 숫자를 말합니다.

가만히 보면 첫번째에 나오는 레지스터가 bx, bp이고 그 다음이 si,di 이고 그 다음이 숫자라는 규칙이 있는걸 알 수 있습니다. bx, bp의 이름이 베이스 레지스터, 베이스 포인터 레지스터라는 것을 보면 bx, bp는 항상 기본 주소를 나타낸다는 것을 알 수 있습니다. 또 si, di의 이름이 소스 인덱스 레지스터, 목적destination 인덱스 레지스터라는 것을 보면 베이스 주소에 더하는 인덱스라는 것이 생각납니다. C언어 하시는 분들은 뭔가 생각나는거 없으세요? 힌트는 배열입니다. (주1)

실습 코드를 보겠습니다.

d8 refers to an 8-bit number, and d16 refers to a 16-bit number.

If you look at it carefully, you can see a sequence of the registers. The first register is bx, bp, then si, di and then the number. The full names of bx, bp are "base register" and "base pointer register", so bx, bp always indicate base address. Also, we know that the names of si and di are the "source index register" and the "destination destination index register", so we can think they has the index added to the base address. If you know C language, you might think of something similar. Yes, those are representations of the array. (Note 1)

Let's take an example code.

```
org 100h
mov ax, 0b800h
mov ds, ax
mov bx, 0
mov cl, 'A'
mov ch, 11011111b
mov ds:[bx], cx
mov [bx+2], cx
mov si, 4
mov [bx+si], cx
mov [bx+si+2], cx
ret
```

일단 실행하기 전에 코드를 보면서 A라는 글자가 화면에 몇번 나올지 생각해보세요. 메모리에 데이터를 쓰는 명령이 몇개 있나요? 4개입니다. [] 표시가 있는 명령어만 보면 되니까요.

그럼 메모리 주소가 각각 몇번지가 될까요?

첫번째로 메모리에 쓰는 명령어는 mov ds:[bx], cx입니다. 이때 ds값은 0b800h이고 bx 값은 0입니다. 세그먼트 주소 * 10h + 레지스터 값이 주소값이므로 0b8000h + 0h = 0b8000h 값이 주소 값입니다. 0b8000h 위치의 메모리에 'A'라는 값을 쓴 것입니다.

그 다음 명령어는 [bx+2]입니다. 세그먼트 ds 값은 0b800h이고 레지스터 값 bx에 2가 더해졌으니 0b8000h + 0 + 2 = 0b8002h 가 주소 값이 됩니다. 앞에서 쓴 메모리 주소보다 2가 더해졌지요?
Before you run it, think about how many times you will see the letter A on the screen while watching the code. How many instructions do you write to memory? There are four because there are four commands with [].

So how many memory addresses are there?

The first command to write to memory is ``mov ds:[bx], cx``. The ds value is 0b800h and the bx value is 0. "Segment address * 10h + register value" is the address value, so 0b8000h + 0h = 0b8000h is the address value. 'A' is written to memory at the address of 0b8000h.

The next address expression is ``[bx + 2]``. The segment ds value is 0b800h and 2 is added to the register value bx, so 0b8000h + 0 + 2 = 0b8002h becomes the address value. It adds 2 to the privious memory address.


그 다음은 bx+si인데 si에는 4라는 값이 있습니다. 그래서 0b8000h + 0 + 4 = 0b8004h이 메모리 주소가 됩니다. 그 다음은 bx+si+2 이므로 계산할 필요도 없이 0b8006h가 되겠지요.

한번 실행해보세요. 핑크색 A가 몇개 나왔나요?

핑크색 A들이 서로 붙어있나요 아니면 떨어져있나요?

예제에 없는 다른 형태들을 사용해서 한줄을 A로 채워보세요. 그리고 그 다음줄로 넘어가 보세요. 메모리 주소에 계속 2를 더하면 한줄 한줄 채울 수 있습니다. 색깔도 바꿔보고 글자도 다른 글자로 바꿔보세요. 색깔을 지정하는 11011111b 값을 아무 값으로나 바꿔서 해보세요.

잘된다면 이번엔 안되는걸 해보세요. d8 위치에 16비트 값을 넣어보세요. 레지스터 2개를 이용하는 [bx + si] 형태말고 [ax + bx + cx] 같이 3개의 레지스터를 써보세요. 테이블을 보면 항상 첫번째 레지스터가 bx, bp, si, di 레지스터인데 ax나 cx같이 다른 레지스터를 써보세요. 어떻게 되나요?

The next expression is ``bx + si``, where si valus is 4. So the address is 0b8000h + 0 + 4 = 0b8004h. The next one is ``bx + si + 2``, so it will be 0b8006h.

Run the code now. How many pink A's are there?

Are the pink A sticking together or apart?

Try making a line of A with other forms not in the example. And then move on to the next line. If you continue to add 2 to the memory address, you can fill one line. Change the color and change the letters into different letters. You can change the color with changing the value of 11011111b to any value.

If it works well, try wrong expression. Try placing a 16-bit value in d8. Write other three registers like ```[ax + bx + cx]``` instead of [bx + si] using two registers. In the table, the first register is always bx, bp, si, and di, but try another register like ax or cx. What happens?
---
주1: 베이스 주소 + 인덱스 주소라는걸 보면 포인터 연산이 생각나야 합니다. 안그러면 C언어 개발자라고 하기에 부끄러운 겁니다. 진짜에요. 저도 포인터 연산을 생각못해서 절 가르쳐준 선배님에게 혼난 기억이 있거든요. *(p + 1), *(p + 3) 이런걸 생각해보세요. C언어가 왜 어셈블리 언어를 계승하는 언어인지 아시겠지요?

Note1: If you're C language programmer, you must realize immediately that the expressions are same to pointer operations. Think about ``*(p + 1)`` or ``*(pp + 3) + 4 when p is a pointer and pp is a doube pointer. Please note that the C language is origianally designed for assembly programmer.

