/*
    JavaScript | 表达式，类型准换
    根据这节课上讲师已写好的部分，补充写完函数 convertStringToNumber
    以及函数 convertNumberToString
*/

function convertStringToNumber(myString: string, hex: number = 10) {
    if (hex > 10) {
      return;
    }
    let flag = /e|E/.test(myString);
    if (!flag) {
      let chars: string[] = myString.split('');
      let number: number = 0;
      let i: number = 0;
      while (i < chars.length && chars[i] !== '.') {
        number = number * hex;
        number += chars[i].codePointAt(0) - '0'.codePointAt(0);
        i++;
      }
      if (chars[i] === '.') {
        i++;
      }
      let fraction = 1;
      while (i < chars.length) {
        fraction /= hex;
        number += (chars[i].codePointAt(0) - '0'.codePointAt(0)) * fraction;
        i++;
      }
      return number;
    } else {
      let logNumber = Number(myString.match(/\d+$/)[0]);
      let number: any = myString.match(/^[\d\.]+/)[0].replace(/\./, '');
      if (/e-|E-/.test(myString)) {
        return Number(number.padEnd(logNumber + 1, 0));
      } else {
        return Number(number.padStart(logNumber + number.length, 0).replace(/^0/, '0.'));
      }
    }
  }


function convertNumberToString(number, x = 10) {
    let integer = Math.floor(number);
    let decimal = number - integer;
    let string = !integer ? '0' : '';
    while (integer > 0) {
      string = `${integer % x}${string}`;
      integer = Math.floor(integer / x);
    }
  
    if (decimal) {
      string += '.';
      while (decimal && !/\.\d{20}$/.test(string)) {
        decimal *= x;
        string += `${Math.floor(decimal)}`;
        decimal -= Math.floor(decimal);
      }
    }
    return string;
}