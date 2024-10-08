# LCD_Interfacing_Uding_Verilog
module Lcd(clk, rst, data, Lcd_e, Lcd_rw, Lcd_rs, SF_CE0);
input clk,rst;
output [3:0] data;
output reg SF_CE0;
output reg Lcd_e,Lcd_rw,Lcd_rs;
reg [3:0]Lcd_cmd;
reg [5:0]state=0;
reg init_done, disp_done;
reg [19:0] count=0;
assign data=Lcd_cmd;
always@(posedge clk or posedge rst)
begin if(rst)
begin
Lcd_e<=0;
init_done<=0;
Lcd_rs<=0;
Lcd_rw<=0;
SF_CE0<=1'b1;
end
else
begin
case(state)
0:begin
Lcd_e<=0;
Lcd_rw<=0;
Lcd_rs<=0;
if(count==750000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

1:begin
Lcd_e<=1;
Lcd_cmd<=4'h3; 
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

2:begin
Lcd_e<=0;
if(count==205000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

3:begin
Lcd_e<=1;
Lcd_cmd<=4'h3;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

4:begin
Lcd_e<=0;
if(count==5000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

5:begin
Lcd_e<=1;
Lcd_cmd<=4'h3;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

6:begin
Lcd_e<=0;
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

7:begin
Lcd_e<=1;
Lcd_cmd<=4'h2;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

8: begin
Lcd_e<=0;
if(count==2000)
begin
count<=0;
state<=state+1;
init_done<=1;
end
else
count<=count+1;
end

9:begin
Lcd_e<=1;
Lcd_cmd<=4'h2;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

10:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h8;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

11:begin
if(count==12) 
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

12:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

13:begin
Lcd_e<=1;
Lcd_cmd<=4'h0;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

14:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h6;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

15:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

16:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

17:begin
Lcd_e<=1;
Lcd_cmd<=4'h0;
if(count==12) 
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

18:begin
Lcd_e<=0;
if(count==50) 
begin
Lcd_e<=1;
Lcd_cmd<=4'hc;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

19:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

20:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

21:begin
Lcd_e<=1;
Lcd_cmd<=4'h0;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

22:begin 
Lcd_e<=0; 
if(count==50)
Lcd_e<=1;
Lcd_cmd<=4'h1;
count<=0; state<=state+1; 
end

23:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

24:begin
if(count==82000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

25:begin
Lcd_e<=1;
Lcd_cmd<=4'h8;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

26:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

27:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

28:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

29:begin
Lcd_e<=1;
Lcd_rs<=1;
Lcd_cmd<=4'h4;
if(count==12) 
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

30:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h9;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

31:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

32:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

33:begin
Lcd_e<=1;
Lcd_rs<=1;
Lcd_cmd<=4'h4;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

34:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h3;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

35:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

36:begin
if(count==2000)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

37:begin
Lcd_e<=1;
Lcd_rs<=1;
Lcd_cmd<=4'h5;
if(count==12)
begin
count<=0;
state<=state+1;
end
else
count<=count+1;
end

38:begin
Lcd_e<=0;
if(count==50)
begin
Lcd_e<=1;
Lcd_cmd<=4'h4;
count<=0;
state<=state+1;
end
else
count<=count+1;
end

39:begin
if(count==12)
begin
Lcd_e<=0;
count<=0;
end
else
count<=count+1;
end
endcase
end
end
endmodule
