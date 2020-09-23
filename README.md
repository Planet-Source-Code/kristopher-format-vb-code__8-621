<div align="center">

## Format VB Code


</div>

### Description

This PHP function takes Visual Basic source code as input, and then outputs a color-coded version of the source code in HTML. Great for sites that have code archives. Simply pull the code from your file or SQL database, run it through this function, and you have your easy to read, color-coded VB code in a second.
 
### More Info
 
Input is Visual Basic source code.

Returns color-coded source code in HTML format.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Kristopher](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kristopher.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Strings](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/strings__8-26.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kristopher-format-vb-code__8-621/archive/master.zip)





### Source Code

```
<?php
function format($code) {
$reserved = Array("Public", "Private", "Sub", "Dim", "As", "Integer", "End", "Me", "String", "Long", "Function", "Declare", "Lib", "ByVal", "With", "If", "Then", "Else", "Option", "Explicit", "Type", "Const", "Open", "Close", "Print", "Write", "As", "For", "Next", "To");
$numr = count($reserved);
$code = str_replace('(', ' ( ', $code);
$code = str_replace(')', ' ) ', $code);
$code = str_replace('.', ' . ', $code);
$code = str_replace("'", " ' ", $code);
$code = str_replace('"', ' " ', $code);
$code = str_replace(",", " , ", $code);
$lines = explode("\n", $code);
$numl = count($lines);
//for each line
for ($i = 0; $i < $numl; $i++) {
	$lines[$i] = str_replace("\r", '', $lines[$i]);
 $words = explode(' ', $lines[$i]);
 $numw = count($words);
 $line = '';
 //for each word
 for ($j = 0; $j < $numw; $j++) {
  $b = 0;
  //if it's a comment '
  if($words[$j] == "'") {
   $line = substr($line, 0, strlen($line) -1) . '<font color="#008800">' . "'";
   for ($m = $j + 1; $m < $numw; $m++) {
    $line = $line . $words[$m] . ' ';
   }
   $line = $line . "</font>";
   break;
  }
  //if it's a quote "
  if ($words[$j] == '"') {
   $line = substr($line, 0, strlen($line) -1) . $words[$j];
   if ($skip == 1) {
    $skip = 0;
   } else {
    $skip = 1;
   }
  } else {
   if ($skip == 0) { //if we're not skipping
   //for each reserved word
   for ($k = 0; $k < $numr; $k++) {
    if (strtolower(trim($words[$j])) == strtolower($reserved[$k])) {
     $b = 1;
     $line = $line . '<font color="#000088">' . $words[$j] . '</font> ';
     break;
    }
   }
   //if it's not in a comment
   if ($b != 1) {
    $line = $line . $words[$j];
    if(trim($words[$j]) != '"') {
     if(trim($words[$j]) != "'") {
      $line = $line . ' ';
     }
    }
   }
   } else {
    if (trim($words[$j]) == '"') {
     $line = trim($line) . '"';
    } else {
     $line = $line . $words[$j] . ' ';
    }
   }
  }
 }
 $fcode = $fcode . $line . "\n";
}
$fcode = str_replace(" ( ", "(", $fcode);
$fcode = str_replace(" ) ", ")", $fcode);
$fcode = str_replace(" . ", ".", $fcode);
$fcode = str_replace(" ' ", "'", $fcode);
$fcode = str_replace(" , ", ",", $fcode);
return '<pre style="background:#F4F4F4;">' . trim($fcode, "\n") . '</pre>';
}
?>
```

