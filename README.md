# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>Ressourcer</title>
<style>
body {font-family: "Gill Sans", "Gill Sans MT", "Myriad Pro", "DejaVu Sans Condensed", Helvetica, Arial, sans-serif;
	  font-size: 18px;}
table, tr, td, th {border: 1px solid black;}
td, th {padding: 10px;}
th {background-color: #7fcec9;}
td {background-color: #f0f2f2;}
</style>
</head>

<body>

Tilbage til <a href="index.php">forsiden</a> // Tilbage til <a href="projectlist.php">projekter</a>
<h1>Ressourcer</h1>
<!-- Tabelstart -->
<table>
<thead>
	<tr>
    	<!-- Tabeloverskrifter -->
		<th>ID</th>
		<th>Ressourcenavn</th>
		<th>Detaljer</th>
		<th>Ressourcetype</th>
</thead>
<?php
	require_once 'dbcon.php'; // Opret forbindelse til databasen
	// data hentes fra 'project' tabellen i databasen
	$sql = 'select Resource_ID, Resource_Name, Other_Resource_Details, Resource_Type_Name from resource, resource_type
	WHERE Resource_Type_Resource_Type_Code = Resource_Type_Code';
	$stmt = $link->prepare($sql);
	$stmt->execute();
	$stmt->bind_result($rid, $rname, $ord, $rtname);
	while($stmt->fetch()){
	// data skrives ud i en tabel
		echo '<tr><td>' .$rid. '</td><td>' .$rname. '</td>
		<td>' .$ord. '</td><td>' .$rtname. '</td></tr>';
	}
?>
</table>
<!-- Tabelslut -->
</body>
</html>
