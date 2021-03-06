#mov 명령어 The first instruction: mov

이제서야 실습을 하게 되었습니다. 16진수, 2진수와 8086 구조에 대한 글을 보면서 하나도 모르겠다고 생각하셔도 전혀 상관없습니다. 원래 처음 뭔가를 배운다는게 내가 뭘 모르는지 모르는 상태에서 뭘 모르는지 아는 상태로 옮겨가는 거라고 합니다. 이제 "16진수, 2진수, 8086의 구조에 대해서 모르겠다"라는 것을 아신 것입니다. 그러니 진일보한 것이지요.

실습을 하면 16진수,2진수,레지스터들에 대해서 좀더 이해해보겠습니다.

일단 emu8086의 압축을 풀었던 디렉토리를 열어봅니다. emu8086.exe 파일이 보이지만 지금은 emu8086.exe가 아니라 cmdhere.cmd 파일을 실행합니다. 그러면 터미널 창이 나타납니다. 아마 터미널을 처음 보신 분들도 계실것 같습니다. 당황하지않고 notepad라고 키보드로 칩니다. 그리고 엔터를 치면 메모장이 실행될 것입니다. 메모장에 실습할 어셈블리 명령어들을 입력합니다.
Let's start the first exercise. It's ok if you do not understanding anything about hexadecimal, binary and 8086 structures discribed in privious chapters. The first thing to learn is always that you know what you do not know. Now you know that "I do not know about hexadecimal, binary, 8086 structure". So it is a step forward.

In this chapter I'll describe the mov instruction. It is the basis instruction of all 8086 instructions and very simple.

Let's run the mov instruction with the emu8086. If you have the old version of emu8086, you might have the emu8086.exe file and cmdhere.cmd file. Please run the cmdhere.cmd file. A terminal window appears. Maybe some of you have seen the terminal for the first time. Do not afraid and type notepad with keyboard. And hit enter to run Notepad. In Notepad, type the following assembly instructions.
If you have another version of the emu8086 or another emulator, it must have the same feature. Please run your emulator and run the following code.

```
mov ax, 1000
mov bx, 1000h
mov cx, 0ffffh
```


그리고 파일을 저장합니다. 이름은 상관없지만 키보드로 입력하기 편하게 mov.txt로 하겠습니다. 그리고 다시 터미널에 들어가서 emu8086.exe mov.txt 라고 입력합니다. 그럼 emu8086이 실행되면서 텍스트 편집기에 우리의 예제 소스가 나타납니다. 바로 emulate 메뉴를 실행합니다.

일부러 화면을 캡처하지 않겠습니다. 한번 해보세요. 에물레이터 화면을 보면 왼쪽에 레지스터 값이 나타나고 오른쪽에는 메모리 값과 메모리에 있는 어셈블리 명령어가 나타납니다. 우리가 입력한 mov ax, 1000이 있나요? 아마 없을 겁니다. mov bx, 1000h는 있나요? 있습니다. 무슨 차이일까요?

이전 글에서 프로세서는 2진수만 알 수 있고 어셈블리 명령에서는 2진수를 보기쉽게 만드는 16진수만을 쓴다고 말씀드렸습니다. 바로 지금 우리가 입력한 10진수가 16진수로 어셈블링되서 프로세서에 저장된 것을 볼 수 있습니다. 10진수 1000이 16진수로 3e8h입니다. 그래서 명령어 화면에 mov ax, 3e8h로 나타난 것입니다. 1000h는 16진수이므로 명령어 화면에 그대로 mov bx, 1000h로 나타납니다. 0ffffh도 마찬가지로 그대로 나타나구요.
And save the file. You can use any file name, for instance mov.txt. Then type emu8086.exe mov.txt on the terminal window. Then emu8086 runs and our sample source appears in a text editor of emu8086. Just run the emulate menu.

I will not capture the screen deliberately. Try it for yourself. It could be a little different for each version. On the emulator screen of the old version, register values ​​appear on the left, and memory values ​​and assembly instructions in memory appear on the right. Is there a "mov ax, 1000" we entered int the instruction list? Probably not. Is there "mov bx, 1000h"? There is. What's the difference?

In the previous article I mentioned that the processor only knows the binary number and that the assembly instructions only use hexadecimal numbers to make the binary numbers easier to see. Right now we can see that the decimal numbers we entered are assembled into hexadecimal and run by the processor. The decimal number 1000 is 3e8h in hexadecimal. So, the command screen shows "mov ax, 3e8h". Since 1000h is a hexadecimal number, "mov bx, 1000h" are displayed on the command screen. 0ffffh is the same.

그리고 single step 버튼을 눌러보세요. 레지스터 값이 바뀌나요? step back 버튼도 눌러보세요. 그리고 다른 버튼들도 눌러서 어떻게 실행되나 해보세요.

어셈블리 명령이 뭔지 레지스터에 어떻게 값을 쓰는지 알것 같으신가요? 이렇게 레지스터에 직접적으로 값을 쓰는 명령어가 mov입니다.

레지스터에 데이터를 써놨는데요 이번에는 다른걸 해보시기 바랍니다. 레지스터의 값을 다른 레지스터로 옮기는건 어떻게 하면 될까요?

그리고 CS, IP, SS, SP 등등 범용 레지스터가 아닌 특수한 레지스터들에 값을 한번 써보세요. 특수한 레지스터와 범용 레지스터간에 값을 옮겨보세요.
Then press the single step button. Does the register value change? Please also press the step back button. And press any other button to see how it works.

Can you feel what mov instruction does? The command to write the value directly to the register is mov.

We wrote the data in the register. Please try something else. Please find how we can move the value of a register to another register.

Also, please write the values ​​to special registers such as CS, IP, SS, SP other than general purpose registers AX, BX, CX and DX. Is it possible to move values ​​between special registers and general registers?

