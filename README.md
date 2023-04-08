# Slow_clk_generation

To create clk_slow of 1000Hz     System clk=100MHz


Number of clk cycles or count value =
```math
\frac{1}{2} * \frac{100MHz}{1000Hz}= 50,000 
```


```
   50_000
       /|     /|
      / |    / |
     /  |   /  |
    /   |  /   |
   /    | /    |
 0/     |/     |
 
_        ______
 |      |      |
 |      |      |
 |______|      |______
 <-(1/1000)Sec->
 <------> 
 (1/2)*(1/1000)
```
## Method-1
```
module slow_clk #(parameter COUNT_MAX=30)(
    input clk, rst,
    output reg clk_slow
    );
    
    reg [10:0] count; //Count value storing reg.
    
    always @(posedge clk or posedge rst) begin
        
        //1st priority rst signal
        if (rst) begin count<= 0; clk_slow<=0; end
        
        //clk_slow transition
        else if(count==(COUNT_MAX-1)) begin count<=0; clk_slow = ~clk_slow; end
        
        //increase count value
        else count = count +1;
    end
endmodule
```
