
### wgrib2: -set\_int



### Introduction



The -set\_int option sets 4 octets to an
signed integer value as commonly use by grib for signed integers.
The integer must range from -2147483647 to 2147483647,


```

-set_int I J K
  I = 1..7
  J = 1..(section length-3)
  K = -(2**23-1) .. (2**23-1)
would set 
  Section I, Octet J+0:  if (K >= 0) (K >> 24) & 255
  Section I, Octet J+0:  if (K < 0) ((abs(K) >> 24) && 255) | 128
  Section I, Octet J+1:  (abs(K) >> 16) & 255
  Section I, Octet J+2:  (abs(K) >> 8) & 255
  Section I, Octet J+3:   abs(K) & 255;
 The above is using C syntax.

```


Multiple integers can be set by making the third argument a colon seperated list.

### Usage




```

-set_int  SECTION STARTING_OCTET_LOCATION I-1:I-2:..:I-N
SECTION=0 .. 7
OCTET_LOCATION = 1..N
I-M = Mth integer

```

### Example



See also: 
[-get\_int](get_int.html)
[-set\_byte](set_byte.html)
[-set\_hex](set_hex.html)
[-set\_ieee](set_ieee.html)
[-set\_int2](set_int2.html)










----

>Description: misc  X Y Z  set 4-byte ints in Section X, Octet Y, signed integers Z (a|a:b:c)

_Docs derived from <https://www.cpc.ncep.noaa.gov/products/wesley/wgrib2/set_int.html>_