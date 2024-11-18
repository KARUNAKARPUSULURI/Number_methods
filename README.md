# Number_methods
1.ParseInt()
const fontSize = "42.664634asdasd123123";
console.log(parseInt(fontSize)) 

const a = "asd"
console.log(Number(a))

2.ParseFloat()

const userInput = prompt("Enter the Number: "); //"42.123ad"
// +, Number, pars3
console.log(typeof Number(userInput))
console.log(Number(userInput))
console.log(parseInt(userInput))
console.log(parseFloat(userInput))
console.log(typeof Number(userInput))
console.log(typeof parseInt(userInput))
console.log(typeof parseFloat(userInput))

3.toFixed()

4.toPrecision()

const input = "42.123123asdasda"
// console.log(typeof input.toFixed()) //
// console.log(input.toFixed(0)) //
// console.log(input.toFixed(2)) //
console.log(typeof input.toPrecision(5)) //

5.isNaN()
const a = 2
const b = "asd2"
const c = a - b //NaN
NaN
console.log(isNaN(a))  //false
console.log(isNaN(b))  //true\
// if(!isNaN(NaN)){
//     console.log("")
// }
// if(isNaN(a) || isNaN(b) && str == " "){
    
// }
// validations-> checkings -> 
// password:- asdjhabd332

//IsInteger()
//IsFinite()