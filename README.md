# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<?php
require_once 'dbcon.php'; // Opret forbindelse til databasen
?>
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>Ændring i kundeoplysninger</title>
<style>
body {font-family: "Gill Sans", "Gill Sans MT", "Myriad Pro", "DejaVu Sans Condensed", Helvetica, Arial, sans-serif;
	  font-size: 18px;}
input {height: 30px; font-size: 14px; margin-bottom: 5px;}
select {height: 30px; font-size: 14px; margin-bottom: 5px; width: 167px;}
input[type=submit] {background-color: #7fcec9; width: 100px; margin-top: 15px;}
</style>
</head>

<body>
Tilbage til <a href="index.php">forsiden</a> // Tilbage til <a href="clientlist.php">Kunder</a><br><br>
    <!-- 'form action' henter informationerne (bl.a. SQL statement 'UPDATE') 
    fra filen updateclient_action.php, der gør det muligt at ændre kundeoplysninger i tabellen -->
    <form action="updateclient_action.php" method="POST">
		<fieldset>
        	<legend>Lav ændringer i kundeoplysninger</legend>
            <!-- Alle kunder der findes i tabellen 'client' hentes i en dropdown -->
            <select type="text" placeholder="Kunde" name="cid">
				<option value="">Kunde</option>
				<?php
					$sql = 'select Client_ID, Client_Name 
							from client';
					$stmt = $link->prepare($sql);
					$stmt->bind_result($cid, $cname);
					$stmt->execute();
					while ($stmt->fetch()) {
					echo '	<option value="'.$cid.'">'.$cname.'</option>'.PHP_EOL;
					}
                ?>
            </select><br>
            <input type="text" placeholder="Adresse" name="cad"><br>
            <!-- Alle postnumre der findes i tabellen 'zipcode' hentes i en dropdown -->
            <select type="text" placeholder="Postnummer" name="zip">
				<option value="">Vælg postnr.</option>
				<?php
					$sql = 'select Zipcode FROM zipcode';
					$stmt = $link->prepare($sql);
					$stmt->bind_result($zip);
					$stmt->execute();
					while ($stmt->fetch()) {
					echo '	<option value="'.$zip.'">'.$zip.'</option>'.PHP_EOL;
					}
                ?>
            </select><br>
            <input type="submit" value="Tilføj ændring">
		</fieldset>
	</form>

</body>
</html>
