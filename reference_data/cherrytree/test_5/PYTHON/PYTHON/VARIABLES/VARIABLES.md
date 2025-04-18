x = 5
y = “John”

print(type(x))

print(type(y))   =>  used to print variable type


**Assign Multiple value**

x , y , z  = “Orange ” , “Apple  ”  ,  “Mango ”

print(x)
print(y)
print(z)

**Output Variable**

print(x)



Either we can mention Global keyword to make the variable global

x= "Python"

def func():
    print(x)

def func2():
    print(x)
    global y
    y ="Change"
    print(y)
func()
func2()

