# TP12 - Apache CXF SOAP Web Service

Projet de démonstration d'un service web SOAP avec Apache CXF, incluant la sécurité WS-Security.

## 📋 Description

Ce projet illustre la création d'un service web SOAP complet utilisant Apache CXF avec :
- Publication de services SOAP via JAX-WS
- Sérialisation XML avec JAXB
- Authentification WS-Security avec UsernameToken
- Client Java pour consommer le service

## 🏗️ Structure du Projet

```
src/main/java/com/acme/cxf/
├── model/
│   └── Person.java              # Modèle JAXB sérialisable
├── api/
│   └── HelloService.java        # Interface du contrat SOAP
├── impl/
│   └── HelloServiceImpl.java    # Implémentation du service
├── security/
│   └── UTPasswordCallback.java  # Validation des credentials
├── client/
│   └── ClientDemo.java          # Client de test
├── Server.java                  # Serveur SOAP standard
└── SecureServer.java            # Serveur SOAP sécurisé
```

## 🚀 Démarrage Rapide

### Prérequis
- Java 17+
- Maven 3.6+

### Lancer le serveur standard
```bash
mvn exec:java
```
Le service sera accessible à : `http://localhost:8080/services/hello`

WSDL : `http://localhost:8080/services/hello?wsdl`

### Lancer le client
```bash
mvn exec:java -Pclient
```

### Lancer le serveur sécurisé
```bash
mvn exec:java -Psecure
```
Le service sécurisé sera accessible à : `http://localhost:8080/services/hello-secure`

## 🔒 Sécurité WS-Security

Le serveur sécurisé requiert un UsernameToken pour l'authentification :
- **Utilisateur** : `student`
- **Mot de passe** : `secret123`
- **Type de mot de passe** : PasswordText

### Test avec SoapUI
1. Importer le WSDL : `http://localhost:8080/services/hello-secure?wsdl`
2. Configurer WS-Security → Add UsernameToken
3. Définir Username: `student`, Password: `secret123`, Password Type: Text
4. Envoyer la requête

## 📦 Dépendances Principales

- **Apache CXF** 4.0.3
  - cxf-rt-frontend-jaxws
  - cxf-rt-transports-http
  - cxf-rt-transports-http-jetty
  - cxf-rt-ws-security
- **Jakarta XML Bind API** 4.0.1
- **JAXB Implementation** 4.0.5
- **WSS4J** 3.0.1

## 🛠️ Opérations Disponibles

### SayHello
Retourne un message de salutation personnalisé.

**Requête** :
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
                  xmlns:api="http://api.cxf.acme.com/">
   <soapenv:Header/>
   <soapenv:Body>
      <api:SayHello>
         <name>ClientJava</name>
      </api:SayHello>
   </soapenv:Body>
</soapenv:Envelope>
```

### FindPerson
Retourne un objet Person complexe.

**Requête** :
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
                  xmlns:api="http://api.cxf.acme.com/">
   <soapenv:Header/>
   <soapenv:Body>
      <api:FindPerson>
         <id>P-777</id>
      </api:FindPerson>
   </soapenv:Body>
</soapenv:Envelope>
```

## 📝 Bonnes Pratiques

En production, il est recommandé de :
- Utiliser **PasswordDigest** au lieu de PasswordText
- Activer **HTTPS** pour le transport
- Ajouter la **signature** et le **chiffrement** des messages sensibles
- Utiliser un **keystore** pour les certificats

## 📄 Licence

Ce projet est un exemple éducatif.

## 👤 Auteur

3asma
