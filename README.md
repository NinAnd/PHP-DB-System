# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<?php
require_once 'dbcon.php'; // Opret forbindelse til databasen

$cname = filter_input(INPUT_POST, 'cname') or die('noget gik galt');
// sletter alle data tilknyttet et specifikt 'Client_Name'
$sql = 'DELETE FROM client 
		WHERE Client_Name=?';

	$stmt = $link->prepare($sql); 
	$stmt->bind_param('s', $cname);
	$stmt->execute();
	if ($stmt->affected_rows >0 ){
	echo 'Kunde er slettet';
	}
	else {
	echo 'Der opstod en fejl';
}
?>
