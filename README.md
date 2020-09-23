﻿<div align="center">

## Database Search


</div>

### Description

This is a search engine script that lets you scan through various pages depending on what you put as the maximum query per page.
 
### More Info
 
just the basic mySQL stuff. (password, username, datbase, table, columns)

It displays your search results.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Todd Williams](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/todd-williams.md)
**Level**          |Intermediate
**User Rating**    |3.8 (19 globes from 5 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__8-5.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/todd-williams-database-search__8-312/archive/master.zip)

### API Declarations

This code is Open Source to everyone. I just request that you please give me credit on your webpage if you use my codes.


### Source Code

```
<html>
<head>
<title>Todd Williams: Database Search</title>
</head>
<body>
<p align="center">Database Search</p>
<?php
//*************************************
//** SEARCH SCRIPT BY: Todd Williams **
//*************************************
//*************************************
//**       CODE        **
//*************************************
$connection = mysql_connect("server.server.server","user","password");
if(!$connection){
echo "Couldn't make a connection!!!";
exit;
}
$db = mysql_select_db("database_name",$connection);
if(!$db) {
echo "The database disapeared!";
mysql_close($connection);
exit;
}
$max = 0;
$bmax = mysql_query("SELECT * from table WHERE columntobesearched like '%$search%'");
 while ($result = mysql_fetch_array($bmax)) {
$max++;
}
?>
<table border="0" cellspacing="0" width="100%">
<tr>
<td height="12" align="left" background="bg2.jpg" width="50%">
<?php
echo "<form action=\"search.php\" method=\"get\"><input type=\"text\" name=\"search\" value=\"$search\"><input type=\"submit\" value=\"Search\">";
echo "</td><td height=\"12\" align=\"right\" bgcolor=\"red\" width=\"50%\">";
echo "By: Todd Williams";
echo "<td height=\"12\" align=\"right\" background=\"bg2.jpg\" width=\"100%\" colspan=\"2\">";
echo "<center>Database Search returned $max items containing \"<i>$search</i>\".</center>";
echo "</td></tr></table></form>";
$maxresult = 10;
$sql_text = ("SELECT * from table WHERE columntobesearched like '%$search%'");
if (!$page) {
$page = 1;
 }
$backpage = $page - 1;
$nextpage = $page + 1;
$query = mysql_query($sql_text);
$start = ($maxresult * $page) - $maxresult;
$num_rows = mysql_num_rows($query);
if ($num_rows <= $maxresult) {
 $num_pages = 1;
} else if (($num_rows % $max result) == 0) { $num_pages = ($num_rows / $maxresult);
 } else {
 $num_pages = ($num_rows / $maxresult) + 1;
 }
$num_pages = (int) $num_pages;
 if (($page > $num_pages) || ($page < 0)) {
 error("You have specified an invalid page number");
 }
$sql_text = $sql_text . " LIMIT $start, $maxresult";
 $query = mysql_query($sql_text);
 if ($max>$maxresult)
 {
  echo "<center>- ";
  if ($backpage) {
  echo "<a href=\"search.php?search=$search&page=$backpage\">Prev</a>";
  } else {
  echo "Prev";
  }
  for ($i = 1; $i <= $num_pages; $i++) {
  if ($i != $page) {
  echo " <a href=\"search.php?search=$search&page=$i\">$i</a> ";
  } else {
  echo " $i ";
  }
  }
  if ($page != $num_pages) {
  echo "<a href=\"search.php?search=$search&page=$nextpage\">Next</a> -";
  } else {
  echo "Next -";
  }
  echo "</center>";
 }
?>
<table border="0" cellspacing="0" width="100%">
<?php
$a = $start + 1;
 while ($result = mysql_fetch_array($query)) {
?>
<tr>
<td height="12" align="left" background="bg2.jpg" width="70%">
<?php
printf("$a. <a href=\"%s\">", $result['linkcolumn']);
printf("%s </a></td><td align=\"right\" background=\"bg2.jpg\">", $result['namecolumn']);
printf("%s ", $result['authorcolumn']);
printf("</a>");
$a++;
?>
</td>
</tr>
<tr>
<td colspan="2">
<?php printf("%s <br>", $result['descriptioncolumn']); ?>
</td>
</tr>
<?php
}
echo "</table>";
 if ($max>$maxresult)
 {
  echo "<br><br><br><center>- ";
  if ($backpage) {
  echo "<a href=\"search.php?search=$search&page=$backpage\">Prev</a>";
  } else {
  echo "Prev";
  }
  for ($i = 1; $i <= $num_pages; $i++) {
  if ($i != $page) {
  echo " <a href=\"search.php?search=$search&page=$i\">$i</a> ";
  } else {
  echo " $i ";
  }
  }
  if ($page != $num_pages) {
  echo "<a href=\"search.php?search=$search&page=$nextpage\">Next</a> -";
  } else {
  echo "Next -";
  }
  echo "</center>";
 }
?>
</body>
</html>
```

