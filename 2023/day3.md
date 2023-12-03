# Advent 2023 day 3

Question

[https://adventofcode.com/2023/day/3](https://adventofcode.com/2023/day/3)

Code:

```jsx
var str = `... advent string ...`

var symbol_regex = /[^\d\w\.\n]/gm;
var number_regex = /\d+/gm;

// test string
// str = `467..114..
// ...*......
// ..35..633.
// ......#...
// 617*......
// .....+.58.
// ..592.....
// ......755.
// ...$.*....
// .664.598..`

var str = `... advent string ...`

var symbol_regex = /[^\d\w\.\n]/gm;
var number_regex = /\d+/gm;

// test string
// str = `467..114..
// ...*......
// ..35..633.
// ......#...
// 617*......
// .....+.58.
// ..592.....
// ......755.
// ...$.*....
// .664.598..`

var str_len = str.split('\n')[0].length

console.log(str_len)

var symbol_matches = [...str.matchAll(symbol_regex)]
var number_matches = [...str.matchAll(number_regex)];

var gear_ratio = [];
var checked_array = number_matches.map((e, i) => {
  var main_index = i;

  var left_index = number_matches[main_index].index + number_matches[main_index][0].length
  var right_index = number_matches[main_index].index - 1



  var check_left_right = symbol_matches.find((val) => (val.index == right_index) || (val.index == left_index))
  var check_top_diagonal_left_right = symbol_matches.find(
    (val) => (val.index == right_index - str_len - 1) || (val.index == left_index - str_len - 1)
  )
  var check_bottom_diagonal_left_right = symbol_matches.find(
    (val) => (val.index == right_index + str_len + 1) || (val.index == left_index + str_len + 1)
  )

  var check_top = symbol_matches.find(
    (val) => (val.index > right_index - str_len - 1) && (val.index < left_index - str_len - 1)
  )
  var check_bottom = symbol_matches.find(
    (val) => (val.index > right_index + str_len + 1) && (val.index < left_index + str_len + 1)
  )

  var matched_symbol = check_left_right || check_top_diagonal_left_right || check_bottom_diagonal_left_right || check_top || check_bottom;

  if (matched_symbol && matched_symbol[0] == '*') {
    let val = gear_ratio[matched_symbol.index]
    if (val) {
      gear_ratio[matched_symbol.index] = {
        'mul_v': val.mul_v * Number(e[0]),
        'valid': true
      }
    } else {
      gear_ratio[matched_symbol.index] = {
        'mul_v': Number(e[0]),
        'valid': false
      }
    }
  }

  var is_valid = !!(check_left_right || check_top_diagonal_left_right || check_bottom_diagonal_left_right || check_top || check_bottom)

  //  !is_valid || console.log(Number(e[0]), check_left_right, check_top_diagonal_left_right, check_bottom_diagonal_left_right, check_top, check_bottom)



  return {
    'value': Number(e[0]),
    'is_valid': is_valid
  }

})


var sum = checked_array.reduce((acc, curr) => curr.is_valid ? acc + curr.value : acc, 0)
console.log('part 1: ',sum)

console.log('part 2:',gear_ratio.reduce((acc, curr) => curr.valid ? curr.mul_v + acc : acc, 0))
```