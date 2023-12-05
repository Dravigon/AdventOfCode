# Advent 2023 day 4 part 1

Question

[https://adventofcode.com/2023/day/4](https://adventofcode.com/2023/day/4)
Code:

```jsx
var regex = /Card\s+(\d+): ((\s*\d+)+) \| ((\s*\d+)+)/gm;

// Alternative syntax using RegExp constructor
// const regex = new RegExp('Card (\\d+): ((\\s*\\d+)+) \\| ((\\s*\\d+)+)', 'gm')

var str = ` --- advent string ---`;

str = `Card 1: 41 48 83 86 17 | 83 86  6 31 17  9 48 53
Card 2: 13 32 20 16 61 | 61 30 68 82 17 32 24 19
Card 3:  1 21 53 59 44 | 69 82 63 72 16 21 14  1
Card 4: 41 92 73 84 69 | 59 84 76 51 58  5 54 83
Card 5: 87 83 26 28 32 | 88 30 70 12 93 22 82 36
Card 6: 31 18 13 56 72 | 74 77 10 23 35 67 36 11
`;

var match = [...str.matchAll(regex)]
console.log(match)
var parseddata = match.map(data=>{return {'cardno':data[1],'winning':data[2].trim().split(' '),'mynumbers':data[4].trim().split(' ')}})

console.log(parseddata)

var cardWins = parseddata.map(data=>{
  let is_winning = data.mynumbers.filter(x=>{
    console.log((!!x)&&data.winning.indexOf(x)>=0,x,!!x,data.cardno)
    return (!!x)&&data.winning.indexOf(x)>=0;
  }
                                     
    
  )
  let point = Math.floor( Math.pow(2,is_winning.length-1))
  console.log(is_winning.length-1)
  return {'id':data.cardno,'point':point,'matches':is_winning}
})

console.log(cardWins)

var sum = cardWins.reduce((a,c)=>a+c.point,0)
console.log(sum)
```