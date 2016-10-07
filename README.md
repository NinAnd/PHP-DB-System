# PHP-DB-System
Semester 3: Modul 2, opgave 3.

<?php
require_once 'dbcon.php'; // Opret forbindelse til databasen
?>
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>Tilføj ny kunde</title>
<style>
body {font-family: "Gill Sans", "Gill Sans MT", "Myriad Pro", "DejaVu Sans Condensed", Helvetica, Arial, sans-serif;}
</style>
</head>

<body>
<!-- Links til de andre sider -->
Tilbage til <a href="index.php">forsiden</a> | Tilbage til <a href="clientlist.php">Kunder</a><br><br>
	<!-- 'form action' henter informationerne (bl.a. SQL statement 'INSERT INTO') 
    fra filen addclient_action.php, der gør det muligt at tilføje en ny kunde til tabellen -->
    <form action="addclient_action.php" method="POST">
		<fieldset>
        	<legend>Tilføj ny kunde</legend>
            <input type="text" placeholder="Navn" name="cname"><br>
            <input type="text" placeholder="Kontaktperson" name="ccn"><br>
            <input type="text" placeholder="Telefonnummer" name="ccph"><br>
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
            <input type="submit" value="Tilføj">
		</fieldset>
	</form>

</body>
</html>
