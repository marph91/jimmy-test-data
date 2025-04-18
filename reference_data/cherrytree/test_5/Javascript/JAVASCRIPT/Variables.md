**Scope of the Variable :** 

var user="Gokul";
{
    let user="Martin";    //within scope can access
    const  lastname="S"   //within scope can access
    console.log(user);
}
console.log(user);
console.log(user);
console.log(lastname);

**Redeclaration of Variables :** 

var a=10;
console.log(a);     // 10
var a =20;              
console.log(a);       //  20

let b=10;                       
const c=20;
console.log(b);         //10
console.log(b);        //  20

**Value reassign :**

var d=10;
d=11;              
console.log(d);
let e=10;
e=11;
console.log(e);
const f=20;
f=30;                  // cant reassign `const` like this
console.log(f);

**Object is assigned as a values  for const we can change the values**

const college={"name":"gokul","age":11};
console.log(college);
console.log(college.name);
college.name="Hari"
console.log(college);





