# Sample Model ea-s0001.owl README

## Setup

To use the SPARQL plugin in Protege for this ontology, you will need to configure Protege to use more memory than the default configuration.  If you do not, Protege freezes and outputs an error message about out of memory.

* Edit the [Protege installation direction]\run.bat file (for Windows)
* Edit the line executing the Java VM

    jre\bin\java -Xmx500M -Xms200M -Xss16M ...
* Remove the "-Xmx500M -Xms200M -Xss16M" parameters
* Add the "-XX:-UseGCOverheadLimit" parameter
* The new version should look like this

    jre\bin\java -XX:-UseGCOverheadLimit ...

## Sample SPARQL Queries

Get list of individuals of type application system (using IRI)

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
    PREFIX zmas: <https://raw.githubusercontent.com/zombiemaker/application-system-ontology/main/application-system.owl#>
    PREFIX zmea: <https://raw.githubusercontent.com/zombiemaker/enterprise-architecture-ontology/main/ea.owl#>
    SELECT ?subject
    WHERE { 
        ?subject rdf:type zmas:OWLClass_204b2cd0_342c_4d4f_85f1_9d2667c1190e
    }

Get list of individuals of type application system (using label)

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
    PREFIX zmas: <https://raw.githubusercontent.com/zombiemaker/application-system-ontology/main/application-system.owl#>
    PREFIX zmea: <https://raw.githubusercontent.com/zombiemaker/enterprise-architecture-ontology/main/ea.owl#>

    SELECT ?object
    WHERE { 
        ?object rdf:type $appsys .
        $appsys rdfs:label "application system"@en .
    }

Get individual with rdfs:label "dns application system"@en

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
    PREFIX zmas: <https://raw.githubusercontent.com/zombiemaker/application-system-ontology/main/application-system.owl#>
    PREFIX zmea: <https://raw.githubusercontent.com/zombiemaker/enterprise-architecture-ontology/main/ea.owl#>
    SELECT ?subject
    WHERE { 
        ?subject rdfs:label "dns application system"@en

    }


Get list of individuals that sends data to other individuals

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
    PREFIX zmas: <https://raw.githubusercontent.com/zombiemaker/application-system-ontology/main/application-system.owl#>
    PREFIX zmea: <https://raw.githubusercontent.com/zombiemaker/enterprise-architecture-ontology/main/ea.owl#>
    SELECT ?source ?destination
    WHERE { 
        ?source ?sends ?destination .
        ?sends rdfs:label "sends data to"@en

    }

Manually construct inverse relationships

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
    PREFIX zmas: <https://raw.githubusercontent.com/zombiemaker/application-system-ontology/main/application-system.owl#>
    PREFIX zmea: <https://raw.githubusercontent.com/zombiemaker/enterprise-architecture-ontology/main/ea.owl#>


    CONSTRUCT {
        ?destination ?receives ?source
    }
    WHERE { 
        ?source ?sends ?destination .
        ?sends rdfs:label "sends data to"@en .
        ?receives rdfs:label "receives data from"@en .
    }