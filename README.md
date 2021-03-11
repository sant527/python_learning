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
