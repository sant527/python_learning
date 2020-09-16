# python_learning

## Q: List changes unexpectedly after assignment. How do I clone or copy it to prevent this?

https://stackoverflow.com/questions/2612802/list-changes-unexpectedly-after-assignment-how-do-i-clone-or-copy-it-to-prevent
> While using `new_list = my_list`, any modifications to new_list changes my_list everytime. Why is this, and how can I clone or copy the list to prevent it?

### Answer:

With `new_list = my_list`, you don't actually have two lists. The assignment just copies the reference to the list, not the actual list, so both `new_list` and `my_list` refer to the same list after the assignment.

To actually copy the list, you have various possibilities:

- You can use the builtin [`list.copy()`](https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types) method (available since Python 3.3):

        new_list = old_list.copy()

- You can slice it: 

        new_list = old_list[:]

  [Alex Martelli's][1] opinion (at least [back in 2007][2]) about this is, that *it is a weird syntax and it does not make sense to use it ever*. ;) (In his opinion, the next one is more readable).

- You can use the built in [`list()`][3] function:

        new_list = list(old_list)


- You can use generic [`copy.copy()`][4]:

        import copy
        new_list = copy.copy(old_list)

  This is a little slower than `list()` because it has to find out the datatype of `old_list` first.

- If the list contains objects and you want to copy them as well, use generic [`copy.deepcopy()`][5]:

        import copy
        new_list = copy.deepcopy(old_list)

  Obviously the slowest and most memory-needing method, but sometimes unavoidable.


**Example:**

    import copy
    
    class Foo(object):
        def __init__(self, val):
             self.val = val
    
        def __repr__(self):
            return 'Foo({!r})'.format(self.val)
    
    foo = Foo(1)
    
    a = ['foo', foo]
    b = a.copy()
    c = a[:]
    d = list(a)
    e = copy.copy(a)
    f = copy.deepcopy(a)
    
    # edit orignal list and instance 
    a.append('baz')
    foo.val = 5
    
    print('original: %r\nlist.copy(): %r\nslice: %r\nlist(): %r\ncopy: %r\ndeepcopy: %r'
          % (a, b, c, d, e, f))

Result:

    original: ['foo', Foo(5), 'baz']
    list.copy(): ['foo', Foo(5)]
    slice: ['foo', Foo(5)]
    list(): ['foo', Foo(5)]
    copy: ['foo', Foo(5)]
    deepcopy: ['foo', Foo(1)]


[1]: https://en.wikipedia.org/wiki/Alex_Martelli "Alex Martelli"
[2]: https://www.youtube.com/watch?v=g7V89K8QfgQ "Bay Area Python Interest Group August 2007 Meeting"
[3]: https://docs.python.org/2/library/functions.html#list "list"
[4]: https://docs.python.org/2/library/copy.html#copy.copy "copy.copy"
[5]: https://docs.python.org/2/library/copy.html#copy.deepcopy "copy.deepcopy"
