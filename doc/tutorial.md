# Quick tutorial for aa_sbst (self-balancing binary search tree implementation for Python)

## How to embed

There are three ways to embed this functionality into your project:
1. Get this module by `pip install aa_sbst` and then import into your module by `import aa_sbst`.
2. Directly download `aa_sbst.py` file and adopt it into your project.
3. In some cases you might prefer simply copy-paste the implementation into your source code. Feel free doing this. Just find comments "# -------------- Start copy-paste from here" and "# -------------- Finish copy-paste here", and take the lines between them.

## How to use

Actually, you do not need to bother about tree nodes. You simply create tree, and then add values (whatever they would be) and get them from the tree.

If you embedded this functionality using thw way 1 or 2 described above, first of all import this module:
```
import aa_sbst
```
Then create the tree object:
```
my_tree = aa_sbst.sbst()
```
We just created uninitializes tree with default arranging function.

### Basic functions (`add`, `addfrom`, `min`, `max`, `forward_from`, `backward_from`, and `remove`)

Let's add some values:
```
my_tree.add(1)
my_tree.add(3)
my_tree.add(-2)
my_tree.add(10)
```
Also you can add values from an iterable object:
```
my_tree.addfrom(i**3 for i in range(2, 6))
```
Now we are ready to look for values in the tree. Let's find maximal value that is not greater then, for example, 20:
```
my_tree.max(20)
```
Result:
```
10
```
Lookin for the minimal value that is not less then 27:
```
my_tree.min(27)
```
Result:
```
27
```
Lookin for the minimal value that is greater then 27 (`inclusive` parameter set to `False`):
```
my_tree.min(27, False)
```
Result:
```
64
```
Methods `forward_from` and `backward_from` useful for getting sequences from the tree, and they can be used just for lookin at the values stored in the tree:
```
print(*[v for v in my_tree.forward_from()])
```
Result:
```
-2 1 3 8 10 27 64 125
```
We did not specified starting value so all the values are printed. Let specify a starting value, for example, 10:
```
print(*[v for v in my_tree.forward_from(10)])
```
Result:
```
10 27 64 125
```
Or 11 (not present in the tree) for starting value:
```
print(*[v for v in my_tree.forward_from(11)])
```
Result:
```
27 64 125
```
If you need to excude starting value from the iteration, set `False` for parameter `inclusive`:
```
print(*[v for v in my_tree.forward_from(10, False)])
```
Result:
```
27 64 125
```
To set upper limit for `forward_from`, use parameter `stop` and, if needed, `stop_incl`:
```
print(*[v for v in my_tree.forward_from(10, False, stop=100)])
```
Result:
```
27 64
```

**Important:** Including/excluding options for starting and stopping values by default are *True for start* and *False for stop*. Like start and stop for `range` object.

`backward_from` works like `forward_from`, but enumerates values backward from start to stop:
```
print(*[v for v in my_tree.backward_from(100, stop=10)])
```
Result:
```
64 27
```
Removing values from the tree:
```
print(*[v for v in my_tree.forward_from()])
my_tree.remove(8)
print(*[v for v in my_tree.forward_from()])
```
Result:
```
-2 1 3 8 10 27 64 125
-2 1 3 10 27 64 125
```

**Important notice:** This implementation holds all the inserted duplicates:
```
print(*[v for v in my_tree.forward_from()])
my_tree.add(10)
print(*[v for v in my_tree.forward_from()])
```
Result:
```
-2 1 3 10 27 64 125
-2 1 3 10 10 27 64 125
```

### Using custom comparison functions

Coming soon...
