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


