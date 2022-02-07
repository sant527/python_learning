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



# using django runserver_plus for ajax calls

This is quite an old question, but as I saw it as reference and have a slightly different solution, I figured I might as well add my two cents.

I use python manage.py runserver_plus, which comes with django extensions, and gives you an awesome debugger with the ability to open a shell at each level of the stack trace, with local variables intact. The problem here is that on ajax calls, the interface didn't show up correctly, even in the preview window. My solution was to find the calling javascript code, and on error

**NOTE DIDNT WORK IN CHROME** Says winPrint is null. Firefox it works


      $.ajax({
                url : window.location.pathname,
                type : "POST",
                dataType: "json",
                data : dataPacket,
                success : function(json) {
                    alert('it worked!');
                },
                error : function(xhr,errmsg,err) {
                    if(xhr.status == 500){
                        var winPrint = window.open();
                        winPrint.document.write(xhr.responseText);
                        winPrint.document.close();
                    }
                });
                
                
for axios  use

```
           if(error.response.status == 500){
                var winPrint2 = window.open();
                winPrint.document.write(error.response.data);
                winPrint.document.close();
            }
```
                
This causes the full stack trace to replace the current window.
Happy debugging! 



# python standalone script debugging in console
https://stackoverflow.com/a/41748274/2897115

If you have ipython (highly, highly recommended), you can go to any point in your program and add the following lines

** also install ipdb : `pip install ipdb`, else the code does not stop there

    import IPython
    IPython.embed()

    or
    
    import IPython
    IPython.embed(); exit() 
    
    to avoid looping
   
 ALSO USE 

this will open console even with runserver in DJango
https://stackoverflow.com/questions/1118183/how-to-debug-in-django-the-good-way

Once your program reaches that point, the `embed` command will open up a new IPython shell within that context.

I really like to do that for things where I don't want to go the full pdb route.

# USING DOCKER HOW TO USE IPYTHON THING

https://blog.lucasferreira.org/howto/2017/06/03/running-pdb-with-docker-and-gunicorn.html

## Adding support for PDB debug

We should change two things in the file docker-compose.yml to support the PDB debugger:

- Add `stdin_open: true` and `tty: true` to the service configuration. These options will allow us to attach into the gunicorn running process and use the debugger.
-  Add `-t 3600` to the gunicorn command. This will change the timeout value to 3600 seconds. The default value of 30 seconds would probably kill the process before we finish using the debugger, so this value must be increased.

docker-compose.yml

```
version: '3'

services:
    demo_web:
        build:
            context: .
            dockerfile: demo_web/Dockerfile
        ports:
            - "80:8000"
        command: /usr/local/bin/gunicorn -w 2 -t 3600 -b :8000 app:app --reload
        volumes:
            - ./demo_web:/usr/src/app
        stdin_open: true
        tty: true
```

## Attach into the process

The debugger is running inside the container, so we need to attach into the container to use it.

- Find the container id using docker container ps and copy the first two or three letters of the container id column.
- Use the command docker attach CONTAINER_ID to attach to the container.

To exit you should use `CONTROL + P, CONTROL + Q`. This will detach from the container without killing it. If you use `Control + C` the container will stop.






# Django multi language (for permanent setting)
https://samulinatri.com/blog/django-translation/

## step1:: pipenv install gettext

gettext cannot be installed using pip

its a GNU package in linux

so login as root to the webapp

```
docker-compose -p bagnoli -f docker-compose-localhost.yml exec --user root webapp /bin/bash
```

then do

```
apt-get update
apt-get install gettext

or for docker

docker-compose -p bagnoli -f docker-compose-localhost.yml exec --user root webapp /bin/bash -c "apt-get update;apt-get -y install gettext"
```


## step2:: add in settings

```
#LANGUAGE_CODE = 'en-us'
LANGUAGE_CODE = 'fi'
```

and

```
LOCALE_PATHS = [os.path.join(BASE_DIR, 'locale')]
```

## step3 make a dir called locale in BASE_DIR

```
mkdir locale
```

## step 4: Edit a template file, load the i18n tag and use the trans tag to translate a string:

```
{% load i18n %}
<p>{% trans "Life is life." %}</p>
```

## step 5:  run the makemessages command:

```
django-admin makemessages -l fi --ignore venv
```

## step6: Edit locale/fi/LC_MESSAGES/django.po and add the translation:

```
msgid "Life is life."
msgstr "Elämä on laiffii." # HERE
```

## compile the messages

```
django-admin compilemessages --ignore venv
```

# Django multi language (for browser based)

you have to use a middleware


# How to get the log time in a specified timezone
https://stackoverflow.com/a/47104004

```

import datetime
import logging
import pytz

class Formatter(logging.Formatter):
    """override logging.Formatter to use an aware datetime object"""
    def converter(self, timestamp):
        #dt = datetime.datetime.fromtimestamp(timestamp)
        #we use
        dt = datetime.datetime.utcnow()
        current_time_utc = pytz.utc.localize(dt)
        tzinfo = pytz.timezone('America/New_York')
        current_time_time_zone = current_time_utc.astimezone(tzinfo)
        #print(current_time_time_zone)
        return current_time_time_zone
        
    def formatTime(self, record, datefmt=None):
        dt = self.converter(record.created)
        if datefmt:
            s = dt.strftime(datefmt)
        else:
            try:
                s = dt.isoformat(timespec='milliseconds')
            except TypeError:
                s = dt.isoformat()
        return s


logger = logging.root
handler = logging.StreamHandler()
handler.setFormatter(Formatter("%(asctime)s %(message)s"))
logger.addHandler(handler)
logger.setLevel(logging.DEBUG)
logger.debug('test')

```


# Windows how to open cmd propmpt with subprocess

```
import sys
import os
import subprocess

file = "D:\\Dev\\Stock-chart\\backend_django\\stock\\cron_jobs\\cron_job.py"
python_path = sys.executable
dir1 = os.path.dirname(os.path.abspath(file))
file1 = "top50Scores.py"
filename = os.path.join(dir1,file1)
command = [python_path,filename]
command = ['start','cmd', '@cmd','/k',python_path,filename]
subprocess.Popen(command,shell=True)
```



# In windows create a showtchut file .bat to run django server

```

D:
cd D:\Dev\Stock-chart\backend_django

set "VIRTUAL_ENV=D:\Dev\Stock-chart\backend_django\venv"

set "WERKZEUG_DEBUG_PIN=off"


if defined _OLD_VIRTUAL_PROMPT (

    set "PROMPT=%_OLD_VIRTUAL_PROMPT%"

) else (

    if not defined PROMPT (

        set "PROMPT=$P$G"

    )

    if not defined VIRTUAL_ENV_DISABLE_PROMPT (

        set "_OLD_VIRTUAL_PROMPT=%PROMPT%"

    )

)

if not defined VIRTUAL_ENV_DISABLE_PROMPT (

    set "ENV_PROMPT="

    if NOT DEFINED ENV_PROMPT (

        for %%d in ("%VIRTUAL_ENV%") do set "ENV_PROMPT=(%%~nxd) "

    )

    )

    set "PROMPT=%ENV_PROMPT%%PROMPT%"

)



REM Don't use () to avoid problems with them in %PATH%

if defined _OLD_VIRTUAL_PYTHONHOME goto ENDIFVHOME

    set "_OLD_VIRTUAL_PYTHONHOME=%PYTHONHOME%"

:ENDIFVHOME



set PYTHONHOME=



REM if defined _OLD_VIRTUAL_PATH (

if not defined _OLD_VIRTUAL_PATH goto ENDIFVPATH1

    set "PATH=%_OLD_VIRTUAL_PATH%"

:ENDIFVPATH1

REM ) else (

if defined _OLD_VIRTUAL_PATH goto ENDIFVPATH2

    set "_OLD_VIRTUAL_PATH=%PATH%"

:ENDIFVPATH2



set "PATH=%VIRTUAL_ENV%\Scripts;%PATH%"

python manage.py runserver_plus 0.0.0.0:8000 --noreload
```

and for just opening a cmd prompt with activating virtualenv

```
D:
cd D:\Dev\Stock-chart\backend_django

set "VIRTUAL_ENV=D:\Dev\Stock-chart\backend_django\venv"



if defined _OLD_VIRTUAL_PROMPT (

    set "PROMPT=%_OLD_VIRTUAL_PROMPT%"

) else (

    if not defined PROMPT (

        set "PROMPT=$P$G"

    )

    if not defined VIRTUAL_ENV_DISABLE_PROMPT (

        set "_OLD_VIRTUAL_PROMPT=%PROMPT%"

    )

)

if not defined VIRTUAL_ENV_DISABLE_PROMPT (

    set "ENV_PROMPT="

    if NOT DEFINED ENV_PROMPT (

        for %%d in ("%VIRTUAL_ENV%") do set "ENV_PROMPT=(%%~nxd) "

    )

    )

    set "PROMPT=%ENV_PROMPT%%PROMPT%"

)



REM Don't use () to avoid problems with them in %PATH%

if defined _OLD_VIRTUAL_PYTHONHOME goto ENDIFVHOME

    set "_OLD_VIRTUAL_PYTHONHOME=%PYTHONHOME%"

:ENDIFVHOME



set PYTHONHOME=



REM if defined _OLD_VIRTUAL_PATH (

if not defined _OLD_VIRTUAL_PATH goto ENDIFVPATH1

    set "PATH=%_OLD_VIRTUAL_PATH%"

:ENDIFVPATH1

REM ) else (

if defined _OLD_VIRTUAL_PATH goto ENDIFVPATH2

    set "_OLD_VIRTUAL_PATH=%PATH%"

:ENDIFVPATH2



set "PATH=%VIRTUAL_ENV%\Scripts;%PATH%"

cmd
```


# celery import circular reference problem

https://stackoverflow.com/a/19942749/2897115

Instead of using he name `celery.py` use `celeryapp.py`

and change this in the __init__.py

```
from .celeryapp import app as celery_app

__all__ = ['celery_app']
```

reset all remains same

```
celery -A boiler worker
```
https://stackoverflow.com/questions/66521113/django-standalone-script-cannot-import-name-celery-from-celery?noredirect=1#comment117597299_66521113

# standalone DJANGO

`testing_standalone_django.py`

```py
import os, sys, django

"""
project folder:
--/home/simha/app
	-- boiler  <-- django-admin startproject mysite
		-- boiler
			-- setting.py
			-- testing_standalone_django.py  <-- current file
	-- Pipfile
	-- Pipefile.lock
	-- .venv
"""

# eg: proj_path :: /home/simha/app/boiler
proj_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
print(f"proj_path :: {proj_path}")

# if we dont add to sys.path then django.setup() will say boiler module not found
sys.path.append(proj_path)


os.environ.setdefault("DJANGO_SETTINGS_MODULE", "boiler.settings")
django.setup()

from django.contrib.auth import get_user_model
User = get_user_model()

test = User.objects.all()
for t in test:
	print(t)
```

Note for standalone Django script to work we have to rename celery.py to celeryapp.py

For 
```
python manager.py runserver 
and
celery -A boiler worker
```
its not required, else we will face circular reference error.

https://stackoverflow.com/questions/66521113/django-standalone-script-cannot-import-name-celery-from-celery?noredirect=1#comment117597299_66521113

# How to restart celery when changes are done in python files

```
pipenv install watchdog[watchmedo]
```

it stores in pipfile as
```
watchdog = {extras = ["watchmedo"], version = "*"}
```

and then do

```
 watchmedo auto-restart --directory=./ --pattern=*.py --recursive -- celery -A boiler worker --concurrency=1 --loglevel=DEBUG
```

implementing in the docker it becomes

```
  celery_worker:
    image: django:python-3.7.9-buster
    environment:
      - SQLPRINT=1
      - DEBUG=1       
    volumes:
      - type: bind
        source: ./python_django/Django_project_and_venv
        target: /home/simha/app
      - type: bind # .cache of pip will avoid download whl files again
        source: ../DO_NOT_DELETE_LOGS/DJANGO
        target: /home/simha/LOGS
    command:
      - sh
      - -c
      - |
        cd src
        pipenv run watchmedo auto-restart --directory=./ --pattern=*.py --recursive -- celery -A boiler worker --concurrency=1 --loglevel=DEBUG
      # https://www.distributedpython.com/2019/04/23/celery-reload/
      # https://gist.github.com/jsheedy/fda57e82c27f612d9aa875d9d869003f
      #pipenv run celery -A boiler worker --loglevel=debug #ensure redis-server is running in root and change backed to respective
    depends_on:  # wait for postgresql, redis to be "ready" before starting this service
      - postgresql
      - redis
    networks:  # connect to the bridge
      - postgresql_network
      - redis_network
```

# celery logging: How to control logging of outside celery task code

- This explains how to customize celery logging
https://www.distributedpython.com/2018/08/28/celery-logging/

- This explains how to allow celery logging only when something is called by celery task and rest of the time use other logging
https://www.distributedpython.com/2018/11/06/celery-task-logger-format/


# How to implement a logging system to store all the logging related to a sepecific task to a specicific folder

Change the folder name and dir1 as needed

`logging_for_celery.py`

```
# Also change dir1 as needed
# by default its the path of the current file
# assign dir2
LOG_DIRECTORY = "celery_logs"
TIMEZONE = 'America/New_York'
import json
def jdmp(obj):
    return json.dumps(obj,indent=4,default=str)

import pytz
import datetime
import logging
class Formatter(logging.Formatter):
    """override logging.Formatter to use an aware datetime object"""
    def converter(self, timestamp):
        #dt = datetime.datetime.fromtimestamp(timestamp)
        #we use
        dt = datetime.datetime.utcnow()
        current_time_utc = pytz.utc.localize(dt)
        tzinfo = pytz.timezone(TIMEZONE)
        current_time_time_zone = current_time_utc.astimezone(tzinfo)
        #print(current_time_time_zone)
        return current_time_time_zone
        
    def formatTime(self, record, datefmt=None):
        dt = self.converter(record.created)
        if datefmt:
            s = dt.strftime(datefmt)
        else:
            try:
                s = dt.isoformat(timespec='milliseconds')
            except TypeError:
                s = dt.isoformat()
        return s


    def format(self, record):
        try:
            ## We want to show some code lines while logging. So that its eays to know 
            #create a list of all the linenumber: lines 
            lines=[]
            with open(record.pathname) as src:
                for index, line in enumerate(src.readlines(), start=1):
                    if index == record.lineno:
                        lines.append('{:4d}***: {}'.format(index, line))
                    else:
                        lines.append('{:7d}: {}'.format(index, line))
            # select +/-3 lines from the current line
            start=(record.lineno -1) - 2
            end=(record.lineno -1) + 2
            if record.lineno == len(lines):
                end = record.lineno-1
            if end > len(lines)-1:
                end = len(lines)-1
            if record.lineno -1 == 0:
                start = 0
            if start < 0:
                start = 0
            code = ''.join(lines[start:end+1]) #lines[start:length]
        except Exception as e:
            code = str(e)
        record.codelines = code
        record.topline = "--------------------------------------------------------------------------------------------------------------"
        record.botline = "--------------------------------------------------------------------------------------------------------------"
        return super(Formatter, self).format(record)


class SQLFormatter(Formatter):
    def format(self, record):


        # Check if sqlparse is available for indentation
        try:
            import sqlparse
        except ImportError:
            sqlparse = None

        # Remove leading and trailing whitespaces
        sql = record.sql.strip()

        if sqlparse:
            # Indent the SQL query
            sql = sqlparse.format(sql, reindent=True)

        # Set the record's statement to the formatted query
        record.statement = sql
        if 'duration' in record.__dict__:
          pass
        else:
          record.duration = "NA"
        return super(SQLFormatter, self).format(record)

def create_logger(task_id,task_name=""):
    import pathlib
    import logging
    from logging.handlers import RotatingFileHandler
    import os
    import sys
    logger = logging.getLogger('normal_logger') # root logger
    logger.setLevel(logging.INFO)
    for hdlr in logger.handlers[:]:  # remove all old handlers
        logger.removeHandler(hdlr)

    proj_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    # i.e src
    dir1  = f"{proj_path}/../../LOGS"
    dir2  = f"{LOG_DIRECTORY}/{task_name}"

    file1 = task_id+".log"
    filename1 = os.path.join(dir1,dir2,file1)
    #print(filename1)

    # Create the rotating file handler. Limit the size to 1000000Bytes ~ 1MB .
    handler = RotatingFileHandler(filename1, mode='a', maxBytes=1000000, backupCount=1, encoding='utf-8', delay=0)
    #handler = logging.FileHandler(filename1,mode='w')
    #handler = logging.StreamHandler()

    #%(pathname)s[:%(lineno)s] %(name)s\n -- %(absolute_path)s\n%(topline)s\n\n%(codelines)s\n\n%(message)s"
    handler.setFormatter(Formatter("\n%(asctime)s::::::::::::::::::::%(levelname)-8s\n%(pathname)s ::: Logger:: %(name)s\n[%(filename)s:%(lineno)s - %(funcName)30s() ]\n%(topline)s\n\n%(codelines)s\n\n%(message)s"))
    handler.setLevel(logging.INFO)
    logger.addHandler(handler)

    logger.info("LOGGER CREATED NORMAL")

def addhandlertobackendlogging(task_id,task_name=""):
    import pathlib
    import logging
    from logging.handlers import RotatingFileHandler
    import os
    import sys
    logger = logging.getLogger("django.db.backends")
    #logger = logging.getLogger("test")
    logger.setLevel(logging.DEBUG)
    for hdlr in logger.handlers[:]:  # remove all old handlers
        logger.removeHandler(hdlr)
    for filter in logger.filters[:]:  # remove all old handlers
        logger.removeFilter(filter)

    logger.handlers.clear()

    proj_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    # i.e src
    dir1  = f"{proj_path}/../../LOGS"
    dir2  = f"{LOG_DIRECTORY}/{task_name}"

    file1 = task_id+".log"
    filename1 = os.path.join(dir1,dir2,file1)
    #print(filename1)

    # Create the rotating file handler. Limit the size to 1000000Bytes ~ 1MB .
    #handler = RotatingFileHandler(filename1, mode='a', maxBytes=1000000, backupCount=1, encoding='utf-8', delay=0)
    handler = logging.FileHandler(filename1,mode='a')
    #handler = logging.StreamHandler()

    # SET HANDLER FORMATTER AND LEVEL
    handler.setFormatter(SQLFormatter('\n%(asctime)s:::::::::SQL:::::::::::%(levelname)-1s\n[%(duration).3f]\n%(statement)s'))
    handler.setLevel(logging.DEBUG)
    logger.addHandler(handler)


def addhandlertorequestlogging(task_id,task_name=""):
    import pathlib
    import logging
    from logging.handlers import RotatingFileHandler
    import os
    import sys

    import requests
    import http.client as http_client
    http_client.HTTPConnection.debuglevel = 1

    def print_to_log(*args):
        logging.getLogger("urllib3").debug(" ".join(args))
    http_client.print = print_to_log


    #logger = logging.getLogger("requests.packages.urllib3")
    logger = logging.getLogger("urllib3")
    #logger = logging.getLogger("test")
    logger.setLevel(logging.DEBUG)
    logger.propagate = False
    for hdlr in logger.handlers[:]:  # remove all old handlers
        logger.removeHandler(hdlr)
    for filter in logger.filters[:]:  # remove all old handlers
        logger.removeFilter(filter)

    logger.handlers.clear()


    proj_path = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    # i.e src
    dir1  = f"{proj_path}/../../LOGS"
    dir2  = f"{LOG_DIRECTORY}/{task_name}"

    file1 = task_id+".log"
    filename1 = os.path.join(dir1,dir2,file1)
    #print(filename1)

    # Create the rotating file handler. Limit the size to 1000000Bytes ~ 1MB .
    #handler = RotatingFileHandler(filename1, mode='a', maxBytes=1000000, backupCount=1, encoding='utf-8', delay=0)
    handler = logging.FileHandler(filename1,mode='a')
    #handler = logging.StreamHandler()

    # SET HANDLER FORMATTER AND LEVEL
    handler.setFormatter(Formatter("%(asctime)s::%(levelname)-0s::%(message)s"))
    handler.setLevel(logging.DEBUG)
    logger.addHandler(handler)
```


and then in the tasks.py

```
import logging
import pytz
import datetime
from boiler.logging_for_celery import create_logger, addhandlertorequestlogging, addhandlertobackendlogging
logger = logging.getLogger()

from boiler.settings import pp_odir_getobject

def get_logger_celery():
    global logger
    from celery._state import get_current_task

    try:
        from celery._state import get_current_task
        get_current_task_1 = get_current_task
    except ImportError:
        get_current_task_1 = lambda: None

    task = get_current_task_1()
    
    if task and task.request:
        print(json.dumps(pp_odir_getobject(task),default=str,indent=4))
        print(json.dumps(pp_odir_getobject(task.request),default=str,indent=4))
        print("TRUE CELERY TASK")
        ########## INTIALIZING ##################
        ## Time at which the cron job is started
        task_name = task.name
        task_id= task.request.id
        print(f"task.name :: {task_name}")
        print(f"task.request.id :: {task_id}")

        create_logger(task_id,task_name)
        addhandlertorequestlogging(task_id,task_name)
        addhandlertobackendlogging(task_id,task_name) #THIS IS NEEDS TO BE RUN AGAIN WHEN DJANGO IS IMPORTED. 
        # WHEN IMPORTING DJANG IT WILL RESET THIS LOGGER
        logger = logging.getLogger("normal_logger")
    print(logger.handlers)
    print(logging.getLogger("django.db.backends").handlers)
    print(logging.getLogger("urllib3").handlers)


@celery_app.task
def add(x, y):
    get_logger_celery()

    logger.info("Testing")

    hare = User.objects.all()

    logger.info("QUERY")
    for h in hare:
        pass

    logger.info("REQUESTS")
    requests.get("http://google.com")
    
    # also call outside function of task
    function_outside()
    
    return x * y


def function_outside():
   get_logger_celery()
   # we want this logger to be handled differently when called using celery task
   # and called by any other Django views. 
   # Basically get_logger_add() does that. It will check if celery task assign logger to customization
   # else it will keep it as it is
   logger.info("testing")
```

# python global and local variables inside function and class.



https://stackoverflow.com/questions/10814452/how-can-i-access-global-variable-inside-class-in-python

```
g_c = 0
print ("Initial value of g_c: " + str(g_c))
print("Variable defined outside of method automatically global? "
      + str("g_c" in globals()))

class TestClass():
    def direct_print(self):
        print("Directly printing g_c without declaration or modification: "
              + str(g_c))
        #Without any local reference to the name
        #Python defaults to search for the variable in globals()
        #This of course happens for all the module names you import

    def mod_without_dec(self):
        g_c = 1
        #A local assignment without declaring reference to global variable
        #makes Python default to access local name
        print ("After mod_without_dec, local g_c=" + str(g_c))
        print ("After mod_without_dec, global g_c=" + str(globals()["g_c"]))


    def mod_with_late_dec(self):
        g_c = 2
        #Even with a late declaration, the global variable is accessed
        #However, a syntax warning will be issued
        global g_c
        print ("After mod_with_late_dec, local g_c=" + str(g_c))
        print ("After mod_with_late_dec, global g_c=" + str(globals()["g_c"]))

    def mod_without_dec_error(self):
        try:
            print("This is g_c" + str(g_c))
        except:
            print("Error occured while accessing g_c")
            #If you try to access g_c without declaring it global
            #but within the method you also alter it at some point
            #then Python will not search for the name in globals()
            #!!!!!Even if the assignment command occurs later!!!!!
        g_c = 3

    def sound_practice(self):
        global g_c
        #With correct declaration within the method
        #The local name g_c becomes an alias for globals()["g_c"]
        g_c = 4
        print("In sound_practice, the name g_c points to: " + str(g_c))


t = TestClass()
t.direct_print()
t.mod_without_dec()
t.mod_with_late_dec()
t.mod_without_dec_error()
t.sound_practice()
```

# how to debug celery using ipdb

celery offers officially rdb and telnet

https://medium.com/@kennethjiang/debug-celery-tasks-in-ipdb-6f71506e6430

but we want to use ipdb

so use apply() instead of delay()


# How to run a script inside IPython

```
import os
filepath='C:\\Users\\User\\FolderWithPythonScript' 
os.chdir(filepath)
%run pyFileInThatFilePath.py
```
OR

```
%run ./my_script.py
```

# python know current directory

```
To get the current working directory use

import os
cwd = os.getcwd()
```

To get the full path to the directory a Python file is contained in, write this in that file:
```
import os 
dir_path = os.path.dirname(os.path.realpath(__file__))
```

# How to use a variable inside a regular expression?

https://stackoverflow.com/a/55810892

From python 3.6 on you can also use [Literal String Interpolation][1], "f-strings". In your particular case the solution would be:

    if re.search(rf"\b(?=\w){TEXTO}\b(?!\w)", subject, re.IGNORECASE):
        ...do something

EDIT:

Since there have been some questions in the comment on how to deal with special characters I'd like to extend my answer:

**raw strings ('r'):**

One of the main concepts you have to understand when dealing with special characters in regular expressions is to distinguish between string literals and the regular expression itself. It is very well explained [here][2]: 

In short:

Let's say instead of finding a word boundary `\b` after `TEXTO` you want to match the string `\boundary`. The you have to write:

    TEXTO = "Var"
    subject = r"Var\boundary"
    
    if re.search(rf"\b(?=\w){TEXTO}\\boundary(?!\w)", subject, re.IGNORECASE):
        print("match")

This only works because we are using a raw-string (the regex is preceded by 'r'), otherwise we must write "\\\\\\\\boundary" in the regex (four backslashes). Additionally, without '\r', \b' would not converted to a word boundary anymore but to a backspace!

**re.escape**:

Basically puts a backspace in front of any special character. Hence, if you expect a special character in TEXTO, you need to write:

    if re.search(rf"\b(?=\w){re.escape(TEXTO)}\b(?!\w)", subject, re.IGNORECASE):
        print("match")

NOTE: For any version >= python 3.7: `!`, `"`, `%`, `'`, `,`, `/`, `:`, `;`, `<`, `=`, `>`, `@`, and `` ` `` are not escaped. Only special characters with meaning in a regex are still escaped. `_` is not escaped since Python 3.3.(s. [here][3])

**Curly braces:**

If you want to use quantifiers within the regular expression using f-strings, you have to use double curly braces. Let's say you want to match TEXTO followed by exactly 2 digits:

    if re.search(rf"\b(?=\w){re.escape(TEXTO)}\d{{2}}\b(?!\w)", subject, re.IGNORECASE):
        print("match")


  [1]: https://www.python.org/dev/peps/pep-0498/
  [2]: https://docs.python.org/3/howto/regex.html#the-backslash-plague
  [3]: https://docs.python.org/3/library/re.html#re.escape


# match a string from a list in python

Use re.search function along with the list comprehension.
```
>>> teststr = ['1 FirstString', '2x Sec String', '3rd String', 'x forString', '5X fifth']
>>> [i for i in teststr if re.search(r'\d+[xX]', i) ]
['2x Sec String', '5X fifth']
```


# celery calling a celery task from another celery task as normal function

```
@celery.task
def task1()
    task2()
    
@celery.task
def task2()
    pass
```
this is not the proper way, task2 will be created as a dangling task, no task id


the proper way is use task2.run() (then task2 is run in the task of task1)
```
@celery.task
def task1()
    task2.run()
    
@celery.task
def task2()
    pass
```

# Another way of Django ipd docker
https://gist.githubusercontent.com/katylava/3559c29160573488a7bbccb474b55356/raw/aa2da70090da1069e06c8eaadb445faabcc9697e/README.md
## With `docker-compose up`

```
$ docker-compose up
Starting dockeripdb_web_1
Attaching to dockeripdb_web_1

# ...After loading http://192.168.99.100:8000 in browser...

web_1  | Performing system checks...
web_1  |
web_1  | System check identified no issues (0 silenced).
web_1  | August 07, 2017 - 19:58:48
web_1  | Django version 1.11.3, using settings None
web_1  | Starting development server at http://0.0.0.0:8000/
web_1  | Quit the server with CONTROL-C.
web_1  | > /dockeripdb/app.py(23)index()
web_1  |      22     import ipdb; ipdb.set_trace()
web_1  | ---> 23     return HttpResponse('Hello World')
web_1  |      24
web_1  |
web_1  | ipdb> Internal Server Error: /
web_1  | Traceback (most recent call last):
web_1  |   File "/usr/local/lib/python3.5/site-packages/django/core/handlers/exception.py", line 41, in inner
web_1  |     response = get_response(request)
web_1  |   File "/usr/local/lib/python3.5/site-packages/django/core/handlers/base.py", line 249, in _legacy_get_response
web_1  |     response = self._get_response(request)
web_1  |   File "/usr/local/lib/python3.5/site-packages/django/core/handlers/base.py", line 185, in _get_response
web_1  |     response = wrapped_callback(request, *callback_args, **callback_kwargs)
web_1  |   File "/usr/local/lib/python3.5/site-packages/django/core/handlers/base.py", line 185, in _get_response
web_1  |     response = wrapped_callback(request, *callback_args, **callback_kwargs)
web_1  |   File "app.py", line 23, in index
web_1  |     return HttpResponse('Hello World')
web_1  |   File "app.py", line 23, in index
web_1  |     return HttpResponse('Hello World')
web_1  |   File "/usr/local/lib/python3.5/bdb.py", line 48, in trace_dispatch
web_1  |     return self.dispatch_line(frame)
web_1  |   File "/usr/local/lib/python3.5/bdb.py", line 67, in dispatch_line
web_1  |     if self.quitting: raise BdbQuit
web_1  | bdb.BdbQuit
```

## With `docker-compose run --service-ports web`

```
$ docker-compose run --service-ports web
Performing system checks...

System check identified no issues (0 silenced).
August 07, 2017 - 20:01:33
Django version 1.11.3, using settings None
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.

# ...After loading http://192.168.99.100:8000 in browser...

> /dockeripdb/app.py(23)index()
     22     import ipdb; ipdb.set_trace()
---> 23     return HttpResponse('Hello World')
     24

ipdb>
```

But instead of this use stdin in yml file and then docker attach

But this gives how to use it with run

# How can I avoid “Using selector: EpollSelector” log message in Django?

https://stackoverflow.com/questions/60503705/how-can-i-avoid-using-selector-epollselector-log-message-in-django

This message is from the [`asyncio`][1] library that comes with Python 3. You can configure its logging by modifying the [`LOGGING`][2] configuration:

```
LOGGING = {
    'version': 1,
    'loggers': {
        'asyncio': {
            'level': 'WARNING',
        },
    },
}
```

If you're not using Django, you can use this line of code:

```
import logging
logging.getLogger('asyncio').setLevel(logging.WARNING)
```

  [1]: https://docs.python.org/3/library/asyncio.html
  [2]: https://docs.djangoproject.com/en/stable/ref/settings/#std:setting-LOGGING


# how to save previos value of select
https://stackoverflow.com/a/4076852
```
$(document).ready(function(){
  var sel = $("#sel");
  sel.data("prev",sel.val());

  sel.change(function(data){
     var jqThis = $(this);
     alert(jqThis.data("prev"));
     jqThis.data("prev",jqThis.val());
  });
});
```


# how to use vars or __dict__ or vars  

```python
vars(Form) is same as Form.__dict__

it retuns a mappingdict

ipdb> Form.__dict__                                                                                                                                                 
mappingproxy({'declared_fields': {'id': <django.forms.fields.DecimalField object at 0x7fdff9c9a160>, 'ids': <django_filters.filters.BaseCSVFilter.__init__.<locals>.ConcreteCSVField object at 0x7fdff90fa5c0>, 'ordering': <django.forms.fields.CharField object at 0x7fdff923be10>, 'auto_complete': <django.forms.fields.CharField object at 0x7fdff923b198>, 'any_field': <django.forms.fields.CharField object at 0x7fdff923b320>, 'role': <django.forms.fields.CharField object at 0x7fdff923b2b0>}, '__module__': 'django.forms.widgets', '__doc__': None, 'media': <property object at 0x7fdff932c3b8>, 'base_fields': {'id': <django.forms.fields.DecimalField object at 0x7fdff9c9a160>, 'ids': <django_filters.filters.BaseCSVFilter.__init__.<locals>.ConcreteCSVField object at 0x7fdff90fa5c0>, 'ordering': <django.forms.fields.CharField object at 0x7fdff923be10>, 'auto_complete': <django.forms.fields.CharField object at 0x7fdff923b198>, 'any_field': <django.forms.fields.CharField object at 0x7fdff923b320>, 'role': <django.forms.fields.CharField object at 0x7fdff923b2b0>}})

ipdb> type(Form.__dict__)                                                                                                                                           
<class 'mappingproxy'>

# convert to dict

ipdb> dict(Form.__dict__)

then use import json; print(json.dumps(dict(Form.__dict__),indent=4,default=str))


```

## But __dict__ and vars miss some variables

so we have to use dir(obj)
```python
import json; print(json.dumps(dict( (key, getattr(OBJREPLACE, key) ) for key in dir(OBJREPLACE) ),indent=4,default=str))
```
but we dont want to see "__" variables so use

```python
import json; print(json.dumps(dict((key, getattr(filter_, key)) if not key.startswith("__") else (1,1) for key in dir(filter_)),indent=4,default=str))
```

Note: `else (1,1)` is just anything. we have to show else


## DJango ipdb does not stop 

https://stackoverflow.com/a/28277178/2897115

I've been through the same problem.

Try something like `python -m pdb ./manage.py runserver --nothreading --noreload 127.0.0.1:8080`. It solved the issue for me.

It seems that breakpoints with PDB are thread-specific, and the `--nothreading` and `--noreload` options are necessary to avoid some forking that may confuse PDB. This is also why `set_trace` works, as it's called directly inside the thread of interest.

What worked for me is

```python
python manage.py runserver  --nothreading 0.0.0.0:8009
```


## Django how to use group by

https://hakibenita.com/django-group-by-sql



## create dictionary from list of variables
https://stackoverflow.com/questions/9495262/create-dictionary-from-list-of-variables

```python
pip install sorcery
```

```python
from sorcery import dict_of

a = 1
b = 2
c = 3
d = dict_of(a, b, c)
print(d)
# {'a': 1, 'b': 2, 'c': 3}
```

# HOW to access website on localhost from outside
# ngrok

use ngrok to show someone our webapplication from the pc

https://stackoverflow.com/a/54679176/2897115

for this all the django urls should start with /api

and also

```
STATIC_URL = "/api/static/"

MEDIA_URL = "/api/media/"
```
and in nginx use

```
upstream webapp {
    server webapp:8000;
}

upstream nodejs {
    server node:3000;
}

server {
    listen 80;

    location / {
        proxy_pass http://nodejs;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }

    location /api {
        proxy_pass http://webapp;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }

}
```

and then run ngrok 

```
  ngrok:
    image: wernight/ngrok:latest
    ports:
      - 4040:4040
    environment:
      NGROK_PROTOCOL: http
      NGROK_PORT: nginx:80
      NGROK_AUTH: "1rsPdDdjitZKvEuPGGN3QzX9pmx_7vBUN76poPdd7voB9sUXQ" # get the token https://dashboard.ngrok.com/get-started/your-authtoken
      NGROK_REGION: "ap"
    depends_on:
      - nginx
    networks:
      - nginx_network
```

But django to serve static and media files

add this

```
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

and also make all urls begin with /api

```
from django.contrib import admin
from django.urls import path, include
from rest_framework import routers
from django.urls import re_path
from django.conf.urls import url
from django.views.generic import TemplateView
from django.views.generic.base import RedirectView

from main.api import RegisterAPI, LoginAPI, UserAPI
from knox import views as knox_views

from main import views

from django.conf import settings
from django.conf.urls.static import static

router = routers.DefaultRouter()
router.register(r"profiles", views.UserProfileViewSet)


urlpatterns = [
    path("api/dmin/", admin.site.urls),
    path("api/index/", TemplateView.as_view(template_name="index.html")),
    path("api/restauth/", include("rest_framework.urls", namespace="restauth")),
    path("api/", include(router.urls)),
    path("api/auth", include("knox.urls")),
    path("api/auth/register", RegisterAPI.as_view()),
    path("api/auth/login", LoginAPI.as_view()),
    path("api/auth/user", UserAPI.as_view()),
    path("api/auth/logout", knox_views.LogoutView.as_view(), name="knox_logout"),
    path(
        "api/password_reset/",
        include("django_rest_passwordreset.urls", namespace="password_reset"),
    ),
    url(r"api/^(?:.*)/?$", TemplateView.as_view(template_name="index.html")),
    # path(
    #     "passwordreset/verifytoken/",
    #     views.CustomPasswordTokenVerificationView.as_view(),
    #     name="password_reset_verify_token",
    # ),
]
```

in reactjs use in index.js as

```
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import * as serviceWorker from "./serviceWorker";

// SUGGESTION BEGINS: TO ADD THIS

import axios from 'axios';

axios.defaults.baseURL = `http://${window.location.hostname}`

// SUGGESTION ENDS: TO ADD THIS

ReactDOM.render(
  <React.Fragment>
    <App />
  </React.Fragment>,
  document.getElementById("root")
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

and final docker file
```
version: "3.7"
services:

  nginx:
    image: nginx:1.18.0-alpine
    ports:
      - 8000:80
    volumes:
      - ./nginx/localhost/conf.d:/etc/nginx/conf.d
    depends_on:  # <-- wait for webapp to be "ready" before starting this service
      - webapp
      - node
    networks:  # connect to the bridge
      - nginx_network


  postgresql:
    image: "postgres:12-alpine"
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_postgres_data
        target: /var/lib/postgresql/data
    environment:
      POSTGRES_USER: 'admin' # this is optional because default it posstgres
      POSTGRES_PASSWORD: 'admin'
      POSTGRES_DB: 'elemzy' # this is optional because default it postgres
      PGDATA: '/var/lib/postgresql/data/pgdata'
    networks:  # connect to the bridge
      - postgresql_network
    command: ["postgres", "-c", "log_statement=all","-c", "log_destination=stderr"]


  webapp:
    #image: "django:python-3.7.7-alpin3.11-with-builddeps"
    image: "python-node-buster:nikolaik-python3.7-nodejs15"
    environment:
      - SQLPRINT=1
      - DEBUG=1
      - WERKZEUG_DEBUG_PIN=off
      - POSTGRES_REMOTE=
      - PYTHONBREAKPOINT=ipdb.set_trace
    volumes:
      - type: bind
        source: ./python_django/Django_project_and_venv
        target: /home/simha/app
      - type: bind
        source: ./python_django/Pipenv_cache_directory/.cache
        target: /home/simha/.cache
      - type: bind # .cache of pipenv will avoid to download the .whl files again
        source: ./python_django/Pipenv_cache_directory/.cache/pip-tools
        target: /home/simha/.cache/pip-tools
      - type: bind # .cache of pipenv will avoid to download the .whl files again
        source: ./python_django/Pipenv_cache_directory/.cache/pipenv
        target: /home/simha/.cache/pipenv
      - type: bind # .cache of pip will avoid download whl files again  
        source: ./python_django/Pip_cache/.cache/pip
        target: /home/simha/.cache/pip
      - type: bind # .cache of pip will avoid download whl files again
        source: ../DO_NOT_DELETE_LOGS/DJANGO
        target: /home/simha/LOGS
      - type: bind # .cache of pip will avoid download whl files again
        source: ../DO_NOT_DELETE_MEDIA_DJANGO
        target: /home/simha/app/src/media
############################## ********** APP SPECIFIC  ******** #########################
      - type: bind # .cache of pip will avoid download whl files again  
        source: ./python_django/Django_external_config
        target: /home/simha/app/src/reon/external_config
    ports:
      - "8001:8000"
    command:
      - sh
      - -c
      - |
        cd src/
        pipenv run python manage.py runserver 0.0.0.0:8000
    stdin_open: true   # Add this line into your service
    tty: true   # Add this line into your service
    networks:
      - postgresql_network
      - nginx_network
    depends_on:
      - postgresql


  jupyter:
    # Jupyter needs buildversion: Error loading shared library libzmq.so.5
    image: "python-node-buster:nikolaik-python3.7-nodejs15"
    environment:
      - SQLPRINT=1
      - JUPYTER_PASS=1
      - DEBUG=1
      - POSTGRES_REMOTE=0
      - PYTHONBREAKPOINT=ipdb.set_trace
    #image: "django:python-3.7.7-alpin3.11"
    volumes:
      - type: bind
        source: ./python_django/Django_project_and_venv
        target: /home/simha/app
      - type: bind
        source: ./python_django/Pipenv_cache_directory/.cache
        target: /home/simha/.cache
      - type: bind # We want to also set some configurations for jupyter
        source: ./python_django/jupyter/.jupyter
        target: /home/simha/.jupyter
      - type: bind # .cache of pipenv will avoid to download the .whl files again
        source: ./python_django/Pipenv_cache_directory/.cache/pip-tools
        target: /home/simha/.cache/pip-tools
      - type: bind # .cache of pipenv will avoid to download the .whl files again
        source: ./python_django/Pipenv_cache_directory/.cache/pipenv
        target: /home/simha/.cache/pipenv
      - type: bind # .cache of pip will avoid download whl files again
        source: ./python_django/Pip_cache/.cache/pip
        target: /home/simha/.cache/pip
      - type: bind # .cache of pip will avoid download whl files again
        source: ../DO_NOT_DELETE_LOGS/DJANGO
        target: /home/simha/LOGS
      - type: bind # .cache of pip will avoid download whl files again
        source: ../DO_NOT_DELETE_MEDIA_DJANGO
        target: /home/simha/app/src/media
############################## ********** APP SPECIFIC  ******** #########################
      - type: bind # .cache of pip will avoid download whl files again  
        source: ./python_django/Django_external_config
        target: /home/simha/app/src/reon/external_config
      # NOTE we have to import the .env from the host. This is for safety purpose 
    ports:
      - "8888:8888"
    command:
      - sh
      - -c
      - |
        cd src/
        pipenv run python manage.py shell_plus --notebook
    networks:
      - postgresql_network
    depends_on:
      - postgresql



  pgadmin:
    image: dpage/pgadmin4:5.2
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
      PGADMIN_LISTEN_PORT: 80
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_pgadmin_data
        target: /var/lib/pgadmin
    ports:
      - "8080:80"
    networks:
      - postgresql_network


  node:
    image: "python-node-buster:nikolaik-python3.7-nodejs15"
    volumes:
      - type: bind
        source: ./node_reacts/reactjs_app
        target: /home/simha/app
    ports:
      - "3000:3000"
    stdin_open: true  #https://stackoverflow.com/a/60902143/2897115
    command:
      - sh
      - -c
      - |
        npm start
    networks:
      - nginx_network


  ngrok:
    image: wernight/ngrok:latest
    ports:
      - 4040:4040
    environment:
      NGROK_PROTOCOL: http
      NGROK_PORT: nginx:80
      NGROK_AUTH: "XXXXXXXXXX" # get the token https://dashboard.ngrok.com/get-started/your-authtoken
      NGROK_REGION: "ap"
    depends_on:
      - nginx
    networks:
      - nginx_network

networks:
  postgresql_network:
    driver: bridge
  nginx_network:
    driver: bridge
```

## Specify an SSH key for git push for a given domain
https://stackoverflow.com/a/62278407/2897115

Configure your repository using `git config`

```
git config --add --local core.sshCommand 'ssh -i <<<PATH_TO_SSH_KEY>>>'
```
This applies to your *local repository* only.

![](https://i.imgur.com/cejrX4w.png)
		       
		       
		       
# Bootstrap 4 correct way to use row and col classes [duplicate]
		       
https://stackoverflow.com/a/49187634/2897115

> For the second row instead of that should I have to wrap that button inside a column. Like this

Yes, only a Bootstrap column is allowed to be a direct child of a Bootstrap row.

So, in every Bootstrap row, you **must have at least one Bootstrap column** and all of your content must go into Bootstrap columns and never into Bootstrap rows directly.

This is because Bootstrap rows and columns are designed to work in pairs i.e. no content may ever be placed directly into a Bootstrap row. Only Bootstrap columns may be direct children of Bootstrap rows.

Reference: 

https://getbootstrap.com/docs/4.0/layout/grid/



# python and Django:

Python >= 3.6 installed on your machine. Django 3.0 is only compatible with Python 3.6 and up because it makes use of the async and await keywords.
	
	
# python run from subfolder without changing the urls
	
i.e localhost:8000/django/
	
## docker compose file
	
```
# My version of docker = 18.09.4-ce
# Compose file format supported till version 18.06.0+ is 3.7
version: "3.7"
services:
  nginx:
    image: nginx:1.18.0-alpine
    ports:
      - 8025:80
    volumes:
      - ./nginx/localhost/conf.d:/etc/nginx/conf.d
      - ../DO_NOT_DELETE_CODING_FOLDER/backend_django/staticfiles:/staticfiles
      - ../DO_NOT_DELETE_MEDIA_DJANGO:/mediafiles
    depends_on:
      - webapp
    networks:
      - nginx_network

  postgresql:
    image: "postgres:13-alpine"
    restart: always
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_postgres_data
        target: /var/lib/postgresql/data
    environment:
      POSTGRES_DB: gauranga
      POSTGRES_USER: simha
      POSTGRES_PASSWORD: krishna
      PGDATA: "/var/lib/postgresql/data/pgdata"
    networks:
      - postgresql_network

  phppgadmin:
    image: "bitnami/phppgadmin:7.13.0"
    environment:
      DATABASE_HOST: "postgresql"
      DATABASE_SSL_MODE: "disable"
    networks:
      - nginx_network
      - postgresql_network

  redis:
    image: "redis:5.0.9-alpine3.11"
    command: redis-server
    environment:
      - REDIS_REPLICATION_MODE=master
    networks: # connect to the bridge
      - redis_network

  celery_worker:
    image: "python3.9-nodejs16-buster:nikolaik-python3.9-nodejs16"
    environment:
      - SQLPRINT=1
      - DEBUG=1
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_CODING_FOLDER/backend_django
        target: /home/simha/app
      ############################## ********** APP SPECIFIC  ******** #########################
      # ensure external_config folder exists on host else it will create folder with root:root on the host
      # but on the docker it will be created using simha:users
      - type: bind
        source: ./python_django/Django_external_config
        target: /home/simha/app/petsproject/external_config
    command:
      - sh
      - -c
      - |
        pipenv run celery -A petsproject worker --loglevel=debug #ensure redis-server is running in root and change backed to respective
      #pipenv run watchmedo auto-restart --directory=./ --pattern=*.py --recursive -- celery -A boiler worker --concurrency=1 --loglevel=DEBUG
      # https://www.distributedpython.com/2019/04/23/celery-reload/
      # https://gist.github.com/jsheedy/fda57e82c27f612d9aa875d9d869003f
      #pipenv run celery -A boiler worker --loglevel=debug #ensure redis-server is running in root and change backed to respective
    depends_on: # wait for postgresql, redis to be "ready" before starting this service
      - redis
      - postgresql
    networks: # connect to the bridge
      - redis_network
      - postgresql_network

  webapp:
    image: "python3.9-nodejs16-buster:nikolaik-python3.9-nodejs16"
    environment:
      - SQLPRINT=1
      - DEBUG=1
      - WERKZEUG_DEBUG_PIN=off
      - PYTHONBREAKPOINT=ipdb.set_trace
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_CODING_FOLDER/backend_django
        target: /home/simha/app
      ############################## ********** APP SPECIFIC  ******** #########################
      # ensure external_config folder exists on host else it will create folder with root:root on the host
      # but on the docker it will be created using simha:users
      - type: bind
        source: ./python_django/Django_external_config
        target: /home/simha/app/petsproject/external_config
    command:
      - sh
      - -c
      - |
        pipenv run python manage.py runserver_plus 0.0.0.0:8000
    depends_on:
      - postgresql
      - celery_worker
    stdin_open: true # Add this line into your service
    tty: true # Add this line into your service
    networks:
      - postgresql_network
      - nginx_network

  jupyter:
    image: "python3.9-nodejs16-buster:nikolaik-python3.9-nodejs16"
    environment:
      - SQLPRINT=1
      - JUPYTER_PASS=1
      - DEBUG=1
      - PYTHONBREAKPOINT=ipdb.set_trace
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_CODING_FOLDER/backend_django
        target: /home/simha/app
      - type: bind
        source: ./python_django/jupyter/.jupyter
        target: /home/simha/.jupyter
        # ensure jupyter_related folder exists on host else it will create folder with root:root on the host
        # but on the docker it will be created using simha:users
      - type: bind
        source: ../DO_NOT_DELETE_JUPYTER_NOTEBOOKS
        target: /home/simha/app/jupyter_related
      ############################## ********** APP SPECIFIC  ******** #########################
      # ensure external_config folder exists on host else it will create folder with root:root on the host
      # but on the docker it will be created using simha:users
      - type: bind
        source: ./python_django/Django_external_config
        target: /home/simha/app/petsproject/external_config
    depends_on:
      - postgresql
      - celery_worker
    command:
      - sh
      - -c
      - |
        pipenv run python manage.py shell_plus --notebook
    networks:
      - postgresql_network
      - nginx_network

  node:
    image: "python3.9-nodejs16-buster:nikolaik-python3.9-nodejs16"
    volumes:
      - type: bind
        source: ../DO_NOT_DELETE_CODING_FOLDER/frontend_reactjs_dash
        target: /home/simha/app
    depends_on: # wait for celery, postgresql, redis to be "ready" before starting this service
      - webapp
    networks:
      - nginx_network
    ports:
      - "3025:3000"
    stdin_open: true #https://stackoverflow.com/a/60902143/2897115
    command:
      - sh
      - -c
      - |
        npm start

  # also set up ngninx and reactjs axios accordingly
  # https://stackoverflow.com/a/63139550/2897115
  ngrok:
    image: wernight/ngrok:latest
    ports:
      - 4030:4040
    environment:
      NGROK_PROTOCOL: http
      NGROK_PORT: nginx:80
      NGROK_AUTH: "1rsPdDdjitZKvEuPGGN3QzX9pmx_7vBUN76poPdd7voB9sUXQ" # get the token https://dashboard.ngrok.com/get-started/your-authtoken
      NGROK_REGION: "ap"
    depends_on:
      - nginx
    networks:
      - nginx_network

networks:
  postgresql_network:
    driver: bridge
  redis_network:
    driver: bridge
  nginx_network:
    driver: bridge

```
	
# nginx default.conf

```
upstream webapp {
    server webapp:8000;
}

upstream jupyter {
    server jupyter:8888;
}

upstream db {
    server phppgadmin:8080;
}

upstream node {
    server node:3000;
}


# https://stackoverflow.com/a/54679176/2897115
# multiple ports on ngrok
server {
    listen 80;

    location / {
        proxy_pass http://node;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
    }

    # https://ruddra.com/deploy-django-subpath-openshift/
    # https://stackoverflow.com/a/47945170/2897115
    # Here is the important part
    location /django {
        proxy_pass http://webapp;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-Script-Name /django;
        proxy_cookie_path / /django;
    }


}


# For normal django access using api. subdomain
server {
    listen 80;

    server_name api.*;

    location / {
        proxy_pass http://webapp;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        # https://serverfault.com/a/993559
        #proxy_read_timeout 1800;
        #proxy_connect_timeout 1800;
        #proxy_send_timeout 1800;
        #send_timeout 1800;
    }
}


#    location /static {
#        autoindex on;
#        alias /staticfiles/;
#    }
#
#    location /media {
#        autoindex on;
#        alias /mediafiles/;
#    }


server {
    listen 80;

    server_name db.*;

    location / {
        proxy_pass http://db;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        #proxy_read_timeout 99999;
        #proxy_connect_timeout 99999;
        #proxy_send_timeout 99999;
        #send_timeout 99999;
    }

}



map $http_upgrade $connection_upgrade {
    default upgrade;
    ''      close;
}

server {
    listen 80;

    server_name jyp.*;

    location / {
        # or whichever port you've set for your Jupyter
        proxy_pass http://jupyter;
        # $http_host is important for accessing Jupyter locally
        proxy_set_header Host $http_host;
        # http://nginx.org/en/docs/http/websocket.html
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
    }
}
```

# django settings.py 
	
```
FORCE_SCRIPT_NAME = '/django'  # without trailing slash
```

```
"""
Django settings for petsproject project.

Generated by 'django-admin startproject' using Django 3.1.

For more information on this file, see
https://docs.djangoproject.com/en/3.1/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/3.1/ref/settings/
"""

from pathlib import Path
from datetime import timedelta
import os

# install snoop for this
# https://github.com/alexmojaki/snoop
import snoop
from cheap_repr import find_repr_function
import six


# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve(strict=True).parent.parent


# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = "kjyj$22$3*le0&v)0q-=yukolocqe+f19^=$125q^*6aj=u^+-"

# SECURITY WARNING: don't run with debug turned on in production!

# we will check the environ variable if defined
try:
    if os.environ["DEBUG"] == "1":
        DEBUG = True
    else:
        DEBUG = False
except Exception as e:
    print(str(e))
    DEBUG = True

ALLOWED_HOSTS = ["*"]

# Application definition

INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "all_models",
    # third party
    "rest_framework",
    "rest_framework.authtoken",
    "dj_rest_auth",
    "django.contrib.sites",
    "allauth",
    "allauth.account",
    "dj_rest_auth.registration",
    "allauth.socialaccount",
    "corsheaders",
]

# required for 'django.contrib.sites' which is required by rest-auth or all-auth
SITE_ID = 2

REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": ("dj_rest_auth.jwt_auth.JWTCookieAuthentication",)
}

REST_USE_JWT = True
JWT_AUTH_COOKIE = "jwt-access-token"  # you can set these
JWT_AUTH_REFRESH_COOKIE = "jwt-refresh-token"  # to anything

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(seconds=5),
    "REFRESH_TOKEN_LIFETIME": timedelta(minutes=60),
}

ACCOUNT_USER_MODEL_USERNAME_FIELD = None
ACCOUNT_EMAIL_REQUIRED = True
ACCOUNT_UNIQUE_EMAIL = True
ACCOUNT_USERNAME_REQUIRED = False
ACCOUNT_AUTHENTICATION_METHOD = "email"
ACCOUNT_EMAIL_VERIFICATION = "mandatory"
ACCOUNT_CONFIRM_EMAIL_ON_GET = True
ACCOUNT_EMAIL_CONFIRMATION_ANONYMOUS_REDIRECT_URL = (
    "http://localhost:3025/email_verified"
)
OLD_PASSWORD_FIELD_ENABLED = True

CORS_ALLOW_ALL_ORIGINS = True

FORCE_SCRIPT_NAME = '/django'  # without trailing slash

MIDDLEWARE = [
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
]

ROOT_URLCONF = "petsproject.urls"

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [str(BASE_DIR / "templates")],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.debug",
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]

WSGI_APPLICATION = "petsproject.wsgi.application"


# Password validation
# https://docs.djangoproject.com/en/3.1/ref/settings/#auth-password-validators

# AUTH_PASSWORD_VALIDATORS = [
#     {
#         'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
#     },
#     {
#         'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
#     },
#     {
#         'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
#     },
#     {
#         'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
#     },
# ]

AUTH_PASSWORD_VALIDATORS = [
    {
        "NAME": "django.contrib.auth.password_validation.MinimumLengthValidator",
        "OPTIONS": {
            "min_length": 3,
        },
    }
]

REST_AUTH_SERIALIZERS = {
    "PASSWORD_RESET_SERIALIZER": "all_models.views.MyPasswordResetSerializer"
}


# Internationalization
# https://docs.djangoproject.com/en/3.1/topics/i18n/

LANGUAGE_CODE = "en-us"

TIME_ZONE = "UTC"

USE_I18N = True

USE_L10N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.1/howto/static-files/

# STATIC_ROOT -- where collect static saves files
STATIC_ROOT = str(BASE_DIR / ".." / "staticfiles")

STATIC_URL = "/static/"

# STATICFILES_DIRS -- This setting defines the additional locations the collect static app will traverse
STATICFILES_DIRS = [str(BASE_DIR / "static")]


MEDIA_URL = "/media/"
# note this is the path as per the docker not as per this system
MEDIA_ROOT = str(BASE_DIR / "media")

AUTH_USER_MODEL = "all_models.User"


#####################################################
# CUSTOMIZE THESE SETTINGS <BEGINS>
#####################################################

# change the EMAIL BACKEND ONE WANTS TO USE
# Email settings  (currently we are using file based email backed)
EMAIL_FILE_PATH = str(BASE_DIR / "sent_emails")
EMAIL_BACKEND = "django.core.mail.backends.filebased.EmailBackend"


# Celery configs
# change the REDIS_HOST
REDIS_HOST = "redis"
REDIS_PORT = "6379"
CELERY_BROKER_URL = f"redis://{REDIS_HOST}:{REDIS_PORT}"


# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases

# change the NAME, USER, PASSWORD AND HOST the way one needs
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql_psycopg2",
        "NAME": "competible",
        "USER": "django",
        "PASSWORD": "django",
        "HOST": "127.0.0.1",
        "PORT": "5432",
    }
}

#####################################################
# CUSTOMIZE THESE SETTINGS <ENDS>
#####################################################


#####################################################
# MISC: DONT TOUCH THE BELOW <START>
#####################################################


def path(event):
    return event.code.co_filename[-20:]


find_repr_function(object).maxparts = 100000000
find_repr_function(dict).maxparts = 100000000
find_repr_function(list).maxparts = 100000000
find_repr_function(six.text_type).maxparts = 500000000
find_repr_function(six.binary_type).maxparts = 100000000


snoop.install(enabled=DEBUG, columns=[path, "function"])

if DEBUG:

    PROJECT_HOME = os.path.dirname(os.path.realpath(__file__))
    print(f"PROJECT_HOME :: {PROJECT_HOME}")

    if os.path.exists(
        os.path.join(PROJECT_HOME, "external_config", "api_local_settings_fixed.py")
    ):
        from .external_config.api_local_settings_fixed import *  # noqa

    if os.path.exists(
        os.path.join(PROJECT_HOME, "external_config", "api_local_settings_var.py")
    ):
        from .external_config.api_local_settings_var import *  # noqa

#####################################################
# MISC: DONT TOUCH THE BELOW <END>
#####################################################


overrides = None
try:
    import petsproject.sys_specific_settings as sys_specific_settings

    overrides = sys_specific_settings.__dict__
except ModuleNotFoundError:
    print("using default settings")

if overrides is not None:
    for name, val in overrides.items():
        if not name.startswith("__") and name in globals() and globals()[name] != val:
            globals()[name] = val
            print(f"overwriting default value for {name} >> {val}")

```

# reactjs 
	
setup axios baseurl and also subtitute the medial url with base url

```
import axios from "axios";

//const baseURL = `http://${window.location.hostname}:8025`;

const baseURL = `http://${window.location.hostname}:${window.location.port}/django`;

const axiosInstance = axios.create({
  baseURL: baseURL,
  timeout: 5000,
  headers: {
    Authorization: localStorage.getItem("access_token")
      ? "Bearer " + localStorage.getItem("access_token")
      : null,
    "Content-Type": "application/json",
    accept: "application/json",
  },
});

// https://www.youtube.com/watch?v=ANvVndhOxIc
// https://stackoverflow.com/questions/64576410/react-axios-interceptor-for-refresh-token
// NOTE: dj-rest-auth/token/refresh return only access and not both again.
axiosInstance.interceptors.response.use(
  (response) => response,
  (error) => {
    const originalRequest = error.config;

    // Reject promise if usual error
    if (!error.response) {
      return Promise.reject(error);
    }

    // Prevent infinite loops
    if (
      error.response.status === 401 &&
      originalRequest.url === "dj-rest-auth/token/refresh/"
    ) {
      localStorage.removeItem("access_token");
      localStorage.removeItem("refresh_token");
      window.location.href = "/login/";
      return Promise.reject(error);
    }

    if (error.response.status === 401) {
      const refreshToken = localStorage.getItem("refresh_token");
      if (refreshToken) {
        return axiosInstance
          .post("dj-rest-auth/token/refresh/", { refresh: refreshToken })
          .then((response) => {
            localStorage.setItem("access_token", response.data.access);
            axiosInstance.defaults.headers["Authorization"] =
              "Bearer " + response.data.access;
            originalRequest.headers["Authorization"] =
              "Bearer " + response.data.access;
            return axiosInstance(originalRequest);
          })
          .catch((err) => {
            return Promise.reject(err);
          });
      } else {
        console.log("Refresh token not available.");
        window.location.href = "/login/";
      }
    } else {
      return Promise.reject(error);
    }
  }
);

export { axiosInstance, baseURL };

```
	
## replacing the url

the media url needs to be appended /django

so do this
```
<img
  src={`${baseURL}${rowData.photo.replace(/^.*\/\/[^/]+/, "")}`}
  style={{ width: 50 }}
/>
```
# Digital Ocean Create a Droplet and access it:

- Create a droplet
- Select the 5 dollar plar
![](https://i.imgur.com/OhtHpDC.png)
- Choose data center region
![](https://i.imgur.com/jFFDSRL.png)
- choose ssh keys as access
![](https://i.imgur.com/UdN029L.png)
	
Now to access do
```
ssh root@xx.xxx.xxx.xx
```

after that create a user we want to

	
# USEFUL TIP DIGITAL OCEAN

## ADD USER WITH SUDO

https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-18-04-quickstart

```
adduser simha

Enter new UNIX password:

# generate random password

date +%s | sha256sum | base64 | head -c 32 ; echo

# adding user to sudo group

usermod -aG sudo simha

# testing

su - simha

sudo ls -la /root


# sudo dont ask password

sudo visudo

# add the below line

simha ALL=(ALL) NOPASSWD: ALL
```
	
NOw access as
```
ssh simha@xx.xx.xxx.xx
```


# now install docker

check docker is installed or not
```
docker info
```


First, update your existing list of packages:
```
sudo apt update
```

Install from standard ubuntu repository
```
sudo apt install docker.io
```

Enable docker

```
sudo systemctl enable --now docker
```

Install docker-compose

```
sudo apt  install docker-compose
```

Get the user name:
```
whoami
```

If you want to be able to run the docker CLI command as a non-root user, add your user to the docker user group, re-login, and restart docker.service.

```
sudo usermod -aG docker ubuntu

note: immeditely after this the user may not get access

check

# groups 

see if docker is listed, if not logout and login back

```
-aG means add to a group


after logout and login check the groups

```
groups

-- output
ubuntu adm dialout cdrom floppy sudo audio dip video plugdev netdev lxd docker
```


check docker version

```
docker --version

-- output
Docker version 19.03.8, build afacb8b7f0
```

kernel version:
```
uname -r

--output
5.4.0-1029-aws
```

# SERVER BOTTLE NECK1: IMPORTANT: DOCKER SETUP LOG ROTATION ELSE THE LOGS FILES WILL GROW AND LEFT WITH NO SPACE

>By default, Docker captures the standard output (and standard error) of all your containers, and writes them in files using the JSON format.

By default, the stdout and stderr of the container are written in a JSON file located in 

```
/var/lib/docker/containers/[container-id]/[container-id]-json.log`
```
If you leave it unattended, it can take up a large amount of disk space, as shown below.

## Solution system wide
 
Add this into your `/etc/docker/daemon.json` to cap your container logs to 1gb (100x 10mb files):

`/etc/docker/daemon.json` needs to be created. By default it does not exist

sudo vi /etc/docker/daemon.json

```
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "100"
  }
}

```

after this stop all the containers and restart the docker

```
docker stop $(docker ps -aq); docker rm $(docker ps -a -q); docker container prune; docker image prune; docker network prune
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## solution dockercompose

```
version: '3'
services:
    app:
        ...
        logging:
            driver: "json-file"
            options:
                max-size: "10m"
                max-file: "100"
```


# SERVER BOTTLE NECK: DONT DELETE THE FOLDER DO_NOT_DELETE_postgres_data and dont include in the github repo

Reason:
the below command will remove the volumes also. SO if we want some data to persist then we will be loosing it when the below command runs
```
docker stop $(docker ps -aq); docker rm $(docker ps -a -q); docker container prune; docker image prune; docker network prune
```

DO_NOT_DELETE_postgres_data -- stored the postgresql database.
	

# Basic Docker folder structure
```
project_folder
||-- CODE
|-----django_backend (create seperate git repo for this)
|-----reacts-frontend (create seperate git repo for this)

||-- docker_based (create seperate git repo for this)
|-----Dockerbuild_node16_python3.9
|-----nginx
|-----docker-compose-localhost-localdb.yml
|-----python_related
|-----------Django_external_config
|-----------jupyter
	
||-- DO_NOT_DELETE_POSTGRES_DATA (this is persistent data)
||-- DO_NOT_DELETE_JUPYTER_NOTEBOOKS (this is persistent data)
```

	
## USEFUL TIP zsh

# install zsh
    sudo apt-get update
    sudo apt install zsh

# change the default shell
    sudo chsh -s /usr/bin/zsh

the above will ask for password so better do this

    sudo chsh -s $(which zsh) $(whoami)

run zsh command to configure the .zshrc and select empty file and place this

    ~/.zshrc
    autoload -Uz compinit promptinit
    compinit
    promptinit

    # This will set the default prompt to the walters theme
    prompt walters


# install oh-my-zsh

    sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

and replace theme as `aussiegeek`

# USEFUL TIP install hstr later after docker

```
sudo add-apt-repository ppa:ultradvorka/ppa
sudo apt-get update
sudo apt-get install hstr

after this

# Configure HSTR just by running:
hstr --show-configuration >> ~/.zshrc

then logout and login back

```

bash auto completion history

method1 add this to .zshrc
```
bindkey '^S' history-incremental-pattern-search-backward
```
	
	
```
cat >> ~/.inputrc <<'EOF'                                                                                                   
"\e[A": history-search-backward
"\e[B": history-search-forward
EOF
```

```
bind -f  ~/.inputrc
```
	
# USEFUL TIP docker compose related commands:
```
docker stop $(docker ps -aq); docker rm $(docker ps -a -q); docker container prune; docker image prune; docker network prune
docker-compose -p somename -f docker-compose-localhost.yml up --build --force-recreate
docker-compose -p esomenamelemzy -f docker-compose-localhost-staging.yml logs --no-color --tail=2000 webapp


	
hostfolder="$(pwd)"
dockerfolder="/home/simha/app"
docker run --rm -it \
  -v ${hostfolder}:${dockerfolder} \
python3.9-nodejs16-buster:nikolaik-python3.9-nodejs16 /bin/bash

docker build -t python-node-buster:nikolaik-python3.7-nodejs15 --file Dockerfile_node_python_buster_aws_ubuntu .
	
hostfolder="$(pwd)"
dockerfolder="/home/simha/app"
docker run --rm -it \
  -v ${hostfolder}:${dockerfolder} \
python-node-buster:nikolaik-python3.7-nodejs15 /bin/bash


```

# How to update the code on remote server and restart
	
```
$ ssh_sant=1;  
cd /path/docker_based;
git add -A; git commit -m "changes"; git push origin
ssh simha@xx.xx.xx.xx<<'ENDSSH'
set -x -o verbose;
cd project/docker_based/
git stash --include-untracked
git pull origin --rebase
docker-compose -p test -f docker-compose-localhost_onserver.yml up --build --force-recreate --remove-orphans -d
set +x
ENDSSH

```

# FREE SSL


after cloning the repo and setting the virtualenv in django 

0) start the docker-compose

```
docker-compose -p production -f docker-compose-somedomain-com.yml up -d
```

1) create the ssl certificates using

```
sudo bash init-letsencrypt_somedomain_com.sh
```

Once its done 

2) stop all the dockers

```
docker stop $(docker ps -aq); docker rm $(docker ps -a -q); docker container prune; docker image prune; docker network prune
```

0) restart the docker-compose

```
docker-compose -p production -f docker-compose-somedomain-com.yml up -d
```

init-letsencrypt_somedomain_com.sh
```
#!/bin/bash
set -x -o verbose;

# https://github.com/wmnnd/nginx-certbot
# https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71

if ! [ -x "$(command -v docker-compose)" ]; then
  echo 'Error: docker-compose is not installed.' >&2
  exit 1
fi

domains=(somedomain.com www.somedomain.com app.somedomain.com admin.somedomain.com)
rsa_key_size=4096
data_path="./certbot"
email="someemail@gmail.com" # Adding a valid address is strongly recommended
staging=0 # Set to 1 if you're testing your setup to avoid hitting request limits

if [ -d "$data_path" ]; then
  read -p "Existing data found for $domains. Continue and replace existing certificate? (y/N) " decision
  if [ "$decision" != "Y" ] && [ "$decision" != "y" ]; then
    exit
  fi
fi


if [ ! -e "$data_path/conf/options-ssl-nginx.conf" ] || [ ! -e "$data_path/conf/ssl-dhparams.pem" ]; then
  echo "### Downloading recommended TLS parameters ..."
  mkdir -p "$data_path/conf"
  curl -s https://raw.githubusercontent.com/certbot/certbot/master/certbot-nginx/certbot_nginx/_internal/tls_configs/options-ssl-nginx.conf > "$data_path/conf/options-ssl-nginx.conf"
  curl -s https://raw.githubusercontent.com/certbot/certbot/master/certbot/certbot/ssl-dhparams.pem > "$data_path/conf/ssl-dhparams.pem"
  echo
fi

echo "### Creating dummy certificate for $domains ..."
path="/etc/letsencrypt/live/$domains"
mkdir -p "$data_path/conf/live/$domains"
docker-compose -p production -f docker-compose-somedomain-com.yml run --rm --entrypoint "\
  openssl req -x509 -nodes -newkey rsa:$rsa_key_size -days 1\
    -keyout '$path/privkey.pem' \
    -out '$path/fullchain.pem' \
    -subj '/CN=localhost'" certbot
echo


echo "### Starting nginx ..."
docker-compose -p production -f docker-compose-somedomain-com.yml up --force-recreate -d nginx
echo

echo "### Deleting dummy certificate for $domains ..."
docker-compose -p production -f docker-compose-somedomain-com.yml run --rm --entrypoint "\
  rm -Rf /etc/letsencrypt/live/$domains && \
  rm -Rf /etc/letsencrypt/archive/$domains && \
  rm -Rf /etc/letsencrypt/renewal/$domains.conf" certbot
echo


echo "### Requesting Let's Encrypt certificate for $domains ..."
#Join $domains to -d args
domain_args=""
for domain in "${domains[@]}"; do
  domain_args="$domain_args -d $domain"
done

# Select appropriate email arg
case "$email" in
  "") email_arg="--register-unsafely-without-email" ;;
  *) email_arg="--email $email" ;;
esac

# Enable staging mode if needed
if [ $staging != "0" ]; then staging_arg="--staging"; fi

docker-compose -p production -f docker-compose-somedomain-com.yml run --rm --entrypoint "\
  certbot certonly --webroot -w /var/www/certbot \
    $staging_arg \
    $email_arg \
    $domain_args \
    --rsa-key-size $rsa_key_size \
    --agree-tos \
    --force-renewal" certbot
echo

echo "### Reloading nginx ..."
docker-compose -p production -f docker-compose-somedomain-com.yml exec nginx -s reload

```

	
# jupyter add virtual env
	
> Jupyter Notebook makes sure that the IPython kernel is available, but you have to manually add a kernel with a different version of Python or a virtual environment. 

	
- Next you can add your virtual environment to Jupyter by typing:

```
python -m ipykernel install --user --name=myenv
	
or
	
ipython kernel install --name "local-venv" --user

or

ipython kernel install --user --name=.venv
	
```

- This should print the following:
```
Installed kernelspec myenv in /home/user/.local/share/jupyter/kernels/myenv
```

In this folder you will find a kernel.json file which should look the following way if you did everything correctly:

```
{
 "argv": [
  "/home/user/anaconda3/envs/myenv/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "myenv",
 "language": "python"
}
```
```
ls ~/.local/share/jupyter/kernels/venv/kernel.json
```
	
- Select venv
	
```
jupyter notebook
```
	
# jupyter notebook allow access 

To begin with, if not available, create a config file first

    jupyter notebook --generate-config
    Writing default config to: /home/simha/.jupyter/jupyter_notebook_config.py

Then head over to the file and edit it 

    cd ~/.jupyter

Uncomment the three lines or delete all and add the three lines
    
    c.NotebookApp.allow_origin = '*' #allow all origins
    c.NotebookApp.ip = '0.0.0.0' # listen on all IPs
    c.NotebookApp.allow_remote_access = True

Try to connect with remote IP.
*(If you are using AWS EC2, you'll need to whitelist your ip and enable inbound connections for your client pc or all IP address over the port 8888)*
    
If you still can't connect, you can try

    jupyter notebook --ip 0.0.0.0 --port 8888


	
# git clone with different rsa key
	
First generate a key
	
```
ssh-keyge
```
give a different name `~/.ssh/id_rsa.pub`

## Clone the repos	

```
git -c core.sshCommand="ssh -i ~/.ssh/id_rsa_vishnu" clone git@github.com:xxxxxx/Notes_job.git .
```
	
## after cloning add the key
```
git config --add --local core.sshCommand 'ssh -i ~/.ssh/id_rsa_vishnu'
```
	
# Django Class Based Views
	
## What `as_view()` does in the URLConf

`https://stackoverflow.com/a/31491074/2897115`

```
response = MyView.as_view()(request)  # valid way
```	
By calling the `as_view()` function on my view class MyView will give me a view which i will call with request parameter to initiate the request-response cycle.
	
    my_callable_view = BlogIndex.as_view() # returns a callable view
    <function blog.views.BlogIndex>

Now, call this function and pass the `request`.

     response = my_callable_view(request) # generate proper response

## Another explanation
https://stackoverflow.com/a/15056648/2897115

![](https://i.imgur.com/AA1sYbX.png)
![](https://i.imgur.com/uhrxsGG.png)

	    
## what are differnce between `initkwargs` and `kwargs`

### Question
https://stackoverflow.com/q/28770701/2897115

![](https://i.imgur.com/d9zza1k.png)

### Answer  
https://stackoverflow.com/a/28770985/2897115

![](https://i.imgur.com/raokKqP.png)

## as_view classbased method
```
@classonlymethod
def as_view(cls, **initkwargs):
```

https://djangodeconstructed.com/2020/01/03/mental-models-for-class-based-views/
![](https://i.imgur.com/Tef0SQc.png)
	    
### checking
![](https://i.imgur.com/JMS0RPc.png)
	    
### entire process and closures
![](https://i.imgur.com/PM7qjiv.png)

	    
# Using SSH keys with GitLab CI/CD ALL TIERS
https://docs.gitlab.com/ee/ci/ssh_keys/

## Generate private and public keys

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/simha/.ssh/id_rsa): /home/simha/.ssh/id_rsa_QA
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/simha/.ssh/id_rsa_QA
Your public key has been saved in /home/simha/.ssh/id_rsa_QA.pub
The key fingerprint is:
SHA256:hAkR6p+++R8zZRXXsJtn9XS1SMWAvg+VL70f1SFwj8s simha@gauranga
The key's randomart image is:
+---[RSA 3072]----+
|    +o     .o+*+.|
|   . . o   .+o+o+|
|  .   o . . .+o++|
| .     .   o.oo+*|
|  .     S o oE= *|
|   . .   o o . =.|
|    o   +   o ...|
|   . .   +   . ..|
|    +o...       o|
+----[SHA256]-----+
```

### Copy the public key to servers authorized keys

```
$ cat /home/simha/.ssh/id_rsa_QA.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAOQtlWF/GIo21VjtC4x4c480oz4GDpWzYOGAD2HNeUft4dydo5V9coPQpnzz5/kOtcQEzFo+kpyQ4TK0Wm5MiaC3EvRmteJlZI4fXW9x/EkFEcM9v0VUGZisidpoLQIJmXPai2VOSE8Jf7ZZ7Xc71xTaYNCCuZc= xxxx@yyyyy
```
Login to the remote server and put it there

```
ssh username@xx.xx.xxx
$ vi ~/.ssh/authorized_keys
```

### ADD CI/CD variable private key

```
$ cat /home/simha/.ssh/id_rsa_QA
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEA5lETR8hIYbpsYdlXNwLlLEUSomwvLQZ37+5IMdsUe7Aomd6KmWSj
0Pb/Hsu7EgLIG4xF9X1S+fNALCbeQCNrjO0mmrZ9RfafAX5QxEoe/Bp/cNtztP27PQn69n
R4uYNQ3lro6wibr3WnO+gXeATAfVF9I1JZDxYuLh2wFyExE3Z8Uaz6iTwlBPFqIKBDunD6
sIm691pzvoF3gEwH1RfSNSWQ8WLi4dsBchMRN2fFGs+ok8JQTxaiCgQ7pw+qyapisEpAFJ
ZKVHKtvwPiZEEpf9CbU+nVOcE6L38hyYwaN+c9HwQYTXBdxHmPyMKZzSzJmn6ZI4EQWPMr
ftqNG/ZGwLaRILHNyGlr41ar3QHSrqJ9XljHUHlWKjXA1UdPXt5LNplSyosD8BYJIYmX0v
/VPO3i/UMLAM5C2VYX8YijbVWO0LjHhzjzSjPgYOlbNg4YAPYc15R+3h3J2jlX1yg9CmfP
Pn+Q61xATMWj6SnJDhMrRabkyJoLcS9Ga14mVkjh9db3H8SQURwz2/RVQZmKyJ2mgtAgmZ
c9qLZU5ITwl/tlntdzvXFNpg0IK5lwAAAAMBAAEAAAGAam1Uh3sZV2+Z3a1dC+Kem9JfRg
bP1fKDQa/OVJtz36QLXu7jBPbobAt24HgsPapjZbdwLHx4919cbAqZ8PFtJXYAvMVPJiFM
YJhKIipOHxjvguslkKEfAJm4CmLP1onDuLwxnUohBvdLC/e3wJIRkNczCDtpQ/tv44d8c3
O3BdNepy9Tpk7QnHQiImlsYp8KdvAPkRlX3/BWPbmhKHjffzc9kFYxQjto39XjjQ8eJfDA
qhgo1P48iHIEF0JOg4UQZSd32NoVBFt3XwDkvMzGZ1MTu0xrsG0puV4EfmunmBvwGF9naV
MNAkfquikbozieNzI98vLDbj+7USnWfQvbkSmqvXZ1qi2okNa1flCiLhDYa0VcBOX1yI4c
W0p2k0+4rQaUo1tLjWZ/agntidiUYU+V+7Ruz5tENJ4Rj7Zo8ydNx9GWn6yl6IocinQOxB
6J9ivooA/QrhPNYO/BztiIHZ3bVBjfFMYxrJhRLxs5LlVVfjtobevUWdMroGVvf0bhAAAA
wH3UUoQY5vFTNZthMP97963mJ/QgWYmOCEPr18xsQ5gAJLdW0W4FA/Eh8rt
-----END OPENSSH PRIVATE KEY-----
```

Go to gitlab project > settings > CI/CD > variables and add the private key `SSH_PRIVATE_KEY` there

## gitlab CI/CD `gitlab-ci.yml`

```
variables:
  DEPLOY_USER: username
  DEPLOY_HOST: xx.xx.xx.xx

deploy:
  image: docker:19.03.13
  stage: deploy_qa
  only:
    - QA  
  before_script:
    - "which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )"
    - eval $(ssh-agent -s)
    - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add - > /dev/null
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - ssh-keyscan ssh-keyscan $DEPLOY_HOST >> ~/.ssh/known_hosts
    - chmod 644 ~/.ssh/known_hosts
  script:
    - |
      ssh $DEPLOY_USER@$DEPLOY_HOST<<'ENDSSH'                                                                    
      set -x -o verbose;
      ..... do the tasks
      ENDSSH
```


# react hook form Onchange

You just have to move the `onChange` props after `{...register(...)}`

```tsx
const productImageField = register("productImage", { required: true });

return (
    <input
        className="form-control"
        type="file"
        {...productImageField}
        onChange={(e) => {
          productImageField.onChange(e);
          handleImageUpload(e);
     }}
    />
)
```

	    
	    
	    
# moment javascript


## convert moment object to string
```
momentObject.format('YYYY-MM-DD')

or

moment().format('MM/DD/YYYY');
```

### another Example

```
var moment = require('moment');

let yourdate = '2021-01-02T07:57:45.121Z'; // for example

moment(yourdate).format('MM/DD/YYYY');

// output : 01-02-2021


moment(yourdate).format('DD-MMM-YYYY');

// output : 01-Jan-2021
```

if you want to use moment() in the Chrome console you can try to open the official site and then go to the console.

## parse string to moment object

If you know the format of an input string, you can use that to parse a moment.

```
moment("12-25-1995", "MM-DD-YYYY");
```

The parser ignores non-alphanumeric characters by default, so both of the following will return the same thing.

```
moment("12-25-1995", "MM-DD-YYYY");
moment("12/25/1995", "MM-DD-YYYY");
```
# moment tips
	    
```
moment().toISOString()
"2021-11-23T13:02:05.728Z"
```

```
String(moment())
"Tue Nov 23 2021 18:56:18 GMT+0530"
String(moment().utc())
"Tue Nov 23 2021 13:26:32 GMT+0000"
moment().toString()
"Tue Nov 23 2021 18:56:53 GMT+0530"
moment().toISOString()
"2021-11-23T13:26:57.748Z"
moment(5, "HH").toString()
"Tue Nov 23 2021 05:00:00 GMT+0530"
moment("1-15 AM +05:30","h-mm A Z").toString()
"Tue Nov 23 2021 01:15:00 GMT+0530"
moment("1-15 AM +05:30","h-mm A Z").utc().toString()
"Mon Nov 22 2021 19:45:00 GMT+0000"
moment("1-15 AM +05:30","h-mm A Z").utc().format("HH:mm")
"19:45"

```

	    
# Moment
	    
# USING TRUE: HOW TO KEEP TIME SAME AND ONLY CHANGE THE TIME ZONE  OR HOW TO CREATE TIME IN A PARTICULAT TIMEZONE

```
//moment('00:00','HH:mm')  created in local time zone by default
moment('00:00','HH:mm').toString()
"Tue Nov 23 2021 00:00:00 GMT+0530"

//.tz("timezone",true) (WITH TRUE)  creates time in the specific time zone
moment('00:00','HH:mm').tz("UTC",true).toString()
"Tue Nov 23 2021 00:00:00 GMT+0000"
```

# NOT USING TRUE  -- to convert time from one time zone to another (here time changes)
	    
```
//.tz("timezone") (WITHOUT TRUE)  converts time to that time zone
//here moment('00:00','HH:mm') creates time in loca time zone and then its converted to the corresponding time in UTC without using true
moment('00:00','HH:mm').tz("UTC").toString()
"Mon Nov 22 2021 18:30:00 GMT+0000"

NOTE SAME THING CAN BE DONE USING

moment('00:00','HH:mm').utc().toString()
"Mon Nov 22 2021 18:30:00 GMT+0000"
```

	    
# Activating virtualenv inside Dockerfile
	    
https://pythonspeed.com/articles/activate-virtualenv-dockerfile/
	    
## The repetitive method that totally works

You can fix that by actually activating the virtualenv separately for each RUN as well as the CMD:

```
FROM python:3.9-slim-bullseye

RUN python3 -m venv /opt/venv

# Install dependencies:
COPY requirements.txt .
RUN . /opt/venv/bin/activate && pip install -r requirements.txt

# Run the application:
COPY myapp.py .
CMD . /opt/venv/bin/activate && exec python myapp.py
```

(The exec is there to get correct signal handling.)

## without any repetition or need to remember anything.

The most important part is setting PATH: PATH is a list of directories which are searched for commands to run. activate simply adds the virtualenv’s bin/ directory to the start of the list.

We can replace activate by setting the appropriate environment variables: Docker’s ENV command applies both subsequent RUNs as well as to the CMD.

```
FROM python:3.9-slim-bullseye

ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Install dependencies:
COPY requirements.txt .
RUN pip install -r requirements.txt

# Run the application:
COPY myapp.py .
CMD ["python", "myapp.py"]
```
	    
	    
# Install KVM on archinux
https://transang.me/install-kvm-on-arch-linux/

## Checking support for KVM

### Hardware support

KVM requires that the virtual machine host's processor has virtualization support (named VT-x for Intel processors and AMD-V for AMD processors). You can check whether your processor supports hardware virtualization with the following command:
```
$ LC_ALL=C lscpu | grep Virtualization
```
	    
You may need to enable virtualization support in your BIOS

![](https://i.imgur.com/ncypijp.png)
	    
### Kernel support

* One can check if the necessary modules, kvm and either kvm_amd or kvm_intel, are available in the kernel with the following command:

```
$ zgrep CONFIG_KVM /proc/config.gz

CONFIG_KVM_GUEST=y
CONFIG_KVM_MMIO=y
CONFIG_KVM_ASYNC_PF=y
CONFIG_KVM_VFIO=y
CONFIG_KVM_GENERIC_DIRTYLOG_READ_PROTECT=y
CONFIG_KVM_COMPAT=y
CONFIG_KVM_XFER_TO_GUEST_WORK=y
CONFIG_KVM=m
CONFIG_KVM_INTEL=m
CONFIG_KVM_AMD=m
CONFIG_KVM_AMD_SEV=y
CONFIG_KVM_XEN=y
CONFIG_KVM_MMU_AUDIT=y
```

The module is available only if it is set to either y or m.

* Then, ensure that the kernel modules are automatically loaded, with the command:

```
$ lsmod | grep kvm
kvm_intel             335872  0
kvm                  1036288  1 kvm_intel
irqbypass              16384  1 kvm
```

## How to use KVM
https://illuad.fr/2021/04/28/install-kvm-qemu-and-libvirt-on-arch-linux.html

### REFER  QEMU

QEMU can use other hypervisors like Xen or KVM to use CPU extensions (HVM) for virtualization.

https://boseji.com/posts/manjaro-kvm-virtmanager/

# QEMU Installation

```
sudo pacman -S qemu qemu-arch-extra ovmf bridge-utils dnsmasq vde2 openbsd-netcat ebtables iptables-nft dmidecode libvirt

ovmf helps to do the UEFI Bios and Secure Boot setups.
bridge-utils for network bridge needed for VMs
vde2 for QEMU distributed ethernet emulation
dnsmasq the DNS forwarder and DHCP server
openbsd-netcat network testing tool (Optional)
ebtables and iptables-nft to create packet routing and firewalls
dmidecode: reports information about your system’s hardware as described in your system BIOS
libvirt: Libvirt,
```
## Virt-Manager and libvirtd Service Install

Virt-manager is a UI that helps to create and organize the VM’s. And virt-viewer is used to open remote window into the VM instance.

```
sudo pacman -S virt-manager virt-viewer
```
	    
RUNNIG

```
 sudo pacman -S qemu qemu-arch-extra ovmf bridge-utils dnsmasq vde2 openbsd-netcat ebtables iptables-nft dmidecode

warning: bridge-utils-1.7.1-1 is up to date -- reinstalling
warning: vde2-2.3.2-16 is up to date -- reinstalling
warning: dmidecode-3.3-1 is up to date -- reinstalling
resolving dependencies...
looking for conflicting packages...
:: openbsd-netcat and gnu-netcat are in conflict. Remove gnu-netcat? [y/N] y
:: iptables-nft and iptables are in conflict. Remove iptables? [y/N] y

Packages (14) gnu-netcat-0.7.1-8 [removal]  iptables-1:1.8.7-1 [removal]  libbpf-0.5.0-1  nftables-1:1.0.0-1  sdl2_image-2.0.5-2  bridge-utils-1.7.1-1
              dmidecode-3.3-1  dnsmasq-2.86-1  edk2-ovmf-202108-1  iptables-nft-1:1.8.7-1  openbsd-netcat-1.217_2-1  qemu-6.1.0-5  qemu-arch-extra-6.1.0-5
              vde2-2.3.2-16

Total Download Size:    78.44 MiB
Total Installed Size:  804.29 MiB
Net Upgrade Size:      757.68 MiB

:: Proceed with installation? [Y/n] 
```

### If you want to play with Libvirt, you must be in the libvirt group.
```
sudo usermod -aG libvirt $USER
```
	    
## Step 3: Start KVM libvirt service

https://computingforgeeks.com/install-kvm-qemu-virt-manager-arch-manjar/

```
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
```
	    
## enable services

```
$ sudo systemctl enable --now libvirtd
sudo systemctl enable --now dnsmasq.service
Created symlink /etc/systemd/system/multi-user.target.wants/libvirtd.service → /usr/lib/systemd/system/libvirtd.service.
Created symlink /etc/systemd/system/sockets.target.wants/virtlockd.socket → /usr/lib/systemd/system/virtlockd.socket.
Created symlink /etc/systemd/system/sockets.target.wants/virtlogd.socket → /usr/lib/systemd/system/virtlogd.socket.
Created symlink /etc/systemd/system/sockets.target.wants/libvirtd.socket → /usr/lib/systemd/system/libvirtd.socket.
Created symlink /etc/systemd/system/sockets.target.wants/libvirtd-ro.socket → /usr/lib/systemd/system/libvirtd-ro.socket.
Created symlink /etc/systemd/system/multi-user.target.wants/dnsmasq.service → /usr/lib/systemd/system/dnsmasq.service.
```

## make sure that Libvirt daemon runs by checking its status.

```
$ sudo systemctl status libvirtd
● libvirtd.service - Virtualization daemon
     Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: disabled)
     Active: active (running) since Sat 2021-12-04 19:41:45 IST; 1min 10s ago
TriggeredBy: ● libvirtd.socket
             ● libvirtd-ro.socket
             ● libvirtd-admin.socket
       Docs: man:libvirtd(8)
             https://libvirt.org
   Main PID: 506320 (libvirtd)
      Tasks: 19 (limit: 32768)
     Memory: 13.2M
        CPU: 485ms
     CGroup: /system.slice/libvirtd.service
             └─506320 /usr/bin/libvirtd --timeout 120

Dec 04 19:41:45 gauranga systemd[1]: Started Virtualization daemon.
```

## Allow Non-root User to use KVM/QEMU Virtualization
https://www.howtoforge.com/how-to-install-kvm-qemu-on-manjaro-archlinux/

By default, only user "root" can create and manage virtual machines. To allow non-root users to create and manage virtual machines, you should follow the libvirtd configuration below.

Execute the following command to edit the libvirtd configuration.

```
sudo nano /etc/libvirt/libvirtd.conf
```
Uncomment the option "unix_sock_group" and enter the group name as "libvirt".
```
# Set the UNIX domain socket group ownership. This can be used to
# allow a 'trusted' set of users access to management capabilities
# without becoming root.
#
# This setting is not required or honoured if using systemd socket
# activation.
#
# This is restricted to 'root' by default.
unix_sock_group = "libvirt"
```
After that, uncomment the option "unix_sock_rw_perms" and leave the permission as default "0770".
```
# Set the UNIX socket permissions for the R/W socket. This is used
# for full management of VMs
#
# This setting is not required or honoured if using systemd socket
# activation.
#
# Default allows only root. If PolicyKit is enabled on the socket,
# the default will change to allow everyone (eg, 0777)
#
# If not using PolicyKit and setting group ownership for access
# control, then you may want to relax this too.
unix_sock_rw_perms = "0770"
```
Save the configuration by pressing the Ctrl+x button and type y, then enter.

2. Next, add your user to the group "libvirt" using the following command.
```
sudo usermod -a -G libvirt username
```
3. After that, restart the libvirtd service to apply a new configuration.
```
sudo systemctl restart libvirtd
```
Now all users within the group "libvirt" will be able to create and configure virtual machines.



	    
# HOW TO CHECK LINUX SYSTEM IS PHYSICAL OR VIRTUAL

https://ostechnix.com/check-linux-system-physical-virtual-machine/

```
$ sudo dmidecode -s system-manufacturer
[sudo] password for simha: 
LENOVO
```

and

```
$ sudo dmidecode | grep Product
	Product Name: 80E5
	Product Name: Lenovo G50-80
```

Commom outputs

```
[Physical system]

Inspiron N5050

[Virtual system on VirtualBox]

VirtualBox

[Virtual system on KVM/QEMU]

Standard PC (Q35 + ICH9, 2009)
```

# Differences between QEMU, KVM, and Libvirt

QEMU is a machine (hardware) emulator.

KVM is a kernel module for Linux to enable virtualization; this is the hypervisor.

QEMU can run without KVM but it can be quite a bit slower.

libvirt is a virtualization library which wraps QEMU and KVM to provide APIs for use by other programs, such as Vagrant, which is a tool for creating virtualized development environments.

Summary:

Vagrant uses libvirt.
libvirt uses QEMU and KVM.


# KVM vs QEMU vs Libvirt
https://www.thegeekyway.com/kvm-vs-qemu-vs-libvirt/

Hypervisor is the agent that helps you create virtual machines. He is the guy who creates and runs the guest machine and provide the host’s resource to the guest

QEMU and KVM both are able to act as hypervisor. Then why are they used together?

QEMU it is a little slower

QEMU is the hypervisor/emulator and KVM is the accelerating agent.

Then we come to libvirt. Libvirt is quite innocent in the sense that is doesn’t confuse you! It is simply a virtualization management library. And what does it do? It manages both KVM and QEMU. It consists of three utilities namely - an API library, a daemon (libvirtd) and a command line tool -virsh

So, whenever you are using these all together, remember there is a hypervisor, an accelerating agent and a management library.

# KVM VS QEMU VS LIBVERT

https://octetz.com/docs/2020/2020-05-06-linux-hypervisor-setup/

These are the key tools/services/features that enable vitalization.

## key system tools:

kvm:

  - Kernel-based Virtual Machine
  - Kernel module that handles CPU and memory communication

qemu:

  - Quick EMUlator
  - Emulates many hardware resources such as disk, network, and USB. While it can emulate CPU, you'll be exposed to qemu/kvm, which delegates concerns like that to the KVM (which is HVM).
  - Memory relationship between qemu/kvm is a little more complicated but can be read about here.

libvirt:

  - Exposes a consistent API atop many virtualization technologies. APIs are consumed by client tools for provisioning and managing VMs.

## user/client tools:

![](https://i.imgur.com/Jn4IL6j.png)

## ancillary system tools:

![](https://i.imgur.com/GfAuvf4.png)

## The overall diagram

![](https://i.imgur.com/1BKhEy0.png)

## How to install

```
pacman -Sy --needed \
  qemu \
  dhclient \
  openbsd-netcat \
  virt-viewer \
  libvirt \
  dnsmasq \
  dmidecode \
  ebtables \
  virt-install \
  virt-manager \
  bridge-utils
```

## storage location


ibvirt keeps its files at /var/lib/libvirt/. There are multiple directories within.
```
drwxr-xr-x  2 root   root 4096 Apr  4 05:05 boot
drwxr-xr-x  2 root   root 4096 May  6 16:16 dnsmasq
drwxr-xr-x  2 root   root 4096 Apr  4 05:05 filesystems
drwxr-xr-x  2 root   root 4096 May  6 10:52 images
drwxr-xr-x  3 root   root 4096 May  6 09:55 lockd
drwxr-xr-x  2 root   root 4096 Apr  4 05:05 lxc
drwxr-xr-x  2 root   root 4096 Apr  4 05:05 network
drwxr-xr-x 11 nobody kvm  4096 May  6 16:16 qemu
drwxr-xr-x  2 root   root 4096 Apr  4 05:05 swtpm
The images directory is the default location a VM's disk image will be stored (e.g. qcow2).
```

# qemu:///system vs qemu:///session

https://blog.wikichoon.com/2016/01/qemusystem-vs-qemusession.html

# How to change default location of libvirt VM images

https://www.xmodulo.com/change-default-location-libvirt-vm-images.html

libvirt and its GUI front-end virt-manager can create and manage VMs using different hypervisors such as KVM and Xen. By default, all the VM images created via libvirt go to /var/lib/libvirt/images directory. 

However, this may not be desirable in some cases. For example, the disk partition where /var/lib/libvirt/images resides may have limited free space. 

In fact, you can easily change the default location of the libvirt image directory, or what they call a "storage pool".

If you are using virt-manager GUI program, changing the default storage pool is very easy.

![](https://i.imgur.com/Uwkb9RF.png)

![](https://i.imgur.com/7qK58ZM.png)

![](https://i.imgur.com/tVQLNBK.png)

![](https://i.imgur.com/OnTHtPM.png)

![](https://i.imgur.com/LzVDvos.png)



# Docker Machine Benefits

https://burmillaos.org/docs/installation/workstation/docker-machine/

With Docker Machine, you can point the docker client on your host to the docker daemon running inside of the VM. This allows you to run your docker commands as if you had installed docker on your host.

To point your docker client to the docker daemon inside the VM, use the following command:

```
$ eval $(docker-machine env <MACHINE-NAME>)
```
After setting this up, you can run any docker command in your host, and it will execute the command in your BurmillaOS VM.

```
$ docker run -p 80:80 -p 443:443 -d nginx
```
In your VM, a nginx container will start on your VM. To access the container, you will need the IP address of the VM.

```
$ docker-machine ip <MACHINE-NAME>
```
Once you obtain the IP address, paste it in a browser and a Welcome Page for nginx will be displayed.

# docker machine

https://blog.scottlowe.org/2017/11/24/using-docker-machine-kvm-libvirt/

Docker Machine is, in my opinion, a useful and underrated tool. 

You might be wondering if there’s any value in using Docker Machine to run a VM on Linux when you can just run Docker directly on the Linux host. I haven’t fully tested the idea yet, but my initial thought is that it would enable users to run various different versions of the Docker Engine (using the --engine-install-url option, as I outlined here). If you have other ideas where this sort of arrangement might have value, I’d love to hear them; hit me up on Twitter.


# QEMU VS KVM

https://www.packetcoders.io/what-is-the-difference-between-qemu-and-kvm/

## QEMU

QEMU is a userland type 2 (i.e runs upon a host OS) hypervisor for performing hardware virtualization (not to be confused with hardware-assisted virtualization), such as disk, network, VGA, PCI, USB, serial/parallel ports, etc. It is flexible in that **it can emulate CPUs via dynamic binary translation (DBT) allowing code written for a given processor to be executed on another (i.e ARM on x86, or PPC on ARM)**. Though QEMU can run on its own and emulate all of the virtual machine’s resources, **as all the emulation is performed in software it is extremely slow.**

## KVM

KVM is a Linux kernel module. It is a type 1 hypervisor that is a full virtualization solution for Linux on x86 hardware containing virtualization extensions (Intel VT or AMD-V)[1]. **But what is full virtualization, you may ask?** When a CPU is emulated (vCPU) by the hypervisor, the hypervisor has to translate the instructions meant for the vCPU to the physical CPU. **As you can imagine this has a massive performance impact**. To overcome this, modern processors support virtualization extensions, such as Intel VT-x and AMD-V. These technologies provide the ability for a slice of the **physical CPU to be directly mapped to the vCPU**. **Therefore the instructions meant for the vCPU can be directly executed on the physical CPU slice.[2]**

## summary

As previously mentioned, QEMU can run independently, but due to the emulation being performed entirely in software it is extremely slow. To overcome this, QEMU allows you to use KVM as an accelerator so that the physical CPU virtualization extensions can be used. So to conclude: QEMU is a type 2 hypervisor that runs within user space and performs virtual hardware emulation, whereas KVM is a type 1 hypervisor that runs in kernel space, that allows a user space program access to the hardware virtualization features of various processors.[3]

![](https://www.packetcoders.io/content/images/2020/01/image1.png)

# Switching from Minikube with VirtualBox to KVM

![](https://i.imgur.com/ufpYzG6.png)

## steps to switch

![](https://i.imgur.com/AmiaKgM.png)

## Restarting minikube
After stopping minikube you may run into an issue when trying to restart it.
```
Error starting host: Error starting stopped host: Error creating VM: virError(Code=55, Domain=19, Message='Requested operation is not valid: network 'minikube-net' is not active').
```
KVM will not autostart the minikube network. To instruct KVM to autostart it, run:
```
virsh net-autostart minikube-net
```
Start the stopped network:
```
virsh net-start minikube-net
```
You can see a list of networks with their status by running:
```
virsh net-list --all
```

# Jupyter and Django

install django extensions

```
pip install django-extensions
```

Add into settings.py

```
INSTALLED_APPS = (
____...
__)

if DEBUG:_
_____INSTALLED_APPS += [ 'django_extensions']
```
	    
Some use of django extensions
```
python manage.py shell_plus
#Run the enhanced django shell:
```

## Install ipython in dev server:
A powerful interactive shell and also A kernel for Jupyter. Also Prints sql

installation of shell_plus
```
pip install ipython --dev
```
```
python manage.py shell_plus --ipython --print-sql
```

Install jupyter notebook in dev server:

installation of jupyter
```
pip install jupyter
```

```
python manage.py shell_plus --notebook
```
	    
	    
# django wsgi
	    
https://djangodeconstructed.com/2018/02/15/how-a-request-becomes-a-response-diving-deeper-into-wsgi/
	    
![](https://i.imgur.com/uOfql2y.png)
![](https://i.imgur.com/B7p3Yu3.png)
![](https://i.imgur.com/tT9Tp4g.png)

https://www.toptal.com/python/pythons-wsgi-server-application-interface
### info
![](https://i.imgur.com/AAf6B1Y.png)

### info
![](https://i.imgur.com/xPCo5Fu.png)


# Python Generators/Coroutines/Async IO with examples - async

https://medium.com/analytics-vidhya/python-generators-coroutines-async-io-with-examples-28771b586578


## info

![](https://i.imgur.com/07MYzpb.png)

## info

![](https://i.imgur.com/rx9Ke8H.png)

## info

![](https://i.imgur.com/sUTVb0b.png)

## info

![](https://i.imgur.com/wsYXG66.png)
	    
	    
# yield 

![](https://i.imgur.com/v99gL2v.png)

## info

![](https://i.imgur.com/r2VUH6I.png)
	    
## info

![](https://i.imgur.com/BbmcNOb.png)

## info

![](https://i.imgur.com/zNlil34.png)

## info

https://stackabuse.com/python-async-await-tutorial/

![](https://i.imgur.com/Mdk41TO.png)

## info sync keyword

![](https://i.imgur.com/NZJhX0g.png)

## info yield from

![](https://i.imgur.com/zgQxwig.png)

## info

![](https://i.imgur.com/Wb9nw5E.png)

## Running the event loop

![](https://i.imgur.com/PWQojKC.png)

## info
![](https://i.imgur.com/JOZynbp.png)

## The asyncio module in Python

https://www.educative.io/edpresso/how-to-implement-async-await-in-python

![](https://i.imgur.com/tIuQHFb.png)

## info

![](https://i.imgur.com/WDkp6ng.png)

## info

![](https://i.imgur.com/8qmmkNi.png)

## async

https://arunrocks.com/a-guide-to-asgi-in-django-30-and-its-performance/

![](https://i.imgur.com/g5fxbwj.png)
	    
## info

![](https://i.imgur.com/mPFMrxx.png)

## info

![](https://i.imgur.com/x8a2THg.png)
	    
## info

![](https://i.imgur.com/EakCAD3.png)
	    
## info

![](https://i.imgur.com/nQ6Vaqr.png)

# django channels and rest auth

![](https://i.imgur.com/CylZ2X0.png)

## info
	    
https://florimond.dev/en/posts/2019/08/introduction-to-asgi-async-python-web/

![](https://i.imgur.com/Nny8lcn.png)

# from asgiref.sync import async_to_sync

https://blog.proximity.tech/steering-django-towards-an-async-world

![](https://i.imgur.com/Dm3vOkl.png)
	    
# await

https://www.aeracode.org/2018/02/19/python-async-simplified/

![](https://i.imgur.com/txdFAXr.png)
	    
## info
![](https://i.imgur.com/bt5RtKx.png)

## The event loop is really what makes everything possible, and without it, async Python would just be a super weird control flow with no actual speed benefits.

# Simplest async/await example possible in Python

This way it's possible to write code that works:

```
import asyncio

async def main():
    print('done!')

if __name__ ==  '__main__':
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
```


# async

![](https://i.imgur.com/QYRvPz5.png)

## info

![](https://i.imgur.com/3cry4Tl.png)

## info 
https://stackoverflow.com/questions/50757497/simplest-async-await-example-possible-in-python

![](https://i.imgur.com/6Q4BEsO.png)

## info

![](https://i.imgur.com/CDmZJux.png)

## info

https://www.integralist.co.uk/posts/python-asyncio/

![](https://i.imgur.com/mblFig4.png)

## info

![](https://i.imgur.com/hXOV1il.png)

## info

![](https://i.imgur.com/xSzYn3S.png)

## info

![](https://i.imgur.com/mVwFDxL.png)

## info

![](https://i.imgur.com/CpwyigS.png)

## info

![](https://i.imgur.com/5uUFYGH.png)
	    
	    
	    
# ws protocol does not work with nginx

in docker open port in webapp instead of using nginx proxy if we want websockets to work

	    
# What's the difference between KVM, QEMU and libvirt?

Qemu is the lowest level that emulates processor and peripherals. KVM is to accelerate it if the CPU has VT enabled. Libvirt provides a daemon and client to manipulate VMs for convenience. See also Difference between KVM and QEMU on Server Fault.

## answer 2

**Qemu** is a processor emulating virtualization software with many virtual devices support (such as HDD,RAM,sound,ethernet,USB,VGA , etc.)

**KVM** is a kernel module which allows passing through CPU cores via **host-passthrough** without virtualizing them. It also allows passing through PCI devices via **vfio-pci** kernel module. 

All these passthrough functionality are possible via **IOMMU** (Input output memory mapping unit), which maps real DMA addresses to virtualized addresses so direct access becomes possible and it brings bare-metal (native) performance. IOMMU is a mechanism which is part software in kernel and part hardware in chipsets, featured as **VT-D** (vmx) **AMD-VI** (svm). **SR-IOV** is a chipset feature which allows splitting one PCI device to many virtual ones without performance drop via parallelized direct IO access.

**Libvirt** is a library, allowing you to use python and other programming languages to configure virtual machines. **Virsh** is a toolkit which works in terminal to monitor and configure virtual machine settings. **Virt-manager** is VMware player like GUI as an alternative to virsh and it uses libvirt. 
	    
	    
# Kubernetes Basic modules

![](https://i.imgur.com/ZOzVHDY.png)

# Kubernets cluster

Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.

The abstractions in Kubernetes allow you to deploy containerized applications to a cluster without tying them specifically to individual machines

Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way.

# A Kubernetes cluster consists of two types of resources:

- The Control Plane coordinates the cluster
- Nodes are the workers that run applications

![](https://i.imgur.com/fCPWWaj.png)

# Control Plane

The Control Plane is responsible for managing the cluster. 

The Control Plane coordinates all activities in your cluster, such as scheduling applications, maintaining applications' desired state, scaling applications, and rolling out new updates.

# node

A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster. 

Each node has a Kubelet, which is an agent for managing the node and communicating with the Kubernetes control plane.

The node should also have tools for handling container operations, such as containerd or Docker.

# What is a Kubernetes Cluster?

A Kubernetes (K8s) cluster is a grouping of nodes that run containerized apps in an efficient, automated, distributed, and scalable manner.

https://www.weave.works/blog/kubernetes-cluster

# pod vs node

![](https://i.imgur.com/HrHAW0f.png)
