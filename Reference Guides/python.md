# Python

Tim Stanford

- [Python](#python)
  - [Named Tuples](#named-tuples)
  - [Special Methods](#special-methods)
  - [List Comprehensions (listcomps)](#list-comprehensions-listcomps)
  - [Generator Expressions (genexp)](#generator-expressions-genexp)
  - [Argument Parsing](#argument-parsing)
  - [Unpacking tuples](#unpacking-tuples)
  - [Sorting Lists](#sorting-lists)
    - [Sort and modify the original array](#sort-and-modify-the-original-array)
    - [Sort and return a sorted array leaving original intact](#sort-and-return-a-sorted-array-leaving-original-intact)
  - [Sets](#sets)
  - [deque](#deque)
  - [Arrays](#arrays)
  - [memoryview](#memoryview)
  - [NumPy and SciPy](#numpy-and-scipy)

## Named Tuples

    Card = collections.namedtuple('Card', ['rank', 'suit'])
    mycard = Card("5", "Hearts")
    print(mycard.rank)
    print(mycard.suit)

## Special Methods

Always start with 2 underscores and end with 2 underscores. Add interface to built in python workings.

    __len__     get number of items in list. len(myobj)
    __getitem__ used when refering to index of object. myobj[5]
    __init__    class constructor
    __repr__    called when print("my object: %r" % (myobj))
    __str__     called when print("my object: %s" % (myobj))
    __bool__    boolean representation of object
    __add__     implement add operator support
    __mul__     implement multiply operator support

## List Comprehensions (listcomps)

These are surrounded by square brackets and directly produce a list in memory

    chars = "abcdefg"
    codes = [ord(c) for c in chars]
    print(codes)

## Generator Expressions (genexp)

These are surrounded by normal brackets and produce an iterator to generate the values on demand through a for loop.

    chars = "abcdefg"
    codes = (ord(c) for c in chars)
    for code in codes:
        print code

## Argument Parsing

The argparse package provides a way to specify certain available switches for your command line script and havw them parsed automatically. In addition, It provides automatic help generation to inform the user which switches are available.

https://docs.python.org/3/library/argparse.html

    parser = argparse.ArgumentParser(description="Simple tiling for GTK")
    parser.add_argument("w", type=int,
                        help="Frame width (in percentage of screen width)")
    parser.add_argument("h", type=int,
                        help="Frame height (in percentage of screen height)")
    parser.add_argument("x", type=int,
                        help="Frame x coordinate (in percentage of screen width)")
    parser.add_argument("y", type=int,
                        help="Frame y coordinate (in percentage of screen height)")
    parser.add_argument("-d", type=int, choices=[0, 1], default=1,
                        help="1 for window decorations, 0 for none")
    args = parser.parse_args()

    w = int(round(args.w / 100.0 * screen_width))

## Unpacking tuples

    metro_areas = [
        ('Tokyo', 'JP', 36.933, (35.689722, 139.691667)),
        ('Delhi NCR', 'IN', 21.935, (28.613889, 77.208889)),
        ('Mexico City', 'MX', 20.142, (19.433333, -99.133333)),
        ('New York-Newark', 'US', 20.104, (40.808611, -74.020386)),
        ('Sao Paulo', 'BR', 19.649, (-23.547778, -46.635833)),
    ]

    print('{:15} | {:^9} | {:^9}'.format('', 'lat.', 'long.'))
    fmt = '{:15} | {:9.4f} | {:9.4f}'
    for name, cc, pop, (latitude, longitude) in metro_areas:
        if longitude <= 0:  # 3
            print(fmt.format(name, latitude, longitude))

## Sorting Lists

### Sort and modify the original array

    myArray.sort()

### Sort and return a sorted array leaving original intact

    mySortedList = sorted(myArray)

## Sets

## deque
Double ended queues

## Arrays
More efficient than lists but values must be the same type. Arrays are stored like C array but are mutable.

Arrays support array.tofile array.fromfile method to read and write from/to disk.

The pickle module can also persist and retrieve data on disk.

For representing binary data, python has bytes and bytearray types

Arrays don't have a sorted method. you have to sort an array using the sorted function

## memoryview

## NumPy and SciPy

