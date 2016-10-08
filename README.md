# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>Projekter</title>
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

Tilbage til <a href="index.php">forsiden</a> // Se også <a href="clientlist.php">Kunder</a>
<h1>Projekter</h1>
<!-- Tabelstart -->
<table>
<thead>
	<tr>
    	<!-- Tabeloverskrifter -->
		<th>ID</th>
		<th>Projekt</th>
		<th>Beskrivelse</th>
		<th>I øvrigt</th>
        	<th>Startdato</th>
		<th>Slutdato</th>
        <th>Kunde</th>
        <th>Resource</th>
</thead>
<?php
	require_once 'dbcon.php'; // Opret forbindelse til databasen
	// data hentes fra 'project' tabellen i databasen
	$sql = 'select Project_ID, Project_Name, Project_Description, Other_Project_Details, 
	Project_Startdate, Project_Enddate, Client_Name, Resource_Name
	FROM project, client, resource
	WHERE Project_ID = Client_ID
	AND Resource_ID = 10';
	$stmt = $link->prepare($sql);
	$stmt->execute();
	$stmt->bind_result($pid, $pname, $pd, $opd, $pstart, $pend, $cname, $rname);
	while($stmt->fetch()){
	// data skrives ud i en tabel
		echo '<tr><td>' .$pid. '</td><td>' .$pname. '</td>
		<td>' .$pd. '</td><td>' .$opd. '</td><td>' .$pstart. '</td>
		<td>' .$pend. '</td><td><a href="clientlist.php">' .$cname. '</a></td>
		<td><a href="resourcelist.php">' .$rname. '</a></td></tr>';
	}
?>
</table>
<!-- Tabelslut -->
</body>
</html>
