# Data Model

## Liste des entitées

**User** : Classe abstraite representant les utilisateurs de DigiFeet\
**Patient** : Claase representant un patient utilisant le dispositif DigiFeet\
**Practitioner**: Classe representant un practitiens utilisant DigiFeet\
**FeetHistory**: Classe representant un antécedent de l'un des pied d'un patient\
**FootData**: Classe representant l'ensemble des donnée récupérer sur un pied\
**SensorData**": Classe representant les données horodatée des pieds d'un patient\
**ClinicalAlert**: Classe representant les alertes remontées par DigiFeet

## Diagramme de Classe

```mermaid
classDiagram
    class User {
        <<abstract>>
        guid id

        string FirstName
        string LastName
        string Mail
        string PhoneNumber

    }

    class Patient {
        %% Identité
        int Age
        string Sex
        double HeighInCm
        double WeightInKg
        
        %% JSP
        timestamp DeviceStart
        timestamp FirstDiagnostic
        double GlycemieLevel
        int LeftFootGrade
        int RightFootGrade
        string Diagnistic
        int tabac
        double EGFR
        int amputation
        string jgerison 
        %% jour de gerision?
        double AnkleBrachialIndex
        double TcP02
        bool Neuropath
        bool Charcot
        bool dialyse
        bool deform
        bool artherio
        bool solo
        string 
        FootAnomalies[] history
    }
    User <-- Patient : inherits

    class Practitioner {
    }
    User <-- Practitioner: inherits
    Patient "1" --> "*" Practitioner

    class FeetHistory {
        timestamp dateTime
        Shape Shape

        string type
        string[] sensorArray
        sting[] sensorZoneName
        
        %% sinbad
        string site
        string[][] selectionTable
        string[] SelectionDepth
        int sinbadScore
        int siteValue
        bool isChemie
        bool isNeuropathie
        bool isSuperficial
        bool isInfection
        double depth
    }
    FeetHistory "1" --> "*" Patient

    class FootData {
        double[] PressureValuesInKPa
        double[] PressureValuesInNewton
        double[]TemperatureInCelcius
    }

    class SensorData {
        timestamp dateTime
        int seq
        int protocolVersion

        FootData left
        FootData right
    }
    FootData "1" --> "2" SensorData
    SensorData "1"--> "*" Patient

    class ClinicalAlert {
        Guid id

        string type
        string severity
        string footSide
        int zoneIndex
        string sensor

        double value
        double threshold
        double durationInMs'
        double firstSeenInMs
        doublelastSeenInMd

        string title
        string message
        string recommandation
        string disclaimer
    }
    ClinicalAlert "1" --> "*" Patient

```