# Verilog-bouncing-ball-Game
The bouncing ball game described in Verilog HDL. The top.mod outputs RGB values of the corresponding coordinates to the monitor, and **the design related to the actual game behavior is done in grahp.mod.**

<table style="margin-left: auto; margin-right: auto;">
  <tr>
    <td colspan="7">TOP.mod</td>
  </tr>
  <tr>
    <td rowspan="2">clk_wiz_0</td>
    <td rowspan="2">clk_divier</td>
    <td rowspan="2">keypad.mod</td>
    <td rowspan="2">debounce.mod</td>
    <td colspan="2">graph_mod</td>
    <td rowspan="2">sync_mod</td>
  </tr>
  <tr>
    <td>font_rom</td>
    <td>reach_floor</td>
  </tr>
</table>

<table style="margin-left: auto; margin-right: auto;">
  <tr>
    <td>구분</td>
    <td>기능</td>
    <td>설계 아이디어</td>
  </tr>
  <tr>
    <td rowspan="3">설계 요소</td>
    <td>물리적 현상을 그대로 적용</td>
    <td>1)ball_y_reg가 2)ball_vy_reg에 의해 변화량이 증감하고, ball_vy_reg 또한 3)BALL_A에 의해 클록에 따라 변화하도록 설계</td>
  </tr>
  <tr>
    <td>공이 땅에 닿았을 때를 인식</td>
    <td>4)ball_x_reg가 bar의 x축 길이 안에 위치하고, ball_y_reg가 bar의 y축 윗면 위에 위치할 때, 5)ball_y_b가 6)bar_y_t 보다 커졌을 때, ‘reach’ 신호를 주어 반대 방향으로 속도 부여</td>
  </tr>
  <tr>
    <td>공중에 위치한 바를 식별</td>
    <td>위 reach 신호에 대한 회로를 모듈로 만들어, bar에 대한 x_reg, y_reg, 길이와 폭, 현재 공의 위치 등 필요한 데이터를 input으로 받아 공이 bar에 닿았는지를 graph 모듈에 instance.</td>
  </tr>
</table>

1 ) ball_y_reg : 공의 수직 좌표
2 ) ball_vy_reg : 공의 수직 속도
3 ) BALL_A : 수직 아래 방향 const 한 가속도

4 ) ball_x_reg : 공의 수평 좌표
5 ) ball_y_b : 공의 바닥 면 좌표
6 ) bar_y_t : bar의 윗면 좌표

### This game follows the following flow chart
![image](https://user-images.githubusercontent.com/80473250/166265171-77e942e9-9fc7-459b-8032-9d1d8e001f3c.png)

1 ) 공의 수직 좌표 운동은 단위 시간에 대해 준 식으로 표현 가능하며, 이때 속도도 "*"로 서술한다.

![image](https://user-images.githubusercontent.com/80473250/166266876-0307129f-9678-417b-bb95-a572920c8aa5.png)

_**따라서 ball_y_reg = ball_y_reg + ball_vy_reg 이며, ball_vy_reg = ball_vy_reg + BALL_A 다.**_

2 ) 키 패드를 눌렀을 때 if(key_pad == ***)으로 식별하여 수평 좌표를 제어하며, ball_x_reg = ball_x_reg + BALL_V 이다.

3 ) 공의 x,y 좌표가 결정되었을 때 gound 를 포함하여 bar(1~6)까지의 폭, 너비, 좌표와 공
의 위치, flag_input을 instance 한 reach_floor 모듈의 input으로 설정하여 공이 땅에 닿았는지 모니터링하여 output으로 flag_output을 출력

4 ) 공이 땅에 닿았을 때( ball_y_b >= ball_y_t ), flag_output은 ~flag_input으로 변경된다. graph_mod 모듈에서 두 flag가 같지 않을 때를 “땅에 닿았다”라고 판단하여 공을 수직 위로 발사( ball_vy_reg = -1 * 20 )한다.

5 ) 함정 bar의 경우 reach_floor에 들어가는 flag가 dead_flag_input과 dead_flag_output이며, 마찬가지로, graph_mod 모듈에서 두 flag가 같지 않을 때를 “함정에 닿았다”라고 판단하여 life를 1회 차감하고 다시 게임을 실행한다.

*위 3~5 과정은 reach_floor 모듈로 설계했으며 graph_mod 모듈에서 bar마다 instantiation
하여 설계한다.*

### Target board : Libertron ZYNQ Starter Kit
![image](https://user-images.githubusercontent.com/80473250/165802459-fc9b9679-4769-4b79-ba48-462de958ab81.png)
### Playing Video
![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/80473250/165800417-dba2f1d4-a024-4c5b-b966-d1bd704d012a.gif)


