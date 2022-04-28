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
    <td>font_rom</td>
    <td>font_rom</td>
    <td>font_rom</td>
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

### Target board : Libertron ZYNQ Starter Kit
![image](https://user-images.githubusercontent.com/80473250/165802459-fc9b9679-4769-4b79-ba48-462de958ab81.png)
### Playing Video
![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/80473250/165800417-dba2f1d4-a024-4c5b-b966-d1bd704d012a.gif)


