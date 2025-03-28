### Asynchronous Low-code compiler for python
[github](https://github.com/play-go/xfox-code)

# How to install

```bash
pip install xfox
```

## Optional

```bash
pip install termcolor
```

# Example

```python
import asyncio
import xfox
#Custom Function

@xfox.addfunc(xfox.funcs)
async def test_func(item:str, *args, **kwargs):
    print("-----",kwargs)

@xfox.addfunc(xfox.funcs)
async def somef(item:str,*args, **kwargs):
    return kwargs["ctx"]

@xfox.addfunc(xfox.funcs)
async def function4(*args, **kwargs):
    return "FOX"

@xfox.addfunc(xfox.funcs)
async def function1(item:int, type:bool,*args, **kwargs):
    return type, args

@xfox.addfunc(xfox.funcs)
async def function2(item:str, *args, **kwargs):
    await xfox.isempty(item)
    return eval(item)

@xfox.addfunc(xfox.funcs)
async def inside(item:str, type:bool=False,*args, **kwargs):
    return type

@xfox.addfunc(xfox.funcs, 'usefunc')
async def functest(func:xfox.AnonFunction,*args, **kwargs):
    return (await func.compile(), func.name)



# Sync Parsing

print(asyncio.run(xfox.parse("""
/* TRASH (xd) */
$test_func[$test_func[sfsaf]]
$function1[1;$inside[true];$sadsadsdsd[]] $onlyif[1<2;ONLYIF]
$function2[1+2;dsadasd] sometext
$function4[]
$function1[1;$inside[fsfdfd;true];$sadsadsdsd[]]
$sdasdasd[sadsadsad]
sdasdsa $exec[true;print(1+231321, end='')] $exec[true;print(1+231321, end='')] $exec[true;print(1+231321, end='')]

/* Let/Get */
$let[test;good]
$get[test]

/* Internal Functions Test */
$usefunc[$def[$print[hello!]]]
$Test[]
$def[$print[hello!];Test]
$Test[] 
                             
/* While Test */
$let[a;0]
$while[$eval[$get[a]<=5];$let[a;$eval[$get[a]+1]]]
$get[a]
123 $while[True;$if[$get[a]<15;$let[a;$eval[$get[a]+1]];$break[]] $get[a]]
123 $while[True;$break[]]
$break[]

/* DoWhile Test */
$dowhile[1>2;Test]
                             
/* For Test */
$for[1..5;$get[i]]
$for[0..100..10;$get[i]]
$for[5;$if[$get[i]==2;$break[];$get[i]]]

/* Try Test */
$try[ERROR $get[_];$function1[]] 
$try[$print[$get[_]];$function2[]]
$try[$get[_];$raise[name;text]]

/* Import usage
$import[ttest]
$functiomm[] <- (custom function from ttest) */

/* Exit - $exit[] */
                                                                              
/* a Comment */ | &s Not a Comment &s
""", ctx="asdsdsdasds",del_empty_lines=True)))
```

Output:
```
----- {'ctx': 'asdsdsdasds'}
----- {'ctx': 'asdsdsdasds'}
[LOG] hello!
[LOG] hello!
[LOG] Mising var item in function2
None
(False, ('$sadsadsdsd[]',))
3 sometext
FOX
(True, ('$sadsadsdsd[]',))
$sdasdasd[sadsadsad]
sdasdsa 231322 231322 231322
good
('', 'a547f0')
$Test[]
6
123 789101112131415
123
Test
12345
0102030405060708090100
01
ERROR Mising var type in function1
[ERROR] name: text
 | // Not a Comment //
```

# Interactive Xfox Interpreter

```bash
python -m xfox
```

# Start xfox files

```bash
python -m xfox (filename).xfox
```

# Examples

Soon...
