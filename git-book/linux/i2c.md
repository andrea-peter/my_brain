# I2C



## How to

### Detect installed I2C busses

```
$ sudo i2cdetect -y -l
i2c-3	i2c       	3190000.i2c                     	I2C adapter
i2c-10	i2c       	i2c-2-mux (chan_id 1)           	I2C adapter
i2c-1	i2c       	c240000.i2c                     	I2C adapter
i2c-8	i2c       	31e0000.i2c                     	I2C adapter
i2c-6	i2c       	31c0000.i2c                     	I2C adapter
i2c-4	i2c       	Tegra BPMP I2C adapter          	I2C adapter
i2c-2	i2c       	3180000.i2c                     	I2C adapter
i2c-0	i2c       	3160000.i2c                     	I2C adapter
i2c-9	i2c       	i2c-2-mux (chan_id 0)           	I2C adapter
i2c-7	i2c       	c250000.i2c                     	I2C adapter
i2c-5	i2c       	31b0000.i2c                     	I2C adapter

```

### Detect devices on a bus

```
$ sudo i2cdetect -y -rF 4
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- UU -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --                         

```

* "--"
