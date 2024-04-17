instrument { name = "MG Shark 8xTrade V2", short_name = "SMA", overlay = true }

period1 = input (3, "Period 1", input.integer)

period2 = input (5, "Period 2", input.integer)

ma1=sma(close,period1)
ma2=sma(close,period2)


input_group {
   "Line 1",
   color1 = input { default = "green", type = input.color },
   width1 = input { default = 1, type = input.line_width}
}

input_group {
   "Line2",
   color2 = input { default = "red", type = input.color },
   width2 = input { default = 1, type = input.line_width}
}


plot (ma1, "EMA 1", color1, width1)

plot (ma2, "EMA 2", color2, width2)

sizeprev=max(close[1],open[1])-min(close[1],open[1])
sizeprev=sizeprev/2

cursize=max(close,open)-min(close,open)
buycond=ma1>ma2 and ma1[1]<ma2[1] and cursize<sizeprev and close>ma1 and close>ma2 and close[1]>ma1[1] and close[1]>ma2[1] and max(close[1],open[1])>ma1[1] and max(close[1],open[1])>ma2[1] and min(close[1],open[1])<ma1[1] and min(close[1],open[1])<ma2[1]
sellcond=ma1<ma2 and ma1[1]>ma2[1] and  cursize<sizeprev and close<ma1 and close<ma2 and close[1]<ma1[1] and close[1]<ma2[1] and max(close[1],open[1])>ma1[1] and max(close[1],open[1])>ma2[1] and min(close[1],open[1])<ma1[1] and min(close[1],open[1])<ma2[1]


plot_shape(
(buycond),
"",
shape_style.triangleup,
shape_size.huge,
"green",
shape_location.belowbar,0,
"MG Shark 8x Buy",
"green"
)



plot_shape(
(sellcond),
