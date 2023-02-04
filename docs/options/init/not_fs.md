
### wgrib2: -not\_fs



### Introduction



The -not option and the -not\_fs option 
are very similar. The -not\_fs is a not
-match\_fs. The difference between
-not and -not\_fs is the the former
uses (extended) regular expressions and the latter uses "Fixed Strings" (fs).


```


    wgrib2 -not_fs X (...)

is the same as 

    wgrib2 -match_inv file | fgrep -v X | wgrib2 -i (...)

    wgrib2 -match_fs X  -not_fs Y (...)

is the same as 

    wgrib2 -match_inv file | fgrep X | fgrep -v Y | wgrib2 -i (...)

where X, and Y are strings. Note, X and Y will not match 
the second (byte location) field of the short inventory.


```

### Usage




```

-not_fs X

X is string

```



The -match, and -not selection
facility is more limited than the "wgrib2 | filter | wgrib2 -i" syntax.
However, it can be more efficient especially when combined with the 
-end option.

### Future Changes



The format of the "match inventory" has evolved and will continue to evolve.
The rule for future changes is that new items in the "match inventory" will be added
as the second last item. Consequently the last item in the inventory will always
be ":vt=YYYYMMDDHH:". In order to future proof your
-match, and -not selections, you
must not include any item before the ":vt=YYYYMMDD:" field.


```

    -match ":vt=2011111500:"                  good
    -not ":vt=2011111500:$"                   good (dollar sign matches the end of the line)
    -not ":n=10:vt=2011111500:"               bad (item before :vt=)
    -match ":RH:975 mb:anl::vt=2010050806:"   bad (item before :vt=)

```


Some recent changes (as of Nov 2011) to the match inventory include:

* adding the "extended name of the variable", ex. TMP.prob\_<273
* adding the inventory number, ex. n=10
* adding ensemble/chemical/probability information (-misc)



See also:
 [-not](./not.html), 
 [-not\_if](./not_if.html), 
[-match](./match.html), 
[-match\_inv](./match_inv.html), 
[-end](./end.html), 
[-i](./i.html),
[-if](./if.html),
[-set\_regex](./set_regex.html).












----

>Description: init  X      process data that does not match X (fixed string)

_Docs derived from <https://www.cpc.ncep.noaa.gov/products/wesley/wgrib2/not_fs.html>_