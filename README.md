   * [python_learning](#python_learning)
      * [Q: List changes unexpectedly after assignment. How do I clone or copy it to prevent this?](#q-list-changes-unexpectedly-after-assignment-how-do-i-clone-or-copy-it-to-prevent-this)
         * [Answer PART1: List changes unexpectedly after assignment](#answer-part1-list-changes-unexpectedly-after-assignment)
            * [Understanding mutable vs immutable](#understanding-mutable-vs-immutable)
      * [Python Classes](#python-classes)
         * [To create a class, use the keyword class:](#to-create-a-class-use-the-keyword-class)
         * [Create Object](#create-object)
      * [Python getattr()](#python-getattr)
   * [How to flatten a nested array and again get it back to nested state:](#how-to-flatten-a-nested-array-and-again-get-it-back-to-nested-state)
   * [Tabs and invalid syntax](#tabs-and-invalid-syntax)
   * [How to know the path of a module](#how-to-know-the-path-of-a-module)

# python_learning

## Q: List changes unexpectedly after assignment. How do I clone or copy it to prevent this?

https://stackoverflow.com/questions/2612802/list-changes-unexpectedly-after-assignment-how-do-i-clone-or-copy-it-to-prevent
> While using `new_list = my_list`, any modifications to new_list changes my_list everytime. Why is this, and how can I clone or copy the list to prevent it?

### Answer PART1: List changes unexpectedly after assignment

**Trying to Assign mutable objects**
```python
m = list([1, 2, 3])`
n = m
```
Since, python lists are mutable, m and n will still be reference to the same object after mutation. Whereas, for immutable objects like int, a new object will be created and the identifier will refer to the new object.

With `new_list = my_list`, you don't actually have two lists. The assignment just copies the reference to the list, not the actual list, so both `new_list` and `my_list` refer to the same list after the assignment.

**Answer PART2: How do I clone or copy it to prevent this**

However, if you need the original list unchanged when the new list is modified, you can use the copy() method.

`newlist = [*mylist]` also is a possibility in Python 3. `newlist = list(mylist)` maybe is more clear though.

`new_list = original_list.copy()`

The ids of new_list and original_list is different.

#### Understanding mutable vs immutable

**Mutable**

`lists, dictionaries and sets` are mutable , meaning you can change their content without changing their identity. Custom classes are generally mutable.

Trying to change mutable objects
```python
# Python code to test that 
# lists are mutable 
color = ["red", "blue", "green"] 
print(color) 

color[0] = "pink"
color[-1] = "orange"
print(color) 
```

**Immutable**

These are of in-built types like `int, float, bool, string, unicode, tuple`. In simple words, an immutable object can’t be changed after it is created

```python
tuple1 = (0, 1, 2, 3)  
tuple1[0] = 4
print(tuple1)
```
>Traceback (most recent call last):
>  File "e0eaddff843a8695575daec34506f126.py", line 3, in 
>    tuple1[0]=4
>TypeError: 'tuple' object does not support item assignment

## Python Classes

### To create a class, use the keyword class:

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self):
    print("Hello my name is " + self.name)

p1 = Person("John", 36)
p1.myfunc()

```
> Note: The `self` parameter is a reference to the current instance of the class, and is used to access variables that belong to the class.

**Python 3: 3 ways of creating class; Class and object inheritance**
**Q: Should all Python classes extend object?**

>In python 3 you can create a class in three different ways & internally they are all equal (see examples). It doesn't matter how you create a class, all classes in python 3 inherits from special class called object. The class object is fundamental class in python and provides lot of functionality like double-underscore methods, descriptors, super() method, property() method etc.

Example 1.
```python
class MyClass:
 pass
```
Example 2.
```python
class MyClass():
 pass
```
Example 3.
```python
class MyClass(object):
  pass
```

### Create Object
Now we can use the class named MyClass to create objects:

Example
Create an object named p1, and print the value of x:
```python
p1 = Person("John", 36)
p1.myfunc()
```

## Python getattr()
The `getattr()` method returns the value of the named attribute of an object. If not found, it returns the default value provided to the function.

**The syntax of getattr() method is:**
```python
getattr(object, name[, default])
```
The above syntax is equivalent to:
```python
object.name
```

**getattr() Parameters**  
getattr() method takes multiple parameters:  
`object` - object whose named attribute's value is to be returned  
`name` - string that contains the attribute's name  
`default (Optional)` - value that is returned when the named attribute is not found

**Return value from getattr()**  
getattr() method returns:  
`value` of the named attribute of the given object  
`default`, if no named attribute is found  
`AttributeError` exception, if named attribute is not found and default is not defined

**Example 1: How getattr() works in Python?**
```python
class Person:
    age = 23
    name = "Adam"

person = Person()
print('The age is:', getattr(person, "age"))
print('The age is:', person.age)
```
Output
```
The age is: 23
The age is: 23
Example 2: getattr() when named attribute is not found
class Person:
    age = 23
    name = "Adam"

person = Person()
```
**when default value is provided**
```python
print('The sex is:', getattr(person, 'sex', 'Male'))
```
**when no default value is provided**
```python
print('The sex is:', getattr(person, 'sex'))
```
Output
```
The sex is: Male
AttributeError: 'Person' object has no attribute 'sex'
The named attribute sex is not present in the class Person. So, when calling getattr() method with a default value Male, it returns Male.
```
**But, if we don't provide any default value, when the named attribute sex is not found, it raises an AttributeError saying the object has no sex attribute.**


# How to flatten a nested array and again get it back to nested state:

```python
#Nested bookmark array:

bookmarks = [
    {
        "/Page": "0",
        "/Title": "title000",
        "/Type": "/Fit"
    },
    {
        "/Page": "0",
        "/Title": "title000",
        "/Type": "/Fit"
    },
    [
        {
            "/Page": "1",
            "/Title": "title001",
            "/Type": "/Fit"
        },
        [
            {
                "/Page": "3",
                "/Title": "title008",
                "/Type": "/Fit"
            },
            [
                {
                    "/Page": "6",
                    "/Title": "title006",
                    "/Type": "/Fit"
                }
            ]
        ],
        {
            "/Page": "2",
            "/Title": "title002",
            "/Type": "/Fit"
        },
        [
            {
                "/Page": "3",
                "/Title": "title008",
                "/Type": "/Fit"
            },
            [
                {
                    "/Page": "6",
                    "/Title": "title006",
                    "/Type": "/Fit"
                },
                {
                    "/Page": "7",
                    "/Title": "title007",
                    "/Type": "/Fit"
                }
            ]
        ]
    ],
    {
        "/Page": "0",
        "/Title": "title000",
        "/Type": "/Fit"
    },
    [
        {
            "/Page": "1",
            "/Title": "title001",
            "/Type": "/Fit"
        },
        {
            "/Page": "2",
            "/Title": "title002",
            "/Type": "/Fit"
        }
    ]
]


#### CONVERT NESTED ARRAY TO FLATTENED ARRAY

def flatten1(bookmarks,hare_array,last_added=0):
    hare= hare_array
    last_added = last_added + 1
    for b in bookmarks:
        if isinstance(b, list):
            flatten1(b, hare, last_added)
            continue
        b["level"] = last_added
        hare.append(b)

hare=[]
flatten1(bookmarks,hare)

import json
print("hare = "+json.dumps(hare, indent=1, sort_keys=True, default=str))

#PRINTOUTPUT
# hare = [
#     {"/Page": "0","/Title": "title000","/Type": "/Fit","level": 1},
#     {"/Page": "0","/Title": "title000","/Type": "/Fit","level": 1},
#     {"/Page": "1","/Title": "title001","/Type": "/Fit","level": 2},
#     {"/Page": "3","/Title": "title008","/Type": "/Fit","level": 3},
#     {"/Page": "6","/Title": "title006","/Type": "/Fit","level": 4},
#     {"/Page": "2","/Title": "title002","/Type": "/Fit","level": 2},
#     {"/Page": "3","/Title": "title008","/Type": "/Fit","level": 3},
#     {"/Page": "6","/Title": "title006","/Type": "/Fit","level": 4},
#     {"/Page": "7","/Title": "title007","/Type": "/Fit","level": 4},
#     {"/Page": "0","/Title": "title000","/Type": "/Fit","level": 1},
#     {"/Page": "1","/Title": "title001","/Type": "/Fit","level": 2},
#     {"/Page": "2","/Title": "title002","/Type": "/Fit","level": 2}
# ]

# Note that we add parameter called level



#### CONVERT FLATTENED ARRAY TO NESTED ARRAY BACK

toc = hare.copy()

toclen = len(toc)


import pudb;pudb.set_trace()
nested_array=[]
for i in range(toclen):
    o = toc[i]
    n=toc[i]["level"]
    print("n=toc[i][\"level\"]:: i,n ::"+str(i)+","+str(n))
    index=""
    arr1 = None
    for j in range(0,n):
        print("i,j ::::"+str(i)+","+str(j))
        if arr1 is None:
            arr1 = nested_array
        else:
            len_arr1 = len(arr1)
            if isinstance(arr1[len_arr1-1], list):
                arr1=arr1[len_arr1-1]
            else:
                arr1.append([])
                len_arr1 = len(arr1)
                arr1=arr1[len_arr1-1]
    arr1.append(o)

import json
print("nested_array == "+json.dumps(nested_array, indent=4, sort_keys=True, default=str))


#PRINT OUTPUT
### nested_array == [
###     {
###         "/Page": "0",
###         "/Title": "title000",
###         "/Type": "/Fit",
###         "level": 1
###     },
###     {
###         "/Page": "0",
###         "/Title": "title000",
###         "/Type": "/Fit",
###         "level": 1
###     },
###     [
###         {
###             "/Page": "1",
###             "/Title": "title001",
###             "/Type": "/Fit",
###             "level": 2
###         },
###         [
###             {
###                 "/Page": "3",
###                 "/Title": "title008",
###                 "/Type": "/Fit",
###                 "level": 3
###             },
###             [
###                 {
###                     "/Page": "6",
###                     "/Title": "title006",
###                     "/Type": "/Fit",
###                     "level": 4
###                 }
###             ]
###         ],
###         {
###             "/Page": "2",
###             "/Title": "title002",
###             "/Type": "/Fit",
###             "level": 2
###         },
###         [
###             {
###                 "/Page": "3",
###                 "/Title": "title008",
###                 "/Type": "/Fit",
###                 "level": 3
###             },
###             [
###                 {
###                     "/Page": "6",
###                     "/Title": "title006",
###                     "/Type": "/Fit",
###                     "level": 4
###                 },
###                 {
###                     "/Page": "7",
###                     "/Title": "title007",
###                     "/Type": "/Fit",
###                     "level": 4
###                 }
###             ]
###         ]
###     ],
###     {
###         "/Page": "0",
###         "/Title": "title000",
###         "/Type": "/Fit",
###         "level": 1
###     },
###     [
###         {
###             "/Page": "1",
###             "/Title": "title001",
###             "/Type": "/Fit",
###             "level": 2
###         },
###         {
###             "/Page": "2",
###             "/Title": "title002",
###             "/Type": "/Fit",
###             "level": 2
###         }
###     ]
### ]
```


# Tabs and invalid syntax

The below code works well in python shell

```
import fitz
filename="Adi_index.pdf"
doc = fitz.open(filename)  # open file
toc_mu = doc.getToC(False) # its table of contents (list)
# [ [level,Title,Pagenum],[level,Title,Pagenum] .....]
pc = len(doc)  # number of its pages

new_format=[]
for line in toc_mu:  # read toc 
    new_format.append({"/Page": line[2],"/Title": line[1],"/Type": "/Fit","level": line[0]})

print(new_format)
```

This will look as below in python shell

```
>>> import fitz
>>> filename="Adi_index.pdf"
>>> doc = fitz.open(filename)  # open file
>>> toc_mu = doc.getToC(False) # its table of contents (list)
>>> # [ [level,Title,Pagenum],[level,Title,Pagenum] .....]
... pc = len(doc)  # number of its pages
>>> 
>>> new_format=[]
>>> for line in toc_mu:  # read toc 
...     new_format.append({"/Page": line[2],"/Title": line[1],"/Type": "/Fit","level": line[0]})
... 
>>> print(new_format)
```


whereas 

```
import fitz
filename="Adi_index.pdf"
doc = fitz.open(filename)  # open file
toc_mu = doc.getToC(False) # its table of contents (list)
# [ [level,Title,Pagenum],[level,Title,Pagenum] .....]
pc = len(doc)  # number of its pages

new_format=[]
for line in toc_mu:  # read toc 
    new_format.append({"/Page": line[2],"/Title": line[1],"/Type": "/Fit","level": line[0]})
    
# IF THERE IS TAB ABOVE THEN ITS INVALID SYNTAX
print(new_format)
```

![](./images/2020-09-18_12-20.png)

This will look as belwo in python shell and it gives error

```
>>> import fitz
>>> filename="Adi_index.pdf"
>>> doc = fitz.open(filename)  # open file
>>> toc_mu = doc.getToC(False) # its table of contents (list)
>>> # [ [level,Title,Pagenum],[level,Title,Pagenum] .....]
... pc = len(doc)  # number of its pages
>>> 
>>> new_format=[]
>>> for line in toc_mu:  # read toc 
...     new_format.append({"/Page": line[2],"/Title": line[1],"/Type": "/Fit","level": line[0]})
...     
... # IF THERE IS TAB ABOVE THEN ITS INVALID SYNTAX
... print(new_format)
  File "<stdin>", line 5
    print(new_format)
```

![](./images/2020-09-18_12-29.png)

# How to know the path of a module

```
>> import PyPDF2
>>> PyPDF2.__file__
'/usr/lib/python3.7/site-packages/PyPDF2/__init__.py'
>>> 
```


# Checking bool: is vs ==

https://stackoverflow.com/questions/27276610/boolean-identity-true-vs-is-true

 > if you want to check that some variable "is exactly True", you have to use the identity operator is and dont use ==
 
 ```python
 >>> d = True
>>> d is True
True
>>> d = 1
>>> d is True
False
>>> d == True
True
>>> d = 2
>>> d == True
False
 ```
 
 > If you want to make sure that foo really is a boolean and of value True, use the is operator.




# TIME ZONE AND PYTHON WITH DAYLIST SAVING

## Q I want to know the current time as per time zone 'America/New_York'

Note: datetime.now() does not return a timezone aware timestamp. It will return the pc local time

```python
from datetime import datetime 
import pytz
pacific = pytz.timezone('America/New_York')
# datetime.utcnow() -- gives current time in utc time zone
# but this time is not a timezone aware time. 
# So we make it utc time zone aware
current_time_utc = pytz.utc.localize(datetime.utcnow())
current_time_utc.isoformat()
current_time_pacific = current_time_utc.astimezone(pacific)
current_time_pacific.isoformat()
```
Example
```python
>>> pacific = pytz.timezone('America/New_York')
>>> current_time_utc = pytz.utc.localize(datetime.utcnow())
>>> current_time_utc.isoformat()
'2021-01-31T03:57:59.431527+00:00'
>>> current_time_pacific = current_time_utc.astimezone(pacific)
>>> current_time_pacific.isoformat()
'2021-01-30T22:57:59.431527-05:00'
```


## checking for daylight saving
in usa/newyork EST is winter time and EDT is summer time where day light saving is used

```python
from datetime import datetime 
import pytz
pacific = pytz.timezone('America/New_York')
# we are using a particular time in june month and making it as utc time aware
current_time_utc = pytz.utc.localize(datetime(2021,6,1,0,0,0))
current_time_utc.isoformat()
current_time_pacific = current_time_utc.astimezone(pacific)
current_time_pacific.isoformat()
```

```python
>>> pacific = pytz.timezone('America/New_York')
>>> current_time_utc = pytz.utc.localize(datetime(2021,6,1,0,0,0))
>>> current_time_utc.isoformat()
'2021-06-01T00:00:00+00:00'
>>> current_time_pacific = current_time_utc.astimezone(pacific)
>>> current_time_pacific.isoformat()
'2021-05-31T20:00:00-04:00'
```

so -4:00 and -5:00 means its showing correct


## How to get midnight time from current time

sometimes we want to know the data for that day till that time from midnight.

By below we can get the midnight time and from above we can get the current time

```
from datetime import datetime, time
import pytz
#get current time in that particular time zone
pacific = pytz.timezone('America/New_York')
current_time_utc = pytz.utc.localize(datetime.utcnow())
current_time_utc.isoformat()
current_time_pacific = current_time_utc.astimezone(pacific)
current_time_pacific.isoformat()

# get the date and from that get the midnight datetime
date = current_time_pacific.date()
date
mid_night_pacific = pacific.localize(datetime.combine(date, time.min)).isoformat()
mid_night_pacific
```


## How to convert isoformat string to datetime

```python
import dateutil.parser
import datetime
import pytz

EST = pytz.timezone('America/New_york')
when  = dateutil.parser.parse("2021-01-30 09:59:57+00")
when.astimezone(EST)
```


# Django Safely outputs a Python object as JSON, wrapped in a <script> tag, ready for use with JavaScript.
https://docs.djangoproject.com/en/3.1/ref/templates/builtins/#json-script

```javascript
{{ value|json_script:"hello-data" }}
```

If value is the dictionary {'hello': 'world'}, the output will be:

```javascript
<script id="hello-data" type="application/json">{"hello": "world"}</script>
```

The resulting data can be accessed in JavaScript like this:

```javascript
const value = JSON.parse(document.getElementById('hello-data').textContent);
```



# PANDAS INDEXING

## how to change a value in a pandas table

I have a sample pandas dataframe `df`

```
       id          name   state
229  1281  something000      0
230  1465  something001      1
231  1467  something002      0
232  1469  something003      1
233  1470  something004      0
234  1472  something005      1
235  1474  something006      0
236  1475  something007      1
237  1477  something008      0
238  1479  something009      1
239  1480  something010      0
240  1482  something011      1
241  1484  something012      0
242  1488  something013      1
243  1489  something014      0
244  1493  something015      1
245  1494  something016      0
246  1499  something017      1
247  1500  something018      0
248  1507  something019      1
249  1508  something020      0
250  1632  something021      1
```

Now i want to change the value of last row from `something021` to `something2000`

If i try: since -1 indicates last row
```
df.loc[-1, 'name'] = something2000
```
and now we check what happened

```
       id          name   state
229  1281  something000      0
230  1465  something001      1
231  1467  something002      0
232  1469  something003      1
233  1470  something004      0
234  1472  something005      1
235  1474  something006      0
236  1475  something007      1
237  1477  something008      0
238  1479  something009      1
239  1480  something010      0
240  1482  something011      1
241  1484  something012      0
242  1488  something013      1
243  1489  something014      0
244  1493  something015      1
245  1494  something016      0
246  1499  something017      1
247  1500  something018      0
248  1507  something019      1
249  1508  something020      0
250  1632  something021      1
-1    NaN  something2000    NaN
```

so instead of changing the last row (-1) it added a row with index -1

so the right way is

```
df.loc[df.index[-1], 'name'] = something2000
```

```
df.index[-1] gives 250
```
https://stackoverflow.com/questions/66096734/pandas-df-loc-1-col-sometimes-work-and-sometimes-add-extra-row-with-nan/66096764?noredirect=1#comment116873879_66096764


# how to see a row from a dataframe

## if we know the position: best way using iloc 
```
df.iloc[0]
id       1281
name     something000
state    0
Name: 229, dtype: object
```

## if we know the string value of the index then
```
df.loc[229]
id       1281
name     something000
state    0
Name: 229, dtype: object
```

https://stackoverflow.com/a/31593712

## How pandas work


## How to use ROOT_URLS settings to use the same app for different domains

https://www.valentinog.com/blog/django-vhosts/

>**When Django receives a request it has to pick a root url configuration** from which it extracts all the paths available for our users. By default the root urlconf is defined in ROOT_URLCONF. For example our simple project has the following root url configuration:

## How to handle multiple sites in Django: the middleware

using middleware

```
virtual_hosts = {
    "www.example-a.dev": "blog.urls",
    "www.example-b.dev": "links.urls",
    "www.example-c.dev": "links.urls",
}


class VirtualHostMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        # let's configure the root urlconf
        host = request.get_host()
        request.urlconf = virtual_hosts.get(host)
        # order matters!
        response = self.get_response(request)
        return response
```

```
MIDDLEWARE = [
    # our custom middleware
    "django_quick_start.virtualhostmiddleware.VirtualHostMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
]
```

## A note on url namespaces

It is a good idea in Django to namespace each application's url:

```
from django.urls import path
from .views import index

app_name = "blog"

urlpatterns = [path("blog/", index, name="index")]
```

Here the namespace for this app is "blog", and the index view is "index". Whenever we want to reference this view in our code we can use reverse:

```
from django.urls import reverse

# omit
view = reverse("blog:index")
# omit
```

Now **the problem here is that with our virtual host middleware we effectively make the namespace redundant.**

When we set request.urlconf in the middleware to a single URL conf, that configuration will be the only group of paths to be loaded. 

So instead of:
```
<form action="{% url "blog:post_create" %}" method="post">
<!-- omit -->
</form>
```
do:
```
<form action="{% url "post_create" %}" method="post">
<!-- omit -->
</form>
```

# Use django-hosts for using django for multiple subdomains

Note: django-hosts searches for the `regex` + `(.|$)(added by it)`.

https://www.ordinarycoders.com/blog/article/django-subdomains
## Access the subdomain on your localhost
>If you run the server and visit 127.0.0.1:800, the main app is displaying.
>
>But to get to the blog app, we need to visit blog.local:8000. If you try to access this page, it does not load. That's because there is no local DNS host that matches. We need to add it to the list of hosts. 
