# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>Kunder</title>
<style>
body 	{font-family: "Gill Sans", "Gill Sans MT", "Myriad Pro", "DejaVu Sans Condensed", Helvetica, Arial, sans-serif;
		 font-size: 18px;}
table, tr, td, th {border: 1px solid black;}
td, th {padding: 10px;}
th {background-color: #7fcec9;}
input[type=submit] {background-color: #7fcec9; height: 30px; width: 50px; font-size: 14px;}
select {height: 30px; font-size: 14px;}
td {background-color: #f0f2f2;}
</style>
</head>

<body>
Tilbage til <a href="index.php">forsiden</a> // Se også <a href="projectlist.php">Projekter</a> //
<a href="addclient.php">Opret kunde</a> // <a href="updateclient.php">Opdater kunde</a><br>
<h1>Kunder</h1>
<!-- Tabelstart -->
<table>
<thead>
	<tr>
    	<!-- Tabeloverskrifter -->
		<th>ID</th>
		<th>Kunde</th>
		<th>Kontakt</th>
		<th>Tlf.nr.</th>
        <th>Adresse</th>
		<th>Postnr.</th>
	</tr>
</thead>
<?php
	require_once 'dbcon.php'; // Opret forbindelse til databasen
	// data hentes fra 'client' tabellen i databasen
	$sql = 'select Client_ID, Client_Name, 
	Client_Contact_Name, Client_Contact_Phone, Client_Adress, Zipcode_Zipcode 
	FROM client';
	$stmt = $link->prepare($sql);
	$stmt->execute();
	$stmt->bind_result($cid, $cname, $ccn, $ccph, $cad, $zip);
	while($stmt->fetch()){
	// data skrives ud i en tabel
		echo '<tr><td>' .$cid. '</td><td>' .$cname. '</td>
		<td>' .$ccn. '</td><td>' .$ccph. '</td><td>' .$cad. '</td><td>' .$zip. 
		'</td></tr>';
	}
?>
</table><br>
<!-- Tabelslut -->
<h3>Slet kunde</h3>
	<!-- 'form action' henter informationerne (bl.a. SQL statement 'DELETE FROM') 
    fra filen deleteclient_action.php, der gør det muligt at slette en kunde fra tabellen -->
	<form action="deleteclient_action.php" method="POST">
             <!-- Alle kundenavne der findes i tabellen 'client' hentes i en dropdown -->
            <select type="text" placeholder="Kunde" name="cname">
				<option value="select">Kundenavn</option>
				<?php
					$sql = 'select Client_ID, Client_Name 
							from client
							where Client_ID >3';
					$stmt = $link->prepare($sql);
					$stmt->bind_result($cid, $cname);
					$stmt->execute();
					while ($stmt->fetch()) {
					echo '	<option value="'.$cid.'">'.$cname.'</option>'.PHP_EOL;
					}
                ?>
            </select>
            <input type="submit" value="Slet">
	</form>
</body>
</html>
