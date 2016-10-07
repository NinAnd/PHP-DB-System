# PHP-DB-System
Semester 3: Modul 2, opgave 3.

-- MySQL dump 10.13  Distrib 5.6.23, for Win64 (x86_64)
--
-- Host: 127.0.0.1    Database: client_project
-- ------------------------------------------------------
-- Server version	5.5.5-10.1.16-MariaDB

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `client`
--

DROP TABLE IF EXISTS `client`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `client` (
  `Client_ID` int(11) NOT NULL AUTO_INCREMENT,
  `Client_Name` varchar(45) NOT NULL,
  `Client_Adress` varchar(45) NOT NULL,
  `Client_Contact_Name` varchar(45) NOT NULL,
  `Client_Contact_Phone` varchar(45) NOT NULL,
  `Zipcode_Zipcode` int(11) NOT NULL,
  PRIMARY KEY (`Client_ID`),
  KEY `fk_Client_Zipcode_idx` (`Zipcode_Zipcode`),
  CONSTRAINT `fk_Client_Zipcode` FOREIGN KEY (`Zipcode_Zipcode`) REFERENCES `zipcode` (`Zipcode`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `client`
--

LOCK TABLES `client` WRITE;
/*!40000 ALTER TABLE `client` DISABLE KEYS */;
INSERT INTO `client` VALUES (1,'Pouls Grillbar','Burgervej 6','Poul Madsen','23456789',2400),(2,'LoveLand','Kærlighedsvej 69','Lady Love','88888888',4800),(3,'Kollektivet','Fælleskabs Allé 10','Buster Grav','12345678',2900),(4,'HusK','Fuglegade 67','Hanne Usk','11223344',2920),(8,'Kulturstyrelsen','Afrikavej 76','Gorm Gammelgaard','99001234',2000),(9,'Gertruds Blomster','Violvej 23','Gertrud','77665544',4800);
/*!40000 ALTER TABLE `client` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `client_has_project`
--

DROP TABLE IF EXISTS `client_has_project`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `client_has_project` (
  `Client_Client_ID` int(11) NOT NULL,
  `Project_Project_ID` int(11) NOT NULL,
  PRIMARY KEY (`Client_Client_ID`,`Project_Project_ID`),
  KEY `fk_Client_has_Project_Project1_idx` (`Project_Project_ID`),
  KEY `fk_Client_has_Project_Client1_idx` (`Client_Client_ID`),
  CONSTRAINT `fk_Client_has_Project_Client1` FOREIGN KEY (`Client_Client_ID`) REFERENCES `client` (`Client_ID`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  CONSTRAINT `fk_Client_has_Project_Project1` FOREIGN KEY (`Project_Project_ID`) REFERENCES `project` (`Project_ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `client_has_project`
--

LOCK TABLES `client_has_project` WRITE;
/*!40000 ALTER TABLE `client_has_project` DISABLE KEYS */;
/*!40000 ALTER TABLE `client_has_project` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `project`
--

DROP TABLE IF EXISTS `project`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `project` (
  `Project_ID` int(11) NOT NULL AUTO_INCREMENT,
  `Project_Name` varchar(45) NOT NULL,
  `Project_Description` varchar(100) NOT NULL,
  `Project_Startdate` date NOT NULL,
  `Project_Enddate` date NOT NULL,
  `Other_Project_Details` text NOT NULL,
  PRIMARY KEY (`Project_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `project`
--

LOCK TABLES `project` WRITE;
/*!40000 ALTER TABLE `project` DISABLE KEYS */;
INSERT INTO `project` VALUES (1,'Pouls hjemmeside','Website inkl. tidsbestilling','2016-10-09','2016-10-27','Skal holdes i rolige farver'),(2,'LoveLands World','Website og visuel identitet','2016-10-31','2016-11-16','Gerne fyldt med stærke farver'),(3,'Kollektiv Forum','Database over alle kollektiver i Danmark','2016-11-17','2016-12-05','Skal give et indtryk af fred, harmoni og fællesskab');
/*!40000 ALTER TABLE `project` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `project_has_resource`
--

DROP TABLE IF EXISTS `project_has_resource`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `project_has_resource` (
  `Project_Project_ID` int(11) NOT NULL,
  `Resource_Resource_ID` int(11) NOT NULL,
  `From_Date_Time` date DEFAULT NULL,
  `To_Date_Time` date DEFAULT NULL,
  `Hourly_Usage_Rate` decimal(6,0) DEFAULT NULL,
  PRIMARY KEY (`Project_Project_ID`,`Resource_Resource_ID`),
  KEY `fk_Project_has_Resource_Resource1_idx` (`Resource_Resource_ID`),
  KEY `fk_Project_has_Resource_Project1_idx` (`Project_Project_ID`),
  CONSTRAINT `fk_Project_has_Resource_Project1` FOREIGN KEY (`Project_Project_ID`) REFERENCES `project` (`Project_ID`) ON DELETE NO ACTION ON UPDATE NO ACTION,
  CONSTRAINT `fk_Project_has_Resource_Resource1` FOREIGN KEY (`Resource_Resource_ID`) REFERENCES `resource` (`Resource_ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `project_has_resource`
--

LOCK TABLES `project_has_resource` WRITE;
/*!40000 ALTER TABLE `project_has_resource` DISABLE KEYS */;
/*!40000 ALTER TABLE `project_has_resource` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `resource`
--

DROP TABLE IF EXISTS `resource`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `resource` (
  `Resource_ID` int(11) NOT NULL,
  `Resource_Name` varchar(45) DEFAULT NULL,
  `Other_Resource_Details` text,
  `Resource_Type_Resource_Type_Code` int(11) NOT NULL,
  PRIMARY KEY (`Resource_ID`),
  KEY `fk_Resource_Resource_Type1_idx` (`Resource_Type_Resource_Type_Code`),
  CONSTRAINT `fk_Resource_Resource_Type1` FOREIGN KEY (`Resource_Type_Resource_Type_Code`) REFERENCES `resource_type` (`Resource_Type_Code`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `resource`
--

LOCK TABLES `resource` WRITE;
/*!40000 ALTER TABLE `resource` DISABLE KEYS */;
INSERT INTO `resource` VALUES (1,'Katja','God til layout',2),(2,'Troels','God til logodesign',1),(3,'Huemac','Kan alt indenfor Backend',0),(4,'Mads','JavaScript ekspert',3),(8,'Sille','Særligt god til baggrundsdesign',1),(10,'Nanna','God til HTML og CSS',3);
/*!40000 ALTER TABLE `resource` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `resource_type`
--

DROP TABLE IF EXISTS `resource_type`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `resource_type` (
  `Resource_Type_Code` int(11) NOT NULL,
  `Resource_Type_Name` varchar(45) NOT NULL,
  PRIMARY KEY (`Resource_Type_Code`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `resource_type`
--

LOCK TABLES `resource_type` WRITE;
/*!40000 ALTER TABLE `resource_type` DISABLE KEYS */;
INSERT INTO `resource_type` VALUES (0,'Backend'),(1,'Illustrator'),(2,'Grafiker'),(3,'Frontend');
/*!40000 ALTER TABLE `resource_type` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `zipcode`
--

DROP TABLE IF EXISTS `zipcode`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `zipcode` (
  `Zipcode` int(11) NOT NULL,
  `City` varchar(45) NOT NULL,
  PRIMARY KEY (`Zipcode`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `zipcode`
--

LOCK TABLES `zipcode` WRITE;
/*!40000 ALTER TABLE `zipcode` DISABLE KEYS */;
INSERT INTO `zipcode` VALUES (1000,'København K'),(1050,'København K'),(1208,'København K'),(2000,'Frederiksberg'),(2100,'København Ø'),(2200,'København N'),(2300,'København S'),(2400,'København NV'),(2800,'Lyngby'),(2900,'Hellerup'),(2920,'Charlottenlund'),(3000,'Helsingør'),(4000,'Roskilde'),(4200,'Slagelse'),(4800,'Nykøbing F'),(4930,'Maribo'),(5000,'Odense C'),(6000,'Kolding'),(7000,'Fredericia'),(7400,'Herning'),(8000,'Aahus C'),(9000,'Aalborg');
/*!40000 ALTER TABLE `zipcode` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2016-10-07 12:52:29
