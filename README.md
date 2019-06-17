# FPGALock
## 背景

本学期的数字逻辑期末大作业的选择之一：在EGO1开发板上实现电子密码锁

## 平台
Vivado 2018.3

## 工作原理

密码锁初始位于上锁状态，前四位七段数码管显示“0000”，后四位七段数码管显示“LoAd”表示正在工作，内置 4 位密码 1000。
  
启动后自动进入开锁状态，前四位七段数码管显示用户输入，通过上下按钮增加或减少当前位的用户输入密码的值，左右按钮更改当前位，当前位的显示数字闪烁。按动中间按钮确定密码，进行开锁尝试。下方流水灯亮灭状态表示当前倒计时。
  
进入开锁状态后，输入限时（5s）启动，若在限时内未能成功开锁，报警装置工作报警，后四位七段数码管显示“FAIL”表示失败，进入上锁状态。
  
成功开锁后，后四位七段数码管显示“Good”表示成功。
  
用户可以拨动下方开关进入修改密码模式，输入四位密码，按动中间按钮确定密码。
  
reset按钮将重置密码锁，密码变为初始密码，密码锁状态回到初始状态。

## 管脚定义表

端口名称 | 输入输出方向 | 管脚号
:-: | :-: | :-:
sys_clk |	input |	P17
rst_n |	input |	P15
up_button |	input |	U4
down_button |	input |	R17
left_button |	input |	V1
right_button | input |	R11
middle_button |	input |	R15
mode | input |	P5
ledlow | output |	F6
ledbit[0]	| output |	G6
ledbit[1]	| output | E1
ledbit[2] | output | F1
ledbit[3] |	output |	G1
ledbit[4] |	output |	H1
ledbit[5] |	output |	C1
ledbit[6] |	output |	C2
ledbit[7] |	output |	G2
ledshow[0] |	output |	B1
ledshow[1] |	output |	A3
ledshow[2] |	output |	A1
ledshow[3] |	output |	B2
ledshow[4] |	output |	A4
ledshow[5] |	output |	B3
ledshow[6] |	output |	B4
ledshow2[0] |	output |	F4
ledshow2[1]	| output |	D3
ledshow2[2]	| output |	F3
ledshow2[3]	| output |	D2
ledshow2[4]	| output |	E3
ledshow2[5]	| output |	E2
ledshow2[6]	| output |	D4
leddown[0]	| output |	K3
leddown[1]	| output |	M1
leddown[2]	| output |	L1
leddown[3]	| output |	K6
leddown[4]	| output |	J5
leddown[5]	| output |	H5
leddown[6]	| output |	H6
leddown[7]	| output |	K1

## 模块说明
### digital_put

管脚|	类型|	位宽|	功能
:-:|:-:|:-:|:-:
number1[3:0]|	input|	4|	前四位数码管数字信息
number2[3:0]|	input|	4|	后四位数码管数字信息
numbit[7:0]|	input|	8|	数字显示位信息
ledbit[7:0]|	output|	8|	数码管显示位信息
ledshow[6:0]|	output|	7|	前四位数码管每段信息
ledshow2[6:0]|	output|	7|	后四位数码管每段信息

### clock_make
管脚|	类型|	位宽|	功能
:-:|:-:|:-:|:-:
sys_clk|	input	|1|	总时钟
rst_n|	input	|1|	重置清零信号
left_button|	input|	1|	左键选中情况
right_button|	input|	1|	右键选中情况
up_button|	input|	1|	上键选中情况
down_button|	input|	1|	下键选中情况
middle_button|	input|	1|	中键选中情况
lock_status|	input|	1|	是否为锁住状态
read_status|	input|	1|	是否为检验密码状态
load_status|	input|	1|	是否为修改密码状态
is_jmp[7:0]|	input|	8|	当前选中位（实现闪烁）

## 开源许可
本工程由Init_new_world(Initialize)独立开发完成，请遵循GPL V3开源许可证。
