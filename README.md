# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<?php
require_once 'dbcon.php'; // Opret forbindelse til databasen

$cad = filter_input(INPUT_POST, 'cad') or die('noget gik galt');
$zip = filter_input(INPUT_POST, 'zip') or die('noget gik galt');
$cid = filter_input(INPUT_POST, 'cid') or die('noget gik galt');

// ændrer adresse og postnummer der er tilknyttet et specifikt kunde-id
$sql = "UPDATE client SET Client_Adress=?, Zipcode_Zipcode=? 
		WHERE Client_ID=?";

	$stmt = $link->prepare($sql); 
	$stmt->bind_param('sis', $cad, $zip, $cid);
	$stmt->execute();
	if ($stmt->affected_rows >0 ){
	echo 'Kundeoplysningerne er ændret.<br><br>
	Tilbage til <a href="clientlist.php">Kunder</a><br><br>';
	}
	else {
	echo 'Der opstod en fejl i forsøget på at ændre kundeoplysningerne. Prøv igen.';
	}
?>
