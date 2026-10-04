# Data Model

## Liste des entitées

### Db A
**User** : Classe abstraite representant les utilisateurs de DigiFeet\
**Patient** : Claase representant un patient utilisant le dispositif DigiFeet\
**Practitioner**: Classe representant un practitiens utilisant DigiFeet\
**FeetHistory**: Classe representant un antécedent de l'un des pied d'un patient\
**ClinicalAlert**: Classe representant les alertes remontées par DigiFeet

### Db B (Continuous data)
**FootData**: Classe representant l'ensemble des donnée récupérer sur un pied\
**SensorData**": Classe representant les données horodatée des pieds d'un patient\

## Diagramme de Classe

```mermaid
classDiagram
    namespace DbA {
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
            
            %% info cliniques
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
            string notes
        }

        class Practitioner {
        }

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
    }
    User <-- Patient: inherits
    FeetHistory "1" --> "*" Patient
    User <-- Practitioner: inherits
    Patient "1" --> "*" Practitioner
    ClinicalAlert "1" --> "*" Patient

    namespace DbB {
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
    }
    FootData "1" --> "2" SensorData
    SensorData "1"--> "*" Patient


```
