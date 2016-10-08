# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<?php
require_once 'dbcon.php'; // Opret forbindelse til databasen

$cname = filter_input(INPUT_POST, 'cname') or die('noget gik galt ved indtastning af Kundenavn');
$ccn = filter_input(INPUT_POST, 'ccn') or die('noget gik galt ved indtastning af Kontaktperson');
$ccph = filter_input(INPUT_POST, 'ccph') or die('noget gik galt ved indtastning af Telefonnummer');
$cad = filter_input(INPUT_POST, 'cad') or die('noget gik galt ved indtastning af Adresse');
$zip = filter_input(INPUT_POST, 'zip', FILTER_VALIDATE_INT) or die('noget gik galt ved indtastning af Postnummer');

// tilføjer en ny kunde i tabellen 'client'
$sql = 'INSERT INTO client (Client_Name, Client_Contact_Name, Client_Contact_Phone, 
Client_Adress, Zipcode_Zipcode)
values (?, ?, ?, ?, ?)';

	$stmt = $link->prepare($sql); 
	$stmt->bind_param('ssisi', $cname, $ccn, $ccph, $cad, $zip);
	$stmt->execute();
		if ($stmt->affected_rows >0 ){
	echo 'Kunden er nu tilføjet kundekartoteket.<br><br>
	Tilbage til <a href="clientlist.php">Kunder</a><br><br>';
	}
	else {
	echo 'Der opstod en fejl.';
	}

	echo 'inserted '.$cname.' as id:'.($stmt->insert_id); // id for inserted record
?>
